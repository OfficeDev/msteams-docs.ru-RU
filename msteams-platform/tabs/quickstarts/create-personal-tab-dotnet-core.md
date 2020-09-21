---
title: Создание личной вкладки с ядром ASP.NET
author: laujan
description: Руководство по созданию настраиваемой личной вкладки с ядром ASP.NET.
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 21d1de18bfa8b7959cbecfe6eb50430ed8d3f3ec
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964580"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core"></a><span data-ttu-id="48031-103">Создание настраиваемой вкладки личных компонентов с ASP.NET</span><span class="sxs-lookup"><span data-stu-id="48031-103">Create a Custom Personal Tab with ASP.NET Core</span></span>

<span data-ttu-id="48031-104">В этом руководстве мы рассмотрим создание настраиваемой вкладки личного уровня с основными страницами Razor для C# и ASP.Net.</span><span class="sxs-lookup"><span data-stu-id="48031-104">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="48031-105">Мы также используем [Приложение App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) , чтобы завершить манифест приложения и развернуть вкладку в Teams.</span><span class="sxs-lookup"><span data-stu-id="48031-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="48031-106">Получение исходного кода</span><span class="sxs-lookup"><span data-stu-id="48031-106">Get the source code</span></span>

<span data-ttu-id="48031-107">Откройте командную строку и создайте новый каталог для проекта со вкладками.</span><span class="sxs-lookup"><span data-stu-id="48031-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="48031-108">Мы предоставили простой проект, чтобы приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="48031-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="48031-109">Чтобы получить исходный код, можно скачать папку ZIP и извлечь файлы или клонировать репозиторий примера в новый каталог:</span><span class="sxs-lookup"><span data-stu-id="48031-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="48031-110">После создания исходного кода откройте Visual Studio и выберите **Открыть проект или решение**.</span><span class="sxs-lookup"><span data-stu-id="48031-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="48031-111">Перейдите в каталог приложений вкладки и откройте **персоналтаб. sln**.</span><span class="sxs-lookup"><span data-stu-id="48031-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="48031-112">Чтобы построить и запустить приложение, нажмите клавишу **F5** или в меню **Отладка** выберите команду **начать отладку** .</span><span class="sxs-lookup"><span data-stu-id="48031-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="48031-113">В браузере перейдите по следующим URL-адресам, чтобы убедиться, что приложение загружено должным образом:</span><span class="sxs-lookup"><span data-stu-id="48031-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="48031-114">Просмотр исходного кода</span><span class="sxs-lookup"><span data-stu-id="48031-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="48031-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="48031-115">Startup.cs</span></span>

<span data-ttu-id="48031-116">Этот проект был создан из пустого шаблона веб-приложения ASP.NET Core 2,2 с установленным флажком *Расширенная настройка для HTTPS* , установленным во время установки.</span><span class="sxs-lookup"><span data-stu-id="48031-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="48031-117">Службы MVC регистрируются методом платформы внедрения зависимостей `ConfigureServices()` .</span><span class="sxs-lookup"><span data-stu-id="48031-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="48031-118">Кроме того, по умолчанию в пустом шаблоне не включается возможность обслуживания статического содержимого, поэтому в метод добавляется промежуточное по промежуточным файлам `Configure()` .</span><span class="sxs-lookup"><span data-stu-id="48031-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="48031-119">Папка wwwroot</span><span class="sxs-lookup"><span data-stu-id="48031-119">wwwroot folder</span></span>

<span data-ttu-id="48031-120">В ядре ASP.NET корневая папка веб-сайта — это место, в котором приложение выполняет поиск статических файлов.</span><span class="sxs-lookup"><span data-stu-id="48031-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="48031-121">Index. cshtml</span><span class="sxs-lookup"><span data-stu-id="48031-121">Index.cshtml</span></span>

<span data-ttu-id="48031-122">ASP.NET Core рассматривает файлы с именем *index* как страницу по умолчанию или домашнюю страницу сайта.</span><span class="sxs-lookup"><span data-stu-id="48031-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="48031-123">Если URL-адрес браузера указывает на корневой сайт сайта, в качестве домашней страницы для приложения будет отображаться **index. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="48031-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="48031-124">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="48031-124">AppManifest folder</span></span>

<span data-ttu-id="48031-125">Эта папка содержит следующие обязательные файлы пакета приложения:</span><span class="sxs-lookup"><span data-stu-id="48031-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="48031-126">**Значок с полным цветом** , измеряющий 192 x 192 пикселей.</span><span class="sxs-lookup"><span data-stu-id="48031-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="48031-127">**Прозрачный значок структуры** , измеряющий 32 x 32 пикселей.</span><span class="sxs-lookup"><span data-stu-id="48031-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="48031-128">**manifest.js** файла, определяющего атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="48031-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="48031-129">Эти файлы необходимо заархивировать в пакете приложения для использования при загрузке вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="48031-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="48031-130">Microsoft Teams загрузит `contentUrl` указанное в манифесте, внедрите его в IFRAME и откроет его на вкладке.</span><span class="sxs-lookup"><span data-stu-id="48031-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="48031-131">CSPROJ</span><span class="sxs-lookup"><span data-stu-id="48031-131">.csproj</span></span>

<span data-ttu-id="48031-132">В окне обозревателя решений Visual Studio щелкните правой кнопкой мыши проект и выберите команду **изменить файл проекта**.</span><span class="sxs-lookup"><span data-stu-id="48031-132">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="48031-133">В нижней части файла вы увидите код, который создает и обновляет папку zip при построении приложения:</span><span class="sxs-lookup"><span data-stu-id="48031-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="48031-134">Откройте командную строку в корне каталога проекта и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="48031-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:44325 -host-header="localhost:44325"
```

- <span data-ttu-id="48031-135">Ngrok прослушивает запросы из Интернета и направляет их в ваше приложение, когда оно выполняется на порте 44325.</span><span class="sxs-lookup"><span data-stu-id="48031-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="48031-136">Он должен выглядеть примерно так `https://y8rPrT2b.ngrok.io/` , где *y8rPrT2b* ЗАМЕНЯЕТСЯ URL-адресом https ngrok, сооснованным на цифровом алфавите.</span><span class="sxs-lookup"><span data-stu-id="48031-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="48031-137">Убедитесь, что Командная строка ngrok запущена, и запишите URL-адрес, он понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="48031-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL—you'll need it later.</span></span>

- <span data-ttu-id="48031-138">Убедитесь, что *ngrok* работает и правильно работает, открыв браузер и перейдя на страницу содержимого с помощью URL-адреса ngrok HTTPS, который был предоставлен в окне командной строки.</span><span class="sxs-lookup"><span data-stu-id="48031-138">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="48031-139">Для выполнения этого краткого руководства необходимо одновременное выполнение приложения в Visual Studio и ngrok.</span><span class="sxs-lookup"><span data-stu-id="48031-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="48031-140">Если вам нужно остановить работу приложения в Visual Studio для работы с ним, **Держите ngrok**в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="48031-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="48031-141">Он будет продолжать прослушивать и возобновить маршрутизацию запроса приложения при его перезапуске в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="48031-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="48031-142">Если необходимо перезапустить службу ngrok, будет возвращен новый URL-адрес, и вам потребуется обновить все место, где используется этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="48031-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="48031-143">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="48031-143">Run your application</span></span>

- <span data-ttu-id="48031-144">В Visual Studio нажмите клавишу **F5** или выберите команду **начать отладку** в меню **Отладка** приложения.</span><span class="sxs-lookup"><span data-stu-id="48031-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
