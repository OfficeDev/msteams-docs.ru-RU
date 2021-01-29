---
title: Учебник. Создание первого приложения с помощью Node.js
description: Узнайте, как начать создание приложений Microsoft Teams с помощью Node.js.
keywords: начало работы node.js nodejs App Studio
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 03dcf79a46266321e54c7e99bf01cdd2a87075fa
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037048"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a><span data-ttu-id="9db95-104">Создайте свое первое приложение Microsoft Teams с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="9db95-104">Create your first Microsoft Teams app using Node.js</span></span>

<span data-ttu-id="9db95-105">Это руководство поможет вам при создании приложения Microsoft Teams с помощью Node.js.</span><span class="sxs-lookup"><span data-stu-id="9db95-105">This tutorial helps you get started creating a Microsoft Teams app using Node.js.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="9db95-106">Скачивание и хостинг приложения</span><span class="sxs-lookup"><span data-stu-id="9db95-106">Download and host your app</span></span>

<span data-ttu-id="9db95-107">Выполните следующие действия, чтобы скачать и провести простое приложение "Hello world" в Teams.</span><span class="sxs-lookup"><span data-stu-id="9db95-107">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="9db95-108">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="9db95-108">Get prerequisites</span></span>

<span data-ttu-id="9db95-109">Для выполнения этого руководства необходимы следующие средства.</span><span class="sxs-lookup"><span data-stu-id="9db95-109">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="9db95-110">Если их еще нет, их можно установить по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="9db95-110">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="9db95-111">Git</span><span class="sxs-lookup"><span data-stu-id="9db95-111">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="9db95-112">Node.js и NPM</span><span class="sxs-lookup"><span data-stu-id="9db95-112">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="9db95-113">Получите любой текстовый редактор или IDE.</span><span class="sxs-lookup"><span data-stu-id="9db95-113">Get any text editor or IDE.</span></span> <span data-ttu-id="9db95-114">Вы можете установить и [использовать Visual Studio code](https://code.visualstudio.com/download) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="9db95-114">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="9db95-115">Если во время установки вы видите параметры для добавления `git` `node` , и `npm` `code` path, выберите это сделать.</span><span class="sxs-lookup"><span data-stu-id="9db95-115">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="9db95-116">Это будет удобно.</span><span class="sxs-lookup"><span data-stu-id="9db95-116">It will be handy.</span></span>

<span data-ttu-id="9db95-117">Убедитесь, что эти средства доступны, вы можете запускать следующие средства в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="9db95-117">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="9db95-118">Используйте окно терминала, наиболее удобное для вашей платформы.</span><span class="sxs-lookup"><span data-stu-id="9db95-118">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="9db95-119">В этих примерах используется Bash (включенный в Git), но эти сценарии будут работать на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="9db95-119">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 2.3.0
Local version 4.0.2
```

<span data-ttu-id="9db95-120">У вас может быть другая версия этих приложений.</span><span class="sxs-lookup"><span data-stu-id="9db95-120">You may have a different version of these applications.</span></span> <span data-ttu-id="9db95-121">Это не должно быть проблемой, за исключением gulp.</span><span class="sxs-lookup"><span data-stu-id="9db95-121">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="9db95-122">Для gulp необходимо использовать версию 4.0.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="9db95-122">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="9db95-123">Если вы не установили gulp (или у вас установлена неправильная версия), сделайте это сейчас, за `npm install gulp` запущенным в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="9db95-123">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="9db95-124">Если вы установили Visual Studio кода, вы можете проверить установку, вы можете:</span><span class="sxs-lookup"><span data-stu-id="9db95-124">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="9db95-125">Вы можете продолжать использовать это окно терминала для запуска команд, которые следуют в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="9db95-125">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="9db95-126">Скачать пример</span><span class="sxs-lookup"><span data-stu-id="9db95-126">Download the sample</span></span>

<span data-ttu-id="9db95-127">Мы предоставили простой [привет, мир!](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span><span class="sxs-lookup"><span data-stu-id="9db95-127">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span></span> <span data-ttu-id="9db95-128">пример для начала работы.</span><span class="sxs-lookup"><span data-stu-id="9db95-128">sample to get you started.</span></span> <span data-ttu-id="9db95-129">В окне терминала запустите следующую команду, чтобы клонировать образец репозитория на локальный компьютер:</span><span class="sxs-lookup"><span data-stu-id="9db95-129">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> <span data-ttu-id="9db95-130">Вы можете [раздвоить](https://help.github.com/articles/fork-a-repo/) этот репозиционный репозитарий, если хотите изменить и проверить изменения в репозитарии GitHub для дальнейшей ссылки. [](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span><span class="sxs-lookup"><span data-stu-id="9db95-130">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="9db95-131">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="9db95-131">Build and run the sample</span></span>

<span data-ttu-id="9db95-132">После клонирования репо перенаменуем в каталог, в который будет вмещаться пример:</span><span class="sxs-lookup"><span data-stu-id="9db95-132">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd msteams-samples-hello-world-nodejs
```

<span data-ttu-id="9db95-133">Чтобы создать пример, необходимо установить все его зависимости.</span><span class="sxs-lookup"><span data-stu-id="9db95-133">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="9db95-134">Для этого запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9db95-134">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="9db95-135">Вы увидите, что устанавливается множество зависимостей.</span><span class="sxs-lookup"><span data-stu-id="9db95-135">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="9db95-136">Завершив их, вы можете запустить приложение:</span><span class="sxs-lookup"><span data-stu-id="9db95-136">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="9db95-137">Когда приложение hello-world запускается, оно отображается `App started listening on port 3333` в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="9db95-137">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="9db95-138">Если в вышеуказанном сообщении отображается другой номер порта, это необходимо потому, что у вас установлена переменная среды PORT.</span><span class="sxs-lookup"><span data-stu-id="9db95-138">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="9db95-139">Вы можете продолжать использовать этот порт или изменить переменную среды на 3333.</span><span class="sxs-lookup"><span data-stu-id="9db95-139">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="9db95-140">На этом этапе можно открыть окно браузера и перейти по следующим URL-адресам, чтобы убедиться, что загружаются все URL-адреса приложений:</span><span class="sxs-lookup"><span data-stu-id="9db95-140">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="9db95-141">Хост-приложение для примера</span><span class="sxs-lookup"><span data-stu-id="9db95-141">Host the sample app</span></span>

<span data-ttu-id="9db95-142">Помните, что приложения в Microsoft Teams — это веб-приложения, которые предлагают одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="9db95-142">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="9db95-143">Чтобы платформа Teams загружала ваше приложение, ваше приложение должно быть доступно из Интернета.</span><span class="sxs-lookup"><span data-stu-id="9db95-143">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="9db95-144">Чтобы ваше приложение было доступно из Интернета, необходимо провести *его.*</span><span class="sxs-lookup"><span data-stu-id="9db95-144">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="9db95-145">Для локального тестирования можно запустить приложение на локальном компьютере и создать для него туннель с веб-конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="9db95-145">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="9db95-146">[ngrok](https://ngrok.com) — это бесплатное средство, которое позволяет сделать именно это.</span><span class="sxs-lookup"><span data-stu-id="9db95-146">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="9db95-147">С *помощью ngrok* можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` (этот URL-адрес является лишь примером).</span><span class="sxs-lookup"><span data-stu-id="9db95-147">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="9db95-148">Вы можете [скачать и установить](https://ngrok.com/download) *ngrok* для своей среды.</span><span class="sxs-lookup"><span data-stu-id="9db95-148">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="9db95-149">Убедитесь, что вы добавили его в расположение в вашем `PATH` .</span><span class="sxs-lookup"><span data-stu-id="9db95-149">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="9db95-150">После установки можно открыть новое окно терминала и выполнить следующую команду, чтобы создать туннель.</span><span class="sxs-lookup"><span data-stu-id="9db95-150">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="9db95-151">В примере используется порт 3333, поэтому не забудьте указать его здесь.</span><span class="sxs-lookup"><span data-stu-id="9db95-151">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="9db95-152">*Ngrok* будет прослушивать запросы из Интернета и маршрутит их в ваше приложение, запущенного через порт 3333.</span><span class="sxs-lookup"><span data-stu-id="9db95-152">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="9db95-153">Вы можете проверить, открыв браузер и загрузив страницу `https://d0ac14a5.ngrok.io/hello` hello приложения.</span><span class="sxs-lookup"><span data-stu-id="9db95-153">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="9db95-154">Вместо этого URL-адреса используйте адрес переадрикии, отображающийся *ngrok* в сеансе консоли.</span><span class="sxs-lookup"><span data-stu-id="9db95-154">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="9db95-155">Если вы использовали другой порт [](#build-and-run-the-sample) в сборке и на шаге выше, убедитесь, что для настройки туннеля *ngrok* используется один и тот же номер порта.</span><span class="sxs-lookup"><span data-stu-id="9db95-155">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="9db95-156">Лучше запустить *ngrok* в другом окне терминала, чтобы не мешать приложению узла, которое впоследствии может потребоваться остановить, перестроить и повторно запустить.</span><span class="sxs-lookup"><span data-stu-id="9db95-156">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="9db95-157">Сеанс *ngrok* возвращает полезные сведения об отладке в этом окне.</span><span class="sxs-lookup"><span data-stu-id="9db95-157">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="9db95-158">Существует платная версия *ngrok,* которая разрешает постоянные имена.</span><span class="sxs-lookup"><span data-stu-id="9db95-158">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="9db95-159">Если вы используете бесплатную версию, ваше приложение будет доступно только во время текущего сеанса на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="9db95-159">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="9db95-160">Если компьютер выключен или переводится в спящий режим, служба будет недоступна.</span><span class="sxs-lookup"><span data-stu-id="9db95-160">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="9db95-161">Помните об этом при совместном использовании приложения для тестирования другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="9db95-161">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="9db95-162">Если вам нужно перезапустить службу, она возвратит новый адрес, и вам придется обновить все места, где используется этот адрес.</span><span class="sxs-lookup"><span data-stu-id="9db95-162">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="9db95-163">Обратите внимание на URL-адрес приложения, так как он понадобится вам позже при регистрации приложения в Teams с помощью App studio.</span><span class="sxs-lookup"><span data-stu-id="9db95-163">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="9db95-164">Для этой цели хорошо работает Блокнот.</span><span class="sxs-lookup"><span data-stu-id="9db95-164">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="9db95-165">Развертывание приложения в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9db95-165">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="9db95-166">На этом этапе у вас есть приложение, которое находится в Интернете, но вы еще не можете сказать Teams, где его искать или даже что ваше приложение называется.</span><span class="sxs-lookup"><span data-stu-id="9db95-166">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="9db95-167">Для этого необходимо создать пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="9db95-167">To do this you now have to create an app package.</span></span> <span data-ttu-id="9db95-168">Это не более чем текстовый файл, содержащий манифест приложения и некоторые значки, которые клиент Teams будет использовать для правильного отображения и фирменой символики приложения.</span><span class="sxs-lookup"><span data-stu-id="9db95-168">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="9db95-169">Вы можете вручную создать этот пакет приложения или использовать App Studio— средство, которое работает в Teams, что упростит процесс регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="9db95-169">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="9db95-170">App Studio — это рекомендуемый способ создания и обновления пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="9db95-170">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="9db95-171">Для обоих методов вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="9db95-171">For either method you will need the following:</span></span>

- <span data-ttu-id="9db95-172">URL-адрес приложения в Интернете.</span><span class="sxs-lookup"><span data-stu-id="9db95-172">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="9db95-173">Значки, которые Teams будет использовать для фирменой символики вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="9db95-173">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="9db95-174">Пример поставляется со значками-замесятелями, расположенными в "src\static\images".</span><span class="sxs-lookup"><span data-stu-id="9db95-174">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="9db95-175">App Studio также предоставляет значки по умолчанию при необходимости.</span><span class="sxs-lookup"><span data-stu-id="9db95-175">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="9db95-176">Обновление ведущего приложения</span><span class="sxs-lookup"><span data-stu-id="9db95-176">Update your hosted app</span></span>

<span data-ttu-id="9db95-177">Пример приложения требует, чтобы для следующих переменных среды были установлены значения, которые вы ранее заметили.</span><span class="sxs-lookup"><span data-stu-id="9db95-177">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="9db95-178">То, как это сделать, зависит от того, как было организовано приложение.</span><span class="sxs-lookup"><span data-stu-id="9db95-178">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="9db95-179">Важно использовать переменные среды, так как эти значения являются частью вашей среды. К ним можно получить доступ с помощью кода вашего приложения, но они не будут доступны третьим лицам, которые могут изучить файлы, составляющие сайт.</span><span class="sxs-lookup"><span data-stu-id="9db95-179">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="9db95-180">Если вы используете приложение с помощью ngrok, вам потребуется настроить некоторые локальные переменные среды.</span><span class="sxs-lookup"><span data-stu-id="9db95-180">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="9db95-181">Это можно сделать множеством способов, но проще всего добавить конфигурацию запуска, если вы используете Visual Studio [Code:](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)</span><span class="sxs-lookup"><span data-stu-id="9db95-181">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

``` 
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

<span data-ttu-id="9db95-182">Где:</span><span class="sxs-lookup"><span data-stu-id="9db95-182">Where:</span></span>

<span data-ttu-id="9db95-183">MICROSOFT_APP_ID и MICROSOFT_APP_PASSWORD это ИД и пароль, соответственно, для вашего бота.</span><span class="sxs-lookup"><span data-stu-id="9db95-183">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="9db95-184">NODE_DEBUG покажите, что происходит в вашем боте в консоли Visual Studio отлаживка кода.</span><span class="sxs-lookup"><span data-stu-id="9db95-184">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="9db95-185">NODE_CONFIG_DIR указывает на каталог в корне репозитория (по умолчанию при локальном запуске приложения оно ищет его в папке src).</span><span class="sxs-lookup"><span data-stu-id="9db95-185">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="9db95-186">Если вы еще не остановили npm из предыдущего руководства, вам потребуется выполнить его, чтобы Visual Studio Code правильно подберет переменные конфигурации `npm stop` запуска.</span><span class="sxs-lookup"><span data-stu-id="9db95-186">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="9db95-187">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="9db95-187">Configure the app tab</span></span>

<span data-ttu-id="9db95-188">После установки приложения в команде необходимо настроить его для показа содержимого.</span><span class="sxs-lookup"><span data-stu-id="9db95-188">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="9db95-189">Перейдите на канал в команде и нажмите кнопку **"+",** чтобы добавить новую вкладку. Затем можно выбрать `Hello World` в списке **"Добавить** вкладку".</span><span class="sxs-lookup"><span data-stu-id="9db95-189">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="9db95-190">После этого вам будет представлено диалоговое окно конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9db95-190">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="9db95-191">Это диалоговое окно позволит выбрать вкладку, отображаемую в этом канале.</span><span class="sxs-lookup"><span data-stu-id="9db95-191">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="9db95-192">Выбрав вкладку и щелкнув ее, вы увидите вкладку, загруженную `Save` `Hello World` выбранной вкладками.</span><span class="sxs-lookup"><span data-stu-id="9db95-192">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" alt-text="Screenshot of configure" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="9db95-193">Тестирование бота в Teams</span><span class="sxs-lookup"><span data-stu-id="9db95-193">Test your bot in Teams</span></span>

<span data-ttu-id="9db95-194">Теперь вы можете взаимодействовать с ботом в Teams.</span><span class="sxs-lookup"><span data-stu-id="9db95-194">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="9db95-195">Выберите канал в команде, в которой вы зарегистрировали приложение, и введите `@your-bot-name` (за ним следует сообщение).</span><span class="sxs-lookup"><span data-stu-id="9db95-195">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="9db95-196">Это называется **\@ упоминанием.**</span><span class="sxs-lookup"><span data-stu-id="9db95-196">This is called an **\@mention**.</span></span> <span data-ttu-id="9db95-197">Все сообщения, отправляемые боту, будут отправлены вам в качестве ответа.</span><span class="sxs-lookup"><span data-stu-id="9db95-197">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt-text="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="9db95-198">Проверка расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9db95-198">Test your messaging extension</span></span>

<span data-ttu-id="9db95-199">Чтобы протестировать расширение обмена сообщениями, можно щелкнуть три точки под полем ввода в представлении беседы.</span><span class="sxs-lookup"><span data-stu-id="9db95-199">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="9db95-200">В меню будет всплывающее меню с приложением **"Hello World".**</span><span class="sxs-lookup"><span data-stu-id="9db95-200">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="9db95-201">Щелкнув его, вы увидите несколько произвольных текстов.</span><span class="sxs-lookup"><span data-stu-id="9db95-201">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="9db95-202">Вы можете выбрать любой из них, и он будет вставлен в беседу.</span><span class="sxs-lookup"><span data-stu-id="9db95-202">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="430px" alt-text="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt-text="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="9db95-203">Выберите один из случайных текстов, и внизу отформатированная карточка будет готова к отправке с собственным сообщением.</span><span class="sxs-lookup"><span data-stu-id="9db95-203">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="430px" alt-text="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
