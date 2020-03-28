---
title: Начало работы с App Studio и Node. js
description: Приступая к созданию замечательных приложений в Microsoft Teams с помощью Node. js и App Studio
keywords: Приступая к работе Node. js NodeJS App Studio
ms.date: 11/09/2018
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 92fbbdd30e9cdaf54644b42bf642ca5825bcec51
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2020
ms.locfileid: "43034052"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-nodejs-and-app-studio"></a><span data-ttu-id="406d0-104">Приступая к работе на платформе Microsoft Teams с Node. js и App Studio</span><span class="sxs-lookup"><span data-stu-id="406d0-104">Get started on the Microsoft Teams platform with Node.js and App Studio</span></span>

<span data-ttu-id="406d0-105">Платформа для разработчиков [Microsoft Teams](/microsoftteams/) позволяет легко расширять Teams и самостоятельно интегрировать свои приложения и службы в рабочую область Teams.</span><span class="sxs-lookup"><span data-stu-id="406d0-105">The [Microsoft Teams](/microsoftteams/) developer platform makes it easy for you to extend Teams and integrate your own applications and services seamlessly into the Teams workspace.</span></span> <span data-ttu-id="406d0-106">Затем эти приложения можно распространять на предприятие или в Teams по всему миру.</span><span class="sxs-lookup"><span data-stu-id="406d0-106">These apps can then be distributed to your enterprise or for teams around the world.</span></span>

<span data-ttu-id="406d0-107">Для расширения Microsoft Teams необходимо создать приложение Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="406d0-107">To extend Microsoft Teams, you need to create a Microsoft Teams app.</span></span> <span data-ttu-id="406d0-108">Приложение Microsoft Teams — это веб-приложение, которое вы размещаете.</span><span class="sxs-lookup"><span data-stu-id="406d0-108">A Microsoft Teams app is a web application that you host.</span></span> <span data-ttu-id="406d0-109">Затем это приложение можно интегрировать в рабочую область пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="406d0-109">This app can then be integrated into the user's workspace in Teams.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="406d0-110">Скачайте приложение и разместите его</span><span class="sxs-lookup"><span data-stu-id="406d0-110">Download and host your app</span></span>

<span data-ttu-id="406d0-111">Выполните следующие действия, чтобы скачать и разместить простое приложение "Hello World" в Teams.</span><span class="sxs-lookup"><span data-stu-id="406d0-111">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="406d0-112">Получение необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="406d0-112">Get prerequisites</span></span>

<span data-ttu-id="406d0-113">Для выполнения этого руководства необходимы следующие средства.</span><span class="sxs-lookup"><span data-stu-id="406d0-113">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="406d0-114">Если у вас их еще нет, их можно установить из этих ссылок.</span><span class="sxs-lookup"><span data-stu-id="406d0-114">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="406d0-115">Git</span><span class="sxs-lookup"><span data-stu-id="406d0-115">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="406d0-116">Node. js и NPM</span><span class="sxs-lookup"><span data-stu-id="406d0-116">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="406d0-117">Получение любого текстового редактора или IDE.</span><span class="sxs-lookup"><span data-stu-id="406d0-117">Get any text editor or IDE.</span></span> <span data-ttu-id="406d0-118">Вы можете установить и использовать [Visual Studio Code](https://code.visualstudio.com/download) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="406d0-118">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="406d0-119">Если вы видите варианты для добавления `git`, `node`, `npm`и `code` для пути во время установки, выберите для этого.</span><span class="sxs-lookup"><span data-stu-id="406d0-119">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="406d0-120">Это будет удобно.</span><span class="sxs-lookup"><span data-stu-id="406d0-120">It will be handy.</span></span>

<span data-ttu-id="406d0-121">Убедитесь, что средства доступны, выполнив следующую команду в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="406d0-121">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="406d0-122">Используйте окно терминала, наиболее удобное для вашей платформы.</span><span class="sxs-lookup"><span data-stu-id="406d0-122">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="406d0-123">В этих примерах используется bash (включенный в Git), но эти сценарии будут выполняться на большинстве платформ.</span><span class="sxs-lookup"><span data-stu-id="406d0-123">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 4.0.2
```

<span data-ttu-id="406d0-124">У вас может быть другая версия этих приложений.</span><span class="sxs-lookup"><span data-stu-id="406d0-124">You may have a different version of these applications.</span></span> <span data-ttu-id="406d0-125">Это не должна быть проблема, за исключением gulp.</span><span class="sxs-lookup"><span data-stu-id="406d0-125">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="406d0-126">Для gulp необходимо использовать версию 4.0.0 или более позднюю.</span><span class="sxs-lookup"><span data-stu-id="406d0-126">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="406d0-127">Если у вас не установлен gulp (или установлена неправильная версия), сделайте это сейчас, выполнив `npm install gulp` в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="406d0-127">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="406d0-128">Если вы установили код Visual Studio, вы можете проверить установку, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="406d0-128">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="406d0-129">Вы можете продолжить использование этого окна терминала для выполнения команд, приведенных в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="406d0-129">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="406d0-130">Скачать пример</span><span class="sxs-lookup"><span data-stu-id="406d0-130">Download the sample</span></span>

<span data-ttu-id="406d0-131">Мы предоставили простой [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span><span class="sxs-lookup"><span data-stu-id="406d0-131">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span></span> <span data-ttu-id="406d0-132">пример, чтобы приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="406d0-132">sample to get you started.</span></span> <span data-ttu-id="406d0-133">В окне терминала выполните приведенную ниже команду, чтобы клонировать репозиторий примера на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="406d0-133">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> <span data-ttu-id="406d0-134">Вы можете [разветвление](https://help.github.com/articles/fork-a-repo/) этого [репозитория](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) , если вы хотите изменить и вернуть изменения в репозитории GitHub для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="406d0-134">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="406d0-135">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="406d0-135">Build and run the sample</span></span>

<span data-ttu-id="406d0-136">После клонирования репозитория перейдите к каталогу, содержащему пример:</span><span class="sxs-lookup"><span data-stu-id="406d0-136">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd msteams-samples-hello-world-nodejs
```

<span data-ttu-id="406d0-137">Чтобы создать пример, необходимо установить все его зависимости.</span><span class="sxs-lookup"><span data-stu-id="406d0-137">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="406d0-138">Выполните следующую команду, чтобы сделать это:</span><span class="sxs-lookup"><span data-stu-id="406d0-138">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="406d0-139">Должна появиться подмножество зависимостей.</span><span class="sxs-lookup"><span data-stu-id="406d0-139">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="406d0-140">После завершения можно запустить приложение:</span><span class="sxs-lookup"><span data-stu-id="406d0-140">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="406d0-141">Когда приложение приветствия запускается, оно отображается `App started listening on port 3333` в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="406d0-141">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="406d0-142">Если в приведенном выше сообщении отображается другой номер порта, это вызвано тем, что задана переменная среды порта.</span><span class="sxs-lookup"><span data-stu-id="406d0-142">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="406d0-143">Вы можете продолжить использовать этот порт или изменить переменную среды на 3333.</span><span class="sxs-lookup"><span data-stu-id="406d0-143">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="406d0-144">На этом шаге можно открыть окно браузера и перейти по следующим URL-адресам, чтобы убедиться, что загружаются все URL-адреса приложений:</span><span class="sxs-lookup"><span data-stu-id="406d0-144">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="406d0-145">Размещение примера приложения</span><span class="sxs-lookup"><span data-stu-id="406d0-145">Host the sample app</span></span>

<span data-ttu-id="406d0-146">Помните, что приложения в Microsoft Teams представляют собой веб-приложения, которые предоставляют одну или несколько возможностей.</span><span class="sxs-lookup"><span data-stu-id="406d0-146">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="406d0-147">Чтобы платформа Teams загружала приложение, ваше приложение должно быть достижимо из Интернета.</span><span class="sxs-lookup"><span data-stu-id="406d0-147">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="406d0-148">Чтобы приложение было достижимо из Интернета, необходимо *разместить* приложение.</span><span class="sxs-lookup"><span data-stu-id="406d0-148">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="406d0-149">Для локального тестирования можно запустить приложение на локальном компьютере и создать для него туннель с конечной точкой веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="406d0-149">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="406d0-150">[ngrok](https://ngrok.com) — это бесплатный инструмент, который позволяет вам выполнить именно эту задачу.</span><span class="sxs-lookup"><span data-stu-id="406d0-150">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="406d0-151">С помощью *ngrok* вы можете получить веб-адрес, `https://d0ac14a5.ngrok.io` например (этот URL-адрес — это только пример).</span><span class="sxs-lookup"><span data-stu-id="406d0-151">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="406d0-152">Вы можете [скачать и установить](https://ngrok.com/download) *ngrok* для своей среды.</span><span class="sxs-lookup"><span data-stu-id="406d0-152">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="406d0-153">Убедитесь, что вы добавляете его в папку `PATH`.</span><span class="sxs-lookup"><span data-stu-id="406d0-153">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="406d0-154">После установки можно открыть новое окно терминала и выполнить следующую команду для создания туннеля.</span><span class="sxs-lookup"><span data-stu-id="406d0-154">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="406d0-155">В примере используется порт 3333, поэтому обязательно указывайте его здесь.</span><span class="sxs-lookup"><span data-stu-id="406d0-155">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="406d0-156">*Ngrok* прослушивает запросы из Интернета и направляет их в ваше приложение, работающее на порте 3333.</span><span class="sxs-lookup"><span data-stu-id="406d0-156">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="406d0-157">Вы можете проверить его, открыв браузер и перейдя `https://d0ac14a5.ngrok.io/hello` на страницу приветствия приложения.</span><span class="sxs-lookup"><span data-stu-id="406d0-157">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="406d0-158">Обязательно используйте адрес пересылки, отображаемый в *ngrok* в сеансе консоли, а не этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="406d0-158">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="406d0-159">Если вы использовали другой порт в описанном выше шаге [Build and run](#build-and-run-the-sample) , убедитесь, что для установки туннеля *ngrok* используется тот же номер порта.</span><span class="sxs-lookup"><span data-stu-id="406d0-159">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="406d0-160">Рекомендуется запустить *ngrok* в другом окне терминала, чтобы оно было запущено без конфликта с приложением узла, которое позже необходимо остановить, перестроить и повторно запустить.</span><span class="sxs-lookup"><span data-stu-id="406d0-160">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="406d0-161">Сеанс *ngrok* возвратит полезную информацию об отладке в этом окне.</span><span class="sxs-lookup"><span data-stu-id="406d0-161">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="406d0-162">Существует платная версия *ngrok* , позволяющая использовать постоянные имена.</span><span class="sxs-lookup"><span data-stu-id="406d0-162">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="406d0-163">Если вы используете бесплатную версию, приложение будет доступно только в текущем сеансе на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="406d0-163">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="406d0-164">Если компьютер выключен или перейдет в спящий режим, служба станет недоступна.</span><span class="sxs-lookup"><span data-stu-id="406d0-164">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="406d0-165">Помните об этом при совместном использовании приложения для тестирования другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="406d0-165">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="406d0-166">Если вам нужно перезапустить службу, она возвратит новый адрес, и вам потребуется обновить все место, где используется этот адрес.</span><span class="sxs-lookup"><span data-stu-id="406d0-166">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="406d0-167">Помните, что запишите URL-адрес своего приложения, так как это потребуется позже при регистрации приложения в Teams с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="406d0-167">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="406d0-168">Для этой цели Блокнот работает нормально.</span><span class="sxs-lookup"><span data-stu-id="406d0-168">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="406d0-169">Развертывание приложения в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="406d0-169">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="406d0-170">На этом шаге у вас есть приложение, размещенное в Интернете, но вы пока не назначите Teams, где искать его, или даже то, что вызывает приложение.</span><span class="sxs-lookup"><span data-stu-id="406d0-170">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="406d0-171">Теперь необходимо создать пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="406d0-171">To do this you now have to create an app package.</span></span> <span data-ttu-id="406d0-172">Это немного больше текстового файла, содержащего манифест приложения, и некоторые значки, которые клиент Teams будет использовать для правильного отображения и фирменного стиля приложения.</span><span class="sxs-lookup"><span data-stu-id="406d0-172">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="406d0-173">Этот пакет приложения можно создать вручную или с помощью App Studio — средства, которое работает в Teams, которое упростит процесс регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="406d0-173">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="406d0-174">App Studio — это рекомендуемый способ создания и обновления пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="406d0-174">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="406d0-175">Для любого способа потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="406d0-175">For either method you will need the following:</span></span>

- <span data-ttu-id="406d0-176">URL-адрес, по которому ваше приложение может быть найдено в Интернете.</span><span class="sxs-lookup"><span data-stu-id="406d0-176">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="406d0-177">Значки, которые будут использоваться Teams для фирменного стиля приложения.</span><span class="sxs-lookup"><span data-stu-id="406d0-177">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="406d0-178">Пример сопровождается значками заполнителя, расположенными в разделе "срк\статик\имажес.</span><span class="sxs-lookup"><span data-stu-id="406d0-178">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="406d0-179">Кроме того, при необходимости в App Studio будут использоваться значки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="406d0-179">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="406d0-180">Обновление размещенного приложения</span><span class="sxs-lookup"><span data-stu-id="406d0-180">Update your hosted app</span></span>

<span data-ttu-id="406d0-181">Для примера приложения требуются следующие переменные среды, чтобы задать значения, которые вы захотите заметку ранее.</span><span class="sxs-lookup"><span data-stu-id="406d0-181">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="406d0-182">То, как это делается, зависит от того, как вы размещаете приложение.</span><span class="sxs-lookup"><span data-stu-id="406d0-182">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="406d0-183">Важно то, что использование переменных среды заключается в том, что эти значения являются частью среды, но они могут быть доступны для кода приложения, но они не видны третьим лицам, которые могут изучать файлы, составляющие сайт.</span><span class="sxs-lookup"><span data-stu-id="406d0-183">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="406d0-184">Если вы используете приложение с помощью ngrok, вам потребуется настроить некоторые локальные переменные среды.</span><span class="sxs-lookup"><span data-stu-id="406d0-184">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="406d0-185">Это можно сделать множеством способов, но при использовании Visual Studio Code проще всего добавить [конфигурацию запуска](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span><span class="sxs-lookup"><span data-stu-id="406d0-185">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

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

<span data-ttu-id="406d0-186">Где:</span><span class="sxs-lookup"><span data-stu-id="406d0-186">Where:</span></span>

<span data-ttu-id="406d0-187">MICROSOFT_APP_ID и MICROSOFT_APP_PASSWORD — это идентификатор и пароль, соответственно, для ленты.</span><span class="sxs-lookup"><span data-stu-id="406d0-187">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="406d0-188">NODE_DEBUG покажет, что происходит в программе Bot в консоли отладки кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="406d0-188">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="406d0-189">NODE_CONFIG_DIR указывает на каталог в корне репозитория (по умолчанию при локальном запуске приложения он ищет его в папке src).</span><span class="sxs-lookup"><span data-stu-id="406d0-189">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="406d0-190">Если вы еще не остановили NPM в руководстве ранее, вам потребуется выполнить `npm stop` его, чтобы Visual Studio Code мог правильно расказывать переменные настройки запуска.</span><span class="sxs-lookup"><span data-stu-id="406d0-190">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="406d0-191">Настройка вкладки "приложение"</span><span class="sxs-lookup"><span data-stu-id="406d0-191">Configure the app tab</span></span>

<span data-ttu-id="406d0-192">После установки приложения в команду его необходимо настроить для отображения контента.</span><span class="sxs-lookup"><span data-stu-id="406d0-192">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="406d0-193">Перейдите к каналу в группе и нажмите кнопку **"+"** , чтобы добавить новую вкладку. Затем можно выбрать `Hello World` в списке **Добавить вкладку** .</span><span class="sxs-lookup"><span data-stu-id="406d0-193">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="406d0-194">После этого появится диалоговое окно настройки.</span><span class="sxs-lookup"><span data-stu-id="406d0-194">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="406d0-195">Это диалоговое окно позволит выбрать вкладку для отображения в этом канале.</span><span class="sxs-lookup"><span data-stu-id="406d0-195">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="406d0-196">После того, как вы настроили `Save` вкладку и нажали кнопку `Hello World` , вы увидите вкладку, загруженную с выбранной вкладкой.</span><span class="sxs-lookup"><span data-stu-id="406d0-196">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" title="Снимок экрана: Настройка" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="406d0-198">Тестирование ленты в Teams</span><span class="sxs-lookup"><span data-stu-id="406d0-198">Test your bot in Teams</span></span>

<span data-ttu-id="406d0-199">Теперь вы можете взаимодействовать с роботом в Teams.</span><span class="sxs-lookup"><span data-stu-id="406d0-199">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="406d0-200">Выберите канал в группе, в которой вы зарегистрировали свое приложение, и `@your-bot-name`введите текст, за которым следует сообщение.</span><span class="sxs-lookup"><span data-stu-id="406d0-200">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="406d0-201">Это называется \*\* \@упоминанием\*\*.</span><span class="sxs-lookup"><span data-stu-id="406d0-201">This is called an **\@mention**.</span></span> <span data-ttu-id="406d0-202">Любое сообщение, отправляемое в Bot, будет отправлено вам в качестве ответа.</span><span class="sxs-lookup"><span data-stu-id="406d0-202">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" title="Ответы от Bot" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="406d0-204">Проверка расширения системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="406d0-204">Test your messaging extension</span></span>

<span data-ttu-id="406d0-205">Чтобы проверить расширение системы обмена сообщениями, щелкните три точки под полем ввода в представлении беседы.</span><span class="sxs-lookup"><span data-stu-id="406d0-205">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="406d0-206">В меню появится приложение **"Hello World"** .</span><span class="sxs-lookup"><span data-stu-id="406d0-206">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="406d0-207">Щелкнув его, вы увидите несколько случайных текстов.</span><span class="sxs-lookup"><span data-stu-id="406d0-207">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="406d0-208">Вы можете выбрать один из них и вставить его в беседу.</span><span class="sxs-lookup"><span data-stu-id="406d0-208">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="430px" title="Меню расширения для обмена сообщениями" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" title="Результат расширения системы обмена сообщениями" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="406d0-211">Выберите один из случайных текстов, и вы увидите карту, отформатированную и готовую к отправке сообщения в нижней части.</span><span class="sxs-lookup"><span data-stu-id="406d0-211">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="430px" title="Отправка расширения обмена сообщениями" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
