---
title: Создание приложений с помощью Microsoft Teams набор средств и Visual Studio Code
description: Начало создания больших пользовательских приложений непосредственно Visual Studio Code с Microsoft Teams набор средств
keywords: команда визуальный набор кода студии
ms.localizationpriority: medium
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: f2bb0d5dbd999a5d935c051d854bd94b21ce3f19
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889323"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Создание приложений с помощью Teams набор средств и Visual Studio Code

Программа Teams набор средств для Visual Studio Code помогает разработчикам создавать и развертывать приложения Teams с интегрированной идентификацией, доступом к облачному хранилище, данным microsoft Graph и другим службам в Azure и M365 с подходом "нулевой конфигурации" к опыту разработчика.  

Вы также можете использовать набор инструментов с Visual Studio или как CLI `teamsfx` (называется).

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>Установите Teams набор средств для Visual Studio Code

1. Откройте Visual Studio Code.
1. Выберите представление Расширения **(Ctrl+Shift+X**  /  **⌘⇧-X** или **> расширения).**
1. В поле поиска введите _Teams набор средств_.
1. Выберите на зеленой кнопке установки рядом с Teams набор средств.

Вы также можете найти Teams набор средств на Visual Studio Code [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

Следующие средства устанавливаются расширением Visual Studio Code при необходимости. Если уже установлено, вместо нее используется установленная версия. Если используется Linux (в том числе WSL), необходимо установить эти средства перед использованием:

- [Основные средства Azure Functions](/azure/azure-functions/functions-run-local)

    Основные средства Azure Functions используются для локального запуска отлаженных компонентов, включая помощников проверки подлинности, необходимых при запуске служб в Azure. Он устанавливается в каталоге проекта с помощью `devDependencies` npm.

- [SDK .NET](/dotnet/core/install/)

    SDK .NET используется для установки настраиваемых привязки для локального отладки и развертывания приложений Azure Functions. Если во всем мире не установленА SDK .NET 3.1 или более поздней версии, установлена портативная версия.

- [ngrok](https://ngrok.com/download)

    Некоторые Teams приложения (беседные боты, расширения обмена сообщениями и входящие веб-оки) требуют входящих подключений.  Необходимо подвергать систему разработки Teams через туннель. Туннель не требуется для приложений, которые включают только вкладки.  Этот пакет устанавливается в каталоге проекта (с помощью `devDependencies` npm).

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>Используйте Teams набор средств для Visual Studio Code

- [Настройка нового проекта](#set-up-a-new-teams-project)
- [Настройка приложения](#configure-your-app)
- [Локальный запуск приложения](#install-and-run-your-app-locally)
- [Публикация приложения](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Настройка нового проекта Teams

В Teams набор средств можно создавать React, которые находятся в Веб-частях Azure или SPFx, которые находятся в среде M365 SharePoint. Чтобы создать новое приложение React, которое будет организовано в Azure:

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

Приложение Teams создается в течение нескольких секунд. Приложение scaffolded содержит код для обработки одной входной записи с помощью Azure Active Directory и доступа к microsoft Graph.  Если вы выбрали ресурсы Azure, код для этих ресурсов также доступен.

Подробнее о процессе создания SPFx публикации см. в [SPFx.](../get-started/first-app-spfx.md)

## <a name="configure-your-app"></a>Настройка приложения

В основе приложения Teams три компонента:

  1. Клиент Microsoft Teams (веб-, настольный или мобильный), где пользователи взаимодействуют с вашим приложением.
  1. Сервер, который отвечает на запросы контента, отображаемой в Teams. Например, содержимое вкладок HTML или адаптивная карта бота.
  1. Пакет Teams состоит из трех файлов:

      > [!div class="checklist"]
      >
      > - Манифест.json.
      > - Значок [цвета](../resources/schema/manifest-schema.md#icons) для отображения приложения в каталоге общедоступных или организаций.
      > - Значок [плана](../resources/schema/manifest-schema.md#icons) для отображения на панели Teams действий.

Манифест и значки хранятся в папке проекта перед отправкой `.fx` в Teams. При установке приложения клиент Teams определяет файл манифеста, чтобы определить необходимые сведения, такие как имя приложения и URL-адрес, в котором находятся службы.

1. Чтобы настроить приложение, перейдите на вкладку Teams набор средств **в** Visual Studio Code.
1. Выберите **редактор манифеста** **в Project** разделе.

Редактирование полей на странице сведения приложения обновляет содержимое файла manifest.json, который в конечном счете отправляется в составе пакета приложений.

## <a name="install-and-run-your-app-locally"></a>Установка и локальное запуск приложения

Чтобы создать и запустить приложение локально, выполните следующие действия.

1. В Visual Studio Code нажмите клавишу **F5**, чтобы запустить приложение в режиме отладки.

   > При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.  По завершении сборки автоматически откроется окно браузера.  Для завершения может потребоваться от 3 до 5 минут.

   В наборе инструментов при необходимости необходимо установить локальный сертификат. Этот сертификат позволяет Teams загружать приложение из `https://localhost`. Выберите "Да", когда появится следующее диалоговое окно:

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. Откроется веб-браузер для запуска приложения. При появлении запроса на открытие Microsoft Teams выберите "Отмена", чтобы остаться в браузере. Вам также может быть предложено перейти на Teams приложение в другое время. Выберите веб-приложение, когда это произойдет.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Снимок экрана: выбор веб-версии Teams при запуске":::

1. Вам может быть предложено выполнить вход. В этом случае войдите с учетной записью M365.
1. При появлении запроса на установку приложения в Teams нажмите кнопку **Добавить**.

В отладку подключены как Visual Studio Code, так и Visual Studio Code.  Это позволяет устанавливать точки разрыва в любом месте кода и проверять состояние.  В браузере также можно использовать любые средства отладки frontend (например, средства React разработчика).  Дополнительные сведения о отладки в Visual Studio Code, [просмотрите документацию](https://code.visualstudio.com/Docs/editor/debugging).

## <a name="publish-your-app-to-teams"></a>Опубликуйте свое приложение в Teams

Прежде чем использовать его другими людьми, необходимо опубликовать приложение на портале разработчиков для Teams.

1. Чтобы опубликовать приложение, перейдите на вкладку **Teams набор средств** в Visual Studio Code.
1. Выберите **Опубликовать Teams** в разделе **Project.**

При использовании хостинга Azure необходимо предварительно и развернуто в облаке. Подробнее о процессе публикации SPFx см. в [SPFx.](../get-started/first-app-spfx.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Ведение и поддержка опубликованного приложения](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

## <a name="see-also"></a>См. также

* [Создание приложений с помощью Teams набор средств и Visual Studio](~/toolkit/visual-studio-overview.md)
* [Создание вкладок и других опытом работы с клиентом Microsoft Teams JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md)
