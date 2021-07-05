---
title: 'Учебник . Создайте свое первое приложение с помощью C #'
description: Узнайте, как начать создание Microsoft Teams с помощью C# или .NET.
keywords: начало работы .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: f63e729400fa74f1675faddbe0b5f8fa101c8824
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254362"
---
# <a name="build-your-first-teams-app-using-c"></a><span data-ttu-id="42fd5-104">Создайте первое Teams с помощью C #</span><span class="sxs-lookup"><span data-stu-id="42fd5-104">Build your first Teams app using C#</span></span>

<span data-ttu-id="42fd5-105">В этом руководстве вы узнаете, как создать свое первое приложение Microsoft Teams с помощью .NET или C#.</span><span class="sxs-lookup"><span data-stu-id="42fd5-105">In this tutorial, you will learn how to build your very first Microsoft Teams app using .NET or C#.</span></span> <span data-ttu-id="42fd5-106">Кроме того, вы проходите по шагам:</span><span class="sxs-lookup"><span data-stu-id="42fd5-106">It also walks you through the steps to:</span></span>

1. [<span data-ttu-id="42fd5-107">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="42fd5-107">Prepare your environment</span></span>](#prepare-your-environment)
1. [<span data-ttu-id="42fd5-108">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="42fd5-108">Get prerequisites</span></span>](#GetPrerequisites)
1. [<span data-ttu-id="42fd5-109">Скачайте пример</span><span class="sxs-lookup"><span data-stu-id="42fd5-109">Download the sample</span></span>](#DownloadSample)
1. [<span data-ttu-id="42fd5-110">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="42fd5-110">Build and run the sample</span></span>](#BuildRun)
1. [<span data-ttu-id="42fd5-111">Хост пример приложения</span><span class="sxs-lookup"><span data-stu-id="42fd5-111">Host the sample app</span></span>](#hostsample)
1. [<span data-ttu-id="42fd5-112">Обновление учетных данных для вашего хозяйского приложения</span><span class="sxs-lookup"><span data-stu-id="42fd5-112">Update the credentials for your hosted app</span></span>](#updatecredentials)
1. [<span data-ttu-id="42fd5-113">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="42fd5-113">Configure the app tab</span></span>](#configureapptab)

<a name="prepare-your-environment"></a>
[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="42fd5-114">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="42fd5-114">Get prerequisites</span></span>

<span data-ttu-id="42fd5-115">Чтобы завершить этот учебник, необходимо установить следующие средства:</span><span class="sxs-lookup"><span data-stu-id="42fd5-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="42fd5-116">Установка Git</span><span class="sxs-lookup"><span data-stu-id="42fd5-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="42fd5-117">Установка Visual Studio</span><span class="sxs-lookup"><span data-stu-id="42fd5-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="42fd5-118">Вы можете установить бесплатное издание сообщества Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="42fd5-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="42fd5-119">Во время установки, если есть возможность добавить `git` в путь, выберите его.</span><span class="sxs-lookup"><span data-stu-id="42fd5-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="42fd5-120">В окне терминала запустите следующую команду для проверки `git` установки:</span><span class="sxs-lookup"><span data-stu-id="42fd5-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="42fd5-121">Используйте подходящее окно терминала на платформе.</span><span class="sxs-lookup"><span data-stu-id="42fd5-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="42fd5-122">В этих примерах используется Git Bash, но его можно запустить на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="42fd5-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="42fd5-123">Откройте последнюю версию Visual Studio и установите все обновления.</span><span class="sxs-lookup"><span data-stu-id="42fd5-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="42fd5-124">Вы можете использовать одно и то же окно терминала для запуска команд в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="42fd5-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="42fd5-125">Скачайте пример</span><span class="sxs-lookup"><span data-stu-id="42fd5-125">Download the sample</span></span>

<span data-ttu-id="42fd5-126">Вы можете начать работу с помощью простого [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="42fd5-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="42fd5-127">пример в C#.</span><span class="sxs-lookup"><span data-stu-id="42fd5-127">sample in C#.</span></span> <span data-ttu-id="42fd5-128">В окне терминала запустите следующую команду, чтобы клонировать репозиторий образца на компьютер:</span><span class="sxs-lookup"><span data-stu-id="42fd5-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="42fd5-129">Вы можете [вилкой](https://help.github.com/articles/fork-a-repo/) это [репо изменить](https://github.com/OfficeDev/Microsoft-Teams-Samples) и сохранить изменения в GitHub.</span><span class="sxs-lookup"><span data-stu-id="42fd5-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="42fd5-130">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="42fd5-130">Build and run the sample</span></span>

<span data-ttu-id="42fd5-131">Вы можете создать и запустить smaple после его клонирования.</span><span class="sxs-lookup"><span data-stu-id="42fd5-131">You can build and run the smaple after it is cloned.</span></span> 

<span data-ttu-id="42fd5-132">**Создание и запуск клонированной выборки**</span><span class="sxs-lookup"><span data-stu-id="42fd5-132">**To build and run the cloned sample**</span></span>

1. <span data-ttu-id="42fd5-133">Откройте файл решения **Microsoft.Teams. Samples.HelloWorld.sln** из каталога **Microsoft-Teams-Samples/samples/app-hello-world/csharp** образца.</span><span class="sxs-lookup"><span data-stu-id="42fd5-133">Open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span>
1. <span data-ttu-id="42fd5-134">Выберите **решение сборки** из меню **Сборка.**</span><span class="sxs-lookup"><span data-stu-id="42fd5-134">Select **Build Solution** from the **Build** menu.</span></span>
1. <span data-ttu-id="42fd5-135">Выберите **клавишу F5** или выберите **Пуск** отладки из меню **отладки** для запуска примера.</span><span class="sxs-lookup"><span data-stu-id="42fd5-135">Select the **F5** key, or select **Start Debugging** from the **Debug** menu to run the sample.</span></span>

    <span data-ttu-id="42fd5-136">При запуске приложения открывается окно браузера с корнем запущенного приложения.</span><span class="sxs-lookup"><span data-stu-id="42fd5-136">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="42fd5-137">Вы можете перейти к следующим URL-адресам, чтобы убедиться, что все URL-адреса приложений загружаются:</span><span class="sxs-lookup"><span data-stu-id="42fd5-137">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

    - `https://localhost:44327/`
    - `https://localhost:44327/hello`
    - `https://localhost:44327/first`
    - `https://localhost:44327/second`

    > [!Note]
    > <span data-ttu-id="42fd5-138">Если вы получили `Could not find a part of the path … bin\roslyn\csc.exe` ошибку, обнови пакет командой `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="42fd5-138">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="42fd5-139">Дополнительные сведения см. [в этом вопросе о переполнении стека.](https://stackoverflow.com/questions/32780315)</span><span class="sxs-lookup"><span data-stu-id="42fd5-139">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

    <a name="hostsample"></a>
    ## <a name="deploy-your-sample-app"></a><span data-ttu-id="42fd5-140">Развертывание примера приложения</span><span class="sxs-lookup"><span data-stu-id="42fd5-140">Deploy your sample app</span></span>

    <span data-ttu-id="42fd5-141">Приложения в Microsoft Teams — это веб-приложения, которые предоставляют одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="42fd5-141">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="42fd5-142">Для Teams платформы для загрузки приложения ваше приложение должно быть доступно в Интернете.</span><span class="sxs-lookup"><span data-stu-id="42fd5-142">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="42fd5-143">Для этого необходимо провести свое приложение.</span><span class="sxs-lookup"><span data-stu-id="42fd5-143">To do this, you need to host your app.</span></span> <span data-ttu-id="42fd5-144">Вы можете либо бесплатно Microsoft Azure, либо создать туннель для локального процесса на компьютере с помощью `ngrok` .</span><span class="sxs-lookup"><span data-stu-id="42fd5-144">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="42fd5-145">После хозяйского хозяйского приложения сделайте примечание корневого URL-адреса, например `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="42fd5-145">After you host your app, make a note of its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="42fd5-146">Tunnel ngrok</span><span class="sxs-lookup"><span data-stu-id="42fd5-146">Tunnel using ngrok</span></span>

<span data-ttu-id="42fd5-147">Для быстрого тестирования можно запустить приложение на компьютере и создать туннель к ней через веб-конечную точку.</span><span class="sxs-lookup"><span data-stu-id="42fd5-147">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="42fd5-148">[`ngrok`](https://ngrok.com) это бесплатный инструмент, с помощью которого можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="42fd5-148">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="42fd5-149">Вы можете [скачать и установить](https://ngrok.com/download) ngrok и добавить его в расположение в `PATH` вашем .</span><span class="sxs-lookup"><span data-stu-id="42fd5-149">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="42fd5-150">После установки откройте новое окно терминала и запустите следующую команду, `ngrok` чтобы создать туннель:</span><span class="sxs-lookup"><span data-stu-id="42fd5-150">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="42fd5-151">`Ngrok` отвечает на запросы из Интернета и передает их в приложение, которое работает в порту 44327.</span><span class="sxs-lookup"><span data-stu-id="42fd5-151">`Ngrok` responds to requests from the internet and routes them to your app running on port 44327.</span></span> 

<span data-ttu-id="42fd5-152">**Проверка ответа**</span><span class="sxs-lookup"><span data-stu-id="42fd5-152">**To verify the response**</span></span>

1. <span data-ttu-id="42fd5-153">Откройте браузер и перейдите к `https://d0ac14a5.ngrok.io/hello` .</span><span class="sxs-lookup"><span data-stu-id="42fd5-153">Open your browser and go to `https://d0ac14a5.ngrok.io/hello`.</span></span> <span data-ttu-id="42fd5-154">Это загрузит страницу Hello приложения.</span><span class="sxs-lookup"><span data-stu-id="42fd5-154">This will load your app's Hello page.</span></span>
1. <span data-ttu-id="42fd5-155">Вместо URL-адреса, упомянутого в шаге 1, используйте адрес переададки, отображающийся `ngrok` в сеансе консоли.</span><span class="sxs-lookup"><span data-stu-id="42fd5-155">Instead of the URL mentioned in Step 1, use the forwarding address displayed by `ngrok` in your console session.</span></span>
    > [!NOTE]
    > <span data-ttu-id="42fd5-156">Если вы использовали другой порт в шаге [сборки](#build-and-run-the-sample) и запуска, убедитесь, что для установки туннеля используется один и тот же номер `ngrok` порта.</span><span class="sxs-lookup"><span data-stu-id="42fd5-156">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>
    > [!TIP]
    > <span data-ttu-id="42fd5-157">Это хорошая идея для запуска `ngrok` в другом окне терминала.</span><span class="sxs-lookup"><span data-stu-id="42fd5-157">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="42fd5-158">Это делается для того, чтобы не вмешиваться в работу `ngrok` приложения.</span><span class="sxs-lookup"><span data-stu-id="42fd5-158">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="42fd5-159">Необходимо остановить, перестроить и повторно перезахоранить приложение.</span><span class="sxs-lookup"><span data-stu-id="42fd5-159">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="42fd5-160">Сеанс `ngrok` предоставляет полезную информацию об отладки в этом окне.</span><span class="sxs-lookup"><span data-stu-id="42fd5-160">The `ngrok` session provides useful debugging information in this window.</span></span>

    <span data-ttu-id="42fd5-161">Приложение доступно только во время текущего сеанса на компьютере.</span><span class="sxs-lookup"><span data-stu-id="42fd5-161">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="42fd5-162">Если машина отключена или заснул, служба больше недоступна.</span><span class="sxs-lookup"><span data-stu-id="42fd5-162">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="42fd5-163">Помните об этом при совместном доступе приложения для тестирования другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="42fd5-163">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="42fd5-164">Если вам нужно перезапустить службу, приложение возвращает новый адрес, и необходимо обновить каждое расположение, использующее этот адрес.</span><span class="sxs-lookup"><span data-stu-id="42fd5-164">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="42fd5-165">Платная версия `ngrok` не имеет этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="42fd5-165">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="42fd5-166">Хост в Azure</span><span class="sxs-lookup"><span data-stu-id="42fd5-166">Host in Azure</span></span>

<span data-ttu-id="42fd5-167">Microsoft Azure размещено приложение .NET на бесплатном уровне с помощью общей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="42fd5-167">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="42fd5-168">Этого достаточно для запуска `Hello World` примера.</span><span class="sxs-lookup"><span data-stu-id="42fd5-168">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="42fd5-169">Дополнительные сведения см. в [создании новой бесплатной учетной записи Azure.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="42fd5-169">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="42fd5-170">Visual Studio имеет встроенную поддержку развертывания приложений для различных поставщиков, в том числе Azure:</span><span class="sxs-lookup"><span data-stu-id="42fd5-170">Visual Studio has built-in support for app deployment to different providers, including Azure:</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

<span data-ttu-id="42fd5-171">**Обновление пакета приложений**</span><span class="sxs-lookup"><span data-stu-id="42fd5-171">**Update the app package**</span></span>

# <a name="app-studio"></a>[<span data-ttu-id="42fd5-172">App Studio</span><span class="sxs-lookup"><span data-stu-id="42fd5-172">App Studio</span></span>](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[<span data-ttu-id="42fd5-173">Портал разработчика</span><span class="sxs-lookup"><span data-stu-id="42fd5-173">Developer Portal</span></span>](#tab/DP)

<span data-ttu-id="42fd5-174">**Установка портала разработчиков (предварительный просмотр) в Teams**</span><span class="sxs-lookup"><span data-stu-id="42fd5-174">**To install Developer Portal (preview) in Teams**</span></span>


1. <span data-ttu-id="42fd5-175">Выберите **значок Apps** в нижней части левой панели и поиск **портала разработчиков.**</span><span class="sxs-lookup"><span data-stu-id="42fd5-175">Select the **Apps** icon at the bottom of the left-hand bar, and search for **Developer Portal**.</span></span>

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. <span data-ttu-id="42fd5-176">Выберите **портал разработчика** и выберите **Open**.</span><span class="sxs-lookup"><span data-stu-id="42fd5-176">Select **Developer Portal** and select **Open**.</span></span>

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. <span data-ttu-id="42fd5-177">Выберите вкладку Apps и **выберите Импорт существующего приложения.**</span><span class="sxs-lookup"><span data-stu-id="42fd5-177">Select the Apps tab and select **Import an existing app**.</span></span>

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. <span data-ttu-id="42fd5-178">Выберите **Hello World** и выберите **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="42fd5-178">Select **Hello World** and select **Import**.</span></span> <span data-ttu-id="42fd5-179">Приложение **Hello World** импортируется на портале разработчиков.</span><span class="sxs-lookup"><span data-stu-id="42fd5-179">The **Hello World** app is imported in Developer Portal.</span></span> 

    <span data-ttu-id="42fd5-180">Вы можете настроить приложение с помощью портала Teams разработчика.</span><span class="sxs-lookup"><span data-stu-id="42fd5-180">You can configure your app using the Teams Developer Portal.</span></span> <span data-ttu-id="42fd5-181">Манифест находится в статье Распределить.</span><span class="sxs-lookup"><span data-stu-id="42fd5-181">The Manifest is found under Distribute.</span></span> <span data-ttu-id="42fd5-182">Манифест можно использовать для настройки возможностей, необходимых ресурсов и других важных атрибутов для приложения.</span><span class="sxs-lookup"><span data-stu-id="42fd5-182">You can use the Manifest to configure capabilities, required resources, and other important attributes for your app.</span></span> <span data-ttu-id="42fd5-183">Дополнительные сведения о настройке приложения с помощью портала разработчиков см. в Teams [портале разработчиков.](../concepts/build-and-test/teams-developer-portal.md)</span><span class="sxs-lookup"><span data-stu-id="42fd5-183">For more details on how to configure your app using Developer Portal, see [Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).</span></span>

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>
---

<a name="updatecredentials"></a>
## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="42fd5-184">Обновление учетных данных для вашего хозяйского приложения</span><span class="sxs-lookup"><span data-stu-id="42fd5-184">Update the credentials for your hosted app</span></span>

<span data-ttu-id="42fd5-185">Пример приложения требует, чтобы переменные среды были задатки значениям, сохраненным в текстовом файле.</span><span class="sxs-lookup"><span data-stu-id="42fd5-185">The sample app requires the environment variables to be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="42fd5-186">**Обновление учетных данных для вашего хозяйского приложения**</span><span class="sxs-lookup"><span data-stu-id="42fd5-186">**To update the credentials for your hosted app**</span></span>

1. <span data-ttu-id="42fd5-187">Откройте файл `appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="42fd5-187">Open the `appsettings.json` file.</span></span> 
1. <span data-ttu-id="42fd5-188">Обновите **значение MicrosoftAppId** с помощью бот-ИД, сохраненного в текстовом файле.</span><span class="sxs-lookup"><span data-stu-id="42fd5-188">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> 
1. <span data-ttu-id="42fd5-189">Обнови **microsoftAppPassword с** помощью сохраненного пароля бота.</span><span class="sxs-lookup"><span data-stu-id="42fd5-189">Update the **MicrosoftAppPassword** with the bot password that you saved.</span></span>

    <img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

    <span data-ttu-id="42fd5-190">После внесения этих изменений перестроим приложение.</span><span class="sxs-lookup"><span data-stu-id="42fd5-190">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="42fd5-191">Если вы используете ngrok, запустите приложение локально, а если вы размещены в Azure, передискуй приложение.</span><span class="sxs-lookup"><span data-stu-id="42fd5-191">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

<a name="configureapptab"></a>
## <a name="configure-the-app-tab"></a><span data-ttu-id="42fd5-192">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="42fd5-192">Configure the app tab</span></span>

<span data-ttu-id="42fd5-193">После установки приложения в группы необходимо настроить его для отображения контента.</span><span class="sxs-lookup"><span data-stu-id="42fd5-193">After you have installed the app into teams, you must configure it to display the content.</span></span> 

<span data-ttu-id="42fd5-194">**Настройка вкладки приложения**</span><span class="sxs-lookup"><span data-stu-id="42fd5-194">**To configure the app tab**</span></span>

1. <span data-ttu-id="42fd5-195">Перейдите к каналу в команде, где установлен пример приложения, и выберите кнопку **"+",** чтобы добавить новую вкладку.</span><span class="sxs-lookup"><span data-stu-id="42fd5-195">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab.</span></span>
1. <span data-ttu-id="42fd5-196">Выберите **Hello World** из списка Добавить **вкладку.**</span><span class="sxs-lookup"><span data-stu-id="42fd5-196">Select **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="42fd5-197">Отображается диалоговое окно конфигурации, которое позволяет выбрать вкладку для отображения в этом канале.</span><span class="sxs-lookup"><span data-stu-id="42fd5-197">A configuration dialog box is displayed that enables you to select the tab to display in this channel.</span></span> 
1. <span data-ttu-id="42fd5-198">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="42fd5-198">Select **Save**.</span></span> <span data-ttu-id="42fd5-199">Вкладка `Hello World` загружается вкладками.</span><span class="sxs-lookup"><span data-stu-id="42fd5-199">The `Hello World` tab is loaded with the tab.</span></span>

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="42fd5-200">Проверьте бот в Teams</span><span class="sxs-lookup"><span data-stu-id="42fd5-200">Test your bot in Teams</span></span>

<span data-ttu-id="42fd5-201">Теперь вы можете протестировать бот в Teams.</span><span class="sxs-lookup"><span data-stu-id="42fd5-201">You can now test the bot in Teams.</span></span> 

<span data-ttu-id="42fd5-202">**Тестирование бота**</span><span class="sxs-lookup"><span data-stu-id="42fd5-202">**To test your bot**</span></span>

* <span data-ttu-id="42fd5-203">Выберите канал в команде, в которой вы зарегистрировали приложение и `@your-bot-name` введите.</span><span class="sxs-lookup"><span data-stu-id="42fd5-203">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="42fd5-204">Это называется **\@ упоминанием**.</span><span class="sxs-lookup"><span data-stu-id="42fd5-204">This is called an **\@mention**.</span></span> <span data-ttu-id="42fd5-205">Бот отвечает на любое сообщение, которое вы отправляете.</span><span class="sxs-lookup"><span data-stu-id="42fd5-205">The bot replies to any message that you send.</span></span>

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="42fd5-206">Тестирование расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="42fd5-206">Test your messaging extension</span></span>

<span data-ttu-id="42fd5-207">**Тестирование расширения обмена сообщениями**</span><span class="sxs-lookup"><span data-stu-id="42fd5-207">**To test your messaging extension**</span></span>
1. <span data-ttu-id="42fd5-208">Выберите **...** ниже входного окна в представлении беседы.</span><span class="sxs-lookup"><span data-stu-id="42fd5-208">Select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="42fd5-209">Отображается меню с приложением **"Hello World".**</span><span class="sxs-lookup"><span data-stu-id="42fd5-209">A menu with the **'Hello World'** app is displayed.</span></span> 
1. <span data-ttu-id="42fd5-210">Выберите меню, будет отображаться набор случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="42fd5-210">Select the menu, a set of random texts is displayed.</span></span> <span data-ttu-id="42fd5-211">Вы можете выбрать один из случайных текстов, который вставляется в беседу.</span><span class="sxs-lookup"><span data-stu-id="42fd5-211">You can select one of the random text and that is inserted into your conversation.</span></span>

    <img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. <span data-ttu-id="42fd5-212">Выберите один из случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="42fd5-212">Select one of the random text.</span></span> <span data-ttu-id="42fd5-213">Показана карта, отформатированная и готовая к отправке с помощью собственного сообщения.</span><span class="sxs-lookup"><span data-stu-id="42fd5-213">A card formatted and ready to send with your own message is shown.</span></span>

    <img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

## <a name="see-also"></a><span data-ttu-id="42fd5-214">См. также</span><span class="sxs-lookup"><span data-stu-id="42fd5-214">See also</span></span>

* [<span data-ttu-id="42fd5-215">Обзор учебников</span><span class="sxs-lookup"><span data-stu-id="42fd5-215">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="42fd5-216">Создание бота беседы</span><span class="sxs-lookup"><span data-stu-id="42fd5-216">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="42fd5-217">Создание расширения для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="42fd5-217">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="42fd5-218">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="42fd5-218">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)