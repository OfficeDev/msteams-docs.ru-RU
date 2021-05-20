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
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Добавьте меню бота в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Чтобы помочь в обнаружении и просвещать пользователей о функциональности вашего бота, теперь вы можете добавлять меню, которые потуха, когда пользователь взаимодействует с вашим ботом. В меню будет помеся текст команды, а также будет приведен текст справки, например пример использования или описание цели команды.

![Скриншот меню бота](~/assets/images/bots/bot-menus-bot-menu-sample.png)

Когда пользователь выбирает элемент меню, строка команды вставляется в текстовый ящик, чтобы помочь пользователю завершить сообщение бота.

## <a name="bot-menu-support-on-teams-mobile-app"></a>Поддержка меню Bot в Teams мобильном приложении
> [!NOTE] 
> Меню Бота не отображается на мобильных устройствах.

## <a name="app-manifest"></a>Манифест приложения

Чтобы создать меню бота, добавьте [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) новый объект в манифест приложения под разделом бота. Вы можете объявить отдельные меню с отдельными командами для каждой `personal` области, которую поддерживает `groupChat` ваш бот `team` (, или) Каждое меню поддерживает до 10 команд.

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>Отрывок манифеста - одно меню для обоих областей

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>Отрывок манифеста - отдельное меню в области

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

* Держите его простым: Меню бота предназначено, чтобы представить ключевые возможности вашего бота.
* Держите его коротким: Параметры меню не должны быть очень длинными и сложными заявлениями на естественном языке - они должны быть простыми командами.
* Всегда доступны: Бот меню действия / команды должны быть всегда invokable, независимо от состояния разговора или диалог бот дюйма
