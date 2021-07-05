---
title: 'Начало работы : создайте свое первое приложение Teams на основе React'
author: adrianhall
description: Вы сможете быстро разработать приложение Microsoft Teams, которое выводит строку "Hello, World!",  на базе набора средств Microsoft Teams и библиотеки React.
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: c257bcd805a6b7b38ab657cb31cad961df1c4704
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254323"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a><span data-ttu-id="85379-104">Создайте и запустите свое первое приложение Microsoft Teams, пользуясь библиотекой React</span><span class="sxs-lookup"><span data-stu-id="85379-104">Build and run your first Microsoft Teams app with React</span></span>

<span data-ttu-id="85379-105">В этом руководстве вы узнаете, как создать новое приложение Microsoft Teams в React, которое реализует простое личное приложение для получения информации из microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="85379-105">In this tutorial, you will learn how to create a new Microsoft Teams app in React that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="85379-106">Например, личное *приложение включает* набор вкладок для индивидуального использования.</span><span class="sxs-lookup"><span data-stu-id="85379-106">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="85379-107">Во время руководства вы узнаете о структуре приложения Teams, локальном запуске приложения и развертывании приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="85379-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="85379-108">Приложение, которое мы построим, выводит основные сведения о текущем пользователе.</span><span class="sxs-lookup"><span data-stu-id="85379-108">The app that is built displays basic user information for the current user.</span></span> <span data-ttu-id="85379-109">Когда разрешение будет предоставлено, приложение подключится к Microsoft Graph в качестве текущего пользователя, чтобы получить его полный профиль.</span><span class="sxs-lookup"><span data-stu-id="85379-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="85379-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="85379-110">Before you begin</span></span>

<span data-ttu-id="85379-111">Убедитесь, что среда разработки настроена путем установки необходимых условий.</span><span class="sxs-lookup"><span data-stu-id="85379-111">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="85379-112">Необходимые условия для установки</span><span class="sxs-lookup"><span data-stu-id="85379-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="85379-113">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="85379-113">Create your project</span></span>

<span data-ttu-id="85379-114">Используйте набор средств Teams для создания своего первого проекта.</span><span class="sxs-lookup"><span data-stu-id="85379-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="85379-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="85379-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="85379-116">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="85379-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="85379-117">Откройте Teams набор средств и выберите значок Teams на боковой панели:</span><span class="sxs-lookup"><span data-stu-id="85379-117">Open the Teams Toolkit and select the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. <span data-ttu-id="85379-119">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="85379-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. <span data-ttu-id="85379-121">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="85379-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания проекта":::

1. <span data-ttu-id="85379-123">В разделе **Выбор возможностей** укайм, что **вкладка** выбрана и выберите **ОК.**</span><span class="sxs-lookup"><span data-stu-id="85379-123">In the **Select capabilities** section, varify that **Tab** is selected and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. <span data-ttu-id="85379-125">В разделе **Тип размещения в Frontend** выберите **Azure.**</span><span class="sxs-lookup"><span data-stu-id="85379-125">In the **Frontend hosting type** section, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Снимок экрана: выбор размещения для нового приложения.":::

1. <span data-ttu-id="85379-127">В разделе **Облачные ресурсы** выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="85379-127">In the **Cloud resources** section, select **OK**.</span></span>  <span data-ttu-id="85379-128">В этом руководстве вам не понадобятся дополнительные облачные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="85379-128">We do not need additional cloud resources for this tutorial.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Снимок экрана: добавление облачных ресурсов в новое приложение.":::

1. <span data-ttu-id="85379-130">В разделе **Язык программирования** выберите **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="85379-130">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Снимок экрана: выбор языка.":::

1. <span data-ttu-id="85379-132">Выберите папку рабочей области.</span><span class="sxs-lookup"><span data-stu-id="85379-132">Select a workspace folder.</span></span> <span data-ttu-id="85379-133">Папка создается в папке рабочего пространства для созданного вами проекта.</span><span class="sxs-lookup"><span data-stu-id="85379-133">A folder is created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="85379-134">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="85379-134">Enter a suitable name for your app, like `helloworld`.</span></span> <span data-ttu-id="85379-135">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="85379-135">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="85379-136">Чтобы продолжить, нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="85379-136">Press **Enter** to continue.</span></span>

   <span data-ttu-id="85379-137">Приложение Teams создается в течение нескольких секунд.</span><span class="sxs-lookup"><span data-stu-id="85379-137">Your Teams app is created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="85379-138">Командная строка</span><span class="sxs-lookup"><span data-stu-id="85379-138">Command line</span></span>](#tab/cli)

<span data-ttu-id="85379-139">Используйте для создания первого проекта интерфейс командной строки `teamsfx`.</span><span class="sxs-lookup"><span data-stu-id="85379-139">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="85379-140">Начните с папки, в которой будет создана папка проекта.</span><span class="sxs-lookup"><span data-stu-id="85379-140">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="85379-141">Интерфейс командной строки выдаст несколько вопросов, ответы на которые используются для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="85379-141">The CLI walks through some questions to create the project.</span></span> <span data-ttu-id="85379-142">На каждом вопросе будет посвеяно, как ответить на него, например, использовать клавиши со стрелками для выбора варианта.</span><span class="sxs-lookup"><span data-stu-id="85379-142">Each question will tell you how to answer it, for example, use arrow keys to select an option.</span></span> <span data-ttu-id="85379-143">Ответив на вопрос, подтвердите свой выбор, нажав клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="85379-143">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="85379-144">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="85379-144">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="85379-145">Выберите возможность **Tab.**</span><span class="sxs-lookup"><span data-stu-id="85379-145">Select the **Tab** capability.</span></span>
1. <span data-ttu-id="85379-146">В качестве размещения на клиенте выберите **Azure**.</span><span class="sxs-lookup"><span data-stu-id="85379-146">Select **Azure** frontend hosting.</span></span> <span data-ttu-id="85379-147">Не добавляйте облачные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="85379-147">Do not select any cloud resources.</span></span>
1. <span data-ttu-id="85379-148">Выберите **JavaScript** в качестве языка программирования.</span><span class="sxs-lookup"><span data-stu-id="85379-148">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="85379-149">Нажмите клавишу **ВВОД**, чтобы выбрать папку рабочей области по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="85379-149">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="85379-150">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="85379-150">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="85379-151">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="85379-151">The name of the app must consist only of alphanumeric characters.</span></span>

   <span data-ttu-id="85379-152">После ответа на все вопросы создается проект.</span><span class="sxs-lookup"><span data-stu-id="85379-152">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="85379-153">Знакомство с исходным кодом</span><span class="sxs-lookup"><span data-stu-id="85379-153">Take a tour of the source code</span></span>

<span data-ttu-id="85379-154">Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="85379-154">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="85379-155">После настройки Teams набор средств проекта у вас есть компоненты для создания базового личного приложения для Teams.</span><span class="sxs-lookup"><span data-stu-id="85379-155">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="85379-156">Каталоги и файлы проекта отображаются в области проводника Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="85379-156">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="Снимок экрана: файлы проектов приложения для личного приложения в Visual Studio Code.":::

<span data-ttu-id="85379-158">Набор средств автоматически формирует шаблоны в каталоге проекта на основе возможностей, добавленных во время установки.</span><span class="sxs-lookup"><span data-stu-id="85379-158">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="85379-159">Набор средств Teams сохраняет свое состояние для вашего приложения в каталоге `.fx`.</span><span class="sxs-lookup"><span data-stu-id="85379-159">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="85379-160">Среди других элементов в этом каталоге находятся:</span><span class="sxs-lookup"><span data-stu-id="85379-160">Among other items in this directory:</span></span>

- <span data-ttu-id="85379-161">Значки приложений, хранимые как PNG-файлы в `color.png` и `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="85379-161">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="85379-162">Манифест приложения для публикации на портале разработчика для Teams, хранимый в `manifest.source.json`.</span><span class="sxs-lookup"><span data-stu-id="85379-162">The app manifest for publishing to the Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="85379-163">Параметры, выбранные при создании проекта, хранятся в `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="85379-163">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="85379-164">Так как вы выбрали вкладку во время настройки, набор средств Teams создает шаблоны всего необходимого кода для программирования базовой вкладки в каталоге `tabs`.</span><span class="sxs-lookup"><span data-stu-id="85379-164">Since you selected the tab capability during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab in the `tabs` directory.</span></span> <span data-ttu-id="85379-165">В этом каталоге есть несколько важных файлов:</span><span class="sxs-lookup"><span data-stu-id="85379-165">Within this directory there are several important files:</span></span>

- <span data-ttu-id="85379-166">`tabs/src/index.jsx` — точка входа приложения на клиентской стороне, где проводится отрисовка основного компонента `App` с помощью `ReactDOM.render()`.</span><span class="sxs-lookup"><span data-stu-id="85379-166">`tabs/src/index.jsx` is the front-end app's entry point, where the main `App` component is rendered with `ReactDOM.render()`.</span></span>
- <span data-ttu-id="85379-167">`tabs/src/components/App.jsx` несет ответственность за маршрутизацию URL-адресов в приложении.</span><span class="sxs-lookup"><span data-stu-id="85379-167">`tabs/src/components/App.jsx` handles URL routing in your app.</span></span> <span data-ttu-id="85379-168">Он вызывает [SDK JavaScript для Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md), чтобы реализовать обмен сообщениями между вашим приложением и Teams.</span><span class="sxs-lookup"><span data-stu-id="85379-168">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>
- <span data-ttu-id="85379-169">`tabs/src/components/Tab.jsx` содержит код для реализации пользовательского интерфейса вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="85379-169">`tabs/src/components/Tab.jsx` contains the code to implement the UI of your app.</span></span>
- <span data-ttu-id="85379-170">`tabs/src/components/TabConfig.jsx` содержит код для реализации пользовательского интерфейса настройки вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="85379-170">`tabs/src/components/TabConfig.jsx` contains the code to implement the UI that configures your app.</span></span>

<span data-ttu-id="85379-171">Среде выполнения Teams требуется несколько вкладок, в том числе для уведомления о конфиденциальности, для условий использования и для настроек.</span><span class="sxs-lookup"><span data-stu-id="85379-171">Several tabs are required by the Teams runtime, including the privacy notice, terms of use, and configuration tabs.</span></span>  <span data-ttu-id="85379-172">Код уведомления о конфиденциальности и условия использования находятся в том же каталоге.</span><span class="sxs-lookup"><span data-stu-id="85379-172">The code for the privacy notice and terms of use are located in the same directory.</span></span>

<span data-ttu-id="85379-173">При добавлении функций облака в проект добавляются дополнительные каталоги.</span><span class="sxs-lookup"><span data-stu-id="85379-173">When you add cloud functionality, additional directories are added to the project.</span></span>  <span data-ttu-id="85379-174">В первую очередь, каталог `api` содержит код для всех разработанных вами функций Azure.</span><span class="sxs-lookup"><span data-stu-id="85379-174">Most notably, the `api` directory holds the code to any Azure Functions you write.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="85379-175">Запустите приложение локально</span><span class="sxs-lookup"><span data-stu-id="85379-175">Run your app locally</span></span>

<span data-ttu-id="85379-176">Набор средств Teams позволяет запускать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="85379-176">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="85379-177">Нужно выполнить несколько действий для обеспечения правильной инфраструктуры. Teams ожидает, что:</span><span class="sxs-lookup"><span data-stu-id="85379-177">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="85379-178">Приложение зарегистрировано в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="85379-178">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="85379-179">Оно имеет разрешения, связанные с расположением, из которого загружается, и с любыми ресурсами серверной сторонй, которые использует.</span><span class="sxs-lookup"><span data-stu-id="85379-179">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="85379-180">Веб-API позволяет выполнять задачи проверки подлинности, действуя в качестве прокси-сервера между приложением и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="85379-180">A web API is hosted to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  <span data-ttu-id="85379-181">Этим занимается набор инструментов Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="85379-181">This is run by Azure Functions Core Tools.</span></span>  <span data-ttu-id="85379-182">Доступ к нему можно получить по URL `https://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="85379-182">It can be accessed at the URL `https://localhost:5000`.</span></span>
- <span data-ttu-id="85379-183">Ресурсы HTML, CSS и JavaScript, которые составляют клиентскую часть приложения, размещены в локальной службе.</span><span class="sxs-lookup"><span data-stu-id="85379-183">The HTML, CSS, and JavaScript resources that make up the front end of the app are hosted on a local service.</span></span> <span data-ttu-id="85379-184">Доступ к ней можно получить по URL `https://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="85379-184">It can be accessed at `https://localhost:3000`.</span></span>
- <span data-ttu-id="85379-185">Манифест приложения создается и существует на портале разработчика для Teams.</span><span class="sxs-lookup"><span data-stu-id="85379-185">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="85379-186">Teams использует манифест приложения, чтобы сообщить подключенным клиентам, откуда загружать приложение.</span><span class="sxs-lookup"><span data-stu-id="85379-186">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="85379-187">После этого приложение может быть загружено в клиенте Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="85379-187">After this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="85379-188">Мы используем веб-клиент Teams, чтобы иметь возможность видеть код HTML, CSS и JavaScript в стандартной среде веб-разработки.</span><span class="sxs-lookup"><span data-stu-id="85379-188">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="85379-189">Создайте и запустите приложение локально в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="85379-189">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="85379-190">Чтобы создать и запустить приложение локально, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="85379-190">To build and run your app locally:</span></span>

1. <span data-ttu-id="85379-191">В Visual Studio Code нажмите клавишу **F5**, чтобы запустить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="85379-191">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="85379-192">При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.</span><span class="sxs-lookup"><span data-stu-id="85379-192">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="85379-193">По завершении сборки автоматически откроется окно браузера.</span><span class="sxs-lookup"><span data-stu-id="85379-193">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="85379-194">Для завершения может потребоваться от 3 до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="85379-194">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="85379-195">В набор средств необходимо установить локальный сертификат.</span><span class="sxs-lookup"><span data-stu-id="85379-195">The Toolkit prompts you to install a local certificate if required.</span></span> <span data-ttu-id="85379-196">Этот сертификат позволяет Teams загружать приложение из `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="85379-196">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="85379-197">Выберите "Да", когда появится следующее диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="85379-197">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. <span data-ttu-id="85379-199">Веб-браузер начинает запускать приложение.</span><span class="sxs-lookup"><span data-stu-id="85379-199">Your web browser starts to run the app.</span></span> <span data-ttu-id="85379-200">Если вам будет предложено открыть Teams рабочий стол, выберите **Отмена,** чтобы оставаться в браузере.</span><span class="sxs-lookup"><span data-stu-id="85379-200">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="85379-201">Вам также может быть предложено перейти на рабочий Teams в другое время; выберите Teams веб-приложение, когда это произойдет.</span><span class="sxs-lookup"><span data-stu-id="85379-201">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Снимок экрана: выбор веб-версии Teams при запуске":::

1. <span data-ttu-id="85379-203">Во входе в учетную запись M365 при запросе.</span><span class="sxs-lookup"><span data-stu-id="85379-203">Sign in with your M365 account when prompted.</span></span>
1. <span data-ttu-id="85379-204">При появлении запроса на установку приложения в Teams нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="85379-204">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="85379-205">Теперь ваше приложение отображается:</span><span class="sxs-lookup"><span data-stu-id="85379-205">Your app is now displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="Снимок экрана: готовое приложение":::

<span data-ttu-id="85379-207">Вы можете делать обычные действия отладки, как если бы это было любое другое веб-приложение, например настройка точек остановок.</span><span class="sxs-lookup"><span data-stu-id="85379-207">You can do normal debugging activities as if this were any other web application, such as setting breakpoints.</span></span> <span data-ttu-id="85379-208">Приложение поддерживает горячую перезагрузку.</span><span class="sxs-lookup"><span data-stu-id="85379-208">The app supports hot reloading.</span></span> <span data-ttu-id="85379-209">Если вы измените какой-либо файл в составе проекта, страница будет перезагружена.</span><span class="sxs-lookup"><span data-stu-id="85379-209">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="85379-210">Узнайте, что происходит при локальном запуске приложения в отладчике.</span><span class="sxs-lookup"><span data-stu-id="85379-210">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="85379-211">При нажатии **клавиши F5** Teams набор средств:</span><span class="sxs-lookup"><span data-stu-id="85379-211">When you press the **F5** key, the Teams Toolkit:</span></span>

* <span data-ttu-id="85379-212">Регистрирует приложение с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="85379-212">Registers your application with Azure Active Directory.</span></span>
* <span data-ttu-id="85379-213">*Sideloads* your app in Teams.</span><span class="sxs-lookup"><span data-stu-id="85379-213">*Sideloads* your app in Teams.</span></span>
* <span data-ttu-id="85379-214">Запускает локализованную работу backend приложения с помощью основных средств [Azure Function.](/azure/azure-functions/functions-run-local?#start)</span><span class="sxs-lookup"><span data-stu-id="85379-214">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
* <span data-ttu-id="85379-215">Запускает локальное локальное хостинг приложения.</span><span class="sxs-lookup"><span data-stu-id="85379-215">Starts your application front-end hosted locally.</span></span>
* <span data-ttu-id="85379-216">Начинается Microsoft Teams в веб-браузере с командой Teams, чтобы загрузить приложение из `https://localhost:3000/tab` .</span><span class="sxs-lookup"><span data-stu-id="85379-216">Starts Microsoft Teams in a web browser with a command to instruct Teams to side load the application from `https://localhost:3000/tab`.</span></span> <span data-ttu-id="85379-217">Это URL-адрес, зарегистрированный в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="85379-217">This is the URL registered in the application manifest.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="85379-218">Научитесь искать и устранять распространенные проблемы при локальном запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="85379-218">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="85379-219">Чтобы запустить приложение в Teams, у вас должна быть учетная запись разработчика Teams, позволяющая устанавливать неопубликованные приложения.</span><span class="sxs-lookup"><span data-stu-id="85379-219">To successfully run your app in Teams, you must have a Teams account that allows app sideloading.</span></span> <span data-ttu-id="85379-220">Дополнительные сведения о создании учетной записи см. в разделе [Обязательные требования](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="85379-220">For more information on account opening, see [prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="85379-221">Узнайте, что происходит в ходе развертывания приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="85379-221">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="85379-222">До развертывания приложение работает локально:</span><span class="sxs-lookup"><span data-stu-id="85379-222">Before deployment, the application has been running locally:</span></span>

* <span data-ttu-id="85379-223">Серверная часть работает с использованием **Azure Functions Core Tools**.</span><span class="sxs-lookup"><span data-stu-id="85379-223">The backend runs using **Azure Functions Core Tools**.</span></span>
* <span data-ttu-id="85379-224">Конечная точка HTTP приложения, в которую Microsoft Teams загружает приложение, работает локально.</span><span class="sxs-lookup"><span data-stu-id="85379-224">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="85379-225">Развертывание включает в себя подготовка ресурсов по активной подписке Azure и развертывание или отправка кода backend и frontend для приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="85379-225">Deployment involves provisioning resources on an active Azure subscription and deploying or uploading the backend and frontend code for the application to Azure.</span></span>

* <span data-ttu-id="85379-226">При настройке в приложении используется множество служб Azure, включая Службу приложений Azure и служба хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="85379-226">The backend if configured uses a variety of Azure services, including Azure App Service and Azure Storage.</span></span>
* <span data-ttu-id="85379-227">Клиентское приложение будет развернуто под учетной записью хранилища Azure, настроенной для статического размещения веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="85379-227">The frontend application will be deployed to an Azure Storage account configured for static web hosting.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="85379-228">См. также</span><span class="sxs-lookup"><span data-stu-id="85379-228">See also</span></span>

* [<span data-ttu-id="85379-229">Обзор учебников</span><span class="sxs-lookup"><span data-stu-id="85379-229">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="85379-230">Создание бота беседы</span><span class="sxs-lookup"><span data-stu-id="85379-230">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="85379-231">Создание расширения для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="85379-231">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="85379-232">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="85379-232">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
