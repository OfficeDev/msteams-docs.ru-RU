---
title: Начало работы — сборка и запуск первого приложения
author: heath-hamilton
description: Быстро создайте приложение Microsoft Teams, которое отображает "Hello, World!" сообщение с помощью microsoft Teams набор средств.
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 1b34c3f3121e834abc8a8a92a8a0ac9a049c9e07
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020886"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="e74cb-104">Создание и запуск первого приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e74cb-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="e74cb-105">Начните разработку Microsoft Teams с создания личной вкладки с отображением "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="e74cb-105">Start Microsoft Teams development by building a personal tab that displays "Hello, World!".</span></span>
<span data-ttu-id="e74cb-106">Создайте и запустите свое первое приложение Teams с помощью следующих действий:</span><span class="sxs-lookup"><span data-stu-id="e74cb-106">Build and run your first Teams app using the following steps:</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="e74cb-107">1. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="e74cb-107">1. Create your app project</span></span>

<span data-ttu-id="e74cb-108">Используйте microsoft Teams набор средств в Visual Studio коде, чтобы настроить свой первый проект приложения.</span><span class="sxs-lookup"><span data-stu-id="e74cb-108">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span> <span data-ttu-id="e74cb-109">Создайте проект приложения с помощью следующих действий:</span><span class="sxs-lookup"><span data-stu-id="e74cb-109">Create your app project using the following steps:</span></span>

1. В Visual Studio коде выберите **Microsoft Teams** в левой панели действий и создайте новое приложение :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams.**
1. <span data-ttu-id="e74cb-111">При запросе впишитесь в учетную запись разработки Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="e74cb-111">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="e74cb-112">На экране **Добавить возможности** выберите **вкладку затем** **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e74cb-112">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Снимок экрана, показывающий, как настроить проект приложения с помощью Visual Studio команд кода набор средств.":::
1. <span data-ttu-id="e74cb-114">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="e74cb-114">Enter a name for your Teams app.</span></span> <span data-ttu-id="e74cb-115">(Это имя по умолчанию для вашего приложения, а также имя каталога проектов приложений на локальной машине.)</span><span class="sxs-lookup"><span data-stu-id="e74cb-115">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="e74cb-116">Проверьте только параметр **Личные вкладки** и выберите **Готово** в нижней части экрана, чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="e74cb-116">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="e74cb-117">2. Понимание важных компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="e74cb-117">2. Understand important app project components</span></span>

<span data-ttu-id="e74cb-118">Как только набор инструментов настраивает проект, у вас есть компоненты для создания базовой личной вкладки для Teams.</span><span class="sxs-lookup"><span data-stu-id="e74cb-118">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="e74cb-119">Каталоги проектов и файлы отображаются в области Explorer Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e74cb-119">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Снимок экрана, показывающий файлы проектов приложений для личной вкладки Visual Studio Code.":::

### <a name="app-scaffolding"></a><span data-ttu-id="e74cb-121">Строительные леса приложений</span><span class="sxs-lookup"><span data-stu-id="e74cb-121">App scaffolding</span></span>

<span data-ttu-id="e74cb-122">Набор инструментов автоматически создает леса для вас в каталоге на основе возможностей, которые `src` вы добавили во время установки.</span><span class="sxs-lookup"><span data-stu-id="e74cb-122">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="e74cb-123">Например, если во время настройки создается вкладка, файл в каталоге имеет важное значение, так как он обрабатывает инициализацию и `App.js` `src/components` маршрутизацию приложения.</span><span class="sxs-lookup"><span data-stu-id="e74cb-123">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="e74cb-124">Он вызывает [SDK клиента Microsoft Teams JavaScript,](../tabs/how-to/using-teams-client-sdk.md) чтобы установить связь между вашим приложением и teams.</span><span class="sxs-lookup"><span data-stu-id="e74cb-124">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="e74cb-125">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="e74cb-125">App ID</span></span>

<span data-ttu-id="e74cb-126">Настройка приложения в App Studio с помощью ID приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="e74cb-126">Configure your app with App Studio using the Teams app ID.</span></span> <span data-ttu-id="e74cb-127">Найдите ID в `teamsAppId` объекте, который находится в файле `package.json` проекта.</span><span class="sxs-lookup"><span data-stu-id="e74cb-127">Find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="e74cb-128">3. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="e74cb-128">3. Build and run your app</span></span>

<span data-ttu-id="e74cb-129">Создайте и запустите приложение локально, чтобы сэкономить время.</span><span class="sxs-lookup"><span data-stu-id="e74cb-129">Build and run your app locally to save time.</span></span> <span data-ttu-id="e74cb-130">Эти сведения также доступны в наборе `README` инструментов.</span><span class="sxs-lookup"><span data-stu-id="e74cb-130">This information is also available in the toolkit `README`.</span></span> <span data-ttu-id="e74cb-131">Создайте и запустите приложение с помощью следующих действий:</span><span class="sxs-lookup"><span data-stu-id="e74cb-131">Build and run your app using the following steps:</span></span>

1. <span data-ttu-id="e74cb-132">В терминале перейдите в корневой каталог проекта приложения и запустите `npm install` .</span><span class="sxs-lookup"><span data-stu-id="e74cb-132">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="e74cb-133">Запуск `npm start` .</span><span class="sxs-lookup"><span data-stu-id="e74cb-133">Run `npm start`.</span></span>

<span data-ttu-id="e74cb-134">После завершения, есть **компилятор успешно!**</span><span class="sxs-lookup"><span data-stu-id="e74cb-134">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="e74cb-135">сообщение в терминале.</span><span class="sxs-lookup"><span data-stu-id="e74cb-135">message in the terminal.</span></span> <span data-ttu-id="e74cb-136">Ваше приложение `https://localhost:3000` запущено.</span><span class="sxs-lookup"><span data-stu-id="e74cb-136">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="e74cb-137">4. Sideload ваше приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="e74cb-137">4. Sideload your app in Teams</span></span>

<span data-ttu-id="e74cb-138">Ваше приложение готово для тестирования в Teams.</span><span class="sxs-lookup"><span data-stu-id="e74cb-138">Your app is ready to test in Teams.</span></span> <span data-ttu-id="e74cb-139">Для этого необходимо иметь учетную запись разработки Microsoft 365, которая позволяет загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="e74cb-139">To do this, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="e74cb-140">Дополнительные сведения об открытии учетной записи см. в [записи разработки Teams.](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)</span><span class="sxs-lookup"><span data-stu-id="e74cb-140">For more information on account opening, see [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).</span></span> 

> [!TIP]
> <span data-ttu-id="e74cb-141">Проверьте проблемы перед загрузкой приложения с помощью функции проверки в [App Studio,](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)которая входит в набор инструментов.</span><span class="sxs-lookup"><span data-stu-id="e74cb-141">Check for issues before sideloading your app, using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="e74cb-142">Устранение ошибок для успешной загрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="e74cb-142">Fix the errors to successfully sideload the app.</span></span>

<span data-ttu-id="e74cb-143">Загрузка приложения в Teams с помощью следующих действий:</span><span class="sxs-lookup"><span data-stu-id="e74cb-143">Sideload your app in Teams using the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="e74cb-144">Чтобы включить побную загрузку перед загрузкой приложения в Teams, выполните действия в [включите загрузку приложения.](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)</span><span class="sxs-lookup"><span data-stu-id="e74cb-144">To enable sideloading before you sideload your app in Teams, follow the steps in [Turn on app sideloading](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

1. <span data-ttu-id="e74cb-145">Выберите **клавишу F5** для запуска веб-клиента Teams в Visual Studio коде.</span><span class="sxs-lookup"><span data-stu-id="e74cb-145">Select the **F5** key to launch a Teams web client in Visual Studio Code.</span></span>
1. <span data-ttu-id="e74cb-146">Чтобы отобразить содержимое приложения в Teams, укажите, что в том месте, где работает ваше приложение ( `localhost` ) можно доверять:</span><span class="sxs-lookup"><span data-stu-id="e74cb-146">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="e74cb-147">Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которая открылась после нажатия **F5.**</span><span class="sxs-lookup"><span data-stu-id="e74cb-147">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="e74cb-148">Перейдите `https://localhost:3000/tab` на страницу и перейдите к этой странице.</span><span class="sxs-lookup"><span data-stu-id="e74cb-148">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="e74cb-149">Возвращайся в Teams.</span><span class="sxs-lookup"><span data-stu-id="e74cb-149">Go back to Teams.</span></span> <span data-ttu-id="e74cb-150">В диалоговом октаге **выберите Добавить для меня,** чтобы установить ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="e74cb-150">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Снимок экрана, показывающий пример личного приложения вкладки &quot;Hello, World!&quot;, запущенного в Teams.":::

<span data-ttu-id="e74cb-152">🎉 поздравляем!</span><span class="sxs-lookup"><span data-stu-id="e74cb-152">🎉 Congratulations!</span></span> <span data-ttu-id="e74cb-153">Ваше приложение работает в Teams.</span><span class="sxs-lookup"><span data-stu-id="e74cb-153">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="e74cb-154">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="e74cb-154">Next step</span></span>

<span data-ttu-id="e74cb-155">Разведите личные вкладки, которые вы только что создали, или создайте другое приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="e74cb-155">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e74cb-156">Добавление в личную вкладку</span><span class="sxs-lookup"><span data-stu-id="e74cb-156">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="e74cb-157">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="e74cb-157">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="e74cb-158">Создание бота</span><span class="sxs-lookup"><span data-stu-id="e74cb-158">Build a bot</span></span>](../build-your-first-app/build-bot.md)
