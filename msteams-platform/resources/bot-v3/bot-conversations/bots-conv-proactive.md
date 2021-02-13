---
title: Упреждающие сообщения
description: Описание ботов, которые могут начать беседу в Microsoft Teams
keywords: teams scenarios proactive messaging conversation bot
ms.openlocfilehash: 8c93696f79b5d99c32162a7374c7d9adccacb984
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231626"
---
# <a name="proactive-messaging-for-bots"></a><span data-ttu-id="43e4b-104">Упреждающий обмен сообщениями для ботов</span><span class="sxs-lookup"><span data-stu-id="43e4b-104">Proactive messaging for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="43e4b-105">Заблаговременное сообщение — это сообщение, от отправленное ботом для начала беседы.</span><span class="sxs-lookup"><span data-stu-id="43e4b-105">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="43e4b-106">Бот может начать беседу по ряду причин, в том числе:</span><span class="sxs-lookup"><span data-stu-id="43e4b-106">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="43e4b-107">Приветствия для личных бесед ботов</span><span class="sxs-lookup"><span data-stu-id="43e4b-107">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="43e4b-108">Ответы на опрос</span><span class="sxs-lookup"><span data-stu-id="43e4b-108">Poll responses</span></span>
* <span data-ttu-id="43e4b-109">Уведомления о внешних событиях</span><span class="sxs-lookup"><span data-stu-id="43e4b-109">External event notifications</span></span>

<span data-ttu-id="43e4b-110">Отправка сообщения для запуска нового цепочки беседы отличается от отправки сообщения в ответ на существующую беседу: когда бот начинает новую беседу, нет существующей беседы для публикации сообщения.</span><span class="sxs-lookup"><span data-stu-id="43e4b-110">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="43e4b-111">Чтобы отправить упреждающие сообщения, необходимо:</span><span class="sxs-lookup"><span data-stu-id="43e4b-111">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="43e4b-112">Решите, что вы собираетесь сказать</span><span class="sxs-lookup"><span data-stu-id="43e4b-112">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="43e4b-113">Получение уникального ИД пользователя и ид клиента</span><span class="sxs-lookup"><span data-stu-id="43e4b-113">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="43e4b-114">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="43e4b-114">Send the message</span></span>](#examples)

<span data-ttu-id="43e4b-115">При создании упреждающих **сообщений** необходимо вызвать и передать URL-адрес службы, прежде чем создавать сообщения, которые будут `MicrosoftAppCredentials.TrustServiceUrl` использовать для `ConnectorClient` отправки.</span><span class="sxs-lookup"><span data-stu-id="43e4b-115">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="43e4b-116">Если этого не сделать, ваше приложение получит `401: Unauthorized` ответ.</span><span class="sxs-lookup"><span data-stu-id="43e4b-116">If you do not, your app will receive a `401: Unauthorized` response.</span></span> <span data-ttu-id="43e4b-117">См. [примеры ниже.](#net-example-from-this-sample)</span><span class="sxs-lookup"><span data-stu-id="43e4b-117">See [the samples below](#net-example-from-this-sample).</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="43e4b-118">Best practices for proactive messaging</span><span class="sxs-lookup"><span data-stu-id="43e4b-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="43e4b-119">Отправка упреждающих сообщений пользователям может быть очень эффективным способом общения с пользователями.</span><span class="sxs-lookup"><span data-stu-id="43e4b-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="43e4b-120">Однако с их точки зрения это сообщение может казаться им полностью необсмещенным, и в случае приветствия сообщения будут отображаться при первом взаимодействии с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="43e4b-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="43e4b-121">Поэтому очень важно использовать эту функцию экономно (не спамить пользователей) и предоставлять им достаточно информации, чтобы дать им понять, почему они рассылаются сообщения.</span><span class="sxs-lookup"><span data-stu-id="43e4b-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="43e4b-122">Упреждающие сообщения обычно попадают в одну из двух категорий: приветствия или уведомления.</span><span class="sxs-lookup"><span data-stu-id="43e4b-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="43e4b-123">Приветствия</span><span class="sxs-lookup"><span data-stu-id="43e4b-123">Welcome messages</span></span>

<span data-ttu-id="43e4b-124">При использовании упреждающих сообщений для отправки приветствия пользователю следует помнить, что для большинства людей, получающих сообщение, у них не будет контекста для причины его получения.</span><span class="sxs-lookup"><span data-stu-id="43e4b-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="43e4b-125">Это также первый раз, когда они будут взаимодействовать с вашим приложением; это ваша возможность создать хорошее первое впечатление.</span><span class="sxs-lookup"><span data-stu-id="43e4b-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="43e4b-126">К наиболее оптимальным приветствиям относятся:</span><span class="sxs-lookup"><span data-stu-id="43e4b-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="43e4b-127">**Почему они получают это сообщение.**</span><span class="sxs-lookup"><span data-stu-id="43e4b-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="43e4b-128">Пользователю должно быть понятно, почему он получает сообщение.</span><span class="sxs-lookup"><span data-stu-id="43e4b-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="43e4b-129">Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен и кто, возможно, установил его.</span><span class="sxs-lookup"><span data-stu-id="43e4b-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="43e4b-130">**Что вы предлагаете.**</span><span class="sxs-lookup"><span data-stu-id="43e4b-130">**What do you offer.**</span></span> <span data-ttu-id="43e4b-131">Что они могут делать с вашим приложением?</span><span class="sxs-lookup"><span data-stu-id="43e4b-131">What can they do with your app?</span></span> <span data-ttu-id="43e4b-132">Какое значение вы можете им дать?</span><span class="sxs-lookup"><span data-stu-id="43e4b-132">What value can you bring to them?</span></span>
* <span data-ttu-id="43e4b-133">**Что они должны делать дальше.**</span><span class="sxs-lookup"><span data-stu-id="43e4b-133">**What should they do next.**</span></span> <span data-ttu-id="43e4b-134">Предложите им опробовать команду или каким-либо образом взаимодействовать с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="43e4b-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="43e4b-135">Уведомления</span><span class="sxs-lookup"><span data-stu-id="43e4b-135">Notification messages</span></span>

<span data-ttu-id="43e4b-136">При использовании упреждающих сообщений для отправки уведомлений необходимо убедиться, что у пользователей есть четкий путь к общим действиям на основе уведомления и четкое понимание причины отправки уведомления.</span><span class="sxs-lookup"><span data-stu-id="43e4b-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="43e4b-137">Хорошие уведомления обычно включают в себя следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="43e4b-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="43e4b-138">**Что случилось.**</span><span class="sxs-lookup"><span data-stu-id="43e4b-138">**What happened.**</span></span> <span data-ttu-id="43e4b-139">Четкое указание того, что стало причиной уведомления.</span><span class="sxs-lookup"><span data-stu-id="43e4b-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="43e4b-140">**С чем это произошло.**</span><span class="sxs-lookup"><span data-stu-id="43e4b-140">**What it happened to.**</span></span> <span data-ttu-id="43e4b-141">Должно быть понятно, какой элемент или элемент был обновлен для уведомления.</span><span class="sxs-lookup"><span data-stu-id="43e4b-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="43e4b-142">**Кто это сделал.**</span><span class="sxs-lookup"><span data-stu-id="43e4b-142">**Who did it.**</span></span> <span data-ttu-id="43e4b-143">Кто принял действие, которое привело к отправлению уведомления.</span><span class="sxs-lookup"><span data-stu-id="43e4b-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="43e4b-144">**Что они могут делать с этим.**</span><span class="sxs-lookup"><span data-stu-id="43e4b-144">**What they can do about it.**</span></span> <span data-ttu-id="43e4b-145">Сделайте так, чтобы пользователи легко сделайте действия на основе ваших уведомлений.</span><span class="sxs-lookup"><span data-stu-id="43e4b-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="43e4b-146">**Как они могут отказаться.** Необходимо предоставить пользователям путь для отказа от дополнительных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="43e4b-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="43e4b-147">Получение необходимых сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="43e4b-147">Obtain necessary user information</span></span>

<span data-ttu-id="43e4b-148">Боты могут создавать новые беседы с отдельным пользователем Microsoft  Teams, получив уникальный ИД пользователя и *ИД клиента.*</span><span class="sxs-lookup"><span data-stu-id="43e4b-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user's *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="43e4b-149">Эти значения можно получить с помощью одного из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="43e4b-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="43e4b-150">Путем [получения группы из](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) канала, в который устанавливается ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="43e4b-150">By [fetching the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) from a channel your app is installed in.</span></span>
* <span data-ttu-id="43e4b-151">Кэшing их, когда пользователь [взаимодействует с ботом в канале.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)</span><span class="sxs-lookup"><span data-stu-id="43e4b-151">By caching them when a user [interacts with your bot in a channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span></span>
* <span data-ttu-id="43e4b-152">Когда пользователь @mentioned [в беседе канала,](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) в его состав входит бот.</span><span class="sxs-lookup"><span data-stu-id="43e4b-152">When a users is [@mentioned in a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="43e4b-153">Кэшing их, когда [ `conversationUpdate` вы](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) получаете событие, когда приложение установлено в личной области, или новые участники добавляются в канал или групповой чат,</span><span class="sxs-lookup"><span data-stu-id="43e4b-153">By caching them when you [receive the `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="43e4b-154">Упреждающие установки приложения с помощью Graph</span><span class="sxs-lookup"><span data-stu-id="43e4b-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="43e4b-155">Упреждающие установки приложений с помощью graph в настоящее время находятся в бета-версии.</span><span class="sxs-lookup"><span data-stu-id="43e4b-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="43e4b-156">Иногда может потребоваться заблаговременное сообщение пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="43e4b-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="43e4b-157">Например, вы хотите использовать company [communicator](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации.</span><span class="sxs-lookup"><span data-stu-id="43e4b-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="43e4b-158">В этом сценарии можно использовать API Graph для упреждающего установки приложения для пользователей, а затем кэшировать необходимые значения из события, которое ваше приложение получит после `conversationUpdate` установки.</span><span class="sxs-lookup"><span data-stu-id="43e4b-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="43e4b-159">Вы можете устанавливать только приложения, которые находятся в каталоге приложения организации или в магазине приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="43e4b-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="43e4b-160">Подробные [сведения см. в](/graph/teams-proactive-messaging) документации По установке приложений для пользователей в документации Graph.</span><span class="sxs-lookup"><span data-stu-id="43e4b-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="43e4b-161">Кроме того, в [.NET есть пример.](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)</span><span class="sxs-lookup"><span data-stu-id="43e4b-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="43e4b-162">Примеры</span><span class="sxs-lookup"><span data-stu-id="43e4b-162">Examples</span></span>

<span data-ttu-id="43e4b-163">Перед созданием новой беседы с помощью REST API убедитесь, что вы пройдете проверку подлинности и имеете маркер носители.</span><span class="sxs-lookup"><span data-stu-id="43e4b-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span>

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

<span data-ttu-id="43e4b-164">Необходимо предоставить ид пользователя, и ид клиента.</span><span class="sxs-lookup"><span data-stu-id="43e4b-164">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="43e4b-165">В случае успешного вызова API возвращается со следующим объектом ответа.</span><span class="sxs-lookup"><span data-stu-id="43e4b-165">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="43e4b-166">Этот ИД является уникальным ид беседы личного чата.</span><span class="sxs-lookup"><span data-stu-id="43e4b-166">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="43e4b-167">Оохраняйте это значение и повторно его использовать для будущих взаимодействий с пользователем.</span><span class="sxs-lookup"><span data-stu-id="43e4b-167">Please store this value and reuse it for future interactions with the user.</span></span>

### <a name="using-net"></a><span data-ttu-id="43e4b-168">Использование .NET</span><span class="sxs-lookup"><span data-stu-id="43e4b-168">Using .NET</span></span>

<span data-ttu-id="43e4b-169">В этом примере используется [пакет NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="43e4b-169">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create or get existing chat conversation with user
var response = client.Conversations.CreateOrGetDirectConversation(activity.Recipient, activity.From, activity.GetTenantId());

// Construct the message to post to conversation
Activity newActivity = new Activity()
{
    Text = "Hello",
    Type = ActivityTypes.Message,
    Conversation = new ConversationAccount
    {
        Id = response.Id
    },
};

// Post the message to chat conversation with user
await client.Conversations.SendToConversationAsync(newActivity, response.Id);
```

### <a name="using-nodejs"></a><span data-ttu-id="43e4b-170">Использование Node.js</span><span class="sxs-lookup"><span data-stu-id="43e4b-170">Using Node.js</span></span>

```javascript
var address =
{
    channelId: 'msteams',
    user: { id: userId },
    channelData: {
        tenant: {
            id: tenantId
        }
    },
    bot:
    {
        id: appId,
        name: appName
    },
    serviceUrl: session.message.address.serviceUrl,
    useAuth: true
}

var msg = new builder.Message().address(address);
msg.text('Hello, this is a notification');
bot.send(msg);
```

<span data-ttu-id="43e4b-171">*См. также* [примеры Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="43e4b-171">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="43e4b-172">Создание беседы в канале</span><span class="sxs-lookup"><span data-stu-id="43e4b-172">Creating a channel conversation</span></span>

<span data-ttu-id="43e4b-173">Добавленный в команду бот может опубликовать в канале, чтобы создать новую цепочку ответов.</span><span class="sxs-lookup"><span data-stu-id="43e4b-173">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="43e4b-174">Если вы используете Node.js Teams SDK, используйте его, чтобы у вас был полностью заполнен адрес с правильным идом действия и ид `startReplyChain()` беседы. Если вы используете C#, см. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="43e4b-174">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="43e4b-175">Кроме того, вы можете использовать REST API и опубликовать запрос POST к [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ресурсу.</span><span class="sxs-lookup"><span data-stu-id="43e4b-175">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

### <a name="net-example-from-this-sample"></a><span data-ttu-id="43e4b-176">Пример .NET [(из этого примера)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)</span><span class="sxs-lookup"><span data-stu-id="43e4b-176">.NET example (from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span></span>

```csharp
using Microsoft.Bot.Builder.Dialogs;
using Microsoft.Bot.Connector;
using Microsoft.Bot.Connector.Teams.Models;
using Microsoft.Teams.TemplateBotCSharp.Properties;
using System;
using System.Threading.Tasks;

namespace Microsoft.Teams.TemplateBotCSharp.Dialogs
{
    [Serializable]
    public class ProactiveMsgTo1to1Dialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            var channelData = context.Activity.GetChannelData<TeamsChannelData>();
            var message = Activity.CreateMessageActivity();
            message.Text = "Hello World";

            var conversationParameters = new ConversationParameters
            {
                  IsGroup = true,
                  ChannelData = new TeamsChannelData
                  {
                      Channel = new ChannelInfo(channelData.Channel.Id),
                  },
                  Activity = (Activity) message
            };

            MicrosoftAppCredentials.TrustServiceUrl(serviceUrl, DateTime.MaxValue);
            var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl));
            var response = await connectorClient.Conversations.CreateConversationAsync(conversationParameters);

            context.Done<object>(null);
        }
    }
}
```
