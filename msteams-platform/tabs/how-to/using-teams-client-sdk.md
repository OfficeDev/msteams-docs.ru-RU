---
title: Создание вкладок и других размещенных опытов с клиентом JavaScript SDK
author: heath-hamilton
ms.author: surbhigupta
description: Обзор Microsoft Teams JavaScript SDK, который может помочь вам создать Teams приложения, размещенные в <iframe>.
localization_priority: Normal
keywords: команды вкладок групповой канал настраиваемый статический SDK JavaScript личные
ms.topic: conceptual
ms.openlocfilehash: d3dfadda7f2a56e32ecf8e5b67df3b9831c52739
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566658"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Создание вкладок и других размещенных опытов с Microsoft Teams JavaScript SDK

Данный Microsoft Teams JavaScript SDK может помочь вам создать размещенный опыт в Teams, что означает отображение содержимого приложения в iframe.

SDK полезен для разработки приложений с любой из следующих Teams возможностей:

* [Вкладки](../../tabs/what-are-tabs.md)
* [Модули задач](../../task-modules-and-cards/what-are-task-modules.md)

Например, SDK может заставить вашу [вкладку реагировать на изменения темы,](../../build-your-first-app/build-personal-tab.md) внесенные пользователями в Teams клиента.

## <a name="getting-started"></a>Начало работы

Сделайте одно из следующих в зависимости от ваших предпочтений в области развития:

* [Установка SDK с npm или пряжи](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)

## <a name="common-sdk-functions"></a>Общие функции SDK

Смотрите следующие таблицы, чтобы понять часто используемые функции SDK. Справочная [документация SDK содержит](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) более полную информацию:


### <a name="basic-functions"></a>Основные функции

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | Инициализирует SDK. Эта функция должна быть вызвана перед любыми другими вызовами SDK.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| Получает текущее состояние, в котором работает страница. Обратный вызов извлекает **объект Контекста.**|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-&preserve-view=true)<br/>[контекст obj](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Инициализирует Teams и устанавливает контекст кадра [вкладки в зависимости](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) от contentUrl и websiteUrl. Это гарантирует, что функция перезагрузки или перезагрузки работает по правильному URL-адресу.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | Устанавливает контекст кадра [вкладки в зависимости](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) от contentUrl и веб-сайтаUrl. Это гарантирует, что функция перезагрузки или перезагрузки работает по правильному URL-адресу.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |Обработчик, зарегистрированный при просмотре полноэкранным или оконным экраном вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-&preserve-view=true)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerFullScreenHandler__isFullScreen__boolean_____void_&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |Обработчик, зарегистрированный при выборе пользователем включенной кнопки **Параметры** для перенастройки вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Получает вкладки, принадлежащие приложению. Обратный вызов получает объект **TabInformation.** Объект **TabInstanceParameters является** необязательным параметром.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Получает самые последние используемые вкладки для пользователя. Обратный вызов получает объект **TabInformation.** Объект **TabInstanceParameters является** необязательным параметром.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Принимает объект **DeepLinkParameters в качестве** ввода и разделяет глубокую ссылку диалоговое окно, которое пользователь может использовать для навигации по *содержимому в вкладке*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-&preserve-view=true)<br/>[deepLink obj](/javascript/api/@microsoft/teams-js/deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|Принимает необходимый **deepLink** в качестве ввода и перемещает пользователя на URL или запускает действия клиента, такие как открытие или установка приложения в *течение Teams*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|Принимает объект **TabInstance в** качестве ввода и переходит в указанный экземпляр вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>Пространство имен аутентификации

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Инициирует запрос на аутентификацию, который открывает новое окно с параметрами, предоставленными абонентом. Дополнительные значения ввода определяются **объектом AuthenticateParameters.**|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[Аут Obj](/javascript/api/@microsoft/teams-js/authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Уведомляет кадр, инициировав запрос на проверку подлинности, о том, что запрос был успешным, и закрывает окно проверки подлинности|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Уведомляет кадр, инициировав запрос на проверку подлинности, о том, что запрос не удалось, и закрывает окно проверки подлинности.|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|

### <a name="settings-namespace"></a>Параметры имен

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|Начальное значение является ложным. Активирует кнопку **«Сохранить** **или** удалить», когда состояние действия верно.|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Получает настройки для текущего экземпляра. Обратный вызов получает **Параметры** объекта.|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[настройки obj](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|Настраивает настройки для текущего экземпляра. Действительные настройки определяются Параметры **объектом.**|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[настройки obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Обработчик, зарегистрированный при выборе пользователем кнопки **Сохранения.** Этот обработчик должен использоваться для создания или обновления базового ресурса, подемеющих содержимому.|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|Обработчик, зарегистрированный при выборе пользователем **кнопки «Удалить».** Этот обработчик должен использоваться для удаления базового ресурса, подемеющих содержимому.|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>Целевые модули именоваемое пространство

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Принимает объект **TaskInfo** в качестве ввода и позволяет приложению открыть модуль задачи. **Необязательная отправкаHandler** регистрируется при выполнения модуля задачи. |[function](/javascript/api/@microsoft/teams-js/tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[задачаИнфо obj](/javascript/api/@microsoft/teams-js/taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Отправляет модуль задачи. Параметр строки **факультативного** результата — это результат, отправленный боту или приложению, и, как правило, является объектом JSON или сериализацией; Дополнительный параметр **строки или строки appIds** помогает проверить, что вызов возник из того же appId, что и тот, который вызвал модуль задачи.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)|
