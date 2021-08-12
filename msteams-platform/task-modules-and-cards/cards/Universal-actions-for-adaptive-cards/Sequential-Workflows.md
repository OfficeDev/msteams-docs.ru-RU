---
title: Последовательные рабочие процессы
description: Пример последовательного рабочего процесса с использованием универсальных действий
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: c6e247fd2b3cb8d908cc3cb7282bd3f7666d2ed0
ms.sourcegitcommit: 6a41c529a423c81a184c7a79125dbaaed0179788
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/26/2021
ms.locfileid: "53585993"
---
# <a name="sequential-workflows"></a>Последовательные рабочие процессы

Адаптивные карты теперь поддерживают секентальные процессы, которые обновляются в действии пользователя. С помощью последовательного рабочего процесса адаптивные карточки обновляются в действии пользователя, и пользователь может пройти через ряд карт, которые требуют ввода пользователя. `Action.Execute` поддерживает последовательность процессов, что позволяет разработчикам ботов возвращать адаптивные карты в ответ на действия пользователя.

Например, возьмем сценарий, в котором кафетерий хочет сделать заказ для команды или канала. При выборе пользователя для различных элементов, таких как продукты питания и напитки, можно записывать `Action.Execute` последовательно. Пользователь также может проходить по картам по логике, определенной разработчиком бота. <br/>

На следующем изображении показан секентальный рабочий процесс:

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Пользователь может добиться прогресса в процессе рабочего процесса без изменения карты для других пользователей. Рабочий процесс также полезен для проведения викторин с помощью последовательной адаптивной карты. На следующем изображении показано, что разные пользователи могут быть на разных этапах рабочего процесса и состояниях карты:

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Состояния бота кейтеринга":::

> [!NOTE]
> Чтобы синхронизировать прогресс пользователя на устройствах, используйте свойство в `refresh` Adaptive Card JSON.

## <a name="sequential-workflow-for-adaptive-cards"></a>Последовательное рабочий процесс для адаптивных карт

В следующем коде приводится пример адаптивных карт:

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

`Action.Execute`в качестве ответа бот может возвращать адаптивные карты, которые заменяют существующую карту в Teams.
В следующем примере приводится информация о том, что возвращает бот при выборе продуктов питания или напитках или подтверждении заказа:

* При выборе продуктов питания из карточки 1 бот может вернуть карточку для выбора напитков с карточкой 2.
* При выборе напитка из карты 2 бот может вернуть карту подтверждения заказа, которая является карточкой 3.
* При подтверждении заказа с карты 3 бот может вернуть подтвержденную карту заказа, которая является карточкой 4.

## <a name="invoke-request-received-on-bot-side"></a>Вызов запроса, полученного на стороне бота

В следующем коде приводится пример запроса на вызов, полученного на стороне бота:

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

## <a name="invoke-response-to-return-adaptive-cards"></a>Вызов ответа для возврата адаптивных карт

В следующем коде приводится пример ответа на вызов для возврата адаптивных карт:

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
| Бот организации питания Teams | Создайте бот, который принимает порядок питания с помощью адаптивных карт. |[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| Эта функция пока недоступна |
| Адаптивные карточки последовательного рабочего процесса | Демонстрация того, как реализовать последовательное рабочий процесс, пользовательские представления и адаптивные карты в ботах. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |


## <a name="see-also"></a>Дополнительные ресурсы

* [Действия адаптивной карточки в Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Как работают боты](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
