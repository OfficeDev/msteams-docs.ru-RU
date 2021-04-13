---
title: отправка упреждающих сообщений
description: описывает, как отправлять упреждающие сообщения с помощью бота Microsoft Teams.
ms.topic: overview
ms.author: anclear
Keywords: отправка сообщения получить ID-ID-ID канала для беседы
ms.openlocfilehash: 7da470eaba6ae9ecb82c9a7ba04d69b2f196a9d7
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654295"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="897af-104">Отправлять активные сообщения</span><span class="sxs-lookup"><span data-stu-id="897af-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="897af-105">Проактивное сообщение — это любое сообщение, отправленное ботом, которое не является прямым ответом на запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="897af-105">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="897af-106">Это может включать такие сообщения, как:</span><span class="sxs-lookup"><span data-stu-id="897af-106">This can include messages like:</span></span>

* <span data-ttu-id="897af-107">Приветствия</span><span class="sxs-lookup"><span data-stu-id="897af-107">Welcome messages</span></span>
* <span data-ttu-id="897af-108">Уведомления</span><span class="sxs-lookup"><span data-stu-id="897af-108">Notifications</span></span>
* <span data-ttu-id="897af-109">Запланированные сообщения</span><span class="sxs-lookup"><span data-stu-id="897af-109">Scheduled messages</span></span>

<span data-ttu-id="897af-110">Для отправки упреждающего сообщения бот должен иметь доступ к пользователю, групповому чату или команде, в которую необходимо отправить сообщение.</span><span class="sxs-lookup"><span data-stu-id="897af-110">For your bot to send a proactive message, it must have access to the user, group chat, or team that you want to send the message to.</span></span> <span data-ttu-id="897af-111">Для группового чата или группы это означает, что приложение, содержа которое содержит бот, сначала должно быть установлено в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="897af-111">For a group chat or team, this means the app that contains your bot must be installed to that location first.</span></span> <span data-ttu-id="897af-112">Вы можете [упреждающий](#proactively-install-your-app-using-graph) установку приложения с помощью Graph [](/microsoftteams/teams-custom-app-policies-and-settings) в команде, если это необходимо, или использовать политику приложения для вытеснки приложений для групп и пользователей в клиенте.</span><span class="sxs-lookup"><span data-stu-id="897af-112">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team, if required or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="897af-113">Для пользователей ваше приложение либо должно быть установлено для пользователя, либо пользователь должен быть частью команды, в которой установлено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="897af-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="897af-114">Отправка упреждающего сообщения отличается от обычного сообщения.</span><span class="sxs-lookup"><span data-stu-id="897af-114">Sending a proactive message is different than sending a regular message.</span></span> <span data-ttu-id="897af-115">В этом нет активного использования `turnContext` для ответа.</span><span class="sxs-lookup"><span data-stu-id="897af-115">In that, there is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="897af-116">Перед отправкой сообщения может потребоваться также создать беседу.</span><span class="sxs-lookup"><span data-stu-id="897af-116">You may also need to create the conversation before sending the message.</span></span> <span data-ttu-id="897af-117">Например, новый чат один к одному или новый поток беседы в канале.</span><span class="sxs-lookup"><span data-stu-id="897af-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="897af-118">Невозможно создать новый групповой чат или новый канал в команде с активной передачей сообщений.</span><span class="sxs-lookup"><span data-stu-id="897af-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="897af-119">На высоком уровне необходимо выполнить действия, необходимые для отправки проактивного сообщения:</span><span class="sxs-lookup"><span data-stu-id="897af-119">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="897af-120">[Получите пользовательский ID или team/channel ID](#get-the-user-id-or-teamchannel-id) (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="897af-120">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="897af-121">[Создание потока беседы](#create-the-conversation) или беседы (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="897af-121">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="897af-122">[Получите ID беседы](#get-the-conversation-id).</span><span class="sxs-lookup"><span data-stu-id="897af-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="897af-123">[Отправка сообщения](#send-the-message).</span><span class="sxs-lookup"><span data-stu-id="897af-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="897af-124">Фрагменты кода в разделе [примеры](#examples) для создания беседы один к одному.</span><span class="sxs-lookup"><span data-stu-id="897af-124">The code snippets in the [examples](#examples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="897af-125">Ссылки на полные рабочие примеры для бесед и групп или каналов см. в [примере кода.](#code-samples)</span><span class="sxs-lookup"><span data-stu-id="897af-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code samples](#code-samples).</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="897af-126">Получить пользовательский ИД или team/channel ID</span><span class="sxs-lookup"><span data-stu-id="897af-126">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="897af-127">Для создания нового потока беседы или беседы в канале необходим правильный ID.</span><span class="sxs-lookup"><span data-stu-id="897af-127">To create a new conversation or conversation thread in a channel, you need the correct ID.</span></span> <span data-ttu-id="897af-128">Этот ID можно получить или получить несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="897af-128">You can receive or retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="897af-129">Когда ваше приложение установлено в определенном контексте, вы получите [ `onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="897af-129">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="897af-130">При добавлении нового пользователя в контекст, в котором установлено приложение, вы получите [ `onMembersAdded` действие.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="897af-130">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="897af-131">Список [каналов в](~/bots/how-to/get-teams-context.md) команде, установленной в приложении, можно получить.</span><span class="sxs-lookup"><span data-stu-id="897af-131">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="897af-132">Вы можете получить [список членов команды,](~/bots/how-to/get-teams-context.md) установленной вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="897af-132">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="897af-133">Каждое действие, получаемые ботом, должно содержать необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="897af-133">Every Activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="897af-134">Независимо от того, как вы получаете информацию, вам потребуется сохранить и либо создать `tenantId` `userId` новый `channelId` разговор.</span><span class="sxs-lookup"><span data-stu-id="897af-134">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="897af-135">Вы также можете использовать этот поток для создания нового потока беседы в общем или по умолчанию `teamId` канале группы.</span><span class="sxs-lookup"><span data-stu-id="897af-135">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="897af-136">Уникальный для вашего бота и определенного пользователя, вы не можете `userId` повторно использовать их между ботами.</span><span class="sxs-lookup"><span data-stu-id="897af-136">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="897af-137">Однако, прежде чем отправить проактивное сообщение на канал, бот должен быть установлен в `channelId` команде.</span><span class="sxs-lookup"><span data-stu-id="897af-137">The `channelId` is global, however, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="897af-138">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="897af-138">Create the conversation</span></span>

<span data-ttu-id="897af-139">После получения сведений о пользователе или канале необходимо создать беседу, если она еще не существует или вы не знаете `conversationId` .</span><span class="sxs-lookup"><span data-stu-id="897af-139">After you have the user or channel information, you need to create the conversation if it doesn't already exist or you don't know the `conversationId`.</span></span> <span data-ttu-id="897af-140">Вы должны создать беседу только один раз и убедиться, что вы сохраняете значение или объект, который `conversationId` будет использовать в `conversationReference` будущем.</span><span class="sxs-lookup"><span data-stu-id="897af-140">You must only create the conversation once and make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="897af-141">Получить ID беседы</span><span class="sxs-lookup"><span data-stu-id="897af-141">Get the conversation ID</span></span>

<span data-ttu-id="897af-142">После создания беседы используйте объект `conversationReference` или `conversationId` отправить `tenantId` сообщение.</span><span class="sxs-lookup"><span data-stu-id="897af-142">After the conversation is created, use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="897af-143">Этот ID можно получить, создав беседу или храня ее из любого действия, отправленного вам из этого контекста.</span><span class="sxs-lookup"><span data-stu-id="897af-143">You can get this ID by either creating the conversation or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="897af-144">Убедитесь, что вы сохраняете этот ID.</span><span class="sxs-lookup"><span data-stu-id="897af-144">Make certain that you store this ID.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="897af-145">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="897af-145">Send the message</span></span>

<span data-ttu-id="897af-146">Теперь, когда у вас есть правильные сведения о адресе, вы можете отправить свое сообщение.</span><span class="sxs-lookup"><span data-stu-id="897af-146">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="897af-147">Если вы используете SDK, вы сделаете это с помощью метода, а также для прямого `continueConversation` `conversationId` вызова `tenantId` API.</span><span class="sxs-lookup"><span data-stu-id="897af-147">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="897af-148">Чтобы успешно отправить сообщение, необходимо правильно `conversationParameters` установить.</span><span class="sxs-lookup"><span data-stu-id="897af-148">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="897af-149">См. [раздел примеры](#examples) или используйте один из примеров, перечисленных в разделе примеры [кода.](#code-samples)</span><span class="sxs-lookup"><span data-stu-id="897af-149">See the [examples](#examples) section or use one of the samples listed in the [code samples](#code-samples) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="897af-150">Лучшие практики для активного обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="897af-150">Best practices for proactive messaging</span></span>

<span data-ttu-id="897af-151">Отправка активных сообщений пользователям — это очень эффективный способ общения с пользователями.</span><span class="sxs-lookup"><span data-stu-id="897af-151">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="897af-152">Однако с их точки зрения это сообщение может отображаться совершенно незащищенным, и в случае приветствия сообщений это первый раз, когда они взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="897af-152">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="897af-153">Поэтому очень важно использовать эти функции экономно, не спамить пользователей и предоставлять достаточно информации, чтобы пользователи могли понять, почему они рассылаются.</span><span class="sxs-lookup"><span data-stu-id="897af-153">Therefore, it is very important to use this functionality sparingly, don't spam your users, and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="897af-154">Приветствия</span><span class="sxs-lookup"><span data-stu-id="897af-154">Welcome messages</span></span>

<span data-ttu-id="897af-155">При использовании активного обмена сообщениями для отправки приветствия пользователю необходимо иметь в виду, что для большинства людей, получающих сообщение, нет контекста для его получения.</span><span class="sxs-lookup"><span data-stu-id="897af-155">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there is no context for why they are receiving it.</span></span> <span data-ttu-id="897af-156">Кроме того, они впервые взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="897af-156">This is also the first time they have interacted with your app.</span></span> <span data-ttu-id="897af-157">Это ваша возможность создать хорошее первое впечатление.</span><span class="sxs-lookup"><span data-stu-id="897af-157">It is your opportunity to create a good first impression.</span></span> <span data-ttu-id="897af-158">Лучшие приветствия должны включать в себя:</span><span class="sxs-lookup"><span data-stu-id="897af-158">The best welcome messages must include:</span></span>

* <span data-ttu-id="897af-159">**Почему пользователь получает сообщение.**</span><span class="sxs-lookup"><span data-stu-id="897af-159">**Why a user is receiving the message.**</span></span> <span data-ttu-id="897af-160">Пользователю должно быть ясно, почему он получает сообщение.</span><span class="sxs-lookup"><span data-stu-id="897af-160">It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="897af-161">Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен и кто его установил.</span><span class="sxs-lookup"><span data-stu-id="897af-161">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="897af-162">**Что вы предлагаете.**</span><span class="sxs-lookup"><span data-stu-id="897af-162">**What do you offer.**</span></span> <span data-ttu-id="897af-163">Что они могут сделать с вашим приложением?</span><span class="sxs-lookup"><span data-stu-id="897af-163">What can they do with your app?</span></span> <span data-ttu-id="897af-164">Какое значение вы можете принести им?</span><span class="sxs-lookup"><span data-stu-id="897af-164">What value can you bring to them?</span></span>
* <span data-ttu-id="897af-165">**Что они должны делать дальше.**</span><span class="sxs-lookup"><span data-stu-id="897af-165">**What should they do next.**</span></span> <span data-ttu-id="897af-166">Предложите им опробовать команду или каким-то образом взаимодействовать с приложением.</span><span class="sxs-lookup"><span data-stu-id="897af-166">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="897af-167">Помните, что неудовлетворительные приветствия могут привести к блокировке бота пользователями.</span><span class="sxs-lookup"><span data-stu-id="897af-167">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="897af-168">Утратите много времени на то, чтобы создать приветствия и итерировать их, если они не будут иметь желаемого эффекта.</span><span class="sxs-lookup"><span data-stu-id="897af-168">Spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="897af-169">Уведомления</span><span class="sxs-lookup"><span data-stu-id="897af-169">Notification messages</span></span>

<span data-ttu-id="897af-170">При использовании упреждающих сообщений для отправки уведомлений необходимо убедиться, что у пользователей есть четкий путь к общим действиям, основанным на уведомлении и четком понимании причин, по которым произошло уведомление.</span><span class="sxs-lookup"><span data-stu-id="897af-170">When using proactive messaging to send notifications you must ensure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="897af-171">Хорошие сообщения уведомлений обычно включают в себя:</span><span class="sxs-lookup"><span data-stu-id="897af-171">Good notification messages generally include:</span></span>

* <span data-ttu-id="897af-172">**Что случилось.**</span><span class="sxs-lookup"><span data-stu-id="897af-172">**What happened.**</span></span> <span data-ttu-id="897af-173">Четкое указание на то, что стало причиной уведомления.</span><span class="sxs-lookup"><span data-stu-id="897af-173">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="897af-174">**Какой был результат.**</span><span class="sxs-lookup"><span data-stu-id="897af-174">**What was the result.**</span></span> <span data-ttu-id="897af-175">Должно быть ясно, какой элемент или вещь была обновлена, чтобы вызвать уведомление.</span><span class="sxs-lookup"><span data-stu-id="897af-175">It must be clear what item or thing was updated to cause the notification.</span></span>
* <span data-ttu-id="897af-176">**Кто и что вызвало его.**</span><span class="sxs-lookup"><span data-stu-id="897af-176">**Who/what triggered it.**</span></span> <span data-ttu-id="897af-177">Кто или какие действия привели к отправлению уведомления.</span><span class="sxs-lookup"><span data-stu-id="897af-177">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="897af-178">**Что пользователи могут сделать в ответ.**</span><span class="sxs-lookup"><span data-stu-id="897af-178">**What can users do in response.**</span></span> <span data-ttu-id="897af-179">Сделайте так, чтобы пользователям было проще принимать меры на основе ваших уведомлений.</span><span class="sxs-lookup"><span data-stu-id="897af-179">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="897af-180">**Как пользователи могут отказаться.** Необходимо предоставить пользователям путь к отказу от дополнительных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="897af-180">**How can users opt out.** You must provide a path for users to opt out of additional notifications.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="897af-181">Запланированные сообщения</span><span class="sxs-lookup"><span data-stu-id="897af-181">Scheduled messages</span></span>

<span data-ttu-id="897af-182">При использовании активных сообщений для отправки запланированных сообщений пользователям убедитесь, что часовой пояс обновляется до часового пояса.</span><span class="sxs-lookup"><span data-stu-id="897af-182">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="897af-183">Это обеспечивает доставку сообщений пользователям в соответствующее время.</span><span class="sxs-lookup"><span data-stu-id="897af-183">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="897af-184">Расписание сообщений обычно включает в себя:</span><span class="sxs-lookup"><span data-stu-id="897af-184">Schedule messages generally include:</span></span>

* <span data-ttu-id="897af-185">**Почему пользователь получает** сообщение. Чтобы пользователям было легко понять причину, по которой они получают сообщение.</span><span class="sxs-lookup"><span data-stu-id="897af-185">**Why is the user receiving the message**: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="897af-186">**Что может сделать пользователь далее.** Пользователи могут принять необходимые действия на основе контента сообщения.</span><span class="sxs-lookup"><span data-stu-id="897af-186">**What can user do next**: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="897af-187">Активная установка приложения с помощью Graph</span><span class="sxs-lookup"><span data-stu-id="897af-187">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="897af-188">Активная установка приложений с помощью Microsoft Graph в настоящее время находится в бета-версии.</span><span class="sxs-lookup"><span data-stu-id="897af-188">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="897af-189">Иногда может потребоваться заблаговременное сообщение пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="897af-189">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="897af-190">Например, вы хотите использовать коммуникатор [компании](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации.</span><span class="sxs-lookup"><span data-stu-id="897af-190">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="897af-191">Для этого сценария можно использовать API Graph для активной установки приложения для пользователей, а затем кэшировать необходимые значения из события, которое ваше приложение получает при `conversationUpdate` установке.</span><span class="sxs-lookup"><span data-stu-id="897af-191">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="897af-192">Можно установить только приложения, которые находятся в каталоге организационных приложений или в магазине приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="897af-192">You can only install apps that are in your organizational app catalog or the Teams app store.</span></span>

<span data-ttu-id="897af-193">См. [в документе](/graph/api/userteamwork-post-installedapps) Install apps for users in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="897af-193">See [Install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="897af-194">На платформе GitHub также имеется пример фреймворка [Microsoft.NET.](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)</span><span class="sxs-lookup"><span data-stu-id="897af-194">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="897af-195">Примеры</span><span class="sxs-lookup"><span data-stu-id="897af-195">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="897af-196">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="897af-196">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="897af-197">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="897af-197">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="897af-198">Python</span><span class="sxs-lookup"><span data-stu-id="897af-198">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="897af-199">JSON</span><span class="sxs-lookup"><span data-stu-id="897af-199">JSON</span></span>](#tab/json)

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

<span data-ttu-id="897af-200">Необходимо предоставить пользовательский ИД и ИД клиента.</span><span class="sxs-lookup"><span data-stu-id="897af-200">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="897af-201">Если вызов удался, API возвращается со следующим объектом ответа.</span><span class="sxs-lookup"><span data-stu-id="897af-201">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a><span data-ttu-id="897af-202">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="897af-202">Code samples</span></span>

<span data-ttu-id="897af-203">Официальные примеры проактивных сообщений:</span><span class="sxs-lookup"><span data-stu-id="897af-203">The official proactive messaging samples are as follows:</span></span>

| <span data-ttu-id="897af-204">Имя образца</span><span class="sxs-lookup"><span data-stu-id="897af-204">Sample Name</span></span>           | <span data-ttu-id="897af-205">Описание</span><span class="sxs-lookup"><span data-stu-id="897af-205">Description</span></span>                                                                      | <span data-ttu-id="897af-206">.NET</span><span class="sxs-lookup"><span data-stu-id="897af-206">.NET</span></span>    | <span data-ttu-id="897af-207">JavaScript</span><span class="sxs-lookup"><span data-stu-id="897af-207">JavaScript</span></span>   | <span data-ttu-id="897af-208">Python</span><span class="sxs-lookup"><span data-stu-id="897af-208">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="897af-209">Основы беседы teams</span><span class="sxs-lookup"><span data-stu-id="897af-209">Teams Conversation Basics</span></span>  | <span data-ttu-id="897af-210">Демонстрирует основы бесед в Teams, в том числе отправку одно к одному упреждающих сообщений.</span><span class="sxs-lookup"><span data-stu-id="897af-210">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="897af-211">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="897af-211">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="897af-212">JavaScript</span><span class="sxs-lookup"><span data-stu-id="897af-212">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="897af-213">Python</span><span class="sxs-lookup"><span data-stu-id="897af-213">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="897af-214">Запуск нового потока в канале</span><span class="sxs-lookup"><span data-stu-id="897af-214">Start new thread in a channel</span></span>     | <span data-ttu-id="897af-215">Демонстрирует создание нового потока в канале.</span><span class="sxs-lookup"><span data-stu-id="897af-215">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="897af-216">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="897af-216">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="897af-217">JavaScript</span><span class="sxs-lookup"><span data-stu-id="897af-217">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="897af-218">Python</span><span class="sxs-lookup"><span data-stu-id="897af-218">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a><span data-ttu-id="897af-219">Просмотр дополнительных примеров кода</span><span class="sxs-lookup"><span data-stu-id="897af-219">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="897af-220">**Teams proactive messaging code samples**</span><span class="sxs-lookup"><span data-stu-id="897af-220">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
