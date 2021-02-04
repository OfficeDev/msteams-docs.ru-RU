---
title: Подготовка клиента Microsoft 365
description: Начало работы с Teams в Microsoft 365
ms.topic: how-to
keywords: Настройка отправки Teams для клиента Microsoft 365
ms.openlocfilehash: 50765271b93edd380d1c23672289b618baf1d346
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093945"
---
# <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="e40a1-104">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="e40a1-104">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="e40a1-105">Если вы подписчик Microsoft 365, вы можете разрабатывать приложения для Microsoft Teams с помощью одного из следующих [планов:](https://products.office.com/business/compare-more-office-365-for-business-plans)</span><span class="sxs-lookup"><span data-stu-id="e40a1-105">If you are a Microsoft 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="e40a1-106">Обычный</span><span class="sxs-lookup"><span data-stu-id="e40a1-106">Basic</span></span>
* <span data-ttu-id="e40a1-107">Стандартный</span><span class="sxs-lookup"><span data-stu-id="e40a1-107">Standard</span></span>
* <span data-ttu-id="e40a1-108">Корпоративные E1, E3 и E5</span><span class="sxs-lookup"><span data-stu-id="e40a1-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="e40a1-109">Developer</span><span class="sxs-lookup"><span data-stu-id="e40a1-109">Developer</span></span>
* <span data-ttu-id="e40a1-110">Education, Education Plus и Education E5</span><span class="sxs-lookup"><span data-stu-id="e40a1-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="e40a1-111">Microsoft Teams также будет доступен клиентам, которые подписаны на E4 до его выхода из [нее.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)</span><span class="sxs-lookup"><span data-stu-id="e40a1-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="e40a1-112">Нужна только среда разработки?</span><span class="sxs-lookup"><span data-stu-id="e40a1-112">Just need a development environment?</span></span>

<span data-ttu-id="e40a1-113">Если у вас нет учетной записи Microsoft 365, вы можете подписаться на программу для разработчиков [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="e40a1-113">If you don't currently have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="e40a1-114">Он *бесплатный* в течение 90 дней и будет постоянно обновляться, пока вы используете его для разработки.</span><span class="sxs-lookup"><span data-stu-id="e40a1-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="e40a1-115">Если у вас есть подписка Visual Studio *Корпоративная* или *Профессиональная,* обе программы включают бесплатную подписку разработчика Microsoft 365, активную в течение Visual Studio подписки. [](https://aka.ms/MyVisualStudioBenefits)</span><span class="sxs-lookup"><span data-stu-id="e40a1-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="e40a1-116">*См.* ["Настройка подписки разработчика Microsoft 365".](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="e40a1-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="e40a1-117">Включить Microsoft Teams для своей организации</span><span class="sxs-lookup"><span data-stu-id="e40a1-117">Enable Microsoft Teams for your organization</span></span> 

<span data-ttu-id="e40a1-118">Если Microsoft Teams не включен для вашей организации, это необходимо сделать в первую очередь.</span><span class="sxs-lookup"><span data-stu-id="e40a1-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="e40a1-119">Подробное руководство по введению [Teams для вашей организации.](/microsoftteams/enable-features-office-365)</span><span class="sxs-lookup"><span data-stu-id="e40a1-119">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="e40a1-120">Включите настраиваемые приложения Teams и включите отправку пользовательских приложений</span><span class="sxs-lookup"><span data-stu-id="e40a1-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="e40a1-121">Включите настраиваемую загрузку нео том же приложения для клиента разработчика следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e40a1-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="e40a1-122">Войдите в [Центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="e40a1-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="e40a1-123">Выберите **"Показать все**  -->  **команды"**.</span><span class="sxs-lookup"><span data-stu-id="e40a1-123">Select **Show All** --> **Teams**.</span></span> 

![Изображение меню Центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> <span data-ttu-id="e40a1-125">Для появления параметра "Teams" может занять до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="e40a1-125">It can take up to 24 hours for the "Teams" option to appear.</span></span> <span data-ttu-id="e40a1-126">Во время промежуточного действия вы можете [отправить пользовательское приложение в среду Teams](/microsoftteams/upload-custom-apps#validate) для тестирования и проверки.</span><span class="sxs-lookup"><span data-stu-id="e40a1-126">During interim, you can [Upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation.</span></span>

3. <span data-ttu-id="e40a1-127">Переход к **глобальным политикам установки** приложений Teams  -->    -->  **(по умолчанию для всей организации)**</span><span class="sxs-lookup"><span data-stu-id="e40a1-127">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![включить представление неогрузки](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="e40a1-129">Перенимите **отправку пользовательских приложений** в **положение "на месте".**</span><span class="sxs-lookup"><span data-stu-id="e40a1-129">Toggle **upload custom apps** to the **on** position.</span></span>

5. <span data-ttu-id="e40a1-130">Выберите **"Сохранить",** чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="e40a1-130">Select **Save** to save the changes.</span></span>

<span data-ttu-id="e40a1-131">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="e40a1-131">That's it!</span></span> <span data-ttu-id="e40a1-132">Теперь тестовый клиент разрешит загрузку неогрузки пользовательского приложения.</span><span class="sxs-lookup"><span data-stu-id="e40a1-132">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="e40a1-133">Загрузка нео боков может занять до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="e40a1-133">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="e40a1-134">В это время вы можете использовать **отправку для \<your tenant>** тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="e40a1-134">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![представление приложения updload](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="e40a1-136">Полные сведения о взаимодействии этих параметров см. в подстройки *"Управление* настраиваемой политикой и настройками приложений в [Microsoft Teams"](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) и "Управление политиками настройки приложений [в Microsoft Teams".](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)</span><span class="sxs-lookup"><span data-stu-id="e40a1-136">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>
