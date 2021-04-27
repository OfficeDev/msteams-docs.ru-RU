---
title: Боты только для уведомлений
description: Описывает, какие только уведомления боты находятся в Microsoft Teams
keywords: уведомление о ботах teams
ms.topic: conceptual
localization_priority: Normal
ms.date: 01/29/2020
ms.openlocfilehash: 42a0b9acecbc1821ea492cb6c850c7a9b11bbbfe
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019764"
---
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="a9cf2-104">Боты только для уведомлений в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a9cf2-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="a9cf2-105">Если единственная цель бота — доставить уведомление пользователям и не является разговорным, вы можете включить поле `isNotificationOnly` в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="a9cf2-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="a9cf2-106">Это приводит к следующим изменениям:</span><span class="sxs-lookup"><span data-stu-id="a9cf2-106">This produces the following changes:</span></span>

* <span data-ttu-id="a9cf2-107">Пользователи не могут отправлять сообщения только для уведомления бота.</span><span class="sxs-lookup"><span data-stu-id="a9cf2-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="a9cf2-108">Пользователи не @mention бота.</span><span class="sxs-lookup"><span data-stu-id="a9cf2-108">Users cannot @mention the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="a9cf2-109">Приложения только для ботов будут всплыть в личном подносе приложения в обоих случаях: `isNotificationOnly: true` или `isNotificationOnly: false` .</span><span class="sxs-lookup"><span data-stu-id="a9cf2-109">The bot-only apps will surface in the personal app tray in both cases: `isNotificationOnly: true` or `isNotificationOnly: false`.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="a9cf2-110">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="a9cf2-110">App manifest</span></span>

<span data-ttu-id="a9cf2-111">Чтобы включить это, заданной `isNotificationOnly` `true` для .</span><span class="sxs-lookup"><span data-stu-id="a9cf2-111">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="a9cf2-112">Следует помнить, что значение `isNotificationOnly` boolean , а не строка.</span><span class="sxs-lookup"><span data-stu-id="a9cf2-112">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "isNotificationOnly": true,
      "scopes": [
        "personal",
        "team"
      ],
    }
  ],
  ...
}
```

## <a name="best-practices-and-limitations"></a><span data-ttu-id="a9cf2-113">Рекомендации и ограничения</span><span class="sxs-lookup"><span data-stu-id="a9cf2-113">Best practices and limitations</span></span>

* <span data-ttu-id="a9cf2-114">Только для уведомлений боты используют проактивные сообщения для общения с пользователем.</span><span class="sxs-lookup"><span data-stu-id="a9cf2-114">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="a9cf2-115">Дополнительные [сведения см. в материале Proactive messaging for bots.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)</span><span class="sxs-lookup"><span data-stu-id="a9cf2-115">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>
