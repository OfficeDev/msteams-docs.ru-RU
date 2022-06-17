---
title: Добавление меню бота
description: В этом модуле вы узнаете, как добавить меню бота в Microsoft Teams и создать меню для ботов в Microsoft Teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: ed65699b930d3e5334dd7fbb03da18a1482d6e5d
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143384"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Добавление меню бота в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Чтобы помочь в обнаружении и обучить пользователей функциональным возможностям бота, теперь можно добавлять меню, которые будут доступны при взаимодействии пользователя с ботом. В меню отобразится текст команды, а также текст справки, например пример использования или описание назначения команды.

![Снимок экрана: меню бота](~/assets/images/bots/bot-menus-bot-menu-sample.png)

Когда пользователь выбирает пункт меню, в текстовое поле вставляется строка команды, которая помогает пользователю выполнить сообщение бота.

## <a name="bot-menu-support-on-teams-mobile-app"></a>Поддержка меню бота в Teams мобильном приложении

> [!NOTE]
> Меню бота не отображаются на мобильных устройствах.

## <a name="app-manifest"></a>Манифест приложения

Чтобы создать меню бота, добавьте новый [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) объект в манифест приложения в разделе бота. Вы можете объявлять отдельные меню с отдельными командами для каждой области, `groupChat``team`поддерживаемой ботом (`personal`или). Каждое меню поддерживает до 10 команд.

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>Фрагмент манифеста — отдельное меню для области

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

* Не усложняйте: меню бота предназначено для представления основных возможностей бота.
* Будьте кратки: параметры меню не должны быть очень длинными и сложными операторами естественного языка— они должны быть простыми командами.
* Всегда доступно: действия или команды меню бота должны всегда быть вызовом независимо от состояния беседы или диалогового окна, в который находится бот.
