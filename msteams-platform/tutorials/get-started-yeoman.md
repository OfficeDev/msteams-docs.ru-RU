---
title: Приступая к работе с генератором Yeoman для Microsoft Teams
description: Знакомство с созданием качественных приложений с помощью генератора Yeoman для Microsoft Teams
keywords: Приступая к работе Node. js NodeJS Yeoman
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 217c0900e067a61e083e7ffb0b121afdaa51c49f
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2020
ms.locfileid: "43034045"
---
# <a name="build-your-first-microsoft-teams-app"></a><span data-ttu-id="e333d-104">Создание первого приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e333d-104">Build your First Microsoft Teams App</span></span>

>[!Note]
><span data-ttu-id="e333d-105">Это руководство поступает из [генератора Yeoman для вики-сайта Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="e333d-105">This tutorial comes from the [yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span></span>

<span data-ttu-id="e333d-106">В этом руководстве мы рассмотрим создание первого приложения Microsoft Teams с помощью генератора Yeoman для Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e333d-106">In this tutorial we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="e333d-107">Предполагается, что вы [включили загрузку приложений Microsoft Teams](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e333d-107">It assumes that you have [enabled side-loading of Microsoft Teams apps](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![Git генератора Yeoman](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="e333d-109">Настройка и подготовка компьютера</span><span class="sxs-lookup"><span data-stu-id="e333d-109">Setup and prepare your machine</span></span>

<span data-ttu-id="e333d-110">Перед началом работы с генератором Teams необходимо установить на компьютере следующий продукт.</span><span class="sxs-lookup"><span data-stu-id="e333d-110">You need to install the following on your machine before starting to use the Teams Generator.</span></span>

### <a name="install-node"></a><span data-ttu-id="e333d-111">Узел установки</span><span class="sxs-lookup"><span data-stu-id="e333d-111">Install Node</span></span>

<span data-ttu-id="e333d-112">На вашем компьютере должен быть установлен NodeJS.</span><span class="sxs-lookup"><span data-stu-id="e333d-112">You need to have NodeJS installed on your machine.</span></span> <span data-ttu-id="e333d-113">Следует использовать последнюю [версию LTS](https://nodejs.org/dist/latest-v8.x/).</span><span class="sxs-lookup"><span data-stu-id="e333d-113">You should use the latest [LTS version](https://nodejs.org/dist/latest-v8.x/).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="e333d-114">Установка редактора кода</span><span class="sxs-lookup"><span data-stu-id="e333d-114">Install a code editor</span></span>

<span data-ttu-id="e333d-115">Кроме того, вы можете использовать редактор кода, вы можете использовать любой текстовый редактор, который вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="e333d-115">You also need a code editor, feel free to use whatever text editor you prefer.</span></span> <span data-ttu-id="e333d-116">Однако большинство этих документов и снимков экрана ссылаются на [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="e333d-116">However most of this documentation and screenshots refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="e333d-117">Установка Yeoman и gulp CLI</span><span class="sxs-lookup"><span data-stu-id="e333d-117">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="e333d-118">Чтобы иметь возможность создавать шаблоны для проектов с помощью генератора команд, необходимо установить средство Yeoman, а также диспетчер задач CLI gulp.</span><span class="sxs-lookup"><span data-stu-id="e333d-118">To be able to scaffold projects using the Teams generator you need to install the Yeoman tool as well as the Gulp CLI task manager.</span></span>

<span data-ttu-id="e333d-119">Откройте командную строку и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e333d-119">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-microsoft-teams-apps-generator---yo-teams"></a><span data-ttu-id="e333d-120">Установка Microsoft Teams генераторов приложений Microsoft Teams — Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e333d-120">Install the Microsoft Teams Apps generator - Yo Teams</span></span>

<span data-ttu-id="e333d-121">Генератор Yeoman для приложений Microsoft Teams устанавливается с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e333d-121">The Yeoman generator for Microsoft Teams apps are installed with the following command:</span></span>

```bash
npm install generator-teams --global
```

#### <a name="install-preview-versions"></a><span data-ttu-id="e333d-122">Установка предварительных версий</span><span class="sxs-lookup"><span data-stu-id="e333d-122">Install preview versions</span></span>

<span data-ttu-id="e333d-123">Если вы хотите установить предварительные версии генератора Teams с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e333d-123">If you want to install preview versions of the Teams generator with this command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="e333d-124">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="e333d-124">Generate your project</span></span>

<span data-ttu-id="e333d-125">Откройте командную строку и создайте каталог, в котором нужно создать проект, и в этом каталоге введите команду `yo teams`.</span><span class="sxs-lookup"><span data-stu-id="e333d-125">Open up a command prompt and create a new directory where you want to create your project and in that directory type the command `yo teams`.</span></span> <span data-ttu-id="e333d-126">При этом будет запущен генератор приложений Teams, и вам будет предложено указать вопросы.</span><span class="sxs-lookup"><span data-stu-id="e333d-126">This will start the Teams Apps generator and you will be asked a set of questions.</span></span>

![yo Teams](~/assets/yeoman-images/teams-first-app-1.png)

<span data-ttu-id="e333d-128">Первый вопрос — имя проекта, вы можете оставить его, нажав клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="e333d-128">The first question is about your project name, you can leave it as is by pressing enter.</span></span> <span data-ttu-id="e333d-129">Следующий вопрос спрашивает, хотите ли вы создать новый каталог или использовать текущий.</span><span class="sxs-lookup"><span data-stu-id="e333d-129">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="e333d-130">Так как мы уже намерены в нужном каталоге, просто нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="e333d-130">As we already are in the directory we want, we just press enter.</span></span>

<span data-ttu-id="e333d-131">На следующем этапе запрашивается название проекта, этот заголовок будет использоваться в манифесте и описании приложения.</span><span class="sxs-lookup"><span data-stu-id="e333d-131">The following step asks for a title of your project, this title will be used in the manifest and description of your app.</span></span> <span data-ttu-id="e333d-132">После этого вам будет предложено ввести название компании, которое также будет использоваться в манифесте.</span><span class="sxs-lookup"><span data-stu-id="e333d-132">And then you will be asked for a company name, which also will be used in the manifest.</span></span>

<span data-ttu-id="e333d-133">В пятом вопросе вы запрашиваете, какую версию манифеста вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="e333d-133">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="e333d-134">В этом руководстве выбирается `v1.5`текущая схема общего доступа.</span><span class="sxs-lookup"><span data-stu-id="e333d-134">For this tutorial select `v1.5`, which is the current general available schema.</span></span>

<span data-ttu-id="e333d-135">После этого генератор запросит, какие элементы вы хотите добавить в проект.</span><span class="sxs-lookup"><span data-stu-id="e333d-135">After this the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="e333d-136">Можно выбрать одну или любую комбинацию элементов.</span><span class="sxs-lookup"><span data-stu-id="e333d-136">You can select a single one or any combination of items.</span></span> <span data-ttu-id="e333d-137">Пока что просто выберите *вкладку*.</span><span class="sxs-lookup"><span data-stu-id="e333d-137">For now, just select *a Tab*.</span></span>

![Выбор элемента](~/assets/yeoman-images/teams-first-app-2.png)

<span data-ttu-id="e333d-139">В зависимости от того, какие элементы выбраны, вам будет предложен набор вопросов с дальнейшими действиями.</span><span class="sxs-lookup"><span data-stu-id="e333d-139">Based on what items you select, you will be asked a set of follow-up questions.</span></span>

<span data-ttu-id="e333d-140">Теперь необходимо ввести URL-адрес, по которому будет размещено решение.</span><span class="sxs-lookup"><span data-stu-id="e333d-140">Now you need to enter a URL of where you will host your solution.</span></span> <span data-ttu-id="e333d-141">Это может быть любой URL-адрес, но по умолчанию генератор предлагает URL-адрес веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="e333d-141">This can be any URL, but by default the generator suggests an Azure Web Sites URL.</span></span>

<span data-ttu-id="e333d-142">У генератора есть множество встроенных расширенных функций, которые можно согласиться или отказаться от него.</span><span class="sxs-lookup"><span data-stu-id="e333d-142">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span> <span data-ttu-id="e333d-143">После ответа на URL-адрес вам будет предложено включить модульное тестирование для вашего решения, значение по умолчанию — Да.</span><span class="sxs-lookup"><span data-stu-id="e333d-143">Following the URL question you will be asked if you want to include unit-testing for your solution, default is yes.</span></span> <span data-ttu-id="e333d-144">При выборе этого элемента в созданном проекте будет создана платформа модульного тестирования и некоторые модульные тесты по умолчанию для различных элементов, обрабатываемых в формировании шаблонов.</span><span class="sxs-lookup"><span data-stu-id="e333d-144">If you choose this the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> <span data-ttu-id="e333d-145">В этом руководстве не следует включать платформу тестирования.</span><span class="sxs-lookup"><span data-stu-id="e333d-145">For this tutorial choose not to include a test framework.</span></span>

<span data-ttu-id="e333d-146">Чтобы упростить ведение журнала, вам также будет предложено использовать для ведения журнала Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e333d-146">In order to make logging easy for you, you will also be asked if you want to use Azure Application Insights for logging.</span></span> <span data-ttu-id="e333d-147">При нажатии кнопки Да потребуется указать ключ Application Insights для Azure.</span><span class="sxs-lookup"><span data-stu-id="e333d-147">If you choose Yes, you will need to provide a Azure Application Insights key.</span></span> <span data-ttu-id="e333d-148">В этом руководстве отказ от использования Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e333d-148">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="e333d-149">Следующий набор вопросов будет основываться на выбранных ранее элементах.</span><span class="sxs-lookup"><span data-stu-id="e333d-149">The next set of questions will be based on your selection of items previously.</span></span> <span data-ttu-id="e333d-150">Для вкладки достаточно указать имя и при необходимости выбрать, следует ли использовать это приложение в качестве веб-части SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e333d-150">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="e333d-151">После предоставления этого имени генератор создаст проект и установит все зависимости.</span><span class="sxs-lookup"><span data-stu-id="e333d-151">Once you have provided this name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="e333d-152">Это займет около двух минут.</span><span class="sxs-lookup"><span data-stu-id="e333d-152">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="e333d-153">Добавление кода на вкладку</span><span class="sxs-lookup"><span data-stu-id="e333d-153">Add some code to your tab</span></span>

<span data-ttu-id="e333d-154">После завершения генератора вы можете открыть решение в вашем любимом редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="e333d-154">Once the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="e333d-155">Уделите пару минутам или двум и познакомимся с принципами организации кода — вы можете узнать больше об этом в документации по [структуре проекта](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) .</span><span class="sxs-lookup"><span data-stu-id="e333d-155">Take a minute or two and familiarize yourself with how the code is organized - you can read more about that in the [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="e333d-156">Вкладка будет размещена в `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` файле.</span><span class="sxs-lookup"><span data-stu-id="e333d-156">Your Tab will be located in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="e333d-157">Это класс на основе реакции TypeScript для вкладки. Перейдите к `render()` методу и добавьте строку кода в `<PanelBody>` элемент управления, чтобы она выглядела следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e333d-157">This is the TypeScript React based class for your Tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="e333d-158">Сохраните файл и вернитесь в окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="e333d-158">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="e333d-159">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="e333d-159">Build your app</span></span>

<span data-ttu-id="e333d-160">Теперь можно создать проект.</span><span class="sxs-lookup"><span data-stu-id="e333d-160">You can now build your project.</span></span> <span data-ttu-id="e333d-161">Это выполняется в два этапа (или один шаг см. ниже).</span><span class="sxs-lookup"><span data-stu-id="e333d-161">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="e333d-162">Сначала необходимо создать файл манифеста приложения Teams, который вы отправляете или Загрузка неопубликованных в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e333d-162">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="e333d-163">Это выполняется задачей `gulp manifest`gulp.</span><span class="sxs-lookup"><span data-stu-id="e333d-163">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="e333d-164">При этом будет проверен манифест и создан ZIP-файл в `./package` каталоге.</span><span class="sxs-lookup"><span data-stu-id="e333d-164">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="e333d-165">Чтобы создать решение, используйте `gulp build` команду.</span><span class="sxs-lookup"><span data-stu-id="e333d-165">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="e333d-166">При этом решение будет превышено в `./dist` папку.</span><span class="sxs-lookup"><span data-stu-id="e333d-166">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="e333d-167">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="e333d-167">Run your app</span></span>

<span data-ttu-id="e333d-168">Чтобы запустить приложение, используйте `gulp serve` команду.</span><span class="sxs-lookup"><span data-stu-id="e333d-168">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="e333d-169">Это приведет к созданию и запуску локального веб-сервера для тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="e333d-169">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="e333d-170">Команда также перестраивает приложение при каждом сохранении файла в проекте.</span><span class="sxs-lookup"><span data-stu-id="e333d-170">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="e333d-171">Теперь вы можете перейти к просмотру `http://localhost:3007/myFirstAppTab/` вкладки.</span><span class="sxs-lookup"><span data-stu-id="e333d-171">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="e333d-172">Тем не менее в Microsoft Teams пока нет.</span><span class="sxs-lookup"><span data-stu-id="e333d-172">However, not in Microsoft Teams yet.</span></span>

![Просмотр сайта в браузере](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="e333d-174">Запуск приложения в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e333d-174">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="e333d-175">Microsoft Teams не позволяет размещать приложение на localhost, поэтому необходимо опубликовать его на общедоступном URL-адресе или использовать прокси-сервер, такой как ngrok.</span><span class="sxs-lookup"><span data-stu-id="e333d-175">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="e333d-176">Хорошая новость состоит в том, что проект с формированием шаблонов содержит эту встроенную надстройку.</span><span class="sxs-lookup"><span data-stu-id="e333d-176">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="e333d-177">При запуске `gulp ngrok-serve` службы ngrok будет запускаться в фоновом режиме с уникальной и общедоступной ЗАПИСЬю DNS, а также будет упакован манифест с помощью этого уникального URL-адреса, а затем выполнить точно `gulp serve`то же самое, что и.</span><span class="sxs-lookup"><span data-stu-id="e333d-177">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="e333d-178">После запуска `gulp ngrok-serve`создайте новую группу Microsoft Teams и при ее создании щелкните имя группы, чтобы перейти к параметрам Teams, а затем выберите *приложения*.</span><span class="sxs-lookup"><span data-stu-id="e333d-178">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="e333d-179">В правом нижнем углу должна появиться ссылка *Отправить настраиваемое приложение*, выбрать его и перейти к папке проекта и вызываемой `package`вложенной папке.</span><span class="sxs-lookup"><span data-stu-id="e333d-179">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="e333d-180">Выберите ZIP-файл в этой папке и нажмите кнопку Открыть.</span><span class="sxs-lookup"><span data-stu-id="e333d-180">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="e333d-181">Теперь ваше приложение неопубликованные в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e333d-181">Your App is now sideloaded into Microsoft Teams.</span></span>

![приложение неопубликованные](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="e333d-183">Вернитесь к *общему* каналу и щелкните *+* , чтобы добавить новую вкладку. Вкладка должна отображаться в списке вкладок.</span><span class="sxs-lookup"><span data-stu-id="e333d-183">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![Настройка вкладки](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="e333d-185">Перейдите на вкладку и следуйте инструкциям по ее добавлению.</span><span class="sxs-lookup"><span data-stu-id="e333d-185">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="e333d-186">Обратите внимание, что у вас есть настраиваемое диалоговое окно конфигурации, в котором можно изменить источник.</span><span class="sxs-lookup"><span data-stu-id="e333d-186">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="e333d-187">Нажмите кнопку *сохранить* , чтобы добавить вкладку в канал.</span><span class="sxs-lookup"><span data-stu-id="e333d-187">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="e333d-188">После этого вкладка должна быть загружена в Microsoft Teams!</span><span class="sxs-lookup"><span data-stu-id="e333d-188">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![Вкладка "работа" в Teams](~/assets/yeoman-images/teams-first-app-6.png)

<span data-ttu-id="e333d-190">**Поздравляем! Вы создали и развернули первое приложение Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="e333d-190">**Congrats! You built and deployed your first Microsoft Teams App**</span></span>
