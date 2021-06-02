---
title: Начало работы — создайте первое Teams с помощью SPFx
author: zhenyasav
description: Узнайте, как создать настраиваемую вкладку с помощью SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 54886b47bbe70fed5dd1f010517e6c91d8d5a50d
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646768"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a>Сборка и запуск первого Microsoft Teams с помощью SharePoint Framework (SPFx)

В этом руководстве вы создайте новое приложение Microsoft Teams в SharePoint Framework (SPFx), которое реализует простое личное приложение. (Личное *приложение включает* набор вкладок для индивидуального использования.) Во время руководства вы узнаете о структуре приложения Teams, локальном запуске приложения и развертывании приложения для SharePoint.

## <a name="before-you-begin"></a>Прежде чем начать

Убедитесь, что среда разработки настроена путем установки [необходимых условий](prerequisites.md)

> [!div class="nextstepaction"]
> [Установка необходимых компонентов](prerequisites.md)

## <a name="get-organized"></a>Упорядочьте работу

Помимо необходимых условий, необходимо также быть администратором для SharePoint веб-сайтов.  Здесь вы развернете приложение для размещения.  Если вы используете клиента программы разработчика M365, используйте учетную запись администратора, созданную при регистрации для программы.  

## <a name="create-your-project"></a>Создание проекта

Используйте Teams набор средств для создания первого проекта:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Откройте Visual Studio код.
1. Откройте Teams набор средств, выбрав значок Teams на боковой панели:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на Visual Studio Code панели.":::

1. Выберите **Создание новых Project**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки Create New Project в Teams набор средств панели.":::

1. Выберите **Создание нового Teams приложения**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Мастер для создания новых Project":::

1. На **шаге Выбор** возможностей  уже будет выбрана возможность Tab.  Нажмите кнопку **ОК**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Снимок экрана, показывающий, как добавить возможности в новое приложение.":::

1. На **шаге типа** размещения Frontend выберите SharePoint Framework **(SPFx).**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Снимок экрана, показывающий, как выбрать хостинг для нового приложения.":::

1. На **шаге Framework** выберите **React**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Выбор Framework":::

1. При запросе имени **Вебпарта** нажмите **кнопку Ввод,** чтобы принять по умолчанию.

1. При запросе **описания Вебпарта** нажмите **кнопку Ввод,** чтобы принять по умолчанию.

1. При запросе языка **программирования** нажмите **кнопку Ввод,** чтобы принять по умолчанию.

1. Выберите папку рабочего пространства.  Папка будет создана в папке рабочей области для созданного вами проекта.

1. Введите подходящее имя для вашего приложения, например `helloworld` .  Имя приложения должно состоять только из символов альфа-цифр.  Нажмите **кнопку Ввод** для продолжения.

Ваше Teams приложение будет создано в течение нескольких секунд.

# <a name="command-line"></a>[Командная строка](#tab/cli)

Используйте `teamsfx` CLI для создания первого проекта.  Начните с папки, в которой необходимо создать папку проекта.

``` bash
teamsfx new
```

CLI передает некоторые вопросы для создания проекта.  На каждый вопрос будет сообщите, как на него ответить (например, использовать клавиши стрелки для выбора варианта).  Когда вы ответили на вопрос, подтвердите свой выбор, нажав **кнопку Ввод**.

1. Выберите **Создание нового Teams приложения**.
1. Выберите **функцию Tab.**
1. Выберите **SharePoint Framework (SPFx)** переднего размещения.
1. Выберите **React.**
1. Нажмите **кнопку Введите** имя **Вебпарта.**
1. Нажмите **кнопку Ввод** для **описания Webpart**.
1. Нажмите **кнопку Ввод** для **языка программирования**.
1. Нажмите **кнопку Ввод,** чтобы выбрать папку рабочего пространства по умолчанию.
1. Введите подходящее имя для вашего приложения, например `helloworld` .  Имя приложения должно состоять только из символов альфа-цифр.

После ответа на все вопросы будет создан проект.

---

- [Узнайте больше о разработке для SharePoint Framework](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a>Осмотр исходных кодов

Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально.](#run-your-app-locally)

Как только Teams набор средств настраивает проект, у вас есть компоненты для создания базового личного приложения для Teams, которое находится в SharePoint Framework.  Каталоги проектов и файлы отображаются в области Explorer Visual Studio Code.

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Снимок экрана, показывающий файлы проектов приложений для личного приложения в Visual Studio Code.":::

Система набор средств автоматически создает леса для вас в каталоге проектов на основе возможностей, добавленных во время установки. В Teams набор средств сохраняется состояние приложения в `.fx` каталоге.  Среди других элементов в этом каталоге:

- Значки приложения хранятся в качестве PNG-файлов и `color.png` `outline.png` .
- Манифест приложения для публикации на портале разработчиков для Teams хранится в `manifest.source.json` .
- Параметры, выбранные при создании проекта, хранятся в `settings.json` .

Так как вы выбрали проект SPFx Webpart, к вашему пользовательскому интерфейсу имеют отношение следующие файлы:

- Папка содержит `SPFx/src/webparts/{webpart}` веб-SPFx веб-части.
- В `.vscode/launch.json` файле описываются конфигурации отладки, доступные в палитре отладки.

Дополнительные сведения о веб SharePoint веб-Teams для Teams, обратитесь к документации [SharePoint.](/sharepoint/dev/spfx/build-for-teams-overview)

## <a name="run-your-app-locally"></a>Запустите приложение локально

Teams набор средств позволяет локализовку приложения и запуск его через [SharePoint Framework Workbench.](/sharepoint/dev/spfx/debug-in-vscode)

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a>Создайте и запустите приложение локально в Visual Studio Code

Чтобы создать и запустить приложение локально:

1. С Visual Studio Code нажмите **F5**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="Снимок экрана, показывающий, как SPFx приложение в локальной работе.":::

   > [!NOTE]
   > При первом запуске приложения все зависимости загружаются и приложение построено.  Окно браузера автоматически открывается и загружает SharePoint Workbench после завершения сборки.  Это может занять 3-5 минут.

   После загрузки SharePoint workbench.

   >[!NOTE]
   > В набор средств будет предложено установить локальный сертификат, если это необходимо. Этот сертификат позволяет Teams загрузку приложения из `https://localhost` . Выберите да, когда появится следующий диалог:

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана, показывающий, как запрос на установку сертификата SSL для Teams загрузки приложения из localhost.":::

1. Нажмите одну из значков **Добавить веб-часть** (+) для добавления веб-части.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Снимок экрана, SPFx рабочийбек, запущенный с всплывающее всплывающее изображение, чтобы добавить веб-страницу с указанием.":::

1. Выберите веб-сайт из меню.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Снимок экрана, SPFx рабочийбек, запущенный с всплывающее всплывающее изображение, чтобы добавить выбор веб-части.":::

Теперь приложение должно быть запущено.  Вы можете делать обычные действия отладки, как если бы это были какие-либо другие веб SPFx (например, настройка точек взлома).

> [!TIP]
> Попробуйте разместить точки breakpoints в методе рендеринга и `SPFx/src/webparts/{webpart}/{webpart}.ts` перезагрузить окно браузера. VS Code остановится на точках остановок в коде.

## <a name="deploy-your-app-to-sharepoint"></a>Развертывание приложения для SharePoint

Убедитесь SharePoint каталог приложений существует в развертывании.  Если его не существует, [создайте один](/sharepoint/use-app-catalog).  Полное создание каталога приложений может занять до 15 минут.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Откройте Visual Studio Code.
1. Выберите Teams набор средств на боковой панели, выбрав значок Teams.
1. Выберите **Положение в облаке**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Снимок экрана, показывающий команды по подготовкам":::

1. Вы можете отслеживать ход, наблюдая за диалогами в правом нижнем углу.  Через несколько секунд вы увидите следующее уведомление:

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Снимок экрана, показывающий полный диалоговое окно подготовка.":::

1. Как только подготовка завершена, выберите **Развертывание в облаке.**

1. В настоящее время автоматическое развертывание не доступно.  Диалоговое окно будет всплывающее запрос на сборку и развертывание вручную. Пакет **сборки SharePoint.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="Снимок экрана для диалогового пакета Build Sharepoint Package":::

# <a name="command-line"></a>[Командная строка](#tab/cli)

В окне терминала:

1. Запуск `teamsfx provision` .

   ``` bash
   teamsfx provision
   ```

   Возможно, вам будет предложено войти в свою подписку Azure.  При необходимости вам будет предложено выбрать подписку Azure для использования для ресурсов Azure.

   > [!NOTE]
   > Для размещения приложения всегда используются некоторые ресурсы Azure.

1. Запуск `teamsfx deploy` .

   ``` bash
   teamsfx deploy
   ```

1. При запросе выберите **пакет сборки SharePoint.**

---

Пакет SharePoint находится в рамках `SPFx/sharepoint/solution` проекта.  Upload пакет для SharePoint:

1. Войдите в консоль администратора M365, а затем перейдите в каталог SharePoint приложений.

   - Откройте `https://admin.microsoft.com/AdminPortal/Home` .
   - В **центрах администрирования** выберите **SharePoint** центр администрирования.
   - Выберите **дополнительные функции** из меню боковой панели.
   - Нажмите **кнопку Открыть** в **приложениях**.
   - Щелкните **Каталог приложений**.

1. Выберите **Распределить приложения для SharePoint.**

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="Распространение приложений для SharePoint.":::

1. Выберите **Upload**.

1. Нажмите **кнопку Выберите файл**.

1. Найдите `{project}.sppkg` файл, расположенный в `SPFx/sharepoint/solution` папке в проекте.  Нажмите **кнопку Открыть**.

1. Нажмите кнопку **ОК**.

1. Автоматически SharePoint развертывания.  **Убедитесь, что это решение доступно для всех сайтов** в организации проверяется, а затем нажмите **кнопку Развертывание**.

1. Выберите **вкладку FILES.**

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="Выберите вкладку файлы в каталоге SharePoint приложения.":::

1. выберите развернутый пакет, затем нажмите синхронизацию Teams **в** ленте.

    > [!Note]
    > Процесс синхронизации Teams может занять несколько минут.  В правой части браузера вы увидите сообщение, указывающее, что приложение успешно синхронизируется с Teams.

Откройте приложение Teams (или во `https://teams.microsoft.com` входе).  Нажмите тройную точку на боковую панель, а затем выберите **все приложения**.  Приложение будет размещено в **приложениях, построенных для вашей категории org.**  Вы можете добавить приложение оттуда.

:::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="Снимок экрана, показывающий приложение в Teams":::

## <a name="next-steps"></a>Дальнейшие действия

Узнайте о других методах создания Teams приложений:

- [Создание приложения Teams с React](first-app-react.md)
- [Создание приложения Teams с помощью Blazor](first-app-blazor.md)
- [Создание приложения-бота для разговоров](first-app-bot.md)
- [Создать расширение для обмена сообщениями](first-message-extension.md)