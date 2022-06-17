---
title: Пользовательские просмотры
description: В этом модуле вы узнаете о пользовательских представлениях с использованием универсальных действий с примером кода и adaptiveCard/action invoke response card
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: a3fdc937ba1528a2bf9aa304bf484bbcae68b5c6
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143923"
---
# <a name="user-specific-views"></a>Пользовательские просмотры

Ранее, если адаптивные карточки отправлялись в беседе Teams, все пользователи могли видеть одно и то же содержимое карточки. С появлением модели универсальных `refresh` действий и адаптивных карточек разработчики ботов теперь могут предоставлять пользователям представления адаптивных карточек. Теперь та же адаптивная карточка может обновляться до адаптивной карточки конкретного пользователя. Адаптивная карточка предоставляет мощные сценарии, такие как утверждения, элементы управления создателем опроса, запросы, управление инцидентами и карточки управления проектами.

> [!NOTE]
>
> * Пользовательское представление поддерживается для адаптивных карточек, отправляемых ботом, и зависит от универсальных действий.
> * Не более 60 разных пользователей могут видеть другую версию карточки с дополнительными сведениями или действиями.

Например, Марта, инспектор безопасности компании Contoso, хочет создать инцидент и назначить его Алексу. Кроме того, Она хочет, чтобы все участники команды знали об инциденте. Она использует расширение сообщений об инцидентах Contoso на основе универсальных действий для адаптивных карточек.

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Представления для отдельных пользователей мобильных устройств" lightbox="../../../assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg":::

# <a name="desktop"></a>[Компьютер](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Пользовательские просмотры" lightbox="../../../assets/images/adaptive-cards/universal-bots-incident-management.png":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a>Пользовательские представления для адаптивных карточек

В следующем коде приведен пример адаптивных карточек:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView",
      "data": {
            "refresh info": "<refresh info>"
      }
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ]
}
```

Чтобы отправить адаптивные карточки, обновите пользовательские представления и вызовите запросы к боту:

1. Когда Марта создает новый инцидент, бот отправляет адаптивную карточку или общую карточку с подробными сведениями об Teams беседе.
2. Теперь эта карточка автоматически обновляется в пользовательском представлении для Меган и Алекс. МИ-коды `userIds` `refresh` пользователя Алексея и Меганы добавляются в свойство свойства JSON адаптивной карточки. Карточка остается одинаковой для других пользователей в беседе.
3. Для Меня автоматическое обновление активирует запрос `adaptiveCard/action` на вызов к боту. Бот может вернуть карточку создателя инцидента с кнопкой `Edit` в качестве ответа на этот запрос на вызов.
4. Аналогично для Алекса автоматическое обновление активирует еще один запрос `adaptiveCard/action` на вызов к боту. Бот может вернуть кнопку карточки владельца `Resolve` инцидента в ответ на этот запрос на вызов.

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>Вызов запроса, отправляемого Teams клиента боту

В следующем коде приведен пример запроса на вызов, отправляемого боту из Teams клиента Алексея и Teams:

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "editOrResolveView",
      "data": { 
            "refresh info": "<refresh info>"
      } 
    },
    "trigger": "automatic" 
  }
}
```

## <a name="adaptivecardaction-invoke-response-card"></a>adaptiveCard/action invoke response card

В следующем коде приведен пример адаптивной карточки ответа на вызов adaptiveCard/action для Megan:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Edit",
      "verb": "edit",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>AdaptiveCard/action invoke response card for Alex

В следующем коде приведен пример карточки ответа на вызов adaptiveCard/action для Алекса:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Resolve",
      "verb": "resolve",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="invoke-response-to-return-adaptive-cards"></a>Вызов ответа для возврата адаптивных карточек

В следующем коде приведен пример ответа на вызов для возврата адаптивных карточек:

### <a name="c"></a>[C#](#tab/C)

```csharp
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
var card = "<adaptive card json>";
 
const cardRes = {
        statusCode: 200,
        type: 'application/vnd.microsoft.card.adaptive',
        value: card
    };
    const res = {
        status: 200,
        body: cardRes
    };
    return res;

```

***

В следующем списке приведены рекомендации по проектированию карточек для представлений, определенных пользователем:

* Поведение при обновлении: можно создать не более 60 представлений для конкретной карточки, отправляемой в беседу, `userIds` указав их в свойстве `Refresh` .

  * Если поле `userIds` не `Refresh` указано в свойстве, Teams клиент может автоматически активировать обновление для всех пользователей, если в беседе не более 60 участников.

  * Чтобы пользователи могли вручную активировать обновление карточки, они могут выбрать **"Обновить"** в меню параметров сообщения. Это происходит со всеми пользователями, если в беседе содержится менее 60 участников, или с набором пользователей, `userIds` не указанных в списке, если в беседе содержится не более 60 пользователей.

* Базовая карточка: бот отправляет сообщение, которое внедряет базовую версию карточки. Все участники беседы могут просматривать одинаково. Затем бот извлекает карточку пользователя с помощью обновления для пользователей, указанных в разделе `userIds` .

* Время ожидания обновления: Teams клиент инициирует обновление двумя способами: с помощью функции **"** Обновить" или выбрав команду **"Выполнить"**. Обновление активируется, только если карточка из последнего вызова старше минуты. Вы можете управлять поведением обновления, добавляя метку времени в контейнер данных и проверяя ее перед отправкой обновленной карточки.

* Обновление сообщения можно использовать для обновления базовой карточки и одновременного обновления пользовательской карточки. При открытии чата или канала также обновляется карточка для пользователей с **включенным обновлением** .

* В сценариях с большими группами, в которых пользователи переключаются на представление о действии, которое требует динамических обновлений для отвечающего, можно добавить в список до 60 `userIds` пользователей. Вы можете удалить первого отвечающего из списка, когда 61-й пользователь ответит. Для пользователей, которые удаляются `userIds` из списка, можно вручную обновить, чтобы получить  последний результат.

* Предложите пользователям получить представление для конкретного пользователя, где они видят только определенное представление карточки или некоторые действия.

> [!NOTE]
> Карточка пользователя, возвращаемая ботом, отправляется только конкретному клиенту, который запросит ее. Например, если пользователь переключается на другой клиент, например с рабочего стола на мобильный, то для получения обновленной карточки запускается другое событие вызова.

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Адаптивные карточки последовательных рабочих процессов | Демонстрация реализации последовательных рабочих процессов, пользовательских представлений и актуальных адаптивных карточек в ботах. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>См. также

* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
* [Актуальные представления](Up-To-Date-Views.md)
* [Отзывы о завершении формы](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
