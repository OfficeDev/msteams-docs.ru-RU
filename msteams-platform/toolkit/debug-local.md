---
title: Отладка приложения Teams
description: Отлаживайте приложения Teams локально в наборе средств Teams
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: 5615175ef6dac7f232f276c73f2991db8433224c
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123978"
---
# <a name="debug-your-teams-app-locally"></a>Отлаживайте приложения Teams локально

Набор средств Teams поможет отладить и предварительно просмотреть приложение Teams локально. Отладка — это процесс проверки, выявления и исправления проблем или дефектов, чтобы обеспечить успешную работу программы. Visual Studio Code позволяет отладить вкладку, бот, расширение для сообщений и Функции Azure. Набор средств Teams поддерживает следующие функции отладки:

* [Начать отладку](#start-debugging)
* [Многоцелевая отладка](#multi-target-debugging)
* [Точки останова](#toggle-breakpoints)
* [Горячая перезагрузка](#hot-reload)
* [Остановить отладку](#stop-debugging)  

В процессе отладки набор средств Teams автоматически запускает службы приложений, запускает отладчики и загружает без публикации приложение Teams. После отладки приложение Teams будет доступно для предварительного просмотра в веб клиенте Teams локально. Можно также настраивать параметры отладки для загрузки настроенного приложения, используя конечные точки бота, сертификат разработки или частичную отладку компонента.

## <a name="prerequisite"></a>Предварительное условие

Установка [последней версии набора средств Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

## <a name="key-features-of-teams-toolkit"></a>Ключевые функции набора средств Teams

В следующем списке приведены основные функции набора средств Teams.

### <a name="start-debugging"></a>Начало отладки

Вы можете выполнить одну операцию. Нажмите клавишу **F5**, чтобы начать отладку. Набор средств Teams начинает проверять предварительные требования, регистрирует приложение Azure AD, приложение Teams и регистрирует бот, запускает службы и браузер.

### <a name="multi-target-debugging"></a>Многоцелевая отладка

Для одновременной отладки вкладки, бота, расширения для сообщений и Функций Azure набор средств Teams использует функцию многоцелевой отладки.

### <a name="toggle-breakpoints"></a>Переключать точки останова

Вы можете переключать точки останова в исходном коде вкладок, ботов, расширений для сообщений и Функций Azure. Точки останова выполняются при взаимодействии с приложением Teams в веб-браузере. На следующем рисунке показаны переключаемые точки останова:

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/toggle-points.png" alt-text="Переключение точек останова":::

### <a name="hot-reload"></a>Горячая перезагрузка

Одновременно с отладкой приложения Teams можно обновить и сохранить исходный код вкладки, бота, расширения для сообщений и Функций Azure. Приложение перезагружается, а отладчик снова присоединится к языкам программирования.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hot-reload.png" alt-text="горячая перезагрузка для исходного кода":::

### <a name="stop-debugging"></a>Остановить отладку

После завершения локальной отладки можно выбрать **Остановить** или **Отключиться** на перемещаемой панели инструментов отладки, чтобы остановить все сеансы отладки и завершить задачи. На следующем изображении показано действие остановки отладки.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/stop-debug.png" alt-text="остановить отладку":::

## <a name="debug-your-teams-app-locally"></a>Отлаживайте приложения Teams локально

Ниже приведены инструкции по локальной отладке приложения Teams.

### <a name="set-up-your-teams-toolkit"></a>Настройка набора средств Teams

Создав приложение с помощью набора средств Teams, выполните следующие действия для отладки приложения.

# <a name="windows"></a>[Windows](#tab/Windows)

1. Выберите **Отладку для Edge** или **Отладку для Chrome** в элементе **Выполнить и отладить** в панели действий.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Параметр браузера" border="false":::

1. Выберите **Начать отладку (F5)** или **Запустить**, чтобы запустить приложение Teams в режиме отладки.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Начать отладку" border="false":::

3. Выберите **Войти** в учетную запись Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="Вход" border="true":::

   > [!TIP]
   > Можете выбрать **Дополнительные сведения**, чтобы узнать больше о программе разработчиков Microsoft 365. Откроется веб-браузер по умолчанию, чтобы войти в учетную запись Microsoft 365 с вашими учетными данными.

4. Выберите **Установить**, чтобы установить сертификат разработки для localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="сертификат" border="true":::

   > [!TIP]
   > Чтобы узнать о сертификате разработки, выберите **Дополнительные сведения**.

5. Выберите **Да**, если появится следующее диалоговое окно.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="Центр сертификации" border="true":::

Набор средств запустит новый экземпляр браузера Microsoft Edge или Chrome (на основе вашего выбора) и откроет веб-страницу для загрузки клиента Teams.  

# <a name="macos"></a>[macOS](#tab/macOS)

1. Выберите **Отладку для Edge** или **Отладку для Chrome** в элементе **Выполнить и отладить** в панели действий.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Списки браузеров" border="false":::

1. Выберите **Начать отладку (F5)** или **Запустить**, чтобы запустить приложение Teams в режиме отладки.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Отладка приложения" border="false":::

3. Выберите **Войти** в учетную запись Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="Вход в учетную запись M365" border="true":::

   > [!TIP]
   > Можете выбрать **Дополнительные сведения**, чтобы узнать больше о программе разработчиков Microsoft 365. Откроется веб-браузер по умолчанию, чтобы войти в учетную запись Microsoft 365 с вашими учетными данными.

4. Выберите **Установить**, чтобы установить сертификат разработки для localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="сертификат" border="true":::

   > [!TIP]
   > Чтобы узнать о сертификате разработки, выберите **Дополнительные сведения**.

5. Введите **Имя пользователя** и **Пароль**, а затем выберите **Обновить параметры** в следующем диалоговом окне:

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="Вход в учетную запись mac" border="true":::

Набор средств запустит новый экземпляр выбранного браузера (Edge или Chrome) и откроет веб-страницу для загрузки клиента Teams.

---

### <a name="debug-your-app"></a>Отладка приложения

По окончании начальной настройки набор средств Teams запускает следующие процессы:

<br>

<details>
<summary><b>Запускает службы приложений</b></summary>

Выполняет задачи, определенные в `.vscode/tasks.json` как:

|  Компонент |  Имя задачи  | Folder |
| --- | --- | --- |
|  Tab |  **Запустить интерфейсный сервер** |  tabs |
|  Бот или расширения для сообщений |  **Запустить бот** |  бот |
|  Функции Azure |  **Запустить внутреннюю службу** |  API |

На следующем изображении показаны имена задач на вкладке **Терминал** **вывода** в Visual Studio Code во время работы вкладки, бота или расширения для сообщений и Функций Azure.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal.png" alt-text="Запуск служб приложений":::

</details>
<details>
<summary><b>Запускает отладчики</b></summary>

Запускает конфигурацию отладки, определенную в `.vscode/launch.json` как:

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="Запуск отладчика":::

В следующей таблице указаны имена и типы конфигураций отладки для проекта с приложением вкладки и бот-приложением:

|  Компонент |  Имя конфигурации отладки  | Тип конфигурации отладки |
| --- | --- | --- |
|  Tab |  **Присоединение к интерфейсу (Edge)** или **Присоединение к интерфейсу (Chrome)**  |  pwa-msedge или pwa-chrome  |
|  Бот или расширения для сообщений |   **Присоединение к боту** |  pwa-node |
| Функции Azure |   **Присоединение к внутренней службе** |  pwa-node |

В следующей таблице указаны имена и типы конфигураций отладки для проекта с бот-приложением и без приложения вкладки:

|  Компонент |  Имя конфигурации отладки  | Тип конфигурации отладки  |
| --- | --- | --- |
|  Бот или расширение для сообщений  | **Запуск бота (Edge)** или **Запуск бота (Chrome)**  |   pwa-msedge или pwa-chrome  |
|  Бот или расширение для сообщений  |   **Присоединение к боту** |  pwa-node  |
|  Функции Azure |  **Присоединение к внутренней службе** |  pwa-node |

</details>
<details>
<summary><b>Загружает без публикации приложение Teams</b></summary>

Конфигурация **Присоединение к интерфейсу** или **Запуск бота** запускает новый экземпляр браузера Edge или Chrome и открывает веб-страницу для загрузки клиента Teams. Загрузив клиент, Teams загружает без публикации приложение Teams, управляемое соответствующим URL-адресом, заданным в конфигурации запуска [Microsoft Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}). Когда клиент Teams загрузится в веб-браузере, выберите **Добавить** или другую нужную команду из раскрывающегося списка.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="локальная отладка" border="true":::

   Ваше приложение добавлено в Teams!

</details>

## <a name="customize-debug-settings"></a>Настроить параметры отладки

Набор средств Teams снимает флажки с некоторых необходимых условий и позволяет настраивать параметры отладки для создания вашей вкладки или бота:

<br>

<details>
<summary><b>Использование конечной точки бота</b></summary>

1. В параметрах Visual Studio Code убрать флажок с **Убедитесь, что Ngrok установлен и запущен (ngrok)**.

1. В качестве конфигурации `siteEndpoint` в `.fx/configs/config.local.json` укажите конечную точку.

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

1. В параметрах Visual Studio Code снимите флажок **Убедитесь, что сертификату разработки можно доверять (devCert)**.

1. Укажите в конфигурации `sslCertFile` и `sslKeyFile` в `.fx/configs/config.local.json` путь к вашему файлу сертификата и путь к ключевому файлу

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

1. Если вы отлаживаете вкладку, обновите сценарий `dev:teamsfx` в `tabs/package.json`.

1. Для бота или расширения обмена сообщениями обновите сценарий `dev:teamsfx` в `bot/package.json`

1. Если вы отлаживаете функции Azure, обновите сценарий `dev:teamsfx` в `api/package.json`, а если TypeScript, обновите сценарий `watch:teamsfx`.

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

1. Добавьте комментарий в **Прикрепление к боту** и **Прикрепление к внутренней службе** из набора отладки в `.vscode/launch.json`.

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

2. Добавьте комментарий в **Запуск внутренней службы** и запустите бот из задачи "Начать все" в .vscode/tasks.json.

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

## <a name="next-step"></a>Следующее действие

> [!div class="nextstepaction"]
> [Отладка фонового процесса](debug-background-process.md).

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов с помощью набора средств Teams](provision.md)
* [Добавление возможностей в приложения Teams](add-capability.md)
* [Развертывание в облаке](deploy.md)
* [Управление несколькими средами в наборе средств Teams](TeamsFx-multi-env.md)
