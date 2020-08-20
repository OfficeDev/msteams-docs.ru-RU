---
title: Использование Microsoft Graph для включения упреждающие установки и обмена сообщениями ботов в Teams
description: Описывает упреждающие сообщения в Teams и как реализовать их.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: графический клиент, применяемый в упреждающем сообщении teams
ms.openlocfilehash: b601c5858e5141ce81985dca62968b1713e1d2ba
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819163"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a><span data-ttu-id="db790-104">Включение упреждающей установки бота и упреждающие сообщения в Teams с помощью Microsoft Graph (общедоступная предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="db790-104">Enable proactive bot installation and proactive messaging in Teams with Microsoft Graph (Public Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="db790-105">Для раннего доступа и получения отзывов доступны общедоступные предварительные версии Microsoft Graph и Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="db790-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="db790-106">Хотя в этом выпуске прошло обширное тестирование, он не предназначен для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="db790-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="db790-107">Заранее обмен сообщениями в Teams</span><span class="sxs-lookup"><span data-stu-id="db790-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="db790-108">Заблаговременное сообщение инициируется ботами для начала беседы с пользователем.</span><span class="sxs-lookup"><span data-stu-id="db790-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="db790-109">Они служат многими целями, в том числе отправка приветственных сообщений, проведение опросов или опросов, а также трансформация уведомлений для всей организации.</span><span class="sxs-lookup"><span data-stu-id="db790-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span>  <span data-ttu-id="db790-110">Заранее упреждающие сообщения в Teams можно доставлять в виде **нерегламентированных** или **диалоговых** бесед.</span><span class="sxs-lookup"><span data-stu-id="db790-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="db790-111">Тип сообщения</span><span class="sxs-lookup"><span data-stu-id="db790-111">Message Type</span></span> | <span data-ttu-id="db790-112">Description</span><span class="sxs-lookup"><span data-stu-id="db790-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="db790-113">Нерегулярное сообщение</span><span class="sxs-lookup"><span data-stu-id="db790-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="db790-114">Бот интерпретирует сообщение, не прерывая поток беседы.</span><span class="sxs-lookup"><span data-stu-id="db790-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="db790-115">Заблаговорное сообщение на основе диалогового окна</span><span class="sxs-lookup"><span data-stu-id="db790-115">Dialog-based proactive message</span></span> | <span data-ttu-id="db790-116">Бот создает новую цепочку диалоговых окон, получает управление беседой, превращает заблаговремяное сообщение, закрывает и возвращает управление в предыдущее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="db790-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="db790-117">*Просмотр:* [отправка упреждающие уведомлений SDK 4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span><span class="sxs-lookup"><span data-stu-id="db790-117">*See*, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="db790-118">Упреждающая установка приложений в Teams</span><span class="sxs-lookup"><span data-stu-id="db790-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="db790-119">Прежде чем ваш бот сможет заблагоена отдать сообщение о пользователе, его необходимо установить в виде личного приложения или в команде, в которой пользователь является участником.</span><span class="sxs-lookup"><span data-stu-id="db790-119">Before your bot can proactively message a user, it needs to be installed either as a personal app, or in a team where the user is a member.</span></span> <span data-ttu-id="db790-120">Иногда может потребоваться заблаговременно профилактиковать пользователей, _которые_ не работали или ранее не взаимодействовали с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="db790-120">At times,  you may need to proactively message users that have _not_ installed or previously interacted with your app.</span></span> <span data-ttu-id="db790-121">Например, необходимость сообщения о пользователе сообщения о пользователе всех пользователей в организации.</span><span class="sxs-lookup"><span data-stu-id="db790-121">For instance, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="db790-122">В таких случаях можно использовать API Microsoft Graph, чтобы заблагообразовать свой бот для пользователей.</span><span class="sxs-lookup"><span data-stu-id="db790-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="db790-123">Разрешения</span><span class="sxs-lookup"><span data-stu-id="db790-123">Permissions</span></span>

<span data-ttu-id="db790-124">Разрешения [типа ресурса teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) в Microsoft Graph позволяют управлять жизненным циклом установки приложения для всех пользователей (личных) или областей команд (канала) в платформе Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="db790-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) permissions allow you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="db790-125">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="db790-125">Application permission</span></span> | <span data-ttu-id="db790-126">Description</span><span class="sxs-lookup"><span data-stu-id="db790-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="db790-127">Позволяет приложению Teams читать, устанавливать, обновлять и удалить себя для **любого пользователя,** не предыдущие вход или использование.</span><span class="sxs-lookup"><span data-stu-id="db790-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="db790-128">Позволяет приложению Teams читать, устанавливать, обновлять и удалить себя в любой **команде**без предварительного входа или использования.</span><span class="sxs-lookup"><span data-stu-id="db790-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="db790-129">Чтобы использовать эти разрешения, добавьте ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="db790-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="db790-130">**id**  — идентификатор приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="db790-130">**id**  — your Azure AD app id.</span></span>
> * <span data-ttu-id="db790-131">**resource** — URL-адрес ресурса для приложения.</span><span class="sxs-lookup"><span data-stu-id="db790-131">**resource** — the resource URL for the app.</span></span>
>

>[!NOTE]
>
> * <span data-ttu-id="db790-132">Вашему боту _требуются разрешения приложения,_ _которые не_ делегированы пользователям, поскольку установка предназначена не для себя, а для других.</span><span class="sxs-lookup"><span data-stu-id="db790-132">Your bot requires _application_ not _user delegated_ permissions because the installation is not for yourself but for others.</span></span>
>
> * <span data-ttu-id="db790-133">Администратор клиента Azure AD должен [явным образом предоставить разрешения для приложения.](/graph/security-authorization#grant-permissions-to-an-application)</span><span class="sxs-lookup"><span data-stu-id="db790-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="db790-134">После получения приложением разрешений _все члены_ клиента Azure AD полбадят предоставленные разрешения.</span><span class="sxs-lookup"><span data-stu-id="db790-134">After an application is granted permissions, _all_ members of the Azure AD tenant will gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="db790-135">Включение упреждающие установки приложений и обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="db790-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="db790-136">Microsoft Graph устанавливает только приложения, опубликованные в каталоге [приложений организации](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) или [в AppSource.](https://appsource.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="db790-136">Microsoft Graph will only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="db790-137">✔ и публикация бота для сообщений, упреждающем в Teams</span><span class="sxs-lookup"><span data-stu-id="db790-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="db790-138">Для начала вам потребуется [бот](../../bots/how-to/create-a-bot-for-teams.md) для Teams со возможностями [заблаговорного](../../concepts/bots/bot-conversations/bots-conv-proactive.md) обмена сообщениями, который [опубликован](../../concepts/deploy-and-publish/overview.md) в каталоге приложений вашей [организации](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) [или в AppSource.](https://appsource.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="db790-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="db790-139">Готовый для [**рабочей Communicator**](../..//samples/app-templates.md#company-communicator) шаблон приложения "Готово к работе" обеспечивает передачу сообщений и является хорошей основой для создания проактивного приложения бота.</span><span class="sxs-lookup"><span data-stu-id="db790-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template enables broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="db790-140">✔Получение `teamsAppId` приложения</span><span class="sxs-lookup"><span data-stu-id="db790-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="db790-141">**1.** Он `teamsAppId`  понадобится на последующих этапах.</span><span class="sxs-lookup"><span data-stu-id="db790-141">**1.** You will need the `teamsAppId`  for the next steps.</span></span>

<span data-ttu-id="db790-142">Его `teamsAppId` можно получить из каталога приложений вашей организации:</span><span class="sxs-lookup"><span data-stu-id="db790-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="db790-143">**Справочник по страницам Microsoft Graph:** [тип ресурса teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span><span class="sxs-lookup"><span data-stu-id="db790-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span></span>

<span data-ttu-id="db790-144">**HTTP-запрос GET:**</span><span class="sxs-lookup"><span data-stu-id="db790-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="db790-145">Запрос возвратит `teamsApp`  объект.</span><span class="sxs-lookup"><span data-stu-id="db790-145">The request will return a `teamsApp`  object.</span></span> <span data-ttu-id="db790-146">Возвращаемый объект — это идентификатор `id`  приложения, сгенерированный каталогом приложения и отличается от идентификатора "id:", который вы указали в манифесте приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="db790-146">The returned object's `id`  is the app's catalog generated app id and is different from the "id:" that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="db790-147">**2.**  Если ваше приложение уже отправлено или неопубликовано для пользователя в личной области, вы можете получить `teamsAppId` следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="db790-147">**2.**  If your app has already been uploaded/sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="db790-148">**Справочник по страницам Microsoft Graph: список** [установленных для пользователя приложений](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="db790-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="db790-149">**HTTP-запрос GET:**</span><span class="sxs-lookup"><span data-stu-id="db790-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="db790-150">**3.** Если ваше приложение уже отправлено или неопубликовано для канала в области действия команды, вы можете получить `teamsAppId` указанные ниже разрешения.</span><span class="sxs-lookup"><span data-stu-id="db790-150">**3.** If your app has already been uploaded/sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="db790-151">**Справочник по страницам Microsoft Graph: список** [приложений в команде](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="db790-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="db790-152">**HTTP-запрос GET:**</span><span class="sxs-lookup"><span data-stu-id="db790-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="db790-153">Вы можете фильтровать данные по любому из полей [**объекта teamsApp,**](/graph/api/resources/teamsapp?view=graph-rest-1.0) чтобы сузить список результатов.</span><span class="sxs-lookup"><span data-stu-id="db790-153">You can filter on any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) object to narrow the list of results.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="db790-154">✔ Определение того, установлен ли ваш бот для получателя сообщения</span><span class="sxs-lookup"><span data-stu-id="db790-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="db790-155">**Справочник по страницам Microsoft Graph: список** [установленных для пользователя приложений](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="db790-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="db790-156">**HTTP-запрос GET:**</span><span class="sxs-lookup"><span data-stu-id="db790-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="db790-157">Если приложение не установлено, этот запрос вернет пустой массив или массив с одним объектом [teamsAppInstallation,](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) если оно установлено.</span><span class="sxs-lookup"><span data-stu-id="db790-157">This request will return an empty array if the app is not installed, or an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) object if it has been installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="db790-158">✔ установка приложения</span><span class="sxs-lookup"><span data-stu-id="db790-158">✔ Install your app</span></span>

<span data-ttu-id="db790-159">**Справка по Microsoft Graph:** [установка приложения для пользователя](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="db790-159">**Microsoft Graph reference:** [Install app for user](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="db790-160">**HTTP-запрос POST:**</span><span class="sxs-lookup"><span data-stu-id="db790-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="db790-161">Если пользователь работает под управлением Microsoft Teams, он может сразу увидеть установку приложения.</span><span class="sxs-lookup"><span data-stu-id="db790-161">If the user has Microsoft Teams running, they may see the app install immediately.</span></span> <span data-ttu-id="db790-162">Или же может потребоваться перезагрузка, чтобы увидеть установленное приложение.</span><span class="sxs-lookup"><span data-stu-id="db790-162">Alternatively,  a  restart may be necessary to see the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="db790-163">✔ получение идентификатора **чата**</span><span class="sxs-lookup"><span data-stu-id="db790-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="db790-164">Если ваше приложение установлено для пользователя, бот получит уведомление о событии, которое будет содержать необходимые сведения `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) для отправки проактивного сообщения.</span><span class="sxs-lookup"><span data-stu-id="db790-164">When your app is installed for the user, the bot will receive a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that will contain the necessary information to send the proactive message.</span></span>

<span data-ttu-id="db790-165">Его `chatId` также можно получить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db790-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="db790-166">**Справка по Microsoft Graph: получение** [чатов](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="db790-166">**Microsoft Graph reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="db790-167">**1.** Вам понадобится ваше `{teamsAppInstallationId}` приложение.</span><span class="sxs-lookup"><span data-stu-id="db790-167">**1.** You will need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="db790-168">Если это не так, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="db790-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="db790-169">**HTTP-запрос GET:**</span><span class="sxs-lookup"><span data-stu-id="db790-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="db790-170">Свойство **id** отклика — `teamsAppInstallationId` это.</span><span class="sxs-lookup"><span data-stu-id="db790-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="db790-171">**2.** Отправьте приведенный ниже запрос для `chatId` получения.</span><span class="sxs-lookup"><span data-stu-id="db790-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="db790-172">**HTTP-запрос GET** (разрешение `TeamsAppInstallation.ReadWriteSelfForUser.All` — ):</span><span class="sxs-lookup"><span data-stu-id="db790-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="db790-173">Свойство **id** отклика — `chatId` это.</span><span class="sxs-lookup"><span data-stu-id="db790-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="db790-174">Кроме того, запрос можно `chatId`  получить с помощью запроса ниже, но для него требуется более широкий `Chat.Read.All` уровень разрешений:</span><span class="sxs-lookup"><span data-stu-id="db790-174">Alternately, you can retrieve the `chatId`  with the request below, but it will require the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="db790-175">**HTTP-запрос GET** (разрешение `Chat.Read.All` — ):</span><span class="sxs-lookup"><span data-stu-id="db790-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="db790-176">✔ отправка упреждающих сообщений</span><span class="sxs-lookup"><span data-stu-id="db790-176">✔ Send proactive messages</span></span>

<span data-ttu-id="db790-177">После того как ваш бот будет добавлен для пользователя или группы и получить необходимые сведения, можно начинать [отправку заблагоприятных сообщений.](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span><span class="sxs-lookup"><span data-stu-id="db790-177">Once your bot has been added for a user or team and has acquired the necessary user  information, it can begin to [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).</span></span>

# <a name="c--net"></a>[<span data-ttu-id="db790-178">C# / .NET</span><span class="sxs-lookup"><span data-stu-id="db790-178">C# / .NET</span></span>](#tab/csharp)

<span data-ttu-id="db790-179">Фрагмент кода ниже взят [из примеров Microsoft Bot Framework для C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span><span class="sxs-lookup"><span data-stu-id="db790-179">The following code snippet is from the [Microsoft Bot Framework Samples for C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span></span>

```csharp
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Bot.Builder;
using Microsoft.Bot.Schema;

namespace Microsoft.BotBuilderSamples
{
    public class ProactiveBot : ActivityHandler
    {
        // Message to send to users when the bot receives a Conversation Update event
        private const string WelcomeMessage = "Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.";

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

        public ProactiveBot(ConcurrentDictionary<string, ConversationReference> conversationReferences)
        {
            _conversationReferences = conversationReferences;
        }

        private void AddConversationReference(Activity activity)
        {
            var conversationReference = activity.GetConversationReference();
            _conversationReferences.AddOrUpdate(conversationReference.User.Id, conversationReference, (key, newValue) => conversationReference);
        }

        protected override Task OnConversationUpdateActivityAsync(ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            return base.OnConversationUpdateActivityAsync(turnContext, cancellationToken);
        }

        protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            foreach (var member in membersAdded)
            {
                // Greet anyone that was not the target (recipient) of this message.
                if (member.Id != turnContext.Activity.Recipient.Id)
                {
                    await turnContext.SendActivityAsync(MessageFactory.Text(WelcomeMessage), cancellationToken);
                }
            }
        }

        protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            // Echo back what the user said
            await turnContext.SendActivityAsync(MessageFactory.Text($"You sent '{turnContext.Activity.Text}'"), cancellationToken);
        }
    }
}
```

# <a name="javascript"></a>[<span data-ttu-id="db790-180">JavaScript</span><span class="sxs-lookup"><span data-stu-id="db790-180">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="db790-181">Фрагмент кода приведен ниже в [примерах Microsoft Bot Framework для JavaScript.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)</span><span class="sxs-lookup"><span data-stu-id="db790-181">The following code snippet is from the [Microsoft Bot Framework Samples for JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span></span>

```javascript
const { ActivityHandler, TurnContext } = require('botbuilder');

class ProactiveBot extends ActivityHandler {
    constructor(conversationReferences) {
        super();

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        this.conversationReferences = conversationReferences;

        this.onConversationUpdate(async (context, next) => {
            this.addConversationReference(context.activity);

            await next();
        });

        this.onMembersAdded(async (context, next) => {
            const membersAdded = context.activity.membersAdded;
            for (let cnt = 0; cnt < membersAdded.length; cnt++) {
                if (membersAdded[cnt].id !== context.activity.recipient.id) {
                    const welcomeMessage = 'Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.';
                    await context.sendActivity(welcomeMessage);
                }
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });

        this.onMessage(async (context, next) => {
            this.addConversationReference(context.activity);

            // Echo back what the user said
            await context.sendActivity(`You sent '${ context.activity.text }'`);
            await next();
        });
    }

    addConversationReference(activity) {
        const conversationReference = TurnContext.getConversationReference(activity);
        this.conversationReferences[conversationReference.conversation.id] = conversationReference;
    }
}

module.exports.ProactiveBot = ProactiveBot;

```
---

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="db790-182">Статья по теме для администраторов Teams</span><span class="sxs-lookup"><span data-stu-id="db790-182">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="db790-183">**Управление политиками настройки приложений в Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="db790-183">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="db790-184">Просмотр дополнительных примеров кода</span><span class="sxs-lookup"><span data-stu-id="db790-184">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="db790-185">**Примеры упреждающего кода обмена сообщениями Teams**</span><span class="sxs-lookup"><span data-stu-id="db790-185">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
