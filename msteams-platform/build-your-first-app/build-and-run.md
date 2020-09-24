---
title: Создание и запуск "Hello, World!" Приложение Teams
author: heath-hamilton
description: Создание и запуск первого приложения Microsoft Teams, вкладки личных параметров, в которой отображается слово "Hello, World!"
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 244a899670f71b9446c8c3d3e404c9fd7c7b510c
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237834"
---
# <a name="build-a-hello-world-teams-app"></a><span data-ttu-id="41d23-104">Создание приложения "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="41d23-104">Build a "Hello, World!"</span></span> <span data-ttu-id="41d23-105">Приложение Teams</span><span class="sxs-lookup"><span data-stu-id="41d23-105">Teams app</span></span>

<span data-ttu-id="41d23-106">Вы можете перейти непосредственно к разработке платформы Microsoft Teams, создав личную вкладку со свойством "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="41d23-106">You can jump right into Microsoft Teams platform development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="41d23-107">1. Создайте проект приложения.</span><span class="sxs-lookup"><span data-stu-id="41d23-107">1. Create your app project</span></span>

<span data-ttu-id="41d23-108">Используйте набор средств Microsoft Teams в Visual Studio Code, чтобы настроить первый проект приложения.</span><span class="sxs-lookup"><span data-stu-id="41d23-108">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="Снимок экрана, на котором показано, как создать новое приложение с набором средств Visual Studio Code Teams Toolkit.":::
1. <span data-ttu-id="41d23-111">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="41d23-111">Enter a name for your Teams app.</span></span> <span data-ttu-id="41d23-112">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="41d23-112">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="41d23-113">На экране **добавить возможности** выберите **вкладка** **Далее**.</span><span class="sxs-lookup"><span data-stu-id="41d23-113">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Снимок экрана, на котором показано, как настроить проект приложения с помощью набора инструментов Visual Studio Code Teams.":::
1. <span data-ttu-id="41d23-115">Установите флажок **Личная вкладка** , а затем в нижней части экрана нажмите кнопку **Готово** , чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="41d23-115">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="41d23-116">2. Изучите важные компоненты проекта приложения</span><span class="sxs-lookup"><span data-stu-id="41d23-116">2. Understand important app project components</span></span>

<span data-ttu-id="41d23-117">После того как набор инструментов настроит свой проект, у вас будут компоненты для создания базовой вкладки "личные" для Teams.</span><span class="sxs-lookup"><span data-stu-id="41d23-117">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="41d23-118">Каталоги и файлы проекта отображаются в области обозревателя Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="41d23-118">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Снимок экрана, на котором показаны файлы проекта приложения для вкладки "личные" в Visual Studio Code.":::

<span data-ttu-id="41d23-120">Давайте рассмотрим некоторые ключевые файлы, с которыми работают разработчики приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="41d23-120">Let's take a moment to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="41d23-121">Манифест приложения ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="41d23-121">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="41d23-122">В каталоге манифест приложения размещается в качестве `.publish` отправной точки для любого проекта приложения.</span><span class="sxs-lookup"><span data-stu-id="41d23-122">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="41d23-123">Манифест определяет основные атрибуты приложения и указывает на необходимые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="41d23-123">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="41d23-124">При установке приложения Teams анализирует манифест, чтобы узнать, как визуализировать приложение в клиенте.</span><span class="sxs-lookup"><span data-stu-id="41d23-124">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="41d23-125">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="41d23-125">App scaffolding</span></span>

<span data-ttu-id="41d23-126">Набор средств автоматически создает формирование шаблонов в `src` каталоге на основе возможностей, добавленных во время установки.</span><span class="sxs-lookup"><span data-stu-id="41d23-126">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="41d23-127">Например, при создании вкладки во время установки, `App.js` файл в `src/components` каталоге важен, так как он обрабатывает инициализацию и маршрутизацию приложения.</span><span class="sxs-lookup"><span data-stu-id="41d23-127">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="41d23-128">Он вызывает [пакет Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) для установления связи между приложением и Teams.</span><span class="sxs-lookup"><span data-stu-id="41d23-128">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="41d23-129">Пакет приложения ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="41d23-129">App package (`Development.zip`)</span></span>

<span data-ttu-id="41d23-130">В `.publish` каталоге вам нужен пакет приложения, чтобы [Загрузка неопубликованных ваше приложение](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) в Teams.</span><span class="sxs-lookup"><span data-stu-id="41d23-130">Located in the `.publish` directory, you need the app package to [sideload your app](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="41d23-131">Пакет также используется при [публикации в каталоге приложений организации](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) или [AppSource](../concepts/deploy-and-publish/appsource/publish.md).</span><span class="sxs-lookup"><span data-stu-id="41d23-131">The package is also used when [publishing to your organization's app catalog](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="41d23-132">Ниже приведены некоторые сведения о файлах пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="41d23-132">Here are some details about the app package files:</span></span>

|<span data-ttu-id="41d23-133">Имя</span><span class="sxs-lookup"><span data-stu-id="41d23-133">Name</span></span>|<span data-ttu-id="41d23-134">Тип</span><span class="sxs-lookup"><span data-stu-id="41d23-134">Type</span></span>|<span data-ttu-id="41d23-135">Size</span><span class="sxs-lookup"><span data-stu-id="41d23-135">Size</span></span>|<span data-ttu-id="41d23-136">Расположение манифеста</span><span class="sxs-lookup"><span data-stu-id="41d23-136">Manifest location</span></span>|<span data-ttu-id="41d23-137">Имя файла набора инструментов</span><span class="sxs-lookup"><span data-stu-id="41d23-137">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="41d23-138">**Манифест приложения**</span><span class="sxs-lookup"><span data-stu-id="41d23-138">**App manifest**</span></span>|`.json`| <span data-ttu-id="41d23-139">—</span><span class="sxs-lookup"><span data-stu-id="41d23-139">—</span></span> | <span data-ttu-id="41d23-140">—</span><span class="sxs-lookup"><span data-stu-id="41d23-140">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="41d23-141">**Цветовой логотип**</span><span class="sxs-lookup"><span data-stu-id="41d23-141">**Color logo**</span></span>|`.png`|<span data-ttu-id="41d23-142">192 &times; 192 пикселя</span><span class="sxs-lookup"><span data-stu-id="41d23-142">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="41d23-143">**Эмблема структуры**</span><span class="sxs-lookup"><span data-stu-id="41d23-143">**Outline logo**</span></span>|`.png`|<span data-ttu-id="41d23-144">32 &times; 32 пикселя</span><span class="sxs-lookup"><span data-stu-id="41d23-144">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="3-run-your-app"></a><span data-ttu-id="41d23-145">3. Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="41d23-145">3. Run your app</span></span>

<span data-ttu-id="41d23-146">В течение этого времени вы создадите и запустите свое приложение локально.</span><span class="sxs-lookup"><span data-stu-id="41d23-146">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="41d23-147">(Эти сведения также доступны в наборе инструментов `README` .)</span><span class="sxs-lookup"><span data-stu-id="41d23-147">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="41d23-148">В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .</span><span class="sxs-lookup"><span data-stu-id="41d23-148">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="41d23-149">Выполните команду `npm start` .</span><span class="sxs-lookup"><span data-stu-id="41d23-149">Run `npm start`.</span></span> <span data-ttu-id="41d23-150">По завершении **компиляции успешно выполняется.**</span><span class="sxs-lookup"><span data-stu-id="41d23-150">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="41d23-151">сообщение в терминале.</span><span class="sxs-lookup"><span data-stu-id="41d23-151">message in the terminal.</span></span>
1. <span data-ttu-id="41d23-152">Откройте браузер и перейдите по адресу, чтобы `https://localhost:3000` Просмотреть пустую веб-страницу с именем **"Вкладка Microsoft Teams"**. Не волнуйтесь, что на странице не должно отображаться никаких контента.</span><span class="sxs-lookup"><span data-stu-id="41d23-152">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="Снимок экрана, на котором показано, как просмотреть работающее приложение в браузере.":::

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="41d23-154">4. Настройка безопасного туннеля для приложения</span><span class="sxs-lookup"><span data-stu-id="41d23-154">4. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="41d23-155">Ваше приложение запущено и работает на локальном веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="41d23-155">Your app is up and running on your local web server.</span></span> <span data-ttu-id="41d23-156">Для запуска приложения в Teams необходимо предоставить `localhost` доступ к нему по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="41d23-156">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="41d23-157">Установите [ngrok](https://ngrok.com/download) , если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="41d23-157">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="41d23-158">При запуске этого средства создаются два глобально доступных URL-адреса, указывающие на локальный веб-сервер ( `http://localhost:3000` ).</span><span class="sxs-lookup"><span data-stu-id="41d23-158">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="41d23-159">Вам потребуется URL-адрес переадресации, начинающийся с `HTTPS` .</span><span class="sxs-lookup"><span data-stu-id="41d23-159">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="41d23-160">Откройте новый терминал и запустите его `ngrok http 3000` .</span><span class="sxs-lookup"><span data-stu-id="41d23-160">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="41d23-161">Скопируйте предоставленный URL-адрес HTTPS (см. Следующий пример).</span><span class="sxs-lookup"><span data-stu-id="41d23-161">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="Снимок экрана с терминалом, на котором запущен ngrok.":::
1. <span data-ttu-id="41d23-163">В `.publish` каталоге откройте `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="41d23-163">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="41d23-164">Замените `baseUrl0` значение скопированным URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="41d23-164">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="41d23-165">(Например, замените `baseUrl0=http://localhost:3000` на `baseUrl0=https://85528b2b3ba5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="41d23-165">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="41d23-166">Теперь манифест приложения указывает на место размещения приложения.</span><span class="sxs-lookup"><span data-stu-id="41d23-166">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="5-sideload-your-app-in-teams"></a><span data-ttu-id="41d23-167">5. Загрузка неопубликованных ваше приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="41d23-167">5. Sideload your app in Teams</span></span>

<span data-ttu-id="41d23-168">Когда ваше приложение работает и доступно через HTTPS, вы можете отправить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="41d23-168">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="41d23-169">Прежде чем приступить к работе с неопубликованным приложением, проверьте наличие проблем с помощью [средства проверки набора](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span><span class="sxs-lookup"><span data-stu-id="41d23-169">Before sideloading your app, check for issues using the [toolkit's validation feature](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="41d23-170">Чтобы успешно Загрузка неопубликованных приложение, необходимо исправить ошибки.</span><span class="sxs-lookup"><span data-stu-id="41d23-170">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="41d23-171">Выполните вход в клиент Teams с учетной записью, позволяющей выполнять загрузку неопубликованных приложений.</span><span class="sxs-lookup"><span data-stu-id="41d23-171">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="41d23-172">(Если вы не знаете этого, Узнайте о том, как получить [учетную запись разработки Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span><span class="sxs-lookup"><span data-stu-id="41d23-172">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="41d23-173">Выберите **приложения**, а затем нажмите кнопку **Отправить пользовательское приложение**.</span><span class="sxs-lookup"><span data-stu-id="41d23-173">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="41d23-174">Перейдите в папку проекта приложения `.publish` и выберите `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="41d23-174">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="41d23-175">Модальные дисплеи установки.</span><span class="sxs-lookup"><span data-stu-id="41d23-175">An installation modal displays.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="Снимок экрана, на котором показан пример модальной установки приложения Teams.":::
1. <span data-ttu-id="41d23-177">Нажмите кнопку **Добавить** , чтобы установить приложение.</span><span class="sxs-lookup"><span data-stu-id="41d23-177">Select **Add** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Снимок экрана, на котором показан пример приложения "Hello, World!", которое работает в Teams.":::

<span data-ttu-id="41d23-179">Поздравляем 🎉!</span><span class="sxs-lookup"><span data-stu-id="41d23-179">🎉 Congratulations!</span></span> <span data-ttu-id="41d23-180">Ваше приложение работает в Teams.</span><span class="sxs-lookup"><span data-stu-id="41d23-180">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="41d23-181">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="41d23-181">Next step</span></span>

<span data-ttu-id="41d23-182">Разверните вкладку Персональная личная и создайте другой тип приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="41d23-182">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="41d23-183">Добавление на вкладку "личные"</span><span class="sxs-lookup"><span data-stu-id="41d23-183">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="41d23-184">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="41d23-184">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="41d23-185">Создание бота</span><span class="sxs-lookup"><span data-stu-id="41d23-185">Build a bot</span></span>](../build-your-first-app/build-bot.md)
