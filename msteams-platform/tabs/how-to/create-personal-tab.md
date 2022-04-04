---
title: Создание личной вкладки
author: laujan
description: Руководство quickstart по созданию личной вкладки с генератором Yeoman, ASP.NET Core или ASP.NET Core MVC для Microsoft Teams с помощью Node.js и обновления манифеста приложения.
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
keywords: yeoman ASP.NET MVC пакет appmanifest магазин разрешений домена разговора
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: d19ecc04aa14561d443a65d4ea896c210fdf4d94
ms.sourcegitcommit: 3d6aa10d2f58a63c6a4281a30e8771469dba0d0b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2022
ms.locfileid: "64636166"
---
# <a name="create-a-personal-tab"></a>Создание личной вкладки

Личные вкладки, как и персональные боты, являются частью личных приложений и доступны только одному пользователю. Их можно прикрепить к левой области для легкого доступа. Вы также можете [переустроить](#reorder-static-personal-tabs) и добавить [`registerOnFocused` API](#add-registeronfocused-api-for-tabs-or-personal-apps) для личных вкладок.

Убедитесь, что у вас есть все [prerequsites](~/tabs/how-to/tab-requirements.md) для создания личной вкладки.

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>Создайте личную вкладку с Node.js

1. В командной подсказке установите [пакеты Yeoman](https://yeoman.io/) и [gulp-cli](https://www.npmjs.com/package/gulp-cli) , введите следующую команду после установки Node.js:

    ```cmd
    npm install yo gulp-cli --global
    ```

1. В командной подсказке установите Microsoft Teams app generator, введите следующую команду:

    ```cmd
    npm install generator-teams --global
    ```

Ниже следующую информацию о создании личной вкладки:

1. [Создание приложения с помощью личной вкладки](#generate-your-application-with-a-personal-tab)
1. [Добавление страницы контента на личную вкладку](#add-a-content-page-to-the-personal-tab)
1. [Создание пакета приложения](#create-your-app-package)
1. [Сборка и запуск приложения](#build-and-run-your-application)
1. [Создание безопасного туннеля на личной вкладке](#establish-a-secure-tunnel-to-your-tab)
1. [Upload приложение для Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Создание приложения с помощью личной вкладки

1. В командной подсказке создайте новый каталог для личной вкладки.

1. Введите следующую команду в новом каталоге, чтобы запустить Microsoft Teams app:

    ```cmd
    yo teams
    ```

1. Предодавайте значения ряду вопросов, задамых генератором Microsoft Teams для обновления файла **manifest.json**.

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="Teams генератор" border="true":::

    <details>
    <summary><b>Серия вопросов для обновления файла manifest.json</b></summary>

    * **Как называется решение?**

      Имя решения — это имя проекта. Вы можете принять предложенное имя, выбрав **Ввод**.

    * **Где следует разместить файлы?**

      В настоящее время вы в каталоге проектов. Выберите **Ввод**.

    * **Название проекта Microsoft Teams приложения?**

      Название — это имя пакета приложений и используется в манифесте и описании приложения. Введите название или выберите **Ввод,** чтобы принять имя по умолчанию.

    * **Ваше (компания) имя? (максимум 32 символа)**

      Имя вашей компании будет использоваться в манифесте приложения. Введите имя компании или выберите **Ввод,** чтобы принять имя по умолчанию.

    * **Какую версию манифеста вы бы хотели использовать?**

      Выберите схему по умолчанию.

    * **Быстрый строительный лес? (Y/n)**

      По умолчанию — да; **введите n** , чтобы ввести свой microsoft Partner ID.

    * **Введите свой microsoft Partner Id, если он у вас есть? (Оставьте пустым, чтобы пропустить)**

      Это поле не требуется и должно использоваться только в том случае, если вы уже входите в [сеть партнеров Майкрософт](https://partner.microsoft.com).

    * **Что нужно добавить в проект?**

      Выберите **( &ast; ) Вкладка**.

    * **URL-адрес, на котором будет организовано это решение?**

      По умолчанию генератор предлагает URL-адрес веб-сайтов Azure. Вы тестируете приложение только локально, поэтому допустимый URL-адрес не требуется.

    * **Хотите показать индикатор загрузки при загрузке приложения и вкладки?**

      Выберите **не** включать индикатор загрузки при загрузке приложения или вкладки. По умолчанию нет, введите **n**.

    * **Вы хотите, чтобы личные приложения отображались без строки заголовков вкладок?**

      Не **следует** включать личные приложения, которые будут отрисовки без заглавной панели вкладок. По умолчанию нет, введите **n**.

    * **Хотите включить тестовые рамки и начальные тесты? (y/N)**

      Выберите **не** включать тестовую базу для этого проекта. По умолчанию нет, введите **n**.

    * **Хотите включить поддержку ESLint? (y/N)**

      Не включать поддержку ESLint. По умолчанию нет, введите **n**.

    * **Хотите использовать приложения Azure Аналитика для телеметрии? (y/N)**

      Выберите **не** включать [приложение Azure Аналитика](/azure/azure-monitor/app/app-insights-overview). По умолчанию нет; **введите n**.

    * **Имя вкладки по умолчанию (максимум 16 символов)?**

      Назови свою вкладку. Это имя вкладки используется во всем проекте в качестве компонента пути к файлу или URL-адресу.

    * **Какую вкладку вы хотели бы создать?**

      Используйте клавиши стрелки для выбора **Личного (статического)**.

    * **Требуется ли Microsoft Azure Active Directory (Azure AD) для единой входной поддержки вкладки?**

      Не **включай** поддержку для вкладки Azure AD с одним входом. По умолчанию — да, введите **n**.

    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>Добавление страницы контента на личную вкладку

Создайте страницу контента и обновите существующие файлы приложения личной вкладки:

1. Создайте новый **файлpersonal.html** в Visual Studio Code с помощью следующей разметки:

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

1. **Сохранитеpersonal.html** **в общедоступных** папках приложения в следующем расположении:

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. Откройте **manifest.json из** следующего расположения в Visual Studio Code:

    ```
     ./src/manifest/manifest.json
    ```

1. Добавьте следующее в пустой массив `staticTabs` (`staticTabs":[]`) и добавьте следующий объект JSON:

    ```json
    {
        "entityId": "personalTab",
        "name": "Personal Tab ",
        "contentUrl": "https://{{PUBLIC_HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
        "websiteUrl": "https://{{PUBLIC_HOSTNAME}}",
        "scopes": ["personal"]
    }
    ```

    > [!IMPORTANT]
    > Компонент пути **yourDefaultTabNameTab** — это значение, которое вы ввели в генератор имени вкладки по **умолчанию плюс слово** **Tab**.
    >
    > Например: DefaultTabName **— это MyTab** then **/MyTabTab/**

1. **Обновите компонент пути contentURL** **yourDefaultTabNameTab с** фактическим именем вкладки.

1. Сохраните обновленный **файл manifest.json** .

1. Откройте **tab.ts** в Visual Studio Code из следующего пути, чтобы предоставить свою страницу контента в IFrame:

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. Добавьте в список декораторов IFrame следующее:

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. Сохраните обновленный файл. Код вкладки завершен.

### <a name="create-your-app-package"></a>Создание пакета приложения

Для создания и запуска приложения в Teams необходимо иметь пакет Teams. Пакет приложения создается с помощью задачи gulp, которая проверяет файл **manifest.json** и создает папку **zip в каталоге ./package** . В командной строке введите следующую команду:

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>Сборка и запуск приложения

#### <a name="build-your-application"></a>Сборка приложения

Введите следующую команду в командной подсказке, чтобы переводить решение в **папку ./dist** :

```cmd
gulp build
```

#### <a name="run-your-application"></a>Запуск приложения

1. В командной подсказке введите следующую команду для запуска локального веб-сервера:

    ```cmd
    gulp serve
    ```

1. Введите `http://localhost:3007/<yourDefaultAppNameTab>/` в браузере, чтобы просмотреть домашняя страница приложения.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Вкладка по умолчанию" border="true":::

1. Просмотр `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`, чтобы просмотреть вашу личную вкладку.

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="Html Tab по умолчанию" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Создание безопасного туннеля на вкладке

По командной подсказке выйдите из локального канала и введите следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> После того как вкладка будет загружена Microsoft Teams **ngrok** и успешно сохранена, ее можно просмотреть в Teams до окончания сеанса туннеля.

### <a name="upload-your-application-to-teams"></a>Upload приложение для Teams

1. Перейдите Microsoft Teams и выберите **Store**&nbsp; :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::.
1. Выберите **Управление приложениями**
1. Выберите **Опубликовать приложение** **и Upload настраиваемом приложении**.

    :::image type="content" source="~/assets/images/tab-images/publish-app.png" alt-text="Upload настраиваемом приложении" border="true":::

1. Перейдите в каталог проекта, просмотрите **папку ./package**, выберите папку zip **и откройте.**

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="Добавление личной вкладки" border="true":::

1. Выберите **Добавить** в диалоговом ок. Вкладка загружается в Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="Загруженная личная вкладка" border="true":::

1. В левой области Teams выберите эллипсы &#x25CF;&#x25CF;&#x25CF; и выберите загруженные приложения для просмотра личной вкладки.

   Теперь вы создали и добавили личную вкладку в Teams.
  
   Поскольку ваша личная вкладка Teams, [](#reorder-static-personal-tabs) [`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps) вы также можете перенастроить и добавить API для личной вкладки.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>Создайте личную вкладку с ASP.NET Core

1. В командной подсказке создайте новый каталог для проекта вкладки.

1. Клонировать репозиторий образца в новый каталог с помощью следующей команды или можно [](https://github.com/OfficeDev/Microsoft-Teams-Samples) скачать исходный код и извлечь файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже следующую информацию о создании личной вкладки:

1. [Создание приложения с помощью личной вкладки](#generate-your-application-with-a-personal-tab-1)
1. [Обновление и запуск приложения](#update-and-run-your-application)
1. [Создание безопасного туннеля на вкладке](#establish-a-secure-tunnel-to-your-tab-1)
1. [Обновление пакета приложений с помощью портала разработчиков](#update-your-app-package-with-developer-portal)
1. [Просмотр приложения в Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Создание приложения с помощью личной вкладки

1. Откройте Visual Studio и **выберите Откройте проект или решение**.

1. Перейдите в папку Microsoft-Teams-Samplessamplestab-personalrazor-csharp  >  >  >  и откройте **PersonalTab.sln**.

1. В Visual Studio выберите **F5** или выберите Пуск отладки  из меню отладки приложения, чтобы проверить правильность загрузки приложения. В браузере перейдите к следующим URL-адресам:

    * <http://localhost:3978/>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Просмотр исходных кодов</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан из пустого шаблона ASP.NET Core 3.1 веб-приложения с расширенным **- Настройка для проверки HTTPS**, выбранной при установке. Службы MVC регистрируются методом впрыскивания зависимостей `ConfigureServices()` . Кроме того, пустой шаблон не позволяет обслуживать статический контент по умолчанию, `Configure()` поэтому в метод добавляется среднее по статическим файлам с помощью следующего кода:

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

#### <a name="wwwroot-folder"></a>папка wwwroot

В ASP.NET Core веб-корневой папке приложение ищет статические файлы.

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core относится к файлам, называемым **Index**, как к домашней странице по умолчанию для сайта. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** отображается в качестве домашней страницы приложения.

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложений:

* **Значок полного цвета** размером 192 x 192 пикселя.
* **Прозрачный значок контура** размером 32 x 32 пикселя.
* Файл **manifest.json** , который указывает атрибуты вашего приложения.

Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams. Microsoft Teams загружает `contentUrl` указанное в манифесте, встраив его в <iframe\> и отрисовка его на вкладке.

#### <a name="csproj"></a>.csproj

В Visual Studio Обозреватель решений нажмите правой кнопкой мыши на проекте и выберите **Изменить Project файл**. В конце файла можно увидеть следующий код, который создает и обновляет папку zip при создании приложения:

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

</details>

### <a name="update-and-run-your-application"></a>Обновление и запуск приложения

1. Откройте Visual Studio Обозреватель решений и перейдите в **папку PagesShared** >  **и откройте _Layout.cshtml** `<head>` и добавьте в раздел теги следующее:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. В Visual Studio Обозреватель решений **откройте PersonalTab.cshtml** из папки **Pages** и добавьте `microsoftTeams.initialize()` `<script>` теги и сохраните.

1. В Visual Studio выберите **F5** **или выберите Пуск** отладки из меню отладки **приложения**.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Создание безопасного туннеля на вкладке

На командной подсказке в корневом каталоге проекта запустите следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Обновление пакета приложений с помощью портала разработчиков

1. Перейдите на [**портал Разработчик.**](https://dev.teams.microsoft.com/home)

1. Откройте **приложения** и выберите **импортное приложение**.

1. Имя вашего пакета **приложенийtab.zip.** Он доступен по следующему пути:

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Выберите **tab.zip** и откройте его на портале разработчиков.

1. По умолчанию **создается** и заполняется ID приложения по умолчанию в **разделе Основные сведения** .

1. Добавьте краткое и длинное описание для приложения в **Описания**.

1. В **сведениях разработчика** добавьте необходимые сведения, а на веб-сайте (должен быть допустимый **URL-адрес HTTPS)** укажи URL-адрес ngrok HTTPS.

1. В **URL-адресах** приложений обновите политику конфиденциальности `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` и сохраните ее.

1. В **функции Приложения** выберите **Личный appCreate** >  **первую личную** вкладку приложения и введите имя и обновите **URL-адрес** контента с `https://<yourngrokurl>/personalTab`помощью . Оставьте поле URL-адрес веб-сайта пустым и **выберите Context** в качестве personalTab из списка dropdown и **Добавить**.

1. Выберите **Сохранить**.

1. В разделе Домены домены с вкладок должны содержать URL-адрес ngrok без префикса `<yourngrokurl>.ngrok.io`HTTPS.

### <a name="preview-your-app-in-teams"></a>Просмотр приложения в Teams

1. Выберите **предварительный просмотр Teams** панели инструментов портала разработчика, портал разработчика сообщает вам, что приложение успешно загружено боком. Страница **Добавить** отображается для приложения в Teams.

1. Выберите **Добавить** для загрузки вкладки в Teams. Вкладка теперь доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="Вкладка по умолчанию" border="true":::

   Теперь вы создали и добавили личную вкладку в Teams.
  
   Поскольку ваша личная вкладка Teams, [](#reorder-static-personal-tabs) [`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps) вы также можете перенастроить и добавить API для личной вкладки.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>Создание личной вкладки с ASP.NET Core MVC

1. В командной подсказке создайте новый каталог для проекта вкладки.

1. Клонировать репозиторий образца в новый каталог с помощью следующей команды или можно [](https://github.com/OfficeDev/Microsoft-Teams-Samples) скачать исходный код и извлечь файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже следующую информацию о создании личной вкладки:

1. [Создание приложения с помощью личной вкладки](#generate-your-application-with-a-personal-tab-2)
1. [Обновление и запуск приложения](#update-and-run-your-application-1)
1. [Создание безопасного туннеля на вкладке](#establish-a-secure-tunnel-to-your-tab-2)
1. [Обновление пакета приложений с помощью портала разработчиков](#update-your-app-package-with-developer-portal-1)
1. [Просмотр приложения в Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>Создание приложения с помощью личной вкладки

1. Откройте Visual Studio и **выберите Откройте проект или решение**.

1. Перейдите в папку Microsoft-Teams-Samplessamplestab-personalmvc-csharp  >  >  >  и откройте **PersonalTabMVC.sln** в Visual Studio.

1. В Visual Studio выберите **F5** или выберите Пуск отладки  из меню отладки приложения, чтобы проверить правильность загрузки приложения. В браузере перейдите к следующим URL-адресам:

    * <http://localhost:3978>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Просмотр исходных кодов</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан из пустого шаблона ASP.NET Core 3.1 веб-приложения с расширенным **- Настройка для проверки HTTPS**, выбранной при установке. Службы MVC регистрируются методом впрыскивания зависимостей `ConfigureServices()` . Кроме того, пустой шаблон не позволяет обслуживать статический контент по умолчанию, `Configure()` поэтому в метод добавляется среднее по статическим файлам с помощью следующего кода:

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

#### <a name="wwwroot-folder"></a>папка wwwroot

В ASP.NET Core веб-корневой папке приложение ищет статические файлы.

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложений:

* **Значок полного цвета** размером 192 x 192 пикселя.
* **Прозрачный значок контура** размером 32 x 32 пикселя.
* Файл **manifest.json** , который указывает атрибуты вашего приложения.

Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams. Microsoft Teams загружает `contentUrl` указанное в манифесте, встраив его в IFrame и отрисовывая его на вкладке.

#### <a name="csproj"></a>.csproj

В Visual Studio Обозреватель решений щелкните правой кнопкой мыши по проекту и выберите **Изменить Project файл**. В конце файла вы увидите следующий код, который создает и обновляет папку zip при создании приложения:

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

#### <a name="models"></a>Модели

**PersonalTab.cs** представляет объект сообщения и методы, которые вызваны из **PersonalTabController** , когда пользователь выбирает кнопку в **представлении PersonalTab** .

#### <a name="views"></a>Представления

Эти представления являются различными представлениями в ASP.NET Core MVC:

* Главная: ASP.NET Core обрабатывает файлы под названием **Index** в качестве домашней страницы или по умолчанию для сайта. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** отображается в качестве домашней страницы приложения.

* Общий доступ. Частичная разметка **_Layout.cshtml** содержит общую структуру страницы приложения и общие визуальные элементы. Он также ссылается на Teams библиотеку.

#### <a name="controllers"></a>Контроллеры

Контроллеры используют свойство `ViewBag` для динамической передачи значений в Представления.

</details>

### <a name="update-and-run-your-application"></a>Обновление и запуск приложения

1. Откройте Visual Studio Обозреватель решений и перейдите в **папку** **ViewsShared** >  **и откройте _Layout.cshtml** и `<head>` добавьте в раздел теги следующее:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. В Visual Studio Обозреватель решений **откройте PersonalTab.cshtml** из **папки** **ViewsPersonalTab** `microsoftTeams.initialize()` > `<script>` и добавьте в теги и сохраните.

1. В Visual Studio выберите **F5** **или выберите Пуск** отладки из меню отладки **приложения**.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Создание безопасного туннеля на вкладке

На командной подсказке в корневом каталоге проекта запустите следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Обновление пакета приложений с помощью портала разработчиков

1. Перейдите на [**портал Разработчик.**](https://dev.teams.microsoft.com/home)

1. Откройте **приложения** и выберите **импортное приложение**.

1. Имя вашего пакета **приложенийtab.zip.** Он доступен по следующему пути:

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Выберите **tab.zip** и откройте его на портале разработчиков.

1. По умолчанию **создается** и заполняется ID приложения по умолчанию в **разделе Основные сведения** .

1. Добавьте краткое и длинное описание для приложения в **Описания**.

1. В **сведениях разработчика** добавьте необходимые сведения, а на веб-сайте (должен быть допустимый **URL-адрес HTTPS)** укажи URL-адрес ngrok HTTPS.

1. В **URL-адресах** приложений обновите политику конфиденциальности `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` и сохраните ее.

1. В **функции Приложения** выберите **Личный appCreate** >  **первую личную** вкладку приложения и введите имя и обновите **URL-адрес** контента с `https://<yourngrokurl>/personalTab`помощью . Оставьте поле URL-адрес веб-сайта пустым и **выберите Context** в качестве personalTab из списка dropdown и **Добавить**.

1. Выберите **Сохранить**.

1. В разделе Домены домены с вкладок должны содержать URL-адрес ngrok без префикса `<yourngrokurl>.ngrok.io`HTTPS.

### <a name="preview-your-app-in-teams"></a>Просмотр приложения в Teams

1. Выберите **предварительный просмотр Teams** панели инструментов портала разработчика, портал разработчика сообщает вам, что приложение успешно загружено боком. Страница **Добавить** отображается для приложения в Teams.

1. Выберите **Добавить** для загрузки вкладки на Teams. Вкладка теперь доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="Личная вкладка" border="true":::
  
   Теперь вы создали и добавили личную вкладку в Teams.

   Поскольку ваша личная вкладка Teams, [](#reorder-static-personal-tabs) [`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps) вы также можете перенастроить и добавить API для личной вкладки.

::: zone-end

## <a name="reorder-static-personal-tabs"></a>Reorder static personal tabs

Начиная с манифеста версии 1.7, разработчики могут изменить все вкладки в своем личном приложении. В частности, разработчик может переместить вкладку  чата бота, которая всегда по умолчанию, в первую позицию, в любом месте в личном загонах вкладки приложения. Объявляются два зарезервированных `entityId` ключевых слова вкладки, **беседы** и **около**.

Если вы создаете бот с личной **областью** , он появляется на первой позиции вкладки в личном приложении по умолчанию. Если вы хотите переместить его в другую позицию, необходимо добавить в манифест статичный объект вкладки с зарезервированным ключевым словом **, беседами**. **Вкладка беседы** отображается на веб-сайте или на рабочем столе в зависимости от того, где вы добавляете вкладку **беседы** в массиве`staticTabs`.

``` JSON

{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}

```

## <a name="add-registeronfocused-api-for-tabs-or-personal-apps"></a>Добавление `registerOnFocused` API для вкладок или личных приложений

API `registerOnFocused` SDK позволяет использовать клавиатуру на Teams. Вы можете вернуться в личное приложение и сохранить фокус на вкладке или личном приложении с помощью ключей Ctrl, Shift и F6. Например, вы можете отойти от личного приложения для поиска чего-либо, а затем вернуться в личное приложение или использовать Ctrl+F6, чтобы обойти необходимые места.

В следующем коде приводится пример `registerFocusEnterHandler` определения обработчиков на SDK, когда фокус должен быть возвращен на вкладку или личное приложение:

``` C#

export function registerFocusEnterHandler(handler: (navigateForward: boolean) => void): 
void {
  HandlersPrivate.focusEnterHandler = handler;
  handler && sendMessageToParent('registerHandler', ['focusEnter']);
}
function handleFocusEnter(navigateForward: boolean): void
 {
  if (HandlersPrivate.focusEnterHandler)
   {
    HandlersPrivate.focusEnterHandler(navigateForward);
  }
}

```

После запуска обработка `focusEnter`с помощью ключевого слова обработник `registerFocusEnterHandler` `focusEnterHandler` вызывается с функцией вызова, которая принимает параметр под названием `navigateForward`. Значение определяет `navigateForward` тип событий. Вызывается `focusEnterHandler` только Ctrl+F6, а не клавиша вкладки.
Клавиши, полезные для перемещения событий в Teams, следуют следующим образом:

* Событие forward: клавиши Ctrl+F6
* Событие назад: клавиши Ctrl+Shift+F6

``` C#

case 'focusEnter':     
this.registerFocusEnterHandler((navigateForward: boolean = true) => {
this.sdkWindowMessageHandler.sendRequestMessage(this.frame, this.constants.SdkMessageTypes.focusEnter, [navigateForward]);
// Set focus on iframe or webview
if (this.frame && this.frame.sourceElem) {
  this.frame.sourceElem.focus();
}
return true;
});
}

// callback function to be passed to the handler
private focusEnterHandler: (navigateForward: boolean) => boolean;

// function that gets invoked after handler is registered.
private registerFocusEnterHandler(focusEnterHandler: (navigateForward: boolean) => boolean): void {
this.focusEnterHandler = focusEnterHandler;
this.layoutService.registerAppFocusEnterCallback(this.focusEnterHandler);
}

```

### <a name="personal-app"></a>Личное приложение

:::image type="content" source="../../assets/images/personal-apps/registerfocus.png" alt-text="В примере показаны варианты добавления API registerOnFocussed" border="true":::

#### <a name="personal-app-forward-event"></a>Личное приложение: событие Forward

:::image type="content" source="../../assets/images/personal-apps/registerfocus-forward-event.png" alt-text="В примере показаны варианты добавления переадновки API registerOnFocussed" border="true":::

#### <a name="personal-app-backward-event"></a>Личное приложение: событие назад

:::image type="content" source="../../assets/images/personal-apps/registerfocus-backward-event.png" alt-text="В примере показаны параметры добавления обратного перемещения registerOnFocussed API" border="true":::

### <a name="tab"></a>Tab

:::image type="content" source="../../assets/images/personal-apps/registerfocus-tab.png" alt-text="В примере показаны варианты добавления API registerOnFocussed для вкладки" border="true":::

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>См. также

* [Teams вкладки](~/tabs/what-are-tabs.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Создание вкладок бесед](~/tabs/how-to/conversational-tabs.md)
