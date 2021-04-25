---
title: Подготовка клиента Microsoft 365
description: Начало работы с Teams в Microsoft 365
ms.topic: how-to
keywords: Настройка отправки команд клиентов Microsoft 365
ms.openlocfilehash: 4fbe1dcc7ba202aff0b46c7fc50d9aebc0278c38
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946468"
---
# <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="88221-104">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="88221-104">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="88221-105">Подписчики Microsoft 365 могут разрабатывать приложения для Microsoft Teams с одним из следующих планов:</span><span class="sxs-lookup"><span data-stu-id="88221-105">Microsoft 365 subscribers can develop apps for Microsoft Teams with one of the following plans:</span></span>

* <span data-ttu-id="88221-106">Обычный</span><span class="sxs-lookup"><span data-stu-id="88221-106">Basic</span></span>
* <span data-ttu-id="88221-107">Стандартный</span><span class="sxs-lookup"><span data-stu-id="88221-107">Standard</span></span>
* <span data-ttu-id="88221-108">Корпоративные E1, E3 и E5</span><span class="sxs-lookup"><span data-stu-id="88221-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="88221-109">Developer</span><span class="sxs-lookup"><span data-stu-id="88221-109">Developer</span></span>
* <span data-ttu-id="88221-110">Education, Education Plus и Education E5</span><span class="sxs-lookup"><span data-stu-id="88221-110">Education, Education Plus, and Education E5</span></span>

> [!NOTE]
> * <span data-ttu-id="88221-111">Дополнительные сведения о подписках на Microsoft 365 см. в [журнале plans.](https://products.office.com/business/compare-more-office-365-for-business-plans)</span><span class="sxs-lookup"><span data-stu-id="88221-111">For more information on Microsoft 365 subscriptions, see [plans](https://products.office.com/business/compare-more-office-365-for-business-plans).</span></span>
> * <span data-ttu-id="88221-112">Teams также доступны для клиентов, подписавших подписку на E4 до ее выхода на [пенсию.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)</span><span class="sxs-lookup"><span data-stu-id="88221-112">Teams is also available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="create-your-development-environment"></a><span data-ttu-id="88221-113">Создание среды разработки</span><span class="sxs-lookup"><span data-stu-id="88221-113">Create your development environment</span></span>

<span data-ttu-id="88221-114">Если у вас нет учетной записи Microsoft 365, необходимо зарегистрироваться для подписки на программу разработчиков [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="88221-114">If you do not have a Microsoft 365 account, you must sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="88221-115">Подписка бесплатна в течение 90 дней и продолжает обновляться до тех пор, пока вы используете ее для разработки.</span><span class="sxs-lookup"><span data-stu-id="88221-115">The subscription is free for 90 days and continues to renew as long as you are using it for development activity.</span></span> <span data-ttu-id="88221-116">Если у вас есть подписка Visual Studio enterprise или Professional, обе программы [](https://aka.ms/MyVisualStudioBenefits)включают бесплатную подписку на разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="88221-116">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits).</span></span> <span data-ttu-id="88221-117">Она активна до тех пор, пока Visual Studio подписка активна.</span><span class="sxs-lookup"><span data-stu-id="88221-117">It is active as long as your Visual Studio subscription is active.</span></span> <span data-ttu-id="88221-118">Дополнительные сведения см. [в журнале Настройка подписки на разработчика Microsoft 365.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="88221-118">For more information, see [set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-teams-for-your-organization"></a><span data-ttu-id="88221-119">Включить Teams для организации</span><span class="sxs-lookup"><span data-stu-id="88221-119">Enable Teams for your organization</span></span>

<span data-ttu-id="88221-120">Включить Teams для организации и дополнительные сведения см. в [дополнительных сведениях о](/microsoftteams/enable-features-office-365)том, как включить Teams для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="88221-120">Enable Teams for your organization and for more information, see [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="88221-121">Включить настраиваемые приложения Teams и включить настраиваемую загрузку приложений</span><span class="sxs-lookup"><span data-stu-id="88221-121">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="88221-122">**Включить настраиваемую загрузку или загрузку приложения для клиента разработчика**</span><span class="sxs-lookup"><span data-stu-id="88221-122">**To turn on the custom app uploading or sideloading for your developer tenant**</span></span>

1. <span data-ttu-id="88221-123">Во входе [в центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="88221-123">Sign in to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>

2. <span data-ttu-id="88221-124">Выберите **Показать все**  >  **команды.**</span><span class="sxs-lookup"><span data-stu-id="88221-124">Select **Show All** > **Teams**.</span></span>

    ![Меню центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > <span data-ttu-id="88221-126">Для появления параметра **Teams** может занять до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="88221-126">It can take up to 24 hours for the **Teams** option to appear.</span></span> <span data-ttu-id="88221-127">В это время вы можете загрузить [свое настраиваемую](/microsoftteams/upload-custom-apps#validate) приложение в среду Teams для тестирования и проверки.</span><span class="sxs-lookup"><span data-stu-id="88221-127">You can [upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation in that time.</span></span>

3. <span data-ttu-id="88221-128">Перейдите в **Teams Apps**  >  **Setup Policies**  >  **Global.**</span><span class="sxs-lookup"><span data-stu-id="88221-128">Navigate to **Teams apps** > **Setup Policies** > **Global**.</span></span>

   ![Включайте представление боковой нагрузки](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="88221-130">Чтобы загрузить **настраиваемые приложения в** положение **On.**</span><span class="sxs-lookup"><span data-stu-id="88221-130">Toggle **Upload custom apps** to the **On** position.</span></span>

5. <span data-ttu-id="88221-131">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="88221-131">Select **Save**.</span></span> <span data-ttu-id="88221-132">Клиент тестового клиента может разрешить настраиваемую загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="88221-132">Your test tenant can permit custom app sideloading.</span></span>

    > [!Note]
    > <span data-ttu-id="88221-133">Для активной загрузки побок может занять до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="88221-133">It can take up to 24 hours for the sideloading to be active.</span></span> <span data-ttu-id="88221-134">В промежуточном периоде вы можете использовать **отправку для \<your tenant>** тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="88221-134">In the interim, you can use **upload for \<your tenant>** to test your app.</span></span> <span data-ttu-id="88221-135">Чтобы загрузить файл пакета .zip приложения, см. в [приложении upload custom apps.](/microsoftteams/upload-custom-apps#upload)</span><span class="sxs-lookup"><span data-stu-id="88221-135">To upload the .zip package file of the app, see [upload custom apps](/microsoftteams/upload-custom-apps#upload).</span></span>

    ![Загрузка представления приложения](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="88221-137">Полные сведения о взаимодействии этих параметров см. в сведениях об управлении настраиваемой политикой и настройками приложений [в Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) и об управлении политиками установки приложений [в Teams.](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)</span><span class="sxs-lookup"><span data-stu-id="88221-137">For complete information on how these settings interact, see [manage custom app policies and settings in Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [manage app setup policies in Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>

## <a name="next-step"></a><span data-ttu-id="88221-138">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="88221-138">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="88221-139">Выбор параметров тестирования</span><span class="sxs-lookup"><span data-stu-id="88221-139">Choose a test setup</span></span>](~/concepts/build-and-test/debug.md)

