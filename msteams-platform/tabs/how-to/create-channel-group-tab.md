---
title: Создание вкладки канала или вкладки группы
author: laujan
description: Создайте пользовательский канал, вкладку группы с Node.js, ASP.NET Core ASP.NET Core MVC. Создание приложения, создание пакета, сборка и запуск приложения, туннель секретов, отправка в Teams
ms.localizationpriority: high
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 2ad44d0c43df7193106474fc3b6534d9ddde5bfc
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791666"
---
# <a name="create-a-channel-tab-or-group-tab"></a>Создание вкладки канала или вкладки группы

Вкладки каналов или групп доставляют содержимое в каналы и групповые чаты, что помогает создавать пространства для совместной работы вокруг выделенного веб-содержимого.

Убедитесь, что у вас есть все [необходимые условия для создания вкладки](~/tabs/how-to/tab-requirements.md) канала или группы.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>Создание настраиваемой вкладки канала или группы с помощью Node.js

1. В командной строке установите пакеты [Yeoman](https://yeoman.io/) и [gulp-cli](https://www.npmjs.com/package/gulp-cli), введя следующую команду после установки **Node.js**:

    ```cmd
    npm install yo gulp-cli --global
    ```

2. В командной строке установите генератор приложений Microsoft Teams, введя следующую команду:

    ```cmd
    npm install generator-teams --global
    ```

Ниже приведены этапы создания вкладки канала или группы:

* [Создайте свое приложение с вкладкой канала или группы](#generate-your-application-with-a-channel-or-group-tab)
* [Создание пакета приложения](#create-your-app-package)
* [Создайте и запустите свое приложение](#build-and-run-your-application)
* [Установите безопасный туннель к вашей вкладке](#establish-a-secure-tunnel-to-your-tab)
* [Загрузите приложение в Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Создание приложения с вкладкой канала или группы

1. В командной строке создайте новый каталог для вашей вкладки канала или группы.

1. Введите следующую команду в новом каталоге, чтобы запустить генератор приложений Microsoft Teams:

    ```cmd
    yo teams
    ```

1. Укажите значения для ряда вопросов, которые генератор приложений Microsoft Teams предложит обновить файл `manifest.json` :

    ![генератор, открывающий снимок экрана](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <details>
    <summary><b>Серия вопросов для обновления файла manifest.json</b></summary>

    * **Как называется решение?**

        Имя решения — это имя проекта. Вы можете принять предложенное имя, нажав **ВВОД**.

    * **Где следует разместить файлы?**

        Сейчас вы находитесь в каталоге проекта. Выберите **ВВОД**.

    * **Название вашего проекта приложения Microsoft Teams?**

        Название — это имя пакета приложения, которое используется в манифесте и описании приложения. Введите название или выберите **ВВОД** чтобы принять имя по умолчанию.

    * **Имя (компании)? (не более 32 символов)**

        Название вашей компании можно использовать в манифесте приложения. Введите название компании или выберите **ВВОД** чтобы принять имя по умолчанию.

    * **Какую версию манифеста вы хотите использовать?**

        Выберите схему по умолчанию.

    * **Быстрое формирование шаблонов (Y или N)**

        Значение по умолчанию — "да". Введите **n**, чтобы указать свой идентификатор партнера Microsoft.

    * **Введите идентификатор партнера Microsoft, если он у вас есть? (Оставьте пустым, чтобы пропустить)**

        Это поле не является обязательным и заполняется только в том случае, если вы уже являетесь участником [Microsoft Partner Network](https://partner.microsoft.com).

    * **Что вы хотите добавить в проект?**

        Выберите **( &ast; ) Вкладка**.

    * **URL-адрес для размещения этого решения?**

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

        С помощью клавиш со стрелками выберите вкладку **Настраиваемая**.

    * **Какие области вы собираетесь использовать для вкладки?**

        Вы можете выбрать команду или групповой чат.

    * **Требуется ли вам поддержка единого входа Microsoft Azure Active Directory (Azure AD) для вкладки?**

        Выберите **нет**, чтобы включить поддержку единого входа Microsoft Azure Active Directory (Azure AD) для вкладки. Значение по умолчанию — "да", введите **n**.

    * **Вы хотите, чтобы эта вкладка была доступна в SharePoint Online? (Y или N)**

        Введите **N**.

    </details>

> [!IMPORTANT]
> Компонент пути **yourDefaultTabNameTab**— это значение, которое вы ввели в генератор для **Имени вкладки по умолчанию** а также слово **Вкладка**. Например, `DefaultTabName` это **MyTab**, а затем **/MyTabTab/**.

<!--- TBD: this info seems removed from the main branch.
* A **full color icon** measuring 192 x 192 pixels.
* A **transparent outline icon** measuring 32 x 32 pixels.
* A `manifest.json` file that specifies the attributes of your app.
--->

### <a name="create-your-app-package"></a>Создание пакета приложения

У вас должен быть пакет приложения для создания и запуска приложения в Teams. Пакет приложения создается с помощью задачи gulp, которая проверяет файл `manifest.json` и создает zip-папку в каталоге `./package`. В командной строке введите следующую команду:

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>Создайте и запустите приложение

#### <a name="build-your-application"></a>Создание приложения

Введите следующую команду в командной строке, чтобы перенести решение в папку `./dist`:

```cmd
gulp build
```

#### <a name="run-your-application"></a>Запустите приложение

1. В командной строке введите следующую команду, чтобы запустить локальный веб-сервер:

    ```bash
    gulp serve
    ```

1. В браузере ведите `http://localhost:3007/<yourDefaultAppNameTab>/` для просмотра домашней страницы приложения.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Вкладка по умолчанию":::

1. Чтобы просмотреть страницу конфигурации вкладки, перейдите в `http://localhost:3007/<yourDefaultAppNameTab>/config.html`.

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="Страница конфигурации вкладки":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установите безопасный туннель к вашей вкладке

Чтобы установить безопасный туннель к своей вкладке, выйдите из локального хоста и введите следующую команду:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> После того, как ваша вкладка загружена в Microsoft Teams через **ngrok** и успешно сохранена, вы можете просматривать ее в Teams до завершения сеанса туннеля. При перезапуске сеанса ngrok необходимо обновить приложение с новым URL-адресом.

### <a name="upload-your-application-to-teams"></a>Загрузите свое приложение в Teams

1. Перейдите в Teams и выберите **Приложения**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::.
1. Выберите **Управление приложениями** > **Отправка приложения** > **Отправка пользовательского приложения**.
1. Перейдите в каталог проекта, в папку **./package** выберите папку zip пакета приложения и нажмите **Открыть**.

    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="Загруженная вкладка канала":::

1. В диалоговом окне выберите **Добавить**. Вкладка загружена в Teams.

    > [!NOTE]
    > Если в диалоговом окне не отображается **Добавить**, удалите следующий код из манифеста zip-папки пакета приложения. Снова добавьте папку в zip-архив и отправьте ее в Teams.
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. Следуйте указаниям по добавлению вкладки. Существует диалоговое окно настраиваемой конфигурации для канала или вкладки группы.
1. Выберите **Сохранить** и вкладка будет добавлена на панель вкладок канала.

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="Вкладка канала загружена":::

    Теперь вы успешно создали и добавили вкладку канала или группы в Teams.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>Создание настраиваемой вкладки канала или группы с помощью ASP.NET Core

1. В командной строке создайте новый каталог для вашего проекта вкладок.

1. Клонируйте образец репозитория в новый каталог, используя следующую команду, или загрузите [исходный код](https://github.com/OfficeDev/Microsoft-Teams-Samples) и извлеките файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже приведены этапы создания вкладки канала или группы:

* [Создайте свое приложение с вкладкой канала или группы](#generate-your-application-with-a-channel-or-group-tab-1)
* [Установите безопасный туннель к вашей вкладке](#establish-a-secure-tunnel-to-your-tab-1)
* [Обновите приложение](#update-your-application)
* [Создайте и запустите свое приложение](#build-and-run-your-application-1)
* [Обновите пакет приложения с помощью портала разработчика](#update-your-app-package-with-developer-portal)
* [Просмотрите приложение в Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Создание приложения с вкладкой канала или группы

1. Откройте Visual Studio и выберите **Открыть проект или решение**.

1. Перейдите в папку **Microsoft-Teams-Samples** > **samples** > **tab-channel-group** > **razor-csharp** и откройте **channelGroupTab.sln**.

1. В Visual Studio выберите **F5** или **Начать отладку** в меню **Отладка** вашего приложения, чтобы проверить, правильно ли загружено приложение. В браузере перейдите по следующим URL-адресам:

    * `https://localhost:3978/`
    * `https://localhost:3978/privacy`
    * `https://localhost:3978/tou`

<details>
<summary><b>Просмотреть исходный код</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан на основе пустого шаблона веб-приложения ASP.NET Core 3.1 с установленным флажком **Дополнительно * Настроить для HTTPS** при установке. Службы MVC регистрируются с помощью метода `ConfigureServices()` инфраструктуры внедрения зависимостей Кроме того, пустой шаблон по умолчанию не позволяет обслуживать статическое содержимое, поэтому промежуточное ПО для статических файлов добавляется в метод `Configure()` с помощью следующего кода:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc(options => options.EnableEndpointRouting = false);
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

#### <a name="tabcs"></a>Tab.cs

Этот файл C# содержит метод, который вызывается из **Tab.cshtml** во время настройки.

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложения:

* **Полноцветный значок** размером 192 x 192 пикселя.
* **Прозрачный контурный значок** размером 32 x 32 пикселя.
* Файл `manifest.json`, определяющий атрибуты приложения.

Эти файлы нужно заархивировать в пакете приложения для использования при загрузке вкладки в Teams. Когда пользователь решает добавить или обновить вкладку, Teams загружает указанный `configurationUrl` в манифесте объект, внедряет его в IFrame и отрисовывает на вкладке.

#### <a name="csproj"></a>.csproj

В окне обозревателя решений Visual Studio щелкните правой кнопкой мыши проект и выберите **Редактировать файл проекта**. В конце файла вы видите следующий код, который создает и обновляет вашу zip-папку при сборке приложения:

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

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установите безопасный туннель к вашей вкладке

В командной строке в корневом каталоге проекта выполните следующую команду, чтобы установить безопасный туннель на вкладку:

```cmd
ngrok http 3978 --host-header=localhost
```

Убедитесь, что командная строка с ngrok запущена и запишите URL-адрес.

### <a name="update-your-application"></a>Обновите приложение

1. Откройте обозреватель решений Visual Studio, перейдите в папку **Страницы** > **Общие**, откройте **_Layout.cshtml** и добавьте следующее <head> в раздел тегов:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.2.0/js/MicrosoftTeams.min.js" 
      integrity="sha384yBjE++eHeBPzIg+IKl9OHFqMbSdrzY2S/LW3qeitc5vqXewEYRWegByWzBN/chRh" 
      crossorigin="anonymous" >
    </script>
    ```

    > [!IMPORTANT]
    > Не копируйте и не вставляйте URL-адреса `<script src="...">` с этой страницы, так как они не представляют собой последнюю версию. Чтобы получить последнюю версию SDK, всегда переходите к [ API JavaScript для Microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js).

1. Вставьте вызов `microsoftTeams.app.initialize();` в тег `script`.

1. В Visual Studio Обозреватель решений перейдите в папку **Pages** и откройте **Файл Tab.cshtml**.

    В **Файле Tab.cshtml** приложение предоставляет пользователю два варианта отображения вкладки с красным или серым значком. Кнопка **"Выбрать серый"** или **"Выбрать красный"** активирует `saveGray()` или `saveRed()` , соответственно, задает `pages.config.setValidityState(true)`и включает **сохранить** на странице конфигурации. Этот код сообщает Teams, что вы выполнили настройку требований и можете продолжить установку. Параметры `pages.config.setConfig` заданы. Наконец, `saveEvent.notifySuccess()` вызывается, чтобы указать, что URL-адрес содержимого успешно разрешен.

1. Обновите значения `websiteUrl` и `contentUrl` в каждой функции с помощью URL-адреса ngrok HTTPS на вкладке.

    Теперь ваш код должен включать следующее: **y8rCgT2b** с заменой на URL-адрес ngrok:

    ```javascript
        
        let saveGray = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl: ""
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl: ""
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. Сохраните обновленный **Tab.cshtml**.

### <a name="build-and-run-your-application"></a>Создайте и запустите приложение

1. В Visual Studio выберите **F5** или выберите **Начать отладку** из меню **Отладка**.

1. Убедитесь, что **ngrok** работает правильно, открыв браузер и открыв страницу содержимого по URL-адресу HTTPS ngrok, который был указан в окне командной команды.

    > [!TIP]
    > Для выполнения действий, которые предоставляются в этой статье, необходимо запускать как приложение в Visual Studio, так и ngrok. Если вам нужно остановить запуск приложения в Visual Studio для работы с приложением, **не отключайте ngrok**. Он прослушивает и возобновляет маршрутизировать запрос приложения при перезапуске в Visual Studio. Если вам нужно перезапустить службу ngrok, она возвращает новый URL-адрес и вам нужно обновить приложение с помощью нового URL-адреса.

<!--- TBD: This note seems to be removed from main. Commenting it for now.
> [!NOTE]
> App Studio can be used to edit your `manifest.json` file and upload the completed package to Teams. You can also manually edit the `manifest.json` file. If you do, ensure that you build the solution again to create the `tab.zip` file to upload.
--->

### <a name="update-your-app-package-with-developer-portal"></a>Обновите пакет приложения с помощью портала разработчика

1. Перейдите в Teams. Если вы используете [веб-версию](https://teams.microsoft.com), вы можете проверить код интерфейсной части с помощью [средств для разработчиков](~/tabs/how-to/developer-tools.md).

1. Перейдите на [**Портал разработчика**](https://dev.teams.microsoft.com/home).

1. Откройте **Приложения** и выберите **Импорт приложений**.

   <!--- TBD: This steps seems to be removed from main now so commenting it for now.

   Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest. The name of your app package is `tab.zip`. It is available from the following path:
   --->

1. Имя пакета приложения — `tab.zip`. Он доступен по следующему пути:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Выберите `tab.zip` и откройте его на портале разработчика.

1. По умолчанию **Идентификатор приложения** создается и заполняется в разделе **Основная информация**.

1. Добавьте краткое и подробное описание для своего приложения в **Описания**.

1. В разделе **Информация для разработчиков** добавьте необходимые данные, а в разделе **Веб-сайт (это должен быть действительный URL-адрес HTTPS)** укажите URL-адрес HTTPS ngrok.

1. В **URL-адресах приложений** измените политику конфиденциальности на `https://<yourngrokurl>/privacy` и условия использования на `https://<yourngrokurl>/tou` и сохраните.

1. В **разделе Функции приложения** выберите **Группирование и приложение канала**. Обновите **URL-адрес конфигурации** с помощью `https://<yourngrokurl>/tab` и выберите для вкладки **Область**.

1. Нажмите кнопку **Сохранить**.

1. В разделе "Домены" домены из ваших вкладок должны содержать ваш URL-адрес ngrok без префикса HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Предварительный просмотр приложения в Teams

1. Выберите **Предварительный просмотр в Teams** на панели инструментов портала разработчика. Портал разработчика сообщит вам, что ваше приложение успешно загружено. **Страница добавления** отображается для вашего приложения в Teams.

1. Выберите **Добавить в команду**, чтобы настроить вкладку в команде. Настройте вкладку и выберите **Сохранить**. Теперь вкладка доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Загруженная вкладка канала ASPNET":::

    Теперь вы успешно создали и добавили вкладку канала или группы в Teams.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>Создание настраиваемой вкладки канала или группы с помощью ASP.NET Core MVC

1. В командной строке создайте новый каталог для вашего проекта вкладок.

1. Клонируйте образец репозитория в новый каталог, используя следующую команду, или загрузите [исходный код](https://github.com/OfficeDev/Microsoft-Teams-Samples) и извлеките файлы:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Ниже приведены этапы создания вкладки канала или группы:

* [Создайте свое приложение с вкладкой канала или группы](#generate-your-application-with-a-channel-or-group-tab-2)
* [Установите безопасный туннель к вашей вкладке](#establish-a-secure-tunnel-to-your-tab-2)
* [Обновите приложение](#update-your-application-1)
* [Создайте и запустите свое приложение](#build-and-run-your-application-2)
* [Обновите пакет приложения с помощью портала разработчика](#update-your-app-package-with-developer-portal-1)
* [Просмотрите приложение в Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Создание приложения с вкладкой канала или группы

1. Откройте Visual Studio и выберите **Открыть проект или решение**.

1. Перейдите в папку **Microsoft-Teams-Samples** > **samples** > **tab-channel-group** > **mvc-csharp** и откройте **ChannelGroupTabMVC.sln**.

1. В Visual Studio выберите **F5** или **Начать отладку** в меню **Отладка** вашего приложения, чтобы проверить, правильно ли загружено приложение. В браузере перейдите по следующим URL-адресам:

    * `https://localhost:3978/`
    * `https://localhost:3978/privacy`
    * `https://localhost:3978/tou`

<details>
<summary><b>Просмотреть исходный код</b></summary>

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан на основе пустого шаблона веб-приложения ASP.NET Core 3.1 с установленным флажком **Дополнительно — настроить для HTTPS** при установке. Службы MVC регистрируются с помощью метода `ConfigureServices()` инфраструктуры внедрения зависимостей Кроме того, пустой шаблон по умолчанию не позволяет обслуживать статическое содержимое, поэтому промежуточное ПО для статических файлов добавляется в метод `Configure()` с помощью следующего кода:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc(options => options.EnableEndpointRouting = false);
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

Эти файлы нужно заархивировать в пакете приложения для использования при загрузке вкладки в Teams.

#### <a name="csproj"></a>.csproj

В окне обозревателя решений Visual Studio щелкните правой кнопкой мыши проект и выберите **Редактировать файл проекта**. В конце файла вы увидите следующий код, который создает и обновляет zip-папку при сборке приложения:

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

**ChannelGroup.cs** представляет объект сообщения и методы, которые можно вызывать из контроллеров во время настройки.

#### <a name="views"></a>Представления

Это различные представления в ASP.NET Core MVC:

* Домашняя страница: ASP.NET Core рассматривает файлы с именем **Index** как домашнюю страницу сайта по умолчанию. Если URL-адрес браузера указывает на корень сайта, **файл Index.cshtml** может отображаться в качестве домашней страницы приложения.

* Общий. Разметка частичного представления **_Layout.cshtml** содержит общую структуру страницы приложения и общие визуальные элементы, которые также ссылались на библиотеку Teams.

#### <a name="controllers"></a>Контроллеры

Контроллеры используют свойство `ViewBag` для динамической передачи значений представлениям.

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Установите безопасный туннель к вашей вкладке

В командной строке в корневом каталоге проекта выполните следующую команду, чтобы установить безопасный туннель на вкладку:

```cmd
ngrok http 3978 --host-header=localhost
```

Убедитесь, что командная строка с ngrok запущена и запишите URL-адрес.

### <a name="update-your-application"></a>Обновите приложение

1. Откройте обозреватель решений Visual Studio, перейдите в папку **Представления** > **Общие**, откройте **_Layout.cshtml** и добавьте следующее <head> в раздел тегов:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.2.0/js/MicrosoftTeams.min.js" 
      integrity="sha384yBjE++eHeBPzIg+IKl9OHFqMbSdrzY2S/LW3qeitc5vqXewEYRWegByWzBN/chRh" 
      crossorigin="anonymous" >
    </script>
    ```

    > [!IMPORTANT]
    > Не копируйте и не вставляйте URL-адреса `<script src="...">` с этой страницы, так как они не представляют собой последнюю версию. Чтобы получить последнюю версию SDK, всегда переходите к [ API JavaScript для Microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js).

1. Вставьте вызов `microsoftTeams.app.initialize();` в тег `script`.

1. В Visual Studio Обозреватель решений перейдите в папку **Tab** и откройте **файл Tab.cshtml**.

    В **Файле Tab.cshtml** приложение предоставляет пользователю два варианта отображения вкладки с красным или серым значком. Кнопка **"Выбрать серый"** или **"Выбрать красный"** активирует `saveGray()` или `saveRed()` , соответственно, задает `pages.config.setValidityState(true)`и включает **сохранить** на странице конфигурации. Этот код сообщает Teams, что вы выполнили настройку требований и можете продолжить установку. Параметры `pages.config.setConfig` заданы. Наконец, `saveEvent.notifySuccess()` вызывается, чтобы указать, что URL-адрес содержимого успешно разрешен.

1. Обновите значения `websiteUrl` и `contentUrl` в каждой функции с помощью URL-адреса ngrok HTTPS на вкладке.

    Теперь ваш код должен включать следующее: **y8rCgT2b** с заменой на URL-адрес ngrok:

    ```javascript

        let saveGray = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl:""
                });
                saveEvent.notifySuccess();
            });
        }
    
        let saveRed = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl:""
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. Обязательно сохраните обновленный **Tab.cshtml**.

### <a name="build-and-run-your-application"></a>Создайте и запустите приложение

1. В Visual Studio выберите **F5** или выберите **Начать отладку** из меню **Отладка**.

1. Убедитесь, что **ngrok** работает правильно, открыв браузер и открыв страницу содержимого по URL-адресу HTTPS ngrok, который был указан в окне командной команды.

    > [!TIP]
    > Для выполнения действий, которые предоставляются в этой статье, необходимо запускать как приложение в Visual Studio, так и ngrok. Если вам нужно остановить запуск приложения в Visual Studio для работы с приложением, **не отключайте ngrok**. Он прослушивает и возобновляет маршрутизировать запрос приложения при перезапуске в Visual Studio. Если вам нужно перезапустить службу ngrok, она возвращает новый URL-адрес и вам нужно обновить приложение с помощью нового URL-адреса.

### <a name="update-your-app-package-with-developer-portal"></a>Обновите пакет приложения с помощью портала разработчика

1. Перейдите в Teams. Если вы используете [веб-версию](https://teams.microsoft.com), вы можете проверить код интерфейсной части с помощью [средств для разработчиков](~/tabs/how-to/developer-tools.md).

1. Перейдите на [**Портал разработчика**](https://dev.teams.microsoft.com/home).

1. Откройте **Приложения** и выберите **Импорт приложений**.

1. Имя пакета приложения — **tab.zip**. Он доступен по следующему пути:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Выберите **tab.zip** и откройте его на портале разработчиков.

1. По умолчанию **Идентификатор приложения** создается и заполняется в разделе **Основная информация**.

1. Добавьте краткое и подробное описание для своего приложения в **Описания**.

1. В разделе **Информация для разработчиков** добавьте необходимые данные, а в разделе **Веб-сайт (это должен быть действительный URL-адрес HTTPS)** укажите URL-адрес HTTPS ngrok.

1. В **URL-адресах приложений** измените политику конфиденциальности на `https://<yourngrokurl>/privacy` и условия использования на `https://<yourngrokurl>/tou` и сохраните.

1. В **разделе Функции приложения** выберите **Группирование и приложение канала**. Обновите **URL-адрес конфигурации** с помощью `https://<yourngrokurl>/tab` и выберите для вкладки **Область**.

1. Нажмите кнопку **Сохранить**.

1. В разделе "Домены" домены из ваших вкладок должны содержать ваш URL-адрес ngrok без префикса HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Предварительный просмотр приложения в Teams

1. Выберите **Предварительный просмотр в Teams** на панели инструментов портала разработчика. Портал разработчика сообщит вам, что ваше приложение успешно загружено. **Страница добавления** отображается для вашего приложения в Teams.

1. Выберите **Добавить в команду**, чтобы настроить вкладку в команде. Настройте вкладку и выберите **Сохранить**. Теперь вкладка доступна в Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Загруженная вкладка канала ASPNET MVC":::

    Теперь вы успешно создали и добавили вкладку канала или группы в Teams.

::: zone-end

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создать страницу контента](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Создать страницу удаления](~/tabs/how-to/create-tab-pages/removal-page.md)
* [Добавление страницы SharePoint в виде вкладки в Teams](https://support.microsoft.com/en-us/office/add-a-sharepoint-page-list-or-document-library-as-a-tab-in-teams-131edef1-455f-4c67-a8ce-efa2ebf25f0b)
