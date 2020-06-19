---
title: Беседы в каналах и группах для общения с Боты
description: Описывает сквозной сценарий, в котором беседа с Bot в канале в Microsoft Teams
keywords: сценарии команд каналы ленты
ms.date: 06/25/2019
ms.openlocfilehash: d2d72bdba43de6ebb10c7504dd309459cb09d56c
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801281"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="78e73-104">Беседы в каналах и группах для общения с помощью робота Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="78e73-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="78e73-105">Microsoft Teams позволяет пользователям перенести боты в беседы по каналам или группового чата.</span><span class="sxs-lookup"><span data-stu-id="78e73-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="78e73-106">Добавляя робота в группу или чат, все пользователи беседы могут воспользоваться всеми преимуществами функции Bot в беседе.</span><span class="sxs-lookup"><span data-stu-id="78e73-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="78e73-107">Вы также можете получать доступ к функциям, зависящим от Teams, в вашей почтовой среде, запрашивают сведения о команде и @mentioning пользователей.</span><span class="sxs-lookup"><span data-stu-id="78e73-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="78e73-108">Чат в каналах и беседах групп отличается от личного разговора тем, что пользователь должен @mention Bot.</span><span class="sxs-lookup"><span data-stu-id="78e73-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="78e73-109">Если используется в нескольких областях (личное, groupchat или Channel), необходимо определить область, из которой поступило сообщение Bot, и обработать их соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="78e73-109">If a bot is used in multiple scopes (personal, groupchat or channel) you will need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="78e73-110">Разработка отличного канала Bot для каналов или групп</span><span class="sxs-lookup"><span data-stu-id="78e73-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="78e73-111">Боты, добавленный в команду, становится другим участником группы, который может быть @mentioned в составе беседы.</span><span class="sxs-lookup"><span data-stu-id="78e73-111">Bots added to a team become another team member, who can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="78e73-112">На самом деле Боты получают сообщения только при @mentioned, поэтому другие беседы по каналу не отправляются в Bot.</span><span class="sxs-lookup"><span data-stu-id="78e73-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="78e73-113">Для удобства при ответе на сообщения Bot в канале имя Bot добавляется в поле создать сообщение автоматически.</span><span class="sxs-lookup"><span data-stu-id="78e73-113">For convenience when replying to bot messages in a channel, the bot name is prepended in the compose message box automatically.</span></span>

<span data-ttu-id="78e73-114">В группе или канале Bot должна предоставляться информация, соответствующая всем участникам.</span><span class="sxs-lookup"><span data-stu-id="78e73-114">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="78e73-115">В то время как ваш Bot может предоставить любую информацию, относящуюся к опыту, следует учитывать, что беседы видны всем пользователям.</span><span class="sxs-lookup"><span data-stu-id="78e73-115">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="78e73-116">Таким образом, с помощью удобного обмена сведениями в группе или канале может быть достаточно добавить значение ко всем пользователям и, безусловно, непреднамеренно использовать информацию в беседе "один к одному".</span><span class="sxs-lookup"><span data-stu-id="78e73-116">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate in a one-to-one conversation.</span></span>

<span data-ttu-id="78e73-117">Ваш робот может быть полностью связан со всеми областями как есть, и не требуется значительных дополнительных действий, чтобы ваш робот мог работать над ними.</span><span class="sxs-lookup"><span data-stu-id="78e73-117">Your bot might be entirely relevant in all scopes as is, and no significant extra work is required to allow your bot to work across them.</span></span> <span data-ttu-id="78e73-118">В Microsoft Teams не предполагается, что функция Bot во всех областях, но вы должны убедиться, что у ленты есть пользовательское значение в любой области, которую вы выбрали для поддержки.</span><span class="sxs-lookup"><span data-stu-id="78e73-118">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="78e73-119">Для получения дополнительных сведений об областях обратитесь к разделу [приложения в Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78e73-119">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="78e73-120">Разработка ленты, которая работает в группах или каналах, использует многие функции личных бесед.</span><span class="sxs-lookup"><span data-stu-id="78e73-120">Developing a bot that works in groups or channels uses much of the same functionality from personal conversations.</span></span> <span data-ttu-id="78e73-121">Дополнительные события и данные в полезных данных содержат сведения о группах и каналах Teams.</span><span class="sxs-lookup"><span data-stu-id="78e73-121">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="78e73-122">Эти отличия, а также ключевые отличия в общих функциональных возможностях описаны в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="78e73-122">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="78e73-123">Создание сообщений</span><span class="sxs-lookup"><span data-stu-id="78e73-123">Creating messages</span></span>

<span data-ttu-id="78e73-124">Дополнительные сведения о Боты создании сообщений в каналах см в статье [Active Messaging for Боты](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)и специальном [создании беседы с каналом](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span><span class="sxs-lookup"><span data-stu-id="78e73-124">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="78e73-125">Получение сообщений</span><span class="sxs-lookup"><span data-stu-id="78e73-125">Receiving messages</span></span>

<span data-ttu-id="78e73-126">В дополнение к [схеме обычных сообщений](https://docs.botframework.com/core-concepts/reference/#activity)для Bot в группе или канале Bot также получают следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="78e73-126">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="78e73-127">`channelData`Ознакомьтесь с [данными канала Teams](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span><span class="sxs-lookup"><span data-stu-id="78e73-127">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="78e73-128">В сеансе групповой беседы содержит сведения, относящиеся к этому разговору.</span><span class="sxs-lookup"><span data-stu-id="78e73-128">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="78e73-129">`conversation.id`ИДЕНТИФИКАТОР цепочки ответа, состоящий из идентификатора канала и идентификатора первого сообщения в цепочке ответа.</span><span class="sxs-lookup"><span data-stu-id="78e73-129">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain</span></span>
* <span data-ttu-id="78e73-130">`conversation.isGroup`Предназначено `true` для сообщений Bot в каналах или групповых беседах</span><span class="sxs-lookup"><span data-stu-id="78e73-130">`conversation.isGroup` Is `true` for bot messages in channels or group chats</span></span>
* <span data-ttu-id="78e73-131">`conversation.conversationType`Один `groupChat` или`channel`</span><span class="sxs-lookup"><span data-stu-id="78e73-131">`conversation.conversationType` Either `groupChat` or `channel`</span></span>
* <span data-ttu-id="78e73-132">`entities`Может содержать одно или несколько упоминаний (см. [упоминание](#-mentions))</span><span class="sxs-lookup"><span data-stu-id="78e73-132">`entities` Can contain one or more mentions (see [Mentions](#-mentions))</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="78e73-133">Ответ на сообщения</span><span class="sxs-lookup"><span data-stu-id="78e73-133">Replying to messages</span></span>

<span data-ttu-id="78e73-134">Чтобы ответить на существующее сообщение, звоните [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) в .NET или [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) в Node.js.</span><span class="sxs-lookup"><span data-stu-id="78e73-134">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="78e73-135">Пакет SDK построителя построителя обрабатывает все подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="78e73-135">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="78e73-136">Если вы решили использовать REST API, вы также можете вызвать [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) конечную точку.</span><span class="sxs-lookup"><span data-stu-id="78e73-136">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="78e73-137">В канале ответ на сообщение отображается как ответ на инициированную цепь ответа.</span><span class="sxs-lookup"><span data-stu-id="78e73-137">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="78e73-138">`conversation.id`Содержит канал и идентификатор сообщения верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="78e73-138">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="78e73-139">Несмотря на то, что у Bot Framework есть сведения, вы можете кэшировать их `conversation.id` для будущих ответов на этот поток беседы по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="78e73-139">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="78e73-140">Советы и рекомендации: приветственные сообщения в Teams</span><span class="sxs-lookup"><span data-stu-id="78e73-140">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="78e73-141">При первом добавлении ленты в группу или команду, как правило, полезно отправить приветственное сообщение для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="78e73-141">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="78e73-142">Приветственное сообщение должно содержать описание функции и преимуществ пользователя Bot.</span><span class="sxs-lookup"><span data-stu-id="78e73-142">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="78e73-143">В идеале сообщение также должно включать команды для взаимодействия пользователя с приложением.</span><span class="sxs-lookup"><span data-stu-id="78e73-143">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="78e73-144">Для этого необходимо убедиться, что в объекте Bot реагирует на `conversationUpdate` сообщение с параметром `teamsAddMembers` EventType в `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="78e73-144">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="78e73-145">Убедитесь, что `memberAdded` идентификатор является собственно идентификатором приложения-робота, так как при добавлении пользователя в команду отправляется то же самое событие.</span><span class="sxs-lookup"><span data-stu-id="78e73-145">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="78e73-146">Дополнительные сведения см. в разделе " [участник группы" или "Добавление ленты](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) ".</span><span class="sxs-lookup"><span data-stu-id="78e73-146">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="78e73-147">Кроме того, вы можете отправить личное сообщение каждому участнику команды при добавлении ленты.</span><span class="sxs-lookup"><span data-stu-id="78e73-147">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="78e73-148">Для этого вы можете получить список [команд](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) и отправить каждому пользователю [прямое сообщение](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span><span class="sxs-lookup"><span data-stu-id="78e73-148">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="78e73-149">*Не* рекомендуется отправлять приветственное сообщение в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="78e73-149">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="78e73-150">Команда является большой (субъективно субъективна, но например, более 100 членов).</span><span class="sxs-lookup"><span data-stu-id="78e73-150">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="78e73-151">Ваш робот может отображаться как "нежелательный", а пользователь, который добавил его, может получать жалобу, если вы не хотите явно сообщить о значении для пользователя, который видит приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="78e73-151">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="78e73-152">Первый из них упоминается в группе или канале (в отличие от первого добавления в группу).</span><span class="sxs-lookup"><span data-stu-id="78e73-152">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="78e73-153">Переименование группы или канала</span><span class="sxs-lookup"><span data-stu-id="78e73-153">A group or channel is renamed</span></span>
* <span data-ttu-id="78e73-154">Участник группы добавляется в группу или канал</span><span class="sxs-lookup"><span data-stu-id="78e73-154">A team member is added to a group or channel</span></span>

## <a name="-mentions"></a><span data-ttu-id="78e73-155">@ Упоминания</span><span class="sxs-lookup"><span data-stu-id="78e73-155">@ Mentions</span></span>

<span data-ttu-id="78e73-156">Так как боты в группе или канале отвечают только на то, что они упоминаются ("@_ботнаме_") в сообщении, каждое сообщение, полученное в канале группы "bot", содержит собственное имя, и вы должны убедиться в том, что дескрипторы синтаксического анализа сообщений.</span><span class="sxs-lookup"><span data-stu-id="78e73-156">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="78e73-157">Кроме того, Боты может проанализировать других пользователей, упомянутых и упомянутых пользователям, в составе своих сообщений.</span><span class="sxs-lookup"><span data-stu-id="78e73-157">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="78e73-158">Получение упоминаний</span><span class="sxs-lookup"><span data-stu-id="78e73-158">Retrieving mentions</span></span>

<span data-ttu-id="78e73-159">Упоминания возвращаются в `entities` объекте полезных данных и содержат как уникальный идентификатор пользователя, так и, в большинстве случаев, имя пользователя, указанное пользователем.</span><span class="sxs-lookup"><span data-stu-id="78e73-159">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="78e73-160">Вы можете получить все упоминания в сообщении, вызвав `GetMentions` функцию в пакете SDK построителя построителя для .NET, которая возвращает массив `Mentioned` объектов.</span><span class="sxs-lookup"><span data-stu-id="78e73-160">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="78e73-161">Пример кода .NET: Поиск и чередование @bot упоминаний</span><span class="sxs-lookup"><span data-stu-id="78e73-161">.NET example code: Check for and strip @bot mention</span></span>

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
> <span data-ttu-id="78e73-162">Вы также можете использовать функцию расширения Teams `GetTextWithoutMentions` , которая выполнит все упоминания, включая Bot.</span><span class="sxs-lookup"><span data-stu-id="78e73-162">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="78e73-163">Node.js пример кода: Поиск и чередование @bot упоминаний</span><span class="sxs-lookup"><span data-stu-id="78e73-163">Node.js example code: Check for and strip @bot mention</span></span>

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

<span data-ttu-id="78e73-164">Вы также можете использовать функцию расширения Teams `getTextWithoutMentions` , которая выполнит все упоминания, включая Bot.</span><span class="sxs-lookup"><span data-stu-id="78e73-164">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="78e73-165">Создание упоминаний</span><span class="sxs-lookup"><span data-stu-id="78e73-165">Constructing mentions</span></span>

<span data-ttu-id="78e73-166">Ваш Bot может заупоминаниь других пользователей в сообщениях, размещенных в каналах.</span><span class="sxs-lookup"><span data-stu-id="78e73-166">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="78e73-167">Для этого сообщение должно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="78e73-167">To do this, your message must do the following:</span></span>

* <span data-ttu-id="78e73-168">Включить `<at>@username</at>` в текст сообщения</span><span class="sxs-lookup"><span data-stu-id="78e73-168">Include `<at>@username</at>` in the message text</span></span>
* <span data-ttu-id="78e73-169">Включение `mention` объекта в коллекцию сущностей</span><span class="sxs-lookup"><span data-stu-id="78e73-169">Include the `mention` object inside the entities collection</span></span>

#### <a name="net-example"></a><span data-ttu-id="78e73-170">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="78e73-170">.NET example</span></span>

<span data-ttu-id="78e73-171">В этом примере используется пакет NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .</span><span class="sxs-lookup"><span data-stu-id="78e73-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="78e73-172">Пример Node.js</span><span class="sxs-lookup"><span data-stu-id="78e73-172">Node.js example</span></span>

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

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="78e73-173">Пример: исходящее сообщение с указанным пользователем</span><span class="sxs-lookup"><span data-stu-id="78e73-173">Example: Outgoing message with user mentioned</span></span>

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

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="78e73-174">Доступ к области groupChat или канала</span><span class="sxs-lookup"><span data-stu-id="78e73-174">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="78e73-175">Ваш робот может выполнять больше, чем отправлять и получать сообщения в группах и в Teams.</span><span class="sxs-lookup"><span data-stu-id="78e73-175">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="78e73-176">Например, он также может получить список элементов, включая сведения о их профилях, а также список каналов.</span><span class="sxs-lookup"><span data-stu-id="78e73-176">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="78e73-177">Чтобы узнать больше, ознакомьтесь со [статьей получение контекста для робота Microsoft Teams](~/resources/bot-v3/bots-context.md) .</span><span class="sxs-lookup"><span data-stu-id="78e73-177">See [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md) to learn more.</span></span>

<span data-ttu-id="78e73-178">В этой статье *также приведены* [примеры кода Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="78e73-178">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
