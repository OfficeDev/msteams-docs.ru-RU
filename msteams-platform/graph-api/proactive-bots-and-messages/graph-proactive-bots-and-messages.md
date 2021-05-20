---
title: Используйте Microsoft Graph для авторизации упреждающей установки ботов и обмена сообщениями в Teams
description: Описывает упреждающие сообщения в Teams и как реализовать.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: команды проактивной установки чата обмена сообщениями Graph
ms.openlocfilehash: 06b50e5ab8594c257959430383bab5e355af4e06
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566154"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a><span data-ttu-id="a9cc8-104">Упреждающая установку приложений с помощью API Graph и отправка сообщений</span><span class="sxs-lookup"><span data-stu-id="a9cc8-104">Proactive installation of apps using Graph API and send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="a9cc8-105">Microsoft Graph и Microsoft Teams предварительные просмотры доступны для раннего доступа и обратной связи.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="a9cc8-106">Хотя этот релиз прошел обширное тестирование, он не предназначен для использования в производстве.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="a9cc8-107">Проактивные сообщения в Teams</span><span class="sxs-lookup"><span data-stu-id="a9cc8-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="a9cc8-108">Проактивные сообщения ими ими ими ими ими и начинаются с пользователем.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="a9cc8-109">Они служат многим целям, включая отправку приветственных сообщений, проведение опросов или опросов, а также трансляцию уведомлений по всей организации.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="a9cc8-110">Проактивные сообщения Teams могут быть доставлены как **специальные, так** **и диалоговые:**</span><span class="sxs-lookup"><span data-stu-id="a9cc8-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="a9cc8-111">Тип сообщения</span><span class="sxs-lookup"><span data-stu-id="a9cc8-111">Message Type</span></span> | <span data-ttu-id="a9cc8-112">Описание</span><span class="sxs-lookup"><span data-stu-id="a9cc8-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="a9cc8-113">Специальное упреждающее сообщение</span><span class="sxs-lookup"><span data-stu-id="a9cc8-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="a9cc8-114">Бот вставляет сообщение, не прерывая поток разговора.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="a9cc8-115">Упреждающее сообщение на основе Dialog</span><span class="sxs-lookup"><span data-stu-id="a9cc8-115">Dialog-based proactive message</span></span> | <span data-ttu-id="a9cc8-116">Бот создает новый диалоговый поток, берет под контроль разговор, доставляет упреждающее сообщение, закрывает и возвращает контроль к предыдущему диалогу.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="a9cc8-117">Проактивная установка приложений в Teams</span><span class="sxs-lookup"><span data-stu-id="a9cc8-117">Proactive app installation in Teams</span></span>

<span data-ttu-id="a9cc8-118">Прежде чем ваш бот сможет активно отправить сообщение пользователю, он должен быть установлен либо в качестве личного приложения, либо в команде, в которой пользователь является участником.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-118">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="a9cc8-119">Иногда необходимо активно сообщения пользователям, которые не установили или ранее взаимодействовали с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-119">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="a9cc8-120">Например, необходимость сообщения жизненно важной информации всем в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-120">For example, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="a9cc8-121">Для таких сценариев можно использовать API Microsoft Graph для упреждающей установки бота для пользователей.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-121">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="a9cc8-122">Разрешения</span><span class="sxs-lookup"><span data-stu-id="a9cc8-122">Permissions</span></span>

<span data-ttu-id="a9cc8-123">Разрешения Graph [группы Microsoft, в том](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) есть разрешения на установку ресурсов для всех областей пользователей (личных) или командных (каналов) в рамках Microsoft Teams платформы:</span><span class="sxs-lookup"><span data-stu-id="a9cc8-123">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions helps you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="a9cc8-124">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="a9cc8-124">Application permission</span></span> | <span data-ttu-id="a9cc8-125">Описание</span><span class="sxs-lookup"><span data-stu-id="a9cc8-125">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="a9cc8-126">Позволяет Teams для чтения, установки, обновления и удаления себя для любого **пользователя,** без предварительного вовсяка или использования.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-126">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="a9cc8-127">Позволяет Teams читать, устанавливать, модернизировать и удалять себя в любой **команде, без** предварительного вовсяка или использования.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-127">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="a9cc8-128">Чтобы использовать эти разрешения, необходимо добавить ключ [webApplicationInfo к манифесту](../../resources/schema/manifest-schema.md#webapplicationinfo) приложения со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="a9cc8-128">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="a9cc8-129">**ID** - идентификатор приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-129">**id** — your Azure AD app ID.</span></span>
> * <span data-ttu-id="a9cc8-130">**ресурс** — URL-адрес ресурса для приложения.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-130">**resource** — the resource URL for the app.</span></span>
>
>[!NOTE]
>
> * <span data-ttu-id="a9cc8-131">Ваш бот требует применения, а не пользовательских разрешений, потому что установка для других.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-131">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="a9cc8-132">Администратор арендатора Azure AD [должен явно предоставлять разрешения на приложение.](/graph/security-authorization#grant-permissions-to-an-application)</span><span class="sxs-lookup"><span data-stu-id="a9cc8-132">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="a9cc8-133">После получения разрешения на приложение все участники azure AD-арендатор получают предоставленные разрешения.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-133">After an application is granted permissions, all members of the Azure AD tenant gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="a9cc8-134">Включить проактивную установку приложений и обмен сообщениями</span><span class="sxs-lookup"><span data-stu-id="a9cc8-134">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
><span data-ttu-id="a9cc8-135">Корпорация Graph может устанавливать только приложения, опубликованные в магазине приложений вашей организации или в магазине Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-135">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="a9cc8-136">✔ создать и опубликовать свой упреждающий бот обмена сообщениями для Teams</span><span class="sxs-lookup"><span data-stu-id="a9cc8-136">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="a9cc8-137">Чтобы начать работу, вам нужен [бот для Teams с упреждающими](../../bots/how-to/create-a-bot-for-teams.md) [возможностями](../../concepts/bots/bot-conversations/bots-conv-proactive.md) обмена сообщениями, которые [есть в магазине приложений вашей](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) [организации или в магазине Teams магазина.](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)</span><span class="sxs-lookup"><span data-stu-id="a9cc8-137">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that's in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

>[!TIP]
> <span data-ttu-id="a9cc8-138">Готовая к производству [**компания Communicator позволяет**](../..//samples/app-templates.md#company-communicator) транслировать сообщения и является хорошей основой для создания вашего активного приложения бота.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-138">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="a9cc8-139">✔ получите для `teamsAppId` вашего приложения</span><span class="sxs-lookup"><span data-stu-id="a9cc8-139">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="a9cc8-140">**1.** Вам нужно `teamsAppId` для следующих шагов.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-140">**1.** You need the `teamsAppId` for the next steps.</span></span>

<span data-ttu-id="a9cc8-141">Можно `teamsAppId` получить из каталога приложений вашей организации:</span><span class="sxs-lookup"><span data-stu-id="a9cc8-141">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="a9cc8-142">**Ссылка Graph microsoft на страницу:** [тип ресурса teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a9cc8-142">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="a9cc8-143">**Запрос HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="a9cc8-143">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="a9cc8-144">Запрос должен вернуть `teamsApp` объект.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-144">The request must return a `teamsApp` object.</span></span> <span data-ttu-id="a9cc8-145">Возвращенный объект `id` является идентификатором приложения, созданным в каталоге приложений, и отличается от идентификатора, предоставленного вами в Teams приложении:</span><span class="sxs-lookup"><span data-stu-id="a9cc8-145">The returned object `id` is the app's catalog generated app ID and is different from the ID that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="a9cc8-146">**2.**  Если ваше приложение уже загружено или загружено для пользователя в личном прицеле, вы можете получить `teamsAppId` следующее:</span><span class="sxs-lookup"><span data-stu-id="a9cc8-146">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="a9cc8-147">**Ссылка Graph Microsoft: Список приложений,** [установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a9cc8-147">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="a9cc8-148">**Запрос HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="a9cc8-148">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="a9cc8-149">**3.** Если ваше приложение было загружено или загружено для канала в области команды, вы можете получить `teamsAppId` следующее:</span><span class="sxs-lookup"><span data-stu-id="a9cc8-149">**3.** If your app has been uploaded or sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="a9cc8-150">**Ссылка Graph microsoft на странице:** [Список приложений в команде](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a9cc8-150">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="a9cc8-151">**Запрос HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="a9cc8-151">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="a9cc8-152">Чтобы сузить список результатов, можно фильтровать на любом из полей [**объекта teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a9cc8-152">To narrow the list of results, you can filter on any of the fields of [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="a9cc8-153">✔ определить, установлен ли ваш бот в настоящее время для получателя сообщения</span><span class="sxs-lookup"><span data-stu-id="a9cc8-153">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="a9cc8-154">**Ссылка Graph Microsoft: Список приложений,** [установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a9cc8-154">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="a9cc8-155">**Запрос HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="a9cc8-155">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="a9cc8-156">Этот запрос возвращает пустой массив, если приложение не установлено, и массив с одним [объектом teamsAppInstallation,](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) если приложение установлено.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-156">This request returns an empty array if the app is not installed and an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="a9cc8-157">✔ Установите приложение</span><span class="sxs-lookup"><span data-stu-id="a9cc8-157">✔ Install your app</span></span>

<span data-ttu-id="a9cc8-158">**Ссылка Graph microsoft на страницу:** [Установите приложение для пользователя](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a9cc8-158">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="a9cc8-159">**Запрос HTTP POST:**</span><span class="sxs-lookup"><span data-stu-id="a9cc8-159">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="a9cc8-160">Если пользователь не Microsoft Teams, установка приложения немедленно рассматривается.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-160">If the user has Microsoft Teams running, app installation is seen immediately.</span></span> <span data-ttu-id="a9cc8-161">Для просмотра установленного приложения может потребоваться перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-161">A restart may be required to view the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="a9cc8-162">✔ Получить разговор **chatId**</span><span class="sxs-lookup"><span data-stu-id="a9cc8-162">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="a9cc8-163">Когда ваше приложение установлено для пользователя, бот получает уведомление о `conversationUpdate` [событии, которое содержит](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) необходимую информацию для отправки упреждающего сообщения.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-163">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="a9cc8-164">Можно `chatId` также получить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a9cc8-164">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="a9cc8-165">**Ссылка Graph microsoft на страницу:** [Получить чат](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a9cc8-165">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="a9cc8-166">**1.** Вы должны нуждаться в вашем приложении `{teamsAppInstallationId}` .</span><span class="sxs-lookup"><span data-stu-id="a9cc8-166">**1.** You must need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="a9cc8-167">Если у вас его нет, используйте следующее:</span><span class="sxs-lookup"><span data-stu-id="a9cc8-167">If you don't have it, use the following:</span></span>

<span data-ttu-id="a9cc8-168">**Запрос HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="a9cc8-168">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="a9cc8-169">**Идентификатором** свойства ответа является `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="a9cc8-169">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="a9cc8-170">**2.** Сделайте следующий запрос, чтобы `chatId` получить:</span><span class="sxs-lookup"><span data-stu-id="a9cc8-170">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="a9cc8-171">**Запрос HTTP GET** (разрешение - `TeamsAppInstallation.ReadWriteSelfForUser.All` ):</span><span class="sxs-lookup"><span data-stu-id="a9cc8-171">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="a9cc8-172">**Идентификатором** свойства ответа является `chatId` .</span><span class="sxs-lookup"><span data-stu-id="a9cc8-172">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="a9cc8-173">Вы также можете получить `chatId` следующий запрос, но он требует более широкого `Chat.Read.All` разрешения:</span><span class="sxs-lookup"><span data-stu-id="a9cc8-173">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="a9cc8-174">**Запрос HTTP GET** (разрешение - `Chat.Read.All` ):</span><span class="sxs-lookup"><span data-stu-id="a9cc8-174">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="a9cc8-175">✔ отправлять упреждающие сообщения</span><span class="sxs-lookup"><span data-stu-id="a9cc8-175">✔ Send proactive messages</span></span>

<span data-ttu-id="a9cc8-176">Ваш бот может [отправлять упреждающие сообщения](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) после того, как бот был добавлен для пользователя или команды и получил всю информацию о пользователе.</span><span class="sxs-lookup"><span data-stu-id="a9cc8-176">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team and has received all the user information.</span></span>

## <a name="see-also"></a><span data-ttu-id="a9cc8-177">См. также</span><span class="sxs-lookup"><span data-stu-id="a9cc8-177">See also</span></span>

* [<span data-ttu-id="a9cc8-178">**Управление политиками настройки приложений в Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="a9cc8-178">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [<span data-ttu-id="a9cc8-179">Отправка упреждающих уведомлений пользователям SDK v4</span><span class="sxs-lookup"><span data-stu-id="a9cc8-179">Send proactive notifications to users SDK v4</span></span>](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a><span data-ttu-id="a9cc8-180">Просмотр дополнительных образцов кода</span><span class="sxs-lookup"><span data-stu-id="a9cc8-180">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a9cc8-181">**Teams упреждающие образцы кода обмена сообщениями**</span><span class="sxs-lookup"><span data-stu-id="a9cc8-181">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)