---
title: Начало работы — создайте Teams приложение с помощью Blazor
author: adrianhall
description: Вы сможете быстро разработать приложение Microsoft Teams, которое выводит строку "Hello, World!",  сообщение с Microsoft Teams набор средств и .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: c14f55d014af120cab88044d31ee8600017e3c57
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254309"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a><span data-ttu-id="3a6ad-104">Создание и запуск первого Microsoft Teams приложения с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="3a6ad-104">Build and run your first Microsoft Teams app with Blazor</span></span>

<span data-ttu-id="3a6ad-105">В этом руководстве вы узнаете, как создать новое приложение Microsoft Teams в .NET/Blazor, которое реализует простое личное приложение для получения информации из microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-105">In this tutorial, you will learn how to create a new Microsoft Teams app in .NET/Blazor that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="3a6ad-106">Например, личное *приложение включает* набор вкладок для индивидуального использования.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-106">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="3a6ad-107">Во время руководства вы узнаете о структуре приложения Teams, локальном запуске приложения и развертывании приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="3a6ad-108">Приложение, которое мы построим, выводит основные сведения о текущем пользователе.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-108">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="3a6ad-109">Когда разрешение будет предоставлено, приложение подключится к Microsoft Graph в качестве текущего пользователя, чтобы получить его полный профиль.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3a6ad-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="3a6ad-110">Before you begin</span></span>

<span data-ttu-id="3a6ad-111">Убедитесь, что среда разработки настроена путем установки необходимых условий.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-111">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3a6ad-112">Необходимые условия для установки</span><span class="sxs-lookup"><span data-stu-id="3a6ad-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="3a6ad-113">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="3a6ad-113">Create your project</span></span>

<span data-ttu-id="3a6ad-114">Используйте набор средств Teams для создания своего первого проекта.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="3a6ad-115">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="3a6ad-115">Visual Studio 2019</span></span>](#tab/vs)

1. <span data-ttu-id="3a6ad-116">Open Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-116">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="3a6ad-117">Выберите **Создание нового проекта.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-117">Select **Create a new project**.</span></span>

1. <span data-ttu-id="3a6ad-118">Выберите **Microsoft Teams App,** а затем выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-118">Select **Microsoft Teams App**, then select **Next**.</span></span>  <span data-ttu-id="3a6ad-119">Чтобы помочь найти шаблон, используйте тип **проекта Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-119">To help you find the template, use the project type **Microsoft Teams**.</span></span>

1. <span data-ttu-id="3a6ad-120">Введите имя и выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-120">Enter a name and select **Next**.</span></span>

1. <span data-ttu-id="3a6ad-121">Введите имя приложения и имя компании.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-121">Enter the application name and company name.</span></span>

1. <span data-ttu-id="3a6ad-122">Нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-122">Select **Create**.</span></span>  <span data-ttu-id="3a6ad-123">Имя приложения и имя компании отображаются конечным пользователям.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-123">The application name and company name are displayed to your end users.</span></span> <span data-ttu-id="3a6ad-124">Создание приложения Teams займет несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-124">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="3a6ad-125">После создания проекта установите единую регистрацию с помощью M365:</span><span class="sxs-lookup"><span data-stu-id="3a6ad-125">After the project is created, set up single sign-on with M365:</span></span>

   1. <span data-ttu-id="3a6ad-126">Выберите **Project**  >  **TeamsFx**  >  **Configure для SSO...**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-126">Select **Project** > **TeamsFx** > **Configure for SSO...**.</span></span>
   1. <span data-ttu-id="3a6ad-127">При запросе впишитесь в свою учетную запись администратора M365.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-127">When prompted, sign in to your M365 administrator account.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="3a6ad-128">Командная строка</span><span class="sxs-lookup"><span data-stu-id="3a6ad-128">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="3a6ad-129">Откройте терминал и выберите каталог, в котором вы хотите создать проект.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-129">Open a Terminal and select the directory where you wish to create the project.</span></span>

1. <span data-ttu-id="3a6ad-130">Выполнить `dotnet new -i` установку шаблона из NuGet:</span><span class="sxs-lookup"><span data-stu-id="3a6ad-130">Run `dotnet new -i` to install the template from NuGet:</span></span>

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   <span data-ttu-id="3a6ad-131">Это необходимо сделать только в первый раз или при обновлении шаблона.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-131">You only need to do this the first time or when updating the template.</span></span> <span data-ttu-id="3a6ad-132">Проверьте [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) последнюю версию этого пакета.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-132">Check [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) for the latest version of this package.</span></span>

1. <span data-ttu-id="3a6ad-133">Создание каталога:</span><span class="sxs-lookup"><span data-stu-id="3a6ad-133">Create a directory:</span></span>

   ``` bash
   mkdir helloworld
   ```

1. <span data-ttu-id="3a6ad-134">Запуск `dotnet new` для создания нового проекта:</span><span class="sxs-lookup"><span data-stu-id="3a6ad-134">Run `dotnet new` to create a new project:</span></span>

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. <span data-ttu-id="3a6ad-135">После строительных лесов настройте проект для Teams развертывания:</span><span class="sxs-lookup"><span data-stu-id="3a6ad-135">After scaffolding, configure the project for Teams deployment:</span></span>

   ``` bash
   teamsfx init
   ```

   <span data-ttu-id="3a6ad-136">Теперь можно открыть решение в Visual Studio для отладки.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-136">You can now open the solution in Visual Studio for debugging.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="3a6ad-137">Знакомство с исходным кодом</span><span class="sxs-lookup"><span data-stu-id="3a6ad-137">Take a tour of the source code</span></span>

<span data-ttu-id="3a6ad-138">Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="3a6ad-138">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="3a6ad-139">После настройки Teams набор средств проекта у вас есть компоненты для создания базового личного приложения для Teams.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-139">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="3a6ad-140">Каталоги и файлы проекта отображаются в области Обозреватель решений в Visual Studio 2019 г.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-140">The project directories and files display in the Solution Explorer area of Visual Studio 2019.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Снимок экрана, показывающий файлы проектов приложений для личного приложения в Visual Studio 2019 г.":::

- <span data-ttu-id="3a6ad-142">Значки приложений, хранимые как PNG-файлы в `color.png` и `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-142">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="3a6ad-143">Манифест приложения для публикации на портале разработчиков для Teams хранится в `Properties/manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="3a6ad-143">The app manifest for publishing through the Developer Portal for Teams is stored in `Properties/manifest.json`.</span></span>
- <span data-ttu-id="3a6ad-144">Контроллер backend предоставляется для `Controllers/BackendController.cs` оказания помощи в проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-144">A backend controller is provided in `Controllers/BackendController.cs` for assisting with authentication.</span></span>

<span data-ttu-id="3a6ad-145">Так как вы создали приложение вкладки во время установки, Teams набор средств наберет весь необходимый код для базовой вкладки в качестве [сервера Blazor.](/aspnet/core/blazor)</span><span class="sxs-lookup"><span data-stu-id="3a6ad-145">Since you created a tab app during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab as a [Blazor Server](/aspnet/core/blazor).</span></span>

- <span data-ttu-id="3a6ad-146">`Pages/Tab.razor` является точкой входа переднего приложения.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-146">`Pages/Tab.razor` is the front-end application's entry point.</span></span>
- <span data-ttu-id="3a6ad-147">`TeamsFx.cs`и `JS/src/index.js` используется для инициализации коммуникаций с Teams хостом.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-147">`TeamsFx.cs` and `JS/src/index.js` is used for initializing communications with the Teams host.</span></span>

<span data-ttu-id="3a6ad-148">Можно добавить функции backend, добавив в приложение дополнительные ASP.NET Core контроллеры.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-148">You can add backend functionality by adding additional ASP.NET Core controllers to your application.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="3a6ad-149">Запустите приложение локально</span><span class="sxs-lookup"><span data-stu-id="3a6ad-149">Run your app locally</span></span>

<span data-ttu-id="3a6ad-150">Набор средств Teams позволяет запускать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-150">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="3a6ad-151">Нужно выполнить несколько действий для обеспечения правильной инфраструктуры. Teams ожидает, что:</span><span class="sxs-lookup"><span data-stu-id="3a6ad-151">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="3a6ad-152">Приложение зарегистрировано в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-152">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="3a6ad-153">Оно имеет разрешения, связанные с расположением, из которого загружается, и с любыми ресурсами серверной сторонй, которые использует.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-153">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="3a6ad-154">Веб-API находится (IIS Express) для оказания помощи в задачах проверки подлинности, выступая в качестве прокси-сервера между приложением и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-154">A web API is hosted (via IIS Express) to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  
- <span data-ttu-id="3a6ad-155">Манифест приложения создается и существует на портале разработчика для Teams.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-155">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="3a6ad-156">Teams использует манифест приложения, чтобы сообщить подключенным клиентам, откуда загружать приложение.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-156">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="3a6ad-157">После этого приложение может быть загружено в клиенте Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-157">After this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="3a6ad-158">Мы используем веб-клиент Teams, чтобы иметь возможность видеть код HTML, CSS и JavaScript в стандартной среде веб-разработки.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-158">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

<span data-ttu-id="3a6ad-159">Чтобы создать и запустить приложение локально, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-159">To build and run your app locally:</span></span>


1. <span data-ttu-id="3a6ad-160">С Visual Studio Code нажмите **клавишу F5,** чтобы запустить приложение в режиме отлаживания.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-160">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>


1. <span data-ttu-id="3a6ad-161">При запросе установите самозаверяющийся сертификат SSL для локальной отладки.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-161">If requested, install the self-signed SSL certificate for local debugging.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. <span data-ttu-id="3a6ad-163">В браузере будет выполнена загрузка Teams, и вам будет предложено войти.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-163">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="3a6ad-164">При появлении запроса на открытие Microsoft Teams выберите "Отменить", чтобы остаться в браузере.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-164">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="3a6ad-165">Войдите с помощью своей учетной записи M365.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-165">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="3a6ad-166">Если вам предложено установить приложение на Teams, выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-166">When prompted to install the app onto Teams, select **Add**.</span></span>

   <span data-ttu-id="3a6ad-167">Откроется окно приложения:</span><span class="sxs-lookup"><span data-stu-id="3a6ad-167">Your app will now be displayed:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="Снимок экрана: готовое приложение":::

   <span data-ttu-id="3a6ad-169">Вы можете выполнять отладку действий, как если бы это было любое другое веб-приложение, как установка точек перерывов.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-169">You can perform the debugging activities as if this were any other web application like setting breakpoints.</span></span> <span data-ttu-id="3a6ad-170">Приложение поддерживает горячую перезагрузку.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-170">The app supports hot reloading.</span></span>  <span data-ttu-id="3a6ad-171">Если вы измените какой-либо файл в составе проекта, страница будет перезагружена.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-171">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="3a6ad-172">Узнайте, что происходит при локальном запуске приложения в отладчике.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-172">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="3a6ad-173">При нажатии **клавиши F5** Teams набор средств:</span><span class="sxs-lookup"><span data-stu-id="3a6ad-173">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="3a6ad-174">Регистрирует приложение с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-174">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="3a6ad-175">Регистрирует приложение для "боковой загрузки" в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-175">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="3a6ad-176">Запускается локализованная задатка приложения.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-176">Starts your application backend running locally.</span></span>
1. <span data-ttu-id="3a6ad-177">Запускает локальное локальное хостинг приложения.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-177">Starts your application front-end hosted locally.</span></span>
1. <span data-ttu-id="3a6ad-178">Запускает Microsoft Teams в веб-браузере с командой Teams для боковой загрузки приложения (URL-адрес зарегистрирован в манифесте приложения).</span><span class="sxs-lookup"><span data-stu-id="3a6ad-178">Starts Microsoft Teams in a web browser with a command to instruct Teams to side load the application (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="3a6ad-179">Узнайте, как устранить распространенные проблемы при локальном запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-179">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="3a6ad-180">Чтобы успешно запустить приложение в Teams, необходимо иметь учетную запись Microsoft 365 разработки, которая позволяет загружать приложения в стороне.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-180">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app side loading.</span></span> <span data-ttu-id="3a6ad-181">Дополнительные сведения о создании учетной записи см. в разделе [Необходимые компоненты](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="3a6ad-181">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="3a6ad-182">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="3a6ad-182">Deploy your app to Azure</span></span>

<span data-ttu-id="3a6ad-183">Развертывание состоит из двух этапов:</span><span class="sxs-lookup"><span data-stu-id="3a6ad-183">Deployment consists of two steps:</span></span> 

1. <span data-ttu-id="3a6ad-184">Создаются необходимые облачные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-184">Necessary cloud resources are created.</span></span> <span data-ttu-id="3a6ad-185">Это также называется подготовка.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-185">This is also known as provisioning.</span></span>
1. <span data-ttu-id="3a6ad-186">Начните кодирование и скопируйте приложение в созданные облачные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-186">Start coding and copy your app into the created cloud resources.</span></span>

> <span data-ttu-id="3a6ad-187">**Предварительный просмотр**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-187">**PREVIEW**</span></span>
>
> <span data-ttu-id="3a6ad-188">Поддержка приложений Blazor является новой в Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-188">Support for Blazor apps is new in Teams Toolkit.</span></span>  <span data-ttu-id="3a6ad-189">Подготовка и развертывание делаются с Visual Studio 2019 г. и порталом разработчиков для Teams.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-189">Provisioning and deployment are done with a combination of Visual Studio 2019 and the Developer Portal for Teams.</span></span>

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a><span data-ttu-id="3a6ad-190">Подготовка и развертывание приложения в Службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="3a6ad-190">Provision and deploy your app to Azure App Service</span></span>

1. <span data-ttu-id="3a6ad-191">В Обозревателе решений щелкните правой кнопкой мыши узел проекта и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-191">In Solution Explorer, right-click the project node and select **Publish**.</span></span> <span data-ttu-id="3a6ad-192">Вы также можете использовать элемент **меню Build**  >  **Publish.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-192">You can also use the **Build** > **Publish** menu item.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="Выберите операцию Публикация в проекте":::

1. <span data-ttu-id="3a6ad-194">В **окне Публикация** выберите **Azure** и selct **Next**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-194">In the **Publish** window, select **Azure** and selct **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="Выберите Azure в качестве цели публикации":::

1. <span data-ttu-id="3a6ad-196">Выберите **службу приложений Azure (Windows)** и выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-196">Select **Azure App Service (Windows)** and select **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="Выберите службу приложений Azure в качестве цели публикации":::

1. <span data-ttu-id="3a6ad-198">Выберите **+** для создания нового экземпляра службы приложений.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-198">Select **+** to create a new App Service instance.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="Создание нового экземпляра.":::

1. <span data-ttu-id="3a6ad-200">В **диалоговом октаге Create App Service (Windows)** заполняются  поля "Имя", "Имя подписки", "Группа ресурсов" и "Планирование размещения". </span><span class="sxs-lookup"><span data-stu-id="3a6ad-200">In the **Create App Service (Windows)** dialog, the **Name**, **Subscription name**, **Resource Group**, and **Hosting Plan** entry fields are populated.</span></span> <span data-ttu-id="3a6ad-201">Если у вас уже запущена служба приложений, выбираются существующие параметры.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-201">If you have already got an App Service running, existing settings are selected.</span></span>  <span data-ttu-id="3a6ad-202">Вы можете выбрать создание новой группы ресурсов и плана размещения.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-202">You can opt to create a new resource group and hosting plan.</span></span>  <span data-ttu-id="3a6ad-203">Когда вы готовы, выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-203">When ready, select **Create**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="Выбор плана размещения и подписки":::

1. <span data-ttu-id="3a6ad-205">В **диалоговом** окте "Публикация" вновь созданный экземпляр выбран автоматически.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-205">In the **Publish** dialog, the newly created instance has been automatically selected.</span></span>  <span data-ttu-id="3a6ad-206">Когда вы готовы, выберите **Finish**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-206">When ready, select **Finish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="Выберите новый экземпляр.":::

1. <span data-ttu-id="3a6ad-208">Выберите **значок Редактирование** (карандаш) рядом с **режимом развертывания** и выберите **автономный**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-208">Select the **Edit** (pencil) icon next to **Deployment Mode**, and select **Self-contained**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="Выберите автономный режим развертывания.":::

1. <span data-ttu-id="3a6ad-210">Нажмите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-210">Select **Publish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="Публикация приложения в службу приложений":::

   <span data-ttu-id="3a6ad-212">Visual Studio развертывает приложение в службе приложений Azure, а веб-приложение загружается в браузере.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-212">Visual Studio deploys the app to your Azure App Service, and the web app loads in your browser.</span></span>  <span data-ttu-id="3a6ad-213">Добавьте `/tab` в конец URL-адреса, чтобы увидеть свою страницу.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-213">Add `/tab` to the end of the URL to see your page.</span></span>

   <span data-ttu-id="3a6ad-214">В области свойства проекта **Publish** показаны URL-адрес сайта и другие сведения.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-214">The project properties **Publish** pane shows the site URL and other details.</span></span> <span data-ttu-id="3a6ad-215">Заметьте URL-адрес сайта.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-215">Make a note of the site URL.</span></span>

## <a name="create-an-environment-for-your-app"></a><span data-ttu-id="3a6ad-216">Создание среды для приложения</span><span class="sxs-lookup"><span data-stu-id="3a6ad-216">Create an environment for your app</span></span>

<span data-ttu-id="3a6ad-217">Портал разработчиков для Teams управляет загрузкой вкладок для приложения с помощью **среды.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-217">The Developer Portal for Teams manages where the tabs for your app are loaded from with an **Environment**.</span></span>  

<span data-ttu-id="3a6ad-218">**Чтобы создать среду:**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-218">**To create an environment:**</span></span>

1. <span data-ttu-id="3a6ad-219">Откройте портал [разработчиков для Teams](https://dev.teams.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3a6ad-219">Open the [Developer Portal for Teams](https://dev.teams.microsoft.com).</span></span>  <span data-ttu-id="3a6ad-220">Во входе с помощью административной учетной записи M365.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-220">Sign in with your M365 administrative account.</span></span>

1. <span data-ttu-id="3a6ad-221">На боковой панели выберите **Приложения.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-221">From the sidebar, select **Apps**.</span></span>

1. <span data-ttu-id="3a6ad-222">Если у вас есть только одно приложение, оно будет выбрано автоматически.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-222">If you only have one app, it will be automatically selected.</span></span>  <span data-ttu-id="3a6ad-223">Если нет, выберите приложение из списка.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-223">If not, select your app from the list.</span></span>

1. <span data-ttu-id="3a6ad-224">Выбор **сред**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-224">Select **Environments**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="Выбор сред":::

1. <span data-ttu-id="3a6ad-226">Выберите **Создать первую среду.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-226">Select **Create your first environment**.</span></span>

1. <span data-ttu-id="3a6ad-227">Введите имя для среды и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-227">Enter a name for your environment and select **Add**.</span></span> <span data-ttu-id="3a6ad-228">Например, `_Production_`.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-228">For example, `_Production_`.</span></span>

1. <span data-ttu-id="3a6ad-229">Выберите **Создать свою первую переменную среды.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-229">Select **Create your first environment variable**.</span></span>

1. <span data-ttu-id="3a6ad-230">`azure_app_url`Введите **имя**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-230">Enter `azure_app_url` for the **Name**.</span></span>  <span data-ttu-id="3a6ad-231">Введите URL-адрес сайта Azure без `https://` значения **.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-231">Enter your Azure site URL without the `https://` as the **Value**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="Создание переменной среды":::

   <span data-ttu-id="3a6ad-233">Нажмите **кнопку Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-233">Press **Add**.</span></span>

## <a name="update-the-app-manifest"></a><span data-ttu-id="3a6ad-234">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="3a6ad-234">Update the app manifest</span></span>

<span data-ttu-id="3a6ad-235">Манифест приложения загружает вкладку с `localhost` URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-235">The app manifest loads the tab from a `localhost` URL.</span></span>  <span data-ttu-id="3a6ad-236">В этом разделе вы настроит манифест приложения для загрузки вкладки из URL-адреса, перечисленного в только что созданной среде.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-236">In this section, you will configure the app manifest to load the tab from the URL listed within the environment you just created.</span></span>

1. <span data-ttu-id="3a6ad-237">На боковой панели выберите **основные сведения.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-237">From the sidebar, select **Basic information**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="Выбор базовых сведений":::

1. <span data-ttu-id="3a6ad-239">В манифесте есть несколько мест, которые перечисляют `locahost:XXXXX` как часть URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-239">There are several places within the manifest that list a `locahost:XXXXX` as part of a URL.</span></span>  <span data-ttu-id="3a6ad-240">Замените все `{{azure_app_url}}` случаи, включая фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-240">Replace all occurrences with `{{azure_app_url}}`, including the curly braces.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="Настройка базовых сведений для среды":::

1. <span data-ttu-id="3a6ad-242">После завершения выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-242">When complete, select **Save**.</span></span>

1. <span data-ttu-id="3a6ad-243">На боковой панели выберите **Возможности**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-243">From the sidebar, select **Capabilities**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="Выбор возможностей":::

1. <span data-ttu-id="3a6ad-245">Выберите **личную вкладку**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-245">Select **Personal Tab**.</span></span>
1. <span data-ttu-id="3a6ad-246">Рядом с личной **вкладке** выберите тройные точки, а затем выберите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-246">Next to the **Personal Tab**, select the triple dots, then select **Edit**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="Изменение личных параметров вкладок":::

1. <span data-ttu-id="3a6ad-248">Замените URL-адрес переменной среды в **полях URL-адрес контента** и **веб-сайта.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-248">Replace the URL with the environment variable within the **Content Url** and **Website Url** fields.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="Изменение URL-адресов личных вкладок":::

1. <span data-ttu-id="3a6ad-250">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-250">Select **Update**.</span></span>

1. <span data-ttu-id="3a6ad-251">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-251">Select **Save**.</span></span>

1. <span data-ttu-id="3a6ad-252">На боковой панели выберите **один вход.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-252">From the sidebar, select **Single Sign-On**.</span></span>

1. <span data-ttu-id="3a6ad-253">Замените `localhost` внутри **URI ID приложения** на `{{azure_app_url}}` .</span><span class="sxs-lookup"><span data-stu-id="3a6ad-253">Replace the `localhost` within the **Application ID URI** with `{{azure_app_url}}`.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="Изменение единого входного URI приложения":::

1. <span data-ttu-id="3a6ad-255">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-255">Select **Save**.</span></span>

1. <span data-ttu-id="3a6ad-256">На боковой панели выберите **домены.**</span><span class="sxs-lookup"><span data-stu-id="3a6ad-256">From the sidebar, select **Domains**.</span></span>

1. <span data-ttu-id="3a6ad-257">Выберите пункт **Добавить домен**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-257">Select **Add a domain**.</span></span>

1. <span data-ttu-id="3a6ad-258">Если домен не указан как допустимый, добавьте его как `{{azure_app_url}}` допустимый домен, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-258">If `{{azure_app_url}}` is not listed as a valid domain, add it as a valid domain, then select **Add**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="Добавление домена":::

   <span data-ttu-id="3a6ad-260">Теперь вы можете использовать параметр **Preview Teams** в верхней части страницы для запуска приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="3a6ad-260">You can now use the **Preview in Teams** option at the top of the page to launch your app within Teams.</span></span>

## <a name="see-also"></a><span data-ttu-id="3a6ad-261">См. также</span><span class="sxs-lookup"><span data-stu-id="3a6ad-261">See also</span></span>

* [<span data-ttu-id="3a6ad-262">Обзор учебников</span><span class="sxs-lookup"><span data-stu-id="3a6ad-262">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="3a6ad-263">Создание бота беседы</span><span class="sxs-lookup"><span data-stu-id="3a6ad-263">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="3a6ad-264">Создание расширения для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="3a6ad-264">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="3a6ad-265">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="3a6ad-265">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
