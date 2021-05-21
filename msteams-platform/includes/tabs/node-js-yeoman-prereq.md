## <a name="prerequisites"></a><span data-ttu-id="096b0-101">Предварительные условия</span><span class="sxs-lookup"><span data-stu-id="096b0-101">Prerequisites</span></span>

- <span data-ttu-id="096b0-102">Для завершения этого quickstart вам потребуется Office 365 клиент и команда, настроенная с возможностью загрузки *настраиваемых приложений* включен.</span><span class="sxs-lookup"><span data-stu-id="096b0-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="096b0-103">Дополнительные дополнительные информации см. в [Office 365 клиента.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="096b0-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="096b0-104">Если у вас нет учетной записи Office 365, вы можете зарегистрироваться для бесплатной подписки через Office 365 разработчика.</span><span class="sxs-lookup"><span data-stu-id="096b0-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="096b0-105">Подписка будет оставаться активной до тех пор, пока вы используете ее для текущей разработки.</span><span class="sxs-lookup"><span data-stu-id="096b0-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="096b0-106">См. [в Office 365 программе разработчиков.](/office/developer-program/microsoft-365-developer-program)</span><span class="sxs-lookup"><span data-stu-id="096b0-106">See [Welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="096b0-107">Кроме того, для этого проекта необходимо установить следующее в среде разработки:</span><span class="sxs-lookup"><span data-stu-id="096b0-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="096b0-108">Любой редактор текста или IDE.</span><span class="sxs-lookup"><span data-stu-id="096b0-108">Any text editor or IDE.</span></span> <span data-ttu-id="096b0-109">Вы можете установить и [использовать Visual Studio Code](https://code.visualstudio.com/download) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="096b0-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="096b0-110">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="096b0-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="096b0-111">Следует использовать последнюю версию LTS.</span><span class="sxs-lookup"><span data-stu-id="096b0-111">You should use the latest LTS version.</span></span> <span data-ttu-id="096b0-112">Узел диспетчер пакетов (npm) будет устанавливаться в систему с установкой Node.js.</span><span class="sxs-lookup"><span data-stu-id="096b0-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="096b0-113">После успешной установки Node.js установите [пакеты Yeoman](https://yeoman.io/) и [gulp-cli,](https://www.npmjs.com/package/gulp-cli) введя в командную подсказку следующее:</span><span class="sxs-lookup"><span data-stu-id="096b0-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="096b0-114">Установите генератор Microsoft Teams приложений, введя в командную подсказку следующее:</span><span class="sxs-lookup"><span data-stu-id="096b0-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

## <a name="generate-your-project"></a><span data-ttu-id="096b0-115">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="096b0-115">Generate your project</span></span>

- <span data-ttu-id="096b0-116">Откройте командную подсказку и создайте новый каталог для проекта вкладки.</span><span class="sxs-lookup"><span data-stu-id="096b0-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="096b0-117">Чтобы запустить генератор, перейдите в новый каталог и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="096b0-117">To start the generator, navigate to your new directory and type the following command:</span></span>

    ```bash
    yo teams
    ```

- <span data-ttu-id="096b0-118">Далее вы предоставите ряд значений, которые будут использоваться в файле **manifest.jsприложения:**</span><span class="sxs-lookup"><span data-stu-id="096b0-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

    ![Снимок экрана открытия генератора](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="096b0-120">**Как называется ваше решение?**</span><span class="sxs-lookup"><span data-stu-id="096b0-120">**What is your solution name?**</span></span>

    <span data-ttu-id="096b0-121">Это имя проекта.</span><span class="sxs-lookup"><span data-stu-id="096b0-121">This is your project name.</span></span> <span data-ttu-id="096b0-122">Вы можете принять предложенное имя, нажав ввод.</span><span class="sxs-lookup"><span data-stu-id="096b0-122">You can accept the suggested name by pressing enter.</span></span>

    <span data-ttu-id="096b0-123">**Где следует разместить файлы?**</span><span class="sxs-lookup"><span data-stu-id="096b0-123">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="096b0-124">В настоящее время вы в каталоге проектов.</span><span class="sxs-lookup"><span data-stu-id="096b0-124">You're currently in your project directory.</span></span> <span data-ttu-id="096b0-125">Нажмите кнопку ввод.</span><span class="sxs-lookup"><span data-stu-id="096b0-125">Press enter.</span></span>

    <span data-ttu-id="096b0-126">**Название проекта Microsoft Teams приложения?**</span><span class="sxs-lookup"><span data-stu-id="096b0-126">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="096b0-127">Это имя пакета приложений, которое будет использоваться в манифесте и описании приложения.</span><span class="sxs-lookup"><span data-stu-id="096b0-127">This is your app package name and will be used in the app manifest and description.</span></span>

    <span data-ttu-id="096b0-128">**Ваше (компания) имя? (максимум 32 символа)**</span><span class="sxs-lookup"><span data-stu-id="096b0-128">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="096b0-129">Имя вашей компании будет использоваться в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="096b0-129">Your company name will be used in the app manifest.</span></span>

    <span data-ttu-id="096b0-130">**Какую версию манифеста вы бы хотели использовать?**</span><span class="sxs-lookup"><span data-stu-id="096b0-130">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="096b0-131">Выберите схему по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="096b0-131">Select the default schema.</span></span>

    <span data-ttu-id="096b0-132">**Быстрый строительный лес? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="096b0-132">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="096b0-133">По умолчанию — да; введите **n,** чтобы ввести свой microsoft Partner Id.</span><span class="sxs-lookup"><span data-stu-id="096b0-133">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="096b0-134">**Введите свой microsoft Partner Id, если он у вас есть? (Оставьте пустым, чтобы пропустить)**</span><span class="sxs-lookup"><span data-stu-id="096b0-134">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="096b0-135">Это поле не требуется и должно использоваться только в том случае, если вы уже входите в [сеть партнеров Майкрософт.](https://partner.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="096b0-135">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="096b0-136">**Что нужно добавить в проект?**</span><span class="sxs-lookup"><span data-stu-id="096b0-136">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="096b0-137">Выберите &ast; () Вкладка.</span><span class="sxs-lookup"><span data-stu-id="096b0-137">Select ( &ast; ) A Tab.</span></span>

    <span data-ttu-id="096b0-138">**URL-адрес, на котором будет организовано это решение?**</span><span class="sxs-lookup"><span data-stu-id="096b0-138">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="096b0-139">По умолчанию генератор предлагает URL-адрес веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="096b0-139">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="096b0-140">Вы будете тестировать приложение только локально, поэтому для выполнения этого quickstart допустимый URL-адрес не требуется.</span><span class="sxs-lookup"><span data-stu-id="096b0-140">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

    <span data-ttu-id="096b0-141">**Хотите включить тестовые рамки и начальные тесты? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="096b0-141">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="096b0-142">Выберите **не** включать тестовую базу для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="096b0-142">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="096b0-143">По умолчанию — да; введите **n**.</span><span class="sxs-lookup"><span data-stu-id="096b0-143">The default is yes; enter **n**.</span></span>

    <span data-ttu-id="096b0-144">**Хотите использовать для телеметрии сведения о приложениях Azure? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="096b0-144">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="096b0-145">Выберите **не включать** azure Application [Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="096b0-145">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="096b0-146">По умолчанию нет; введите **n**.</span><span class="sxs-lookup"><span data-stu-id="096b0-146">The default is no; enter **n**.</span></span>

    <span data-ttu-id="096b0-147">**Имя вкладки по умолчанию (максимум 16 символов)?**</span><span class="sxs-lookup"><span data-stu-id="096b0-147">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="096b0-148">Назови свою вкладку. Это имя вкладки будет использоваться во всем проекте в качестве компонента пути к файлу или URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="096b0-148">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
