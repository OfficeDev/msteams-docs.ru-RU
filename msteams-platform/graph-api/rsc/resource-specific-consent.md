---
title: Согласие с определенными ресурсами в Teams
description: В этой статье описывается согласие с определенным ресурсом в Teams и его преимущества.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Авторизация в Teams единого входа OAuth RSC Graph
ms.openlocfilehash: 7d0927fc360d8c005326cdff6453796fb45bf113
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867141"
---
# <a name="resource-specific-consent-rsc--developer-preview"></a><span data-ttu-id="fd592-104">Согласие для определенных ресурсов (RSC) — Предварительная версия для разработчиков</span><span class="sxs-lookup"><span data-stu-id="fd592-104">Resource-specific consent (RSC) — Developer Preview</span></span>

>[!NOTE]
><span data-ttu-id="fd592-105">Разрешения на доступ для определенных ресурсов доступны только в клиентах настольных ПК и Android после включения предварительной версии для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="fd592-105">The resource-specific consent permissions are only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="fd592-106">Узнайте, [как включить предварительный просмотр для разработчиков](../../resources/dev-preview/developer-preview-intro.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="fd592-106">See [How do I enable Developer Preview](../../resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

<span data-ttu-id="fd592-107">Согласие с конкретными ресурсами (RSC) — это интеграция Microsoft Teams и Graph API, которая позволяет приложению использовать конечные точки API для управления определенными командами в Организации.</span><span class="sxs-lookup"><span data-stu-id="fd592-107">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="fd592-108">Модель разрешений согласия для определенных ресурсов (RSC) позволяет *владельцам групп* предоставлять согласие на доступ к данным приложения и/или изменять их.</span><span class="sxs-lookup"><span data-stu-id="fd592-108">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="fd592-109">Детализация, зависящие от Teams, разрешения RSC определяют, что приложение может выполнять в определенной команде:</span><span class="sxs-lookup"><span data-stu-id="fd592-109">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="fd592-110">Разрешения для определенных ресурсов</span><span class="sxs-lookup"><span data-stu-id="fd592-110">Resource-specific permissions</span></span>

|<span data-ttu-id="fd592-111">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="fd592-111">Application permission</span></span>| <span data-ttu-id="fd592-112">Action</span><span class="sxs-lookup"><span data-stu-id="fd592-112">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="fd592-113">Теамсеттингс. Read. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-113">TeamSettings.Read.Group</span></span> | <span data-ttu-id="fd592-114">Получение параметров для этой команды.</span><span class="sxs-lookup"><span data-stu-id="fd592-114">Get the settings for this team.</span></span>|
|<span data-ttu-id="fd592-115">Теамсеттингс. Edit. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-115">TeamSettings.Edit.Group</span></span>|<span data-ttu-id="fd592-116">Обновление параметров для этой команды.</span><span class="sxs-lookup"><span data-stu-id="fd592-116">Update the settings for this team.</span></span>|
|<span data-ttu-id="fd592-117">Чаннелсеттингс. Read. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-117">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="fd592-118">Получите имена каналов, описания каналов и параметры канала для этой команды.</span><span class="sxs-lookup"><span data-stu-id="fd592-118">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="fd592-119">Чаннелсеттингс. Edit. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-119">ChannelSettings.Edit.Group</span></span>|<span data-ttu-id="fd592-120">Обновите имена каналов, описания каналов и параметры канала для этой команды.</span><span class="sxs-lookup"><span data-stu-id="fd592-120">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="fd592-121">Channel. Create. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-121">Channel.Create.Group</span></span>|<span data-ttu-id="fd592-122">Создание каналов в этой команде.</span><span class="sxs-lookup"><span data-stu-id="fd592-122">Create channels in this team.</span></span>|
|<span data-ttu-id="fd592-123">Channel. Delete. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-123">Channel.Delete.Group</span></span>|<span data-ttu-id="fd592-124">Удаление каналов в этой команде.</span><span class="sxs-lookup"><span data-stu-id="fd592-124">Delete channels in this team.</span></span>|
|<span data-ttu-id="fd592-125">Чаннелмессаже. Read. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-125">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="fd592-126">Получение сообщений о каналах этой группы.</span><span class="sxs-lookup"><span data-stu-id="fd592-126">Get this team's channel messages.</span></span>|
|<span data-ttu-id="fd592-127">TeamsApp. Read. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-127">TeamsApp.Read.Group</span></span>|<span data-ttu-id="fd592-128">Получение списка установленных приложений этой группы.</span><span class="sxs-lookup"><span data-stu-id="fd592-128">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="fd592-129">TeamsTab. Read. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-129">TeamsTab.Read.Group</span></span>|<span data-ttu-id="fd592-130">Получение списка вкладок этой группы.</span><span class="sxs-lookup"><span data-stu-id="fd592-130">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="fd592-131">TeamsTab. Create. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-131">TeamsTab.Create.Group</span></span>|<span data-ttu-id="fd592-132">Создание вкладок в этой команде.</span><span class="sxs-lookup"><span data-stu-id="fd592-132">Create tabs in this team.</span></span>|
|<span data-ttu-id="fd592-133">TeamsTab. Edit. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-133">TeamsTab.Edit.Group</span></span>|<span data-ttu-id="fd592-134">Обновите вкладки этой группы.</span><span class="sxs-lookup"><span data-stu-id="fd592-134">Update this team's tabs.</span></span>|
|<span data-ttu-id="fd592-135">TeamsTab. Delete. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-135">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="fd592-136">Удаление вкладок этой группы.</span><span class="sxs-lookup"><span data-stu-id="fd592-136">Delete this team's tabs.</span></span>|
|<span data-ttu-id="fd592-137">Member. Read. Group</span><span class="sxs-lookup"><span data-stu-id="fd592-137">Member.Read.Group</span></span>|<span data-ttu-id="fd592-138">Получение сведений о членах этой группы.</span><span class="sxs-lookup"><span data-stu-id="fd592-138">Get this team's members.</span></span>|
|<span data-ttu-id="fd592-139">Владелец. чтение. Группа</span><span class="sxs-lookup"><span data-stu-id="fd592-139">Owner.Read.Group</span></span>|<span data-ttu-id="fd592-140">Получение сведений о владельцах этой группы.</span><span class="sxs-lookup"><span data-stu-id="fd592-140">Get this team's owners.</span></span>|

>[!NOTE]
><span data-ttu-id="fd592-141">Разрешения, связанные с ресурсами, доступны только для приложений Teams, установленных в клиенте Teams и в настоящее время не входят в состав портала Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd592-141">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enabling-resource-specific-consent-in-your-application"></a><span data-ttu-id="fd592-142">Включение согласия, зависящей от ресурса, в приложении</span><span class="sxs-lookup"><span data-stu-id="fd592-142">Enabling resource-specific consent in your application</span></span>

<span data-ttu-id="fd592-143">Ниже приведены действия по включению RSC в приложении.</span><span class="sxs-lookup"><span data-stu-id="fd592-143">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="fd592-144">[Настройте параметры разрешения владельца группы на портале Azure Active Directory](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="fd592-144">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="fd592-145">[Зарегистрируйте свое приложение с помощью платформы удостоверений Майкрософт через портал Azure AD](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="fd592-145">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. [<span data-ttu-id="fd592-146">Просмотр разрешений приложения на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd592-146">Review your application permissions in the Azure AD portal</span></span>](#review-your-application-permissions-in-the-azure-ad-portal)
1. <span data-ttu-id="fd592-147">[Получите маркер доступа от платформы идентификации Майкрософт](#obtain-an-access-token-from-the-microsoft-identity-platform).</span><span class="sxs-lookup"><span data-stu-id="fd592-147">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="fd592-148">[Обновите манифест приложения Teams](#update-your-teams-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="fd592-148">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="fd592-149">[Установка приложения непосредственно в Teams](#install-your-app-directly-in-teams).</span><span class="sxs-lookup"><span data-stu-id="fd592-149">[Install your app directly in Teams](#install-your-app-directly-in-teams).</span></span>
1. <span data-ttu-id="fd592-150">[Проверьте приложение на наличие добавленных разрешений RSC](#check-your-app-for-added-rsc-permissions).</span><span class="sxs-lookup"><span data-stu-id="fd592-150">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="fd592-151">Настройка параметров согласия владельца группы на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd592-151">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="fd592-152">Вы можете включать и отключать [согласие владельца группы](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) непосредственно на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="fd592-152">You can enable or disable  [group owner consent](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="fd592-153">Войдите на [портал Azure](https://portal.azure.com) в качестве [глобального администратора или администратора компании](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span><span class="sxs-lookup"><span data-stu-id="fd592-153">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="fd592-154">Выберите **Azure Active Directory**  => **Enterprise applications**  => **Параметры пользователя**для корпоративных приложений Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd592-154">Select **Azure Active Directory** =>**Enterprise applications** =>**User settings**.</span></span>
> - <span data-ttu-id="fd592-155">Разрешите, запретите или ограничьте согласие пользователя с помощью элемента управления с надписью **пользователи могут получать согласие на доступ к данным компании для групп, которыми они владеют** (Эта возможность включена по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="fd592-155">Enable, disable, or limit user consent with the control labeled **Users can consent to apps accessing company data for the groups they own** (This capability is enabled by default).</span></span>

![Конфигурация Azure RSC](../../assets/images/azure-rsc-configuration.svg)

| <span data-ttu-id="fd592-157">Значение</span><span class="sxs-lookup"><span data-stu-id="fd592-157">Value</span></span> | <span data-ttu-id="fd592-158">Описание</span><span class="sxs-lookup"><span data-stu-id="fd592-158">Description</span></span>|
|--- | --- |
|<span data-ttu-id="fd592-159">Да</span><span class="sxs-lookup"><span data-stu-id="fd592-159">Yes</span></span> | <span data-ttu-id="fd592-160">Разрешите согласие с определенными группами для всех владельцев группы.</span><span class="sxs-lookup"><span data-stu-id="fd592-160">Enable group-specific consent for all group owners.</span></span>|
|<span data-ttu-id="fd592-161">Нет</span><span class="sxs-lookup"><span data-stu-id="fd592-161">No</span></span> |<span data-ttu-id="fd592-162">Отключение согласия, зависящей от группы, для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="fd592-162">Disable group-specific consent for all users.</span></span>| 
|<span data-ttu-id="fd592-163">Возможностями</span><span class="sxs-lookup"><span data-stu-id="fd592-163">Limited</span></span> | <span data-ttu-id="fd592-164">Разрешение согласия, зависящей от группы, для участников выбранной группы.</span><span class="sxs-lookup"><span data-stu-id="fd592-164">Enable group-specific consent for members of a selected group.</span></span>|

<span data-ttu-id="fd592-165">Чтобы включить или отключить согласие владельца группы на портале Azure с помощью PowerShell, выполните действия, описанные в разделе [Настройка разрешения владельца группы с помощью PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).</span><span class="sxs-lookup"><span data-stu-id="fd592-165">To enable or disable group owner consent within the Azure portal using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="fd592-166">Регистрация приложения с помощью платформы удостоверений Майкрософт через портал Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd592-166">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="fd592-167">Портал Azure Active Directory предоставляет центральную платформу для регистрации и настройки приложений.</span><span class="sxs-lookup"><span data-stu-id="fd592-167">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="fd592-168">Ваше приложение должно быть зарегистрировано на портале Azure AD для интеграции с API Microsoft Identity Platform и Graph Calls.</span><span class="sxs-lookup"><span data-stu-id="fd592-168">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Graph APIs.</span></span> <span data-ttu-id="fd592-169">В *разделе* [Регистрация приложения с помощью платформы удостоверений Майкрософт](/graph/auth-register-app-v2).</span><span class="sxs-lookup"><span data-stu-id="fd592-169">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="fd592-170">Не регистрировать несколько приложений Teams в одном идентификаторе приложения Azure AD. Идентификатор приложения должен быть уникальным для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="fd592-170">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="fd592-171">Попытки установить несколько приложений для одного идентификатора приложения завершатся неудачей.</span><span class="sxs-lookup"><span data-stu-id="fd592-171">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="fd592-172">Просмотр разрешений приложения на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd592-172">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="fd592-173">Перейдите на страницу **Home**  =>  **регистрации домашнего приложения** и выберите приложение RSC.</span><span class="sxs-lookup"><span data-stu-id="fd592-173">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="fd592-174">Выберите **разрешения API** в левой панели навигации и просмотрите список настроенных разрешений для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="fd592-174">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="fd592-175">Если ваше приложение будет выполнять только вызовы для графа RSC, удалите все разрешения на этой странице.</span><span class="sxs-lookup"><span data-stu-id="fd592-175">If your app will only make RSC Graph calls, delete all the permission on that page.</span></span> <span data-ttu-id="fd592-176">Если ваше приложение также сделает вызовы, не входящие в RSC,, не будут иметь соответствующих разрешений.</span><span class="sxs-lookup"><span data-stu-id="fd592-176">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fd592-177">Портал Azure AD не может использоваться для запроса разрешений RSC.</span><span class="sxs-lookup"><span data-stu-id="fd592-177">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="fd592-178">Разрешения RSC в настоящее время являются эксклюзивными для приложений Teams, установленных в клиенте Teams, и объявляются в файле манифеста приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="fd592-178">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="fd592-179">Получение маркера доступа от платформы удостоверений Майкрософт</span><span class="sxs-lookup"><span data-stu-id="fd592-179">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="fd592-180">Чтобы сделать вызовы API Graph, необходимо получить маркер доступа для приложения из платформы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="fd592-180">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="fd592-181">Прежде чем приложение сможет получить маркер от платформы удостоверений Майкрософт, его необходимо зарегистрировать на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd592-181">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="fd592-182">Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="fd592-182">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="fd592-183">Для получения маркера доступа от платформы удостоверений необходимо иметь следующие значения из процесса регистрации Azure AD:</span><span class="sxs-lookup"><span data-stu-id="fd592-183">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="fd592-184">**Идентификатор приложения** , назначенный порталом регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="fd592-184">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="fd592-185">Если ваше приложение поддерживает единый вход (SSO), необходимо использовать тот же идентификатор приложения для приложения и единого входа.</span><span class="sxs-lookup"><span data-stu-id="fd592-185">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="fd592-186">**Секрет и пароль клиента** или открытый/закрытый ключ (**сертификат**).</span><span class="sxs-lookup"><span data-stu-id="fd592-186">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="fd592-187">Это необязательно для нативных приложений;</span><span class="sxs-lookup"><span data-stu-id="fd592-187">This is not required for native apps.</span></span>
- <span data-ttu-id="fd592-188">**URI перенаправления** (или URL-адрес ответа) для приложения на получение ответов от Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd592-188">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="fd592-189">В *разделе* [Получение доступа от имени пользователя](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) и [Получение доступа без пользователя](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="fd592-189">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="fd592-190">Обновление манифеста приложения Teams</span><span class="sxs-lookup"><span data-stu-id="fd592-190">Update your Teams app manifest</span></span>

<span data-ttu-id="fd592-191">Разрешения RSC объявляются в файле манифеста приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="fd592-191">The RSC permissions are declared in you app manifest (JSON) file.</span></span>  <span data-ttu-id="fd592-192">Добавьте в манифест приложения ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="fd592-192">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="fd592-193">**ID** — идентификатор приложения Azure AD. В *разделе* [Регистрация приложения на портале Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="fd592-193">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="fd592-194">**ресурс** — любая строка.</span><span class="sxs-lookup"><span data-stu-id="fd592-194">**resource**  — any string.</span></span> <span data-ttu-id="fd592-195">Это поле не содержит операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ошибки. выполняется любая строка.</span><span class="sxs-lookup"><span data-stu-id="fd592-195">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="fd592-196">**разрешения приложения** — сведения о разрешениях RSC для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="fd592-196">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="fd592-197">*See* [Разрешения для определенных ресурсов](resource-specific-consent.md#resource-specific-permissions).</span><span class="sxs-lookup"><span data-stu-id="fd592-197">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="fd592-198">Разрешения, отличные от RSC, хранятся на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="fd592-198">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="fd592-199">Не добавляйте их в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="fd592-199">Do not add them to the app manifest.</span></span>
>

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

## <a name="install-your-app-directly-in-teams"></a><span data-ttu-id="fd592-200">Установка приложения непосредственно в Teams</span><span class="sxs-lookup"><span data-stu-id="fd592-200">Install your app directly in Teams</span></span>

<span data-ttu-id="fd592-201">После создания приложения вы можете [отправить пакет приложения](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) непосредственно определенной команде.</span><span class="sxs-lookup"><span data-stu-id="fd592-201">Once you've created your app you can [upload your app package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directly to a specific team.</span></span>  <span data-ttu-id="fd592-202">Для этого необходимо включить параметр " **Отправить настраиваемые политики приложений** " в рамках настраиваемых политик установки приложений.</span><span class="sxs-lookup"><span data-stu-id="fd592-202">To do so, the **Upload custom apps** policy setting must be enabled as part of the custom app setup policies.</span></span> <span data-ttu-id="fd592-203">*Просмотрите* [Настраиваемые параметры политики приложений](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span><span class="sxs-lookup"><span data-stu-id="fd592-203">*See* [Custom app policy settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="fd592-204">Проверка приложения на наличие добавленных разрешений RSC</span><span class="sxs-lookup"><span data-stu-id="fd592-204">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="fd592-205">Разрешения RSC не заносятся в атрибуты пользователя.</span><span class="sxs-lookup"><span data-stu-id="fd592-205">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="fd592-206">Звонки выполняются с разрешениями приложения, а не делегированными разрешениями пользователя.</span><span class="sxs-lookup"><span data-stu-id="fd592-206">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="fd592-207">Таким образом, приложению может быть разрешено выполнять действия, которые пользователь не может выполнить, например создание канала или удаление вкладки. Перед выполнением вызовов API RSC необходимо проанализировать назначение владельца команды для вашего варианта использования.</span><span class="sxs-lookup"><span data-stu-id="fd592-207">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="fd592-208">*Ознакомьтесь* с [обзором API Microsoft Teams](/graph/teams-concept-overview).</span><span class="sxs-lookup"><span data-stu-id="fd592-208">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="fd592-209">После установки приложения в команду можно использовать [проводник диаграмм](https://developer.microsoft.com/graph/graph-explorer) для просмотра разрешений, предоставленных приложению в команде:</span><span class="sxs-lookup"><span data-stu-id="fd592-209">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="fd592-210">Получение группы клиентов группы **из клиента** Teams.</span><span class="sxs-lookup"><span data-stu-id="fd592-210">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="fd592-211">В клиенте Teams выберите **Teams (Teams** ) в крайней левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="fd592-211">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="fd592-212">В раскрывающемся меню выберите команду, в которой установлено приложение.</span><span class="sxs-lookup"><span data-stu-id="fd592-212">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="fd592-213">Выберите значок **Дополнительные параметры** (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="fd592-213">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="fd592-214">Выберите команду **получить ссылку на команду**.</span><span class="sxs-lookup"><span data-stu-id="fd592-214">Select **Get link to team**.</span></span>
> - <span data-ttu-id="fd592-215">Скопируйте и сохраните значение **groupId** из строки.</span><span class="sxs-lookup"><span data-stu-id="fd592-215">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="fd592-216">Войдите в **проводник Graph**.</span><span class="sxs-lookup"><span data-stu-id="fd592-216">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="fd592-217">Выполните вызов **Get** для следующей конечной точки: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` .</span><span class="sxs-lookup"><span data-stu-id="fd592-217">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="fd592-218">Поле Клиентаппид в отклике будет сопоставляться с appId, указанным в манифесте приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="fd592-218">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>

 ![Ответ в проводнике Graph для получения вызова.](../../assets/images/graph-permissions.png)

 > [!div class="nextstepaction"]
> [<span data-ttu-id="fd592-220">Проверка разрешений согласия для определенных ресурсов в Teams</span><span class="sxs-lookup"><span data-stu-id="fd592-220">Test resource-specific consent permissions in Teams</span></span>](test-resource-specific-consent.md)
