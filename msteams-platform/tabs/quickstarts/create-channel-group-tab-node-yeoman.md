---
title: Создайте пользовательский канал и группу Tab с Node.js и генератором Yeoman для Microsoft Teams
author: laujan
description: Краткое руководство по созданию канала и группы вкладку с генератором Yeoman для Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 559393884e3b8a4aad1787ea4ca8f9f4de54d151
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566649"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="c9f15-103">Создайте пользовательский канал и групповую вкладку, Node.js и генератор Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c9f15-103">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="c9f15-104">Этот быстрый старт следует шагам, изложенным [в приложении Microsoft Teams в вики,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) найденном в репозитории Microsoft OfficeDev GitHub microsoft OfficeDev.</span><span class="sxs-lookup"><span data-stu-id="c9f15-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="c9f15-105">В этом quickstart мы будем ходить через создание пользовательского канала и группы вкладку с [помощью Teams генератора Yeoman](https://github.com/OfficeDev/generator-teams/).</span><span class="sxs-lookup"><span data-stu-id="c9f15-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="c9f15-106">**Вы хотите создать настраиваемую или статичную вкладку?**</span><span class="sxs-lookup"><span data-stu-id="c9f15-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="c9f15-107">Используйте клавиши стрелки, чтобы выбрать настраиваемую вкладку.</span><span class="sxs-lookup"><span data-stu-id="c9f15-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="c9f15-108">**Какие области вы собираетесь использовать для вкладки?**</span><span class="sxs-lookup"><span data-stu-id="c9f15-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="c9f15-109">Вы можете выбрать команду и/или групповой чат</span><span class="sxs-lookup"><span data-stu-id="c9f15-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="c9f15-110">**Вы хотите, чтобы эта вкладка была доступна в интернете SharePoint Интернете? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="c9f15-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="c9f15-111">Выберите **n**.</span><span class="sxs-lookup"><span data-stu-id="c9f15-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c9f15-112">Компонент пути **yourDefaultTabNameTab**, на который ссылается в этом quickstart, это значение, которое вы ввели в генератор **для имени вкладки по умолчанию** плюс слово **Tab**.</span><span class="sxs-lookup"><span data-stu-id="c9f15-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="c9f15-113">Например: DefaultTabName: **MyTab**  =>  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="c9f15-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="c9f15-114">В каталоге проекта перейдите к следующему:</span><span class="sxs-lookup"><span data-stu-id="c9f15-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="c9f15-115">Вот где вы найдете свою логику вкладок.</span><span class="sxs-lookup"><span data-stu-id="c9f15-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="c9f15-116">Найдите `render()` метод и добавьте `<div>` следующий тег и содержимое в верхней части `<PanelBody>` кода контейнера:</span><span class="sxs-lookup"><span data-stu-id="c9f15-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="c9f15-117">Убедитесь в том, чтобы сохранить обновленный файл.</span><span class="sxs-lookup"><span data-stu-id="c9f15-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="c9f15-118">Создание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="c9f15-118">Build and Run Your Application</span></span>

<span data-ttu-id="c9f15-119">Откройте командный запрос в каталоге проекта для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="c9f15-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="c9f15-120">Для просмотра страницы конфигурации вкладок перейдите `https://localhost:3007/<yourDefaultAppNameTab>/config.html` в .</span><span class="sxs-lookup"><span data-stu-id="c9f15-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="c9f15-121">Должны отображаться следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="c9f15-121">You should see the following:</span></span>

![скриншот страницы конфигурации](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="c9f15-123">Создание безопасного туннеля для вкладки</span><span class="sxs-lookup"><span data-stu-id="c9f15-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="c9f15-124">Microsoft Teams является полностью облачным продуктом и требует, чтобы содержимое вкладок было доступно из облака с помощью конечных точек HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c9f15-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="c9f15-125">Teams не позволяет локального хостинга, поэтому, вам нужно либо опубликовать свою вкладку на общедоступный URL или использовать прокси, который будет подвергать ваш местный порт в интернет-адрес.</span><span class="sxs-lookup"><span data-stu-id="c9f15-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="c9f15-126">Чтобы проверить расширение вкладок, вы будете использовать [ngrok](https://ngrok.com/docs), который встроен в это приложение.</span><span class="sxs-lookup"><span data-stu-id="c9f15-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="c9f15-127">Ngrok является обратным прокси программное обеспечение инструмент, который создаст туннель для локально работает веб-сервера общедоступных https конечных точек.</span><span class="sxs-lookup"><span data-stu-id="c9f15-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="c9f15-128">Веб-конечные точки сервера будут доступны в течение текущего сеанса на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="c9f15-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="c9f15-129">Когда машина выключена или засыпает, служба больше не будет доступна.</span><span class="sxs-lookup"><span data-stu-id="c9f15-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="c9f15-130">В вашем командном запросе выйдите из локального хостинга и введите следующее:</span><span class="sxs-lookup"><span data-stu-id="c9f15-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="c9f15-131">После того, как вкладка была загружена в команды Майкрософт и успешно сохранена, вы можете просмотреть ее в галерее вкладок, добавить ее в бар вкладок и взаимодействовать с ней до окончания сеанса туннеля ngrok.</span><span class="sxs-lookup"><span data-stu-id="c9f15-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="c9f15-132">Если вы перезапустите сеанс ngrok, вам нужно обновить приложение с помощью нового URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="c9f15-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="c9f15-133">Upload заявление в Teams</span><span class="sxs-lookup"><span data-stu-id="c9f15-133">Upload your application to Teams</span></span>

- <span data-ttu-id="c9f15-134">Откройте Microsoft Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="c9f15-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="c9f15-135">Если вы [используете веб-версию,](https://teams.microsoft.com) вы можете проверить свой передний код с помощью инструментов [разработчика браузера.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="c9f15-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="c9f15-136">В *панели YourTeams* слева выберите меню рядом с командой, `...` которую вы используете, чтобы протестировать вкладку и выбрать **команду Manage.**</span><span class="sxs-lookup"><span data-stu-id="c9f15-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="c9f15-137">В основной панели **выберите Приложения** из панели **вкладок Upload выбрать специальное** приложение, расположенное в правом нижнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="c9f15-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="c9f15-138">Откройте каталог проекта, просмотрите папку **./package,** выберите папку застежки-молнии пакета приложений и **выберите Open.**</span><span class="sxs-lookup"><span data-stu-id="c9f15-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="c9f15-139">Ваша вкладка будет загружаться в Teams.</span><span class="sxs-lookup"><span data-stu-id="c9f15-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="c9f15-140">Вернитесь в свою команду, выберите канал, где вы хотели бы отобразить вкладку, выберите ➕ из бара вкладок и выберите вкладку из галереи.</span><span class="sxs-lookup"><span data-stu-id="c9f15-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="c9f15-141">Следуйте указаниям для добавления вкладки. Обратите внимание, что существует пользовательский диалог конфигурации для вкладки канал/группа.</span><span class="sxs-lookup"><span data-stu-id="c9f15-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="c9f15-142">Выберите **Сохранить** и вкладка будет добавлена в таблицу канала.</span><span class="sxs-lookup"><span data-stu-id="c9f15-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>

## <a name="next-step"></a><span data-ttu-id="c9f15-143">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="c9f15-143">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c9f15-144">Создание пользовательского канала и групповой вкладки с помощью ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="c9f15-144">Create a Custom Channel and Group Tab with ASP.NETCore</span></span>](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)