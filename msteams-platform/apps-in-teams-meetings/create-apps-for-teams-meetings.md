---
title: Создание приложений для собраний групп
author: laujan
description: создание приложений для собраний групп
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: команды приложений встречи пользователь участник роль api
ms.openlocfilehash: 84d0f5564d7e8e6e34dde1f3d59cc6e7a68d3332
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565916"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="c0c6c-104">Создание приложений для собраний Teams</span><span class="sxs-lookup"><span data-stu-id="c0c6c-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="c0c6c-105">Предпосылки и соображения</span><span class="sxs-lookup"><span data-stu-id="c0c6c-105">Prerequisites and considerations</span></span>

<span data-ttu-id="c0c6c-106">Прежде чем создавать приложения Teams собраний, необходимо иметь представление о следующем:</span><span class="sxs-lookup"><span data-stu-id="c0c6c-106">Before you create apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="c0c6c-107">Вы должны иметь знания о том, как Teams приложений.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-107">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="c0c6c-108">Для получения дополнительной информации [с Teams м.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-108">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="c0c6c-109">Необходимо обновить манифест Teams, чтобы указать, что приложение доступно для встреч.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-109">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="c0c6c-110">Для получения дополнительной информации [см.](#update-your-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-110">For more information, see [app manifest](#update-your-app-manifest).</span></span>

* <span data-ttu-id="c0c6c-111">Для того чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки, оно должно поддерживать настраиваемые вкладки в области группового чата.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-111">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the groupchat scope.</span></span> <span data-ttu-id="c0c6c-112">Для получения дополнительной информации [можно просмотреть область группового](../resources/schema/manifest-schema.md#configurabletabs) [чата и создать вкладку группы.](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-112">For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="c0c6c-113">Необходимо придерживаться общих Teams разработке вкладок для сценариев предварительного и после собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-113">You must adhere to general Teams tab design guidelines for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="c0c6c-114">Для получения опыта во время встреч обратитесь к вкладке в заседании и рекомендациям по проектированию диалогов на совещании.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-114">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="c0c6c-115">Для получения дополнительной информации [см. Teams руководства по проектированию вкладок,](../tabs/design/tabs.md) [рекомендации по проектированию вкладок](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) на совещании [и рекомендации по проектированию диалоговых диалогов.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-115">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="c0c6c-116">Необходимо поддерживать область `groupchat` действия приложения в чатах перед встречей и после собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-116">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="c0c6c-117">С помощью приложения перед встречей можно найти и добавить приложения для встреч и выполнить задачи перед встречей.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-117">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="c0c6c-118">С помощью приложения после собрания можно просматривать результаты собрания, такие как результаты опроса или отзывы.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-118">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="c0c6c-119">Совещание параметров URL API должно `meetingId` `userId` иметь, и `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="c0c6c-119">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="c0c6c-120">Они доступны в рамках программы Teams SDK и бота.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-120">These are available as part of the Teams client SDK and bot activity.</span></span> <span data-ttu-id="c0c6c-121">Кроме того, надежную информацию для идентификатора пользователя и идентификатора клиента можно получить с помощью [проверки подлинности Tab SSO.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-121">In addition, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="c0c6c-122">API `GetParticipant` должен иметь регистрацию бота и ID для создания токенов auth.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-122">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="c0c6c-123">Для получения дополнительной информации, [см.](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-123">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="c0c6c-124">Для обновления приложения в режиме реального времени оно должно быть обновлено на основе событий на собрании.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-124">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="c0c6c-125">Эти события могут быть в поле диалога на встрече и на других этапах жизненного цикла собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-125">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="c0c6c-126">Для окна диалога на встрече см. `bot Id` `Notification Signal API`</span><span class="sxs-lookup"><span data-stu-id="c0c6c-126">For the in-meeting dialog box, see completion `bot Id` parameter in `Notification Signal API`.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="c0c6c-127">Совещание приложений API ссылки</span><span class="sxs-lookup"><span data-stu-id="c0c6c-127">Meeting apps API reference</span></span>

|<span data-ttu-id="c0c6c-128">API</span><span class="sxs-lookup"><span data-stu-id="c0c6c-128">API</span></span>|<span data-ttu-id="c0c6c-129">Описание</span><span class="sxs-lookup"><span data-stu-id="c0c6c-129">Description</span></span>|<span data-ttu-id="c0c6c-130">Запрос</span><span class="sxs-lookup"><span data-stu-id="c0c6c-130">Request</span></span>|<span data-ttu-id="c0c6c-131">Источник</span><span class="sxs-lookup"><span data-stu-id="c0c6c-131">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="c0c6c-132">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-132">**GetUserContext**</span></span>| <span data-ttu-id="c0c6c-133">Этот API позволяет получать контекстную информацию для отображения соответствующего контента в Teams вкладке.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-133">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="c0c6c-134">_**microsoftTeams.getContext (>) / } )**_</span><span class="sxs-lookup"><span data-stu-id="c0c6c-134">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="c0c6c-135">Microsoft Teams клиент SDK</span><span class="sxs-lookup"><span data-stu-id="c0c6c-135">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="c0c6c-136">**ПолучитьПартийный**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-136">**GetParticipant**</span></span>| <span data-ttu-id="c0c6c-137">Этот API позволяет боту получать информацию об участниках, вевея идентификатор и идентификатор участника.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-137">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="c0c6c-138">**GET** _**/v1/meetings/«meetingId»/участники/«участникИ?арендаторИдеантия»**_</span><span class="sxs-lookup"><span data-stu-id="c0c6c-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="c0c6c-139">Microsoft Bot Framework СДК</span><span class="sxs-lookup"><span data-stu-id="c0c6c-139">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="c0c6c-140">**УведомлениеСгальный**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-140">**NotificationSignal**</span></span> | <span data-ttu-id="c0c6c-141">Этот API позволяет предоставлять сигналы собрания, которые доставляются с помощью существующего API уведомления о разговоре для чата пользователя-бота.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-141">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="c0c6c-142">Это позволяет сигнализировать на основе действий пользователя, который показывает в заседании диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-142">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="c0c6c-143">**POST** _**/v3/разговоры/РазговорИде/деятельность**_</span><span class="sxs-lookup"><span data-stu-id="c0c6c-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="c0c6c-144">Microsoft Bot Framework СДК</span><span class="sxs-lookup"><span data-stu-id="c0c6c-144">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="c0c6c-145">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="c0c6c-145">GetUserContext</span></span>

<span data-ttu-id="c0c6c-146">Чтобы определить и получить контекстную информацию для содержимого вкладки, [смотрите контекст для вашей вкладки Teams вкладку.](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) `meetingId`используется вкладкой при запуске в контексте собрания и добавляется для полезной нагрузки ответа.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-146">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="c0c6c-147">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="c0c6c-147">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="c0c6c-148">Не кэшировать роли участников, так как организатор собрания может изменить роль в любое время.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-148">Do not cache participant roles since the meeting organizer can change a role any time.</span></span>
> * <span data-ttu-id="c0c6c-149">Teams в настоящее время не поддерживает большие списки рассылки или реестр размеров более 350 участников для `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-149">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="c0c6c-150">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="c0c6c-150">Query parameters</span></span>

|<span data-ttu-id="c0c6c-151">Значение</span><span class="sxs-lookup"><span data-stu-id="c0c6c-151">Value</span></span>|<span data-ttu-id="c0c6c-152">Тип</span><span class="sxs-lookup"><span data-stu-id="c0c6c-152">Type</span></span>|<span data-ttu-id="c0c6c-153">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0c6c-153">Required</span></span>|<span data-ttu-id="c0c6c-154">Описание</span><span class="sxs-lookup"><span data-stu-id="c0c6c-154">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="c0c6c-155">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-155">**meetingId**</span></span>| <span data-ttu-id="c0c6c-156">string</span><span class="sxs-lookup"><span data-stu-id="c0c6c-156">string</span></span> | <span data-ttu-id="c0c6c-157">Да</span><span class="sxs-lookup"><span data-stu-id="c0c6c-157">Yes</span></span> | <span data-ttu-id="c0c6c-158">Идентификатор собрания доступен через Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-158">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="c0c6c-159">**участникИ**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-159">**participantId**</span></span>| <span data-ttu-id="c0c6c-160">string</span><span class="sxs-lookup"><span data-stu-id="c0c6c-160">string</span></span> | <span data-ttu-id="c0c6c-161">Да</span><span class="sxs-lookup"><span data-stu-id="c0c6c-161">Yes</span></span> | <span data-ttu-id="c0c6c-162">Идентификатор участника является идентификатором пользователя.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-162">The participant ID is the user ID.</span></span> <span data-ttu-id="c0c6c-163">Он доступен в Tab SSO, Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="c0c6c-164">Рекомендуется получить идентификатор участника из Tab SSO.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-164">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="c0c6c-165">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-165">**tenantId**</span></span>| <span data-ttu-id="c0c6c-166">string</span><span class="sxs-lookup"><span data-stu-id="c0c6c-166">string</span></span> | <span data-ttu-id="c0c6c-167">Да</span><span class="sxs-lookup"><span data-stu-id="c0c6c-167">Yes</span></span> | <span data-ttu-id="c0c6c-168">Идентификатор арендатора требуется пользователям-арендаторам.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-168">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="c0c6c-169">Он доступен в Tab SSO, Bot Invoke и Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-169">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="c0c6c-170">Рекомендуется получить идентификатор арендатора в Tab SSO.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-170">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="c0c6c-171">Пример</span><span class="sxs-lookup"><span data-stu-id="c0c6c-171">Example</span></span>

# <a name="c"></a>[<span data-ttu-id="c0c6c-172">C#</span><span class="sxs-lookup"><span data-stu-id="c0c6c-172">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="c0c6c-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="c0c6c-173">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="c0c6c-174">JSON</span><span class="sxs-lookup"><span data-stu-id="c0c6c-174">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="c0c6c-175">Орган реагирования JSON `GetParticipant` для API:</span><span class="sxs-lookup"><span data-stu-id="c0c6c-175">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="c0c6c-176">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="c0c6c-176">Response codes</span></span>

|<span data-ttu-id="c0c6c-177">Код ответа</span><span class="sxs-lookup"><span data-stu-id="c0c6c-177">Response code</span></span>|<span data-ttu-id="c0c6c-178">Описание</span><span class="sxs-lookup"><span data-stu-id="c0c6c-178">Description</span></span>|
|---|---|
| <span data-ttu-id="c0c6c-179">**403**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-179">**403**</span></span> | <span data-ttu-id="c0c6c-180">Приложение не имеет права получать информацию о участнике.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-180">The app is not allowed to get participant information.</span></span> <span data-ttu-id="c0c6c-181">Это наиболее распространенный ответ на ошибку и срабатывает, если приложение не установлено на собрании.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-181">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="c0c6c-182">Например, если приложение отключено администратором-арендатором или заблокировано во время миграции живого сайта.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-182">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="c0c6c-183">**200**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-183">**200**</span></span> | <span data-ttu-id="c0c6c-184">Информация об участнике успешно извлекается.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-184">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="c0c6c-185">**401**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-185">**401**</span></span> | <span data-ttu-id="c0c6c-186">Приложение отвечает недействительным маркером.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-186">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="c0c6c-187">**404**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-187">**404**</span></span> | <span data-ttu-id="c0c6c-188">Заседание либо истекло, либо участник не может быть найден.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-188">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="c0c6c-189">**500**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-189">**500**</span></span> | <span data-ttu-id="c0c6c-190">Срок действия собрания либо истек более чем на 60 дней с момента окончания собрания, либо у участника нет разрешений, основанных на его роли.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-190">The meeting has either expired more than 60 days since the meeting ended or the participant does not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="c0c6c-191">УведомлениеСеньальный API</span><span class="sxs-lookup"><span data-stu-id="c0c6c-191">NotificationSignal API</span></span>

<span data-ttu-id="c0c6c-192">Все пользователи на собрании получают уведомления, отправленные через `NotificationSignal` API.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-192">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="c0c6c-193">При вызываемом диалоговом поле на собрании содержимое представляется как сообщение чата.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-193">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="c0c6c-194">В настоящее время отправка целевых уведомлений не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-194">Currently, sending targeted notifications is not supported.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="c0c6c-195">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="c0c6c-195">Query parameters</span></span>

|<span data-ttu-id="c0c6c-196">Значение</span><span class="sxs-lookup"><span data-stu-id="c0c6c-196">Value</span></span>|<span data-ttu-id="c0c6c-197">Тип</span><span class="sxs-lookup"><span data-stu-id="c0c6c-197">Type</span></span>|<span data-ttu-id="c0c6c-198">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0c6c-198">Required</span></span>|<span data-ttu-id="c0c6c-199">Описание</span><span class="sxs-lookup"><span data-stu-id="c0c6c-199">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="c0c6c-200">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-200">**conversationId**</span></span>| <span data-ttu-id="c0c6c-201">string</span><span class="sxs-lookup"><span data-stu-id="c0c6c-201">string</span></span> | <span data-ttu-id="c0c6c-202">Да</span><span class="sxs-lookup"><span data-stu-id="c0c6c-202">Yes</span></span> | <span data-ttu-id="c0c6c-203">Идентификатор разговора доступен как часть вызова бота.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-203">The conversation identifier is available as part of bot invoke.</span></span> |

#### <a name="example"></a><span data-ttu-id="c0c6c-204">Пример</span><span class="sxs-lookup"><span data-stu-id="c0c6c-204">Example</span></span>

<span data-ttu-id="c0c6c-205">Объявлен `Bot ID` в манифесте и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-205">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="c0c6c-206">Параметр `completionBotId` не является обязательным в `externalResourceUrl` запрошенном примере полезной нагрузки.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-206">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="c0c6c-207">`Bot ID` объявляется в манифесте, и бот получает объект результата.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-207">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="c0c6c-208">Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-208">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="c0c6c-209">Чтобы убедиться, что размеры находятся в пределах разрешенных пределов, [см.](design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-209">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="c0c6c-210">URL-адрес — это страница, загруженная `<iframe>` в диалоговое окно во время встречи.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-210">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="c0c6c-211">Домен должен быть в массиве приложения в `validDomains` манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-211">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="c"></a>[<span data-ttu-id="c0c6c-212">C#</span><span class="sxs-lookup"><span data-stu-id="c0c6c-212">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="c0c6c-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="c0c6c-213">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="c0c6c-214">JSON</span><span class="sxs-lookup"><span data-stu-id="c0c6c-214">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="c0c6c-215">Коды ответа</span><span class="sxs-lookup"><span data-stu-id="c0c6c-215">Response codes</span></span>

|<span data-ttu-id="c0c6c-216">Код ответа</span><span class="sxs-lookup"><span data-stu-id="c0c6c-216">Response code</span></span>|<span data-ttu-id="c0c6c-217">Описание</span><span class="sxs-lookup"><span data-stu-id="c0c6c-217">Description</span></span>|
|---|---|
| <span data-ttu-id="c0c6c-218">**201**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-218">**201**</span></span> | <span data-ttu-id="c0c6c-219">Деятельность с сигналом успешно отправляется.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-219">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="c0c6c-220">**401**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-220">**401**</span></span> | <span data-ttu-id="c0c6c-221">Приложение отвечает недействительным маркером.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-221">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="c0c6c-222">**403**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-222">**403**</span></span> | <span data-ttu-id="c0c6c-223">Приложение не может послать сигнал.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-223">The app is unable to send the signal.</span></span> <span data-ttu-id="c0c6c-224">Это может произойти по разным причинам, таким как администратор-арендатор отключает приложение, приложение блокируется во время миграции живого сайта и так далее.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-224">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="c0c6c-225">В этом случае полезная нагрузка содержит подробное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-225">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="c0c6c-226">**404**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-226">**404**</span></span> | <span data-ttu-id="c0c6c-227">Чат собрания не существует.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-227">The meeting chat does not exist.</span></span> |

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="c0c6c-228">Включить приложение для Teams собраний</span><span class="sxs-lookup"><span data-stu-id="c0c6c-228">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="c0c6c-229">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="c0c6c-229">Update your app manifest</span></span>

<span data-ttu-id="c0c6c-230">Возможности приложения для собраний заявлены в манифесте приложения `configurableTabs` с `scopes` использованием `context` массивов и массивов.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-230">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="c0c6c-231">Область данных определяет, кому и контекст определяет, где доступно ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-231">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> <span data-ttu-id="c0c6c-232">Попробуйте обновить манифест приложения с помощью [явной схемы.](../resources/schema/manifest-schema-dev-preview.md)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-232">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> <span data-ttu-id="c0c6c-233">Приложения на собраниях нуждаются в *сфере группового* чата.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-233">Apps in meetings need *groupchat* scope.</span></span> <span data-ttu-id="c0c6c-234">Область *действия* команды работает только для вкладок в каналах.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-234">The *team* scope works for tabs in channels only.</span></span>

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
> <span data-ttu-id="c0c6c-235">`meetingStage` в настоящее время доступна только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-235">`meetingStage` is currently available in developer preview only.</span></span>

### <a name="context-property"></a><span data-ttu-id="c0c6c-236">Свойство контекста</span><span class="sxs-lookup"><span data-stu-id="c0c6c-236">Context property</span></span>

<span data-ttu-id="c0c6c-237">Вкладка `context` и `scopes` свойства позволяют определить, где должно отображаться ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-237">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="c0c6c-238">Вкладки в `team` области или области могут иметь несколько `groupchat` контекстов.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-238">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="c0c6c-239">Ниже приведены значения для `context` свойства, из которого можно использовать все или некоторые значения:</span><span class="sxs-lookup"><span data-stu-id="c0c6c-239">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="c0c6c-240">Значение</span><span class="sxs-lookup"><span data-stu-id="c0c6c-240">Value</span></span>|<span data-ttu-id="c0c6c-241">Описание</span><span class="sxs-lookup"><span data-stu-id="c0c6c-241">Description</span></span>|
|---|---|
| <span data-ttu-id="c0c6c-242">**каналТаб**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-242">**channelTab**</span></span> | <span data-ttu-id="c0c6c-243">Вкладка в заголовке командный канал.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-243">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="c0c6c-244">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-244">**privateChatTab**</span></span> | <span data-ttu-id="c0c6c-245">Вкладка в заголовке группового чата между набором пользователей не в контексте группы или собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-245">A tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="c0c6c-246">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-246">**meetingChatTab**</span></span> | <span data-ttu-id="c0c6c-247">Вкладка в заголовке группового чата между набором пользователей в контексте запланированного собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-247">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="c0c6c-248">**встречаДтейлТайлТаб**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-248">**meetingDetailsTab**</span></span> | <span data-ttu-id="c0c6c-249">Вкладка в заголовке представления деталей собрания календаря.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-249">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="c0c6c-250">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-250">**meetingSidePanel**</span></span> | <span data-ttu-id="c0c6c-251">Панель заседаний открылась через единый бар (U-bar).</span><span class="sxs-lookup"><span data-stu-id="c0c6c-251">An in-meeting panel opened via the unified bar (U-bar).</span></span> |
| <span data-ttu-id="c0c6c-252">**meetingStage**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-252">**meetingStage**</span></span> | <span data-ttu-id="c0c6c-253">Приложение с боковойпанеля может быть передано на стадию собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-253">An app from the sidepanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="c0c6c-254">`Context` недвижимость в настоящее время не поддерживается на мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-254">`Context` property is currently not supported on mobile clients.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="c0c6c-255">Настройка приложения для сценариев встреч</span><span class="sxs-lookup"><span data-stu-id="c0c6c-255">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="c0c6c-256">Чтобы ваше приложение было видно в галерее вкладок, оно должно поддерживать настраиваемые вкладки и область группового чата.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-256">For your app to be visible in the tab gallery it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="c0c6c-257">Мобильные клиенты поддерживают вкладки только на стадии предварительного и после собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-257">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="c0c6c-258">Опыт встречи, который является диалоговым окном и вкладкой на встрече, в настоящее время не поддерживается мобильными клиентами.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-258">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="c0c6c-259">Для получения дополнительной информации, [см. руководство для вкладок на мобильный](../tabs/design/tabs-mobile.md) при создании вкладок для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-259">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="c0c6c-260">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="c0c6c-260">Before a meeting</span></span>

<span data-ttu-id="c0c6c-261">Перед собранием пользователи могут добавлять вкладки, боты и расширения обмена сообщениями на собрание.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-261">Before a meeting, users can add tabs, bots and messaging extensions to a meeting.</span></span> <span data-ttu-id="c0c6c-262">Пользователи с ролями организатора и докладчика могут добавлять вкладки на собрание.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-262">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="c0c6c-263">**Добавление вкладки к собранию**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-263">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="c0c6c-264">В календаре выберите собрание, к которому вы хотите добавить вкладку.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-264">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="c0c6c-265">Выберите **вкладку Подробная** информация и выберите плюс</span><span class="sxs-lookup"><span data-stu-id="c0c6c-265">Select the **Details** tab and select plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="c0c6c-266">.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-266">.</span></span> <span data-ttu-id="c0c6c-267">Появляется галерея вкладок.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-267">The tab gallery appears.</span></span>

    ![Опыт предварительного собрания](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="c0c6c-269">В галерее вкладок выберите приложение, которое вы хотите добавить, и следуйте необходимым шагам.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-269">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="c0c6c-270">Приложение устанавливается в качестве вкладки.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-270">The app is installed as a tab.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="c0c6c-271">В настоящее время во вкладке заседаний получение информации о собраниях и участниках не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-271">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="c0c6c-272">**Добавление расширения обмена сообщениями на собрание**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-272">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="c0c6c-273">Выберите эллипсы или меню переполнения &#x25CF;&#x25CF;&#x25CF; , расположенных в области композиций сообщений в чате.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-273">Select the ellipses or overflow menu &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="c0c6c-274">Выберите приложение, которое вы хотите добавить, и следуйте необходимым шагам.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-274">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="c0c6c-275">Приложение устанавливается в качестве расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-275">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="c0c6c-276">**Добавление бота на собрание**</span><span class="sxs-lookup"><span data-stu-id="c0c6c-276">**To add a bot to a meeting**</span></span>

<span data-ttu-id="c0c6c-277">В чате собрания введите **@** ключ и выберите **Get bots**.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-277">In a meeting chat enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="c0c6c-278">Личность пользователя должна быть подтверждена с [помощью Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="c0c6c-278">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="c0c6c-279">После проверки подлинности приложение может получить роль пользователя с помощью `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-279">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="c0c6c-280">Основываясь на роли пользователя, приложение имеет возможность предоставлять ролевые опыты.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-280">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="c0c6c-281">Например, приложение для голосования позволяет создавать новый опрос только организаторам и докладчикам.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-281">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="c0c6c-282">Назначения роли могут быть изменены во время собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-282">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="c0c6c-283">Для получения дополнительной информации [см Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-283">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="c0c6c-284">Во время собрания</span><span class="sxs-lookup"><span data-stu-id="c0c6c-284">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="c0c6c-285">sidePanel</span><span class="sxs-lookup"><span data-stu-id="c0c6c-285">sidePanel</span></span>

<span data-ttu-id="c0c6c-286">С sidePanel, вы можете настроить опыт в заседании, которые позволяют организаторам и докладчикам иметь различный набор представлений и действий.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-286">With the sidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="c0c6c-287">В манифесте приложения необходимо добавить sidePanel в массив контекста.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-287">In your app manifest, you must add sidePanel to the context array.</span></span> <span data-ttu-id="c0c6c-288">В собрании и во всех сценариях приложение отображается во вкладке, которая составляет 320 пикселей в ширину.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-288">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="c0c6c-289">Для получения дополнительной информации [см.](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-289">For more information, see [FrameContext interface](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span></span>

<span data-ttu-id="c0c6c-290">Чтобы использовать `userContext` API для соответствующих запросов маршрута, [см. Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span><span class="sxs-lookup"><span data-stu-id="c0c6c-290">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="c0c6c-291">Можно [Teams потока аутентификации для вкладок.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-291">See [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="c0c6c-292">Поток аутентификации для вкладок очень похож на поток ва-аута для веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-292">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="c0c6c-293">Таким образом, вкладки могут использовать OAuth 2.0 напрямую.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-293">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="c0c6c-294">Смотрите, [платформа удостоверений Майкрософт и OAuth 2.0 поток кода авторизации](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="c0c6c-294">See, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="c0c6c-295">Расширение обмена сообщениями работает, как и ожидалось, когда пользователь находится в представлении на собрании, и пользователь может размещать карточки расширения составить сообщения.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-295">Messaging extension works as expected when a user is in an in-meeting view and the user can post compose message extension cards.</span></span> <span data-ttu-id="c0c6c-296">AppName in-meeting — это инструмент, в который упомятается имя приложения в собрании U-bar.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-296">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

> [!NOTE]
> <span data-ttu-id="c0c6c-297">Используйте версию 1.7.0 [или выше Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), так как версии до нее не поддерживают боковую панель.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-297">Use version 1.7.0 or higher of [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="c0c6c-298">Диалоговое окно собрания</span><span class="sxs-lookup"><span data-stu-id="c0c6c-298">In-meeting dialog</span></span>

<span data-ttu-id="c0c6c-299">Диалоговое окно на собрании может быть использовано для привлечения участников во время собрания и сбора информации или обратной связи во время собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-299">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="c0c6c-300">Используйте [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API, чтобы сигнализировать о том, что уведомление о пузыре должно быть срабатывать.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-300">Use the [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="c0c6c-301">В рамках полезной нагрузки запроса уведомлений включите URL-адрес, в котором размещается содержимое, которое будет показано.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-301">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="c0c6c-302">Диалог на встрече не должен использовать модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-302">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="c0c6c-303">Модуль задачи не вызывается в чате собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-303">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="c0c6c-304">URL-адрес внешнего ресурса используется для отображения пузыря содержимого на собрании.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-304">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="c0c6c-305">Метод можно использовать `submitTask` для отправки данных в чате собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-305">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="c0c6c-306">Вы должны вызвать [функцию submitTask ()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического увольнения после того, как пользователь принимает меры в веб-представлении.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-306">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web-view.</span></span> <span data-ttu-id="c0c6c-307">Это требование для отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-307">This is a requirement for app submission.</span></span> <span data-ttu-id="c0c6c-308">Для получения дополнительной информации [с Teams м.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-308">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="c0c6c-309">Если вы хотите, чтобы ваше приложение поддержало анонимных пользователей, ваша первоначальная полезная нагрузка запроса на вызов `from.id` должна опираться на метаданные `from` запроса в объекте, а `from.aadObjectId` не на метаданные запроса.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-309">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="c0c6c-310">`from.id`является идентификатором пользователя `from.aadObjectId` и Azure Active Directory (AAD) идентификатором пользователя.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-310">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="c0c6c-311">Для получения дополнительной информации [см.](../task-modules-and-cards/task-modules/task-modules-tabs.md) [](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="c0c6c-311">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="share-to-stage"></a><span data-ttu-id="c0c6c-312">Делитесь на сцену</span><span class="sxs-lookup"><span data-stu-id="c0c6c-312">Share to stage</span></span> 

> [!NOTE]
> * <span data-ttu-id="c0c6c-313">Эта возможность в настоящее время доступна только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-313">This capability is currently available in developer preview only.</span></span>
> * <span data-ttu-id="c0c6c-314">Чтобы использовать эту функцию, приложение должно поддерживать боковойпанель в заседании.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-314">To use this feature, the app must support an in-meeting sidepanel.</span></span>


<span data-ttu-id="c0c6c-315">Эта возможность дает разработчикам возможность поделиться приложением на этапе собрания.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-315">This capability gives developers the ability to share an app to the meeting stage.</span></span> <span data-ttu-id="c0c6c-316">Включив совместное участие в стадии собрания, участники собрания могут сотрудничать в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-316">By enabling share to the meeting stage, meeting participants can collaborate in real-time.</span></span> 

<span data-ttu-id="c0c6c-317">Необходимый контекст находится `meetingStage` в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-317">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="c0c6c-318">Предпосылкой для этого является иметь `meetingSidePanel` контекст.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-318">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="c0c6c-319">Это позволяет кнопку **Доля** в sidepanel как depecited в следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="c0c6c-319">This enables the **Share** button in the sidepanel as depecited in the following image:</span></span>

  ![share_to_stage_during_meeting опыт](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="c0c6c-321">Явное изменение, необходимое для включения этой возможности, заключается в следующем:</span><span class="sxs-lookup"><span data-stu-id="c0c6c-321">The manifest change that is needed to enable this capability is as follows:</span></span> 

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



### <a name="after-a-meeting"></a><span data-ttu-id="c0c6c-322">После собрания</span><span class="sxs-lookup"><span data-stu-id="c0c6c-322">After a meeting</span></span>

<span data-ttu-id="c0c6c-323">Конфигурации после собрания и предварительного собрания эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-323">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="code-sample"></a><span data-ttu-id="c0c6c-324">Пример кода</span><span class="sxs-lookup"><span data-stu-id="c0c6c-324">Code sample</span></span>

|<span data-ttu-id="c0c6c-325">Название образца</span><span class="sxs-lookup"><span data-stu-id="c0c6c-325">Sample name</span></span> | <span data-ttu-id="c0c6c-326">Описание</span><span class="sxs-lookup"><span data-stu-id="c0c6c-326">Description</span></span> | <span data-ttu-id="c0c6c-327">.NET</span><span class="sxs-lookup"><span data-stu-id="c0c6c-327">.NET</span></span> | <span data-ttu-id="c0c6c-328">Node.js</span><span class="sxs-lookup"><span data-stu-id="c0c6c-328">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="c0c6c-329">Разгибаемость заседаний</span><span class="sxs-lookup"><span data-stu-id="c0c6c-329">Meetings extensibility</span></span> | <span data-ttu-id="c0c6c-330">Microsoft Teams образец разгибаемости для передачи токенов.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-330">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="c0c6c-331">View</span><span class="sxs-lookup"><span data-stu-id="c0c6c-331">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="c0c6c-332">View</span><span class="sxs-lookup"><span data-stu-id="c0c6c-332">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="c0c6c-333">Встреча содержание пузырь бот</span><span class="sxs-lookup"><span data-stu-id="c0c6c-333">Meeting content bubble bot</span></span> | <span data-ttu-id="c0c6c-334">Microsoft Teams примеру разгибаемости для взаимодействия с ботом пузыря содержимого на собрании.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-334">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="c0c6c-335">View</span><span class="sxs-lookup"><span data-stu-id="c0c6c-335">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="c0c6c-336">View</span><span class="sxs-lookup"><span data-stu-id="c0c6c-336">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="c0c6c-337">Встреча SidePanel</span><span class="sxs-lookup"><span data-stu-id="c0c6c-337">Meeting SidePanel</span></span> | <span data-ttu-id="c0c6c-338">Microsoft Teams выборка для итерактирования с боковой панелью в заседании.</span><span class="sxs-lookup"><span data-stu-id="c0c6c-338">Microsoft Teams meeting extensibility sample for iteracting with the side panel in-meeting.</span></span> | [<span data-ttu-id="c0c6c-339">View</span><span class="sxs-lookup"><span data-stu-id="c0c6c-339">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a><span data-ttu-id="c0c6c-340">См. также</span><span class="sxs-lookup"><span data-stu-id="c0c6c-340">See also</span></span>

* [<span data-ttu-id="c0c6c-341">Руководящие принципы проектирования диалогов на совещании</span><span class="sxs-lookup"><span data-stu-id="c0c6c-341">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="c0c6c-342">Teams проверки подлинности для вкладок</span><span class="sxs-lookup"><span data-stu-id="c0c6c-342">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
