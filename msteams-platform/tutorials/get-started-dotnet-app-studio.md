---
title: 'Учебник . Создайте свое первое приложение с помощью C #'
description: Узнайте, как начать создание приложений Microsoft Teams с помощью C# или .NET.
keywords: начало работы .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 29cc4e0f434bf9ece9c6073af84627acc048b628
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294756"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a><span data-ttu-id="d7649-104">Создайте свое первое приложение Teams с помощью C# или .NET</span><span class="sxs-lookup"><span data-stu-id="d7649-104">Create your first Teams app using C# or .NET</span></span>

<span data-ttu-id="d7649-105">Этот учебник поможет вам создать приложение Microsoft Teams с помощью C# или .NET.</span><span class="sxs-lookup"><span data-stu-id="d7649-105">This tutorial helps you to create a Microsoft Teams app using C# or .NET.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="d7649-106">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="d7649-106">Get prerequisites</span></span>

<span data-ttu-id="d7649-107">Чтобы завершить этот учебник, необходимо получить следующие средства:</span><span class="sxs-lookup"><span data-stu-id="d7649-107">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="d7649-108">Установка Git</span><span class="sxs-lookup"><span data-stu-id="d7649-108">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="d7649-109">[Установка Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d7649-109">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="d7649-110">Вы можете установить бесплатное издание сообщества.</span><span class="sxs-lookup"><span data-stu-id="d7649-110">You can install the free community edition.</span></span>

<span data-ttu-id="d7649-111">При установке, если есть возможность добавить в `git` PATH, выберите его.</span><span class="sxs-lookup"><span data-stu-id="d7649-111">During installation, if there is an option to add `git` to the PATH, choose it.</span></span>

<span data-ttu-id="d7649-112">В окне терминала запустите следующую команду для проверки `git` установки:</span><span class="sxs-lookup"><span data-stu-id="d7649-112">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="d7649-113">Используйте подходящее окно терминала на платформе.</span><span class="sxs-lookup"><span data-stu-id="d7649-113">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="d7649-114">В этих примерах используется Bash, но они работают на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="d7649-114">These examples use Bash but run on most platforms.</span></span>

<span data-ttu-id="d7649-115">Обязательно запустите последнюю версию Visual Studio и установите все обновления.</span><span class="sxs-lookup"><span data-stu-id="d7649-115">Make sure to launch the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="d7649-116">Вы можете использовать одно и то же окно терминала для запуска команд в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="d7649-116">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="d7649-117">Скачайте пример</span><span class="sxs-lookup"><span data-stu-id="d7649-117">Download the sample</span></span>

<span data-ttu-id="d7649-118">Вы можете начать работу с помощью простого [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="d7649-118">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="d7649-119">пример в C#.</span><span class="sxs-lookup"><span data-stu-id="d7649-119">sample in C#.</span></span> <span data-ttu-id="d7649-120">В окне терминала запустите следующую команду, чтобы клонировать репозиторий образца на локальной машине:</span><span class="sxs-lookup"><span data-stu-id="d7649-120">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="d7649-121">Вы можете [вилка](https://help.github.com/articles/fork-a-repo/) этого [репо](https://github.com/OfficeDev/Microsoft-Teams-Samples) изменить и сохранить изменения в GitHub для справки.</span><span class="sxs-lookup"><span data-stu-id="d7649-121">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub for reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="d7649-122">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="d7649-122">Build and run the sample</span></span>

<span data-ttu-id="d7649-123">После клонирования репо используйте Visual Studio файл решения из каталога `Microsoft.Teams.Samples.HelloWorld.sln` **Microsoft-Teams-Samples/samples/app-hello-world/csharp** и выберите из `Build Solution` `Build` меню.</span><span class="sxs-lookup"><span data-stu-id="d7649-123">After the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample and select `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="d7649-124">Для запуска примерного `F5` нажатия или `Start Debugging` выбора `Debug` меню.</span><span class="sxs-lookup"><span data-stu-id="d7649-124">To run the sample press `F5` or choose `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="d7649-125">При запуске приложения открывается окно браузера с корнем запущенного приложения.</span><span class="sxs-lookup"><span data-stu-id="d7649-125">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="d7649-126">Вы можете перейти к следующим URL-адресам, чтобы убедиться, что все URL-адреса приложений загружаются:</span><span class="sxs-lookup"><span data-stu-id="d7649-126">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- <span data-ttu-id="d7649-127">[https://localhost:44327/second]https://localhost:44327/second)</span><span class="sxs-lookup"><span data-stu-id="d7649-127">[https://localhost:44327/second]https://localhost:44327/second)</span></span>

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="d7649-128">Если вы получили `Could not find a part of the path … bin\roslyn\csc.exe` ошибку, обнови пакет командой `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="d7649-128">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="d7649-129">Дополнительные сведения см. [в этом вопросе на сайте StackOverflow.](https://stackoverflow.com/questions/32780315)</span><span class="sxs-lookup"><span data-stu-id="d7649-129">For more information, see [this question on StackOverflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="d7649-130">Хост пример приложения</span><span class="sxs-lookup"><span data-stu-id="d7649-130">Host the sample app</span></span>

<span data-ttu-id="d7649-131">Приложения в Microsoft Teams — это веб-приложения, которые предоставляют одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="d7649-131">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="d7649-132">Для загрузки приложения на платформе Teams ваше приложение должно быть доступно из Интернета.</span><span class="sxs-lookup"><span data-stu-id="d7649-132">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="d7649-133">Чтобы сделать ваше приложение доступно из Интернета, необходимо провести ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="d7649-133">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="d7649-134">Вы можете бесплатно разработать его в Microsoft Azure или создать туннель для локального процесса на компьютере `ngrok` разработки.</span><span class="sxs-lookup"><span data-stu-id="d7649-134">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="d7649-135">Когда вы закончите размещение приложения, обратите внимание на его корневой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="d7649-135">When you finish hosting your app, note its root URL.</span></span> <span data-ttu-id="d7649-136">Например, `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="d7649-136">For example, `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="d7649-137">Туннель с помощью ngrok</span><span class="sxs-lookup"><span data-stu-id="d7649-137">Tunnel using ngrok</span></span>

<span data-ttu-id="d7649-138">Для быстрого тестирования можно запустить приложение на локальной машине и создать туннель к ней через веб-конечную точку.</span><span class="sxs-lookup"><span data-stu-id="d7649-138">For quick testing, you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="d7649-139">[ngrok](https://ngrok.com) — это бесплатный инструмент, с помощью которого можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="d7649-139">[ngrok](https://ngrok.com) is a free tool with which you can get a web address such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="d7649-140">Вы можете [скачать и установить](https://ngrok.com/download) ngrok.</span><span class="sxs-lookup"><span data-stu-id="d7649-140">You can [download and install](https://ngrok.com/download) ngrok.</span></span> <span data-ttu-id="d7649-141">Убедитесь, что вы добавляете его в расположение в вашем `PATH` .</span><span class="sxs-lookup"><span data-stu-id="d7649-141">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="d7649-142">После установки ngrok откройте новое окно терминала и запустите следующую команду, чтобы создать туннель:</span><span class="sxs-lookup"><span data-stu-id="d7649-142">After you install ngrok, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="d7649-143">В примере используется порт 44327, чтобы указать его.</span><span class="sxs-lookup"><span data-stu-id="d7649-143">The sample uses port 44327 be sure to specify it.</span></span>

<span data-ttu-id="d7649-144">Ngrok прослушивает запросы из Интернета и передает их в приложение, которое работает в порту 44327.</span><span class="sxs-lookup"><span data-stu-id="d7649-144">Ngrok listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="d7649-145">Чтобы проверить, откройте браузер и перейдите к загрузке страницы `https://d0ac14a5.ngrok.io/hello` привета приложения.</span><span class="sxs-lookup"><span data-stu-id="d7649-145">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="d7649-146">Вместо этого URL-адреса используйте адрес переададки, отображающийся ngrok в сеансе консоли.</span><span class="sxs-lookup"><span data-stu-id="d7649-146">Instead of this URL, use the forwarding address displayed by ngrok in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="d7649-147">Если вы использовали другой порт в шаге [сборки](#build-and-run-the-sample) и запуска, убедитесь, что для установки туннеля используется один и тот же номер `ngrok` порта.</span><span class="sxs-lookup"><span data-stu-id="d7649-147">If you have used a different port in the [build and run](#build-and-run-the-sample) step, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="d7649-148">Это хорошая идея для запуска `ngrok` в другом окне терминала.</span><span class="sxs-lookup"><span data-stu-id="d7649-148">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="d7649-149">Это делается для того, чтобы не мешать запуску ngrok без вмешиваться в работу приложения, которое необходимо остановить, восстановить и повторно перезагрузить.</span><span class="sxs-lookup"><span data-stu-id="d7649-149">This is done to keep ngrok from running without interfering with the app, which you have to stop, rebuild, and rerun.</span></span> <span data-ttu-id="d7649-150">Сеанс `ngrok` предоставляет полезную информацию об отладки в этом окне.</span><span class="sxs-lookup"><span data-stu-id="d7649-150">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="d7649-151">Приложение доступно только во время текущего сеанса на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="d7649-151">The app is only available during the current session on your development machine.</span></span> <span data-ttu-id="d7649-152">Если машина отключена или заснул, служба больше недоступна.</span><span class="sxs-lookup"><span data-stu-id="d7649-152">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="d7649-153">Помните об этом при совместном доступе приложения для тестирования другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="d7649-153">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="d7649-154">Если вам нужно перезапустить службу, приложение возвращает новый адрес, и необходимо обновить каждое расположение, использующее этот адрес.</span><span class="sxs-lookup"><span data-stu-id="d7649-154">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="d7649-155">Платная версия ngrok не имеет этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="d7649-155">The paid version of ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="d7649-156">Хост в Azure</span><span class="sxs-lookup"><span data-stu-id="d7649-156">Host in Azure</span></span>

<span data-ttu-id="d7649-157">В Microsoft Azure размещено приложение .NET на бесплатном уровне с помощью общей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="d7649-157">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="d7649-158">Этого достаточно для запуска `Hello World` примера.</span><span class="sxs-lookup"><span data-stu-id="d7649-158">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="d7649-159">Дополнительные сведения см. [в создании новой бесплатной учетной записи.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="d7649-159">For more information, see [creating a new free account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="d7649-160">Visual Studio имеет встроенную поддержку развертывания приложений для различных поставщиков, в том числе Azure.</span><span class="sxs-lookup"><span data-stu-id="d7649-160">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="d7649-161">Обновление учетных данных для вашего хозяйского приложения</span><span class="sxs-lookup"><span data-stu-id="d7649-161">Update the credentials for your hosted app</span></span>

<span data-ttu-id="d7649-162">Пример приложения требует, чтобы следующие переменные среды были задаты значениям, которые вы сделали ранее.</span><span class="sxs-lookup"><span data-stu-id="d7649-162">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="d7649-163">Откройте файл appsettings.jsфайле.</span><span class="sxs-lookup"><span data-stu-id="d7649-163">Open up the appsettings.json file.</span></span> <span data-ttu-id="d7649-164">Обновите *значение MicrosoftAppId* с помощью бот-ИД, сохраненного ранее.</span><span class="sxs-lookup"><span data-stu-id="d7649-164">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="d7649-165">Обнови *microsoftAppPassword* с помощью сохраненного ранее пароля Bot.</span><span class="sxs-lookup"><span data-stu-id="d7649-165">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="d7649-166">После внесения этих изменений перестроим приложение.</span><span class="sxs-lookup"><span data-stu-id="d7649-166">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="d7649-167">Если вы используете ngrok, запустите приложение локально, а если вы размещены в Azure, передиските приложение.</span><span class="sxs-lookup"><span data-stu-id="d7649-167">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="d7649-168">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="d7649-168">Configure the app tab</span></span>

<span data-ttu-id="d7649-169">После установки приложения в команду необходимо настроить его для демонстрации контента.</span><span class="sxs-lookup"><span data-stu-id="d7649-169">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="d7649-170">Перейдите к каналу в команде, где установлен пример приложения, и нажмите кнопку **"+",** чтобы добавить новую вкладку. Затем можно выбрать `Hello World` из списка **Добавить вкладку.**</span><span class="sxs-lookup"><span data-stu-id="d7649-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="d7649-171">Затем вам будет представлен диалоговое окно конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d7649-171">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="d7649-172">Этот диалоговое окно позволит выбрать вкладку, которая будет отображаться в этом канале.</span><span class="sxs-lookup"><span data-stu-id="d7649-172">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="d7649-173">После выбора вкладки и нажатия на нее можно увидеть вкладку, `Save` `Hello World` загруженную выбранной вкладками.</span><span class="sxs-lookup"><span data-stu-id="d7649-173">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="d7649-174">Тестирование бота в Teams</span><span class="sxs-lookup"><span data-stu-id="d7649-174">Test your bot in Teams</span></span>

<span data-ttu-id="d7649-175">Теперь вы можете взаимодействовать с ботом в Teams.</span><span class="sxs-lookup"><span data-stu-id="d7649-175">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="d7649-176">Выберите канал в команде, в которой вы зарегистрировали приложение и `@your-bot-name` введите.</span><span class="sxs-lookup"><span data-stu-id="d7649-176">Choose a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="d7649-177">Это называется **\@ упоминанием**.</span><span class="sxs-lookup"><span data-stu-id="d7649-177">This is called an **\@mention**.</span></span> <span data-ttu-id="d7649-178">Любое сообщение, отправленное боту, будет отправлено вам в качестве ответа.</span><span class="sxs-lookup"><span data-stu-id="d7649-178">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="d7649-179">Тестирование расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d7649-179">Test your messaging extension</span></span>

<span data-ttu-id="d7649-180">Чтобы проверить расширение обмена сообщениями, вы можете щелкнуть три точки ниже входного окна в представлении беседы.</span><span class="sxs-lookup"><span data-stu-id="d7649-180">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="d7649-181">В нем всплывет меню с приложением **"Hello World".**</span><span class="sxs-lookup"><span data-stu-id="d7649-181">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="d7649-182">При нажатии кнопки отображается куча случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="d7649-182">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="d7649-183">Вы можете выбрать любой из них, и он вставляется в ваш разговор.</span><span class="sxs-lookup"><span data-stu-id="d7649-183">You can choose any one of them and it is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="d7649-184">Выберите один из случайных текстов, и в нижней части будет отформатирована карточка, готовая к отправке с собственным сообщением.</span><span class="sxs-lookup"><span data-stu-id="d7649-184">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
