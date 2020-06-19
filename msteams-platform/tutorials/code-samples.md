---
title: Примеры кода Microsoft Teams
description: Ссылки и описания примеров приложений для платформы разработчика Microsoft Teams
keywords: Примеры разработчиков Microsoft Teams
ms.openlocfilehash: 955588608fde694b163104d0a9e9e94289719003
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801488"
---
# <a name="tutorials-and-code-samples-for-the-microsoft-teams-developer-platform"></a>Учебники и примеры кода для платформы разработчика Microsoft Teams

Здесь вы найдете список учебных курсов и примеров кода, демонстрирующих способы расширения возможностей платформы для разработчиков Teams путем создания пользовательских приложений.

## <a name="getting-started-with-microsoft-learn"></a>Начало работы со сведениями о корпорации Майкрософт

| Возможность| Модуль "сведения"|
|--------|-------------|
| Вкладки — встроенные веб-интерфейсы  |  [Создание встроенных веб-приложений с помощью вкладок для Microsoft Teams](https://docs.microsoft.com/learn/modules/embedded-web-experiences/) |
| Веб-перехватчики и соединительные линии  |  [Подключение веб-служб к Microsoft Teams с помощью веб-перехватчиков и соединителей Office 365](https://docs.microsoft.com/learn/modules/msteams-webhooks-connectors/) |
|расширения для обмена сообщениями;  | [Взаимодействия с задачами в Microsoft Teams с расширениями обмена сообщениями](https://docs.microsoft.com/learn/modules/msteams-messaging-extensions/)  |
| Модули задач |  [Сбор данных в Microsoft Teams с модулями задач](https://docs.microsoft.com/learn/modules/msteams-task-modules/) |
| Беседы Боты  | [Создание интерактивных бесед боты для Microsoft Teams](https://docs.microsoft.com/learn/modules/msteams-conversation-bots/)  |

## <a name="getting-started-with-code-samples"></a>Начало работы с примерами кода

Чтобы скачать наши примеры из GitHub, выполните следующие действия.

1. Выберите один из перечисленных ниже проектов и откройте проект в GitHub.
2. Нажмите кнопку **клонировать или скачать** и скопируйте URL-адрес.
3. Откройте командную строку в родительском каталоге, в который необходимо установить пример проекта.
4. Выполняем`git clone <pasted url>`

### <a name="for-netc-samples"></a>Примеры для .NET и C#

Каждый из наших примеров .NET включает файл решения Visual Studio, с помощью которого можно полностью создать решение, включая восстановление пакетов NuGet.

### <a name="for-nodejs-samples"></a>Примеры Node.js

Мы предоставляем packages.jsфайла, в котором перечисляются все необходимые пакеты для примера. Просто запустите `npm install` из командной строки каталога проекта Node.js, чтобы установить необходимые пакеты. Теперь вы готовы открыть проект в Visual Studio Code и начать эксперимент.

### <a name="for-other-samples"></a>Для других примеров

Как всегда, файл README проекта должен содержать более подробную информацию о конкретных примерах.

## <a name="bots-using-the-v4-sdk"></a>Боты (с использованием пакета SDK v4)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

>[!TIP]
>Посетите [репозиторий образцов для ленты](https://github.com/Microsoft/BotBuilder-Samples) Office, чтобы просмотреть образцы, ориентированные на задачи Microsoft Bot Framework v4 SDK для C#, JavaScript, TypeScript и Python.

## <a name="messaging-extensions-using-the-v4-sdk"></a>Расширения обмена сообщениями (с помощью пакета SDK v4)

| Пример | Описание | .NET Core | JavaScript | Python|
|--------|------------- |---|---|----|
| Команда поиска | Расширение простого обмена сообщениями с помощью команды поиска | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)| [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/50.teams-messaging-extension-search)|
| Команда Action | Расширение простой системы обмена сообщениями с помощью команды Action. Отклик, вставленный в область сообщения "создание". | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/51.teams-messaging-extensions-action)|
| Команда Action с откликом от ленты | Расширение системы обмена сообщениями с помощью команды Action. Отклик, вставленный в беседу в беседе с помощью Bot. | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/53.teams-messaging-extensions-action-preview)|
| Команда поиска | расширение системы обмена сообщениями с помощью команды поиска и проверки подлинности и конфигурации | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)| [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/52.teams-messaging-extensions-search-auth-config)|

## <a name="outgoing-webhooks"></a>Исходящие веб-перехватчики

| Пример | Описание
|--------|-------------
| [Исходящий веб-перехватчик для C#/.нет](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | Описывается создание **исходящего веб-перехватчика** для Microsoft Teams в C#/.нет.
| [Исходящий веб-перехватчик для Node.js](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | Показано, как создать простой **исходящий веб-перехватчик** для Microsoft Teams в строках кода Node.js ~ 50.

## <a name="connectors"></a>Соединители

| Пример | Описание
|--------|-------------
| [Пример соединителя для Node.js](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | В этом примере, написанном на Node.js, показано, как создать соединитель для Microsoft Teams, используя GitHub в качестве примера для создания уведомлений соединителей.
| [Пример соединителя для C#/.нет](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | В этом примере, написанном на языке C#, показано, как создать соединитель для Microsoft Teams, используя пример приложения списка задач в качестве примера для создания уведомлений соединителей.

## <a name="graph-api"></a>API Graph

| Пример | Описание
|--------|-------------
| [Примеры API Microsoft Graph](https://github.com/OfficeDev/microsoft-teams-sample-graph) | В этих примерах демонстрируется использование вызовов API Microsoft Graph для выполнения таких задач, как запросы к Teams и каналам из веб-службы, запущенной за пределами Microsoft Teams.

### <a name="bot-framework-sdk-v3-samples"></a>Примеры SDK для Bot Framework v3

| Пример | Описание |
|--------|------------- |
| [Пример кода робота для C#/.нет](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Примеры для Bot Framework v3|
| [Пример кода робота для Node.js](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Примеры для Bot Framework v3 |
