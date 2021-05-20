---
title: Добавить меню бота
description: Описывает, как создать меню для ботов в Microsoft Teams
keywords: создание меню команд ботов
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
# <a name="add-a-bot-menu-in-microsoft-teams"></a><span data-ttu-id="a5fc3-104">Добавьте меню бота в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a5fc3-104">Add a bot menu in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="a5fc3-105">Чтобы помочь в обнаружении и просвещать пользователей о функциональности вашего бота, теперь вы можете добавлять меню, которые потуха, когда пользователь взаимодействует с вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="a5fc3-105">To aid discovery and to help educate users about your bot’s functionality, you can now add menus that surface whenever the user interacts with your bot.</span></span> <span data-ttu-id="a5fc3-106">В меню будет помеся текст команды, а также будет приведен текст справки, например пример использования или описание цели команды.</span><span class="sxs-lookup"><span data-stu-id="a5fc3-106">The menu will show the command text and also provide help text, such as a usage example or description of the command’s purpose.</span></span>

![Скриншот меню бота](~/assets/images/bots/bot-menus-bot-menu-sample.png)

<span data-ttu-id="a5fc3-108">Когда пользователь выбирает элемент меню, строка команды вставляется в текстовый ящик, чтобы помочь пользователю завершить сообщение бота.</span><span class="sxs-lookup"><span data-stu-id="a5fc3-108">When a user selects a menu item, the command string is inserted into the text box to aid in user completion of the bot message.</span></span>

## <a name="bot-menu-support-on-teams-mobile-app"></a><span data-ttu-id="a5fc3-109">Поддержка меню Bot в Teams мобильном приложении</span><span class="sxs-lookup"><span data-stu-id="a5fc3-109">Bot menu support on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="a5fc3-110">Меню Бота не отображается на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="a5fc3-110">Bot menus are not displayed on mobile devices.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="a5fc3-111">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="a5fc3-111">App manifest</span></span>

<span data-ttu-id="a5fc3-112">Чтобы создать меню бота, добавьте [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) новый объект в манифест приложения под разделом бота.</span><span class="sxs-lookup"><span data-stu-id="a5fc3-112">To create a bot menu, add a new [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) object to your app manifest under the bot section.</span></span> <span data-ttu-id="a5fc3-113">Вы можете объявить отдельные меню с отдельными командами для каждой `personal` области, которую поддерживает `groupChat` ваш бот `team` (, или) Каждое меню поддерживает до 10 команд.</span><span class="sxs-lookup"><span data-stu-id="a5fc3-113">You can declare individual menus with separate commands for each scope your bot supports (`personal`, `groupChat`, or `team`) Each menu supports up to 10 commands.</span></span>

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a><span data-ttu-id="a5fc3-114">Отрывок манифеста - одно меню для обоих областей</span><span class="sxs-lookup"><span data-stu-id="a5fc3-114">Manifest excerpt - single menu for both scopes</span></span>

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a><span data-ttu-id="a5fc3-115">Отрывок манифеста - отдельное меню в области</span><span class="sxs-lookup"><span data-stu-id="a5fc3-115">Manifest excerpt - separate menu per scope</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="a5fc3-116">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="a5fc3-116">Best practices</span></span>

* <span data-ttu-id="a5fc3-117">Держите его простым: Меню бота предназначено, чтобы представить ключевые возможности вашего бота.</span><span class="sxs-lookup"><span data-stu-id="a5fc3-117">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="a5fc3-118">Держите его коротким: Параметры меню не должны быть очень длинными и сложными заявлениями на естественном языке - они должны быть простыми командами.</span><span class="sxs-lookup"><span data-stu-id="a5fc3-118">Keep it short: Menu options shouldn’t be extremely long and complex natural language statements - they should be simple commands.</span></span>
* <span data-ttu-id="a5fc3-119">Всегда доступны: Бот меню действия / команды должны быть всегда invokable, независимо от состояния разговора или диалог бот дюйма</span><span class="sxs-lookup"><span data-stu-id="a5fc3-119">Always available: Bot menu actions/commands should be always invokable, regardless of the state of the conversation or the dialog the bot is in.</span></span>
