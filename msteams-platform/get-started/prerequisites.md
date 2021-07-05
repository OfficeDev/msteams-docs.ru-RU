---
title: Начало работы - Необходимые условия
author: adrianhall
description: Узнайте, как начать работу с разработкой Microsoft Teams и настроить среду.
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 4796d37aa0ef904805fbfe2956f9e1d49960bfe9
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254268"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="2d7e7-103">Необходимые условия: начало разработки Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="2d7e7-103">Prerequisites: Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="2d7e7-104">Прежде чем приступить к созданию первого Teams приложения, необходимо установить несколько инструментов и настроить среду разработки.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-104">Before you begin with creating your first Teams app, you must install a few tools and set up your development environment.</span></span>

## <a name="install-required-tools"></a><span data-ttu-id="2d7e7-105">Установка необходимых средств</span><span class="sxs-lookup"><span data-stu-id="2d7e7-105">Install required tools</span></span>

<span data-ttu-id="2d7e7-106">Некоторые из необходимых инструментов зависят от того, как вы предпочитаете создавать Teams приложение:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-106">Some of the tools you need depend on how you prefer to build your Teams app:</span></span>

- <span data-ttu-id="2d7e7-107">[Node.js](https://nodejs.org/en/download/) (используйте последний выпуск V14 LTS)</span><span class="sxs-lookup"><span data-stu-id="2d7e7-107">[Node.js](https://nodejs.org/en/download/) (use the latest v14 LTS release)</span></span>
- <span data-ttu-id="2d7e7-108">Браузер с средствами разработки, такими как [Microsoft Edge](https://www.microsoft.com/edge) (рекомендуется) или [Google Chrome](https://www.google.com/chrome/)</span><span class="sxs-lookup"><span data-stu-id="2d7e7-108">A browser with developer tools, such as, [Microsoft Edge](https://www.microsoft.com/edge) (recommended) or [Google Chrome](https://www.google.com/chrome/)</span></span>
- <span data-ttu-id="2d7e7-109">Если вы разрабатываете с Помощью JavaScript, TypeScript или SharePoint Framework (SPFx), установите Visual Studio Code [версии](https://code.visualstudio.com/download)1.55 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-109">If you are developing with JavaScript, TypeScript, or the SharePoint Framework (SPFx), install [Visual Studio Code](https://code.visualstudio.com/download), version 1.55 or later.</span></span>  
- <span data-ttu-id="2d7e7-110">Если вы разрабатываете с помощью .NET, [установите Visual Studio 2019](https://visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="2d7e7-110">If you are developing with .NET, install [Visual Studio 2019](https://visualstudio.com/download).</span></span> <span data-ttu-id="2d7e7-111">Убедитесь, что ASP.NET **и веб-разработки** или **межплатформеной** рабочей нагрузки .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-111">Ensure you install the **ASP.NET and web development** or **.NET Core cross-platform development** workload.</span></span>

> [!WARNING]
> <span data-ttu-id="2d7e7-112">Известны проблемы с пакетом `npm@7` с node v15 и более поздним пакетом.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-112">There are known issues with `npm@7`, packaged with Node v15 and later.</span></span> <span data-ttu-id="2d7e7-113">Если у вас возникли проблемы с запуском, убедитесь, что `npm install` вы используете узел v14 (LTS)</span><span class="sxs-lookup"><span data-stu-id="2d7e7-113">If you have problems running `npm install`, ensure you're using Node v14 (LTS)</span></span>

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="2d7e7-114">Установка Teams набор средств</span><span class="sxs-lookup"><span data-stu-id="2d7e7-114">Install the Teams Toolkit</span></span>

<span data-ttu-id="2d7e7-115">Этот Teams набор средств упрощает процесс разработки с помощью средств для обеспечения и развертывания облачных ресурсов для приложения, публикации в Teams магазине и других.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-115">The Teams Toolkit helps simplify the development process with tools to provision and deploy cloud resources for your app, publish to the Teams store, and more.</span></span> <span data-ttu-id="2d7e7-116">Инструментарий можно использовать с помощью Visual Studio Code, Visual Studio или CLI `teamsfx` (называется).</span><span class="sxs-lookup"><span data-stu-id="2d7e7-116">You can use the toolkit with Visual Studio Code, Visual Studio, or as a CLI (called `teamsfx`).</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="2d7e7-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2d7e7-117">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="2d7e7-118">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-118">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="2d7e7-119">Выберите представление **Расширения** **(Ctrl+Shift+X**  /  **⌘⇧-X** или **> расширения).**</span><span class="sxs-lookup"><span data-stu-id="2d7e7-119">Select the **Extensions** view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="2d7e7-120">В поле поиска введите **Teams набор средств**.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-120">In the search box, enter **Teams Toolkit**.</span></span>
1. <span data-ttu-id="2d7e7-121">Выберите **Установите** рядом с Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-121">Select **Install** next to the Teams Toolkit.</span></span>

<span data-ttu-id="2d7e7-122">Вы также можете найти Teams набор средств на Visual Studio Code [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span><span class="sxs-lookup"><span data-stu-id="2d7e7-122">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="2d7e7-123">Следующие средства могут быть установлены расширением Visual Studio Code при необходимости.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-123">The following tools can be installed by the Visual Studio Code extension when they are needed.</span></span> <span data-ttu-id="2d7e7-124">Если уже установлено, установленную версию можно использовать вместо нее.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-124">If already installed, the installed version can be used instead.</span></span> <span data-ttu-id="2d7e7-125">Если используется Linux, включая WSL, необходимо установить эти средства перед использованием:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-125">If using Linux including WSL, you must install these tools before use:</span></span>

- [<span data-ttu-id="2d7e7-126">Основные средства Azure Functions</span><span class="sxs-lookup"><span data-stu-id="2d7e7-126">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="2d7e7-127">Основные средства Azure Functions используются для локального запуска отлаженных компонентов, включая помощников проверки подлинности, необходимых при запуске служб в Azure.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-127">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span> <span data-ttu-id="2d7e7-128">Он устанавливается в каталоге проекта (с помощью `devDependencies` npm).</span><span class="sxs-lookup"><span data-stu-id="2d7e7-128">It is installed within the project directory (using the npm `devDependencies`).</span></span>

- [<span data-ttu-id="2d7e7-129">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="2d7e7-129">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="2d7e7-130">SDK .NET используется для установки настраиваемых привязки для локального отладки и развертывания приложений Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-130">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span> <span data-ttu-id="2d7e7-131">Если вы не установили SDK .NET 3.1 (или более поздней версии) глобально, портативная версия может быть установлена.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-131">If you have not installed the .NET 3.1 (or later) SDK globally, the portable version can be installed.</span></span>

- [<span data-ttu-id="2d7e7-132">ngrok</span><span class="sxs-lookup"><span data-stu-id="2d7e7-132">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="2d7e7-133">Некоторые Teams приложения (беседные боты, расширения обмена сообщениями и входящие веб-оки) требуют входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-133">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span> <span data-ttu-id="2d7e7-134">Необходимо подвергать систему разработки Teams через туннель.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-134">You need to expose your development system to Teams through a tunnel.</span></span> <span data-ttu-id="2d7e7-135">Туннель не требуется для приложений, которые включают только вкладки.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-135">A tunnel is not required for apps that only include tabs.</span></span> <span data-ttu-id="2d7e7-136">Этот пакет устанавливается в каталоге проекта (с помощью `devDependencies` npm).</span><span class="sxs-lookup"><span data-stu-id="2d7e7-136">This package is installed within the project directory (using npm `devDependencies`).</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="2d7e7-137">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="2d7e7-137">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="2d7e7-138">Вы можете использовать Visual Studio 2019 для разработки Teams с помощью Blazor Server в .NET.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-138">You can use Visual Studio 2019 to develop Teams apps with Blazor Server in .NET.</span></span> <span data-ttu-id="2d7e7-139">Если вы не собираетесь разрабатывать Teams в .NET, установите Visual Studio Code версию Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-139">If you are not intending to develop Teams apps in .NET, install the Visual Studio Code version of Teams Toolkit.</span></span>

<span data-ttu-id="2d7e7-140">Чтобы установить расширение Teams набор средств:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-140">To install the Teams Toolkit extension:</span></span>

1. <span data-ttu-id="2d7e7-141">Open Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-141">Open Visual Studio 2019.</span></span>
1. <span data-ttu-id="2d7e7-142">Выберите **Расширения Управление**  >  **расширениями**.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-142">Select **Extensions** > **Manage Extensions**.</span></span>
1. <span data-ttu-id="2d7e7-143">В поле поиска введите **Teams набор средств**.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-143">In the search box, enter **Teams Toolkit**.</span></span>
1. <span data-ttu-id="2d7e7-144">Выберите расширение Teams набор средств и выберите **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-144">Select the Teams Toolkit extension and select **Download**.</span></span> <span data-ttu-id="2d7e7-145">Расширение загружается.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-145">The extension is downloaded.</span></span>
1. <span data-ttu-id="2d7e7-146">Закрыть Visual Studio 2019 г. для установки расширения.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-146">Close Visual Studio 2019 to install the extension.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="2d7e7-147">Командная строка</span><span class="sxs-lookup"><span data-stu-id="2d7e7-147">Command line</span></span>](#tab/cli)

<span data-ttu-id="2d7e7-148">Чтобы установить CLI TeamsFx, используйте диспетчер `npm` пакетов:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-148">To install the TeamsFx CLI, use the `npm` package manager:</span></span>

``` bash
npm install -g @microsoft/teamsfx-cli
```

<span data-ttu-id="2d7e7-149">В зависимости от конфигурации может потребоваться использовать для `sudo` установки CLI:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-149">Depending on your configuration, you may need to use `sudo` to install the CLI:</span></span>

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

<span data-ttu-id="2d7e7-150">Это чаще встречается в системах Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-150">This is more common on Linux and macOS systems.</span></span>

<span data-ttu-id="2d7e7-151">Убедитесь, что вы добавляете глобальный кэш npm в path.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-151">Ensure you add the npm global cache to your PATH.</span></span> <span data-ttu-id="2d7e7-152">Обычно это делается как часть Node.js установки.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-152">This is normally done as part of the Node.js installer.</span></span>  

<span data-ttu-id="2d7e7-153">CLI можно использовать с `teamsfx` командой.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-153">You can use the CLI with the `teamsfx` command.</span></span> <span data-ttu-id="2d7e7-154">Убедитесь, что команда работает с помощью `teamsfx -h` запуска .</span><span class="sxs-lookup"><span data-stu-id="2d7e7-154">Verify that the command is working by running `teamsfx -h`.</span></span>

> [!CAUTION]
> <span data-ttu-id="2d7e7-155">Прежде чем запустить TeamsFx в терминалах PowerShell, необходимо включить политику "удаленного подписанного" выполнения для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-155">Before you can run TeamsFx in PowerShell terminals, you must enable the "remote signed" execution policy for PowerShell.</span></span> <span data-ttu-id="2d7e7-156">Дополнительные сведения можно найти в [документации PowerShell.](/powershell/module/microsoft.powershell.core/about/about_signing)</span><span class="sxs-lookup"><span data-stu-id="2d7e7-156">For more information, refer to the [PowerShell documentation](/powershell/module/microsoft.powershell.core/about/about_signing).</span></span>

---

## <a name="install-optional-tools"></a><span data-ttu-id="2d7e7-157">Установка необязательных средств</span><span class="sxs-lookup"><span data-stu-id="2d7e7-157">Install optional tools</span></span>

<span data-ttu-id="2d7e7-158">Установите средства браузера для разработки приложений.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-158">Install browser tools for app development.</span></span> <span data-ttu-id="2d7e7-159">Например, если приложение написано с помощью React, вы можете использовать React средства разработчика:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-159">For instance, if your app is written with React, you can use React Developer Tools:</span></span>

- [<span data-ttu-id="2d7e7-160">React Средства разработчика для Chrome</span><span class="sxs-lookup"><span data-stu-id="2d7e7-160">React Developer Tools for Chrome</span></span>](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

<span data-ttu-id="2d7e7-161">Если вы хотите получить доступ к данным, хранимым в Azure, или развернуть облачную Teams приложения в Azure, установите эти средства:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-161">If you want to access data stored in Azure or deploy a cloud-based backend for your Teams app in Azure, install these tools:</span></span>

- [<span data-ttu-id="2d7e7-162">Azure Tools для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2d7e7-162">Azure Tools for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [<span data-ttu-id="2d7e7-163">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2d7e7-163">Azure CLI</span></span>](/cli/azure/install-azure-cli)

<span data-ttu-id="2d7e7-164">Если вы работаете с данными microsoft Graph, вы должны узнать о и закладки Microsoft Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-164">If you work with Microsoft Graph data, you should learn about and bookmark the Microsoft Graph Explorer.</span></span> <span data-ttu-id="2d7e7-165">Этот инструмент на основе браузера позволяет запрашивать microsoft Graph за пределами приложения.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-165">This browser-based tool allows you to query Microsoft Graph outside of an app.</span></span>

- [<span data-ttu-id="2d7e7-166">Microsoft Graph Explorer</span><span class="sxs-lookup"><span data-stu-id="2d7e7-166">Microsoft Graph Explorer</span></span>](https://developer.microsoft.com/graph/graph-explorer)

<span data-ttu-id="2d7e7-167">С помощью портала разработчиков для Teams вы можете настроить, управлять и распространять Teams приложения, в том числе в организации или Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-167">With the Developer Portal for Teams, you can configure, manage, and distribute your Teams app including to your organization or the Teams store.</span></span>

- [<span data-ttu-id="2d7e7-168">Портал разработчиков Teams</span><span class="sxs-lookup"><span data-stu-id="2d7e7-168">Developer Portal for Teams</span></span>](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a><span data-ttu-id="2d7e7-169">Включить загрузку побок</span><span class="sxs-lookup"><span data-stu-id="2d7e7-169">Enable sideloading</span></span>

<span data-ttu-id="2d7e7-170">Во время разработки необходимо загрузить приложение в пределах Teams без его распространения.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-170">During development, you must load your app within Teams without distributing it.</span></span> <span data-ttu-id="2d7e7-171">Это называется боковой загрузкой.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-171">This is known as sideloading.</span></span>

<span data-ttu-id="2d7e7-172">Если у вас есть Teams учетная запись, проверьте, можно ли перегружать приложения в Teams:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-172">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>

1. <span data-ttu-id="2d7e7-173">В клиенте Teams выберите **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-173">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="2d7e7-174">Выберите **Upload настраиваемом приложении.**</span><span class="sxs-lookup"><span data-stu-id="2d7e7-174">Select **Upload a custom app**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, Teams вы можете загрузить пользовательское приложение.":::

> [!NOTE]
> <span data-ttu-id="2d7e7-176">Если вы по-прежнему не можете разгрузить приложения, поговорите с Teams администратором.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-176">If you still cannot sideload apps, talk to your Teams administrator.</span></span> <span data-ttu-id="2d7e7-177">См. в Teams настраиваемые приложения и [включите настраиваемую загрузку](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) приложений для подробных сведений.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-177">See [enable custom Teams apps and turn on custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for details.</span></span>

## <a name="get-a-free-teams-developer-tenant-optional"></a><span data-ttu-id="2d7e7-178">Получите бесплатный клиент Teams разработчика (необязательный)</span><span class="sxs-lookup"><span data-stu-id="2d7e7-178">Get a free Teams developer tenant (optional)</span></span>

<span data-ttu-id="2d7e7-179">Если вы не видите параметр sideload или у вас нет учетной записи Teams, вы можете получить бесплатную учетную запись Teams разработчика, присоединившись к программе разработчика M365.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-179">If you cannot see the sideload option, or you do not have a Teams account, you can get a free Teams developer account by joining the M365 developer program.</span></span>  <span data-ttu-id="2d7e7-180">Процесс регистрации занимает примерно две минуты.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-180">The registration process takes approximately two minutes.</span></span>

1. <span data-ttu-id="2d7e7-181">Перейдите в [Microsoft 365 разработчика](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="2d7e7-181">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="2d7e7-182">Выберите **Join Now** и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-182">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="2d7e7-183">На экране приветствия выберите **настройка подписки E5.**</span><span class="sxs-lookup"><span data-stu-id="2d7e7-183">In the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="2d7e7-184">Настройка учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-184">Set up your administrator account.</span></span> <span data-ttu-id="2d7e7-185">После завершения, вы должны увидеть экран, как это.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-185">After you finish, you should see a screen like this.</span></span>

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации на программу Microsoft 365 разработчика.":::

1. <span data-ttu-id="2d7e7-187">Вопишитесь Teams с помощью только что настроенной учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-187">Sign in to Teams using the administrator account you just set up.</span></span> <span data-ttu-id="2d7e7-188">Убедитесь, что у **Upload есть настраиваемый параметр** приложения.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-188">Verify that you have the **Upload a custom app** option.</span></span>

## <a name="get-a-free-azure-account"></a><span data-ttu-id="2d7e7-189">Получить бесплатную учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="2d7e7-189">Get a free Azure account</span></span>

<span data-ttu-id="2d7e7-190">Если вы хотите провести свое приложение или получить доступ к ресурсам в Azure, необходимо иметь подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-190">If you wish to host your app or access resources within Azure, you must have an Azure subscription.</span></span>  <span data-ttu-id="2d7e7-191">Перед [началом работы можно](https://azure.microsoft.com/free/) создать бесплатную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-191">You can [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a><span data-ttu-id="2d7e7-192">Вход в учетные записи Microsoft 365 Azure</span><span class="sxs-lookup"><span data-stu-id="2d7e7-192">Sign in to your Microsoft 365 and Azure accounts</span></span>

<span data-ttu-id="2d7e7-193">Необходимо иметь доступ к двум учетным записям:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-193">You must have access to two accounts:</span></span>

- <span data-ttu-id="2d7e7-194">Учетные данные Microsoft 365 учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-194">Your Microsoft 365 account credentials.</span></span> <span data-ttu-id="2d7e7-195">Это учетная запись, которую вы используете для регистрации Teams.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-195">This is the account that you use to sign in to Teams.</span></span> <span data-ttu-id="2d7e7-196">Если вы используете клиента Microsoft 365 разработчика, это учетная запись администратора, настроенная при регистрации для программы.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-196">If you're using a Microsoft 365 developer program tenant, this is the admin account you set up when you registered for the program.</span></span>
- <span data-ttu-id="2d7e7-197">Учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-197">Your Azure credentials.</span></span> <span data-ttu-id="2d7e7-198">Это учетная запись, используемая для доступа к порталу Azure и для предоставления новых облачных ресурсов для поддержки приложения.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-198">This is the account that you use to access the Azure Portal and for provisioning new cloud resources to support your app.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="2d7e7-199">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2d7e7-199">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="2d7e7-200">Откройте Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2d7e7-200">Open Visual Studio Code</span></span>
1. <span data-ttu-id="2d7e7-201">Выберите значок Teams на боковой панели:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-201">Select the Teams icon in the sidebar:</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. <span data-ttu-id="2d7e7-203">Выберите **вход в M365**.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-203">Select **Sign in to M365**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Расположение раздела Учетные записи, используемого для регистрации.":::

    <span data-ttu-id="2d7e7-205">Процесс регистрации начинается с обычного веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-205">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="2d7e7-206">Завершите процесс регистрации для учетной записи M365.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-206">Complete the sign-in process for your M365 account.</span></span> <span data-ttu-id="2d7e7-207">При запросе можно закрыть браузер и вернуться к Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-207">When you are prompted, you can close the browser and return to Visual Studio Code.</span></span>
1. <span data-ttu-id="2d7e7-208">Возвращайся к Teams набор средств в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-208">Return to the Teams Toolkit within Visual Studio Code.</span></span>
1. <span data-ttu-id="2d7e7-209">Выберите **вход в Azure.**</span><span class="sxs-lookup"><span data-stu-id="2d7e7-209">Select **Sign in to Azure**.</span></span>

    > [!TIP]
    > <span data-ttu-id="2d7e7-210">Если у вас установлено расширение учетной записи Azure и используется та же учетная запись, вы можете пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-210">If you have the Azure Account extension installed and are using the same account, you can skip this step.</span></span> <span data-ttu-id="2d7e7-211">Используйте ту же учетную запись, что и в других расширениях.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-211">Use the same account as you are using in other extensions.</span></span>

1. <span data-ttu-id="2d7e7-212">Процесс регистрации начинается с обычного веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-212">The sign-in process starts using your normal web browser.</span></span>  <span data-ttu-id="2d7e7-213">Завершите процесс регистрации для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-213">Complete the sign-in process for your Azure account.</span></span> <span data-ttu-id="2d7e7-214">При запросе можно закрыть браузер и вернуться к Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-214">When are prompted, you can close the browser and return to Visual Studio Code.</span></span>

    <span data-ttu-id="2d7e7-215">По завершению раздел **ACCOUNTS** боковой панели отображает две учетные записи отдельно, а также количество доступных вам подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-215">When complete, the **ACCOUNTS** section of the sidebar shows the two accounts separately, together with the number of usable Azure subscriptions available to you.</span></span> <span data-ttu-id="2d7e7-216">Убедитесь, что у вас есть по крайней мере одна доступная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-216">Ensure you have at least one usable Azure subscription available.</span></span> <span data-ttu-id="2d7e7-217">Если нет, выпишитесь и используйте другую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-217">If not, sign out and use a different account.</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="2d7e7-218">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="2d7e7-218">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="2d7e7-219">Visual Studio 2019 г. при необходимости необходимо войти в каждую службу.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-219">Visual Studio 2019 prompts you to log in to each service as required.</span></span> <span data-ttu-id="2d7e7-220">Вам не нужно заранее войти в учетные записи M365 и Azure.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-220">You do not need to sign in to your M365 and Azure accounts in advance.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="2d7e7-221">Командная строка</span><span class="sxs-lookup"><span data-stu-id="2d7e7-221">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="2d7e7-222">Во входе Microsoft 365 с CLI TeamsFx:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-222">Sign in to Microsoft 365 with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login m365
    ```

    <span data-ttu-id="2d7e7-223">Процесс регистрации начинается с обычного веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-223">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="2d7e7-224">Завершите процесс регистрации для учетной записи M365.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-224">Complete the sign-in process for your M365 account.</span></span> <span data-ttu-id="2d7e7-225">Вам будет предложено закрыть браузер.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-225">You are prompted when you can close the browser.</span></span>

2. <span data-ttu-id="2d7e7-226">Во входе в Azure с CLI TeamsFx:</span><span class="sxs-lookup"><span data-stu-id="2d7e7-226">Sign in to Azure with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login azure
    ```

    <span data-ttu-id="2d7e7-227">Процесс регистрации начинается с обычного веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-227">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="2d7e7-228">Завершите процесс регистрации для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-228">Complete the sign-in process for your Azure account.</span></span> <span data-ttu-id="2d7e7-229">Вам будет предложено закрыть браузер.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-229">You are prompted when you can close the browser.</span></span>

    <span data-ttu-id="2d7e7-230">Логины учетных записей делятся между Visual Studio Code и CLI TeamsFx.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-230">The account logins are shared between Visual Studio Code and the TeamsFx CLI.</span></span>



    <span data-ttu-id="2d7e7-231">После настройки среды разработки можно создать, создать и развернуть первое Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="2d7e7-231">Now that your development environment is configured, you can create, build, and deploy your first Teams app.</span></span>

## <a name="see-also"></a><span data-ttu-id="2d7e7-232">См. также</span><span class="sxs-lookup"><span data-stu-id="2d7e7-232">See also</span></span>

* [<span data-ttu-id="2d7e7-233">Обзор учебников</span><span class="sxs-lookup"><span data-stu-id="2d7e7-233">Tutorials Overview</span></span>](code-samples.md) 
* [<span data-ttu-id="2d7e7-234">Создание приложения с React</span><span class="sxs-lookup"><span data-stu-id="2d7e7-234">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="2d7e7-235">Создание приложения с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="2d7e7-235">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="2d7e7-236">Создание приложения с SPFx</span><span class="sxs-lookup"><span data-stu-id="2d7e7-236">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="2d7e7-237">Создание приложения с помощью C# или .NET</span><span class="sxs-lookup"><span data-stu-id="2d7e7-237">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="2d7e7-238">Создайте приложение с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="2d7e7-238">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="2d7e7-239">Создание приложения с помощью генератора Yeoman</span><span class="sxs-lookup"><span data-stu-id="2d7e7-239">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="2d7e7-240">Создание бота беседы</span><span class="sxs-lookup"><span data-stu-id="2d7e7-240">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="2d7e7-241">Создание расширения для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="2d7e7-241">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="2d7e7-242">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="2d7e7-242">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
