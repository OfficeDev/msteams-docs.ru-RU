---
title: 'Быстрый старт: Создайте пользовательскую личную вкладку с Node.js и генератором Yeoman для Microsoft Teams'
author: laujan
description: Краткое руководство по созданию личной вкладке с генератором Yeoman для Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 88ad05aacaed69d695bc918e3e8a44ec18e560ae
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566611"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="a6607-103">Создайте пользовательскую личную вкладку, Node.js и генератор Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a6607-103">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="a6607-104">Этот быстрый старт следует шагам, изложенным [в приложении Microsoft Teams в вики,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) найденном в репозитории Microsoft OfficeDev GitHub microsoft OfficeDev.</span><span class="sxs-lookup"><span data-stu-id="a6607-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="a6607-105">В этом quickstart мы будем ходить через создание пользовательских личных вкладку с [помощью Teams генератора Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="a6607-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="a6607-106">Мы также загрузим приложение в Team.</span><span class="sxs-lookup"><span data-stu-id="a6607-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="a6607-107">**Создание настраиваемой или статической вкладки**</span><span class="sxs-lookup"><span data-stu-id="a6607-107">**Create a configurable or static tab**</span></span>

<span data-ttu-id="a6607-108">Используйте клавиши стрелки, чтобы выбрать статическую вкладку.</span><span class="sxs-lookup"><span data-stu-id="a6607-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="a6607-109">Компонент пути *yourDefaultTabNameTab*, на который ссылается в этом quickstart, это значение, которое вы ввели в генератор *для имени вкладки по умолчанию* плюс слово *Tab*.</span><span class="sxs-lookup"><span data-stu-id="a6607-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="a6607-110">Например: DefaultTabName: *MyTab*  =>  */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="a6607-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="a6607-111">Создайте свою личную вкладку</span><span class="sxs-lookup"><span data-stu-id="a6607-111">Create your personal tab</span></span>

<span data-ttu-id="a6607-112">Чтобы добавить личную вкладку в это приложение, вы создадите страницу содержимого и обновит существующие файлы:</span><span class="sxs-lookup"><span data-stu-id="a6607-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="a6607-113">В редакторе кода создайте новый HTML-файл, **personal.html** и добавьте следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="a6607-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

- <span data-ttu-id="a6607-114">Сохранить **personal.html** в веб-папке **приложения:**</span><span class="sxs-lookup"><span data-stu-id="a6607-114">Save **personal.html** in your application's **web** folder:</span></span>

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- <span data-ttu-id="a6607-115">Откройте **manifest.jsв** редакторе кода:</span><span class="sxs-lookup"><span data-stu-id="a6607-115">Open **manifest.json** in your code editor:</span></span>

    ```bash
    ./src/manifest/manifest.json/
    ```

<span data-ttu-id="a6607-116">Добавьте следующее в `staticTabs` пустой массив `staticTabs":[]` () и добавьте следующий объект JSON:</span><span class="sxs-lookup"><span data-stu-id="a6607-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="a6607-117">Не забудьте обновить **компонент пути "contentURL"** **yourDefaultTabNameTab с** вашим фактическим именем вкладки.</span><span class="sxs-lookup"><span data-stu-id="a6607-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="a6607-118">Сохраните обновленный **manifest.jsна**.</span><span class="sxs-lookup"><span data-stu-id="a6607-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="a6607-119">Ваша страница содержимого должна быть подана в IFrame.</span><span class="sxs-lookup"><span data-stu-id="a6607-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="a6607-120">Откройте **Tab.ts** в редакторе кода:</span><span class="sxs-lookup"><span data-stu-id="a6607-120">Open **Tab.ts** in your code editor:</span></span>

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- <span data-ttu-id="a6607-121">Добавьте следующее в список декораторов IFrame:</span><span class="sxs-lookup"><span data-stu-id="a6607-121">Add the following to the list of IFrame decorators:</span></span>

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- <span data-ttu-id="a6607-122">Убедитесь в том, чтобы сохранить **обновленный файл Tab.ts.**</span><span class="sxs-lookup"><span data-stu-id="a6607-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="a6607-123">Код вкладки завершен.</span><span class="sxs-lookup"><span data-stu-id="a6607-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="a6607-124">Создание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="a6607-124">Build and Run Your Application</span></span>

<span data-ttu-id="a6607-125">Откройте командный запрос в каталоге проекта для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="a6607-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="a6607-126">Чтобы просмотреть вашу личную вкладку, перейдите на `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="a6607-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![личный скриншот вкладки](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="a6607-128">Создание безопасного туннеля для вкладки</span><span class="sxs-lookup"><span data-stu-id="a6607-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="a6607-129">Microsoft Teams является полностью облачным продуктом и требует, чтобы содержимое вкладок было доступно из облака с помощью конечных точек HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a6607-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="a6607-130">Teams не позволяет локального хостинга, поэтому, вам нужно либо опубликовать свою вкладку на общедоступный URL или использовать прокси, который будет подвергать ваш местный порт в интернет-адрес.</span><span class="sxs-lookup"><span data-stu-id="a6607-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="a6607-131">Чтобы проверить расширение вкладок, вы будете использовать [ngrok](https://ngrok.com/docs), который встроен в это приложение.</span><span class="sxs-lookup"><span data-stu-id="a6607-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="a6607-132">Ngrok является обратным прокси программное обеспечение инструмент, который создаст туннель для локально работает веб-сервера общедоступных https конечных точек.</span><span class="sxs-lookup"><span data-stu-id="a6607-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="a6607-133">Веб-конечные точки сервера будут доступны в течение текущего сеанса на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="a6607-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="a6607-134">Когда машина выключена или засыпает, служба больше не будет доступна.</span><span class="sxs-lookup"><span data-stu-id="a6607-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="a6607-135">В вашем командном запросе выйдите из локального хостинга и введите следующее:</span><span class="sxs-lookup"><span data-stu-id="a6607-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="a6607-136">После того, как вкладка была загружена в команды Майкрософт, **через ngrok,** и успешно сохранена, вы можете просмотреть ее в Teams до окончания сеанса туннеля.</span><span class="sxs-lookup"><span data-stu-id="a6607-136">After your tab has been uploaded to Microsoft teams, via **ngrok**, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="a6607-137">Upload заявление в Teams</span><span class="sxs-lookup"><span data-stu-id="a6607-137">Upload your application to Teams</span></span>

- <span data-ttu-id="a6607-138">Откройте Microsoft Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="a6607-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="a6607-139">Если вы [используете веб-версию,](https://teams.microsoft.com) вы можете проверить свой передний код с помощью инструментов [разработчика браузера.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="a6607-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="a6607-140">В **панели YourTeams** слева выберите меню рядом с командой, `...` которую вы используете, чтобы протестировать вкладку и выбрать **команду Manage.**</span><span class="sxs-lookup"><span data-stu-id="a6607-140">In the **YourTeams** panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="a6607-141">В основной панели **выберите Приложения** из панели **вкладок Upload выбрать специальное** приложение, расположенное в правом нижнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="a6607-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="a6607-142">Откройте каталог проекта, просмотрите папку **./package,** выберите папку на молнии, нажмите правой кнопкой мыши и выберите **Open.**</span><span class="sxs-lookup"><span data-stu-id="a6607-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="a6607-143">Ваша вкладка будет загружаться в Teams.</span><span class="sxs-lookup"><span data-stu-id="a6607-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="a6607-144">Просмотр личных вкладок</span><span class="sxs-lookup"><span data-stu-id="a6607-144">View your personal tabs</span></span>

<span data-ttu-id="a6607-145">В навигационной панели, расположенной слева от Teams, `...` выберите меню и выберите приложение из списка.</span><span class="sxs-lookup"><span data-stu-id="a6607-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>

## <a name="next-step"></a><span data-ttu-id="a6607-146">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="a6607-146">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a6607-147">Создание личной вкладки с помощью ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="a6607-147">Create a personal tab using ASP.NETCore</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
