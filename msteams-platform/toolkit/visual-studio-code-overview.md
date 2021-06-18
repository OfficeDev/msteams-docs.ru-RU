---
title: Создание приложений с помощью кода Microsoft Teams набор средств и Visual Studio
description: Начало создания больших пользовательских приложений непосредственно в Visual Studio с microsoft Teams набор средств
keywords: команда визуальный набор кода студии
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: b2cfab5cb2ea2d727608b6ea3bbfec3271b2b039
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994142"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="21d82-104">Создание приложений с кодом Teams набор средств и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21d82-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="21d82-105">Код Teams набор средств для Visual Studio помогает разработчикам создавать и развертывать приложения Teams с интегрированным удостоверением, доступом к облачному хранилище, данным Microsoft Graph и другим службам в Azure и M365 с подходом "нулевой конфигурации" к опыту разработчика.</span><span class="sxs-lookup"><span data-stu-id="21d82-105">The Teams Toolkit for Visual Studio Code helps developers create and deploy Teams apps with integrated identity, access to cloud storage, data from Microsoft Graph, and other services in Azure and M365 with a “zero-configuration” approach to the developer experience.</span></span>  

<span data-ttu-id="21d82-106">Вы также можете использовать набор инструментов с Visual Studio или как CLI `teamsfx` (называется).</span><span class="sxs-lookup"><span data-stu-id="21d82-106">You also can use the toolkit with Visual Studio or as a CLI (called `teamsfx`).</span></span>

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="21d82-107">Установка команд набор средств для Visual Studio кода</span><span class="sxs-lookup"><span data-stu-id="21d82-107">Install the Teams Toolkit for Visual Studio Code</span></span>

1. <span data-ttu-id="21d82-108">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="21d82-108">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="21d82-109">Выберите представление Расширения **(Ctrl+Shift+X**  /  **⌘⇧-X** или **> расширения).**</span><span class="sxs-lookup"><span data-stu-id="21d82-109">Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="21d82-110">В поле поиска введите _Teams набор средств_.</span><span class="sxs-lookup"><span data-stu-id="21d82-110">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="21d82-111">Выберите на зеленой кнопке установки рядом с командой набор средств.</span><span class="sxs-lookup"><span data-stu-id="21d82-111">Select on the green install button next to the Teams Toolkit.</span></span>

<span data-ttu-id="21d82-112">Вы также можете найти командные набор средств на Visual Studio [Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span><span class="sxs-lookup"><span data-stu-id="21d82-112">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="21d82-113">Следующие средства устанавливаются расширением Visual Studio кода при необходимости.</span><span class="sxs-lookup"><span data-stu-id="21d82-113">The following tools are installed by the Visual Studio Code extension when they are needed.</span></span> <span data-ttu-id="21d82-114">Если уже установлено, вместо нее используется установленная версия.</span><span class="sxs-lookup"><span data-stu-id="21d82-114">If already installed, the installed version is used instead.</span></span> <span data-ttu-id="21d82-115">Если используется Linux (в том числе WSL), необходимо установить эти средства перед использованием:</span><span class="sxs-lookup"><span data-stu-id="21d82-115">If using Linux (including WSL), you must install these tools before use:</span></span>

- [<span data-ttu-id="21d82-116">Основные средства Azure Functions</span><span class="sxs-lookup"><span data-stu-id="21d82-116">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="21d82-117">Основные средства Azure Functions используются для локального запуска отлаженных компонентов, включая помощников проверки подлинности, необходимых при запуске служб в Azure.</span><span class="sxs-lookup"><span data-stu-id="21d82-117">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span> <span data-ttu-id="21d82-118">Он устанавливается в каталоге проекта с помощью `devDependencies` npm.</span><span class="sxs-lookup"><span data-stu-id="21d82-118">It is installed within the project directory using the npm `devDependencies`.</span></span>

- [<span data-ttu-id="21d82-119">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="21d82-119">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="21d82-120">SDK .NET используется для установки настраиваемых привязки для локального отладки и развертывания приложений Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="21d82-120">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span> <span data-ttu-id="21d82-121">Если во всем мире не установленА SDK .NET 3.1 или более поздней версии, установлена портативная версия.</span><span class="sxs-lookup"><span data-stu-id="21d82-121">If you have not installed the .NET 3.1 or later SDK globally, the portable version is installed.</span></span>

- [<span data-ttu-id="21d82-122">ngrok</span><span class="sxs-lookup"><span data-stu-id="21d82-122">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="21d82-123">Некоторые функции приложения Teams (беседующие боты, расширения обмена сообщениями и входящие веб-окки) требуют входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="21d82-123">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span>  <span data-ttu-id="21d82-124">Вам необходимо выставить систему разработки в Teams через туннель.</span><span class="sxs-lookup"><span data-stu-id="21d82-124">You need to expose your development system to Teams through a tunnel.</span></span> <span data-ttu-id="21d82-125">Туннель не требуется для приложений, которые включают только вкладки.</span><span class="sxs-lookup"><span data-stu-id="21d82-125">A tunnel is not required for apps that only include tabs.</span></span>  <span data-ttu-id="21d82-126">Этот пакет устанавливается в каталоге проекта (с помощью `devDependencies` npm).</span><span class="sxs-lookup"><span data-stu-id="21d82-126">This package is installed within the project directory (using npm `devDependencies`).</span></span>

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="21d82-127">Используйте командные набор средств для Visual Studio кода</span><span class="sxs-lookup"><span data-stu-id="21d82-127">Use the Teams Toolkit for Visual Studio Code</span></span>

- [<span data-ttu-id="21d82-128">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="21d82-128">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="21d82-129">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="21d82-129">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="21d82-130">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="21d82-130">Run your app locally</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="21d82-131">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="21d82-131">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="21d82-132">Настройка нового проекта Teams</span><span class="sxs-lookup"><span data-stu-id="21d82-132">Set up a new Teams project</span></span>

<span data-ttu-id="21d82-133">Teams набор средств приложения React, которые находятся в веб-частях Azure или SPFx, которые находятся в среде M365 SharePoint.</span><span class="sxs-lookup"><span data-stu-id="21d82-133">The Teams Toolkit can create React apps that are hosted in Azure or SPFx web parts that are hosted on your M365 SharePoint environment.</span></span> <span data-ttu-id="21d82-134">Чтобы создать новое приложение React, которое будет организовано в Azure:</span><span class="sxs-lookup"><span data-stu-id="21d82-134">To create a new React app to be hosted on Azure:</span></span>

1. <span data-ttu-id="21d82-135">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="21d82-135">Open Visual Studio code.</span></span>
1. <span data-ttu-id="21d82-136">Откройте набор средств Teams, выбрав значок Teams на боковой панели:</span><span class="sxs-lookup"><span data-stu-id="21d82-136">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. <span data-ttu-id="21d82-138">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="21d82-138">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. <span data-ttu-id="21d82-140">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="21d82-140">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания проекта":::

1. <span data-ttu-id="21d82-142">На **шаге Выбор возможностей** уже выбрана возможность **Tab.**</span><span class="sxs-lookup"><span data-stu-id="21d82-142">On the **Select capabilities** step, the **Tab** capability is already selected.</span></span> <span data-ttu-id="21d82-143">Кроме того, можно дополнительно выбрать **расширение бота** **и обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="21d82-143">You can also optionally select **Bot** and **Messaging Extension**.</span></span>  <span data-ttu-id="21d82-144">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21d82-144">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. <span data-ttu-id="21d82-146">На шаге **Тип размещения на клиенте** выберите **Azure**.</span><span class="sxs-lookup"><span data-stu-id="21d82-146">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Снимок экрана: выбор размещения для нового приложения.":::

1. <span data-ttu-id="21d82-148">Необязательно на шаге **Облачные ресурсы** выберите облачные ресурсы, которые использует ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="21d82-148">Optionally, on the **Cloud resources** step, select cloud resources that your application uses.</span></span> <span data-ttu-id="21d82-149">Можно выбрать CRUD (создать, прочитать, обновить и удалить) доступ к SQL или API:</span><span class="sxs-lookup"><span data-stu-id="21d82-149">You can select CRUD (create, read, update, and delete) access to a SQL table or an API:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Снимок экрана: добавление облачных ресурсов в новое приложение.":::

1. <span data-ttu-id="21d82-151">На **шаге Язык программирования** можно выбрать **JavaScript** или **TypeScript:**</span><span class="sxs-lookup"><span data-stu-id="21d82-151">On the **Programming Language** step, you can choose **JavaScript** or **TypeScript**:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Снимок экрана: выбор языка.":::

1. <span data-ttu-id="21d82-153">Выберите папку рабочей области.</span><span class="sxs-lookup"><span data-stu-id="21d82-153">Select a workspace folder.</span></span> <span data-ttu-id="21d82-154">Папка создается в папке рабочего пространства для созданного вами проекта.</span><span class="sxs-lookup"><span data-stu-id="21d82-154">A folder is created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="21d82-155">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="21d82-155">Enter a suitable name for your app, like `helloworld`.</span></span> <span data-ttu-id="21d82-156">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="21d82-156">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="21d82-157">Чтобы продолжить, нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="21d82-157">Press **Enter** to continue.</span></span>

<span data-ttu-id="21d82-158">Приложение Teams создается в течение нескольких секунд.</span><span class="sxs-lookup"><span data-stu-id="21d82-158">Your Teams app is created within a few seconds.</span></span> <span data-ttu-id="21d82-159">Приложение scaffolded содержит код для обработки одной входной записи с Помощью Azure Active Directory и доступа к Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="21d82-159">The scaffolded app contains code to handle single sign-on with Azure Active Directory and access to the Microsoft Graph.</span></span>  <span data-ttu-id="21d82-160">Если вы выбрали ресурсы Azure, код для этих ресурсов также доступен.</span><span class="sxs-lookup"><span data-stu-id="21d82-160">If you selected Azure resources, then the code for those resources is also available.</span></span>

<span data-ttu-id="21d82-161">Подробнее о процессе создания и публикации SPFx см. в руководстве [SPFx.](../get-started/first-app-spfx.md)</span><span class="sxs-lookup"><span data-stu-id="21d82-161">For a walk-through of the SPFx creation and publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="21d82-162">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="21d82-162">Configure your app</span></span>

<span data-ttu-id="21d82-163">В основе приложения Teams три компонента:</span><span class="sxs-lookup"><span data-stu-id="21d82-163">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="21d82-164">Клиент Microsoft Teams (веб-, настольный или мобильный), в котором пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="21d82-164">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="21d82-165">Сервер, который отвечает на запросы контента, отображаемой в Teams.</span><span class="sxs-lookup"><span data-stu-id="21d82-165">A server that responds to requests for content that is displayed in Teams.</span></span> <span data-ttu-id="21d82-166">Например, содержимое вкладок HTML или адаптивная карта бота.</span><span class="sxs-lookup"><span data-stu-id="21d82-166">For example, HTML tab content or a bot Adaptive Card.</span></span>
  1. <span data-ttu-id="21d82-167">Пакет приложений Teams состоит из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="21d82-167">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="21d82-168">В manifest.js.</span><span class="sxs-lookup"><span data-stu-id="21d82-168">The manifest.json.</span></span>
      > - <span data-ttu-id="21d82-169">Значок [цвета](../resources/schema/manifest-schema.md#icons) для отображения приложения в каталоге общедоступных или организаций.</span><span class="sxs-lookup"><span data-stu-id="21d82-169">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      > - <span data-ttu-id="21d82-170">Значок [плана](../resources/schema/manifest-schema.md#icons) для отображения в панели действий Teams.</span><span class="sxs-lookup"><span data-stu-id="21d82-170">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="21d82-171">Манифест и значки хранятся в папке проекта перед отправкой `.fx` в Teams.</span><span class="sxs-lookup"><span data-stu-id="21d82-171">The manifest and icons are stored in the `.fx` folder of your project prior to being uploaded to Teams.</span></span> <span data-ttu-id="21d82-172">При установке приложения клиент Teams определяет файл манифеста, чтобы определить необходимые сведения, такие как имя приложения и URL-адрес, в котором находятся службы.</span><span class="sxs-lookup"><span data-stu-id="21d82-172">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="21d82-173">Чтобы настроить приложение, перейдите на **вкладку Teams набор средств** в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="21d82-173">To configure your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="21d82-174">Выберите **редактор манифеста** в разделе **Project.**</span><span class="sxs-lookup"><span data-stu-id="21d82-174">Select **Manifest Editor** in the **Project** section.</span></span>

<span data-ttu-id="21d82-175">Редактирование полей на странице подробные сведения приложения обновляет содержимое manifest.jsфайла, который в конечном итоге отправляется в составе пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="21d82-175">Editing the fields in the App details page updates the contents of the manifest.json file that is ultimately shipped as part of the app package.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="21d82-176">Установка и локальное запуск приложения</span><span class="sxs-lookup"><span data-stu-id="21d82-176">Install and run your app locally</span></span>

<span data-ttu-id="21d82-177">Чтобы создать и запустить приложение локально, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="21d82-177">To build and run your app locally:</span></span>

1. <span data-ttu-id="21d82-178">В Visual Studio Code нажмите клавишу **F5**, чтобы запустить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="21d82-178">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="21d82-179">При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.</span><span class="sxs-lookup"><span data-stu-id="21d82-179">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="21d82-180">По завершении сборки автоматически откроется окно браузера.</span><span class="sxs-lookup"><span data-stu-id="21d82-180">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="21d82-181">Для завершения может потребоваться от 3 до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="21d82-181">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="21d82-182">В наборе инструментов при необходимости необходимо установить локальный сертификат.</span><span class="sxs-lookup"><span data-stu-id="21d82-182">The toolkit prompts you to install a local certificate if required.</span></span> <span data-ttu-id="21d82-183">Этот сертификат позволяет Teams загружать приложение из `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="21d82-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="21d82-184">Выберите "Да", когда появится следующее диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="21d82-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. <span data-ttu-id="21d82-186">Откроется веб-браузер для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="21d82-186">Your web browser is started to run the application.</span></span> <span data-ttu-id="21d82-187">При появлении запроса на открытие Microsoft Teams выберите "Отмена", чтобы остаться в браузере.</span><span class="sxs-lookup"><span data-stu-id="21d82-187">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="21d82-188">Вам также может быть предложено перейти в приложение Teams в другое время.</span><span class="sxs-lookup"><span data-stu-id="21d82-188">You may also be prompted to switch to the Teams application at other times.</span></span> <span data-ttu-id="21d82-189">Выберите веб-приложение, когда это произойдет.</span><span class="sxs-lookup"><span data-stu-id="21d82-189">Select the web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Снимок экрана: выбор веб-версии Teams при запуске":::

1. <span data-ttu-id="21d82-191">Вам может быть предложено выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="21d82-191">You may be prompted to sign in.</span></span> <span data-ttu-id="21d82-192">В этом случае войдите с учетной записью M365.</span><span class="sxs-lookup"><span data-stu-id="21d82-192">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="21d82-193">При появлении запроса на установку приложения в Teams нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="21d82-193">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="21d82-194">В отладку кода Visual Studio подключаются как Visual Studio, так и frontend.</span><span class="sxs-lookup"><span data-stu-id="21d82-194">Both the backend and frontend are hooked into the Visual Studio Code debugger.</span></span>  <span data-ttu-id="21d82-195">Это позволяет устанавливать точки разрыва в любом месте кода и проверять состояние.</span><span class="sxs-lookup"><span data-stu-id="21d82-195">This allows you to set breakpoints anywhere in your code and inspect state.</span></span>  <span data-ttu-id="21d82-196">В браузере также можно использовать любые средства отладки переднего входа (например, средства разработчика React).</span><span class="sxs-lookup"><span data-stu-id="21d82-196">You can also use any frontend debugging tools (such as the React Developer Tools) within the browser.</span></span>  <span data-ttu-id="21d82-197">Дополнительные сведения о отладки в Visual Studio Коде [просмотрите документацию.](https://code.visualstudio.com/Docs/editor/debugging)</span><span class="sxs-lookup"><span data-stu-id="21d82-197">For more information about debugging in Visual Studio Code, review [the documentation](https://code.visualstudio.com/Docs/editor/debugging).</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="21d82-198">Опубликуйте свое приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="21d82-198">Publish your app to Teams</span></span>

<span data-ttu-id="21d82-199">Прежде чем использовать его другими людьми, необходимо опубликовать приложение на портале разработчиков для teams.</span><span class="sxs-lookup"><span data-stu-id="21d82-199">Before it can be used by other people, you must publish your app to the Developer Portal for Teams.</span></span>

1. <span data-ttu-id="21d82-200">Чтобы опубликовать приложение, перейдите на **вкладку Teams набор средств** в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="21d82-200">To publish your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="21d82-201">Выберите **Опубликовать Teams** в разделе **Project.**</span><span class="sxs-lookup"><span data-stu-id="21d82-201">Select **Publish to Teams** in the **Project** section.</span></span>

<span data-ttu-id="21d82-202">При использовании хостинга Azure необходимо предварительно и развернуто в облаке.</span><span class="sxs-lookup"><span data-stu-id="21d82-202">If using Azure hosting, you must have provisioned and deployed to the cloud.</span></span> <span data-ttu-id="21d82-203">Подробнее о процессе публикации SPFx см. в [SPFx.](../get-started/first-app-spfx.md)</span><span class="sxs-lookup"><span data-stu-id="21d82-203">For a walk-through of the SPFx publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="21d82-204">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="21d82-204">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="21d82-205">Ведение и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="21d82-205">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
