---
title: Создание приложений для собраний групп
author: laujan
description: создание приложений для собраний teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API роли участника собраний в приложениях teams
ms.openlocfilehash: 7f6d8fec735aa21033c6bcb2462c20458634f10a
ms.sourcegitcommit: 843da1730443ff8474a05295f60a6b376ed140da
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2021
ms.locfileid: "50073098"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="b4310-104">Создание приложений для собраний Teams</span><span class="sxs-lookup"><span data-stu-id="b4310-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="b4310-105">Предварительные условия и соображения</span><span class="sxs-lookup"><span data-stu-id="b4310-105">Prerequisites and considerations</span></span>

* <span data-ttu-id="b4310-106">Приложения на собраниях требуют базовых знаний о [разработке приложений Teams.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="b4310-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="b4310-107">Приложение на собрании может состоять [](../bots/what-are-bots.md)из вкладок, [](../tabs/what-are-tabs.md)ботов и функций расширений обмена сообщениями и требует обновления манифеста приложения [Teams,](#update-your-app-manifest) чтобы указать, что приложение доступно для собраний [](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="b4310-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

* <span data-ttu-id="b4310-108">Чтобы приложение функционировало в жизненном цикле собрания в качестве вкладки, оно должно поддерживать настраиваемые вкладки в области [groupchat](../resources/schema/manifest-schema.md#configurabletabs) (см. создание [вкладки группы).](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="b4310-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) (see how to [build a group tab](../build-your-first-app/build-channel-tab.md)).</span></span> <span data-ttu-id="b4310-109">Поддержка области позволяет вашему приложению в чатах до `groupchat` [и](teams-apps-in-meetings.md#pre-meeting-app-experience) [после](teams-apps-in-meetings.md#post-meeting-app-experience) собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-109">Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

* <span data-ttu-id="b4310-110">Для параметров URL-адреса API собраний может потребоваться и tenantId. Они доступны в составе `meetingId` `userId` клиентского SDK Teams и бота. [](/onedrive/find-your-office-365-tenant-id)</span><span class="sxs-lookup"><span data-stu-id="b4310-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="b4310-111">Кроме того, с помощью проверки подлинности tab SSO можно получить надежные сведения об ИД пользователя и [клиенте.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="b4310-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="b4310-112">Некоторые API собраний, например, требуют регистрации бота и `GetParticipant` [ИД](../build-your-first-app/build-bot.md) для создания маркеров auth.</span><span class="sxs-lookup"><span data-stu-id="b4310-112">Some meeting APIs, such as `GetParticipant`, require a [bot registration and ID](../build-your-first-app/build-bot.md) to generate auth tokens.</span></span>

* <span data-ttu-id="b4310-113">Для сценариев [](../tabs/design/tabs.md) до и после собрания необходимо соблюдать общие рекомендации по проектированию вкладок Teams.</span><span class="sxs-lookup"><span data-stu-id="b4310-113">You must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="b4310-114">Для работы во время собраний [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) обратитесь к [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) рекомендациям по проектированию вкладки "Собрание" и диалоговое окно собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-114">For experiences during meetings, refer to the [in-meeting tab](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) design guidelines.</span></span>

* <span data-ttu-id="b4310-115">Чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть в курсе событий собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-115">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="b4310-116">Эти события могут быть в диалоговом окну собрания (см. параметр завершения в) и других поверхностях в течение `bot Id` `Notification Signal API` жизненного цикла собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-116">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="b4310-117">Справочник по API приложений для собраний</span><span class="sxs-lookup"><span data-stu-id="b4310-117">Meeting apps API reference</span></span>

|<span data-ttu-id="b4310-118">API</span><span class="sxs-lookup"><span data-stu-id="b4310-118">API</span></span>|<span data-ttu-id="b4310-119">Описание</span><span class="sxs-lookup"><span data-stu-id="b4310-119">Description</span></span>|<span data-ttu-id="b4310-120">Запрос</span><span class="sxs-lookup"><span data-stu-id="b4310-120">Request</span></span>|<span data-ttu-id="b4310-121">Source</span><span class="sxs-lookup"><span data-stu-id="b4310-121">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="b4310-122">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="b4310-122">**GetUserContext**</span></span>| <span data-ttu-id="b4310-123">Получите контекстную информацию, чтобы отобразить релевантный контент на вкладке Teams.</span><span class="sxs-lookup"><span data-stu-id="b4310-123">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="b4310-124">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="b4310-124">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="b4310-125">SDK клиента Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b4310-125">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="b4310-126">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="b4310-126">**GetParticipant**</span></span>|<span data-ttu-id="b4310-127">Этот API позволяет боту получать сведения об участниках по их ид.</span><span class="sxs-lookup"><span data-stu-id="b4310-127">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="b4310-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="b4310-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="b4310-129">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="b4310-129">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="b4310-130">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="b4310-130">**NotificationSignal**</span></span> |<span data-ttu-id="b4310-131">Сигналы собрания будут доставляться с помощью следующего существующего API уведомлений о беседе (для чата пользователя-бота).</span><span class="sxs-lookup"><span data-stu-id="b4310-131">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="b4310-132">Этот API позволяет разработчикам сигнализировать о действии пользователя, чтобы показать диалоговое окно собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-132">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="b4310-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="b4310-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="b4310-134">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="b4310-134">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="b4310-135">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="b4310-135">GetUserContext</span></span>

<span data-ttu-id="b4310-136">Обратитесь к нашему контексту ["Получить" в документации](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) по вкладке Teams, чтобы получить инструкции по идентификации получения контекстных сведений для содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="b4310-136">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="b4310-137">В рамках возможностей для собраний добавлено новое значение для полезной нагрузки ответа:</span><span class="sxs-lookup"><span data-stu-id="b4310-137">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="b4310-138">✔ **meetingId**: используется вкладками при запуске в контексте собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-138">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="b4310-139">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="b4310-139">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="b4310-140">Не кэшделайте роли участников кэшом, так как организатор собрания может изменить роль в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="b4310-140">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="b4310-141">В настоящее время Teams не поддерживает большие списки рассылки или размеры списков для API более чем 350 `GetParticipant` участников.</span><span class="sxs-lookup"><span data-stu-id="b4310-141">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="b4310-142">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="b4310-142">Query parameters</span></span>

|<span data-ttu-id="b4310-143">Значение</span><span class="sxs-lookup"><span data-stu-id="b4310-143">Value</span></span>|<span data-ttu-id="b4310-144">Тип</span><span class="sxs-lookup"><span data-stu-id="b4310-144">Type</span></span>|<span data-ttu-id="b4310-145">Обязательный</span><span class="sxs-lookup"><span data-stu-id="b4310-145">Required</span></span>|<span data-ttu-id="b4310-146">Описание</span><span class="sxs-lookup"><span data-stu-id="b4310-146">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="b4310-147">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="b4310-147">**meetingId**</span></span>| <span data-ttu-id="b4310-148">string</span><span class="sxs-lookup"><span data-stu-id="b4310-148">string</span></span> | <span data-ttu-id="b4310-149">Да</span><span class="sxs-lookup"><span data-stu-id="b4310-149">Yes</span></span> | <span data-ttu-id="b4310-150">Идентификатор собрания доступен через Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="b4310-150">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="b4310-151">**participantId**</span><span class="sxs-lookup"><span data-stu-id="b4310-151">**participantId**</span></span>| <span data-ttu-id="b4310-152">string</span><span class="sxs-lookup"><span data-stu-id="b4310-152">string</span></span> | <span data-ttu-id="b4310-153">Да</span><span class="sxs-lookup"><span data-stu-id="b4310-153">Yes</span></span> | <span data-ttu-id="b4310-154">ParticipantId — это ИД пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4310-154">The participantId is the user ID.</span></span> <span data-ttu-id="b4310-155">Он доступен в SSO tab, Bot Invoke и клиентском SDK Teams.</span><span class="sxs-lookup"><span data-stu-id="b4310-155">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="b4310-156">Настоятельно рекомендуется получить participantId из SSO tab.</span><span class="sxs-lookup"><span data-stu-id="b4310-156">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="b4310-157">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="b4310-157">**tenantId**</span></span>| <span data-ttu-id="b4310-158">string</span><span class="sxs-lookup"><span data-stu-id="b4310-158">string</span></span> | <span data-ttu-id="b4310-159">Да</span><span class="sxs-lookup"><span data-stu-id="b4310-159">Yes</span></span> | <span data-ttu-id="b4310-160">Для пользователей клиента требуется tenantId.</span><span class="sxs-lookup"><span data-stu-id="b4310-160">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="b4310-161">Он доступен в SSO tab, Bot Invoke и клиентском SDK Teams.</span><span class="sxs-lookup"><span data-stu-id="b4310-161">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="b4310-162">Настоятельно рекомендуется получить tenantId из SSO tab.</span><span class="sxs-lookup"><span data-stu-id="b4310-162">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="b4310-163">Пример</span><span class="sxs-lookup"><span data-stu-id="b4310-163">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b4310-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b4310-164">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="b4310-165">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b4310-165">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="b4310-166">JSON</span><span class="sxs-lookup"><span data-stu-id="b4310-166">JSON</span></span>](#tab/json)

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="b4310-167">Тело ответа:</span><span class="sxs-lookup"><span data-stu-id="b4310-167">The response body is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="b4310-168">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="b4310-168">Response codes</span></span>

* <span data-ttu-id="b4310-169">**403:** приложению запрещено получать сведения об участниках.</span><span class="sxs-lookup"><span data-stu-id="b4310-169">**403**: The app is not allowed to get participant information.</span></span>  <span data-ttu-id="b4310-170">Это наиболее распространенный ответ об ошибке, который запускается, если приложение не установлено на собрании.</span><span class="sxs-lookup"><span data-stu-id="b4310-170">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="b4310-171">Например, если приложение отключено администратором клиента или заблокировано во время прямой миграции сайта.</span><span class="sxs-lookup"><span data-stu-id="b4310-171">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>
* <span data-ttu-id="b4310-172">**200**: сведения об участниках успешно извлечены.</span><span class="sxs-lookup"><span data-stu-id="b4310-172">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="b4310-173">**401**: недопустимый маркер.</span><span class="sxs-lookup"><span data-stu-id="b4310-173">**401**: Invalid token.</span></span>
* <span data-ttu-id="b4310-174">**404**: не удается найти участника.</span><span class="sxs-lookup"><span data-stu-id="b4310-174">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="b4310-175">**500:** срок действия собрания истек (более 60 дней с момента окончания собрания) или у участника нет разрешений на основе их роли.</span><span class="sxs-lookup"><span data-stu-id="b4310-175">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="b4310-176">**Ожидается в ближайшее время**</span><span class="sxs-lookup"><span data-stu-id="b4310-176">**Coming Soon**</span></span>

* <span data-ttu-id="b4310-177">**404:** истек срок действия собрания или не удается найти участника.</span><span class="sxs-lookup"><span data-stu-id="b4310-177">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="b4310-178">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="b4310-178">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="b4310-179">При вызове диалоговое окно собрания то же содержимое также будет представлено в качестве сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="b4310-179">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="b4310-180">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="b4310-180">Query parameters</span></span>

|<span data-ttu-id="b4310-181">Значение</span><span class="sxs-lookup"><span data-stu-id="b4310-181">Value</span></span>|<span data-ttu-id="b4310-182">Тип</span><span class="sxs-lookup"><span data-stu-id="b4310-182">Type</span></span>|<span data-ttu-id="b4310-183">Обязательный</span><span class="sxs-lookup"><span data-stu-id="b4310-183">Required</span></span>|<span data-ttu-id="b4310-184">Описание</span><span class="sxs-lookup"><span data-stu-id="b4310-184">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="b4310-185">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="b4310-185">**conversationId**</span></span>| <span data-ttu-id="b4310-186">string</span><span class="sxs-lookup"><span data-stu-id="b4310-186">string</span></span> | <span data-ttu-id="b4310-187">Да</span><span class="sxs-lookup"><span data-stu-id="b4310-187">Yes</span></span> | <span data-ttu-id="b4310-188">Идентификатор беседы доступен при вызове бота</span><span class="sxs-lookup"><span data-stu-id="b4310-188">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="b4310-189">Пример</span><span class="sxs-lookup"><span data-stu-id="b4310-189">Example</span></span>

> [!NOTE]
>
<span data-ttu-id="b4310-190">Параметр `completionBotId` параметра является `externalResourceUrl` необязательным в запрашиваемом примере полезной нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b4310-190">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="b4310-191">`Bot ID` объявляется в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="b4310-191">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="b4310-192">Параметры ширины и высоты externalResourceUrl должны быть в пикселях.</span><span class="sxs-lookup"><span data-stu-id="b4310-192">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="b4310-193">Чтобы [убедиться,](design/designing-apps-in-meetings.md) что размеры находятся в пределах допустимого, обратитесь к рекомендациям по проектированию.</span><span class="sxs-lookup"><span data-stu-id="b4310-193">Refer to the [design guidelines](design/designing-apps-in-meetings.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="b4310-194">URL-адрес — это страница, загруженная в диалоговом оке `<iframe>` собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-194">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="b4310-195">Домен должен быть в массиве приложения `validDomains` в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="b4310-195">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b4310-196">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b4310-196">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="b4310-197">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b4310-197">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="b4310-198">JSON</span><span class="sxs-lookup"><span data-stu-id="b4310-198">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="b4310-199">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="b4310-199">Response Codes</span></span>

* <span data-ttu-id="b4310-200">**201**: успешно отправлена активность с сигналом</span><span class="sxs-lookup"><span data-stu-id="b4310-200">**201**: activity with signal is successfully sent</span></span>  
* <span data-ttu-id="b4310-201">**401**: недопустимый маркер</span><span class="sxs-lookup"><span data-stu-id="b4310-201">**401**: invalid token</span></span>  
* <span data-ttu-id="b4310-202">**201**: успешно отправлено действие с сигналом.</span><span class="sxs-lookup"><span data-stu-id="b4310-202">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="b4310-203">**401**: недопустимый маркер.</span><span class="sxs-lookup"><span data-stu-id="b4310-203">**401**: Invalid token.</span></span>
* <span data-ttu-id="b4310-204">**403:** приложению не удается отправить сигнал.</span><span class="sxs-lookup"><span data-stu-id="b4310-204">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="b4310-205">Это может произойти из-за различных причин, таких как отключение приложения администратором клиента, блокировка приложения во время миграции на прямом сайте и так далее.</span><span class="sxs-lookup"><span data-stu-id="b4310-205">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="b4310-206">В этом случае полезное сообщение содержит подробное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="b4310-206">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="b4310-207">**404:** чат собрания не существует.</span><span class="sxs-lookup"><span data-stu-id="b4310-207">**404**: Meeting chat doesn't exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="b4310-208">Включить приложение для собраний Teams</span><span class="sxs-lookup"><span data-stu-id="b4310-208">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="b4310-209">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="b4310-209">Update your app manifest</span></span>

<span data-ttu-id="b4310-210">Возможности приложения для собраний объявляются в манифесте приложения с помощью настраиваемых областейtabs  ->   и **массивов контекста.**</span><span class="sxs-lookup"><span data-stu-id="b4310-210">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="b4310-211">*Область* определяет, кому и *где будет* доступно ваше приложение, а также контекст.</span><span class="sxs-lookup"><span data-stu-id="b4310-211">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="b4310-212">Используйте Developer Preview [манифеста,](../resources/schema/manifest-schema-dev-preview.md) чтобы попробовать это в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="b4310-212">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="b4310-213">Свойство Context</span><span class="sxs-lookup"><span data-stu-id="b4310-213">Context property</span></span>

<span data-ttu-id="b4310-214">Вкладка и свойства работают согласованно, чтобы вы могли определить, где будет отображаться `context` `scopes` ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="b4310-214">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="b4310-215">Вкладки в области `team` или области могут иметь несколько `groupchat` контекстов.</span><span class="sxs-lookup"><span data-stu-id="b4310-215">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="b4310-216">Возможные значения для свойства контекста:</span><span class="sxs-lookup"><span data-stu-id="b4310-216">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="b4310-217">**channelTab**: вкладка в заголке канала команды.</span><span class="sxs-lookup"><span data-stu-id="b4310-217">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="b4310-218">**privateChatTab**: вкладка в заголке группового чата между набором пользователей, не в контексте команды или собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-218">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="b4310-219">**meetingChatTab**: вкладка в заголке группового чата между набором пользователей в контексте запланированного собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-219">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="b4310-220">**meetingDetailsTab**: вкладка в заголовке представления сведений о собрании календаря.</span><span class="sxs-lookup"><span data-stu-id="b4310-220">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="b4310-221">**meetingSidePanel**: панель собрания, открытая через единую панель (u-bar).</span><span class="sxs-lookup"><span data-stu-id="b4310-221">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="b4310-222">Свойство "Context" в настоящее время не поддерживается и, следовательно, игнорируется на мобильных клиентах</span><span class="sxs-lookup"><span data-stu-id="b4310-222">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="b4310-223">Настройка приложения для сценариев собраний</span><span class="sxs-lookup"><span data-stu-id="b4310-223">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="b4310-224">Чтобы приложение было видимым в коллекции вкладок, оно должно поддерживать настраиваемые вкладки и область **группового чата.** </span><span class="sxs-lookup"><span data-stu-id="b4310-224">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="b4310-225">Мобильные клиенты поддерживают вкладки только на поверхностях до и после собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-225">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="b4310-226">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span><span class="sxs-lookup"><span data-stu-id="b4310-226">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="b4310-227">Следуйте [указаниям для вкладок на мобильных](../tabs/design/tabs-mobile.md) устройствах при создании вкладок для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b4310-227">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="b4310-228">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="b4310-228">Before a meeting</span></span>

<span data-ttu-id="b4310-229">Пользователи с ролями организатора и/или выдавщика добавляют вкладки  к собранию с помощью кнопки плюса ➕ на страницах сведений о **собрании** и чате.</span><span class="sxs-lookup"><span data-stu-id="b4310-229">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="b4310-230">Расширения сообщений добавляются в меню эллипса или переполнения &#x25CF;&#x25CF;&#x25CF; под областью составить сообщение в чате.</span><span class="sxs-lookup"><span data-stu-id="b4310-230">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="b4310-231">Боты добавляются в чат собрания с помощью клавиши **@** "" и выбора **get bots.**</span><span class="sxs-lookup"><span data-stu-id="b4310-231">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="b4310-232">✔ удостоверение пользователя *должно* быть подтверждено с помощью [SSO вкладок.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="b4310-232">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="b4310-233">После этой проверки подлинности приложение может получить роль пользователя с помощью API GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="b4310-233">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="b4310-234">✔ зависимости от роли пользователя, приложение теперь сможет представлять специальные возможности.</span><span class="sxs-lookup"><span data-stu-id="b4310-234">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="b4310-235">Например, приложение для опроса может разрешить создание опроса только организаторам и организаторам.</span><span class="sxs-lookup"><span data-stu-id="b4310-235">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="b4310-236">**ПРИМЕЧАНИЕ.** Назначения ролей можно изменить во время собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-236">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="b4310-237">*См.* [роли в собрании Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="b4310-237">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="b4310-238">Во время собрания</span><span class="sxs-lookup"><span data-stu-id="b4310-238">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="b4310-239">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="b4310-239">**sidePanel**</span></span>

<span data-ttu-id="b4310-240">✔ в манифесте приложения добавьте **sidePanel** в массив **контекста,** как описано выше.</span><span class="sxs-lookup"><span data-stu-id="b4310-240">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="b4310-241">✔ собрания, как и во всех сценариях, приложение будет отрисовыно на вкладке собрания шириной 320px.</span><span class="sxs-lookup"><span data-stu-id="b4310-241">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="b4310-242">Для этого необходимо оптимизировать вкладку.</span><span class="sxs-lookup"><span data-stu-id="b4310-242">Your tab must be optimized for this.</span></span> <span data-ttu-id="b4310-243">*См.* интерфейс [FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="b4310-243">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="b4310-244">✔Относите запросы в [SDK Teams](../tabs/how-to/access-teams-context.md#user-context) для использования API **userContext.**</span><span class="sxs-lookup"><span data-stu-id="b4310-244">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="b4310-245">✔ для вкладок обратитесь к потоку проверки [подлинности Teams.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="b4310-245">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="b4310-246">Поток проверки подлинности для вкладок очень похож на поток проверки подлинности для веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="b4310-246">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="b4310-247">Таким образом, вкладки могут использовать OAuth 2.0 напрямую.</span><span class="sxs-lookup"><span data-stu-id="b4310-247">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="b4310-248">*См. также,* платформа удостоверений Майкрософт и поток кода авторизации [OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)</span><span class="sxs-lookup"><span data-stu-id="b4310-248">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="b4310-249">✔ сообщение должно работать ожидаемым, когда пользователь находится в представлении собрания и должен иметь возможность опубликовать карточки расширения сообщения.</span><span class="sxs-lookup"><span data-stu-id="b4310-249">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="b4310-250">✔ AppName in-meeting — в выдавке tooltip должно быть занося имя приложения в панели U-bar собрания.</span><span class="sxs-lookup"><span data-stu-id="b4310-250">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="b4310-251">**Диалоговое окно собрания**</span><span class="sxs-lookup"><span data-stu-id="b4310-251">**In-meeting dialog**</span></span>

<span data-ttu-id="b4310-252">✔ Вы должны соблюдать рекомендации по проектированию [диалогового окна собрания.](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="b4310-252">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="b4310-253">✔ для вкладок обратитесь к потоку проверки [подлинности Teams.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="b4310-253">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="b4310-254">✔ использовать [API NotificationSignal,](create-apps-for-teams-meetings.md#notificationsignal-api) чтобы сигнализировать о том, что необходимо инициализировать уведомление о пузырьковом сигнале.</span><span class="sxs-lookup"><span data-stu-id="b4310-254">✔ Use the [NotificationSignal API](create-apps-for-teams-meetings.md#notificationsignal-api) to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="b4310-255">✔ как часть полезной нагрузки запроса на уведомление, включайте URL-адрес, где находится демонстрация содержимого.</span><span class="sxs-lookup"><span data-stu-id="b4310-255">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="b4310-256">✔ собрания не должен использовать модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="b4310-256">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="b4310-257">Эти уведомления имеют постоянный характер.</span><span class="sxs-lookup"><span data-stu-id="b4310-257">These notifications are persistent in nature.</span></span> <span data-ttu-id="b4310-258">Необходимо вызвать функцию [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического скрытие после того, как пользователь делает действие в веб-представлении.</span><span class="sxs-lookup"><span data-stu-id="b4310-258">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="b4310-259">Это требование для отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="b4310-259">This is a requirement for app submission.</span></span> <span data-ttu-id="b4310-260">*См. также*, [Teams SDK: модуль задачи](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="b4310-260">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="b4310-261">Если вы хотите, чтобы ваше приложение поддерживает анонимных пользователей, то для исходного запроса на вызов необходимо использовать метаданные запроса (ИД пользователя) в объекте, а не метаданные `from.id` `from` `from.aadObjectId` запроса (Azure Active Directory ID пользователя).</span><span class="sxs-lookup"><span data-stu-id="b4310-261">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="b4310-262">*См.* ["Использование модулей задач на вкладке"](../task-modules-and-cards/task-modules/task-modules-tabs.md) и ["Создание и отправка модуля задачи".](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="b4310-262">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="b4310-263">После собрания</span><span class="sxs-lookup"><span data-stu-id="b4310-263">After a meeting</span></span>

<span data-ttu-id="b4310-264">Конфигурации после собрания и до собрания эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="b4310-264">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="b4310-265">Пример приложения для собраний</span><span class="sxs-lookup"><span data-stu-id="b4310-265">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="b4310-266">Приложение генератора маркеров собраний</span><span class="sxs-lookup"><span data-stu-id="b4310-266">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
