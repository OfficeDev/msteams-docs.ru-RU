---
title: Получение контекста для вкладки
description: Сведения о получении контекста пользователя для вкладок
keywords: контекст пользователя вкладок Teams
ms.openlocfilehash: 5c52e6eea21f0c059f3cd650770e1076f903fb8e
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552439"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a>Получение контекста для вкладки Microsoft Teams

Для отображения соответствующего контента на вкладке может потребоваться Контекстная информация.

* Для вкладки могут потребоваться основные сведения о пользователе, команде или компании.
* Для вкладки может потребоваться информация о языковых стандартах и теме.
* На вкладке может потребоваться прочитать `entityId` или `subEntityId` определить, что находится на этой вкладке.

## <a name="user-context"></a>Контекст пользователя

Контекст пользователя, группы или компании особенно полезен при

* Необходимо создать или связать ресурсы в приложении с указанным пользователем или группой.
* Вы хотите инициировать процесс проверки подлинности для Azure Active Directory или другого поставщика удостоверений и не требовать от пользователя повторного ввода имени пользователя. (Дополнительные сведения о проверке подлинности на вкладке Microsoft Teams можно найти [в разделе Проверка подлинности пользователя на вкладке Microsoft Teams](~/concepts/authentication/authentication.md).)

> [!IMPORTANT]
> Несмотря на то что эти сведения о пользователях помогают обеспечить гладкую работу пользователей, *не* следует использовать его для подтверждения подлинности. Например, злоумышленник может загрузить страницу в виде "плохого браузера" и отобразить нежелательные сведения или запросы.

## <a name="accessing-context"></a>Доступ к контексту

Доступ к сведениям о контексте можно получить двумя способами:

* Вставка значений заполнителей URL-адресов
* Использование [пакета SDK клиента JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client)

### <a name="getting-context-by-inserting-url-placeholder-values"></a>Извлечение контекста путем вставки значений заполнители URL-адресов

Используйте заполнители в URL-адресах конфигурации или контента. Microsoft Teams заменяет заполнители соответствующими значениями при определении фактической конфигурации или URL-адреса контента. Доступные заполнители включают все поля в объекте [context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) . Общие заполнители включают в себя следующее:

* {Ентитид}: идентификатор, указанный для элемента на этой вкладке при первой [настройке вкладки](~/tabs/how-to/create-tab-pages/configuration-page.md).
* {Субентитид}: идентификатор, указанный при создании [детальной ссылки](~/concepts/build-and-test/deep-links.md) для _определенного элемента на_ этой вкладке. Используется для восстановления в определенном состоянии в пределах объекта; Например, прокрутите или активируйте определенный фрагмент содержимого.
* {Логинхинт}: значение, которое подходит как подсказка для входа для Azure AD. Как правило, это имя входа текущего пользователя в его домашнем клиенте.
* {userPrincipalName}: имя участника пользователя текущего пользователя в текущем клиенте.
* {Усеробжектид}: идентификатор объекта Azure AD текущего пользователя в текущем клиенте.
* {Theme}: текущие темы пользовательского интерфейса, такие как `default` , `dark` или `contrast` .
* {groupId}: идентификатор группы Office 365, в которой находится вкладка.
* {TID}: идентификатор клиента Azure AD для текущего пользователя.
* {locale}: текущий языковой стандарт пользователя, отформатированный как languageId-Каунтрид (например, EN-US).

>[!NOTE]
>Предыдущий `{upn}` заполнитель теперь не является устаревшим. Для обратной совместимости он в настоящее время является синонимом `{loginHint}` .

Например, предположим, что в манифесте вкладки атрибуту присвоено значение `configURL`

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

И пользователь, вошедшего в систему, имеет следующие атрибуты:

* Имя пользователя — "user@example.com"
* Идентификатор клиента компании — "e2653c-and-etc"
* Они являются членами группы Office 365 с идентификатором ' 00209384 ' и т. д.
* Тема Teams пользователя задается "темная"

При настройке вкладки Teams вызывает этот URL-адрес:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a>Извлечение контекста с помощью библиотеки JavaScript для Microsoft Teams

Вы также можете получить приведенные выше сведения с помощью [пакета SDK для JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client) , вызвав `microsoftTeams.getContext(function(context) { /* ... */ })` .

Переменная контекста будет выглядеть так, как показано в следующем примере.

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The User Principal Name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current O365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates whether the tab is in full-screen mode",
    "userLicenseType": "Indicates the user licence type in the given SKU (for example, student or teacher)",
    "tenantSKU": "Indicates the SKU category of the tenant (for example, EDU)",
    "channelType": "microsoftTeams.ChannelType.Private | microsoftTeams.ChannelType.Regular"
}
```

## <a name="retrieving-context-in-private-channels"></a>Получение контекста в частных каналах

> [!Note]
> В настоящее время частные каналы находятся в предварительной версии для разработчиков личных версий.

Когда страница контента загружается в частном канале, данные, получаемые из `getContext` вызова, будут замаскированы для защиты конфиденциальности канала. Следующие поля изменяются, когда страница контента находится в частном канале. Если страница использует любое из указанных ниже значений, необходимо проверить `channelType` поле, чтобы определить, загружена ли страница в частном канале, и ответить соответствующим образом.

* `groupId` — Не определено для частных каналов
* `teamId` — Задает threadId для частного канала
* `teamName` — Укажите имя закрытого канала.
* `teamSiteUrl` -Задать URL-адрес уникального уникального сайта SharePoint для частного канала
* `teamSitePath` -Задать путь к отдельному, уникальному сайту SharePoint для частного канала
* `teamSiteDomain` — Укажите домен для частного канала в отдельном домене сайта SharePoint.

> [!Note]
>  Теамситеурл также хорошо работает для стандартных каналов.

## <a name="theme-change-handling"></a>Обработка изменений темы

Вы можете зарегистрировать свое приложение, чтобы сообщить, изменяется ли тема с помощью вызова `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` .

`theme`Аргумент в функции будет строкой со значением `default` , `dark` или `contrast` .
