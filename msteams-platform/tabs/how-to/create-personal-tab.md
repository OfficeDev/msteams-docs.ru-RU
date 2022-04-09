---
title: Создание личной вкладки
author: laujan
description: Краткое руководство по созданию личной вкладки с помощью генератора Yeoman, ASP.NET Core или ASP.NET Core MVC для Microsoft Teams с помощью Node.js и обновлению манифеста приложения.
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
keywords: yeoman ASP.NET appmanifest conversation domain appmanifest package MVC
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 40afdd1692b0f5d7c99eaaf228969ba8c95ba20b
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737216"
---
# <a name="create-a-personal-tab"></a>Создание личной вкладки

Личные вкладки, как и персональные боты, являются частью личных приложений и доступны только одному пользователю. Их можно закрепить на левой панели для простого доступа. Вы также можете [изменить порядок и](#reorder-static-personal-tabs) добавить [`registerOnFocused` API для](#add-registeronfocused-api-for-tabs-or-personal-apps) личных вкладок.

Убедитесь, что у [вас есть все](~/tabs/how-to/tab-requirements.md) предварительные требования для создания личной вкладки.

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>Создание личной вкладки с Node.js

1. В командной строке установите пакеты [Yeoman](https://yeoman.io/) и [gulp-cli](https://www.npmjs.com/package/gulp-cli) , введя следующую команду после установки Node.js:

    ```cmd
    npm install yo gulp-cli --global
    ```

1. В командной строке установите Microsoft Teams app, введя следующую команду:

    ```cmd
    npm install generator-teams --global
    ```

Ниже приведены шаги по созданию личной вкладки:

1. [Создание приложения с помощью личной вкладки](#generate-your-application-with-a-personal-tab)
1. [Добавление страницы содержимого на личную вкладку](#add-a-content-page-to-the-personal-tab)
1. [Создание пакета приложения](#create-your-app-package)
1. [Сборка и запуск приложения](#build-and-run-your-application)
1. [Установка безопасного туннеля на личную вкладку](#establish-a-secure-tunnel-to-your-tab)
1. [Upload приложения для Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Создание приложения с помощью личной вкладки

1. В командной строке создайте каталог для личной вкладки.

1. Введите следующую команду в новом каталоге, чтобы запустить Microsoft Teams App:

    ```cmd
    yo teams
    ```

1. Укажите значения для ряда вопросов, которые Microsoft Teams app generator для обновления `manifest.json` файла.

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="Teams генератора" border="true":::

    <details>
    <summary><b>Ряд вопросов по обновлению файла manifest.json</b></summary>

    * **Как называется решение?**

      Имя решения — это имя проекта. Чтобы принять предложенное имя, нажмите клавишу **ВВОД**.

    * **Где следует разместить файлы?**

      В настоящее время вы в каталоге проекта. Нажмите **клавишу ВВОД**.

    * **Название проекта Microsoft Teams приложения?**

      Заголовок — это имя пакета приложения, которое используется в манифесте и описании приложения. Введите заголовок или нажмите **клавишу ВВОД** , чтобы принять имя по умолчанию.

    * **Имя вашей компании? (не более 32 символов)**

      Название вашей компании будет использоваться в манифесте приложения. Введите название компании или нажмите **клавишу ВВОД** , чтобы принять имя по умолчанию.

    * **Какую версию манифеста вы хотите использовать?**

      Выберите схему по умолчанию.

    * **Быстрое формирование шаблонов? (Y/n)**

      Значение по умолчанию — yes; **Введите n** , чтобы ввести идентификатор партнера Майкрософт.

    * **Введите идентификатор партнера Майкрософт, если он у вас есть? (Оставьте пустым, чтобы пропустить)**

      Это поле не является обязательным и должно использоваться только в том случае, если вы уже являетесь частью [Microsoft Partner Network](https://partner.microsoft.com).

    * **Что вы хотите добавить в проект?**

      Выберите **( &ast; ) Вкладка**.

    * **URL-адрес, где будет размещено это решение?**

      По умолчанию генератор предлагает URL-адрес веб-сайтов Azure. Вы тестируете приложение только локально, поэтому допустимый URL-адрес не требуется.

    * **Хотите отобразить индикатор загрузки при загрузке приложения или вкладки?**

      Выберите **не** включать индикатор загрузки при загрузке приложения или вкладки. Значение по умолчанию — нет, введите **n**.

    * **Вы хотите, чтобы личные приложения отображались без строки заголовков вкладок?**

      Не **включайте** личные приложения для отрисовки без заголовка табуляции. Значение по умолчанию — нет, введите **n**.

    * **Включить платформу тестирования и начальные тесты? (y/N)**

      Выберите **не** включать тестовую платформу для этого проекта. Значение по умолчанию — нет, введите **n**.

    * **Включить поддержку ESLint? (y/N)**

      Не включайте поддержку ESLint. Значение по умолчанию — нет, введите **n**.

    * **Вы хотите использовать приложения Azure Аналитика для телеметрии? (y/N)**

      Не **включайте** [приложение Azure Аналитика](/azure/azure-monitor/app/app-insights-overview). Значение по умолчанию — нет; **введите n**.

    * **Имя вкладки по умолчанию (не более 16 символов)?**

      Приведите имя для вкладки. Это имя вкладки используется в проекте в качестве компонента пути к файлу или URL-адресу.

    * **Какую вкладку вы хотите создать?**

      Используйте клавиши со стрелками для выбора **личного (статического)**.

    * **Требуется ли Microsoft Azure Active Directory единого входа (Azure AD) для вкладки?**

      Не **включайте** поддержку единого входа Azure AD для вкладки. Значение по умолчанию — да, введите **n**.

    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>Добавление страницы содержимого на личную вкладку

Создайте страницу содержимого и обновите существующие файлы приложения личной вкладки:

1. Создайте новый **personal.html** в Visual Studio Code с помощью следующей разметки:

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

1. **Сохранитеpersonal.html** в общедоступной папке приложения  в следующем расположении:

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. Откройте `manifest.json` его в следующем расположении в Visual Studio Code:

    ```
     ./src/manifest/manifest.json
    ```

1. Добавьте следующий код в пустой массив `staticTabs` (`staticTabs":[]`) и добавьте следующий объект JSON:

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
    > Компонент пути **yourDefaultTabNameTab** — это значение, введенное в генераторе для имени  вкладки по умолчанию и слова **TAB**.
    >
    > Например: DefaultTabName — **MyTab** then **/MyTabTab/**

1. **Обновите компонент пути contentURL** **yourDefaultTabNameTab**, используя фактическое имя вкладки.

1. Сохраните обновленный `manifest.json` файл.

1. Откройте **tab.ts** в Visual Studio Code из следующего пути, чтобы предоставить страницу содержимого в IFrame:

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. Добавьте следующий код в список декораторов IFrame:

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. Сохраните обновленный файл. Код вкладки завершен.

### <a name="create-your-app-package"></a>Создание пакета приложения

У вас должен быть пакет приложения для сборки и запуска приложения в Teams. Пакет приложения создается с помощью задачи gulp, `manifest.json` которая проверяет файл и создает ZIP-папку в `./package` каталоге. В командной строке используйте команду `gulp manifest`.

### <a name="build-and-run-your-application"></a>Сборка и запуск приложения

#### <a name="build-your-application"></a>Создание приложения

Введите следующую команду в командной строке, чтобы транспилировать решение в папку **./dist** :

```cmd
gulp build
```

#### <a name="run-your-application"></a>Запуск приложения

1. В командной строке введите следующую команду, чтобы запустить локальный веб-сервер:

    ```cmd
    gulp serve
    ```

1. Введите `http://localhost:3007/<yourDefaultAppNameTab>/` данные в браузере, чтобы просмотреть домашнюю страницу приложения.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Вкладка по умолчанию" border="true":::

1. Перейдите `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`, чтобы просмотреть личную вкладку.

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="Вкладка HTML по умолчанию" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установка безопасного туннеля на вкладке

В командной строке выйдите из localhost и введите следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> После отправки в Microsoft Teams **ngrok** и успешного сохранения ее можно просмотреть в Teams до завершения сеанса туннеля.

### <a name="upload-your-application-to-teams"></a>Upload приложения для Teams

1. Перейдите Microsoft Teams и выберите **"**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Приложения Teams Store&quot;":::.
1. Выберите **"Управление приложениями****" и Upload настраиваемое приложение**.
1. Перейдите в каталог проекта, перейдите в папку **./package** , выберите ZIP-папку и нажмите кнопку **"Открыть"**.

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="Добавление личной вкладки" border="true":::

1. Выберите **"Добавить** " в диалоговом окне. Вкладка отправляется в Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="Отправлена личная вкладка" border="true":::

1. В левой области окна Teams нажмите многоточие &#x25CF;&#x25CF;&#x25CF; а затем выберите отправленное приложение, чтобы просмотреть личную вкладку.

   Теперь вы успешно создали и добавили личную вкладку в Teams.
  
   Так как у вас есть личная вкладка в Teams, вы также можете изменить [порядок](#reorder-static-personal-tabs) [`registerOnFocused` и добавить API](#add-registeronfocused-api-for-tabs-or-personal-apps) для личной вкладки.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>Создание личной вкладки с ASP.NET Core

1. В командной строке создайте каталог для проекта вкладки.

1. Клонируйте пример репозитория в новый каталог с помощью следующей команды или скачайте исходный [код и](https://github.com/OfficeDev/Microsoft-Teams-Samples) извлеките файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже приведены шаги по созданию личной вкладки:

1. [Создание приложения с помощью личной вкладки](#generate-your-application-with-a-personal-tab-1)
1. [Обновление и запуск приложения](#update-and-run-your-application)
1. [Установка безопасного туннеля на вкладке](#establish-a-secure-tunnel-to-your-tab-1)
1. [Обновление пакета приложения с помощью портала разработчика](#update-your-app-package-with-developer-portal)
1. [Предварительный просмотр приложения в Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Создание приложения с помощью личной вкладки

1. Откройте Visual Studio и выберите **"Открыть проект или решение"**.

1. Перейдите в папку Microsoft-Teams-Samplessamplestab-personalrazor-csharp  >  >  >  и откройте **файл PersonalTab.sln**.

1. В Visual Studio нажмите **клавишу F5** или выберите команду **"** Начать отладку" в меню отладки  приложения, чтобы убедиться, что приложение загружено правильно. В браузере перейдите по следующим URL-адресам:

    * <http://localhost:3978/>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Просмотр исходного кода</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан на основе пустого шаблона ASP.NET Core 3.1 с флажком "Дополнительно — настройка **HTTPS**", выбранным при установке. Службы MVC регистрируются с помощью метода платформы внедрения зависимостей `ConfigureServices()` . Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, `Configure()` поэтому ПО промежуточного слоя статических файлов добавляется в метод с помощью следующего кода:

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

#### <a name="wwwroot-folder"></a>Папка wwwroot

В ASP.NET Core корневой папке веб-сайта приложение ищет статические файлы.

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core обрабатывает файлы с именем **Index** как домашнюю страницу сайта по умолчанию. Если URL-адрес браузера указывает на корень сайта, **index.cshtml** отображается как домашняя страница приложения.

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакетов приложений:

* Значок полного цвета, размером 192 x 192 пикселя.
* Значок прозрачной структуры размером 32 x 32 пикселя.
* Файл `manifest.json` , указывающий атрибуты приложения.

Эти файлы должны быть сжаты в пакете приложения для использования при отправке вкладки в Teams. Microsoft Teams загружает `contentUrl` указанный в манифесте, внедряет его в <iframe\> и отображает на вкладке.

#### <a name="csproj"></a>CSPROJ

В Visual Studio Обозреватель решений щелкните проект правой кнопкой мыши и выберите команду "Изменить **Project файл"**. В конце файла вы увидите следующий код, который создает и обновляет ZIP-папку при сборке приложения:

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

1. Откройте Visual Studio Обозреватель решений и перейдите в папку **PagesShared** > , откройте **_Layout.cshtml** `<head>` и добавьте в раздел тегов следующее:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. В Visual Studio Обозреватель решений **файле PersonalTab.cshtml** из папки **Pages**, `microsoftTeams.initialize()` `<script>` добавьте теги и сохраните их.

1. В Visual Studio нажмите **клавишу F5** или выберите **команду "** Начать отладку" в меню "**Отладка" приложения**.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установка безопасного туннеля на вкладке

В командной строке в корне каталога проекта выполните следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Обновление пакета приложения с помощью портала разработчика

1. Перейдите на [**портал разработчика**](https://dev.teams.microsoft.com/home).

1. Откройте **"Приложения** " и выберите **"Импорт приложения"**.

1. Имя файла пакета приложения есть `tab.zip` и доступно по пути `/bin/Debug/netcoreapp3.1/tab.zip` .

1. Выберите `tab.zip` и откройте его на портале разработчика.

1. Идентификатор приложения **по умолчанию создается** и заполняется в разделе " **Основные сведения** ".

1. Добавьте краткое и длинное описание приложения в **описание**.

1. В **разделе "Сведения** о разработчике" добавьте необходимые сведения, а на веб-сайте (должен быть допустимым **URL-адресом HTTPS)** укажите URL-адрес HTTPS ngrok.

1. В **URL-адресах приложений** обновите политику конфиденциальности `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` и сохраните условия использования.

1. В **разделе "Функции приложения**" выберите **"Личный appCreate** >  **your first personal app tab**" (Создать первую личную вкладку приложения), введите имя и обновите **URL-адрес** содержимого`https://<yourngrokurl>/personalTab`. Оставьте поле URL-адреса веб-сайта пустым и выберите **"Контекст** как personalTab" в раскрывающемся списке и " **Добавить"**.

1. Выберите **Сохранить**.

1. В разделе "Домены" домены с вкладок должны содержать URL-адрес ngrok без префикса HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Предварительный просмотр приложения в Teams

1. Выберите **предварительный просмотр Teams** на панели инструментов портала разработчика. Портал разработчика информирует вас об успешной загрузке неопубликованного приложения. Страница **"Добавить**" появится для вашего приложения в Teams.

1. Нажмите **кнопку "** Добавить", чтобы загрузить вкладку в Teams. Вкладка теперь доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="Вкладка по умолчанию" border="true":::

   Теперь вы успешно создали и добавили личную вкладку в Teams.
  
   Так как у вас есть личная вкладка в Teams, вы также можете изменить [порядок](#reorder-static-personal-tabs) [`registerOnFocused` и добавить API](#add-registeronfocused-api-for-tabs-or-personal-apps) для личной вкладки.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>Создание личной вкладки с ASP.NET Core MVC

1. В командной строке создайте каталог для проекта вкладки.

1. Клонируйте пример репозитория в новый каталог с помощью следующей команды или скачайте исходный [код и](https://github.com/OfficeDev/Microsoft-Teams-Samples) извлеките файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже приведены шаги по созданию личной вкладки:

1. [Создание приложения с помощью личной вкладки](#generate-your-application-with-a-personal-tab-2)
1. [Обновление и запуск приложения](#update-and-run-your-application-1)
1. [Установка безопасного туннеля на вкладке](#establish-a-secure-tunnel-to-your-tab-2)
1. [Обновление пакета приложения с помощью портала разработчика](#update-your-app-package-with-developer-portal-1)
1. [Предварительный просмотр приложения в Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>Создание приложения с помощью личной вкладки

1. Откройте Visual Studio и выберите **"Открыть проект или решение"**.

1. Перейдите в папку Microsoft-Teams-Samplessamplestab-personalmvc-csharp  >  >  >  и откройте **файл PersonalTabMVC.sln** в Visual Studio.

1. В Visual Studio нажмите **клавишу F5** или выберите команду **"** Начать отладку" в меню отладки  приложения, чтобы убедиться, что приложение загружено правильно. В браузере перейдите по следующим URL-адресам:

    * <http://localhost:3978>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Просмотр исходного кода</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан на основе пустого шаблона ASP.NET Core 3.1 с флажком "Дополнительно — настройка **HTTPS**", выбранным при установке. Службы MVC регистрируются с помощью метода платформы внедрения зависимостей `ConfigureServices()` . Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, `Configure()` поэтому ПО промежуточного слоя статических файлов добавляется в метод с помощью следующего кода:

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

#### <a name="wwwroot-folder"></a>Папка wwwroot

В ASP.NET Core корневой папке веб-сайта приложение ищет статические файлы.

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакетов приложений:

* **Значок полного цвета**, размером 192 x 192 пикселя.
* **Значок прозрачной структуры** размером 32 x 32 пикселя.
* Файл `manifest.json` , указывающий атрибуты приложения.

Эти файлы должны быть сжаты в пакете приложения для использования при отправке вкладки в Teams. Microsoft Teams загружает `contentUrl` указанный манифест, внедряет его в IFrame и отображает на вкладке.

#### <a name="csproj"></a>CSPROJ

В Visual Studio Обозреватель решений щелкните проект правой кнопкой мыши и выберите команду **"Изменить Project файл"**. В конце файла вы увидите следующий код, который создает и обновляет ZIP-папку при сборке приложения:

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

**PersonalTab.cs** представляет объект сообщения и методы, вызываемые из **PersonalTabController** , когда пользователь нажмет кнопку в представлении **PersonalTab** .

#### <a name="views"></a>Представления

Эти представления являются различными представлениями в ASP.NET Core MVC:

* Главная: ASP.NET Core обрабатывает файлы с именем **Index** как домашнюю страницу сайта или по умолчанию. Если URL-адрес браузера указывает на корень сайта, **index.cshtml** отображается как домашняя страница приложения.

* Общий доступ. Частичная разметка **представления _Layout.cshtml** содержит общую структуру страницы приложения и общие визуальные элементы. Он также ссылается на Teams библиотеку.

#### <a name="controllers"></a>Контроллеры

Контроллеры используют это свойство `ViewBag` для динамической передачи значений в представления.

</details>

### <a name="update-and-run-your-application"></a>Обновление и запуск приложения

1. Откройте Visual Studio Обозреватель решений и перейдите в папку **ViewsShared** > , **откройте _Layout.cshtml** и `<head>` добавьте в раздел тегов следующее:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. В Visual Studio Обозреватель решений **файле PersonalTab.cshtml** из папки **ViewsPersonalTab** `microsoftTeams.initialize()`  > `<script>`, добавьте в теги и сохраните их.

1. В Visual Studio нажмите **клавишу F5** или выберите **команду "** Начать отладку" в меню "**Отладка" приложения**.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установка безопасного туннеля на вкладке

В командной строке в корне каталога проекта выполните следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Обновление пакета приложения с помощью портала разработчика

1. Перейдите на [**портал разработчика**](https://dev.teams.microsoft.com/home).

1. Откройте **"Приложения** " и выберите **"Импорт приложения"**.

1. Имя пакета приложения **—tab.zip.** Он доступен по следующему пути:

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Выберите **tab.zip** и откройте его на портале разработчика.

1. Идентификатор приложения **по умолчанию создается** и заполняется в разделе " **Основные сведения** ".

1. Добавьте краткое и длинное описание приложения в **описание**.

1. В **разделе "Сведения** о разработчике" добавьте необходимые сведения, а на веб-сайте (должен быть допустимым **URL-адресом HTTPS)** укажите URL-адрес HTTPS ngrok.

1. В **URL-адресах приложений** обновите политику конфиденциальности `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` и сохраните условия использования.

1. В **разделе "Функции приложения**" выберите **"Личный appCreate** >  **your first personal app tab**" (Создать первую личную вкладку приложения), введите имя и обновите **URL-адрес** содержимого`https://<yourngrokurl>/personalTab`. Оставьте поле URL-адреса веб-сайта пустым и выберите **"Контекст** как personalTab" в раскрывающемся списке и " **Добавить"**.

1. Выберите **Сохранить**.

1. В разделе "Домены" домены с вкладок должны содержать URL-адрес ngrok без префикса HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Предварительный просмотр приложения в Teams

1. Выберите **предварительный просмотр Teams** на панели инструментов портала разработчика. Портал разработчика информирует вас об успешной загрузке неопубликованного приложения. Страница **"Добавить**" появится для вашего приложения в Teams.

1. Нажмите **кнопку "** Добавить", чтобы загрузить вкладку на Teams. Вкладка теперь доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="Личная вкладка" border="true":::
  
   Теперь вы успешно создали и добавили личную вкладку в Teams.

   Так как у вас есть личная вкладка в Teams, вы также можете изменить [порядок](#reorder-static-personal-tabs) [`registerOnFocused` и добавить API](#add-registeronfocused-api-for-tabs-or-personal-apps) для личной вкладки.

::: zone-end

## <a name="reorder-static-personal-tabs"></a>Изменение порядка статических личных вкладок

Начиная с версии манифеста 1.7 разработчики могут переупорядочить все вкладки в своем личном приложении. В частности, разработчик может переместить вкладку  чата бота, которая всегда используется по умолчанию, в первую позицию в любом месте заголовка вкладки личного приложения. Объявляются два зарезервированных `entityId` ключевых слова табуляции: **беседы и** **о программе**.

При создании бота с личной областью он по умолчанию отображается в первой позиции вкладки в личном приложении. Если вы хотите переместить его в другую позицию, необходимо добавить в манифест статический объект табуляции с зарезервированным ключевым словом **"беседы"**. **Вкладка беседы** отображается в Интернете или на рабочем столе в зависимости от того, куда вы добавляете вкладку беседы в массиве`staticTabs`.

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

API `registerOnFocused` пакета SDK позволяет использовать клавиатуру на Teams. Вы можете вернуться к личному приложению и сосредоточиться на вкладке или личном приложении с помощью клавиш CTRL, SHIFT и F6. Например, вы можете перейти от личного приложения к поиску, а затем вернуться к личному приложению или использовать клавиши CTRL+F6, чтобы обойти необходимые места.

В следующем коде приведен пример `registerFocusEnterHandler` определения обработчика в пакете SDK, когда фокус должен быть возвращен на вкладку или личное приложение:

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

После активации обработчика `focusEnter`с ключевым словом обработчик `registerFocusEnterHandler` `focusEnterHandler` вызывается с помощью функции обратного вызова, которая принимает параметр с именем `navigateForward`. Значение определяет `navigateForward` тип событий. Вызывается `focusEnterHandler` только сочетанием клавиш CTRL+F6, а не клавишей TAB.
Ниже приведены ключи, полезные для событий Teams перемещения.

* Событие пересылки: клавиши CTRL+F6
* Событие назад: клавиши CTRL+SHIFT+F6

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

:::image type="content" source="../../assets/images/personal-apps/registerfocus.png" alt-text="В примере показаны параметры для добавления API registerOnFocussed" border="true":::

#### <a name="personal-app-forward-event"></a>Личное приложение: событие пересылки

:::image type="content" source="../../assets/images/personal-apps/registerfocus-forward-event.png" alt-text="В примере показаны параметры для добавления перемещения вперед в API registerOnFocussed" border="true":::

#### <a name="personal-app-backward-event"></a>Личное приложение: событие назад

:::image type="content" source="../../assets/images/personal-apps/registerfocus-backward-event.png" alt-text="В примере показаны параметры для добавления registerOnFocussed API обратного перемещения" border="true":::

### <a name="tab"></a>Tab

:::image type="content" source="../../assets/images/personal-apps/registerfocus-tab.png" alt-text="В примере показаны параметры добавления registerOnFocussed API для tab" border="true":::

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>См. также

* [Teams вкладок](~/tabs/what-are-tabs.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Создание вкладок бесед](~/tabs/how-to/conversational-tabs.md)
* [Поделиться в Teams из личного приложения или вкладки](~/concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md)
