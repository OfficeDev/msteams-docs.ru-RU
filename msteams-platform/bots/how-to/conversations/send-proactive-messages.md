---
title: Отправка упреждающих сообщений
description: Описывает, как отправлять упреждающие сообщения с помощью Microsoft Teams бота.
ms.topic: conceptual
ms.author: anclear
localization_priority: Normal
Keywords: отправка сообщения получить ID-ID-ID канала для беседы
ms.openlocfilehash: ae651ac94b1b092374f6fae284b67070036b561f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020921"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="1221a-104">Отправка упреждающих сообщений</span><span class="sxs-lookup"><span data-stu-id="1221a-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="1221a-105">Проактивное сообщение — это любое сообщение, отправленное ботом, которое не является ответом на запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="1221a-105">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="1221a-106">Это может включать такие сообщения, как:</span><span class="sxs-lookup"><span data-stu-id="1221a-106">This can include messages, such as:</span></span>

* <span data-ttu-id="1221a-107">Приветствия</span><span class="sxs-lookup"><span data-stu-id="1221a-107">Welcome messages</span></span>
* <span data-ttu-id="1221a-108">Уведомления</span><span class="sxs-lookup"><span data-stu-id="1221a-108">Notifications</span></span>
* <span data-ttu-id="1221a-109">Запланированные сообщения</span><span class="sxs-lookup"><span data-stu-id="1221a-109">Scheduled messages</span></span>

<span data-ttu-id="1221a-110">Для того чтобы бот отправил проактивное сообщение пользователю, групповому чату или группе, он должен иметь доступ к отправке сообщения.</span><span class="sxs-lookup"><span data-stu-id="1221a-110">For your bot to send a proactive message to a user, group chat, or team, it must have access to send the message.</span></span> <span data-ttu-id="1221a-111">Для группового чата или группы приложение с ботом должно быть сначала установлено в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="1221a-111">For a group chat or team, the app that contains your bot must be first installed in that location.</span></span> <span data-ttu-id="1221a-112">Вы можете активно устанавливать приложение с [помощью Microsoft Graph](#proactively-install-your-app-using-graph) в команде, если [](/microsoftteams/teams-custom-app-policies-and-settings) это необходимо, или использовать политику приложения, чтобы вытесдить приложения для групп и пользователей в клиенте.</span><span class="sxs-lookup"><span data-stu-id="1221a-112">You can [proactively install your app using Microsoft Graph](#proactively-install-your-app-using-graph) in a team, if required, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="1221a-113">Для пользователей ваше приложение либо должно быть установлено для пользователя, либо пользователь должен быть частью команды, в которой установлено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="1221a-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="1221a-114">Отправка упреждающего сообщения отличается от обычного сообщения.</span><span class="sxs-lookup"><span data-stu-id="1221a-114">Sending a proactive message is different from sending a regular message.</span></span> <span data-ttu-id="1221a-115">Нет активного `turnContext` использования для ответа.</span><span class="sxs-lookup"><span data-stu-id="1221a-115">There is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="1221a-116">Перед отправкой сообщения необходимо создать беседу.</span><span class="sxs-lookup"><span data-stu-id="1221a-116">You must create the conversation before sending the message.</span></span> <span data-ttu-id="1221a-117">Например, новый чат один к одному или новый поток беседы в канале.</span><span class="sxs-lookup"><span data-stu-id="1221a-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="1221a-118">Невозможно создать новый групповой чат или новый канал в команде с активной передачей сообщений.</span><span class="sxs-lookup"><span data-stu-id="1221a-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="1221a-119">**Отправка проактивного сообщения**</span><span class="sxs-lookup"><span data-stu-id="1221a-119">**To send a proactive message**</span></span>

1. <span data-ttu-id="1221a-120">При необходимости получите пользовательский [ИД, командный или канал.](#get-the-user-id-team-id-or-channel-id)</span><span class="sxs-lookup"><span data-stu-id="1221a-120">[Get the user ID, team ID, or channel ID](#get-the-user-id-team-id-or-channel-id), if required.</span></span>
1. <span data-ttu-id="1221a-121">[Создайте беседу,](#create-the-conversation)если потребуется.</span><span class="sxs-lookup"><span data-stu-id="1221a-121">[Create the conversation](#create-the-conversation), if required.</span></span>
1. <span data-ttu-id="1221a-122">[Получите ID беседы](#get-the-conversation-id).</span><span class="sxs-lookup"><span data-stu-id="1221a-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="1221a-123">[Отправка сообщения](#send-the-message).</span><span class="sxs-lookup"><span data-stu-id="1221a-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="1221a-124">Фрагменты кода в разделе [примеры](#samples) для создания беседы один к одному.</span><span class="sxs-lookup"><span data-stu-id="1221a-124">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="1221a-125">Ссылки на полные рабочие примеры для бесед и групп или каналов см. в [примере кода.](#code-sample)</span><span class="sxs-lookup"><span data-stu-id="1221a-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code sample](#code-sample).</span></span>

<span data-ttu-id="1221a-126">Для эффективного использования упреждающих сообщений см. [в переупреждающихся практиках для активного обмена сообщениями.](#best-practices-for-proactive-messaging)</span><span class="sxs-lookup"><span data-stu-id="1221a-126">For using proactive messages effectively, see [best practices for proactive messaging](#best-practices-for-proactive-messaging).</span></span> <span data-ttu-id="1221a-127">Для определенных сценариев необходимо активно установить приложение с помощью [Graph.](#proactively-install-your-app-using-graph)</span><span class="sxs-lookup"><span data-stu-id="1221a-127">For certain scenarios, you must [proactively install your app using Graph](#proactively-install-your-app-using-graph).</span></span> <span data-ttu-id="1221a-128">Фрагменты кода в разделе [примеры](#samples) для создания беседы один к одному.</span><span class="sxs-lookup"><span data-stu-id="1221a-128">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="1221a-129">Полные рабочие примеры для бесед и групп или каналов см. в [примере кода.](#code-sample)</span><span class="sxs-lookup"><span data-stu-id="1221a-129">For complete working samples for both one-to-one conversations and groups or channels, see [code sample](#code-sample).</span></span>

## <a name="get-the-user-id-team-id-or-channel-id"></a><span data-ttu-id="1221a-130">Получите пользовательский ИД, командный или каналный ИД</span><span class="sxs-lookup"><span data-stu-id="1221a-130">Get the user ID, team ID or channel ID</span></span>

<span data-ttu-id="1221a-131">Чтобы создать новый поток беседы или беседы в канале, необходимо иметь правильный ID.</span><span class="sxs-lookup"><span data-stu-id="1221a-131">To create a new conversation or conversation thread in a channel, you must have the correct ID.</span></span> <span data-ttu-id="1221a-132">Вы можете получить или получить этот ID с помощью любого из следующих ниже.</span><span class="sxs-lookup"><span data-stu-id="1221a-132">You can receive or retrieve this ID using any of the following:</span></span>

* <span data-ttu-id="1221a-133">Когда ваше приложение установлено в любом конкретном контексте, вы получаете [ `onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="1221a-133">When your app is installed in any particular context, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="1221a-134">При добавлении нового пользователя в контекст, в котором установлено приложение, вы получаете [ `onMembersAdded` действие.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="1221a-134">When a new user is added to a context where your app is installed, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="1221a-135">Вы можете получить [список каналов](~/bots/how-to/get-teams-context.md) в команде, где установлено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="1221a-135">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team where your app is installed.</span></span>
* <span data-ttu-id="1221a-136">Вы можете получить [список членов группы,](~/bots/how-to/get-teams-context.md) в которой установлено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="1221a-136">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team where your app is installed.</span></span>
* <span data-ttu-id="1221a-137">Каждое действие, получаемые ботом, должно содержать необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="1221a-137">Every activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="1221a-138">Независимо от того, как вы получаете информацию, необходимо сохранить или создать `tenantId` `userId` новый `channelId` разговор.</span><span class="sxs-lookup"><span data-stu-id="1221a-138">Regardless of how you get the information, you must store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="1221a-139">Вы также можете использовать этот поток для создания нового потока беседы в общем или по умолчанию `teamId` канале группы.</span><span class="sxs-lookup"><span data-stu-id="1221a-139">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="1221a-140">Уникальный `userId` для вашего бот-ИД и определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="1221a-140">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="1221a-141">Нельзя повторно использовать между `userId` ботами.</span><span class="sxs-lookup"><span data-stu-id="1221a-141">You cannot reuse the `userId` between bots.</span></span> <span data-ttu-id="1221a-142">`channelId`Глобальный.</span><span class="sxs-lookup"><span data-stu-id="1221a-142">The `channelId` is global.</span></span> <span data-ttu-id="1221a-143">Однако перед отправкой проактивного сообщения на канал необходимо установить бот в команде.</span><span class="sxs-lookup"><span data-stu-id="1221a-143">However, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

<span data-ttu-id="1221a-144">После получения сведений о пользователе или канале необходимо создать беседу.</span><span class="sxs-lookup"><span data-stu-id="1221a-144">After you have the user or channel information, you must create the conversation.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="1221a-145">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="1221a-145">Create the conversation</span></span>

<span data-ttu-id="1221a-146">Вы должны создать беседу, если она не существует или вы не знаете `conversationId` .</span><span class="sxs-lookup"><span data-stu-id="1221a-146">You must create the conversation if it does not exist or you do not know the `conversationId`.</span></span> <span data-ttu-id="1221a-147">Необходимо создать беседу только один раз и сохранить `conversationId` значение или `conversationReference` объект.</span><span class="sxs-lookup"><span data-stu-id="1221a-147">You must only create the conversation once and store the `conversationId` value or `conversationReference` object.</span></span>

<span data-ttu-id="1221a-148">После создания беседы необходимо получить ID беседы.</span><span class="sxs-lookup"><span data-stu-id="1221a-148">After the conversation is created, you must get the conversation ID.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="1221a-149">Получить ID беседы</span><span class="sxs-lookup"><span data-stu-id="1221a-149">Get the conversation ID</span></span>

<span data-ttu-id="1221a-150">Используйте объект `conversationReference` или `conversationId` отправить `tenantId` сообщение.</span><span class="sxs-lookup"><span data-stu-id="1221a-150">Use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="1221a-151">Этот ID можно получить, создав беседу или храня ее из любого действия, отправленного вам из этого контекста.</span><span class="sxs-lookup"><span data-stu-id="1221a-151">You can get this ID by either creating the conversation or storing it from any activity sent to you from that context.</span></span> <span data-ttu-id="1221a-152">Храните этот ID для справки.</span><span class="sxs-lookup"><span data-stu-id="1221a-152">Store this ID for reference.</span></span>

<span data-ttu-id="1221a-153">После получения соответствующей адресной информации можно отправить сообщение.</span><span class="sxs-lookup"><span data-stu-id="1221a-153">After you get the appropriate address information, you can send your message.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="1221a-154">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="1221a-154">Send the message</span></span>

<span data-ttu-id="1221a-155">Теперь, когда у вас есть правильные сведения о адресе, вы можете отправить свое сообщение.</span><span class="sxs-lookup"><span data-stu-id="1221a-155">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="1221a-156">Если вы используете SDK, вы сделаете это с помощью метода, а также для прямого `continueConversation` `conversationId` вызова `tenantId` API.</span><span class="sxs-lookup"><span data-stu-id="1221a-156">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="1221a-157">Чтобы успешно отправить сообщение, необходимо правильно `conversationParameters` установить.</span><span class="sxs-lookup"><span data-stu-id="1221a-157">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="1221a-158">См. [раздел примеры](#samples) или используйте один из примеров, перечисленных в [примере](#code-sample) кода.</span><span class="sxs-lookup"><span data-stu-id="1221a-158">See the [samples](#samples) section or use one of the samples listed in the [code sample](#code-sample) section.</span></span>

<span data-ttu-id="1221a-159">Если вы используете SDK, для отправки сообщения необходимо использовать метод и прямой вызов `continueConversation` `conversationId` `tenantId` API.</span><span class="sxs-lookup"><span data-stu-id="1221a-159">If you are using the SDK, you must use the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call to send the message.</span></span> <span data-ttu-id="1221a-160">Чтобы успешно отправить сообщение, необходимо правильно `conversationParameters` установить.</span><span class="sxs-lookup"><span data-stu-id="1221a-160">You must set the `conversationParameters` correctly to successfully send your message.</span></span>

<span data-ttu-id="1221a-161">Теперь, когда вы отправили проактивное сообщение, вы должны следовать этим лучшим практикам, отправляя проактивные сообщения для улучшения обмена информацией между пользователями и ботом.</span><span class="sxs-lookup"><span data-stu-id="1221a-161">Now that you have sent the proactive message, you must follow these best practices while sending proactive messages for better information exchange between users and the bot.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="1221a-162">Лучшие практики для активного обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="1221a-162">Best practices for proactive messaging</span></span>

<span data-ttu-id="1221a-163">Отправка активных сообщений пользователям — это очень эффективный способ общения с пользователями.</span><span class="sxs-lookup"><span data-stu-id="1221a-163">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="1221a-164">Однако с их точки зрения это сообщение может отображаться совершенно незащищенным, и в случае приветствия сообщений это первый раз, когда они взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="1221a-164">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="1221a-165">Поэтому очень важно использовать упреждающий обмен сообщениями, а не нежелательной почты пользователей, а также предоставлять достаточно информации, чтобы пользователи могли понять, почему они получают сообщения.</span><span class="sxs-lookup"><span data-stu-id="1221a-165">Therefore, it is very important to use proactive messaging sparingly, not spam your users, and provide enough information to let users understand why they are receiving the messages.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="1221a-166">Приветствия</span><span class="sxs-lookup"><span data-stu-id="1221a-166">Welcome messages</span></span>

<span data-ttu-id="1221a-167">Если для отправки приветствия пользователю используется проактивный обмен сообщениями, нет контекста, по которым пользователи получают сообщение.</span><span class="sxs-lookup"><span data-stu-id="1221a-167">When proactive messaging is used to send a welcome message to a user, there is no context for why the users receive the message.</span></span> <span data-ttu-id="1221a-168">Кроме того, пользователи впервые взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="1221a-168">This is also the first time users interact with your app.</span></span> <span data-ttu-id="1221a-169">Это возможность создать хорошее первое впечатление.</span><span class="sxs-lookup"><span data-stu-id="1221a-169">It is an opportunity to create a good first impression.</span></span> <span data-ttu-id="1221a-170">Лучшие приветствия должны включать в себя:</span><span class="sxs-lookup"><span data-stu-id="1221a-170">The best welcome messages must include:</span></span>

* <span data-ttu-id="1221a-171">Почему пользователь получает сообщение: пользователю должно быть ясно, почему он получает сообщение.</span><span class="sxs-lookup"><span data-stu-id="1221a-171">Why a user is receiving the message: It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="1221a-172">Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен и кто его установил.</span><span class="sxs-lookup"><span data-stu-id="1221a-172">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and who installed it.</span></span>
* <span data-ttu-id="1221a-173">Что вы предлагаете. Пользователи должны быть в состоянии определить, что они могут сделать с вашим приложением и какое значение вы можете принести к ним.</span><span class="sxs-lookup"><span data-stu-id="1221a-173">What do you offer: Users must be able to identify what they can do with your app and what value can you bring to them.</span></span>
* <span data-ttu-id="1221a-174">Что они должны делать дальше: предложить пользователям опробовать команду или взаимодействовать с приложением.</span><span class="sxs-lookup"><span data-stu-id="1221a-174">What should they do next: Invite users to try out a command, or interact with your app.</span></span>

<span data-ttu-id="1221a-175">Неудовлетворительные приветствия могут привести к блокировке бота пользователями.</span><span class="sxs-lookup"><span data-stu-id="1221a-175">Poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="1221a-176">Напишите в точку и ясно приветствуя сообщения.</span><span class="sxs-lookup"><span data-stu-id="1221a-176">Write to the point and clear welcome messages.</span></span> <span data-ttu-id="1221a-177">Итерировать на приветствие сообщений, если они не имеют желаемого эффекта.</span><span class="sxs-lookup"><span data-stu-id="1221a-177">Iterate on the welcome messages if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="1221a-178">Уведомления</span><span class="sxs-lookup"><span data-stu-id="1221a-178">Notification messages</span></span>

<span data-ttu-id="1221a-179">Чтобы отправлять уведомления с помощью активного обмена сообщениями, убедитесь, что у пользователей есть четкий путь к общим действиям на основе вашего уведомления.</span><span class="sxs-lookup"><span data-stu-id="1221a-179">To send notifications using proactive messaging, ensure your users have a clear path to take common actions based on your notification.</span></span> <span data-ttu-id="1221a-180">Убедитесь, что у пользователей есть четкое представление о том, почему они получили уведомление.</span><span class="sxs-lookup"><span data-stu-id="1221a-180">Ensure users have a clear understanding of why they have received a notification.</span></span> <span data-ttu-id="1221a-181">Хорошие сообщения уведомлений обычно включают в себя следующие:</span><span class="sxs-lookup"><span data-stu-id="1221a-181">Good notification messages generally include the following:</span></span>

* <span data-ttu-id="1221a-182">Что произошло: четкое указание на то, что стало причиной уведомления.</span><span class="sxs-lookup"><span data-stu-id="1221a-182">What happened: A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="1221a-183">Каков был результат: необходимо четко знать, какой элемент был обновлен, чтобы вызвать уведомление.</span><span class="sxs-lookup"><span data-stu-id="1221a-183">What was the result: It must be clear what item was updated to cause the notification.</span></span>
* <span data-ttu-id="1221a-184">Кто или что вызвало его: Кто или действия, которые привели к отправлению уведомления.</span><span class="sxs-lookup"><span data-stu-id="1221a-184">Who or what triggered it: Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="1221a-185">Что пользователи могут сделать в ответ: у вас будет легко принимать меры на основе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="1221a-185">What can users do in response: Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="1221a-186">Как пользователи могут отказаться от этого. Необходимо предоставить пользователям путь к отказу от дополнительных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="1221a-186">How can users opt-out: You must provide a path for users to opt-out of additional notifications.</span></span>

<span data-ttu-id="1221a-187">Чтобы отправлять сообщения большой группе пользователей, например в организацию, упреждающие установки приложения с помощью Graph.</span><span class="sxs-lookup"><span data-stu-id="1221a-187">To send messages to a large group of users, for example to your organization, proactively install your app using Graph.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="1221a-188">Запланированные сообщения</span><span class="sxs-lookup"><span data-stu-id="1221a-188">Scheduled messages</span></span>

<span data-ttu-id="1221a-189">При использовании активных сообщений для отправки запланированных сообщений пользователям убедитесь, что часовой пояс обновляется до часового пояса.</span><span class="sxs-lookup"><span data-stu-id="1221a-189">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="1221a-190">Это обеспечивает доставку сообщений пользователям в соответствующее время.</span><span class="sxs-lookup"><span data-stu-id="1221a-190">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="1221a-191">Расписание сообщений обычно включает в себя:</span><span class="sxs-lookup"><span data-stu-id="1221a-191">Schedule messages generally include:</span></span>

* <span data-ttu-id="1221a-192">Почему пользователь получает сообщение: чтобы пользователям было легко понять причину получения сообщения.</span><span class="sxs-lookup"><span data-stu-id="1221a-192">Why is the user receiving the message: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="1221a-193">Что может сделать пользователь далее: пользователи могут принять необходимые действия на основе контента сообщения.</span><span class="sxs-lookup"><span data-stu-id="1221a-193">What can user do next: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="1221a-194">Активная установка приложения с помощью Graph</span><span class="sxs-lookup"><span data-stu-id="1221a-194">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="1221a-195">Активная установка приложений с Graph в настоящее время находится в бета-версии.</span><span class="sxs-lookup"><span data-stu-id="1221a-195">Proactively installing apps using Graph is currently in beta.</span></span>

<span data-ttu-id="1221a-196">Активно сообщайте пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="1221a-196">Proactively message users that have previously not installed or interacted with your app.</span></span> <span data-ttu-id="1221a-197">Например, вы хотите использовать коммуникатор [компании](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации.</span><span class="sxs-lookup"><span data-stu-id="1221a-197">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="1221a-198">В этом случае вы можете использовать API Graph для активной установки приложения для пользователей.</span><span class="sxs-lookup"><span data-stu-id="1221a-198">In this case, you can use the Graph API to proactively install your app for your users.</span></span> <span data-ttu-id="1221a-199">Кэшйте необходимые значения из события, которое `conversationUpdate` ваше приложение получает при установке.</span><span class="sxs-lookup"><span data-stu-id="1221a-199">Cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="1221a-200">Можно установить только приложения, которые находятся в каталоге организационных приложений или Teams App Store.</span><span class="sxs-lookup"><span data-stu-id="1221a-200">You can only install apps that are in your organizational app catalog or the Teams App Store.</span></span>

<span data-ttu-id="1221a-201">Узнайте [об установке приложений](/graph/api/userteamwork-post-installedapps) для пользователей в документации Graph и активной установке ботов и обмена сообщениями в Teams с [Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="1221a-201">See [install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [proactive bot installation and messaging in Teams with Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="1221a-202">Кроме того, на платформе GitHub пример фреймворка [Microsoft.NET.](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)</span><span class="sxs-lookup"><span data-stu-id="1221a-202">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="samples"></a><span data-ttu-id="1221a-203">Примеры</span><span class="sxs-lookup"><span data-stu-id="1221a-203">Samples</span></span>

<span data-ttu-id="1221a-204">В следующем коде показан простой пример кода, который активно устанавливает приложение с помощью Graph:</span><span class="sxs-lookup"><span data-stu-id="1221a-204">The following code shows a simple code sample that proactively installs your app using Graph:</span></span>

# <a name="c"></a>[<span data-ttu-id="1221a-205">C#</span><span class="sxs-lookup"><span data-stu-id="1221a-205">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="1221a-206">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1221a-206">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="1221a-207">Python</span><span class="sxs-lookup"><span data-stu-id="1221a-207">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="1221a-208">JSON</span><span class="sxs-lookup"><span data-stu-id="1221a-208">JSON</span></span>](#tab/json)

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

<span data-ttu-id="1221a-209">Необходимо предоставить пользовательский ИД и ИД клиента.</span><span class="sxs-lookup"><span data-stu-id="1221a-209">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="1221a-210">Если вызов удался, API возвращает следующий объект ответа:</span><span class="sxs-lookup"><span data-stu-id="1221a-210">If the call succeeds, the API returns the following response object:</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a><span data-ttu-id="1221a-211">Пример кода</span><span class="sxs-lookup"><span data-stu-id="1221a-211">Code sample</span></span>

<span data-ttu-id="1221a-212">В следующей таблице приводится простой пример кода, который включает основной поток беседы в приложение Teams и способ создания нового потока беседы в канале в Teams:</span><span class="sxs-lookup"><span data-stu-id="1221a-212">The following table provides a simple code sample that incorporate basic conversation flow into a Teams application and how to create a new conversation thread in a channel in Teams:</span></span>

| <span data-ttu-id="1221a-213">**Имя образца**</span><span class="sxs-lookup"><span data-stu-id="1221a-213">**Sample Name**</span></span> | <span data-ttu-id="1221a-214">**Описание**</span><span class="sxs-lookup"><span data-stu-id="1221a-214">**Description**</span></span> | <span data-ttu-id="1221a-215">**.NET**</span><span class="sxs-lookup"><span data-stu-id="1221a-215">**.NET**</span></span> | <span data-ttu-id="1221a-216">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="1221a-216">**Node.js**</span></span> | <span data-ttu-id="1221a-217">**Python**</span><span class="sxs-lookup"><span data-stu-id="1221a-217">**Python**</span></span> |
|---------------|--------------|--------|-------------|--------|
| <span data-ttu-id="1221a-218">Teams Основы беседы</span><span class="sxs-lookup"><span data-stu-id="1221a-218">Teams Conversation Basics</span></span>  | <span data-ttu-id="1221a-219">Демонстрирует основы бесед в Teams, в том числе отправку одно к одному упреждающих сообщений.</span><span class="sxs-lookup"><span data-stu-id="1221a-219">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>| [<span data-ttu-id="1221a-220">View</span><span class="sxs-lookup"><span data-stu-id="1221a-220">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [<span data-ttu-id="1221a-221">View</span><span class="sxs-lookup"><span data-stu-id="1221a-221">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="1221a-222">View</span><span class="sxs-lookup"><span data-stu-id="1221a-222">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| <span data-ttu-id="1221a-223">Запуск нового потока в канале</span><span class="sxs-lookup"><span data-stu-id="1221a-223">Start new thread in a channel</span></span> | <span data-ttu-id="1221a-224">Демонстрирует создание нового потока в канале.</span><span class="sxs-lookup"><span data-stu-id="1221a-224">Demonstrates creating a new thread in a channel.</span></span> | [<span data-ttu-id="1221a-225">View</span><span class="sxs-lookup"><span data-stu-id="1221a-225">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [<span data-ttu-id="1221a-226">View</span><span class="sxs-lookup"><span data-stu-id="1221a-226">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [<span data-ttu-id="1221a-227">View</span><span class="sxs-lookup"><span data-stu-id="1221a-227">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a><span data-ttu-id="1221a-228">Дополнительный пример кода</span><span class="sxs-lookup"><span data-stu-id="1221a-228">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1221a-229">Teams примеры кода проактивных сообщений</span><span class="sxs-lookup"><span data-stu-id="1221a-229">Teams proactive messaging code samples</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a><span data-ttu-id="1221a-230">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="1221a-230">Next step</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="1221a-231">[**Teams примеры кода проактивных сообщений**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp) 
>  [Формат сообщений бота](~/bots/how-to/format-your-bot-messages.md)</span><span class="sxs-lookup"><span data-stu-id="1221a-231">[**Teams proactive messaging code samples**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
[Format your bot messages](~/bots/how-to/format-your-bot-messages.md)</span></span>
