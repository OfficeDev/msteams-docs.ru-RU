---
title: Создать страницу конфигурации
author: laujan
description: создание страницы конфигурации.
keywords: Настраиваемый канал группы вкладок teams
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c041c311245bb5bfc5e2655ef8d596b2839fdb70
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731967"
---
# <a name="create-a-configuration-page"></a>Создать страницу конфигурации

Страница конфигурации — это специальный тип страницы [содержимого,](content-page.md) который позволяет пользователям настраивать некоторые аспекты приложения Teams. Как правило, они используются в составе:

* Вкладка канала или группового чата — страница конфигурации позволяет собирать сведения от пользователей и устанавливать отображаемую `contentUrl` страницу содержимого.
* Расширение [для обмена сообщениями](~/messaging-extensions/what-are-messaging-extensions.md)
* [Соединители Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>Настройка вкладки чата канала или группы

Страница конфигурации информирует страницу содержимого о том, как она должна отрисовки. Приложение должно ссылаться на [клиентский SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и вызывать `microsoft.initialize()` его. Кроме того, URL-адреса должны быть защищены конечными точками HTTPS и доступны из облака. Ниже приведен пример страницы конфигурации.

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

Здесь пользователь получает две кнопки **выбора:** "Выбрать  серый" или "Красный" для отображения содержимого вкладки с помощью красного или серого значка. При нажатии относительной кнопки активна или `saveGray()` `saveRed()` вызывается следующая кнопка:

1. За `settings.setValidityState(true)` установлено true.
1. `microsoftTeams.settings.registerOnSaveHandler()`Инициирует обработник событий.
1. **Кнопка** "Сохранить" на странице конфигурации приложения, загруженная в Teams, включена.

Этот код сообщает Teams, что требования к конфигурации выполнены и что установка может продолжиться. При **сохранения** параметры заданы в зависимости от интерфейса `settings.setSettings()` для `Settings` текущего экземпляра. Дополнительные сведения см. в [интерфейсе "Параметры".](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true) Наконец, `saveEvent.notifySuccess()` он вызван, чтобы указать, что URL-адрес контента успешно разрешен.

>[!NOTE]
>
>* Если обработель сохранения был зарегистрирован с помощью этого обработка, то он должен вызвать или указать `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` результат `saveEvent.notifyFailure()` настройки.
>* Если обработка сохранения не зарегистрирована, вызов автоматически делается сразу после того, как пользователь `saveEvent.notifySuccess()` нажал кнопку **"Сохранить".**

### <a name="get-context-data-for-your-tab-settings"></a>Получить контекстные данные для параметров вкладок

Для отображения релевантной информации на вкладке может потребоваться контекстная информация. Контекстная информация может еще больше повысить привлекательность вкладки, обеспечивая более настраиваемый пользовательский интерфейс.

Контекстный [интерфейс](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) Teams определяет свойства, которые можно использовать для настройки вкладки. Значения переменных данных контекста можно собирать двумя способами:

1. Вставьте в манифесте строки запроса `configurationURL` URL-адреса.

1. Используйте метод [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{}`

#### <a name="insert-placeholders-in-the-configurationurl"></a>Вставка в них заме- `configurationURL`

В базу можно добавить замессеры контекстного `configurationUrl` интерфейса. Например:

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

После отправки страницы в Teams будут добавлены соответствующие значения. На странице конфигурации можно включить логику для извлечения и использования этих значений. Дополнительные сведения о работе со строками запроса URL-адресов см. в [urlSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) в веб-документы MDN. Вот пример извлечения значения из вышеуказанного `configurationURL` свойства:

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Использование `getContext()` функции для извлечения контекста

При вызове функция `microsoftTeams.getContext((context) => {})` извлекает интерфейс [контекста.](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) Эту функцию можно добавить на страницу конфигурации для получения значений контекста:

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

Прежде чем разрешить пользователю настроить приложение, может потребоваться проверка подлинности, или содержимое может включать источники с собственными протоколами проверки подлинности. См. [статью "Проверка](~/tabs/how-to/authentication/auth-flow-tab.md) подлинности пользователя" на вкладке "Контекст" в Microsoft Teams. Сведения о контексте можно использовать для создания запросов проверки подлинности и URL-адресов страниц авторизации.
Убедитесь, что все домены, используемые на страницах вкладок, указаны в `manifest.json` `validDomains` массиве.

## <a name="modify-or-remove-a-tab"></a>Изменение или удаление вкладки

Поддерживаемые параметры удаления могут дополнительно уточнить пользовательский интерфейс. Вы можете позволить пользователям изменять, перенастройку или переименовывать вкладку группы или канала, задав свойству манифеста `canUpdateConfiguration` имя `true` .  Кроме того, вы можете узначить, что происходит с содержимым при удалении вкладки, включив в приложение страницу параметров удаления и задав значение свойства в конфигурации `removeUrl`  `setSettings()` (см. ниже). Личные вкладки не могут быть изменены, но могут быть выгрузлены пользователем. Дополнительные сведения см. в [подсети "Создание страницы удаления".](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="mobile-clients"></a>Мобильные приложения

Если вкладка "Канал/группа" будет отображаться на мобильных клиентах Teams, конфигурация должна иметь значение свойства `setSettings()` `websiteUrl` (см. ниже). См. [инструкции для вкладок на мобильных устройствах.](~/tabs/design/tabs-mobile.md)

Конфигурация Microsoft Teams setSettings() для страницы удаления и/или мобильных клиентов:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
