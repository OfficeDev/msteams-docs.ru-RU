---
title: Пользовательские просмотры
description: Пример для пользовательских представлений с помощью универсальных действий
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: c24697b300d07ed53a172df162d0d3851361f579
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853517"
---
# <a name="user-specific-views"></a><span data-ttu-id="c08f3-103">Пользовательские просмотры</span><span class="sxs-lookup"><span data-stu-id="c08f3-103">User Specific Views</span></span>

<span data-ttu-id="c08f3-104">Ранее, если адаптивные карты были отправлены в беседе Teams, все пользователи видят одно и то же содержимое карты.</span><span class="sxs-lookup"><span data-stu-id="c08f3-104">Earlier if Adaptive Cards was sent in a Teams conversation, all users see the exact same card content.</span></span> <span data-ttu-id="c08f3-105">С введением модели универсальных действий и адаптивных карт разработчики ботов теперь могут предоставлять пользователям специальные представления `refresh` адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="c08f3-105">With the introduction of the Universal Actions model and `refresh` for Adaptive Cards, bot developers can now provide User Specific Views of Adaptive Cards to users.</span></span> <span data-ttu-id="c08f3-106">Теперь та же адаптивная карта может обновиться до специальной адаптивной карты пользователя.</span><span class="sxs-lookup"><span data-stu-id="c08f3-106">The same Adaptive Card can now refresh to a User Specific Adaptive Card.</span></span> <span data-ttu-id="c08f3-107">Не более 60 разных пользователей могут видеть другую версию карты с дополнительной информацией или действиями.</span><span class="sxs-lookup"><span data-stu-id="c08f3-107">Maximum 60 different users can see a different version of the card with additional information or actions.</span></span> <span data-ttu-id="c08f3-108">Это обеспечивает мощные сценарии, такие как утверждения, элементы управления создателями опросов, билеты, управление инцидентами и карты управления проектами.</span><span class="sxs-lookup"><span data-stu-id="c08f3-108">This provides powerful scenarios like approvals, poll creator controls, ticketing, incident management, and project management cards.</span></span>

<span data-ttu-id="c08f3-109">Например, Меган, инспектор безопасности в Contoso, хочет создать инцидент и назначить его Алексу.</span><span class="sxs-lookup"><span data-stu-id="c08f3-109">For example, Megan, a safety inspector at Contoso, wants to create an incident and assign it to Alex.</span></span> <span data-ttu-id="c08f3-110">Она также хочет, чтобы все в команде знали об инциденте.</span><span class="sxs-lookup"><span data-stu-id="c08f3-110">She also wants everyone in the team to be aware about the incident.</span></span> <span data-ttu-id="c08f3-111">Меган использует расширение сообщений об инцидентах Contoso с питанием от универсальных действий для адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="c08f3-111">Megan uses Contoso incident reporting message extension powered by Universal Actions for Adaptive Cards.</span></span>

# <a name="mobile"></a>[<span data-ttu-id="c08f3-112">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="c08f3-112">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Представления для мобильных пользователей":::

# <a name="desktop"></a>[<span data-ttu-id="c08f3-114">Desktop</span><span class="sxs-lookup"><span data-stu-id="c08f3-114">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Пользовательские просмотры":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a><span data-ttu-id="c08f3-116">Пользовательские представления для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="c08f3-116">User Specific Views for Adaptive Cards</span></span>

<span data-ttu-id="c08f3-117">В следующем коде приводится пример адаптивных карт:</span><span class="sxs-lookup"><span data-stu-id="c08f3-117">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="c08f3-118">**Чтобы отправить адаптивные карты, обновить пользовательские представления и вызвать запросы к боту**</span><span class="sxs-lookup"><span data-stu-id="c08f3-118">**To send Adaptive Cards, refresh User Specific Views, and invoke requests to the bot**</span></span>

1. <span data-ttu-id="c08f3-119">Когда Меган создает новый инцидент, бот отправляет адаптивную карту или общую карту с сведениями об инциденте в Teams беседе.</span><span class="sxs-lookup"><span data-stu-id="c08f3-119">When Megan creates a new incident, the bot sends the Adaptive Card or common card with incident details in the Teams conversation.</span></span>
2. <span data-ttu-id="c08f3-120">Теперь эта карта автоматически обновляется до пользовательского представления для Меган и Алекс.</span><span class="sxs-lookup"><span data-stu-id="c08f3-120">Now this card automatically refreshes to User Specific View for Megan and Alex.</span></span> <span data-ttu-id="c08f3-121">МРИС пользователя Алекса и Меган добавляются в свойство `userIds` `refresh` свойства адаптивной карты JSON.</span><span class="sxs-lookup"><span data-stu-id="c08f3-121">Alex's and Megan's user MRIs are added in `userIds` property of `refresh` property of the Adaptive Card JSON.</span></span> <span data-ttu-id="c08f3-122">Карта остается той же для других пользователей в беседе.</span><span class="sxs-lookup"><span data-stu-id="c08f3-122">The card remains the same for other users in the conversation.</span></span>
3. <span data-ttu-id="c08f3-123">Для Меган автоматическое обновление вызывает запрос `adaptiveCard/action` на вызов бота.</span><span class="sxs-lookup"><span data-stu-id="c08f3-123">For Megan, automatic refresh triggers an `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="c08f3-124">Бот может вернуть карточку создателя инцидента с помощью `Edit` кнопки в качестве ответа на этот запрос на вызов.</span><span class="sxs-lookup"><span data-stu-id="c08f3-124">The bot can return an incident creator card with `Edit` button as a response to this invoke request.</span></span>
4. <span data-ttu-id="c08f3-125">Аналогично для Alex автоматическое обновление вызывает другой запрос `adaptiveCard/action` на вызов бота.</span><span class="sxs-lookup"><span data-stu-id="c08f3-125">Similarly for Alex, automatic refresh triggers another `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="c08f3-126">Бот может вернуть кнопку карточки владельца инцидента `Resolve` в качестве ответа на этот запрос на вызов.</span><span class="sxs-lookup"><span data-stu-id="c08f3-126">The bot can return an incident owner card `Resolve` button as a response to this invoke request.</span></span>

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a><span data-ttu-id="c08f3-127">Вызов запроса, отосланного Teams клиента боту</span><span class="sxs-lookup"><span data-stu-id="c08f3-127">Invoke request sent from Teams client to the bot</span></span>

<span data-ttu-id="c08f3-128">В следующем коде приводится пример запроса на вызов, отосланного от Teams клиента Алекса и Меган в бот:</span><span class="sxs-lookup"><span data-stu-id="c08f3-128">The following code provides an example of an invoke request sent from Alex's and Megan's Teams client to the bot:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card"></a><span data-ttu-id="c08f3-129">adaptiveCard/action вызывает карточку ответа</span><span class="sxs-lookup"><span data-stu-id="c08f3-129">adaptiveCard/action invoke response card</span></span>

<span data-ttu-id="c08f3-130">В следующем коде приводится пример адаптивной карты/действия, вызываемой для Меган:</span><span class="sxs-lookup"><span data-stu-id="c08f3-130">The following code provides an example of an adaptiveCard/action invoke response card for Megan:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a><span data-ttu-id="c08f3-131">adaptiveCard/action вызывает карточку ответа для Alex</span><span class="sxs-lookup"><span data-stu-id="c08f3-131">adaptiveCard/action invoke response card for Alex</span></span>

<span data-ttu-id="c08f3-132">В следующем коде приводится пример адаптивной карточки вызова ответа на действия для Alex:</span><span class="sxs-lookup"><span data-stu-id="c08f3-132">The following code provides an example of an adaptiveCard/action invoke response card for Alex:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="c08f3-133">Вызов ответа для возврата адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="c08f3-133">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="c08f3-134">В следующем коде приводится пример ответа на вызов для возврата адаптивных карт:</span><span class="sxs-lookup"><span data-stu-id="c08f3-134">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

<span data-ttu-id="c08f3-135">Рекомендации по разработке карт, которые необходимо иметь в виду при разработке пользовательских представлений:</span><span class="sxs-lookup"><span data-stu-id="c08f3-135">Card design guidelines to keep in mind while designing User Specific Views:</span></span>

* <span data-ttu-id="c08f3-136">Можно создать не более **60** пользовательских представлений для определенной карты, отправленной в чат или канал, указав их `userIds` в `refresh` разделе.</span><span class="sxs-lookup"><span data-stu-id="c08f3-136">You can create a maximum of **60 User Specific Views** for a particular card sent to a chat or channel by specifying their `userIds` in the `refresh` section.</span></span>
* <span data-ttu-id="c08f3-137">**Базовая карта:** Базовая версия карты, которую разработчик бота отправляет в чат.</span><span class="sxs-lookup"><span data-stu-id="c08f3-137">**Base Card:** The base version of the card that the bot developer sends to the chat.</span></span> <span data-ttu-id="c08f3-138">Это версия адаптивной карты для всех пользователей, не указанных в `userIds` разделе.</span><span class="sxs-lookup"><span data-stu-id="c08f3-138">This is the version of the Adaptive Card for all users who are not specified in the `userIds` section.</span></span>
* <span data-ttu-id="c08f3-139">Обновление сообщения можно использовать для обновления базовой карты и одновременного обновления пользовательской конкретной карты.</span><span class="sxs-lookup"><span data-stu-id="c08f3-139">A message update can be used to update the base card and simultaneously refresh the User Specific Card.</span></span> <span data-ttu-id="c08f3-140">Открытие чата или канала также обновляет карту для пользователей с включенной поддержкой обновления.</span><span class="sxs-lookup"><span data-stu-id="c08f3-140">Opening the chat or channel also refreshes the card for users with refresh enabled.</span></span>
* <span data-ttu-id="c08f3-141">В сценариях с более крупными группами, в которых пользователи переключаются на представление о действии, которое требует динамических обновлений для ответчиков, можно продолжать добавлять до 60 пользователей в `userIds` список.</span><span class="sxs-lookup"><span data-stu-id="c08f3-141">For scenarios with larger groups where users switch to a view on action, which needs dynamic updates for responders, you can keep adding up to 60 users to the `userIds` list.</span></span> <span data-ttu-id="c08f3-142">Первый ответ можно удалить из списка при ответе 61-го пользователя.</span><span class="sxs-lookup"><span data-stu-id="c08f3-142">You can remove the first responder from the list when the 61st user responds.</span></span> <span data-ttu-id="c08f3-143">Для пользователей, которые удаляются из списка, вы можете предоставить ручную кнопку обновления или использовать кнопку обновления в меню параметры сообщений, чтобы `userIds` получить последний результат.</span><span class="sxs-lookup"><span data-stu-id="c08f3-143">For the users who get removed from the `userIds` list, you can provide a manual refresh button or use the refresh button in the message options menu to get the latest result.</span></span>
* <span data-ttu-id="c08f3-144">Дайте пользователям подсказку для получения пользовательского представления, в котором они видят только определенное представление карты или какие-либо действия.</span><span class="sxs-lookup"><span data-stu-id="c08f3-144">Give a prompt to users to get a User Specific View, where they see only a particular view of the card or some actions.</span></span>

## <a name="see-also"></a><span data-ttu-id="c08f3-145">См. также</span><span class="sxs-lookup"><span data-stu-id="c08f3-145">See also</span></span>

* [<span data-ttu-id="c08f3-146">Работа с универсальными действиями для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="c08f3-146">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="c08f3-147">Просмотры на сегодняшний день</span><span class="sxs-lookup"><span data-stu-id="c08f3-147">Up to date views</span></span>](Up-To-Date-Views.md)
