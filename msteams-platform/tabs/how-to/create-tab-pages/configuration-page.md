---
title: Создать страницу конфигурации
author: laujan
description: Создание страницы конфигурации
keywords: вкладки Teams канал группы настраиваемого канала
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 591e1aa91bd33d1a61e9d70b35fd1561368fcda4
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964608"
---
# <a name="create-a-configuration-page"></a>Создать страницу конфигурации

Страница конфигурации — это особый тип [страницы контента](content-page.md) , позволяющий пользователям настраивать некоторые аспекты приложения Teams. Обычно они используются в качестве части:

* Вкладка "канал" или "Группа чата" — страница настройки позволяет собирать сведения от пользователей и задавать `contentUrl` отображаемую страницу контента.
* [Расширение системы обмена сообщениями](~/messaging-extensions/what-are-messaging-extensions.md)
* [Соединитель Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>Настройка вкладки канала или группового чата

Страница конфигурации информирует страницу содержимого о том, как она должна отображаться. Ваше приложение должно ссылаться на [клиентский пакет SDK и вызов Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoft.initialize()` . Кроме того, ваш URL-адрес должен быть защищенными конечными точками HTTPS и доступен в облаке. Ниже приведен пример страницы конфигурации.

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

Здесь у пользователя есть два переключателя, **выберите серый** или **красный** , чтобы отобразить содержимое вкладки с помощью значка красного или серого. При нажатии кнопки относитель срабатывает `saveGray()` или `saveRed()` вызывается следующее:

1. `settings.setValidityState(true)`Для параметра задано значение true.
1. `microsoftTeams.settings.registerOnSaveHandler()`Запускается обработчик событий.
1. Кнопка **сохранить** на странице настройки приложения, отправленная в Teams, включена.

С помощью этого кода Teams вы узнаете, что требования к конфигурации выполнены, и установка может быть продолжена. При **сохранении**параметры `settings.setSettings()` задаются, как определено `Settings` интерфейсом, для текущего экземпляра (см. [интерфейс параметров](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) ). Finally `saveEvent.notifySuccess()` вызывается, чтобы показать, что URL-адрес контента успешно разрешен.

>[!NOTE]
>
>* Если обработчик сохранения зарегистрирован с помощью `microsoftTeams.settings.registerOnSaveHandler()` , обратный вызов должен вызвать `saveEvent.notifySuccess()` или `saveEvent.notifyFailure()` указать результат конфигурации.
>* Если обработчик сохранения не зарегистрирован, `saveEvent.notifySuccess()` вызов автоматически выполняется сразу после нажатия кнопки **сохранить** .

### <a name="get-context-data-for-your-tab-settings"></a>Получение данных контекста для параметров вкладки

Для отображения соответствующего контента на вкладке может потребоваться Контекстная информация. Контекстные сведения могут улучшить внешний вид вкладки, обеспечивая более настраиваемое взаимодействие с пользователем.

[Интерфейс контекста](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) Teams определяет свойства, которые можно использовать для настройки вкладки. Вы можете собирать значения переменных контекстных данных двумя способами:

1. Вставьте в манифесте заполнители строки запроса URL-адреса `configurationURL` .

1. Используйте метод [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{}` .

#### <a name="insert-placeholders-in-the-configurationurl"></a>Вставьте заполнители в поле `configurationURL`

Заполнители интерфейса контекста можно добавлять к базе `configurationUrl` . Например:

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

После отправки страницы заполнители строки запроса будут обновлены в Teams с соответствующими значениями. Вы можете включить логику на странице конфигурации, чтобы извлечь и использовать эти значения. Дополнительные сведения о работе с строками запросов URL-адресов [урлсеарчпарамс](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) в веб-документах МДН. Ниже приведен пример того, как извлечь значение из вышеуказанного `configurationURL` Свойства:

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

При вызове `microsoftTeams.getContext((context) => {})` функция получает [интерфейс контекста](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest&preserve-view=true). Вы можете добавить эту функцию на страницу конфигурации для получения значений контекста:

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

Проверка подлинности может потребоваться, прежде чем разрешить пользователю настраивать приложение или контент может включать источники с собственными протоколами проверки подлинности. Просмотреть [проверку подлинности пользователь в контексте вкладки Microsoft Teams](~/tabs/how-to/authentication/auth-flow-tab.md) можно использовать для создания URL-адресов страниц проверки подлинности и страниц авторизации.
Убедитесь, что все домены, используемые на страницах вкладок, указаны в `manifest.json` `validDomains` массиве.

## <a name="modify-or-remove-a-tab"></a>Изменение или удаление вкладки

Поддерживаемые варианты удаления могут дополнительно улучшить взаимодействие с пользователем. Вы можете разрешить пользователям изменять, перенастраивать или переименовывать вкладки группа и канал, устанавливая для свойства манифеста значение `canUpdateConfiguration` `true` .  Кроме того, вы можете указать, что происходит с содержимым при удалении вкладки, включив страницу параметров удаления в свое приложение и задав значение для `removeUrl` свойства в  `setSettings()` конфигурации (см. ниже). Личные вкладки нельзя изменить, но можно удалить пользователя. Дополнительные сведения можно найти [в разделе Создание страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md).

## <a name="mobile-clients"></a>Мобильные приложения

Если вкладка канал и группа отображается в клиентах Teams для мобильных устройств, то `setSettings()` конфигурация должна иметь значение для `websiteUrl` Свойства (см. ниже). В ближайшее время будет выпущена полная поддержка вкладок на мобильных клиентах. Чтобы подготовиться к обновлению, следуйте [указаниям для вкладок на странице Mobile](~/tabs/design/tabs-mobile.md) при создании вкладок.

Настройка Microsoft Teams Сетсеттингс () для страницы удаления и/или мобильных клиентов:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
