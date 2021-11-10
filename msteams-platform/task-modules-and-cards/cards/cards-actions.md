---
title: Добавление действий карточек в бот
description: Описание действий карточек в Microsoft Teams и их использования в ботах
ms.localizationpriority: medium
ms.topic: conceptual
keywords: teams действия карточек боты
ms.openlocfilehash: 3509ab49f8e2031176743a9330ee3b6757b70277
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889330"
---
# <a name="card-actions"></a>Действия карточек

Карточки, используемые ботами и расширениями для обмена сообщениями в Teams, поддерживают следующие типы действий [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards):

> [!NOTE]
> Действия `CardAction` отличаются от `potentialActions` для карточек соединителей Office 365 при их использовании из соединителей.

| Тип | Действие |
| --- | --- |
| `openUrl` | Открывает URL-адрес в браузере по умолчанию. |
| `messageBack` | Отправляет боту сообщение и полезные данные от пользователя, нажавшего кнопку или коснувшегося карточки. Отправляет отдельное сообщение в поток чата. |
| `imBack`| Отправляет боту сообщение от пользователя, нажавшего кнопку или коснувшегося карточки. Это сообщение от пользователя боту отображается для всех участников беседы. |
| `invoke` | Отправляет боту сообщение и полезные данные от пользователя, нажавшего кнопку или коснувшегося карточки. Это сообщение не отображается. |
| `signin` | Инициирует поток OAuth, позволяя ботам подключаться к защищенным службам. |

> [!NOTE]
>* Teams не поддерживает типы `CardAction`, не указанные в предыдущей таблице.
>* Teams не поддерживает свойство `potentialActions`.
>* Действия с карточками отличаются от [рекомендуемых действий](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) в Bot Framework или службе Azure Bot. Рекомендуемые действия не поддерживаются в Microsoft Teams. Если вы хотите, чтобы в сообщении бота Teams появлялись кнопки, используйте карточку.
>* Если вы используете действие карточки в расширении для обмена сообщениями, эти действия не будут работать, пока карточка не будет отправлена в канал. Действия не работают, пока карточка находится в окне составления сообщения.

## <a name="action-type-openurl"></a>Тип действия openUrl

Тип действия `openUrl` указывает URL-адрес, который необходимо открыть в браузере по умолчанию.

> [!NOTE]
> Бот не получает уведомления о том, какая нажата кнопка.

С помощью `openUrl` вы можете создать действие со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается как метка кнопки. |
| `value` | Это поле должно содержать полный и правильно оформленный URL-адрес. |

# <a name="json"></a>[JSON](#tab/json)

Следующий код представляет собой пример типа действия `openUrl` в JSON:

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[C#](#tab/csharp)

Следующий код представляет собой пример типа действия `openUrl` в C#:

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

Следующий код представляет собой пример типа действия `openUrl` в JavaScript:

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a>Тип действия messageBack

С помощью `messageBack` вы можете создать полностью настроенное действие со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается как метка кнопки. |
| `displayText` | Необязательное. Применяется пользователем в потоке чата при выполнении действия. Этот текст не отправляется вашему боту. |
| `value` | Отправляется боту при выполнении действия. Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON. |
| `text` | Отправляется боту при выполнении действия. Используйте это свойство, чтобы упростить разработку бота. Ваш код может проверить одно свойство верхнего уровня для выполнения логики бота. |

Гибкость `messageBack` означает, что ваш код не может оставить видимое сообщение пользователя в журнале, просто не используя `displayText`.

# <a name="json"></a>[JSON](#tab/json)

Следующий код представляет собой пример типа действия `messageBack` в JSON:

```json
{
  "buttons": [
    {
    "type": "messageBack",
    "title": "My MessageBack button",
    "displayText": "I clicked this button",
    "text": "User just clicked the MessageBack button",
    "value": "{\"property\": \"propertyValue\" }"
    }
  ]
}
```

Свойство `value` может быть сериализованной строкой JSON или объектом JSON.

# <a name="c"></a>[C#](#tab/csharp)

Следующий код представляет собой пример типа действия `messageBack` в C#:

```csharp
var button = new CardAction()
{
    Type = ActionTypes.MessageBack,
    Title = "My MessageBack button",
    DisplayText = "I clicked this button",
    Text = "User just clicked the MessageBack button",
    Value = "{\"property\": \"propertyValue\" }"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

Следующий код представляет собой пример типа действия `messageBack` в JavaScript:

```javascript
CardFactory.actions([
{
    type: 'messageBack',
    title: "My MessageBack button",
    displayText: "I clicked this button",
    text: "User just clicked the MessageBack button",
    value: {property: "propertyValue" }
}])
```

---

### <a name="inbound-message-example"></a>Пример входящего сообщения

`replyToId` содержит идентификатор сообщения, от которого поступило действие карточки. Используйте его, если вы хотите обновить сообщение.

Следующий код представляет собой пример входящего сообщения:

```json
{
   "text":"User just clicked the MessageBack button",
   "value":{
      "property":"propertyValue"
   },
   "type":"message",
   "timestamp":"2017-06-22T22:38:47.407Z",
   "id":"f:5261769396935243054",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:102jd210jd010icsoaeclaejcoa9ue09u",
      "name":"John Smith"
   },
   "conversation":{
      "id":"19:malejcou081i20ojmlcau0@thread.skype;messageid=1498171086622"
   },
   "recipient":{
      "id":"28:76096e45-119f-4736-859c-6dfff54395f7",
      "name":"MyBot"
   },
   "entities":[
      {
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo" 
      }
   ],
   "channelData":{
      "channel":{
         "id":"19:malejcou081i20ojmlcau0@thread.skype"
      },
      "team":{
         "id":"19:12d021jdoijsaeoaue0u@thread.skype"
      },
      "tenant":{
         "id":"bec8e231-67ad-484e-87f4-3e5438390a77"
      }
   },
        "replyToId": "1575667808184",
}
```

## <a name="action-type-imback"></a>Тип действия imBack

Действие `imBack` вызывает обратное сообщение боту, как если бы пользователь ввел его в обычном сообщении чата. Ваш пользователь и все остальные пользователи канала могут видеть ответ, отправленный с использованием кнопки.

С помощью `imBack` вы можете создать действие со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается как метка кнопки. |
| `value` | Это поле должно содержать текстовую строку, используемую в чате и, следовательно, отправляемую обратно боту. Это текст сообщения, который вы обрабатываете в боте для выполнения нужной логики. |

> [!NOTE]
> Поле `value` является простой строкой. Форматирование и скрытые символы не поддерживаются.

# <a name="json"></a>[JSON](#tab/json)

Следующий код представляет собой пример типа действия `imBack` в JSON:

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[C#](#tab/csharp)

Следующий код представляет собой пример типа действия `imBack` в C#:

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

Следующий код представляет собой пример типа действия `imBack` в JavaScript:

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a>Тип действия invoke

Действие `invoke` используется для вызова [модулей задач](~/task-modules-and-cards/task-modules/task-modules-bots.md).

Действие `invoke` содержит три свойства: `type`, `title` и `value`.

С помощью `invoke` вы можете создать действие со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается как метка кнопки. |
| `value` | Это свойство может содержать строку, строковый объект JSON или объект JSON. |

# <a name="json"></a>[JSON](#tab/json)

Следующий код представляет собой пример типа действия `invoke` в JSON:

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

Когда пользователь нажимает кнопку, бот получает объект `value` с некоторой дополнительной информацией.

> [!NOTE]
> Тип действия `invoke`, а не `message`, т. е. `activity.Type == "invoke"`.

# <a name="c"></a>[C#](#tab/csharp)

Следующий код представляет собой пример типа действия `invoke` в C#:

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

Следующий код представляет собой пример типа действия `invoke` в Node.js:

```javascript
CardFactory.actions([
{
    type: "invoke",
    title: "Option 1",
    value: {
        option: "opt1"
    }
}])
```

---

### <a name="example-of-incoming-invoke-message"></a>Пример входящего сообщения invoke

Свойство `replyToId` верхнего уровня содержит идентификатор сообщения, от которого поступило действие карточки. Используйте его, если вы хотите обновить сообщение.

Следующий код представляет собой пример входящего сообщения invoke:

```json
{
    "type": "invoke",
    "value": {
        "option": "opt1"
    },
    "timestamp": "2017-02-10T04:11:19.614Z",
    "localTimestamp": "2017-02-09T21:11:19.614-07:00",
    "id": "f:6894910862892785420",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1Eniglq0-uVL83xNB9GU6w_G5a4SZF0gcJLprZzhtEbel21G_5h-
    NgoprRw45mP0AXUIZVeqrsIHSYV4ntgfVJQ",
        "name": "John Doe"
    },
    "conversation": {
        "id": "19:97b1ec61-45bf-453c-9059-6e8984e0cef4_8d88f59b-ae61-4300-bec0-caace7d28446@unq.gbl.spaces"
    },
    "recipient": {
        "id": "28:8d88f59b-ae61-4300-bec0-caace7d28446",
        "name": "MyBot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Web",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "channel": {
            "id": "19:dc5ba12695be4eb7bf457cad6b4709eb@thread.skype"
        },
        "team": {
            "id": "19:712c61d0ef384e5fa681ba90ca943398@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

## <a name="action-type-signin"></a>Тип действия signin

Тип действия `signin` инициирует поток OAuth, который позволяет ботам подключаться к защищенным службам. Дополнительные сведения см. в статье о [потоке проверки подлинности в ботах](~/bots/how-to/authentication/auth-flow-bot.md).

Teams также поддерживает [действия адаптивных карточек](#adaptive-cards-actions) которые используются только в адаптивных карточках.

# <a name="json"></a>[JSON](#tab/json)

Следующий код представляет собой пример типа действия `signin` в JSON:

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[C#](#tab/csharp)

Следующий код представляет собой пример типа действия `signin` в C#:

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

Следующий код представляет собой пример типа действия `signin` в JavaScript:

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a>Действия адаптивных карточек

Адаптивные карточки поддерживают четыре типа действий:

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

Кроме того, вы можете изменить полезные данные адаптивной карточки `Action.Submit` для поддержки существующих действий Bot Framework с помощью свойства `msteams` в объекте `data`, относящемся к `Action.Submit`. Следующий раздел посвящен использованию существующих действий Bot Framework с адаптивными карточками.

> [!NOTE]
> Добавление `msteams` к данным с помощью действия Bot Framework не работает с модулем задач адаптивной карточки.

### <a name="adaptive-cards-with-messageback-action"></a>Адаптивные карточки с действием messageBack

Чтобы включить действие `messageBack` в адаптивную карточку, включите в объект `msteams` следующую информацию:

> [!NOTE]
> При необходимости можно включить в объект `data` дополнительные скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установите значение `messageBack`. |
| `displayText` | Необязательное. Применяется пользователем в потоке чата при выполнении действия. Этот текст не отправляется вашему боту. |
| `value` | Отправляется боту при выполнении действия. Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON. |
| `text` | Отправляется боту при выполнении действия. Используйте это свойство, чтобы упростить разработку бота. Ваш код может проверить одно свойство верхнего уровня для выполнения логики бота. |

Следующий код представляет собой пример адаптивных карточек с действием `messageBack`:

```json
{
  "type": "Action.Submit",
  "title": "Click me for messageBack",
  "data": {
    "msteams": {
        "type": "messageBack",
        "displayText": "I clicked this button",
        "text": "text to bots",
        "value": "{\"bfKey\": \"bfVal\", \"conflictKey\": \"from value\"}"
    }
  }
}
```

### <a name="adaptive-cards-with-imback-action"></a>Адаптивные карточки с действием imBack

Чтобы включить действие `imBack` в адаптивную карточку, включите в объект `msteams` следующую информацию:

> [!NOTE]
> При необходимости можно включить в объект `data` дополнительные скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установите значение `imBack`. |
| `value` | Строка, которую необходимо вернуть в чат. |

Следующий код представляет собой пример адаптивных карточек с действием `imBack`:

```json
{
  "type": "Action.Submit",
  "title": "Click me for imBack",
  "data": {
    "msteams": {
        "type": "imBack",
        "value": "Text to reply in chat"
    }
  }
}
```

### <a name="adaptive-cards-with-signin-action"></a>Адаптивные карточки с действием signin

Чтобы включить действие `signin` в адаптивную карточку, включите в объект `msteams` следующую информацию:

> [!NOTE]
> При необходимости можно включить в объект `data` дополнительные скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установите значение `signin`. |
| `value` | В качестве значения задайте URL-адрес для перенаправления.  |

Следующий код представляет собой пример адаптивных карточек с действием `signin`:

```json
{
  "type": "Action.Submit",
  "title": "Click me for signin",
  "data": {
    "msteams": {
        "type": "signin",
        "value": "https://signin.com"
    }
  }
}
```

### <a name="adaptive-cards-with-invoke-action"></a>Адаптивные карточки с действием invoke

Чтобы включить действие `invoke` в адаптивную карточку, включите в объект `msteams` следующую информацию:

> [!NOTE]
> При необходимости можно включить в объект `data` дополнительные скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установите значение `task/fetch`. |
| `data` | Задайте значение.  |

Следующий код представляет собой пример адаптивных карточек с действием `invoke`:

```json
{
  "type": "Action.Submit",
  "title": "submit",
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

Следующий код представляет собой пример адаптивных карточек с действием `invoke` и дополнительными полезными данными:

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    },
    "Value1": "some value"
  }
}
```
## <a name="next-step"></a>Следующее действие

> [!div class="nextstepaction"]
> [Универсальные действия для адаптивных карточек](../cards/Universal-actions-for-adaptive-cards/Overview.md)

## <a name="see-also"></a>См. также

* [Справочные материалы о карточках](./cards-reference.md)
* [Использование модулей задач из ботов](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [Адаптивные карты в ботах](../../bots/how-to/conversations/conversation-messages.md#adaptive-cards)
* [Универсальные действия для адаптивных карточек](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md)
