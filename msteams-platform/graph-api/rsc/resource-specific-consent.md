---
title: Согласие на определенные ресурсы в Teams
description: Описывает согласие на конкретные ресурсы в Teams и как использовать его.
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: команды авторизации OAuth SSO AAD rsc Graph
ms.openlocfilehash: f364371f7763235e64da71b91db9b16b41ddf389
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068550"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="a088a-104">Согласие на определенный ресурс (RSC)</span><span class="sxs-lookup"><span data-stu-id="a088a-104">Resource-specific consent (RSC)</span></span>

> [!NOTE]
> <span data-ttu-id="a088a-105">Согласие на доступ к области чата с конкретными ресурсами доступно только для [предварительного просмотра общедоступных](../../resources/dev-preview/developer-preview-intro.md) разработчиков.</span><span class="sxs-lookup"><span data-stu-id="a088a-105">Resource-specific consent for chat scope is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="a088a-106">Согласие для конкретного ресурса (RSC) — это интеграция API Microsoft Teams и Microsoft Graph, которая позволяет приложению использовать конечные точки API для управления определенными ресурсами — группами или чатами — в организации.</span><span class="sxs-lookup"><span data-stu-id="a088a-106">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific resources—either teams or chats—within an organization.</span></span> <span data-ttu-id="a088a-107">Модель разрешений, характерных для конкретных ресурсов,  позволяет  владельцам команд и владельцам чатов предоставлять согласие приложению на доступ и(или) изменять данные группы и данные чата соответственно.</span><span class="sxs-lookup"><span data-stu-id="a088a-107">The resource-specific consent (RSC) permissions model enables *team owners* and *chat owners* to grant consent for an application to access and/or modify a team's data and a chat's data, respectively.</span></span> <span data-ttu-id="a088a-108">Разнонакладные разрешения RSC определяют, что приложение может сделать в определенном ресурсе:</span><span class="sxs-lookup"><span data-stu-id="a088a-108">The granular RSC permissions define what an application can do within a specific resource:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="a088a-109">Разрешения, определенные для ресурсов</span><span class="sxs-lookup"><span data-stu-id="a088a-109">Resource-specific permissions</span></span>

### <a name="resource-specific-permissions-for-a-team"></a><span data-ttu-id="a088a-110">Разрешения на использование ресурсов для группы</span><span class="sxs-lookup"><span data-stu-id="a088a-110">Resource-specific permissions for a team</span></span>
|<span data-ttu-id="a088a-111">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="a088a-111">Application permission</span></span>| <span data-ttu-id="a088a-112">Действие</span><span class="sxs-lookup"><span data-stu-id="a088a-112">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="a088a-113">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-113">TeamSettings.Read.Group</span></span> | <span data-ttu-id="a088a-114">Получите параметры этой группы.</span><span class="sxs-lookup"><span data-stu-id="a088a-114">Get this team's settings.</span></span>|
|<span data-ttu-id="a088a-115">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-115">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="a088a-116">Обновление параметров этой группы.</span><span class="sxs-lookup"><span data-stu-id="a088a-116">Update this team's settings.</span></span>|
|<span data-ttu-id="a088a-117">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-117">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="a088a-118">Получите имена каналов этой группы, описания каналов и параметры канала.</span><span class="sxs-lookup"><span data-stu-id="a088a-118">Get this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="a088a-119">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-119">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="a088a-120">Обновим имена каналов этой группы, описания каналов и параметры канала.</span><span class="sxs-lookup"><span data-stu-id="a088a-120">Update this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="a088a-121">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-121">Channel.Create.Group</span></span>|<span data-ttu-id="a088a-122">Создание каналов в этой команде.</span><span class="sxs-lookup"><span data-stu-id="a088a-122">Create channels in this team.</span></span> |
|<span data-ttu-id="a088a-123">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-123">Channel.Delete.Group</span></span>|<span data-ttu-id="a088a-124">Удаление каналов в этой группе.</span><span class="sxs-lookup"><span data-stu-id="a088a-124">Delete channels in this team.</span></span> |
|<span data-ttu-id="a088a-125">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-125">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="a088a-126">Получите сообщения канала этой группы.</span><span class="sxs-lookup"><span data-stu-id="a088a-126">Get this team's channel messages.</span></span> |
|<span data-ttu-id="a088a-127">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-127">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="a088a-128">Получите список установленных приложений этой группы.</span><span class="sxs-lookup"><span data-stu-id="a088a-128">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="a088a-129">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-129">TeamsTab.Read.Group</span></span>|<span data-ttu-id="a088a-130">Получите список вкладок этой группы.</span><span class="sxs-lookup"><span data-stu-id="a088a-130">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="a088a-131">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-131">TeamsTab.Create.Group</span></span>|<span data-ttu-id="a088a-132">Создание вкладок в этой команде.</span><span class="sxs-lookup"><span data-stu-id="a088a-132">Create tabs in this team.</span></span> |
|<span data-ttu-id="a088a-133">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-133">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="a088a-134">Обновление вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="a088a-134">Update this team's tabs.</span></span> |
|<span data-ttu-id="a088a-135">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-135">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="a088a-136">Удаление вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="a088a-136">Delete this team's tabs.</span></span> |
|<span data-ttu-id="a088a-137">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="a088a-137">TeamMember.Read.Group</span></span>|<span data-ttu-id="a088a-138">Получите членов этой группы.</span><span class="sxs-lookup"><span data-stu-id="a088a-138">Get this team's members.</span></span> |

<span data-ttu-id="a088a-139">Дополнительные сведения см. в [материале Team resource-specific consent permissions.](/graph/permissions-reference#team-resource-specific-consent-permissions)</span><span class="sxs-lookup"><span data-stu-id="a088a-139">For more details, see [Team resource-specific consent permissions](/graph/permissions-reference#team-resource-specific-consent-permissions).</span></span>

### <a name="resource-specific-permissions-for-a-chat"></a><span data-ttu-id="a088a-140">Разрешения на доступ к ресурсам для чата</span><span class="sxs-lookup"><span data-stu-id="a088a-140">Resource-specific permissions for a chat</span></span>
|<span data-ttu-id="a088a-141">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="a088a-141">Application permission</span></span>| <span data-ttu-id="a088a-142">Действие</span><span class="sxs-lookup"><span data-stu-id="a088a-142">Action</span></span> |
| ----- | ----- |
| <span data-ttu-id="a088a-143">ChatSettings.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="a088a-143">ChatSettings.Read.Chat</span></span>         | <span data-ttu-id="a088a-144">Получите параметры этого чата.</span><span class="sxs-lookup"><span data-stu-id="a088a-144">Get this chat's settings.</span></span>                                    |
| <span data-ttu-id="a088a-145">ChatSettings.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="a088a-145">ChatSettings.ReadWrite.Chat</span></span>    | <span data-ttu-id="a088a-146">Обновление параметров этого чата.</span><span class="sxs-lookup"><span data-stu-id="a088a-146">Update this chat's settings.</span></span>                          |
| <span data-ttu-id="a088a-147">ChatMessage.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="a088a-147">ChatMessage.Read.Chat</span></span>          | <span data-ttu-id="a088a-148">Получите сообщения этого чата.</span><span class="sxs-lookup"><span data-stu-id="a088a-148">Get this chat's messages.</span></span>                                    |
| <span data-ttu-id="a088a-149">ChatMember.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="a088a-149">ChatMember.Read.Chat</span></span>           | <span data-ttu-id="a088a-150">Получите участников этого чата.</span><span class="sxs-lookup"><span data-stu-id="a088a-150">Get this chat's members.</span></span>                                     |
| <span data-ttu-id="a088a-151">Chat.Manage.Chat</span><span class="sxs-lookup"><span data-stu-id="a088a-151">Chat.Manage.Chat</span></span>               | <span data-ttu-id="a088a-152">Управление чатом.</span><span class="sxs-lookup"><span data-stu-id="a088a-152">Manage this chat.</span></span>                                             |
| <span data-ttu-id="a088a-153">TeamsTab.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="a088a-153">TeamsTab.Read.Chat</span></span>             | <span data-ttu-id="a088a-154">Получите вкладки этого чата.</span><span class="sxs-lookup"><span data-stu-id="a088a-154">Get this chat's tabs.</span></span>                                        |
| <span data-ttu-id="a088a-155">TeamsTab.Create.Chat</span><span class="sxs-lookup"><span data-stu-id="a088a-155">TeamsTab.Create.Chat</span></span>           | <span data-ttu-id="a088a-156">Создание вкладок в чате.</span><span class="sxs-lookup"><span data-stu-id="a088a-156">Create tabs in this chat.</span></span>                                     |
| <span data-ttu-id="a088a-157">TeamsTab.Delete.Chat</span><span class="sxs-lookup"><span data-stu-id="a088a-157">TeamsTab.Delete.Chat</span></span>           | <span data-ttu-id="a088a-158">Удаление вкладок чата.</span><span class="sxs-lookup"><span data-stu-id="a088a-158">Delete this chat's tabs.</span></span>                                      |
| <span data-ttu-id="a088a-159">TeamsTab.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="a088a-159">TeamsTab.ReadWrite.Chat</span></span>        | <span data-ttu-id="a088a-160">Управление вкладками чата.</span><span class="sxs-lookup"><span data-stu-id="a088a-160">Manage this chat's tabs.</span></span>                                      |
| <span data-ttu-id="a088a-161">TeamsAppInstallation.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="a088a-161">TeamsAppInstallation.Read.Chat</span></span> | <span data-ttu-id="a088a-162">Получите, какие приложения установлены в этом чате.</span><span class="sxs-lookup"><span data-stu-id="a088a-162">Get which apps are installed in this chat.</span></span>                   |
| <span data-ttu-id="a088a-163">OnlineMeeting.ReadBasic.Chat</span><span class="sxs-lookup"><span data-stu-id="a088a-163">OnlineMeeting.ReadBasic.Chat</span></span>   | <span data-ttu-id="a088a-164">Получите основные свойства, такие как имя, расписание, организатор и ссылка на ссылку на собрание, связанное с этим чатом.</span><span class="sxs-lookup"><span data-stu-id="a088a-164">Get basic properties—such as name, schedule, organizer, and join link—of a meeting associated with this chat.</span></span> |

<span data-ttu-id="a088a-165">Дополнительные сведения см. в [материале Chat resource-specific consent permissions.](/graph/permissions-reference#chat-resource-specific-consent-permissions)</span><span class="sxs-lookup"><span data-stu-id="a088a-165">For more details, see [Chat resource-specific consent permissions](/graph/permissions-reference#chat-resource-specific-consent-permissions).</span></span>

>[!NOTE]
><span data-ttu-id="a088a-166">Разрешения на использование ресурсов доступны только Teams приложениям, установленным на клиенте Teams и в настоящее время не являются частью Azure Active Directory портала.</span><span class="sxs-lookup"><span data-stu-id="a088a-166">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="a088a-167">Включить в приложении согласие, определенное для ресурсов</span><span class="sxs-lookup"><span data-stu-id="a088a-167">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="a088a-168">Действия для включения RSC в приложении следующие:</span><span class="sxs-lookup"><span data-stu-id="a088a-168">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="a088a-169">[Настройка параметров согласия на Azure Active Directory портале](#configure-consent-settings-in-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="a088a-169">[Configure consent settings in the Azure Active Directory portal](#configure-consent-settings-in-the-azure-ad-portal).</span></span>
    1. <span data-ttu-id="a088a-170">Настройка параметров согласия владельца группы [для RSC в команде.](#configure-group-owner-consent-settings-for-rsc-in-a-team)</span><span class="sxs-lookup"><span data-stu-id="a088a-170">[Configure group owner consent settings for RSC in a team](#configure-group-owner-consent-settings-for-rsc-in-a-team).</span></span>
    1. <span data-ttu-id="a088a-171">[Настройка параметров согласия пользователей для RSC в чате.](#configure-user-consent-settings-for-rsc-in-a-chat)</span><span class="sxs-lookup"><span data-stu-id="a088a-171">[Configure user consent settings for RSC in a chat](#configure-user-consent-settings-for-rsc-in-a-chat).</span></span>
1. <span data-ttu-id="a088a-172">[Зарегистрируйте свое приложение платформа удостоверений Майкрософт с помощью портала Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="a088a-172">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="a088a-173">[Просмотрите разрешения приложений на портале Azure AD.](#review-your-application-permissions-in-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="a088a-173">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="a088a-174">[Получение маркера доступа с платформы Microsoft Identity.](#obtain-an-access-token-from-the-microsoft-identity-platform)</span><span class="sxs-lookup"><span data-stu-id="a088a-174">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="a088a-175">[Обновление манифеста Teams приложения](#update-your-teams-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="a088a-175">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="a088a-176">[Установите приложение непосредственно в Teams.](#sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="a088a-176">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="a088a-177">[Проверьте приложение для дополнительных разрешений RSC](#check-your-app-for-added-rsc-permissions).</span><span class="sxs-lookup"><span data-stu-id="a088a-177">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>
    1. <span data-ttu-id="a088a-178">[Проверьте приложение для добавленных разрешений RSC в команде.](#check-your-app-for-added-rsc-permissions-in-a-team)</span><span class="sxs-lookup"><span data-stu-id="a088a-178">[Check your app for added RSC permissions in a team](#check-your-app-for-added-rsc-permissions-in-a-team).</span></span>
    1. <span data-ttu-id="a088a-179">[Проверьте приложение для добавленных разрешений RSC в чате.](#check-your-app-for-added-rsc-permissions-in-a-chat)</span><span class="sxs-lookup"><span data-stu-id="a088a-179">[Check your app for added RSC permissions in a chat](#check-your-app-for-added-rsc-permissions-in-a-chat).</span></span>

## <a name="configure-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="a088a-180">Настройка параметров согласия на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="a088a-180">Configure consent settings in the Azure AD portal</span></span>

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a><span data-ttu-id="a088a-181">Настройка параметров согласия владельца группы для RSC в команде</span><span class="sxs-lookup"><span data-stu-id="a088a-181">Configure group owner consent settings for RSC in a team</span></span>

<span data-ttu-id="a088a-182">Вы можете включить или отключить согласие владельца [группы](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) непосредственно на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="a088a-182">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="a088a-183">Во входе на [портал Azure](https://portal.azure.com) в качестве [глобального администратора или администратора компании.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a088a-183">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>  
 > - <span data-ttu-id="a088a-184">[Выберите](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory**  =>  **Enterprise приложения** Consent и  =>  **permissions** User consent  =>  **settings.**</span><span class="sxs-lookup"><span data-stu-id="a088a-184">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="a088a-185">Включить, отключить или ограничить согласие пользователя с согласия владельца группы с меткой управления для доступа к данным **приложений** (по умолчанию разрешается согласие владельца группы для всех **владельцев групп).**</span><span class="sxs-lookup"><span data-stu-id="a088a-185">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="a088a-186">Чтобы владелец группы устанавливал приложение с помощью RSC, для этого пользователя необходимо включить согласие владельца группы.</span><span class="sxs-lookup"><span data-stu-id="a088a-186">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![конфигурация команды azure rsc](../../assets/images/azure-rsc-team-configuration.png)

<span data-ttu-id="a088a-188">Чтобы включить или отключить согласие владельца группы с помощью PowerShell, выполните действия, описанные в Настройка согласия владельца группы [с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)</span><span class="sxs-lookup"><span data-stu-id="a088a-188">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a><span data-ttu-id="a088a-189">Настройка параметров согласия пользователя для RSC в чате</span><span class="sxs-lookup"><span data-stu-id="a088a-189">Configure user consent settings for RSC in a chat</span></span>

<span data-ttu-id="a088a-190">Вы можете включить или отключить [согласие пользователя непосредственно](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="a088a-190">You can enable or disable [user consent](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="a088a-191">Во входе на [портал Azure](https://portal.azure.com) в качестве [глобального администратора или администратора компании.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a088a-191">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>  
 > - <span data-ttu-id="a088a-192">[Выберите](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory**  =>  **Enterprise приложения** Consent и  =>  **permissions** User consent  =>  **settings.**</span><span class="sxs-lookup"><span data-stu-id="a088a-192">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="a088a-193">Включить, отключить или ограничить согласие пользователя с разрешением пользователя с меткой управления для приложений **(по** умолчанию разрешается согласие пользователя **для приложений).**</span><span class="sxs-lookup"><span data-stu-id="a088a-193">Enable, disable, or limit user consent with the control labeled **User consent for applications** (The default is **Allow user consent for apps**).</span></span> <span data-ttu-id="a088a-194">Чтобы участник чата устанавливал приложение с помощью RSC, для этого пользователя необходимо включить согласие пользователя.</span><span class="sxs-lookup"><span data-stu-id="a088a-194">For a chat member to install an app using RSC, user consent must be enabled for that user.</span></span>

![конфигурация чата azure rsc](../../assets/images/azure-rsc-chat-configuration.png)

<span data-ttu-id="a088a-196">Чтобы включить или отключить согласие пользователя с помощью PowerShell, выполните действия, описанные в Настройка согласия пользователя [с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)</span><span class="sxs-lookup"><span data-stu-id="a088a-196">To enable or disable user consent using PowerShell, follow the steps outlined in [Configure user consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell).</span></span>


## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="a088a-197">Регистрация приложения с помощью платформа удостоверений Майкрософт на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="a088a-197">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="a088a-198">Портал Azure Active Directory предоставляет центральную платформу для регистрации и настройки приложений.</span><span class="sxs-lookup"><span data-stu-id="a088a-198">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="a088a-199">Ваше приложение должно быть зарегистрировано на портале Azure AD, чтобы интегрироваться с платформа удостоверений Майкрософт и вызвать API Graph Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a088a-199">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="a088a-200">Дополнительные сведения [см. в приложении Register with the платформа удостоверений Майкрософт.](/graph/auth-register-app-v2)</span><span class="sxs-lookup"><span data-stu-id="a088a-200">For more information, see [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="a088a-201">ID приложения Azure AD не должен быть общим для нескольких Teams приложений.</span><span class="sxs-lookup"><span data-stu-id="a088a-201">An Azure AD app ID should not be shared across multiple Teams apps.</span></span> <span data-ttu-id="a088a-202">Должно быть сопоставление 1:1 между приложением Teams и приложением Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a088a-202">There should be a 1:1 mapping between a Teams App and an Azure AD app.</span></span> <span data-ttu-id="a088a-203">Попытки установки нескольких Teams приложений, связанных с одинаковым ИД приложения Azure AD, приводят к сбоям установки и запуска.</span><span class="sxs-lookup"><span data-stu-id="a088a-203">Attempts to install multiple Teams apps which are associated with the same Azure AD app ID will cause installation/runtime failures.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="a088a-204">Просмотр разрешений приложения на портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="a088a-204">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="a088a-205">Перейдите на **страницу**  =>  **регистрации домашнего приложения** и выберите приложение RSC.</span><span class="sxs-lookup"><span data-stu-id="a088a-205">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="a088a-206">Выберите **разрешения API** из левой панели nav и изучите список настроенных разрешений для приложения.</span><span class="sxs-lookup"><span data-stu-id="a088a-206">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="a088a-207">Если ваше приложение будет только делать вызовы API Graph RSC, удалите все разрешения на этой странице.</span><span class="sxs-lookup"><span data-stu-id="a088a-207">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="a088a-208">Если ваше приложение также будет звонить не RSC, храните эти разрешения по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="a088a-208">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="a088a-209">Портал Azure AD не может использоваться для запроса разрешений RSC.</span><span class="sxs-lookup"><span data-stu-id="a088a-209">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="a088a-210">Разрешения RSC в настоящее время являются исключительными для Teams приложений, установленных в клиенте Teams и объявляются в файле манифеста Teams приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="a088a-210">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the Teams app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="a088a-211">Получение маркера доступа из платформа удостоверений Майкрософт</span><span class="sxs-lookup"><span data-stu-id="a088a-211">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="a088a-212">Чтобы сделать Graph API, необходимо получить маркер доступа для приложения с платформы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="a088a-212">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="a088a-213">Прежде чем приложение сможет получить маркер из платформа удостоверений Майкрософт, его необходимо зарегистрировать на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a088a-213">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="a088a-214">Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="a088a-214">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="a088a-215">Для получения маркера доступа с платформы удостоверений необходимо иметь следующие значения из процесса регистрации Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a088a-215">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="a088a-216">ID **приложения,** присвоенный порталом регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="a088a-216">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="a088a-217">Если приложение поддерживает один вход (SSO), необходимо использовать тот же ID приложения для приложения и SSO.</span><span class="sxs-lookup"><span data-stu-id="a088a-217">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="a088a-218">Секрет **клиента или пароль** или пара ключей общего и частного доступа **(сертификат).**</span><span class="sxs-lookup"><span data-stu-id="a088a-218">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="a088a-219">Это необязательно для нативных приложений;</span><span class="sxs-lookup"><span data-stu-id="a088a-219">This is not required for native apps.</span></span>
- <span data-ttu-id="a088a-220">URI **перенаправления** (или URL-адрес ответа) для вашего приложения для получения ответов из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a088a-220">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="a088a-221">*См.* [статью Получить](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) доступ от имени пользователя и [получить доступ без пользователя](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="a088a-221">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="a088a-222">Обновление манифеста Teams приложения</span><span class="sxs-lookup"><span data-stu-id="a088a-222">Update your Teams app manifest</span></span>

<span data-ttu-id="a088a-223">Разрешения RSC объявляются в файле манифеста приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="a088a-223">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="a088a-224">Добавьте ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="a088a-224">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="a088a-225">**id**  — ваш ID приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a088a-225">**id**  — your Azure AD app ID.</span></span> <span data-ttu-id="a088a-226">Дополнительные сведения см. в сайте [Регистрация приложения на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="a088a-226">For more information, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="a088a-227">**ресурс**  — любая строка.</span><span class="sxs-lookup"><span data-stu-id="a088a-227">**resource**  — any string.</span></span> <span data-ttu-id="a088a-228">Это поле не имеет операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа на ошибку; любая строка будет делать.</span><span class="sxs-lookup"><span data-stu-id="a088a-228">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="a088a-229">**разрешения приложения** — разрешения RSC для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a088a-229">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="a088a-230">Дополнительные сведения см. [в специальном ресурсе Permissions.](resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="a088a-230">For more information, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="a088a-231">Разрешения не RSC хранятся на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a088a-231">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="a088a-232">Не добавляйте их в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="a088a-232">Do not add them to the app manifest.</span></span>
>

### <a name="example-for-rsc-in-a-team"></a><span data-ttu-id="a088a-233">Пример RSC в команде</span><span class="sxs-lookup"><span data-stu-id="a088a-233">Example for RSC in a team</span></span>
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

### <a name="example-for-rsc-in-a-chat"></a><span data-ttu-id="a088a-234">Пример RSC в чате</span><span class="sxs-lookup"><span data-stu-id="a088a-234">Example for RSC in a chat</span></span>
```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "ChatSettings.Read.Chat",
      "ChatSettings.ReadWrite.Chat",
      "ChatMessage.Read.Chat",
      "ChatMember.Read.Chat",
      "Chat.Manage.Chat",
      "TeamsTab.Read.Chat",
      "TeamsTab.Create.Chat",
      "TeamsTab.Delete.Chat",
      "TeamsTab.ReadWrite.Chat",
      "TeamsAppInstallation.Read.Chat",
      "OnlineMeeting.ReadBasic.Chat"
    ]
  }
```

>[!NOTE]
><span data-ttu-id="a088a-235">Если приложение предназначено для поддержки установки в командных и чатных сферах, в одном манифесте могут быть указаны разрешения как группы, так и `applicationPermissions` чата.</span><span class="sxs-lookup"><span data-stu-id="a088a-235">If the app is meant to support installation in both team and chat scopes, then both team and chat permissions can be specified in the same manifest under `applicationPermissions`.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="a088a-236">Sideload ваше приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="a088a-236">Sideload your app in Teams</span></span>

<span data-ttu-id="a088a-237">Если администратор Teams позволяет настраивать загрузки приложений, [](~/concepts/deploy-and-publish/apps-upload.md) вы можете загрузить приложение непосредственно в определенную группу или чат.</span><span class="sxs-lookup"><span data-stu-id="a088a-237">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team or chat.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="a088a-238">Проверьте приложение на дополнительные разрешения RSC</span><span class="sxs-lookup"><span data-stu-id="a088a-238">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="a088a-239">Разрешения RSC не приписываются пользователю.</span><span class="sxs-lookup"><span data-stu-id="a088a-239">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="a088a-240">Вызовы сделаны с разрешениями приложения, а не с делегированием разрешений пользователя.</span><span class="sxs-lookup"><span data-stu-id="a088a-240">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="a088a-241">Таким образом, приложению может быть разрешено выполнять действия, которые не могут выполняться пользователем, например удаление вкладки. Перед вызовами API RSC необходимо просмотреть намерения владельца группы или владельца чата для вашего случая использования.</span><span class="sxs-lookup"><span data-stu-id="a088a-241">Thus, the app may be allowed to perform actions that the user cannot, such as deleting a tab. You should review the team owner's or chat owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="a088a-242">Дополнительные сведения [см. в Microsoft Teams API.](/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="a088a-242">For more information, see [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="a088a-243">После установки приложения на ресурс можно использовать [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) для просмотра разрешений, предоставленных приложению на ресурсе:</span><span class="sxs-lookup"><span data-stu-id="a088a-243">Once the app has been installed to a resource, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in the resource:</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a><span data-ttu-id="a088a-244">Проверьте приложение на дополнительные разрешения RSC в команде</span><span class="sxs-lookup"><span data-stu-id="a088a-244">Check your app for added RSC permissions in a team</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="a088a-245">Получите **группуId** группы из Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="a088a-245">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="a088a-246">В клиенте Teams выберите **Teams** из левого левого панели nav.</span><span class="sxs-lookup"><span data-stu-id="a088a-246">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="a088a-247">Выберите команду, в которой установлено приложение из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="a088a-247">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="a088a-248">Выберите **значок Дополнительные** параметры (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="a088a-248">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="a088a-249">Выберите **Получить ссылку на команду**.</span><span class="sxs-lookup"><span data-stu-id="a088a-249">Select **Get link to team**.</span></span>
> - <span data-ttu-id="a088a-250">Скопируйте и сохраните **значение groupId** из строки.</span><span class="sxs-lookup"><span data-stu-id="a088a-250">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="a088a-251">Войдите **в Graph Explorer**.</span><span class="sxs-lookup"><span data-stu-id="a088a-251">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="a088a-252">Вызов **GET на** следующую конечную точку: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` .</span><span class="sxs-lookup"><span data-stu-id="a088a-252">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="a088a-253">Поле `clientAppId` в ответе будет соедино указанному в `webApplicationInfo.id` манифесте Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="a088a-253">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>
  <span data-ttu-id="a088a-254">![Graph ответа исследователя на вызов GET для разрешений RSC группы.](../../assets/images/team-graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="a088a-254">![Graph explorer response to GET call for team RSC permissions.](../../assets/images/team-graph-permissions.png)</span></span>

<span data-ttu-id="a088a-255">Сведения о том, как получить сведения о приложениях, установленных в определенной группе, см. в материале [Get the names and other details of apps installed in the specified team.](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)</span><span class="sxs-lookup"><span data-stu-id="a088a-255">For information about how to get details about apps installed in a specific team, see [Get the names and other details of apps installed in the specified team](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps).</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a><span data-ttu-id="a088a-256">Проверьте приложение на дополнительные разрешения RSC в чате</span><span class="sxs-lookup"><span data-stu-id="a088a-256">Check your app for added RSC permissions in a chat</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="a088a-257">Получите ID потока чата из веб Teams *клиента.*</span><span class="sxs-lookup"><span data-stu-id="a088a-257">Get the chat thread ID from the Teams *web* client.</span></span>
> - <span data-ttu-id="a088a-258">В веб Teams клиенте выберите **Чат из** левой панели nav.</span><span class="sxs-lookup"><span data-stu-id="a088a-258">In the Teams web client, select **Chat** from the far left nav bar.</span></span>
> - <span data-ttu-id="a088a-259">Выберите чат, в котором установлено приложение из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="a088a-259">Select the chat where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="a088a-260">Скопируйте веб-URL-адрес и сохраните ID потока чата из строки.</span><span class="sxs-lookup"><span data-stu-id="a088a-260">Copy the web URL and save the chat thread ID from the string.</span></span>
<span data-ttu-id="a088a-261">![ID потока чата с веб-URL-адреса.](../../assets/images/chat-thread-id.png)</span><span class="sxs-lookup"><span data-stu-id="a088a-261">![Chat thread id from web URL.](../../assets/images/chat-thread-id.png)</span></span>
> - <span data-ttu-id="a088a-262">Войдите **в Graph Explorer**.</span><span class="sxs-lookup"><span data-stu-id="a088a-262">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="a088a-263">Вызов **GET на** следующую конечную точку: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` .</span><span class="sxs-lookup"><span data-stu-id="a088a-263">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`.</span></span> <span data-ttu-id="a088a-264">Поле `clientAppId` в ответе будет соедино указанному в `webApplicationInfo.id` манифесте Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="a088a-264">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>
  <span data-ttu-id="a088a-265">![Graph ответ обозревателя на вызов GET для разрешений RSC чата.](../../assets/images/chat-graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="a088a-265">![Graph explorer response to GET call for chat RSC permissions.](../../assets/images/chat-graph-permissions.png)</span></span>

<span data-ttu-id="a088a-266">Сведения о том, как получить сведения о приложениях, установленных в определенном чате, см. в материале [Get the names and other details of apps installed in the specified chat.](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)</span><span class="sxs-lookup"><span data-stu-id="a088a-266">For information about how to get details about apps installed in a specific chat, see [Get the names and other details of apps installed in the specified chat](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat).</span></span>

## <a name="code-sample"></a><span data-ttu-id="a088a-267">Пример кода</span><span class="sxs-lookup"><span data-stu-id="a088a-267">Code sample</span></span>
| <span data-ttu-id="a088a-268">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="a088a-268">**Sample name**</span></span> | <span data-ttu-id="a088a-269">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a088a-269">**Description**</span></span> | <span data-ttu-id="a088a-270">**.NET**</span><span class="sxs-lookup"><span data-stu-id="a088a-270">**.NET**</span></span> |<span data-ttu-id="a088a-271">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="a088a-271">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="a088a-272">Конкретное согласие ресурса (RSC)</span><span class="sxs-lookup"><span data-stu-id="a088a-272">Resource Specific Consent (RSC)</span></span> | <span data-ttu-id="a088a-273">Используйте RSC для вызова Graph API.</span><span class="sxs-lookup"><span data-stu-id="a088a-273">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="a088a-274">View</span><span class="sxs-lookup"><span data-stu-id="a088a-274">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="a088a-275">View</span><span class="sxs-lookup"><span data-stu-id="a088a-275">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a><span data-ttu-id="a088a-276">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="a088a-276">See also</span></span>
 
* [<span data-ttu-id="a088a-277">Тестирование разрешений на согласие для определенных ресурсов в Teams</span><span class="sxs-lookup"><span data-stu-id="a088a-277">Test resource-specific consent permissions in Teams</span></span>](test-resource-specific-consent.md)
* [<span data-ttu-id="a088a-278">Согласие на определенные ресурсы в Microsoft Teams для администраторов</span><span class="sxs-lookup"><span data-stu-id="a088a-278">Resource-specific consent in Microsoft Teams for admins</span></span>](/MicrosoftTeams/resource-specific-consent)


