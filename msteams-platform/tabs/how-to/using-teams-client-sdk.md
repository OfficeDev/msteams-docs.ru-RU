---
title: Создание вкладок и других услуг с помощью клиентского SDK JavaScript
author: heath-hamilton
ms.author: surbhigupta
description: Обзор клиентского SDK JavaScript для Microsoft Teams, который поможет вам создавать приложения Teams в <iframe>.
keywords: Teams tabs group channel configurable static SDK JavaScript personal
ms.topic: conceptual
ms.openlocfilehash: 7ba900990507e2d32992d6d2c26fff07d7c84bd8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/28/2021
ms.locfileid: "50036999"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Создание вкладок и других услуг с помощью клиентского SDK JavaScript для Microsoft Teams

Клиентский SDK JavaScript для Microsoft Teams поможет вам создать в Teams возможности, которые будут отображать содержимое приложения в iframe.

SDK полезен для разработки приложений с помощью любой из следующих возможностей Teams:

* [Вкладки](../../tabs/what-are-tabs.md)
* [Модули задач](../../task-modules-and-cards/what-are-task-modules.md)

Например, SDK позволяет вкладке реагировать на изменения тем, которые пользователи внести в клиенте Teams. [](../../build-your-first-app/build-personal-tab.md#3-update-the-tab-theme)

## <a name="getting-started"></a>Начало работы

В зависимости от настроек разработки сделайте одно из следующих:

* [Установка SDK с помощью npm или Yarn](https://docs.microsoft.com/javascript/api/overview/msteams-client?view=msteams-client-js-latest)
* [Клонирование SDK (GitHub)](https://github.com/OfficeDev/microsoft-teams-library-js)

## <a name="common-sdk-functions"></a>Общие функции SDK

В следующих таблицах приводится понимание часто используемых функций SDK. Справочная [документация по SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest) предоставляет более подробную информацию.

### <a name="basic-functions"></a>Основные функции

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | Инициализирует SDK. Эта функция должна быть вызвана перед любыми другими вызовами SDK.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| Получает текущее состояние, в котором запущена страница. При вызове извлекется объект **Context.**|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-&preserve-view=true)<br/>[context obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Инициализирует библиотеку Teams и [](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) задает контекст кадра вкладки в зависимости от contentUrl и websiteUrl. Это гарантирует, что функция "перезагрузить веб-сайт" будет работать с правильным URL-адресом.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | Задает контекст кадра [вкладки](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) в зависимости от contentUrl и websiteUrl. Это гарантирует, что функция "перезагрузить веб-сайт" будет работать с правильным URL-адресом.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |Обработец, регистрируется, когда пользователь перегнобит полноэкранное или оконное представление вкладки.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-&preserve-view=true)<br/>[boolean](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerFullScreenHandler__isFullScreen__boolean_____void_&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |Обработтель, зарегистрированный при нажатии  пользователем включенной кнопки "Параметры" для перенастройки вкладки.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Получает вкладки, которые принадлежат приложению. При вызове извлекется **объект TabInformation.** Объект **TabInstanceParameters** является необязательным параметром.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Получает последние использованные вкладки для пользователя. При вызове извлекется **объект TabInformation.** Объект **TabInstanceParameters** является необязательным параметром.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Принимает объект **DeepLinkParameters** в качестве входных данных и использует диалоговое окно с глубокой ссылкой, которое пользователь может использовать для навигации к содержимому *на вкладке.*|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-&preserve-view=true)<br/>[deepLink obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|Принимает требуемую **deepLink** в качестве входных данных и переходит по URL-адресу или запускает действие клиента ( например, открытие или установка) приложения *в Teams.*|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|Принимает объект **TabInstance** в качестве входных данных и переходит к указанному экземпляру вкладки.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-&preserve-view=true)<br/>[tabInstance obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>Пространство имен проверки подлинности

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Инициирует запрос проверки подлинности, который открывает новое окно с параметрами, предоставленными вызываемой. Необязательные входные значения определяются объектом **AuthenticateParameters.**|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Сообщает кадру, который инициировал запрос проверки подлинности, о том, что запрос был успешным, и закрывает окно проверки подлинности|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Сообщает кадру, который инициировал запрос проверки подлинности, о сбойе запроса и закрывает окно проверки подлинности.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|

### <a name="settings-namespace"></a>Пространство имен "Параметры"

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|Исходное значение — false. Активирует **кнопку "Сохранить"** или **"Удалить",** если имеется действительное состояние.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Получает параметры для текущего экземпляра. При вызове извлекется объект **Settings.**|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|Настраивает параметры для текущего экземпляра. Допустимые параметры определяются объектом **Settings.**|[function](/https://docs.microsoft.com/en-us/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Обработок, зарегистрированный при нажатии пользователем кнопки **"Сохранить".** Этот обработок следует использовать для создания или обновления ресурса, используемой для содержимого.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|Обработок, зарегистрированный при нажатии пользователем кнопки **"Удалить".** Этот обработок следует использовать для удаления ресурса, который используется для питания контента.|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>Пространство имен модулей задач

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Принимает объект **TaskInfo** в качестве входных данных и позволяет приложению открыть модуль задачи. **Необязательный submitHandler** регистрируется после завершения работы модуля задачи. |[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Отправка модуля задачи. **Необязательный параметр** строки результата — это результат, который отправляется боту или приложению и обычно является объектом JSON или сериализацией; Необязательный параметр **строки appIds** или массива строк помогает в проверке того, что вызов исходит из того же appId, что и тот, который вызывает модуль задачи.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)|
