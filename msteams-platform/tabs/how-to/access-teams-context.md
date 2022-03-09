---
title: Получение контекста для вкладки
description: В этой статье описывается, как получить контекст пользователя для вкладок
ms.localizationpriority: medium
ms.topic: how-to
keywords: пользовательский контекст вкладок teams
ms.openlocfilehash: 4c18ba7f7e7dbb90f6a357a567b2b6145afcd827
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356268"
---
# <a name="get-context-for-your-tab"></a>Получение контекста для вкладки

Для отображения соответствующего контента на вкладке требуются контекстные сведения:

* Основные сведения о пользователе, команде или компании.
* Сведения о locale и теме.
* Прочитайте или `entityId` `subEntityId` определяйте, что находится на этой вкладке.

## <a name="user-context"></a>Контекст пользователя

Контекст о пользователе, команде или компании может быть особенно полезен, когда:

* Вы создаете или связываете ресурсы в приложении с указанным пользователем или командой.
* Вы инициируете поток проверки подлинности из Microsoft Azure Active Directory (Azure AD) или другого поставщика удостоверений, и не требуется, чтобы пользователь снова вводил свое имя пользователя. 

Дополнительные сведения см. в [записи проверки](~/concepts/authentication/authentication.md) подлинности пользователя в Microsoft Teams.

> [!IMPORTANT]
> Хотя эта информация пользователя может помочь обеспечить плавный пользовательский опыт, вы не должны использовать его в качестве доказательства удостоверения.  Например, злоумышленник может загрузить страницу в браузер и отрисовки вредных сведений или запросов.

## <a name="access-context-information"></a>Доступ к данным контекста

Доступ к контекстной информации можно получить двумя способами:

* Вставьте значения местообнамерщика URL- адресов.
* Используйте [SDK Microsoft Teams Клиента JavaScript](/javascript/api/overview/msteams-client).

### <a name="get-context-by-inserting-url-placeholder-values"></a>Получить контекст, вставив значения задатки URL-адресов

Используйте заполнители в конфигурации или в URL-адресах контента. Microsoft Teams заменяет заполнители соответствующими значениями, когда определяет фактическую конфигурацию или URL-адрес контента. Доступные держатели включают все поля на [объекте контекста](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) . Распространенные сценарии:

* {entityId}: ИД, который вы предоставили для элемента на этой вкладке при [первоначальной настройке](~/tabs/how-to/create-tab-pages/configuration-page.md).
* {subEntityId}: ID, который вы предоставили при создании глубокой ссылки для определенного элемента в этой вкладке.[](~/concepts/build-and-test/deep-links.md) Это необходимо использовать для восстановления определенного состояния в объекте; например, прокрутка или активация определенного фрагмента контента.
* {LoginHint}: значение, подходящее в качестве подсказки для входа в Azure AD. Обычно это имя входа текущего пользователя в домашнем клиенте.
* {userPrincipalName}: основное имя пользователя текущего пользователя в текущем клиенте.
* {userObjectId}: ID объекта Azure AD текущего пользователя текущего клиента.
* {theme}: текущая тема пользовательского интерфейса (пользовательского интерфейса), например `default`, или `dark``contrast`.
* {groupId}: ID группы Office 365, в которой находится вкладка.
* {tid}: ИД объекта Azure AD текущего пользователя в текущем клиенте
* {locale}: текущий локализ пользователя, форматированный как languageId-countryId(ru-ru).

> [!NOTE]
> Предыдущий заполнитель `{upn}` теперь не поддерживается. Для обратной совместимости в настоящее время он является синонимом для `{loginHint}`.

Например, в манифесте вкладки `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`вы за установите атрибут, чтобы пользователь, вписав его, получил следующие атрибуты:

* Имя пользователя — **user@example.com**.
* Их ID клиента компании **e2653c-etc**.
* Они являются членами группы Office 365 id **00209384-etc**.
* Пользователь установил свою Teams **темную** тему.

При настройке вкладки Teams следующий URL-адрес:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Получить контекст с помощью Microsoft Teams JavaScript

Вы также можете получить сведения, перечисленные выше, с помощью [клиентского SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client), вызвав `microsoftTeams.getContext(function(context) { /* ... */ })`.

В следующем коде приводится пример переменной контекста:

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
    "hostClientType": "The type of host client. Possible values are android, ios, web, desktop, rigel",
    "frameContext": "The context where tab URL is loaded (for example, content, task, setting, remove, sidePanel)",
    "sharepoint": "The SharePoint context is available only when hosted in SharePoint",
    "tenantSKU": "The license type for the current user tenant. Possible values are enterprise, free, edu, unknown",
    "userLicenseType": "The license type for the current user",
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

## <a name="retrieve-context-in-private-channels"></a>Извлечение контекста в частных каналах

Когда страница контента загружается в частный канал, данные, полученные от вызова, `getContext` запутываются для защиты конфиденциальности канала. 

Если страница контента находится в частном канале, меняются следующие поля:

* `groupId`: Неопределяемая для частных каналов
* `teamId`: Установите для threadId частного канала
* `teamName`: Установите имя частного канала
* `teamSiteUrl`: Установите URL-адрес отдельного, уникального SharePoint для частного канала
* `teamSitePath`: Установите путь отдельного, уникального SharePoint для частного канала
* `teamSiteDomain`: Установите домен отдельного, уникального SharePoint для частного канала

Если на вашей странице используется любое из этих значений, `channelType` `Private` значение поля должно быть, чтобы определить, загружена ли страница в частном канале и может ли она отвечать соответствующим образом.

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>Извлечение контекста Microsoft Teams Подключение общих каналах

> [!NOTE]
> В настоящее время Microsoft Teams Подключение общие каналы находятся только [в предварительном просмотре разработчика](../../resources/dev-preview/developer-preview-intro.md).

При загрузке страницы контента в Microsoft Teams Подключение канале, данные, полученные от вызова, `getContext` изменяются из-за уникального реестра пользователей в общих каналах. 

Если страница контента находится в общем канале, меняются следующие поля:

* `groupId`: Неопределяемая для общих каналов.
* `teamId`. Установите для `threadId` команды канал общий для текущего пользователя. Если у пользователя есть доступ к нескольким командам, `teamId` за набором для группы, которая создает (создает) общий канал.
* `teamName`. Установите имя команды, канал является общим для текущего пользователя. Если у пользователя есть доступ к нескольким командам, `teamName` за набором для группы, которая создает (создает) общий канал.
* `teamSiteUrl`: Установите URL-адрес отдельного уникального SharePoint для общего канала.
* `teamSitePath`: Установите путь отдельного, уникального SharePoint для общего канала.
* `teamSiteDomain`: Установите домен отдельного, уникального SharePoint для общего канала.

В дополнение к этим изменениям поля доступны два новых поля для общих каналов:

* `hostTeamGroupId`: Установите связанное `groupId` с командой хостинга или командой, создав общий канал. Свойство может заставить вызовы API Graph Майкрософт извлечения членства общего канала.
* `hostTeamTenantId`: Установите связанное `tenantId` с командой хостинга или командой, создав общий канал. Свойство можно пересечено `tid` `getContext` с ИД клиента текущего пользователя, найденного в поле, чтобы определить, является ли пользователь внутренним или внешним для клиента группы размещения.

Если на странице используется любое из этих значений, `channelType` `Shared` значение поля должно быть, чтобы определить, загружена ли страница в общем канале и может ли она отвечать соответствующим образом.

## <a name="handle-theme-change"></a>Обработка изменения темы

Вы можете зарегистрировать приложение, чтобы быть информированным, если тема изменяется по вызову `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

Аргументом `theme` в функции является строка со значением `default`, или `dark``contrast`.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>См. также

* [Рекомендации по разработке вкладок](../../tabs/design/tabs.md)
* [Teams вкладки](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Использование модулей задач во вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
