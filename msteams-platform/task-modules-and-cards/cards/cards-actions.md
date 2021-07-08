---
title: Добавление действий карты в боте
description: Описывает действия карт в Microsoft Teams и их использование в ботах
localization_priority: Normal
ms.topic: conceptual
keywords: teams bots cards actions
ms.openlocfilehash: 4af152f6179785687d4fd7371d202c56e1aee170
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254204"
---
# <a name="card-actions"></a>Действия карточек

Карты, используемые ботами и расширениями обмена сообщениями в Teams поддерживают следующие [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) типы действий:

> [!NOTE]
> Действия `CardAction` отличаются от `potentialActions` Office 365 соединители, когда используются соединители.

| Type | Action |
| --- | --- |
| `openUrl` | Открывает URL-адрес в браузере по умолчанию. |
| `messageBack` | Отправляет сообщение и полезное сообщение боту от пользователя, который выбрал кнопку или постучал по карте. Отправляет отдельное сообщение в поток чата. |
| `imBack`| Отправляет сообщение боту от пользователя, который выбрал кнопку или постучал по карте. Это сообщение от пользователя к боту видно всем участникам беседы. |
| `invoke` | Отправляет сообщение и полезное сообщение боту от пользователя, который выбрал кнопку или постучал по карте. Это сообщение не отображается. |
| `signin` | Инициирует поток OAuth, позволяя ботам подключаться к безопасным службам. |

> [!NOTE]
>* Teams не поддерживает `CardAction` типы, не указанные в предыдущей таблице.
>* Teams не поддерживает `potentialActions` свойство.
>* Действия карт отличаются от [предлагаемых действий](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) в Bot Framework или Azure Bot Service. Предлагаемые действия не поддерживаются в Microsoft Teams. Если вы хотите, чтобы в сообщении бота Teams кнопки, используйте карточку.
>* Если вы используете действие карты в рамках расширения обмена сообщениями, эти действия не будут работать до отправки карты в канал. Действия не работают, пока карта находится в поле составить сообщение.

## <a name="action-type-openurl"></a>Тип действия openUrl

`openUrl` Тип действия указывает URL-адрес для запуска в браузере по умолчанию.

> [!NOTE]
> Ваш бот не получает уведомления о выборе кнопки.

С помощью этого действия можно `openUrl` создать действие со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается как метка кнопки. |
| `value` | Это поле должно содержать полный и правильно сформированный URL-адрес. |

# <a name="json"></a>[JSON](#tab/json)

В следующем коде показан пример `openUrl` типа действия в JSON:

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[C#](#tab/csharp)

В следующем коде показан пример типа действия `openUrl` в C#:

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

В следующем коде показан пример типа `openUrl` действий в JavaScript:

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a>MessageBack типа действия

С `messageBack` помощью этого параметра можно создать полностью настраиваемые действия со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается как метка кнопки. |
| `displayText` | Необязательно. Используется пользователем в потоке чата при выполнении действия. Этот текст не отправляется в бот. |
| `value` | Отправляется в бот при выполнении действия. Вы можете кодировать контекст для действия, например уникальные идентификаторы или объект JSON. |
| `text` | Отправляется в бот при выполнении действия. Используйте это свойство для упрощения разработки ботов. Код может проверить одно свойство верхнего уровня для отправки логики бота. |

Гибкость означает, что код не может оставить видимое сообщение пользователя в истории, просто `messageBack` не используя `displayText` .

# <a name="json"></a>[JSON](#tab/json)

В следующем коде показан пример `messageBack` типа действия в JSON:

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

Свойство `value` может быть как сериализированной строкой JSON, так и объектом JSON.

# <a name="c"></a>[C#](#tab/csharp)

В следующем коде показан пример типа действия `messageBack` в C#:

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

В следующем коде показан пример типа `messageBack` действий в JavaScript:

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

### <a name="inbound-message-example"></a>Пример входящие сообщения

`replyToId` содержит ID сообщения, из которое пришло действие карты. Используйте его, если вы хотите обновить сообщение.

В следующем коде показан пример входящие сообщения:

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

Действие вызывает возвращение сообщения в бот, как если бы пользователь впечатлл `imBack` его в обычном сообщении чата. Пользователь и все другие пользователи канала могут видеть отклик кнопки.

С помощью этого действия можно `imBack` создать действие со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается как метка кнопки. |
| `value` | Это поле должно содержать текстовую строку, используемую в чате, и поэтому отправляется обратно в бот. Это текст сообщения, который вы обрабатываете в боте для выполнения нужной логики. |

> [!NOTE]
> Поле `value` — это простая строка. Нет поддержки форматирования или скрытых символов.

# <a name="json"></a>[JSON](#tab/json)

В следующем коде показан пример `imBack` типа действия в JSON:

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[C#](#tab/csharp)

В следующем коде показан пример типа действия `imBack` в C#:

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

В следующем коде показан пример типа `imBack` действий в JavaScript:

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a>Вызов типа действия

Действие `invoke` используется для наводки [модулей задач.](~/task-modules-and-cards/task-modules/task-modules-bots.md)

Действие `invoke` содержит три `type` свойства, и `title` `value` .

С помощью этого действия можно `invoke` создать действие со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается как метка кнопки. |
| `value` | Это свойство может содержать строку, объект JSON или объект JSON. |

# <a name="json"></a>[JSON](#tab/json)

В следующем коде показан пример `invoke` типа действия в JSON:

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

Когда пользователь выбирает кнопку, бот получает объект `value` с некоторыми дополнительными сведениями.

> [!NOTE]
> Вместо этого тип действия `invoke` `message` `activity.Type == "invoke"` .

# <a name="c"></a>[C#](#tab/csharp)

В следующем коде показан пример типа действия `invoke` в C#:

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

В следующем коде показан пример типа действия `invoke` в Node.js:

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

### <a name="example-of-incoming-invoke-message"></a>Пример входящих сообщений вызова

Свойство верхнего уровня содержит ID сообщения, из которое `replyToId` пришло действие карты. Используйте его, если вы хотите обновить сообщение.

В следующем коде показан пример входящих сообщений вызова:

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

## <a name="action-type-signin"></a>Знак типа действия

`signin` Тип действия инициирует поток OAuth, который позволяет ботам подключаться к безопасным службам. Дополнительные сведения см. в [потоке проверки подлинности в ботах.](~/bots/how-to/authentication/auth-flow-bot.md)

Teams также поддерживает действия [адаптивных карт,](#adaptive-cards-actions) которые используются только адаптивными картами.

# <a name="json"></a>[JSON](#tab/json)

В следующем коде показан пример `signin` типа действия в JSON:

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[C#](#tab/csharp)

В следующем коде показан пример типа действия `signin` в C#:

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

В следующем коде показан пример типа `signin` действий в JavaScript:

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a>Действия адаптивных карт

Адаптивные карты поддерживают четыре типа действий:

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

Вы также можете изменить полезной нагрузки адаптивной карты для поддержки существующих действий Bot Framework с помощью свойства `Action.Submit` `msteams` в `data` объекте `Action.Submit` . В следующем разделе вы можете узнать, как использовать существующие действия Bot Framework с помощью адаптивных карт.

> [!NOTE]
> Добавление к данным с помощью действия Bot Framework не работает с модулем адаптивной `msteams` карты.

### <a name="adaptive-cards-with-messageback-action"></a>Адаптивные карты с действием messageBack

Чтобы включить `messageBack` действие с адаптивной картой, включим в объект следующие `msteams` сведения:

> [!NOTE]
> При необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установите `messageBack` для . |
| `displayText` | Необязательно. Используется пользователем в потоке чата при выполнении действия. Этот текст не отправляется в бот. |
| `value` | Отправляется в бот при выполнении действия. Вы можете кодировать контекст для действия, например уникальные идентификаторы или объект JSON. |
| `text` | Отправляется в бот при выполнении действия. Используйте это свойство для упрощения разработки ботов. Код может проверить одно свойство верхнего уровня для отправки логики бота. |

В следующем коде показан пример адаптивных карт с `messageBack` действием:

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

### <a name="adaptive-cards-with-imback-action"></a>Адаптивные карты с действием imBack

Чтобы включить `imBack` действие с адаптивной картой, включив в объект следующие `msteams` сведения:

> [!NOTE]
> При необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установите `imBack` для . |
| `value` | Строка, которую необходимо повторить в чате. |

В следующем коде показан пример адаптивных карт с `imBack` действием:

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

### <a name="adaptive-cards-with-signin-action"></a>Адаптивные карты с действием signin

Чтобы включить `signin` действие с адаптивной картой, включим в объект следующие `msteams` сведения:

> [!NOTE]
> При необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установите `signin` для . |
| `value` | Установите URL-адрес, в котором необходимо перенаправить.  |

В следующем коде показан пример адаптивных карт с `signin` действием:

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

### <a name="adaptive-cards-with-invoke-action"></a>Адаптивные карты с действием вызова

Чтобы включить `invoke` действие с адаптивной картой, включив в объект следующие `msteams` сведения:

> [!NOTE]
> При необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установите `task/fetch` для . |
| `data` | Установите значение.  |

В следующем коде показан пример адаптивных карт с `invoke` действием:

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

В следующем коде показан пример адаптивных карт с действием `invoke` с дополнительными данными полезной нагрузки:

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

## <a name="see-also"></a>См. также

[Ссылки на карточки](./cards-reference.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Универсальные действия для адаптивных карточек](../cards/Universal-actions-for-adaptive-cards/Overview.md)
