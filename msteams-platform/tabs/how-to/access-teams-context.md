---
title: Получение контекста для вкладки
description: В этой статье описывается, как получить контекст пользователя для вкладок
localization_priority: Normal
ms.topic: how-to
keywords: пользовательский контекст вкладок teams
ms.openlocfilehash: 29f574ae924ddde52b63590aba3fcc06a3d446af
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140280"
---
# <a name="get-context-for-your-tab"></a>Получение контекста для вкладки

Для отображения соответствующего контента на вкладке требуются контекстные сведения:

* Основные сведения о пользователе, команде или компании.
* Сведения о locale и теме.
* Прочитайте `entityId` или `subEntityId` определяйте, что находится на этой вкладке.

## <a name="user-context"></a>Контекст пользователя

Контекст о пользователе, команде или компании может быть особенно полезен, когда:

* Вы создаете или связываете ресурсы в приложении с указанным пользователем или командой.
* Вы инициируете поток проверки подлинности из Azure Active Directory (AAD) или другого поставщика удостоверений, и вам не требуется повторно вводить имя пользователя. Дополнительные сведения см. в записи проверки подлинности [пользователя на вкладке Microsoft Teams.](~/concepts/authentication/authentication.md)

> [!IMPORTANT]
> Хотя эта информация пользователя может помочь обеспечить плавный пользовательский опыт, вы не должны использовать его в качестве доказательства удостоверения. Например, злоумышленник может загрузить страницу в браузер и отрисовки вредных сведений или запросов.

## <a name="access-context-information"></a>Доступ к данным контекста

Доступ к контекстной информации можно получить двумя способами:

* Вставьте значения местообнамерщика URL- адресов.
* Используйте [SDK Microsoft Teams JavaScript.](/javascript/api/overview/msteams-client)

### <a name="get-context-by-inserting-url-placeholder-values"></a>Получить контекст, вставив значения задатки URL-адресов

Используйте заполнители в конфигурации или в URL-адресах контента. Microsoft Teams заменяет заполнители соответствующими значениями, когда определяет фактическую конфигурацию или URL-адрес контента. Доступные держатели включают все поля на [объекте контекста.](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) Распространенные сценарии:

* {entityId}: ИД, который вы предоставили для элемента на этой вкладке при [первоначальной настройке](~/tabs/how-to/create-tab-pages/configuration-page.md).
* {subEntityId}: ID, который вы предоставили при создании глубокой ссылки для определенного элемента в этой вкладке. [](~/concepts/build-and-test/deep-links.md) Это необходимо использовать для восстановления определенного состояния в объекте; например, прокрутка или активация определенного фрагмента контента.
* {LoginHint}: значение, подходящее в качестве подсказки входа для AAD. Обычно это имя входа текущего пользователя в домашнем клиенте.
* {userPrincipalName}: основное имя пользователя текущего пользователя в текущем клиенте.
* {userObjectId}: ID объекта AAD текущего пользователя текущего клиента.
* {theme}: текущая тема пользовательского интерфейса (пользовательского интерфейса), например `default` `dark` , или `contrast` .
* {groupId}: ID группы Office 365, в которой находится вкладка.
* {tid}: ID клиента AAD текущего пользователя.
* {locale}: текущий локализ пользователя, форматированный как languageId-countryId. Например, en-ru.

> [!NOTE]
> Предыдущий заполнитель `{upn}` теперь не поддерживается. Для обратной совместимости в настоящее время он является синонимом для `{loginHint}`.

Например, в манифесте вкладки вы за установите атрибут, чтобы пользователь, вписав его, получил `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` следующие атрибуты:

* Их имя пользователя **user@example.com**.
* Их ID клиента компании **e2653c-etc**.
* Они являются членами группы Office 365 id **00209384-etc**.
* Пользователь установил свою Teams **темную** тему.

При настройке вкладки Teams следующий URL-адрес:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Получить контекст с помощью библиотеки Microsoft Teams JavaScript

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

## <a name="retrieve-context-in-private-channels"></a>Извлечение контекста в частных каналах

> [!Note]
> Закрытые каналы в настоящее время находятся в закрытой предварительной версии для разработчиков.

Когда страница контента загружается в частный канал, данные, полученные от вызова, запутываются для защиты `getContext` конфиденциальности канала. Если страница контента находится в частном канале, меняются следующие поля:

* `groupId`: Неопределяемая для частных каналов
* `teamId`: Установите для threadId частного канала
* `teamName`: Установите имя частного канала
* `teamSiteUrl`: Установите URL-адрес отдельного уникального SharePoint для частного канала
* `teamSitePath`: Установите путь отдельного, уникального SharePoint для частного канала
* `teamSiteDomain`: Установите домен отдельного, уникального SharePoint для частного канала

Если на странице используется любое из этих значений, необходимо проверить поле, чтобы определить, загружена ли страница в частном канале, и ответить `channelType` соответствующим образом.

> [!Note]
> `teamSiteUrl` также хорошо работает для стандартных каналов.

## <a name="handle-theme-change"></a>Обработка изменения темы

Вы можете зарегистрировать приложение, чтобы быть информированным, если тема изменяется по вызову `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` .

Аргументом `theme` в функции является строка со значением `default` , или `dark` `contrast` .

## <a name="see-also"></a>См. также

* [Рекомендации по разработке вкладок](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Teams вкладки](~/tabs/what-are-tabs.md)
* [Необходимые условия](~/tabs/how-to/tab-requirements.md)
* [Создать личную вкладку](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Создать страницу контента](~/tabs/how-to/create-tab-pages/content-page.md)
* [Создать страницу конфигурации](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [Создание страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Предварительный просмотр для ссылки "Вкладки" и представление стадий](~/tabs/tabs-link-unfurling.md)
* [Создание вкладок бесед](~/tabs/how-to/conversational-tabs.md)
* [Изменения полей вкладок](~/resources/removing-tab-margins.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)