---
title: 'Учебник: создание первого приложения с помощью C #'
description: Узнайте, как начать создание приложений Microsoft Teams с помощью C#/.NET.
keywords: начало работы .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c28c4d00c375b8e37f82c343eec2c5405ae0c1c8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037041"
---
# <a name="create-your-first-microsoft-teams-app-using-c"></a>Создание первого приложения Microsoft Teams с помощью C #

Это руководство поможет вам начать создание приложения Microsoft Teams с помощью C# на .NET.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Получить необходимые условия

Чтобы выполнить это руководство, необходимо получить следующие средства:

- [Установка Git](https://git-scm.com/downloads)
- [Установите Visual Studio](https://www.visualstudio.com/downloads/). Вы можете установить бесплатный выпуск сообщества.

Если во время установки вы видите возможность добавления в `git` path, выберите этот вариант. Это будет удобно.

Проверьте `git` установку, вынеся в окне терминала следующую информацию:
> [!NOTE]
> Используйте окно терминала, наиболее удобное для вашей платформы. В этих примерах используется Bash, но он будет работать на большинстве платформ.

```bash
$ git --version
git version 2.17.1.windows.2

```

Обязательно запустите последнюю версию Visual Studio и установите все обновления, если они показаны.

Вы можете продолжать использовать это окно терминала для запуска команд, которые следуют в этом руководстве.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Скачать пример

Мы предоставили простой [привет, мир!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) пример на C#, чтобы начать работу. В окне терминала запустите следующую команду, чтобы клонировать образец репозитория на локальный компьютер:

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> Вы можете [раздвоить](https://help.github.com/articles/fork-a-repo/) этот репозитарий, если вы хотите изменить и проверить изменения в GitHub для дальнейшей ссылки. [](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Сборка и запуск примера

После клонирования репо используйте Visual Studio, чтобы открыть файл решения из корневого каталога примера и щелкнуть `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` в `Build` меню. Пример можно запустить, нажав `F5` или выбрав `Start Debugging` пункт `Debug` меню.

При запуске приложения откроется окно браузера с корнем запущенного приложения. Чтобы убедиться, что загружаются все URL-адреса приложений, можно перейти по следующим URL-адресам:

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> Если вы получили сообщение об ошибке `Could not find a part of the path … bin\roslyn\csc.exe` , попробуйте обновить пакет с помощью `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` команды. Дополнительные сведения см. в этом вопросе на сайте [StackOverflow.](https://stackoverflow.com/questions/32780315)

## <a name="host-the-sample-app"></a>Хост-приложение для примера

Помните, что приложения в Microsoft Teams — это веб-приложения, которые предлагают одну или несколько возможностей. Чтобы платформа Teams загружала ваше приложение, ваше приложение должно быть доступно из Интернета. Чтобы ваше приложение было доступно из Интернета, необходимо провести его. Вы можете либо бесплатно провести его в Microsoft Azure, либо создать туннель для локального процесса на компьютере `ngrok` разработки. Когда вы закончите размещение приложения, заметьте его корневой URL-адрес. Он будет выглядеть так: `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Туннель с помощью ngrok

Для быстрого тестирования вы можете запустить приложение на локальном компьютере и создать для него туннель через веб-конечную точку. [ngrok](https://ngrok.com) — это бесплатное средство, которое позволяет сделать именно это. С помощью ngrok можно получить веб-адрес, например `https://d0ac14a5.ngrok.io` (этот URL-адрес является лишь примером). Вы можете [скачать и установить](https://ngrok.com/download) ngrok для своей среды. Убедитесь, что вы добавили его в расположение в вашем `PATH` .

После установки можно открыть новое окно терминала и выполнить следующую команду, чтобы создать туннель. В примере используется порт 3333, поэтому не забудьте указать его здесь.

```bash
ngrok http 3333 -host-header=localhost:3333
```

Ngrok будет прослушивать запросы из Интернета и маршрутит их в ваше приложение, запущенного через порт 3333. Вы можете проверить, открыв браузер и загрузив страницу `https://d0ac14a5.ngrok.io/hello` hello приложения. Вместо этого URL-адреса используйте адрес переадрикии, отображающийся ngrok в сеансе консоли.

> [!NOTE]
> Если вы использовали другой порт [](#build-and-run-the-sample) в сборке и на шаге выше, убедитесь, что для настройки туннеля используется один и тот же `ngrok` номер порта.
> [!TIP]
> Лучше всего запустить его в другом окне терминала, чтобы оно не помешать приложению, которое впоследствии может потребоваться остановить, перестроить `ngrok` и повторно запустить. Сеанс `ngrok` возвращает полезные сведения об отладки в этом окне.

Приложение будет доступно только во время текущего сеанса на вашем компьютере разработки. Если компьютер выключен или переводится в спящий режим, служба будет недоступна. Помните об этом при совместном использовании приложения для тестирования другими пользователями. Если вам нужно перезапустить службу, она возвратит новый адрес, и вам придется обновить все места, где используется этот адрес. Платная версия Ngrok не имеет этого ограничения.

### <a name="host-in-azure"></a>Хост в Azure

Microsoft Azure позволяет вам проводить приложение .NET на бесплатном уровне с помощью общей инфраструктуры. Этого будет достаточно для запуска этого `Hello World` примера. Дополнительные [сведения см.](https://azure.microsoft.com/free/) в создании новой бесплатной учетной записи.

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

Чтобы протестировать расширение обмена сообщениями, можно щелкнуть три точки под полем ввода в представлении беседы. В меню будет всплывающее меню с приложением **"Hello World".** Щелкнув его, вы увидите множество случайных текстов. Вы можете выбрать любой из них, и он будет вставлен в беседу.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Выберите один из случайных текстов, и внизу отформатированная карточка будет готова к отправке с собственным сообщением.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
