---
title: Добавление действий карты в боте
description: Описывает действия карт в Microsoft Teams и их использование в ботах
localization_priority: Normal
ms.topic: conceptual
keywords: teams bots cards actions
ms.openlocfilehash: b9276c7197070df43ba447707e6fa4d3d4098591
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566854"
---
# <a name="card-actions"></a>Действия карты

Карточки, используемые ботами и расширениями обмена сообщениями в Teams поддерживают следующие типы [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) действий (). Обратите внимание, что эти действия отличаются `potentialActions` от Office 365 соединители при их использования из соединители.

| Тип | Действие |
| --- | --- |
| `openUrl` | Открывает URL-адрес в браузере по умолчанию. |
| `messageBack` | Отправляет сообщение и полезное сообщение боту от пользователя, который нажал кнопку или постучал по карте и отправляет отдельное сообщение в поток чата. |
| `imBack`| Отправляет сообщение боту от пользователя, который нажал кнопку или постучал по карте. Это сообщение (от пользователя до бота) видно всем участникам беседы. |
| `invoke` | Отправляет сообщение и полезное сообщение боту от пользователя, который нажал кнопку или постучал по карте. Это сообщение не отображается. |
| `signin` | Инициирует поток OAuth, позволяя ботам подключаться к безопасным службам. |

> [!NOTE]
>* Teams не поддерживает `CardAction` типы, не указанные в предыдущей таблице.
>* Teams не поддерживает `potentialActions` свойство.
>* Действия карт отличаются от [предлагаемых действий](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) в службе bot Framework/Azure Bot. Предлагаемые действия не поддерживаются в Microsoft Teams: если вы хотите, чтобы в сообщении бота Teams кнопки, используйте карточку.
>* Если вы используете действие карты в рамках расширения обмена сообщениями, эти действия не будут работать до отправки карты в канал. Они не работают, пока карта находится в поле составить сообщение.

Teams также поддерживает действия [адаптивных](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)карт, которые используются только адаптивными картами. Эти действия перечислены в их собственном разделе в конце этой ссылки.

## <a name="openurl"></a>openUrl

Этот тип действия указывает URL-адрес для запуска в браузере по умолчанию. Обратите внимание, что ваш бот не получает уведомления о нажатии кнопки.

Поле `value` должно содержать полный и правильно сформированный URL-адрес.

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>messageBack

С `messageBack` помощью этого параметра можно создать полностью настраиваемые действия со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается как метка кнопки. |
| `displayText` | Необязательно. Вторил пользователю в поток чата при выполнении действия. Этот текст *не отправляется* в бот. |
| `value` | Отправляется в бот при выполнении действия. Вы можете кодировать контекст для действия, например уникальные идентификаторы или объект JSON. |
| `text` | Отправляется в бот при выполнении действия. Используйте это свойство для упрощения разработки ботов: код может проверить одно свойство верхнего уровня для отправки логики бота. |

Гибкость означает, что код может не оставлять видимое сообщение пользователя в истории, просто `messageBack` не используя `displayText` .

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

### <a name="inbound-message-example"></a>Пример входящие сообщения

`replyToId` содержит ID сообщения, из которое пришло действие карты. Используйте его, если вы хотите обновить сообщение.

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

Это действие вызывает возвращение сообщения в бот, как если бы пользователь впечатлл его в обычном сообщении чата. Пользователь и все другие пользователи, если в канале, увидят ответ на эту кнопку.

Поле должно содержать текстовую строку, повторяемую в чате и, `value` следовательно, отправленную обратно в бот. Это текст сообщения, который будет обрабатываться в боте для выполнения нужной логики. Примечание. Это поле — простая строка — нет поддержки форматирования или скрытых символов.

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>вызов

Действие `invoke` используется для наводки [модулей задач.](~/task-modules-and-cards/task-modules/task-modules-bots.md)

Действие `invoke` содержит три свойства: и `type` `title` `value` . Свойство `value` может содержать строку, объект JSON или объект JSON.

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

Когда пользователь нажмет кнопку, бот получит `value` объект с дополнительной информацией. Обратите внимание, что тип действия будет вместо `invoke` `message` `activity.Type == "invoke"` ().

### <a name="example-invoke-button-definition-net"></a>Пример: Определение кнопки вызова (.NET)

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>Пример: Входящий вызов сообщения

Свойство верхнего уровня содержит ID сообщения, из которое `replyToId` пришло действие карты. Используйте его, если вы хотите обновить сообщение.

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

Инициирует поток OAuth, позволяющий ботам подключаться к безопасным службам, как описано более подробно здесь: поток проверки подлинности [в ботах.](~/bots/how-to/authentication/auth-flow-bot.md)

## <a name="adaptive-cards-actions"></a>Действия адаптивных карт

Адаптивные карты поддерживают четыре типа действий:

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Exeмило](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

В дополнение к указанным выше действиям вы можете изменить полезной нагрузки адаптивной карты для поддержки существующих действий Bot Framework с помощью свойства `Action.Submit` `msteams` в `data` объекте `Action.Submit` . В ниженазванных разделах подробно излагается, как использовать существующие действия Bot Framework с адаптивными картами.

> [!NOTE]
> Добавление к данным с помощью действия Bot Framework не работает с модулем адаптивной `msteams` карты.

### <a name="adaptive-cards-with-messageback-action"></a>Адаптивные карты с действием messageBack

Чтобы включить `messageBack` действие с адаптивной картой, включив в объект следующие `msteams` сведения. Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установлено, что `messageBack` |
| `displayText` | Необязательно. Вторил пользователю в поток чата при выполнении действия. Этот текст *не отправляется* в бот. |
| `value` | Отправляется в бот при выполнении действия. Вы можете кодировать контекст для действия, например уникальные идентификаторы или объект JSON. |
| `text` | Отправляется в бот при выполнении действия. Используйте это свойство для упрощения разработки ботов: код может проверить одно свойство верхнего уровня для отправки логики бота. |

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

Чтобы включить `imBack` действие с адаптивной картой, включив в объект следующие `msteams` сведения. Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установлено, что `imBack` |
| `value` | Строка, которую необходимо повторить в чате |

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

### <a name="adaptive-cards-with-signin-action"></a>Адаптивные карты с действием signin

Чтобы включить `signin` действие с адаптивной картой, включив в объект следующие `msteams` сведения. Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установите `signin` для . |
| `value` | Установите URL-адрес, на который необходимо перенаправить.  |

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
 
Чтобы включить `invoke` действие с адаптивной картой, включив в объект следующие `msteams` сведения. Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | Установлено, что `task/fetch` |
| `data` | Установите значение  |

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
