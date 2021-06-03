---
title: Создание приложений с помощью Microsoft Teams набор средств и Visual Studio Code
description: Начало создания больших пользовательских приложений непосредственно Visual Studio Code с Microsoft Teams набор средств
keywords: команда визуальный набор кода студии
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: bc97a78df5618c87dfc66fae179145acd749ad1f
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721824"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="d3ef9-104">Создание приложений с помощью Teams набор средств и Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d3ef9-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="d3ef9-105">Программа Teams набор средств для Visual Studio Code помогает разработчикам создавать и развертывать приложения Teams с интегрированной идентификацией, доступом к облачному хранилище, данным microsoft Graph и другим службам в Azure и M365 с подходом "нулевой конфигурации" к опыту разработчика.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-105">The Teams Toolkit for Visual Studio Code helps developers create and deploy Teams apps with integrated identity, access to cloud storage, data from Microsoft Graph, and other services in Azure and M365 with a “zero-configuration” approach to the developer experience.</span></span>  

<span data-ttu-id="d3ef9-106">Вы также можете использовать набор инструментов с Visual Studio или как CLI `teamsfx` (называется).</span><span class="sxs-lookup"><span data-stu-id="d3ef9-106">You also can use the toolkit with Visual Studio or as a CLI (called `teamsfx`).</span></span>

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="d3ef9-107">Установите Teams набор средств для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d3ef9-107">Install the Teams Toolkit for Visual Studio Code</span></span>

1. <span data-ttu-id="d3ef9-108">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-108">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="d3ef9-109">Выберите представление Расширения **(Ctrl+Shift+X**  /  **⌘⇧-X** или **> расширения).**</span><span class="sxs-lookup"><span data-stu-id="d3ef9-109">Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="d3ef9-110">В поле поиска введите _Teams набор средств_.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-110">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="d3ef9-111">Выберите на зеленой кнопке установки рядом с Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-111">Select on the green install button next to the Teams Toolkit.</span></span>

<span data-ttu-id="d3ef9-112">Вы также можете найти Teams набор средств на Visual Studio Code [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span><span class="sxs-lookup"><span data-stu-id="d3ef9-112">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="d3ef9-113">Следующие средства будут установлены расширением Visual Studio Code при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-113">The following tools will be installed by the Visual Studio Code extension when they are needed.</span></span>  <span data-ttu-id="d3ef9-114">Если уже установлено, вместо нее будет использоваться установленная версия.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-114">If already installed, the installed version will be used instead.</span></span>  <span data-ttu-id="d3ef9-115">Если используется Linux (в том числе WSL), необходимо установить эти средства перед использованием:</span><span class="sxs-lookup"><span data-stu-id="d3ef9-115">If using Linux (including WSL), you must install these tools before use:</span></span>

- [<span data-ttu-id="d3ef9-116">Основные средства Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d3ef9-116">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="d3ef9-117">Основные средства Azure Functions используются для локального запуска отлаженных компонентов, включая помощников проверки подлинности, необходимых при запуске служб в Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-117">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span>  <span data-ttu-id="d3ef9-118">Он устанавливается в каталоге проекта (с помощью `devDependencies` npm).</span><span class="sxs-lookup"><span data-stu-id="d3ef9-118">It is installed within the project directory (using the npm `devDependencies`).</span></span>

- [<span data-ttu-id="d3ef9-119">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="d3ef9-119">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="d3ef9-120">SDK .NET используется для установки настраиваемых привязки для локального отладки и развертывания приложений Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-120">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span>  <span data-ttu-id="d3ef9-121">Если вы не установили SDK .NET 3.1 (или более поздней версии) глобально, портативная версия будет установлена.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-121">If you have not installed the .NET 3.1 (or later) SDK globally, the portable version will be installed.</span></span>

- [<span data-ttu-id="d3ef9-122">ngrok</span><span class="sxs-lookup"><span data-stu-id="d3ef9-122">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="d3ef9-123">Некоторые Teams приложения (беседные боты, расширения обмена сообщениями и входящие веб-оки) требуют входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-123">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span>  <span data-ttu-id="d3ef9-124">Необходимо подвергать систему разработки Teams через туннель.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-124">You need to expose your development system to Teams through a tunnel.</span></span>  <span data-ttu-id="d3ef9-125">Туннель не требуется для приложений, которые включают только вкладки.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-125">A tunnel is not required for apps that only include tabs.</span></span>  <span data-ttu-id="d3ef9-126">Этот пакет устанавливается в каталоге проекта (с помощью `devDependencies` npm).</span><span class="sxs-lookup"><span data-stu-id="d3ef9-126">This package is installed within the project directory (using npm `devDependencies`).</span></span>

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="d3ef9-127">Используйте Teams набор средств для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d3ef9-127">Use the Teams Toolkit for Visual Studio Code</span></span>

- [<span data-ttu-id="d3ef9-128">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="d3ef9-128">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="d3ef9-129">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="d3ef9-129">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="d3ef9-130">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="d3ef9-130">Run your app locally</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="d3ef9-131">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="d3ef9-131">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="d3ef9-132">Настройка нового проекта Teams</span><span class="sxs-lookup"><span data-stu-id="d3ef9-132">Set up a new Teams project</span></span>

<span data-ttu-id="d3ef9-133">В Teams набор средств могут создаваться React, которые будут SPFx azure или SPFx веб-части в среде M365 SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-133">The Teams Toolkit can create React apps that will be hosted in Azure or SPFx web parts that will be hosted on your M365 SharePoint environment.</span></span>  <span data-ttu-id="d3ef9-134">Чтобы создать новое приложение React, которое будет организовано в Azure:</span><span class="sxs-lookup"><span data-stu-id="d3ef9-134">To create a new React app to be hosted on Azure:</span></span>

1. <span data-ttu-id="d3ef9-135">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-135">Open Visual Studio code.</span></span>
1. <span data-ttu-id="d3ef9-136">Откройте набор средств Teams, выбрав значок Teams на боковой панели:</span><span class="sxs-lookup"><span data-stu-id="d3ef9-136">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. <span data-ttu-id="d3ef9-138">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-138">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. <span data-ttu-id="d3ef9-140">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-140">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания нового проекта":::

1. <span data-ttu-id="d3ef9-142">На странице **выбора возможностей** уже будет выбрана возможность **Вкладка**.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-142">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="d3ef9-143">Кроме того, можно дополнительно выбрать **расширение бота** **и обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="d3ef9-143">You can also optionally select **Bot** and **Messaging Extension**.</span></span>  <span data-ttu-id="d3ef9-144">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-144">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. <span data-ttu-id="d3ef9-146">На шаге **Тип размещения на клиенте** выберите **Azure**.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-146">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Снимок экрана: выбор размещения для нового приложения.":::

1. <span data-ttu-id="d3ef9-148">(Необязательный) На **шаге Облачные ресурсы** выберите облачные ресурсы, которые будет использовать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-148">(Optional) On the **Cloud resources** step, select cloud resources that your application will use.</span></span>  <span data-ttu-id="d3ef9-149">Вы можете выбрать CRUD (создать, прочитать, обновить, удалить) доступ к SQL таблице или API:</span><span class="sxs-lookup"><span data-stu-id="d3ef9-149">You can select CRUD (create, read, update, delete) access to a SQL table or an API:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Снимок экрана: добавление облачных ресурсов в новое приложение.":::

1. <span data-ttu-id="d3ef9-151">На **шаге Язык программирования** можно выбрать **JavaScript** или **TypeScript:**</span><span class="sxs-lookup"><span data-stu-id="d3ef9-151">On the **Programming Language** step, you can choose **JavaScript** or **TypeScript**:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Снимок экрана: выбор языка.":::

1. <span data-ttu-id="d3ef9-153">Выберите папку рабочей области.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-153">Select a workspace folder.</span></span>  <span data-ttu-id="d3ef9-154">В папке рабочей области будет создана папка для создаваемого проекта.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-154">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="d3ef9-155">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-155">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="d3ef9-156">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-156">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="d3ef9-157">Чтобы продолжить, нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-157">Press **Enter** to continue.</span></span>

<span data-ttu-id="d3ef9-158">Создание приложения Teams займет несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-158">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="d3ef9-159">Приложение scaffolded содержит код для обработки одной входной записи с помощью Azure Active Directory и доступа к microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-159">The scaffolded app contains code to handle single sign-on with Azure Active Directory and access to the Microsoft Graph.</span></span>  <span data-ttu-id="d3ef9-160">Если вы выбрали ресурсы Azure, код для этих ресурсов также будет доступен.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-160">If you selected Azure resources, then the code for those resources will also be available.</span></span>

<span data-ttu-id="d3ef9-161">Подробнее о процессе создания SPFx публикации см. в [SPFx.](../get-started/first-app-spfx.md)</span><span class="sxs-lookup"><span data-stu-id="d3ef9-161">For a walk-through of the SPFx creation and publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="d3ef9-162">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="d3ef9-162">Configure your app</span></span>

<span data-ttu-id="d3ef9-163">В основе приложения Teams три компонента:</span><span class="sxs-lookup"><span data-stu-id="d3ef9-163">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="d3ef9-164">Клиент Microsoft Teams (веб-, настольный или мобильный), где пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-164">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="d3ef9-165">Сервер, который отвечает на запросы контента, который будет отображаться в Teams.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-165">A server that responds to requests for content that will be displayed in Teams.</span></span> <span data-ttu-id="d3ef9-166">Например, содержимое htmL-вкладок или адаптивная карта бота.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-166">For example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="d3ef9-167">Пакет Teams состоит из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="d3ef9-167">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="d3ef9-168">В manifest.js.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-168">The manifest.json.</span></span>
      > - <span data-ttu-id="d3ef9-169">Значок [цвета](../resources/schema/manifest-schema.md#icons) для отображения приложения в каталоге общедоступных или организаций.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-169">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      > - <span data-ttu-id="d3ef9-170">Значок [плана](../resources/schema/manifest-schema.md#icons) для отображения на панели Teams действий.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-170">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="d3ef9-171">Манифест и значки хранятся в папке проекта перед отправкой `.fx` в Teams.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-171">The manifest and icons are stored in the `.fx` folder of your project prior to being uploaded to Teams.</span></span> <span data-ttu-id="d3ef9-172">При установке приложения клиент Teams определяет файл манифеста, чтобы определить необходимые сведения, такие как имя приложения и URL-адрес, в котором находятся службы.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-172">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="d3ef9-173">Чтобы настроить приложение, перейдите на вкладку Teams набор средств **в** Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-173">To configure your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="d3ef9-174">Выберите **редактор манифеста** **в Project** разделе.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-174">Select **Manifest Editor** in the **Project** section.</span></span>

<span data-ttu-id="d3ef9-175">Редактирование полей на странице сведения приложения обновляет содержимое manifest.jsфайла, который в конечном итоге будет отгрузка в составе пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-175">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="d3ef9-176">Установка и локальное запуск приложения</span><span class="sxs-lookup"><span data-stu-id="d3ef9-176">Install and run your app locally</span></span>

<span data-ttu-id="d3ef9-177">Чтобы создать и запустить приложение локально, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-177">To build and run your app locally:</span></span>

1. <span data-ttu-id="d3ef9-178">В Visual Studio Code нажмите клавишу **F5**, чтобы запустить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-178">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="d3ef9-179">При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-179">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="d3ef9-180">По завершении сборки автоматически откроется окно браузера.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-180">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="d3ef9-181">Для завершения может потребоваться от 3 до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-181">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="d3ef9-182">В наборе инструментов будет предложено установить локальный сертификат, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-182">The toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="d3ef9-183">Этот сертификат позволяет Teams загружать приложение из `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="d3ef9-184">Выберите "Да", когда появится следующее диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="d3ef9-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. <span data-ttu-id="d3ef9-186">Откроется веб-браузер для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-186">Your web browser is started to run the application.</span></span> <span data-ttu-id="d3ef9-187">При появлении запроса на открытие Microsoft Teams выберите "Отмена", чтобы остаться в браузере.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-187">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="d3ef9-188">Вам также может быть предложено перейти на Teams приложение в другое время.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-188">You may also be prompted to switch to the Teams application at other times.</span></span> <span data-ttu-id="d3ef9-189">Выберите веб-приложение, когда это произойдет.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-189">Select the web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Снимок экрана: выбор веб-версии Teams при запуске":::

1. <span data-ttu-id="d3ef9-191">Вам может быть предложено выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-191">You may be prompted to sign in.</span></span>  <span data-ttu-id="d3ef9-192">В этом случае войдите с учетной записью M365.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-192">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="d3ef9-193">При появлении запроса на установку приложения в Teams нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-193">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="d3ef9-194">В отладку подключены как Visual Studio Code, так и Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-194">Both the backend and frontend are hooked into the Visual Studio Code debugger.</span></span>  <span data-ttu-id="d3ef9-195">Это позволяет устанавливать точки разрыва в любом месте кода и проверять состояние.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-195">This allows you to set breakpoints anywhere in your code and inspect state.</span></span>  <span data-ttu-id="d3ef9-196">В браузере также можно использовать любые средства отладки frontend (например, средства React разработчика).</span><span class="sxs-lookup"><span data-stu-id="d3ef9-196">You can also use any frontend debugging tools (such as the React Developer Tools) within the browser.</span></span>  <span data-ttu-id="d3ef9-197">Дополнительные сведения о отладки в Visual Studio Code, [просмотрите документацию](https://code.visualstudio.com/Docs/editor/debugging).</span><span class="sxs-lookup"><span data-stu-id="d3ef9-197">For more information about debugging in Visual Studio Code, review [the documentation](https://code.visualstudio.com/Docs/editor/debugging).</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="d3ef9-198">Опубликуйте свое приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="d3ef9-198">Publish your app to Teams</span></span>

<span data-ttu-id="d3ef9-199">Прежде чем использовать его другими людьми, необходимо опубликовать приложение на портале разработчиков для Teams.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-199">Before it can be used by other people, you must publish your app to the Developer Portal for Teams.</span></span>

1. <span data-ttu-id="d3ef9-200">Чтобы опубликовать приложение, перейдите на вкладку **Teams набор средств** в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-200">To publish your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="d3ef9-201">Выберите **Опубликовать Teams** в разделе **Project.**</span><span class="sxs-lookup"><span data-stu-id="d3ef9-201">Select **Publish to Teams** in the **Project** section.</span></span>

<span data-ttu-id="d3ef9-202">При использовании хостинга Azure необходимо предварительно и развернуто в облаке.</span><span class="sxs-lookup"><span data-stu-id="d3ef9-202">If using Azure hosting, you must have provisioned and deployed to the cloud.</span></span> <span data-ttu-id="d3ef9-203">Подробнее о процессе публикации SPFx см. в [SPFx.](../get-started/first-app-spfx.md)</span><span class="sxs-lookup"><span data-stu-id="d3ef9-203">For a walk-through of the SPFx publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="d3ef9-204">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="d3ef9-204">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d3ef9-205">Ведение и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="d3ef9-205">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
