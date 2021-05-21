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
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Добавление меню бота в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Для помощи в обнаружении и информировании пользователей о функциональных возможностях вашего бота теперь можно добавлять меню, которые будут открываться при взаимодействии пользователя с ботом. В меню будет показываться текст команды, а также текст справки, например пример использования или описание цели команды.

![Снимок экрана меню бота](~/assets/images/bots/bot-menus-bot-menu-sample.png)

Когда пользователь выбирает элемент меню, строка команды вставляется в текстовое поле, чтобы помочь пользователю завершить сообщение бота.

## <a name="bot-menu-support-on-teams-mobile-app"></a>Поддержка меню бота Teams мобильном приложении
> [!NOTE] 
> Меню бота не отображается на мобильных устройствах.

## <a name="app-manifest"></a>Манифест приложения

Чтобы создать меню бота, добавьте новый объект в [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) манифест приложения в разделе бот. Вы можете объявить отдельные меню с отдельными командами для каждой области, поддерживаемой ботом (или) Каждое меню поддерживает до `personal` `groupChat` `team` 10 команд.

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>Выдержка манифеста — одно меню для обеих областей

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>Выдержка манифеста — отдельное меню для области

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

* Сохраняйте простое: меню бота предназначено для того, чтобы представить основные возможности вашего бота.
* Кратко: параметры меню не должны быть очень длинными и сложными выражениями естественного языка , они должны быть простыми командами.
* Всегда доступно: действия или команды меню бота всегда должны быть неосказуемыми, независимо от состояния беседы или диалоговом окне, в который находится бот.
