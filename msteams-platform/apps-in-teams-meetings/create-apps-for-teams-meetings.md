---
title: Необходимые условия и ссылки на API для приложений в собраниях Teams
author: surbhigupta
description: Работа с приложениями для Teams собраний
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams apps meetings user participant role api
ms.openlocfilehash: 38a7a5fdf9794fb95b4141f2c73e8282a9bf8601
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211592"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a><span data-ttu-id="69a8f-104">Необходимые условия и ссылки на API для приложений в собраниях Teams</span><span class="sxs-lookup"><span data-stu-id="69a8f-104">Prerequisites and API references for apps in Teams meetings</span></span>

<span data-ttu-id="69a8f-105">Чтобы расширить возможности ваших приложений на протяжении жизненного цикла собраний, Teams позволяет работать с приложениями для Teams собраний.</span><span class="sxs-lookup"><span data-stu-id="69a8f-105">To expand the capabilities of your apps across the meeting lifecycle, Teams enables you to work with apps for Teams meetings.</span></span> <span data-ttu-id="69a8f-106">Необходимо пройти необходимые условия и использовать ссылки API приложений для собраний для улучшения работы с собраниями.</span><span class="sxs-lookup"><span data-stu-id="69a8f-106">You must  go through the prerequisites and you can use the meeting apps API references to enhance the meeting experience.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69a8f-107">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="69a8f-107">Prerequisites</span></span>

<span data-ttu-id="69a8f-108">Прежде чем работать с приложениями для Teams собраний, необходимо иметь представление о следующем:</span><span class="sxs-lookup"><span data-stu-id="69a8f-108">Before you work with apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="69a8f-109">Вы должны иметь знания о разработке Teams приложений.</span><span class="sxs-lookup"><span data-stu-id="69a8f-109">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="69a8f-110">Дополнительные сведения см. [в Teams разработки приложения.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="69a8f-110">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="69a8f-111">Необходимо обновить манифест Teams, чтобы указать, что приложение доступно для собраний.</span><span class="sxs-lookup"><span data-stu-id="69a8f-111">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="69a8f-112">Дополнительные сведения см. в [манифесте приложения.](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="69a8f-112">For more information, see [app manifest](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span></span>

* <span data-ttu-id="69a8f-113">Ваше приложение должно поддерживать настраиваемые вкладки в области группового чата, чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки. Дополнительные сведения см. в [поле groupchat и](../resources/schema/manifest-schema.md#configurabletabs) [создайте вкладку группы.](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="69a8f-113">Your app must support configurable tabs in the groupchat scope, for your app to function in the meeting lifecycle as a tab. For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="69a8f-114">Необходимо придерживаться общих Teams правил разработки вкладок для сценариев до и после собрания.</span><span class="sxs-lookup"><span data-stu-id="69a8f-114">You must adhere to general Teams tab design guidelines for pre and post-meeting scenarios.</span></span> <span data-ttu-id="69a8f-115">Для работы во время собраний обратитесь к вкладке на собрании и рекомендациям по проектированию диалогов на собрании.</span><span class="sxs-lookup"><span data-stu-id="69a8f-115">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="69a8f-116">Дополнительные сведения см. [Teams](../tabs/design/tabs.md)руководства по разработке вкладок, [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)рекомендации по проектированию вкладок на собрании и рекомендации по проектированию диалогов на [собрании.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="69a8f-116">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab), and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="69a8f-117">Необходимо поддерживать область, чтобы включить приложение в чаты перед собранием и `groupchat` после собрания.</span><span class="sxs-lookup"><span data-stu-id="69a8f-117">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="69a8f-118">С помощью предварительного собрания приложения можно найти и добавить приложения для собраний и выполнить задачи перед собранием.</span><span class="sxs-lookup"><span data-stu-id="69a8f-118">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="69a8f-119">С помощью приложения после собрания можно просмотреть результаты собрания, такие как результаты опроса или отзывы.</span><span class="sxs-lookup"><span data-stu-id="69a8f-119">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="69a8f-120">Параметры URL-адресов API должны иметь `meetingId` и `userId` `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="69a8f-120">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="69a8f-121">Они доступны в рамках Teams клиентской SDK и бот-активности.</span><span class="sxs-lookup"><span data-stu-id="69a8f-121">These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="69a8f-122">Кроме того, вы можете получить достоверную информацию для идентификации пользователя и идентификации клиента с помощью вкладки [SSO authentication.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="69a8f-122">In addition, you can retrieve reliable information for user ID and tenant ID using [tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="69a8f-123">API `GetParticipant` должен иметь регистрацию бота и ID для создания маркеров auth.</span><span class="sxs-lookup"><span data-stu-id="69a8f-123">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="69a8f-124">Дополнительные сведения см. в [сведениях о регистрации ботов и ID.](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="69a8f-124">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="69a8f-125">Чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть обновлено в зависимости от событий на собрании.</span><span class="sxs-lookup"><span data-stu-id="69a8f-125">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="69a8f-126">Эти события могут быть в диалоговом окне собрания и на других этапах жизненного цикла собрания.</span><span class="sxs-lookup"><span data-stu-id="69a8f-126">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="69a8f-127">Параметр завершения в диалоговом окне на собрании `bot Id` см. в `NotificationSignal` API.</span><span class="sxs-lookup"><span data-stu-id="69a8f-127">For the in-meeting dialog box, see completion `bot Id` parameter in `NotificationSignal` API.</span></span>

* <span data-ttu-id="69a8f-128">API сведений о собраниях должен иметь регистрацию бота и бот-ID.</span><span class="sxs-lookup"><span data-stu-id="69a8f-128">Meeting Details API must have a bot registration and bot ID.</span></span> <span data-ttu-id="69a8f-129">Для этого требуется бот SDK для получения `TurnContext` .</span><span class="sxs-lookup"><span data-stu-id="69a8f-129">It requires Bot SDK to get `TurnContext`.</span></span>

* <span data-ttu-id="69a8f-130">Для событий собраний в режиме реального времени необходимо ознакомиться с объектом, доступным `TurnContext` через SDK Bot.</span><span class="sxs-lookup"><span data-stu-id="69a8f-130">For real-time meeting events, you must be familiar with the `TurnContext` object available through the Bot SDK.</span></span> <span data-ttu-id="69a8f-131">Объект `Activity` содержит `TurnContext` полезной нагрузки с фактическим временем начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="69a8f-131">The `Activity` object in `TurnContext` contains the payload with the actual start and end time.</span></span> <span data-ttu-id="69a8f-132">Для проведения собраний в режиме реального времени требуется зарегистрированный бот-ИД с Teams платформы.</span><span class="sxs-lookup"><span data-stu-id="69a8f-132">Real-time meeting events require a registered bot ID from the Teams platform.</span></span>

<span data-ttu-id="69a8f-133">После того как вы прошли необходимые условия, вы можете использовать ссылки API приложений собраний , и API сведений о собраниях, которые позволяют получать доступ к информации с помощью атрибутов и отображать соответствующий `GetUserContext` `GetParticipant` `NotificationSignal` контент.</span><span class="sxs-lookup"><span data-stu-id="69a8f-133">After you have gone through the prerequisites, you can use the meeting apps API references `GetUserContext`, `GetParticipant`, `NotificationSignal`, and Meeting Details API that enable you to access information using attributes and display relevant content.</span></span>

## <a name="meeting-apps-api-references"></a><span data-ttu-id="69a8f-134">Ссылки на API приложений для собраний</span><span class="sxs-lookup"><span data-stu-id="69a8f-134">Meeting apps API references</span></span>

<span data-ttu-id="69a8f-135">Новые функции собраний предоставляют API, которые преобразовывают возможности собраний.</span><span class="sxs-lookup"><span data-stu-id="69a8f-135">The new meeting extensibilities provide you with APIs that transform the meeting experience.</span></span> <span data-ttu-id="69a8f-136">С помощью этой новой возможности можно создавать приложения или интегрировать существующие приложения в жизненный цикл собрания.</span><span class="sxs-lookup"><span data-stu-id="69a8f-136">With this new capability, you can build apps or integrate existing apps within the meeting lifecycle.</span></span> <span data-ttu-id="69a8f-137">Вы можете использовать API для того, чтобы ваше приложение знало о собрании.</span><span class="sxs-lookup"><span data-stu-id="69a8f-137">You can use the APIs to make your app aware of the meeting.</span></span> <span data-ttu-id="69a8f-138">Вы можете выбрать API, которые необходимо использовать для повышения качества работы собраний.</span><span class="sxs-lookup"><span data-stu-id="69a8f-138">You can choose which APIs you want to use to enhance the meeting experience.</span></span>

<span data-ttu-id="69a8f-139">В следующей таблице приводится список этих API:</span><span class="sxs-lookup"><span data-stu-id="69a8f-139">The following table provides a list of these APIs:</span></span>

|<span data-ttu-id="69a8f-140">API</span><span class="sxs-lookup"><span data-stu-id="69a8f-140">API</span></span>|<span data-ttu-id="69a8f-141">Описание</span><span class="sxs-lookup"><span data-stu-id="69a8f-141">Description</span></span>|<span data-ttu-id="69a8f-142">Запрос</span><span class="sxs-lookup"><span data-stu-id="69a8f-142">Request</span></span>|<span data-ttu-id="69a8f-143">Источник</span><span class="sxs-lookup"><span data-stu-id="69a8f-143">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="69a8f-144">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="69a8f-144">**GetUserContext**</span></span>| <span data-ttu-id="69a8f-145">Этот API позволяет получать контекстную информацию для отображения соответствующего контента на вкладке Teams.</span><span class="sxs-lookup"><span data-stu-id="69a8f-145">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="69a8f-146">_**microsoftTeams.getContext() => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="69a8f-146">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="69a8f-147">Microsoft Teams Клиентская SDK</span><span class="sxs-lookup"><span data-stu-id="69a8f-147">Microsoft Teams Client SDK</span></span>|
|<span data-ttu-id="69a8f-148">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="69a8f-148">**GetParticipant**</span></span>| <span data-ttu-id="69a8f-149">Этот API позволяет боту получать сведения о участниках, встречая ID и ID участника.</span><span class="sxs-lookup"><span data-stu-id="69a8f-149">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="69a8f-150">**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="69a8f-150">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="69a8f-151">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="69a8f-151">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="69a8f-152">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="69a8f-152">**NotificationSignal**</span></span> | <span data-ttu-id="69a8f-153">Этот API позволяет предоставлять сигналы собрания, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота.</span><span class="sxs-lookup"><span data-stu-id="69a8f-153">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="69a8f-154">Он позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно на собрании.</span><span class="sxs-lookup"><span data-stu-id="69a8f-154">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="69a8f-155">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="69a8f-155">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="69a8f-156">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="69a8f-156">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="69a8f-157">**Сведения о собрании**</span><span class="sxs-lookup"><span data-stu-id="69a8f-157">**Meeting Details**</span></span> | <span data-ttu-id="69a8f-158">Этот API позволяет получать статические метаданные собраний.</span><span class="sxs-lookup"><span data-stu-id="69a8f-158">This API enables you to get static meeting metadata.</span></span> |<span data-ttu-id="69a8f-159">**GET** _**/v1/meetings/{meetingId}**_</span><span class="sxs-lookup"><span data-stu-id="69a8f-159">**GET** _**/v1/meetings/{meetingId}**_</span></span>| <span data-ttu-id="69a8f-160">Bot SDK</span><span class="sxs-lookup"><span data-stu-id="69a8f-160">Bot SDK</span></span> |

### <a name="getusercontext-api"></a><span data-ttu-id="69a8f-161">GetUserContext API</span><span class="sxs-lookup"><span data-stu-id="69a8f-161">GetUserContext API</span></span>

<span data-ttu-id="69a8f-162">Чтобы определить и получить контекстную информацию для содержимого вкладки, см. в этой Teams [контексте.](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library) `meetingId`используется вкладками при работе в контексте собрания и добавляется для полезной нагрузки ответа.</span><span class="sxs-lookup"><span data-stu-id="69a8f-162">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="69a8f-163">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="69a8f-163">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="69a8f-164">Не кэшить роли участников, так как организатор собрания может изменить роли в любое время.</span><span class="sxs-lookup"><span data-stu-id="69a8f-164">Do not cache participant roles since the meeting organizer can change the roles any time.</span></span>
> * <span data-ttu-id="69a8f-165">Teams в настоящее время не поддерживает большие списки рассылки или размеры реестра более 350 участников `GetParticipant` для API.</span><span class="sxs-lookup"><span data-stu-id="69a8f-165">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

<span data-ttu-id="69a8f-166">API позволяет боту получать сведения о `GetParticipant` участниках, встречая ID и ID участника.</span><span class="sxs-lookup"><span data-stu-id="69a8f-166">The `GetParticipant` API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> <span data-ttu-id="69a8f-167">API включает параметры запросов, примеры и коды ответа.</span><span class="sxs-lookup"><span data-stu-id="69a8f-167">The API includes query parameters, examples, and response codes.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="69a8f-168">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="69a8f-168">Query parameters</span></span>

<span data-ttu-id="69a8f-169">API `GetParticipant` включает следующие параметры запроса:</span><span class="sxs-lookup"><span data-stu-id="69a8f-169">The `GetParticipant` API includes the following query parameters:</span></span>

|<span data-ttu-id="69a8f-170">Значение</span><span class="sxs-lookup"><span data-stu-id="69a8f-170">Value</span></span>|<span data-ttu-id="69a8f-171">Тип</span><span class="sxs-lookup"><span data-stu-id="69a8f-171">Type</span></span>|<span data-ttu-id="69a8f-172">Обязательный</span><span class="sxs-lookup"><span data-stu-id="69a8f-172">Required</span></span>|<span data-ttu-id="69a8f-173">Описание</span><span class="sxs-lookup"><span data-stu-id="69a8f-173">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="69a8f-174">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="69a8f-174">**meetingId**</span></span>| <span data-ttu-id="69a8f-175">String</span><span class="sxs-lookup"><span data-stu-id="69a8f-175">String</span></span> | <span data-ttu-id="69a8f-176">Да</span><span class="sxs-lookup"><span data-stu-id="69a8f-176">Yes</span></span> | <span data-ttu-id="69a8f-177">Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK.</span><span class="sxs-lookup"><span data-stu-id="69a8f-177">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="69a8f-178">**participantId**</span><span class="sxs-lookup"><span data-stu-id="69a8f-178">**participantId**</span></span>| <span data-ttu-id="69a8f-179">String</span><span class="sxs-lookup"><span data-stu-id="69a8f-179">String</span></span> | <span data-ttu-id="69a8f-180">Да</span><span class="sxs-lookup"><span data-stu-id="69a8f-180">Yes</span></span> | <span data-ttu-id="69a8f-181">ID участника — это пользовательский ИД.</span><span class="sxs-lookup"><span data-stu-id="69a8f-181">The participant ID is the user ID.</span></span> <span data-ttu-id="69a8f-182">Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK.</span><span class="sxs-lookup"><span data-stu-id="69a8f-182">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="69a8f-183">Рекомендуется получить ID участника из SSO Tab.</span><span class="sxs-lookup"><span data-stu-id="69a8f-183">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="69a8f-184">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="69a8f-184">**tenantId**</span></span>| <span data-ttu-id="69a8f-185">Строка</span><span class="sxs-lookup"><span data-stu-id="69a8f-185">String</span></span> | <span data-ttu-id="69a8f-186">Да</span><span class="sxs-lookup"><span data-stu-id="69a8f-186">Yes</span></span> | <span data-ttu-id="69a8f-187">Для пользователей-клиентов требуется ID клиента.</span><span class="sxs-lookup"><span data-stu-id="69a8f-187">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="69a8f-188">Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK.</span><span class="sxs-lookup"><span data-stu-id="69a8f-188">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="69a8f-189">Рекомендуется получить ID клиента из SSO tab.</span><span class="sxs-lookup"><span data-stu-id="69a8f-189">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="69a8f-190">Пример</span><span class="sxs-lookup"><span data-stu-id="69a8f-190">Example</span></span>

<span data-ttu-id="69a8f-191">API `GetParticipant` содержит следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="69a8f-191">The `GetParticipant` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="69a8f-192">C#</span><span class="sxs-lookup"><span data-stu-id="69a8f-192">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}

```

# <a name="javascript"></a>[<span data-ttu-id="69a8f-193">JavaScript</span><span class="sxs-lookup"><span data-stu-id="69a8f-193">JavaScript</span></span>](#tab/javascript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = getMeetingParticipant(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="69a8f-194">JSON</span><span class="sxs-lookup"><span data-stu-id="69a8f-194">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

---

<span data-ttu-id="69a8f-195">Тело ответа JSON для `GetParticipant` API:</span><span class="sxs-lookup"><span data-stu-id="69a8f-195">The JSON response body for `GetParticipant` API is:</span></span>

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"e236c4bf-88b1-4f3a-b1d7-8891dfc332b5",
      "name":"Bob Young",
      "givenName":"Bob",
      "surname":"Young",
      "email":"Bob.young@microsoft.com",
      "userPrincipalName":"Bob.young@microsoft.com",
      "tenantId":"2fe477ab-0efc-4dfd-bde2-484374e2c373",
      "userRole":"user"
   },
   "meeting":{
      "role ":"Presenter",
      "inMeeting":true
   },
   "conversation":{
      "id":"<conversation id>",
      "isGroup":true
   }
}
```

#### <a name="response-codes"></a><span data-ttu-id="69a8f-196">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="69a8f-196">Response codes</span></span>

<span data-ttu-id="69a8f-197">API `GetParticipant` включает в себя следующие коды ответа:</span><span class="sxs-lookup"><span data-stu-id="69a8f-197">The `GetParticipant` API includes the following response codes:</span></span>

|<span data-ttu-id="69a8f-198">Код ответа</span><span class="sxs-lookup"><span data-stu-id="69a8f-198">Response code</span></span>|<span data-ttu-id="69a8f-199">Описание</span><span class="sxs-lookup"><span data-stu-id="69a8f-199">Description</span></span>|
|---|---|
| <span data-ttu-id="69a8f-200">**403**</span><span class="sxs-lookup"><span data-stu-id="69a8f-200">**403**</span></span> | <span data-ttu-id="69a8f-201">Приложение не может получать сведения о участниках.</span><span class="sxs-lookup"><span data-stu-id="69a8f-201">The app is not allowed to get participant information.</span></span> <span data-ttu-id="69a8f-202">Это наиболее распространенный ответ на ошибки, который запускается, если приложение не установлено на собрании.</span><span class="sxs-lookup"><span data-stu-id="69a8f-202">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="69a8f-203">Например, если приложение отключено администратором клиента или заблокировано во время переноса веб-сайтов в прямом эфире.</span><span class="sxs-lookup"><span data-stu-id="69a8f-203">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="69a8f-204">**200**</span><span class="sxs-lookup"><span data-stu-id="69a8f-204">**200**</span></span> | <span data-ttu-id="69a8f-205">Данные участника успешно извлекаются.</span><span class="sxs-lookup"><span data-stu-id="69a8f-205">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="69a8f-206">**401**</span><span class="sxs-lookup"><span data-stu-id="69a8f-206">**401**</span></span> | <span data-ttu-id="69a8f-207">Приложение отвечает недействительным маркером.</span><span class="sxs-lookup"><span data-stu-id="69a8f-207">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="69a8f-208">**404**</span><span class="sxs-lookup"><span data-stu-id="69a8f-208">**404**</span></span> | <span data-ttu-id="69a8f-209">Собрание истеко или участник не может быть найден.</span><span class="sxs-lookup"><span data-stu-id="69a8f-209">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="69a8f-210">**500**</span><span class="sxs-lookup"><span data-stu-id="69a8f-210">**500**</span></span> | <span data-ttu-id="69a8f-211">Срок действия собрания истек (более 60 дней) с момента окончания собрания, или у участников нет разрешений, основанных на их роли.</span><span class="sxs-lookup"><span data-stu-id="69a8f-211">The meeting has either expired (more than 60 days) since the meeting ended or the participants do not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="69a8f-212">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="69a8f-212">NotificationSignal API</span></span>

<span data-ttu-id="69a8f-213">Все пользователи на собрании получают уведомления, отправленные через `NotificationSignal` API.</span><span class="sxs-lookup"><span data-stu-id="69a8f-213">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="69a8f-214">При вызове диалогового окна на собрании содержимое представляется в качестве сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="69a8f-214">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="69a8f-215">В настоящее время отправка целевых уведомлений не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="69a8f-215">Currently, sending targeted notifications is not supported.</span></span>

<span data-ttu-id="69a8f-216">`NotificationSignal` API позволяет предоставлять сигналы собраний, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота.</span><span class="sxs-lookup"><span data-stu-id="69a8f-216">`NotificationSignal` API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="69a8f-217">Этот API позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно в собрании.</span><span class="sxs-lookup"><span data-stu-id="69a8f-217">This API allows you to signal based on user action that shows an in-meeting dialog box.</span></span> <span data-ttu-id="69a8f-218">API включает параметр запроса, примеры и коды ответа.</span><span class="sxs-lookup"><span data-stu-id="69a8f-218">The API includes query parameter, examples, and response codes.</span></span>

#### <a name="query-parameter"></a><span data-ttu-id="69a8f-219">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="69a8f-219">Query parameter</span></span>

<span data-ttu-id="69a8f-220">API `NotificationSignal` включает в себя следующий параметр запроса:</span><span class="sxs-lookup"><span data-stu-id="69a8f-220">The `NotificationSignal` API includes the following query parameter:</span></span>

|<span data-ttu-id="69a8f-221">Значение</span><span class="sxs-lookup"><span data-stu-id="69a8f-221">Value</span></span>|<span data-ttu-id="69a8f-222">Тип</span><span class="sxs-lookup"><span data-stu-id="69a8f-222">Type</span></span>|<span data-ttu-id="69a8f-223">Обязательный</span><span class="sxs-lookup"><span data-stu-id="69a8f-223">Required</span></span>|<span data-ttu-id="69a8f-224">Описание</span><span class="sxs-lookup"><span data-stu-id="69a8f-224">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="69a8f-225">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="69a8f-225">**conversationId**</span></span>| <span data-ttu-id="69a8f-226">Строка</span><span class="sxs-lookup"><span data-stu-id="69a8f-226">String</span></span> | <span data-ttu-id="69a8f-227">Да</span><span class="sxs-lookup"><span data-stu-id="69a8f-227">Yes</span></span> | <span data-ttu-id="69a8f-228">Идентификатор беседы доступен в рамках Bot Invoke.</span><span class="sxs-lookup"><span data-stu-id="69a8f-228">The conversation identifier is available as part of Bot Invoke.</span></span> |

#### <a name="examples"></a><span data-ttu-id="69a8f-229">Примеры</span><span class="sxs-lookup"><span data-stu-id="69a8f-229">Examples</span></span>

<span data-ttu-id="69a8f-230">Объявляется `Bot ID` в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="69a8f-230">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="69a8f-231">Параметр `completionBotId` необязательный `externalResourceUrl` в примере запрашиваемой полезной нагрузки.</span><span class="sxs-lookup"><span data-stu-id="69a8f-231">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="69a8f-232">`Bot ID` объявляется в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="69a8f-232">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="69a8f-233">Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях.</span><span class="sxs-lookup"><span data-stu-id="69a8f-233">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="69a8f-234">Чтобы размеры были в пределах допустимого, см. в [рекомендациях по проектированию.](design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="69a8f-234">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="69a8f-235">URL-адрес — это страница, загруженная в диалоговом окне на `<iframe>` собрании.</span><span class="sxs-lookup"><span data-stu-id="69a8f-235">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="69a8f-236">Домен должен быть в массиве приложения в `validDomains` манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="69a8f-236">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

<span data-ttu-id="69a8f-237">API `NotificationSignal` содержит следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="69a8f-237">The `NotificationSignal` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="69a8f-238">C#</span><span class="sxs-lookup"><span data-stu-id="69a8f-238">C#</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");

activity.ChannelData = new TeamsChannelData
  {
    Notification = new NotificationInfo()
                    {
                        AlertInMeeting = true,
                        ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
                    }
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="69a8f-239">JavaScript</span><span class="sxs-lookup"><span data-stu-id="69a8f-239">JavaScript</span></span>](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

# <a name="json"></a>[<span data-ttu-id="69a8f-240">JSON</span><span class="sxs-lookup"><span data-stu-id="69a8f-240">JSON</span></span>](#tab/json)

```http
POST /v3/conversations/{conversationId}/activities

{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

---

#### <a name="response-codes"></a><span data-ttu-id="69a8f-241">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="69a8f-241">Response codes</span></span>

<span data-ttu-id="69a8f-242">API `NotificationSignal` включает в себя следующие коды ответа:</span><span class="sxs-lookup"><span data-stu-id="69a8f-242">The `NotificationSignal` API includes the following response codes:</span></span>

|<span data-ttu-id="69a8f-243">Код ответа</span><span class="sxs-lookup"><span data-stu-id="69a8f-243">Response code</span></span>|<span data-ttu-id="69a8f-244">Описание</span><span class="sxs-lookup"><span data-stu-id="69a8f-244">Description</span></span>|
|---|---|
| <span data-ttu-id="69a8f-245">**201**</span><span class="sxs-lookup"><span data-stu-id="69a8f-245">**201**</span></span> | <span data-ttu-id="69a8f-246">Успешно отправляется действие с сигналом.</span><span class="sxs-lookup"><span data-stu-id="69a8f-246">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="69a8f-247">**401**</span><span class="sxs-lookup"><span data-stu-id="69a8f-247">**401**</span></span> | <span data-ttu-id="69a8f-248">Приложение отвечает недействительным маркером.</span><span class="sxs-lookup"><span data-stu-id="69a8f-248">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="69a8f-249">**403**</span><span class="sxs-lookup"><span data-stu-id="69a8f-249">**403**</span></span> | <span data-ttu-id="69a8f-250">Приложение не может отправить сигнал.</span><span class="sxs-lookup"><span data-stu-id="69a8f-250">The app is unable to send the signal.</span></span> <span data-ttu-id="69a8f-251">Это может произойти из-за различных причин, таких как отключение приложения администратором клиента, блокировка приложения во время переноса веб-сайта в прямом эфире и так далее.</span><span class="sxs-lookup"><span data-stu-id="69a8f-251">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="69a8f-252">В этом случае полезное сообщение содержит подробное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="69a8f-252">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="69a8f-253">**404**</span><span class="sxs-lookup"><span data-stu-id="69a8f-253">**404**</span></span> | <span data-ttu-id="69a8f-254">Чат собрания не существует.</span><span class="sxs-lookup"><span data-stu-id="69a8f-254">The meeting chat does not exist.</span></span> |

### <a name="meeting-details-api"></a><span data-ttu-id="69a8f-255">API сведений о собраниях</span><span class="sxs-lookup"><span data-stu-id="69a8f-255">Meeting Details API</span></span>

> [!NOTE]
> <span data-ttu-id="69a8f-256">В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../resources/dev-preview/developer-preview-intro.md) разработчиков.</span><span class="sxs-lookup"><span data-stu-id="69a8f-256">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="69a8f-257">API сведений о собраниях позволяет приложению получать статические метаданные собраний.</span><span class="sxs-lookup"><span data-stu-id="69a8f-257">The Meeting Details API enables your app to get static meeting metadata.</span></span> <span data-ttu-id="69a8f-258">Это точки данных, которые не изменяются динамически.</span><span class="sxs-lookup"><span data-stu-id="69a8f-258">These are data points that do not change dynamically.</span></span>
<span data-ttu-id="69a8f-259">API доступен через службы ботов.</span><span class="sxs-lookup"><span data-stu-id="69a8f-259">The API is available through Bot Services.</span></span>

#### <a name="prerequisite"></a><span data-ttu-id="69a8f-260">Обязательное условие</span><span class="sxs-lookup"><span data-stu-id="69a8f-260">Prerequisite</span></span>

<span data-ttu-id="69a8f-261">Чтобы использовать API сведений о собраниях, необходимо получить разрешения RSC.</span><span class="sxs-lookup"><span data-stu-id="69a8f-261">To use the Meeting Details API, you must obtain RSC permissions.</span></span> <span data-ttu-id="69a8f-262">Чтобы настроить свойство манифеста приложения, используйте следующий `webApplicationInfo` пример:</span><span class="sxs-lookup"><span data-stu-id="69a8f-262">Use the following example to configure your app manifest's `webApplicationInfo` property:</span></span>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```
 
#### <a name="query-parameter"></a><span data-ttu-id="69a8f-263">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="69a8f-263">Query parameter</span></span>

<span data-ttu-id="69a8f-264">API сведений о собраниях включает в себя следующий параметр запроса:</span><span class="sxs-lookup"><span data-stu-id="69a8f-264">The Meeting Details API includes the following query parameter:</span></span>

|<span data-ttu-id="69a8f-265">Значение</span><span class="sxs-lookup"><span data-stu-id="69a8f-265">Value</span></span>|<span data-ttu-id="69a8f-266">Тип</span><span class="sxs-lookup"><span data-stu-id="69a8f-266">Type</span></span>|<span data-ttu-id="69a8f-267">Обязательный</span><span class="sxs-lookup"><span data-stu-id="69a8f-267">Required</span></span>|<span data-ttu-id="69a8f-268">Описание</span><span class="sxs-lookup"><span data-stu-id="69a8f-268">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="69a8f-269">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="69a8f-269">**meetingId**</span></span>| <span data-ttu-id="69a8f-270">String</span><span class="sxs-lookup"><span data-stu-id="69a8f-270">String</span></span> | <span data-ttu-id="69a8f-271">Да</span><span class="sxs-lookup"><span data-stu-id="69a8f-271">Yes</span></span> | <span data-ttu-id="69a8f-272">Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK.</span><span class="sxs-lookup"><span data-stu-id="69a8f-272">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span> |

#### <a name="example"></a><span data-ttu-id="69a8f-273">Пример</span><span class="sxs-lookup"><span data-stu-id="69a8f-273">Example</span></span>

<span data-ttu-id="69a8f-274">API сведений о собраниях содержит следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="69a8f-274">The Meeting Details API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="69a8f-275">C#</span><span class="sxs-lookup"><span data-stu-id="69a8f-275">C#</span></span>](#tab/dotnet)

```csharp
var connectorClient = parameters.TurnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage(HttpMethod.Get, new Uri(new Uri(connectorClient.BaseUri.OriginalString), $"v1/meetings/{meetingId}"));
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, CancellationToken.None).ConfigureAwait(false);
string content;
if (response.Content != null)
{
    content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
}
```

# <a name="javascript"></a>[<span data-ttu-id="69a8f-276">JavaScript</span><span class="sxs-lookup"><span data-stu-id="69a8f-276">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="69a8f-277">Недоступно</span><span class="sxs-lookup"><span data-stu-id="69a8f-277">Not available</span></span>

# <a name="json"></a>[<span data-ttu-id="69a8f-278">JSON</span><span class="sxs-lookup"><span data-stu-id="69a8f-278">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

---

<span data-ttu-id="69a8f-279">The JSON response body for Meeting Details API is as follows:</span><span class="sxs-lookup"><span data-stu-id="69a8f-279">The JSON response body for Meeting Details API is as follows:</span></span>

```json
{ 
   "details": { 
        "id": "meeting ID", 
        "msGraphResourceId": "", 
        "scheduledStartTime": "2020-08-21T02:30:00+00:00", 
        "scheduledEndTime": "2020-08-21T03:00:00+00:00", 
        "joinUrl": "https://teams.microsoft.com/l/xx", 
        "title": "All Hands", 
        "type": "Scheduled" 
    }, 
    "conversation": { 
            "isGroup": true, 
            “conversationType”: “groupchat”, 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="real-time-teams-meeting-events"></a><span data-ttu-id="69a8f-280">События Teams в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="69a8f-280">Real-time Teams meeting events</span></span>

> [!NOTE]
> <span data-ttu-id="69a8f-281">В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../resources/dev-preview/developer-preview-intro.md) разработчиков.</span><span class="sxs-lookup"><span data-stu-id="69a8f-281">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="69a8f-282">Пользователь может получать события собраний в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="69a8f-282">The user can receive real-time meeting events.</span></span> <span data-ttu-id="69a8f-283">Как только любое приложение связано с собранием, фактическое время начала и окончания собрания передается боту.</span><span class="sxs-lookup"><span data-stu-id="69a8f-283">As soon as any app is associated with a meeting, the actual meeting start and meeting end time are shared with the bot.</span></span>

<span data-ttu-id="69a8f-284">Фактическое время начала и окончания собрания отличается от запланированного времени начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="69a8f-284">Actual start and end time of a meeting are different from the scheduled start and end time.</span></span> <span data-ttu-id="69a8f-285">API сведений о собрании предоставляет запланированное время начала и окончания, а событие предоставляет фактическое время начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="69a8f-285">The meeting details API provides the scheduled start and end time while the event provides the actual start and end time.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="69a8f-286">Обязательное условие</span><span class="sxs-lookup"><span data-stu-id="69a8f-286">Prerequisite</span></span>

<span data-ttu-id="69a8f-287">Манифест приложения должен иметь свойство для получения событий `webApplicationInfo` начала и окончания собрания.</span><span class="sxs-lookup"><span data-stu-id="69a8f-287">Your app manifest must have the `webApplicationInfo` property to receive the meeting start and end events.</span></span> <span data-ttu-id="69a8f-288">Чтобы настроить манифест, используйте следующий пример:</span><span class="sxs-lookup"><span data-stu-id="69a8f-288">Use the following example to configure your manifest:</span></span>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

### <a name="example-of-meeting-start-event-payload"></a><span data-ttu-id="69a8f-289">Пример полезной нагрузки на начало собрания</span><span class="sxs-lookup"><span data-stu-id="69a8f-289">Example of meeting start event payload</span></span>

<span data-ttu-id="69a8f-290">В следующем коде приводится пример полезной нагрузки на событие начала собрания:</span><span class="sxs-lookup"><span data-stu-id="69a8f-290">The following code provides an example of meeting start event payload:</span></span>

```json
{ 
    "name": "application/vnd.microsoft.meetingStart", 
    "type": "event", 
    "timestamp": "2021-04-29T16:10:41.1252256Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "userID", 
        "aadObjectId": "aadOnjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user Id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event", 
        "Id":"meeting id", 
        "JoinUrl": "url" 
        "StartTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-meeting-end-event-payload"></a><span data-ttu-id="69a8f-291">Пример полезной нагрузки конечного события собрания</span><span class="sxs-lookup"><span data-stu-id="69a8f-291">Example of meeting end event payload</span></span>

<span data-ttu-id="69a8f-292">В следующем коде приводится пример полезной нагрузки на конечные события собрания:</span><span class="sxs-lookup"><span data-stu-id="69a8f-292">The following code provides an example of meeting end event payload:</span></span>

```json
{ 
    "name": "application/vnd.microsoft.meetingEnd", 
    "type": "event", 
    "timestamp": "2021-04-29T16:17:17.4388966Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "user id", 
        "aadObjectId": "aadObjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting Id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event in Canary", 
        "Id": "19:meeting_NTM3ZDJjOTUtZGRhOS00MzYxLTk5NDAtMzY4M2IzZWFjZGE1@thread.v2", 
        "JoinUrl": "url", 
        "EndTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-getting-metadata-of-a-meeting"></a><span data-ttu-id="69a8f-293">Пример получения метаданных собрания</span><span class="sxs-lookup"><span data-stu-id="69a8f-293">Example of getting metadata of a meeting</span></span>

<span data-ttu-id="69a8f-294">Ваш бот получает событие через `OnEventActivityAsync` обработник.</span><span class="sxs-lookup"><span data-stu-id="69a8f-294">Your bot receives the event through the `OnEventActivityAsync` handler.</span></span>

<span data-ttu-id="69a8f-295">Для десерализации полезной нагрузки json для получения метаданных собрания вводится объект модели.</span><span class="sxs-lookup"><span data-stu-id="69a8f-295">To deserialize the json payload, a model object is introduced to get the metadata of a meeting.</span></span> <span data-ttu-id="69a8f-296">Метаданные собрания находятся в свойстве `value` в полезной нагрузке события.</span><span class="sxs-lookup"><span data-stu-id="69a8f-296">The metadata of a meeting resides in the `value` property in the event payload.</span></span> <span data-ttu-id="69a8f-297">Создается объект модели, переменные члена которого соответствуют клавишам, которые находятся под свойством `MeetingStartEndEventvalue` `value` в полезной нагрузке события.</span><span class="sxs-lookup"><span data-stu-id="69a8f-297">The `MeetingStartEndEventvalue` model object is created, whose member variables correspond to the keys under the `value` property in the event payload.</span></span>

<span data-ttu-id="69a8f-298">В следующем коде показано, как захватить метаданные собрания , , , и от `MeetingType` начала и окончания собрания `Title` `Id` `JoinUrl` `StartTime` `EndTime` события:</span><span class="sxs-lookup"><span data-stu-id="69a8f-298">The following code shows how to capture the metadata of a meeting that is `MeetingType`, `Title`, `Id`, `JoinUrl`, `StartTime`, and `EndTime` from a meeting start and end event:</span></span>

```csharp
protected override async Task OnEventActivityAsync(
ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    // Event Name is either 'application/vnd.microsoft.meetingStart' or 'application/vnd.microsoft.meetingEnd'
    var meetingEventName = turnContext.Activity.Name;
    // Value contains meeting information (ex: meeting type, start time, etc).
    var meetingEventInfo = turnContext.Activity.Value as JObject; 
    var meetingEventInfoObject =
meetingEventInfo.ToObject<MeetingStartEndEventValue>();
    // Create a very simple adaptive card with meeting information
var attachmentCard = createMeetingStartOrEndEventAttachment(meetingEventName,
meetingEventInfoObject);
    await turnContext.SendActivityAsync(MessageFactory.Attachment(attachmentCard));
}
```

<span data-ttu-id="69a8f-299">MeetingStartEndEventvalue.cs содержит следующий код:</span><span class="sxs-lookup"><span data-stu-id="69a8f-299">The MeetingStartEndEventvalue.cs includes the following code:</span></span>

```csharp
public class MeetingStartEndEventValue
{
    public string Id { get; set; }
    public string Title { get; set; }
    public string MeetingType { get; set; }
    public string JoinUrl { get; set; }
    public string StartTime { get; set; }
    public string EndTime { get; set; }
}
```

## <a name="code-sample"></a><span data-ttu-id="69a8f-300">Пример кода</span><span class="sxs-lookup"><span data-stu-id="69a8f-300">Code sample</span></span>

|<span data-ttu-id="69a8f-301">Пример имени</span><span class="sxs-lookup"><span data-stu-id="69a8f-301">Sample name</span></span> | <span data-ttu-id="69a8f-302">Описание</span><span class="sxs-lookup"><span data-stu-id="69a8f-302">Description</span></span> | <span data-ttu-id="69a8f-303">.NET</span><span class="sxs-lookup"><span data-stu-id="69a8f-303">.NET</span></span> | <span data-ttu-id="69a8f-304">Node.js</span><span class="sxs-lookup"><span data-stu-id="69a8f-304">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="69a8f-305">Разнонасть собраний</span><span class="sxs-lookup"><span data-stu-id="69a8f-305">Meetings extensibility</span></span> | <span data-ttu-id="69a8f-306">Microsoft Teams для прохождения маркеров.</span><span class="sxs-lookup"><span data-stu-id="69a8f-306">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="69a8f-307">View</span><span class="sxs-lookup"><span data-stu-id="69a8f-307">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="69a8f-308">View</span><span class="sxs-lookup"><span data-stu-id="69a8f-308">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="69a8f-309">Бот-бот для пузырьков контента для собраний</span><span class="sxs-lookup"><span data-stu-id="69a8f-309">Meeting content bubble bot</span></span> | <span data-ttu-id="69a8f-310">Microsoft Teams для взаимодействия с ботом пузырьков контента на собрании.</span><span class="sxs-lookup"><span data-stu-id="69a8f-310">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="69a8f-311">View</span><span class="sxs-lookup"><span data-stu-id="69a8f-311">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="69a8f-312">View</span><span class="sxs-lookup"><span data-stu-id="69a8f-312">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="69a8f-313">Собрание MeetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="69a8f-313">Meeting meetingSidePanel</span></span> | <span data-ttu-id="69a8f-314">Microsoft Teams для взаимодействия с боковой панелью на собрании.</span><span class="sxs-lookup"><span data-stu-id="69a8f-314">Microsoft Teams meeting extensibility sample for interacting with the side panel in-meeting.</span></span> | [<span data-ttu-id="69a8f-315">View</span><span class="sxs-lookup"><span data-stu-id="69a8f-315">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [<span data-ttu-id="69a8f-316">View</span><span class="sxs-lookup"><span data-stu-id="69a8f-316">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| <span data-ttu-id="69a8f-317">Вкладка "Сведения в собрании"</span><span class="sxs-lookup"><span data-stu-id="69a8f-317">Details Tab in Meeting</span></span> | <span data-ttu-id="69a8f-318">Microsoft Teams для итерактинга с помощью вкладки Подробные сведения на собрании.</span><span class="sxs-lookup"><span data-stu-id="69a8f-318">Microsoft Teams meeting extensibility sample for iteracting with Details Tab in-meeting.</span></span> | [<span data-ttu-id="69a8f-319">View</span><span class="sxs-lookup"><span data-stu-id="69a8f-319">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [<span data-ttu-id="69a8f-320">View</span><span class="sxs-lookup"><span data-stu-id="69a8f-320">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|

## <a name="see-also"></a><span data-ttu-id="69a8f-321">См. также</span><span class="sxs-lookup"><span data-stu-id="69a8f-321">See also</span></span>

* [<span data-ttu-id="69a8f-322">Рекомендации по проектированию диалогов на собрании</span><span class="sxs-lookup"><span data-stu-id="69a8f-322">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="69a8f-323">Teams потока проверки подлинности для вкладок</span><span class="sxs-lookup"><span data-stu-id="69a8f-323">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
* [<span data-ttu-id="69a8f-324">Приложения для Teams собраний</span><span class="sxs-lookup"><span data-stu-id="69a8f-324">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="69a8f-325">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="69a8f-325">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="69a8f-326">Включить и настроить приложения для Teams собраний</span><span class="sxs-lookup"><span data-stu-id="69a8f-326">Enable and configure your apps for Teams meetings</span></span>](enable-and-configure-your-app-for-teams-meetings.md)
