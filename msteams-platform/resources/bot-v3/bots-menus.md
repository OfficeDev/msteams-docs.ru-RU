---
title: Добавление меню бота
description: Описывает, как создавать меню для ботов в Microsoft Teams
keywords: teams bots menus creation
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: da6f36e1b7071b92f6411ab7d2afdccb795946b7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566770"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a><span data-ttu-id="03fca-104">Добавление меню бота в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="03fca-104">Add a bot menu in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="03fca-105">Для помощи в обнаружении и информировании пользователей о функциональных возможностях вашего бота теперь можно добавлять меню, которые будут открываться при взаимодействии пользователя с ботом.</span><span class="sxs-lookup"><span data-stu-id="03fca-105">To aid discovery and to help educate users about your bot’s functionality, you can now add menus that surface whenever the user interacts with your bot.</span></span> <span data-ttu-id="03fca-106">В меню будет показываться текст команды, а также текст справки, например пример использования или описание цели команды.</span><span class="sxs-lookup"><span data-stu-id="03fca-106">The menu will show the command text and also provide help text, such as a usage example or description of the command’s purpose.</span></span>

![Снимок экрана меню бота](~/assets/images/bots/bot-menus-bot-menu-sample.png)

<span data-ttu-id="03fca-108">Когда пользователь выбирает элемент меню, строка команды вставляется в текстовое поле, чтобы помочь пользователю завершить сообщение бота.</span><span class="sxs-lookup"><span data-stu-id="03fca-108">When a user selects a menu item, the command string is inserted into the text box to aid in user completion of the bot message.</span></span>

## <a name="bot-menu-support-on-teams-mobile-app"></a><span data-ttu-id="03fca-109">Поддержка меню бота Teams мобильном приложении</span><span class="sxs-lookup"><span data-stu-id="03fca-109">Bot menu support on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="03fca-110">Меню бота не отображается на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="03fca-110">Bot menus are not displayed on mobile devices.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="03fca-111">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="03fca-111">App manifest</span></span>

<span data-ttu-id="03fca-112">Чтобы создать меню бота, добавьте новый объект в [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) манифест приложения в разделе бот.</span><span class="sxs-lookup"><span data-stu-id="03fca-112">To create a bot menu, add a new [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) object to your app manifest under the bot section.</span></span> <span data-ttu-id="03fca-113">Вы можете объявить отдельные меню с отдельными командами для каждой области, поддерживаемой ботом (или) Каждое меню поддерживает до `personal` `groupChat` `team` 10 команд.</span><span class="sxs-lookup"><span data-stu-id="03fca-113">You can declare individual menus with separate commands for each scope your bot supports (`personal`, `groupChat`, or `team`) Each menu supports up to 10 commands.</span></span>

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a><span data-ttu-id="03fca-114">Выдержка манифеста — одно меню для обеих областей</span><span class="sxs-lookup"><span data-stu-id="03fca-114">Manifest excerpt - single menu for both scopes</span></span>

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a><span data-ttu-id="03fca-115">Выдержка манифеста — отдельное меню для области</span><span class="sxs-lookup"><span data-stu-id="03fca-115">Manifest excerpt - separate menu per scope</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="03fca-116">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="03fca-116">Best practices</span></span>

* <span data-ttu-id="03fca-117">Сохраняйте простое: меню бота предназначено для того, чтобы представить основные возможности вашего бота.</span><span class="sxs-lookup"><span data-stu-id="03fca-117">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="03fca-118">Кратко: параметры меню не должны быть очень длинными и сложными выражениями естественного языка , они должны быть простыми командами.</span><span class="sxs-lookup"><span data-stu-id="03fca-118">Keep it short: Menu options shouldn’t be extremely long and complex natural language statements - they should be simple commands.</span></span>
* <span data-ttu-id="03fca-119">Всегда доступно: действия или команды меню бота всегда должны быть неосказуемыми, независимо от состояния беседы или диалоговом окне, в который находится бот.</span><span class="sxs-lookup"><span data-stu-id="03fca-119">Always available: Bot menu actions/commands should be always invokable, regardless of the state of the conversation or the dialog the bot is in.</span></span>
