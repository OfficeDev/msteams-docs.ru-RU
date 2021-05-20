---
title: Добавление действий карты в бота
description: Описывает действия карты в Microsoft Teams и как их использовать в ботах
localization_priority: Normal
ms.topic: conceptual
keywords: команды ботов карты действия
ms.openlocfilehash: b9276c7197070df43ba447707e6fa4d3d4098591
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566854"
---
# <a name="card-actions"></a>Действия карты

Карты, используемые ботами и расширениями обмена сообщениями Teams для поддержки следующих типов [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) активности () . Обратите внимание, что эти действия `potentialActions` отличаются от Office 365 connector при использовании из Connectors.

| Тип | Действие |
| --- | --- |
| `openUrl` | Открывает URL-адрес в браузере по умолчанию. |
| `messageBack` | Отправляет сообщение и полезную нагрузку боту от пользователя, который нажал на кнопку или нажал на карту и отправил отдельное сообщение в поток чата. |
| `imBack`| Отправляет сообщение боту от пользователя, который нажал на кнопку или нажал на карту. Это сообщение (от пользователя к боту) видно всем участникам беседы. |
| `invoke` | Отправляет сообщение и полезную нагрузку боту от пользователя, который нажал на кнопку или нажал на карту. Это сообщение не видно. |
| `signin` | Инициирует поток OAuth, позволяя ботам подключаться к безопасным службам. |

> [!NOTE]
>* Teams не поддерживает `CardAction` типы, не перечисленные в предыдущей таблице.
>* Teams не поддерживает `potentialActions` свойство.
>* Действия карты отличаются от [предлагаемых действий](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) в службе Bot Framework/Azure Bot. Предлагаемые действия не поддерживаются в Microsoft Teams: если вы хотите, чтобы кнопки Teams сообщении бота, используйте карту.
>* Если вы используете действие карты в рамках расширения обмена сообщениями, действия не работают до тех пор, пока карта не будет отправлена каналу. Они не работают, пока карта находится в поле для составления сообщений.

Teams поддерживает действия [Adaptive Cards,](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)которые используются только адаптивными картами. Эти действия перечислены в их собственном разделе в конце этой ссылки.

## <a name="openurl"></a>openUrl

Этот тип действия определяет URL для запуска в браузере по умолчанию. Обратите внимание, что ваш бот не получает никакого уведомления о том, какая кнопка была нажата.

Поле `value` должно содержать полный и правильно сформированный URL.

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>messageBack

С `messageBack` помощью, вы можете создать полностью настроенные действия со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается как метка кнопки. |
| `displayText` | Необязательный элемент. Вторит пользователю в поток чата, когда действие выполняется. Этот текст не *отправляется* вашему боту. |
| `value` | Отправлено вашему боту, когда действие выполняется. Контекст для действия можно кодировать, например, уникальные идентификаторы или объект JSON. |
| `text` | Отправлено вашему боту, когда действие выполняется. Используйте это свойство для упрощения разработки бота: ваш код может проверить одно свойство верхнего уровня для отправки логики бота. |

Гибкость средств, `messageBack` которые ваш код может выбрать, чтобы не оставлять видимое сообщение пользователя в истории, просто не используя `displayText` .

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

Свойство `value` может быть либо сериализованной строкой JSON, либо объектом JSON.

### <a name="inbound-message-example"></a>Пример входящих сообщений

`replyToId` содержит идентификатор сообщения, от которого пришло действие карты. Используйте его, если вы хотите обновить сообщение.

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

## <a name="imback"></a>imBack

Это действие запускает возврат сообщения для вашего бота, как если бы пользователь набрал его в обычном сообщении чата. Ваш пользователь, и все другие пользователи, если в канале, увидите, что кнопка ответа.

Поле `value` должно содержать текстовую строку, вторя в чате, и поэтому отправлено обратно боту. Это текст сообщения, который вы обработать в вашем боте для выполнения желаемой логики. Примечание: это поле является простой строкой - нет поддержки для форматирования или скрытых символов.

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>взывать

Действие `invoke` используется для вызова [модулей задач.](~/task-modules-and-cards/task-modules/task-modules-bots.md)

Действие `invoke` содержит три свойства: , и `type` `title` `value` . Свойство `value` может содержать строку, струнный объект JSON или объект JSON.

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

Когда пользователь нажимает на кнопку, ваш бот получит объект с `value` некоторой дополнительной информацией. Пожалуйста, обратите внимание, что тип действия `invoke` будет вместо `message` ( `activity.Type == "invoke"` ).

### <a name="example-invoke-button-definition-net"></a>Пример: Определение кнопки вызова (.NET)

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>Пример: Входящее сообщение вызова

Свойство верхнего `replyToId` уровня содержит идентификатор сообщения, откуда пришло действие карты. Используйте его, если вы хотите обновить сообщение.

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

## <a name="signin"></a>signin

Инициирует поток OAuth, позволяя ботам связаться с безопасными службами, как описано более подробно здесь: [Поток аутентификации в ботах.](~/bots/how-to/authentication/auth-flow-bot.md)

## <a name="adaptive-cards-actions"></a>Действия адаптивных карт

Адаптивные карты поддерживают четыре типа действий:

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Exeмило](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

В дополнение к действиям, упомянутым выше, вы можете изменить полезную нагрузку Adaptive Card `Action.Submit` для поддержки существующих действий Bot `msteams` Framework, используя `data` свойство в `Action.Submit` объекте. В нижесемейных разделах подробно описано, как использовать существующие действия Bot Framework с помощью адаптивных карт.

> [!NOTE]
> Добавление `msteams` к данным с действием Bot Framework не работает с модулем задач Adaptive Card.

### <a name="adaptive-cards-with-messageback-action"></a>Адаптивные карты с действием messageBack

Чтобы включить действие `messageBack` с адаптивной картой, включите в объект следующие `msteams` детали. Обратите внимание, что при необходимости в объект могут быть включены `data` дополнительные скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установить для `messageBack` |
| `displayText` | Необязательный элемент. Вторит пользователю в поток чата, когда действие выполняется. Этот текст не *отправляется* вашему боту. |
| `value` | Отправлено вашему боту, когда действие выполняется. Контекст для действия можно кодировать, например, уникальные идентификаторы или объект JSON. |
| `text` | Отправлено вашему боту, когда действие выполняется. Используйте это свойство для упрощения разработки бота: ваш код может проверить одно свойство верхнего уровня для отправки логики бота. |

#### <a name="example"></a>Пример

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

Чтобы включить действие `imBack` с адаптивной картой, включите в объект следующие `msteams` детали. Обратите внимание, что при необходимости в объект могут быть включены `data` дополнительные скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установить для `imBack` |
| `value` | Строка, которая должна быть повторена обратно в чате |

#### <a name="example"></a>Пример

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

### <a name="adaptive-cards-with-signin-action"></a>Адаптивные карты с сигнином действий

Чтобы включить действие `signin` с адаптивной картой, включите в объект следующие `msteams` детали. Обратите внимание, что при необходимости в объект могут быть включены `data` дополнительные скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установить на `signin` . |
| `value` | Установите URL-адрес, на который вы хотите перенаправить.  |

#### <a name="example"></a>Пример

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
 
Чтобы включить действие `invoke` с адаптивной картой, включите в объект следующие `msteams` детали. Обратите внимание, что при необходимости в объект могут быть включены `data` дополнительные скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установить для `task/fetch` |
| `data` | Установить значение  |

#### <a name="example"></a>Пример

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

#### <a name="example-2-with-additional-payload-data"></a>Пример 2 (с дополнительными данными полезной нагрузки)

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
