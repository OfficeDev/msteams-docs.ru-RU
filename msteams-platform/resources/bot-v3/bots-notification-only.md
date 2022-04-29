---
title: Боты только для уведомлений
description: Описание ботов только для уведомлений в Microsoft Teams
keywords: уведомление ботов Teams
ms.topic: conceptual
ms.localizationpriority: high
ms.date: 01/29/2020
ms.openlocfilehash: 1ee009fb76a52bcebdd3fe24c7a672f1ed455b42
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111481"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Боты только для уведомлений в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Если единственное назначение бота состоит в доставке уведомлений пользователям и он не предназначен для бесед, вы можете включить поле `isNotificationOnly` в манифесте своего приложения. Это приведет к следующим изменениям.

* Пользователи не могут отправлять сообщения боту, предназначенному только для уведомлений.
* Пользователи не могут @упоминать бота.

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

* Боты только для уведомлений используют упреждающие сообщения для взаимодействия с пользователем. Дополнительные сведения см. в статье [Упреждающие сообщения для ботов](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).
