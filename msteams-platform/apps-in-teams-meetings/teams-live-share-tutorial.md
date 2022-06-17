---
title: Руководство по коду Live Share
description: В этом модуле вы узнаете, как приступить к работе с пакетом SDK Live Share и как с помощью пакета SDK Live Share создать пример приложения Dice Roller
ms.topic: concept
ms.localizationpriority: high
ms.author: stevenic
ms.openlocfilehash: b13b37c73760d18cc11f30afca989c34ba1c1bb8
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143566"
---
---

# <a name="dice-roller-code-tutorial"></a>Руководство по коду Dice Roller

В примере приложения Dice Roller пользователям демонстрируется игральная кость с кнопкой для ее вращения. При вращении игральной кости пакет SDK Live Share использует Fluid Framework для синхронизации данных между клиентами, чтобы все увидели одинаковый результат. Чтобы синхронизировать данные, выполните следующие действия в файле [app.js](https://github.com/microsoft/live-share-sdk/blob/main/samples/01.dice-roller/src/app.js).

1. [Настройка приложения](#set-up-the-application)
2. [Присоединение к контейнеру Fluid](#join-a-fluid-container)
3. [Запись представления стадий](#write-the-stage-view)
4. [Подключение представления стадий к данным Fluid](#connect-stage-view-to-fluid-data)
5. [Запись представления боковой панели](#write-the-side-panel-view)
6. [Запись представления параметров](#write-the-settings-view)

:::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="Пример DiceRoller":::

## <a name="set-up-the-application"></a>Настройка приложения

Начните с импорта необходимых модулей. В примере используются [SharedMap DDS](https://fluidframework.com/docs/data-structures/map/) из Fluid Framework и [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient) из пакета SDK Live Share. Этот пример поддерживает возможности расширения собраний Teams, поэтому нам потребуется включить [пакет SDK клиента Teams](https://github.com/OfficeDev/microsoft-teams-library-js). Наконец, пример предназначен как для локального запуска, так и для запуска в собрании Teams, поэтому нам потребуется включить дополнительные элементы Fluid Framework, необходимые для [локального тестирования примера](https://fluidframework.com/docs/testing/testing/#azure-fluid-relay-as-an-abstraction-for-tinylicious).
  
Приложения создают контейнеры Fluid с помощью схемы, определяющей набор *начальных объектов*, которые будут доступны контейнеру. В примере используется SharedMap для хранения последнего значения прокрученной игральной кости. Дополнительные сведения см. в разделе [Моделирование данных](https://fluidframework.com/docs/build/data-modeling/).

Приложениям для собраний Teams требуется несколько представлений (содержимое, конфигурация и сцена). Мы создадим функцию `start()`, которая поможет определить представление для отрисовки и выполнить любую требуемую инициализацию. Мы хотим, чтобы наше приложение запускалось локально в веб-браузере и из собрания Teams, поэтому функция `start()` ищет параметр запроса `inTeams=true` для определения того, запущено ли оно в Teams. При запуске в Teams ваше приложение должно вызывать `app.initialize()` перед вызовом любых других методов teams-js.

В дополнение к параметру запроса `inTeams=true` можно использовать параметр запроса `view=content|config|stage`, чтобы определить представление, которое необходимо отрисовать.

```js
import { SharedMap } from "fluid-framework";
import { TeamsFluidClient } from "@microsoft/live-share";
import { app, pages } from "@microsoft/teams-js";
import { LOCAL_MODE_TENANT_ID } from "@fluidframework/azure-client";
import { InsecureTokenProvider } from "@fluidframework/test-client-utils";

const searchParams = new URL(window.location).searchParams;
const root = document.getElementById("content");

// Define container schema

const diceValueKey = "dice-value-key";

const containerSchema = {
  initialObjects: { diceMap: SharedMap }
};

function onContainerFirstCreated(container) {
  // Set initial state of the rolled dice to 1.
  container.initialObjects.diceMap.set(diceValueKey, 1);
}


// STARTUP LOGIC

async function start() {

  // Check for page to display
  let view = searchParams.get('view') || 'stage';

  // Check if we are running on stage.
  if (!!searchParams.get('inTeams')) {

    // Initialize teams app
    await app.initialize();

    // Get our frameContext from context of our app in Teams
    const context = await app.getContext();
    if (context.page.frameContext == 'meetingStage') {
      view = 'stage';
    }
  }

  // Load the requested view
  switch (view) {
    case 'content':
      renderSidePanel(root);
      break;
    case 'config':
      renderSettings(root);
      break;
    case 'stage':
    default:
      const { container } = await joinContainer();
      renderStage(container.initialObjects.diceMap, root);
      break;
  }
}

start().catch((error) => console.error(error));
```

## <a name="join-a-fluid-container"></a>Присоединение к контейнеру Fluid

Не все представления приложений должны поддерживать совместную работу. Представлению `stage` *всегда* требуются функции совместной работы, представлению `content` *могут* требоваться функции совместной работы, а представлению `config` *никогда* не требуются функции совместной работы. В случае представлений, которым требуются функции совместной работы, необходимо присоединиться к контейнеру Fluid, связанному с текущим собранием.

Присоединение контейнера к собранию выполняется очень просто: создается новый объект [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient) с последующим вызовом метода [joinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer).  При локальном запуске необходимо передать настраиваемую конфигурацию подключения с помощью специального `LOCAL_MODE_TENANT_ID`. В противном случае присоединение локального контейнера аналогично присоединению контейнера в Teams.

```js
async function joinContainer() {
  // Are we running in teams?
  let client;
  if (!!searchParams.get('inTeams')) {
      // Create client
      client = new TeamsFluidClient();
  } else {
      // Create client and configure for testing
      client = new TeamsFluidClient({
        connection: {
          tenantId: LOCAL_MODE_TENANT_ID,
          tokenProvider: new InsecureTokenProvider("", { id: "123", name: "Test User" }),
          orderer: "http://localhost:7070",
          storage: "http://localhost:7070",
        }
      });
  }

  // Join container
  return await client.joinContainer(containerSchema, onContainerFirstCreated);
}
```

> [!NOTE]
> При локальном тестировании TeamsFluidClient обновляет URL-адрес браузера, чтобы он содержал идентификатор созданного тестового контейнера. Копирование этой ссылки на другие вкладки браузера приводит к присоединению TeamsFluidClient к созданному тестовому контейнеру. Если изменение URL-адреса приложения мешает работе приложения, стратегию, которая используется для хранения идентификатора тестовых контейнеров, можно настроить с помощью параметров [setLocalTestContainerId](/javascript/api/@microsoft/live-share/iteamsfluidclientoptions#@microsoft-live-share-iteamsfluidclientoptions-setlocaltestcontainerid) и [getLocalTestContainerId](/javascript/api/@microsoft/live-share/iteamsfluidclientoptions#@microsoft-live-share-iteamsfluidclientoptions-getlocaltestcontainerid), передаваемых для TeamsFluidClient.

## <a name="write-the-stage-view"></a>Запись представления стадий

Многие приложения для расширения собраний Teams предназначены для использования React в качестве платформы представления, но это не обязательно. Например, в этом примере используются стандартные методы HTML/DOM для отрисовки представления.

### <a name="start-with-a-static-view"></a>Начало со статического представления

Вы можете легко создать представление с использованием локальных данных без функций Fluid, а затем добавить функции Fluid, изменив некоторые ключевые части приложения.

Функция `renderStage` добавляет `stageTemplate` к передаваемому HTML-элементу и создает рабочий инструмент прокрутки игральной кости со случайным значением кости при каждом нажатии кнопки **Roll** (Прокрутить). `diceMap` используется в следующих нескольких действиях.

```js
const stageTemplate = document.createElement("template");

stageTemplate["innerHTML"] = `
  <div class="wrapper">
    <div class="dice"></div>
    <button class="roll"> Roll </button>
  </div>
`
function renderStage(diceMap, elem) {
    elem.appendChild(stageTemplate.content.cloneNode(true));
    const rollButton = elem.querySelector(".roll");
    const dice = elem.querySelector(".dice");

    rollButton.onclick = () => updateDice(Math.floor(Math.random() * 6)+1);

    const updateDice = (value) => {
        // Unicode 0x2680-0x2685 are the sides of a die (⚀⚁⚂⚃⚄⚅).
        dice.textContent = String.fromCodePoint(0x267f + value);
    };
    updateDice(1);
}
```

## <a name="connect-stage-view-to-fluid-data"></a>Подключение представления стадий к данным Fluid

### <a name="modify-fluid-data"></a>Изменение данных Fluid

Чтобы начать использовать Fluid в приложении, первым делом нужно изменить действие, выполняемое при выборе пользователем `rollButton`. Вместо обновления локального состояния напрямую кнопка обновляет число, хранящееся в ключе `value` переданного `diceMap`. Так как `diceMap` является параметром `SharedMap` Fluid, изменения распространяются на все клиенты. Любые изменения в `diceMap` приведут к возникновению события `valueChanged`, а обработчик событий может инициировать обновление представления.

Этот шаблон распространен во Fluid, так как позволяет представлению действовать одинаково при локальных и удаленных изменениях.

```js
    rollButton.onclick = () => diceMap.set("dice-value-key", Math.floor(Math.random() * 6)+1);
```

### <a name="rely-on-fluid-data"></a>Использование данных Fluid

Следующее изменение, которое необходимо внести — изменение функции `updateDice`, чтобы она больше не принимала произвольное значение. Это означает, что приложение больше не может напрямую изменять локальное значение игральной кости. Вместо этого значение извлекается из `SharedMap` при каждом вызове `updateDice`.

```js
    const updateDice = () => {
        const diceValue = diceMap.get("dice-value-key");
        dice.textContent = String.fromCodePoint(0x267f + diceValue);
    };
    updateDice();
```

### <a name="handle-remote-changes"></a>Обработка удаленных изменений

Значения, возвращаемые из `diceMap`, являются только моментальным снимком во времени. Чтобы поддерживать данные в актуальном состоянии при их изменении, обработчик событий должен быть настроен в `diceMap` на вызов `updateDice` при каждой отправке события `valueChanged`. Чтобы получить список возникших событий и значения, переданные этим событиям, см. раздел [SharedMap](https://fluidframework.com/docs/data-structures/map/).

```js
    diceMap.on("valueChanged", updateDice);
```

## <a name="write-the-side-panel-view"></a>Запись представления боковой панели

Представление боковой панели, загруженное с помощью вкладки `contentUrl` с контекстом фрейма `sidePanel`, отображается пользователю на боковой панели, когда он открывает ваше приложение на собрании. Цель этого представления — разрешить пользователю выбирать содержимое приложения перед демонстрацией приложения на сцене собрания. Для приложений пакета SDK Live Share представление боковой панели также можно использовать в качестве вспомогательного интерфейса приложения. Вызов [joinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer) из представления боковой панели подключается к тому же контейнеру Fluid, к которому подключено представление стадий. Затем этот контейнер можно использовать для взаимодействия с представлением стадий. Убедитесь, что вы взаимодействуете с представлением стадий *и* представлением боковой панели всех пользователей.

В представлении боковой панели примера пользователю предлагается нажать кнопку демонстрации на сцене.

```js
const sidePanelTemplate = document.createElement("template");

sidePanelTemplate["innerHTML"] = `
  <style>
    .wrapper { text-align: center }
    .title { font-size: large; font-weight: bolder; }
    .text { font-size: medium; }
  </style>
  <div class="wrapper">
    <p class="title">Lets get started</p>
    <p class="text">Press the share to stage button to share Dice Roller to the meeting stage.</p>
  </div>
`;

function renderSidePanel(elem) {
    elem.appendChild(sidePanelTemplate.content.cloneNode(true));
}
```

## <a name="write-the-settings-view"></a>Запись представления параметров

Представление параметров, загруженное посредством `configurationUrl` в манифесте приложения, отображается пользователю, когда он впервые добавляет ваше приложение в собрание Teams. Это представление позволяет разработчику настроить `contentUrl` для вкладки, закрепленной на собрании с учетом введенных пользователем данных. Эта страница в настоящее время является обязательной, даже если для настройки `contentUrl` не требуется ввод данных пользователем.

> [!Important]
> [joinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer) пакета SDK Live Share не поддерживается в контексте вкладки `settings`.

В представлении параметров примера пользователю предлагается нажать кнопку "Сохранить".

```js
const settingsTemplate = document.createElement("template");

settingsTemplate["innerHTML"] = `
  <style>
    .wrapper { text-align: center }
    .title { font-size: large; font-weight: bolder; }
    .text { font-size: medium; }
  </style>
  <div class="wrapper">
    <p class="title">Welcome to Dice Roller!</p>
    <p class="text">Press the save button to continue.</p>
  </div>
`;

function renderSettings(elem) {
    elem.appendChild(settingsTemplate.content.cloneNode(true));

    // Save the configurable tab
    pages.config.registerOnSaveHandler(saveEvent => {
      pages.config.setConfig({
        websiteUrl: window.location.origin,
        contentUrl: window.location.origin + '?inTeams=1&view=content',
        entityId: 'DiceRollerFluidLiveShare',
        suggestedDisplayName: 'DiceRollerFluidLiveShare'
      });
      saveEvent.notifySuccess();
    });

    // Enable the Save button in config dialog
    pages.config.setValidityState(true);
}
```

## <a name="test-locally"></a>Локальное тестирование

Вы можете протестировать свое приложение локально с помощью `npm run start`. Дополнительные сведения см. в [кратком руководстве по началу работы](./teams-live-share-quick-start.md).

## <a name="test-in-teams"></a>Тестирование в Teams

После запуска приложения в локальной среде с помощью `npm run start` вы можете протестировать его в Teams. Если вы хотите протестировать приложение без развертывания, скачайте и используйте службу туннелирования [`ngrok`](https://ngrok.com/).

### <a name="create-a-ngrok-tunnel-to-allow-teams-to-reach-your-app"></a>Создание туннеля ngrok, чтобы разрешить Teams доступ к вашему приложению

1. [Скачайте ngrok](https://ngrok.com/download).

1. Используйте ngrok для создания туннеля с портом 8080. Выполните следующую команду:

    ```
     `ngrok http 8080 --host-header=localhost`
    ```

    Откроется новый терминал ngrok с новым URL-адресом, например `https:...ngrok.io`. Новый URL-адрес — это туннель, указывающий на ваше приложение, который необходимо обновить в `manifest.json` приложения.

### <a name="create-the-app-package-to-sideload-into-teams"></a>Создание пакета приложения для загрузки неопубликованных приложений в Teams

1. Перейдите в папку примера Dice Roller `\live-share-sdk\samples\01.dice-roller` на своем компьютере. Вы также можете просмотреть [`.\manifest\manifest.json`](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller/manifest) в примере Dice Roller на GitHub.

1. Откройте файл manifest.json и обновите URL-адрес конфигурации.

   Замените `https://<<BASE_URI_DOMAIN>>` своей конечной точкой HTTP из ngrok.

1. Вы можете обновить следующие поля.
   * Настройте для `developer.name` ваше имя.
   * Обновите `developer.websiteUrl` с использованием вашего веб-сайта.
   * Обновите `developer.privacyUrl` с использованием вашей политики конфиденциальности.
   * Обновите `developer.termsOfUseUrl` с применением ваших условий использования.

1. Заархивируйте содержимое папки манифеста для создания `manifest.zip`. Убедитесь, что `manifest.zip` содержит только исходный файл `manifest.json`, значок `color` и значок `outline`.

   1. В Windows выберите все файлы в каталоге `.\manifest` и сожмите их.
  
   > [!NOTE]
   >
   > * Не архивируйте содержащую папку.
   > * Присвойте ZIP-файлу описательное имя. Например, `DiceRollerLiveShare`.
  
   Дополнительные сведения о манифесте см. в [ документации манифеста Teams](../resources/schema/manifest-schema.md)

### <a name="sideload-your-app-into-a-meeting"></a>Загрузка неопубликованного приложения в собрание

1. Откройте Teams.

1. Запланируйте собрание в календаре Teams. Пригласите хотя бы одного участника на собрание.

1. Присоединитесь к собранию.

1. В верхней части окна собрания выберите **+ Приложения** > **Управление приложениями**.

1. В области **Управление приложениями** выберите **Отправить пользовательское приложение**.

   1. Если вы не видите параметр **Отправить пользовательское приложение**, следуйте [инструкциям](/microsoftteams/teams-custom-app-policies-and-settings), чтобы включить пользовательские приложения в клиенте.

1. Выберите и отправьте файл `manifest.zip` со своего компьютера.

1. Нажмите **Добавить**, чтобы добавить пример приложения в собрание.

1. Выберите **+ Приложения**, введите "Dice Roller" в поле поиска **Найти приложение**.

1. Выберите приложение, чтобы активировать его на собрании.

1. Нажмите кнопку **Сохранить**.

   Приложение Dice Roller добавляется на панель собрания Teams.

1. На боковой панели щелкните значок демонстрации на сцене. Teams начинает динамическую синхронизацию с пользователями на сцене текущего собрания.

   :::image type="content" source="../assets/images/teams-live-share/teams-live-share-to-stage.png" alt-text="Значок демонстрации на сцене":::

   Теперь на сцене собрания должно появиться приложение Dice-Roller.

   :::image type="content" source="../assets/images/teams-live-share/teams-live-share-meeting-stage.png" alt-text="изображение сцены собрания":::

Пользователи, приглашенные на собрание, смогут увидеть ваше приложение на сцене после присоединения к собранию.

## <a name="deployment"></a>Развертывание

Когда вы будете готовы развернуть код, вы можете использовать [набор средств Teams](../toolkit/provision.md#provision-using-teams-toolkit) или [портал разработчика Teams](https://dev.teams.microsoft.com/apps) для подготовки и отправки ZIP-файла приложения.

> [!NOTE]
> Перед отправкой или распространением приложения необходимо добавить подготовленный идентификатор приложения в `manifest.json`.

## <a name="code-samples"></a>Примеры кода

| Название примера | Описание                                                      | JavaScript                                                                           |
| :---------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Dice Roller | Включение во всех подключенных клиентах возможности прокрутки игральной кости и просмотра результата. | [View](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Основные возможности](teams-live-share-capabilities.md)

## <a name="see-also"></a>См. также

* [Репозиторий GitHub](https://github.com/microsoft/live-share-sdk)
* [Справочные документы по пакету SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Справочные документы по пакету SDK мультимедиа Live Share](/javascript/api/@microsoft/live-share-media/)
* [Вопросы и ответы о Live Share](teams-live-share-faq.md)
* [Приложения Teams на собраниях](teams-apps-in-meetings.md)
