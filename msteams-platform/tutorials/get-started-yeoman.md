---
title: Учебник - Создайте свое первое приложение с помощью генератора Yeoman
description: Узнайте, как начать строить Microsoft Teams приложения с генератором Yeoman.
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
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="e479d-104">Создайте свое первое Microsoft Teams с помощью генератора Yeoman</span><span class="sxs-lookup"><span data-stu-id="e479d-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="e479d-105">Этот учебник исходит от [генератора Yeoman для Teams вики](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="e479d-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="e479d-106">В этом учебнике мы пройдитесь по созданию вашего самого первого Microsoft Teams с помощью Microsoft Teams генератора Yeoman.</span><span class="sxs-lookup"><span data-stu-id="e479d-106">In this tutorial, we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="e479d-107">Он также проходит через процесс модернизации вашего Teams с помощью генератора Yeoman.</span><span class="sxs-lookup"><span data-stu-id="e479d-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="e479d-108">Предпосылкой для начала с этого учебника является то, что у вас есть Teams, которая позволяет [приложение sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e479d-108">The prerequisite to start with this tutorial is that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![генератор yeoman git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="e479d-110">Настройка и подготовка машины</span><span class="sxs-lookup"><span data-stu-id="e479d-110">Setup and prepare your machine</span></span>

<span data-ttu-id="e479d-111">Вы должны установить следующее на вашей машине, прежде чем начать использовать генератор Yeoman.</span><span class="sxs-lookup"><span data-stu-id="e479d-111">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="e479d-112">Установите Node.js.</span><span class="sxs-lookup"><span data-stu-id="e479d-112">Install Node.js</span></span>

<span data-ttu-id="e479d-113">Вы должны иметь Node.js установлен на вашей машине.</span><span class="sxs-lookup"><span data-stu-id="e479d-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="e479d-114">Вы должны использовать последнюю [версию LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="e479d-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="e479d-115">Установка редактора кода</span><span class="sxs-lookup"><span data-stu-id="e479d-115">Install a code editor</span></span>

<span data-ttu-id="e479d-116">Вам нужен редактор кода.</span><span class="sxs-lookup"><span data-stu-id="e479d-116">You need a code editor.</span></span> <span data-ttu-id="e479d-117">Большая часть этой документации и изображений относится к [использованию Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="e479d-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="e479d-118">Тем не менее, не стесняйтесь использовать любой текстовый редактор вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="e479d-118">However, feel free to use whatever text editor you prefer.</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="e479d-119">Установка Yeoman и Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="e479d-119">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="e479d-120">Для строительных лесов проектов с помощью генератора, вы должны установить инструмент Yeoman и Gulp CLI менеджер задач.</span><span class="sxs-lookup"><span data-stu-id="e479d-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

<span data-ttu-id="e479d-121">Откройте подсказку команды и ввеми следующие:</span><span class="sxs-lookup"><span data-stu-id="e479d-121">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="e479d-122">Установка генератора</span><span class="sxs-lookup"><span data-stu-id="e479d-122">Install the generator</span></span>

<span data-ttu-id="e479d-123">Установите Teams Yeoman со следующей командой:</span><span class="sxs-lookup"><span data-stu-id="e479d-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="e479d-124">Установите предварительную версию генератора со следующей командой:</span><span class="sxs-lookup"><span data-stu-id="e479d-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="e479d-125">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="e479d-125">Generate your project</span></span>

<span data-ttu-id="e479d-126">Этот раздел проготовит шаги по созданию проекта.</span><span class="sxs-lookup"><span data-stu-id="e479d-126">This section walks you through the steps for generating your project.</span></span>

<span data-ttu-id="e479d-127">**Создание проекта**</span><span class="sxs-lookup"><span data-stu-id="e479d-127">**To generate your project**</span></span>

1. <span data-ttu-id="e479d-128">Откройте подсказку команды и создайте новый каталог, где вы хотите создать свой проект, и в этом каталоге запустите `yo teams` команду.</span><span class="sxs-lookup"><span data-stu-id="e479d-128">Open up a command prompt and create a new directory where you want to create your project, and in that directory run the command `yo teams`.</span></span> <span data-ttu-id="e479d-129">Генератор запускается.</span><span class="sxs-lookup"><span data-stu-id="e479d-129">The generator starts.</span></span>
1. <span data-ttu-id="e479d-130">Ответьте на набор вопросов, подсказав генератором:</span><span class="sxs-lookup"><span data-stu-id="e479d-130">Respond to the set of questions prompted by the generator:</span></span>

   ![йо команды](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="e479d-132">Первый вопрос о названии проекта, вы можете оставить его как есть, нажав введите.</span><span class="sxs-lookup"><span data-stu-id="e479d-132">The first question is about your project name, you can leave it as is by pressing enter.</span></span>
   1. <span data-ttu-id="e479d-133">Следующий вопрос задает вам, хотите ли вы создать новый каталог или использовать текущий.</span><span class="sxs-lookup"><span data-stu-id="e479d-133">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="e479d-134">Как вы уже в каталоге вы хотите, просто нажмите введите.</span><span class="sxs-lookup"><span data-stu-id="e479d-134">As you are already in the directory you want, just press enter.</span></span>
   1. <span data-ttu-id="e479d-135">В следующем вопросе ввемите название проекта.</span><span class="sxs-lookup"><span data-stu-id="e479d-135">In the next question, type the title of your project.</span></span> <span data-ttu-id="e479d-136">Это название будет использовано в манифесте и описании вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="e479d-136">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="e479d-137">Далее вас попросят название компании, которое также будет использовано в манифесте.</span><span class="sxs-lookup"><span data-stu-id="e479d-137">Next, you will be asked for a company name, which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="e479d-138">Пятый вопрос спрашивает вас о том, какую версию манифеста вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="e479d-138">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="e479d-139">Для этого учебника `v1.5` выберите , который является текущей общей доступной схеме.</span><span class="sxs-lookup"><span data-stu-id="e479d-139">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="e479d-140">Далее генератор спросит вас, какие элементы вы хотите добавить в свой проект.</span><span class="sxs-lookup"><span data-stu-id="e479d-140">Next, the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="e479d-141">Вы можете выбрать одну или любую комбинацию элементов.</span><span class="sxs-lookup"><span data-stu-id="e479d-141">You can select a single one or any combination of items.</span></span> <span data-ttu-id="e479d-142">Для этого учебники, просто *выберите Tab:*</span><span class="sxs-lookup"><span data-stu-id="e479d-142">For this tutorials, just select *a Tab*:</span></span>

    ![выбор элемента](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="e479d-144">Ответьте на следующий набор последующих вопросов, которые отображаются на основе элементов, выбранных в шаге 2.</span><span class="sxs-lookup"><span data-stu-id="e479d-144">Respond to the next set of follow-up questions that appear based on the items you selected in step 2.</span></span>
1. <span data-ttu-id="e479d-145">Введите URL-адрес, где вы будете разместить свое решение.</span><span class="sxs-lookup"><span data-stu-id="e479d-145">Enter a URL of where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="e479d-146">URL может быть любым URL, но по умолчанию генератор предлагает URL веб-узла Azure.</span><span class="sxs-lookup"><span data-stu-id="e479d-146">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="e479d-147">В следующем вопросе подтвердите, хотите ли вы включить в свое решение унитарное тестирование.</span><span class="sxs-lookup"><span data-stu-id="e479d-147">In the next question, confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="e479d-148">Ответ по умолчанию *да*.</span><span class="sxs-lookup"><span data-stu-id="e479d-148">The default response is *yes*.</span></span> <span data-ttu-id="e479d-149">Если вы решите включить в него унитарное тестирование, то генерируемый проект будет иметь рамку тестирования единицы и некоторые единицы тестов по умолчанию для различных элементов, которые вымолись под строительные леса.</span><span class="sxs-lookup"><span data-stu-id="e479d-149">If you choose to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="e479d-150">Для этого учебника не включать тестовую основу.</span><span class="sxs-lookup"><span data-stu-id="e479d-150">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="e479d-151">Генератор имеет много встроенных расширенных функций, которые вы можете отказаться или отказаться от.</span><span class="sxs-lookup"><span data-stu-id="e479d-151">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="e479d-152">Для того, чтобы сделать регистрацию легкой для вас, вас также попросят, хотите ли вы использовать Azure Application Insights для регистрации.</span><span class="sxs-lookup"><span data-stu-id="e479d-152">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="e479d-153">Если вы *выберете* Да, вам нужно будет предоставить ключ Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e479d-153">If you choose *Yes*, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="e479d-154">Для этого учебника отказаться от использования приложения Исследования.</span><span class="sxs-lookup"><span data-stu-id="e479d-154">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="e479d-155">Следующий набор вопросов будет основываться на ранее выбранных пунктах.</span><span class="sxs-lookup"><span data-stu-id="e479d-155">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="e479d-156">Для вкладки вам нужно только узнать имя и дополнительно выбрать, если вы хотите иметь возможность использовать это приложение в качестве SharePoint интернет-части.</span><span class="sxs-lookup"><span data-stu-id="e479d-156">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="e479d-157">После предоставления имени генератор будет генерировать проект и устанавливать все зависимости.</span><span class="sxs-lookup"><span data-stu-id="e479d-157">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="e479d-158">Это займет минуту или две.</span><span class="sxs-lookup"><span data-stu-id="e479d-158">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="e479d-159">Добавить код в вкладку</span><span class="sxs-lookup"><span data-stu-id="e479d-159">Add some code to your tab</span></span>

<span data-ttu-id="e479d-160">После того, как генератор будет сделан, вы можете открыть решение в любимом редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="e479d-160">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="e479d-161">Возьмите минуту или две и ознакомитесь с тем, как организован код.</span><span class="sxs-lookup"><span data-stu-id="e479d-161">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="e479d-162">Для получения дополнительной информации [с Project м.](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)</span><span class="sxs-lookup"><span data-stu-id="e479d-162">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="e479d-163">Ваша вкладка в `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` файле.</span><span class="sxs-lookup"><span data-stu-id="e479d-163">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="e479d-164">Это класс TypeScript React основе для вашей вкладки. Найдите `render()` метод и добавьте строку кода внутри `<PanelBody>` управления, чтобы она выглядела так:</span><span class="sxs-lookup"><span data-stu-id="e479d-164">This is the TypeScript React-based class for your tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="e479d-165">Сохраните файл и вернитесь к подсказке команды.</span><span class="sxs-lookup"><span data-stu-id="e479d-165">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="e479d-166">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="e479d-166">Build your app</span></span>

<span data-ttu-id="e479d-167">Теперь вы можете построить свой проект.</span><span class="sxs-lookup"><span data-stu-id="e479d-167">You can now build your project.</span></span> <span data-ttu-id="e479d-168">Это делается в два этапа (или один шаг, см. ниже).</span><span class="sxs-lookup"><span data-stu-id="e479d-168">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="e479d-169">Сначала вам нужно создать Teams app манифест файл, который вы загружаете / sideload в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e479d-169">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="e479d-170">Это делается по задаче Gulp `gulp manifest` .</span><span class="sxs-lookup"><span data-stu-id="e479d-170">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="e479d-171">Это позволит проверить манифест и создать почтовый файл в `./package` каталоге.</span><span class="sxs-lookup"><span data-stu-id="e479d-171">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="e479d-172">Для создания решения используется `gulp build` команда.</span><span class="sxs-lookup"><span data-stu-id="e479d-172">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="e479d-173">Это перекапит ваше решение в `./dist` папку.</span><span class="sxs-lookup"><span data-stu-id="e479d-173">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="e479d-174">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="e479d-174">Run your app</span></span>

<span data-ttu-id="e479d-175">Для запуска приложения используется `gulp serve` команда.</span><span class="sxs-lookup"><span data-stu-id="e479d-175">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="e479d-176">Это позволит создать и начать локальный веб-сервер для тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="e479d-176">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="e479d-177">Команда также восстанавливает приложение всякий раз, когда вы сохраните файл в проекте.</span><span class="sxs-lookup"><span data-stu-id="e479d-177">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="e479d-178">Теперь вы должны быть в состоянии просматривать, `http://localhost:3007/myFirstAppTab/` чтобы убедиться, что ваша вкладка рендеринга.</span><span class="sxs-lookup"><span data-stu-id="e479d-178">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="e479d-179">Однако, еще Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="e479d-179">However, not in Microsoft Teams yet:</span></span>

![просмотр вашего сайта в браузере](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="e479d-181">Запустите приложение в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e479d-181">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="e479d-182">Microsoft Teams не позволяет вам иметь ваше приложение размещено на localhost, так что вам нужно либо опубликовать его на общедоступный URL или использовать прокси, такие как ngrok.</span><span class="sxs-lookup"><span data-stu-id="e479d-182">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="e479d-183">Хорошей новостью является то, что леса проекта имеет этот встроенный.</span><span class="sxs-lookup"><span data-stu-id="e479d-183">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="e479d-184">При запуске `gulp ngrok-serve` ngrok служба будет запущена в фоновом режиме, с уникальной и публичной записи DNS, и он также пакет манифест с этим уникальным URL, а затем сделать то же самое, как `gulp serve` .</span><span class="sxs-lookup"><span data-stu-id="e479d-184">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="e479d-185">После запуска `gulp ngrok-serve` создайте новую команду Microsoft Teams и когда она будет создана, нажмите на имя команды, чтобы перейти к настройкам команд, а затем выбрать *Apps.*</span><span class="sxs-lookup"><span data-stu-id="e479d-185">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="e479d-186">В правом нижнем углу вы должны увидеть ссылку *Upload пользовательское приложение,* выберите его, а затем просматривать папку проекта и subfolder называется `package` .</span><span class="sxs-lookup"><span data-stu-id="e479d-186">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="e479d-187">Выберите файл zip в этой папке и выберите открытый.</span><span class="sxs-lookup"><span data-stu-id="e479d-187">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="e479d-188">Теперь ваше приложение загружено в Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="e479d-188">Your App is now sideloaded into Microsoft Teams:</span></span>

![боковое приложение](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="e479d-190">Вернитесь к *Общему* каналу и *+* выберите добавление новой вкладки. Вы должны увидеть свою вкладку в списке вкладок:</span><span class="sxs-lookup"><span data-stu-id="e479d-190">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs:</span></span>

![настройка вкладки](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="e479d-192">Выберите вкладку и следуйте инструкциям, чтобы добавить ее.</span><span class="sxs-lookup"><span data-stu-id="e479d-192">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="e479d-193">Обратите внимание, что у вас есть пользовательский диалог конфигурации, для которого вы можете редактировать источник.</span><span class="sxs-lookup"><span data-stu-id="e479d-193">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="e479d-194">Выберите *Сохранить,* чтобы добавить вкладку в канал.</span><span class="sxs-lookup"><span data-stu-id="e479d-194">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="e479d-195">После того, как сделали вкладку должны быть загружены Microsoft Teams!</span><span class="sxs-lookup"><span data-stu-id="e479d-195">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![работает вкладка в командах](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a><span data-ttu-id="e479d-197">Обновление Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e479d-197">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="e479d-198">Вы также можете обновить текущую Microsoft Teams версию до последней версии с помощью Microsoft Teams генератора Yeoman.</span><span class="sxs-lookup"><span data-stu-id="e479d-198">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="e479d-199">**Для обновления Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="e479d-199">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="e479d-200">Получите текущую версию Teams со следующей командой:</span><span class="sxs-lookup"><span data-stu-id="e479d-200">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="e479d-201">Используйте следующую команду, чтобы выбрать обновление генератора:</span><span class="sxs-lookup"><span data-stu-id="e479d-201">Use the following command to select update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="e479d-202">Используйте клавиши **стрелки, чтобы выбрать обновление генераторов:**</span><span class="sxs-lookup"><span data-stu-id="e479d-202">Use the  arrow keys to choose **Update your Generators**:</span></span>

   ![изображение YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="e479d-204">Выберите генератор, который вы хотите из списка генераторов:</span><span class="sxs-lookup"><span data-stu-id="e479d-204">Select the generator you want from the list of generators:</span></span>
   > [!NOTE]
   > <span data-ttu-id="e479d-205">Используйте планку пространства, чтобы выбрать или очистить выбранную Teams версию из доступных опций.</span><span class="sxs-lookup"><span data-stu-id="e479d-205">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![изображение UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="e479d-207">Установка системы занимает от нескольких секунд Teams минут.</span><span class="sxs-lookup"><span data-stu-id="e479d-207">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="e479d-208">После завершения установки используйте следующую команду для проверки установленной версии:</span><span class="sxs-lookup"><span data-stu-id="e479d-208">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
   
<span data-ttu-id="e479d-209">**Поздравляю! Вы создали и развернули свое первое Microsoft Teams приложение. Вы также обновили Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="e479d-209">**Congrats! You built and deployed your first Microsoft Teams app. You also upgraded Microsoft Teams.**</span></span>
