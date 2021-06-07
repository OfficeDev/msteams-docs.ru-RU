---
title: Подготовка к отправке в магазин
description: Описывает последние действия перед отправкой Microsoft Teams приложения, которое будет перечислены в магазине.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: c0f9c3328018884290c86a49b8026ce81022cd83
ms.sourcegitcommit: 25539046d408c4270b988fd826d7cf1275f4b9dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2021
ms.locfileid: "52763110"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a><span data-ttu-id="abb03-103">Подготовка отправки Microsoft Teams магазина</span><span class="sxs-lookup"><span data-stu-id="abb03-103">Prepare your Microsoft Teams store submission</span></span>

<span data-ttu-id="abb03-104">Вы разработали, создали и протестировали Microsoft Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="abb03-104">You've designed, built, and tested your Microsoft Teams app.</span></span> <span data-ttu-id="abb03-105">Теперь вы готовы перечислить его, чтобы люди могли обнаружить и начать использовать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="abb03-105">Now you're ready to list it so people can discover and start using your app.</span></span>

<span data-ttu-id="abb03-106">Перед отправкой приложения в [Центр партнеров](/office/dev/store/use-partner-center-to-submit-to-appsource)убедитесь, что вы сделали следующее.</span><span class="sxs-lookup"><span data-stu-id="abb03-106">Before you submit your app to [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource), make sure you've done the following.</span></span>

## <a name="validate-your-app-package"></a><span data-ttu-id="abb03-107">Проверка пакета приложений</span><span class="sxs-lookup"><span data-stu-id="abb03-107">Validate your app package</span></span>

<span data-ttu-id="abb03-108">Хотя ваше приложение может работать в тестовой среде, необходимо проверить пакет приложений, чтобы избежать проблем во время процесса отправки.</span><span class="sxs-lookup"><span data-stu-id="abb03-108">While your app may be working in a test environment, you should check your app package to avoid running into issues during the submission process.</span></span>

<span data-ttu-id="abb03-109">Средство Microsoft Teams проверки приложений помогает выявлять и устранять проблемы перед отправкой в Центр партнеров.</span><span class="sxs-lookup"><span data-stu-id="abb03-109">The Microsoft Teams app validation tool helps you identify and fix issues before submitting to Partner Center.</span></span> <span data-ttu-id="abb03-110">Средство автоматически проверяет конфигурации вашего приложения на фоне тех же тестовых случаев, используемых во время проверки в магазине.</span><span class="sxs-lookup"><span data-stu-id="abb03-110">The tool automatically checks your app's configurations against the same test cases used during store validation.</span></span>

1. <span data-ttu-id="abb03-111">Перейдите к [средству проверки Microsoft Teams приложения.](https://dev.teams.microsoft.com/appvalidation.html)</span><span class="sxs-lookup"><span data-stu-id="abb03-111">Go to the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span></span> <span data-ttu-id="abb03-112">(Примечание. Этот инструмент также доступен в [App Studio.)](../../../build-and-test/app-studio-overview.md)</span><span class="sxs-lookup"><span data-stu-id="abb03-112">(Note: The tool is also available in [App Studio](../../../build-and-test/app-studio-overview.md).)</span></span>
1. <span data-ttu-id="abb03-113">Upload пакет приложения для запуска автоматических тестов.</span><span class="sxs-lookup"><span data-stu-id="abb03-113">Upload your app package to run the automated tests.</span></span>
1. <span data-ttu-id="abb03-114">Перейдите в **предварительный контрольный список** и просмотрите тестовые случаи, которые трудно автоматизировать.</span><span class="sxs-lookup"><span data-stu-id="abb03-114">Go to the **Preliminary checklist** and review the test cases that are difficult to automate.</span></span>
1. <span data-ttu-id="abb03-115">[Устранение проблем с](~/resources/schema/manifest-schema.md) конфигурациями или приложением в целом, если автоматические тесты дают вам ошибки или вы не выполнили все критерии в списке.</span><span class="sxs-lookup"><span data-stu-id="abb03-115">[Fix issues with your configurations](~/resources/schema/manifest-schema.md) or app in general if the automated tests give you errors or you haven't met all the criteria in the checklist.</span></span>

## <a name="compile-testing-instructions"></a><span data-ttu-id="abb03-116">Компиляляйте инструкции по тестированию</span><span class="sxs-lookup"><span data-stu-id="abb03-116">Compile testing instructions</span></span>

<span data-ttu-id="abb03-117">Предоставление инструкций и ресурсов, которые помогут рецензентам протестировать ваше приложение, включая тестовые учетные записи, учетные данные и ключи лицензии.</span><span class="sxs-lookup"><span data-stu-id="abb03-117">Provide instructions and resources to help the reviewers test your app, including test accounts, credentials, and license keys.</span></span> <span data-ttu-id="abb03-118">Вы можете добавить инструкции в Центре партнеров или загрузить их в общедоступные расположения в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="abb03-118">You can add instructions in Partner Center or upload them to a publicly available location on SharePoint.</span></span>

### <a name="feature-list"></a><span data-ttu-id="abb03-119">Список функций</span><span class="sxs-lookup"><span data-stu-id="abb03-119">Feature list</span></span>

<span data-ttu-id="abb03-120">Сведения о возможностях вашего приложения в Teams и действиях для тестирования каждого из них.</span><span class="sxs-lookup"><span data-stu-id="abb03-120">Provide details about your app's capabilities in Teams and steps for testing each one.</span></span>

### <a name="accounts"></a><span data-ttu-id="abb03-121">Учетные записи</span><span class="sxs-lookup"><span data-stu-id="abb03-121">Accounts</span></span>

<span data-ttu-id="abb03-122">Необходимо предоставить тестовые учетные записи, если вашему приложению требуется лицензия или дополнительный безопасный список.</span><span class="sxs-lookup"><span data-stu-id="abb03-122">You must provide test accounts if your app requires a license or backend safelisting.</span></span> <span data-ttu-id="abb03-123">Все учетные записи, которые вы предоставляете, должны включать предварительно заполненные данные для облегчения тестирования.</span><span class="sxs-lookup"><span data-stu-id="abb03-123">All accounts you provide must include pre-populated data to facilitate testing.</span></span>

<span data-ttu-id="abb03-124">В зависимости от функций приложения может потребоваться предоставить все следующие функции:</span><span class="sxs-lookup"><span data-stu-id="abb03-124">Depending on your app's features, you may need to provide all of the following:</span></span>

* <span data-ttu-id="abb03-125">Учетная запись администратора (требуется)</span><span class="sxs-lookup"><span data-stu-id="abb03-125">Admin account (required)</span></span>
* <span data-ttu-id="abb03-126">Учетная запись без администрирования (требуется)</span><span class="sxs-lookup"><span data-stu-id="abb03-126">Non-admin account (required)</span></span>
* <span data-ttu-id="abb03-127">Учетная запись, которая не настроена заранее, чтобы правильно протестировать первый запуск работы с входом (обязательно)</span><span class="sxs-lookup"><span data-stu-id="abb03-127">An account that isn't pre-configured in order to properly test the first-run sign-in experience (required)</span></span>
* <span data-ttu-id="abb03-128">Учетная запись с доступом к премиум-или обновленным функциям (если применимо)</span><span class="sxs-lookup"><span data-stu-id="abb03-128">An account with access to premium or upgraded features (if applicable)</span></span>
* <span data-ttu-id="abb03-129">Две учетные записи в одном клиенте для проверки взаимодействия для приложений, которые работают в общих контекстах (если применимо)</span><span class="sxs-lookup"><span data-stu-id="abb03-129">Two accounts in the same tenant to test the collaboration experience for apps that work in shared contexts (if applicable)</span></span>

### <a name="tenant-configurations"></a><span data-ttu-id="abb03-130">Конфигурации клиента</span><span class="sxs-lookup"><span data-stu-id="abb03-130">Tenant configurations</span></span>

<span data-ttu-id="abb03-131">Если необходимо настроить клиента Teams для использования приложения, включите эти инструкции и учетные записи администратора и не администратора для проверки.</span><span class="sxs-lookup"><span data-stu-id="abb03-131">If you must configure a Teams tenant to use your app, include those instructions and admin and non-admin accounts for validation.</span></span>

### <a name="video-optional"></a><span data-ttu-id="abb03-132">Видео (необязательно)</span><span class="sxs-lookup"><span data-stu-id="abb03-132">Video (optional)</span></span>

<span data-ttu-id="abb03-133">Предописите запись вашего приложения, чтобы Корпорация Майкрософт полностью понимала его функции.</span><span class="sxs-lookup"><span data-stu-id="abb03-133">Provide a recording of your app so that Microsoft can fully understand its functionality.</span></span>

## <a name="create-your-store-listing-details"></a><span data-ttu-id="abb03-134">Создание сведений о списке магазина</span><span class="sxs-lookup"><span data-stu-id="abb03-134">Create your store listing details</span></span>

<span data-ttu-id="abb03-135">Сведения, которые вы [](https://partner.microsoft.com) передаете в Центр партнеров&#8212;включая ваше имя, описания, значки и изображения,&#8212;становятся Teams магазином и списком Microsoft AppSource для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="abb03-135">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="abb03-136">Список магазинов может быть первым впечатлением от вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="abb03-136">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="abb03-137">Увеличение установок с помощью списка, который эффективно передает преимущества, функциональные возможности и бренд вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="abb03-137">Increase installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

### <a name="specify-a-short-name"></a><span data-ttu-id="abb03-138">Укажите короткое имя</span><span class="sxs-lookup"><span data-stu-id="abb03-138">Specify a short name</span></span>

<span data-ttu-id="abb03-139">Имя вашего приложения (в частности, его короткое [*имя)*](~/resources/schema/manifest-schema.md#name)играет решающую роль в том, как пользователи обнаруживают его в магазине.</span><span class="sxs-lookup"><span data-stu-id="abb03-139">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="Пример экрана показывает, где короткое имя приложения отображается в списке магазина.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="abb03-141">Убедитесь, что ваше короткое имя соответствует рекомендациям по [проверке хранения.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#app-name)</span><span class="sxs-lookup"><span data-stu-id="abb03-141">Make sure your short name adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#app-name).</span></span>

### <a name="write-descriptions"></a><span data-ttu-id="abb03-142">Написание описаний</span><span class="sxs-lookup"><span data-stu-id="abb03-142">Write descriptions</span></span>

<span data-ttu-id="abb03-143">Вы должны иметь краткое и длинное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="abb03-143">You must have a short and long description of your app.</span></span>

#### <a name="short-description"></a><span data-ttu-id="abb03-144">Краткое описание</span><span class="sxs-lookup"><span data-stu-id="abb03-144">Short description</span></span>

<span data-ttu-id="abb03-145">Краткий сводка приложения, которая должна быть оригинальной, привлекательной и направленной для целевой аудитории.</span><span class="sxs-lookup"><span data-stu-id="abb03-145">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="abb03-146">Сохраняй краткое описание в одном предложении.</span><span class="sxs-lookup"><span data-stu-id="abb03-146">Keep the short description to one sentence.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Пример экрана показывает, где краткое описание приложения отображается в списке магазина.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="abb03-148">Убедитесь, что краткое описание соответствует рекомендациям по проверке [хранения.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#short-description)</span><span class="sxs-lookup"><span data-stu-id="abb03-148">Make sure your short description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#short-description).</span></span>

#### <a name="long-description"></a><span data-ttu-id="abb03-149">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="abb03-149">Long description</span></span>

<span data-ttu-id="abb03-150">Длинное описание может предоставить повествование, которое выделяет основные функции приложения, проблемы, которые оно решает, и его целевую аудиторию.</span><span class="sxs-lookup"><span data-stu-id="abb03-150">The long description can provide a narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="abb03-151">Хотя это описание может быть до 4000 символов, большинство пользователей будут читать только между 300-500 слов.</span><span class="sxs-lookup"><span data-stu-id="abb03-151">While this description can be as long as 4,000 characters, most users will only read between 300-500 words.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="Пример экрана показывает, где длинное описание приложения отображается в списке магазина.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="abb03-153">Убедитесь, что ваше длинное описание соответствует рекомендациям проверки [магазина.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#long-description)</span><span class="sxs-lookup"><span data-stu-id="abb03-153">Make sure your long description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#long-description).</span></span>

### <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="abb03-154">Соблюдайте рекомендации по проектированию значков</span><span class="sxs-lookup"><span data-stu-id="abb03-154">Adhere to icon design guidelines</span></span>

<span data-ttu-id="abb03-155">Значки являются одним из основных элементов, которые пользователи видят при просмотре магазина.</span><span class="sxs-lookup"><span data-stu-id="abb03-155">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="abb03-156">Значки должны сообщать о фирме и цели приложения, а также о Teams требованиях.</span><span class="sxs-lookup"><span data-stu-id="abb03-156">Your icons should communicate your app's brand and purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="abb03-157">Дополнительные сведения см. [в руководстве по созданию значков Teams приложений.](~/concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="abb03-157">For more information, see [guidance on creating Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

### <a name="capture-screenshots"></a><span data-ttu-id="abb03-158">Захват скриншотов</span><span class="sxs-lookup"><span data-stu-id="abb03-158">Capture screenshots</span></span>

<span data-ttu-id="abb03-159">Скриншоты предоставляют видную визуальную предварительную версию приложения в дополнение к имени, значку и описаниям приложения.</span><span class="sxs-lookup"><span data-stu-id="abb03-159">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="Пример экрана показывает, где скриншоты приложений отображаются в списке магазина.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="abb03-161">Помните следующие снимки экрана:</span><span class="sxs-lookup"><span data-stu-id="abb03-161">Remember the following about screenshots:</span></span>

* <span data-ttu-id="abb03-162">В списке может быть до пяти снимков экрана.</span><span class="sxs-lookup"><span data-stu-id="abb03-162">You can have up to five screenshots per listing.</span></span>
* <span data-ttu-id="abb03-163">Поддерживаемые типы файлов включают PNG, JPEG и GIF.</span><span class="sxs-lookup"><span data-stu-id="abb03-163">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="abb03-164">Размеры должны быть 1366x768 пикселей.</span><span class="sxs-lookup"><span data-stu-id="abb03-164">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="abb03-165">Максимальный размер 1024 КБ.</span><span class="sxs-lookup"><span data-stu-id="abb03-165">Maximum size of 1,024 KB.</span></span>

<span data-ttu-id="abb03-166">Дополнительные возможности см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="abb03-166">For best practices, see the following resources:</span></span>

* [<span data-ttu-id="abb03-167">Teams проверки хранения</span><span class="sxs-lookup"><span data-stu-id="abb03-167">Teams store validation guidelines</span></span>](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#screenshots)
* [<span data-ttu-id="abb03-168">Создай эффективные изображения для магазинов приложений Майкрософт</span><span class="sxs-lookup"><span data-stu-id="abb03-168">Craft effective images for Microsoft app stores</span></span>](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a><span data-ttu-id="abb03-169">Создание видео</span><span class="sxs-lookup"><span data-stu-id="abb03-169">Create a video</span></span>

<span data-ttu-id="abb03-170">Видео в вашем списке может быть наиболее эффективным способом сообщить, почему люди должны использовать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="abb03-170">A video in your listing can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="abb03-171">В видео необходимо ответить на следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="abb03-171">You should address the following questions in a video:</span></span>

* <span data-ttu-id="abb03-172">Кто для вашего приложения?</span><span class="sxs-lookup"><span data-stu-id="abb03-172">Who is your app for?</span></span>
* <span data-ttu-id="abb03-173">Какие проблемы может решить приложение?</span><span class="sxs-lookup"><span data-stu-id="abb03-173">What problems can your app solve?</span></span>
* <span data-ttu-id="abb03-174">Как работает ваше приложение?</span><span class="sxs-lookup"><span data-stu-id="abb03-174">How does your app work?</span></span>
* <span data-ttu-id="abb03-175">Какие еще преимущества вы получаете от использования приложения?</span><span class="sxs-lookup"><span data-stu-id="abb03-175">What other benefits do you get from using your app?</span></span>

#### <a name="best-practices-for-videos"></a><span data-ttu-id="abb03-176">Лучшие практики для видео</span><span class="sxs-lookup"><span data-stu-id="abb03-176">Best practices for videos</span></span>

* <span data-ttu-id="abb03-177">Сохраняйте видео в течение 30-90 секунд.</span><span class="sxs-lookup"><span data-stu-id="abb03-177">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="abb03-178">Стремиться к качеству.</span><span class="sxs-lookup"><span data-stu-id="abb03-178">Aim for quality.</span></span> <span data-ttu-id="abb03-179">В списке пользователи увидят ваше видео перед снимками экрана.</span><span class="sxs-lookup"><span data-stu-id="abb03-179">In a listing, users will see your video before screenshots.</span></span>

### <a name="select-a-category-for-your-app"></a><span data-ttu-id="abb03-180">Выберите категорию для приложения</span><span class="sxs-lookup"><span data-stu-id="abb03-180">Select a category for your app</span></span>

<span data-ttu-id="abb03-181">Во время отправки вам будет предложено классифицировать приложение.</span><span class="sxs-lookup"><span data-stu-id="abb03-181">During submission, you're asked to categorize your app.</span></span> <span data-ttu-id="abb03-182">В следующей таблице Teams категории магазинов к категориям, перечисленным в [Центре партнеров.](https://aka.ms/PartnerCenterHomePage)</span><span class="sxs-lookup"><span data-stu-id="abb03-182">The following table maps Teams store categories to the categories listed in [Partner Center](https://aka.ms/PartnerCenterHomePage).</span></span>

| <span data-ttu-id="abb03-183">Teams категорий</span><span class="sxs-lookup"><span data-stu-id="abb03-183">Teams categories</span></span>       | <span data-ttu-id="abb03-184">Категории Центра партнеров</span><span class="sxs-lookup"><span data-stu-id="abb03-184">Partner Center categories</span></span>  |
|:---------------------|:---------------|
| <span data-ttu-id="abb03-185">Аналитика и бизнес-аналитика</span><span class="sxs-lookup"><span data-stu-id="abb03-185">Analytics and BI</span></span> | <span data-ttu-id="abb03-186">Аналитика, визуализация данных и bi</span><span class="sxs-lookup"><span data-stu-id="abb03-186">Analytics, Data Visualization and BI</span></span> |
| <span data-ttu-id="abb03-187">Разработчик и ИТ</span><span class="sxs-lookup"><span data-stu-id="abb03-187">Developer and IT</span></span> | <span data-ttu-id="abb03-188">Средства разработчика, ИТ-администратор</span><span class="sxs-lookup"><span data-stu-id="abb03-188">Developer Tools, IT Admin</span></span> |
| <span data-ttu-id="abb03-189">Образование</span><span class="sxs-lookup"><span data-stu-id="abb03-189">Education</span></span> | <span data-ttu-id="abb03-190">Образование</span><span class="sxs-lookup"><span data-stu-id="abb03-190">Education</span></span> |
| <span data-ttu-id="abb03-191">Управление персоналом</span><span class="sxs-lookup"><span data-stu-id="abb03-191">Human resources</span></span> | <span data-ttu-id="abb03-192">Кадры и рекрутинг</span><span class="sxs-lookup"><span data-stu-id="abb03-192">Human Resources and Recruiting</span></span> |
| <span data-ttu-id="abb03-193">Эффективность</span><span class="sxs-lookup"><span data-stu-id="abb03-193">Productivity</span></span> | <span data-ttu-id="abb03-194">Управление контентом, файлы и документы, производительность, обучение и учебники и утилиты</span><span class="sxs-lookup"><span data-stu-id="abb03-194">Content Management, Files and documents, Productivity, Training and Tutorials, and Utilities</span></span> |
| <span data-ttu-id="abb03-195">Управление проектами</span><span class="sxs-lookup"><span data-stu-id="abb03-195">Project management</span></span> | <span data-ttu-id="abb03-196">Коммуникация, Project управление, рабочий процесс и управление бизнесом</span><span class="sxs-lookup"><span data-stu-id="abb03-196">Communication, Project Management, Workflow, and Business Management</span></span> |
| <span data-ttu-id="abb03-197">Продажи и поддержка</span><span class="sxs-lookup"><span data-stu-id="abb03-197">Sales and support</span></span> | <span data-ttu-id="abb03-198">Управление клиентами и контактами, поддержка клиентов, финансовое управление, продажи и маркетинг</span><span class="sxs-lookup"><span data-stu-id="abb03-198">Customer and Contact Management, Customer Support, Financial Management, Sales and Marketing</span></span> |
| <span data-ttu-id="abb03-199">Социальная и веселая</span><span class="sxs-lookup"><span data-stu-id="abb03-199">Social and fun</span></span> | <span data-ttu-id="abb03-200">Image and Video Galleries, Lifestyle, News and Weather, Social, Travel and Navigation</span><span class="sxs-lookup"><span data-stu-id="abb03-200">Image and Video Galleries, Lifestyle, News and Weather, Social, Travel, and Navigation</span></span> |

### <a name="localize-your-store-listing"></a><span data-ttu-id="abb03-201">Локализовать список магазина</span><span class="sxs-lookup"><span data-stu-id="abb03-201">Localize your store listing</span></span>

<span data-ttu-id="abb03-202">Центр партнеров поддерживает [локализованные списки магазинов.](/office/dev/store/prepare-localized-solutions)</span><span class="sxs-lookup"><span data-stu-id="abb03-202">Partner Center supports [localized store listings](/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="abb03-203">Дополнительные сведения см. [в том, как локализовать список Teams приложения.](../../../../concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="abb03-203">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="complete-publisher-verification"></a><span data-ttu-id="abb03-204">Полное Publisher проверки</span><span class="sxs-lookup"><span data-stu-id="abb03-204">Complete Publisher Verification</span></span>

<span data-ttu-id="abb03-205">[Publisher для](/azure/active-directory/develop/publisher-verification-overview) Teams приложений, перечисленных в магазине.</span><span class="sxs-lookup"><span data-stu-id="abb03-205">[Publisher Verification](/azure/active-directory/develop/publisher-verification-overview) is required for Teams apps listed in the store.</span></span> <span data-ttu-id="abb03-206">Дополнительные сведения см. в [](/azure/active-directory/develop/mark-app-as-publisher-verified)часто [задаваемом вопросе,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)о том, как пометить ваше приложение как проверенного издателя и устранить [неполадки в проверке издателя.](/azure/active-directory/develop/troubleshoot-publisher-verification)</span><span class="sxs-lookup"><span data-stu-id="abb03-206">For more information, see [frequently asked questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [how to mark your app as publisher verified](/azure/active-directory/develop/mark-app-as-publisher-verified), and [troubleshoot publisher verification](/azure/active-directory/develop/troubleshoot-publisher-verification).</span></span>

## <a name="complete-publisher-attestation"></a><span data-ttu-id="abb03-207">Полное Publisher проверки</span><span class="sxs-lookup"><span data-stu-id="abb03-207">Complete Publisher Attestation</span></span>

<span data-ttu-id="abb03-208">[Publisher также](/microsoft-365-app-certification/docs/attestation) требуется для Teams приложений, перечисленных в магазине.</span><span class="sxs-lookup"><span data-stu-id="abb03-208">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation) is also required for Teams apps listed in the store.</span></span> <span data-ttu-id="abb03-209">Этот процесс включает в себя самооценку безопасности, обработки данных и соответствия требованиям, которые могут помочь потенциальным клиентам принимать обоснованные решения об использовании приложения.</span><span class="sxs-lookup"><span data-stu-id="abb03-209">The process includes completing a self-assessment of your app's security, data handling, and compliance practices that can help potential customers make informed decisions about using your app.</span></span>

> [!NOTE]
> <span data-ttu-id="abb03-210">Если вы отправили новое приложение, вы не можете официально завершить проверку Publisher, пока ваше приложение не будет перечислены в Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="abb03-210">If you're submitting a new app, you can't officially complete Publisher Attestation until your app is listed on the Teams store.</span></span> <span data-ttu-id="abb03-211">Если вы обновляете перечисленное приложение, Publisher проверку перед отправкой последней версии приложения для проверки.</span><span class="sxs-lookup"><span data-stu-id="abb03-211">If you're updating a listed app, complete Publisher Attestation before you submit the latest version of the app for validation.</span></span>

## <a name="next-step"></a><span data-ttu-id="abb03-212">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="abb03-212">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="abb03-213">Отправка приложения</span><span class="sxs-lookup"><span data-stu-id="abb03-213">Submit your app</span></span>](/office/dev/store/add-in-submission-guide)
