---
title: Боты только для уведомлений
description: Описывает, какие только уведомления находятся в Microsoft Teams
keywords: уведомление о ботах teams
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: d3ee5343ea159950859237f2a488557d9063eb6e
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355729"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Боты только для уведомлений в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Если единственная цель бота — доставить уведомление пользователям и не является разговорным, `isNotificationOnly` вы можете включить поле в манифесте приложения. Это приводит к следующим изменениям:

* Пользователи не могут отправлять сообщения только для уведомления бота.
* Пользователи не @mention бота.

> [!NOTE]
> Приложения только для ботов будут всплыть в личном подносе приложения в обоих случаях: `isNotificationOnly: true` или `isNotificationOnly: false`.

## <a name="app-manifest"></a>Манифест приложения

Чтобы включить это, заданной `isNotificationOnly` для `true`.

> [!NOTE]
> Значение boolean `isNotificationOnly` , а не строка.

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

* Только для уведомлений боты используют проактивные сообщения для общения с пользователем. Дополнительные сведения см. в [сообщении Proactive для ботов](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).
