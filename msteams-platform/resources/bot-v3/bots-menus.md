---
title: Добавление меню "bot"
description: Сведения о создании меню для боты в Microsoft Teams
keywords: Создание меню Teams Боты
ms.date: 05/20/2019
ms.openlocfilehash: 36a224dc21cccc5fcd1047e45e3d749e7ca19ea7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675205"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a><span data-ttu-id="ceaa3-104">Добавление меню "bot" в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ceaa3-104">Add a bot menu in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="ceaa3-105">Чтобы упростить обнаружение и облегчить обучение пользователей функциям Bot, теперь можно добавлять меню, которые отображаются каждый раз, когда пользователь взаимодействует с роботом.</span><span class="sxs-lookup"><span data-stu-id="ceaa3-105">To aid discovery and to help educate users about your bot’s functionality, you can now add menus that surface whenever the user interacts with your bot.</span></span> <span data-ttu-id="ceaa3-106">В меню отображается текст команды, а также текст справки, например, пример использования команды или описание ее назначения.</span><span class="sxs-lookup"><span data-stu-id="ceaa3-106">The menu will show the command text and also provide help text, such as a usage example or description of the command’s purpose.</span></span>

![Снимок экрана: меню Bot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

<span data-ttu-id="ceaa3-108">Когда пользователь выбирает элемент меню, в текстовое поле вставляется Командная строка, чтобы помочь пользователю завершить сообщение ленты.</span><span class="sxs-lookup"><span data-stu-id="ceaa3-108">When a user selects a menu item, the command string is inserted into the text box to aid in user completion of the bot message.</span></span>

## <a name="bot-menu-support-on-teams-mobile-app"></a><span data-ttu-id="ceaa3-109">Поддержка меню Bot в мобильном приложении Teams</span><span class="sxs-lookup"><span data-stu-id="ceaa3-109">Bot menu support on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="ceaa3-110">Меню ленты не отображаются на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="ceaa3-110">Bot menus are not displayed on mobile devices</span></span>

## <a name="app-manifest"></a><span data-ttu-id="ceaa3-111">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="ceaa3-111">App manifest</span></span>

<span data-ttu-id="ceaa3-112">Чтобы создать меню Bot, добавьте новый [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) объект в манифест приложения в разделе "bot".</span><span class="sxs-lookup"><span data-stu-id="ceaa3-112">To create a bot menu, add a new [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) object to your app manifest under the bot section.</span></span> <span data-ttu-id="ceaa3-113">Вы можете объявить отдельные меню с отдельными командами для каждой области,`personal` `groupChat` которую поддерживает Bot `team`(или) каждое меню поддерживает до 10 команд.</span><span class="sxs-lookup"><span data-stu-id="ceaa3-113">You can declare individual menus with separate commands for each scope your bot supports (`personal`, `groupChat` or `team`) Each menu supports up to 10 commands.</span></span>

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a><span data-ttu-id="ceaa3-114">Фрагмент манифеста — одно меню для обеих областей</span><span class="sxs-lookup"><span data-stu-id="ceaa3-114">Manifest excerpt - single menu for both scopes</span></span>

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a><span data-ttu-id="ceaa3-115">Выдержка — разделяет меню на область</span><span class="sxs-lookup"><span data-stu-id="ceaa3-115">Manifest excerpt - separate menu per scope</span></span>

```json
{
  ...
  "bots":[
    {
      "botId":"[Microsoft app ID for your bot]",
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

## <a name="best-practices"></a><span data-ttu-id="ceaa3-116">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="ceaa3-116">Best practices</span></span>

* <span data-ttu-id="ceaa3-117">Для простоты сделайте следующее: меню Bot предназначено для представления ключевых возможностей робота.</span><span class="sxs-lookup"><span data-stu-id="ceaa3-117">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="ceaa3-118">Не забудьте: параметры меню не должны быть чрезвычайно длинными и сложными естественными языками — они должны быть простыми командами.</span><span class="sxs-lookup"><span data-stu-id="ceaa3-118">Keep it short: Menu options shouldn’t be extremely long and complex natural language statements - they should be simple commands.</span></span>
* <span data-ttu-id="ceaa3-119">Всегда доступно: действия и команды меню "bot" всегда могут вызываться, независимо от состояния беседы или диалогового окна, в котором находится Bot.</span><span class="sxs-lookup"><span data-stu-id="ceaa3-119">Always available: Bot menu actions/commands should be always invokable, regardless of the state of the conversation or the dialog the bot is in.</span></span>
