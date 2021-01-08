---
title: Добавление действий карточки в бота
description: Описание действий карт в Microsoft Teams и их использования в ботах
keywords: действия карточек ботов teams
ms.openlocfilehash: 2bee1072405d91cd29d1aa227884516a87d10bde
ms.sourcegitcommit: b9771f8f4be9ac1ff8c85c2d7bd8d5c5408bc653
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "49768076"
---
# <a name="card-actions"></a>Действия с карточками

Карточки, используемые ботами и расширениями обмена сообщениями в Teams, поддерживают следующие типы действий ( [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) ). Обратите внимание, что эти действия отличаются от действий для карт соединители `potentialActions` Office 365 при их использования.

| Тип | Действие |
| --- | --- |
| `openUrl` | Открывает URL-адрес в браузере по умолчанию. |
| `messageBack` | Отправляет сообщение и полезное сообщение боту (от пользователя, нажавшего кнопку или нажавшего карточку) и отправляет отдельное сообщение в поток чата. |
| `imBack`| Отправляет сообщение боту (от пользователя, нажавшего кнопку или нажавшего карточку). Это сообщение (от пользователя к боту) отображается всем участникам беседы. |
| `invoke` | Отправляет сообщение и полезное сообщение боту (от пользователя, нажавшего кнопку или нажавшего карточку). Это сообщение не отображается. |
| `signin` | Инициирует поток OAuth, позволяя ботам подключаться к защищенным службам. |

> [!NOTE]
>* Teams не поддерживает `CardAction` типы, не указанные в предыдущей таблице.
>* Teams не поддерживает `potentialActions` свойство.
>* Действия с карточками отличаются [от предлагаемых действий](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) в Bot Framework или службе ботов Azure. Рекомендуемые действия не поддерживаются в Microsoft Teams: если вы хотите, чтобы кнопки появлялись в сообщении бота Teams, используйте карточку.
>* Если вы используете действие карточки в составе расширения обмена сообщениями, действия не будут работать, пока карточка не будет отправлена в канал (они не будут работать, пока карточка находится в окне сообщения составить).

Teams также поддерживает [действия адаптивных карточек,](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)которые используются только адаптивными карточками. Эти действия перечислены в собственном разделе в конце этой ссылки.

## <a name="openurl"></a>openUrl

Этот тип действия указывает URL-адрес для запуска в браузере по умолчанию. Обратите внимание, что бот не получает уведомления о нажатии кнопки.

Поле должно содержать полный и `value` правильно сформированный URL-адрес.

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>messageBack

С помощью этого параметра можно `messageBack` создать полностью настроенную действие со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается как метка кнопки. |
| `displayText` | Необязательное свойство. Эхо от пользователя в потоке чата при выполнении действия. Этот текст не *отправляется* вашему боту. |
| `value` | Отправляется боту при выполнении действия. Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON. |
| `text` | Отправляется боту при выполнении действия. Используйте это свойство для упрощения разработки ботов: код может проверять одно свойство верхнего уровня для отправки логики бота. |

Гибкость означает, что код может не оставлять видимое сообщение пользователя в истории, `messageBack` просто не используя `displayText` .

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

### <a name="inbound-message-example"></a>Пример входящие сообщения

`replyToId` содержит ИД сообщения, из которое поступило действие карточки. Используйте его, если вы хотите обновить сообщение.

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

Это действие инициирует возврат сообщения боту, как если бы пользователь ввести его в обычном сообщении чата. Ваш пользователь и все остальные пользователи, если они есть в канале, увидят этот ответ кнопки.

Поле должно содержать текстовую строку, которая эхом повторяется в чате и, следовательно, `value` отправляется боту. Это текст сообщения, который будет обрабатываться в боте для выполнения нужной логики. Примечание. Это поле является простой строкой. Форматирование или скрытые символы не поддерживаются.

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>invoke

Это `invoke` действие используется для вызова [модулей задач.](~/task-modules-and-cards/task-modules/task-modules-bots.md)

Действие `invoke` содержит три свойства: , и `type` `title` `value` . Свойство `value` может содержать строку, строковый объект JSON или объект JSON.

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

Когда пользователь нажимает кнопку, бот получает `value` объект с дополнительной информацией. Обратите внимание, что тип действия будет вместо `invoke` `message` ( `activity.Type == "invoke"` ).

### <a name="example-invoke-button-definition-net"></a>Пример: определение кнопки вызова (.NET)

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>Пример: входящий вызов сообщения

Свойство верхнего уровня содержит ИД сообщения, от которое `replyToId` поступило действие карточки. Используйте его, если вы хотите обновить сообщение.

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

Инициирует поток OAuth, позволяя ботам подключаться к защищенным службам, как описано ниже: поток проверки подлинности [в ботах.](~/bots/how-to/authentication/auth-flow-bot.md)

## <a name="adaptive-cards-actions"></a>Действия адаптивных карточек

Адаптивные карточки поддерживают три типа действий:

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)

В дополнение к вышеперечисленным действиям можно изменить полезной нагрузки адаптивной карточки для поддержки существующих действий Bot Framework с помощью свойства `Action.Submit` `msteams` в `data` объекте `Action.Submit` . В разделах ниже подробно поется, как использовать существующие действия Bot Framework с адаптивными карточками.

> [!NOTE]
> Добавление данных с помощью действия Bot Framework не работает с модулем задачи `msteams` адаптивной карточки.

### <a name="adaptive-cards-with-messageback-action"></a>Адаптивные карточки с действием messageBack

Чтобы включить действие `messageBack` с адаптивной карточкой, включаем в объект следующие `msteams` сведения. Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | За установлено `messageBack` |
| `displayText` | Необязательное свойство. Эхо от пользователя в потоке чата при выполнении действия. Этот текст не *отправляется* вашему боту. |
| `value` | Отправляется боту при выполнении действия. Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON. |
| `text` | Отправляется боту при выполнении действия. Используйте это свойство для упрощения разработки ботов: код может проверять одно свойство верхнего уровня для отправки логики бота. |

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

### <a name="adaptive-cards-with-imback-action"></a>Адаптивные карточки с действием imBack

Чтобы включить действие `imBack` с адаптивной карточкой, включаем в объект следующие `msteams` сведения. Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | За установлено `imBack` |
| `value` | Строка, которая должна быть повторяема в чате |

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

### <a name="adaptive-cards-with-signin-action"></a>Адаптивные карточки с действием для регистрации

Чтобы включить действие `signin` с адаптивной карточкой, включаем в объект следующие `msteams` сведения. Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | За установлено `signin` |
| `value` | Установите URL-адрес, на который нужно перенаправить  |

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

### <a name="adaptive-cards-with-invoke-action"></a>Адаптивные карточки с действием вызова
 
Чтобы включить действие `invoke` с адаптивной карточкой, включаем в объект следующие `msteams` сведения. Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.

| Свойство | Описание |
| --- | --- |
| `type` | За установлено `task/fetch` |
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
