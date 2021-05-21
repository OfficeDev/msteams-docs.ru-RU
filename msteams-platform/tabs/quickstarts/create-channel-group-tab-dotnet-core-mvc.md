---
title: Создание вкладки каналов и групп с ASP.NET Core MVC
author: laujan
description: Руководство quickstart по созданию настраиваемой вкладки канала и группы с ASP.NET Core MVC
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: ea929edf5a281a4bb80a37b2d5c6e19c82fce6e4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52580464"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="95b57-103">Создание настраиваемой вкладки канала и группы ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="95b57-103">Create a Custom Channel and Group Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="95b57-104">В этом quickstart мы создам настраиваемую вкладку channel/group с C# и ASP.Net core MVC.</span><span class="sxs-lookup"><span data-stu-id="95b57-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="95b57-105">Мы также используем [App Studio для](~/concepts/build-and-test/app-studio-overview.md) Microsoft Teams манифеста приложения и развертывания вкладки Teams.</span><span class="sxs-lookup"><span data-stu-id="95b57-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="95b57-106">Получить исходный код</span><span class="sxs-lookup"><span data-stu-id="95b57-106">Get the source code</span></span>

<span data-ttu-id="95b57-107">Откройте командную подсказку и создайте новый каталог для проекта вкладки.</span><span class="sxs-lookup"><span data-stu-id="95b57-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="95b57-108">Мы предоставили простой проект [Вкладки группы каналов](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) для начала работы.</span><span class="sxs-lookup"><span data-stu-id="95b57-108">We have provided a simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) project to get you started.</span></span> <span data-ttu-id="95b57-109">Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в новый каталог:</span><span class="sxs-lookup"><span data-stu-id="95b57-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="95b57-110">После того как у вас есть исходный код, откройте Visual Studio и выберите **Открыть проект или решение**.</span><span class="sxs-lookup"><span data-stu-id="95b57-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="95b57-111">Перейдите к каталогу приложений вкладок и откройте **ChannelGroupTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="95b57-111">Navigate to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>

<span data-ttu-id="95b57-112">Для создания и запуска приложения нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки.**</span><span class="sxs-lookup"><span data-stu-id="95b57-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="95b57-113">В браузере перейдите к URL-адресам ниже и убедитесь, что приложение загружено правильно:</span><span class="sxs-lookup"><span data-stu-id="95b57-113">In a browser, navigate to the URLs below and verify that the application loaded properly:</span></span>

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="95b57-114">Просмотр исходных кодов</span><span class="sxs-lookup"><span data-stu-id="95b57-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="95b57-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="95b57-115">Startup.cs</span></span>

<span data-ttu-id="95b57-116">Этот проект был создан из пустого шаблона ASP.NET Core 2.2 веб-приложения с расширенным — настройка для контрольного окна *HTTPS,* выбранного при установке.</span><span class="sxs-lookup"><span data-stu-id="95b57-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="95b57-117">Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей.</span><span class="sxs-lookup"><span data-stu-id="95b57-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="95b57-118">Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее по статическим `Configure()` файлам:</span><span class="sxs-lookup"><span data-stu-id="95b57-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="95b57-119">папка wwwroot</span><span class="sxs-lookup"><span data-stu-id="95b57-119">wwwroot folder</span></span>

<span data-ttu-id="95b57-120">В ASP.NET Core веб-корневой папке приложение ищет статические файлы.</span><span class="sxs-lookup"><span data-stu-id="95b57-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="95b57-121">Папка AppManifest</span><span class="sxs-lookup"><span data-stu-id="95b57-121">AppManifest folder</span></span>

<span data-ttu-id="95b57-122">Эта папка содержит следующие необходимые файлы пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="95b57-122">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="95b57-123">Значок **полного цвета** размером 192 x 192 пикселя.</span><span class="sxs-lookup"><span data-stu-id="95b57-123">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="95b57-124">Прозрачный **значок контура** размером 32 x 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="95b57-124">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="95b57-125">Файл **manifest.js,** который указывает атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="95b57-125">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="95b57-126">Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="95b57-126">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

### <a name="csproj"></a><span data-ttu-id="95b57-127">.csproj</span><span class="sxs-lookup"><span data-stu-id="95b57-127">.csproj</span></span>

<span data-ttu-id="95b57-128">В окне Visual Studio Обозреватель решений щелкните правой кнопкой мыши по проекту и выберите **Изменить Project файл**.</span><span class="sxs-lookup"><span data-stu-id="95b57-128">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="95b57-129">В нижней части файла вы увидите код, который создает и обновляет папку zip при создании приложения:</span><span class="sxs-lookup"><span data-stu-id="95b57-129">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="95b57-130">Модели</span><span class="sxs-lookup"><span data-stu-id="95b57-130">Models</span></span>

<span data-ttu-id="95b57-131">*ChannelGroup.cs представляет* объект Сообщения и методы, которые будут вызваны из контроллеров во время настройки.</span><span class="sxs-lookup"><span data-stu-id="95b57-131">*ChannelGroup.cs* presents a Message object and methods that will be called from the Controllers during configuration.</span></span>

### <a name="views"></a><span data-ttu-id="95b57-132">Представления</span><span class="sxs-lookup"><span data-stu-id="95b57-132">Views</span></span>

#### <a name="home"></a><span data-ttu-id="95b57-133">Главная</span><span class="sxs-lookup"><span data-stu-id="95b57-133">Home</span></span>

<span data-ttu-id="95b57-134">ASP.NET Core обрабатывает файлы под названием *Index* в качестве домашней страницы по умолчанию для сайта.</span><span class="sxs-lookup"><span data-stu-id="95b57-134">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="95b57-135">Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** будет отображаться в качестве домашней страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="95b57-135">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="95b57-136">Shared</span><span class="sxs-lookup"><span data-stu-id="95b57-136">Shared</span></span>

<span data-ttu-id="95b57-137">Частичная разметка *_Layout.cshtml* содержит общую структуру страницы приложения и общие визуальные элементы.</span><span class="sxs-lookup"><span data-stu-id="95b57-137">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="95b57-138">Он также будет ссылаться на Teams библиотеку.</span><span class="sxs-lookup"><span data-stu-id="95b57-138">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="95b57-139">Контроллеры</span><span class="sxs-lookup"><span data-stu-id="95b57-139">Controllers</span></span>

<span data-ttu-id="95b57-140">Контроллеры используют свойство ViewBag для динамической передачи значений в Представления.</span><span class="sxs-lookup"><span data-stu-id="95b57-140">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="95b57-141">Откройте командную подсказку в корневом каталоге проекта и запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="95b57-141">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:443560 -host-header="localhost:44360"
    ```

- <span data-ttu-id="95b57-142">Ngrok будет прослушивать запросы из Интернета и перенанастрает их в ваше приложение, когда оно запущено в порту 44355.</span><span class="sxs-lookup"><span data-stu-id="95b57-142">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span>  <span data-ttu-id="95b57-143">Он должен `https://y8rCgT2b.ngrok.io/` напоминать, где *y8rCgT2b* заменяется url-адресом https ngrok alpha-numeric HTTPS.</span><span class="sxs-lookup"><span data-stu-id="95b57-143">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="95b57-144">Убедитесь в том, что командная подсказка будет запущена с помощью ngrok, и обратите внимание на URL-адрес , который вам понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="95b57-144">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="95b57-145">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="95b57-145">Update your application</span></span>

<span data-ttu-id="95b57-146">В **Tab.cshtml** приложение представляет пользователю две кнопки параметра для отображения вкладки с красным или серым значком.</span><span class="sxs-lookup"><span data-stu-id="95b57-146">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="95b57-147">Выбор кнопки **Выберите серый** или **выберите** красный или, соответственно, задает и включает кнопку Сохранить `saveGray()` на странице `saveRed()` `settings.setValidityState(true)` конфигурации. </span><span class="sxs-lookup"><span data-stu-id="95b57-147">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="95b57-148">Этот код позволяет Teams, что вы удовлетворяли требованиям конфигурации и установка может продолжиться.</span><span class="sxs-lookup"><span data-stu-id="95b57-148">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="95b57-149">При сохранения `settings.setSettings` заданы параметры.</span><span class="sxs-lookup"><span data-stu-id="95b57-149">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="95b57-150">Наконец, `saveEvent.notifySuccess()` называется, чтобы указать, что URL-адрес контента успешно решен.</span><span class="sxs-lookup"><span data-stu-id="95b57-150">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]