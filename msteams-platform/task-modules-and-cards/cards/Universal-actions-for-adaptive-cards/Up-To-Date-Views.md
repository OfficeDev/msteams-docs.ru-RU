---
title: Актуальные представления
description: В этом модуле вы узнаете о актуальных представлениях карточек с использованием универсального бота с примерами кода в Microsoft Teams
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 5c6f7d13cd884baf9ffbc1fd30cafb7cfab33295
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143622"
---
# <a name="up-to-date-cards"></a>Актуальные карточки

Теперь вы можете предоставлять пользователям последние сведения на адаптивных карточках. Включите сочетание обновлений и изменений сообщений в Teams. Динамическое обновление пользовательских представлений до последнего состояния, как и при изменении службы. Например, для карт управления проектами или билетных карточек обновите комментарии и состояние задачи. Для утверждений отображается последнее состояние, а также предоставляется дифференцированная информация и действия.

Например, пользователь может создать запрос на утверждение актива в Teams беседе. Алексей создает запрос на утверждение и назначает его Мегане и Вестору. Ниже приведены две части для создания запроса на утверждение:

* Пользовательские представления можно применять с помощью `refresh` свойства адаптивных карточек.
С помощью пользовательских представлений можно отобразить карточку с кнопками "Утвердить" или "Отклонить" для набора пользователей и отобразить карточку без этих кнопок другим пользователям. 

* Чтобы состояние карточки всегда обновлялись, Teams можно использовать механизм редактирования сообщений. Например, при каждом утверждении бот может активировать изменение сообщения для всех пользователей. Это изменение сообщения бота активирует запрос `adaptiveCard/action` на вызов для всех пользователей автоматического обновления, на который бот может ответить с помощью обновленной карточки пользователя.

Дополнительные сведения см. [в статье о том, как изменить сообщение бота](/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards).

## <a name="approval-base-card"></a>Базовая карточка утверждения

В следующем коде приведен пример базовой карточки утверждения:

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

## <a name="approval-card-with-approve-and-reject-buttons"></a>Карточка утверждения с кнопками "Утвердить" и "Отклонить"

В следующем коде приведен пример карточки утверждения с кнопками **"** Утвердить" и **"Отклонить** ":

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

Ниже приведены две роли, которые отображаются пользователям в зависимости от запроса на утверждение:

* Базовая карточка утверждения: отображается для пользователей, не входящих в список утверждающих, и запрос еще не утвержден или отклонен и `userIds` `refresh` не является частью списка в свойстве JSON адаптивной карточки.
* Карточка **утверждения с** кнопками "Утвердить" или "Отклонить":  `userIds` `refresh` отображается для пользователей, которые являются частью списка утверждающих и списка в свойстве JSON адаптивной карточки.

Чтобы отправить запрос на утверждение актива, скажите следующее:

1. Алексей создает запрос на утверждение актива в беседе Teams и назначает его Мегане и Вестору.
2. Бот отправляет базовую карточку утверждения в беседе.
3. Все остальные пользователи беседы видят карточку, отправленную ботом. Автоматическое обновление активируется для Марта и Вложения,  `userIds` `refresh` которые теперь видят карточку пользователя с кнопками "Утвердить" или "Отклонить", когда их пользовательские МPI добавляются в список в свойстве адаптивной карточки.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="Пользовательские просмотры":::

4. Nestor **нажмет кнопку "** Утвердить".`Action.Execute` Бот получает запрос на вызов `adaptiveCard/action` , на который он может вернуть адаптивную карточку в ответе.
5. Бот активирует изменение сообщения с помощью обновленной карточки, в которой говорится, что Nestor утверждает запрос, пока Ожидается утверждение М.
6. При изменении сообщения бота запускается автоматическое обновление для Марты, и она видит обновленную карточку пользователя, которая говорит, что Nestor утверждает запрос, но также  видит кнопки  "Утвердить" или "Отклонить". MRI пользователя Nestor `userIds` `refresh` удаляется из списка в свойстве этого JSON адаптивной карточки на шагах 4 и 5. Теперь автоматическое обновление активируется только для Megan.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="Актуальные пользовательские представления":::

7. Теперь Она нажмет кнопку "Утвердить". `Action.Execute` Бот получает запрос на вызов `adaptiveCard/action` , на который он может вернуть адаптивную карточку в ответе.
8. Бот инициирует изменение сообщения с помощью обновленной карточки, в которой говорится, что Nestor и Марта утверждены запросом.
9. При изменении сообщения бота автоматическое обновление не запускается. MRI пользователя Megan `userIds` `refresh` также удаляется из списка в свойстве этого JSON адаптивной карточки на шагах 7 и 8.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="Актуальные представления":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a>Адаптивная карточка, отправленная в ответ и `adaptiveCard/action``message edit`

В следующем коде приведен пример адаптивных `adaptiveCard/action` `message edit` карточек, отправленных в ответ на шаги 4 и 5.

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

В следующем коде приведен пример адаптивных карточек, отправляемых в ответ на `adaptiveCard/action` вызов с помощью автоматического обновления для шага 6:

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

В следующем коде приведен пример адаптивных карточек `adaptiveCard/action` `message edit` , отправленных в ответ на шаги 7 и 8.

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
| Адаптивные карточки последовательных рабочих процессов | Демонстрация реализации последовательных рабочих процессов, пользовательских представлений и актуальных адаптивных карточек в ботах. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>См. также

* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
* [Пользовательские просмотры](User-Specific-Views.md)
* [Отзывы о завершении формы](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
