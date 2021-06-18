---
title: Начало работы — Создание первого чат-бота
author: adrianhall
description: Создание чат-бота для Microsoft Teams с помощью набора средств Teams.
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: e59980e7f33c326c16faefd412f9845e47f234e5
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994261"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a><span data-ttu-id="37603-103">Создание первого чат-бота для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="37603-103">Build your first conversational bot for Microsoft Teams</span></span>

<span data-ttu-id="37603-104">Чат-бот выступает в качестве посредника между пользователем Teams и веб-службой.</span><span class="sxs-lookup"><span data-stu-id="37603-104">A bot acts as an intermediary between a Teams user and a web service.</span></span>  <span data-ttu-id="37603-105">Пользователи могут общаться с ботом, чтобы быстро получить информацию, инициировать рабочие процессы или выполнить другие действия, предлагаемые веб-службой.</span><span class="sxs-lookup"><span data-stu-id="37603-105">Users can chat with a bot to quickly get information, initiate workflows, or anything else your web service can do.</span></span>  <span data-ttu-id="37603-106">Это руководство содержит сведения о том, как создать, запустить и развернуть чат-бота для Teams.</span><span class="sxs-lookup"><span data-stu-id="37603-106">In this tutorial, you will learn how to build, run, and deploy a Teams bot app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="37603-107">Подготовка к работе</span><span class="sxs-lookup"><span data-stu-id="37603-107">Before you begin</span></span>

<span data-ttu-id="37603-108">Настройте среду разработки, установив [необходимые компоненты](prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="37603-108">Make sure your development environment is set up by installing the [Prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37603-109">Установка необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="37603-109">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="37603-110">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="37603-110">Create your project</span></span>

<span data-ttu-id="37603-111">Используйте набор средств Teams для создания своего первого проекта.</span><span class="sxs-lookup"><span data-stu-id="37603-111">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="37603-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="37603-112">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="37603-113">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="37603-113">Open Visual Studio code.</span></span>
1. <span data-ttu-id="37603-114">Откройте набор средств Teams, выбрав значок Teams на боковой панели:</span><span class="sxs-lookup"><span data-stu-id="37603-114">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. <span data-ttu-id="37603-116">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="37603-116">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. <span data-ttu-id="37603-118">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="37603-118">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания нового проекта":::

1. <span data-ttu-id="37603-120">На этапе **Выбор возможностей** выберите **Бот** и снимите флажок рядом с пунктом **Вкладка**. Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="37603-120">On the **Select capabilities** step, select **Bot** and deselect **Tab**.  Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. <span data-ttu-id="37603-122">На этапе **Регистрация бота** выберите **Создать новую регистрацию бота**.</span><span class="sxs-lookup"><span data-stu-id="37603-122">On the **Bot registration** step, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Выбор создания новой регистрации бота":::

1. <span data-ttu-id="37603-124">На этапе **Язык программирования** выберите **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="37603-124">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Снимок экрана: выбор языка.":::

1. <span data-ttu-id="37603-126">Выберите папку рабочей области.</span><span class="sxs-lookup"><span data-stu-id="37603-126">Select a workspace folder.</span></span>  <span data-ttu-id="37603-127">В папке рабочей области будет создана папка для создаваемого проекта.</span><span class="sxs-lookup"><span data-stu-id="37603-127">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="37603-128">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="37603-128">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="37603-129">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="37603-129">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="37603-130">Чтобы продолжить, нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="37603-130">Press **Enter** to continue.</span></span>

<span data-ttu-id="37603-131">Создание приложения Teams займет несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="37603-131">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="37603-132">Командная строка</span><span class="sxs-lookup"><span data-stu-id="37603-132">Command line</span></span>](#tab/cli)

<span data-ttu-id="37603-133">Используйте для создания первого проекта интерфейс командной строки `teamsfx`.</span><span class="sxs-lookup"><span data-stu-id="37603-133">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="37603-134">Начните с папки, в которой будет создана папка проекта.</span><span class="sxs-lookup"><span data-stu-id="37603-134">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="37603-135">Интерфейс командной строки выдаст несколько вопросов, ответы на которые используются для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="37603-135">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="37603-136">Каждый вопрос сопровождается подсказкой о том, как на него отвечать (например, использовать клавиши со стрелками для выбора варианта).</span><span class="sxs-lookup"><span data-stu-id="37603-136">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="37603-137">Ответив на вопрос, подтвердите свой выбор, нажав клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="37603-137">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="37603-138">Выберите **Создать приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="37603-138">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="37603-139">Выберите возможность **Бот** и снимите флажок рядом с возможностью **Вкладка**.</span><span class="sxs-lookup"><span data-stu-id="37603-139">Select the **Bot** capability and deselect the **Tab** capability.</span></span>
1. <span data-ttu-id="37603-140">Выберите **Создать новую регистрацию бота**.</span><span class="sxs-lookup"><span data-stu-id="37603-140">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="37603-141">Выберите **JavaScript** в качестве языка.</span><span class="sxs-lookup"><span data-stu-id="37603-141">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="37603-142">Нажмите клавишу **ВВОД**, чтобы выбрать папку рабочей области по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="37603-142">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="37603-143">Введите подходящее имя для приложения, например `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="37603-143">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="37603-144">Имя приложения должно состоять только из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="37603-144">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="37603-145">После того, как вы ответите на все вопросы, будет создан проект.</span><span class="sxs-lookup"><span data-stu-id="37603-145">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="37603-146">Знакомство с исходным кодом</span><span class="sxs-lookup"><span data-stu-id="37603-146">Take a tour of the source code</span></span>

<span data-ttu-id="37603-147">Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="37603-147">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="37603-148">Расширение для сообщений использует [Bot Framework](https://docs.botframework.com), чтобы дать пользователю возможность взаимодействовать со службой посредством общения.</span><span class="sxs-lookup"><span data-stu-id="37603-148">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="37603-149">После генерации кода проект будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="37603-149">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="Макет файла проекта бота.":::

<span data-ttu-id="37603-151">Код бота хранится в каталоге `bot`.</span><span class="sxs-lookup"><span data-stu-id="37603-151">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="37603-152">`bots/teamsBot.js` — основная точка входа для бота. Диалоги хранятся в каталоге `dialogs`.</span><span class="sxs-lookup"><span data-stu-id="37603-152">The `bots/teamsBot.js` is the main entry point for the bot, and the dialogs are stored in the `dialogs` directory.</span></span>

> [!Tip]
> <span data-ttu-id="37603-153">Перед интеграцией своего первого бота в Teams ознакомьтесь с чат-ботами за пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="37603-153">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="37603-154">Дополнительные сведения о ботах см. в руководстве [Служба Azure Bot](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="37603-154">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="37603-155">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="37603-155">Run your app locally</span></span>

<span data-ttu-id="37603-156">Набор средств Teams позволяет размещать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="37603-156">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="37603-157">Для этого:</span><span class="sxs-lookup"><span data-stu-id="37603-157">To do this:</span></span>

- <span data-ttu-id="37603-158">Приложение Azure Active Directory регистрируется в клиенте M365.</span><span class="sxs-lookup"><span data-stu-id="37603-158">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="37603-159">Манифест приложения отправляется в Центр разработчиков для Teams.</span><span class="sxs-lookup"><span data-stu-id="37603-159">An app manifest is submitted to the Developer Center for Teams.</span></span>
- <span data-ttu-id="37603-160">API запускается локально с помощью Azure Functions Core Tools для поддержки приложения.</span><span class="sxs-lookup"><span data-stu-id="37603-160">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="37603-161">[ngrok](https://ngrok.io) устанавливается и используется для обеспечения туннеля между Teams и кодом бота.</span><span class="sxs-lookup"><span data-stu-id="37603-161">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your bot code.</span></span>

<span data-ttu-id="37603-162">Чтобы создать и запустить приложение локально, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="37603-162">To build and run your app locally:</span></span>

1. <span data-ttu-id="37603-163">В Visual Studio Code нажмите клавишу **F5**, чтобы запустить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="37603-163">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="37603-164">При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.</span><span class="sxs-lookup"><span data-stu-id="37603-164">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="37603-165">По завершении сборки автоматически откроется окно браузера.</span><span class="sxs-lookup"><span data-stu-id="37603-165">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="37603-166">Для завершения может потребоваться от 3 до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="37603-166">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="37603-167">Веб-браузер начинает запускать приложение.</span><span class="sxs-lookup"><span data-stu-id="37603-167">Your web browser starts to run the app.</span></span> <span data-ttu-id="37603-168">Если вам будет предложено открыть Teams рабочий стол, выберите **Отмена,** чтобы оставаться в браузере.</span><span class="sxs-lookup"><span data-stu-id="37603-168">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="37603-169">Вам также может быть предложено перейти на рабочий Teams в другое время; выберите Teams веб-приложение, когда это произойдет.</span><span class="sxs-lookup"><span data-stu-id="37603-169">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Снимок экрана: выбор веб-версии Teams при запуске":::

1. <span data-ttu-id="37603-171">Вам может быть предложено выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="37603-171">You may be prompted to sign in.</span></span>  <span data-ttu-id="37603-172">В этом случае войдите с учетной записью M365.</span><span class="sxs-lookup"><span data-stu-id="37603-172">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="37603-173">При появлении запроса на установку приложения в Teams нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="37603-173">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="37603-174">После загрузки приложения запустится сеанс общения с ботом.</span><span class="sxs-lookup"><span data-stu-id="37603-174">Once the app is loaded, you will be taken directly to a chat session with the bot.</span></span>  <span data-ttu-id="37603-175">Вы можете ввести `intro`, чтобы просмотреть ознакомительную карточку, и `show`, чтобы просмотреть свои данные в Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="37603-175">You can type `intro` to show an introduction card, and `show` to show your details from Microsoft Graph.</span></span>  <span data-ttu-id="37603-176">(Для этого потребуется утверждение дополнительных разрешений).</span><span class="sxs-lookup"><span data-stu-id="37603-176">(This will require an additional permissions approval).</span></span>

<span data-ttu-id="37603-177">Отладка работает надлежащим образом — попробуйте сами!</span><span class="sxs-lookup"><span data-stu-id="37603-177">Debugging works as you normally would expect - try it yourself!</span></span> <span data-ttu-id="37603-178">Откройте файл `bot/dialogs/rootDialog.js` и найдите метод `triggerCommand(...)`.</span><span class="sxs-lookup"><span data-stu-id="37603-178">Open the `bot/dialogs/rootDialog.js` file and locate the `triggerCommand(...)` method.</span></span>  <span data-ttu-id="37603-179">Задайте точку останова для варианта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="37603-179">Set a breakpoint on the default case.</span></span>  <span data-ttu-id="37603-180">Затем введите какой-нибудь текст.</span><span class="sxs-lookup"><span data-stu-id="37603-180">Then type some text.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="37603-181">Узнайте, что происходит при локальном запуске приложения в отладчике.</span><span class="sxs-lookup"><span data-stu-id="37603-181">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="37603-182">При нажатии клавиши F5 набор средств Teams:</span><span class="sxs-lookup"><span data-stu-id="37603-182">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="37603-183">Зарегистрировал приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37603-183">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="37603-184">Зарегистрировал приложение для установки неопубликованных приложений в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="37603-184">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="37603-185">Запустил серверную часть приложения локально с помощью [Azure Functions Core Tools](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="37603-185">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="37603-186">Запустил туннель ngrok, чтобы обеспечить взаимодействие Teams с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="37603-186">Started an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="37603-187">Запустил Microsoft Teams с помощью команды, обеспечивающей установку неопубликованного приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="37603-187">Started Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="37603-188">Узнайте, как устранить распространенные проблемы при локальном запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="37603-188">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="37603-189">Чтобы запустить приложение в Teams, у вас должна быть учетная запись разработчика Microsoft 365, позволяющая устанавливать неопубликованные приложения.</span><span class="sxs-lookup"><span data-stu-id="37603-189">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="37603-190">Дополнительные сведения о создании учетной записи см. в разделе [Необходимые компоненты](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="37603-190">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="37603-191">Перед установкой неопубликованного приложения проверьте наличие проблем с помощью [средства проверки приложений](https://dev.teams.microsoft.com/appvalidation.html), которое входит в набор средств.</span><span class="sxs-lookup"><span data-stu-id="37603-191">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="37603-192">Исправьте ошибки, чтобы успешно установить неопубликованное приложение.</span><span class="sxs-lookup"><span data-stu-id="37603-192">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="37603-193">Узнайте, что происходит после развертывания приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="37603-193">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="37603-194">До развертывания приложение работает локально:</span><span class="sxs-lookup"><span data-stu-id="37603-194">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="37603-195">Серверная часть работает с использованием _Azure Functions Core Tools_.</span><span class="sxs-lookup"><span data-stu-id="37603-195">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="37603-196">Конечная точка HTTP приложения, в которую Microsoft Teams загружает приложение, работает локально.</span><span class="sxs-lookup"><span data-stu-id="37603-196">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="37603-197">Развертывание включает подготовку ресурсов для активной подписки Azure и развертывание (загрузку) внутреннего и внешнего кода приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="37603-197">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="37603-198">Серверная часть использует различные службы Azure, включая службу приложений Azure и службу Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="37603-198">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="37603-199">См. также</span><span class="sxs-lookup"><span data-stu-id="37603-199">See also</span></span>

- [<span data-ttu-id="37603-200">Создание приложения Teams с помощью React</span><span class="sxs-lookup"><span data-stu-id="37603-200">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="37603-201">Создание приложения Teams с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="37603-201">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="37603-202">[Создание приложения Teams в формате веб-части SharePoint](first-app-spfx.md) (Azure не требуется)</span><span class="sxs-lookup"><span data-stu-id="37603-202">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>

## <a name="next-step"></a><span data-ttu-id="37603-203">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="37603-203">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37603-204">Создание расширения для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="37603-204">Create a messaging extension</span></span>](first-message-extension.md)
