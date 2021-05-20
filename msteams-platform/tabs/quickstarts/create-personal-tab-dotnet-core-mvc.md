---
title: Создайте личную вкладку с помощью ASP. NET Core MVC
author: laujan
description: Краткое руководство по созданию пользовательских личных вкладку с ASP. NET Core MVC.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 01418adb32335660bb20f74ecfaa0e7e27230c93
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566635"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a>Создание пользовательской персональной вкладки с ASP.NET Core MVC

В этом quickstart мы будем ходить через создание пользовательских личных вкладку с C и ASP.Net Core MVC. Мы также будем использовать [App Studio для Microsoft Teams для](~/concepts/build-and-test/app-studio-overview.md) завершения манифеста приложения и развертывания вкладки для Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Получить исходный код

Откройте командный запрос и создайте новый каталог для вашего проекта вкладок. Мы предоставили простой проект, чтобы вы начали. Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в свой новый каталог:

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Если у вас есть исходный код, откройте Visual Studio и **выберите Открыть проект или решение.** Перейдите в каталог приложений вкладок и **откройте PersonalTabMVC.sln**.

Для создания и запуска приложения нажмите **F5 или** выберите **Start Debugging** из **меню отладки.** В браузере перейдите на URL-адреса ниже, чтобы убедиться, что приложение загружено должным образом:

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a>Просмотр исходный код

### <a name="startupcs"></a>Стартап.cs

Этот проект был создан из ASP. NET Core 2.2 Web Application пустой шаблон с *Расширенный - Настройка для https проверить окно* выбрано при настройке. Службы MVC регистрируются методом фреймворка впрыска `ConfigureServices()` зависимости. Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее программное обеспечение статических `Configure()` файлов:

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

### <a name="wwwroot-folder"></a>wwwroot папка

В ASP. NET Core, папка веб-корня, где приложение ищет статические файлы.

### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложений:

* Значок **полного цвета** размером 192 х 192 пикселей.
* **Прозрачная иконка контура** размером 32 х 32 пикселя.
* В **manifest.jsфайле,** в который указаны атрибуты приложения.

Эти файлы должны быть застегнуты на молнии в пакете приложений для использования в загрузке вкладки, чтобы Teams. Microsoft Teams загрузит `contentUrl` указанное в манифесте, встраивает его в IFrame и отображает в вкладке.

### <a name="csproj"></a>.csproj

В окне Visual Studio Solution Explorer нажмите правой кнопкой мыши на проект и выберите **Редактировать Project файл**. В нижней части файла вы увидите код, который создает и обновляет папку zip при сборке приложения:

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

### <a name="models"></a>Модели

**PersonalTab.cs** представляет объект сообщения и методы, которые будут *вызваны из PersonalTabController,* когда пользователь выберет кнопку **в представлении PersonalTab.**

### <a name="views"></a>Представления

#### <a name="home"></a>Главная

гадюка. NET Core рассматривает файлы, **называемые Index,** как по умолчанию или домашнюю страницу для сайта. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml будет** отображаться в качестве главной страницы для вашего приложения.

#### <a name="shared"></a>Shared

Частичная разметка представления *_Layout.cshtml содержит* общую структуру страницы приложения и общие визуальные элементы. Он также будет ссылаться на Teams библиотеку.

### <a name="controllers"></a>Контроллеры

Контроллеры используют свойство ViewBag для динамической передачи значений представлениям.

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* Откройте подсказку команды в корне каталога проекта и запустите следующую команду:

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

* Ngrok будет слушать запросы из Интернета и будет маршрут их к вашему приложению, когда он работает на порт 44325.  Он должен `https://y8rPrT2b.ngrok.io/` *напоминать, где y8rPrT2b* заменяется вашим ngrok альфа-числом HTTPS URL.

* Не забудьте сохранить подсказку команды с ngrok работает, и сделать заметку о URL - вам это понадобится позже.

* **Убедитесь, что ngrok** работает и работает должным образом, открыв браузер и переходя на страницу содержимого через URL ngrok HTTPS, который был предоставлен в окне оперативной команды.

> [!TIP]
> Вы должны иметь как ваше приложение в Visual Studio ngrok работает, чтобы завершить этот быстрый старт. Если вам нужно прекратить запуск приложения в Visual Studio над ним, **продолжайте работать ngrok.** Он будет продолжать слушать и возобновит маршрутизацию запроса вашего приложения, когда он перезапустится в Visual Studio. Если вам придется перезапустить службу ngrok он вернет новый URL, и вам придется обновлять каждое место, которое использует этот URL.

### <a name="run-your-application"></a>Вы запустите приложение

* В Visual Studio **нажмите F5** или **выберите Start Debugging** из меню **отладки приложения.**

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Создайте пользовательский канал и групповую вкладку, Node.js и генератор Yeoman для Microsoft Teams](~/tabs/quickstarts/create-channel-group-tab-node-yeoman.md)
