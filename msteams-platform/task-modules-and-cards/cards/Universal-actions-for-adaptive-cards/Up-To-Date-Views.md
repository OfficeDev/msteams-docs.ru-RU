---
title: Просмотры на сегодняшний день
description: Пример для представления до даты с помощью универсального бота
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 2027d07961929fb40e7afc3ee268e1267b235a02
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088887"
---
# <a name="up-to-date-cards"></a><span data-ttu-id="acd8b-103">Актуальные карточки</span><span class="sxs-lookup"><span data-stu-id="acd8b-103">Up to date cards</span></span>

<span data-ttu-id="acd8b-104">Теперь вы можете предоставить пользователям последнюю информацию по адаптивным картам с сочетанием обновлений и изменений сообщений в Teams.</span><span class="sxs-lookup"><span data-stu-id="acd8b-104">You can now provide latest information to your users on Adaptive Cards with a combination of refresh and message edits in Teams.</span></span> <span data-ttu-id="acd8b-105">Благодаря этому вы можете динамически обновлять пользовательские представления до последнего состояния, как и когда в службе происходит изменение.</span><span class="sxs-lookup"><span data-stu-id="acd8b-105">With this you are able to update the User Specific Views dynamically to its latest state as and when there is a change on your service.</span></span> <span data-ttu-id="acd8b-106">Например, в случае управления проектами или карточек с билетами можно обновить комментарии и состояние задачи.</span><span class="sxs-lookup"><span data-stu-id="acd8b-106">For example, in the case of project management or ticketing cards, you can update comments and the status of the task.</span></span> <span data-ttu-id="acd8b-107">В случае утверждений отражается последнее состояние, а также предоставляется дифференцированная информация и действия.</span><span class="sxs-lookup"><span data-stu-id="acd8b-107">In case of approvals the latest state is reflected while also providing differentiated information and actions.</span></span>

<span data-ttu-id="acd8b-108">Например, пользователь может создать запрос на утверждение активов в Teams беседе.</span><span class="sxs-lookup"><span data-stu-id="acd8b-108">For example, a user can create an asset approval request in a Teams conversation.</span></span> <span data-ttu-id="acd8b-109">Алекс создает запрос на утверждение и назначает его Меган и Нестор.</span><span class="sxs-lookup"><span data-stu-id="acd8b-109">Alex creates an approval request and assigns it to Megan and Nestor.</span></span> <span data-ttu-id="acd8b-110">Ниже следующую часть для создания запроса на утверждение:</span><span class="sxs-lookup"><span data-stu-id="acd8b-110">The following are the two parts to create the approval request:</span></span>

* <span data-ttu-id="acd8b-111">Пользовательские представления можно использовать с помощью `refresh` свойства адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="acd8b-111">User Specific Views can be leveraged using the `refresh` property of the Adaptive Cards.</span></span>
<span data-ttu-id="acd8b-112">С помощью пользовательских представлений можно  показать карточку с кнопками **Утверждение** или Отклонение для набора пользователей и показать карту без этих кнопок другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="acd8b-112">Using User Specific Views one can show a card with **Approve** or **Reject** buttons to a set of users, and show a card without these buttons to other users.</span></span>

* <span data-ttu-id="acd8b-113">Чтобы состояние карты постоянно обновлялось, Teams можно использовать механизм редактирования сообщений.</span><span class="sxs-lookup"><span data-stu-id="acd8b-113">To keep the card state updated at all times, Teams message edit mechanism can be leveraged.</span></span> <span data-ttu-id="acd8b-114">Например, при каждом утверждении бот может запускать правки сообщений для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="acd8b-114">For example, each time there is an approval, bot can trigger a message edit to all users.</span></span> <span data-ttu-id="acd8b-115">Это изменение сообщения бота вызывает запрос на вызов для всех пользователей автоматического обновления, на которые бот может отвечать с помощью обновленной `adaptiveCard/action` пользовательской конкретной карты.</span><span class="sxs-lookup"><span data-stu-id="acd8b-115">This bot message edit triggers an `adaptiveCard/action` invoke request for all automatic refresh users, to which the bot can respond with the updated user specific card.</span></span>

<span data-ttu-id="acd8b-116">Дополнительные сведения см. [в дополнительных сведениях о том, как изменить сообщение бота.](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards)</span><span class="sxs-lookup"><span data-stu-id="acd8b-116">For more information, see [how to do a bot message edit](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards).</span></span>

## <a name="approval-base-card"></a><span data-ttu-id="acd8b-117">Базовая карта утверждения</span><span class="sxs-lookup"><span data-stu-id="acd8b-117">Approval base card</span></span>

<span data-ttu-id="acd8b-118">В следующем коде приводится пример базовой карты утверждения:</span><span class="sxs-lookup"><span data-stu-id="acd8b-118">The following code provides an example of an approval base card:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>", "<Nestor's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ]
}
```

## <a name="approval-card-with-approve-and-reject-buttons"></a><span data-ttu-id="acd8b-119">Карточка утверждения с кнопками Утверждение и Отклонение</span><span class="sxs-lookup"><span data-stu-id="acd8b-119">Approval card with Approve and Reject buttons</span></span>

<span data-ttu-id="acd8b-120">В следующем коде приводится пример карточки утверждения с кнопками **Утверждение** и **Отклонение:**</span><span class="sxs-lookup"><span data-stu-id="acd8b-120">The following code provides an example of an approval card with **Approve** and **Reject** buttons:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Nestor's user MRI>", "<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

<span data-ttu-id="acd8b-121">Ниже показаны две роли, показанные пользователям в зависимости от их участия в запросе на утверждение:</span><span class="sxs-lookup"><span data-stu-id="acd8b-121">Following are the two roles that are shown to users depending on their involvement in the approval request:</span></span>

* <span data-ttu-id="acd8b-122">Базовая карточка утверждения. Показана пользователям, которые не являются частью списка утверждений и еще не одобрили или не отклонили запрос, и не являются частью списка в свойстве адаптивной `userIds` `refresh` карты JSON.</span><span class="sxs-lookup"><span data-stu-id="acd8b-122">Approval base card: Shown to users who are not part of approvers list and have not yet approved or rejected the request, and are not part of `userIds` list in `refresh` property of the Adaptive Card JSON.</span></span>
* <span data-ttu-id="acd8b-123">Карточка **утверждения**  с кнопками Утверждение или Отклонение: Показана пользователям, которые являются частью списка утверждений, и списком в свойстве `userIds` `refresh` адаптивной карты JSON.</span><span class="sxs-lookup"><span data-stu-id="acd8b-123">Approval card with **Approve** or **Reject** buttons: Shown to the users who are part of the approvers list and the `userIds` list in the `refresh` property of the Adaptive Card JSON.</span></span>

<span data-ttu-id="acd8b-124">**Отправка запроса на утверждение активов**</span><span class="sxs-lookup"><span data-stu-id="acd8b-124">**To send the asset approval request**</span></span>

1. <span data-ttu-id="acd8b-125">Алекс поднимает запрос на утверждение активов в беседе Teams и назначает его Меган и Нестор.</span><span class="sxs-lookup"><span data-stu-id="acd8b-125">Alex raises an asset approval request in a Teams conversation and assigns it to Megan and Nestor.</span></span>
2. <span data-ttu-id="acd8b-126">Бот отправляет базовую карточку утверждения в беседе.</span><span class="sxs-lookup"><span data-stu-id="acd8b-126">Bot sends the approval base card in the conversation.</span></span>
3. <span data-ttu-id="acd8b-127">Все остальные пользователи в беседе видят карточку, отправленную ботом.</span><span class="sxs-lookup"><span data-stu-id="acd8b-127">All other users in the conversation see the card sent by the bot.</span></span> <span data-ttu-id="acd8b-128">Автоматическое обновление запускается для Меган и Нестор, которые теперь  видят определенную карточку пользователя с кнопками **Утверждение** или Отклонение при добавлении их пользовательских МРЦ в список в свойстве `userIds` `refresh` адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="acd8b-128">Automatic refresh is triggered for Megan and Nestor, who now see the user specific card with **Approve** or **Reject** buttons as their user MRIs are added to the `userIds` list in the `refresh` property of the Adaptive Card.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="Пользовательские просмотры":::

4. <span data-ttu-id="acd8b-130">Нестор выбирает кнопку **Утверждение,** которая питание с `Action.Execute` .</span><span class="sxs-lookup"><span data-stu-id="acd8b-130">Nestor selects the **Approve** button which is powered with `Action.Execute`.</span></span> <span data-ttu-id="acd8b-131">Бот получает запрос на вызов, на который он `adaptiveCard/action` может вернуть адаптивную карту в ответ.</span><span class="sxs-lookup"><span data-stu-id="acd8b-131">The bot gets an `adaptiveCard/action` invoke request to which it can return an Adaptive Card in response.</span></span>
5. <span data-ttu-id="acd8b-132">Бот запускает редактирование сообщения с помощью обновленной карты, в которой говорится, что Нестор одобрил запрос, пока меган находится на стадии утверждения.</span><span class="sxs-lookup"><span data-stu-id="acd8b-132">The bot triggers a message edit with an updated card which says Nestor has approved the request while Megan's approval is pending.</span></span>
6. <span data-ttu-id="acd8b-133">Редактирование сообщения бота запускает автоматическое обновление для Меган, и она видит обновленную карточку пользователя, которая говорит, что Нестор одобрил запрос, но также видит кнопки **Утверждение** или **Отклонение.**</span><span class="sxs-lookup"><span data-stu-id="acd8b-133">Bot message edit triggers an automatic refresh for Megan and she sees the updated user specific card, which says Nestor has approved the request, but also sees the **Approve** or **Reject** buttons.</span></span> <span data-ttu-id="acd8b-134">MRI пользователя Nestor удаляется из списка в свойстве этой адаптивной карты JSON в шагах `userIds` `refresh` 4 и 5.</span><span class="sxs-lookup"><span data-stu-id="acd8b-134">Nestor's user MRI is removed from the `userIds` list in `refresh` property of this Adaptive Card JSON in steps 4 and 5.</span></span> <span data-ttu-id="acd8b-135">Теперь автоматическое обновление запускается только для Меган.</span><span class="sxs-lookup"><span data-stu-id="acd8b-135">Now, automatic refresh is only triggered for Megan.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="В курсе конкретных представлений пользователей":::

7. <span data-ttu-id="acd8b-137">Теперь Меган выбирает кнопку **Утверждение,** которая питание с `Action.Execute` .</span><span class="sxs-lookup"><span data-stu-id="acd8b-137">Now, Megan selects the **Approve** button, which is powered with `Action.Execute`.</span></span> <span data-ttu-id="acd8b-138">Бот получает запрос на вызов, на который он `adaptiveCard/action` может вернуть адаптивную карту в ответ.</span><span class="sxs-lookup"><span data-stu-id="acd8b-138">The bot gets an `adaptiveCard/action` invoke request to which it can return an Adaptive Card in response.</span></span>
8. <span data-ttu-id="acd8b-139">Бот запускает редактирование сообщения с помощью обновленной карты, в которой говорится, что Нестор и Меган одобрили запрос.</span><span class="sxs-lookup"><span data-stu-id="acd8b-139">The bot triggers a message edit with an updated card, which says Nestor and Megan have approved the request.</span></span>
9. <span data-ttu-id="acd8b-140">Изменение сообщения бота не вызывает автоматического обновления.</span><span class="sxs-lookup"><span data-stu-id="acd8b-140">Bot message edit does not trigger any automatic refresh.</span></span> <span data-ttu-id="acd8b-141">MRI пользователя Меган также удаляется из списка в свойстве этой адаптивной карты JSON в шагах `userIds` `refresh` 7 и 8.</span><span class="sxs-lookup"><span data-stu-id="acd8b-141">Megan's user MRI is also removed from the `userIds` list in `refresh` property of this Adaptive Card JSON in steps 7 and 8.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="Просмотры на сегодняшний день":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a><span data-ttu-id="acd8b-143">Адаптивная карта, отправленная в `adaptiveCard/action` ответ и `message edit`</span><span class="sxs-lookup"><span data-stu-id="acd8b-143">Adaptive Card sent as response of `adaptiveCard/action` and `message edit`</span></span>

<span data-ttu-id="acd8b-144">В следующем коде приводится пример адаптивных карт, отправленных в ответ на действия `adaptiveCard/action` `message edit` 4 и 5.</span><span class="sxs-lookup"><span data-stu-id="acd8b-144">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` and `message edit` for steps 4 and 5:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ]
}
```

<span data-ttu-id="acd8b-145">В следующем коде приводится пример адаптивных карт, отправленных в ответ на вызов с помощью автоматического `adaptiveCard/action` обновления для шага 6:</span><span class="sxs-lookup"><span data-stu-id="acd8b-145">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` invoke through automatic refresh for step 6:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

<span data-ttu-id="acd8b-146">В следующем коде приводится пример адаптивных карт, отправленных в ответ на действия 7 и `adaptiveCard/action` `message edit` 8.</span><span class="sxs-lookup"><span data-stu-id="acd8b-146">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` and `message edit` for steps 7 and 8:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": []
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor and Megan**"
    }
  ]
}
```

## <a name="see-also"></a><span data-ttu-id="acd8b-147">См. также</span><span class="sxs-lookup"><span data-stu-id="acd8b-147">See also</span></span>

* [<span data-ttu-id="acd8b-148">Работа с универсальными действиями для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="acd8b-148">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="acd8b-149">Пользовательские просмотры</span><span class="sxs-lookup"><span data-stu-id="acd8b-149">User Specific Views</span></span>](User-Specific-Views.md)
