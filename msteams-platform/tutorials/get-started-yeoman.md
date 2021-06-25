---
title: Учебник . Создание первого приложения с помощью генератора Yeoman
description: Узнайте, как начать создание Microsoft Teams с помощью генератора Yeoman.
keywords: начало работы node.js nodejs yeoman
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: ed9e9c15c1287bb6d26778161302e45833205a75
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114400"
---
# <a name="build-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="0923f-104">Создайте первое Microsoft Teams приложение с помощью генератора Yeoman</span><span class="sxs-lookup"><span data-stu-id="0923f-104">Build your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="0923f-105">Этот учебник исходит от [генератора Yeoman для Teams вики](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="0923f-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="0923f-106">В этом руководстве вы узнаете, как создать первое приложение Microsoft Teams с помощью Microsoft Teams генератора Yeoman.</span><span class="sxs-lookup"><span data-stu-id="0923f-106">In this tutorial, you will learn how to build your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="0923f-107">Кроме того, вы проходите процесс обновления Teams с помощью генератора Yeoman.</span><span class="sxs-lookup"><span data-stu-id="0923f-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="0923f-108">Перед началом работы необходимо иметь Teams учетную запись, позволяющую [загрузку приложений.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="0923f-108">Before you begin, you must have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![git генератора yeoman](~/assets/yeoman-demo.gif)

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="0923f-110">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="0923f-110">Get Prerequisites</span></span>

<span data-ttu-id="0923f-111">Чтобы начать использовать генератор Yeoman, необходимо установить следующее на компьютере:</span><span class="sxs-lookup"><span data-stu-id="0923f-111">You need to install the following on your machine before starting to use the Yeoman generator:</span></span>

* <span data-ttu-id="0923f-112">Node.js</span><span class="sxs-lookup"><span data-stu-id="0923f-112">Node.js</span></span>

   <span data-ttu-id="0923f-113">Необходимо установить Node.js на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0923f-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="0923f-114">Вы должны использовать последнюю [версию LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="0923f-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

* <span data-ttu-id="0923f-115">Редактор кода</span><span class="sxs-lookup"><span data-stu-id="0923f-115">A code editor</span></span>

   <span data-ttu-id="0923f-116">Вам нужен редактор кода.</span><span class="sxs-lookup"><span data-stu-id="0923f-116">You need a code editor.</span></span> <span data-ttu-id="0923f-117">Большая часть этой документации и изображений относится к использованию [Visual Studio Code.](https://code.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="0923f-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="0923f-118">Однако не стесняйся использовать любой текстовый редактор, который вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="0923f-118">However, feel free to use whatever text editor you prefer.</span></span>

* <span data-ttu-id="0923f-119">Yeoman и Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="0923f-119">Yeoman and Gulp CLI</span></span>

   <span data-ttu-id="0923f-120">Для реализации проектов с помощью генератора необходимо установить средство Yeoman и диспетчер задач Gulp CLI.</span><span class="sxs-lookup"><span data-stu-id="0923f-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

   <span data-ttu-id="0923f-121">Откройте командную подсказку и введите следующее:</span><span class="sxs-lookup"><span data-stu-id="0923f-121">Open up a command prompt and type the following:</span></span>

   ```bash
   npm install yo gulp-cli --global
   ```

## <a name="install-the-generator"></a><span data-ttu-id="0923f-122">Установка генератора</span><span class="sxs-lookup"><span data-stu-id="0923f-122">Install the generator</span></span>

<span data-ttu-id="0923f-123">Установите генератор Teams Yeoman со следующей командой:</span><span class="sxs-lookup"><span data-stu-id="0923f-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm init yo teams
```

<span data-ttu-id="0923f-124">Установите предварительную версию генератора со следующей командой:</span><span class="sxs-lookup"><span data-stu-id="0923f-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm init yo teams@preview
```

## <a name="generate-your-project"></a><span data-ttu-id="0923f-125">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="0923f-125">Generate your project</span></span>

<span data-ttu-id="0923f-126">В этом разделе вы сможете ходить по шагам, которые необходимо предпринять для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="0923f-126">This section walks you through the steps to generate your project.</span></span>

<span data-ttu-id="0923f-127">**Создание проекта**</span><span class="sxs-lookup"><span data-stu-id="0923f-127">**To generate your project**</span></span>

1. <span data-ttu-id="0923f-128">Откройте командную подсказку и создайте новый каталог, в котором необходимо создать проект.</span><span class="sxs-lookup"><span data-stu-id="0923f-128">Open a command prompt and create a new directory where you want to create your project.</span></span>
1. <span data-ttu-id="0923f-129">Перейдите в каталог и запустите команду `yo teams` .</span><span class="sxs-lookup"><span data-stu-id="0923f-129">Go to the directory, and run the command `yo teams`.</span></span> <span data-ttu-id="0923f-130">Запускается генератор.</span><span class="sxs-lookup"><span data-stu-id="0923f-130">The generator starts.</span></span>
1. <span data-ttu-id="0923f-131">Ответьте на набор вопросов, задамых генератором:</span><span class="sxs-lookup"><span data-stu-id="0923f-131">Respond to the set of questions prompted by the generator:</span></span>

   ![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="0923f-133">Введите имя для проекта.</span><span class="sxs-lookup"><span data-stu-id="0923f-133">Enter a name for your project.</span></span> <span data-ttu-id="0923f-134">Вы можете оставить его так же, как и при нажатии ввода.</span><span class="sxs-lookup"><span data-stu-id="0923f-134">You can leave it as is by pressing Enter.</span></span>
   1. <span data-ttu-id="0923f-135">Введите путь для нового каталога, если вы хотите создать новый каталог.</span><span class="sxs-lookup"><span data-stu-id="0923f-135">Enter a path for the new directory if you want to create a new directory.</span></span> <span data-ttu-id="0923f-136">Как вы уже находитесь в каталоге вы хотите, просто нажмите ввод.</span><span class="sxs-lookup"><span data-stu-id="0923f-136">As you are already in the directory you want, just press Enter.</span></span>
   1. <span data-ttu-id="0923f-137">Введите название проекта.</span><span class="sxs-lookup"><span data-stu-id="0923f-137">Enter the title of your project.</span></span> <span data-ttu-id="0923f-138">Это название будет использоваться в манифесте и описании приложения.</span><span class="sxs-lookup"><span data-stu-id="0923f-138">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="0923f-139">Введите имя компании, которое также будет использоваться в манифесте.</span><span class="sxs-lookup"><span data-stu-id="0923f-139">Enter a company name which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="0923f-140">Введите версию манифеста, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="0923f-140">Enter the version of the manifest you want to use.</span></span> <span data-ttu-id="0923f-141">Для этого руководства выберите `v1.5` , которая является текущей общей доступной схемой.</span><span class="sxs-lookup"><span data-stu-id="0923f-141">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="0923f-142">Выберите элементы, которые необходимо добавить в проект.</span><span class="sxs-lookup"><span data-stu-id="0923f-142">Select the items you want to add to your project.</span></span> <span data-ttu-id="0923f-143">Вы можете выбрать одно или любое сочетание элементов.</span><span class="sxs-lookup"><span data-stu-id="0923f-143">You can select a single one or any combination of items.</span></span> <span data-ttu-id="0923f-144">Для этого руководства просто выберите *вкладку*:</span><span class="sxs-lookup"><span data-stu-id="0923f-144">For this tutorials, just select *a Tab*:</span></span>

    ![Выбор элементов](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="0923f-146">Ответьте на следующий набор последующих вопросов, которые отображаются на основе элементов, выбранных в шаге 2.</span><span class="sxs-lookup"><span data-stu-id="0923f-146">Respond to the next set of follow-up questions that appear based on the items you selected in Step 2.</span></span>
1. <span data-ttu-id="0923f-147">Введите URL-адрес для расположения, в котором будет расположено решение.</span><span class="sxs-lookup"><span data-stu-id="0923f-147">Enter a URL for the location where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="0923f-148">URL-адрес может быть любым URL-адресом, но по умолчанию генератор предлагает URL-адрес веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="0923f-148">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="0923f-149">Подтвердите, хотите ли вы включить для решения unit-testing.</span><span class="sxs-lookup"><span data-stu-id="0923f-149">Confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="0923f-150">Ответ по умолчанию **да**.</span><span class="sxs-lookup"><span data-stu-id="0923f-150">The default response is **Yes**.</span></span> <span data-ttu-id="0923f-151">Если вы решите включить unit-testing, созданный проект будет иметь структуру тестирования единицы и некоторые тесты по умолчанию для различных элементов, которые леса.</span><span class="sxs-lookup"><span data-stu-id="0923f-151">If you opt to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="0923f-152">В этом руководстве не включаем тестовую базу.</span><span class="sxs-lookup"><span data-stu-id="0923f-152">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="0923f-153">У генератора есть множество встроенных расширенных функций, от которые можно отказаться или отказаться.</span><span class="sxs-lookup"><span data-stu-id="0923f-153">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="0923f-154">Чтобы сделать вход простым для вас, вам также будет предложено использовать приложение Azure Аналитика для регистрации.</span><span class="sxs-lookup"><span data-stu-id="0923f-154">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="0923f-155">Если вы **выберете Да,** вам потребуется предоставить ключ azure application Аналитика.</span><span class="sxs-lookup"><span data-stu-id="0923f-155">If you select **Yes**, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="0923f-156">Для этого руководства отказаться от использования приложения Аналитика.</span><span class="sxs-lookup"><span data-stu-id="0923f-156">For this tutorial opt-out of using Application Insights.</span></span>

   <span data-ttu-id="0923f-157">Следующий набор вопросов будет основан на выбранных ранее пунктах.</span><span class="sxs-lookup"><span data-stu-id="0923f-157">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="0923f-158">Для вкладки необходимо только у предоставить имя и необязательно выбрать, если вы хотите иметь возможность использовать это приложение в качестве веб-SharePoint Веб-части.</span><span class="sxs-lookup"><span data-stu-id="0923f-158">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="0923f-159">После предоставления имени генератор будет создавать проект и устанавливать все зависимости.</span><span class="sxs-lookup"><span data-stu-id="0923f-159">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="0923f-160">Это займет минуту или две.</span><span class="sxs-lookup"><span data-stu-id="0923f-160">This will take a minute or two.</span></span>

## <a name="add-code-to-your-tab"></a><span data-ttu-id="0923f-161">Добавление кода на вкладку</span><span class="sxs-lookup"><span data-stu-id="0923f-161">Add code to your tab</span></span>

<span data-ttu-id="0923f-162">После того как генератор будет сделан, вы можете открыть решение в любимом редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="0923f-162">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="0923f-163">Минутку или две и ознакомьтесь с тем, как организован код.</span><span class="sxs-lookup"><span data-stu-id="0923f-163">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="0923f-164">Дополнительные сведения см. [в Project документации по структуре.](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)</span><span class="sxs-lookup"><span data-stu-id="0923f-164">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="0923f-165">Вкладка находится в `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` файле.</span><span class="sxs-lookup"><span data-stu-id="0923f-165">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="0923f-166">Это класс typeScript React на основе вкладки.</span><span class="sxs-lookup"><span data-stu-id="0923f-166">This is the TypeScript React-based class for your tab.</span></span> 

1. <span data-ttu-id="0923f-167">Найдите `render()` метод и добавьте строку кода внутри `<PanelBody>` управления, чтобы он выглядел так:</span><span class="sxs-lookup"><span data-stu-id="0923f-167">Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

   ``` TypeScript
   <PanelBody>
      <div style={styles.section}>
      Hello World! Yo Teams rocks!
      </div>
   </PanelBody>
   ```
1. <span data-ttu-id="0923f-168">Сохраните файл и вернись к командной подсказке.</span><span class="sxs-lookup"><span data-stu-id="0923f-168">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="0923f-169">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="0923f-169">Build your app</span></span>

<span data-ttu-id="0923f-170">Теперь вы можете создать свой проект.</span><span class="sxs-lookup"><span data-stu-id="0923f-170">You can now build your project.</span></span> <span data-ttu-id="0923f-171">Это делается в два шага.</span><span class="sxs-lookup"><span data-stu-id="0923f-171">This is done in two steps.</span></span>

1. <span data-ttu-id="0923f-172">Создайте файл манифеста Teams приложения для приложения, которое вы загрузили в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0923f-172">Create the Teams App manifest file for the app that you uploaded into Microsoft Teams.</span></span> <span data-ttu-id="0923f-173">Это делается задачей Gulp `gulp manifest` .</span><span class="sxs-lookup"><span data-stu-id="0923f-173">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="0923f-174">Это позволит проверить манифест и создать почтовый файл в `./package` каталоге.</span><span class="sxs-lookup"><span data-stu-id="0923f-174">This will validate the manifest and create a zip file in the `./package` directory.</span></span>
1. <span data-ttu-id="0923f-175">Запустите `gulp build` команду для создания решения.</span><span class="sxs-lookup"><span data-stu-id="0923f-175">Run the `gulp build` command to build the solution.</span></span> <span data-ttu-id="0923f-176">Это будет перенакладывание решения в `./dist` папку.</span><span class="sxs-lookup"><span data-stu-id="0923f-176">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="0923f-177">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="0923f-177">Run your app</span></span>

<span data-ttu-id="0923f-178">Чтобы запустить приложение, используйте `gulp serve` команду.</span><span class="sxs-lookup"><span data-stu-id="0923f-178">To run your app, use the `gulp serve` command.</span></span> <span data-ttu-id="0923f-179">Это позволит создать и запустить локальный веб-сервер для тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="0923f-179">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="0923f-180">Команда также восстановит приложение всякий раз, когда вы сохраните файл в проекте.</span><span class="sxs-lookup"><span data-stu-id="0923f-180">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="0923f-181">Теперь необходимо перейти к `http://localhost:3007/myFirstAppTab/` и убедиться, что вкладка отрисовка.</span><span class="sxs-lookup"><span data-stu-id="0923f-181">You should now be go to `http://localhost:3007/myFirstAppTab/` and ensure that your tab is rendering.</span></span> <span data-ttu-id="0923f-182">Однако он еще не Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0923f-182">However, it is not in Microsoft Teams yet.</span></span> 

<span data-ttu-id="0923f-183">**Чтобы отрисовка вкладки в Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="0923f-183">**To render your tab in Microsoft Teams**</span></span>

![просмотр сайта в браузере](~/assets/yeoman-images/teams-first-app-3.png)

### <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="0923f-185">Запустите приложение в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0923f-185">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="0923f-186">Microsoft Teams не позволяет размещению приложения на локальном сайте, поэтому необходимо либо опубликовать его на общедоступный URL-адрес, либо использовать прокси-сервер, например ngrok.</span><span class="sxs-lookup"><span data-stu-id="0923f-186">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span> <span data-ttu-id="0923f-187">Хорошая новость заключается в том, что проект scaffolded имеет эту встроенную.</span><span class="sxs-lookup"><span data-stu-id="0923f-187">Good news is that the scaffolded project has this built-in.</span></span> 

<span data-ttu-id="0923f-188">**Запуск приложения в Teams**</span><span class="sxs-lookup"><span data-stu-id="0923f-188">**To run your app in Teams**</span></span>

1. <span data-ttu-id="0923f-189">Запуск `gulp ngrok-serve` в терминале.</span><span class="sxs-lookup"><span data-stu-id="0923f-189">Run `gulp ngrok-serve` in Terminal.</span></span> <span data-ttu-id="0923f-190">При запуске службы ngrok будет запущена в фоновом режиме с уникальной и открытой записью DNS, которая также будет упаковывать манифест с этим уникальным URL-адресом, а затем делать то же самое, что `gulp ngrok-serve` `gulp serve` и .</span><span class="sxs-lookup"><span data-stu-id="0923f-190">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>
1. <span data-ttu-id="0923f-191">Создайте новую команду Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0923f-191">Create a new Microsoft Teams team.</span></span>
1. <span data-ttu-id="0923f-192">Выберите имя команды > Teams Параметры > Apps.</span><span class="sxs-lookup"><span data-stu-id="0923f-192">Select the Team name > Teams Settings > Apps.</span></span>
1. <span data-ttu-id="0923f-193">В правом нижнем углу **выберите Upload настраиваемого приложения.**</span><span class="sxs-lookup"><span data-stu-id="0923f-193">From the lower right corner, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="0923f-194">Перейдите в `package` папку в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="0923f-194">Go to the `package` folder under your project folder.</span></span> 
1. <span data-ttu-id="0923f-195">Выберите почтовый файл в этой папке и откройте.</span><span class="sxs-lookup"><span data-stu-id="0923f-195">Select the zip file in that folder and select open.</span></span> 
   <span data-ttu-id="0923f-196">Ваше приложение теперь загружено в Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="0923f-196">Your App is now sideloaded into Microsoft Teams:</span></span>

   ![sideloaded app](~/assets/yeoman-images/teams-first-app-4.png)
1. <span data-ttu-id="0923f-198">Возвращайся на **общий** канал и **+** выберите, чтобы добавить новую вкладку. Вы должны видеть вкладку в списке вкладок: ![ настройка вкладки](~/assets/yeoman-images/teams-first-app-5.png)</span><span class="sxs-lookup"><span data-stu-id="0923f-198">Go back to the **General** channel and select **+** to add a new Tab. You should see your tab in the list of tabs: ![configure tab](~/assets/yeoman-images/teams-first-app-5.png)</span></span>
1. <span data-ttu-id="0923f-199">Выберите вкладку и выполните инструкции по ее добавлению.</span><span class="sxs-lookup"><span data-stu-id="0923f-199">Select your tab and follow the instructions to add it.</span></span> <span data-ttu-id="0923f-200">Обратите внимание, что у вас есть настраиваемый диалог конфигурации, для которого можно изменить источник.</span><span class="sxs-lookup"><span data-stu-id="0923f-200">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="0923f-201">Выберите *Сохранить,* чтобы добавить вкладку в канал.</span><span class="sxs-lookup"><span data-stu-id="0923f-201">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="0923f-202">Теперь вкладка загружается внутри Microsoft Teams!</span><span class="sxs-lookup"><span data-stu-id="0923f-202">Your tab is now loaded inside Microsoft Teams!</span></span>

   ![запуск вкладки в командах](~/assets/yeoman-images/teams-first-app-6.png)

### <a name="upgrade-microsoft-teams"></a><span data-ttu-id="0923f-204">Обновление Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0923f-204">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="0923f-205">Вы также можете обновить текущую версию Microsoft Teams до последней версии с помощью Microsoft Teams генератора Yeoman.</span><span class="sxs-lookup"><span data-stu-id="0923f-205">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="0923f-206">**Обновление Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="0923f-206">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="0923f-207">Получите текущую версию Teams со следующей командой:</span><span class="sxs-lookup"><span data-stu-id="0923f-207">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="0923f-208">Чтобы выбрать и обновить генератор, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0923f-208">Use the following command to select and update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="0923f-209">Используйте клавиши со стрелками, чтобы **выбрать Обновление генераторов:**</span><span class="sxs-lookup"><span data-stu-id="0923f-209">Use the  arrow keys to select **Update your Generators**:</span></span>

   ![изображение YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="0923f-211">Выберите нужный генератор из списка генераторов:</span><span class="sxs-lookup"><span data-stu-id="0923f-211">Select the generator you want from the list of generators:</span></span>
   > [!NOTE]
   > <span data-ttu-id="0923f-212">Используйте пробел для выбора или очистки выбранной Teams из доступных параметров.</span><span class="sxs-lookup"><span data-stu-id="0923f-212">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![изображение useSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="0923f-214">Для завершения установки Teams занимает несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="0923f-214">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="0923f-215">После завершения установки используйте следующую команду для проверки установленной версии:</span><span class="sxs-lookup"><span data-stu-id="0923f-215">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
 <span data-ttu-id="0923f-216">Поздравляю!</span><span class="sxs-lookup"><span data-stu-id="0923f-216">Congrats!</span></span> <span data-ttu-id="0923f-217">Вы создали и развернули первое Microsoft Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="0923f-217">You built and deployed your first Microsoft Teams app.</span></span> <span data-ttu-id="0923f-218">Вы также обновили Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0923f-218">You also upgraded Microsoft Teams.</span></span>

 ## <a name="see-also"></a><span data-ttu-id="0923f-219">См. также</span><span class="sxs-lookup"><span data-stu-id="0923f-219">See also</span></span>

* [<span data-ttu-id="0923f-220">Обзор учебников</span><span class="sxs-lookup"><span data-stu-id="0923f-220">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="0923f-221">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="0923f-221">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)