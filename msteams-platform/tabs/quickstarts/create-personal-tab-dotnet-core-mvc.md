---
title: Создайте личную вкладку с помощью ASP. NET Core MVC
author: laujan
description: Краткое руководство по созданию пользовательских личных вкладку с ASP. NET Core MVC.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 01418adb32335660bb20f74ecfaa0e7e27230c93
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566635"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a><span data-ttu-id="dbeef-105">Создание пользовательской персональной вкладки с ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="dbeef-105">Create a Custom Personal Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="dbeef-106">В этом quickstart мы будем ходить через создание пользовательских личных вкладку с C и ASP.Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="dbeef-106">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="dbeef-107">Мы также будем использовать [App Studio для Microsoft Teams для](~/concepts/build-and-test/app-studio-overview.md) завершения манифеста приложения и развертывания вкладки для Teams.</span><span class="sxs-lookup"><span data-stu-id="dbeef-107">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="dbeef-108">Получить исходный код</span><span class="sxs-lookup"><span data-stu-id="dbeef-108">Get the source code</span></span>

<span data-ttu-id="dbeef-109">Откройте командный запрос и создайте новый каталог для вашего проекта вкладок.</span><span class="sxs-lookup"><span data-stu-id="dbeef-109">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="dbeef-110">Мы предоставили простой проект, чтобы вы начали.</span><span class="sxs-lookup"><span data-stu-id="dbeef-110">We have provided a simple project to get you started.</span></span> <span data-ttu-id="dbeef-111">Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в свой новый каталог:</span><span class="sxs-lookup"><span data-stu-id="dbeef-111">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="dbeef-112">Если у вас есть исходный код, откройте Visual Studio и **выберите Открыть проект или решение.**</span><span class="sxs-lookup"><span data-stu-id="dbeef-112">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="dbeef-113">Перейдите в каталог приложений вкладок и **откройте PersonalTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="dbeef-113">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="dbeef-114">Для создания и запуска приложения нажмите **F5 или** выберите **Start Debugging** из **меню отладки.**</span><span class="sxs-lookup"><span data-stu-id="dbeef-114">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="dbeef-115">В браузере перейдите на URL-адреса ниже, чтобы убедиться, что приложение загружено должным образом:</span><span class="sxs-lookup"><span data-stu-id="dbeef-115">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="dbeef-116">Просмотр исходный код</span><span class="sxs-lookup"><span data-stu-id="dbeef-116">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="dbeef-117">Стартап.cs</span><span class="sxs-lookup"><span data-stu-id="dbeef-117">Startup.cs</span></span>

<span data-ttu-id="dbeef-118">Этот проект был создан из ASP.</span><span class="sxs-lookup"><span data-stu-id="dbeef-118">This project was created from an ASP.</span></span> <span data-ttu-id="dbeef-119">NET Core 2.2 Web Application пустой шаблон с *Расширенный - Настройка для https проверить окно* выбрано при настройке.</span><span class="sxs-lookup"><span data-stu-id="dbeef-119">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="dbeef-120">Службы MVC регистрируются методом фреймворка впрыска `ConfigureServices()` зависимости.</span><span class="sxs-lookup"><span data-stu-id="dbeef-120">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="dbeef-121">Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее программное обеспечение статических `Configure()` файлов:</span><span class="sxs-lookup"><span data-stu-id="dbeef-121">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

``` csharp
public void ConfigureServices(IServiceCollection services)
  {
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

### <a name="wwwroot-folder"></a><span data-ttu-id="dbeef-122">wwwroot папка</span><span class="sxs-lookup"><span data-stu-id="dbeef-122">wwwroot folder</span></span>

<span data-ttu-id="dbeef-123">В ASP.</span><span class="sxs-lookup"><span data-stu-id="dbeef-123">In ASP.</span></span> <span data-ttu-id="dbeef-124">NET Core, папка веб-корня, где приложение ищет статические файлы.</span><span class="sxs-lookup"><span data-stu-id="dbeef-124">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="dbeef-125">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="dbeef-125">AppManifest folder</span></span>

<span data-ttu-id="dbeef-126">Эта папка содержит следующие необходимые файлы пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="dbeef-126">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="dbeef-127">Значок **полного цвета** размером 192 х 192 пикселей.</span><span class="sxs-lookup"><span data-stu-id="dbeef-127">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="dbeef-128">**Прозрачная иконка контура** размером 32 х 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="dbeef-128">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="dbeef-129">В **manifest.jsфайле,** в который указаны атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="dbeef-129">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="dbeef-130">Эти файлы должны быть застегнуты на молнии в пакете приложений для использования в загрузке вкладки, чтобы Teams.</span><span class="sxs-lookup"><span data-stu-id="dbeef-130">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="dbeef-131">Microsoft Teams загрузит `contentUrl` указанное в манифесте, встраивает его в IFrame и отображает в вкладке.</span><span class="sxs-lookup"><span data-stu-id="dbeef-131">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="dbeef-132">.csproj</span><span class="sxs-lookup"><span data-stu-id="dbeef-132">.csproj</span></span>

<span data-ttu-id="dbeef-133">В окне Visual Studio Solution Explorer нажмите правой кнопкой мыши на проект и выберите **Редактировать Project файл**.</span><span class="sxs-lookup"><span data-stu-id="dbeef-133">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="dbeef-134">В нижней части файла вы увидите код, который создает и обновляет папку zip при сборке приложения:</span><span class="sxs-lookup"><span data-stu-id="dbeef-134">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

``` xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

### <a name="models"></a><span data-ttu-id="dbeef-135">Модели</span><span class="sxs-lookup"><span data-stu-id="dbeef-135">Models</span></span>

<span data-ttu-id="dbeef-136">**PersonalTab.cs** представляет объект сообщения и методы, которые будут *вызваны из PersonalTabController,* когда пользователь выберет кнопку **в представлении PersonalTab.**</span><span class="sxs-lookup"><span data-stu-id="dbeef-136">**PersonalTab.cs** presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the **PersonalTab** View.</span></span>

### <a name="views"></a><span data-ttu-id="dbeef-137">Представления</span><span class="sxs-lookup"><span data-stu-id="dbeef-137">Views</span></span>

#### <a name="home"></a><span data-ttu-id="dbeef-138">Главная</span><span class="sxs-lookup"><span data-stu-id="dbeef-138">Home</span></span>

<span data-ttu-id="dbeef-139">гадюка.</span><span class="sxs-lookup"><span data-stu-id="dbeef-139">ASP.</span></span> <span data-ttu-id="dbeef-140">NET Core рассматривает файлы, **называемые Index,** как по умолчанию или домашнюю страницу для сайта.</span><span class="sxs-lookup"><span data-stu-id="dbeef-140">NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="dbeef-141">Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml будет** отображаться в качестве главной страницы для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="dbeef-141">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="dbeef-142">Shared</span><span class="sxs-lookup"><span data-stu-id="dbeef-142">Shared</span></span>

<span data-ttu-id="dbeef-143">Частичная разметка представления *_Layout.cshtml содержит* общую структуру страницы приложения и общие визуальные элементы.</span><span class="sxs-lookup"><span data-stu-id="dbeef-143">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="dbeef-144">Он также будет ссылаться на Teams библиотеку.</span><span class="sxs-lookup"><span data-stu-id="dbeef-144">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="dbeef-145">Контроллеры</span><span class="sxs-lookup"><span data-stu-id="dbeef-145">Controllers</span></span>

<span data-ttu-id="dbeef-146">Контроллеры используют свойство ViewBag для динамической передачи значений представлениям.</span><span class="sxs-lookup"><span data-stu-id="dbeef-146">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="dbeef-147">Откройте подсказку команды в корне каталога проекта и запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dbeef-147">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

* <span data-ttu-id="dbeef-148">Ngrok будет слушать запросы из Интернета и будет маршрут их к вашему приложению, когда он работает на порт 44325.</span><span class="sxs-lookup"><span data-stu-id="dbeef-148">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="dbeef-149">Он должен `https://y8rPrT2b.ngrok.io/` *напоминать, где y8rPrT2b* заменяется вашим ngrok альфа-числом HTTPS URL.</span><span class="sxs-lookup"><span data-stu-id="dbeef-149">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="dbeef-150">Не забудьте сохранить подсказку команды с ngrok работает, и сделать заметку о URL - вам это понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="dbeef-150">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="dbeef-151">**Убедитесь, что ngrok** работает и работает должным образом, открыв браузер и переходя на страницу содержимого через URL ngrok HTTPS, который был предоставлен в окне оперативной команды.</span><span class="sxs-lookup"><span data-stu-id="dbeef-151">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="dbeef-152">Вы должны иметь как ваше приложение в Visual Studio ngrok работает, чтобы завершить этот быстрый старт.</span><span class="sxs-lookup"><span data-stu-id="dbeef-152">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="dbeef-153">Если вам нужно прекратить запуск приложения в Visual Studio над ним, **продолжайте работать ngrok.**</span><span class="sxs-lookup"><span data-stu-id="dbeef-153">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="dbeef-154">Он будет продолжать слушать и возобновит маршрутизацию запроса вашего приложения, когда он перезапустится в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbeef-154">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="dbeef-155">Если вам придется перезапустить службу ngrok он вернет новый URL, и вам придется обновлять каждое место, которое использует этот URL.</span><span class="sxs-lookup"><span data-stu-id="dbeef-155">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="dbeef-156">Вы запустите приложение</span><span class="sxs-lookup"><span data-stu-id="dbeef-156">Run your application</span></span>

* <span data-ttu-id="dbeef-157">В Visual Studio **нажмите F5** или **выберите Start Debugging** из меню **отладки приложения.**</span><span class="sxs-lookup"><span data-stu-id="dbeef-157">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="dbeef-158">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="dbeef-158">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dbeef-159">Создайте пользовательский канал и групповую вкладку, Node.js и генератор Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dbeef-159">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-channel-group-tab-node-yeoman.md)
