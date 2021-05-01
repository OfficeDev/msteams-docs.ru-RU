---
title: Использование microsoft Graph для авторизации активной установки ботов и обмена сообщениями в Teams
description: Описывает активный обмен сообщениями в Teams и как реализовать.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: группы проактивной установки чата Graph
ms.openlocfilehash: 62974f6f3b26e53558658f0b6cfda815dee1de8a
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101802"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a><span data-ttu-id="19c6f-104">Упреждающая установку приложений с помощью API Graph и отправка сообщений</span><span class="sxs-lookup"><span data-stu-id="19c6f-104">Proactive installation of apps using Graph API and send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="19c6f-105">Предварительные Graph и Microsoft Teams доступны для раннего доступа и отзывов.</span><span class="sxs-lookup"><span data-stu-id="19c6f-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="19c6f-106">Хотя этот выпуск прошел широкое тестирование, он не предназначен для использования в производстве.</span><span class="sxs-lookup"><span data-stu-id="19c6f-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="19c6f-107">Активный обмен сообщениями в Teams</span><span class="sxs-lookup"><span data-stu-id="19c6f-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="19c6f-108">Активные сообщения инициировали боты, чтобы начать беседы с пользователем.</span><span class="sxs-lookup"><span data-stu-id="19c6f-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="19c6f-109">Они служат многим целям, включая отправку приветствия, проведение опросов или опросов, а также уведомления для всей организации вещания.</span><span class="sxs-lookup"><span data-stu-id="19c6f-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="19c6f-110">Активные сообщения в Teams могут быть доставлены в качестве бесед на основе **ad-hoc** или **диалогов:**</span><span class="sxs-lookup"><span data-stu-id="19c6f-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="19c6f-111">Тип сообщения</span><span class="sxs-lookup"><span data-stu-id="19c6f-111">Message Type</span></span> | <span data-ttu-id="19c6f-112">Описание</span><span class="sxs-lookup"><span data-stu-id="19c6f-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="19c6f-113">Ad-hoc proactive message</span><span class="sxs-lookup"><span data-stu-id="19c6f-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="19c6f-114">Бот перенабивает сообщение, не прерывая поток беседы.</span><span class="sxs-lookup"><span data-stu-id="19c6f-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="19c6f-115">Упреждающие сообщения на основе диалогов</span><span class="sxs-lookup"><span data-stu-id="19c6f-115">Dialog-based proactive message</span></span> | <span data-ttu-id="19c6f-116">Бот создает новый диалоговое нить, контролирует беседу, доставляет проактивное сообщение, закрывает и возвращает контроль в предыдущий диалог.</span><span class="sxs-lookup"><span data-stu-id="19c6f-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="19c6f-117">См. в [рубрике Отправка упреждающих уведомлений пользователям SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="19c6f-117">See, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="19c6f-118">Активная установка приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="19c6f-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="19c6f-119">Прежде чем ваш бот сможет активно отправлять сообщения пользователю, он должен быть установлен как личное приложение или в команде, в которой пользователь является участником.</span><span class="sxs-lookup"><span data-stu-id="19c6f-119">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="19c6f-120">Иногда необходимо заблаговременно отправлять сообщения пользователям, которые не установили или ранее не взаимодействовали с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="19c6f-120">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="19c6f-121">Например, необходимо отправлять жизненно важные сведения всем в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="19c6f-121">For example, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="19c6f-122">Для таких сценариев можно использовать API microsoft Graph для активной установки бота для пользователей.</span><span class="sxs-lookup"><span data-stu-id="19c6f-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="19c6f-123">Разрешения</span><span class="sxs-lookup"><span data-stu-id="19c6f-123">Permissions</span></span>

<span data-ttu-id="19c6f-124">Разрешения типа ресурсов Microsoft Graph [TeamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) помогают управлять жизненным циклом установки приложения для всех областей пользовательского (личного) или командного (канала) в Microsoft Teams платформе:</span><span class="sxs-lookup"><span data-stu-id="19c6f-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions helps you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="19c6f-125">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="19c6f-125">Application permission</span></span> | <span data-ttu-id="19c6f-126">Описание</span><span class="sxs-lookup"><span data-stu-id="19c6f-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="19c6f-127">Позволяет приложению Teams чтение, установку, обновление и самоустановку для любого пользователя без предварительного входе или использования.</span><span class="sxs-lookup"><span data-stu-id="19c6f-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="19c6f-128">Позволяет приложению Teams читать, устанавливать, обновлять и удалить себя в любой команде без предварительного входе или использования.</span><span class="sxs-lookup"><span data-stu-id="19c6f-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="19c6f-129">Чтобы использовать эти разрешения, необходимо добавить ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="19c6f-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="19c6f-130">**id** — ваш ID приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19c6f-130">**id** — your Azure AD app ID.</span></span>
> * <span data-ttu-id="19c6f-131">**ресурс** — URL-адрес ресурса для приложения.</span><span class="sxs-lookup"><span data-stu-id="19c6f-131">**resource** — the resource URL for the app.</span></span>
>
>[!NOTE]
>
> * <span data-ttu-id="19c6f-132">Боту требуется приложение, а не делегированная пользователем разрешения, так как установка для других пользователей.</span><span class="sxs-lookup"><span data-stu-id="19c6f-132">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="19c6f-133">Администратор клиента Azure AD должен явно предоставлять разрешения [приложению.](/graph/security-authorization#grant-permissions-to-an-application)</span><span class="sxs-lookup"><span data-stu-id="19c6f-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="19c6f-134">После получения разрешений все члены клиента Azure AD получают предоставленные разрешения.</span><span class="sxs-lookup"><span data-stu-id="19c6f-134">After an application is granted permissions, all members of the Azure AD tenant gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="19c6f-135">Включить активную установку приложений и обмен сообщениями</span><span class="sxs-lookup"><span data-stu-id="19c6f-135">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
><span data-ttu-id="19c6f-136">Microsoft Graph может устанавливать только приложения, опубликованные в магазине приложений организации или Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="19c6f-136">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="19c6f-137">✔ создайте и опубликуйте свой активный бот обмена сообщениями для Teams</span><span class="sxs-lookup"><span data-stu-id="19c6f-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="19c6f-138">Чтобы начать работу, [](../../bots/how-to/create-a-bot-for-teams.md) вам нужен бот для [](../../concepts/bots/bot-conversations/bots-conv-proactive.md) Teams с проактивными [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) возможностями обмена сообщениями, которые есть в магазине приложений организации или [Teams магазине.](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)</span><span class="sxs-lookup"><span data-stu-id="19c6f-138">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that's in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

>[!TIP]
> <span data-ttu-id="19c6f-139">Готовый к производству [**шаблон Communicator**](../..//samples/app-templates.md#company-communicator) позволяет транслировать сообщения и является хорошей основой для создания вашего проактивного приложения-бота.</span><span class="sxs-lookup"><span data-stu-id="19c6f-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="19c6f-140">✔ Получить для `teamsAppId` вашего приложения</span><span class="sxs-lookup"><span data-stu-id="19c6f-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="19c6f-141">**1.** Необходимы `teamsAppId` следующие действия.</span><span class="sxs-lookup"><span data-stu-id="19c6f-141">**1.** You need the `teamsAppId` for the next steps.</span></span>

<span data-ttu-id="19c6f-142">Можно извлечь из каталога приложений `teamsAppId` организации:</span><span class="sxs-lookup"><span data-stu-id="19c6f-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="19c6f-143">**Ссылка Graph Microsoft:** [тип ресурсов teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="19c6f-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="19c6f-144">**ЗАПРОС HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="19c6f-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="19c6f-145">Запрос должен вернуть `teamsApp` объект.</span><span class="sxs-lookup"><span data-stu-id="19c6f-145">The request must return a `teamsApp` object.</span></span> <span data-ttu-id="19c6f-146">Возвращенный объект — это созданный каталог приложения ИД приложения, который отличается от ID, который вы предоставили в манифесте `id` Teams приложения:</span><span class="sxs-lookup"><span data-stu-id="19c6f-146">The returned object `id` is the app's catalog generated app ID and is different from the ID that you provided in your Teams app manifest:</span></span>

```json
{
  "value": [
    {
      "id": "b1c5353a-7aca-41b3-830f-27d5218fe0e5",
      "externalId": "f31b1263-ba99-435a-a679-911d24850d7c",
      "name": "Test App",
      "version": "1.0.1",
      "distributionMethod": "Organization"
    }
  ]
}
```

<span data-ttu-id="19c6f-147">**2.**  Если ваше приложение уже загружено или загружено для пользователя в личной области, вы можете получить следующим `teamsAppId` образом:</span><span class="sxs-lookup"><span data-stu-id="19c6f-147">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="19c6f-148">**Ссылка Graph Microsoft: Список** [приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="19c6f-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="19c6f-149">**ЗАПРОС HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="19c6f-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="19c6f-150">**3.** Если ваше приложение было загружено или загружено для канала в области группы, вы можете получить следующим `teamsAppId` образом:</span><span class="sxs-lookup"><span data-stu-id="19c6f-150">**3.** If your app has been uploaded or sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="19c6f-151">**Ссылка Graph Microsoft: Список** [приложений в команде](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="19c6f-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="19c6f-152">**ЗАПРОС HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="19c6f-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="19c6f-153">Чтобы сузить список результатов, можно фильтровать любой из полей [**объекта teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="19c6f-153">To narrow the list of results, you can filter on any of the fields of [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="19c6f-154">✔ определите, установлен ли ваш бот для получателя сообщения</span><span class="sxs-lookup"><span data-stu-id="19c6f-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="19c6f-155">**Ссылка Graph Microsoft: Список** [приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="19c6f-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="19c6f-156">**ЗАПРОС HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="19c6f-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="19c6f-157">В этом запросе возвращается пустой массив, если приложение не установлено, и массив с одним объектом [teamsAppInstallation,](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) если приложение установлено.</span><span class="sxs-lookup"><span data-stu-id="19c6f-157">This request returns an empty array if the app is not installed and an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="19c6f-158">✔ Установите приложение</span><span class="sxs-lookup"><span data-stu-id="19c6f-158">✔ Install your app</span></span>

<span data-ttu-id="19c6f-159">**Ссылка Graph Microsoft:** [Установите приложение для пользователя](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="19c6f-159">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="19c6f-160">**ЗАПРОС HTTP POST:**</span><span class="sxs-lookup"><span data-stu-id="19c6f-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="19c6f-161">Если у пользователя есть Microsoft Teams, установка приложения рассматривается немедленно.</span><span class="sxs-lookup"><span data-stu-id="19c6f-161">If the user has Microsoft Teams running, app installation is seen immediately.</span></span> <span data-ttu-id="19c6f-162">Для просмотра установленного приложения может потребоваться перезапуск.</span><span class="sxs-lookup"><span data-stu-id="19c6f-162">A restart may be required to view the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="19c6f-163">✔ диалог **chatId**</span><span class="sxs-lookup"><span data-stu-id="19c6f-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="19c6f-164">Когда приложение установлено для пользователя, бот получает уведомление о событии, содержа которое содержит необходимые сведения для `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) отправки проактивного сообщения.</span><span class="sxs-lookup"><span data-stu-id="19c6f-164">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="19c6f-165">Можно `chatId` также извлечь следующим образом:</span><span class="sxs-lookup"><span data-stu-id="19c6f-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="19c6f-166">**Ссылка Graph microsoft:** [получить чат](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="19c6f-166">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="19c6f-167">**1.** Вам необходимо ваше приложение `{teamsAppInstallationId}` .</span><span class="sxs-lookup"><span data-stu-id="19c6f-167">**1.** You must need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="19c6f-168">Если у вас его нет, используйте следующие:</span><span class="sxs-lookup"><span data-stu-id="19c6f-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="19c6f-169">**ЗАПРОС HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="19c6f-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="19c6f-170">Свойство **id** ответа — `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="19c6f-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="19c6f-171">**2.** Сделайте следующий запрос, чтобы получить `chatId` :</span><span class="sxs-lookup"><span data-stu-id="19c6f-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="19c6f-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):</span><span class="sxs-lookup"><span data-stu-id="19c6f-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="19c6f-173">Свойство **id** ответа — `chatId` .</span><span class="sxs-lookup"><span data-stu-id="19c6f-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="19c6f-174">Вы также можете получить следующий запрос, но для этого требуется `chatId` более широкое `Chat.Read.All` разрешение:</span><span class="sxs-lookup"><span data-stu-id="19c6f-174">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="19c6f-175">**HTTP GET** request (permission — `Chat.Read.All` ):</span><span class="sxs-lookup"><span data-stu-id="19c6f-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="19c6f-176">✔ Отправка проактивных сообщений</span><span class="sxs-lookup"><span data-stu-id="19c6f-176">✔ Send proactive messages</span></span>

<span data-ttu-id="19c6f-177">Ваш бот может [отправлять упреждающие](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) сообщения после того, как бот был добавлен для пользователя или группы и получил всю информацию о пользователе.</span><span class="sxs-lookup"><span data-stu-id="19c6f-177">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team and has received all the user information.</span></span>

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="19c6f-178">Связанная тема для Teams администраторов</span><span class="sxs-lookup"><span data-stu-id="19c6f-178">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="19c6f-179">**Управление политиками установки приложений в Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="19c6f-179">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="19c6f-180">Просмотр дополнительных примеров кода</span><span class="sxs-lookup"><span data-stu-id="19c6f-180">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="19c6f-181">**Teams примеры кода проактивных сообщений**</span><span class="sxs-lookup"><span data-stu-id="19c6f-181">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
