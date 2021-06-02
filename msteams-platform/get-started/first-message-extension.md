---
title: Начало работы — создание первого расширения для сообщений
author: adrianhall
description: Создайте расширение для сообщений для Microsoft Teams с помощью набора средств Teams.
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: eaecb045993f8dfd21f4c2c4359a4a3388d659e6
ms.sourcegitcommit: e50cdeb6b7f481e12911b2bb74a8da22af0bffac
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/01/2021
ms.locfileid: "52710650"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="5e60b-103">Создание и запуск первого расширения для сообщений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5e60b-103">Build and run your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="5e60b-104">Существует два типа **расширений для сообщений** Teams.</span><span class="sxs-lookup"><span data-stu-id="5e60b-104">There are two types of Teams **messaging extensions**:</span></span>

- <span data-ttu-id="5e60b-105">[Команды поиска](../messaging-extensions/how-to/search-commands/define-search-command.md) позволяют выполнять поиск во внешних системах и вставлять результаты поиска в сообщение в виде карточки.</span><span class="sxs-lookup"><span data-stu-id="5e60b-105">[Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) allow you to search external systems and insert the results of that search into a message in the form of a card.</span></span>
- <span data-ttu-id="5e60b-106">[Команды действий](../messaging-extensions/how-to/action-commands/define-action-command.md) позволяют предоставлять пользователям модальное всплывающее окно для сбора или отображения информации, а затем обрабатывать их действия и отправлять информацию обратно в Teams.</span><span class="sxs-lookup"><span data-stu-id="5e60b-106">[Action commands](../messaging-extensions/how-to/action-commands/define-action-command.md) allow you present your users with a modal popup to collect or display information, then process their interaction and send information back to Teams.</span></span>

<span data-ttu-id="5e60b-107">С помощью этого руководства вы создадите *команду поиска* для поиска внешних данных и вставки результатов в сообщение.</span><span class="sxs-lookup"><span data-stu-id="5e60b-107">In this tutorial, you will create a *search command* to search for external data and insert the results into a message.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="5e60b-108">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="5e60b-108">Before you begin</span></span>

<span data-ttu-id="5e60b-109">Настройте среду разработки, установив [необходимые компоненты](prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="5e60b-109">Make sure your development environment is set up by installing the [Prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e60b-110">Установка необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="5e60b-110">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="5e60b-111">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="5e60b-111">Create your project</span></span>

<span data-ttu-id="5e60b-112">Используйте набор средств Teams для создания своего первого проекта.</span><span class="sxs-lookup"><span data-stu-id="5e60b-112">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="5e60b-113">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5e60b-113">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="5e60b-114">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="5e60b-114">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="5e60b-115">Откройте набор средств Teams, щелкнув значок Teams на боковой панели.</span><span class="sxs-lookup"><span data-stu-id="5e60b-115">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. <span data-ttu-id="5e60b-117">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="5e60b-117">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. <span data-ttu-id="5e60b-119">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="5e60b-119">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания проекта":::

1. <span data-ttu-id="5e60b-121">На этапе **Выбор возможностей** выберите **Расширение для сообщений** и снимите флажок **Вкладка**.  Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5e60b-121">On the **Select capabilities** step, select **Message Extension** and deselect **Tab**.  Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. <span data-ttu-id="5e60b-123">На этапе **Регистрация бота** выберите **Создать новую регистрацию бота**.</span><span class="sxs-lookup"><span data-stu-id="5e60b-123">On the **Bot registration** step, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Выбор создания новой регистрации бота":::

   > [!NOTE]
   > <span data-ttu-id="5e60b-125">Расширения для сообщений используют боты для диалога между пользователем и кодом.</span><span class="sxs-lookup"><span data-stu-id="5e60b-125">Messaging extensions rely on bots to provide a dialog between the user and your code.</span></span>

1. <span data-ttu-id="5e60b-126">На этапе **Язык** выберите **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="5e60b-126">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Снимок экрана: выбор языка.":::

1. <span data-ttu-id="5e60b-128">Выберите папку рабочей области.</span><span class="sxs-lookup"><span data-stu-id="5e60b-128">Select a workspace folder.</span></span>  <span data-ttu-id="5e60b-129">В папке рабочей области будет создана папка для создаваемого проекта.</span><span class="sxs-lookup"><span data-stu-id="5e60b-129">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="5e60b-130">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="5e60b-130">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="5e60b-131">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="5e60b-131">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="5e60b-132">Чтобы продолжить, нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="5e60b-132">Press **Enter** to continue.</span></span>

<span data-ttu-id="5e60b-133">Создание приложения Teams займет несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="5e60b-133">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="5e60b-134">Командная строка</span><span class="sxs-lookup"><span data-stu-id="5e60b-134">Command line</span></span>](#tab/cli)

<span data-ttu-id="5e60b-135">Используйте для создания первого проекта интерфейс командной строки `teamsfx`.</span><span class="sxs-lookup"><span data-stu-id="5e60b-135">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="5e60b-136">Начните с папки, в которой будет создана папка проекта.</span><span class="sxs-lookup"><span data-stu-id="5e60b-136">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="5e60b-137">Интерфейс командной строки выдаст несколько вопросов, ответы на которые используются для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="5e60b-137">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="5e60b-138">Каждый вопрос сопровождается подсказкой о том, как на него отвечать (например, использовать клавиши со стрелками для выбора варианта).</span><span class="sxs-lookup"><span data-stu-id="5e60b-138">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="5e60b-139">Ответив на вопрос, подтвердите свой выбор, нажав клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="5e60b-139">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="5e60b-140">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="5e60b-140">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="5e60b-141">Выберите возможность **Расширение для сообщений** и снимите флажок рядом с возможностью **Вкладка**.</span><span class="sxs-lookup"><span data-stu-id="5e60b-141">Select the **Message Extension** capability and deselect the **Tab** capability.</span></span>
1. <span data-ttu-id="5e60b-142">Выберите **Создать новую регистрацию бота**.</span><span class="sxs-lookup"><span data-stu-id="5e60b-142">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="5e60b-143">Выберите **JavaScript** в качестве языка.</span><span class="sxs-lookup"><span data-stu-id="5e60b-143">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="5e60b-144">Нажмите клавишу **ВВОД**, чтобы выбрать папку рабочей области по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5e60b-144">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="5e60b-145">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="5e60b-145">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="5e60b-146">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="5e60b-146">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="5e60b-147">После того, как вы ответите на все вопросы, будет создан проект.</span><span class="sxs-lookup"><span data-stu-id="5e60b-147">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="5e60b-148">Знакомство с исходным кодом</span><span class="sxs-lookup"><span data-stu-id="5e60b-148">Take a tour of the source code</span></span>

<span data-ttu-id="5e60b-149">Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="5e60b-149">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="5e60b-150">Расширение для сообщений использует [Bot Framework](https://docs.botframework.com), чтобы дать пользователю возможность взаимодействовать со службой посредством общения.</span><span class="sxs-lookup"><span data-stu-id="5e60b-150">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="5e60b-151">После генерации кода проект будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5e60b-151">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="Макет файла проекта бота.":::

<span data-ttu-id="5e60b-153">Код бота хранится в каталоге `bot`.</span><span class="sxs-lookup"><span data-stu-id="5e60b-153">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="5e60b-154">`bots/messageExtensionBot.js` — это главная точка входа для расширения для сообщений.</span><span class="sxs-lookup"><span data-stu-id="5e60b-154">The `bots/messageExtensionBot.js` is the main entry point for the messaging extension.</span></span>

> [!Tip]
> <span data-ttu-id="5e60b-155">Перед интеграцией своего первого бота в Teams ознакомьтесь с ботами за пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="5e60b-155">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="5e60b-156">Дополнительные сведения о ботах см. в руководстве [Служба Azure Bot](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="5e60b-156">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="5e60b-157">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="5e60b-157">Run your app locally</span></span>

<span data-ttu-id="5e60b-158">Набор средств Teams позволяет размещать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="5e60b-158">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="5e60b-159">Для этого:</span><span class="sxs-lookup"><span data-stu-id="5e60b-159">To do this:</span></span>

- <span data-ttu-id="5e60b-160">Приложение Azure Active Directory регистрируется в клиенте M365.</span><span class="sxs-lookup"><span data-stu-id="5e60b-160">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="5e60b-161">Манифест приложения отправляется на портал разработчика для Teams.</span><span class="sxs-lookup"><span data-stu-id="5e60b-161">An app manifest is submitted to the Developer Portal for Teams.</span></span>
- <span data-ttu-id="5e60b-162">API запускается локально с помощью Azure Functions Core Tools для поддержки приложения.</span><span class="sxs-lookup"><span data-stu-id="5e60b-162">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="5e60b-163">[ngrok](https://ngrok.io) устанавливается и используется для обеспечения туннеля между Teams и расширением для сообщений.</span><span class="sxs-lookup"><span data-stu-id="5e60b-163">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your messaging extension.</span></span>

<span data-ttu-id="5e60b-164">Чтобы создать и запустить приложение локально, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5e60b-164">To build and run your app locally:</span></span>

1. <span data-ttu-id="5e60b-165">В Visual Studio Code нажмите клавишу **F5**, чтобы запустить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="5e60b-165">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="5e60b-166">При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.</span><span class="sxs-lookup"><span data-stu-id="5e60b-166">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="5e60b-167">По завершении сборки автоматически откроется окно браузера.</span><span class="sxs-lookup"><span data-stu-id="5e60b-167">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="5e60b-168">Для завершения может потребоваться от 3 до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="5e60b-168">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="5e60b-169">В браузере будет выполнена загрузка Teams, и вам будет предложено войти.</span><span class="sxs-lookup"><span data-stu-id="5e60b-169">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="5e60b-170">При появлении запроса на открытие Microsoft Teams выберите "Отменить", чтобы остаться в браузере.</span><span class="sxs-lookup"><span data-stu-id="5e60b-170">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="5e60b-171">Войдите с помощью своей учетной записи M365.</span><span class="sxs-lookup"><span data-stu-id="5e60b-171">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="5e60b-172">Нажмите **Добавить**, чтобы добавить приложение в свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="5e60b-172">Press **Add** to add the app to your account.</span></span>

<span data-ttu-id="5e60b-173">После загрузки приложения откроется диалоговое окно поиска.</span><span class="sxs-lookup"><span data-stu-id="5e60b-173">Once the app is loaded, you will be taken directly to a search dialog:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="Принцип работы расширения для сообщений на основе поиска":::

<span data-ttu-id="5e60b-175">Введите текст в поле поиска и выберите один из вариантов.</span><span class="sxs-lookup"><span data-stu-id="5e60b-175">Type some text in the search box, then select one of the options.</span></span>  <span data-ttu-id="5e60b-176">В поле ввода будет добавлена адаптивная карточка.</span><span class="sxs-lookup"><span data-stu-id="5e60b-176">An adaptive card will be added to your input box.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="5e60b-177">Узнайте, что происходит при локальном запуске приложения в отладчике.</span><span class="sxs-lookup"><span data-stu-id="5e60b-177">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="5e60b-178">При нажатии клавиши F5 набор средств Teams:</span><span class="sxs-lookup"><span data-stu-id="5e60b-178">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="5e60b-179">Зарегистрировал приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5e60b-179">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="5e60b-180">Зарегистрировал приложение для установки неопубликованных приложений в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="5e60b-180">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="5e60b-181">Запустил серверную часть приложения локально с помощью [Azure Functions Core Tools](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="5e60b-181">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="5e60b-182">Запустил туннель ngrok, чтобы обеспечить взаимодействие Teams с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="5e60b-182">Started an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="5e60b-183">Запустил Microsoft Teams с помощью команды, обеспечивающей установку неопубликованного приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="5e60b-183">Started Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="5e60b-184">Узнайте, как устранить распространенные проблемы при локальном запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="5e60b-184">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="5e60b-185">Чтобы запустить приложение в Teams, у вас должна быть учетная запись разработчика Microsoft 365, позволяющая устанавливать неопубликованные приложения.</span><span class="sxs-lookup"><span data-stu-id="5e60b-185">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="5e60b-186">Дополнительные сведения о создании учетной записи см. в разделе [Необходимые компоненты](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="5e60b-186">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="5e60b-187">Перед установкой неопубликованного приложения проверьте наличие проблем с помощью [средства проверки приложений](https://dev.teams.microsoft.com/appvalidation.html), которое входит в набор средств.</span><span class="sxs-lookup"><span data-stu-id="5e60b-187">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="5e60b-188">Исправьте ошибки, чтобы успешно установить неопубликованное приложение.</span><span class="sxs-lookup"><span data-stu-id="5e60b-188">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="5e60b-189">Узнайте, что происходит после развертывания приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="5e60b-189">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="5e60b-190">До развертывания приложение работает локально:</span><span class="sxs-lookup"><span data-stu-id="5e60b-190">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="5e60b-191">Серверная часть работает с использованием _Azure Functions Core Tools_.</span><span class="sxs-lookup"><span data-stu-id="5e60b-191">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="5e60b-192">Конечная точка HTTP приложения, в которую Microsoft Teams загружает приложение, работает локально.</span><span class="sxs-lookup"><span data-stu-id="5e60b-192">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="5e60b-193">Развертывание включает подготовку ресурсов для активной подписки Azure и развертывание (загрузку) внутреннего и внешнего кода приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="5e60b-193">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="5e60b-194">Серверная часть использует различные службы Azure, включая службу приложений Azure и службу Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="5e60b-194">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="add-a-configuration-page-to-your-messaging-extension"></a><span data-ttu-id="5e60b-195">Добавление страницы конфигурации в расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="5e60b-195">Add a configuration page to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="code-sample"></a><span data-ttu-id="5e60b-196">Пример кода</span><span class="sxs-lookup"><span data-stu-id="5e60b-196">Code sample</span></span>

<span data-ttu-id="5e60b-197">В Teams в примере проектов по GitHub показано, как создавать расширения обмена сообщениями, включающие страницу конфигурации и проверку подлинности службы [ботов.](https://github.com/microsoft/BotBuilder-Samples#teams-samples)</span><span class="sxs-lookup"><span data-stu-id="5e60b-197">The Teams Search Auth Config for sample projects on GitHub, demonstrate how to create messaging extensions that include a configuration page and [Bot Service authentication](https://github.com/microsoft/BotBuilder-Samples#teams-samples).</span></span> <span data-ttu-id="5e60b-198">В примерах также показано, как создавать расширения сообщений, которые принимают запросы на поиск и возвращают результаты после того, как пользователь вписался.</span><span class="sxs-lookup"><span data-stu-id="5e60b-198">The samples also demonstrate how to create message extensions that accept search requests and return the results after the user has signed in.</span></span>

| <span data-ttu-id="5e60b-199">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="5e60b-199">**Sample name**</span></span> | <span data-ttu-id="5e60b-200">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5e60b-200">**Description**</span></span> | <span data-ttu-id="5e60b-201">**.NET**</span><span class="sxs-lookup"><span data-stu-id="5e60b-201">**.NET**</span></span> | <span data-ttu-id="5e60b-202">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="5e60b-202">**Node.js**</span></span> | <span data-ttu-id="5e60b-203">**Python**</span><span class="sxs-lookup"><span data-stu-id="5e60b-203">**Python**</span></span> |
|-----------------|-----------------|-------------|--------------|--------|
| <span data-ttu-id="5e60b-204">Строитель ботов</span><span class="sxs-lookup"><span data-stu-id="5e60b-204">Bot builder</span></span> | <span data-ttu-id="5e60b-205">Создание расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="5e60b-205">To create messaging extensions.</span></span> | [<span data-ttu-id="5e60b-206">View</span><span class="sxs-lookup"><span data-stu-id="5e60b-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="5e60b-207">View</span><span class="sxs-lookup"><span data-stu-id="5e60b-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="5e60b-208">View</span><span class="sxs-lookup"><span data-stu-id="5e60b-208">View</span></span>]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a><span data-ttu-id="5e60b-209">Дополнительный пример кода</span><span class="sxs-lookup"><span data-stu-id="5e60b-209">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e60b-210">Просмотр дополнительных примеров bot Framework в GitHub</span><span class="sxs-lookup"><span data-stu-id="5e60b-210">View more Bot Framework Samples on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="next-steps"></a><span data-ttu-id="5e60b-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e60b-211">Next steps</span></span>

<span data-ttu-id="5e60b-212">Узнайте о других методах создания приложений Teams:</span><span class="sxs-lookup"><span data-stu-id="5e60b-212">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="5e60b-213">Создание приложения Teams с помощью React</span><span class="sxs-lookup"><span data-stu-id="5e60b-213">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="5e60b-214">Создание приложения Teams с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="5e60b-214">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="5e60b-215">[Создание приложения Teams в формате веб-части SharePoint](first-app-spfx.md) (Azure не требуется)</span><span class="sxs-lookup"><span data-stu-id="5e60b-215">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="5e60b-216">Создание бота для общения</span><span class="sxs-lookup"><span data-stu-id="5e60b-216">Create a conversation bot</span></span>](first-app-bot.md)
