---
title: 'Учебник: создание первого приложения с помощью генератора Yeoman'
description: Узнайте, как начать создание приложений Microsoft Teams с помощью генератора Yeoman.
keywords: начало работы node.js nodejs yeoman
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: f7f0fb3ba1be28dfa7d343be3af9d122b4ad090d
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037006"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="41faf-104">Создание первого приложения Microsoft Teams с помощью генератора Yeoman</span><span class="sxs-lookup"><span data-stu-id="41faf-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

>[!Note]
><span data-ttu-id="41faf-105">Это руководство входит в состав [генератора Yeoman для вики-сайта Teams.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="41faf-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="41faf-106">В этом руководстве мы поимяем, как создать ваше первое приложение Microsoft Teams с помощью генератора Yeoman для Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="41faf-106">In this tutorial we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="41faf-107">Предполагается, что у вас есть учетная запись Teams, которая разрешает [загрузку неогрузки приложения.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="41faf-107">It assumes that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![Генератор yeoman git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="41faf-109">Настройка и подготовка компьютера</span><span class="sxs-lookup"><span data-stu-id="41faf-109">Setup and prepare your machine</span></span>

<span data-ttu-id="41faf-110">Перед началом использования генератора Yeoman необходимо установить на компьютере следующую следующую систему.</span><span class="sxs-lookup"><span data-stu-id="41faf-110">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="41faf-111">Установите Node.js.</span><span class="sxs-lookup"><span data-stu-id="41faf-111">Install Node.js</span></span>

<span data-ttu-id="41faf-112">Необходимо установить Node.js на компьютере.</span><span class="sxs-lookup"><span data-stu-id="41faf-112">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="41faf-113">Следует использовать последнюю [версию LTS.](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="41faf-113">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="41faf-114">Установка редактора кода</span><span class="sxs-lookup"><span data-stu-id="41faf-114">Install a code editor</span></span>

<span data-ttu-id="41faf-115">Вам также нужен редактор кода, вы можете использовать любой текстовый редактор, который вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="41faf-115">You also need a code editor, feel free to use whatever text editor you prefer.</span></span> <span data-ttu-id="41faf-116">Однако большая часть этой документации и снимков экрана относится к [использованию Visual Studio Code.](https://code.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="41faf-116">However most of this documentation and screenshots refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="41faf-117">Установка Yeoman и Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="41faf-117">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="41faf-118">Чтобы иметь возможность скафровки проектов с помощью генератора Teams, необходимо установить средство Yeoman, а также диспетчер задач Gulp CLI.</span><span class="sxs-lookup"><span data-stu-id="41faf-118">To be able to scaffold projects using the Teams generator you need to install the Yeoman tool as well as the Gulp CLI task manager.</span></span>

<span data-ttu-id="41faf-119">Откройте командную подсказку и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="41faf-119">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="41faf-120">Установка генератора</span><span class="sxs-lookup"><span data-stu-id="41faf-120">Install the generator</span></span>

<span data-ttu-id="41faf-121">Установите генератор Yeoman для Teams с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="41faf-121">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="41faf-122">Чтобы установить предварительные версии генератора, запустите команду:</span><span class="sxs-lookup"><span data-stu-id="41faf-122">To install preview versions of the generator, run this command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="41faf-123">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="41faf-123">Generate your project</span></span>

<span data-ttu-id="41faf-124">Откройте командную подсказку и создайте каталог, в котором вы хотите создать проект, и в этом каталоге запустите `yo teams` команду.</span><span class="sxs-lookup"><span data-stu-id="41faf-124">Open up a command prompt and create a new directory where you want to create your project and in that directory run the command `yo teams`.</span></span>

<span data-ttu-id="41faf-125">При этом запускается генератор, который задает вам несколько вопросов.</span><span class="sxs-lookup"><span data-stu-id="41faf-125">This starts the generator, which prompts you with a set of questions.</span></span>

![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

<span data-ttu-id="41faf-127">Первый вопрос — имя проекта, и вы можете оставить его без проблем, нажав ввод.</span><span class="sxs-lookup"><span data-stu-id="41faf-127">The first question is about your project name, you can leave it as is by pressing enter.</span></span> <span data-ttu-id="41faf-128">Далее вам будет запросят вопрос о том, хотите ли вы создать новый каталог или использовать текущий.</span><span class="sxs-lookup"><span data-stu-id="41faf-128">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="41faf-129">Так как мы уже находятся в нужном каталоге, мы просто нажимаем ввод.</span><span class="sxs-lookup"><span data-stu-id="41faf-129">As we already are in the directory we want, we just press enter.</span></span>

<span data-ttu-id="41faf-130">На следующем этапе вы запросите название вашего проекта. Этот заголовок будет использоваться в манифесте и описании вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="41faf-130">The following step asks for a title of your project, this title will be used in the manifest and description of your app.</span></span> <span data-ttu-id="41faf-131">Затем вам будет предложено название компании, которое также будет использоваться в манифесте.</span><span class="sxs-lookup"><span data-stu-id="41faf-131">And then you will be asked for a company name, which also will be used in the manifest.</span></span>

<span data-ttu-id="41faf-132">В пятом вопросе вы спросите, какую версию манифеста вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="41faf-132">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="41faf-133">В этом учебнике выберите `v1.5` текущую общую доступную схему.</span><span class="sxs-lookup"><span data-stu-id="41faf-133">For this tutorial select `v1.5`, which is the current general available schema.</span></span>

<span data-ttu-id="41faf-134">После этого генератор спросит, какие элементы вы хотите добавить в проект.</span><span class="sxs-lookup"><span data-stu-id="41faf-134">After this the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="41faf-135">Можно выбрать одну или любую комбинацию элементов.</span><span class="sxs-lookup"><span data-stu-id="41faf-135">You can select a single one or any combination of items.</span></span> <span data-ttu-id="41faf-136">На данный момент просто выберите *вкладку.*</span><span class="sxs-lookup"><span data-stu-id="41faf-136">For now, just select *a Tab*.</span></span>

![выбор элемента](~/assets/yeoman-images/teams-first-app-2.png)

<span data-ttu-id="41faf-138">В зависимости от выбранных элементов вам будет задан набор последующих вопросов.</span><span class="sxs-lookup"><span data-stu-id="41faf-138">Based on what items you select, you will be asked a set of follow-up questions.</span></span>

<span data-ttu-id="41faf-139">Теперь необходимо ввести URL-адрес места для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="41faf-139">Now you need to enter a URL of where you will host your solution.</span></span> <span data-ttu-id="41faf-140">Это может быть любой URL-адрес, но по умолчанию генератор предлагает URL-адрес веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="41faf-140">This can be any URL, but by default the generator suggests an Azure Web Sites URL.</span></span>

<span data-ttu-id="41faf-141">Генератор имеет множество встроенных расширенных функций, которые можно использовать или от них отказаться.</span><span class="sxs-lookup"><span data-stu-id="41faf-141">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span> <span data-ttu-id="41faf-142">После вопроса URL-адреса вам будет предложено включить unit-testing для вашего решения, по умолчанию да.</span><span class="sxs-lookup"><span data-stu-id="41faf-142">Following the URL question you will be asked if you want to include unit-testing for your solution, default is yes.</span></span> <span data-ttu-id="41faf-143">Если вы выберете этот вариант, созданный проект будет иметь структуру unit testing и некоторые стандартные тесты для различных элементов, скафруемых.</span><span class="sxs-lookup"><span data-stu-id="41faf-143">If you choose this the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> <span data-ttu-id="41faf-144">В этом руководстве не нужно включать тестовую структуру.</span><span class="sxs-lookup"><span data-stu-id="41faf-144">For this tutorial choose not to include a test framework.</span></span>

<span data-ttu-id="41faf-145">Чтобы упростить ведение журнала, вам также будет предложено использовать Azure Application Insights для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="41faf-145">In order to make logging easy for you, you will also be asked if you want to use Azure Application Insights for logging.</span></span> <span data-ttu-id="41faf-146">Если вы выберете "Да", вам потребуется предоставить ключ Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="41faf-146">If you choose Yes, you will need to provide a Azure Application Insights key.</span></span> <span data-ttu-id="41faf-147">В этом руководстве отказ от использования Application Insights.</span><span class="sxs-lookup"><span data-stu-id="41faf-147">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="41faf-148">Следующий набор вопросов будет основан на ранее выборе элементов.</span><span class="sxs-lookup"><span data-stu-id="41faf-148">The next set of questions will be based on your selection of items previously.</span></span> <span data-ttu-id="41faf-149">Для вкладки необходимо уделить только имя и при необходимости выбрать, сможете ли вы использовать это приложение в качестве веб-части SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="41faf-149">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="41faf-150">После того как вы указав это имя, генератор создает проект и устанавливает все зависимости.</span><span class="sxs-lookup"><span data-stu-id="41faf-150">Once you have provided this name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="41faf-151">Это займет минуту или две.</span><span class="sxs-lookup"><span data-stu-id="41faf-151">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="41faf-152">Добавление кода на вкладку</span><span class="sxs-lookup"><span data-stu-id="41faf-152">Add some code to your tab</span></span>

<span data-ttu-id="41faf-153">После того как генератор будет сделан, вы можете открыть решение в своем любимом редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="41faf-153">Once the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="41faf-154">Почитайте минуту или две и ознакомьтесь с тем, как организован код. Дополнительные информацию об этом можно узнать в документации [по структуре](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) проекта.</span><span class="sxs-lookup"><span data-stu-id="41faf-154">Take a minute or two and familiarize yourself with how the code is organized - you can read more about that in the [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="41faf-155">Вкладка будет расположена в `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` файле.</span><span class="sxs-lookup"><span data-stu-id="41faf-155">Your Tab will be located in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="41faf-156">Это класс на основе TypeScript React для вашей вкладки. Найдите метод и добавьте строку кода внутри управления, чтобы он `render()` `<PanelBody>` выглядел так:</span><span class="sxs-lookup"><span data-stu-id="41faf-156">This is the TypeScript React based class for your Tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="41faf-157">Сохраните файл и вернетесь в командную команду.</span><span class="sxs-lookup"><span data-stu-id="41faf-157">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="41faf-158">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="41faf-158">Build your app</span></span>

<span data-ttu-id="41faf-159">Теперь вы можете создать свой проект.</span><span class="sxs-lookup"><span data-stu-id="41faf-159">You can now build your project.</span></span> <span data-ttu-id="41faf-160">Это делается в два этапа (или один шаг, см. ниже).</span><span class="sxs-lookup"><span data-stu-id="41faf-160">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="41faf-161">Сначала необходимо создать файл манифеста приложения Teams, который вы загружаете или загружаете в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="41faf-161">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="41faf-162">Это делается задачей `gulp manifest` Gulp.</span><span class="sxs-lookup"><span data-stu-id="41faf-162">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="41faf-163">Это позволит проверить манифест и создать ZIP-файл в `./package` каталоге.</span><span class="sxs-lookup"><span data-stu-id="41faf-163">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="41faf-164">Чтобы создать решение, используйте `gulp build` команду.</span><span class="sxs-lookup"><span data-stu-id="41faf-164">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="41faf-165">При этом решение будет перенакоплено в `./dist` папку.</span><span class="sxs-lookup"><span data-stu-id="41faf-165">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="41faf-166">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="41faf-166">Run your app</span></span>

<span data-ttu-id="41faf-167">Чтобы запустить приложение, используйте `gulp serve` команду.</span><span class="sxs-lookup"><span data-stu-id="41faf-167">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="41faf-168">Это позволит создать и запустить локальный веб-сервер для тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="41faf-168">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="41faf-169">Команда также будет перестраивать приложение всякий раз, когда вы сохраняете файл в проекте.</span><span class="sxs-lookup"><span data-stu-id="41faf-169">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="41faf-170">Теперь вы сможете просмотреть, чтобы `http://localhost:3007/myFirstAppTab/` убедиться, что вкладка отрисовка.</span><span class="sxs-lookup"><span data-stu-id="41faf-170">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="41faf-171">Однако пока нет в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="41faf-171">However, not in Microsoft Teams yet.</span></span>

![просмотр сайта в браузере](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="41faf-173">Запуск приложения в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="41faf-173">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="41faf-174">Microsoft Teams не позволяет вам публиковать приложение на localhost, поэтому необходимо опубликовать его на общедоступный URL-адрес или использовать прокси-сервер, например ngrok.</span><span class="sxs-lookup"><span data-stu-id="41faf-174">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="41faf-175">Хорошие новости — это то, что в проекте скафолдера есть эта встроенная надстройка.</span><span class="sxs-lookup"><span data-stu-id="41faf-175">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="41faf-176">При запуске службы ngrok будет запущена в фоновом режиме с уникальной и открытой записью DNS, которая также упакует манифест с этим уникальным URL-адресом, а затем сделает то же самое, что `gulp ngrok-serve` `gulp serve` и .</span><span class="sxs-lookup"><span data-stu-id="41faf-176">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="41faf-177">После запуска создайте новую команду Microsoft Teams и при ее создании щелкните имя команды, чтобы перейти к параметрам команды и `gulp ngrok-serve` выбрать *"Приложения".*</span><span class="sxs-lookup"><span data-stu-id="41faf-177">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="41faf-178">В правом нижнем углу должна отобраться ссылка "Отправить пользовательское приложение", выберите его, а затем перейдите к папке проекта и вложенной папке, которая называется `package` .</span><span class="sxs-lookup"><span data-stu-id="41faf-178">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="41faf-179">Выберите ZIP-файл в этой папке и откройте.</span><span class="sxs-lookup"><span data-stu-id="41faf-179">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="41faf-180">Теперь ваше приложение загружено неогруженным в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="41faf-180">Your App is now sideloaded into Microsoft Teams.</span></span>

![неогруженные приложения](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="41faf-182">Перейдите в *общий* канал и *+* выберите, чтобы добавить новую вкладку. Вкладка должна быть в списке вкладок.</span><span class="sxs-lookup"><span data-stu-id="41faf-182">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![настройка вкладки](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="41faf-184">Выберите вкладку и следуйте инструкциям, чтобы добавить ее.</span><span class="sxs-lookup"><span data-stu-id="41faf-184">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="41faf-185">Обратите внимание, что у вас есть диалоговое окно настраиваемой конфигурации, для которого можно изменить источник.</span><span class="sxs-lookup"><span data-stu-id="41faf-185">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="41faf-186">Выберите *"Сохранить",* чтобы добавить вкладку в канал.</span><span class="sxs-lookup"><span data-stu-id="41faf-186">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="41faf-187">После этого вкладка должна быть загружена в Microsoft Teams!</span><span class="sxs-lookup"><span data-stu-id="41faf-187">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![запуск вкладки в командах](~/assets/yeoman-images/teams-first-app-6.png)

<span data-ttu-id="41faf-189">**Congrats! Вы создали и развернули свое первое приложение Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="41faf-189">**Congrats! You built and deployed your first Microsoft Teams app**</span></span>
