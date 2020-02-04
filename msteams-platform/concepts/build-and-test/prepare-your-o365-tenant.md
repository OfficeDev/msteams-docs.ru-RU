---
title: Подготовка клиента Office 365
description: Как приступить к работе с Teams в Office 365
keywords: Настройка загрузки Office 365 для клиентов Teams
ms.openlocfilehash: 62cd640196631f50c72762253ff1bd75a143337d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675531"
---
# <a name="prepare-your-office-365-tenant"></a><span data-ttu-id="16960-104">Подготовка клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="16960-104">Prepare your Office 365 tenant</span></span>

<span data-ttu-id="16960-105">Для разработки приложений для Microsoft Teams необходимо быть [клиентом Office 365 с одним из следующих планов](https://products.office.com/business/compare-more-office-365-for-business-plans).</span><span class="sxs-lookup"><span data-stu-id="16960-105">To develop apps for Microsoft Teams, you need to be an [Office 365 customer with one of the following plans](https://products.office.com/business/compare-more-office-365-for-business-plans).</span></span>

* <span data-ttu-id="16960-106">Бизнес базовый</span><span class="sxs-lookup"><span data-stu-id="16960-106">Business Essentials</span></span>
* <span data-ttu-id="16960-107">Бизнес премиум</span><span class="sxs-lookup"><span data-stu-id="16960-107">Business Premium</span></span>
* <span data-ttu-id="16960-108">Корпоративный E1, E3 и т. д.</span><span class="sxs-lookup"><span data-stu-id="16960-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="16960-109">Developer</span><span class="sxs-lookup"><span data-stu-id="16960-109">Developer</span></span>
* <span data-ttu-id="16960-110">Образование, образование и образование</span><span class="sxs-lookup"><span data-stu-id="16960-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="16960-111">Microsoft Teams также будет доступен клиентам, которые приобрели E4 до выхода на пенсию.</span><span class="sxs-lookup"><span data-stu-id="16960-111">Microsoft Teams will also be available to customers who purchased E4 prior to its retirement.</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="16960-112">Нужна среда разработки?</span><span class="sxs-lookup"><span data-stu-id="16960-112">Just need a development environment?</span></span>

<span data-ttu-id="16960-113">Если у вас в настоящее время нет учетной записи Office 365, вы можете зарегистрироваться в [программе для разработчиков office 365](https://dev.office.com/devprogram) , чтобы получить 90 *Бесплатные* дни (обновление можно выполнить до тех пор, пока вы его используете для действий по разработке) клиент Office 365 Developer.</span><span class="sxs-lookup"><span data-stu-id="16960-113">If you don't currently have an Office 365 account, you can sign up for the [Office 365 Developer program](https://dev.office.com/devprogram) to get a *free* 90 days (can be renewed for as long as you're using it for development activity) Office 365 Developer Tenant.</span></span> <span data-ttu-id="16960-114">Эту учетную запись можно использовать только для целей тестирования.</span><span class="sxs-lookup"><span data-stu-id="16960-114">This account can only be used for testing purposes.</span></span> <span data-ttu-id="16960-115">Подробнее о [настройке тестовых учетных записей](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="16960-115">See more information on [setting up your test accounts](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="16960-116">Включение Microsoft Teams для Организации</span><span class="sxs-lookup"><span data-stu-id="16960-116">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="16960-117">Если Microsoft Teams еще не активирован для вашей организации, сначала потребуется сделать это.</span><span class="sxs-lookup"><span data-stu-id="16960-117">If Microsoft Teams is not yet enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="16960-118">Ознакомьтесь с подробными инструкциями по [обеспечению поддержки Teams в Организации](/microsoftteams/how-to-roll-out-teams).</span><span class="sxs-lookup"><span data-stu-id="16960-118">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/how-to-roll-out-teams).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="16960-119">Включение пользовательских приложений Teams и включение специальной отправки приложений</span><span class="sxs-lookup"><span data-stu-id="16960-119">Enable custom Teams apps and turn on custom app uploading</span></span>

> <span data-ttu-id="16960-120">Примечание. Если вы используете организацию разработчика O365 для создания своего приложения, эти параметры уже должны быть настроены, чтобы позволить вам создавать, загружать и тестировать приложение.</span><span class="sxs-lookup"><span data-stu-id="16960-120">Note: If you're using an O365 Developer Organization to build your app, these settings should already be configured to allow you to build, upload and test your app.</span></span>

<span data-ttu-id="16960-121">Включение настраиваемых приложений и пользовательских приложений обеспечивается тремя параметрами:</span><span class="sxs-lookup"><span data-stu-id="16960-121">There are three settings involved in enabling custom apps and custom app uploading:</span></span>

* <span data-ttu-id="16960-122">**Параметр настраиваемого приложения для всей** Организации — этот параметр включает или отключает настраиваемые приложения для Организации.</span><span class="sxs-lookup"><span data-stu-id="16960-122">**Org-wide custom app setting** - This setting either enables or disables custom apps for your organization.</span></span> <span data-ttu-id="16960-123">Он должен быть включен.</span><span class="sxs-lookup"><span data-stu-id="16960-123">It needs to be on.</span></span> 
* <span data-ttu-id="16960-124">**Параметр настраиваемого приложения Team** — этот параметр предназначен для каждой отдельной команды в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="16960-124">**Team custom app setting** - This setting is for each individual team inside Microsoft Teams.</span></span> <span data-ttu-id="16960-125">Если вы хотите установить приложение для определенной команды, это будет необходимо для этой команды.</span><span class="sxs-lookup"><span data-stu-id="16960-125">If you want to install your app for a specific team, this will need to be on for that team.</span></span>
* <span data-ttu-id="16960-126">**Настраиваемая политика приложений пользователя** — этот набор параметров управляет разрешениями для отдельного пользователя.</span><span class="sxs-lookup"><span data-stu-id="16960-126">**User custom app policy** - This set of settings controls the permissions for an individual user.</span></span> <span data-ttu-id="16960-127">Это необходимо сделать для тех пользователей, которым вы хотите отправить пользовательские приложения.</span><span class="sxs-lookup"><span data-stu-id="16960-127">You'll need to enable this for individuals you want to upload custom apps.</span></span>

<span data-ttu-id="16960-128">Для получения полной информации о том, как работают эти параметры, ознакомьтесь со статьей [Управление пользовательскими политиками и параметрами приложений в Microsoft Teams](/MicrosoftTeams/teams-custom-app-policies-and-settings).</span><span class="sxs-lookup"><span data-stu-id="16960-128">For complete information on how these settings interact see [Manage custom app policies and settings in Microsoft Teams](/MicrosoftTeams/teams-custom-app-policies-and-settings).</span></span>
