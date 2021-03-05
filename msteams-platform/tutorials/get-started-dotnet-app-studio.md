---
title: 'Учебник . Создайте свое первое приложение с помощью C #'
description: Узнайте, как начать создание приложений Microsoft Teams с помощью C# или .NET.
keywords: начало работы .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: ededd0800c7f789469e79e2a475c125b7fc37795
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449357"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a><span data-ttu-id="2075b-104">Создание первого приложения Teams с C# или .NET</span><span class="sxs-lookup"><span data-stu-id="2075b-104">Create your first Teams app using C# or .NET</span></span>

<span data-ttu-id="2075b-105">Этот учебник поможет вам создать приложение Microsoft Teams с C# или .NET.</span><span class="sxs-lookup"><span data-stu-id="2075b-105">This tutorial helps you to create a Microsoft Teams app using C# or .NET.</span></span> <span data-ttu-id="2075b-106">Чтобы достичь этого, примите следующие меры:</span><span class="sxs-lookup"><span data-stu-id="2075b-106">To do this, you must:</span></span>

* <span data-ttu-id="2075b-107">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="2075b-107">Prepare your environment</span></span>
* <span data-ttu-id="2075b-108">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="2075b-108">Get prerequisites</span></span>
* <span data-ttu-id="2075b-109">Скачайте пример</span><span class="sxs-lookup"><span data-stu-id="2075b-109">Download the sample</span></span>
* <span data-ttu-id="2075b-110">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="2075b-110">Build and run the sample</span></span>
* <span data-ttu-id="2075b-111">Хост пример приложения</span><span class="sxs-lookup"><span data-stu-id="2075b-111">Host the sample app</span></span>
* <span data-ttu-id="2075b-112">Обновление учетных данных для вашего хозяйского приложения</span><span class="sxs-lookup"><span data-stu-id="2075b-112">Update the credentials for your hosted app</span></span>
* <span data-ttu-id="2075b-113">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="2075b-113">Configure the app tab</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="2075b-114">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="2075b-114">Get prerequisites</span></span>

<span data-ttu-id="2075b-115">Чтобы завершить этот учебник, необходимо установить следующие средства:</span><span class="sxs-lookup"><span data-stu-id="2075b-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="2075b-116">Установка Git</span><span class="sxs-lookup"><span data-stu-id="2075b-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="2075b-117">Установка Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2075b-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="2075b-118">Вы можете установить бесплатное издание Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2075b-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="2075b-119">Во время установки, если есть возможность добавить `git` в путь, выберите его.</span><span class="sxs-lookup"><span data-stu-id="2075b-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="2075b-120">В окне терминала запустите следующую команду для проверки `git` установки:</span><span class="sxs-lookup"><span data-stu-id="2075b-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="2075b-121">Используйте подходящее окно терминала на платформе.</span><span class="sxs-lookup"><span data-stu-id="2075b-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="2075b-122">В этих примерах используется Git Bash, но его можно запустить на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="2075b-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="2075b-123">Откройте последнюю версию Visual Studio и установите все обновления.</span><span class="sxs-lookup"><span data-stu-id="2075b-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="2075b-124">Вы можете использовать одно и то же окно терминала для запуска команд в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="2075b-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="2075b-125">Скачайте пример</span><span class="sxs-lookup"><span data-stu-id="2075b-125">Download the sample</span></span>

<span data-ttu-id="2075b-126">Вы можете начать работу с помощью простого [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="2075b-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="2075b-127">пример в C#.</span><span class="sxs-lookup"><span data-stu-id="2075b-127">sample in C#.</span></span> <span data-ttu-id="2075b-128">В окне терминала запустите следующую команду, чтобы клонировать репозиторий образца на компьютер:</span><span class="sxs-lookup"><span data-stu-id="2075b-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="2075b-129">Вы можете [раздвоить](https://help.github.com/articles/fork-a-repo/) [это репо,](https://github.com/OfficeDev/Microsoft-Teams-Samples) чтобы изменить и сохранить изменения в GitHub.</span><span class="sxs-lookup"><span data-stu-id="2075b-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="2075b-130">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="2075b-130">Build and run the sample</span></span>

<span data-ttu-id="2075b-131">После клонирования репо используйте Visual Studio для открытия файла решений **Microsoft.Teams.Samples.HelloWorld.sln** из каталога **Образцов/образцов Microsoft-Teams/samples/app-hello-world/csharp** образца.</span><span class="sxs-lookup"><span data-stu-id="2075b-131">After the repo is cloned, use Visual Studio to open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span> <span data-ttu-id="2075b-132">Затем выберите **решение сборки** из меню **Сборка.**</span><span class="sxs-lookup"><span data-stu-id="2075b-132">Then, select **Build Solution** from the **Build** menu.</span></span> <span data-ttu-id="2075b-133">Чтобы запустить пример, нажмите **кнопку F5 или** выберите **Пуск** отладки из **меню отладки.**</span><span class="sxs-lookup"><span data-stu-id="2075b-133">To run the sample, press **F5** or select **Start Debugging** from the **Debug** menu.</span></span>

<span data-ttu-id="2075b-134">При запуске приложения открывается окно браузера с корнем запущенного приложения.</span><span class="sxs-lookup"><span data-stu-id="2075b-134">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="2075b-135">Вы можете перейти к следующим URL-адресам, чтобы убедиться, что все URL-адреса приложений загружаются:</span><span class="sxs-lookup"><span data-stu-id="2075b-135">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- <span data-ttu-id="2075b-136">[https://localhost:44327/second]https://localhost:44327/second)</span><span class="sxs-lookup"><span data-stu-id="2075b-136">[https://localhost:44327/second]https://localhost:44327/second)</span></span>

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="2075b-137">Если вы получили `Could not find a part of the path … bin\roslyn\csc.exe` ошибку, обнови пакет командой `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="2075b-137">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="2075b-138">Дополнительные сведения см. [в этом вопросе о переполнении стека.](https://stackoverflow.com/questions/32780315)</span><span class="sxs-lookup"><span data-stu-id="2075b-138">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="2075b-139">Хост пример приложения</span><span class="sxs-lookup"><span data-stu-id="2075b-139">Host the sample app</span></span>

<span data-ttu-id="2075b-140">Приложения в Microsoft Teams — это веб-приложения, которые предоставляют одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="2075b-140">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="2075b-141">Для загрузки приложения на платформе Teams ваше приложение должно быть доступно в Интернете.</span><span class="sxs-lookup"><span data-stu-id="2075b-141">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="2075b-142">Для этого необходимо провести свое приложение.</span><span class="sxs-lookup"><span data-stu-id="2075b-142">To do this, you need to host your app.</span></span> <span data-ttu-id="2075b-143">Вы можете бесплатно разработать его в Microsoft Azure или создать туннель для локального процесса на `ngrok` компьютере.</span><span class="sxs-lookup"><span data-stu-id="2075b-143">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="2075b-144">После хозяйского приложения обратите внимание на его корневой URL-адрес, например `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="2075b-144">After you host your app, note its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="2075b-145">Туннель с помощью ngrok</span><span class="sxs-lookup"><span data-stu-id="2075b-145">Tunnel using ngrok</span></span>

<span data-ttu-id="2075b-146">Для быстрого тестирования можно запустить приложение на компьютере и создать туннель к ней через веб-конечную точку.</span><span class="sxs-lookup"><span data-stu-id="2075b-146">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="2075b-147">[`ngrok`](https://ngrok.com) это бесплатный инструмент, с помощью которого можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="2075b-147">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="2075b-148">Вы можете [скачать и установить](https://ngrok.com/download) ngrok и добавить его в расположение в `PATH` вашем .</span><span class="sxs-lookup"><span data-stu-id="2075b-148">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="2075b-149">После установки откройте новое окно терминала и запустите следующую команду, `ngrok` чтобы создать туннель:</span><span class="sxs-lookup"><span data-stu-id="2075b-149">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="2075b-150">`Ngrok` прослушивает запросы из Интернета и передает их в приложение, которое работает в порту 44327.</span><span class="sxs-lookup"><span data-stu-id="2075b-150">`Ngrok` listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="2075b-151">Чтобы проверить, откройте браузер и перейдите к загрузке страницы `https://d0ac14a5.ngrok.io/hello` привета приложения.</span><span class="sxs-lookup"><span data-stu-id="2075b-151">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="2075b-152">Вместо этого URL-адреса используйте адрес переададки, отображающийся в `ngrok` сеансе консоли.</span><span class="sxs-lookup"><span data-stu-id="2075b-152">Instead of this URL, use the forwarding address displayed by `ngrok` in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="2075b-153">Если вы использовали другой порт в шаге [сборки](#build-and-run-the-sample) и запуска, убедитесь, что для установки туннеля используется один и тот же номер `ngrok` порта.</span><span class="sxs-lookup"><span data-stu-id="2075b-153">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="2075b-154">Это хорошая идея для запуска `ngrok` в другом окне терминала.</span><span class="sxs-lookup"><span data-stu-id="2075b-154">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="2075b-155">Это делается для того, чтобы не вмешиваться в работу `ngrok` приложения.</span><span class="sxs-lookup"><span data-stu-id="2075b-155">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="2075b-156">Необходимо остановить, перестроить и повторно перезахоранить приложение.</span><span class="sxs-lookup"><span data-stu-id="2075b-156">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="2075b-157">Сеанс `ngrok` предоставляет полезную информацию об отладки в этом окне.</span><span class="sxs-lookup"><span data-stu-id="2075b-157">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="2075b-158">Приложение доступно только во время текущего сеанса на компьютере.</span><span class="sxs-lookup"><span data-stu-id="2075b-158">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="2075b-159">Если машина отключена или заснул, служба больше недоступна.</span><span class="sxs-lookup"><span data-stu-id="2075b-159">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="2075b-160">Помните об этом при совместном доступе приложения для тестирования другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="2075b-160">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="2075b-161">Если вам нужно перезапустить службу, приложение возвращает новый адрес, и необходимо обновить каждое расположение, использующее этот адрес.</span><span class="sxs-lookup"><span data-stu-id="2075b-161">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="2075b-162">Платная версия `ngrok` не имеет этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="2075b-162">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="2075b-163">Хост в Azure</span><span class="sxs-lookup"><span data-stu-id="2075b-163">Host in Azure</span></span>

<span data-ttu-id="2075b-164">В Microsoft Azure размещено приложение .NET на бесплатном уровне с помощью общей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="2075b-164">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="2075b-165">Этого достаточно для запуска `Hello World` примера.</span><span class="sxs-lookup"><span data-stu-id="2075b-165">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="2075b-166">Дополнительные сведения см. в [создании новой бесплатной учетной записи Azure.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="2075b-166">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="2075b-167">Visual Studio имеет встроенную поддержку развертывания приложений для различных поставщиков, включая Azure.</span><span class="sxs-lookup"><span data-stu-id="2075b-167">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="2075b-168">Обновление учетных данных для вашего хозяйского приложения</span><span class="sxs-lookup"><span data-stu-id="2075b-168">Update the credentials for your hosted app</span></span>

<span data-ttu-id="2075b-169">Пример приложения требует, чтобы переменные среды были задатки значениям, сохраненным в [текстовом файле.](~/includes/get-started/get-started-use-app-studio.md#bots)</span><span class="sxs-lookup"><span data-stu-id="2075b-169">The sample app requires the environment variables to be set to the values that you saved in the [text file](~/includes/get-started/get-started-use-app-studio.md#bots).</span></span>

<span data-ttu-id="2075b-170">Откройте appsettings.jsфайл.</span><span class="sxs-lookup"><span data-stu-id="2075b-170">Open the appsettings.json file.</span></span> <span data-ttu-id="2075b-171">Обновите **значение MicrosoftAppId** с помощью бот-ИД, сохраненного в текстовом файле.</span><span class="sxs-lookup"><span data-stu-id="2075b-171">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> <span data-ttu-id="2075b-172">Обнови **microsoftAppPassword с** помощью сохраненного пароля бота.</span><span class="sxs-lookup"><span data-stu-id="2075b-172">Update the **MicrosoftAppPassword** with the bot password you saved.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="2075b-173">После внесения этих изменений перестроим приложение.</span><span class="sxs-lookup"><span data-stu-id="2075b-173">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="2075b-174">Если вы используете ngrok, запустите приложение локально, а если вы размещены в Azure, передискуй приложение.</span><span class="sxs-lookup"><span data-stu-id="2075b-174">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="2075b-175">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="2075b-175">Configure the app tab</span></span>

<span data-ttu-id="2075b-176">После установки приложения в команду необходимо настроить его для демонстрации контента.</span><span class="sxs-lookup"><span data-stu-id="2075b-176">Once you install the app into a team, you must configure it to show content.</span></span> <span data-ttu-id="2075b-177">Перейдите к каналу в команде, где установлен пример приложения, и выберите кнопку **"+",** чтобы добавить новую вкладку. Выберите **Hello World** из списка Добавить **вкладку.**</span><span class="sxs-lookup"><span data-stu-id="2075b-177">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab. Choose **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="2075b-178">Отображается диалоговое окно конфигурации, которое позволяет выбрать вкладку для отображения в этом канале.</span><span class="sxs-lookup"><span data-stu-id="2075b-178">A configuration dialog box is displayed that enables you to choose the tab to display in this channel.</span></span> <span data-ttu-id="2075b-179">После выбора вкладки и выбора **сохранить** `Hello World` вкладку загружается вкладка.</span><span class="sxs-lookup"><span data-stu-id="2075b-179">After you select the tab and select **Save** the `Hello World` tab is loaded with the tab.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="2075b-180">Тестирование бота в Teams</span><span class="sxs-lookup"><span data-stu-id="2075b-180">Test your bot in Teams</span></span>

<span data-ttu-id="2075b-181">Теперь вы можете протестировать бот в Teams.</span><span class="sxs-lookup"><span data-stu-id="2075b-181">Now you can test the bot in Teams.</span></span> <span data-ttu-id="2075b-182">Выберите канал в команде, в которой вы зарегистрировали приложение и `@your-bot-name` введите.</span><span class="sxs-lookup"><span data-stu-id="2075b-182">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="2075b-183">Это называется **\@ упоминанием**.</span><span class="sxs-lookup"><span data-stu-id="2075b-183">This is called an **\@mention**.</span></span> <span data-ttu-id="2075b-184">Бот отвечает на любое сообщение, которое вы отправляете.</span><span class="sxs-lookup"><span data-stu-id="2075b-184">The bot replies to any message that you send.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="2075b-185">Тестирование расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="2075b-185">Test your messaging extension</span></span>

<span data-ttu-id="2075b-186">Чтобы протестировать расширение обмена сообщениями, вы можете **выбрать ...** ниже входного окна в представлении беседы.</span><span class="sxs-lookup"><span data-stu-id="2075b-186">To test your messaging extension, you can select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="2075b-187">Отображается меню с приложением **"Hello World".**</span><span class="sxs-lookup"><span data-stu-id="2075b-187">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="2075b-188">При его выборе отображается набор случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="2075b-188">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="2075b-189">Вы можете выбрать один из случайных текстов, который вставляется в беседу.</span><span class="sxs-lookup"><span data-stu-id="2075b-189">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="2075b-190">Выберите один из случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="2075b-190">Select one of the random text.</span></span> <span data-ttu-id="2075b-191">Показана карта, отформатированная и готовая к отправке с помощью собственного сообщения.</span><span class="sxs-lookup"><span data-stu-id="2075b-191">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
