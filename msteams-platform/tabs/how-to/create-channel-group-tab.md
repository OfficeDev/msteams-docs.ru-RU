---
title: Создание вкладки канала или группы
author: laujan
description: Руководство по созданию вкладки каналов и групп с генератором Yeoman для Microsoft Teams, в том числе обзор исходных кодов с примерами кода.
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 7d74a49ff85986b27ec30eeffbc15ca836a6a94b
ms.sourcegitcommit: 52af681132e496a57b18f468c5b73265a49a5f44
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/31/2022
ms.locfileid: "64590674"
---
# <a name="channel-or-group-tab"></a>Вкладка канал или группа

Вкладки каналов или групп позволяют добавлять нужный контент на каналы и в групповые чаты. Это отличный способ создать пространство для совместной работы над определенным веб-контентом.

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>Создание настраиваемой вкладки канала или группы с помощью Node.js

1. В командной подсказке установите [пакеты Yeoman](https://yeoman.io/) и [gulp-cli](https://www.npmjs.com/package/gulp-cli) , введите следующую команду после установки **Node.js**:

    ```cmd
    npm install yo gulp-cli --global
    ```

2. В командной подсказке установите Microsoft Teams app generator, введите следующую команду:

    ```cmd
    npm install generator-teams --global
    ```

Ниже следующую следующую меру по созданию вкладки канала или группы:

* [Создание приложения с помощью вкладки канала или группы](#generate-your-application-with-a-channel-or-group-tab)
* [Создание пакета приложения](#create-your-app-package)
* [Сборка и запуск приложения](#build-and-run-your-application)
* [Создание безопасного туннеля на вкладке](#establish-a-secure-tunnel-to-your-tab)
* [Upload приложение для Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Создание приложения с помощью вкладки канала или группы

1. В командной подсказке создайте новый каталог для вкладки канала или группы.

1. Введите следующую команду в новом каталоге, чтобы запустить Microsoft Teams app:

    ```cmd
    yo teams
    ```

1. Предодавайте значения ряду вопросов, задамых генератором Microsoft Teams для обновления файла **manifest.json**:

    ![Снимок экрана открытия генератора](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

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

        Используйте клавиши со стрелками, чтобы выбрать **вкладку Configurable** .

    * **Какие области вы собираетесь использовать для вкладки?**

        Вы можете выбрать группу или групповой чат.

    * **Требуется ли Microsoft Azure Active Directory (Azure AD) для единой входной поддержки вкладки?**

        Не **включай** Microsoft Azure Active Directory (Azure AD) для вкладки с одним входом. По умолчанию — да, введите **n**.

    * **Хотите, чтобы эта вкладка была доступна в SharePoint Online? (Y/n)**

        **Введите n**.

    </details>

> [!IMPORTANT]
> Компонент пути **yourDefaultTabNameTab** — это значение, которое вы ввели в генератор имени вкладки по **умолчанию плюс слово** **Tab**.
>
> Например: DefaultTabName **— это MyTab** then **/MyTabTab/**

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

    ```bash
    gulp serve
    ```

1. Введите `http://localhost:3007/<yourDefaultAppNameTab>/` в браузере, чтобы просмотреть домашняя страница приложения.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Вкладка по умолчанию" border="true":::

1. Чтобы просмотреть страницу конфигурации вкладок, перейдите к `https://localhost:3007/<yourDefaultAppNameTab>/config.html`. Ниже показано:

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="Страница конфигурации вкладок" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Создание безопасного туннеля на вкладке

Чтобы установить безопасный туннель на вкладке, выйдите из localhost и введите следующую команду:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> После того как вкладка будет загружена Microsoft Teams **ngrok** и успешно сохранена, ее можно просмотреть в Teams до окончания сеанса туннеля. Если вы перезапустите сеанс ngrok, необходимо обновить приложение с помощью нового URL-адреса.

### <a name="upload-your-application-to-teams"></a>Upload приложение для Teams

1. Перейдите Microsoft Teams и выберите **Store**&nbsp; :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::.
1. Выберите **Управление приложениями**.
1. Выберите **Опубликовать приложение** **и Upload настраиваемом приложении**.

    :::image type="content" source="~/assets/images/tab-images/publish-app.png" alt-text="Upload настраиваемом приложении" border="true":::

1. Перейдите в каталог проекта, просмотрите **папку ./package**, выберите папку почтовый индекс пакета приложений **и откройте.**
    
    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="Загруженная вкладка канала" border="true":::

1. Выберите **Добавить** в всплывающее окно. Вкладка загружается в Teams.
    
    > [!NOTE]
    > Если  **Add** не отображается в диалоговом окне, удалите следующий код из манифеста папки почтовых ящиков пакетов приложений. Снова застегивать папку и загружать ее в Teams.
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. Вернись в свою команду, выберите канал, в котором нужно добавить вкладку, ➕ выберите из панели вкладок и выберите вкладку из списка.
1. Следуйте указаниям для добавления вкладки. Существует настраиваемый диалоговое окно конфигурации для канала или вкладки группы.
1. Выберите **Сохранить** и вкладка добавляется в вкладку канала.

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="Загруженная вкладка канала" border="true":::

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>Создание настраиваемой вкладки канала или группы с помощью ASP.NET Core

1. В командной подсказке создайте новый каталог для проекта вкладки.

1. Клонировать репозиторий образца в новый каталог с помощью следующей команды или можно [](https://github.com/OfficeDev/Microsoft-Teams-Samples) скачать исходный код и извлечь файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже следующую следующую меру по созданию вкладки канала или группы:

* [Создание приложения с помощью вкладки канала или группы](#generate-your-application-with-a-channel-or-group-tab-1)
* [Создание безопасного туннеля на вкладке](#establish-a-secure-tunnel-to-your-tab-1)
* [Обновление приложения](#update-your-application)
* [Сборка и запуск приложения](#build-and-run-your-application-1)
* [Обновление пакета приложений с помощью портала разработчиков](#update-your-app-package-with-developer-portal)
* [Просмотр приложения в Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Создание приложения с помощью вкладки канала или группы

1. Откройте Visual Studio и **выберите Откройте проект или решение**.

1. Перейдите в папку Microsoft-Teams-Samplessamplestab-channel-grouprazor-csharp  >  >  >  и открытый **каналGroupTab.sln**.

1. В Visual Studio нажмите **кнопку F5** или выберите Пуск отладки из меню отладки приложения, чтобы  проверить правильность загрузки приложения. В браузере перейдите к следующим URL-адресам:

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>Просмотр исходных кодов</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан из пустого шаблона ASP.NET Core 3.1 веб-приложения с расширенным *** Настройка для контрольного окна HTTPS**, выбранного при установке. Службы MVC регистрируются методом впрыскивания зависимостей `ConfigureServices()` . Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, `Configure()` поэтому в метод добавляется среднее по статическим файлам с помощью следующего кода:

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

#### <a name="tabcs"></a>Tab.cs

Этот C# содержит метод, который вызван из **Tab.cshtml** во время настройки.

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложений:

* **Значок полного цвета** размером 192 x 192 пикселя.
* **Прозрачный значок контура** размером 32 x 32 пикселя.
* Файл **manifest.json** , который указывает атрибуты вашего приложения.

Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams. Когда пользователь выбирает добавить или обновить вкладку, `configurationUrl` Microsoft Teams загружает указанные в манифесте данные, встраив ее в IFrame и отрисовка ее на вкладке.

#### <a name="csproj"></a>.csproj

В окне Visual Studio Обозреватель решений нажмите правой кнопкой мыши на проект и выберите **Изменить Project Файл**. В конце файла вы увидите следующий код, который создает и обновляет папку zip при создании приложения:

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

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Создание безопасного туннеля на вкладке

На командной подсказке в корневом каталоге проекта запустите следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
ngrok http 3978 --host-header=localhost
```

Убедитесь, что командная подсказка будет запущена с помощью ngrok, и сделайте примечание URL-адреса.

### <a name="update-your-application"></a>Обновление приложения

1. Перейдите в **папку PagesShared** >  **и откройте _Layout.cshtml** и добавьте следующие <head> Раздел тегов:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > Не копируйте и не вделайте `<script src="...">` URL-адреса на этой странице, так как они не представляют последнюю версию. Чтобы получить последнюю версию SDK, всегда Microsoft Teams [API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).
    
1. В верхней части тега `script` вставьте вызов `microsoftTeams.initialize();`.

1. Перейдите в **папку Страницы** и откройте **Tab.cshtml**

    В **Tab.cshtml** приложение представляет пользователю две кнопки параметра для отображения вкладки с красным или серым значком. Выбор триггеров **выберите серый** или **выберите** `saveGray()` `saveRed()`красный или, соответственно, `settings.setValidityState(true)`наборы и включает кнопку **Сохранить** на странице конфигурации. Этот код позволяет Teams, что вы выполнили требования к конфигурации и установка может продолжиться. Параметры `settings.setSettings` заданы. Наконец, `saveEvent.notifySuccess()` называется, чтобы указать, что URL-адрес контента успешно решен.

1. Обновление значений `websiteUrl` `contentUrl` и значений в каждой функции с ПОМОЩЬЮ URL-адреса https ngrok на вкладке.

    Теперь в коде должны быть указаны следующие **y8rCgT2b** , замененные URL-адресом ngrok:

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

1. Сохраните обновленный **Tab.cshtml**.

### <a name="build-and-run-your-application"></a>Сборка и запуск приложения

1. В Visual Studio нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки**.

1. Убедитесь, что ngrok работает и работает должным образом, открыв браузер и переехав на страницу контента через URL-адрес https **ngrok** , который был представлен в окне командной подсказки.

    > [!TIP]
    > Для выполнения действий, предусмотренных в этой статье, необходимо Visual Studio и ngrok. Если для работы с приложением необходимо прекратить Visual Studio, продолжайте **работать с ngrok**. Он прослушивает и возобновляет маршрутизаку запроса приложения при его перезапуске в Visual Studio. Если вам нужно перезапустить службу ngrok, она возвращает новый URL-адрес, и вам необходимо обновить приложение с помощью нового URL-адреса.

### <a name="update-your-app-package-with-developer-portal"></a>Обновление пакета приложений с помощью портала разработчиков

1. Перейдите в Microsoft Teams. Если вы используете [веб-версию](https://teams.microsoft.com), вы можете проверить исходный код с помощью средств разработки [браузера](~/tabs/how-to/developer-tools.md).

1. Перейдите на **портал разработчика** в Teams.

1. Откройте **приложения** и выберите **импортное приложение**.

1. Имя вашего пакета **приложенийtab.zip.** Он доступен по следующему пути:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Выберите **tab.zip** и откройте его на портале разработчиков.

1. По умолчанию **создается** и заполняется ID приложения по умолчанию в **разделе Основные сведения** .

1. Добавьте краткое и длинное описание для приложения в **Описания**.

1. В **сведениях разработчика** добавьте необходимые сведения, а на веб-сайте (должен быть допустимый **URL-адрес HTTPS)** укажи URL-адрес ngrok HTTPS.

1. В **URL-адресах** приложений обновите политику конфиденциальности `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` и сохраните ее.

1. В **функции Приложения** выберите личное приложение и введите имя и обнови **url-адрес** контента с `https://<yourngrokurl>/personalTab`помощью . Оставьте поле URL-адрес веб-сайта пустым. 

1. Нажмите кнопку **Сохранить**.

1. В разделе Домены домены с вкладок должны содержать URL-адрес ngrok без префикса `<yourngrokurl>.ngrok.io`HTTPS.

### <a name="preview-your-app-in-teams"></a>Просмотр приложения в Teams

1. Выберите **предварительный просмотр Teams** из панели инструментов портала разработчиков. Портал разработчиков сообщает, что ваше приложение успешно загружено боком.

1. Выберите **Управление приложениями**. Ваше приложение перечислены в загруженных приложениях.

1. Найдите приложение с помощью поиска, выберите &#x25CF;&#x25CF;&#x25CF;.

1. Выберите параметр **Просмотр сведений** . Окно сведений о приложении отображается для приложения.

1. Выберите &nbsp;:::image type="content" source="~/assets/images/tab-images/app-dropdown.png" alt-text="dropdown App" border="true":::&nbsp; >  **DetailsAdd для загрузки** вкладки в команде. Вкладка теперь доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Загружена вкладка канала ASPNET" border="true":::

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>Создание настраиваемой вкладки канала или группы с помощью ASP.NET Core MVC

1. В командной подсказке создайте новый каталог для проекта вкладки.

1. Клонировать репозиторий образца в новый каталог с помощью следующей команды или можно [](https://github.com/OfficeDev/Microsoft-Teams-Samples) скачать исходный код и извлечь файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже следующую следующую меру по созданию вкладки канала или группы:

* [Создание приложения с помощью вкладки канала или группы](#generate-your-application-with-a-channel-or-group-tab-2)
* [Создание безопасного туннеля на вкладке](#establish-a-secure-tunnel-to-your-tab-2)
* [Обновление приложения](#update-your-application-1)
* [Сборка и запуск приложения](#build-and-run-your-application-2)
* [Обновление пакета приложений с помощью портала разработчиков](#update-your-app-package-with-developer-portal-1)
* [Просмотр приложения в Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Создание приложения с помощью вкладки канала или группы

1. Откройте Visual Studio и **выберите Откройте проект или решение**.

1. Перейдите в папку Microsoft-Teams-Samplessamplestab-channel-groupmvc-csharp  >  >  >  и откройте **ChannelGroupTabMVC.sln**.

1. В Visual Studio нажмите **кнопку F5** или выберите Пуск отладки из меню отладки приложения, чтобы  проверить правильность загрузки приложения. В браузере перейдите к следующим URL-адресам:

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>Просмотр исходных кодов</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан из пустого шаблона ASP.NET Core 3.1 веб-приложения с расширенным **- Настройка для проверки HTTPS**, выбранной при установке. Службы MVC регистрируются методом впрыскивания зависимостей `ConfigureServices()` . Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, `Configure()` поэтому в метод добавляется среднее по статическим файлам с помощью следующего кода:

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

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложений:

* **Значок полного цвета** размером 192 x 192 пикселя.
* **Прозрачный значок контура** размером 32 x 32 пикселя.
* Файл **manifest.json** , который указывает атрибуты вашего приложения.

Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams.

#### <a name="csproj"></a>.csproj

В окне Visual Studio Обозреватель решений нажмите правой кнопкой мыши на проект и выберите **Изменить Project Файл**. В конце файла вы увидите следующий код, который создает и обновляет папку zip при создании приложения:

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

**ChannelGroup.cs представляет** объект Сообщения и методы, которые будут вызваны из контроллеров во время настройки.

#### <a name="views"></a>Представления

Это различные представления в ASP.NET Core MVC:

* Главная: ASP.NET Core обрабатывает файлы под названием **Index** в качестве домашней страницы или по умолчанию для сайта. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** будет отображаться в качестве домашней страницы приложения.

* Общий доступ. Частичная разметка **_Layout.cshtml** содержит общую структуру страницы приложения и общие визуальные элементы. Он также будет ссылаться на Teams библиотеку.

#### <a name="controllers"></a>Контроллеры

Контроллеры используют свойство `ViewBag` для динамического переноса значений в представления.

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Создание безопасного туннеля на вкладке

На командной подсказке в корневом каталоге проекта запустите следующую команду, чтобы установить безопасный туннель на вкладке:

```cmd
ngrok http 3978 --host-header=localhost
```

Убедитесь, что командная подсказка будет запущена с помощью ngrok, и сделайте примечание URL-адреса.

### <a name="update-your-application"></a>Обновление приложения

1. Перейдите в **папку** **ViewsShared** >  и **откройте _Layout.cshtml** и добавьте следующее в <head> Раздел тегов:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > Не копируйте и не вделайте `<script src="...">` URL-адреса на этой странице, так как они не представляют последнюю версию. Чтобы получить последнюю версию SDK, всегда Microsoft Teams [API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).
    
1. В верхней части тега `script` вставьте вызов `microsoftTeams.initialize();`.

1. Перейдите в **папку Tab** и откройте **Tab.cshtml**

    В **Tab.cshtml** приложение представляет пользователю две кнопки параметра для отображения вкладки с красным или серым значком. Выбор триггеров **выберите серый** или **выберите** `saveGray()` `saveRed()`красный или, соответственно, `settings.setValidityState(true)`наборы и включает кнопку **Сохранить** на странице конфигурации. Этот код позволяет Teams, что вы выполнили требования к конфигурации и установка может продолжиться. Параметры `settings.setSettings` заданы. Наконец, `saveEvent.notifySuccess()` называется, чтобы указать, что URL-адрес контента успешно решен. 

1. Обновление значений `websiteUrl` `contentUrl` и значений в каждой функции с ПОМОЩЬЮ URL-адреса https ngrok на вкладке.

    Теперь в коде должны быть указаны следующие **y8rCgT2b** , замененные URL-адресом ngrok:

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

1. Обязательно сохраните обновленный **Tab.cshtml**.

### <a name="build-and-run-your-application"></a>Сборка и запуск приложения

1. В Visual Studio нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки**.

1. Убедитесь, что ngrok работает и работает должным образом, открыв браузер и переехав на страницу контента через URL-адрес https **ngrok** , который был представлен в окне командной подсказки.

    > [!TIP]
    > Для выполнения действий, предусмотренных в этой статье, необходимо Visual Studio и ngrok. Если для работы с приложением необходимо прекратить Visual Studio, продолжайте **работать с ngrok**. Он прослушивает и возобновляет маршрутизаку запроса приложения при его перезапуске в Visual Studio. Если вам нужно перезапустить службу ngrok, она возвращает новый URL-адрес, и вам необходимо обновить приложение с помощью нового URL-адреса.

### <a name="update-your-app-package-with-developer-portal"></a>Обновление пакета приложений с помощью портала разработчиков

1. Перейдите в Microsoft Teams. Если вы используете [веб-версию](https://teams.microsoft.com), вы можете проверить исходный код с помощью средств разработки [браузера](~/tabs/how-to/developer-tools.md).

1. Перейдите **на портал разработчика** в Teams.

1. Откройте **приложения** и выберите **импортное приложение**.

1. Имя вашего пакета **приложенийtab.zip.** Он доступен по следующему пути:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Выберите **tab.zip** и откройте его на портале разработчиков.

1. По умолчанию **создается** и заполняется ID приложения по умолчанию в **разделе Основные сведения** .

1. Добавьте краткое и длинное описание для приложения в **Описания**.

1. В **сведениях разработчика** добавьте необходимые сведения, а на веб-сайте (должен быть допустимый **URL-адрес HTTPS)** укажи URL-адрес ngrok HTTPS.

1. В **URL-адресах** приложений обновите политику конфиденциальности `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` и сохраните ее.

1. В **функции Приложения** выберите личное приложение и введите имя и обнови **url-адрес** контента с `https://<yourngrokurl>/personalTab`помощью . Оставьте поле URL-адрес веб-сайта пустым.

1. Нажмите кнопку **Сохранить**.

1. В разделе Домены домены с вкладок должны содержать URL-адрес ngrok без префикса `<yourngrokurl>.ngrok.io`HTTPS.

### <a name="preview-your-app-in-teams"></a>Просмотр приложения в Teams

1. Выберите **предварительный просмотр Teams** из панели инструментов портала разработчиков. Портал разработчиков сообщает, что ваше приложение успешно загружено боком.

1. Выберите **Управление приложениями**. Ваше приложение перечислены в загруженных приложениях.

1. Найдите приложение с помощью поиска, выберите &#x25CF;&#x25CF;&#x25CF;.

1. Выберите параметр **Просмотр сведений** . Окно сведений о приложении отображается для приложения.

1. Выберите &nbsp;:::image type="content" source="~/assets/images/tab-images/app-dropdown.png" alt-text="вкладку Канал ASPNET, загруженнуюAdd" border="true":::&nbsp; >  **в команду**, чтобы загрузить вкладку на Teams. Вкладка теперь доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Загруженная вкладка КАНАЛА ASPNET MVC" border="true":::

::: zone-end

## <a name="next-step"></a>Следующее действие

> [!div class="nextstepaction"]
> [Создать страницу контента](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>См. также

* [Teams вкладки](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Создать страницу удаления](~/tabs/how-to/create-tab-pages/removal-page.md)
