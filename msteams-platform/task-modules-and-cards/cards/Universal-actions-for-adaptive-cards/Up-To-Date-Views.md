---
title: Просмотры на сегодняшний день
description: Узнайте о представлениях с использованием универсального бота с примерами кода
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Базовая карта утверждения отклоняет адаптивную
ms.openlocfilehash: 3eea8e3c08927ab797525a10f59774410197d0e1
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453735"
---
# <a name="up-to-date-cards"></a>Актуальные карточки

Теперь вы можете предоставить пользователям последнюю информацию по адаптивным картам. Включите сочетание обновлений и изменений сообщений в Teams. Динамически обновите пользовательские представления до последнего состояния, как и при изменении службы. Например, для управления проектами или карточек с билетами, обновления комментариев и состояния задачи. Для утверждений отражается последнее состояние, а также предоставляется дифференцированная информация и действия.

Например, пользователь может создать запрос на утверждение активов в Teams беседе. Алекс создает запрос на утверждение и назначает его Меган и Нестор. Ниже следующую часть для создания запроса на утверждение:

* Пользовательские представления можно применять с помощью `refresh` свойства адаптивных карт.
С помощью пользовательских представлений можно показать карточку с кнопками **Утверждение** или Отклонение для набора пользователей и показать карту без этих кнопок другим пользователям.

* Чтобы состояние карты всегда обновлялось, Teams можно использовать механизм редактирования сообщений. Например, для каждого утверждения бот может вызвать изменение сообщения для всех пользователей. Это изменение сообщения бота вызывает `adaptiveCard/action` запрос на вызов для всех пользователей автоматического обновления, на которые бот может отвечать с помощью обновленной пользовательской конкретной карты.

Дополнительные сведения см. [в сообщении бота](/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards).

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

В следующем коде приводится пример карточки утверждения с кнопками **Утверждение** и **Отклонение** :

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

Ниже показаны две роли, показанные пользователям в зависимости от запроса на утверждение:

* Базовая карточка утверждения. Показана пользователям, не в состав списка одобрений и запрос еще не утвержден или отклонен, `userIds` `refresh` а не часть списка в свойстве Adaptive Card JSON.
* Карточка **утверждения с** кнопками Утверждение или Отклонение:  `userIds` `refresh` Показана пользователям, которые являются частью списка утверждений, и списком в свойстве адаптивной карты JSON.

Чтобы отправить запрос на утверждение активов:

1. Алекс поднимает запрос на утверждение активов в беседе Teams и назначает его Меган и Нестор.
2. Бот отправляет базовую карточку утверждения в беседе.
3. Все остальные пользователи в беседе видят карточку, отправленную ботом. Автоматическое обновление запускается для Меган и Нестор, которые теперь видят определенную карточку пользователя с кнопками  **Утверждение** `userIds` `refresh` или Отклонение при добавлении их пользовательских МРЦ в список в свойстве адаптивной карты.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="Пользовательские просмотры":::

4. Нестор выбирает кнопку **Утверждение** , которая питание от `Action.Execute`. Бот получает запрос на `adaptiveCard/action` вызов, на который он может вернуть адаптивную карту в ответ.
5. Бот запускает редактирование сообщения с помощью обновленной карты, в которой говорится, что Нестор одобрил запрос, пока меган находится на стадии утверждения.
6. Редактирование сообщения бота запускает автоматическое обновление для Меган, и она видит обновленную карточку пользователя, которая говорит, что Нестор одобрил запрос, но также видит кнопки **Утверждение** или **Отклонение** . MRI пользователя Nestor `userIds` `refresh` удаляется из списка в свойстве этой адаптивной карты JSON в шагах 4 и 5. Теперь автоматическое обновление запускается только для Меган.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="В курсе конкретных представлений пользователей":::

7. Теперь Меган выбирает кнопку **Утверждение** , которая питание с `Action.Execute`. Бот получает запрос на `adaptiveCard/action` вызов, на который он может вернуть адаптивную карту в ответ.
8. Бот запускает редактирование сообщения с помощью обновленной карты, в которой говорится, что Нестор и Меган одобрили запрос.
9. Изменение сообщения бота не вызывает автоматического обновления. MRI пользователя `userIds` `refresh` Меган также удаляется из списка в свойстве этой адаптивной карты JSON в шагах 7 и 8.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="Просмотры на сегодняшний день":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a>Адаптивная карта, отправленная в ответ и `adaptiveCard/action``message edit`

В следующем коде приводится пример адаптивных `adaptiveCard/action` `message edit` карт, отправленных в ответ на действия 4 и 5.

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

В следующем коде приводится пример адаптивных `adaptiveCard/action` карт, отправленных в ответ на вызов с помощью автоматического обновления для шага 6:

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

В следующем коде приводится пример адаптивных `adaptiveCard/action` `message edit` карт, отправленных в ответ на действия 7 и 8.

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

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Адаптивные карточки последовательного рабочего процесса | Демонстрация того, как реализовать последовательное рабочий процесс, пользовательские представления и адаптивные карты в ботах. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
* [Пользовательские просмотры](User-Specific-Views.md)
* [Отзывы о завершении формы](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
