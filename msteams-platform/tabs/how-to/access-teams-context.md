---
title: Получение контекста для вкладки
description: В этом модуле вы узнаете, как получить контекст пользователя для вкладок, контекста пользователя и сведений о контексте Access.
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 63bbc9c0e5f20e293f9230000597860e3f053274
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841724"
---
# <a name="get-context-for-your-tab"></a>Получение контекста для вкладки

Для отображения соответствующего содержимого на вкладке требуются контекстные сведения:

* Основные сведения о пользователе, команде или компании.
* Сведения о языковом стандарте и теме.
* И `page.id` которые `page.subPageId` определяют, что находится на этой вкладке ( `entityId` `subEntityId` известной как и до TeamsJS версии 2.0.0).

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="user-context"></a>Контекст пользователя

Контекст о пользователе, команде или компании может быть особенно полезен в следующих случаях:

* Вы создаете или связываете ресурсы в приложении с указанным пользователем или командой.
* Вы инициируете поток проверки подлинности из Microsoft Azure Active Directory (Azure AD) или другого поставщика удостоверений, и вам не нужно повторно вводить имя пользователя.

Дополнительные сведения см. в [статье о проверке подлинности пользователя в Microsoft Teams](~/concepts/authentication/authentication.md).

> [!IMPORTANT]
> Хотя эти сведения о пользователе помогают обеспечить бесперебойное взаимодействие с пользователем, их не следует использовать в качестве подтверждения личности.  Например, злоумышленник может загрузить страницу в браузере и отобразить вредоносные сведения или запросы.

## <a name="access-context-information"></a>Доступ к контекстным сведениям

Доступ к контекстной информации можно получить двумя способами:

* Использование [значений заполнителей URL-адресов](#get-context-by-inserting-url-placeholder-values).
* Из объекта контекста клиентского пакета SDK [](/javascript/api/@microsoft/teams-js/app.context) javaScript для Microsoft Teams.

### <a name="get-context-by-inserting-url-placeholder-values"></a>Получение контекста путем вставки значений заполнителей URL-адресов

Используйте заполнители в конфигурации или в URL-адресах контента. Microsoft Teams заменяет заполнители соответствующими значениями, когда определяет фактическую конфигурацию или URL-адрес контента. Доступные заполнители включают все поля в [объекте контекста](/javascript/api/@microsoft/teams-js/app.context) . Распространенные заполнители включают следующие списки:

* [{page.id}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-id): уникальный идентификатор страницы, определяемый разработчиком при [первой настройке страницы](~/tabs/how-to/create-tab-pages/configuration-page.md). (Известен как до `{entityId}` TeamsJS версии 2.0.0).
* [{page.subPageId}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-subpageid): уникальный идентификатор, определенный разработчиком для вложенной страницы, которая определяется этим содержимым при создании [](~/concepts/build-and-test/deep-links.md) глубокой ссылки для определенного элемента на странице. (Известен как до `{subEntityId}` TeamsJS версии 2.0.0).
* [{user.loginHint}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-loginhint): значение, подходящее в качестве указания входа для Azure AD. Обычно это имя входа текущего пользователя в домашнем клиенте. (Известен как до `{loginHint}` TeamsJS версии 2.0.0).
* [{user.userPrincipalName}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-userprincipalname): имя участника-пользователя текущего пользователя в текущем клиенте. (Известен как до `{userPrincipalName}` TeamsJS версии 2.0.0).
* [{user.id}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-id): Azure AD объекта текущего пользователя в текущем клиенте. (Известен как до `{userObjectId}` TeamsJS версии 2.0.0).
* [{app.theme}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-theme): текущая тема пользовательского интерфейса, например `default`, или `dark``contrast`. (Известен как до `{theme}` TeamsJS версии 2.0.0).
* [{team.groupId}](/javascript/api/@microsoft/teams-js/app.teaminfo#@microsoft-teams-js-app-teaminfo-groupid): идентификатор Office 365 группы, в которой находится вкладка. (Известен как до `{groupId}` TeamsJS версии 2.0.0)
* [{user.tenant.id}](/javascript/api/@microsoft/teams-js/app.tenantinfo#@microsoft-teams-js-app-tenantinfo-id): Azure AD клиента текущего пользователя. (Известен как до `{tid}` TeamsJS версии 2.0.0).
* [{app.locale}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-locale): текущий языковой стандарт пользователя, отформатированный как *languageId-countryId*, например `en-us`. (Известен как до `{locale}` TeamsJS версии 2.0.0).

> [!NOTE]
> Предыдущий заполнитель `{upn}` теперь не поддерживается. Для обратной совместимости в настоящее время он является синонимом для `{user.loginHint}`.

Например, в манифесте приложения, если для атрибута *tab configurationUrl* `"https://www.contoso.com/config?name={user.loginHint}&tenant={user.tenant.id}&group={team.groupId}&theme={app.theme}"` задано значение и пользователь, выполнив вход, имеет следующие атрибуты:

* Имя **пользователя — user@example.com**.
* Идентификатор клиента компании — **e2653c-etc**.
* Они являются членами Office 365 с идентификатором **00209384 и т. д**.
* Пользователь настроит темную тему **Teams.**

. . . Затем Teams будет вызывать следующий URL-адрес при настройке вкладки:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Получение контекста с помощью библиотеки JavaScript для Microsoft Teams

Вы также можете получить сведения, перечисленные выше, с помощью [клиентского SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client), вызвав `microsoftTeams.getContext(function(context) { /* ... */ })`.

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
| app.locale | языковые стандарты | Текущий языковой стандарт, настроенный пользователем для приложения, отформатированного как languageId-countryId (например, en-us). |
| page.id | entityId | Уникальный идентификатор страницы, на который указывает данное содержимое, определяемый разработчиком. |
| page.subPageId | subEntityId | Уникальный идентификатор, определенный разработчиком для вложенной страницы, на который указывает данное содержимое. Это поле следует использовать для восстановления до определенного состояния на странице, например для прокрутки или активации определенного фрагмента содержимого. |
| user.loginHint | loginHint | Значение, подходящее для использования в качестве login_hint при проверке подлинности с Azure AD. Так как вредоносная сторона может запускать содержимое в браузере, это значение следует использовать только в качестве указания о том, кто является пользователем и никогда не является подтверждением личности. Это поле доступно только в том случае, если в манифесте запрашивается разрешение удостоверения. |
| user.userPrincipalName | Upn | Имя участника-пользователя текущего пользователя. Это может быть имя участника-пользователя, прошедшее внешнюю проверку подлинности (например, гостевые пользователи). Так как вредоносная сторона запускает содержимое в браузере, это значение следует использовать только в качестве указания о том, кто является пользователем и никогда не является подтверждением личности. Это поле доступно только в том случае, если в манифесте запрашивается разрешение удостоверения. |
| user.id | userObjectId | Идентификатор Azure AD объекта текущего пользователя. Так как вредоносная сторона запускает содержимое в браузере, это значение следует использовать только в качестве указания о том, кто является пользователем и никогда не является подтверждением личности. Это поле доступно только в том случае, если в манифесте запрашивается разрешение удостоверения. |
| user.tenant.id | Tid | Идентификатор Azure AD клиента текущего пользователя. Так как вредоносная сторона может запускать содержимое в браузере, это значение следует использовать только в качестве указания о том, кто является пользователем и никогда не является подтверждением личности. Это поле доступно только в том случае, если в манифесте запрашивается разрешение удостоверения. |
| team.groupId | groupId | Идентификатор Office 365 группы, с которой связано содержимое. Это поле доступно только в том случае, если в манифесте запрашивается разрешение удостоверения. |
| app.theme  | theme | Текущая тема пользовательского интерфейса: по умолчанию, темная, контрастность |
| page.isFullScreen | isFullScreen | Указывает, находится ли страница в полноэкранном режиме. |
| team.type | teamType | Тип команды. |
| sharepointSite.teamSiteUrl | teamSiteUrl | Корневой сайт SharePoint, связанный с командой. |
| sharepointSite.teamSiteDomain | teamSiteDomain | Домен корневого сайта SharePoint, связанного с командой. |
| sharepointSite.teamSitePath | teamSitePath | Относительный путь к сайту SharePoint, связанному с командой. |
| channel.relativeUrl | channelRelativeUrl | Относительный путь к папке SharePoint, связанной с каналом. |
| App.host.sessionId | Sessionid | Уникальный идентификатор текущего сеанса узла для использования при сопоставлении данных телеметрии. |
| team.userRole | userTeamRole | Роль пользователя в команде. Так как вредоносная сторона может запускать содержимое в браузере, это значение следует использовать только в качестве указания роли пользователя и никогда не в качестве подтверждения ее роли. |
| team.isArchived | isTeamArchived | Указывает, архивирована ли команда. Приложения должны использовать его в качестве сигнала, чтобы предотвратить любые изменения содержимого, связанного с архивными командами. |
| app.host.clientType | hostClientType | Тип главного клиента. Возможные значения: android, ios, web, desktop, rigel |
| page.frameContext | frameContext | Контекст, в который загружается URL-адрес страницы (содержимое, задача, настройка, удаление, sidePanel) |
| sharepoint | sharepoint | Контекст SharePoint. Это доступно только при размещении в SharePoint. |
| user.tenant.teamsSku | tenantSKU | Тип лицензии для текущего клиента пользователя. Возможные значения: enterprise, free, edu, unknown |
| user.licenseType | userLicenseType | Тип лицензии для текущего пользователя. Возможные значения: корпоративные планы E1, E3 и E5 |
| app.parentMessageId | parentMessageId | Идентификатор родительского сообщения, из которого был запущен этот модуль задачи. Это доступно только в модулях задач, запущенных с карточек ботов. |
| App.host.ringId | ringId | Идентификатор текущего кольца. |
| App.sessionId | appSessionId | Уникальный идентификатор текущего сеанса узла для использования при сопоставлении данных телеметрии. |
| user.isCallingAllowed | isCallingAllowed | Указывает, разрешен ли вызов для текущего пользователя, выполнив вход. |
| user.isPSTNCallingAllowed | isPSTNCallingAllowed | Указывает, разрешены ли вызовы ТСОП для текущего пользователя |
| meeting.id | meetingId | Идентификатор собрания, используемый вкладкой при выполнении в контексте собрания. |
| channel.defaultOneNoteSectionId | defaultOneNoteSectionId | Идентификатор раздела OneNote, связанный с каналом. |
| page.isMultiWindow | isMultiWindow | Указывает, находится ли вкладка во всплывающем окне. |

Дополнительные сведения см [. Обновления *контекстного*](using-teams-client-sdk.md#updates-to-the-context-interface) интерфейса и справочника по API [интерфейса](/javascript/api/@microsoft/teams-js/app.context) контекста.

## <a name="retrieve-context-in-private-channels"></a>Получение контекста в частных каналах

Когда страница содержимого загружается в закрытый канал, данные, получаемые при вызове, `getContext` замаскируются для защиты конфиденциальности канала.

Следующие поля изменяются, если страница содержимого находится в частном канале:

* `team.groupId`: не определено для частных каналов
* `team.internalId`: задайте значение threadId закрытого канала.
* `team.displayName`: задайте имя частного канала.
* `sharepointSite.url`: задайте URL-адрес отдельного уникального сайта SharePoint для частного канала.
* `sharepointSite.path`: задайте путь к отдельному уникальному сайту SharePoint для частного канала.
* `sharepointSite.domain`: задайте домен уникального домена сайта SharePoint для частного канала.

Если на странице используется любое из этих значений, `channel.membershipType` `Private` значение поля должно быть таким, чтобы определить, загружена ли страница в частный канал и может ли она отвечать соответствующим образом.

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>Получение контекста в Microsoft Teams Связи общих каналах

> [!NOTE]
> В настоящее Microsoft Teams Связи общие каналы доступны только в [предварительной версии разработчика](../../resources/dev-preview/developer-preview-intro.md).

Когда страница содержимого загружается в общий Microsoft Teams Связи канале, данные, получаемые при вызове, `getContext` изменяются из-за уникального списка пользователей в общих каналах.

Следующие поля изменяются, если страница содержимого находится в общем канале:

* `team.groupId`: не определено для общих каналов.
* `team.internalId`: задайте для `threadId` команды общий доступ к каналу для текущего пользователя. Если у пользователя есть доступ к нескольким командам, это задается для команды, которая размещает (создает) общий канал.
* `team.displayName`: задайте имя команды, канал является общим для текущего пользователя. Если у пользователя есть доступ к нескольким командам, это задается для команды, которая размещает (создает) общий канал.
* `sharepointSite.url`: задайте URL-адрес отдельного уникального сайта SharePoint для общего канала.
* `sharepointSite.path`: задайте путь к отдельному уникальному сайту SharePoint для общего канала.
* `sharepointSite.domain`: задайте домен отдельного уникального домена сайта SharePoint для общего канала.

Помимо этих изменений полей, для общих каналов доступны два новых поля:

* `hostTeamGroupId`: задайте связанное `team.groupId` с группой размещения или командой, создающей общий канал. Это свойство может API Graph вызовы Майкрософт для получения членства в общем канале.
* `hostTeamTenantId`: задайте связанное `channel.ownerTenantId` с группой размещения или командой, создающей общий канал. На свойство `user.tenant.id` можно перекрестно ссылаться с идентификатором клиента текущего пользователя, найденным в поле объекта *контекста* , чтобы определить, является ли пользователь внутренним или внешним для клиента группы размещения.

Если на странице используется любое из этих значений, `channel.membershipType` `Shared` значение поля должно быть таким, чтобы определить, загружена ли страница в общем канале и может ли она отвечать соответствующим образом.

> [!NOTE]
> Каждый раз, когда пользователь перезапускает или перезагружает рабочий или веб-клиент Teams, создается новый sessionID, который отслеживается сеансом Teams, в то время как когда пользователь выходит из приложений Teams и перезагружает его на платформе Teams, создается новый sessionID приложения, который отслеживается сеансом приложения.

## <a name="handle-theme-change"></a>Обработка изменения темы

Вы можете зарегистрировать приложение для получения сведений об изменении темы путем вызова `microsoftTeams.app.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

Аргументом `theme` в функции является строка со значением `default`, `dark`или `contrast`.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>См. также

* [Рекомендации по проектированию вкладок](../../tabs/design/tabs.md)
* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Использование модулей задач во вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
