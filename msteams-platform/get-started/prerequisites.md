---
title: Начало работы - Необходимые условия
author: adrianhall
description: Узнайте, как начать работу с разработкой Microsoft Teams и настроить среду.
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 73d99f2bbbc69bf13242110a56e13e662655283c
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646773"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="ad9f4-103">Необходимые условия: начало разработки Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="ad9f4-103">Prerequisites: Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="ad9f4-104">Перед созданием первого Teams необходимо установить несколько инструментов и настроить среду разработки.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-104">Before your create your first Teams app, you must install a few tools and set up your development environment.</span></span>

## <a name="install-required-tools"></a><span data-ttu-id="ad9f4-105">Установка необходимых средств</span><span class="sxs-lookup"><span data-stu-id="ad9f4-105">Install required tools</span></span>

<span data-ttu-id="ad9f4-106">Некоторые из необходимых инструментов зависят от того, как вы предпочитаете создавать Teams приложение:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-106">Some of the tools you need depend on how you you prefer to build your Teams app:</span></span>

- <span data-ttu-id="ad9f4-107">[Node.js](https://nodejs.org/en/download/) (используйте последний выпуск V14 LTS)</span><span class="sxs-lookup"><span data-stu-id="ad9f4-107">[Node.js](https://nodejs.org/en/download/) (use the latest v14 LTS release)</span></span> 
- <span data-ttu-id="ad9f4-108">Браузер с средствами разработчика , такими как [Microsoft Edge](https://www.microsoft.com/edge) (рекомендуется) или [Google Chrome](https://www.google.com/chrome/)</span><span class="sxs-lookup"><span data-stu-id="ad9f4-108">A browser with developer tools - such as [Microsoft Edge](https://www.microsoft.com/edge) (recommended) or [Google Chrome](https://www.google.com/chrome/)</span></span>
- <span data-ttu-id="ad9f4-109">Если вы разрабатываете с Помощью JavaScript, TypeScript или SharePoint Framework (SPFx), установите Visual Studio Code [версии](https://code.visualstudio.com/download)1.55 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-109">If you're developing with JavaScript, TypeScript, or the SharePoint Framework (SPFx), install [Visual Studio Code](https://code.visualstudio.com/download), version 1.55 or later.</span></span>  
- <span data-ttu-id="ad9f4-110">Если вы разрабатываете с помощью .NET, установите Visual Studio [2019](https://visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="ad9f4-110">If you're developing with .NET, install [Visual Studio 2019](https://visualstudio.com/download).</span></span>  <span data-ttu-id="ad9f4-111">Убедитесь, что ASP.NET **и веб-разработки** или **межплатформеной** рабочей нагрузки .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-111">Ensure you install the **ASP.NET and web development** or **.NET Core cross-platform development** workload.</span></span>

> [!WARNING]
> <span data-ttu-id="ad9f4-112">Известны проблемы с пакетом `npm@7` с node v15 и более поздним пакетом.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-112">There are known issues with `npm@7`, packaged with Node v15 and later.</span></span> <span data-ttu-id="ad9f4-113">Если у вас возникли проблемы с запуском, убедитесь, что `npm install` вы используете узел v14 (LTS)</span><span class="sxs-lookup"><span data-stu-id="ad9f4-113">If you have problems running `npm install`, ensure you're using Node v14 (LTS)</span></span>

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="ad9f4-114">Установка Teams набор средств</span><span class="sxs-lookup"><span data-stu-id="ad9f4-114">Install the Teams Toolkit</span></span>

<span data-ttu-id="ad9f4-115">Этот Teams набор средств упрощает процесс разработки с помощью средств для обеспечения и развертывания облачных ресурсов для приложения, публикации в Teams магазине и других.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-115">The Teams Toolkit helps simplify the development process with tools to provision and deploy cloud resources for your app, publish to the Teams store, and more.</span></span> <span data-ttu-id="ad9f4-116">Инструментарий можно использовать с помощью Visual Studio Code, Visual Studio или CLI `teamsfx` (называется).</span><span class="sxs-lookup"><span data-stu-id="ad9f4-116">You can use the toolkit with Visual Studio Code, Visual Studio, or as a CLI (called `teamsfx`).</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="ad9f4-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ad9f4-117">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="ad9f4-118">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-118">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="ad9f4-119">Выберите представление Расширения **(Ctrl+Shift+X**  /  **⌘⇧-X** или **> расширения).**</span><span class="sxs-lookup"><span data-stu-id="ad9f4-119">Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="ad9f4-120">В поле поиска введите _Teams набор средств_.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-120">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="ad9f4-121">Выберите на зеленой кнопке установки рядом с Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-121">Select on the green install button next to the Teams Toolkit.</span></span>

<span data-ttu-id="ad9f4-122">Вы также можете найти Teams набор средств на Visual Studio Code [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span><span class="sxs-lookup"><span data-stu-id="ad9f4-122">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="ad9f4-123">Следующие средства будут установлены расширением Visual Studio Code при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-123">The following tools will be installed by the Visual Studio Code extension when they are needed.</span></span>  <span data-ttu-id="ad9f4-124">Если уже установлено, вместо нее будет использоваться установленная версия.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-124">If already installed, the installed version will be used instead.</span></span>  <span data-ttu-id="ad9f4-125">Если используется Linux (в том числе WSL), необходимо установить эти средства перед использованием:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-125">If using Linux (including WSL), you must install these tools before use:</span></span>

- [<span data-ttu-id="ad9f4-126">Основные средства Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ad9f4-126">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="ad9f4-127">Основные средства Azure Functions используются для локального запуска отлаженных компонентов, включая помощников проверки подлинности, необходимых при запуске служб в Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-127">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span>  <span data-ttu-id="ad9f4-128">Он устанавливается в каталоге проекта (с помощью `devDependencies` npm).</span><span class="sxs-lookup"><span data-stu-id="ad9f4-128">It is installed within the project directory (using the npm `devDependencies`).</span></span>

- [<span data-ttu-id="ad9f4-129">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="ad9f4-129">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="ad9f4-130">SDK .NET используется для установки настраиваемых привязки для локального отладки и развертывания приложений Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-130">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span>  <span data-ttu-id="ad9f4-131">Если вы не установили SDK .NET 3.1 (или более поздней версии) глобально, портативная версия будет установлена.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-131">If you have not installed the .NET 3.1 (or later) SDK globally, the portable version will be installed.</span></span>

- [<span data-ttu-id="ad9f4-132">ngrok</span><span class="sxs-lookup"><span data-stu-id="ad9f4-132">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="ad9f4-133">Некоторые Teams приложения (беседные боты, расширения обмена сообщениями и входящие веб-оки) требуют входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-133">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span>  <span data-ttu-id="ad9f4-134">Необходимо подвергать систему разработки Teams через туннель.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-134">You need to expose your development system to Teams through a tunnel.</span></span>  <span data-ttu-id="ad9f4-135">Туннель не требуется для приложений, которые включают только вкладки.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-135">A tunnel is not required for apps that only include tabs.</span></span>  <span data-ttu-id="ad9f4-136">Этот пакет устанавливается в каталоге проекта (с помощью `devDependencies` npm).</span><span class="sxs-lookup"><span data-stu-id="ad9f4-136">This package is installed within the project directory (using npm `devDependencies`).</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="ad9f4-137">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="ad9f4-137">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="ad9f4-138">Вы можете использовать Visual Studio 2019 для разработки Teams с помощью Blazor Server в .NET.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-138">You can use Visual Studio 2019 to develop Teams apps with Blazor Server in .NET.</span></span>  <span data-ttu-id="ad9f4-139">Если вы не собираетесь разрабатывать Teams приложения в .NET, установите Visual Studio Code версию Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-139">If you're not intending to develop Teams apps in .NET, install the Visual Studio Code version of Teams Toolkit.</span></span>

<span data-ttu-id="ad9f4-140">Чтобы установить расширение Teams набор средств:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-140">To install the Teams Toolkit extension:</span></span>

1. <span data-ttu-id="ad9f4-141">Open Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-141">Open Visual Studio 2019.</span></span>
1. <span data-ttu-id="ad9f4-142">Выберите **Расширения Управление**  >  **расширениями**.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-142">Select **Extensions** > **Manage Extensions**.</span></span>
1. <span data-ttu-id="ad9f4-143">В поле поиска введите _Teams набор средств_.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-143">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="ad9f4-144">Выберите расширение Teams набор средств и выберите **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-144">Select the Teams Toolkit extension and select **Download**.</span></span>

<span data-ttu-id="ad9f4-145">Расширение будет загружено.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-145">The extension will be downloaded.</span></span>  <span data-ttu-id="ad9f4-146">Закрыть Visual Studio 2019 г. для установки расширения.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-146">Close Visual Studio 2019 to install the extension.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="ad9f4-147">Командная строка</span><span class="sxs-lookup"><span data-stu-id="ad9f4-147">Command line</span></span>](#tab/cli)

<span data-ttu-id="ad9f4-148">Чтобы установить CLI TeamsFx, используйте диспетчер `npm` пакетов:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-148">To install the TeamsFx CLI, use the `npm` package manager:</span></span>

``` bash
npm install -g @microsoft/teamsfx-cli
```

<span data-ttu-id="ad9f4-149">В зависимости от конфигурации может потребоваться использовать для `sudo` установки CLI:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-149">Depending on your configuration, you may need to use `sudo` to install the CLI:</span></span>

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

<span data-ttu-id="ad9f4-150">Это чаще встречается в системах Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-150">This is more common on Linux and macOS systems.</span></span>

<span data-ttu-id="ad9f4-151">Убедитесь, что вы добавляете глобальный кэш npm в path.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-151">Ensure you add the npm global cache to your PATH.</span></span>  <span data-ttu-id="ad9f4-152">Обычно это делается как часть Node.js установки.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-152">This is normally done as part of the Node.js installer.</span></span>  

<span data-ttu-id="ad9f4-153">CLI можно использовать с `teamsfx` командой.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-153">You can use the CLI with the `teamsfx` command.</span></span>  <span data-ttu-id="ad9f4-154">Убедитесь, что команда работает с помощью `teamsfx -h` запуска .</span><span class="sxs-lookup"><span data-stu-id="ad9f4-154">Verify that the command is working by running `teamsfx -h`.</span></span>

> [!CAUTION]
> <span data-ttu-id="ad9f4-155">Прежде чем запустить TeamsFx в терминалах PowerShell, необходимо включить политику выполнения powerShell с "удаленной подписью".</span><span class="sxs-lookup"><span data-stu-id="ad9f4-155">Before you can run TeamsFx in PowerShell terminals, you need to enable the "remote signed" execution policy for PowerShell.</span></span>  <span data-ttu-id="ad9f4-156">Дополнительные сведения можно найти в [документации PowerShell.](/powershell/module/microsoft.powershell.core/about/about_signing)</span><span class="sxs-lookup"><span data-stu-id="ad9f4-156">For more information, refer to the [PowerShell documentation](/powershell/module/microsoft.powershell.core/about/about_signing).</span></span>

---

## <a name="install-optional-tools"></a><span data-ttu-id="ad9f4-157">Установка необязательных средств</span><span class="sxs-lookup"><span data-stu-id="ad9f4-157">Install optional tools</span></span>

<span data-ttu-id="ad9f4-158">Установите средства браузера для разработки приложений.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-158">Install browser tools for app development.</span></span> <span data-ttu-id="ad9f4-159">Например, если приложение написано с помощью React, вы можете использовать React средства разработчика:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-159">For instance, if your app is written with React, you can use React Developer Tools:</span></span>

- [<span data-ttu-id="ad9f4-160">React Средства разработчика для Chrome</span><span class="sxs-lookup"><span data-stu-id="ad9f4-160">React Developer Tools for Chrome</span></span>](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

<span data-ttu-id="ad9f4-161">Если вы хотите получить доступ к данным, хранимым в Azure, или развернуть облачную Teams приложения в Azure, установите эти средства:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-161">If you want to access data stored in Azure or deploy a cloud-based backend for your Teams app in Azure, install these tools:</span></span>

- [<span data-ttu-id="ad9f4-162">Azure Tools для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ad9f4-162">Azure Tools for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [<span data-ttu-id="ad9f4-163">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ad9f4-163">Azure CLI</span></span>](/cli/azure/install-azure-cli)

<span data-ttu-id="ad9f4-164">Если вы работаете с данными microsoft Graph, вы должны узнать о и закладки Microsoft Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-164">If you work with Microsoft Graph data, you should learn about and bookmark the Microsoft Graph Explorer.</span></span> <span data-ttu-id="ad9f4-165">Этот инструмент на основе браузера позволяет запрашивать microsoft Graph за пределами приложения.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-165">This browser-based tool allows you to query Microsoft Graph outside of an app.</span></span>

- [<span data-ttu-id="ad9f4-166">Microsoft Graph Explorer</span><span class="sxs-lookup"><span data-stu-id="ad9f4-166">Microsoft Graph Explorer</span></span>](https://developer.microsoft.com/graph/graph-explorer)

<span data-ttu-id="ad9f4-167">С помощью портала разработчиков для Teams можно настроить, управлять и распространять приложение Teams (в том числе на ваш сайт или Teams магазин).</span><span class="sxs-lookup"><span data-stu-id="ad9f4-167">With the Developer Portal for Teams, you can configure, manage, and distribute your Teams app (including to your org or the Teams store).</span></span>

- [<span data-ttu-id="ad9f4-168">Портал разработчика для Teams</span><span class="sxs-lookup"><span data-stu-id="ad9f4-168">Developer Portal for Teams</span></span>](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a><span data-ttu-id="ad9f4-169">Включить загрузку побок</span><span class="sxs-lookup"><span data-stu-id="ad9f4-169">Enable sideloading</span></span>

<span data-ttu-id="ad9f4-170">Во время разработки необходимо загрузить приложение в течение Teams, не распространяя его.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-170">During development, you will need to load your app within Teams without distributing it.</span></span>  <span data-ttu-id="ad9f4-171">Это называется "боковой загрузкой".</span><span class="sxs-lookup"><span data-stu-id="ad9f4-171">This is known as "sideloading".</span></span>

1. <span data-ttu-id="ad9f4-172">Если у вас есть Teams учетная запись, проверьте, можно ли перегружать приложения в Teams:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-172">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>

    1. <span data-ttu-id="ad9f4-173">В клиенте Teams выберите **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-173">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="ad9f4-174">Найди вариант Upload **настраиваемого приложения.**</span><span class="sxs-lookup"><span data-stu-id="ad9f4-174">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, Teams вы можете загрузить пользовательское приложение.":::

> [!NOTE]
> <span data-ttu-id="ad9f4-176">Если вы все еще не можете разгрузить приложения, поговорите с Teams администратором.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-176">If you still can't sideload apps, talk to your Teams administrator.</span></span> <span data-ttu-id="ad9f4-177">См. в Teams настраиваемые приложения и [включите настраиваемую загрузку](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) приложений для подробных сведений.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-177">See [enable custom Teams apps and turn on custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for details.</span></span>

## <a name="get-a-free-teams-developer-tenant-optional"></a><span data-ttu-id="ad9f4-178">Получите бесплатный клиент Teams разработчика (необязательный)</span><span class="sxs-lookup"><span data-stu-id="ad9f4-178">Get a free Teams developer tenant (optional)</span></span>

<span data-ttu-id="ad9f4-179">Если вы не видите параметр sideload или у вас нет учетной записи Teams, вы можете получить бесплатную учетную запись Teams разработчика, присоединившись к программе разработчика M365.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-179">If you cannot see the sideload option, or you don't have a Teams account, you can get a free Teams developer account by joining the M365 developer program.</span></span>  <span data-ttu-id="ad9f4-180">Процесс регистрации занимает примерно две минуты.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-180">The registration process takes approximately two minutes.</span></span>

1. <span data-ttu-id="ad9f4-181">Перейдите в [Microsoft 365 разработчика](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="ad9f4-181">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="ad9f4-182">Выберите **Join Now** и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-182">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="ad9f4-183">Когда вы доберетсяе до экрана приветствия, выберите **настройка подписки E5**.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-183">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="ad9f4-184">Настройка учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-184">Set up your administrator account.</span></span> <span data-ttu-id="ad9f4-185">Как только вы закончите, вы должны увидеть экран, как это.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-185">Once you finish, you should see a screen like this.</span></span>

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации на программу Microsoft 365 разработчика.":::

1. <span data-ttu-id="ad9f4-187">Войдите Teams с помощью только что настроенной учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-187">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="ad9f4-188">Проверьте, есть ли у **вас Upload настраиваемый параметр** приложения.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-188">Verify if you now have the **Upload a custom app** option.</span></span>

## <a name="get-a-free-azure-account"></a><span data-ttu-id="ad9f4-189">Получить бесплатную учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="ad9f4-189">Get a free Azure account</span></span>

<span data-ttu-id="ad9f4-190">Если вы хотите провести свое приложение или получить доступ к ресурсам в Azure, вам потребуется подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-190">If you wish to host your app or access resources within Azure, you will need an Azure subscription.</span></span>  <span data-ttu-id="ad9f4-191">Перед [началом работы можно](https://azure.microsoft.com/free/) создать бесплатную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-191">You can [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a><span data-ttu-id="ad9f4-192">Вход в учетные записи Microsoft 365 Azure</span><span class="sxs-lookup"><span data-stu-id="ad9f4-192">Sign in to your Microsoft 365 and Azure accounts</span></span>

<span data-ttu-id="ad9f4-193">Вам потребуется доступ к двум учетным записям:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-193">You will need access to two accounts:</span></span>

- <span data-ttu-id="ad9f4-194">Учетные данные Microsoft 365 учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-194">Your Microsoft 365 account credentials.</span></span> <span data-ttu-id="ad9f4-195">Это учетная запись, которую вы используете для регистрации Teams.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-195">This is the account that you use to sign in to Teams.</span></span> <span data-ttu-id="ad9f4-196">Если вы используете клиента Microsoft 365 разработчика, это учетная запись администратора, созданная при регистрации программы.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-196">If you're using an Microsoft 365 developer program tenant, this is the admin account you set up when you registered for the program.</span></span>
- - <span data-ttu-id="ad9f4-197">Учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-197">Your Azure credentials.</span></span> <span data-ttu-id="ad9f4-198">Это учетная запись, используемая для доступа к порталу Azure и для предоставления новых облачных ресурсов для поддержки приложения.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-198">This is the account that you use to access the Azure Portal and for provisioning new cloud resources to support your app.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="ad9f4-199">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ad9f4-199">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="ad9f4-200">Откройте Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ad9f4-200">Open Visual Studio Code</span></span>
1. <span data-ttu-id="ad9f4-201">Выберите значок Teams на боковой панели:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-201">Select the Teams icon in the sidebar:</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на Visual Studio Code панели.":::

1. <span data-ttu-id="ad9f4-203">Выберите **вход в M365**.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-203">Select **Sign in to M365**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Расположение раздела Учетные записи, используемого для регистрации.":::

1. <span data-ttu-id="ad9f4-205">Процесс регистрации начнется с обычного веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-205">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="ad9f4-206">Завершите процесс регистрации для учетной записи M365.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-206">Complete the sign-in process for your M365 account.</span></span>  <span data-ttu-id="ad9f4-207">Вам будет предложено закрыть браузер и вернуться к Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-207">You will be prompted when you can close the browser and return to Visual Studio Code.</span></span>
1. <span data-ttu-id="ad9f4-208">Возвращайся к Teams набор средств в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-208">Return to the Teams Toolkit within Visual Studio Code.</span></span>
1. <span data-ttu-id="ad9f4-209">Выберите **вход в Azure.**</span><span class="sxs-lookup"><span data-stu-id="ad9f4-209">Select **Sign in to Azure**.</span></span>

    > [!TIP]
    > <span data-ttu-id="ad9f4-210">Если у вас установлено расширение учетной записи Azure и используется та же учетная запись, вы можете пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-210">If you have the Azure Account extension installed and are using the same account, you can skip this step.</span></span>  <span data-ttu-id="ad9f4-211">Вы автоматически будете использовать ту же учетную запись, что и в других расширениях.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-211">You will automatically use the same account as you are using in other extensions.</span></span>

1. <span data-ttu-id="ad9f4-212">Процесс регистрации начнется с обычного веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-212">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="ad9f4-213">Завершите процесс регистрации для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-213">Complete the sign-in process for your Azure account.</span></span>  <span data-ttu-id="ad9f4-214">Вам будет предложено закрыть браузер и вернуться к Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-214">You will be prompted when you can close the browser and return to Visual Studio Code.</span></span>

<span data-ttu-id="ad9f4-215">По завершению раздел **ACCOUNTS** боковой панели будет показывать две учетные записи отдельно, а также количество доступных для вас подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-215">When complete, the **ACCOUNTS** section of the sidebar will show the two accounts separately, together with the number of usable Azure subscriptions available to you.</span></span>  <span data-ttu-id="ad9f4-216">Убедитесь, что у вас есть по крайней мере одна доступная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-216">Ensure you have at least one usable Azure subscription available.</span></span>  <span data-ttu-id="ad9f4-217">Если нет, выпишитесь и используйте другую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-217">If not, sign out and use a different account.</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="ad9f4-218">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="ad9f4-218">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="ad9f4-219">Visual Studio 2019 г. вы сможете войти в каждую службу по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-219">Visual Studio 2019 will prompt you to log in to each service as it is needed.</span></span>  <span data-ttu-id="ad9f4-220">Вам не нужно заранее войти в учетные записи M365 и Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-220">You do not need to sign in to your M365 and Azure accounts in advance.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="ad9f4-221">Командная строка</span><span class="sxs-lookup"><span data-stu-id="ad9f4-221">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="ad9f4-222">Во входе Microsoft 365 с CLI TeamsFx:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-222">Sign in to Microsoft 365 with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login m365
    ```

    <span data-ttu-id="ad9f4-223">Процесс регистрации начнется с обычного веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-223">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="ad9f4-224">Завершите процесс регистрации для учетной записи M365.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-224">Complete the sign-in process for your M365 account.</span></span>  <span data-ttu-id="ad9f4-225">Вам будет предложено закрыть браузер.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-225">You will be prompted when you can close the browser.</span></span>

2. <span data-ttu-id="ad9f4-226">Во входе в Azure с CLI TeamsFx:</span><span class="sxs-lookup"><span data-stu-id="ad9f4-226">Sign in to Azure with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login azure
    ```

    <span data-ttu-id="ad9f4-227">Процесс регистрации начнется с обычного веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-227">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="ad9f4-228">Завершите процесс регистрации для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-228">Complete the sign-in process for your Azure account.</span></span>  <span data-ttu-id="ad9f4-229">Вам будет предложено закрыть браузер.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-229">You will be prompted when you can close the browser.</span></span>

<span data-ttu-id="ad9f4-230">Логины учетных записей делятся между Visual Studio Code и CLI TeamsFx.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-230">The account logins are shared between Visual Studio Code and the TeamsFx CLI.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="ad9f4-231">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad9f4-231">Next steps</span></span>

<span data-ttu-id="ad9f4-232">После настройки среды разработки можно создать, создать и развернуть первое Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="ad9f4-232">Now that your development environment is configured, you can create, build, and deploy your first Teams app.</span></span>

- [<span data-ttu-id="ad9f4-233">Создайте первое Teams с помощью React</span><span class="sxs-lookup"><span data-stu-id="ad9f4-233">Create your first Teams app using React</span></span>](first-app-react.md)
- [<span data-ttu-id="ad9f4-234">Создайте первое Teams приложение с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="ad9f4-234">Create your first Teams app with Blazor</span></span>](first-app-blazor.md)
- [<span data-ttu-id="ad9f4-235">Создайте первое приложение Teams с SharePoint Framework (SPFx)</span><span class="sxs-lookup"><span data-stu-id="ad9f4-235">Create your first Teams app using SharePoint Framework (SPFx)</span></span>](first-app-spfx.md)
- [<span data-ttu-id="ad9f4-236">Создание приложения-бота для разговоров</span><span class="sxs-lookup"><span data-stu-id="ad9f4-236">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="ad9f4-237">Создать расширение для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="ad9f4-237">Create a messaging extension</span></span>](first-message-extension.md)
