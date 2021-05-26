---
title: Пользовательские просмотры
description: Пример для пользовательских представлений с помощью универсальных действий
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: cadf66082582cfd9009a0497b3eb5e58f0a2ef02
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649633"
---
# <a name="user-specific-views"></a><span data-ttu-id="274c1-103">Пользовательские просмотры</span><span class="sxs-lookup"><span data-stu-id="274c1-103">User Specific Views</span></span>

<span data-ttu-id="274c1-104">Ранее, если адаптивные карты были отправлены в беседе Teams, все пользователи видят одно и то же содержимое карты.</span><span class="sxs-lookup"><span data-stu-id="274c1-104">Earlier if Adaptive Cards was sent in a Teams conversation, all users see the exact same card content.</span></span> <span data-ttu-id="274c1-105">С введением модели универсальных действий и адаптивных карт разработчики ботов теперь могут предоставлять пользователям специальные представления `refresh` адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="274c1-105">With the introduction of the Universal Actions model and `refresh` for Adaptive Cards, bot developers can now provide User Specific Views of Adaptive Cards to users.</span></span> <span data-ttu-id="274c1-106">Теперь та же адаптивная карта может обновиться до специальной адаптивной карты пользователя.</span><span class="sxs-lookup"><span data-stu-id="274c1-106">The same Adaptive Card can now refresh to a User Specific Adaptive Card.</span></span>

<span data-ttu-id="274c1-107">Например, Меган, инспектор безопасности в Contoso, хочет создать инцидент и назначить его Алексу.</span><span class="sxs-lookup"><span data-stu-id="274c1-107">For example, Megan, a safety inspector at Contoso, wants to create an incident and assign it to Alex.</span></span> <span data-ttu-id="274c1-108">Она также хочет, чтобы все в команде знали об инциденте.</span><span class="sxs-lookup"><span data-stu-id="274c1-108">She also wants everyone in the team to be aware about the incident.</span></span> <span data-ttu-id="274c1-109">Меган использует расширение сообщений об инцидентах Contoso с питанием от универсальных действий для адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="274c1-109">Megan uses Contoso incident reporting message extension powered by Universal Actions for Adaptive Cards.</span></span>

# <a name="mobile"></a>[<span data-ttu-id="274c1-110">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="274c1-110">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Представления для мобильных пользователей":::

# <a name="desktop"></a>[<span data-ttu-id="274c1-112">Desktop</span><span class="sxs-lookup"><span data-stu-id="274c1-112">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Пользовательские просмотры":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a><span data-ttu-id="274c1-114">Пользовательские представления для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="274c1-114">User Specific Views for Adaptive Cards</span></span>

<span data-ttu-id="274c1-115">В следующем коде приводится пример адаптивных карт:</span><span class="sxs-lookup"><span data-stu-id="274c1-115">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="274c1-116">**Чтобы отправить адаптивные карты, обновить пользовательские представления и вызвать запросы к боту**</span><span class="sxs-lookup"><span data-stu-id="274c1-116">**To send Adaptive Cards, refresh User Specific Views, and invoke requests to the bot**</span></span>

1. <span data-ttu-id="274c1-117">Когда Меган создает новый инцидент, бот отправляет адаптивную карту или общую карту с сведениями об инциденте в Teams беседе.</span><span class="sxs-lookup"><span data-stu-id="274c1-117">When Megan creates a new incident, the bot sends the Adaptive Card or common card with incident details in the Teams conversation.</span></span>
2. <span data-ttu-id="274c1-118">Теперь эта карта автоматически обновляется до пользовательского представления для Меган и Алекс.</span><span class="sxs-lookup"><span data-stu-id="274c1-118">Now this card automatically refreshes to User Specific View for Megan and Alex.</span></span> <span data-ttu-id="274c1-119">МРИС пользователя Алекса и Меган добавляются в свойство `userIds` `refresh` свойства адаптивной карты JSON.</span><span class="sxs-lookup"><span data-stu-id="274c1-119">Alex's and Megan's user MRIs are added in `userIds` property of `refresh` property of the Adaptive Card JSON.</span></span> <span data-ttu-id="274c1-120">Карта остается той же для других пользователей в беседе.</span><span class="sxs-lookup"><span data-stu-id="274c1-120">The card remains the same for other users in the conversation.</span></span>
3. <span data-ttu-id="274c1-121">Для Меган автоматическое обновление вызывает запрос `adaptiveCard/action` на вызов бота.</span><span class="sxs-lookup"><span data-stu-id="274c1-121">For Megan, automatic refresh triggers an `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="274c1-122">Бот может вернуть карточку создателя инцидента с помощью `Edit` кнопки в качестве ответа на этот запрос на вызов.</span><span class="sxs-lookup"><span data-stu-id="274c1-122">The bot can return an incident creator card with `Edit` button as a response to this invoke request.</span></span>
4. <span data-ttu-id="274c1-123">Аналогично для Alex автоматическое обновление вызывает другой запрос `adaptiveCard/action` на вызов бота.</span><span class="sxs-lookup"><span data-stu-id="274c1-123">Similarly for Alex, automatic refresh triggers another `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="274c1-124">Бот может вернуть кнопку карточки владельца инцидента `Resolve` в качестве ответа на этот запрос на вызов.</span><span class="sxs-lookup"><span data-stu-id="274c1-124">The bot can return an incident owner card `Resolve` button as a response to this invoke request.</span></span>

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a><span data-ttu-id="274c1-125">Вызов запроса, отосланного Teams клиента боту</span><span class="sxs-lookup"><span data-stu-id="274c1-125">Invoke request sent from Teams client to the bot</span></span>

<span data-ttu-id="274c1-126">В следующем коде приводится пример запроса на вызов, отосланного от Teams клиента Алекса и Меган в бот:</span><span class="sxs-lookup"><span data-stu-id="274c1-126">The following code provides an example of an invoke request sent from Alex's and Megan's Teams client to the bot:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card"></a><span data-ttu-id="274c1-127">adaptiveCard/action вызывает карточку ответа</span><span class="sxs-lookup"><span data-stu-id="274c1-127">adaptiveCard/action invoke response card</span></span>

<span data-ttu-id="274c1-128">В следующем коде приводится пример адаптивной карты/действия, вызываемой для Меган:</span><span class="sxs-lookup"><span data-stu-id="274c1-128">The following code provides an example of an adaptiveCard/action invoke response card for Megan:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a><span data-ttu-id="274c1-129">adaptiveCard/action вызывает карточку ответа для Alex</span><span class="sxs-lookup"><span data-stu-id="274c1-129">adaptiveCard/action invoke response card for Alex</span></span>

<span data-ttu-id="274c1-130">В следующем коде приводится пример адаптивной карточки вызова ответа на действия для Alex:</span><span class="sxs-lookup"><span data-stu-id="274c1-130">The following code provides an example of an adaptiveCard/action invoke response card for Alex:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="274c1-131">Вызов ответа для возврата адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="274c1-131">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="274c1-132">В следующем коде приводится пример ответа на вызов для возврата адаптивных карт:</span><span class="sxs-lookup"><span data-stu-id="274c1-132">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

<span data-ttu-id="274c1-133">Рекомендации по разработке карт, которые необходимо иметь в виду при разработке пользовательских представлений:</span><span class="sxs-lookup"><span data-stu-id="274c1-133">Card design guidelines to keep in mind while designing User Specific Views:</span></span>

* <span data-ttu-id="274c1-134">Вы можете создать не более **60** пользовательских представлений для определенной карты, отправленной в чат или канал, указав их `userIds` в `refresh` разделе.</span><span class="sxs-lookup"><span data-stu-id="274c1-134">You can create a maximum of **60 User Specific Views** for a particular card being sent to a chat or channel by specifying their `userIds` in the `refresh` section.</span></span>
* <span data-ttu-id="274c1-135">**Базовая карта:** Базовая версия карты, которую разработчик бота отправляет в чат.</span><span class="sxs-lookup"><span data-stu-id="274c1-135">**Base Card:** The base version of the card that the bot developer sends to the chat.</span></span> <span data-ttu-id="274c1-136">Это версия адаптивной карты для всех пользователей, не указанных в `userIds` разделе.</span><span class="sxs-lookup"><span data-stu-id="274c1-136">This is the version of the Adaptive Card for all users who are not specified in the `userIds` section.</span></span>
* <span data-ttu-id="274c1-137">Обновление или изменение сообщения можно использовать для обновления базовой карты и одновременного обновления пользовательской карты.</span><span class="sxs-lookup"><span data-stu-id="274c1-137">A message update or edit can be used to update the base card and simultaneously refresh the User Specific Card.</span></span>

## <a name="see-also"></a><span data-ttu-id="274c1-138">См. также</span><span class="sxs-lookup"><span data-stu-id="274c1-138">See also</span></span>

* [<span data-ttu-id="274c1-139">Работа с универсальными действиями для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="274c1-139">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="274c1-140">Просмотры на сегодняшний день</span><span class="sxs-lookup"><span data-stu-id="274c1-140">Up to date views</span></span>](Up-To-Date-Views.md)
