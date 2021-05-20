---
title: 'Учебник - Создайте свое первое приложение с помощью C #'
description: Узнайте, как начать строить Microsoft Teams приложения с помощью C-NET или .NET.
keywords: начало работы .net c' csharp
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
# <a name="create-your-first-teams-app-using-c"></a><span data-ttu-id="ece04-104">Создайте свое первое Teams с помощью C #</span><span class="sxs-lookup"><span data-stu-id="ece04-104">Create your first Teams app using C#</span></span>

<span data-ttu-id="ece04-105">Этот учебник поможет вам создать приложение Microsoft Teams с помощью C.</span><span class="sxs-lookup"><span data-stu-id="ece04-105">This tutorial helps you to create a Microsoft Teams app using C#.</span></span> <span data-ttu-id="ece04-106">Чтобы достичь этого, примите следующие меры:</span><span class="sxs-lookup"><span data-stu-id="ece04-106">To do this, you must:</span></span>

* <span data-ttu-id="ece04-107">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="ece04-107">Prepare your environment</span></span>
* <span data-ttu-id="ece04-108">Получить предпосылки</span><span class="sxs-lookup"><span data-stu-id="ece04-108">Get prerequisites</span></span>
* <span data-ttu-id="ece04-109">Скачать образец</span><span class="sxs-lookup"><span data-stu-id="ece04-109">Download the sample</span></span>
* <span data-ttu-id="ece04-110">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="ece04-110">Build and run the sample</span></span>
* <span data-ttu-id="ece04-111">Хозяин образца приложения</span><span class="sxs-lookup"><span data-stu-id="ece04-111">Host the sample app</span></span>
* <span data-ttu-id="ece04-112">Обновление учетных данных для размещенной приложения</span><span class="sxs-lookup"><span data-stu-id="ece04-112">Update the credentials for your hosted app</span></span>
* <span data-ttu-id="ece04-113">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="ece04-113">Configure the app tab</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="ece04-114">Получить предпосылки</span><span class="sxs-lookup"><span data-stu-id="ece04-114">Get prerequisites</span></span>

<span data-ttu-id="ece04-115">Чтобы завершить этот учебник, вам нужно установить следующие инструменты:</span><span class="sxs-lookup"><span data-stu-id="ece04-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="ece04-116">Установка Git</span><span class="sxs-lookup"><span data-stu-id="ece04-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="ece04-117">Установка Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ece04-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="ece04-118">Вы можете установить бесплатное издание сообщества Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ece04-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="ece04-119">Во время установки, если есть возможность добавить `git` в путь, выберите его.</span><span class="sxs-lookup"><span data-stu-id="ece04-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="ece04-120">В окне терминала запустите следующую команду для проверки `git` установки:</span><span class="sxs-lookup"><span data-stu-id="ece04-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="ece04-121">Используйте подходящее окно терминала на вашей платформе.</span><span class="sxs-lookup"><span data-stu-id="ece04-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="ece04-122">Эти примеры используют Git Bash, но могут быть запущены на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="ece04-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="ece04-123">Откройте последнюю версию Visual Studio установите любые обновления.</span><span class="sxs-lookup"><span data-stu-id="ece04-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="ece04-124">Вы можете использовать то же окно терминала для запуска команд в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ece04-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="ece04-125">Скачать образец</span><span class="sxs-lookup"><span data-stu-id="ece04-125">Download the sample</span></span>

<span data-ttu-id="ece04-126">Вы можете начать работу с простого [Здравствуйте, Мир!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="ece04-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="ece04-127">образец в СЗ.</span><span class="sxs-lookup"><span data-stu-id="ece04-127">sample in C#.</span></span> <span data-ttu-id="ece04-128">В окне терминала запустите следующую команду клонировать репозиторий образца на компьютер:</span><span class="sxs-lookup"><span data-stu-id="ece04-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="ece04-129">Вы можете [раскошелиться](https://help.github.com/articles/fork-a-repo/) [на это репо,](https://github.com/OfficeDev/Microsoft-Teams-Samples) чтобы изменить и сохранить ваши изменения, GitHub.</span><span class="sxs-lookup"><span data-stu-id="ece04-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="ece04-130">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="ece04-130">Build and run the sample</span></span>

<span data-ttu-id="ece04-131">После клонирования репо используйте Visual Studio для открытия файла решения **Microsoft.Teams. Примеры.HelloWorld.sln** **из каталога Microsoft-Teams-Samples/samples/app-hello-world/csharp.**</span><span class="sxs-lookup"><span data-stu-id="ece04-131">After the repo is cloned, use Visual Studio to open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span> <span data-ttu-id="ece04-132">Затем выберите **решение Build из** **меню Build.**</span><span class="sxs-lookup"><span data-stu-id="ece04-132">Then, select **Build Solution** from the **Build** menu.</span></span> <span data-ttu-id="ece04-133">Чтобы выбежать из образца, **нажмите F5** или выберите **Start Debugging** из **меню отладки.**</span><span class="sxs-lookup"><span data-stu-id="ece04-133">To run the sample, press **F5** or select **Start Debugging** from the **Debug** menu.</span></span>

<span data-ttu-id="ece04-134">Когда приложение запускается, окно браузера открывается с корнем запущенного приложения.</span><span class="sxs-lookup"><span data-stu-id="ece04-134">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="ece04-135">Вы можете перейти к следующим URL-адресам, чтобы убедиться, что все URL-адреса приложений загружаются:</span><span class="sxs-lookup"><span data-stu-id="ece04-135">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="ece04-136">Если вы получили `Could not find a part of the path … bin\roslyn\csc.exe` ошибку, обновите пакет с `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` командой.</span><span class="sxs-lookup"><span data-stu-id="ece04-136">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="ece04-137">Для получения дополнительной информации, [см. этот вопрос на стек переполнения](https://stackoverflow.com/questions/32780315).</span><span class="sxs-lookup"><span data-stu-id="ece04-137">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="ece04-138">Хозяин образца приложения</span><span class="sxs-lookup"><span data-stu-id="ece04-138">Host the sample app</span></span>

<span data-ttu-id="ece04-139">Приложения в Microsoft Teams веб-приложений, которые обеспечивают одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="ece04-139">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="ece04-140">Для Teams платформы для загрузки приложения приложение должно быть доступно в Интернете.</span><span class="sxs-lookup"><span data-stu-id="ece04-140">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="ece04-141">Для этого необходимо разместить приложение.</span><span class="sxs-lookup"><span data-stu-id="ece04-141">To do this, you need to host your app.</span></span> <span data-ttu-id="ece04-142">Вы можете либо разместить его Microsoft Azure бесплатно, либо создать туннель для локального процесса на вашем компьютере с помощью `ngrok` .</span><span class="sxs-lookup"><span data-stu-id="ece04-142">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="ece04-143">После размещения приложения обратите внимание на его корневой URL, например `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="ece04-143">After you host your app, note its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="ece04-144">Tunnel использование ngrok</span><span class="sxs-lookup"><span data-stu-id="ece04-144">Tunnel using ngrok</span></span>

<span data-ttu-id="ece04-145">Для быстрого тестирования можно запустить приложение на компьютере и создать туннель к нему через веб-конечную точку.</span><span class="sxs-lookup"><span data-stu-id="ece04-145">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="ece04-146">[`ngrok`](https://ngrok.com) это бесплатный инструмент, с помощью которого вы можете получить веб-адрес, например `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="ece04-146">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="ece04-147">Вы можете [скачать и](https://ngrok.com/download) установить ngrok и добавить его в место в `PATH` вашем .</span><span class="sxs-lookup"><span data-stu-id="ece04-147">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="ece04-148">После установки `ngrok` откройте новое окно терминала и запустите следующую команду для создания туннеля:</span><span class="sxs-lookup"><span data-stu-id="ece04-148">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="ece04-149">`Ngrok` прослушивает запросы из Интернета и маршрутит их в приложение, запущеное в порту 44327.</span><span class="sxs-lookup"><span data-stu-id="ece04-149">`Ngrok` listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="ece04-150">Чтобы проверить, откройте браузер и перейдите `https://d0ac14a5.ngrok.io/hello` на загрузку привет страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="ece04-150">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="ece04-151">Вместо этого URL используйте адрес переголовки, отображаемый `ngrok` в сеансе консоли.</span><span class="sxs-lookup"><span data-stu-id="ece04-151">Instead of this URL, use the forwarding address displayed by `ngrok` in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="ece04-152">Если вы использовали другой порт в этапе [сборки и запуска,](#build-and-run-the-sample) убедитесь, что вы используете тот же номер порта для настройки `ngrok` туннеля.</span><span class="sxs-lookup"><span data-stu-id="ece04-152">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="ece04-153">Это хорошая идея, чтобы `ngrok` работать в другом окне терминала.</span><span class="sxs-lookup"><span data-stu-id="ece04-153">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="ece04-154">Это делается для того, `ngrok` чтобы не работать, не мешая приложению.</span><span class="sxs-lookup"><span data-stu-id="ece04-154">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="ece04-155">Вы должны остановить, восстановить и повторно использовать приложение.</span><span class="sxs-lookup"><span data-stu-id="ece04-155">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="ece04-156">Сеанс `ngrok` предоставляет полезную информацию об отладке в этом окне.</span><span class="sxs-lookup"><span data-stu-id="ece04-156">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="ece04-157">Приложение доступно только во время текущего сеанса на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ece04-157">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="ece04-158">Если машина выключена или засыпает, услуга больше недоступна.</span><span class="sxs-lookup"><span data-stu-id="ece04-158">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="ece04-159">Помните об этом, когда вы делитесь приложением для тестирования с другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="ece04-159">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="ece04-160">Если вам нужно перезапустить службу, приложение возвращает новый адрес, и вы должны обновить каждое место, которое использует этот адрес.</span><span class="sxs-lookup"><span data-stu-id="ece04-160">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="ece04-161">Платная версия `ngrok` не имеет этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="ece04-161">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="ece04-162">Хозяин в Azure</span><span class="sxs-lookup"><span data-stu-id="ece04-162">Host in Azure</span></span>

<span data-ttu-id="ece04-163">Microsoft Azure размещает ваше приложение .NET на бесплатном уровне с использованием общей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="ece04-163">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="ece04-164">Этого достаточно для запуска `Hello World` выборки.</span><span class="sxs-lookup"><span data-stu-id="ece04-164">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="ece04-165">Для получения дополнительной информации [можно создать новую бесплатную учетную запись Azure.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="ece04-165">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="ece04-166">Visual Studio имеет встроенную поддержку развертывания приложений для различных поставщиков, включая Azure:</span><span class="sxs-lookup"><span data-stu-id="ece04-166">Visual Studio has built-in support for app deployment to different providers, including Azure:</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="ece04-167">Обновление учетных данных для размещенной приложения</span><span class="sxs-lookup"><span data-stu-id="ece04-167">Update the credentials for your hosted app</span></span>

<span data-ttu-id="ece04-168">Пример приложения требует, чтобы переменные среды были установлены на значения, сохраненные в текстовом файле.</span><span class="sxs-lookup"><span data-stu-id="ece04-168">The sample app requires the environment variables to be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="ece04-169">Откройте файл `appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="ece04-169">Open the `appsettings.json` file.</span></span> <span data-ttu-id="ece04-170">Обновление значения **MicrosoftAppId с** помощью идентификатора бота, сохраненного в текстовом файле.</span><span class="sxs-lookup"><span data-stu-id="ece04-170">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> <span data-ttu-id="ece04-171">Обновление **MicrosoftAppPassword с сохраненный** вами пароль бота.</span><span class="sxs-lookup"><span data-stu-id="ece04-171">Update the **MicrosoftAppPassword** with the bot password you saved.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="ece04-172">После внесения этих изменений переутомить приложение.</span><span class="sxs-lookup"><span data-stu-id="ece04-172">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="ece04-173">Если вы используете ngrok, запустите приложение локально, и если вы хостинг в Azure, передислоцировать приложение.</span><span class="sxs-lookup"><span data-stu-id="ece04-173">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="ece04-174">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="ece04-174">Configure the app tab</span></span>

<span data-ttu-id="ece04-175">После установки приложения в команду необходимо настроить его для показов содержимого.</span><span class="sxs-lookup"><span data-stu-id="ece04-175">Once you install the app into a team, you must configure it to show content.</span></span> <span data-ttu-id="ece04-176">Перейдите на канал в команде, где вы установили образец приложения и выберите **кнопку "Я",** чтобы добавить новую вкладку. Выберите **Hello World** из **списка вкладок Add.**</span><span class="sxs-lookup"><span data-stu-id="ece04-176">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab. Choose **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="ece04-177">Отображается диалоговое окно конфигурации, которое позволяет выбрать вкладку для отображения в этом канале.</span><span class="sxs-lookup"><span data-stu-id="ece04-177">A configuration dialog box is displayed that enables you to choose the tab to display in this channel.</span></span> <span data-ttu-id="ece04-178">После выбора вкладки и выбора **Сохранить** `Hello World` вкладку загружается с вкладкой.</span><span class="sxs-lookup"><span data-stu-id="ece04-178">After you select the tab and select **Save** the `Hello World` tab is loaded with the tab.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="ece04-179">Проверьте своего бота в Teams</span><span class="sxs-lookup"><span data-stu-id="ece04-179">Test your bot in Teams</span></span>

<span data-ttu-id="ece04-180">Теперь вы можете протестировать бота в Teams.</span><span class="sxs-lookup"><span data-stu-id="ece04-180">Now you can test the bot in Teams.</span></span> <span data-ttu-id="ece04-181">Выберите канал в команде, где вы зарегистрировали приложение и ввех. `@your-bot-name`</span><span class="sxs-lookup"><span data-stu-id="ece04-181">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="ece04-182">Это называется **\@ упоминанием**.</span><span class="sxs-lookup"><span data-stu-id="ece04-182">This is called an **\@mention**.</span></span> <span data-ttu-id="ece04-183">Бот отвечает на любое сообщение, которое вы отправляете.</span><span class="sxs-lookup"><span data-stu-id="ece04-183">The bot replies to any message that you send.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="ece04-184">Проверьте расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="ece04-184">Test your messaging extension</span></span>

<span data-ttu-id="ece04-185">Чтобы проверить расширение обмена сообщениями, вы можете выбрать **...**</span><span class="sxs-lookup"><span data-stu-id="ece04-185">To test your messaging extension, you can select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="ece04-186">Отображается меню **с приложением** «Здравствуйте, мир».</span><span class="sxs-lookup"><span data-stu-id="ece04-186">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="ece04-187">При его выборе отображается набор случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="ece04-187">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="ece04-188">Вы можете выбрать один из случайных текста, который вставляется в ваш разговор.</span><span class="sxs-lookup"><span data-stu-id="ece04-188">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="ece04-189">Выберите один из случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="ece04-189">Select one of the random text.</span></span> <span data-ttu-id="ece04-190">Отображается карта, отформатированная и готовая к отправке с вашим собственным сообщением.</span><span class="sxs-lookup"><span data-stu-id="ece04-190">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
