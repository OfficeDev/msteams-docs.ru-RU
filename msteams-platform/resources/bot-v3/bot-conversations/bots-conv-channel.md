---
title: Телефонные и групповые беседы чата с ботами
description: Описывает конечный сценарий беседы с ботом в канале в Microsoft Teams
keywords: teams scenarios channels conversation bot
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: be4610f45ab5891edcc6a9683ec994d2ba5c505c
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696180"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="14cb8-104">Беседы в каналах и групповых чатах с ботом Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="14cb8-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="14cb8-105">Microsoft Teams позволяет пользователям вводить ботов в свои каналы или групповые беседы в чате.</span><span class="sxs-lookup"><span data-stu-id="14cb8-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="14cb8-106">Добавляя бота в команду или чат, все пользователи беседы могут воспользоваться функциональными возможностями бота прямо во время беседы.</span><span class="sxs-lookup"><span data-stu-id="14cb8-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="14cb8-107">Кроме того, вы можете получить доступ к функциональным возможностям teams в боте, например запрашивать сведения о группе и @mentioning пользователей.</span><span class="sxs-lookup"><span data-stu-id="14cb8-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="14cb8-108">Чат в каналах и групповых чатах отличается от личного чата тем, что пользователю необходимо @mention бота.</span><span class="sxs-lookup"><span data-stu-id="14cb8-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="14cb8-109">Если бот используется в нескольких сферах (личный, групповой или канал), необходимо определить область, из какой области пришли сообщения бота, и обработать их соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="14cb8-109">If a bot is used in multiple scopes (personal, groupchat or channel) you will need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="14cb8-110">Разработка отличного бота для каналов или групп</span><span class="sxs-lookup"><span data-stu-id="14cb8-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="14cb8-111">Боты, добавленные в команду, становятся другими членами группы и @mentioned быть частью беседы.</span><span class="sxs-lookup"><span data-stu-id="14cb8-111">Bots added to a team become another team member and can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="14cb8-112">Фактически, боты получают сообщения только при @mentioned, поэтому другие беседы на канале не отправляются боту.</span><span class="sxs-lookup"><span data-stu-id="14cb8-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

<span data-ttu-id="14cb8-113">Бот в группе или канале должен предоставлять информацию, соответствующую и соответствующую всем участникам.</span><span class="sxs-lookup"><span data-stu-id="14cb8-113">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="14cb8-114">Хотя ваш бот, безусловно, может предоставить любую информацию, относяную к опыту, имейте в виду, что беседы с ним видны всем.</span><span class="sxs-lookup"><span data-stu-id="14cb8-114">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="14cb8-115">Таким образом, большой бот в группе или канале должен добавить значение для всех пользователей и, конечно, непреднамеренно обмениваться информацией, более подходящей для беседы один к одному.</span><span class="sxs-lookup"><span data-stu-id="14cb8-115">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate to a one-to-one conversation.</span></span>

<span data-ttu-id="14cb8-116">Ваш бот, как и он есть, может быть полностью актуальным во всех сферах без необходимости дополнительной работы.</span><span class="sxs-lookup"><span data-stu-id="14cb8-116">Your bot, just as it is, may be entirely relevant in all scopes without requiring additional work.</span></span> <span data-ttu-id="14cb8-117">В Microsoft Teams не ожидается, что ваш бот будет функционировать во всех сферах, но вы должны убедиться, что ваш бот предоставляет пользователю значение в том, в какой области (s) вы решите поддерживать.</span><span class="sxs-lookup"><span data-stu-id="14cb8-117">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure that your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="14cb8-118">Дополнительные сведения о области см. в [руб. Приложения в Microsoft Teams.](~/concepts/build-and-test/app-studio-overview.md)</span><span class="sxs-lookup"><span data-stu-id="14cb8-118">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="14cb8-119">Разработка бота, работающего в группах или каналах, использует те же функции, что и личные беседы.</span><span class="sxs-lookup"><span data-stu-id="14cb8-119">Developing a bot that works in groups or channels uses much of the same functionality as personal conversations.</span></span> <span data-ttu-id="14cb8-120">Дополнительные события и данные в полезной нагрузке предоставляют сведения о группах и каналах Teams.</span><span class="sxs-lookup"><span data-stu-id="14cb8-120">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="14cb8-121">Эти различия, а также ключевые различия в общих функциональных возможностях описаны в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="14cb8-121">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="14cb8-122">Создание сообщений</span><span class="sxs-lookup"><span data-stu-id="14cb8-122">Creating messages</span></span>

<span data-ttu-id="14cb8-123">Дополнительные сведения о ботах, создающих [](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)сообщения в каналах, см. в дополнительных сведениях проактивное сообщение для ботов и, в [частности, создание беседы на канале.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)</span><span class="sxs-lookup"><span data-stu-id="14cb8-123">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="14cb8-124">Получение сообщений</span><span class="sxs-lookup"><span data-stu-id="14cb8-124">Receiving messages</span></span>

<span data-ttu-id="14cb8-125">Для бота в группе или канале, в дополнение к схеме регулярного [сообщения,](https://docs.botframework.com/core-concepts/reference/#activity)ваш бот также получает следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="14cb8-125">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="14cb8-126">`channelData`См. [данные канала Teams.](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)</span><span class="sxs-lookup"><span data-stu-id="14cb8-126">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="14cb8-127">В групповом чате содержится информация, специфическая для этого чата.</span><span class="sxs-lookup"><span data-stu-id="14cb8-127">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="14cb8-128">`conversation.id` ID цепочки ответов, состоящий из ИД канала плюс ID первого сообщения в цепочке ответов</span><span class="sxs-lookup"><span data-stu-id="14cb8-128">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain</span></span>
* <span data-ttu-id="14cb8-129">`conversation.isGroup` Для `true` бот-сообщений в каналах или групповых чатах</span><span class="sxs-lookup"><span data-stu-id="14cb8-129">`conversation.isGroup` Is `true` for bot messages in channels or group chats</span></span>
* <span data-ttu-id="14cb8-130">`conversation.conversationType` Либо, `groupChat` либо `channel`</span><span class="sxs-lookup"><span data-stu-id="14cb8-130">`conversation.conversationType` Either `groupChat` or `channel`</span></span>
* <span data-ttu-id="14cb8-131">`entities`Может содержать одно или несколько упоминаний (см. [упоминания)](#-mentions)</span><span class="sxs-lookup"><span data-stu-id="14cb8-131">`entities` Can contain one or more mentions (see [Mentions](#-mentions))</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="14cb8-132">Ответы на сообщения</span><span class="sxs-lookup"><span data-stu-id="14cb8-132">Replying to messages</span></span>

<span data-ttu-id="14cb8-133">Чтобы ответить на существующее сообщение, [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) позвоните в .NET или [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) в Node.js.</span><span class="sxs-lookup"><span data-stu-id="14cb8-133">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="14cb8-134">SDK Bot Builder обрабатывает все сведения.</span><span class="sxs-lookup"><span data-stu-id="14cb8-134">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="14cb8-135">Если вы решите использовать API REST, вы также можете вызвать [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) конечную точку.</span><span class="sxs-lookup"><span data-stu-id="14cb8-135">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="14cb8-136">В канале, отвечая на сообщение показывает, как ответ на начало цепочки ответов.</span><span class="sxs-lookup"><span data-stu-id="14cb8-136">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="14cb8-137">Содержит `conversation.id` канал и ID сообщения верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="14cb8-137">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="14cb8-138">Несмотря на то, что bot Framework заботится о деталях, можно кэширует эти ответы для будущих ответов на этот поток беседы по `conversation.id` мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="14cb8-138">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="14cb8-139">Best practice: Welcome messages in Teams</span><span class="sxs-lookup"><span data-stu-id="14cb8-139">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="14cb8-140">При первом добавлении бота в группу или группу обычно полезно отправить приветствие, в которое будет вводиться бот всем пользователям.</span><span class="sxs-lookup"><span data-stu-id="14cb8-140">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="14cb8-141">В приветовом сообщении должно быть описано функциональные возможности и преимущества бота.</span><span class="sxs-lookup"><span data-stu-id="14cb8-141">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="14cb8-142">В идеале сообщение должно также включать команды для взаимодействия пользователя с приложением.</span><span class="sxs-lookup"><span data-stu-id="14cb8-142">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="14cb8-143">Для этого убедитесь, что бот отвечает на сообщение `conversationUpdate` с `teamsAddMembers` помощью eventType в `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="14cb8-143">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="14cb8-144">Убедитесь, что ID — это сам app ID бота, так как одно и то же событие отправляется при добавлении `memberAdded` пользователя в команду.</span><span class="sxs-lookup"><span data-stu-id="14cb8-144">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="14cb8-145">Дополнительные [сведения см. в дополнительных сведениях о](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) члене команды или добавлении бота.</span><span class="sxs-lookup"><span data-stu-id="14cb8-145">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="14cb8-146">Кроме того, при добавлении бота может потребоваться отправить личное сообщение каждому члену группы.</span><span class="sxs-lookup"><span data-stu-id="14cb8-146">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="14cb8-147">Для этого можно получить список [команд](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) и отправить каждому пользователю [прямое сообщение.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)</span><span class="sxs-lookup"><span data-stu-id="14cb8-147">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="14cb8-148">Рекомендуется не отправлять *боту* приветствие в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="14cb8-148">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="14cb8-149">Группа большая (очевидно субъективная, но, например, более 100 участников).</span><span class="sxs-lookup"><span data-stu-id="14cb8-149">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="14cb8-150">Ваш бот может рассматриваться как "spammy", а добавленный в него пользователь может получать жалобы, если вы четко не сообщаете всем, кто видит приветствие, о ценности вашего бота.</span><span class="sxs-lookup"><span data-stu-id="14cb8-150">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="14cb8-151">Ваш бот впервые упоминается в группе или канале (по сравнению с первым добавлением в команду)</span><span class="sxs-lookup"><span data-stu-id="14cb8-151">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="14cb8-152">Группа или канал переименованы</span><span class="sxs-lookup"><span data-stu-id="14cb8-152">A group or channel is renamed</span></span>
* <span data-ttu-id="14cb8-153">Член группы добавляется в группу или канал</span><span class="sxs-lookup"><span data-stu-id="14cb8-153">A team member is added to a group or channel</span></span>

## <a name="-mentions"></a><span data-ttu-id="14cb8-154">@ Упоминания</span><span class="sxs-lookup"><span data-stu-id="14cb8-154">@ Mentions</span></span>

<span data-ttu-id="14cb8-155">Так как боты в группе или канале отвечают только тогда, когда они упоминаются ("@_botname")_ в сообщении, каждое сообщение, полученное ботом в групповом канале, содержит свое имя, и необходимо убедиться, что обработка размывов сообщений обрабатывает это.</span><span class="sxs-lookup"><span data-stu-id="14cb8-155">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="14cb8-156">Кроме того, боты могут сравнений между другими пользователями, упомянутыми в сообщениях, и упоминать их в качестве части сообщений.</span><span class="sxs-lookup"><span data-stu-id="14cb8-156">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="14cb8-157">Получение упоминаний</span><span class="sxs-lookup"><span data-stu-id="14cb8-157">Retrieving mentions</span></span>

<span data-ttu-id="14cb8-158">Упоминания возвращаются в объект в полезной нагрузке и содержат как уникальный ID пользователя, так и, в большинстве случаев, имя `entities` упомянутого пользователя.</span><span class="sxs-lookup"><span data-stu-id="14cb8-158">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="14cb8-159">Вы можете получить все упоминания в сообщении, позвонив функции в SDK bot Builder для .NET, которая возвращает `GetMentions` массив `Mentioned` объектов.</span><span class="sxs-lookup"><span data-stu-id="14cb8-159">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="14cb8-160">Код примера .NET: проверка упоминания о @bot и @bot</span><span class="sxs-lookup"><span data-stu-id="14cb8-160">.NET example code: Check for and strip @bot mention</span></span>

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
> <span data-ttu-id="14cb8-161">Вы также можете использовать функцию расширения Teams, которая отключит все упоминания, включая `GetTextWithoutMentions` бот.</span><span class="sxs-lookup"><span data-stu-id="14cb8-161">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="14cb8-162">Node.js пример кода: проверка упоминания о @bot и @bot</span><span class="sxs-lookup"><span data-stu-id="14cb8-162">Node.js example code: Check for and strip @bot mention</span></span>

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

<span data-ttu-id="14cb8-163">Вы также можете использовать функцию расширения Teams, которая отключит все упоминания, включая `getTextWithoutMentions` бот.</span><span class="sxs-lookup"><span data-stu-id="14cb8-163">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="14cb8-164">Построение упоминаний</span><span class="sxs-lookup"><span data-stu-id="14cb8-164">Constructing mentions</span></span>

<span data-ttu-id="14cb8-165">Ваш бот может упоминать других пользователей в сообщениях, которые размещены в каналах.</span><span class="sxs-lookup"><span data-stu-id="14cb8-165">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="14cb8-166">Для этого ваше сообщение должно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="14cb8-166">To do this, your message must do the following:</span></span>

* <span data-ttu-id="14cb8-167">Включить `<at>@username</at>` в текст сообщения</span><span class="sxs-lookup"><span data-stu-id="14cb8-167">Include `<at>@username</at>` in the message text</span></span>
* <span data-ttu-id="14cb8-168">`mention`Включив объект в коллекцию сущностями</span><span class="sxs-lookup"><span data-stu-id="14cb8-168">Include the `mention` object inside the entities collection</span></span>

#### <a name="net-example"></a><span data-ttu-id="14cb8-169">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="14cb8-169">.NET example</span></span>

<span data-ttu-id="14cb8-170">В этом примере используется [пакет Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.</span><span class="sxs-lookup"><span data-stu-id="14cb8-170">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="14cb8-171">Node.js пример</span><span class="sxs-lookup"><span data-stu-id="14cb8-171">Node.js example</span></span>

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

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="14cb8-172">Пример. Исходяние сообщения с указанным пользователем</span><span class="sxs-lookup"><span data-stu-id="14cb8-172">Example: Outgoing message with user mentioned</span></span>

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

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="14cb8-173">Доступ к groupChat или области каналов</span><span class="sxs-lookup"><span data-stu-id="14cb8-173">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="14cb8-174">Ваш бот может не только отправлять и получать сообщения в группах и группах.</span><span class="sxs-lookup"><span data-stu-id="14cb8-174">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="14cb8-175">Например, он также может получать список участников, включая сведения о профиле, а также список каналов.</span><span class="sxs-lookup"><span data-stu-id="14cb8-175">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="14cb8-176">Дополнительные [дополнительные уроки см. в дополнительных подробной информации о](~/resources/bot-v3/bots-context.md) контексте для бота Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="14cb8-176">See [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md) to learn more.</span></span>

<span data-ttu-id="14cb8-177">*См. также* [примеры Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="14cb8-177">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
