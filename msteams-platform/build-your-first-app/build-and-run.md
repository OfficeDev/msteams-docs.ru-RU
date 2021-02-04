---
title: 'Начало работы : сборка и запуск первого приложения'
author: heath-hamilton
description: Быстро создайте приложение Microsoft Teams, которое отображает "Hello, World!" сообщение с помощью microsoft Teams набор средств.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093952"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="7f786-104">Создание и запуск первого приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7f786-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="7f786-105">Начните разработку Microsoft Teams, построив личную вкладку "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="7f786-105">Start Microsoft Teams development by building a personal tab that displays "Hello, World!".</span></span>
<span data-ttu-id="7f786-106">Создайте и запустите свое первое приложение Teams с помощью следующих действий:</span><span class="sxs-lookup"><span data-stu-id="7f786-106">Build and run your first Teams app using the following steps:</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="7f786-107">1. Создайте проект приложения</span><span class="sxs-lookup"><span data-stu-id="7f786-107">1. Create your app project</span></span>

<span data-ttu-id="7f786-108">Используйте microsoft Teams набор средств в Visual Studio Code, чтобы настроить свой первый проект приложения.</span><span class="sxs-lookup"><span data-stu-id="7f786-108">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span> <span data-ttu-id="7f786-109">Создайте проект приложения с помощью следующих действий:</span><span class="sxs-lookup"><span data-stu-id="7f786-109">Create your app project using the following steps:</span></span>

1. В Visual Studio кода выберите **Microsoft Teams** в левой панели действий и выберите :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **"Создать новое приложение Teams".**
1. <span data-ttu-id="7f786-111">При запросе во sign in with your Microsoft 365 development account.</span><span class="sxs-lookup"><span data-stu-id="7f786-111">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="7f786-112">На экране **"Добавление возможностей" выберите** "Вкладка", а затем  **"Далее".**</span><span class="sxs-lookup"><span data-stu-id="7f786-112">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Screenshot showing how to configure your app project with the Visual Studio Code Teams набор средств.":::
1. <span data-ttu-id="7f786-114">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="7f786-114">Enter a name for your Teams app.</span></span> <span data-ttu-id="7f786-115">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="7f786-115">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="7f786-116">Проверьте только параметр **"Личная вкладка"** и выберите "Готово" в нижней части экрана, чтобы настроить проект. </span><span class="sxs-lookup"><span data-stu-id="7f786-116">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="7f786-117">2. Понимание важных компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="7f786-117">2. Understand important app project components</span></span>

<span data-ttu-id="7f786-118">После того как набор средств настроит проект, у вас будут компоненты для создания базовой личной вкладки для Teams.</span><span class="sxs-lookup"><span data-stu-id="7f786-118">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="7f786-119">Каталоги и файлы проекта отображаются в области проводника Visual Studio кода.</span><span class="sxs-lookup"><span data-stu-id="7f786-119">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Screenshot showing app project files for a personal tab in Visual Studio Code.":::

### <a name="app-scaffolding"></a><span data-ttu-id="7f786-121">Скафаолдинг приложений</span><span class="sxs-lookup"><span data-stu-id="7f786-121">App scaffolding</span></span>

<span data-ttu-id="7f786-122">Набор средств автоматически создает скафолдинг для вас в каталоге на основе возможностей, добавленных `src` во время установки.</span><span class="sxs-lookup"><span data-stu-id="7f786-122">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="7f786-123">Например, если вы создаете вкладку во время установки, файл в каталоге имеет важное значение, так как он обрабатывает инициализацию и `App.js` `src/components` маршрутизацию приложения.</span><span class="sxs-lookup"><span data-stu-id="7f786-123">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="7f786-124">Он вызывает [клиентский SDK JavaScript](../tabs/how-to/using-teams-client-sdk.md) для Microsoft Teams, чтобы установить связь между вашим приложением и Teams.</span><span class="sxs-lookup"><span data-stu-id="7f786-124">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="7f786-125">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="7f786-125">App ID</span></span>

<span data-ttu-id="7f786-126">Настройте приложение с помощью App Studio с помощью ИД приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="7f786-126">Configure your app with App Studio using the Teams app ID.</span></span> <span data-ttu-id="7f786-127">Найдите ИД в объекте, который находится `teamsAppId` в файле `package.json` проекта.</span><span class="sxs-lookup"><span data-stu-id="7f786-127">Find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="7f786-128">3. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="7f786-128">3. Build and run your app</span></span>

<span data-ttu-id="7f786-129">Создайте и запустите приложение локально, чтобы сэкономить время.</span><span class="sxs-lookup"><span data-stu-id="7f786-129">Build and run your app locally to save time.</span></span> <span data-ttu-id="7f786-130">Эти сведения также доступны в наборе `README` средств.</span><span class="sxs-lookup"><span data-stu-id="7f786-130">This information is also available in the toolkit `README`.</span></span> <span data-ttu-id="7f786-131">Создайте и запустите приложение с помощью следующих действий:</span><span class="sxs-lookup"><span data-stu-id="7f786-131">Build and run your app using the following steps:</span></span>

1. <span data-ttu-id="7f786-132">В терминале перейдите в корневой каталог проекта приложения и запустите `npm install` его.</span><span class="sxs-lookup"><span data-stu-id="7f786-132">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="7f786-133">Запустите `npm start` .</span><span class="sxs-lookup"><span data-stu-id="7f786-133">Run `npm start`.</span></span>

<span data-ttu-id="7f786-134">После завершения компилятор **успешно скомпилироваться!**</span><span class="sxs-lookup"><span data-stu-id="7f786-134">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="7f786-135">сообщение в терминале.</span><span class="sxs-lookup"><span data-stu-id="7f786-135">message in the terminal.</span></span> <span data-ttu-id="7f786-136">Ваше приложение работает в `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="7f786-136">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="7f786-137">4. Загрузка неогрузки приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="7f786-137">4. Sideload your app in Teams</span></span>

<span data-ttu-id="7f786-138">Ваше приложение готово для тестирования в Teams.</span><span class="sxs-lookup"><span data-stu-id="7f786-138">Your app is ready to test in Teams.</span></span> <span data-ttu-id="7f786-139">Для этого у вас должна быть учетная запись разработки Microsoft 365, которая разрешает загрузку нео том же приложения.</span><span class="sxs-lookup"><span data-stu-id="7f786-139">To do this, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="7f786-140">Дополнительные сведения об открытии учетной записи см. в [записи разработки Teams.](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)</span><span class="sxs-lookup"><span data-stu-id="7f786-140">For more information on account opening, see [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).</span></span> 

> [!TIP]
> <span data-ttu-id="7f786-141">Проверьте, есть ли проблемы перед загрузкой неогрузки приложения с помощью функции проверки [в App Studio,](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)которая включена в набор средств.</span><span class="sxs-lookup"><span data-stu-id="7f786-141">Check for issues before sideloading your app, using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="7f786-142">Исправьте ошибки для успешной загрузки неокрепленного приложения.</span><span class="sxs-lookup"><span data-stu-id="7f786-142">Fix the errors to successfully sideload the app.</span></span>

<span data-ttu-id="7f786-143">Загрузка неогрузки приложения в Teams с помощью следующих действий:</span><span class="sxs-lookup"><span data-stu-id="7f786-143">Sideload your app in Teams using the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="7f786-144">Чтобы включить загрузку нео том же приложения перед загрузкой неогрузки в Teams, выполните действия, которые необходимо предпринять в этой [части.](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)</span><span class="sxs-lookup"><span data-stu-id="7f786-144">To enable sideloading before you sideload your app in Teams, follow the steps in [Turn on app sideloading](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

1. <span data-ttu-id="7f786-145">Выберите **клавишу F5,** чтобы запустить веб-клиент Teams в Visual Studio коде.</span><span class="sxs-lookup"><span data-stu-id="7f786-145">Select the **F5** key to launch a Teams web client in Visual Studio Code.</span></span>
1. <span data-ttu-id="7f786-146">Чтобы отобразить содержимое приложения в Teams, укажите, что приложение является `localhost` надежным:</span><span class="sxs-lookup"><span data-stu-id="7f786-146">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="7f786-147">Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которая была открыта после нажатия **F5.**</span><span class="sxs-lookup"><span data-stu-id="7f786-147">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="7f786-148">Перейдите `https://localhost:3000/tab` на страницу и перейдите на нее.</span><span class="sxs-lookup"><span data-stu-id="7f786-148">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="7f786-149">Вернуться в Teams.</span><span class="sxs-lookup"><span data-stu-id="7f786-149">Go back to Teams.</span></span> <span data-ttu-id="7f786-150">В диалоговом оке выберите **"Добавить для меня",** чтобы установить приложение.</span><span class="sxs-lookup"><span data-stu-id="7f786-150">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Снимок экрана с примером приложения личной вкладки &quot;Hello, World!&quot;, запущенного в Teams.":::

<span data-ttu-id="7f786-152">🎉 поздравляем!</span><span class="sxs-lookup"><span data-stu-id="7f786-152">🎉 Congratulations!</span></span> <span data-ttu-id="7f786-153">Ваше приложение работает в Teams.</span><span class="sxs-lookup"><span data-stu-id="7f786-153">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="7f786-154">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="7f786-154">Next step</span></span>

<span data-ttu-id="7f786-155">Разведите личные вкладки, которые вы только что создали, или создайте приложение Teams другого типа.</span><span class="sxs-lookup"><span data-stu-id="7f786-155">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f786-156">Добавление на личную вкладку</span><span class="sxs-lookup"><span data-stu-id="7f786-156">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="7f786-157">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="7f786-157">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="7f786-158">Создание бота</span><span class="sxs-lookup"><span data-stu-id="7f786-158">Build a bot</span></span>](../build-your-first-app/build-bot.md)
