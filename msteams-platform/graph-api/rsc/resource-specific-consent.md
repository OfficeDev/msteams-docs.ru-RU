---
title: Согласие на конкретные ресурсы в Teams
description: Описывает согласие, специфичное для Teams и как им воспользоваться.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: команды авторизации OAuth SSO AAD rsc Graph
ms.openlocfilehash: dabe0c33013fbb398eee7bf00ac2881cd86e6bc5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566135"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="c81a3-104">Согласие на конкретные ресурсы (RSC)</span><span class="sxs-lookup"><span data-stu-id="c81a3-104">Resource-specific consent (RSC)</span></span>

<span data-ttu-id="c81a3-105">Согласие с конкретными ресурсами (RSC) — это интеграция Microsoft Teams и Microsoft Graph API, которая позволяет приложению использовать конечные точки API для управления определенными группами в организации.</span><span class="sxs-lookup"><span data-stu-id="c81a3-105">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="c81a3-106">Модель разрешений на согласие с конкретными  ресурсами (RSC) позволяет владельцам групп дать согласие на получение заявки на доступ и/или изменение данных группы.</span><span class="sxs-lookup"><span data-stu-id="c81a3-106">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="c81a3-107">Детальные, Teams RSC определяют, что приложение может сделать в рамках конкретной группы:</span><span class="sxs-lookup"><span data-stu-id="c81a3-107">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="c81a3-108">Разрешения, специфичные для ресурсов</span><span class="sxs-lookup"><span data-stu-id="c81a3-108">Resource-specific permissions</span></span>

|<span data-ttu-id="c81a3-109">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="c81a3-109">Application permission</span></span>| <span data-ttu-id="c81a3-110">Действие</span><span class="sxs-lookup"><span data-stu-id="c81a3-110">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="c81a3-111">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-111">TeamSettings.Read.Group</span></span> | <span data-ttu-id="c81a3-112">Получите настройки для этой команды.</span><span class="sxs-lookup"><span data-stu-id="c81a3-112">Get the settings for this team.</span></span>|
|<span data-ttu-id="c81a3-113">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-113">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="c81a3-114">Обновление параметров для команды.</span><span class="sxs-lookup"><span data-stu-id="c81a3-114">Update the settings for this team.</span></span>|
|<span data-ttu-id="c81a3-115">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-115">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="c81a3-116">Получите имена каналов, описания каналов и настройки каналов для этой команды.</span><span class="sxs-lookup"><span data-stu-id="c81a3-116">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="c81a3-117">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-117">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="c81a3-118">Обновление имен каналов, описаний каналов и настроек каналов для этой команды.</span><span class="sxs-lookup"><span data-stu-id="c81a3-118">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="c81a3-119">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-119">Channel.Create.Group</span></span>|<span data-ttu-id="c81a3-120">Создание каналов в этой команде.</span><span class="sxs-lookup"><span data-stu-id="c81a3-120">Create channels in this team.</span></span>|
|<span data-ttu-id="c81a3-121">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-121">Channel.Delete.Group</span></span>|<span data-ttu-id="c81a3-122">Удалить каналы в этой команде.</span><span class="sxs-lookup"><span data-stu-id="c81a3-122">Delete channels in this team.</span></span>|
|<span data-ttu-id="c81a3-123">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-123">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="c81a3-124">Получите сообщения канала этой команды.</span><span class="sxs-lookup"><span data-stu-id="c81a3-124">Get this team's channel messages.</span></span>|
|<span data-ttu-id="c81a3-125">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-125">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="c81a3-126">Получить список установленных приложений этой команды.</span><span class="sxs-lookup"><span data-stu-id="c81a3-126">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="c81a3-127">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-127">TeamsTab.Read.Group</span></span>|<span data-ttu-id="c81a3-128">Получить список вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="c81a3-128">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="c81a3-129">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-129">TeamsTab.Create.Group</span></span>|<span data-ttu-id="c81a3-130">Создание вкладок в этой команде.</span><span class="sxs-lookup"><span data-stu-id="c81a3-130">Create tabs in this team.</span></span>|
|<span data-ttu-id="c81a3-131">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-131">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="c81a3-132">Обновление вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="c81a3-132">Update this team's tabs.</span></span>|
|<span data-ttu-id="c81a3-133">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-133">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="c81a3-134">Удаление вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="c81a3-134">Delete this team's tabs.</span></span>|
|<span data-ttu-id="c81a3-135">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="c81a3-135">TeamMember.Read.Group</span></span>|<span data-ttu-id="c81a3-136">Возьми членов этой команды.</span><span class="sxs-lookup"><span data-stu-id="c81a3-136">Get this team's members.</span></span>|

>[!NOTE]
><span data-ttu-id="c81a3-137">Разрешения на использование ресурсов доступны только для Teams, установленных на Teams и в настоящее время не являются частью Azure Active Directory портала.</span><span class="sxs-lookup"><span data-stu-id="c81a3-137">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="c81a3-138">Включить согласие на использование ресурсов в приложении</span><span class="sxs-lookup"><span data-stu-id="c81a3-138">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="c81a3-139">Шаги для включения RSC в приложении следующие:</span><span class="sxs-lookup"><span data-stu-id="c81a3-139">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="c81a3-140">[Настройка настроек согласия владельца группы на Azure Active Directory портале.](#configure-group-owner-consent-settings-in-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="c81a3-140">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="c81a3-141">[Зарегистрируйте приложение на платформа удостоверений Майкрософт через портал Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="c81a3-141">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="c81a3-142">[Просмотрите разрешения приложений на портале Azure AD.](#review-your-application-permissions-in-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="c81a3-142">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="c81a3-143">[Получить токен доступа с платформы Microsoft Identity.](#obtain-an-access-token-from-the-microsoft-identity-platform)</span><span class="sxs-lookup"><span data-stu-id="c81a3-143">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="c81a3-144">[Обновите манифест Teams приложения.](#update-your-teams-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="c81a3-144">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="c81a3-145">[Установите приложение прямо в Teams](#sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="c81a3-145">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="c81a3-146">[Проверьте приложение на наличие дополнительных разрешений RSC.](#check-your-app-for-added-rsc-permissions)</span><span class="sxs-lookup"><span data-stu-id="c81a3-146">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="c81a3-147">Настройка параметров согласия владельца группы на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="c81a3-147">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="c81a3-148">Вы можете включить или отключить [согласие владельца группы](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) непосредственно на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="c81a3-148">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="c81a3-149">Войтись на [портал Azure в](https://portal.azure.com) качестве [глобального администратора/администратора компании.](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)</span><span class="sxs-lookup"><span data-stu-id="c81a3-149">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="c81a3-150">[Выберите](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** Enterprise  =>  **приложения Согласие** и разрешения  =>    =>  **Настройки согласия пользователя.**</span><span class="sxs-lookup"><span data-stu-id="c81a3-150">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="c81a3-151">Включить, отключить или ограничить согласие пользователя с согласия владельца группы, помеченного **как контроль, на доступ к данным** приложений (по умолчанию **разрешается согласие владельца группы для всех владельцев групп).**</span><span class="sxs-lookup"><span data-stu-id="c81a3-151">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="c81a3-152">Для установки приложения с помощью RSC владелец группы должен быть включен для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="c81a3-152">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![лазурный rsc конфигурации](../../assets/images/azure-rsc-configuration.png)

<span data-ttu-id="c81a3-154">Чтобы включить или отключить согласие владельца группы с помощью PowerShell, следуйте шагам, изложенным в [согласии владельца группы Configure с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)</span><span class="sxs-lookup"><span data-stu-id="c81a3-154">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="c81a3-155">Зарегистрируйте приложение в платформа удостоверений Майкрософт через портал Azure AD</span><span class="sxs-lookup"><span data-stu-id="c81a3-155">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="c81a3-156">Портал Azure Active Directory предоставляет центральную платформу для регистрации и настройки приложений.</span><span class="sxs-lookup"><span data-stu-id="c81a3-156">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="c81a3-157">Ваше приложение должно быть зарегистрировано на портале Azure AD для интеграции с платформа удостоверений Майкрософт вызова microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="c81a3-157">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="c81a3-158">Для получения дополнительной [информации, см Регистрация приложения с платформа удостоверений Майкрософт](/graph/auth-register-app-v2).</span><span class="sxs-lookup"><span data-stu-id="c81a3-158">For more information, see [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="c81a3-159">Не регистрировать несколько Teams на один и тот же идентификатор приложения Azure AD. Идентификатор приложения должен быть уникальным для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="c81a3-159">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="c81a3-160">Попытки установить несколько приложений на один и тот же идентификатор приложения не увенчаются успехом.</span><span class="sxs-lookup"><span data-stu-id="c81a3-160">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="c81a3-161">Просмотрите разрешения приложений на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="c81a3-161">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="c81a3-162">Перейдите на  =>  **страницу регистрации домашних** приложений и выберите приложение RSC.</span><span class="sxs-lookup"><span data-stu-id="c81a3-162">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="c81a3-163">Выберите **разрешения API** из левой навигационной бара и изучите список настроенных разрешений для приложения.</span><span class="sxs-lookup"><span data-stu-id="c81a3-163">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="c81a3-164">Если ваше приложение будет делать только RSC Graph API звонки, удалите все разрешения на этой странице.</span><span class="sxs-lookup"><span data-stu-id="c81a3-164">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="c81a3-165">Если ваше приложение также будет делать вызовы, не в том числе RSC, сохраняйте эти разрешения по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="c81a3-165">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c81a3-166">Портал Azure AD не может использоваться для запроса разрешений RSC.</span><span class="sxs-lookup"><span data-stu-id="c81a3-166">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="c81a3-167">Разрешения RSC в настоящее время Teams для приложений, Teams клиента и заявлены в файле манифеста приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="c81a3-167">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="c81a3-168">Получить токен доступа от платформа удостоверений Майкрософт</span><span class="sxs-lookup"><span data-stu-id="c81a3-168">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="c81a3-169">Чтобы сделать Graph API, необходимо получить токен доступа для приложения с платформы идентификации.</span><span class="sxs-lookup"><span data-stu-id="c81a3-169">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="c81a3-170">Прежде чем ваше приложение сможет получить токен от платформа удостоверений Майкрософт, оно должно быть зарегистрировано на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c81a3-170">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="c81a3-171">Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="c81a3-171">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="c81a3-172">Для получения токена доступа с платформы идентификации необходимо иметь следующие значения из процесса регистрации Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c81a3-172">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="c81a3-173">Идентификатор **приложения,** присвоенный порталом регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="c81a3-173">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="c81a3-174">Если ваше приложение поддерживает один ва-по (SSO), вы должны использовать тот же идентификатор приложения для вашего приложения и SSO.</span><span class="sxs-lookup"><span data-stu-id="c81a3-174">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="c81a3-175">Секрет **клиента/пароль или** публичная/частная ключевая пара **(Сертификат).**</span><span class="sxs-lookup"><span data-stu-id="c81a3-175">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="c81a3-176">Это необязательно для нативных приложений;</span><span class="sxs-lookup"><span data-stu-id="c81a3-176">This is not required for native apps.</span></span>
- <span data-ttu-id="c81a3-177">**Перенаправление URI** (или ОТВЕТ URL) для вашего приложения для получения ответов от Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c81a3-177">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="c81a3-178">*Смотрите* [Получить доступ от имени пользователя](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) и получить доступ без [пользователя](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="c81a3-178">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="c81a3-179">Обновление манифеста Teams приложения</span><span class="sxs-lookup"><span data-stu-id="c81a3-179">Update your Teams app manifest</span></span>

<span data-ttu-id="c81a3-180">Разрешения RSC объявлены в файле манифеста приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="c81a3-180">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="c81a3-181">Добавьте [ключ webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) к манифесту приложения со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="c81a3-181">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="c81a3-182">**ID** - идентификатор приложения Azure AD. Для получения дополнительной информации [см. Зарегистрируйте свое приложение на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="c81a3-182">**id**  — your Azure AD app id. For more information, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="c81a3-183">**ресурс**  - любая строка.</span><span class="sxs-lookup"><span data-stu-id="c81a3-183">**resource**  — any string.</span></span> <span data-ttu-id="c81a3-184">Это поле не имеет работы в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа на ошибку; любая строка будет делать.</span><span class="sxs-lookup"><span data-stu-id="c81a3-184">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="c81a3-185">**разрешения приложений** - разрешения RSC для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="c81a3-185">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="c81a3-186">Для получения дополнительной информации [см.](resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="c81a3-186">For more information, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="c81a3-187">Разрешения, не вносяные RSC, хранятся на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c81a3-187">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="c81a3-188">Не добавляйте их в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="c81a3-188">Do not add them to the app manifest.</span></span>
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

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="c81a3-189">Загрузка приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="c81a3-189">Sideload your app in Teams</span></span>

<span data-ttu-id="c81a3-190">Если администратор Teams пользовательских загрузок приложений, вы [можете загрузить приложение непосредственно](~/concepts/deploy-and-publish/apps-upload.md) в конкретную группу.</span><span class="sxs-lookup"><span data-stu-id="c81a3-190">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="c81a3-191">Проверьте приложение на наличие дополнительных разрешений RSC</span><span class="sxs-lookup"><span data-stu-id="c81a3-191">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="c81a3-192">Разрешения RSC не приписываются пользователю.</span><span class="sxs-lookup"><span data-stu-id="c81a3-192">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="c81a3-193">Звонки будут сделаны с разрешениями приложений, а не с разрешениями, делегированным пользователями.</span><span class="sxs-lookup"><span data-stu-id="c81a3-193">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="c81a3-194">Таким образом, приложению может быть разрешено выполнять действия, которые пользователь не может, такие как создание канала или удаление вкладки. Вы должны просмотреть намерения владельца команды для вашего использования случае до принятия RSC API звонки.</span><span class="sxs-lookup"><span data-stu-id="c81a3-194">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="c81a3-195">Для получения дополнительной информации [см. Microsoft Teams обзор API](/graph/teams-concept-overview).</span><span class="sxs-lookup"><span data-stu-id="c81a3-195">For more information, see [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="c81a3-196">После установки приложения в группу можно [использовать Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) для просмотра разрешений, предоставленных приложению в команде:</span><span class="sxs-lookup"><span data-stu-id="c81a3-196">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="c81a3-197">Получите группу **командыId от** клиента Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="c81a3-197">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="c81a3-198">В Teams, выберите **Teams из** крайне левого навигационной бара.</span><span class="sxs-lookup"><span data-stu-id="c81a3-198">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="c81a3-199">Выберите команду, в которой приложение установлено из выпадают из меню.</span><span class="sxs-lookup"><span data-stu-id="c81a3-199">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="c81a3-200">Выберите **значок больше** вариантов (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="c81a3-200">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="c81a3-201">Выберите **Получить ссылку на команду**.</span><span class="sxs-lookup"><span data-stu-id="c81a3-201">Select **Get link to team**.</span></span>
> - <span data-ttu-id="c81a3-202">Копировать и сохранить **значение groupId** из строки.</span><span class="sxs-lookup"><span data-stu-id="c81a3-202">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="c81a3-203">Войдите **в Graph Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c81a3-203">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="c81a3-204">Сделайте **get** вызов к следующей конечной точке: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` .</span><span class="sxs-lookup"><span data-stu-id="c81a3-204">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="c81a3-205">Поле clientAppId в ответе будет картой к appId, указанному в Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="c81a3-205">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="c81a3-206">![Graph explorer на вызов GET.](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="c81a3-206">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="c81a3-207">Пример кода</span><span class="sxs-lookup"><span data-stu-id="c81a3-207">Code sample</span></span>
| <span data-ttu-id="c81a3-208">**Название образца**</span><span class="sxs-lookup"><span data-stu-id="c81a3-208">**Sample name**</span></span> | <span data-ttu-id="c81a3-209">**Описание**</span><span class="sxs-lookup"><span data-stu-id="c81a3-209">**Description**</span></span> | <span data-ttu-id="c81a3-210">**.NET**</span><span class="sxs-lookup"><span data-stu-id="c81a3-210">**.NET**</span></span> |<span data-ttu-id="c81a3-211">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="c81a3-211">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="c81a3-212">Ресурсное конкретное согласие (RSC)</span><span class="sxs-lookup"><span data-stu-id="c81a3-212">Resource Specific Consent (RSC)</span></span> | <span data-ttu-id="c81a3-213">Используйте RSC для вызова Graph API.</span><span class="sxs-lookup"><span data-stu-id="c81a3-213">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="c81a3-214">View</span><span class="sxs-lookup"><span data-stu-id="c81a3-214">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="c81a3-215">View</span><span class="sxs-lookup"><span data-stu-id="c81a3-215">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a><span data-ttu-id="c81a3-216">См. также</span><span class="sxs-lookup"><span data-stu-id="c81a3-216">See also</span></span>
 
* [<span data-ttu-id="c81a3-217">Тестирование разрешений на согласие с конкретными ресурсами в Teams</span><span class="sxs-lookup"><span data-stu-id="c81a3-217">Test resource-specific consent permissions in Teams</span></span>](test-resource-specific-consent.md)
* [<span data-ttu-id="c81a3-218">Согласие на использование ресурсов в Microsoft Teams для администраторов</span><span class="sxs-lookup"><span data-stu-id="c81a3-218">Resource-specific consent in Microsoft Teams for admins</span></span>](/MicrosoftTeams/resource-specific-consent)


