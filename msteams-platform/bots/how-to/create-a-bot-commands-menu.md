---
title: Создать меню команд для бота
author: surbhigupta
description: Узнайте, как создать и обработать командное меню для бота Microsoft Teams, а также рекомендации. Узнайте, как удалить команды из манифеста.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 0e0f9ce9ada0cde0aa6f7b6b29c7badb07dd7db9
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100905"
---
# <a name="create-a-commands-menu"></a>Создать меню команд

> [!NOTE]
> Рекомендуется создать бот команд, следуя пошаговое руководство по созданию бота команд с [помощью JavaScript](../../sbs-gs-commandbot.yml) с помощью средства разработки нового поколения для Teams. Дополнительные сведения о Наборе средств Teams см. в разделе "Обзор набора средств [Teams" Visual Studio Code](../../toolkit/teams-toolkit-fundamentals.md) и обзор [набора средств Teams для Visual Studio](../../toolkit/teams-toolkit-overview-visual-studio.md).

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Чтобы определить набор основных команд, на которые может отвечать бот, можно добавить для него командное меню с раскрывающимся списком команд. Список команд предоставляется пользователям в области создания сообщений, когда они беседуют с ботом. Выберите команду из списка, чтобы вставить строку команды в окно создания сообщения и щелкните **Отправить**.

# <a name="desktop"></a>[Компьютер](#tab/desktop)

:::image type="content" source="conversations/Media/bot-menu-sample.png" alt-text="Bot-command-menu":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="conversations/Media/mobile-bot-menu-sample.png" alt-text="Mobile-bot-command-menu":::

* * *

## <a name="create-a-command-menu-for-your-bot"></a>Создать меню команд для бота

Меню команд определяются в манифесте приложения. Их можно создать **с помощью портала** разработчика или вручную добавить в манифест приложения.

### <a name="create-a-command-menu-for-your-bot-using-developer-portal"></a>Создание командного меню для бота с помощью портала разработчика

Чтобы создать командное меню для бота, необходимо изменить существующий манифест приложения. Действия по добавлению командного меню одинаковы независимо от того, создаете ли вы новый манифест или изменяете существующий.

Чтобы создать командное меню для бота с помощью портала разработчика, выполните следующие действия.

1. Откройте Teams и выберите **Приложения** в левой области. На странице **"Приложения** " найдите портал **разработчика** и нажмите кнопку " **Открыть"**.

   :::image type="content" source="../../assets/images/tdp/add-dev-portal.png" alt-text="Снимок экрана: добавление портала разработчика в клиент Teams.":::
  
1. На **портале разработчика** выберите **вкладку "Приложения** ". Если у вас нет существующего пакета приложения, можно создать или импортировать существующее приложение. Дополнительные сведения см. на [портале разработчика для Teams](../../concepts/build-and-test/teams-developer-portal.md).

1. Выберите **вкладку** "Приложения" **, выберите компоненты** приложения на левой панели, а затем — **"Боты"**.

1. Выберите **"Добавить команду"** в **разделе "Команды** ".

   :::image type="content" source="../../assets/images/tdp/add-a-bot-command.png" alt-text="Снимок экрана: добавление команды для бота на портале разработчика.":::

1. Введите **команду,** которая отображается в меню команд для бота.

1. Введите **описание,** которое отображается под текстом команды в меню. **Описание** должно быть кратким описанием назначения команды.

1. Установите **флажок "** Область" и нажмите кнопку **"Добавить"**.
   Это определяет, где должно отображаться меню команд.

   :::image type="content" source="../../assets/images/tdp/bot-command.png" alt-text="Снимок экрана: добавление команды, описания и областей для бота.":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Создание командного меню для бота путем редактирования Файла Manifest.json

Another way to create a command menu is to create it directly in the manifest file while developing your bot source code. To use this method, follow these points:

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

You can parse out the **@Mention** portion of the message text using a static method provided with the Bot Framework. It is a method of the `TurnContext` class named `remove_recipient_mention`.

Код Python для синтаксического анализа фрагмента-**\@Упоминания** текста сообщения выглядит следующим образом:

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

Чтобы обеспечить бесперебойную работу программного кода бота, последуйте нескольким рекомендациям.

## <a name="command-menu-best-practices"></a>Рекомендации по применению командного меню

Ниже приведены рекомендации по применению командного меню.

* Не усложняйте: меню бота предназначено для представления основных возможностей бота.
* Keep it short: Menu options must not be long and must not be complex natural language statements. They must be simple commands.
* Позаботьтесь о вызываемости: действия или команды меню бота всегда должны быть доступны независимо от состояния беседы или диалогового окна, в котором находится бот.

> [!NOTE]
> При удалении каких-либо команд из манифеста необходимо повторно развернуть приложение для реализации изменений. Как правило, любые изменения манифеста требуют повторного развертывания приложения.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Канал и групповые разговоры](~/bots/how-to/conversations/channel-and-group-conversations.md)
