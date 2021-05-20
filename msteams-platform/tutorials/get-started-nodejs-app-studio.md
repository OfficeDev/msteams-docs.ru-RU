---
title: Учебник - Создайте свое первое приложение с помощью Node.js
description: Узнайте, как начать строить Microsoft Teams приложения с Node.js.
keywords: начало работы node.js nodejs App Studio
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 46272671443e07432513b667af424b5c5be05f2e
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566544"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a><span data-ttu-id="12d4e-104">Создайте свое первое Microsoft Teams приложение с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="12d4e-104">Create your first Microsoft Teams app using Node.js</span></span>

<span data-ttu-id="12d4e-105">Этот учебник поможет вам начать создавать приложение Microsoft Teams с помощью Node.js.</span><span class="sxs-lookup"><span data-stu-id="12d4e-105">This tutorial helps you get started creating a Microsoft Teams app using Node.js.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="12d4e-106">Загрузка и хост приложения</span><span class="sxs-lookup"><span data-stu-id="12d4e-106">Download and host your app</span></span>

<span data-ttu-id="12d4e-107">Следуйте этим шагам, чтобы загрузить и разместить простое приложение "привет миру" Teams.</span><span class="sxs-lookup"><span data-stu-id="12d4e-107">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="12d4e-108">Получить предпосылки</span><span class="sxs-lookup"><span data-stu-id="12d4e-108">Get prerequisites</span></span>

<span data-ttu-id="12d4e-109">Чтобы завершить этот учебник, вам нужны следующие инструменты.</span><span class="sxs-lookup"><span data-stu-id="12d4e-109">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="12d4e-110">Если у вас их еще нет, вы можете установить их по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="12d4e-110">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="12d4e-111">Git</span><span class="sxs-lookup"><span data-stu-id="12d4e-111">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="12d4e-112">Node.js и NPM</span><span class="sxs-lookup"><span data-stu-id="12d4e-112">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="12d4e-113">Получите любой текстовый редактор или IDE.</span><span class="sxs-lookup"><span data-stu-id="12d4e-113">Get any text editor or IDE.</span></span> <span data-ttu-id="12d4e-114">Вы можете установить и [использовать Visual Studio Code](https://code.visualstudio.com/download) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="12d4e-114">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="12d4e-115">Если вы видите `git` `node` варианты, чтобы добавить , , и PATH во время `npm` `code` установки, решили сделать это.</span><span class="sxs-lookup"><span data-stu-id="12d4e-115">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="12d4e-116">Это будет удобно.</span><span class="sxs-lookup"><span data-stu-id="12d4e-116">It will be handy.</span></span>

<span data-ttu-id="12d4e-117">Убедитесь, что инструменты доступны, выехав в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="12d4e-117">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="12d4e-118">Используйте окно терминала, которое вам больше всего удобно на платформе.</span><span class="sxs-lookup"><span data-stu-id="12d4e-118">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="12d4e-119">В этих примерах используется Bash (который включен в Git), но эти скрипты будут работать на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="12d4e-119">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

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

<span data-ttu-id="12d4e-120">У вас может быть другая версия этих приложений.</span><span class="sxs-lookup"><span data-stu-id="12d4e-120">You may have a different version of these applications.</span></span> <span data-ttu-id="12d4e-121">Это не должно быть проблемой, за исключением глотка.</span><span class="sxs-lookup"><span data-stu-id="12d4e-121">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="12d4e-122">Для глотка вам нужно будет использовать версию 4.0.0 или позже.</span><span class="sxs-lookup"><span data-stu-id="12d4e-122">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="12d4e-123">Если у вас нет установленного глотка (или установлена неправильная версия), сделайте это сейчас, `npm install gulp` заев в окно терминала.</span><span class="sxs-lookup"><span data-stu-id="12d4e-123">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="12d4e-124">Если вы установили Visual Studio Code, вы можете проверить установку, вытехав:</span><span class="sxs-lookup"><span data-stu-id="12d4e-124">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="12d4e-125">Вы можете продолжать использовать это окно терминала для запуска команд, которые следуют в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="12d4e-125">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="12d4e-126">Скачать образец</span><span class="sxs-lookup"><span data-stu-id="12d4e-126">Download the sample</span></span>

<span data-ttu-id="12d4e-127">Мы предоставили простой [Привет, Мир!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span><span class="sxs-lookup"><span data-stu-id="12d4e-127">We have provided a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span></span> <span data-ttu-id="12d4e-128">образец, чтобы вы начали.</span><span class="sxs-lookup"><span data-stu-id="12d4e-128">sample to get you started.</span></span> <span data-ttu-id="12d4e-129">В окне терминала запустите следующую команду клонировать репозиторий образца локальной машины:</span><span class="sxs-lookup"><span data-stu-id="12d4e-129">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="12d4e-130">Вы можете [раскошелиться](https://help.github.com/articles/fork-a-repo/) на [это репо,](https://github.com/OfficeDev/Microsoft-Teams-Samples) если вы хотите изменить и проверить свои изменения в GitHub репо для будущей ссылки.</span><span class="sxs-lookup"><span data-stu-id="12d4e-130">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="12d4e-131">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="12d4e-131">Build and run the sample</span></span>

<span data-ttu-id="12d4e-132">После клонирования репо измените каталог, в который хранится образец:</span><span class="sxs-lookup"><span data-stu-id="12d4e-132">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

<span data-ttu-id="12d4e-133">Для создания образца необходимо установить все его зависимости.</span><span class="sxs-lookup"><span data-stu-id="12d4e-133">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="12d4e-134">Вы запустите следующую команду, чтобы сделать это:</span><span class="sxs-lookup"><span data-stu-id="12d4e-134">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="12d4e-135">Вы должны увидеть кучу зависимостей получить установлен.</span><span class="sxs-lookup"><span data-stu-id="12d4e-135">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="12d4e-136">Как только они будут закончены, вы можете запустить приложение:</span><span class="sxs-lookup"><span data-stu-id="12d4e-136">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="12d4e-137">Когда начинается приложение hello-world, оно `App started listening on port 3333` отображается в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="12d4e-137">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="12d4e-138">Если вы видите другой номер порта, отображаемый в сообщении выше, это потому, что у вас есть переменный набор среды PORT.</span><span class="sxs-lookup"><span data-stu-id="12d4e-138">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="12d4e-139">Вы можете продолжать использовать этот порт или изменять переменную среды до 3333.</span><span class="sxs-lookup"><span data-stu-id="12d4e-139">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="12d4e-140">На этом этапе можно открыть окно браузера и перейти к следующим URL-адресам, чтобы убедиться, что все URL-адреса приложений загружаются:</span><span class="sxs-lookup"><span data-stu-id="12d4e-140">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="12d4e-141">Хозяин образца приложения</span><span class="sxs-lookup"><span data-stu-id="12d4e-141">Host the sample app</span></span>

<span data-ttu-id="12d4e-142">Помните, что приложения Microsoft Teams веб-приложений подвергая одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="12d4e-142">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="12d4e-143">Для Teams платформы для загрузки приложения приложение должно быть доступно из Интернета.</span><span class="sxs-lookup"><span data-stu-id="12d4e-143">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="12d4e-144">Чтобы сделать приложение доступно из Интернета, необходимо разместить *приложение.*</span><span class="sxs-lookup"><span data-stu-id="12d4e-144">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="12d4e-145">Для локального тестирования вы можете запустить приложение на локальной машине и создать туннель к нему с веб-конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="12d4e-145">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="12d4e-146">[ngrok](https://ngrok.com) это бесплатный инструмент, который позволяет делать именно это.</span><span class="sxs-lookup"><span data-stu-id="12d4e-146">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="12d4e-147">С *ngrok вы* можете получить веб-адрес, такой как `https://d0ac14a5.ngrok.io` (этот URL является лишь примером).</span><span class="sxs-lookup"><span data-stu-id="12d4e-147">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="12d4e-148">Вы можете [скачать и установить](https://ngrok.com/download) *ngrok для* вашей среды.</span><span class="sxs-lookup"><span data-stu-id="12d4e-148">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="12d4e-149">Убедитесь, что вы добавляете его в место в `PATH` вашем .</span><span class="sxs-lookup"><span data-stu-id="12d4e-149">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="12d4e-150">После установки можно открыть новое окно терминала и вы запустить следующую команду для создания туннеля.</span><span class="sxs-lookup"><span data-stu-id="12d4e-150">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="12d4e-151">Образец использует порт 3333, поэтому не забудьте указать его здесь:</span><span class="sxs-lookup"><span data-stu-id="12d4e-151">The sample uses port 3333, so be sure to specify it here:</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="12d4e-152">*Ngrok* будет слушать запросы из Интернета и будет маршрут их к вашему приложению работает на порт 3333.</span><span class="sxs-lookup"><span data-stu-id="12d4e-152">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="12d4e-153">Вы можете проверить, открыв браузер и `https://d0ac14a5.ngrok.io/hello` загрузив страницу привет вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="12d4e-153">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="12d4e-154">Пожалуйста, не забудьте использовать адрес переголовки, *отображаемый ngrok* в сеансе консоли, а не этот URL.</span><span class="sxs-lookup"><span data-stu-id="12d4e-154">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="12d4e-155">Если вы использовали другой порт в [сборке и запустить шаг](#build-and-run-the-sample) выше, убедитесь, что вы используете тот же номер порта для *установки туннеля ngrok.*</span><span class="sxs-lookup"><span data-stu-id="12d4e-155">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="12d4e-156">Это хорошая идея, чтобы запустить *ngrok в* другом окне терминала, чтобы держать его работает, не мешая с приложением узла, который вы, возможно, позже придется остановить, восстановить и повторно запустить.</span><span class="sxs-lookup"><span data-stu-id="12d4e-156">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="12d4e-157">Сеанс *ngrok вернет* полезную информацию об отладке в этом окне.</span><span class="sxs-lookup"><span data-stu-id="12d4e-157">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="12d4e-158">Существует платная версия *ngrok, которая* позволяет стойкие имена.</span><span class="sxs-lookup"><span data-stu-id="12d4e-158">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="12d4e-159">Если вы используете бесплатную версию, ваше приложение будет доступно только во время текущей сессии на вашей машине разработки.</span><span class="sxs-lookup"><span data-stu-id="12d4e-159">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="12d4e-160">Если машина выключена или засыпает, служба больше не будет доступна.</span><span class="sxs-lookup"><span data-stu-id="12d4e-160">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="12d4e-161">Помните об этом при совместном использовании приложения для тестирования другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="12d4e-161">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="12d4e-162">Если вам придется перезапустить службу он вернет новый адрес, и вам придется обновить каждое место, которое использует этот адрес.</span><span class="sxs-lookup"><span data-stu-id="12d4e-162">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="12d4e-163">Помните, обратите внимание на URL вашего приложения, потому что вам понадобится это позже, когда вы регистрируете приложение с Teams с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="12d4e-163">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="12d4e-164">Блокнот прекрасно работает для этой цели.</span><span class="sxs-lookup"><span data-stu-id="12d4e-164">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="12d4e-165">Развертывайте приложение для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="12d4e-165">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="12d4e-166">На данный момент у вас есть приложение, размещено в Интернете, но у вас нет еще способа сказать Teams, где его искать, или даже то, что ваше приложение называется.</span><span class="sxs-lookup"><span data-stu-id="12d4e-166">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="12d4e-167">Для этого теперь вам придется создать пакет приложений.</span><span class="sxs-lookup"><span data-stu-id="12d4e-167">To do this you now have to create an app package.</span></span> <span data-ttu-id="12d4e-168">Это немного больше, чем текстовый файл, который содержит манифест приложения и некоторые значки, которые Teams клиент будет использовать для правильного отображения и бренд вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="12d4e-168">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="12d4e-169">Вы можете вручную создать этот пакет приложений, или вы можете использовать App Studio, инструмент, который работает Teams, который упростит процесс регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="12d4e-169">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="12d4e-170">App Studio является рекомендуемый способ создания и обновления пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="12d4e-170">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="12d4e-171">Для любого метода вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="12d4e-171">For either method you will need the following:</span></span>

- <span data-ttu-id="12d4e-172">URL-адрес, по которому ваше приложение можно найти в Интернете.</span><span class="sxs-lookup"><span data-stu-id="12d4e-172">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="12d4e-173">Иконки, Teams будут использоваться для бренд вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="12d4e-173">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="12d4e-174">Образец поставляется с иконками заполнителя, расположенными в "src'static"images.</span><span class="sxs-lookup"><span data-stu-id="12d4e-174">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="12d4e-175">App Studio также предоставит значки по умолчанию, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="12d4e-175">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="12d4e-176">Обновление размещено приложение</span><span class="sxs-lookup"><span data-stu-id="12d4e-176">Update your hosted app</span></span>

<span data-ttu-id="12d4e-177">Пример приложения требует, чтобы следующие переменные среды были установлены на значения, которые вы сделали к сведению ранее:</span><span class="sxs-lookup"><span data-stu-id="12d4e-177">The sample app requires the following environment variables to be set to the values you made a note of earlier:</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="12d4e-178">Как вы это делаете, отличается в зависимости от того, как вы размещали приложение.</span><span class="sxs-lookup"><span data-stu-id="12d4e-178">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="12d4e-179">Важно использовать переменные среды в том, что эти значения являются частью вашей среды - они могут быть доступны по коду для вашего приложения, но они не подвергаются третьим лицам, которые могут изучить файлы, которые составляют ваш сайт.</span><span class="sxs-lookup"><span data-stu-id="12d4e-179">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="12d4e-180">Если вы используете приложение с помощью ngrok, вам нужно настроить некоторые локальные переменные среды.</span><span class="sxs-lookup"><span data-stu-id="12d4e-180">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="12d4e-181">Есть много способов сделать это, но проще всего, если вы используете Visual Studio Code, заключается в том, чтобы добавить [конфигурацию запуска:](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)</span><span class="sxs-lookup"><span data-stu-id="12d4e-181">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

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

<span data-ttu-id="12d4e-182">Где:</span><span class="sxs-lookup"><span data-stu-id="12d4e-182">Where:</span></span>

<span data-ttu-id="12d4e-183">MICROSOFT_APP_ID и MICROSOFT_APP_PASSWORD является идентификатором и паролем, соответственно, для вашего бота.</span><span class="sxs-lookup"><span data-stu-id="12d4e-183">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="12d4e-184">NODE_DEBUG покажет вам, что происходит в вашем боте в Visual Studio Code отладки.</span><span class="sxs-lookup"><span data-stu-id="12d4e-184">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="12d4e-185">NODE_CONFIG_DIR указывает на каталог в корне репозитория (по умолчанию, когда приложение запущено локально, оно ищет его в папке src).</span><span class="sxs-lookup"><span data-stu-id="12d4e-185">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="12d4e-186">Если вы не остановили npm от более предыдущего в учебнике, то вам будет нужно побежать `npm stop` для того чтобы Visual Studio Code для того чтобы pickup ваши переменные конфигурации старта правильно.</span><span class="sxs-lookup"><span data-stu-id="12d4e-186">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="12d4e-187">Настройка вкладки приложения</span><span class="sxs-lookup"><span data-stu-id="12d4e-187">Configure the app tab</span></span>

<span data-ttu-id="12d4e-188">Как только вы установите приложение в команду, вам нужно будет настроить его, чтобы показать содержимое.</span><span class="sxs-lookup"><span data-stu-id="12d4e-188">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="12d4e-189">Перейдите на канал в команде и нажмите на **кнопку «Я»,** чтобы добавить новую вкладку. Затем вы можете выбрать `Hello World` из **списка вкладок** Добавить.</span><span class="sxs-lookup"><span data-stu-id="12d4e-189">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="12d4e-190">Затем вам будет представлен диалог конфигурации.</span><span class="sxs-lookup"><span data-stu-id="12d4e-190">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="12d4e-191">Этот диалог позволит вам выбрать, какую вкладку для отображения в этом канале.</span><span class="sxs-lookup"><span data-stu-id="12d4e-191">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="12d4e-192">После выбора вкладки и нажатия кнопки вы `Save` можете увидеть вкладку `Hello World` загружены вкладке вы выбрали:</span><span class="sxs-lookup"><span data-stu-id="12d4e-192">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose:</span></span>

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="12d4e-193">Проверьте своего бота в Teams</span><span class="sxs-lookup"><span data-stu-id="12d4e-193">Test your bot in Teams</span></span>

<span data-ttu-id="12d4e-194">Теперь вы можете взаимодействовать с ботом в Teams.</span><span class="sxs-lookup"><span data-stu-id="12d4e-194">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="12d4e-195">Выберите канал в команде, где вы зарегистрировали приложение, и ввемите, `@your-bot-name` а затем ваше сообщение.</span><span class="sxs-lookup"><span data-stu-id="12d4e-195">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="12d4e-196">Это называется **\@ упоминанием**.</span><span class="sxs-lookup"><span data-stu-id="12d4e-196">This is called an **\@mention**.</span></span> <span data-ttu-id="12d4e-197">Независимо от сообщения, которое вы отправляете боту, вы будете отправлены вам в качестве ответа:</span><span class="sxs-lookup"><span data-stu-id="12d4e-197">Whatever message you send to the bot will be sent back to you as a reply:</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="12d4e-198">Проверьте расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="12d4e-198">Test your messaging extension</span></span>

<span data-ttu-id="12d4e-199">Чтобы проверить расширение обмена сообщениями, вы можете нажать на три точки ниже входной коробки в представлении разговора.</span><span class="sxs-lookup"><span data-stu-id="12d4e-199">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="12d4e-200">Меню будет всплывающее с **приложением "Hello World"** в нем.</span><span class="sxs-lookup"><span data-stu-id="12d4e-200">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="12d4e-201">При нажатии на него, вы увидите ряд случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="12d4e-201">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="12d4e-202">Вы можете выбрать любой из них, и он будет вставлен в ваш разговор:</span><span class="sxs-lookup"><span data-stu-id="12d4e-202">You can choose any one of them and it will be inserted it into your conversation:</span></span>

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="12d4e-203">Выберите один из случайных текстов, и вы увидите карту отформатированы и готовы отправить с вашим собственным сообщением в нижней части:</span><span class="sxs-lookup"><span data-stu-id="12d4e-203">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom:</span></span>

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
