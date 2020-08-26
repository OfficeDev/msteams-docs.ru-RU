---
title: Подготовьте своего клиента Office 365
description: Как приступить к работе с Teams в Office 365
keywords: Настройка загрузки Office 365 для клиентов Teams
ms.openlocfilehash: a246b13ae3a12a486a06ff9d98d37d4d147e4ed4
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874865"
---
# <a name="prepare-your-office-365-tenant"></a><span data-ttu-id="69db7-104">Подготовьте своего клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="69db7-104">Prepare your Office 365 tenant</span></span>

<span data-ttu-id="69db7-105">Если вы являетесь подписчиком Office 365, вы можете разрабатывать приложения для Microsoft Teams с одним из следующих [планов](https://products.office.com/business/compare-more-office-365-for-business-plans):</span><span class="sxs-lookup"><span data-stu-id="69db7-105">If you are an Office 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="69db7-106">Бизнес базовый</span><span class="sxs-lookup"><span data-stu-id="69db7-106">Business Essentials</span></span>
* <span data-ttu-id="69db7-107">Бизнес премиум</span><span class="sxs-lookup"><span data-stu-id="69db7-107">Business Premium</span></span>
* <span data-ttu-id="69db7-108">Корпоративный E1, E3 и т. д.</span><span class="sxs-lookup"><span data-stu-id="69db7-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="69db7-109">Developer</span><span class="sxs-lookup"><span data-stu-id="69db7-109">Developer</span></span>
* <span data-ttu-id="69db7-110">Образование, образование и образование</span><span class="sxs-lookup"><span data-stu-id="69db7-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="69db7-111">Microsoft Teams также будет доступен клиентам, которые подписываются на E4 до [выхода](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)из нее.</span><span class="sxs-lookup"><span data-stu-id="69db7-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="69db7-112">Нужна среда разработки?</span><span class="sxs-lookup"><span data-stu-id="69db7-112">Just need a development environment?</span></span>

<span data-ttu-id="69db7-113">Если у вас в настоящее время нет учетной записи Office 365, вы можете зарегистрироваться для подписки на [программу Microsoft 365 для разработчиков](https://developer.microsoft.com/microsoft-365/dev-program) .</span><span class="sxs-lookup"><span data-stu-id="69db7-113">If you don't currently have an Office 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="69db7-114">Он *освободится* на 90 дней и будет обновляться до тех пор, пока вы его используете для разработки действий.</span><span class="sxs-lookup"><span data-stu-id="69db7-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="69db7-115">Если у вас есть подписка на Visual Studio *Enterprise* или *Professional* , обе программы включают бесплатную [подписку](https://aka.ms/MyVisualStudioBenefits)на Microsoft 365 для разработчиков, действующую в течение всего срока действия вашей подписки на Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="69db7-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="69db7-116">*Ознакомьтесь* [со статьей Настройка подписки на Microsoft 365 для разработчиков](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span><span class="sxs-lookup"><span data-stu-id="69db7-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="69db7-117">Включение Microsoft Teams для Организации</span><span class="sxs-lookup"><span data-stu-id="69db7-117">Enable Microsoft Teams for your organization</span></span> 

<span data-ttu-id="69db7-118">Если для вашей организации не включена поддержка Microsoft Teams, сначала потребуется сделать это.</span><span class="sxs-lookup"><span data-stu-id="69db7-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="69db7-119">Ознакомьтесь с подробными инструкциями по [обеспечению поддержки Teams в Организации](/microsoftteams/enable-features-office-365).</span><span class="sxs-lookup"><span data-stu-id="69db7-119">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="69db7-120">Включение пользовательских приложений Teams и включение специальной отправки приложений</span><span class="sxs-lookup"><span data-stu-id="69db7-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="69db7-121">Включите нестандартную загрузку приложений для клиента разработчика следующим образом:</span><span class="sxs-lookup"><span data-stu-id="69db7-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="69db7-122">Войдите в [центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="69db7-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="69db7-123">Выберите **Показать все**  -->  **команды**.</span><span class="sxs-lookup"><span data-stu-id="69db7-123">Select **Show All** --> **Teams**.</span></span> 

![изображение меню центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> <span data-ttu-id="69db7-125">Для отображения параметра "Teams" может потребоваться до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="69db7-125">It can take up to 24 hours for the "Teams" option to appear.</span></span> <span data-ttu-id="69db7-126">Во время промежуточного приложения вы можете [отправить свое приложение в среду Teams](/microsoftteams/upload-custom-apps#validate) для тестирования и проверки.</span><span class="sxs-lookup"><span data-stu-id="69db7-126">During interim, you can [Upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation.</span></span>

3. <span data-ttu-id="69db7-127">Перейдите к разделу политики установки **приложений Teams**  -->  **Setup Policies**  -->  **Global (по умолчанию на уровне Организации)**</span><span class="sxs-lookup"><span data-stu-id="69db7-127">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![Включение представления Загрузка неопубликованных](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="69db7-129">Переключите флажок **Отправить настраиваемые приложения** в положение **вкл** .</span><span class="sxs-lookup"><span data-stu-id="69db7-129">Toggle **upload custom apps** to the **on** position.</span></span>

<span data-ttu-id="69db7-130">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="69db7-130">That's it!</span></span> <span data-ttu-id="69db7-131">Теперь тестовый клиент позволит разрешить нестандартную загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="69db7-131">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="69db7-132">Поддержка загрузки неопубликованных приложений может занимать до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="69db7-132">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="69db7-133">Во время промежуточного режима вы можете использовать \*\*отправку для \<your tenant> \*\* тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="69db7-133">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![представление приложения упдлоад](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="69db7-135">Для получения полной информации о том, как эти параметры взаимодействуют, *Ознакомьтесь*со статьей [Управление пользовательскими политиками и параметрами приложений в Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) и [Управление политиками установки приложений в Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span><span class="sxs-lookup"><span data-stu-id="69db7-135">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>
