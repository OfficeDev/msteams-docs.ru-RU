---
title: Основы разговора
description: Введение в беседы
ms.topic: overview
ms.author: anclear
keyword: conversations basics messages
ms.openlocfilehash: eff1c6fe18f7b2ba082b5075b6c1806f41b68a6b
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2021
ms.locfileid: "51996039"
---
# <a name="conversation-basics"></a><span data-ttu-id="a2d12-103">Основы разговора</span><span class="sxs-lookup"><span data-stu-id="a2d12-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="a2d12-104">Беседа — это серия сообщений, отправленных между ботом Microsoft Teams и одним или более пользователями.</span><span class="sxs-lookup"><span data-stu-id="a2d12-104">A conversation is a series of messages sent between your Microsoft Teams bot and one or more users.</span></span> <span data-ttu-id="a2d12-105">В следующей таблице 3 типа бесед, которые также называются области в Teams:</span><span class="sxs-lookup"><span data-stu-id="a2d12-105">The following table provides the three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="a2d12-106">Тип беседы</span><span class="sxs-lookup"><span data-stu-id="a2d12-106">Conversation type</span></span> | <span data-ttu-id="a2d12-107">Описание</span><span class="sxs-lookup"><span data-stu-id="a2d12-107">Description</span></span> |
| ------- | ----------- |
| `channel` | <span data-ttu-id="a2d12-108">Этот тип беседы виден всем участникам канала.</span><span class="sxs-lookup"><span data-stu-id="a2d12-108">This conversation type is visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="a2d12-109">Этот тип беседы включает беседы между ботами и одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="a2d12-109">This conversation type includes conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="a2d12-110">Этот тип беседы включает чат между ботом и двумя или более пользователями.</span><span class="sxs-lookup"><span data-stu-id="a2d12-110">This conversation type includes chat between a bot and two or more users.</span></span> <span data-ttu-id="a2d12-111">Он также позволяет вашему боту в чатах собраний.</span><span class="sxs-lookup"><span data-stu-id="a2d12-111">It also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="a2d12-112">Бот ведет себя по-разному в зависимости от разговора, в который он вовлечен:</span><span class="sxs-lookup"><span data-stu-id="a2d12-112">A bot behaves differently depending on the conversation it is involved in:</span></span>

* <span data-ttu-id="a2d12-113">Боты в беседах с каналами и групповыми чатами требуют от пользователя @ упоминания бота, чтобы вызвать его в канале.</span><span class="sxs-lookup"><span data-stu-id="a2d12-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="a2d12-114">Боты в беседе один к одному не требуют упоминания @.</span><span class="sxs-lookup"><span data-stu-id="a2d12-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="a2d12-115">Все сообщения, отправленные пользователем по маршрутам к боту.</span><span class="sxs-lookup"><span data-stu-id="a2d12-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="a2d12-116">Чтобы бот работал в определенной беседе или области, добавьте поддержку к этой области в [манифесте приложения.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="a2d12-116">For the bot to work in a particular conversation or scope, add support to that scope in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

<span data-ttu-id="a2d12-117">Каждое сообщение в беседе с ботом — `Activity` это объект типа `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="a2d12-117">Each message in a bot conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="a2d12-118">Когда пользователь отправляет сообщение, Teams отправляет сообщение боту, а бот обрабатывает сообщение.</span><span class="sxs-lookup"><span data-stu-id="a2d12-118">When a user sends a message, Teams posts the message to your bot and the bot handles the message.</span></span> <span data-ttu-id="a2d12-119">Кроме того, чтобы определить основные команды, на которые отвечает бот, можно добавить меню команд со списком команд для бота.</span><span class="sxs-lookup"><span data-stu-id="a2d12-119">In addition, to define core commands that your bot responds to, you can add a command menu with a drop-down list of commands for your bot.</span></span> <span data-ttu-id="a2d12-120">Боты в группе или канале получают сообщения только в том случае, если они упоминаются @botname.</span><span class="sxs-lookup"><span data-stu-id="a2d12-120">Bots in a group or channel only receive messages when they are mentioned @botname.</span></span> <span data-ttu-id="a2d12-121">Teams отправляет уведомления вашему боту для событий беседы, которые происходят в сферах, где ваш бот активен.</span><span class="sxs-lookup"><span data-stu-id="a2d12-121">Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="a2d12-122">Вы можете зафиксировать эти события в коде и принять меры по ним.</span><span class="sxs-lookup"><span data-stu-id="a2d12-122">You can capture these events in your code and take action on them.</span></span> 

<span data-ttu-id="a2d12-123">Бот также может отправлять пользователям упреждающие сообщения.</span><span class="sxs-lookup"><span data-stu-id="a2d12-123">A bot can also send proactive messages to users.</span></span> <span data-ttu-id="a2d12-124">Проактивное сообщение — это любое сообщение, отправленное ботом, которое не является ответом на запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="a2d12-124">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="a2d12-125">Вы можете форматирование сообщений бота, чтобы включить богатые карты, которые включают интерактивные элементы, такие как кнопки, текст, изображения, аудио, видео и так далее.</span><span class="sxs-lookup"><span data-stu-id="a2d12-125">You can format your bot messages to include rich cards that include interactive elements, such as buttons, text, images, audio, video, and so on.</span></span> <span data-ttu-id="a2d12-126">Бот может динамически обновлять сообщения после их отправки, а не иметь сообщения в виде статических снимков данных.</span><span class="sxs-lookup"><span data-stu-id="a2d12-126">Bot can dynamically update messages after sending them, instead of having your messages as static snapshots of data.</span></span> <span data-ttu-id="a2d12-127">Сообщения также можно удалить с помощью метода Bot `DeleteActivity` Framework.</span><span class="sxs-lookup"><span data-stu-id="a2d12-127">Messages can also be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

## <a name="next-step"></a><span data-ttu-id="a2d12-128">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="a2d12-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a2d12-129">Сообщения в беседах с ботами</span><span class="sxs-lookup"><span data-stu-id="a2d12-129">Messages in bot conversations</span></span>](~/bots/how-to/conversations/conversation-messages.md)
