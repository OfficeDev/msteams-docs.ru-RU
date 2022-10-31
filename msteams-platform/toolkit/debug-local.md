---
title: Локальная отладка приложения Teams
author: surbhigupta
description: В этом модуле вы узнаете, как выполнить локальную отладку приложения Teams в Teams Toolkit, а также получите информацию об основных функциях Teams Toolkit
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 65eb9599bb60b35448aaf1b6239fc155b7d397d5
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791575"
---
# <a name="debug-your-teams-app-locally"></a>Отлаживайте приложения Teams локально

Набор средств Teams помогает выполнять отладку и предварительный просмотр приложения Microsoft Teams локально. Во время отладки Набор средств Teams автоматически запускает службы приложений, запускает отладчики и загружает приложение Teams неопубликоном. Вы можете просмотреть приложение Teams в веб-клиенте Teams локально после отладки.

::: zone pivot="visual-studio-code"

## <a name="debug-your-microsoft-teams-app-locally-for-visual-studio-code"></a>Локальная отладка приложения Microsoft Teams для Visual Studio Code

Набор средств Teams в Visual Studio Code предоставляет функции для автоматизации локальной отладки приложения Teams. Visual Studio позволяет выполнять отладку вкладки, бота и расширения сообщений. Перед отладкой приложения необходимо настроить Набор средств Teams.

> [!NOTE]
>
> Вы можете обновить старый проект Teams Toolkit для использования новых задач. Дополнительные сведения см. в [документации по параметрам отладки](https://aka.ms/teamsfx-debug-upgrade-new-tasks).

## <a name="set-up-your-teams-toolkit-for-debugging"></a>Настройка набора средств Teams для отладки

Следующие действия помогут вам настроить набор средств Teams перед началом процесса отладки.

# <a name="windows"></a>[Windows](#tab/Windows)

1. Выберите **Отладка (Edge)** или **Отладка (Chrome)** на панели действий в раскрывающемся списке **ЗАПУСК И ОТЛАДКА ▷** .

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Параметр браузера":::

1. Выберите **Запустить** > **запуск отладки (F5).**

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Начать отладку":::

3. Выберите **Войти** в учетную запись Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="Вход":::

   > [!TIP]
   > Можете выбрать **Дополнительные сведения**, чтобы узнать больше о программе разработчиков Microsoft 365. Откроется веб-браузер по умолчанию, чтобы разрешить вход в учетную запись Microsoft 365 с помощью учетных данных.

4. Выберите **Установить**, чтобы установить сертификат разработки для localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="сертификат":::

   > [!TIP]
   > Чтобы узнать о сертификате разработки, выберите **Дополнительные сведения**.

5. Выберите **Да** в диалоговом окне **Предупреждение системы безопасности** :

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="Центр сертификации":::

Набор средств запустит новый экземпляр браузера Microsoft Edge или Chrome (на основе вашего выбора) и откроет веб-страницу для загрузки клиента Teams.  

# <a name="macos"></a>[macOS](#tab/macOS)

1. Выберите **Отладка Edge** или **Отладка Chrome** в раскрывающемся списке **ЗАПУСК И ОТЛАДКА ▷** .

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

5. Введите **имя пользователя** и **пароль**, а затем выберите **Обновить параметры**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="Вход в учетную запись mac":::

Teams Toolkit запускает экземпляр браузера и открывает веб-страницу для загрузки клиента Teams.

---

## <a name="debug-your-app"></a>Отладка приложения

После первоначальной настройки Набор средств Teams запускает следующие процессы:

* [Запускает службы приложений](#starts-app-services)
* [Запускает конфигурации отладки](#launches-debug-configurations)
* [Загружает без публикации приложение Teams](#sideloads-the-teams-app)

### <a name="starts-app-services"></a>Запускает службы приложений

Выполняет задачи, определенные в `.vscode/tasks.json`.

|  Компонент |  Имя задачи  | Folder |
| --- | --- | --- |
|  Tab |  **Запустить интерфейсный сервер** |  tabs |
|  Бот или расширения для сообщений |  **Запустить бот** |  бот |
|  Функции Azure |  **Запустить внутреннюю службу** |  API |

На следующем рисунке отображаются имена задач на вкладках **ВЫВОД** и **ТЕРМИНАЛ** Visual Studio Code при запуске вкладки, расширения бота или сообщения, а также Функции Azure.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal1.png" alt-text="Запуск служб приложений" lightbox="../assets/images/teams-toolkit-v2/debug/Terminal1.png":::

### <a name="launches-debug-configurations"></a>Запускает конфигурации отладки

Запускает конфигурации отладки, определенные в `.vscode/launch.json`.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="Запуск отладчика":::

В следующей таблице перечислены имена и типы конфигураций отладки для проекта с вкладкой, ботом или приложением расширения сообщений, а также Функции Azure:

|  Компонент |  Имя конфигурации отладки  | Тип конфигурации отладки |
| --- | --- | --- |
|  Tab |  **Присоединение к интерфейсу (Edge)** или **Присоединение к интерфейсу (Chrome)**  |  pwa-msedge или pwa-chrome  |
|  Бот или расширения для сообщений |   **Присоединение к боту** |  pwa-node |
| Функции Azure |   **Присоединение к внутренней службе** |  pwa-node |

В следующей таблице перечислены имена и типы конфигураций отладки для проекта с приложением-ботом, Функции Azure и без приложения вкладки.

|  Компонент |  Имя конфигурации отладки  | Тип конфигурации отладки  |
| --- | --- | --- |
|  Бот или расширение для сообщений  | **Запуск бота (Edge)** или **Запуск бота (Chrome)**  |   pwa-msedge или pwa-chrome  |
|  Бот или расширение для сообщений  |   **Присоединение к боту** |  pwa-node  |
|  Функции Azure |  **Присоединение к внутренней службе** |  pwa-node |

### <a name="sideloads-the-teams-app"></a>Загружает приложение Teams без публикации

Конфигурация **Подключение к интерфейсу** или **Запуск бота** запускает экземпляр браузера Edge или Chrome для загрузки клиента Teams на веб-странице. После загрузки клиента Teams Teams загружает неопубликованное приложение Teams, которое управляется URL-адресом загрузки неопубликованных приложений, определенным в конфигурациях запуска [Microsoft Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}). Когда клиент Teams загружается в веб-браузере, выберите **Добавить** или выберите нужный параметр в раскрывающемся списке.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="Добавление локальной отладки" lightbox="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png":::

   Ваше приложение добавлено в Teams!

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [Отладка фоновых процессов](debug-background-process.md)

::: zone-end

::: zone pivot="visual-studio"

## <a name="debug-your-teams-app-locally-using-visual-studio"></a>Локальная отладка приложения Teams с помощью Visual Studio

Набор средств Teams помогает выполнять отладку и предварительный просмотр приложения Microsoft Teams локально. Visual Studio позволяет выполнять отладку вкладки, бота и расширения сообщений. Вы можете выполнить отладку приложения локально в Visual Studio с помощью набора средств Teams, выполнив следующие действия:

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>Настройка ngrok (только для бота и приложения расширения сообщений)

Используйте командную строку, чтобы выполнить следующую команду:

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>Настройка набора средств Teams

Выполните следующие действия с помощью набора средств Teams для отладки приложения после создания проекта.

1. Щелкните **проект** правой кнопкой мыши.
1. Выберите **Teams Toolkit** > **Prepare Teams App Dependencies (Подготовка зависимостей приложений Teams**).

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="Зависимости приложений Teams для локальной отладки" lightbox="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png":::

   > [!NOTE]
   > В этом сценарии проект называется MyTeamsApp1.

   У вашей учетной записи Microsoft 365 должно быть разрешение на загрузку со стороны, прежде чем выполнять вход.  Убедитесь, что приложение Teams можно отправить в клиент, в противном случае приложение Teams может не запуститься в клиенте Teams.

1. Войдите в **учетную запись Microsoft 365**, а затем нажмите **кнопку Продолжить**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="Вход в учетную запись Microsoft 365":::

   > [!Note]
   > Дополнительные сведения о неопубликованных разрешениях см. на странице <https://aka.ms/teamsfx-sideloading-option>.

1. Выберите **Отладка** > **Начать отладку** или напрямую щелкните **F5**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Startdebug.png" alt-text="Запуск отладки":::

   Visual Studio запускает приложение Teams в клиенте Microsoft Teams в браузере.

   > [!Note]
   > Дополнительные сведения см. на .<https://aka.ms/teamsfx-vs-debug>

1. После загрузки Microsoft Teams выберите **Добавить** , чтобы установить приложение в Teams.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-add-loadapp.png" alt-text="Выберите добавить, чтобы загрузить приложение":::

   > [!TIP]
   > Вы также можете использовать функцию горячей перезагрузки Visual Studio во время отладки. Дополнительные сведения см. на .<https://aka.ms/teamsfx-vs-hotreload>

   > [!NOTE]
   > Обязательно опубликуйте HTTP-запрос в , чтобы `http://localhost:5130/api/notification` активировать уведомление при отладке приложения бота уведомлений. Если при создании проекта выбран триггер HTTP, можно использовать любые средства API, такие как curl (командная строка Windows), Postman и т. д.

   > [!TIP]
   > Если вы вносите какие-либо изменения в файл манифеста приложения Teams (/templates/appPackage/manifest.template.json), обязательно выполните команду Подготовка зависимостей приложения Teams. Прежде чем пытаться снова запустить приложение Teams локально.

::: zone-end

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов с помощью набора средств Teams](provision.md)
* [Добавление возможностей в приложения Teams](add-capability.md)
* [Развертывание в облаке](deploy.md)
* [Управление несколькими средами в наборе средств Teams](TeamsFx-multi-env.md)
