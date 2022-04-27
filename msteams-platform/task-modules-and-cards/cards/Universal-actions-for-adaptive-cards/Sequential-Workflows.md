---
title: Последовательные рабочие процессы
description: Сведения о последовательных рабочих процессах для адаптивных карточек с использованием универсальных действий с примерами кода
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 32200fc7a4df12567ba4000aad34e5a229dbc466
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073783"
---
# <a name="sequential-workflows"></a>Последовательные рабочие процессы

Адаптивные карточки теперь поддерживают последовательные рабочие процессы, которые обновляются при действии пользователя. С помощью последовательных рабочих процессов адаптивные карточки обновляются при действии пользователя, и пользователь может проходить через ряд карточек, для которых требуется ввод данных пользователем. `Action.Execute` поддерживает последовательные рабочие процессы, которые позволяют разработчикам ботов возвращать адаптивные карточки в ответ на действия пользователя.

Например, рассмотрим сценарий, в котором этот человек хочет получить заказ для команды или канала. При `Action.Execute` выборе пользователем различных элементов, таких как продукты питания и напитки, можно записывать последовательно. Пользователь также может перемещаться по карточкам в соответствии с логикой, определенной разработчиком бота. <br/>

На следующем рисунке показан последовательный рабочий процесс:

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Пользователь может проходить рабочий процесс, не изменяя карточку для других пользователей. Рабочий процесс также полезен для проведения тестов с использованием последовательных адаптивных карточек. На следующем рисунке показано, что разные пользователи могут быть на разных этапах рабочего процесса и состояния карточки:

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Состояния ботов для питания" lightbox="../../../assets/images/adaptive-cards/universal-bots-catering-bot.png":::

> [!NOTE]
> Чтобы синхронизировать ход выполнения пользователя на разных устройствах, используйте свойство `refresh` в JSON адаптивной карточки.

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

`Action.Execute`Вызов бота может возвращать адаптивные карточки в качестве ответа, который заменяет существующую карточку в Teams.
В следующем примере показано, что бот возвращает при выборе продуктов или кофе или подтверждении заказа:

* При выборе продуктов из карточки 1 бот может вернуть карточку для выбора напитков, которая является карточкой 2.
* При выборе кофе из карточки 2 бот может вернуть карточку подтверждения заказа, которая является карточкой 3.
* После подтверждения заказа из карточки 3 бот может вернуть подтвержденную карточку заказа, которая является карточкой 4.

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

В следующем коде приведен пример ответа на вызов для возврата адаптивных карточек:

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
| Бот организации питания Teams | Создайте бота, который принимает заказ на питание с помощью адаптивных карточек. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| Эта функция пока недоступна |
| Адаптивные карточки последовательных рабочих процессов | Демонстрация реализации последовательных рабочих процессов, пользовательских представлений и актуальных адаптивных карточек в ботах. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Действия адаптивной карточки в Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Как работают боты](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
* [Отзывы о завершении формы](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
