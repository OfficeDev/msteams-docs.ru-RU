---
title: Локальная отладка приложения Teams
author: surbhigupta
description: В этом модуле вы узнаете, как выполнить локальную отладку приложения Teams в Teams Toolkit, а также получите информацию об основных функциях Teams Toolkit
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 5aeaba2248306d8f638ed2529dac964d96ffaea5
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780867"
---
# <a name="debug-your-microsoft-teams-app-locally"></a>Локальная отладка приложения Microsoft Teams

Набор средств Teams поможет отладить и предварительно просмотреть приложение Teams локально. В процессе отладки Набор средств Teams автоматически запускает службы приложений, запускает отладчики и загружает неопубликовающее приложение Teams. Вы можете просмотреть приложение Teams в веб-клиенте Teams локально после отладки.

::: zone pivot="visual-studio-code"

## <a name="debug-your-microsoft-teams-app-locally-for-visual-studio-code"></a>Локальная отладка приложения Microsoft Teams для Visual Studio Code

Набор средств Teams в Visual Studio Code предоставляет функции для автоматизации отладки приложения Teams локально. Visual Studio позволяет выполнять отладку вкладки, бота и расширения сообщений. Перед отладой приложения необходимо настроить Набор средств Teams.

## <a name="set-up-your-teams-toolkit-for-debugging"></a>Настройка набора средств Teams для отладки

Ниже приведены инструкции по настройке набора средств Teams перед началом процесса отладки.

# <a name="windows"></a>[Windows](#tab/Windows)

1. В **раскрывающемся списке** "Запуск и отладка" выберите "Отладка (Edge)  или "Отладка **" (Chrome)** на панели действий.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Параметр браузера":::

1. Выберите **команду "** > **Запуск отладки" (F5).**

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Начать отладку":::

3. Выберите **Войти** в учетную запись Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="Вход":::

   > [!TIP]
   > Можете выбрать **Дополнительные сведения**, чтобы узнать больше о программе разработчиков Microsoft 365. Откроется веб-браузер по умолчанию, позволяющий войти в учетную запись Microsoft 365 с учетными данными.

4. Выберите **Установить**, чтобы установить сертификат разработки для localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="сертификат":::

   > [!TIP]
   > Чтобы узнать о сертификате разработки, выберите **Дополнительные сведения**.

5. В **диалоговом** **окне "Предупреждение системы безопасности** " нажмите кнопку "Да":

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="Центр сертификации":::

Набор средств запустит новый экземпляр браузера Microsoft Edge или Chrome (на основе вашего выбора) и откроет веб-страницу для загрузки клиента Teams.  

# <a name="macos"></a>[macOS](#tab/macOS)

1. В **раскрывающемся списке** "Запуск и отладка **"** выберите "Отладка edge" или "**Отладка Chrome**".

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Списки браузеров":::

1. Выберите **Начать отладку (F5)** или **Запустить**, чтобы запустить приложение Teams в режиме отладки.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Отладка приложения":::

3. Выберите **Войти** в учетную запись Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="Вход в учетную запись M365":::

   > [!TIP]
   > Можете выбрать **Дополнительные сведения**, чтобы узнать больше о программе разработчиков Microsoft 365. Откроется веб-браузер по умолчанию, чтобы войти в учетную запись Microsoft 365 с вашими учетными данными.

4. Выберите **Установить**, чтобы установить сертификат разработки для localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="сертификат":::

   > [!TIP]
   > Чтобы узнать о сертификате разработки, выберите **Дополнительные сведения**.

5. Введите **имя пользователя** и **пароль**, а затем выберите **"Параметры обновления"**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="Вход в учетную запись mac":::

Набор средств Teams запускает экземпляр браузера и открывает веб-страницу для загрузки клиента Teams.

---

## <a name="debug-your-app"></a>Отладка приложения

После первоначальной настройки Набор средств Teams запускает следующие процессы:

* [Запускает службы приложений](#starts-app-services)
* [Запуск конфигураций отладки](#launches-debug-configurations)
* [Загружает без публикации приложение Teams](#sideloads-the-teams-app)

### <a name="starts-app-services"></a>Запускает службы приложений

Выполняет задачи, как определено в `.vscode/tasks.json`.

|  Компонент |  Имя задачи  | Folder |
| --- | --- | --- |
|  Tab |  **Запустить интерфейсный сервер** |  tabs |
|  Бот или расширения для сообщений |  **Запустить бот** |  бот |
|  Функции Azure |  **Запустить внутреннюю службу** |  API |

На следующем рисунке отображаются имена задач на вкладке **OUTPUT** и **TERMINAL** Visual Studio Code при запуске вкладки, бота или расширения сообщения и Функции Azure.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal.png" alt-text="Запуск служб приложений":::

### <a name="launches-debug-configurations"></a>Запуск конфигураций отладки

Запускает конфигурации отладки, как определено в `.vscode/launch.json`.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="Запуск отладчика":::

В следующей таблице перечислены имена и типы конфигурации отладки для проекта с вкладкой, ботом или приложением расширения сообщений и Функции Azure:

|  Компонент |  Имя конфигурации отладки  | Тип конфигурации отладки |
| --- | --- | --- |
|  Tab |  **Присоединение к интерфейсу (Edge)** или **Присоединение к интерфейсу (Chrome)**  |  pwa-msedge или pwa-chrome  |
|  Бот или расширения для сообщений |   **Присоединение к боту** |  pwa-node |
| Функции Azure |   **Присоединение к внутренней службе** |  pwa-node |

В следующей таблице перечислены имена и типы конфигурации отладки для проекта с приложением бота, Функции Azure и без приложения табуляции:

|  Компонент |  Имя конфигурации отладки  | Тип конфигурации отладки  |
| --- | --- | --- |
|  Бот или расширение для сообщений  | **Запуск бота (Edge)** или **Запуск бота (Chrome)**  |   pwa-msedge или pwa-chrome  |
|  Бот или расширение для сообщений  |   **Присоединение к боту** |  pwa-node  |
|  Функции Azure |  **Присоединение к внутренней службе** |  pwa-node |

### <a name="sideloads-the-teams-app"></a>Загружает приложение Teams без публикации

Подключение **конфигурации к интерфейсу или** запуск **бота** запускает экземпляр браузера Edge или Chrome для загрузки клиента Teams на веб-странице. После загрузки клиента Teams загружает неопубликованное приложение Teams, которое управляется URL-адресом загрузки неопубликованных приложений, определенным в конфигурациях запуска [Microsoft Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}). Когда клиент Teams загружается в веб-браузере, выберите  "Добавить" или выберите параметр из раскрывающегося списка в соответствии с вашим требованием.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="Добавление локальной отладки" lightbox="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png":::

   Ваше приложение добавлено в Teams!

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [Отладка фоновых процессов](debug-background-process.md)

::: zone-end

::: zone pivot="visual-studio"

## <a name="debug-your-microsoft-teams-app-locally-using-visual-studio"></a>Локальная отладка приложения Microsoft Teams с помощью Visual Studio

Набор средств Teams помогает выполнять локальную отладку и предварительный просмотр приложения Microsoft Teams. Visual Studio позволяет выполнять отладку вкладки, бота и расширения сообщений. Вы можете выполнить локальную отладку приложения в Visual Studio с помощью набора средств Teams, выполнив следующие действия:

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>Настройка ngrok (только для бота и приложения расширения сообщений)

Выполните следующую команду с помощью командной строки:

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>Настройка набора средств Teams

Выполните следующие действия с помощью набора средств Teams для отладки приложения после создания проекта:

1. Щелкните проект правой **кнопкой мыши**.
1. Выберите **Teams Toolkit Prepare** > **Teams App Dependencies (Подготовка зависимостей приложений Teams**).

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="Зависимости приложений Teams для локальной отладки" lightbox="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png":::

   > [!NOTE]
   > В этом сценарии имя проекта — MyTeamsApp1.

   Ваша учетная запись Microsoft 365 должна иметь разрешение на загрузку на стороне перед входом.  Убедитесь, что приложение Teams можно отправить в клиент, в противном случае приложение Teams может не запуститься в клиенте Teams.

1. Войдите в учетную **запись Microsoft 365** и нажмите кнопку " **Продолжить".**

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="Вход в учетную запись Microsoft 365":::

   > [!Note]
   > Learn more about sideloading permission by visiting <https://aka.ms/teamsfx-sideloading-option>.

1. Выберите **"Начать отладку** > **отладки"** или нажмите **клавишу F5 напрямую**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Startdebug.png" alt-text="Запуск отладки":::

   Visual Studio запускает приложение Teams в клиенте Microsoft Teams в браузере.

   > [!Note]
   > Learn more by visiting <https://aka.ms/teamsfx-vs-debug>.

1. После загрузки Microsoft Teams нажмите **кнопку "** Добавить", чтобы установить приложение в Teams.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-add-loadapp.png" alt-text="Выберите &quot;Добавить&quot;, чтобы загрузить приложение":::

   > [!TIP]
   > Вы также можете использовать функцию горячей перезагрузки Visual Studio во время отладки. Learn more by visiting <https://aka.ms/teamsfx-vs-hotreload>.

   > [!NOTE]
   > Убедитесь, что при отладке приложения бота уведомлений необходимо опубликовать HTTP-запрос<http://localhost:5130/api/notification> на "", чтобы активировать уведомление. Если при создании проекта вы выбрали триггер HTTP, можно использовать любые средства API, такие как curl (командная строка Windows), Postman и т. д.

   > [!TIP]
   > При внесении изменений в файл манифеста приложения Teams (/templates/appPackage/manifest.template.json) убедитесь, что выполнена команда "Подготовка зависимостей приложений Teams". Прежде чем пытаться запустить приложение Teams в локальной среде.

::: zone-end

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов с помощью набора средств Teams](provision.md)
* [Добавление возможностей в приложения Teams](add-capability.md)
* [Развертывание в облаке](deploy.md)
* [Управление несколькими средами в наборе средств Teams](TeamsFx-multi-env.md)
* [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
* [Развертывание приложения Teams в облаке с помощью Visual Studio](deploy-teams-app.md)
* [Изменение манифеста приложения Teams с помощью Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
