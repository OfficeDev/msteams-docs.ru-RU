---
title: Создание вкладки каналов и групп с помощью ASP.NET Core
author: surbhigupta
description: Руководство quickstart по созданию настраиваемой вкладки канала и группы с ASP.NET Core.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 2f7906f1fb9874503cecabdeb607251daf863e97
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069116"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnetcore"></a><span data-ttu-id="0743a-103">Создание настраиваемой вкладки канала и группы с помощью ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="0743a-103">Create a Custom Channel and Group Tab with ASP.NETCore</span></span>

<span data-ttu-id="0743a-104">В этом quickstart мы создам настраиваемую вкладку каналов и групп с C# и ASP.Net Core Razor.</span><span class="sxs-lookup"><span data-stu-id="0743a-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="0743a-105">Мы также используем [App Studio для](~/concepts/build-and-test/app-studio-overview.md) Microsoft Teams манифеста приложения и развертывания вкладки Teams.</span><span class="sxs-lookup"><span data-stu-id="0743a-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="0743a-106">Получить исходный код</span><span class="sxs-lookup"><span data-stu-id="0743a-106">Get the source code</span></span>

<span data-ttu-id="0743a-107">Откройте командную подсказку и создайте новый каталог для проекта вкладки.</span><span class="sxs-lookup"><span data-stu-id="0743a-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="0743a-108">Мы предоставили простой проект для начала работы.</span><span class="sxs-lookup"><span data-stu-id="0743a-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="0743a-109">Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в новый каталог:</span><span class="sxs-lookup"><span data-stu-id="0743a-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="0743a-110">После того как у вас есть исходный код, откройте Visual Studio и выберите **Открыть проект или решение**.</span><span class="sxs-lookup"><span data-stu-id="0743a-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="0743a-111">Перейдите к каталогу приложений вкладок и **откройте ChannelGroupTab.sln**.</span><span class="sxs-lookup"><span data-stu-id="0743a-111">Navigate to the tab application directory and open **ChannelGroupTab.sln**.</span></span>

<span data-ttu-id="0743a-112">Для создания и запуска приложения нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки.**</span><span class="sxs-lookup"><span data-stu-id="0743a-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="0743a-113">В браузере перейдите к URL-адресам ниже и убедитесь, что приложение загружено правильно:</span><span class="sxs-lookup"><span data-stu-id="0743a-113">In a browser navigate to the URLs below and verify the application loaded properly:</span></span>

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="0743a-114">Просмотр исходных кодов</span><span class="sxs-lookup"><span data-stu-id="0743a-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="0743a-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="0743a-115">Startup.cs</span></span>

<span data-ttu-id="0743a-116">Этот проект был создан из пустого шаблона ASP.NET Core 2.2 веб-приложения с расширенным — настройка для контрольного окна *HTTPS,* выбранного при установке.</span><span class="sxs-lookup"><span data-stu-id="0743a-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="0743a-117">Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей.</span><span class="sxs-lookup"><span data-stu-id="0743a-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="0743a-118">Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее по статическим `Configure()` файлам:</span><span class="sxs-lookup"><span data-stu-id="0743a-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="0743a-119">папка wwwroot</span><span class="sxs-lookup"><span data-stu-id="0743a-119">wwwroot folder</span></span>

<span data-ttu-id="0743a-120">В ASP.NET Core веб-корневой папке приложение ищет статические файлы.</span><span class="sxs-lookup"><span data-stu-id="0743a-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="0743a-121">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="0743a-121">Index.cshtml</span></span>

<span data-ttu-id="0743a-122">ASP.NET Core обрабатывает файлы под названием *Index* в качестве домашней страницы по умолчанию для сайта.</span><span class="sxs-lookup"><span data-stu-id="0743a-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="0743a-123">Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** будет отображаться в качестве домашней страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="0743a-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="tabcs"></a><span data-ttu-id="0743a-124">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="0743a-124">Tab.cs</span></span>

<span data-ttu-id="0743a-125">Этот C# содержит метод, который будет вызван из **Tab.cshtml** во время настройки.</span><span class="sxs-lookup"><span data-stu-id="0743a-125">This C# file contains a method that will be called from **Tab.cshtml** during configuration.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="0743a-126">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="0743a-126">AppManifest folder</span></span>

<span data-ttu-id="0743a-127">Эта папка содержит следующие необходимые файлы пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="0743a-127">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="0743a-128">Значок **полного цвета** размером 192 x 192 пикселя.</span><span class="sxs-lookup"><span data-stu-id="0743a-128">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="0743a-129">Прозрачный **значок контура** размером 32 x 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="0743a-129">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="0743a-130">Файл **manifest.js,** который указывает атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="0743a-130">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="0743a-131">Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="0743a-131">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="0743a-132">Когда пользователь выбирает добавить или обновить вкладку, Microsoft Teams загрузит указанный в манифесте, встроит его в IFrame и отрисует его на `configurationUrl` вкладке.</span><span class="sxs-lookup"><span data-stu-id="0743a-132">When a user chooses to add or update your tab, Microsoft Teams will load the `configurationUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="0743a-133">.csproj</span><span class="sxs-lookup"><span data-stu-id="0743a-133">.csproj</span></span>

<span data-ttu-id="0743a-134">В окне Visual Studio Обозреватель решений щелкните правой кнопкой мыши по проекту и выберите **Изменить Project файл**.</span><span class="sxs-lookup"><span data-stu-id="0743a-134">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="0743a-135">В нижней части файла вы увидите код, который создает и обновляет папку zip при создании приложения:</span><span class="sxs-lookup"><span data-stu-id="0743a-135">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="0743a-136">Откройте командную подсказку в корневом каталоге проекта и запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0743a-136">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44355 -host-header="localhost:44355"
    ```

- <span data-ttu-id="0743a-137">Ngrok будет прослушивать запросы из Интернета и перенанастрает их в ваше приложение, когда оно запущено в порту 44355.</span><span class="sxs-lookup"><span data-stu-id="0743a-137">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="0743a-138">Он должен `https://y8rCgT2b.ngrok.io/` напоминать, где *y8rCgT2b* заменяется url-адресом https ngrok alpha-numeric HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0743a-138">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="0743a-139">Убедитесь в том, что командная подсказка будет запущена с помощью ngrok, и обратите внимание на URL-адрес , который вам понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="0743a-139">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="0743a-140">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="0743a-140">Update your application</span></span>

<span data-ttu-id="0743a-141">В *Tab.cshtml* приложение представляет пользователю две кнопки параметра для отображения вкладки с красным или серым значком.</span><span class="sxs-lookup"><span data-stu-id="0743a-141">Within *Tab.cshtml* the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="0743a-142">Выбор кнопки **Выберите серый** или **выберите** красный или, соответственно, задает и включает кнопку Сохранить `saveGray()` на странице `saveRed()` `settings.setValidityState(true)` конфигурации. </span><span class="sxs-lookup"><span data-stu-id="0743a-142">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="0743a-143">Этот код позволяет Teams, что вы удовлетворяли требованиям конфигурации и установка может продолжиться.</span><span class="sxs-lookup"><span data-stu-id="0743a-143">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="0743a-144">При сохранения `settings.setSettings` заданы параметры.</span><span class="sxs-lookup"><span data-stu-id="0743a-144">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="0743a-145">Наконец, `saveEvent.notifySuccess()` называется, чтобы указать, что URL-адрес контента успешно решен.</span><span class="sxs-lookup"><span data-stu-id="0743a-145">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

## <a name="next-step"></a><span data-ttu-id="0743a-146">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="0743a-146">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0743a-147">Создание настраиваемой вкладки канала и группы с помощью MVC ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="0743a-147">Create a Custom Channel and Group Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-channel-group-tab-dotnet-core-mvc.md)
