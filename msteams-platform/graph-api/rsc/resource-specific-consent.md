---
title: Согласие на ресурсы в Teams
description: Описание согласия на ресурсы в Teams и способы его использования.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams Authorization OAuth SSO AAD rsc Graph
ms.openlocfilehash: 7e3fc3faa111f4ba982c1c79e6b5b873b8773aef
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819184"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="7df18-104">Согласие на ресурсы (RSC)</span><span class="sxs-lookup"><span data-stu-id="7df18-104">Resource-specific consent (RSC)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="7df18-105">Эти API доступны в конечной https://graph.microsoft.com/beta точке.</span><span class="sxs-lookup"><span data-stu-id="7df18-105">These APIs are accessible in the https://graph.microsoft.com/beta endpoint.</span></span>  <span data-ttu-id="7df18-106">Конечная [точка версии бета-версии](/graph/versioning-and-support#beta-version) включает API-интерфейсы, которые в настоящий момент находятся в предварительной версии и не являются общедоступными.</span><span class="sxs-lookup"><span data-stu-id="7df18-106">The [beta version](/graph/versioning-and-support#beta-version) endpoint includes APIs that are currently in preview and are not yet generally available.</span></span> <span data-ttu-id="7df18-107">API-интерфейсы в конечной точке бета-версий могут меняться, и мы не рекомендуем использовать их в рабочих приложениях.</span><span class="sxs-lookup"><span data-stu-id="7df18-107">The APIs in the beta endpoint are subject to change and we don't recommend that you use them in your production apps.</span></span> 

<span data-ttu-id="7df18-108">Согласие на ресурсы (RSC) — это интеграция API Microsoft Teams и Graph, позволяющая приложению использовать конечные точки API для управления определенными командами в организации.</span><span class="sxs-lookup"><span data-stu-id="7df18-108">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="7df18-109">Модель разрешений RSC позволяет владельцам *группы* дать приложению разрешение на доступ к его данным и/или изменение.</span><span class="sxs-lookup"><span data-stu-id="7df18-109">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="7df18-110">Детальные разрешения RSC для Teams определяют возможности приложения в конкретной команде:</span><span class="sxs-lookup"><span data-stu-id="7df18-110">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="7df18-111">Разрешения для конкретных ресурсов</span><span class="sxs-lookup"><span data-stu-id="7df18-111">Resource-specific permissions</span></span>

|<span data-ttu-id="7df18-112">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="7df18-112">Application permission</span></span>| <span data-ttu-id="7df18-113">Действие</span><span class="sxs-lookup"><span data-stu-id="7df18-113">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="7df18-114">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-114">TeamSettings.Read.Group</span></span> | <span data-ttu-id="7df18-115">Получение параметров для команды.</span><span class="sxs-lookup"><span data-stu-id="7df18-115">Get the settings for this team.</span></span>|
|<span data-ttu-id="7df18-116">TeamSettings.Edit.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-116">TeamSettings.Edit.Group</span></span>|<span data-ttu-id="7df18-117">Обновите параметры для этой команды.</span><span class="sxs-lookup"><span data-stu-id="7df18-117">Update the settings for this team.</span></span>|
|<span data-ttu-id="7df18-118">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-118">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="7df18-119">Получение имен каналов, описаний каналов и параметров каналов для этой команды.</span><span class="sxs-lookup"><span data-stu-id="7df18-119">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="7df18-120">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-120">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="7df18-121">Обновите имена каналов, описания каналов и параметры каналов для этой команды.</span><span class="sxs-lookup"><span data-stu-id="7df18-121">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="7df18-122">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-122">Channel.Create.Group</span></span>|<span data-ttu-id="7df18-123">Создание каналов в этой команде.</span><span class="sxs-lookup"><span data-stu-id="7df18-123">Create channels in this team.</span></span>|
|<span data-ttu-id="7df18-124">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-124">Channel.Delete.Group</span></span>|<span data-ttu-id="7df18-125">Удаление каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="7df18-125">Delete channels in this team.</span></span>|
|<span data-ttu-id="7df18-126">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-126">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="7df18-127">Получение сообщений канала этой команды.</span><span class="sxs-lookup"><span data-stu-id="7df18-127">Get this team's channel messages.</span></span>|
|<span data-ttu-id="7df18-128">TeamsApp.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-128">TeamsApp.Read.Group</span></span>|<span data-ttu-id="7df18-129">Получение списка установленных приложений этой команды.</span><span class="sxs-lookup"><span data-stu-id="7df18-129">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="7df18-130">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-130">TeamsTab.Read.Group</span></span>|<span data-ttu-id="7df18-131">Получение списка вкладок этой группы.</span><span class="sxs-lookup"><span data-stu-id="7df18-131">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="7df18-132">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-132">TeamsTab.Create.Group</span></span>|<span data-ttu-id="7df18-133">Создание вкладок в этой команде.</span><span class="sxs-lookup"><span data-stu-id="7df18-133">Create tabs in this team.</span></span>|
|<span data-ttu-id="7df18-134">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-134">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="7df18-135">Обновляйте вкладки этой команды.</span><span class="sxs-lookup"><span data-stu-id="7df18-135">Update this team's tabs.</span></span>|
|<span data-ttu-id="7df18-136">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-136">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="7df18-137">Удаление вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="7df18-137">Delete this team's tabs.</span></span>|
|<span data-ttu-id="7df18-138">Member.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-138">Member.Read.Group</span></span>|<span data-ttu-id="7df18-139">Получение участников команды.</span><span class="sxs-lookup"><span data-stu-id="7df18-139">Get this team's members.</span></span>|
|<span data-ttu-id="7df18-140">Owner.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7df18-140">Owner.Read.Group</span></span>|<span data-ttu-id="7df18-141">Получение владельцев команды.</span><span class="sxs-lookup"><span data-stu-id="7df18-141">Get this team's owners.</span></span>|

>[!NOTE]
><span data-ttu-id="7df18-142">Разрешения для конкретных ресурсов доступны только приложениям Teams, установленным в клиенте Teams и в настоящее время не являются частью портала Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7df18-142">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="7df18-143">Включение согласия для ресурсов в приложении</span><span class="sxs-lookup"><span data-stu-id="7df18-143">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="7df18-144">Для включения RSC в приложении выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7df18-144">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="7df18-145">[Настройте параметры согласия владельца группы на портале Azure Active Directory.](#configure-group-owner-consent-settings-in-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="7df18-145">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="7df18-146">[Регистрация приложения с помощью платформы удостоверений Майкрософт на портале Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="7df18-146">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. [<span data-ttu-id="7df18-147">Проверьте разрешения приложений на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="7df18-147">Review your application permissions in the Azure AD portal</span></span>](#review-your-application-permissions-in-the-azure-ad-portal)
1. <span data-ttu-id="7df18-148">[Получите маркер доступа с платформы удостоверений Майкрософт.](#obtain-an-access-token-from-the-microsoft-identity-platform)</span><span class="sxs-lookup"><span data-stu-id="7df18-148">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="7df18-149">[Обновите манифест приложения Teams.](#update-your-teams-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="7df18-149">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="7df18-150">[Установите приложение непосредственно в Teams.](#install-your-app-directly-in-teams)</span><span class="sxs-lookup"><span data-stu-id="7df18-150">[Install your app directly in Teams](#install-your-app-directly-in-teams).</span></span>
1. <span data-ttu-id="7df18-151">[Проверьте, как в вашем приложении предоставлены разрешения, предоставленные для RSC-каналов.](#check-your-app-for-added-rsc-permissions)</span><span class="sxs-lookup"><span data-stu-id="7df18-151">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="7df18-152">Настройка параметров согласия владельца группы на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="7df18-152">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="7df18-153">Вы можете включать и  [отключать согласие](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) владельцев группы непосредственно на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="7df18-153">You can enable or disable  [group owner consent](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="7df18-154">Войдите на портал [Azure под учетной](https://portal.azure.com) [записью глобального администратора или администратора организации.](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)</span><span class="sxs-lookup"><span data-stu-id="7df18-154">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="7df18-155">Выберите **параметры пользователя для**  => **корпоративных приложений**Azure Active  => **User settings**Directory.</span><span class="sxs-lookup"><span data-stu-id="7df18-155">Select **Azure Active Directory** =>**Enterprise applications** =>**User settings**.</span></span>
> - <span data-ttu-id="7df18-156">Разрешать, отключать или ограничивать согласие пользователя с помощью контролировщика "Пользователи могут разрешать" доступ к приложениям **для принадлежащих им групп** (эта возможность включена по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="7df18-156">Enable, disable, or limit user consent with the control labeled **Users can consent to apps accessing company data for the groups they own** (This capability is enabled by default).</span></span>

![Конфигурация azure rsc](../../assets/images/azure-rsc-configuration.svg)

| <span data-ttu-id="7df18-158">Значение</span><span class="sxs-lookup"><span data-stu-id="7df18-158">Value</span></span> | <span data-ttu-id="7df18-159">Описание</span><span class="sxs-lookup"><span data-stu-id="7df18-159">Description</span></span>|
|--- | --- |
|<span data-ttu-id="7df18-160">Да</span><span class="sxs-lookup"><span data-stu-id="7df18-160">Yes</span></span> | <span data-ttu-id="7df18-161">Включение согласия для группы для всех владельцев групп.</span><span class="sxs-lookup"><span data-stu-id="7df18-161">Enable group-specific consent for all group owners.</span></span>|
|<span data-ttu-id="7df18-162">Нет</span><span class="sxs-lookup"><span data-stu-id="7df18-162">No</span></span> |<span data-ttu-id="7df18-163">Отключите согласие для группы для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="7df18-163">Disable group-specific consent for all users.</span></span>| 
|<span data-ttu-id="7df18-164">Ограничено</span><span class="sxs-lookup"><span data-stu-id="7df18-164">Limited</span></span> | <span data-ttu-id="7df18-165">Включение согласия для групп для участников выбранной группы.</span><span class="sxs-lookup"><span data-stu-id="7df18-165">Enable group-specific consent for members of a selected group.</span></span>|

<span data-ttu-id="7df18-166">Чтобы включить или отключить согласие владельца группы на портале Azure с помощью PowerShell, выполните действия, описанные в разделе ["Настройка согласия владельца группы с помощью PowerShell".](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell)</span><span class="sxs-lookup"><span data-stu-id="7df18-166">To enable or disable group owner consent within the Azure portal using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="7df18-167">Регистрация приложения на платформе удостоверений Майкрософт на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="7df18-167">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="7df18-168">Портал Azure Active Directory представляет собой центральную платформу для регистрации и настройки приложений.</span><span class="sxs-lookup"><span data-stu-id="7df18-168">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="7df18-169">Ваше приложение должно быть зарегистрировано на портале Azure AD, чтобы интегрироватьегоего его с платформой удостоверений Майкрософт и вызывать API Graph.</span><span class="sxs-lookup"><span data-stu-id="7df18-169">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Graph APIs.</span></span> <span data-ttu-id="7df18-170">*См.* [раздел "Регистрация приложения с помощью платформы удостоверений Майкрософт".](/graph/auth-register-app-v2)</span><span class="sxs-lookup"><span data-stu-id="7df18-170">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="7df18-171">Не регистрируйте несколько приложений Teams с одинаковым идентификатором приложения Azure AD. Идентификатор приложения должен быть уникальным для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="7df18-171">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="7df18-172">Попытки установить несколько приложений с один и тем же идентификатором приложения завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="7df18-172">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="7df18-173">Проверьте разрешения приложений на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="7df18-173">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="7df18-174">Перейдите на **страницу**  =>  **регистрации домашнего приложения** и выберите свое RSC-приложение.</span><span class="sxs-lookup"><span data-stu-id="7df18-174">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="7df18-175">Выберите **разрешения API** из левой панели навигации и проверьте список настроенных разрешений для приложения.</span><span class="sxs-lookup"><span data-stu-id="7df18-175">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="7df18-176">Если ваше приложение будет выполнять только вызовы RSC Graph, удалите все разрешения на этой странице.</span><span class="sxs-lookup"><span data-stu-id="7df18-176">If your app will only make RSC Graph calls, delete all the permission on that page.</span></span> <span data-ttu-id="7df18-177">Если ваше приложение также будет выполнять вызовы, не использующие поддержку RSC, не забудьте эти разрешения по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="7df18-177">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="7df18-178">Невозможно использовать портал Azure AD для запроса разрешений RSC.</span><span class="sxs-lookup"><span data-stu-id="7df18-178">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="7df18-179">Разрешения RSC в настоящее время используются только для приложений Teams, установленных в клиенте Teams и объявляются в файле манифеста приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="7df18-179">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="7df18-180">Получите маркер доступа от платформы удостоверений Майкрософт</span><span class="sxs-lookup"><span data-stu-id="7df18-180">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="7df18-181">Для вызова API Graph необходимо получить маркер доступа для приложения с платформы идентификации.</span><span class="sxs-lookup"><span data-stu-id="7df18-181">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="7df18-182">Чтобы приложение сможет получить маркер от платформы удостоверений Майкрософт, оно должно быть зарегистрировано на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7df18-182">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="7df18-183">Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="7df18-183">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="7df18-184">Вам потребуются следующие значения из процесса регистрации Azure AD, чтобы получать маркер доступа из платформы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7df18-184">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="7df18-185">Идентификатор **приложения,** назначенный порталом регистрации.</span><span class="sxs-lookup"><span data-stu-id="7df18-185">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="7df18-186">Если ваше приложение поддерживает единый вход, следует использовать для приложения и единого входа один и тот же идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="7df18-186">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="7df18-187">**Секрет/пароль клиента** либо открытый и закрытый ключ (**сертификат).**</span><span class="sxs-lookup"><span data-stu-id="7df18-187">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="7df18-188">Это необязательно для нативных приложений;</span><span class="sxs-lookup"><span data-stu-id="7df18-188">This is not required for native apps.</span></span>
- <span data-ttu-id="7df18-189">**URI перенаправления** (или URL-адрес ответа), с помощью которого приложение будет получать отклики от Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7df18-189">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="7df18-190">*Просмотр* [сведений о доступе от имени пользователя и](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) получение [доступа без пользователя](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="7df18-190">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="7df18-191">Обновление манифеста приложения Teams</span><span class="sxs-lookup"><span data-stu-id="7df18-191">Update your Teams app manifest</span></span>

<span data-ttu-id="7df18-192">Разрешения RSC объявляются в файле манифеста приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="7df18-192">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="7df18-193">Добавьте [ключ webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="7df18-193">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="7df18-194">**id** — идентификатор приложения Azure AD. *См.* ["Регистрация приложения" на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="7df18-194">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="7df18-195">**resource —**  любая строка.</span><span class="sxs-lookup"><span data-stu-id="7df18-195">**resource**  — any string.</span></span> <span data-ttu-id="7df18-196">Это поле не имеет операций в RSC, но его необходимо добавить и значение, чтобы избежать отклика с ошибкой; любая строка выполнит это.</span><span class="sxs-lookup"><span data-stu-id="7df18-196">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="7df18-197">**разрешения приложений** — разрешения RSC для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7df18-197">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="7df18-198">*См.* [разрешения для конкретных ресурсов.](resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="7df18-198">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="7df18-199">Разрешения, не относящиеся к RSC, хранятся на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7df18-199">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="7df18-200">Не добавляйте их в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="7df18-200">Do not add them to the app manifest.</span></span>
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

## <a name="install-your-app-directly-in-teams"></a><span data-ttu-id="7df18-201">Установка приложения непосредственно в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7df18-201">Install your app directly in Teams</span></span>

<span data-ttu-id="7df18-202">После создания приложения можно отправить пакет [приложения непосредственно](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) определенной команде.</span><span class="sxs-lookup"><span data-stu-id="7df18-202">Once you've created your app you can [upload your app package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directly to a specific team.</span></span>  <span data-ttu-id="7df18-203">Для этого параметр **политики "Отправить пользовательские приложения"** должен быть включен в рамках настраиваемых политик настройки приложений.</span><span class="sxs-lookup"><span data-stu-id="7df18-203">To do so, the **Upload custom apps** policy setting must be enabled as part of the custom app setup policies.</span></span> <span data-ttu-id="7df18-204">*См.* ["Настраиваемые параметры политики приложений".](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)</span><span class="sxs-lookup"><span data-stu-id="7df18-204">*See* [Custom app policy settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="7df18-205">Проверьте добавляемые разрешения для RSC в приложении</span><span class="sxs-lookup"><span data-stu-id="7df18-205">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="7df18-206">Разрешения RSC не обращаются к пользователю.</span><span class="sxs-lookup"><span data-stu-id="7df18-206">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="7df18-207">Вызовы касаются разрешений приложения, а не делегированных пользователем разрешений.</span><span class="sxs-lookup"><span data-stu-id="7df18-207">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="7df18-208">Поэтому приложению может быть разрешено выполнять действия, которые не могут выполняться пользователю (например, создать канал или удалять вкладку). Перед вызовами API RSC следует просмотреть намерения владельца команды об вашем варианте использования.</span><span class="sxs-lookup"><span data-stu-id="7df18-208">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="7df18-209">*Ознакомьтесь* [с обзором API Microsoft Teams.](/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="7df18-209">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="7df18-210">После установки приложения в команде вы можете просматривать разрешения, предоставленные приложению в команде, с помощью песочницы [Graph.](https://developer.microsoft.com/graph/graph-explorer)</span><span class="sxs-lookup"><span data-stu-id="7df18-210">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="7df18-211">Получение идентификатора **группы команды** из клиента Teams.</span><span class="sxs-lookup"><span data-stu-id="7df18-211">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="7df18-212">В клиенте Teams выберите **Teams** на левой левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="7df18-212">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="7df18-213">Выберите команду, в которой устанавливается приложение, из раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="7df18-213">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="7df18-214">Щелкните **значок "Дополнительные** параметры" (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="7df18-214">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="7df18-215">Выберите **"Получить ссылку на команду".**</span><span class="sxs-lookup"><span data-stu-id="7df18-215">Select **Get link to team**.</span></span>
> - <span data-ttu-id="7df18-216">Скопируйте и **сохраните значение groupId** из строки.</span><span class="sxs-lookup"><span data-stu-id="7df18-216">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="7df18-217">Войдите в **песочницу Graph.**</span><span class="sxs-lookup"><span data-stu-id="7df18-217">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="7df18-218">Выполните **вызов GET** к следующей конечной точке: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`</span><span class="sxs-lookup"><span data-stu-id="7df18-218">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="7df18-219">Поле clientAppId в ответе будет сопоставлено с appId, указанным в манифесте приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="7df18-219">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="7df18-220">![Ответ песочницы graph на вызов GET.](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="7df18-220">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>
 
## <a name="test-resource-specific-consent"></a><span data-ttu-id="7df18-221">Проверка согласия для ресурса</span><span class="sxs-lookup"><span data-stu-id="7df18-221">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="7df18-222">**Тестирование разрешений на согласие для конкретных ресурсов в Teams**</span><span class="sxs-lookup"><span data-stu-id="7df18-222">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="7df18-223">Статья по теме для администраторов Teams</span><span class="sxs-lookup"><span data-stu-id="7df18-223">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7df18-224">**Для администраторов согласие на ресурсы в Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="7df18-224">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 
