---
title: 'Начало работы : сборка и запуск первого приложения'
author: heath-hamilton
description: Быстро создайте приложение Microsoft Teams, которое отображает "Hello, World!" сообщение с помощью microsoft Teams набор средств.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093952"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>Создание и запуск первого приложения Microsoft Teams

Начните разработку Microsoft Teams, построив личную вкладку "Hello, World!".
Создайте и запустите свое первое приложение Teams с помощью следующих действий:

## <a name="1-create-your-app-project"></a>1. Создайте проект приложения

Используйте microsoft Teams набор средств в Visual Studio Code, чтобы настроить свой первый проект приложения. Создайте проект приложения с помощью следующих действий:

1. В Visual Studio кода выберите **Microsoft Teams** в левой панели действий и выберите :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **"Создать новое приложение Teams".**
1. При запросе во sign in with your Microsoft 365 development account.
1. На экране **"Добавление возможностей" выберите** "Вкладка", а затем  **"Далее".**
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Screenshot showing how to configure your app project with the Visual Studio Code Teams набор средств.":::
1. Введите имя приложения Teams. (Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)
1. Проверьте только параметр **"Личная вкладка"** и выберите "Готово" в нижней части экрана, чтобы настроить проект. 

## <a name="2-understand-important-app-project-components"></a>2. Понимание важных компонентов проекта приложения

После того как набор средств настроит проект, у вас будут компоненты для создания базовой личной вкладки для Teams. Каталоги и файлы проекта отображаются в области проводника Visual Studio кода.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Screenshot showing app project files for a personal tab in Visual Studio Code.":::

### <a name="app-scaffolding"></a>Скафаолдинг приложений

Набор средств автоматически создает скафолдинг для вас в каталоге на основе возможностей, добавленных `src` во время установки.

Например, если вы создаете вкладку во время установки, файл в каталоге имеет важное значение, так как он обрабатывает инициализацию и `App.js` `src/components` маршрутизацию приложения. Он вызывает [клиентский SDK JavaScript](../tabs/how-to/using-teams-client-sdk.md) для Microsoft Teams, чтобы установить связь между вашим приложением и Teams.

### <a name="app-id"></a>Идентификатор приложения

Настройте приложение с помощью App Studio с помощью ИД приложения Teams. Найдите ИД в объекте, который находится `teamsAppId` в файле `package.json` проекта.

## <a name="3-build-and-run-your-app"></a>3. Сборка и запуск приложения

Создайте и запустите приложение локально, чтобы сэкономить время. Эти сведения также доступны в наборе `README` средств. Создайте и запустите приложение с помощью следующих действий:

1. В терминале перейдите в корневой каталог проекта приложения и запустите `npm install` его.
1. Запустите `npm start` .

После завершения компилятор **успешно скомпилироваться!** сообщение в терминале. Ваше приложение работает в `https://localhost:3000` .

## <a name="4-sideload-your-app-in-teams"></a>4. Загрузка неогрузки приложения в Teams

Ваше приложение готово для тестирования в Teams. Для этого у вас должна быть учетная запись разработки Microsoft 365, которая разрешает загрузку нео том же приложения. Дополнительные сведения об открытии учетной записи см. в [записи разработки Teams.](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account) 

> [!TIP]
> Проверьте, есть ли проблемы перед загрузкой неогрузки приложения с помощью функции проверки [в App Studio,](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)которая включена в набор средств. Исправьте ошибки для успешной загрузки неокрепленного приложения.

Загрузка неогрузки приложения в Teams с помощью следующих действий:

> [!NOTE]
> Чтобы включить загрузку нео том же приложения перед загрузкой неогрузки в Teams, выполните действия, которые необходимо предпринять в этой [части.](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)

1. Выберите **клавишу F5,** чтобы запустить веб-клиент Teams в Visual Studio коде.
1. Чтобы отобразить содержимое приложения в Teams, укажите, что приложение является `localhost` надежным:
   1. Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которая была открыта после нажатия **F5.**
   1. Перейдите `https://localhost:3000/tab` на страницу и перейдите на нее.
1. Вернуться в Teams. В диалоговом оке выберите **"Добавить для меня",** чтобы установить приложение.
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Снимок экрана с примером приложения личной вкладки &quot;Hello, World!&quot;, запущенного в Teams.":::

🎉 поздравляем! Ваше приложение работает в Teams.

## <a name="next-step"></a>Следующий этап

Разведите личные вкладки, которые вы только что создали, или создайте приложение Teams другого типа.

> [!div class="nextstepaction"]
> [Добавление на личную вкладку](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [Создание вкладки канала](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Создание бота](../build-your-first-app/build-bot.md)
