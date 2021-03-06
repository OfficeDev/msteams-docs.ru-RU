---
title: Создание приложений с помощью кода Microsoft Teams набор средств и Visual Studio
description: Начало создания больших пользовательских приложений непосредственно в Visual Studio с microsoft Teams набор средств
keywords: команда визуальный набор кода студии
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: b2cfab5cb2ea2d727608b6ea3bbfec3271b2b039
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994142"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Создание приложений с кодом Teams набор средств и Visual Studio

Код Teams набор средств для Visual Studio помогает разработчикам создавать и развертывать приложения Teams с интегрированным удостоверением, доступом к облачному хранилище, данным Microsoft Graph и другим службам в Azure и M365 с подходом "нулевой конфигурации" к опыту разработчика.  

Вы также можете использовать набор инструментов с Visual Studio или как CLI `teamsfx` (называется).

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>Установка команд набор средств для Visual Studio кода

1. Откройте Visual Studio Code.
1. Выберите представление Расширения **(Ctrl+Shift+X**  /  **⌘⇧-X** или **> расширения).**
1. В поле поиска введите _Teams набор средств_.
1. Выберите на зеленой кнопке установки рядом с командой набор средств.

Вы также можете найти командные набор средств на Visual Studio [Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

Следующие средства устанавливаются расширением Visual Studio кода при необходимости. Если уже установлено, вместо нее используется установленная версия. Если используется Linux (в том числе WSL), необходимо установить эти средства перед использованием:

- [Основные средства Azure Functions](/azure/azure-functions/functions-run-local)

    Основные средства Azure Functions используются для локального запуска отлаженных компонентов, включая помощников проверки подлинности, необходимых при запуске служб в Azure. Он устанавливается в каталоге проекта с помощью `devDependencies` npm.

- [SDK .NET](/dotnet/core/install/)

    SDK .NET используется для установки настраиваемых привязки для локального отладки и развертывания приложений Azure Functions. Если во всем мире не установленА SDK .NET 3.1 или более поздней версии, установлена портативная версия.

- [ngrok](https://ngrok.com/download)

    Некоторые функции приложения Teams (беседующие боты, расширения обмена сообщениями и входящие веб-окки) требуют входящих подключений.  Вам необходимо выставить систему разработки в Teams через туннель. Туннель не требуется для приложений, которые включают только вкладки.  Этот пакет устанавливается в каталоге проекта (с помощью `devDependencies` npm).

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>Используйте командные набор средств для Visual Studio кода

- [Настройка нового проекта](#set-up-a-new-teams-project)
- [Настройка приложения](#configure-your-app)
- [Локальный запуск приложения](#install-and-run-your-app-locally)
- [Публикация приложения](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Настройка нового проекта Teams

Teams набор средств приложения React, которые находятся в веб-частях Azure или SPFx, которые находятся в среде M365 SharePoint. Чтобы создать новое приложение React, которое будет организовано в Azure:

1. Откройте Visual Studio Code.
1. Откройте набор средств Teams, выбрав значок Teams на боковой панели:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. Выберите **Создать проект**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. Выберите **Создать приложение Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания проекта":::

1. На **шаге Выбор возможностей** уже выбрана возможность **Tab.** Кроме того, можно дополнительно выбрать **расширение бота** **и обмена сообщениями.**  Нажмите кнопку **ОК**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. На шаге **Тип размещения на клиенте** выберите **Azure**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Снимок экрана: выбор размещения для нового приложения.":::

1. Необязательно на шаге **Облачные ресурсы** выберите облачные ресурсы, которые использует ваше приложение. Можно выбрать CRUD (создать, прочитать, обновить и удалить) доступ к SQL или API:

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Снимок экрана: добавление облачных ресурсов в новое приложение.":::

1. На **шаге Язык программирования** можно выбрать **JavaScript** или **TypeScript:**

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Снимок экрана: выбор языка.":::

1. Выберите папку рабочей области. Папка создается в папке рабочего пространства для созданного вами проекта.

1. Введите подходящее имя для приложения, например `helloworld`. Имя приложения должно состоять только из букв и цифр.  Чтобы продолжить, нажмите клавишу **ВВОД**.

Приложение Teams создается в течение нескольких секунд. Приложение scaffolded содержит код для обработки одной входной записи с Помощью Azure Active Directory и доступа к Microsoft Graph.  Если вы выбрали ресурсы Azure, код для этих ресурсов также доступен.

Подробнее о процессе создания и публикации SPFx см. в руководстве [SPFx.](../get-started/first-app-spfx.md)

## <a name="configure-your-app"></a>Настройка приложения

В основе приложения Teams три компонента:

  1. Клиент Microsoft Teams (веб-, настольный или мобильный), в котором пользователи взаимодействуют с вашим приложением.
  1. Сервер, который отвечает на запросы контента, отображаемой в Teams. Например, содержимое вкладок HTML или адаптивная карта бота.
  1. Пакет приложений Teams состоит из трех файлов:

      > [!div class="checklist"]
      >
      > - В manifest.js.
      > - Значок [цвета](../resources/schema/manifest-schema.md#icons) для отображения приложения в каталоге общедоступных или организаций.
      > - Значок [плана](../resources/schema/manifest-schema.md#icons) для отображения в панели действий Teams.

Манифест и значки хранятся в папке проекта перед отправкой `.fx` в Teams. При установке приложения клиент Teams определяет файл манифеста, чтобы определить необходимые сведения, такие как имя приложения и URL-адрес, в котором находятся службы.

1. Чтобы настроить приложение, перейдите на **вкладку Teams набор средств** в Visual Studio Code.
1. Выберите **редактор манифеста** в разделе **Project.**

Редактирование полей на странице подробные сведения приложения обновляет содержимое manifest.jsфайла, который в конечном итоге отправляется в составе пакета приложений.

## <a name="install-and-run-your-app-locally"></a>Установка и локальное запуск приложения

Чтобы создать и запустить приложение локально, выполните следующие действия.

1. В Visual Studio Code нажмите клавишу **F5**, чтобы запустить приложение в режиме отладки.

   > При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.  По завершении сборки автоматически откроется окно браузера.  Для завершения может потребоваться от 3 до 5 минут.

   В наборе инструментов при необходимости необходимо установить локальный сертификат. Этот сертификат позволяет Teams загружать приложение из `https://localhost`. Выберите "Да", когда появится следующее диалоговое окно:

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. Откроется веб-браузер для запуска приложения. При появлении запроса на открытие Microsoft Teams выберите "Отмена", чтобы остаться в браузере. Вам также может быть предложено перейти в приложение Teams в другое время. Выберите веб-приложение, когда это произойдет.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Снимок экрана: выбор веб-версии Teams при запуске":::

1. Вам может быть предложено выполнить вход. В этом случае войдите с учетной записью M365.
1. При появлении запроса на установку приложения в Teams нажмите кнопку **Добавить**.

В отладку кода Visual Studio подключаются как Visual Studio, так и frontend.  Это позволяет устанавливать точки разрыва в любом месте кода и проверять состояние.  В браузере также можно использовать любые средства отладки переднего входа (например, средства разработчика React).  Дополнительные сведения о отладки в Visual Studio Коде [просмотрите документацию.](https://code.visualstudio.com/Docs/editor/debugging)

## <a name="publish-your-app-to-teams"></a>Опубликуйте свое приложение в Teams

Прежде чем использовать его другими людьми, необходимо опубликовать приложение на портале разработчиков для teams.

1. Чтобы опубликовать приложение, перейдите на **вкладку Teams набор средств** в Visual Studio Code.
1. Выберите **Опубликовать Teams** в разделе **Project.**

При использовании хостинга Azure необходимо предварительно и развернуто в облаке. Подробнее о процессе публикации SPFx см. в [SPFx.](../get-started/first-app-spfx.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Ведение и поддержка опубликованного приложения](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
