---
title: Проактивные сообщения
description: Описывает, как боты могут начать беседу в Microsoft Teams
ms.topic: conceptual
keywords: teams scenarios proactive messaging conversation bot
ms.openlocfilehash: ee0d2900818a587e447e17ae3111bee621fa8de9
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696166"
---
# <a name="proactive-messaging-for-bots"></a><span data-ttu-id="368f6-104">Активный обмен сообщениями для ботов</span><span class="sxs-lookup"><span data-stu-id="368f6-104">Proactive messaging for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="368f6-105">Проактивное сообщение — это сообщение, отправленное ботом для начала беседы.</span><span class="sxs-lookup"><span data-stu-id="368f6-105">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="368f6-106">Существует множество различных причин для инициирования беседы ботом, в том числе:</span><span class="sxs-lookup"><span data-stu-id="368f6-106">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="368f6-107">приветствия в личных беседах с ботами;</span><span class="sxs-lookup"><span data-stu-id="368f6-107">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="368f6-108">ответы на опросы;</span><span class="sxs-lookup"><span data-stu-id="368f6-108">Poll responses</span></span>
* <span data-ttu-id="368f6-109">уведомления о внешних событиях.</span><span class="sxs-lookup"><span data-stu-id="368f6-109">External event notifications</span></span>

<span data-ttu-id="368f6-110">Отправка сообщения для запуска нового потока беседы отличается от отправки сообщения в ответ на существующий разговор: когда ваш бот начинает новый разговор, для отправки сообщения не существует предварительно существующего разговора.</span><span class="sxs-lookup"><span data-stu-id="368f6-110">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="368f6-111">Чтобы отправить проактивное сообщение, необходимо:</span><span class="sxs-lookup"><span data-stu-id="368f6-111">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="368f6-112">Решите, что вы собираетесь сказать</span><span class="sxs-lookup"><span data-stu-id="368f6-112">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="368f6-113">Получение уникального ИД пользователя и его клиента</span><span class="sxs-lookup"><span data-stu-id="368f6-113">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="368f6-114">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="368f6-114">Send the message</span></span>](#examples)

<span data-ttu-id="368f6-115">При создании упреждающих **сообщений** необходимо вызвать и передать URL-адрес службы перед созданием используемого для `MicrosoftAppCredentials.TrustServiceUrl` `ConnectorClient` отправки сообщения.</span><span class="sxs-lookup"><span data-stu-id="368f6-115">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="368f6-116">Если этого не сделать, приложение получит `401: Unauthorized` ответ.</span><span class="sxs-lookup"><span data-stu-id="368f6-116">If you do not, your app will receive a `401: Unauthorized` response.</span></span> <span data-ttu-id="368f6-117">Примеры [см. ниже.](#net-example-from-this-sample)</span><span class="sxs-lookup"><span data-stu-id="368f6-117">See [the samples below](#net-example-from-this-sample).</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="368f6-118">Лучшие практики для активного обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="368f6-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="368f6-119">Отправка активных сообщений пользователям может быть очень эффективным способом общения с пользователями.</span><span class="sxs-lookup"><span data-stu-id="368f6-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="368f6-120">Однако с их точки зрения это сообщение может казаться совершенно незащищенным, и в случае приветствия сообщения будут впервые взаимодействовать с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="368f6-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="368f6-121">Поэтому очень важно использовать эту функцию щадя (не спамить пользователей) и предоставлять им достаточно информации, чтобы они могли понять, почему они рассылаются.</span><span class="sxs-lookup"><span data-stu-id="368f6-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="368f6-122">Как правило, упреждающие сообщения относятся к одной из двух категорий: приветствиям или уведомлениям.</span><span class="sxs-lookup"><span data-stu-id="368f6-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="368f6-123">Приветствия</span><span class="sxs-lookup"><span data-stu-id="368f6-123">Welcome messages</span></span>

<span data-ttu-id="368f6-124">При использовании активного обмена сообщениями для отправки приветствия пользователю необходимо иметь в виду, что для большинства людей, получающих сообщение, у них не будет контекста для его получения.</span><span class="sxs-lookup"><span data-stu-id="368f6-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="368f6-125">Это также первый раз, когда они будут взаимодействовать с вашим приложением; это ваша возможность создать хорошее первое впечатление.</span><span class="sxs-lookup"><span data-stu-id="368f6-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="368f6-126">Лучшие приветствия будут включать в себя:</span><span class="sxs-lookup"><span data-stu-id="368f6-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="368f6-127">**Почему они получают это сообщение.**</span><span class="sxs-lookup"><span data-stu-id="368f6-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="368f6-128">Пользователю должно быть ясно, почему он получает сообщение.</span><span class="sxs-lookup"><span data-stu-id="368f6-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="368f6-129">Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен и кто его установил.</span><span class="sxs-lookup"><span data-stu-id="368f6-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="368f6-130">**Что вы предлагаете.**</span><span class="sxs-lookup"><span data-stu-id="368f6-130">**What do you offer.**</span></span> <span data-ttu-id="368f6-131">Что они могут сделать с вашим приложением?</span><span class="sxs-lookup"><span data-stu-id="368f6-131">What can they do with your app?</span></span> <span data-ttu-id="368f6-132">Какое значение вы можете принести им?</span><span class="sxs-lookup"><span data-stu-id="368f6-132">What value can you bring to them?</span></span>
* <span data-ttu-id="368f6-133">**Что они должны делать дальше.**</span><span class="sxs-lookup"><span data-stu-id="368f6-133">**What should they do next.**</span></span> <span data-ttu-id="368f6-134">Предложите им опробовать команду или каким-то образом взаимодействовать с приложением.</span><span class="sxs-lookup"><span data-stu-id="368f6-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="368f6-135">Уведомления</span><span class="sxs-lookup"><span data-stu-id="368f6-135">Notification messages</span></span>

<span data-ttu-id="368f6-136">При использовании активного обмена сообщениями для отправки уведомлений необходимо убедиться, что у пользователей есть четкий путь к общим действиям на основе уведомления и четкого понимания причин, по которым произошло уведомление.</span><span class="sxs-lookup"><span data-stu-id="368f6-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="368f6-137">Хорошие сообщения уведомлений обычно включают в себя:</span><span class="sxs-lookup"><span data-stu-id="368f6-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="368f6-138">**Что случилось.**</span><span class="sxs-lookup"><span data-stu-id="368f6-138">**What happened.**</span></span> <span data-ttu-id="368f6-139">Четкое указание на то, что стало причиной уведомления.</span><span class="sxs-lookup"><span data-stu-id="368f6-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="368f6-140">**С чем это случилось.**</span><span class="sxs-lookup"><span data-stu-id="368f6-140">**What it happened to.**</span></span> <span data-ttu-id="368f6-141">Должно быть понятно, какой элемент/вещь был обновлен, чтобы вызвать уведомление.</span><span class="sxs-lookup"><span data-stu-id="368f6-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="368f6-142">**Кто это сделал.**</span><span class="sxs-lookup"><span data-stu-id="368f6-142">**Who did it.**</span></span> <span data-ttu-id="368f6-143">Кто принял действие, из-за которого было отправлено уведомление.</span><span class="sxs-lookup"><span data-stu-id="368f6-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="368f6-144">**Что они могут с этим сделать.**</span><span class="sxs-lookup"><span data-stu-id="368f6-144">**What they can do about it.**</span></span> <span data-ttu-id="368f6-145">Сделайте так, чтобы пользователям было проще принимать меры на основе ваших уведомлений.</span><span class="sxs-lookup"><span data-stu-id="368f6-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="368f6-146">**Как они могут отказаться.** Необходимо предоставить пользователям путь к отказу от дополнительных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="368f6-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="368f6-147">Получение необходимых сведений о пользователях</span><span class="sxs-lookup"><span data-stu-id="368f6-147">Obtain necessary user information</span></span>

<span data-ttu-id="368f6-148">Боты могут создавать новые беседы с отдельным пользователем Microsoft Teams, получив уникальный *ID* пользователя и *ID клиента.*</span><span class="sxs-lookup"><span data-stu-id="368f6-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user's *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="368f6-149">Эти значения можно получить с помощью одного из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="368f6-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="368f6-150">[Извлечение реестра команды из](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) канала, в который установлено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="368f6-150">By [fetching the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) from a channel your app is installed in.</span></span>
* <span data-ttu-id="368f6-151">Кэшинг их при взаимодействии пользователя с [ботом в канале.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)</span><span class="sxs-lookup"><span data-stu-id="368f6-151">By caching them when a user [interacts with your bot in a channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span></span>
* <span data-ttu-id="368f6-152">Когда пользователи @mentioned [в разговоре канала,](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) бот является частью.</span><span class="sxs-lookup"><span data-stu-id="368f6-152">When a users is [@mentioned in a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="368f6-153">Кэшинг их при [ `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) приеме события при установке приложения в личной области или добавлении новых участников в канал или групповой чат,</span><span class="sxs-lookup"><span data-stu-id="368f6-153">By caching them when you [receive the `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="368f6-154">Активная установка приложения с помощью Graph</span><span class="sxs-lookup"><span data-stu-id="368f6-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="368f6-155">Активная установка приложений с помощью графа в настоящее время находится в бета-версии.</span><span class="sxs-lookup"><span data-stu-id="368f6-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="368f6-156">Иногда может потребоваться заблаговременное сообщение пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="368f6-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="368f6-157">Например, вы хотите использовать коммуникатор [компании](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации.</span><span class="sxs-lookup"><span data-stu-id="368f6-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="368f6-158">Для этого сценария можно использовать API Graph для активной установки приложения для пользователей, а затем кэшировать необходимые значения из события, которое ваше приложение получит после `conversationUpdate` установки.</span><span class="sxs-lookup"><span data-stu-id="368f6-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="368f6-159">Можно установить только приложения, которые находятся в каталоге организационных приложений или в магазине приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="368f6-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="368f6-160">Дополнительные [сведения см. в документации](/graph/teams-proactive-messaging) По установке приложений для пользователей в документации Graph.</span><span class="sxs-lookup"><span data-stu-id="368f6-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="368f6-161">Существует также пример [в .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span><span class="sxs-lookup"><span data-stu-id="368f6-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="368f6-162">Примеры</span><span class="sxs-lookup"><span data-stu-id="368f6-162">Examples</span></span>

<span data-ttu-id="368f6-163">Убедитесь, что перед созданием нового разговора с помощью API REST у вас есть маркер проверки подлинности и носите.</span><span class="sxs-lookup"><span data-stu-id="368f6-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span>

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

<span data-ttu-id="368f6-164">Необходимо предоставить пользовательский ИД и ИД клиента.</span><span class="sxs-lookup"><span data-stu-id="368f6-164">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="368f6-165">Если вызов удался, API возвращается со следующим объектом ответа.</span><span class="sxs-lookup"><span data-stu-id="368f6-165">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="368f6-166">Этот ID является уникальным ид беседы личного чата.</span><span class="sxs-lookup"><span data-stu-id="368f6-166">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="368f6-167">Пожалуйста, сохраняйте это значение и повторно его использовать для будущих взаимодействий с пользователем.</span><span class="sxs-lookup"><span data-stu-id="368f6-167">Please store this value and reuse it for future interactions with the user.</span></span>

### <a name="using-net"></a><span data-ttu-id="368f6-168">Использование .NET</span><span class="sxs-lookup"><span data-stu-id="368f6-168">Using .NET</span></span>

<span data-ttu-id="368f6-169">В этом примере используется [пакет Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.</span><span class="sxs-lookup"><span data-stu-id="368f6-169">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

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

### <a name="using-nodejs"></a><span data-ttu-id="368f6-170">Использование Node.js</span><span class="sxs-lookup"><span data-stu-id="368f6-170">Using Node.js</span></span>

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

<span data-ttu-id="368f6-171">*См. также* [примеры Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="368f6-171">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="368f6-172">Создание беседы на канале</span><span class="sxs-lookup"><span data-stu-id="368f6-172">Creating a channel conversation</span></span>

<span data-ttu-id="368f6-173">Бот, добавленный в команду, может публиковать сообщения на канале, создавая новые цепочки ответов.</span><span class="sxs-lookup"><span data-stu-id="368f6-173">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="368f6-174">Если вы используете Node.js Teams SDK, используйте его, который дает вам полностью заполненный адрес с правильным ид-ид `startReplyChain()` действий. Если вы используете C#, см. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="368f6-174">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="368f6-175">Кроме того, можно использовать API REST и опубликовать запрос POST на [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ресурс.</span><span class="sxs-lookup"><span data-stu-id="368f6-175">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

### <a name="net-example-from-this-sample"></a><span data-ttu-id="368f6-176">Пример .NET [(из этого примера)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)</span><span class="sxs-lookup"><span data-stu-id="368f6-176">.NET example (from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span></span>

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
