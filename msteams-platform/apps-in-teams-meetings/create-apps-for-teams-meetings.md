---
title: Создание приложений для собраний групп
author: laujan
description: создание приложений для собраний групп
ms.topic: conceptual
ms.author: lajanuar
keywords: teams apps meetings user participant role api
ms.openlocfilehash: bd0f53ae34a23bdbbdc2e6f3992c7dd0836e9f28
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449495"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="80765-104">Создание приложений для собраний Teams</span><span class="sxs-lookup"><span data-stu-id="80765-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="80765-105">Предпосылки и соображения</span><span class="sxs-lookup"><span data-stu-id="80765-105">Prerequisites and considerations</span></span>

* <span data-ttu-id="80765-106">Приложения на собраниях требуют некоторых базовых знаний о разработке [приложений Teams.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="80765-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="80765-107">Приложение на собрании может состоять [](../bots/what-are-bots.md)из функций [](../messaging-extensions/what-are-messaging-extensions.md) вкладок, [](../tabs/what-are-tabs.md)ботов и расширений обмена сообщениями и потребует обновлений манифеста приложения [Teams,](#update-your-app-manifest) чтобы указать, что приложение доступно для собраний.</span><span class="sxs-lookup"><span data-stu-id="80765-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

* <span data-ttu-id="80765-108">Чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки, оно должно поддерживать настраиваемые вкладки в области [группового](../resources/schema/manifest-schema.md#configurabletabs) чата (см. в нем, как создать [вкладку группы).](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="80765-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) (see how to [build a group tab](../build-your-first-app/build-channel-tab.md)).</span></span> <span data-ttu-id="80765-109">Поддержка области `groupchat` позволит вашему [](teams-apps-in-meetings.md#pre-meeting-app-experience) приложению использовать чаты перед собранием и [после](teams-apps-in-meetings.md#post-meeting-app-experience) собрания.</span><span class="sxs-lookup"><span data-stu-id="80765-109">Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

* <span data-ttu-id="80765-110">Для параметров URL-адресов API собраний может потребоваться , и tenantId Они доступны в рамках `meetingId` `userId` SDK клиента Teams и бота. [](/onedrive/find-your-office-365-tenant-id)</span><span class="sxs-lookup"><span data-stu-id="80765-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="80765-111">Кроме того, с помощью проверки подлинности [Tab SSO](../tabs/how-to/authentication/auth-aad-sso.md)можно получить достоверную информацию для идентификации пользователя и клиента.</span><span class="sxs-lookup"><span data-stu-id="80765-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="80765-112">Некоторые API собраний, например, требуют регистрации бота и `GetParticipant` [ID](../build-your-first-app/build-bot.md) для создания маркеров auth.</span><span class="sxs-lookup"><span data-stu-id="80765-112">Some meeting APIs, such as `GetParticipant`, require a [bot registration and ID](../build-your-first-app/build-bot.md) to generate auth tokens.</span></span>

* <span data-ttu-id="80765-113">Необходимо придерживаться общих правил разработки вкладок [Teams](../tabs/design/tabs.md) для сценариев до и после собрания.</span><span class="sxs-lookup"><span data-stu-id="80765-113">You must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="80765-114">Для работы во время собраний [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) обратитесь к [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) вкладке на собрании и рекомендациям по проектированию диалогов на собрании.</span><span class="sxs-lookup"><span data-stu-id="80765-114">For experiences during meetings, refer to the [in-meeting tab](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) design guidelines.</span></span>

* <span data-ttu-id="80765-115">Чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть обновлено в зависимости от событий на собрании.</span><span class="sxs-lookup"><span data-stu-id="80765-115">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="80765-116">Эти события могут быть в диалоговом окну (обратитесь к параметру завершения) и другим поверхностям на `bot Id` `Notification Signal API` жизненном цикле собрания.</span><span class="sxs-lookup"><span data-stu-id="80765-116">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="80765-117">Ссылка на API приложений для собраний</span><span class="sxs-lookup"><span data-stu-id="80765-117">Meeting apps API reference</span></span>

|<span data-ttu-id="80765-118">API</span><span class="sxs-lookup"><span data-stu-id="80765-118">API</span></span>|<span data-ttu-id="80765-119">Описание</span><span class="sxs-lookup"><span data-stu-id="80765-119">Description</span></span>|<span data-ttu-id="80765-120">Запрос</span><span class="sxs-lookup"><span data-stu-id="80765-120">Request</span></span>|<span data-ttu-id="80765-121">Источник</span><span class="sxs-lookup"><span data-stu-id="80765-121">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="80765-122">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="80765-122">**GetUserContext**</span></span>| <span data-ttu-id="80765-123">Получите контекстную информацию для отображения соответствующего контента на вкладке Teams.</span><span class="sxs-lookup"><span data-stu-id="80765-123">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="80765-124">_**microsoftTeams.getContext() => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="80765-124">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="80765-125">Клиент Microsoft Teams SDK</span><span class="sxs-lookup"><span data-stu-id="80765-125">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="80765-126">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="80765-126">**GetParticipant**</span></span>|<span data-ttu-id="80765-127">Этот API позволяет боту получать сведения о участниках, встречая id и id участника.</span><span class="sxs-lookup"><span data-stu-id="80765-127">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="80765-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="80765-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="80765-129">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="80765-129">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="80765-130">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="80765-130">**NotificationSignal**</span></span> |<span data-ttu-id="80765-131">Сигналы собрания будут доставляться с помощью следующего существующего API уведомлений о беседе (для чата пользователя-бота).</span><span class="sxs-lookup"><span data-stu-id="80765-131">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="80765-132">Этот API позволяет разработчикам сигнализировать на основе действий конечных пользователей, чтобы показать в случае встречи диалоговое пузырек.</span><span class="sxs-lookup"><span data-stu-id="80765-132">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="80765-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="80765-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="80765-134">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="80765-134">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="80765-135">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="80765-135">GetUserContext</span></span>

<span data-ttu-id="80765-136">Обратитесь к нашему [контексту Get for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and retrieving contextual information for your tab content.</span><span class="sxs-lookup"><span data-stu-id="80765-136">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="80765-137">В рамках расстановки собраний добавлено новое значение для полезной нагрузки ответа:</span><span class="sxs-lookup"><span data-stu-id="80765-137">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="80765-138">✔ **meetingId**: используется вкладками при работе в контексте собрания.</span><span class="sxs-lookup"><span data-stu-id="80765-138">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="80765-139">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="80765-139">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="80765-140">Не кэшить роли участников, так как организатор собрания может изменить роль в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="80765-140">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="80765-141">В настоящее время teams не поддерживают большие списки рассылки или размер реестра, вметив более 350 `GetParticipant` участников для API.</span><span class="sxs-lookup"><span data-stu-id="80765-141">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="80765-142">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="80765-142">Query parameters</span></span>

|<span data-ttu-id="80765-143">Значение</span><span class="sxs-lookup"><span data-stu-id="80765-143">Value</span></span>|<span data-ttu-id="80765-144">Тип</span><span class="sxs-lookup"><span data-stu-id="80765-144">Type</span></span>|<span data-ttu-id="80765-145">Обязательный</span><span class="sxs-lookup"><span data-stu-id="80765-145">Required</span></span>|<span data-ttu-id="80765-146">Описание</span><span class="sxs-lookup"><span data-stu-id="80765-146">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="80765-147">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="80765-147">**meetingId**</span></span>| <span data-ttu-id="80765-148">string</span><span class="sxs-lookup"><span data-stu-id="80765-148">string</span></span> | <span data-ttu-id="80765-149">Да</span><span class="sxs-lookup"><span data-stu-id="80765-149">Yes</span></span> | <span data-ttu-id="80765-150">Идентификатор собрания доступен через Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="80765-150">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="80765-151">**participantId**</span><span class="sxs-lookup"><span data-stu-id="80765-151">**participantId**</span></span>| <span data-ttu-id="80765-152">string</span><span class="sxs-lookup"><span data-stu-id="80765-152">string</span></span> | <span data-ttu-id="80765-153">Да</span><span class="sxs-lookup"><span data-stu-id="80765-153">Yes</span></span> | <span data-ttu-id="80765-154">УчастникId — это пользовательский ID.</span><span class="sxs-lookup"><span data-stu-id="80765-154">The participantId is the user ID.</span></span> <span data-ttu-id="80765-155">Он доступен в SSO tab, Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="80765-155">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="80765-156">Настоятельно рекомендуется получить участникаId из SSO tab.</span><span class="sxs-lookup"><span data-stu-id="80765-156">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="80765-157">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="80765-157">**tenantId**</span></span>| <span data-ttu-id="80765-158">string</span><span class="sxs-lookup"><span data-stu-id="80765-158">string</span></span> | <span data-ttu-id="80765-159">Да</span><span class="sxs-lookup"><span data-stu-id="80765-159">Yes</span></span> | <span data-ttu-id="80765-160">TenantId является обязательной для пользователей-клиентов.</span><span class="sxs-lookup"><span data-stu-id="80765-160">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="80765-161">Он доступен в SSO tab, Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="80765-161">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="80765-162">Настоятельно рекомендуется получить tenantId из SSO tab.</span><span class="sxs-lookup"><span data-stu-id="80765-162">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="80765-163">Пример</span><span class="sxs-lookup"><span data-stu-id="80765-163">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="80765-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="80765-164">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="80765-165">JavaScript</span><span class="sxs-lookup"><span data-stu-id="80765-165">JavaScript</span></span>](#tab/javascript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="80765-166">JSON</span><span class="sxs-lookup"><span data-stu-id="80765-166">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="80765-167">Тело ответа:</span><span class="sxs-lookup"><span data-stu-id="80765-167">The response body is:</span></span>

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

* * *

#### <a name="response-codes"></a><span data-ttu-id="80765-168">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="80765-168">Response codes</span></span>

* <span data-ttu-id="80765-169">**403.** Приложение не может получать сведения о участниках.</span><span class="sxs-lookup"><span data-stu-id="80765-169">**403**: The app is not allowed to get participant information.</span></span> <span data-ttu-id="80765-170">Это наиболее распространенный ответ на ошибки, который запускается, если приложение не установлено на собрании.</span><span class="sxs-lookup"><span data-stu-id="80765-170">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="80765-171">Например, если приложение отключено администратором клиента или заблокировано во время смягчения последствий для жизни.</span><span class="sxs-lookup"><span data-stu-id="80765-171">For example, if the app is disabled by tenant admin or blocked during livesite mitigation.</span></span>
* <span data-ttu-id="80765-172">**200.** Успешно извлекаемая информация участника.</span><span class="sxs-lookup"><span data-stu-id="80765-172">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="80765-173">**401.** Недействительный маркер.</span><span class="sxs-lookup"><span data-stu-id="80765-173">**401**: Invalid token.</span></span>
* <span data-ttu-id="80765-174">**404.** Участник не может быть найден.</span><span class="sxs-lookup"><span data-stu-id="80765-174">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="80765-175">**500.** Срок действия собрания истек (более 60 дней с момента окончания собрания), либо у участника нет разрешений, основанных на их роли.</span><span class="sxs-lookup"><span data-stu-id="80765-175">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="80765-176">**Ожидается в ближайшее время**</span><span class="sxs-lookup"><span data-stu-id="80765-176">**Coming Soon**</span></span>

* <span data-ttu-id="80765-177">**404.** Собрание истеко или участник не может быть найден.</span><span class="sxs-lookup"><span data-stu-id="80765-177">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="80765-178">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="80765-178">NotificationSignal API</span></span>

<span data-ttu-id="80765-179">Все пользователи на собрании получают уведомления, отправленные через API NotificationSignal.</span><span class="sxs-lookup"><span data-stu-id="80765-179">All users in a meeting receive the notifications sent through the NotificationSignal API.</span></span>

> [!NOTE]
> <span data-ttu-id="80765-180">В настоящее время отправка целевых уведомлений не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="80765-180">Currently, sending targetted notifications is not supported.</span></span>
> <span data-ttu-id="80765-181">Когда вызывается диалоговое окно в собрании, то тот же контент также будет представлен в качестве сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="80765-181">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="80765-182">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="80765-182">Query parameters</span></span>

|<span data-ttu-id="80765-183">Значение</span><span class="sxs-lookup"><span data-stu-id="80765-183">Value</span></span>|<span data-ttu-id="80765-184">Тип</span><span class="sxs-lookup"><span data-stu-id="80765-184">Type</span></span>|<span data-ttu-id="80765-185">Обязательный</span><span class="sxs-lookup"><span data-stu-id="80765-185">Required</span></span>|<span data-ttu-id="80765-186">Описание</span><span class="sxs-lookup"><span data-stu-id="80765-186">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="80765-187">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="80765-187">**conversationId**</span></span>| <span data-ttu-id="80765-188">string</span><span class="sxs-lookup"><span data-stu-id="80765-188">string</span></span> | <span data-ttu-id="80765-189">Да</span><span class="sxs-lookup"><span data-stu-id="80765-189">Yes</span></span> | <span data-ttu-id="80765-190">Идентификатор беседы доступен в рамках вызова бота</span><span class="sxs-lookup"><span data-stu-id="80765-190">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="80765-191">Пример</span><span class="sxs-lookup"><span data-stu-id="80765-191">Example</span></span>

<span data-ttu-id="80765-192">Объявляется `Bot ID` в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="80765-192">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span> <span data-ttu-id="80765-193">В следующем примере параметр необязательный в `completionBotId` `externalResourceUrl` запрашиваемой полезной нагрузке:</span><span class="sxs-lookup"><span data-stu-id="80765-193">In the following example, the `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload:</span></span>

> [!NOTE]
> * <span data-ttu-id="80765-194">Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях.</span><span class="sxs-lookup"><span data-stu-id="80765-194">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="80765-195">Чтобы размеры были в пределах допустимого, см. в [рекомендациях по проектированию.](design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="80765-195">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="80765-196">URL-адрес — это страница, загруженная в диалоговом окруже `<iframe>` на собрании.</span><span class="sxs-lookup"><span data-stu-id="80765-196">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="80765-197">Домен должен быть в массиве приложения в `validDomains` манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="80765-197">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="80765-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="80765-198">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="80765-199">JavaScript</span><span class="sxs-lookup"><span data-stu-id="80765-199">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="80765-200">JSON</span><span class="sxs-lookup"><span data-stu-id="80765-200">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="80765-201">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="80765-201">Response Codes</span></span>

* <span data-ttu-id="80765-202">**201.** Успешно отправляется действие с сигналом.</span><span class="sxs-lookup"><span data-stu-id="80765-202">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="80765-203">**401.** Недействительный маркер.</span><span class="sxs-lookup"><span data-stu-id="80765-203">**401**: Invalid token.</span></span>
* <span data-ttu-id="80765-204">**403.** Приложение не может отправить сигнал.</span><span class="sxs-lookup"><span data-stu-id="80765-204">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="80765-205">Это может произойти из-за различных причин, таких как отключение приложения администратором клиента, блокировка приложения во время переноса веб-сайта в прямом эфире и так далее.</span><span class="sxs-lookup"><span data-stu-id="80765-205">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="80765-206">В этом случае полезное сообщение содержит подробное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="80765-206">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="80765-207">**404.** Чат собраний не существует.</span><span class="sxs-lookup"><span data-stu-id="80765-207">**404**: Meeting chat does not exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="80765-208">Включить приложение для собраний Teams</span><span class="sxs-lookup"><span data-stu-id="80765-208">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="80765-209">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="80765-209">Update your app manifest</span></span>

<span data-ttu-id="80765-210">Возможности приложения собраний объявляются в манифесте приложения с помощью настраиваемых областей **и**  ->   массивов **контекста.**</span><span class="sxs-lookup"><span data-stu-id="80765-210">The meetings app capabilities are declared in your app manifest through the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="80765-211">*Область* определяет, кому и *в котором контекст* определяет, где будет доступно ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="80765-211">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="80765-212">Используйте [схему Developer Preview манифеста,](../resources/schema/manifest-schema-dev-preview.md) чтобы попробовать это в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="80765-212">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="80765-213">Свойство Context</span><span class="sxs-lookup"><span data-stu-id="80765-213">Context property</span></span>

<span data-ttu-id="80765-214">Вкладка и свойства работают в гармонии, чтобы определить, где нужно `context` `scopes` отображаться ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="80765-214">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="80765-215">Вкладки в области или области `team` `groupchat` могут иметь несколько контекстов.</span><span class="sxs-lookup"><span data-stu-id="80765-215">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="80765-216">Возможные значения для свойства контекста следующим образом:</span><span class="sxs-lookup"><span data-stu-id="80765-216">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="80765-217">**channelTab**: вкладка в загонах канала команды.</span><span class="sxs-lookup"><span data-stu-id="80765-217">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="80765-218">**privateChatTab**: вкладка в загона группового чата между набором пользователей, не в контексте группы или собрания.</span><span class="sxs-lookup"><span data-stu-id="80765-218">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="80765-219">**meetingChatTab**: вкладка в заглавной части группового чата между набором пользователей в контексте запланированного собрания.</span><span class="sxs-lookup"><span data-stu-id="80765-219">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="80765-220">**meetingDetailsTab**: вкладка в заглавной части представления сведений о собрании календаря.</span><span class="sxs-lookup"><span data-stu-id="80765-220">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="80765-221">**meetingSidePanel**: панель на собрании, открытая с помощью единой панели (u-bar).</span><span class="sxs-lookup"><span data-stu-id="80765-221">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="80765-222">Свойство "Context" в настоящее время не поддерживается и, таким образом, будет игнорироваться для мобильных клиентов</span><span class="sxs-lookup"><span data-stu-id="80765-222">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="80765-223">Настройка приложения для сценариев собраний</span><span class="sxs-lookup"><span data-stu-id="80765-223">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="80765-224">Чтобы приложение было видимым в галерее вкладок, оно должно поддерживать **настраиваемые** вкладки и область **группового чата.**</span><span class="sxs-lookup"><span data-stu-id="80765-224">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="80765-225">Мобильные клиенты поддерживают вкладки только в pre и post meeting Surfaces.</span><span class="sxs-lookup"><span data-stu-id="80765-225">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="80765-226">В ближайшее время будут доступны опытом в собрании (диалоговое окно и вкладка на собрании) на мобильном телефоне.</span><span class="sxs-lookup"><span data-stu-id="80765-226">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="80765-227">Следуйте [указаниям для вкладок на мобильных устройствах](../tabs/design/tabs-mobile.md) при создании вкладок для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="80765-227">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="80765-228">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="80765-228">Before a meeting</span></span>

<span data-ttu-id="80765-229">Пользователи с ролями организатора и/или презента добавляют вкладки на  собрание с помощью кнопки плюс ➕ на страницах чата собрания и сведений **о** собраниях.</span><span class="sxs-lookup"><span data-stu-id="80765-229">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="80765-230">Расширения обмена сообщениями добавляются в меню эллипсов и переполнений &#x25CF;&#x25CF;&#x25CF; под областью составить сообщение в чате.</span><span class="sxs-lookup"><span data-stu-id="80765-230">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="80765-231">Боты добавляются в чат собраний с помощью ключа **@** "" и выбора **ботов Get.**</span><span class="sxs-lookup"><span data-stu-id="80765-231">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="80765-232">✔ удостоверение пользователя *должно* быть подтверждено с помощью [SSO Tabs.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="80765-232">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="80765-233">После проверки подлинности приложение может получить роль пользователя с помощью API GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="80765-233">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="80765-234">✔ зависимости от роли пользователя приложение теперь будет иметь возможность представлять определенные функции.</span><span class="sxs-lookup"><span data-stu-id="80765-234">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="80765-235">Например, приложение для опроса может разрешить создавать новый опрос только организаторам и презентаторам.</span><span class="sxs-lookup"><span data-stu-id="80765-235">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="80765-236">**ПРИМЕЧАНИЕ.** Назначения ролей могут быть изменены во время собрания.</span><span class="sxs-lookup"><span data-stu-id="80765-236">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="80765-237">*См.* [роли в собрании Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="80765-237">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="80765-238">Во время собрания</span><span class="sxs-lookup"><span data-stu-id="80765-238">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="80765-239">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="80765-239">**sidePanel**</span></span>

<span data-ttu-id="80765-240">✔ В манифесте приложения добавьте **sidePanel** в массив **контекста,** как описано выше.</span><span class="sxs-lookup"><span data-stu-id="80765-240">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="80765-241">✔ на собрании, как и во всех сценариях, приложение будет отрисовка на вкладке в собрании шириной 320px.</span><span class="sxs-lookup"><span data-stu-id="80765-241">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="80765-242">Для этого необходимо оптимизировать вкладку.</span><span class="sxs-lookup"><span data-stu-id="80765-242">Your tab must be optimized for this.</span></span> <span data-ttu-id="80765-243">*См.* интерфейс [FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="80765-243">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="80765-244">✔Refer для команд [SDK,](../tabs/how-to/access-teams-context.md#user-context) чтобы использовать **API userContext** для маршрутных запросов соответственно.</span><span class="sxs-lookup"><span data-stu-id="80765-244">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="80765-245">✔ Обратитесь к потоку [проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="80765-245">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="80765-246">Поток проверки подлинности для вкладок очень похож на поток auth для веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="80765-246">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="80765-247">Таким образом, вкладки могут напрямую использовать OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="80765-247">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="80765-248">*См. также,* платформа удостоверений Майкрософт и поток кода авторизации [OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)</span><span class="sxs-lookup"><span data-stu-id="80765-248">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="80765-249">✔ расширение сообщения должно работать так, как ожидалось, когда пользователь находится в представлении на собрании и должен иметь возможность отправлять составить карточки расширения сообщений.</span><span class="sxs-lookup"><span data-stu-id="80765-249">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="80765-250">✔ AppName на собрании — Tooltip должен указать имя приложения на собрании U-bar.</span><span class="sxs-lookup"><span data-stu-id="80765-250">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="80765-251">**Диалоговое окно собрания**</span><span class="sxs-lookup"><span data-stu-id="80765-251">**In-meeting dialog**</span></span>

<span data-ttu-id="80765-252">✔ Необходимо придерживаться рекомендаций по проектированию диалогов на [собрании.](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="80765-252">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="80765-253">✔ Обратитесь к потоку [проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="80765-253">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="80765-254">✔ [API NotificationSignal](create-apps-for-teams-meetings.md#notificationsignal-api) для сигнала о том, что нужно запускать уведомление о пузыре.</span><span class="sxs-lookup"><span data-stu-id="80765-254">✔ Use the [NotificationSignal API](create-apps-for-teams-meetings.md#notificationsignal-api) to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="80765-255">✔ В качестве части полезной нагрузки запроса уведомлений включайте URL-адрес, на котором будет демонстрироваться содержимое.</span><span class="sxs-lookup"><span data-stu-id="80765-255">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="80765-256">✔ диалоговое окно на собрании не должно использовать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="80765-256">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="80765-257">Эти уведомления являются постоянными по своему характеру.</span><span class="sxs-lookup"><span data-stu-id="80765-257">These notifications are persistent in nature.</span></span> <span data-ttu-id="80765-258">После действия пользователя в веб-представлении необходимо вызвать функцию [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического увольнения.</span><span class="sxs-lookup"><span data-stu-id="80765-258">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="80765-259">Это требование для отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="80765-259">This is a requirement for app submission.</span></span> <span data-ttu-id="80765-260">*См. также*, [Teams SDK: модуль задач](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="80765-260">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="80765-261">Если вы хотите, чтобы приложение поддержало анонимных пользователей, ваша начальная нагрузка запроса на вызов должна опираться на метаданные запроса (ID пользователя), а не метаданные `from.id` `from` `from.aadObjectId` запроса (Azure Active Directory пользователя).</span><span class="sxs-lookup"><span data-stu-id="80765-261">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="80765-262">*См.* [в рубке](../task-modules-and-cards/task-modules/task-modules-tabs.md) Использование модулей задач и создание и [отправка модуля задач.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="80765-262">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="80765-263">После собрания</span><span class="sxs-lookup"><span data-stu-id="80765-263">After a meeting</span></span>

<span data-ttu-id="80765-264">Конфигурации после собрания и предварительного собрания эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="80765-264">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="80765-265">Пример приложения для собраний</span><span class="sxs-lookup"><span data-stu-id="80765-265">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="80765-266">Приложение генератора маркеров собраний</span><span class="sxs-lookup"><span data-stu-id="80765-266">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
