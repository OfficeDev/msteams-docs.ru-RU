---
title: 'Начало работы : сборка и запуск первого приложения'
author: heath-hamilton
description: Быстро создайте приложение Microsoft Teams, которое отображает "Hello, World!" сообщение с помощью microsoft Teams набор средств.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: bc5d18dd887cbdbf56b8d6d013f53c21d1540370
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795470"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="33c33-104">Создание и запуск первого приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="33c33-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="33c33-105">Вы можете сразу перейти к разработке для Microsoft Teams, построив личную вкладку с отображением "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="33c33-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="33c33-106">1. Создайте проект приложения</span><span class="sxs-lookup"><span data-stu-id="33c33-106">1. Create your app project</span></span>

<span data-ttu-id="33c33-107">Используйте microsoft Teams набор средств в Visual Studio Code, чтобы настроить свой первый проект приложения.</span><span class="sxs-lookup"><span data-stu-id="33c33-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. В Visual Studio кода выберите **Microsoft Teams** в левой панели действий и выберите :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **"Создать новое приложение Teams".**
1. <span data-ttu-id="33c33-109">При запросе во sign in with your Microsoft 365 development account.</span><span class="sxs-lookup"><span data-stu-id="33c33-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="33c33-110">На экране **"Добавление возможностей" выберите** "Вкладка", а затем  **"Далее".**</span><span class="sxs-lookup"><span data-stu-id="33c33-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Screenshot showing how to configure your app project with the Visual Studio Code Teams набор средств.":::
1. <span data-ttu-id="33c33-112">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="33c33-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="33c33-113">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="33c33-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="33c33-114">Проверьте только параметр **"Личная вкладка"** и выберите "Готово" в нижней части экрана, чтобы настроить проект. </span><span class="sxs-lookup"><span data-stu-id="33c33-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="33c33-115">2. Понимание важных компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="33c33-115">2. Understand important app project components</span></span>

<span data-ttu-id="33c33-116">После того как набор средств настроит проект, у вас будут компоненты для создания базовой личной вкладки для Teams.</span><span class="sxs-lookup"><span data-stu-id="33c33-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="33c33-117">Каталоги и файлы проекта отображаются в области проводника Visual Studio кода.</span><span class="sxs-lookup"><span data-stu-id="33c33-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Screenshot showing app project files for a personal tab in Visual Studio Code.":::

### <a name="app-scaffolding"></a><span data-ttu-id="33c33-119">Скафаолдинг приложений</span><span class="sxs-lookup"><span data-stu-id="33c33-119">App scaffolding</span></span>

<span data-ttu-id="33c33-120">Набор средств автоматически создает скафолдинг для вас в каталоге на основе возможностей, добавленных `src` во время установки.</span><span class="sxs-lookup"><span data-stu-id="33c33-120">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="33c33-121">Например, если вы создаете вкладку во время установки, файл в каталоге имеет важное значение, так как он обрабатывает инициализацию и `App.js` `src/components` маршрутизацию приложения.</span><span class="sxs-lookup"><span data-stu-id="33c33-121">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="33c33-122">Он вызывает [клиентский SDK JavaScript](../tabs/how-to/using-teams-client-sdk.md) для Microsoft Teams, чтобы установить связь между вашим приложением и Teams.</span><span class="sxs-lookup"><span data-stu-id="33c33-122">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="33c33-123">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="33c33-123">App ID</span></span>

<span data-ttu-id="33c33-124">Ваш ИД приложения Teams необходим для настройки приложения с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="33c33-124">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="33c33-125">Вы можете найти ИД в объекте, который находится в `teamsAppId` файле `package.json` проекта.</span><span class="sxs-lookup"><span data-stu-id="33c33-125">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="33c33-126">3. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="33c33-126">3. Build and run your app</span></span>

<span data-ttu-id="33c33-127">В интересах времени вы будете создавать и запускать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="33c33-127">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="33c33-128">(Эти сведения также доступны в наборе `README` средств.)</span><span class="sxs-lookup"><span data-stu-id="33c33-128">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="33c33-129">В терминале перейдите в корневой каталог проекта приложения и запустите `npm install` его.</span><span class="sxs-lookup"><span data-stu-id="33c33-129">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="33c33-130">Запустите `npm start` .</span><span class="sxs-lookup"><span data-stu-id="33c33-130">Run `npm start`.</span></span>

<span data-ttu-id="33c33-131">После завершения компилятор **успешно скомпилироваться!**</span><span class="sxs-lookup"><span data-stu-id="33c33-131">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="33c33-132">сообщение в терминале.</span><span class="sxs-lookup"><span data-stu-id="33c33-132">message in the terminal.</span></span> <span data-ttu-id="33c33-133">Ваше приложение работает в `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="33c33-133">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="33c33-134">4. Загрузка нео sideload приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="33c33-134">4. Sideload your app in Teams</span></span>

<span data-ttu-id="33c33-135">Ваше приложение готово для тестирования в Teams.</span><span class="sxs-lookup"><span data-stu-id="33c33-135">Your app is ready to test in Teams.</span></span> <span data-ttu-id="33c33-136">Для этого необходимо иметь учетную запись, которая разрешает загрузку нео том же приложения.</span><span class="sxs-lookup"><span data-stu-id="33c33-136">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="33c33-137">(Если вы не уверены в этом, узнайте о получении учетной записи [разработки Teams.)](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)</span><span class="sxs-lookup"><span data-stu-id="33c33-137">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="33c33-138">Перед загрузкой неогрузки приложения проверьте, нет ли проблем с использованием функции проверки [в App Studio,](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)которая включена в набор средств.</span><span class="sxs-lookup"><span data-stu-id="33c33-138">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="33c33-139">Для успешной загрузки неокрепленного приложения необходимо исправить ошибки.</span><span class="sxs-lookup"><span data-stu-id="33c33-139">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="33c33-140">В Visual Studio Code нажмите клавишу **F5,** чтобы запустить веб-клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="33c33-140">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="33c33-141">Чтобы отобразить содержимое приложения в Teams, укажите, где работает ваше приложение ( `localhost` ) является надежным:</span><span class="sxs-lookup"><span data-stu-id="33c33-141">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="33c33-142">Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которая была открыта после нажатия **F5.**</span><span class="sxs-lookup"><span data-stu-id="33c33-142">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="33c33-143">Перейдите `https://localhost:3000/tab` на страницу и перейдите на нее.</span><span class="sxs-lookup"><span data-stu-id="33c33-143">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="33c33-144">Вернуться в Teams.</span><span class="sxs-lookup"><span data-stu-id="33c33-144">Go back to Teams.</span></span> <span data-ttu-id="33c33-145">В диалоговом оке выберите **"Добавить для меня",** чтобы установить приложение.</span><span class="sxs-lookup"><span data-stu-id="33c33-145">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Снимок экрана с примером приложения личной вкладки &quot;Hello, World!&quot;, запущенного в Teams.":::

<span data-ttu-id="33c33-147">🎉 поздравляем!</span><span class="sxs-lookup"><span data-stu-id="33c33-147">🎉 Congratulations!</span></span> <span data-ttu-id="33c33-148">Ваше приложение работает в Teams.</span><span class="sxs-lookup"><span data-stu-id="33c33-148">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="33c33-149">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="33c33-149">Next step</span></span>

<span data-ttu-id="33c33-150">Разведите личные вкладки, которые вы только что создали, или создайте приложение Teams другого типа.</span><span class="sxs-lookup"><span data-stu-id="33c33-150">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="33c33-151">Добавление на личную вкладку</span><span class="sxs-lookup"><span data-stu-id="33c33-151">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="33c33-152">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="33c33-152">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="33c33-153">Создание бота</span><span class="sxs-lookup"><span data-stu-id="33c33-153">Build a bot</span></span>](../build-your-first-app/build-bot.md)
