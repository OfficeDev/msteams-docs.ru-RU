---
title: Создание личной вкладки с помощью ASP.NET Core
author: laujan
description: Руководство quickstart по созданию настраиваемой личной вкладки с ASP.NET Core.
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
# <a name="create-a-personal-tab-using-aspnetcore"></a><span data-ttu-id="83028-103">Создание личной вкладки с помощью ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="83028-103">Create a personal tab using ASP.NETCore</span></span>

<span data-ttu-id="83028-104">В этом quickstart мы создам настраиваемую личную вкладку со страницами C# ASP.Net Core Razor.</span><span class="sxs-lookup"><span data-stu-id="83028-104">In this quickstart, we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="83028-105">Мы также используем [App Studio для](~/concepts/build-and-test/app-studio-overview.md) Microsoft Teams манифеста приложения и развертывания вкладки Teams.</span><span class="sxs-lookup"><span data-stu-id="83028-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="83028-106">Получить исходный код</span><span class="sxs-lookup"><span data-stu-id="83028-106">Get the source code</span></span>

<span data-ttu-id="83028-107">Откройте командную подсказку и создайте новый каталог для проекта вкладки.</span><span class="sxs-lookup"><span data-stu-id="83028-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="83028-108">Мы предоставили простой проект для начала работы.</span><span class="sxs-lookup"><span data-stu-id="83028-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="83028-109">Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в новый каталог:</span><span class="sxs-lookup"><span data-stu-id="83028-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="83028-110">После того как у вас есть исходный код, откройте Visual Studio и выберите **Открыть проект или решение**.</span><span class="sxs-lookup"><span data-stu-id="83028-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="83028-111">Перейдите к каталогу приложений вкладок и откройте **PersonalTab.sln**.</span><span class="sxs-lookup"><span data-stu-id="83028-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="83028-112">Для создания и запуска приложения нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки.**</span><span class="sxs-lookup"><span data-stu-id="83028-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="83028-113">В браузере перейдите к URL-адресам ниже, чтобы проверить правильно загруженные приложения:</span><span class="sxs-lookup"><span data-stu-id="83028-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="83028-114">Просмотр исходных кодов</span><span class="sxs-lookup"><span data-stu-id="83028-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="83028-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="83028-115">Startup.cs</span></span>

<span data-ttu-id="83028-116">Этот проект был создан из пустого шаблона ASP.NET Core 2.2 веб-приложения с расширенным — настройка для контрольного окна **HTTPS,** выбранного при установке.</span><span class="sxs-lookup"><span data-stu-id="83028-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="83028-117">Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей.</span><span class="sxs-lookup"><span data-stu-id="83028-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="83028-118">Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее по статическим `Configure()` файлам:</span><span class="sxs-lookup"><span data-stu-id="83028-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="83028-119">папка wwwroot</span><span class="sxs-lookup"><span data-stu-id="83028-119">wwwroot folder</span></span>

<span data-ttu-id="83028-120">В ASP.NET Core веб-корневой папке приложение ищет статические файлы.</span><span class="sxs-lookup"><span data-stu-id="83028-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="83028-121">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="83028-121">Index.cshtml</span></span>

<span data-ttu-id="83028-122">ASP.NET Core обрабатывает файлы под названием *Index* в качестве домашней страницы по умолчанию для сайта.</span><span class="sxs-lookup"><span data-stu-id="83028-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="83028-123">Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** будет отображаться в качестве домашней страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="83028-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="83028-124">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="83028-124">AppManifest folder</span></span>

<span data-ttu-id="83028-125">Эта папка содержит следующие необходимые файлы пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="83028-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="83028-126">Значок **полного цвета** размером 192 x 192 пикселя.</span><span class="sxs-lookup"><span data-stu-id="83028-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="83028-127">Прозрачный **значок контура** размером 32 x 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="83028-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="83028-128">Файл **manifest.js,** который указывает атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="83028-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="83028-129">Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="83028-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="83028-130">Microsoft Teams загрузите указанное в манифесте, встраите его в <iframe и отрисуйте на `contentUrl` \> вкладке.</span><span class="sxs-lookup"><span data-stu-id="83028-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an <iframe\>, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="83028-131">.csproj</span><span class="sxs-lookup"><span data-stu-id="83028-131">.csproj</span></span>

<span data-ttu-id="83028-132">В окне Visual Studio обозревателя решений щелкните правой кнопкой мыши по проекту и выберите **Изменить Project Файл**.</span><span class="sxs-lookup"><span data-stu-id="83028-132">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="83028-133">В нижней части файла вы увидите код, который создает и обновляет папку zip при создании приложения:</span><span class="sxs-lookup"><span data-stu-id="83028-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="83028-134">Откройте командную подсказку в корневом каталоге проекта и запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="83028-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

- <span data-ttu-id="83028-135">Ngrok будет прослушивать запросы из Интернета и перенанастрает их в ваше приложение, когда оно запущено в порту 44325.</span><span class="sxs-lookup"><span data-stu-id="83028-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="83028-136">Он должен `https://y8rPrT2b.ngrok.io/` напоминать, где *y8rPrT2b* заменяется url-адресом https ngrok alpha-numeric HTTPS.</span><span class="sxs-lookup"><span data-stu-id="83028-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="83028-137">Убедитесь в том, что командная подсказка будет запущена с помощью ngrok, и обратите внимание на URL-адрес , который вам понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="83028-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

- <span data-ttu-id="83028-138">Убедитесь, что **ngrok** работает и работает должным образом, открыв браузер и переехав на страницу контента через URL-адрес https ngrok, который был представлен в окне командной подсказки.</span><span class="sxs-lookup"><span data-stu-id="83028-138">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="83028-139">Для выполнения этого quickstart необходимо Visual Studio и ngrok.</span><span class="sxs-lookup"><span data-stu-id="83028-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="83028-140">Если для работы с приложением необходимо прекратить Visual Studio, продолжайте **работать с ngrok.**</span><span class="sxs-lookup"><span data-stu-id="83028-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="83028-141">После перезапуска в Visual Studio он будет продолжать прослушивать запрос приложения и возобновлять маршрутиза Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83028-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="83028-142">Если вам придется перезапустить службу ngrok, она возвращает новый URL-адрес, и вам придется обновить каждое место, использующее этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="83028-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="83028-143">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="83028-143">Run your application</span></span>

- <span data-ttu-id="83028-144">В Visual Studio нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки** приложения.</span><span class="sxs-lookup"><span data-stu-id="83028-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="83028-145">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="83028-145">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="83028-146">Создание настраиваемой личной вкладки с помощью MVC ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="83028-146">Create a Custom Personal Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
