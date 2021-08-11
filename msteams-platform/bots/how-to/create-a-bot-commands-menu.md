---
title: Создание меню команд для бота
author: surbhigupta
description: Создание командного меню для Microsoft Teams бота
ms.topic: how-to
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 978c34a950669386464037850601878a98c191c50710cc62c556f4104ad325e6
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2021
ms.locfileid: "57704093"
---
# <a name="bot-command-menus"></a>Меню команд бота

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Чтобы определить набор основных команд, на которые может отвечать бот, можно добавить меню команд со списком команд для бота. Список команд представлен пользователям в области составить сообщение, когда они находятся в беседе с ботом. Выберите команду из списка, чтобы вставить строку команды в поле составить сообщение и выбрать **Отправить**.

# <a name="desktop"></a>[Классическая версия](#tab/desktop)

![Меню команд бота](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[Мобильная версия](#tab/mobile)

![Меню команды мобильных ботов](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a>Создание меню команд для бота

Меню команд определяется в манифесте приложения. Для их создания можно использовать **App Studio** или вручную добавлять их в манифест приложения.

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>Создание командного меню для бота с помощью App Studio

Обязательным условием для создания командного меню для бота является то, что необходимо изменить существующий манифест приложения. Действия по добавлению меню команд одинаковы, независимо от того, создаете ли вы новый манифест или редактируете существующий.

**Создание командного меню для бота с помощью App Studio**

1. Откройте Teams и выберите **Приложения** с левой области. На странице **Приложения** ищите **App Studio** и выберите **Open**. 
   > [!NOTE]
   > Если у вас нет **App Studio,** вы можете скачать его. Дополнительные сведения см. в [записи установки App Studio.](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio)

    ![App Studio](./conversations/media/AppStudio.png)

2. В **App Studio** выберите **вкладку Редактор Манифеста.** Если у вас нет существующего пакета приложений, можно создать или импортировать существующее приложение. Дополнительные сведения см. [в обновленном пакете приложений.](~/get-started/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package)

3. В левой области редактора **Манифеста** и в разделе **Возможности** выберите **Bots**.

4. В правой области редактора **Манифеста** и в разделе **Команды** выберите **Добавить**. Появится экран **New Command.**

    ![Меню Добавить кнопку Добавить меню App Studio](./conversations/media/AppStudio-CommandMenu-Add.png)

5. Введите **командный текст,** который должен отображаться в качестве командного меню для бота.

6. Введите **текст справки,** который должен отображаться в тексте команды в меню. **Текст справки** должен быть кратким объяснением цели команды.

7. Выберите **флажки Область,** чтобы выбрать, где должно отображаться это командное меню, и выберите **Сохранить**.

    ![Кнопка меню меню App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Создание командного меню для бота путем редактирования Manifest.jsна

Другой способ создания командного меню — это создание его непосредственно в файле манифеста при разработке исходных кодов бота. Чтобы использовать этот метод, следуйте следующим пунктам:

* Каждое меню поддерживает до десяти команд.
* Создайте одно командное меню, которое работает во всех сферах.
* Создайте другое меню команд для каждой области.

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>Пример манифеста для одного меню для обеих областей

Пример кода манифеста для одного меню для обеих областей:

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

Пример кода манифеста для меню для каждой области:

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

Вы должны обрабатывать команды меню в коде бота при обработке любых сообщений от пользователей. Вы можете обрабатывать команды меню в коде бота, разобрав часть **\@ упоминания** текста сообщения.

## <a name="handle-menu-commands-in-your-bot-code"></a>Обработка команд меню в коде бота

Боты в группе или канале отвечают только тогда, когда они упоминаются `@botname` в сообщении. Каждое сообщение, полученное ботом, когда в области группы или канала содержит свое имя в возвращаемом тексте сообщения. Перед обработкой возвращаемой команды необходимо обработать сообщение, полученное ботом с его именем.

> [!NOTE]
> Для обработки команд в коде они отправляются вашему боту в качестве регулярного сообщения. Вы должны обрабатывать их так же, как и любое другое сообщение от пользователей. Команды в коде вставляют предварительно настроенный текст в текстовое поле. Затем пользователь должен отправить этот текст так же, как и любое другое сообщение.

# <a name="c"></a>[C#](#tab/dotnet)

Вы можете разсмеять часть **\@ Упоминания** текста сообщения с помощью статического метода, предоставленного Microsoft Bot Framework. Это метод класса `Activity` с именем `RemoveRecipientMention` .

Код C# для размывки части **\@ Упоминания** текста сообщения следующим образом:

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Вы можете разсмеять часть **\@ Упоминания** текста сообщения с помощью статического метода, предоставленного с помощью Bot Framework. Это метод класса `TurnContext` с именем `removeMentionText` .

Код JavaScript для размыва части **\@ Упоминания** текста сообщения следующим образом:

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

Вы можете разобрать  @Mention текст сообщения с помощью статического метода, предоставленного с помощью Bot Framework. Это метод класса `TurnContext` с именем `remove_recipient_mention` .

Код Python для размывки части **\@ Упоминания** текста сообщения следующим образом:

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

Чтобы обеспечить бесперебойную работу кода бота, необходимо придерживаться нескольких методов.

## <a name="command-menu-best-practices"></a>Лучшие практики меню команд

Ниже ниже ниже приводится пример лучших практик меню команд:

* Сохраняйте простое: меню бота предназначено для того, чтобы представить основные возможности вашего бота.
* Кратко: параметры меню не должны быть длинными и не должны быть сложными естественными языковыми утверждениями. Они должны быть простыми командами.
* Сохраняйте его на словах: действия или команды меню бота всегда должны быть доступны, независимо от состояния беседы или диалоговом окне, в который находится бот.

> [!NOTE]
> Если вы удалите какие-либо команды из манифеста, необходимо изменить приложение для реализации изменений. Как правило, любые изменения манифеста требуют переделок вашего приложения.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Канал и групповые разговоры](~/bots/how-to/conversations/channel-and-group-conversations.md)
