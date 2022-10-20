---
title: Использование гибких функций в Teams
author: timtwang
ms.author: mobajemu
description: Руководство по интеграции функций совместной работы в режиме реального времени на основе гибких возможностей в приложение вкладок Microsoft Teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 620e2150ca6300fb8d37bc7c68b965aacb19700b
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615440"
---
# <a name="use-fluid-with-teams"></a>Использование гибких функций в Teams

По завершении работы с этим руководством вы можете интегрировать любое гибкое приложение в Teams и работать совместно с другими пользователями в режиме реального времени.

В этом разделе описаны следующие понятия:

1. Интеграция гибкого клиента в приложение вкладок Teams.
1. Запустите приложение Teams и подключите его к гибкой службе (Azure Fluid Relay).
1. Создайте и получите гибкие контейнеры и передайте их в React компонента.

Дополнительные сведения о создании сложного приложения см. в [Hello World в](https://github.com/microsoft/FluidExamples/tree/main/teams-fluid-hello-world) репозитории FluidExamples.

## <a name="prerequisites"></a>Предварительные требования

Для работы с этим руководством необходимо ознакомиться со следующими понятиями и ресурсами:

- [Общие сведения о Fluid Framework](https://fluidframework.com/docs/)
- [Краткое руководство по Fluid Framework](https://fluidframework.com/docs/start/quick-start/)
- Основные [сведения о React](https://reactjs.org/) и [React-перехватчиков](https://reactjs.org/docs/hooks-intro.html)
- Создание вкладки [Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs)

> [!div class="nextstepaction"]
> [Необходимые условия для установки](tab-requirements.md)

## <a name="create-the-project"></a>Создание проекта

1. Откройте командную строку и перейдите к родительской папке, в которой вы хотите создать проект, `/My Microsoft Teams Projects`например.
1. Создайте приложение вкладки Teams, выполнив следующую команду [и создав вкладку канала](create-channel-group-tab.md#create-a-custom-channel-or-group-tab-with-nodejs):

    ```cmd
    yo teams
    ```

1. После создания перейдите к проекту с помощью следующей команды `cd <your project name>`.
1. В проекте используются следующие библиотеки:

    |Library |Описание |
    |---|---|
    | `fluid-framework`    |Содержит IFluidContainer и другие распределенные структуры данных, которые синхронизируются между клиентами.[](https://fluidframework.com/docs/build/dds/)|
    | `@fluidframework/azure-client`   |Определяет начальную схему для [контейнера Fluid](https://fluidframework.com/docs/build/containers/).|
    | `@fluidframework/test-client-utils` |Определяет необходимые `InsecureTokenProvider` точки для создания подключения к гибкой службе.|

    Выполните следующую команду, чтобы установить библиотеки:

    ```cmd
    npm install @fluidframework/azure-client fluid-framework @fluidframework/test-client-utils
    ```

## <a name="code-the-project"></a>Код проекта

1. Откройте файл в `/src/client/<your tab name>` редакторе кода.
1. Создайте новый файл и добавьте `Util.ts` следующие инструкции импорта:

    ```ts
    //`Util.ts

    import { IFluidContainer } from "fluid-framework";
    import { AzureClient, AzureClientProps } from "@fluidframework/azure-client";
    import { InsecureTokenProvider } from "@fluidframework/test-client-utils";
    ```

### <a name="defining-fluid-functions-and-parameters"></a>Определение гибких функций и параметров

Это приложение предназначено для использования в контексте Microsoft Teams со всеми связанными с гибкими функциями импортом, инициализацией и функциями. Это обеспечивает расширенный интерфейс и упрощает его использование в будущем. В инструкции импорта можно добавить следующий код:

```ts
// TODO 1: Define the parameter key(s).
// TODO 2: Define container schema.
// TODO 3: Define connectionConfig (AzureClientProps).
// TODO 4: Create Azure client.
// TODO 5: Define create container function.
// TODO 6: Define get container function.
```

> [!NOTE]
> Комментарии определяют все функции и константы, необходимые для взаимодействия со службой и контейнером Fluid.

1. Замените `TODO 1:` на приведенный ниже код.

    ```ts
    export const containerIdQueryParamKey = "containerId";
    ```

    Константа экспортируется `contentUrl` по мере добавления в параметры Microsoft Teams, а затем для анализа идентификатора контейнера на странице содержимого. Часто важные ключи параметров запроса хранятся в виде констант, а не вводить необработанную строку каждый раз.

    Перед созданием контейнеров `containerSchema` клиент должен определить общие объекты, используемые в этом приложении. В этом примере в качестве общего объекта `initialObjects`используется SharedMap, но можно использовать любой общий объект.

    > [!NOTE]
    > Идентификатор `map` объекта, который `SharedMap` должен быть уникальным в пределах контейнера, как и любые другие DDSe.

1. Замените `TODO: 2` на приведенный ниже код.

    ```ts
    const containerSchema = {
        initialObjects: { map: SharedMap }
    };
    ```

1. Замените `TODO: 3` на приведенный ниже код.

    ```ts
    const connectionConfig : AzureClientProps =
    {
        connection: {
            type: "local",
            tokenProvider: new InsecureTokenProvider("foobar", { id: "user" }),
            endpoint: "http://localhost:7070"
        }
    };
    ```

    Прежде чем клиент можно будет использовать, он должен `AzureClientProps` определить тип подключения, используемого клиентом. Это `connectionConfig` свойство требуется для подключения к службе. Используется локальный режим клиента Azure. Чтобы обеспечить совместную работу для всех клиентов, замените его учетными данными службы гибкого ретранслятора. Дополнительные сведения см. в статье о настройке [службы Azure Fluid Relay](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal).

1. Замените `TODO: 4` на приведенный ниже код.

    ```ts
    const client = new AzureClient(connectionConfig);
    ```

1. Замените `TODO: 5` на приведенный ниже код.

    ```ts
    export async function createContainer() : Promise<string> {
        const { container } = await client.createContainer(containerSchema);
        const containerId = await container.attach();
        return containerId;
    };
    ```

    При создании контейнера `contentUrl` на странице конфигурации и его добавлении в параметр Teams необходимо вернуть идентификатор контейнера после подключения контейнера.

1. Замените `TODO: 6` на приведенный ниже код.

    ```ts
    export async function getContainer(id : string) : Promise<IFluidContainer> {
        const { container } = await client.getContainer(id, containerSchema);
        return container;
    };
    ```

    При получении контейнера Fluid необходимо вернуть контейнер, так как приложение должно взаимодействовать с контейнером и DDSes внутри него на странице содержимого.

### <a name="create-fluid-container-in-the-configuration-page"></a>Создание гибкого контейнера на странице конфигурации

1. Откройте файл в `src/client/<your tab name>/<your tab name>Config.tsx` редакторе кода.

    Стандартный поток приложения на вкладке Teams переходит от конфигурации к странице содержимого. Чтобы обеспечить совместную работу, крайне важно сохранить контейнер при загрузке на страницу содержимого. Лучшим решением для сохранения `contentUrl` `websiteUrl`контейнера является добавление идентификатора контейнера к URL-адресам страницы содержимого и url-адресам в качестве параметра запроса. Кнопка "Сохранить" на странице конфигурации Teams — это шлюз между страницей конфигурации и страницей содержимого. Это место для создания контейнера и добавления идентификатора контейнера в параметры.

1. Добавьте следующий оператор импорта:

    ```ts
    import { createContainer, containerIdQueryParamKey } from "./Util";
    ```

1. Замените метод `onSaveHandler` следующим кодом. Единственными добавленными `Utils.ts` `contentUrl` `websiteUrl` здесь строками являются вызов метода создания контейнера, определенного ранее, а затем добавление возвращенного идентификатора контейнера к параметру запроса и в качестве параметра запроса.

    ```ts {linenos=inline,hl_lines=[134,136,137]}
    const onSaveHandler = async (saveEvent: microsoftTeams.settings.SaveEvent) => {
        const host = "https://" + window.location.host;
        const containerId = await createContainer();
        microsoftTeams.settings.setSettings({
            contentUrl: host + "/<your tab name>/?" + containerIdQueryParamKey + "=" + containerId + "&name={loginHint}&tenant={tid}&group={groupId}&theme={theme}",
            websiteUrl: host + "/<your tab name>/?" + containerIdQueryParamKey + "=" + containerId + "&name={loginHint}&tenant={tid}&group={groupId}&theme={theme}",
            suggestedDisplayName: "<your tab name>",
            removeUrl: host + "/<your tab name>/remove.html?theme={theme}",
            entityId: entityId.current
        });
        saveEvent.notifySuccess();
    };
    ```

    Убедитесь, что `<your tab name>` вы замените имя вкладки из проекта.

    > [!WARNING]
    > Так как URL-адрес страницы содержимого используется для хранения идентификатора контейнера, эта запись удаляется при удалении вкладки Teams.
    > Кроме того, каждая страница содержимого может поддерживать только один идентификатор контейнера.

### <a name="refactor-content-page-to-reflect-fluid-application"></a>Страница рефакторинга содержимого для отражения гибкого приложения

1. Откройте файл в `src/client/<your tab name>/<your tab name>.tsx` редакторе кода. Типичное гибкое приложение состоит из представления и гибкой структуры данных. Сосредоточьте внимание на получении и загрузке контейнера Fluid и оставьте все связанные с гибкими взаимодействиями React компоненте.

1. Добавьте следующие инструкции импорта на страницу содержимого:

    ```ts
    import { IFluidContainer } from "fluid-framework";
    import { getContainer, containerIdQueryParamKey } from "./Util";
    ```

1. Удалите весь код под инструкциями импорта на странице содержимого и замените его следующим кодом:

    ```ts
    export const <your tab name> = () => {
      // TODO 1: Initialize Microsoft Teams.
      // TODO 2: Initialize inTeams boolean.
      // TODO 3: Define container as a React state.
      // TODO 4: Define a method that gets the Fluid container
      // TODO 5: Get Fluid container on content page startup.
      // TODO 6: Pass the container to the React component as argument.
    }
    ```

    Убедитесь, что `<your tab name>` вы замените имя вкладки, определенное для проекта.

1. Замените `TODO 1` на приведенный ниже код.

    ```ts
    microsoftTeams.initialize();
    ```

    Чтобы отобразить страницу содержимого в Teams, необходимо включить клиентский [пакет SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client) и включить вызов для инициализации после загрузки страницы.

1. Замените `TODO 2` на приведенный ниже код.

    ```ts
    const [{ inTeams }] = useTeams();
    ```

    Так как приложение Teams является просто внедрением IFrame веб-страницы, `inTeams` необходимо инициализировать логическую константу, чтобы узнать, находится ли приложение внутри Teams или нет, и доступны ли ресурсы Teams, `contentUrl`такие как the.

1. Замените `TODO 3` на приведенный ниже код.

    ```ts
    const [fluidContainer, setFluidContainer] = useState<IFluidContainer | undefined>(undefined);
    ```

    Используйте React для контейнера, так как он предоставляет возможность динамического обновления контейнера и объектов данных в нем.

1. Замените `TODO 4` на приведенный ниже код.

    ```ts
    const getFluidContainer = async (url : URLSearchParams) => {
        const containerId = url.get(containerIdQueryParamKey);
        if (!containerId) {
            throw Error("containerId not found in the URL");
        }
        const container = await getContainer(containerId);
        setFluidContainer(container);
    };
    ```

    Проанализируйте URL-адрес, чтобы получить строку параметра запроса, определенную `containerIdQueryParamKey`и получить идентификатор контейнера. С помощью идентификатора контейнера можно загрузить контейнер. После создания контейнера задайте React `fluidContainer` , см. предыдущий шаг.

1. Замените `TODO 5` на приведенный ниже код.

    ```ts
    useEffect(() => {
        if (inTeams === true) {
            microsoftTeams.settings.getSettings(async (instanceSettings) => {
                const url = new URL(instanceSettings.contentUrl);
                getFluidContainer(url.searchParams);
            });
            microsoftTeams.appInitialization.notifySuccess();
        }
    }, [inTeams]);
    ```

    Определив способ получения контейнера Fluid, необходимо сообщить React при загрузке, а затем сохранить результат в состоянии в зависимости от того, `getFluidContainer` находится ли приложение в Teams.
    React [useState](https://reactjs.org/docs/hooks-state.html) предоставляет необходимое хранилище, а [useEffect](https://reactjs.org/docs/hooks-effect.html) `getFluidContainer` позволяет вызывать отрисовку, передавая возвращенное значение `setFluidContainer`в .

    Добавляя `inTeams` в массив зависимостей `useEffect`в конце объекта, приложение гарантирует, что эта функция будет вызываться только при загрузке страницы содержимого.

1. Замените `TODO 6` на приведенный ниже код.

    ```ts
    if (inTeams === false) {
      return (
          <div>This application only works in the context of Microsoft Teams</div>
      );
    }

    if (fluidContainer !== undefined) {
      return (
          <FluidComponent fluidContainer={fluidContainer} />
      );
    }

    return (
      <div>Loading FluidComponent...</div>
    );
    ```

    > [!NOTE]
    > Важно убедиться, что страница содержимого загружена в Teams и что контейнер Fluid определен перед передачей в компонент React (`FluidComponent`определяется как ( см. ниже).

### <a name="create-react-component-for-fluid-view-and-data"></a>Создание React для гибкого представления и данных

Вы интегрировали базовый поток создания Teams и Fluid. Теперь можно создать собственный React, который обрабатывает взаимодействие между представлением приложения и гибкими данными. Теперь логика и поток ведут себя так же, как и другие приложения на основе гибких функций. Настроив базовую структуру, вы можете создать [](https://github.com/microsoft/FluidExamples) любой из гибких примеров в качестве приложения Teams`ContainerSchema`, изменив взаимодействие представления приложения с объектами DDSes и данными на странице содержимого.

## <a name="start-the-fluid-server-and-run-the-application"></a>Запустите гибкий сервер и запустите приложение.

Если вы запускаете приложение Teams локально в локальном режиме клиента Azure, выполните следующую команду в командной строке, чтобы запустить гибкую службу:

```cmd
npx @fluidframework/azure-local-service@latest
```

Чтобы запустить и запустить приложение Teams, откройте другой терминал и следуйте инструкциям по [запуску сервера приложений](create-channel-group-tab.md#upload-your-application-to-teams).

> [!WARNING]
> HostNames с `ngrok`бесплатными туннели не сохраняются. При каждом запуске создается другой URL-адрес. При создании нового `ngrok` туннеля старый контейнер больше не будет доступен. Сведения о рабочих сценариях см. [в статье об использовании AzureClient с Azure Fluid Relay](#use-azureclient-with-azure-fluid-relay).

> [!NOTE]
> Установите дополнительную зависимость, чтобы сделать эту демонстрацию совместимой с Webpack 5. Если возникает ошибка компиляции, связанная с пакетом buffer, выполните и `npm install -D buffer` повторите попытку. Эта проблема будет устранена в следующем выпуске Fluid Framework.

## <a name="next-steps"></a>Дальнейшие действия

### <a name="use-azureclient-with-azure-fluid-relay"></a>Использование AzureClient с Гибким ретранслятором Azure

Так как это приложение на вкладке Teams, основное внимание уделяется совместной работе и взаимодействию. Замените локальный `AzureClientProps` режим, предоставленный ранее, не локальными учетными данными из экземпляра службы Azure, чтобы другие пользователи могли присоединиться к вам и взаимодействовать с вами в приложении. Узнайте [, как подготовить службу Azure Fluid Relay](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal).

> [!IMPORTANT]
> Важно скрыть учетные `AzureClientProps` данные, которые вы передаете, от случайной фиксации в системах управления версиями. Проект Teams поставляется с файлом `.env` , в котором учетные данные можно хранить как переменные среды, а сам файл уже включен в `.gitignore`. Сведения об использовании переменных среды в Teams см. в разделе ["Задание и получение переменной среды"](#set-and-get-environment-variable).

> [!WARNING]
> `InsecureTokenProvider` — это удобный способ локального тестирования приложения. Вы несете ответственность за обработку любой проверки подлинности пользователя и использование безопасного маркера [для любой](/azure/azure-fluid-relay/how-tos/connect-fluid-azure-service) рабочей среды.

### <a name="set-and-get-environment-variable"></a>Задание и получение переменной среды

Чтобы задать переменную среды и получить ее в Teams, можно воспользоваться встроенным файлом `.env` . Следующий код используется для задания переменной среды в следующем коде `.env`:

```
# .env

TENANT_KEY=foobar
```

Чтобы передать содержимое `.env` файла в клиентское приложение, необходимо настроить его таким образом, `webpack.config.js` `webpack` чтобы предоставить к ним доступ во время выполнения. Используйте следующий код, чтобы добавить переменную среды из `.env`:

```js
// webpack,config.js

webpack.EnvironmentPlugin({
    PUBLIC_HOSTNAME: undefined,
    TAB_APP_ID: null,
    TAB_APP_URI: null,
    REACT_APP_TENANT_KEY: JSON.stringify(process.env.TENANT_KEY) // Add environment variable here
}),
```

Доступ к переменной среды можно получить в `Util.ts`

```ts
// Util.ts

tokenProvider: new InsecureTokenProvider(JSON.parse(process.env.REACT_APP_TENANT_KEY!), { id: "user" }),
```

> [!TIP]
> При внесении изменений в код проект автоматически перестраивается, а сервер приложений перезагружается. Однако при внесении изменений в схему контейнера они вступает в силу только при закрытии и перезапуске сервера приложений. Для этого перейдите в командную строку и дважды нажмите клавиши CTRL+C. Затем выполните или `gulp serve` повторите `gulp ngrok-serve` попытку.

## <a name="see-also"></a>См. также

- [Документация по Azure Fluid Relay](/azure/azure-fluid-relay)

- [Документация по Fluid Framework](https://fluidframework.com/docs/)
- [Гибкие примеры репозитория GitHub](https://github.com/microsoft/FluidExamples)
