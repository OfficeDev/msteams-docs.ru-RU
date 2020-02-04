---
title: Примеры кода Microsoft Teams
description: Ссылки и описания примеров приложений для платформы разработчика Microsoft Teams
keywords: Примеры разработчиков Microsoft Teams
ms.openlocfilehash: eb7794e788f8eb39102ac874748e23d8621f281e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675152"
---
# <a name="code-samples-for-the-microsoft-teams-developer-platform"></a>Примеры кода для платформы разработчика Microsoft Teams

Здесь вы найдете список примеров кода, демонстрирующих различные возможности платформы разработки Microsoft Teams и создание приложений для использования этих функций.

## <a name="getting-samples"></a>Извлечение образцов

Чтобы скачать наши примеры из GitHub, выполните следующие действия.

1. Выберите один из перечисленных ниже проектов и откройте проект в GitHub.
2. Нажмите кнопку **клонировать или скачать** и скопируйте URL-адрес.
3. Откройте командную строку в родительском каталоге, в который необходимо установить пример проекта.
4. Выполняем`git clone <pasted url>`

### <a name="for-netc-samples"></a>Примеры для .NET и C#

Каждый из наших примеров .NET включает файл решения Visual Studio, с помощью которого можно полностью создать решение, включая восстановление пакетов NuGet.

### <a name="for-nodejs-samples"></a>Примеры для Node. js

Мы предоставляем файл Packages. JSON, в котором перечислены все необходимые пакеты для примера. Просто запустите `npm install` из командной строки в каталоге проекта Node. js, чтобы установить необходимые пакеты. Теперь вы готовы открыть проект в Visual Studio Code и начать эксперимент.

### <a name="for-other-samples"></a>Для других примеров

Как всегда, файл README проекта должен содержать более подробную информацию о конкретных примерах.

## <a name="get-started"></a>Начало работы

| Пример | Описание|
|--------|-------------|
| [Hello World в Microsoft Teams с Node. js](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) | Пример приложения Teams, `Node.js` в котором вы можете получить базовые возможности приложений.|
| [Hello World в Microsoft Teams с C# .NET](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) | Пример приложения Teams, `C# .NET` в котором вы можете получить базовые возможности приложений.|
| [Приступая к работе с генератором Yeoman для Teams](~/tutorials/get-started-yeoman.md) | Создайте приложение Teams с нуля с помощью генератора Yeoman для Microsoft Teams. |

## <a name="bots-using-the-v4-sdk"></a>Боты (с использованием пакета SDK v4)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="messaging-extensions-using-the-v4-sdk"></a>Расширения обмена сообщениями (с помощью пакета SDK v4)

| Пример | Описание | .NET Core | JavaScript |
|--------|------------- |---|---|
| Команда поиска | Расширение простого обмена сообщениями с помощью команды поиска | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|
| Команда Action | Расширение простой системы обмена сообщениями с помощью команды Action. Отклик, вставленный в область сообщения "создание". | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)|
| Команда Action с откликом от ленты | Расширение системы обмена сообщениями с помощью команды Action. Отклик, вставленный в беседу в беседе с помощью Bot. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview)|
| Команда поиска | расширение системы обмена сообщениями с помощью команды поиска и проверки подлинности и конфигурации | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|

## <a name="outgoing-webhooks"></a>Исходящие веб-перехватчики

| Пример | Описание
|--------|-------------
| [Исходящий веб-перехватчик для C#/.нет](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | Описывается создание **исходящего веб-перехватчика** для Microsoft Teams в C#/.нет.
| [Исходящий веб-перехватчик для Node. js](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | В этом примере показано, как создать простой **исходящий веб-перехватчик** для Microsoft Teams в строках ~ 50, посвященных коду Node. js.

## <a name="connectors"></a>Соединители

| Пример | Описание
|--------|-------------
| [Пример соединителя для Node. js](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | В этом примере, написанном на Node. js, показано, как создать соединитель для Microsoft Teams, используя GitHub в качестве примера для создания уведомлений соединителей.
| [Пример соединителя для C#/.нет](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | В этом примере, написанном на языке C#, показано, как создать соединитель для Microsoft Teams, используя пример приложения списка задач в качестве примера для создания уведомлений соединителей.

## <a name="graph-api"></a>API Graph

| Пример | Описание
|--------|-------------
| [Примеры API Microsoft Graph](https://github.com/OfficeDev/microsoft-teams-sample-graph) | В этих примерах демонстрируется использование вызовов API Microsoft Graph для выполнения таких задач, как запросы к Teams и каналам из веб-службы, запущенной за пределами Microsoft Teams.

## <a name="others"></a>Другие

| Код | Описание |
|------|------------- |
| [Полный пример в Node. js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) | В этом примере показано, как использовать все функции платформы Microsoft Teams. NOTE: в этом примере используется пакет SDK для Bot Framework v3.|
| [Полный пример в C#/.нет](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) | В этом примере показано, как использовать все функции платформы Microsoft Teams. NOTE: в этом примере используется пакет SDK для Bot Framework v3. |
| [Бизнес-приложения в C#/.нет](https://github.com/OfficeDev/msteams-sample-line-of-business-apps-csharp) | Этот репозиторий содержит несколько примеров бизнес-приложений, которые можно использовать как для создания идей, так и для шаблонов, создаваемых поверх. Примечание. в этих примерах используется пакет SDK для Bot Framework v3.|
| [Пример приложения вкладки "список дел"](https://github.com/OfficeDev/microsoft-teams-sample-todo) | В этом примере Node. js показано, как легко преобразовать существующее веб-приложение на вкладку. |
| [орки](https://github.com/OfficeDev/Orky) | Вы можете использовать орки для регистрации собственной локальной программы Bot в Microsoft Teams и выполнения сценариев из любого места! |
| [Создание прогноза 2017](https://github.com/OfficeDev/microsoft-teams-build2017-weather) | Прием. Исходный код для сеанса//Build/2017, чтобы добавить вкладку Weather в скелет приложения, созданного ранее в сеансе. |

### <a name="bot-framework-sdk-v3-samples"></a>Примеры SDK для Bot Framework v3

| Пример | Описание |
|--------|------------- |
| [Пример кода робота для C#/.нет](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Примеры для Bot Framework v3|
| [Пример кода робота для Node. js](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Примеры для Bot Framework v3 |
