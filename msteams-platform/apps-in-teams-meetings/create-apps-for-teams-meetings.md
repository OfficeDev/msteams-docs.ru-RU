---
title: Создание приложений для собраний групп
author: laujan
description: создание приложений для собраний групп
ms.topic: conceptual
ms.author: lajanuar
keywords: teams apps meetings user participant role api
ms.openlocfilehash: 267c90792e07b483c92965bc61e46fca33573841
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654377"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="1acf1-104">Создание приложений для собраний Teams</span><span class="sxs-lookup"><span data-stu-id="1acf1-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="1acf1-105">Предпосылки и соображения</span><span class="sxs-lookup"><span data-stu-id="1acf1-105">Prerequisites and considerations</span></span>

<span data-ttu-id="1acf1-106">Прежде чем создавать приложения для собраний Teams, необходимо иметь представление о следующих ниже.</span><span class="sxs-lookup"><span data-stu-id="1acf1-106">Before you create apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="1acf1-107">Вы должны иметь знания о разработке приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="1acf1-107">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="1acf1-108">Дополнительные сведения см. в [приложении Teams.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="1acf1-108">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="1acf1-109">Необходимо обновить манифест приложения Teams, чтобы указать, что приложение доступно для собраний.</span><span class="sxs-lookup"><span data-stu-id="1acf1-109">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="1acf1-110">Дополнительные сведения см. в [манифесте приложения.](#update-your-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="1acf1-110">For more information, see [app manifest](#update-your-app-manifest).</span></span>

* <span data-ttu-id="1acf1-111">Чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки, оно должно поддерживать настраиваемые вкладки в области groupchat.</span><span class="sxs-lookup"><span data-stu-id="1acf1-111">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the groupchat scope.</span></span> <span data-ttu-id="1acf1-112">Дополнительные сведения см. в [поле groupchat и](../resources/schema/manifest-schema.md#configurabletabs) [создайте вкладку группы.](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="1acf1-112">For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="1acf1-113">Необходимо придерживаться общих правил разработки вкладок Teams для сценариев до и после собрания.</span><span class="sxs-lookup"><span data-stu-id="1acf1-113">You must adhere to general Teams tab design guidelines for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="1acf1-114">Для работы во время собраний обратитесь к вкладке на собрании и рекомендациям по проектированию диалогов на собрании.</span><span class="sxs-lookup"><span data-stu-id="1acf1-114">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="1acf1-115">Дополнительные сведения см. в рекомендациях по разработке вкладок [Teams,](../tabs/design/tabs.md)рекомендациях по разработке вкладок на собрании и рекомендациях по проектированию диалогов на [собрании.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)</span><span class="sxs-lookup"><span data-stu-id="1acf1-115">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="1acf1-116">Необходимо поддерживать область, чтобы включить приложение в чаты перед собранием и `groupchat` после собрания.</span><span class="sxs-lookup"><span data-stu-id="1acf1-116">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="1acf1-117">С помощью предварительного собрания приложения можно найти и добавить приложения для собраний и выполнить задачи перед собранием.</span><span class="sxs-lookup"><span data-stu-id="1acf1-117">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="1acf1-118">С помощью приложения после собрания можно просмотреть результаты собрания, такие как результаты опроса или отзывы.</span><span class="sxs-lookup"><span data-stu-id="1acf1-118">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="1acf1-119">Параметры URL-адресов API должны иметь `meetingId` и `userId` `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="1acf1-119">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="1acf1-120">Они доступны в рамках клиентской SDK и бот-активности Teams.</span><span class="sxs-lookup"><span data-stu-id="1acf1-120">These are available as part of the Teams client SDK and bot activity.</span></span> <span data-ttu-id="1acf1-121">Кроме того, с помощью проверки подлинности [Tab SSO](../tabs/how-to/authentication/auth-aad-sso.md)можно получить достоверную информацию для идентификации пользователя и идентификации клиента.</span><span class="sxs-lookup"><span data-stu-id="1acf1-121">In addition, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="1acf1-122">API `GetParticipant` должен иметь регистрацию бота и ID для создания маркеров auth.</span><span class="sxs-lookup"><span data-stu-id="1acf1-122">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="1acf1-123">Дополнительные сведения см. в [сведениях о регистрации ботов и ID.](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="1acf1-123">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="1acf1-124">Чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть обновлено в зависимости от событий на собрании.</span><span class="sxs-lookup"><span data-stu-id="1acf1-124">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="1acf1-125">Эти события могут быть в диалоговом окне собрания и на других этапах жизненного цикла собрания.</span><span class="sxs-lookup"><span data-stu-id="1acf1-125">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="1acf1-126">Параметр завершения в диалоговом окне на собрании см. `bot Id` в `Notification Signal API` .</span><span class="sxs-lookup"><span data-stu-id="1acf1-126">For the in-meeting dialog box, see completion `bot Id` parameter in `Notification Signal API`.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="1acf1-127">Ссылка на API приложений для собраний</span><span class="sxs-lookup"><span data-stu-id="1acf1-127">Meeting apps API reference</span></span>

|<span data-ttu-id="1acf1-128">API</span><span class="sxs-lookup"><span data-stu-id="1acf1-128">API</span></span>|<span data-ttu-id="1acf1-129">Описание</span><span class="sxs-lookup"><span data-stu-id="1acf1-129">Description</span></span>|<span data-ttu-id="1acf1-130">Запрос</span><span class="sxs-lookup"><span data-stu-id="1acf1-130">Request</span></span>|<span data-ttu-id="1acf1-131">Source</span><span class="sxs-lookup"><span data-stu-id="1acf1-131">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="1acf1-132">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="1acf1-132">**GetUserContext**</span></span>| <span data-ttu-id="1acf1-133">Этот API позволяет получать контекстную информацию для отображения соответствующего контента на вкладке Teams.</span><span class="sxs-lookup"><span data-stu-id="1acf1-133">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="1acf1-134">_**microsoftTeams.getContext() => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="1acf1-134">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="1acf1-135">Клиент Microsoft Teams SDK</span><span class="sxs-lookup"><span data-stu-id="1acf1-135">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="1acf1-136">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="1acf1-136">**GetParticipant**</span></span>| <span data-ttu-id="1acf1-137">Этот API позволяет боту получать сведения о участниках, встречая ID и ID участника.</span><span class="sxs-lookup"><span data-stu-id="1acf1-137">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="1acf1-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="1acf1-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="1acf1-139">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="1acf1-139">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="1acf1-140">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="1acf1-140">**NotificationSignal**</span></span> | <span data-ttu-id="1acf1-141">Этот API позволяет предоставлять сигналы собрания, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота.</span><span class="sxs-lookup"><span data-stu-id="1acf1-141">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="1acf1-142">Он позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно на собрании.</span><span class="sxs-lookup"><span data-stu-id="1acf1-142">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="1acf1-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="1acf1-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="1acf1-144">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="1acf1-144">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="1acf1-145">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="1acf1-145">GetUserContext</span></span>

<span data-ttu-id="1acf1-146">Чтобы определить и получить контекстную информацию для содержимого вкладки, см. в тексте получить контекст [для вкладки Teams.](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) `meetingId` используется вкладками при работе в контексте собрания и добавляется для полезной нагрузки ответа.</span><span class="sxs-lookup"><span data-stu-id="1acf1-146">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="1acf1-147">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="1acf1-147">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="1acf1-148">Не кэшить роли участников, так как организатор собрания может изменить роль в любое время.</span><span class="sxs-lookup"><span data-stu-id="1acf1-148">Do not cache participant roles since the meeting organizer can change a role any time.</span></span>
> * <span data-ttu-id="1acf1-149">В настоящее время teams не поддерживают большие списки рассылки или размер реестра, вметив более 350 `GetParticipant` участников для API.</span><span class="sxs-lookup"><span data-stu-id="1acf1-149">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="1acf1-150">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="1acf1-150">Query parameters</span></span>

|<span data-ttu-id="1acf1-151">Значение</span><span class="sxs-lookup"><span data-stu-id="1acf1-151">Value</span></span>|<span data-ttu-id="1acf1-152">Тип</span><span class="sxs-lookup"><span data-stu-id="1acf1-152">Type</span></span>|<span data-ttu-id="1acf1-153">Обязательный</span><span class="sxs-lookup"><span data-stu-id="1acf1-153">Required</span></span>|<span data-ttu-id="1acf1-154">Описание</span><span class="sxs-lookup"><span data-stu-id="1acf1-154">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="1acf1-155">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="1acf1-155">**meetingId**</span></span>| <span data-ttu-id="1acf1-156">string</span><span class="sxs-lookup"><span data-stu-id="1acf1-156">string</span></span> | <span data-ttu-id="1acf1-157">Да</span><span class="sxs-lookup"><span data-stu-id="1acf1-157">Yes</span></span> | <span data-ttu-id="1acf1-158">Идентификатор собрания доступен через Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="1acf1-158">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="1acf1-159">**participantId**</span><span class="sxs-lookup"><span data-stu-id="1acf1-159">**participantId**</span></span>| <span data-ttu-id="1acf1-160">string</span><span class="sxs-lookup"><span data-stu-id="1acf1-160">string</span></span> | <span data-ttu-id="1acf1-161">Да</span><span class="sxs-lookup"><span data-stu-id="1acf1-161">Yes</span></span> | <span data-ttu-id="1acf1-162">ID участника — это пользовательский ИД.</span><span class="sxs-lookup"><span data-stu-id="1acf1-162">The participant ID is the user ID.</span></span> <span data-ttu-id="1acf1-163">Он доступен в SSO tab, Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="1acf1-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="1acf1-164">Рекомендуется получить ID участника из SSO Tab.</span><span class="sxs-lookup"><span data-stu-id="1acf1-164">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="1acf1-165">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="1acf1-165">**tenantId**</span></span>| <span data-ttu-id="1acf1-166">string</span><span class="sxs-lookup"><span data-stu-id="1acf1-166">string</span></span> | <span data-ttu-id="1acf1-167">Да</span><span class="sxs-lookup"><span data-stu-id="1acf1-167">Yes</span></span> | <span data-ttu-id="1acf1-168">Для пользователей-клиентов требуется ID клиента.</span><span class="sxs-lookup"><span data-stu-id="1acf1-168">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="1acf1-169">Он доступен в SSO tab, Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="1acf1-169">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="1acf1-170">Рекомендуется получить ID клиента из SSO tab.</span><span class="sxs-lookup"><span data-stu-id="1acf1-170">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="1acf1-171">Пример</span><span class="sxs-lookup"><span data-stu-id="1acf1-171">Example</span></span>

# <a name="c"></a>[<span data-ttu-id="1acf1-172">C#</span><span class="sxs-lookup"><span data-stu-id="1acf1-172">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="1acf1-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1acf1-173">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="1acf1-174">JSON</span><span class="sxs-lookup"><span data-stu-id="1acf1-174">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="1acf1-175">Тело ответа JSON для `GetParticipant` API:</span><span class="sxs-lookup"><span data-stu-id="1acf1-175">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="1acf1-176">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="1acf1-176">Response codes</span></span>

|<span data-ttu-id="1acf1-177">Код ответа</span><span class="sxs-lookup"><span data-stu-id="1acf1-177">Response code</span></span>|<span data-ttu-id="1acf1-178">Описание</span><span class="sxs-lookup"><span data-stu-id="1acf1-178">Description</span></span>|
|---|---|
| <span data-ttu-id="1acf1-179">**403**</span><span class="sxs-lookup"><span data-stu-id="1acf1-179">**403**</span></span> | <span data-ttu-id="1acf1-180">Приложение не может получать сведения о участниках.</span><span class="sxs-lookup"><span data-stu-id="1acf1-180">The app is not allowed to get participant information.</span></span> <span data-ttu-id="1acf1-181">Это наиболее распространенный ответ на ошибки, который запускается, если приложение не установлено на собрании.</span><span class="sxs-lookup"><span data-stu-id="1acf1-181">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="1acf1-182">Например, если приложение отключено администратором клиента или заблокировано во время переноса веб-сайтов в прямом эфире.</span><span class="sxs-lookup"><span data-stu-id="1acf1-182">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="1acf1-183">**200**</span><span class="sxs-lookup"><span data-stu-id="1acf1-183">**200**</span></span> | <span data-ttu-id="1acf1-184">Данные участника успешно извлекаются.</span><span class="sxs-lookup"><span data-stu-id="1acf1-184">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="1acf1-185">**401**</span><span class="sxs-lookup"><span data-stu-id="1acf1-185">**401**</span></span> | <span data-ttu-id="1acf1-186">Приложение отвечает недействительным маркером.</span><span class="sxs-lookup"><span data-stu-id="1acf1-186">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="1acf1-187">**404**</span><span class="sxs-lookup"><span data-stu-id="1acf1-187">**404**</span></span> | <span data-ttu-id="1acf1-188">Собрание истеко или участник не может быть найден.</span><span class="sxs-lookup"><span data-stu-id="1acf1-188">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="1acf1-189">**500**</span><span class="sxs-lookup"><span data-stu-id="1acf1-189">**500**</span></span> | <span data-ttu-id="1acf1-190">Срок действия собрания истек более 60 дней с момента окончания собрания, либо у участника нет разрешений, основанных на их роли.</span><span class="sxs-lookup"><span data-stu-id="1acf1-190">The meeting has either expired more than 60 days since the meeting ended or the participant does not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="1acf1-191">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="1acf1-191">NotificationSignal API</span></span>

<span data-ttu-id="1acf1-192">Все пользователи на собрании получают уведомления, отправленные через `NotificationSignal` API.</span><span class="sxs-lookup"><span data-stu-id="1acf1-192">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="1acf1-193">При вызове диалогового окна на собрании содержимое представляется в качестве сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="1acf1-193">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="1acf1-194">В настоящее время отправка целевых уведомлений не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="1acf1-194">Currently, sending targeted notifications is not supported.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="1acf1-195">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="1acf1-195">Query parameters</span></span>

|<span data-ttu-id="1acf1-196">Значение</span><span class="sxs-lookup"><span data-stu-id="1acf1-196">Value</span></span>|<span data-ttu-id="1acf1-197">Тип</span><span class="sxs-lookup"><span data-stu-id="1acf1-197">Type</span></span>|<span data-ttu-id="1acf1-198">Обязательный</span><span class="sxs-lookup"><span data-stu-id="1acf1-198">Required</span></span>|<span data-ttu-id="1acf1-199">Описание</span><span class="sxs-lookup"><span data-stu-id="1acf1-199">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="1acf1-200">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="1acf1-200">**conversationId**</span></span>| <span data-ttu-id="1acf1-201">string</span><span class="sxs-lookup"><span data-stu-id="1acf1-201">string</span></span> | <span data-ttu-id="1acf1-202">Да</span><span class="sxs-lookup"><span data-stu-id="1acf1-202">Yes</span></span> | <span data-ttu-id="1acf1-203">Идентификатор беседы доступен в рамках вызова бота</span><span class="sxs-lookup"><span data-stu-id="1acf1-203">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="1acf1-204">Пример</span><span class="sxs-lookup"><span data-stu-id="1acf1-204">Example</span></span>

<span data-ttu-id="1acf1-205">Объявляется `Bot ID` в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="1acf1-205">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="1acf1-206">Параметр `completionBotId` необязательный `externalResourceUrl` в примере запрашиваемой полезной нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1acf1-206">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="1acf1-207">`Bot ID` объявляется в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="1acf1-207">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="1acf1-208">Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях.</span><span class="sxs-lookup"><span data-stu-id="1acf1-208">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="1acf1-209">Чтобы размеры были в пределах допустимого, см. в [рекомендациях по проектированию.](design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="1acf1-209">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="1acf1-210">URL-адрес — это страница, загруженная в диалоговом окне на `<iframe>` собрании.</span><span class="sxs-lookup"><span data-stu-id="1acf1-210">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="1acf1-211">Домен должен быть в массиве приложения в `validDomains` манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="1acf1-211">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="c"></a>[<span data-ttu-id="1acf1-212">C#</span><span class="sxs-lookup"><span data-stu-id="1acf1-212">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="1acf1-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1acf1-213">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="1acf1-214">JSON</span><span class="sxs-lookup"><span data-stu-id="1acf1-214">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="1acf1-215">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="1acf1-215">Response codes</span></span>

|<span data-ttu-id="1acf1-216">Код ответа</span><span class="sxs-lookup"><span data-stu-id="1acf1-216">Response code</span></span>|<span data-ttu-id="1acf1-217">Описание</span><span class="sxs-lookup"><span data-stu-id="1acf1-217">Description</span></span>|
|---|---|
| <span data-ttu-id="1acf1-218">**201**</span><span class="sxs-lookup"><span data-stu-id="1acf1-218">**201**</span></span> | <span data-ttu-id="1acf1-219">Успешно отправляется действие с сигналом</span><span class="sxs-lookup"><span data-stu-id="1acf1-219">The activity with signal is successfully sent</span></span> |
| <span data-ttu-id="1acf1-220">**401**</span><span class="sxs-lookup"><span data-stu-id="1acf1-220">**401**</span></span> | <span data-ttu-id="1acf1-221">Приложение отвечает недействительным маркером.</span><span class="sxs-lookup"><span data-stu-id="1acf1-221">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="1acf1-222">**403**</span><span class="sxs-lookup"><span data-stu-id="1acf1-222">**403**</span></span> | <span data-ttu-id="1acf1-223">Приложение не может отправить сигнал.</span><span class="sxs-lookup"><span data-stu-id="1acf1-223">The app is unable to send the signal.</span></span> <span data-ttu-id="1acf1-224">Это может произойти из-за различных причин, таких как отключение приложения администратором клиента, блокировка приложения во время переноса веб-сайта в прямом эфире и так далее.</span><span class="sxs-lookup"><span data-stu-id="1acf1-224">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="1acf1-225">В этом случае полезное сообщение содержит подробное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="1acf1-225">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="1acf1-226">**404**</span><span class="sxs-lookup"><span data-stu-id="1acf1-226">**404**</span></span> | <span data-ttu-id="1acf1-227">Чат собрания не существует.</span><span class="sxs-lookup"><span data-stu-id="1acf1-227">The meeting chat does not exist.</span></span> |

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="1acf1-228">Включить приложение для собраний Teams</span><span class="sxs-lookup"><span data-stu-id="1acf1-228">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="1acf1-229">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="1acf1-229">Update your app manifest</span></span>

<span data-ttu-id="1acf1-230">Возможности приложения собраний объявляются в манифесте приложения с помощью `configurableTabs` массивов и `scopes` `context` массивов.</span><span class="sxs-lookup"><span data-stu-id="1acf1-230">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="1acf1-231">Область определяет, кому и в котором контекст определяет, где доступно ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="1acf1-231">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> <span data-ttu-id="1acf1-232">Попробуйте обновить манифест приложения с помощью [схемы манифеста.](../resources/schema/manifest-schema-dev-preview.md)</span><span class="sxs-lookup"><span data-stu-id="1acf1-232">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> <span data-ttu-id="1acf1-233">Приложениям на собраниях нужна *область группового чата.*</span><span class="sxs-lookup"><span data-stu-id="1acf1-233">Apps in meetings need *groupchat* scope.</span></span> <span data-ttu-id="1acf1-234">Область *команды* работает только для вкладок в каналах.</span><span class="sxs-lookup"><span data-stu-id="1acf1-234">The *team* scope works for tabs in channels only.</span></span>

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
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```
> [!NOTE]
> <span data-ttu-id="1acf1-235">`meetingStage` в настоящее время доступна только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="1acf1-235">`meetingStage` is currently available in developer preview only.</span></span>

### <a name="context-property"></a><span data-ttu-id="1acf1-236">Свойство Context</span><span class="sxs-lookup"><span data-stu-id="1acf1-236">Context property</span></span>

<span data-ttu-id="1acf1-237">Вкладка `context` и свойства позволяют `scopes` определить, где должно отображаться ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="1acf1-237">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="1acf1-238">Вкладки в области или области `team` `groupchat` могут иметь несколько контекстов.</span><span class="sxs-lookup"><span data-stu-id="1acf1-238">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="1acf1-239">Ниже ниже 10 значений для свойства, из которого можно использовать все или некоторые `context` из этих значений:</span><span class="sxs-lookup"><span data-stu-id="1acf1-239">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="1acf1-240">Значение</span><span class="sxs-lookup"><span data-stu-id="1acf1-240">Value</span></span>|<span data-ttu-id="1acf1-241">Описание</span><span class="sxs-lookup"><span data-stu-id="1acf1-241">Description</span></span>|
|---|---|
| <span data-ttu-id="1acf1-242">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="1acf1-242">**channelTab**</span></span> | <span data-ttu-id="1acf1-243">Вкладка в загонах канала команды.</span><span class="sxs-lookup"><span data-stu-id="1acf1-243">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="1acf1-244">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="1acf1-244">**privateChatTab**</span></span> | <span data-ttu-id="1acf1-245">Вкладка в загонах группового чата между набором пользователей, не в контексте группы или собрания.</span><span class="sxs-lookup"><span data-stu-id="1acf1-245">A tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="1acf1-246">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="1acf1-246">**meetingChatTab**</span></span> | <span data-ttu-id="1acf1-247">Вкладка в загонах группового чата между набором пользователей в контексте запланированного собрания.</span><span class="sxs-lookup"><span data-stu-id="1acf1-247">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="1acf1-248">**meetingDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="1acf1-248">**meetingDetailsTab**</span></span> | <span data-ttu-id="1acf1-249">Вкладка в загонах сведений о собрании для просмотра календаря.</span><span class="sxs-lookup"><span data-stu-id="1acf1-249">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="1acf1-250">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="1acf1-250">**meetingSidePanel**</span></span> | <span data-ttu-id="1acf1-251">Панель на собрании, открытая с помощью единой панели (U-bar).</span><span class="sxs-lookup"><span data-stu-id="1acf1-251">An in-meeting panel opened via the unified bar (U-bar).</span></span> |
| <span data-ttu-id="1acf1-252">**meetingStage**</span><span class="sxs-lookup"><span data-stu-id="1acf1-252">**meetingStage**</span></span> | <span data-ttu-id="1acf1-253">Приложение из боковогопанеля можно использовать на стадии собрания.</span><span class="sxs-lookup"><span data-stu-id="1acf1-253">An app from the sidepanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="1acf1-254">`Context` свойство в настоящее время не поддерживается для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="1acf1-254">`Context` property is currently not supported on mobile clients.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="1acf1-255">Настройка приложения для сценариев собраний</span><span class="sxs-lookup"><span data-stu-id="1acf1-255">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="1acf1-256">Чтобы приложение было видимым в галерее вкладок, оно должно поддерживать настраиваемые вкладки и область группового чата.</span><span class="sxs-lookup"><span data-stu-id="1acf1-256">For your app to be visible in the tab gallery it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="1acf1-257">Мобильные клиенты поддерживают вкладки только на этапах предварительного и после собраний.</span><span class="sxs-lookup"><span data-stu-id="1acf1-257">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="1acf1-258">В настоящее время в мобильных клиентах не поддерживается диалоговое окно и вкладка на собрании.</span><span class="sxs-lookup"><span data-stu-id="1acf1-258">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="1acf1-259">Дополнительные сведения см. [в руководстве по вкладки на мобильных](../tabs/design/tabs-mobile.md) устройствах при создании вкладок для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="1acf1-259">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="1acf1-260">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="1acf1-260">Before a meeting</span></span>

<span data-ttu-id="1acf1-261">Перед собранием пользователи могут добавлять вкладки, боты и расширения обмена сообщениями на собрание.</span><span class="sxs-lookup"><span data-stu-id="1acf1-261">Before a meeting, users can add tabs, bots and messaging extensions to a meeting.</span></span> <span data-ttu-id="1acf1-262">Пользователи с ролями организатора и презентовщика могут добавлять вкладки в собрание.</span><span class="sxs-lookup"><span data-stu-id="1acf1-262">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="1acf1-263">**Добавление вкладки к собранию**</span><span class="sxs-lookup"><span data-stu-id="1acf1-263">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="1acf1-264">В календаре выберите собрание, на которое нужно добавить вкладку.</span><span class="sxs-lookup"><span data-stu-id="1acf1-264">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="1acf1-265">Выберите **вкладку Details** и выберите плюс</span><span class="sxs-lookup"><span data-stu-id="1acf1-265">Select the **Details** tab and select plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="1acf1-266">.</span><span class="sxs-lookup"><span data-stu-id="1acf1-266">.</span></span> <span data-ttu-id="1acf1-267">Отображается галерея вкладок.</span><span class="sxs-lookup"><span data-stu-id="1acf1-267">The tab gallery appears.</span></span>

    ![Опыт предварительного собрания](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="1acf1-269">В галерее вкладок выберите приложение, которое необходимо добавить, и выполните необходимые действия.</span><span class="sxs-lookup"><span data-stu-id="1acf1-269">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="1acf1-270">Приложение устанавливается в качестве вкладки.</span><span class="sxs-lookup"><span data-stu-id="1acf1-270">The app is installed as a tab.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="1acf1-271">В настоящее время на вкладке "Собрания" сведения о собраниях и сведения о участниках не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="1acf1-271">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="1acf1-272">**Добавление расширения обмена сообщениями на собрание**</span><span class="sxs-lookup"><span data-stu-id="1acf1-272">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="1acf1-273">Выберите меню эллипсов или &#x25CF;&#x25CF;&#x25CF; , расположенное в области композитных сообщений в чате.</span><span class="sxs-lookup"><span data-stu-id="1acf1-273">Select the ellipses or overflow menu &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="1acf1-274">Выберите приложение, которое необходимо добавить, и выполните необходимые действия.</span><span class="sxs-lookup"><span data-stu-id="1acf1-274">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="1acf1-275">Приложение устанавливается в качестве расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="1acf1-275">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="1acf1-276">**Добавление бота на собрание**</span><span class="sxs-lookup"><span data-stu-id="1acf1-276">**To add a bot to a meeting**</span></span>

<span data-ttu-id="1acf1-277">В чате собраний **@** введите ключ и выберите **Get bots**.</span><span class="sxs-lookup"><span data-stu-id="1acf1-277">In a meeting chat enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="1acf1-278">Удостоверение пользователя должно быть подтверждено с помощью [SSO Tabs.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="1acf1-278">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="1acf1-279">После проверки подлинности приложение может получить роль пользователя с помощью `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="1acf1-279">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="1acf1-280">В зависимости от роли пользователя приложение может предоставлять определенные функции.</span><span class="sxs-lookup"><span data-stu-id="1acf1-280">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="1acf1-281">Например, приложение для опроса позволяет создавать новый опрос только организаторам и презентаторам.</span><span class="sxs-lookup"><span data-stu-id="1acf1-281">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="1acf1-282">Назначения ролей могут быть изменены во время собрания.</span><span class="sxs-lookup"><span data-stu-id="1acf1-282">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="1acf1-283">Дополнительные сведения см. [в сведениях о ролях в собрании Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="1acf1-283">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="1acf1-284">Во время собрания</span><span class="sxs-lookup"><span data-stu-id="1acf1-284">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="1acf1-285">sidePanel</span><span class="sxs-lookup"><span data-stu-id="1acf1-285">sidePanel</span></span>

<span data-ttu-id="1acf1-286">В sidePanel можно настроить опыт собрания, который позволяет организаторам и презентаторам иметь различные представления и действия.</span><span class="sxs-lookup"><span data-stu-id="1acf1-286">With the sidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="1acf1-287">В манифесте приложения необходимо добавить sidePanel в массив контекста.</span><span class="sxs-lookup"><span data-stu-id="1acf1-287">In your app manifest, you must add sidePanel to the context array.</span></span> <span data-ttu-id="1acf1-288">В собрании и во всех сценариях приложение отрисовка в вкладке в собрании шириной 320 пикселей.</span><span class="sxs-lookup"><span data-stu-id="1acf1-288">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="1acf1-289">Дополнительные сведения см. в [интерфейсе FrameContext.](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="1acf1-289">For more information, see [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span></span>

<span data-ttu-id="1acf1-290">Чтобы использовать `userContext` API для соответственного маршрута запросов, см. [в рубрике Teams SDK.](../tabs/how-to/access-teams-context.md#user-context)</span><span class="sxs-lookup"><span data-stu-id="1acf1-290">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="1acf1-291">См. [поток проверки подлинности Teams для вкладок.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="1acf1-291">See [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="1acf1-292">Поток проверки подлинности для вкладок очень похож на поток auth для веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="1acf1-292">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="1acf1-293">Таким образом, вкладки могут напрямую использовать OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1acf1-293">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="1acf1-294">См., платформа удостоверений Майкрософт и поток кода авторизации [OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)</span><span class="sxs-lookup"><span data-stu-id="1acf1-294">See, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="1acf1-295">Расширение обмена сообщениями работает так, как и ожидалось, когда пользователь находится в представлении на собрании, и пользователь может отправлять составить карточки расширения сообщений.</span><span class="sxs-lookup"><span data-stu-id="1acf1-295">Messaging extension works as expected when a user is in an in-meeting view and the user can post compose message extension cards.</span></span> <span data-ttu-id="1acf1-296">AppName in-meeting — это инструмент, который сообщает имя приложения на собрании U-bar.</span><span class="sxs-lookup"><span data-stu-id="1acf1-296">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="1acf1-297">Диалоговое окно собрания</span><span class="sxs-lookup"><span data-stu-id="1acf1-297">In-meeting dialog</span></span>

<span data-ttu-id="1acf1-298">Диалоговое окно на собрании можно использовать для вовлечения участников во время собрания и сбора сведений или отзывов во время собрания.</span><span class="sxs-lookup"><span data-stu-id="1acf1-298">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="1acf1-299">Используйте [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API для сигнала о том, что необходимо вызвать уведомление о пузыре.</span><span class="sxs-lookup"><span data-stu-id="1acf1-299">Use the [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="1acf1-300">В качестве полезной нагрузки запроса уведомлений включайте URL-адрес, на котором будет хозяйствовать контент.</span><span class="sxs-lookup"><span data-stu-id="1acf1-300">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="1acf1-301">Диалоговое окно на собрании не должно использовать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="1acf1-301">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="1acf1-302">Модуль задач не вызывается в чате собрания.</span><span class="sxs-lookup"><span data-stu-id="1acf1-302">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="1acf1-303">Url-адрес внешнего ресурса используется для отображения пузыря контента на собрании.</span><span class="sxs-lookup"><span data-stu-id="1acf1-303">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="1acf1-304">Этот метод можно `submitTask` использовать для отправки данных в чате собраний.</span><span class="sxs-lookup"><span data-stu-id="1acf1-304">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="1acf1-305">Необходимо вызвать функцию [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического увольнения после действия пользователя в веб-представлении.</span><span class="sxs-lookup"><span data-stu-id="1acf1-305">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web-view.</span></span> <span data-ttu-id="1acf1-306">Это требование для отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="1acf1-306">This is a requirement for app submission.</span></span> <span data-ttu-id="1acf1-307">Дополнительные сведения см. в [модуле задач Teams SDK.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="1acf1-307">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="1acf1-308">Если вы хотите, чтобы ваше приложение поддержало анонимных пользователей, то при первоначальном запросе необходимо использовать метаданные запроса в объекте, а не `from.id` `from` `from.aadObjectId` метаданные запроса.</span><span class="sxs-lookup"><span data-stu-id="1acf1-308">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="1acf1-309">`from.id` является ИД пользователя и `from.aadObjectId` является ИД Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="1acf1-309">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="1acf1-310">Дополнительные сведения см. в [таблицах](../task-modules-and-cards/task-modules/task-modules-tabs.md) с использованием модулей задач и созданием и [отправкой модуля задач.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="1acf1-310">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="share-to-stage"></a><span data-ttu-id="1acf1-311">Share to stage</span><span class="sxs-lookup"><span data-stu-id="1acf1-311">Share to stage</span></span> 

> [!NOTE]
> * <span data-ttu-id="1acf1-312">В настоящее время эта возможность доступна только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="1acf1-312">This capability is currently available in developer preview only.</span></span>
> * <span data-ttu-id="1acf1-313">Чтобы использовать эту функцию, приложение должно поддерживать боковойпанель на собрании.</span><span class="sxs-lookup"><span data-stu-id="1acf1-313">To use this feature, the app must support an in-meeting sidepanel.</span></span>


<span data-ttu-id="1acf1-314">Эта возможность дает разработчикам возможность делиться приложением на стадии собрания.</span><span class="sxs-lookup"><span data-stu-id="1acf1-314">This capability gives developers the ability to share an app to the meeting stage.</span></span> <span data-ttu-id="1acf1-315">Включив совместное использование на этапе собрания, участники собраний могут сотрудничать в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="1acf1-315">By enabling share to the meeting stage, meeting participants can collaborate in real-time.</span></span> 

<span data-ttu-id="1acf1-316">Необходимый контекст находится `meetingStage` в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="1acf1-316">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="1acf1-317">Обязательным условием для этого является `meetingSidePanel` контекст.</span><span class="sxs-lookup"><span data-stu-id="1acf1-317">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="1acf1-318">Это позволяет включить **кнопку Share** в боковомпанеэле, как обезвожив на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="1acf1-318">This enables the **Share** button in the sidepanel as depecited in the following image:</span></span>

  ![share_to_stage_during_meeting](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="1acf1-320">Изменение манифеста, необходимое для обеспечения этой возможности, является следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1acf1-320">The manifest change that is needed to enable this capability is as follows:</span></span> 

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```



### <a name="after-a-meeting"></a><span data-ttu-id="1acf1-321">После собрания</span><span class="sxs-lookup"><span data-stu-id="1acf1-321">After a meeting</span></span>

<span data-ttu-id="1acf1-322">Конфигурации после собрания и предварительного собрания эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="1acf1-322">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="code-sample"></a><span data-ttu-id="1acf1-323">Пример кода</span><span class="sxs-lookup"><span data-stu-id="1acf1-323">Code sample</span></span>

|<span data-ttu-id="1acf1-324">Пример имени</span><span class="sxs-lookup"><span data-stu-id="1acf1-324">Sample name</span></span> | <span data-ttu-id="1acf1-325">Описание</span><span class="sxs-lookup"><span data-stu-id="1acf1-325">Description</span></span> | <span data-ttu-id="1acf1-326">.NET</span><span class="sxs-lookup"><span data-stu-id="1acf1-326">.NET</span></span> | <span data-ttu-id="1acf1-327">Node.js</span><span class="sxs-lookup"><span data-stu-id="1acf1-327">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="1acf1-328">Разнонасть собраний</span><span class="sxs-lookup"><span data-stu-id="1acf1-328">Meetings extensibility</span></span> | <span data-ttu-id="1acf1-329">Пример extensibility microsoft Teams для передачи маркеров.</span><span class="sxs-lookup"><span data-stu-id="1acf1-329">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="1acf1-330">View</span><span class="sxs-lookup"><span data-stu-id="1acf1-330">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | |
| <span data-ttu-id="1acf1-331">Бот-бот для пузырьков контента для собраний</span><span class="sxs-lookup"><span data-stu-id="1acf1-331">Meeting content bubble bot</span></span> | <span data-ttu-id="1acf1-332">Пример extensibility microsoft Teams для взаимодействия с ботом пузырьков контента на собрании.</span><span class="sxs-lookup"><span data-stu-id="1acf1-332">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="1acf1-333">View</span><span class="sxs-lookup"><span data-stu-id="1acf1-333">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="1acf1-334">View</span><span class="sxs-lookup"><span data-stu-id="1acf1-334">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|

## <a name="see-also"></a><span data-ttu-id="1acf1-335">См. также</span><span class="sxs-lookup"><span data-stu-id="1acf1-335">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1acf1-336">Рекомендации по проектированию диалогов на собрании</span><span class="sxs-lookup"><span data-stu-id="1acf1-336">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
> [!div class="nextstepaction"]
> [<span data-ttu-id="1acf1-337">Поток проверки подлинности teams для вкладок</span><span class="sxs-lookup"><span data-stu-id="1acf1-337">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
