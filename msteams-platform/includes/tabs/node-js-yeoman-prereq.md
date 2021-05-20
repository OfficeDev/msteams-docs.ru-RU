## <a name="prerequisites"></a><span data-ttu-id="ad042-101">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ad042-101">Prerequisites</span></span>

- <span data-ttu-id="ad042-102">Для завершения этого быстрого начала вам понадобится Office 365 и команда, настроенная с *включенным приложением Allow uploading* custom.</span><span class="sxs-lookup"><span data-stu-id="ad042-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="ad042-103">Чтобы узнать больше, [см Office 365.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="ad042-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="ad042-104">Если в настоящее время у вас нет Office 365 учетной записи, вы можете подписаться на бесплатную подписку через программу Office 365 разработчика.</span><span class="sxs-lookup"><span data-stu-id="ad042-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="ad042-105">Подписка будет оставаться активной до тех пор, пока вы используете ее для постоянной разработки.</span><span class="sxs-lookup"><span data-stu-id="ad042-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="ad042-106">Смотрите [Добро пожаловать в Office 365 разработчика .](/office/developer-program/microsoft-365-developer-program)</span><span class="sxs-lookup"><span data-stu-id="ad042-106">See [Welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="ad042-107">Кроме того, этот проект требует, чтобы в среде разработки было установлено следующее:</span><span class="sxs-lookup"><span data-stu-id="ad042-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="ad042-108">Любой текстовый редактор или IDE.</span><span class="sxs-lookup"><span data-stu-id="ad042-108">Any text editor or IDE.</span></span> <span data-ttu-id="ad042-109">Вы можете установить и [использовать Visual Studio Code](https://code.visualstudio.com/download) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="ad042-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="ad042-110">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="ad042-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="ad042-111">Вы должны использовать последнюю версию LTS.</span><span class="sxs-lookup"><span data-stu-id="ad042-111">You should use the latest LTS version.</span></span> <span data-ttu-id="ad042-112">Узел диспетчер пакетов (npm) установится в вашу систему с установкой Node.js.</span><span class="sxs-lookup"><span data-stu-id="ad042-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="ad042-113">После успешной установки Node.js установите [пакеты Yeoman](https://yeoman.io/) [и gulp-cli,](https://www.npmjs.com/package/gulp-cli) введя следующее в подсказке команды:</span><span class="sxs-lookup"><span data-stu-id="ad042-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="ad042-114">Установите Microsoft Teams apps, введя следующее в подсказке команды:</span><span class="sxs-lookup"><span data-stu-id="ad042-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

## <a name="generate-your-project"></a><span data-ttu-id="ad042-115">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="ad042-115">Generate your project</span></span>

- <span data-ttu-id="ad042-116">Откройте командный запрос и создайте новый каталог для вашего проекта вкладок.</span><span class="sxs-lookup"><span data-stu-id="ad042-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="ad042-117">Чтобы начать работу генератора, перейдите на новый каталог и ввемите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ad042-117">To start the generator, navigate to your new directory and type the following command:</span></span>

    ```bash
    yo teams
    ```

- <span data-ttu-id="ad042-118">Далее вы предоставите ряд значений, которые будут использоваться в данных **приложенияmanifest.jsфайле:**</span><span class="sxs-lookup"><span data-stu-id="ad042-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

    ![генератор открытия скриншот](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="ad042-120">**Как называется ваше решение?**</span><span class="sxs-lookup"><span data-stu-id="ad042-120">**What is your solution name?**</span></span>

    <span data-ttu-id="ad042-121">Это название вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="ad042-121">This is your project name.</span></span> <span data-ttu-id="ad042-122">Вы можете принять предложенное имя, нажав на введите.</span><span class="sxs-lookup"><span data-stu-id="ad042-122">You can accept the suggested name by pressing enter.</span></span>

    <span data-ttu-id="ad042-123">**Где следует разместить файлы?**</span><span class="sxs-lookup"><span data-stu-id="ad042-123">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="ad042-124">В настоящее время вы находитесь в каталоге проектов.</span><span class="sxs-lookup"><span data-stu-id="ad042-124">You're currently in your project directory.</span></span> <span data-ttu-id="ad042-125">Нажмите войти.</span><span class="sxs-lookup"><span data-stu-id="ad042-125">Press enter.</span></span>

    <span data-ttu-id="ad042-126">**Название вашего Microsoft Teams приложения?**</span><span class="sxs-lookup"><span data-stu-id="ad042-126">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="ad042-127">Это имя пакета вашего приложения и будет использоваться в манифесте и описании приложения.</span><span class="sxs-lookup"><span data-stu-id="ad042-127">This is your app package name and will be used in the app manifest and description.</span></span>

    <span data-ttu-id="ad042-128">**Ваше (компания) имя? (максимум 32 символа)**</span><span class="sxs-lookup"><span data-stu-id="ad042-128">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="ad042-129">Название вашей компании будет использовано в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="ad042-129">Your company name will be used in the app manifest.</span></span>

    <span data-ttu-id="ad042-130">**Какую явную версию вы хотели бы использовать?**</span><span class="sxs-lookup"><span data-stu-id="ad042-130">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="ad042-131">Выберите схему по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ad042-131">Select the default schema.</span></span>

    <span data-ttu-id="ad042-132">**Быстрые строительные леса? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="ad042-132">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="ad042-133">По умолчанию да; **введите n** для введите идентификатор партнера Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ad042-133">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="ad042-134">**Введите идентификатор партнера Майкрософт, если он у вас есть? (Оставьте пустым, чтобы пропустить)**</span><span class="sxs-lookup"><span data-stu-id="ad042-134">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="ad042-135">Это поле не требуется и должно использоваться только в том случае, если вы уже входите в партнерской [сети Майкрософт.](https://partner.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="ad042-135">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="ad042-136">**Что вы хотите добавить в свой проект?**</span><span class="sxs-lookup"><span data-stu-id="ad042-136">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="ad042-137">Выберите &ast; () Вкладку.</span><span class="sxs-lookup"><span data-stu-id="ad042-137">Select ( &ast; ) A Tab.</span></span>

    <span data-ttu-id="ad042-138">**URL, где вы будете принимать это решение?**</span><span class="sxs-lookup"><span data-stu-id="ad042-138">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="ad042-139">По умолчанию генератор предлагает URL-адрес веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="ad042-139">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="ad042-140">Вы будете тестировать приложение только локально, поэтому для завершения этого быстрого начала не требуется действительный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="ad042-140">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

    <span data-ttu-id="ad042-141">**Хотите включить рамки тестирования и первоначальные тесты? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="ad042-141">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="ad042-142">Не **включать** тестовую основу для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="ad042-142">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="ad042-143">По умолчанию да; **введите n**.</span><span class="sxs-lookup"><span data-stu-id="ad042-143">The default is yes; enter **n**.</span></span>

    <span data-ttu-id="ad042-144">**Хотите использовать Azure Applications Insights для телеметрии? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="ad042-144">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="ad042-145">Не **включать** Azure [Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad042-145">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="ad042-146">По умолчанию нет; **введите n**.</span><span class="sxs-lookup"><span data-stu-id="ad042-146">The default is no; enter **n**.</span></span>

    <span data-ttu-id="ad042-147">**Имя вкладки по умолчанию (максимум 16 символов)?**</span><span class="sxs-lookup"><span data-stu-id="ad042-147">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="ad042-148">Назовите свою вкладку. Это название вкладки будет использоваться на протяжении всего проекта в качестве компонента пути файла/URL.</span><span class="sxs-lookup"><span data-stu-id="ad042-148">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
