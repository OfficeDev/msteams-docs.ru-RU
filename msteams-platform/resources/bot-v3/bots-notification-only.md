---
title: Боты только для уведомлений
description: Описывает, какие боты только для уведомлений находятся в Microsoft Teams
keywords: команды ботов уведомления
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

Если единственной целью бота является доставка уведомлений пользователям и не является разговорной, вы можете включить `isNotificationOnly` поле в манифесте приложения. Это приводит к следующим изменениям:

* Пользователи не могут отправить сообщение только для уведомлений бота.
* Пользователи не @mention с ботом.

> [!NOTE]
> Приложения только для ботов будут всплывать в подносе личного приложения в обоих случаях: `isNotificationOnly: true` или `isNotificationOnly: false` .

## <a name="app-manifest"></a>Манифест приложения

Чтобы включить это, `isNotificationOnly` установите на `true` .

> [!NOTE]
> Имейте в виду, что `isNotificationOnly` значение boolean, а не строка.

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

* Боты только для уведомлений используют упреждающие сообщения для общения с пользователем. Для получения дополнительной информации [см.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)
