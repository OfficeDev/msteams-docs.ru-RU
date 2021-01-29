---
title: 'Учебник: создание первого приложения с помощью C #'
description: Узнайте, как начать создание приложений Microsoft Teams с помощью C#/.NET.
keywords: начало работы .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c28c4d00c375b8e37f82c343eec2c5405ae0c1c8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037041"
---
# <a name="create-your-first-microsoft-teams-app-using-c"></a><span data-ttu-id="e644c-104">Создание первого приложения Microsoft Teams с помощью C #</span><span class="sxs-lookup"><span data-stu-id="e644c-104">Create your first Microsoft Teams app using C#</span></span>

<span data-ttu-id="e644c-105">Это руководство поможет вам начать создание приложения Microsoft Teams с помощью C# на .NET.</span><span class="sxs-lookup"><span data-stu-id="e644c-105">This tutorial helps you get started creating a Microsoft Teams app using C# on .NET.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="e644c-106">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="e644c-106">Get prerequisites</span></span>

<span data-ttu-id="e644c-107">Чтобы выполнить это руководство, необходимо получить следующие средства:</span><span class="sxs-lookup"><span data-stu-id="e644c-107">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="e644c-108">Установка Git</span><span class="sxs-lookup"><span data-stu-id="e644c-108">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="e644c-109">[Установите Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e644c-109">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="e644c-110">Вы можете установить бесплатный выпуск сообщества.</span><span class="sxs-lookup"><span data-stu-id="e644c-110">You can install the free community edition.</span></span>

<span data-ttu-id="e644c-111">Если во время установки вы видите возможность добавления в `git` path, выберите этот вариант.</span><span class="sxs-lookup"><span data-stu-id="e644c-111">If you see an option to add `git` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="e644c-112">Это будет удобно.</span><span class="sxs-lookup"><span data-stu-id="e644c-112">It will be handy.</span></span>

<span data-ttu-id="e644c-113">Проверьте `git` установку, вынеся в окне терминала следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="e644c-113">Verify your `git` installation by running the following in a terminal window:</span></span>
> [!NOTE]
> <span data-ttu-id="e644c-114">Используйте окно терминала, наиболее удобное для вашей платформы.</span><span class="sxs-lookup"><span data-stu-id="e644c-114">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="e644c-115">В этих примерах используется Bash, но он будет работать на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="e644c-115">These examples use Bash, but will run on most platforms.</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

<span data-ttu-id="e644c-116">Обязательно запустите последнюю версию Visual Studio и установите все обновления, если они показаны.</span><span class="sxs-lookup"><span data-stu-id="e644c-116">Make sure to launch the latest version of Visual Studio and install any updates if shown.</span></span>

<span data-ttu-id="e644c-117">Вы можете продолжать использовать это окно терминала для запуска команд, которые следуют в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="e644c-117">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="e644c-118">Скачать пример</span><span class="sxs-lookup"><span data-stu-id="e644c-118">Download the sample</span></span>

<span data-ttu-id="e644c-119">Мы предоставили простой [привет, мир!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="e644c-119">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="e644c-120">пример на C#, чтобы начать работу.</span><span class="sxs-lookup"><span data-stu-id="e644c-120">sample in C# to get you started.</span></span> <span data-ttu-id="e644c-121">В окне терминала запустите следующую команду, чтобы клонировать образец репозитория на локальный компьютер:</span><span class="sxs-lookup"><span data-stu-id="e644c-121">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="e644c-122">Вы можете [раздвоить](https://help.github.com/articles/fork-a-repo/) этот репозитарий, если вы хотите изменить и проверить изменения в GitHub для дальнейшей ссылки. [](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="e644c-122">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) if you want to modify and check in your changes to GitHub for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="e644c-123">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="e644c-123">Build and run the sample</span></span>

<span data-ttu-id="e644c-124">После клонирования репо используйте Visual Studio, чтобы открыть файл решения из корневого каталога примера и щелкнуть `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` в `Build` меню.</span><span class="sxs-lookup"><span data-stu-id="e644c-124">Once the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and click `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="e644c-125">Пример можно запустить, нажав `F5` или выбрав `Start Debugging` пункт `Debug` меню.</span><span class="sxs-lookup"><span data-stu-id="e644c-125">You can run the sample by pressing `F5` or choosing `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="e644c-126">При запуске приложения откроется окно браузера с корнем запущенного приложения.</span><span class="sxs-lookup"><span data-stu-id="e644c-126">When the app starts, you will see a browser window open with the root of the app launched.</span></span> <span data-ttu-id="e644c-127">Чтобы убедиться, что загружаются все URL-адреса приложений, можно перейти по следующим URL-адресам:</span><span class="sxs-lookup"><span data-stu-id="e644c-127">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="e644c-128">Если вы получили сообщение об ошибке `Could not find a part of the path … bin\roslyn\csc.exe` , попробуйте обновить пакет с помощью `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` команды.</span><span class="sxs-lookup"><span data-stu-id="e644c-128">If you receive an error like `Could not find a part of the path … bin\roslyn\csc.exe`, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="e644c-129">Дополнительные сведения см. в этом вопросе на сайте [StackOverflow.](https://stackoverflow.com/questions/32780315)</span><span class="sxs-lookup"><span data-stu-id="e644c-129">See [this question on StackOverflow](https://stackoverflow.com/questions/32780315) for additional details.</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="e644c-130">Хост-приложение для примера</span><span class="sxs-lookup"><span data-stu-id="e644c-130">Host the sample app</span></span>

<span data-ttu-id="e644c-131">Помните, что приложения в Microsoft Teams — это веб-приложения, которые предлагают одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="e644c-131">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="e644c-132">Чтобы платформа Teams загружала ваше приложение, ваше приложение должно быть доступно из Интернета.</span><span class="sxs-lookup"><span data-stu-id="e644c-132">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="e644c-133">Чтобы ваше приложение было доступно из Интернета, необходимо провести его.</span><span class="sxs-lookup"><span data-stu-id="e644c-133">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="e644c-134">Вы можете либо бесплатно провести его в Microsoft Azure, либо создать туннель для локального процесса на компьютере `ngrok` разработки.</span><span class="sxs-lookup"><span data-stu-id="e644c-134">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="e644c-135">Когда вы закончите размещение приложения, заметьте его корневой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="e644c-135">When you finish hosting your app make a note of its root URL.</span></span> <span data-ttu-id="e644c-136">Он будет выглядеть так: `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="e644c-136">It will look something like: `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="e644c-137">Туннель с помощью ngrok</span><span class="sxs-lookup"><span data-stu-id="e644c-137">Tunnel using ngrok</span></span>

<span data-ttu-id="e644c-138">Для быстрого тестирования вы можете запустить приложение на локальном компьютере и создать для него туннель через веб-конечную точку.</span><span class="sxs-lookup"><span data-stu-id="e644c-138">For quick testing you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="e644c-139">[ngrok](https://ngrok.com) — это бесплатное средство, которое позволяет сделать именно это.</span><span class="sxs-lookup"><span data-stu-id="e644c-139">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="e644c-140">С помощью ngrok можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` (этот URL-адрес является лишь примером).</span><span class="sxs-lookup"><span data-stu-id="e644c-140">With ngrok you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="e644c-141">Вы можете [скачать и установить](https://ngrok.com/download) ngrok для своей среды.</span><span class="sxs-lookup"><span data-stu-id="e644c-141">You can [download and install](https://ngrok.com/download) ngrok for your environment.</span></span> <span data-ttu-id="e644c-142">Убедитесь, что вы добавили его в расположение в вашем `PATH` .</span><span class="sxs-lookup"><span data-stu-id="e644c-142">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="e644c-143">После установки можно открыть новое окно терминала и выполнить следующую команду, чтобы создать туннель.</span><span class="sxs-lookup"><span data-stu-id="e644c-143">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="e644c-144">В примере используется порт 3333, поэтому не забудьте указать его здесь.</span><span class="sxs-lookup"><span data-stu-id="e644c-144">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="e644c-145">Ngrok будет прослушивать запросы из Интернета и маршрутит их в ваше приложение, запущенного через порт 3333.</span><span class="sxs-lookup"><span data-stu-id="e644c-145">Ngrok will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="e644c-146">Вы можете проверить, открыв браузер и загрузив страницу `https://d0ac14a5.ngrok.io/hello` hello приложения.</span><span class="sxs-lookup"><span data-stu-id="e644c-146">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="e644c-147">Вместо этого URL-адреса используйте адрес переадрикии, отображающийся ngrok в сеансе консоли.</span><span class="sxs-lookup"><span data-stu-id="e644c-147">Please be sure to use the forwarding address displayed by ngrok in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="e644c-148">Если вы использовали другой порт [](#build-and-run-the-sample) в сборке и на шаге выше, убедитесь, что для настройки туннеля используется один и тот же `ngrok` номер порта.</span><span class="sxs-lookup"><span data-stu-id="e644c-148">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="e644c-149">Лучше всего запустить его в другом окне терминала, чтобы оно не помешать приложению, которое впоследствии может потребоваться остановить, перестроить `ngrok` и повторно запустить.</span><span class="sxs-lookup"><span data-stu-id="e644c-149">It is a good idea to run `ngrok` in a different terminal window to keep it running without interfering with the app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="e644c-150">Сеанс `ngrok` возвращает полезные сведения об отладки в этом окне.</span><span class="sxs-lookup"><span data-stu-id="e644c-150">The `ngrok` session will return useful debugging information in this window.</span></span>

<span data-ttu-id="e644c-151">Приложение будет доступно только во время текущего сеанса на вашем компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="e644c-151">The app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="e644c-152">Если компьютер выключен или переводится в спящий режим, служба будет недоступна.</span><span class="sxs-lookup"><span data-stu-id="e644c-152">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="e644c-153">Помните об этом при совместном использовании приложения для тестирования другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="e644c-153">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="e644c-154">Если вам нужно перезапустить службу, она возвратит новый адрес, и вам придется обновить все места, где используется этот адрес.</span><span class="sxs-lookup"><span data-stu-id="e644c-154">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span> <span data-ttu-id="e644c-155">Платная версия Ngrok не имеет этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="e644c-155">The paid version of Ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="e644c-156">Хост в Azure</span><span class="sxs-lookup"><span data-stu-id="e644c-156">Host in Azure</span></span>

<span data-ttu-id="e644c-157">Microsoft Azure позволяет вам проводить приложение .NET на бесплатном уровне с помощью общей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="e644c-157">Microsoft Azure lets you host your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="e644c-158">Этого будет достаточно для запуска этого `Hello World` примера.</span><span class="sxs-lookup"><span data-stu-id="e644c-158">This will be sufficient to run this `Hello World` sample.</span></span> <span data-ttu-id="e644c-159">Дополнительные [сведения см.](https://azure.microsoft.com/free/) в создании новой бесплатной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e644c-159">See [creating a new free account](https://azure.microsoft.com/free/) for more information.</span></span>

<span data-ttu-id="e644c-160">Visual Studio имеет встроенную поддержку развертывания приложений для разных поставщиков, включая Azure.</span><span class="sxs-lookup"><span data-stu-id="e644c-160">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="e644c-161">Обновление учетных данных для вашего ведущего приложения</span><span class="sxs-lookup"><span data-stu-id="e644c-161">Update the credentials for your hosted app</span></span>

<span data-ttu-id="e644c-162">Пример приложения требует, чтобы для следующих переменных среды были установлены значения, которые вы ранее заметили.</span><span class="sxs-lookup"><span data-stu-id="e644c-162">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="e644c-163">Откройте файл appsettings.jsфайла.</span><span class="sxs-lookup"><span data-stu-id="e644c-163">Open up the appsettings.json file.</span></span> <span data-ttu-id="e644c-164">*Обновите значение MicrosoftAppId* с помощью сохраненного ранее ИД бота.</span><span class="sxs-lookup"><span data-stu-id="e644c-164">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="e644c-165">*Обновив MicrosoftAppPassword с* помощью сохраненного ранее пароля бота.</span><span class="sxs-lookup"><span data-stu-id="e644c-165">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="e644c-166">После внесения этих изменений перестроение приложения.</span><span class="sxs-lookup"><span data-stu-id="e644c-166">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="e644c-167">Если вы используете ngrok, запустите приложение локально, а если вы размещены в Azure, развяжите приложение еще раз.</span><span class="sxs-lookup"><span data-stu-id="e644c-167">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="e644c-168">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="e644c-168">Configure the app tab</span></span>

<span data-ttu-id="e644c-169">После установки приложения в команде необходимо настроить его для показа содержимого.</span><span class="sxs-lookup"><span data-stu-id="e644c-169">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="e644c-170">Перейдите на канал в команде, где установлен пример приложения, и нажмите кнопку **"+",** чтобы добавить новую вкладку. Затем можно выбрать `Hello World` в списке **"Добавить** вкладку".</span><span class="sxs-lookup"><span data-stu-id="e644c-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="e644c-171">После этого вам будет представлено диалоговое окно конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e644c-171">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="e644c-172">Это диалоговое окно позволит выбрать вкладку, отображаемую в этом канале.</span><span class="sxs-lookup"><span data-stu-id="e644c-172">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="e644c-173">Выбрав вкладку и щелкнув ее, вы увидите вкладку, загруженную `Save` `Hello World` выбранной вкладками.</span><span class="sxs-lookup"><span data-stu-id="e644c-173">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="e644c-174">Тестирование бота в Teams</span><span class="sxs-lookup"><span data-stu-id="e644c-174">Test your bot in Teams</span></span>

<span data-ttu-id="e644c-175">Теперь вы можете взаимодействовать с ботом в Teams.</span><span class="sxs-lookup"><span data-stu-id="e644c-175">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="e644c-176">Выберите канал в команде, в которой вы зарегистрировали приложение, и введите `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="e644c-176">Choose a channel in the team where you registered your app, and type `@your-bot-name`.</span></span> <span data-ttu-id="e644c-177">Это называется **\@ упоминанием.**</span><span class="sxs-lookup"><span data-stu-id="e644c-177">This is called an **\@mention**.</span></span> <span data-ttu-id="e644c-178">Все сообщения, отправляемые боту, будут отправлены вам в качестве ответа.</span><span class="sxs-lookup"><span data-stu-id="e644c-178">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="e644c-179">Проверка расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="e644c-179">Test your messaging extension</span></span>

<span data-ttu-id="e644c-180">Чтобы протестировать расширение обмена сообщениями, можно щелкнуть три точки под полем ввода в представлении беседы.</span><span class="sxs-lookup"><span data-stu-id="e644c-180">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="e644c-181">В меню будет всплывающее меню с приложением **"Hello World".**</span><span class="sxs-lookup"><span data-stu-id="e644c-181">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="e644c-182">Щелкнув его, вы увидите множество случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="e644c-182">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="e644c-183">Вы можете выбрать любой из них, и он будет вставлен в беседу.</span><span class="sxs-lookup"><span data-stu-id="e644c-183">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="e644c-184">Выберите один из случайных текстов, и внизу отформатированная карточка будет готова к отправке с собственным сообщением.</span><span class="sxs-lookup"><span data-stu-id="e644c-184">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
