---
title: отправка упреждающих сообщений
description: описывает, как отправлять упреждающие сообщения с помощью бота Microsoft Teams.
ms.topic: overview
ms.author: anclear
Keywords: send a message get user ID channel ID conversation ID
ms.openlocfilehash: 2d7ff10469a181bb06fda5029c8f6b2725b0402d
ms.sourcegitcommit: 7db6eabe3ef128ac7f14b32d07e9e86c995d187f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/04/2021
ms.locfileid: "50103607"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="3cdc3-104">Отправлять активные сообщения</span><span class="sxs-lookup"><span data-stu-id="3cdc3-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="3cdc3-105">Упреждающие сообщения — это любое сообщение, отправленное ботом, которое не является прямым ответом на запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-105">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="3cdc3-106">Это может включать следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="3cdc3-106">This can include messages like:</span></span>

* <span data-ttu-id="3cdc3-107">Приветствия</span><span class="sxs-lookup"><span data-stu-id="3cdc3-107">Welcome messages</span></span>
* <span data-ttu-id="3cdc3-108">Уведомления</span><span class="sxs-lookup"><span data-stu-id="3cdc3-108">Notifications</span></span>
* <span data-ttu-id="3cdc3-109">Запланированные сообщения</span><span class="sxs-lookup"><span data-stu-id="3cdc3-109">Scheduled messages</span></span>

<span data-ttu-id="3cdc3-110">Чтобы бот мог отправить упреждающие сообщения, он должен иметь доступ к пользователю, групповому чату или команде, в которую вы хотите отправить сообщение.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-110">For your bot to send a proactive message, it must have access to the user, group chat, or team that you want to send the message to.</span></span> <span data-ttu-id="3cdc3-111">Для группового чата или команды это означает, что приложение, содержа которое содержит бота, должно быть сначала установлено в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-111">For a group chat or team, this means the app that contains your bot must be installed to that location first.</span></span> <span data-ttu-id="3cdc3-112">Вы можете [заблаговременно установить](#proactively-install-your-app-using-graph) приложение с помощью Graph в команде, если это необходимо, или использовать политику приложений для раздатки приложений командам и пользователям в клиенте. [](/microsoftteams/teams-custom-app-policies-and-settings)</span><span class="sxs-lookup"><span data-stu-id="3cdc3-112">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team, if required or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="3cdc3-113">Для пользователей ваше приложение либо должно быть установлено для пользователя, либо пользователь должен быть частью команды, в которой установлено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="3cdc3-114">Отправка упреждающего сообщения отличается от отправки обычного сообщения.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-114">Sending a proactive message is different than sending a regular message.</span></span> <span data-ttu-id="3cdc3-115">При этом нет активного `turnContext` ответа.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-115">In that, there is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="3cdc3-116">Кроме того, перед отправкой сообщения может потребоваться создать беседу.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-116">You may also need to create the conversation before sending the message.</span></span> <span data-ttu-id="3cdc3-117">Например, новый чат "один к одному" или новый поток беседы в канале.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="3cdc3-118">Невозможно создать новый групповой чат или новый канал в команде с упреждающего обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="3cdc3-119">На высоком уровне действия, необходимые для отправки упреждающего сообщения:</span><span class="sxs-lookup"><span data-stu-id="3cdc3-119">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="3cdc3-120">[Получите ИД пользователя или ид команды или канала](#get-the-user-id-or-teamchannel-id) (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="3cdc3-120">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="3cdc3-121">[Создайте беседу или цепочку](#create-the-conversation) бесед (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="3cdc3-121">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="3cdc3-122">[Получите ИД беседы.](#get-the-conversation-id)</span><span class="sxs-lookup"><span data-stu-id="3cdc3-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="3cdc3-123">[Отправьте сообщение.](#send-the-message)</span><span class="sxs-lookup"><span data-stu-id="3cdc3-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="3cdc3-124">Фрагменты кода в разделе [примеров](#examples) для создания беседы "один к одному".</span><span class="sxs-lookup"><span data-stu-id="3cdc3-124">The code snippets in the [examples](#examples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="3cdc3-125">Ссылки на полные рабочие примеры для бесед "один к одному", а также для групп или каналов см. в [примерах кода.](#code-samples)</span><span class="sxs-lookup"><span data-stu-id="3cdc3-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code samples](#code-samples).</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="3cdc3-126">Get the user ID or team/channel ID</span><span class="sxs-lookup"><span data-stu-id="3cdc3-126">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="3cdc3-127">Чтобы создать беседу или цепочку бесед в канале, необходим правильный ИД.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-127">To create a new conversation or conversation thread in a channel, you need the correct ID.</span></span> <span data-ttu-id="3cdc3-128">Этот ИД можно получить несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="3cdc3-128">You can receive or retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="3cdc3-129">Когда приложение устанавливается в любом конкретном контексте, вы получите [ `onMembersAdded` действие.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="3cdc3-129">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="3cdc3-130">При добавлении нового пользователя в контекст, в котором установлено приложение, вы получите [ `onMembersAdded` действие.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="3cdc3-130">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="3cdc3-131">Вы можете получить [список каналов](~/bots/how-to/get-teams-context.md) в команде, в которая установлено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-131">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="3cdc3-132">Вы можете получить [список участников команды,](~/bots/how-to/get-teams-context.md) в которая установлено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-132">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="3cdc3-133">Все действия, получаемые ботом, должны содержать необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-133">Every Activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="3cdc3-134">Независимо от того, как вы получаете информацию, вам потребуется сохранить беседу или создать `tenantId` `userId` новую `channelId` беседу.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-134">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="3cdc3-135">Вы также можете создать цепочку беседы в общем или канале команды по `teamId` умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-135">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="3cdc3-136">Уникальный для вашего ИД бота и конкретного пользователя, вы не можете повторно использовать их `userId` между ботами.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-136">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="3cdc3-137">Однако перед отправкой упреждающего сообщения в канал бот должен быть установлен в `channelId` команде.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-137">The `channelId` is global, however, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="3cdc3-138">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="3cdc3-138">Create the conversation</span></span>

<span data-ttu-id="3cdc3-139">После получения сведений о пользователе или канале необходимо создать беседу, если она еще не существует или вы не `conversationId` знаете.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-139">After you have the user or channel information, you need to create the conversation if it doesn't already exist or you don't know the `conversationId`.</span></span> <span data-ttu-id="3cdc3-140">Необходимо создать беседу только один раз и убедиться, что вы сохраняете значение или объект для `conversationId` `conversationReference` использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-140">You must only create the conversation once and make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="3cdc3-141">Получить ИД беседы</span><span class="sxs-lookup"><span data-stu-id="3cdc3-141">Get the conversation ID</span></span>

<span data-ttu-id="3cdc3-142">После создания беседы используйте объект `conversationReference` или `conversationId` отправьте `tenantId` сообщение.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-142">After the conversation is created, use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="3cdc3-143">Этот ИД можно получить, создав беседу или с помощью любого действия, отправленного вам из этого контекста.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-143">You can get this ID by either creating the conversation or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="3cdc3-144">Убедитесь, что вы сохраняете этот ИД.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-144">Make certain that you store this ID.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="3cdc3-145">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="3cdc3-145">Send the message</span></span>

<span data-ttu-id="3cdc3-146">Теперь, когда у вас есть правильные сведения об адресе, вы можете отправить сообщение.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-146">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="3cdc3-147">Если вы используете SDK, вы сделаете это с помощью метода, а также для прямого `continueConversation` `conversationId` вызова `tenantId` API.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-147">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="3cdc3-148">Чтобы успешно отправить сообщение, необходимо `conversationParameters` правильно настроить его.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-148">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="3cdc3-149">См. [раздел примеров](#examples) или используйте один из примеров, перечисленных в разделе [примеров](#code-samples) кода.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-149">See the [examples](#examples) section or use one of the samples listed in the [code samples](#code-samples) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="3cdc3-150">Практические методики упреждающего обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="3cdc3-150">Best practices for proactive messaging</span></span>

<span data-ttu-id="3cdc3-151">Отправка упреждающих сообщений пользователям — очень эффективный способ общения с пользователями.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-151">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="3cdc3-152">Однако с их точки зрения это сообщение может отображаться полностью незащищенным, и в случае приветствия это сообщение впервые взаимодействует с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-152">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="3cdc3-153">Поэтому очень важно использовать эту функцию не слишком часто, не рассылая пользователям нежелаую почту, и предоставлять достаточно информации, чтобы пользователи могли понять, почему они рассылаются.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-153">Therefore, it is very important to use this functionality sparingly, don't spam your users, and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="3cdc3-154">Приветствия</span><span class="sxs-lookup"><span data-stu-id="3cdc3-154">Welcome messages</span></span>

<span data-ttu-id="3cdc3-155">При использовании упреждающих сообщений для отправки приветствия пользователю необходимо помнить, что для большинства людей, получающих сообщение, нет контекста для его получения.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-155">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there is no context for why they are receiving it.</span></span> <span data-ttu-id="3cdc3-156">Это также первый раз, когда они взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-156">This is also the first time they have interacted with your app.</span></span> <span data-ttu-id="3cdc3-157">Это ваша возможность создать хорошее первое впечатление.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-157">It is your opportunity to create a good first impression.</span></span> <span data-ttu-id="3cdc3-158">Лучшие приветствия должны включать следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="3cdc3-158">The best welcome messages must include:</span></span>

* <span data-ttu-id="3cdc3-159">**Почему пользователь получает сообщение.**</span><span class="sxs-lookup"><span data-stu-id="3cdc3-159">**Why a user is receiving the message.**</span></span> <span data-ttu-id="3cdc3-160">Пользователю должно быть понятно, почему он получает сообщение.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-160">It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="3cdc3-161">Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен, и, возможно, кто его установил.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-161">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="3cdc3-162">**Что вы предлагаете.**</span><span class="sxs-lookup"><span data-stu-id="3cdc3-162">**What do you offer.**</span></span> <span data-ttu-id="3cdc3-163">Что они могут делать с вашим приложением?</span><span class="sxs-lookup"><span data-stu-id="3cdc3-163">What can they do with your app?</span></span> <span data-ttu-id="3cdc3-164">Какое значение вы можете им дать?</span><span class="sxs-lookup"><span data-stu-id="3cdc3-164">What value can you bring to them?</span></span>
* <span data-ttu-id="3cdc3-165">**Что они должны делать дальше.**</span><span class="sxs-lookup"><span data-stu-id="3cdc3-165">**What should they do next.**</span></span> <span data-ttu-id="3cdc3-166">Предложите им опробовать команду или каким-либо образом взаимодействовать с приложением.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-166">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="3cdc3-167">Помните, что неудовлетворительные приветствия могут привести к блокированию бота пользователями.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-167">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="3cdc3-168">Потратите много времени на то, чтобы создать приветствия, и итерации на них, если они не имеют желаемого эффекта.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-168">Spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="3cdc3-169">Уведомления</span><span class="sxs-lookup"><span data-stu-id="3cdc3-169">Notification messages</span></span>

<span data-ttu-id="3cdc3-170">При использовании упреждающих сообщений для отправки уведомлений необходимо убедиться, что у пользователей есть четкий путь для распространенных действий на основе уведомления и четкого понимания причины отправки уведомления.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-170">When using proactive messaging to send notifications you must ensure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="3cdc3-171">К хорошим уведомлениям обычно относятся:</span><span class="sxs-lookup"><span data-stu-id="3cdc3-171">Good notification messages generally include:</span></span>

* <span data-ttu-id="3cdc3-172">**Что случилось.**</span><span class="sxs-lookup"><span data-stu-id="3cdc3-172">**What happened.**</span></span> <span data-ttu-id="3cdc3-173">Четкое указание того, что стало причиной уведомления.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-173">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="3cdc3-174">**Результат.**</span><span class="sxs-lookup"><span data-stu-id="3cdc3-174">**What was the result.**</span></span> <span data-ttu-id="3cdc3-175">Чтобы вызвать уведомление, необходимо четко знать, какой элемент или что было обновлено.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-175">It must be clear what item or thing was updated to cause the notification.</span></span>
* <span data-ttu-id="3cdc3-176">**Кто и что инициировало его.**</span><span class="sxs-lookup"><span data-stu-id="3cdc3-176">**Who/what triggered it.**</span></span> <span data-ttu-id="3cdc3-177">Кто или какие действия привели к отправлению уведомления.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-177">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="3cdc3-178">**Что пользователи могут делать в ответе.**</span><span class="sxs-lookup"><span data-stu-id="3cdc3-178">**What can users do in response.**</span></span> <span data-ttu-id="3cdc3-179">Сделайте так, чтобы пользователи легко делайте действия на основе ваших уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-179">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="3cdc3-180">**Как пользователи могут отказаться от этого.** Необходимо предоставить пользователям путь для отказа от дополнительных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-180">**How can users opt out.** You must provide a path for users to opt out of additional notifications.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="3cdc3-181">Упреждающие установки приложения с помощью Graph</span><span class="sxs-lookup"><span data-stu-id="3cdc3-181">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="3cdc3-182">Упреждающие установки приложений с помощью Microsoft Graph в настоящее время находятся в бета-версии.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-182">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="3cdc3-183">Иногда может потребоваться заблаговременно отправлять сообщения пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-183">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="3cdc3-184">Например, вы хотите использовать company [communicator](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-184">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="3cdc3-185">В этом сценарии можно использовать API Graph для упреждающего установки приложения для пользователей, а затем кэшировать необходимые значения из события, получаемого вашим приложением `conversationUpdate` после установки.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-185">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="3cdc3-186">Вы можете устанавливать только приложения, которые находятся в каталоге приложений организации или в магазине приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-186">You can only install apps that are in your organizational app catalog or the Teams app store.</span></span>

<span data-ttu-id="3cdc3-187">См. ["Установка приложений для пользователей"](/graph/api/userteamwork-post-installedapps) в документации по Graph, а также в документации по профилактической установке ботов и обмену сообщениями [в Teams с помощью Microsoft Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="3cdc3-187">See [Install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="3cdc3-188">На платформе [GitHub также](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) есть пример платформы Microsoft .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-188">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="3cdc3-189">Примеры</span><span class="sxs-lookup"><span data-stu-id="3cdc3-189">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="3cdc3-190">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="3cdc3-190">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="3cdc3-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="3cdc3-191">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="3cdc3-192">Python</span><span class="sxs-lookup"><span data-stu-id="3cdc3-192">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="3cdc3-193">JSON</span><span class="sxs-lookup"><span data-stu-id="3cdc3-193">JSON</span></span>](#tab/json)

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

<span data-ttu-id="3cdc3-194">Необходимо предоставить ид пользователя, и ид клиента.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-194">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="3cdc3-195">В случае успешного вызова API возвращается со следующим объектом ответа.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-195">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a><span data-ttu-id="3cdc3-196">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="3cdc3-196">Code samples</span></span>

<span data-ttu-id="3cdc3-197">Официальные примеры упреждающих сообщений:</span><span class="sxs-lookup"><span data-stu-id="3cdc3-197">The official proactive messaging samples are as follows:</span></span>

| <span data-ttu-id="3cdc3-198">Имя примера</span><span class="sxs-lookup"><span data-stu-id="3cdc3-198">Sample Name</span></span>           | <span data-ttu-id="3cdc3-199">Описание</span><span class="sxs-lookup"><span data-stu-id="3cdc3-199">Description</span></span>                                                                      | <span data-ttu-id="3cdc3-200">.NET</span><span class="sxs-lookup"><span data-stu-id="3cdc3-200">.NET</span></span>    | <span data-ttu-id="3cdc3-201">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3cdc3-201">JavaScript</span></span>   | <span data-ttu-id="3cdc3-202">Python</span><span class="sxs-lookup"><span data-stu-id="3cdc3-202">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="3cdc3-203">Основные принципы бесед Teams</span><span class="sxs-lookup"><span data-stu-id="3cdc3-203">Teams Conversation Basics</span></span>  | <span data-ttu-id="3cdc3-204">В этой теме показано, как начать беседы в Teams, включая отправку сообщений "один к одному".</span><span class="sxs-lookup"><span data-stu-id="3cdc3-204">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="3cdc3-205">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="3cdc3-205">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="3cdc3-206">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3cdc3-206">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="3cdc3-207">Python</span><span class="sxs-lookup"><span data-stu-id="3cdc3-207">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="3cdc3-208">Запуск нового потока в канале</span><span class="sxs-lookup"><span data-stu-id="3cdc3-208">Start new thread in a channel</span></span>     | <span data-ttu-id="3cdc3-209">Демонстрирует создание нового потока в канале.</span><span class="sxs-lookup"><span data-stu-id="3cdc3-209">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="3cdc3-210">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="3cdc3-210">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="3cdc3-211">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3cdc3-211">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="3cdc3-212">Python</span><span class="sxs-lookup"><span data-stu-id="3cdc3-212">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a><span data-ttu-id="3cdc3-213">Просмотр дополнительных примеров кода</span><span class="sxs-lookup"><span data-stu-id="3cdc3-213">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3cdc3-214">**Примеры кода упреждающих сообщений Teams**</span><span class="sxs-lookup"><span data-stu-id="3cdc3-214">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
