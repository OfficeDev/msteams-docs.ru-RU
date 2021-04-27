---
title: Создание личной вкладки с помощью ASP. NET Core MVC
author: laujan
description: Руководство quickstart по созданию настраиваемой личной вкладки с помощью ASP. NET Core MVC.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 3ec6b5c054384653e30e46cbffed4a2af6662c33
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019568"
---
# <a name="create-a-custom-personal-tab-with-asp-net-core-mvc"></a>Создайте настраиваемую личную вкладку с помощью ASP. NET Core MVC

В этом quickstart мы создам настраиваемую личную вкладку с C# и ASP. Net Core MVC. Кроме того, мы будем использовать [App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) для окончательного развертывания манифеста приложения и развертывания вкладки в Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Получить исходный код

Откройте командную подсказку и создайте новый каталог для проекта вкладки. Мы предоставили простой проект для начала работы. Чтобы получить исходный код, вы можете скачать папку zip и извлечь файлы или клонировать репозиторий образца в новый каталог:

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

После того как у вас есть исходный код, откройте Visual Studio и выберите **Открыть проект или решение**. Перейдите к каталогу приложений вкладок и откройте **PersonalTabMVC.sln**.

Для создания и запуска приложения нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки.** В браузере перейдите к URL-адресам ниже, чтобы убедиться, что приложение загружено правильно:

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a>Просмотр исходных кодов

### <a name="startupcs"></a>Startup.cs

Этот проект был создан из asP. Net Core 2.2 Веб-приложение пустой шаблон с *расширенным - Настройка для https* check box, выбранного при установке. Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей. Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому к методу добавляется среднее по статическим `Configure()` файлам:

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

### <a name="wwwroot-folder"></a>папка wwwroot

В ASP. NET Core — это веб-корневая папка, в которой приложение ищет статические файлы.

### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложений:

* Значок **полного цвета** размером 192 x 192 пикселя.
* Прозрачный **значок контура** размером 32 x 32 пикселя.
* Файл **manifest.js,** который указывает атрибуты приложения.

Эти файлы необходимо использовать в пакете приложений для отправки вкладки в Teams. Microsoft Teams загрузит указанное в манифесте, встраит его в `contentUrl` IFrame и отрисует его на вкладке.

### <a name="csproj"></a>.csproj

В окне Visual Studio обозревателя решений щелкните правой кнопкой мыши по проекту и выберите **Файл редактирования проекта.** В нижней части файла вы увидите код, который создает и обновляет папку zip при создании приложения:

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

*PersonalTab.cs* представляет объект Сообщения и методы, которые будут вызваны из *PersonalTabController,* когда пользователь выбирает кнопку в *представлении PersonalTab.*

### <a name="views"></a>Представления

#### <a name="home"></a>Главная

ASP. Net Core обрабатывает *файлы,* называемые Index, как домашняя страница по умолчанию для сайта. Когда URL-адрес браузера указывает на корень сайта, *Index.cshtml* будет отображаться в качестве домашней страницы приложения.

#### <a name="shared"></a>Shared

Частичная разметка *_Layout.cshtml* содержит общую структуру страницы приложения и общие визуальные элементы. Он также будет ссылаться на библиотеку teams.

### <a name="controllers"></a>Контроллеры

Контроллеры используют свойство ViewBag для динамической передачи значений в Представления.

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* Откройте командную подсказку в корневом каталоге проекта и запустите следующую команду:

``` bash
ngrok http https://localhost:44345 -host-header="localhost:44345"
```

* Ngrok будет прослушивать запросы из Интернета и перенанастрает их в ваше приложение, когда оно запущено в порту 44325.  Он должен `https://y8rPrT2b.ngrok.io/` напоминать, где *y8rPrT2b* заменяется url-адресом https ngrok alpha-numeric HTTPS.

* Убедитесь в том, что командная подсказка будет запущена с помощью ngrok, и обратите внимание на URL-адрес , который вам понадобится позже.

* Убедитесь, что *ngrok* работает и работает должным образом, открыв браузер и переехав на страницу контента через URL-адрес https ngrok, который был представлен в окне командной подсказки.

> [! СОВЕТ] Чтобы выполнить эту быструю работу, необходимо Visual Studio и ngrok. Если для работы с приложением необходимо прекратить Visual Studio, продолжайте **работать с ngrok.** После перезапуска в Visual Studio он продолжит прослушивание и возобновит маршрутизаку запроса приложения. Если вам придется перезапустить службу ngrok, она возвращает новый URL-адрес, и вам придется обновить каждое место, использующее этот URL-адрес.

### <a name="run-your-application"></a>Запуск приложения

* В Visual Studio **нажмите кнопку F5** или **выберите Пуск** отладки из меню отладки **приложения.**

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
