---
title: 'Учебник . Создайте свое первое приложение с помощью C #'
description: Узнайте, как начать создание приложений Microsoft Teams с помощью C# или .NET.
keywords: начало работы .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 52af53d61215e41a885e21081a9f6148e81a0fdf
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020229"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a>Создание первого приложения Teams с C# или .NET

Этот учебник поможет вам создать приложение Microsoft Teams с C# или .NET. Чтобы достичь этого, примите следующие меры:

* Подготовка среды
* Получить необходимые условия
* Скачайте пример
* Сборка и запуск примера
* Хост пример приложения
* Обновление учетных данных для вашего хозяйского приложения
* Настройка вкладки приложения

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Получить необходимые условия

Чтобы завершить этот учебник, необходимо установить следующие средства:

- [Установка Git](https://git-scm.com/downloads)
- [Установка Visual Studio](https://www.visualstudio.com/downloads/)

Вы можете установить бесплатное издание Visual Studio. Во время установки, если есть возможность добавить `git` в путь, выберите его. В окне терминала запустите следующую команду для проверки `git` установки:

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
> Вы можете [раздвоить](https://help.github.com/articles/fork-a-repo/) [это репо,](https://github.com/OfficeDev/Microsoft-Teams-Samples) чтобы изменить и сохранить изменения в GitHub.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Сборка и запуск примера

После клонирования репо используйте Visual Studio для открытия файла решений **Microsoft.Teams.Samples.HelloWorld.sln** из каталога **Образцов/образцов Microsoft-Teams/samples/app-hello-world/csharp** образца. Затем выберите **решение сборки** из меню **Сборка.** Чтобы запустить пример, нажмите **кнопку F5 или** выберите **Пуск** отладки из **меню отладки.**

При запуске приложения открывается окно браузера с корнем запущенного приложения. Вы можете перейти к следующим URL-адресам, чтобы убедиться, что все URL-адреса приложений загружаются:

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second](https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> Если вы получили `Could not find a part of the path … bin\roslyn\csc.exe` ошибку, обнови пакет командой `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` . Дополнительные сведения см. [в этом вопросе о переполнении стека.](https://stackoverflow.com/questions/32780315)

## <a name="host-the-sample-app"></a>Хост пример приложения

Приложения в Microsoft Teams — это веб-приложения, которые предоставляют одну или несколько возможностей. Для загрузки приложения на платформе Teams ваше приложение должно быть доступно в Интернете. Для этого необходимо провести свое приложение. Вы можете бесплатно разработать его в Microsoft Azure или создать туннель для локального процесса на `ngrok` компьютере. После хозяйского приложения обратите внимание на его корневой URL-адрес, например `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Туннель с помощью ngrok

Для быстрого тестирования можно запустить приложение на компьютере и создать туннель к ней через веб-конечную точку. [`ngrok`](https://ngrok.com) это бесплатный инструмент, с помощью которого можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` . Вы можете [скачать и установить](https://ngrok.com/download) ngrok и добавить его в расположение в `PATH` вашем .

После установки откройте новое окно терминала и запустите следующую команду, `ngrok` чтобы создать туннель:

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` прослушивает запросы из Интернета и передает их в приложение, которое работает в порту 44327. Чтобы проверить, откройте браузер и перейдите к загрузке страницы `https://d0ac14a5.ngrok.io/hello` привета приложения. Вместо этого URL-адреса используйте адрес переададки, отображающийся в `ngrok` сеансе консоли.

> [!NOTE]
> Если вы использовали другой порт в шаге [сборки](#build-and-run-the-sample) и запуска, убедитесь, что для установки туннеля используется один и тот же номер `ngrok` порта.

> [!TIP]
> Это хорошая идея для запуска `ngrok` в другом окне терминала. Это делается для того, чтобы не вмешиваться в работу `ngrok` приложения. Необходимо остановить, перестроить и повторно перезахоранить приложение. Сеанс `ngrok` предоставляет полезную информацию об отладки в этом окне.

Приложение доступно только во время текущего сеанса на компьютере. Если машина отключена или заснул, служба больше недоступна. Помните об этом при совместном доступе приложения для тестирования другим пользователям. Если вам нужно перезапустить службу, приложение возвращает новый адрес, и необходимо обновить каждое расположение, использующее этот адрес. Платная версия `ngrok` не имеет этого ограничения.

### <a name="host-in-azure"></a>Хост в Azure

В Microsoft Azure размещено приложение .NET на бесплатном уровне с помощью общей инфраструктуры. Этого достаточно для запуска `Hello World` примера. Дополнительные сведения см. в [создании новой бесплатной учетной записи Azure.](https://azure.microsoft.com/free/)

Visual Studio имеет встроенную поддержку развертывания приложений для различных поставщиков, включая Azure.

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>Обновление учетных данных для вашего хозяйского приложения

Пример приложения требует, чтобы переменные среды были задатки значениям, сохраненным в текстовом файле.

Откройте файл `appsettings.json`. Обновите **значение MicrosoftAppId** с помощью бот-ИД, сохраненного в текстовом файле. Обнови **microsoftAppPassword с** помощью сохраненного пароля бота.

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

После внесения этих изменений перестроим приложение. Если вы используете ngrok, запустите приложение локально, а если вы размещены в Azure, передискуй приложение.

## <a name="configure-the-app-tab"></a>Настройка вкладки приложения

После установки приложения в команду необходимо настроить его для демонстрации контента. Перейдите к каналу в команде, где установлен пример приложения, и выберите кнопку **"+",** чтобы добавить новую вкладку. Выберите **Hello World** из списка Добавить **вкладку.** Отображается диалоговое окно конфигурации, которое позволяет выбрать вкладку для отображения в этом канале. После выбора вкладки и выбора **сохранить** `Hello World` вкладку загружается вкладка.

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Тестирование бота в Teams

Теперь вы можете протестировать бот в Teams. Выберите канал в команде, в которой вы зарегистрировали приложение и `@your-bot-name` введите. Это называется **\@ упоминанием**. Бот отвечает на любое сообщение, которое вы отправляете.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Тестирование расширения обмена сообщениями

Чтобы протестировать расширение обмена сообщениями, вы можете **выбрать ...** ниже входного окна в представлении беседы. Отображается меню с приложением **"Hello World".** При его выборе отображается набор случайных текстов. Вы можете выбрать один из случайных текстов, который вставляется в беседу.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Выберите один из случайных текстов. Показана карта, отформатированная и готовая к отправке с помощью собственного сообщения.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
