---
title: Создание расширения для сообщений с помощью App Studio
author: surbhigupta
description: Узнайте, как создать расширение Microsoft Teams сообщений с помощью App Studio.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 09bc7a7884f69c7c3ac4c8e195e5ac6d14d20990
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032783"
---
# <a name="create-a-messaging-extension-using-app-studio"></a>Создание расширения для сообщений с помощью App Studio

> [!TIP]
> Ищете более быстрый способ начать работу? Создайте [расширение для обмена сообщениями](../build-your-first-app/build-messaging-extension.md) с помощью Microsoft Teams Toolkit.

На высоком уровне вам потребуется выполнить следующие действия, чтобы создать расширение для обмена сообщениями.

1. Подготовка среды разработки
2. Создание и развертывание веб-службы (во время разработки используйте службу туннелирования, например ngrok, для локального запуска).
3. Регистрация веб-службы в Bot Framework
4. Создание пакета приложения
5. Отправка пакета в Microsoft Teams

Создание веб-службы, создание пакета приложения и регистрация веб-службы в Bot Framework можно выполнить в любом порядке. Так как эти три фрагмента настолько упорядочены, независимо от того, в каком порядке вы их выполняете, вам потребуется вернуться для обновления остальных. Для регистрации требуется конечная точка обмена сообщениями из развернутой веб-службы, а веб-службе — идентификатор и пароль, созданные при регистрации. Манифесту приложения также требуется этот идентификатор для подключения Teams к веб-службе.

При создании расширения для обмена сообщениями вы будете регулярно переключаться между изменением манифеста приложения и развертыванием кода в веб-службе. При работе с манифестом приложения убедитесь, что вы можете вручную изменить JSON-файл или внести изменения в App Studio. В любом случае вам потребуется повторно развернуть (отправить) приложение в Teams при внесении изменений в манифест, но это не нужно делать при развертывании изменений в веб-службе.

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Создание веб-службы

Основной частью расширения для обмена сообщениями является веб-служба. Он определяет один маршрут, как правило `/api/messages`, для получения всех запросов. Если вы приступите к работе с нуля, у вас есть несколько вариантов выбора.

* Воспользуйтесь одним из наших [кратких руководств](#learn-more) по созданию веб-службы.
* Выберите один из примеров расширений для обмена сообщениями, доступных в [репозитории примеров Bot Framework](https://github.com/Microsoft/BotBuilder-Samples) , чтобы начать с этого.
* Если вы используете JavaScript, используйте генератор [Yeoman](https://github.com/OfficeDev/generator-teams) для Microsoft Teams шаблона приложения Teams, включая веб-службу.
* Создайте веб-службу с нуля. Вы можете добавить пакет SDK Bot Framework для своего языка или работать непосредственно с полезными данными JSON.

## <a name="register-your-web-service-with-the-bot-framework"></a>Регистрация веб-службы в Bot Framework

Расширения обмена сообщениями используют схему обмена сообщениями Bot Framework и протокол безопасного обмена сообщениями. Если у вас ее еще нет, необходимо зарегистрировать веб-службу в Bot Framework. Идентификатор приложения Майкрософт (мы будем называть его идентификатором бота из Teams, чтобы идентифицировать его из другого идентификатора приложения, с помощью которых вы можете работать), а конечная точка обмена сообщениями, с помощью которых регистрируется в Bot Framework, будет использоваться в расширении обмена сообщениями для получения запросов и реагирования на них. Если вы используете существующую регистрацию, убедитесь, что включен Microsoft Teams [канал](/azure/bot-service/bot-service-manage-channels?preserve-view=true&view=azure-bot-service-4.0).

Если вы выполните одно из кратких руководств или начните с одного из доступных примеров, вам будет предложено зарегистрировать веб-службу. Если вы хотите вручную зарегистрировать службу, это можно сделать тремя способами. Если вы решили зарегистрироваться без использования подписки Azure, вы не сможете воспользоваться упрощенным потоком проверки подлинности OAuth, предоставляемым Bot Framework. После создания вы сможете перенести регистрацию в Azure.

* Если у вас есть подписка Azure (или вы хотите создать новую), вы можете зарегистрировать веб-службу вручную с помощью Microsoft Azure портала. Создайте ресурс "Регистрация каналов бота". Вы можете выбрать бесплатную ценовую категорию, так как сообщения из Microsoft Teams не учитываются в общем допустимом количестве сообщений в месяц.
* Если вы не хотите использовать подписку Azure, можно использовать устаревший [портал регистрации](https://dev.botframework.com/bots/new).
* App Studio также может помочь вам зарегистрировать веб-службу (бот). Веб-службы, зарегистрированные через App Studio, не регистрируются в Azure. Вы можете использовать [устаревший портал для](https://dev.botframework.com/bots) просмотра и переноса регистраций, а также управления ими.

## <a name="create-your-app-manifest"></a>Создание манифеста приложения

Вы можете использовать App Studio для создания манифеста приложения или создать его вручную.

### <a name="create-your-app-manifest-using-app-studio"></a>Создание манифеста приложения с помощью App Studio

Приложение App Studio можно использовать в клиенте Microsoft Teams для создания манифеста приложения.

1. В клиенте Teams откройте App Studio из меню переполнения **...** на панели навигации слева. Если он еще не установлен, это можно сделать, выполнив поиск.
2. На **вкладке редактора** манифеста выберите **"** Создать новое приложение" (или при добавлении расширения для обмена сообщениями в существующее приложение можно импортировать пакет приложения).
3. Добавьте сведения о приложении (см. [определение схемы манифеста](~/resources/schema/manifest-schema.md) с полным описанием каждого поля).
4. На **вкладке "Расширения для обмена сообщениями** " нажмите **кнопку "Настройка** ".
5. Вы можете создать новую веб-службу (бот) для расширения обмена сообщениями или, если вы уже зарегистрировали один из них, выберите или добавьте его здесь.
6. При необходимости обновите адрес конечной точки бота, чтобы он указывал на вашего бота. Он должен выглядеть примерно следующим образом: `https://someplace.com/api/messages`.
7. **Кнопка "** Добавить **" в разделе** "Команда" поможет вам добавить команды в расширение обмена сообщениями. Дополнительные [сведения о](#learn-more) добавлении команд см. в разделе "Дополнительные сведения". Помните, что для расширения обмена сообщениями можно определить до 10 команд.
8. Раздел **"Обработчики** сообщений" позволяет добавить домен, в котором будет активироваться обмен сообщениями. [Дополнительные сведения см. в разделе "Размыкание](~/messaging-extensions/how-to/link-unfurling.md) ссылок".

На вкладке **"Готово" =>** "Тестирование и распространение" можно  скачать пакет приложения (который включает манифест приложения, а также значки приложения) или установить пакет.

### <a name="create-your-app-manifest-manually"></a>Создание манифеста приложения вручную

Как и в случае с ботами и вкладками, [](~/resources/schema/manifest-schema.md#composeextensions) манифест приложения обновляется, чтобы включить свойства расширения для обмена сообщениями. Эти свойства определяют, как расширение обмена сообщениями отображается и ведет себя в Microsoft Teams клиенте. Расширения обмена сообщениями поддерживаются начиная с версии 1.0 манифеста.

#### <a name="declare-your-messaging-extension"></a>Объявление расширения для обмена сообщениями

Чтобы добавить расширение для обмена сообщениями, добавьте новую структуру JSON верхнего уровня в манифест приложения со свойством `composeExtensions` . Для приложения создается одно расширение для обмена сообщениями с до 10 командами.

> [!NOTE]
> Манифест ссылается на расширения обмена сообщениями как `composeExtensions`. Это необходимо для обеспечения обратной совместимости.

Определение расширения — это объект со следующей структурой:

| Имя свойства | Назначение | Обязательный? |
|---|---|---|
| `botId` | Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework. Обычно он должен совпадать с идентификатором для общего Teams приложения. | Да |
| `canUpdateConfiguration` | Включает **Параметры меню**. | Нет |
| `commands` | Массив команд, поддерживаемых этим расширением обмена сообщениями. Количество команд ограничено 10. | Да |

#### <a name="define-your-commands"></a>Определение команд

Расширение обмена сообщениями должно объявлять одну или несколько команд, которые определяют, где пользователи могут активировать расширение обмена сообщениями, и тип взаимодействия. [Дополнительные сведения о](#learn-more) командах расширения для обмена сообщениями см. в этой статье.

#### <a name="simple-manifest-example"></a>Пример простого манифеста

В следующем примере показан простой объект расширения для обмена сообщениями в манифесте приложения с командой поиска. Это не весь файл манифеста приложения, а только часть, относящаяся к расширениям для обмена сообщениями. Полный [пример см. в](~/resources/schema/manifest-schema.md) схеме манифеста приложения.

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

Когда пользователи активирует расширение обмена сообщениями, вам потребуется обработать начальное сообщение об вызове, собрать некоторые сведения от пользователя, а затем обработать эти сведения и ответить соответствующим образом. Для этого сначала необходимо решить, какие команды вы хотите добавить в расширение обмена сообщениями, а также добавить команды действий или команды [поиска](~/messaging-extensions/how-to/search-commands/define-search-command.md).[](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="messaging-extensions-in-teams-meetings"></a>Расширения обмена сообщениями на Teams собраниях

> [!NOTE]
> Если во время собрания или группового чата есть федеративные пользователи в списке, Teams доступ к расширениям обмена сообщениями для всех пользователей, включая организатора.

Когда собрание начнется, Teams могут напрямую взаимодействовать с расширением обмена сообщениями во время прямого звонка. При создании расширения для обмена сообщениями на собрании учитывайте следующее:

1. **Location**. Расширение обмена сообщениями можно вызвать из области создания сообщения, командного поля или @mentioned в чате собрания.

1. **Метаданные**. При вызове расширения обмена сообщениями оно может идентифицировать пользователя и клиента из `userId` и `tenantId`. `meetingId` может быть частью объекта `channelData`. Приложение может использовать запрос `userId` API и `meetingId` `GetParticipant` для получения ролей пользователя.

1. **Тип команды**. Если расширение сообщения использует [команды](../messaging-extensions/what-are-messaging-extensions.md#action-commands) на основе действий, оно должно соответствовать проверке [](../tabs/how-to/authentication/tab-sso-overview.md) подлинности единого входа на вкладке.

1. **Взаимодействие с пользователем**. Расширение обмена сообщениями должно выглядеть и вести себя так же, как за пределами собрания.

## <a name="next-steps"></a>Дальнейшие действия

* [Создание команд действий](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [Создание команд поиска](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Развертывание ссылки](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>Подробнее

Ознакомьтесь с кратким руководством.

* Краткие руководства по C#
  * [Расширение обмена сообщениями с командами на основе действий](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [Расширение обмена сообщениями с командами на основе поиска](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* Краткие руководства по JavaScript
  * [Расширение обмена сообщениями с командами на основе действий](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [Расширение обмена сообщениями с командами на основе поиска](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

Дополнительные сведения о Teams разработки:

* [Общие Teams приложения](../concepts/capabilities-overview.md)
* [Что такое расширения для сообщений?](../messaging-extensions/what-are-messaging-extensions.md)
