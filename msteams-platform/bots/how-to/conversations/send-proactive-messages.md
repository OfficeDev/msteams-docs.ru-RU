---
title: Отправлять активные сообщения
description: Описывает, как отправлять упреждающие сообщения с помощью бота Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
Keywords: отправка сообщения получить ID-ID-ID канала для беседы
ms.openlocfilehash: 25d5c6a1b51240c87ff0d8610a965d30f6b01095
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697055"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="a050f-104">Отправлять активные сообщения</span><span class="sxs-lookup"><span data-stu-id="a050f-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="a050f-105">Проактивное сообщение — это любое сообщение, отправленное ботом, которое не является ответом на запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="a050f-105">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="a050f-106">Это может включать такие сообщения, как:</span><span class="sxs-lookup"><span data-stu-id="a050f-106">This can include messages, such as:</span></span>

* <span data-ttu-id="a050f-107">Приветствия</span><span class="sxs-lookup"><span data-stu-id="a050f-107">Welcome messages</span></span>
* <span data-ttu-id="a050f-108">Уведомления</span><span class="sxs-lookup"><span data-stu-id="a050f-108">Notifications</span></span>
* <span data-ttu-id="a050f-109">Запланированные сообщения</span><span class="sxs-lookup"><span data-stu-id="a050f-109">Scheduled messages</span></span>

<span data-ttu-id="a050f-110">Для того чтобы бот отправил проактивное сообщение пользователю, групповому чату или группе, он должен иметь доступ к отправке сообщения.</span><span class="sxs-lookup"><span data-stu-id="a050f-110">For your bot to send a proactive message to a user, group chat, or team, it must have access to send the message.</span></span> <span data-ttu-id="a050f-111">Для группового чата или группы приложение с ботом должно быть сначала установлено в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="a050f-111">For a group chat or team, the app that contains your bot must be first installed in that location.</span></span> <span data-ttu-id="a050f-112">Вы можете активно устанавливать приложение с помощью [Microsoft Graph](#proactively-install-your-app-using-graph) в команде, если это необходимо, или использовать политику приложения для оттеснки приложений к группам и пользователям в клиенте. [](/microsoftteams/teams-custom-app-policies-and-settings)</span><span class="sxs-lookup"><span data-stu-id="a050f-112">You can [proactively install your app using Microsoft Graph](#proactively-install-your-app-using-graph) in a team, if required, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="a050f-113">Для пользователей ваше приложение либо должно быть установлено для пользователя, либо пользователь должен быть частью команды, в которой установлено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="a050f-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="a050f-114">Отправка упреждающего сообщения отличается от обычного сообщения.</span><span class="sxs-lookup"><span data-stu-id="a050f-114">Sending a proactive message is different from sending a regular message.</span></span> <span data-ttu-id="a050f-115">Нет активного `turnContext` использования для ответа.</span><span class="sxs-lookup"><span data-stu-id="a050f-115">There is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="a050f-116">Перед отправкой сообщения необходимо создать беседу.</span><span class="sxs-lookup"><span data-stu-id="a050f-116">You must create the conversation before sending the message.</span></span> <span data-ttu-id="a050f-117">Например, новый чат один к одному или новый поток беседы в канале.</span><span class="sxs-lookup"><span data-stu-id="a050f-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="a050f-118">Невозможно создать новый групповой чат или новый канал в команде с активной передачей сообщений.</span><span class="sxs-lookup"><span data-stu-id="a050f-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="a050f-119">**Отправка проактивного сообщения**</span><span class="sxs-lookup"><span data-stu-id="a050f-119">**To send a proactive message**</span></span>

1. <span data-ttu-id="a050f-120">При необходимости получите пользовательский [ИД, командный или канал.](#get-the-user-id-team-id-or-channel-id)</span><span class="sxs-lookup"><span data-stu-id="a050f-120">[Get the user ID, team ID, or channel ID](#get-the-user-id-team-id-or-channel-id), if required.</span></span>
1. <span data-ttu-id="a050f-121">[Создайте беседу,](#create-the-conversation)если потребуется.</span><span class="sxs-lookup"><span data-stu-id="a050f-121">[Create the conversation](#create-the-conversation), if required.</span></span>
1. <span data-ttu-id="a050f-122">[Получите ID беседы](#get-the-conversation-id).</span><span class="sxs-lookup"><span data-stu-id="a050f-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="a050f-123">[Отправка сообщения](#send-the-message).</span><span class="sxs-lookup"><span data-stu-id="a050f-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="a050f-124">Для эффективного использования упреждающих сообщений см. [в переупреждающихся практиках для активного обмена сообщениями.](#best-practices-for-proactive-messaging)</span><span class="sxs-lookup"><span data-stu-id="a050f-124">For using proactive messages effectively, see [best practices for proactive messaging](#best-practices-for-proactive-messaging).</span></span> <span data-ttu-id="a050f-125">Для определенных сценариев необходимо активно установить приложение с [помощью Graph.](#proactively-install-your-app-using-graph)</span><span class="sxs-lookup"><span data-stu-id="a050f-125">For certain scenarios, you must [proactively install your app using Graph](#proactively-install-your-app-using-graph).</span></span> <span data-ttu-id="a050f-126">Фрагменты кода в разделе [примеры](#samples) для создания беседы один к одному.</span><span class="sxs-lookup"><span data-stu-id="a050f-126">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="a050f-127">Полные рабочие примеры для бесед и групп или каналов см. в [примере кода.](#code-sample)</span><span class="sxs-lookup"><span data-stu-id="a050f-127">For complete working samples for both one-to-one conversations and groups or channels, see [code sample](#code-sample).</span></span>

## <a name="get-the-user-id-team-id-or-channel-id"></a><span data-ttu-id="a050f-128">Получите пользовательский ИД, командный или каналный ИД</span><span class="sxs-lookup"><span data-stu-id="a050f-128">Get the user ID, team ID or channel ID</span></span>

<span data-ttu-id="a050f-129">Чтобы создать новый поток беседы или беседы в канале, необходимо иметь правильный ID.</span><span class="sxs-lookup"><span data-stu-id="a050f-129">To create a new conversation or conversation thread in a channel, you must have the correct ID.</span></span> <span data-ttu-id="a050f-130">Вы можете получить или получить этот ID с помощью любого из следующих ниже.</span><span class="sxs-lookup"><span data-stu-id="a050f-130">You can receive or retrieve this ID using any of the following:</span></span>

* <span data-ttu-id="a050f-131">Когда ваше приложение установлено в любом конкретном контексте, вы получаете [ `onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="a050f-131">When your app is installed in any particular context, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="a050f-132">При добавлении нового пользователя в контекст, в котором установлено приложение, вы получаете [ `onMembersAdded` действие.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="a050f-132">When a new user is added to a context where your app is installed, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="a050f-133">Вы можете получить [список каналов](~/bots/how-to/get-teams-context.md) в команде, где установлено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="a050f-133">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team where your app is installed.</span></span>
* <span data-ttu-id="a050f-134">Вы можете получить [список членов группы,](~/bots/how-to/get-teams-context.md) в которой установлено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="a050f-134">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team where your app is installed.</span></span>
* <span data-ttu-id="a050f-135">Каждое действие, получаемые ботом, должно содержать необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="a050f-135">Every activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="a050f-136">Независимо от того, как вы получаете информацию, необходимо сохранить или создать `tenantId` `userId` новый `channelId` разговор.</span><span class="sxs-lookup"><span data-stu-id="a050f-136">Regardless of how you get the information, you must store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="a050f-137">Вы также можете использовать этот поток для создания нового потока беседы в общем или по умолчанию `teamId` канале группы.</span><span class="sxs-lookup"><span data-stu-id="a050f-137">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="a050f-138">Уникальный `userId` для вашего бот-ИД и определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="a050f-138">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="a050f-139">Нельзя повторно использовать между `userId` ботами.</span><span class="sxs-lookup"><span data-stu-id="a050f-139">You cannot reuse the `userId` between bots.</span></span> <span data-ttu-id="a050f-140">`channelId`Глобальный.</span><span class="sxs-lookup"><span data-stu-id="a050f-140">The `channelId` is global.</span></span> <span data-ttu-id="a050f-141">Однако перед отправкой проактивного сообщения на канал необходимо установить бот в команде.</span><span class="sxs-lookup"><span data-stu-id="a050f-141">However, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

<span data-ttu-id="a050f-142">После получения сведений о пользователе или канале необходимо создать беседу.</span><span class="sxs-lookup"><span data-stu-id="a050f-142">After you have the user or channel information, you must create the conversation.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="a050f-143">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="a050f-143">Create the conversation</span></span>

<span data-ttu-id="a050f-144">Вы должны создать беседу, если она не существует или вы не знаете `conversationId` .</span><span class="sxs-lookup"><span data-stu-id="a050f-144">You must create the conversation if it does not exist or you do not know the `conversationId`.</span></span> <span data-ttu-id="a050f-145">Необходимо создать беседу только один раз и сохранить `conversationId` значение или `conversationReference` объект.</span><span class="sxs-lookup"><span data-stu-id="a050f-145">You must only create the conversation once and store the `conversationId` value or `conversationReference` object.</span></span>

<span data-ttu-id="a050f-146">После создания беседы необходимо получить ID беседы.</span><span class="sxs-lookup"><span data-stu-id="a050f-146">After the conversation is created, you must get the conversation ID.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="a050f-147">Получить ID беседы</span><span class="sxs-lookup"><span data-stu-id="a050f-147">Get the conversation ID</span></span>

<span data-ttu-id="a050f-148">Используйте объект `conversationReference` или `conversationId` отправить `tenantId` сообщение.</span><span class="sxs-lookup"><span data-stu-id="a050f-148">Use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="a050f-149">Этот ID можно получить, создав беседу или храня ее из любого действия, отправленного вам из этого контекста.</span><span class="sxs-lookup"><span data-stu-id="a050f-149">You can get this ID by either creating the conversation or storing it from any activity sent to you from that context.</span></span> <span data-ttu-id="a050f-150">Храните этот ID для справки.</span><span class="sxs-lookup"><span data-stu-id="a050f-150">Store this ID for reference.</span></span>

<span data-ttu-id="a050f-151">После получения соответствующей адресной информации можно отправить сообщение.</span><span class="sxs-lookup"><span data-stu-id="a050f-151">After you get the appropriate address information, you can send your message.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="a050f-152">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="a050f-152">Send the message</span></span>

<span data-ttu-id="a050f-153">Если вы используете SDK, для отправки сообщения необходимо использовать метод и прямой вызов `continueConversation` `conversationId` `tenantId` API.</span><span class="sxs-lookup"><span data-stu-id="a050f-153">If you are using the SDK, you must use the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call to send the message.</span></span> <span data-ttu-id="a050f-154">Чтобы успешно отправить сообщение, необходимо правильно `conversationParameters` установить.</span><span class="sxs-lookup"><span data-stu-id="a050f-154">You must set the `conversationParameters` correctly to successfully send your message.</span></span>

<span data-ttu-id="a050f-155">Теперь, когда вы отправили проактивное сообщение, вы должны следовать этим лучшим практикам, отправляя проактивные сообщения для улучшения обмена информацией между пользователями и ботом.</span><span class="sxs-lookup"><span data-stu-id="a050f-155">Now that you have sent the proactive message, you must follow these best practices while sending proactive messages for better information exchange between users and the bot.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="a050f-156">Лучшие практики для активного обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a050f-156">Best practices for proactive messaging</span></span>

<span data-ttu-id="a050f-157">Отправка активных сообщений пользователям — это очень эффективный способ общения с пользователями.</span><span class="sxs-lookup"><span data-stu-id="a050f-157">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="a050f-158">Однако с их точки зрения это сообщение может отображаться совершенно незащищенным, и в случае приветствия сообщений это первый раз, когда они взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="a050f-158">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="a050f-159">Поэтому очень важно использовать упреждающий обмен сообщениями, а не нежелательной почты пользователей, а также предоставлять достаточно информации, чтобы пользователи могли понять, почему они получают сообщения.</span><span class="sxs-lookup"><span data-stu-id="a050f-159">Therefore, it is very important to use proactive messaging sparingly, not spam your users, and provide enough information to let users understand why they are receiving the messages.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="a050f-160">Приветствия</span><span class="sxs-lookup"><span data-stu-id="a050f-160">Welcome messages</span></span>

<span data-ttu-id="a050f-161">Если для отправки приветствия пользователю используется проактивный обмен сообщениями, нет контекста, по которым пользователи получают сообщение.</span><span class="sxs-lookup"><span data-stu-id="a050f-161">When proactive messaging is used to send a welcome message to a user, there is no context for why the users receive the message.</span></span> <span data-ttu-id="a050f-162">Кроме того, пользователи впервые взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="a050f-162">This is also the first time users interact with your app.</span></span> <span data-ttu-id="a050f-163">Это возможность создать хорошее первое впечатление.</span><span class="sxs-lookup"><span data-stu-id="a050f-163">It is an opportunity to create a good first impression.</span></span> <span data-ttu-id="a050f-164">Лучшие приветствия должны включать в себя:</span><span class="sxs-lookup"><span data-stu-id="a050f-164">The best welcome messages must include:</span></span>

* <span data-ttu-id="a050f-165">Почему пользователь получает сообщение: пользователю должно быть ясно, почему он получает сообщение.</span><span class="sxs-lookup"><span data-stu-id="a050f-165">Why a user is receiving the message: It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="a050f-166">Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен и кто его установил.</span><span class="sxs-lookup"><span data-stu-id="a050f-166">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and who installed it.</span></span>
* <span data-ttu-id="a050f-167">Что вы предлагаете. Пользователи должны быть в состоянии определить, что они могут сделать с вашим приложением и какое значение вы можете принести к ним.</span><span class="sxs-lookup"><span data-stu-id="a050f-167">What do you offer: Users must be able to identify what they can do with your app and what value can you bring to them.</span></span>
* <span data-ttu-id="a050f-168">Что они должны делать дальше: предложить пользователям опробовать команду или взаимодействовать с приложением.</span><span class="sxs-lookup"><span data-stu-id="a050f-168">What should they do next: Invite users to try out a command, or interact with your app.</span></span>

<span data-ttu-id="a050f-169">Неудовлетворительные приветствия могут привести к блокировке бота пользователями.</span><span class="sxs-lookup"><span data-stu-id="a050f-169">Poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="a050f-170">Напишите в точку и ясно приветствуя сообщения.</span><span class="sxs-lookup"><span data-stu-id="a050f-170">Write to the point and clear welcome messages.</span></span> <span data-ttu-id="a050f-171">Итерировать на приветствие сообщений, если они не имеют желаемого эффекта.</span><span class="sxs-lookup"><span data-stu-id="a050f-171">Iterate on the welcome messages if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="a050f-172">Уведомления</span><span class="sxs-lookup"><span data-stu-id="a050f-172">Notification messages</span></span>

<span data-ttu-id="a050f-173">Чтобы отправлять уведомления с помощью активного обмена сообщениями, убедитесь, что у пользователей есть четкий путь к общим действиям на основе вашего уведомления.</span><span class="sxs-lookup"><span data-stu-id="a050f-173">To send notifications using proactive messaging, ensure your users have a clear path to take common actions based on your notification.</span></span> <span data-ttu-id="a050f-174">Убедитесь, что у пользователей есть четкое представление о том, почему они получили уведомление.</span><span class="sxs-lookup"><span data-stu-id="a050f-174">Ensure users have a clear understanding of why they have received a notification.</span></span> <span data-ttu-id="a050f-175">Хорошие сообщения уведомлений обычно включают в себя следующие:</span><span class="sxs-lookup"><span data-stu-id="a050f-175">Good notification messages generally include the following:</span></span>

* <span data-ttu-id="a050f-176">Что произошло: четкое указание на то, что стало причиной уведомления.</span><span class="sxs-lookup"><span data-stu-id="a050f-176">What happened: A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="a050f-177">Каков был результат: необходимо четко знать, какой элемент был обновлен, чтобы вызвать уведомление.</span><span class="sxs-lookup"><span data-stu-id="a050f-177">What was the result: It must be clear what item was updated to cause the notification.</span></span>
* <span data-ttu-id="a050f-178">Кто или что вызвало его: кто или какие действия привели к отправлению уведомления.</span><span class="sxs-lookup"><span data-stu-id="a050f-178">Who or what triggered it: Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="a050f-179">Что пользователи могут сделать в ответ: у вас будет легко принимать меры на основе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a050f-179">What can users do in response: Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="a050f-180">Как пользователи могут отказаться от этого. Необходимо предоставить пользователям путь к отказу от дополнительных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a050f-180">How can users opt-out: You must provide a path for users to opt-out of additional notifications.</span></span>

<span data-ttu-id="a050f-181">Для отправки сообщений большой группе пользователей, например в организацию, упреждайте установку приложения с помощью Graph.</span><span class="sxs-lookup"><span data-stu-id="a050f-181">To send messages to a large group of users, for example to your organization, proactively install your app using Graph.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="a050f-182">Запланированные сообщения</span><span class="sxs-lookup"><span data-stu-id="a050f-182">Scheduled messages</span></span>

<span data-ttu-id="a050f-183">При использовании активных сообщений для отправки запланированных сообщений пользователям убедитесь, что часовой пояс обновляется до часового пояса.</span><span class="sxs-lookup"><span data-stu-id="a050f-183">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="a050f-184">Это обеспечивает доставку сообщений пользователям в соответствующее время.</span><span class="sxs-lookup"><span data-stu-id="a050f-184">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="a050f-185">Расписание сообщений обычно включает в себя:</span><span class="sxs-lookup"><span data-stu-id="a050f-185">Schedule messages generally include:</span></span>

* <span data-ttu-id="a050f-186">**Почему пользователь получает** сообщение. Чтобы пользователям было легко понять причину, по которой они получают сообщение.</span><span class="sxs-lookup"><span data-stu-id="a050f-186">**Why is the user receiving the message**: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="a050f-187">**Что может сделать пользователь далее.** Пользователи могут принять необходимые действия на основе контента сообщения.</span><span class="sxs-lookup"><span data-stu-id="a050f-187">**What can user do next**: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="a050f-188">Активная установка приложения с помощью Graph</span><span class="sxs-lookup"><span data-stu-id="a050f-188">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="a050f-189">Активная установка приложений с помощью Graph в настоящее время находится в бета-версии.</span><span class="sxs-lookup"><span data-stu-id="a050f-189">Proactively installing apps using Graph is currently in beta.</span></span>

<span data-ttu-id="a050f-190">Активно сообщайте пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="a050f-190">Proactively message users that have previously not installed or interacted with your app.</span></span> <span data-ttu-id="a050f-191">Например, вы хотите использовать коммуникатор [компании](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации.</span><span class="sxs-lookup"><span data-stu-id="a050f-191">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="a050f-192">В этом случае для активной установки приложения для пользователей можно использовать API Graph.</span><span class="sxs-lookup"><span data-stu-id="a050f-192">In this case, you can use the Graph API to proactively install your app for your users.</span></span> <span data-ttu-id="a050f-193">Кэшйте необходимые значения из события, которое `conversationUpdate` ваше приложение получает при установке.</span><span class="sxs-lookup"><span data-stu-id="a050f-193">Cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="a050f-194">Можно установить только приложения, которые находятся в каталоге организационных приложений или в Магазине приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="a050f-194">You can only install apps that are in your organizational app catalog or the Teams App Store.</span></span>

<span data-ttu-id="a050f-195">Об [установке приложений для пользователей см. в](/graph/api/userteamwork-post-installedapps) документации Graph, а также в упреждающих установках ботов и обмена сообщениями [в Teams with Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="a050f-195">See [install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [proactive bot installation and messaging in Teams with Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="a050f-196">На платформе GitHub также имеется пример фреймворка [Microsoft.NET.](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)</span><span class="sxs-lookup"><span data-stu-id="a050f-196">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="samples"></a><span data-ttu-id="a050f-197">Примеры</span><span class="sxs-lookup"><span data-stu-id="a050f-197">Samples</span></span>

<span data-ttu-id="a050f-198">В следующем коде показан простой пример кода, который активно устанавливает приложение с помощью Graph:</span><span class="sxs-lookup"><span data-stu-id="a050f-198">The following code shows a simple code sample that proactively installs your app using Graph:</span></span>

# <a name="c"></a>[<span data-ttu-id="a050f-199">C#</span><span class="sxs-lookup"><span data-stu-id="a050f-199">C#</span></span>](#tab/dotnet)

```csharp
[Route("api/notify")]
[ApiController]
public class NotifyController : ControllerBase
{
    private readonly IBotFrameworkHttpAdapter _adapter;
    private readonly string _appId;
    private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

    public NotifyController(IBotFrameworkHttpAdapter adapter, IConfiguration configuration, ConcurrentDictionary<string, ConversationReference> conversationReferences)
    {
        _adapter = adapter;
        _conversationReferences = conversationReferences;
        _appId = configuration["MicrosoftAppId"] ?? string.Empty;
    }

    public async Task<IActionResult> Get()
    {
        foreach (var conversationReference in _conversationReferences.Values)
        {
            await ((BotAdapter)_adapter).ContinueConversationAsync(_appId, conversationReference, BotCallback, default(CancellationToken));
        }
        
        // Let the caller know proactive messages have been sent
        return new ContentResult()
        {
            Content = "<html><body><h1>Proactive messages have been sent.</h1></body></html>",
            ContentType = "text/html",
            StatusCode = (int)HttpStatusCode.OK,
        };
    }

    private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
    {
        // If you encounter permission-related errors when sending this message, see
        // https://aka.ms/BotTrustServiceUrl
        await turnContext.SendActivityAsync("proactive hello");
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="a050f-200">TypeScript</span><span class="sxs-lookup"><span data-stu-id="a050f-200">TypeScript</span></span>](#tab/typescript)

```javascript

async messageAllMembersAsync(context) {
    const members = await this.getPagedMembers(context);

    members.forEach(async (teamMember) => {
        const message = MessageFactory.text('Hello ${ teamMember.givenName } ${ teamMember.surname }. I\'m a Teams conversation bot.');

        var ref = TurnContext.getConversationReference(context.activity);
        ref.user = teamMember;

        await context.adapter.createConversation(ref,
            async (t1) => {
                const ref2 = TurnContext.getConversationReference(t1.activity);
                await t1.adapter.continueConversation(ref2, async (t2) => {
                    await t2.sendActivity(message);
                });
            });
    });

    await context.sendActivity(MessageFactory.text('All messages have been sent.'));
}
```

# <a name="python"></a>[<span data-ttu-id="a050f-201">Python</span><span class="sxs-lookup"><span data-stu-id="a050f-201">Python</span></span>](#tab/python)

```python
async def _message_all_members(self, turn_context: TurnContext):
    team_members = await self._get_paged_members(turn_context)

    for member in team_members:
        conversation_reference = TurnContext.get_conversation_reference(
            turn_context.activity
        )

        conversation_parameters = ConversationParameters(
            is_group=False,
            bot=turn_context.activity.recipient,
            members=[member],
            tenant_id=turn_context.activity.conversation.tenant_id,
        )

        async def get_ref(tc1):
            conversation_reference_inner = TurnContext.get_conversation_reference(
                tc1.activity
            )
            return await tc1.adapter.continue_conversation(
                conversation_reference_inner, send_message, self._app_id
            )

        async def send_message(tc2: TurnContext):
            return await tc2.send_activity(
                f"Hello {member.name}. I'm a Teams conversation bot."
            )

        await turn_context.adapter.create_conversation(
            conversation_reference, get_ref, conversation_parameters
        )

    await turn_context.send_activity(
        MessageFactory.text("All messages have been sent")
    )

```

# <a name="json"></a>[<span data-ttu-id="a050f-202">JSON</span><span class="sxs-lookup"><span data-stu-id="a050f-202">JSON</span></span>](#tab/json)

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

<span data-ttu-id="a050f-203">Необходимо предоставить пользовательский ИД и ИД клиента.</span><span class="sxs-lookup"><span data-stu-id="a050f-203">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="a050f-204">Если вызов удался, API возвращает следующий объект ответа:</span><span class="sxs-lookup"><span data-stu-id="a050f-204">If the call succeeds, the API returns the following response object:</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a><span data-ttu-id="a050f-205">Пример кода</span><span class="sxs-lookup"><span data-stu-id="a050f-205">Code sample</span></span>

<span data-ttu-id="a050f-206">В следующей таблице приводится простой пример кода, который включает основной поток беседы в приложение Teams и способ создания нового потока беседы в канале Teams:</span><span class="sxs-lookup"><span data-stu-id="a050f-206">The following table provides a simple code sample that incorporate basic conversation flow into a Teams application and how to create a new conversation thread in a channel in Teams:</span></span>

| <span data-ttu-id="a050f-207">Пример имени</span><span class="sxs-lookup"><span data-stu-id="a050f-207">Sample name</span></span>           | <span data-ttu-id="a050f-208">Описание</span><span class="sxs-lookup"><span data-stu-id="a050f-208">Description</span></span>                                                                      | <span data-ttu-id="a050f-209">.NET</span><span class="sxs-lookup"><span data-stu-id="a050f-209">.NET</span></span>    | <span data-ttu-id="a050f-210">Node.js</span><span class="sxs-lookup"><span data-stu-id="a050f-210">Node.js</span></span>   | <span data-ttu-id="a050f-211">Python</span><span class="sxs-lookup"><span data-stu-id="a050f-211">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="a050f-212">Основы беседы команд</span><span class="sxs-lookup"><span data-stu-id="a050f-212">Teams conversation basics</span></span>  | <span data-ttu-id="a050f-213">Демонстрирует основы бесед в Teams, в том числе отправку одно к одному упреждающих сообщений.</span><span class="sxs-lookup"><span data-stu-id="a050f-213">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="a050f-214">View</span><span class="sxs-lookup"><span data-stu-id="a050f-214">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="a050f-215">View</span><span class="sxs-lookup"><span data-stu-id="a050f-215">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="a050f-216">View</span><span class="sxs-lookup"><span data-stu-id="a050f-216">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="a050f-217">Запуск нового потока в канале</span><span class="sxs-lookup"><span data-stu-id="a050f-217">Start new thread in a channel</span></span>     | <span data-ttu-id="a050f-218">Демонстрирует создание нового потока в канале.</span><span class="sxs-lookup"><span data-stu-id="a050f-218">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="a050f-219">View</span><span class="sxs-lookup"><span data-stu-id="a050f-219">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="a050f-220">View</span><span class="sxs-lookup"><span data-stu-id="a050f-220">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="a050f-221">View</span><span class="sxs-lookup"><span data-stu-id="a050f-221">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a><span data-ttu-id="a050f-222">Дополнительный пример кода</span><span class="sxs-lookup"><span data-stu-id="a050f-222">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a050f-223">Teams proactive messaging code samples</span><span class="sxs-lookup"><span data-stu-id="a050f-223">Teams proactive messaging code samples</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a><span data-ttu-id="a050f-224">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="a050f-224">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a050f-225">Формат сообщений бота</span><span class="sxs-lookup"><span data-stu-id="a050f-225">Format your bot messages</span></span>](~/bots/how-to/format-your-bot-messages.md)
