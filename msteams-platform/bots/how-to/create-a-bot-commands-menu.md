---
title: Создание командного меню для бота
author: surbhigupta
description: Узнайте, как создать командное меню для бота Microsoft Teams с примерами кода.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
keywords: командное меню создает беседу с сообщением @mention
ms.openlocfilehash: 6f4b9cdac76fc9beb42a39dde3b320036ea580b5
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102556"
---
# <a name="bot-command-menus"></a>Меню команд бота

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Чтобы определить набор основных команд, на которые может отвечать бот, можно добавить меню команд с раскрывающимся списком команд для бота. Список команд предоставляется пользователям в области создания сообщений, когда они беседуют с ботом. Выберите команду из списка, чтобы вставить строку команды в окно сообщения создания и выбрать команду **"Отправить"**.

# <a name="desktop"></a>[Компьютер](#tab/desktop)

![Меню команд бота](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

![Меню команд мобильного бота](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a>Создание командного меню для бота

Меню команд определяются в манифесте приложения. Их можно создать с **помощью App Studio** или вручную добавить в манифест приложения.

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>Создание командного меню для бота с помощью App Studio

Чтобы создать командное меню для бота, необходимо изменить существующий манифест приложения. Действия по добавлению командного меню одинаковы независимо от того, создаете ли вы новый манифест или изменяете существующий.

**Создание командного меню для бота с помощью App Studio**

1. Откройте Teams и выберите **"Приложения**" в левой области. На странице **"Приложения** " найдите **App Studio** и выберите " **Открыть"**.
   > [!NOTE]
   > Если у вас нет **App Studio**, его можно скачать. Дополнительные сведения см. [в статье об установке App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).

    :::image type="content" source="/media/AppStudio.png" alt-text="Установка App Studio"lightbox="media/AppStudio.png"border="true":::

2. В **App Studio перейдите** на **вкладку редактора манифеста** . Если у вас нет существующего пакета приложения, можно создать или импортировать существующее приложение. Дополнительные сведения см. [в статье об обновлении пакета приложения](~/get-started/deploy-csharp-app-studio.md).

3. В левой области редактора **манифеста** и в разделе **"** Возможности" выберите **"Боты"**.

4. В правой области редактора **манифеста** и в разделе **"Команды"** нажмите кнопку **"Добавить"**. **Появится экран "** Новая команда".

    :::image type="content" source="/media/AppStudio-CommandMenu-Add.png" alt-text="Выбор пакета приложения"lightbox="/media/AppStudio-CommandMenu-Add.png"border="true":::

5. Введите **текст команды,** который должен отображаться в меню команд для бота.

6. Введите **текст справки** , который должен отображаться под текстом команды в меню. **Текст справки** должен быть кратким описанием назначения команды.

7. Установите **флажки** области, чтобы выбрать место, где должно отображаться это командное меню, и нажмите кнопку **"Сохранить"**.

:::image type="content" source="/media/AppStudio-NewCommandMenu.png" alt-text="Кнопка меню &quot;Новые команды&quot; в App Studio"lightbox="/media/AppStudio-NewCommandMenu.png"border="true":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Создание командного меню для бота путем редактирования Файла Manifest.json

Еще один способ создать командное меню — создать его непосредственно в файле манифеста при разработке исходного кода бота. Чтобы использовать этот метод, выполните следующие действия.

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

Команды меню необходимо обрабатывать в коде бота при обработке любого сообщения от пользователей. Команды меню можно обрабатывать в коде бота **\@**, анализируя часть "Упоминание" в тексте сообщения.

## <a name="handle-menu-commands-in-your-bot-code"></a>Обработка команд меню в коде бота

Боты в группе или канале отвечают только в том случае, если они упомянуты `@botname` в сообщении. Каждое сообщение, полученное ботом в группе или области канала, содержит его имя в тексте сообщения. Перед обработкой возвращаемой команды анализ сообщений должен обрабатывать сообщение, полученное ботом с его именем.

> [!NOTE]
> Для обработки команд в коде они отправляются боту в виде обычного сообщения. Их необходимо обрабатывать так же, как и любое другое сообщение от пользователей. Команды в коде вставляют предварительно настроенный текст в текстовое поле. Затем пользователь должен отправить этот текст так же, как и для любого другого сообщения.

# <a name="c"></a>[C#](#tab/dotnet)

Вы можете проанализировать часть **\@** упоминания текста сообщения с помощью статического метода, предоставленного Microsoft Bot Framework. Это метод класса с именем `Activity` `RemoveRecipientMention`.

Код C# для синтаксического **\@** анализа части Упоминания в тексте сообщения выглядит следующим образом:

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Вы можете проанализировать часть **\@** упоминания текста сообщения с помощью статического метода, предоставленного в Bot Framework. Это метод класса с именем `TurnContext` `removeMentionText`.

Код JavaScript для синтаксического анализа **\@части упоминания** в тексте сообщения выглядит следующим образом:

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

Вы можете проанализировать @Mention текст сообщения  с помощью статического метода, предоставленного в Bot Framework. Это метод класса с именем `TurnContext` `remove_recipient_mention`.

Код Python для синтаксического анализа части **\@упоминания** в тексте сообщения выглядит следующим образом:

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

Чтобы обеспечить бесперебойную работу кода бота, необходимо следовать нескольким рекомендациям.

## <a name="command-menu-best-practices"></a>Рекомендации по использованию командного меню

Ниже приведены рекомендации по использованию командного меню.

* Укажите простое: меню бота предназначено для представления ключевых возможностей бота.
* Будьте кратки: параметры меню не должны быть длинными и не должны быть сложными операторами естественного языка. Они должны быть простыми командами.
* Оставьте ее доступной: действия или команды меню бота всегда должны быть доступны независимо от состояния беседы или диалогового окна, в который находится бот.

> [!NOTE]
> При удалении каких-либо команд из манифеста необходимо повторно развернуть приложение для реализации изменений. Как правило, любые изменения манифеста требуют повторного развертывания приложения.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Канал и групповые разговоры](~/bots/how-to/conversations/channel-and-group-conversations.md)
