---
title: Начало работы — сборка и запуск первого приложения
author: heath-hamilton
description: Быстро создайте приложение Microsoft Teams, которое отображает "Hello, World!" сообщение с помощью microsoft Teams набор средств.
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 1b34c3f3121e834abc8a8a92a8a0ac9a049c9e07
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020886"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>Создание и запуск первого приложения Microsoft Teams

Начните разработку Microsoft Teams с создания личной вкладки с отображением "Hello, World!".
Создайте и запустите свое первое приложение Teams с помощью следующих действий:

## <a name="1-create-your-app-project"></a>1. Создание проекта приложения

Используйте microsoft Teams набор средств в Visual Studio коде, чтобы настроить свой первый проект приложения. Создайте проект приложения с помощью следующих действий:

1. В Visual Studio коде выберите **Microsoft Teams** в левой панели действий и создайте новое приложение :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams.**
1. При запросе впишитесь в учетную запись разработки Microsoft 365.
1. На экране **Добавить возможности** выберите **вкладку затем** **Далее**.
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Снимок экрана, показывающий, как настроить проект приложения с помощью Visual Studio команд кода набор средств.":::
1. Введите имя приложения Teams. (Это имя по умолчанию для вашего приложения, а также имя каталога проектов приложений на локальной машине.)
1. Проверьте только параметр **Личные вкладки** и выберите **Готово** в нижней части экрана, чтобы настроить проект.

## <a name="2-understand-important-app-project-components"></a>2. Понимание важных компонентов проекта приложения

Как только набор инструментов настраивает проект, у вас есть компоненты для создания базовой личной вкладки для Teams. Каталоги проектов и файлы отображаются в области Explorer Visual Studio Code.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Снимок экрана, показывающий файлы проектов приложений для личной вкладки Visual Studio Code.":::

### <a name="app-scaffolding"></a>Строительные леса приложений

Набор инструментов автоматически создает леса для вас в каталоге на основе возможностей, которые `src` вы добавили во время установки.

Например, если во время настройки создается вкладка, файл в каталоге имеет важное значение, так как он обрабатывает инициализацию и `App.js` `src/components` маршрутизацию приложения. Он вызывает [SDK клиента Microsoft Teams JavaScript,](../tabs/how-to/using-teams-client-sdk.md) чтобы установить связь между вашим приложением и teams.

### <a name="app-id"></a>Идентификатор приложения

Настройка приложения в App Studio с помощью ID приложения Teams. Найдите ID в `teamsAppId` объекте, который находится в файле `package.json` проекта.

## <a name="3-build-and-run-your-app"></a>3. Сборка и запуск приложения

Создайте и запустите приложение локально, чтобы сэкономить время. Эти сведения также доступны в наборе `README` инструментов. Создайте и запустите приложение с помощью следующих действий:

1. В терминале перейдите в корневой каталог проекта приложения и запустите `npm install` .
1. Запуск `npm start` .

После завершения, есть **компилятор успешно!** сообщение в терминале. Ваше приложение `https://localhost:3000` запущено.

## <a name="4-sideload-your-app-in-teams"></a>4. Sideload ваше приложение в Teams

Ваше приложение готово для тестирования в Teams. Для этого необходимо иметь учетную запись разработки Microsoft 365, которая позволяет загрузку приложений. Дополнительные сведения об открытии учетной записи см. в [записи разработки Teams.](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account) 

> [!TIP]
> Проверьте проблемы перед загрузкой приложения с помощью функции проверки в [App Studio,](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)которая входит в набор инструментов. Устранение ошибок для успешной загрузки приложения.

Загрузка приложения в Teams с помощью следующих действий:

> [!NOTE]
> Чтобы включить побную загрузку перед загрузкой приложения в Teams, выполните действия в [включите загрузку приложения.](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)

1. Выберите **клавишу F5** для запуска веб-клиента Teams в Visual Studio коде.
1. Чтобы отобразить содержимое приложения в Teams, укажите, что в том месте, где работает ваше приложение ( `localhost` ) можно доверять:
   1. Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которая открылась после нажатия **F5.**
   1. Перейдите `https://localhost:3000/tab` на страницу и перейдите к этой странице.
1. Возвращайся в Teams. В диалоговом октаге **выберите Добавить для меня,** чтобы установить ваше приложение.
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Снимок экрана, показывающий пример личного приложения вкладки &quot;Hello, World!&quot;, запущенного в Teams.":::

🎉 поздравляем! Ваше приложение работает в Teams.

## <a name="next-step"></a>Следующий шаг

Разведите личные вкладки, которые вы только что создали, или создайте другое приложение Teams.

> [!div class="nextstepaction"]
> [Добавление в личную вкладку](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [Создание вкладки канала](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Создание бота](../build-your-first-app/build-bot.md)
