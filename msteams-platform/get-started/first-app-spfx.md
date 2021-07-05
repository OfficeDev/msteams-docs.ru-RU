---
title: Начало работы — создайте первое Teams с помощью SPFx
author: zhenyasav
description: Узнайте, как создать настраиваемую вкладку с помощью SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 4df2bb71837af520a2d2500a45b8605e5fae08b2
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254225"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a><span data-ttu-id="00d0c-103">Сборка и запуск первого Microsoft Teams с помощью SharePoint Framework (SPFx)</span><span class="sxs-lookup"><span data-stu-id="00d0c-103">Build and run your first Microsoft Teams app with SharePoint Framework (SPFx)</span></span>

<span data-ttu-id="00d0c-104">В этом руководстве вы узнаете, как создать новое приложение Microsoft Teams в SharePoint Framework SPFx, которое реализует простое личное приложение.</span><span class="sxs-lookup"><span data-stu-id="00d0c-104">In this tutorial, you will learn how to create a new Microsoft Teams app in SharePoint Framework SPFx that implements a simple personal app.</span></span> <span data-ttu-id="00d0c-105">Например, личное *приложение включает* набор вкладок для индивидуального использования.</span><span class="sxs-lookup"><span data-stu-id="00d0c-105">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="00d0c-106">Во время руководства вы узнаете о структуре приложения Teams, локальном запуске приложения и развертывании приложения для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="00d0c-106">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to SharePoint.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="00d0c-107">Подготовка</span><span class="sxs-lookup"><span data-stu-id="00d0c-107">Before you begin</span></span>

<span data-ttu-id="00d0c-108">Убедитесь, что среда разработки настроена путем установки необходимых условий.</span><span class="sxs-lookup"><span data-stu-id="00d0c-108">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="00d0c-109">Необходимые условия для установки</span><span class="sxs-lookup"><span data-stu-id="00d0c-109">Install prerequisites</span></span>](prerequisites.md)

## <a name="get-organized"></a><span data-ttu-id="00d0c-110">Упорядочьте работу</span><span class="sxs-lookup"><span data-stu-id="00d0c-110">Get organized</span></span>

<span data-ttu-id="00d0c-111">Помимо необходимых условий, необходимо также быть администратором для SharePoint веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="00d0c-111">In addition to the prerequisites, you also need to be an Administrator for a SharePoint Site Collection.</span></span>  <span data-ttu-id="00d0c-112">Здесь вы развернете приложение для размещения.</span><span class="sxs-lookup"><span data-stu-id="00d0c-112">This is where you will deploy your app for hosting.</span></span>  <span data-ttu-id="00d0c-113">Если вы используете клиента программы разработчика M365, используйте учетную запись администратора, созданную при регистрации для программы.</span><span class="sxs-lookup"><span data-stu-id="00d0c-113">If you are using an M365 developer program tenant, use the administrator account you set up when you registered for the program.</span></span>  

## <a name="create-your-project"></a><span data-ttu-id="00d0c-114">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="00d0c-114">Create your project</span></span>

<span data-ttu-id="00d0c-115">Используйте набор средств Teams для создания своего первого проекта.</span><span class="sxs-lookup"><span data-stu-id="00d0c-115">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="00d0c-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="00d0c-116">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="00d0c-117">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="00d0c-117">Open Visual Studio code.</span></span>
1. <span data-ttu-id="00d0c-118">Выберите значок Teams на боковой панели, чтобы открыть Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="00d0c-118">Select the Teams icon in the sidebar to open the Teams Toolkit.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. <span data-ttu-id="00d0c-120">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-120">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. <span data-ttu-id="00d0c-122">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-122">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания проекта":::

1. <span data-ttu-id="00d0c-124">В разделе **Выбор возможностей** выберите **вкладку и** выберите **ОК.**</span><span class="sxs-lookup"><span data-stu-id="00d0c-124">In the **Select capabilities** section, select **Tab** and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. <span data-ttu-id="00d0c-126">В разделе **Тип типа хостинга Frontend** выберите SharePoint Framework **(SPFx).**</span><span class="sxs-lookup"><span data-stu-id="00d0c-126">In the **Frontend hosting type** section, select **SharePoint Framework (SPFx)**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Снимок экрана: выбор размещения для нового приложения.":::

1. <span data-ttu-id="00d0c-128">В разделе **Framework** выберите **React**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-128">In the **Framework** section, select **React**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Выбор Framework":::

1. <span data-ttu-id="00d0c-130">При запросе имени **Вебпарта** нажмите **кнопку Ввод,** чтобы принять по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="00d0c-130">When asked for a **Webpart Name**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="00d0c-131">При запросе **описания Вебпарта** нажмите **кнопку Ввод,** чтобы принять по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="00d0c-131">When asked for the **Webpart Description**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="00d0c-132">При запросе языка **программирования** нажмите **кнопку Ввод,** чтобы принять по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="00d0c-132">When asked for the **Programming Language**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="00d0c-133">Выберите папку рабочей области.</span><span class="sxs-lookup"><span data-stu-id="00d0c-133">Select a workspace folder.</span></span>  <span data-ttu-id="00d0c-134">В папке рабочей области будет создана папка для создаваемого проекта.</span><span class="sxs-lookup"><span data-stu-id="00d0c-134">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="00d0c-135">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="00d0c-135">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="00d0c-136">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="00d0c-136">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="00d0c-137">Чтобы продолжить, нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-137">Press **Enter** to continue.</span></span>

   <span data-ttu-id="00d0c-138">Создание приложения Teams займет несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="00d0c-138">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="00d0c-139">Командная строка</span><span class="sxs-lookup"><span data-stu-id="00d0c-139">Command line</span></span>](#tab/cli)

<span data-ttu-id="00d0c-140">Используйте для создания первого проекта интерфейс командной строки `teamsfx`.</span><span class="sxs-lookup"><span data-stu-id="00d0c-140">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="00d0c-141">Начните с папки, в которой будет создана папка проекта.</span><span class="sxs-lookup"><span data-stu-id="00d0c-141">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="00d0c-142">Интерфейс командной строки выдаст несколько вопросов, ответы на которые используются для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="00d0c-142">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="00d0c-143">Каждый вопрос сопровождается подсказкой о том, как на него отвечать (например, использовать клавиши со стрелками для выбора варианта).</span><span class="sxs-lookup"><span data-stu-id="00d0c-143">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="00d0c-144">Ответив на вопрос, подтвердите свой выбор, нажав клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-144">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="00d0c-145">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-145">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="00d0c-146">Выберите **вкладку**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-146">Select **Tab**.</span></span>
1. <span data-ttu-id="00d0c-147">Выберите **SharePoint Framework (SPFx)** переднего размещения.</span><span class="sxs-lookup"><span data-stu-id="00d0c-147">Select **SharePoint Framework (SPFx)** frontend hosting.</span></span>
1. <span data-ttu-id="00d0c-148">Выберите **React.**</span><span class="sxs-lookup"><span data-stu-id="00d0c-148">Select **React** framework.</span></span>
1. <span data-ttu-id="00d0c-149">Нажмите **кнопку Введите** имя **Вебпарта.**</span><span class="sxs-lookup"><span data-stu-id="00d0c-149">Press **Enter** for the **Webpart Name**.</span></span>
1. <span data-ttu-id="00d0c-150">Нажмите **кнопку Ввод** для **описания Webpart**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-150">Press **Enter** for the **Webpart Description**.</span></span>
1. <span data-ttu-id="00d0c-151">Нажмите **кнопку Ввод** для **языка программирования**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-151">Press **Enter** for the **Programming Language**.</span></span>
1. <span data-ttu-id="00d0c-152">Нажмите клавишу **ВВОД**, чтобы выбрать папку рабочей области по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="00d0c-152">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="00d0c-153">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="00d0c-153">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="00d0c-154">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="00d0c-154">The name of the app must consist only of alphanumeric characters.</span></span>

   <span data-ttu-id="00d0c-155">После ответа на все вопросы будет создан проект.</span><span class="sxs-lookup"><span data-stu-id="00d0c-155">After all the questions have been answered, your project will be created.</span></span>

---

- [<span data-ttu-id="00d0c-156">Узнайте больше о разработке для SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="00d0c-156">Learn more about developing for SharePoint Framework</span></span>](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="00d0c-157">Знакомство с исходным кодом</span><span class="sxs-lookup"><span data-stu-id="00d0c-157">Take a tour of the source code</span></span>

<span data-ttu-id="00d0c-158">Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="00d0c-158">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="00d0c-159">После настройки Teams набор средств проекта у вас есть компоненты для создания базового личного приложения для Teams, которое находится в SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="00d0c-159">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams that is hosted within the SharePoint Framework.</span></span>  <span data-ttu-id="00d0c-160">Каталоги и файлы проекта отображаются в области проводника Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="00d0c-160">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Снимок экрана: файлы проектов приложения для личного приложения в Visual Studio Code.":::

<span data-ttu-id="00d0c-162">Набор средств автоматически формирует шаблоны в каталоге проекта на основе возможностей, добавленных во время установки.</span><span class="sxs-lookup"><span data-stu-id="00d0c-162">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="00d0c-163">Набор средств Teams сохраняет свое состояние для вашего приложения в каталоге `.fx`.</span><span class="sxs-lookup"><span data-stu-id="00d0c-163">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="00d0c-164">Среди других элементов в этом каталоге находятся:</span><span class="sxs-lookup"><span data-stu-id="00d0c-164">Among other items in this directory:</span></span>

- <span data-ttu-id="00d0c-165">Значки приложений, хранимые как PNG-файлы в `color.png` и `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="00d0c-165">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="00d0c-166">Манифест приложения для публикации на портале разработчиков для Teams хранится в `manifest.source.json` .</span><span class="sxs-lookup"><span data-stu-id="00d0c-166">The app manifest for publishing to Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="00d0c-167">Параметры, выбранные при создании проекта, хранятся в `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="00d0c-167">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="00d0c-168">Так как вы выбрали проект SPFx Webpart, к вашему пользовательскому интерфейсу имеют отношение следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="00d0c-168">Since you selected a SPFx Webpart project, the following files are relevant to your UI:</span></span>

- <span data-ttu-id="00d0c-169">Папка содержит `SPFx/src/webparts/{webpart}` веб-SPFx веб-части.</span><span class="sxs-lookup"><span data-stu-id="00d0c-169">The folder `SPFx/src/webparts/{webpart}` contains your SPFx webpart.</span></span>
- <span data-ttu-id="00d0c-170">В `.vscode/launch.json` файле описываются конфигурации отладки, доступные в палитре отладки.</span><span class="sxs-lookup"><span data-stu-id="00d0c-170">The file `.vscode/launch.json` describes the debugging configurations available in the debug palette.</span></span>

<span data-ttu-id="00d0c-171">Дополнительные сведения о веб SharePoint веб-Teams для Teams, обратитесь к документации [SharePoint.](/sharepoint/dev/spfx/build-for-teams-overview)</span><span class="sxs-lookup"><span data-stu-id="00d0c-171">For more information about SharePoint Webparts for Teams, [refer to the SharePoint documentation](/sharepoint/dev/spfx/build-for-teams-overview).</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="00d0c-172">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="00d0c-172">Run your app locally</span></span>

<span data-ttu-id="00d0c-173">Teams набор средств позволяет локализовку приложения и запуск его через [SharePoint Framework Workbench.](/sharepoint/dev/spfx/debug-in-vscode)</span><span class="sxs-lookup"><span data-stu-id="00d0c-173">Teams Toolkit allows you to host your app locally and run it through the [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="00d0c-174">Создайте и запустите приложение локально в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="00d0c-174">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="00d0c-175">Чтобы создать и запустить приложение локально, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="00d0c-175">To build and run your app locally:</span></span>

1. <span data-ttu-id="00d0c-176">С Visual Studio Code нажмите **клавишу F5.**</span><span class="sxs-lookup"><span data-stu-id="00d0c-176">From Visual Studio Code, press the **F5** key.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="Снимок экрана, показывающий, как SPFx приложение в локальной работе.":::

   > [!NOTE]
   > <span data-ttu-id="00d0c-178">При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.</span><span class="sxs-lookup"><span data-stu-id="00d0c-178">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="00d0c-179">Окно браузера автоматически открывается и загружает SharePoint Workbench после завершения сборки.</span><span class="sxs-lookup"><span data-stu-id="00d0c-179">A browser window automatically opens and loads the SharePoint Workbench when the build is complete.</span></span>  <span data-ttu-id="00d0c-180">Для завершения может потребоваться от 3 до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="00d0c-180">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="00d0c-181">После загрузки SharePoint workbench.</span><span class="sxs-lookup"><span data-stu-id="00d0c-181">After the SharePoint Workbench is loaded.</span></span>

   >[!NOTE]
   > <span data-ttu-id="00d0c-182">Набор средств при необходимости выведет запрос на установку локального сертификата.</span><span class="sxs-lookup"><span data-stu-id="00d0c-182">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="00d0c-183">Этот сертификат позволяет Teams загружать приложение из `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="00d0c-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="00d0c-184">Выберите "Да", когда появится следующее диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="00d0c-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. <span data-ttu-id="00d0c-186">Выберите **Добавить значки Webpart +** для добавления веб-части.</span><span class="sxs-lookup"><span data-stu-id="00d0c-186">Select **Add Webpart +** icons to add your webpart.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Снимок экрана, SPFx рабочийбек, запущенный с всплывающее всплывающее изображение, чтобы добавить веб-страницу с указанием.":::

1. <span data-ttu-id="00d0c-188">Выберите веб-сайт из меню.</span><span class="sxs-lookup"><span data-stu-id="00d0c-188">Select your webpart from the menu.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Снимок экрана, SPFx рабочийбек, запущенный с всплывающее всплывающее изображение, чтобы добавить выбор веб-части.":::

   <span data-ttu-id="00d0c-190">Теперь приложение должно быть запущено.</span><span class="sxs-lookup"><span data-stu-id="00d0c-190">Your app should now be running.</span></span>  <span data-ttu-id="00d0c-191">Вы можете делать обычные действия отладки, как если бы это были какие-либо другие веб SPFx (например, настройка точек взлома).</span><span class="sxs-lookup"><span data-stu-id="00d0c-191">You can do normal debugging activities as if this were any other SPFx webpart (such as setting breakpoints).</span></span>

   > [!TIP]
   > <span data-ttu-id="00d0c-192">Попробуйте разместить точки breakpoints в методе рендеринга и `SPFx/src/webparts/{webpart}/{webpart}.ts` перезагрузить окно браузера.</span><span class="sxs-lookup"><span data-stu-id="00d0c-192">Try placing breakpoints in the render method of `SPFx/src/webparts/{webpart}/{webpart}.ts` and reloading the browser window.</span></span> <span data-ttu-id="00d0c-193">VS Code остановится на точках остановок в коде.</span><span class="sxs-lookup"><span data-stu-id="00d0c-193">VS Code will stop on breakpoints in your code.</span></span>

## <a name="deploy-your-app-to-sharepoint"></a><span data-ttu-id="00d0c-194">Развертывание приложения для SharePoint</span><span class="sxs-lookup"><span data-stu-id="00d0c-194">Deploy your app to SharePoint</span></span>

<span data-ttu-id="00d0c-195">Убедитесь SharePoint каталог приложений существует в развертывании.</span><span class="sxs-lookup"><span data-stu-id="00d0c-195">Ensure a SharePoint App Catalog exists in your deployment.</span></span>  <span data-ttu-id="00d0c-196">Если его не существует, [создайте один](/sharepoint/use-app-catalog).</span><span class="sxs-lookup"><span data-stu-id="00d0c-196">If one does not exist, [create one](/sharepoint/use-app-catalog).</span></span>  <span data-ttu-id="00d0c-197">Полное создание каталога приложений может занять до 15 минут.</span><span class="sxs-lookup"><span data-stu-id="00d0c-197">It may take up to 15 minutes for the app catalog to be fully created.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="00d0c-198">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="00d0c-198">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="00d0c-199">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="00d0c-199">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="00d0c-200">Выберите Teams набор средств на боковой панели, выбрав значок Teams.</span><span class="sxs-lookup"><span data-stu-id="00d0c-200">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="00d0c-201">Выберите **Положение в облаке**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-201">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Снимок экрана, показывающий команды по подготовкам":::

   <span data-ttu-id="00d0c-203">Вы можете отслеживать ход, наблюдая за диалогами в правом нижнем углу.</span><span class="sxs-lookup"><span data-stu-id="00d0c-203">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="00d0c-204">Через несколько секунд вы увидите следующее уведомление:</span><span class="sxs-lookup"><span data-stu-id="00d0c-204">After a few seconds, you will see the following notice:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Снимок экрана, показывающий полный диалоговое окно подготовка.":::

1. <span data-ttu-id="00d0c-206">После завершения подготовка выберите **Развертывание в облаке.**</span><span class="sxs-lookup"><span data-stu-id="00d0c-206">After provisioning is complete, select **Deploy to the cloud**.</span></span>

1. <span data-ttu-id="00d0c-207">В настоящее время автоматическое развертывание не доступно.</span><span class="sxs-lookup"><span data-stu-id="00d0c-207">Currently, automated deployment is not available.</span></span>  <span data-ttu-id="00d0c-208">Диалоговое окно будет всплывающее запрос на сборку и развертывание вручную.</span><span class="sxs-lookup"><span data-stu-id="00d0c-208">A dialog will pop up prompting you to build and deploy manually.</span></span> <span data-ttu-id="00d0c-209">Выберите **пакет SharePoint сборки.**</span><span class="sxs-lookup"><span data-stu-id="00d0c-209">Select **Build SharePoint Package**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="Снимок экрана для диалогового пакета Build Sharepoint Package":::

# <a name="command-line"></a>[<span data-ttu-id="00d0c-211">Командная строка</span><span class="sxs-lookup"><span data-stu-id="00d0c-211">Command line</span></span>](#tab/cli)

<span data-ttu-id="00d0c-212">В окне терминала:</span><span class="sxs-lookup"><span data-stu-id="00d0c-212">In your terminal window:</span></span>

1. <span data-ttu-id="00d0c-213">Запустите `teamsfx provision`.</span><span class="sxs-lookup"><span data-stu-id="00d0c-213">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="00d0c-214">Возможно, вам будет предложено войти в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="00d0c-214">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="00d0c-215">При необходимости вам будет предложено выбрать подписку Azure для использования для ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="00d0c-215">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="00d0c-216">Для размещения приложения всегда используются некоторые ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="00d0c-216">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="00d0c-217">Запустите `teamsfx deploy`.</span><span class="sxs-lookup"><span data-stu-id="00d0c-217">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

1. <span data-ttu-id="00d0c-218">При запросе выберите **пакет сборки SharePoint.**</span><span class="sxs-lookup"><span data-stu-id="00d0c-218">When prompted, select **Build SharePoint Package**.</span></span>

---

<span data-ttu-id="00d0c-219">Пакет SharePoint находится в рамках `SPFx/sharepoint/solution` проекта.</span><span class="sxs-lookup"><span data-stu-id="00d0c-219">The SharePoint package is located in `SPFx/sharepoint/solution` within your project.</span></span>  <span data-ttu-id="00d0c-220">Upload пакет для SharePoint:</span><span class="sxs-lookup"><span data-stu-id="00d0c-220">Upload the package to SharePoint:</span></span>

1. <span data-ttu-id="00d0c-221">Войдите в консоль администратора M365, а затем перейдите в каталог SharePoint приложений.</span><span class="sxs-lookup"><span data-stu-id="00d0c-221">Log into the M365 Admin Console, then navigate to the SharePoint App Catalog.</span></span>

   1. <span data-ttu-id="00d0c-222">Откройте `https://admin.microsoft.com/AdminPortal/Home` .</span><span class="sxs-lookup"><span data-stu-id="00d0c-222">Open `https://admin.microsoft.com/AdminPortal/Home`.</span></span>
   1. <span data-ttu-id="00d0c-223">В **центрах администрирования** выберите **SharePoint** центр администрирования.</span><span class="sxs-lookup"><span data-stu-id="00d0c-223">Under **Admin centers**, select the **SharePoint** admin center.</span></span>
   1. <span data-ttu-id="00d0c-224">Выберите **дополнительные функции** из меню боковой панели.</span><span class="sxs-lookup"><span data-stu-id="00d0c-224">Select **More features** from the sidebar menu.</span></span>
   1. <span data-ttu-id="00d0c-225">Нажмите **кнопку Открыть** в **приложениях**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-225">Press **Open** under **Apps**.</span></span>
   1. <span data-ttu-id="00d0c-226">Щелкните **Каталог приложений**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-226">Select **App Catalog**.</span></span>

1. <span data-ttu-id="00d0c-227">Выберите **Распределить приложения для SharePoint.**</span><span class="sxs-lookup"><span data-stu-id="00d0c-227">Select **Distribute apps for SharePoint**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="Распространение приложений для SharePoint.":::

1. <span data-ttu-id="00d0c-229">Выберите **Upload**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-229">Select **Upload**.</span></span>

1. <span data-ttu-id="00d0c-230">Выберите **выберите файл**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-230">Select **Choose File**.</span></span>

1. <span data-ttu-id="00d0c-231">Найдите `{project}.sppkg` файл в `SPFx/sharepoint/solution` папке в проекте.</span><span class="sxs-lookup"><span data-stu-id="00d0c-231">Locate your `{project}.sppkg` file in the `SPFx/sharepoint/solution` folder within your project.</span></span> <span data-ttu-id="00d0c-232">Выберите **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-232">Select **Open**.</span></span>

1. <span data-ttu-id="00d0c-233">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-233">Select **OK**.</span></span>

1. <span data-ttu-id="00d0c-234">Автоматически SharePoint развертывания.</span><span class="sxs-lookup"><span data-stu-id="00d0c-234">The SharePoint deployment process will automatically start.</span></span> <span data-ttu-id="00d0c-235">**Убедитесь, что это решение доступно всем сайтам** организации.</span><span class="sxs-lookup"><span data-stu-id="00d0c-235">Verify that **Make this solution available to all sites in the organization** is selected.</span></span> <span data-ttu-id="00d0c-236">Затем выберите **Развертывание.**</span><span class="sxs-lookup"><span data-stu-id="00d0c-236">Then select **Deploy**.</span></span>

1. <span data-ttu-id="00d0c-237">Выберите **вкладку FILES.**</span><span class="sxs-lookup"><span data-stu-id="00d0c-237">Select the **FILES** tab.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="Выберите вкладку файлы в каталоге SharePoint приложения.":::

1. <span data-ttu-id="00d0c-239">выберите развернутый пакет, а затем Teams **синхронизацию** с верхним правом углу.</span><span class="sxs-lookup"><span data-stu-id="00d0c-239">select the package you deployed, then select **Sync to Teams** from the upper right corner.</span></span>

    > [!Note]
    > <span data-ttu-id="00d0c-240">Процесс синхронизации Teams может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="00d0c-240">The Sync to Teams process can take a couple of minutes.</span></span>  <span data-ttu-id="00d0c-241">В правой части браузера вы увидите сообщение, указывающее, что приложение успешно синхронизируется с Teams.</span><span class="sxs-lookup"><span data-stu-id="00d0c-241">You will see a message on the right-hand side of the browser indicating that the app has successfully synchronized to Teams.</span></span>

   <span data-ttu-id="00d0c-242">Откройте приложение Teams (или во `https://teams.microsoft.com` входе).</span><span class="sxs-lookup"><span data-stu-id="00d0c-242">Open the Teams application (or sign in at `https://teams.microsoft.com`).</span></span>  <span data-ttu-id="00d0c-243">Нажмите тройную точку на боковую панель, а затем выберите **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="00d0c-243">Press the triple-dot on the sidebar, then select **All apps**.</span></span>  <span data-ttu-id="00d0c-244">Приложение будет размещено в **приложениях, построенных для вашей категории org.**</span><span class="sxs-lookup"><span data-stu-id="00d0c-244">The app will be placed in the **Apps built for your org** category.</span></span>  <span data-ttu-id="00d0c-245">Вы можете добавить приложение оттуда.</span><span class="sxs-lookup"><span data-stu-id="00d0c-245">You can add the app from there.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="Снимок экрана, показывающий приложение в Teams":::

## <a name="see-also"></a><span data-ttu-id="00d0c-247">См. также</span><span class="sxs-lookup"><span data-stu-id="00d0c-247">See also</span></span>

* [<span data-ttu-id="00d0c-248">Обзор учебников</span><span class="sxs-lookup"><span data-stu-id="00d0c-248">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="00d0c-249">Создание бота беседы</span><span class="sxs-lookup"><span data-stu-id="00d0c-249">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="00d0c-250">Создание расширения для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="00d0c-250">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="00d0c-251">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="00d0c-251">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
