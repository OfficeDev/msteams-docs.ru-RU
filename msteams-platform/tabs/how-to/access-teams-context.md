---
title: Получение контекста для вкладки
description: В этой статье описывается, как получить контекст пользователя для вкладок
localization_priority: Normal
ms.topic: how-to
keywords: пользовательский контекст вкладок teams
ms.openlocfilehash: 0d9224a941ae4f6a5ad125c93d5877ec49b6df28
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566868"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a>Получение контекста для вкладки Microsoft Teams

Для отображения соответствующего содержимого вкладке должна потребоваться контекстная информация:

* Основная информация о пользователе, команде или компании.
* Локале и тематическая информация.
* Прочитайте `entityId` или `subEntityId` что определяет, что находится в этой вкладке.

## <a name="user-context"></a>Контекст пользователя

Контекст о пользователе, команде или компании может быть особенно полезен, когда:

* Вы создаете или связываете ресурсы в приложении с указанным пользователем или командой.
* Вы инициируете поток аутентификации Azure Active Directory или другого поставщика идентификационных данных, и вы не хотите требовать от пользователя снова ввести свое имя пользователя. Для получения дополнительной информации о проверке подлинности Microsoft Teams [Microsoft Teams](~/concepts/authentication/authentication.md)вкладке, см.

> [!IMPORTANT]
> Хотя эти сведения о пользователях помогают обеспечить плавное взаимодействие с пользователем, *не надо* использовать их в качестве подтверждения личности. Например, злоумышленник может загрузить страницу в "плохом браузере" и показать опасные сведения или ввести злонамеренные запросы.

## <a name="accessing-context"></a>Доступ к контексту

Доступ к контекстной информации можно получить двумя способами:

* Вставьте значения заполнителя URL.
* Используйте [Microsoft Teams JavaScript SDK](/javascript/api/overview/msteams-client).

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
* «Locale»: Текущая локать пользователя, отформатированная как languageId-countryId. Например, ан-нас.

>[!NOTE]
>Предыдущий заполнитель `{upn}` теперь не поддерживается. Для обратной совместимости в настоящее время он является синонимом для `{loginHint}`.

Например, предположим, что в манифесте вкладки `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` вы установите атрибут, у вписавного пользователя следующие атрибуты:

* Их имя пользователя "user@example.com".
* Их компания арендатора ID является "e2653c-и т.д".
* Они являются членом группы Office 365 id '00209384-т.д.
* Пользователь установил свою тему Teams "темный".

Когда они настраивают вкладку, Teams вызывает следующий URL:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a>Получение контекста с помощью библиотеки JavaScript для Microsoft Teams

Вы также можете получить сведения, перечисленные выше, с помощью [клиентского SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client), вызвав `microsoftTeams.getContext(function(context) { /* ... */ })`.

Переменная контекста выглядит следующим примером:

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
    "tenantSKU": "The license type for the current user tenant. Possible values are enterprise, free, edu, unknown",
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

* `groupId`: Неопределенный для частных каналов
* `teamId`: Установить на потокId частного канала
* `teamName`: Установить на имя частного канала
* `teamSiteUrl`: Установить на URL различных, уникальный SharePoint сайт для частного канала
* `teamSitePath`: Установить на пути различных, уникальный SharePoint сайт для частного канала
* `teamSiteDomain`: Установить в домене различных, уникальных SharePoint домена сайта для частного канала

> [!Note]
>  Переменная teamSiteUrl также хорошо работает для стандартных каналов.

## <a name="theme-change-handling"></a>Обработка изменений темы

Вы можете зарегистрировать свое приложение — тогда вы сможете получать уведомления о том, что тема изменится, вызовом `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

Аргумент `theme` функции будет строкой со значением `default`, `dark`или `contrast`.
