---
title: Начало работы — создайте первое Teams с помощью SPFx
author: zhenyasav
description: Узнайте, как создать настраиваемую вкладку с помощью SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.localizationpriority: none
ms.openlocfilehash: 36aa779db0c45ab3724673cb0030a97cceef6a78
ms.sourcegitcommit: 72de146d11e81fd9777374dd3915ad290fd07d82
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2021
ms.locfileid: "59360816"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a>Сборка и запуск первого Microsoft Teams с помощью SharePoint Framework (SPFx)

В этом руководстве вы узнаете, как создать новое приложение Microsoft Teams в SharePoint Framework SPFx, которое реализует простое личное приложение. Например, личное *приложение включает* набор вкладок для индивидуального использования. Во время руководства вы узнаете о структуре приложения Teams, локальном запуске приложения и развертывании приложения для SharePoint.

## <a name="before-you-begin"></a>Прежде чем начать

Убедитесь, что среда разработки настроена путем установки необходимых условий.

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)

## <a name="get-organized"></a>Упорядочьте работу

Помимо необходимых условий, необходимо также быть администратором для SharePoint веб-сайтов.  Здесь вы развернете приложение для размещения.  Если вы используете клиента программы разработчика M365, используйте учетную запись администратора, созданную при регистрации для программы.  

## <a name="create-your-project"></a>Создание проекта

Используйте набор средств Teams для создания своего первого проекта.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Откройте Visual Studio Code.
1. Выберите значок Teams на боковой панели, чтобы открыть Teams набор средств.

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. Выберите **Создать проект**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. Выберите **Создать приложение Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания проекта":::

1. В разделе **Выбор возможностей** выберите **вкладку и** выберите **ОК.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. В разделе **Тип типа хостинга Frontend** выберите SharePoint Framework **(SPFx).**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Снимок экрана: выбор размещения для нового приложения.":::

1. В разделе **Framework** выберите **React**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Выбор Framework":::

1. При запросе имени **Вебпарта** нажмите **кнопку Ввод,** чтобы принять по умолчанию.

1. При запросе **описания Вебпарта** нажмите **кнопку Ввод,** чтобы принять по умолчанию.

1. При запросе языка **программирования** нажмите **кнопку Ввод,** чтобы принять по умолчанию.

1. Выберите папку рабочей области.  В папке рабочей области будет создана папка для создаваемого проекта.

1. Введите подходящее имя для приложения, например `helloworld`.  Имя приложения должно состоять только из букв и цифр.  Чтобы продолжить, нажмите клавишу **ВВОД**.

   Создание приложения Teams займет несколько секунд.

# <a name="command-line"></a>[Командная строка](#tab/cli)

Используйте для создания первого проекта интерфейс командной строки `teamsfx`.  Начните с папки, в которой будет создана папка проекта.

``` bash
teamsfx new
```

Интерфейс командной строки выдаст несколько вопросов, ответы на которые используются для создания проекта.  Каждый вопрос сопровождается подсказкой о том, как на него отвечать (например, использовать клавиши со стрелками для выбора варианта).  Ответив на вопрос, подтвердите свой выбор, нажав клавишу **ВВОД**.

1. Выберите **Создать приложение Teams**.
1. Выберите **вкладку**.
1. Выберите **SharePoint Framework (SPFx)** переднего размещения.
1. Выберите **React.**
1. Нажмите **кнопку Введите** имя **Вебпарта.**
1. Нажмите **кнопку Ввод** для **описания Webpart**.
1. Нажмите **кнопку Ввод** для **языка программирования**.
1. Нажмите клавишу **ВВОД**, чтобы выбрать папку рабочей области по умолчанию.
1. Введите подходящее имя для приложения, например `helloworld`.  Имя приложения должно состоять только из букв и цифр.

   После ответа на все вопросы будет создан проект.

---

- [Узнайте больше о разработке для SharePoint Framework](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a>Знакомство с исходным кодом

Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально](#run-your-app-locally).

После настройки Teams набор средств проекта у вас есть компоненты для создания базового личного приложения для Teams, которое находится в SharePoint Framework.  Каталоги и файлы проекта отображаются в области проводника Visual Studio Code.

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Снимок экрана: файлы проектов приложения для личного приложения в Visual Studio Code.":::

Набор средств автоматически формирует шаблоны в каталоге проекта на основе возможностей, добавленных во время установки. Набор средств Teams сохраняет свое состояние для вашего приложения в каталоге `.fx`. 

- Параметры, выбранные при создании проекта, хранятся в `.fx/settings.json`.
- Состояние проекта хранится в `.fx/env.*.json` .

Кроме того Teams сведения о приложении хранятся в `appPackage` каталоге.

- Значки приложений, хранимые как PNG-файлы в `appPackage/color.png` и `appPackage/outline.png`.
- Манифест приложения для публикации на портале разработчиков для Teams хранится в `appPackage/manifest.source.json` .


Так как вы выбрали проект SPFx Webpart, к вашему пользовательскому интерфейсу имеют отношение следующие файлы:

- Папка содержит `SPFx/src/webparts/{webpart}` веб-SPFx веб-части.
- В `.vscode/launch.json` файле описываются конфигурации отладки, доступные в палитре отладки.

Дополнительные сведения о веб SharePoint веб-Teams для Teams, обратитесь к документации [SharePoint.](/sharepoint/dev/spfx/build-for-teams-overview)

## <a name="run-your-app-locally"></a>Локальный запуск приложения

Teams набор средств позволяет локализовку приложения и запуск его через [SharePoint Framework Workbench.](/sharepoint/dev/spfx/debug-in-vscode)

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a>Создайте и запустите приложение локально в Visual Studio Code

Чтобы создать и запустить приложение локально, выполните следующие действия.

1. С Visual Studio Code нажмите **клавишу F5.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="Снимок экрана, показывающий, как SPFx приложение в локальной работе.":::

   > [!NOTE]
   > При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.  Окно браузера автоматически открывается и загружает SharePoint Workbench после завершения сборки.  Для завершения может потребоваться от 3 до 5 минут.

   После загрузки SharePoint workbench.

   >[!NOTE]
   > Набор средств при необходимости выведет запрос на установку локального сертификата. Этот сертификат позволяет Teams загружать приложение из `https://localhost`. Выберите "Да", когда появится следующее диалоговое окно:

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Снимок экрана: запрос на установку SSL-сертификата, чтобы разрешить Teams загрузку вашего приложения из localhost.":::

1. Выберите **Добавить значки Webpart +** для добавления веб-части.

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

   Вы можете отслеживать ход, наблюдая за диалогами в правом нижнем углу.  Через несколько секунд вы увидите следующее уведомление:

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Снимок экрана, показывающий полный диалоговое окно подготовка.":::

1. После завершения подготовка выберите **Развертывание в облаке.**

1. В настоящее время автоматическое развертывание не доступно.  Диалоговое окно будет всплывающее запрос на сборку и развертывание вручную. Выберите **пакет SharePoint сборки.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="Снимок экрана для диалогового пакета Build Sharepoint Package":::

# <a name="command-line"></a>[Командная строка](#tab/cli)

В окне терминала:

1. Запустите `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   Возможно, вам будет предложено войти в свою подписку Azure.  При необходимости вам будет предложено выбрать подписку Azure для использования для ресурсов Azure.

   > [!NOTE]
   > Для размещения приложения всегда используются некоторые ресурсы Azure.

1. Запустите `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

1. При запросе выберите **пакет сборки SharePoint.**

---

Пакет SharePoint находится в рамках `SPFx/sharepoint/solution` проекта.  Upload пакет для SharePoint:

1. Войдите в консоль администратора M365, а затем перейдите в каталог SharePoint приложений.

   1. Откройте `https://admin.microsoft.com/AdminPortal/Home` .
   1. В **центрах администрирования** выберите **SharePoint** центр администрирования.
   1. Выберите **дополнительные функции** из меню боковой панели.
   1. Нажмите **кнопку Открыть** в **приложениях**.
   1. Щелкните **Каталог приложений**.

1. Выберите **Распределить приложения для SharePoint.**

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="Распространение приложений для SharePoint.":::

1. Выберите **Upload**.

1. Выберите **выберите файл**.

1. Найдите `{project}.sppkg` файл в `SPFx/sharepoint/solution` папке в проекте. Выберите **Открыть**.

1. Нажмите кнопку **ОК**.

1. Автоматически SharePoint развертывания. **Убедитесь, что это решение доступно всем сайтам** организации. Затем выберите **Развертывание.**

1. Выберите **вкладку FILES.**

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="Выберите вкладку файлы в каталоге SharePoint приложения.":::

1. выберите развернутый пакет, а затем Teams **синхронизацию** с верхним правом углу.

    > [!Note]
    > Процесс синхронизации Teams может занять несколько минут.  В правой части браузера вы увидите сообщение, указывающее, что приложение успешно синхронизируется с Teams.

   Откройте приложение Teams (или во `https://teams.microsoft.com` входе).  Нажмите тройную точку на боковую панель, а затем выберите **все приложения**.  Приложение будет размещено в **приложениях, построенных для вашей категории org.**  Вы можете добавить приложение оттуда.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="Снимок экрана, показывающий приложение в Teams":::

## <a name="see-also"></a>См. также

* [Обзор учебников](code-samples.md)
* [Создание бота беседы](first-app-bot.md)
* [Создание расширения для обмена сообщениями](first-message-extension.md)
* [Примеры кода](https://github.com/OfficeDev/Microsoft-Teams-Samples)
