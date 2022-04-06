---
title: Создание вкладки канала или группы
author: laujan
description: Краткое руководство по созданию вкладки канала и группы с помощью генератора Yeoman для Microsoft Teams, включая просмотр исходного кода с примерами кода.
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 736b8821a7d0f9e1eda35377bc4937e68c035c75
ms.sourcegitcommit: b2f6599e44a418b4cce92f28843b7e013fd6e86d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2022
ms.locfileid: "64686678"
---
# <a name="channel-or-group-tab"></a>Вкладка "Канал" или "Группа"

Вкладки каналов или групп позволяют добавлять нужный контент на каналы и в групповые чаты. Это отличный способ создать пространство для совместной работы над определенным веб-контентом.

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>Создание настраиваемой вкладки канала или группы с Node.js

1. В командной строке установите пакеты [Yeoman](https://yeoman.io/) и [gulp-cli](https://www.npmjs.com/package/gulp-cli) , введя следующую команду **после** установкиNode.js:

    ```cmd
    npm install yo gulp-cli --global
    ```

2. В командной строке установите Microsoft Teams app, введя следующую команду:

    ```cmd
    npm install generator-teams --global
    ```

Ниже приведены шаги по созданию вкладки канала или группы:

* [Создание приложения с помощью вкладки канала или группы](#generate-your-application-with-a-channel-or-group-tab)
* [Создание пакета приложения](#create-your-app-package)
* [Сборка и запуск приложения](#build-and-run-your-application)
* [Установка безопасного туннеля на вкладке](#establish-a-secure-tunnel-to-your-tab)
* [Upload приложения для Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Создание приложения с помощью вкладки канала или группы

1. В командной строке создайте каталог для вкладки канала или группы.

1. Введите следующую команду в новом каталоге, чтобы запустить Microsoft Teams App:

    ```cmd
    yo teams
    ```

1. Укажите свои значения для ряда вопросов, которые Microsoft Teams app generator для обновления **файла manifest.json**:

    ![Снимок экрана: открытие генератора](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

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

        Используйте клавиши со стрелками, чтобы выбрать **вкладку "Настройка** ".

    * **Какие области планируется использовать для вкладки?**

        Вы можете выбрать команду или групповой чат.

    * **Требуется ли Microsoft Azure Active Directory единого входа (Azure AD) для вкладки?**

        Не **включайте** Microsoft Azure Active Directory единого входа (Azure AD) для вкладки. Значение по умолчанию — да, введите **n**.

    * **Вы хотите, чтобы эта вкладка была доступна в SharePoint Online? (Y/n)**

        **Введите n**.

    </details>

> [!IMPORTANT]
> Компонент пути **yourDefaultTabNameTab** — это значение, введенное в генераторе для имени  вкладки по умолчанию и слова **TAB**.
>
> Например: DefaultTabName — **MyTab** then **/MyTabTab/**

### <a name="create-your-app-package"></a>Создание пакета приложения

У вас должен быть пакет приложения для сборки и запуска приложения в Teams. Пакет приложения создается с помощью задачи gulp, которая проверяет файл **manifest.json** и создает ZIP-папку в **каталоге ./package** . В командной строке введите следующую команду:

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>Сборка и запуск приложения

#### <a name="build-your-application"></a>Создание приложения

Введите следующую команду в командной строке, чтобы транспилировать решение в папку **./dist** :

```cmd
gulp build
```

#### <a name="run-your-application"></a>Запуск приложения

1. В командной строке введите следующую команду, чтобы запустить локальный веб-сервер:

    ```bash
    gulp serve
    ```

1. Введите `http://localhost:3007/<yourDefaultAppNameTab>/` данные в браузере, чтобы просмотреть домашнюю страницу приложения.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Вкладка по умолчанию" border="true":::

1. Чтобы просмотреть страницу конфигурации вкладки, перейдите на страницу `http://localhost:3007/<yourDefaultAppNameTab>/config.html`. Ниже показано следующее.

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="Страница конфигурации табуляции" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установка безопасного туннеля на вкладке

Чтобы установить безопасный туннель на вкладке, выйдите из localhost и введите следующую команду:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> После отправки в Microsoft Teams **ngrok** и успешного сохранения ее можно просмотреть в Teams до завершения сеанса туннеля. При перезапуске сеанса ngrok необходимо обновить приложение с помощью нового URL-адреса.

### <a name="upload-your-application-to-teams"></a>Upload приложения для Teams

1. Перейдите Microsoft Teams и выберите **"**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Приложения Teams Store&quot;":::.
1. Выберите **"Управление приложениями****" и Upload настраиваемое приложение**.
1. Перейдите в каталог проекта, перейдите в папку **./package** , выберите ZIP-папку пакета приложения и нажмите кнопку **"Открыть"**.
    
    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="Вкладка &quot;Отправленный канал&quot;" border="true":::

1. Выберите **"Добавить** " в диалоговом окне. Вкладка отправляется в Teams.
    
    > [!NOTE]
    > Если  **add** не отображается в диалоговом окне, удалите следующий код из манифеста zip-папки отправленного пакета приложения. Снова заархивируйте папку и отправьте ее в Teams.
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. Следуйте указаниям по добавлению вкладки. Существует диалоговое окно настраиваемой конфигурации для вкладки канала или группы.
1. Нажмите **кнопку "** Сохранить", и вкладка будет добавлена на панель вкладок канала.

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="Вкладка &quot;Канал&quot; отправлена" border="true":::
    
    Теперь вы успешно создали и добавили вкладку канала или группы в Teams.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>Создание настраиваемой вкладки канала или группы с ASP.NET Core

1. В командной строке создайте каталог для проекта вкладки.

1. Клонируйте пример репозитория в новый каталог с помощью следующей команды или скачайте исходный [код и](https://github.com/OfficeDev/Microsoft-Teams-Samples) извлеките файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже приведены шаги по созданию вкладки канала или группы:

* [Создание приложения с помощью вкладки канала или группы](#generate-your-application-with-a-channel-or-group-tab-1)
* [Установка безопасного туннеля на вкладке](#establish-a-secure-tunnel-to-your-tab-1)
* [Обновление приложения](#update-your-application)
* [Сборка и запуск приложения](#build-and-run-your-application-1)
* [Обновление пакета приложения с помощью портала разработчика](#update-your-app-package-with-developer-portal)
* [Предварительный просмотр приложения в Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Создание приложения с помощью вкладки канала или группы

1. Откройте Visual Studio и выберите **"Открыть проект или решение"**.

1. Перейдите в папку Microsoft-Teams-Samplessamplestab-channel-grouprazor-csharp  >  >  >  и откройте **файл channelGroupTab.sln**.

1. В Visual Studio нажмите **клавишу F5** или выберите команду **"** Начать отладку" в меню отладки  приложения, чтобы убедиться, что приложение загружено правильно. В браузере перейдите по следующим URL-адресам:

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>Просмотр исходного кода</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан на основе пустого шаблона ASP.NET Core 3.1 с флажком "Дополнительно *** Настройка HTTPS**", выбранным при установке. Службы MVC регистрируются с помощью метода платформы внедрения зависимостей `ConfigureServices()` . Кроме того, пустой шаблон не включает обслуживание статического содержимого по умолчанию, `Configure()` поэтому ПО промежуточного слоя статических файлов добавляется в метод с помощью следующего кода:

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

#### <a name="tabcs"></a>Tab.cs

Этот файл C# содержит метод, вызываемый из **tab.cshtml во** время настройки.

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакетов приложений:

* **Значок полного цвета**, размером 192 x 192 пикселя.
* **Значок прозрачной структуры** размером 32 x 32 пикселя.
* Файл **manifest.json** , указывающий атрибуты приложения.

Эти файлы необходимо заархивируйте в пакете приложения для использования при отправке вкладки в Teams. Когда пользователь выбирает добавление или обновление вкладки, `configurationUrl` Microsoft Teams загружает указанный манифест, внедряет ее в IFrame и отображает на вкладке.

#### <a name="csproj"></a>CSPROJ

В окне Visual Studio Обозреватель решений щелкните проект правой кнопкой мыши и выберите команду "Изменить **Project"**. В конце файла вы увидите следующий код, который создает и обновляет ZIP-папку при сборке приложения:

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

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установка безопасного туннеля на вкладке

В командной строке в корне каталога проекта выполните следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
ngrok http 3978 --host-header=localhost
```

Убедитесь, что командная строка запущена с помощью ngrok, и запишите URL-адрес.

### <a name="update-your-application"></a>Обновление приложения

1. Откройте Visual Studio Обозреватель решений и перейдите в папку **PagesShared**  >  и **откройте _Layout.cshtml** и добавьте в файл <head> Раздел тегов:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > Не копируйте и не вставьте `<script src="...">` URL-адреса на этой странице, так как они не представляют последнюю версию. Чтобы получить последнюю версию пакета SDK, всегда перейдите [Microsoft Teams API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).
    
1. Вставьте вызов в `microsoftTeams.initialize();` тег `script` .

1. В Visual Studio Обозреватель решений перейдите в папку **Pages** и откройте **tab.cshtml**.

    В **файле Tab.cshtml** приложение предоставляет пользователю две кнопки для отображения вкладки с красным или серым значком. Выбор триггеров **кнопки "Выбрать серый**  `saveGray()` `saveRed()`" или "Красный" или , соответственно, `settings.setValidityState(true)`задает и включает кнопку "**Сохранить" на** странице конфигурации. Этот код Teams, что вы выполнили требования к конфигурации и установка может продолжиться. Задайте параметры `settings.setSettings` . Наконец, `saveEvent.notifySuccess()` вызывается, чтобы указать, что URL-адрес содержимого успешно разрешен.

1. Обновите `websiteUrl` значения `contentUrl` в каждой функции, указав URL-адрес ngrok HTTPS на вкладке.

    Теперь код должен содержать следующий код **, заменив y8rCgT2b** URL-адресом ngrok:

    ```javascript
        
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
        });
        }
    ```

1. Сохраните обновленный **файл Tab.cshtml**.

### <a name="build-and-run-your-application"></a>Сборка и запуск приложения

1. В Visual Studio нажмите **клавишу F5** или выберите **команду "** Начать отладку" в меню **"Отладка**".

1. Убедитесь **, что ngrok** работает и работает правильно, открыв браузер и перейдя на страницу содержимого по URL-адресу ngrok HTTPS, указанному в окне командной строки.

    > [!TIP]
    > Для выполнения действий, описанных в этой статье, необходимо Visual Studio и ngrok. Если вам нужно остановить запуск приложения в Visual Studio для работы с ним, продолжайте **работу ngrok**. Он прослушивает и возобновляет маршрутизацию запроса приложения при его перезапуске в Visual Studio. Если вам нужно перезапустить службу ngrok, она возвращает новый URL-адрес и необходимо обновить приложение новым URL-адресом.

### <a name="update-your-app-package-with-developer-portal"></a>Обновление пакета приложения с помощью портала разработчика

1. Перейдите к Microsoft Teams. Если вы используете [веб-версию](https://teams.microsoft.com), вы можете проверить интерфейсный код с помощью средств разработчика [браузера](~/tabs/how-to/developer-tools.md).

1. Перейдите на [**портал разработчика**](https://dev.teams.microsoft.com/home).

1. Откройте **"Приложения** " и выберите **"Импорт приложения"**.

1. Имя пакета приложения **—tab.zip.** Он доступен по следующему пути:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Выберите **tab.zip** и откройте его на портале разработчика.

1. Идентификатор приложения **по умолчанию создается** и заполняется в разделе " **Основные сведения** ".

1. Добавьте краткое и длинное описание приложения в **описание**.

1. В **разделе "Сведения** о разработчике" добавьте необходимые сведения, а на веб-сайте (должен быть допустимым **URL-адресом HTTPS)** укажите URL-адрес HTTPS ngrok.

1. В **URL-адресах приложений** обновите политику конфиденциальности `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` и сохраните условия использования.

1. В **разделе "Функции приложения**" выберите приложение "Группа" и "Канал". Обновите **URL-адрес конфигурации** и `https://<yourngrokurl>/tab` выберите **область вкладки**.

1. Выберите **Сохранить**.

1. В разделе "Домены" домены с вкладок должны содержать URL-адрес ngrok без префикса HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Предварительный просмотр приложения в Teams

1. Выберите **предварительный просмотр Teams** на панели инструментов портала разработчика. Портал разработчика информирует вас об успешной загрузке неопубликованного приложения. Страница **"Добавить**" появится для вашего приложения в Teams.

1. Выберите **"Добавить в команду** ", чтобы настроить вкладку в команде. Настройте вкладку и нажмите кнопку " **Сохранить"**. Вкладка теперь доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Вкладка канала ASPNET отправлена" border="true":::
    
    Теперь вы успешно создали и добавили вкладку канала или группы в Teams.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>Создание настраиваемой вкладки канала или группы с ASP.NET Core MVC

1. В командной строке создайте каталог для проекта вкладки.

1. Клонируйте пример репозитория в новый каталог с помощью следующей команды или скачайте исходный [код и](https://github.com/OfficeDev/Microsoft-Teams-Samples) извлеките файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже приведены шаги по созданию вкладки канала или группы:

* [Создание приложения с помощью вкладки канала или группы](#generate-your-application-with-a-channel-or-group-tab-2)
* [Установка безопасного туннеля на вкладке](#establish-a-secure-tunnel-to-your-tab-2)
* [Обновление приложения](#update-your-application-1)
* [Сборка и запуск приложения](#build-and-run-your-application-2)
* [Обновление пакета приложения с помощью портала разработчика](#update-your-app-package-with-developer-portal-1)
* [Предварительный просмотр приложения в Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Создание приложения с помощью вкладки канала или группы

1. Откройте Visual Studio и выберите **"Открыть проект или решение"**.

1. Перейдите в папку Microsoft-Teams-Samplessamplestab-channel-groupmvc-csharp  >  >  >  и откройте **файл ChannelGroupTabMVC.sln**.

1. В Visual Studio нажмите **клавишу F5** или выберите команду **"** Начать отладку" в меню отладки  приложения, чтобы убедиться, что приложение загружено правильно. В браузере перейдите по следующим URL-адресам:

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>Просмотр исходного кода</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан на основе пустого шаблона ASP.NET Core 3.1 с флажком "Дополнительно — настройка **HTTPS**", выбранным при установке. Службы MVC регистрируются с помощью метода платформы внедрения зависимостей `ConfigureServices()` . Кроме того, пустой шаблон не включает обслуживание статического содержимого по умолчанию, `Configure()` поэтому ПО промежуточного слоя статических файлов добавляется в метод с помощью следующего кода:

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

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакетов приложений:

* **Значок полного цвета**, размером 192 x 192 пикселя.
* **Значок прозрачной структуры** размером 32 x 32 пикселя.
* Файл **manifest.json** , указывающий атрибуты приложения.

Эти файлы необходимо заархивируйте в пакете приложения для использования при отправке вкладки в Teams.

#### <a name="csproj"></a>CSPROJ

В окне Visual Studio Обозреватель решений щелкните проект правой кнопкой мыши и выберите команду "Изменить **Project"**. В конце файла вы увидите следующий код, который создает и обновляет ZIP-папку при сборке приложения:

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

#### <a name="models"></a>Модели

**ChannelGroup.cs** представляет объект Message и методы, которые будут вызываться из контроллеров во время настройки.

#### <a name="views"></a>Представления

Ниже приведены различные представления в ASP.NET Core MVC:

* Главная: ASP.NET Core обрабатывает файлы с именем **Index** как домашнюю страницу сайта или по умолчанию. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** будет отображаться как домашняя страница приложения.

* Общий доступ. Частичная разметка **представления _Layout.cshtml** содержит общую структуру страницы приложения и общие визуальные элементы. Он также будет ссылаться на Teams библиотеку.

#### <a name="controllers"></a>Контроллеры

Контроллеры используют свойство `ViewBag` для динамической передачи значений в представления.

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установка безопасного туннеля на вкладке

В командной строке в корне каталога проекта выполните следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
ngrok http 3978 --host-header=localhost
```

Убедитесь, что командная строка запущена с помощью ngrok, и запишите URL-адрес.

### <a name="update-your-application"></a>Обновление приложения

1. Откройте Visual Studio Обозреватель решений и перейдите в папку **ViewsShared**  >  и **откройте _Layout.cshtml** и добавьте в файл <head> Раздел тегов:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > Не копируйте и не вставьте `<script src="...">` URL-адреса на этой странице, так как они не представляют последнюю версию. Чтобы получить последнюю версию пакета SDK, всегда перейдите [Microsoft Teams API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).
    
1. Вставьте вызов в `microsoftTeams.initialize();` тег `script` .

1. В Visual Studio Обозреватель решений перейдите в **папку TAB** и откройте **файл Tab.cshtml**.

    В **файле Tab.cshtml** приложение предоставляет пользователю две кнопки для отображения вкладки с красным или серым значком. Выбор триггеров **кнопки "Выбрать серый**  `saveGray()` `saveRed()`" или "Красный" или , соответственно, `settings.setValidityState(true)`задает и включает кнопку "**Сохранить" на** странице конфигурации. Этот код Teams, что вы выполнили требования к конфигурации и установка может продолжиться. Задайте параметры `settings.setSettings` . Наконец, `saveEvent.notifySuccess()` вызывается, чтобы указать, что URL-адрес содержимого успешно разрешен. 

1. Обновите `websiteUrl` значения `contentUrl` в каждой функции, указав URL-адрес ngrok HTTPS на вкладке.

    Теперь код должен содержать следующий код **, заменив y8rCgT2b** URL-адресом ngrok:

    ```javascript

        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    
        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. Обязательно сохраните обновленный **файл Tab.cshtml**.

### <a name="build-and-run-your-application"></a>Сборка и запуск приложения

1. В Visual Studio нажмите **клавишу F5** или выберите **команду "** Начать отладку" в меню **"Отладка**".

1. Убедитесь **, что ngrok** работает и работает правильно, открыв браузер и перейдя на страницу содержимого по URL-адресу ngrok HTTPS, указанному в окне командной строки.

    > [!TIP]
    > Для выполнения действий, описанных в этой статье, необходимо Visual Studio и ngrok. Если вам нужно остановить запуск приложения в Visual Studio для работы с ним, продолжайте **работу ngrok**. Он прослушивает и возобновляет маршрутизацию запроса приложения при его перезапуске в Visual Studio. Если вам нужно перезапустить службу ngrok, она возвращает новый URL-адрес и необходимо обновить приложение новым URL-адресом.

### <a name="update-your-app-package-with-developer-portal"></a>Обновление пакета приложения с помощью портала разработчика

1. Перейдите к Microsoft Teams. Если вы используете [веб-версию](https://teams.microsoft.com), вы можете проверить интерфейсный код с помощью средств разработчика [браузера](~/tabs/how-to/developer-tools.md).

1. Перейдите на [**портал разработчика**](https://dev.teams.microsoft.com/home).

1. Откройте **"Приложения** " и выберите **"Импорт приложения"**.

1. Имя пакета приложения **—tab.zip.** Он доступен по следующему пути:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Выберите **tab.zip** и откройте его на портале разработчика.

1. Идентификатор приложения **по умолчанию создается** и заполняется в разделе " **Основные сведения** ".

1. Добавьте краткое и длинное описание приложения в **описание**.

1. В **разделе "Сведения** о разработчике" добавьте необходимые сведения, а на веб-сайте (должен быть допустимым **URL-адресом HTTPS)** укажите URL-адрес HTTPS ngrok.

1. В **URL-адресах приложений** обновите политику конфиденциальности `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` и сохраните условия использования.

1. В **разделе "Функции приложения**" выберите приложение "Группа" и "Канал". Обновите **URL-адрес конфигурации** и `https://<yourngrokurl>/tab` выберите **область вкладки**.

1. Выберите **Сохранить**.

1. В разделе "Домены" домены с вкладок должны содержать URL-адрес ngrok без префикса HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Предварительный просмотр приложения в Teams

1. Выберите **предварительный просмотр Teams** на панели инструментов портала разработчика. Портал разработчика информирует вас об успешной загрузке неопубликованного приложения. Страница **"Добавить**" появится для вашего приложения в Teams.

1. Выберите **"Добавить в команду** ", чтобы настроить вкладку в команде. Настройте вкладку и нажмите кнопку " **Сохранить"**. Вкладка теперь доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Вкладка канала ASPNET MVC отправлена" border="true":::
    
    Теперь вы успешно создали и добавили вкладку канала или группы в Teams.

::: zone-end

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создать страницу контента](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>См. также

* [Teams вкладок](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Создать страницу удаления](~/tabs/how-to/create-tab-pages/removal-page.md)
