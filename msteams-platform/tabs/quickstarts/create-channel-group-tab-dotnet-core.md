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
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core"></a>Создание настраиваемой вкладки каналов и групп с ядром ASP.NET

В этом руководстве мы рассмотрим создание настраиваемой вкладки каналов/групп с помощью C# и ASP.Net основной страницы Razor. Мы также используем [Приложение App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) , чтобы завершить манифест приложения и развернуть вкладку в Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Получение исходного кода

Откройте командную строку и создайте новый каталог для проекта со вкладками. Мы предоставили простой проект, чтобы приступить к работе. Чтобы получить исходный код, можно скачать папку ZIP и извлечь файлы или клонировать репозиторий примера в новый каталог:

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

После создания исходного кода откройте Visual Studio и выберите **Открыть проект или решение**. Перейдите в каталог приложений вкладки и откройте **чаннелграуптаб. sln**.

Чтобы построить и запустить приложение, нажмите клавишу **F5** или в меню **Отладка** выберите команду **начать отладку** . В браузере перейдите к следующим URL-адресам и убедитесь, что приложение загружено правильно:

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

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

### <a name="tabcs"></a>Tab.cs

Этот файл C# содержит метод, который будет вызываться из **TAB. cshtml** во время настройки.

### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие обязательные файлы пакета приложения:

- **Значок с полным цветом** , измеряющий 192 x 192 пикселей.
- **Прозрачный значок структуры** , измеряющий 32 x 32 пикселей.
- Файл **manifest. JSON** , задающий атрибуты приложения.

Эти файлы необходимо заархивировать в пакете приложения для использования при загрузке вкладки в Teams. Когда пользователь выбирает Добавление или обновление вкладки, Microsoft Teams загружает `configurationUrl` указанную в манифесте, внедряет ее в Интернет, а затем отображает ее на вкладке.

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

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- Откройте командную строку в корне каталога проекта и выполните следующую команду:

```bash
ngrok http https://localhost:44355 -host-header="localhost:44355"
```

- Ngrok прослушивает запросы из Интернета и направляет их в ваше приложение, когда оно выполняется на порте 44355. Он должен выглядеть примерно `https://y8rCgT2b.ngrok.io/` так, где *y8rCgT2b* заменяется URL-адресом https ngrok, сооснованным на цифровом алфавите.

- Убедитесь, что Командная строка ngrok запущена и запишите URL-адрес, а затем это потребуется позже.

## <a name="update-your-application"></a>Обновление приложения

В пределах *TAB. cshtml* приложение предоставляет пользователю два переключателя для отображения вкладки с помощью значка красного или серого. При `saveRed()`нажатии `settings.setValidityState(true)`кнопки `saveGray()` **выбрать серое** или **выбрать красную** , соответственно, задает набор и активируется кнопка **сохранить** на странице Конфигурация. Этот код позволяет Teams знать, что вы удовлетворены требованиями к конфигурации и можете продолжить установку. При сохранении задаются параметры `settings.setSettings` . `saveEvent.notifySuccess()` Finally вызывается, чтобы показать, что URL-адрес контента успешно разрешен.

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
