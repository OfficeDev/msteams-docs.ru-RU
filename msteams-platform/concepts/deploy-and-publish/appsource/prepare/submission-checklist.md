---
title: Подготовка к отправке в магазин
description: Описывает последние шаги перед отправкой вашего Microsoft Teams, которое будет перечислено в магазине.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 975d3ef8fc8bdc8d6d7c336cf3a61a3a42ef5315
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566035"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a><span data-ttu-id="30ff4-103">Подготовь Microsoft Teams представления магазина</span><span class="sxs-lookup"><span data-stu-id="30ff4-103">Prepare your Microsoft Teams store submission</span></span>

<span data-ttu-id="30ff4-104">Вы разработали, построили и протестировали свое Microsoft Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="30ff4-104">You've designed, built, and tested your Microsoft Teams app.</span></span> <span data-ttu-id="30ff4-105">Теперь вы готовы перечислить его, чтобы люди могли обнаружить и начать использовать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="30ff4-105">Now you're ready to list it so people can discover and start using your app.</span></span>

<span data-ttu-id="30ff4-106">Перед отправкой приложения в [Партнерский центр](/office/dev/store/use-partner-center-to-submit-to-appsource)убедитесь, что вы сделали следующее.</span><span class="sxs-lookup"><span data-stu-id="30ff4-106">Before you submit your app to [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource), make sure you've done the following.</span></span>

## <a name="validate-your-app-package"></a><span data-ttu-id="30ff4-107">Проверка пакета приложений</span><span class="sxs-lookup"><span data-stu-id="30ff4-107">Validate your app package</span></span>

<span data-ttu-id="30ff4-108">Хотя приложение может работать в тестовой среде, следует проверить пакет приложений, чтобы избежать проблем в процессе отправки.</span><span class="sxs-lookup"><span data-stu-id="30ff4-108">While your app may be working in a test environment, you should check your app package to avoid running into issues during the submission process.</span></span>

<span data-ttu-id="30ff4-109">Инструмент Microsoft Teams проверки приложений поможет вам выявить и устранить проблемы перед отправкой в Партнерский центр.</span><span class="sxs-lookup"><span data-stu-id="30ff4-109">The Microsoft Teams app validation tool helps you identify and fix issues before submitting to Partner Center.</span></span> <span data-ttu-id="30ff4-110">Инструмент автоматически проверяет конфигурации приложения на тех же тестовых случаях, которые использовались во время проверки магазина.</span><span class="sxs-lookup"><span data-stu-id="30ff4-110">The tool automatically checks your app's configurations against the same test cases used during store validation.</span></span>

1. <span data-ttu-id="30ff4-111">Перейти к [Microsoft Teams проверки приложения](https://dev.teams.microsoft.com/appvalidation.html).</span><span class="sxs-lookup"><span data-stu-id="30ff4-111">Go to the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span></span> <span data-ttu-id="30ff4-112">(Примечание: Инструмент также доступен в [App Studio](../../../build-and-test/app-studio-overview.md).)</span><span class="sxs-lookup"><span data-stu-id="30ff4-112">(Note: The tool is also available in [App Studio](../../../build-and-test/app-studio-overview.md).)</span></span>
1. <span data-ttu-id="30ff4-113">Upload пакет приложений для запуска автоматизированных тестов.</span><span class="sxs-lookup"><span data-stu-id="30ff4-113">Upload your app package to run the automated tests.</span></span>
1. <span data-ttu-id="30ff4-114">Перейдите в **предварительный контрольный** список и просмотрите тестовые случаи, которые трудно автоматизировать.</span><span class="sxs-lookup"><span data-stu-id="30ff4-114">Go to the **Preliminary checklist** and review the test cases that are difficult to automate.</span></span>
1. <span data-ttu-id="30ff4-115">[Исправьте проблемы с конфигурациями или](~/resources/schema/manifest-schema.md) приложением в целом, если автоматизированные тесты дают вам ошибки или вы не выполнили все критерии в контрольном списке.</span><span class="sxs-lookup"><span data-stu-id="30ff4-115">[Fix issues with your configurations](~/resources/schema/manifest-schema.md) or app in general if the automated tests give you errors or you haven't met all the criteria in the checklist.</span></span>

## <a name="compile-testing-instructions"></a><span data-ttu-id="30ff4-116">Составить инструкции по тестированию</span><span class="sxs-lookup"><span data-stu-id="30ff4-116">Compile testing instructions</span></span>

<span data-ttu-id="30ff4-117">Предоставьте инструкции и ресурсы, чтобы помочь рецензентам протестировать ваше приложение, включая тестовые учетные записи, учетные данные и ключи лицензии.</span><span class="sxs-lookup"><span data-stu-id="30ff4-117">Provide instructions and resources to help the reviewers test your app, including test accounts, credentials, and license keys.</span></span> <span data-ttu-id="30ff4-118">Вы можете добавить инструкции в Партнер-центре или загрузить их в общедоступное место SharePoint.</span><span class="sxs-lookup"><span data-stu-id="30ff4-118">You can add instructions in Partner Center or upload them to a publicly available location on SharePoint.</span></span>

### <a name="feature-list"></a><span data-ttu-id="30ff4-119">Список функций</span><span class="sxs-lookup"><span data-stu-id="30ff4-119">Feature list</span></span>

<span data-ttu-id="30ff4-120">Предоставьте подробную информацию о возможностях приложения в Teams и шагах для тестирования каждого из них.</span><span class="sxs-lookup"><span data-stu-id="30ff4-120">Provide details about your app's capabilities in Teams and steps for testing each one.</span></span>

### <a name="accounts"></a><span data-ttu-id="30ff4-121">Учетные записи</span><span class="sxs-lookup"><span data-stu-id="30ff4-121">Accounts</span></span>

<span data-ttu-id="30ff4-122">Вы должны предоставить тестовые учетные записи, если вашему приложению требуется лицензия или бэкэнд-безопасный список.</span><span class="sxs-lookup"><span data-stu-id="30ff4-122">You must provide test accounts if your app requires a license or backend safelisting.</span></span> <span data-ttu-id="30ff4-123">Все учетные записи, которые вы предоставляете, должны включать предварительно заселенные данные для облегчения тестирования.</span><span class="sxs-lookup"><span data-stu-id="30ff4-123">All accounts you provide must include pre-populated data to facilitate testing.</span></span>

<span data-ttu-id="30ff4-124">В зависимости от функций приложения может потребоваться предоставить все следующие:</span><span class="sxs-lookup"><span data-stu-id="30ff4-124">Depending on your app's features, you may need to provide all of the following:</span></span>

* <span data-ttu-id="30ff4-125">Учетная запись администратора (требуется)</span><span class="sxs-lookup"><span data-stu-id="30ff4-125">Admin account (required)</span></span>
* <span data-ttu-id="30ff4-126">Учетная запись без администратора (требуется)</span><span class="sxs-lookup"><span data-stu-id="30ff4-126">Non-admin account (required)</span></span>
* <span data-ttu-id="30ff4-127">Учетная запись, которая не настроена заранее, чтобы должным образом протестировать первый запуск в режиме действия (требуется)</span><span class="sxs-lookup"><span data-stu-id="30ff4-127">An account that isn't pre-configured in order to properly test the first-run sign-in experience (required)</span></span>
* <span data-ttu-id="30ff4-128">Учетная запись с доступом к премиум или обновленным функциям (если это применимо)</span><span class="sxs-lookup"><span data-stu-id="30ff4-128">An account with access to premium or upgraded features (if applicable)</span></span>
* <span data-ttu-id="30ff4-129">Две учетные записи в одном и том же арендаторе для проверки опыта совместной работы приложений, которые работают в общих контекстах (если это применимо)</span><span class="sxs-lookup"><span data-stu-id="30ff4-129">Two accounts in the same tenant to test the collaboration experience for apps that work in shared contexts (if applicable)</span></span>

### <a name="tenant-configurations"></a><span data-ttu-id="30ff4-130">Конфигурации арендаторов</span><span class="sxs-lookup"><span data-stu-id="30ff4-130">Tenant configurations</span></span>

<span data-ttu-id="30ff4-131">Если вы должны настроить Teams для использования приложения, включите эти инструкции и учетные записи администратора и не администратора для проверки.</span><span class="sxs-lookup"><span data-stu-id="30ff4-131">If you must configure a Teams tenant to use your app, include those instructions and admin and non-admin accounts for validation.</span></span>

### <a name="video-optional"></a><span data-ttu-id="30ff4-132">Видео (по желанию)</span><span class="sxs-lookup"><span data-stu-id="30ff4-132">Video (optional)</span></span>

<span data-ttu-id="30ff4-133">Предоставьте запись вашего приложения, чтобы корпорация Майкрософт можно было полностью понять его функциональность.</span><span class="sxs-lookup"><span data-stu-id="30ff4-133">Provide a recording of your app so that Microsoft can fully understand its functionality.</span></span>

## <a name="create-your-store-listing-details"></a><span data-ttu-id="30ff4-134">Создайте сведения о листинге в магазине</span><span class="sxs-lookup"><span data-stu-id="30ff4-134">Create your store listing details</span></span>

<span data-ttu-id="30ff4-135">Информация, которую вы отправляете [в Партнерский](https://partner.microsoft.com) центр&#8212;включая ваше имя, описания, значки и изображения&#8212;становится магазином Teams и списком Microsoft AppSource для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="30ff4-135">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="30ff4-136">Объявление в магазине может быть первым впечатлением от вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="30ff4-136">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="30ff4-137">Увеличьте установки с помощью списка, который эффективно передает преимущества, функциональность и бренд вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="30ff4-137">Increase installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

### <a name="specify-a-short-name"></a><span data-ttu-id="30ff4-138">Укажите короткое имя</span><span class="sxs-lookup"><span data-stu-id="30ff4-138">Specify a short name</span></span>

<span data-ttu-id="30ff4-139">Имя вашего приложения (в частности, его [*короткое имя)*](~/resources/schema/manifest-schema.md#name)играет решающую роль в том, как пользователи обнаруживают его в магазине.</span><span class="sxs-lookup"><span data-stu-id="30ff4-139">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="Пример скриншота показывает, где короткое имя приложения отображается в списке магазина.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="30ff4-141">Убедитесь, что ваше короткое имя [придерживается принципов проверки магазина.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)</span><span class="sxs-lookup"><span data-stu-id="30ff4-141">Make sure your short name adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name).</span></span>

### <a name="write-descriptions"></a><span data-ttu-id="30ff4-142">Пишите описания</span><span class="sxs-lookup"><span data-stu-id="30ff4-142">Write descriptions</span></span>

<span data-ttu-id="30ff4-143">Вы должны иметь краткое и длинное описание вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="30ff4-143">You must have a short and long description of your app.</span></span>

#### <a name="short-description"></a><span data-ttu-id="30ff4-144">Краткое описание</span><span class="sxs-lookup"><span data-stu-id="30ff4-144">Short description</span></span>

<span data-ttu-id="30ff4-145">Краткое резюме приложения, которое должно быть оригинальным, привлекательным и направленным на целевую аудиторию.</span><span class="sxs-lookup"><span data-stu-id="30ff4-145">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="30ff4-146">Держите краткое описание в одном предложении.</span><span class="sxs-lookup"><span data-stu-id="30ff4-146">Keep the short description to one sentence.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Пример скриншота показывает, где краткое описание приложения отображается в объявлении магазина.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="30ff4-148">Убедитесь, что ваше краткое описание придерживается [руководящих принципов проверки магазина.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)</span><span class="sxs-lookup"><span data-stu-id="30ff4-148">Make sure your short description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description).</span></span>

#### <a name="long-description"></a><span data-ttu-id="30ff4-149">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="30ff4-149">Long description</span></span>

<span data-ttu-id="30ff4-150">Длинное описание может предоставить повествование, которое подчеркивает основные функции вашего приложения, проблемы, которые оно решает, и его целевую аудиторию.</span><span class="sxs-lookup"><span data-stu-id="30ff4-150">The long description can provide a narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="30ff4-151">Хотя это описание может быть до тех пор, как 4000 символов, большинство пользователей будет читать только между 300-500 слов.</span><span class="sxs-lookup"><span data-stu-id="30ff4-151">While this description can be as long as 4,000 characters, most users will only read between 300-500 words.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="Пример скриншота показывает, где длинное описание приложения отображается в объявлении магазина.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="30ff4-153">Убедитесь, что ваше длинное описание придерживается [принципов проверки магазина.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)</span><span class="sxs-lookup"><span data-stu-id="30ff4-153">Make sure your long description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description).</span></span>

### <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="30ff4-154">Придерживайтесь руководящих принципов проектирования значков</span><span class="sxs-lookup"><span data-stu-id="30ff4-154">Adhere to icon design guidelines</span></span>

<span data-ttu-id="30ff4-155">Иконки являются одним из основных элементов, которые пользователи видят при просмотре магазина.</span><span class="sxs-lookup"><span data-stu-id="30ff4-155">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="30ff4-156">Значки должны сообщать о бренде и цели приложения, а также соблюдать Teams требованиям.</span><span class="sxs-lookup"><span data-stu-id="30ff4-156">Your icons should communicate your app's brand and purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="30ff4-157">Для получения дополнительной информации [см Teams.](~/concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="30ff4-157">For more information, see [guidance on creating Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

### <a name="capture-screenshots"></a><span data-ttu-id="30ff4-158">Захват скриншотов</span><span class="sxs-lookup"><span data-stu-id="30ff4-158">Capture screenshots</span></span>

<span data-ttu-id="30ff4-159">Скриншоты обеспечивают видный визуальный просмотр вашего приложения в дополнение к имени, значку и описаниям приложения.</span><span class="sxs-lookup"><span data-stu-id="30ff4-159">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="Пример скриншот подчеркивает, где приложение скриншоты отображения в магазине листинг.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="30ff4-161">Помните следующее о скриншотах:</span><span class="sxs-lookup"><span data-stu-id="30ff4-161">Remember the following about screenshots:</span></span>

* <span data-ttu-id="30ff4-162">Вы можете иметь до пяти скриншотов на листинг.</span><span class="sxs-lookup"><span data-stu-id="30ff4-162">You can have up to five screenshots per listing.</span></span>
* <span data-ttu-id="30ff4-163">Поддерживаемые типы файлов включают PNG, JPEG и GIF.</span><span class="sxs-lookup"><span data-stu-id="30ff4-163">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="30ff4-164">Размеры должны быть 1366x768 пикселей.</span><span class="sxs-lookup"><span data-stu-id="30ff4-164">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="30ff4-165">Максимальный размер 1024 КБ.</span><span class="sxs-lookup"><span data-stu-id="30ff4-165">Maximum size of 1,024 KB.</span></span>

<span data-ttu-id="30ff4-166">Для наилучшей практики см.</span><span class="sxs-lookup"><span data-stu-id="30ff4-166">For best practices, see the following resources:</span></span>

* [<span data-ttu-id="30ff4-167">Teams правила проверки магазина</span><span class="sxs-lookup"><span data-stu-id="30ff4-167">Teams store validation guidelines</span></span>](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [<span data-ttu-id="30ff4-168">Создание эффективных изображений для магазинов приложений Майкрософт</span><span class="sxs-lookup"><span data-stu-id="30ff4-168">Craft effective images for Microsoft app stores</span></span>](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a><span data-ttu-id="30ff4-169">Создание видео</span><span class="sxs-lookup"><span data-stu-id="30ff4-169">Create a video</span></span>

<span data-ttu-id="30ff4-170">Видео в вашем объявлении может быть наиболее эффективным способом сообщить, почему люди должны использовать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="30ff4-170">A video in your listing can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="30ff4-171">Вы должны ответить на следующие вопросы в видео:</span><span class="sxs-lookup"><span data-stu-id="30ff4-171">You should address the following questions in a video:</span></span>

* <span data-ttu-id="30ff4-172">Кто ваше приложение для?</span><span class="sxs-lookup"><span data-stu-id="30ff4-172">Who is your app for?</span></span>
* <span data-ttu-id="30ff4-173">Какие проблемы может решить ваше приложение?</span><span class="sxs-lookup"><span data-stu-id="30ff4-173">What problems can your app solve?</span></span>
* <span data-ttu-id="30ff4-174">Как работает ваше приложение?</span><span class="sxs-lookup"><span data-stu-id="30ff4-174">How does your app work?</span></span>
* <span data-ttu-id="30ff4-175">Какие еще преимущества вы получаете от использования приложения?</span><span class="sxs-lookup"><span data-stu-id="30ff4-175">What other benefits do you get from using your app?</span></span>

#### <a name="best-practices-for-videos"></a><span data-ttu-id="30ff4-176">Лучшие практики для видео</span><span class="sxs-lookup"><span data-stu-id="30ff4-176">Best practices for videos</span></span>

* <span data-ttu-id="30ff4-177">Держите видео между 30-90 секунд.</span><span class="sxs-lookup"><span data-stu-id="30ff4-177">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="30ff4-178">Стремитесь к качеству.</span><span class="sxs-lookup"><span data-stu-id="30ff4-178">Aim for quality.</span></span> <span data-ttu-id="30ff4-179">В объявлении пользователи увидят ваше видео перед скриншотами.</span><span class="sxs-lookup"><span data-stu-id="30ff4-179">In a listing, users will see your video before screenshots.</span></span>

### <a name="select-a-category-for-your-app"></a><span data-ttu-id="30ff4-180">Выберите категорию для приложения</span><span class="sxs-lookup"><span data-stu-id="30ff4-180">Select a category for your app</span></span>

<span data-ttu-id="30ff4-181">Во время отправки предлагается классифицировать приложение.</span><span class="sxs-lookup"><span data-stu-id="30ff4-181">During submission, you're asked to categorize your app.</span></span> <span data-ttu-id="30ff4-182">Следующие таблицы карты Teams категории магазинов к категориям, перечисленным в [Партнер-центре](https://aka.ms/PartnerCenterHomePage).</span><span class="sxs-lookup"><span data-stu-id="30ff4-182">The following table maps Teams store categories to the categories listed in [Partner Center](https://aka.ms/PartnerCenterHomePage).</span></span>

| <span data-ttu-id="30ff4-183">Teams категории</span><span class="sxs-lookup"><span data-stu-id="30ff4-183">Teams categories</span></span>       | <span data-ttu-id="30ff4-184">Категории Партнерский центр</span><span class="sxs-lookup"><span data-stu-id="30ff4-184">Partner Center categories</span></span>  |
|:---------------------|:---------------|
| <span data-ttu-id="30ff4-185">Аналитика и BI</span><span class="sxs-lookup"><span data-stu-id="30ff4-185">Analytics and BI</span></span> | <span data-ttu-id="30ff4-186">Аналитика, визуализация данных и BI</span><span class="sxs-lookup"><span data-stu-id="30ff4-186">Analytics, Data Visualization and BI</span></span> |
| <span data-ttu-id="30ff4-187">Разработчик и ИТ</span><span class="sxs-lookup"><span data-stu-id="30ff4-187">Developer and IT</span></span> | <span data-ttu-id="30ff4-188">Инструменты разработчика, ИТ-администратор</span><span class="sxs-lookup"><span data-stu-id="30ff4-188">Developer Tools, IT Admin</span></span> |
| <span data-ttu-id="30ff4-189">Образование</span><span class="sxs-lookup"><span data-stu-id="30ff4-189">Education</span></span> | <span data-ttu-id="30ff4-190">Образование</span><span class="sxs-lookup"><span data-stu-id="30ff4-190">Education</span></span> |
| <span data-ttu-id="30ff4-191">Управление персоналом</span><span class="sxs-lookup"><span data-stu-id="30ff4-191">Human resources</span></span> | <span data-ttu-id="30ff4-192">Кадровые ресурсы и рекрутинг</span><span class="sxs-lookup"><span data-stu-id="30ff4-192">Human Resources and Recruiting</span></span> |
| <span data-ttu-id="30ff4-193">Эффективность</span><span class="sxs-lookup"><span data-stu-id="30ff4-193">Productivity</span></span> | <span data-ttu-id="30ff4-194">Управление контентом, файлы и документы, производительность, обучение и обучение, а также коммунальные услуги</span><span class="sxs-lookup"><span data-stu-id="30ff4-194">Content Management, Files and documents, Productivity, Training and Tutorials, and Utilities</span></span> |
| <span data-ttu-id="30ff4-195">Управление проектами</span><span class="sxs-lookup"><span data-stu-id="30ff4-195">Project management</span></span> | <span data-ttu-id="30ff4-196">Коммуникация, Project управление, рабочий процесс и управление бизнесом</span><span class="sxs-lookup"><span data-stu-id="30ff4-196">Communication, Project Management, Workflow, and Business Management</span></span> |
| <span data-ttu-id="30ff4-197">Продажи и поддержка</span><span class="sxs-lookup"><span data-stu-id="30ff4-197">Sales and support</span></span> | <span data-ttu-id="30ff4-198">Управление клиентами и контактами, поддержка клиентов, управление финансами, продажи и маркетинг</span><span class="sxs-lookup"><span data-stu-id="30ff4-198">Customer and Contact Management, Customer Support, Financial Management, Sales and Marketing</span></span> |
| <span data-ttu-id="30ff4-199">Социальные и веселые</span><span class="sxs-lookup"><span data-stu-id="30ff4-199">Social and fun</span></span> | <span data-ttu-id="30ff4-200">Изображения и видео галереи, образ жизни, новости и погода, социальные, путешествия и навигация</span><span class="sxs-lookup"><span data-stu-id="30ff4-200">Image and Video Galleries, Lifestyle, News and Weather, Social, Travel, and Navigation</span></span> |

### <a name="localize-your-store-listing"></a><span data-ttu-id="30ff4-201">Локализация списка магазинов</span><span class="sxs-lookup"><span data-stu-id="30ff4-201">Localize your store listing</span></span>

<span data-ttu-id="30ff4-202">Партнер центр поддерживает [локализованные списки магазинов.](/office/dev/store/prepare-localized-solutions)</span><span class="sxs-lookup"><span data-stu-id="30ff4-202">Partner Center supports [localized store listings](/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="30ff4-203">Для получения дополнительной информации [узнайте, как локализовать список Teams приложений.](../../../../concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="30ff4-203">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="complete-publisher-verification"></a><span data-ttu-id="30ff4-204">Полная Publisher безопасности</span><span class="sxs-lookup"><span data-stu-id="30ff4-204">Complete Publisher Verification</span></span>

<span data-ttu-id="30ff4-205">[Publisher проверка требуется](/azure/active-directory/develop/publisher-verification-overview) для Teams приложений, перечисленных в магазине.</span><span class="sxs-lookup"><span data-stu-id="30ff4-205">[Publisher Verification](/azure/active-directory/develop/publisher-verification-overview) is required for Teams apps listed in the store.</span></span> <span data-ttu-id="30ff4-206">Для получения дополнительной информации, [смотрите часто задаваемые](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions) [вопросы, как отметить ваше приложение, как издатель проверены,](/azure/active-directory/develop/mark-app-as-publisher-verified)и [устранение неполадок проверки издателя.](/azure/active-directory/develop/troubleshoot-publisher-verification)</span><span class="sxs-lookup"><span data-stu-id="30ff4-206">For more information, see [frequently asked questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [how to mark your app as publisher verified](/azure/active-directory/develop/mark-app-as-publisher-verified), and [troubleshoot publisher verification](/azure/active-directory/develop/troubleshoot-publisher-verification).</span></span>

## <a name="complete-publisher-attestation"></a><span data-ttu-id="30ff4-207">Полное Publisher засвидетельство</span><span class="sxs-lookup"><span data-stu-id="30ff4-207">Complete Publisher Attestation</span></span>

<span data-ttu-id="30ff4-208">[Publisher attestation также](/microsoft-365-app-certification/docs/attestation) требуется для Teams приложений, перечисленных в магазине.</span><span class="sxs-lookup"><span data-stu-id="30ff4-208">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation) is also required for Teams apps listed in the store.</span></span> <span data-ttu-id="30ff4-209">Этот процесс включает в себя самооценку безопасности приложения, обработки данных и соблюдения требований, которые могут помочь потенциальным клиентам принимать обоснованные решения об использовании вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="30ff4-209">The process includes completing a self-assessment of your app's security, data handling, and compliance practices that can help potential customers make informed decisions about using your app.</span></span>

> [!NOTE]
> <span data-ttu-id="30ff4-210">Если вы отправляете новое приложение, вы не можете официально завершить проверку Publisher до тех пор, пока ваше приложение не будет перечислено в Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="30ff4-210">If you're submitting a new app, you can't officially complete Publisher Attestation until your app is listed on the Teams store.</span></span> <span data-ttu-id="30ff4-211">Если вы обновляете перечисленное приложение, Publisher, прежде чем отправить последнюю версию приложения для проверки.</span><span class="sxs-lookup"><span data-stu-id="30ff4-211">If you're updating a listed app, complete Publisher Attestation before you submit the latest version of the app for validation.</span></span>

## <a name="next-step"></a><span data-ttu-id="30ff4-212">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="30ff4-212">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="30ff4-213">Отправка приложения</span><span class="sxs-lookup"><span data-stu-id="30ff4-213">Submit your app</span></span>](/office/dev/store/add-in-submission-guide)
