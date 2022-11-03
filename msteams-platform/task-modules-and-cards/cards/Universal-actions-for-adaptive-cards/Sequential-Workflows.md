---
title: Последовательные рабочие процессы
description: В этом модуле вы узнаете о последовательных рабочих процессах для адаптивных карточек с помощью примеров универсальных действий с кодом.
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: bd3fbf560099487ba45c2454460b82b852b675fa
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833193"
---
# <a name="sequential-workflows"></a>Последовательные рабочие процессы

Адаптивные карточки теперь поддерживают последовательные рабочие процессы, которые обновляются в соответствии с действиями пользователя. С помощью последовательных рабочих процессов адаптивные карточки обновляются в действиях пользователя, и пользователь может выполнять серию карточек, требующих ввода пользователем. `Action.Execute` поддерживает последовательные рабочие процессы, что позволяет разработчикам ботов возвращать адаптивные карточки в ответ на действия пользователя.

Например, возьмем сценарий, в котором кафетерий хочет принять заказ на команду или канал. При `Action.Execute` выборе пользователя для различных элементов, таких как еда и напитки, можно записывать последовательно. Пользователь также может проходить через карточки в соответствии с логикой, определенной разработчиком бота. <br/>

На следующем рисунке показан последовательный рабочий процесс:

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Пользователь может выполнять свой рабочий процесс, не изменяя карточку для других пользователей. Рабочий процесс также полезен для проведения викторин с помощью последовательных адаптивных карточек. На следующем рисунке показано, как разные пользователи могут находиться на разных этапах рабочего процесса и состояния карточки:

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Состояния бота общественного питания" lightbox="../../../assets/images/adaptive-cards/universal-bots-catering-bot.png":::

> [!NOTE]
> Чтобы синхронизировать ход выполнения пользователя на разных устройствах, используйте `refresh` свойство в формате JSON адаптивной карточки.

## <a name="sequential-workflow-for-adaptive-cards"></a>Последовательный рабочий процесс для адаптивных карточек

В следующем коде приведен пример адаптивных карточек:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "body": [
    {
      "type": "TextBlock",
      "text": "Select from food options"
    },
    { 
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Execute",
          "title": "Chicken",
          "verb": "food",
          "data": {
              "item": "chicken"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Beef",
          "verb": "food",
          "data": {
              "item": "beef"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Vegan",
          "verb": "food",
          "data": {
              "item": "vegan"
          }
        }
      ]
    }
  ]
}
```

`Action.Execute` Вызов бота может возвращать адаптивные карточки в ответ, что заменяет существующую карточку в Teams.
В следующем примере показано, что бот возвращает при выборе продуктов питания или напитках или подтверждении заказа.

* При выборе продуктов питания из карточки 1, бот может вернуть карту для выбора напитков, которая является Картой 2.
* При выборе напитка из карточки 2 бот может вернуть карту подтверждения заказа, которая является Картой 3.
* При подтверждении заказа с карточки 3 бот может вернуть карту с подтверждением заказа, которая является Картой 4.

## <a name="invoke-request-received-on-bot-side"></a>Вызов запроса, полученного на стороне бота

В следующем коде приведен пример запроса на вызов, полученного на стороне бота:

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "food",
      "data": { 
            "item": "vegan"
      } 
    },
    "trigger": "manual" 
  }
}
```

## <a name="invoke-response-to-return-adaptive-cards"></a>Вызов ответа для возврата адаптивных карточек

В следующем коде приведен пример ответа вызова для возврата адаптивных карточек:

```C#
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

## <a name="code-samples"></a>Примеры кода

|Название примера | Описание | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Бот организации питания Teams | Создание бота, который принимает заказы на обед с помощью адаптивных карточек. |[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| Н/Д |
| Адаптивные карточки последовательных рабочих процессов | Демонстрация реализации последовательных рабочих процессов, пользовательских представлений и актуальных адаптивных карточек в ботах. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Действия адаптивной карточки в Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Как работают боты](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
* [Отзывы о завершении формы](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
