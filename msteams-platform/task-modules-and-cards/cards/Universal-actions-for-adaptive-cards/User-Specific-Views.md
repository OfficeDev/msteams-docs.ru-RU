---
title: Пользовательские просмотры
description: Пример для пользовательских представлений с помощью универсальных действий
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: d607250d0d34367c097cdfd25050e4180f72eeda
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156288"
---
# <a name="user-specific-views"></a>Пользовательские просмотры

Ранее, если адаптивные карточки были отправлены в беседе Teams, все пользователи видят одно и то же содержимое карты. С введением модели универсальных действий и адаптивных карт разработчики ботов теперь могут предоставлять пользователям специальные представления `refresh` адаптивных карт. Теперь та же адаптивная карта может обновиться до специальной адаптивной карты пользователя. Не более 60 разных пользователей могут видеть другую версию карты с дополнительной информацией или действиями. Адаптивная карта предоставляет мощные сценарии, такие как утверждения, элементы управления создателями опросов, билеты, управление инцидентами и карты управления проектами.

Например, Меган, инспектор безопасности в Contoso, хочет создать инцидент и назначить его Алексу. Меган также хочет, чтобы все в команде знали об инциденте. Меган использует расширение сообщений об инцидентах Contoso с питанием от универсальных действий для адаптивных карт.

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Представления для мобильных пользователей":::

# <a name="desktop"></a>[Компьютер](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Пользовательские просмотры":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a>Пользовательские представления для адаптивных карт

В следующем коде приводится пример адаптивных карт:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView",
      "data": {
              "refresh info": "<refresh info>"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ]
}
```

**Чтобы отправить адаптивные карты, обновить пользовательские представления и вызвать запросы к боту**

1. Когда Меган создает новый инцидент, бот отправляет адаптивную карту или общую карту с сведениями об инциденте в Teams беседе.
2. Теперь эта карта автоматически обновляется до пользовательского представления для Меган и Алекс. МРИС пользователя Алекса и Меган добавляются в свойство `userIds` `refresh` свойства адаптивной карты JSON. Карта остается той же для других пользователей в беседе.
3. Для Меган автоматическое обновление вызывает запрос `adaptiveCard/action` на вызов бота. Бот может вернуть карточку создателя инцидента с помощью `Edit` кнопки в качестве ответа на этот запрос на вызов.
4. Аналогично для Alex автоматическое обновление вызывает другой запрос `adaptiveCard/action` на вызов бота. Бот может вернуть кнопку карточки владельца инцидента `Resolve` в качестве ответа на этот запрос на вызов.

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>Вызов запроса, отосланного Teams клиента боту

В следующем коде приводится пример запроса на вызов, отосланного от Teams клиента Алекса и Меган в бот:

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "editOrResolveView",
      "data": { 
            "refresh info": "<refresh info>"
      } 
    },
    "trigger": "automatic" 
  }
}
```

## <a name="adaptivecardaction-invoke-response-card"></a>adaptiveCard/action вызывает карточку ответа

В следующем коде приводится пример адаптивной карты/действия, вызываемой для Меган:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Edit",
      "verb": "edit",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>adaptiveCard/action вызывает карточку ответа для Alex

В следующем коде приводится пример адаптивной карточки вызова ответа на действия для Alex:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Resolve",
      "verb": "resolve",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="invoke-response-to-return-adaptive-cards"></a>Вызов ответа для возврата адаптивных карт

В следующем коде приводится пример ответа на вызов для возврата адаптивных карт:

```C#
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

Рекомендации по разработке карт, которые необходимо иметь в виду при разработке пользовательских представлений:

* Можно создать не более **60** пользовательских представлений для определенной карты, отправленной в чат или канал, указав их `userIds` в `refresh` разделе.
* **Базовая карта:** Базовая версия карты, которую разработчик бота отправляет в чат. Базовая версия — это версия адаптивной карты для всех пользователей, не указанных в `userIds` разделе.
* Обновление сообщения можно использовать для обновления базовой карты и одновременного обновления пользовательской конкретной карты. Открытие чата или канала также обновляет карту для пользователей с включенной поддержкой обновления.
* В сценариях с более крупными группами, в которых пользователи переключаются на представление о действии, которое требует динамических обновлений для ответчиков, можно продолжать добавлять до 60 пользователей в `userIds` список. Первый ответ можно удалить из списка при ответе 61-го пользователя. Для пользователей, которые удаляются из списка, вы можете предоставить ручную кнопку обновления или использовать кнопку обновления в меню параметры сообщений, чтобы `userIds` получить последний результат.
* Дайте пользователям подсказку для получения пользовательского представления, в котором они видят только определенное представление карты или какие-либо действия.

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Адаптивные карточки последовательного рабочего процесса | Демонстрация того, как реализовать последовательное рабочий процесс, пользовательские представления и адаптивные карты в ботах. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
* [Просмотры на сегодняшний день](Up-To-Date-Views.md)
