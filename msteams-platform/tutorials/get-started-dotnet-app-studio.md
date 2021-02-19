---
title: 'Учебник . Создайте свое первое приложение с помощью C #'
description: Узнайте, как начать создание приложений Microsoft Teams с помощью C# или .NET.
keywords: начало работы .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 29cc4e0f434bf9ece9c6073af84627acc048b628
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294756"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a>Создайте свое первое приложение Teams с помощью C# или .NET

Этот учебник поможет вам создать приложение Microsoft Teams с помощью C# или .NET.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Получить необходимые условия

Чтобы завершить этот учебник, необходимо получить следующие средства:

- [Установка Git](https://git-scm.com/downloads)
- [Установка Visual Studio](https://www.visualstudio.com/downloads/). Вы можете установить бесплатное издание сообщества.

При установке, если есть возможность добавить в `git` PATH, выберите его.

В окне терминала запустите следующую команду для проверки `git` установки:

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> Используйте подходящее окно терминала на платформе. В этих примерах используется Bash, но они работают на большинстве платформ.

Обязательно запустите последнюю версию Visual Studio и установите все обновления.

Вы можете использовать одно и то же окно терминала для запуска команд в этом учебнике.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Скачайте пример

Вы можете начать работу с помощью простого [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) пример в C#. В окне терминала запустите следующую команду, чтобы клонировать репозиторий образца на локальной машине:

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Вы можете [вилка](https://help.github.com/articles/fork-a-repo/) этого [репо](https://github.com/OfficeDev/Microsoft-Teams-Samples) изменить и сохранить изменения в GitHub для справки.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Сборка и запуск примера

После клонирования репо используйте Visual Studio файл решения из каталога `Microsoft.Teams.Samples.HelloWorld.sln` **Microsoft-Teams-Samples/samples/app-hello-world/csharp** и выберите из `Build Solution` `Build` меню. Для запуска примерного `F5` нажатия или `Start Debugging` выбора `Debug` меню.

При запуске приложения открывается окно браузера с корнем запущенного приложения. Вы можете перейти к следующим URL-адресам, чтобы убедиться, что все URL-адреса приложений загружаются:

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second]https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> Если вы получили `Could not find a part of the path … bin\roslyn\csc.exe` ошибку, обнови пакет командой `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` . Дополнительные сведения см. [в этом вопросе на сайте StackOverflow.](https://stackoverflow.com/questions/32780315)

## <a name="host-the-sample-app"></a>Хост пример приложения

Приложения в Microsoft Teams — это веб-приложения, которые предоставляют одну или несколько возможностей. Для загрузки приложения на платформе Teams ваше приложение должно быть доступно из Интернета. Чтобы сделать ваше приложение доступно из Интернета, необходимо провести ваше приложение. Вы можете бесплатно разработать его в Microsoft Azure или создать туннель для локального процесса на компьютере `ngrok` разработки. Когда вы закончите размещение приложения, обратите внимание на его корневой URL-адрес. Например, `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net`.

### <a name="tunnel-using-ngrok"></a>Туннель с помощью ngrok

Для быстрого тестирования можно запустить приложение на локальной машине и создать туннель к ней через веб-конечную точку. [ngrok](https://ngrok.com) — это бесплатный инструмент, с помощью которого можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` . Вы можете [скачать и установить](https://ngrok.com/download) ngrok. Убедитесь, что вы добавляете его в расположение в вашем `PATH` .

После установки ngrok откройте новое окно терминала и запустите следующую команду, чтобы создать туннель:

```bash
ngrok http 44327 -host-header=localhost:44327
```

В примере используется порт 44327, чтобы указать его.

Ngrok прослушивает запросы из Интернета и передает их в приложение, которое работает в порту 44327. Чтобы проверить, откройте браузер и перейдите к загрузке страницы `https://d0ac14a5.ngrok.io/hello` привета приложения. Вместо этого URL-адреса используйте адрес переададки, отображающийся ngrok в сеансе консоли.

> [!NOTE]
> Если вы использовали другой порт в шаге [сборки](#build-and-run-the-sample) и запуска, убедитесь, что для установки туннеля используется один и тот же номер `ngrok` порта.

> [!TIP]
> Это хорошая идея для запуска `ngrok` в другом окне терминала. Это делается для того, чтобы не мешать запуску ngrok без вмешиваться в работу приложения, которое необходимо остановить, восстановить и повторно перезагрузить. Сеанс `ngrok` предоставляет полезную информацию об отладки в этом окне.

Приложение доступно только во время текущего сеанса на компьютере разработки. Если машина отключена или заснул, служба больше недоступна. Помните об этом при совместном доступе приложения для тестирования другим пользователям. Если вам нужно перезапустить службу, приложение возвращает новый адрес, и необходимо обновить каждое расположение, использующее этот адрес. Платная версия ngrok не имеет этого ограничения.

### <a name="host-in-azure"></a>Хост в Azure

В Microsoft Azure размещено приложение .NET на бесплатном уровне с помощью общей инфраструктуры. Этого достаточно для запуска `Hello World` примера. Дополнительные сведения см. [в создании новой бесплатной учетной записи.](https://azure.microsoft.com/free/)

Visual Studio имеет встроенную поддержку развертывания приложений для различных поставщиков, в том числе Azure.

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>Обновление учетных данных для вашего хозяйского приложения

Пример приложения требует, чтобы следующие переменные среды были задаты значениям, которые вы сделали ранее.

Откройте файл appsettings.jsфайле. Обновите *значение MicrosoftAppId* с помощью бот-ИД, сохраненного ранее. Обнови *microsoftAppPassword* с помощью сохраненного ранее пароля Bot.

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

После внесения этих изменений перестроим приложение. Если вы используете ngrok, запустите приложение локально, а если вы размещены в Azure, передиските приложение.

## <a name="configure-the-app-tab"></a>Настройка вкладки приложения

После установки приложения в команду необходимо настроить его для демонстрации контента. Перейдите к каналу в команде, где установлен пример приложения, и нажмите кнопку **"+",** чтобы добавить новую вкладку. Затем можно выбрать `Hello World` из списка **Добавить вкладку.** Затем вам будет представлен диалоговое окно конфигурации. Этот диалоговое окно позволит выбрать вкладку, которая будет отображаться в этом канале. После выбора вкладки и нажатия на нее можно увидеть вкладку, `Save` `Hello World` загруженную выбранной вкладками.

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Тестирование бота в Teams

Теперь вы можете взаимодействовать с ботом в Teams. Выберите канал в команде, в которой вы зарегистрировали приложение и `@your-bot-name` введите. Это называется **\@ упоминанием**. Любое сообщение, отправленное боту, будет отправлено вам в качестве ответа.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Тестирование расширения обмена сообщениями

Чтобы проверить расширение обмена сообщениями, вы можете щелкнуть три точки ниже входного окна в представлении беседы. В нем всплывет меню с приложением **"Hello World".** При нажатии кнопки отображается куча случайных текстов. Вы можете выбрать любой из них, и он вставляется в ваш разговор.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Выберите один из случайных текстов, и в нижней части будет отформатирована карточка, готовая к отправке с собственным сообщением.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
