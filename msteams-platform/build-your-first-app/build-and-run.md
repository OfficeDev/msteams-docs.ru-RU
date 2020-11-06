---
title: Начало работы — сборка и запуск первого приложения
author: heath-hamilton
description: Быстрое создание приложения Microsoft Teams, в котором отображается "Hello, World!". сообщение с помощью набора инструментов Microsoft Teams.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 62c4bd950183ceb64fb30b528661cf84e9210d89
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931781"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>Создание и запуск первого приложения Microsoft Teams

Вы можете перейти непосредственно к разработке Microsoft Teams, создав личную вкладку со значком "Hello, World!".

## <a name="1-create-your-app-project"></a>1. Создайте проект приложения.

Используйте набор средств Microsoft Teams в Visual Studio Code, чтобы настроить первый проект приложения.

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
1. При появлении соответствующего запроса войдите в систему с помощью учетной записи разработчика Microsoft 365.
1. На экране **добавить возможности** выберите **вкладка** **Далее**.
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Снимок экрана, на котором показано, как настроить проект приложения с помощью набора инструментов Visual Studio Code Teams.":::
1. Введите имя приложения Teams. (Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)
1. Установите флажок только для **личной вкладки** и в нижней части экрана нажмите кнопку **Готово** , чтобы настроить свой проект.

## <a name="2-understand-important-app-project-components"></a>2. Изучите важные компоненты проекта приложения

После того как набор инструментов настроит свой проект, у вас будут компоненты для создания базовой вкладки "личные" для Teams. Каталоги и файлы проекта отображаются в области обозревателя Visual Studio Code.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Снимок экрана, на котором показаны файлы проекта приложения для вкладки &quot;личные&quot; в Visual Studio Code.":::

### <a name="app-scaffolding"></a>Формирование шаблонов приложений

Набор средств автоматически создает формирование шаблонов в `src` каталоге на основе возможностей, добавленных во время установки.

Например, при создании вкладки во время установки, `App.js` файл в `src/components` каталоге важен, так как он обрабатывает инициализацию и маршрутизацию приложения. Он вызывает [пакет Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) для установления связи между приложением и Teams.

### <a name="app-id"></a>Идентификатор приложения

Идентификатор приложения Teams необходим для настройки приложения с помощью App Studio. Вы можете найти идентификатор в `teamsAppId` объекте, который находится в `package.json` файле проекта.

## <a name="3-build-and-run-your-app"></a>3. Построение и запуск приложения

В течение этого времени вы создадите и запустите свое приложение локально.

(Эти сведения также доступны в наборе инструментов `README` .)

1. В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .
1. Выполните команду `npm start` .

По завершении **компиляции успешно выполняется.** сообщение в терминале. Ваше приложение запущено `https://localhost:3000` .

## <a name="4-sideload-your-app-in-teams"></a>4. Загрузка неопубликованных ваше приложение в Teams

Ваше приложение готово к тестированию в Teams. Для этого необходимо иметь учетную запись, позволяющую выполнять загрузку неопубликованных приложений. (Если вы не знаете этого, Узнайте о том, как получить [учетную запись разработки Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)

> [!TIP]
> Прежде чем приступить к работе с неопубликованным приложением, проверьте наличие проблем с помощью [функции проверки в App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), которая включена в набор средств. Чтобы успешно Загрузка неопубликованных приложение, необходимо исправить ошибки.

1. В Visual Studio Code нажмите клавишу **F5** , чтобы запустить веб-клиент Teams.
1. Чтобы отобразить содержимое приложения в Teams, укажите, что приложение работает ( `localhost` ) является надежным:
   1. Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которое открывалось после нажатия клавиши **F5**.
   1. Перейдите к `https://localhost:3000/tab` странице и перейдите к ней.
1. Вернитесь в Teams. В диалоговом окне нажмите кнопку **Добавить** , чтобы установить приложение.
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Снимок экрана, на котором показан пример приложения &quot;Hello, World!&quot;, которое работает в Teams.":::

Поздравляем 🎉! Ваше приложение работает в Teams.

## <a name="next-step"></a>Следующий шаг

Разверните вкладку Персональная личная и создайте другой тип приложения Teams.

> [!div class="nextstepaction"]
> [Добавление на вкладку "личные"](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [Создание вкладки канала](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Создание бота](../build-your-first-app/build-bot.md)
