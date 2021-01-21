---
title: Примеры кода Microsoft Teams
description: Ссылки и описания примеров приложений для платформы разработчика Microsoft Teams
keywords: Примеры для разработчиков Microsoft Teams
ms.openlocfilehash: 665d3565f4f453d263fef6a17cb27f5060111468
ms.sourcegitcommit: 6d9c60cce1f2e5204e680c074ce77a8376233b59
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/20/2021
ms.locfileid: "49912318"
---
# <a name="tutorials-and-code-samples-for-the-microsoft-teams-developer-platform"></a>Учебники и примеры кода для платформы разработчиков Microsoft Teams

Здесь вы найдете список учебников и примеров кода, демонстрируя, как расширить возможности платформы разработчика Teams, создав настраиваемые приложения.

## <a name="getting-started-with-microsoft-learn"></a>Начало работы с Microsoft Learn

| Возможность| Модуль "Подробнее"|
|--------|-------------|
| Вкладки — встроенные веб-приложения  |  [Создание встроенных веб-элементов с вкладками для Microsoft Teams](https://docs.microsoft.com/learn/modules/embedded-web-experiences/) |
| Веб-перехватчики и соединительные линии  |  [Подключение веб-служб к Microsoft Teams с помощью веб-hooks и соединители Office 365](https://docs.microsoft.com/learn/modules/msteams-webhooks-connectors/) |
|Расширения для система обмена сообщениями  | [Ориентированные на задачи взаимодействия в Microsoft Teams с расширениями обмена сообщениями](https://docs.microsoft.com/learn/modules/msteams-messaging-extensions/)  |
| Модули задач |  [Сбор входных данных в Microsoft Teams с помощью модулей задач](https://docs.microsoft.com/learn/modules/msteams-task-modules/) |
| Боты для бесед  | [Создание интерактивных ботов для бесед для Microsoft Teams](https://docs.microsoft.com/learn/modules/msteams-conversation-bots/)  |

## <a name="getting-started-with-code-samples"></a>Начало работы с примерами кода

Чтобы скачать наши примеры с GitHub:

1. Выберите один из проектов, перечисленных ниже, и откройте его в GitHub.
2. Выберите **кнопку "Клонировать" или "Скачать"** и скопируйте URL-адрес
3. Откройте командную подсказку в родительском каталоге, в который нужно установить пример проекта
4. Run `git clone <pasted url>`

### <a name="for-netc-samples"></a>Для примеров .NET/C#

Каждый из наших примеров .NET содержит Visual Studio решения, который может полностью построить решение, включая восстановление пакетов NuGet.

### <a name="for-nodejs-samples"></a>Для Node.js примеров

В файле packages.jsсписок всех необходимых пакетов для примера. Просто `npm install` запустите из командной строки в Node.js проекта, чтобы установить необходимые пакеты. Теперь вы готовы открыть проект в Visual Studio Code и начать экспериментировать.

### <a name="for-other-samples"></a>Для других примеров

Как всегда, файл README проекта должен иметь дополнительные сведения о конкретных потребностях в определенных примерах.

## <a name="bots-using-the-v4-sdk"></a>Боты (с помощью V4 SDK)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

>[!TIP]
>Посетите [репозиторий](https://github.com/Microsoft/BotBuilder-Samples) примеров Bot Framework, чтобы просмотреть образцы SDK Microsoft Bot Framework v4 для C#, JavaScript, TypeScript и Python.

## <a name="messaging-extensions-using-the-v4-sdk"></a>Расширения обмена сообщениями (с помощью V4 SDK)

| Пример | Описание | .NET Core | JavaScript | Python|
|--------|------------- |---|---|----|
| Расширения для обмена сообщениями — поиск | Расширение обмена сообщениями, которое принимает поисковые запросы и возвращает результаты. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
| Расширения обмена сообщениями — действие | Расширение обмена сообщениями, которое принимает параметры и возвращает карточку. Кроме того, как получить переад вперед сообщение в качестве параметра в расширении обмена сообщениями. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Расширения для обмена сообщениями — auth и config | Расширение обмена сообщениями, которое имеет страницу конфигурации, принимает поисковые запросы и возвращает результаты после того, как пользователь войт. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) |
| Расширения обмена сообщениями — предварительный просмотр действий | В этой теме показано, как создать поток предварительного просмотра и редактирования для расширения обмена сообщениями. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/53.teams-messaging-extensions-action-preview) |
| Развернуть ссылку | Расширение обмена сообщениями, которое выполняет размевание ссылок. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/55.teams-link-unfurling) |


## <a name="outgoing-webhooks"></a>Исходяющие веб-hooks

| Пример | Описание
|--------|-------------
| [Outgoing Webhook for C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | Здесь показано, как создать исходяющий **веб-ook** для Microsoft Teams на C#/.NET.
| [Исходяющий веб-Node.js](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | Иллюстрирует создание простого исходяного **веб-ook** для Microsoft Teams в 50 строках Node.js кода.

## <a name="connectors"></a>Соединители

| Пример | Описание
|--------|-------------
| [Пример соединители для Node.js](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | В этом примере, написанном Node.js, демонстрируется создание соединителя для Microsoft Teams с помощью GitHub в качестве примера для создания уведомлений соединителя.
| [Пример соединители для C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | В этом примере, написанном на C#, демонстрируется создание соединители для Microsoft Teams с использованием примера приложения списка задач в качестве примера для создания уведомлений соединители. В этом примере также показано, как реализовать функции входа на странице конфигурации соединители. 

## <a name="graph-api"></a>Graph API

| Пример | Описание
|--------|-------------
| [Примеры API Microsoft Graph](https://github.com/OfficeDev/microsoft-teams-sample-graph) | В этих примерах показано использование вызовов API Microsoft Graph для выполнения таких задач, как запрос команд и каналов из веб-службы, запущенной за пределами Microsoft Teams.

### <a name="bot-framework-sdk-v3-samples"></a>Примеры bot Framework SDK v3

| Пример | Описание |
|--------|------------- |
| [Пример бота для C#/.NET](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Примеры Bot Framework v3|
| [Пример бота для Node.js](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Примеры Bot Framework v3 |
