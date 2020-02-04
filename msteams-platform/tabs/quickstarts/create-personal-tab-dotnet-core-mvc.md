---
title: Создайте личную вкладку с ASP. NET Core MVC
author: laujan
description: Краткое руководство по созданию настраиваемой вкладки личных настроек с ASP. NET Core MVC.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 3bdd23692eca5ff3f6fc3f82cdaa233d34d4c69f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675166"
---
# <a name="create-a-custom-personal-tab-with-asp-net-core-mvc"></a><span data-ttu-id="530c7-105">Создайте настраиваемую вкладку личного кода с помощью ASP.</span><span class="sxs-lookup"><span data-stu-id="530c7-105">Create a Custom Personal Tab with ASP.</span></span> <span data-ttu-id="530c7-106">NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="530c7-106">NET Core MVC</span></span>

<span data-ttu-id="530c7-107">В этом руководстве мы рассмотрим создание настраиваемой вкладки личных настроек с помощью C# и ASP.</span><span class="sxs-lookup"><span data-stu-id="530c7-107">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.</span></span> <span data-ttu-id="530c7-108">NET Core MVC.</span><span class="sxs-lookup"><span data-stu-id="530c7-108">Net Core MVC.</span></span> <span data-ttu-id="530c7-109">Мы также используем [Приложение App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) , чтобы завершить манифест приложения и развернуть вкладку в Teams.</span><span class="sxs-lookup"><span data-stu-id="530c7-109">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="530c7-110">Получение исходного кода</span><span class="sxs-lookup"><span data-stu-id="530c7-110">Get the source code</span></span>

<span data-ttu-id="530c7-111">Откройте командную строку и создайте новый каталог для проекта со вкладками.</span><span class="sxs-lookup"><span data-stu-id="530c7-111">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="530c7-112">Мы предоставили простой проект, чтобы приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="530c7-112">We have provided a simple project to get you started.</span></span> <span data-ttu-id="530c7-113">Чтобы получить исходный код, можно скачать папку ZIP и извлечь файлы или клонировать репозиторий примера в новый каталог:</span><span class="sxs-lookup"><span data-stu-id="530c7-113">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="530c7-114">После создания исходного кода откройте Visual Studio и выберите **Открыть проект или решение**.</span><span class="sxs-lookup"><span data-stu-id="530c7-114">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="530c7-115">Перейдите в каталог приложений вкладки и откройте **персоналтабмвк. sln**.</span><span class="sxs-lookup"><span data-stu-id="530c7-115">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="530c7-116">Чтобы построить и запустить приложение, нажмите клавишу **F5** или в меню **Отладка** выберите команду **начать отладку** .</span><span class="sxs-lookup"><span data-stu-id="530c7-116">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="530c7-117">В браузере перейдите по приведенным ниже URL-адресам, чтобы убедиться, что приложение загружено правильно:</span><span class="sxs-lookup"><span data-stu-id="530c7-117">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="530c7-118">Просмотр исходного кода</span><span class="sxs-lookup"><span data-stu-id="530c7-118">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="530c7-119">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="530c7-119">Startup.cs</span></span>

<span data-ttu-id="530c7-120">Этот проект был создан на основе ASP.</span><span class="sxs-lookup"><span data-stu-id="530c7-120">This project was created from an ASP.</span></span> <span data-ttu-id="530c7-121">Веб-приложение NET Core 2,2 пустой шаблон с установленным флажком *Расширенная настройка для HTTPS* .</span><span class="sxs-lookup"><span data-stu-id="530c7-121">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="530c7-122">Службы MVC регистрируются `ConfigureServices()` методом платформы внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="530c7-122">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="530c7-123">Кроме того, по умолчанию в пустом шаблоне не включается возможность обслуживания статического содержимого, поэтому в `Configure()` метод добавляется промежуточное по промежуточным файлам.</span><span class="sxs-lookup"><span data-stu-id="530c7-123">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="530c7-124">Папка wwwroot</span><span class="sxs-lookup"><span data-stu-id="530c7-124">wwwroot folder</span></span>

<span data-ttu-id="530c7-125">В ASP.</span><span class="sxs-lookup"><span data-stu-id="530c7-125">In ASP.</span></span> <span data-ttu-id="530c7-126">Основной корневой каталог веб-сайта — это место, в котором приложение выполняет поиск статических файлов.</span><span class="sxs-lookup"><span data-stu-id="530c7-126">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="530c7-127">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="530c7-127">AppManifest folder</span></span>

<span data-ttu-id="530c7-128">Эта папка содержит следующие обязательные файлы пакета приложения:</span><span class="sxs-lookup"><span data-stu-id="530c7-128">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="530c7-129">**Значок с полным цветом** , измеряющий 192 x 192 пикселей.</span><span class="sxs-lookup"><span data-stu-id="530c7-129">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="530c7-130">**Прозрачный значок структуры** , измеряющий 32 x 32 пикселей.</span><span class="sxs-lookup"><span data-stu-id="530c7-130">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="530c7-131">Файл **manifest. JSON** , задающий атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="530c7-131">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="530c7-132">Эти файлы необходимо заархивировать в пакете приложения для использования при загрузке вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="530c7-132">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="530c7-133">Microsoft Teams загрузит `contentUrl` указанное в манифесте, внедрите его в IFRAME и откроет его на вкладке.</span><span class="sxs-lookup"><span data-stu-id="530c7-133">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="530c7-134">CSPROJ</span><span class="sxs-lookup"><span data-stu-id="530c7-134">.csproj</span></span>

<span data-ttu-id="530c7-135">В окне обозревателя решений Visual Studio щелкните правой кнопкой мыши проект и выберите команду **изменить файл проекта**.</span><span class="sxs-lookup"><span data-stu-id="530c7-135">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="530c7-136">В нижней части файла вы увидите код, который создает и обновляет папку zip при построении приложения:</span><span class="sxs-lookup"><span data-stu-id="530c7-136">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="530c7-137">Модели</span><span class="sxs-lookup"><span data-stu-id="530c7-137">Models</span></span>

<span data-ttu-id="530c7-138">*PersonalTab.CS* представляет объект сообщения и методы, которые будут вызываться из *персоналтабконтроллер* , когда пользователь нажимает кнопку в представлении *персоналтаб* .</span><span class="sxs-lookup"><span data-stu-id="530c7-138">*PersonalTab.cs* presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the *PersonalTab* View.</span></span>

### <a name="views"></a><span data-ttu-id="530c7-139">Представления</span><span class="sxs-lookup"><span data-stu-id="530c7-139">Views</span></span>

#### <a name="home"></a><span data-ttu-id="530c7-140">Главная</span><span class="sxs-lookup"><span data-stu-id="530c7-140">Home</span></span>

<span data-ttu-id="530c7-141">Стилей.</span><span class="sxs-lookup"><span data-stu-id="530c7-141">ASP.</span></span> <span data-ttu-id="530c7-142">NET Core рассматривает файлы с именем *index* как страницу по умолчанию или домашнюю страницу сайта.</span><span class="sxs-lookup"><span data-stu-id="530c7-142">NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="530c7-143">Если URL-адрес браузера указывает на корневой сайт сайта, в качестве домашней страницы для приложения будет отображаться *index. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="530c7-143">When your browser URL points to the root of the site, *Index.cshtml* will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="530c7-144">Shared</span><span class="sxs-lookup"><span data-stu-id="530c7-144">Shared</span></span>

<span data-ttu-id="530c7-145">Разметка частичного представления *_layout. cshtml* содержит общую структуру страницы и общие визуальные элементы приложения.</span><span class="sxs-lookup"><span data-stu-id="530c7-145">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="530c7-146">Он также будет ссылаться на библиотеку Teams.</span><span class="sxs-lookup"><span data-stu-id="530c7-146">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="530c7-147">Controller</span><span class="sxs-lookup"><span data-stu-id="530c7-147">Controllers</span></span>

<span data-ttu-id="530c7-148">Контроллеры используют свойство Виевбаг для динамического переноса значений в представлениях.</span><span class="sxs-lookup"><span data-stu-id="530c7-148">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="530c7-149">Откройте командную строку в корне каталога проекта и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="530c7-149">Open a command prompt in the root of your project directory and run the following command:</span></span>

``` bash
ngrok http https://localhost:44345 -host-header="localhost:44345"
```

* <span data-ttu-id="530c7-150">Ngrok прослушивает запросы из Интернета и направляет их в ваше приложение, когда оно выполняется на порте 44325.</span><span class="sxs-lookup"><span data-stu-id="530c7-150">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="530c7-151">Он должен выглядеть примерно `https://y8rPrT2b.ngrok.io/` так, где *y8rPrT2b* заменяется URL-адресом https ngrok, сооснованным на цифровом алфавите.</span><span class="sxs-lookup"><span data-stu-id="530c7-151">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="530c7-152">Убедитесь, что Командная строка ngrok запущена, и запишите URL-адрес, он понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="530c7-152">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="530c7-153">Убедитесь, что *ngrok* работает и правильно работает, открыв браузер и перейдя на страницу содержимого с помощью URL-адреса ngrok HTTPS, который был предоставлен в окне командной строки.</span><span class="sxs-lookup"><span data-stu-id="530c7-153">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> <span data-ttu-id="530c7-154">[!</span><span class="sxs-lookup"><span data-stu-id="530c7-154">[!</span></span> <span data-ttu-id="530c7-155">Совет] для выполнения этого краткого руководства необходимо, чтобы в Visual Studio и ngrok выполнялось приложение.</span><span class="sxs-lookup"><span data-stu-id="530c7-155">TIP] You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="530c7-156">Если вам нужно остановить работу приложения в Visual Studio для работы с ним, **Держите ngrok**в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="530c7-156">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="530c7-157">Он будет продолжать прослушивать и возобновить маршрутизацию запроса приложения при его перезапуске в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="530c7-157">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="530c7-158">Если необходимо перезапустить службу ngrok, будет возвращен новый URL-адрес, и вам потребуется обновить все место, где используется этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="530c7-158">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="530c7-159">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="530c7-159">Run your application</span></span>

* <span data-ttu-id="530c7-160">В Visual Studio нажмите клавишу **F5** или выберите команду **начать отладку** в меню **Отладка** приложения.</span><span class="sxs-lookup"><span data-stu-id="530c7-160">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
