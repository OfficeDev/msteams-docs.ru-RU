---
title: Создание приложений для собраний групп
author: laujan
description: Создание приложений для собраний в Teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API роли участника для собраний приложений Teams
ms.openlocfilehash: f448885e3664209858eb90fa9f0853c3d31e015a
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409115"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="cee64-104">Создание приложений для собраний групп</span><span class="sxs-lookup"><span data-stu-id="cee64-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="cee64-105">Необходимые условия и рекомендации</span><span class="sxs-lookup"><span data-stu-id="cee64-105">Prerequisites and considerations</span></span>

1. <span data-ttu-id="cee64-106">Приложения в собраниях требуют некоторых базовых знаний о [разработке приложений Teams](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="cee64-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="cee64-107">Приложение на собрании может состоять из компонентов [вкладок](../tabs/what-are-tabs.md), [Боты](../bots/what-are-bots.md)и [расширений обмена сообщениями](../messaging-extensions/what-are-messaging-extensions.md) и потребует обновления [манифеста приложения](#update-your-app-manifest) Teams, чтобы указать, что приложение доступно для собраний.</span><span class="sxs-lookup"><span data-stu-id="cee64-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="cee64-108">Чтобы ваше приложение функционировало в жизненном цикле собрания как вкладка, оно должно поддерживать настраиваемые вкладки в [области groupchat](../resources/schema/manifest-schema.md#configurabletabs).</span><span class="sxs-lookup"><span data-stu-id="cee64-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="cee64-109">*Ознакомьтесь* [со статьей расширение приложения Teams с помощью настраиваемой вкладки](../tabs/how-to/add-tab.md). Поддержка `groupchat` области позволит приложению в беседах, [выполняемых перед собранием](teams-apps-in-meetings.md#pre-meeting-app-experience) и [после](teams-apps-in-meetings.md#post-meeting-app-experience) него.</span><span class="sxs-lookup"><span data-stu-id="cee64-109">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="cee64-110">Параметры URL-адреса API собраний могут потребоваться `meetingId` , `userId` а значение [tenantId](/onedrive/find-your-office-365-tenant-id) — в составе клиента Teams SDK и действия Bot.</span><span class="sxs-lookup"><span data-stu-id="cee64-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="cee64-111">Кроме того, можно получить сведения о надежной информации для идентификатора пользователя и идентификатора клиента с помощью [проверки подлинности на основе единого входа](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="cee64-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="cee64-112">Некоторые API собраний, например, `GetParticipant` требуют [регистрации Bot и идентификатора приложения Bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) для создания маркеров проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="cee64-112">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="cee64-113">Разработчикам следует соблюдать общие [рекомендации по проектированию вкладок Teams](../tabs/design/tabs.md) для сценариев, выполняемых перед и после собраний, а также [указания по диалоговому](design/designing-in-meeting-dialog.md) окну для собраний в диалоговом окне для собраний, инициированном во время собрания Teams.</span><span class="sxs-lookup"><span data-stu-id="cee64-113">As a developer, you must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-in-meeting-dialog.md) for in-meeting dialog triggered during a Teams meeting.</span></span>

1. <span data-ttu-id="cee64-114">Обратите внимание, что чтобы приложение обновлялось в режиме реального времени, оно должно быть актуальным в соответствии с действиями событий в собрании.</span><span class="sxs-lookup"><span data-stu-id="cee64-114">Please note that in order for your app to be updated in real-time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="cee64-115">Эти события могут находиться в диалоговом окне собрания (обратитесь к `bot Id` параметру завершения в `Notification Signal API` ) и другим поверхностям во время жизненного цикла собрания.</span><span class="sxs-lookup"><span data-stu-id="cee64-115">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="cee64-116">Справочные материалы по API приложений для собраний</span><span class="sxs-lookup"><span data-stu-id="cee64-116">Meeting apps API reference</span></span>

|<span data-ttu-id="cee64-117">API</span><span class="sxs-lookup"><span data-stu-id="cee64-117">API</span></span>|<span data-ttu-id="cee64-118">Описание</span><span class="sxs-lookup"><span data-stu-id="cee64-118">Description</span></span>|<span data-ttu-id="cee64-119">Запрос</span><span class="sxs-lookup"><span data-stu-id="cee64-119">Request</span></span>|<span data-ttu-id="cee64-120">Source</span><span class="sxs-lookup"><span data-stu-id="cee64-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="cee64-121">**жетусерконтекст**</span><span class="sxs-lookup"><span data-stu-id="cee64-121">**GetUserContext**</span></span>| <span data-ttu-id="cee64-122">Получение контекстной информации для отображения релевантного контента на вкладке "команды".</span><span class="sxs-lookup"><span data-stu-id="cee64-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="cee64-123">_**microsoftTeams. SPContext (() => {/*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="cee64-123">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="cee64-124">Пакет SDK для клиента Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cee64-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="cee64-125">**В качестве имени участника**</span><span class="sxs-lookup"><span data-stu-id="cee64-125">**GetParticipant**</span></span>|<span data-ttu-id="cee64-126">Этот API позволяет интерфейсу Bot получать сведения об участниках по идентификатору собрания и идентификатору участника.</span><span class="sxs-lookup"><span data-stu-id="cee64-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="cee64-127">**Получение** _**/v1/meetings/{meetingId}/Participants/{participantId}? tenantId = {tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="cee64-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="cee64-128">Пакет SDK Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="cee64-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="cee64-129">**нотификатионсигнал**</span><span class="sxs-lookup"><span data-stu-id="cee64-129">**NotificationSignal**</span></span> |<span data-ttu-id="cee64-130">Сигналы собраний будут доставляться с помощью следующего существующего API уведомления о беседе (для разговора пользователя в Bot).</span><span class="sxs-lookup"><span data-stu-id="cee64-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="cee64-131">Этот API позволяет разработчикам сообщать на основании действий пользователя, чтобы показывать всплывающее диалоговое окно в собрании.</span><span class="sxs-lookup"><span data-stu-id="cee64-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="cee64-132">**POST** _**/v3/conversations/{conversationId}/Activities**_</span><span class="sxs-lookup"><span data-stu-id="cee64-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="cee64-133">Пакет SDK Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="cee64-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="cee64-134">жетусерконтекст</span><span class="sxs-lookup"><span data-stu-id="cee64-134">GetUserContext</span></span>

<span data-ttu-id="cee64-135">Обратитесь к нашему [контексту Get for Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) , чтобы узнать, как идентифицировать и получить контекстные сведения для содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="cee64-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="cee64-136">В рамках расширяемости собраний для полезных данных ответа было добавлено новое значение.</span><span class="sxs-lookup"><span data-stu-id="cee64-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="cee64-137">✔ **meetingId**: используется вкладкой при запуске в контексте собрания.</span><span class="sxs-lookup"><span data-stu-id="cee64-137">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="cee64-138">API-интерфейс-участник</span><span class="sxs-lookup"><span data-stu-id="cee64-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="cee64-139">Не кэшировать роли участников, так как организатор собрания может изменить роль в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="cee64-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="cee64-140">В настоящее время Teams не поддерживает большие списки рассылки или размеры списков, более 350 участников для `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="cee64-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>
>
> * <span data-ttu-id="cee64-141">Поддержка пакет SDK для ленты скоро будет доступна.</span><span class="sxs-lookup"><span data-stu-id="cee64-141">Support for the Bot Framework SDK is coming soon.</span></span>


#### <a name="request"></a><span data-ttu-id="cee64-142">Запрос</span><span class="sxs-lookup"><span data-stu-id="cee64-142">Request</span></span>

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="cee64-143">*Ознакомьтесь* со статьей [Справочник по API-интерфейсу Bot Framework](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="cee64-143">*See* the [Bot Framework API reference](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<!-- markdownlint-disable MD025 -->

<span data-ttu-id="cee64-144">**Пример на языке C#**</span><span class="sxs-lookup"><span data-stu-id="cee64-144">**C# Example**</span></span>

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
}
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a><span data-ttu-id="cee64-145">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="cee64-145">Query parameters</span></span>

|<span data-ttu-id="cee64-146">Value</span><span class="sxs-lookup"><span data-stu-id="cee64-146">Value</span></span>|<span data-ttu-id="cee64-147">Тип</span><span class="sxs-lookup"><span data-stu-id="cee64-147">Type</span></span>|<span data-ttu-id="cee64-148">Обязательный</span><span class="sxs-lookup"><span data-stu-id="cee64-148">Required</span></span>|<span data-ttu-id="cee64-149">Описание</span><span class="sxs-lookup"><span data-stu-id="cee64-149">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="cee64-150">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="cee64-150">**meetingId**</span></span>| <span data-ttu-id="cee64-151">string</span><span class="sxs-lookup"><span data-stu-id="cee64-151">string</span></span> | <span data-ttu-id="cee64-152">Да</span><span class="sxs-lookup"><span data-stu-id="cee64-152">Yes</span></span> | <span data-ttu-id="cee64-153">Идентификатор собрания можно получить с помощью вызова Bot и клиента Teams SDK Teams.</span><span class="sxs-lookup"><span data-stu-id="cee64-153">The meeting identifier is available via Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="cee64-154">**партиЦипантид**</span><span class="sxs-lookup"><span data-stu-id="cee64-154">**participantId**</span></span>| <span data-ttu-id="cee64-155">string</span><span class="sxs-lookup"><span data-stu-id="cee64-155">string</span></span> | <span data-ttu-id="cee64-156">Да</span><span class="sxs-lookup"><span data-stu-id="cee64-156">Yes</span></span> | <span data-ttu-id="cee64-157">Это поле является ИДЕНТИФИКАТОРом пользователя и доступно в разделе SSO, вызове Bot и пакете SDK Teams.</span><span class="sxs-lookup"><span data-stu-id="cee64-157">This field is the User ID and it is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="cee64-158">Настоятельно рекомендуется использовать единый вход.</span><span class="sxs-lookup"><span data-stu-id="cee64-158">Tab SSO is highly recommended</span></span>|
|<span data-ttu-id="cee64-159">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="cee64-159">**tenantId**</span></span>| <span data-ttu-id="cee64-160">string</span><span class="sxs-lookup"><span data-stu-id="cee64-160">string</span></span> | <span data-ttu-id="cee64-161">Да</span><span class="sxs-lookup"><span data-stu-id="cee64-161">Yes</span></span> | <span data-ttu-id="cee64-162">Это необходимо для пользователей клиента.</span><span class="sxs-lookup"><span data-stu-id="cee64-162">This required for tenant users.</span></span> <span data-ttu-id="cee64-163">Он доступен при вводе-вызываемой клавишей TAB, с использованием ленты и клиента Teams SDK.</span><span class="sxs-lookup"><span data-stu-id="cee64-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="cee64-164">Настоятельно рекомендуется использовать единый вход.</span><span class="sxs-lookup"><span data-stu-id="cee64-164">Tab SSO is highly recommended</span></span>|

#### <a name="response-payload"></a><span data-ttu-id="cee64-165">Полезные данные ответа</span><span class="sxs-lookup"><span data-stu-id="cee64-165">Response Payload</span></span>
<!-- markdownlint-disable MD036 -->

<span data-ttu-id="cee64-166">**роль** в разделе "собрание" может быть *организатором*, *докладчиком* или *участником*.</span><span class="sxs-lookup"><span data-stu-id="cee64-166">**role** under "meeting" can be *Organizer*, *Presenter*, or *Attendee*.</span></span>

<span data-ttu-id="cee64-167">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="cee64-167">**Example 1**</span></span>

```json
{
  "user":
  {
      "id": "29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId": "6aebbad0-e5a5-424a-834a-20fb051f3c1a",
      "name": "Allan Deyoung",
      "givenName": "Allan",
      "surname": "Deyoung",
      "email": "Allan.Deyoung@microsoft.com",
      "userPrincipalName": "Allan.Deyoung@microsoft.com",
      "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
      "userRole": "user"
  },
  "meeting":
  {
      "role ": "Presenter",
      "inMeeting":true
  },
  "conversation":
  {
      "id": "<conversation id>"
  }
}
```
#### <a name="response-codes"></a><span data-ttu-id="cee64-168">Коды ответов</span><span class="sxs-lookup"><span data-stu-id="cee64-168">Response Codes</span></span>

<span data-ttu-id="cee64-169">**403**: приложению не разрешено получать сведения об участнике.</span><span class="sxs-lookup"><span data-stu-id="cee64-169">**403**: The app is not allowed to get participant information.</span></span> <span data-ttu-id="cee64-170">Это наиболее распространенный ответ об ошибке, который активируется, когда приложение не установлено на собрании, например, когда оно отключено администратором клиента или блокируется во время миграции Live site.</span><span class="sxs-lookup"><span data-stu-id="cee64-170">This will be the most common error response and is triggered when the app is not installed in the meeting such as when it is disabled by tenant admin or blocked during live site migration.</span></span>  
<span data-ttu-id="cee64-171">**200**: сведения о участниках успешно получены.</span><span class="sxs-lookup"><span data-stu-id="cee64-171">**200**: Participant information successfully retrieved.</span></span>  
<span data-ttu-id="cee64-172">**401**: недопустимый маркер.</span><span class="sxs-lookup"><span data-stu-id="cee64-172">**401**: Invalid token.</span></span>  
<span data-ttu-id="cee64-173">**404**: не удается найти участника.</span><span class="sxs-lookup"><span data-stu-id="cee64-173">**404**: Participant cannot be found.</span></span> 
<span data-ttu-id="cee64-174">**500**: срок действия собрания истечет (более 60 дней с момента завершения собрания), или у участника нет разрешений на основе их роли.</span><span class="sxs-lookup"><span data-stu-id="cee64-174">**500**: The meeting is either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>

<span data-ttu-id="cee64-175">**Ожидается в ближайшее время**</span><span class="sxs-lookup"><span data-stu-id="cee64-175">**Coming Soon**</span></span>

<span data-ttu-id="cee64-176">**404**: срок действия собрания истек или участник не может быть найден.</span><span class="sxs-lookup"><span data-stu-id="cee64-176">**404**: the meeting has either expired or participant cannot be found.</span></span> 

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a><span data-ttu-id="cee64-177">API Нотификатионсигнал</span><span class="sxs-lookup"><span data-stu-id="cee64-177">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="cee64-178">Когда вызывается диалоговое окно для собраний, то то же самое содержимое также будет представлено в виде сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="cee64-178">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="request"></a><span data-ttu-id="cee64-179">Запрос</span><span class="sxs-lookup"><span data-stu-id="cee64-179">Request</span></span>

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a><span data-ttu-id="cee64-180">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="cee64-180">Query parameters</span></span>

|<span data-ttu-id="cee64-181">Value</span><span class="sxs-lookup"><span data-stu-id="cee64-181">Value</span></span>|<span data-ttu-id="cee64-182">Тип</span><span class="sxs-lookup"><span data-stu-id="cee64-182">Type</span></span>|<span data-ttu-id="cee64-183">Обязательный</span><span class="sxs-lookup"><span data-stu-id="cee64-183">Required</span></span>|<span data-ttu-id="cee64-184">Описание</span><span class="sxs-lookup"><span data-stu-id="cee64-184">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="cee64-185">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="cee64-185">**conversationId**</span></span>| <span data-ttu-id="cee64-186">string</span><span class="sxs-lookup"><span data-stu-id="cee64-186">string</span></span> | <span data-ttu-id="cee64-187">Да</span><span class="sxs-lookup"><span data-stu-id="cee64-187">Yes</span></span> | <span data-ttu-id="cee64-188">Идентификатор беседы доступен в составе вызова по методу Bot</span><span class="sxs-lookup"><span data-stu-id="cee64-188">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="request-payload"></a><span data-ttu-id="cee64-189">Полезные данные запроса</span><span class="sxs-lookup"><span data-stu-id="cee64-189">Request Payload</span></span>

> [!NOTE]
>
> *  <span data-ttu-id="cee64-190">В приведенных ниже полезных полезных данных `completionBotId` параметр `externalResourceUrl` является необязательным.</span><span class="sxs-lookup"><span data-stu-id="cee64-190">In the requested payload below, the `completionBotId` parameter of the `externalResourceUrl`is an optional.</span></span> <span data-ttu-id="cee64-191">Это то `Bot ID` , что объявлено в манифесте.</span><span class="sxs-lookup"><span data-stu-id="cee64-191">It is the `Bot ID` that is declared in the manifest.</span></span> <span data-ttu-id="cee64-192">Bot получит объект Result.</span><span class="sxs-lookup"><span data-stu-id="cee64-192">The bot will receive a result object.</span></span>
> * <span data-ttu-id="cee64-193">Параметры ширины и высоты Екстерналресаурцеурл должны находиться в точках.</span><span class="sxs-lookup"><span data-stu-id="cee64-193">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="cee64-194">Ознакомьтесь с [рекомендациями по проектированию](design/designing-in-meeting-dialog.md) , чтобы убедиться в том, что размеры находятся в пределах допустимых пределов.</span><span class="sxs-lookup"><span data-stu-id="cee64-194">Refer to the [design guidelines](design/designing-in-meeting-dialog.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="cee64-195">URL-адрес — это страница, загруженная в `<iframe>` диалоговом окне для собраний.</span><span class="sxs-lookup"><span data-stu-id="cee64-195">The URL is the page loaded as an `<iframe>` inside the in-meeting dialog.</span></span> <span data-ttu-id="cee64-196">Домен URL-адреса должен находиться в `validDomains` массиве приложения в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="cee64-196">The URL's domain must be in the app's `validDomains` array in your app manifest.</span></span>


# <a name="json"></a>[<span data-ttu-id="cee64-197">JSON</span><span class="sxs-lookup"><span data-stu-id="cee64-197">JSON</span></span>](#tab/json)

```json
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

# <a name="cnet"></a>[<span data-ttu-id="cee64-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cee64-198">C#/.NET</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
  {
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
  };
activity.ChannelData = new TeamsChannelData
  {
    Notification = notification
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="cee64-199">JavaScript</span><span class="sxs-lookup"><span data-stu-id="cee64-199">JavaScript</span></span>](#tab/javascript)

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

* * *

> [!IMPORTANT]
> <span data-ttu-id="cee64-200">URL-адрес в пузырьке содержимого (URL-адрес Таскинфо) должен быть включен в список [допустимых доменов](../resources/schema/manifest-schema.md#validdomains) , включенный в манифест приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="cee64-200">The URL in the content bubble (taskInfo URL) must be included in the [valid domains](../resources/schema/manifest-schema.md#validdomains) list included in the Teams app manifest.</span></span>

#### <a name="response-codes"></a><span data-ttu-id="cee64-201">Коды ответов</span><span class="sxs-lookup"><span data-stu-id="cee64-201">Response Codes</span></span>

<span data-ttu-id="cee64-202">**201**: действие с сигналом успешно отправлено</span><span class="sxs-lookup"><span data-stu-id="cee64-202">**201**: activity with signal is successfully sent</span></span>  
<span data-ttu-id="cee64-203">**401**: недопустимый маркер</span><span class="sxs-lookup"><span data-stu-id="cee64-203">**401**: invalid token</span></span>  
<span data-ttu-id="cee64-204">**403**: приложению не разрешено отправлять сигнал.</span><span class="sxs-lookup"><span data-stu-id="cee64-204">**403**: the app is not allowed to send the signal.</span></span> <span data-ttu-id="cee64-205">В этом случае полезная нагрузка должна содержать более подробное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="cee64-205">In this case, the payload should contain more detail error message.</span></span> <span data-ttu-id="cee64-206">Может быть несколько причин: приложение отключено администратором клиента, заблокировано во время снижения риска на сайте Live и т. д.</span><span class="sxs-lookup"><span data-stu-id="cee64-206">There can be many reasons: app disabled by tenant admin, blocked during live site mitigation, etc.</span></span>  
<span data-ttu-id="cee64-207">**404**: чат для собрания не существует</span><span class="sxs-lookup"><span data-stu-id="cee64-207">**404**: meeting chat doesn't exist</span></span>  

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="cee64-208">Включение собраний для приложений в Teams</span><span class="sxs-lookup"><span data-stu-id="cee64-208">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="cee64-209">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="cee64-209">Update your app manifest</span></span>

<span data-ttu-id="cee64-210">Возможности приложений для собраний объявляются в манифесте приложения с **configurableTabs** помощью  ->  **областей** конфигураблетабс и **контекстных** массивов.</span><span class="sxs-lookup"><span data-stu-id="cee64-210">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="cee64-211">*Область* определяет, для кого и *контекст* определяет, где будет доступно ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="cee64-211">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> * <span data-ttu-id="cee64-212">Используйте [схему манифеста Preview для разработчиков](../resources/schema/manifest-schema-dev-preview.md) , чтобы попробовать это в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="cee64-212">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="cee64-213">Свойство Context</span><span class="sxs-lookup"><span data-stu-id="cee64-213">Context property</span></span>

<span data-ttu-id="cee64-214">Вкладка `context` и `scopes` свойства работают по гармонии, чтобы определить, где должно отображаться ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="cee64-214">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="cee64-215">Вкладки в `team` `groupchat` области действия могут иметь более одного контекста.</span><span class="sxs-lookup"><span data-stu-id="cee64-215">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="cee64-216">Для свойства Context возможны следующие значения:</span><span class="sxs-lookup"><span data-stu-id="cee64-216">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="cee64-217">**чаннелтаб**: вкладка в заголовке канала команды.</span><span class="sxs-lookup"><span data-stu-id="cee64-217">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="cee64-218">**приватечаттаб**: вкладка в заголовке группового чата между набором пользователей, которых нет в контексте команды или собрания.</span><span class="sxs-lookup"><span data-stu-id="cee64-218">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="cee64-219">**митингчаттаб**: вкладка в заголовке группового чата между набором пользователей в контексте запланированного собрания.</span><span class="sxs-lookup"><span data-stu-id="cee64-219">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="cee64-220">**митингдетаилстаб**: вкладка в заголовке представления сведений о собрании календаря.</span><span class="sxs-lookup"><span data-stu-id="cee64-220">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="cee64-221">**митингсидепанел**: панель для собраний, открытая с помощью унифицированной панели (u-борта).</span><span class="sxs-lookup"><span data-stu-id="cee64-221">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="cee64-222">В настоящее время свойство "Context" в настоящее время не поддерживается и поэтому будет игнорироваться на мобильных клиентах</span><span class="sxs-lookup"><span data-stu-id="cee64-222">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="cee64-223">Настройка приложения для сценариев собраний</span><span class="sxs-lookup"><span data-stu-id="cee64-223">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="cee64-224">Чтобы ваше приложение отображалось в коллекции вкладок, оно должно **поддерживать настраиваемые вкладки** и **область применения группового чата**.</span><span class="sxs-lookup"><span data-stu-id="cee64-224">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="cee64-225">Мобильные клиенты поддерживают вкладки только на поверхностях предварительных и посылаемых собраний.</span><span class="sxs-lookup"><span data-stu-id="cee64-225">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="cee64-226">Скоро будет доступен интерфейс для собраний (диалоговое окно и панель на собрании) на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="cee64-226">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon.</span></span> <span data-ttu-id="cee64-227">Следуйте [указаниям по использованию вкладок на мобильном устройстве](../tabs/design/tabs-mobile.md) при создании вкладок для мобильного устройства.</span><span class="sxs-lookup"><span data-stu-id="cee64-227">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span> 

### <a name="pre-meeting"></a><span data-ttu-id="cee64-228">Предварительное собрание</span><span class="sxs-lookup"><span data-stu-id="cee64-228">Pre-meeting</span></span>

<span data-ttu-id="cee64-229">Пользователи с ролями органайзера и докладчика добавляют вкладки на собрание с помощью кнопки "плюс ➕" в разделе " **беседы** для собраний" и " **сведения о** собрании".</span><span class="sxs-lookup"><span data-stu-id="cee64-229">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="cee64-230">Расширения обмена сообщениями добавляются в меню "многоточия/переполнение" &#x25CF;&#x25CF;&#x25CF; , расположенного под областью создание сообщения в чате.</span><span class="sxs-lookup"><span data-stu-id="cee64-230">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="cee64-231">Боты добавляются в чат для собрания с помощью **@** ключа "" и выбора **Get Боты**.</span><span class="sxs-lookup"><span data-stu-id="cee64-231">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="cee64-232">✔ Удостоверение пользователя *должно* быть подтверждено с помощью [единого входа вкладок](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="cee64-232">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="cee64-233">После проверки подлинности приложение может получить роль пользователя через API-участник.</span><span class="sxs-lookup"><span data-stu-id="cee64-233">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="cee64-234">✔ На основе роли пользователя, приложение теперь будет иметь возможность для отображения специальных интерфейсов для ролей.</span><span class="sxs-lookup"><span data-stu-id="cee64-234">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="cee64-235">Например, приложение опроса может разрешить только организаторов и докладчикам создавать новый опрос.</span><span class="sxs-lookup"><span data-stu-id="cee64-235">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="cee64-236">**Note**: назначения ролей могут быть изменены во время собрания.</span><span class="sxs-lookup"><span data-stu-id="cee64-236">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="cee64-237">*Просмотр* [ролей в собрании Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="cee64-237">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="in-meeting"></a><span data-ttu-id="cee64-238">На собрании</span><span class="sxs-lookup"><span data-stu-id="cee64-238">In-meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="cee64-239">**сидепанел**</span><span class="sxs-lookup"><span data-stu-id="cee64-239">**sidePanel**</span></span>

<span data-ttu-id="cee64-240">✔ В манифесте приложения добавьте **сидепанел** в массив **контекста** , как описано выше.</span><span class="sxs-lookup"><span data-stu-id="cee64-240">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="cee64-241">✔ На собрании, так же, как и во всех сценариях, приложение будет отображаться на вкладке, расположенной в собрании, 320 пикселей по ширине.</span><span class="sxs-lookup"><span data-stu-id="cee64-241">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="cee64-242">Для этого необходимо оптимизировать вкладку.</span><span class="sxs-lookup"><span data-stu-id="cee64-242">Your tab must be optimized for this.</span></span> <span data-ttu-id="cee64-243">*Просмотр*, [интерфейс фрамеконтекст](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="cee64-243">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="cee64-244">✔ Ссылаться на [пакет SDK Teams](../tabs/how-to/access-teams-context.md#user-context) , чтобы использовать API **UserContext** для соответствующей маршрутизации запросов.</span><span class="sxs-lookup"><span data-stu-id="cee64-244">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="cee64-245">✔ Ссылаться на [процесс проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="cee64-245">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="cee64-246">Процесс проверки подлинности для вкладок очень похож на процесс проверки подлинности для веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="cee64-246">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="cee64-247">Таким образом, вкладки могут напрямую использовать OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="cee64-247">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="cee64-248">*Кроме того, можно просмотреть* [потоки кода авторизации для платформы Microsoft identity и OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="cee64-248">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="cee64-249">Расширение сообщения ✔ должно работать должным образом, если пользователь находится в представлении собраний, и должен иметь возможность отправлять карточки расширения сообщения.</span><span class="sxs-lookup"><span data-stu-id="cee64-249">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="cee64-250">✔ AppName in to Meeting — всплывающая подсказка должна указать имя приложения в панели U для собраний.</span><span class="sxs-lookup"><span data-stu-id="cee64-250">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="cee64-251">**диалоговое окно "в собрании"**</span><span class="sxs-lookup"><span data-stu-id="cee64-251">**in-meeting dialog**</span></span>

<span data-ttu-id="cee64-252">✔ Необходимо следовать [рекомендациям по разработке диалоговых окон для собраний](design/designing-in-meeting-dialog.md).</span><span class="sxs-lookup"><span data-stu-id="cee64-252">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-in-meeting-dialog.md).</span></span>

<span data-ttu-id="cee64-253">✔ Ссылаться на [процесс проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="cee64-253">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="cee64-254">✔ Использовать API [уведомлений](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) для сигнализации о необходимости запуска пузырькового уведомления.</span><span class="sxs-lookup"><span data-stu-id="cee64-254">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="cee64-255">✔ Как часть полезных данных запроса уведомления, укажите URL-адрес, по которому размещается контент, предназначенный для демонстрации.</span><span class="sxs-lookup"><span data-stu-id="cee64-255">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="cee64-256">✔ Диалоговое окно для собраний не должно использовать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="cee64-256">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="cee64-257">Эти уведомления постоянны.</span><span class="sxs-lookup"><span data-stu-id="cee64-257">These notifications are persistent in nature.</span></span> <span data-ttu-id="cee64-258">Необходимо вызвать функцию [**субмиттаск ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического закрытия после того, как пользователь выполняет действие в веб-представлении.</span><span class="sxs-lookup"><span data-stu-id="cee64-258">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="cee64-259">Это требование для отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="cee64-259">This is a requirement for app submission.</span></span> <span data-ttu-id="cee64-260">*Раздел* [пакет SDK для teams: Task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="cee64-260">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="cee64-261">Если вы хотите, чтобы приложение поддерживало анонимных пользователей, полезные данные начального запроса вызова должны полагаться на `from.id`  метаданные запроса (ID пользователя) в `from` объекте, а не на `from.aadObjectId` метаданные запроса (идентификатор Azure Active Directory для пользователя).</span><span class="sxs-lookup"><span data-stu-id="cee64-261">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="cee64-262">*Просмотрите раздел* [Использование модулей задач на вкладках](../task-modules-and-cards/task-modules/task-modules-tabs.md) и [Создайте и отправьте модуль задач](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span><span class="sxs-lookup"><span data-stu-id="cee64-262">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="post-meeting"></a><span data-ttu-id="cee64-263">Завершающее собрание</span><span class="sxs-lookup"><span data-stu-id="cee64-263">Post-meeting</span></span>

<span data-ttu-id="cee64-264">Конфигурации после собрания и предварительного собрания эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="cee64-264">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="cee64-265">Пример приложения для собраний</span><span class="sxs-lookup"><span data-stu-id="cee64-265">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="cee64-266">Приложение генератора маркеров собраний</span><span class="sxs-lookup"><span data-stu-id="cee64-266">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
