---
title: Универсальные действия для расширений сообщений на основе поиска
author: v-ypalikila
description: Из этой статьи вы узнаете о универсальных действиях и автоматическом обновлении адаптивных карточек в расширениях сообщений на основе поиска.
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
ms.openlocfilehash: 78b8c525b51603245fc379a826fa0cc11cbc5fd8
ms.sourcegitcommit: 176bbca74ba46b7ac298899d19a2d75087fb37c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/04/2022
ms.locfileid: "68376594"
---
# <a name="universal-actions-for-search-based-message-extensions"></a>Универсальные действия для расширений сообщений на основе поиска

Адаптивные карточки в расширениях сообщений на основе поиска теперь поддерживают универсальные действия. Чтобы включить универсальные действия для расширений сообщений на основе поиска, приложение должно соответствовать схеме универсальных действий для адаптивных карточек вместе со следующими требованиями:[](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#schema-for-universal-actions-for-adaptive-cards)

1. В манифесте приложения должен быть определен бот беседы.
1. Если у вас уже есть чат-бот, необходимо использовать тот же бот, который используется в расширении сообщения.
1. Если карточка отправляется в группе, приложение должно `team` `groupchat` указать или область бота в манифесте.

Пример схемы JSON со значениями `team` и их `groupchat` значениями:

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

Включите автоматическое обновление адаптивных карточек в расширениях сообщений на основе поиска, чтобы пользователи всегда могли видеть последние сведения. Чтобы включить этот параметр, определите `userIds` массив в  `29:<ID>` свойстве `8:orgid:<AAD ID>` в формате или формате `refresh` . Дополнительные сведения см. [в статье "Работа с универсальными действиями для адаптивных карточек"](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#user-ids-in-refresh).

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
> Автоматическое обновление включено для всех пользователей в групповом чате или  канале, в которых не более 60 пользователей. Для бесед (групповой чат или канал) с более чем 60 пользователями пользователи могут использовать кнопку обновления в меню параметров сообщения, чтобы получить последний результат.

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

JIT-доступ позволяет установить карточку или расширение сообщения для нескольких пользователей в групповом чате или канале. Чтобы обеспечить поддержку универсальных действий в расширениях сообщений на основе поиска, бот добавляется в беседу, в которую пользователь отправляет карточку ( `Action.Execute`с).

Когда пользователь выбирает карточку и отправляет ее в групповом чате или канале, появляется **запрос на JIT-установку** . Когда пользователь выберет **параметр отправки** , приложение будет добавлено для всех пользователей в чате или канале в фоновом режиме.

> [!NOTE]
> Для приложений, которые не имеют `Action.Execute` `refresh` и схемы определены, запрос на установку не отображается для пользователей.

Пример динамического потока пользователя установки ME и JIT:

  :::image type="content" source="../../../assets/videos/dynamic-me-jit-flow.gif" alt-text="GIF показывает поток пользователя для расширения динамических сообщений и установки JIT.":::

## <a name="see-also"></a>См. также

* [Расширения для сообщений](../../what-are-messaging-extensions.md)
* [Универсальные действия для адаптивных карточек](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Overview.md)
