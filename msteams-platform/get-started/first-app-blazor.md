---
title: Начало работы — создайте Teams приложение с помощью Blazor
author: adrianhall
description: Вы сможете быстро разработать приложение Microsoft Teams, которое выводит строку "Hello, World!",  сообщение с Microsoft Teams набор средств и .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: 6a9c7e008e2fb6d77c3314286b09d006bd468c37
ms.sourcegitcommit: 25c02757fe207cdff916ba63aa215f88e24e1d6f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/26/2021
ms.locfileid: "52667456"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a><span data-ttu-id="ffedd-104">Создание и запуск первого Microsoft Teams приложения с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="ffedd-104">Build and run your first Microsoft Teams app with Blazor</span></span>

<span data-ttu-id="ffedd-105">В этом руководстве вы создайте новое приложение Microsoft Teams в .NET/Blazor, которое реализует простое личное приложение для получения информации из microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ffedd-105">In this tutorial, you will create a new Microsoft Teams app in .NET/Blazor that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="ffedd-106">(Личное *приложение включает* набор вкладок для индивидуального использования.)  Во время руководства вы узнаете о структуре приложения Teams, локальном запуске приложения и развертывании приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="ffedd-106">(A *personal app* includes a set of tabs scoped for individual use.)  During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="ffedd-107">Приложение, которое мы построим, выводит основные сведения о текущем пользователе.</span><span class="sxs-lookup"><span data-stu-id="ffedd-107">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="ffedd-108">Когда разрешение будет предоставлено, приложение подключится к Microsoft Graph в качестве текущего пользователя, чтобы получить его полный профиль.</span><span class="sxs-lookup"><span data-stu-id="ffedd-108">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ffedd-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="ffedd-109">Before you begin</span></span>

<span data-ttu-id="ffedd-110">Настройте среду разработки, установив [необходимые компоненты](prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="ffedd-110">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ffedd-111">Необходимые условия для установки</span><span class="sxs-lookup"><span data-stu-id="ffedd-111">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="ffedd-112">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="ffedd-112">Create your project</span></span>

<span data-ttu-id="ffedd-113">Используйте набор средств Teams для создания своего первого проекта.</span><span class="sxs-lookup"><span data-stu-id="ffedd-113">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="ffedd-114">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="ffedd-114">Visual Studio 2019</span></span>](#tab/vs)

1. <span data-ttu-id="ffedd-115">Open Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="ffedd-115">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="ffedd-116">Выберите **Создание нового проекта.**</span><span class="sxs-lookup"><span data-stu-id="ffedd-116">Select **Create a new project**.</span></span>

1. <span data-ttu-id="ffedd-117">Выберите **Microsoft Teams app,** а затем нажмите **кнопку Далее**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-117">Select **Microsoft Teams App**, then press **Next**.</span></span>  <span data-ttu-id="ffedd-118">Чтобы помочь найти шаблон, используйте тип **проекта Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="ffedd-118">To help you find the template, use the project type **Microsoft Teams**.</span></span>

1. <span data-ttu-id="ffedd-119">Дайте проекту и решению хорошее имя, а затем нажмите **кнопку Далее**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-119">Give the project and solution a good name, then press **Next**.</span></span>

1. <span data-ttu-id="ffedd-120">Укайте имя приложения и имя компании, а затем нажмите **кнопку Создать**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-120">Provide the application name and company name, then press **Create**.</span></span>  <span data-ttu-id="ffedd-121">Имя приложения и имя компании отображаются конечным пользователям.</span><span class="sxs-lookup"><span data-stu-id="ffedd-121">The application name and company name are displayed to your end users.</span></span>

1. <span data-ttu-id="ffedd-122">Создание приложения Teams займет несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="ffedd-122">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="ffedd-123">После создания проекта установите единую регистрацию с помощью M365:</span><span class="sxs-lookup"><span data-stu-id="ffedd-123">Once the project is created, set up single sign-on with M365:</span></span>

   - <span data-ttu-id="ffedd-124">Выберите **Project**  >  **TeamsFx**  >  **Configure для SSO...**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-124">Select **Project** > **TeamsFx** > **Configure for SSO...**.</span></span>
   - <span data-ttu-id="ffedd-125">При запросе впишитесь в свою учетную запись администратора M365.</span><span class="sxs-lookup"><span data-stu-id="ffedd-125">When prompted, sign in to your M365 administrator account.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="ffedd-126">Командная строка</span><span class="sxs-lookup"><span data-stu-id="ffedd-126">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="ffedd-127">Откройте терминал и выберите каталог, в котором вы хотите создать проект.</span><span class="sxs-lookup"><span data-stu-id="ffedd-127">Open a Terminal and select the directory where you wish to create the project.</span></span>

1. <span data-ttu-id="ffedd-128">Выполнить `dotnet new -i` установку шаблона из NuGet:</span><span class="sxs-lookup"><span data-stu-id="ffedd-128">Run `dotnet new -i` to install the template from NuGet:</span></span>

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   <span data-ttu-id="ffedd-129">Это необходимо сделать только в первый раз или при обновлении шаблона.</span><span class="sxs-lookup"><span data-stu-id="ffedd-129">You only need to do this the first time or when updating the template.</span></span> <span data-ttu-id="ffedd-130">Проверьте [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) последнюю версию этого пакета.</span><span class="sxs-lookup"><span data-stu-id="ffedd-130">Check [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) for the latest version of this package.</span></span>

1. <span data-ttu-id="ffedd-131">Создание каталога:</span><span class="sxs-lookup"><span data-stu-id="ffedd-131">Create a directory:</span></span>

   ``` bash
   mkdir helloworld
   ```

1. <span data-ttu-id="ffedd-132">Запуск `dotnet new` для создания нового проекта:</span><span class="sxs-lookup"><span data-stu-id="ffedd-132">Run `dotnet new` to create a new project:</span></span>

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. <span data-ttu-id="ffedd-133">После развертывания на эшафоте настройте проект для Teams развертывания:</span><span class="sxs-lookup"><span data-stu-id="ffedd-133">Once scaffolded, configure the project for Teams deployment:</span></span>

   ``` bash
   teamsfx init
   ```

<span data-ttu-id="ffedd-134">Теперь можно открыть решение в Visual Studio для отладки.</span><span class="sxs-lookup"><span data-stu-id="ffedd-134">You can now open the solution in Visual Studio for debugging.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="ffedd-135">Знакомство с исходным кодом</span><span class="sxs-lookup"><span data-stu-id="ffedd-135">Take a tour of the source code</span></span>

<span data-ttu-id="ffedd-136">Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="ffedd-136">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="ffedd-137">После того как набор средств Teams настроит ваш проект, у вас появятся компоненты для создания простого личного приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="ffedd-137">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="ffedd-138">Каталоги и файлы проекта отображаются в области Обозреватель решений в Visual Studio 2019 г.</span><span class="sxs-lookup"><span data-stu-id="ffedd-138">The project directories and files display in the Solution Explorer area of Visual Studio 2019.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Снимок экрана, показывающий файлы проектов приложений для личного приложения в Visual Studio 2019 г.":::

- <span data-ttu-id="ffedd-140">Значки приложений, хранимые как PNG-файлы в `color.png` и `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="ffedd-140">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="ffedd-141">Манифест приложения для публикации на портале разработчиков для Teams хранится в `Properties/manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="ffedd-141">The app manifest for publishing through the Developer Portal for Teams is stored in `Properties/manifest.json`.</span></span>
- <span data-ttu-id="ffedd-142">Контроллер backend предоставляется для `Controllers/BackendController.cs` оказания помощи в проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="ffedd-142">A backend controller is provided in `Controllers/BackendController.cs` for assisting with authentication.</span></span>

<span data-ttu-id="ffedd-143">Так как вы создали приложение вкладки во время установки, Teams набор средств наберет весь необходимый код для базовой вкладки в качестве [сервера Blazor.](/aspnet/core/blazor)</span><span class="sxs-lookup"><span data-stu-id="ffedd-143">Since you created a tab app during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab as a [Blazor Server](/aspnet/core/blazor).</span></span>

- <span data-ttu-id="ffedd-144">`Pages/Tab.razor` является точкой входа переднего приложения.</span><span class="sxs-lookup"><span data-stu-id="ffedd-144">`Pages/Tab.razor` is the front-end application's entry point.</span></span>
- <span data-ttu-id="ffedd-145">`TeamsFx.cs`и `JS/src/index.js` используется для инициализации коммуникаций с Teams хостом.</span><span class="sxs-lookup"><span data-stu-id="ffedd-145">`TeamsFx.cs` and `JS/src/index.js` is used for initializing communications with the Teams host.</span></span>

<span data-ttu-id="ffedd-146">Можно добавить функции backend, добавив в приложение дополнительные ASP.NET Core контроллеры.</span><span class="sxs-lookup"><span data-stu-id="ffedd-146">You can add backend functionality by adding additional ASP.NET Core controllers to your application.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="ffedd-147">Запустите приложение локально</span><span class="sxs-lookup"><span data-stu-id="ffedd-147">Run your app locally</span></span>

<span data-ttu-id="ffedd-148">Набор средств Teams позволяет запускать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="ffedd-148">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="ffedd-149">Нужно выполнить несколько действий для обеспечения правильной инфраструктуры. Teams ожидает, что:</span><span class="sxs-lookup"><span data-stu-id="ffedd-149">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="ffedd-150">Приложение зарегистрировано в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ffedd-150">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="ffedd-151">Оно имеет разрешения, связанные с расположением, из которого загружается, и с любыми ресурсами серверной сторонй, которые использует.</span><span class="sxs-lookup"><span data-stu-id="ffedd-151">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="ffedd-152">Веб-API находится (IIS Express) для оказания помощи в задачах проверки подлинности, выступая в качестве прокси-сервера между приложением и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ffedd-152">A web API is hosted (via IIS Express) to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  
- <span data-ttu-id="ffedd-153">Манифест приложения создается и существует на портале разработчика для Teams.</span><span class="sxs-lookup"><span data-stu-id="ffedd-153">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="ffedd-154">Teams использует манифест приложения, чтобы сообщить подключенным клиентам, откуда загружать приложение.</span><span class="sxs-lookup"><span data-stu-id="ffedd-154">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="ffedd-155">После этого приложение можно загрузить в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="ffedd-155">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="ffedd-156">Мы используем веб-клиент Teams, чтобы иметь возможность видеть код HTML, CSS и JavaScript в стандартной среде веб-разработки.</span><span class="sxs-lookup"><span data-stu-id="ffedd-156">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

<span data-ttu-id="ffedd-157">Чтобы создать и запустить приложение локально, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ffedd-157">To build and run your app locally:</span></span>

1. <span data-ttu-id="ffedd-158">В Visual Studio Code нажмите клавишу **F5**, чтобы запустить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="ffedd-158">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

1. <span data-ttu-id="ffedd-159">При запросе установите самозаверяющийся сертификат SSL для локальной отладки.</span><span class="sxs-lookup"><span data-stu-id="ffedd-159">If requested, install the self-signed SSL certificate for local debugging.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. <span data-ttu-id="ffedd-161">В браузере будет выполнена загрузка Teams, и вам будет предложено войти.</span><span class="sxs-lookup"><span data-stu-id="ffedd-161">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="ffedd-162">При появлении запроса на открытие Microsoft Teams выберите "Отменить", чтобы остаться в браузере.</span><span class="sxs-lookup"><span data-stu-id="ffedd-162">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="ffedd-163">Войдите с помощью своей учетной записи M365.</span><span class="sxs-lookup"><span data-stu-id="ffedd-163">Sign in with your M365 account.</span></span>
1. <span data-ttu-id="ffedd-164">При появлении запроса на установку приложения в Teams нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-164">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="ffedd-165">Откроется окно приложения:</span><span class="sxs-lookup"><span data-stu-id="ffedd-165">Your app will now be displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="Снимок экрана: готовое приложение":::

<span data-ttu-id="ffedd-167">Вы можете проводить обычные действия отладки так же, как если бы это было любое другое веб-приложение (например, установка точек останова).</span><span class="sxs-lookup"><span data-stu-id="ffedd-167">You can do normal debugging activities as if this were any other web application (such as setting breakpoints).</span></span> <span data-ttu-id="ffedd-168">Приложение поддерживает горячую перезагрузку.</span><span class="sxs-lookup"><span data-stu-id="ffedd-168">The app supports hot reloading.</span></span>  <span data-ttu-id="ffedd-169">Если вы измените какой-либо файл в составе проекта, страница будет перезагружена.</span><span class="sxs-lookup"><span data-stu-id="ffedd-169">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="ffedd-170">Узнайте, что происходит при локальном запуске приложения в отладчике.</span><span class="sxs-lookup"><span data-stu-id="ffedd-170">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="ffedd-171">При нажатии клавиши F5 набор средств Teams:</span><span class="sxs-lookup"><span data-stu-id="ffedd-171">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="ffedd-172">Зарегистрировал приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ffedd-172">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="ffedd-173">Зарегистрировал приложение для установки неопубликованных приложений в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ffedd-173">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="ffedd-174">Начался локальный запуск backend приложения.</span><span class="sxs-lookup"><span data-stu-id="ffedd-174">Started your application backend running locally.</span></span>
1. <span data-ttu-id="ffedd-175">Запускает локальную часть приложения, размещенную на клиентской стороне.</span><span class="sxs-lookup"><span data-stu-id="ffedd-175">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="ffedd-176">Начало Microsoft Teams в веб-браузере с командой Teams для боковой загрузки приложения (URL-адрес зарегистрирован в манифесте приложения).</span><span class="sxs-lookup"><span data-stu-id="ffedd-176">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="ffedd-177">Узнайте, как устранить распространенные проблемы при локальном запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="ffedd-177">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="ffedd-178">Чтобы успешно запустить приложение в Teams, необходимо иметь учетную запись Microsoft 365 разработки, которая позволяет загружать приложения в стороне.</span><span class="sxs-lookup"><span data-stu-id="ffedd-178">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app side loading.</span></span> <span data-ttu-id="ffedd-179">Дополнительные сведения о создании учетной записи см. в разделе [Необходимые компоненты](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="ffedd-179">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="ffedd-180">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="ffedd-180">Deploy your app to Azure</span></span>

<span data-ttu-id="ffedd-181">Развертывание состоит из двух этапов.</span><span class="sxs-lookup"><span data-stu-id="ffedd-181">Deployment consists of two steps.</span></span>  <span data-ttu-id="ffedd-182">Сначала создаются необходимые облачные ресурсы (также известные как подготовка), затем код, который составляет ваше приложение, копируется в созданные облачные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ffedd-182">First, necessary cloud resources are created (also known as provisioning), then the code that makes up your app is copied into the created cloud resources.</span></span>

> <span data-ttu-id="ffedd-183">**Предварительный просмотр**</span><span class="sxs-lookup"><span data-stu-id="ffedd-183">**PREVIEW**</span></span>
>
> <span data-ttu-id="ffedd-184">Поддержка приложений Blazor является новой в Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="ffedd-184">Support for Blazor apps is new in Teams Toolkit.</span></span>  <span data-ttu-id="ffedd-185">Подготовка и развертывание делаются с Visual Studio 2019 г. и порталом разработчиков для Teams.</span><span class="sxs-lookup"><span data-stu-id="ffedd-185">Provisioning and deployment are done with a combination of Visual Studio 2019 and the Developer Portal for Teams.</span></span>

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a><span data-ttu-id="ffedd-186">Подготовка и развертывание приложения в Службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="ffedd-186">Provision and deploy your app to Azure App Service</span></span>

1. <span data-ttu-id="ffedd-187">В Обозревателе решений щелкните правой кнопкой мыши узел проекта и выберите **Опубликовать** (или используйте элемент **меню Build**  >  **Publish).**</span><span class="sxs-lookup"><span data-stu-id="ffedd-187">In Solution Explorer, right-click the project node and choose **Publish** (or use the **Build** > **Publish** menu item).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="Выберите операцию Публикация в проекте":::

1. <span data-ttu-id="ffedd-189">В **окне Публикация** выберите **Azure**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-189">In the **Publish** window, select **Azure**.</span></span>  <span data-ttu-id="ffedd-190">Нажмите **кнопку Далее**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-190">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="Выберите Azure в качестве цели публикации":::

1. <span data-ttu-id="ffedd-192">Выберите **службу приложений Azure (Windows).**</span><span class="sxs-lookup"><span data-stu-id="ffedd-192">Select **Azure App Service (Windows)**.</span></span>  <span data-ttu-id="ffedd-193">Нажмите **кнопку Далее**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-193">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="Выберите службу приложений Azure в качестве цели публикации":::

1. <span data-ttu-id="ffedd-195">Выберите **+** для создания нового экземпляра службы приложений.</span><span class="sxs-lookup"><span data-stu-id="ffedd-195">Select **+** to create a new App Service instance.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="Создание нового экземпляра.":::

1. <span data-ttu-id="ffedd-197">В **диалоговом октаге Create App Service (Windows)** заполняются  поля "Имя", "Имя подписки", "Группа ресурсов" и "Планирование размещения". </span><span class="sxs-lookup"><span data-stu-id="ffedd-197">In the **Create App Service (Windows)** dialog, the **Name**, **Subscription name**, **Resource Group**, and **Hosting Plan** entry fields are populated.</span></span> <span data-ttu-id="ffedd-198">Если у вас уже запущена служба приложений, будут выбраны существующие параметры.</span><span class="sxs-lookup"><span data-stu-id="ffedd-198">If you have already got an App Service running, existing settings will be selected.</span></span>  <span data-ttu-id="ffedd-199">Вы можете выбрать создание новой группы ресурсов и плана размещения (Рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="ffedd-199">You can opt to create a new resource group and hosting plan (Recommended).</span></span>  <span data-ttu-id="ffedd-200">Когда вы готовы, выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-200">When ready, select **Create**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="Выбор плана размещения и подписки":::

1. <span data-ttu-id="ffedd-202">В **диалоговом** окте "Публикация" вновь созданный экземпляр выбран автоматически.</span><span class="sxs-lookup"><span data-stu-id="ffedd-202">In the **Publish** dialog, the newly created instance has been automatically selected.</span></span>  <span data-ttu-id="ffedd-203">Когда вы готовы, выберите **Finish**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-203">When ready, select **Finish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="Выберите новый экземпляр.":::

1. <span data-ttu-id="ffedd-205">Нажмите **значок Изменить** (карандаш) рядом с **режимом развертывания,** а затем выберите **автономный**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-205">Press the **Edit** (pencil) icon next to **Deployment Mode**, then select **Self-contained**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="Выберите автономный режим развертывания.":::

1. <span data-ttu-id="ffedd-207">Нажмите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-207">Select **Publish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="Публикация приложения в службу приложений":::

<span data-ttu-id="ffedd-209">Visual Studio развертывает приложение в службе приложений Azure, а веб-приложение загружается в браузере.</span><span class="sxs-lookup"><span data-stu-id="ffedd-209">Visual Studio deploys the app to your Azure App Service, and the web app loads in your browser.</span></span>  <span data-ttu-id="ffedd-210">Добавьте `/tab` в конец URL-адреса, чтобы увидеть свою страницу.</span><span class="sxs-lookup"><span data-stu-id="ffedd-210">Add `/tab` to the end of the URL to see your page.</span></span>

<span data-ttu-id="ffedd-211">В области свойства проекта **Publish** показаны URL-адрес сайта и другие сведения.</span><span class="sxs-lookup"><span data-stu-id="ffedd-211">The project properties **Publish** pane shows the site URL and other details.</span></span> <span data-ttu-id="ffedd-212">Заметьте URL-адрес сайта.</span><span class="sxs-lookup"><span data-stu-id="ffedd-212">Make a note of the site URL.</span></span>

## <a name="create-an-environment-for-your-app"></a><span data-ttu-id="ffedd-213">Создание среды для приложения</span><span class="sxs-lookup"><span data-stu-id="ffedd-213">Create an environment for your app</span></span>

<span data-ttu-id="ffedd-214">Портал разработчиков для Teams управляет загрузкой вкладок для приложения с помощью **среды.**</span><span class="sxs-lookup"><span data-stu-id="ffedd-214">The Developer Portal for Teams manages where the tabs for your app are loaded from with an **Environment**.</span></span>  <span data-ttu-id="ffedd-215">Чтобы создать среду:</span><span class="sxs-lookup"><span data-stu-id="ffedd-215">To create an environment:</span></span>

1. <span data-ttu-id="ffedd-216">Откройте портал [разработчиков для Teams](https://dev.teams.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ffedd-216">Open the [Developer Portal for Teams](https://dev.teams.microsoft.com).</span></span>  <span data-ttu-id="ffedd-217">Во входе с помощью административной учетной записи M365.</span><span class="sxs-lookup"><span data-stu-id="ffedd-217">Sign in with your M365 administrative account.</span></span>

1. <span data-ttu-id="ffedd-218">На боковой панели выберите **Приложения.**</span><span class="sxs-lookup"><span data-stu-id="ffedd-218">From the sidebar, select **Apps**.</span></span>

1. <span data-ttu-id="ffedd-219">Если у вас есть только одно приложение, оно будет выбрано автоматически.</span><span class="sxs-lookup"><span data-stu-id="ffedd-219">If you only have one app, it will be automatically selected.</span></span>  <span data-ttu-id="ffedd-220">Если нет, выберите приложение из списка.</span><span class="sxs-lookup"><span data-stu-id="ffedd-220">If not, select your app from the list.</span></span>

1. <span data-ttu-id="ffedd-221">Выбор **сред**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-221">Select **Environments**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="Выбор сред":::

1. <span data-ttu-id="ffedd-223">Выберите **Создать первую среду.**</span><span class="sxs-lookup"><span data-stu-id="ffedd-223">Select **Create your first environment**.</span></span>

1. <span data-ttu-id="ffedd-224">Введите имя для среды и нажмите кнопку **Добавить;** например _Production_.</span><span class="sxs-lookup"><span data-stu-id="ffedd-224">Enter a name for your environment, then press **Add**; for example _Production_.</span></span>

1. <span data-ttu-id="ffedd-225">После выбора новой среды нажмите кнопку **Создать свою первую переменную** среды.</span><span class="sxs-lookup"><span data-stu-id="ffedd-225">With the newly created environment selected, press **Create your first environment variable**.</span></span>

1. <span data-ttu-id="ffedd-226">`azure_app_url`Введите **имя**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-226">Enter `azure_app_url` for the **Name**.</span></span>  <span data-ttu-id="ffedd-227">Введите URL-адрес сайта Azure (без `https://` ) в качестве **значения**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-227">Enter your Azure site URL (without the `https://`) as the **Value**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="Создание переменной среды":::

   <span data-ttu-id="ffedd-229">Нажмите **кнопку Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-229">Press **Add**.</span></span>

## <a name="update-the-app-manifest"></a><span data-ttu-id="ffedd-230">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="ffedd-230">Update the app manifest</span></span>

<span data-ttu-id="ffedd-231">Манифест приложения загружает вкладку с `localhost` URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="ffedd-231">The app manifest is loading the tab from a `localhost` URL.</span></span>  <span data-ttu-id="ffedd-232">В этом разделе вы отрегулируете манифест приложения для загрузки вкладки из URL-адреса, перечисленного в только что созданной среде.</span><span class="sxs-lookup"><span data-stu-id="ffedd-232">In this section, you will adjust the app manifest to load the tab from the URL listed within the environment you just created.</span></span>

1. <span data-ttu-id="ffedd-233">На боковой панели выберите **основные сведения.**</span><span class="sxs-lookup"><span data-stu-id="ffedd-233">From the sidebar, select **Basic information**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="Выбор базовых сведений":::

1. <span data-ttu-id="ffedd-235">В манифесте есть несколько мест, которые перечисляют `locahost:XXXXX` как часть URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="ffedd-235">There are several places within the manifest that list a `locahost:XXXXX` as part of a URL.</span></span>  <span data-ttu-id="ffedd-236">Замените все случаи (включая фигурные `{{azure_app_url}}` скобки).</span><span class="sxs-lookup"><span data-stu-id="ffedd-236">Replace all occurrences with `{{azure_app_url}}` (including the curly braces).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="Настройка базовых сведений для среды":::

1. <span data-ttu-id="ffedd-238">После завершения нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-238">When complete, press **Save**.</span></span>

1. <span data-ttu-id="ffedd-239">На боковой панели выберите **Возможности**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-239">From the sidebar, select **Capabilities**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="Выбор возможностей":::

1. <span data-ttu-id="ffedd-241">Выберите **личную вкладку**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-241">Select **Personal Tab**.</span></span>
1. <span data-ttu-id="ffedd-242">Рядом с личной **вкладке** выберите тройные точки, а затем выберите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-242">Next to the **Personal Tab**, select the triple dots, then select **Edit**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="Изменение личных параметров вкладок":::

1. <span data-ttu-id="ffedd-244">Замените URL-адрес переменной среды в **полях URL-адрес контента** и **веб-сайта.**</span><span class="sxs-lookup"><span data-stu-id="ffedd-244">Replace the URL with the environment variable within the **Content Url** and **Website Url** fields.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="Изменение URL-адресов личных вкладок":::

1. <span data-ttu-id="ffedd-246">Обновление **прессы**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-246">Press **Update**.</span></span>

1. <span data-ttu-id="ffedd-247">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-247">Press **Save**.</span></span>

1. <span data-ttu-id="ffedd-248">На боковой панели выберите **один вход.**</span><span class="sxs-lookup"><span data-stu-id="ffedd-248">From the sidebar, select **Single Sign-On**.</span></span>

1. <span data-ttu-id="ffedd-249">Замените `localhost` внутри **URI ID приложения** на `{{azure_app_url}}` .</span><span class="sxs-lookup"><span data-stu-id="ffedd-249">Replace the `localhost` within the **Application ID URI** with `{{azure_app_url}}`.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="Изменение единого входного URI приложения":::

1. <span data-ttu-id="ffedd-251">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-251">Press **Save**.</span></span>

1. <span data-ttu-id="ffedd-252">С боковой панели нажмите **домены**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-252">From the sidebar, press **Domains**.</span></span>

1. <span data-ttu-id="ffedd-253">Нажмите **кнопку Добавить домен**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-253">Press **Add a domain**.</span></span>

1. <span data-ttu-id="ffedd-254">Если он не указан как допустимый домен, добавьте его как `{{azure_app_url}}` допустимый домен, нажмите **кнопку Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ffedd-254">If `{{azure_app_url}}` is not listed as a valid domain, add it as a valid domain, then press **Add**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="Добавление домена":::

<span data-ttu-id="ffedd-256">Теперь вы можете использовать кнопку **Preview Teams** в верхней части страницы для запуска приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="ffedd-256">You can now use the **Preview in Teams** button at the top of the page to launch your app within Teams.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffedd-257">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ffedd-257">Next steps</span></span>

<span data-ttu-id="ffedd-258">Узнайте о других методах создания приложений Teams:</span><span class="sxs-lookup"><span data-stu-id="ffedd-258">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="ffedd-259">Создание приложения Teams с помощью React</span><span class="sxs-lookup"><span data-stu-id="ffedd-259">Create a Teams app with React</span></span>](first-app-react.md)
- <span data-ttu-id="ffedd-260">[Создание приложения Teams в формате веб-части SharePoint](first-app-spfx.md) (Azure не требуется)</span><span class="sxs-lookup"><span data-stu-id="ffedd-260">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="ffedd-261">Создание бота беседы</span><span class="sxs-lookup"><span data-stu-id="ffedd-261">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="ffedd-262">Создание расширения для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="ffedd-262">Create a messaging extension</span></span>](first-message-extension.md)
