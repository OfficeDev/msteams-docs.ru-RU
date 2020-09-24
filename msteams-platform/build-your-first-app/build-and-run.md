---
title: Создание и запуск "Hello, World!" Приложение Teams
author: heath-hamilton
description: Создание и запуск первого приложения Microsoft Teams, вкладки личных параметров, в которой отображается слово "Hello, World!"
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 244a899670f71b9446c8c3d3e404c9fd7c7b510c
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237834"
---
# <a name="build-a-hello-world-teams-app"></a>Создание приложения "Hello World!" Приложение Teams

Вы можете перейти непосредственно к разработке платформы Microsoft Teams, создав личную вкладку со свойством "Hello, World!".

## <a name="1-create-your-app-project"></a>1. Создайте проект приложения.

Используйте набор средств Microsoft Teams в Visual Studio Code, чтобы настроить первый проект приложения.

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="Снимок экрана, на котором показано, как создать новое приложение с набором средств Visual Studio Code Teams Toolkit.":::
1. Введите имя приложения Teams. (Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)
1. На экране **добавить возможности** выберите **вкладка** **Далее**.
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Снимок экрана, на котором показано, как настроить проект приложения с помощью набора инструментов Visual Studio Code Teams.":::
1. Установите флажок **Личная вкладка** , а затем в нижней части экрана нажмите кнопку **Готово** , чтобы настроить проект.

## <a name="2-understand-important-app-project-components"></a>2. Изучите важные компоненты проекта приложения

После того как набор инструментов настроит свой проект, у вас будут компоненты для создания базовой вкладки "личные" для Teams. Каталоги и файлы проекта отображаются в области обозревателя Visual Studio Code.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Снимок экрана, на котором показаны файлы проекта приложения для вкладки "личные" в Visual Studio Code.":::

Давайте рассмотрим некоторые ключевые файлы, с которыми работают разработчики приложений Teams.

### <a name="app-manifest-manifestjson"></a>Манифест приложения ( `manifest.json` )

В каталоге манифест приложения размещается в качестве `.publish` отправной точки для любого проекта приложения. Манифест определяет основные атрибуты приложения и указывает на необходимые ресурсы. При установке приложения Teams анализирует манифест, чтобы узнать, как визуализировать приложение в клиенте.

### <a name="app-scaffolding"></a>Формирование шаблонов приложений

Набор средств автоматически создает формирование шаблонов в `src` каталоге на основе возможностей, добавленных во время установки.

Например, при создании вкладки во время установки, `App.js` файл в `src/components` каталоге важен, так как он обрабатывает инициализацию и маршрутизацию приложения. Он вызывает [пакет Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) для установления связи между приложением и Teams.

### <a name="app-package-developmentzip"></a>Пакет приложения ( `Development.zip` )

В `.publish` каталоге вам нужен пакет приложения, чтобы [Загрузка неопубликованных ваше приложение](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) в Teams. Пакет также используется при [публикации в каталоге приложений организации](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) или [AppSource](../concepts/deploy-and-publish/appsource/publish.md).

Ниже приведены некоторые сведения о файлах пакета приложения.

|Имя|Тип|Size|Расположение манифеста|Имя файла набора инструментов|
|---|---|:---:|:---:|-----|
|**Манифест приложения**|`.json`| — | — |`.publish/manifest.json`|
|**Цветовой логотип**|`.png`|192 &times; 192 пикселя|`icon.color`|`.publish/color.png`|
|**Эмблема структуры**|`.png`|32 &times; 32 пикселя|`icon.outline`|`.publish/outline.png`|

## <a name="3-run-your-app"></a>3. Запустите приложение.

В течение этого времени вы создадите и запустите свое приложение локально.

(Эти сведения также доступны в наборе инструментов `README` .)

1. В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .
1. Выполните команду `npm start` . По завершении **компиляции успешно выполняется.** сообщение в терминале.
1. Откройте браузер и перейдите по адресу, чтобы `https://localhost:3000` Просмотреть пустую веб-страницу с именем **"Вкладка Microsoft Teams"**. Не волнуйтесь, что на странице не должно отображаться никаких контента.<br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="Снимок экрана, на котором показано, как просмотреть работающее приложение в браузере.":::

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a>4. Настройка безопасного туннеля для приложения

Ваше приложение запущено и работает на локальном веб-сервере. Для запуска приложения в Teams необходимо предоставить `localhost` доступ к нему по протоколу HTTPS.

Установите [ngrok](https://ngrok.com/download) , если вы этого еще не сделали. При запуске этого средства создаются два глобально доступных URL-адреса, указывающие на локальный веб-сервер ( `http://localhost:3000` ). Вам потребуется URL-адрес переадресации, начинающийся с `HTTPS` .

1. Откройте новый терминал и запустите его `ngrok http 3000` .
1. Скопируйте предоставленный URL-адрес HTTPS (см. Следующий пример).
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="Снимок экрана с терминалом, на котором запущен ngrok.":::
1. В `.publish` каталоге откройте `Development.env` .
1. Замените `baseUrl0` значение скопированным URL-адресом. (Например, замените `baseUrl0=http://localhost:3000` на `baseUrl0=https://85528b2b3ba5.ngrok.io` .)

Теперь манифест приложения указывает на место размещения приложения.

## <a name="5-sideload-your-app-in-teams"></a>5. Загрузка неопубликованных ваше приложение в Teams

Когда ваше приложение работает и доступно через HTTPS, вы можете отправить его в Teams.

> [!TIP]
> Прежде чем приступить к работе с неопубликованным приложением, проверьте наличие проблем с помощью [средства проверки набора](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool). Чтобы успешно Загрузка неопубликованных приложение, необходимо исправить ошибки.

1. Выполните вход в клиент Teams с учетной записью, позволяющей выполнять загрузку неопубликованных приложений. (Если вы не знаете этого, Узнайте о том, как получить [учетную запись разработки Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)
1. Выберите **приложения**, а затем нажмите кнопку **Отправить пользовательское приложение**.
1. Перейдите в папку проекта приложения `.publish` и выберите `Development.zip` . Модальные дисплеи установки.
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="Снимок экрана, на котором показан пример модальной установки приложения Teams.":::
1. Нажмите кнопку **Добавить** , чтобы установить приложение.
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Снимок экрана, на котором показан пример приложения "Hello, World!", которое работает в Teams.":::

Поздравляем 🎉! Ваше приложение работает в Teams.

## <a name="next-step"></a>Следующий шаг

Разверните вкладку Персональная личная и создайте другой тип приложения Teams.

> [!div class="nextstepaction"]
> [Добавление на вкладку "личные"](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [Создание вкладки канала](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Создание бота](../build-your-first-app/build-bot.md)
