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
# <a name="bot-command-menus"></a>Меню команд Bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> Меню ленты не отображаются на мобильных клиентах.

Команда добавить меню для ленты позволяет определить набор основных команд, на которые пользователь Bot всегда может отвечать. Список команд предоставляется пользователю, расположенному над областью создание сообщения, при их взаимосравнении с Bot. При выборе команды из списка в поле создать сообщение будет вставлена Командная строка, тогда все пользователи должны выполнить команду **Отправить**.

![Меню команд Bot](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a>Создание командного меню для ленты

Меню команд определяются в манифесте приложения. Вы можете использовать приложение App Studio, чтобы создать их или добавить вручную.

### <a name="creating-a-command-menu-for-your-bot-using-app-studio"></a>Создание командного меню для ленты с помощью App Studio

В этих инструкциях предполагается, что вы будете редактировать существующий манифест приложения. Действия для добавления командного меню одинаковы, независимо от того, создаете ли вы новый манифест или редактируете существующий.

1. Откройте приложение App Studio из... меню переполнения на левой панели навигации. Если у вас нет доступной App Studio, вы можете скачать его. Более подробную информацию об использовании App Studio можно узнать в статье [Установка App Studio](https://aka.ms/teams-app-studio#installing-app-studio) .

    ![App Studio](./conversations/media/AppStudio.png)

2. В App Studio перейдите на вкладку **редактор манифестов** .

3. В левом столбце представления редактор манифестов в разделе **возможности** выберите **Боты**.

4. В правой колонке представления "редактор манифестов" в разделе **команды** нажмите кнопку **Добавить** .

    ![Кнопка "Добавить" меню "команд" в App Studio](./conversations/media/AppStudio-CommandMenu-Add.png)

5. Откроется экран **Новая команда** . Введите **текст команды** , который должен отображаться в качестве команды меню, и **текст справки** , который должен отображаться непосредственно под текстом команды в меню. Это должно быть краткое описание назначения команды.

6. Затем выберите области, в которых должно отображаться меню команд, а затем нажмите кнопку **сохранить** .

    ![Кнопка "Добавить" меню "команд" в App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="creating-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Создание командного меню для ленты с помощью редактирования **manifest. JSON**

Другой допустимый подход к созданию командного меню состоит в том, чтобы создать его непосредственно в файле манифеста во время разработки исходного кода для ленты. Ниже приведены некоторые моменты, которые необходимо учитывать при использовании такого подхода.

1. Каждое меню поддерживает до 10 команд.

2. Вы можете создать одно командное меню, которое будет работать во всех областях.

3. Вы можете создать другое меню команд для каждой области.

#### <a name="manifest-example---single-menu-for-both-scopes"></a>Пример манифеста — одно меню для обеих областей

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

#### <a name="manifest-example---menu-for-each-scope"></a>Пример манифеста для каждой области

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

## <a name="handling-menu-commands-in-your-bot-code"></a>Обработка команд меню в коде Bot

Боты в группе или канале отвечают только на то время, когда они упоминаются ("@botname") в сообщении. В результате каждое сообщение, полученное с помощью Bot в области группы или канала, будет содержать собственное имя в возвращенном тексте сообщения. Прежде чем обрабатывать возвращаемую команду, необходимо убедиться в том, что дескрипторы синтаксического анализа сообщений.

# <a name="cnettabdotnet"></a>[ЯЗЫК C#/.НЕТ](#tab/dotnet)

Вы можете анализировать ** \@упоминание** текста сообщения с помощью статического метода, поставляемого с Microsoft Bot Framework — метод `Activity` класса с именем `RemoveRecipientMention`.

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/Node. js](#tab/javascript)

Вы можете анализировать ** \@упоминание** текста сообщения с помощью статического метода, поставляемого с Microsoft Bot Framework — метод `TurnContext` класса с именем `removeMentionText`.

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="pythontabpython"></a>[Python](#tab/python)


Вы можете проанализировать **@Mention** часть текста сообщения с помощью статического метода, предоставляемого с помощью Microsoft Bot Framework — метода `TurnContext` класса с именем. `remove_recipient_mention`

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

## <a name="command-menu-best-practices"></a>Рекомендации по использованию меню команд

* Для **простоты**сделайте следующее: меню Bot предназначено для представления ключевых возможностей робота.
* **Не**забудьте: параметры меню не должны быть чрезвычайно длинными и сложными естественными языками — они должны быть простыми командами.
* **Поддерживать возможность вызова**: действия и команды меню "bot" всегда должны быть доступны, независимо от состояния беседы или диалогового окна, в котором находится почтовый робот.
