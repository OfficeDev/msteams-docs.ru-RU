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
# <a name="notification-only-bots-in-microsoft-teams"></a>Боты только для уведомлений в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Если единственная цель бота — доставить уведомление пользователям и не является разговорным, вы можете включить поле `isNotificationOnly` в манифесте приложения. Это приводит к следующим изменениям:

* Пользователи не могут отправлять сообщения только для уведомления бота.
* Пользователи не @mention бота.

> [!NOTE]
> Приложения только для ботов будут всплыть в личном подносе приложения в обоих случаях: `isNotificationOnly: true` или `isNotificationOnly: false` .

## <a name="app-manifest"></a>Манифест приложения

Чтобы включить это, заданной `isNotificationOnly` `true` для .

> [!NOTE]
> Следует помнить, что значение `isNotificationOnly` boolean , а не строка.

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

* Только для уведомлений боты используют проактивные сообщения для общения с пользователем. Дополнительные сведения см. в [сообщении Proactive для ботов.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)
