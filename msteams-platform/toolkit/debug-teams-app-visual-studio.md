---
author: surbhigupta
title: Отладка приложения Teams для Visual Studio
description: В этом модуле вы узнаете, как выполнить локальную отладку приложения Teams в Visual Studio с помощью набора средств Teams.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: cff0b3e18f63bc7943a7fc16875294f41257a37c
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027448"
---
# <a name="debug-your-teams-app-locally-using-visual-studio"></a>Локальная отладка приложения Teams с помощью Visual Studio

Набор средств Teams помогает выполнять локальную отладку и предварительный просмотр приложения Microsoft Teams. Отладка — это процесс сборки, проверки, обнаружения и исправления проблем или ошибок в приложении. Отладка гарантирует успешное выполнение программы. Visual Studio позволяет выполнять отладку вкладки, бота, расширения сообщений. Набор средств Teams поддерживает следующие функции отладки:

* Подготовка зависимостей приложений Teams
* Начало отладки
* Переключать точки останова
* Горячая перезагрузка
* Остановить отладку

В процессе отладки Набор средств Teams автоматически запускает службы приложений, инициирует отладку и загружает неопубликуемую версию приложения Teams. После отладки вы можете просмотреть приложение Teams в веб-клиенте Teams. Вы также можете настроить параметры отладки для использования конечных точек бота или переменных среды для загрузки настроенного приложения.

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

## <a name="debug-your-app-locally"></a>Локальная отладка приложений

Вы можете выполнить локальную отладку приложения в Visual Studio с помощью набора средств Teams, выполнив следующие действия:

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>Настройка ngrok (только для бота и приложения расширения сообщений)

Выполните следующую команду с помощью командной строки:

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>Настройка набора средств Teams

Выполните следующие действия с помощью набора средств Teams для отладки приложения после создания проекта:

1. Щелкните проект правой **кнопкой мыши**.
1. Выберите **Набор средств Teams**.
1. Выберите **"Подготовка зависимостей приложений Teams"**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="Зависимости приложений Teams для локальной отладки":::

   > [!NOTE]
   > В этом сценарии имя проекта — MyTeamsApp1.

   Ваша учетная запись Microsoft 365 должна иметь разрешение на загрузку на стороне перед входом.  Убедитесь, что приложение Teams можно отправить в клиент, в противном случае приложение Teams может не запуститься в клиенте Teams.

1. Войдите в свою **учетную запись Microsoft 365**.
1. Выберите **"Продолжить**
   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="вход в учетную запись Microsoft 365&quot;":::

   > [!Note]
   > Learn more about sideloading permission by visiting <https://aka.ms/teamsfx-sideloading-option>.

1. Выберите **"Отладка"**.
1. Нажмите **кнопку "Начать отладку**" или нажмите **клавишу F5 напрямую**.

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

## <a name="key-features-of-teams-toolkit"></a>Ключевые функции набора средств Teams

Вы увидите следующие ключевые функции Набора средств Teams, которые автоматизируют локальный процесс отладки приложения Teams:

### <a name="prepare-teams-app-dependencies"></a>Подготовка зависимостей приложений Teams

Набор средств Teams подготавливает зависимости локальной отладки и регистрирует приложение Teams в клиенте в вашей учетной записи. Для приложений Бота и расширения сообщений Набор средств Teams регистрирует и настраивает бот.

### <a name="start-debugging"></a>Начало отладки

Отладку можно выполнить с помощью одной операции, нажмите **клавишу F5** , чтобы начать отладку. Teams Toolkit создает код, запускает службы и запускает приложение в браузере.

### <a name="toggle-breakpoints"></a>Переключать точки останова

Вы можете переключать точки останова в исходных кодах вкладок, ботов, расширений сообщений и функций Azure. Точки останова выполняются при взаимодействии с приложением Teams в веб-браузере.
На следующем рисунке показаны переключаемые точки останова:

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png" alt-text="Локальные точки останова переключателя отладки":::

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

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png" alt-text="Запуск команд в качестве веб-приложения путем удаления launchurl":::

1. Щелкните решение правой **кнопкой мыши**.
1. Выберите пункт **Свойства**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png" alt-text="Щелкните решение правой кнопкой мыши и выберите свойства":::

1. Выберите **конфигурацию свойств конфигурации** >  в диалоговом окне.
1. Снимите флажок " **Развернуть** процесс".
1. Нажмите кнопку **ОК**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png" alt-text="Снимите флажок развертывания в свойствах конфигурации ":::

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
* [Развертывание приложения Teams в облаке с помощью Visual Studio](deploy-teams-app.md)
* [Изменение манифеста приложения Teams с помощью Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
