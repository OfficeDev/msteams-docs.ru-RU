---
title: Создание вкладки канала или группы
author: laujan
description: Руководство quickstart по созданию вкладки канала и группы с генератором Yeoman для Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: fedaf3ec639917110e16c666734fa3eedbcda18e
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179995"
---
# <a name="create-a-channel-or-group-tab"></a><span data-ttu-id="3f34b-103">Создание вкладки канала или группы</span><span class="sxs-lookup"><span data-stu-id="3f34b-103">Create a channel or group tab</span></span>

## <a name="create-a-custom-channel-or-group-tab"></a><span data-ttu-id="3f34b-104">Создание настраиваемой вкладки канала или группы</span><span class="sxs-lookup"><span data-stu-id="3f34b-104">Create a custom channel or group tab</span></span>

<span data-ttu-id="3f34b-105">Вы можете создать вкладку канала или группы с помощью Node.js и генератора Yeoman, ASP.NETCore или MVC ASP.NETCore.</span><span class="sxs-lookup"><span data-stu-id="3f34b-105">You can create a channel or group tab using Node.js and the Yeoman Generator, ASP.NETCore, or ASP.NETCore MVC.</span></span>

# <a name="nodejs"></a>[<span data-ttu-id="3f34b-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="3f34b-106">Node.js</span></span>](#tab/nodejs)

### <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator"></a><span data-ttu-id="3f34b-107">Создание настраиваемой вкладки канала и группы с Node.js и генератора Yeoman</span><span class="sxs-lookup"><span data-stu-id="3f34b-107">Create a custom channel and group tab using Node.js and the Yeoman Generator</span></span>

> [!NOTE]
> <span data-ttu-id="3f34b-108">В этой статье описаны действия, описанные в сборке первого Microsoft Teams приложения [Wiki,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) найденного в репозитории Microsoft OfficeDev GitHub.</span><span class="sxs-lookup"><span data-stu-id="3f34b-108">This article follows the steps outlined in the [build Your first Microsoft Teams app](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="3f34b-109">Вы можете создать настраиваемую вкладку канала или группы с [помощью Teams Yeoman.](https://github.com/OfficeDev/generator-teams/)</span><span class="sxs-lookup"><span data-stu-id="3f34b-109">You can create a custom channel or group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

### <a name="prerequisites-for-apps"></a><span data-ttu-id="3f34b-110">Необходимые условия для приложений</span><span class="sxs-lookup"><span data-stu-id="3f34b-110">Prerequisites for apps</span></span>

<span data-ttu-id="3f34b-111">Необходимо иметь представление о следующих предпосылках:</span><span class="sxs-lookup"><span data-stu-id="3f34b-111">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="3f34b-112">Необходимо иметь клиента Office 365 и команду с **включенной возможностью загрузки настраиваемых приложений.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-112">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="3f34b-113">Дополнительные сведения см. в [Office 365 клиента.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="3f34b-113">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="3f34b-114">Если у вас нет учетной записи Office 365, вы можете зарегистрироваться для бесплатной подписки через Office 365 разработчика.</span><span class="sxs-lookup"><span data-stu-id="3f34b-114">If you do not currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="3f34b-115">Подписка остается активной до тех пор, пока вы используете ее для текущей разработки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-115">The subscription remains active as long as you are using it for ongoing development.</span></span> <span data-ttu-id="3f34b-116">См. [добро пожаловать в программу Office 365 разработчика](/office/developer-program/microsoft-365-developer-program).</span><span class="sxs-lookup"><span data-stu-id="3f34b-116">See [welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="3f34b-117">Кроме того, для этого проекта необходимо установить следующее в среде разработки:</span><span class="sxs-lookup"><span data-stu-id="3f34b-117">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="3f34b-118">Любой редактор текста или IDE.</span><span class="sxs-lookup"><span data-stu-id="3f34b-118">Any text editor or IDE.</span></span> <span data-ttu-id="3f34b-119">Вы можете установить и [использовать Visual Studio Code](https://code.visualstudio.com/download) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="3f34b-119">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="3f34b-120">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="3f34b-120">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="3f34b-121">Используйте последнюю версию LTS.</span><span class="sxs-lookup"><span data-stu-id="3f34b-121">Use the latest LTS version.</span></span> <span data-ttu-id="3f34b-122">Узел диспетчер пакетов (npm) устанавливается в системе с установкой Node.js.</span><span class="sxs-lookup"><span data-stu-id="3f34b-122">The Node Package Manager (npm) installs in your system with the installation of Node.js.</span></span>

- <span data-ttu-id="3f34b-123">После успешной установки Node.js установите [пакеты Yeoman](https://yeoman.io/) и [gulp-cli,](https://www.npmjs.com/package/gulp-cli) введите следующее в командной подсказке:</span><span class="sxs-lookup"><span data-stu-id="3f34b-123">After you have successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by entering the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="3f34b-124">Установите генератор Microsoft Teams приложений, введите следующее в командной подсказке:</span><span class="sxs-lookup"><span data-stu-id="3f34b-124">Install the Microsoft Teams Apps generator by entering the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

### <a name="generate-your-project"></a><span data-ttu-id="3f34b-125">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="3f34b-125">Generate your project</span></span>

<span data-ttu-id="3f34b-126">**Создание проекта**</span><span class="sxs-lookup"><span data-stu-id="3f34b-126">**To generate your project**</span></span>

1. <span data-ttu-id="3f34b-127">В командной подсказке создайте новый каталог для проекта вкладки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-127">At a command prompt, create a new directory for your tab project.</span></span>

1. <span data-ttu-id="3f34b-128">Чтобы запустить генератор, перейдите в новый каталог и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3f34b-128">To start the generator, go to your new directory and type the following command:</span></span>

    ```bash
    yo teams
    ```

1. <span data-ttu-id="3f34b-129">Далее укайте ряд значений, используемых в файле **manifest.jsприложения:**</span><span class="sxs-lookup"><span data-stu-id="3f34b-129">Next, provide a series of values that are used in your application's **manifest.json** file:</span></span>

    ![Снимок экрана открытия генератора](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="3f34b-131">**Как называется ваше решение?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-131">**What is your solution name?**</span></span>

    <span data-ttu-id="3f34b-132">Это имя проекта.</span><span class="sxs-lookup"><span data-stu-id="3f34b-132">This is your project name.</span></span> <span data-ttu-id="3f34b-133">Вы можете принять предложенное имя, выбрав ключ **Enter.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-133">You can accept the suggested name by selecting the **Enter** key.</span></span>

    <span data-ttu-id="3f34b-134">**Где следует разместить файлы?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-134">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="3f34b-135">В настоящее время вы находитесь в каталоге проектов.</span><span class="sxs-lookup"><span data-stu-id="3f34b-135">You are currently in your project directory.</span></span> <span data-ttu-id="3f34b-136">Выберите **Ввод**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-136">Select **Enter**.</span></span>

    <span data-ttu-id="3f34b-137">**Название проекта Microsoft Teams приложения?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-137">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="3f34b-138">Это имя пакета приложений, которое будет использоваться в манифесте и описании приложения.</span><span class="sxs-lookup"><span data-stu-id="3f34b-138">This is your app package name and will be used in the app manifest and description.</span></span> <span data-ttu-id="3f34b-139">Введите название или выберите **Ввод,** чтобы принять имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3f34b-139">Enter a title or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="3f34b-140">**Ваше (компания) имя? (максимум 32 символа)**</span><span class="sxs-lookup"><span data-stu-id="3f34b-140">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="3f34b-141">Имя вашей компании будет использоваться в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="3f34b-141">Your company name will be used in the app manifest.</span></span> <span data-ttu-id="3f34b-142">Введите имя компании или выберите **Ввод,** чтобы принять имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3f34b-142">Enter a company name or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="3f34b-143">**Какую версию манифеста вы бы хотели использовать?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-143">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="3f34b-144">Выберите схему по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3f34b-144">Select the default schema.</span></span>

    <span data-ttu-id="3f34b-145">**Быстрый строительный лес? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="3f34b-145">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="3f34b-146">По умолчанию — да; введите **n,** чтобы ввести свой microsoft Partner Id.</span><span class="sxs-lookup"><span data-stu-id="3f34b-146">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="3f34b-147">**Введите свой microsoft Partner Id, если он у вас есть? (Оставьте пустым, чтобы пропустить)**</span><span class="sxs-lookup"><span data-stu-id="3f34b-147">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="3f34b-148">Это поле не требуется и должно использоваться только в том случае, если вы уже входите в [партнерской сети Майкрософт.](https://partner.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="3f34b-148">This field is not required and should only be used if you are already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="3f34b-149">**Что нужно добавить в проект?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-149">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="3f34b-150">Выберите **&ast; () Вкладка**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-150">Select **( &ast; ) A Tab**.</span></span>

    <span data-ttu-id="3f34b-151">**URL-адрес, на котором будет организовано это решение?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-151">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="3f34b-152">По умолчанию генератор предлагает URL-адрес веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="3f34b-152">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="3f34b-153">Вы тестируете приложение только локально, поэтому допустимый URL-адрес не требуется.</span><span class="sxs-lookup"><span data-stu-id="3f34b-153">You are only testing your app locally, therefore, a valid URL is not necessary.</span></span>

    <span data-ttu-id="3f34b-154">**Хотите показать индикатор загрузки при загрузке приложения и вкладки?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-154">**Would you like show a loading indicator when your app/tab loads?**</span></span>

    <span data-ttu-id="3f34b-155">Выберите **не** включать индикатор загрузки при загрузке приложения или вкладки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-155">Choose **not** to include a loading indicator when your app or tab loads.</span></span> <span data-ttu-id="3f34b-156">По умолчанию нет, введите **n**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-156">The default is no, enter **n**.</span></span>

   <span data-ttu-id="3f34b-157">**Вы хотите, чтобы личные приложения отображались без строки заголовков вкладок?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-157">**Would you like personal apps to be rendered without a tab header-bar?**</span></span>

    <span data-ttu-id="3f34b-158">Не **следует** включать личные приложения, которые будут отрисовки без заглавной панели вкладок.</span><span class="sxs-lookup"><span data-stu-id="3f34b-158">Choose **not** to include personal apps to be rendered without a tab header-bar.</span></span> <span data-ttu-id="3f34b-159">По умолчанию нет, введите **n**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-159">Default is no, enter **n**.</span></span>

    <span data-ttu-id="3f34b-160">**Хотите включить тестовые рамки и начальные тесты? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="3f34b-160">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="3f34b-161">Выберите **не** включать тестовую базу для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="3f34b-161">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="3f34b-162">По умолчанию — да; введите **n**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-162">The default is yes; enter **n**.</span></span>

    <span data-ttu-id="3f34b-163">**Хотите использовать приложения Azure Аналитика для телеметрии? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="3f34b-163">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="3f34b-164">Не **включать** приложения [Azure Аналитика.](/azure/azure-monitor/app/app-insights-overview)</span><span class="sxs-lookup"><span data-stu-id="3f34b-164">Choose **not** to include [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview).</span></span> <span data-ttu-id="3f34b-165">По умолчанию нет; введите **n**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-165">The default is no; enter **n**.</span></span>

    <span data-ttu-id="3f34b-166">**Имя вкладки по умолчанию (максимум 16 символов)?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-166">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="3f34b-167">Назови свою вкладку. Это имя вкладки будет использоваться во всем проекте в качестве компонента пути к файлу или URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="3f34b-167">Name your tab. This tab name will be used throughout your project as a file or URL path component.</span></span>

    <span data-ttu-id="3f34b-168">**Какую вкладку вы хотели бы создать?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-168">**What kind of Tab would you like to create?**</span></span>

    <span data-ttu-id="3f34b-169">Используйте клавиши со стрелками, чтобы выбрать **вкладку Configurable.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-169">Use the arrow keys to select **Configurable** tab.</span></span>

    <span data-ttu-id="3f34b-170">**Какие области вы собираетесь использовать для вкладки?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-170">**What scopes do you intend to use for your Tab?**</span></span>

    <span data-ttu-id="3f34b-171">Вы можете выбрать группу или групповой чат.</span><span class="sxs-lookup"><span data-stu-id="3f34b-171">You can select a team or a group chat.</span></span>

    <span data-ttu-id="3f34b-172">**Требуется ли поддержка единого входа Azure AD для этой вкладки?**</span><span class="sxs-lookup"><span data-stu-id="3f34b-172">**Do you require Azure AD Single-Sign-On support for the tab?**</span></span>

    <span data-ttu-id="3f34b-173">Не  включай поддержку для вкладки Azure AD с одним входом. По умолчанию — да, введите **n**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-173">Choose **not** to include Azure AD Single-Sign-On support for the tab. The default is yes, enter **n**.</span></span>

    <span data-ttu-id="3f34b-174">**Хотите, чтобы эта вкладка была доступна в SharePoint Online? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="3f34b-174">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span>

    <span data-ttu-id="3f34b-175">Введите **n**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-175">Enter **n**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3f34b-176">Компонент пути **yourDefaultTabNameTab**— это значение, которое вы ввели в генератор имени вкладки по умолчанию **плюс** слово **Tab**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-176">The path component **yourDefaultTabNameTab**, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
    >
    > <span data-ttu-id="3f34b-177">Например: DefaultTabName: **MyTab**  >  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="3f34b-177">For example: DefaultTabName: **MyTab** > **/MyTabTab/**</span></span>

1. <span data-ttu-id="3f34b-178">В Visual Studio Code редакторе кода перейдите в каталог проекта и откройте следующий файл:</span><span class="sxs-lookup"><span data-stu-id="3f34b-178">In Visual Studio Code or any code editor, go to your project directory and open the following file:</span></span>

    ```bash
    ./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
    ```

1. <span data-ttu-id="3f34b-179">Найдите метод и добавьте следующий тег и содержимое в `render()` `<div>` верхнюю часть `<PanelBody>` кода контейнера:</span><span class="sxs-lookup"><span data-stu-id="3f34b-179">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

    ```html
        <PanelBody>
            <div style={styles.section}>
                Hello World! Yo Teams rocks!
            </div>
        </PanelBody>
    ```

1. <span data-ttu-id="3f34b-180">Обязательно сохраните обновленный файл.</span><span class="sxs-lookup"><span data-stu-id="3f34b-180">Make sure to save the updated file.</span></span>

### <a name="build-and-run-your-application"></a><span data-ttu-id="3f34b-181">Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="3f34b-181">Build and run your application</span></span>

<span data-ttu-id="3f34b-182">В командной подсказке откройте каталог проекта для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="3f34b-182">At a command prompt, open your project directory to complete the next tasks.</span></span>

#### <a name="create-the-app-package"></a><span data-ttu-id="3f34b-183">Создание пакета приложений</span><span class="sxs-lookup"><span data-stu-id="3f34b-183">Create the app package</span></span>

<span data-ttu-id="3f34b-184">Чтобы проверить вкладку в Teams, необходимо иметь пакет Teams.</span><span class="sxs-lookup"><span data-stu-id="3f34b-184">You must have an app package to test your tab in Teams.</span></span> <span data-ttu-id="3f34b-185">Это папка zip, которая содержит следующие необходимые файлы:</span><span class="sxs-lookup"><span data-stu-id="3f34b-185">It is a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="3f34b-186">Значок **полного цвета** размером 192 x 192 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3f34b-186">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="3f34b-187">Прозрачный **значок контура** размером 32 x 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3f34b-187">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="3f34b-188">Файл **manifest.js,** который указывает атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="3f34b-188">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="3f34b-189">Пакет создается с помощью задачи gulp, которая проверяет manifest.jsфайл и создает папку zip в **каталоге ./package.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-189">The package is created through a gulp task that validates the manifest.json file and generates the zip folder in the **./package directory**.</span></span> <span data-ttu-id="3f34b-190">В командной подсказке введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3f34b-190">In the command prompt, enter the following command:</span></span>

```bash
gulp manifest
```

#### <a name="build-your-application"></a><span data-ttu-id="3f34b-191">Сборка приложения</span><span class="sxs-lookup"><span data-stu-id="3f34b-191">Build your application</span></span>

<span data-ttu-id="3f34b-192">Команда сборки перекладывания решения в **папку ./dist.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-192">The build command transpiles your solution into the **./dist** folder.</span></span> <span data-ttu-id="3f34b-193">Введите следующую команду в командной подсказке:</span><span class="sxs-lookup"><span data-stu-id="3f34b-193">Enter the following command in the command prompt:</span></span>

```bash
gulp build
```

#### <a name="run-your-application-in-localhost"></a><span data-ttu-id="3f34b-194">Запустите приложение в localhost</span><span class="sxs-lookup"><span data-stu-id="3f34b-194">Run your application in localhost</span></span>

1. <span data-ttu-id="3f34b-195">Запустите локальный веб-сервер, введя в командную подсказку следующее:</span><span class="sxs-lookup"><span data-stu-id="3f34b-195">Start a local web server by entering the following in the command prompt:</span></span>

    ```bash
    gulp serve
    ```

1. <span data-ttu-id="3f34b-196">Введите в браузере, замените имя вкладки и просмотр домашней страницы приложения, как показано на `http://localhost:3007/<yourDefaultAppNameTab>/` **<yourDefaultAppNameTab>** следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="3f34b-196">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser, replace **<yourDefaultAppNameTab>** with your tab name, and view your application's home page as shown in the following image:</span></span>

    ![Снимок экрана домашней страницы](~/assets/images/tab-images/homePage.png)

1. <span data-ttu-id="3f34b-198">Чтобы просмотреть страницу конфигурации вкладок, перейдите к `https://localhost:3007/<yourDefaultAppNameTab>/config.html` .</span><span class="sxs-lookup"><span data-stu-id="3f34b-198">To view your tab configuration page, go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="3f34b-199">Ниже показано:</span><span class="sxs-lookup"><span data-stu-id="3f34b-199">The following is shown:</span></span>

    ![Скриншот страницы конфигурации](~/assets/images/tab-images/configurationPage.png)

### <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="3f34b-201">Создание безопасного туннеля на вкладке</span><span class="sxs-lookup"><span data-stu-id="3f34b-201">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="3f34b-202">Microsoft Teams является облачным продуктом и требует, чтобы содержимое вкладки было доступно в облаке с помощью конечных точек HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3f34b-202">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="3f34b-203">Teams не разрешает локальный хостинг.</span><span class="sxs-lookup"><span data-stu-id="3f34b-203">Teams does not allow local hosting.</span></span> <span data-ttu-id="3f34b-204">Необходимо либо опубликовать вкладку на общедоступный URL-адрес, либо использовать прокси-сервер, который предоставляет локальный порт URL-адресу, относящаяся к Интернету.</span><span class="sxs-lookup"><span data-stu-id="3f34b-204">You must either publish your tab to a public URL or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="3f34b-205">Чтобы проверить расширение вкладки, используйте [ngrok,](https://ngrok.com/docs)встроенный в это приложение.</span><span class="sxs-lookup"><span data-stu-id="3f34b-205">To test your tab extension, use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="3f34b-206">Ngrok — это средство обратного прокси-программного обеспечения, которое создает туннель к общедоступным конечным точкам HTTPS локального веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="3f34b-206">Ngrok is a reverse proxy software tool that creates a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="3f34b-207">Веб-точки сервера доступны во время текущего сеанса на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3f34b-207">Your server's web endpoints are available during the current session on your computer.</span></span> <span data-ttu-id="3f34b-208">Когда компьютер выключен или заснул, служба перестает быть доступной.</span><span class="sxs-lookup"><span data-stu-id="3f34b-208">When the computer is shut down or goes to sleep the service is no longer available.</span></span>

<span data-ttu-id="3f34b-209">В командной подсказке выйдите из localhost и введите следующее:</span><span class="sxs-lookup"><span data-stu-id="3f34b-209">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="3f34b-210">После того как вкладка была загружена в Microsoft Teams и успешно сохранена, ее можно просмотреть в галерее вкладок, добавить ее в планку вкладок и взаимодействовать с ней до окончания сеанса туннеля ngrok.</span><span class="sxs-lookup"><span data-stu-id="3f34b-210">After your tab has been uploaded to Microsoft Teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="3f34b-211">Если вы перезапустите сеанс ngrok, необходимо обновить приложение с помощью нового URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="3f34b-211">If you restart your ngrok session, you must update your app with the new URL.</span></span>

### <a name="upload-your-application-to-teams"></a><span data-ttu-id="3f34b-212">Upload приложение для Teams</span><span class="sxs-lookup"><span data-stu-id="3f34b-212">Upload your application to Teams</span></span>

<span data-ttu-id="3f34b-213">**Отправка приложения в Teams**</span><span class="sxs-lookup"><span data-stu-id="3f34b-213">**To upload your application to Teams**</span></span>

1. <span data-ttu-id="3f34b-214">Перейдите Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3f34b-214">Go to Microsoft Teams.</span></span> <span data-ttu-id="3f34b-215">Если вы используете [веб-версию,](https://teams.microsoft.com) вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="3f34b-215">If you use the [web-based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
1. <span data-ttu-id="3f34b-216">На левой стороне группы выберите эллипсы &#x25CF;&#x25CF;&#x25CF; рядом с командой, которую вы используете для тестирования вкладки, и выберите **команду Manage.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-216">From your teams on the left pane, select the ellipses &#x25CF;&#x25CF;&#x25CF; next to the team that you are using to test your tab and choose **Manage team**.</span></span>
1. <span data-ttu-id="3f34b-217">В главной области  выберите Приложения из панели **вкладок** и Upload настраиваемого приложения, расположенного в нижнем правом углу страницы.</span><span class="sxs-lookup"><span data-stu-id="3f34b-217">In the main pane, select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right corner of the page.</span></span>
1. <span data-ttu-id="3f34b-218">Перейдите в каталог проекта, просмотрите **папку ./package,** выберите папку почтовый индекс пакета приложений и **откройте**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-218">Go your project directory, browse to the **./package** folder, select the app package zip folder, and choose **Open**.</span></span>

    ![Добавлена вкладка Канала](../../assets/images/tab-images/channeltabadded.png)

1. <span data-ttu-id="3f34b-220">Выберите **Добавить** в диалоговом окне всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="3f34b-220">Select **Add** in the pop-up dialog box.</span></span> <span data-ttu-id="3f34b-221">Вкладка загружается в Teams.</span><span class="sxs-lookup"><span data-stu-id="3f34b-221">Your tab uploads into Teams.</span></span>
1. <span data-ttu-id="3f34b-222">Вернись в свою команду, выберите канал, в котором нужно отобразить вкладку, выберите ➕ из панели вкладок и выберите вкладку из галереи.</span><span class="sxs-lookup"><span data-stu-id="3f34b-222">Return to your team, choose the channel where you want to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
1. <span data-ttu-id="3f34b-223">Следуйте указаниям для добавления вкладки. Существует настраиваемый диалоговое окно конфигурации для канала или вкладки группы.</span><span class="sxs-lookup"><span data-stu-id="3f34b-223">Follow the directions for adding a tab. There is a custom configuration dialog box for your channel or group tab.</span></span>
1. <span data-ttu-id="3f34b-224">Выберите **Сохранить** и вкладка добавляется в вкладку канала.</span><span class="sxs-lookup"><span data-stu-id="3f34b-224">Select **Save** and your tab is added to the channel's tab bar.</span></span>

    ![Загруженная вкладка канала](../../assets/images/tab-images/channeltabuploaded.png)

# <a name="aspnet-core"></a>[<span data-ttu-id="3f34b-226">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="3f34b-226">ASP.NET Core</span></span>](#tab/aspnetcore)

### <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a><span data-ttu-id="3f34b-227">Создание настраиваемой вкладки канала или группы с помощью ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="3f34b-227">Create a custom channel or group tab with ASP.NET Core</span></span>

<span data-ttu-id="3f34b-228">Вы можете создать настраиваемую вкладку канала или группы с помощью C# и ASP.Net страницы Core Razor.</span><span class="sxs-lookup"><span data-stu-id="3f34b-228">You can create a custom channel or group tab using C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="3f34b-229">[App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) также используется для окончательного развертывания манифеста приложения и развертывания вкладки Teams.</span><span class="sxs-lookup"><span data-stu-id="3f34b-229">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-teams-apps"></a><span data-ttu-id="3f34b-230">Необходимые условия для Teams приложений</span><span class="sxs-lookup"><span data-stu-id="3f34b-230">Prerequisites for Teams apps</span></span>

<span data-ttu-id="3f34b-231">Необходимо иметь представление о следующих предпосылках:</span><span class="sxs-lookup"><span data-stu-id="3f34b-231">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="3f34b-232">Необходимо иметь клиента Office 365 и команду с **включенной возможностью загрузки настраиваемых приложений.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-232">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="3f34b-233">Дополнительные сведения см. в [Office 365 клиента.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="3f34b-233">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="3f34b-234">Если у вас в настоящее время нет Microsoft 365 учетной записи, вы можете зарегистрироваться на бесплатную подписку через [Программу разработчиков Майкрософт.](https://developer.microsoft.com/en-us/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="3f34b-234">If you do not currently have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="3f34b-235">Подписка остается активной до тех пор, пока вы используете ее для текущей разработки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-235">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="3f34b-236">Используйте App Studio для импорта приложения для Teams.</span><span class="sxs-lookup"><span data-stu-id="3f34b-236">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="3f34b-237">Чтобы установить App Studio, выберите **App Store** App в ![ нижнем левом углу приложения Teams и выберите ](~/assets/images/tab-images/storeApp.png) **App Studio.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-237">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="3f34b-238">После того как вы найдете плитку, выберите ее и выберите **Добавить** в всплывающее диалоговое окно, чтобы установить его.</span><span class="sxs-lookup"><span data-stu-id="3f34b-238">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="3f34b-239">Кроме того, для этого проекта необходимо установить следующее в среде разработки:</span><span class="sxs-lookup"><span data-stu-id="3f34b-239">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="3f34b-240">Текущая версия Visual Studio IDE с установленной рабочей нагрузкой на межплатформу **.NET CORE.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-240">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="3f34b-241">Если у вас еще нет Visual Studio, вы можете [](https://visualstudio.microsoft.com/downloads) скачать и установить последнюю версию Microsoft Visual Studio Community бесплатно.</span><span class="sxs-lookup"><span data-stu-id="3f34b-241">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="3f34b-242">Средство [обратного прокси ngrok.](https://ngrok.com)</span><span class="sxs-lookup"><span data-stu-id="3f34b-242">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="3f34b-243">Используйте ngrok для создания туннеля для локальных конечных точек HTTPS на локальном веб-сервере, доступных для общего пользования.</span><span class="sxs-lookup"><span data-stu-id="3f34b-243">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="3f34b-244">Вы можете [скачать ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="3f34b-244">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="3f34b-245">Получить исходный код</span><span class="sxs-lookup"><span data-stu-id="3f34b-245">Get the source code</span></span>

<span data-ttu-id="3f34b-246">В командной подсказке создайте новый каталог для проекта вкладки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-246">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="3f34b-247">Для начала работы предоставляется простой проект.</span><span class="sxs-lookup"><span data-stu-id="3f34b-247">A simple project is provided to get you started.</span></span> <span data-ttu-id="3f34b-248">Клонировать репозиторий образца в новый каталог с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="3f34b-248">Clone the sample repository into your new directory using the following command:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="3f34b-249">Кроме того, вы можете получить исходный код, скачав папку zip и извлекая файлы.</span><span class="sxs-lookup"><span data-stu-id="3f34b-249">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="3f34b-250">**Создание и запуск проекта вкладки**</span><span class="sxs-lookup"><span data-stu-id="3f34b-250">**To build and run the tab project**</span></span>

1. <span data-ttu-id="3f34b-251">После того как у вас есть исходный код, перейдите Visual Studio и выберите **Открыть проект или решение**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-251">After you have the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="3f34b-252">Перейдите к каталогу приложений вкладок и откройте **ChannelGroupTab.sln**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-252">Go to the tab application directory and open **ChannelGroupTab.sln**.</span></span>
1. <span data-ttu-id="3f34b-253">Чтобы создать и запустить приложение, нажмите **кнопку F5** или выберите **начало** отладки из **меню отладки.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-253">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="3f34b-254">В браузере перейдите к следующим URL-адресам и убедитесь, что приложение загружено правильно:</span><span class="sxs-lookup"><span data-stu-id="3f34b-254">In a browser, go to the following URLs and verify the application loaded properly:</span></span>

    - `http://localhost:44355`
    - `http://localhost:44355/privacy`
    - `http://localhost:44355/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="3f34b-255">Просмотр исходных кодов</span><span class="sxs-lookup"><span data-stu-id="3f34b-255">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="3f34b-256">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="3f34b-256">Startup.cs</span></span>

<span data-ttu-id="3f34b-257">Этот проект был создан из пустого шаблона ASP.NET Core 2.2 веб-приложения с расширенным — настройка для контрольного окна **HTTPS,** выбранного при установке.</span><span class="sxs-lookup"><span data-stu-id="3f34b-257">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="3f34b-258">Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3f34b-258">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="3f34b-259">Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому в метод добавляется среднее по статическим файлам с помощью `Configure()` следующего кода:</span><span class="sxs-lookup"><span data-stu-id="3f34b-259">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
  {
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

#### <a name="wwwroot-folder"></a><span data-ttu-id="3f34b-260">папка wwwroot</span><span class="sxs-lookup"><span data-stu-id="3f34b-260">wwwroot folder</span></span>

<span data-ttu-id="3f34b-261">В ASP.NET Core веб-корневой папке приложение ищет статические файлы.</span><span class="sxs-lookup"><span data-stu-id="3f34b-261">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="indexcshtml"></a><span data-ttu-id="3f34b-262">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="3f34b-262">Index.cshtml</span></span>

<span data-ttu-id="3f34b-263">ASP.NET Core обрабатывает файлы под названием **Index** в качестве домашней страницы по умолчанию для сайта.</span><span class="sxs-lookup"><span data-stu-id="3f34b-263">ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="3f34b-264">Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** отображается в качестве домашней страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="3f34b-264">When your browser URL points to the root of the site, **Index.cshtml** is displayed as the home page for your application.</span></span>

#### <a name="tabcs"></a><span data-ttu-id="3f34b-265">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="3f34b-265">Tab.cs</span></span>

<span data-ttu-id="3f34b-266">Этот C# содержит метод, который вызван из **Tab.cshtml во** время настройки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-266">This C# file contains a method that is called from **Tab.cshtml** during configuration.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="3f34b-267">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="3f34b-267">AppManifest folder</span></span>

<span data-ttu-id="3f34b-268">Эта папка содержит следующие необходимые файлы пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="3f34b-268">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="3f34b-269">Значок **полного цвета** размером 192 x 192 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3f34b-269">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="3f34b-270">Прозрачный **значок контура** размером 32 x 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3f34b-270">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="3f34b-271">Файл **manifest.js,** который указывает атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="3f34b-271">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="3f34b-272">Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="3f34b-272">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="3f34b-273">Когда пользователь выбирает добавить или обновить вкладку, Microsoft Teams загружает указанные в манифесте, встраив ее в IFrame и отрисовывает ее на `configurationUrl` вкладке.</span><span class="sxs-lookup"><span data-stu-id="3f34b-273">When a user chooses to add or update your tab, Microsoft Teams loads the `configurationUrl` specified in your manifest, embeds it in an IFrame, and renders it in your tab.</span></span>

#### <a name="csproj"></a><span data-ttu-id="3f34b-274">.csproj</span><span class="sxs-lookup"><span data-stu-id="3f34b-274">.csproj</span></span>

<span data-ttu-id="3f34b-275">В окне Visual Studio обозревателя решений щелкните правой кнопкой мыши по проекту и выберите **Изменить Project Файл**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-275">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="3f34b-276">В конце файла вы увидите следующий код, который создает и обновляет папку zip при создании приложения:</span><span class="sxs-lookup"><span data-stu-id="3f34b-276">At the end of the file, you see the following code that creates and updates your zip folder when the application builds:</span></span>

```xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

### <a name="establish-a-secure-tunnel-to-your-tab-for-teams"></a><span data-ttu-id="3f34b-277">Создание безопасного туннеля на вкладке для Teams</span><span class="sxs-lookup"><span data-stu-id="3f34b-277">Establish a secure tunnel to your tab for Teams</span></span>

<span data-ttu-id="3f34b-278">Microsoft Teams является облачным продуктом и требует, чтобы содержимое вкладки было доступно в облаке с помощью конечных точек HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3f34b-278">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="3f34b-279">Teams не разрешает локальный хостинг.</span><span class="sxs-lookup"><span data-stu-id="3f34b-279">Teams does not allow local hosting.</span></span> <span data-ttu-id="3f34b-280">Необходимо либо опубликовать вкладку на общедоступный URL-адрес, либо использовать прокси-сервер, который предоставляет локальный порт URL-адресу, относящаяся к Интернету.</span><span class="sxs-lookup"><span data-stu-id="3f34b-280">You must either publish your tab to a public URL, or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="3f34b-281">Чтобы проверить вкладку, используйте [ngrok](https://ngrok.com/docs).</span><span class="sxs-lookup"><span data-stu-id="3f34b-281">To test your tab, use [ngrok](https://ngrok.com/docs).</span></span> <span data-ttu-id="3f34b-282">Веб-точки сервера доступны во время запуска ngrok на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3f34b-282">Your server's web endpoints are available while ngrok is running on your computer.</span></span> <span data-ttu-id="3f34b-283">В бесплатной версии ngrok при закрытии ngrok URL-адреса отличаются при следующем запуске.</span><span class="sxs-lookup"><span data-stu-id="3f34b-283">In the free version of ngrok, if you close ngrok, the URLs are different the next time you start it.</span></span>

- <span data-ttu-id="3f34b-284">По командной подсказке в корневом каталоге проекта запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3f34b-284">At a command prompt in the root of your project directory, run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44355 -host-header="localhost:44355"
    ```

- <span data-ttu-id="3f34b-285">Ngrok прослушивает запросы из Интернета и передает их в приложение при работе в порту 44355.</span><span class="sxs-lookup"><span data-stu-id="3f34b-285">Ngrok listens to requests from the internet and routes them to your application when it is running on port 44355.</span></span> <span data-ttu-id="3f34b-286">Он должен `https://y8rCgT2b.ngrok.io/` напоминать, где **y8rCgT2b** заменяется url-адресом https ngrok alpha-numeric HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3f34b-286">It should resemble `https://y8rCgT2b.ngrok.io/` where **y8rCgT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="3f34b-287">Убедитесь, что командная подсказка будет запущена с помощью ngrok, и сделайте примечание URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="3f34b-287">Ensure that you keep the command prompt with ngrok running and make a note of the URL.</span></span>

### <a name="update-your-application"></a><span data-ttu-id="3f34b-288">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="3f34b-288">Update your application</span></span>

<span data-ttu-id="3f34b-289">В **Tab.cshtml** приложение представляет пользователю две кнопки параметра для отображения вкладки с красным или серым значком.</span><span class="sxs-lookup"><span data-stu-id="3f34b-289">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="3f34b-290">Выбор триггеров **выберите серый** или **выберите** красный или, соответственно, наборы и включает кнопку `saveGray()` Сохранить на странице `saveRed()` `settings.setValidityState(true)`  конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3f34b-290">Choosing the **Select Gray** or **Select Red** button triggers `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="3f34b-291">Этот код позволяет Teams, что вы выполнили требования к конфигурации и установка может продолжиться.</span><span class="sxs-lookup"><span data-stu-id="3f34b-291">This code lets Teams know that you have completed the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="3f34b-292">Параметры `settings.setSettings` заданы.</span><span class="sxs-lookup"><span data-stu-id="3f34b-292">The parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="3f34b-293">Наконец, `saveEvent.notifySuccess()` называется, чтобы указать, что URL-адрес контента успешно решен.</span><span class="sxs-lookup"><span data-stu-id="3f34b-293">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has been successfully resolved.</span></span>

#### <a name="_layoutcshtml"></a><span data-ttu-id="3f34b-294">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="3f34b-294">_Layout.cshtml</span></span>

<span data-ttu-id="3f34b-295">Чтобы вкладка отображалась в Teams, необходимо включить Microsoft Teams **клиента JavaScript** и включить вызов после загрузки `microsoftTeams.initialize()` страницы.</span><span class="sxs-lookup"><span data-stu-id="3f34b-295">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="3f34b-296">Это то, как ваша вкладка и Teams клиент:</span><span class="sxs-lookup"><span data-stu-id="3f34b-296">This is how your tab and the Teams client communicate:</span></span>

<span data-ttu-id="3f34b-297">Перейдите в **общую** папку, **откройте _Layout.cshtml** и добавьте в тег `<head>` следующее:</span><span class="sxs-lookup"><span data-stu-id="3f34b-297">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

> [!IMPORTANT]
> <span data-ttu-id="3f34b-298">Не копируйте и не вделайте URL-адреса на этой странице, так как они `<script src="...">` не представляют последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="3f34b-298">Do not copy and paste the `<script src="...">` URLs from this page, as they do not represent the latest version.</span></span> <span data-ttu-id="3f34b-299">Чтобы получить последнюю версию SDK, всегда Microsoft Teams [API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).</span><span class="sxs-lookup"><span data-stu-id="3f34b-299">To get the latest version of the SDK, always go to [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

#### <a name="tabcshtml"></a><span data-ttu-id="3f34b-300">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="3f34b-300">Tab.cshtml</span></span>

<span data-ttu-id="3f34b-301">**Обновление Tab.cshtml**</span><span class="sxs-lookup"><span data-stu-id="3f34b-301">**To update Tab.cshtml**</span></span>

1. <span data-ttu-id="3f34b-302">Откройте **вкладку cshtml** в Visual Studio и обновим встроенную `<script>` .</span><span class="sxs-lookup"><span data-stu-id="3f34b-302">Open **Tab.cshtml** in Visual Studio and update the embedded `<script>`.</span></span>

1. <span data-ttu-id="3f34b-303">В верхней части сценария позвоните `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="3f34b-303">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

1. <span data-ttu-id="3f34b-304">Обновление `websiteUrl` `contentUrl` значений и значений в каждой функции с ПОМОЩЬЮ URL-адреса https ngrok на вкладке.</span><span class="sxs-lookup"><span data-stu-id="3f34b-304">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

    <span data-ttu-id="3f34b-305">Теперь в коде должны быть указаны следующие **y8rCgT2b,** замененные URL-адресом ngrok:</span><span class="sxs-lookup"><span data-stu-id="3f34b-305">Your code should now include the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

    ```javascript
        microsoftTeams.initialize();

        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
        });
        }
    ```

1. <span data-ttu-id="3f34b-306">Сохраните обновленный **Tab.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-306">Save the updated **Tab.cshtml**.</span></span>

### <a name="build-and-run-your-application-for-teams"></a><span data-ttu-id="3f34b-307">Сборка и запуск приложения для Teams</span><span class="sxs-lookup"><span data-stu-id="3f34b-307">Build and run your application for Teams</span></span>

<span data-ttu-id="3f34b-308">**Создание и запуск приложения**</span><span class="sxs-lookup"><span data-stu-id="3f34b-308">**To build and run your application**</span></span>

1. <span data-ttu-id="3f34b-309">В Visual Studio нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-309">In Visual Studio, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="3f34b-310">Убедитесь, что **ngrok** работает и работает должным образом, открыв браузер и переехав на страницу контента через URL-адрес https ngrok, который был представлен в окне командной подсказки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-310">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="3f34b-311">Для выполнения действий, предусмотренных в этой статье, необходимо Visual Studio приложение в Visual Studio ngrok.</span><span class="sxs-lookup"><span data-stu-id="3f34b-311">You need to have both your application in Visual Studio and ngrok running to complete the steps provided in this article.</span></span> <span data-ttu-id="3f34b-312">Если для работы с приложением необходимо прекратить Visual Studio, продолжайте **работать с ngrok.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-312">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="3f34b-313">Он прослушивает и возобновляет маршрутизаку запроса приложения при его перезапуске в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3f34b-313">It listens and resumes routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="3f34b-314">Если вам нужно перезапустить службу ngrok, она возвращает новый URL-адрес, и вам необходимо обновить приложение с помощью нового URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="3f34b-314">If you have to restart the ngrok service it returns a new URL and you have to update your application with the new URL.</span></span>

### <a name="upload-your-tab-for-teams"></a><span data-ttu-id="3f34b-315">Upload вкладку для Teams</span><span class="sxs-lookup"><span data-stu-id="3f34b-315">Upload your tab for Teams</span></span>

> [!NOTE]
> <span data-ttu-id="3f34b-316">App Studio можно использовать для редактированияmanifest.js **файла** и отправки завершенного пакета в Teams.</span><span class="sxs-lookup"><span data-stu-id="3f34b-316">App Studio can be used to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="3f34b-317">Вы также можете вручную **изменитьmanifest.jsфайл.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-317">You can also manually edit the **manifest.json** file.</span></span> <span data-ttu-id="3f34b-318">Если это так, убедитесь, что вы создайте решение снова, чтобы создатьtab.zip **файл** для загрузки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-318">If you do, ensure that you build the solution again to create the **tab.zip** file to upload.</span></span>

<span data-ttu-id="3f34b-319">**Для загрузки вкладки в App Studio**</span><span class="sxs-lookup"><span data-stu-id="3f34b-319">**To upload your tab with App Studio**</span></span>

1. <span data-ttu-id="3f34b-320">Перейдите Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3f34b-320">Go to Microsoft Teams.</span></span> <span data-ttu-id="3f34b-321">Если вы используете [веб-версию,](https://teams.microsoft.com)вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="3f34b-321">If you use the [web-based version](https://teams.microsoft.com), you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="3f34b-322">Перейдите **в App Studio и** выберите **вкладку Редактор Манифеста.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-322">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="3f34b-323">Выберите **импорт существующего приложения в** **редакторе Манифеста,** чтобы приступить к обновлению пакета приложений для вкладки. Исходный код поставляется со своим частично полным манифестом.</span><span class="sxs-lookup"><span data-stu-id="3f34b-323">Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="3f34b-324">Имя вашего пакета приложений **tab.zip**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-324">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="3f34b-325">Он доступен по следующему пути:</span><span class="sxs-lookup"><span data-stu-id="3f34b-325">It is available from the following path:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="3f34b-326">Upload **tab.zip** App Studio.</span><span class="sxs-lookup"><span data-stu-id="3f34b-326">Upload **tab.zip** to App Studio.</span></span>

#### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="3f34b-327">Обновление пакета приложений с помощью редактора Manifest</span><span class="sxs-lookup"><span data-stu-id="3f34b-327">Update your app package with Manifest editor</span></span>

<span data-ttu-id="3f34b-328">После отправки пакета приложений в App Studio необходимо настроить его.</span><span class="sxs-lookup"><span data-stu-id="3f34b-328">After you have uploaded your app package into App Studio, you must configure it.</span></span>

<span data-ttu-id="3f34b-329">Выберите плитку для недавно импортируемой вкладки в правой панели приветствия редактора Манифеста.</span><span class="sxs-lookup"><span data-stu-id="3f34b-329">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="3f34b-330">Слева от редактора Манифеста имеется список действий, а справа — список свойств, которые должны иметь значения для каждого из этих действий.</span><span class="sxs-lookup"><span data-stu-id="3f34b-330">There is a list of steps on the left side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="3f34b-331">Большая часть сведений предоставлена вашими **manifest.js,** но есть поля, которые необходимо обновить.</span><span class="sxs-lookup"><span data-stu-id="3f34b-331">Much of the information has been provided by your **manifest.json** but there are fields that you must update.</span></span>

##### <a name="details-app-details"></a><span data-ttu-id="3f34b-332">Сведения: сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="3f34b-332">Details: App details</span></span>

<span data-ttu-id="3f34b-333">В разделе **Сведения о приложении:**</span><span class="sxs-lookup"><span data-stu-id="3f34b-333">In the **App details** section:</span></span>

1. <span data-ttu-id="3f34b-334">В **статье Идентификация** выберите **Создание** для замены удостоверения замещающего удостоверения на необходимый GUID для вкладки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-334">Under **Identification**, select **Generate** to replace the placeholder ID with the required GUID for your tab.</span></span>

1. <span data-ttu-id="3f34b-335">В **соответствии с сведениями разработчика** **обновите веб-сайт** **url-адресом https ngrok.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-335">Under **Developer information**, update **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="3f34b-336">В **URL-адресах** приложений обнови заявление **конфиденциальности** и условия использования `https://<yourngrokurl>/privacy` **для** `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="3f34b-336">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

##### <a name="capabilities-tabs"></a><span data-ttu-id="3f34b-337">Возможности: Вкладки</span><span class="sxs-lookup"><span data-stu-id="3f34b-337">Capabilities: Tabs</span></span>

<span data-ttu-id="3f34b-338">В разделе **Tabs:**</span><span class="sxs-lookup"><span data-stu-id="3f34b-338">In the **Tabs** section:</span></span>

1. <span data-ttu-id="3f34b-339">В **вкладке Team** выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-339">Under **Team tab**, select **Add**.</span></span>

1. <span data-ttu-id="3f34b-340">В **всплывающее** окно вкладки "Команда" обнови **URL-адрес конфигурации** `https://<yourngrokurl>/tab` до .</span><span class="sxs-lookup"><span data-stu-id="3f34b-340">In the **Team tab** pop-up window, update the **Configuration URL** to `https://<yourngrokurl>/tab`.</span></span>

1. <span data-ttu-id="3f34b-341">Убедитесь, что конфигурация может **обновляться?**, **Командные** и **групповые** почтовые ящики чата выбраны и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-341">Ensure the **Can update configuration?**, **Team**, and **Group chat** checkboxes are selected and select **Save**.</span></span>

##### <a name="finish-domains-and-permissions"></a><span data-ttu-id="3f34b-342">Finish: Домены и разрешения</span><span class="sxs-lookup"><span data-stu-id="3f34b-342">Finish: Domains and permissions</span></span>

<span data-ttu-id="3f34b-343">В разделе **Домены и**  разрешения домены с вкладок должны содержать URL-адрес ngrok без префикса `<yourngrokurl>.ngrok.io/` HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3f34b-343">In the **Domains and permissions** section, **Domains from your tabs** must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="3f34b-344">Finish: Test and distribute</span><span class="sxs-lookup"><span data-stu-id="3f34b-344">Finish: Test and distribute</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f34b-345">Справа в **описании** см. следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="3f34b-345">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="3f34b-346">&#9888; массив **"validDomains"** не может содержать сайт тоннелей... "</span><span class="sxs-lookup"><span data-stu-id="3f34b-346">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
> <span data-ttu-id="3f34b-347">Это предупреждение можно игнорировать при тестировании вкладки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-347">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="3f34b-348">В разделе **Тест и распространение** выберите **Установите**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-348">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="3f34b-349">В диалоговом окне всплывающее окно выберите **Добавить** в команду или из выпадающее окно, выберите **Добавить в чат**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-349">In the pop-up dialog box, select **Add to a team** or from the drop-down, select **Add to a chat**.</span></span>

1. <span data-ttu-id="3f34b-350">Выберите команду или чат, где нужно отобразить вкладку, и выберите **Настройка вкладки.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-350">Choose the team or chat where you want the tab to be displayed and select **Set up a tab**.</span></span>

1. <span data-ttu-id="3f34b-351">В следующем диалоговом окне всплывающее окно выберите **Выберите серый** или **выберите красный** цвет и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-351">In the next pop-up dialog box, choose either **Select Gray** or **Select Red**, and select **Save**.</span></span>

1. <span data-ttu-id="3f34b-352">Чтобы просмотреть вкладку, перейдите в команду или чат, где установлена вкладка, и выберите ее из панели вкладок.</span><span class="sxs-lookup"><span data-stu-id="3f34b-352">To view your tab, go to the team or chat where you installed the tab, and select it from the tab bar.</span></span> <span data-ttu-id="3f34b-353">Отображается страница, выбранная во время настройки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-353">The page that you chose during configuration is displayed.</span></span>

    ![Загружена вкладка канала ASPNET](../../assets/images/tab-images/channeltabaspnetuploaded.png)

# <a name="aspnet-core-mvc"></a>[<span data-ttu-id="3f34b-355">ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="3f34b-355">ASP.NET Core MVC</span></span>](#tab/aspnetcoremvc)

### <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="3f34b-356">Создание настраиваемой вкладки канала или группы с помощью ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="3f34b-356">Create a custom channel or group tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="3f34b-357">Вы можете создать настраиваемую вкладку канала или группы с C# ASP.Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="3f34b-357">You can create a custom channel or group tab using C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="3f34b-358">[App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) также используется для окончательного развертывания манифеста приложения и развертывания вкладки Teams.</span><span class="sxs-lookup"><span data-stu-id="3f34b-358">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-custom-channel-or-group-tab"></a><span data-ttu-id="3f34b-359">Необходимые условия для настраиваемой вкладки канала или группы</span><span class="sxs-lookup"><span data-stu-id="3f34b-359">Prerequisites for custom channel or group tab</span></span>

- <span data-ttu-id="3f34b-360">Необходимо иметь клиента Microsoft 365 и команду, настроенную с **включенной возможностью загрузки настраиваемых приложений.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-360">You must have a Microsoft 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="3f34b-361">Дополнительные сведения см. в [Office 365 клиента.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="3f34b-361">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="3f34b-362">Если у вас в настоящее время нет Microsoft 365 учетной записи, вы можете зарегистрироваться на бесплатную подписку через [Программу разработчиков Майкрософт.](https://developer.microsoft.com/en-us/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="3f34b-362">If you do not currently have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="3f34b-363">Подписка остается активной до тех пор, пока вы используете ее для текущей разработки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-363">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="3f34b-364">Используйте App Studio для импорта приложения для Teams.</span><span class="sxs-lookup"><span data-stu-id="3f34b-364">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="3f34b-365">Чтобы установить App Studio, выберите **App Store** App в ![ нижнем левом углу приложения Teams и выберите ](~/assets/images/tab-images/storeApp.png) **App Studio.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-365">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="3f34b-366">После того как вы найдете плитку, выберите ее и выберите **Добавить** в всплывающее диалоговое окно, чтобы установить его.</span><span class="sxs-lookup"><span data-stu-id="3f34b-366">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="3f34b-367">Кроме того, для этого проекта необходимо установить следующее в среде разработки:</span><span class="sxs-lookup"><span data-stu-id="3f34b-367">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="3f34b-368">Текущая версия Visual Studio IDE с установленной рабочей нагрузкой на межплатформу **.NET CORE.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-368">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="3f34b-369">Если у вас еще нет Visual Studio, вы можете [](https://visualstudio.microsoft.com/downloads) скачать и установить последнюю версию Microsoft Visual Studio Community бесплатно.</span><span class="sxs-lookup"><span data-stu-id="3f34b-369">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="3f34b-370">Средство [обратного прокси ngrok.](https://ngrok.com)</span><span class="sxs-lookup"><span data-stu-id="3f34b-370">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="3f34b-371">Используйте ngrok для создания туннеля для локальных конечных точек HTTPS на локальном веб-сервере, доступных для общего пользования.</span><span class="sxs-lookup"><span data-stu-id="3f34b-371">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="3f34b-372">Вы можете [скачать ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="3f34b-372">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="3f34b-373">Получить исходный код</span><span class="sxs-lookup"><span data-stu-id="3f34b-373">Get the source code</span></span>

<span data-ttu-id="3f34b-374">В командной подсказке создайте новый каталог для проекта вкладки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-374">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="3f34b-375">Для начала [работы](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) предоставляется простой проект Вкладки группы каналов.</span><span class="sxs-lookup"><span data-stu-id="3f34b-375">A simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) project is provided to get you started.</span></span> <span data-ttu-id="3f34b-376">Клонировать репозиторий образца в новый каталог с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="3f34b-376">Clone the sample repository into your new directory using the following command:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="3f34b-377">Кроме того, вы можете получить исходный код, скачав папку zip и извлекая файлы.</span><span class="sxs-lookup"><span data-stu-id="3f34b-377">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="3f34b-378">**Создание и запуск проекта вкладки**</span><span class="sxs-lookup"><span data-stu-id="3f34b-378">**To build and run the tab project**</span></span>

1. <span data-ttu-id="3f34b-379">После того как у вас есть исходный код, перейдите Visual Studio и выберите **Открыть проект или решение**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-379">After you have the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="3f34b-380">Перейдите к каталогу приложений вкладок и откройте **ChannelGroupTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-380">Go to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>
1. <span data-ttu-id="3f34b-381">Чтобы создать и запустить приложение, нажмите **кнопку F5** или выберите **начало** отладки из **меню отладки.**</span><span class="sxs-lookup"><span data-stu-id="3f34b-381">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="3f34b-382">В браузере перейдите к следующим URL-адресам и убедитесь, что приложение загружено правильно:</span><span class="sxs-lookup"><span data-stu-id="3f34b-382">In a browser, navigate to the following URLs and verify that the application loaded properly:</span></span>

    - `http://localhost:44360`
    - `http://localhost:44360/privacy`
    - `http://localhost:44360/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="3f34b-383">Просмотр исходных кодов</span><span class="sxs-lookup"><span data-stu-id="3f34b-383">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="3f34b-384">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="3f34b-384">Startup.cs</span></span>

<span data-ttu-id="3f34b-385">Этот проект был создан из пустого шаблона ASP.NET Core 2.2 веб-приложения с расширенным — настройка для контрольного окна **HTTPS,** выбранного при установке.</span><span class="sxs-lookup"><span data-stu-id="3f34b-385">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="3f34b-386">Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3f34b-386">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="3f34b-387">Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому в метод добавляется среднее по статическим файлам с помощью `Configure()` следующего кода:</span><span class="sxs-lookup"><span data-stu-id="3f34b-387">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
  {
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

#### <a name="wwwroot-folder"></a><span data-ttu-id="3f34b-388">папка wwwroot</span><span class="sxs-lookup"><span data-stu-id="3f34b-388">wwwroot folder</span></span>

<span data-ttu-id="3f34b-389">В ASP.NET Core веб-корневой папке приложение ищет статические файлы.</span><span class="sxs-lookup"><span data-stu-id="3f34b-389">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="3f34b-390">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="3f34b-390">AppManifest folder</span></span>

<span data-ttu-id="3f34b-391">Эта папка содержит следующие необходимые файлы пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="3f34b-391">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="3f34b-392">Значок **полного цвета** размером 192 x 192 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3f34b-392">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="3f34b-393">Прозрачный **значок контура** размером 32 x 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3f34b-393">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="3f34b-394">Файл **manifest.js,** который указывает атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="3f34b-394">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="3f34b-395">Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="3f34b-395">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

#### <a name="csproj"></a><span data-ttu-id="3f34b-396">.csproj</span><span class="sxs-lookup"><span data-stu-id="3f34b-396">.csproj</span></span>

<span data-ttu-id="3f34b-397">В окне Visual Studio обозревателя решений щелкните правой кнопкой мыши по проекту и выберите **Изменить Project Файл**.</span><span class="sxs-lookup"><span data-stu-id="3f34b-397">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="3f34b-398">В конце файла вы увидите следующий код, который создает и обновляет папку zip при создании приложения:</span><span class="sxs-lookup"><span data-stu-id="3f34b-398">At the end of the file you see the following code that creates and updates your zip folder when the application builds:</span></span>

```xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

#### <a name="models"></a><span data-ttu-id="3f34b-399">Модели</span><span class="sxs-lookup"><span data-stu-id="3f34b-399">Models</span></span>

<span data-ttu-id="3f34b-400">**ChannelGroup.cs представляет** объект Сообщения и методы, которые будут вызваны из контроллеров во время настройки.</span><span class="sxs-lookup"><span data-stu-id="3f34b-400">**ChannelGroup.cs** presents a Message object and methods that will be called from the controllers during configuration.</span></span>

#### <a name="views"></a><span data-ttu-id="3f34b-401">Представления</span><span class="sxs-lookup"><span data-stu-id="3f34b-401">Views</span></span>

<span data-ttu-id="3f34b-402">Это различные представления в ASP.NET Core MVC:</span><span class="sxs-lookup"><span data-stu-id="3f34b-402">These are the different views in ASP.NET Core MVC:</span></span>

* <span data-ttu-id="3f34b-403">Главная: ASP.NET Core обрабатывает файлы под названием **Index** в качестве домашней страницы по умолчанию для сайта.</span><span class="sxs-lookup"><span data-stu-id="3f34b-403">Home: ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="3f34b-404">Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** будет отображаться в качестве домашней страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="3f34b-404">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

* <span data-ttu-id="3f34b-405">Общий доступ. Частичная разметка **_Layout.cshtml** содержит общую структуру страниц приложения и общие визуальные элементы.</span><span class="sxs-lookup"><span data-stu-id="3f34b-405">Shared: The partial view markup **_Layout.cshtml** contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="3f34b-406">Он также будет ссылаться на Teams библиотеку.</span><span class="sxs-lookup"><span data-stu-id="3f34b-406">It will also reference the Teams Library.</span></span>

#### <a name="controllers"></a><span data-ttu-id="3f34b-407">Контроллеры</span><span class="sxs-lookup"><span data-stu-id="3f34b-407">Controllers</span></span>

<span data-ttu-id="3f34b-408">Контроллеры используют свойство для динамического переноса значений `ViewBag` в представления.</span><span class="sxs-lookup"><span data-stu-id="3f34b-408">The controllers use the `ViewBag` property to transfer values dynamically to the views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="3f34b-409">Откройте командную подсказку в корневом каталоге проекта и запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3f34b-409">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:443560 -host-header="localhost:44360"
    ```

* <span data-ttu-id="3f34b-410">Ngrok будет прослушивать запросы из Интернета и перенанастрает их в ваше приложение, когда оно запущено в порту 44355.</span><span class="sxs-lookup"><span data-stu-id="3f34b-410">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="3f34b-411">Он должен `https://y8rCgT2b.ngrok.io/` напоминать, где **y8rCgT2b** заменяется url-адресом https ngrok alpha-numeric HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3f34b-411">It should resemble `https://y8rCgT2b.ngrok.io/` where **y8rCgT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="3f34b-412">Убедитесь, что командная подсказка будет запущена с помощью ngrok, и сделайте примечание URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="3f34b-412">Ensure that you keep the command prompt with ngrok running and make a note of the URL.</span></span>

### <a name="update-your-application"></a><span data-ttu-id="3f34b-413">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="3f34b-413">Update your application</span></span>

<span data-ttu-id="3f34b-414">В **Tab.cshtml** приложение представляет пользователю две кнопки параметра для отображения вкладки с красным или серым значком.</span><span class="sxs-lookup"><span data-stu-id="3f34b-414">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="3f34b-415">Выбор кнопки **Выберите серый** или **выберите** красный, триггеры или, соответственно, задает и включает кнопку Сохранить `saveGray()` на странице `saveRed()` `settings.setValidityState(true)` конфигурации. </span><span class="sxs-lookup"><span data-stu-id="3f34b-415">Choosing the **Select Gray** or **Select Red** button, triggers `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="3f34b-416">Этот код позволяет Teams, что вы выполнили требования к конфигурации и установка может продолжиться.</span><span class="sxs-lookup"><span data-stu-id="3f34b-416">This code lets Teams know that you have completed the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="3f34b-417">При сохранения `settings.setSettings` заданы параметры.</span><span class="sxs-lookup"><span data-stu-id="3f34b-417">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="3f34b-418">Наконец, `saveEvent.notifySuccess()` называется, чтобы указать, что URL-адрес контента успешно решен.</span><span class="sxs-lookup"><span data-stu-id="3f34b-418">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has been successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

---

## <a name="see-also"></a><span data-ttu-id="3f34b-419">См. также</span><span class="sxs-lookup"><span data-stu-id="3f34b-419">See also</span></span>

* [<span data-ttu-id="3f34b-420">Teams вкладки</span><span class="sxs-lookup"><span data-stu-id="3f34b-420">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="3f34b-421">Создание личной вкладки</span><span class="sxs-lookup"><span data-stu-id="3f34b-421">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="3f34b-422">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="3f34b-422">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="3f34b-423">Создание вкладок с использованием адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="3f34b-423">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="next-step"></a><span data-ttu-id="3f34b-424">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="3f34b-424">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3f34b-425">Создать страницу контента</span><span class="sxs-lookup"><span data-stu-id="3f34b-425">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
