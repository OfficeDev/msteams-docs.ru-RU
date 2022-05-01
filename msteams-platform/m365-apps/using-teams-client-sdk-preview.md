---
title: Предварительная версия SDK клиента Microsoft Teams JavaScript v2
description: Узнайте об изменениях, которые появятся в предварительной версии SDK клиента Microsoft Teams JavaScript v2
ms.date: 11/15/2021
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 91f012821efacd0f0ff6032703d0520d5bd469e0
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111698"
---
# <a name="microsoft-teams-javascript-client-sdk-v2-preview"></a>Предварительная версия SDK клиента Microsoft Teams JavaScript v2

В [предварительной версии SDK клиента Microsoft Teams JavaScript v2](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true) существующий SDK Teams (`@microsoft/teams-js` или просто`TeamsJS`) был переорганизован, чтобы дать разработчикам Teams возможность [расширять приложения Teams для запуска в Outlook и Office](overview.md). С функциональной точки зрения предварительная версия TeamsJS SDK v2 (`@microsoft/teams-js@next`) является расширенным набором текущего TeamsJS SDK, она поддерживает существующие функции приложений Teams, добавляя возможность размещать приложения Teams в Outlook и Office.

В TeamsJS SDK v2 предварительной версии есть два существенных изменения, которые код должен учитывать для работы в других приложениях Microsoft 365:

* [**Функции обратного вызова теперь возвращают объекты Promise.**](#callbacks-converted-to-promises) Все существующие функции с параметром обратного вызова были модернизированы, чтобы возвращать объект JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)для улучшения обработки асинхронных операций и удобочитаемости кода.

* [**Теперь API организованы в *возможности*.**](#apis-organized-into-capabilities) Вы можете рассматривать возможности как логические группы API-интерфейсов, которые предоставляют схожие функции, такие как `authentication`, `calendar`, `mail`, `monetization`, `meeting`, и `sharing`.

 Вы можете использовать [расширение Teams Toolkit](https://aka.ms/teams-toolkit) для Microsoft Visual Studio Code, чтобы упростить процесс обновления приложения Teams, как описано в следующем разделе.

> [!NOTE]
> Для включения существующего приложения Teams для запуска в Outlook и Office требуется следующее:
>
> 1. Зависимость от `@microsoft/teams-js@2.0.0-beta.1` или более поздней и
> 2. Изменение существующего кода приложения в соответствии с требуемыми изменениями, описанными в этом документе.
>
> Если вы ссылались на `@microsoft/teams-js@2.0.0-beta.1` (или более поздней версии) из существующего приложения Teams, вы увидите предупреждения об устаревании, если ваш код вызывает API, которые изменились. Уровень перевода API (сопоставление текущего пакета SDK с предварительными вызовами API SDK) предоставляется, чтобы позволить существующим приложениям Teams продолжать работу в Teams до тех пор, пока они не смогут обновить код для работы с TeamsJS SDK v2 Preview. После обновления кода с изменениями, описанными в этой статье, личная вкладка также будет работать в Outlook и Office.

## <a name="updating-to-the-teams-client-sdk-v2-preview"></a>Обновление до предварительной версии SDK клиента Teams v2

Самый простой способ обновить приложение Teams для использования предварительной версии TeamsJS SDK v2 — использовать [Расширение Teams Toolkit](https://aka.ms/teams-toolkit) для Visual Studio Code. Этот раздел поможет вам сделать это пошагово. Если вы предпочитаете обновлять свой код вручную, см. разделы [Обратные вызовы, преобразованные в Promise](#callbacks-converted-to-promises), и [API, организованные в разделы возможностей](#apis-organized-into-capabilities), чтобы получить дополнительные сведения о необходимых изменениях API.

### <a name="1-install-the-latest-teams-toolkit-visual-studio-code-extension"></a>1. Установите последнее расширение Teams Toolkit Visual Studio Code.

В *Visual Studio Code Extensions Marketplace*, найдите **Teams Toolkit** и установите версию `2.10.0` или более позднюю. Инструментарий предоставляет две команды для помощи в этом процессе:

1. Команда для обновления схемы манифеста
1. Команда для обновления ссылок на SDK и сайтов вызовов

Ниже приведены два ключевых обновления, которые вам потребуются для запуска приложения с личной вкладкой Teams в других приложениях Microsoft 365: ``

### <a name="2-updating-the-manifest"></a>2. Обновление манифеста

# <a name="teams-toolkit"></a>[Набор средств Teams](#tab/manifest-teams-toolkit)

1. Откройте *Палитру команд*: `Ctrl+Shift+P`
1. Запустите **Teams: обновите манифест Teams для поддержки команды приложений** Outlook и Office и выберите файл манифеста приложения. Изменения будут внесены на месте.

# <a name="manual-steps"></a>[Выполнение вручную](#tab/manifest-manual)

Откройте манифест приложения Teams и обновите `$schema` и `manifestVersion` со следующими значениями:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Если вы использовали Teams Toolkit для создания личного приложения, вы также можете использовать его для проверки изменений в файле манифеста и выявления ошибок. Откройте палитру команд `Ctrl+Shift+P` и найдите **Teams: проверьте файл манифеста** или выберите параметр в меню ''Развертывание'' набора инструментов Teams (найдите значок Teams в левой части кода Visual Studio).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Параметр Teams Toolkit &quot;Проверить файл манифеста&quot; в меню &quot;Развертывание&quot;":::

### <a name="2-update-sdk-references"></a>2. Обновление ссылок на SDK

Для работы в Outlook и Office ваше приложение должно зависеть от [пакета npm](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0-beta.1) `@microsoft/teams-js@2.0.0-beta.1` (или более поздней *бета-версии*). Для запуска в Outlook и Office ваше приложение должно быть зависимым. Чтобы выполнить эти действия вручную и получить дополнительные сведения об изменениях API, см. следующие разделы, посвященные [обратным вызовам, преобразованным в promise](#callbacks-converted-to-promises), и [API, организованным в возможности](#apis-organized-into-capabilities).

1. Убедитесь, что у вас есть [Teams Toolkit](https://aka.ms/teams-toolkit) `v2.10.0` или более поздний.
1. Откройте *Палитру команд*: `Ctrl+Shift+P`
1. Выполните команду `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

После завершения утилита обновит файл `package.json` с помощью зависимости предварительной версии TeamsJS SDK v2 (`@microsoft/teams-js@2.0.0-beta.1` или более поздней версии), а файлы `*.js/.ts` и `*.jsx/.tsx` будут обновлены:

> [!div class="checklist"]
>
> * `package.json` ссылки на предварительную версию TeamsJS SDK v2
> * Операторы импорта для TeamsJS SDK v2 предварительной версии
> * [Вызовы функций, Enum и интерфейса ](#apis-organized-into-capabilities) для TeamsJS SDK v2 предварительной версии
> * `TODO` напоминания о комментариях для просмотра областей, на которые могут повлиять изменения интерфейса [Контекста](#updates-to-the-context-interface)
> * `TODO` напоминания о комментариях, чтобы обеспечить успешное [преобразование функций promise из функций стиля обратного вызова](#callbacks-converted-to-promises) прошло успешно на каждом сайте вызова, найденном инструментом

> [!IMPORTANT]
> Код в HTML-файлах не поддерживается инструментами обновления и требует внесения изменений вручную.

## <a name="callbacks-converted-to-promises"></a>Вызовы, преобразованные в promise

API-интерфейсы Teams, которые ранее принимали параметр обратного вызова, были обновлены для возврата объекта JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). К ним относятся следующие API:

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, core.executeDeepLink, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, media.captureImage, media.getMedia, media.selectMedia, media.viewImages, media.scanBarCode, meeting.getAppContentStageSharingCapabilities, meeting.getAuthenticationTokenForAnonymousUser, meeting.getIncomingClientAudioState, meeting.getLiveStreamState, meeting.getMeetingDetails, meeting.requestStartLiveStreaming, meeting.requestStopLiveStreaming, meeting.shareAppContentToStage, meeting.stopSharingAppContentToStage, meeting.toggleIncomingClientAudio, meeting.getAppContentStageSharingState, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.config.setConfig, pages.config.getConfig, people.selectPeople, ChildAppWindow.postMessage, ParentAppWindow.postMessage
```

Вам нужно будет обновить способ, которым ваш код вызывает любой из этих API, чтобы использовать promise. Например, если код вызывает Teams API следующим образом:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Этот код:

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => { /* ... */ });
```

Необходимо обновить до:

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context) => {
    /*...*/
});
```

... или эквивалентного `async/await` шаблона:

```js
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context = await app.getContext();
  /*...*/
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Этот код:

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context: microsoftTeams.Context) => {
  /* ... */
});
```

Необходимо обновить до:

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

... или эквивалентного `async/await` шаблона:

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

---

> [!TIP]
> Когда вы обновляете код для TeamsJS SDK v2 Preview с помощью [Teams Toolkit](#updating-to-the-teams-client-sdk-v2-preview), необходимые обновления помечаются для вас `TODO` комментариями в клиентском коде.

## <a name="apis-organized-into-capabilities"></a>API организованы в возможности

*Возможность* — это логическая группа API-интерфейсов, предоставляющих схожие функции. Вы можете думать о Microsoft Teams, Outlook и Office как об узлах. Узел поддерживает данную возможность, если он поддерживает все API, определенные в этой возможности. Узел не может частично реализовать возможность.  Возможности могут быть основаны на функциях или контенте, например, *диалог* или *проверка подлинности*. Существуют также возможности для типов приложений, таких как *вкладки и страницы* или *боты*, и другие группы.

В TeamsJS SDK v2 Preview API-интерфейсы определяются как функции в пространстве имен JavaScript, имя которых соответствует их требуемым возможностям. Если приложение работает на узле, который поддерживает возможность диалога, то приложение может безопасно вызывать такие API, как `dialog.open` (в дополнение к другим API, связанным с диалогом, определенным в пространстве имен). Между тем, если приложение попытается вызвать API, который не поддерживается на этом узле, API выдаст исключение.

### <a name="differentiate-your-app-experience"></a>Сделайте свой опыт работы с приложением особенным

Вы можете проверить поддержку узлом данной возможности во время выполнения, вызвав функцию `isSupported()` для этой возможности (пространства имен). Он возвращает `true` если он поддерживается и `false` если нет, и вы можете настроить поведение приложения соответствующим образом. Это позволяет приложению освещать пользовательский интерфейс и функциональность на узлах, которые его поддерживают, продолжая работать на узлах, которые этого не делают.

Имя узла, на котором работает ваше приложение, отображается как свойство *hostName* в интерфейсе Context (`app.Context.app.host.name`), которое можно запросить во время выполнения, вызвав `getContext`. Он также доступен в качестве `{hostName}` [значения заполнителя URL](../tabs/how-to/access-teams-context.md#get-context-by-inserting-url-placeholder-values). Лучшей практикой является экономное использование механизма *hostName*:

* **Не** предполагайте, что определенные функции доступны или недоступны на узле на основе значения свойства *hostName*. Вместо этого проверьте наличие поддержки возможностей (`isSupported`).
* **Не** используйте *hostName* для блокировки вызовов API. Вместо этого проверьте наличие поддержки возможностей (`isSupported`).
* **Используйте** *hostName*, чтобы различать тему вашего приложения в зависимости от узла, на котором оно работает. Например, вы можете использовать фиолетовый цвет Microsoft Teams в качестве основного цвета акцента при работе в Teams и синий цвет Outlook при работе в Outlook.
* **Используйте** *hostName*, чтобы различать сообщения, отображаемые пользователю, в зависимости от того, на каком хосте он работает. Например, покажите *Управление задачами в Office* при работе в Office в Интернете и *Управление задачами в Teams* при работе в Microsoft Teams.

### <a name="namespaces"></a>Пространства имен

TeamsJS SDK v2 Preview организует API в *возможности* посредством пространств имен. Несколько новых пространств имен, имеющих особое значение, — *приложение*, *страницы*, *диалог*, и *teamsCore*.

#### <a name="app-namespace"></a>*приложение* пространство имен

Пространство имен `app` содержит API-интерфейсы верхнего уровня, необходимые для общего использования приложений в Microsoft Teams, Office и Outlook. Все API-интерфейсы из различных других пространств имен TeamsJS были перемещены в пространство имен `app` в TeamsJS SDK v2 Preview:

| Исходное пространство имен `global (window)` | Новое пространство имен `app` |
| - | - |
| `initialize` | `app.initialize` |
| `getContext` | `app.getContext` |
| `registerOnThemeChangeHandler` | `app.registerOnThemeChangeHandler` |

| Исходное пространство имен `appInitialization` | Новое пространство имен `app` |
| - | - |
| `appInitialization.notifyAppLoaded` | `app.notifyAppLoaded` |
| `appInitialization.notifySuccess` | `app.notifySuccess` |
| `appInitialization.notifyFailure` | `app.notifyFailure` |
| `appInitialization.notifyExpectedFailure` | `app.notifyExpectedFailure` |
| Перечисление `appInitialization.FailedReason` | `app.FailedReason` |
| Перечисление `appInitialization.ExpectedFailureReason` | `app.ExpectedFailureReason` |
| Перечисление `appInitialization.IFailedRequest` | `app.IFailedRequest` |
| Перечисление `appInitialization.IExpectedFailureRequest` | `app.IExpectedFailureRequest` |

#### <a name="core-namespace"></a>*основное* пространство имен

Пространство имен `core` включает функции для глубоких ссылок.

| Исходное пространство имен `publicAPIs` | Новое пространство имен `core` |
| - | - |
| `shareDeepLink` | `core.shareDeepLink` |
| `executeDeepLink` | `core.executeDeepLink` |

#### <a name="pages-namespace"></a>*страницы* пространства имен

Пространство имен `pages` включает функции для запуска веб-страниц и навигации по ним в различных клиентах Microsoft 365, включая Teams, Office и Outlook Оно также включает в себя несколько подвозможностей, реализованных в виде подпространств имен.

| Исходное пространство имен `global (window)` | Новое пространство имен `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame` (переименовано) |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |

##### <a name="pagestabs"></a>*pages.tabs*

| Исходное пространство имен `global (window)` | Новое пространство имен `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |
| `navigateToTab` | `pages.tabs.navigateToTab` |

| Исходное пространство имен `navigation` | Новое пространство имен `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

##### <a name="pagesconfig"></a>*pages.config*

| Исходное пространство имен `settings` | Новое пространство имен `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig` (переименовано)
| `settings.getSettings` | `pages.config.getConfig` (переименовано)
| `settings.setValidityState`| `pages.config.setValidityState`
| `settings.initialize` | `pages.config.initialize`
| `settings.registerOnSaveHandler`| `pages.config.registerOnSaveHandler`
| `settings.registerOnRemoveHandler` | `pages.config.registerOnRemoveHandler`
| интерфейс `settings.Settings` | `pages.config.Config` (переименовано)
| интерфейс `settings.SaveEvent` | `pages.config.SaveEvent` (переименовано)
| интерфейс `settings.RemoveEvent` | `pages.config.RemoveEvent` (переименовано)
| интерфейс `settings.SaveParameters` | `pages.config.SaveParameters` (переименовано)
| интерфейс `settings.SaveEventImpl` | `pages.config.SaveEventImpl` (переименовано)

| Исходное пространство имен `global (window)` | Новое пространство имен `pages.config` |
| - | - |
| `registerEnterSettingsHandler` | `pages.config.registerChangeConfigHandler` (переименовано)

##### <a name="pagesbackstack"></a>*pages.backStack*

| Исходное пространство имен `navigation` | Новое пространство имен `pages.backStack`  |
| - | - |
| `navigation.navigateBack` | `pages.backStack.navigateBack`

| Исходное пространство имен `global (window)` | Новое пространство имен `pages.backStack`  |
| - | - |
| `registerBackButtonHandler` | `pages.backStack.registerBackButtonHandler`

##### <a name="pagesappbutton"></a>*pages.appButton*

| Исходное пространство имен `global (window)` | Новое пространство имен `pages.appButton`  |
| - | - |
| `registerAppButtonClickHandler` | `pages.appButton.onClick` (переименовано)
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter` (переименовано)
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave` (переименовано)
| интерфейс `FrameContext`. | `pages.appButton.FrameInfo` (переименовано) |

#### <a name="dialog-namespace"></a>*диалог* пространства имен

Пространство имен *задачи* TeamsJS было переименовано в *диалог*, а следующие API были переименованы:

| Исходное пространство имен `tasks` | Новое пространство имен `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (переименовано) |
| `tasks.submitTasks` | `dialog.submit` (переименовано) |
| `tasks.updateTasks` | `dialog.resize` (переименовано) |
| перечисление `tasks.TaskModuleDimension` | `dialog.DialogDimension` (переименовано) |
| интерфейс `tasks.TaskInfo` | `dialog.DialogInfo` (переименовано) |

#### <a name="teamscore-namespace"></a>*teamsCore* пространство имен

Чтобы обобщить TeamsJS SDK для запуска других узлов Microsoft 365, таких как Office и Outlook, функции Teams (первоначально в *глобальном* пространстве имен) были перемещены в пространство имен *teamsCore*:

| Исходное пространство имен `global (window)` | Новое пространство имен `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`
| `registerFocusEnterHandler` | `teamsCore.registerFocusEnterHandler`

### <a name="updates-to-the-context-interface"></a>Обновления интерфейса *Контекста*

Интерфейс `Context` был перемещен в пространство имен `app` и обновлен, чтобы сгруппировать схожие свойства для лучшей масштабируемости, поскольку он работает в Outlook и Office, а также в Teams.

Добавлено новое свойство `app.Context.app.host.name`, позволяющее персональным вкладкам различать взаимодействие с пользователем в зависимости от основного приложения.

Вы также можете визуализировать изменения, просмотрев функцию [`transformLegacyContextToAppContext`](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/src/public/app.ts) в исходном коде TeamsJS SDK v2 Preview.

| Исходное имя в интерфейсе `Context` | Новое местоположение в `app.Context` |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *НЕ В предварительной версии Teams client SDK v2* |
| `appSessionId` | `app.Context.app.sessionId`|
| `channelId`| `app.Context.channel.id` |
| `channelName`| `app.Context.channel.displayName`|
| `channelRelativeUrl` | `app.Context.channel.relativeUrl`|
| `channelType`| `app.Context.channel.membershipType` |
| `chatId` | `app.Context.chat.id`|
| `defaultOneNoteSectionId`| `app.Context.channel.defaultOneNoteSectionId`|
| `entityId` | `app.Context.page.id`|
| `frameContext` | `app.Context.page.frameContext`|
| `groupId`| `app.Context.team.groupId` |
| `hostClientType` | `app.Context.app.host.clientType`|
| `hostTeamGroupId`| `app.Context.channel.ownerGroupId` |
| `hostTeamTenantId` | `app.Context.channel.ownerTenantId`|
| `isCallingAllowed` | `app.Context.user.isCallingAllowed`|
| `isFullScreen` | `app.Context.page.isFullScreen`|
| `isMultiWindow`| `app.Context.page.isMultiWindow` |
| `isPSTNCallingAllowed` | `app.Context.user.isPSTNCallingAllowed`|
| `isTeamArchived` | `app.Context.team.isArchived`|
| `locale` | `app.Context.app.locale` |
| `loginHint`| `app.Context.user.loginHint` |
| `meetingId`| `app.Context.meeting.id` |
| `osLocaleInfo` | `app.Context.app.osLocaleInfo` |
| `parentMessageId`| `app.Context.app.parentMessageId`|
| `ringId` | `app.Context.app.host.ringId`|
| `sessionId`| `app.Context.app.host.sessionId` |
| `sourceOrigin` | `app.Context.page.sourceOrigin`|
| `subEntityId`| `app.Context.page.subPageId` |
| `teamId` | `app.Context.team.internalId`|
| `teamSiteDomain` | `app.Context.sharepointSite.domain`|
| `teamSitePath` | `app.Context.sharepointSite.path`|
| `teamSiteUrl`| `app.Context.sharepointSite.url` |
| `teamTemplateId` | `app.Context.team.templateId`|
| `teamType` | `app.Context.team.type`|
| `tenantSKU`| `app.Context.user.tenant.teamsSku` |
| `tid`| `app.Context.user.tenant.id` |
| `upn` | `app.Context.user.userPrincipalName` |
|`userClickTime`| `app.Context.app.userClickTime`|
| `userFileOpenPreference` | `app.Context.app.userFileOpenPreference` |
| `userLicenseType`| `app.Context.user.licenseType` |
| `userObjectId` | `app.Context.user.id`|
| `userTeamRole` | `app.Context.team.userRole`|
| `userDisplayName` | `app.Context.user.displayName` |
| Недоступно | `app.Context.app.host.name`|

## <a name="next-steps"></a>Дальнейшие действия

Вы также можете узнать больше о критических изменениях в [журнале изменений предварительной версии TeamsJS SDK v2](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/CHANGELOG.md) и в [справочнике API TeamsJS SDK v2 Preview](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true).

Когда вы будете готовы протестировать приложения Teams, работающие в Outlook и Office, см.:

> [!div class="nextstepaction"]
> [Расширьте возможности своего приложения Teams в Microsoft 365](overview.md)
