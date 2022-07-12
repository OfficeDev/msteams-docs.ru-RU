---
title: Создать меню команд для бота
author: surbhigupta
description: В этом модуле вы узнаете, как создать и обработать командное меню для бота Microsoft Teams с примерами кода.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 6252531565693f318550398967db16297bfd40c0
ms.sourcegitcommit: 526ad8562d3bacc13141cd7f695aa5f3f3752052
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2022
ms.locfileid: "66737421"
---
# <a name="create-a-commands-menu"></a>Создать меню команд

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Чтобы определить набор основных команд, на которые может отвечать бот, можно добавить для него командное меню с раскрывающимся списком команд. Список команд предоставляется пользователям в области создания сообщений, когда они беседуют с ботом. Выберите команду из списка, чтобы вставить строку команды в окно создания сообщения и щелкните **Отправить**.

# <a name="desktop"></a>[Компьютер](#tab/desktop)

:::image type="content" source="conversations/Media/bot-menu-sample.png" alt-text="Bot-command-menu":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="conversations/Media/mobile-bot-menu-sample.png" alt-text="Mobile-bot-command-menu":::

* * *

## <a name="create-a-command-menu-for-your-bot"></a>Создать меню команд для бота

Меню команд определяются в манифесте приложения. Их можно создать с помощью **App Studio** или вручную добавить в манифест приложения.

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>Создание командного меню для бота с помощью App Studio

Чтобы создать командное меню для бота, необходимо изменить существующий манифест приложения. Действия по добавлению командного меню одинаковы независимо от того, создаете ли вы новый манифест или изменяете существующий.

**Создание командного меню для бота с помощью App Studio**

1. Откройте Teams и выберите **Приложения** в левой области. На странице **Приложения** найдите **App Studio** и выберите **Открыть**.

   > [!WARNING]
   > Если вы использовали App Studio, рекомендуем попробовать Портал разработчика для настройки, распространения и управления приложениями Teams. App Studio будет объявлен нерекомендуемым до 1 августа 2022 г.

   :::image type="content" source="conversations/Media/AppStudio.png" alt-text="appstudio-media":::

2. В **App Studio** перейдите на вкладку **редактора манифеста**. Если у вас еще нет пакета приложения, можно создать приложение или импортировать существующее. Дополнительные сведения см. в [C# app package in App Studio](../../get-started/deploy-csharp-app-studio.md).

3. В **редакторе манифеста** на панели слева и в разделе **Возможности** выберите **Боты**.

4. В **редакторе манифеста** на панели справа и в разделе **Команды** выберите **Добавить**. Будет отображен экран **Новая команда**.

   :::image type="content" source="media/AppStudio-CommandMenu-Add.png" alt-text="Выбор файла пакета приложения" lightbox="media/AppStudio-CommandMenu-Add.png "border="true":::

5. Введите **текст команды**, который будет показан в меню команд для бота.

6. Введите **текст справки**, который будет показан под текстом команды в меню. **Текст справки** должен быть кратким описанием назначения команды.

7. Установите флажки **области**, чтобы выбрать место, где будет показано командное меню, и нажмите кнопку **Сохранить**.

   :::image type="content" source="media/AppStudio-NewCommandMenu.png" alt-text="Кнопка меню &quot;Новые команды&quot; в App Studio "lightbox="media/AppStudio-NewCommandMenu.png "border="true":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Создание командного меню для бота путем редактирования Файла Manifest.json

Еще один способ создания командного меню — создать его непосредственно в файле манифеста при разработке исходного кода бота. Чтобы использовать этот метод, сделайте следующее:

* Каждое меню поддерживает до десяти команд.
* Создайте одно командное меню, которое работает во всех областях.
* Создайте отдельное командное меню для каждой области.

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>Пример манифеста для одного меню для обеих областей

Пример кода манифеста для одного меню для обеих областей выглядит следующим образом:

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

#### <a name="manifest-example-for-the-menu-for-each-scope"></a>Пример манифеста для меню для каждой области

Пример кода манифеста для меню для каждой области выглядит следующим образом:

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

Команды меню необходимо обрабатывать в коде бота аналогично обработке любого сообщения от пользователей. Команды меню можно обрабатывать в коде бота, проводя синтаксический анализ части **\@Упоминание** в тексте сообщения.

## <a name="handle-menu-commands-in-your-bot-code"></a>Обработка команд меню в коде бота

Боты в группе или канале отвечают только в том случае, если они упомянуты `@botname` в сообщении. Текст каждого сообщения, полученного ботом в группе или области канала, содержит его имя. Перед обработкой возвращаемой команды анализ сообщений должен обрабатывать сообщение, полученное ботом и содержащее его имя.

> [!NOTE]
> Для обработки команд программным образом их отправляют боту в виде обычного сообщения. Их обрабатывают так же, как и любое другое сообщение от пользователей. Команды в коде вставляют предварительно настроенный текст в текстовое поле. Затем пользователь должен отправить этот текст так же, как и любое другое сообщение.

# <a name="c"></a>[C#](#tab/dotnet)

Фрагмент текста сообщения, представляющий собой **\@упоминание**, можно анализировать с помощью статического метода, предоставленного Microsoft Bot Framework. Это метод `RemoveRecipientMention` класса `Activity`.

Код C# для синтаксического анализа фрагмента-**\@Упоминания** текста сообщения выглядит следующим образом:

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Фрагмент текста сообщения, представляющий собой **\@упоминание**, можно анализировать с помощью статического метода, предоставленного Bot Framework. Это метод `removeMentionText` класса `TurnContext`.

Код JavaScript для синтаксического анализа фрагмента-**\@Упоминания** текста сообщения выглядит следующим образом:

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

Фрагмент текста сообщения, представляющий собой **@упоминание**, можно анализировать с помощью статического метода, предоставленного Bot Framework. Это метод класса `TurnContext` под названием `remove_recipient_mention`.

Код Python для синтаксического анализа фрагмента-**\@Упоминания** текста сообщения выглядит следующим образом:

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

Чтобы обеспечить бесперебойную работу программного кода бота, последуйте нескольким рекомендациям.

## <a name="command-menu-best-practices"></a>Рекомендации по применению командного меню

Ниже приведены рекомендации по применению командного меню.

* Не усложняйте: меню бота предназначено для представления основных возможностей бота.
* Будьте кратки: пункты меню не должны быть длинными и не должны представлять собой сложные фразы естественного языка. Это должны быть простые команды.
* Позаботьтесь о вызываемости: действия или команды меню бота всегда должны быть доступны независимо от состояния беседы или диалогового окна, в котором находится бот.

> [!NOTE]
> При удалении каких-либо команд из манифеста необходимо повторно развернуть приложение для реализации изменений. Как правило, любые изменения манифеста требуют повторного развертывания приложения.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Канал и групповые разговоры](~/bots/how-to/conversations/channel-and-group-conversations.md)
