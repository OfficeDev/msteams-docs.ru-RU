---
title: Создание приложений для собраний групп
author: laujan
description: создание приложений для собраний групп
ms.topic: conceptual
ms.author: lajanuar
keywords: teams apps meetings user participant role api
ms.openlocfilehash: ac0d3dee30e82cde51651f7eab3b05e569b820f7
ms.sourcegitcommit: 94b1d3e50563b31c1ff01c52d563c112a2553611
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/30/2021
ms.locfileid: "51435038"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="24c0d-104">Создание приложений для собраний Teams</span><span class="sxs-lookup"><span data-stu-id="24c0d-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="24c0d-105">Предпосылки и соображения</span><span class="sxs-lookup"><span data-stu-id="24c0d-105">Prerequisites and considerations</span></span>

<span data-ttu-id="24c0d-106">Прежде чем создавать приложения для собраний Teams, необходимо иметь представление о следующих ниже.</span><span class="sxs-lookup"><span data-stu-id="24c0d-106">Before you create apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="24c0d-107">Вы должны иметь знания о разработке приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="24c0d-107">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="24c0d-108">Дополнительные сведения см. в [приложении Teams.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="24c0d-108">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="24c0d-109">Необходимо обновить манифест приложения Teams, чтобы указать, что приложение доступно для собраний.</span><span class="sxs-lookup"><span data-stu-id="24c0d-109">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="24c0d-110">Дополнительные сведения см. в [манифесте приложения.](#update-your-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="24c0d-110">For more information, see [app manifest](#update-your-app-manifest).</span></span>

* <span data-ttu-id="24c0d-111">Чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки, оно должно поддерживать настраиваемые вкладки в области groupchat.</span><span class="sxs-lookup"><span data-stu-id="24c0d-111">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the groupchat scope.</span></span> <span data-ttu-id="24c0d-112">Дополнительные сведения см. в [поле groupchat и](../resources/schema/manifest-schema.md#configurabletabs) [создайте вкладку группы.](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="24c0d-112">For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="24c0d-113">Необходимо придерживаться общих правил разработки вкладок Teams для сценариев до и после собрания.</span><span class="sxs-lookup"><span data-stu-id="24c0d-113">You must adhere to general Teams tab design guidelines for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="24c0d-114">Для работы во время собраний обратитесь к вкладке на собрании и рекомендациям по проектированию диалогов на собрании.</span><span class="sxs-lookup"><span data-stu-id="24c0d-114">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="24c0d-115">Дополнительные сведения см. в рекомендациях по разработке вкладок [Teams,](../tabs/design/tabs.md)рекомендациях по разработке вкладок на собрании и рекомендациях по проектированию диалогов на [собрании.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)</span><span class="sxs-lookup"><span data-stu-id="24c0d-115">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="24c0d-116">Необходимо поддерживать область, чтобы включить приложение в чаты перед собранием и `groupchat` после собрания.</span><span class="sxs-lookup"><span data-stu-id="24c0d-116">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="24c0d-117">С помощью предварительного собрания приложения можно найти и добавить приложения для собраний и выполнить задачи перед собранием.</span><span class="sxs-lookup"><span data-stu-id="24c0d-117">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="24c0d-118">С помощью приложения после собрания можно просмотреть результаты собрания, такие как результаты опроса или отзывы.</span><span class="sxs-lookup"><span data-stu-id="24c0d-118">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="24c0d-119">Параметры URL-адресов API должны иметь `meetingId` и `userId` `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="24c0d-119">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="24c0d-120">Они доступны в рамках клиентской SDK и бот-активности Teams.</span><span class="sxs-lookup"><span data-stu-id="24c0d-120">These are available as part of the Teams client SDK and bot activity.</span></span> <span data-ttu-id="24c0d-121">Кроме того, с помощью проверки подлинности [Tab SSO](../tabs/how-to/authentication/auth-aad-sso.md)можно получить достоверную информацию для идентификации пользователя и идентификации клиента.</span><span class="sxs-lookup"><span data-stu-id="24c0d-121">In addition, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="24c0d-122">API `GetParticipant` должен иметь регистрацию бота и ID для создания маркеров auth.</span><span class="sxs-lookup"><span data-stu-id="24c0d-122">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="24c0d-123">Дополнительные сведения см. в [сведениях о регистрации ботов и ID.](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="24c0d-123">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="24c0d-124">Чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть обновлено в зависимости от событий на собрании.</span><span class="sxs-lookup"><span data-stu-id="24c0d-124">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="24c0d-125">Эти события могут быть в диалоговом окне собрания и на других этапах жизненного цикла собрания.</span><span class="sxs-lookup"><span data-stu-id="24c0d-125">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="24c0d-126">Параметр завершения в диалоговом окне на собрании см. `bot Id` в `Notification Signal API` .</span><span class="sxs-lookup"><span data-stu-id="24c0d-126">For the in-meeting dialog box, see completion `bot Id` parameter in `Notification Signal API`.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="24c0d-127">Ссылка на API приложений для собраний</span><span class="sxs-lookup"><span data-stu-id="24c0d-127">Meeting apps API reference</span></span>

|<span data-ttu-id="24c0d-128">API</span><span class="sxs-lookup"><span data-stu-id="24c0d-128">API</span></span>|<span data-ttu-id="24c0d-129">Описание</span><span class="sxs-lookup"><span data-stu-id="24c0d-129">Description</span></span>|<span data-ttu-id="24c0d-130">Запрос</span><span class="sxs-lookup"><span data-stu-id="24c0d-130">Request</span></span>|<span data-ttu-id="24c0d-131">Source</span><span class="sxs-lookup"><span data-stu-id="24c0d-131">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="24c0d-132">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="24c0d-132">**GetUserContext**</span></span>| <span data-ttu-id="24c0d-133">Этот API позволяет получать контекстную информацию для отображения соответствующего контента на вкладке Teams.</span><span class="sxs-lookup"><span data-stu-id="24c0d-133">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="24c0d-134">_**microsoftTeams.getContext() => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="24c0d-134">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="24c0d-135">Клиент Microsoft Teams SDK</span><span class="sxs-lookup"><span data-stu-id="24c0d-135">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="24c0d-136">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="24c0d-136">**GetParticipant**</span></span>| <span data-ttu-id="24c0d-137">Этот API позволяет боту получать сведения о участниках, встречая ID и ID участника.</span><span class="sxs-lookup"><span data-stu-id="24c0d-137">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="24c0d-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="24c0d-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="24c0d-139">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="24c0d-139">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="24c0d-140">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="24c0d-140">**NotificationSignal**</span></span> | <span data-ttu-id="24c0d-141">Этот API позволяет предоставлять сигналы собрания, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота.</span><span class="sxs-lookup"><span data-stu-id="24c0d-141">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="24c0d-142">Он позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно на собрании.</span><span class="sxs-lookup"><span data-stu-id="24c0d-142">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="24c0d-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="24c0d-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="24c0d-144">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="24c0d-144">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="24c0d-145">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="24c0d-145">GetUserContext</span></span>

<span data-ttu-id="24c0d-146">Чтобы определить и получить контекстную информацию для содержимого вкладки, см. в тексте получить контекст [для вкладки Teams.](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) `meetingId` используется вкладками при работе в контексте собрания и добавляется для полезной нагрузки ответа.</span><span class="sxs-lookup"><span data-stu-id="24c0d-146">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="24c0d-147">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="24c0d-147">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="24c0d-148">Не кэшить роли участников, так как организатор собрания может изменить роль в любое время.</span><span class="sxs-lookup"><span data-stu-id="24c0d-148">Do not cache participant roles since the meeting organizer can change a role any time.</span></span>
> * <span data-ttu-id="24c0d-149">В настоящее время teams не поддерживают большие списки рассылки или размер реестра, вметив более 350 `GetParticipant` участников для API.</span><span class="sxs-lookup"><span data-stu-id="24c0d-149">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="24c0d-150">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="24c0d-150">Query parameters</span></span>

|<span data-ttu-id="24c0d-151">Значение</span><span class="sxs-lookup"><span data-stu-id="24c0d-151">Value</span></span>|<span data-ttu-id="24c0d-152">Тип</span><span class="sxs-lookup"><span data-stu-id="24c0d-152">Type</span></span>|<span data-ttu-id="24c0d-153">Обязательный</span><span class="sxs-lookup"><span data-stu-id="24c0d-153">Required</span></span>|<span data-ttu-id="24c0d-154">Описание</span><span class="sxs-lookup"><span data-stu-id="24c0d-154">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="24c0d-155">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="24c0d-155">**meetingId**</span></span>| <span data-ttu-id="24c0d-156">string</span><span class="sxs-lookup"><span data-stu-id="24c0d-156">string</span></span> | <span data-ttu-id="24c0d-157">Да</span><span class="sxs-lookup"><span data-stu-id="24c0d-157">Yes</span></span> | <span data-ttu-id="24c0d-158">Идентификатор собрания доступен через Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="24c0d-158">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="24c0d-159">**participantId**</span><span class="sxs-lookup"><span data-stu-id="24c0d-159">**participantId**</span></span>| <span data-ttu-id="24c0d-160">string</span><span class="sxs-lookup"><span data-stu-id="24c0d-160">string</span></span> | <span data-ttu-id="24c0d-161">Да</span><span class="sxs-lookup"><span data-stu-id="24c0d-161">Yes</span></span> | <span data-ttu-id="24c0d-162">ID участника — это пользовательский ИД.</span><span class="sxs-lookup"><span data-stu-id="24c0d-162">The participant ID is the user ID.</span></span> <span data-ttu-id="24c0d-163">Он доступен в SSO tab, Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="24c0d-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="24c0d-164">Рекомендуется получить ID участника из SSO Tab.</span><span class="sxs-lookup"><span data-stu-id="24c0d-164">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="24c0d-165">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="24c0d-165">**tenantId**</span></span>| <span data-ttu-id="24c0d-166">string</span><span class="sxs-lookup"><span data-stu-id="24c0d-166">string</span></span> | <span data-ttu-id="24c0d-167">Да</span><span class="sxs-lookup"><span data-stu-id="24c0d-167">Yes</span></span> | <span data-ttu-id="24c0d-168">Для пользователей-клиентов требуется ID клиента.</span><span class="sxs-lookup"><span data-stu-id="24c0d-168">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="24c0d-169">Он доступен в SSO tab, Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="24c0d-169">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="24c0d-170">Рекомендуется получить ID клиента из SSO tab.</span><span class="sxs-lookup"><span data-stu-id="24c0d-170">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="24c0d-171">Пример</span><span class="sxs-lookup"><span data-stu-id="24c0d-171">Example</span></span>

# <a name="c"></a>[<span data-ttu-id="24c0d-172">C#</span><span class="sxs-lookup"><span data-stu-id="24c0d-172">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="24c0d-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="24c0d-173">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="24c0d-174">JSON</span><span class="sxs-lookup"><span data-stu-id="24c0d-174">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="24c0d-175">Тело ответа JSON для `GetParticipant` API:</span><span class="sxs-lookup"><span data-stu-id="24c0d-175">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="24c0d-176">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="24c0d-176">Response codes</span></span>

|<span data-ttu-id="24c0d-177">Код ответа</span><span class="sxs-lookup"><span data-stu-id="24c0d-177">Response code</span></span>|<span data-ttu-id="24c0d-178">Описание</span><span class="sxs-lookup"><span data-stu-id="24c0d-178">Description</span></span>|
|---|---|
| <span data-ttu-id="24c0d-179">**403**</span><span class="sxs-lookup"><span data-stu-id="24c0d-179">**403**</span></span> | <span data-ttu-id="24c0d-180">Приложение не может получать сведения о участниках.</span><span class="sxs-lookup"><span data-stu-id="24c0d-180">The app is not allowed to get participant information.</span></span> <span data-ttu-id="24c0d-181">Это наиболее распространенный ответ на ошибки, который запускается, если приложение не установлено на собрании.</span><span class="sxs-lookup"><span data-stu-id="24c0d-181">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="24c0d-182">Например, если приложение отключено администратором клиента или заблокировано во время переноса веб-сайтов в прямом эфире.</span><span class="sxs-lookup"><span data-stu-id="24c0d-182">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="24c0d-183">**200**</span><span class="sxs-lookup"><span data-stu-id="24c0d-183">**200**</span></span> | <span data-ttu-id="24c0d-184">Данные участника успешно извлекаются.</span><span class="sxs-lookup"><span data-stu-id="24c0d-184">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="24c0d-185">**401**</span><span class="sxs-lookup"><span data-stu-id="24c0d-185">**401**</span></span> | <span data-ttu-id="24c0d-186">Приложение отвечает недействительным маркером.</span><span class="sxs-lookup"><span data-stu-id="24c0d-186">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="24c0d-187">**404**</span><span class="sxs-lookup"><span data-stu-id="24c0d-187">**404**</span></span> | <span data-ttu-id="24c0d-188">Собрание истеко или участник не может быть найден.</span><span class="sxs-lookup"><span data-stu-id="24c0d-188">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="24c0d-189">**500**</span><span class="sxs-lookup"><span data-stu-id="24c0d-189">**500**</span></span> | <span data-ttu-id="24c0d-190">Срок действия собрания истек более 60 дней с момента окончания собрания, либо у участника нет разрешений, основанных на их роли.</span><span class="sxs-lookup"><span data-stu-id="24c0d-190">The meeting has either expired more than 60 days since the meeting ended or the participant does not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="24c0d-191">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="24c0d-191">NotificationSignal API</span></span>

<span data-ttu-id="24c0d-192">Все пользователи на собрании получают уведомления, отправленные через `NotificationSignal` API.</span><span class="sxs-lookup"><span data-stu-id="24c0d-192">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="24c0d-193">При вызове диалогового окна на собрании содержимое представляется в качестве сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="24c0d-193">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="24c0d-194">В настоящее время отправка целевых уведомлений не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="24c0d-194">Currently, sending targeted notifications is not supported.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="24c0d-195">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="24c0d-195">Query parameters</span></span>

|<span data-ttu-id="24c0d-196">Значение</span><span class="sxs-lookup"><span data-stu-id="24c0d-196">Value</span></span>|<span data-ttu-id="24c0d-197">Тип</span><span class="sxs-lookup"><span data-stu-id="24c0d-197">Type</span></span>|<span data-ttu-id="24c0d-198">Обязательный</span><span class="sxs-lookup"><span data-stu-id="24c0d-198">Required</span></span>|<span data-ttu-id="24c0d-199">Описание</span><span class="sxs-lookup"><span data-stu-id="24c0d-199">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="24c0d-200">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="24c0d-200">**conversationId**</span></span>| <span data-ttu-id="24c0d-201">string</span><span class="sxs-lookup"><span data-stu-id="24c0d-201">string</span></span> | <span data-ttu-id="24c0d-202">Да</span><span class="sxs-lookup"><span data-stu-id="24c0d-202">Yes</span></span> | <span data-ttu-id="24c0d-203">Идентификатор беседы доступен в рамках вызова бота</span><span class="sxs-lookup"><span data-stu-id="24c0d-203">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="24c0d-204">Пример</span><span class="sxs-lookup"><span data-stu-id="24c0d-204">Example</span></span>

<span data-ttu-id="24c0d-205">Объявляется `Bot ID` в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="24c0d-205">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="24c0d-206">Параметр `completionBotId` необязательный `externalResourceUrl` в примере запрашиваемой полезной нагрузки.</span><span class="sxs-lookup"><span data-stu-id="24c0d-206">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="24c0d-207">`Bot ID` объявляется в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="24c0d-207">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="24c0d-208">Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях.</span><span class="sxs-lookup"><span data-stu-id="24c0d-208">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="24c0d-209">Чтобы размеры были в пределах допустимого, см. в [рекомендациях по проектированию.](design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="24c0d-209">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="24c0d-210">URL-адрес — это страница, загруженная в диалоговом окне на `<iframe>` собрании.</span><span class="sxs-lookup"><span data-stu-id="24c0d-210">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="24c0d-211">Домен должен быть в массиве приложения в `validDomains` манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="24c0d-211">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="c"></a>[<span data-ttu-id="24c0d-212">C#</span><span class="sxs-lookup"><span data-stu-id="24c0d-212">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="24c0d-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="24c0d-213">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="24c0d-214">JSON</span><span class="sxs-lookup"><span data-stu-id="24c0d-214">JSON</span></span>](#tab/json)

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

* * *

#### <a name="response-codes"></a><span data-ttu-id="24c0d-215">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="24c0d-215">Response codes</span></span>

|<span data-ttu-id="24c0d-216">Код ответа</span><span class="sxs-lookup"><span data-stu-id="24c0d-216">Response code</span></span>|<span data-ttu-id="24c0d-217">Описание</span><span class="sxs-lookup"><span data-stu-id="24c0d-217">Description</span></span>|
|---|---|
| <span data-ttu-id="24c0d-218">**201**</span><span class="sxs-lookup"><span data-stu-id="24c0d-218">**201**</span></span> | <span data-ttu-id="24c0d-219">Успешно отправляется действие с сигналом</span><span class="sxs-lookup"><span data-stu-id="24c0d-219">The activity with signal is successfully sent</span></span> |
| <span data-ttu-id="24c0d-220">**401**</span><span class="sxs-lookup"><span data-stu-id="24c0d-220">**401**</span></span> | <span data-ttu-id="24c0d-221">Приложение отвечает недействительным маркером.</span><span class="sxs-lookup"><span data-stu-id="24c0d-221">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="24c0d-222">**403**</span><span class="sxs-lookup"><span data-stu-id="24c0d-222">**403**</span></span> | <span data-ttu-id="24c0d-223">Приложение не может отправить сигнал.</span><span class="sxs-lookup"><span data-stu-id="24c0d-223">The app is unable to send the signal.</span></span> <span data-ttu-id="24c0d-224">Это может произойти из-за различных причин, таких как отключение приложения администратором клиента, блокировка приложения во время переноса веб-сайта в прямом эфире и так далее.</span><span class="sxs-lookup"><span data-stu-id="24c0d-224">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="24c0d-225">В этом случае полезное сообщение содержит подробное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="24c0d-225">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="24c0d-226">**404**</span><span class="sxs-lookup"><span data-stu-id="24c0d-226">**404**</span></span> | <span data-ttu-id="24c0d-227">Чат собрания не существует.</span><span class="sxs-lookup"><span data-stu-id="24c0d-227">The meeting chat does not exist.</span></span> |

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="24c0d-228">Включить приложение для собраний Teams</span><span class="sxs-lookup"><span data-stu-id="24c0d-228">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="24c0d-229">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="24c0d-229">Update your app manifest</span></span>

<span data-ttu-id="24c0d-230">Возможности приложения собраний объявляются в манифесте приложения с помощью `configurableTabs` массивов и `scopes` `context` массивов.</span><span class="sxs-lookup"><span data-stu-id="24c0d-230">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="24c0d-231">Область определяет, кому и в котором контекст определяет, где доступно ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="24c0d-231">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> <span data-ttu-id="24c0d-232">Попробуйте обновить манифест приложения с помощью [схемы манифеста.](../resources/schema/manifest-schema-dev-preview.md)</span><span class="sxs-lookup"><span data-stu-id="24c0d-232">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel"
     ]
    }
  ]
```

### <a name="context-property"></a><span data-ttu-id="24c0d-233">Свойство Context</span><span class="sxs-lookup"><span data-stu-id="24c0d-233">Context property</span></span>

<span data-ttu-id="24c0d-234">Вкладка `context` и свойства позволяют `scopes` определить, где должно отображаться ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="24c0d-234">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="24c0d-235">Вкладки в области или области `team` `groupchat` могут иметь несколько контекстов.</span><span class="sxs-lookup"><span data-stu-id="24c0d-235">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="24c0d-236">Ниже ниже 10 значений для свойства, из которого можно использовать все или некоторые `context` из этих значений:</span><span class="sxs-lookup"><span data-stu-id="24c0d-236">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="24c0d-237">Значение</span><span class="sxs-lookup"><span data-stu-id="24c0d-237">Value</span></span>|<span data-ttu-id="24c0d-238">Описание</span><span class="sxs-lookup"><span data-stu-id="24c0d-238">Description</span></span>|
|---|---|
| <span data-ttu-id="24c0d-239">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="24c0d-239">**channelTab**</span></span> | <span data-ttu-id="24c0d-240">Вкладка в загонах канала команды.</span><span class="sxs-lookup"><span data-stu-id="24c0d-240">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="24c0d-241">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="24c0d-241">**privateChatTab**</span></span> | <span data-ttu-id="24c0d-242">Вкладка в загонах группового чата между набором пользователей, не в контексте группы или собрания.</span><span class="sxs-lookup"><span data-stu-id="24c0d-242">A tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="24c0d-243">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="24c0d-243">**meetingChatTab**</span></span> | <span data-ttu-id="24c0d-244">Вкладка в загонах группового чата между набором пользователей в контексте запланированного собрания.</span><span class="sxs-lookup"><span data-stu-id="24c0d-244">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="24c0d-245">**meetingDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="24c0d-245">**meetingDetailsTab**</span></span> | <span data-ttu-id="24c0d-246">Вкладка в загонах сведений о собрании для просмотра календаря.</span><span class="sxs-lookup"><span data-stu-id="24c0d-246">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="24c0d-247">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="24c0d-247">**meetingSidePanel**</span></span> | <span data-ttu-id="24c0d-248">Панель на собрании, открытая с помощью единой панели (U-bar).</span><span class="sxs-lookup"><span data-stu-id="24c0d-248">An in-meeting panel opened via the unified bar (U-bar).</span></span> |

> [!NOTE]
> <span data-ttu-id="24c0d-249">`Context` свойство в настоящее время не поддерживается для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="24c0d-249">`Context` property is currently not supported on mobile clients.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="24c0d-250">Настройка приложения для сценариев собраний</span><span class="sxs-lookup"><span data-stu-id="24c0d-250">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="24c0d-251">Чтобы приложение было видимым в галерее вкладок, оно должно поддерживать настраиваемые вкладки и область группового чата.</span><span class="sxs-lookup"><span data-stu-id="24c0d-251">For your app to be visible in the tab gallery it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="24c0d-252">Мобильные клиенты поддерживают вкладки только на этапах предварительного и после собраний.</span><span class="sxs-lookup"><span data-stu-id="24c0d-252">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="24c0d-253">В настоящее время в мобильных клиентах не поддерживается диалоговое окно и вкладка на собрании.</span><span class="sxs-lookup"><span data-stu-id="24c0d-253">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="24c0d-254">Дополнительные сведения см. [в руководстве по вкладки на мобильных](../tabs/design/tabs-mobile.md) устройствах при создании вкладок для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="24c0d-254">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="24c0d-255">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="24c0d-255">Before a meeting</span></span>

<span data-ttu-id="24c0d-256">Перед собранием пользователи могут добавлять вкладки, боты и расширения обмена сообщениями на собрание.</span><span class="sxs-lookup"><span data-stu-id="24c0d-256">Before a meeting, users can add tabs, bots and messaging extensions to a meeting.</span></span> <span data-ttu-id="24c0d-257">Пользователи с ролями организатора и презентовщика могут добавлять вкладки в собрание.</span><span class="sxs-lookup"><span data-stu-id="24c0d-257">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="24c0d-258">**Добавление вкладки к собранию**</span><span class="sxs-lookup"><span data-stu-id="24c0d-258">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="24c0d-259">В календаре выберите собрание, на которое нужно добавить вкладку.</span><span class="sxs-lookup"><span data-stu-id="24c0d-259">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="24c0d-260">Выберите **вкладку Details** и выберите плюс</span><span class="sxs-lookup"><span data-stu-id="24c0d-260">Select the **Details** tab and select plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="24c0d-261">.</span><span class="sxs-lookup"><span data-stu-id="24c0d-261">.</span></span> <span data-ttu-id="24c0d-262">Отображается галерея вкладок.</span><span class="sxs-lookup"><span data-stu-id="24c0d-262">The tab gallery appears.</span></span>

    ![Опыт предварительного собрания](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="24c0d-264">В галерее вкладок выберите приложение, которое необходимо добавить, и выполните необходимые действия.</span><span class="sxs-lookup"><span data-stu-id="24c0d-264">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="24c0d-265">Приложение устанавливается в качестве вкладки.</span><span class="sxs-lookup"><span data-stu-id="24c0d-265">The app is installed as a tab.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="24c0d-266">В настоящее время на вкладке "Собрания" сведения о собраниях и сведения о участниках не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="24c0d-266">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="24c0d-267">**Добавление расширения обмена сообщениями на собрание**</span><span class="sxs-lookup"><span data-stu-id="24c0d-267">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="24c0d-268">Выберите меню эллипсов или &#x25CF;&#x25CF;&#x25CF; , расположенное в области композитных сообщений в чате.</span><span class="sxs-lookup"><span data-stu-id="24c0d-268">Select the ellipses or overflow menu &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="24c0d-269">Выберите приложение, которое необходимо добавить, и выполните необходимые действия.</span><span class="sxs-lookup"><span data-stu-id="24c0d-269">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="24c0d-270">Приложение устанавливается в качестве расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="24c0d-270">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="24c0d-271">**Добавление бота на собрание**</span><span class="sxs-lookup"><span data-stu-id="24c0d-271">**To add a bot to a meeting**</span></span>

<span data-ttu-id="24c0d-272">В чате собраний **@** введите ключ и выберите **Get bots**.</span><span class="sxs-lookup"><span data-stu-id="24c0d-272">In a meeting chat enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="24c0d-273">Удостоверение пользователя должно быть подтверждено с помощью [SSO Tabs.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="24c0d-273">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="24c0d-274">После проверки подлинности приложение может получить роль пользователя с помощью `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="24c0d-274">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="24c0d-275">В зависимости от роли пользователя приложение может предоставлять определенные функции.</span><span class="sxs-lookup"><span data-stu-id="24c0d-275">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="24c0d-276">Например, приложение для опроса позволяет создавать новый опрос только организаторам и презентаторам.</span><span class="sxs-lookup"><span data-stu-id="24c0d-276">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="24c0d-277">Назначения ролей могут быть изменены во время собрания.</span><span class="sxs-lookup"><span data-stu-id="24c0d-277">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="24c0d-278">Дополнительные сведения см. [в сведениях о ролях в собрании Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="24c0d-278">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="24c0d-279">Во время собрания</span><span class="sxs-lookup"><span data-stu-id="24c0d-279">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="24c0d-280">sidePanel</span><span class="sxs-lookup"><span data-stu-id="24c0d-280">sidePanel</span></span>

<span data-ttu-id="24c0d-281">В sidePanel можно настроить опыт собрания, который позволяет организаторам и презентаторам иметь различные представления и действия.</span><span class="sxs-lookup"><span data-stu-id="24c0d-281">With the sidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="24c0d-282">В манифесте приложения необходимо добавить sidePanel в массив контекста.</span><span class="sxs-lookup"><span data-stu-id="24c0d-282">In your app manifest, you must add sidePanel to the context array.</span></span> <span data-ttu-id="24c0d-283">В собрании и во всех сценариях приложение отрисовка в вкладке в собрании шириной 320 пикселей.</span><span class="sxs-lookup"><span data-stu-id="24c0d-283">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="24c0d-284">Дополнительные сведения см. в [интерфейсе FrameContext.](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="24c0d-284">For more information, see [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span></span>

<span data-ttu-id="24c0d-285">Чтобы использовать `userContext` API для соответственного маршрута запросов, см. [в рубрике Teams SDK.](../tabs/how-to/access-teams-context.md#user-context)</span><span class="sxs-lookup"><span data-stu-id="24c0d-285">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="24c0d-286">См. [поток проверки подлинности Teams для вкладок.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="24c0d-286">See [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="24c0d-287">Поток проверки подлинности для вкладок очень похож на поток auth для веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="24c0d-287">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="24c0d-288">Таким образом, вкладки могут напрямую использовать OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="24c0d-288">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="24c0d-289">См., платформа удостоверений Майкрософт и поток кода авторизации [OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)</span><span class="sxs-lookup"><span data-stu-id="24c0d-289">See, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="24c0d-290">Расширение обмена сообщениями работает так, как и ожидалось, когда пользователь находится в представлении на собрании, и пользователь может отправлять составить карточки расширения сообщений.</span><span class="sxs-lookup"><span data-stu-id="24c0d-290">Messaging extension works as expected when a user is in an in-meeting view and the user can post compose message extension cards.</span></span> <span data-ttu-id="24c0d-291">AppName in-meeting — это инструмент, который сообщает имя приложения на собрании U-bar.</span><span class="sxs-lookup"><span data-stu-id="24c0d-291">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="24c0d-292">Диалоговое окно собрания</span><span class="sxs-lookup"><span data-stu-id="24c0d-292">In-meeting dialog</span></span>

<span data-ttu-id="24c0d-293">Диалоговое окно на собрании можно использовать для вовлечения участников во время собрания и сбора сведений или отзывов во время собрания.</span><span class="sxs-lookup"><span data-stu-id="24c0d-293">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="24c0d-294">Используйте [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API для сигнала о том, что необходимо вызвать уведомление о пузыре.</span><span class="sxs-lookup"><span data-stu-id="24c0d-294">Use the [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="24c0d-295">В качестве полезной нагрузки запроса уведомлений включайте URL-адрес, на котором будет хозяйствовать контент.</span><span class="sxs-lookup"><span data-stu-id="24c0d-295">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="24c0d-296">Диалоговое окно на собрании не должно использовать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="24c0d-296">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="24c0d-297">Модуль задач не вызывается в чате собрания.</span><span class="sxs-lookup"><span data-stu-id="24c0d-297">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="24c0d-298">Url-адрес внешнего ресурса используется для отображения пузыря контента на собрании.</span><span class="sxs-lookup"><span data-stu-id="24c0d-298">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="24c0d-299">Этот метод можно `submitTask` использовать для отправки данных в чате собраний.</span><span class="sxs-lookup"><span data-stu-id="24c0d-299">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="24c0d-300">Необходимо вызвать функцию [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического увольнения после действия пользователя в веб-представлении.</span><span class="sxs-lookup"><span data-stu-id="24c0d-300">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web-view.</span></span> <span data-ttu-id="24c0d-301">Это требование для отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="24c0d-301">This is a requirement for app submission.</span></span> <span data-ttu-id="24c0d-302">Дополнительные сведения см. в [модуле задач Teams SDK.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="24c0d-302">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="24c0d-303">Если вы хотите, чтобы ваше приложение поддержало анонимных пользователей, то при первоначальном запросе необходимо использовать метаданные запроса в объекте, а не `from.id` `from` `from.aadObjectId` метаданные запроса.</span><span class="sxs-lookup"><span data-stu-id="24c0d-303">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="24c0d-304">`from.id` является ИД пользователя и `from.aadObjectId` является ИД Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="24c0d-304">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="24c0d-305">Дополнительные сведения см. в [таблицах](../task-modules-and-cards/task-modules/task-modules-tabs.md) с использованием модулей задач и созданием и [отправкой модуля задач.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="24c0d-305">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="24c0d-306">После собрания</span><span class="sxs-lookup"><span data-stu-id="24c0d-306">After a meeting</span></span>

<span data-ttu-id="24c0d-307">Конфигурации после собрания и предварительного собрания эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="24c0d-307">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="code-sample"></a><span data-ttu-id="24c0d-308">Пример кода</span><span class="sxs-lookup"><span data-stu-id="24c0d-308">Code sample</span></span>

|<span data-ttu-id="24c0d-309">Пример имени</span><span class="sxs-lookup"><span data-stu-id="24c0d-309">Sample name</span></span> | <span data-ttu-id="24c0d-310">Описание</span><span class="sxs-lookup"><span data-stu-id="24c0d-310">Description</span></span> | <span data-ttu-id="24c0d-311">C #</span><span class="sxs-lookup"><span data-stu-id="24c0d-311">C#</span></span> |
|----------------|-----------------|--------------|
| <span data-ttu-id="24c0d-312">Разнонасть собраний</span><span class="sxs-lookup"><span data-stu-id="24c0d-312">Meetings extensibility</span></span> | <span data-ttu-id="24c0d-313">Пример extensibility microsoft Teams для передачи маркеров.</span><span class="sxs-lookup"><span data-stu-id="24c0d-313">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="24c0d-314">View</span><span class="sxs-lookup"><span data-stu-id="24c0d-314">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) |
| <span data-ttu-id="24c0d-315">Бот-бот для пузырьков контента для собраний</span><span class="sxs-lookup"><span data-stu-id="24c0d-315">Meeting content bubble bot</span></span> | <span data-ttu-id="24c0d-316">Пример extensibility microsoft Teams для взаимодействия с ботом пузырьков контента на собрании.</span><span class="sxs-lookup"><span data-stu-id="24c0d-316">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="24c0d-317">View</span><span class="sxs-lookup"><span data-stu-id="24c0d-317">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |

## <a name="see-also"></a><span data-ttu-id="24c0d-318">См. также</span><span class="sxs-lookup"><span data-stu-id="24c0d-318">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="24c0d-319">Рекомендации по проектированию диалогов на собрании</span><span class="sxs-lookup"><span data-stu-id="24c0d-319">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
> [!div class="nextstepaction"]
> [<span data-ttu-id="24c0d-320">Поток проверки подлинности teams для вкладок</span><span class="sxs-lookup"><span data-stu-id="24c0d-320">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
