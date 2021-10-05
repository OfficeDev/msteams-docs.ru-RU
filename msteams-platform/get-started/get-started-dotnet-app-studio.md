---
title: 'Учебник . Создайте свое первое приложение с помощью C #'
description: Узнайте, как начать создание Microsoft Teams с помощью C# или .NET.
keywords: начало работы .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.localizationpriority: medium
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: dac0874850094c7f3bbe83f6cbc4f26209213410
ms.sourcegitcommit: 5bb12fd185a3bd6e308cc3a65b54341a5ae10af9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2021
ms.locfileid: "60116756"
---
# <a name="build-your-first-teams-app-using-c"></a>Создайте первое Teams с помощью C #

В этом руководстве вы узнаете, как создать свое первое приложение Microsoft Teams с помощью .NET или C#. Кроме того, вы проходите по шагам:

1. [Подготовка среды](#prepare-your-environment)
1. [Получить необходимые условия](#GetPrerequisites)
1. [Скачайте пример](#DownloadSample)
1. [Сборка и запуск примера](#BuildRun)
1. [Хост пример приложения](#hostsample)
1. [Обновление учетных данных для вашего хозяйского приложения](#updatecredentials)
1. [Настройка вкладки приложения](#configureapptab)

<a name="prepare-your-environment"></a>
[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Получить необходимые условия

Чтобы завершить этот учебник, необходимо установить следующие средства:

- [Установка Git](https://git-scm.com/downloads)
- [Установка Visual Studio](https://www.visualstudio.com/downloads/)

Вы можете установить бесплатное издание сообщества Visual Studio. Во время установки, если есть возможность добавить `git` в путь, выберите его. В окне терминала запустите следующую команду для проверки `git` установки:

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> Используйте подходящее окно терминала на платформе. В этих примерах используется Git Bash, но его можно запустить на большинстве платформ.

Откройте последнюю версию Visual Studio и установите все обновления.

Вы можете использовать одно и то же окно терминала для запуска команд в этом учебнике.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Скачайте пример

Вы можете начать работу с помощью простого [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) пример в C#. В окне терминала запустите следующую команду, чтобы клонировать репозиторий образца на компьютер:

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Вы можете [вилкой](https://help.github.com/articles/fork-a-repo/) это [репо изменить](https://github.com/OfficeDev/Microsoft-Teams-Samples) и сохранить изменения в GitHub.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Сборка и запуск примера

Вы можете создать и запустить образец после его клонирования. 

**Создание и запуск клонированной выборки**

1. Откройте файл решения **Microsoft.Teams. Samples.HelloWorld.sln** из каталога **Microsoft-Teams-Samples/samples/app-hello-world/csharp** образца.
1. Выберите **решение сборки** из меню **Сборка.**
1. Выберите **клавишу F5** или выберите **Пуск** отладки из меню **отладки** для запуска примера.

    При запуске приложения открывается окно браузера с корнем запущенного приложения. Вы можете перейти к следующим URL-адресам, чтобы убедиться, что все URL-адреса приложений загружаются:

    - `https://localhost:44327/`
    - `https://localhost:44327/hello`
    - `https://localhost:44327/first`
    - `https://localhost:44327/second`

    > [!Note]
    > Если вы получили `Could not find a part of the path … bin\roslyn\csc.exe` ошибку, обнови пакет командой `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` . Дополнительные сведения см. [в этом вопросе о переполнении стека.](https://stackoverflow.com/questions/32780315)

    <a name="hostsample"></a>
    ## <a name="deploy-your-sample-app"></a>Развертывание примера приложения

    Приложения в Microsoft Teams — это веб-приложения, которые предоставляют одну или несколько возможностей. Для Teams платформы для загрузки приложения ваше приложение должно быть доступно в Интернете. Для этого необходимо провести свое приложение. Вы можете либо бесплатно Microsoft Azure, либо создать туннель для локального процесса на компьютере с помощью `ngrok` . После хозяйского хозяйского приложения сделайте примечание корневого URL-адреса, например `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Tunnel ngrok

Для быстрого тестирования можно запустить приложение на компьютере и создать туннель к ней через веб-конечную точку. [`ngrok`](https://ngrok.com) это бесплатный инструмент, с помощью которого можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` . Вы можете [скачать и установить](https://ngrok.com/download) ngrok и добавить его в расположение в `PATH` вашем .

После установки откройте новое окно терминала и запустите следующую команду, `ngrok` чтобы создать туннель:

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` отвечает на запросы из Интернета и передает их в приложение, которое работает в порту 44327. 

**Проверка ответа**

1. В браузере перейдите по адресу `https://d0ac14a5.ngrok.io/hello`. Это загрузит страницу Hello приложения.
1. Вместо URL-адреса, упомянутого в шаге 1, используйте адрес переададки, отображающийся `ngrok` в сеансе консоли.
    > [!NOTE]
    > Если вы использовали другой порт в шаге [сборки](#build-and-run-the-sample) и запуска, убедитесь, что для установки туннеля используется один и тот же номер `ngrok` порта.
    > [!TIP]
    > Это хорошая идея для запуска `ngrok` в другом окне терминала. Это делается для того, чтобы не вмешиваться в работу `ngrok` приложения. Необходимо остановить, перестроить и повторно перезахоранить приложение. Сеанс `ngrok` предоставляет полезную информацию об отладки в этом окне.

    Приложение доступно только во время текущего сеанса на компьютере. Если машина отключена или заснул, служба больше недоступна. Помните об этом при совместном доступе приложения для тестирования другим пользователям. Если вам нужно перезапустить службу, приложение возвращает новый адрес, и необходимо обновить каждое расположение, использующее этот адрес. Платная версия `ngrok` не имеет этого ограничения.

### <a name="host-in-azure"></a>Хост в Azure

Microsoft Azure размещено приложение .NET на бесплатном уровне с помощью общей инфраструктуры. Этого достаточно для запуска `Hello World` примера. Дополнительные сведения см. в [создании новой бесплатной учетной записи Azure.](https://azure.microsoft.com/free/)

Visual Studio имеет встроенную поддержку развертывания приложений для различных поставщиков, в том числе Azure:

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

**Обновление пакета приложений**

> [!NOTE]
>  App Studio скоро будет отвягот. Настройка, распространение и управление Teams приложениями с помощью нового [портала разработчиков.](https://dev.teams.microsoft.com/)

# <a name="app-studio"></a>[App Studio](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[Портал разработчика](#tab/DP)

**Настройка пакета приложений на портале разработчиков в Teams**


1. Перейдите на **[портал Разработчик](https://dev.teams.microsoft.com/)**.

     <img width="600px" alt="Screenshot of TDP" src="~/assets/images/tdp/tdp_home_1.png"/>

1. Перейдите к **приложениям.**

    <img width="600px" alt="Open Apps" src="~/assets/images/tdp/screen2.png"/>

1. Выберите **Импорт существующего приложения.**

    <img width="600px" alt="Screenshot of import app in tdp" src="~/assets/images/tdp/screen3.png"/>

1. Выберите **Hello World** и выберите **Импорт**. Приложение **Hello World** импортируется на портале разработчиков. 

    Вы можете настроить приложение с помощью портала Teams разработчика. Манифест находится в статье Распределить. Манифест можно использовать для настройки возможностей, необходимых ресурсов и других важных атрибутов для приложения. Дополнительные сведения о настройке приложения с помощью портала разработчиков см. в Teams [портале разработчиков.](../concepts/build-and-test/teams-developer-portal.md)

    <img width="600px" alt="Screenshot of configure tdp" src="~/assets/images/tdp/Screen4.png"/>
---

<a name="updatecredentials"></a>
## <a name="update-the-credentials-for-your-hosted-app"></a>Обновление учетных данных для вашего хозяйского приложения

Пример приложения требует, чтобы переменные среды были задатки значениям, сохраненным в текстовом файле.

**Обновление учетных данных для вашего хозяйского приложения**

1. Откройте файл `appsettings.json`. 
1. Обновите **значение MicrosoftAppId** с помощью бот-ИД, сохраненного в текстовом файле. 
1. Обнови **microsoftAppPassword с** помощью сохраненного пароля бота.

    <img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

    После внесения этих изменений перестроим приложение. Если вы используете ngrok, запустите приложение локально, а если вы размещены в Azure, передискуй приложение.

<a name="configureapptab"></a>
## <a name="configure-the-app-tab"></a>Настройка вкладки приложения

После установки приложения в группы необходимо настроить его для отображения контента. 

**Настройка вкладки приложения**

1. Перейдите к каналу в команде, где установлен пример приложения, и выберите кнопку **"+",** чтобы добавить новую вкладку.
1. Выберите **Hello World** из списка Добавить **вкладку.** Отображается диалоговое окно конфигурации, которое позволяет выбрать вкладку для отображения в этом канале. 
1. Нажмите **Сохранить**. Вкладка `Hello World` загружается вкладками.

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Проверьте бот в Teams

Теперь вы можете протестировать бот в Teams. 

**Тестирование бота**

* Выберите канал в команде, в которой вы зарегистрировали приложение и `@your-bot-name` введите. Это называется **\@ упоминанием**. Бот отвечает на любое сообщение, которое вы отправляете.

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Тестирование расширения обмена сообщениями

**Тестирование расширения обмена сообщениями**
1. Выберите **...** ниже входного окна в представлении беседы. Отображается меню с приложением **"Hello World".** 
1. Выберите меню, будет отображаться набор случайных текстов. Вы можете выбрать один из случайных текстов, который вставляется в беседу.

    <img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. Выберите один из случайных текстов. Показана карта, отформатированная и готовая к отправке с помощью собственного сообщения.

    <img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

## <a name="see-also"></a>См. также

* [Обзор учебников](code-samples.md)
* [Создание бота беседы](first-app-bot.md)
* [Создание расширения для обмена сообщениями](first-message-extension.md)
* [Примеры кода](https://github.com/OfficeDev/Microsoft-Teams-Samples)
