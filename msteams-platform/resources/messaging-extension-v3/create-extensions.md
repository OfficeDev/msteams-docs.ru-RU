---
title: Инициировать действия с расширениями обмена сообщениями
description: Создание расширений обмена сообщениями на основе действий, позволяющих пользователям запускать внешние службы
localization_priority: Normal
ms.topic: how-to
keywords: команды расширения обмена сообщениями расширениями обмена сообщениями поиска
ms.openlocfilehash: 5604d86f05bad42bf3a00f611711afc34beedf42
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140371"
---
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="8b994-104">Инициировать действия с расширениями обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="8b994-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="8b994-105">Расширения обмена сообщениями на основе действий позволяют пользователям запускать действия во внешних службах во время Teams.</span><span class="sxs-lookup"><span data-stu-id="8b994-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![Пример карточки расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="8b994-107">В следующих разделах описано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="8b994-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="8b994-108">Расширения сообщений типа действия</span><span class="sxs-lookup"><span data-stu-id="8b994-108">Action type message extensions</span></span>

<span data-ttu-id="8b994-109">Чтобы инициировать действия из расширения обмена сообщениями, задан `type` параметр `action` .</span><span class="sxs-lookup"><span data-stu-id="8b994-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="8b994-110">Ниже приведен пример манифеста с поиском и командой создания.</span><span class="sxs-lookup"><span data-stu-id="8b994-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="8b994-111">Одно расширение обмена сообщениями может иметь до 10 различных команд.</span><span class="sxs-lookup"><span data-stu-id="8b994-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="8b994-112">Это может включать как несколько команд поиска, так и несколько команд на основе действий.</span><span class="sxs-lookup"><span data-stu-id="8b994-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="8b994-113">Полный пример манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="8b994-113">Complete app manifest example</span></span>

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

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="8b994-114">Инициировать действия из сообщений</span><span class="sxs-lookup"><span data-stu-id="8b994-114">Initiate actions from messages</span></span>

<span data-ttu-id="8b994-115">Помимо инициации действий из области составить сообщение, вы также можете использовать расширение обмена сообщениями, чтобы инициировать действие из сообщения.</span><span class="sxs-lookup"><span data-stu-id="8b994-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="8b994-116">Это позволит отправлять содержимое сообщения боту для обработки и необязательно отвечать на это сообщение ответом с помощью метода, описанного в ответе для [отправки.](#responding-to-submit)</span><span class="sxs-lookup"><span data-stu-id="8b994-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="8b994-117">Ответ будет вставлен в качестве ответа на сообщение, которое пользователи могут изменить перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="8b994-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="8b994-118">Пользователи могут получить доступ к расширению обмена сообщениями из меню переполнения, а затем выбрать, `...` `Take action` как на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="8b994-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the following image:</span></span>

![Пример инициирования действия из сообщения](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="8b994-120">Чтобы расширение обмена сообщениями работало из сообщения, необходимо добавить параметр к объекту расширения обмена сообщениями в манифесте приложения, как в `context` `commands` примере ниже.</span><span class="sxs-lookup"><span data-stu-id="8b994-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="8b994-121">Допустимые строки `context` для массива `"message"` являются , `"commandBox"` и `"compose"` .</span><span class="sxs-lookup"><span data-stu-id="8b994-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="8b994-122">Значение по умолчанию — `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="8b994-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="8b994-123">Подробные [сведения](#define-commands) о параметре см. в разделе Определить `context` команды.</span><span class="sxs-lookup"><span data-stu-id="8b994-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

```json
"composeExtensions": [
  {
    "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Create To Do",
        "type": "Action",
        "context": ["message"],
        "fetchTask": true
    }]
    ...

```

<span data-ttu-id="8b994-124">Ниже приведен пример объекта, содержащего сведения о сообщении, которые будут отправлены в рамках запроса, `value` `composeExtension` отправленного вашему боту.</span><span class="sxs-lookup"><span data-stu-id="8b994-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "this is the message"
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

### <a name="test-via-uploading"></a><span data-ttu-id="8b994-125">Тестирование с помощью загрузки</span><span class="sxs-lookup"><span data-stu-id="8b994-125">Test via uploading</span></span>

<span data-ttu-id="8b994-126">Вы можете протестировать расширение обмена сообщениями, загрузив приложение.</span><span class="sxs-lookup"><span data-stu-id="8b994-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="8b994-127">Дополнительные сведения см. [в сайте Uploading your app in a team.](~/concepts/deploy-and-publish/apps-upload.md)</span><span class="sxs-lookup"><span data-stu-id="8b994-127">For more information, see [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md).</span></span>

<span data-ttu-id="8b994-128">Чтобы открыть расширение обмена сообщениями, перейдите к любому из ваших чатов или каналов.</span><span class="sxs-lookup"><span data-stu-id="8b994-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="8b994-129">Выберите **кнопку Дополнительные** параметры **(&#8943;)** в поле составить и выберите расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8b994-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="8b994-130">Сбор входных данных от пользователей</span><span class="sxs-lookup"><span data-stu-id="8b994-130">Collecting input from users</span></span>

<span data-ttu-id="8b994-131">Существует три способа сбора сведений от пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="8b994-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="8b994-132">Список статических параметров</span><span class="sxs-lookup"><span data-stu-id="8b994-132">Static parameter list</span></span>

<span data-ttu-id="8b994-133">В этом методе необходимо определить статический список параметров манифеста, как показано выше в команде "Создание To Do".</span><span class="sxs-lookup"><span data-stu-id="8b994-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="8b994-134">Для использования этого метода задана настройка и определение `fetchTask` `false` параметров в манифесте.</span><span class="sxs-lookup"><span data-stu-id="8b994-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="8b994-135">Когда пользователь выбирает команду со статичными параметрами, Teams создает форму в модуле задач с параметрами, определенными в манифесте.</span><span class="sxs-lookup"><span data-stu-id="8b994-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="8b994-136">При нажатии Отправить `composeExtension/submitAction` отправляется боту.</span><span class="sxs-lookup"><span data-stu-id="8b994-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="8b994-137">Дополнительные сведения о ожидаемом наборе ответов см. в [ответе на отправку.](#responding-to-submit)</span><span class="sxs-lookup"><span data-stu-id="8b994-137">For more information on the expected set of responses, see [Responding to submit](#responding-to-submit).</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="8b994-138">Динамический ввод с помощью адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="8b994-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="8b994-139">В этом методе служба может определить настраиваемую адаптивную карту для сбора ввода конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="8b994-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="8b994-140">Для этого подхода установите параметр `fetchTask` в `true` манифесте.</span><span class="sxs-lookup"><span data-stu-id="8b994-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="8b994-141">Обратите внимание, что если вы заданы какие-либо статические параметры, определенные для `fetchTask` `true` команды, будут проигнорированы.</span><span class="sxs-lookup"><span data-stu-id="8b994-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="8b994-142">В этом методе служба получает событие и отвечает адаптивным ответом модуля задач на основе `composeExtension/fetchTask` [карт.](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="8b994-142">In this method your service receives a `composeExtension/fetchTask` event and responds with an adaptive card based [task module response](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="8b994-143">Ниже приводится пример ответа с адаптивной картой:</span><span class="sxs-lookup"><span data-stu-id="8b994-143">Following is a sample response with an adaptive card:</span></span>

```json
{
    "task": {
        "type": "continue",
        "value": {
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": {
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Please enter the following information:"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Name"
                        },
                        {
                            "type": "Input.Text",
                            "spacing": "None",
                            "title": "New Input.Toggle",
                            "placeholder": "Placeholder text"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Date of birth"
                        },
                        {
                            "type": "Input.Date",
                            "spacing": "None",
                            "title": "New Input.Toggle"
                        }
                    ],
                    "type": "AdaptiveCard",
                    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
                    "version": "1.0"
                }
            }
        }
    }
}
```

<span data-ttu-id="8b994-144">Бот также может отвечать ответом auth/config, если пользователю необходимо проверить подлинность или настроить расширение перед получением ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="8b994-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="8b994-145">Динамический ввод с помощью веб-представления</span><span class="sxs-lookup"><span data-stu-id="8b994-145">Dynamic input using a web view</span></span>

<span data-ttu-id="8b994-146">В этом методе служба может показать основанный виджет, чтобы показать любой пользовательский `<iframe>` пользовательский интерфейс и собрать пользовательский ввод.</span><span class="sxs-lookup"><span data-stu-id="8b994-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="8b994-147">Для этого подхода установите параметр `fetchTask` в `true` манифесте.</span><span class="sxs-lookup"><span data-stu-id="8b994-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="8b994-148">Так же, как и в потоке адаптивной карты, служба отправляет событие и отвечает ответом целевого модуля на основе `fetchTask` [URL-адресов.](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="8b994-148">Just like in the adaptive card flow your service sends a `fetchTask` event and responds with a URL based [task module response](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="8b994-149">Ниже приводится пример ответа с адаптивной картой:</span><span class="sxs-lookup"><span data-stu-id="8b994-149">Following is a sample response with an Adaptive card:</span></span>

```json
{
    "task": {
        "value": {
            "url": "http://mywebapp.com/input"
        },
        "type": "continue"
    }
}
```

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="8b994-150">Запрос на установку разговорного бота</span><span class="sxs-lookup"><span data-stu-id="8b994-150">Request to install your conversational bot</span></span>

<span data-ttu-id="8b994-151">Если ваше приложение также содержит разговорный бот, может потребоваться убедиться, что ваш бот установлен в беседе перед загрузкой модуля задач.</span><span class="sxs-lookup"><span data-stu-id="8b994-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="8b994-152">Это может быть полезно в ситуациях, когда необходимо получить дополнительный контекст для модуля задач.</span><span class="sxs-lookup"><span data-stu-id="8b994-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="8b994-153">Например, может потребоваться получить список для заполнения управления сборщиком людей или список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="8b994-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="8b994-154">Чтобы облегчить этот поток, когда расширение обмена сообщениями сначала получает проверку вызова, чтобы узнать, установлен ли ваш бот `composeExtension/fetchTask` в текущем контексте.</span><span class="sxs-lookup"><span data-stu-id="8b994-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context.</span></span> <span data-ttu-id="8b994-155">Для этого можно выполнить вызов реестра получения, например, если бот не установлен, вы возвращаете адаптивную карту с действием, которое запрашивает у пользователя установку бота См. в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="8b994-155">You could accomplish this by attempting the get roster call, for example, If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="8b994-156">Обратите внимание, что для этого пользователю необходимо иметь разрешение на установку приложений в этом расположении; если они не могут, им будет представлено сообщение с просьбой связаться со своим администратором.</span><span class="sxs-lookup"><span data-stu-id="8b994-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="8b994-157">Вот пример ответа:</span><span class="sxs-lookup"><span data-stu-id="8b994-157">Here's an example of the response:</span></span>

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

<span data-ttu-id="8b994-158">Как только пользователь завершит установку, ваш бот получит еще одно сообщение вызова с `name = composeExtension/submitAction` и `value.data.msteams.justInTimeInstall = true` .</span><span class="sxs-lookup"><span data-stu-id="8b994-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="8b994-159">Вот пример вызова:</span><span class="sxs-lookup"><span data-stu-id="8b994-159">Here's an example of the invoke:</span></span>

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

<span data-ttu-id="8b994-160">Вы должны ответить на этот вызов тем же ответом задачи, на который вы ответили бы, если бы бот уже был установлен.</span><span class="sxs-lookup"><span data-stu-id="8b994-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="8b994-161">Реагирование на отправку</span><span class="sxs-lookup"><span data-stu-id="8b994-161">Responding to submit</span></span>

<span data-ttu-id="8b994-162">После ввода ввода пользователь получит событие с набором командных `composeExtension/submitAction` и параметров.</span><span class="sxs-lookup"><span data-stu-id="8b994-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="8b994-163">Это различные ожидаемые ответы на `submitAction` .</span><span class="sxs-lookup"><span data-stu-id="8b994-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="8b994-164">Ответ модуля задач</span><span class="sxs-lookup"><span data-stu-id="8b994-164">Task Module response</span></span>

<span data-ttu-id="8b994-165">Это используется, когда для получения дополнительных сведений в расширении необходимо цепные диалоги.</span><span class="sxs-lookup"><span data-stu-id="8b994-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="8b994-166">Ответ точно такой же, как `fetchTask` упоминалось ранее.</span><span class="sxs-lookup"><span data-stu-id="8b994-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="8b994-167">Compose extension auth/config response</span><span class="sxs-lookup"><span data-stu-id="8b994-167">Compose extension auth/config response</span></span>

<span data-ttu-id="8b994-168">Это используется, когда для продолжения расширения необходимо либо проверить подлинность, либо настроить.</span><span class="sxs-lookup"><span data-stu-id="8b994-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="8b994-169">Дополнительные сведения см. [в разделе проверка](~/resources/messaging-extension-v3/search-extensions.md#authentication) подлинности в разделе поиск.</span><span class="sxs-lookup"><span data-stu-id="8b994-169">For more information, see [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="8b994-170">Compose extension result response</span><span class="sxs-lookup"><span data-stu-id="8b994-170">Compose extension result response</span></span>

<span data-ttu-id="8b994-171">Это используется для вставки карточки в поле составить в результате команды.</span><span class="sxs-lookup"><span data-stu-id="8b994-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="8b994-172">Это тот же ответ, который используется в команде поиска, но он ограничен одной картой или одним результатом в массиве.</span><span class="sxs-lookup"><span data-stu-id="8b994-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        },
    "attachments": [
      {  
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="8b994-173">Ответьте адаптивным сообщением карточки, отправленным от бота</span><span class="sxs-lookup"><span data-stu-id="8b994-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="8b994-174">Вы также можете ответить на действие отправки, вставив сообщение с адаптивной картой в канал с помощью бота.</span><span class="sxs-lookup"><span data-stu-id="8b994-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="8b994-175">Пользователь сможет предварительно просмотреть сообщение перед отправкой и, возможно, изменить или взаимодействовать с ним.</span><span class="sxs-lookup"><span data-stu-id="8b994-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="8b994-176">Это может быть очень полезно в сценариях, в которых необходимо собрать информацию от пользователей перед созданием адаптивного ответа карты.</span><span class="sxs-lookup"><span data-stu-id="8b994-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="8b994-177">В следующем сценарии показано, как использовать этот поток для настройки опроса без включаемых этапов настройки в сообщение канала.</span><span class="sxs-lookup"><span data-stu-id="8b994-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="8b994-178">Пользователь щелкает расширение обмена сообщениями, чтобы вызвать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="8b994-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="8b994-179">Для настройки опроса пользователь использует модуль задач.</span><span class="sxs-lookup"><span data-stu-id="8b994-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="8b994-180">После отправки модуля задач конфигурации приложение использует сведения, представленные в модуле задач, для изготовления адаптивной карты и отправляет ее в качестве ответа `botMessagePreview` клиенту.</span><span class="sxs-lookup"><span data-stu-id="8b994-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="8b994-181">Пользователь может предварительно просмотреть сообщение адаптивной карты, прежде чем бот вставляет его в канал.</span><span class="sxs-lookup"><span data-stu-id="8b994-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="8b994-182">Если бот еще не является участником канала, щелкнув, `Send` он добавит бота.</span><span class="sxs-lookup"><span data-stu-id="8b994-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="8b994-183">Взаимодействие с адаптивной картой изменит сообщение перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="8b994-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="8b994-184">Как только пользователь `Send` щелкнет, бот будет отправлять сообщение в канал.</span><span class="sxs-lookup"><span data-stu-id="8b994-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="8b994-185">Чтобы включить этот поток, модуль задач должен отвечать, как в приведенной ниже примере, в которой будет представлено сообщение предварительного просмотра пользователю.</span><span class="sxs-lookup"><span data-stu-id="8b994-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="8b994-186">Должен содержать действие с 1 адаптивным `activityPreview` вложением `message` карт.</span><span class="sxs-lookup"><span data-stu-id="8b994-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

```json
{
  "composeExtension": {
    "type": "botMessagePreview",
    "activityPreview": {
      "type": "message",
      "attachments":  [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": << Card Payload >>
        }
      ]
    }
  }
}
```

<span data-ttu-id="8b994-187">Теперь расширению сообщения потребуется ответить на два новых типа взаимодействий и `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="8b994-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="8b994-188">Ниже приведен пример `value` объекта, необходимого для обработки:</span><span class="sxs-lookup"><span data-stu-id="8b994-188">Below is an example of the `value` object you will need to process:</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send" | "edit",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

<span data-ttu-id="8b994-189">При ответе на запрос необходимо ответить с помощью значений, заполняемых сведениями, которые пользователь `edit` `task` уже представил.</span><span class="sxs-lookup"><span data-stu-id="8b994-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="8b994-190">При ответе на запрос необходимо отправить сообщение в канал, содержащий `send` завершенную адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="8b994-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8b994-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8b994-191">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
teamChatConnector.onComposeExtensionSubmitAction((
    event: builder.IEvent,
    request: teamBuilder.IComposeExtensionActionCommandRequest,
    callback: (err: Error, result: any, statusCode: number) => void) => {
        let invokeValue = (<any> event).value;

        if (invokeValue.botMessagePreviewAction ) {
            let attachment = invokeValue.botActivityPreview[0].attachments[0];

            if (invokeValue.botMessagePreviewAction === 'send') {
                let msg = new builder.Message()
                    .address(event.address)
                    .addAttachment(attachment);
                teamChatConnector.send([msg.toMessage()],
                    (error) => {
                        if(error){
                            //TODO: Handle error and callback
                        }
                        else {
                            callback(null, null, 200);
                        }
                    }
                );
            }

            else if (invokeValue.botMessagePreviewAction === 'edit') {
              // Create the card and populate with user-inputted information
              let card = { ... }

              let taskResponse = {
                task: {
                  type: "continue",
                  value: {
                    title: "Card Preview",
                    card: {
                      contentType: 'application/vnd.microsoft.card.adaptive',
                      content: card
                    }
                  }
                }
              }
              callback(null, taskResponse, 200);
            }

        else {
            let attachment = {
                  //create adaptive card
                };
            let activity = new builder.Message().addAttachment(attachment).toMessage();
            let response = teamBuilder.ComposeExtensionResponse.messagePreview()
                .preview(activity)
                .toResponse();
            callback(null, response, 200);
        }
    });
```

# <a name="cnet"></a>[<span data-ttu-id="8b994-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8b994-192">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="8b994-193">В этом примере показан этот поток с помощью [Microsoft.Bot.Connector.Teams SDK (v3).](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="8b994-193">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

```csharp
public class MessagesController : ApiController
{

    [BotAuthentication]
    public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
    {
        MicrosoftAppCredentials.TrustServiceUrl(activity.ServiceUrl, DateTime.MaxValue);
        ConnectorClient connectorClient = new ConnectorClient(
            new Uri(activity.ServiceUrl),
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppIdKey],
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppPasswordKey]);

        if (activity.Type == ActivityTypes.Invoke)
        {
            // Initial task module presented to the user
            if (activity.Name == "composeExtension/fetchTask")
            {
                string task = GetTaskModule();

                return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
            }
            else if (activity.Name == "composeExtension/submitAction")
            {
                dynamic activityValue = JObject.FromObject(activity.Value);
                string botMessagePreviewAction = activityValue["botMessagePreviewAction"];

                //This is the initial card response sent after the task module is submitted
                if (botMessagePreviewAction is null)
                {
                    string text = activityValue.data.cardMessage;

                    AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "This card will be inserted into the conversation by the bot.",
                        Size = AdaptiveTextSize.Large,
                        Wrap = true
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "The text below is what you provided."
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = text,
                    });

                    string cardJson = card.ToJson();

                    string cardMessage = $@"{{
                        'composeExtension': {{
                        'type': 'botMessagePreview',
                        'activityPreview': {{
                            'type': 'message',
                            'attachments': [{{
                                'contentType': 'application/vnd.microsoft.card.adaptive',
                                'content': {cardJson}
                            }}]
                        }}
                        }}
                    }}";

                    JObject res = JObject.Parse(cardMessage);
                    return Request.CreateResponse(HttpStatusCode.OK, res);

                }
                else
                {
                    //This is the "send the card to the channel" event
                    if (botMessagePreviewAction.Equals("send"))
                    {
                        string cardJson = JsonConvert.SerializeObject(activityValue.botActivityPreview[0].attachments[0].content);

                        AdaptiveCardParseResult cardResult = AdaptiveCard.FromJson(cardJson);
                        AdaptiveCard card = cardResult.Card;
                        Attachment cardAttachment = new Attachment
                        {
                            ContentType = AdaptiveCard.ContentType,
                            Content = card
                        };


                        Activity response = activity.CreateReply();
                        response.Attachments.Add(cardAttachment);

                        var result = await connectorClient.Conversations.SendToConversationAsync(response);
                    }
                    //This is fired if the user edits the card before sending it
                    else if (botMessagePreviewAction.Equals("edit"))
                    {
                        string task = GetTaskModule();

                        return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
                    }
                    else
                    {
                        return Request.CreateResponse(HttpStatusCode.NotImplemented);
                    }
                }
            }
        }

        return Request.CreateResponse(HttpStatusCode.NotImplemented);

    }

    private static string GetTaskModule()
    {
        AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Please enter the following information:",
            Size = AdaptiveTextSize.Large
        });
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Card Message:"
        });
        card.Body.Add(new AdaptiveTextInput()
        {
            Id = "cardMessage",
            Spacing = AdaptiveSpacing.None,
            Placeholder = "Card message goes here."
        });
        card.Actions.Add(new AdaptiveSubmitAction()
        {
            Title = "Submit"
        });

        string cardJson = card.ToJson();

        //Create the task module response
        string task = $@"{{
                            'task': {{
                                'type': 'continue',
                                'value': {{
                                    'card': {{
                                        'contentType': 'application/vnd.microsoft.card.adaptive',
                                        'content': {cardJson}
                                        }}
                                    }}
                                }}
                            }}";
        return task;
    }

}
```

## <a name="see-also"></a><span data-ttu-id="8b994-194">См. также</span><span class="sxs-lookup"><span data-stu-id="8b994-194">See also</span></span>

[<span data-ttu-id="8b994-195">Примеры Bot Framework</span><span class="sxs-lookup"><span data-stu-id="8b994-195">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)