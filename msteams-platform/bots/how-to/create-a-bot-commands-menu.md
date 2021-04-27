---
title: Создание меню команд для бота
author: clearab
description: Создание меню команд для бота Microsoft Teams
ms.topic: how-to
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: da87725fca6b4eeacd43f48f6946920251d772e9
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020914"
---
# <a name="bot-command-menus"></a><span data-ttu-id="ef5a3-103">Меню команд бота</span><span class="sxs-lookup"><span data-stu-id="ef5a3-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> <span data-ttu-id="ef5a3-104">Меню бота не отображаются в мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-104">Bot menus do not appear on mobile clients.</span></span>

<span data-ttu-id="ef5a3-105">Чтобы определить набор основных команд, на которые может отвечать бот, можно добавить меню команд со списком команд для бота.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-105">To define a set of core commands that your bot can respond to, you can add a command menu with a drop-down list of commands for your bot.</span></span> <span data-ttu-id="ef5a3-106">Список команд представлен пользователям в области составить сообщение, когда они находятся в беседе с ботом.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-106">The list of commands is presented to the users in the compose message area when they are in conversation with your bot.</span></span> <span data-ttu-id="ef5a3-107">Выберите команду из списка, чтобы вставить строку команды в поле составить сообщение и выбрать **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-107">Select a command from the list to insert the command string into the compose message box and select **Send**.</span></span>

![Меню команд бота](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="ef5a3-109">Создание меню команд для бота</span><span class="sxs-lookup"><span data-stu-id="ef5a3-109">Create a command menu for your bot</span></span>

<span data-ttu-id="ef5a3-110">Меню команд определяется в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-110">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="ef5a3-111">Для их создания можно использовать **App Studio** или вручную добавлять их в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-111">You can either use **App Studio** to create them or add them manually in the app manifest.</span></span>

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="ef5a3-112">Создание командного меню для бота с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="ef5a3-112">Create a command menu for your bot using App Studio</span></span>

<span data-ttu-id="ef5a3-113">Обязательным условием для создания командного меню для бота является то, что необходимо изменить существующий манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-113">A prerequisite to create a command menu for your bot is that you must edit an existing app manifest.</span></span> <span data-ttu-id="ef5a3-114">Действия по добавлению меню команд одинаковы, независимо от того, создаете ли вы новый манифест или редактируете существующий.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-114">The steps to add a command menu are the same, whether you create a new manifest or edit an existing one.</span></span>

<span data-ttu-id="ef5a3-115">**Создание командного меню для бота с помощью App Studio**</span><span class="sxs-lookup"><span data-stu-id="ef5a3-115">**To create a command menu for your bot using App Studio**</span></span>

1. <span data-ttu-id="ef5a3-116">Откройте teams и выберите **Приложения** с левой области.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-116">Open Teams and select **Apps** from the left pane.</span></span> <span data-ttu-id="ef5a3-117">На странице **Приложения** ищите **App Studio** и выберите **Open**.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-117">In the **Apps** page, search for **App Studio**, and select **Open**.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="ef5a3-118">Если у вас нет **App Studio,** вы можете скачать его.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-118">If you do not have **App Studio**, you can download it.</span></span> <span data-ttu-id="ef5a3-119">Дополнительные сведения см. в [записи установки App Studio.](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio)</span><span class="sxs-lookup"><span data-stu-id="ef5a3-119">For more information, see [installing App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).</span></span>

    ![App Studio](./conversations/media/AppStudio.png)

2. <span data-ttu-id="ef5a3-121">В **App Studio** выберите **вкладку Редактор Манифеста.** Если у вас нет существующего пакета приложений, можно создать или импортировать существующее приложение.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-121">In **App Studio**, select the **Manifest editor** tab. If you do not have an existing app package, you can create or import an existing app.</span></span> <span data-ttu-id="ef5a3-122">Дополнительные сведения см. [в обновленном пакете приложений.](~/tutorials/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package)</span><span class="sxs-lookup"><span data-stu-id="ef5a3-122">For more information, see [update an app package](~/tutorials/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package).</span></span>

3. <span data-ttu-id="ef5a3-123">В левой области редактора **Манифеста** и в разделе **Возможности** выберите **Bots**.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-123">In the left pane of the **Manifest editor** and in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="ef5a3-124">В правой области редактора **Манифеста** и в разделе **Команды** выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-124">In the right pane of the **Manifest editor** and in the **Commands** section, select **Add**.</span></span> <span data-ttu-id="ef5a3-125">Появится экран **New Command.**</span><span class="sxs-lookup"><span data-stu-id="ef5a3-125">The **New Command** screen appears.</span></span>

    ![Меню Добавить кнопку Добавить меню App Studio](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="ef5a3-127">Введите **командный текст,** который должен отображаться в качестве командного меню для бота.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-127">Enter the **Command text** that must appear as the command menu for your bot.</span></span>

6. <span data-ttu-id="ef5a3-128">Введите **текст справки,** который должен отображаться в тексте команды в меню.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-128">Enter the **Help text** that must appear under the command text in the menu.</span></span> <span data-ttu-id="ef5a3-129">**Текст справки** должен быть кратким объяснением цели команды.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-129">**Help text** must be a brief explanation of the purpose of the command.</span></span>

7. <span data-ttu-id="ef5a3-130">Выберите **флажки Область,** чтобы выбрать, где должно отображаться это командное меню, и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-130">Select the **Scope** check boxes to select where this command menu must appear, and select **Save**.</span></span>

    ![Кнопка меню меню App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="ef5a3-132">Создание командного меню для бота путем редактирования Manifest.jsна</span><span class="sxs-lookup"><span data-stu-id="ef5a3-132">Create a command menu for your bot by editing Manifest.json</span></span>

<span data-ttu-id="ef5a3-133">Другой способ создания командного меню — это создание его непосредственно в файле манифеста при разработке исходных кодов бота.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-133">Another way to create a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="ef5a3-134">Чтобы использовать этот метод, следуйте следующим пунктам:</span><span class="sxs-lookup"><span data-stu-id="ef5a3-134">To use this method, follow these points:</span></span>

* <span data-ttu-id="ef5a3-135">Каждое меню поддерживает до десяти команд.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-135">Each menu supports up to ten commands.</span></span>
* <span data-ttu-id="ef5a3-136">Создайте одно командное меню, которое работает во всех сферах.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-136">Create a single command menu that works in all scopes.</span></span>
* <span data-ttu-id="ef5a3-137">Создайте другое меню команд для каждой области.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-137">Create a different command menu for each scope.</span></span>

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a><span data-ttu-id="ef5a3-138">Пример манифеста для одного меню для обеих областей</span><span class="sxs-lookup"><span data-stu-id="ef5a3-138">Manifest example for single menu for both scopes</span></span>

<span data-ttu-id="ef5a3-139">Пример кода манифеста для одного меню для обеих областей:</span><span class="sxs-lookup"><span data-stu-id="ef5a3-139">The manifest example code for single menu for both scopes is as follows:</span></span>

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "scopes": [
        "personal",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team",
            "personal"
          ],
          "commands":[
            {
              "title":"Help",
              "description":"Displays this help message"
            },
            {
              "title":"Search Flights",
              "description":"Search flights from Seattle to Phoenix May 2-5 departing after 3pm"
            },
            {
              "title":"Search Hotels",
              "description":"Search hotels in Portland tonight"
            },
            {
              "title":"Best Time to Fly",
              "description":"Best time to fly to London for a 5 day trip this summer"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

#### <a name="manifest-example-for-the-menu-for-each-scope"></a><span data-ttu-id="ef5a3-140">Пример манифеста для меню для каждой области</span><span class="sxs-lookup"><span data-stu-id="ef5a3-140">Manifest example for the menu for each scope</span></span>

<span data-ttu-id="ef5a3-141">Пример кода манифеста для меню для каждой области:</span><span class="sxs-lookup"><span data-stu-id="ef5a3-141">The manifest example code for the menu for each scope is as follows:</span></span>

```json
{
  ...
  "bots":[
    {
      "botId":"<Microsoft app ID for your bot>",
      "scopes": [
        "groupChat",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for channels"
            }
          ]
        },
        {
          "scopes":[
            "groupChat"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for group chat"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

<span data-ttu-id="ef5a3-142">Вы должны обрабатывать команды меню в коде бота при обработке любых сообщений от пользователей.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-142">You must handle menu commands in your bot code as you handle any message from users.</span></span> <span data-ttu-id="ef5a3-143">Вы можете обрабатывать команды меню в коде бота, разобрав часть **\@ упоминания** текста сообщения.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-143">You can handle menu commands in your bot code by parsing out the **\@Mention** portion of the message text.</span></span>

## <a name="handle-menu-commands-in-your-bot-code"></a><span data-ttu-id="ef5a3-144">Обработка команд меню в коде бота</span><span class="sxs-lookup"><span data-stu-id="ef5a3-144">Handle menu commands in your bot code</span></span>

<span data-ttu-id="ef5a3-145">Боты в группе или канале отвечают только тогда, когда они упоминаются `@botname` в сообщении.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-145">Bots in a group or channel respond only when they are mentioned `@botname` in a message.</span></span> <span data-ttu-id="ef5a3-146">Каждое сообщение, полученное ботом, когда в области группы или канала содержит свое имя в возвращаемом тексте сообщения.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-146">Every message received by a bot when in a group or channel scope contains its name in the message text returned.</span></span> <span data-ttu-id="ef5a3-147">Перед обработкой возвращаемой команды необходимо обработать сообщение, полученное ботом с его именем.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-147">Before handling the command being returned, your message parsing must handle the message received by a bot with its name.</span></span>

> [!NOTE]
> <span data-ttu-id="ef5a3-148">Для обработки команд в коде они отправляются вашему боту в качестве регулярного сообщения.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-148">To handle the commands in code, they are sent to your bot as a regular message.</span></span> <span data-ttu-id="ef5a3-149">Вы должны обрабатывать их так же, как и любое другое сообщение от пользователей.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-149">You must handle them as you would handle any other message from your users.</span></span> <span data-ttu-id="ef5a3-150">Команды в коде вставляют предварительно настроенный текст в текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-150">The commands in code insert pre-configured text into the text box.</span></span> <span data-ttu-id="ef5a3-151">Затем пользователь должен отправить этот текст так же, как и любое другое сообщение.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-151">The user must then send that text as they do for any other message.</span></span>

# <a name="c"></a>[<span data-ttu-id="ef5a3-152">C#</span><span class="sxs-lookup"><span data-stu-id="ef5a3-152">C#</span></span>](#tab/dotnet)

<span data-ttu-id="ef5a3-153">Вы можете разобрать часть **\@ Упоминания** текста сообщения с помощью статического метода, предоставленного Microsoft Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-153">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework.</span></span> <span data-ttu-id="ef5a3-154">Это метод класса `Activity` с именем `RemoveRecipientMention` .</span><span class="sxs-lookup"><span data-stu-id="ef5a3-154">It is a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

<span data-ttu-id="ef5a3-155">Код C# для размывки части **\@ Упоминания** текста сообщения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ef5a3-155">The C# code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[<span data-ttu-id="ef5a3-156">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ef5a3-156">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="ef5a3-157">Вы можете разсмеять часть **\@ Упоминания** текста сообщения с помощью статического метода, предоставленного с помощью Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-157">You can parse out the **\@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="ef5a3-158">Это метод класса `TurnContext` с именем `removeMentionText` .</span><span class="sxs-lookup"><span data-stu-id="ef5a3-158">It is a method of the `TurnContext` class named `removeMentionText`.</span></span>

<span data-ttu-id="ef5a3-159">Код JavaScript для размыва части **\@ Упоминания** текста сообщения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ef5a3-159">The JavaScript code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[<span data-ttu-id="ef5a3-160">Python</span><span class="sxs-lookup"><span data-stu-id="ef5a3-160">Python</span></span>](#tab/python)

<span data-ttu-id="ef5a3-161">Вы можете разобрать  @Mention текст сообщения с помощью статического метода, предоставленного с помощью Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-161">You can parse out the **@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="ef5a3-162">Это метод класса `TurnContext` с именем `remove_recipient_mention` .</span><span class="sxs-lookup"><span data-stu-id="ef5a3-162">It is a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

<span data-ttu-id="ef5a3-163">Код Python для размывки части **\@ Упоминания** текста сообщения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ef5a3-163">The Python code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

<span data-ttu-id="ef5a3-164">Чтобы обеспечить бесперебойную работу кода бота, необходимо придерживаться нескольких методов.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-164">To enable smooth functioning of your bot code, there are few best practices that you must follow.</span></span>

## <a name="command-menu-best-practices"></a><span data-ttu-id="ef5a3-165">Лучшие практики меню команд</span><span class="sxs-lookup"><span data-stu-id="ef5a3-165">Command menu best practices</span></span>

<span data-ttu-id="ef5a3-166">Ниже ниже ниже приводится пример лучших практик меню команд:</span><span class="sxs-lookup"><span data-stu-id="ef5a3-166">Following are the command menu best practices:</span></span>

* <span data-ttu-id="ef5a3-167">Сохраняйте простое: меню бота предназначено для того, чтобы представить основные возможности вашего бота.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-167">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="ef5a3-168">Кратко: параметры меню не должны быть длинными и не должны быть сложными естественными языковыми утверждениями.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-168">Keep it short: Menu options must not be long and must not be complex natural language statements.</span></span> <span data-ttu-id="ef5a3-169">Они должны быть простыми командами.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-169">They must be simple commands.</span></span>
* <span data-ttu-id="ef5a3-170">Сохраняйте его на словах: действия или команды меню бота всегда должны быть доступны, независимо от состояния беседы или диалоговом окне, в который находится бот.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-170">Keep it invokable: Bot menu actions or commands must always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>

> [!NOTE]
> <span data-ttu-id="ef5a3-171">Если вы удалите какие-либо команды из манифеста, необходимо изменить приложение для реализации изменений.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-171">If you remove any commands from your manifest, you must redeploy your app to implement the changes.</span></span> <span data-ttu-id="ef5a3-172">Как правило, любые изменения манифеста требуют переделок вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ef5a3-172">In general, any changes to the manifest require you to redeploy your app.</span></span>

## <a name="next-step"></a><span data-ttu-id="ef5a3-173">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="ef5a3-173">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ef5a3-174">Канал и групповые разговоры</span><span class="sxs-lookup"><span data-stu-id="ef5a3-174">Channel and group conversations</span></span>](~/bots/how-to/conversations/channel-and-group-conversations.md)
