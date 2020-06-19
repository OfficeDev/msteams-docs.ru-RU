---
title: Отправка и получение сообщений с помощью Bot
description: Сведения о том, как отправлять и получать сообщения с помощью боты в Microsoft Teams
keywords: Боты сообщения Teams
ms.date: 05/20/2019
ms.openlocfilehash: 4a15bb9b4ae8c0ede3214d3a534649e2769baf6e
ms.sourcegitcommit: 2b1fd50466d807869fd173371ba7dfd82a0064ac
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2020
ms.locfileid: "44801509"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="5cc13-104">Беседа с роботом Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5cc13-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="5cc13-105">Беседа — это серия сообщений, отправляемых между Bot и одним или несколькими пользователями.</span><span class="sxs-lookup"><span data-stu-id="5cc13-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="5cc13-106">В Teams существует три вида бесед (также называемых областями):</span><span class="sxs-lookup"><span data-stu-id="5cc13-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="5cc13-107">`teams`Также называется каналы каналов, видимых всем участникам канала.</span><span class="sxs-lookup"><span data-stu-id="5cc13-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="5cc13-108">`personal`Беседы между Боты и одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="5cc13-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="5cc13-109">`groupChat`Чат между Bot и двумя или несколькими пользователями.</span><span class="sxs-lookup"><span data-stu-id="5cc13-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="5cc13-110">В зависимости от типа беседы, в которой она участвует, программа-робота немного ведет себя по-разному.</span><span class="sxs-lookup"><span data-stu-id="5cc13-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="5cc13-111">Для [боты в беседах в канале и группе](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) необходимо, чтобы пользователь "@" привызывал его в канале.</span><span class="sxs-lookup"><span data-stu-id="5cc13-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="5cc13-112">Для [боты в беседах с одним пользователем](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) не требуется @ упоминание, что пользователь может просто ввести.</span><span class="sxs-lookup"><span data-stu-id="5cc13-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @ mention -  the user can just type.</span></span>

<span data-ttu-id="5cc13-113">Чтобы элемент Bot мог работать в определенной области, он должен быть указан в манифесте как поддерживающий эту область в манифесте.</span><span class="sxs-lookup"><span data-stu-id="5cc13-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="5cc13-114">Области определены и обсуждаются в [справочнике по манифесту](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5cc13-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="5cc13-115">Упреждающие сообщения</span><span class="sxs-lookup"><span data-stu-id="5cc13-115">Proactive messages</span></span>

<span data-ttu-id="5cc13-116">Боты могут участвовать в беседе или инициировать ее.</span><span class="sxs-lookup"><span data-stu-id="5cc13-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="5cc13-117">Большая часть обмена сообщениями заключается в ответ на другое сообщение.</span><span class="sxs-lookup"><span data-stu-id="5cc13-117">Most communication is in response to another message.</span></span> <span data-ttu-id="5cc13-118">Если программа-робот инициирует беседу, она называется *упреждающим сообщением*.</span><span class="sxs-lookup"><span data-stu-id="5cc13-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="5cc13-119">Примеры:</span><span class="sxs-lookup"><span data-stu-id="5cc13-119">Examples include:</span></span>

* <span data-ttu-id="5cc13-120">Приветственные сообщения</span><span class="sxs-lookup"><span data-stu-id="5cc13-120">Welcome messages</span></span>
* <span data-ttu-id="5cc13-121">Уведомления о событиях</span><span class="sxs-lookup"><span data-stu-id="5cc13-121">Event notifications</span></span>
* <span data-ttu-id="5cc13-122">Опрос сообщений</span><span class="sxs-lookup"><span data-stu-id="5cc13-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="5cc13-123">Основы разговора</span><span class="sxs-lookup"><span data-stu-id="5cc13-123">Conversation basics</span></span>

<span data-ttu-id="5cc13-124">Каждое сообщение является `Activity` объектом типа `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="5cc13-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="5cc13-125">Когда пользователь отправляет сообщение, Teams отправляет сообщение на сервер почтовых роботов; в частности, он отправляет объект JSON в конечную точку обмена сообщениями ленты.</span><span class="sxs-lookup"><span data-stu-id="5cc13-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="5cc13-126">Ваш почтовый робот просматривает сообщение, чтобы определить его тип и ответить соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="5cc13-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="5cc13-127">Боты также поддерживает сообщения в стиле события.</span><span class="sxs-lookup"><span data-stu-id="5cc13-127">Bots also support event-style messages.</span></span> <span data-ttu-id="5cc13-128">Более подробную информацию можно узнать [в статье обработка событий Bot в Microsoft Teams](~/resources/bot-v3/bots-notifications.md) .</span><span class="sxs-lookup"><span data-stu-id="5cc13-128">See [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md) for more details.</span></span> <span data-ttu-id="5cc13-129">В настоящее время речь не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="5cc13-129">Speech is currently not supported.</span></span>

<span data-ttu-id="5cc13-130">Сообщения для большинства областей имеют одинаковое значение, но существуют различия в доступе к интерфейсу Bot в пользовательском интерфейсе и различиях в сценах, о которых необходимо знать.</span><span class="sxs-lookup"><span data-stu-id="5cc13-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="5cc13-131">Основная беседа обрабатывается через соединитель Bot Framework, один REST API, позволяющий роботам общаться с Teams и другими каналами.</span><span class="sxs-lookup"><span data-stu-id="5cc13-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="5cc13-132">Пакет SDK построителя позволяет легко получить доступ к этому API, дополнительные функции для управления движением и состоянием беседы, а также простые способы внедрения таких служб, как естественный язык (НЛП).</span><span class="sxs-lookup"><span data-stu-id="5cc13-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="5cc13-133">Содержимое сообщения</span><span class="sxs-lookup"><span data-stu-id="5cc13-133">Message content</span></span>

<span data-ttu-id="5cc13-134">Ваш робот может отправлять форматированный текст, изображения и карточки.</span><span class="sxs-lookup"><span data-stu-id="5cc13-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="5cc13-135">Пользователи могут отправлять форматированный текст и изображения в Bot.</span><span class="sxs-lookup"><span data-stu-id="5cc13-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="5cc13-136">Вы можете указать тип контента, который может обработать пользователь Bot, на странице параметров Microsoft Teams для ленты.</span><span class="sxs-lookup"><span data-stu-id="5cc13-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="5cc13-137">Format</span><span class="sxs-lookup"><span data-stu-id="5cc13-137">Format</span></span> | <span data-ttu-id="5cc13-138">От пользователя к Bot</span><span class="sxs-lookup"><span data-stu-id="5cc13-138">From user to bot</span></span>  | <span data-ttu-id="5cc13-139">От Bot к пользователю</span><span class="sxs-lookup"><span data-stu-id="5cc13-139">From bot to user</span></span> |  <span data-ttu-id="5cc13-140">Примечания</span><span class="sxs-lookup"><span data-stu-id="5cc13-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="5cc13-141">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="5cc13-141">Rich text</span></span> | <span data-ttu-id="5cc13-142">✔</span><span class="sxs-lookup"><span data-stu-id="5cc13-142">✔</span></span> | <span data-ttu-id="5cc13-143">✔</span><span class="sxs-lookup"><span data-stu-id="5cc13-143">✔</span></span> |  |
| <span data-ttu-id="5cc13-144">Изображения</span><span class="sxs-lookup"><span data-stu-id="5cc13-144">Pictures</span></span> | <span data-ttu-id="5cc13-145">✔</span><span class="sxs-lookup"><span data-stu-id="5cc13-145">✔</span></span> | <span data-ttu-id="5cc13-146">✔</span><span class="sxs-lookup"><span data-stu-id="5cc13-146">✔</span></span> | <span data-ttu-id="5cc13-147">Не более 1024 × 1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF-файл не поддерживается</span><span class="sxs-lookup"><span data-stu-id="5cc13-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span> |
| <span data-ttu-id="5cc13-148">Карточки</span><span class="sxs-lookup"><span data-stu-id="5cc13-148">Cards</span></span> | <span data-ttu-id="5cc13-149">✖</span><span class="sxs-lookup"><span data-stu-id="5cc13-149">✖</span></span> | <span data-ttu-id="5cc13-150">✔</span><span class="sxs-lookup"><span data-stu-id="5cc13-150">✔</span></span> | <span data-ttu-id="5cc13-151">Поддерживаемые карточки представлены в [справочнике по карточке Teams](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="5cc13-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="5cc13-152">Эмодзи</span><span class="sxs-lookup"><span data-stu-id="5cc13-152">Emojis</span></span> | <span data-ttu-id="5cc13-153">✖</span><span class="sxs-lookup"><span data-stu-id="5cc13-153">✖</span></span> | <span data-ttu-id="5cc13-154">✔</span><span class="sxs-lookup"><span data-stu-id="5cc13-154">✔</span></span> | <span data-ttu-id="5cc13-155">В настоящее время Teams поддерживает эмодзи, используя кодировку UTF-16 (например, U + 1F600 для гриннинг Face)</span><span class="sxs-lookup"><span data-stu-id="5cc13-155">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span> |
|

<span data-ttu-id="5cc13-156">Для получения дополнительных сведений о типах взаимодействий с Bot, поддерживаемых с помощью Bot Framework (которые основаны на Боты в Teams), ознакомьтесь с документацией по [разработке для ленты и](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) связанными понятиями, изложенными в документации по [пакету SDK построителя для .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) и [пакету SDK построителя для Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="5cc13-156">For more information on the types of bot interaction supported by the Bot Framework (which bots in teams are based on), see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="5cc13-157">Форматирование сообщения</span><span class="sxs-lookup"><span data-stu-id="5cc13-157">Message formatting</span></span>

<span data-ttu-id="5cc13-158">Можно задать необязательное [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) свойство элемента, `message` чтобы управлять отображением текстового контента сообщения.</span><span class="sxs-lookup"><span data-stu-id="5cc13-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="5cc13-159">В статье [Форматирование сообщений](~/resources/bot-v3/bots-message-format.md) представлено подробное описание поддерживаемого форматирования в сообщениях Bot.</span><span class="sxs-lookup"><span data-stu-id="5cc13-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="5cc13-160">Можно задать необязательное [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) свойство, чтобы управлять отображением текстового контента сообщения.</span><span class="sxs-lookup"><span data-stu-id="5cc13-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="5cc13-161">Подробные сведения о том, как teams поддерживает форматирование текста в Teams, см [в разделе Форматирование текста в сообщениях Bot](~/resources/bot-v3/bots-text-formats.md).</span><span class="sxs-lookup"><span data-stu-id="5cc13-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="5cc13-162">Сведения о форматировании карточек в сообщениях можно узнать в статье [Форматирование карточки](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="5cc13-162">For information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="5cc13-163">Графические сообщения</span><span class="sxs-lookup"><span data-stu-id="5cc13-163">Picture messages</span></span>

<span data-ttu-id="5cc13-164">Изображения отправляются путем добавления вложений к сообщению.</span><span class="sxs-lookup"><span data-stu-id="5cc13-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="5cc13-165">Дополнительные сведения о вложениях можно найти в [документации по среде Bot](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="5cc13-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span></span>

<span data-ttu-id="5cc13-166">Рисунки могут иметь не более 1024 × 1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF-файл не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="5cc13-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="5cc13-167">Рекомендуем указать высоту и ширину каждого изображения с помощью XML.</span><span class="sxs-lookup"><span data-stu-id="5cc13-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="5cc13-168">Если вы используете Markdown, размер изображения по умолчанию равен 256 × 256.</span><span class="sxs-lookup"><span data-stu-id="5cc13-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="5cc13-169">Например:</span><span class="sxs-lookup"><span data-stu-id="5cc13-169">For example:</span></span>

* <span data-ttu-id="5cc13-170">Используйте`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="5cc13-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="5cc13-171">Не используйте`![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="5cc13-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages"></a><span data-ttu-id="5cc13-172">Получение сообщений</span><span class="sxs-lookup"><span data-stu-id="5cc13-172">Receiving messages</span></span>

<span data-ttu-id="5cc13-173">В зависимости от того, какие области объявляются, Bot может получать сообщения в следующих контекстах:</span><span class="sxs-lookup"><span data-stu-id="5cc13-173">Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id="5cc13-174">**Личный чат** Пользователи могут общаться в частном разговоре с помощью ленты, просто выбрав добавленного элемента Bot в журнале чата или введя его имя или идентификатор приложения в поле Кому: в новом сеансе разговора.</span><span class="sxs-lookup"><span data-stu-id="5cc13-174">**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id="5cc13-175">**Каналы** Вы можете упомянуть в канале ("@_ботнаме_"), если она была добавлена в команду.</span><span class="sxs-lookup"><span data-stu-id="5cc13-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="5cc13-176">Обратите внимание, что для дополнительных ответов на канале Bot в канале требуется упоминание Bot.</span><span class="sxs-lookup"><span data-stu-id="5cc13-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="5cc13-177">Он не реагирует на ответы, где он не упоминается.</span><span class="sxs-lookup"><span data-stu-id="5cc13-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="5cc13-178">Для входящих сообщений Bot получает [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) объект типа `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="5cc13-178">For incoming messages, your bot receives an [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) object of type `messageType: message`.</span></span> <span data-ttu-id="5cc13-179">Несмотря на то `Activity` , что объект может содержать другие типы информации, например [обновления канала](~/resources/bot-v3/bots-notifications.md#channel-updates) , отправляемые в Bot, `message` тип представляет связь между Bot и пользователем.</span><span class="sxs-lookup"><span data-stu-id="5cc13-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="5cc13-180">Ваш Bot получает полезные данные, содержащие сообщение пользователя `Text` , а также другие сведения о пользователе, источник сообщения и сведения о Teams.</span><span class="sxs-lookup"><span data-stu-id="5cc13-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="5cc13-181">Примечание:</span><span class="sxs-lookup"><span data-stu-id="5cc13-181">Of note:</span></span>

* <span data-ttu-id="5cc13-182">`timestamp`Дата и время сообщения в формате всемирного координированного времени (UTC).</span><span class="sxs-lookup"><span data-stu-id="5cc13-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC)</span></span>
* <span data-ttu-id="5cc13-183">`localTimestamp`Дата и время сообщения в часовом поясе отправителя</span><span class="sxs-lookup"><span data-stu-id="5cc13-183">`localTimestamp` The date and time of the message in the time zone of the sender</span></span>
* <span data-ttu-id="5cc13-184">`channelId`Всегда "мстеамс".</span><span class="sxs-lookup"><span data-stu-id="5cc13-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="5cc13-185">Это относится к каналу Bot Framework, а не к каналу Teams.</span><span class="sxs-lookup"><span data-stu-id="5cc13-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="5cc13-186">`from.id`Уникальный и зашифрованный идентификатор пользователя для ленты. подходит в качестве ключа, если ваше приложение должно хранить пользовательские данные.</span><span class="sxs-lookup"><span data-stu-id="5cc13-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="5cc13-187">Он уникален для почтового робота и не может использоваться непосредственно за престоронним экземпляром Bot с помощью какого-либо осмысленного способа идентификации этого пользователя</span><span class="sxs-lookup"><span data-stu-id="5cc13-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user</span></span>
* <span data-ttu-id="5cc13-188">`channelData.tenant.id`Идентификатор клиента для пользователя.</span><span class="sxs-lookup"><span data-stu-id="5cc13-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="5cc13-189">`from.id`является уникальным для почтового робота и не может использоваться непосредственно за престоронним экземпляром Bot с помощью какого-либо осмысленного способа идентификации этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="5cc13-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="5cc13-190">Объединение каналов и частных взаимодействий с Bot</span><span class="sxs-lookup"><span data-stu-id="5cc13-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="5cc13-191">При взаимодействии с каналом Bot должен быть разумным, чтобы принимать определенные беседы в автономном режиме с пользователем.</span><span class="sxs-lookup"><span data-stu-id="5cc13-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="5cc13-192">Например, предположим, что пользователь пытается координировать сложную задачу, например планирование с набором участников группы.</span><span class="sxs-lookup"><span data-stu-id="5cc13-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="5cc13-193">Вместо того чтобы всю последовательность взаимодействий, видимых каналу, рассмотрите возможность отправки пользователю личного сообщения разговора.</span><span class="sxs-lookup"><span data-stu-id="5cc13-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="5cc13-194">Ваш робот должен легко перевести пользователя между личными и каналами бесед без потери состояния.</span><span class="sxs-lookup"><span data-stu-id="5cc13-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="5cc13-195">Не забудьте обновить канал после завершения взаимодействия, чтобы уведомить других участников группы.</span><span class="sxs-lookup"><span data-stu-id="5cc13-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="5cc13-196">Пример полной входящей схемы</span><span class="sxs-lookup"><span data-stu-id="5cc13-196">Full inbound schema example</span></span>

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
> <span data-ttu-id="5cc13-197">Текстовое поле для входящих сообщений иногда содержит упоминания.</span><span class="sxs-lookup"><span data-stu-id="5cc13-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="5cc13-198">Обязательно проверьте и извлеките их.</span><span class="sxs-lookup"><span data-stu-id="5cc13-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="5cc13-199">Дополнительные сведения [см.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)</span><span class="sxs-lookup"><span data-stu-id="5cc13-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="5cc13-200">Данные канала Teams</span><span class="sxs-lookup"><span data-stu-id="5cc13-200">Teams channel data</span></span>

<span data-ttu-id="5cc13-201">`channelData`Объект содержит сведения, зависящие от команды, и является основным источником для идентификаторов команд и каналов.</span><span class="sxs-lookup"><span data-stu-id="5cc13-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="5cc13-202">Вы должны кэшировать и использовать эти идентификаторы в качестве ключей для локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="5cc13-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="5cc13-203">Этот `channelData` объект не включается в сообщения в личных беседах, так как они выполняются вне какого-либо канала.</span><span class="sxs-lookup"><span data-stu-id="5cc13-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="5cc13-204">Типичный объект Чаннелдата в действии, отправляемом на почтовый робот, содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="5cc13-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="5cc13-205">`eventType`Тип события Teams; передается только в случае [событий изменения канала](~/resources/bot-v3/bots-notifications.md#channel-updates)</span><span class="sxs-lookup"><span data-stu-id="5cc13-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates)</span></span>
* <span data-ttu-id="5cc13-206">`tenant.id`Идентификатор клиента Azure Active Directory; передается во всех контекстах</span><span class="sxs-lookup"><span data-stu-id="5cc13-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="5cc13-207">`team`Передается только в контекстах канала, а не в личном сеансе чата.</span><span class="sxs-lookup"><span data-stu-id="5cc13-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="5cc13-208">`id`GUID для канала</span><span class="sxs-lookup"><span data-stu-id="5cc13-208">`id` GUID for the channel</span></span>
  * <span data-ttu-id="5cc13-209">`name`Имя команды; передается только в случае [событий переименования команды](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span><span class="sxs-lookup"><span data-stu-id="5cc13-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span></span>
* <span data-ttu-id="5cc13-210">`channel`Передается только в контекстах канала при упоминании Bot или для событий в каналах в Microsoft Teams, где добавлен Bot</span><span class="sxs-lookup"><span data-stu-id="5cc13-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="5cc13-211">`id`GUID для канала</span><span class="sxs-lookup"><span data-stu-id="5cc13-211">`id` GUID for the channel</span></span>
  * <span data-ttu-id="5cc13-212">`name`Имя канала; передается только в случае [событий изменения канала](~/resources/bot-v3/bots-notifications.md#channel-updates).</span><span class="sxs-lookup"><span data-stu-id="5cc13-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="5cc13-213">`channelData.teamsTeamId`Устаревшие.</span><span class="sxs-lookup"><span data-stu-id="5cc13-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="5cc13-214">Это свойство включено только для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="5cc13-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="5cc13-215">`channelData.teamsChannelId`Устаревшие.</span><span class="sxs-lookup"><span data-stu-id="5cc13-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="5cc13-216">Это свойство включено только для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="5cc13-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="5cc13-217">Пример объекта Чаннелдата (событие Чаннелкреатед)</span><span class="sxs-lookup"><span data-stu-id="5cc13-217">Example channelData object (channelCreated event)</span></span>

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

### <a name="net-example"></a><span data-ttu-id="5cc13-218">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="5cc13-218">.NET example</span></span>

<span data-ttu-id="5cc13-219">Пакет NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) предоставляет специализированный `TeamsChannelData` объект, который предоставляет свойства для доступа к сведениям, относящимся к Teams.</span><span class="sxs-lookup"><span data-stu-id="5cc13-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="5cc13-220">Отправка ответов на сообщения</span><span class="sxs-lookup"><span data-stu-id="5cc13-220">Sending replies to messages</span></span>

<span data-ttu-id="5cc13-221">Чтобы ответить на существующее сообщение, звоните [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) в .NET или [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) в Node.js.</span><span class="sxs-lookup"><span data-stu-id="5cc13-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) in Node.js.</span></span> <span data-ttu-id="5cc13-222">Пакет SDK построителя построителя обрабатывает все подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="5cc13-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="5cc13-223">Если вы решили использовать REST API, вы также можете вызвать [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) конечную точку.</span><span class="sxs-lookup"><span data-stu-id="5cc13-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) endpoint.</span></span>

<span data-ttu-id="5cc13-224">Само содержимое сообщения может содержать простой текст или некоторые [карточки и действия карточки с](~/task-modules-and-cards/cards/cards-actions.md)Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="5cc13-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="5cc13-225">Обратите внимание, что в используемой схеме исходящей почты следует всегда использовать ту же информацию, что и `serviceUrl` в полученном виде.</span><span class="sxs-lookup"><span data-stu-id="5cc13-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="5cc13-226">Имейте в виду, что значение `serviceUrl` является стабильным, но может измениться.</span><span class="sxs-lookup"><span data-stu-id="5cc13-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="5cc13-227">Когда поступает новое сообщение, ваш робот должен проверить сохраненное значение `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="5cc13-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="5cc13-228">Обновление сообщений</span><span class="sxs-lookup"><span data-stu-id="5cc13-228">Updating messages</span></span>

<span data-ttu-id="5cc13-229">Вместо того чтобы сообщения были статическими моментальными снимками данных, ваш Bot может динамически обновлять сообщения после отправки.</span><span class="sxs-lookup"><span data-stu-id="5cc13-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="5cc13-230">Динамическое обновление сообщений можно использовать для таких сценариев, как обновление опросов, изменение доступных действий после нажатия кнопки или любое другое изменение асинхронного состояния.</span><span class="sxs-lookup"><span data-stu-id="5cc13-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="5cc13-231">Новое сообщение не должно быть соответствующим исходному типу.</span><span class="sxs-lookup"><span data-stu-id="5cc13-231">The new message need not match the original in type.</span></span> <span data-ttu-id="5cc13-232">Например, если исходное сообщение содержит вложение, новое сообщение может быть простым текстовым сообщением.</span><span class="sxs-lookup"><span data-stu-id="5cc13-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="5cc13-233">Вы можете обновить только содержимое, отправленное в сообщениях с одним вложением и в виде схем обоймы.</span><span class="sxs-lookup"><span data-stu-id="5cc13-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="5cc13-234">Публикация обновлений сообщений с несколькими вложениями в раскладке списков не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="5cc13-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="5cc13-235">REST API</span><span class="sxs-lookup"><span data-stu-id="5cc13-235">REST API</span></span>

<span data-ttu-id="5cc13-236">Чтобы отправить сообщение об обновлении, просто выполните запрос PUT для `/v3/conversations/<conversationId>/activities/<activityId>/` конечной точки, используя заданный идентификатор действия.</span><span class="sxs-lookup"><span data-stu-id="5cc13-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="5cc13-237">Для выполнения этого сценария необходимо кэшировать идентификатор действия, возвращенный исходным вызовом POST.</span><span class="sxs-lookup"><span data-stu-id="5cc13-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="5cc13-238">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="5cc13-238">.NET example</span></span>

<span data-ttu-id="5cc13-239">`UpdateActivityAsync`С помощью метода в пакете SDK построителя построителя можно обновить существующее сообщение.</span><span class="sxs-lookup"><span data-stu-id="5cc13-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

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

### <a name="nodejs-example"></a><span data-ttu-id="5cc13-240">Пример Node.js</span><span class="sxs-lookup"><span data-stu-id="5cc13-240">Node.js example</span></span>

<span data-ttu-id="5cc13-241">`session.connector.update`С помощью метода в пакете SDK построителя построителя можно обновить существующее сообщение.</span><span class="sxs-lookup"><span data-stu-id="5cc13-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

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

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="5cc13-242">Начало беседы (упреждающий обмен сообщениями)</span><span class="sxs-lookup"><span data-stu-id="5cc13-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="5cc13-243">Вы можете создать личный разговор с пользователем или начать новую цепочку ответа в канале для командного канала.</span><span class="sxs-lookup"><span data-stu-id="5cc13-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="5cc13-244">Это позволяет отправлять сообщения пользователям и пользователям, не прибегая к ним, прежде чем приступить к работе с роботом.</span><span class="sxs-lookup"><span data-stu-id="5cc13-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="5cc13-245">Дополнительную информацию см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="5cc13-245">For more information, see the following topics:</span></span>

<span data-ttu-id="5cc13-246">В этой статье приведены сведения об [активных сообщениях для Боты](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) для получения общих сведений о беседах, запущенных Боты.</span><span class="sxs-lookup"><span data-stu-id="5cc13-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="5cc13-247">Удаление сообщений</span><span class="sxs-lookup"><span data-stu-id="5cc13-247">Deleting messages</span></span>

<span data-ttu-id="5cc13-248">Сообщения можно удалять с помощью метода Connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) в [ботбуилдер SDK](/bot-framework/bot-builder-overview-getstarted).</span><span class="sxs-lookup"><span data-stu-id="5cc13-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

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
