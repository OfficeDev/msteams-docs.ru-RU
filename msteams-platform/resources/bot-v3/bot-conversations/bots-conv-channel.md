---
title: Телефонные и групповые беседы чата с ботами
description: Описывает конечный сценарий беседы с ботом в канале в Microsoft Teams
keywords: teams scenarios channels conversation bot
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: e254302271cf101638c897e1a1952d302705d6a4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566798"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="4ec67-104">Беседы в каналах и групповых чатах с ботом Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4ec67-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="4ec67-105">Microsoft Teams позволяет пользователям вводить ботов в свои каналы или групповые беседы в чате.</span><span class="sxs-lookup"><span data-stu-id="4ec67-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="4ec67-106">Добавляя бота в команду или чат, все пользователи беседы могут воспользоваться функциональными возможностями бота прямо во время беседы.</span><span class="sxs-lookup"><span data-stu-id="4ec67-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="4ec67-107">Вы также можете получить доступ Teams в боте, например запрашивать сведения о группе и @mentioning пользователей.</span><span class="sxs-lookup"><span data-stu-id="4ec67-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="4ec67-108">Чат в каналах и групповых чатах отличается от личного чата тем, что пользователю необходимо @mention бота.</span><span class="sxs-lookup"><span data-stu-id="4ec67-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="4ec67-109">Если бот используется в нескольких сферах, таких как личный, групповой или канал, необходимо определить область, из какой области пришли сообщения бота, и обработать их соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="4ec67-109">If a bot is used in multiple scopes such as personal, groupchat, or channel, you need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="4ec67-110">Разработка отличного бота для каналов или групп</span><span class="sxs-lookup"><span data-stu-id="4ec67-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="4ec67-111">Боты, добавленные в команду, становятся другими членами группы и @mentioned быть частью беседы.</span><span class="sxs-lookup"><span data-stu-id="4ec67-111">Bots added to a team become another team member and can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="4ec67-112">Фактически, боты получают сообщения только при @mentioned, поэтому другие беседы на канале не отправляются боту.</span><span class="sxs-lookup"><span data-stu-id="4ec67-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

<span data-ttu-id="4ec67-113">Бот в группе или канале должен предоставлять информацию, соответствующую и соответствующую всем участникам.</span><span class="sxs-lookup"><span data-stu-id="4ec67-113">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="4ec67-114">Хотя ваш бот, безусловно, может предоставить любую информацию, относяную к опыту, имейте в виду, что беседы с ним видны всем.</span><span class="sxs-lookup"><span data-stu-id="4ec67-114">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="4ec67-115">Таким образом, большой бот в группе или канале должен добавить значение для всех пользователей и, конечно, непреднамеренно обмениваться информацией, более подходящей для беседы один к одному.</span><span class="sxs-lookup"><span data-stu-id="4ec67-115">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate to a one-to-one conversation.</span></span>

<span data-ttu-id="4ec67-116">Ваш бот, как и он есть, может быть полностью актуальным во всех сферах без необходимости дополнительной работы.</span><span class="sxs-lookup"><span data-stu-id="4ec67-116">Your bot, just as it is, may be entirely relevant in all scopes without requiring additional work.</span></span> <span data-ttu-id="4ec67-117">В Microsoft Teams не ожидается, что ваш бот будет функционировать во всех сферах, но вы должны убедиться, что ваш бот предоставляет пользователю значение в том, в какой области (ы) вы решите поддерживать.</span><span class="sxs-lookup"><span data-stu-id="4ec67-117">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure that your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="4ec67-118">Дополнительные сведения о области [см.](~/concepts/build-and-test/app-studio-overview.md)в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="4ec67-118">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="4ec67-119">Разработка бота, работающего в группах или каналах, использует те же функции, что и личные беседы.</span><span class="sxs-lookup"><span data-stu-id="4ec67-119">Developing a bot that works in groups or channels uses much of the same functionality as personal conversations.</span></span> <span data-ttu-id="4ec67-120">Дополнительные события и данные в полезной нагрузке предоставляют Teams группы и канала.</span><span class="sxs-lookup"><span data-stu-id="4ec67-120">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="4ec67-121">Эти различия, а также ключевые различия в общих функциональных возможностях описаны в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="4ec67-121">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="4ec67-122">Создание сообщений</span><span class="sxs-lookup"><span data-stu-id="4ec67-122">Creating messages</span></span>

<span data-ttu-id="4ec67-123">Дополнительные сведения о ботах, создающих [](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)сообщения в каналах, см. в дополнительных сведениях проактивное сообщение для ботов и, в [частности, создание беседы на канале.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)</span><span class="sxs-lookup"><span data-stu-id="4ec67-123">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="4ec67-124">Получение сообщений</span><span class="sxs-lookup"><span data-stu-id="4ec67-124">Receiving messages</span></span>

<span data-ttu-id="4ec67-125">Для бота в группе или канале, в дополнение к схеме регулярного [сообщения,](https://docs.botframework.com/core-concepts/reference/#activity)ваш бот также получает следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="4ec67-125">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="4ec67-126">`channelData`См. [Teams каналов](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)данных.</span><span class="sxs-lookup"><span data-stu-id="4ec67-126">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="4ec67-127">В групповом чате содержится информация, специфическая для этого чата.</span><span class="sxs-lookup"><span data-stu-id="4ec67-127">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="4ec67-128">`conversation.id` ID цепочки ответов, состоящий из ИД канала плюс ID первого сообщения в цепочке ответов.</span><span class="sxs-lookup"><span data-stu-id="4ec67-128">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain.</span></span>
* <span data-ttu-id="4ec67-129">`conversation.isGroup` Для `true` бот-сообщений в каналах или групповых чатах.</span><span class="sxs-lookup"><span data-stu-id="4ec67-129">`conversation.isGroup` Is `true` for bot messages in channels or group chats.</span></span>
* <span data-ttu-id="4ec67-130">`conversation.conversationType` Либо `groupChat` или `channel` .</span><span class="sxs-lookup"><span data-stu-id="4ec67-130">`conversation.conversationType` Either `groupChat` or `channel`.</span></span>
* <span data-ttu-id="4ec67-131">`entities` Может содержать одно или несколько упоминаний.</span><span class="sxs-lookup"><span data-stu-id="4ec67-131">`entities` Can contain one or more mentions.</span></span> <span data-ttu-id="4ec67-132">Дополнительные сведения см. в [руберсах Mentions](#-mentions).</span><span class="sxs-lookup"><span data-stu-id="4ec67-132">For more information, see [Mentions](#-mentions).</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="4ec67-133">Ответы на сообщения</span><span class="sxs-lookup"><span data-stu-id="4ec67-133">Replying to messages</span></span>

<span data-ttu-id="4ec67-134">Чтобы ответить на существующее сообщение, [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) позвоните в .NET или [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) в Node.js.</span><span class="sxs-lookup"><span data-stu-id="4ec67-134">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="4ec67-135">SDK Bot Builder обрабатывает все сведения.</span><span class="sxs-lookup"><span data-stu-id="4ec67-135">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="4ec67-136">Если вы решите использовать API REST, вы также можете вызвать [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) конечную точку.</span><span class="sxs-lookup"><span data-stu-id="4ec67-136">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="4ec67-137">В канале, отвечая на сообщение показывает, как ответ на начало цепочки ответов.</span><span class="sxs-lookup"><span data-stu-id="4ec67-137">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="4ec67-138">Содержит `conversation.id` канал и ID сообщения верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="4ec67-138">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="4ec67-139">Несмотря на то, что bot Framework заботится о деталях, можно кэширует эти ответы для будущих ответов на этот поток беседы по `conversation.id` мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="4ec67-139">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="4ec67-140">Best practice: Welcome messages in Teams</span><span class="sxs-lookup"><span data-stu-id="4ec67-140">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="4ec67-141">При первом добавлении бота в группу или группу обычно полезно отправить приветствие, в которое будет вводиться бот всем пользователям.</span><span class="sxs-lookup"><span data-stu-id="4ec67-141">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="4ec67-142">В приветовом сообщении должно быть описано функциональные возможности и преимущества бота.</span><span class="sxs-lookup"><span data-stu-id="4ec67-142">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="4ec67-143">В идеале сообщение должно также включать команды для взаимодействия пользователя с приложением.</span><span class="sxs-lookup"><span data-stu-id="4ec67-143">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="4ec67-144">Для этого убедитесь, что бот отвечает на сообщение `conversationUpdate` с `teamsAddMembers` помощью eventType в `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="4ec67-144">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="4ec67-145">Убедитесь, что ID — это сам app ID бота, так как одно и то же событие отправляется при добавлении `memberAdded` пользователя в команду.</span><span class="sxs-lookup"><span data-stu-id="4ec67-145">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="4ec67-146">Дополнительные [сведения см. в дополнительных сведениях о](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) члене команды или добавлении бота.</span><span class="sxs-lookup"><span data-stu-id="4ec67-146">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="4ec67-147">Кроме того, при добавлении бота может потребоваться отправить личное сообщение каждому члену группы.</span><span class="sxs-lookup"><span data-stu-id="4ec67-147">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="4ec67-148">Для этого можно получить список [команд](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) и отправить каждому пользователю [прямое сообщение.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)</span><span class="sxs-lookup"><span data-stu-id="4ec67-148">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="4ec67-149">Рекомендуется не отправлять *боту* приветствие в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="4ec67-149">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="4ec67-150">Команда большая (очевидно субъективная, например, более 100 участников).</span><span class="sxs-lookup"><span data-stu-id="4ec67-150">The team is big (obviously subjective, for example, more than 100 members).</span></span> <span data-ttu-id="4ec67-151">Ваш бот может рассматриваться как "spammy", а добавленный в него пользователь может получать жалобы, если вы четко не сообщаете всем, кто видит приветствие, о ценности вашего бота.</span><span class="sxs-lookup"><span data-stu-id="4ec67-151">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="4ec67-152">Ваш бот сначала упоминается в группе или канале, а не добавляется в команду.</span><span class="sxs-lookup"><span data-stu-id="4ec67-152">Your bot is first mentioned in a group or channel, versus being first added to a team.</span></span>
* <span data-ttu-id="4ec67-153">Группа или канал переименованы.</span><span class="sxs-lookup"><span data-stu-id="4ec67-153">A group or channel is renamed.</span></span>
* <span data-ttu-id="4ec67-154">Член группы добавляется в группу или канал.</span><span class="sxs-lookup"><span data-stu-id="4ec67-154">A team member is added to a group or channel.</span></span>

## <a name="-mentions"></a><span data-ttu-id="4ec67-155">@ Упоминания</span><span class="sxs-lookup"><span data-stu-id="4ec67-155">@ Mentions</span></span>

<span data-ttu-id="4ec67-156">Так как боты в группе или канале отвечают только тогда, когда они упоминаются ("@_botname")_ в сообщении, каждое сообщение, полученное ботом в групповом канале, содержит свое имя, и необходимо убедиться, что обработка размывов сообщений обрабатывает это.</span><span class="sxs-lookup"><span data-stu-id="4ec67-156">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="4ec67-157">Кроме того, боты могут сравнений между другими пользователями, упомянутыми в сообщениях, и упоминать их в качестве части сообщений.</span><span class="sxs-lookup"><span data-stu-id="4ec67-157">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="4ec67-158">Получение упоминаний</span><span class="sxs-lookup"><span data-stu-id="4ec67-158">Retrieving mentions</span></span>

<span data-ttu-id="4ec67-159">Упоминания возвращаются в объект в полезной нагрузке и содержат как уникальный ID пользователя, так и, в большинстве случаев, имя `entities` упомянутого пользователя.</span><span class="sxs-lookup"><span data-stu-id="4ec67-159">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="4ec67-160">Вы можете получить все упоминания в сообщении, позвонив функции в SDK bot Builder для .NET, которая возвращает `GetMentions` массив `Mentioned` объектов.</span><span class="sxs-lookup"><span data-stu-id="4ec67-160">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="4ec67-161">Код примера .NET: проверка упоминания о @bot и @bot</span><span class="sxs-lookup"><span data-stu-id="4ec67-161">.NET example code: Check for and strip @bot mention</span></span>

```csharp
Mention[] m = sourceMessage.GetMentions();
var messageText = sourceMessage.Text;

for (int i = 0;i < m.Length;i++)
{
    if (m[i].Mentioned.Id == sourceMessage.Recipient.Id)
    {
        //Bot is in the @mention list.
        //The below example will strip the bot name out of the message, so you can parse it as if it wasn't included. Note that the Text object will contain the full bot name, if applicable.
        if (m[i].Text != null)
            messageText = messageText.Replace(m[i].Text, "");
    }
}
```

> [!NOTE]
> <span data-ttu-id="4ec67-162">Вы также можете использовать функцию Teams расширения, которая отключит все упоминания, включая `GetTextWithoutMentions` бот.</span><span class="sxs-lookup"><span data-stu-id="4ec67-162">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="4ec67-163">Node.js пример кода: проверка упоминания о @bot и @bot</span><span class="sxs-lookup"><span data-stu-id="4ec67-163">Node.js example code: Check for and strip @bot mention</span></span>

```javascript
var text = message.text;
if (message.entities) {
    message.entities
        .filter(entity => ((entity.type === "mention") && (entity.mentioned.id.toLowerCase() === botId)))
        .forEach(entity => {
            text = text.replace(entity.text, "");
        });
    text = text.trim();
}
```

<span data-ttu-id="4ec67-164">Вы также можете использовать функцию Teams расширения, которая отключит все упоминания, включая `getTextWithoutMentions` бот.</span><span class="sxs-lookup"><span data-stu-id="4ec67-164">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="4ec67-165">Построение упоминаний</span><span class="sxs-lookup"><span data-stu-id="4ec67-165">Constructing mentions</span></span>

<span data-ttu-id="4ec67-166">Ваш бот может упоминать других пользователей в сообщениях, которые размещены в каналах.</span><span class="sxs-lookup"><span data-stu-id="4ec67-166">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="4ec67-167">Для этого ваше сообщение должно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="4ec67-167">To do this, your message must do the following:</span></span>

* <span data-ttu-id="4ec67-168">`<at>@username</at>`Включаем в текст сообщения.</span><span class="sxs-lookup"><span data-stu-id="4ec67-168">Include `<at>@username</at>` in the message text.</span></span>
* <span data-ttu-id="4ec67-169">`mention`Включи объект в коллекцию сущностями.</span><span class="sxs-lookup"><span data-stu-id="4ec67-169">Include the `mention` object inside the entities collection.</span></span>

#### <a name="net-example"></a><span data-ttu-id="4ec67-170">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="4ec67-170">.NET example</span></span>

<span data-ttu-id="4ec67-171">В этом примере используется [пакет Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.</span><span class="sxs-lookup"><span data-stu-id="4ec67-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="4ec67-172">Node.js пример</span><span class="sxs-lookup"><span data-stu-id="4ec67-172">Node.js example</span></span>

```javascript
// User to mention
var toMention: builder.IIdentity = {
    name: 'John Doe',
    id: userId
};

// Create a message and add mention to it
var msg = new teams.TeamsMessage(session).text(teams.TeamsMessage.getTenantId(session.message));
var mentionedMsg = msg.addMentionToText(toMention);

// Post the message
var generalMessage = mentionedMsg.routeReplyToGeneralChannel();
session.send(generalMessage);
```

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="4ec67-173">Пример. Исходяние сообщения с указанным пользователем</span><span class="sxs-lookup"><span data-stu-id="4ec67-173">Example: Outgoing message with user mentioned</span></span>

```json
{
    "type": "message", 
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "28:9e52142b-5e5e-4d7b-bb3e- e82dcf620000",
        "name": "SchemaTestBot"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="4ec67-174">Доступ к groupChat или области каналов</span><span class="sxs-lookup"><span data-stu-id="4ec67-174">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="4ec67-175">Ваш бот может не только отправлять и получать сообщения в группах и группах.</span><span class="sxs-lookup"><span data-stu-id="4ec67-175">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="4ec67-176">Например, он также может получать список участников, включая сведения о профиле, а также список каналов.</span><span class="sxs-lookup"><span data-stu-id="4ec67-176">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="4ec67-177">Дополнительные сведения см. в [дополнительных сведениях: Получить контекст для Microsoft Teams бота.](~/resources/bot-v3/bots-context.md)</span><span class="sxs-lookup"><span data-stu-id="4ec67-177">For more information, see [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4ec67-178">См. также</span><span class="sxs-lookup"><span data-stu-id="4ec67-178">See also</span></span>

[<span data-ttu-id="4ec67-179">Примеры Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4ec67-179">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
