---
title: Создать страницу конфигурации
author: surbhigupta
description: Узнайте, как создать страницу конфигурации для настройки канала или группового чата для параметров, таких как получение данных контекста, вставка заполнителей и проверка подлинности с помощью примеров кода.
keywords: Настраиваемый канал группы вкладок teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: dc1c5c7c8852d13ab490ae0782be0a01eef3fbea
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103420"
---
# <a name="create-a-configuration-page"></a>Создать страницу конфигурации

Страница конфигурации — это особый тип [страницы содержимого](content-page.md). Пользователи настраивают некоторые аспекты приложения Microsoft Teams с помощью страницы конфигурации и используют эту конфигурацию в рамках следующих действий:

* Вкладка чата канала или группы: соберите `contentUrl` сведения от пользователей и задайте отображаемую страницу содержимого.
* Расширение [сообщения](~/messaging-extensions/what-are-messaging-extensions.md).
* [Соединитель Office 365.](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configure-a-channel-or-group-chat-tab"></a>Настройка вкладки чата канала или группы

Приложение должно ссылаться на [клиентский пакет SDK Microsoft Teams JavaScript и](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) вызывать его`microsoft.initialize()`. Используемые URL-адреса должны быть защищены конечными точками HTTPS и доступны из облака.

### <a name="example"></a>Пример

Пример страницы конфигурации показан на следующем рисунке:

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

Следующий код является примером соответствующего кода для страницы конфигурации:

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

Нажмите **кнопку "Выбрать серый** " **или "** Красный" на странице конфигурации, чтобы отобразить содержимое вкладки с серым или красным значком.

На следующем рисунке отображается содержимое вкладки с **выбранным серым** значком:

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

На следующем рисунке отображается содержимое вкладки с **выделенным красным** значком:

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

Если выбрать соответствующую кнопку, активируется `saveGray()` `saveRed()`либо вызывается следующее:

* Задайте `settings.setValidityState(true)` значение true.
* Инициируется `microsoftTeams.settings.registerOnSaveHandler()` обработчик событий.
* **Сохранение** на странице конфигурации приложения включено.

Код страницы конфигурации информирует Teams о том, что требования к конфигурации выполнены и установка может продолжаться. Когда пользователь **нажмет** кнопку "Сохранить", `settings.setSettings()` параметры параметра будут заданы, как определено интерфейсом `Settings` . Дополнительные сведения см. в [интерфейсе параметров](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true). `saveEvent.notifySuccess()` вызывается, чтобы указать, что URL-адрес содержимого успешно разрешен.

>[!NOTE]
>
>* У вас есть 30 секунд для завершения операции сохранения (обратный вызов для registerOnSaveHandler) до истечения времени ожидания. По истечении времени ожидания появится общее сообщение об ошибке.
>* При регистрации обработчика сохранения с помощью `microsoftTeams.settings.registerOnSaveHandler()`обратного `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` вызова необходимо вызвать или указать результат конфигурации.
>* Если обработчик сохранения не зарегистрирован, `saveEvent.notifySuccess()` вызов выполняется автоматически, когда пользователь нажмет кнопку **"Сохранить"**.

### <a name="get-context-data-for-your-tab-settings"></a>Получение данных контекста для параметров вкладки

Для отображения соответствующего содержимого на вкладке требуются контекстные сведения. Контекстная информация еще больше повышает привлекательность вкладки, предоставляя более настраиваемый пользовательский интерфейс.

Дополнительные сведения о свойствах, используемых для настройки вкладок, см. в [контекстном интерфейсе](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true). Соберите значения переменных данных контекста двумя способами:

* Вставьте заполнители строки запроса URL-адреса `configurationURL`в манифест.

* Используйте метод [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)`microsoftTeams.getContext((context) =>{})`.

#### <a name="insert-placeholders-in-the-configurationurl"></a>Вставка заполнителей в `configurationUrl`

Добавьте заполнители контекстного интерфейса в базу `configurationUrl`. Например:

##### <a name="base-url"></a>Базовый URL-адрес

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>Базовый URL-адрес со строками запроса

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

После отправки страницы Teams заполнители строки запроса соответствующими значениями. Включите логику на странице конфигурации для получения и использования этих значений. Дополнительные сведения о работе со строками запросов URL-адресов см. в [разделе URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) в веб-документации MDN. В следующем примере кода показано, как извлечь значение из `configurationUrl` свойства:

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Использование функции `getContext()` для получения контекста

Функция `microsoftTeams.getContext((context) => {})` извлекает интерфейс [контекста при](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) вызове.

В следующем коде приведен пример добавления этой функции на страницу конфигурации для получения значений контекста:

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

Прежде чем разрешить пользователю настраивать приложение, необходимо выполнить проверку подлинности. В противном случае содержимое может включать источники с протоколами проверки подлинности. Дополнительные сведения см. в статье о проверке подлинности [пользователя на Microsoft Teams.](~/tabs/how-to/authentication/auth-flow-tab.md) Используйте контекстную информацию для создания запросов проверки подлинности и URL-адресов страниц авторизации. Убедитесь, что все домены, используемые на страницах вкладок, перечислены в массиве `manifest.json` `validDomains` .

## <a name="modify-or-remove-a-tab"></a>Изменение или удаление вкладки

Задайте `canUpdateConfiguration` `true`для свойства манифеста значение, которое позволяет пользователям изменять, перенастраить или переименовывать вкладку канала или группы. Кроме того, укажите, что происходит с содержимым при удалении вкладки, `removeUrl` включив в приложение страницу параметров удаления и указав значение свойства в конфигурации  `setSettings()` . Пользователь может удалить личные вкладки, но не может изменить их. Дополнительные сведения см. [в статье о создании страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md).

`setSettings()` Microsoft Teams конфигурации для страницы удаления:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a>Мобильные приложения

Если вы решили, чтобы вкладка канала или группы отображались на Teams мобильных клиентов, `setSettings()` конфигурация должна иметь значение `websiteUrl`для . Дополнительные сведения см [. в руководстве по вкладке на мобильных устройствах](~/tabs/design/tabs-mobile.md).

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>См. также

* [Teams вкладок](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Создать страницу контента](~/tabs/how-to/create-tab-pages/content-page.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
