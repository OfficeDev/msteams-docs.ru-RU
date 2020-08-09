---
title: Использование Microsoft Graph для включения активной установки и обмена мгновенными сообщениями в Teams
description: Описание упреждающего обмена сообщениями в Teams и способов их реализации.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: установочный график чата активных сообщений в Teams
ms.openlocfilehash: f1d2c51957eefbc548918210b843e408eb1107c8
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587743"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a><span data-ttu-id="d696c-104">Включение активной установки и упреждающего обмена сообщениями в Teams с помощью Microsoft Graph (общедоступная Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="d696c-104">Enable proactive bot installation and proactive messaging in Teams with Microsoft Graph (Public Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="d696c-105">Общедоступные предварительные обзоры Microsoft Graph доступны для раннего доступа и обратной связи.</span><span class="sxs-lookup"><span data-stu-id="d696c-105">Microsoft Graph public previews are available for early-access and feedback.</span></span> <span data-ttu-id="d696c-106">Несмотря на то что этот выпуск протестировался, он не предназначен для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d696c-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="d696c-107">Активная система обмена сообщениями в Teams</span><span class="sxs-lookup"><span data-stu-id="d696c-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="d696c-108">Активные сообщения инициируются Боты, чтобы начать беседу с пользователем.</span><span class="sxs-lookup"><span data-stu-id="d696c-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="d696c-109">Они позволяют выполнять различные задачи, включая отправку приветственных сообщений, проведение опросов и опросов, а также трансляцию уведомлений в масштабах Организации.</span><span class="sxs-lookup"><span data-stu-id="d696c-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span>  <span data-ttu-id="d696c-110">Интерактивные сообщения в Teams могут доставляться как беседы на основе **специальных** или **диалоговых окон** .</span><span class="sxs-lookup"><span data-stu-id="d696c-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="d696c-111">Тип сообщения</span><span class="sxs-lookup"><span data-stu-id="d696c-111">Message Type</span></span> | <span data-ttu-id="d696c-112">Описание</span><span class="sxs-lookup"><span data-stu-id="d696c-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="d696c-113">Прямое упреждающее сообщение</span><span class="sxs-lookup"><span data-stu-id="d696c-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="d696c-114">Элемент Bot интержектс сообщение, не прерывая потоки бесед.</span><span class="sxs-lookup"><span data-stu-id="d696c-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="d696c-115">Упреждающее сообщение на основе диалоговых окон</span><span class="sxs-lookup"><span data-stu-id="d696c-115">Dialog-based proactive message</span></span> | <span data-ttu-id="d696c-116">Bot создает новый поток диалоговых окон, получает Управление беседами, доставляет упреждающее сообщение, закрывает и возвращает управление предыдущему диалоговому окну.</span><span class="sxs-lookup"><span data-stu-id="d696c-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="d696c-117">*Просмотр*, [Отправка упреждающего уведомления пользователям пакет SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span><span class="sxs-lookup"><span data-stu-id="d696c-117">*See*, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="d696c-118">Упреждающее установка приложений в Teams</span><span class="sxs-lookup"><span data-stu-id="d696c-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="d696c-119">Прежде чем приступить к отправку сообщений пользователю Bot, его необходимо установить либо в качестве личного приложения, либо в группу, в которую входит пользователь.</span><span class="sxs-lookup"><span data-stu-id="d696c-119">Before your bot can proactively message a user, it needs to be installed either as a personal app, or in a team where the user is a member.</span></span> <span data-ttu-id="d696c-120">Иногда может потребоваться упреждающее сообщение о том, что приложение не было установлено или _не_ было взаимодействовать с ним ранее.</span><span class="sxs-lookup"><span data-stu-id="d696c-120">At times,  you may need to proactively message users that have _not_ installed or previously interacted with your app.</span></span> <span data-ttu-id="d696c-121">Например, необходимо получить важную информацию для всех пользователей в Организации.</span><span class="sxs-lookup"><span data-stu-id="d696c-121">For instance, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="d696c-122">Для таких сценариев можно использовать API Microsoft Graph для профилактической установки программы-робота для пользователей.</span><span class="sxs-lookup"><span data-stu-id="d696c-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="d696c-123">Разрешения</span><span class="sxs-lookup"><span data-stu-id="d696c-123">Permissions</span></span>

<span data-ttu-id="d696c-124">Разрешения [типа ресурса](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) Microsoft Graph теамсаппинсталлатион позволяют управлять жизненным циклом установки приложения для всех областей пользователя (персональных) или группы (каналов) на платформе Microsoft teams:</span><span class="sxs-lookup"><span data-stu-id="d696c-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) permissions allow you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="d696c-125">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="d696c-125">Application permission</span></span> | <span data-ttu-id="d696c-126">Описание</span><span class="sxs-lookup"><span data-stu-id="d696c-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="d696c-127">Позволяет приложению Teams читать, устанавливать, обновлять и удалять себя для любого **пользователя**без предварительного входа или использования.</span><span class="sxs-lookup"><span data-stu-id="d696c-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="d696c-128">Позволяет приложению Teams читать, устанавливать, обновлять и удалять себя в любой **команде**без предварительного входа или использования.</span><span class="sxs-lookup"><span data-stu-id="d696c-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="d696c-129">Чтобы использовать эти разрешения, необходимо добавить в манифест приложения ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="d696c-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="d696c-130">**ID** — идентификатор приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d696c-130">**id**  — your Azure AD app id.</span></span>
> * <span data-ttu-id="d696c-131">**ресурс** — URL-адрес ресурса для приложения.</span><span class="sxs-lookup"><span data-stu-id="d696c-131">**resource** — the resource URL for the app.</span></span>
>

>[!NOTE]
>
> * <span data-ttu-id="d696c-132">Для работы с Bot требуются _приложения_ , не являющиеся _делегированными пользователями_ , так как установка не предназначена для других пользователей.</span><span class="sxs-lookup"><span data-stu-id="d696c-132">Your bot requires _application_ not _user delegated_ permissions because the installation is not for yourself but for others.</span></span>
>
> * <span data-ttu-id="d696c-133">Администратор клиента Azure AD должен [явным образом предоставить разрешения приложению](/graph/security-authorization#grant-permissions-to-an-application).</span><span class="sxs-lookup"><span data-stu-id="d696c-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="d696c-134">После получения разрешений для приложения _все_ участники клиента Azure AD получат предоставленные разрешения.</span><span class="sxs-lookup"><span data-stu-id="d696c-134">After an application is granted permissions, _all_ members of the Azure AD tenant will gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="d696c-135">Включение упреждающего установки и обмена сообщениями для приложения</span><span class="sxs-lookup"><span data-stu-id="d696c-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="d696c-136">Microsoft Graph будет устанавливать только приложения, опубликованные в [каталоге приложений](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) вашей организации или в [AppSource](https://appsource.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d696c-136">Microsoft Graph will only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="d696c-137">✔ Создания и публикации робота для работы с системой обмена сообщениями для Teams</span><span class="sxs-lookup"><span data-stu-id="d696c-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="d696c-138">Чтобы приступить к работе, вам потребуются [Bot для Teams](../../bots/how-to/create-a-bot-for-teams.md) с возможностями [упреждающего обмена сообщениями](../../concepts/bots/bot-conversations/bots-conv-proactive.md) и [опубликованы](../../concepts/deploy-and-publish/overview.md) в [каталоге приложений](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) организации или в [AppSource](https://appsource.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d696c-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="d696c-139">Шаблон приложения [**Communicator компании Communicator**](../..//samples/app-templates.md#company-communicator) включает обмен сообщениями и является хорошим фундаментом для создания упреждающего приложения-Bot.</span><span class="sxs-lookup"><span data-stu-id="d696c-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template enables broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="d696c-140">✔ Получить `teamsAppId` ваше приложение</span><span class="sxs-lookup"><span data-stu-id="d696c-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="d696c-141">**1.** вам потребуется выполнить `teamsAppId` дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="d696c-141">**1.** You will need the `teamsAppId`  for the next steps.</span></span>

<span data-ttu-id="d696c-142">`teamsAppId`Можно получить из каталога приложений вашей организации:</span><span class="sxs-lookup"><span data-stu-id="d696c-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="d696c-143">**Справочник по страницам Microsoft Graph:** [тип ресурса teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span><span class="sxs-lookup"><span data-stu-id="d696c-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span></span>

<span data-ttu-id="d696c-144">**Http-запрос Get** :</span><span class="sxs-lookup"><span data-stu-id="d696c-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="d696c-145">Запрос возвратит `teamsApp` объект.</span><span class="sxs-lookup"><span data-stu-id="d696c-145">The request will return a `teamsApp`  object.</span></span> <span data-ttu-id="d696c-146">Возвращаемый объект `id` — это идентификатор приложения, создаваемый каталогом приложения, который отличается от идентификатора "ID:", указанного в манифесте приложения teams:</span><span class="sxs-lookup"><span data-stu-id="d696c-146">The returned object's `id`  is the app's catalog generated app id and is different from the "id:" that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="d696c-147">**2.** если ваше приложение уже было отправлено или неопубликованные для пользователя в личной области, вы можете получить `teamsAppId` следующее:</span><span class="sxs-lookup"><span data-stu-id="d696c-147">**2.**  If your app has already been uploaded/sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="d696c-148">**Справочник по страницам Microsoft Graph:** [список приложений, установленных для пользователя](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="d696c-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="d696c-149">**Http-запрос Get** :</span><span class="sxs-lookup"><span data-stu-id="d696c-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="d696c-150">**3.** если ваше приложение уже было отправлено или неопубликованные для канала в области группы, вы можете получить `teamsAppId` следующее:</span><span class="sxs-lookup"><span data-stu-id="d696c-150">**3.** If your app has already been uploaded/sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="d696c-151">**Справочник по страницам Microsoft Graph:** [список приложений в команде](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="d696c-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="d696c-152">**Http-запрос Get** :</span><span class="sxs-lookup"><span data-stu-id="d696c-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{manifestId}'
```

>[!TIP]
> <span data-ttu-id="d696c-153">Для сужения списка результатов можно выполнить фильтрацию по любому из полей объекта [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) .</span><span class="sxs-lookup"><span data-stu-id="d696c-153">You can filter on any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) object to narrow the list of results.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="d696c-154">✔ Определить, установлен ли в данный момент ваш Bot для получателя сообщения</span><span class="sxs-lookup"><span data-stu-id="d696c-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="d696c-155">**Справочник по страницам Microsoft Graph:** [список приложений, установленных для пользователя](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="d696c-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="d696c-156">**Http-запрос Get** :</span><span class="sxs-lookup"><span data-stu-id="d696c-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="d696c-157">Этот запрос возвратит пустой массив, если приложение не установлено, или массив с одним объектом [теамсаппинсталлатион](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) , если он был установлен.</span><span class="sxs-lookup"><span data-stu-id="d696c-157">This request will return an empty array if the app is not installed, or an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) object if it has been installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="d696c-158">✔ Установить приложение</span><span class="sxs-lookup"><span data-stu-id="d696c-158">✔ Install your app</span></span>

<span data-ttu-id="d696c-159">**Справка по Microsoft Graph:** [Установка приложения для пользователя](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="d696c-159">**Microsoft Graph reference:** [Install app for user](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="d696c-160">**Http-запрос POST** :</span><span class="sxs-lookup"><span data-stu-id="d696c-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="d696c-161">Если у пользователя установлена служба Microsoft Teams, вы можете сразу же увидеть установку приложения.</span><span class="sxs-lookup"><span data-stu-id="d696c-161">If the user has Microsoft Teams running, they may see the app install immediately.</span></span> <span data-ttu-id="d696c-162">Кроме того, для просмотра установленного приложения может потребоваться перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="d696c-162">Alternatively,  a  restart may be necessary to see the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="d696c-163">✔ Получить **чатид** беседы</span><span class="sxs-lookup"><span data-stu-id="d696c-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="d696c-164">Когда приложение устанавливается для пользователя, Bot получит `conversationUpdate` [уведомление о событии](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) , в котором будут содержаться необходимые сведения для отправки упреждающего сообщения.</span><span class="sxs-lookup"><span data-stu-id="d696c-164">When your app is installed for the user, the bot will receive a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that will contain the necessary information to send the proactive message.</span></span>

<span data-ttu-id="d696c-165">`chatId`Кроме того, можно получить следующие значения:</span><span class="sxs-lookup"><span data-stu-id="d696c-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="d696c-166">**Справка по Microsoft Graph:** [Получение чата](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="d696c-166">**Microsoft Graph reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="d696c-167">**1.** вам потребуются приложения `{teamsAppInstallationId}` .</span><span class="sxs-lookup"><span data-stu-id="d696c-167">**1.** You will need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="d696c-168">Если у вас его нет, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d696c-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="d696c-169">**Http-запрос Get** :</span><span class="sxs-lookup"><span data-stu-id="d696c-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="d696c-170">Свойство **ID** ответа имеет значение `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="d696c-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="d696c-171">**2.** сделайте следующий запрос для получения `chatId` :</span><span class="sxs-lookup"><span data-stu-id="d696c-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="d696c-172">**Http-запрос Get** (разрешение `TeamsAppInstallation.ReadWriteSelfForUser.All` ):</span><span class="sxs-lookup"><span data-stu-id="d696c-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="d696c-173">Свойство **ID** ответа имеет значение `chatId` .</span><span class="sxs-lookup"><span data-stu-id="d696c-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="d696c-174">Кроме того, вы можете получить `chatId` запрос с запросом ниже, но для этого потребуется более широкое `Chat.Read.All` разрешение:</span><span class="sxs-lookup"><span data-stu-id="d696c-174">Alternately, you can retrieve the `chatId`  with the request below, but it will require the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="d696c-175">**Http-запрос Get** (разрешение `Chat.Read.All` ):</span><span class="sxs-lookup"><span data-stu-id="d696c-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="d696c-176">✔ Отправки упреждающих сообщений</span><span class="sxs-lookup"><span data-stu-id="d696c-176">✔ Send proactive messages</span></span>

<span data-ttu-id="d696c-177">После добавления ленты для пользователя или группы и получения необходимых сведений о пользователе он может начать [отправку активных сообщений](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).</span><span class="sxs-lookup"><span data-stu-id="d696c-177">Once your bot has been added for a user or team and has acquired the necessary user  information, it can begin to [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).</span></span>

# <a name="c--net"></a>[<span data-ttu-id="d696c-178">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d696c-178">C# / .NET</span></span>](#tab/csharp)

<span data-ttu-id="d696c-179">Приведенный ниже фрагмент кода относится к [примерам Microsoft Bot Framework для C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span><span class="sxs-lookup"><span data-stu-id="d696c-179">The following code snippet is from the [Microsoft Bot Framework Samples for C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="d696c-180">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d696c-180">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="d696c-181">Приведенный ниже фрагмент кода относится к [примерам Microsoft Bot Framework для JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span><span class="sxs-lookup"><span data-stu-id="d696c-181">The following code snippet is from the [Microsoft Bot Framework Samples for JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span></span>

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

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="d696c-182">Раздел, посвященный администраторам Teams</span><span class="sxs-lookup"><span data-stu-id="d696c-182">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d696c-183">**Управление политиками установки приложений в Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="d696c-183">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="d696c-184">Просмотр дополнительных примеров кода</span><span class="sxs-lookup"><span data-stu-id="d696c-184">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d696c-185">**Примеры кода для активных сообщений Teams**</span><span class="sxs-lookup"><span data-stu-id="d696c-185">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
