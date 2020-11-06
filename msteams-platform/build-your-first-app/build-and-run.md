---
title: Начало работы — сборка и запуск первого приложения
author: heath-hamilton
description: Быстрое создание приложения Microsoft Teams, в котором отображается "Hello, World!". сообщение с помощью набора инструментов Microsoft Teams.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 62c4bd950183ceb64fb30b528661cf84e9210d89
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931781"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="bf986-104">Создание и запуск первого приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bf986-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="bf986-105">Вы можете перейти непосредственно к разработке Microsoft Teams, создав личную вкладку со значком "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="bf986-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="bf986-106">1. Создайте проект приложения.</span><span class="sxs-lookup"><span data-stu-id="bf986-106">1. Create your app project</span></span>

<span data-ttu-id="bf986-107">Используйте набор средств Microsoft Teams в Visual Studio Code, чтобы настроить первый проект приложения.</span><span class="sxs-lookup"><span data-stu-id="bf986-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
1. <span data-ttu-id="bf986-109">При появлении соответствующего запроса войдите в систему с помощью учетной записи разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="bf986-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="bf986-110">На экране **добавить возможности** выберите **вкладка** **Далее**.</span><span class="sxs-lookup"><span data-stu-id="bf986-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Снимок экрана, на котором показано, как настроить проект приложения с помощью набора инструментов Visual Studio Code Teams.":::
1. <span data-ttu-id="bf986-112">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="bf986-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="bf986-113">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="bf986-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="bf986-114">Установите флажок только для **личной вкладки** и в нижней части экрана нажмите кнопку **Готово** , чтобы настроить свой проект.</span><span class="sxs-lookup"><span data-stu-id="bf986-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="bf986-115">2. Изучите важные компоненты проекта приложения</span><span class="sxs-lookup"><span data-stu-id="bf986-115">2. Understand important app project components</span></span>

<span data-ttu-id="bf986-116">После того как набор инструментов настроит свой проект, у вас будут компоненты для создания базовой вкладки "личные" для Teams.</span><span class="sxs-lookup"><span data-stu-id="bf986-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="bf986-117">Каталоги и файлы проекта отображаются в области обозревателя Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bf986-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Снимок экрана, на котором показаны файлы проекта приложения для вкладки _OL_QUOTE_PLACEHOLDER_личные_OL_QUOTE_PLACEHOLDER_ в Visual Studio Code.":::

### <a name="app-scaffolding"></a><span data-ttu-id="bf986-119">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="bf986-119">App scaffolding</span></span>

<span data-ttu-id="bf986-120">Набор средств автоматически создает формирование шаблонов в `src` каталоге на основе возможностей, добавленных во время установки.</span><span class="sxs-lookup"><span data-stu-id="bf986-120">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="bf986-121">Например, при создании вкладки во время установки, `App.js` файл в `src/components` каталоге важен, так как он обрабатывает инициализацию и маршрутизацию приложения.</span><span class="sxs-lookup"><span data-stu-id="bf986-121">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="bf986-122">Он вызывает [пакет Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) для установления связи между приложением и Teams.</span><span class="sxs-lookup"><span data-stu-id="bf986-122">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="bf986-123">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="bf986-123">App ID</span></span>

<span data-ttu-id="bf986-124">Идентификатор приложения Teams необходим для настройки приложения с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="bf986-124">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="bf986-125">Вы можете найти идентификатор в `teamsAppId` объекте, который находится в `package.json` файле проекта.</span><span class="sxs-lookup"><span data-stu-id="bf986-125">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="bf986-126">3. Построение и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="bf986-126">3. Build and run your app</span></span>

<span data-ttu-id="bf986-127">В течение этого времени вы создадите и запустите свое приложение локально.</span><span class="sxs-lookup"><span data-stu-id="bf986-127">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="bf986-128">(Эти сведения также доступны в наборе инструментов `README` .)</span><span class="sxs-lookup"><span data-stu-id="bf986-128">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="bf986-129">В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .</span><span class="sxs-lookup"><span data-stu-id="bf986-129">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="bf986-130">Выполните команду `npm start` .</span><span class="sxs-lookup"><span data-stu-id="bf986-130">Run `npm start`.</span></span>

<span data-ttu-id="bf986-131">По завершении **компиляции успешно выполняется.**</span><span class="sxs-lookup"><span data-stu-id="bf986-131">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="bf986-132">сообщение в терминале.</span><span class="sxs-lookup"><span data-stu-id="bf986-132">message in the terminal.</span></span> <span data-ttu-id="bf986-133">Ваше приложение запущено `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="bf986-133">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="bf986-134">4. Загрузка неопубликованных ваше приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="bf986-134">4. Sideload your app in Teams</span></span>

<span data-ttu-id="bf986-135">Ваше приложение готово к тестированию в Teams.</span><span class="sxs-lookup"><span data-stu-id="bf986-135">Your app is ready to test in Teams.</span></span> <span data-ttu-id="bf986-136">Для этого необходимо иметь учетную запись, позволяющую выполнять загрузку неопубликованных приложений.</span><span class="sxs-lookup"><span data-stu-id="bf986-136">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="bf986-137">(Если вы не знаете этого, Узнайте о том, как получить [учетную запись разработки Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span><span class="sxs-lookup"><span data-stu-id="bf986-137">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="bf986-138">Прежде чем приступить к работе с неопубликованным приложением, проверьте наличие проблем с помощью [функции проверки в App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), которая включена в набор средств.</span><span class="sxs-lookup"><span data-stu-id="bf986-138">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="bf986-139">Чтобы успешно Загрузка неопубликованных приложение, необходимо исправить ошибки.</span><span class="sxs-lookup"><span data-stu-id="bf986-139">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="bf986-140">В Visual Studio Code нажмите клавишу **F5** , чтобы запустить веб-клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="bf986-140">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="bf986-141">Чтобы отобразить содержимое приложения в Teams, укажите, что приложение работает ( `localhost` ) является надежным:</span><span class="sxs-lookup"><span data-stu-id="bf986-141">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="bf986-142">Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которое открывалось после нажатия клавиши **F5**.</span><span class="sxs-lookup"><span data-stu-id="bf986-142">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="bf986-143">Перейдите к `https://localhost:3000/tab` странице и перейдите к ней.</span><span class="sxs-lookup"><span data-stu-id="bf986-143">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="bf986-144">Вернитесь в Teams.</span><span class="sxs-lookup"><span data-stu-id="bf986-144">Go back to Teams.</span></span> <span data-ttu-id="bf986-145">В диалоговом окне нажмите кнопку **Добавить** , чтобы установить приложение.</span><span class="sxs-lookup"><span data-stu-id="bf986-145">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Снимок экрана, на котором показан пример приложения _OL_QUOTE_PLACEHOLDER_Hello, World!_OL_QUOTE_PLACEHOLDER_, которое работает в Teams.":::

<span data-ttu-id="bf986-147">Поздравляем 🎉!</span><span class="sxs-lookup"><span data-stu-id="bf986-147">🎉 Congratulations!</span></span> <span data-ttu-id="bf986-148">Ваше приложение работает в Teams.</span><span class="sxs-lookup"><span data-stu-id="bf986-148">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="bf986-149">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="bf986-149">Next step</span></span>

<span data-ttu-id="bf986-150">Разверните вкладку Персональная личная и создайте другой тип приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="bf986-150">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bf986-151">Добавление на вкладку "личные"</span><span class="sxs-lookup"><span data-stu-id="bf986-151">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="bf986-152">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="bf986-152">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="bf986-153">Создание бота</span><span class="sxs-lookup"><span data-stu-id="bf986-153">Build a bot</span></span>](../build-your-first-app/build-bot.md)
