---
title: Клиентский SDK JavaScript для Teams
author: heath-hamilton
ms.author: surbhigupta
description: В этом модуле вы узнаете о пакете SDK для клиента Microsoft Teams JavaScript, помогающем в создании приложений Teams, размещенных в <iframe> в Teams, Office и Outlook.
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: ca5a02a067c44aaeab52bdde3c7be3a45c6797df
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100156"
---
# <a name="teams-javascript-client-sdk"></a>Клиентский SDK JavaScript для Teams

Клиентский пакет SDK Microsoft Teams для JavaScript помогает создавать размещенные функции Teams, то есть приложения, интерфейсы которых размещаются в [iframe](https://developer.mozilla.org/docs/Web/HTML/Element/iframe). Пакет SDK полезен для разработки приложений со следующими возможностями Teams:

* [Вкладки](../../tabs/what-are-tabs.md)
* [Диалоги (модули задач)](../../task-modules-and-cards/what-are-task-modules.md)

Начиная с версии `2.0.0`, существующий клиентский пакет SDK Teams (`@microsoft/teams-js` или просто `TeamsJS`) был переработан, чтобы запускать приложения Teams в [Outlook и Office](/microsoftteams/platform/m365-apps/overview), в дополнение к Microsoft Teams. С функциональной точки зрения последняя версия TeamsJS поддерживает весь спектр функций приложений Teams (версии 1.x.x), добавляя при этом дополнительную возможность размещения приложений Teams в Outlook и Office.

Здесь приводится действующее руководство по управления версиями для различных сценариев приложений.

[!INCLUDE [pre-release-label](~/includes/teamjs-version-details.md)]

Далее в этой статье вы узнаете о структуре и последних обновлениях клиентского пакета SDK Teams JavaScript.

### <a name="microsoft-365-support-running-teams-apps-in-office-and-outlook"></a>Поддержка Microsoft 365 (запуск приложений Teams в Office и Outlook)

TeamsJS версии 2.0 предоставляет возможность запуска определенных типов приложений Teams в экосистеме Microsoft 365. В настоящее время другие части экосистемы Microsoft 365 (в том числе Office и Outlook) для размещения приложений Teams поддерживают некоторое подмножество типов и возможностей приложений платформы Teams. Это подмножество будет постепенно расширяться. Общие сведения о поддержке размещения приложений Teams см. в разделе [Расширение приложений Teams на всю экосистему Microsoft 365](../../m365-apps/overview.md).

В следующей таблице перечислены вкладки, диалоговые окна (модули задач), и возможности (общедоступные пространства имен) Teams с расширенной поддержкой для выполнения в других частях экосистемы Microsoft 365.

> [!TIP]
> Чтобы проверить во время выполнения, поддерживает ли данное размещение конкретную возможность, вызовите для этой возможности (пространства имен) функцию `isSupported()`.

|Возможность | Поддержка ведущим приложением | Примечания |
|-----------|--------------|-------|
| приложение | Teams, Outlook, Office, приложение Office для Android | Пространство имен, представляющее инициализацию и жизненный цикл приложения. |
| appInitialization| | Устарело. Заменено пространством имен `app`. |
| appInstallDialog | Teams||
| authentication | Teams, Outlook, Office, приложение Office для Android | |
| calendar | Outlook ||
| call | Teams||
| чат |Teams||
| диалоговое окно | Teams, Outlook, Office | Пространство имен, представляющее диалоговые окна (ранее назывались *модули задач*). См. документацию по [диалоговым окнам](#dialogs). |
| расположение; |Teams| См. документацию по теме [Разрешения приложения](#app-permissions).|
| почта; | Outlook (только классические приложения Windows)||
| мультимедиа |Teams| См. документацию по теме [Разрешения приложения](#app-permissions).|
| pages | Teams, Outlook, Office, приложение Office для Android | Пространство имен, представляющее навигацию по страницам. См. документацию по теме [Глубокая компоновка](#deep-linking). |
| people |Teams||
| settings || Устарело. Заменено на `pages.config`.|
| предоставляет общий доступ к | Teams||
| tasks | | Устарело. Заменено возможностью `dialog`. См. документацию по [диалоговым окнам](#dialogs).|
| teamsCore | Teams | Пространство имен, содержащее специфическую функциональность Teams.|
| video | Teams||

#### <a name="app-permissions"></a>Разрешения приложения

Возможности приложений, требующие, чтобы пользователь предоставил [разрешения устройства](../../concepts/device-capabilities/device-capabilities-overview.md) (например, *расположение*), пока не поддерживаются для приложений, работающих за пределами Teams. В настоящее время нет способа проверить разрешения приложения в разделе "Параметры" или заголовке приложения при запуске в Outlook или Office. Если приложение Teams, работающее в Office или Outlook вызывает API-интерфейс TeamsJS или HTML5, активирующий разрешения устройства, этот API вызовет ошибку и не выведет системное диалоговое окно с запросом согласия пользователя.

Пока рекомендуется изменить код, чтобы перехватывать ошибку:

* Перед использованием возможности вызовите [isSupported()](#differentiate-your-app-experience), чтобы проверить совместимость. `media`, `meeting`и `files` пока не поддерживают вызовы *isSupported* и не работают вне Teams.
* Перехватывайте и обрабатывайте ошибки при вызове API TeamsJS и HTML5.

Если API не поддерживается или вызывает ошибку, добавьте программную логику для корректной обработки сбоя или обходное решение. Например:

* Перенаправьте пользователя на веб-сайт вашего приложения.
* Сообщите пользователю, что для выполнения потока операций следует использовать это приложение в Teams.
* Уведомите пользователя о недоступности функций.

Кроме того, рекомендуем проверять, указаны ли в манифесте приложения разрешения только на те устройства, которые оно использует.

#### <a name="deep-linking"></a>Создание прямых ссылок

До TeamsJS версии 2.0  все сценарии работы с глубинными ссылками обрабатывались с помощью `shareDeepLink` (для создания ссылки, ведущей *в* определенную часть приложения) и `executeDeepLink` (для перехода по глубинной ссылке *из* приложения или *внутри* приложения). В TeamsJS версии 2.0 добавлен новый API `navigateToApp` для последовательного перемещения по страницам и вложенным страницам внутри приложения по всем размещениям приложения (Office и Outlook в добавление к Teams). Вот обновленное руководство для сценариев работы с глубинными ссылками:

##### <a name="deep-links-into-your-app"></a>Прямые ссылки на приложение

Используйте функцию `pages.shareDeepLink` (в версиях TeamsJS ниже 2.0 называемую также *shareDeepLink*) для создания и вывода ссылки, которую пользователь может скопировать и поделиться ею. При щелчке пользователю будет предложено установить приложение, если оно еще не установлено для конкретного размещения (указанного в пути ссылки).

##### <a name="navigation-within-your-app"></a>Навигация внутри приложения

Используйте новый API `pages.navigateToApp` для навигации внутри вашего приложения, размещенного в другом приложении.

Этот API обеспечивает эквивалент перехода по глубинной ссылке (раньше для этой цели использовалась функция *executeDeepLink*, ныне выведенная из употребления), так что вашему приложению не нужно ни генерировать URL-адреса, ни управлять различными форматами прямых ссылок для разных размещений приложений.

##### <a name="deep-links-out-of-your-app"></a>Прямые ссылки, ведущие из приложения

Для прямых ссылок, ведущих из приложения в различные области текущего размещения, используйте строго типизированные API, предоставляемые пакетом SDK teamsJS. Например, используйте возможность *Календарь*, чтобы открыть из приложения диалоговое окно планирования или элемент календаря.

Для прямых ссылок из приложения в другие приложения, работающие в том же размещении, используйте `pages.navigateToApp`.

Для любых других внешних сценариев глубокой компоновки можно использовать функции, `app.openLink`аналогичные устаревшим (начиная с TeamsJS версии 2.0) API *executeDeepLink*.

#### <a name="dialogs"></a>Диалоговые окна

Начиная с версии 2.0 TeamsJS понятие платформы Teams [модуль задач](../../task-modules-and-cards/what-are-task-modules.md) было переименовано в *диалоговое окно* для улучшения согласованности с терминологией, уже существующей в экосистеме разработки Microsoft 365. Соответственно, пространство имен `tasks` устарело и заменено новым пространством имен, `dialog`.

Эта новая возможность диалогового окна разбивается на основную возможность (`dialog`) для поддержки диалогов на основе HTML и вложенную возможность (`dialog.bot`) для разработки диалогов на основе ботов.

Возможность диалогового окна пока не поддерживает [диалоги на основе адаптивных карточек](../../task-modules-and-cards/task-modules/design-teams-task-modules.md). Диалоги на основе адаптивных карточек по-прежнему необходимо вызывать с помощью `tasks.startTask()`.

Функция `dialog.open` в настоящее время работает только для открытия диалогов на основе HTML и возвращает функцию обратного вызова (`PostMessageChannel`), которую можно использовать для передачи сообщений (`ChildAppWindow.postMessage`) в только что открытое диалоговое окно.  `dialog.open` возвращает обратный вызов (а не обещание), так как не требует, чтобы приложение приостановило работу в ожидании закрытия диалогового окна (что обеспечивает большую гибкость для различных сценариев взаимодействия с пользователем).

## <a name="whats-new-in-teamsjs-version-20"></a>Новые возможности TeamsJS версии 2.0

Начиная с версии 2.0.0 появились два существенных изменения по сравнению с версиями TeamsJS 1.x.x:

* [**Функции обратного вызова теперь возвращают объекты Promise.**](#callbacks-converted-to-promises) Все существующие в TeamsJS v.1.12 функции с параметром обратного вызова были модернизированы, чтобы возвращать объект JavaScript [Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)(обещание) для улучшения обработки асинхронных операций и удобочитаемости кода.

* [**Теперь API организованы в *возможности*.**](#apis-organized-into-capabilities) Возможности можно рассматривать как логические группы API-интерфейсов, предоставляющих сходные функции, такие как `authentication`, `dialog`, `chat` и `calendar`. Каждое пространство имен представляет отдельную возможность.

> [!TIP]
> [Расширение Teams Toolkit](https://aka.ms/teams-toolkit) для Microsoft Visual Studio Code упрощает [процесс обновления приложения TeamsJS v.2.0](#updating-to-the-teams-client-sdk-v200), как описано в следующем разделе.

### <a name="backwards-compatibility"></a>Обратная совместимость

Начав ссылаться на `@microsoft/teams-js@2.0.0` или более позднюю версию из существующего приложения Teams, вы увидите предупреждения об устаревании при любом программном вызове API, которые были изменены.

Слой перевода API (сопоставление API пакета SDK версии 1 с API SDK версии 2) позволяет существующим приложениям Teams продолжать работу в Teams до тех пор, пока разработчики не обновят программный код для совместимости с шаблонами TeamsJS SDK v2.

#### <a name="teams-only-apps"></a>Приложения, работающие только в Teams

Даже если вы создаете приложение для работы только в Teams (а не в Office и Outlook), рекомендуем как можно скорее начать ссылаться на последнюю версию TeamsJS (версии не ниже *2.0*), чтобы воспользоваться последними улучшениями, новыми функциями и поддержкой (даже для приложений, предназначенных только для Teams). TeamsJS версии 1.12 все еще будет поддерживаться, но новые функции и улучшения в нее добавляться уже не будут..

Когда у вас появится такая возможность, [обновите существующий код приложения](#2-update-sdk-references), внеся изменения, описанные в этой статье. Пока что слой преобразования API версии 1 в версию 2 обеспечивает обратную совместимость, гарантируя, что существующее приложение Teams продолжит работать в TeamsJS версии 2.0.

#### <a name="teams-apps-running-across-microsoft-365"></a>Работа приложений Teams во всей экосистеме Microsoft 365

Чтобы приложение Teams могло работать в Outlook и Office, нужны все перечисленные ниже пункты.

1. Зависимость от TeamsJS версии не ниже 2.0 (`@microsoft/teams-js@2.0`)

2. [Переработка существующего кода приложения](#2-update-sdk-references) в соответствии с изменениями, описанными в этом документе.

3. [Обновление манифеста приложения](#3-update-the-manifest-optional) до версии не ниже 1.13.

Подробнее см. в разделе [Расширение функциональности приложений Teams на всю Microsoft 365](../../m365-apps/overview.md).

### <a name="callbacks-converted-to-promises"></a>Вызовы, преобразованные в promise

API-интерфейсы Teams, которые ранее принимали параметр обратного вызова, были обновлены для возврата объекта JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). К ним относятся следующие API:

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, app.openLink, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, chat.getChatMembers, conversations.openConversation, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.getConfig, pages.config.setConfig, pages.backStack.navigateBack, people.selectPeople, teams.fullTrust.getConfigSetting, teams.fullTrust.joinedTeams.getUserJoinedTeams
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
> При использовании [Teams Toolkit для обновления до TeamsJS версии 2.0](#updating-to-the-teams-client-sdk-v200) необходимые обновления в клиентском коде будут помечены `TODO` в комментариях.

### <a name="apis-organized-into-capabilities"></a>API организованы в возможности

*Возможность* — это логическая группа API-интерфейсов, предоставляющих схожие функции (группировка проводится посредством пространства имен). Представляйте себе Microsoft Teams, Outlook и Office как узлы, где размещается ваше приложение. Узел поддерживает данную возможность, если он поддерживает все API, определенные в этой возможности. Узел не может реализовать возможность частично. Возможности могут быть основаны на функциях или содержимом, например, *диалог* или *проверка подлинности*. Существуют также возможности для типов приложений, таких как *страницы* и другие группы.

В TeamsJS SDK начиная с версии 2.0 API-интерфейсы определяются как функции в пространстве имен JavaScript, имя которых соответствует нужной возможности. Если приложение работает на узле, поддерживающем возможность *диалога*, оно может безопасно вызывать такие API, как `dialog.open` (в дополнение к другим определенным в пространстве имен API-интерфейсам, связанным с диалогом). Если приложение попытается вызвать API, который не поддерживается этим узлом, API создает исключение. Проверить, поддерживает ли узел, на котором выполняется приложение, конкретную возможность, вызовите функцию [isSupported()](#differentiate-your-app-experience) ее пространства имен.

#### <a name="differentiate-your-app-experience"></a>Сделайте свой опыт работы с приложением особенным

Вы можете проверить поддержку узлом данной возможности во время выполнения, вызвав функцию `isSupported()` для этой возможности (пространства имен). Она вернет `true`, если возможность поддерживается и `false` если нет, и в этом случае вы можете изменить поведение приложения соответствующим образом. Это позволяет приложению освещать пользовательский интерфейс и функциональность на узлах, которые его поддерживают, продолжая работать на узлах, которые этого не делают.

Имя узла, на котором работает ваше приложение, отображается как свойство *hostName* в интерфейсе Context (`app.Context.app.host.name`), которое можно запросить во время выполнения, вызвав `getContext`. Оно также доступно в качестве `{hostName}` [значения заполнителя URL](./access-teams-context.md#get-context-by-inserting-url-placeholder-values). Лучшей практикой является экономное использование механизма *hostName*:

* **Don't** assume certain functionality is or isn't available in a host based on the *hostName* property value. Instead, check for capability support (`isSupported`).
* **Не** используйте *hostName* для блокировки вызовов API. Вместо этого проверьте наличие поддержки возможностей (`isSupported`).
* **Используйте** *hostName*, чтобы отличать тему вашего приложения в зависимости от узла, на котором оно работает. Например, вы можете использовать фиолетовый цвет Microsoft Teams в качестве основного цвета акцента при работе в Teams и синий цвет Outlook при работе в Outlook.
* **Используйте** *hostName*, чтобы различать сообщения, отображаемые пользователю, в зависимости от того, на каком хосте он работает. Например, покажите *Управление задачами в Office* при работе в Office в Интернете и *Управление задачами в Teams* при работе в Teams.

#### <a name="namespaces"></a>Пространства имен

Начиная с TeamsJS версии 2.0 API организованы в *возможности* с помощью пространств имен. Несколько новых пространств имен, имеющих особое значение, — *приложение*, *страницы*, *диалог*, и *teamsCore*.

##### <a name="app-namespace"></a>*приложение* пространство имен

Пространство имен `app` содержит API верхнего уровня, необходимые для общего использования приложений в Teams, Office и Outlook. Начиная с TeamsJS версии 2.0 все API-интерфейсы из других пространств имен TeamsJS были перемещены в пространство имен `app`:

| Исходное пространство имен `global (window)` | Новое пространство имен `app` |
| - | - |
| `executeDeepLink` | `app.openLink` (переименовано) |
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

##### <a name="pages-namespace"></a>*страницы* пространства имен

Пространство имен `pages` содержит функциональность для запуска веб-страниц и навигации по ним в различных узлах Microsoft 365, в том числе Teams, Office и Outlook Оно также включает в себя несколько вложенных возможностей, реализованных в виде подпространств имен.

| Исходное пространство имен `global (window)` | Новое пространство имен `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame` (переименовано) |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFocusEnterHandler` | `pages.registerFocusEnterHandler`
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |
| `shareDeepLink` | `pages.shareDeepLink` |

| Исходное пространство имен `settings` | Новое пространство имен `pages`  |
| - | - |
| `settings.getSettings` | `pages.getConfig` (переименовано)

###### <a name="pagestabs"></a>*pages.tabs*

| Исходное пространство имен `global (window)` | Новое пространство имен `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |

| Исходное пространство имен `navigation` | Новое пространство имен `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

###### <a name="pagesconfig"></a>*pages.config*

| Исходное пространство имен `settings` | Новое пространство имен `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig` (переименовано)
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
| `registerChangeConfigHandler` | `pages.config.registerChangeConfigHandler` (переименовано)

###### <a name="pagesbackstack"></a>*pages.backStack*

| Исходное пространство имен `navigation` | Новое пространство имен `pages.backStack`  |
| - | - |
| `navigation.navigateBack` | `pages.backStack.navigateBack`

| Исходное пространство имен `global (window)` | Новое пространство имен `pages.backStack`  |
| - | - |
| `registerBackButtonHandler` | `pages.backStack.registerBackButtonHandler`

###### <a name="pagesappbutton"></a>*pages.appButton*

| Исходное пространство имен `global (window)` | Новое пространство имен `pages.appButton`  |
| - | - |
| `registerAppButtonClickHandler` | `pages.appButton.onClick` (переименовано)
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter` (переименовано)
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave` (переименовано)
| интерфейс `FrameContext`. | `pages.appButton.FrameInfo` (переименовано) |

##### <a name="dialog-namespace"></a>*диалог* пространства имен

Пространство имен *задачи* TeamsJS было переименовано в *диалог*, а следующие API были переименованы:

| Исходное пространство имен `tasks` | Новое пространство имен `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (переименовано) |
| `tasks.submitTasks` | `dialog.submit` (переименовано) |
| `tasks.updateTasks` | `dialog.update.resize` (переименовано) |
| перечисление `tasks.TaskModuleDimension` | `dialog.DialogDimension` (переименовано) |
| интерфейс `tasks.TaskInfo` | `dialog.DialogInfo` (переименовано) |

Кроме того, эта возможность была разделена на основную возможность (`dialog`) для поддержки диалогов на основе HTML и вложенную возможность для диалогов на основе ботов. `dialog.bot`

##### <a name="teamscore-namespace"></a>*teamsCore* пространство имен

Чтобы обобщить TeamsJS SDK для запуска других узлов Microsoft 365, таких как Office и Outlook, функции Teams (первоначально в *глобальном* пространстве имен) были перемещены в пространство имен *teamsCore*:

| Исходное пространство имен `global (window)` | Новое пространство имен `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`

#### <a name="updates-to-the-context-interface"></a>Обновления интерфейса *Контекста*

Интерфейс `Context` был перемещен в пространство имен `app` и обновлен, чтобы сгруппировать схожие свойства для лучшей масштабируемости, поскольку он работает в Outlook и Office, а также в Teams.

Добавлено новое свойство `app.Context.app.host.name`, позволяющее вкладкам реализовать различное взаимодействие с пользователем в зависимости от узла, в котором размещено приложение.

Изменения наглядно представлены в функции `transformLegacyContextToAppContext` в исходном коде [TeamsJS SDK v2.0](https://github.com/OfficeDev/microsoft-teams-library-js/blob/main/packages/teams-js/src/public/app.ts) (файл *app.ts*).

| Исходное имя в интерфейсе `Context` | Новое местоположение в `app.Context` |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *НЕ В TeamsJS версии 2.0* |
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
| Н/Д | `app.Context.app.host.name`|

## <a name="updating-to-the-teams-client-sdk-v200"></a>Обновление до SDK клиента Teams версии 2.0.0

Самый простой способ обновить приложение Teams для совместимости с TeamsJS SDK версии 2.0 — использовать [Расширение Teams Toolkit](https://aka.ms/teams-toolkit) для Visual Studio Code. Этот раздел поможет вам сделать это пошагово. Если вы предпочитаете обновлять свой код вручную, см. разделы [Обратные вызовы, преобразованные в Promise](#callbacks-converted-to-promises), и [API, организованные в разделы возможностей](#apis-organized-into-capabilities), чтобы получить дополнительные сведения о необходимых изменениях API.

### <a name="1-install-the-latest-teams-toolkit-visual-studio-code-extension"></a>1. Установите последнее расширение Teams Toolkit Visual Studio Code.

В *Visual Studio Code Extensions Marketplace*, найдите **Teams Toolkit** и установите версию `2.10.0` или более позднюю.

### <a name="2-update-sdk-references"></a>2. Обновление ссылок на SDK

Для работы в Outlook и Office ваше приложение должно ссылаться на [пакет npm](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0) `@microsoft/teams-js@2.0.0` (или более поздней версии). Для запуска в Outlook и Office ваше приложение должно быть зависимым. Чтобы выполнить эти действия вручную и получить дополнительные сведения об изменениях API, см. следующие разделы, посвященные [обратным вызовам, преобразованным в promise](#callbacks-converted-to-promises), и [API, организованным в возможности](#apis-organized-into-capabilities).

1. Убедитесь, что у вас есть [Teams Toolkit](https://aka.ms/teams-toolkit) `v.2.10.0` или более поздний.
1. Откройте *Палитру команд*: `Ctrl+Shift+P`
1. Выполните команду `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

После завершения утилита обновит файл `package.json`, внеся зависимость от TeamsJS SDK версии не ниже 2.0 (`@microsoft/teams-js@2.0.0` или более поздней версии), а файлы `*.js/.ts` и `*.jsx/.tsx` будут обновлены следующим образом:

> [!div class="checklist"]
>
> * Ссылки в `package.json` будут изменены для совместимости с TeamsJS версии 2.0
> * Инструкции импорта будут изменены для совместимости с TeamsJS версии 2.0
> * [Вызовы функций, перечислений и интерфейсов](#apis-organized-into-capabilities) будут изменены для совместимости с TeamsJS версии 2.0
> * `TODO` напоминания о комментариях для просмотра областей, на которые могут повлиять изменения интерфейса [Контекста](#updates-to-the-context-interface)
> * Напоминания в комментариях `TODO` о том, что [ следует преобразовать функции обратного вызова в обещания](#callbacks-converted-to-promises)

> [!IMPORTANT]
> Код в HTML-файлах не поддерживается инструментами обновления и требует внесения изменений вручную.

### <a name="3-update-the-manifest-optional"></a>3. Обновление манифеста (необязательно)

Если вы добавляете в приложение Teams возможность запуска в Office и Outlook, нужно также обновить манифест приложения до версии не ниже 1.13. Это легко сделать с помощью Teams Toolkit или вручную.

# <a name="teams-toolkit"></a>[Набор средств Teams](#tab/manifest-teams-toolkit)

1. Откройте *Палитру команд*: `Ctrl+Shift+P`
1. Run **Teams: Upgrade Teams manifest to support Outlook and Office apps** command and select your app manifest file. Changes will be made in place.

# <a name="manual-steps"></a>[Выполнение вручную](#tab/manifest-manual)

Откройте манифест приложения Teams и обновите `$schema` и `manifestVersion` со следующими значениями:

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

Если вы использовали Teams Toolkit для создания личного приложения, вы также можете использовать его для проверки изменений в файле манифеста и выявления ошибок. Откройте палитру команд `Ctrl+Shift+P` и найдите **Teams: проверьте файл манифеста** или выберите параметр в меню ''Развертывание'' набора инструментов Teams (найдите значок Teams в левой части кода Visual Studio).

:::image type="content" source="../../m365-apps/images/toolkit-validate-manifest-file.png" alt-text="Параметр Teams Toolkit &quot;Проверить файл манифеста&quot; в меню &quot;Развертывание&quot;":::

## <a name="next-steps"></a>Дальнейшие действия

* Используйте [документацию по TeamsJS](/javascript/api/overview/msteams-client) чтобы начать работу с клиентским пакетом SDK Microsoft Teams JavaScript.
* Просмотрите [журнал изменений](https://github.com/OfficeDev/microsoft-teams-library-js/blob/main/packages/teams-js/CHANGELOG.md), чтобы узнать о последних обновлениях TeamsJS.
