---
title: Создание расширения для сообщений с помощью App Studio
author: surbhigupta
description: Узнайте, как создать расширение Microsoft Teams с помощью App Studio.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 61bfed969b981bd5000bdb6eca0bbd77196e8086
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157211"
---
# <a name="create-a-messaging-extension-using-app-studio"></a>Создание расширения для сообщений с помощью App Studio

> [!TIP]
> Ищете более быстрый способ начать работу? Создание [расширения обмена сообщениями с](../build-your-first-app/build-messaging-extension.md) помощью Microsoft Teams набор средств.

На высоком уровне необходимо выполнить следующие действия для создания расширения обмена сообщениями.

1. Подготовка среды разработки
2. Создание и развертывание веб-службы (при разработке используйте туннельную службу, например ngrok, чтобы запустить ее локально)
3. Регистрация веб-службы в Bot Framework
4. Создание пакета приложения
5. Отправка пакета в Microsoft Teams

Создание веб-службы, создание пакета приложений и регистрация веб-службы с помощью Bot Framework можно сделать в любом порядке. Так как эти три части настолько переплетены, независимо от того, какой порядок вы их делаете, вам потребуется вернуться, чтобы обновить другие. Для регистрации требуется конечная точка обмена сообщениями из развернутой веб-службы, а веб-службе необходим код и пароль, созданные в вашей регистрации. Манифест приложения также должен быть id для подключения Teams к веб-службе.

При создании расширения обмена сообщениями вы будете регулярно передвигаться между изменением манифеста приложения и развертыванием кода в веб-службе. При работе с манифестом приложения имейте в виду, что вы можете либо вручную управлять JSON-файлом, либо вносить изменения через App Studio. В любом случае при внесении изменений в манифест необходимо повторно развернуть (загрузить) приложение в Teams, но при развертывании изменений в веб-службе это не требуется.

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Создание веб-службы

Сердцем расширения обмена сообщениями является веб-служба. Он определяет один маршрут, как `/api/messages` правило, для получения всех запросов. Если вы начинаете работу с нуля, у вас есть несколько вариантов на выбор.

* Используйте один из наших [учебников quickstarts,](#learn-more) который поможет вам создать веб-службу.
* Выберите один из примеров расширения обмена сообщениями, доступный в репозитории [образца Bot Framework,](https://github.com/Microsoft/BotBuilder-Samples) чтобы начать с него.
* Если вы используете JavaScript, используйте генератор [Yeoman](https://github.com/OfficeDev/generator-teams) для Microsoft Teams для Teams приложения, в том числе веб-службы.
* Создайте веб-службу с нуля. Вы можете добавить пакет SDK Bot Framework для своего языка или работать непосредственно с полезными данными JSON.

## <a name="register-your-web-service-with-the-bot-framework"></a>Регистрация веб-службы в Bot Framework

Расширения обмена сообщениями пользуются схемой обмена сообщениями Bot Framework и протоколом безопасной связи; если у вас еще нет его, вам потребуется зарегистрировать веб-службу в Bot Framework. Id Приложения Майкрософт (мы назначим это как бот-Ид изнутри Teams, чтобы идентифицировать его из другого app Id, с помощью который вы можете работать) и конечная точка обмена сообщениями, с помощью регистра с помощью Bot Framework, будет использоваться в расширении обмена сообщениями для получения запросов и ответа на них. Если вы используете существующую регистрацию, убедитесь, что вы включаете [Microsoft Teams канал](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true).

Если вы выполните один из quickstarts или начнете с одного из доступных образцов, вы будете руководствоваться регистрацией веб-службы. Если вы хотите вручную зарегистрировать свою службу, у вас есть три варианта для этого. Если вы решите зарегистрироваться без использования подписки Azure, вы не сможете воспользоваться упрощенным потоком проверки подлинности OAuth, предоставляемым Bot Framework. После создания вы сможете перенести регистрацию в Azure.

* Если у вас есть подписка Azure (или вы хотите создать новую), вы можете зарегистрировать веб-службу вручную с помощью портала Azure. Создайте ресурс "Регистрация каналов ботов". Вы можете выбрать уровень бесплатных цен, так как сообщения из Microsoft Teams не учитываются в сумме допустимых сообщений в месяц.
* Если вы не хотите использовать подписку Azure, вы можете использовать устаревший портал [регистрации.](https://dev.botframework.com/bots/new)
* App Studio также может помочь вам зарегистрировать веб-службу (бот). Веб-службы, зарегистрированные через App Studio, не регистрируются в Azure. Вы можете использовать [устаревший портал для](https://dev.botframework.com/bots) просмотра, управления и переноса регистраций.

## <a name="create-your-app-manifest"></a>Создание манифеста приложения

Вы можете использовать App Studio для создания манифеста приложения или создать его вручную.

### <a name="create-your-app-manifest-using-app-studio"></a>Создание манифеста приложения с помощью App Studio

Приложение App Studio можно использовать в клиенте Microsoft Teams, чтобы помочь создать манифест приложения.

1. В клиенте Teams откройте App Studio из меню переполнения **...** на панели навигации слева. Если он еще не установлен, это можно сделать, ища его.
2. На **вкладке Редактор** Манифест выберите **Создание** нового приложения (или если вы добавляете расширение обмена сообщениями в существующее приложение, вы можете импортировать пакет приложения)
3. Добавьте сведения о приложении (см. [определение схемы манифеста](~/resources/schema/manifest-schema.md) с полным описанием каждого поля).
4. На **вкладке Расширения обмена сообщениями нажмите** кнопку **Настройка.**
5. Вы можете создать новую веб-службу (бот) для расширения обмена сообщениями для использования, или если вы уже зарегистрировали один выбор или добавить его здесь.
6. При необходимости обновите адрес конечной точки бота, чтобы он указывал на вашего бота. Он должен выглядеть примерно следующим образом: `https://someplace.com/api/messages`.
7. Кнопка **Добавить** в разделе **Команда** поможет вам добавить команды в расширение обмена сообщениями. Дополнительные [ссылки на](#learn-more) дополнительные сведения о добавлении команд см. в разделе Дополнительные сведения. Помните, что для расширения обмена сообщениями можно определить до 10 команд.
8. Раздел **Обработчики** сообщений позволяет добавить домен, на который будут запускаться ваши сообщения. Дополнительные [сведения см. в ссылке unfurling.](~/messaging-extensions/how-to/link-unfurling.md)

На **вкладке Готово =>** тест и  распространение можно скачать пакет приложения (который включает манифест  приложения, а также значки приложения) или установить пакет.

### <a name="create-your-app-manifest-manually"></a>Создание манифеста приложения вручную

Как и в ботах и [](~/resources/schema/manifest-schema.md#composeextensions) вкладок, вы обновляете манифест приложения для приложения, чтобы включить свойства расширения обмена сообщениями. Эти свойства регулируют, как отображается и ведет себя расширение обмена сообщениями в Microsoft Teams клиенте. Расширения обмена сообщениями поддерживаются начиная с v1.0 манифеста.

#### <a name="declare-your-messaging-extension"></a>Объявление расширения обмена сообщениями

Чтобы добавить расширение обмена сообщениями, включите новую структуру JSON верхнего уровня в манифест приложения с `composeExtensions` свойством. Для приложения создается одно расширение обмена сообщениями с до 10 командами.

> [!NOTE]
> Манифест относится к расширениям обмена сообщениями как `composeExtensions` . Это необходимо для поддержания обратной совместимости.

Определение расширения — это объект, который имеет следующую структуру:

| Имя свойства | Назначение | Обязательный? |
|---|---|---|
| `botId` | Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework. Это обычно должно быть таким же, как ИД для общего Teams приложения. | Да |
| `canUpdateConfiguration` | Включает **Параметры** меню. | Нет |
| `commands` | Массив команд, поддерживаемых этим расширением обмена сообщениями. Вы ограничены 10 командами. | Да |

#### <a name="define-your-commands"></a>Определение команд

Расширение обмена сообщениями должно объявлять одну или несколько команд, определяющих, где пользователи могут запускать расширение обмена сообщениями, и тип взаимодействия. Дополнительные [сведения о](#learn-more) командах расширения обмена сообщениями см. в дополнительных сведениях.

#### <a name="simple-manifest-example"></a>Пример простого манифеста

Ниже приводится простой объект расширения обмена сообщениями в манифесте приложения с командой поиска. Это не весь файл манифеста приложения, а только часть, относящаяся к расширениям для обмена сообщениями. Полный [пример см. в](~/resources/schema/manifest-schema.md) схеме манифеста приложения.

```json
...
"composeExtensions": [
  {
    "botId": "abcd1234-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "searchCmd",
        "description": "Search you ToDo's",
        "title": "Search",
        "initialRun": true,
        "parameters": [
          {
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }
        ]
      }
    ]
  }
]
...
```

#### <a name="complete-app-manifest-example"></a>Полный пример манифеста приложения

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

## <a name="add-your-invoke-message-handlers"></a>Добавление обработчиков сообщений вызова

Когда пользователи запускают расширение обмена сообщениями, вам потребуется обрабатывать начальное сообщение вызова, собирать некоторые сведения от пользователя, а затем обрабатывать эти сведения и соответствующим образом реагировать. Для этого сначала необходимо решить, какие команды необходимо добавить в расширение обмена сообщениями, [](~/messaging-extensions/how-to/action-commands/define-action-command.md) а также добавить команды действий или добавить команды [поиска.](~/messaging-extensions/how-to/search-commands/define-search-command.md)

## <a name="messaging-extensions-in-teams-meetings"></a>Расширения обмена сообщениями в Teams собраниях

> [!NOTE]
> Если в реестре на собрании или групповом чате есть федераторы, Teams подавляет доступ к расширениям обмена сообщениями для всех пользователей, включая организатора.

После начала собрания участники Teams напрямую взаимодействовать с расширением обмена сообщениями во время прямого звонка. При создании расширения обмена сообщениями на собрании рассмотрим следующее:

1. **Location**. Расширение обмена сообщениями можно вызвать из области составить сообщение, командного окна или @mentioned в чате собрания.

1. **Метаданные**. При вызове расширения обмена сообщениями он может идентифицировать пользователя и клиента от `userId` и `tenantId` . `meetingId` может быть частью объекта `channelData`. Приложение может использовать запрос API и для получения `userId` `meetingId`  ролей `GetParticipant` пользователя.

1. **Тип команды**. Если в расширении сообщения [используются команды,](../messaging-extensions/what-are-messaging-extensions.md#action-commands)основанные на действиях, оно должно выполнять проверку подлинности вкладки с одним [входом.](../tabs/how-to/authentication/auth-aad-sso.md)

1. **Пользовательский опыт**. Расширение обмена сообщениями должно выглядеть и вести себя так же, как и вне собрания.

## <a name="next-steps"></a>Дальнейшие действия

* [Создание команд действий](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [Создание команд поиска](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Развертывание ссылки](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>Подробнее

Попробуйте его в quickstart:

* Quickstarts для C #
  * [Расширение обмена сообщениями с командами на основе действий](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [Расширение обмена сообщениями с командами на основе поиска](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* Quickstarts для JavaScript
  * [Расширение обмена сообщениями с командами на основе действий](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [Расширение обмена сообщениями с командами на основе поиска](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

Дополнительные дополнительные Teams концепции разработки:

* [Понимание Teams приложений](../concepts/capabilities-overview.md)
* [Что такое расширения для сообщений?](../messaging-extensions/what-are-messaging-extensions.md)
