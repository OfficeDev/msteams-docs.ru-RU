## <a name="prerequisites"></a><span data-ttu-id="868e3-101">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="868e3-101">Prerequisites</span></span>

- <span data-ttu-id="868e3-102">Для выполнения этого руководства вам потребуется клиент Office 365 и группа, настроенная с разрешенной *отправкой пользовательских приложений* .</span><span class="sxs-lookup"><span data-stu-id="868e3-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="868e3-103">Чтобы узнать больше, ознакомьтесь со статьей [Подготовка клиента Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="868e3-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="868e3-104">Если у вас в настоящее время нет учетной записи Office 365, вы можете получить бесплатную подписку в программе для разработчиков Office 365.</span><span class="sxs-lookup"><span data-stu-id="868e3-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="868e3-105">Подписка останется активной до тех пор, пока вы ее используете для текущей разработки.</span><span class="sxs-lookup"><span data-stu-id="868e3-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="868e3-106">Ознакомьтесь со статьей [Добро пожаловать в программу для разработчиков Office 365](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md).</span><span class="sxs-lookup"><span data-stu-id="868e3-106">See [Welcome to the Office 365 Developer Program](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md).</span></span>

<span data-ttu-id="868e3-107">Кроме того, для этого проекта необходимо установить следующие компоненты в среде разработки:</span><span class="sxs-lookup"><span data-stu-id="868e3-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="868e3-108">Любой текстовый редактор или IDE.</span><span class="sxs-lookup"><span data-stu-id="868e3-108">Any text editor or IDE.</span></span> <span data-ttu-id="868e3-109">Вы можете установить и использовать [Visual Studio Code](https://code.visualstudio.com/download) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="868e3-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="868e3-110">[Node. js/NPM](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="868e3-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="868e3-111">Следует использовать последнюю версию LTS.</span><span class="sxs-lookup"><span data-stu-id="868e3-111">You should use the latest LTS version.</span></span> <span data-ttu-id="868e3-112">Диспетчер пакетов узла (NPM) будет установлен в системе с установкой Node. js.</span><span class="sxs-lookup"><span data-stu-id="868e3-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="868e3-113">После успешной установки Node. js установите пакеты [Yeoman](https://yeoman.io/) и [gulp – CLI](https://www.npmjs.com/package/gulp-cli) , введя в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="868e3-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

```bash
npm install yo gulp-cli --global
```

- <span data-ttu-id="868e3-114">Установите генератор приложений Microsoft Teams, введя в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="868e3-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a><span data-ttu-id="868e3-115">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="868e3-115">Generate your project</span></span>

- <span data-ttu-id="868e3-116">Откройте командную строку и создайте новый каталог для проекта со вкладками.</span><span class="sxs-lookup"><span data-stu-id="868e3-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="868e3-117">Чтобы запустить генератор, перейдите к новому каталогу и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="868e3-117">To start the generator, navigate to your new directory and type the following command:</span></span>

```bash
yo teams
```

- <span data-ttu-id="868e3-118">Далее вы задаете ряд значений, которые будут использоваться в файле **manifest. JSON** приложения:</span><span class="sxs-lookup"><span data-stu-id="868e3-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

![снимок экрана открытия генератора](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

<span data-ttu-id="868e3-120">**Имя вашего решения**</span><span class="sxs-lookup"><span data-stu-id="868e3-120">**What is your solution name?**</span></span>

<span data-ttu-id="868e3-121">Это имя проекта.</span><span class="sxs-lookup"><span data-stu-id="868e3-121">This is your project name.</span></span> <span data-ttu-id="868e3-122">Вы можете принять предложенное имя, нажав клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="868e3-122">You can accept the suggested name by pressing enter.</span></span>

<span data-ttu-id="868e3-123">**Где следует разместить файлы?**</span><span class="sxs-lookup"><span data-stu-id="868e3-123">**Where do you want to place the files?**</span></span>

<span data-ttu-id="868e3-124">В настоящее время вы находитесь в каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="868e3-124">You're currently in your project directory.</span></span> <span data-ttu-id="868e3-125">Нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="868e3-125">Press enter.</span></span>

<span data-ttu-id="868e3-126">**Название проекта приложения Microsoft Teams?**</span><span class="sxs-lookup"><span data-stu-id="868e3-126">**Title of your Microsoft Teams app project?**</span></span>

<span data-ttu-id="868e3-127">Это имя пакета приложения, которое будет использоваться в манифесте и описании приложения.</span><span class="sxs-lookup"><span data-stu-id="868e3-127">This is your app package name and will be used in the app manifest and description.</span></span>

<span data-ttu-id="868e3-128">**Имя вашей компании? (максимум 32 символов)**</span><span class="sxs-lookup"><span data-stu-id="868e3-128">**Your (company) name? (max 32 characters)**</span></span>

<span data-ttu-id="868e3-129">В манифесте приложения будет использоваться название вашей компании.</span><span class="sxs-lookup"><span data-stu-id="868e3-129">Your company name will be used in the app manifest.</span></span>

<br><span data-ttu-id="868e3-130">**Какую версию манифеста вы хотите использовать?**</span><span class="sxs-lookup"><span data-stu-id="868e3-130">**Which manifest version would you like to use?**</span></span>

<span data-ttu-id="868e3-131">Выберите схему по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="868e3-131">Select the default schema.</span></span>

<span data-ttu-id="868e3-132">**Введите свой идентификатор партнера Майкрософт (если он есть). (Оставьте пустым для пропуска)**</span><span class="sxs-lookup"><span data-stu-id="868e3-132">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

<span data-ttu-id="868e3-133">Это поле не является обязательным и должно использоваться только в том случае, если вы уже участвуете в [сети партнерской корпорации Майкрософт](https://partner.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="868e3-133">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

<span data-ttu-id="868e3-134">**Что вы хотите добавить в проект?**</span><span class="sxs-lookup"><span data-stu-id="868e3-134">**What do you want to add to your project?**</span></span>

<span data-ttu-id="868e3-135">Выберите ( &ast; ) вкладку.</span><span class="sxs-lookup"><span data-stu-id="868e3-135">Select ( &ast; ) A Tab.</span></span>

<span data-ttu-id="868e3-136">**URL-адрес, на котором будет размещаться это решение?**</span><span class="sxs-lookup"><span data-stu-id="868e3-136">**The URL where you will host this solution?**</span></span>

<span data-ttu-id="868e3-137">По умолчанию генератор предлагает URL-адрес веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="868e3-137">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="868e3-138">Вы будете тестировать ваше приложение только локально, поэтому для этого краткого руководства не требуется действительный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="868e3-138">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

<span data-ttu-id="868e3-139">**Вы хотите включить тестовую платформу и начальные тесты? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="868e3-139">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

<span data-ttu-id="868e3-140">Выберите вариант **не** включать тестовую платформу для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="868e3-140">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="868e3-141">Значение по умолчанию: Да; Введите **n**.</span><span class="sxs-lookup"><span data-stu-id="868e3-141">The default is yes; enter **n**.</span></span>

<span data-ttu-id="868e3-142">**Вы хотите использовать для телеметрии Azure Application Insights? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="868e3-142">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

<span data-ttu-id="868e3-143">**Не** включайте [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="868e3-143">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="868e3-144">Значение по умолчанию — нет; Введите **n**.</span><span class="sxs-lookup"><span data-stu-id="868e3-144">The default is no; enter **n**.</span></span>

<span data-ttu-id="868e3-145">**Имя вкладки по умолчанию (максимум 16 символов)?**</span><span class="sxs-lookup"><span data-stu-id="868e3-145">**Default Tab Name (max 16 characters)?**</span></span>

<span data-ttu-id="868e3-146">Присвойте вкладке имя. Это имя вкладки будет использоваться в рамках проекта в качестве компонента файла или URL-пути.</span><span class="sxs-lookup"><span data-stu-id="868e3-146">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
