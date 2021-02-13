---
title: 'Учебник: создание первого приложения с помощью C #'
description: Узнайте, как начать создание приложений Microsoft Teams с помощью C# или .NET.
keywords: начало работы .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: b37a8d555117e38383504dc99d82d564439a3ebf
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231531"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a><span data-ttu-id="333f1-104">Создание первого приложения Teams на C# или .NET</span><span class="sxs-lookup"><span data-stu-id="333f1-104">Create your first Teams app using C# or .NET</span></span>

<span data-ttu-id="333f1-105">Это руководство поможет вам создать приложение Microsoft Teams на C# или .NET.</span><span class="sxs-lookup"><span data-stu-id="333f1-105">This tutorial helps you to create a Microsoft Teams app using C# or .NET.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="333f1-106">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="333f1-106">Get prerequisites</span></span>

<span data-ttu-id="333f1-107">Чтобы выполнить это руководство, необходимо получить следующие средства:</span><span class="sxs-lookup"><span data-stu-id="333f1-107">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="333f1-108">Установка Git</span><span class="sxs-lookup"><span data-stu-id="333f1-108">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="333f1-109">[Установите Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="333f1-109">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="333f1-110">Вы можете установить бесплатный выпуск сообщества.</span><span class="sxs-lookup"><span data-stu-id="333f1-110">You can install the free community edition.</span></span>

<span data-ttu-id="333f1-111">При установке, если есть возможность добавить `git` путь, выберите его.</span><span class="sxs-lookup"><span data-stu-id="333f1-111">During installation, if there is an option to add `git` to the PATH, choose it.</span></span>

<span data-ttu-id="333f1-112">В окне терминала запустите следующую команду, чтобы проверить `git` установку:</span><span class="sxs-lookup"><span data-stu-id="333f1-112">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="333f1-113">Используйте подходящее окно терминала на своей платформе.</span><span class="sxs-lookup"><span data-stu-id="333f1-113">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="333f1-114">В этих примерах используется Bash, но он работает на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="333f1-114">These examples use Bash but run on most platforms.</span></span>

<span data-ttu-id="333f1-115">Обязательно запустите последнюю версию Visual Studio и установите все обновления.</span><span class="sxs-lookup"><span data-stu-id="333f1-115">Make sure to launch the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="333f1-116">Для запуска команд в этом руководстве можно использовать то же окно терминала.</span><span class="sxs-lookup"><span data-stu-id="333f1-116">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="333f1-117">Скачать пример</span><span class="sxs-lookup"><span data-stu-id="333f1-117">Download the sample</span></span>

<span data-ttu-id="333f1-118">Вы можете начать работу с простым [hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="333f1-118">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="333f1-119">пример на C#.</span><span class="sxs-lookup"><span data-stu-id="333f1-119">sample in C#.</span></span> <span data-ttu-id="333f1-120">В окне терминала запустите следующую команду, чтобы клонировать образец репозитория на локальный компьютер:</span><span class="sxs-lookup"><span data-stu-id="333f1-120">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="333f1-121">Вы можете [раздвоить](https://help.github.com/articles/fork-a-repo/) [этот репозитив,](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) чтобы изменить и сохранить изменения в GitHub для справки.</span><span class="sxs-lookup"><span data-stu-id="333f1-121">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) to modify and save your changes to GitHub for reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="333f1-122">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="333f1-122">Build and run the sample</span></span>

<span data-ttu-id="333f1-123">После клонирования репо используйте Visual Studio, чтобы открыть файл решения из корневого каталога примера и выбрать его `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` из `Build` меню.</span><span class="sxs-lookup"><span data-stu-id="333f1-123">After the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and select `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="333f1-124">Чтобы запустить пример `F5` нажатий или выбрать `Start Debugging` из `Debug` меню.</span><span class="sxs-lookup"><span data-stu-id="333f1-124">To run the sample press `F5` or choose `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="333f1-125">При запуске приложения откроется окно браузера с корнем запущенного приложения.</span><span class="sxs-lookup"><span data-stu-id="333f1-125">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="333f1-126">Чтобы убедиться, что загружаются все URL-адреса приложений, можно перейти по следующим URL-адресам:</span><span class="sxs-lookup"><span data-stu-id="333f1-126">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- <span data-ttu-id="333f1-127">[https://localhost:44327/second]https://localhost:44327/second)</span><span class="sxs-lookup"><span data-stu-id="333f1-127">[https://localhost:44327/second]https://localhost:44327/second)</span></span>

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="333f1-128">Если вы получили сообщение об `Could not find a part of the path … bin\roslyn\csc.exe` ошибке, обновим пакет с помощью `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` команды.</span><span class="sxs-lookup"><span data-stu-id="333f1-128">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="333f1-129">Дополнительные сведения см. [в этом вопросе на сайте StackOverflow.](https://stackoverflow.com/questions/32780315)</span><span class="sxs-lookup"><span data-stu-id="333f1-129">For more information, see [this question on StackOverflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="333f1-130">Хост-приложение для примера</span><span class="sxs-lookup"><span data-stu-id="333f1-130">Host the sample app</span></span>

<span data-ttu-id="333f1-131">Приложения в Microsoft Teams — это веб-приложения, которые предоставляют одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="333f1-131">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="333f1-132">Чтобы платформа Teams загружала ваше приложение, ваше приложение должно быть доступно из Интернета.</span><span class="sxs-lookup"><span data-stu-id="333f1-132">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="333f1-133">Чтобы ваше приложение было доступно из Интернета, необходимо провести его.</span><span class="sxs-lookup"><span data-stu-id="333f1-133">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="333f1-134">Вы можете либо бесплатно провести его в Microsoft Azure, либо создать туннель для локального процесса на компьютере `ngrok` разработки.</span><span class="sxs-lookup"><span data-stu-id="333f1-134">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="333f1-135">После завершения размещения приложения обратите внимание на его корневой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="333f1-135">When you finish hosting your app, note its root URL.</span></span> <span data-ttu-id="333f1-136">Например, `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="333f1-136">For example, `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="333f1-137">Туннель с помощью ngrok</span><span class="sxs-lookup"><span data-stu-id="333f1-137">Tunnel using ngrok</span></span>

<span data-ttu-id="333f1-138">Для быстрого тестирования можно запустить приложение на локальном компьютере и создать для него туннель через веб-конечную точку.</span><span class="sxs-lookup"><span data-stu-id="333f1-138">For quick testing, you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="333f1-139">[ngrok](https://ngrok.com) — это бесплатное средство, с помощью которого можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="333f1-139">[ngrok](https://ngrok.com) is a free tool with which you can get a web address such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="333f1-140">Вы можете [скачать и установить](https://ngrok.com/download) ngrok.</span><span class="sxs-lookup"><span data-stu-id="333f1-140">You can [download and install](https://ngrok.com/download) ngrok.</span></span> <span data-ttu-id="333f1-141">Убедитесь, что вы добавили его в расположение в вашем `PATH` .</span><span class="sxs-lookup"><span data-stu-id="333f1-141">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="333f1-142">После установки ngrok откройте новое окно терминала и запустите следующую команду, чтобы создать туннель:</span><span class="sxs-lookup"><span data-stu-id="333f1-142">After you install ngrok, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="333f1-143">В примере используется порт 44327, не забудьте указать его.</span><span class="sxs-lookup"><span data-stu-id="333f1-143">The sample uses port 44327 be sure to specify it.</span></span>

<span data-ttu-id="333f1-144">Ngrok прослушивает запросы из Интернета и маршрутит их в ваше приложение, запущенного на порту 44327.</span><span class="sxs-lookup"><span data-stu-id="333f1-144">Ngrok listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="333f1-145">Чтобы проверить, откройте браузер и перейдите к загрузке страницы `https://d0ac14a5.ngrok.io/hello` hello приложения.</span><span class="sxs-lookup"><span data-stu-id="333f1-145">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="333f1-146">Вместо этого URL-адреса используйте адрес переадрики, отображающийся ngrok в сеансе консоли.</span><span class="sxs-lookup"><span data-stu-id="333f1-146">Instead of this URL, use the forwarding address displayed by ngrok in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="333f1-147">Если вы использовали другой порт [](#build-and-run-the-sample) на этапе сборки и запуска, убедитесь, что для настройки туннеля используется тот же `ngrok` номер порта.</span><span class="sxs-lookup"><span data-stu-id="333f1-147">If you have used a different port in the [build and run](#build-and-run-the-sample) step, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="333f1-148">Лучше всего запустить его в `ngrok` другом окне терминала.</span><span class="sxs-lookup"><span data-stu-id="333f1-148">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="333f1-149">Это делается для того, чтобы ngrok не запускал приложение, которое необходимо остановить, перестроить и повторно запускать.</span><span class="sxs-lookup"><span data-stu-id="333f1-149">This is done to keep ngrok from running without interfering with the app, which you have to stop, rebuild, and rerun.</span></span> <span data-ttu-id="333f1-150">Сеанс `ngrok` предоставляет полезные сведения об отладки в этом окне.</span><span class="sxs-lookup"><span data-stu-id="333f1-150">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="333f1-151">Приложение доступно только во время текущего сеанса на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="333f1-151">The app is only available during the current session on your development machine.</span></span> <span data-ttu-id="333f1-152">Если компьютер выключен или переводится в спящий режим, служба больше недоступна.</span><span class="sxs-lookup"><span data-stu-id="333f1-152">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="333f1-153">Помните об этом, когда вы делитесь приложением для тестирования с другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="333f1-153">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="333f1-154">Если необходимо перезапустить службу, приложение возвращает новый адрес, и необходимо обновить все расположения, использующие этот адрес.</span><span class="sxs-lookup"><span data-stu-id="333f1-154">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="333f1-155">Платная версия ngrok не имеет этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="333f1-155">The paid version of ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="333f1-156">Хост в Azure</span><span class="sxs-lookup"><span data-stu-id="333f1-156">Host in Azure</span></span>

<span data-ttu-id="333f1-157">В Microsoft Azure приложение .NET размещено на бесплатном уровне с использованием общей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="333f1-157">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="333f1-158">Этого достаточно для запуска `Hello World` примера.</span><span class="sxs-lookup"><span data-stu-id="333f1-158">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="333f1-159">Дополнительные сведения см. [в создании новой бесплатной учетной записи.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="333f1-159">For more information, see [creating a new free account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="333f1-160">Visual Studio имеет встроенную поддержку развертывания приложений для разных поставщиков, включая Azure.</span><span class="sxs-lookup"><span data-stu-id="333f1-160">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="333f1-161">Обновление учетных данных для вашего ведущего приложения</span><span class="sxs-lookup"><span data-stu-id="333f1-161">Update the credentials for your hosted app</span></span>

<span data-ttu-id="333f1-162">Пример приложения требует, чтобы для следующих переменных среды были установлены значения, которые вы ранее заметили.</span><span class="sxs-lookup"><span data-stu-id="333f1-162">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="333f1-163">Откройте файл appsettings.jsфайла.</span><span class="sxs-lookup"><span data-stu-id="333f1-163">Open up the appsettings.json file.</span></span> <span data-ttu-id="333f1-164">*Обновите значение MicrosoftAppId* с помощью сохраненного ранее ИД бота.</span><span class="sxs-lookup"><span data-stu-id="333f1-164">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="333f1-165">*Обновив MicrosoftAppPassword с* помощью сохраненного ранее пароля бота.</span><span class="sxs-lookup"><span data-stu-id="333f1-165">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="333f1-166">После внесения этих изменений перестроение приложения.</span><span class="sxs-lookup"><span data-stu-id="333f1-166">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="333f1-167">Если вы используете ngrok, запустите приложение локально, а если вы размещены в Azure, развяжите приложение еще раз.</span><span class="sxs-lookup"><span data-stu-id="333f1-167">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="333f1-168">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="333f1-168">Configure the app tab</span></span>

<span data-ttu-id="333f1-169">После установки приложения в команде необходимо настроить его для показа содержимого.</span><span class="sxs-lookup"><span data-stu-id="333f1-169">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="333f1-170">Перейдите на канал в команде, где установлен пример приложения, и нажмите кнопку **"+",** чтобы добавить новую вкладку. Затем можно выбрать `Hello World` в списке **"Добавить** вкладку".</span><span class="sxs-lookup"><span data-stu-id="333f1-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="333f1-171">После этого вам будет представлено диалоговое окно конфигурации.</span><span class="sxs-lookup"><span data-stu-id="333f1-171">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="333f1-172">Это диалоговое окно позволит выбрать вкладку, отображаемую в этом канале.</span><span class="sxs-lookup"><span data-stu-id="333f1-172">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="333f1-173">Выбрав вкладку и щелкнув ее, вы увидите вкладку, загруженную `Save` `Hello World` выбранной вкладками.</span><span class="sxs-lookup"><span data-stu-id="333f1-173">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="333f1-174">Тестирование бота в Teams</span><span class="sxs-lookup"><span data-stu-id="333f1-174">Test your bot in Teams</span></span>

<span data-ttu-id="333f1-175">Теперь вы можете взаимодействовать с ботом в Teams.</span><span class="sxs-lookup"><span data-stu-id="333f1-175">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="333f1-176">Выберите канал в команде, в которой вы зарегистрировали приложение, и введите `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="333f1-176">Choose a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="333f1-177">Это называется **\@ упоминанием.**</span><span class="sxs-lookup"><span data-stu-id="333f1-177">This is called an **\@mention**.</span></span> <span data-ttu-id="333f1-178">Все сообщения, отправляемые боту, будут отправлены вам в качестве ответа.</span><span class="sxs-lookup"><span data-stu-id="333f1-178">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="333f1-179">Проверка расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="333f1-179">Test your messaging extension</span></span>

<span data-ttu-id="333f1-180">Чтобы протестировать расширение обмена сообщениями, можно щелкнуть три точки под полем ввода в представлении беседы.</span><span class="sxs-lookup"><span data-stu-id="333f1-180">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="333f1-181">В меню будет всплывающее меню с приложением **"Hello World".**</span><span class="sxs-lookup"><span data-stu-id="333f1-181">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="333f1-182">Щелкнув его, вы увидите множество случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="333f1-182">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="333f1-183">Вы можете выбрать любой из них и вставить его в беседу.</span><span class="sxs-lookup"><span data-stu-id="333f1-183">You can choose any one of them and it is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="333f1-184">Выберите один из случайных текстов, и внизу отформатированная карточка будет готова к отправке с собственным сообщением.</span><span class="sxs-lookup"><span data-stu-id="333f1-184">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
