---
title: Добавление меню бота
description: Описывает создание меню для ботов в Microsoft Teams
keywords: teams bots menus creation
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 6f339f23298c14607eb1d9ca12daa50bcc98775b
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452902"
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

Чтобы создать меню бота, добавьте новый [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) объект в манифест приложения в разделе бот. Вы можете объявить отдельные меню с отдельными командами для каждой области, поддерживаемой ботом (`personal`или`team``groupChat`) Каждое меню поддерживает до 10 команд.

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

## <a name="best-practices"></a>Лучшие методики

* Сохраняйте простое: меню бота предназначено для того, чтобы представить основные возможности вашего бота.
* Кратко: параметры меню не должны быть очень длинными и сложными выражениями естественного языка , они должны быть простыми командами.
* Всегда доступно: действия или команды меню бота всегда должны быть неосказуемыми, независимо от состояния беседы или диалоговом окне, в который находится бот.
