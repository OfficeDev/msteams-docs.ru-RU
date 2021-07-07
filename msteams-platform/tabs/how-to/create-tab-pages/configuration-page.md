---
title: Создать страницу конфигурации
author: surbhigupta
description: создание страницы конфигурации
keywords: команды вкладки группового канала настраиваются
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6f79480fb3ec6eb50de622e0b67b70e021d8cce7
ms.sourcegitcommit: a6253e89cb8c8c34d45b06e08c9668daeebc30a3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/06/2021
ms.locfileid: "53300314"
---
# <a name="create-a-configuration-page"></a>Создать страницу конфигурации

Страница конфигурации — это особый тип [страницы контента.](content-page.md) Пользователи настраивают некоторые аспекты приложения Microsoft Teams, используя страницу конфигурации, и используют эту конфигурацию в следующем:

* Вкладка чата канала или группы: сбор сведений от пользователей и отображение страницы `contentUrl` контента.
* Расширение [обмена сообщениями.](~/messaging-extensions/what-are-messaging-extensions.md)
* Соедините [Office 365.](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configure-a-channel-or-group-chat-tab"></a>Настройка вкладки чата канала или группы

Приложение должно ссылаться на [Microsoft Teams клиента JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и вызывать `microsoft.initialize()` . Используемые URL-адреса должны быть защищены конечными точками HTTPS и доступны в облаке.

### <a name="example"></a>Пример

Пример страницы конфигурации показан на следующем изображении:

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

Следующий код — пример соответствующего кода для страницы конфигурации:

```html
<head>
    <script src='https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
</head>
<body>
    <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
    <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
    <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

    <script>
        microsoftTeams.initialize();
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.settings.setSettings({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/gray",
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.settings.setSettings({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/red",
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let gr = document.getElementById("gray").style;
        let rd = document.getElementById("red").style;

        const colorClickGray = () => {
            gr.display = "block";
            rd.display = "none";
            microsoftTeams.settings.setValidityState(true);
            saveGray()
        }

        const colorClickRed = () => {
            rd.display = "block";
            gr.display = "none";
            microsoftTeams.settings.setValidityState(true);
            saveRed();
        }
    </script>
    ...
</body>
```

Выберите **кнопку Выберите серый** или **красный** на странице конфигурации, чтобы отобразить содержимое вкладки с серым или красным значком.

На следующем изображении отображается содержимое вкладки с серым значком:

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

На следующем изображении отображается содержимое вкладки с красным значком:

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

Выбор соответствующей кнопки запускает или `saveGray()` вызывает `saveRed()` следующее:

* Установите `settings.setValidityState(true)` для true. 
* Запускается `microsoftTeams.settings.registerOnSaveHandler()` обработник событий.
* **Сохранение** на странице конфигурации приложения включено.

Код страницы конфигурации информирует Teams, что требования к конфигурации удовлетворены и установка может продолжиться. Когда пользователь выбирает **Сохранить,** параметры заданы, `settings.setSettings()` как определено `Settings` интерфейсом. Дополнительные сведения см. в [интерфейсе параметров.](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) `saveEvent.notifySuccess()` называется, чтобы указать, что URL-адрес контента успешно решен.

>[!NOTE]
>
>* Если вы регистрируете обработчивель сохранения с помощью, он должен вызвать вызов или указать `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` результат `saveEvent.notifyFailure()` конфигурации.
>* Если обработник сохранения не зарегистрирован, вызов делается автоматически, когда пользователь `saveEvent.notifySuccess()` выбирает **Сохранить**.

### <a name="get-context-data-for-your-tab-settings"></a>Получите контекстные данные для параметров вкладки

Для отображения соответствующего контента на вкладке требуются контекстные сведения. Контекстная информация еще больше повышает привлекательность вкладки, предоставляя более настраиваемый пользовательский интерфейс.

Дополнительные сведения о свойствах, используемых для конфигурации вкладок, см. в [интерфейсе контекста.](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) Собирайте значения переменных данных контекста следующими способами:

* Вставьте в манифесте строки строки URL-адресов. `configurationURL`

* Используйте метод [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`

#### <a name="insert-placeholders-in-the-configurationurl"></a>Вставьте местообладатели в `configurationUrl`

Добавьте в базу местообладатели интерфейса `configurationUrl` контекста. Пример:

##### <a name="base-url"></a>Базовый URL-адрес

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>Базовый URL-адрес со строками запросов

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

После загрузки страницы Teams строки запросов с соответствующими значениями. Включай логику на странице конфигурации для получения и использования этих значений. Дополнительные сведения о работе со строками запросов URL-адресов см. в [странице URLSearchParams в](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) веб-docs MDN. В следующем примере кода приводится способ извлечения значения из `configurationUrl` свойства:

```html
<script>
   microsoftTeams.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Использование `getContext()` функции для получения контекста

Функция `microsoftTeams.getContext((context) => {})` извлекает интерфейс [контекста при](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) вызове.

В следующем коде приводится пример добавления этой функции на страницу конфигурации для получения значений контекста:

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    microsoftTeams.getContext((context) =>{
        let userId = document.getElementById('user');
        userId.innerHTML = context.userPrincipalName;
    });
</script>
...
```

## <a name="context-and-authentication"></a>Контекст и проверка подлинности

Проверка подлинности перед разрешением пользователю настроить приложение. В противном случае содержимое может включать источники, у них есть протоколы проверки подлинности. Дополнительные сведения см. в записи проверки подлинности [пользователя на вкладке Microsoft Teams.](~/tabs/how-to/authentication/auth-flow-tab.md) Используйте контекстные сведения для создания запросов на проверку подлинности и URL-адресов страниц авторизации. Убедитесь, что все домены, используемые на страницах вкладок, перечислены в `manifest.json` `validDomains` массиве и массиве.

## <a name="modify-or-remove-a-tab"></a>Изменение или удаление вкладки

Установите свойство манифеста, которое позволяет пользователям изменять, перенастроять или переименовывать вкладку канала `canUpdateConfiguration` `true` или группы. Кроме того, указать, что происходит с контентом при удалении вкладки, включив страницу параметры удаления в приложение и установив значение для свойства `removeUrl` в  `setSettings()` конфигурации. Пользователь может удалить личные вкладки, но не может изменить их. Дополнительные сведения см. [в странице создание страницы удаления для вкладки.](~/tabs/how-to/create-tab-pages/removal-page.md)

`setSettings()`Microsoft Teams конфигурация для удаления страницы:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a>Мобильные приложения

Если вы хотите, чтобы вкладка канала или группы Teams мобильных клиентов, конфигурация должна иметь `setSettings()` значение `websiteUrl` для . Дополнительные сведения см. [в руководстве по вкладке на мобильных устройствах.](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>См. также

* [Teams вкладки](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Создать страницу контента](~/tabs/how-to/create-tab-pages/content-page.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md)
