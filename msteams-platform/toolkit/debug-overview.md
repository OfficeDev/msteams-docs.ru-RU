---
title: Отладка приложения Teams
author: surbhigupta
description: В этом модуле вы узнаете, как отлаживать приложение Teams в наборе средств Teams и основные функции набора средств Teams.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: db6e3b99ab737b7ea8cac393e6ee3e0830cd0acc
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791792"
---
# <a name="debug-your-teams-app"></a>Отладка приложения Teams

Набор средств Teams помогает выполнять отладку и предварительный просмотр приложения Microsoft Teams. Отладка — это процесс проверки, обнаружения и исправления проблем или ошибок, чтобы убедиться, что программа успешно работает в Teams.

::: zone pivot="visual-studio-code"

## <a name="debug-your-teams-app-for-visual-studio-code"></a>Отладка приложения Teams для Visual Studio Code

Набор средств Teams в Microsoft Visual Studio Code автоматизирует процесс отладки. Вы можете обнаруживать ошибки и исправлять их, а также просматривать приложение Teams. Вы также можете настроить параметры отладки для создания вкладки или бота.

## <a name="debug-your-microsoft-teams-app-for-visual-studio-code"></a>Отладка приложения Microsoft Teams для Visual Studio Code

Набор средств Teams в Visual Studio Code автоматизирует процесс отладки. Вы можете обнаруживать ошибки и исправлять их, а также просматривать приложение Teams. Вы также можете настроить параметры отладки для создания вкладки или бота.

В процессе отладки:

* Набор средств Teams автоматически запускает службы приложений, запускает отладчики и загружает неопубликованное приложение Teams.
* Набор средств Teams проверяет предварительные требования во время фонового процесса отладки.
* Приложение Teams доступно для предварительной версии в веб-клиенте Teams локально после отладки.
* Можно также настраивать параметры отладки для загрузки настроенного приложения, используя конечные точки бота, сертификат разработки или частичную отладку компонента.
* Microsoft Visual Studio Code позволяет выполнять отладку вкладки, бота, расширения сообщений и Функции Azure.

## <a name="key-debug-features-of-teams-toolkit"></a>Основные функции отладки набора средств Teams

Набор средств Teams поддерживает следующие функции отладки:

* [Начать отладку](#start-debugging)
* [Многоцелевая отладка](#multi-target-debugging)
* [Точки останова](#toggle-breakpoints)
* [Горячая перезагрузка](#hot-reload)
* [Остановить отладку](#stop-debugging)

Набор средств Teams выполняет фоновые функции во время отладки, включая проверку необходимых условий для отладки. Ход выполнения проверки можно просмотреть в выходном канале набора средств Teams. В процессе настройки можно зарегистрировать и настроить приложение Teams.

### <a name="start-debugging"></a>Начало отладки

Вы можете нажать **клавишу F5** в качестве одной операции, чтобы начать отладку. Набор средств Teams начинает проверять предварительные требования, регистрирует приложение Azure AD, приложение Teams и регистрирует бот, запускает службы и браузер.

### <a name="multi-target-debugging"></a>Многоцелевая отладка

Для одновременной отладки вкладки, бота, расширения для сообщений и Функций Azure набор средств Teams использует функцию многоцелевой отладки.

### <a name="toggle-breakpoints"></a>Переключать точки останова

Вы можете переключать точки останова в исходном коде вкладок, ботов, расширений для сообщений и Функций Azure. Точки останова выполняются при взаимодействии с приложением Teams в веб-браузере. На следующем рисунке показана точка останова:

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/toggle-points.png" alt-text="Переключение точек останова" lightbox="../assets/images/teams-toolkit-v2/debug/toggle-points.png":::

### <a name="hot-reload"></a>Горячая перезагрузка

Вы можете одновременно обновлять и сохранять исходные коды вкладок, бота, расширения сообщений и Функции Azure при отладке приложения Teams. Приложение перезагружается, а отладчик снова присоединится к языкам программирования.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hot-reload.png" alt-text="горячая перезагрузка для исходного кода" lightbox="../assets/images/teams-toolkit-v2/debug/hot-reload.png":::

### <a name="stop-debugging"></a>Остановить отладку

После завершения локальной отладки можно выбрать **Остановить (SHIFT+F5)** или **[ALT] Отключить (SHIFT+F5)** на плавающей панели инструментов отладки, чтобы остановить все сеансы отладки и завершить задачи. На следующем рисунке показано действие "Остановить отладку":

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/stop-debug.png" alt-text="остановить отладку":::

## <a name="prepare-for-debug"></a>Подготовка к отладке

Следующие действия помогут вам подготовиться к отладке.

### <a name="sign-in-to-microsoft-365"></a>Вход в Microsoft 365

Если вы уже зарегистрировались в Microsoft 365, войдите в Microsoft 365. Дополнительные сведения см. в [статье Программа для разработчиков Microsoft 365](tools-prerequisites.md#microsoft-365-developer-program).

### <a name="toggle-breakpoints"></a>Переключать точки останова

Убедитесь, что вы можете переключать точки останова в исходных кодах вкладок, ботов, расширений сообщений и Функции Azure дополнительные сведения см. в разделе [Переключение точек останова](#toggle-breakpoints).

## <a name="customize-debug-settings"></a>Настроить параметры отладки

Набор средств Teams позволяет настроить параметры отладки для создания вкладки или бота. Дополнительные сведения о полном списке настраиваемых параметров см. в [документации по параметрам отладки](https://aka.ms/teamsfx-debug-tasks).

### <a name="customize-scenarios"></a>Настройка сценариев

<br>

<details>

<summary><b>Пропустить проверки готовности</b></summary>

В `.fx/configs/tasks.json` разделе `"Validate & install prerequisites"` >  > `"args"``"prerequisites"`обновите проверки готовности, которые нужно пропустить.

  :::image type="content" source="../assets/images/teams-toolkit-v2/debug/skip-prerequisite-checks.png" alt-text="пропустить проверки готовности":::

</details>

<details>
<summary><b>Использование сертификата разработки</b></summary>

1. В `.fx/configs/tasks.json`снимите флажок `"devCert"` в разделе `"Validate & install prerequisites"``"prerequisites"` > `"args"` > .
1. Задайте "SSL_CRT_FILE" и "SSL_KEY_FILE" в `.env.teamsfx.local` качестве пути к файлу сертификата и пути к файлу ключа.

</details>

<details>
<summary><b>Настройка args установки npm</b></summary>

В `.fx/configs/tasks.json`задайте npmInstallArgs в разделе `"Install npm packages"`.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/customize-npm-install.png" alt-text="Установка пакета npm":::

</details>

<details>
<summary><b>Изменение портов</b></summary>

* Bot
  1. Выполните поиск `"3978"` по всему проекту и найдите внешние представления в `tasks.json`, `ngrok.yml` и `index.js`.
  1. Замените его своим портом.
     :::image type="content" source="../assets/images/teams-toolkit-v2/debug/modify-ports-bot.png" alt-text="Замена порта для бота":::
* Tab
  1. В `.fx/configs/tasks.json`найдите `"53000"`.
  1. Замените его своим портом.
     :::image type="content" source="../assets/images/teams-toolkit-v2/debug/modify-ports-tab.png" alt-text="Замена порта для вкладки":::

</details>

<details>
<summary><b>Использование собственного пакета приложения</b></summary>

В `.fx/configs/tasks.json`укажите `"appPackagePath"` `"Build & upload Teams manifest"` путь к пакету приложения.

  :::image type="content" source="../assets/images/teams-toolkit-v2/debug/app-package-path.png" alt-text="использовать собственный путь к пакету приложения":::

</details>

<details>
<summary><b>Использование собственного туннеля</b></summary>

1. В `.fx/configs/tasks.json` разделе `"Start Teams App Locally"`можно обновить `"Start Local tunnel"`.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-local-tunnel.png" alt-text="Использование собственного туннеля":::
1. Запустите собственную службу туннелирования, а затем обновите `"botMessagingEndpoint"` собственную конечную точку сообщения в `.fx/configs/tasks.json` в разделе `"Set up bot"`.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/set-up-bot.png" alt-text="Обновление конечной точки обмена сообщениями":::

</details>

<details>

<summary><b>Добавление переменных среды</b></summary>

Вы можете добавить переменные среды в файл `.env.teamsfx.local` для вкладки, бота, расширения для сообщений и Функций Azure. Набор средств Teams загружает добавленные вами переменные среды при запуске служб во время локальной отладки.

 > [!NOTE]
 > Не забудьте запустить новую локальную отладку после добавления новых переменных среды, так как переменные среды не поддерживают горячую перезагрузку.

</details>

<details>
<summary><b>Отладка частичного компонента</b></summary>

Набор средств Teams использует многоцелевую отладку Visual Studio Code для одновременной отладки вкладки, бота, расширения для сообщений и Функций Azure. Можно обновить `.vscode/launch.json` и `.vscode/tasks.json` для отладки частичного компонента. Если вы хотите отладить только вкладку в проекте, содержащем вкладку и бот с Azure Functions, используйте следующие действия:

1. Обновление `"Attach to Bot"` и `"Attach to Backend"` из отладочного соединения в `.vscode/launch.json`.

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

2. Обновите `"Start Backend"` задачу "Запустить все" и `"Start Bot"` "Запустить все" в vscode/tasks.json.

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

Набор средств Teams автоматизирует службы запуска приложений, инициирует отладку и загружает приложение Teams на стороне. После отладки вы можете просмотреть приложение Teams в веб-клиенте Teams. Вы также можете настроить параметры отладки, чтобы использовать конечные точки бота или переменные среды для загрузки настроенного приложения. Visual Studio позволяет выполнять отладку вкладки, бота и расширения сообщений. В процессе отладки Набор средств Teams поддерживает следующие функции отладки:

* Подготовка зависимостей приложений Teams
* Начало отладки
* Переключать точки останова
* Горячая перезагрузка
* Остановить отладку

## <a name="prerequisites"></a>Предварительные требования

| &nbsp; | Установка | Для использования... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 2022 версии 17.3 | Вы можете установить корпоративный выпуск Visual Studio, а также рабочую нагрузку "ASP.NET" и средства разработки Microsoft Teams. |
| &nbsp; | Набор средств Teams | Расширение Visual Studio, создающее шаблон проекта для приложения. Используйте последнюю версию. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams для взаимодействия в одном месте со всеми пользователями, с которыми вы работаете, с помощью приложений для чата, собраний и звонков. |
| &nbsp; | [Подготовка клиента Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md) | Доступ к учетной записи Teams с соответствующими разрешениями для установки приложения. |
| &nbsp; | [Учетная запись разработчика Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md) | Доступ к учетной записи Teams с соответствующими разрешениями для установки приложения. |
| &nbsp; | Средства Azure и [Microsoft Azure CLI](/cli/azure/install-azure-cli) | Средства Azure для доступа к хранимым данным или для развертывания облачной серверной части приложения Teams в Azure. |
|&nbsp;  | **Необязательное** | &nbsp; |
|&nbsp; |[Ngrok](https://ngrok.com/) | Ngrok используется для пересылки внешних сообщений из Azure Bot Framework на локальный компьютер.|

## <a name="key-features-of-teams-toolkit"></a>Ключевые функции набора средств Teams

Вы можете увидеть следующие ключевые функции Набора средств Teams, которые автоматизируют локальный процесс отладки приложения Teams:

### <a name="prepare-teams-app-dependencies"></a>Подготовка зависимостей приложений Teams

Набор средств Teams подготавливает локальные зависимости отладки и регистрирует приложение Teams в клиенте в вашей учетной записи. Для приложений bot и message extension набор средств Teams будет регистрировать и настраивать бота.

### <a name="start-debugging"></a>Начало отладки

Вы можете выполнить отладку с помощью одной операции, нажав **клавишу F5** , чтобы начать отладку. Набор средств Teams создает код, запускает службы и запускает приложение в браузере.

### <a name="toggle-breakpoints"></a>Переключать точки останова

Точки останова можно переключать в исходных кодах вкладок, ботов, расширений сообщений и функций Azure. Точки останова выполняются при взаимодействии с приложением Teams в веб-браузере.
На следующем рисунке показаны переключаемые точки останова:

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png" alt-text="Переключение точек останова локальной отладки" lightbox="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png":::

### <a name="hot-reload"></a>Горячая перезагрузка

Выберите **Горячая перезагрузка**, чтобы применить изменения в приложении Teams, если вы хотите одновременно обновлять и сохранять исходные коды во время отладки.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload.png" alt-text="Значок горячей перезагрузки":::

Выберите параметр **Горячая перезагрузка в разделе Сохранение файла** в раскрывающемся списке, чтобы включить автоматическую горячую перезагрузку.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload-filesave.png" alt-text="Выбор горячей перезагрузки при сохранении файла":::
  
   > [!Tip]
   > Дополнительные сведения о Горячая перезагрузка функции Visual Studio во время отладки см. на сайте <https://aka.ms/teamsfx-vs-hotreload>.

### <a name="stop-debugging"></a>Остановить отладку

После завершения локальной **отладки выберите Остановить отладку** .

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Stopdebug.png" alt-text="Значок остановки отладки":::

## <a name="customize-debug-settings"></a>Настроить параметры отладки

Вы можете настроить параметр отладки для приложения Teams, чтобы использовать конечные точки бота и добавить переменные среды:

### <a name="use-your-bot-endpoint"></a>Использование конечной точки бота

Конфигурацию siteEndpoint можно задать в **.fx/configs/config.local.json** для конечной точки.

```
"bot": {
    "siteEndpoint": "https://baidu.com"
}
```

### <a name="add-environment-variables"></a>Добавление переменных среды

Вы можете добавить **environmentVariables** в файл **launchSettings.json** .

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-environment-variables.png" alt-text="Добавление настраиваемых переменных среды":::

### <a name="launch-teams-app-as-a-web-app"></a>Запуск приложения Teams в качестве веб-приложения

Вы можете запустить приложение Teams как веб-приложение, а не запускать в клиенте Teams.

1. Выберите **Свойства** > **launchSettings.json** на панели Обозреватель решений под проектом.
1. Удалите **launchUrl** из файла.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png" alt-text="Запуск команд в качестве веб-приложения путем удаления launchurl" lightbox="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png":::

1. Щелкните правой кнопкой мыши **Решение** и выберите **Свойства**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png" alt-text="Щелкните правой кнопкой мыши решение и выберите свойства" lightbox="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png":::

1. В диалоговом окне выберите **Свойства** > **конфигурации Конфигурация** .
1. Снимите флажок **Развернуть** .
1. Нажмите кнопку **ОК**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png" alt-text="Снимите флажок развернуть в свойствах конфигурации" lightbox="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png":::

::: zone-end

## <a name="see-also"></a>См. также

* [Отладка фонового процесса](debug-background-process.md)
* [Подготовка облачных ресурсов с помощью набора средств Teams](provision.md)
* [Развертывание в облаке](deploy.md)
* [Предварительный просмотр и настройка манифеста приложения Teams](TeamsFx-preview-and-customize-app-manifest.md)
