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
# <a name="create-a-personal-tab-using-aspnetcore"></a>Создание личной вкладки с помощью ASP.NETCore

В этом quickstart, мы будем ходить через создание пользовательских личных вкладку с C и ASP.Net Core Razor страниц. Мы также будем использовать [App Studio для Microsoft Teams для](~/concepts/build-and-test/app-studio-overview.md) завершения манифеста приложения и развертывания вкладки для Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Получить исходный код

Откройте командный запрос и создайте новый каталог для вашего проекта вкладок. Мы предоставили простой проект, чтобы вы начали. Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в свой новый каталог:

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Если у вас есть исходный код, откройте Visual Studio и **выберите Открыть проект или решение.** Перейдите в каталог приложений вкладок и **откройте PersonalTab.sln**.

Для создания и запуска приложения нажмите **F5 или** выберите **Start Debugging** из **меню отладки.** В браузере перейдите на URL-адреса ниже, чтобы проверить приложение загружено должным образом:

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a>Просмотр исходный код

### <a name="startupcs"></a>Стартап.cs

Этот проект был создан из ASP.NET Core 2.2 Web Application пустой шаблон **с Расширенный - Настройка для HTTPS проверить окно** выбрано при настройке. Службы MVC регистрируются методом фреймворка впрыска `ConfigureServices()` зависимости. Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее программное обеспечение статических `Configure()` файлов:

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

### <a name="wwwroot-folder"></a>wwwroot папка

В ASP.NET Core веб-папка—корень— это папка, в которой приложение ищет статические файлы.

### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core рассматривает файлы под *названием Index* как страницу по умолчанию/домашнюю страницу для сайта. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml будет** отображаться в качестве главной страницы для вашего приложения.

### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложений:

- Значок **полного цвета** размером 192 х 192 пикселей.
- **Прозрачная иконка контура** размером 32 х 32 пикселя.
- В **manifest.jsфайле,** в который указаны атрибуты приложения.

Эти файлы должны быть застегнуты на молнии в пакете приложений для использования в загрузке вкладки, чтобы Teams. Microsoft Teams загрузит `contentUrl` указанное в манифесте, встраивает его в <iframe \> и отображает в вкладке.

### <a name="csproj"></a>.csproj

В окне Visual Studio Solution Explorer нажмите правой кнопкой мыши на проекте и выберите **Project файл.** В нижней части файла вы увидите код, который создает и обновляет папку zip при сборке приложения:

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

- Откройте подсказку команды в корне каталога проекта и запустите следующую команду:

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

- Ngrok будет слушать запросы из Интернета и будет маршрут их к вашему приложению, когда он работает на порт 44325.  Он должен `https://y8rPrT2b.ngrok.io/` *напоминать, где y8rPrT2b* заменяется вашим ngrok альфа-числом HTTPS URL.

- Не забудьте сохранить подсказку команды с ngrok работает, и сделать заметку о URL - вам это понадобится позже.

- **Убедитесь, что ngrok** работает и работает должным образом, открыв браузер и переходя на страницу содержимого через URL ngrok HTTPS, который был предоставлен в окне оперативной команды.

>[!TIP]
>Вы должны иметь как ваше приложение в Visual Studio ngrok работает, чтобы завершить этот быстрый старт. Если вам нужно прекратить запуск приложения в Visual Studio над ним, **продолжайте работать ngrok.** Он будет продолжать слушать и возобновит маршрутизацию запроса вашего приложения, когда он перезапустится в Visual Studio. Если вам придется перезапустить службу ngrok он вернет новый URL, и вам придется обновлять каждое место, которое использует этот URL.

### <a name="run-your-application"></a>Вы запустите приложение

- В Visual Studio **нажмите F5** или **выберите Start Debugging** из меню **отладки приложения.**

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Создание пользовательской персональной вкладки с помощью ASP.NETCore MVC](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
