---
title: 'Краткое руководство: Создание настраиваемой вкладки личных настроек с Node. js и генератором Yeoman для Microsoft Teams'
author: laujan
description: Руководство по созданию личных вкладок с генератором Yeoman для Microsoft Teams.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 2d1b17360b92a161179091c1f6ba06ffa194e958
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675161"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="57fda-103">Краткое руководство: Создание настраиваемой вкладки личных настроек с Node. js и генератором Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="57fda-103">Quickstart: Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="57fda-104">Это руководство соответствует действиям, описанным в статье [Создание первого вики-сайта приложения Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) , который находится в репозитории Microsoft OfficeDev GitHub.</span><span class="sxs-lookup"><span data-stu-id="57fda-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="57fda-105">В этом руководстве мы рассмотрим создание настраиваемой вкладки с помощью [генератора Yeoman Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="57fda-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="57fda-106">Мы также загружаем приложение в группу.</span><span class="sxs-lookup"><span data-stu-id="57fda-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="57fda-107">**Вы хотите создать настраиваемую или статическую вкладку?**</span><span class="sxs-lookup"><span data-stu-id="57fda-107">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="57fda-108">С помощью клавиш со стрелками выберите статическую вкладку.</span><span class="sxs-lookup"><span data-stu-id="57fda-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="57fda-109">Компонент Path *йоурдефаулттабнаметаб*, указанный в этом кратком руководстве, — это значение, введенное в генератор для *имени вкладки по умолчанию* , а также для *вкладки*Word.</span><span class="sxs-lookup"><span data-stu-id="57fda-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="57fda-110">Пример: дефаулттабнаме: *митаб* => */митабтаб/*</span><span class="sxs-lookup"><span data-stu-id="57fda-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="57fda-111">Создание вкладки "личные"</span><span class="sxs-lookup"><span data-stu-id="57fda-111">Create your personal tab</span></span>

<span data-ttu-id="57fda-112">Чтобы добавить в это приложение вкладку Личные, вы создадите страницу контента и обновите существующие файлы:</span><span class="sxs-lookup"><span data-stu-id="57fda-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="57fda-113">В редакторе кода создайте новый HTML-файл **Personal. HTML** и добавьте следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="57fda-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="57fda-114">Сохраните **личный. HTML** в **веб-** папке приложения:</span><span class="sxs-lookup"><span data-stu-id="57fda-114">Save **personal.html** in your application's **web** folder:</span></span>

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- <span data-ttu-id="57fda-115">Откройте **манифест. JSON** в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="57fda-115">Open **manifest.json** in your code editor:</span></span>

```bash
./src/manifest/manifest.json/
```

<span data-ttu-id="57fda-116">Добавьте следующий код в пустой `staticTabs` массив (`staticTabs":[]`) и добавьте следующий объект JSON:</span><span class="sxs-lookup"><span data-stu-id="57fda-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="57fda-117">Не забудьте обновить компонент пути **"contentURL"** **йоурдефаулттабнаметаб** с именем текущей вкладки.</span><span class="sxs-lookup"><span data-stu-id="57fda-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="57fda-118">Сохраните обновленный **манифест. JSON**.</span><span class="sxs-lookup"><span data-stu-id="57fda-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="57fda-119">Страница контента должна обслуживаться в IFrame.</span><span class="sxs-lookup"><span data-stu-id="57fda-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="57fda-120">Откройте **вкладку "TS"** в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="57fda-120">Open **Tab.ts** in your code editor:</span></span>

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- <span data-ttu-id="57fda-121">Добавьте следующие элементы в список декораторов IFrame:</span><span class="sxs-lookup"><span data-stu-id="57fda-121">Add the following to the list of IFrame decorators:</span></span>

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- <span data-ttu-id="57fda-122">Обязательно сохраните обновленный файл **TAB. TS** .</span><span class="sxs-lookup"><span data-stu-id="57fda-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="57fda-123">Ваш код табуляции заполнен.</span><span class="sxs-lookup"><span data-stu-id="57fda-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="57fda-124">Построение и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="57fda-124">Build and Run Your Application</span></span>

<span data-ttu-id="57fda-125">Откройте командную строку в каталоге проекта, чтобы выполнить следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="57fda-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="57fda-126">Чтобы просмотреть вкладку Личные, перейдите на страницу`http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="57fda-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![снимок экрана: вкладка "личные"](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="57fda-128">Установка безопасного туннеля для вкладки</span><span class="sxs-lookup"><span data-stu-id="57fda-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="57fda-129">Microsoft Teams является полностью облачным продуктом и требует, чтобы содержимое вкладки было доступно из облака с использованием конечных точек HTTPS.</span><span class="sxs-lookup"><span data-stu-id="57fda-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="57fda-130">В Teams не разрешается локальное размещение, поэтому необходимо либо опубликовать вкладку на общедоступном URL-адресе, либо использовать прокси-сервер, который будет предоставлять локальный порт URL-адресу, доступному для выхода в Интернет.</span><span class="sxs-lookup"><span data-stu-id="57fda-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="57fda-131">Чтобы протестировать расширение вкладки, вы будете использовать [ngrok](https://ngrok.com/docs), встроенный в это приложение.</span><span class="sxs-lookup"><span data-stu-id="57fda-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="57fda-132">Ngrok — это программное средство обратного прокси-сервера, которое создает туннель для общедоступных конечных точек HTTPS на локальном веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="57fda-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="57fda-133">Конечные точки веб-сервера будут доступны в текущем сеансе на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="57fda-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="57fda-134">При завершении работы компьютера или переходе в спящий режим служба становится недоступной.</span><span class="sxs-lookup"><span data-stu-id="57fda-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="57fda-135">В командной строки выйдите из localhost и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="57fda-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="57fda-136">После отправки вкладки в Microsoft Teams с помощью *ngrok*и успешного сохранения его можно просмотреть в Teams до завершения сеанса туннеля.</span><span class="sxs-lookup"><span data-stu-id="57fda-136">After your tab has been uploaded to Microsoft teams, via *ngrok*, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="57fda-137">Отправка приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="57fda-137">Upload your application to Teams</span></span>

- <span data-ttu-id="57fda-138">Откройте клиент Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="57fda-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="57fda-139">Если вы используете [версию на основе веб-сайта](https://teams.microsoft.com) , вы можете проверить интерфейсный код с помощью [средств разработчика](~/tabs/how-to/developer-tools.md)в браузере.</span><span class="sxs-lookup"><span data-stu-id="57fda-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="57fda-140">На панели *йоуртеамс* слева выберите `...` меню рядом с командой, которую вы используете для тестирования вкладки, и выберите пункт **Управление командой**.</span><span class="sxs-lookup"><span data-stu-id="57fda-140">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="57fda-141">В главной панели выберите **приложения** из панели вкладок и нажмите кнопку **Отправить пользовательское приложение** , расположенное в правом нижнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="57fda-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="57fda-142">Откройте каталог проекта, перейдите в папку **./паккаже** , выберите папку ZIP, щелкните правой кнопкой мыши и выберите команду **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="57fda-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="57fda-143">Вкладка будет загружена в Teams.</span><span class="sxs-lookup"><span data-stu-id="57fda-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="57fda-144">Просмотр личных вкладок</span><span class="sxs-lookup"><span data-stu-id="57fda-144">View your personal tabs</span></span>

<span data-ttu-id="57fda-145">В панели навигации, расположенной в левой части клиента Teams, выберите `...` меню и выберите приложение из списка.</span><span class="sxs-lookup"><span data-stu-id="57fda-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>
