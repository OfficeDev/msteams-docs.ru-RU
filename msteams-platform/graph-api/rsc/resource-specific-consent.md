---
title: Согласие на определенные ресурсы в Teams
description: Описывает согласие на конкретные ресурсы в Teams и как использовать его.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: команды авторизации OAuth SSO AAD rsc Graph
ms.openlocfilehash: 39e5c1bb8375fb5b5a3bd3900cb6ad870a3ff677
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101795"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="b9c0a-104">Согласие на определенный ресурс (RSC)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-104">Resource-specific consent (RSC)</span></span>

<span data-ttu-id="b9c0a-105">Согласие для конкретного ресурса (RSC) — это интеграция Microsoft Teams и API microsoft Graph, которая позволяет приложению использовать конечные точки API для управления определенными группами в организации.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-105">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="b9c0a-106">Модель разрешений, определенных для ресурсов( RSC), позволяет владельцам команд предоставлять согласие для приложения на доступ и/или изменение данных группы. </span><span class="sxs-lookup"><span data-stu-id="b9c0a-106">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="b9c0a-107">Детальное, Teams, RSC-разрешения определяют, что приложение может сделать в определенной группе:</span><span class="sxs-lookup"><span data-stu-id="b9c0a-107">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="b9c0a-108">Разрешения, определенные для ресурсов</span><span class="sxs-lookup"><span data-stu-id="b9c0a-108">Resource-specific permissions</span></span>

|<span data-ttu-id="b9c0a-109">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="b9c0a-109">Application permission</span></span>| <span data-ttu-id="b9c0a-110">Action</span><span class="sxs-lookup"><span data-stu-id="b9c0a-110">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="b9c0a-111">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-111">TeamSettings.Read.Group</span></span> | <span data-ttu-id="b9c0a-112">Получите параметры для этой группы.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-112">Get the settings for this team.</span></span>|
|<span data-ttu-id="b9c0a-113">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-113">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="b9c0a-114">Обновление параметров для команды.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-114">Update the settings for this team.</span></span>|
|<span data-ttu-id="b9c0a-115">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-115">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="b9c0a-116">Получите имена каналов, описания каналов и параметры канала для этой группы.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-116">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="b9c0a-117">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-117">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="b9c0a-118">Обновление имен каналов, описаний каналов и параметров канала для этой группы.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-118">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="b9c0a-119">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-119">Channel.Create.Group</span></span>|<span data-ttu-id="b9c0a-120">Создание каналов в этой команде.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-120">Create channels in this team.</span></span>|
|<span data-ttu-id="b9c0a-121">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-121">Channel.Delete.Group</span></span>|<span data-ttu-id="b9c0a-122">Удаление каналов в этой группе.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-122">Delete channels in this team.</span></span>|
|<span data-ttu-id="b9c0a-123">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-123">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="b9c0a-124">Получите сообщения канала этой группы.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-124">Get this team's channel messages.</span></span>|
|<span data-ttu-id="b9c0a-125">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-125">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="b9c0a-126">Получите список установленных приложений этой группы.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-126">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="b9c0a-127">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-127">TeamsTab.Read.Group</span></span>|<span data-ttu-id="b9c0a-128">Получите список вкладок этой группы.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-128">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="b9c0a-129">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-129">TeamsTab.Create.Group</span></span>|<span data-ttu-id="b9c0a-130">Создание вкладок в этой команде.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-130">Create tabs in this team.</span></span>|
|<span data-ttu-id="b9c0a-131">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-131">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="b9c0a-132">Обновление вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-132">Update this team's tabs.</span></span>|
|<span data-ttu-id="b9c0a-133">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-133">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="b9c0a-134">Удаление вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-134">Delete this team's tabs.</span></span>|
|<span data-ttu-id="b9c0a-135">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b9c0a-135">TeamMember.Read.Group</span></span>|<span data-ttu-id="b9c0a-136">Получите членов этой группы.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-136">Get this team's members.</span></span>|

>[!NOTE]
><span data-ttu-id="b9c0a-137">Разрешения на использование ресурсов доступны только Teams приложениям, установленным на клиенте Teams и в настоящее время не являются частью Azure Active Directory портала.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-137">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="b9c0a-138">Включить в приложении согласие, определенное для ресурсов</span><span class="sxs-lookup"><span data-stu-id="b9c0a-138">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="b9c0a-139">Действия для включения RSC в приложении следующие:</span><span class="sxs-lookup"><span data-stu-id="b9c0a-139">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="b9c0a-140">[Настройка параметров согласия владельца группы на портале Azure Active Directory.](#configure-group-owner-consent-settings-in-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-140">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="b9c0a-141">[Зарегистрируйте свое приложение платформа удостоверений Майкрософт с помощью портала Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-141">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="b9c0a-142">[Просмотрите разрешения приложений на портале Azure AD.](#review-your-application-permissions-in-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-142">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="b9c0a-143">[Получение маркера доступа с платформы Microsoft Identity.](#obtain-an-access-token-from-the-microsoft-identity-platform)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-143">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="b9c0a-144">[Обновление манифеста Teams приложения](#update-your-teams-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="b9c0a-144">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="b9c0a-145">[Установите приложение непосредственно в Teams.](#sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-145">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="b9c0a-146">[Проверьте приложение для дополнительных разрешений RSC](#check-your-app-for-added-rsc-permissions).</span><span class="sxs-lookup"><span data-stu-id="b9c0a-146">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="b9c0a-147">Настройка параметров согласия владельца группы на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9c0a-147">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="b9c0a-148">Вы можете включить или отключить согласие владельца [группы](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) непосредственно на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="b9c0a-148">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="b9c0a-149">Во входе на [портал Azure](https://portal.azure.com) в качестве [глобального администратора или администратора компании.](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-149">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="b9c0a-150">[Выберите](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory**  =>  **Enterprise приложения** Consent и  =>  **permissions** User consent  =>  **settings.**</span><span class="sxs-lookup"><span data-stu-id="b9c0a-150">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="b9c0a-151">Включить, отключить или ограничить согласие пользователя с согласия владельца группы с меткой управления для доступа к данным **приложений** (по умолчанию разрешается согласие владельца группы для всех **владельцев групп).**</span><span class="sxs-lookup"><span data-stu-id="b9c0a-151">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="b9c0a-152">Чтобы владелец группы устанавливал приложение с помощью RSC, для этого пользователя необходимо включить согласие владельца группы.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-152">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![конфигурация azure rsc](../../assets/images/azure-rsc-configuration.png)

<span data-ttu-id="b9c0a-154">Чтобы включить или отключить согласие владельца группы с помощью PowerShell, выполните действия, описанные в Настройка согласия владельца группы [с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-154">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="b9c0a-155">Регистрация приложения с помощью платформа удостоверений Майкрософт на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9c0a-155">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="b9c0a-156">Портал Azure Active Directory предоставляет центральную платформу для регистрации и настройки приложений.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-156">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="b9c0a-157">Ваше приложение должно быть зарегистрировано на портале Azure AD, чтобы интегрироваться с платформа удостоверений Майкрософт и вызвать API Graph Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-157">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="b9c0a-158">*Регистрация* [приложения с помощью платформа удостоверений Майкрософт.](/graph/auth-register-app-v2)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-158">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="b9c0a-159">Не регистрируйте несколько Teams приложений в один и тот же id приложения Azure AD. ID приложения должен быть уникальным для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-159">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="b9c0a-160">Попытки установить несколько приложений в один и тот же id приложения не удастся.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-160">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="b9c0a-161">Просмотр разрешений приложения на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9c0a-161">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="b9c0a-162">Перейдите на **страницу**  =>  **регистрации домашнего приложения** и выберите приложение RSC.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-162">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="b9c0a-163">Выберите **разрешения API** из левой панели nav и изучите список настроенных разрешений для приложения.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-163">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="b9c0a-164">Если ваше приложение будет только делать вызовы API Graph RSC, удалите все разрешения на этой странице.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-164">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="b9c0a-165">Если ваше приложение также будет звонить не RSC, храните эти разрешения по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-165">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b9c0a-166">Портал Azure AD не может использоваться для запроса разрешений RSC.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-166">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="b9c0a-167">Разрешения RSC в настоящее время являются исключительными для Teams приложений, установленных в клиенте Teams и объявляются в файле манифеста приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="b9c0a-167">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="b9c0a-168">Получение маркера доступа из платформа удостоверений Майкрософт</span><span class="sxs-lookup"><span data-stu-id="b9c0a-168">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="b9c0a-169">Чтобы сделать Graph API, необходимо получить маркер доступа для приложения с платформы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-169">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="b9c0a-170">Прежде чем приложение сможет получить маркер из платформа удостоверений Майкрософт, его необходимо зарегистрировать на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-170">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="b9c0a-171">Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-171">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="b9c0a-172">Для получения маркера доступа с платформы удостоверений необходимо иметь следующие значения из процесса регистрации Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b9c0a-172">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="b9c0a-173">ID **приложения,** присвоенный порталом регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-173">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="b9c0a-174">Если приложение поддерживает один вход (SSO), необходимо использовать тот же ID приложения для приложения и SSO.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-174">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="b9c0a-175">Секрет **клиента или пароль** или пара ключей общего и частного доступа **(сертификат).**</span><span class="sxs-lookup"><span data-stu-id="b9c0a-175">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="b9c0a-176">Это необязательно для нативных приложений;</span><span class="sxs-lookup"><span data-stu-id="b9c0a-176">This is not required for native apps.</span></span>
- <span data-ttu-id="b9c0a-177">URI **перенаправления** (или URL-адрес ответа) для вашего приложения для получения ответов из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-177">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="b9c0a-178">*См.* [статью Получить](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) доступ от имени пользователя и [получить доступ без пользователя](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-178">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="b9c0a-179">Обновление манифеста Teams приложения</span><span class="sxs-lookup"><span data-stu-id="b9c0a-179">Update your Teams app manifest</span></span>

<span data-ttu-id="b9c0a-180">Разрешения RSC объявляются в файле манифеста приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="b9c0a-180">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="b9c0a-181">Добавьте ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="b9c0a-181">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="b9c0a-182">**id** — ваш id приложения Azure AD. *Зарегистрируйте* свое приложение [на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-182">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="b9c0a-183">**ресурс**  — любая строка.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-183">**resource**  — any string.</span></span> <span data-ttu-id="b9c0a-184">Это поле не имеет операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа на ошибку; любая строка будет делать.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-184">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="b9c0a-185">**разрешения приложения** — разрешения RSC для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-185">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="b9c0a-186">*См.* [в руб. Разрешения, определенные для ресурсов.](resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-186">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="b9c0a-187">Разрешения не RSC хранятся на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-187">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="b9c0a-188">Не добавляйте их в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-188">Do not add them to the app manifest.</span></span>
>

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.ReadWrite.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.ReadWrite.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="b9c0a-189">Sideload ваше приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="b9c0a-189">Sideload your app in Teams</span></span>

<span data-ttu-id="b9c0a-190">Если администратор Teams позволяет настраивать загрузки приложений, [](~/concepts/deploy-and-publish/apps-upload.md) вы можете загрузить приложение непосредственно в определенную группу.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-190">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="b9c0a-191">Проверьте приложение на дополнительные разрешения RSC</span><span class="sxs-lookup"><span data-stu-id="b9c0a-191">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="b9c0a-192">Разрешения RSC не приписываются пользователю.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-192">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="b9c0a-193">Вызовы сделаны с разрешениями приложения, а не с делегированием разрешений пользователя.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-193">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="b9c0a-194">Таким образом, приложению может быть разрешено выполнять действия, которые не могут выполняться пользователем, например создание канала или удаление вкладки. Перед вызовами API RSC следует просмотреть намерения владельца группы по вашему делу использования.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-194">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="b9c0a-195">*Обзор* [Microsoft Teams API .](/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-195">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="b9c0a-196">После установки приложения в команду можно использовать [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) для просмотра разрешений, предоставленных приложению в команде:</span><span class="sxs-lookup"><span data-stu-id="b9c0a-196">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="b9c0a-197">Получите **группуId** группы из Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-197">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="b9c0a-198">В клиенте Teams выберите **Teams** из левого левого панели nav.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-198">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="b9c0a-199">Выберите команду, в которой установлено приложение из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-199">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="b9c0a-200">Выберите **значок Дополнительные** параметры (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="b9c0a-200">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="b9c0a-201">Выберите **Получить ссылку на команду**.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-201">Select **Get link to team**.</span></span>
> - <span data-ttu-id="b9c0a-202">Скопируйте и сохраните **значение groupId** из строки.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-202">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="b9c0a-203">Войдите **в Graph Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-203">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="b9c0a-204">Вызов **GET на** следующую конечную точку: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` .</span><span class="sxs-lookup"><span data-stu-id="b9c0a-204">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="b9c0a-205">Поле clientAppId в ответе будет соедино с приложением, указанным в манифесте Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-205">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="b9c0a-206">![Graph ответ обозревателя на вызов GET.](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-206">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="b9c0a-207">Пример кода</span><span class="sxs-lookup"><span data-stu-id="b9c0a-207">Code sample</span></span>
| <span data-ttu-id="b9c0a-208">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="b9c0a-208">**Sample name**</span></span> | <span data-ttu-id="b9c0a-209">**Description**</span><span class="sxs-lookup"><span data-stu-id="b9c0a-209">**Description**</span></span> | <span data-ttu-id="b9c0a-210">**.NET**</span><span class="sxs-lookup"><span data-stu-id="b9c0a-210">**.NET**</span></span> |<span data-ttu-id="b9c0a-211">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="b9c0a-211">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="b9c0a-212">Конкретное согласие ресурса (RSC)</span><span class="sxs-lookup"><span data-stu-id="b9c0a-212">Resource Specific Consent (RSC)</span></span> | <span data-ttu-id="b9c0a-213">Используйте RSC для вызова Graph API.</span><span class="sxs-lookup"><span data-stu-id="b9c0a-213">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="b9c0a-214">View</span><span class="sxs-lookup"><span data-stu-id="b9c0a-214">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="b9c0a-215">View</span><span class="sxs-lookup"><span data-stu-id="b9c0a-215">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="test-resource-specific-consent"></a><span data-ttu-id="b9c0a-216">Проверка согласия на конкретные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b9c0a-216">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="b9c0a-217">**Тестирование разрешений на согласие для определенных ресурсов в Teams**</span><span class="sxs-lookup"><span data-stu-id="b9c0a-217">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="b9c0a-218">Связанная тема для Teams администраторов</span><span class="sxs-lookup"><span data-stu-id="b9c0a-218">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9c0a-219">**Согласие на определенные ресурсы в Microsoft Teams для администраторов**</span><span class="sxs-lookup"><span data-stu-id="b9c0a-219">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 

