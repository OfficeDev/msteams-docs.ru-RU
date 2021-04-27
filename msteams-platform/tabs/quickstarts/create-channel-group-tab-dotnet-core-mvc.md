---
title: Создание вкладки каналов и групп с ASP.NET MVC
author: laujan
description: Руководство quickstart по созданию настраиваемой вкладки канала и группы с ASP.NET Core MVC
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 9d89fd98bae9732a8f9e2d34b82d7fc0e6985e01
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020312"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a>Создание настраиваемой вкладки канала и группы с ASP.NET MVC

В этом quickstart мы создам настраиваемую вкладку channel/group с C# и ASP.Net core MVC. Кроме того, мы будем использовать [App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) для окончательного развертывания манифеста приложения и развертывания вкладки в Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Получить исходный код

Откройте командную подсказку и создайте новый каталог для проекта вкладки. Мы предоставили простой проект [Вкладки группы каналов](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) для начала работы. Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в новый каталог:

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

После того как у вас есть исходный код, откройте Visual Studio и выберите **Открыть проект или решение**. Перейдите к каталогу приложений вкладок и откройте **ChannelGroupTabMVC.sln**.

Для создания и запуска приложения нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки.** В браузере перейдите к URL-адресам ниже и убедитесь, что приложение загружено правильно:

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a>Просмотр исходных кодов

### <a name="startupcs"></a>Startup.cs

Этот проект был создан из пустого шаблона ASP.NET Core 2.2 веб-приложения с расширенным - Настройка для *httpS-окна,* выбранного при установке. Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей. Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее по статическим `Configure()` файлам:

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

В ASP.NET Core веб-корневая папка — это место, где приложение ищет статические файлы.

### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложений:

- Значок **полного цвета** размером 192 x 192 пикселя.
- Прозрачный **значок контура** размером 32 x 32 пикселя.
- Файл **manifest.js,** который указывает атрибуты приложения.

Эти файлы необходимо использовать в пакете приложений для отправки вкладки в Teams.

### <a name="csproj"></a>.csproj

В окне Visual Studio обозревателя решений щелкните правой кнопкой мыши по проекту и выберите **Файл редактирования проекта.** В нижней части файла вы увидите код, который создает и обновляет папку zip при создании приложения:

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

*ChannelGroup.cs представляет* объект Сообщения и методы, которые будут вызваны из контроллеров во время настройки.

### <a name="views"></a>Представления

#### <a name="home"></a>Главная

ASP.NET Core обрабатывает файлы под названием *Index* в качестве домашней страницы по умолчанию для сайта. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** будет отображаться в качестве домашней страницы приложения.

#### <a name="shared"></a>Shared

Частичная разметка *_Layout.cshtml* содержит общую структуру страницы приложения и общие визуальные элементы. Он также будет ссылаться на библиотеку teams.

### <a name="controllers"></a>Контроллеры

Контроллеры используют свойство ViewBag для динамической передачи значений в Представления.

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- Откройте командную подсказку в корневом каталоге проекта и запустите следующую команду:

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- Ngrok будет прослушивать запросы из Интернета и перенанастрает их в ваше приложение, когда оно запущено в порту 44355.  Он должен `https://y8rCgT2b.ngrok.io/` напоминать, где *y8rCgT2b* заменяется url-адресом https ngrok alpha-numeric HTTPS.

- Убедитесь в том, что командная подсказка будет запущена с помощью ngrok, и обратите внимание на URL-адрес , который вам понадобится позже.

## <a name="update-your-application"></a>Обновление приложения

В **Tab.cshtml** приложение представляет пользователю две кнопки параметра для отображения вкладки с красным или серым значком. Выбор кнопки **Выберите серый** или **выберите** красный или, соответственно, задает и включает кнопку Сохранить `saveGray()` на странице `saveRed()` `settings.setValidityState(true)` конфигурации.  Этот код позволяет Teams узнать, что вы удовлетворили требования к конфигурации и установка может продолжиться. При сохранения `settings.setSettings` заданы параметры. Наконец, `saveEvent.notifySuccess()` называется, чтобы указать, что URL-адрес контента успешно решен.

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
