---
title: Последовательные рабочие процессы
description: Пример последовательного рабочего процесса с использованием универсальных действий
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: f36e65133572569cd01de1053044336c810656f3
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649650"
---
# <a name="sequential-workflows"></a><span data-ttu-id="49cfa-103">Последовательные рабочие процессы</span><span class="sxs-lookup"><span data-stu-id="49cfa-103">Sequential Workflows</span></span>

<span data-ttu-id="49cfa-104">Адаптивные карты теперь поддерживают секентальные процессы, то есть, когда адаптивные карты обновляются в действии пользователя, и пользователь может пройти через ряд карт, которые требуют ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="49cfa-104">Adaptive Cards now support Sequential Workflows that is when Adaptive Cards are updated on user action and user can progress through a series of cards that require user input.</span></span> <span data-ttu-id="49cfa-105">Это поддерживается с помощью , что позволяет разработчикам-ботам возвращать адаптивные карты в ответ `Action.Execute` на действия пользователя.</span><span class="sxs-lookup"><span data-stu-id="49cfa-105">This is supported through `Action.Execute`, which allows bot developers to return Adaptive Cards in response to a user action.</span></span>

<span data-ttu-id="49cfa-106">Например, возьмем сценарий, в котором кафетерий хочет сделать заказ для команды или канала.</span><span class="sxs-lookup"><span data-stu-id="49cfa-106">For example, take a scenario where the cafeteria wants to take an order for a team or channel.</span></span> <span data-ttu-id="49cfa-107">Выбор пользователя для различных элементов, таких как еда, напитки и т. д., можно записывать `Action.Execute` последовательно.</span><span class="sxs-lookup"><span data-stu-id="49cfa-107">With `Action.Execute` the user's choice for various items, such as food, drinks, and so on can be recorded sequentially.</span></span> <span data-ttu-id="49cfa-108">Пользователь также может проходить по картам по логике, определенной разработчиком бота.</span><span class="sxs-lookup"><span data-stu-id="49cfa-108">User can also go back and forth through the cards as per the logic defined by the bot developer.</span></span> <br/>

<span data-ttu-id="49cfa-109">На следующем изображении показан секентальный рабочий процесс:</span><span class="sxs-lookup"><span data-stu-id="49cfa-109">The following image shows the Sequential Workflow:</span></span>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="49cfa-110">Пользователь может добиться прогресса в процессе рабочего процесса без изменения карты для других пользователей.</span><span class="sxs-lookup"><span data-stu-id="49cfa-110">A user can progress through their workflow without modifying the card for other users.</span></span> <span data-ttu-id="49cfa-111">Это также полезно для проведения викторин с помощью последовательной адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="49cfa-111">This is also useful for conducting quizzes using sequential Adaptive Cards.</span></span> <span data-ttu-id="49cfa-112">Как показано на следующем изображении, различные пользователи могут быть на разных этапах рабочего процесса, и они видят различные состояния карты:</span><span class="sxs-lookup"><span data-stu-id="49cfa-112">As shown in the following image, different users can be at different stages of the workflow and they see different states of the card:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Состояния бота кейтеринга":::

> [!NOTE]
> <span data-ttu-id="49cfa-114">Чтобы синхронизировать прогресс пользователя на устройствах, используйте свойство в `refresh` Adaptive Card JSON.</span><span class="sxs-lookup"><span data-stu-id="49cfa-114">In order to sync the user's progress across devices, use the `refresh` property in Adaptive Card JSON.</span></span>

## <a name="sequential-workflow-for-adaptive-cards"></a><span data-ttu-id="49cfa-115">Последовательное рабочий процесс для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="49cfa-115">Sequential Workflow for Adaptive Cards</span></span>

<span data-ttu-id="49cfa-116">В следующем коде приводится пример адаптивных карт:</span><span class="sxs-lookup"><span data-stu-id="49cfa-116">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="49cfa-117">`Action.Execute`в качестве ответа бот может возвращать адаптивные карты, которые заменяют существующую карту в Teams.</span><span class="sxs-lookup"><span data-stu-id="49cfa-117">`Action.Execute` invoking the bot can return Adaptive Cards as a response, which replaces the existing card in Teams.</span></span>
<span data-ttu-id="49cfa-118">В следующем примере приводится информация о том, что возвращает бот при выборе продуктов питания или напитках или подтверждении заказа:</span><span class="sxs-lookup"><span data-stu-id="49cfa-118">The following example provides what the bot returns on food or drink selection or order confirmation:</span></span>

* <span data-ttu-id="49cfa-119">При выборе продуктов питания из карточки 1 бот может вернуть карточку для выбора напитков с карточкой 2.</span><span class="sxs-lookup"><span data-stu-id="49cfa-119">On food selection from Card 1, bot can return a card for selection of drinks that is Card 2.</span></span>
* <span data-ttu-id="49cfa-120">При выборе напитка из карты 2 бот может вернуть карту подтверждения заказа, которая является карточкой 3.</span><span class="sxs-lookup"><span data-stu-id="49cfa-120">On drink selection from Card 2, bot can return an order confirmation card that is Card 3.</span></span>
* <span data-ttu-id="49cfa-121">При подтверждении заказа с карты 3 бот может вернуть подтвержденную карту заказа, которая является карточкой 4.</span><span class="sxs-lookup"><span data-stu-id="49cfa-121">On order confirmation from Card 3, bot can return an order confirmed card that is Card 4.</span></span>

## <a name="invoke-request-received-on-bot-side"></a><span data-ttu-id="49cfa-122">Вызов запроса, полученного на стороне бота</span><span class="sxs-lookup"><span data-stu-id="49cfa-122">Invoke request received on bot side</span></span>

<span data-ttu-id="49cfa-123">В следующем коде приводится пример запроса на вызов, полученного на стороне бота:</span><span class="sxs-lookup"><span data-stu-id="49cfa-123">The following code provides an example of an invoke request received on bot side:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="49cfa-124">Вызов ответа для возврата адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="49cfa-124">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="49cfa-125">В следующем коде приводится пример ответа на вызов для возврата адаптивных карт:</span><span class="sxs-lookup"><span data-stu-id="49cfa-125">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="49cfa-126">Пример кода</span><span class="sxs-lookup"><span data-stu-id="49cfa-126">Code sample</span></span>

|<span data-ttu-id="49cfa-127">Пример имени</span><span class="sxs-lookup"><span data-stu-id="49cfa-127">Sample name</span></span> | <span data-ttu-id="49cfa-128">Описание</span><span class="sxs-lookup"><span data-stu-id="49cfa-128">Description</span></span> | <span data-ttu-id="49cfa-129">. NETCore</span><span class="sxs-lookup"><span data-stu-id="49cfa-129">.NETCore</span></span> |
|----------------|-----------------|--------------|
| <span data-ttu-id="49cfa-130">Teams питания бот</span><span class="sxs-lookup"><span data-stu-id="49cfa-130">Teams catering bot</span></span> | <span data-ttu-id="49cfa-131">Создайте простой бот, который принимает порядок питания с помощью адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="49cfa-131">Create a simple bot that accepts food order using Adaptive Cards.</span></span> |[<span data-ttu-id="49cfa-132">View</span><span class="sxs-lookup"><span data-stu-id="49cfa-132">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)|

## <a name="see-also"></a><span data-ttu-id="49cfa-133">См. также</span><span class="sxs-lookup"><span data-stu-id="49cfa-133">See also</span></span>

* [<span data-ttu-id="49cfa-134">Действия адаптивной карты в Teams</span><span class="sxs-lookup"><span data-stu-id="49cfa-134">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="49cfa-135">Как работают боты</span><span class="sxs-lookup"><span data-stu-id="49cfa-135">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [<span data-ttu-id="49cfa-136">Работа с универсальными действиями для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="49cfa-136">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
