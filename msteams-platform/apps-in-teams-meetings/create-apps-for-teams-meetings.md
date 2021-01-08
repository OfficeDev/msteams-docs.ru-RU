---
title: Создание приложений для собраний групп
author: laujan
description: создание приложений для собраний teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API роли участника собраний в приложениях Teams
ms.openlocfilehash: e768c2dc6722d006c89927adfe60e03243a076d0
ms.sourcegitcommit: f0dfae429385ef02f61896ad49172c4803ef6622
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/31/2020
ms.locfileid: "49740873"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="6699f-104">Создание приложений для собраний Teams</span><span class="sxs-lookup"><span data-stu-id="6699f-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="6699f-105">Предварительные условия и вопросы</span><span class="sxs-lookup"><span data-stu-id="6699f-105">Prerequisites and considerations</span></span>

1. <span data-ttu-id="6699f-106">Приложения на собраниях требуют базовых знаний о [разработке приложений Teams.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="6699f-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="6699f-107">Приложение на собрании может состоять [](../bots/what-are-bots.md)из вкладок, [](../tabs/what-are-tabs.md)ботов и функций расширений обмена сообщениями и требует обновления манифеста приложения [Teams,](#update-your-app-manifest) чтобы указать, что приложение доступно для собраний [](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="6699f-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="6699f-108">Чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки, оно должно поддерживать настраиваемые вкладки в области [groupchat.](../resources/schema/manifest-schema.md#configurabletabs)</span><span class="sxs-lookup"><span data-stu-id="6699f-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="6699f-109">*См.* [расширение приложения Teams с помощью настраиваемой вкладки.](../tabs/how-to/add-tab.md) Поддержка области позволяет вашему приложению в чатах до `groupchat` [и](teams-apps-in-meetings.md#pre-meeting-app-experience) [после](teams-apps-in-meetings.md#post-meeting-app-experience) собрания.</span><span class="sxs-lookup"><span data-stu-id="6699f-109">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="6699f-110">Для параметров URL-адреса API собраний может потребоваться и tenantId. Они доступны в составе `meetingId` `userId` клиентского SDK Teams и бота. [](/onedrive/find-your-office-365-tenant-id)</span><span class="sxs-lookup"><span data-stu-id="6699f-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="6699f-111">Кроме того, с помощью проверки подлинности tab SSO можно получить надежные сведения об ИД пользователя и [клиенте.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="6699f-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="6699f-112">Некоторые API собраний, например, требуют регистрации бота и ИД `GetParticipant` [приложения-бота](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) для создания маркеров auth.</span><span class="sxs-lookup"><span data-stu-id="6699f-112">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="6699f-113">Как разработчик, вы должны соблюдать общие рекомендации по проектированию вкладок [Teams](../tabs/design/tabs.md) для [](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) сценариев до и после собрания, а также рекомендации по диалоговом оклу в собрании, срабатываем во время собрания Teams.</span><span class="sxs-lookup"><span data-stu-id="6699f-113">As a developer, you must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) for in-meeting dialog triggered during a Teams meeting.</span></span>

1. <span data-ttu-id="6699f-114">Обратите внимание, что чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть в курсе событий собрания.</span><span class="sxs-lookup"><span data-stu-id="6699f-114">Please note that in order for your app to be updated in real-time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="6699f-115">Эти события могут быть в диалоговом окну собрания (см. параметр завершения в) и других поверхностях в течение `bot Id` `Notification Signal API` жизненного цикла собрания.</span><span class="sxs-lookup"><span data-stu-id="6699f-115">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="6699f-116">Справочник по API приложений для собраний</span><span class="sxs-lookup"><span data-stu-id="6699f-116">Meeting apps API reference</span></span>

|<span data-ttu-id="6699f-117">API</span><span class="sxs-lookup"><span data-stu-id="6699f-117">API</span></span>|<span data-ttu-id="6699f-118">Описание</span><span class="sxs-lookup"><span data-stu-id="6699f-118">Description</span></span>|<span data-ttu-id="6699f-119">Запрос</span><span class="sxs-lookup"><span data-stu-id="6699f-119">Request</span></span>|<span data-ttu-id="6699f-120">Source</span><span class="sxs-lookup"><span data-stu-id="6699f-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="6699f-121">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="6699f-121">**GetUserContext**</span></span>| <span data-ttu-id="6699f-122">Получите контекстную информацию, чтобы отобразить релевантный контент на вкладке Teams.</span><span class="sxs-lookup"><span data-stu-id="6699f-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="6699f-123">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="6699f-123">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="6699f-124">SDK клиента Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6699f-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="6699f-125">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="6699f-125">**GetParticipant**</span></span>|<span data-ttu-id="6699f-126">Этот API позволяет боту получать сведения об участниках по их ид.</span><span class="sxs-lookup"><span data-stu-id="6699f-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="6699f-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="6699f-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="6699f-128">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="6699f-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="6699f-129">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="6699f-129">**NotificationSignal**</span></span> |<span data-ttu-id="6699f-130">Сигналы собрания будут доставляться с помощью следующего существующего API уведомлений о беседе (для чата пользователя-бота).</span><span class="sxs-lookup"><span data-stu-id="6699f-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="6699f-131">Этот API позволяет разработчикам сигнализировать на основе действия пользователя, чтобы показать диалоговое окно собрания.</span><span class="sxs-lookup"><span data-stu-id="6699f-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="6699f-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="6699f-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="6699f-133">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="6699f-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="6699f-134">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="6699f-134">GetUserContext</span></span>

<span data-ttu-id="6699f-135">Обратитесь к нашему контексту ["Получить" в документации](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) по вкладке Teams, чтобы получить инструкции по идентификации получения контекстных сведений для содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="6699f-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="6699f-136">В рамках функции "Расстановка собраний" добавлено новое значение для полезной нагрузки ответа:</span><span class="sxs-lookup"><span data-stu-id="6699f-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="6699f-137">✔ **meetingId**: используется вкладками при запуске в контексте собрания.</span><span class="sxs-lookup"><span data-stu-id="6699f-137">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="6699f-138">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="6699f-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="6699f-139">Не кэшделайте роли участников кэшом, так как организатор собрания может изменить роль в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="6699f-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="6699f-140">В настоящее время Teams не поддерживает большие списки рассылки или размеры списков для API более чем 350 `GetParticipant` участников.</span><span class="sxs-lookup"><span data-stu-id="6699f-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="6699f-141">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="6699f-141">Query parameters</span></span>

|<span data-ttu-id="6699f-142">Значение</span><span class="sxs-lookup"><span data-stu-id="6699f-142">Value</span></span>|<span data-ttu-id="6699f-143">Тип</span><span class="sxs-lookup"><span data-stu-id="6699f-143">Type</span></span>|<span data-ttu-id="6699f-144">Обязательный</span><span class="sxs-lookup"><span data-stu-id="6699f-144">Required</span></span>|<span data-ttu-id="6699f-145">Описание</span><span class="sxs-lookup"><span data-stu-id="6699f-145">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="6699f-146">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="6699f-146">**meetingId**</span></span>| <span data-ttu-id="6699f-147">string</span><span class="sxs-lookup"><span data-stu-id="6699f-147">string</span></span> | <span data-ttu-id="6699f-148">Да</span><span class="sxs-lookup"><span data-stu-id="6699f-148">Yes</span></span> | <span data-ttu-id="6699f-149">Идентификатор собрания доступен через Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="6699f-149">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="6699f-150">**participantId**</span><span class="sxs-lookup"><span data-stu-id="6699f-150">**participantId**</span></span>| <span data-ttu-id="6699f-151">string</span><span class="sxs-lookup"><span data-stu-id="6699f-151">string</span></span> | <span data-ttu-id="6699f-152">Да</span><span class="sxs-lookup"><span data-stu-id="6699f-152">Yes</span></span> | <span data-ttu-id="6699f-153">ParticipantId — это ИД пользователя.</span><span class="sxs-lookup"><span data-stu-id="6699f-153">The participantId is the user ID.</span></span> <span data-ttu-id="6699f-154">Он доступен в SSO tab, Bot Invoke и клиентском SDK Teams.</span><span class="sxs-lookup"><span data-stu-id="6699f-154">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="6699f-155">Настоятельно рекомендуется получить participantId из SSO tab.</span><span class="sxs-lookup"><span data-stu-id="6699f-155">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="6699f-156">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="6699f-156">**tenantId**</span></span>| <span data-ttu-id="6699f-157">string</span><span class="sxs-lookup"><span data-stu-id="6699f-157">string</span></span> | <span data-ttu-id="6699f-158">Да</span><span class="sxs-lookup"><span data-stu-id="6699f-158">Yes</span></span> | <span data-ttu-id="6699f-159">Для пользователей клиента требуется tenantId.</span><span class="sxs-lookup"><span data-stu-id="6699f-159">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="6699f-160">Он доступен в SSO tab, Bot Invoke и клиентском SDK Teams.</span><span class="sxs-lookup"><span data-stu-id="6699f-160">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="6699f-161">Настоятельно рекомендуется получить tenantId из SSO tab.</span><span class="sxs-lookup"><span data-stu-id="6699f-161">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="6699f-162">Пример</span><span class="sxs-lookup"><span data-stu-id="6699f-162">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6699f-163">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6699f-163">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="6699f-164">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6699f-164">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="6699f-165">JSON</span><span class="sxs-lookup"><span data-stu-id="6699f-165">JSON</span></span>](#tab/json)

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="6699f-166">Тело ответа:</span><span class="sxs-lookup"><span data-stu-id="6699f-166">The response body is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="6699f-167">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="6699f-167">Response codes</span></span>

* <span data-ttu-id="6699f-168">**403:** приложению запрещено получать сведения об участниках.</span><span class="sxs-lookup"><span data-stu-id="6699f-168">**403**: The app is not allowed to get participant information.</span></span>  <span data-ttu-id="6699f-169">Это наиболее распространенный ответ об ошибке, который вызывается, если приложение не установлено на собрании.</span><span class="sxs-lookup"><span data-stu-id="6699f-169">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="6699f-170">Например, если приложение отключено администратором клиента или заблокировано во время прямой миграции сайта.</span><span class="sxs-lookup"><span data-stu-id="6699f-170">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>
* <span data-ttu-id="6699f-171">**200**: сведения об участниках успешно извлечены.</span><span class="sxs-lookup"><span data-stu-id="6699f-171">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="6699f-172">**401**: недопустимый маркер.</span><span class="sxs-lookup"><span data-stu-id="6699f-172">**401**: Invalid token.</span></span>
* <span data-ttu-id="6699f-173">**404**: не удается найти участника.</span><span class="sxs-lookup"><span data-stu-id="6699f-173">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="6699f-174">**500:** срок действия собрания истек (более 60 дней с момента окончания собрания) или у участника нет разрешений на основе их роли.</span><span class="sxs-lookup"><span data-stu-id="6699f-174">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="6699f-175">**Ожидается в ближайшее время**</span><span class="sxs-lookup"><span data-stu-id="6699f-175">**Coming Soon**</span></span>

* <span data-ttu-id="6699f-176">**404:** истек срок действия собрания или не удается найти участника.</span><span class="sxs-lookup"><span data-stu-id="6699f-176">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="6699f-177">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="6699f-177">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="6699f-178">Когда вызывается диалоговое окно собрания, то же содержимое также будет представлено в качестве сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="6699f-178">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="6699f-179">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="6699f-179">Query parameters</span></span>

|<span data-ttu-id="6699f-180">Значение</span><span class="sxs-lookup"><span data-stu-id="6699f-180">Value</span></span>|<span data-ttu-id="6699f-181">Тип</span><span class="sxs-lookup"><span data-stu-id="6699f-181">Type</span></span>|<span data-ttu-id="6699f-182">Обязательный</span><span class="sxs-lookup"><span data-stu-id="6699f-182">Required</span></span>|<span data-ttu-id="6699f-183">Описание</span><span class="sxs-lookup"><span data-stu-id="6699f-183">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="6699f-184">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="6699f-184">**conversationId**</span></span>| <span data-ttu-id="6699f-185">string</span><span class="sxs-lookup"><span data-stu-id="6699f-185">string</span></span> | <span data-ttu-id="6699f-186">Да</span><span class="sxs-lookup"><span data-stu-id="6699f-186">Yes</span></span> | <span data-ttu-id="6699f-187">Идентификатор беседы доступен при вызове бота</span><span class="sxs-lookup"><span data-stu-id="6699f-187">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="6699f-188">Пример</span><span class="sxs-lookup"><span data-stu-id="6699f-188">Example</span></span>

> [!NOTE]
>
<span data-ttu-id="6699f-189">Параметр `completionBotId` параметра является `externalResourceUrl` необязательным в запрашиваемом примере полезной нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6699f-189">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="6699f-190">`Bot ID` объявляется в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="6699f-190">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="6699f-191">Параметры ширины и высоты externalResourceUrl должны быть в пикселях.</span><span class="sxs-lookup"><span data-stu-id="6699f-191">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="6699f-192">Чтобы [убедиться,](design/designing-apps-in-meetings.md) что размеры находятся в пределах допустимого, обратитесь к рекомендациям по проектированию.</span><span class="sxs-lookup"><span data-stu-id="6699f-192">Refer to the [design guidelines](design/designing-apps-in-meetings.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="6699f-193">URL-адрес — это страница, загруженная в диалоговом оке `<iframe>` собрания.</span><span class="sxs-lookup"><span data-stu-id="6699f-193">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="6699f-194">Домен должен быть в массиве приложения `validDomains` в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="6699f-194">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6699f-195">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6699f-195">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="6699f-196">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6699f-196">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="6699f-197">JSON</span><span class="sxs-lookup"><span data-stu-id="6699f-197">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="6699f-198">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="6699f-198">Response Codes</span></span>

* <span data-ttu-id="6699f-199">**201**: успешно отправлена активность с сигналом</span><span class="sxs-lookup"><span data-stu-id="6699f-199">**201**: activity with signal is successfully sent</span></span>  
* <span data-ttu-id="6699f-200">**401**: недопустимый маркер</span><span class="sxs-lookup"><span data-stu-id="6699f-200">**401**: invalid token</span></span>  
* <span data-ttu-id="6699f-201">**201**: успешно отправлено действие с сигналом.</span><span class="sxs-lookup"><span data-stu-id="6699f-201">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="6699f-202">**401**: недопустимый маркер.</span><span class="sxs-lookup"><span data-stu-id="6699f-202">**401**: Invalid token.</span></span>
* <span data-ttu-id="6699f-203">**403:** приложению не удается отправить сигнал.</span><span class="sxs-lookup"><span data-stu-id="6699f-203">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="6699f-204">Это может произойти из-за различных причин, таких как отключение приложения администратором клиента, блокировка приложения во время миграции на веб-сайт и так далее.</span><span class="sxs-lookup"><span data-stu-id="6699f-204">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="6699f-205">В этом случае полезное сообщение содержит подробное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="6699f-205">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="6699f-206">**404:** чат собрания не существует.</span><span class="sxs-lookup"><span data-stu-id="6699f-206">**404**: Meeting chat doesn't exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="6699f-207">Включить приложение для собраний Teams</span><span class="sxs-lookup"><span data-stu-id="6699f-207">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="6699f-208">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="6699f-208">Update your app manifest</span></span>

<span data-ttu-id="6699f-209">Возможности приложения для собраний объявляются в манифесте приложения с помощью настраиваемых областейtabs  ->   и **массивов контекста.**</span><span class="sxs-lookup"><span data-stu-id="6699f-209">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="6699f-210">*Область* определяет, кому и *где будет* доступно ваше приложение, а также контекст.</span><span class="sxs-lookup"><span data-stu-id="6699f-210">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="6699f-211">Используйте [схему Developer Preview для](../resources/schema/manifest-schema-dev-preview.md) использования в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="6699f-211">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="6699f-212">Свойство Context</span><span class="sxs-lookup"><span data-stu-id="6699f-212">Context property</span></span>

<span data-ttu-id="6699f-213">Вкладка и свойства работают согласованно, чтобы вы могли определить, где будет отображаться `context` `scopes` ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="6699f-213">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="6699f-214">Вкладки в `team` области или области могут иметь несколько `groupchat` контекстов.</span><span class="sxs-lookup"><span data-stu-id="6699f-214">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="6699f-215">Возможные значения для свойства контекста:</span><span class="sxs-lookup"><span data-stu-id="6699f-215">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="6699f-216">**channelTab**: вкладка в заголке канала команды.</span><span class="sxs-lookup"><span data-stu-id="6699f-216">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="6699f-217">**privateChatTab**: вкладка в заголке группового чата между набором пользователей, не в контексте команды или собрания.</span><span class="sxs-lookup"><span data-stu-id="6699f-217">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="6699f-218">**meetingChatTab**: вкладка в заголке группового чата между набором пользователей в контексте запланированного собрания.</span><span class="sxs-lookup"><span data-stu-id="6699f-218">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="6699f-219">**meetingDetailsTab**: вкладка в заголовке представления сведений о собрании календаря.</span><span class="sxs-lookup"><span data-stu-id="6699f-219">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="6699f-220">**meetingSidePanel**: панель на собрании, открытая через единую панель (u-bar).</span><span class="sxs-lookup"><span data-stu-id="6699f-220">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="6699f-221">Свойство "Context" в настоящее время не поддерживается и, следовательно, игнорируется на мобильных клиентах</span><span class="sxs-lookup"><span data-stu-id="6699f-221">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="6699f-222">Настройка приложения для сценариев собраний</span><span class="sxs-lookup"><span data-stu-id="6699f-222">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="6699f-223">Чтобы приложение было видимым в коллекции вкладок, оно должно поддерживать настраиваемые вкладки и область **группового чата.** </span><span class="sxs-lookup"><span data-stu-id="6699f-223">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="6699f-224">Мобильные клиенты поддерживают вкладки только на поверхностях до и после собрания.</span><span class="sxs-lookup"><span data-stu-id="6699f-224">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="6699f-225">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span><span class="sxs-lookup"><span data-stu-id="6699f-225">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="6699f-226">Следуйте [указаниям для вкладок на мобильных](../tabs/design/tabs-mobile.md) устройствах при создании вкладок для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="6699f-226">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="6699f-227">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="6699f-227">Before a meeting</span></span>

<span data-ttu-id="6699f-228">Пользователи с ролями организатора и/или presenter добавляют вкладки к собранию с помощью кнопки плюс ➕ на страницах сведений о **собрании** и чате. </span><span class="sxs-lookup"><span data-stu-id="6699f-228">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="6699f-229">Расширения сообщений добавляются в меню эллипса или переполнения &#x25CF;&#x25CF;&#x25CF; под областью составить сообщение в чате.</span><span class="sxs-lookup"><span data-stu-id="6699f-229">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="6699f-230">Боты добавляются в чат собрания с помощью клавиши **@** "" и выбора **get bots.**</span><span class="sxs-lookup"><span data-stu-id="6699f-230">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="6699f-231">✔ удостоверение пользователя *должно* быть подтверждено с помощью [SSO вкладок.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="6699f-231">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="6699f-232">После этой проверки подлинности приложение может получить роль пользователя с помощью API GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="6699f-232">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="6699f-233">✔ зависимости от роли пользователя, теперь приложение сможет представлять специальные возможности.</span><span class="sxs-lookup"><span data-stu-id="6699f-233">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="6699f-234">Например, приложение для опроса может разрешить создание опроса только организаторам и организаторам.</span><span class="sxs-lookup"><span data-stu-id="6699f-234">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="6699f-235">**ПРИМЕЧАНИЕ.** Назначения ролей можно изменить во время собрания.</span><span class="sxs-lookup"><span data-stu-id="6699f-235">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="6699f-236">*См.* [роли в собрании Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="6699f-236">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="6699f-237">Во время собрания</span><span class="sxs-lookup"><span data-stu-id="6699f-237">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="6699f-238">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="6699f-238">**sidePanel**</span></span>

<span data-ttu-id="6699f-239">✔ в манифесте приложения добавьте **sidePanel** в массив **контекста,** как описано выше.</span><span class="sxs-lookup"><span data-stu-id="6699f-239">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="6699f-240">✔ собрания, как и во всех сценариях, приложение будет отрисовыно на вкладке собрания шириной 320px.</span><span class="sxs-lookup"><span data-stu-id="6699f-240">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="6699f-241">Для этого необходимо оптимизировать вкладку.</span><span class="sxs-lookup"><span data-stu-id="6699f-241">Your tab must be optimized for this.</span></span> <span data-ttu-id="6699f-242">*См.* интерфейс [FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="6699f-242">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="6699f-243">✔Соотделите в [SDK Teams,](../tabs/how-to/access-teams-context.md#user-context) чтобы использовать API **userContext** для маршрутов запросов соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="6699f-243">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="6699f-244">✔ для вкладок обратитесь к [потоку проверки подлинности Teams.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="6699f-244">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="6699f-245">Поток проверки подлинности для вкладок очень похож на поток проверки подлинности для веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="6699f-245">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="6699f-246">Таким образом, вкладки могут использовать OAuth 2.0 напрямую.</span><span class="sxs-lookup"><span data-stu-id="6699f-246">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="6699f-247">*См. также,* платформа удостоверений Майкрософт и поток кода авторизации [OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)</span><span class="sxs-lookup"><span data-stu-id="6699f-247">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="6699f-248">✔ сообщение должно работать ожидаемым, когда пользователь находится в представлении собрания и должен иметь возможность опубликовать карточки расширения сообщения.</span><span class="sxs-lookup"><span data-stu-id="6699f-248">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="6699f-249">✔ AppName in-meeting — в выдавке tooltip должно быть занося имя приложения в панели U-bar собрания.</span><span class="sxs-lookup"><span data-stu-id="6699f-249">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="6699f-250">**Диалоговое окно собрания**</span><span class="sxs-lookup"><span data-stu-id="6699f-250">**In-meeting dialog**</span></span>

<span data-ttu-id="6699f-251">✔ Вы должны соблюдать рекомендации по проектированию [диалогового окна собрания.](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="6699f-251">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="6699f-252">✔ для вкладок обратитесь к [потоку проверки подлинности Teams.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="6699f-252">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="6699f-253">✔ использовать API [](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) уведомлений, чтобы сигнализировать о том, что необходимо инициализировать уведомление о пузырьке.</span><span class="sxs-lookup"><span data-stu-id="6699f-253">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="6699f-254">✔ Как часть полезной нагрузки запроса на уведомление, включайте URL-адрес, где находится демонстрация содержимого.</span><span class="sxs-lookup"><span data-stu-id="6699f-254">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="6699f-255">✔ собрания не должен использовать модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="6699f-255">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="6699f-256">Эти уведомления имеют постоянный характер.</span><span class="sxs-lookup"><span data-stu-id="6699f-256">These notifications are persistent in nature.</span></span> <span data-ttu-id="6699f-257">Необходимо вызвать функцию [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического скрытие после того, как пользователь делает действие в веб-представлении.</span><span class="sxs-lookup"><span data-stu-id="6699f-257">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="6699f-258">Это требование для отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="6699f-258">This is a requirement for app submission.</span></span> <span data-ttu-id="6699f-259">*См. также*, [Teams SDK: модуль задачи](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="6699f-259">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="6699f-260">Если вы хотите, чтобы ваше приложение поддерживает анонимных пользователей, то для исходного запроса на вызов необходимо использовать метаданные запроса (ИД пользователя) в объекте, а не метаданные `from.id` `from` `from.aadObjectId` запроса (Azure Active Directory ID пользователя).</span><span class="sxs-lookup"><span data-stu-id="6699f-260">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="6699f-261">*См.* ["Использование модулей задач на вкладке"](../task-modules-and-cards/task-modules/task-modules-tabs.md) и ["Создание и отправка модуля задачи".](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="6699f-261">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="6699f-262">После собрания</span><span class="sxs-lookup"><span data-stu-id="6699f-262">After a meeting</span></span>

<span data-ttu-id="6699f-263">Конфигурации после собрания и до собрания эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="6699f-263">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="6699f-264">Пример приложения для собраний</span><span class="sxs-lookup"><span data-stu-id="6699f-264">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="6699f-265">Приложение генератора маркеров собраний</span><span class="sxs-lookup"><span data-stu-id="6699f-265">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
