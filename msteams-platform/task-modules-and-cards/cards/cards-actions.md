---
title: Добавление действий карточки в Bot
description: Описывает действия с карточками в Microsoft Teams и способы их использования в Боты.
keywords: действия карточек Боты Teams
ms.openlocfilehash: f4db5d137051fa8d557d8a060adae6f15b4769c3
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346779"
---
# <a name="card-actions"></a>Действия с картой

Карты, используемые Боты и расширениями обмена сообщениями в Teams, поддерживают следующие типы действий ( [`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) ). Обратите внимание, что эти действия отличаются `potentialActions` для соединителей карт Office 365 при их использовании от соединителей.

| Type | Action |
| --- | --- |
| `openUrl` | Открывает URL-адрес в браузере по умолчанию. |
| `messageBack` | Отправляет сообщение и полезные данные в Bot (от пользователя, который нанажали кнопку или выделяют карточку) и отправляет отдельное сообщение в поток чата. |
| `imBack`| Отправляет сообщение на Bot (от пользователя, который нанажали кнопку или нанажали карточку). Это сообщение (от пользователя к Bot) видимо всем участникам беседы. |
| `invoke` | Отправляет сообщение и полезные данные в Bot (от пользователя, который нанажали кнопку или нанажали карточку). Это сообщение не отображается. |
| `signin` | Инициирует процесс OAuth, позволяя Боты подключаться к защищенным службам. |

> [!NOTE]
>* Teams не поддерживает `CardAction` типы, не указанные в предыдущей таблице.
>* Teams не поддерживает это `potentialActions` свойство.
>* Действия с картой отличаются от [предлагаемых действий](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) в службе Bot Framework/Azure Bot. Предлагаемые действия не поддерживаются в Microsoft teams: Если вы хотите, чтобы кнопки отображались в сообщении ленты Teams, используйте карточку.
>* Если вы используете действие карточки в составе расширения для обмена сообщениями, действия не будут работать до тех пор, пока карточка не будет отправлена в канал (они не будут работать, пока карточка находится в окне сообщения создания).

Teams также поддерживает [действия со адаптивными карточками](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), которые используются только адаптивными картами. Эти действия перечислены в отдельном разделе в конце этой ссылки.

## <a name="openurl"></a>openUrl

Этот тип действия задает URL-адрес, который будет запускаться в браузере по умолчанию. Обратите внимание, что для ленты не отображается уведомление о нажатии кнопки.

`value`Поле должно содержать полный и правильно сформированный URL-адрес.

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>мессажебакк

С помощью `messageBack` можно создать полностью настраиваемое действие со следующими свойствами:

| Свойство | Описание |
| --- | --- |
| `title` | Отображается в виде подписи кнопки. |
| `displayText` | Необязательный атрибут. Подается пользователю в поток чата при выполнении действия. Этот текст *не* отправляется в робот. |
| `value` | Отправляется на ваш робот при выполнении действия. Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON. |
| `text` | Отправляется на ваш робот при выполнении действия. Используйте это свойство для упрощения разработки в Bot: ваш код может проверять одно свойство верхнего уровня для обработки логики Bot. |

Гибкость заключается в `messageBack` том, что ваш код может не оставлять видимое пользовательское сообщение в истории простым, не используя `displayText` .

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

`value`Свойство может быть либо сериализованной строкой JSON, либо объектом JSON.

### <a name="inbound-message-example"></a>Пример входящего сообщения

`replyToId` содержит идентификатор сообщения, из которого поступило действие карточки. Используйте его, если хотите обновить сообщение.

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

## <a name="imback"></a>Обратное воспроизведение

Это действие вызывает возврат сообщения для ленты, как если бы пользователь ввел его в обычном сообщении чата. Пользователь и все остальные пользователи, если они находятся в канале, увидят этот ответ на эту кнопку.

`value`Поле должно содержать текстовую строку, которая помещается в чат и, следовательно, отправляется обратно в Bot. Это текст сообщения, которое будет обрабатываться в Bot, чтобы выполнить нужную логику. Note: это поле представляет собой простую строку — поддержка форматирования и скрытых символов отсутствует.

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>метода

`invoke`Действие используется для вызова [модулей задач](~/task-modules-and-cards/task-modules/task-modules-bots.md).

`invoke`Действие содержит три свойства: `type` , `title` и `value` . `value`Свойство может содержать строку, объект ПРЕОБРАЗОВАННОГО JSON или объект JSON.

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

Когда пользователь нажимает кнопку, ваш объект Bot будет получать `value` объект с дополнительными сведениями. Обратите внимание, что вместо него будет использоваться тип действия `invoke` `message` ( `activity.Type == "invoke"` ).

### <a name="example-invoke-button-definition-net"></a>Пример: вызов определения кнопки (.NET)

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>Пример: сообщение входящего вызова

Свойство верхнего уровня `replyToId` содержит идентификатор сообщения, из которого поступило действие карточки. Используйте его, если хотите обновить сообщение.

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

## <a name="signin"></a>SignIn

Инициирует процесс OAuth, позволяя Боты подключаться к защищенным службам, как описано ниже. [процесс проверки подлинности в Боты](~/bots/how-to/authentication/auth-flow-bot.md).

## <a name="adaptive-cards-actions"></a>Действия с адаптивными карточками

Адаптивные карты поддерживают три типа действий:

* [Action. OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action. ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)

В дополнение к приведенным выше действиям можно изменить данные адаптивной карточки, `Action.Submit` чтобы поддерживать существующие действия с помощью ленты с помощью `msteams` свойства в `data` объекте `Action.Submit` . В следующих разделах подробно описано, как использовать существующие действия с использованием ленты с адаптивными картами.

> [!NOTE]
> Добавление `msteams` к данным с действием Bot Framework не работает с модулем задачи адаптивной карточки.

### <a name="adaptive-cards-with-messageback-action"></a>Адаптивные карты с действием Мессажебакк

Чтобы включить `messageBack` действие с помощью адаптивной карточки, добавьте следующие сведения в `msteams` объект. Обратите внимание, что при необходимости вы можете добавить в объект дополнительные скрытые свойства `data` .

| Свойство | Описание |
| --- | --- |
| `type` | Значение `messageBack` |
| `displayText` | Необязательный атрибут. Подается пользователю в поток чата при выполнении действия. Этот текст *не* отправляется в робот. |
| `value` | Отправляется на ваш робот при выполнении действия. Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON. |
| `text` | Отправляется на ваш робот при выполнении действия. Используйте это свойство для упрощения разработки в Bot: ваш код может проверять одно свойство верхнего уровня для обработки логики Bot. |

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

### <a name="adaptive-cards-with-imback-action"></a>Адаптивные карты с действием при обратной передаче

Чтобы включить `imBack` действие с помощью адаптивной карточки, добавьте следующие сведения в `msteams` объект. Обратите внимание, что при необходимости вы можете добавить в объект дополнительные скрытые свойства `data` .

| Свойство | Описание |
| --- | --- |
| `type` | Значение `imBack` |
| `value` | Строка, которая должна быть возвращена в чате |

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

### <a name="adaptive-cards-with-signin-action"></a>Адаптивные карточки с действием SignIn

Чтобы включить `signin` действие с помощью адаптивной карточки, добавьте следующие сведения в `msteams` объект. Обратите внимание, что при необходимости вы можете добавить в объект дополнительные скрытые свойства `data` .

| Свойство | Описание |
| --- | --- |
| `type` | Значение `signin` |
| `value` | Укажите URL-адрес, на который требуется перенаправить  |

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
