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
# <a name="sequential-workflows"></a><span data-ttu-id="9e008-103">Последовательные рабочие процессы</span><span class="sxs-lookup"><span data-stu-id="9e008-103">Sequential Workflows</span></span>

<span data-ttu-id="9e008-104">Адаптивные карты теперь поддерживают последовательные рабочие процессы, то есть когда адаптивные карты обновляются на действия пользователя и пользователь может прогрессировать через ряд карт, которые требуют пользовательского ввода.</span><span class="sxs-lookup"><span data-stu-id="9e008-104">Adaptive Cards now support Sequential Workflows that is when Adaptive Cards are updated on user action and user can progress through a series of cards that require user input.</span></span> <span data-ttu-id="9e008-105">Это поддерживается через `Action.Execute` , что позволяет разработчикам ботов вернуть адаптивные карты в ответ на действия пользователя.</span><span class="sxs-lookup"><span data-stu-id="9e008-105">This is supported through `Action.Execute`, which allows bot developers to return Adaptive Cards in response to a user action.</span></span>

<span data-ttu-id="9e008-106">Например, возьмем сценарий, при котором кафетерий хочет сделать заказ на команду или канал.</span><span class="sxs-lookup"><span data-stu-id="9e008-106">For example, take a scenario where the cafeteria wants to take an order for a team or channel.</span></span> <span data-ttu-id="9e008-107">С `Action.Execute` выбором пользователя для различных предметов, таких как продукты питания, напитки, и так далее могут быть записаны последовательно.</span><span class="sxs-lookup"><span data-stu-id="9e008-107">With `Action.Execute` the user's choice for various items, such as food, drinks, and so on can be recorded sequentially.</span></span> <span data-ttu-id="9e008-108">Пользователь также может ходить туда и обратно через карты в соответствии с логикой, определенной разработчиком бота.</span><span class="sxs-lookup"><span data-stu-id="9e008-108">User can also go back and forth through the cards as per the logic defined by the bot developer.</span></span> <br/>

<span data-ttu-id="9e008-109">На следующем изображении показан последовательный рабочий процесс:</span><span class="sxs-lookup"><span data-stu-id="9e008-109">The following image shows the Sequential Workflow:</span></span>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="9e008-110">Пользователь может прогрессировать через свой рабочий процесс без изменения карты для других пользователей.</span><span class="sxs-lookup"><span data-stu-id="9e008-110">A user can progress through their workflow without modifying the card for other users.</span></span> <span data-ttu-id="9e008-111">Это также полезно для проведения викторин с использованием последовательных адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="9e008-111">This is also useful for conducting quizzes using sequential Adaptive Cards.</span></span> <span data-ttu-id="9e008-112">Как показано на следующем изображении, различные пользователи могут быть на разных стадиях рабочего процесса, и они видят различные состояния карты:</span><span class="sxs-lookup"><span data-stu-id="9e008-112">As shown in the following image, different users can be at different stages of the workflow and they see different states of the card:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Питание бот государств":::

> [!NOTE]
> <span data-ttu-id="9e008-114">Для синхронизации прогресса пользователя на разных устройствах используйте свойство `refresh` в adaptive Card JSON.</span><span class="sxs-lookup"><span data-stu-id="9e008-114">In order to sync the user's progress across devices, use the `refresh` property in Adaptive Card JSON.</span></span>

## <a name="sequential-workflow-for-adaptive-cards"></a><span data-ttu-id="9e008-115">Последовательный рабочий процесс для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="9e008-115">Sequential Workflow for Adaptive Cards</span></span>

<span data-ttu-id="9e008-116">В следующем коде приведен пример адаптивных карт:</span><span class="sxs-lookup"><span data-stu-id="9e008-116">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="9e008-117">`Action.Execute`Ссылаясь бот может вернуть адаптивные карты в качестве ответа, который заменяет существующую карту в Teams.</span><span class="sxs-lookup"><span data-stu-id="9e008-117">`Action.Execute` invoking the bot can return Adaptive Cards as a response, which replaces the existing card in Teams.</span></span>
<span data-ttu-id="9e008-118">В следующем примере приводится то, что бот возвращает при выборе продуктов питания или напитков или подтверждении заказа:</span><span class="sxs-lookup"><span data-stu-id="9e008-118">The following example provides what the bot returns on food or drink selection or order confirmation:</span></span>

* <span data-ttu-id="9e008-119">При выборе продуктов питания с карты 1, бот может вернуть карту для выбора напитков, которая является картой 2.</span><span class="sxs-lookup"><span data-stu-id="9e008-119">On food selection from Card 1, bot can return a card for selection of drinks that is Card 2.</span></span>
* <span data-ttu-id="9e008-120">При выборе напитка из карты 2 бот может вернуть карту подтверждения заказа, которая является картой 3.</span><span class="sxs-lookup"><span data-stu-id="9e008-120">On drink selection from Card 2, bot can return an order confirmation card that is Card 3.</span></span>
* <span data-ttu-id="9e008-121">При подтверждении заказа с карты 3 бот может вернуть подтвержденную карту заказа, которая является Картой 4.</span><span class="sxs-lookup"><span data-stu-id="9e008-121">On order confirmation from Card 3, bot can return an order confirmed card that is Card 4.</span></span>

## <a name="invoke-request-received-on-bot-side"></a><span data-ttu-id="9e008-122">Запрос на вызов, полученный на стороне бота</span><span class="sxs-lookup"><span data-stu-id="9e008-122">Invoke request received on bot side</span></span>

<span data-ttu-id="9e008-123">Следующий код приводит пример запроса на вызов, полученного на стороне бота:</span><span class="sxs-lookup"><span data-stu-id="9e008-123">The following code provides an example of an invoke request received on bot side:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="9e008-124">Вызов ответа на возврат адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="9e008-124">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="9e008-125">Следующий код служит примером ответа на вызов для возврата адаптивных карт:</span><span class="sxs-lookup"><span data-stu-id="9e008-125">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="9e008-126">См. также</span><span class="sxs-lookup"><span data-stu-id="9e008-126">See also</span></span>

* [<span data-ttu-id="9e008-127">Действия адаптивной карты в Teams</span><span class="sxs-lookup"><span data-stu-id="9e008-127">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="9e008-128">Как работают боты</span><span class="sxs-lookup"><span data-stu-id="9e008-128">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [<span data-ttu-id="9e008-129">Работа с универсальными действиями для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="9e008-129">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
