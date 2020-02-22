---
title: Запуск действий с расширениями обмена сообщениями
description: Создайте расширения для обмена сообщениями на основе действий, чтобы разрешить пользователям запускать внешние службы.
keywords: службы расширения обмена сообщениями Teams.
ms.openlocfilehash: 1a38b4f7bfb413defd28950ca9b97f7411cf9c09
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228033"
---
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="24968-104">Запуск действий с расширениями обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="24968-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="24968-105">Расширения обмена сообщениями на основе действий позволяют пользователям активировать действия во внешних службах в Teams.</span><span class="sxs-lookup"><span data-stu-id="24968-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![Пример карточки расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="24968-107">В следующих разделах описано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="24968-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="24968-108">Расширения сообщений для типов действий</span><span class="sxs-lookup"><span data-stu-id="24968-108">Action type message extensions</span></span>

<span data-ttu-id="24968-109">Чтобы инициировать действия из расширения обмена сообщениями, `type` задайте для `action`параметра значение.</span><span class="sxs-lookup"><span data-stu-id="24968-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="24968-110">Ниже приведен пример манифеста с командой поиска и созданием.</span><span class="sxs-lookup"><span data-stu-id="24968-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="24968-111">Одно расширение системы обмена сообщениями может содержать до 10 разных команд.</span><span class="sxs-lookup"><span data-stu-id="24968-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="24968-112">Сюда могут входить как несколько команд поиска, так и несколько команд, основанных на действиях.</span><span class="sxs-lookup"><span data-stu-id="24968-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="24968-113">Пример полного манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="24968-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="24968-114">Инициация действий из сообщений</span><span class="sxs-lookup"><span data-stu-id="24968-114">Initiate actions from messages</span></span>

<span data-ttu-id="24968-115">Кроме запуска действий из области создание сообщения, можно также использовать расширение системы обмена сообщениями, чтобы инициировать действие из сообщения.</span><span class="sxs-lookup"><span data-stu-id="24968-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="24968-116">Это позволит отправить содержимое сообщения в Bot для обработки и при необходимости ответить на это сообщение с помощью метода, описанного при ответе [на отправку](#responding-to-submit).</span><span class="sxs-lookup"><span data-stu-id="24968-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="24968-117">Ответ будет вставлен в ответ на сообщение, которое пользователи могут изменить перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="24968-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="24968-118">Пользователи могут получить доступ к своему расширению обмена сообщениями из меню переполнения `...` , а затем выбрать `Take action` , как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="24968-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the image below.</span></span>

![Пример инициирования действия из сообщения](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="24968-120">Чтобы ваше расширение обмена сообщениями работало из сообщения, необходимо добавить `context` параметр в `commands` объект расширения обмена сообщениями в манифесте приложения, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="24968-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="24968-121">Допустимые строки для `context` массива: `"message"`, `"commandBox"`и `"compose"`.</span><span class="sxs-lookup"><span data-stu-id="24968-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="24968-122">Значение по умолчанию — `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="24968-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="24968-123">Для получения подробных сведений о `context` параметре обратитесь к разделу [define Commands](#define-commands) .</span><span class="sxs-lookup"><span data-stu-id="24968-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

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

<span data-ttu-id="24968-124">Ниже приведен пример `value` объекта, содержащего сведения о сообщении, которое будет отправлено в качестве части `composeExtension` запроса, отправляемого на сервер робота.</span><span class="sxs-lookup"><span data-stu-id="24968-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

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

### <a name="test-via-uploading"></a><span data-ttu-id="24968-125">Тестирование через отправку</span><span class="sxs-lookup"><span data-stu-id="24968-125">Test via uploading</span></span>

<span data-ttu-id="24968-126">Вы можете проверить расширение системы обмена сообщениями, отправив свое приложение.</span><span class="sxs-lookup"><span data-stu-id="24968-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="24968-127">Сведения о [том, как загрузить ваше приложение в группу,](~/concepts/deploy-and-publish/apps-upload.md) можно найти в разделе.</span><span class="sxs-lookup"><span data-stu-id="24968-127">See [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md) for details.</span></span>

<span data-ttu-id="24968-128">Чтобы открыть расширение системы обмена сообщениями, перейдите к любому из бесед или каналов.</span><span class="sxs-lookup"><span data-stu-id="24968-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="24968-129">Нажмите кнопку **Дополнительные параметры** (**&#8943;**) в поле создать и выберите ваш добавочный номер для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="24968-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="24968-130">Сбор данных, вводимых пользователями</span><span class="sxs-lookup"><span data-stu-id="24968-130">Collecting input from users</span></span>

<span data-ttu-id="24968-131">Существует три способа сбора информации от конечного пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="24968-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="24968-132">Список статических параметров</span><span class="sxs-lookup"><span data-stu-id="24968-132">Static parameter list</span></span>

<span data-ttu-id="24968-133">В этом методе необходимо только определить статический список параметров в манифесте, как показано выше в команде "создать".</span><span class="sxs-lookup"><span data-stu-id="24968-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="24968-134">Чтобы использовать этот метод, `fetchTask` убедитесь, что `false` в манифесте заданы и определены параметры.</span><span class="sxs-lookup"><span data-stu-id="24968-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="24968-135">Когда пользователь выбирает команду с помощью статических параметров, Teams создаст форму в модуле задач с параметрами, определенными в манифесте.</span><span class="sxs-lookup"><span data-stu-id="24968-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="24968-136">При нажатии на `composeExtension/submitAction` команду Отправить сообщение a отправляется в Bot.</span><span class="sxs-lookup"><span data-stu-id="24968-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="24968-137">В разделе [ответ на отправляются](#responding-to-submit) дополнительные сведения о ожидаемом наборе ответов.</span><span class="sxs-lookup"><span data-stu-id="24968-137">See the topic [Responding to submit](#responding-to-submit) for more information on the expected set of responses.</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="24968-138">Динамическое входное значение с использованием адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="24968-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="24968-139">В этом методе служба может определить настраиваемую адаптивную карточку для сбора данных, вводимых пользователем.</span><span class="sxs-lookup"><span data-stu-id="24968-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="24968-140">Для этого подхода задайте для `fetchTask` `true` параметра значение в манифесте.</span><span class="sxs-lookup"><span data-stu-id="24968-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="24968-141">Обратите внимание, что `fetchTask` если `true` вы задаете любые статические параметры, определенные для команды, будут игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="24968-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="24968-142">В этом методе служба будет получать `composeExtension/fetchTask` событие и реагировать на [отклики](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)от функции адаптивного модуля задач на основе карты.</span><span class="sxs-lookup"><span data-stu-id="24968-142">In this method your service will receive a `composeExtension/fetchTask` event and needs to respond with an adaptive card based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="24968-143">Ниже приведен пример ответа с помощью адаптивной карточки:</span><span class="sxs-lookup"><span data-stu-id="24968-143">Below is an sample response with an adaptive card:</span></span>

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

<span data-ttu-id="24968-144">Bot также может отвечать с ответом на запрос проверки подлинности и конфигурации, если пользователю необходимо проверить подлинность или настроить расширение перед тем, как получить входные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="24968-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="24968-145">Динамическое входное значение с использованием веб-представления</span><span class="sxs-lookup"><span data-stu-id="24968-145">Dynamic input using a web view</span></span>

<span data-ttu-id="24968-146">В этом методе служба может показать `<iframe>` мини-приложение для отображения любого НАСТРАИВАЕМОГО пользовательского интерфейса и сбора вводимых пользователем данных.</span><span class="sxs-lookup"><span data-stu-id="24968-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="24968-147">Для этого подхода задайте для `fetchTask` `true` параметра значение в манифесте.</span><span class="sxs-lookup"><span data-stu-id="24968-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="24968-148">Как и в случае с адаптивным продвижением карт, ваша `fetchTask` служба отправляет событие и требует [ответа на модуль задачи](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)на основе URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="24968-148">Just like in the adaptive card flow your service will be send a `fetchTask` event and needs to respond with a URL based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="24968-149">Ниже приведен пример ответа с помощью адаптивной карточки:</span><span class="sxs-lookup"><span data-stu-id="24968-149">Below is an sample response with an Adaptive card:</span></span>

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="24968-150">Запрос на установку программы "bot" для беседы</span><span class="sxs-lookup"><span data-stu-id="24968-150">Request to install your conversational bot</span></span>

<span data-ttu-id="24968-151">Если ваше приложение также содержит объект Bot для общения, возможно, перед загрузкой модуля задачи необходимо убедиться, что в беседе установлен почтовый робот.</span><span class="sxs-lookup"><span data-stu-id="24968-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="24968-152">Это может быть удобно в тех случаях, когда требуется получить дополнительный контекст для модуля задач.</span><span class="sxs-lookup"><span data-stu-id="24968-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="24968-153">Например, может потребоваться получить список для заполнения элемента управления "Выбор людей" или список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="24968-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="24968-154">Для упрощения этого процесса, когда расширение системы обмена сообщениями `composeExtension/fetchTask` сначала получает запрос на вызов, чтобы проверить, установлен ли ваш Bot в текущем контексте (например, вы можете сделать это с помощью попытки получения списка, например).</span><span class="sxs-lookup"><span data-stu-id="24968-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context (you could accomplish this by attempting the get roster call, for example).</span></span> <span data-ttu-id="24968-155">Если сервер-робот не установлен, вы возвращаете адаптивную карту с действием, которое запрашивает у пользователя установку ленты, в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="24968-155">If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="24968-156">Обратите внимание, что для этого необходимо, чтобы у пользователя было разрешение на установку приложений в этом расположении; Если они не смогут получить сообщение, попросите их обратиться к администратору.</span><span class="sxs-lookup"><span data-stu-id="24968-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="24968-157">Ниже приведен пример ответа.</span><span class="sxs-lookup"><span data-stu-id="24968-157">Here's an example of the response:</span></span>

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

<span data-ttu-id="24968-158">Когда пользователь завершит установку, ваш робот получит еще одно сообщение Invoke с `name = composeExtension/submitAction`, и. `value.data.msteams.justInTimeInstall = true`</span><span class="sxs-lookup"><span data-stu-id="24968-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="24968-159">Ниже приведен пример вызова:</span><span class="sxs-lookup"><span data-stu-id="24968-159">Here's an example of the invoke:</span></span>

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

<span data-ttu-id="24968-160">Вы должны ответить на этот вызов с тем же ответом задачи, на который вы ответили, если он уже установлен.</span><span class="sxs-lookup"><span data-stu-id="24968-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="24968-161">Ответ на отправляют</span><span class="sxs-lookup"><span data-stu-id="24968-161">Responding to submit</span></span>

<span data-ttu-id="24968-162">После того как пользователь завершит ввод данных, пользователь Bot получит `composeExtension/submitAction` событие с идентификатором команды и значением параметра.</span><span class="sxs-lookup"><span data-stu-id="24968-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="24968-163">Это различные ожидаемые ответы на `submitAction`.</span><span class="sxs-lookup"><span data-stu-id="24968-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="24968-164">Отклик модуля задачи</span><span class="sxs-lookup"><span data-stu-id="24968-164">Task Module response</span></span>

<span data-ttu-id="24968-165">Он используется, когда расширение должно повязать диалоговые окна для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="24968-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="24968-166">Ответ точно такой же, как `fetchTask` и упоминалось ранее.</span><span class="sxs-lookup"><span data-stu-id="24968-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="24968-167">Ответ на запрос проверки подлинности и настройки расширения</span><span class="sxs-lookup"><span data-stu-id="24968-167">Compose extension auth/config response</span></span>

<span data-ttu-id="24968-168">Этот параметр используется, если для продолжения расширения требуется проверка подлинности или Настройка.</span><span class="sxs-lookup"><span data-stu-id="24968-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="24968-169">Дополнительные сведения см. в [разделе "Проверка подлинности](~/resources/messaging-extension-v3/search-extensions.md#authentication) " в разделе "Поиск".</span><span class="sxs-lookup"><span data-stu-id="24968-169">See [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section for more details.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="24968-170">Ответ на результат расширения создания</span><span class="sxs-lookup"><span data-stu-id="24968-170">Compose extension result response</span></span>

<span data-ttu-id="24968-171">Используется для вставки карточки в поле создание в результате выполнения команды.</span><span class="sxs-lookup"><span data-stu-id="24968-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="24968-172">Это тот же ответ, который используется в команде поиска, но он ограничен одной картой или одним результатом в массиве.</span><span class="sxs-lookup"><span data-stu-id="24968-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

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
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="24968-173">Ответ с сообщением адаптивной карточки, отправленной с ленты</span><span class="sxs-lookup"><span data-stu-id="24968-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="24968-174">Вы также можете ответить на действие Отправить, вставив сообщение с адаптивной картой в канал с помощью ленты.</span><span class="sxs-lookup"><span data-stu-id="24968-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="24968-175">Пользователь сможет просмотреть сообщение перед его отправкой и потенциально редактировать/взаимодействовать с ним.</span><span class="sxs-lookup"><span data-stu-id="24968-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="24968-176">Это может быть очень удобно в сценариях, в которых необходимо собрать информацию от пользователей, прежде чем создавать адаптивный ответ карты.</span><span class="sxs-lookup"><span data-stu-id="24968-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="24968-177">В приведенном ниже сценарии показано, как можно использовать этот процесс для настройки опроса без включения действий по настройке в сообщение канала.</span><span class="sxs-lookup"><span data-stu-id="24968-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="24968-178">Пользователь выбирает расширение системы обмена сообщениями для запуска модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="24968-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="24968-179">Пользователь использует модуль задач для настройки опроса.</span><span class="sxs-lookup"><span data-stu-id="24968-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="24968-180">После отправки модуля задач конфигурации приложение использует сведения, представленные в модуле задачи, для создания адаптивной карточки и отправки ее в качестве `botMessagePreview` ответа клиенту.</span><span class="sxs-lookup"><span data-stu-id="24968-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="24968-181">После этого пользователь может просмотреть сообщение адаптивной карточки, прежде чем Bot вставит его в канал.</span><span class="sxs-lookup"><span data-stu-id="24968-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="24968-182">Если Bot еще не является участником канала, щелчок `Send` добавит элемент Bot.</span><span class="sxs-lookup"><span data-stu-id="24968-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="24968-183">При взаимодействии с адаптивной картой изменится сообщение перед его отправкой.</span><span class="sxs-lookup"><span data-stu-id="24968-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="24968-184">После того, как `Send` пользователь нажмет на Bot, в канал будет отправлено сообщение.</span><span class="sxs-lookup"><span data-stu-id="24968-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="24968-185">Чтобы включить этот рабочий процесс, модуль задачи должен отвечать, как показано в примере ниже, который будет предоставлять пользователю сообщение о предварительном просмотре.</span><span class="sxs-lookup"><span data-stu-id="24968-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="24968-186">`activityPreview` Должен содержать `message` действие с ровно 1 вложенной картой.</span><span class="sxs-lookup"><span data-stu-id="24968-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

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

<span data-ttu-id="24968-187">Теперь для расширения сообщения необходимо ответить на два новых типа взаимодействия `value.botMessagePreviewAction = "send"` и. `value.botMessagePreviewAction = "edit"`</span><span class="sxs-lookup"><span data-stu-id="24968-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="24968-188">Ниже приведен пример `value` объекта, который необходимо обработать:</span><span class="sxs-lookup"><span data-stu-id="24968-188">Below is an example of the `value` object you will need to process:</span></span>

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

<span data-ttu-id="24968-189">При ответе на `edit` запрос необходимо ответить на `task` отклик со значениями, заполненными данными, которые уже были отправлены пользователем.</span><span class="sxs-lookup"><span data-stu-id="24968-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="24968-190">При ответе на `send` запрос необходимо отправить сообщение каналу, содержащему завершенную адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="24968-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejs"></a>[<span data-ttu-id="24968-191">TypeScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="24968-191">TypeScript/Node.js</span></span>](#tab/typescript)

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

<span data-ttu-id="24968-192">В этой статье *также приведены* [примеры кода Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="24968-192">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="24968-193">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="24968-193">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="24968-194">В этом примере показан этот процесс с помощью [пакета SDK Microsoft. Bot. Connector. Teams (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span><span class="sxs-lookup"><span data-stu-id="24968-194">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

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
