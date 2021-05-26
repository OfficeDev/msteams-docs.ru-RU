---
title: Начало работы — создайте Teams приложение с помощью Blazor
author: adrianhall
description: Быстро создайте Microsoft Teams приложение, которое отображает "Hello, World!" сообщение с Microsoft Teams набор средств и .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: 861b6921d7a2092a746ea7dc1399f8aaa523e207
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646780"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a><span data-ttu-id="1d50d-104">Создание и запуск первого Microsoft Teams приложения с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="1d50d-104">Build and run your first Microsoft Teams app with Blazor</span></span>

<span data-ttu-id="1d50d-105">В этом руководстве вы создайте новое приложение Microsoft Teams в .NET/Blazor, которое реализует простое личное приложение для получения информации из microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1d50d-105">In this tutorial, you will create a new Microsoft Teams app in .NET/Blazor that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="1d50d-106">(Личное *приложение включает* набор вкладок для индивидуального использования.)  Во время руководства вы узнаете о структуре приложения Teams, локальном запуске приложения и развертывании приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="1d50d-106">(A *personal app* includes a set of tabs scoped for individual use.)  During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="1d50d-107">Построенное приложение отображает основные сведения о пользователе для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="1d50d-107">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="1d50d-108">Когда будет предоставлено разрешение, приложение подключается к microsoft Graph как текущий пользователь, чтобы получить полный профиль.</span><span class="sxs-lookup"><span data-stu-id="1d50d-108">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1d50d-109">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="1d50d-109">Before you begin</span></span>

<span data-ttu-id="1d50d-110">Убедитесь, что среда разработки настроена путем установки [необходимых условий](prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="1d50d-110">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1d50d-111">Установка необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="1d50d-111">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="1d50d-112">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="1d50d-112">Create your project</span></span>

<span data-ttu-id="1d50d-113">Используйте Teams набор средств для создания первого проекта:</span><span class="sxs-lookup"><span data-stu-id="1d50d-113">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="1d50d-114">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="1d50d-114">Visual Studio 2019</span></span>](#tab/vs)

1. <span data-ttu-id="1d50d-115">Open Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="1d50d-115">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="1d50d-116">Выберите **Создание нового проекта.**</span><span class="sxs-lookup"><span data-stu-id="1d50d-116">Select **Create a new project**.</span></span>

1. <span data-ttu-id="1d50d-117">Выберите **Microsoft Teams app,** а затем нажмите **кнопку Далее**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-117">Select **Microsoft Teams App**, then press **Next**.</span></span>  <span data-ttu-id="1d50d-118">Чтобы помочь найти шаблон, используйте тип **проекта Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="1d50d-118">To help you find the template, use the project type **Microsoft Teams**.</span></span>

1. <span data-ttu-id="1d50d-119">Дайте проекту и решению хорошее имя, а затем нажмите **кнопку Далее**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-119">Give the project and solution a good name, then press **Next**.</span></span>

1. <span data-ttu-id="1d50d-120">Укайте имя приложения и имя компании, а затем нажмите **кнопку Создать**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-120">Provide the application name and company name, then press **Create**.</span></span>  <span data-ttu-id="1d50d-121">Имя приложения и имя компании отображаются конечным пользователям.</span><span class="sxs-lookup"><span data-stu-id="1d50d-121">The application name and company name are displayed to your end users.</span></span>

1. <span data-ttu-id="1d50d-122">Ваше Teams приложение будет создано в течение нескольких секунд.</span><span class="sxs-lookup"><span data-stu-id="1d50d-122">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="1d50d-123">После создания проекта установите единую регистрацию с помощью M365:</span><span class="sxs-lookup"><span data-stu-id="1d50d-123">Once the project is created, set up single sign-on with M365:</span></span>

   - <span data-ttu-id="1d50d-124">Выберите **Project**  >  **TeamsFx**  >  **Configure для SSO...**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-124">Select **Project** > **TeamsFx** > **Configure for SSO...**.</span></span>
   - <span data-ttu-id="1d50d-125">При запросе впишитесь в свою учетную запись администратора M365.</span><span class="sxs-lookup"><span data-stu-id="1d50d-125">When prompted, sign in to your M365 administrator account.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="1d50d-126">Командная строка</span><span class="sxs-lookup"><span data-stu-id="1d50d-126">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="1d50d-127">Откройте терминал и выберите каталог, в котором вы хотите создать проект.</span><span class="sxs-lookup"><span data-stu-id="1d50d-127">Open a Terminal and select the directory where you wish to create the project.</span></span>

1. <span data-ttu-id="1d50d-128">Выполнить `dotnet new -i` установку шаблона из NuGet:</span><span class="sxs-lookup"><span data-stu-id="1d50d-128">Run `dotnet new -i` to install the template from NuGet:</span></span>

   ``` bash
   dotnet new -i Microsoft.TeamsApp.Blazor
   ```

   <span data-ttu-id="1d50d-129">Это необходимо сделать только в первый раз или при обновлении шаблона.</span><span class="sxs-lookup"><span data-stu-id="1d50d-129">You only need to do this the first time or when updating the template.</span></span>

1. <span data-ttu-id="1d50d-130">Создание каталога:</span><span class="sxs-lookup"><span data-stu-id="1d50d-130">Create a directory:</span></span>

   ``` bash
   mkdir helloworld
   ```

1. <span data-ttu-id="1d50d-131">Запуск `dotnet new` для создания нового проекта:</span><span class="sxs-lookup"><span data-stu-id="1d50d-131">Run `dotnet new` to create a new project:</span></span>

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. <span data-ttu-id="1d50d-132">После развертывания на эшафоте настройте проект для Teams развертывания:</span><span class="sxs-lookup"><span data-stu-id="1d50d-132">Once scaffolded, configure the project for Teams deployment:</span></span>

   ``` bash
   teamsfx init
   ```

<span data-ttu-id="1d50d-133">Теперь можно открыть решение в Visual Studio для отладки.</span><span class="sxs-lookup"><span data-stu-id="1d50d-133">You can now open the solution in Visual Studio for debugging.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="1d50d-134">Осмотр исходных кодов</span><span class="sxs-lookup"><span data-stu-id="1d50d-134">Take a tour of the source code</span></span>

<span data-ttu-id="1d50d-135">Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально.](#run-your-app-locally)</span><span class="sxs-lookup"><span data-stu-id="1d50d-135">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="1d50d-136">Как только Teams набор средств настраивает проект, у вас есть компоненты для создания базового личного приложения для Teams.</span><span class="sxs-lookup"><span data-stu-id="1d50d-136">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="1d50d-137">Каталоги и файлы проекта отображаются в области Обозреватель решений в Visual Studio 2019 г.</span><span class="sxs-lookup"><span data-stu-id="1d50d-137">The project directories and files display in the Solution Explorer area of Visual Studio 2019.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Снимок экрана, показывающий файлы проектов приложений для личного приложения в Visual Studio 2019 г.":::

- <span data-ttu-id="1d50d-139">Значки приложения хранятся в качестве PNG-файлов и `color.png` `outline.png` .</span><span class="sxs-lookup"><span data-stu-id="1d50d-139">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="1d50d-140">Манифест приложения для публикации на портале разработчиков для Teams хранится в `Properties/manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="1d50d-140">The app manifest for publishing through the Developer Portal for Teams is stored in `Properties/manifest.json`.</span></span>
- <span data-ttu-id="1d50d-141">Контроллер backend предоставляется для `Controllers/BackendController.cs` оказания помощи в проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="1d50d-141">A backend controller is provided in `Controllers/BackendController.cs` for assisting with authentication.</span></span>

<span data-ttu-id="1d50d-142">Так как вы создали приложение вкладки во время установки, Teams набор средств наберет весь необходимый код для базовой вкладки в качестве [сервера Blazor.](/aspnet/core/blazor)</span><span class="sxs-lookup"><span data-stu-id="1d50d-142">Since you created a tab app during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab as a [Blazor Server](/aspnet/core/blazor).</span></span>

- <span data-ttu-id="1d50d-143">`Pages/Tab.razor` является точкой входа переднего приложения.</span><span class="sxs-lookup"><span data-stu-id="1d50d-143">`Pages/Tab.razor` is the front-end application's entry point.</span></span>
- <span data-ttu-id="1d50d-144">`TeamsFx.cs`и `JS/src/index.js` используется для инициализации коммуникаций с Teams хостом.</span><span class="sxs-lookup"><span data-stu-id="1d50d-144">`TeamsFx.cs` and `JS/src/index.js` is used for initializing communications with the Teams host.</span></span>

<span data-ttu-id="1d50d-145">Можно добавить функции backend, добавив в приложение дополнительные ASP.NET Core контроллеры.</span><span class="sxs-lookup"><span data-stu-id="1d50d-145">You can add backend functionality by adding additional ASP.NET Core controllers to your application.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="1d50d-146">Запустите приложение локально</span><span class="sxs-lookup"><span data-stu-id="1d50d-146">Run your app locally</span></span>

<span data-ttu-id="1d50d-147">Teams набор средств позволяет запускать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="1d50d-147">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="1d50d-148">Она состоит из нескольких частей, необходимых для обеспечения правильной инфраструктуры, Teams ожидает:</span><span class="sxs-lookup"><span data-stu-id="1d50d-148">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="1d50d-149">Приложение регистрируется в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1d50d-149">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="1d50d-150">Это приложение имеет разрешения, связанные с расположением, которое загружается приложение, и любыми дополнительными ресурсами, к которые оно имеет доступ.</span><span class="sxs-lookup"><span data-stu-id="1d50d-150">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="1d50d-151">Веб-API находится (IIS Express) для оказания помощи в задачах проверки подлинности, выступая в качестве прокси-сервера между приложением и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1d50d-151">A web API is hosted (via IIS Express) to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  
- <span data-ttu-id="1d50d-152">Манифест приложения создается и существует на портале разработчиков для Teams.</span><span class="sxs-lookup"><span data-stu-id="1d50d-152">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="1d50d-153">Teams манифест приложения, чтобы сообщить подключенным клиентам, из чего загрузить приложение.</span><span class="sxs-lookup"><span data-stu-id="1d50d-153">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="1d50d-154">После этого приложение может быть загружено в Teams клиенте.</span><span class="sxs-lookup"><span data-stu-id="1d50d-154">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="1d50d-155">Мы используем веб Teams клиента, чтобы мы могли видеть код HTML, CSS и JavaScript в стандартной среде веб-разработки.</span><span class="sxs-lookup"><span data-stu-id="1d50d-155">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

<span data-ttu-id="1d50d-156">Чтобы создать и запустить приложение локально:</span><span class="sxs-lookup"><span data-stu-id="1d50d-156">To build and run your app locally:</span></span>

1. <span data-ttu-id="1d50d-157">С Visual Studio Code нажмите **кнопку F5** для запуска приложения в режиме отлаживания.</span><span class="sxs-lookup"><span data-stu-id="1d50d-157">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

1. <span data-ttu-id="1d50d-158">При запросе установите самозаверяющийся сертификат SSL для локальной отладки.</span><span class="sxs-lookup"><span data-stu-id="1d50d-158">If requested, install the self-signed SSL certificate for local debugging.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана, показывающий, как запрос на установку сертификата SSL для Teams загрузки приложения из localhost.":::

1. <span data-ttu-id="1d50d-160">Teams будет загружен в веб-браузер, и вам будет предложено войти.</span><span class="sxs-lookup"><span data-stu-id="1d50d-160">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="1d50d-161">Если вам будет предложено открыть Microsoft Teams, выберите Отмена, чтобы оставаться в браузере.</span><span class="sxs-lookup"><span data-stu-id="1d50d-161">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="1d50d-162">Во входе с учетной записью M365.</span><span class="sxs-lookup"><span data-stu-id="1d50d-162">Sign in with your M365 account.</span></span>
1. <span data-ttu-id="1d50d-163">При запросе установки приложения на Teams нажмите **кнопку Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-163">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="1d50d-164">Теперь ваше приложение будет отображаться:</span><span class="sxs-lookup"><span data-stu-id="1d50d-164">Your app will now be displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="Снимок экрана завершенного приложения":::

<span data-ttu-id="1d50d-166">Вы можете делать обычные действия отладки, как если бы это было любое другое веб-приложение (например, настройка точек взлома).</span><span class="sxs-lookup"><span data-stu-id="1d50d-166">You can do normal debugging activities as if this were any other web application (such as setting breakpoints).</span></span> <span data-ttu-id="1d50d-167">Приложение поддерживает горячую перезагрузку.</span><span class="sxs-lookup"><span data-stu-id="1d50d-167">The app supports hot reloading.</span></span>  <span data-ttu-id="1d50d-168">Если вы измените какой-либо файл в проекте, страница будет перезагружена.</span><span class="sxs-lookup"><span data-stu-id="1d50d-168">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="1d50d-169">Узнайте, что происходит при локальном запуске приложения в отладите.</span><span class="sxs-lookup"><span data-stu-id="1d50d-169">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="1d50d-170">При нажатии F5 Teams набор средств:</span><span class="sxs-lookup"><span data-stu-id="1d50d-170">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="1d50d-171">Зарегистрировали приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1d50d-171">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="1d50d-172">Зарегистрировала приложение для "боковой загрузки" в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1d50d-172">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="1d50d-173">Начался локальный запуск backend приложения.</span><span class="sxs-lookup"><span data-stu-id="1d50d-173">Started your application backend running locally.</span></span>
1. <span data-ttu-id="1d50d-174">Начало локального локального хозяйского хостинга приложения.</span><span class="sxs-lookup"><span data-stu-id="1d50d-174">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="1d50d-175">Начало Microsoft Teams в веб-браузере с командой Teams для боковой загрузки приложения (URL-адрес зарегистрирован в манифесте приложения).</span><span class="sxs-lookup"><span data-stu-id="1d50d-175">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="1d50d-176">Узнайте, как устранить распространенные проблемы при локальном запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="1d50d-176">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="1d50d-177">Чтобы успешно запустить приложение в Teams, необходимо иметь учетную запись Microsoft 365 разработки, которая позволяет загружать приложения в стороне.</span><span class="sxs-lookup"><span data-stu-id="1d50d-177">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app side loading.</span></span> <span data-ttu-id="1d50d-178">Дополнительные сведения об открытии учетной записи см. в [дополнительных сведениях.](prerequisites.md#enable-sideloading)</span><span class="sxs-lookup"><span data-stu-id="1d50d-178">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="1d50d-179">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="1d50d-179">Deploy your app to Azure</span></span>

<span data-ttu-id="1d50d-180">Развертывание состоит из двух этапов.</span><span class="sxs-lookup"><span data-stu-id="1d50d-180">Deployment consists of two steps.</span></span>  <span data-ttu-id="1d50d-181">Сначала создаются необходимые облачные ресурсы (также известные как подготовка), затем код, который составляет ваше приложение, копируется в созданные облачные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1d50d-181">First, necessary cloud resources are created (also known as provisioning), then the code that makes up your app is copied into the created cloud resources.</span></span>

> <span data-ttu-id="1d50d-182">**Предварительный просмотр**</span><span class="sxs-lookup"><span data-stu-id="1d50d-182">**PREVIEW**</span></span>
>
> <span data-ttu-id="1d50d-183">Поддержка приложений Blazor является новой в Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="1d50d-183">Support for Blazor apps is new in Teams Toolkit.</span></span>  <span data-ttu-id="1d50d-184">Подготовка и развертывание делаются с Visual Studio 2019 г. и порталом разработчиков для Teams.</span><span class="sxs-lookup"><span data-stu-id="1d50d-184">Provisioning and deployment are done with a combination of Visual Studio 2019 and the Developer Portal for Teams.</span></span>

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a><span data-ttu-id="1d50d-185">Подготовка и развертывание приложения в Службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="1d50d-185">Provision and deploy your app to Azure App Service</span></span>

1. <span data-ttu-id="1d50d-186">В Обозревателе решений щелкните правой кнопкой мыши узел проекта и выберите **Опубликовать** (или используйте элемент **меню Build**  >  **Publish).**</span><span class="sxs-lookup"><span data-stu-id="1d50d-186">In Solution Explorer, right-click the project node and choose **Publish** (or use the **Build** > **Publish** menu item).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="Выберите операцию Публикация в проекте":::

1. <span data-ttu-id="1d50d-188">В **окне Публикация** выберите **Azure**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-188">In the **Publish** window, select **Azure**.</span></span>  <span data-ttu-id="1d50d-189">Нажмите **кнопку Далее**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-189">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="Выберите Azure в качестве цели публикации":::

1. <span data-ttu-id="1d50d-191">Выберите **службу приложений Azure (Windows).**</span><span class="sxs-lookup"><span data-stu-id="1d50d-191">Select **Azure App Service (Windows)**.</span></span>  <span data-ttu-id="1d50d-192">Нажмите **кнопку Далее**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-192">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="Выберите службу приложений Azure в качестве цели публикации":::

1. <span data-ttu-id="1d50d-194">Выберите **+** для создания нового экземпляра службы приложений.</span><span class="sxs-lookup"><span data-stu-id="1d50d-194">Select **+** to create a new App Service instance.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="Создание нового экземпляра.":::

1. <span data-ttu-id="1d50d-196">В **диалоговом октаге Create App Service (Windows)** заполняются  поля "Имя", "Имя подписки", "Группа ресурсов" и "Планирование размещения". </span><span class="sxs-lookup"><span data-stu-id="1d50d-196">In the **Create App Service (Windows)** dialog, the **Name**, **Subscription name**, **Resource Group**, and **Hosting Plan** entry fields are populated.</span></span> <span data-ttu-id="1d50d-197">Если у вас уже запущена служба приложений, будут выбраны существующие параметры.</span><span class="sxs-lookup"><span data-stu-id="1d50d-197">If you have already got an App Service running, existing settings will be selected.</span></span>  <span data-ttu-id="1d50d-198">Вы можете выбрать создание новой группы ресурсов и плана размещения (Рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="1d50d-198">You can opt to create a new resource group and hosting plan (Recommended).</span></span>  <span data-ttu-id="1d50d-199">Когда вы готовы, выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-199">When ready, select **Create**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="Выбор плана размещения и подписки":::

1. <span data-ttu-id="1d50d-201">В **диалоговом** окте "Публикация" вновь созданный экземпляр выбран автоматически.</span><span class="sxs-lookup"><span data-stu-id="1d50d-201">In the **Publish** dialog, the newly created instance has been automatically selected.</span></span>  <span data-ttu-id="1d50d-202">Когда вы готовы, выберите **Finish**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-202">When ready, select **Finish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="Выберите новый экземпляр.":::

1. <span data-ttu-id="1d50d-204">Нажмите **значок Изменить** (карандаш) рядом с **режимом развертывания,** а затем выберите **автономный**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-204">Press the **Edit** (pencil) icon next to **Deployment Mode**, then select **Self-contained**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="Выберите автономный режим развертывания.":::

1. <span data-ttu-id="1d50d-206">Нажмите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-206">Select **Publish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="Публикация приложения в службу приложений":::

<span data-ttu-id="1d50d-208">Visual Studio развертывает приложение в службе приложений Azure, а веб-приложение загружается в браузере.</span><span class="sxs-lookup"><span data-stu-id="1d50d-208">Visual Studio deploys the app to your Azure App Service, and the web app loads in your browser.</span></span>  <span data-ttu-id="1d50d-209">Добавьте `/tab` в конец URL-адреса, чтобы увидеть свою страницу.</span><span class="sxs-lookup"><span data-stu-id="1d50d-209">Add `/tab` to the end of the URL to see your page.</span></span>

<span data-ttu-id="1d50d-210">В области свойства проекта **Publish** показаны URL-адрес сайта и другие сведения.</span><span class="sxs-lookup"><span data-stu-id="1d50d-210">The project properties **Publish** pane shows the site URL and other details.</span></span> <span data-ttu-id="1d50d-211">Заметьте URL-адрес сайта.</span><span class="sxs-lookup"><span data-stu-id="1d50d-211">Make a note of the site URL.</span></span>

## <a name="create-an-environment-for-your-app"></a><span data-ttu-id="1d50d-212">Создание среды для приложения</span><span class="sxs-lookup"><span data-stu-id="1d50d-212">Create an environment for your app</span></span>

<span data-ttu-id="1d50d-213">Портал разработчиков для Teams управляет загрузкой вкладок для приложения с помощью **среды.**</span><span class="sxs-lookup"><span data-stu-id="1d50d-213">The Developer Portal for Teams manages where the tabs for your app are loaded from with an **Environment**.</span></span>  <span data-ttu-id="1d50d-214">Чтобы создать среду:</span><span class="sxs-lookup"><span data-stu-id="1d50d-214">To create an environment:</span></span>

1. <span data-ttu-id="1d50d-215">Откройте портал [разработчиков для Teams](https://dev.teams.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="1d50d-215">Open the [Developer Portal for Teams](https://dev.teams.microsoft.com).</span></span>  <span data-ttu-id="1d50d-216">Во входе с помощью административной учетной записи M365.</span><span class="sxs-lookup"><span data-stu-id="1d50d-216">Sign in with your M365 administrative account.</span></span>

1. <span data-ttu-id="1d50d-217">На боковой панели выберите **Приложения.**</span><span class="sxs-lookup"><span data-stu-id="1d50d-217">From the sidebar, select **Apps**.</span></span>

1. <span data-ttu-id="1d50d-218">Если у вас есть только одно приложение, оно будет выбрано автоматически.</span><span class="sxs-lookup"><span data-stu-id="1d50d-218">If you only have one app, it will be automatically selected.</span></span>  <span data-ttu-id="1d50d-219">Если нет, выберите приложение из списка.</span><span class="sxs-lookup"><span data-stu-id="1d50d-219">If not, select your app from the list.</span></span>

1. <span data-ttu-id="1d50d-220">Выбор **сред**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-220">Select **Environments**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="Выбор сред":::

1. <span data-ttu-id="1d50d-222">Выберите **Создать первую среду.**</span><span class="sxs-lookup"><span data-stu-id="1d50d-222">Select **Create your first environment**.</span></span>

1. <span data-ttu-id="1d50d-223">Введите имя для среды и нажмите кнопку **Добавить;** например _Production_.</span><span class="sxs-lookup"><span data-stu-id="1d50d-223">Enter a name for your environment, then press **Add**; for example _Production_.</span></span>

1. <span data-ttu-id="1d50d-224">После выбора новой среды нажмите кнопку **Создать свою первую переменную** среды.</span><span class="sxs-lookup"><span data-stu-id="1d50d-224">With the newly created environment selected, press **Create your first environment variable**.</span></span>

1. <span data-ttu-id="1d50d-225">`azure_app_url`Введите **имя**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-225">Enter `azure_app_url` for the **Name**.</span></span>  <span data-ttu-id="1d50d-226">Введите URL-адрес сайта Azure (без `https://` ) в качестве **значения**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-226">Enter your Azure site URL (without the `https://`) as the **Value**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="Создание переменной среды":::

   <span data-ttu-id="1d50d-228">Нажмите **кнопку Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-228">Press **Add**.</span></span>

## <a name="update-the-app-manifest"></a><span data-ttu-id="1d50d-229">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="1d50d-229">Update the app manifest</span></span>

<span data-ttu-id="1d50d-230">Манифест приложения загружает вкладку с `localhost` URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="1d50d-230">The app manifest is loading the tab from a `localhost` URL.</span></span>  <span data-ttu-id="1d50d-231">В этом разделе вы отрегулируете манифест приложения для загрузки вкладки из URL-адреса, перечисленного в только что созданной среде.</span><span class="sxs-lookup"><span data-stu-id="1d50d-231">In this section, you will adjust the app manifest to load the tab from the URL listed within the environment you just created.</span></span>

1. <span data-ttu-id="1d50d-232">На боковой панели выберите **основные сведения.**</span><span class="sxs-lookup"><span data-stu-id="1d50d-232">From the sidebar, select **Basic information**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="Выбор базовых сведений":::

1. <span data-ttu-id="1d50d-234">В манифесте есть несколько мест, которые перечисляют `locahost:XXXXX` как часть URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="1d50d-234">There are several places within the manifest that list a `locahost:XXXXX` as part of a URL.</span></span>  <span data-ttu-id="1d50d-235">Замените все случаи (включая фигурные `{{azure_app_url}}` скобки).</span><span class="sxs-lookup"><span data-stu-id="1d50d-235">Replace all occurrences with `{{azure_app_url}}` (including the curly braces).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="Настройка базовых сведений для среды":::

1. <span data-ttu-id="1d50d-237">После завершения нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-237">When complete, press **Save**.</span></span>

1. <span data-ttu-id="1d50d-238">На боковой панели выберите **Возможности**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-238">From the sidebar, select **Capabilities**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="Выбор возможностей":::

1. <span data-ttu-id="1d50d-240">Выберите **личную вкладку**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-240">Select **Personal Tab**.</span></span>
1. <span data-ttu-id="1d50d-241">Рядом с личной **вкладке** выберите тройные точки, а затем выберите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-241">Next to the **Personal Tab**, select the triple dots, then select **Edit**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="Изменение личных параметров вкладок":::

1. <span data-ttu-id="1d50d-243">Замените URL-адрес переменной среды в **полях URL-адрес контента** и **веб-сайта.**</span><span class="sxs-lookup"><span data-stu-id="1d50d-243">Replace the URL with the environment variable within the **Content Url** and **Website Url** fields.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="Изменение URL-адресов личных вкладок":::

1. <span data-ttu-id="1d50d-245">Обновление **прессы**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-245">Press **Update**.</span></span>

1. <span data-ttu-id="1d50d-246">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-246">Press **Save**.</span></span>

1. <span data-ttu-id="1d50d-247">На боковой панели выберите **один вход.**</span><span class="sxs-lookup"><span data-stu-id="1d50d-247">From the sidebar, select **Single Sign-On**.</span></span>

1. <span data-ttu-id="1d50d-248">Замените `localhost` внутри **URI ID приложения** на `{{azure_app_url}}` .</span><span class="sxs-lookup"><span data-stu-id="1d50d-248">Replace the `localhost` within the **Application ID URI** with `{{azure_app_url}}`.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="Изменение единого входного URI приложения":::

1. <span data-ttu-id="1d50d-250">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-250">Press **Save**.</span></span>

1. <span data-ttu-id="1d50d-251">С боковой панели нажмите **домены**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-251">From the sidebar, press **Domains**.</span></span>

1. <span data-ttu-id="1d50d-252">Нажмите **кнопку Добавить домен**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-252">Press **Add a domain**.</span></span>

1. <span data-ttu-id="1d50d-253">Если он не указан как допустимый домен, добавьте его как `{{azure_app_url}}` допустимый домен, нажмите **кнопку Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1d50d-253">If `{{azure_app_url}}` is not listed as a valid domain, add it as a valid domain, then press **Add**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="Добавление домена":::

<span data-ttu-id="1d50d-255">Теперь вы можете использовать кнопку **Preview Teams** в верхней части страницы для запуска приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="1d50d-255">You can now use the **Preview in Teams** button at the top of the page to launch your app within Teams.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d50d-256">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d50d-256">Next steps</span></span>

<span data-ttu-id="1d50d-257">Узнайте о других методах создания Teams приложений:</span><span class="sxs-lookup"><span data-stu-id="1d50d-257">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="1d50d-258">Создание приложения Teams с React</span><span class="sxs-lookup"><span data-stu-id="1d50d-258">Create a Teams app with React</span></span>](first-app-react.md)
- <span data-ttu-id="1d50d-259">[Создание приложения Teams как веб-SharePoint](first-app-spfx.md) (Azure не требуется)</span><span class="sxs-lookup"><span data-stu-id="1d50d-259">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="1d50d-260">Создание приложения-бота для разговоров</span><span class="sxs-lookup"><span data-stu-id="1d50d-260">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="1d50d-261">Создать расширение для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="1d50d-261">Create a messaging extension</span></span>](first-message-extension.md)
