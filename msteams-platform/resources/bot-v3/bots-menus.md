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
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Добавление меню "bot" в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Чтобы упростить обнаружение и облегчить обучение пользователей функциям Bot, теперь можно добавлять меню, которые отображаются каждый раз, когда пользователь взаимодействует с роботом. В меню отображается текст команды, а также текст справки, например, пример использования команды или описание ее назначения.

![Снимок экрана: меню Bot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

Когда пользователь выбирает элемент меню, в текстовое поле вставляется Командная строка, чтобы помочь пользователю завершить сообщение ленты.

## <a name="bot-menu-support-on-teams-mobile-app"></a>Поддержка меню Bot в мобильном приложении Teams
> [!NOTE] 
> Меню ленты не отображаются на мобильных устройствах

## <a name="app-manifest"></a>Манифест приложения

Чтобы создать меню Bot, добавьте новый [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) объект в манифест приложения в разделе "bot". Вы можете объявить отдельные меню с отдельными командами для каждой области,`personal` `groupChat` которую поддерживает Bot `team`(или) каждое меню поддерживает до 10 команд.

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>Фрагмент манифеста — одно меню для обеих областей

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>Выдержка — разделяет меню на область

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

## <a name="best-practices"></a>Рекомендации

* Для простоты сделайте следующее: меню Bot предназначено для представления ключевых возможностей робота.
* Не забудьте: параметры меню не должны быть чрезвычайно длинными и сложными естественными языками — они должны быть простыми командами.
* Всегда доступно: действия и команды меню "bot" всегда могут вызываться, независимо от состояния беседы или диалогового окна, в котором находится Bot.
