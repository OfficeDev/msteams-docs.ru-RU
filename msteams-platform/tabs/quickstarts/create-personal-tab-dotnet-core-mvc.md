---
title: Создание личной вкладки с помощью ASP. NET Core MVC
author: surbhigupta
description: Руководство quickstart по созданию настраиваемой личной вкладки с помощью ASP. NET Core MVC.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: ac01ae64f44ccf3e06476d4412b16ac9a4730f6c
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069149"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a><span data-ttu-id="69bb4-105">Создание настраиваемой личной вкладки с ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="69bb4-105">Create a Custom Personal Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="69bb4-106">В этом quickstart мы создам настраиваемую личную вкладку с C# и ASP.Net core MVC.</span><span class="sxs-lookup"><span data-stu-id="69bb4-106">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="69bb4-107">Мы также используем [App Studio для](~/concepts/build-and-test/app-studio-overview.md) Microsoft Teams манифеста приложения и развертывания вкладки Teams.</span><span class="sxs-lookup"><span data-stu-id="69bb4-107">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="69bb4-108">Получить исходный код</span><span class="sxs-lookup"><span data-stu-id="69bb4-108">Get the source code</span></span>

<span data-ttu-id="69bb4-109">Откройте командную подсказку и создайте новый каталог для проекта вкладки.</span><span class="sxs-lookup"><span data-stu-id="69bb4-109">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="69bb4-110">Мы предоставили простой проект для начала работы.</span><span class="sxs-lookup"><span data-stu-id="69bb4-110">We have provided a simple project to get you started.</span></span> <span data-ttu-id="69bb4-111">Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в новый каталог:</span><span class="sxs-lookup"><span data-stu-id="69bb4-111">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="69bb4-112">После того как у вас есть исходный код, откройте Visual Studio и выберите **Открыть проект или решение**.</span><span class="sxs-lookup"><span data-stu-id="69bb4-112">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="69bb4-113">Перейдите к каталогу приложений вкладок и откройте **PersonalTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="69bb4-113">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="69bb4-114">Для создания и запуска приложения нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки.**</span><span class="sxs-lookup"><span data-stu-id="69bb4-114">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="69bb4-115">В браузере перейдите к URL-адресам ниже, чтобы убедиться, что приложение загружено правильно:</span><span class="sxs-lookup"><span data-stu-id="69bb4-115">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="69bb4-116">Просмотр исходных кодов</span><span class="sxs-lookup"><span data-stu-id="69bb4-116">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="69bb4-117">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="69bb4-117">Startup.cs</span></span>

<span data-ttu-id="69bb4-118">Этот проект был создан из asP.</span><span class="sxs-lookup"><span data-stu-id="69bb4-118">This project was created from an ASP.</span></span> <span data-ttu-id="69bb4-119">Net Core 2.2 Веб-приложение пустой шаблон с *расширенным - Настройка для https* check box, выбранного при установке.</span><span class="sxs-lookup"><span data-stu-id="69bb4-119">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="69bb4-120">Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей.</span><span class="sxs-lookup"><span data-stu-id="69bb4-120">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="69bb4-121">Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее по статическим `Configure()` файлам:</span><span class="sxs-lookup"><span data-stu-id="69bb4-121">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="69bb4-122">папка wwwroot</span><span class="sxs-lookup"><span data-stu-id="69bb4-122">wwwroot folder</span></span>

<span data-ttu-id="69bb4-123">В ASP.</span><span class="sxs-lookup"><span data-stu-id="69bb4-123">In ASP.</span></span> <span data-ttu-id="69bb4-124">NET Core — это веб-корневая папка, в которой приложение ищет статические файлы.</span><span class="sxs-lookup"><span data-stu-id="69bb4-124">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="69bb4-125">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="69bb4-125">AppManifest folder</span></span>

<span data-ttu-id="69bb4-126">Эта папка содержит следующие необходимые файлы пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="69bb4-126">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="69bb4-127">Значок **полного цвета** размером 192 x 192 пикселя.</span><span class="sxs-lookup"><span data-stu-id="69bb4-127">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="69bb4-128">Прозрачный **значок контура** размером 32 x 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="69bb4-128">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="69bb4-129">Файл **manifest.js,** который указывает атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="69bb4-129">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="69bb4-130">Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="69bb4-130">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="69bb4-131">Microsoft Teams загрузите указанное в манифесте, встраите его в `contentUrl` IFrame и отрисуйте на вкладке.</span><span class="sxs-lookup"><span data-stu-id="69bb4-131">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="69bb4-132">.csproj</span><span class="sxs-lookup"><span data-stu-id="69bb4-132">.csproj</span></span>

<span data-ttu-id="69bb4-133">В окне Visual Studio Обозреватель решений щелкните правой кнопкой мыши по проекту и выберите **Изменить Project файл**.</span><span class="sxs-lookup"><span data-stu-id="69bb4-133">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="69bb4-134">В нижней части файла вы увидите код, который создает и обновляет папку zip при создании приложения:</span><span class="sxs-lookup"><span data-stu-id="69bb4-134">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="69bb4-135">Модели</span><span class="sxs-lookup"><span data-stu-id="69bb4-135">Models</span></span>

<span data-ttu-id="69bb4-136">**PersonalTab.cs** представляет объект Сообщения и методы, которые будут вызваны из *PersonalTabController,* когда пользователь выбирает кнопку в **представлении PersonalTab.**</span><span class="sxs-lookup"><span data-stu-id="69bb4-136">**PersonalTab.cs** presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the **PersonalTab** View.</span></span>

### <a name="views"></a><span data-ttu-id="69bb4-137">Представления</span><span class="sxs-lookup"><span data-stu-id="69bb4-137">Views</span></span>

#### <a name="home"></a><span data-ttu-id="69bb4-138">Главная</span><span class="sxs-lookup"><span data-stu-id="69bb4-138">Home</span></span>

<span data-ttu-id="69bb4-139">ASP.</span><span class="sxs-lookup"><span data-stu-id="69bb4-139">ASP.</span></span> <span data-ttu-id="69bb4-140">NET Core обрабатывает файлы **index** как страницу по умолчанию или домашняя страница для сайта.</span><span class="sxs-lookup"><span data-stu-id="69bb4-140">NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="69bb4-141">Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** будет отображаться в качестве домашней страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="69bb4-141">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="69bb4-142">Shared</span><span class="sxs-lookup"><span data-stu-id="69bb4-142">Shared</span></span>

<span data-ttu-id="69bb4-143">Частичная разметка *_Layout.cshtml* содержит общую структуру страницы приложения и общие визуальные элементы.</span><span class="sxs-lookup"><span data-stu-id="69bb4-143">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="69bb4-144">Он также будет ссылаться на Teams библиотеку.</span><span class="sxs-lookup"><span data-stu-id="69bb4-144">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="69bb4-145">Контроллеры</span><span class="sxs-lookup"><span data-stu-id="69bb4-145">Controllers</span></span>

<span data-ttu-id="69bb4-146">Контроллеры используют свойство ViewBag для динамической передачи значений в Представления.</span><span class="sxs-lookup"><span data-stu-id="69bb4-146">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="69bb4-147">Откройте командную подсказку в корневом каталоге проекта и запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="69bb4-147">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

* <span data-ttu-id="69bb4-148">Ngrok будет прослушивать запросы из Интернета и перенанастрает их в ваше приложение, когда оно запущено в порту 44325.</span><span class="sxs-lookup"><span data-stu-id="69bb4-148">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="69bb4-149">Он должен `https://y8rPrT2b.ngrok.io/` напоминать, где *y8rPrT2b* заменяется url-адресом https ngrok alpha-numeric HTTPS.</span><span class="sxs-lookup"><span data-stu-id="69bb4-149">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="69bb4-150">Убедитесь в том, что командная подсказка будет запущена с помощью ngrok, и обратите внимание на URL-адрес , который вам понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="69bb4-150">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="69bb4-151">Убедитесь, что **ngrok** работает и работает должным образом, открыв браузер и переехав на страницу контента через URL-адрес https ngrok, который был представлен в окне командной подсказки.</span><span class="sxs-lookup"><span data-stu-id="69bb4-151">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="69bb4-152">Для выполнения этого quickstart необходимо Visual Studio и ngrok.</span><span class="sxs-lookup"><span data-stu-id="69bb4-152">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="69bb4-153">Если для работы с приложением необходимо прекратить Visual Studio, продолжайте **работать с ngrok.**</span><span class="sxs-lookup"><span data-stu-id="69bb4-153">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="69bb4-154">После перезапуска в Visual Studio он будет продолжать прослушивать запрос приложения и возобновлять маршрутиза Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="69bb4-154">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="69bb4-155">Если вам придется перезапустить службу ngrok, она возвращает новый URL-адрес, и вам придется обновить каждое место, использующее этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="69bb4-155">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="69bb4-156">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="69bb4-156">Run your application</span></span>

* <span data-ttu-id="69bb4-157">В Visual Studio нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки** приложения.</span><span class="sxs-lookup"><span data-stu-id="69bb4-157">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="69bb4-158">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="69bb4-158">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="69bb4-159">Создание настраиваемой вкладки канала и группы с Node.js и генератора Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="69bb4-159">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-channel-group-tab-node-yeoman.md)
