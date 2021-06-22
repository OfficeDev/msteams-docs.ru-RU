---
title: Начало работы — создайте первое Teams с помощью SPFx
author: zhenyasav
description: Узнайте, как создать настраиваемую вкладку с помощью SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 7bbbf7ae1d74a9094af5bc6ca4b3ac797ba05d5d
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037665"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a><span data-ttu-id="37694-103">Сборка и запуск первого Microsoft Teams с помощью SharePoint Framework (SPFx)</span><span class="sxs-lookup"><span data-stu-id="37694-103">Build and run your first Microsoft Teams app with SharePoint Framework (SPFx)</span></span>

<span data-ttu-id="37694-104">В этом руководстве вы создайте новое приложение Microsoft Teams в SharePoint Framework (SPFx), которое реализует простое личное приложение.</span><span class="sxs-lookup"><span data-stu-id="37694-104">In this tutorial, you will create a new Microsoft Teams app in SharePoint Framework (SPFx) that implements a simple personal app.</span></span> <span data-ttu-id="37694-105">(Личное *приложение включает* набор вкладок для индивидуального использования.) Во время руководства вы узнаете о структуре приложения Teams, локальном запуске приложения и развертывании приложения для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="37694-105">(A *personal app* includes a set of tabs scoped for individual use.) During the tutorial, you will learn about the structure of a Teams app, how to run the app locally, and how to deploy the app to SharePoint.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="37694-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="37694-106">Before you begin</span></span>

<span data-ttu-id="37694-107">Настройте среду разработки, установив [необходимые компоненты](prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="37694-107">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37694-108">Необходимые условия для установки</span><span class="sxs-lookup"><span data-stu-id="37694-108">Install prerequisites</span></span>](prerequisites.md)

## <a name="get-organized"></a><span data-ttu-id="37694-109">Упорядочьте работу</span><span class="sxs-lookup"><span data-stu-id="37694-109">Get organized</span></span>

<span data-ttu-id="37694-110">Помимо необходимых условий, необходимо также быть администратором для SharePoint веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="37694-110">In addition to the prerequisites, you also need to be an Administrator for a SharePoint Site Collection.</span></span>  <span data-ttu-id="37694-111">Здесь вы развернете приложение для размещения.</span><span class="sxs-lookup"><span data-stu-id="37694-111">This is where you will deploy your app for hosting.</span></span>  <span data-ttu-id="37694-112">Если вы используете клиента программы разработчика M365, используйте учетную запись администратора, созданную при регистрации для программы.</span><span class="sxs-lookup"><span data-stu-id="37694-112">If you are using an M365 developer program tenant, use the administrator account you set up when you registered for the program.</span></span>  

## <a name="create-your-project"></a><span data-ttu-id="37694-113">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="37694-113">Create your project</span></span>

<span data-ttu-id="37694-114">Используйте набор средств Teams для создания своего первого проекта.</span><span class="sxs-lookup"><span data-stu-id="37694-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="37694-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="37694-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="37694-116">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="37694-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="37694-117">Откройте набор средств Teams, выбрав значок Teams на боковой панели:</span><span class="sxs-lookup"><span data-stu-id="37694-117">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. <span data-ttu-id="37694-119">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="37694-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. <span data-ttu-id="37694-121">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="37694-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания нового проекта":::

1. <span data-ttu-id="37694-123">На странице **выбора возможностей** уже будет выбрана возможность **Вкладка**.</span><span class="sxs-lookup"><span data-stu-id="37694-123">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="37694-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="37694-124">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. <span data-ttu-id="37694-126">На **шаге типа** размещения Frontend выберите SharePoint Framework **(SPFx).**</span><span class="sxs-lookup"><span data-stu-id="37694-126">On the **Frontend hosting type** step, select **SharePoint Framework (SPFx)**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Снимок экрана: выбор размещения для нового приложения.":::

1. <span data-ttu-id="37694-128">На **шаге Framework** выберите **React**.</span><span class="sxs-lookup"><span data-stu-id="37694-128">On the **Framework** step, select **React**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Выбор Framework":::

1. <span data-ttu-id="37694-130">При запросе имени **Вебпарта** нажмите **кнопку Ввод,** чтобы принять по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="37694-130">When asked for a **Webpart Name**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="37694-131">При запросе **описания Вебпарта** нажмите **кнопку Ввод,** чтобы принять по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="37694-131">When asked for the **Webpart Description**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="37694-132">При запросе языка **программирования** нажмите **кнопку Ввод,** чтобы принять по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="37694-132">When asked for the **Programming Language**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="37694-133">Выберите папку рабочей области.</span><span class="sxs-lookup"><span data-stu-id="37694-133">Select a workspace folder.</span></span>  <span data-ttu-id="37694-134">В папке рабочей области будет создана папка для создаваемого проекта.</span><span class="sxs-lookup"><span data-stu-id="37694-134">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="37694-135">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="37694-135">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="37694-136">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="37694-136">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="37694-137">Чтобы продолжить, нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="37694-137">Press **Enter** to continue.</span></span>

<span data-ttu-id="37694-138">Создание приложения Teams займет несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="37694-138">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="37694-139">Командная строка</span><span class="sxs-lookup"><span data-stu-id="37694-139">Command line</span></span>](#tab/cli)

<span data-ttu-id="37694-140">Используйте для создания первого проекта интерфейс командной строки `teamsfx`.</span><span class="sxs-lookup"><span data-stu-id="37694-140">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="37694-141">Начните с папки, в которой будет создана папка проекта.</span><span class="sxs-lookup"><span data-stu-id="37694-141">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="37694-142">Интерфейс командной строки выдаст несколько вопросов, ответы на которые используются для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="37694-142">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="37694-143">Каждый вопрос сопровождается подсказкой о том, как на него отвечать (например, использовать клавиши со стрелками для выбора варианта).</span><span class="sxs-lookup"><span data-stu-id="37694-143">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="37694-144">Ответив на вопрос, подтвердите свой выбор, нажав клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="37694-144">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="37694-145">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="37694-145">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="37694-146">Выберите возможность **Вкладка**.</span><span class="sxs-lookup"><span data-stu-id="37694-146">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="37694-147">Выберите **SharePoint Framework (SPFx)** переднего размещения.</span><span class="sxs-lookup"><span data-stu-id="37694-147">Select **SharePoint Framework (SPFx)** frontend hosting.</span></span>
1. <span data-ttu-id="37694-148">Выберите **React.**</span><span class="sxs-lookup"><span data-stu-id="37694-148">Select **React** framework.</span></span>
1. <span data-ttu-id="37694-149">Нажмите **кнопку Введите** имя **Вебпарта.**</span><span class="sxs-lookup"><span data-stu-id="37694-149">Press **Enter** for the **Webpart Name**.</span></span>
1. <span data-ttu-id="37694-150">Нажмите **кнопку Ввод** для **описания Webpart**.</span><span class="sxs-lookup"><span data-stu-id="37694-150">Press **Enter** for the **Webpart Description**.</span></span>
1. <span data-ttu-id="37694-151">Нажмите **кнопку Ввод** для **языка программирования**.</span><span class="sxs-lookup"><span data-stu-id="37694-151">Press **Enter** for the **Programming Language**.</span></span>
1. <span data-ttu-id="37694-152">Нажмите клавишу **ВВОД**, чтобы выбрать папку рабочей области по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="37694-152">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="37694-153">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="37694-153">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="37694-154">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="37694-154">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="37694-155">После того, как вы ответите на все вопросы, будет создан проект.</span><span class="sxs-lookup"><span data-stu-id="37694-155">Once all the questions have been answered, your project will be created.</span></span>

---

- [<span data-ttu-id="37694-156">Узнайте больше о разработке для SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="37694-156">Learn more about developing for SharePoint Framework</span></span>](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="37694-157">Знакомство с исходным кодом</span><span class="sxs-lookup"><span data-stu-id="37694-157">Take a tour of the source code</span></span>

<span data-ttu-id="37694-158">Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="37694-158">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="37694-159">Как только Teams набор средств настраивает проект, у вас есть компоненты для создания базового личного приложения для Teams, которое находится в SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="37694-159">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams that is hosted within the SharePoint Framework.</span></span>  <span data-ttu-id="37694-160">Каталоги и файлы проекта отображаются в области проводника Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="37694-160">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Снимок экрана: файлы проектов приложения для личного приложения в Visual Studio Code.":::

<span data-ttu-id="37694-162">Набор средств автоматически формирует шаблоны в каталоге проекта на основе возможностей, добавленных во время установки.</span><span class="sxs-lookup"><span data-stu-id="37694-162">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="37694-163">Набор средств Teams сохраняет свое состояние для вашего приложения в каталоге `.fx`.</span><span class="sxs-lookup"><span data-stu-id="37694-163">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="37694-164">Среди других элементов в этом каталоге находятся:</span><span class="sxs-lookup"><span data-stu-id="37694-164">Among other items in this directory:</span></span>

- <span data-ttu-id="37694-165">Значки приложений, хранимые как PNG-файлы в `color.png` и `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="37694-165">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="37694-166">Манифест приложения для публикации на портале разработчиков для Teams хранится в `manifest.source.json` .</span><span class="sxs-lookup"><span data-stu-id="37694-166">The app manifest for publishing to Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="37694-167">Параметры, выбранные при создании проекта, хранятся в `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="37694-167">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="37694-168">Так как вы выбрали проект SPFx Webpart, к вашему пользовательскому интерфейсу имеют отношение следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="37694-168">Since you selected a SPFx Webpart project, the following files are relevant to your UI:</span></span>

- <span data-ttu-id="37694-169">Папка содержит `SPFx/src/webparts/{webpart}` веб-SPFx веб-части.</span><span class="sxs-lookup"><span data-stu-id="37694-169">The folder `SPFx/src/webparts/{webpart}` contains your SPFx webpart.</span></span>
- <span data-ttu-id="37694-170">В `.vscode/launch.json` файле описываются конфигурации отладки, доступные в палитре отладки.</span><span class="sxs-lookup"><span data-stu-id="37694-170">The file `.vscode/launch.json` describes the debugging configurations available in the debug palette.</span></span>

<span data-ttu-id="37694-171">Дополнительные сведения о веб SharePoint веб-Teams для Teams, обратитесь к документации [SharePoint.](/sharepoint/dev/spfx/build-for-teams-overview)</span><span class="sxs-lookup"><span data-stu-id="37694-171">For more information about SharePoint Webparts for Teams, [refer to the SharePoint documentation](/sharepoint/dev/spfx/build-for-teams-overview).</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="37694-172">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="37694-172">Run your app locally</span></span>

<span data-ttu-id="37694-173">Teams набор средств позволяет локализовку приложения и запуск его через [SharePoint Framework Workbench.](/sharepoint/dev/spfx/debug-in-vscode)</span><span class="sxs-lookup"><span data-stu-id="37694-173">Teams Toolkit allows you to host your app locally and run it through the [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="37694-174">Создайте и запустите приложение локально в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="37694-174">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="37694-175">Чтобы создать и запустить приложение локально, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="37694-175">To build and run your app locally:</span></span>

1. <span data-ttu-id="37694-176">С Visual Studio Code нажмите **F5**.</span><span class="sxs-lookup"><span data-stu-id="37694-176">From Visual Studio Code, press **F5**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="Снимок экрана, показывающий, как SPFx приложение в локальной работе.":::

   > [!NOTE]
   > <span data-ttu-id="37694-178">При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.</span><span class="sxs-lookup"><span data-stu-id="37694-178">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="37694-179">Окно браузера автоматически открывается и загружает SharePoint Workbench после завершения сборки.</span><span class="sxs-lookup"><span data-stu-id="37694-179">A browser window automatically opens and loads the SharePoint Workbench when the build is complete.</span></span>  <span data-ttu-id="37694-180">Для завершения может потребоваться от 3 до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="37694-180">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="37694-181">После загрузки SharePoint workbench.</span><span class="sxs-lookup"><span data-stu-id="37694-181">Once the SharePoint Workbench is loaded.</span></span>

   >[!NOTE]
   > <span data-ttu-id="37694-182">Набор средств при необходимости выведет запрос на установку локального сертификата.</span><span class="sxs-lookup"><span data-stu-id="37694-182">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="37694-183">Этот сертификат позволяет Teams загружать приложение из `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="37694-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="37694-184">Выберите "Да", когда появится следующее диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="37694-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. <span data-ttu-id="37694-186">Нажмите одну из значков **Добавить веб-часть** (+) для добавления веб-части.</span><span class="sxs-lookup"><span data-stu-id="37694-186">Press one of the **Add Webpart** (+) icons to add your webpart.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Снимок экрана, SPFx рабочийбек, запущенный с всплывающее всплывающее изображение, чтобы добавить веб-страницу с указанием.":::

1. <span data-ttu-id="37694-188">Выберите веб-сайт из меню.</span><span class="sxs-lookup"><span data-stu-id="37694-188">Choose your webpart from the menu.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Снимок экрана, SPFx рабочийбек, запущенный с всплывающее всплывающее изображение, чтобы добавить выбор веб-части.":::

<span data-ttu-id="37694-190">Теперь приложение должно быть запущено.</span><span class="sxs-lookup"><span data-stu-id="37694-190">Your app should now be running.</span></span>  <span data-ttu-id="37694-191">Вы можете делать обычные действия отладки, как если бы это были какие-либо другие веб SPFx (например, настройка точек взлома).</span><span class="sxs-lookup"><span data-stu-id="37694-191">You can do normal debugging activities as if this were any other SPFx webpart (such as setting breakpoints).</span></span>

> [!TIP]
> <span data-ttu-id="37694-192">Попробуйте разместить точки breakpoints в методе рендеринга и `SPFx/src/webparts/{webpart}/{webpart}.ts` перезагрузить окно браузера.</span><span class="sxs-lookup"><span data-stu-id="37694-192">Try placing breakpoints in the render method of `SPFx/src/webparts/{webpart}/{webpart}.ts` and reloading the browser window.</span></span> <span data-ttu-id="37694-193">VS Code остановится на точках остановок в коде.</span><span class="sxs-lookup"><span data-stu-id="37694-193">VS Code will stop on breakpoints in your code.</span></span>

## <a name="deploy-your-app-to-sharepoint"></a><span data-ttu-id="37694-194">Развертывание приложения для SharePoint</span><span class="sxs-lookup"><span data-stu-id="37694-194">Deploy your app to SharePoint</span></span>

<span data-ttu-id="37694-195">Убедитесь SharePoint каталог приложений существует в развертывании.</span><span class="sxs-lookup"><span data-stu-id="37694-195">Ensure a SharePoint App Catalog exists in your deployment.</span></span>  <span data-ttu-id="37694-196">Если его не существует, [создайте один](/sharepoint/use-app-catalog).</span><span class="sxs-lookup"><span data-stu-id="37694-196">If one does not exist, [create one](/sharepoint/use-app-catalog).</span></span>  <span data-ttu-id="37694-197">Полное создание каталога приложений может занять до 15 минут.</span><span class="sxs-lookup"><span data-stu-id="37694-197">It may take up to 15 minutes for the app catalog to be fully created.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="37694-198">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="37694-198">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="37694-199">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="37694-199">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="37694-200">Выберите Teams набор средств на боковой панели, выбрав значок Teams.</span><span class="sxs-lookup"><span data-stu-id="37694-200">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="37694-201">Выберите **Положение в облаке**.</span><span class="sxs-lookup"><span data-stu-id="37694-201">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Снимок экрана, показывающий команды по подготовкам":::

1. <span data-ttu-id="37694-203">Вы можете отслеживать ход, наблюдая за диалогами в правом нижнем углу.</span><span class="sxs-lookup"><span data-stu-id="37694-203">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="37694-204">Через несколько секунд вы увидите следующее уведомление:</span><span class="sxs-lookup"><span data-stu-id="37694-204">After a few seconds, you will see the following notice:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Снимок экрана, показывающий полный диалоговое окно подготовка.":::

1. <span data-ttu-id="37694-206">Как только подготовка завершена, выберите **Развертывание в облаке.**</span><span class="sxs-lookup"><span data-stu-id="37694-206">Once provisioning is complete, select **Deploy to the cloud**.</span></span>

1. <span data-ttu-id="37694-207">В настоящее время автоматическое развертывание не доступно.</span><span class="sxs-lookup"><span data-stu-id="37694-207">Currently, automated deployment is not available.</span></span>  <span data-ttu-id="37694-208">Диалоговое окно будет всплывающее запрос на сборку и развертывание вручную.</span><span class="sxs-lookup"><span data-stu-id="37694-208">A dialog will pop up prompting you to build and deploy manually.</span></span> <span data-ttu-id="37694-209">Пакет **сборки SharePoint.**</span><span class="sxs-lookup"><span data-stu-id="37694-209">Press **Build SharePoint Package**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="Снимок экрана для диалогового пакета Build Sharepoint Package":::

# <a name="command-line"></a>[<span data-ttu-id="37694-211">Командная строка</span><span class="sxs-lookup"><span data-stu-id="37694-211">Command line</span></span>](#tab/cli)

<span data-ttu-id="37694-212">В окне терминала:</span><span class="sxs-lookup"><span data-stu-id="37694-212">In your terminal window:</span></span>

1. <span data-ttu-id="37694-213">Запустите `teamsfx provision`.</span><span class="sxs-lookup"><span data-stu-id="37694-213">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="37694-214">Возможно, вам будет предложено войти в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="37694-214">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="37694-215">При необходимости вам будет предложено выбрать подписку Azure для использования для ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="37694-215">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="37694-216">Для размещения приложения всегда используются некоторые ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="37694-216">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="37694-217">Запустите `teamsfx deploy`.</span><span class="sxs-lookup"><span data-stu-id="37694-217">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

1. <span data-ttu-id="37694-218">При запросе выберите **пакет сборки SharePoint.**</span><span class="sxs-lookup"><span data-stu-id="37694-218">When prompted, select **Build SharePoint Package**.</span></span>

---

<span data-ttu-id="37694-219">Пакет SharePoint находится в рамках `SPFx/sharepoint/solution` проекта.</span><span class="sxs-lookup"><span data-stu-id="37694-219">The SharePoint package is located in `SPFx/sharepoint/solution` within your project.</span></span>  <span data-ttu-id="37694-220">Upload пакет для SharePoint:</span><span class="sxs-lookup"><span data-stu-id="37694-220">Upload the package to SharePoint:</span></span>

1. <span data-ttu-id="37694-221">Войдите в консоль администратора M365, а затем перейдите в каталог SharePoint приложений.</span><span class="sxs-lookup"><span data-stu-id="37694-221">Log into the M365 Admin Console, then navigate to the SharePoint App Catalog.</span></span>

   - <span data-ttu-id="37694-222">Откройте `https://admin.microsoft.com/AdminPortal/Home` .</span><span class="sxs-lookup"><span data-stu-id="37694-222">Open `https://admin.microsoft.com/AdminPortal/Home`.</span></span>
   - <span data-ttu-id="37694-223">В **центрах администрирования** выберите **SharePoint** центр администрирования.</span><span class="sxs-lookup"><span data-stu-id="37694-223">Under **Admin centers**, select the **SharePoint** admin center.</span></span>
   - <span data-ttu-id="37694-224">Выберите **дополнительные функции** из меню боковой панели.</span><span class="sxs-lookup"><span data-stu-id="37694-224">Select **More features** from the sidebar menu.</span></span>
   - <span data-ttu-id="37694-225">Нажмите **кнопку Открыть** в **приложениях**.</span><span class="sxs-lookup"><span data-stu-id="37694-225">Press **Open** under **Apps**.</span></span>
   - <span data-ttu-id="37694-226">Щелкните **Каталог приложений**.</span><span class="sxs-lookup"><span data-stu-id="37694-226">Select **App Catalog**.</span></span>

1. <span data-ttu-id="37694-227">Выберите **Распределить приложения для SharePoint.**</span><span class="sxs-lookup"><span data-stu-id="37694-227">Select **Distribute apps for SharePoint**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="Распространение приложений для SharePoint.":::

1. <span data-ttu-id="37694-229">Выберите **Upload**.</span><span class="sxs-lookup"><span data-stu-id="37694-229">Select **Upload**.</span></span>

1. <span data-ttu-id="37694-230">Нажмите **кнопку Выберите файл**.</span><span class="sxs-lookup"><span data-stu-id="37694-230">Press **Choose File**.</span></span>

1. <span data-ttu-id="37694-231">Найдите `{project}.sppkg` файл, расположенный в `SPFx/sharepoint/solution` папке в проекте.</span><span class="sxs-lookup"><span data-stu-id="37694-231">Locate your `{project}.sppkg` file, located in the `SPFx/sharepoint/solution` folder within your project.</span></span>  <span data-ttu-id="37694-232">Нажмите **кнопку Открыть**.</span><span class="sxs-lookup"><span data-stu-id="37694-232">Press **Open**.</span></span>

1. <span data-ttu-id="37694-233">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="37694-233">Press **OK**.</span></span>

1. <span data-ttu-id="37694-234">Автоматически SharePoint развертывания.</span><span class="sxs-lookup"><span data-stu-id="37694-234">The SharePoint deployment process will automatically start.</span></span>  <span data-ttu-id="37694-235">**Убедитесь, что это решение доступно для всех сайтов** в организации проверяется, а затем нажмите **кнопку Развертывание**.</span><span class="sxs-lookup"><span data-stu-id="37694-235">Ensure **Make this solution available to all sites in the organization** is checked, then press **Deploy**.</span></span>

1. <span data-ttu-id="37694-236">Выберите **вкладку FILES.**</span><span class="sxs-lookup"><span data-stu-id="37694-236">Select the **FILES** tab.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="Выберите вкладку файлы в каталоге SharePoint приложения.":::

1. <span data-ttu-id="37694-238">выберите развернутый пакет, затем нажмите синхронизацию Teams **в** ленте.</span><span class="sxs-lookup"><span data-stu-id="37694-238">select the package you deployed, then press **Sync to Teams** in the ribbon.</span></span>

    > [!Note]
    > <span data-ttu-id="37694-239">Процесс синхронизации Teams может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="37694-239">The Sync to Teams process can take a couple of minutes.</span></span>  <span data-ttu-id="37694-240">В правой части браузера вы увидите сообщение, указывающее, что приложение успешно синхронизируется с Teams.</span><span class="sxs-lookup"><span data-stu-id="37694-240">You will see a message on the right-hand side of the browser indicating that the app has successfully synchronized to Teams.</span></span>

<span data-ttu-id="37694-241">Откройте приложение Teams (или во `https://teams.microsoft.com` входе).</span><span class="sxs-lookup"><span data-stu-id="37694-241">Open the Teams application (or sign in at `https://teams.microsoft.com`).</span></span>  <span data-ttu-id="37694-242">Нажмите тройную точку на боковую панель, а затем выберите **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="37694-242">Press the triple-dot on the sidebar, then select **All apps**.</span></span>  <span data-ttu-id="37694-243">Приложение будет размещено в **приложениях, построенных для вашей категории org.**</span><span class="sxs-lookup"><span data-stu-id="37694-243">The app will be placed in the **Apps built for your org** category.</span></span>  <span data-ttu-id="37694-244">Вы можете добавить приложение оттуда.</span><span class="sxs-lookup"><span data-stu-id="37694-244">You can add the app from there.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="Снимок экрана, показывающий приложение в Teams":::

## <a name="see-also"></a><span data-ttu-id="37694-246">См. также</span><span class="sxs-lookup"><span data-stu-id="37694-246">See also</span></span>

- [<span data-ttu-id="37694-247">Создание приложения Teams с помощью React</span><span class="sxs-lookup"><span data-stu-id="37694-247">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="37694-248">Создание приложения Teams с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="37694-248">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- [<span data-ttu-id="37694-249">Создание расширения для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="37694-249">Create a messaging extension</span></span>](first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="37694-250">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="37694-250">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37694-251">Создание бота беседы</span><span class="sxs-lookup"><span data-stu-id="37694-251">Create a conversational bot app</span></span>](first-app-bot.md)
