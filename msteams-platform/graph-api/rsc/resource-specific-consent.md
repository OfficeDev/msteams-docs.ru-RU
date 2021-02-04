---
title: Согласие для определенных ресурсов в Teams
description: В этой статье описывается согласие на определенные ресурсы в Teams и его преимущества.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: RSC-граф AAD для авторизации OAuth
ms.openlocfilehash: 1b5c0f645d93ed33c11bf3279e70133f35f53a2c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093931"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="4ec39-104">Согласие для определенных ресурсов (RSC)</span><span class="sxs-lookup"><span data-stu-id="4ec39-104">Resource-specific consent (RSC)</span></span>

<span data-ttu-id="4ec39-105">Согласие для определенных ресурсов (RSC) — это интеграция Microsoft Teams и API Microsoft Graph, которая позволяет приложению использовать конечные точки API для управления определенными командами в организации.</span><span class="sxs-lookup"><span data-stu-id="4ec39-105">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="4ec39-106">Модель разрешений на предоставление разрешений для определенных ресурсов (RSC) позволяет владельцам команд предоставлять приложению согласие на доступ к данным команды и(или) изменение их данных. </span><span class="sxs-lookup"><span data-stu-id="4ec39-106">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="4ec39-107">Детализированное разрешение RSC для Teams определяет, что приложение может делать в определенной команде:</span><span class="sxs-lookup"><span data-stu-id="4ec39-107">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="4ec39-108">Разрешения для определенных ресурсов</span><span class="sxs-lookup"><span data-stu-id="4ec39-108">Resource-specific permissions</span></span>

|<span data-ttu-id="4ec39-109">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="4ec39-109">Application permission</span></span>| <span data-ttu-id="4ec39-110">Действие</span><span class="sxs-lookup"><span data-stu-id="4ec39-110">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="4ec39-111">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-111">TeamSettings.Read.Group</span></span> | <span data-ttu-id="4ec39-112">Получите параметры для этой команды.</span><span class="sxs-lookup"><span data-stu-id="4ec39-112">Get the settings for this team.</span></span>|
|<span data-ttu-id="4ec39-113">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-113">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="4ec39-114">Обновление параметров для команды.</span><span class="sxs-lookup"><span data-stu-id="4ec39-114">Update the settings for this team.</span></span>|
|<span data-ttu-id="4ec39-115">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-115">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="4ec39-116">Получите имена каналов, описания каналов и параметры канала для этой команды.</span><span class="sxs-lookup"><span data-stu-id="4ec39-116">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="4ec39-117">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-117">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="4ec39-118">Обновление имен каналов, описаний каналов и параметров каналов для этой команды.</span><span class="sxs-lookup"><span data-stu-id="4ec39-118">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="4ec39-119">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-119">Channel.Create.Group</span></span>|<span data-ttu-id="4ec39-120">Создание каналов в этой команде.</span><span class="sxs-lookup"><span data-stu-id="4ec39-120">Create channels in this team.</span></span>|
|<span data-ttu-id="4ec39-121">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-121">Channel.Delete.Group</span></span>|<span data-ttu-id="4ec39-122">Удалите каналы в этой команде.</span><span class="sxs-lookup"><span data-stu-id="4ec39-122">Delete channels in this team.</span></span>|
|<span data-ttu-id="4ec39-123">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-123">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="4ec39-124">Получите сообщения канала этой команды.</span><span class="sxs-lookup"><span data-stu-id="4ec39-124">Get this team's channel messages.</span></span>|
|<span data-ttu-id="4ec39-125">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-125">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="4ec39-126">Получите список установленных приложений этой команды.</span><span class="sxs-lookup"><span data-stu-id="4ec39-126">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="4ec39-127">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-127">TeamsTab.Read.Group</span></span>|<span data-ttu-id="4ec39-128">Получите список вкладок команды.</span><span class="sxs-lookup"><span data-stu-id="4ec39-128">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="4ec39-129">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-129">TeamsTab.Create.Group</span></span>|<span data-ttu-id="4ec39-130">Создание вкладок в этой команде.</span><span class="sxs-lookup"><span data-stu-id="4ec39-130">Create tabs in this team.</span></span>|
|<span data-ttu-id="4ec39-131">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-131">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="4ec39-132">Обновление вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="4ec39-132">Update this team's tabs.</span></span>|
|<span data-ttu-id="4ec39-133">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-133">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="4ec39-134">Удаление вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="4ec39-134">Delete this team's tabs.</span></span>|
|<span data-ttu-id="4ec39-135">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4ec39-135">TeamMember.Read.Group</span></span>|<span data-ttu-id="4ec39-136">Получите участников этой команды.</span><span class="sxs-lookup"><span data-stu-id="4ec39-136">Get this team's members.</span></span>|

>[!NOTE]
><span data-ttu-id="4ec39-137">Разрешения для определенных ресурсов доступны только приложениям Teams, установленным в клиенте Teams и в настоящее время не являются частью портала Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ec39-137">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="4ec39-138">Включить согласие для определенных ресурсов в приложении</span><span class="sxs-lookup"><span data-stu-id="4ec39-138">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="4ec39-139">Для включения RSC в приложении выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4ec39-139">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="4ec39-140">[Настройка параметров согласия владельца группы на портале Azure Active Directory.](#configure-group-owner-consent-settings-in-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="4ec39-140">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="4ec39-141">[Зарегистрируйте свое приложение с помощью платформы удостоверений Майкрософт на портале Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="4ec39-141">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="4ec39-142">[Просмотрите разрешения приложений на портале Azure AD.](#review-your-application-permissions-in-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="4ec39-142">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="4ec39-143">[Получите маркер доступа от платформы удостоверений Майкрософт.](#obtain-an-access-token-from-the-microsoft-identity-platform)</span><span class="sxs-lookup"><span data-stu-id="4ec39-143">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="4ec39-144">[Обновите манифест приложения Teams.](#update-your-teams-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="4ec39-144">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="4ec39-145">[Установите приложение непосредственно в Teams.](#install-your-app-directly-in-teams)</span><span class="sxs-lookup"><span data-stu-id="4ec39-145">[Install your app directly in Teams](#install-your-app-directly-in-teams).</span></span>
1. <span data-ttu-id="4ec39-146">[Проверьте, нет ли в приложении дополнительных разрешений RSC.](#check-your-app-for-added-rsc-permissions)</span><span class="sxs-lookup"><span data-stu-id="4ec39-146">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="4ec39-147">Настройка параметров согласия владельца группы на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ec39-147">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="4ec39-148">Вы можете включить или отключить [согласие владельца группы](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) непосредственно на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="4ec39-148">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="4ec39-149">Во sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span><span class="sxs-lookup"><span data-stu-id="4ec39-149">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="4ec39-150">[Выберите](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **для корпоративных приложений Azure Active Directory** параметры согласия пользователя и  =>    =>    =>  **разрешения.**</span><span class="sxs-lookup"><span data-stu-id="4ec39-150">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="4ec39-151">Включать, отключать или ограничивать согласие пользователя с согласия владельца группы с меткой на управление для приложений, которые имеют доступ к данным **(по** умолчанию разрешается согласие владельца группы для **всех владельцев группы).**</span><span class="sxs-lookup"><span data-stu-id="4ec39-151">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="4ec39-152">Чтобы владелец группы устанавливал приложение с помощью RSC, для этого пользователя должно быть включено согласие владельца группы.</span><span class="sxs-lookup"><span data-stu-id="4ec39-152">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![Конфигурация azure rsc](../../assets/images/azure-rsc-configuration.png)

<span data-ttu-id="4ec39-154">Чтобы включить или отключить согласие владельца группы с помощью PowerShell, выполните действия, описанные в описании настройки согласия владельца группы [с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)</span><span class="sxs-lookup"><span data-stu-id="4ec39-154">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="4ec39-155">Регистрация приложения с помощью платформы удостоверений Майкрософт на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ec39-155">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="4ec39-156">Портал Azure Active Directory предоставляет центральную платформу для регистрации и настройки приложений.</span><span class="sxs-lookup"><span data-stu-id="4ec39-156">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="4ec39-157">Ваше приложение должно быть зарегистрировано на портале Azure AD для интеграции с платформой удостоверений Майкрософт и вызова API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="4ec39-157">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="4ec39-158">*См.* [статью "Регистрация приложения с помощью платформы удостоверений Майкрософт".](/graph/auth-register-app-v2)</span><span class="sxs-lookup"><span data-stu-id="4ec39-158">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="4ec39-159">Не регистрируйте несколько приложений Teams в одном и том же ИД приложения Azure AD. ИД приложения должен быть уникальным для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="4ec39-159">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="4ec39-160">Попытки установить несколько приложений с одинаковым ид приложения не удастся.</span><span class="sxs-lookup"><span data-stu-id="4ec39-160">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="4ec39-161">Просмотр разрешений приложения на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ec39-161">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="4ec39-162">Перейдите на **страницу**  =>  **регистрации домашнего** приложения и выберите приложение RSC.</span><span class="sxs-lookup"><span data-stu-id="4ec39-162">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="4ec39-163">Выберите **разрешения API** на левой панели nav и изучите список настроенных разрешений для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="4ec39-163">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="4ec39-164">Если ваше приложение будет делать только вызовы API Graph RSC, удалите все разрешения на этой странице.</span><span class="sxs-lookup"><span data-stu-id="4ec39-164">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="4ec39-165">Если ваше приложение также будет делать вызовы без RSC, при необходимости оохраните эти разрешения.</span><span class="sxs-lookup"><span data-stu-id="4ec39-165">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="4ec39-166">Портал Azure AD нельзя использовать для запроса разрешений RSC.</span><span class="sxs-lookup"><span data-stu-id="4ec39-166">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="4ec39-167">В настоящее время разрешения RSC являются монопольными для приложений Teams, установленных в клиенте Teams, и объявляются в файле манифеста приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="4ec39-167">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="4ec39-168">Получение маркера доступа от платформы удостоверений Майкрософт</span><span class="sxs-lookup"><span data-stu-id="4ec39-168">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="4ec39-169">Чтобы сделать вызовы API Graph, необходимо получить маркер доступа для приложения из платформы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4ec39-169">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="4ec39-170">Прежде чем приложение сможет получить маркер от платформы удостоверений Майкрософт, оно должно быть зарегистрировано на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ec39-170">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="4ec39-171">Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="4ec39-171">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="4ec39-172">Для получения маркера доступа с платформы удостоверений вам потребуется получить следующие значения из процесса регистрации Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4ec39-172">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="4ec39-173">ИД **приложения,** присвоенный порталом регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="4ec39-173">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="4ec39-174">Если ваше приложение поддерживает единый вход( SSO), следует использовать тот же ИД приложения для вашего приложения и SSO.</span><span class="sxs-lookup"><span data-stu-id="4ec39-174">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="4ec39-175">Секрет **клиента или пароль или** пара открытых и закрытых ключей **(сертификат).**</span><span class="sxs-lookup"><span data-stu-id="4ec39-175">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="4ec39-176">Это необязательно для нативных приложений;</span><span class="sxs-lookup"><span data-stu-id="4ec39-176">This is not required for native apps.</span></span>
- <span data-ttu-id="4ec39-177">URI **перенаправления** (или URL-адрес ответа) для вашего приложения, чтобы получать ответы от Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ec39-177">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="4ec39-178">*См.* ["Получить доступ от имени пользователя"](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) и ["Получить доступ без пользователя"](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="4ec39-178">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="4ec39-179">Обновление манифеста приложения Teams</span><span class="sxs-lookup"><span data-stu-id="4ec39-179">Update your Teams app manifest</span></span>

<span data-ttu-id="4ec39-180">Разрешения RSC объявляются в файле манифеста приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="4ec39-180">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="4ec39-181">Добавьте ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="4ec39-181">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="4ec39-182">**id** — ваш ид приложения Azure AD. *Зарегистрируйте* свое [приложение на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="4ec39-182">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="4ec39-183">**ресурс**  — любая строка.</span><span class="sxs-lookup"><span data-stu-id="4ec39-183">**resource**  — any string.</span></span> <span data-ttu-id="4ec39-184">Это поле не имеет операции в RSC, но его необходимо добавить и иметь значение, чтобы избежать ошибки; любая строка будет делать.</span><span class="sxs-lookup"><span data-stu-id="4ec39-184">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="4ec39-185">**разрешения приложения —** RSC-разрешения для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="4ec39-185">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="4ec39-186">*См.* ["Разрешения для определенных ресурсов".](resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="4ec39-186">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="4ec39-187">Не RSC-разрешения хранятся на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec39-187">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="4ec39-188">Не добавляйте их в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="4ec39-188">Do not add them to the app manifest.</span></span>
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

## <a name="install-your-app-directly-in-teams"></a><span data-ttu-id="4ec39-189">Установка приложения непосредственно в Teams</span><span class="sxs-lookup"><span data-stu-id="4ec39-189">Install your app directly in Teams</span></span>

<span data-ttu-id="4ec39-190">После создания приложения вы можете [](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) отправить пакет приложения непосредственно определенной команде.</span><span class="sxs-lookup"><span data-stu-id="4ec39-190">Once you've created your app you can [upload your app package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directly to a specific team.</span></span>  <span data-ttu-id="4ec39-191">Для этого необходимо включить **параметр** политики отправки настраиваемого приложения в рамках настраиваемой политики установки приложений.</span><span class="sxs-lookup"><span data-stu-id="4ec39-191">To do so, the **Upload custom apps** policy setting must be enabled as part of the custom app setup policies.</span></span> <span data-ttu-id="4ec39-192">*См.* [параметры настраиваемой политики приложений.](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)</span><span class="sxs-lookup"><span data-stu-id="4ec39-192">*See* [Custom app policy settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="4ec39-193">Проверка добавленных разрешений RSC в приложении</span><span class="sxs-lookup"><span data-stu-id="4ec39-193">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="4ec39-194">Разрешения RSC не связаны с пользователем.</span><span class="sxs-lookup"><span data-stu-id="4ec39-194">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="4ec39-195">Вызовы веются с разрешениями приложения, а не делегными разрешениями пользователя.</span><span class="sxs-lookup"><span data-stu-id="4ec39-195">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="4ec39-196">Таким образом, приложению может быть разрешено выполнять действия, которые пользователь не может выполнять, например создание канала или удаление вкладки. Перед вызовами API RSC вам следует проанализировать намерение владельца команды в отношении вашего случая использования.</span><span class="sxs-lookup"><span data-stu-id="4ec39-196">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="4ec39-197">*См.* [обзор API Microsoft Teams.](/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="4ec39-197">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="4ec39-198">После установки приложения в команде вы можете использовать [проводник Graph](https://developer.microsoft.com/graph/graph-explorer)  для просмотра разрешений, предоставленных приложению в команде:</span><span class="sxs-lookup"><span data-stu-id="4ec39-198">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="4ec39-199">Получите **groupId** команды из клиента Teams.</span><span class="sxs-lookup"><span data-stu-id="4ec39-199">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="4ec39-200">В клиенте Teams выберите **Teams** на левой панели.</span><span class="sxs-lookup"><span data-stu-id="4ec39-200">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="4ec39-201">Выберите команду, в которой установлено приложение, в выпадаемом меню.</span><span class="sxs-lookup"><span data-stu-id="4ec39-201">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="4ec39-202">Выберите **значок "Дополнительные параметры"** (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="4ec39-202">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="4ec39-203">Выберите **"Получить ссылку на команду".**</span><span class="sxs-lookup"><span data-stu-id="4ec39-203">Select **Get link to team**.</span></span>
> - <span data-ttu-id="4ec39-204">Скопируйте и **сохраните значение groupId** из строки.</span><span class="sxs-lookup"><span data-stu-id="4ec39-204">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="4ec39-205">Войдите в **обозреватель Graph.**</span><span class="sxs-lookup"><span data-stu-id="4ec39-205">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="4ec39-206">Сделайте **вызов GET** для следующей конечной точки: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` .</span><span class="sxs-lookup"><span data-stu-id="4ec39-206">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="4ec39-207">Поле clientAppId в отклике со картой appId, указанным в манифесте приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="4ec39-207">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="4ec39-208">![Ответ обозревателя Graph на вызов GET.](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="4ec39-208">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>
 
## <a name="test-resource-specific-consent"></a><span data-ttu-id="4ec39-209">Проверка согласия для определенных ресурсов</span><span class="sxs-lookup"><span data-stu-id="4ec39-209">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="4ec39-210">**Проверка разрешений на согласие для определенных ресурсов в Teams**</span><span class="sxs-lookup"><span data-stu-id="4ec39-210">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="4ec39-211">Связанный раздел для администраторов Teams</span><span class="sxs-lookup"><span data-stu-id="4ec39-211">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ec39-212">**Согласие администраторов в Microsoft Teams для определенных ресурсов**</span><span class="sxs-lookup"><span data-stu-id="4ec39-212">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 
