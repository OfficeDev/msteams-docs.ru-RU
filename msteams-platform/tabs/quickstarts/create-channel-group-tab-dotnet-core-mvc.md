---
title: Создание вкладки каналов и групп с ASP.NET основной MVC
author: laujan
description: Краткое руководство по созданию настраиваемой вкладки каналов и групп с ASP.NET основной MVC.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 57c22d10414eb8ec93249584219488397f0b6b33
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675383"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="facaf-103">Создание настраиваемой вкладки каналов и групп с ASP.NET основной MVC</span><span class="sxs-lookup"><span data-stu-id="facaf-103">Create a Custom Channel and Group Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="facaf-104">В этом руководстве мы рассмотрим создание настраиваемой вкладки канал/группа с помощью C# и ASP.Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="facaf-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="facaf-105">Мы также используем [Приложение App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) , чтобы завершить манифест приложения и развернуть вкладку в Teams.</span><span class="sxs-lookup"><span data-stu-id="facaf-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="facaf-106">Получение исходного кода</span><span class="sxs-lookup"><span data-stu-id="facaf-106">Get the source code</span></span>

<span data-ttu-id="facaf-107">Откройте командную строку и создайте новый каталог для проекта со вкладками.</span><span class="sxs-lookup"><span data-stu-id="facaf-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="facaf-108">Чтобы приступить к работе, мы предоставили проект [вкладки простой группы каналов](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) .</span><span class="sxs-lookup"><span data-stu-id="facaf-108">We have provided a simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) project to get you started.</span></span> <span data-ttu-id="facaf-109">Чтобы получить исходный код, можно скачать папку ZIP и извлечь файлы или клонировать репозиторий примера в новый каталог:</span><span class="sxs-lookup"><span data-stu-id="facaf-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="facaf-110">После создания исходного кода откройте Visual Studio и выберите **Открыть проект или решение**.</span><span class="sxs-lookup"><span data-stu-id="facaf-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="facaf-111">Перейдите в каталог приложений вкладки и откройте **чаннелграуптабмвк. sln**.</span><span class="sxs-lookup"><span data-stu-id="facaf-111">Navigate to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>

<span data-ttu-id="facaf-112">Чтобы построить и запустить приложение, нажмите клавишу **F5** или в меню **Отладка** выберите команду **начать отладку** .</span><span class="sxs-lookup"><span data-stu-id="facaf-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="facaf-113">В браузере перейдите по приведенным ниже URL-адресам и убедитесь, что приложение загружено правильно:</span><span class="sxs-lookup"><span data-stu-id="facaf-113">In a browser, navigate to the URLs below and verify that the application loaded properly:</span></span>

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="facaf-114">Просмотр исходного кода</span><span class="sxs-lookup"><span data-stu-id="facaf-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="facaf-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="facaf-115">Startup.cs</span></span>

<span data-ttu-id="facaf-116">Этот проект был создан из пустого шаблона веб-приложения ASP.NET Core 2,2 с установленным флажком *Расширенная настройка для HTTPS* , установленным во время установки.</span><span class="sxs-lookup"><span data-stu-id="facaf-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="facaf-117">Службы MVC регистрируются `ConfigureServices()` методом платформы внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="facaf-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="facaf-118">Кроме того, по умолчанию в пустом шаблоне не включается возможность обслуживания статического содержимого, поэтому в `Configure()` метод добавляется промежуточное по промежуточным файлам.</span><span class="sxs-lookup"><span data-stu-id="facaf-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="facaf-119">Папка wwwroot</span><span class="sxs-lookup"><span data-stu-id="facaf-119">wwwroot folder</span></span>

<span data-ttu-id="facaf-120">В ядре ASP.NET корневая папка веб-сайта — это место, в котором приложение выполняет поиск статических файлов.</span><span class="sxs-lookup"><span data-stu-id="facaf-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="facaf-121">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="facaf-121">AppManifest folder</span></span>

<span data-ttu-id="facaf-122">Эта папка содержит следующие обязательные файлы пакета приложения:</span><span class="sxs-lookup"><span data-stu-id="facaf-122">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="facaf-123">**Значок с полным цветом** , измеряющий 192 x 192 пикселей.</span><span class="sxs-lookup"><span data-stu-id="facaf-123">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="facaf-124">**Прозрачный значок структуры** , измеряющий 32 x 32 пикселей.</span><span class="sxs-lookup"><span data-stu-id="facaf-124">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="facaf-125">Файл **manifest. JSON** , задающий атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="facaf-125">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="facaf-126">Эти файлы необходимо заархивировать в пакете приложения для использования при загрузке вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="facaf-126">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

### <a name="csproj"></a><span data-ttu-id="facaf-127">CSPROJ</span><span class="sxs-lookup"><span data-stu-id="facaf-127">.csproj</span></span>

<span data-ttu-id="facaf-128">В окне обозревателя решений Visual Studio щелкните правой кнопкой мыши проект и выберите команду **изменить файл проекта**.</span><span class="sxs-lookup"><span data-stu-id="facaf-128">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="facaf-129">В нижней части файла вы увидите код, который создает и обновляет папку zip при построении приложения:</span><span class="sxs-lookup"><span data-stu-id="facaf-129">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="facaf-130">Модели</span><span class="sxs-lookup"><span data-stu-id="facaf-130">Models</span></span>

<span data-ttu-id="facaf-131">*ChannelGroup.CS* представляет объект сообщения и методы, которые будут вызываться из контроллеров во время настройки.</span><span class="sxs-lookup"><span data-stu-id="facaf-131">*ChannelGroup.cs* presents a Message object and methods that will be called from the Controllers during configuration.</span></span>

### <a name="views"></a><span data-ttu-id="facaf-132">Представления</span><span class="sxs-lookup"><span data-stu-id="facaf-132">Views</span></span>

#### <a name="home"></a><span data-ttu-id="facaf-133">Главная</span><span class="sxs-lookup"><span data-stu-id="facaf-133">Home</span></span>

<span data-ttu-id="facaf-134">ASP.NET Core рассматривает файлы с именем *index* как страницу по умолчанию или домашнюю страницу сайта.</span><span class="sxs-lookup"><span data-stu-id="facaf-134">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="facaf-135">Если URL-адрес браузера указывает на корневой сайт сайта, в качестве домашней страницы для приложения будет отображаться **index. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="facaf-135">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="facaf-136">Shared</span><span class="sxs-lookup"><span data-stu-id="facaf-136">Shared</span></span>

<span data-ttu-id="facaf-137">Разметка частичного представления *_layout. cshtml* содержит общую структуру страницы и общие визуальные элементы приложения.</span><span class="sxs-lookup"><span data-stu-id="facaf-137">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="facaf-138">Он также будет ссылаться на библиотеку Teams.</span><span class="sxs-lookup"><span data-stu-id="facaf-138">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="facaf-139">Controller</span><span class="sxs-lookup"><span data-stu-id="facaf-139">Controllers</span></span>

<span data-ttu-id="facaf-140">Контроллеры используют свойство Виевбаг для динамического переноса значений в представлениях.</span><span class="sxs-lookup"><span data-stu-id="facaf-140">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="facaf-141">Откройте командную строку в корне каталога проекта и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="facaf-141">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- <span data-ttu-id="facaf-142">Ngrok прослушивает запросы из Интернета и направляет их в ваше приложение, когда оно выполняется на порте 44355.</span><span class="sxs-lookup"><span data-stu-id="facaf-142">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span>  <span data-ttu-id="facaf-143">Он должен выглядеть примерно `https://y8rCgT2b.ngrok.io/` так, где *y8rCgT2b* заменяется URL-адресом https ngrok, сооснованным на цифровом алфавите.</span><span class="sxs-lookup"><span data-stu-id="facaf-143">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="facaf-144">Убедитесь, что Командная строка ngrok запущена и запишите URL-адрес, а затем это потребуется позже.</span><span class="sxs-lookup"><span data-stu-id="facaf-144">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="facaf-145">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="facaf-145">Update your application</span></span>

<span data-ttu-id="facaf-146">В пределах **TAB. cshtml** приложение предоставляет пользователю два переключателя для отображения вкладки с помощью значка красного или серого.</span><span class="sxs-lookup"><span data-stu-id="facaf-146">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="facaf-147">При `saveRed()`нажатии `settings.setValidityState(true)`кнопки `saveGray()` **выбрать серое** или **выбрать красную** , соответственно, задает набор и активируется кнопка **сохранить** на странице Конфигурация.</span><span class="sxs-lookup"><span data-stu-id="facaf-147">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="facaf-148">Этот код позволяет Teams знать, что вы удовлетворены требованиями к конфигурации и можете продолжить установку.</span><span class="sxs-lookup"><span data-stu-id="facaf-148">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="facaf-149">При сохранении задаются параметры `settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="facaf-149">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="facaf-150">`saveEvent.notifySuccess()` Finally вызывается, чтобы показать, что URL-адрес контента успешно разрешен.</span><span class="sxs-lookup"><span data-stu-id="facaf-150">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
