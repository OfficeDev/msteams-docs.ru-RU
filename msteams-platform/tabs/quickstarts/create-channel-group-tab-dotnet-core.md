---
title: Создание вкладки каналов и групп с ядром ASP.NET
author: laujan
description: Краткое руководство по созданию настраиваемой вкладки каналов и групп с ядром ASP.NET.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 7fdc4b042aac0664ae9d62c73c90689c75823592
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675646"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core"></a><span data-ttu-id="89557-103">Создание настраиваемой вкладки каналов и групп с ядром ASP.NET</span><span class="sxs-lookup"><span data-stu-id="89557-103">Create a Custom Channel and Group Tab with ASP.NET Core</span></span>

<span data-ttu-id="89557-104">В этом руководстве мы рассмотрим создание настраиваемой вкладки каналов/групп с помощью C# и ASP.Net основной страницы Razor.</span><span class="sxs-lookup"><span data-stu-id="89557-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="89557-105">Мы также используем [Приложение App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) , чтобы завершить манифест приложения и развернуть вкладку в Teams.</span><span class="sxs-lookup"><span data-stu-id="89557-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="89557-106">Получение исходного кода</span><span class="sxs-lookup"><span data-stu-id="89557-106">Get the source code</span></span>

<span data-ttu-id="89557-107">Откройте командную строку и создайте новый каталог для проекта со вкладками.</span><span class="sxs-lookup"><span data-stu-id="89557-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="89557-108">Мы предоставили простой проект, чтобы приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="89557-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="89557-109">Чтобы получить исходный код, можно скачать папку ZIP и извлечь файлы или клонировать репозиторий примера в новый каталог:</span><span class="sxs-lookup"><span data-stu-id="89557-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="89557-110">После создания исходного кода откройте Visual Studio и выберите **Открыть проект или решение**.</span><span class="sxs-lookup"><span data-stu-id="89557-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="89557-111">Перейдите в каталог приложений вкладки и откройте **чаннелграуптаб. sln**.</span><span class="sxs-lookup"><span data-stu-id="89557-111">Navigate to the tab application directory and open **ChannelGroupTab.sln**.</span></span>

<span data-ttu-id="89557-112">Чтобы построить и запустить приложение, нажмите клавишу **F5** или в меню **Отладка** выберите команду **начать отладку** .</span><span class="sxs-lookup"><span data-stu-id="89557-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="89557-113">В браузере перейдите к следующим URL-адресам и убедитесь, что приложение загружено правильно:</span><span class="sxs-lookup"><span data-stu-id="89557-113">In a browser navigate to the URLs below and verify the application loaded properly:</span></span>

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="89557-114">Просмотр исходного кода</span><span class="sxs-lookup"><span data-stu-id="89557-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="89557-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="89557-115">Startup.cs</span></span>

<span data-ttu-id="89557-116">Этот проект был создан из пустого шаблона веб-приложения ASP.NET Core 2,2 с установленным флажком *Расширенная настройка для HTTPS* , установленным во время установки.</span><span class="sxs-lookup"><span data-stu-id="89557-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="89557-117">Службы MVC регистрируются `ConfigureServices()` методом платформы внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="89557-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="89557-118">Кроме того, по умолчанию в пустом шаблоне не включается возможность обслуживания статического содержимого, поэтому в `Configure()` метод добавляется промежуточное по промежуточным файлам.</span><span class="sxs-lookup"><span data-stu-id="89557-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="89557-119">Папка wwwroot</span><span class="sxs-lookup"><span data-stu-id="89557-119">wwwroot folder</span></span>

<span data-ttu-id="89557-120">В ядре ASP.NET корневая папка веб-сайта — это место, в котором приложение выполняет поиск статических файлов.</span><span class="sxs-lookup"><span data-stu-id="89557-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="89557-121">Index. cshtml</span><span class="sxs-lookup"><span data-stu-id="89557-121">Index.cshtml</span></span>

<span data-ttu-id="89557-122">ASP.NET Core рассматривает файлы с именем *index* как страницу по умолчанию или домашнюю страницу сайта.</span><span class="sxs-lookup"><span data-stu-id="89557-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="89557-123">Если URL-адрес браузера указывает на корневой сайт сайта, в качестве домашней страницы для приложения будет отображаться **index. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="89557-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="tabcs"></a><span data-ttu-id="89557-124">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="89557-124">Tab.cs</span></span>

<span data-ttu-id="89557-125">Этот файл C# содержит метод, который будет вызываться из **TAB. cshtml** во время настройки.</span><span class="sxs-lookup"><span data-stu-id="89557-125">This C# file contains a method that will be called from **Tab.cshtml** during configuration.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="89557-126">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="89557-126">AppManifest folder</span></span>

<span data-ttu-id="89557-127">Эта папка содержит следующие обязательные файлы пакета приложения:</span><span class="sxs-lookup"><span data-stu-id="89557-127">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="89557-128">**Значок с полным цветом** , измеряющий 192 x 192 пикселей.</span><span class="sxs-lookup"><span data-stu-id="89557-128">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="89557-129">**Прозрачный значок структуры** , измеряющий 32 x 32 пикселей.</span><span class="sxs-lookup"><span data-stu-id="89557-129">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="89557-130">Файл **manifest. JSON** , задающий атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="89557-130">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="89557-131">Эти файлы необходимо заархивировать в пакете приложения для использования при загрузке вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="89557-131">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="89557-132">Когда пользователь выбирает Добавление или обновление вкладки, Microsoft Teams загружает `configurationUrl` указанную в манифесте, внедряет ее в Интернет, а затем отображает ее на вкладке.</span><span class="sxs-lookup"><span data-stu-id="89557-132">When a user chooses to add or update your tab, Microsoft Teams will load the `configurationUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="89557-133">CSPROJ</span><span class="sxs-lookup"><span data-stu-id="89557-133">.csproj</span></span>

<span data-ttu-id="89557-134">В окне обозревателя решений Visual Studio щелкните правой кнопкой мыши проект и выберите команду **изменить файл проекта**.</span><span class="sxs-lookup"><span data-stu-id="89557-134">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="89557-135">В нижней части файла вы увидите код, который создает и обновляет папку zip при построении приложения:</span><span class="sxs-lookup"><span data-stu-id="89557-135">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="89557-136">Откройте командную строку в корне каталога проекта и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="89557-136">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:44355 -host-header="localhost:44355"
```

- <span data-ttu-id="89557-137">Ngrok прослушивает запросы из Интернета и направляет их в ваше приложение, когда оно выполняется на порте 44355.</span><span class="sxs-lookup"><span data-stu-id="89557-137">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="89557-138">Он должен выглядеть примерно `https://y8rCgT2b.ngrok.io/` так, где *y8rCgT2b* заменяется URL-адресом https ngrok, сооснованным на цифровом алфавите.</span><span class="sxs-lookup"><span data-stu-id="89557-138">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="89557-139">Убедитесь, что Командная строка ngrok запущена и запишите URL-адрес, а затем это потребуется позже.</span><span class="sxs-lookup"><span data-stu-id="89557-139">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="89557-140">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="89557-140">Update your application</span></span>

<span data-ttu-id="89557-141">В пределах *TAB. cshtml* приложение предоставляет пользователю два переключателя для отображения вкладки с помощью значка красного или серого.</span><span class="sxs-lookup"><span data-stu-id="89557-141">Within *Tab.cshtml* the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="89557-142">При `saveRed()`нажатии `settings.setValidityState(true)`кнопки `saveGray()` **выбрать серое** или **выбрать красную** , соответственно, задает набор и активируется кнопка **сохранить** на странице Конфигурация.</span><span class="sxs-lookup"><span data-stu-id="89557-142">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="89557-143">Этот код позволяет Teams знать, что вы удовлетворены требованиями к конфигурации и можете продолжить установку.</span><span class="sxs-lookup"><span data-stu-id="89557-143">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="89557-144">При сохранении задаются параметры `settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="89557-144">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="89557-145">`saveEvent.notifySuccess()` Finally вызывается, чтобы показать, что URL-адрес контента успешно разрешен.</span><span class="sxs-lookup"><span data-stu-id="89557-145">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
