---
title: Только уведомления Боты
description: В этой статье описано, какие уведомления относятся только к боты в Microsoft Teams.
keywords: уведомление о Боты Teams
ms.date: 05/20/2019
ms.openlocfilehash: 37652bc2d6171191c81be4e5a2875f47c79574f9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675204"
---
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="1d7e1-104">Только уведомления боты в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1d7e1-104">Notification only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="1d7e1-105">Если только для пользователя, предназначенного для ленты, требуется доставлять уведомления для пользователей, а не для общения, `isNotificationOnly` вы можете включить поле в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="1d7e1-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="1d7e1-106">Это приводит к следующим изменениям:</span><span class="sxs-lookup"><span data-stu-id="1d7e1-106">This produces the following changes:</span></span>

* <span data-ttu-id="1d7e1-107">Пользователи не могут заменять сообщение только роботом.</span><span class="sxs-lookup"><span data-stu-id="1d7e1-107">Users cannot message your notification only bot.</span></span>
* <span data-ttu-id="1d7e1-108">Пользователи не могут @mention ленты.</span><span class="sxs-lookup"><span data-stu-id="1d7e1-108">Users cannot @mention the bot.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="1d7e1-109">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="1d7e1-109">App manifest</span></span>

<span data-ttu-id="1d7e1-110">Чтобы включить этот параметр, `isNotificationOnly` установите `true`значение.</span><span class="sxs-lookup"><span data-stu-id="1d7e1-110">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="1d7e1-111">Обратите внимание, что значение `isNotificationOnly` является логическим, а не строкой.</span><span class="sxs-lookup"><span data-stu-id="1d7e1-111">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="1d7e1-112">Рекомендации и ограничения</span><span class="sxs-lookup"><span data-stu-id="1d7e1-112">Best practices and limitations</span></span>

* <span data-ttu-id="1d7e1-113">Вы не можете создать `personal` только почтовые ленты, так как пользователь не может обмениваться сообщениями только в личном сеансе.</span><span class="sxs-lookup"><span data-stu-id="1d7e1-113">You cannot create a `personal` scoped notification only bot, as the user cannot message your notification only bot in a personal chat.</span></span> <span data-ttu-id="1d7e1-114">Это означает, что вы не можете `conversationUpdate` получить событие, которое предоставит вам необходимые сведения для отправки уведомления.</span><span class="sxs-lookup"><span data-stu-id="1d7e1-114">This means that you can't receive a `conversationUpdate` event that would provide you with the necessary details to send a notification.</span></span> <span data-ttu-id="1d7e1-115">Только для вашего уведомления Bot будет работать правильно, только если он `team` поддерживает область и добавляется в команду.</span><span class="sxs-lookup"><span data-stu-id="1d7e1-115">Your notification only bot will only function correctly if it supports the `team` scope and is added to a team.</span></span> <span data-ttu-id="1d7e1-116">В параметрах команды у пользователя Bot будет доступ к необходимым сведениям, чтобы отправить уведомление в канал или в частном порядке.</span><span class="sxs-lookup"><span data-stu-id="1d7e1-116">In the team setting, your bot will have access to the necessary information to either send a notification to a channel or privately to a user.</span></span>
* <span data-ttu-id="1d7e1-117">Уведомление только Боты использование упреждающего обмена сообщениями для обмена данными с пользователем.</span><span class="sxs-lookup"><span data-stu-id="1d7e1-117">Notification only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="1d7e1-118">Дополнительные сведения см. в статье [Active Messaging for Боты](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .</span><span class="sxs-lookup"><span data-stu-id="1d7e1-118">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>
