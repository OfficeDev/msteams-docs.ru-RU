---
title: Учебник . Создание первого приложения с помощью генератора Yeoman
description: Узнайте, как начать создание Microsoft Teams с помощью генератора Yeoman.
keywords: начало работы node.js nodejs yeoman
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 96a4f64d487e1d16bf25abd978759fedeac1061c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566826"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="89a4f-104">Создайте первое Microsoft Teams приложение с помощью генератора Yeoman</span><span class="sxs-lookup"><span data-stu-id="89a4f-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="89a4f-105">Этот учебник исходит от [генератора Yeoman для Teams вики](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="89a4f-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="89a4f-106">В этом руководстве мы пройдите по созданию первого приложения Microsoft Teams с помощью Microsoft Teams генератора Yeoman.</span><span class="sxs-lookup"><span data-stu-id="89a4f-106">In this tutorial, we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="89a4f-107">Кроме того, вы проходите процесс обновления Teams с помощью генератора Yeoman.</span><span class="sxs-lookup"><span data-stu-id="89a4f-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="89a4f-108">Обязательным условием для начала с этого руководства является то, что у вас есть Teams учетная запись, которая позволяет [загрузку приложений.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="89a4f-108">The prerequisite to start with this tutorial is that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![git генератора yeoman](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="89a4f-110">Настройка и подготовка компьютера</span><span class="sxs-lookup"><span data-stu-id="89a4f-110">Setup and prepare your machine</span></span>

<span data-ttu-id="89a4f-111">Перед использованием генератора Yeoman необходимо установить следующее на компьютере.</span><span class="sxs-lookup"><span data-stu-id="89a4f-111">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="89a4f-112">Установите Node.js.</span><span class="sxs-lookup"><span data-stu-id="89a4f-112">Install Node.js</span></span>

<span data-ttu-id="89a4f-113">Необходимо установить Node.js на компьютере.</span><span class="sxs-lookup"><span data-stu-id="89a4f-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="89a4f-114">Вы должны использовать последнюю [версию LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="89a4f-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="89a4f-115">Установка редактора кода</span><span class="sxs-lookup"><span data-stu-id="89a4f-115">Install a code editor</span></span>

<span data-ttu-id="89a4f-116">Вам нужен редактор кода.</span><span class="sxs-lookup"><span data-stu-id="89a4f-116">You need a code editor.</span></span> <span data-ttu-id="89a4f-117">Большая часть этой документации и изображений относится к использованию [Visual Studio Code.](https://code.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="89a4f-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="89a4f-118">Однако не стесняйся использовать любой текстовый редактор, который вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="89a4f-118">However, feel free to use whatever text editor you prefer.</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="89a4f-119">Установка CLI Yeoman и Gulp</span><span class="sxs-lookup"><span data-stu-id="89a4f-119">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="89a4f-120">Для реализации проектов с помощью генератора необходимо установить средство Yeoman и диспетчер задач Gulp CLI.</span><span class="sxs-lookup"><span data-stu-id="89a4f-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

<span data-ttu-id="89a4f-121">Откройте командную подсказку и введите следующее:</span><span class="sxs-lookup"><span data-stu-id="89a4f-121">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="89a4f-122">Установка генератора</span><span class="sxs-lookup"><span data-stu-id="89a4f-122">Install the generator</span></span>

<span data-ttu-id="89a4f-123">Установите генератор Teams Yeoman со следующей командой:</span><span class="sxs-lookup"><span data-stu-id="89a4f-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="89a4f-124">Установите предварительную версию генератора со следующей командой:</span><span class="sxs-lookup"><span data-stu-id="89a4f-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="89a4f-125">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="89a4f-125">Generate your project</span></span>

<span data-ttu-id="89a4f-126">В этом разделе вы можете пройти этапы создания проекта.</span><span class="sxs-lookup"><span data-stu-id="89a4f-126">This section walks you through the steps for generating your project.</span></span>

<span data-ttu-id="89a4f-127">**Создание проекта**</span><span class="sxs-lookup"><span data-stu-id="89a4f-127">**To generate your project**</span></span>

1. <span data-ttu-id="89a4f-128">Откройте командную подсказку и создайте новый каталог, в котором нужно создать проект, и в этом каталоге запустите команду `yo teams` .</span><span class="sxs-lookup"><span data-stu-id="89a4f-128">Open up a command prompt and create a new directory where you want to create your project, and in that directory run the command `yo teams`.</span></span> <span data-ttu-id="89a4f-129">Запускается генератор.</span><span class="sxs-lookup"><span data-stu-id="89a4f-129">The generator starts.</span></span>
1. <span data-ttu-id="89a4f-130">Ответьте на набор вопросов, задамых генератором:</span><span class="sxs-lookup"><span data-stu-id="89a4f-130">Respond to the set of questions prompted by the generator:</span></span>

   ![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="89a4f-132">Первый вопрос заключается в названии проекта, его можно оставить, как и при нажатии ввода.</span><span class="sxs-lookup"><span data-stu-id="89a4f-132">The first question is about your project name, you can leave it as is by pressing enter.</span></span>
   1. <span data-ttu-id="89a4f-133">Следующий вопрос задает вам, хотите ли вы создать новый каталог или использовать текущий.</span><span class="sxs-lookup"><span data-stu-id="89a4f-133">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="89a4f-134">Как вы уже находитесь в каталоге вы хотите, просто нажмите введите.</span><span class="sxs-lookup"><span data-stu-id="89a4f-134">As you are already in the directory you want, just press enter.</span></span>
   1. <span data-ttu-id="89a4f-135">В следующем вопросе введите название проекта.</span><span class="sxs-lookup"><span data-stu-id="89a4f-135">In the next question, type the title of your project.</span></span> <span data-ttu-id="89a4f-136">Это название будет использоваться в манифесте и описании приложения.</span><span class="sxs-lookup"><span data-stu-id="89a4f-136">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="89a4f-137">Далее вам будет предложено имя компании, которое также будет использоваться в манифесте.</span><span class="sxs-lookup"><span data-stu-id="89a4f-137">Next, you will be asked for a company name, which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="89a4f-138">В пятом вопросе задается вопрос о том, какую версию манифеста вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="89a4f-138">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="89a4f-139">Для этого руководства выберите `v1.5` , которая является текущей общей доступной схемой.</span><span class="sxs-lookup"><span data-stu-id="89a4f-139">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="89a4f-140">Далее генератор спросит, какие элементы необходимо добавить в проект.</span><span class="sxs-lookup"><span data-stu-id="89a4f-140">Next, the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="89a4f-141">Вы можете выбрать одно или любое сочетание элементов.</span><span class="sxs-lookup"><span data-stu-id="89a4f-141">You can select a single one or any combination of items.</span></span> <span data-ttu-id="89a4f-142">Для этого руководства просто выберите *вкладку*:</span><span class="sxs-lookup"><span data-stu-id="89a4f-142">For this tutorials, just select *a Tab*:</span></span>

    ![Выбор элементов](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="89a4f-144">Ответьте на следующий набор последующих вопросов, которые отображаются на основе элементов, выбранных на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="89a4f-144">Respond to the next set of follow-up questions that appear based on the items you selected in step 2.</span></span>
1. <span data-ttu-id="89a4f-145">Введите URL-адрес, где будет организовано решение.</span><span class="sxs-lookup"><span data-stu-id="89a4f-145">Enter a URL of where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="89a4f-146">URL-адрес может быть любым URL-адресом, но по умолчанию генератор предлагает URL-адрес веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="89a4f-146">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="89a4f-147">В следующем вопросе подтвердите, хотите ли вы включить для решения unit-testing.</span><span class="sxs-lookup"><span data-stu-id="89a4f-147">In the next question, confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="89a4f-148">Ответ по умолчанию *— да.*</span><span class="sxs-lookup"><span data-stu-id="89a4f-148">The default response is *yes*.</span></span> <span data-ttu-id="89a4f-149">Если вы решите включить блок-тестирование, созданный проект будет иметь структуру тестирования единицы и некоторые тесты по умолчанию для различных элементов, которые scaffolded.</span><span class="sxs-lookup"><span data-stu-id="89a4f-149">If you choose to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="89a4f-150">В этом руководстве не включаем тестовую базу.</span><span class="sxs-lookup"><span data-stu-id="89a4f-150">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="89a4f-151">У генератора есть множество встроенных расширенных функций, от которые можно отказаться или отказаться.</span><span class="sxs-lookup"><span data-stu-id="89a4f-151">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="89a4f-152">Чтобы упростить вход, вам также будет предложено использовать Azure Application Insights для регистрации.</span><span class="sxs-lookup"><span data-stu-id="89a4f-152">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="89a4f-153">Если вы *выберете Да,* вам потребуется предоставить ключ Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="89a4f-153">If you choose *Yes*, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="89a4f-154">Для этого руководства отказаться от использования приложения Insights.</span><span class="sxs-lookup"><span data-stu-id="89a4f-154">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="89a4f-155">Следующий набор вопросов будет основан на выбранных ранее пунктах.</span><span class="sxs-lookup"><span data-stu-id="89a4f-155">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="89a4f-156">Для вкладки необходимо только у предоставить имя и необязательно выбрать, если вы хотите иметь возможность использовать это приложение в качестве веб-SharePoint Веб-части.</span><span class="sxs-lookup"><span data-stu-id="89a4f-156">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="89a4f-157">После предоставления имени генератор будет создавать проект и устанавливать все зависимости.</span><span class="sxs-lookup"><span data-stu-id="89a4f-157">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="89a4f-158">Это займет минуту или две.</span><span class="sxs-lookup"><span data-stu-id="89a4f-158">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="89a4f-159">Добавление кода на вкладку</span><span class="sxs-lookup"><span data-stu-id="89a4f-159">Add some code to your tab</span></span>

<span data-ttu-id="89a4f-160">После того как генератор будет сделан, вы можете открыть решение в любимом редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="89a4f-160">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="89a4f-161">Минутку или две и ознакомьтесь с тем, как организован код.</span><span class="sxs-lookup"><span data-stu-id="89a4f-161">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="89a4f-162">Дополнительные сведения см. [в Project документации по структуре.](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)</span><span class="sxs-lookup"><span data-stu-id="89a4f-162">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="89a4f-163">Вкладка находится в `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` файле.</span><span class="sxs-lookup"><span data-stu-id="89a4f-163">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="89a4f-164">Это класс typeScript React на основе вкладки. Найдите `render()` метод и добавьте строку кода внутри `<PanelBody>` управления, чтобы он выглядел так:</span><span class="sxs-lookup"><span data-stu-id="89a4f-164">This is the TypeScript React-based class for your tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="89a4f-165">Сохраните файл и вернись к командной подсказке.</span><span class="sxs-lookup"><span data-stu-id="89a4f-165">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="89a4f-166">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="89a4f-166">Build your app</span></span>

<span data-ttu-id="89a4f-167">Теперь вы можете создать свой проект.</span><span class="sxs-lookup"><span data-stu-id="89a4f-167">You can now build your project.</span></span> <span data-ttu-id="89a4f-168">Это делается в два шага (или один шаг, см. ниже).</span><span class="sxs-lookup"><span data-stu-id="89a4f-168">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="89a4f-169">Сначала необходимо создать файл манифеста Teams, который вы загружаете/загружаете в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="89a4f-169">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="89a4f-170">Это делается задачей Gulp `gulp manifest` .</span><span class="sxs-lookup"><span data-stu-id="89a4f-170">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="89a4f-171">Это позволит проверить манифест и создать почтовый файл в `./package` каталоге.</span><span class="sxs-lookup"><span data-stu-id="89a4f-171">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="89a4f-172">Для создания решения используется `gulp build` команда.</span><span class="sxs-lookup"><span data-stu-id="89a4f-172">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="89a4f-173">Это будет перенакладывание решения в `./dist` папку.</span><span class="sxs-lookup"><span data-stu-id="89a4f-173">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="89a4f-174">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="89a4f-174">Run your app</span></span>

<span data-ttu-id="89a4f-175">Для запуска приложения используется `gulp serve` команда.</span><span class="sxs-lookup"><span data-stu-id="89a4f-175">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="89a4f-176">Это позволит создать и запустить локальный веб-сервер для тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="89a4f-176">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="89a4f-177">Команда также восстановит приложение всякий раз, когда вы сохраните файл в проекте.</span><span class="sxs-lookup"><span data-stu-id="89a4f-177">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="89a4f-178">Теперь вы должны иметь возможность просматривать, `http://localhost:3007/myFirstAppTab/` чтобы убедиться, что ваша вкладка отрисовка.</span><span class="sxs-lookup"><span data-stu-id="89a4f-178">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="89a4f-179">Однако пока нет Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="89a4f-179">However, not in Microsoft Teams yet:</span></span>

![просмотр сайта в браузере](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="89a4f-181">Запустите приложение в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="89a4f-181">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="89a4f-182">Microsoft Teams не позволяет размещению приложения на локальном сайте, поэтому необходимо либо опубликовать его на общедоступный URL-адрес, либо использовать прокси-сервер, например ngrok.</span><span class="sxs-lookup"><span data-stu-id="89a4f-182">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="89a4f-183">Хорошая новость заключается в том, что проект scaffolded имеет эту встроенную.</span><span class="sxs-lookup"><span data-stu-id="89a4f-183">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="89a4f-184">При запуске службы ngrok будет запущена в фоновом режиме с уникальной и открытой записью DNS, которая также будет упаковывать манифест с этим уникальным URL-адресом, а затем делать то же самое, что `gulp ngrok-serve` `gulp serve` и .</span><span class="sxs-lookup"><span data-stu-id="89a4f-184">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="89a4f-185">После запуска создайте новую команду Microsoft Teams и при ее создании щелкните имя команды, чтобы перейти к настройкам команд и выбрать `gulp ngrok-serve` *приложения.*</span><span class="sxs-lookup"><span data-stu-id="89a4f-185">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="89a4f-186">В правом нижнем углу следует просмотреть ссылку Upload настраиваемого приложения, выберите *его,* а затем просмотрите папку проекта и подмостки с названием `package` .</span><span class="sxs-lookup"><span data-stu-id="89a4f-186">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="89a4f-187">Выберите почтовый файл в этой папке и откройте.</span><span class="sxs-lookup"><span data-stu-id="89a4f-187">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="89a4f-188">Ваше приложение теперь загружено в Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="89a4f-188">Your App is now sideloaded into Microsoft Teams:</span></span>

![sideloaded app](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="89a4f-190">Возвращайся на *общий* канал и *+* выберите, чтобы добавить новую вкладку. Вы должны увидеть вкладку в списке вкладок:</span><span class="sxs-lookup"><span data-stu-id="89a4f-190">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs:</span></span>

![настройка вкладки](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="89a4f-192">Выберите вкладку и следуйте инструкциям, чтобы добавить ее.</span><span class="sxs-lookup"><span data-stu-id="89a4f-192">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="89a4f-193">Обратите внимание, что у вас есть настраиваемый диалог конфигурации, для которого можно изменить источник.</span><span class="sxs-lookup"><span data-stu-id="89a4f-193">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="89a4f-194">Выберите *Сохранить,* чтобы добавить вкладку в канал.</span><span class="sxs-lookup"><span data-stu-id="89a4f-194">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="89a4f-195">После этого вкладка должна быть загружена внутри Microsoft Teams!</span><span class="sxs-lookup"><span data-stu-id="89a4f-195">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![запуск вкладки в командах](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a><span data-ttu-id="89a4f-197">Обновление Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="89a4f-197">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="89a4f-198">Вы также можете обновить текущую версию Microsoft Teams до последней версии с помощью Microsoft Teams генератора Yeoman.</span><span class="sxs-lookup"><span data-stu-id="89a4f-198">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="89a4f-199">**Обновление Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="89a4f-199">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="89a4f-200">Получите текущую версию Teams со следующей командой:</span><span class="sxs-lookup"><span data-stu-id="89a4f-200">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="89a4f-201">Чтобы обновить генератор, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="89a4f-201">Use the following command to select update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="89a4f-202">Используйте клавиши со стрелками, чтобы **выбрать Обновление генераторов:**</span><span class="sxs-lookup"><span data-stu-id="89a4f-202">Use the  arrow keys to choose **Update your Generators**:</span></span>

   ![изображение YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="89a4f-204">Выберите нужный генератор из списка генераторов:</span><span class="sxs-lookup"><span data-stu-id="89a4f-204">Select the generator you want from the list of generators:</span></span>
   > [!NOTE]
   > <span data-ttu-id="89a4f-205">Используйте пробел для выбора или очистки выбранной Teams из доступных параметров.</span><span class="sxs-lookup"><span data-stu-id="89a4f-205">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![изображение useSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="89a4f-207">Для завершения установки Teams занимает несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="89a4f-207">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="89a4f-208">После завершения установки используйте следующую команду для проверки установленной версии:</span><span class="sxs-lookup"><span data-stu-id="89a4f-208">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
   
<span data-ttu-id="89a4f-209">**Поздравляю! Вы создали и развернули первое Microsoft Teams приложение. Вы также обновили Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="89a4f-209">**Congrats! You built and deployed your first Microsoft Teams app. You also upgraded Microsoft Teams.**</span></span>
