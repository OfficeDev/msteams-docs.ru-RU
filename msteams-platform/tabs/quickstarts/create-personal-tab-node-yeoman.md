---
title: Quickstart. Создайте настраиваемую личную вкладку с Node.js и генератором Yeoman для Microsoft Teams
author: laujan
description: Руководство по созданию личной вкладки с генератором Yeoman для Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 30143fa3c84a68ae6c34176b252badaa4cef9613
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019554"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="04b53-103">Quickstart. Создайте настраиваемую личную вкладку с Node.js и генератором Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="04b53-103">Quickstart: Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="04b53-104">Этот quickstart следует шагам, описанным в приложении [Build Your First Microsoft Teams App Wiki,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) найденном в репозитории Microsoft OfficeDev GitHub.</span><span class="sxs-lookup"><span data-stu-id="04b53-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="04b53-105">В этом quickstart мы создам настраиваемую личную вкладку с помощью генератора [Teams Yeoman.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="04b53-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="04b53-106">Мы также загрузим приложение в Team.</span><span class="sxs-lookup"><span data-stu-id="04b53-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="04b53-107">**Хотите создать настраиваемую или статическую вкладку?**</span><span class="sxs-lookup"><span data-stu-id="04b53-107">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="04b53-108">Используйте клавиши со стрелками, чтобы выбрать статическую вкладку.</span><span class="sxs-lookup"><span data-stu-id="04b53-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="04b53-109">Компонент пути *yourDefaultTabNameTab,* на который ссылается в этом quickstart,  это значение, которое вы ввели в генератор для имени вкладки по умолчанию плюс слово *Tab*.</span><span class="sxs-lookup"><span data-stu-id="04b53-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="04b53-110">Например: DefaultTabName: *MyTab*  =>  */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="04b53-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="04b53-111">Создание личной вкладки</span><span class="sxs-lookup"><span data-stu-id="04b53-111">Create your personal tab</span></span>

<span data-ttu-id="04b53-112">Чтобы добавить личную вкладку в это приложение, вы создайте страницу контента и обновим существующие файлы:</span><span class="sxs-lookup"><span data-stu-id="04b53-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="04b53-113">В редакторе кода создайте новый HTML-файлpersonal.htm **l** и добавьте следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="04b53-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="04b53-114">Сохраните **personal.html** в **веб-папке** приложения:</span><span class="sxs-lookup"><span data-stu-id="04b53-114">Save **personal.html** in your application's **web** folder:</span></span>

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- <span data-ttu-id="04b53-115">Откройте **manifest.jsв** редакторе кода:</span><span class="sxs-lookup"><span data-stu-id="04b53-115">Open **manifest.json** in your code editor:</span></span>

```bash
./src/manifest/manifest.json/
```

<span data-ttu-id="04b53-116">Добавьте следующее в пустой массив `staticTabs` () и `staticTabs":[]` добавьте следующий объект JSON:</span><span class="sxs-lookup"><span data-stu-id="04b53-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="04b53-117">Не забудьте обновить компонент **пути "contentURL"** **yourDefaultTabNameTab** с фактическим именем вкладки.</span><span class="sxs-lookup"><span data-stu-id="04b53-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="04b53-118">Сохраните обновленные **manifest.js.**</span><span class="sxs-lookup"><span data-stu-id="04b53-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="04b53-119">Ваша страница контента должна быть подана в IFrame.</span><span class="sxs-lookup"><span data-stu-id="04b53-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="04b53-120">Откройте **Tab.ts в** редакторе кода:</span><span class="sxs-lookup"><span data-stu-id="04b53-120">Open **Tab.ts** in your code editor:</span></span>

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- <span data-ttu-id="04b53-121">Добавьте в список декораторов IFrame следующее:</span><span class="sxs-lookup"><span data-stu-id="04b53-121">Add the following to the list of IFrame decorators:</span></span>

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- <span data-ttu-id="04b53-122">Обязательно сохраните обновленный **файл Tab.ts.**</span><span class="sxs-lookup"><span data-stu-id="04b53-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="04b53-123">Код вкладки завершен.</span><span class="sxs-lookup"><span data-stu-id="04b53-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="04b53-124">Создание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="04b53-124">Build and Run Your Application</span></span>

<span data-ttu-id="04b53-125">Откройте командную подсказку в каталоге проектов для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="04b53-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="04b53-126">Чтобы просмотреть личную вкладку, перейдите к `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="04b53-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![снимок экрана личной вкладки](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="04b53-128">Создание безопасного туннеля на вкладке</span><span class="sxs-lookup"><span data-stu-id="04b53-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="04b53-129">Microsoft Teams — это полностью облачный продукт, который требует, чтобы содержимое вкладок было доступно в облаке с помощью конечных точек HTTPS.</span><span class="sxs-lookup"><span data-stu-id="04b53-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="04b53-130">Команды не позволяют локальному размещению, поэтому необходимо либо опубликовать вкладку на общедоступный URL-адрес, либо использовать прокси-сервер, который будет подвергать локальный порт URL-адресу, относящаяся к Интернету.</span><span class="sxs-lookup"><span data-stu-id="04b53-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="04b53-131">Чтобы протестировать расширение вкладки, вы будете использовать [ngrok,](https://ngrok.com/docs)встроенный в это приложение.</span><span class="sxs-lookup"><span data-stu-id="04b53-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="04b53-132">Ngrok — это средство обратного прокси-программного обеспечения, которое создаст туннель для общедоступных конечных точек HTTPS локального веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="04b53-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="04b53-133">Веб-точки сервера будут доступны во время текущего сеанса на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="04b53-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="04b53-134">Когда машина отключена или заснул, служба больше не будет доступна.</span><span class="sxs-lookup"><span data-stu-id="04b53-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="04b53-135">В командной подсказке выйдите из localhost и введите следующее:</span><span class="sxs-lookup"><span data-stu-id="04b53-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="04b53-136">После того как вкладка была загружена в microsoft teams с помощью *ngrok* и успешно сохранена, ее можно просмотреть в Teams до окончания сеанса туннеля.</span><span class="sxs-lookup"><span data-stu-id="04b53-136">After your tab has been uploaded to Microsoft teams, via *ngrok*, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="04b53-137">Отправка приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="04b53-137">Upload your application to Teams</span></span>

- <span data-ttu-id="04b53-138">Откройте клиент Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="04b53-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="04b53-139">Если вы используете [веб-версию,](https://teams.microsoft.com) вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="04b53-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="04b53-140">В панели *YourTeams* слева выберите меню рядом с командой, которую вы используете для тестирования вкладки, и `...` выберите команду **Manage.**</span><span class="sxs-lookup"><span data-stu-id="04b53-140">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="04b53-141">На главной панели выберите **Приложения** из панели вкладок и выберите **Загрузите** пользовательское приложение, расположенное в нижнем правом углу страницы.</span><span class="sxs-lookup"><span data-stu-id="04b53-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="04b53-142">Откройте каталог проектов, просмотрите **папку ./package,** выберите папку zip, щелкните правой кнопкой мыши и выберите **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="04b53-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="04b53-143">Вкладка будет загружена в Teams.</span><span class="sxs-lookup"><span data-stu-id="04b53-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="04b53-144">Просмотр личных вкладок</span><span class="sxs-lookup"><span data-stu-id="04b53-144">View your personal tabs</span></span>

<span data-ttu-id="04b53-145">В области navbar, расположенной слева от клиента Teams, выберите меню и выберите `...` приложение из списка.</span><span class="sxs-lookup"><span data-stu-id="04b53-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>
