---
title: Учебник . Создайте свое первое приложение с Node.js
description: Узнайте, как начать создание Microsoft Teams с помощью Node.js.
keywords: начало работы node.js nodejs App Studio
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: bbb2e50592eaa8a69a2cd9abda6a17ba2aa0e6bc
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114521"
---
# <a name="build-your-first-microsoft-teams-app-using-nodejs"></a><span data-ttu-id="1531c-104">Создайте первое Microsoft Teams с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="1531c-104">Build your first Microsoft Teams app using Node.js</span></span>

<span data-ttu-id="1531c-105">В этом руководстве вы узнаете, как создать свое первое приложение Microsoft Teams с помощью Node.js.</span><span class="sxs-lookup"><span data-stu-id="1531c-105">In this tutorial, you will learn how to build your very first Microsoft Teams app using Node.js.</span></span> <span data-ttu-id="1531c-106">Кроме того, вы проходите по шагам:</span><span class="sxs-lookup"><span data-stu-id="1531c-106">It also walks you through the steps to:</span></span> 

1. [<span data-ttu-id="1531c-107">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="1531c-107">Prepare your environment</span></span>](#prepare-environment)
1. [<span data-ttu-id="1531c-108">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="1531c-108">Get prerequisites</span></span>](#GetPrerequisites)
1. [<span data-ttu-id="1531c-109">Скачайте пример</span><span class="sxs-lookup"><span data-stu-id="1531c-109">Download the sample</span></span>](#DownloadSample)
1. [<span data-ttu-id="1531c-110">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="1531c-110">Build and run the sample</span></span>](#BuildRun)
1. [<span data-ttu-id="1531c-111">Хост пример приложения</span><span class="sxs-lookup"><span data-stu-id="1531c-111">Host the sample app</span></span>](#HostSample)
1. [<span data-ttu-id="1531c-112">Обновление учетных данных для вашего хозяйского приложения</span><span class="sxs-lookup"><span data-stu-id="1531c-112">Update the credentials for your hosted app</span></span>](#updatecredentials)
1. [<span data-ttu-id="1531c-113">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="1531c-113">Configure the app tab</span></span>](#ConfigureTheAppTab)

<a name="prepare-environment"></a>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

### <a name="download-and-host-your-app"></a><span data-ttu-id="1531c-114">Загрузка и хост-сайт приложения</span><span class="sxs-lookup"><span data-stu-id="1531c-114">Download and host your app</span></span>

<span data-ttu-id="1531c-115">Выполните следующие действия, чтобы скачать и провести простое приложение "Hello World" в Teams.</span><span class="sxs-lookup"><span data-stu-id="1531c-115">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="1531c-116">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="1531c-116">Get prerequisites</span></span>

<span data-ttu-id="1531c-117">Для завершения этого руководства необходимы следующие средства.</span><span class="sxs-lookup"><span data-stu-id="1531c-117">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="1531c-118">Если их еще нет, их можно установить по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="1531c-118">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="1531c-119">Git</span><span class="sxs-lookup"><span data-stu-id="1531c-119">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="1531c-120">Node.js и NPM</span><span class="sxs-lookup"><span data-stu-id="1531c-120">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="1531c-121">Получите любой текстовый редактор или IDE.</span><span class="sxs-lookup"><span data-stu-id="1531c-121">Get any text editor or IDE.</span></span> <span data-ttu-id="1531c-122">Вы можете установить и [использовать Visual Studio Code](https://code.visualstudio.com/download) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="1531c-122">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="1531c-123">Если вы видите варианты добавления , и path во время `git` `node` `npm` `code` установки, выберите параметры.</span><span class="sxs-lookup"><span data-stu-id="1531c-123">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, select the options.</span></span> 

<span data-ttu-id="1531c-124">Убедитесь, что эти средства доступны, запуская следующие средства в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="1531c-124">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="1531c-125">Используйте окно терминала, которое наиболее удобно для вашей платформы.</span><span class="sxs-lookup"><span data-stu-id="1531c-125">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="1531c-126">В этих примерах используется Bash (который входит в Git), но эти скрипты будут работать на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="1531c-126">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

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

<span data-ttu-id="1531c-127">У вас может быть другая версия этих приложений.</span><span class="sxs-lookup"><span data-stu-id="1531c-127">You may have a different version of these applications.</span></span> <span data-ttu-id="1531c-128">Это не должно быть проблемой, за исключением глотка.</span><span class="sxs-lookup"><span data-stu-id="1531c-128">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="1531c-129">Для глотка необходимо использовать версию 4.0.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1531c-129">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="1531c-130">Если у вас не установлена глоток (или установлена неправильная версия), делайте это сейчас, запуская `npm install gulp` в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="1531c-130">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="1531c-131">Если установлена Visual Studio Code, вы можете проверить установку при запуске:</span><span class="sxs-lookup"><span data-stu-id="1531c-131">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="1531c-132">Вы можете продолжать использовать это окно терминала для запуска команд, которые следуют в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="1531c-132">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="1531c-133">Скачайте пример</span><span class="sxs-lookup"><span data-stu-id="1531c-133">Download the sample</span></span>

<span data-ttu-id="1531c-134">Мы предоставили простой [привет, мир!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span><span class="sxs-lookup"><span data-stu-id="1531c-134">We have provided a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span></span> <span data-ttu-id="1531c-135">пример, чтобы вы начали.</span><span class="sxs-lookup"><span data-stu-id="1531c-135">sample to get you started.</span></span> <span data-ttu-id="1531c-136">В окне терминала запустите следующую команду, чтобы клонировать репозиторий образца на локальной машине:</span><span class="sxs-lookup"><span data-stu-id="1531c-136">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="1531c-137">Вы можете [вилка](https://help.github.com/articles/fork-a-repo/) этого [репо,](https://github.com/OfficeDev/Microsoft-Teams-Samples) если вы хотите изменить и проверить изменения в вашем GitHub для будущей ссылки.</span><span class="sxs-lookup"><span data-stu-id="1531c-137">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="1531c-138">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="1531c-138">Build and run the sample</span></span>

<span data-ttu-id="1531c-139">После клонирования репозитория запустите команду каталога изменений в терминале, чтобы изменить каталог на пример:</span><span class="sxs-lookup"><span data-stu-id="1531c-139">After the repository is cloned, run the change directory command in terminal to change the directory to the sample:</span></span>

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

<span data-ttu-id="1531c-140">Чтобы создать образец, необходимо установить все его зависимости.</span><span class="sxs-lookup"><span data-stu-id="1531c-140">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="1531c-141">Для этого запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1531c-141">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="1531c-142">Необходимо увидеть, как устанавливается куча зависимостей.</span><span class="sxs-lookup"><span data-stu-id="1531c-142">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="1531c-143">После установки вы можете запустить приложение со следующей командой:</span><span class="sxs-lookup"><span data-stu-id="1531c-143">After installation you can run the app with the following command:</span></span>

```bash
npm start
```

<span data-ttu-id="1531c-144">Когда приложение hello-world запускается, оно отображается `App started listening on port 3333` в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="1531c-144">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="1531c-145">Если в вышеуказанном сообщении отображается другой номер порта, это потому, что у вас есть переменная среды ПОРТ.</span><span class="sxs-lookup"><span data-stu-id="1531c-145">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="1531c-146">Вы можете продолжать использовать этот порт или изменить переменную среды на 3333.</span><span class="sxs-lookup"><span data-stu-id="1531c-146">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="1531c-147">На этом этапе можно открыть окно браузера и перейти к следующим URL-адресам, чтобы убедиться, что все URL-адреса приложений загружаются:</span><span class="sxs-lookup"><span data-stu-id="1531c-147">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

## <a name="deploy-your-sample-app"></a><span data-ttu-id="1531c-148">Развертывание примера приложения</span><span class="sxs-lookup"><span data-stu-id="1531c-148">Deploy your sample app</span></span>

<span data-ttu-id="1531c-149">Помните, что приложения в Microsoft Teams являются веб-приложениями, которые обнажают одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="1531c-149">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="1531c-150">Чтобы платформа Teams загрузить приложение, ваше приложение должно быть доступно из Интернета.</span><span class="sxs-lookup"><span data-stu-id="1531c-150">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="1531c-151">Чтобы сделать ваше приложение доступно из Интернета, необходимо *провести* ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="1531c-151">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="1531c-152">Для локального тестирования можно запустить приложение на локальной машине и создать туннель к ней с помощью веб-конечной точки.</span><span class="sxs-lookup"><span data-stu-id="1531c-152">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="1531c-153">[ngrok](https://ngrok.com) — это бесплатный инструмент, который позволяет делать именно это.</span><span class="sxs-lookup"><span data-stu-id="1531c-153">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="1531c-154">С *помощью ngrok* вы можете получить такой веб-адрес, как `https://d0ac14a5.ngrok.io` (этот URL-адрес — только пример).</span><span class="sxs-lookup"><span data-stu-id="1531c-154">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="1531c-155">Вы можете [скачать и установить](https://ngrok.com/download) *ngrok для* вашей среды.</span><span class="sxs-lookup"><span data-stu-id="1531c-155">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="1531c-156">Убедитесь, что вы добавляете его в расположение в вашем `PATH` .</span><span class="sxs-lookup"><span data-stu-id="1531c-156">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="1531c-157">После установки можно открыть новое окно терминала и запустить следующую команду для создания туннеля.</span><span class="sxs-lookup"><span data-stu-id="1531c-157">After you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="1531c-158">В примере используется порт 3333, поэтому не забудьте указать его здесь:</span><span class="sxs-lookup"><span data-stu-id="1531c-158">The sample uses port 3333, so be sure to specify it here:</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="1531c-159">*Ngrok* будет прослушивать запросы из Интернета и перенанастрает их в приложение, которое работает в порту 3333.</span><span class="sxs-lookup"><span data-stu-id="1531c-159">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="1531c-160">Вы можете проверить, открыв браузер и загрузив страницу `https://d0ac14a5.ngrok.io/hello` привета приложения.</span><span class="sxs-lookup"><span data-stu-id="1531c-160">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="1531c-161">Не забудьте использовать адрес переададки, *отображающийся ngrok* в сеансе консоли, а не этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="1531c-161">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="1531c-162">Если вы использовали другой порт [](#build-and-run-the-sample) в сборке и на шаге выше, убедитесь, что для установки туннеля *ngrok* используется один и тот же номер порта.</span><span class="sxs-lookup"><span data-stu-id="1531c-162">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="1531c-163">Неплохо запустить *ngrok* в другом окне терминала, чтобы не мешать приложению узла, которое впоследствии может быть необходимо остановить, перестроить и повторно запустить.</span><span class="sxs-lookup"><span data-stu-id="1531c-163">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="1531c-164">Сеанс *ngrok* возвращает полезную информацию об отладке в этом окне.</span><span class="sxs-lookup"><span data-stu-id="1531c-164">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="1531c-165">Существует платная версия *ngrok,* которая позволяет настойчивые имена.</span><span class="sxs-lookup"><span data-stu-id="1531c-165">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="1531c-166">Если вы используете бесплатную версию, приложение будет доступно только во время текущего сеанса на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="1531c-166">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="1531c-167">Если машина отключена или переходит в спящий режим, служба больше не будет доступна.</span><span class="sxs-lookup"><span data-stu-id="1531c-167">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="1531c-168">Помните об этом при совместном использовании приложения для тестирования другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="1531c-168">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="1531c-169">Если вам придется перезапустить службу, она возвращает новый адрес, и вам придется обновить каждое место, которое использует этот адрес.</span><span class="sxs-lookup"><span data-stu-id="1531c-169">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="1531c-170">Обратите внимание на URL-адрес вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="1531c-170">Make a note of the URL of your app.</span></span> <span data-ttu-id="1531c-171">Это потребуется позже, когда вы зарегистрируете приложение Teams с помощью студии приложения или портала разработчиков.</span><span class="sxs-lookup"><span data-stu-id="1531c-171">You will need this later when you register the app with Teams using App studio or Developer Portal.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="1531c-172">Развертывание приложения для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1531c-172">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="1531c-173">На данный момент у вас есть приложение, которое находится в Интернете, но вы еще не можете сказать Teams, где его искать, или даже то, что ваше приложение называется.</span><span class="sxs-lookup"><span data-stu-id="1531c-173">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="1531c-174">Для этого необходимо создать пакет приложений.</span><span class="sxs-lookup"><span data-stu-id="1531c-174">To do this you now have to create an app package.</span></span> <span data-ttu-id="1531c-175">Это не более чем текстовый файл, содержащий манифест приложения и некоторые значки, которые Teams клиент будет использовать для правильного отображения и брендинга приложения.</span><span class="sxs-lookup"><span data-stu-id="1531c-175">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="1531c-176">Вы можете вручную создать этот пакет приложений или использовать App Studio или Портал разработчиков, инструменты, которые работают в Teams, что упростит процесс регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="1531c-176">You can manually create this app package, or you can use App Studio or Developer Portal, tools that run in Teams, that will simplify the process of registering the app.</span></span> <span data-ttu-id="1531c-177">App Studio и Портал разработчиков — это рекомендуемые способы создания и обновления пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="1531c-177">App Studio and Developer Portal are the recommended ways of creating and updating the app package.</span></span>

<span data-ttu-id="1531c-178">Для любого метода потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="1531c-178">For either method you will need the following:</span></span>

- <span data-ttu-id="1531c-179">URL-адрес, на котором ваше приложение можно найти в Интернете.</span><span class="sxs-lookup"><span data-stu-id="1531c-179">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="1531c-180">Значки, Teams будут использовать для брендинга приложения.</span><span class="sxs-lookup"><span data-stu-id="1531c-180">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="1531c-181">Пример поставляется с значками-местообнаружителями, расположенными в "src\static\images".</span><span class="sxs-lookup"><span data-stu-id="1531c-181">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="1531c-182">App Studio также будет предоставлять значки по умолчанию, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="1531c-182">App Studio also will provide default icons if needed.</span></span>

<span data-ttu-id="1531c-183">**Обновление пакета приложений**</span><span class="sxs-lookup"><span data-stu-id="1531c-183">**Update the app package**</span></span>

# <a name="app-studio"></a>[<span data-ttu-id="1531c-184">App Studio</span><span class="sxs-lookup"><span data-stu-id="1531c-184">App Studio</span></span>](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[<span data-ttu-id="1531c-185">Портал разработчика</span><span class="sxs-lookup"><span data-stu-id="1531c-185">Developer Portal</span></span>](#tab/DP)

<span data-ttu-id="1531c-186">**Установка портала разработчиков (предварительный просмотр) в Teams**</span><span class="sxs-lookup"><span data-stu-id="1531c-186">**To install Developer Portal (preview) in Teams**</span></span>

1. <span data-ttu-id="1531c-187">Выберите **значок Apps** в нижней части левой панели и поиск **портала разработчиков.**</span><span class="sxs-lookup"><span data-stu-id="1531c-187">Select the **Apps** icon at the bottom of the left-hand bar, and search for **Developer Portal**.</span></span>

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. <span data-ttu-id="1531c-188">Выберите **портал разработчика** и выберите **Open**.</span><span class="sxs-lookup"><span data-stu-id="1531c-188">Select **Developer Portal** and select **Open**.</span></span>

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. <span data-ttu-id="1531c-189">Выберите вкладку Apps и **выберите Импорт существующего приложения.**</span><span class="sxs-lookup"><span data-stu-id="1531c-189">Select the Apps tab and select **Import an existing app**.</span></span>

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. <span data-ttu-id="1531c-190">Выберите **Hello World** и выберите **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="1531c-190">Select **Hello World** and select **Import**.</span></span> <span data-ttu-id="1531c-191">Приложение **Hello World** импортируется на портале разработчиков.</span><span class="sxs-lookup"><span data-stu-id="1531c-191">The **Hello World** app is imported in Developer Portal.</span></span> 

    <span data-ttu-id="1531c-192">Вы можете настроить приложение с помощью портала Teams разработчика.</span><span class="sxs-lookup"><span data-stu-id="1531c-192">You can configure your app using the Teams Developer Portal.</span></span> <span data-ttu-id="1531c-193">Манифест находится в статье Распределить.</span><span class="sxs-lookup"><span data-stu-id="1531c-193">The Manifest is found under Distribute.</span></span> <span data-ttu-id="1531c-194">Манифест можно использовать для настройки возможностей, необходимых ресурсов и других важных атрибутов для приложения.</span><span class="sxs-lookup"><span data-stu-id="1531c-194">You can use the Manifest to configure capabilities, required resources, and other important attributes for your app.</span></span> <span data-ttu-id="1531c-195">Дополнительные сведения о настройке приложения с помощью портала разработчиков см. в Teams [портале разработчиков.](../concepts/build-and-test/teams-developer-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1531c-195">For more details on how to configure your app using Developer Portal, see [Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).</span></span>

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>

---
<a name="updatecredentials"></a>

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="1531c-196">Обновление учетных данных для вашего хозяйского приложения</span><span class="sxs-lookup"><span data-stu-id="1531c-196">Update the credentials for your hosted app</span></span>

<span data-ttu-id="1531c-197">Пример приложения требует, чтобы следующие переменные среды были задаты значениям, которые вы сделали ранее:</span><span class="sxs-lookup"><span data-stu-id="1531c-197">The sample app requires the following environment variables to be set to the values you made a note of earlier:</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="1531c-198">То, как это сделать, зависит от того, как вы хозяйили приложение.</span><span class="sxs-lookup"><span data-stu-id="1531c-198">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="1531c-199">Важное значение в использовании переменных среды в том, что эти значения являются частью вашей среды : к ним можно получить доступ с помощью кода для вашего приложения, но они не подвергаются воздействию третьих лиц, которые могут изучить файлы, составляющие ваш сайт.</span><span class="sxs-lookup"><span data-stu-id="1531c-199">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="1531c-200">Если вы используете приложение с помощью ngrok, вам потребуется настроить некоторые локальные переменные среды.</span><span class="sxs-lookup"><span data-stu-id="1531c-200">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="1531c-201">Существует множество способов, но проще всего, если вы используете Visual Studio Code, добавить конфигурацию [запуска:](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)</span><span class="sxs-lookup"><span data-stu-id="1531c-201">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

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

<span data-ttu-id="1531c-202">Где:</span><span class="sxs-lookup"><span data-stu-id="1531c-202">Where:</span></span>

<span data-ttu-id="1531c-203">MICROSOFT_APP_ID и MICROSOFT_APP_PASSWORD является ID и пароль, соответственно, для вашего бота.</span><span class="sxs-lookup"><span data-stu-id="1531c-203">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="1531c-204">NODE_DEBUG покажите, что происходит в боте в консоли Visual Studio Code отлаживке.</span><span class="sxs-lookup"><span data-stu-id="1531c-204">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="1531c-205">NODE_CONFIG_DIR указывает на каталог в корне репозитория (по умолчанию при локальном запуске приложения он ищет его в папке SRC).</span><span class="sxs-lookup"><span data-stu-id="1531c-205">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="1531c-206">Если вы не остановили npm из более ранней в учебнике, вам потребуется выполнить, чтобы Visual Studio Code правильно подобрать переменные конфигурации `npm stop` запуска.</span><span class="sxs-lookup"><span data-stu-id="1531c-206">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="1531c-207">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="1531c-207">Configure the app tab</span></span>

<span data-ttu-id="1531c-208">После установки приложения в команду необходимо настроить его для демонстрации контента.</span><span class="sxs-lookup"><span data-stu-id="1531c-208">After you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="1531c-209">Перейдите к каналу в команде и нажмите кнопку **"+",** чтобы добавить новую вкладку. Затем можно выбрать `Hello World` из списка **Добавить вкладку.**</span><span class="sxs-lookup"><span data-stu-id="1531c-209">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="1531c-210">Затем вам будет представлен диалоговое окно конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1531c-210">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="1531c-211">Этот диалоговое окно позволит выбрать вкладку, которая будет отображаться в этом канале.</span><span class="sxs-lookup"><span data-stu-id="1531c-211">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="1531c-212">После выбора вкладки и нажмите **кнопку Сохранить,** вы увидите вкладку, загруженную `Hello World` выбранной вкладками:</span><span class="sxs-lookup"><span data-stu-id="1531c-212">After you select the tab and click **Save** you can see the `Hello World` tab loaded with the tab you chose:</span></span>

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="1531c-213">Проверьте бот в Teams</span><span class="sxs-lookup"><span data-stu-id="1531c-213">Test your bot in Teams</span></span>

<span data-ttu-id="1531c-214">Теперь вы можете взаимодействовать с ботом в Teams.</span><span class="sxs-lookup"><span data-stu-id="1531c-214">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="1531c-215">Выберите канал в команде, в которой вы зарегистрировали приложение, и введите, а затем `@your-bot-name` ваше сообщение.</span><span class="sxs-lookup"><span data-stu-id="1531c-215">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="1531c-216">Это называется **\@ упоминанием**.</span><span class="sxs-lookup"><span data-stu-id="1531c-216">This is called an **\@mention**.</span></span> <span data-ttu-id="1531c-217">Любое сообщение, отправленное боту, будет отправлено вам в качестве ответа:</span><span class="sxs-lookup"><span data-stu-id="1531c-217">Whatever message you send to the bot will be sent back to you as a reply:</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="1531c-218">Тестирование расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="1531c-218">Test your messaging extension</span></span>

<span data-ttu-id="1531c-219">Чтобы проверить расширение обмена сообщениями, вы можете щелкнуть три точки ниже входного окна в представлении беседы.</span><span class="sxs-lookup"><span data-stu-id="1531c-219">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="1531c-220">В нем всплывет меню с приложением **"Hello World".**</span><span class="sxs-lookup"><span data-stu-id="1531c-220">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="1531c-221">При нажатии на него вы увидите несколько случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="1531c-221">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="1531c-222">Вы можете выбрать любой из них, и он будет вставлен в ваш разговор:</span><span class="sxs-lookup"><span data-stu-id="1531c-222">You can choose any one of them and it will be inserted it into your conversation:</span></span>

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

<span data-ttu-id="1531c-223">Выберите один из случайных текстов, и в нижней части вы увидите карту, отформатированную и готовую к отправке с собственным сообщением:</span><span class="sxs-lookup"><span data-stu-id="1531c-223">Select one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom:</span></span>

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

 ## <a name="see-also"></a><span data-ttu-id="1531c-224">См. также</span><span class="sxs-lookup"><span data-stu-id="1531c-224">See also</span></span>

* [<span data-ttu-id="1531c-225">Обзор учебников</span><span class="sxs-lookup"><span data-stu-id="1531c-225">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="1531c-226">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="1531c-226">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)