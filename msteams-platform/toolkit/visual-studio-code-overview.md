---
title: Создание приложений с помощью набора средств Microsoft Teams и Visual Studio Code
description: начало работы создавать отличные пользовательские приложения непосредственно в Visual Studio Code с помощью Microsoft Teams Toolkit.
keywords: Набор средств Visual Studio Code для Teams
ms.localizationpriority: medium
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 4672c6be9629d70c50885ecd0d9d034c943a337a
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123078"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Создание приложений с помощью Teams toolkit и Visual Studio Code

Набор средств Teams для Visual Studio Code помогает разработчикам создавать и развертывать приложения Teams с интегрированными удостоверениями, доступом к облачному хранилищу, данным из Microsoft Graph и другим службам в Azure и Microsoft 365 с подходом "нулевой конфигурации" к интерфейсу разработчика.

Вы также можете использовать набор средств с Visual Studio или в виде интерфейса командной строки (называется).`teamsfx`

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>Установите Teams toolkit for Visual Studio Code

1. Откройте Visual Studio Code.
1. Выберите представление расширений (**CTRL+SHIFT+X** / **⌘⇧-X** или **view > Extensions**).
1. В поле поиска введите _Teams Toolkit_.
1. Нажмите зеленую кнопку установки рядом с Teams Toolkit.

Вы также можете найти Teams toolkit [на Visual Studio Code Marketplace.](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

Следующие средства устанавливаются расширением Visual Studio Code при необходимости. Если установленная версия уже установлена, вместо нее используется установленная версия. При использовании Linux (включая WSL) перед использованием необходимо установить следующие средства:

- [Azure Functions Core Tools](/azure/azure-functions/functions-run-local)

    Функции Azure Core Tools используется для локального запуска внутренних компонентов во время выполнения локальной отладки, включая вспомогательные средства проверки подлинности, необходимые при запуске служб в Azure. Он устанавливается в каталоге проекта с помощью `devDependencies`npm.

- [Пакет SDK для .NET](/dotnet/core/install/)

    Пакет .NET SDK используется для установки настраиваемых привязок для локальной отладки и Функции Azure приложений. Если вы не установили пакет SDK .NET версии 3.1 или более поздней версии глобально, устанавливается переносимая версия.

- [ngrok](https://ngrok.com/download)

    Некоторые Teams приложения (чат-боты, расширения для обмена сообщениями и входящие веб-перехватчики) требуют входящих подключений.  Необходимо предоставить систему разработки для Teams через туннель. Туннель не требуется для приложений, которые включают только вкладки.  Этот пакет устанавливается в каталоге проекта (с npm`devDependencies`).

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>Используйте Teams toolkit for Visual Studio Code

- [Настройка нового проекта](#set-up-a-new-teams-project)
- [Настройка приложения](#configure-your-app)
- [Локальный запуск приложения](#install-and-run-your-app-locally)
- [Публикация приложения](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Настройка нового проекта Teams проекта

Набор Teams toolkit может React приложения, размещенные в Azure или SPFx веб-частях, размещенных в Microsoft 365 SharePoint среде. Чтобы создать новое React, которое будет размещено в Azure:

1. Откройте Visual Studio Code.
1. Откройте набор средств Teams, выбрав значок Teams на боковой панели:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. Выберите **Создать проект**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. Выберите **Создать приложение Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания проекта":::

1. На **шаге "Выбор возможностей** " функция **tab** уже выбрана. Вы также можете выбрать бот **и** **расширение для обмена сообщениями**.  Нажмите кнопку **ОК**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. На шаге **Тип размещения на клиенте** выберите **Azure**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Снимок экрана: выбор размещения для нового приложения.":::

1. При необходимости на шаге " **Облачные ресурсы** " выберите облачные ресурсы, используемые приложением. Вы можете выбрать CRUD (создать, прочитать, обновить и удалить) доступ к SQL таблице или API:

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Снимок экрана: добавление облачных ресурсов в новое приложение.":::

1. На **шаге "** Язык программирования" можно выбрать **JavaScript** или **TypeScript**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Снимок экрана: выбор языка.":::

1. Выберите папку рабочей области. Папка создается в папке рабочей области для проекта, который вы создаете.

1. Введите подходящее имя для приложения, например `helloworld`. Имя приложения должно состоять только из букв и цифр. Чтобы продолжить, нажмите клавишу **ВВОД**.

Ваше Teams создается в течение нескольких секунд. Сформированное приложение содержит код для обработки единого входа с Azure Active Directory доступа к microsoft Graph. Если вы выбрали ресурсы Azure, код для этих ресурсов также будет доступен.

Пошаговые инструкции по созданию SPFx публикации см. в SPFx [руководстве](../get-started/first-app-spfx.md).

## <a name="configure-your-app"></a>Настройка приложения

В основе приложения Teams три компонента:

  1. Клиент Microsoft Teams (веб-, настольный или мобильный), в котором пользователи взаимодействуют с вашим приложением.
  1. Сервер, который отвечает на запросы содержимого, отображаемого в Teams. Например, содержимое вкладки HTML или адаптивная карточка бота.
  1. Пакет Teams состоит из трех файлов:

      > [!div class="checklist"]
      >
      > - Файл manifest.json.
      > - [Значок цвета для](../resources/schema/manifest-schema.md#icons) вашего приложения, отображаемый в общедоступном каталоге или каталоге приложений организации.
      > - [Значок структуры для](../resources/schema/manifest-schema.md#icons) отображения на панели Teams действий.

Манифест и значки хранятся в папке `.fx` проекта перед отправкой в Teams. При установке приложения клиент Teams анализирует файл манифеста, чтобы определить необходимые сведения, такие как имя приложения и URL-адрес, где находятся службы.

1. Чтобы настроить приложение, перейдите на вкладку **Teams Toolkit** в Visual Studio Code.
1. Выберите **редактор манифеста** **в Project разделе**.

При редактировании полей на странице сведений о приложении обновляется содержимое файла manifest.json, который в конечном итоге поставляется как часть пакета приложения.

## <a name="install-and-run-your-app-locally"></a>Установка и запуск приложения локально

Чтобы создать и запустить приложение локально, выполните следующие действия.

1. В Visual Studio Code нажмите клавишу **F5**, чтобы запустить приложение в режиме отладки.

   > При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.  По завершении сборки автоматически откроется окно браузера. Для завершения может потребоваться от 3 до 5 минут.

   При необходимости набор средств предложит установить локальный сертификат. Этот сертификат позволяет Teams загружать приложение из `https://localhost`. Выберите "Да", когда появится следующее диалоговое окно:

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. Откроется веб-браузер для запуска приложения. При появлении запроса на открытие Microsoft Teams выберите "Отмена", чтобы остаться в браузере. Вам также может быть предложено переключиться на Teams в другое время. Выберите веб-приложение, когда это произойдет.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Снимок экрана: выбор веб-версии Teams при запуске":::

1. Вам может быть предложено выполнить вход. Если да, войдите с помощью Microsoft 365 учетной записи.
1. При появлении запроса на установку приложения в Teams нажмите кнопку **Добавить**.

Как внутренний, так и внешний интерфейсы подключаются к Visual Studio Code отладчику. Это позволяет задать точки останова в любом месте кода и проверить состояние.  Вы также можете использовать любые средства отладки внешнего интерфейса (например, React developer Tools) в браузере.  Дополнительные сведения об отладке в Visual Studio Code см. [в документации](https://code.visualstudio.com/Docs/editor/debugging).

## <a name="publish-your-app-to-teams"></a>Опубликуйте свое приложение в Teams

Прежде чем использовать его другими пользователями, необходимо опубликовать приложение на портале разработчика для Teams.

1. Чтобы опубликовать приложение, перейдите на вкладку **Teams Toolkit** в Visual Studio Code.
1. В **разделе Teams** **"Опубликовать** Project".

При использовании размещения Azure необходимо подготовить и развернуть его в облаке. Пошаговые инструкции по SPFx публикации см. в SPFx [руководстве](../get-started/first-app-spfx.md).

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Обслуживание и поддержка опубликованного приложения](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

## <a name="see-also"></a>См. также

- [Создание приложений с помощью набора средств Teams и Visual Studio](~/toolkit/visual-studio-overview.md)
- [Вкладки сборки и другие размещенные возможности с клиентским пакетом SDK Microsoft Teams JavaScript](~/tabs/how-to/using-teams-client-sdk.md)
