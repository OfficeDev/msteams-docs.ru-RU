---
title: Основы разговора
description: Введение в беседы
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: conversations basics messages
ms.openlocfilehash: a0c00d093827221968714aad88c35efa00660d82
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630987"
---
# <a name="conversation-basics"></a>Основы разговора

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Беседа — это серия сообщений, отправленных между Microsoft Teams ботом и одним или более пользователями. В следующей таблице 3 типа бесед, которые также называются области в Teams:

| Тип беседы | Описание |
| ------- | ----------- |
| `channel` | Этот тип беседы виден всем участникам канала. |
| `personal` | Этот тип беседы включает беседы между ботами и одним пользователем. |
| `groupChat` | Этот тип беседы включает чат между ботом и двумя или более пользователями. Он также позволяет вашему боту в чатах собраний. |

Бот ведет себя по-разному в зависимости от разговора, в который он вовлечен:

* Боты в беседах канала и группового чата требуют, чтобы пользователь @упомянул бота, чтобы вызвать его в канале.

* Боты в беседе один к одному не требуют @mention. Все сообщения, отправленные пользователем по маршрутам к боту.

> [!NOTE]
> Ботам можно разрешить получать все сообщения канала в команде, не @mentioned с помощью разрешений, определенных для ресурсов( RSC). В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../../../resources/dev-preview/developer-preview-intro.md) разработчиков. Дополнительные сведения см. в [сообщении о приеме всех сообщений канала с помощью RSC.](channel-messages-with-rsc.md)

Чтобы бот работал в определенной беседе или области, добавьте поддержку к этой области в [манифесте приложения.](~/resources/schema/manifest-schema.md)

Каждое сообщение в беседе с ботом — `Activity` это объект типа `messageType: message` . Когда пользователь отправляет сообщение, Teams отправляет сообщение боту, а бот обрабатывает сообщение. Кроме того, чтобы определить основные команды, на которые отвечает бот, можно добавить меню команд со списком команд для бота. Боты в группе или канале получают сообщения только в том случае, если они упоминаются @botname. Teams отправляет уведомления боту для событий беседы, которые происходят в сферах, где ваш бот активен. Вы можете зафиксировать эти события в коде и принять меры по ним.

Бот также может отправлять пользователям упреждающие сообщения. Проактивное сообщение — это любое сообщение, отправленное ботом, которое не является ответом на запрос пользователя. Вы можете форматирование сообщений бота, чтобы включить богатые карты, которые включают интерактивные элементы, такие как кнопки, текст, изображения, аудио, видео и так далее. Бот может динамически обновлять сообщения после их отправки, а не иметь сообщения в виде статических снимков данных. Сообщения также можно удалить с помощью метода Bot `DeleteActivity` Framework.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Сообщения в беседах с ботами](~/bots/how-to/conversations/conversation-messages.md)
