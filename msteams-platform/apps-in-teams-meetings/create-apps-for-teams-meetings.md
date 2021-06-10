---
title: Необходимые условия и ссылки на API для приложений в собраниях Teams
author: laujan
description: Работа с приложениями для Teams собраний
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams apps meetings user participant role api
ms.openlocfilehash: f42e827801e21bbd039f52dbb685d4559ae5cf81
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853510"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a><span data-ttu-id="d3b96-104">Необходимые условия и ссылки на API для приложений в собраниях Teams</span><span class="sxs-lookup"><span data-stu-id="d3b96-104">Prerequisites and API references for apps in Teams meetings</span></span>

<span data-ttu-id="d3b96-105">Чтобы расширить возможности ваших приложений на протяжении жизненного цикла собраний, Teams позволяет работать с приложениями для Teams собраний.</span><span class="sxs-lookup"><span data-stu-id="d3b96-105">To expand the capabilities of your apps across the meeting lifecycle, Teams enables you to work with apps for Teams meetings.</span></span> <span data-ttu-id="d3b96-106">Необходимо пройти необходимые условия и использовать ссылки API приложений для собраний для улучшения работы с собраниями.</span><span class="sxs-lookup"><span data-stu-id="d3b96-106">You must  go through the prerequisites and you can use the meeting apps API references to enhance the meeting experience.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3b96-107">Предварительные условия</span><span class="sxs-lookup"><span data-stu-id="d3b96-107">Prerequisites</span></span>

<span data-ttu-id="d3b96-108">Прежде чем работать с приложениями для Teams собраний, необходимо иметь представление о следующем:</span><span class="sxs-lookup"><span data-stu-id="d3b96-108">Before you work with apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="d3b96-109">Вы должны иметь знания о разработке Teams приложений.</span><span class="sxs-lookup"><span data-stu-id="d3b96-109">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="d3b96-110">Дополнительные сведения см. [в Teams разработки приложения.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="d3b96-110">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="d3b96-111">Необходимо обновить манифест Teams, чтобы указать, что приложение доступно для собраний.</span><span class="sxs-lookup"><span data-stu-id="d3b96-111">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="d3b96-112">Дополнительные сведения см. в [манифесте приложения.](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="d3b96-112">For more information, see [app manifest](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span></span>

* <span data-ttu-id="d3b96-113">Ваше приложение должно поддерживать настраиваемые вкладки в области группового чата, чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки. Дополнительные сведения см. в [поле groupchat и](../resources/schema/manifest-schema.md#configurabletabs) [создайте вкладку группы.](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="d3b96-113">Your app must support configurable tabs in the groupchat scope, for your app to function in the meeting lifecycle as a tab. For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="d3b96-114">Необходимо придерживаться общих Teams правил разработки вкладок для сценариев до и после собрания.</span><span class="sxs-lookup"><span data-stu-id="d3b96-114">You must adhere to general Teams tab design guidelines for pre and post-meeting scenarios.</span></span> <span data-ttu-id="d3b96-115">Для работы во время собраний обратитесь к вкладке на собрании и рекомендациям по проектированию диалогов на собрании.</span><span class="sxs-lookup"><span data-stu-id="d3b96-115">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="d3b96-116">Дополнительные сведения см. [Teams](../tabs/design/tabs.md)руководства по разработке вкладок, [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)рекомендации по проектированию вкладок на собрании и рекомендации по проектированию диалогов на [собрании.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="d3b96-116">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab), and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="d3b96-117">Необходимо поддерживать область, чтобы включить приложение в чаты перед собранием и `groupchat` после собрания.</span><span class="sxs-lookup"><span data-stu-id="d3b96-117">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="d3b96-118">С помощью предварительного собрания приложения можно найти и добавить приложения для собраний и выполнить задачи перед собранием.</span><span class="sxs-lookup"><span data-stu-id="d3b96-118">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="d3b96-119">С помощью приложения после собрания можно просмотреть результаты собрания, такие как результаты опроса или отзывы.</span><span class="sxs-lookup"><span data-stu-id="d3b96-119">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="d3b96-120">Параметры URL-адресов API должны иметь `meetingId` и `userId` `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="d3b96-120">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="d3b96-121">Они доступны в рамках Teams клиентской SDK и бот-активности.</span><span class="sxs-lookup"><span data-stu-id="d3b96-121">These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="d3b96-122">Кроме того, вы можете получить достоверную информацию для идентификации пользователя и идентификации клиента с помощью вкладки [SSO authentication.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="d3b96-122">In addition, you can retrieve reliable information for user ID and tenant ID using [tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="d3b96-123">API `GetParticipant` должен иметь регистрацию бота и ID для создания маркеров auth.</span><span class="sxs-lookup"><span data-stu-id="d3b96-123">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="d3b96-124">Дополнительные сведения см. в [сведениях о регистрации ботов и ID.](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="d3b96-124">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="d3b96-125">Чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть обновлено в зависимости от событий на собрании.</span><span class="sxs-lookup"><span data-stu-id="d3b96-125">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="d3b96-126">Эти события могут быть в диалоговом окне собрания и на других этапах жизненного цикла собрания.</span><span class="sxs-lookup"><span data-stu-id="d3b96-126">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="d3b96-127">Параметр завершения в диалоговом окне на собрании `bot Id` см. в `NotificationSignal` API.</span><span class="sxs-lookup"><span data-stu-id="d3b96-127">For the in-meeting dialog box, see completion `bot Id` parameter in `NotificationSignal` API.</span></span>

<span data-ttu-id="d3b96-128">После того как вы прошли все необходимые условия, вы можете использовать ссылки API приложений собраний, которые позволяют получать доступ к информации с помощью атрибутов и отображать `GetUserContext` `GetParticipant` `NotificationSignal` соответствующий контент.</span><span class="sxs-lookup"><span data-stu-id="d3b96-128">After you have gone through the prerequisites, you can use the meeting apps API references `GetUserContext`, `GetParticipant`, and `NotificationSignal` that enable you to access information using attributes and display relevant content.</span></span>

## <a name="meeting-apps-api-references"></a><span data-ttu-id="d3b96-129">Ссылки на API приложений для собраний</span><span class="sxs-lookup"><span data-stu-id="d3b96-129">Meeting apps API references</span></span>

<span data-ttu-id="d3b96-130">Новые функции собраний предоставляют API, которые преобразовывают возможности собраний.</span><span class="sxs-lookup"><span data-stu-id="d3b96-130">The new meeting extensibilities provide you with APIs that transform the meeting experience.</span></span> <span data-ttu-id="d3b96-131">С помощью этой новой возможности можно создавать приложения или интегрировать существующие приложения в жизненный цикл собрания.</span><span class="sxs-lookup"><span data-stu-id="d3b96-131">With this new capability, you can build apps or integrate existing apps within the meeting lifecycle.</span></span> <span data-ttu-id="d3b96-132">Вы можете использовать API для того, чтобы ваше приложение знало о собрании.</span><span class="sxs-lookup"><span data-stu-id="d3b96-132">You can use the APIs to make your app aware of the meeting.</span></span> <span data-ttu-id="d3b96-133">Вы можете выбрать API, которые необходимо использовать для повышения качества работы собраний.</span><span class="sxs-lookup"><span data-stu-id="d3b96-133">You can choose which APIs you want to use to enhance the meeting experience.</span></span>

<span data-ttu-id="d3b96-134">В следующей таблице приводится список этих API:</span><span class="sxs-lookup"><span data-stu-id="d3b96-134">The following table provides a list of these APIs:</span></span>

|<span data-ttu-id="d3b96-135">API</span><span class="sxs-lookup"><span data-stu-id="d3b96-135">API</span></span>|<span data-ttu-id="d3b96-136">Описание</span><span class="sxs-lookup"><span data-stu-id="d3b96-136">Description</span></span>|<span data-ttu-id="d3b96-137">Запрос</span><span class="sxs-lookup"><span data-stu-id="d3b96-137">Request</span></span>|<span data-ttu-id="d3b96-138">Источник</span><span class="sxs-lookup"><span data-stu-id="d3b96-138">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="d3b96-139">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="d3b96-139">**GetUserContext**</span></span>| <span data-ttu-id="d3b96-140">Этот API позволяет получать контекстную информацию для отображения соответствующего контента на вкладке Teams.</span><span class="sxs-lookup"><span data-stu-id="d3b96-140">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="d3b96-141">_**microsoftTeams.getContext() => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="d3b96-141">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="d3b96-142">Microsoft Teams Клиентская SDK</span><span class="sxs-lookup"><span data-stu-id="d3b96-142">Microsoft Teams Client SDK</span></span>|
|<span data-ttu-id="d3b96-143">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="d3b96-143">**GetParticipant**</span></span>| <span data-ttu-id="d3b96-144">Этот API позволяет боту получать сведения о участниках, встречая ID и ID участника.</span><span class="sxs-lookup"><span data-stu-id="d3b96-144">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="d3b96-145">**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="d3b96-145">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="d3b96-146">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="d3b96-146">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="d3b96-147">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="d3b96-147">**NotificationSignal**</span></span> | <span data-ttu-id="d3b96-148">Этот API позволяет предоставлять сигналы собрания, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота.</span><span class="sxs-lookup"><span data-stu-id="d3b96-148">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="d3b96-149">Он позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно на собрании.</span><span class="sxs-lookup"><span data-stu-id="d3b96-149">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="d3b96-150">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="d3b96-150">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="d3b96-151">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="d3b96-151">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext-api"></a><span data-ttu-id="d3b96-152">GetUserContext API</span><span class="sxs-lookup"><span data-stu-id="d3b96-152">GetUserContext API</span></span>

<span data-ttu-id="d3b96-153">Чтобы определить и получить контекстную информацию для содержимого вкладки, см. в этой Teams [контексте.](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) `meetingId`используется вкладками при работе в контексте собрания и добавляется для полезной нагрузки ответа.</span><span class="sxs-lookup"><span data-stu-id="d3b96-153">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="d3b96-154">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="d3b96-154">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="d3b96-155">Не кэшить роли участников, так как организатор собрания может изменить роли в любое время.</span><span class="sxs-lookup"><span data-stu-id="d3b96-155">Do not cache participant roles since the meeting organizer can change the roles any time.</span></span>
> * <span data-ttu-id="d3b96-156">Teams в настоящее время не поддерживает большие списки рассылки или размеры реестра более 350 участников `GetParticipant` для API.</span><span class="sxs-lookup"><span data-stu-id="d3b96-156">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

<span data-ttu-id="d3b96-157">API позволяет боту получать сведения о `GetParticipant` участниках, встречая ID и ID участника.</span><span class="sxs-lookup"><span data-stu-id="d3b96-157">The `GetParticipant` API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> <span data-ttu-id="d3b96-158">API включает параметры запросов, примеры и коды ответа.</span><span class="sxs-lookup"><span data-stu-id="d3b96-158">The API includes query parameters, examples, and response codes.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="d3b96-159">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d3b96-159">Query parameters</span></span>

<span data-ttu-id="d3b96-160">API `GetParticipant` включает следующие параметры запроса:</span><span class="sxs-lookup"><span data-stu-id="d3b96-160">The `GetParticipant` API includes the following query parameters:</span></span>

|<span data-ttu-id="d3b96-161">Значение</span><span class="sxs-lookup"><span data-stu-id="d3b96-161">Value</span></span>|<span data-ttu-id="d3b96-162">Тип</span><span class="sxs-lookup"><span data-stu-id="d3b96-162">Type</span></span>|<span data-ttu-id="d3b96-163">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3b96-163">Required</span></span>|<span data-ttu-id="d3b96-164">Описание</span><span class="sxs-lookup"><span data-stu-id="d3b96-164">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="d3b96-165">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="d3b96-165">**meetingId**</span></span>| <span data-ttu-id="d3b96-166">String</span><span class="sxs-lookup"><span data-stu-id="d3b96-166">String</span></span> | <span data-ttu-id="d3b96-167">Да</span><span class="sxs-lookup"><span data-stu-id="d3b96-167">Yes</span></span> | <span data-ttu-id="d3b96-168">Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK.</span><span class="sxs-lookup"><span data-stu-id="d3b96-168">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="d3b96-169">**participantId**</span><span class="sxs-lookup"><span data-stu-id="d3b96-169">**participantId**</span></span>| <span data-ttu-id="d3b96-170">String</span><span class="sxs-lookup"><span data-stu-id="d3b96-170">String</span></span> | <span data-ttu-id="d3b96-171">Да</span><span class="sxs-lookup"><span data-stu-id="d3b96-171">Yes</span></span> | <span data-ttu-id="d3b96-172">ID участника — это пользовательский ИД.</span><span class="sxs-lookup"><span data-stu-id="d3b96-172">The participant ID is the user ID.</span></span> <span data-ttu-id="d3b96-173">Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK.</span><span class="sxs-lookup"><span data-stu-id="d3b96-173">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="d3b96-174">Рекомендуется получить ID участника из SSO Tab.</span><span class="sxs-lookup"><span data-stu-id="d3b96-174">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="d3b96-175">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="d3b96-175">**tenantId**</span></span>| <span data-ttu-id="d3b96-176">Строка</span><span class="sxs-lookup"><span data-stu-id="d3b96-176">String</span></span> | <span data-ttu-id="d3b96-177">Да</span><span class="sxs-lookup"><span data-stu-id="d3b96-177">Yes</span></span> | <span data-ttu-id="d3b96-178">Для пользователей-клиентов требуется ID клиента.</span><span class="sxs-lookup"><span data-stu-id="d3b96-178">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="d3b96-179">Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK.</span><span class="sxs-lookup"><span data-stu-id="d3b96-179">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="d3b96-180">Рекомендуется получить ID клиента из SSO tab.</span><span class="sxs-lookup"><span data-stu-id="d3b96-180">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="d3b96-181">Пример</span><span class="sxs-lookup"><span data-stu-id="d3b96-181">Example</span></span>

<span data-ttu-id="d3b96-182">API `GetParticipant` содержит следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="d3b96-182">The `GetParticipant` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="d3b96-183">C#</span><span class="sxs-lookup"><span data-stu-id="d3b96-183">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="d3b96-184">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d3b96-184">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="d3b96-185">JSON</span><span class="sxs-lookup"><span data-stu-id="d3b96-185">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="d3b96-186">Тело ответа JSON для `GetParticipant` API:</span><span class="sxs-lookup"><span data-stu-id="d3b96-186">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="d3b96-187">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="d3b96-187">Response codes</span></span>

<span data-ttu-id="d3b96-188">API `GetParticipant` включает в себя следующие коды ответа:</span><span class="sxs-lookup"><span data-stu-id="d3b96-188">The `GetParticipant` API includes the following response codes:</span></span>

|<span data-ttu-id="d3b96-189">Код ответа</span><span class="sxs-lookup"><span data-stu-id="d3b96-189">Response code</span></span>|<span data-ttu-id="d3b96-190">Описание</span><span class="sxs-lookup"><span data-stu-id="d3b96-190">Description</span></span>|
|---|---|
| <span data-ttu-id="d3b96-191">**403**</span><span class="sxs-lookup"><span data-stu-id="d3b96-191">**403**</span></span> | <span data-ttu-id="d3b96-192">Приложение не может получать сведения о участниках.</span><span class="sxs-lookup"><span data-stu-id="d3b96-192">The app is not allowed to get participant information.</span></span> <span data-ttu-id="d3b96-193">Это наиболее распространенный ответ на ошибки, который запускается, если приложение не установлено на собрании.</span><span class="sxs-lookup"><span data-stu-id="d3b96-193">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="d3b96-194">Например, если приложение отключено администратором клиента или заблокировано во время переноса веб-сайтов в прямом эфире.</span><span class="sxs-lookup"><span data-stu-id="d3b96-194">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="d3b96-195">**200**</span><span class="sxs-lookup"><span data-stu-id="d3b96-195">**200**</span></span> | <span data-ttu-id="d3b96-196">Данные участника успешно извлекаются.</span><span class="sxs-lookup"><span data-stu-id="d3b96-196">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="d3b96-197">**401**</span><span class="sxs-lookup"><span data-stu-id="d3b96-197">**401**</span></span> | <span data-ttu-id="d3b96-198">Приложение отвечает недействительным маркером.</span><span class="sxs-lookup"><span data-stu-id="d3b96-198">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="d3b96-199">**404**</span><span class="sxs-lookup"><span data-stu-id="d3b96-199">**404**</span></span> | <span data-ttu-id="d3b96-200">Собрание истеко или участник не может быть найден.</span><span class="sxs-lookup"><span data-stu-id="d3b96-200">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="d3b96-201">**500**</span><span class="sxs-lookup"><span data-stu-id="d3b96-201">**500**</span></span> | <span data-ttu-id="d3b96-202">Срок действия собрания истек (более 60 дней) с момента окончания собрания, или у участников нет разрешений, основанных на их роли.</span><span class="sxs-lookup"><span data-stu-id="d3b96-202">The meeting has either expired (more than 60 days) since the meeting ended or the participants do not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="d3b96-203">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="d3b96-203">NotificationSignal API</span></span>

<span data-ttu-id="d3b96-204">Все пользователи на собрании получают уведомления, отправленные через `NotificationSignal` API.</span><span class="sxs-lookup"><span data-stu-id="d3b96-204">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="d3b96-205">При вызове диалогового окна на собрании содержимое представляется в качестве сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="d3b96-205">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="d3b96-206">В настоящее время отправка целевых уведомлений не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d3b96-206">Currently, sending targeted notifications is not supported.</span></span>

<span data-ttu-id="d3b96-207">`NotificationSignal` API позволяет предоставлять сигналы собраний, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота.</span><span class="sxs-lookup"><span data-stu-id="d3b96-207">`NotificationSignal` API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="d3b96-208">Этот API позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно в собрании.</span><span class="sxs-lookup"><span data-stu-id="d3b96-208">This API allows you to signal based on user action that shows an in-meeting dialog box.</span></span> <span data-ttu-id="d3b96-209">API включает параметр запроса, примеры и коды ответа.</span><span class="sxs-lookup"><span data-stu-id="d3b96-209">The API includes query parameter, examples, and response codes.</span></span>

#### <a name="query-parameter"></a><span data-ttu-id="d3b96-210">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="d3b96-210">Query parameter</span></span>

<span data-ttu-id="d3b96-211">API `NotificationSignal` включает в себя следующий параметр запроса:</span><span class="sxs-lookup"><span data-stu-id="d3b96-211">The `NotificationSignal` API includes the following query parameter:</span></span>

|<span data-ttu-id="d3b96-212">Значение</span><span class="sxs-lookup"><span data-stu-id="d3b96-212">Value</span></span>|<span data-ttu-id="d3b96-213">Тип</span><span class="sxs-lookup"><span data-stu-id="d3b96-213">Type</span></span>|<span data-ttu-id="d3b96-214">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3b96-214">Required</span></span>|<span data-ttu-id="d3b96-215">Описание</span><span class="sxs-lookup"><span data-stu-id="d3b96-215">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="d3b96-216">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="d3b96-216">**conversationId**</span></span>| <span data-ttu-id="d3b96-217">Строка</span><span class="sxs-lookup"><span data-stu-id="d3b96-217">String</span></span> | <span data-ttu-id="d3b96-218">Да</span><span class="sxs-lookup"><span data-stu-id="d3b96-218">Yes</span></span> | <span data-ttu-id="d3b96-219">Идентификатор беседы доступен в рамках Bot Invoke.</span><span class="sxs-lookup"><span data-stu-id="d3b96-219">The conversation identifier is available as part of Bot Invoke.</span></span> |

#### <a name="examples"></a><span data-ttu-id="d3b96-220">Примеры</span><span class="sxs-lookup"><span data-stu-id="d3b96-220">Examples</span></span>

<span data-ttu-id="d3b96-221">Объявляется `Bot ID` в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="d3b96-221">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="d3b96-222">Параметр `completionBotId` необязательный `externalResourceUrl` в примере запрашиваемой полезной нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d3b96-222">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="d3b96-223">`Bot ID` объявляется в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="d3b96-223">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="d3b96-224">Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях.</span><span class="sxs-lookup"><span data-stu-id="d3b96-224">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="d3b96-225">Чтобы размеры были в пределах допустимого, см. в [рекомендациях по проектированию.](design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="d3b96-225">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="d3b96-226">URL-адрес — это страница, загруженная в диалоговом окне на `<iframe>` собрании.</span><span class="sxs-lookup"><span data-stu-id="d3b96-226">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="d3b96-227">Домен должен быть в массиве приложения в `validDomains` манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="d3b96-227">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

<span data-ttu-id="d3b96-228">API `NotificationSignal` содержит следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="d3b96-228">The `NotificationSignal` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="d3b96-229">C#</span><span class="sxs-lookup"><span data-stu-id="d3b96-229">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="d3b96-230">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d3b96-230">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="d3b96-231">JSON</span><span class="sxs-lookup"><span data-stu-id="d3b96-231">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="d3b96-232">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="d3b96-232">Response codes</span></span>

<span data-ttu-id="d3b96-233">API `NotificationSignal` включает в себя следующие коды ответа:</span><span class="sxs-lookup"><span data-stu-id="d3b96-233">The `NotificationSignal` API includes the following response codes:</span></span>

|<span data-ttu-id="d3b96-234">Код ответа</span><span class="sxs-lookup"><span data-stu-id="d3b96-234">Response code</span></span>|<span data-ttu-id="d3b96-235">Описание</span><span class="sxs-lookup"><span data-stu-id="d3b96-235">Description</span></span>|
|---|---|
| <span data-ttu-id="d3b96-236">**201**</span><span class="sxs-lookup"><span data-stu-id="d3b96-236">**201**</span></span> | <span data-ttu-id="d3b96-237">Успешно отправляется действие с сигналом.</span><span class="sxs-lookup"><span data-stu-id="d3b96-237">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="d3b96-238">**401**</span><span class="sxs-lookup"><span data-stu-id="d3b96-238">**401**</span></span> | <span data-ttu-id="d3b96-239">Приложение отвечает недействительным маркером.</span><span class="sxs-lookup"><span data-stu-id="d3b96-239">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="d3b96-240">**403**</span><span class="sxs-lookup"><span data-stu-id="d3b96-240">**403**</span></span> | <span data-ttu-id="d3b96-241">Приложение не может отправить сигнал.</span><span class="sxs-lookup"><span data-stu-id="d3b96-241">The app is unable to send the signal.</span></span> <span data-ttu-id="d3b96-242">Это может произойти из-за различных причин, таких как отключение приложения администратором клиента, блокировка приложения во время переноса веб-сайта в прямом эфире и так далее.</span><span class="sxs-lookup"><span data-stu-id="d3b96-242">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="d3b96-243">В этом случае полезное сообщение содержит подробное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="d3b96-243">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="d3b96-244">**404**</span><span class="sxs-lookup"><span data-stu-id="d3b96-244">**404**</span></span> | <span data-ttu-id="d3b96-245">Чат собрания не существует.</span><span class="sxs-lookup"><span data-stu-id="d3b96-245">The meeting chat does not exist.</span></span> |

## <a name="code-sample"></a><span data-ttu-id="d3b96-246">Пример кода</span><span class="sxs-lookup"><span data-stu-id="d3b96-246">Code sample</span></span>

|<span data-ttu-id="d3b96-247">Пример имени</span><span class="sxs-lookup"><span data-stu-id="d3b96-247">Sample name</span></span> | <span data-ttu-id="d3b96-248">Описание</span><span class="sxs-lookup"><span data-stu-id="d3b96-248">Description</span></span> | <span data-ttu-id="d3b96-249">.NET</span><span class="sxs-lookup"><span data-stu-id="d3b96-249">.NET</span></span> | <span data-ttu-id="d3b96-250">Node.js</span><span class="sxs-lookup"><span data-stu-id="d3b96-250">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="d3b96-251">Разнонасть собраний</span><span class="sxs-lookup"><span data-stu-id="d3b96-251">Meetings extensibility</span></span> | <span data-ttu-id="d3b96-252">Microsoft Teams для прохождения маркеров.</span><span class="sxs-lookup"><span data-stu-id="d3b96-252">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="d3b96-253">View</span><span class="sxs-lookup"><span data-stu-id="d3b96-253">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="d3b96-254">View</span><span class="sxs-lookup"><span data-stu-id="d3b96-254">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="d3b96-255">Бот-бот для пузырьков контента для собраний</span><span class="sxs-lookup"><span data-stu-id="d3b96-255">Meeting content bubble bot</span></span> | <span data-ttu-id="d3b96-256">Microsoft Teams для взаимодействия с ботом пузырьков контента на собрании.</span><span class="sxs-lookup"><span data-stu-id="d3b96-256">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="d3b96-257">View</span><span class="sxs-lookup"><span data-stu-id="d3b96-257">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="d3b96-258">View</span><span class="sxs-lookup"><span data-stu-id="d3b96-258">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="d3b96-259">Собрание MeetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="d3b96-259">Meeting meetingSidePanel</span></span> | <span data-ttu-id="d3b96-260">Microsoft Teams для взаимодействия с боковой панелью на собрании.</span><span class="sxs-lookup"><span data-stu-id="d3b96-260">Microsoft Teams meeting extensibility sample for interacting with the side panel in-meeting.</span></span> | [<span data-ttu-id="d3b96-261">View</span><span class="sxs-lookup"><span data-stu-id="d3b96-261">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [<span data-ttu-id="d3b96-262">View</span><span class="sxs-lookup"><span data-stu-id="d3b96-262">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|

## <a name="see-also"></a><span data-ttu-id="d3b96-263">См. также</span><span class="sxs-lookup"><span data-stu-id="d3b96-263">See also</span></span>

* [<span data-ttu-id="d3b96-264">Рекомендации по проектированию диалогов на собрании</span><span class="sxs-lookup"><span data-stu-id="d3b96-264">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="d3b96-265">Teams потока проверки подлинности для вкладок</span><span class="sxs-lookup"><span data-stu-id="d3b96-265">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
* [<span data-ttu-id="d3b96-266">Приложения для Teams собраний</span><span class="sxs-lookup"><span data-stu-id="d3b96-266">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="d3b96-267">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="d3b96-267">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d3b96-268">Включить и настроить приложения для Teams собраний</span><span class="sxs-lookup"><span data-stu-id="d3b96-268">Enable and configure your apps for Teams meetings</span></span>](enable-and-configure-your-app-for-teams-meetings.md)
