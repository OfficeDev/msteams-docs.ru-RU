---
title: Начало работы с C#/.нет
description: Приступая к созданию качественных приложений в Microsoft Teams с помощью C#/.нет
keywords: Начало работы с .NET c# CSharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 61237cd3178fcb41357230536827f732faf65ee4
ms.sourcegitcommit: 510ae42f72798fb24ddef0afa771ecd9d38e5348
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "43550961"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-cnet-and-app-studio"></a><span data-ttu-id="1cb0b-104">Начало работы на платформе Microsoft Teams с C#/.нет и App Studio</span><span class="sxs-lookup"><span data-stu-id="1cb0b-104">Get started on the Microsoft Teams platform with C#/.NET and App Studio</span></span>

<span data-ttu-id="1cb0b-105">Платформа для разработчиков [Microsoft Teams](/microsoftteams/) позволяет легко расширять Teams и самостоятельно интегрировать свои приложения и службы в рабочую область Teams.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-105">The [Microsoft Teams](/microsoftteams/) developer platform makes it easy for you to extend Teams and integrate your own applications and services seamlessly into the Teams workspace.</span></span> <span data-ttu-id="1cb0b-106">Затем эти приложения можно распространять на предприятие или в Teams по всему миру.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-106">These apps can then be distributed to your enterprise or for teams around the world.</span></span>

<span data-ttu-id="1cb0b-107">Для расширения Microsoft Teams вам потребуется создать приложение Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-107">To extend Microsoft Teams, you will need to create a Microsoft Teams app.</span></span> <span data-ttu-id="1cb0b-108">Приложение Microsoft Teams — это веб-приложение, которое вы размещаете.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-108">A Microsoft Teams app is a web application that you host.</span></span> <span data-ttu-id="1cb0b-109">Затем это приложение можно интегрировать в рабочую область пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-109">This app can then be integrated into the user's workspace in Teams.</span></span>

<span data-ttu-id="1cb0b-110">Это руководство поможет вам приступить к созданию приложения Microsoft Teams с помощью C# в .NET.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-110">This tutorial helps you get started creating a Microsoft Teams app using C# on .NET.</span></span> <span data-ttu-id="1cb0b-111">Вы можете протестировать приложение, загрузив его в группу, для которой у вас есть разрешения, или в тестовый клиент, созданный с помощью программы разработчика Office.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-111">You can test the app by loading it into a Team that you have permissions for, or into a test tenant created using the Office Developer Program.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="1cb0b-112">Получение необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="1cb0b-112">Get prerequisites</span></span>

<span data-ttu-id="1cb0b-113">Для выполнения этого руководства необходимо получить следующие инструменты:</span><span class="sxs-lookup"><span data-stu-id="1cb0b-113">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="1cb0b-114">Установка Git</span><span class="sxs-lookup"><span data-stu-id="1cb0b-114">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="1cb0b-115">[Установите Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1cb0b-115">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="1cb0b-116">Вы можете установить бесплатную версию сообщества.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-116">You can install the free community edition.</span></span>

<span data-ttu-id="1cb0b-117">Если вы видите параметр, который будет `git` добавлен к пути во время установки, нажмите эту кнопку.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-117">If you see an option to add `git` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="1cb0b-118">Это будет удобно.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-118">It will be handy.</span></span>

<span data-ttu-id="1cb0b-119">Проверьте `git` установку, выполнив следующую команду в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="1cb0b-119">Verify your `git` installation by running the following in a terminal window:</span></span>
> [!NOTE]
> <span data-ttu-id="1cb0b-120">Используйте окно терминала, наиболее удобное для вашей платформы.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-120">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="1cb0b-121">В этих примерах используется bash, но они будут выполняться на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-121">These examples use Bash, but will run on most platforms.</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

<span data-ttu-id="1cb0b-122">Обязательно запустите последнюю версию Visual Studio и установите все обновления, если они отображаются.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-122">Make sure to launch the latest version of Visual Studio and install any updates if shown.</span></span>

<span data-ttu-id="1cb0b-123">Вы можете продолжить использование этого окна терминала для выполнения команд, приведенных в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-123">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="1cb0b-124">Скачать пример</span><span class="sxs-lookup"><span data-stu-id="1cb0b-124">Download the sample</span></span>

<span data-ttu-id="1cb0b-125">Мы предоставили простой [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="1cb0b-125">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="1cb0b-126">Пример в C#, чтобы приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-126">sample in C# to get you started.</span></span> <span data-ttu-id="1cb0b-127">В окне терминала выполните приведенную ниже команду, чтобы клонировать репозиторий примера на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-127">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="1cb0b-128">Вы можете [разветвление](https://help.github.com/articles/fork-a-repo/) этого [репозитория](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) , если вы хотите изменить и вернуть изменения в GitHub для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-128">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) if you want to modify and check in your changes to GitHub for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="1cb0b-129">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="1cb0b-129">Build and run the sample</span></span>

<span data-ttu-id="1cb0b-130">После клонирования репозитория с помощью Visual Studio откройте файл `Microsoft.Teams.Samples.HelloWorld.sln` решения из корневого каталога примера и щелкните `Build Solution` в `Build` меню.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-130">Once the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and click `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="1cb0b-131">Вы можете запустить пример, нажав `F5` или выбрав `Start Debugging` его `Debug` в меню.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-131">You can run the sample by pressing `F5` or choosing `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="1cb0b-132">Когда приложение запустится, откроется окно браузера с корневым каталогом запущенного приложения.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-132">When the app starts, you will see a browser window open with the root of the app launched.</span></span> <span data-ttu-id="1cb0b-133">Вы можете перейти по следующим URL-адресам, чтобы убедиться, что загружаются все URL-адреса приложений:</span><span class="sxs-lookup"><span data-stu-id="1cb0b-133">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="1cb0b-134">Если возникнет ошибка `Could not find a part of the path … bin\roslyn\csc.exe`, попробуйте обновить пакет с помощью команды `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-134">If you receive an error like `Could not find a part of the path … bin\roslyn\csc.exe`, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="1cb0b-135">Для получения дополнительных сведений обратитесь [к этому вопросу в сайте StackOverflow](https://stackoverflow.com/questions/32780315) .</span><span class="sxs-lookup"><span data-stu-id="1cb0b-135">See [this question on StackOverflow](https://stackoverflow.com/questions/32780315) for additional details.</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="1cb0b-136">Размещение примера приложения</span><span class="sxs-lookup"><span data-stu-id="1cb0b-136">Host the sample app</span></span>

<span data-ttu-id="1cb0b-137">Помните, что приложения в Microsoft Teams представляют собой веб-приложения, которые предоставляют одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-137">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="1cb0b-138">Чтобы платформа Teams загружала приложение, ваше приложение должно быть достижимо из Интернета.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-138">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="1cb0b-139">Чтобы приложение было достижимо из Интернета, необходимо разместить приложение.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-139">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="1cb0b-140">Вы можете разместить его в Microsoft Azure бесплатно или создать туннель для локального процесса на вашем компьютере для разработки с помощью `ngrok`.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-140">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="1cb0b-141">После завершения хостинга приложения запишите его корневой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-141">When you finish hosting your app make a note of its root URL.</span></span> <span data-ttu-id="1cb0b-142">Он будет выглядеть примерно так: `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-142">It will look something like: `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="1cb0b-143">Туннелирование с помощью ngrok</span><span class="sxs-lookup"><span data-stu-id="1cb0b-143">Tunnel using ngrok</span></span>

<span data-ttu-id="1cb0b-144">Для быстрого тестирования можно запустить приложение на локальном компьютере и создать для него туннель через конечную точку веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-144">For quick testing you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="1cb0b-145">[ngrok](https://ngrok.com) — это бесплатный инструмент, который позволяет вам выполнить именно эту задачу.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-145">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="1cb0b-146">С помощью ngrok вы можете получить веб-адрес, `https://d0ac14a5.ngrok.io` например (этот URL-адрес — это только пример).</span><span class="sxs-lookup"><span data-stu-id="1cb0b-146">With ngrok you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="1cb0b-147">Вы можете [скачать и установить](https://ngrok.com/download) ngrok для своей среды.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-147">You can [download and install](https://ngrok.com/download) ngrok for your environment.</span></span> <span data-ttu-id="1cb0b-148">Убедитесь, что вы добавляете его в папку `PATH`.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-148">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="1cb0b-149">После установки можно открыть новое окно терминала и выполнить следующую команду для создания туннеля.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-149">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="1cb0b-150">В примере используется порт 3333, поэтому обязательно указывайте его здесь.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-150">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="1cb0b-151">Ngrok прослушивает запросы из Интернета и направляет их в ваше приложение, работающее на порте 3333.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-151">Ngrok will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="1cb0b-152">Вы можете проверить его, открыв браузер и перейдя `https://d0ac14a5.ngrok.io/hello` на страницу приветствия приложения.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-152">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="1cb0b-153">Обязательно используйте адрес пересылки, отображаемый в ngrok в сеансе консоли, а не этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-153">Please be sure to use the forwarding address displayed by ngrok in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="1cb0b-154">Если вы использовали другой порт в описанном выше шаге [Build and run](#build-and-run-the-sample) , убедитесь, что для установки `ngrok` туннеля используется тот же номер порта.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-154">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="1cb0b-155">Рекомендуется запустить `ngrok` в другом окне терминала, чтобы оно было запущено без конфликта с приложением, которое позднее потребуется остановить, перестроить и повторно запустить.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-155">It is a good idea to run `ngrok` in a different terminal window to keep it running without interfering with the app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="1cb0b-156">`ngrok` Сеанс возвратит полезную информацию об отладке в этом окне.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-156">The `ngrok` session will return useful debugging information in this window.</span></span>

<span data-ttu-id="1cb0b-157">Приложение будет доступно только в текущем сеансе на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-157">The app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="1cb0b-158">Если компьютер выключен или перейдет в спящий режим, служба станет недоступна.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-158">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="1cb0b-159">Помните об этом при совместном использовании приложения для тестирования другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-159">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="1cb0b-160">Если вам нужно перезапустить службу, она возвратит новый адрес, и вам потребуется обновить все место, где используется этот адрес.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-160">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span> <span data-ttu-id="1cb0b-161">Платная версия Ngrok не имеет этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-161">The paid version of Ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="1cb0b-162">Узел в Azure</span><span class="sxs-lookup"><span data-stu-id="1cb0b-162">Host in Azure</span></span>

<span data-ttu-id="1cb0b-163">Microsoft Azure позволяет размещать приложение .NET на свободном уровне с использованием общей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-163">Microsoft Azure lets you host your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="1cb0b-164">Это достаточно для запуска этого `Hello World` примера.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-164">This will be sufficient to run this `Hello World` sample.</span></span> <span data-ttu-id="1cb0b-165">Для получения дополнительных сведений ознакомьтесь со статьей [Создание новой бесплатной учетной записи](https://azure.microsoft.com/free/) .</span><span class="sxs-lookup"><span data-stu-id="1cb0b-165">See [creating a new free account](https://azure.microsoft.com/free/) for more information.</span></span>

<span data-ttu-id="1cb0b-166">В Visual Studio есть встроенная поддержка развертывания приложений для разных поставщиков, в том числе Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-166">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" src="~/assets/images/get-started/publishtoazure1.png" title="Visual Studio"/>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="1cb0b-168">Обновление учетных данных для размещаемого приложения</span><span class="sxs-lookup"><span data-stu-id="1cb0b-168">Update the credentials for your hosted app</span></span>

<span data-ttu-id="1cb0b-169">Для примера приложения требуются следующие переменные среды, чтобы задать значения, которые вы захотите заметку ранее.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-169">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="1cb0b-170">Откройте файл Web. config и найдите раздел *appSettings* .</span><span class="sxs-lookup"><span data-stu-id="1cb0b-170">Open up the web.config file and find the *appSettings* section.</span></span> <span data-ttu-id="1cb0b-171">Обновите значение *микрософтаппид* с помощью идентификатора ленты, сохраненного ранее.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-171">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="1cb0b-172">Обновите *микрософтапппассворд* с помощью сохраненного ранее пароля Bot.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-172">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" src="~/assets/images/get-started/get-started-net-azure-add-keys.png" title="Настройка ключей"/>

<span data-ttu-id="1cb0b-174">После внесения этих изменений Перестройте приложение.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-174">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="1cb0b-175">Если вы используете ngrok, запустите приложение локально и, если вы размещаете в Azure, повторно разверните приложение.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-175">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="1cb0b-176">Настройка вкладки "приложение"</span><span class="sxs-lookup"><span data-stu-id="1cb0b-176">Configure the app tab</span></span>

<span data-ttu-id="1cb0b-177">После установки приложения в команду его необходимо настроить для отображения контента.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-177">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="1cb0b-178">Перейдите к каналу в группе, где вы установили пример приложения, и нажмите кнопку **"+"** , чтобы добавить новую вкладку. Затем можно выбрать `Hello World` в списке **Добавить вкладку** .</span><span class="sxs-lookup"><span data-stu-id="1cb0b-178">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="1cb0b-179">После этого появится диалоговое окно настройки.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-179">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="1cb0b-180">Это диалоговое окно позволит выбрать вкладку для отображения в этом канале.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-180">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="1cb0b-181">После выбора вкладки и нажатия на `Save` эту вкладку вы увидите `Hello World` вкладку, загруженную с выбранной вкладкой.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-181">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" src="~/assets/images/samples-hello-world-tab-configure.png" title="Снимок экрана: Настройка" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="1cb0b-183">Тестирование ленты в Teams</span><span class="sxs-lookup"><span data-stu-id="1cb0b-183">Test your bot in Teams</span></span>

<span data-ttu-id="1cb0b-184">Теперь вы можете взаимодействовать с роботом в Teams.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-184">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="1cb0b-185">Выберите канал в группе, в которой вы зарегистрировали свое приложение, и `@your-bot-name`введите.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-185">Choose a channel in the team where you registered your app, and type `@your-bot-name`.</span></span> <span data-ttu-id="1cb0b-186">Это называется \*\* \@упоминанием\*\*.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-186">This is called an **\@mention**.</span></span> <span data-ttu-id="1cb0b-187">Любое сообщение, отправляемое в Bot, будет отправлено вам в качестве ответа.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-187">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" title="Ответы от Bot" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="1cb0b-189">Проверка расширения системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="1cb0b-189">Test your messaging extension</span></span>

<span data-ttu-id="1cb0b-190">Чтобы проверить расширение системы обмена сообщениями, щелкните три точки под полем ввода в представлении беседы.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-190">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="1cb0b-191">В меню появится приложение **"Hello World"** .</span><span class="sxs-lookup"><span data-stu-id="1cb0b-191">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="1cb0b-192">При нажатии на нее отображается множество случайных текстов на экране.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-192">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="1cb0b-193">Вы можете выбрать один из них и вставить его в беседу.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-193">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="530px" title="Меню расширения для обмена сообщениями" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" title="Результат расширения системы обмена сообщениями" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="1cb0b-196">Выберите один из случайных текстов, и вы увидите карту, отформатированную и готовую к отправке сообщения в нижней части.</span><span class="sxs-lookup"><span data-stu-id="1cb0b-196">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" title="Отправка расширения обмена сообщениями" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
