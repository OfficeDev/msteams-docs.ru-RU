---
title: Боты только для уведомлений
description: Описывает, какие только уведомления боты находятся в Microsoft Teams
keywords: уведомление о ботах teams
ms.topic: conceptual
ms.date: 01/29/2020
ms.openlocfilehash: 39ba25893623d6b963b44363b8458db6def58b60
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696075"
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

* Только для уведомлений боты используют проактивные сообщения для общения с пользователем. Дополнительные [сведения см. в материале Proactive messaging for bots.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)
