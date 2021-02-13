---
title: 'Учебник: создание первого приложения с помощью C #'
description: Узнайте, как начать создание приложений Microsoft Teams с помощью C# или .NET.
keywords: начало работы .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: b37a8d555117e38383504dc99d82d564439a3ebf
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231531"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a>Создание первого приложения Teams на C# или .NET

Это руководство поможет вам создать приложение Microsoft Teams на C# или .NET.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Получить необходимые условия

Чтобы выполнить это руководство, необходимо получить следующие средства:

- [Установка Git](https://git-scm.com/downloads)
- [Установите Visual Studio](https://www.visualstudio.com/downloads/). Вы можете установить бесплатный выпуск сообщества.

При установке, если есть возможность добавить `git` путь, выберите его.

В окне терминала запустите следующую команду, чтобы проверить `git` установку:

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> Используйте подходящее окно терминала на своей платформе. В этих примерах используется Bash, но он работает на большинстве платформ.

Обязательно запустите последнюю версию Visual Studio и установите все обновления.

Для запуска команд в этом руководстве можно использовать то же окно терминала.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Скачать пример

Вы можете начать работу с простым [hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) пример на C#. В окне терминала запустите следующую команду, чтобы клонировать образец репозитория на локальный компьютер:

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> Вы можете [раздвоить](https://help.github.com/articles/fork-a-repo/) [этот репозитив,](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) чтобы изменить и сохранить изменения в GitHub для справки.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Сборка и запуск примера

После клонирования репо используйте Visual Studio, чтобы открыть файл решения из корневого каталога примера и выбрать его `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` из `Build` меню. Чтобы запустить пример `F5` нажатий или выбрать `Start Debugging` из `Debug` меню.

При запуске приложения откроется окно браузера с корнем запущенного приложения. Чтобы убедиться, что загружаются все URL-адреса приложений, можно перейти по следующим URL-адресам:

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second]https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> Если вы получили сообщение об `Could not find a part of the path … bin\roslyn\csc.exe` ошибке, обновим пакет с помощью `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` команды. Дополнительные сведения см. [в этом вопросе на сайте StackOverflow.](https://stackoverflow.com/questions/32780315)

## <a name="host-the-sample-app"></a>Хост-приложение для примера

Приложения в Microsoft Teams — это веб-приложения, которые предоставляют одну или несколько возможностей. Чтобы платформа Teams загружала ваше приложение, ваше приложение должно быть доступно из Интернета. Чтобы ваше приложение было доступно из Интернета, необходимо провести его. Вы можете либо бесплатно провести его в Microsoft Azure, либо создать туннель для локального процесса на компьютере `ngrok` разработки. После завершения размещения приложения обратите внимание на его корневой URL-адрес. Например, `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net`.

### <a name="tunnel-using-ngrok"></a>Туннель с помощью ngrok

Для быстрого тестирования можно запустить приложение на локальном компьютере и создать для него туннель через веб-конечную точку. [ngrok](https://ngrok.com) — это бесплатное средство, с помощью которого можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` . Вы можете [скачать и установить](https://ngrok.com/download) ngrok. Убедитесь, что вы добавили его в расположение в вашем `PATH` .

После установки ngrok откройте новое окно терминала и запустите следующую команду, чтобы создать туннель:

```bash
ngrok http 44327 -host-header=localhost:44327
```

В примере используется порт 44327, не забудьте указать его.

Ngrok прослушивает запросы из Интернета и маршрутит их в ваше приложение, запущенного на порту 44327. Чтобы проверить, откройте браузер и перейдите к загрузке страницы `https://d0ac14a5.ngrok.io/hello` hello приложения. Вместо этого URL-адреса используйте адрес переадрики, отображающийся ngrok в сеансе консоли.

> [!NOTE]
> Если вы использовали другой порт [](#build-and-run-the-sample) на этапе сборки и запуска, убедитесь, что для настройки туннеля используется тот же `ngrok` номер порта.

> [!TIP]
> Лучше всего запустить его в `ngrok` другом окне терминала. Это делается для того, чтобы ngrok не запускал приложение, которое необходимо остановить, перестроить и повторно запускать. Сеанс `ngrok` предоставляет полезные сведения об отладки в этом окне.

Приложение доступно только во время текущего сеанса на компьютере разработки. Если компьютер выключен или переводится в спящий режим, служба больше недоступна. Помните об этом, когда вы делитесь приложением для тестирования с другими пользователями. Если необходимо перезапустить службу, приложение возвращает новый адрес, и необходимо обновить все расположения, использующие этот адрес. Платная версия ngrok не имеет этого ограничения.

### <a name="host-in-azure"></a>Хост в Azure

В Microsoft Azure приложение .NET размещено на бесплатном уровне с использованием общей инфраструктуры. Этого достаточно для запуска `Hello World` примера. Дополнительные сведения см. [в создании новой бесплатной учетной записи.](https://azure.microsoft.com/free/)

Visual Studio имеет встроенную поддержку развертывания приложений для разных поставщиков, включая Azure.

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>Обновление учетных данных для вашего ведущего приложения

Пример приложения требует, чтобы для следующих переменных среды были установлены значения, которые вы ранее заметили.

Откройте файл appsettings.jsфайла. *Обновите значение MicrosoftAppId* с помощью сохраненного ранее ИД бота. *Обновив MicrosoftAppPassword с* помощью сохраненного ранее пароля бота.

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

После внесения этих изменений перестроение приложения. Если вы используете ngrok, запустите приложение локально, а если вы размещены в Azure, развяжите приложение еще раз.

## <a name="configure-the-app-tab"></a>Настройка вкладки приложения

После установки приложения в команде необходимо настроить его для показа содержимого. Перейдите на канал в команде, где установлен пример приложения, и нажмите кнопку **"+",** чтобы добавить новую вкладку. Затем можно выбрать `Hello World` в списке **"Добавить** вкладку". После этого вам будет представлено диалоговое окно конфигурации. Это диалоговое окно позволит выбрать вкладку, отображаемую в этом канале. Выбрав вкладку и щелкнув ее, вы увидите вкладку, загруженную `Save` `Hello World` выбранной вкладками.

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Тестирование бота в Teams

Теперь вы можете взаимодействовать с ботом в Teams. Выберите канал в команде, в которой вы зарегистрировали приложение, и введите `@your-bot-name` . Это называется **\@ упоминанием.** Все сообщения, отправляемые боту, будут отправлены вам в качестве ответа.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Проверка расширения обмена сообщениями

Чтобы протестировать расширение обмена сообщениями, можно щелкнуть три точки под полем ввода в представлении беседы. В меню будет всплывающее меню с приложением **"Hello World".** Щелкнув его, вы увидите множество случайных текстов. Вы можете выбрать любой из них и вставить его в беседу.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Выберите один из случайных текстов, и внизу отформатированная карточка будет готова к отправке с собственным сообщением.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
