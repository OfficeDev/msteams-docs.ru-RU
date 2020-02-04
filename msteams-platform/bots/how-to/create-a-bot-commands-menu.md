---
title: Создание командного меню для ленты
author: clearab
description: Создание командного меню для ленты Microsoft Teams
ms.topic: overview, command menu
ms.author: anclear
ms.openlocfilehash: 81efb94fc882aa4653ab162863d5d973aeae87b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675307"
---
# <a name="bot-command-menus"></a><span data-ttu-id="221a6-103">Меню команд Bot</span><span class="sxs-lookup"><span data-stu-id="221a6-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> <span data-ttu-id="221a6-104">Меню ленты не отображаются на мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="221a6-104">Bot menus won't appear on mobile clients.</span></span>

<span data-ttu-id="221a6-105">Команда добавить меню для ленты позволяет определить набор основных команд, на которые пользователь Bot всегда может отвечать.</span><span class="sxs-lookup"><span data-stu-id="221a6-105">Add command menu for your bot allows you to define a set of core commands your bot can always respond to.</span></span> <span data-ttu-id="221a6-106">Список команд предоставляется пользователю, расположенному над областью создание сообщения, при их взаимосравнении с Bot.</span><span class="sxs-lookup"><span data-stu-id="221a6-106">The list of commands is presented to the user above the compose message area when they are conversing with your bot.</span></span> <span data-ttu-id="221a6-107">При выборе команды из списка в поле создать сообщение будет вставлена Командная строка, тогда все пользователи должны выполнить команду **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="221a6-107">Selecting a command from the list will insert the command string into the compose message box, then all users need to do is select **Send**.</span></span>

![Меню команд Bot](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="221a6-109">Создание командного меню для ленты</span><span class="sxs-lookup"><span data-stu-id="221a6-109">Create a command menu for your bot</span></span>

<span data-ttu-id="221a6-110">Меню команд определяются в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="221a6-110">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="221a6-111">Вы можете использовать приложение App Studio, чтобы создать их или добавить вручную.</span><span class="sxs-lookup"><span data-stu-id="221a6-111">You can either use App Studio to help you create them, or add them manually.</span></span>

### <a name="creating-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="221a6-112">Создание командного меню для ленты с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="221a6-112">Creating a command menu for your bot using App Studio</span></span>

<span data-ttu-id="221a6-113">В этих инструкциях предполагается, что вы будете редактировать существующий манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="221a6-113">The instructions here assume that you'll be editing an existing app manifest.</span></span> <span data-ttu-id="221a6-114">Действия для добавления командного меню одинаковы, независимо от того, создаете ли вы новый манифест или редактируете существующий.</span><span class="sxs-lookup"><span data-stu-id="221a6-114">The steps for adding a command menu are the same, whether you're creating a new manifest or editing an existing one.</span></span>

1. <span data-ttu-id="221a6-115">Откройте приложение App Studio из... меню переполнения на левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="221a6-115">Open App Studio from the ... overflow menu on the left navigation rail.</span></span> <span data-ttu-id="221a6-116">Если у вас нет доступной App Studio, вы можете скачать его.</span><span class="sxs-lookup"><span data-stu-id="221a6-116">If you don't have App Studio available you can download it.</span></span> <span data-ttu-id="221a6-117">Более подробную информацию об использовании App Studio можно узнать в статье [Установка App Studio](https://aka.ms/teams-app-studio#installing-app-studio) .</span><span class="sxs-lookup"><span data-stu-id="221a6-117">See [Installing App Studio](https://aka.ms/teams-app-studio#installing-app-studio) for more information on using App Studio.</span></span>

    ![App Studio](./conversations/media/AppStudio.png)

2. <span data-ttu-id="221a6-119">В App Studio перейдите на вкладку **редактор манифестов** .</span><span class="sxs-lookup"><span data-stu-id="221a6-119">Once in App Studio, select the **Manifest editor** tab.</span></span>

3. <span data-ttu-id="221a6-120">В левом столбце представления редактор манифестов в разделе **возможности** выберите **Боты**.</span><span class="sxs-lookup"><span data-stu-id="221a6-120">In the left column of the manifest editor view in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="221a6-121">В правой колонке представления "редактор манифестов" в разделе **команды** нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="221a6-121">In the right column of the manifest editor view in the **Commands** section, select the **Add** button.</span></span>

    ![Кнопка "Добавить" меню "команд" в App Studio](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="221a6-123">Откроется экран **Новая команда** .</span><span class="sxs-lookup"><span data-stu-id="221a6-123">The **New Command** screen appears.</span></span> <span data-ttu-id="221a6-124">Введите **текст команды** , который должен отображаться в качестве команды меню, и **текст справки** , который должен отображаться непосредственно под текстом команды в меню.</span><span class="sxs-lookup"><span data-stu-id="221a6-124">Enter the **Command text** that you want to have appear as the menu command, and the **Help text** that you want to have appear directly under the command text in the menu.</span></span> <span data-ttu-id="221a6-125">Это должно быть краткое описание назначения команды.</span><span class="sxs-lookup"><span data-stu-id="221a6-125">This should be a brief explanation of the purpose of the command.</span></span>

6. <span data-ttu-id="221a6-126">Затем выберите области, в которых должно отображаться меню команд, а затем нажмите кнопку **сохранить** .</span><span class="sxs-lookup"><span data-stu-id="221a6-126">Next, select the scope(s) where you want this command menu to appear, then select the **Save** button.</span></span>

    ![Кнопка "Добавить" меню "команд" в App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="creating-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="221a6-128">Создание командного меню для ленты с помощью редактирования **manifest. JSON**</span><span class="sxs-lookup"><span data-stu-id="221a6-128">Creating a command menu for your bot by editing **Manifest.json**</span></span>

<span data-ttu-id="221a6-129">Другой допустимый подход к созданию командного меню состоит в том, чтобы создать его непосредственно в файле манифеста во время разработки исходного кода для ленты.</span><span class="sxs-lookup"><span data-stu-id="221a6-129">Another valid approach for creating a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="221a6-130">Ниже приведены некоторые моменты, которые необходимо учитывать при использовании такого подхода.</span><span class="sxs-lookup"><span data-stu-id="221a6-130">Here are a few things to keep in mind when using this approach:</span></span>

1. <span data-ttu-id="221a6-131">Каждое меню поддерживает до 10 команд.</span><span class="sxs-lookup"><span data-stu-id="221a6-131">Each menu supports up to 10 commands.</span></span>

2. <span data-ttu-id="221a6-132">Вы можете создать одно командное меню, которое будет работать во всех областях.</span><span class="sxs-lookup"><span data-stu-id="221a6-132">You can create a single command menu that will work in all scopes.</span></span>

3. <span data-ttu-id="221a6-133">Вы можете создать другое меню команд для каждой области.</span><span class="sxs-lookup"><span data-stu-id="221a6-133">You can create a different command menu for each scope</span></span>

#### <a name="manifest-example---single-menu-for-both-scopes"></a><span data-ttu-id="221a6-134">Пример манифеста — одно меню для обеих областей</span><span class="sxs-lookup"><span data-stu-id="221a6-134">Manifest example - single menu for both scopes</span></span>

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

#### <a name="manifest-example---menu-for-each-scope"></a><span data-ttu-id="221a6-135">Пример манифеста для каждой области</span><span class="sxs-lookup"><span data-stu-id="221a6-135">Manifest example - menu for each scope</span></span>

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

## <a name="handling-menu-commands-in-your-bot-code"></a><span data-ttu-id="221a6-136">Обработка команд меню в коде Bot</span><span class="sxs-lookup"><span data-stu-id="221a6-136">Handling menu commands in your bot code</span></span>

<span data-ttu-id="221a6-137">Боты в группе или канале отвечают только на то время, когда они упоминаются ("@botname") в сообщении.</span><span class="sxs-lookup"><span data-stu-id="221a6-137">Bots in a group or channel respond only when they are mentioned ("@botname") in a message.</span></span> <span data-ttu-id="221a6-138">В результате каждое сообщение, полученное с помощью Bot в области группы или канала, будет содержать собственное имя в возвращенном тексте сообщения.</span><span class="sxs-lookup"><span data-stu-id="221a6-138">As a result, every message received by a bot when in a group or channel scope will contain its own name in the message text returned.</span></span> <span data-ttu-id="221a6-139">Прежде чем обрабатывать возвращаемую команду, необходимо убедиться в том, что дескрипторы синтаксического анализа сообщений.</span><span class="sxs-lookup"><span data-stu-id="221a6-139">You need to ensure your message parsing handles that before handling the command being returned.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="221a6-140">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="221a6-140">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="221a6-141">Вы можете анализировать \*\* \@упоминание\*\* текста сообщения с помощью статического метода, поставляемого с Microsoft Bot Framework — метод `Activity` класса с именем `RemoveRecipientMention`.</span><span class="sxs-lookup"><span data-stu-id="221a6-141">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="221a6-142">JavaScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="221a6-142">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="221a6-143">Вы можете анализировать \*\* \@упоминание\*\* текста сообщения с помощью статического метода, поставляемого с Microsoft Bot Framework — метод `TurnContext` класса с именем `removeMentionText`.</span><span class="sxs-lookup"><span data-stu-id="221a6-143">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `removeMentionText`.</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="pythontabpython"></a>[<span data-ttu-id="221a6-144">Python</span><span class="sxs-lookup"><span data-stu-id="221a6-144">Python</span></span>](#tab/python)


<span data-ttu-id="221a6-145">Вы можете проанализировать **@Mention** часть текста сообщения с помощью статического метода, предоставляемого с помощью Microsoft Bot Framework — метода `TurnContext` класса с именем. `remove_recipient_mention`</span><span class="sxs-lookup"><span data-stu-id="221a6-145">You can parse out the **@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

## <a name="command-menu-best-practices"></a><span data-ttu-id="221a6-146">Рекомендации по использованию меню команд</span><span class="sxs-lookup"><span data-stu-id="221a6-146">Command menu best practices</span></span>

* <span data-ttu-id="221a6-147">Для **простоты**сделайте следующее: меню Bot предназначено для представления ключевых возможностей робота.</span><span class="sxs-lookup"><span data-stu-id="221a6-147">**Keep it simple**: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="221a6-148">**Не**забудьте: параметры меню не должны быть чрезвычайно длинными и сложными естественными языками — они должны быть простыми командами.</span><span class="sxs-lookup"><span data-stu-id="221a6-148">**Keep it short**: Menu options shouldn’t be extremely long and complex natural language statements — they should be simple commands.</span></span>
* <span data-ttu-id="221a6-149">**Поддерживать возможность вызова**: действия и команды меню "bot" всегда должны быть доступны, независимо от состояния беседы или диалогового окна, в котором находится почтовый робот.</span><span class="sxs-lookup"><span data-stu-id="221a6-149">**Keep it invokable**: Bot menu actions/commands should always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>
