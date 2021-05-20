---
title: Отправка и получение сообщений с помощью бота
description: Описывает, как отправлять и получать сообщения с ботами в Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: команды ботов сообщения
ms.date: 05/20/2019
ms.openlocfilehash: e1926afe42bca45eda5f39be1be8342452b3aa24
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566497"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="588db-104">Поговорить с Microsoft Teams ботом</span><span class="sxs-lookup"><span data-stu-id="588db-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="588db-105">Беседа — это серия сообщений, отправляемых ботом одним или несколькими пользователями.</span><span class="sxs-lookup"><span data-stu-id="588db-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="588db-106">Существует три типа бесед (также называемых областью) в Teams:</span><span class="sxs-lookup"><span data-stu-id="588db-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="588db-107">`teams` Также называются разговоры канала, видимые всем участникам канала.</span><span class="sxs-lookup"><span data-stu-id="588db-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="588db-108">`personal` Разговоры между ботами и одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="588db-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="588db-109">`groupChat` Чат между ботом и двумя или более пользователями.</span><span class="sxs-lookup"><span data-stu-id="588db-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="588db-110">Бот ведет себя немного по-разному в зависимости от того, в каком разговоре он участвует:</span><span class="sxs-lookup"><span data-stu-id="588db-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="588db-111">[Боты в разговоре в канале и групповом чате](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) требуют, чтобы @mention использовать бота, чтобы вызвать его в канале.</span><span class="sxs-lookup"><span data-stu-id="588db-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="588db-112">[Боты в разговорах одного пользователя](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) не требуют @mention - пользователь может просто набрать.</span><span class="sxs-lookup"><span data-stu-id="588db-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @mention -  the user can just type.</span></span>

<span data-ttu-id="588db-113">Для того, чтобы бот работал в определенном объеме, он должен быть указан в качестве поддержки этой области в манифесте.</span><span class="sxs-lookup"><span data-stu-id="588db-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="588db-114">Области определяются и обсуждаются далее в [Справке Манифеста.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="588db-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="588db-115">Проактивные сообщения</span><span class="sxs-lookup"><span data-stu-id="588db-115">Proactive messages</span></span>

<span data-ttu-id="588db-116">Боты могут участвовать в разговоре или инициировать его.</span><span class="sxs-lookup"><span data-stu-id="588db-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="588db-117">Большинство сообщений в ответ на другое сообщение.</span><span class="sxs-lookup"><span data-stu-id="588db-117">Most communication is in response to another message.</span></span> <span data-ttu-id="588db-118">Если бот инициирует разговор, это называется *упреждающим сообщением.*</span><span class="sxs-lookup"><span data-stu-id="588db-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="588db-119">Вот некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="588db-119">Examples include:</span></span>

* <span data-ttu-id="588db-120">Приветствия</span><span class="sxs-lookup"><span data-stu-id="588db-120">Welcome messages</span></span>
* <span data-ttu-id="588db-121">Уведомления о событии</span><span class="sxs-lookup"><span data-stu-id="588db-121">Event notifications</span></span>
* <span data-ttu-id="588db-122">Сообщения для опроса</span><span class="sxs-lookup"><span data-stu-id="588db-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="588db-123">Основы разговора</span><span class="sxs-lookup"><span data-stu-id="588db-123">Conversation basics</span></span>

<span data-ttu-id="588db-124">Каждое сообщение является объектом `Activity` типа `messageType: message`.</span><span class="sxs-lookup"><span data-stu-id="588db-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="588db-125">Когда пользователь отправляет сообщение, Teams отправляет его боту; в частности, он отправляет объект JSON в конечную точку обмена сообщениями бота.</span><span class="sxs-lookup"><span data-stu-id="588db-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="588db-126">Ваш бот рассматривает сообщение, чтобы определить его тип и реагирует соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="588db-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="588db-127">Боты также поддерживают сообщения в стиле событий.</span><span class="sxs-lookup"><span data-stu-id="588db-127">Bots also support event-style messages.</span></span> <span data-ttu-id="588db-128">Для получения дополнительной информации [см. События бота Handle в Microsoft Teams.](~/resources/bot-v3/bots-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="588db-128">For more information, see [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md).</span></span> <span data-ttu-id="588db-129">В настоящее время речь не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="588db-129">Speech is currently not supported.</span></span>

<span data-ttu-id="588db-130">Сообщения по большей части одинаковы во всех сферах, но есть различия в том, как бот доступен в пользовательском интерфейсе и различия за кулисами, которые вам нужно будет знать.</span><span class="sxs-lookup"><span data-stu-id="588db-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="588db-131">Основной разговор обрабатывается через Бот Рамочный разъем, единый API REST, чтобы ваш бот волен общаться с Teams другими каналами.</span><span class="sxs-lookup"><span data-stu-id="588db-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="588db-132">Bot Builder SDK обеспечивает легкий доступ к этому API, дополнительную функциональность для управления потоком и состоянием разговоров, а также простые способы включения когнитивных услуг, таких как обработка естественного языка (NLP).</span><span class="sxs-lookup"><span data-stu-id="588db-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="588db-133">Содержимое сообщения</span><span class="sxs-lookup"><span data-stu-id="588db-133">Message content</span></span>

<span data-ttu-id="588db-134">Ваш бот может отправлять богатые тексты, фотографии и карты.</span><span class="sxs-lookup"><span data-stu-id="588db-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="588db-135">Пользователи могут отправлять богатый текст и фотографии вашему боту.</span><span class="sxs-lookup"><span data-stu-id="588db-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="588db-136">Вы можете указать тип содержимого, с которого ваш бот может справиться в Microsoft Teams настройки для вашего бота.</span><span class="sxs-lookup"><span data-stu-id="588db-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="588db-137">Формат</span><span class="sxs-lookup"><span data-stu-id="588db-137">Format</span></span> | <span data-ttu-id="588db-138">От пользователя к боту</span><span class="sxs-lookup"><span data-stu-id="588db-138">From user to bot</span></span>  | <span data-ttu-id="588db-139">От бота к пользователю</span><span class="sxs-lookup"><span data-stu-id="588db-139">From bot to user</span></span> |  <span data-ttu-id="588db-140">Примечания</span><span class="sxs-lookup"><span data-stu-id="588db-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="588db-141">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="588db-141">Rich text</span></span> | <span data-ttu-id="588db-142">✔</span><span class="sxs-lookup"><span data-stu-id="588db-142">✔</span></span> | <span data-ttu-id="588db-143">✔</span><span class="sxs-lookup"><span data-stu-id="588db-143">✔</span></span> |  |
| <span data-ttu-id="588db-144">Изображения</span><span class="sxs-lookup"><span data-stu-id="588db-144">Pictures</span></span> | <span data-ttu-id="588db-145">✔</span><span class="sxs-lookup"><span data-stu-id="588db-145">✔</span></span> | <span data-ttu-id="588db-146">✔</span><span class="sxs-lookup"><span data-stu-id="588db-146">✔</span></span> | <span data-ttu-id="588db-147">Максимум 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированные GIF не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="588db-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported.</span></span> |
| <span data-ttu-id="588db-148">Карточки</span><span class="sxs-lookup"><span data-stu-id="588db-148">Cards</span></span> | <span data-ttu-id="588db-149">✖</span><span class="sxs-lookup"><span data-stu-id="588db-149">✖</span></span> | <span data-ttu-id="588db-150">✔</span><span class="sxs-lookup"><span data-stu-id="588db-150">✔</span></span> | <span data-ttu-id="588db-151">Смотрите [справку Teams карты для поддерживаемых](~/task-modules-and-cards/cards/cards-reference.md) карт.</span><span class="sxs-lookup"><span data-stu-id="588db-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="588db-152">Эмодзи</span><span class="sxs-lookup"><span data-stu-id="588db-152">Emojis</span></span> | <span data-ttu-id="588db-153">✖</span><span class="sxs-lookup"><span data-stu-id="588db-153">✖</span></span> | <span data-ttu-id="588db-154">✔</span><span class="sxs-lookup"><span data-stu-id="588db-154">✔</span></span> | <span data-ttu-id="588db-155">Teams в настоящее время поддерживает смайлики через UTF-16, такие как, U'1F600 для ухмыляясь лица.</span><span class="sxs-lookup"><span data-stu-id="588db-155">Teams currently supports emojis via UTF-16 such as, U+1F600 for grinning face.</span></span> |
|

<span data-ttu-id="588db-156">Для получения дополнительной информации о типах взаимодействия ботов, поддерживаемых Bot Framework, на которых основаны боты в командах, смотрите документацию Bot Framework о [потоке](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) разговоров и связанных с ней концепциях в [документации для Bot Builder SDK для .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) [и Bot Builder SDK на Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="588db-156">For more information on the types of bot interaction supported by the Bot Framework, which bots in teams are based on, see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="588db-157">Форматирование сообщения</span><span class="sxs-lookup"><span data-stu-id="588db-157">Message formatting</span></span>

<span data-ttu-id="588db-158">Вы можете установить дополнительное [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) свойство a, `message` чтобы контролировать, как отображается текстовое содержимое вашего сообщения.</span><span class="sxs-lookup"><span data-stu-id="588db-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="588db-159">Можно [просмотреть форматирование](~/resources/bot-v3/bots-message-format.md) сообщений для подробного описания поддерживаемого форматирования в сообщениях бота.</span><span class="sxs-lookup"><span data-stu-id="588db-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="588db-160">Вы можете установить дополнительное [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) свойство для управления тем, как отображается текстовое содержимое вашего сообщения.</span><span class="sxs-lookup"><span data-stu-id="588db-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="588db-161">Для получения подробной информации о том Teams поддерживает форматирование текста в командах, [смотрите форматирование текста в сообщениях бота.](~/resources/bot-v3/bots-text-formats.md)</span><span class="sxs-lookup"><span data-stu-id="588db-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="588db-162">Для получения дополнительной информации о форматировании карт в сообщениях, [см.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="588db-162">For more information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="588db-163">Сообщения изображения</span><span class="sxs-lookup"><span data-stu-id="588db-163">Picture messages</span></span>

<span data-ttu-id="588db-164">Фотографии отправляются путем добавления вложений в сообщение.</span><span class="sxs-lookup"><span data-stu-id="588db-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="588db-165">Более подробную информацию о вложениях можно найти в [документации Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="588db-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span></span>

<span data-ttu-id="588db-166">Изображения могут быть не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="588db-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="588db-167">Мы рекомендуем указать высоту и ширину каждого изображения с помощью XML.</span><span class="sxs-lookup"><span data-stu-id="588db-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="588db-168">Если вы используете Markdown, размер изображения по умолчанию до 256×256.</span><span class="sxs-lookup"><span data-stu-id="588db-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="588db-169">Пример:</span><span class="sxs-lookup"><span data-stu-id="588db-169">For example:</span></span>

* <span data-ttu-id="588db-170">Воспользуйтесь `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="588db-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="588db-171">Не используйте `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="588db-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages&quot;></a><span data-ttu-id=&quot;588db-172&quot;>Получение сообщений</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;588db-172&quot;>Receiving messages</span></span>

<span data-ttu-id=&quot;588db-173&quot;>В зависимости от того, какие области объявлены, ваш бот может получать сообщения в следующих контекстах:</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;588db-173&quot;>Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id=&quot;588db-174&quot;>**личный чат** Пользователи могут взаимодействовать в приватном разговоре с ботом, просто выбрав добавленного бота в истории чата, или введя его имя или идентификатор приложения в поле To: box в новом чате.</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;588db-174&quot;>**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id=&quot;588db-175&quot;>**Каналы** Бот может быть упомянут в _канале,_ если он был добавлен в команду.</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;588db-175&quot;>**Channels** A bot can be mentioned (&quot;@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="588db-176">Обратите внимание, что дополнительные ответы на бота в канале требуют упоминания бота.</span><span class="sxs-lookup"><span data-stu-id="588db-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="588db-177">Он не будет отвечать на ответы там, где он не упоминается.</span><span class="sxs-lookup"><span data-stu-id="588db-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="588db-178">Для входящих сообщений ваш бот [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) получает объект `messageType: message` типа.</span><span class="sxs-lookup"><span data-stu-id="588db-178">For incoming messages, your bot receives an [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) object of type `messageType: message`.</span></span> <span data-ttu-id="588db-179">Хотя объект `Activity` может содержать другие типы информации, такие как [обновления каналов, отправленные](~/resources/bot-v3/bots-notifications.md#channel-updates) вашему боту, `message` тип представляет собой связь между ботом и пользователем.</span><span class="sxs-lookup"><span data-stu-id="588db-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="588db-180">Ваш бот получает полезную нагрузку, которая содержит сообщение `Text` пользователя, а также другую информацию о пользователе, источнике сообщения и Teams информации.</span><span class="sxs-lookup"><span data-stu-id="588db-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="588db-181">Следует отметить:</span><span class="sxs-lookup"><span data-stu-id="588db-181">Of note:</span></span>

* <span data-ttu-id="588db-182">`timestamp` Дата и время сообщения в скоординированном универсальном времени (UTC).</span><span class="sxs-lookup"><span data-stu-id="588db-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC).</span></span>
* <span data-ttu-id="588db-183">`localTimestamp` Дата и время сообщения в часовом поясе отправителя.</span><span class="sxs-lookup"><span data-stu-id="588db-183">`localTimestamp` The date and time of the message in the time zone of the sender.</span></span>
* <span data-ttu-id="588db-184">`channelId` Всегда "мстемы".</span><span class="sxs-lookup"><span data-stu-id="588db-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="588db-185">Это относится к каналу фреймворка бота, а не к каналу команд.</span><span class="sxs-lookup"><span data-stu-id="588db-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="588db-186">`from.id` Уникальный и зашифрованный идентификатор для этого пользователя для вашего бота; подходит в качестве ключа, если вашему приложению необходимо хранить данные пользователей.</span><span class="sxs-lookup"><span data-stu-id="588db-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="588db-187">Он уникален для вашего бота и не может быть непосредственно использован за пределами вашего экземпляра бота каким-либо значимым образом, чтобы определить этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="588db-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>
* <span data-ttu-id="588db-188">`channelData.tenant.id` Идентификатор арендатора для пользователя.</span><span class="sxs-lookup"><span data-stu-id="588db-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="588db-189">`from.id` уникален для вашего бота и не может быть непосредственно использован за пределами вашего экземпляра бота в какой-либо значимый способ идентификации этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="588db-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="588db-190">Объединение каналов и частных взаимодействий с ботом</span><span class="sxs-lookup"><span data-stu-id="588db-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="588db-191">При взаимодействии в канале, ваш бот должен быть умным о принятии определенных разговоров в автономном режиме с пользователем.</span><span class="sxs-lookup"><span data-stu-id="588db-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="588db-192">Например, предположим, что пользователь пытается координировать сложную задачу, например планирование с набором членов группы.</span><span class="sxs-lookup"><span data-stu-id="588db-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="588db-193">Вместо того, чтобы вся последовательность взаимодействий видна каналу, рассмотрите возможность отправки личного сообщения чата пользователю.</span><span class="sxs-lookup"><span data-stu-id="588db-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="588db-194">Ваш бот должен быть в состоянии легко переход пользователя между личными и канал разговоры, не теряя состояния.</span><span class="sxs-lookup"><span data-stu-id="588db-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="588db-195">Не забудьте обновить канал, когда взаимодействие будет завершено, чтобы уведомить других членов команды.</span><span class="sxs-lookup"><span data-stu-id="588db-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="588db-196">Полный пример входящих схем</span><span class="sxs-lookup"><span data-stu-id="588db-196">Full inbound schema example</span></span>

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

> [!NOTE]
> <span data-ttu-id="588db-197">Текстовое поле для входящих сообщений иногда содержит упоминания.</span><span class="sxs-lookup"><span data-stu-id="588db-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="588db-198">Будьте уверены, чтобы должным образом проверить и лишить их.</span><span class="sxs-lookup"><span data-stu-id="588db-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="588db-199">Для получения дополнительной информации [см.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)</span><span class="sxs-lookup"><span data-stu-id="588db-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="588db-200">Teams канал</span><span class="sxs-lookup"><span data-stu-id="588db-200">Teams channel data</span></span>

<span data-ttu-id="588db-201">Объект `channelData` содержит Teams информацию и является окончательным источником для командных и каналов.</span><span class="sxs-lookup"><span data-stu-id="588db-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="588db-202">Вы должны кэшировать и использовать эти идентификаторы в качестве ключей для локального хранения.</span><span class="sxs-lookup"><span data-stu-id="588db-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="588db-203">Объект `channelData` не входит в сообщения в личных беседах, так как они происходят вне какого-либо канала.</span><span class="sxs-lookup"><span data-stu-id="588db-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="588db-204">Типичный объект channelData в действии, отправленной вашему боту, содержит следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="588db-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="588db-205">`eventType`Teams тип события; пройдено только в случаях [событий модификации канала.](~/resources/bot-v3/bots-notifications.md#channel-updates)</span><span class="sxs-lookup"><span data-stu-id="588db-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="588db-206">`tenant.id`Azure Active Directory арендатора; прошли во всех контекстах.</span><span class="sxs-lookup"><span data-stu-id="588db-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts.</span></span>
* <span data-ttu-id="588db-207">`team` Пройдено только в контексте канала, а не в личном чате.</span><span class="sxs-lookup"><span data-stu-id="588db-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="588db-208">`id` GUID для канала.</span><span class="sxs-lookup"><span data-stu-id="588db-208">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="588db-209">`name`Название команды; пройдено только в случаях [переименования команды событий.](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span><span class="sxs-lookup"><span data-stu-id="588db-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates).</span></span>
* <span data-ttu-id="588db-210">`channel` Пройдено только в контексте канала, когда бот упоминается или для событий в каналах в командах, где бот был добавлен.</span><span class="sxs-lookup"><span data-stu-id="588db-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="588db-211">`id` GUID для канала.</span><span class="sxs-lookup"><span data-stu-id="588db-211">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="588db-212">`name`Название канала; пройдено только в случаях [событий модификации канала.](~/resources/bot-v3/bots-notifications.md#channel-updates)</span><span class="sxs-lookup"><span data-stu-id="588db-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="588db-213">`channelData.teamsTeamId` Устаревшие.</span><span class="sxs-lookup"><span data-stu-id="588db-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="588db-214">Это свойство включено только для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="588db-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="588db-215">`channelData.teamsChannelId` Устаревшие.</span><span class="sxs-lookup"><span data-stu-id="588db-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="588db-216">Это свойство включено только для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="588db-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="588db-217">Пример объекта channelData (каналСоздаемое событие)</span><span class="sxs-lookup"><span data-stu-id="588db-217">Example channelData object (channelCreated event)</span></span>

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

### <a name="net-example"></a><span data-ttu-id="588db-218">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="588db-218">.NET example</span></span>

<span data-ttu-id="588db-219">Пакет [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet предоставляет `TeamsChannelData` специализированный объект, который предоставляет свойства для доступа Teams конкретной информации.</span><span class="sxs-lookup"><span data-stu-id="588db-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="588db-220">Отправка ответов на сообщения</span><span class="sxs-lookup"><span data-stu-id="588db-220">Sending replies to messages</span></span>

<span data-ttu-id="588db-221">Чтобы ответить на существующее сообщение, [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) позвоните в .NET [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) или в Node.js.</span><span class="sxs-lookup"><span data-stu-id="588db-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) in Node.js.</span></span> <span data-ttu-id="588db-222">Bot Builder SDK обрабатывает все детали.</span><span class="sxs-lookup"><span data-stu-id="588db-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="588db-223">Если вы решите использовать API REST, вы также можете позвонить в [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) конечную точку.</span><span class="sxs-lookup"><span data-stu-id="588db-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) endpoint.</span></span>

<span data-ttu-id="588db-224">Содержимое сообщения само по себе может содержать простой текст или некоторые из Bot Framework поставляется [карты и действия карты](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="588db-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="588db-225">Обратите внимание, что в своей выездной схеме вы всегда должны использовать то же `serviceUrl` самое, что и полученную схему.</span><span class="sxs-lookup"><span data-stu-id="588db-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="588db-226">Имейте в виду, что `serviceUrl` значение, как правило, стабильны, но может измениться.</span><span class="sxs-lookup"><span data-stu-id="588db-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="588db-227">Когда приходит новое сообщение, бот должен проверить его сохраненную `serviceUrl` стоимость.</span><span class="sxs-lookup"><span data-stu-id="588db-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="588db-228">Обновление сообщений</span><span class="sxs-lookup"><span data-stu-id="588db-228">Updating messages</span></span>

<span data-ttu-id="588db-229">Вместо того, чтобы ваши сообщения были статическими снимками данных, ваш бот может динамически обновлять сообщения в линии после отправки.</span><span class="sxs-lookup"><span data-stu-id="588db-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="588db-230">Динамические обновления сообщений можно использовать для таких сценариев, как обновление опроса, изменение доступных действий после нажатия кнопки или любое другое изменение асинхронного состояния.</span><span class="sxs-lookup"><span data-stu-id="588db-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="588db-231">Новое сообщение не должно соответствовать исходному типу.</span><span class="sxs-lookup"><span data-stu-id="588db-231">The new message need not match the original in type.</span></span> <span data-ttu-id="588db-232">Например, если исходное сообщение содержало вложение, новое сообщение может быть простым текстовым сообщением.</span><span class="sxs-lookup"><span data-stu-id="588db-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="588db-233">Обновлять можно только содержимое, отправленное в односкладных сообщениях и макетах каруселей.</span><span class="sxs-lookup"><span data-stu-id="588db-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="588db-234">Публикация обновлений сообщений с несколькими вложениями в макете списка не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="588db-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="588db-235">REST API</span><span class="sxs-lookup"><span data-stu-id="588db-235">REST API</span></span>

<span data-ttu-id="588db-236">Чтобы выпустить обновление сообщения, просто выполните запрос PUT против конечной `/v3/conversations/<conversationId>/activities/<activityId>/` точки с помощью данного идентификатора действия.</span><span class="sxs-lookup"><span data-stu-id="588db-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="588db-237">Для завершения этого сценария следует кэшировать идентификатор действия, возвращенный исходным вызовом POST.</span><span class="sxs-lookup"><span data-stu-id="588db-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="588db-238">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="588db-238">.NET example</span></span>

<span data-ttu-id="588db-239">Вы можете использовать `UpdateActivityAsync` этот метод в Bot Builder SDK для обновления существующего сообщения.</span><span class="sxs-lookup"><span data-stu-id="588db-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
  if (activity.Type == ActivityTypes.Message)
  {
    ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
    Activity reply = activity.CreateReply($"You sent {activity.Text} which was {activity.Text.Length} characters");
    var msgToUpdate = await connector.Conversations.ReplyToActivityAsync(reply);
    Activity updatedReply = activity.CreateReply($"This is an updated message");
    await connector.Conversations.UpdateActivityAsync(reply.Conversation.Id, msgToUpdate.Id, updatedReply);
  }
}
```

### <a name="nodejs-example"></a><span data-ttu-id="588db-240">Node.js пример</span><span class="sxs-lookup"><span data-stu-id="588db-240">Node.js example</span></span>

<span data-ttu-id="588db-241">Вы можете использовать `session.connector.update` этот метод в Bot Builder SDK для обновления существующего сообщения.</span><span class="sxs-lookup"><span data-stu-id="588db-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

```javascript
function sendCardUpdate(bot, session, originalMessage, address) {

  var origAttachment = originalMessage.data.attachments[0];
  origAttachment.content.subtitle = 'Assigned to Larry Jin';

  var updatedMsg = new builder.Message()
    .address(address)
    .textFormat(builder.TextFormat.markdown)
    .addAttachment(origAttachment)
    .toMessage();

  session.connector.update(updatedMsg, function(err, addresses) {
    if (err) {
      console.log(`Could not update the message`);
    }
  });
}
```

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="588db-242">Начало разговора (активный обмен сообщениями)</span><span class="sxs-lookup"><span data-stu-id="588db-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="588db-243">Вы можете создать личный разговор с пользователем или начать новую цепочку ответов в канале для вашей команды бота.</span><span class="sxs-lookup"><span data-stu-id="588db-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="588db-244">Это позволяет отправлять сообщения пользователю или пользователям, не имея сначала их инициировать контакт с вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="588db-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="588db-245">Дополнительную информацию см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="588db-245">For more information, see the following topics:</span></span>

<span data-ttu-id="588db-246">Более [подробную информацию о беседах,](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) начатых ботами, можно получить в службах обмена сообщениями Proactive для ботов.</span><span class="sxs-lookup"><span data-stu-id="588db-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="588db-247">Удаление сообщений</span><span class="sxs-lookup"><span data-stu-id="588db-247">Deleting messages</span></span>

<span data-ttu-id="588db-248">Сообщения могут быть удалены с помощью метода [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) разъемов в [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span><span class="sxs-lookup"><span data-stu-id="588db-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

```typescript
bot.dialog('BotDeleteMessage', function (session: builder.Session) {
  var msg = new teams.TeamsMessage(session).text("Bot will delete this message in 5 sec.")
  bot.send(msg, function (err, response) {
    if (err) {
      console.log(err);
      session.endDialog();
    }

    console.log('Proactive message response:');
    console.log(response);
    console.log('---------------------------------------------------')
    setTimeout(function () {
      var activityId: string = null;
      var messageAddress: builder.IChatConnectorAddress = null;
      if (response[0]){
        messageAddress = response[0];
        activityId = messageAddress.id;
      }

      if (activityId == null)
      {
        console.log('Message failed to send.');
        session.endDialog();
        return;
      }

      // Bot delete message
      let address: builder.IChatConnectorAddress  = {
        channelId: 'msteams',
        user: messageAddress.user,
        bot: messageAddress.bot,
        id : activityId,
        serviceUrl : (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
        conversation: {
          id: session.message.address.conversation.id
        }
      };

      connector.delete(address, function (err) {
        if (err)
        {
          console.log(err);
        }
        else
        {
          console.log("Message: " + activityId + " deleted successfully.");
        }

        // Try editing deleted message would fail
        var newMsg = new builder.Message().address(address).text("To edit message.");
        connector.update(newMsg.toMessage(), function (err, address) {
          if (err)
          {
            console.log(err);
            console.log('Deleted message can not be edited.');
          }
          else
          {
            console.log("There is something wrong. Message: " + activityId + " edited successfully.");
            console.log(address);
          }

          session.endDialog();
        });
      });
    }, 5000);
  });
})
```
