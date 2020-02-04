---
title: Создание личной вкладки с ядром ASP.NET
author: laujan
description: Руководство по созданию настраиваемой личной вкладки с ядром ASP.NET.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: b279c96f47265fe1928ae90d661e7dc042085b39
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675631"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core"></a>Создание настраиваемой вкладки личных компонентов с ASP.NET

В этом руководстве мы рассмотрим создание настраиваемой вкладки личного уровня с основными страницами Razor для C# и ASP.Net. Мы также используем [Приложение App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) , чтобы завершить манифест приложения и развернуть вкладку в Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Получение исходного кода

Откройте командную строку и создайте новый каталог для проекта со вкладками. Мы предоставили простой проект, чтобы приступить к работе. Чтобы получить исходный код, можно скачать папку ZIP и извлечь файлы или клонировать репозиторий примера в новый каталог:

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

После создания исходного кода откройте Visual Studio и выберите **Открыть проект или решение**. Перейдите в каталог приложений вкладки и откройте **персоналтаб. sln**.

Чтобы построить и запустить приложение, нажмите клавишу **F5** или в меню **Отладка** выберите команду **начать отладку** . В браузере перейдите по следующим URL-адресам, чтобы убедиться, что приложение загружено должным образом:

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a>Просмотр исходного кода

### <a name="startupcs"></a>Startup.cs

Этот проект был создан из пустого шаблона веб-приложения ASP.NET Core 2,2 с установленным флажком *Расширенная настройка для HTTPS* , установленным во время установки. Службы MVC регистрируются `ConfigureServices()` методом платформы внедрения зависимостей. Кроме того, по умолчанию в пустом шаблоне не включается возможность обслуживания статического содержимого, поэтому в `Configure()` метод добавляется промежуточное по промежуточным файлам.

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

### <a name="wwwroot-folder"></a>Папка wwwroot

В ядре ASP.NET корневая папка веб-сайта — это место, в котором приложение выполняет поиск статических файлов.

### <a name="indexcshtml"></a>Index. cshtml

ASP.NET Core рассматривает файлы с именем *index* как страницу по умолчанию или домашнюю страницу сайта. Если URL-адрес браузера указывает на корневой сайт сайта, в качестве домашней страницы для приложения будет отображаться **index. cshtml** .

### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие обязательные файлы пакета приложения:

- **Значок с полным цветом** , измеряющий 192 x 192 пикселей.
- **Прозрачный значок структуры** , измеряющий 32 x 32 пикселей.
- Файл **manifest. JSON** , задающий атрибуты приложения.

Эти файлы необходимо заархивировать в пакете приложения для использования при загрузке вкладки в Teams. Microsoft Teams загрузит `contentUrl` указанное в манифесте, внедрите его в IFRAME и откроет его на вкладке.

### <a name="csproj"></a>CSPROJ

В окне обозревателя решений Visual Studio щелкните правой кнопкой мыши проект и выберите команду **изменить файл проекта**. В нижней части файла вы увидите код, который создает и обновляет папку zip при построении приложения:

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

- Откройте командную строку в корне каталога проекта и выполните следующую команду:

```bash
ngrok http https://localhost:44325 -host-header="localhost:44325"
```

- Ngrok прослушивает запросы из Интернета и направляет их в ваше приложение, когда оно выполняется на порте 44325.  Он должен выглядеть примерно `https://y8rPrT2b.ngrok.io/` так, где *y8rPrT2b* заменяется URL-адресом https ngrok, сооснованным на цифровом алфавите.

- Убедитесь, что Командная строка ngrok запущена, и запишите URL-адрес, он понадобится позже.

- Убедитесь, что *ngrok* работает и правильно работает, открыв браузер и перейдя на страницу содержимого с помощью URL-адреса ngrok HTTPS, который был предоставлен в окне командной строки.

>[!TIP]
>Для выполнения этого краткого руководства необходимо одновременное выполнение приложения в Visual Studio и ngrok. Если вам нужно остановить работу приложения в Visual Studio для работы с ним, **Держите ngrok**в рабочем процессе. Он будет продолжать прослушивать и возобновить маршрутизацию запроса приложения при его перезапуске в Visual Studio. Если необходимо перезапустить службу ngrok, будет возвращен новый URL-адрес, и вам потребуется обновить все место, где используется этот URL-адрес.

### <a name="run-your-application"></a>Запуск приложения

- В Visual Studio нажмите клавишу **F5** или выберите команду **начать отладку** в меню **Отладка** приложения.

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
