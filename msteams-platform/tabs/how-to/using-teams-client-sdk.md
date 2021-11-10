---
title: Создание вкладок и других опытом работы с клиентом JavaScript SDK
author: heath-hamilton
ms.author: surbhigupta
description: Обзор SDK Microsoft Teams JavaScript, который может помочь вам создать Teams приложений в <iframe>. Он включает основные функции, пространство имен проверки подлинности и параметры пространства имен.
ms.localizationpriority: medium
keywords: teams tabs group channel configurable static SDK JavaScript personal
ms.topic: conceptual
ms.openlocfilehash: 5c4a42e78a234616a0b88ef241c63b98fb7a0265
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887548"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Создание вкладок и других опытом работы с клиентом Microsoft Teams JavaScript SDK

SDK Microsoft Teams JavaScript поможет вам создать у себя в Teams, что означает отображение контента приложения в iframe.

SDK полезен для разработки приложений с любым из следующих Teams возможностей:

* [Вкладки](../../tabs/what-are-tabs.md)
* [Модули задач](../../task-modules-and-cards/what-are-task-modules.md)

Например, SDK может заставить [](../../build-your-first-app/build-personal-tab.md#3-update-your-tab-theme) вкладку реагировать на изменения темы, внесенные пользователями в Teams клиенте.

## <a name="getting-started"></a>Начало работы

Сделайте одно из следующих личных предпочтений:

* [Установка SDK с npm или yarn](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* [Клонировать SDK (GitHub)](https://github.com/OfficeDev/microsoft-teams-library-js)

## <a name="common-sdk-functions"></a>Общие функции SDK

См. в следующих таблицах, чтобы понять часто используемые функции SDK. Справочная [документация SDK предоставляет](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) более полную информацию.

### <a name="basic-functions"></a>Основные функции

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | Инициализирует SDK. Эта функция должна быть вызвана перед другими вызовами SDK.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| Получает текущее состояние, в котором запущена страница. Возвращение вызовов извлекает **объект Context.**|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-&preserve-view=true)<br/>[обдж контекста](/javascript/api/@microsoft/teams-js/@microsoft.teams-js?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Инициализирует Teams библиотеку и задает контекст [](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) кадра вкладки в зависимости от contentUrl и websiteUrl. Это гарантирует, что функции перезагрузки и перезагрузки будут работать по правильному URL-адресу.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | Задает контекст кадра [вкладки в](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) зависимости от contentUrl и websiteUrl. Это гарантирует, что функции перезагрузки и перезагрузки будут работать по правильному URL-адресу.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |Обработник, зарегистрированный при перегевке полноэкранного/оконного представления вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-&preserve-view=true)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerFullScreenHandler__isFullScreen__boolean_____void_&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |Обработник, зарегистрированный при выборе включенной  кнопки Параметры для перенастройки вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Получает вкладки, которые принадлежат приложению. Возвращение вызовов извлекает **объект TabInformation.** Объект **TabInstanceParameters** является необязательным параметром.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Получает самые недавно используемые вкладки для пользователя. Возвращение вызовов извлекает **объект TabInformation.** Объект **TabInstanceParameters** является необязательным параметром.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Принимает объект **DeepLinkParameters** в качестве ввода и разделяет диалоговое окно глубокой ссылки, которое пользователь может использовать для навигации по содержимому *в вкладке.*|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-&preserve-view=true)<br/>[deepLink obj](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|Принимает необходимый **deepLink** в качестве ввода и перемещает пользователя на URL-адрес или запускает клиентские действия, такие как открытие или установка приложения в *Teams.*|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|Принимает объект **TabInstance в** качестве ввода и перемещается в указанный экземпляр вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>Пространство имен проверки подлинности

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Инициирует запрос на проверку подлинности, который открывает новое окно с параметрами, предоставляемыми вызываемой. Необязательные значения ввода определяются объектом **AuthenticateParameters.**|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[Auth obj](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Сообщает кадру, который инициировал запрос проверки подлинности, что запрос был успешным, и закрывает окно проверки подлинности|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Сообщает кадру, который инициировал запрос на проверку подлинности, о сбойе запроса и закрывает окно проверки подлинности.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.getAuthToken(authTokenRequest: AuthTokenRequest)`|Отправьте запрос на выпуск маркера Azure AD от имени приложения. Маркер можно приобрести из кэша, если срок его действия не истек. В противном случае запрос отправляется в Azure AD для получения нового маркера.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#getAuthToken_AuthTokenRequest_&preserve-view=true)|

### <a name="settings-namespace"></a>Параметры пространства имен

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|Исходное значение является ложным. Активирует **кнопку Сохранить** или **Удалить,** если состояние действительности верно.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Получает параметры текущего экземпляра. В вызове извлекается **Параметры** объект.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[параметры obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|Настраивает параметры текущего экземпляра. Допустимые параметры определяются объектом **Параметры.**|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[параметры obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Обработник, зарегистрированный при выборе кнопки **Сохранить.** Этот обработок следует использовать для создания или обновления ресурса, на который заправился контент.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|Обработник, зарегистрированный при выборе кнопки **Удалить.** Этот обработок следует использовать для удаления ресурса, который заправит контент.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>Пространство имен модулей задач

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Принимает объект **TaskInfo** в качестве ввода и позволяет приложению открывать модуль задач. **Необязательный submitHandler** регистрируется после завершения модуля задач. |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Представляет модуль задач. **Необязательный** параметр строки результатов — результат, отправленный боту или приложению, и обычно является объектом JSON или сериализацией; Необязательный параметр строки или массива строки **appIds** помогает в проверке того, что вызов исходил из того же приложения, что и тот, который вызывает модуль задач.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)|
