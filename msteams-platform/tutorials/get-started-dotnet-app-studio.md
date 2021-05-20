---
title: 'Учебник - Создайте свое первое приложение с помощью C #'
description: Узнайте, как начать строить Microsoft Teams приложения с помощью C-NET или .NET.
keywords: начало работы .net c' csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: eaa37f1ccb7944ee18bb62ae47882dc4a715b165
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566889"
---
# <a name="create-your-first-teams-app-using-c"></a>Создайте свое первое Teams с помощью C #

Этот учебник поможет вам создать приложение Microsoft Teams с помощью C. Чтобы достичь этого, примите следующие меры:

* Подготовка среды
* Получить предпосылки
* Скачать образец
* Сборка и запуск примера
* Хозяин образца приложения
* Обновление учетных данных для размещенной приложения
* Настройка вкладки приложения

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Получить предпосылки

Чтобы завершить этот учебник, вам нужно установить следующие инструменты:

- [Установка Git](https://git-scm.com/downloads)
- [Установка Visual Studio](https://www.visualstudio.com/downloads/)

Вы можете установить бесплатное издание сообщества Visual Studio. Во время установки, если есть возможность добавить `git` в путь, выберите его. В окне терминала запустите следующую команду для проверки `git` установки:

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> Используйте подходящее окно терминала на вашей платформе. Эти примеры используют Git Bash, но могут быть запущены на большинстве платформ.

Откройте последнюю версию Visual Studio установите любые обновления.

Вы можете использовать то же окно терминала для запуска команд в этом учебнике.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Скачать образец

Вы можете начать работу с простого [Здравствуйте, Мир!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) образец в СЗ. В окне терминала запустите следующую команду клонировать репозиторий образца на компьютер:

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Вы можете [раскошелиться](https://help.github.com/articles/fork-a-repo/) [на это репо,](https://github.com/OfficeDev/Microsoft-Teams-Samples) чтобы изменить и сохранить ваши изменения, GitHub.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Сборка и запуск примера

После клонирования репо используйте Visual Studio для открытия файла решения **Microsoft.Teams. Примеры.HelloWorld.sln** **из каталога Microsoft-Teams-Samples/samples/app-hello-world/csharp.** Затем выберите **решение Build из** **меню Build.** Чтобы выбежать из образца, **нажмите F5** или выберите **Start Debugging** из **меню отладки.**

Когда приложение запускается, окно браузера открывается с корнем запущенного приложения. Вы можете перейти к следующим URL-адресам, чтобы убедиться, что все URL-адреса приложений загружаются:

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

<a name="HostSample"></a>

> [!Note]
> Если вы получили `Could not find a part of the path … bin\roslyn\csc.exe` ошибку, обновите пакет с `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` командой. Для получения дополнительной информации, [см. этот вопрос на стек переполнения](https://stackoverflow.com/questions/32780315).

## <a name="host-the-sample-app"></a>Хозяин образца приложения

Приложения в Microsoft Teams веб-приложений, которые обеспечивают одну или несколько возможностей. Для Teams платформы для загрузки приложения приложение должно быть доступно в Интернете. Для этого необходимо разместить приложение. Вы можете либо разместить его Microsoft Azure бесплатно, либо создать туннель для локального процесса на вашем компьютере с помощью `ngrok` . После размещения приложения обратите внимание на его корневой URL, например `https://yourteamsapp.ngrok.io` или `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Tunnel использование ngrok

Для быстрого тестирования можно запустить приложение на компьютере и создать туннель к нему через веб-конечную точку. [`ngrok`](https://ngrok.com) это бесплатный инструмент, с помощью которого вы можете получить веб-адрес, например `https://d0ac14a5.ngrok.io` . Вы можете [скачать и](https://ngrok.com/download) установить ngrok и добавить его в место в `PATH` вашем .

После установки `ngrok` откройте новое окно терминала и запустите следующую команду для создания туннеля:

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` прослушивает запросы из Интернета и маршрутит их в приложение, запущеное в порту 44327. Чтобы проверить, откройте браузер и перейдите `https://d0ac14a5.ngrok.io/hello` на загрузку привет страницы приложения. Вместо этого URL используйте адрес переголовки, отображаемый `ngrok` в сеансе консоли.

> [!NOTE]
> Если вы использовали другой порт в этапе [сборки и запуска,](#build-and-run-the-sample) убедитесь, что вы используете тот же номер порта для настройки `ngrok` туннеля.

> [!TIP]
> Это хорошая идея, чтобы `ngrok` работать в другом окне терминала. Это делается для того, `ngrok` чтобы не работать, не мешая приложению. Вы должны остановить, восстановить и повторно использовать приложение. Сеанс `ngrok` предоставляет полезную информацию об отладке в этом окне.

Приложение доступно только во время текущего сеанса на вашем компьютере. Если машина выключена или засыпает, услуга больше недоступна. Помните об этом, когда вы делитесь приложением для тестирования с другими пользователями. Если вам нужно перезапустить службу, приложение возвращает новый адрес, и вы должны обновить каждое место, которое использует этот адрес. Платная версия `ngrok` не имеет этого ограничения.

### <a name="host-in-azure"></a>Хозяин в Azure

Microsoft Azure размещает ваше приложение .NET на бесплатном уровне с использованием общей инфраструктуры. Этого достаточно для запуска `Hello World` выборки. Для получения дополнительной информации [можно создать новую бесплатную учетную запись Azure.](https://azure.microsoft.com/free/)

Visual Studio имеет встроенную поддержку развертывания приложений для различных поставщиков, включая Azure:

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>Обновление учетных данных для размещенной приложения

Пример приложения требует, чтобы переменные среды были установлены на значения, сохраненные в текстовом файле.

Откройте файл `appsettings.json`. Обновление значения **MicrosoftAppId с** помощью идентификатора бота, сохраненного в текстовом файле. Обновление **MicrosoftAppPassword с сохраненный** вами пароль бота.

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

После внесения этих изменений переутомить приложение. Если вы используете ngrok, запустите приложение локально, и если вы хостинг в Azure, передислоцировать приложение.

## <a name="configure-the-app-tab"></a>Настройка вкладки приложения

После установки приложения в команду необходимо настроить его для показов содержимого. Перейдите на канал в команде, где вы установили образец приложения и выберите **кнопку "Я",** чтобы добавить новую вкладку. Выберите **Hello World** из **списка вкладок Add.** Отображается диалоговое окно конфигурации, которое позволяет выбрать вкладку для отображения в этом канале. После выбора вкладки и выбора **Сохранить** `Hello World` вкладку загружается с вкладкой.

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Проверьте своего бота в Teams

Теперь вы можете протестировать бота в Teams. Выберите канал в команде, где вы зарегистрировали приложение и ввех. `@your-bot-name` Это называется **\@ упоминанием**. Бот отвечает на любое сообщение, которое вы отправляете.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Проверьте расширение обмена сообщениями

Чтобы проверить расширение обмена сообщениями, вы можете выбрать **...** Отображается меню **с приложением** «Здравствуйте, мир». При его выборе отображается набор случайных текстов. Вы можете выбрать один из случайных текста, который вставляется в ваш разговор.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Выберите один из случайных текстов. Отображается карта, отформатированная и готовая к отправке с вашим собственным сообщением.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
