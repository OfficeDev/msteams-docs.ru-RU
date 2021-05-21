---
title: Создать страницу конфигурации
author: laujan
description: создание страницы конфигурации
keywords: команды вкладки группового канала настраиваются
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: aeab1cf96d1e875db79d9143fefd0e46348f585a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566686"
---
# <a name="create-a-configuration-page"></a>Создать страницу конфигурации

Страница конфигурации — это особый тип [страницы контента.](content-page.md) Пользователи настраивают некоторые аспекты приложения Microsoft Teams, используя страницу конфигурации, и используют эту конфигурацию в следующем:

* Вкладка чата канала или группы: сбор сведений от пользователей и отображение страницы `contentUrl` контента.
* Расширение [обмена сообщениями.](~/messaging-extensions/what-are-messaging-extensions.md)
* Соедините [Office 365.](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>Настройка вкладки чата канала или группы

Приложение должно ссылаться на [Microsoft Teams клиента JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и вызывать `microsoft.initialize()` . Кроме того, используемые URL-адреса должны быть защищены конечными точками HTTPS и доступны в облаке. 

### <a name="example"></a>Пример

Пример страницы конфигурации показан на следующем изображении: 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

Соответствующий код страницы конфигурации показан в следующем разделе:

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
    </body>
...
```

Выберите **кнопку Выберите серый** или **красный** на странице конфигурации, чтобы отобразить содержимое вкладки с серым или красным значком. 

На следующем изображении отображается содержимое вкладки с серым значком:

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

На следующем изображении отображается содержимое вкладки с красным значком:

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

Выбор относительной кнопки вызывает или `saveGray()` вызывает `saveRed()` следующее:

1. `settings.setValidityState(true)`Установлено, что это верно.
1. Запускается `microsoftTeams.settings.registerOnSaveHandler()` обработник событий.
1. Кнопка **Сохранить** на странице конфигурации приложения, загруженная в Teams, включена.

Код страницы конфигурации сообщает Teams, что требования к конфигурации удовлетворены и установка может продолжиться. Когда пользователь выбирает **Сохранить,** параметры заданы, `settings.setSettings()` как определено `Settings` интерфейсом. Дополнительные сведения см. [в Параметры интерфейсе.](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true) На последнем шаге `saveEvent.notifySuccess()` вызвано, чтобы указать, что URL-адрес контента успешно разрешен.

>[!NOTE]
>
>* Если вы регистрируете обработчивель сохранения с помощью, он должен вызвать вызов или указать `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` результат `saveEvent.notifyFailure()` конфигурации.
>* Если обработник сохранения не регистрируется, вызов делается автоматически, когда пользователь `saveEvent.notifySuccess()` выбирает **Сохранить**.

### <a name="get-context-data-for-your-tab-settings"></a>Получите контекстные данные для параметров вкладки

Чтобы отображать соответствующее содержимое, вкладке может быть нужна контекстная информация. Контекстная информация еще больше повышает привлекательность вкладки, предоставляя более настраиваемый пользовательский интерфейс.

Дополнительные сведения о свойствах, используемых для конфигурации вкладок, см. в [интерфейсе Context.](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) Собирайте значения переменных данных контекста следующими способами:

1. Вставьте в манифесте строки строки URL-адресов. `configurationURL`

1. Используйте метод [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`

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

После загрузки страницы Teams строки запросов с соответствующими значениями. Включай логику на странице конфигурации для получения и использования этих значений. Дополнительные сведения о работе со строками запросов URL-адресов см. в [странице URLSearchParams в](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) веб-docs MDN. В следующем примере описывается способ извлечения значения из `configurationUrl` свойства:

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

Функция `microsoftTeams.getContext((context) => {})` извлекает интерфейс [Context при](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) вызове. Добавьте эту функцию на страницу конфигурации для получения значений контекста:

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

 Проверка подлинности перед разрешением пользователю настроить приложение. В противном случае содержимое может включать источники, у них есть протоколы проверки подлинности. Дополнительные сведения см. в вкладке [Authenticate a user in a Microsoft Teams.](~/tabs/how-to/authentication/auth-flow-tab.md) Используйте контекстные сведения для создания запросов на проверку подлинности и URL-адресов страниц авторизации.
Убедитесь, что все домены, используемые на страницах вкладок, перечислены в `manifest.json` `validDomains` массиве и массиве.

## <a name="modify-or-remove-a-tab"></a>Изменение или удаление вкладки

Поддерживаемые параметры удаления дополнительно уточняют пользовательский интерфейс. Задайте свойству манифеста свойство , которое позволяет пользователям изменять, перенастроять или переименовывать `canUpdateConfiguration` `true` вкладку группы или канала. Кроме того, указать, что происходит с контентом при удалении вкладки, включив страницу параметры удаления в приложение и установив значение для свойства `removeUrl` в  `setSettings()` конфигурации. Пользователь может удалить вкладки Personal, но не может изменить их. Дополнительные сведения см. в [странице Создание страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md).

Microsoft Teams setSettings() конфигурация для страницы удаления:

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

Если вы хотите, чтобы вкладка канала или группы Teams мобильных клиентов, конфигурация должна иметь значение `setSettings()` `websiteUrl` для свойства. Дополнительные сведения см. [в руководстве по вкладке на мобильных устройствах.](~/tabs/design/tabs-mobile.md)
