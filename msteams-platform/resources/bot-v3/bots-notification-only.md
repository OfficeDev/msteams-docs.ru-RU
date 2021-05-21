---
title: Боты только для уведомлений
description: Описывает, какие только уведомления находятся в Microsoft Teams
keywords: уведомление о ботах teams
ms.topic: conceptual
localization_priority: Normal
ms.date: 01/29/2020
ms.openlocfilehash: 3de462f73733f5f7cf223444ffe6deeb53faaaaa
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566763"
---
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="1d81b-104">Боты только для уведомлений в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1d81b-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="1d81b-105">Если единственная цель бота — доставить уведомление пользователям и не является разговорным, вы можете включить поле `isNotificationOnly` в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="1d81b-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="1d81b-106">Это приводит к следующим изменениям:</span><span class="sxs-lookup"><span data-stu-id="1d81b-106">This produces the following changes:</span></span>

* <span data-ttu-id="1d81b-107">Пользователи не могут отправлять сообщения только для уведомления бота.</span><span class="sxs-lookup"><span data-stu-id="1d81b-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="1d81b-108">Пользователи не @mention бота.</span><span class="sxs-lookup"><span data-stu-id="1d81b-108">Users cannot @mention the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="1d81b-109">Приложения только для ботов будут всплыть в личном подносе приложения в обоих случаях: `isNotificationOnly: true` или `isNotificationOnly: false` .</span><span class="sxs-lookup"><span data-stu-id="1d81b-109">The bot-only apps will surface in the personal app tray in both cases: `isNotificationOnly: true` or `isNotificationOnly: false`.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="1d81b-110">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="1d81b-110">App manifest</span></span>

<span data-ttu-id="1d81b-111">Чтобы включить это, заданной `isNotificationOnly` `true` для .</span><span class="sxs-lookup"><span data-stu-id="1d81b-111">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="1d81b-112">Следует помнить, что значение `isNotificationOnly` boolean , а не строка.</span><span class="sxs-lookup"><span data-stu-id="1d81b-112">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="1d81b-113">Рекомендации и ограничения</span><span class="sxs-lookup"><span data-stu-id="1d81b-113">Best practices and limitations</span></span>

* <span data-ttu-id="1d81b-114">Только для уведомлений боты используют проактивные сообщения для общения с пользователем.</span><span class="sxs-lookup"><span data-stu-id="1d81b-114">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="1d81b-115">Дополнительные сведения см. в [сообщении Proactive для ботов.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)</span><span class="sxs-lookup"><span data-stu-id="1d81b-115">For more information, see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>
