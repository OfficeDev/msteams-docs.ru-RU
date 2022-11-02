---
title: Универсальные действия для расширений сообщений на основе поиска
author: v-ypalikila
description: Из этой статьи вы узнаете об универсальных действиях и автоматическом обновлении адаптивных карточек в расширениях сообщений на основе поиска.
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
ms.openlocfilehash: 18f5b783797d69144aac82e5ebd95fc30dad57a2
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819970"
---
# <a name="universal-actions-for-search-based-message-extensions"></a>Универсальные действия для расширений сообщений на основе поиска

Адаптивные карточки в расширениях сообщений на основе поиска теперь поддерживают универсальные действия. Чтобы включить универсальные действия для расширений сообщений на основе поиска, приложение должно соответствовать [схеме универсальных действий для адаптивных карточек](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#schema-for-universal-actions-for-adaptive-cards) , а также следующим требованиям:

1. Приложение должно иметь бот беседы, определенный в манифесте приложения.
1. Если у вас уже есть чат-бот, необходимо использовать тот же бот, который используется в расширении сообщений.
1. Если карточка отправляется в группе, приложение должно указать или `groupchat` область `team` действия бота в манифесте.

Пример схемы JSON со значениями `team` и `groupchat` :

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "scopes": [
                    "team",
                    "personal",
                    "groupchat"
                ]
        }
    ],
    "composeExtensions": [
        {
            "canUpdateConfiguration": true,
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%", // Use the same bot as what is specified in the bots section above
        }
    ]
}
```

## <a name="automatic-refresh-for-adaptive-cards-in-search-based-message-extensions"></a>Автоматическое обновление адаптивных карточек в расширениях сообщений на основе поиска

Включите автоматическое обновление адаптивных карточек в расширениях сообщений на основе поиска, чтобы пользователи всегда видели последние сведения. Чтобы включить этот параметр, определите `userIds` массив в `29:<ID>` свойстве `refresh` или `8:orgid:<AAD ID>` в формате . Дополнительные сведения см. в [статье Работа с универсальными действиями для адаптивных карточек](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#user-ids-in-refresh).

Пример массива `userIds` в свойстве `refresh` :

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "userIds": [
                "8:orgid:<AADID>",
                "29:<id>"
            ],
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

> [!NOTE]
> Автоматическое обновление включено для всех пользователей в групповом чате или канале с *менее* чем 60 пользователями. Для бесед (группового чата или канала) с более чем 60 пользователями пользователи могут использовать кнопку обновления в меню параметров сообщения, чтобы получить последний результат.

Пример в `Action.Execute` свойстве `refresh` :

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

## <a name="just-in-time-install"></a>JIT-установка

JIT позволяет установить карточку или расширение для сообщений для нескольких пользователей в групповом чате или канале. Для поддержки универсальных действий в расширениях для сообщений на основе поиска бот добавляется в беседу, в которой пользователь отправляет карточку (с `Action.Execute`).

Когда пользователь выбирает карточку и отправляет ее в групповом чате или канале, появляется запрос на установку **JIT** . Когда пользователь выберет параметр **отправки** , приложение добавляется для всех пользователей в чате или канале в фоновом режиме.

> [!NOTE]
> Для приложений, в которых нет `Action.Execute` и `refresh` определена схема, запрос на установку не отображается пользователям.

Пример потока пользователя динамической установки ME и JIT:

  :::image type="content" source="../../../assets/videos/dynamic-me-jit-flow.gif" alt-text="GIF показывает пользовательский поток для динамического расширения сообщений и JIT-установки.":::

## <a name="see-also"></a>См. также

* [Расширения для сообщений](../../what-are-messaging-extensions.md)
* [Адаптивные карточки](../../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Универсальные действия для адаптивных карточек](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Overview.md)
