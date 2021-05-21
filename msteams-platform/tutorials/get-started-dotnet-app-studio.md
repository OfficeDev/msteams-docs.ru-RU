---
title: 'Учебник . Создайте свое первое приложение с помощью C #'
description: Узнайте, как начать создание Microsoft Teams с помощью C# или .NET.
keywords: начало работы .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: eaa37f1ccb7944ee18bb62ae47882dc4a715b165
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566889"
---
# <a name="create-your-first-teams-app-using-c"></a><span data-ttu-id="10565-104">Создайте первое Teams с помощью C #</span><span class="sxs-lookup"><span data-stu-id="10565-104">Create your first Teams app using C#</span></span>

<span data-ttu-id="10565-105">Этот учебник поможет вам создать приложение Microsoft Teams с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="10565-105">This tutorial helps you to create a Microsoft Teams app using C#.</span></span> <span data-ttu-id="10565-106">Чтобы достичь этого, примите следующие меры:</span><span class="sxs-lookup"><span data-stu-id="10565-106">To do this, you must:</span></span>

* <span data-ttu-id="10565-107">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="10565-107">Prepare your environment</span></span>
* <span data-ttu-id="10565-108">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="10565-108">Get prerequisites</span></span>
* <span data-ttu-id="10565-109">Скачайте пример</span><span class="sxs-lookup"><span data-stu-id="10565-109">Download the sample</span></span>
* <span data-ttu-id="10565-110">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="10565-110">Build and run the sample</span></span>
* <span data-ttu-id="10565-111">Хост пример приложения</span><span class="sxs-lookup"><span data-stu-id="10565-111">Host the sample app</span></span>
* <span data-ttu-id="10565-112">Обновление учетных данных для вашего хозяйского приложения</span><span class="sxs-lookup"><span data-stu-id="10565-112">Update the credentials for your hosted app</span></span>
* <span data-ttu-id="10565-113">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="10565-113">Configure the app tab</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="10565-114">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="10565-114">Get prerequisites</span></span>

<span data-ttu-id="10565-115">Чтобы завершить этот учебник, необходимо установить следующие средства:</span><span class="sxs-lookup"><span data-stu-id="10565-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="10565-116">Установка Git</span><span class="sxs-lookup"><span data-stu-id="10565-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="10565-117">Установка Visual Studio</span><span class="sxs-lookup"><span data-stu-id="10565-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="10565-118">Вы можете установить бесплатное издание сообщества Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10565-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="10565-119">Во время установки, если есть возможность добавить `git` в путь, выберите его.</span><span class="sxs-lookup"><span data-stu-id="10565-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="10565-120">В окне терминала запустите следующую команду для проверки `git` установки:</span><span class="sxs-lookup"><span data-stu-id="10565-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="10565-121">Используйте подходящее окно терминала на платформе.</span><span class="sxs-lookup"><span data-stu-id="10565-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="10565-122">В этих примерах используется Git Bash, но его можно запустить на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="10565-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="10565-123">Откройте последнюю версию Visual Studio и установите все обновления.</span><span class="sxs-lookup"><span data-stu-id="10565-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="10565-124">Вы можете использовать одно и то же окно терминала для запуска команд в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="10565-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="10565-125">Скачайте пример</span><span class="sxs-lookup"><span data-stu-id="10565-125">Download the sample</span></span>

<span data-ttu-id="10565-126">Вы можете начать работу с помощью простого [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="10565-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="10565-127">пример в C#.</span><span class="sxs-lookup"><span data-stu-id="10565-127">sample in C#.</span></span> <span data-ttu-id="10565-128">В окне терминала запустите следующую команду, чтобы клонировать репозиторий образца на компьютер:</span><span class="sxs-lookup"><span data-stu-id="10565-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="10565-129">Вы можете [вилкой](https://help.github.com/articles/fork-a-repo/) это [репо изменить](https://github.com/OfficeDev/Microsoft-Teams-Samples) и сохранить изменения в GitHub.</span><span class="sxs-lookup"><span data-stu-id="10565-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="10565-130">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="10565-130">Build and run the sample</span></span>

<span data-ttu-id="10565-131">После клонирования репо используйте Visual Studio для открытия файла **решений Microsoft.Teams. Samples.HelloWorld.sln** из каталога **Microsoft-Teams-Samples/samples/app-hello-world/csharp** образца.</span><span class="sxs-lookup"><span data-stu-id="10565-131">After the repo is cloned, use Visual Studio to open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span> <span data-ttu-id="10565-132">Затем выберите **решение сборки** из меню **Сборка.**</span><span class="sxs-lookup"><span data-stu-id="10565-132">Then, select **Build Solution** from the **Build** menu.</span></span> <span data-ttu-id="10565-133">Чтобы запустить пример, нажмите **кнопку F5 или** выберите **Пуск** отладки из **меню отладки.**</span><span class="sxs-lookup"><span data-stu-id="10565-133">To run the sample, press **F5** or select **Start Debugging** from the **Debug** menu.</span></span>

<span data-ttu-id="10565-134">При запуске приложения открывается окно браузера с корнем запущенного приложения.</span><span class="sxs-lookup"><span data-stu-id="10565-134">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="10565-135">Вы можете перейти к следующим URL-адресам, чтобы убедиться, что все URL-адреса приложений загружаются:</span><span class="sxs-lookup"><span data-stu-id="10565-135">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="10565-136">Если вы получили `Could not find a part of the path … bin\roslyn\csc.exe` ошибку, обнови пакет командой `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="10565-136">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="10565-137">Дополнительные сведения см. [в этом вопросе о переполнении стека.](https://stackoverflow.com/questions/32780315)</span><span class="sxs-lookup"><span data-stu-id="10565-137">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="10565-138">Хост пример приложения</span><span class="sxs-lookup"><span data-stu-id="10565-138">Host the sample app</span></span>

<span data-ttu-id="10565-139">Приложения в Microsoft Teams — это веб-приложения, которые предоставляют одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="10565-139">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="10565-140">Для Teams платформы для загрузки приложения ваше приложение должно быть доступно в Интернете.</span><span class="sxs-lookup"><span data-stu-id="10565-140">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="10565-141">Для этого необходимо провести свое приложение.</span><span class="sxs-lookup"><span data-stu-id="10565-141">To do this, you need to host your app.</span></span> <span data-ttu-id="10565-142">Вы можете либо бесплатно Microsoft Azure, либо создать туннель для локального процесса на компьютере с помощью `ngrok` .</span><span class="sxs-lookup"><span data-stu-id="10565-142">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="10565-143">После хозяйского приложения обратите внимание на его корневой URL-адрес, например `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="10565-143">After you host your app, note its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="10565-144">Tunnel ngrok</span><span class="sxs-lookup"><span data-stu-id="10565-144">Tunnel using ngrok</span></span>

<span data-ttu-id="10565-145">Для быстрого тестирования можно запустить приложение на компьютере и создать туннель к ней через веб-конечную точку.</span><span class="sxs-lookup"><span data-stu-id="10565-145">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="10565-146">[`ngrok`](https://ngrok.com) это бесплатный инструмент, с помощью которого можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="10565-146">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="10565-147">Вы можете [скачать и установить](https://ngrok.com/download) ngrok и добавить его в расположение в `PATH` вашем .</span><span class="sxs-lookup"><span data-stu-id="10565-147">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="10565-148">После установки откройте новое окно терминала и запустите следующую команду, `ngrok` чтобы создать туннель:</span><span class="sxs-lookup"><span data-stu-id="10565-148">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="10565-149">`Ngrok` прослушивает запросы из Интернета и передает их в приложение, которое работает в порту 44327.</span><span class="sxs-lookup"><span data-stu-id="10565-149">`Ngrok` listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="10565-150">Чтобы проверить, откройте браузер и перейдите к загрузке страницы `https://d0ac14a5.ngrok.io/hello` привета приложения.</span><span class="sxs-lookup"><span data-stu-id="10565-150">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="10565-151">Вместо этого URL-адреса используйте адрес переададки, отображающийся в `ngrok` сеансе консоли.</span><span class="sxs-lookup"><span data-stu-id="10565-151">Instead of this URL, use the forwarding address displayed by `ngrok` in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="10565-152">Если вы использовали другой порт в шаге [сборки](#build-and-run-the-sample) и запуска, убедитесь, что для установки туннеля используется один и тот же номер `ngrok` порта.</span><span class="sxs-lookup"><span data-stu-id="10565-152">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="10565-153">Это хорошая идея для запуска `ngrok` в другом окне терминала.</span><span class="sxs-lookup"><span data-stu-id="10565-153">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="10565-154">Это делается для того, чтобы не вмешиваться в работу `ngrok` приложения.</span><span class="sxs-lookup"><span data-stu-id="10565-154">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="10565-155">Необходимо остановить, перестроить и повторно перезахоранить приложение.</span><span class="sxs-lookup"><span data-stu-id="10565-155">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="10565-156">Сеанс `ngrok` предоставляет полезную информацию об отладки в этом окне.</span><span class="sxs-lookup"><span data-stu-id="10565-156">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="10565-157">Приложение доступно только во время текущего сеанса на компьютере.</span><span class="sxs-lookup"><span data-stu-id="10565-157">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="10565-158">Если машина отключена или заснул, служба больше недоступна.</span><span class="sxs-lookup"><span data-stu-id="10565-158">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="10565-159">Помните об этом при совместном доступе приложения для тестирования другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="10565-159">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="10565-160">Если вам нужно перезапустить службу, приложение возвращает новый адрес, и необходимо обновить каждое расположение, использующее этот адрес.</span><span class="sxs-lookup"><span data-stu-id="10565-160">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="10565-161">Платная версия `ngrok` не имеет этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="10565-161">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="10565-162">Хост в Azure</span><span class="sxs-lookup"><span data-stu-id="10565-162">Host in Azure</span></span>

<span data-ttu-id="10565-163">Microsoft Azure размещено приложение .NET на бесплатном уровне с помощью общей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="10565-163">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="10565-164">Этого достаточно для запуска `Hello World` примера.</span><span class="sxs-lookup"><span data-stu-id="10565-164">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="10565-165">Дополнительные сведения см. в [создании новой бесплатной учетной записи Azure.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="10565-165">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="10565-166">Visual Studio имеет встроенную поддержку развертывания приложений для различных поставщиков, в том числе Azure:</span><span class="sxs-lookup"><span data-stu-id="10565-166">Visual Studio has built-in support for app deployment to different providers, including Azure:</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="10565-167">Обновление учетных данных для вашего хозяйского приложения</span><span class="sxs-lookup"><span data-stu-id="10565-167">Update the credentials for your hosted app</span></span>

<span data-ttu-id="10565-168">Пример приложения требует, чтобы переменные среды были задатки значениям, сохраненным в текстовом файле.</span><span class="sxs-lookup"><span data-stu-id="10565-168">The sample app requires the environment variables to be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="10565-169">Откройте файл `appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="10565-169">Open the `appsettings.json` file.</span></span> <span data-ttu-id="10565-170">Обновите **значение MicrosoftAppId** с помощью бот-ИД, сохраненного в текстовом файле.</span><span class="sxs-lookup"><span data-stu-id="10565-170">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> <span data-ttu-id="10565-171">Обнови **microsoftAppPassword с** помощью сохраненного пароля бота.</span><span class="sxs-lookup"><span data-stu-id="10565-171">Update the **MicrosoftAppPassword** with the bot password you saved.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="10565-172">После внесения этих изменений перестроим приложение.</span><span class="sxs-lookup"><span data-stu-id="10565-172">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="10565-173">Если вы используете ngrok, запустите приложение локально, а если вы размещены в Azure, передискуй приложение.</span><span class="sxs-lookup"><span data-stu-id="10565-173">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="10565-174">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="10565-174">Configure the app tab</span></span>

<span data-ttu-id="10565-175">После установки приложения в команду необходимо настроить его для демонстрации контента.</span><span class="sxs-lookup"><span data-stu-id="10565-175">Once you install the app into a team, you must configure it to show content.</span></span> <span data-ttu-id="10565-176">Перейдите к каналу в команде, где установлен пример приложения, и выберите кнопку **"+",** чтобы добавить новую вкладку. Выберите **Hello World** из списка Добавить **вкладку.**</span><span class="sxs-lookup"><span data-stu-id="10565-176">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab. Choose **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="10565-177">Отображается диалоговое окно конфигурации, которое позволяет выбрать вкладку для отображения в этом канале.</span><span class="sxs-lookup"><span data-stu-id="10565-177">A configuration dialog box is displayed that enables you to choose the tab to display in this channel.</span></span> <span data-ttu-id="10565-178">После выбора вкладки и выбора **сохранить** `Hello World` вкладку загружается вкладка.</span><span class="sxs-lookup"><span data-stu-id="10565-178">After you select the tab and select **Save** the `Hello World` tab is loaded with the tab.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="10565-179">Проверьте бот в Teams</span><span class="sxs-lookup"><span data-stu-id="10565-179">Test your bot in Teams</span></span>

<span data-ttu-id="10565-180">Теперь вы можете протестировать бот в Teams.</span><span class="sxs-lookup"><span data-stu-id="10565-180">Now you can test the bot in Teams.</span></span> <span data-ttu-id="10565-181">Выберите канал в команде, в которой вы зарегистрировали приложение и `@your-bot-name` введите.</span><span class="sxs-lookup"><span data-stu-id="10565-181">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="10565-182">Это называется **\@ упоминанием**.</span><span class="sxs-lookup"><span data-stu-id="10565-182">This is called an **\@mention**.</span></span> <span data-ttu-id="10565-183">Бот отвечает на любое сообщение, которое вы отправляете.</span><span class="sxs-lookup"><span data-stu-id="10565-183">The bot replies to any message that you send.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="10565-184">Тестирование расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="10565-184">Test your messaging extension</span></span>

<span data-ttu-id="10565-185">Чтобы протестировать расширение обмена сообщениями, вы можете **выбрать ...** ниже входного окна в представлении беседы.</span><span class="sxs-lookup"><span data-stu-id="10565-185">To test your messaging extension, you can select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="10565-186">Отображается меню с приложением **"Hello World".**</span><span class="sxs-lookup"><span data-stu-id="10565-186">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="10565-187">При его выборе отображается набор случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="10565-187">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="10565-188">Вы можете выбрать один из случайных текстов, который вставляется в беседу.</span><span class="sxs-lookup"><span data-stu-id="10565-188">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="10565-189">Выберите один из случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="10565-189">Select one of the random text.</span></span> <span data-ttu-id="10565-190">Показана карта, отформатированная и готовая к отправке с помощью собственного сообщения.</span><span class="sxs-lookup"><span data-stu-id="10565-190">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
