---
title: 'Начало работы : создайте свое первое приложение Teams на основе React'
author: adrianhall
description: Вы сможете быстро разработать приложение Microsoft Teams, которое выводит строку "Hello, World!",  на базе набора средств Microsoft Teams и библиотеки React.
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: edd7cf8048dd89156b4b91afecb329d91baf3f53
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994116"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a><span data-ttu-id="ae59d-104">Создайте и запустите свое первое приложение Microsoft Teams, пользуясь библиотекой React</span><span class="sxs-lookup"><span data-stu-id="ae59d-104">Build and run your first Microsoft Teams app with React</span></span>

<span data-ttu-id="ae59d-105">В этом руководстве вы создадите приложение Microsoft Teams в React — реализацию простого личного приложения, получающего информацию из Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ae59d-105">In this tutorial, you will create a new Microsoft Teams app in React that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="ae59d-106">Например, личное *приложение включает* набор вкладок для индивидуального использования.</span><span class="sxs-lookup"><span data-stu-id="ae59d-106">For example, a *personal app* includes a set of tabs scoped for individual use.</span></span> <span data-ttu-id="ae59d-107">Во время руководства вы узнаете о структуре приложения Teams, локальном запуске приложения и развертывании приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="ae59d-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="ae59d-108">Приложение, которое мы построим, выводит основные сведения о текущем пользователе.</span><span class="sxs-lookup"><span data-stu-id="ae59d-108">The app that is built displays basic user information for the current user.</span></span> <span data-ttu-id="ae59d-109">Когда разрешение будет предоставлено, приложение подключится к Microsoft Graph в качестве текущего пользователя, чтобы получить его полный профиль.</span><span class="sxs-lookup"><span data-stu-id="ae59d-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ae59d-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="ae59d-110">Before you begin</span></span>

<span data-ttu-id="ae59d-111">Убедитесь, что среда разработки настроена путем установки [необходимых условий.](prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="ae59d-111">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae59d-112">Необходимые условия для установки</span><span class="sxs-lookup"><span data-stu-id="ae59d-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="ae59d-113">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="ae59d-113">Create your project</span></span>

<span data-ttu-id="ae59d-114">Используйте набор средств Teams для создания своего первого проекта.</span><span class="sxs-lookup"><span data-stu-id="ae59d-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="ae59d-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ae59d-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="ae59d-116">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ae59d-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="ae59d-117">Откройте набор средств Teams, выбрав значок Teams на боковой панели:</span><span class="sxs-lookup"><span data-stu-id="ae59d-117">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. <span data-ttu-id="ae59d-119">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. <span data-ttu-id="ae59d-121">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания проекта":::

1. <span data-ttu-id="ae59d-123">На **шаге Выбор возможностей** уже выбрана возможность **Tab.**</span><span class="sxs-lookup"><span data-stu-id="ae59d-123">On the **Select capabilities** step, the **Tab** capability is already selected.</span></span> <span data-ttu-id="ae59d-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-124">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. <span data-ttu-id="ae59d-126">На шаге **Тип размещения на клиенте** выберите **Azure**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-126">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Снимок экрана: выбор размещения для нового приложения.":::

1. <span data-ttu-id="ae59d-128">На этапе **Облачные ресурсы** нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-128">On the **Cloud resources** step, press **OK**.</span></span>  <span data-ttu-id="ae59d-129">В этом руководстве вам не понадобятся дополнительные облачные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ae59d-129">We do not need additional cloud resources for this tutorial.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Снимок экрана: добавление облачных ресурсов в новое приложение.":::

1. <span data-ttu-id="ae59d-131">На этапе **Язык программирования** выберите **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-131">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Снимок экрана: выбор языка.":::

1. <span data-ttu-id="ae59d-133">Выберите папку рабочей области.</span><span class="sxs-lookup"><span data-stu-id="ae59d-133">Select a workspace folder.</span></span> <span data-ttu-id="ae59d-134">Папка создается в папке рабочего пространства для созданного вами проекта.</span><span class="sxs-lookup"><span data-stu-id="ae59d-134">A folder is created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="ae59d-135">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-135">Enter a suitable name for your app, like `helloworld`.</span></span> <span data-ttu-id="ae59d-136">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="ae59d-136">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="ae59d-137">Чтобы продолжить, нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-137">Press **Enter** to continue.</span></span>

<span data-ttu-id="ae59d-138">Приложение Teams создается в течение нескольких секунд.</span><span class="sxs-lookup"><span data-stu-id="ae59d-138">Your Teams app is created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="ae59d-139">Командная строка</span><span class="sxs-lookup"><span data-stu-id="ae59d-139">Command line</span></span>](#tab/cli)

<span data-ttu-id="ae59d-140">Используйте для создания первого проекта интерфейс командной строки `teamsfx`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-140">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="ae59d-141">Начните с папки, в которой будет создана папка проекта.</span><span class="sxs-lookup"><span data-stu-id="ae59d-141">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="ae59d-142">Интерфейс командной строки выдаст несколько вопросов, ответы на которые используются для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="ae59d-142">The CLI walks through some questions to create the project.</span></span> <span data-ttu-id="ae59d-143">На каждом вопросе будет посвеяно, как ответить на него, например, использовать клавиши со стрелками для выбора варианта.</span><span class="sxs-lookup"><span data-stu-id="ae59d-143">Each question will tell you how to answer it, for example, use arrow keys to select an option.</span></span> <span data-ttu-id="ae59d-144">Ответив на вопрос, подтвердите свой выбор, нажав клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-144">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="ae59d-145">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-145">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="ae59d-146">Выберите возможность **Вкладка**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-146">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="ae59d-147">В качестве размещения на клиенте выберите **Azure**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-147">Select **Azure** frontend hosting.</span></span>
1. <span data-ttu-id="ae59d-148">Не добавляйте облачные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ae59d-148">Do not select any cloud resources.</span></span>
1. <span data-ttu-id="ae59d-149">Выберите **JavaScript** в качестве языка программирования.</span><span class="sxs-lookup"><span data-stu-id="ae59d-149">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="ae59d-150">Нажмите клавишу **ВВОД**, чтобы выбрать папку рабочей области по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ae59d-150">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="ae59d-151">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-151">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="ae59d-152">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="ae59d-152">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="ae59d-153">После ответа на все вопросы создается проект.</span><span class="sxs-lookup"><span data-stu-id="ae59d-153">Once all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="ae59d-154">Знакомство с исходным кодом</span><span class="sxs-lookup"><span data-stu-id="ae59d-154">Take a tour of the source code</span></span>

<span data-ttu-id="ae59d-155">Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="ae59d-155">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="ae59d-156">После того как набор средств Teams настроит ваш проект, у вас появятся компоненты для создания простого личного приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="ae59d-156">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="ae59d-157">Каталоги и файлы проекта отображаются в области проводника Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ae59d-157">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="Снимок экрана: файлы проектов приложения для личного приложения в Visual Studio Code.":::

<span data-ttu-id="ae59d-159">Набор средств автоматически формирует шаблоны в каталоге проекта на основе возможностей, добавленных во время установки.</span><span class="sxs-lookup"><span data-stu-id="ae59d-159">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="ae59d-160">Набор средств Teams сохраняет свое состояние для вашего приложения в каталоге `.fx`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-160">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="ae59d-161">Среди других элементов в этом каталоге находятся:</span><span class="sxs-lookup"><span data-stu-id="ae59d-161">Among other items in this directory:</span></span>

- <span data-ttu-id="ae59d-162">Значки приложений, хранимые как PNG-файлы в `color.png` и `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-162">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="ae59d-163">Манифест приложения для публикации на портале разработчика для Teams, хранимый в `manifest.source.json`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-163">The app manifest for publishing to the Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="ae59d-164">Параметры, выбранные при создании проекта, хранятся в `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-164">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="ae59d-165">Так как вы выбрали вкладку во время настройки, набор средств Teams создает шаблоны всего необходимого кода для программирования базовой вкладки в каталоге `tabs`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-165">Since you selected the tab capability during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab in the `tabs` directory.</span></span> <span data-ttu-id="ae59d-166">В этом каталоге есть несколько важных файлов:</span><span class="sxs-lookup"><span data-stu-id="ae59d-166">Within this directory there are several important files:</span></span>

- <span data-ttu-id="ae59d-167">`tabs/src/index.jsx` — точка входа приложения на клиентской стороне, где проводится отрисовка основного компонента `App` с помощью `ReactDOM.render()`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-167">`tabs/src/index.jsx` is the front-end app's entry point, where the main `App` component is rendered with `ReactDOM.render()`.</span></span>
- <span data-ttu-id="ae59d-168">`tabs/src/components/App.jsx` несет ответственность за маршрутизацию URL-адресов в приложении.</span><span class="sxs-lookup"><span data-stu-id="ae59d-168">`tabs/src/components/App.jsx` handles URL routing in your app.</span></span> <span data-ttu-id="ae59d-169">Он вызывает [SDK JavaScript для Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md), чтобы реализовать обмен сообщениями между вашим приложением и Teams.</span><span class="sxs-lookup"><span data-stu-id="ae59d-169">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>
- <span data-ttu-id="ae59d-170">`tabs/src/components/Tab.jsx` содержит код для реализации пользовательского интерфейса вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ae59d-170">`tabs/src/components/Tab.jsx` contains the code to implement the UI of your app.</span></span>
- <span data-ttu-id="ae59d-171">`tabs/src/components/TabConfig.jsx` содержит код для реализации пользовательского интерфейса настройки вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ae59d-171">`tabs/src/components/TabConfig.jsx` contains the code to implement the UI that configures your app.</span></span>

<span data-ttu-id="ae59d-172">Среде выполнения Teams требуется несколько вкладок, в том числе для уведомления о конфиденциальности, для условий использования и для настроек.</span><span class="sxs-lookup"><span data-stu-id="ae59d-172">Several tabs are required by the Teams runtime, including the privacy notice, terms of use, and configuration tabs.</span></span>  <span data-ttu-id="ae59d-173">Код уведомления о конфиденциальности и условия использования находятся в том же каталоге.</span><span class="sxs-lookup"><span data-stu-id="ae59d-173">The code for the privacy notice and terms of use are located in the same directory.</span></span>

<span data-ttu-id="ae59d-174">При добавлении функций облака в проект добавляются дополнительные каталоги.</span><span class="sxs-lookup"><span data-stu-id="ae59d-174">When you add cloud functionality, additional directories are added to the project.</span></span>  <span data-ttu-id="ae59d-175">В первую очередь, каталог `api` содержит код для всех разработанных вами функций Azure.</span><span class="sxs-lookup"><span data-stu-id="ae59d-175">Most notably, the `api` directory holds the code to any Azure Functions you write.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="ae59d-176">Запустите приложение локально</span><span class="sxs-lookup"><span data-stu-id="ae59d-176">Run your app locally</span></span>

<span data-ttu-id="ae59d-177">Набор средств Teams позволяет запускать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="ae59d-177">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="ae59d-178">Нужно выполнить несколько действий для обеспечения правильной инфраструктуры. Teams ожидает, что:</span><span class="sxs-lookup"><span data-stu-id="ae59d-178">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="ae59d-179">Приложение зарегистрировано в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ae59d-179">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="ae59d-180">Оно имеет разрешения, связанные с расположением, из которого загружается, и с любыми ресурсами серверной сторонй, которые использует.</span><span class="sxs-lookup"><span data-stu-id="ae59d-180">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="ae59d-181">Веб-API позволяет выполнять задачи проверки подлинности, действуя в качестве прокси-сервера между приложением и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ae59d-181">A web API is hosted to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  <span data-ttu-id="ae59d-182">Этим занимается набор инструментов Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="ae59d-182">This is run by Azure Functions Core Tools.</span></span>  <span data-ttu-id="ae59d-183">Доступ к нему можно получить по URL `https://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-183">It can be accessed at the URL `https://localhost:5000`.</span></span>
- <span data-ttu-id="ae59d-184">Ресурсы HTML, CSS и JavaScript, которые составляют клиентскую часть приложения, размещены в локальной службе.</span><span class="sxs-lookup"><span data-stu-id="ae59d-184">The HTML, CSS, and JavaScript resources that make up the front end of the app are hosted on a local service.</span></span> <span data-ttu-id="ae59d-185">Доступ к ней можно получить по URL `https://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-185">It can be accessed at `https://localhost:3000`.</span></span>
- <span data-ttu-id="ae59d-186">Манифест приложения создается и существует на портале разработчика для Teams.</span><span class="sxs-lookup"><span data-stu-id="ae59d-186">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="ae59d-187">Teams использует манифест приложения, чтобы сообщить подключенным клиентам, откуда загружать приложение.</span><span class="sxs-lookup"><span data-stu-id="ae59d-187">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="ae59d-188">После этого приложение можно загрузить в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="ae59d-188">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="ae59d-189">Мы используем веб-клиент Teams, чтобы иметь возможность видеть код HTML, CSS и JavaScript в стандартной среде веб-разработки.</span><span class="sxs-lookup"><span data-stu-id="ae59d-189">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="ae59d-190">Создайте и запустите приложение локально в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ae59d-190">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="ae59d-191">Чтобы создать и запустить приложение локально, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ae59d-191">To build and run your app locally:</span></span>

1. <span data-ttu-id="ae59d-192">В Visual Studio Code нажмите клавишу **F5**, чтобы запустить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="ae59d-192">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="ae59d-193">При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.</span><span class="sxs-lookup"><span data-stu-id="ae59d-193">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="ae59d-194">По завершении сборки автоматически откроется окно браузера.</span><span class="sxs-lookup"><span data-stu-id="ae59d-194">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="ae59d-195">Для завершения может потребоваться от 3 до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="ae59d-195">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="ae59d-196">В набор средств необходимо установить локальный сертификат.</span><span class="sxs-lookup"><span data-stu-id="ae59d-196">The Toolkit prompts you to install a local certificate if required.</span></span> <span data-ttu-id="ae59d-197">Этот сертификат позволяет Teams загружать приложение из `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="ae59d-197">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="ae59d-198">Выберите "Да", когда появится следующее диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="ae59d-198">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. <span data-ttu-id="ae59d-200">Веб-браузер начинает запускать приложение.</span><span class="sxs-lookup"><span data-stu-id="ae59d-200">Your web browser starts to run the app.</span></span> <span data-ttu-id="ae59d-201">Если вам будет предложено открыть Teams рабочий стол, выберите **Отмена,** чтобы оставаться в браузере.</span><span class="sxs-lookup"><span data-stu-id="ae59d-201">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="ae59d-202">Вам также может быть предложено перейти на рабочий Teams в другое время; выберите Teams веб-приложение, когда это произойдет.</span><span class="sxs-lookup"><span data-stu-id="ae59d-202">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Снимок экрана: выбор веб-версии Teams при запуске":::

1. <span data-ttu-id="ae59d-204">Вам может быть предложено выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="ae59d-204">You may be prompted to sign in.</span></span>  <span data-ttu-id="ae59d-205">В этом случае войдите с учетной записью M365.</span><span class="sxs-lookup"><span data-stu-id="ae59d-205">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="ae59d-206">При появлении запроса на установку приложения в Teams нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-206">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="ae59d-207">Теперь ваше приложение отображается:</span><span class="sxs-lookup"><span data-stu-id="ae59d-207">Your app is now displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="Снимок экрана: готовое приложение":::

<span data-ttu-id="ae59d-209">Вы можете делать обычные действия отладки, как если бы это было любое другое веб-приложение, например настройка точек остановок.</span><span class="sxs-lookup"><span data-stu-id="ae59d-209">You can do normal debugging activities as if this were any other web application, such as setting breakpoints.</span></span> <span data-ttu-id="ae59d-210">Приложение поддерживает горячую перезагрузку.</span><span class="sxs-lookup"><span data-stu-id="ae59d-210">The app supports hot reloading.</span></span> <span data-ttu-id="ae59d-211">Если вы измените какой-либо файл в составе проекта, страница будет перезагружена.</span><span class="sxs-lookup"><span data-stu-id="ae59d-211">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="ae59d-212">Узнайте, что происходит при локальном запуске приложения в отладчике.</span><span class="sxs-lookup"><span data-stu-id="ae59d-212">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="ae59d-213">При нажатии клавиши F5 набор средств Teams:</span><span class="sxs-lookup"><span data-stu-id="ae59d-213">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="ae59d-214">Регистрирует приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ae59d-214">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="ae59d-215">*Загружает неопубликованное* приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="ae59d-215">*Sideloaded* your app in Teams.</span></span>
1. <span data-ttu-id="ae59d-216">Запускает серверную часть приложения локально с помощью [Azure Functions Core Tools](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="ae59d-216">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="ae59d-217">Запускает локальную часть приложения, размещенную на клиентской стороне.</span><span class="sxs-lookup"><span data-stu-id="ae59d-217">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="ae59d-218">Начало Microsoft Teams в веб-браузере с командой Teams, чтобы загрузить приложение из `https://localhost:3000/tab` .</span><span class="sxs-lookup"><span data-stu-id="ae59d-218">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application from `https://localhost:3000/tab`.</span></span> <span data-ttu-id="ae59d-219">Это URL-адрес, зарегистрированный в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="ae59d-219">This is the URL registered in the application manifest.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="ae59d-220">Научитесь искать и устранять распространенные проблемы при локальном запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="ae59d-220">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="ae59d-221">Чтобы запустить приложение в Teams, у вас должна быть учетная запись разработчика Teams, позволяющая устанавливать неопубликованные приложения.</span><span class="sxs-lookup"><span data-stu-id="ae59d-221">To successfully run your app in Teams, you must have a Teams account that allows app sideloading.</span></span> <span data-ttu-id="ae59d-222">Дополнительные сведения о создании учетной записи см. в разделе [Обязательные требования](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="ae59d-222">For more information on account opening, see [prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="ae59d-223">Узнайте, что происходит в ходе развертывания приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="ae59d-223">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="ae59d-224">До развертывания приложение работает локально:</span><span class="sxs-lookup"><span data-stu-id="ae59d-224">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="ae59d-225">Серверная часть работает с использованием **Azure Functions Core Tools**.</span><span class="sxs-lookup"><span data-stu-id="ae59d-225">The backend runs using **Azure Functions Core Tools**.</span></span>
1. <span data-ttu-id="ae59d-226">Конечная точка HTTP приложения, в которую Microsoft Teams загружает приложение, работает локально.</span><span class="sxs-lookup"><span data-stu-id="ae59d-226">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="ae59d-227">Развертывание включает в себя подготовка ресурсов по активной подписке Azure и развертывание или отправка кода backend и frontend для приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="ae59d-227">Deployment involves provisioning resources on an active Azure subscription and deploying or uploading the backend and frontend code for the application to Azure.</span></span>

1. <span data-ttu-id="ae59d-228">При настройке в приложении используется множество служб Azure, включая Службу приложений Azure и служба хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ae59d-228">The backend if configured uses a variety of Azure services, including Azure App Service and Azure Storage.</span></span>
1. <span data-ttu-id="ae59d-229">Клиентское приложение будет развернуто под учетной записью хранилища Azure, настроенной для статического размещения веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="ae59d-229">The frontend application will be deployed to an Azure Storage account configured for static web hosting.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="ae59d-230">См. также</span><span class="sxs-lookup"><span data-stu-id="ae59d-230">See also</span></span>

- [<span data-ttu-id="ae59d-231">Создание приложения Teams с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="ae59d-231">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="ae59d-232">[Создание приложения Teams в формате веб-части SharePoint](first-app-spfx.md) (Azure не требуется)</span><span class="sxs-lookup"><span data-stu-id="ae59d-232">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="ae59d-233">Создание бота беседы</span><span class="sxs-lookup"><span data-stu-id="ae59d-233">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="ae59d-234">Создание расширения для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="ae59d-234">Create a messaging extension</span></span>](first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="ae59d-235">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="ae59d-235">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae59d-236">Создание приложения Teams с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="ae59d-236">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
