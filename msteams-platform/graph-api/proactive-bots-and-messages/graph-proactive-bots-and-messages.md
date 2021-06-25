---
title: Использование microsoft Graph для авторизации активной установки ботов и обмена сообщениями в Teams
description: Описывает активный обмен сообщениями в Teams и как реализовать.
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: группы проактивной установки чата Graph
ms.openlocfilehash: 222c69f6349177a72f4b8599068ea1ebacbf6d16
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114240"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a><span data-ttu-id="ff640-104">Активная установка приложений с Graph API для отправки сообщений</span><span class="sxs-lookup"><span data-stu-id="ff640-104">Proactive installation of apps using Graph API to send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="ff640-105">Предварительные Graph и Microsoft Teams доступны для раннего доступа и отзывов.</span><span class="sxs-lookup"><span data-stu-id="ff640-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="ff640-106">Хотя этот выпуск прошел широкое тестирование, он не предназначен для использования в производстве.</span><span class="sxs-lookup"><span data-stu-id="ff640-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="ff640-107">Активный обмен сообщениями в Teams</span><span class="sxs-lookup"><span data-stu-id="ff640-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="ff640-108">Активные сообщения инициировали боты, чтобы начать беседы с пользователем.</span><span class="sxs-lookup"><span data-stu-id="ff640-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="ff640-109">Они служат многим целям, включая отправку приветствия, проведение опросов или опросов, а также уведомления для всей организации вещания.</span><span class="sxs-lookup"><span data-stu-id="ff640-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="ff640-110">Активные сообщения в Teams могут быть доставлены в качестве бесед на основе **ad-hoc** или **диалогов:**</span><span class="sxs-lookup"><span data-stu-id="ff640-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="ff640-111">Тип сообщения</span><span class="sxs-lookup"><span data-stu-id="ff640-111">Message type</span></span> | <span data-ttu-id="ff640-112">Описание</span><span class="sxs-lookup"><span data-stu-id="ff640-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="ff640-113">Ad-hoc proactive message</span><span class="sxs-lookup"><span data-stu-id="ff640-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="ff640-114">Бот перенабивает сообщение, не прерывая поток беседы.</span><span class="sxs-lookup"><span data-stu-id="ff640-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="ff640-115">Упреждающие сообщения на основе диалогов</span><span class="sxs-lookup"><span data-stu-id="ff640-115">Dialog-based proactive message</span></span> | <span data-ttu-id="ff640-116">Бот создает новый диалоговое нить, контролирует беседу, доставляет проактивное сообщение, закрывает и возвращает контроль в предыдущий диалог.</span><span class="sxs-lookup"><span data-stu-id="ff640-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="ff640-117">Активная установка приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="ff640-117">Proactive app installation in Teams</span></span>

<span data-ttu-id="ff640-118">Прежде чем ваш бот сможет активно отправлять сообщения пользователю, он должен быть установлен как личное приложение или в команде, в которой пользователь является участником.</span><span class="sxs-lookup"><span data-stu-id="ff640-118">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="ff640-119">Иногда необходимо заблаговременно отправлять сообщения пользователям, которые не установили или ранее не взаимодействовали с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="ff640-119">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="ff640-120">Например, необходимо отправлять важные сведения всем в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="ff640-120">For example, the need to message important information to everyone in your organization.</span></span> <span data-ttu-id="ff640-121">Для таких сценариев можно использовать API microsoft Graph для активной установки бота для пользователей.</span><span class="sxs-lookup"><span data-stu-id="ff640-121">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="ff640-122">Разрешения</span><span class="sxs-lookup"><span data-stu-id="ff640-122">Permissions</span></span>

<span data-ttu-id="ff640-123">Разрешения типа ресурсов Microsoft Graph [TeamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) помогают управлять жизненным циклом установки приложения для всех областей пользовательского (личного) или командного (канала) в Microsoft Teams платформе:</span><span class="sxs-lookup"><span data-stu-id="ff640-123">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions help you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="ff640-124">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="ff640-124">Application permission</span></span> | <span data-ttu-id="ff640-125">Описание</span><span class="sxs-lookup"><span data-stu-id="ff640-125">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="ff640-126">Позволяет приложению Teams чтение, установку, обновление и самоустановку для любого пользователя без предварительного входе или использования.</span><span class="sxs-lookup"><span data-stu-id="ff640-126">Allows a Teams app to read, install, upgrade, and uninstall itself for any *user*, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="ff640-127">Позволяет приложению Teams читать, устанавливать, обновлять и удалить себя в любой команде без предварительного входе или использования.</span><span class="sxs-lookup"><span data-stu-id="ff640-127">Allows a Teams app to read, install, upgrade, and uninstall itself in any *team*, without prior sign in or use.</span></span>|

<span data-ttu-id="ff640-128">Чтобы использовать эти разрешения, необходимо добавить ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="ff640-128">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

* <span data-ttu-id="ff640-129">**id:** ID Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="ff640-129">**id**: Your Azure Active Directory (AAD) app ID.</span></span>
* <span data-ttu-id="ff640-130">**ресурс.** URL-адрес ресурса для приложения.</span><span class="sxs-lookup"><span data-stu-id="ff640-130">**resource**: The resource URL for the app.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="ff640-131">Боту требуется приложение, а не делегированная пользователем разрешения, так как установка для других пользователей.</span><span class="sxs-lookup"><span data-stu-id="ff640-131">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="ff640-132">Администратор клиента AAD должен [явно предоставлять разрешения приложению.](/graph/security-authorization#grant-permissions-to-an-application)</span><span class="sxs-lookup"><span data-stu-id="ff640-132">An AAD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="ff640-133">После получения разрешений все члены клиента AAD получают предоставленные разрешения.</span><span class="sxs-lookup"><span data-stu-id="ff640-133">After the application is granted permissions, all members of the AAD tenant get the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="ff640-134">Включить активную установку приложений и обмен сообщениями</span><span class="sxs-lookup"><span data-stu-id="ff640-134">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff640-135">Microsoft Graph может устанавливать только приложения, опубликованные в магазине приложений организации или Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="ff640-135">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="ff640-136">Создание и публикация вашего активного бота обмена сообщениями для Teams</span><span class="sxs-lookup"><span data-stu-id="ff640-136">Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="ff640-137">Чтобы начать работу, [](../../bots/how-to/create-a-bot-for-teams.md) вам нужен бот для [](../../concepts/bots/bot-conversations/bots-conv-proactive.md) Teams с проактивными [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) возможностями обмена сообщениями, который находится в магазине приложений организации или [Teams магазине.](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)</span><span class="sxs-lookup"><span data-stu-id="ff640-137">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that is in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

> [!TIP]
> <span data-ttu-id="ff640-138">Готовый к производству [*шаблон Communicator*](../..//samples/app-templates.md#company-communicator) позволяет транслировать сообщения и является хорошим началом для создания вашего проактивного приложения-бота.</span><span class="sxs-lookup"><span data-stu-id="ff640-138">The production-ready [*Company Communicator*](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good start to build your proactive bot application.</span></span>

### <a name="get-the-teamsappid-for-your-app"></a><span data-ttu-id="ff640-139">Get the `teamsAppId` for your app</span><span class="sxs-lookup"><span data-stu-id="ff640-139">Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="ff640-140">Вы можете получить `teamsAppId` следующие способы:</span><span class="sxs-lookup"><span data-stu-id="ff640-140">You can retrieve the `teamsAppId` in the following ways:</span></span>

* <span data-ttu-id="ff640-141">Из каталога приложений организации:</span><span class="sxs-lookup"><span data-stu-id="ff640-141">From your organization's app catalog:</span></span>

    <span data-ttu-id="ff640-142">**Ссылка Graph Microsoft:** [тип ресурсов teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ff640-142">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

    <span data-ttu-id="ff640-143">**ЗАПРОС HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="ff640-143">**HTTP GET** request:</span></span>

    ```http
        GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    <span data-ttu-id="ff640-144">Запрос должен вернуть объект, который является созданным в каталоге приложения `teamsApp` `id` ИД приложения.</span><span class="sxs-lookup"><span data-stu-id="ff640-144">The request must return a `teamsApp` object `id`, which is the app's catalog generated app ID.</span></span> <span data-ttu-id="ff640-145">Это отличается от ID, который вы предоставили в манифесте Teams приложения:</span><span class="sxs-lookup"><span data-stu-id="ff640-145">This is different from the ID that you provided in your Teams app manifest:</span></span>

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

* <span data-ttu-id="ff640-146">Если приложение уже загружено или загружено для пользователя в личной области:</span><span class="sxs-lookup"><span data-stu-id="ff640-146">If your app has already been uploaded or sideloaded for a user in personal scope:</span></span>

    <span data-ttu-id="ff640-147">**Ссылка Graph Microsoft: Список** [приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ff640-147">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

    <span data-ttu-id="ff640-148">**ЗАПРОС HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="ff640-148">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* <span data-ttu-id="ff640-149">Если ваше приложение уже загружено или загружено для канала в области группы:</span><span class="sxs-lookup"><span data-stu-id="ff640-149">If your app has already been uploaded or sideloaded for a channel in team scope:</span></span>

    <span data-ttu-id="ff640-150">**Ссылка Graph Microsoft: Список** [приложений в команде](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ff640-150">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

    <span data-ttu-id="ff640-151">**ЗАПРОС HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="ff640-151">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > <span data-ttu-id="ff640-152">Чтобы сузить список результатов, можно отфильтровать любое из полей [**объекта teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ff640-152">To narrow the list of results, you can filter any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="ff640-153">Определите, установлен ли в настоящее время бот для получателя сообщения</span><span class="sxs-lookup"><span data-stu-id="ff640-153">Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="ff640-154">Вы можете определить, установлен ли ваш бот для получателя сообщений следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ff640-154">You can determine whether your bot is currently installed for a message recipient as follows:</span></span>

<span data-ttu-id="ff640-155">**Ссылка Graph Microsoft: Список** [приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ff640-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="ff640-156">**ЗАПРОС HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="ff640-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="ff640-157">Возвращает запрос:</span><span class="sxs-lookup"><span data-stu-id="ff640-157">The request returns:</span></span>

* <span data-ttu-id="ff640-158">Пустой массив, если приложение не установлено.</span><span class="sxs-lookup"><span data-stu-id="ff640-158">An empty array if the app is not installed.</span></span>
* <span data-ttu-id="ff640-159">Массив с одним [объектом teamsAppInstallation,](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) если приложение установлено.</span><span class="sxs-lookup"><span data-stu-id="ff640-159">An array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="install-your-app"></a><span data-ttu-id="ff640-160">Установка приложения</span><span class="sxs-lookup"><span data-stu-id="ff640-160">Install your app</span></span>

<span data-ttu-id="ff640-161">Вы можете установить приложение следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ff640-161">You can install your app as follows:</span></span>

<span data-ttu-id="ff640-162">**Ссылка Graph Microsoft:** [Установите приложение для пользователя](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ff640-162">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="ff640-163">**ЗАПРОС HTTP POST:**</span><span class="sxs-lookup"><span data-stu-id="ff640-163">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="ff640-164">Если у пользователя есть Microsoft Teams, установка приложения происходит немедленно.</span><span class="sxs-lookup"><span data-stu-id="ff640-164">If the user has Microsoft Teams running, app installation occurs immediately.</span></span> <span data-ttu-id="ff640-165">Для просмотра установленного приложения может потребоваться перезапуск.</span><span class="sxs-lookup"><span data-stu-id="ff640-165">A restart may be required to view the installed app.</span></span>

### <a name="retrieve-the-conversation-chatid"></a><span data-ttu-id="ff640-166">Извлечение беседы `chatId`</span><span class="sxs-lookup"><span data-stu-id="ff640-166">Retrieve the conversation `chatId`</span></span>

<span data-ttu-id="ff640-167">Когда приложение установлено для пользователя, бот получает уведомление о событии, содержа которое содержит необходимые сведения для `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) отправки проактивного сообщения.</span><span class="sxs-lookup"><span data-stu-id="ff640-167">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="ff640-168">**Ссылка Graph microsoft:** [получить чат](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ff640-168">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

1. <span data-ttu-id="ff640-169">Вы должны иметь приложение `{teamsAppInstallationId}` .</span><span class="sxs-lookup"><span data-stu-id="ff640-169">You must have your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="ff640-170">Если у вас его нет, используйте следующие:</span><span class="sxs-lookup"><span data-stu-id="ff640-170">If you do not have it, use the following:</span></span>

    <span data-ttu-id="ff640-171">**ЗАПРОС HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="ff640-171">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    <span data-ttu-id="ff640-172">Свойство **id** ответа — `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="ff640-172">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

1. <span data-ttu-id="ff640-173">Сделайте следующий запрос, чтобы `chatId` получить:</span><span class="sxs-lookup"><span data-stu-id="ff640-173">Make the following request to fetch the `chatId`:</span></span>

    <span data-ttu-id="ff640-174">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):</span><span class="sxs-lookup"><span data-stu-id="ff640-174">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    <span data-ttu-id="ff640-175">Свойство **id** ответа — `chatId` .</span><span class="sxs-lookup"><span data-stu-id="ff640-175">The **id** property of the response is the `chatId`.</span></span>

    <span data-ttu-id="ff640-176">Вы также можете получить следующий запрос, но для этого требуется `chatId` более широкое `Chat.Read.All` разрешение:</span><span class="sxs-lookup"><span data-stu-id="ff640-176">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

    <span data-ttu-id="ff640-177">**HTTP GET** request (permission — `Chat.Read.All` ):</span><span class="sxs-lookup"><span data-stu-id="ff640-177">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a><span data-ttu-id="ff640-178">Отправка упреждающих сообщений</span><span class="sxs-lookup"><span data-stu-id="ff640-178">Send proactive messages</span></span>

<span data-ttu-id="ff640-179">Ваш бот может [отправлять упреждающие](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) сообщения после того, как бот был добавлен для пользователя или группы и получил всю информацию о пользователе.</span><span class="sxs-lookup"><span data-stu-id="ff640-179">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team, and has received all the user information.</span></span>

## <a name="see-also"></a><span data-ttu-id="ff640-180">См. также</span><span class="sxs-lookup"><span data-stu-id="ff640-180">See also</span></span>

* [<span data-ttu-id="ff640-181">**Управление политиками установки приложений в Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="ff640-181">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [<span data-ttu-id="ff640-182">Отправка упреждающих уведомлений пользователям SDK v4</span><span class="sxs-lookup"><span data-stu-id="ff640-182">Send proactive notifications to users SDK v4</span></span>](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="additional-code-samples"></a><span data-ttu-id="ff640-183">Дополнительные примеры кода</span><span class="sxs-lookup"><span data-stu-id="ff640-183">Additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ff640-184">**Teams примеры кода проактивных сообщений**</span><span class="sxs-lookup"><span data-stu-id="ff640-184">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
