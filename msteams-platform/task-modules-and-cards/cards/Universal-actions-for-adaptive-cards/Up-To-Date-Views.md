---
title: Просмотры на сегодняшний день
description: Пример для представления до даты с помощью универсального бота
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 2027d07961929fb40e7afc3ee268e1267b235a02
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088887"
---
# <a name="up-to-date-cards"></a>Актуальные карточки

Теперь вы можете предоставить пользователям последнюю информацию по адаптивным картам с сочетанием обновлений и изменений сообщений в Teams. Благодаря этому вы можете динамически обновлять пользовательские представления до последнего состояния, как и когда в службе происходит изменение. Например, в случае управления проектами или карточек с билетами можно обновить комментарии и состояние задачи. В случае утверждений отражается последнее состояние, а также предоставляется дифференцированная информация и действия.

Например, пользователь может создать запрос на утверждение активов в Teams беседе. Алекс создает запрос на утверждение и назначает его Меган и Нестор. Ниже следующую часть для создания запроса на утверждение:

* Пользовательские представления можно использовать с помощью `refresh` свойства адаптивных карт.
С помощью пользовательских представлений можно  показать карточку с кнопками **Утверждение** или Отклонение для набора пользователей и показать карту без этих кнопок другим пользователям.

* Чтобы состояние карты постоянно обновлялось, Teams можно использовать механизм редактирования сообщений. Например, при каждом утверждении бот может запускать правки сообщений для всех пользователей. Это изменение сообщения бота вызывает запрос на вызов для всех пользователей автоматического обновления, на которые бот может отвечать с помощью обновленной `adaptiveCard/action` пользовательской конкретной карты.

Дополнительные сведения см. [в дополнительных сведениях о том, как изменить сообщение бота.](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards)

## <a name="approval-base-card"></a>Базовая карта утверждения

В следующем коде приводится пример базовой карты утверждения:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>", "<Nestor's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ]
}
```

## <a name="approval-card-with-approve-and-reject-buttons"></a>Карточка утверждения с кнопками Утверждение и Отклонение

В следующем коде приводится пример карточки утверждения с кнопками **Утверждение** и **Отклонение:**

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Nestor's user MRI>", "<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

Ниже показаны две роли, показанные пользователям в зависимости от их участия в запросе на утверждение:

* Базовая карточка утверждения. Показана пользователям, которые не являются частью списка утверждений и еще не одобрили или не отклонили запрос, и не являются частью списка в свойстве адаптивной `userIds` `refresh` карты JSON.
* Карточка **утверждения**  с кнопками Утверждение или Отклонение: Показана пользователям, которые являются частью списка утверждений, и списком в свойстве `userIds` `refresh` адаптивной карты JSON.

**Отправка запроса на утверждение активов**

1. Алекс поднимает запрос на утверждение активов в беседе Teams и назначает его Меган и Нестор.
2. Бот отправляет базовую карточку утверждения в беседе.
3. Все остальные пользователи в беседе видят карточку, отправленную ботом. Автоматическое обновление запускается для Меган и Нестор, которые теперь  видят определенную карточку пользователя с кнопками **Утверждение** или Отклонение при добавлении их пользовательских МРЦ в список в свойстве `userIds` `refresh` адаптивной карты.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="Пользовательские просмотры":::

4. Нестор выбирает кнопку **Утверждение,** которая питание с `Action.Execute` . Бот получает запрос на вызов, на который он `adaptiveCard/action` может вернуть адаптивную карту в ответ.
5. Бот запускает редактирование сообщения с помощью обновленной карты, в которой говорится, что Нестор одобрил запрос, пока меган находится на стадии утверждения.
6. Редактирование сообщения бота запускает автоматическое обновление для Меган, и она видит обновленную карточку пользователя, которая говорит, что Нестор одобрил запрос, но также видит кнопки **Утверждение** или **Отклонение.** MRI пользователя Nestor удаляется из списка в свойстве этой адаптивной карты JSON в шагах `userIds` `refresh` 4 и 5. Теперь автоматическое обновление запускается только для Меган.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="В курсе конкретных представлений пользователей":::

7. Теперь Меган выбирает кнопку **Утверждение,** которая питание с `Action.Execute` . Бот получает запрос на вызов, на который он `adaptiveCard/action` может вернуть адаптивную карту в ответ.
8. Бот запускает редактирование сообщения с помощью обновленной карты, в которой говорится, что Нестор и Меган одобрили запрос.
9. Изменение сообщения бота не вызывает автоматического обновления. MRI пользователя Меган также удаляется из списка в свойстве этой адаптивной карты JSON в шагах `userIds` `refresh` 7 и 8.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="Просмотры на сегодняшний день":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a>Адаптивная карта, отправленная в `adaptiveCard/action` ответ и `message edit`

В следующем коде приводится пример адаптивных карт, отправленных в ответ на действия `adaptiveCard/action` `message edit` 4 и 5.

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ]
}
```

В следующем коде приводится пример адаптивных карт, отправленных в ответ на вызов с помощью автоматического `adaptiveCard/action` обновления для шага 6:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

В следующем коде приводится пример адаптивных карт, отправленных в ответ на действия 7 и `adaptiveCard/action` `message edit` 8.

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": []
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor and Megan**"
    }
  ]
}
```

## <a name="see-also"></a>См. также

* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
* [Пользовательские просмотры](User-Specific-Views.md)
