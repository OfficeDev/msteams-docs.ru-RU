---
title: Боты только для уведомлений
description: Описывает, какие только уведомления находятся в Microsoft Teams
keywords: уведомление о ботах teams
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: 71dbc07445a57194e90ba3985c3aff1e2d4f2cdf
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156115"
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
