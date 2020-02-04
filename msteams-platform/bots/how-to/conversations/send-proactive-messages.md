---
title: Отправка упреждающих сообщений
author: clearab
description: Отправка активных сообщений с помощью робота Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e60fdbfb909abec2c6d64ed0d32fa1a4c4b463a6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675310"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="f9ea4-103">Отправка упреждающих сообщений</span><span class="sxs-lookup"><span data-stu-id="f9ea4-103">Send proactive messages</span></span>

> [!Note]
> <span data-ttu-id="f9ea4-104">В примерах кода, приведенных в этой статье, используются расширения пакета SDK для v3 и 3 для Teams построителя.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-104">The code samples in this article make use of the v3 Bot Framework SDK, and v3 Teams Bot Builder SDK extensions.</span></span> <span data-ttu-id="f9ea4-105">Концептуально сведения применяются при использовании версий пакета v4 SDK V4, но код слегка отличается.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-105">Conceptually, the information applies when using the v4 versions of the SDK, but the code is slightly different.</span></span>

<span data-ttu-id="f9ea4-106">Упреждающее сообщение — это сообщение, которое отправляется с помощью ленты, чтобы начать беседу.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-106">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="f9ea4-107">Вы можете попытаться начать беседу по ряду причин, в том числе:</span><span class="sxs-lookup"><span data-stu-id="f9ea4-107">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="f9ea4-108">Приветственные сообщения для личных бесед</span><span class="sxs-lookup"><span data-stu-id="f9ea4-108">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="f9ea4-109">Ответы опросов</span><span class="sxs-lookup"><span data-stu-id="f9ea4-109">Poll responses</span></span>
* <span data-ttu-id="f9ea4-110">Уведомления о внешних событиях</span><span class="sxs-lookup"><span data-stu-id="f9ea4-110">External event notifications</span></span>

<span data-ttu-id="f9ea4-111">Отправка сообщения для запуска нового цепочки беседы отличается от отправки сообщения в ответ на существующую беседу: при начале новой беседы не существует диалогового окна, в котором будет размещаться сообщение.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-111">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="f9ea4-112">Чтобы отправить упреждающее сообщение, необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f9ea4-112">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="f9ea4-113">Принятие решения о том, что вы собираетесь говорить</span><span class="sxs-lookup"><span data-stu-id="f9ea4-113">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="f9ea4-114">Получение уникального идентификатора пользователя и идентификатора клиента</span><span class="sxs-lookup"><span data-stu-id="f9ea4-114">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="f9ea4-115">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="f9ea4-115">Send the message</span></span>](#examples)

<span data-ttu-id="f9ea4-116">При создании упреждающего сообщения **необходимо** вызвать `MicrosoftAppCredentials.TrustServiceUrl`и передать URL-адрес службы перед созданием `ConnectorClient` , который будет использоваться для отправки сообщения.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-116">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="f9ea4-117">В противном случае ваше приложение получит `401: Unauthorized` ответ.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-117">If you do not, your app will receive a `401: Unauthorized` response.</span></span> 

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="f9ea4-118">Рекомендации по использованию упреждающего обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="f9ea4-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="f9ea4-119">Отправка упреждающих сообщений пользователям может быть очень эффективным способом общения с пользователями.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="f9ea4-120">Однако с их точки зрения это сообщение может быть полностью нежелательным, а в случае приветственных сообщений будет использоваться при первом взаимодействии с приложением.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="f9ea4-121">Таким образом, очень важно использовать эту функцию экономно (не спама для пользователей) и предоставить им достаточно информации, чтобы убедиться в их подлинности.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="f9ea4-122">Упреждающие сообщения обычно делятся на две категории: приветственные сообщения или уведомления.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="f9ea4-123">Приветственные сообщения</span><span class="sxs-lookup"><span data-stu-id="f9ea4-123">Welcome messages</span></span>

<span data-ttu-id="f9ea4-124">При использовании упреждающего обмена сообщениями для отправки пользователю приветственного сообщения необходимо помнить, что большинство людей, получивших сообщение, не будут иметь контекст для их получения.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="f9ea4-125">Это также происходит в первый раз, когда он будет взаимодействовать с вашим приложением; можно создать хорошее первое впечатление.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="f9ea4-126">Лучшие приветственные сообщения будут включать:</span><span class="sxs-lookup"><span data-stu-id="f9ea4-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="f9ea4-127">**Почему они получают это сообщение.**</span><span class="sxs-lookup"><span data-stu-id="f9ea4-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="f9ea4-128">Он должен быть очень очевидным, чтобы пользователь получал сообщение.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="f9ea4-129">Если ваш Bot был установлен в канале и вы отправили приветственное сообщение всем пользователям, сообщите им о том, в каком канале он был установлен и кто его установил.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="f9ea4-130">**Что вы предоставляете.**</span><span class="sxs-lookup"><span data-stu-id="f9ea4-130">**What do you offer.**</span></span> <span data-ttu-id="f9ea4-131">Что можно делать с приложением?</span><span class="sxs-lookup"><span data-stu-id="f9ea4-131">What can they do with your app?</span></span> <span data-ttu-id="f9ea4-132">Какое значение можно перенести?</span><span class="sxs-lookup"><span data-stu-id="f9ea4-132">What value can you bring to them?</span></span>
* <span data-ttu-id="f9ea4-133">**Что делать дальше.**</span><span class="sxs-lookup"><span data-stu-id="f9ea4-133">**What should they do next.**</span></span> <span data-ttu-id="f9ea4-134">Пригласите их, чтобы испытать команду или взаимодействовать с приложением каким бы то ни было способом.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="f9ea4-135">Сообщения уведомления</span><span class="sxs-lookup"><span data-stu-id="f9ea4-135">Notification messages</span></span>

<span data-ttu-id="f9ea4-136">При использовании упреждающего обмена сообщениями для отправки уведомлений необходимо убедиться, что у пользователей есть четко настроенный путь для выполнения общих действий на основе уведомления, и четко понимать, почему возникло уведомление.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="f9ea4-137">К хорошим сообщениям уведомления обычно относятся:</span><span class="sxs-lookup"><span data-stu-id="f9ea4-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="f9ea4-138">**Что случилось.**</span><span class="sxs-lookup"><span data-stu-id="f9ea4-138">**What happened.**</span></span> <span data-ttu-id="f9ea4-139">Четкое указание того, что произошло с причиной уведомления.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="f9ea4-140">**Что случилось.**</span><span class="sxs-lookup"><span data-stu-id="f9ea4-140">**What it happened to.**</span></span> <span data-ttu-id="f9ea4-141">Должно быть ясно, какие элементы/вещи были обновлены, чтобы получить уведомление.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="f9ea4-142">**Кто это сделал.**</span><span class="sxs-lookup"><span data-stu-id="f9ea4-142">**Who did it.**</span></span> <span data-ttu-id="f9ea4-143">Кто потратил действие, вызвавшее отправку уведомления.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="f9ea4-144">**Что они могут сделать.**</span><span class="sxs-lookup"><span data-stu-id="f9ea4-144">**What they can do about it.**</span></span> <span data-ttu-id="f9ea4-145">Облегчить пользователям выполнение действий в соответствии с вашими уведомлениями.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="f9ea4-146">**Как они могут отказаться.** Необходимо указать путь для пользователей, чтобы отказаться от дополнительных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="f9ea4-147">Получение необходимых сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="f9ea4-147">Obtain necessary user information</span></span>

<span data-ttu-id="f9ea4-148">Боты может создавать новые беседы с отдельным пользователем Microsoft Teams, получая *уникальный идентификатор* пользователя и *идентификатор клиента.*</span><span class="sxs-lookup"><span data-stu-id="f9ea4-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user’s *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="f9ea4-149">Эти значения можно получить с помощью одного из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="f9ea4-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="f9ea4-150">[Получение списка команд](../get-teams-context.md#fetching-the-roster-or-user-profile) на канале, в котором установлено приложение.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-150">By [fetching the team roster](../get-teams-context.md#fetching-the-roster-or-user-profile) from a channel your app is installed in.</span></span>
* <span data-ttu-id="f9ea4-151">Путем их кэширования, когда пользователь [взаимодействует с программой Bot в канале](./channel-and-group-conversations.md).</span><span class="sxs-lookup"><span data-stu-id="f9ea4-151">By caching them when a user [interacts with your bot in a channel](./channel-and-group-conversations.md).</span></span>
* <span data-ttu-id="f9ea4-152">Когда пользователи [@mentioned в канале беседы](./channel-and-group-conversations.md#retrieving-mentions) , участником Bot является.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-152">When a users is [@mentioned in a channel conversation](./channel-and-group-conversations.md#retrieving-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="f9ea4-153">Путем их кэширования при [получении `conversationUpdate` ](./subscribe-to-conversation-events.md#team-members-added) события при установке приложения в личную область или добавлении новых участников в канал или группу чата.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-153">By caching them when you [receive the `conversationUpdate`](./subscribe-to-conversation-events.md#team-members-added) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="f9ea4-154">Заактивная установка приложения с помощью Graph</span><span class="sxs-lookup"><span data-stu-id="f9ea4-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="f9ea4-155">Активная установка приложений с помощью Graph в настоящее время находится на стадии бета-тестирования.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="f9ea4-156">Иногда это может потребоваться для упреждающего сообщения пользователей, которые ранее не устанавливали приложение или не работали с ним.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="f9ea4-157">Например, вы хотите использовать [Communicator компании](~/samples/app-templates.md#company-communicator) для отправки сообщений во всю организацию.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="f9ea4-158">В этом сценарии можно использовать API Graph для профилактической установки приложения для пользователей, а затем кэшировать необходимые значения из события, которое `conversationUpdate` получит ваше приложение после установки.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="f9ea4-159">Вы можете устанавливать только приложения, которые находятся в каталоге организационных приложений или в магазине приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="f9ea4-160">Подробные сведения приведены в [статье Установка приложений для пользователей](/graph/teams-proactive-messaging) в документации Graph.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="f9ea4-161">Кроме того, существует [пример в .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span><span class="sxs-lookup"><span data-stu-id="f9ea4-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="f9ea4-162">Примеры</span><span class="sxs-lookup"><span data-stu-id="f9ea4-162">Examples</span></span>

<span data-ttu-id="f9ea4-163">Перед созданием новой беседы с помощью REST API обязательно проверьте подлинность и наличие маркера носителя.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span> <span data-ttu-id="f9ea4-164">`members.id` Поле в расположенном ниже объекте является уникальным в сочетании с пользователем.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-164">The `members.id` field in the object below is unique to the combination of your bot and a user.</span></span> <span data-ttu-id="f9ea4-165">Вы не можете получить его с помощью любого другого метода, чем описано выше.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-165">You cannot obtain it via any other method than those outlined above.</span></span>

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

<span data-ttu-id="f9ea4-166">Необходимо указать идентификатор пользователя и идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-166">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="f9ea4-167">Если вызов завершается успешно, API возвращает следующий объект Response.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-167">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="f9ea4-168">Этот идентификатор является уникальным ИДЕНТИФИКАТОРом беседы личного чата.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-168">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="f9ea4-169">Сохраните это значение и повторно используйте его для последующего взаимодействия с пользователем.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-169">Please store this value and reuse it for future interactions with the user.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="f9ea4-170">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="f9ea4-170">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="f9ea4-171">В этом примере используется пакет NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .</span><span class="sxs-lookup"><span data-stu-id="f9ea4-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

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

# <a name="javascripttabjavascript"></a>[<span data-ttu-id="f9ea4-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f9ea4-172">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="f9ea4-173">В этом примере используется пакет NPM [ботбуилдер – Teams](https://www.npmjs.com/package/botbuilder-teams) .</span><span class="sxs-lookup"><span data-stu-id="f9ea4-173">This example uses the [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) npm package.</span></span>

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

# <a name="pythontabpython"></a>[<span data-ttu-id="f9ea4-174">Python</span><span class="sxs-lookup"><span data-stu-id="f9ea4-174">Python</span></span>](#tab/python)

```python
async def _send_proactive_message():
  for conversation_reference in CONVERSATION_REFERENCES.values():
    return await ADAPTER.continue_conversation(APP_ID, conversation_reference,
      lambda turn_context: turn_context.send_activity("proactive hello")
    )

```

---

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="f9ea4-175">Создание беседы канала</span><span class="sxs-lookup"><span data-stu-id="f9ea4-175">Creating a channel conversation</span></span>

<span data-ttu-id="f9ea4-176">Добавленная командой Bot может отправляться в канал для создания новой цепочки ответа.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-176">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="f9ea4-177">Если вы используете пакет SDK для Teams. js, используйте `startReplyChain()` его, который предоставляет полностью заполненный адрес с правильным идентификатором действия и идентификатором диалога. Если вы используете C#, обратитесь к представленному ниже примеру.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-177">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="f9ea4-178">Кроме того, вы можете использовать REST API и отправить запрос POST [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ресурсу.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-178">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="f9ea4-179">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="f9ea4-179">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="f9ea4-180">В [этом примере](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)показан следующий фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="f9ea4-180">The following code snippet is from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs).</span></span>


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

# <a name="javascripttabjavascript"></a>[<span data-ttu-id="f9ea4-181">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f9ea4-181">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="f9ea4-182">В этом примере используется пакет NPM [ботбуилдер – Teams](https://www.npmjs.com/package/botbuilder-teams) .</span><span class="sxs-lookup"><span data-stu-id="f9ea4-182">This example uses the [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) npm package.</span></span> <span data-ttu-id="f9ea4-183">Приведенный ниже фрагмент кода относится к [теамсконверсатионбот. js](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js).</span><span class="sxs-lookup"><span data-stu-id="f9ea4-183">The following code snippet is from [teamsConversationBot.js](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js).</span></span>

[!code-javascript[messageAllMembersAsync](~/../botbuilder-samples/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js?range=115-134&highlight=13-15)]

# <a name="pythontabpython"></a>[<span data-ttu-id="f9ea4-184">Python</span><span class="sxs-lookup"><span data-stu-id="f9ea4-184">Python</span></span>](#tab/python)

[!code-python[message-all-members](~/../botbuilder-samples/samples/python/57.teams-conversation-bot/bots/teams_conversation_bot.py?range=101-135)]

---
