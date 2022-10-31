---
title: Получение контекста для вкладки
description: Узнайте, как использовать контекст для вкладки, контекст пользователя, команды или компании, получить доступ к информации, получить контекст в частных или общих каналах и обработать изменение темы.
ms.localizationpriority: high
ms.topic: how-to
ms.openlocfilehash: f0a54dc749d1132918e3ec47ac614aff3ce8aab8
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791547"
---
# <a name="get-context-for-your-tab"></a>Получение контекста для вкладки

Для отображения соответствующего содержимого на вкладке требуются контекстные сведения:

* Основные сведения о пользователе, команде или компании.
* Сведения о языковом стандарте и теме.
* `page.subPageId` И `page.id` , которые определяют, что находится на этой вкладке (известный как `entityId` и `subEntityId` до TeamsJS версии 2.0.0).

## <a name="user-context"></a>Контекст пользователя

Контекст пользователя, команды или компании может быть особенно полезен в следующих случаях:

* Вы создаете или связываете ресурсы в приложении с указанным пользователем или командой.
* Вы инициируете поток проверки подлинности из Microsoft Azure Active Directory (Azure AD) или другого поставщика удостоверений, и пользователь не требует повторно вводить свое имя пользователя.

Дополнительные сведения см. [в статье Проверка подлинности пользователя в Microsoft Teams](~/concepts/authentication/authentication.md).

> [!IMPORTANT]
> Хотя эти сведения о пользователе могут помочь обеспечить бесперебойный пользовательский интерфейс, их не следует использовать в качестве подтверждения личности.  Например, злоумышленник может загрузить страницу в браузере и отобразить вредоносные сведения или запросы.

## <a name="access-context-information"></a>Доступ к сведениям о контексте

Доступ к контекстной информации можно получить двумя способами:

* Использование [значений заполнителей URL-адреса](#get-context-by-inserting-url-placeholder-values).
* Из объекта [контекста](/javascript/api/@microsoft/teams-js/app.context) клиентского пакета SDK Для JavaScript для Microsoft Teams.

### <a name="get-context-by-inserting-url-placeholder-values"></a>Получение контекста путем вставки значений заполнителей URL-адреса

Используйте заполнители в конфигурации или в URL-адресах контента. Microsoft Teams заменяет заполнители соответствующими значениями, когда определяет фактическую конфигурацию или URL-адрес контента. Доступные заполнители включают все поля в объекте [контекста](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) . К общим заполнителям относятся следующие свойства:

* [{page.id}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-id): определяемый разработчиком уникальный идентификатор страницы, [определенной при первой настройке страницы](~/tabs/how-to/create-tab-pages/configuration-page.md). (Известный как `{entityId}` до TeamsJS версии 2.0.0).
* [{page.subPageId}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-subpageid): определяемый разработчиком уникальный идентификатор для подстраничной страницы, определенной этим содержимым при создании [глубокой ссылки](~/concepts/build-and-test/deep-links.md) на определенный элемент на странице. (Известный как `{subEntityId}` до TeamsJS версии 2.0.0).
* [{user.loginHint}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-loginhint): значение, подходящее в качестве подсказки для входа для Azure AD. Обычно это имя для входа текущего пользователя в домашнем клиенте. (Известный как `{loginHint}` до TeamsJS версии 2.0.0).
* [{user.userPrincipalName}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-userprincipalname): имя участника-пользователя текущего пользователя в текущем клиенте. (Известный как `{userPrincipalName}` до TeamsJS версии 2.0.0).
* [{user.id}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-id): идентификатор объекта Azure AD текущего пользователя в текущем клиенте. (Известный как `{userObjectId}` до TeamsJS версии 2.0.0).
* [{app.theme}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-theme): тема текущего пользовательского интерфейса, например `default`, `dark`или `contrast`. (Известный как `{theme}` до TeamsJS версии 2.0.0).
* [{team.groupId}](/javascript/api/@microsoft/teams-js/app.teaminfo#@microsoft-teams-js-app-teaminfo-groupid): идентификатор Office 365 группы, в которой находится вкладка. (Известный как `{groupId}` до TeamsJS версии 2.0.0)
* [{user.tenant.id}](/javascript/api/@microsoft/teams-js/app.tenantinfo#@microsoft-teams-js-app-tenantinfo-id): Azure AD идентификатор клиента текущего пользователя. (Известный как `{tid}` до TeamsJS версии 2.0.0).
* [{app.locale}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-locale): текущий языковой стандарт пользователя, отформатированный как *languageId-countryId*, например `en-us`. (Известный как `{locale}` до TeamsJS версии 2.0.0).

> [!NOTE]
> Предыдущий заполнитель `{upn}` теперь не поддерживается. Для обратной совместимости в настоящее время он является синонимом для `{user.loginHint}`.

Например, в манифесте приложения, если для атрибута tab *configurationUrl* задано значение `"https://www.contoso.com/config?name={user.loginHint}&tenant={user.tenant.id}&group={team.groupId}&theme={app.theme}"` , а у вошедшего пользователя есть следующие атрибуты:

* Имя пользователя **— user@example.com**.
* Идентификатор клиента компании **— e2653c-etc**.
* Они вошли в группу Office 365 с идентификатором **00209384 и т. д**.
* Пользователь задал **темную тему** Teams.

. . . При настройке вкладки Teams вызовет следующий URL-адрес:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Получение контекста с помощью библиотеки JavaScript в Microsoft Teams

Вы также можете получить сведения, перечисленные выше, с помощью [клиентского SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client), вызвав `microsoftTeams.getContext(function(context) { /* ... */ })`.

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

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

## <a name="typescript"></a>TypeScript

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

Эквивалентный `async/await` шаблон:

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

## <a name="javascript"></a>JavaScript

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context) => {
    /*...*/
});
```

Эквивалентный `async/await` шаблон:

```js
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context = await app.getContext();
  /*...*/
}
```

# <a name="teamsjs-v1"></a>[TeamsJS версии 1](#tab/teamsjs-v1)

## <a name="typescript"></a>TypeScript

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context: microsoftTeams.Context) => {
  /* ... */
});
```

## <a name="javascript"></a>JavaScript

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => {
  /* ... */ 
});
```

---

В следующей таблице перечислены часто используемые свойства контекста объекта *контекста* :

| Имя TeamsJS версии 2 | Имя TeamsJS версии 1 | Описание |
|-----------------|-----------------|-------------|
| team.internalId | teamId | Идентификатор Microsoft Teams для команды, с которой связано содержимое. |
| team.displayName | teamName | Имя команды, с которой связано содержимое. |
| channel.id | channelId | Идентификатор Microsoft Teams для канала, с которым связано содержимое. |
| channel.displayName | channelName | Имя канала, с которым связано содержимое. |
| chat.id | chatId | Идентификатор Microsoft Teams для чата, с которым связано содержимое. |
| app.locale | языковые стандарты | Текущий языковой стандарт, настроенный пользователем для приложения в формате languageId-countryId (например, en-us). |
| page.id | entityId | Определенный разработчиком уникальный идентификатор страницы, на который указывает это содержимое. |
| page.subPageId | subEntityId | Определенный разработчиком уникальный идентификатор вложенной страницы, на который указывает это содержимое. Это поле должно использоваться для восстановления до определенного состояния на странице, например для прокрутки или активации определенного фрагмента содержимого. |
| user.loginHint | loginHint | Значение, подходящее для использования в качестве login_hint при проверке подлинности с помощью Azure AD. Так как злоумышленник может запустить содержимое в браузере, это значение следует использовать только в качестве подсказки о том, кто является пользователем, и никогда не в качестве подтверждения личности. Это поле доступно только при запросе разрешения удостоверения в манифесте. |
| user.userPrincipalName | Upn | Имя участника-пользователя текущего пользователя. Это может быть имя участника-пользователя, прошедшее внешнюю проверку подлинности (например, гостевые пользователи). Так как злоумышленник запускает содержимое в браузере, это значение следует использовать только в качестве подсказки о том, кто является пользователем, и никогда не в качестве подтверждения личности. Это поле доступно только при запросе разрешения удостоверения в манифесте. |
| user.id | userObjectId | Идентификатор объекта Azure AD текущего пользователя. Так как злоумышленник запускает содержимое в браузере, это значение следует использовать только в качестве подсказки о том, кто является пользователем, и никогда не в качестве подтверждения личности. Это поле доступно только при запросе разрешения удостоверения в манифесте. |
| user.tenant.id | Tid | Идентификатор клиента Azure AD текущего пользователя. Так как злоумышленник может запустить содержимое в браузере, это значение следует использовать только в качестве подсказки о том, кто является пользователем, и никогда не в качестве подтверждения личности. Это поле доступно только при запросе разрешения удостоверения в манифесте. |
| team.groupId | groupId | Идентификатор группы Office 365 для команды, с которой связано содержимое. Это поле доступно только при запросе разрешения удостоверения в манифесте. |
| app.theme  | theme | Текущая тема пользовательского интерфейса: по умолчанию, темная, контрастность |
| page.isFullScreen | isFullScreen | Указывает, находится ли страница в полноэкранном режиме. |
| team.type | teamType | Тип команды. |
| sharepointSite.teamSiteUrl | teamSiteUrl | Корневой сайт SharePoint, связанный с командой. |
| sharepointSite.teamSiteDomain | teamSiteDomain | Домен корневого сайта SharePoint, связанного с командой. |
| sharepointSite.teamSitePath | teamSitePath | Относительный путь к сайту SharePoint, связанному с командой. |
| channel.relativeUrl | channelRelativeUrl | Относительный путь к папке SharePoint, связанной с каналом. |
| app.host.sessionId | Sessionid | Уникальный идентификатор текущего сеанса узла для использования при корреляции данных телеметрии. |
| team.userRole | userTeamRole | Роль пользователя в команде. Так как злоумышленник может запустить содержимое в браузере, это значение следует использовать только в качестве указания на роль пользователя и никогда не в качестве доказательства его роли. |
| team.isArchived | isTeamArchived | Указывает, архивирована ли команда. Приложения должны использовать его в качестве сигнала, чтобы предотвратить любые изменения в содержимом, связанном с архивными командами. |
| app.host.clientType | hostClientType | Тип клиента узла. Возможные значения: android, ios, web, desktop, rigel |
| page.frameContext | frameContext | Контекст, в который загружается URL-адрес страницы (содержимое, задача, настройка, удаление, sidePanel) |
| sharepoint | sharepoint | Контекст SharePoint. Эта возможность доступна только при размещении в SharePoint. |
| user.tenant.teamsSku | tenantSKU | Тип лицензии для текущего клиента пользователя. Возможные значения: enterprise, free, edu, unknown |
| user.licenseType | userLicenseType | Тип лицензии для текущего пользователя. Возможные значения: корпоративные планы E1, E3 и E5. |
| app.parentMessageId | parentMessageId | Идентификатор родительского сообщения, из которого был запущен этот модуль задач. Это доступно только в модулях задач, запускаемых с карточек бота. |
| app.host.ringId | ringId | Идентификатор текущего круга. |
| app.sessionId | appSessionId | Уникальный идентификатор текущего сеанса узла для использования при корреляции данных телеметрии. |
| user.isCallingAllowed | isCallingAllowed | Указывает, разрешен ли вызов для текущего вошедшего в систему пользователя. |
| user.isPSTNCallingAllowed | isPSTNCallingAllowed | Указывает, разрешены ли вызовы ТСОП для текущего пользователя. |
| meeting.id | meetingId | Идентификатор собрания, используемый вкладкой при запуске в контексте собрания. |
| channel.defaultOneNoteSectionId | defaultOneNoteSectionId | Идентификатор раздела OneNote, связанный с каналом. |
| page.isMultiWindow | isMultiWindow | Указывает, находится ли вкладка в всплывающем окне. |

Дополнительные сведения см. в [разделе Обновления интерфейса *контекста*](using-teams-client-sdk.md#updates-to-the-context-interface) и справочник по API [интерфейса контекста](/javascript/api/@microsoft/teams-js/app.context).

## <a name="retrieve-context-in-private-channels"></a>Получение контекста в частных каналах

> [!NOTE]
> В настоящее время частные каналы доступны только в предварительной версии для частных разработчиков.

Когда страница содержимого загружается в частный канал, данные, полученные от `getContext` звонка, маскируются для защиты конфиденциальности канала.

Следующие поля изменяются, когда страница содержимого находится в частном канале:

* `team.groupId`: не определено для частных каналов.
* `team.internalId`: задайте значение threadId частного канала.
* `team.displayName`: задайте имя частного канала.
* `sharepointSite.url`: задайте URL-адрес уникального сайта SharePoint для частного канала.
* `sharepointSite.path`: задайте путь к отдельному уникальному сайту SharePoint для частного канала.
* `sharepointSite.domain`: задайте домен отдельного, уникального домена сайта SharePoint для частного канала.

Если страница использует любое из этих значений, значение `channel.membershipType` поля должно быть `Private` таким, чтобы определить, загружена ли ваша страница в частном канале и может ли она реагировать соответствующим образом.

> [!NOTE]
>`teamSiteUrl` также хорошо подходит для стандартных каналов. Если страница использует любое из этих значений, значение `channelType` поля должно быть `Shared` таким, чтобы определить, загружена ли ваша страница в общем канале и может ли она реагировать соответствующим образом.

## <a name="get-context-in-shared-channels"></a>Получение контекста в общих каналах

При загрузке пользовательского интерфейса содержимого в общий канал используйте данные, полученные из `getContext` вызова, для изменения общего канала. Если вкладка использует любое из следующих значений, необходимо заполнить `channelType` поле, чтобы определить, загружена ли вкладка в общем канале, и ответить соответствующим образом.
Для общих каналов `groupId` значение равно `null`, так как идентификатор groupId принимающей команды не точно отражает истинное членство в общем канале. Чтобы устранить эту проблему, `hostTeamGroupID` свойства и `hostTenantID` добавлены и полезны для выполнения вызовов Microsoft API Graph для получения членства. `hostTeam` ссылается на команду, создающую общий канал. `currentTeam` ссылается на команду, из которой текущий пользователь обращается к общему каналу.

Дополнительные сведения об этих понятиях см. в разделе [Общие каналы](~/concepts/build-and-test/shared-channels.md).

Используйте следующие `getContext` свойства в общих каналах:

| Свойство | Описание |
|----------|--------------|
|`channelId`| Для свойства задается идентификатор потока общих каналов.|
|`channelType`| Свойство имеет значение `sharedChannel` для общих каналов.|
|`groupId`|Свойство предназначено `null` для общих каналов.|
|`hostTenantId`| Свойство добавлено и описывает идентификатор клиента узла, полезное для сравнения со свойством идентификатора `tid` клиента текущего пользователя. |
|`hostTeamGroupId`| Свойство добавлено только что и описывает идентификатор группы Azure AD хост-команды, который полезен для выполнения вызовов Microsoft API Graph для получения членства в общем канале. |
|`teamId`|Свойство добавляется и задает идентификатор потока текущей общей команды. |
|`teamName`|Для свойства задано значение текущей общей команды `teamName`. |
|`teamType`|Для свойства задано значение текущей общей команды `teamType`.|
|`teamSiteUrl`|Свойство описывает общий канал `channelSiteUrl`.|
|`teamSitePath`| Свойство описывает общий канал `channelSitePath`.|
|`teamSiteDomain`| Свойство описывает общий канал `channelSiteDomain`.|
|`tenantSKU`| Свойство описывает `tenantSKU`.|
|`tid`|  Свойство описывает идентификатор клиента текущего пользователя.|
|`userObjectId`|  Свойство описывает идентификатор текущего пользователя.|
|`userPrincipalName`| Свойство описывает имя участника-пользователя текущего пользователя.|

Дополнительные сведения о общих каналах см. в разделе [Общие каналы](~/concepts/build-and-test/shared-channels.md).

## <a name="handle-theme-change"></a>Обработка изменения темы

Вы можете зарегистрировать приложение, чтобы получить информацию о том, изменится ли тема, вызвав .`microsoftTeams.app.registerOnThemeChangeHandler(function(theme) { /* ... */ })`

Аргумент `theme` в функции представляет собой строку со значением `default`, `dark`или `contrast`.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>См. также

* [Рекомендации по проектированию вкладок](../../tabs/design/tabs.md)
* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Использование модулей задач во вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
