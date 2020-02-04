---
title: Использование пакета SDK клиента Teams
author: laujan
description: Использование пакета SDK клиента Teams для добавления функциональных возможностей, поддерживающих Teams, на пользовательские вкладки
keywords: вкладки Teams канал группы настраиваемый статический пакет SDK JavaScript персональный
ms.topic: conceptual
ms.openlocfilehash: eac5a8ec03ba12d926346afb40ca9bc6e9dda8d6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675647"
---
# <a name="using-the-teams-client-sdk"></a>Использование пакета SDK клиента Teams

**Клиентский пакет SDK Teams для JavaScript** и **Библиотека JavaScript** для Teams являются частью [платформы разработчика Microsoft Teams](https://msdn.microsoft.com/microsoft-teams) и предоставляют средства и процессы для упрощения создания приложений Teams. Клиентский пакет SDK для Teams распространяется в виде пакета NPM. Последнюю версию можно найти здесь: <https://www.npmjs.com/package/@microsoft/teams-js>. Библиотека Teams расположена по адресу <https://github.com/OfficeDev/microsoft-teams-library-js>.

В следующей таблице приведены функции библиотеки Teams, которые обычно используются при разработке вкладок:

## <a name="teams-sdk-public-api"></a>Общедоступный API Teams SDK 

| Функция  | Описание          | Документация|
| -----     | -----     | -----    | -----        |
| `microsoftTeams.initialize()` | Инициализирует библиотеку Teams. Эту функцию необходимо вызвать перед любыми вызовами SDK.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-)|
|`microsoftTeams.getContext(callback: (context: Context)`| Получает текущее состояние, в котором выполняется страница. Обратный вызов извлекает объект **context** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-)<br/>[obj-obj](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |Обработчик, который регистрируется, когда пользователь переключает полноэкранное и оконное представление вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest#isfullscreen)|
|`microsoftTeams.registerChangeSettingsHandler()` |Обработчик, который регистрируется, когда пользователь нажимает кнопку Enabled Settings (включить **Параметры** ), чтобы изменить конфигурацию вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Получает вкладки, принадлежащие приложению. Обратный вызов получает объект **табинформатион** . Объект **табинстанцепараметерс** является необязательным параметром.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[Табинфо obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Получает последние использовавшиеся вкладки для пользователя. Обратный вызов получает объект **табинформатион** . Объект **табинстанцепараметерс** является необязательным параметром.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[Табинфо obj](/javascript/api/@microsoft/teams-js/microsoftteams.teaminformation?view=msteams-client-js-latest)<br/>[Табинстанце obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Принимает объект **диплинкпараметерс** в качестве входных данных и предоставляет доступ к диалоговому окну глубокой ссылки, которое пользователь может использовать для перехода к содержимому на *вкладке*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-)<br/>[obj для прямой ссылки](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|Принимает необходимый **прямой** URL-адрес в качестве входных данных и переходит к URL-адресу или запускает действие клиента, например, открытие или установку — приложение *в Teams*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|Получает объект **табинстанце** в качестве входных данных и переходит к указанному экземпляру вкладки.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-)<br/>[Табинстанце obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest)|

## <a name="authentication-namespace"></a>Пространство имен для проверки подлинности

| Функция  | Описание          | Документация|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Инициирует запрос проверки подлинности, который открывает новое окно с параметрами, предоставленными вызывающим абонентом. Необязательные входные значения определяются объектом **аусентикатепараметерс** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#authenticate-authenticateparameters-)<br/>[obj (проверка подлинности)](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Уведомляет кадр, который инициировал запрос на проверку подлинности, который был успешным, и закрывает окно проверки подлинности|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifysuccess-string--string-)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Уведомляет кадр, который инициировал запрос проверки подлинности, который не удалось выполнить в запросе, и закрывает окно проверки подлинности.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifyfailure-string--string-)|

## <a name="settings-namespace"></a>Пространство имен параметров

| Функция  | Описание          | Документация|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|Начальное значение — false. Активирует кнопку **сохранить** или **Удалить** , если допустимое состояние имеет значение true.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setvaliditystate-boolean-)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Получает параметры для текущего экземпляра. Обратный вызов получает объект **Settings** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#getsettings--instancesettings--settings-----void-)<br/>[obj Settings](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|Настраивает параметры для текущего экземпляра. Допустимые параметры определяются объектом **Settings** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setsettings-settings-)<br/>[obj Settings](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Обработчик, который регистрируется, когда пользователь нажимает кнопку **сохранить** . Этот обработчик следует использовать для создания или обновления базовой информации о ресурсе, потребляемом содержимым.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronsavehandler--evt--saveevent-----void-)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|Обработчик, который регистрируется, когда пользователь нажимает кнопку **Remove (удалить** ). Этот обработчик следует использовать для удаления базового ресурса, который переключается в контент.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronremovehandler--evt--removeevent-----void-)|

## <a name="tasks-namespace"></a>Пространство имен Tasks

| Функция  | Описание          | Документация|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Принимает объект **таскинфо** в качестве входных данных и позволяет приложению открыть модуль задачи. Необязательный **субмисандлер** регистрируется при завершении модуля задач. |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#starttask-taskinfo---err--string--result--string-----void-)<br/>[Таскинфо obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Отправит модуль задачи. Необязательный параметр строки **результата** — это результат, отправляемый в Bot или приложение, который обычно является объектом JSON или сериализацией. Необязательные параметры String или **String String помогают** выполнить проверку того, что вызов поступил из того же AppID, что и вызвавший модуль задачи.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---)|