---
title: Начало работы — создание первого расширения для сообщений
author: adrianhall
description: Создайте расширение для сообщений для Microsoft Teams с помощью набора средств Teams.
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: 3566bc55c9995a8407b1344fbdb7d1548e210046
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254290"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="f1125-103">Создание и запуск первого расширения для сообщений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f1125-103">Build and run your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="f1125-104">В этом руководстве вы узнаете, как создать команду поиска для поиска внешних данных и вставить результаты в сообщение. </span><span class="sxs-lookup"><span data-stu-id="f1125-104">In this tutorial, you will learn how to create a *search command* to search for external data and insert the results into a message.</span></span> 

<span data-ttu-id="f1125-105">Существует два типа **расширений для сообщений** Teams.</span><span class="sxs-lookup"><span data-stu-id="f1125-105">There are two types of Teams **messaging extensions**:</span></span>

- <span data-ttu-id="f1125-106">[Команды поиска](../messaging-extensions/how-to/search-commands/define-search-command.md) позволяют выполнять поиск во внешних системах и вставлять результаты поиска в сообщение в виде карточки.</span><span class="sxs-lookup"><span data-stu-id="f1125-106">[Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) allow you to search external systems and insert the results of that search into a message in the form of a card.</span></span>
- <span data-ttu-id="f1125-107">[Команды действий](../messaging-extensions/how-to/action-commands/define-action-command.md) позволяют предоставлять пользователям модальное всплывающее окно для сбора или отображения информации, а затем обрабатывать их действия и отправлять информацию обратно в Teams.</span><span class="sxs-lookup"><span data-stu-id="f1125-107">[Action commands](../messaging-extensions/how-to/action-commands/define-action-command.md) allow you present your users with a modal popup to collect or display information, then process their interaction and send information back to Teams.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f1125-108">Подготовка</span><span class="sxs-lookup"><span data-stu-id="f1125-108">Before you begin</span></span>

<span data-ttu-id="f1125-109">Убедитесь, что среда разработки настроена путем установки необходимых условий.</span><span class="sxs-lookup"><span data-stu-id="f1125-109">Make sure your development environment is set up by installing the Prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1125-110">Установка необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="f1125-110">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="f1125-111">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="f1125-111">Create your project</span></span>

<span data-ttu-id="f1125-112">Используйте набор средств Teams для создания своего первого проекта.</span><span class="sxs-lookup"><span data-stu-id="f1125-112">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="f1125-113">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f1125-113">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="f1125-114">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f1125-114">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="f1125-115">Выберите значок Teams на боковой панели, чтобы открыть Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="f1125-115">Select the Teams icon in the sidebar to open the Teams Toolkit.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. <span data-ttu-id="f1125-117">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="f1125-117">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. <span data-ttu-id="f1125-119">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="f1125-119">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания проекта":::

1. <span data-ttu-id="f1125-121">В разделе **Выбор возможностей выберите** расширение **сообщений,** разблокировать **вкладку и** выбрать **ОК.**</span><span class="sxs-lookup"><span data-stu-id="f1125-121">In the **Select capabilities** section, select **Message Extension**, deselect **Tab** and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. <span data-ttu-id="f1125-123">В разделе **Регистрация ботов** выберите **Создать новую регистрацию бота.**</span><span class="sxs-lookup"><span data-stu-id="f1125-123">In the **Bot registration** section, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Выбор создания новой регистрации бота":::

   > [!NOTE]
   > <span data-ttu-id="f1125-125">Расширения для сообщений используют боты для диалога между пользователем и кодом.</span><span class="sxs-lookup"><span data-stu-id="f1125-125">Messaging extensions rely on bots to provide a dialog between the user and your code.</span></span>

1. <span data-ttu-id="f1125-126">В разделе **Язык программирования** выберите **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="f1125-126">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Снимок экрана: выбор языка.":::

1. <span data-ttu-id="f1125-128">Выберите папку рабочей области.</span><span class="sxs-lookup"><span data-stu-id="f1125-128">Select a workspace folder.</span></span>  <span data-ttu-id="f1125-129">В папке рабочей области будет создана папка для создаваемого проекта.</span><span class="sxs-lookup"><span data-stu-id="f1125-129">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="f1125-130">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="f1125-130">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="f1125-131">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="f1125-131">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="f1125-132">Чтобы продолжить, нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="f1125-132">Press **Enter** to continue.</span></span>

   <span data-ttu-id="f1125-133">Создание приложения Teams займет несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="f1125-133">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="f1125-134">Командная строка</span><span class="sxs-lookup"><span data-stu-id="f1125-134">Command line</span></span>](#tab/cli)

<span data-ttu-id="f1125-135">Используйте для создания первого проекта интерфейс командной строки `teamsfx`.</span><span class="sxs-lookup"><span data-stu-id="f1125-135">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="f1125-136">Начните с папки, в которой будет создана папка проекта.</span><span class="sxs-lookup"><span data-stu-id="f1125-136">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="f1125-137">Интерфейс командной строки выдаст несколько вопросов, ответы на которые используются для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="f1125-137">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="f1125-138">Каждый вопрос сопровождается подсказкой о том, как на него отвечать (например, использовать клавиши со стрелками для выбора варианта).</span><span class="sxs-lookup"><span data-stu-id="f1125-138">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="f1125-139">Ответив на вопрос, подтвердите свой выбор, нажав клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="f1125-139">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="f1125-140">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="f1125-140">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="f1125-141">Выберите **вкладку Расширение сообщений** **и** выселку.</span><span class="sxs-lookup"><span data-stu-id="f1125-141">Select the **Message Extension** and deselect **Tab**.</span></span>
1. <span data-ttu-id="f1125-142">Выберите **Создать новую регистрацию бота**.</span><span class="sxs-lookup"><span data-stu-id="f1125-142">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="f1125-143">Выберите **JavaScript** в качестве языка.</span><span class="sxs-lookup"><span data-stu-id="f1125-143">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="f1125-144">Нажмите клавишу **ВВОД**, чтобы выбрать папку рабочей области по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f1125-144">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="f1125-145">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="f1125-145">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="f1125-146">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="f1125-146">The name of the app must consist only of alphanumeric characters.</span></span>

   <span data-ttu-id="f1125-147">После ответа на все вопросы создается проект.</span><span class="sxs-lookup"><span data-stu-id="f1125-147">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="f1125-148">Знакомство с исходным кодом</span><span class="sxs-lookup"><span data-stu-id="f1125-148">Take a tour of the source code</span></span>

<span data-ttu-id="f1125-149">Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="f1125-149">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="f1125-150">Расширение для сообщений использует [Bot Framework](https://docs.botframework.com), чтобы дать пользователю возможность взаимодействовать со службой посредством общения.</span><span class="sxs-lookup"><span data-stu-id="f1125-150">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="f1125-151">После генерации кода проект будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f1125-151">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="Макет файла проекта бота.":::

<span data-ttu-id="f1125-153">Код бота хранится в каталоге `bot`.</span><span class="sxs-lookup"><span data-stu-id="f1125-153">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="f1125-154">`bot/messageExtensionBot.js` — это главная точка входа для расширения для сообщений.</span><span class="sxs-lookup"><span data-stu-id="f1125-154">The `bot/messageExtensionBot.js` is the main entry point for the messaging extension.</span></span>

> [!Tip]
> <span data-ttu-id="f1125-155">Перед интеграцией своего первого бота в Teams ознакомьтесь с ботами за пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="f1125-155">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="f1125-156">Дополнительные сведения о ботах см. в руководстве [Служба Azure Bot](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f1125-156">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="f1125-157">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1125-157">Run your app locally</span></span>

<span data-ttu-id="f1125-158">Набор средств Teams позволяет размещать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="f1125-158">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="f1125-159">Для этого:</span><span class="sxs-lookup"><span data-stu-id="f1125-159">To do this:</span></span>

- <span data-ttu-id="f1125-160">Приложение Azure Active Directory регистрируется в клиенте M365.</span><span class="sxs-lookup"><span data-stu-id="f1125-160">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="f1125-161">Манифест приложения отправляется на портал разработчика для Teams.</span><span class="sxs-lookup"><span data-stu-id="f1125-161">An app manifest is submitted to the Developer Portal for Teams.</span></span>
- <span data-ttu-id="f1125-162">API запускается локально с помощью Azure Functions Core Tools для поддержки приложения.</span><span class="sxs-lookup"><span data-stu-id="f1125-162">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="f1125-163">[ngrok](https://ngrok.io) устанавливается и используется для обеспечения туннеля между Teams и расширением для сообщений.</span><span class="sxs-lookup"><span data-stu-id="f1125-163">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your messaging extension.</span></span>

<span data-ttu-id="f1125-164">Чтобы создать и запустить приложение локально, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f1125-164">To build and run your app locally:</span></span>

1. <span data-ttu-id="f1125-165">С Visual Studio Code нажмите **клавишу F5,** чтобы запустить приложение в режиме отлаживания.</span><span class="sxs-lookup"><span data-stu-id="f1125-165">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>

   > <span data-ttu-id="f1125-166">При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.</span><span class="sxs-lookup"><span data-stu-id="f1125-166">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="f1125-167">По завершении сборки автоматически откроется окно браузера.</span><span class="sxs-lookup"><span data-stu-id="f1125-167">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="f1125-168">Для завершения может потребоваться от 3 до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="f1125-168">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="f1125-169">В браузере будет выполнена загрузка Teams, и вам будет предложено войти.</span><span class="sxs-lookup"><span data-stu-id="f1125-169">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="f1125-170">При появлении запроса на открытие Microsoft Teams выберите "Отменить", чтобы остаться в браузере.</span><span class="sxs-lookup"><span data-stu-id="f1125-170">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="f1125-171">Войдите с помощью своей учетной записи M365.</span><span class="sxs-lookup"><span data-stu-id="f1125-171">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="f1125-172">Выберите **Добавить,** чтобы добавить приложение в свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="f1125-172">Select **Add** to add the app to your account.</span></span>

   <span data-ttu-id="f1125-173">После загрузки приложения вы будете доставлены непосредственно в диалоговое окно поиска:</span><span class="sxs-lookup"><span data-stu-id="f1125-173">After the app is loaded, you will be taken directly to a search dialog:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="Принцип работы расширения для сообщений на основе поиска":::

   <span data-ttu-id="f1125-175">Введите текст в поле поиска и выберите один из вариантов.</span><span class="sxs-lookup"><span data-stu-id="f1125-175">Type some text in the search box, then select one of the options.</span></span>  <span data-ttu-id="f1125-176">В поле ввода будет добавлена адаптивная карточка.</span><span class="sxs-lookup"><span data-stu-id="f1125-176">An adaptive card will be added to your input box.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="f1125-177">Узнайте, что происходит при локальном запуске приложения в отладчике.</span><span class="sxs-lookup"><span data-stu-id="f1125-177">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="f1125-178">При нажатии **клавиши F5** Teams набор средств:</span><span class="sxs-lookup"><span data-stu-id="f1125-178">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="f1125-179">Регистрирует приложение с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1125-179">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="f1125-180">Регистрирует приложение для "боковой загрузки" в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f1125-180">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="f1125-181">Запускает локализованную работу backend приложения с помощью основных средств [Azure Function.](/azure/azure-functions/functions-run-local?#start)</span><span class="sxs-lookup"><span data-stu-id="f1125-181">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="f1125-182">Запускает туннель ngrok, чтобы Teams взаимодействовать с приложением.</span><span class="sxs-lookup"><span data-stu-id="f1125-182">Starts an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="f1125-183">Начинается Microsoft Teams с командой Teams для загрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="f1125-183">Starts Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="f1125-184">Узнайте, как устранить распространенные проблемы при локальном запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="f1125-184">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="f1125-185">Чтобы запустить приложение в Teams, у вас должна быть учетная запись разработчика Microsoft 365, позволяющая устанавливать неопубликованные приложения.</span><span class="sxs-lookup"><span data-stu-id="f1125-185">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="f1125-186">Дополнительные сведения о создании учетной записи см. в разделе [Необходимые компоненты](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="f1125-186">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="f1125-187">Перед установкой неопубликованного приложения проверьте наличие проблем с помощью [средства проверки приложений](https://dev.teams.microsoft.com/appvalidation.html), которое входит в набор средств.</span><span class="sxs-lookup"><span data-stu-id="f1125-187">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="f1125-188">Исправьте ошибки, чтобы успешно установить неопубликованное приложение.</span><span class="sxs-lookup"><span data-stu-id="f1125-188">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="f1125-189">Узнайте, что происходит после развертывания приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="f1125-189">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="f1125-190">До развертывания приложение работает локально:</span><span class="sxs-lookup"><span data-stu-id="f1125-190">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="f1125-191">Серверная часть работает с использованием _Azure Functions Core Tools_.</span><span class="sxs-lookup"><span data-stu-id="f1125-191">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="f1125-192">Конечная точка HTTP приложения, в которую Microsoft Teams загружает приложение, работает локально.</span><span class="sxs-lookup"><span data-stu-id="f1125-192">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="f1125-193">Развертывание включает подготовку ресурсов для активной подписки Azure и развертывание (загрузку) внутреннего и внешнего кода приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="f1125-193">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="f1125-194">Серверная часть использует различные службы Azure, включая службу приложений Azure и службу Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="f1125-194">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="add-a-configuration-page-to-your-messaging-extension"></a><span data-ttu-id="f1125-195">Добавление страницы конфигурации в расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="f1125-195">Add a configuration page to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="code-sample"></a><span data-ttu-id="f1125-196">Пример кода</span><span class="sxs-lookup"><span data-stu-id="f1125-196">Code sample</span></span>

<span data-ttu-id="f1125-197">В Teams в примере проектов по GitHub показано, как создавать расширения обмена сообщениями, включающие страницу конфигурации и проверку подлинности службы [ботов.](https://github.com/microsoft/BotBuilder-Samples#teams-samples)</span><span class="sxs-lookup"><span data-stu-id="f1125-197">The Teams Search Auth Config for sample projects on GitHub, demonstrate how to create messaging extensions that include a configuration page and [Bot Service authentication](https://github.com/microsoft/BotBuilder-Samples#teams-samples).</span></span> <span data-ttu-id="f1125-198">В примерах также показано, как создавать расширения сообщений, которые принимают запросы на поиск и возвращают результаты после того, как пользователь вписался.</span><span class="sxs-lookup"><span data-stu-id="f1125-198">The samples also demonstrate how to create message extensions that accept search requests and return the results after the user has signed in.</span></span>

| <span data-ttu-id="f1125-199">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="f1125-199">**Sample name**</span></span> | <span data-ttu-id="f1125-200">**Описание**</span><span class="sxs-lookup"><span data-stu-id="f1125-200">**Description**</span></span> | <span data-ttu-id="f1125-201">**.NET**</span><span class="sxs-lookup"><span data-stu-id="f1125-201">**.NET**</span></span> | <span data-ttu-id="f1125-202">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="f1125-202">**Node.js**</span></span> | <span data-ttu-id="f1125-203">**Python**</span><span class="sxs-lookup"><span data-stu-id="f1125-203">**Python**</span></span> |
|-----------------|-----------------|-------------|--------------|--------|
| <span data-ttu-id="f1125-204">Строитель ботов</span><span class="sxs-lookup"><span data-stu-id="f1125-204">Bot builder</span></span> | <span data-ttu-id="f1125-205">Создание расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="f1125-205">To create messaging extensions.</span></span> | [<span data-ttu-id="f1125-206">View</span><span class="sxs-lookup"><span data-stu-id="f1125-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="f1125-207">View</span><span class="sxs-lookup"><span data-stu-id="f1125-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="f1125-208">View</span><span class="sxs-lookup"><span data-stu-id="f1125-208">View</span></span>]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a><span data-ttu-id="f1125-209">Дополнительный пример кода</span><span class="sxs-lookup"><span data-stu-id="f1125-209">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1125-210">Просмотр дополнительных примеров bot Framework в GitHub</span><span class="sxs-lookup"><span data-stu-id="f1125-210">View more Bot Framework Samples on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="see-also"></a><span data-ttu-id="f1125-211">См. также</span><span class="sxs-lookup"><span data-stu-id="f1125-211">See also</span></span>

* [<span data-ttu-id="f1125-212">Обзор учебников</span><span class="sxs-lookup"><span data-stu-id="f1125-212">Tutorials Overview</span></span>](code-samples.md) 
* [<span data-ttu-id="f1125-213">Создание приложения с React</span><span class="sxs-lookup"><span data-stu-id="f1125-213">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="f1125-214">Создание приложения с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="f1125-214">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="f1125-215">Создание приложения с SPFx</span><span class="sxs-lookup"><span data-stu-id="f1125-215">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="f1125-216">Создание приложения с помощью C# или .NET</span><span class="sxs-lookup"><span data-stu-id="f1125-216">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="f1125-217">Создайте приложение с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="f1125-217">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="f1125-218">Создание приложения с помощью генератора Yeoman</span><span class="sxs-lookup"><span data-stu-id="f1125-218">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="f1125-219">Создание бота беседы</span><span class="sxs-lookup"><span data-stu-id="f1125-219">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="f1125-220">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="f1125-220">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)