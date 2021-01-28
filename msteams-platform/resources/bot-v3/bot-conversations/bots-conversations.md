---
title: Отправка и получение сообщений с помощью бота
description: В этой статье описывается, как отправлять и получать сообщения с ботами в Microsoft Teams
ms.topic: overview
keywords: сообщения ботов teams
ms.date: 05/20/2019
ms.openlocfilehash: 20c285a0cd06ac929d628edbc059b2a00b937eec
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014119"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="fb433-104">Общение с ботом Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fb433-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="fb433-105">Беседа — это серия сообщений, отправленных между ботом и одним или более пользователями.</span><span class="sxs-lookup"><span data-stu-id="fb433-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="fb433-106">Существует три типа бесед (также называемых областью) в Teams:</span><span class="sxs-lookup"><span data-stu-id="fb433-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="fb433-107">`teams` Также называется беседами канала, которые видны всем участникам канала.</span><span class="sxs-lookup"><span data-stu-id="fb433-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="fb433-108">`personal` Беседы между ботами и одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="fb433-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="fb433-109">`groupChat` Чат между ботом и двумя или более пользователями.</span><span class="sxs-lookup"><span data-stu-id="fb433-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="fb433-110">Бот ведет себя немного по-разному в зависимости от типа беседы, в которых он участвует:</span><span class="sxs-lookup"><span data-stu-id="fb433-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="fb433-111">[Боты в беседах](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) в канале и групповом чате требуют от пользователя @упоминания бота, чтобы вызвать его в канале.</span><span class="sxs-lookup"><span data-stu-id="fb433-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="fb433-112">[Боты в беседах с одним пользователем](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) не требуют @упоминания — пользователь может просто ввести.</span><span class="sxs-lookup"><span data-stu-id="fb433-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @ mention -  the user can just type.</span></span>

<span data-ttu-id="fb433-113">Чтобы бот работал в определенной области, он должен быть указан как поддерживающие эту область в манифесте.</span><span class="sxs-lookup"><span data-stu-id="fb433-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="fb433-114">Области определяются и обсуждаются далее в справочнике [по манифестам.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="fb433-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="fb433-115">Упреждающие сообщения</span><span class="sxs-lookup"><span data-stu-id="fb433-115">Proactive messages</span></span>

<span data-ttu-id="fb433-116">Боты могут участвовать в беседе или инициировать ее.</span><span class="sxs-lookup"><span data-stu-id="fb433-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="fb433-117">Большая часть сообщений является ответом на другое сообщение.</span><span class="sxs-lookup"><span data-stu-id="fb433-117">Most communication is in response to another message.</span></span> <span data-ttu-id="fb433-118">Если бот инициирует беседу, это называется упреждающего *сообщения.*</span><span class="sxs-lookup"><span data-stu-id="fb433-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="fb433-119">Примеры:</span><span class="sxs-lookup"><span data-stu-id="fb433-119">Examples include:</span></span>

* <span data-ttu-id="fb433-120">Приветствия</span><span class="sxs-lookup"><span data-stu-id="fb433-120">Welcome messages</span></span>
* <span data-ttu-id="fb433-121">Уведомления о событиях</span><span class="sxs-lookup"><span data-stu-id="fb433-121">Event notifications</span></span>
* <span data-ttu-id="fb433-122">Опрос сообщений</span><span class="sxs-lookup"><span data-stu-id="fb433-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="fb433-123">Основы разговора</span><span class="sxs-lookup"><span data-stu-id="fb433-123">Conversation basics</span></span>

<span data-ttu-id="fb433-124">Каждое сообщение является `Activity` объектом типа `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="fb433-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="fb433-125">Когда пользователь отправляет сообщение, Teams отправляет его вашему боту; В частности, он отправляет объект JSON в конечную точку обмена сообщениями бота.</span><span class="sxs-lookup"><span data-stu-id="fb433-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="fb433-126">Бот проверяет сообщение, чтобы определить его тип, и отвечает соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="fb433-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="fb433-127">Боты также поддерживают сообщения в стиле событий.</span><span class="sxs-lookup"><span data-stu-id="fb433-127">Bots also support event-style messages.</span></span> <span data-ttu-id="fb433-128">Дополнительные сведения см. в записи обработки событий ботов [в Microsoft Teams.](~/resources/bot-v3/bots-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="fb433-128">See [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md) for more details.</span></span> <span data-ttu-id="fb433-129">В настоящее время речь не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="fb433-129">Speech is currently not supported.</span></span>

<span data-ttu-id="fb433-130">Сообщения по большей части одинаковы для всех областей, но существуют различия в доступе к боту в пользовательском интерфейсе и различия, о которых вам потребуется знать.</span><span class="sxs-lookup"><span data-stu-id="fb433-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="fb433-131">Базовая беседа обрабатывается через соединители Bot Framework, один API REST, позволяющий боту взаимодействовать с Teams и другими каналами.</span><span class="sxs-lookup"><span data-stu-id="fb433-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="fb433-132">SDK построитель ботов предоставляет простой доступ к этому API, дополнительные функции для управления потоком беседы и состоянием, а также простые способы включения функций распознавания, таких как обработка на естественном языке (NLP).</span><span class="sxs-lookup"><span data-stu-id="fb433-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="fb433-133">Содержимое сообщения</span><span class="sxs-lookup"><span data-stu-id="fb433-133">Message content</span></span>

<span data-ttu-id="fb433-134">Бот может отправлять текст, изображения и карточки.</span><span class="sxs-lookup"><span data-stu-id="fb433-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="fb433-135">Пользователи могут отправлять вашему боту текст и изображения.</span><span class="sxs-lookup"><span data-stu-id="fb433-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="fb433-136">Вы можете указать тип содержимого, которое бот может обрабатывать на странице параметров Microsoft Teams для вашего бота.</span><span class="sxs-lookup"><span data-stu-id="fb433-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="fb433-137">Format</span><span class="sxs-lookup"><span data-stu-id="fb433-137">Format</span></span> | <span data-ttu-id="fb433-138">От пользователя к боту</span><span class="sxs-lookup"><span data-stu-id="fb433-138">From user to bot</span></span>  | <span data-ttu-id="fb433-139">От бота к пользователю</span><span class="sxs-lookup"><span data-stu-id="fb433-139">From bot to user</span></span> |  <span data-ttu-id="fb433-140">Примечания</span><span class="sxs-lookup"><span data-stu-id="fb433-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="fb433-141">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="fb433-141">Rich text</span></span> | <span data-ttu-id="fb433-142">✔</span><span class="sxs-lookup"><span data-stu-id="fb433-142">✔</span></span> | <span data-ttu-id="fb433-143">✔</span><span class="sxs-lookup"><span data-stu-id="fb433-143">✔</span></span> |  |
| <span data-ttu-id="fb433-144">Изображения</span><span class="sxs-lookup"><span data-stu-id="fb433-144">Pictures</span></span> | <span data-ttu-id="fb433-145">✔</span><span class="sxs-lookup"><span data-stu-id="fb433-145">✔</span></span> | <span data-ttu-id="fb433-146">✔</span><span class="sxs-lookup"><span data-stu-id="fb433-146">✔</span></span> | <span data-ttu-id="fb433-147">Не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированное GIF не поддерживается</span><span class="sxs-lookup"><span data-stu-id="fb433-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span> |
| <span data-ttu-id="fb433-148">Карточки</span><span class="sxs-lookup"><span data-stu-id="fb433-148">Cards</span></span> | <span data-ttu-id="fb433-149">✖</span><span class="sxs-lookup"><span data-stu-id="fb433-149">✖</span></span> | <span data-ttu-id="fb433-150">✔</span><span class="sxs-lookup"><span data-stu-id="fb433-150">✔</span></span> | <span data-ttu-id="fb433-151">См. справочник [по карточкам Teams для](~/task-modules-and-cards/cards/cards-reference.md) поддерживаемых карточек</span><span class="sxs-lookup"><span data-stu-id="fb433-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="fb433-152">Эмодзи</span><span class="sxs-lookup"><span data-stu-id="fb433-152">Emojis</span></span> | <span data-ttu-id="fb433-153">✖</span><span class="sxs-lookup"><span data-stu-id="fb433-153">✖</span></span> | <span data-ttu-id="fb433-154">✔</span><span class="sxs-lookup"><span data-stu-id="fb433-154">✔</span></span> | <span data-ttu-id="fb433-155">В настоящее время Teams поддерживает эмодзи через UTF-16 (например, U+1F600 для ухмылки)</span><span class="sxs-lookup"><span data-stu-id="fb433-155">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span> |
|

<span data-ttu-id="fb433-156">Дополнительные сведения о типах взаимодействия ботов, поддерживаемых Bot Framework (на которых основаны [](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) боты в командах), см. в документации Bot Framework о потоке бесед и связанных понятиях в документации для [Bot Builder SDK для .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) и [Bot Builder SDK для Node.js. ](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0)</span><span class="sxs-lookup"><span data-stu-id="fb433-156">For more information on the types of bot interaction supported by the Bot Framework (which bots in teams are based on), see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="fb433-157">Форматирование сообщения</span><span class="sxs-lookup"><span data-stu-id="fb433-157">Message formatting</span></span>

<span data-ttu-id="fb433-158">Вы можете настроить необязательное свойство A для управления отрисовки текстового [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) `message` содержимого сообщения.</span><span class="sxs-lookup"><span data-stu-id="fb433-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="fb433-159">Подробное [описание поддерживаемого форматирования](~/resources/bot-v3/bots-message-format.md) в сообщениях ботов см. в описании форматирования сообщений- ботов.</span><span class="sxs-lookup"><span data-stu-id="fb433-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="fb433-160">Вы можете настроить необязательное [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) свойство, чтобы управлять отрисовка текстового содержимого сообщения.</span><span class="sxs-lookup"><span data-stu-id="fb433-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="fb433-161">Подробные сведения о том, как Teams поддерживает форматирование текста в командах, см. в сообщении [бота.](~/resources/bot-v3/bots-text-formats.md)</span><span class="sxs-lookup"><span data-stu-id="fb433-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="fb433-162">Сведения о форматирования карточек в сообщениях см. в [формате карточки.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="fb433-162">For information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="fb433-163">Сообщения с рисунками</span><span class="sxs-lookup"><span data-stu-id="fb433-163">Picture messages</span></span>

<span data-ttu-id="fb433-164">Изображения отправляются путем добавления вложений в сообщение.</span><span class="sxs-lookup"><span data-stu-id="fb433-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="fb433-165">Дополнительные сведения о вложениях можно найти в [документации Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0)</span><span class="sxs-lookup"><span data-stu-id="fb433-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span></span>

<span data-ttu-id="fb433-166">Изображения могут иметь не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированное GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="fb433-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="fb433-167">Рекомендуется указать высоту и ширину каждого изображения с помощью XML.</span><span class="sxs-lookup"><span data-stu-id="fb433-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="fb433-168">Если вы используете Markdown, размер изображения по умолчанию составляет 256×256.</span><span class="sxs-lookup"><span data-stu-id="fb433-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="fb433-169">Пример:</span><span class="sxs-lookup"><span data-stu-id="fb433-169">For example:</span></span>

* <span data-ttu-id="fb433-170">Воспользуйтесь `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="fb433-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="fb433-171">Не используйте `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="fb433-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages"></a><span data-ttu-id="fb433-172">Получение сообщений</span><span class="sxs-lookup"><span data-stu-id="fb433-172">Receiving messages</span></span>

<span data-ttu-id="fb433-173">В зависимости от объявленных областей бот может получать сообщения в следующих контекстах:</span><span class="sxs-lookup"><span data-stu-id="fb433-173">Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id="fb433-174">**личный чат** Пользователи могут взаимодействовать в частной беседе с ботом, просто выбрав добавленного бота в истории чата или введя его имя или ИД приложения в поле "To:" в новом чате.</span><span class="sxs-lookup"><span data-stu-id="fb433-174">**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id="fb433-175">**Каналы** Бот можно упомянуть ("@_botname")_ в канале, если он был добавлен в команду.</span><span class="sxs-lookup"><span data-stu-id="fb433-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="fb433-176">Обратите внимание, что для дополнительных ответов бота в канале необходимо упомянуть бота.</span><span class="sxs-lookup"><span data-stu-id="fb433-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="fb433-177">Он не будет отвечать на ответы там, где он не упоминается.</span><span class="sxs-lookup"><span data-stu-id="fb433-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="fb433-178">Для входящих сообщений бот получает объект [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) типа `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="fb433-178">For incoming messages, your bot receives an [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) object of type `messageType: message`.</span></span> <span data-ttu-id="fb433-179">Хотя объект может содержать другие типы информации, например обновления каналов, отправленные вашему боту, тип представляет связь между ботом `Activity` и [](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` пользователем.</span><span class="sxs-lookup"><span data-stu-id="fb433-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="fb433-180">Бот получает полезное сообщение пользователя, а также другие сведения о пользователе, источнике сообщения и `Text` сведениях Teams.</span><span class="sxs-lookup"><span data-stu-id="fb433-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="fb433-181">Обратите внимание:</span><span class="sxs-lookup"><span data-stu-id="fb433-181">Of note:</span></span>

* <span data-ttu-id="fb433-182">`timestamp` Дата и время сообщения в универсальном координировании времени (UTC)</span><span class="sxs-lookup"><span data-stu-id="fb433-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC)</span></span>
* <span data-ttu-id="fb433-183">`localTimestamp` Дата и время сообщения в часовом поясе отправитель</span><span class="sxs-lookup"><span data-stu-id="fb433-183">`localTimestamp` The date and time of the message in the time zone of the sender</span></span>
* <span data-ttu-id="fb433-184">`channelId` Всегда "msteams".</span><span class="sxs-lookup"><span data-stu-id="fb433-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="fb433-185">Это относится к каналу bot framework, а не к каналу teams.</span><span class="sxs-lookup"><span data-stu-id="fb433-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="fb433-186">`from.id` Уникальный и зашифрованный код для этого пользователя для вашего бота; подходит в качестве ключа, если приложению необходимо хранить данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="fb433-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="fb433-187">Он уникален для вашего бота и не может непосредственно использоваться за пределами экземпляра бота, чтобы определить этого пользователя</span><span class="sxs-lookup"><span data-stu-id="fb433-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user</span></span>
* <span data-ttu-id="fb433-188">`channelData.tenant.id` ИД клиента для пользователя.</span><span class="sxs-lookup"><span data-stu-id="fb433-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="fb433-189">`from.id` уникален для вашего бота и не может непосредственно использоваться за пределами экземпляра бота для идентификации этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="fb433-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="fb433-190">Сочетание каналов и частных взаимодействий с ботом</span><span class="sxs-lookup"><span data-stu-id="fb433-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="fb433-191">При взаимодействии в канале бот должен быть уверен в том, что некоторые беседы с пользователем будут отключены.</span><span class="sxs-lookup"><span data-stu-id="fb433-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="fb433-192">Например, предположим, что пользователь пытается скоординировать сложную задачу, например планирование с набором участников группы.</span><span class="sxs-lookup"><span data-stu-id="fb433-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="fb433-193">Вместо того, чтобы вся последовательность действий была видна каналу, рассмотрите возможность отправки пользователю личного сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="fb433-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="fb433-194">Бот должен иметь возможность легко перенаупорять пользователя между личными беседами и беседами в каналах, не теряя состояние.</span><span class="sxs-lookup"><span data-stu-id="fb433-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="fb433-195">Не забудьте обновить канал после завершения взаимодействия, чтобы уведомить других участников команды.</span><span class="sxs-lookup"><span data-stu-id="fb433-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="fb433-196">Пример полной схемы входящие</span><span class="sxs-lookup"><span data-stu-id="fb433-196">Full inbound schema example</span></span>

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
> <span data-ttu-id="fb433-197">Текстовое поле для входящие сообщения иногда содержит упоминания.</span><span class="sxs-lookup"><span data-stu-id="fb433-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="fb433-198">Убедитесь, что они правильно проверяются и разостримы.</span><span class="sxs-lookup"><span data-stu-id="fb433-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="fb433-199">Дополнительные сведения см. в [упоминаний.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)</span><span class="sxs-lookup"><span data-stu-id="fb433-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="fb433-200">Данные канала Teams</span><span class="sxs-lookup"><span data-stu-id="fb433-200">Teams channel data</span></span>

<span data-ttu-id="fb433-201">Объект `channelData` содержит сведения, специфичная для Teams, и является окончательным источником для кодов команды и канала.</span><span class="sxs-lookup"><span data-stu-id="fb433-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="fb433-202">Необходимо кэширования и использовать эти ids в качестве ключей для локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="fb433-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="fb433-203">Объект не включается в сообщения в личных беседах, так как они проходят `channelData` за пределами любого канала.</span><span class="sxs-lookup"><span data-stu-id="fb433-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="fb433-204">Типичный объект channelData в действии, отправленный вашему боту, содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="fb433-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="fb433-205">`eventType` Тип события Teams; передается только в случае событий [изменения канала](~/resources/bot-v3/bots-notifications.md#channel-updates)</span><span class="sxs-lookup"><span data-stu-id="fb433-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates)</span></span>
* <span data-ttu-id="fb433-206">`tenant.id` ИД клиента Azure Active Directory; передается во всех контекстах</span><span class="sxs-lookup"><span data-stu-id="fb433-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="fb433-207">`team` Передается только в контекстах канала, а не в личном чате.</span><span class="sxs-lookup"><span data-stu-id="fb433-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="fb433-208">`id` GUID для канала</span><span class="sxs-lookup"><span data-stu-id="fb433-208">`id` GUID for the channel</span></span>
  * <span data-ttu-id="fb433-209">`name` Имя команды; передается только в случаях [переименования команды](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span><span class="sxs-lookup"><span data-stu-id="fb433-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span></span>
* <span data-ttu-id="fb433-210">`channel` Передается только в контекстах канала, когда бот упоминается, или для событий в каналах в командах, в которые был добавлен бот</span><span class="sxs-lookup"><span data-stu-id="fb433-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="fb433-211">`id` GUID для канала</span><span class="sxs-lookup"><span data-stu-id="fb433-211">`id` GUID for the channel</span></span>
  * <span data-ttu-id="fb433-212">`name`Имя канала; передается только в случае событий [изменения канала.](~/resources/bot-v3/bots-notifications.md#channel-updates)</span><span class="sxs-lookup"><span data-stu-id="fb433-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="fb433-213">`channelData.teamsTeamId` Неподготовлено.</span><span class="sxs-lookup"><span data-stu-id="fb433-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="fb433-214">Это свойство включено только для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="fb433-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="fb433-215">`channelData.teamsChannelId` Неподготовлен.</span><span class="sxs-lookup"><span data-stu-id="fb433-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="fb433-216">Это свойство включено только для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="fb433-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="fb433-217">Пример объекта channelData (событие channelCreated)</span><span class="sxs-lookup"><span data-stu-id="fb433-217">Example channelData object (channelCreated event)</span></span>

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

### <a name="net-example"></a><span data-ttu-id="fb433-218">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="fb433-218">.NET example</span></span>

<span data-ttu-id="fb433-219">Пакет [NuGet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) предоставляет специализированный объект, который предоставляет свойства для доступа к сведениям `TeamsChannelData` о Teams.</span><span class="sxs-lookup"><span data-stu-id="fb433-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="fb433-220">Отправка ответов на сообщения</span><span class="sxs-lookup"><span data-stu-id="fb433-220">Sending replies to messages</span></span>

<span data-ttu-id="fb433-221">Чтобы ответить на существующее сообщение, вызовите [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) .NET [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) или Node.js.</span><span class="sxs-lookup"><span data-stu-id="fb433-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) in Node.js.</span></span> <span data-ttu-id="fb433-222">SDK построитель ботов обрабатывает все сведения.</span><span class="sxs-lookup"><span data-stu-id="fb433-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="fb433-223">Если вы решили использовать REST API, можно также вызвать [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) конечную точку.</span><span class="sxs-lookup"><span data-stu-id="fb433-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) endpoint.</span></span>

<span data-ttu-id="fb433-224">Само содержимое сообщения может содержать простой текст или некоторые предоставленные bot Framework карточки [и действия карт.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="fb433-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="fb433-225">Обратите внимание, что в схеме исходящие исходящие должны всегда использовать тот же, `serviceUrl` который вы получили.</span><span class="sxs-lookup"><span data-stu-id="fb433-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="fb433-226">Следует помнить, что значение `serviceUrl` переменной обычно является стабильным, но может меняться.</span><span class="sxs-lookup"><span data-stu-id="fb433-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="fb433-227">Когда приходит новое сообщение, бот должен проверить его сохраненное значение `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="fb433-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="fb433-228">Обновление сообщений</span><span class="sxs-lookup"><span data-stu-id="fb433-228">Updating messages</span></span>

<span data-ttu-id="fb433-229">Вместо того чтобы ваши сообщения были статическими моментальные снимки данных, бот может динамически обновлять сообщения в текстовом режиме после их отправки.</span><span class="sxs-lookup"><span data-stu-id="fb433-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="fb433-230">Динамические обновления сообщений можно использовать для таких сценариев, как обновление опроса, изменение доступных действий после нажатия кнопки или любое другое асинхронное изменение состояния.</span><span class="sxs-lookup"><span data-stu-id="fb433-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="fb433-231">Новое сообщение не соответствует исходному типу.</span><span class="sxs-lookup"><span data-stu-id="fb433-231">The new message need not match the original in type.</span></span> <span data-ttu-id="fb433-232">Например, если исходное сообщение содержало вложение, новое сообщение может быть простым текстовым сообщением.</span><span class="sxs-lookup"><span data-stu-id="fb433-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="fb433-233">Вы можете обновлять только содержимое, отправленное в сообщениях с одним вложением и макетах карусели.</span><span class="sxs-lookup"><span data-stu-id="fb433-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="fb433-234">Публикация обновлений для сообщений с несколькими вложениями в макете списка не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="fb433-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="fb433-235">REST API</span><span class="sxs-lookup"><span data-stu-id="fb433-235">REST API</span></span>

<span data-ttu-id="fb433-236">Чтобы отправить обновление сообщения, просто выполните запрос PUT к конечной точке с использованием `/v3/conversations/<conversationId>/activities/<activityId>/` заданного ИД действия.</span><span class="sxs-lookup"><span data-stu-id="fb433-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="fb433-237">Чтобы завершить этот сценарий, необходимо кэшировали ИД действия, возвращенный исходным вызовом POST.</span><span class="sxs-lookup"><span data-stu-id="fb433-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="fb433-238">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="fb433-238">.NET example</span></span>

<span data-ttu-id="fb433-239">Вы можете использовать метод `UpdateActivityAsync` в SDK bot Builder для обновления существующего сообщения.</span><span class="sxs-lookup"><span data-stu-id="fb433-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

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

### <a name="nodejs-example"></a><span data-ttu-id="fb433-240">Node.js примере</span><span class="sxs-lookup"><span data-stu-id="fb433-240">Node.js example</span></span>

<span data-ttu-id="fb433-241">Вы можете использовать метод `session.connector.update` в SDK построитель ботов для обновления существующего сообщения.</span><span class="sxs-lookup"><span data-stu-id="fb433-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

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

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="fb433-242">Начало беседы (упреждающий обмен сообщениями)</span><span class="sxs-lookup"><span data-stu-id="fb433-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="fb433-243">Вы можете создать личную беседу с пользователем или запустить новую цепочку ответов в канале для бота группы.</span><span class="sxs-lookup"><span data-stu-id="fb433-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="fb433-244">Это позволяет отправлять сообщения пользователям или пользователям, не инициировать контакты с ботом.</span><span class="sxs-lookup"><span data-stu-id="fb433-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="fb433-245">Дополнительную информацию см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="fb433-245">For more information, see the following topics:</span></span>

<span data-ttu-id="fb433-246">Дополнительные [сведения о беседах,](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) запущенных ботами, см. в этой теме.</span><span class="sxs-lookup"><span data-stu-id="fb433-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="fb433-247">Удаление сообщений</span><span class="sxs-lookup"><span data-stu-id="fb433-247">Deleting messages</span></span>

<span data-ttu-id="fb433-248">Сообщения можно удалить с помощью метода [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) соединители в [botBuilder SDK.](/bot-framework/bot-builder-overview-getstarted)</span><span class="sxs-lookup"><span data-stu-id="fb433-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

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
