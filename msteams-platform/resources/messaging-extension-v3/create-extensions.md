---
title: Инициировать действия с расширением обмена сообщениями
description: Создание расширений обмена сообщениями на основе действий, чтобы позволить пользователям вызывать внешние службы
localization_priority: Normal
ms.topic: how-to
keywords: команды обмена сообщениями расширения обмена сообщениями поиск
ms.openlocfilehash: bfb3295726c355164f080c15e3759ea36a99d914
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566742"
---
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="4d7c3-104">Инициировать действия с расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4d7c3-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="4d7c3-105">Расширения обмена сообщениями на основе действий позволяют пользователям инициировать действия во внешних службах, находясь внутри Teams.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![Пример карты расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="4d7c3-107">Следующие разделы описывают, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="4d7c3-108">Расширения сообщений типа действия</span><span class="sxs-lookup"><span data-stu-id="4d7c3-108">Action type message extensions</span></span>

<span data-ttu-id="4d7c3-109">Для инициирования действий от расширения обмена сообщениями `type` установите параметр `action` на .</span><span class="sxs-lookup"><span data-stu-id="4d7c3-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="4d7c3-110">Ниже приведен пример манифеста с поиском и командой создания.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="4d7c3-111">Одно расширение обмена сообщениями может иметь до 10 различных команд.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="4d7c3-112">Это может включать в себя как несколько поисковых запросов, так и несколько команд на основе действий.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="4d7c3-113">Полный пример манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="4d7c3-113">Complete app manifest example</span></span>

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

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="4d7c3-114">Инициировать действия из сообщений</span><span class="sxs-lookup"><span data-stu-id="4d7c3-114">Initiate actions from messages</span></span>

<span data-ttu-id="4d7c3-115">В дополнение к инициированию действий из области композиции сообщений, вы также можете использовать расширение обмена сообщениями для инициирования действия из сообщения.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="4d7c3-116">Это позволит вам отправить содержимое сообщения вашему боту для обработки, и дополнительно ответить на это сообщение с ответом с помощью [метода, описанного в Ответ представить](#responding-to-submit).</span><span class="sxs-lookup"><span data-stu-id="4d7c3-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="4d7c3-117">Ответ будет вставлен в ответ на сообщение, которое пользователи могут редактировать перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="4d7c3-118">Пользователи могут получить доступ к расширению обмена сообщениями из меню `...` переполнения, а затем выбрать `Take action` как на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="4d7c3-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the following image:</span></span>

![Пример инициирования действия из сообщения](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="4d7c3-120">Чтобы расширение обмена сообщениями работало из сообщения, необходимо добавить параметр к объекту расширения обмена сообщениями в `context` приложении, как это имеет место в `commands` приведенной ниже примере.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="4d7c3-121">Действительные строки для `context` `"message"` массива, `"commandBox"` и `"compose"` .</span><span class="sxs-lookup"><span data-stu-id="4d7c3-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="4d7c3-122">Значение по умолчанию — `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="4d7c3-123">Для получения [подробной информации](#define-commands) о параметре можно посмотреть раздел «Определить `context` команды».</span><span class="sxs-lookup"><span data-stu-id="4d7c3-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

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

<span data-ttu-id="4d7c3-124">Ниже приведен пример объекта, содержащего `value` сведения о сообщении, которые будут отправлены в рамках `composeExtension` запроса, отправленного вашему боту.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

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

### <a name="test-via-uploading"></a><span data-ttu-id="4d7c3-125">Тест через загрузку</span><span class="sxs-lookup"><span data-stu-id="4d7c3-125">Test via uploading</span></span>

<span data-ttu-id="4d7c3-126">Вы можете протестировать расширение обмена сообщениями, загрузив приложение.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="4d7c3-127">Для получения дополнительной [информации см.](~/concepts/deploy-and-publish/apps-upload.md)</span><span class="sxs-lookup"><span data-stu-id="4d7c3-127">For more information, see [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md).</span></span>

<span data-ttu-id="4d7c3-128">Чтобы открыть расширение обмена сообщениями, перейдите на любой из ваших чатов или каналов.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="4d7c3-129">Выберите **кнопку «Больше** **&#8943;»**(подробнее) в поле для составления и выберите расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="4d7c3-130">Сбор входных данных от пользователей</span><span class="sxs-lookup"><span data-stu-id="4d7c3-130">Collecting input from users</span></span>

<span data-ttu-id="4d7c3-131">Существует три способа сбора информации от конечному пользователю в Teams.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="4d7c3-132">Статический список параметров</span><span class="sxs-lookup"><span data-stu-id="4d7c3-132">Static parameter list</span></span>

<span data-ttu-id="4d7c3-133">В этом методе все, что вам нужно сделать, это определить статический список параметров в манифесте, как показано выше в команде "Создать To Do" .</span><span class="sxs-lookup"><span data-stu-id="4d7c3-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="4d7c3-134">Для использования этого метода `fetchTask` убедитесь, установлен `false` и что вы определяете параметры в манифесте.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="4d7c3-135">Когда пользователь выбирает команду со статическими параметрами, Teams будет генерировать форму в модуле задач с параметрами, определенными в манифесте.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="4d7c3-136">При ударе Отправить `composeExtension/submitAction` отправляется бот.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="4d7c3-137">Для получения дополнительной информации об ожидаемом наборе ответов [см.](#responding-to-submit)</span><span class="sxs-lookup"><span data-stu-id="4d7c3-137">For more information on the expected set of responses, see [Responding to submit](#responding-to-submit).</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="4d7c3-138">Динамический ввод с помощью адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="4d7c3-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="4d7c3-139">В этом методе служба может определить пользовательскую адаптивную карту для сбора пользовательского ввода.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="4d7c3-140">Для этого подхода установите `fetchTask` параметр в `true` манифесте.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="4d7c3-141">Обратите внимание, что при `fetchTask` наборе `true` каких-либо статических параметров, определенных для команды, будет проигнорировано.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="4d7c3-142">В этом методе ваш сервис получит событие `composeExtension/fetchTask` и должен ответить с адаптивной картой на основе [ответа модуля задач.](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="4d7c3-142">In this method your service will receive a `composeExtension/fetchTask` event and needs to respond with an adaptive card based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="4d7c3-143">Ниже приводится пример ответа с адаптивной картой:</span><span class="sxs-lookup"><span data-stu-id="4d7c3-143">Following is a sample response with an adaptive card:</span></span>

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

<span data-ttu-id="4d7c3-144">Бот также может ответить ответом auth/config, если пользователю необходимо проверить подлинность или настроить расширение перед вводом пользователя.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="4d7c3-145">Динамический ввод с помощью веб-представления</span><span class="sxs-lookup"><span data-stu-id="4d7c3-145">Dynamic input using a web view</span></span>

<span data-ttu-id="4d7c3-146">В этом методе служба может показать виджет на `<iframe>` основе, чтобы показать любой пользовательский интерфейс и собрать пользовательский ввод.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="4d7c3-147">Для этого подхода установите `fetchTask` параметр в `true` манифесте.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="4d7c3-148">Так же, как в адаптивном потоке карт ваша служба будет отправлять `fetchTask` события и должен ответить с URL-адресом на [основе ответа модуля задач.](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="4d7c3-148">Just like in the adaptive card flow your service will be send a `fetchTask` event and needs to respond with a URL based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="4d7c3-149">Ниже приводится пример ответа с адаптивной картой:</span><span class="sxs-lookup"><span data-stu-id="4d7c3-149">Following is a sample response with an Adaptive card:</span></span>

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="4d7c3-150">Запрос на установку разговорного бота</span><span class="sxs-lookup"><span data-stu-id="4d7c3-150">Request to install your conversational bot</span></span>

<span data-ttu-id="4d7c3-151">Если ваше приложение также содержит разговорного бота, может потребоваться убедиться, что ваш бот установлен в разговоре перед загрузкой модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="4d7c3-152">Это может быть полезно в ситуациях, когда вам нужно получить дополнительный контекст для вас модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="4d7c3-153">Например, может потребоваться взять с 1900 человек список для заполнения управления сборщиками данных или список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="4d7c3-154">Чтобы облегчить этот поток, когда расширение обмена сообщениями сначала получает `composeExtension/fetchTask` проверку вызова, чтобы увидеть, если ваш бот установлен в текущем контексте.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context.</span></span> <span data-ttu-id="4d7c3-155">Вы можете сделать это, пытаясь получить список вызова, например, Если ваш бот не установлен, вы возвращаете адаптивную карту с действием, которое просит пользователя установить ваш бот Смотрите пример ниже.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-155">You could accomplish this by attempting the get roster call, for example, If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="4d7c3-156">Обратите внимание, что для этого требуется разрешение пользователя на установку приложений в этом месте; если они не могут, им будет представлено сообщение с просьбой связаться с администратором.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="4d7c3-157">Вот пример ответа:</span><span class="sxs-lookup"><span data-stu-id="4d7c3-157">Here's an example of the response:</span></span>

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

<span data-ttu-id="4d7c3-158">Как только пользователь завершит установку, ваш бот получит еще одно сообщение вызова `name = composeExtension/submitAction` с , и `value.data.msteams.justInTimeInstall = true` .</span><span class="sxs-lookup"><span data-stu-id="4d7c3-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="4d7c3-159">Вот пример вызова:</span><span class="sxs-lookup"><span data-stu-id="4d7c3-159">Here's an example of the invoke:</span></span>

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

<span data-ttu-id="4d7c3-160">Вы должны ответить на этот вызов с той же задачей ответ вы бы ответили, если бот был уже установлен.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="4d7c3-161">Ответ на отправку</span><span class="sxs-lookup"><span data-stu-id="4d7c3-161">Responding to submit</span></span>

<span data-ttu-id="4d7c3-162">Как только пользователь завершает ввод ввода, бот получит событие с `composeExtension/submitAction` идентификатором команды и набором значений параметров.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="4d7c3-163">Это различные ожидаемые ответы на `submitAction` .</span><span class="sxs-lookup"><span data-stu-id="4d7c3-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="4d7c3-164">Ответ на модуль задач</span><span class="sxs-lookup"><span data-stu-id="4d7c3-164">Task Module response</span></span>

<span data-ttu-id="4d7c3-165">Это используется, когда расширение необходимо цепочки диалоги вместе, чтобы получить больше информации.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="4d7c3-166">Ответ точно такой же, как упоминалось `fetchTask` ранее.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="4d7c3-167">Составьте расширение auth/config ответ</span><span class="sxs-lookup"><span data-stu-id="4d7c3-167">Compose extension auth/config response</span></span>

<span data-ttu-id="4d7c3-168">Это используется, когда расширение необходимо либо проверить подлинность, либо настроить для продолжения.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="4d7c3-169">Для получения дополнительной информации [смотрите раздел аутентификации](~/resources/messaging-extension-v3/search-extensions.md#authentication) в разделе поиска.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-169">For more information, see [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="4d7c3-170">Составьте ответ на результат расширения</span><span class="sxs-lookup"><span data-stu-id="4d7c3-170">Compose extension result response</span></span>

<span data-ttu-id="4d7c3-171">Это используется для вставки карты в поле compose в результате команды.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="4d7c3-172">Это тот же ответ, который используется в команде поиска, но он ограничен одной картой или одним результатом в массиве.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="4d7c3-173">Ответить с адаптивной картой сообщение, отправленное от бота</span><span class="sxs-lookup"><span data-stu-id="4d7c3-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="4d7c3-174">Вы также можете ответить на отправку действий, вставив сообщение с адаптивной картой в канал с ботом.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="4d7c3-175">Пользователь сможет просмотреть сообщение перед отправкой, а также, возможно, редактировать/взаимодействовать с ним.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="4d7c3-176">Это может быть очень полезно в сценариях, где вам нужно собрать информацию от пользователей, прежде чем создавать адаптивный ответ карты.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="4d7c3-177">В следующем сценарии показано, как можно использовать этот поток для настройки опроса без включения шагов конфигурации в сообщение канала.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="4d7c3-178">Пользователь нажимает на расширение обмена сообщениями, чтобы вызвать модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="4d7c3-179">Пользователь использует модуль задач для настройки опроса.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="4d7c3-180">После отправки модуля задачи конфигурации приложение использует информацию, представленную в модуле задачи, для создания адаптивной карты и `botMessagePreview` отправляет ее в качестве ответа клиенту.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="4d7c3-181">Пользователь может просмотреть адаптивное сообщение карты, прежде чем бот вставить его в канал.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="4d7c3-182">Если бот еще не является членом канала, `Send` нажав будет добавить бота.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="4d7c3-183">Взаимодействие с адаптивной картой изменит сообщение перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="4d7c3-184">После того, как `Send` пользователь нажимает бот будет размещать сообщение на канале.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="4d7c3-185">Для обеспечения этого потока модуль задачи должен отвечать, как в приведеном ниже примере, который представит предварительное сообщение пользователю.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="4d7c3-186">Необходимо `activityPreview` содержать действие с `message` помощью ровно 1 адаптивного вложения карты.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

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

<span data-ttu-id="4d7c3-187">Теперь расширение сообщения должно будет реагировать на два новых типа взаимодействий `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"` и.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="4d7c3-188">Ниже приведен пример `value` объекта, который необходимо обработать:</span><span class="sxs-lookup"><span data-stu-id="4d7c3-188">Below is an example of the `value` object you will need to process:</span></span>

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

<span data-ttu-id="4d7c3-189">При ответе на `edit` запрос вы должны ответить с `task` значениями, населенными информацией, которую пользователь уже представил.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="4d7c3-190">При ответе на запрос `send` следует отправить сообщение каналу, содержащее доработанную адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="4d7c3-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejs"></a>[<span data-ttu-id="4d7c3-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="4d7c3-191">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="cnet"></a>[<span data-ttu-id="4d7c3-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="4d7c3-192">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="4d7c3-193">Этот пример показывает этот поток с [помощью Microsoft.Bot.Connector.Teams SDK (v3).](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="4d7c3-193">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

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

## <a name="see-also"></a><span data-ttu-id="4d7c3-194">См. также</span><span class="sxs-lookup"><span data-stu-id="4d7c3-194">See also</span></span>

[<span data-ttu-id="4d7c3-195">Образцы Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4d7c3-195">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)