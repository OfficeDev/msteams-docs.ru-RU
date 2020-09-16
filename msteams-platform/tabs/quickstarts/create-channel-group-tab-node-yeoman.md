---
title: Создание настраиваемой вкладки каналов и групп с Node.js и генератором Yeoman для Microsoft Teams
author: laujan
description: Краткое руководство по созданию вкладки каналов и групп с помощью генератора Yeoman для Microsoft Teams.
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 77081f83c753f812032ccfebe2accd3cb8859f99
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818936"
---
# <a name="create-a-custom-channel-and-group-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="8241e-103">Создание настраиваемой вкладки каналов и групп с Node.js и генератором Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8241e-103">Create a custom channel and group tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="8241e-104">Это руководство соответствует действиям, описанным в статье [Создание первого вики-сайта приложения Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) , который находится в репозитории Microsoft OfficeDev GitHub.</span><span class="sxs-lookup"><span data-stu-id="8241e-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="8241e-105">В этом руководстве мы рассмотрим создание настраиваемой вкладки каналов и групп с помощью [генератора Yeoman Teams](https://github.com/OfficeDev/generator-teams/).</span><span class="sxs-lookup"><span data-stu-id="8241e-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="8241e-106">**Вы хотите создать настраиваемую или статическую вкладку?**</span><span class="sxs-lookup"><span data-stu-id="8241e-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="8241e-107">С помощью клавиш со стрелками выберите Настраиваемая вкладка.</span><span class="sxs-lookup"><span data-stu-id="8241e-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="8241e-108">**Какие области вы планируете использовать для вкладки?**</span><span class="sxs-lookup"><span data-stu-id="8241e-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="8241e-109">Вы можете выбрать команду и/или групповой чат</span><span class="sxs-lookup"><span data-stu-id="8241e-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="8241e-110">**Вы хотите, чтобы эта вкладка была доступна в SharePoint Online? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="8241e-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="8241e-111">Выберите **n**.</span><span class="sxs-lookup"><span data-stu-id="8241e-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8241e-112">Компонент Path **йоурдефаулттабнаметаб**, указанный в этом кратком руководстве, — это значение, введенное в генератор для **имени вкладки по умолчанию** , а также для **вкладки**Word.</span><span class="sxs-lookup"><span data-stu-id="8241e-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="8241e-113">Пример: дефаулттабнаме: **митаб**  =>  **/митабтаб/**</span><span class="sxs-lookup"><span data-stu-id="8241e-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="8241e-114">В каталоге проекта перейдите к следующему:</span><span class="sxs-lookup"><span data-stu-id="8241e-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="8241e-115">Здесь вы найдете логику вкладки.</span><span class="sxs-lookup"><span data-stu-id="8241e-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="8241e-116">Нахождение `render()` метода и добавление следующего `<div>` тега и содержимого в начало `<PanelBody>` кода контейнера:</span><span class="sxs-lookup"><span data-stu-id="8241e-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="8241e-117">Обязательно сохраните обновленный файл.</span><span class="sxs-lookup"><span data-stu-id="8241e-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="8241e-118">Построение и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="8241e-118">Build and Run Your Application</span></span>

<span data-ttu-id="8241e-119">Откройте командную строку в каталоге проекта, чтобы выполнить следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="8241e-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="8241e-120">Чтобы просмотреть страницу настройки вкладки, перейдите на страницу `https://localhost:3007/<yourDefaultAppNameTab>/config.html` .</span><span class="sxs-lookup"><span data-stu-id="8241e-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="8241e-121">Должны отображаться следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="8241e-121">You should see the following:</span></span>

![снимок экрана страницы конфигурации](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="8241e-123">Установка безопасного туннеля для вкладки</span><span class="sxs-lookup"><span data-stu-id="8241e-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="8241e-124">Microsoft Teams является полностью облачным продуктом и требует, чтобы содержимое вкладки было доступно из облака с использованием конечных точек HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8241e-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="8241e-125">В Teams не разрешается локальное размещение, поэтому необходимо либо опубликовать вкладку на общедоступном URL-адресе, либо использовать прокси-сервер, который будет предоставлять локальный порт URL-адресу, доступному для выхода в Интернет.</span><span class="sxs-lookup"><span data-stu-id="8241e-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="8241e-126">Чтобы протестировать расширение вкладки, вы будете использовать [ngrok](https://ngrok.com/docs), встроенный в это приложение.</span><span class="sxs-lookup"><span data-stu-id="8241e-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="8241e-127">Ngrok — это программное средство обратного прокси-сервера, которое создает туннель для общедоступных конечных точек HTTPS на локальном веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="8241e-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="8241e-128">Конечные точки веб-сервера будут доступны в текущем сеансе на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="8241e-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="8241e-129">При завершении работы компьютера или переходе в спящий режим служба становится недоступной.</span><span class="sxs-lookup"><span data-stu-id="8241e-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="8241e-130">В командной строки выйдите из localhost и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8241e-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="8241e-131">После того как вкладка загружена в Microsoft Teams и успешно сохранена, ее можно просмотреть в коллекции вкладок, добавить ее на панель вкладок и взаимодействовать с ней до завершения сеанса туннеля ngrok.</span><span class="sxs-lookup"><span data-stu-id="8241e-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="8241e-132">Если вы перезапустите сеанс ngrok, вам потребуется обновить свое приложение с помощью нового URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="8241e-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="8241e-133">Отправка приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="8241e-133">Upload your application to Teams</span></span>

- <span data-ttu-id="8241e-134">Откройте клиент Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8241e-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="8241e-135">Если вы используете [версию на основе веб-сайта](https://teams.microsoft.com) , вы можете проверить интерфейсный код с помощью [средств разработчика](~/tabs/how-to/developer-tools.md)в браузере.</span><span class="sxs-lookup"><span data-stu-id="8241e-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="8241e-136">На панели *йоуртеамс* слева выберите `...` меню рядом с командой, которую вы используете для тестирования вкладки, и выберите пункт **Управление командой**.</span><span class="sxs-lookup"><span data-stu-id="8241e-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="8241e-137">В главной панели выберите **приложения** из панели вкладок и нажмите кнопку **Отправить пользовательское приложение** , расположенное в правом нижнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="8241e-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="8241e-138">Откройте каталог проекта, перейдите в папку **./паккаже** , выберите папку ZIP пакет приложения и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="8241e-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="8241e-139">Вкладка будет загружена в Teams.</span><span class="sxs-lookup"><span data-stu-id="8241e-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="8241e-140">Вернитесь к команде, выберите канал, в котором необходимо отобразить вкладку, нажмите ➕ на панели вкладок и выберите вкладку в коллекции.</span><span class="sxs-lookup"><span data-stu-id="8241e-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="8241e-141">Следуйте инструкциям по добавлению вкладки. Обратите внимание, что для вкладки канал/группа существует настраиваемое диалоговое окно настройки.</span><span class="sxs-lookup"><span data-stu-id="8241e-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="8241e-142">Нажмите кнопку **сохранить** , и вкладка будет добавлена на панель вкладок канала.</span><span class="sxs-lookup"><span data-stu-id="8241e-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>
