---
title: Получение контекста для вкладки
description: В этом модуле вы узнаете, как получить контекст пользователя для вкладок, контекста пользователя и сведений о контексте Access.
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: d6723c4733bd127dd32970e3d1059a75771c8bee
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142313"
---
# <a name="get-context-for-your-tab"></a>Получение контекста для вкладки

Для отображения соответствующего содержимого на вкладке требуются контекстные сведения:

* Основные сведения о пользователе, команде или компании.
* Сведения о языковом стандарте и теме.
* Прочитайте `entityId` или `subEntityId` определяйте, что находится на этой вкладке.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="user-context"></a>Контекст пользователя

Контекст о пользователе, команде или компании может быть особенно полезен в следующих случаях:

* Вы создаете или связываете ресурсы в приложении с указанным пользователем или командой.
* Вы инициируете поток проверки подлинности из Microsoft Azure Active Directory (Azure AD) или другого поставщика удостоверений, и вам не нужно повторно вводить имя пользователя.

Дополнительные сведения см. в статье [о проверке подлинности пользователя в Microsoft Teams](~/concepts/authentication/authentication.md).

> [!IMPORTANT]
> Хотя эти сведения о пользователе помогают обеспечить бесперебойное взаимодействие с пользователем, их не следует использовать в качестве подтверждения личности.  Например, злоумышленник может загрузить страницу в браузере и отобразить вредоносные сведения или запросы.

## <a name="access-context-information"></a>Доступ к контекстным сведениям

Доступ к контекстной информации можно получить двумя способами:

* Вставка значений заполнителей URL-адресов.
* Используйте Microsoft Teams [клиентского пакета SDK для JavaScript](/javascript/api/overview/msteams-client).

### <a name="get-context-by-inserting-url-placeholder-values"></a>Получение контекста путем вставки значений заполнителей URL-адресов

Используйте заполнители в конфигурации или в URL-адресах контента. Microsoft Teams заменяет заполнители соответствующими значениями, когда определяет фактическую конфигурацию или URL-адрес контента. Доступные заполнители включают все поля в [объекте контекста](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-1.12.1&preserve-view=true) . Распространенные сценарии:

* {entityId}: ИД, который вы предоставили для элемента на этой вкладке при [первоначальной настройке](~/tabs/how-to/create-tab-pages/configuration-page.md).
* {subEntityId}: идентификатор, указанный при создании глубокой ссылки [](~/concepts/build-and-test/deep-links.md) для определенного элемента на этой вкладке. Его необходимо использовать для восстановления до определенного состояния в сущности; например, прокрутка до или активация определенного фрагмента содержимого.
* {loginHint}: значение, подходящее в качестве указания входа для Azure AD. Обычно это имя входа текущего пользователя в домашнем клиенте.
* {userPrincipalName}: имя участника-пользователя текущего пользователя в текущем клиенте.
* {userObjectId}: Azure AD объекта текущего пользователя в текущем клиенте.
* {theme}: текущая тема пользовательского интерфейса, например `default`, или `dark``contrast`.
* {groupId}: идентификатор группы Office 365, в которой находится вкладка.
* {tid}: ИД объекта Azure AD текущего пользователя в текущем клиенте
* {locale}: текущий языковой стандарт пользователя, отформатированный как languageId-countryId(en-us).

> [!NOTE]
> Предыдущий заполнитель `{upn}` теперь не поддерживается. Для обратной совместимости в настоящее время он является синонимом для `{loginHint}`.

Например, в манифесте `configURL` вкладки, для которой задано значение атрибута `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, пользователь, выполнив вход, имеет следующие атрибуты:

* Имя **пользователя — user@example.com**.
* Идентификатор клиента компании — **e2653c-etc**.
* Они являются членами Office 365 с идентификатором **00209384 и т. д**.
* Пользователь настроит темную Teams **теме**.

При настройке вкладки Teams следующий URL-адрес:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Получение контекста с помощью Microsoft Teams JavaScript

git-issue-clarify-the-full-set-of-values-any-context-object-property-can-take Можно также получить сведения, перечисленные выше, с помощью клиентского [пакета SDK](/javascript/api/overview/msteams-client) `microsoftTeams.getContext(function(context) { /* ... */ })`Microsoft Teams JavaScript путем вызова .

В следующем коде приведен пример переменной контекста:

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The principal name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current Office 365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates if the tab is in full-screen",
    "teamType": "The type of team",
    "teamSiteUrl": "The root SharePoint site associated with the team",
    "teamSiteDomain": "The domain of the root SharePoint site associated with the team",
    "teamSitePath": "The relative path to the SharePoint site associated with the team",
    "channelRelativeUrl": "The relative path to the SharePoint folder associated with the channel",
    "sessionId": "The unique ID for the current Teams session for use in correlating telemetry data",
    "userTeamRole": "The user's role in the team",
    "isTeamArchived": "Indicates if team is archived",
    "hostClientType": "The type of host client. Possible values are android, ios, web, desktop, surfaceHub, teamsRoomsAndroid, teamsPhones, teamsDisplays rigel (deprecated, use teamsRoomsWindows instead)",
    "frameContext": "The context where tab URL is loaded (for example, content, task, setting, remove, sidePanel)",
    "sharepoint": "The SharePoint context is available only when hosted in SharePoint",
    "tenantSKU": "The license type for the current user tenant. Possible values are enterprise, free, edu, unknown",
    "userLicenseType": "The license type for the current user. Possible values are E1, E3, and E5 enterprise plans",
    "parentMessageId": "The parent message ID from which this task module is launched",
    "ringId": "The current ring ID",
    "appSessionId": "The unique ID for the current session used for correlating telemetry data",
    "isCallingAllowed": "Indicates if calling is allowed for the current logged in user",
    "isPSTNCallingAllowed": "Indicates if PSTN calling is allowed for the current logged in user",
    "meetingId": "The meeting ID used by tab when running in meeting context",
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel",
    "isMultiWindow": "The indication whether the tab is in a pop out window"
}
```

Вы также можете получить перечисленные выше сведения с помощью Microsoft Teams [клиентского пакета SDK для JavaScript](/javascript/api/overview/msteams-client), вызвав функцию`app.getContext()`. Дополнительные сведения см. в свойствах [интерфейса контекста](/javascript/api/@microsoft/teams-js/app.context?view=msteams-client-js-latest&preserve-view=true).


## <a name="retrieve-context-in-private-channels"></a>Получение контекста в частных каналах

Когда страница содержимого загружается в закрытый канал, данные, получаемые при вызове, `getContext` замаскируются для защиты конфиденциальности канала.

Следующие поля изменяются, если страница содержимого находится в частном канале:

* `groupId`: не определено для частных каналов
* `teamId`: задайте значение threadId закрытого канала.
* `teamName`: задайте имя частного канала.
* `teamSiteUrl`: задайте URL-адрес отдельного уникального SharePoint для частного канала.
* `teamSitePath`: задайте путь к отдельному уникальному сайту SharePoint для частного канала.
* `teamSiteDomain`: задайте домен уникального домена SharePoint для частного канала.

Если на странице используется любое из этих значений, `channelType` `Private` значение поля должно быть таким, чтобы определить, загружена ли страница в частный канал и может ли она отвечать соответствующим образом.

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>Получение контекста в Microsoft Teams Связи общих каналах

> [!NOTE]
> В настоящее Microsoft Teams Связи общие каналы доступны только в [предварительной версии разработчика](../../resources/dev-preview/developer-preview-intro.md).

Когда страница содержимого загружается в общий Microsoft Teams Связи канале, данные, получаемые при вызове, `getContext` изменяются из-за уникального списка пользователей в общих каналах.

Следующие поля изменяются, если страница содержимого находится в общем канале:

* `groupId`: не определено для общих каналов.
* `teamId`: задайте для `threadId` команды общий доступ к каналу для текущего пользователя. Если у пользователя есть доступ к нескольким командам, задается команда, `teamId` которая размещает (создает) общий канал.
* `teamName`: задайте имя команды, канал является общим для текущего пользователя. Если у пользователя есть доступ к нескольким командам, задается команда, `teamName` которая размещает (создает) общий канал.
* `teamSiteUrl`: задайте URL-адрес отдельного уникального SharePoint для общего канала.
* `teamSitePath`: задайте путь к отдельному уникальному SharePoint для общего канала.
* `teamSiteDomain`: задайте домен отдельного уникального SharePoint для общего канала.

Помимо этих изменений полей, для общих каналов доступны два новых поля:

* `hostTeamGroupId`: задайте связанное `groupId` с группой размещения или командой, создающей общий канал. Это свойство может API Graph вызовы Майкрософт для получения членства в общем канале.
* `hostTeamTenantId`: задайте связанное `tenantId` с группой размещения или командой, создающей общий канал. На это `tid` `getContext` свойство можно перекрестно ссылаться с идентификатором клиента текущего пользователя, найденным в поле ,чтобы определить, является ли пользователь внутренним или внешним для клиента группы размещения.

Если на странице используется любое из этих значений, `channelType` `Shared` значение поля должно быть таким, чтобы определить, загружена ли страница в общем канале и может ли она отвечать соответствующим образом.

> [!NOTE]
> Каждый раз, когда пользователь перезапускает или перезагружает рабочий или веб-клиент Teams, создается новый sessionID, который отслеживается сеансом Teams, а когда пользователь выходит из приложений Teams и перезагружает его на платформе Teams, создается новый sessionID приложения, который отслеживается сеансом приложения.

## <a name="handle-theme-change"></a>Обработка изменения темы

Вы можете зарегистрировать приложение для получения сведений об изменении темы путем вызова `app.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

Аргументом `theme` в функции является строка со значением `default`, `dark`или `contrast`.

## <a name="next-step"></a>Следующее действие

> [!div class="nextstepaction"]
> [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>См. также

* [Рекомендации по проектированию вкладок](../../tabs/design/tabs.md)
* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Использование модулей задач во вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
