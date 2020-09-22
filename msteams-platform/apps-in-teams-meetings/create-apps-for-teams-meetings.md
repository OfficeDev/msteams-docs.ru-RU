---
title: Создание приложений для собраний в Teams
author: laujan
description: Создание приложений для собраний в Teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API роли участника для собраний приложений Teams
ms.openlocfilehash: 83e0a5b53e363a090935b4afa9840dd96c5f7381
ms.sourcegitcommit: b01986739a05c65094618fbe76aeb53d038b1c74
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2020
ms.locfileid: "48182037"
---
# <a name="create-apps-for-teams-meetings-preview"></a><span data-ttu-id="6e958-104">Создание приложений для собраний в Teams (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="6e958-104">Create apps for Teams meetings (Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="6e958-105">Функции, включенные в Microsoft Teams Preview, предоставляются только для целей раннего доступа, тестирования и обратной связи.</span><span class="sxs-lookup"><span data-stu-id="6e958-105">Features included in Microsoft Teams preview are provided for early-access, testing, and feedback purposes only.</span></span> <span data-ttu-id="6e958-106">Они могут быть подвергнуты изменениям, прежде чем стать доступными в общедоступном выпуске и не должны использоваться в рабочих приложениях.</span><span class="sxs-lookup"><span data-stu-id="6e958-106">They may undergo changes before becoming available in the public release and should not be used in production applications.</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="6e958-107">Необходимые условия и рекомендации</span><span class="sxs-lookup"><span data-stu-id="6e958-107">Prerequisites and considerations</span></span>

1. <span data-ttu-id="6e958-108">Приложения в собраниях требуют некоторых базовых знаний о [разработке приложений Teams](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="6e958-108">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="6e958-109">Приложение на собрании может состоять из компонентов [вкладок](../tabs/what-are-tabs.md), [Боты](../bots/what-are-bots.md)и [расширений обмена сообщениями](../messaging-extensions/what-are-messaging-extensions.md) и потребует обновления [манифеста приложения](#update-your-app-manifest) Teams, чтобы указать, что приложение доступно для собраний.</span><span class="sxs-lookup"><span data-stu-id="6e958-109">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="6e958-110">Чтобы ваше приложение функционировало в жизненном цикле собрания как вкладка, оно должно поддерживать настраиваемые вкладки в [области groupchat](../resources/schema/manifest-schema.md#configurabletabs).</span><span class="sxs-lookup"><span data-stu-id="6e958-110">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="6e958-111">*Ознакомьтесь* [со статьей расширение приложения Teams с помощью настраиваемой вкладки](../tabs/how-to/add-tab.md). Поддержка `groupchat` области позволит приложению в беседах, [выполняемых перед собранием](teams-apps-in-meetings.md#pre-meeting-app-experience) и [после](teams-apps-in-meetings.md#post-meeting-app-experience) него.</span><span class="sxs-lookup"><span data-stu-id="6e958-111">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="6e958-112">Параметры URL-адреса API собраний могут потребоваться `meetingId` , `userId` а значение [tenantId](/onedrive/find-your-office-365-tenant-id) — в составе клиента Teams SDK и действия Bot.</span><span class="sxs-lookup"><span data-stu-id="6e958-112">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="6e958-113">Кроме того, можно получить сведения о надежной информации для идентификатора пользователя и идентификатора клиента с помощью [проверки подлинности на основе единого входа](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="6e958-113">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="6e958-114">Некоторые API собраний, например, `GetParticipant` требуют [регистрации Bot и идентификатора приложения Bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) для создания маркеров проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6e958-114">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="6e958-115">Разработчикам следует соблюдать общие [рекомендации по проектированию вкладок Teams](../tabs/design/tabs.md) для сценариев, выполняемых перед и после собраний, а также [указания по диалоговому](designing-in-meeting-dialog.md) окну для собраний в диалоговом окне для собраний, инициированном во время собрания Teams.</span><span class="sxs-lookup"><span data-stu-id="6e958-115">Developers must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](designing-in-meeting-dialog.md) for in-meeting dialog triggered during a Teams meeting.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="6e958-116">Справочные материалы по API приложений для собраний</span><span class="sxs-lookup"><span data-stu-id="6e958-116">Meeting apps API reference</span></span>

|<span data-ttu-id="6e958-117">API</span><span class="sxs-lookup"><span data-stu-id="6e958-117">API</span></span>|<span data-ttu-id="6e958-118">Описание</span><span class="sxs-lookup"><span data-stu-id="6e958-118">Description</span></span>|<span data-ttu-id="6e958-119">Запрос</span><span class="sxs-lookup"><span data-stu-id="6e958-119">Request</span></span>|<span data-ttu-id="6e958-120">Source</span><span class="sxs-lookup"><span data-stu-id="6e958-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="6e958-121">**жетусерконтекст**</span><span class="sxs-lookup"><span data-stu-id="6e958-121">**GetUserContext**</span></span>| <span data-ttu-id="6e958-122">Получение контекстной информации для отображения релевантного контента на вкладке "команды".</span><span class="sxs-lookup"><span data-stu-id="6e958-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="6e958-123">_**microsoftTeams. SPContext (() => {/*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="6e958-123">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="6e958-124">Пакет SDK для клиента Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6e958-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="6e958-125">**В качестве имени участника**</span><span class="sxs-lookup"><span data-stu-id="6e958-125">**GetParticipant**</span></span>|<span data-ttu-id="6e958-126">Этот API позволяет интерфейсу Bot получать сведения об участниках по идентификатору собрания и идентификатору участника.</span><span class="sxs-lookup"><span data-stu-id="6e958-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="6e958-127">**Получение** _ **/v1/meetings/{meetingId}/Participants/{participantId}? tenantId = {tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="6e958-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="6e958-128">Пакет SDK Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="6e958-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="6e958-129">**нотификатионсигнал**</span><span class="sxs-lookup"><span data-stu-id="6e958-129">**NotificationSignal**</span></span> |<span data-ttu-id="6e958-130">Сигналы собраний будут доставляться с помощью следующего существующего API уведомления о беседе (для разговора пользователя в Bot).</span><span class="sxs-lookup"><span data-stu-id="6e958-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="6e958-131">Этот API позволяет разработчикам сообщать на основании действий пользователя, чтобы показывать всплывающее диалоговое окно в собрании.</span><span class="sxs-lookup"><span data-stu-id="6e958-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="6e958-132">**POST** _ **/v3/conversations/{conversationId}/Activities**_</span><span class="sxs-lookup"><span data-stu-id="6e958-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="6e958-133">Пакет SDK Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="6e958-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="6e958-134">жетусерконтекст</span><span class="sxs-lookup"><span data-stu-id="6e958-134">GetUserContext</span></span>

<span data-ttu-id="6e958-135">Обратитесь к нашему [контексту Get for Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) , чтобы узнать, как идентифицировать и получить контекстные сведения для содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="6e958-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="6e958-136">В рамках расширяемости собраний для полезных данных ответа было добавлено новое значение.</span><span class="sxs-lookup"><span data-stu-id="6e958-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="6e958-137">✔ **meetingId**: используется вкладкой при запуске в контексте собрания.</span><span class="sxs-lookup"><span data-stu-id="6e958-137">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="6e958-138">API-интерфейс-участник</span><span class="sxs-lookup"><span data-stu-id="6e958-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="6e958-139">Не кэшировать роли участников, так как организатор собрания может изменить роль в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="6e958-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="6e958-140">В настоящее время Teams не поддерживает большие списки рассылки или размеры списков, более 350 участников для `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="6e958-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>
>
> * <span data-ttu-id="6e958-141">Поддержка пакет SDK для ленты скоро будет доступна.</span><span class="sxs-lookup"><span data-stu-id="6e958-141">Support for the Bot Framework SDK is coming soon.</span></span>

#### <a name="request"></a><span data-ttu-id="6e958-142">Запрос</span><span class="sxs-lookup"><span data-stu-id="6e958-142">Request</span></span>

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="6e958-143">*Ознакомьтесь* со статьей [Справочник по API-интерфейсу Bot Framework](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="6e958-143">*See* the [Bot Framework API reference](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<!-- markdownlint-disable MD025 -->

<span data-ttu-id="6e958-144">**Пример на языке C#**</span><span class="sxs-lookup"><span data-stu-id="6e958-144">**C# Example**</span></span>

```csharp
string meetingId = "meetingid?";
string participantId = "participantidhere";
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage();
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
request.Method = new HttpMethod("GET");
request.RequestUri = new System.Uri(Path.Combine(connectorClient.BaseUri.OriginalString, $"/meetings/{meetingId}/participants/{participantId}"));
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, cancellationToken).ConfigureAwait(false);
if (response.StatusCode == System.Net.HttpStatusCode.OK)
{
    var content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
    var theObject = Rest.Serialization.SafeJsonConvert.DeserializeObject<WhateverObjectIsReturned>(content, connectorClient.DeserializationSettings);
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a><span data-ttu-id="6e958-145">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="6e958-145">Query parameters</span></span>

<span data-ttu-id="6e958-146">**meetingId**.</span><span class="sxs-lookup"><span data-stu-id="6e958-146">**meetingId**.</span></span> <span data-ttu-id="6e958-147">Необходимо указать идентификатор собрания.</span><span class="sxs-lookup"><span data-stu-id="6e958-147">The meeting identifier is required.</span></span>  
<span data-ttu-id="6e958-148">**партиЦипантид**.</span><span class="sxs-lookup"><span data-stu-id="6e958-148">**participantId**.</span></span> <span data-ttu-id="6e958-149">Необходимо указать идентификатор участника.</span><span class="sxs-lookup"><span data-stu-id="6e958-149">The participant identifier is required.</span></span>  
<span data-ttu-id="6e958-150">**tenantId**.</span><span class="sxs-lookup"><span data-stu-id="6e958-150">**tenantId**.</span></span> <span data-ttu-id="6e958-151">[Идентификатор клиента](/onedrive/find-your-office-365-tenant-id) участника.</span><span class="sxs-lookup"><span data-stu-id="6e958-151">[Tenant id](/onedrive/find-your-office-365-tenant-id) of the participant.</span></span> <span data-ttu-id="6e958-152">Обязательный для пользователя клиента.</span><span class="sxs-lookup"><span data-stu-id="6e958-152">Required for tenant user.</span></span>

#### <a name="response-payload"></a><span data-ttu-id="6e958-153">Полезные данные ответа</span><span class="sxs-lookup"><span data-stu-id="6e958-153">Response Payload</span></span>
<!-- markdownlint-disable MD036 -->

<span data-ttu-id="6e958-154">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="6e958-154">**Example 1**</span></span>

```json
{
    "meetingRole":"Presenter",
    "conversation":{
            "isGroup": true,
            "id": "19:meeting_NDQxMzg1YjUtMGIzNC00Yjc1LWFmYWYtYzk1MGY2MTMwNjE0@thread.v2"
        }
}
```

<span data-ttu-id="6e958-155">**митингроле** может быть *организатором*, *докладчиком*или *участником*.</span><span class="sxs-lookup"><span data-stu-id="6e958-155">**meetingRole** can be *Organizer*, *Presenter*, or *Attendee*.</span></span>

<span data-ttu-id="6e958-156">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="6e958-156">**Example 2**</span></span>

```json
{
    "meetingRole": "Attendee",
    "conversation": {
        "isGroup": true,
        "id": "19:meeting_OWIyYWVhZWMtM2ExMi00ZTc2LTg0OGEtYWNhMTM4MmZlZTNj@thread.v2"
        }
}
```

#### <a name="response-codes"></a><span data-ttu-id="6e958-157">Коды ответов</span><span class="sxs-lookup"><span data-stu-id="6e958-157">Response Codes</span></span>

<span data-ttu-id="6e958-158">**403**: приложению не разрешено получать сведения об участнике.</span><span class="sxs-lookup"><span data-stu-id="6e958-158">**403**: the app is not allowed to get participant information.</span></span> <span data-ttu-id="6e958-159">Это наиболее распространенный ответ об ошибке, который активируется, когда приложение не установлено в собрании, например, когда приложение отключено администратором клиента или блокируется во время снижения риска для Live сайта.</span><span class="sxs-lookup"><span data-stu-id="6e958-159">This will be the most common error response and is triggered when the app is not installed in the meeting such as when the app is disabled by tenant admin or blocked during live site mitigation.</span></span>  
<span data-ttu-id="6e958-160">**200**: сведения о участниках успешно получены</span><span class="sxs-lookup"><span data-stu-id="6e958-160">**200**: participant information successfully retrieved</span></span>  
<span data-ttu-id="6e958-161">**401**: недопустимый маркер</span><span class="sxs-lookup"><span data-stu-id="6e958-161">**401**: invalid token</span></span>  
<span data-ttu-id="6e958-162">**404**: собрание не существует или не удается найти его участника.</span><span class="sxs-lookup"><span data-stu-id="6e958-162">**404**: the meeting doesn't exist or participant can’t be found.</span></span>

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a><span data-ttu-id="6e958-163">API Нотификатионсигнал</span><span class="sxs-lookup"><span data-stu-id="6e958-163">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="6e958-164">Когда вызывается диалоговое окно для собраний, то то же самое содержимое также будет представлено в виде сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="6e958-164">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="request"></a><span data-ttu-id="6e958-165">Запрос</span><span class="sxs-lookup"><span data-stu-id="6e958-165">Request</span></span>

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a><span data-ttu-id="6e958-166">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="6e958-166">Query parameters</span></span>

<span data-ttu-id="6e958-167">**conversationId**: идентификатор беседы.</span><span class="sxs-lookup"><span data-stu-id="6e958-167">**conversationId**: The conversation identifier.</span></span> <span data-ttu-id="6e958-168">Обязательный</span><span class="sxs-lookup"><span data-stu-id="6e958-168">Required</span></span>

#### <a name="request-payload"></a><span data-ttu-id="6e958-169">Полезные данные запроса</span><span class="sxs-lookup"><span data-stu-id="6e958-169">Request Payload</span></span>

# <a name="json"></a>[<span data-ttu-id="6e958-170">JSON</span><span class="sxs-lookup"><span data-stu-id="6e958-170">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
    "notification": {
    "alert": true,
    "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
    }
},
    "replyToId": "1493070356924"
    }
```

# <a name="cnet"></a>[<span data-ttu-id="6e958-171">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6e958-171">C#/.NET</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
{
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
};
activity.ChannelData = new TeamsChannelData
{
    Notification = notification
};
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="6e958-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6e958-172">JavaScript</span></span>](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
        replyActivity.channelData = {
            notification: {
                alertInMeeting: true,
                externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>’
            }
        };
        await context.sendActivity(replyActivity);
```

* * *

> [!IMPORTANT]
> <span data-ttu-id="6e958-173">URL-адрес в пузырьке содержимого (URL-адрес Таскинфо) должен быть включен в список [допустимых доменов](../resources/schema/manifest-schema.md#validdomains) , включенный в манифест приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="6e958-173">The URL in the content bubble (taskInfo URL) must be included in the [valid domains](../resources/schema/manifest-schema.md#validdomains) list included in the Teams app manifest.</span></span>

#### <a name="response-codes"></a><span data-ttu-id="6e958-174">Коды ответов</span><span class="sxs-lookup"><span data-stu-id="6e958-174">Response Codes</span></span>

<span data-ttu-id="6e958-175">**201**: действие с сигналом успешно отправлено</span><span class="sxs-lookup"><span data-stu-id="6e958-175">**201**: activity with signal is successfully sent</span></span>  
<span data-ttu-id="6e958-176">**401**: недопустимый маркер</span><span class="sxs-lookup"><span data-stu-id="6e958-176">**401**: invalid token</span></span>  
<span data-ttu-id="6e958-177">**403**: приложению не разрешено отправлять сигнал.</span><span class="sxs-lookup"><span data-stu-id="6e958-177">**403**: the app is not allowed to send the signal.</span></span> <span data-ttu-id="6e958-178">В этом случае полезная нагрузка должна содержать более подробное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="6e958-178">In this case, the payload should contain more detail error message.</span></span> <span data-ttu-id="6e958-179">Может быть несколько причин: приложение отключено администратором клиента, заблокировано во время снижения риска на сайте Live и т. д.</span><span class="sxs-lookup"><span data-stu-id="6e958-179">There can be many reasons: app disabled by tenant admin, blocked during live site mitigation, etc.</span></span>  
<span data-ttu-id="6e958-180">**404**: чат для собрания не существует</span><span class="sxs-lookup"><span data-stu-id="6e958-180">**404**: meeting chat doesn't exist</span></span>  

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="6e958-181">Включение собраний для приложений в Teams</span><span class="sxs-lookup"><span data-stu-id="6e958-181">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="6e958-182">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="6e958-182">Update your app manifest</span></span>

<span data-ttu-id="6e958-183">Возможности приложений для собраний объявляются в манифесте приложения с **configurableTabs**помощью  ->  **областей** конфигураблетабс и **контекстных** массивов.</span><span class="sxs-lookup"><span data-stu-id="6e958-183">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="6e958-184">*Область* определяет, для кого и *контекст* определяет, где будет доступно ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="6e958-184">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="6e958-185">Свойство Context</span><span class="sxs-lookup"><span data-stu-id="6e958-185">Context property</span></span>

<span data-ttu-id="6e958-186">Вкладка `context` и `scopes` свойства работают по гармонии, чтобы определить, где должно отображаться ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="6e958-186">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="6e958-187">Несмотря на то, `personal` что вкладки в области могут иметь только один контекст, например, `personalTab`  `team` или `groupchat` вкладки с ограниченной областью действия могут иметь несколько контекстов.</span><span class="sxs-lookup"><span data-stu-id="6e958-187">While tabs in the `personal` scope can only have one context, i.e., `personalTab`,  `team` or `groupchat` scoped tabs can have more than one context.</span></span> <span data-ttu-id="6e958-188">Для свойства Context возможны следующие значения:</span><span class="sxs-lookup"><span data-stu-id="6e958-188">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="6e958-189">**чаннелтаб**: вкладка в заголовке канала команды.</span><span class="sxs-lookup"><span data-stu-id="6e958-189">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="6e958-190">**приватечаттаб**: вкладка в заголовке группового чата между набором пользователей, которых нет в контексте команды или собрания.</span><span class="sxs-lookup"><span data-stu-id="6e958-190">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="6e958-191">**митингчаттаб**: вкладка в заголовке группового чата между набором пользователей в контексте запланированного собрания.</span><span class="sxs-lookup"><span data-stu-id="6e958-191">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="6e958-192">**митингдетаилстаб**: вкладка в заголовке представления сведений о собрании календаря.</span><span class="sxs-lookup"><span data-stu-id="6e958-192">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="6e958-193">**митингсидепанел**: панель для собраний, открытая с помощью унифицированной панели (u-борта).</span><span class="sxs-lookup"><span data-stu-id="6e958-193">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="6e958-194">Настройка приложения для сценариев собраний</span><span class="sxs-lookup"><span data-stu-id="6e958-194">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> <span data-ttu-id="6e958-195">Чтобы ваше приложение отображалось в коллекции вкладок, оно должно **поддерживать настраиваемые вкладки** и **область применения группового чата**.</span><span class="sxs-lookup"><span data-stu-id="6e958-195">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>

### <a name="pre-meeting"></a><span data-ttu-id="6e958-196">Предварительное собрание</span><span class="sxs-lookup"><span data-stu-id="6e958-196">Pre-meeting</span></span>

<span data-ttu-id="6e958-197">Пользователи с ролями органайзера и докладчика добавляют вкладки на собрание с помощью кнопки "плюс ➕" в разделе " **беседы** для собраний" и " **сведения о** собрании".</span><span class="sxs-lookup"><span data-stu-id="6e958-197">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="6e958-198">Расширения обмена сообщениями добавляются в меню "многоточия/переполнение" &#x25CF;&#x25CF;&#x25CF; , расположенного под областью создание сообщения в чате.</span><span class="sxs-lookup"><span data-stu-id="6e958-198">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="6e958-199">Боты добавляются в чат для собрания с помощью **@** ключа "" и выбора **Get Боты**.</span><span class="sxs-lookup"><span data-stu-id="6e958-199">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="6e958-200">✔ Удостоверение пользователя *должно* быть подтверждено с помощью [единого входа вкладок](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="6e958-200">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="6e958-201">После проверки подлинности приложение может получить роль пользователя через API-участник.</span><span class="sxs-lookup"><span data-stu-id="6e958-201">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="6e958-202">✔ На основе роли пользователя, приложение теперь будет иметь возможность для отображения специальных интерфейсов для ролей.</span><span class="sxs-lookup"><span data-stu-id="6e958-202">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="6e958-203">Например, приложение опроса может разрешить только организаторов и докладчикам создавать новый опрос.</span><span class="sxs-lookup"><span data-stu-id="6e958-203">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="6e958-204">**Note**: назначения ролей могут быть изменены во время собрания.</span><span class="sxs-lookup"><span data-stu-id="6e958-204">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="6e958-205">*Просмотр* [ролей в собрании Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="6e958-205">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="in-meeting"></a><span data-ttu-id="6e958-206">На собрании</span><span class="sxs-lookup"><span data-stu-id="6e958-206">In-meeting</span></span>

#### <a name="side-panel"></a><span data-ttu-id="6e958-207">**Боковая панель**</span><span class="sxs-lookup"><span data-stu-id="6e958-207">**side-panel**</span></span>

<span data-ttu-id="6e958-208">✔ В манифесте приложения добавьте **сидепанел** в массив **митингсурфацес** , как описано выше.</span><span class="sxs-lookup"><span data-stu-id="6e958-208">✔ In your app manifest add **sidePanel** to the **meetingSurfaces** array as described above.</span></span>

<span data-ttu-id="6e958-209">✔ На собрании, так же, как и во всех сценариях, приложение будет отображаться на вкладке, расположенной в собрании, 320 пикселей по ширине.</span><span class="sxs-lookup"><span data-stu-id="6e958-209">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="6e958-210">Для этого необходимо оптимизировать вкладку.</span><span class="sxs-lookup"><span data-stu-id="6e958-210">Your tab must be optimized for this.</span></span> <span data-ttu-id="6e958-211">*Просмотр*, [интерфейс фрамеконтекст](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="6e958-211">*See*, [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span></span>

<span data-ttu-id="6e958-212">✔ Ссылаться на [пакет SDK Teams](../tabs/how-to/access-teams-context.md#user-context) , чтобы использовать API **UserContext** для соответствующей маршрутизации запросов.</span><span class="sxs-lookup"><span data-stu-id="6e958-212">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="6e958-213">✔ Ссылаться на [процесс проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="6e958-213">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="6e958-214">Процесс проверки подлинности для вкладок очень похож на процесс проверки подлинности для веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="6e958-214">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="6e958-215">Таким образом, вкладки могут напрямую использовать OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="6e958-215">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="6e958-216">*Кроме того, можно просмотреть* [потоки кода авторизации для платформы Microsoft identity и OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="6e958-216">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="6e958-217">**диалоговое окно "в собрании"**</span><span class="sxs-lookup"><span data-stu-id="6e958-217">**in-meeting dialog**</span></span>

<span data-ttu-id="6e958-218">✔ Необходимо следовать [рекомендациям по разработке диалоговых окон для собраний](designing-in-meeting-dialog.md).</span><span class="sxs-lookup"><span data-stu-id="6e958-218">✔ You must adhere to the [in-meeting dialog design guidelines](designing-in-meeting-dialog.md).</span></span>

<span data-ttu-id="6e958-219">✔ Ссылаться на [процесс проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="6e958-219">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="6e958-220">✔ Использовать API [уведомлений](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) для сигнализации о необходимости запуска пузырькового уведомления.</span><span class="sxs-lookup"><span data-stu-id="6e958-220">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="6e958-221">✔ Как часть полезных данных запроса уведомления, укажите URL-адрес, по которому размещается контент, предназначенный для демонстрации.</span><span class="sxs-lookup"><span data-stu-id="6e958-221">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

> [!NOTE]
> <span data-ttu-id="6e958-222">Эти уведомления постоянны.</span><span class="sxs-lookup"><span data-stu-id="6e958-222">These notifications are persistent in nature.</span></span> <span data-ttu-id="6e958-223">Необходимо вызвать функцию [**субмиттаск ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического закрытия после того, как пользователь выполняет действие в веб-представлении.</span><span class="sxs-lookup"><span data-stu-id="6e958-223">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="6e958-224">Это требование для отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="6e958-224">This is a requirement for app submission.</span></span> <span data-ttu-id="6e958-225">*Раздел* [пакет SDK для teams: Task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="6e958-225">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>

### <a name="post-meeting"></a><span data-ttu-id="6e958-226">Завершающее собрание</span><span class="sxs-lookup"><span data-stu-id="6e958-226">Post-meeting</span></span>

<span data-ttu-id="6e958-227">Конфигурации после собрания и предварительного собрания эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="6e958-227">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="6e958-228">Пример приложения для собраний</span><span class="sxs-lookup"><span data-stu-id="6e958-228">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="6e958-229">Приложение генератора маркеров собраний</span><span class="sxs-lookup"><span data-stu-id="6e958-229">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
