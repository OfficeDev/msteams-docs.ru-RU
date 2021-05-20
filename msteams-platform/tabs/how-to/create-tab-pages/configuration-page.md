---
title: Создать страницу конфигурации
author: laujan
description: как создать страницу конфигурации
keywords: команды вкладки группы канал настраиваемый
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

Страница конфигурации является особым типом страницы [содержимого.](content-page.md) Пользователи настраивают некоторые аспекты приложения Microsoft Teams используя страницу конфигурации и используют эту конфигурацию как часть следующего:

* Вкладка канала или группы чата: Соберите информацию от пользователей и `contentUrl` установите страницу содержимого для отображения.
* Расширение [обмена сообщениями](~/messaging-extensions/what-are-messaging-extensions.md).
* Разъем [Office 365 США](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="configuring-a-channel-or-group-chat-tab"></a>Настройка вкладки канала или группового чата

Приложение должно ссылаться на [Microsoft Teams JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и звонить. `microsoft.initialize()` Кроме того, используемые URL-адреса должны быть защищены конечных точек HTTPS и доступны из облака. 

### <a name="example"></a>Пример

Пример страницы конфигурации показан на следующем изображении: 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

Соответствующий код страницы конфигурации отображается в следующем разделе:

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

Выберите **кнопку Select Gray** или Select **Red** на странице конфигурации, чтобы отобразить содержимое вкладки серым или красным значком. 

Следующее изображение отображает содержимое вкладки с серым значком:

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

Следующее изображение отображает содержимое вкладки с красным значком:

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

Выбор относительной кнопки вызывает `saveGray()` либо или , и вызывает `saveRed()` следующее:

1. Установлен `settings.setValidityState(true)` на реальность.
1. Обработчик `microsoftTeams.settings.registerOnSaveHandler()` событий срабатывает.
1. Кнопка **Сохранения** на странице конфигурации приложения, загруженная в Teams, включена.

Код страницы конфигурации информирует Teams, что требования к конфигурации удовлетворены и установка может продолжиться. Когда пользователь выбирает **Сохранить**, параметры устанавливаются, `settings.setSettings()` как это определено `Settings` интерфейсом. Для получения дополнительной информации [с Параметры м.](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true) На последнем этапе `saveEvent.notifySuccess()` вызывается указать, что URL-адрес содержимого успешно решен.

>[!NOTE]
>
>* При регистрации обработчика сохранения `microsoftTeams.settings.registerOnSaveHandler()` с помощью обратного вызова `saveEvent.notifySuccess()` необходимо `saveEvent.notifyFailure()` вызвать или указать результат конфигурации.
>* Если вы не регистрируете обработчик сохранения, `saveEvent.notifySuccess()` вызов делается автоматически, когда пользователь выбирает **Сохранить**.

### <a name="get-context-data-for-your-tab-settings"></a>Получить контекстные данные для настроек вкладок

Чтобы отображать соответствующее содержимое, вкладке может быть нужна контекстная информация. Контекстная информация еще больше повышает привлекательность вашей вкладки, предоставляя более индивидуальный пользовательский интерфейс.

Для получения дополнительной информации о свойствах, используемых для конфигурации вкладок, [см.](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) Соберите значения переменных контекстных данных следующими двумя способами:

1. Вставьте держатели строк URL-запросов в `configurationURL` манифесте.

1. Используйте [Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` SDK.

#### <a name="insert-placeholders-in-the-configurationurl"></a>Вставьте держатели в `configurationUrl`

Добавьте в базу держатели контекстных `configurationUrl` интерфейсов. Пример:

##### <a name="base-url"></a>Базовый URL

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>Базовый URL со строками запросов

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

После загрузки страницы веб-Teams строки запросов с соответствующими значениями. Включите логику в страницу конфигурации для получения и использования этих значений. Для получения дополнительной информации о работе со строками [запросов URL см.](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) В следующем примере описывается способ извлечения значения из `configurationUrl` свойства:

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Используйте `getContext()` функцию для извлечения контекста

Функция `microsoftTeams.getContext((context) => {})` получает интерфейс Контекста при [вызовах.](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) Добавьте эту функцию на страницу конфигурации для получения значений контекста:

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

## <a name="context-and-authentication"></a>Контекст и аутентификация

 Аутентичность, прежде чем разрешить пользователю настроить приложение. В противном случае содержимое может включать источники, в которые есть протоколы проверки подлинности. Для получения дополнительной информации [см Microsoft Teams.](~/tabs/how-to/authentication/auth-flow-tab.md) Используйте контекстную информацию для построения URL-адресов запросов на проверку подлинности и авторизации страниц.
Убедитесь, что все домены, используемые на страницах вкладок, перечислены в `manifest.json` `validDomains` массиве и массиве.

## <a name="modify-or-remove-a-tab"></a>Изменение или удаление вкладки

Поддерживаемые варианты удаления еще больше уточняют пользовательский интерфейс. Установите свойство вашего `canUpdateConfiguration` `true` манифеста, чтобы пользователи могли изменять, перенастраивать или переименовывать вкладку группы или канала. Кроме того, укажите, что происходит с содержимым при удалении вкладки, включив страницу параметров удаления в приложение и установив `removeUrl` значение для свойства в  `setSettings()` конфигурации. Пользователь может удалить Личные вкладки, но не может изменить их. Для получения дополнительной информации [см. Создайте страницу удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md).

Microsoft Teams setSettings () конфигурация для удаления страницы:

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

Если вы решите, чтобы ваш канал или группа вкладка Teams мобильных клиентов, `setSettings()` конфигурация должна иметь значение для `websiteUrl` свойства. Для получения дополнительной информации, [см. руководство для вкладок на мобильном телефоне](~/tabs/design/tabs-mobile.md).
