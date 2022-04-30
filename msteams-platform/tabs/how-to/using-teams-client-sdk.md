---
title: Создание вкладок и других размещенных функций с помощью клиентского пакета SDK для JavaScript
author: heath-hamilton
ms.author: surbhigupta
description: Обзор клиентского пакета SDK Microsoft Teams для JavaScript, который поможет в создании возможностей приложения Teams, размещенных в <iframe>. Он включает основные функции, пространство имен проверки подлинности и пространство имен параметров.
ms.localizationpriority: high
keywords: teams вкладки группа канал настраиваемый статический пакет SDK JavaScript личный
ms.topic: conceptual
ms.openlocfilehash: f4204555e57c270ad03a7a01d5b231d63b72296a
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111894"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Создание вкладок и других размещенных функций с помощью клиентского пакета SDK Microsoft Teams для JavaScript

Клиентский пакет SDK Microsoft Teams для JavaScript может помочь в создании размещенных функций в Teams, что означает отображение содержимого приложения в iframe.

Пакет SDK полезен для разработки приложений с любой из следующих возможностей Teams:

* [Вкладки](../../tabs/what-are-tabs.md)
* [Модули задач](../../task-modules-and-cards/what-are-task-modules.md)

Например, SDK может заставить вашу [вкладку реагировать на изменения темы](../../build-your-first-app/build-personal-tab.md#3-update-your-tab-theme), которые пользователи вносят в клиент Teams.

## <a name="getting-started"></a>Начало работы

Выполните одно из следующих действий в зависимости от ваших предпочтений:

* [Установка пакета SDK с помощью npm или Yarn](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* [Клонирование пакета SDK (GitHub)](https://github.com/OfficeDev/microsoft-teams-library-js)

## <a name="common-sdk-functions"></a>Распространенные функции пакета SDK

В следующих таблицах описаны часто используемые функции пакета SDK. [Справочная документация по пакету SDK](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) содержит более подробные сведения.

### <a name="basic-functions"></a>Основные функции

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | Инициализирует пакет SDK. Эта функция должна вызываться перед любыми другими вызовами пакетами SDK.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initialize&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| Получает текущее состояние, в котором запущена страница. Обратный вызов извлекает объект **Context**.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)<br/>[Объект context](/javascript/api/@microsoft/teams-js/@microsoft.teams-js?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Инициализирует библиотеку Teams и задает [контекст фрейма](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) вкладки в зависимости от ContentUrl и WebsiteUrl. Это гарантирует, что функция перехода на веб-сайт или функция перезагрузки работает с правильным URL-адресом.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initializewithframecontext&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | Задает [контекст фрейма](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) вкладки в зависимости от contentUrl и websiteUrl. Это гарантирует, что функция перехода на веб-сайт или функция перезагрузки работает с правильным URL-адресом.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-setframecontext&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: Boolean)` |Обработчик, который регистрируется, когда пользователь переключает полноэкранное или оконное представление вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)<br/>[Логический](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |Обработчик, который регистрируется, когда пользователь выбирает включенную кнопку **Параметры** для перенастройки вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Получает вкладки, принадлежащие приложению. Обратный вызов извлекает объект **TabInformation**. Объект **TabInstanceParameters** является необязательным параметром.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-gettabinstances&preserve-view=true)<br/>[Объект tabInfo](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Получает последние использованные вкладки для пользователя. Обратный вызов извлекает объект **TabInformation**. Объект **TabInstanceParameters** является необязательным параметром.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-getmrutabinstances&preserve-view=true)<br/>[Объект tabInfo](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[Объект tabInstance](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Принимает объект **DeepLinkParameters** в качестве входных данных и совместно использует диалоговое окно с прямыми ссылками, которое пользователь может использовать для перехода к содержимому *на вкладке*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-sharedeeplink&preserve-view=true)<br/>[Объект deepLink](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: Boolean, reason?: string))`|Принимает требуемую **deepLink** в качестве входных данных и направляет пользователя по URL-адресу или инициирует действие клиента, например открытие или установку приложения *в Teams*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-executedeeplink&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: Boolean, reason?: string))`|Принимает объект **TabInstance** в качестве входных данных и переходит к указанному экземпляру вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-navigatetotab&preserve-view=true)<br/>[Объект tabInstance](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>Пространство имен проверки подлинности

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Инициирует запрос проверки подлинности, который открывает новое окно с параметрами, предоставленными вызывающей стороной. Необязательные входные значения определяются объектом **AuthenticateParameters**.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[Объект auth](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Уведомляет фрейм, инициировавший запрос проверки подлинности, об успешном выполнении запроса и закрывает окно проверки подлинности|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Уведомляет фрейм, инициировавший запрос проверки подлинности, о том, что запрос не выполнен, и закрывает окно проверки подлинности.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.getAuthToken(authTokenRequest: AuthTokenRequest)`|Отправьте запрос на выпуск маркера Azure AD от имени приложения. Маркер можно получить из кэша, если срок его действия не истек. В противном случае в Azure AD отправляется запрос на получение нового маркера.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true)|

### <a name="settings-namespace"></a>Пространство имен параметров

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: Boolean)`|Начальное значение — false. Активирует кнопку **Сохранить** или **Удалить**, если состояние допустимости истинно.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Получает параметры для текущего экземпляра. Обратный вызов извлекает объект **Settings**.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[объект settings](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: Boolean, reason?: string)`|Настраивает параметры для текущего экземпляра. Допустимые параметры определяются объектом **Settings**.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[объект settings](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Обработчик, который регистрируется, когда пользователь нажимает кнопку **Сохранить**. Этот обработчик следует использовать для создания или обновления базового ресурса, поддерживающего содержимое.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|Обработчик, который регистрируется, когда пользователь нажимает кнопку **Удалить**. Этот обработчик следует использовать для удаления базового ресурса, поддерживающего содержимое.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>Пространство имен модулей задач

| Функция  | Описание          | Документация|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Принимает объект **TaskInfo** в качестве входных данных и позволяет приложению открыть модуль задачи. Необязательный **submitHandler** регистрируется после завершения работы модуля задачи. |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[объект taskInfo](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Отправляет модуль задачи. Необязательный параметр строки **result** — это результат, отправленный боту или приложению, и обычно он представляет собой объект JSON или сериализацию. Необязательный параметр строки **appIds** или массив строк помогает проверить, что вызов исходит из того же appId, что и тот, который вызвал модуль задачи.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-tasks-submittask&preserve-view=true)|
