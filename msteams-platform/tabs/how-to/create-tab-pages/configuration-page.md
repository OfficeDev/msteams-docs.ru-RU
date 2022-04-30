---
title: Создать страницу конфигурации
author: surbhigupta
description: Узнайте, как создать страницу конфигурации для настройки параметров канала или группового чата, например получения данных контекста, вставки заполнителей и проверки подлинности с помощью примеров кода.
keywords: настраиваемый канал группы вкладок Teams
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 912e38fc63d8c897f086d27362ad249688ce7ce9
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111642"
---
# <a name="create-a-configuration-page"></a>Создать страницу конфигурации

Страница конфигурации — это особый тип [страницы содержимого](content-page.md). Пользователи настраивают некоторые аспекты приложения Microsoft Teams с помощью страницы конфигурации и используют эту конфигурацию в составе следующих элементов.

* Вкладка канала или группового чата: сбор сведений от пользователей и настройка `contentUrl` отображаемой страницы содержимого.
* [Расширение для сообщений](~/messaging-extensions/what-are-messaging-extensions.md).
* [Соединитель Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="configure-a-channel-or-group-chat-tab"></a>Настройка вкладки канала или группового чата

Приложение должно ссылаться на [клиентский пакет SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и вызывать `microsoft.initialize()`. Используемые URL-адреса должны быть защищенными конечными точками HTTPS, доступными из облака.

### <a name="example"></a>Пример

Пример страницы конфигурации показан на следующем изображении.

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

Следующий код является примером соответствующего кода для страницы конфигурации.

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

Нажмите кнопку **Выбрать серый** или **Выбрать красный** на странице конфигурации, чтобы отобразить содержимое вкладки с серым или красным значком.

На следующем изображении показано содержимое вкладки с выбранным **серым** значком.

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

На следующем изображении показано содержимое вкладки с выбранным **красным** значком.

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

Нажатие соответствующей кнопки запускает `saveGray()` или `saveRed()` и вызывает следующее.

* Для `settings.setValidityState(true)` устанавливается значение true.
* Инициируется обработчик событий `microsoftTeams.settings.registerOnSaveHandler()`.
* **Сохранение** на странице конфигурации приложения, если эта функция включена.

Код страницы конфигурации информирует Teams о том, что требования к конфигурации выполнены и установка может продолжаться. Когда пользователь нажимает кнопку **Сохранить**, настраиваются параметры `settings.setSettings()`, как определено интерфейсом `Settings`. Дополнительные сведения см. в статье [Интерфейсе параметров](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true). `saveEvent.notifySuccess()` вызывается, чтобы указать, что URL-адрес содержимого успешно разрешен.

>[!NOTE]
>
>* У вас есть 30 секунд для завершения операции сохранения (обратный вызов в registerOnSaveHandler) до истечения времени ожидания. По истечении времени ожидания появится общее сообщение об ошибке.
>* Если вы регистрируете обработчик сохранения с помощью `microsoftTeams.settings.registerOnSaveHandler()`, обратный вызов должен вызвать `saveEvent.notifySuccess()` или `saveEvent.notifyFailure()`, чтобы указать результат конфигурации.
>* Если вы не регистрируете обработчик сохранения, вызов `saveEvent.notifySuccess()` выполняется автоматически, когда пользователь нажимает кнопку **Сохранить**.

### <a name="get-context-data-for-your-tab-settings"></a>Получение контекстных данных для параметров вкладки

Чтобы отображать соответствующее содержимое, вкладке требуется контекстная информация. Контекстная информация повышает привлекательность вашей вкладки, предоставляя более персонализированный пользовательский интерфейс.

Дополнительные сведения о свойствах, используемых для настройки вкладок, см. в статье [Контекстный интерфейс](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true). Соберите значения переменных данных контекста двумя способами:

* Вставьте заполнители строк запроса URL-адреса в `configurationURL` вашего манифеста.

* Используйте метод [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`.

#### <a name="insert-placeholders-in-the-configurationurl"></a>Вставка заполнителей в `configurationUrl`

Добавьте заполнители контекстного интерфейса в базовый `configurationUrl`. Например:

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

После отправки вашей страницы приложение Teams обновляет заполнители строк запроса соответствующими значениями. Добавьте логику на странице конфигурации для получения и использования этих значений. Дополнительные сведения о работе со строками запросов URL-адресов см. в разделе [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) веб-документации MDN. В следующем примере кода представлен способ извлечения значения из свойства `configurationUrl`.

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

При вызове функция `microsoftTeams.getContext((context) => {})` получает [контекстный интерфейс](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).

В следующем коде приведен пример добавления этой функции на страницу конфигурации для получения значений контекста.

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

Прежде чем разрешить пользователю настраивать ваше приложение, выполните проверку подлинности. В противном случае ваше содержимое может включать источники со своими протоколами проверки подлинности. Дополнительные сведения см. в статье о [проверке подлинности пользователя на вкладке Microsoft Teams](~/tabs/how-to/authentication/auth-flow-tab.md). Используйте контекстную информацию для создания запросов проверки подлинности и URL-адресов страниц авторизации. Убедитесь, что все домены, используемые на страницах вкладок, перечислены в массиве `manifest.json` и `validDomains`.

## <a name="modify-or-remove-a-tab"></a>Изменение или удаление вкладки

Присвойте свойству `canUpdateConfiguration` вашего манифеста значение `true`, которое позволяет пользователям изменить, перенастроить или переименовать вкладку канала или группы. Кроме того, укажите, что происходит с содержимым при удалении вкладки, включив в приложение страницу параметров удаления и настроив значение свойства `removeUrl` в конфигурации `setSettings()`. Пользователь может удалить личные вкладки, но не может изменить их. Дополнительные сведения см. в статье [Создание страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md).

Конфигурация `setSettings()` Microsoft Teams для страницы удаления:

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

Если вы выбрали вариант отображения вкладки канала или группы в мобильных клиентах Teams, конфигурация `setSettings()` должна содержать значение для `websiteUrl`. Дополнительные сведения см. в [руководстве по вкладкам на мобильных устройствах](~/tabs/design/tabs-mobile.md).

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Создание страницы контента](~/tabs/how-to/create-tab-pages/content-page.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
