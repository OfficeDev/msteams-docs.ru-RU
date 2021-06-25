---
title: В Teams
description: Описывает согласие на конкретные ресурсы в Teams и как использовать его.
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: команды авторизации OAuth SSO AAD rsc Graph
ms.openlocfilehash: 4573140e33bffb0daafbdc9f929b5afd49231af8
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114422"
---
# <a name="resource-specific-consent"></a><span data-ttu-id="cecf3-104">Согласие для определенных ресурсов</span><span class="sxs-lookup"><span data-stu-id="cecf3-104">Resource-specific consent</span></span>

> [!NOTE]
> <span data-ttu-id="cecf3-105">Согласие на доступ к области чата с конкретными ресурсами доступно только для [предварительного просмотра общедоступных](../../resources/dev-preview/developer-preview-intro.md) разработчиков.</span><span class="sxs-lookup"><span data-stu-id="cecf3-105">Resource-specific consent for chat scope is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="cecf3-106">Согласие для конкретного ресурса (RSC) — это интеграция API Microsoft Teams и Microsoft Graph, которая позволяет приложению использовать конечные точки API для управления определенными ресурсами, группами или чатами, в организации.</span><span class="sxs-lookup"><span data-stu-id="cecf3-106">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific resources, either teams or chats, within an organization.</span></span> <span data-ttu-id="cecf3-107">Модель разрешений RSC  позволяет владельцам  команд и владельцам чатов предоставлять согласие приложению на доступ и изменение данных группы и данных чата соответственно.</span><span class="sxs-lookup"><span data-stu-id="cecf3-107">The RSC permissions model enables *team owners* and *chat owners* to grant consent for an application to access and modify a team's data and a chat's data, respectively.</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="cecf3-108">Разрешения, определенные для ресурсов</span><span class="sxs-lookup"><span data-stu-id="cecf3-108">Resource-specific permissions</span></span>

<span data-ttu-id="cecf3-109">Разрешения RSC, Teams, определяют, что приложение может сделать в определенном ресурсе.</span><span class="sxs-lookup"><span data-stu-id="cecf3-109">The granular, Teams-specific, RSC permissions define what an application can do within a specific resource.</span></span>

### <a name="resource-specific-permissions-for-a-team"></a><span data-ttu-id="cecf3-110">Разрешения на использование ресурсов для группы</span><span class="sxs-lookup"><span data-stu-id="cecf3-110">Resource-specific permissions for a team</span></span>

|<span data-ttu-id="cecf3-111">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="cecf3-111">Application permission</span></span>| <span data-ttu-id="cecf3-112">Действие</span><span class="sxs-lookup"><span data-stu-id="cecf3-112">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="cecf3-113">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-113">TeamSettings.Read.Group</span></span> | <span data-ttu-id="cecf3-114">Получите параметры этой группы.</span><span class="sxs-lookup"><span data-stu-id="cecf3-114">Get this team's settings.</span></span>|
|<span data-ttu-id="cecf3-115">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-115">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="cecf3-116">Обновление параметров этой группы.</span><span class="sxs-lookup"><span data-stu-id="cecf3-116">Update this team's settings.</span></span>|
|<span data-ttu-id="cecf3-117">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-117">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="cecf3-118">Получите имена каналов этой группы, описания каналов и параметры канала.</span><span class="sxs-lookup"><span data-stu-id="cecf3-118">Get this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="cecf3-119">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-119">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="cecf3-120">Обновим имена каналов этой группы, описания каналов и параметры канала.</span><span class="sxs-lookup"><span data-stu-id="cecf3-120">Update this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="cecf3-121">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-121">Channel.Create.Group</span></span>|<span data-ttu-id="cecf3-122">Создание каналов в этой команде.</span><span class="sxs-lookup"><span data-stu-id="cecf3-122">Create channels in this team.</span></span> |
|<span data-ttu-id="cecf3-123">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-123">Channel.Delete.Group</span></span>|<span data-ttu-id="cecf3-124">Удаление каналов в этой группе.</span><span class="sxs-lookup"><span data-stu-id="cecf3-124">Delete channels in this team.</span></span> |
|<span data-ttu-id="cecf3-125">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-125">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="cecf3-126">Получите сообщения канала этой группы.</span><span class="sxs-lookup"><span data-stu-id="cecf3-126">Get this team's channel messages.</span></span> |
|<span data-ttu-id="cecf3-127">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-127">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="cecf3-128">Получите список установленных приложений этой группы.</span><span class="sxs-lookup"><span data-stu-id="cecf3-128">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="cecf3-129">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-129">TeamsTab.Read.Group</span></span>|<span data-ttu-id="cecf3-130">Получите список вкладок этой группы.</span><span class="sxs-lookup"><span data-stu-id="cecf3-130">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="cecf3-131">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-131">TeamsTab.Create.Group</span></span>|<span data-ttu-id="cecf3-132">Создание вкладок в этой команде.</span><span class="sxs-lookup"><span data-stu-id="cecf3-132">Create tabs in this team.</span></span> |
|<span data-ttu-id="cecf3-133">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-133">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="cecf3-134">Обновление вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="cecf3-134">Update this team's tabs.</span></span> |
|<span data-ttu-id="cecf3-135">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-135">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="cecf3-136">Удаление вкладок этой команды.</span><span class="sxs-lookup"><span data-stu-id="cecf3-136">Delete this team's tabs.</span></span> |
|<span data-ttu-id="cecf3-137">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="cecf3-137">TeamMember.Read.Group</span></span>|<span data-ttu-id="cecf3-138">Получите членов этой группы.</span><span class="sxs-lookup"><span data-stu-id="cecf3-138">Get this team's members.</span></span> |

<span data-ttu-id="cecf3-139">Дополнительные сведения см. в дополнительных сведениях о разрешениях на [согласие, определенных ресурсами группы.](/graph/permissions-reference#teams-resource-specific-consent-permissions)</span><span class="sxs-lookup"><span data-stu-id="cecf3-139">For more details, see [team resource-specific consent permissions](/graph/permissions-reference#teams-resource-specific-consent-permissions).</span></span>

### <a name="resource-specific-permissions-for-a-chat"></a><span data-ttu-id="cecf3-140">Разрешения на доступ к ресурсам для чата</span><span class="sxs-lookup"><span data-stu-id="cecf3-140">Resource-specific permissions for a chat</span></span>

<span data-ttu-id="cecf3-141">В следующей таблице вы можете получить разрешения на доступ к ресурсам для чата:</span><span class="sxs-lookup"><span data-stu-id="cecf3-141">The following table provides resource-specific permissions for a chat:</span></span>

|<span data-ttu-id="cecf3-142">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="cecf3-142">Application permission</span></span>| <span data-ttu-id="cecf3-143">Действие</span><span class="sxs-lookup"><span data-stu-id="cecf3-143">Action</span></span> |
| ----- | ----- |
| <span data-ttu-id="cecf3-144">ChatSettings.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="cecf3-144">ChatSettings.Read.Chat</span></span>         | <span data-ttu-id="cecf3-145">Получите параметры этого чата.</span><span class="sxs-lookup"><span data-stu-id="cecf3-145">Get this chat's settings.</span></span>                                    |
| <span data-ttu-id="cecf3-146">ChatSettings.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="cecf3-146">ChatSettings.ReadWrite.Chat</span></span>    | <span data-ttu-id="cecf3-147">Обновление параметров этого чата.</span><span class="sxs-lookup"><span data-stu-id="cecf3-147">Update this chat's settings.</span></span>                          |
| <span data-ttu-id="cecf3-148">ChatMessage.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="cecf3-148">ChatMessage.Read.Chat</span></span>          | <span data-ttu-id="cecf3-149">Получите сообщения этого чата.</span><span class="sxs-lookup"><span data-stu-id="cecf3-149">Get this chat's messages.</span></span>                                    |
| <span data-ttu-id="cecf3-150">ChatMember.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="cecf3-150">ChatMember.Read.Chat</span></span>           | <span data-ttu-id="cecf3-151">Получите участников этого чата.</span><span class="sxs-lookup"><span data-stu-id="cecf3-151">Get this chat's members.</span></span>                                     |
| <span data-ttu-id="cecf3-152">Chat.Manage.Chat</span><span class="sxs-lookup"><span data-stu-id="cecf3-152">Chat.Manage.Chat</span></span>               | <span data-ttu-id="cecf3-153">Управление чатом.</span><span class="sxs-lookup"><span data-stu-id="cecf3-153">Manage this chat.</span></span>                                             |
| <span data-ttu-id="cecf3-154">TeamsTab.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="cecf3-154">TeamsTab.Read.Chat</span></span>             | <span data-ttu-id="cecf3-155">Получите вкладки этого чата.</span><span class="sxs-lookup"><span data-stu-id="cecf3-155">Get this chat's tabs.</span></span>                                        |
| <span data-ttu-id="cecf3-156">TeamsTab.Create.Chat</span><span class="sxs-lookup"><span data-stu-id="cecf3-156">TeamsTab.Create.Chat</span></span>           | <span data-ttu-id="cecf3-157">Создание вкладок в чате.</span><span class="sxs-lookup"><span data-stu-id="cecf3-157">Create tabs in this chat.</span></span>                                     |
| <span data-ttu-id="cecf3-158">TeamsTab.Delete.Chat</span><span class="sxs-lookup"><span data-stu-id="cecf3-158">TeamsTab.Delete.Chat</span></span>           | <span data-ttu-id="cecf3-159">Удаление вкладок чата.</span><span class="sxs-lookup"><span data-stu-id="cecf3-159">Delete this chat's tabs.</span></span>                                      |
| <span data-ttu-id="cecf3-160">TeamsTab.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="cecf3-160">TeamsTab.ReadWrite.Chat</span></span>        | <span data-ttu-id="cecf3-161">Управление вкладками чата.</span><span class="sxs-lookup"><span data-stu-id="cecf3-161">Manage this chat's tabs.</span></span>                                      |
| <span data-ttu-id="cecf3-162">TeamsAppInstallation.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="cecf3-162">TeamsAppInstallation.Read.Chat</span></span> | <span data-ttu-id="cecf3-163">Получите, какие приложения установлены в этом чате.</span><span class="sxs-lookup"><span data-stu-id="cecf3-163">Get which apps are installed in this chat.</span></span>                   |
| <span data-ttu-id="cecf3-164">OnlineMeeting.ReadBasic.Chat</span><span class="sxs-lookup"><span data-stu-id="cecf3-164">OnlineMeeting.ReadBasic.Chat</span></span>   | <span data-ttu-id="cecf3-165">Получите основные свойства, такие как имя, расписание, организатор и соедините ссылку на собрание, связанное с этим чатом.</span><span class="sxs-lookup"><span data-stu-id="cecf3-165">Get basic properties, such as name, schedule, organizer, and join link of a meeting associated with this chat.</span></span> |

<span data-ttu-id="cecf3-166">Дополнительные сведения см. в [материале Chat Resource-specific consent permissions.](/graph/permissions-reference#chat-resource-specific-consent-permissions)</span><span class="sxs-lookup"><span data-stu-id="cecf3-166">For more details, see [chat resource-specific consent permissions](/graph/permissions-reference#chat-resource-specific-consent-permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="cecf3-167">Разрешения на использование ресурсов доступны только Teams приложениям, установленным на Teams клиенте, и в настоящее время не являются частью портала Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="cecf3-167">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory (AAD) portal.</span></span>

## <a name="enable-rsc-in-your-application"></a><span data-ttu-id="cecf3-168">Включить RSC в приложении</span><span class="sxs-lookup"><span data-stu-id="cecf3-168">Enable RSC in your application</span></span>

1. <span data-ttu-id="cecf3-169">[Настройка параметров согласия на портале AAD.](#configure-consent-settings-in-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="cecf3-169">[Configure consent settings in the AAD portal](#configure-consent-settings-in-the-aad-portal).</span></span>
    1. <span data-ttu-id="cecf3-170">Настройка параметров согласия владельца группы [для RSC в команде.](#configure-group-owner-consent-settings-for-rsc-in-a-team)</span><span class="sxs-lookup"><span data-stu-id="cecf3-170">[Configure group owner consent settings for RSC in a team](#configure-group-owner-consent-settings-for-rsc-in-a-team).</span></span>
    1. <span data-ttu-id="cecf3-171">[Настройка параметров согласия пользователей для RSC в чате.](#configure-user-consent-settings-for-rsc-in-a-chat)</span><span class="sxs-lookup"><span data-stu-id="cecf3-171">[Configure user consent settings for RSC in a chat](#configure-user-consent-settings-for-rsc-in-a-chat).</span></span>
1. <span data-ttu-id="cecf3-172">[Зарегистрируйте свое приложение платформа удостоверений Майкрософт с помощью портала AAD.](#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="cecf3-172">[Register your app with Microsoft identity platform using the AAD portal](#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).</span></span>
1. <span data-ttu-id="cecf3-173">[Просмотрите разрешения приложения на портале AAD.](#review-your-application-permissions-in-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="cecf3-173">[Review your application permissions in the AAD portal](#review-your-application-permissions-in-the-aad-portal).</span></span>
1. <span data-ttu-id="cecf3-174">[Получение маркера доступа с платформы удостоверений.](#obtain-an-access-token-from-the-microsoft-identity-platform)</span><span class="sxs-lookup"><span data-stu-id="cecf3-174">[Obtain an access token from the identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="cecf3-175">[Обновление манифеста Teams приложения](#update-your-teams-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="cecf3-175">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="cecf3-176">[Установите приложение непосредственно в Teams.](#sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="cecf3-176">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="cecf3-177">[Проверьте приложение для дополнительных разрешений RSC](#check-your-app-for-added-rsc-permissions).</span><span class="sxs-lookup"><span data-stu-id="cecf3-177">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>
    1. <span data-ttu-id="cecf3-178">[Проверьте приложение для добавленных разрешений RSC в команде.](#check-your-app-for-added-rsc-permissions-in-a-team)</span><span class="sxs-lookup"><span data-stu-id="cecf3-178">[Check your app for added RSC permissions in a team](#check-your-app-for-added-rsc-permissions-in-a-team).</span></span>
    1. <span data-ttu-id="cecf3-179">[Проверьте приложение для добавленных разрешений RSC в чате.](#check-your-app-for-added-rsc-permissions-in-a-chat)</span><span class="sxs-lookup"><span data-stu-id="cecf3-179">[Check your app for added RSC permissions in a chat](#check-your-app-for-added-rsc-permissions-in-a-chat).</span></span>

## <a name="configure-consent-settings-in-the-aad-portal"></a><span data-ttu-id="cecf3-180">Настройка параметров согласия на портале AAD</span><span class="sxs-lookup"><span data-stu-id="cecf3-180">Configure consent settings in the AAD portal</span></span>

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a><span data-ttu-id="cecf3-181">Настройка параметров согласия владельца группы для RSC в команде</span><span class="sxs-lookup"><span data-stu-id="cecf3-181">Configure group owner consent settings for RSC in a team</span></span>

<span data-ttu-id="cecf3-182">Вы можете включить или отключить согласие владельца [группы](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) непосредственно на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="cecf3-182">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

1. <span data-ttu-id="cecf3-183">Во входе на портал [Azure](https://portal.azure.com) в качестве [глобального администратора или администратора компании.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="cecf3-183">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator or Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>
1. <span data-ttu-id="cecf3-184">Выберите **Azure Active Directory**  >  **Enterprise приложений** Согласие и  >  **разрешения** параметров согласия  >  [**пользователя.**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)</span><span class="sxs-lookup"><span data-stu-id="cecf3-184">Select **Azure Active Directory** > **Enterprise applications** > **Consent and permissions** > [**User consent settings**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings).</span></span>
1. <span data-ttu-id="cecf3-185">Включить, отключить или ограничить согласие пользователя с согласия владельца группы с меткой управления для **доступа к данным приложений.**</span><span class="sxs-lookup"><span data-stu-id="cecf3-185">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data**.</span></span> <span data-ttu-id="cecf3-186">По умолчанию **разрешается согласие владельца группы для всех владельцев групп.**</span><span class="sxs-lookup"><span data-stu-id="cecf3-186">The default is **Allow group owner consent for all group owners**.</span></span> <span data-ttu-id="cecf3-187">Чтобы владелец группы устанавливал приложение с помощью RSC, для этого пользователя необходимо включить согласие владельца группы.</span><span class="sxs-lookup"><span data-stu-id="cecf3-187">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

    ![Конфигурация команды Azure RSC](../../assets/images/azure-rsc-team-configuration.png)

<span data-ttu-id="cecf3-189">Кроме того, вы можете включить или отключить согласие владельца группы с помощью PowerShell, следуйте шагам, описанным в настройке согласия владельца группы [с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)</span><span class="sxs-lookup"><span data-stu-id="cecf3-189">In addition, you can enable or disable group owner consent using PowerShell, follow the steps outlined in [configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a><span data-ttu-id="cecf3-190">Настройка параметров согласия пользователя для RSC в чате</span><span class="sxs-lookup"><span data-stu-id="cecf3-190">Configure user consent settings for RSC in a chat</span></span>

<span data-ttu-id="cecf3-191">Вы можете включить или отключить [согласие пользователя непосредственно](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="cecf3-191">You can enable or disable [user consent](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) directly within the Azure portal:</span></span>

1. <span data-ttu-id="cecf3-192">Во входе на портал [Azure](https://portal.azure.com) в качестве [глобального администратора или администратора компании.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="cecf3-192">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator or Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>
1. <span data-ttu-id="cecf3-193">Выберите **Azure Active Directory**  >  **Enterprise приложений** Согласие и  >  **разрешения** параметров согласия  >  [**пользователя.**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)</span><span class="sxs-lookup"><span data-stu-id="cecf3-193">Select **Azure Active Directory** > **Enterprise applications** > **Consent and permissions** > [**User consent settings**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings).</span></span>
1. <span data-ttu-id="cecf3-194">Включить, отключить или ограничить согласие пользователя с разрешением пользователя с меткой управления **для приложений.**</span><span class="sxs-lookup"><span data-stu-id="cecf3-194">Enable, disable, or limit user consent with the control labeled **User consent for applications**.</span></span> <span data-ttu-id="cecf3-195">По умолчанию **разрешается согласие пользователя для приложений.**</span><span class="sxs-lookup"><span data-stu-id="cecf3-195">The default is **Allow user consent for apps**.</span></span> <span data-ttu-id="cecf3-196">Чтобы участник чата устанавливал приложение с помощью RSC, для этого пользователя необходимо включить согласие пользователя.</span><span class="sxs-lookup"><span data-stu-id="cecf3-196">For a chat member to install an app using RSC, user consent must be enabled for that user.</span></span>

    ![Конфигурация чата Azure RSC](../../assets/images/azure-rsc-chat-configuration.png)

<span data-ttu-id="cecf3-198">Кроме того, вы можете включить или отключить согласие пользователя с помощью PowerShell, следуйте шагам, описанным в настройке согласия пользователя [с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)</span><span class="sxs-lookup"><span data-stu-id="cecf3-198">In addition, you can enable or disable user consent using PowerShell, follow the steps outlined in [configure user consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-using-the-aad-portal"></a><span data-ttu-id="cecf3-199">Регистрация приложения с помощью платформа удостоверений Майкрософт с помощью портала AAD</span><span class="sxs-lookup"><span data-stu-id="cecf3-199">Register your app with Microsoft identity platform using the AAD portal</span></span>

<span data-ttu-id="cecf3-200">Портал AAD предоставляет центральную платформу для регистрации и настройки приложений.</span><span class="sxs-lookup"><span data-stu-id="cecf3-200">The AAD portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="cecf3-201">Ваше приложение должно быть зарегистрировано на портале AAD для интеграции с платформой удостоверений и вызова API microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="cecf3-201">Your app must be registered in the AAD portal to integrate with the identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="cecf3-202">Дополнительные сведения см. [в примере зарегистрировать приложение с помощью платформы удостоверений.](/graph/auth-register-app-v2)</span><span class="sxs-lookup"><span data-stu-id="cecf3-202">For more information, see [register an application with the identity platform](/graph/auth-register-app-v2).</span></span>

> [!WARNING]
> <span data-ttu-id="cecf3-203">ID приложения AAD не должен быть общим для нескольких Teams приложений.</span><span class="sxs-lookup"><span data-stu-id="cecf3-203">An AAD app ID must not be shared across multiple Teams apps.</span></span> <span data-ttu-id="cecf3-204">Должно быть сопоставление 1:1 между приложением Teams и приложением AAD.</span><span class="sxs-lookup"><span data-stu-id="cecf3-204">There must be a 1:1 mapping between a Teams app and an AAD app.</span></span> <span data-ttu-id="cecf3-205">Попытки установки нескольких Teams приложений, связанных с тем же ID приложения AAD, приводят к сбоям установки или запуска.</span><span class="sxs-lookup"><span data-stu-id="cecf3-205">Attempts to install multiple Teams apps which are associated with the same AAD app ID will cause installation or runtime failures.</span></span>

## <a name="review-your-application-permissions-in-the-aad-portal"></a><span data-ttu-id="cecf3-206">Просмотр разрешений приложения на портале AAD</span><span class="sxs-lookup"><span data-stu-id="cecf3-206">Review your application permissions in the AAD portal</span></span>

1. <span data-ttu-id="cecf3-207">Перейдите на **страницу**  >  **регистрации домашнего приложения** и выберите приложение RSC.</span><span class="sxs-lookup"><span data-stu-id="cecf3-207">Go to the **Home** > **App registrations** page and select your RSC app.</span></span>
1. <span data-ttu-id="cecf3-208">Выберите **разрешения API** с левой области и перейдите по списку настроенных разрешений **для** вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="cecf3-208">Choose **API permissions** from the left pane and go through the list of **Configured permissions** for your app.</span></span> <span data-ttu-id="cecf3-209">Если приложение делает вызовы API Graph RSC, удалите все разрешения на этой странице.</span><span class="sxs-lookup"><span data-stu-id="cecf3-209">If your app only makes RSC Graph API calls, delete all the permissions on that page.</span></span> <span data-ttu-id="cecf3-210">Если ваше приложение также вызывает не RSC, храните эти разрешения по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="cecf3-210">If your app also makes non-RSC calls, keep those permissions as required.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cecf3-211">Портал AAD не может использоваться для запроса разрешений RSC.</span><span class="sxs-lookup"><span data-stu-id="cecf3-211">The AAD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="cecf3-212">Разрешения RSC в настоящее время являются исключительными для Teams приложений, установленных в клиенте Teams и объявляются в файле манифеста Teams приложения (JSON).</span><span class="sxs-lookup"><span data-stu-id="cecf3-212">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the Teams app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="cecf3-213">Получение маркера доступа из платформа удостоверений Майкрософт</span><span class="sxs-lookup"><span data-stu-id="cecf3-213">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="cecf3-214">Чтобы сделать Graph API, необходимо получить маркер доступа для приложения с платформы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="cecf3-214">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="cecf3-215">Прежде чем приложение сможет получить маркер с платформы удостоверений, его необходимо зарегистрировать на портале AAD.</span><span class="sxs-lookup"><span data-stu-id="cecf3-215">Before your app can get a token from the identity platform, it must be registered in the AAD portal.</span></span> <span data-ttu-id="cecf3-216">Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="cecf3-216">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="cecf3-217">Чтобы получить маркер доступа с платформы удостоверений, необходимо иметь следующие значения из процесса регистрации AAD:</span><span class="sxs-lookup"><span data-stu-id="cecf3-217">You must have the following values from the AAD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="cecf3-218">ID **приложения,** присвоенный порталом регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="cecf3-218">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="cecf3-219">Если приложение поддерживает один вход (SSO), необходимо использовать тот же ИД приложения для приложения и SSO.</span><span class="sxs-lookup"><span data-stu-id="cecf3-219">If your app supports single sign-on (SSO) you must use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="cecf3-220">Секрет **клиента/пароль или** пара ключей общего или частного доступа, которая является **сертификатом.**</span><span class="sxs-lookup"><span data-stu-id="cecf3-220">The **Client secret/password** or a public or private key pair that is **Certificate**.</span></span> <span data-ttu-id="cecf3-221">Это необязательно для нативных приложений;</span><span class="sxs-lookup"><span data-stu-id="cecf3-221">This is not required for native apps.</span></span>
- <span data-ttu-id="cecf3-222">**URL-адрес URI** перенаправления или ответ для вашего приложения для получения ответов от AAD.</span><span class="sxs-lookup"><span data-stu-id="cecf3-222">A **Redirect URI** or reply URL for your app to receive responses from AAD.</span></span>

<span data-ttu-id="cecf3-223">Дополнительные сведения см. [в статью Получить](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) доступ от имени пользователя и [получить доступ без пользователя.](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="cecf3-223">For more information, see [get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [get access without a user](/graph/auth-v2-service).</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="cecf3-224">Обновление манифеста Teams приложения</span><span class="sxs-lookup"><span data-stu-id="cecf3-224">Update your Teams app manifest</span></span>

<span data-ttu-id="cecf3-225">Разрешения RSC объявляются в файле JSON манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="cecf3-225">The RSC permissions are declared in your app manifest JSON file.</span></span> <span data-ttu-id="cecf3-226">Добавьте ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="cecf3-226">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

|<span data-ttu-id="cecf3-227">Имя</span><span class="sxs-lookup"><span data-stu-id="cecf3-227">Name</span></span>| <span data-ttu-id="cecf3-228">Тип</span><span class="sxs-lookup"><span data-stu-id="cecf3-228">Type</span></span> | <span data-ttu-id="cecf3-229">Описание</span><span class="sxs-lookup"><span data-stu-id="cecf3-229">Description</span></span>|
|---|---|---|
|`id` |<span data-ttu-id="cecf3-230">String</span><span class="sxs-lookup"><span data-stu-id="cecf3-230">String</span></span> |<span data-ttu-id="cecf3-231">ID приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="cecf3-231">Your AAD app ID.</span></span> <span data-ttu-id="cecf3-232">Дополнительные сведения см. [в приложении на портале AAD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="cecf3-232">For more information, see [register your app in the AAD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).</span></span>|
|`resource`|<span data-ttu-id="cecf3-233">String</span><span class="sxs-lookup"><span data-stu-id="cecf3-233">String</span></span>| <span data-ttu-id="cecf3-234">Это поле не имеет операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа на ошибку; любая строка будет делать.</span><span class="sxs-lookup"><span data-stu-id="cecf3-234">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>|
|`applicationPermissions`|<span data-ttu-id="cecf3-235">Массив строк</span><span class="sxs-lookup"><span data-stu-id="cecf3-235">Array of strings</span></span>|<span data-ttu-id="cecf3-236">Разрешения RSC для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="cecf3-236">RSC permissions for  your app.</span></span> <span data-ttu-id="cecf3-237">Дополнительные сведения см. [в ресурсных разрешениях.](resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="cecf3-237">For more information, see [resource-specific permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>|

>
> [!IMPORTANT]
> <span data-ttu-id="cecf3-238">Разрешения не RSC хранятся на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="cecf3-238">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="cecf3-239">Не добавляйте их в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="cecf3-239">Do not add them to the app manifest.</span></span>
>

### <a name="example-for-rsc-in-a-team"></a><span data-ttu-id="cecf3-240">Пример RSC в команде</span><span class="sxs-lookup"><span data-stu-id="cecf3-240">Example for RSC in a team</span></span>

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

### <a name="example-for-rsc-in-a-chat"></a><span data-ttu-id="cecf3-241">Пример RSC в чате</span><span class="sxs-lookup"><span data-stu-id="cecf3-241">Example for RSC in a chat</span></span>

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

> [!NOTE]
> <span data-ttu-id="cecf3-242">Если приложение предназначено для поддержки установки в командных и чатных сферах, в одном манифесте могут быть указаны разрешения как группы, так и `applicationPermissions` чата.</span><span class="sxs-lookup"><span data-stu-id="cecf3-242">If the app is meant to support installation in both team and chat scopes, then both team and chat permissions can be specified in the same manifest under `applicationPermissions`.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="cecf3-243">Sideload ваше приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="cecf3-243">Sideload your app in Teams</span></span>

<span data-ttu-id="cecf3-244">Если администратор Teams позволяет настраивать загрузки приложений, [](~/concepts/deploy-and-publish/apps-upload.md) вы можете загрузить приложение непосредственно в определенную группу или чат.</span><span class="sxs-lookup"><span data-stu-id="cecf3-244">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team or chat.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="cecf3-245">Проверьте приложение на дополнительные разрешения RSC</span><span class="sxs-lookup"><span data-stu-id="cecf3-245">Check your app for added RSC permissions</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cecf3-246">Разрешения RSC не приписываются пользователю.</span><span class="sxs-lookup"><span data-stu-id="cecf3-246">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="cecf3-247">Вызовы сделаны с разрешениями приложения, а не с делегированием разрешений пользователя.</span><span class="sxs-lookup"><span data-stu-id="cecf3-247">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="cecf3-248">Приложению может быть разрешено выполнять действия, которые пользователь не может выполнять, например удаление вкладки. Перед вызовами API RSC необходимо просмотреть намерения владельца группы или владельца чата.</span><span class="sxs-lookup"><span data-stu-id="cecf3-248">The app can be allowed to perform actions that the user cannot, such as deleting a tab. You must review the team owner's or chat owner's intent for your use before making RSC API calls.</span></span> <span data-ttu-id="cecf3-249">Дополнительные сведения [см. в Microsoft Teams API.](/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="cecf3-249">For more information, see [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="cecf3-250">После установки приложения на ресурс можно использовать [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) для просмотра разрешений, предоставленных приложению на ресурсе.</span><span class="sxs-lookup"><span data-stu-id="cecf3-250">After the app has been installed to a resource, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to view the permissions that have been granted to the app in the resource.</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a><span data-ttu-id="cecf3-251">Проверьте приложение на дополнительные разрешения RSC в команде</span><span class="sxs-lookup"><span data-stu-id="cecf3-251">Check your app for added RSC permissions in a team</span></span>

1. <span data-ttu-id="cecf3-252">Получите **группуId** группы из Teams.</span><span class="sxs-lookup"><span data-stu-id="cecf3-252">Get the team's **groupId** from Teams.</span></span>
1. <span data-ttu-id="cecf3-253">В Teams выберите **Teams** из левой области.</span><span class="sxs-lookup"><span data-stu-id="cecf3-253">In Teams, select **Teams** from the leftmost pane.</span></span>
1. <span data-ttu-id="cecf3-254">Выберите команду, в которой будет установлено приложение.</span><span class="sxs-lookup"><span data-stu-id="cecf3-254">Select the team where the app is to be installed.</span></span>
1. <span data-ttu-id="cecf3-255">Выберите эллипсы, &#x25CF;&#x25CF;&#x25CF; для этой группы.</span><span class="sxs-lookup"><span data-stu-id="cecf3-255">Select the ellipses &#x25CF;&#x25CF;&#x25CF; for that team.</span></span>
1. <span data-ttu-id="cecf3-256">Выберите **Получить ссылку на команду** из выпадаемого меню команды.</span><span class="sxs-lookup"><span data-stu-id="cecf3-256">Select **Get link to team** from the team drop-down menu.</span></span>
1. <span data-ttu-id="cecf3-257">Скопируйте и сохраните **значение groupId** из ссылки на диалоговое окно **всплывающее** окно группы.</span><span class="sxs-lookup"><span data-stu-id="cecf3-257">Copy and save the **groupId** value from the **Get a link to the team** pop-up dialog box.</span></span>
1. <span data-ttu-id="cecf3-258">Во входе **в Graph Explorer**.</span><span class="sxs-lookup"><span data-stu-id="cecf3-258">Sign in to **Graph Explorer**.</span></span>
1. <span data-ttu-id="cecf3-259">Сделайте **вызов GET** в эту конечную точку: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` .</span><span class="sxs-lookup"><span data-stu-id="cecf3-259">Make a **GET** call to this endpoint: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="cecf3-260">Поле `clientAppId` в ответе будет соедино указанному в `webApplicationInfo.id` манифесте Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="cecf3-260">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>

    ![Graph ответа обозревателя на вызов GET для разрешений RSC группы](../../assets/images/team-graph-permissions.png)

<span data-ttu-id="cecf3-262">Дополнительные сведения о том, как получить сведения о приложениях, установленных в определенной группе, см. в материале "Имена и другие сведения о приложениях, установленных в [указанной группе".](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)</span><span class="sxs-lookup"><span data-stu-id="cecf3-262">For more information on how to get details of the apps installed in a specific team, see [get the names and other details of apps installed in the specified team](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps).</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a><span data-ttu-id="cecf3-263">Проверьте приложение на дополнительные разрешения RSC в чате</span><span class="sxs-lookup"><span data-stu-id="cecf3-263">Check your app for added RSC permissions in a chat</span></span>

1. <span data-ttu-id="cecf3-264">Получите ID потока чата из веб Teams *клиента.*</span><span class="sxs-lookup"><span data-stu-id="cecf3-264">Get the chat thread ID from the Teams *web* client.</span></span>
1. <span data-ttu-id="cecf3-265">В веб Teams клиенте выберите **Чат** с левой области.</span><span class="sxs-lookup"><span data-stu-id="cecf3-265">In the Teams web client, select **Chat** from the leftmost pane.</span></span>
1. <span data-ttu-id="cecf3-266">Выберите чат, в котором установлено приложение из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="cecf3-266">Select the chat where the app is installed from the drop-down menu.</span></span>
1. <span data-ttu-id="cecf3-267">Скопируйте веб-URL-адрес и сохраните ID потока чата из строки.</span><span class="sxs-lookup"><span data-stu-id="cecf3-267">Copy the web URL and save the chat thread ID from the string.</span></span>

    ![ID потока чата с веб-URL-адреса](../../assets/images/chat-thread-id.png)

1. <span data-ttu-id="cecf3-269">Во входе **в Graph Explorer**.</span><span class="sxs-lookup"><span data-stu-id="cecf3-269">Sign in to **Graph Explorer**.</span></span>
1. <span data-ttu-id="cecf3-270">Вызов **GET на** следующую конечную точку: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` .</span><span class="sxs-lookup"><span data-stu-id="cecf3-270">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`.</span></span> <span data-ttu-id="cecf3-271">Поле `clientAppId` в ответе будет соедино указанному в `webApplicationInfo.id` манифесте Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="cecf3-271">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>

    ![Graph исследователя на вызов GET для разрешений RSC чата](../../assets/images/chat-graph-permissions.png)

<span data-ttu-id="cecf3-273">Дополнительные сведения о том, как получить сведения о приложениях, установленных в определенном чате, см. в материале "Имена и другие сведения о приложениях, установленных в [указанном чате".](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)</span><span class="sxs-lookup"><span data-stu-id="cecf3-273">For more information on how to get details of apps installed in a specific chat, see [get the names and other details of apps installed in the specified chat](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat).</span></span>

## <a name="code-sample"></a><span data-ttu-id="cecf3-274">Пример кода</span><span class="sxs-lookup"><span data-stu-id="cecf3-274">Code sample</span></span>

| <span data-ttu-id="cecf3-275">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="cecf3-275">**Sample name**</span></span> | <span data-ttu-id="cecf3-276">**Описание**</span><span class="sxs-lookup"><span data-stu-id="cecf3-276">**Description**</span></span> | <span data-ttu-id="cecf3-277">**.NET**</span><span class="sxs-lookup"><span data-stu-id="cecf3-277">**.NET**</span></span> |<span data-ttu-id="cecf3-278">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="cecf3-278">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="cecf3-279">Resource-Specific согласия (RSC)</span><span class="sxs-lookup"><span data-stu-id="cecf3-279">Resource-Specific Consent (RSC)</span></span> | <span data-ttu-id="cecf3-280">Используйте RSC для вызова Graph API.</span><span class="sxs-lookup"><span data-stu-id="cecf3-280">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="cecf3-281">View</span><span class="sxs-lookup"><span data-stu-id="cecf3-281">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="cecf3-282">View</span><span class="sxs-lookup"><span data-stu-id="cecf3-282">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a><span data-ttu-id="cecf3-283">См. также</span><span class="sxs-lookup"><span data-stu-id="cecf3-283">See also</span></span>
 
* [<span data-ttu-id="cecf3-284">Тестирование разрешений на согласие для определенных ресурсов в Teams</span><span class="sxs-lookup"><span data-stu-id="cecf3-284">Test resource-specific consent permissions in Teams</span></span>](test-resource-specific-consent.md)
* [<span data-ttu-id="cecf3-285">Согласие на определенные ресурсы в Microsoft Teams для администраторов</span><span class="sxs-lookup"><span data-stu-id="cecf3-285">Resource-specific consent in Microsoft Teams for admins</span></span>](/MicrosoftTeams/resource-specific-consent)
