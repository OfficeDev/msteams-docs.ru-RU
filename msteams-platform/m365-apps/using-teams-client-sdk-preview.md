---
title: Microsoft Teams JavaScript клиент SDK v2 Preview
description: Понимание изменений, происходящих с Microsoft Teams javaScript клиента SDK v2 Preview
ms.date: 11/15/2021
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 7a8b5ed919cac07b1d0710a1f23c0ade0cca2ffb
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059823"
---
# <a name="microsoft-teams-javascript-client-sdk-v2-preview"></a>Microsoft Teams JavaScript клиент SDK v2 Preview

С [клиентом Microsoft Teams JavaScript SDK v2 Preview](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true)существующий Teams SDK (или просто) был рефактором, чтобы позволить Teams разработчикам возможность расширения Teams приложений для запуска в Outlook и `@microsoft/teams-js` `TeamsJS` [Office](overview.md). С функциональной точки зрения, TeamsJS SDK v2 Preview () является суперсетью текущего teamsJS SDK, он поддерживает существующие функции Teams приложений, добавляя возможность для Teams приложений в `@microsoft/teams-js@next` Outlook и Office.

Существует два значительных изменения в командной версии SDK v2 Preview, которые коду потребуется учитывать для запуска в других Microsoft 365 приложениях:

* [**Функции обратного вызова теперь возвращают объекты Promise.**](#callbacks-converted-to-promises) Все существующие функции с параметром обратного вызова были модернизированы, чтобы вернуть объект JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) для улучшения обработки асинхронных операций и читаемости кода.

 - [**API теперь организованы в *возможности.***](#apis-organized-into-capabilities) Вы можете думать о возможностях как логические группировки API, которые предоставляют аналогичные функции, такие как `authentication` , , , , , и `calendar` `mail` `monetization` `meeting` `sharing` .

 Вы можете использовать расширение [Teams набор средств](https://aka.ms/teams-toolkit) для Visual Studio Code, чтобы упростить процесс обновления Teams приложения, как описано в следующем разделе.

> [!NOTE]
> Для включения существующего Teams приложения в Outlook и Office требуется:
> 1. Зависимость от или `@microsoft/teams-js@2.0.0-beta.1` более поздней и
> 2. Изменение существующего кода приложения в соответствии с требуемой изменениями, описанными в этом документе.
>
>  Если вы ссылались (или позже) из существующего приложения Teams, вы увидите предупреждения об амортизации, если код вызывает измененные `@microsoft/teams-js@2.0.0-beta.1` API. Уровень перевода API (сопоставление текущих вызовов SDK для предварительного просмотра вызовов API SDK) предоставляется для того, чтобы существующие Teams приложения могли продолжать работать в Teams, пока они не смогут обновить код для работы с командной версией SDK v2 Preview. После обновления кода с изменениями, описанными в этой статье, ваша личная вкладка также будет работать в Outlook и Office.

## <a name="updating-to-the-teams-client-sdk-v2-preview"></a>Обновление до Teams клиента SDK v2 Preview

Самый простой способ обновления Teams приложения для использования командных версий SDK v2 Preview — использовать расширение Teams набор средств для Visual Studio Code. [](https://aka.ms/teams-toolkit) В этом разделе вы сможете ходить по этим шагам. Если вы предпочитаете вручную обновлять код, см. в разделах [Callbacks,](#callbacks-converted-to-promises) преобразованных в обещания и API, организованные в разделы возможностей, дополнительные сведения об необходимых изменениях API. [](#apis-organized-into-capabilities)

### <a name="1-install-the-latest-teams-toolkit-vs-code-extension"></a>1. Установка последнего Teams набор средств VS Code расширения

В Visual Studio Code *Расширения Marketplace*, поиск **Teams набор средств** и установить `2.10.0` версию или позже. Набор инструментов предоставляет две команды для оказания помощи процессу:

1. Команда обновления схемы манифеста
1. Команда обновления ссылок и сайтов вызовов SDK

Ниже следующую информацию о двух основных обновлениях, необходимых для запуска приложения Teams вкладок в других Microsoft 365 приложениях: ''

### <a name="2-updating-the-manifest"></a>2. Обновление манифеста

# <a name="teams-toolkit"></a>[Teams набор средств](#tab/manifest-teams-toolkit)

1. Откройте *палитру Команд:*`Ctrl+Shift+P`
1. Запуск **Teams:** манифест обновления Teams для поддержки Outlook и Office приложений и выбора файла манифеста приложения. Изменения будут внесены на месте.

# <a name="manual-steps"></a>[Действия вручную](#tab/manifest-manual)

Откройте манифест Teams приложения и обновите `$schema` следующие `manifestVersion` значения:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

Если вы Teams набор средств для создания личного приложения, вы также можете использовать его для проверки изменений в файле манифеста и выявления ошибок. Откройте палитру команд и Teams: проверьте файл манифеста или выберите параметр из меню развертывания Teams набор средств (найдите значок Teams слева от `Ctrl+Shift+P` Visual Studio Code). 

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams набор средств параметр &quot;Проверка файла манифеста&quot; в меню &quot;Развертывание&quot;":::

### <a name="2-update-sdk-references"></a>2. Обновление ссылок на SDK

Чтобы запустить Outlook и Office, вашему приложению необходимо будет зависеть от [пакета npm](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0-beta.1) (или более `@microsoft/teams-js@2.0.0-beta.1` *поздней бета-версии).* Для выполнения этих действий вручную и получения дополнительных сведений [](#callbacks-converted-to-promises) об изменениях API см. в следующих разделах об обратном вызове, преобразованных в обещания и API, организованных [в возможности.](#apis-organized-into-capabilities)

1. Убедитесь, что [Teams набор средств](https://aka.ms/teams-toolkit) `v2.10.0` или позже
1. Откройте *палитру Команд:*`Ctrl+Shift+P`
1. Запуск команды `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

После завершения утилита обновит файл с зависимостью `package.json` TeamsJS SDK v2 Preview (или более поздней версии), а ваши файлы и файлы будут обновлены с `@microsoft/teams-js@2.0.0-beta.1` `*.js/.ts` `*.jsx/.tsx` помощью:

> [!div class="checklist"]
> * `package.json` ссылки на TeamsJS SDK v2 Preview
> * Отчеты об импорте для TeamsJS SDK v2 Preview
> * [Вызовы функции, enum и интерфейса](#apis-organized-into-capabilities) в TeamsJS SDK v2 Preview
> * `TODO`напоминания о комментариях для просмотра областей, на которые могут повлиять изменения [интерфейса Context](#updates-to-the-context-interface)
> * `TODO` напоминания комментариев для обеспечения преобразования функций [обещаний](#callbacks-converted-to-promises) из функций стилей вызова прошли хорошо на каждом сайте вызова найденного средства

> [!IMPORTANT]
> Код внутри html-файлов не поддерживается инструментом обновления и требует ручных изменений.

## <a name="callbacks-converted-to-promises"></a>Вызовы, преобразованные в обещания

Teams API, которые ранее брали параметр обратного вызова, были обновлены, чтобы вернуть объект JavaScript [Promise.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) К ним относятся следующие API:

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, core.executeDeepLink, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, media.captureImage, media.getMedia, media.selectMedia, media.viewImages, media.scanBarCode, meeting.getAppContentStageSharingCapabilities, meeting.getAuthenticationTokenForAnonymousUser, meeting.getIncomingClientAudioState, meeting.getLiveStreamState, meeting.getMeetingDetails, meeting.requestStartLiveStreaming, meeting.requestStopLiveStreaming, meeting.shareAppContentToStage, meeting.stopSharingAppContentToStage, meeting.toggleIncomingClientAudio, meeting.getAppContentStageSharingState, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.config.setConfig, pages.config.getConfig, people.selectPeople, ChildAppWindow.postMessage, ParentAppWindow.postMessage
```

Вам потребуется обновить способ вызова кодом любого из этих API для использования обещаний. Например, если код вызывает API Teams так:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Этот код:

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => { /* ... */ });
```

Необходимо обновить:

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

... или эквивалентный `async/await` шаблон:

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

Необходимо обновить:

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

... или эквивалентный `async/await` шаблон:

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

---

> [!TIP]
> При обновлении кода для teamsJS SDK v2 Preview с [Teams набор средств,](#updating-to-the-teams-client-sdk-v2-preview)необходимые обновления помечены для вас с комментариями в `TODO` клиентском коде.

## <a name="apis-organized-into-capabilities"></a>API, организованные в возможности

Возможность *— это* логическая группировка API, которые предоставляют аналогичные функции. В качестве хостов Microsoft Teams, Outlook и Office. Хост поддерживает заданную возможность, если поддерживает все API, определенные в этой возможности. Хост не может частично реализовать функцию.  Возможности могут быть на основе функций или контента, таких как *диалоговое окно* или *проверка подлинности.* Существуют также возможности для типов приложений, таких как *вкладки/страницы* или *боты* и другие группировки.

В предварительной версии TeamsJS SDK v2 API определяются как функции в пространстве имен JavaScript, имя которого соответствует их требуемой возможности. Если приложение работает в хосте, поддерживающего диалоговое окно, приложение может безопасно вызывать API, такие как (в дополнение к другим API, связанным с диалогом, определенным в пространстве `dialog.open` имен). Тем временем, если приложение пытается вызвать API, который не поддерживается в этом хосте, API бросает исключение.

### <a name="differentiate-your-app-experience"></a>Дифференцируйте ваш опыт работы с приложением

Вы можете проверить поддержку хост-службы данной возможности во время работы, позвонив в эту функцию `isSupported()` (пространство имен). Он `true` возвращается, если поддерживается, а если нет, и вы можете настроить `false` поведение приложения по мере необходимости. Это позволяет приложению зажигать пользовательский интерфейс и функциональные возможности в поддерживающих его хостах, продолжая запускать для не поддерживающих хостов.

Имя хоста, в котором работает приложение, подвергается воздействию свойства *hostName* в интерфейсе Context (), которое можно запрашивать во время запуска `app.Context.app.host.name` по вызову `getContext` . Он также доступен в качестве `{hostName}` [значения задатки URL-адресов.](../tabs/how-to/access-teams-context.md#get-context-by-inserting-url-placeholder-values) Лучше всего использовать механизм *hostName* экономно:

* **Не предполагайте,** что определенные функции доступны или недоступны в хост-сайте на основе значения *свойства hostName.* Вместо этого проверьте поддержку возможностей ( `isSupported` ).
* **Не используйте** *hostName для* входа вызовов API. Вместо этого проверьте поддержку возможностей ( `isSupported` ).
* **Используйте** *имя hostName* для дифференцированной темы приложения в зависимости от используемого в них хоста. Например, вы можете использовать Microsoft Teams в качестве основного цвета акцента при работе в Teams и Outlook при Outlook.
* **Используйте** *имя hostName* для дифференцированных сообщений, показанных пользователю в зависимости от того, в какой хост он запущен. Например, покажите управление задачами в *Office* при Office в Интернете и  управление задачами в Teams при Microsoft Teams.

### <a name="namespaces"></a>Пространства имен

Командная группа SDK v2 Preview организует API в *возможности* с помощью пространств имен. Несколько новых пространств имен, которые имеют особое значение, это *приложения,* *страницы,* *диалоговое окно* и *teamsCore.*

#### <a name="app-namespace"></a>*Пространство имен* приложений

Пространство имен содержит API верхнего уровня, необходимые для общего использования приложений, `app` Microsoft Teams, Office и Outlook. Все API из различных других пространств имен TeamsJS были перемещены в пространство имен `app` в TeamsJS SDK v2 Preview:

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
| `appInitialization.FailedReason` enum | `app.FailedReason` |
| `appInitialization.ExpectedFailureReason` enum | `app.ExpectedFailureReason` |
| `appInitialization.IFailedRequest` enum | `app.IFailedRequest` |
| `appInitialization.IExpectedFailureRequest` enum | `app.IExpectedFailureRequest` |

#### <a name="core-namespace"></a>*пространство имен* core

Пространство `core` имен включает функции глубоких ссылок.

| Исходное пространство имен `publicAPIs` | Новое пространство имен `core` |
| - | - |
| `shareDeepLink` | `core.shareDeepLink` |
| `executeDeepLink` | `core.executeDeepLink` |

#### <a name="pages-namespace"></a>*пространство* имен страниц

Пространство имен включает функции для запуска и навигации веб-страниц в различных Microsoft 365 `pages` клиентах, включая Teams, Office и Outlook. Он также включает несколько под-возможностей, реализованных в качестве подимейных пространств.

| Исходное пространство имен `global (window)` | Новое пространство имен `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame` (переименован) |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |

##### <a name="pagestabs"></a>*pages.tabs*

| Исходное пространство имен `global (window)` | Новое пространство имен `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |
| ` navigateToTab` | `pages.tabs.navigateToTab` |

| Исходное пространство имен `navigation` | Новое пространство имен `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

##### <a name="pagesconfig"></a>*pages.config*

| Исходное пространство имен `settings` | Новое пространство имен `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig` (переименован)
| `settings.getSettings` | `pages.config.getConfig` (переименован)
| `settings.setValidityState`| `pages.config.setValidityState`
| `settings.initialize` | `pages.config.initialize`
| `settings.registerOnSaveHandler`| `pages.config.registerOnSaveHandler`
| `settings.registerOnRemoveHandler` | `pages.config.registerOnRemoveHandler`
| `settings.Settings` интерфейс | `pages.config.Config` (переименован)
| `settings.SaveEvent` интерфейс | `pages.config.SaveEvent` (переименован)
| `settings.RemoveEvent` интерфейс | `pages.config.RemoveEvent` (переименован)
| `settings.SaveParameters` интерфейс | `pages.config.SaveParameters` (переименован)
| `settings.SaveEventImpl` интерфейс | `pages.config.SaveEventImpl` (переименован)

| Исходное пространство имен `global (window)` | Новое пространство имен `pages.config` |
| - | - |
| `registerEnterSettingsHandler` | `pages.config.registerChangeConfigHandler` (переименован)

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
| `registerAppButtonClickHandler` | `pages.appButton.onClick` (переименован)
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter` (переименован)
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave` (переименован)
| `FrameContext` интерфейс | `pages.appButton.FrameInfo` (переименован)) |

#### <a name="dialog-namespace"></a>*пространство имен диалогов*

Пространство имен  задач TeamsJS было переименовано в диалоговое *окно,* а следующие API переименованы:

| Исходное пространство имен `tasks` | Новое пространство имен `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (переименован) |
| `tasks.submitTasks` | `dialog.submit` (переименован) |
| `tasks.updateTasks` | `dialog.resize` (переименован) |
| `tasks.TaskModuleDimension` enum | `dialog.DialogDimension` (переименован) |
| `tasks.TaskInfo` интерфейс | `dialog.DialogInfo` (переименован) |

#### <a name="teamscore-namespace"></a>*TeamsCore* namespace

Для обобщения SDK TeamsJS для запуска других хостов Microsoft 365, таких как Office и Outlook, Teams-специфические  функции (первоначально в глобальном пространстве имен) были перемещены в пространство имен *teamsCore:*

| Исходное пространство имен `global (window)` | Новое пространство имен `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`
| `registerFocusEnterHandler` | `teamsCore.registerFocusEnterHandler`

### <a name="updates-to-the-context-interface"></a>Обновления интерфейса *Context*

Интерфейс был перемещен в пространство имен и обновлен для группы аналогичных свойств для лучшей масштабируемости, поскольку он выполняется в Outlook и Office, а также `Context` `app` Teams.

Добавлено новое свойство, которое позволяет личные вкладки различать пользовательский интерфейс в зависимости `app.Context.app.host.name` от хост-приложения.

Вы также можете визуализировать изменения, просмотрев функцию в источнике Предварительного просмотра  [`transformLegacyContextToAppContext`](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/src/public/app.ts) TeamsJS SDK v2.

| Исходное имя в `Context` интерфейсе | Новое расположение в `app.Context` |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *NOT IN Teams SDK v2 Preview* |
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
|` userClickTime`| `app.Context.app.userClickTime`|
| `userFileOpenPreference` | `app.Context.app.userFileOpenPreference` |
| `userLicenseType`| `app.Context.user.licenseType` |
| `userObjectId` | `app.Context.user.id`|
| ` userTeamRole` | `app.Context.team.userRole`|
| `userDisplayName` | `app.Context.user.displayName` |
| Недоступно | `app.Context.app.host.name`|

## <a name="next-steps"></a>Дальнейшие действия

Вы также можете узнать больше о том, как изменить изменения в командной версии [SDK v2 Preview и](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/CHANGELOG.md) ссылке на API предварительного просмотра [TeamsJS SDK v2.](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true)

Когда вы будете готовы проверить свои Teams приложения, работающие в Outlook и Office, см. в этой Office.

> [!div class="nextstepaction"]
> [Расширите Teams приложение в Microsoft 365](overview.md)
