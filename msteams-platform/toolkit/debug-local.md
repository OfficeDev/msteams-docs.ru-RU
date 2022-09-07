---
title: Локальная отладка приложения Teams
author: surbhigupta
description: В этом модуле вы узнаете, как выполнить локальную отладку приложения Teams в Teams Toolkit, а также получите информацию об основных функциях Teams Toolkit
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: 68999351232deb60015259840147d2a1ab55681a
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616566"
---
# <a name="debug-your-microsoft-teams-app-locally"></a>Локальная отладка приложения Microsoft Teams

Microsoft Teams Toolkit помогает выполнять локальную отладку и предварительный просмотр приложения Teams. В процессе отладки Набор средств Teams автоматически запускает службы приложений, запускает отладчики и загружает неопубликовающее приложение Teams. Вы можете просмотреть приложение Teams в веб-клиенте Teams локально после отладки. Перед отладой приложения необходимо настроить Набор средств Teams.

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

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов с помощью набора средств Teams](provision.md)
* [Добавление возможностей в приложения Teams](add-capability.md)
* [Развертывание в облаке](deploy.md)
* [Управление несколькими средами в наборе средств Teams](TeamsFx-multi-env.md)
