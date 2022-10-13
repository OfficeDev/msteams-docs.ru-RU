---
title: Создание личной вкладки
author: laujan
description: Узнайте, как создать личную вкладку. Выберите Node.js, ASP.NET Core или ASP.NET Core MVC. Создание приложения, добавление содержимого, создание пакета, сборка и запуск приложения.
ms.localizationpriority: high
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 187f1b40c60d8f7d88b75e6f666239ab70717cf6
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560738"
---
# <a name="create-a-personal-tab"></a>Создание личной вкладки

Личные вкладки, как и персональные боты, являются частью личных приложений и доступны только одному пользователю. Их можно закрепить на левой панели для быстрого доступа. Вы также можете [изменить порядок](#reorder-static-personal-tabs) личных вкладок.

Убедитесь, что у вас есть все [необходимые условия](~/tabs/how-to/tab-requirements.md) для создания личной вкладки.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>Создание личной вкладки с помощью Node.js

1. В командной строке установите пакеты[Yeoman](https://yeoman.io/) и [gulp-cli](https://www.npmjs.com/package/gulp-cli), введя следующую команду после установки Node.js:

    ```cmd
    npm install yo gulp-cli --global
    ```

1. В командной строке установите генератор приложений Microsoft Teams, введя следующую команду:

    ```cmd
    npm install generator-teams --global
    ```

Ниже приведены этапы создания личной вкладки:

1. [Создайте свое приложение с личной вкладкой](#generate-your-application-with-a-personal-tab)
1. [Добавьте страницу содержимого на личную вкладку](#add-a-content-page-to-the-personal-tab)
1. [Создание пакета приложения](#create-your-app-package)
1. [Создайте и запустите свое приложение](#build-and-run-your-application)
1. [Установите безопасный туннель к вашей личной вкладке](#establish-a-secure-tunnel-to-your-tab)
1. [Загрузите приложение в Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Создание приложения с личной вкладкой

1. В командной строке создайте новый каталог для личной вкладки.

1. Введите следующую команду в новом каталоге, чтобы запустить генератор приложений Microsoft Teams:

    ```cmd
    yo teams
    ```

1. Укажите свои значения в ряде вопросов, запрашиваемых генератором приложений Microsoft Teams для обновления `manifest.json` файла.

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="Генератор Teams":::

    <details>
    <summary><b>Серия вопросов для обновления файла manifest.json</b></summary>

    * **Как называется решение?**

      Имя решения — это имя проекта. Вы можете принять предложенное имя, нажав **ВВОД**.

    * **Где следует разместить файлы?**

      Сейчас вы находитесь в каталоге проекта. Выберите **ВВОД**.

    * **Название вашего проекта приложения Microsoft Teams?**

      Название — это имя пакета приложения, которое используется в манифесте и описании приложения. Введите название или выберите **ВВОД** чтобы принять имя по умолчанию.

    * **Имя (компании)? (не более 32 символов)**

      Название вашей компании будет использоваться в манифесте приложения. Введите название компании или выберите **ВВОД** чтобы принять имя по умолчанию.

    * **Какую версию манифеста вы хотите использовать?**

      Выберите схему по умолчанию.

    * **Быстрое формирование шаблонов (Y или N)**

      Значение по умолчанию — "да". Введите **n**, чтобы указать свой идентификатор партнера Microsoft.

    * **Введите идентификатор партнера Microsoft, если он у вас есть? (Оставьте пустым, чтобы пропустить)**

      Это поле не является обязательным и заполняется только в том случае, если вы уже являетесь участником [Microsoft Partner Network](https://partner.microsoft.com).

    * **Что вы хотите добавить в проект?**

      Выберите **( &ast; ) Вкладка**.

    * **URL-адрес, по которому вы будете размещать это решение?**

      По умолчанию генератор предлагает URL-адрес веб-сайта Azure. Вы тестируете свое приложение только локально, поэтому действительный URL-адрес не требуется.

    * **Хотели бы вы показывать индикатор загрузки при загрузке приложения или вкладки?**

      Выберите **нет**, чтобы включить индикатор загрузки приложения или вкладки. Значение по умолчанию — "нет". Введите **n**.

    * **Вы хотите, чтобы личные приложения отображались без строки заголовков вкладок?**

      Выберите **нет**, чтобы включить личные приложения, которые будут отображаться без панели заголовка вкладки. По умолчанию — нет. Введите **n**.

    * **Хотели бы вы включить тестовую среду и начальные тесты? (Y или N)**

      Выберите **нет**, чтобы включить тестовую среду для этого проекта. Значение по умолчанию — "нет". Введите **n**.

    * **Хотите включить поддержку ESLint? (Y или N)**

      Выберите нет, чтобы включить поддержку ESLint. Значение по умолчанию — "нет". Введите **n**.

    * **Хотите использовать Azure Applications Insights для телеметрии? (Y или N)**

      Выберите **нет** чтобы включить [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview). Значение по умолчанию — "нет". Введите **n**.

    * **Имя вкладки по умолчанию (не более 16 символов)?**

      Назовите свою вкладку. Это имя вкладки используется в вашем проекте как компонент пути к файлу или URL-адресу.

    * **Какую вкладку вы хотели бы создать?**

      С помощью клавиш со стрелками выберите **Личная (статическая)**.

    * **Требуется ли вам поддержка единого входа Microsoft Azure Active Directory (Azure AD) для вкладки?**

      Выберите **нет**, чтобы включить поддержку единого входа Azure AD для вкладки. Значение по умолчанию — "да", введите **n**.
    > [!NOTE]
    > На вкладке домашняя страница вкладки отображается только в том случае, если пользователь нажмет кнопку "Назад" (или переместится с вкладки) и вернитесь на домашнюю страницу. По умолчанию вкладка не поддерживает и не сохраняет предыдущее состояние.
    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>Добавьте страницу содержимое на личную вкладку

Создайте страницу содержимого и обновите существующие файлы приложения личной вкладки:

1. Создайте новый файл **personal.html** в Visual Studio Code со следующей разметкой:

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

1. Сохраните **personal.html** в **общедоступной** папке вашего приложения по следующему адресу:

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. Откройте `manifest.json` из следующего места в Visual Studio Code:

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
    > Компонент пути **yourDefaultTabNameTab**— это значение, которое вы ввели в генератор для **Имени вкладки по умолчанию** а также слово **Вкладка**.
    >
    > Например: DefaultTabName — **MyTab** а затем **/MyTabTab/**

1. Обновите компонент пути **contentURL** **yourDefaultTabNameTab**, указав фактическое имя вкладки.

1. Сохраните обновленный файл `manifest.json`.

1. Откройте **tab.ts** в Visual Studio Code из следующего пути, чтобы предоставить страницу содержимого в iFrame:

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. Добавьте следующий код в список декораторов iFrame:

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. Сохраните обновленный файл. Код вкладки завершен.

### <a name="create-your-app-package"></a>Создание пакета приложения

У вас должен быть пакет приложения для создания и запуска приложения в Teams. Пакет приложения создается с помощью задачи gulp, которая проверяет файл `manifest.json` и создает zip-папку в каталоге `./package`. В командной строке используйте команду `gulp manifest`.

### <a name="build-and-run-your-application"></a>Создайте и запустите приложение

#### <a name="build-your-application"></a>Создание приложения

Введите следующую команду в командной строке, чтобы перенести решение в./dist **папку**:

```cmd
gulp build
```

#### <a name="run-your-application"></a>Запустите приложение

1. В командной строке введите следующую команду, чтобы запустить локальный веб-сервер:

    ```cmd
    gulp serve
    ```

1. В браузере ведите `http://localhost:3007/<yourDefaultAppNameTab>/` для просмотра домашней страницы приложения.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Вкладка по умолчанию":::

1. Просмотрите `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`, чтобы найти личную вкладку.

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="Вкладка HTML по умолчанию":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установите безопасный туннель к вашей вкладке

В командной строке выйдите из локального хоста и введите следующую команду, чтобы установить безопасный туннель для вашей вкладки:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> После того, как ваша вкладка загружена в Microsoft Teams через **ngrok** и успешно сохранена, вы можете просматривать ее в Teams до завершения сеанса туннеля.

### <a name="upload-your-application-to-teams"></a>Загрузите свое приложение в Teams

1. Перейдите в Teams и выберите **Приложения**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::.
1. Выберите **"Управление приложениями** > **" "Отправить приложение"** > **"Отправить пользовательское приложение"**.
1. Перейдите в каталог проекта, в папку **./package** выберите папку zip и нажмите **Открыть**.

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="Добавление личной вкладки":::

1. В диалоговом окне выберите **Добавить**. Вкладка загружена в Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="Личная вкладка загружена":::

1. На левой панели Teams выберите многоточие &#x25CF;&#x25CF;&#x25CF; а затем выберите загруженное приложение, чтобы просмотреть личную вкладку.

   Теперь вы успешно создали и добавили личную вкладку в Teams.
  
   Теперь, когда у вас есть личная вкладка в Teams, вы можете [переупорядочить ](#reorder-static-personal-tabs) личную вкладку.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>Создайте личную вкладку с помощью ASP.NET Core

1. В командной строке создайте новый каталог для вашего проекта вкладок.

1. Клонируйте образец репозитория в новый каталог, используя следующую команду, или загрузите [исходный код](https://github.com/OfficeDev/Microsoft-Teams-Samples) и извлеките файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже приведены этапы создания личной вкладки:

1. [Создайте свое приложение с личной вкладкой](#generate-your-application-with-a-personal-tab-1)
1. [Обновите и запустите приложение](#update-and-run-your-application)
1. [Установите безопасный туннель к вкладке](#establish-a-secure-tunnel-to-your-tab-1)
1. [Обновите пакет приложения с помощью портала разработчика](#update-your-app-package-with-developer-portal)
1. [Просмотрите приложение в Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Создание приложения с личной вкладкой

1. Откройте Visual Studio и выберите **Открыть проект или решение**.

1. Перейдите в папку **Microsoft-Teams-Samples** > **samples** > **tab-personal** > **razor-csharp** и откройте **PersonalTab.sln**

1. В Visual Studio выберите **F5** или **Начать отладку** в меню **Отладка** вашего приложения, чтобы проверить, правильно ли загружено приложение. В браузере перейдите по следующим URL-адресам:

    * `<http://localhost:3978/>`
    * `<http://localhost:3978/personalTab>`
    * `<http://localhost:3978/privacy>`
    * `<http://localhost:3978/tou>`

<details>
<summary><b>Просмотреть исходный код</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан на основе пустого шаблона веб-приложения ASP.NET Core 3.1 с установленным флажком **Дополнительно — настроить для HTTPS** при установке. Службы MVC регистрируются с помощью метода `ConfigureServices()` инфраструктуры внедрения зависимостей Кроме того, пустой шаблон по умолчанию не позволяет обслуживать статическое содержимое, поэтому промежуточное ПО для статических файлов добавляется в метод `Configure()` с помощью следующего кода:

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

В ASP.NET Core корневая веб-папка — это место, где приложение ищет статические файлы.

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core рассматривает файлы с именем **Index** как стандартную или домашнюю страницу сайта. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** отображается как домашняя страница вашего приложения.

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложения:

* Полноцветный значок размером 192 x 192 пикселя.
* Прозрачный контурный значок размером 32 x 32 пикселя.
* Файл `manifest.json`, определяющий атрибуты приложения.

Эти файлы должны быть заархивированы в пакете приложения для использования при загрузке вкладки в Teams. Teams загружает `contentUrl`указанные в манифесте, встраивает их в <iframe\> и отображает на вкладке.

#### <a name="csproj"></a>.csproj

В обозревателе решений Visual Studio щелкните правой кнопкой мыши проект и выберите **Изменить файл проекта**. В конце файла вы можете увидеть следующий код, который создает и обновляет zip-папку при сборке приложения:

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

### <a name="update-and-run-your-application"></a>Обновите и запустите приложение

1. Откройте обозреватель решений Visual Studio, перейдите в папку **Страницы** > **Общие**, откройте **_Layout.cshtml** и добавьте следующее в раздел тегов `<head>`:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js" integrity="sha384-QtTBFeFlfRDZBfwHJHYQp7MdLJ2C3sfAEB1Qpy+YblvjavBye+q87TELpTnvlXw4" crossorigin="anonymous"></script>
    ```

1. В Visual Studio Обозреватель решений **откройте файл PersonalTab.cshtml** из папки **Pages** `microsoftTeams.app.initialize()` `<script>` и добавьте теги.

1. Нажмите кнопку **Сохранить**.

1. В Visual Studio выберите **F5** или выберите **Начать отладку** из меню **Отладка** вашего приложения.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установите безопасный туннель к вашей вкладке

В командной строке в корне каталога проекта выполните следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Обновите пакет приложения с помощью портала разработчика

1. Перейдите на [**Портал разработчика**](https://dev.teams.microsoft.com/home).

1. Откройте **Приложения** и выберите **Импорт приложений**.

1. Имя файла пакета приложения есть `tab.zip` и доступно по пути `/bin/Debug/netcoreapp3.1/tab.zip` .

1. Выберите `tab.zip` и откройте его на портале разработчика.

1. По умолчанию **Идентификатор приложения** создается и заполняется в разделе **Основная информация**.

1. Добавьте краткое и подробное описание для своего приложения в **Описания**.

1. В разделе **Информация для разработчиков** добавьте необходимые данные, а в разделе **Веб-сайт (это должен быть действительный URL-адрес HTTPS)** укажите URL-адрес HTTPS ngrok.

1. В **URL-адресах приложений** обновите политику конфиденциальности `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` и установите флажок "Сохранить **".**

1. В **разделе "Функции приложения**" выберите "**Личное** >  приложение **" "Создать первую личную** вкладку приложения", введите имя и **обновите URL-адрес** содержимого`https://<yourngrokurl>/personalTab`. Оставьте поле URL-адреса веб-сайта пустым, выберите **"Контекст** как personalTab" в раскрывающемся списке и нажмите кнопку **"Подтвердить"**.

1. Нажмите кнопку **Сохранить**.

1. В разделе "Домены" домены из ваших вкладок должны содержать ваш URL-адрес ngrok без префикса HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Предварительный просмотр приложения в Teams

1. Выберите **Предварительный просмотр в Teams** на панели инструментов портала разработчика. Портал разработчика сообщит вам, что ваше приложение успешно загружено. **Страница добавления** отображается для вашего приложения в Teams.

1. Выберите **Добавить** чтобы загрузить вкладку в Teams. Теперь вкладка доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="Вкладка по умолчанию":::

   Теперь вы успешно создали и добавили личную вкладку в Teams.
  
   Теперь, когда у вас есть личная вкладка в Teams, вы можете [переупорядочить ](#reorder-static-personal-tabs) личную вкладку.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>Создайте личную вкладку с помощью ASP.NET Core MVC

1. В командной строке создайте новый каталог для вашего проекта вкладок.

1. Клонируйте образец репозитория в новый каталог, используя следующую команду, или загрузите [исходный код](https://github.com/OfficeDev/Microsoft-Teams-Samples) и извлеките файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже приведены этапы создания личной вкладки:

1. [Создайте свое приложение с личной вкладкой](#generate-your-application-with-a-personal-tab-2)
1. [Обновите и запустите приложение](#update-and-run-your-application-1)
1. [Установите безопасный туннель к вашей вкладке](#establish-a-secure-tunnel-to-your-tab-2)
1. [Обновите пакет приложения с помощью портала разработчика](#update-your-app-package-with-developer-portal-1)
1. [Просмотрите приложение в Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>Создание приложения с личной вкладкой

1. Откройте Visual Studio и выберите **Открыть проект или решение**.

1. Перейдите на вкладку **Microsoft-Teams-Samples** > **samples** > **tab-personal** > **mvc-csharp** и откройте **PersonalTabMVC.sln** в Visual Studio.

1. В Visual Studio выберите **F5** или **Начать отладку** в меню **Отладка** вашего приложения, чтобы проверить, правильно ли загружено приложение. В браузере перейдите по следующим URL-адресам:

    * `<http://localhost:3978>`
    * `<http://localhost:3978/personalTab>`
    * `<http://localhost:3978/privacy>`
    * `<http://localhost:3978/tou>`

<details>
<summary><b>Просмотреть исходный код</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан на основе пустого шаблона веб-приложения ASP.NET Core 3.1 с установленным флажком **Дополнительно — настроить для HTTPS** при установке. Службы MVC регистрируются с помощью метода `ConfigureServices()` инфраструктуры внедрения зависимостей Кроме того, пустой шаблон по умолчанию не позволяет обслуживать статическое содержимое, поэтому промежуточное ПО для статических файлов добавляется в метод `Configure()` с помощью следующего кода:

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

В ASP.NET Core корневая веб-папка — это место, где приложение ищет статические файлы.

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложения:

* **Полноцветный значок** размером 192 x 192 пикселя.
* **Прозрачный контурный значок** размером 32 x 32 пикселя.
* Файл `manifest.json`, определяющий атрибуты приложения.

Эти файлы должны быть заархивированы в пакете приложения для использования при загрузке вкладки в Teams. Teams загружает указанные `contentUrl` в манифесте данные, внедряет их в iFrame и отображает на вкладке.

#### <a name="csproj"></a>.csproj

В обозревателе решений Visual Studio щелкните правой кнопкой мыши проект и выберите **Редактировать файл проекта**. В конце файла вы видите следующий код, который создает и обновляет вашу zip-папку при сборке приложения:

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

**PersonalTab.cs** представляет объект сообщения и методы, которые вызываются из **PersonalTabController**, когда пользователь выбирает кнопку в представлении **PersonalTab** View.

#### <a name="views"></a>Представления

Это различные представления в ASP.NET Core MVC:

* Домашняя страница: ASP.NET Core рассматривает файлы с именем **Index** как домашнюю страницу сайта по умолчанию. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** отображается как домашняя страница вашего приложения.

* Общие: разметка частичного представления **_Layout.cshtml** содержит общую структуру страницы приложения и общие визуальные элементы. Он также ссылается на библиотеку Teams.

#### <a name="controllers"></a>Контроллеры

Контроллеры используют свойство `ViewBag` для динамической передачи значений представлениям.

</details>

### <a name="update-and-run-your-application"></a>Обновите и запустите приложение

1. Откройте обозреватель решений Visual Studio, перейдите в папку **Представления** > **Общие**, откройте **_Layout.cshtml** и добавьте следующее в раздел тегов `<head>`:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js" integrity="sha384-QtTBFeFlfRDZBfwHJHYQp7MdLJ2C3sfAEB1Qpy+YblvjavBye+q87TELpTnvlXw4" crossorigin="anonymous"></script>
    ```

1. В Visual Studio Обозреватель решений **откройте файл PersonalTab.cshtml** из папки **Views** > **PersonalTab** `microsoftTeams.app.initialize()` и добавьте их в `<script>` теги.

1. Нажмите кнопку **Сохранить**.

1. В Visual Studio выберите **F5** или выберите **Начать отладку** из меню **Отладка** вашего приложения.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установите безопасный туннель к вашей вкладке

В командной строке в корне каталога проекта выполните следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Обновите пакет приложения с помощью портала разработчика

1. Перейдите на [**Портал разработчика**](https://dev.teams.microsoft.com/home).

1. Откройте **Приложения** и выберите **Импорт приложений**.

1. Имя пакета приложения — **tab.zip**. Он доступен по следующему пути:

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Выберите **tab.zip** и откройте его на портале разработчиков.

1. По умолчанию **Идентификатор приложения** создается и заполняется в разделе **Основная информация**.

1. Добавьте краткое и подробное описание для своего приложения в **Описания**.

1. В **сведениях разработчика** добавьте необходимые сведения и на веб-сайте (должен быть допустимым **URL-адресом HTTPS)** укажите URL-адрес HTTPS ngrok.

1. В **URL-адресах приложений** обновите политику конфиденциальности `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` и установите флажок "Сохранить **".**

1. В **разделе "Функции приложения**" выберите "**Личное** >  приложение **" "Создать первую личную** вкладку приложения", введите имя и **обновите URL-адрес** содержимого`https://<yourngrokurl>/personalTab`. Оставьте поле URL-адреса веб-сайта пустым, выберите **"Контекст** как personalTab" в раскрывающемся списке и нажмите кнопку **"Подтвердить"**.

1. Нажмите кнопку **Сохранить**.

1. В разделе "Домены" домены из ваших вкладок должны содержать ваш URL-адрес ngrok без префикса HTTPS`<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Предварительный просмотр приложения в Teams

1. Выберите **Предварительный просмотр в Teams** на панели инструментов портала разработчика. Портал разработчика сообщит вам, что ваше приложение успешно загружено. **Страница добавления** отображается для вашего приложения в Teams.

1. Выберите **Добавить** чтобы загрузить вкладку в Teams. Теперь вкладка доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="Личная вкладка":::
  
   Теперь вы успешно создали и добавили личную вкладку в Teams.

   Теперь, когда у вас есть личная вкладка в Teams, вы можете [переупорядочить ](#reorder-static-personal-tabs) личную вкладку.

::: zone-end

## <a name="reorder-static-personal-tabs"></a>Изменение порядка статических личных вкладок

Начиная с версии манифеста 1.7, разработчики могут переупорядочивать все вкладки в своем личном приложении. Вы можете переместить вкладку **чата** бота, которая всегда используется по умолчанию, в первую позицию в любом месте заголовка вкладки личного приложения. Объявлены два зарезервированных `entityId` ключевых слова вкладки, **беседы** и **сведения**.

Если вы создаете бота с **личной** областью действия, он по умолчанию отображается на первой вкладке в личном приложении. Если вы хотите переместить его в другое место, вы должны добавить объект статической вкладки в свой манифест с зарезервированным ключевым словом **беседы**. Вкладка **беседа** отображается в Интернете или на настольном компьютере в зависимости от того, где вы добавляете вкладку **беседа** в массиве `staticTabs`.

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

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Создание вкладок бесед](~/tabs/how-to/conversational-tabs.md)
* [Поделиться в Teams из личного приложения или вкладки](~/concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md)
