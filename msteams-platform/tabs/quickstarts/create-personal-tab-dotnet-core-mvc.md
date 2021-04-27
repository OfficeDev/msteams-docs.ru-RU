---
title: Создание личной вкладки с помощью ASP. NET Core MVC
author: laujan
description: Руководство quickstart по созданию настраиваемой личной вкладки с помощью ASP. NET Core MVC.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 3ec6b5c054384653e30e46cbffed4a2af6662c33
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019568"
---
# <a name="create-a-custom-personal-tab-with-asp-net-core-mvc"></a><span data-ttu-id="2e295-105">Создайте настраиваемую личную вкладку с помощью ASP.</span><span class="sxs-lookup"><span data-stu-id="2e295-105">Create a Custom Personal Tab with ASP.</span></span> <span data-ttu-id="2e295-106">NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="2e295-106">NET Core MVC</span></span>

<span data-ttu-id="2e295-107">В этом quickstart мы создам настраиваемую личную вкладку с C# и ASP.</span><span class="sxs-lookup"><span data-stu-id="2e295-107">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.</span></span> <span data-ttu-id="2e295-108">Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="2e295-108">Net Core MVC.</span></span> <span data-ttu-id="2e295-109">Кроме того, мы будем использовать [App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) для окончательного развертывания манифеста приложения и развертывания вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="2e295-109">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="2e295-110">Получить исходный код</span><span class="sxs-lookup"><span data-stu-id="2e295-110">Get the source code</span></span>

<span data-ttu-id="2e295-111">Откройте командную подсказку и создайте новый каталог для проекта вкладки.</span><span class="sxs-lookup"><span data-stu-id="2e295-111">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="2e295-112">Мы предоставили простой проект для начала работы.</span><span class="sxs-lookup"><span data-stu-id="2e295-112">We have provided a simple project to get you started.</span></span> <span data-ttu-id="2e295-113">Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в новый каталог:</span><span class="sxs-lookup"><span data-stu-id="2e295-113">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="2e295-114">После того как у вас есть исходный код, откройте Visual Studio и выберите **Открыть проект или решение**.</span><span class="sxs-lookup"><span data-stu-id="2e295-114">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="2e295-115">Перейдите к каталогу приложений вкладок и откройте **PersonalTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="2e295-115">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="2e295-116">Для создания и запуска приложения нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки.**</span><span class="sxs-lookup"><span data-stu-id="2e295-116">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="2e295-117">В браузере перейдите к URL-адресам ниже, чтобы убедиться, что приложение загружено правильно:</span><span class="sxs-lookup"><span data-stu-id="2e295-117">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="2e295-118">Просмотр исходных кодов</span><span class="sxs-lookup"><span data-stu-id="2e295-118">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="2e295-119">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="2e295-119">Startup.cs</span></span>

<span data-ttu-id="2e295-120">Этот проект был создан из asP.</span><span class="sxs-lookup"><span data-stu-id="2e295-120">This project was created from an ASP.</span></span> <span data-ttu-id="2e295-121">Net Core 2.2 Веб-приложение пустой шаблон с *расширенным - Настройка для https* check box, выбранного при установке.</span><span class="sxs-lookup"><span data-stu-id="2e295-121">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="2e295-122">Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей.</span><span class="sxs-lookup"><span data-stu-id="2e295-122">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="2e295-123">Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее по статическим `Configure()` файлам:</span><span class="sxs-lookup"><span data-stu-id="2e295-123">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="2e295-124">папка wwwroot</span><span class="sxs-lookup"><span data-stu-id="2e295-124">wwwroot folder</span></span>

<span data-ttu-id="2e295-125">В ASP.</span><span class="sxs-lookup"><span data-stu-id="2e295-125">In ASP.</span></span> <span data-ttu-id="2e295-126">NET Core — это веб-корневая папка, в которой приложение ищет статические файлы.</span><span class="sxs-lookup"><span data-stu-id="2e295-126">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="2e295-127">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="2e295-127">AppManifest folder</span></span>

<span data-ttu-id="2e295-128">Эта папка содержит следующие необходимые файлы пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="2e295-128">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="2e295-129">Значок **полного цвета** размером 192 x 192 пикселя.</span><span class="sxs-lookup"><span data-stu-id="2e295-129">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="2e295-130">Прозрачный **значок контура** размером 32 x 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="2e295-130">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="2e295-131">Файл **manifest.js,** который указывает атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="2e295-131">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="2e295-132">Эти файлы необходимо использовать в пакете приложений для отправки вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="2e295-132">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="2e295-133">Microsoft Teams загрузит указанное в манифесте, встраит его в `contentUrl` IFrame и отрисует его на вкладке.</span><span class="sxs-lookup"><span data-stu-id="2e295-133">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="2e295-134">.csproj</span><span class="sxs-lookup"><span data-stu-id="2e295-134">.csproj</span></span>

<span data-ttu-id="2e295-135">В окне Visual Studio обозревателя решений щелкните правой кнопкой мыши по проекту и выберите **Файл редактирования проекта.**</span><span class="sxs-lookup"><span data-stu-id="2e295-135">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="2e295-136">В нижней части файла вы увидите код, который создает и обновляет папку zip при создании приложения:</span><span class="sxs-lookup"><span data-stu-id="2e295-136">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="2e295-137">Модели</span><span class="sxs-lookup"><span data-stu-id="2e295-137">Models</span></span>

<span data-ttu-id="2e295-138">*PersonalTab.cs* представляет объект Сообщения и методы, которые будут вызваны из *PersonalTabController,* когда пользователь выбирает кнопку в *представлении PersonalTab.*</span><span class="sxs-lookup"><span data-stu-id="2e295-138">*PersonalTab.cs* presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the *PersonalTab* View.</span></span>

### <a name="views"></a><span data-ttu-id="2e295-139">Представления</span><span class="sxs-lookup"><span data-stu-id="2e295-139">Views</span></span>

#### <a name="home"></a><span data-ttu-id="2e295-140">Главная</span><span class="sxs-lookup"><span data-stu-id="2e295-140">Home</span></span>

<span data-ttu-id="2e295-141">ASP.</span><span class="sxs-lookup"><span data-stu-id="2e295-141">ASP.</span></span> <span data-ttu-id="2e295-142">Net Core обрабатывает *файлы,* называемые Index, как домашняя страница по умолчанию для сайта.</span><span class="sxs-lookup"><span data-stu-id="2e295-142">NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="2e295-143">Когда URL-адрес браузера указывает на корень сайта, *Index.cshtml* будет отображаться в качестве домашней страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="2e295-143">When your browser URL points to the root of the site, *Index.cshtml* will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="2e295-144">Shared</span><span class="sxs-lookup"><span data-stu-id="2e295-144">Shared</span></span>

<span data-ttu-id="2e295-145">Частичная разметка *_Layout.cshtml* содержит общую структуру страницы приложения и общие визуальные элементы.</span><span class="sxs-lookup"><span data-stu-id="2e295-145">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="2e295-146">Он также будет ссылаться на библиотеку teams.</span><span class="sxs-lookup"><span data-stu-id="2e295-146">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="2e295-147">Контроллеры</span><span class="sxs-lookup"><span data-stu-id="2e295-147">Controllers</span></span>

<span data-ttu-id="2e295-148">Контроллеры используют свойство ViewBag для динамической передачи значений в Представления.</span><span class="sxs-lookup"><span data-stu-id="2e295-148">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="2e295-149">Откройте командную подсказку в корневом каталоге проекта и запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2e295-149">Open a command prompt in the root of your project directory and run the following command:</span></span>

``` bash
ngrok http https://localhost:44345 -host-header="localhost:44345"
```

* <span data-ttu-id="2e295-150">Ngrok будет прослушивать запросы из Интернета и перенанастрает их в ваше приложение, когда оно запущено в порту 44325.</span><span class="sxs-lookup"><span data-stu-id="2e295-150">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="2e295-151">Он должен `https://y8rPrT2b.ngrok.io/` напоминать, где *y8rPrT2b* заменяется url-адресом https ngrok alpha-numeric HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2e295-151">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="2e295-152">Убедитесь в том, что командная подсказка будет запущена с помощью ngrok, и обратите внимание на URL-адрес , который вам понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="2e295-152">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="2e295-153">Убедитесь, что *ngrok* работает и работает должным образом, открыв браузер и переехав на страницу контента через URL-адрес https ngrok, который был представлен в окне командной подсказки.</span><span class="sxs-lookup"><span data-stu-id="2e295-153">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> <span data-ttu-id="2e295-154">[!</span><span class="sxs-lookup"><span data-stu-id="2e295-154">[!</span></span> <span data-ttu-id="2e295-155">СОВЕТ] Чтобы выполнить эту быструю работу, необходимо Visual Studio и ngrok.</span><span class="sxs-lookup"><span data-stu-id="2e295-155">TIP] You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="2e295-156">Если для работы с приложением необходимо прекратить Visual Studio, продолжайте **работать с ngrok.**</span><span class="sxs-lookup"><span data-stu-id="2e295-156">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="2e295-157">После перезапуска в Visual Studio он продолжит прослушивание и возобновит маршрутизаку запроса приложения.</span><span class="sxs-lookup"><span data-stu-id="2e295-157">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="2e295-158">Если вам придется перезапустить службу ngrok, она возвращает новый URL-адрес, и вам придется обновить каждое место, использующее этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="2e295-158">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="2e295-159">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="2e295-159">Run your application</span></span>

* <span data-ttu-id="2e295-160">В Visual Studio **нажмите кнопку F5** или **выберите Пуск** отладки из меню отладки **приложения.**</span><span class="sxs-lookup"><span data-stu-id="2e295-160">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
