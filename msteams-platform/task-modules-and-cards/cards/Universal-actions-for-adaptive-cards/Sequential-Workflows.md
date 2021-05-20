---
title: Последовательные рабочие процессы
description: Пример последовательных рабочих процессов с использованием универсальных действий
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 7f285bf76aac4f0ca276321aee2ce4b4e5c3e7e4
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555404"
---
# <a name="sequential-workflows"></a>Последовательные рабочие процессы

Адаптивные карты теперь поддерживают последовательные рабочие процессы, то есть когда адаптивные карты обновляются на действия пользователя и пользователь может прогрессировать через ряд карт, которые требуют пользовательского ввода. Это поддерживается через `Action.Execute` , что позволяет разработчикам ботов вернуть адаптивные карты в ответ на действия пользователя.

Например, возьмем сценарий, при котором кафетерий хочет сделать заказ на команду или канал. С `Action.Execute` выбором пользователя для различных предметов, таких как продукты питания, напитки, и так далее могут быть записаны последовательно. Пользователь также может ходить туда и обратно через карты в соответствии с логикой, определенной разработчиком бота. <br/>

На следующем изображении показан последовательный рабочий процесс:

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Пользователь может прогрессировать через свой рабочий процесс без изменения карты для других пользователей. Это также полезно для проведения викторин с использованием последовательных адаптивных карт. Как показано на следующем изображении, различные пользователи могут быть на разных стадиях рабочего процесса, и они видят различные состояния карты:

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Питание бот государств":::

> [!NOTE]
> Для синхронизации прогресса пользователя на разных устройствах используйте свойство `refresh` в adaptive Card JSON.

## <a name="sequential-workflow-for-adaptive-cards"></a>Последовательный рабочий процесс для адаптивных карт

В следующем коде приведен пример адаптивных карт:

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

`Action.Execute`Ссылаясь бот может вернуть адаптивные карты в качестве ответа, который заменяет существующую карту в Teams.
В следующем примере приводится то, что бот возвращает при выборе продуктов питания или напитков или подтверждении заказа:

* При выборе продуктов питания с карты 1, бот может вернуть карту для выбора напитков, которая является картой 2.
* При выборе напитка из карты 2 бот может вернуть карту подтверждения заказа, которая является картой 3.
* При подтверждении заказа с карты 3 бот может вернуть подтвержденную карту заказа, которая является Картой 4.

## <a name="invoke-request-received-on-bot-side"></a>Запрос на вызов, полученный на стороне бота

Следующий код приводит пример запроса на вызов, полученного на стороне бота:

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

## <a name="invoke-response-to-return-adaptive-cards"></a>Вызов ответа на возврат адаптивных карт

Следующий код служит примером ответа на вызов для возврата адаптивных карт:

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

## <a name="see-also"></a>См. также

* [Действия адаптивной карты в Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Как работают боты](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
