---
title: Боты только для уведомлений
description: В этом модуле вы узнаете, какие боты доступны только для уведомлений в Microsoft Teams, манифест приложения и его рекомендации и ограничения
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: ac412f37cba03c5da43163bf2eadd47adc676f08
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833018"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Боты только для уведомлений в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Если единственной целью бота является доставка уведомлений пользователям и не является беседой, вы можете включить `isNotificationOnly` поле в манифесте приложения. Это приведет к следующим изменениям.

* Пользователи не могут создавать сообщения боту только для уведомлений.
* Пользователи не могут @mention бота.

> [!NOTE]
> Приложения только для ботов будут отображаться в области личных приложений в обоих случаях: `isNotificationOnly: true` или `isNotificationOnly: false`.

## <a name="app-manifest"></a>Манифест приложения

Чтобы включить это, установите для `isNotificationOnly` значение `true`.

> [!NOTE]
> Значение `isNotificationOnly` является логическим, а не строковым.

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

Боты только для уведомлений используют упреждающие сообщения для взаимодействия с пользователем. Дополнительные сведения см. в статье [Упреждающие сообщения для ботов](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).
