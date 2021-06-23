---
title: Создание личной вкладки с помощью ASP.NET Core
author: surbhigupta
description: Руководство quickstart по созданию настраиваемой личной вкладки с ASP.NET Core.
ms.topic: quickstart
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: a839ae126a2cfdb137b22108038dd15a4b47b95a
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069048"
---
# <a name="create-a-personal-tab-using-aspnetcore"></a>Создание личной вкладки с помощью ASP.NETCore

В этом quickstart мы создам настраиваемую личную вкладку со страницами C# ASP.Net Core Razor. Мы также используем [App Studio для](~/concepts/build-and-test/app-studio-overview.md) Microsoft Teams манифеста приложения и развертывания вкладки Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Получить исходный код

Откройте командную подсказку и создайте новый каталог для проекта вкладки. Мы предоставили простой проект для начала работы. Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в новый каталог:

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

После того как у вас есть исходный код, откройте Visual Studio и выберите **Открыть проект или решение**. Перейдите к каталогу приложений вкладок и откройте **PersonalTab.sln**.

Для создания и запуска приложения нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки.** В браузере перейдите к URL-адресам ниже, чтобы проверить правильно загруженные приложения:

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a>Просмотр исходных кодов

### <a name="startupcs"></a>Startup.cs

Этот проект был создан из пустого шаблона ASP.NET Core 2.2 веб-приложения с расширенным — настройка для контрольного окна **HTTPS,** выбранного при установке. Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей. Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее по статическим `Configure()` файлам:

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

### <a name="wwwroot-folder"></a>папка wwwroot

В ASP.NET Core веб-корневой папке приложение ищет статические файлы.

### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core обрабатывает файлы под названием *Index* в качестве домашней страницы по умолчанию для сайта. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** будет отображаться в качестве домашней страницы приложения.

### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложений:

- Значок **полного цвета** размером 192 x 192 пикселя.
- Прозрачный **значок контура** размером 32 x 32 пикселя.
- Файл **manifest.js,** который указывает атрибуты приложения.

Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams. Microsoft Teams загрузите указанное в манифесте, встраите его в <iframe и отрисуйте на `contentUrl` \> вкладке.

### <a name="csproj"></a>.csproj

В окне Visual Studio обозревателя решений щелкните правой кнопкой мыши по проекту и выберите **Изменить Project Файл**. В нижней части файла вы увидите код, который создает и обновляет папку zip при создании приложения:

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

- Откройте командную подсказку в корневом каталоге проекта и запустите следующую команду:

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

- Ngrok будет прослушивать запросы из Интернета и перенанастрает их в ваше приложение, когда оно запущено в порту 44325.  Он должен `https://y8rPrT2b.ngrok.io/` напоминать, где *y8rPrT2b* заменяется url-адресом https ngrok alpha-numeric HTTPS.

- Убедитесь в том, что командная подсказка будет запущена с помощью ngrok, и обратите внимание на URL-адрес , который вам понадобится позже.

- Убедитесь, что **ngrok** работает и работает должным образом, открыв браузер и переехав на страницу контента через URL-адрес https ngrok, который был представлен в окне командной подсказки.

>[!TIP]
>Для выполнения этого quickstart необходимо Visual Studio и ngrok. Если для работы с приложением необходимо прекратить Visual Studio, продолжайте **работать с ngrok.** После перезапуска в Visual Studio он будет продолжать прослушивать запрос приложения и возобновлять маршрутиза Visual Studio. Если вам придется перезапустить службу ngrok, она возвращает новый URL-адрес, и вам придется обновить каждое место, использующее этот URL-адрес.

### <a name="run-your-application"></a>Запуск приложения

- В Visual Studio нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки** приложения.

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание настраиваемой личной вкладки с помощью MVC ASP.NETCore](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
