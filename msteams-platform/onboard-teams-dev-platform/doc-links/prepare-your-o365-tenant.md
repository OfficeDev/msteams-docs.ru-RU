---
title: Подготовка среды разработки Teams
description: Настройка среды для приложений девелопи Teams
keywords: Настройка среды разработки Office 365 для клиентов Teams
ms.openlocfilehash: 701c6c110026007cf1670e783348bbdbe1aff498
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652140"
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="60053-104">Подготовка среды разработки</span><span class="sxs-lookup"><span data-stu-id="60053-104">Prepare your development environment</span></span>

<span data-ttu-id="60053-105">Если вы являетесь подписчиком Office 365, вы можете разрабатывать приложения для Microsoft Teams с одним из следующих [планов](https://products.office.com/business/compare-more-office-365-for-business-plans):</span><span class="sxs-lookup"><span data-stu-id="60053-105">If you are an Office 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="60053-106">Бизнес базовый</span><span class="sxs-lookup"><span data-stu-id="60053-106">Business Essentials</span></span>
* <span data-ttu-id="60053-107">Бизнес премиум</span><span class="sxs-lookup"><span data-stu-id="60053-107">Business Premium</span></span>
* <span data-ttu-id="60053-108">Корпоративный E1, E3 и т. д.</span><span class="sxs-lookup"><span data-stu-id="60053-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="60053-109">Developer</span><span class="sxs-lookup"><span data-stu-id="60053-109">Developer</span></span>
* <span data-ttu-id="60053-110">Образование, образование и образование</span><span class="sxs-lookup"><span data-stu-id="60053-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="60053-111">Microsoft Teams также будет доступен клиентам, которые подписываются на E4 до [выхода](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)из нее.</span><span class="sxs-lookup"><span data-stu-id="60053-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="60053-112">Нужна среда разработки?</span><span class="sxs-lookup"><span data-stu-id="60053-112">Just need a development environment?</span></span>

<span data-ttu-id="60053-113">Если у вас в настоящее время нет учетной записи Office 365, вы можете зарегистрироваться для подписки на [программу Microsoft 365 для разработчиков](https://developer.microsoft.com/microsoft-365/dev-program) .</span><span class="sxs-lookup"><span data-stu-id="60053-113">If you don't currently have an Office 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="60053-114">Он *освободится* на 90 дней и будет обновляться до тех пор, пока вы его используете для разработки действий.</span><span class="sxs-lookup"><span data-stu-id="60053-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="60053-115">Если у вас есть подписка на Visual Studio *Enterprise* или *Professional* , обе программы включают бесплатную [подписку](https://aka.ms/MyVisualStudioBenefits)на Microsoft 365 для разработчиков, действующую в течение всего срока действия вашей подписки на Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60053-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="60053-116">*Ознакомьтесь* [со статьей Настройка подписки на Microsoft 365 для разработчиков](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span><span class="sxs-lookup"><span data-stu-id="60053-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="60053-117">Включение Microsoft Teams для Организации</span><span class="sxs-lookup"><span data-stu-id="60053-117">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="60053-118">Если для вашей организации не включена поддержка Microsoft Teams, сначала потребуется сделать это.</span><span class="sxs-lookup"><span data-stu-id="60053-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="60053-119">Ознакомьтесь с подробными инструкциями по [обеспечению поддержки Teams в Организации](https://docs.microsoft.com/microsoftteams/enable-features-office-365).</span><span class="sxs-lookup"><span data-stu-id="60053-119">Take a look at our detailed guidance for [enabling Teams for your organization](https://docs.microsoft.com/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="60053-120">Включение пользовательских приложений Teams и включение специальной отправки приложений</span><span class="sxs-lookup"><span data-stu-id="60053-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="60053-121">Включите нестандартную загрузку приложений для клиента разработчика следующим образом:</span><span class="sxs-lookup"><span data-stu-id="60053-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="60053-122">Войдите в [центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="60053-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="60053-123">Выберите **Показать все**  -->  **команды**.</span><span class="sxs-lookup"><span data-stu-id="60053-123">Select **Show All** --> **Teams**.</span></span> 

![изображение меню переполнения приложения](~/assets/images/prepare-test-tenant/admin-center.png)

3. <span data-ttu-id="60053-125">Перейдите к разделу политики установки **приложений Teams**  -->  **Setup Policies**  -->  **Global (по умолчанию на уровне Организации)**</span><span class="sxs-lookup"><span data-stu-id="60053-125">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![изображение меню переполнения приложения](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="60053-127">Переключите флажок **Отправить настраиваемые приложения** в положение **вкл** .</span><span class="sxs-lookup"><span data-stu-id="60053-127">Toggle **upload custom apps** to the **on** position.</span></span>

<span data-ttu-id="60053-128">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="60053-128">That's it!</span></span> <span data-ttu-id="60053-129">Теперь тестовый клиент позволит разрешить нестандартную загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="60053-129">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="60053-130">Поддержка загрузки неопубликованных приложений может занимать до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="60053-130">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="60053-131">Во время промежуточного режима вы можете использовать \*\*отправку для \<your tenant> \*\* тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="60053-131">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![изображение меню переполнения приложения](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="60053-133">Для получения полной информации о том, как эти параметры взаимодействуют, *Ознакомьтесь*со статьей [Управление пользовательскими политиками и параметрами приложений в Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) и [Управление политиками установки приложений в Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span><span class="sxs-lookup"><span data-stu-id="60053-133">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>