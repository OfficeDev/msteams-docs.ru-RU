---
title: Только уведомления Боты
description: В этой статье описано, что только уведомления боты в Microsoft Teams.
keywords: уведомление о Боты Teams
ms.date: 01/29/2020
ms.openlocfilehash: d312f9cd4558d35fc2492b5cf0b4f77b65660833
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783908"
---
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="86bb9-104">Боты только уведомления в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="86bb9-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="86bb9-105">Если только для пользователя, предназначенного для ленты, требуется доставлять уведомления для пользователей, а не для общения, `isNotificationOnly` вы можете включить поле в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="86bb9-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="86bb9-106">Это приводит к следующим изменениям:</span><span class="sxs-lookup"><span data-stu-id="86bb9-106">This produces the following changes:</span></span>

* <span data-ttu-id="86bb9-107">Пользователи не могут заменять сообщением ленты только с уведомлениями.</span><span class="sxs-lookup"><span data-stu-id="86bb9-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="86bb9-108">Пользователи не могут @mention ленты.</span><span class="sxs-lookup"><span data-stu-id="86bb9-108">Users cannot @mention the bot.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="86bb9-109">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="86bb9-109">App manifest</span></span>

<span data-ttu-id="86bb9-110">Чтобы включить этот параметр, `isNotificationOnly` установите `true`значение.</span><span class="sxs-lookup"><span data-stu-id="86bb9-110">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="86bb9-111">Обратите внимание, что значение `isNotificationOnly` является логическим, а не строкой.</span><span class="sxs-lookup"><span data-stu-id="86bb9-111">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="86bb9-112">Рекомендации и ограничения</span><span class="sxs-lookup"><span data-stu-id="86bb9-112">Best practices and limitations</span></span>

* <span data-ttu-id="86bb9-113">Для обмена данными с пользователем Боты использовать профилактическую систему обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="86bb9-113">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="86bb9-114">Дополнительные сведения см. в статье [Active Messaging for Боты](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .</span><span class="sxs-lookup"><span data-stu-id="86bb9-114">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>
