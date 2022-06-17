---
title: Боты только для уведомлений
description: В этом модуле вы узнаете, какие боты только для уведомлений находятся в Microsoft Teams, манифесте приложения и его рекомендациях и ограничениях.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: 547ef73cfd036efe566afe15e4f50701a275c2cd
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144301"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Боты только для уведомлений в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Если единственная цель бота — доставка уведомлений пользователям и не беседа, `isNotificationOnly` вы можете включить это поле в манифесте приложения. Это приведет к следующим изменениям.

* Пользователи не могут отправлять сообщения боту только для уведомлений.
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

* Боты только для уведомлений используют упреждающие сообщения для взаимодействия с пользователем. Дополнительные сведения см. в статье [Упреждающие сообщения для ботов](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).
