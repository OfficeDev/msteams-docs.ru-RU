---
title: Создание вкладки каналов и групп с ASP.NET основной MVC
author: laujan
description: Краткое руководство по созданию настраиваемой вкладки каналов и групп с ASP.NET основной MVC.
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: cda91825ee37da94ee84747c5d2439c2940c728b
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818929"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a>Создание настраиваемой вкладки каналов и групп с ASP.NET основной MVC

В этом руководстве мы рассмотрим создание настраиваемой вкладки канал/группа с помощью C# и ASP.Net Core MVC. Мы также используем [Приложение App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) , чтобы завершить манифест приложения и развернуть вкладку в Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Получение исходного кода

Откройте командную строку и создайте новый каталог для проекта со вкладками. Чтобы приступить к работе, мы предоставили проект [вкладки простой группы каналов](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) . Чтобы получить исходный код, можно скачать папку ZIP и извлечь файлы или клонировать репозиторий примера в новый каталог:

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

После создания исходного кода откройте Visual Studio и выберите **Открыть проект или решение**. Перейдите в каталог приложений вкладки и откройте **чаннелграуптабмвк. sln**.

Чтобы построить и запустить приложение, нажмите клавишу **F5** или в меню **Отладка** выберите команду **начать отладку** . В браузере перейдите по приведенным ниже URL-адресам и убедитесь, что приложение загружено правильно:

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a>Просмотр исходного кода

### <a name="startupcs"></a>Startup.cs

Этот проект был создан из пустого шаблона веб-приложения ASP.NET Core 2,2 с установленным флажком *Расширенная настройка для HTTPS* , установленным во время установки. Службы MVC регистрируются методом платформы внедрения зависимостей `ConfigureServices()` . Кроме того, по умолчанию в пустом шаблоне не включается возможность обслуживания статического содержимого, поэтому в метод добавляется промежуточное по промежуточным файлам `Configure()` .

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

### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие обязательные файлы пакета приложения:

- **Значок с полным цветом** , измеряющий 192 x 192 пикселей.
- **Прозрачный значок структуры** , измеряющий 32 x 32 пикселей.
- **manifest.js** файла, определяющего атрибуты приложения.

Эти файлы необходимо заархивировать в пакете приложения для использования при загрузке вкладки в Teams.

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

### <a name="models"></a>Модели

*ChannelGroup.CS* представляет объект сообщения и методы, которые будут вызываться из контроллеров во время настройки.

### <a name="views"></a>Представления

#### <a name="home"></a>Домашняя

ASP.NET Core рассматривает файлы с именем *index* как страницу по умолчанию или домашнюю страницу сайта. Если URL-адрес браузера указывает на корневой сайт сайта, в качестве домашней страницы для приложения будет отображаться **index. cshtml** .

#### <a name="shared"></a>Shared

Разметка частичного представления *_layout. cshtml* содержит общую структуру страницы и общие визуальные элементы приложения. Он также будет ссылаться на библиотеку Teams.

### <a name="controllers"></a>Controller

Контроллеры используют свойство Виевбаг для динамического переноса значений в представлениях.

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- Откройте командную строку в корне каталога проекта и выполните следующую команду:

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- Ngrok прослушивает запросы из Интернета и направляет их в ваше приложение, когда оно выполняется на порте 44355.  Он должен выглядеть примерно так `https://y8rCgT2b.ngrok.io/` , где *y8rCgT2b* ЗАМЕНЯЕТСЯ URL-адресом https ngrok, сооснованным на цифровом алфавите.

- Убедитесь, что Командная строка ngrok запущена и запишите URL-адрес, а затем это потребуется позже.

## <a name="update-your-application"></a>Обновление приложения

В пределах **TAB. cshtml** приложение предоставляет пользователю два переключателя для отображения вкладки с помощью значка красного или серого. При нажатии кнопки **выбрать серое** или **выбрать красную** , `saveGray()` `saveRed()` соответственно, задает набор `settings.setValidityState(true)` и активируется кнопка **сохранить** на странице Конфигурация. Этот код позволяет Teams знать, что вы удовлетворены требованиями к конфигурации и можете продолжить установку. При сохранении `settings.setSettings` задаются параметры. Finally `saveEvent.notifySuccess()` вызывается, чтобы показать, что URL-адрес контента успешно разрешен.

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
