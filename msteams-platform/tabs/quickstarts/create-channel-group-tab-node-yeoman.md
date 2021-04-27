---
title: Создание настраиваемой вкладки канала и группы с Node.js и генератором Yeoman для Microsoft Teams
author: laujan
description: Руководство по созданию вкладки каналов и групп с генератором Yeoman для Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 962a558014a3bc84010860082df6891bb48c7715
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020305"
---
# <a name="create-a-custom-channel-and-group-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="7f169-103">Создание настраиваемой вкладки канала и группы с Node.js и генератором Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7f169-103">Create a custom channel and group tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="7f169-104">Этот quickstart следует шагам, описанным в приложении [Build Your First Microsoft Teams App Wiki,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) найденном в репозитории Microsoft OfficeDev GitHub.</span><span class="sxs-lookup"><span data-stu-id="7f169-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="7f169-105">В этом quickstart мы создам настраиваемый канал и вкладку группы с помощью [генератора Teams Yeoman.](https://github.com/OfficeDev/generator-teams/)</span><span class="sxs-lookup"><span data-stu-id="7f169-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="7f169-106">**Хотите создать настраиваемую или статическую вкладку?**</span><span class="sxs-lookup"><span data-stu-id="7f169-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="7f169-107">Используйте клавиши стрелки для выбора настраиваемой вкладки.</span><span class="sxs-lookup"><span data-stu-id="7f169-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="7f169-108">**Какие области вы собираетесь использовать для вкладки?**</span><span class="sxs-lookup"><span data-stu-id="7f169-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="7f169-109">Вы можете выбрать группу и/или групповой чат</span><span class="sxs-lookup"><span data-stu-id="7f169-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="7f169-110">**Хотите, чтобы эта вкладка была доступна в SharePoint Online? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="7f169-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="7f169-111">Выберите **n**.</span><span class="sxs-lookup"><span data-stu-id="7f169-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="7f169-112">Компонент пути **yourDefaultTabNameTab,** на который ссылается в этом quickstart,  это значение, которое вы ввели в генератор для имени вкладки по умолчанию плюс слово **Tab**.</span><span class="sxs-lookup"><span data-stu-id="7f169-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="7f169-113">Например: DefaultTabName: **MyTab**  =>  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="7f169-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="7f169-114">В каталоге проектов перейдите к следующему:</span><span class="sxs-lookup"><span data-stu-id="7f169-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="7f169-115">Здесь вы найдете логику вкладки.</span><span class="sxs-lookup"><span data-stu-id="7f169-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="7f169-116">Найдите метод и добавьте следующий тег и содержимое в `render()` `<div>` верхнюю часть `<PanelBody>` кода контейнера:</span><span class="sxs-lookup"><span data-stu-id="7f169-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="7f169-117">Обязательно сохраните обновленный файл.</span><span class="sxs-lookup"><span data-stu-id="7f169-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="7f169-118">Создание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="7f169-118">Build and Run Your Application</span></span>

<span data-ttu-id="7f169-119">Откройте командную подсказку в каталоге проектов для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="7f169-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="7f169-120">Чтобы просмотреть страницу конфигурации вкладок, перейдите к `https://localhost:3007/<yourDefaultAppNameTab>/config.html` .</span><span class="sxs-lookup"><span data-stu-id="7f169-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="7f169-121">Должны отображаться следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="7f169-121">You should see the following:</span></span>

![Скриншот страницы конфигурации](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="7f169-123">Создание безопасного туннеля на вкладке</span><span class="sxs-lookup"><span data-stu-id="7f169-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="7f169-124">Microsoft Teams — это полностью облачный продукт, который требует, чтобы содержимое вкладок было доступно в облаке с помощью конечных точек HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7f169-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="7f169-125">Команды не позволяют локальному размещению, поэтому необходимо либо опубликовать вкладку на общедоступный URL-адрес, либо использовать прокси-сервер, который будет подвергать локальный порт URL-адресу, относящаяся к Интернету.</span><span class="sxs-lookup"><span data-stu-id="7f169-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="7f169-126">Чтобы протестировать расширение вкладки, вы будете использовать [ngrok,](https://ngrok.com/docs)встроенный в это приложение.</span><span class="sxs-lookup"><span data-stu-id="7f169-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="7f169-127">Ngrok — это средство обратного прокси-программного обеспечения, которое создаст туннель для общедоступных конечных точек HTTPS локального веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="7f169-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="7f169-128">Веб-точки сервера будут доступны во время текущего сеанса на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="7f169-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="7f169-129">Когда машина отключена или заснул, служба больше не будет доступна.</span><span class="sxs-lookup"><span data-stu-id="7f169-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="7f169-130">В командной подсказке выйдите из localhost и введите следующее:</span><span class="sxs-lookup"><span data-stu-id="7f169-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="7f169-131">После того как вкладка была загружена в группы Майкрософт и успешно сохранена, ее можно просмотреть в галерее вкладок, добавить ее в планку вкладок и взаимодействовать с ней до окончания сеанса туннеля ngrok.</span><span class="sxs-lookup"><span data-stu-id="7f169-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="7f169-132">Если вы перезапустите сеанс ngrok, вам потребуется обновить приложение с новым URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="7f169-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="7f169-133">Отправка приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="7f169-133">Upload your application to Teams</span></span>

- <span data-ttu-id="7f169-134">Откройте клиент Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7f169-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="7f169-135">Если вы используете [веб-версию,](https://teams.microsoft.com) вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="7f169-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="7f169-136">В панели *YourTeams* слева выберите меню рядом с командой, которую вы используете для тестирования вкладки, и `...` выберите команду **Manage.**</span><span class="sxs-lookup"><span data-stu-id="7f169-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="7f169-137">На главной панели выберите **Приложения** из панели вкладок и выберите **Загрузите** пользовательское приложение, расположенное в нижнем правом углу страницы.</span><span class="sxs-lookup"><span data-stu-id="7f169-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="7f169-138">Откройте каталог проектов, просмотрите **папку ./package,** выберите папку почтовый индекс пакета приложений и **откройте**.</span><span class="sxs-lookup"><span data-stu-id="7f169-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="7f169-139">Вкладка будет загружена в Teams.</span><span class="sxs-lookup"><span data-stu-id="7f169-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="7f169-140">Вернись в команду, выберите канал, в котором вы хотите отобразить вкладку, выберите ➕ из панели вкладок и выберите вкладку из галереи.</span><span class="sxs-lookup"><span data-stu-id="7f169-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="7f169-141">Следуйте указаниям для добавления вкладки. Обратите внимание, что существует настраиваемый диалоговое окно конфигурации для вкладки канал/группа.</span><span class="sxs-lookup"><span data-stu-id="7f169-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="7f169-142">Выберите **Сохранить,** и вкладка будет добавлена в вкладку канала.</span><span class="sxs-lookup"><span data-stu-id="7f169-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>
