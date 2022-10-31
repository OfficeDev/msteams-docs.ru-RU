---
title: Создать страницу конфигурации
author: surbhigupta
description: Создание страницы конфигурации для сбора сведений от пользователя. Кроме того, можно получить данные контекста для вкладок Microsoft Teams, узнать о проверке подлинности, изменить или удалить вкладки.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 51e5ef0a6752ab70ede4d2da699f78910c08f6c9
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791709"
---
# <a name="create-a-configuration-page"></a>Создать страницу конфигурации

Страница конфигурации — это особый тип [страницы содержимого](content-page.md). Пользователи настраивают некоторые аспекты приложения Microsoft Teams с помощью страницы конфигурации и используют эту конфигурацию в составе следующих элементов.

* Вкладка канала или группового чата: сбор сведений от пользователей и настройка `contentUrl` отображаемой страницы содержимого.
* [Расширение для сообщений](~/messaging-extensions/what-are-messaging-extensions.md).
* [Соединитель Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="configure-a-channel-or-group-chat-tab"></a>Настройка вкладки канала или группового чата

Приложение должно ссылаться на [клиентский пакет SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client) и вызывать `app.initialize()`. Используемые URL-адреса должны быть защищены конечными точками HTTPS и доступны из облака.

### <a name="example"></a>Пример

Пример страницы конфигурации показан на следующем изображении.

:::image type="content" source="../../../assets/images/tab-images/configuration-page.png" alt-text="Снимок экрана: страница конфигурации.":::

Следующий код является примером соответствующего кода для страницы конфигурации.

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

```html
<head>
    <script src="https://res.cdn.office.net/teams-js/2.2.0/js/MicrosoftTeams.min.js" 
      integrity="sha384yBjE++eHeBPzIg+IKl9OHFqMbSdrzY2S/LW3qeitc5vqXewEYRWegByWzBN/chRh" 
      crossorigin="anonymous" >
    </script>
<body>
    <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
    <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
    <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

    <script>
        await microsoftTeams.app.initialize();
        let saveGray = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                const configPromise = pages.config.setConfig({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/gray",
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                configPromise.
                    then((result) => {saveEvent.notifySuccess()}).
                    catch((error) => {saveEvent.notifyFailure("failure message")});
            });
        }

        let saveRed = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                const configPromise = pages.config.setConfig({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/red",
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                configPromise.
                    then((result) => {saveEvent.notifySuccess();}).
                    catch((error) => {saveEvent.notifyFailure("failure message")});
            });
        }

        let gr = document.getElementById("gray").style;
        let rd = document.getElementById("red").style;

        const colorClickGray = () => {
            gr.display = "block";
            rd.display = "none";
            microsoftTeams.pages.config.setValidityState(true);
            saveGray()
        }

        const colorClickRed = () => {
            rd.display = "block";
            gr.display = "none";
            microsoftTeams.pages.config.setValidityState(true);
            saveRed();
        }
    </script>
    ...
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS версии 1](#tab/teamsjs-v1)

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

***
Нажмите кнопку **Выбрать серый** или **Выбрать красный** на странице конфигурации, чтобы отобразить содержимое вкладки с серым или красным значком.

На следующем изображении показано содержимое вкладки с выбранным **серым** значком.

:::image type="content" source="../../../assets/images/tab-images/configure-tab-with-gray.png" alt-text="Снимок экрана: вкладка &quot;Настройка&quot; с выделением серого цвета.":::

На следующем изображении показано содержимое вкладки с выбранным **красным** значком.

:::image type="content" source="../../../assets/images/tab-images/configure-tab-with-red.png" alt-text="Снимок экрана: вкладка &quot;Настройка&quot; с выделением красного цвета.":::

Нажатие соответствующей кнопки запускает `saveGray()` или `saveRed()` и вызывает следующее.

* Для `pages.config.setValidityState(true)` устанавливается значение true.
* Инициируется обработчик событий `pages.config.registerOnSaveHandler()`.
* **Сохранение** на странице конфигурации приложения, если эта функция включена.

Код страницы конфигурации сообщает Teams о том, что требования к конфигурации выполнены, и установка может продолжиться. Когда пользователь нажимает кнопку **Сохранить**, настраиваются параметры `pages.config.setConfig()`, как определено интерфейсом `Config`. Дополнительные сведения см. в разделе [Интерфейс конфигурации](/javascript/api/@microsoft/teams-js/pages.config?). `saveEvent.notifySuccess()` вызывается, чтобы указать, что URL-адрес содержимого успешно разрешен.

>[!NOTE]
>
>* У вас есть 30 секунд, чтобы завершить операцию сохранения (обратный вызов ) `registerOnSaveHandler`до истечения времени ожидания. По истечении времени ожидания появится общее сообщение об ошибке.
>* Если вы регистрируете обработчик сохранения с помощью `registerOnSaveHandler()`, обратный вызов должен вызвать `saveEvent.notifySuccess()` или `saveEvent.notifyFailure()`, чтобы указать результат конфигурации.
>* Если вы не регистрируете обработчик сохранения, вызов `saveEvent.notifySuccess()` выполняется автоматически, когда пользователь нажимает кнопку **Сохранить**.
>* Убедитесь, что у вас есть уникальный .`entityId` Повторяющиеся `entityId` перенаправления на первый экземпляр вкладки.

### <a name="get-context-data-for-your-tab-settings"></a>Получение контекстных данных для параметров вкладки

Чтобы отображать соответствующее содержимое, вкладке требуется контекстная информация. Контекстная информация повышает привлекательность вашей вкладки, предоставляя более персонализированный пользовательский интерфейс.

Дополнительные сведения о свойствах, используемых для настройки вкладок, см. в статье [Контекстный интерфейс](/javascript/api/@microsoft/teams-js/app.context?view=msteams-client-js-latest&preserve-view=true). Соберите значения переменных данных контекста двумя способами:

* Вставьте заполнители строк запроса URL-адреса в `configurationURL` вашего манифеста.

* Используйте метод [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `app.getContext()`.

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

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

```html
<script>
   await microsoftTeams.app.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

# <a name="teamsjs-v1"></a>[TeamsJS версии 1](#tab/teamsjs-v1)

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

***

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Использование функции `getContext()` для получения контекста

Функция `app.getContext()` возвращает обещание, которое разрешается с объектом [интерфейса контекста](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest&preserve-view=true) .

В следующем коде приведен пример добавления этой функции на страницу конфигурации для получения значений контекста.

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script type="module">
    import {app} from 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js';
    const contextPromise = app.getContext();
    contextPromise.
        then((context) => {
            let userId = document.getElementById('user');
            userId.innerHTML = context.user.userPrincipalName;
        }).
        catch((error) => {/*Unsuccessful operation*/});
</script>
...
```

# <a name="teamsjs-v1"></a>[TeamsJS версии 1](#tab/teamsjs-v1)

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

***

## <a name="context-and-authentication"></a>Контекст и проверка подлинности

Прежде чем разрешить пользователю настраивать ваше приложение, выполните проверку подлинности. В противном случае ваше содержимое может включать источники со своими протоколами проверки подлинности. Дополнительные сведения см. в статье о [проверке подлинности пользователя на вкладке Microsoft Teams](~/tabs/how-to/authentication/auth-flow-tab.md). Используйте контекстную информацию для создания запросов проверки подлинности и URL-адресов страниц авторизации. Убедитесь, что все домены, используемые на страницах вкладок, перечислены в массиве `manifest.json` и `validDomains`.

## <a name="modify-or-remove-a-tab"></a>Изменение или удаление вкладки

Задайте для свойства манифеста `canUpdateConfiguration` значение `true`. Это позволяет пользователям изменять или перенастраивать вкладку канала или группы. Вы можете переименовать вкладку только через пользовательский интерфейс Teams. Сообщите пользователю о влиянии на содержимое при удалении вкладки. Для этого включите в приложение страницу параметров удаления и задайте значение свойства `removeUrl` в конфигурации `setConfig()` (ранее — `setSettings()`). Пользователь может удалять личные вкладки, но не может изменять их. Дополнительные сведения см. в статье [Создание страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md).

Конфигурация Microsoft Teams `setConfig()` (ранее `setSettings()`) для страницы удаления:

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

```javascript
import { pages } from "@microsoft/teams-js";
const configPromise = pages.config.setConfig({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
configPromise.
    then((result) => {/*Successful operation*/).
    catch((error) => {/*Unsuccessful operation*/});
```

# <a name="teamsjs-v1"></a>[TeamsJS версии 1](#tab/teamsjs-v1)

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

***

## <a name="mobile-clients"></a>Мобильные приложения

Если вы выбрали вариант отображения вкладки канала или группы в мобильных клиентах Teams, конфигурация `setConfig()` должна содержать значение для `websiteUrl`. Дополнительные сведения см. в [руководстве по вкладкам на мобильных устройствах](~/tabs/design/tabs-mobile.md).

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Создание страницы контента](~/tabs/how-to/create-tab-pages/content-page.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
