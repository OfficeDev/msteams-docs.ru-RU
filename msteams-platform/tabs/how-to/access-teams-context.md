---
title: Получение контекста для вкладки
description: В этой статье описывается, как получить контекст пользователя для вкладок
keywords: пользовательский контекст вкладок teams
ms.openlocfilehash: 18c8541e948f206fcdddc3a942325e2f5d6e3e5c
ms.sourcegitcommit: 309823e6911b4e8e307493cbd59880fe69a4dca3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2020
ms.locfileid: "49727165"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a>Получение контекста для вкладки Microsoft Teams

Чтобы отображать соответствующее содержимое, вкладке может быть нужна контекстная информация.

* Или основные сведения о пользователе, группе или компании.
* Вкладке также могут требоваться сведения о языковом стандарте и теме оформления.
* Возможно, на вкладке нужно написать `entityId` или `subEntityId`, чтобы пользователи могли сразу понять, что на ней находится.

## <a name="user-context"></a>Контекст пользователя

Контекст, описывающий пользователя, группу или компанию, может быть особенно полезен, когда:

* Необходимо создать ресурсы в приложении или связать их с указанным пользователем или группой.
* Вы хотите инициировать поток проверки подлинности для Azure Active Directory или другого поставщика удостоверений и не хотите заставлять пользователя снова вводить логин (Дополнительные сведения о проверке подлинности на вкладке Microsoft Teams см. в статье [Проверка подлинности пользователя на вкладке Microsoft Teams](~/concepts/authentication/authentication.md).)

> [!IMPORTANT]
> Хотя эти сведения о пользователях помогают обеспечить плавное взаимодействие с пользователем, *не надо* использовать их в качестве подтверждения личности. Например, злоумышленник может загрузить страницу в "плохом браузере" и показать опасные сведения или ввести злонамеренные запросы.

## <a name="accessing-context"></a>Доступ к контексту

Доступ к контекстной информации можно получить двумя способами:

* Вставлять значения заполнителей в URL-адреса
* Использовать [клиентский SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client)

### <a name="getting-context-by-inserting-url-placeholder-values"></a>Получение контекста путем вставки значений-заполнителей в URL-адреса

Используйте заполнители в конфигурации или в URL-адресах контента. Microsoft Teams заменяет заполнители соответствующими значениями, когда определяет фактическую конфигурацию или URL-адрес контента. В число доступных заполнителей входят все поля объекта [Контекст](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true). Распространенные сценарии:

* {entityId}: ИД, который вы предоставили для элемента на этой вкладке при [первоначальной настройке](~/tabs/how-to/create-tab-pages/configuration-page.md).
* {subEntityId}: ИД, предоставленный при создании [прямой ссылки](~/concepts/build-and-test/deep-links.md) для определенного элемента _внутри_ этой вкладки. Его следует использовать для восстановления определенного состояния объекта, например прокрутки или активации определенного фрагмента содержимого.
* {loginHint}: значение, подходящее в качестве подсказки для входа в Azure AD. Обычно это логин текущего пользователя в его домашнем клиенте.
* {userPrincipalName}: имя субъекта-пользователя данного пользователя в данном клиенте.
* {userObjectId}: ИД объекта Azure AD данного пользователя в данном клиенте.
* {theme}: текущая тема пользовательского интерфейса, например `default`, `dark` или `contrast`.
* {groupId}: ИД группы Office 365, в которой находится вкладка.
* {tid}: ИД объекта Azure AD текущего пользователя в текущем клиенте
* {locale}: текущий языковой стандарт пользователя, отформатированный как languageId-countryId (например, en-us).

>[!NOTE]
>Предыдущий заполнитель `{upn}` теперь не поддерживается. Для обратной совместимости в настоящее время он является синонимом для `{loginHint}`.

Например, предположим, что в манифесте вкладки для атрибута `configURL` установлено значение

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

При этом у пользователя, вошедшего в систему, есть следующие атрибуты:

* Имя пользователя : "user@example.com"
* ИД клиента компании: "e2653c-etc"
* Пользователь входит в группу Office 365 с ИД "00209384-etc"
* Пользователь установил тему Teams "темный"

При настройке вкладки Teams вызывает этот URL-адрес:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a>Получение контекста с помощью библиотеки JavaScript для Microsoft Teams

Вы также можете получить сведения, перечисленные выше, с помощью [клиентского SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client), вызвав `microsoftTeams.getContext(function(context) { /* ... */ })`.

Контекстная переменная должна выглядеть приблизительно как в следующем примере:

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
    "groupId": "Guid identifying the current O365 Group ID",
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
    "tenantSKU": "The license type for the current user tenant",
    "userLicenseType": "The license type for the current user",
    "parentMessageId": "The parent message ID from which this task module is launched",
    "ringId": "The current ring ID",
    "appSessionId": "The unique ID for the current session used for correlating telemetry data",
    "isCallingAllowed": "Indicates if calling is allowed for the current logged in user",
    "isPSTNCallingAllowed": "Indicates if PSTN calling is allowed for the current logged in user",
    "meetingId": "The meeting ID used by tab when running in meeting context",
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel"
}
```

## <a name="retrieving-context-in-private-channels"></a>Получение контекста в закрытых каналах

> [!Note]
> Закрытые каналы в настоящее время находятся в закрытой предварительной версии для разработчиков.

Когда страница содержимого загружается в закрытый канал, данные, полученные от вызова `getContext`, можно замаскировать для защиты конфиденциальности канала. Следующие поля будут изменены, если страница содержимого находится в закрытом канале. Если на странице используется любое из значений, указанных ниже, необходимо проверить поле `channelType`, чтобы определить, загружена ли страница в частном канале, и действовать соответственно.

* `groupId` - Не определено для закрытых каналов
* `teamId` - Присвоить в качестве значения threadId закрытого канала
* `teamName` - Присвоить в качестве значения имя закрытого канала
* `teamSiteUrl` - Присвоить в качестве значения URL-адрес отдельного уникального сайта SharePoint для закрытого канала
* `teamSitePath` - Присвоить в качестве значения путь отдельного уникального сайта SharePoint для закрытого канала
* `teamSiteDomain` - Присвоить в качестве значения домен отдельного уникального сайта SharePoint для закрытого канала

> [!Note]
>  Переменная teamSiteUrl также хорошо работает для стандартных каналов.

## <a name="theme-change-handling"></a>Обработка изменений темы

Вы можете зарегистрировать свое приложение — тогда вы сможете получать уведомления о том, что тема изменится, вызовом `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

Аргумент `theme` функции будет строкой со значением `default`, `dark`или `contrast`.
