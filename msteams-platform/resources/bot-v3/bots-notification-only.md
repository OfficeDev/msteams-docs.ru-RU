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
# <a name="notification-only-bots-in-microsoft-teams"></a>Боты только уведомления в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Если только для пользователя, предназначенного для ленты, требуется доставлять уведомления для пользователей, а не для общения, `isNotificationOnly` вы можете включить поле в манифесте приложения. Это приводит к следующим изменениям:

* Пользователи не могут заменять сообщением ленты только с уведомлениями.
* Пользователи не могут @mention ленты.

## <a name="app-manifest"></a>Манифест приложения

Чтобы включить этот параметр, `isNotificationOnly` установите `true`значение.

> [!NOTE]
> Обратите внимание, что значение `isNotificationOnly` является логическим, а не строкой.

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

## <a name="best-practices-and-limitations"></a>Рекомендации и ограничения

* Для обмена данными с пользователем Боты использовать профилактическую систему обмена сообщениями. Дополнительные сведения см. в статье [Active Messaging for Боты](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .
