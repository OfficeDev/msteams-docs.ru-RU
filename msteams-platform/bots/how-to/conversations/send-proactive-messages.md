---
title: Отправлять активные сообщения
author: clearab
description: Отправка активных сообщений с помощью робота Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2dfb8e18243079ca38d505f4b80deb7abf2de32f
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874851"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="a951a-103">Отправлять активные сообщения</span><span class="sxs-lookup"><span data-stu-id="a951a-103">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="a951a-104">Упреждающее сообщение — это любое сообщение, отправляемое сервером-роботом, которое не находится в прямом ответе на запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="a951a-104">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="a951a-105">Сюда могут относиться такие сообщения, как:</span><span class="sxs-lookup"><span data-stu-id="a951a-105">This can include messages like:</span></span>

* <span data-ttu-id="a951a-106">Приветственные сообщения</span><span class="sxs-lookup"><span data-stu-id="a951a-106">Welcome messages</span></span>
* <span data-ttu-id="a951a-107">Уведомления</span><span class="sxs-lookup"><span data-stu-id="a951a-107">Notifications</span></span>
* <span data-ttu-id="a951a-108">Запланированные сообщения</span><span class="sxs-lookup"><span data-stu-id="a951a-108">Scheduled messages</span></span>

<span data-ttu-id="a951a-109">Чтобы ваш робот мог отправлять упреждающее сообщение, он должен иметь доступ к пользователю, группе или группе, которым вы хотите отправить сообщение.</span><span class="sxs-lookup"><span data-stu-id="a951a-109">In order for your bot to send a proactive message, it must have access to the user, group chat, or team that you wish to send the message to.</span></span> <span data-ttu-id="a951a-110">Для группового чата или команды это означает, что приложение, которое содержит ваш Bot, должно быть сначала установлено в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="a951a-110">For a group chat or team, this means the app that contains your bot must first be installed to that location.</span></span> <span data-ttu-id="a951a-111">Вы можете принудительно [установить приложение с помощью Graph](#proactively-install-your-app-using-graph) в группе, если это необходимо, или использовать [политику приложений](/microsoftteams/teams-custom-app-policies-and-settings) для передачи приложений в Teams и пользователей в клиенте.</span><span class="sxs-lookup"><span data-stu-id="a951a-111">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team if necessary, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="a951a-112">Для пользователей ваше приложение необходимо установить для этого пользователя, или пользователь должен входить в группу, в которой установлено приложение.</span><span class="sxs-lookup"><span data-stu-id="a951a-112">For users, your app either needs to be installed for that user, or your user needs to be part of a team where your app is installed.</span></span>

<span data-ttu-id="a951a-113">Отправка упреждающего сообщения отличается от отправки обычного сообщения в том случае, если вы не будете использовать активное сообщение `turnContext` для ответа.</span><span class="sxs-lookup"><span data-stu-id="a951a-113">Sending a proactive message is different than sending a regular message in that you won't have an active `turnContext` to use for a reply.</span></span> <span data-ttu-id="a951a-114">Кроме того, перед отправкой сообщения вам может потребоваться создать беседу (например, новый чат "один к одному" или "новый поток бесед в канале").</span><span class="sxs-lookup"><span data-stu-id="a951a-114">You may also need to create the conversation (for example a new one-to-one chat, or a new conversation thread in a channel) before sending the message.</span></span> <span data-ttu-id="a951a-115">Вы не можете создать новый чат группы или новый канал в команде "активные системы обмена сообщениями".</span><span class="sxs-lookup"><span data-stu-id="a951a-115">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="a951a-116">На высоком уровне описаны действия, которые необходимо выполнить для отправки упреждающего сообщения:</span><span class="sxs-lookup"><span data-stu-id="a951a-116">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="a951a-117">[Получение идентификатора пользователя или группы или канала](#get-the-user-id-or-teamchannel-id) (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="a951a-117">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="a951a-118">[Создайте обсуждение или](#create-the-conversation) цепочку сообщений (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="a951a-118">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="a951a-119">[Получение идентификатора беседы](#get-the-conversation-id).</span><span class="sxs-lookup"><span data-stu-id="a951a-119">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="a951a-120">[Отправьте сообщение](#send-the-message).</span><span class="sxs-lookup"><span data-stu-id="a951a-120">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="a951a-121">Фрагменты кода, приведенные в разделе " [примеры](#examples) ", предназначены для создания беседы "один к одному", в разделе " [ссылки](#references) " приведены ссылки на готовые рабочие примеры для бесед и групп и каналов "один к одному".</span><span class="sxs-lookup"><span data-stu-id="a951a-121">The code snippets in the [examples](#examples) section below are for creating a one-to-one conversation, see the [references](#references) section for links to complete working samples for both one-to-once conversations and group/channels.</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="a951a-122">Получение идентификатора пользователя или группы или канала</span><span class="sxs-lookup"><span data-stu-id="a951a-122">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="a951a-123">Если вам нужно создать новую беседу или цепочку бесед в канале, сначала необходимо получить правильный идентификатор для создания беседы.</span><span class="sxs-lookup"><span data-stu-id="a951a-123">If you need to create a new conversation or conversation thread in a channel you'll first need the right ID to create the conversation.</span></span> <span data-ttu-id="a951a-124">Вы можете получить или получить этот идентификатор несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="a951a-124">You can receive/retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="a951a-125">Когда приложение устанавливается в каком-либо конкретном контексте, вы получите [ `onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="a951a-125">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="a951a-126">Когда новый пользователь добавляется в контекст, в котором установлено приложение, вы получите [ `onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="a951a-126">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="a951a-127">Вы можете получить [список каналов](~/bots/how-to/get-teams-context.md) в группе, в которой установлено приложение.</span><span class="sxs-lookup"><span data-stu-id="a951a-127">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="a951a-128">Вы можете получить [список членов](~/bots/how-to/get-teams-context.md) группы, установленной на вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="a951a-128">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="a951a-129">Все действия, получаемые с помощью Bot, будут содержать необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="a951a-129">Every Activity your bot receives will contain the necessary information.</span></span>

<span data-ttu-id="a951a-130">Вне зависимости от того, как вы получаете информацию, вам потребуется хранить `tenantId` и один из, `userId` или, `channelId` чтобы создать новую беседу.</span><span class="sxs-lookup"><span data-stu-id="a951a-130">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` in order to create a new conversation.</span></span> <span data-ttu-id="a951a-131">Вы также можете использовать `teamId` для создания нового обсуждения в разделе Общие/по умолчанию в канале команды.</span><span class="sxs-lookup"><span data-stu-id="a951a-131">You can also use the `teamId` to create a new conversation thread in the general/default channel of a team.</span></span>

<span data-ttu-id="a951a-132">`userId`Уникально для идентификатора ленты и определенного пользователя, их нельзя повторно использовать в Боты.</span><span class="sxs-lookup"><span data-stu-id="a951a-132">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="a951a-133">`channelId`Является глобальным, однако для отправки упреждающего сообщения каналу _необходимо_ установить его в команде.</span><span class="sxs-lookup"><span data-stu-id="a951a-133">The `channelId` is global, however your bot _must_ be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="a951a-134">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="a951a-134">Create the conversation</span></span>

<span data-ttu-id="a951a-135">После получения сведений о пользователе и канале необходимо создать беседу, если она еще не существует (или вы не знаете `conversationId` ).</span><span class="sxs-lookup"><span data-stu-id="a951a-135">Once you have the user/channel information, you'll need to create the conversation if it doesn't already exist (or you don't know the `conversationId`).</span></span> <span data-ttu-id="a951a-136">Беседа следует создавать только один раз; обязательно сохраните `conversationId` значение или `conversationReference` объект для использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="a951a-136">You should only create the conversation once; make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="a951a-137">Получение идентификатора беседы</span><span class="sxs-lookup"><span data-stu-id="a951a-137">Get the conversation ID</span></span>

<span data-ttu-id="a951a-138">После создания беседы вы будете использовать `conversationReference` объект, `conversationId` а также и объект `tenantId` для отправки сообщения.</span><span class="sxs-lookup"><span data-stu-id="a951a-138">Once the conversation has been created, you will use either the `conversationReference` object or the `conversationId` and the `tenantId` to send the message.</span></span> <span data-ttu-id="a951a-139">Этот идентификатор можно получить с помощью создания беседы или сохранения его из любого действия, отправленного Вам из этого контекста.</span><span class="sxs-lookup"><span data-stu-id="a951a-139">You can get this Id by either creating the conversation, or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="a951a-140">Убедитесь, что этот идентификатор хранится.</span><span class="sxs-lookup"><span data-stu-id="a951a-140">Make certain that you store this Id.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="a951a-141">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="a951a-141">Send the message</span></span>

<span data-ttu-id="a951a-142">Теперь, когда у вас есть нужные сведения об адресе, вы можете отправить сообщение.</span><span class="sxs-lookup"><span data-stu-id="a951a-142">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="a951a-143">Если вы используете пакет SDK, то можете использовать этот `continueConversation` метод, а также выполнить `conversationId` `tenantId` прямой вызов API.</span><span class="sxs-lookup"><span data-stu-id="a951a-143">If you're using the SDK, you'll do so using the `continueConversation` method,and the `conversationId` and `tenantId` to make a direct API call.</span></span>  <span data-ttu-id="a951a-144">Вам потребуется `conversationParameters` правильно настроить успешную отправку сообщения — просмотрите [примеры](#examples) ниже или воспользуйтесь одним из примеров, приведенных в разделе " [ссылки](#references) ".</span><span class="sxs-lookup"><span data-stu-id="a951a-144">You'll need to set the `conversationParameters` correctly to successfully send your message - see the [examples](#examples) below or use one of the samples listed in the [references](#references) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="a951a-145">Рекомендации по использованию упреждающего обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a951a-145">Best practices for proactive messaging</span></span>

<span data-ttu-id="a951a-146">Отправка упреждающих сообщений пользователям может быть очень эффективным способом общения с пользователями.</span><span class="sxs-lookup"><span data-stu-id="a951a-146">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="a951a-147">Однако с точки зрения это сообщение может быть полностью нежелательным и, в случае приветственных сообщений, будет использоваться при первом взаимодействии с приложением.</span><span class="sxs-lookup"><span data-stu-id="a951a-147">However, from their perspective this message can appear completely unprompted and, in the case of welcome messages, it will be the first time they've interacted with your app.</span></span> <span data-ttu-id="a951a-148">Таким образом, очень важно использовать эту функцию экономно (не спама для пользователей) и предоставить достаточно информации, чтобы пользователи могли понимать, почему они помещаются в сообщениях.</span><span class="sxs-lookup"><span data-stu-id="a951a-148">As such, it is very important to use this functionality sparingly (don't spam your users) and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="a951a-149">Приветственные сообщения</span><span class="sxs-lookup"><span data-stu-id="a951a-149">Welcome messages</span></span>

<span data-ttu-id="a951a-150">При использовании упреждающего обмена сообщениями для отправки пользователю приветственного сообщения необходимо помнить, что для большинства пользователей, получивших сообщение, не будет контекста для их получения.</span><span class="sxs-lookup"><span data-stu-id="a951a-150">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there will be no context for why they are receiving it.</span></span> <span data-ttu-id="a951a-151">Это также происходит в первый раз, когда он будет взаимодействовать с вашим приложением; можно создать хорошее первое впечатление.</span><span class="sxs-lookup"><span data-stu-id="a951a-151">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="a951a-152">Лучшие приветственные сообщения будут включать:</span><span class="sxs-lookup"><span data-stu-id="a951a-152">The best welcome messages will include:</span></span>

* <span data-ttu-id="a951a-153">**Почему пользователь получает сообщение.**</span><span class="sxs-lookup"><span data-stu-id="a951a-153">**Why a user is receiving the message.**</span></span> <span data-ttu-id="a951a-154">Он должен быть очень очевидным, чтобы пользователь получал сообщение.</span><span class="sxs-lookup"><span data-stu-id="a951a-154">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="a951a-155">Если ваш Bot был установлен в канале и вы отправили приветственное сообщение всем пользователям, сообщите им о том, в каком канале он был установлен и кто его установил.</span><span class="sxs-lookup"><span data-stu-id="a951a-155">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="a951a-156">**Что вы предоставляете.**</span><span class="sxs-lookup"><span data-stu-id="a951a-156">**What do you offer.**</span></span> <span data-ttu-id="a951a-157">Что можно делать с приложением?</span><span class="sxs-lookup"><span data-stu-id="a951a-157">What can they do with your app?</span></span> <span data-ttu-id="a951a-158">Какое значение можно перенести?</span><span class="sxs-lookup"><span data-stu-id="a951a-158">What value can you bring to them?</span></span>
* <span data-ttu-id="a951a-159">**Что делать дальше.**</span><span class="sxs-lookup"><span data-stu-id="a951a-159">**What should they do next.**</span></span> <span data-ttu-id="a951a-160">Пригласите их, чтобы испытать команду или взаимодействовать с приложением каким бы то ни было способом.</span><span class="sxs-lookup"><span data-stu-id="a951a-160">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="a951a-161">Помните, что неудачные приветственные сообщения могут приводить к блокированию ленты.</span><span class="sxs-lookup"><span data-stu-id="a951a-161">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="a951a-162">Вы должны тратить много времени на создание приветственных сообщений и перебирать их, если это не оказывает желаемого результата.</span><span class="sxs-lookup"><span data-stu-id="a951a-162">You should spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="a951a-163">Сообщения уведомления</span><span class="sxs-lookup"><span data-stu-id="a951a-163">Notification messages</span></span>

<span data-ttu-id="a951a-164">При использовании упреждающего обмена сообщениями для отправки уведомлений необходимо убедиться, что у пользователей есть четко заданный путь, чтобы выполнять общие действия на основе уведомления и ясно понять, почему возникло уведомление.</span><span class="sxs-lookup"><span data-stu-id="a951a-164">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="a951a-165">К хорошим сообщениям уведомления обычно относятся:</span><span class="sxs-lookup"><span data-stu-id="a951a-165">Good notification messages will generally include:</span></span>

* <span data-ttu-id="a951a-166">**Что случилось.**</span><span class="sxs-lookup"><span data-stu-id="a951a-166">**What happened.**</span></span> <span data-ttu-id="a951a-167">Четкое указание того, что произошло с причиной уведомления.</span><span class="sxs-lookup"><span data-stu-id="a951a-167">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="a951a-168">**Каков результат.**</span><span class="sxs-lookup"><span data-stu-id="a951a-168">**What was the result.**</span></span> <span data-ttu-id="a951a-169">Должно быть ясно, какие элементы/вещи были обновлены, чтобы получить уведомление.</span><span class="sxs-lookup"><span data-stu-id="a951a-169">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="a951a-170">**Кто/что активировал его.**</span><span class="sxs-lookup"><span data-stu-id="a951a-170">**Who/what triggered it.**</span></span> <span data-ttu-id="a951a-171">Кто или что приняло действие, вызвавшее отправку уведомления.</span><span class="sxs-lookup"><span data-stu-id="a951a-171">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="a951a-172">**Что может делать пользователи в ответе.**</span><span class="sxs-lookup"><span data-stu-id="a951a-172">**What can users do in response.**</span></span> <span data-ttu-id="a951a-173">Облегчить пользователям выполнение действий в соответствии с вашими уведомлениями.</span><span class="sxs-lookup"><span data-stu-id="a951a-173">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="a951a-174">**Как пользователи могут отказаться.** Необходимо указать путь для пользователей, чтобы отказаться от дополнительных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a951a-174">**How can users opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="a951a-175">Заактивная установка приложения с помощью Graph</span><span class="sxs-lookup"><span data-stu-id="a951a-175">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="a951a-176">Активная установка приложений с помощью Microsoft Graph в настоящее время находится на стадии бета-тестирования.</span><span class="sxs-lookup"><span data-stu-id="a951a-176">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="a951a-177">Иногда это может потребоваться для упреждающего сообщения пользователей, которые ранее не устанавливали приложение или не работали с ним.</span><span class="sxs-lookup"><span data-stu-id="a951a-177">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="a951a-178">Например, вы хотите использовать [Communicator компании](~/samples/app-templates.md#company-communicator) для отправки сообщений во всю организацию.</span><span class="sxs-lookup"><span data-stu-id="a951a-178">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="a951a-179">В этом сценарии можно использовать API Graph для профилактической установки приложения для пользователей, а затем кэшировать необходимые значения из события, которое `conversationUpdate` получит ваше приложение после установки.</span><span class="sxs-lookup"><span data-stu-id="a951a-179">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="a951a-180">Вы можете устанавливать только приложения, которые находятся в каталоге организационных приложений или в магазине приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="a951a-180">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="a951a-181">Ознакомьтесь с разделом [Установка приложений для пользователей](/graph/teams-proactive-messaging) в документации Graph, а также об [активных установках и обмене сообщениями в Teams с Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="a951a-181">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="a951a-182">Кроме того, на платформе GitHub существует [пример Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  .</span><span class="sxs-lookup"><span data-stu-id="a951a-182">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="a951a-183">Примеры</span><span class="sxs-lookup"><span data-stu-id="a951a-183">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="a951a-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="a951a-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
private async Task MessageAllMembersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var teamsChannelId = turnContext.Activity.TeamsGetChannelId();
    var serviceUrl = turnContext.Activity.ServiceUrl;
    var credentials = new MicrosoftAppCredentials(_appId, _appPassword);
    ConversationReference conversationReference = null;

    //Get the set of member IDs to send the message to
    var members = await GetPagedMembers(turnContext, cancellationToken);

    foreach (var teamMember in members)
    {
        var proactiveMessage = MessageFactory.Text($"Hello {teamMember.GivenName} {teamMember.Surname}. I'm a Teams conversation bot.");

        var conversationParameters = new ConversationParameters
        {
            IsGroup = false,
            Bot = turnContext.Activity.Recipient,
            Members = new ChannelAccount[] { teamMember },
            TenantId = turnContext.Activity.Conversation.TenantId,
        };
        //create the new one-to-one conversations
        await ((BotFrameworkAdapter)turnContext.Adapter).CreateConversationAsync(
            teamsChannelId,
            serviceUrl,
            credentials,
            conversationParameters,
            async (t1, c1) =>
            {
                //Get the conversationReference
                conversationReference = t1.Activity.GetConversationReference();
                //Send the proactive message
                await ((BotFrameworkAdapter)turnContext.Adapter).ContinueConversationAsync(
                    _appId,
                    conversationReference,
                    async (t2, c2) =>
                    {
                        await t2.SendActivityAsync(proactiveMessage, c2);
                    },
                    cancellationToken);
            },
            cancellationToken);
    }

    await turnContext.SendActivityAsync(MessageFactory.Text("All messages have been sent."), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="a951a-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="a951a-185">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="a951a-186">Python</span><span class="sxs-lookup"><span data-stu-id="a951a-186">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="a951a-187">JSON</span><span class="sxs-lookup"><span data-stu-id="a951a-187">JSON</span></span>](#tab/json)

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

<span data-ttu-id="a951a-188">Необходимо указать идентификатор пользователя и идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="a951a-188">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="a951a-189">Если вызов завершается успешно, API возвращает следующий объект Response.</span><span class="sxs-lookup"><span data-stu-id="a951a-189">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="references"></a><span data-ttu-id="a951a-190">Ссылки</span><span class="sxs-lookup"><span data-stu-id="a951a-190">References</span></span>

<span data-ttu-id="a951a-191">Ниже приведены официальные примеры профилактического упреждающего обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="a951a-191">The official proactive messaging samples are listed below.</span></span>

|  <span data-ttu-id="a951a-192">Нет.</span><span class="sxs-lookup"><span data-stu-id="a951a-192">No.</span></span>  | <span data-ttu-id="a951a-193">Имя примера</span><span class="sxs-lookup"><span data-stu-id="a951a-193">Sample Name</span></span>           | <span data-ttu-id="a951a-194">Описание</span><span class="sxs-lookup"><span data-stu-id="a951a-194">Description</span></span>                                                                      | <span data-ttu-id="a951a-195">.NET</span><span class="sxs-lookup"><span data-stu-id="a951a-195">.NET</span></span>    | <span data-ttu-id="a951a-196">JavaScript</span><span class="sxs-lookup"><span data-stu-id="a951a-196">JavaScript</span></span>   | <span data-ttu-id="a951a-197">Python</span><span class="sxs-lookup"><span data-stu-id="a951a-197">Python</span></span>  |
|:--:|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="a951a-198">57</span><span class="sxs-lookup"><span data-stu-id="a951a-198">57</span></span>|<span data-ttu-id="a951a-199">Основные сведения о беседах Teams</span><span class="sxs-lookup"><span data-stu-id="a951a-199">Teams Conversation Basics</span></span>  | <span data-ttu-id="a951a-200">Демонстрируются основные принципы бесед в Microsoft Teams, включая отправку одного и того же упреждающего сообщения.</span><span class="sxs-lookup"><span data-stu-id="a951a-200">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="a951a-201">&nbsp;Ядро .NET</span><span class="sxs-lookup"><span data-stu-id="a951a-201">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="a951a-202">JavaScript</span><span class="sxs-lookup"><span data-stu-id="a951a-202">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="a951a-203">Python</span><span class="sxs-lookup"><span data-stu-id="a951a-203">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="a951a-204">58</span><span class="sxs-lookup"><span data-stu-id="a951a-204">58</span></span>|<span data-ttu-id="a951a-205">Запуск нового потока в канале</span><span class="sxs-lookup"><span data-stu-id="a951a-205">Start new thread in a channel</span></span>     | <span data-ttu-id="a951a-206">Демонстрация создания нового потока в канале.</span><span class="sxs-lookup"><span data-stu-id="a951a-206">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="a951a-207">&nbsp;Ядро .NET</span><span class="sxs-lookup"><span data-stu-id="a951a-207">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="a951a-208">JavaScript</span><span class="sxs-lookup"><span data-stu-id="a951a-208">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="a951a-209">Python</span><span class="sxs-lookup"><span data-stu-id="a951a-209">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

<span data-ttu-id="a951a-210">В приведенном ниже примере показано минимальное количество сведений, необходимых для отправки упреждающего сообщения (без использования `conversationReference` объекта).</span><span class="sxs-lookup"><span data-stu-id="a951a-210">The sample below demonstrates the minimal amount of information needed to send a proactive message (without using a `conversationReference` object).</span></span> <span data-ttu-id="a951a-211">Этот пример может быть полезен, если вы используете вызовы REST API напрямую или не сохраняли полные `conversationReference` объекты.</span><span class="sxs-lookup"><span data-stu-id="a951a-211">This sample can be useful if you're using REST API calls directly, or haven't been storing full `conversationReference` objects.</span></span>

* [<span data-ttu-id="a951a-212">Активные системы обмена сообщениями Teams</span><span class="sxs-lookup"><span data-stu-id="a951a-212">Teams Proactive Messaging</span></span>](https://github.com/clearab/teamsProactiveMessaging)

## <a name="view-additional-code"></a><span data-ttu-id="a951a-213">Просмотр дополнительного кода</span><span class="sxs-lookup"><span data-stu-id="a951a-213">View additional code</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a951a-214">**Примеры кода для активных сообщений Teams**</span><span class="sxs-lookup"><span data-stu-id="a951a-214">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>