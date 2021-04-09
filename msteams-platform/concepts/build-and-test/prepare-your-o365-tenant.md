---
title: Подготовка клиента Microsoft 365
description: Начало работы с Teams в Microsoft 365
ms.topic: how-to
keywords: Настройка отправки команд клиентов Microsoft 365
ms.openlocfilehash: aa7f994744f8b1c62aa32122a5006cfa0f22d391
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634760"
---
# <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="23826-104">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="23826-104">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="23826-105">Подписчики Microsoft 365 могут разрабатывать приложения для Microsoft Teams с одним из следующих планов:</span><span class="sxs-lookup"><span data-stu-id="23826-105">Microsoft 365 subscribers can develop apps for Microsoft Teams with one of the following plans:</span></span>

* <span data-ttu-id="23826-106">Обычный</span><span class="sxs-lookup"><span data-stu-id="23826-106">Basic</span></span>
* <span data-ttu-id="23826-107">Стандартный</span><span class="sxs-lookup"><span data-stu-id="23826-107">Standard</span></span>
* <span data-ttu-id="23826-108">Корпоративные E1, E3 и E5</span><span class="sxs-lookup"><span data-stu-id="23826-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="23826-109">Developer</span><span class="sxs-lookup"><span data-stu-id="23826-109">Developer</span></span>
* <span data-ttu-id="23826-110">Education, Education Plus и Education E5</span><span class="sxs-lookup"><span data-stu-id="23826-110">Education, Education Plus, and Education E5</span></span>

> [!NOTE]
> <span data-ttu-id="23826-111">Дополнительные сведения о подписках на Microsoft 365 см. в [журнале plans.](https://products.office.com/business/compare-more-office-365-for-business-plans)</span><span class="sxs-lookup"><span data-stu-id="23826-111">For more information on Microsoft 365 subscriptions, see [plans](https://products.office.com/business/compare-more-office-365-for-business-plans).</span></span>
> 
> <span data-ttu-id="23826-112">Microsoft Teams также доступна для клиентов, подписавших подписку на E4 до ее выхода на [пенсию.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)</span><span class="sxs-lookup"><span data-stu-id="23826-112">Microsoft Teams is also available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="create-your-development-environment"></a><span data-ttu-id="23826-113">Создание среды разработки</span><span class="sxs-lookup"><span data-stu-id="23826-113">Create your development environment</span></span>

<span data-ttu-id="23826-114">Если у вас нет учетной записи Microsoft 365, необходимо зарегистрироваться для подписки на программу разработчиков [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="23826-114">If you do not have a Microsoft 365 account, you must sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="23826-115">Подписка бесплатна в течение 90 дней и продолжает обновляться до тех пор, пока вы используете ее для разработки.</span><span class="sxs-lookup"><span data-stu-id="23826-115">The subscription is free for 90 days and continues to renew as long as you are using it for development activity.</span></span> <span data-ttu-id="23826-116">Если у вас есть подписка Visual Studio enterprise или Professional, обе программы [](https://aka.ms/MyVisualStudioBenefits)включают бесплатную подписку на разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="23826-116">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits).</span></span> <span data-ttu-id="23826-117">Она активна до тех пор, пока Visual Studio подписка активна.</span><span class="sxs-lookup"><span data-stu-id="23826-117">It is active for as long as your Visual Studio subscription is active.</span></span> <span data-ttu-id="23826-118">Дополнительные сведения см. в [журнале Set up a Microsoft 365 developer subscription.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="23826-118">For more inforamtion, see [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="23826-119">Включить Microsoft Teams для организации</span><span class="sxs-lookup"><span data-stu-id="23826-119">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="23826-120">Включите Microsoft Teams для вашей организации и взгляните на наши подробные рекомендации по [введению Teams для вашей организации.](/microsoftteams/enable-features-office-365)</span><span class="sxs-lookup"><span data-stu-id="23826-120">Enable Microsoft Teams for your organization and take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="23826-121">Включить настраиваемые приложения Teams и включить настраиваемую загрузку приложений</span><span class="sxs-lookup"><span data-stu-id="23826-121">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="23826-122">**Включить настраиваемую загрузку или загрузку приложения для клиента разработчика**</span><span class="sxs-lookup"><span data-stu-id="23826-122">**To turn on the custom app uploading or sideloading for your developer tenant**</span></span>

1. <span data-ttu-id="23826-123">Во входе [в центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="23826-123">Sign in to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>

2. <span data-ttu-id="23826-124">Выберите **Показать все**  >  **команды.**</span><span class="sxs-lookup"><span data-stu-id="23826-124">Select **Show All** > **Teams**.</span></span>

    ![изображение меню центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > <span data-ttu-id="23826-126">Для появления параметра **Teams** может занять до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="23826-126">It can take up to 24 hours for the **Teams** option to appear.</span></span> <span data-ttu-id="23826-127">В это время вы можете загрузить [свое настраиваемую](/microsoftteams/upload-custom-apps#validate) приложение в среду Teams для тестирования и проверки.</span><span class="sxs-lookup"><span data-stu-id="23826-127">You can [upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation in that time.</span></span>

3. <span data-ttu-id="23826-128">Перейдите в **Teams Apps**  >  **Setup Policies**  >  **Global.**</span><span class="sxs-lookup"><span data-stu-id="23826-128">Navigate to **Teams apps** > **Setup Policies** > **Global**.</span></span>

   ![включить представление боковой нагрузки](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="23826-130">Чтобы загрузить **настраиваемые приложения в** позицию. </span><span class="sxs-lookup"><span data-stu-id="23826-130">Toggle **upload custom apps** to the **on** position.</span></span>

5. <span data-ttu-id="23826-131">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="23826-131">Select **Save**.</span></span>
   <span data-ttu-id="23826-132">Клиент тестового клиента может разрешить настраиваемую загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="23826-132">Your test tenant can permit custom app sideloading.</span></span>

    > [!Note]
    > <span data-ttu-id="23826-133">Для активной загрузки побок может занять до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="23826-133">It can take up to 24 hours for the sideloading to be active.</span></span> <span data-ttu-id="23826-134">Во время промежуточной загрузки **можно использовать для \<your tenant>** тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="23826-134">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

    ![представление приложения updload](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="23826-136">Полные сведения о взаимодействии этих параметров см. в приложении [Manage custom policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and Manage app setup [policies in Microsoft Teams.](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)</span><span class="sxs-lookup"><span data-stu-id="23826-136">For complete information on how these settings interact, see [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>

## <a name="next-step"></a><span data-ttu-id="23826-137">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="23826-137">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="23826-138">Выбор тестовой установки</span><span class="sxs-lookup"><span data-stu-id="23826-138">Choose a test setup</span></span>](~/concepts/build-and-test/debug.md)
> 


