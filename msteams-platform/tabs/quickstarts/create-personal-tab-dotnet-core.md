---
title: Создайте личную вкладку с ASP.NET Core
author: laujan
description: Краткое руководство по созданию пользовательских личных вкладку с ASP.NET Core.
ms.topic: quickstart
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 41aa916f4c69d50e48254d0f4934109429dab83c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566896"
---
# <a name="create-a-personal-tab-using-aspnetcore"></a><span data-ttu-id="fbd1a-103">Создание личной вкладки с помощью ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="fbd1a-103">Create a personal tab using ASP.NETCore</span></span>

<span data-ttu-id="fbd1a-104">В этом quickstart, мы будем ходить через создание пользовательских личных вкладку с C и ASP.Net Core Razor страниц.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-104">In this quickstart, we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="fbd1a-105">Мы также будем использовать [App Studio для Microsoft Teams для](~/concepts/build-and-test/app-studio-overview.md) завершения манифеста приложения и развертывания вкладки для Teams.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="fbd1a-106">Получить исходный код</span><span class="sxs-lookup"><span data-stu-id="fbd1a-106">Get the source code</span></span>

<span data-ttu-id="fbd1a-107">Откройте командный запрос и создайте новый каталог для вашего проекта вкладок.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="fbd1a-108">Мы предоставили простой проект, чтобы вы начали.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="fbd1a-109">Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в свой новый каталог:</span><span class="sxs-lookup"><span data-stu-id="fbd1a-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="fbd1a-110">Если у вас есть исходный код, откройте Visual Studio и **выберите Открыть проект или решение.**</span><span class="sxs-lookup"><span data-stu-id="fbd1a-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="fbd1a-111">Перейдите в каталог приложений вкладок и **откройте PersonalTab.sln**.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="fbd1a-112">Для создания и запуска приложения нажмите **F5 или** выберите **Start Debugging** из **меню отладки.**</span><span class="sxs-lookup"><span data-stu-id="fbd1a-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="fbd1a-113">В браузере перейдите на URL-адреса ниже, чтобы проверить приложение загружено должным образом:</span><span class="sxs-lookup"><span data-stu-id="fbd1a-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="fbd1a-114">Просмотр исходный код</span><span class="sxs-lookup"><span data-stu-id="fbd1a-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="fbd1a-115">Стартап.cs</span><span class="sxs-lookup"><span data-stu-id="fbd1a-115">Startup.cs</span></span>

<span data-ttu-id="fbd1a-116">Этот проект был создан из ASP.NET Core 2.2 Web Application пустой шаблон **с Расширенный - Настройка для HTTPS проверить окно** выбрано при настройке.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="fbd1a-117">Службы MVC регистрируются методом фреймворка впрыска `ConfigureServices()` зависимости.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="fbd1a-118">Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее программное обеспечение статических `Configure()` файлов:</span><span class="sxs-lookup"><span data-stu-id="fbd1a-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

```csharp
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

### <a name="wwwroot-folder"></a><span data-ttu-id="fbd1a-119">wwwroot папка</span><span class="sxs-lookup"><span data-stu-id="fbd1a-119">wwwroot folder</span></span>

<span data-ttu-id="fbd1a-120">В ASP.NET Core веб-папка—корень— это папка, в которой приложение ищет статические файлы.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="fbd1a-121">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="fbd1a-121">Index.cshtml</span></span>

<span data-ttu-id="fbd1a-122">ASP.NET Core рассматривает файлы под *названием Index* как страницу по умолчанию/домашнюю страницу для сайта.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="fbd1a-123">Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml будет** отображаться в качестве главной страницы для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="fbd1a-124">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="fbd1a-124">AppManifest folder</span></span>

<span data-ttu-id="fbd1a-125">Эта папка содержит следующие необходимые файлы пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="fbd1a-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="fbd1a-126">Значок **полного цвета** размером 192 х 192 пикселей.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="fbd1a-127">**Прозрачная иконка контура** размером 32 х 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="fbd1a-128">В **manifest.jsфайле,** в который указаны атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="fbd1a-129">Эти файлы должны быть застегнуты на молнии в пакете приложений для использования в загрузке вкладки, чтобы Teams.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="fbd1a-130">Microsoft Teams загрузит `contentUrl` указанное в манифесте, встраивает его в <iframe \> и отображает в вкладке.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an <iframe\>, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="fbd1a-131">.csproj</span><span class="sxs-lookup"><span data-stu-id="fbd1a-131">.csproj</span></span>

<span data-ttu-id="fbd1a-132">В окне Visual Studio Solution Explorer нажмите правой кнопкой мыши на проекте и выберите **Project файл.**</span><span class="sxs-lookup"><span data-stu-id="fbd1a-132">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="fbd1a-133">В нижней части файла вы увидите код, который создает и обновляет папку zip при сборке приложения:</span><span class="sxs-lookup"><span data-stu-id="fbd1a-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

```xml
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

[!INCLUDE  [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="fbd1a-134">Откройте подсказку команды в корне каталога проекта и запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fbd1a-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

- <span data-ttu-id="fbd1a-135">Ngrok будет слушать запросы из Интернета и будет маршрут их к вашему приложению, когда он работает на порт 44325.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="fbd1a-136">Он должен `https://y8rPrT2b.ngrok.io/` *напоминать, где y8rPrT2b* заменяется вашим ngrok альфа-числом HTTPS URL.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="fbd1a-137">Не забудьте сохранить подсказку команды с ngrok работает, и сделать заметку о URL - вам это понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

- <span data-ttu-id="fbd1a-138">**Убедитесь, что ngrok** работает и работает должным образом, открыв браузер и переходя на страницу содержимого через URL ngrok HTTPS, который был предоставлен в окне оперативной команды.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-138">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="fbd1a-139">Вы должны иметь как ваше приложение в Visual Studio ngrok работает, чтобы завершить этот быстрый старт.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="fbd1a-140">Если вам нужно прекратить запуск приложения в Visual Studio над ним, **продолжайте работать ngrok.**</span><span class="sxs-lookup"><span data-stu-id="fbd1a-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="fbd1a-141">Он будет продолжать слушать и возобновит маршрутизацию запроса вашего приложения, когда он перезапустится в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="fbd1a-142">Если вам придется перезапустить службу ngrok он вернет новый URL, и вам придется обновлять каждое место, которое использует этот URL.</span><span class="sxs-lookup"><span data-stu-id="fbd1a-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="fbd1a-143">Вы запустите приложение</span><span class="sxs-lookup"><span data-stu-id="fbd1a-143">Run your application</span></span>

- <span data-ttu-id="fbd1a-144">В Visual Studio **нажмите F5** или **выберите Start Debugging** из меню **отладки приложения.**</span><span class="sxs-lookup"><span data-stu-id="fbd1a-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="fbd1a-145">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="fbd1a-145">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fbd1a-146">Создание пользовательской персональной вкладки с помощью ASP.NETCore MVC</span><span class="sxs-lookup"><span data-stu-id="fbd1a-146">Create a Custom Personal Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
