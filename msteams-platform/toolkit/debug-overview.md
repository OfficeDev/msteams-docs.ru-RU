---
title: Отладка приложения Teams
author: surbhigupta
description: В этом модуле вы узнаете, как отладить приложение Teams в Наборе средств Teams и ключевых функциях Набора средств Teams.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 624cad282e181ed56cbc3041f725b046ca061c72
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499162"
---
# <a name="debug-your-teams-app"></a>Отладка приложения Teams

Набор средств Teams помогает выполнять отладку и предварительный просмотр приложения Microsoft Teams. Отладка — это процесс проверки, обнаружения и исправления проблем или ошибок, чтобы обеспечить успешное выполнение программы в Teams.

::: zone pivot="visual-studio-code"

## <a name="debug-your-teams-app-for-visual-studio-code"></a>Отладка приложения Teams для Visual Studio Code

Набор средств Teams в Microsoft Visual Studio Code автоматизирует процесс отладки. Вы можете обнаружить ошибки и исправить их, а также просмотреть приложение Teams. Вы также можете настроить параметры отладки, чтобы создать вкладку или бот.

## <a name="debug-your-microsoft-teams-app-for-visual-studio-code"></a>Отладка приложения Microsoft Teams для Visual Studio Code

Набор средств Teams в Visual Studio Code автоматизирует процесс отладки. Вы можете обнаружить ошибки и исправить их, а также просмотреть приложение Teams. Вы также можете настроить параметры отладки, чтобы создать вкладку или бот.

В процессе отладки:

* Набор средств Teams автоматически запускает службы приложений, запускает отладчики и загрузку неопубликованного приложения Teams.
* Набор средств Teams проверяет предварительные требования во время фонового процесса отладки.
* Ваше приложение Teams доступно для предварительной версии в веб-клиенте Teams локально после отладки.
* Можно также настраивать параметры отладки для загрузки настроенного приложения, используя конечные точки бота, сертификат разработки или частичную отладку компонента.
* Microsoft Visual Studio Code позволяет выполнять отладку вкладки, бота, расширения сообщений и Функции Azure.

## <a name="key-debug-features-of-teams-toolkit"></a>Основные функции отладки набора средств Teams

Набор средств Teams поддерживает следующие функции отладки:

* [Начать отладку](#start-debugging)
* [Многоцелевая отладка](#multi-target-debugging)
* [Точки останова](#toggle-breakpoints)
* [Горячая перезагрузка](#hot-reload)
* [Остановить отладку](#stop-debugging)

Набор средств Teams выполняет фоновые функции во время процесса отладки, включая проверку предварительных условий, необходимых для отладки. Ход процесса проверки можно просмотреть в выходном канале Набора средств Teams. В процессе установки вы можете зарегистрировать и настроить приложение Teams.

### <a name="start-debugging"></a>Начало отладки

Чтобы начать отладку, можно нажать **клавишу F5** как одну операцию. Набор средств Teams начинает проверять предварительные требования, регистрирует приложение Azure AD, приложение Teams и регистрирует бот, запускает службы и браузер.

### <a name="multi-target-debugging"></a>Многоцелевая отладка

Для одновременной отладки вкладки, бота, расширения для сообщений и Функций Azure набор средств Teams использует функцию многоцелевой отладки.

### <a name="toggle-breakpoints"></a>Переключать точки останова

Вы можете переключать точки останова в исходном коде вкладок, ботов, расширений для сообщений и Функций Azure. Точки останова выполняются при взаимодействии с приложением Teams в веб-браузере. На следующем рисунке показана переключатель точки останова:

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/toggle-points.png" alt-text="Переключение точек останова" lightbox="../assets/images/teams-toolkit-v2/debug/toggle-points.png":::

### <a name="hot-reload"></a>Горячая перезагрузка

Вы можете обновлять и сохранять исходные коды вкладок, ботов, расширений сообщений и Функции Azure одновременно при отладке приложения Teams. Приложение перезагружается, а отладчик снова присоединится к языкам программирования.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hot-reload.png" alt-text="горячая перезагрузка для исходного кода" lightbox="../assets/images/teams-toolkit-v2/debug/hot-reload.png":::

### <a name="stop-debugging"></a>Остановить отладку

Завершив локальную отладку, можно на панели инструментов с плавающей отладкой выбрать stop **(SHIFT+F5)** или **[ALT] Disconnect (SHIFT+F5),** чтобы остановить все сеансы отладки и завершить задачи. На следующем рисунке показано действие "Остановить отладку":

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/stop-debug.png" alt-text="остановить отладку":::

## <a name="prepare-for-debug"></a>Подготовка к отладке

Следующие действия помогут вам подготовиться к отладке:

### <a name="sign-in-to-microsoft-365"></a>Вход в Microsoft 365

Если вы уже зарегистрировались в Microsoft 365, войдите в Microsoft 365. Дополнительные сведения см. в [статье о программе для разработчиков Microsoft 365](tools-prerequisites.md#microsoft-365-developer-program)

### <a name="toggle-breakpoints"></a>Переключать точки останова

Убедитесь, что вы можете переключать точки останова в исходных кодах вкладок, ботов, расширений сообщений и Функции Azure дополнительные сведения см. в разделе "Переключить точки останова["](#toggle-breakpoints).

## <a name="customize-debug-settings"></a>Настроить параметры отладки

Набор средств Teams снимает флажки с некоторых необходимых условий и позволяет настраивать параметры отладки для создания вашей вкладки или бота:

<br>

<details>
<summary><b>Использование конечной точки бота</b></summary>

1. В Visual Studio Code параметров необходимо снять флажок "Убедиться, что **Ngrok установлен и запущен (ngrok)"**.

1. Конфигурацию можно `siteEndpoint` задать для `.fx/configs/config.local.json` конечной точки.

```json
{
    "bot": {
        "siteEndpoint": "https://your-bot-tunneling-url"
    }
}

```

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/bot-endpoint.png" alt-text="Настройка конечной точки бота":::

</details>

<details>
<summary><b>Использование сертификата разработки</b></summary>

1. В Visual Studio Code параметрах необходимо снять флажок "Проверка доверия сертификата разработки **(devCert)"**.

1. Вы можете настроить путь `sslCertFile` `sslKeyFile` `.fx/configs/config.local.json` к файлу сертификата и путь к файлу ключа.

```json
{
    "frontend": {
        "sslCertFile": "",
        "sslKeyFile": ""
    }
}
```

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate-customize.png" alt-text="Настройка сертификата":::

</details>

<details>
<summary><b>Используйте скрипты запуска для запуска служб приложений</b></summary>

1. Для вкладки необходимо обновить скрипт в `dev:teamsfx` `tabs/package.json`.

1. Для расширения бота или сообщения необходимо обновить скрипт `dev:teamsfx` в `bot/package.json`.

1. Для Функции Azure необходимо обновить `dev:teamsfx` сценарий в скрипте `api/package.json` обновления TypeScript и в скрипте обновления `watch:teamsfx` TypeScript.

   > [!NOTE]
   > В настоящее время приложения вкладок, ботов, расширений для сообщений и порты Функций Azure не поддерживают пользовательскую настройку.

</details>

<details>
<summary><b>Добавление переменных среды</b></summary>

Вы можете добавить переменные среды в файл `.env.teamsfx.local` для вкладки, бота, расширения для сообщений и Функций Azure. Набор средств Teams загружает добавленные вами переменные среды при запуске служб во время локальной отладки.

 > [!NOTE]
 > После добавления новых переменных среды обязательно запустите новый сеанс локальной отладки, так как переменные среды не поддерживают горячую перезагрузку.

</details>

<details>
<summary><b>Отладка частичного компонента</b></summary>

Набор средств Teams использует многоцелевую отладку Visual Studio Code для одновременной отладки вкладки, бота, расширения для сообщений и Функций Azure. Можно обновить `.vscode/launch.json` и `.vscode/tasks.json` для отладки частичного компонента. Если вы хотите отладить только вкладку в проекте, содержащем вкладку и бот с Azure Functions, используйте следующие действия:

1. Комментирование **`Attach to Bot`** **`Attach to Backend`** и отладочная составная в `.vscode/launch.json`.

   ```json
   {
       "name": "Debug (Edge)",
        "configurations": [
           "Attach to Frontend (Edge)",
           // "Attach to Bot",
           // "Attach to Backend""
           ],
           "preLaunchTask": "Pre Debug Check & Start All",
           "presentation": {
               "group": "all",
               "order": 1
           },
           "stopAll": true

   }
   ```

2. Закомментируйте **`Start Backend`** и запустите бот из задачи "Запустить все" в файле .vscode/tasks.json.

   ```json
   {
                                           
       "label": "Start All",
       "dependsOn": [
           "Start Frontend",
             // "Start Backend",
             // "Start Bot"

         ]
              
   }
   ```

</details>

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [Локальная отладка приложений](debug-local.md)

::: zone-end

::: zone pivot="visual-studio"

## <a name="debug-your-teams-app-using-visual-studio"></a>Отладка приложения Teams с помощью Visual Studio

Набор средств Teams автоматизирует службы запуска приложений, инициирует отладку и загружает неопубликовающее приложение Teams. После отладки вы можете просмотреть приложение Teams в веб-клиенте Teams. Вы также можете настроить параметры отладки для использования конечных точек бота или переменных среды для загрузки настроенного приложения. Visual Studio позволяет выполнять отладку вкладки, бота и расширения сообщений. В процессе отладки Набор средств Teams поддерживает следующие функции отладки:

* Подготовка зависимостей приложений Teams
* Начало отладки
* Переключать точки останова
* Горячая перезагрузка
* Остановить отладку

## <a name="prerequisites"></a>Предварительные требования

| &nbsp; | Установка | Для использования... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 2022 версии 17.3 | Вы можете установить корпоративный выпуск Visual Studio и установить рабочую нагрузку ASP.NET и средства разработки Microsoft Teams. |
| &nbsp; | Набор средств Teams | Расширение Visual Studio, которое создает шаблон проекта для вашего приложения. Используйте последнюю версию. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams для взаимодействия в одном месте со всеми пользователями, с которыми вы работаете, с помощью приложений для чата, собраний и звонков. |
| &nbsp; | [Подготовка клиента Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) | Доступ к учетной записи Teams с соответствующими разрешениями на установку приложения. |
| &nbsp; | [Учетная запись разработчика Microsoft 365](/../concepts/build-and-test/prepare-your-o365-tenant) | Доступ к учетной записи Teams с соответствующими разрешениями на установку приложения. |
| &nbsp; | Средства Azure и [Интерфейс командной строки Microsoft Azure](/cli/azure/install-azure-cli) | Средства Azure для доступа к хранимых данных или развертывания облачной серверной части для приложения Teams в Azure. |
|&nbsp;  | **Необязательное** | &nbsp; |
|&nbsp; |[Ngrok](https://ngrok.com/) | Ngrok используется для пересылки внешних сообщений из Azure Bot Framework на локальный компьютер.|

## <a name="key-features-of-teams-toolkit"></a>Ключевые функции набора средств Teams

Вы увидите следующие ключевые функции Набора средств Teams, которые автоматизируют локальный процесс отладки приложения Teams:

### <a name="prepare-teams-app-dependencies"></a>Подготовка зависимостей приложений Teams

Набор средств Teams подготавливает зависимости локальной отладки и регистрирует приложение Teams в клиенте в вашей учетной записи. Для приложений Бота и расширения сообщений Набор средств Teams регистрирует и настраивает бот.

### <a name="start-debugging"></a>Начало отладки

Отладку можно выполнить с помощью одной операции, нажмите **клавишу F5** , чтобы начать отладку. Teams Toolkit создает код, запускает службы и запускает приложение в браузере.

### <a name="toggle-breakpoints"></a>Переключать точки останова

Вы можете переключать точки останова в исходных кодах вкладок, ботов, расширений сообщений и функций Azure. Точки останова выполняются при взаимодействии с приложением Teams в веб-браузере.
На следующем рисунке показаны переключаемые точки останова:

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png" alt-text="Локальные точки останова переключателя отладки" lightbox="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png":::

### <a name="hot-reload"></a>Горячая перезагрузка

Выберите **Горячая перезагрузка** применить изменения в приложении Teams, если вы хотите одновременно обновлять и сохранять исходные коды во время отладки.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload.png" alt-text="Выбор значка горячей перезагрузки":::

Выберите параметр Горячая перезагрузка **сохранить** файл из раскрывающегося списка, чтобы включить автоматическую горячую перезагрузку.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload-filesave.png" alt-text="Выбор горячей перезагрузки при сохранении файла":::
  
   > [!Tip]
   > Дополнительные сведения о функции Горячая перезагрузка Visual Studio во время отладки см. здесь<https://aka.ms/teamsfx-vs-hotreload>.

### <a name="stop-debugging"></a>Остановить отладку

Выберите **"Остановить отладку"** после завершения локальной отладки.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Stopdebug.png" alt-text="Значок остановки отладки":::

## <a name="customize-debug-settings"></a>Настроить параметры отладки

Вы можете настроить параметр отладки для приложения Teams, чтобы использовать конечные точки бота, и добавить переменные среды:

### <a name="use-your-bot-endpoint"></a>Использование конечной точки бота

Конфигурацию siteEndpoint можно задать в **файле .fx/configs/config.local.json** для конечной точки.

```
"bot": {
    "siteEndpoint": "https://baidu.com"
}
```

### <a name="add-environment-variables"></a>Добавление переменных среды

Вы можете добавить **environmentVariables для** **файла launchSettings.json** .

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-environment-variables.png" alt-text="Добавление пользовательских переменных среды":::

### <a name="launch-teams-app-as-a-web-app"></a>Запуск приложения Teams в качестве веб-приложения

Вы можете запустить приложение Teams как веб-приложение, а не запускать его в клиенте Teams.

1. Выберите **Properties** > **launchSettings.json** на Обозреватель решений панели в проекте.
1. Удалите **launchUrl** из файла.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png" alt-text="Запуск команд в качестве веб-приложения путем удаления launchurl" lightbox="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png":::

1. Щелкните решение правой **кнопкой** мыши и выберите **пункт "Свойства"**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png" alt-text="Щелкните решение правой кнопкой мыши и выберите свойства" lightbox="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png":::

1. Выберите **конфигурацию свойств конфигурации** >  в диалоговом окне.
1. Снимите **флажок "** Развернуть".
1. Нажмите кнопку **ОК**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png" alt-text="Снимите флажок развертывания в свойствах конфигурации" lightbox="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png":::

::: zone-end

## <a name="see-also"></a>См. также

* [Отладка фонового процесса](debug-background-process.md)
* [Подготовка облачных ресурсов с помощью набора средств Teams](provision.md)
* [Развертывание в облаке](deploy.md)
* [Предварительный просмотр и настройка манифеста приложения Teams](TeamsFx-preview-and-customize-app-manifest.md)
