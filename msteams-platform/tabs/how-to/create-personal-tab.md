---
title: Создание личной вкладки
author: laujan
description: Руководство по созданию личной вкладки с генератором Yeoman для Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 47ed3027f936366964871733e78c7a43851ffb99
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179869"
---
# <a name="create-a-personal-tab"></a>Создание личной вкладки

## <a name="create-a-custom-personal-tab"></a>Создание настраиваемой личной вкладки

Вы можете создать личную вкладку с помощью Node.js и генератора Yeoman, ASP.NET Core или ASP.NET Core MVC.

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

### <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator"></a>Создание настраиваемой личной вкладки Node.js и генератора Yeoman

> [!NOTE]
> В этой статье описаны действия, описанные в создании первого Microsoft Teams приложения [Wiki,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) найденного в репозитории Microsoft OfficeDev GitHub.

Вы можете создать настраиваемую личную вкладку с [помощью Teams Yeoman.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Приложение также загружается в Teams.

### <a name="prerequisites-for-teams-apps"></a>Необходимые условия для Teams приложений

Необходимо иметь представление о следующих предпосылках:

- Необходимо иметь клиента Office 365 и команду с **включенной возможностью загрузки настраиваемых приложений.** Дополнительные сведения см. в [Office 365 клиента.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

    > [!NOTE]
    > Если у вас нет Office 365 учетной записи, вы можете зарегистрироваться для бесплатной подписки через программу Office 365 разработчика. Подписка остается активной до тех пор, пока вы используете ее для текущей разработки. См. [добро пожаловать в программу Office 365 разработчика](/office/developer-program/microsoft-365-developer-program).

Кроме того, для этого проекта необходимо установить следующее в среде разработки:

- Любой редактор текста или IDE. Вы можете установить и [использовать Visual Studio Code](https://code.visualstudio.com/download) бесплатно.

- [Node.js/npm](https://nodejs.org/en/). Используйте последнюю версию LTS. Узел диспетчер пакетов (npm) устанавливается в системе с установкой Node.js.

- После успешной установки Node.js установите [пакеты Yeoman](https://yeoman.io/) и [gulp-cli,](https://www.npmjs.com/package/gulp-cli) введите следующее в командной подсказке:

    ```bash
    npm install yo gulp-cli --global
    ```

- Установите генератор Microsoft Teams приложений, введите следующее в командной подсказке:

    ```bash
    npm install generator-teams --global
    ```

### <a name="generate-your-project"></a>Создание проекта

**Создание проекта**

1. В командной подсказке создайте новый каталог для проекта вкладки.

1. Чтобы запустить генератор, перейдите в новый каталог и введите следующую команду:

    ```bash
    yo teams
    ```

1. Далее укайте ряд значений, используемых в файле **manifest.jsприложения:**

    ![Снимок экрана открытия генератора](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    **Как называется ваше решение?**

    Это имя проекта. Вы можете принять предложенное имя, выбрав ключ **Enter.**

    **Где следует разместить файлы?**

    В настоящее время вы находитесь в каталоге проектов. Выберите **Ввод**.

    **Название проекта Microsoft Teams приложения?**

    Это имя пакета приложений, которое будет использоваться в манифесте и описании приложения. Введите название или выберите **Ввод,** чтобы принять имя по умолчанию.

    **Ваше (компания) имя? (максимум 32 символа)**

    Имя вашей компании будет использоваться в манифесте приложения. Введите имя компании или выберите **Ввод,** чтобы принять имя по умолчанию.

    **Какую версию манифеста вы бы хотели использовать?**

    Выберите схему по умолчанию.

    **Быстрый строительный лес? (Y/n)**

    По умолчанию — да; введите **n,** чтобы ввести свой microsoft Partner Id.

    **Введите свой microsoft Partner Id, если он у вас есть? (Оставьте пустым, чтобы пропустить)**

    Это поле не требуется и должно использоваться только в том случае, если вы уже входите в [партнерской сети Майкрософт.](https://partner.microsoft.com)

    **Что нужно добавить в проект?**

    Выберите **&ast; () Вкладка**.

    **URL-адрес, на котором будет организовано это решение?**

    По умолчанию генератор предлагает URL-адрес веб-сайтов Azure. Вы тестируете приложение только локально, поэтому допустимый URL-адрес не требуется.

    **Хотите показать индикатор загрузки при загрузке приложения и вкладки?**

    Выберите **не** включать индикатор загрузки при загрузке приложения или вкладки. По умолчанию нет, введите **n**.

    **Вы хотите, чтобы личные приложения отображались без строки заголовков вкладок?**

    Не **следует** включать личные приложения, которые будут отрисовки без заглавной панели вкладок. По умолчанию нет, введите **n**.

    **Хотите включить тестовые рамки и начальные тесты? (y/N)**

    Выберите **не** включать тестовую базу для этого проекта. По умолчанию — да, введите **n**.

    **Хотите использовать приложения Azure Аналитика для телеметрии? (y/N)**

    Не **включать** приложения [Azure Аналитика.](/azure/azure-monitor/app/app-insights-overview) По умолчанию нет; введите **n**.

    **Имя вкладки по умолчанию (максимум 16 символов)?**

    Назови свою вкладку. Это имя вкладки используется во всем проекте в качестве компонента пути к файлу или URL-адресу.

    **Какую вкладку вы хотели бы создать?**

    Используйте клавиши стрелки для выбора **Личного (статического)**.

    **Требуется ли поддержка единого входа Azure AD для этой вкладки?**

    Не  включай поддержку для вкладки Azure AD с одним входом. По умолчанию — да, введите **n**.

    > [!IMPORTANT]
    > Компонент пути **yourDefaultTabNameTab** — это значение, которое вы ввели в генератор имени вкладки по умолчанию **плюс** слово **Tab**.
    >
    > Например: DefaultTabName: **MyTab**  >  **/MyTabTab/**

### <a name="add-a-personal-tab"></a>Добавление личной вкладки

**Чтобы добавить личную вкладку в это приложение, создайте страницу контента и обновим существующие файлы**

1. В редакторе кода создайте новый HTML-файлpersonal.htm **l** и добавьте следующую разметку:

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

1. Сохраните **personal.html** в **веб-папке** приложения в следующем расположении:

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

1. Откройте **manifest.jsиз** следующего расположения в редакторе кода:

    ```bash
    ./src/manifest/manifest.json/
    ```

1. Добавьте следующее в пустой массив `staticTabs` () и `staticTabs":[]` добавьте следующий объект JSON:

    ```json
    {
        "entityId": "personalTab",
        "name": "Personal Tab ",
        "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
        "websiteUrl": "https://{{HOSTNAME}}",
        "scopes": ["personal"]
    }
    ```

1. **Обновите компонент пути contentURL** **yourDefaultTabNameTab с** фактическим именем вкладки.

1. Сохраните обновленный **manifest.jsв** файле.

1. Чтобы предоставить страницу контента в IFrame, откройте **Tab.ts** в редакторе кода следующим образом:

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. Добавьте в список декораторов IFrame следующее:

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

1. Сохраните обновленный **файл Tab.ts.** Код вкладки завершен.

### <a name="build-and-run-your-application"></a>Сборка и запуск приложения

В командной подсказке откройте каталог проекта для выполнения следующих задач.

#### <a name="create-the-app-package"></a>Создание пакета приложений

Чтобы проверить вкладку в Teams, необходимо иметь пакет Teams. Это папка zip, которая содержит следующие необходимые файлы:

- Значок **полного цвета** размером 192 x 192 пикселя.
- Прозрачный **значок контура** размером 32 x 32 пикселя.
- Файл **manifest.js,** который указывает атрибуты приложения.

Пакет создается с помощью задачи gulp, которая проверяет manifest.jsфайл и создает папку zip в **каталоге ./package.** В командной подсказке введите следующую команду:

```bash
gulp manifest
```

#### <a name="build-your-application"></a>Сборка приложения

Команда сборки перекладывания решения в **папку ./dist.** Введите следующую команду в командной подсказке:

```bash
gulp build
```

#### <a name="run-your-application-in-localhost"></a>Запустите приложение в localhost

1. Запустите локальный веб-сервер, введя в командную подсказку следующее:

    ```bash
    gulp serve
    ```

1. Введите в браузере, замените имя вкладки и просмотр домашней страницы приложения, как показано на `http://localhost:3007/<yourDefaultAppNameTab>/` **<yourDefaultAppNameTab>** следующем изображении:

    ![Снимок экрана домашней страницы](~/assets/images/tab-images/homePage.png)

1. Чтобы просмотреть личную вкладку, перейдите к `http://localhost:3007/<yourDefaultAppNameTab>/personal.html` .

    >![Снимок экрана личной вкладки](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Создание безопасного туннеля на вкладке

Microsoft Teams является облачным продуктом и требует, чтобы содержимое вкладки было доступно в облаке с помощью конечных точек HTTPS. Teams не разрешает локальный хостинг. Необходимо либо опубликовать вкладку на общедоступный URL-адрес, либо использовать прокси-сервер, который предоставляет локальный порт URL-адресу, относящаяся к Интернету.

Чтобы проверить расширение вкладки, можно использовать [ngrok,](https://ngrok.com/docs)встроенный в это приложение. Ngrok — это средство обратного прокси-программного обеспечения, которое создает туннель к общедоступным конечным точкам HTTPS локального веб-сервера. Веб-точки сервера доступны во время текущего сеанса на компьютере. Когда компьютер выключен или заснул, служба перестает быть доступной.

В командной подсказке выйдите из localhost и введите следующее:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> После того как вкладка была загружена в Microsoft Teams **ngrok** и успешно сохранена, ее можно просмотреть в Teams до окончания сеанса туннеля.

### <a name="upload-your-application-to-teams"></a>Upload приложение для Teams

**Отправка приложения в Teams**

1. Перейдите Microsoft Teams. Если вы используете [веб-версию,](https://teams.microsoft.com) вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)
1. В левом нижнем углу выберите **Приложения.**
1. В левом нижнем углу **выберите Upload настраиваемого приложения.**
1. Перейдите в каталог проекта, просмотрите **папку ./package,** выберите папку zip и **откройте.**

    ![Добавление личной вкладки](../../assets/images/tab-images/addingpersonaltab.png)

1. Выберите **Добавить** в диалоговом окне всплывающее окно. Вкладка загружается в Teams.

    ![Загруженная личная вкладка](../../assets/images/tab-images/personaltabuploaded.png)

### <a name="view-your-personal-tab"></a>Просмотр личной вкладки

В панели навигации, расположенной слева Teams, выберите &#x25CF;&#x25CF;&#x25CF; и выберите приложение из списка.

# <a name="aspnet-core"></a>[ASP.NET Core](#tab/aspnetcore)

### <a name="create-a-custom-personal-tab-using-aspnet-core"></a>Создайте настраиваемую личную вкладку с ASP.NET Core

Вы можете создать настраиваемую личную вкладку с помощью C# и ASP.NET Core страниц Razor. [App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) также используется для окончательного развертывания манифеста приложения и развертывания вкладки Teams.

### <a name="prerequisites-for-personal-tab"></a>Необходимые условия для личной вкладки

Необходимо иметь представление о следующих предпосылках:

- Необходимо иметь клиента Office 365 и команду с **включенной возможностью загрузки настраиваемых приложений.** Дополнительные сведения см. в [Office 365 клиента.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

    > [!NOTE]
    > Если у вас нет Microsoft 365 учетной записи, вы можете зарегистрироваться на бесплатную подписку через [программу разработчиков Майкрософт](https://developer.microsoft.com/en-us/microsoft-365/dev-program). Подписка остается активной до тех пор, пока вы используете ее для текущей разработки.

- Используйте App Studio для импорта приложения для Teams. Чтобы установить App Studio, выберите **App Store** App в ![ нижнем левом углу приложения Teams и выберите ](~/assets/images/tab-images/storeApp.png) **App Studio.** После того как вы найдете плитку, выберите ее и выберите **Добавить** в всплывающее диалоговое окно, чтобы установить его.

Кроме того, для этого проекта необходимо установить следующее в среде разработки:

- Текущая версия Visual Studio IDE с установленной рабочей нагрузкой на межплатформу **.NET CORE.** Если у вас еще нет Visual Studio, вы можете [](https://visualstudio.microsoft.com/downloads) скачать и установить последнюю версию Microsoft Visual Studio Community бесплатно.

- Средство [обратного прокси ngrok.](https://ngrok.com) Используйте ngrok для создания туннеля для локальных конечных точек HTTPS на локальном веб-сервере, доступных для общего пользования. Вы можете [скачать ngrok](https://ngrok.com/download).

### <a name="get-the-source-code"></a>Получить исходный код

В командной подсказке создайте новый каталог для проекта вкладки. Для начала работы предоставляется простой проект. Клонировать репозиторий образца в новый каталог с помощью следующей команды:

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Кроме того, вы можете получить исходный код, скачав папку zip и извлекая файлы.

**Создание и запуск проекта вкладки**

1. После получения исходных кодов перейдите в Visual Studio и выберите **Открыть проект или решение.**
1. Перейдите в каталог приложений вкладок и откройте **PersonalTab.sln**.
1. Чтобы создать и запустить приложение, нажмите **кнопку F5** или выберите **начало** отладки из **меню отладки.**
1. В браузере перейдите к следующим URL-адресам, чтобы проверить правильно загруженные приложения:

    - `http://localhost:44325/`
    - `http://localhost:44325/personal`
    - `http://localhost:44325/privacy`
    - `http://localhost:44325/tou`

### <a name="review-the-source-code"></a>Просмотр исходных кодов

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан из пустого шаблона ASP.NET Core 2.2 веб-приложения с расширенным — настройка для контрольного окна **HTTPS,** выбранного при установке. Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей. Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому в метод добавляется среднее по статическим файлам с помощью `Configure()` следующего кода:

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

ASP.NET Core обрабатывает файлы под названием **Index** в качестве домашней страницы по умолчанию для сайта. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** отображается в качестве домашней страницы приложения.

#### <a name="appmanifest-folder"></a>Папка AppManifest

Эта папка содержит следующие необходимые файлы пакета приложений:

- Значок **полного цвета** размером 192 x 192 пикселя.
- Прозрачный **значок контура** размером 32 x 32 пикселя.
- Файл **manifest.js,** который указывает атрибуты приложения.

Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams. Microsoft Teams загружает указанное в манифесте, встраив его в <iframe и отрисовка его `contentUrl` \> на вкладке.

#### <a name="csproj"></a>.csproj

В окне Visual Studio обозревателя решений щелкните правой кнопкой мыши по проекту и выберите **Изменить Project Файл**. В конце файла вы увидите следующий код, который создает и обновляет папку zip при создании приложения:

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

### <a name="update-your-application-for-teams"></a>Обновление приложения для Teams

#### <a name="_layoutcshtml"></a>_Layout.cshtml

Чтобы вкладка отображалась в Teams, необходимо включить Microsoft Teams **клиента JavaScript** и включить вызов после загрузки `microsoftTeams.initialize()` страницы. Это то, как ваша вкладка и Teams приложение:

Перейдите в **общую** папку, **откройте _Layout.cshtml** и добавьте в раздел `<head>` теги следующее:

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

#### <a name="personaltabcshtml"></a>PersonalTab.cshtml

Откройте **PersonalTab.cshtml** и обновите встроенные `<script>` теги, `microsoftTeams.initialize()` позвонив.

Убедитесь, что вы сохраните **обновленный PersonalTab.cshtml**.

### <a name="establish-a-secure-tunnel-to-your-tab-for-teams"></a>Создание безопасного туннеля на вкладке для Teams

Microsoft Teams является облачным продуктом и требует, чтобы содержимое вкладки было доступно в облаке с помощью конечных точек HTTPS. Teams не разрешает локальный хостинг. Необходимо либо опубликовать вкладку на общедоступный URL-адрес, либо использовать прокси-сервер, который предоставляет локальный порт URL-адресу, относящаяся к Интернету.

Чтобы проверить вкладку, используйте [ngrok](https://ngrok.com/docs). Веб-точки сервера доступны во время запуска ngrok на компьютере. В бесплатной версии ngrok при закрытии ngrok URL-адреса отличаются при следующем запуске.

**Создание безопасного туннеля на вкладке**

1. По командной подсказке в корневом каталоге проекта запустите следующую команду:

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

    Ngrok прослушивает запросы из Интернета и передает их в приложение при работе с портом 44325. Он `https://y8rPrT2b.ngrok.io/` напоминает, где **y8rPrT2b** заменяется url-адресом https ngrok alpha-numeric HTTPS.

    Убедитесь, что командная подсказка будет запущена с помощью ngrok, и заметьте URL-адрес.

2. Убедитесь, что ngrok работает и работает должным образом, открыв браузер и перейдите на страницу контента через **URL-адрес** https ngrok, который был представлен в окне командной подсказки.

> [!TIP]
> Для выполнения действий, предусмотренных в этой статье, необходимо Visual Studio приложение в Visual Studio ngrok. Если для работы с приложением необходимо прекратить Visual Studio, продолжайте **работать с ngrok.** Он прослушивает и возобновляет маршрутизаку запроса приложения при его перезапуске в Visual Studio. Если вам нужно перезапустить службу ngrok, она возвращает новый URL-адрес, и вам необходимо обновить каждое место, которое использует этот URL-адрес.

#### <a name="run-your-application"></a>Запуск приложения

В Visual Studio нажмите **кнопку F5** или выберите **Пуск** отладки из меню отладки **приложения.**

### <a name="upload-your-tab-with-app-studio-for-teams"></a>Upload вкладку в App Studio для Teams

> [!NOTE]
> **App Studio** можно использовать для редактированияmanifest.js **файла** и отправки завершенного пакета в Teams. Вы также можете вручную **редактироватьmanifest.js.** Если это так, убедитесь, что вы создайте решение снова, чтобы создатьTab.zip **файл** для загрузки.

**Для загрузки вкладки в App Studio**

1. Перейдите Microsoft Teams. Если вы используете [веб-версию,](https://teams.microsoft.com)вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)

1. Перейдите **в App Studio и** выберите **вкладку Редактор Манифеста.**

1. Выберите **импорт существующего приложения в** **редакторе Манифеста,** чтобы приступить к обновлению пакета приложений для вкладки. Исходный код поставляется со своим частично полным манифестом. Имя вашего пакета приложений **tab.zip**. Он доступен по следующему пути:

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. Upload **tab.zip** **App Studio**.

#### <a name="update-your-app-package-with-manifest-editor"></a>Обновление пакета приложений с помощью редактора Manifest

После отправки пакета приложений в App Studio необходимо настроить его.

Выберите плитку для недавно импортируемой вкладки в правой области приветствия редактора Манифеста.

Слева от редактора Манифеста имеется список действий, а справа — список свойств, которые должны иметь значения для каждого из этих действий. Большая часть сведений предоставлена вашими **manifest.js,** но есть поля, которые необходимо обновить.

##### <a name="details-app-details"></a>Сведения: сведения о приложении

В разделе **Сведения о приложении:**

1. В **статье Идентификация** выберите **Создание** для создания нового удостоверения приложения для вашего приложения.

1. В **соответствии с сведениями разработчика** **обновите веб-сайт** **url-адресом https ngrok.**

    ![Обновленные URL-адреса приложений](../../assets/images/tab-images/appurls.png)

1. В **URL-адресах** приложений обнови заявление **конфиденциальности** и условия использования `https://<yourngrokurl>/privacy` **для** `https://<yourngrokurl>/tou`>.

##### <a name="capabilities-tabs"></a>Возможности: Вкладки

В разделе **Tabs:**

1. В **статье Добавить личную вкладку** выберите **Добавить**. Появляется всплывающее диалоговое окно.

1. Введите имя личной вкладки в **Name**.

1. Введите **ID объекта**.

1. Обновление **URL-адреса** контента `https://<yourngrokurl>/personalTab` с помощью .

    Оставьте **поле URL-адрес веб-сайта** пустым.

    ![Сведения о личной вкладке](../../assets/images/tab-images/personaltabdetails.png)

1. Нажмите **Сохранить**.

##### <a name="finish-domains-and-permissions"></a>Finish: Домены и разрешения

В разделе **Домены и**  разрешения домены с вкладок должны содержать URL-адрес ngrok без префикса `<yourngrokurl>.ngrok.io/` HTTPS.

###### <a name="finish-test-and-distribute"></a>Finish: Test and distribute

> [!IMPORTANT]
> Справа в **описании** см. следующее предупреждение:
>
> &#9888; массив **"validDomains" не может содержать сайт тоннелей...**
>
> Это предупреждение можно игнорировать при тестировании вкладки.

1. В разделе **Тест и распространение** выберите **Установите**.

1. В диалоговом окне всплывающее окно выберите **Добавить** и отображается вкладка.

    ![Личная вкладка ASPNET, загруженная](../../assets/images/tab-images/personaltabaspnetuploaded.png)

### <a name="view-your-personal-tab-in-teams"></a>Просмотр личной вкладки в Teams

1. В панели навигации, расположенной слева от Teams, выберите &#x25CF;&#x25CF;&#x25CF;. Показан список личных приложений.

1. Выберите вкладку из списка, чтобы просмотреть ее.

# <a name="aspnet-core-mvc"></a>[ASP.NET Core MVC](#tab/aspnetcoremvc)

### <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a>Создание настраиваемой личной вкладки с ASP.NET Core MVC

Вы можете создать настраиваемую личную вкладку с C# и ASP.NET Core MVC. [App Studio для Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) также используется для окончательного развертывания манифеста приложения и развертывания вкладки Teams.

### <a name="prerequisites-for-personal-tab-with-aspnet-core-mvc"></a>Необходимые условия для личной вкладки с ASP.NET Core MVC

- Необходимо иметь клиента Microsoft 365 и команду, настроенную с **включенной возможностью загрузки настраиваемых приложений.** Дополнительные сведения см. в [Office 365 клиента.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

    > [!NOTE]
    > Если у вас нет Microsoft 365 учетной записи, вы можете зарегистрироваться на бесплатную подписку через [программу разработчиков Майкрософт](https://developer.microsoft.com/en-us/microsoft-365/dev-program). Подписка остается активной до тех пор, пока вы используете ее для текущей разработки.

- Используйте App Studio для импорта приложения для Teams. Чтобы установить App Studio, выберите **App Store** App в ![ нижнем левом углу приложения Teams и выберите ](~/assets/images/tab-images/storeApp.png) **App Studio.** После того как вы найдете плитку, выберите ее и выберите **Добавить** в всплывающее диалоговое окно, чтобы установить его.

Кроме того, для этого проекта необходимо установить следующее в среде разработки:

- Текущая версия Visual Studio IDE с установленной рабочей нагрузкой на межплатформу **.NET CORE.** Если у вас еще нет Visual Studio, вы можете [](https://visualstudio.microsoft.com/downloads) скачать и установить последнюю версию Microsoft Visual Studio Community бесплатно.

- Средство [обратного прокси ngrok.](https://ngrok.com) Используйте ngrok для создания туннеля для локальных конечных точек HTTPS на локальном веб-сервере, доступных для общего пользования. Вы можете [скачать ngrok](https://ngrok.com/download).

### <a name="get-the-source-code"></a>Получить исходный код

В командной подсказке создайте новый каталог для проекта вкладки. Для начала работы предоставляется простой проект. Клонировать репозиторий образца в новый каталог с помощью следующей команды:

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Кроме того, вы можете получить исходный код, скачав папку zip и извлекая файлы.

**Создание и запуск проекта вкладки**

1. После того как у вас есть исходный код, перейдите Visual Studio и выберите **Открыть проект или решение**.
1. Перейдите к каталогу приложений вкладок и откройте **PersonalTabMVC.sln**.
1. Чтобы создать и запустить приложение, нажмите **кнопку F5** или выберите **начало** отладки из **меню отладки.**
1. В браузере перейдите к следующим URL-адресам, чтобы убедиться в правильной загрузке приложения:

    * `http://localhost:44335`
    * `http://localhost:44335/privacy`
    * `http://localhost:44335/tou`

### <a name="review-the-source-code"></a>Просмотр исходных кодов

#### <a name="startupcs"></a>Startup.cs

Этот проект был создан из пустого шаблона ASP.NET Core 2.2 веб-приложения с расширенным — настройка для контрольного окна **HTTPS,** выбранного при установке. Службы MVC регистрируются методом впрыскивания `ConfigureServices()` зависимостей. Кроме того, пустой шаблон не позволяет обслуживать статическое содержимое по умолчанию, поэтому в метод добавляется среднее по статическим файлам с помощью `Configure()` следующего кода:

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

* Значок **полного цвета** размером 192 x 192 пикселя.
* Прозрачный **значок контура** размером 32 x 32 пикселя.
* Файл **manifest.js,** который указывает атрибуты приложения.

Эти файлы необходимо использовать в пакете приложений для загрузки вкладки в Teams. Microsoft Teams загружает указанное в манифесте, встраив его в IFrame и отрисовка `contentUrl` его на вкладке.

#### <a name="csproj"></a>.csproj

В окне Visual Studio обозревателя решений щелкните правой кнопкой мыши по проекту и выберите **Изменить Project Файл**. В конце файла вы увидите следующий код, который создает и обновляет папку zip при создании приложения:

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

**PersonalTab.cs** представляет объект Сообщения и методы, которые вызваны из **PersonalTabController,** когда пользователь выбирает кнопку в **представлении PersonalTab.**

#### <a name="views"></a>Представления

Это различные представления в ASP.NET Core MVC:

* Главная: ASP.NET Core обрабатывает файлы под названием **Index** в качестве домашней страницы по умолчанию для сайта. Когда URL-адрес браузера указывает на корень сайта, **Index.cshtml** отображается в качестве домашней страницы приложения.

* Общий доступ. Частичная разметка **_Layout.cshtml** содержит общую структуру страниц приложения и общие визуальные элементы. Он также ссылается на Teams библиотеку.

#### <a name="controllers"></a>Контроллеры

Контроллеры используют свойство для динамической передачи значений `ViewBag` в Представления.

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

**Запуск ngrok и проверка страницы контента**

1. По командной подсказке в корневом каталоге проекта запустите следующую команду:

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

    Ngrok прослушивает запросы из Интернета и передает их в приложение при работе с портом 44325. Он `https://y8rPrT2b.ngrok.io/` напоминает, где **y8rPrT2b** заменяется url-адресом https ngrok alpha-numeric HTTPS.

    Убедитесь, что командная подсказка будет запущена с помощью ngrok, и заметьте URL-адрес.

1. Убедитесь, что ngrok работает и работает должным образом, открыв браузер и перейдите на страницу контента через **URL-адрес** https ngrok, который был представлен в окне командной подсказки.

> [!TIP]
> Для выполнения действий, предусмотренных в этой статье, необходимо Visual Studio приложение в Visual Studio ngrok. Если для работы с приложением необходимо прекратить Visual Studio, продолжайте **работать с ngrok.** Он прослушивает и возобновляет маршрутизаку запроса приложения при его перезапуске в Visual Studio. Если вам нужно перезапустить службу ngrok, она возвращает новый URL-адрес, и вам необходимо обновить каждое место, использующее этот URL-адрес.

#### <a name="run-your-application"></a>Запуск приложения

В Visual Studio нажмите **кнопку F5** или выберите **Пуск** отладки из меню отладки **приложения.**

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

---

## <a name="reorder-static-personal-tabs"></a>Reorder static personal tabs

Начиная с манифеста версии 1.7, разработчики могут изменить все вкладки в своем личном приложении. В частности, разработчик может  переместить вкладку чата бота, которая всегда по умолчанию, в первую позицию, в любом месте в личном загонах вкладки приложения. Объявлены два `entityId` зарезервированных ключевых слова вкладки, **беседы** и **около**.

Если вы создаете бот с личной **областью,** он появляется на первой позиции вкладки в личном приложении по умолчанию. Если вы хотите переместить его в другую позицию, необходимо добавить в манифест статичный объект вкладки с зарезервированным ключевым словом **, беседами.** Вкладка **беседы** отображается на веб-сайте или на рабочем столе в зависимости от того, где вы добавляете вкладку **беседы** в `staticTabs` массиве.

```json
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

## <a name="see-also"></a>См. также

* [Teams вкладки](~/tabs/what-are-tabs.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Создание вкладок бесед](~/tabs/how-to/conversational-tabs.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
