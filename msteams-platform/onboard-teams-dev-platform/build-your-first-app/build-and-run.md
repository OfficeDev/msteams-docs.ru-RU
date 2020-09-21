---
title: Создание и запуск первого приложения Teams
author: heath-hamilton
ms.author: lajanuar
description: Запустите первое приложение Microsoft Teams.
ms.date: 08/31/2020
ms.topic: quickstart
ms.openlocfilehash: 441b70480d9c177e9c6140342df8c9ea29494a29
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964754"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="fc657-103">Создание и запуск первого приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fc657-103">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="fc657-104">Вы можете быстро приступить к разработке на платформе Microsoft Teams, быстро создав и запустив базовую вкладку персональная.</span><span class="sxs-lookup"><span data-stu-id="fc657-104">You can jump right into developing on the Microsoft Teams platform by quickly building and running a basic personal tab.</span></span>

## <a name="create-your-app-project"></a><span data-ttu-id="fc657-105">Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="fc657-105">Create your app project</span></span>

<span data-ttu-id="fc657-106">Используйте набор средств Microsoft Teams в Visual Studio Code, чтобы настроить первый проект приложения.</span><span class="sxs-lookup"><span data-stu-id="fc657-106">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
:::image type="content" source="../doc-links/images/create-teams-app.png" alt-text="Создание образа приложения Teams":::
1. <span data-ttu-id="fc657-109">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="fc657-109">Enter a name for your Teams app.</span></span> <span data-ttu-id="fc657-110">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="fc657-110">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="fc657-111">На экране **добавить возможности** выберите **вкладка** **Далее**.</span><span class="sxs-lookup"><span data-stu-id="fc657-111">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../doc-links/images/choose-tab.png" alt-text="Создание представления образа приложения Teams":::
1. <span data-ttu-id="fc657-113">Установите флажок **Личная вкладка** , а затем в нижней части экрана нажмите кнопку **Готово** , чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="fc657-113">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="understand-important-app-project-components"></a><span data-ttu-id="fc657-114">Общие сведения о важных компонентах проекта приложения</span><span class="sxs-lookup"><span data-stu-id="fc657-114">Understand important app project components</span></span>

<span data-ttu-id="fc657-115">После того как набор инструментов настроит свой проект, у вас будут компоненты для создания базовой вкладки "личные" для Teams.</span><span class="sxs-lookup"><span data-stu-id="fc657-115">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="fc657-116">Каталоги и файлы проекта отображаются в области обозревателя Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="fc657-116">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../doc-links/images/app-project-files.png" alt-text="Файлы проекта приложения в Visual Studio Code.":::

<span data-ttu-id="fc657-118">Для ознакомления с некоторыми ключевыми файлами, с которыми работают разработчики приложений Teams, требуется время.</span><span class="sxs-lookup"><span data-stu-id="fc657-118">Let's take time to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="fc657-119">Манифест приложения ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="fc657-119">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="fc657-120">В каталоге манифест приложения размещается в качестве `.publish` отправной точки для любого проекта приложения.</span><span class="sxs-lookup"><span data-stu-id="fc657-120">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="fc657-121">Манифест определяет основные атрибуты приложения и указывает на необходимые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fc657-121">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="fc657-122">При установке приложения Teams анализирует манифест, чтобы узнать, как визуализировать приложение в клиенте.</span><span class="sxs-lookup"><span data-stu-id="fc657-122">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="fc657-123">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="fc657-123">App scaffolding</span></span>

<span data-ttu-id="fc657-124">Набор средств автоматически создает формирование шаблонов в `src` каталоге на основе возможностей, добавленных во время установки.</span><span class="sxs-lookup"><span data-stu-id="fc657-124">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="fc657-125">Например, при создании вкладки во время установки, `App.js` файл в `src/components` каталоге важен, так как он обрабатывает инициализацию и маршрутизацию приложения.</span><span class="sxs-lookup"><span data-stu-id="fc657-125">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="fc657-126">Он вызывает [пакет Microsoft Teams SDK](../../tabs/how-to/using-teams-client-sdk.md) для установления связи между приложением и Teams.</span><span class="sxs-lookup"><span data-stu-id="fc657-126">It calls the [Microsoft Teams SDK](../../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="fc657-127">Пакет приложения ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="fc657-127">App package (`Development.zip`)</span></span>

<span data-ttu-id="fc657-128">В `.publish` каталоге вам нужен пакет приложения, чтобы [Загрузка неопубликованных ваше приложение](../../concepts/deploy-and-publish/overview.md#upload-your-app-directly) в Teams.</span><span class="sxs-lookup"><span data-stu-id="fc657-128">Located in the `.publish` directory, you need the app package to [sideload your app](../../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="fc657-129">Пакет также используется при [публикации в каталоге приложений организации](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) или [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span><span class="sxs-lookup"><span data-stu-id="fc657-129">The package is also used when [publishing to your organization's app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="fc657-130">Ниже приведены некоторые сведения о файлах пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="fc657-130">Here are some details about the app package files:</span></span>

|<span data-ttu-id="fc657-131">Имя</span><span class="sxs-lookup"><span data-stu-id="fc657-131">Name</span></span>|<span data-ttu-id="fc657-132">Тип</span><span class="sxs-lookup"><span data-stu-id="fc657-132">Type</span></span>|<span data-ttu-id="fc657-133">Size</span><span class="sxs-lookup"><span data-stu-id="fc657-133">Size</span></span>|<span data-ttu-id="fc657-134">Расположение манифеста</span><span class="sxs-lookup"><span data-stu-id="fc657-134">Manifest location</span></span>|<span data-ttu-id="fc657-135">Имя файла набора инструментов</span><span class="sxs-lookup"><span data-stu-id="fc657-135">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="fc657-136">**Манифест приложения**</span><span class="sxs-lookup"><span data-stu-id="fc657-136">**App manifest**</span></span>|`.json`| <span data-ttu-id="fc657-137">—</span><span class="sxs-lookup"><span data-stu-id="fc657-137">—</span></span> | <span data-ttu-id="fc657-138">—</span><span class="sxs-lookup"><span data-stu-id="fc657-138">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="fc657-139">**Цветовой логотип**</span><span class="sxs-lookup"><span data-stu-id="fc657-139">**Color logo**</span></span>|`.png`|<span data-ttu-id="fc657-140">192 &times; 192 пикселя</span><span class="sxs-lookup"><span data-stu-id="fc657-140">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="fc657-141">**Эмблема структуры**</span><span class="sxs-lookup"><span data-stu-id="fc657-141">**Outline logo**</span></span>|`.png`|<span data-ttu-id="fc657-142">32 &times; 32 пикселя</span><span class="sxs-lookup"><span data-stu-id="fc657-142">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="run-your-app"></a><span data-ttu-id="fc657-143">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="fc657-143">Run your app</span></span>

<span data-ttu-id="fc657-144">В течение этого времени вы создадите и запустите свое приложение локально.</span><span class="sxs-lookup"><span data-stu-id="fc657-144">In the interest of time, you'll build and run your app locally.</span></span> <span data-ttu-id="fc657-145">Приложения Teams на уровне Рабочей группы размещаются в облаке.</span><span class="sxs-lookup"><span data-stu-id="fc657-145">Production-level Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="fc657-146">(Эти сведения также доступны в наборе инструментов `README` .)</span><span class="sxs-lookup"><span data-stu-id="fc657-146">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="fc657-147">В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .</span><span class="sxs-lookup"><span data-stu-id="fc657-147">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="fc657-148">Выполните команду `npm start` .</span><span class="sxs-lookup"><span data-stu-id="fc657-148">Run `npm start`.</span></span> <span data-ttu-id="fc657-149">По завершении **компиляции успешно выполняется.**</span><span class="sxs-lookup"><span data-stu-id="fc657-149">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="fc657-150">сообщение в терминале.</span><span class="sxs-lookup"><span data-stu-id="fc657-150">message in the terminal.</span></span>
1. <span data-ttu-id="fc657-151">Откройте браузер и перейдите по адресу, чтобы `https://localhost:3000` Просмотреть пустую веб-страницу с именем **"Вкладка Microsoft Teams"**. Не волнуйтесь, что на странице не должно отображаться никаких контента.</span><span class="sxs-lookup"><span data-stu-id="fc657-151">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../doc-links/images/local-host-tab.png" alt-text="Просмотр приложения в браузере.":::

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="fc657-153">Настройка безопасного туннеля для приложения</span><span class="sxs-lookup"><span data-stu-id="fc657-153">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="fc657-154">Ваше приложение запущено и работает на локальном веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="fc657-154">Your app is up and running on your local web server.</span></span> <span data-ttu-id="fc657-155">Для запуска приложения в Teams необходимо предоставить `localhost` доступ к нему по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fc657-155">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="fc657-156">Установите [ngrok](https://ngrok.com/download) , если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="fc657-156">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="fc657-157">При запуске этого средства создаются два глобально доступных URL-адреса, указывающие на локальный веб-сервер ( `http://localhost:3000` ).</span><span class="sxs-lookup"><span data-stu-id="fc657-157">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="fc657-158">Вам потребуется URL-адрес переадресации, начинающийся с `HTTPS` .</span><span class="sxs-lookup"><span data-stu-id="fc657-158">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="fc657-159">Откройте новый терминал и запустите его `ngrok http 3000` .</span><span class="sxs-lookup"><span data-stu-id="fc657-159">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="fc657-160">Скопируйте предоставленный URL-адрес HTTPS (см. Следующий пример).</span><span class="sxs-lookup"><span data-stu-id="fc657-160">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../doc-links/images/ngrok-running.png" alt-text="работающее изображение ngrok":::
1. <span data-ttu-id="fc657-162">В `.publish` каталоге откройте `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="fc657-162">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="fc657-163">Замените `baseUrl0` значение скопированным URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="fc657-163">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="fc657-164">(Например, замените `baseUrl0=http://localhost:3000` на `baseUrl0=https://85528b2b3ba5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="fc657-164">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="fc657-165">Теперь манифест приложения указывает на место размещения приложения.</span><span class="sxs-lookup"><span data-stu-id="fc657-165">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="fc657-166">Загрузка неопубликованных ваше приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="fc657-166">Sideload your app in Teams</span></span>

<span data-ttu-id="fc657-167">Когда ваше приложение работает и доступно через HTTPS, вы можете отправить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="fc657-167">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="fc657-168">Прежде чем приступить к работе с неопубликованным приложением, проверьте наличие проблем с помощью [средства проверки набора](../../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span><span class="sxs-lookup"><span data-stu-id="fc657-168">Before sideloading your app, check for issues using the [toolkit's validation feature](../../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="fc657-169">Чтобы успешно Загрузка неопубликованных приложение, необходимо исправить ошибки.</span><span class="sxs-lookup"><span data-stu-id="fc657-169">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="fc657-170">Выполните вход в клиент Teams с учетной записью, позволяющей выполнять загрузку неопубликованных приложений.</span><span class="sxs-lookup"><span data-stu-id="fc657-170">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="fc657-171">(Если вы не знаете этого, Узнайте о том, как получить [учетную запись разработки Teams](../build-your-first-app/building-real-world-app.md#set-up-your-development-account).)</span><span class="sxs-lookup"><span data-stu-id="fc657-171">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/building-real-world-app.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="fc657-172">Выберите **приложения**, а затем нажмите кнопку **Отправить пользовательское приложение**.</span><span class="sxs-lookup"><span data-stu-id="fc657-172">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="fc657-173">Перейдите в папку проекта приложения `.publish` и выберите `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="fc657-173">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="fc657-174">Модальные дисплеи установки.</span><span class="sxs-lookup"><span data-stu-id="fc657-174">An install modal displays.</span></span>
:::image type="content" source="../doc-links/images/add-teams-app.png" alt-text="Добавление приложения Teams":::
1. <span data-ttu-id="fc657-176">Нажмите кнопку **Добавить** , чтобы установить приложение.</span><span class="sxs-lookup"><span data-stu-id="fc657-176">Select **Add** to install your app.</span></span>
:::image type="content" source="../doc-links/images/tab-running.png" alt-text="Снимок экрана, на котором показан пример Hello, World! приложение в Teams.":::

<span data-ttu-id="fc657-178">Поздравляем 🎉!</span><span class="sxs-lookup"><span data-stu-id="fc657-178">🎉 Congratulations!</span></span> <span data-ttu-id="fc657-179">Ваше приложение работает в Teams.</span><span class="sxs-lookup"><span data-stu-id="fc657-179">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="fc657-180">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="fc657-180">Next step</span></span>

<span data-ttu-id="fc657-181">Разверните вкладку Персональная личная и создайте другой тип приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="fc657-181">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc657-182">Добавление на вкладку "личные"</span><span class="sxs-lookup"><span data-stu-id="fc657-182">Add to your personal tab</span></span>](../build-your-first-app/add-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="fc657-183">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="fc657-183">Build a channel tab</span></span>](../build-your-first-app/add-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="fc657-184">Создание ленты</span><span class="sxs-lookup"><span data-stu-id="fc657-184">Build a bot</span></span>](../build-your-first-app/add-bot.md)
