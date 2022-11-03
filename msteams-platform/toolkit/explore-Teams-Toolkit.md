---
title: Обзор набора средств Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете об изучении набора средств Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 0fa31c52b206738cfb174519fc6d3c445b604a8e
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833130"
---
# <a name="explore-teams-toolkit"></a>Обзор набора средств Teams

В этом документе вы узнаете о различных элементах пользовательского интерфейса, а также описании и базовом использовании набора средств Teams для Visual Studio Code и Visual Studio.

::: zone pivot="visual-studio-code"

## <a name="teams-toolkit-for-visual-studio-code-basic-ui-elements"></a>Набор средств Teams для Visual Studio Code базовых элементов пользовательского интерфейса

После установки набора средств Teams вы увидите пользовательский интерфейс Набора средств Teams, как показано на следующем рисунке:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/overview1.png" alt-text="Обзор набора средств Teams":::

| Серийный номер | Элементы пользовательского интерфейса | Определение |
| --- | --- |
| 1 | **Начало работы** | Ознакомьтесь с набором средств Teams. |
| &nbsp; | **Учебники** | Доступ к различным руководствам. |
| &nbsp; | **Документация** | Получите доступ к документации разработчика Microsoft Teams. |
| 2 | **Создание приложения Teams** | Создайте приложение Teams на основе ваших требований. |
| 3 | **Просмотр примеров** | Создайте приложения разных типов на основе существующих примеров. |
| 4 | **Открыть папку** | Откройте существующее приложение Teams. |
| 5 | **Создать файл** | Создайте новый файл. |
| &nbsp; | **Открыть файл** | Откройте существующий файл. |
| &nbsp; | **Открыть папку** | Откройте существующую папку. |
| 6 | **Последние** | Просмотр последних файлов. |

### <a name="exploring-the-teams-toolkit-task-pane"></a>Изучение области задач Набора средств Teams

Вы можете просмотреть другие элементы пользовательского интерфейса в области задач в наборе средств Teams. Область задач отображается только после создания приложения с помощью набора средств Teams. В следующем видео вы узнаете о процессе создания нового приложения Teams. После этого вы сможете просмотреть область задач в наборе средств Teams.

   ![Создание приложения Teams](~/assets/videos/javascript-tab-app1.gif)

После создания нового приложения Teams вы увидите структуру каталогов приложения на левой панели и файл сведений на правой панели.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/first-page.png" alt-text="Первая страница набора средств Teams":::

Давайте рассмотрим пользовательский интерфейс Набора средств Teams.

 На панели инструментов Visual Studio Code для набора средств Teams относятся следующие значки:

| Значок | Описание |
| --- | --- |
| **Обозреватель** :::image type="icon" source="../assets/images/teams-toolkit-v2/file-explorer-icon.PNG":::  | Просмотр структуры каталогов приложения. |
| **Запуск и отладка** :::image type="icon" source="../assets/images/teams-toolkit-v2/run-debug-icon.PNG":::  | Запуск локального или удаленного процесса отладки. |
| **Набор средств Teams** :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: | Просмотр области задач в наборе средств Teams. |

В области задач отображаются следующие разделы:

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/accounts1.png" alt-text="Раздел учетных записей":::
   :::column-end:::
   :::column span="":::

        Для разработки приложения Teams вам потребуются следующие учетные записи:
        
        * **Войдите в M365**: используйте учетную запись Microsoft 365 с действительной подпиской E5 для создания приложения.

        * **Войдите в Azure**. Используйте учетную запись Azure для развертывания приложения в Azure. Вы можете [создать бесплатную учетную запись Azure](https://azure.microsoft.com/free/) перед началом работы.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/environment1.png" alt-text="Раздел &quot;Среда&quot;":::
   :::column-end:::
   :::column span="":::

        Чтобы развернуть приложение Teams, вам потребуются следующие среды:
        
       * **local**: разверните приложение в локальной среде по умолчанию с конфигурациями среды локального компьютера.

        * **dev**: разверните приложение в среде разработки по умолчанию с конфигурациями удаленной или облачной среды. При необходимости вы можете создать дополнительные среды.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/development.png" alt-text="Раздел &quot;Разработка&quot;":::
   :::column-end:::
   :::column span="":::

        Чтобы создать и настроить приложение Teams, вам потребуются следующие функции:
        
       * **Создание приложения Teams**. Используйте мастер набора средств для подготовки шаблонов проектов для разработки приложений.

        * **Просмотр примеров**. Выберите любое из примеров приложений Teams Toolkit. Набор средств скачивает код приложения из GitHub, и вы можете создать пример приложения.
        
        * **Добавление функций**. Добавьте другие необходимые возможности Teams в приложение Teams во время разработки и добавьте дополнительные облачные ресурсы, подходящие для вашего приложения.
       
        * **Изменить файл манифеста**. Измените интеграцию приложения Teams с клиентом Teams.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deployment1.png" alt-text="Раздел развертывания":::
   :::column-end:::
   :::column span="":::

        Для подготовки, развертывания и публикации приложения Teams требуются следующие функции:
        
        * **Подготовка в облаке**. Выделение ресурсов Azure для приложения. Набор средств Teams интегрирован с Azure Resource Manager.

        * **Пакет метаданных Zip Teams**. Создайте пакет приложения, который можно отправить в Teams или на портал разработчика. Он содержит манифест приложения и значки приложения.
        
        * **Развертывание в облаке**. Разверните исходный код в Azure.
       
        * **Публикация в Teams**. Опубликуйте разработанное приложение и распространите его в таких областях, как личная, командная, канал или организация.
        
        * **Портал разработчика для Teams**. Используйте портал разработчика для настройки приложения Teams и управления ими. 
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/help-and-feedback1.png" alt-text="Раздел справки и отзывов":::
   :::column-end:::
   :::column span="":::

        Чтобы получить доступ к дополнительным сведениям о наборе средств Teams. Вам потребуется следующая документация и ресурсы.
        
        * **Начало работы**. Просмотрите справку По началу работы с набором средств Teams в Visual Studio Code.

        * **Учебники**. Выберите для доступа к различным руководствам.
        
        * **Документация**. Выберите, чтобы получить доступ к документации разработчика Microsoft Teams.
       
        * **Сообщите о проблемах на сайте GitHub**. Выберите для доступа к странице GitHub и вызовите проблемы.
   :::column-end:::
:::row-end:::

::: zone-end

::: zone pivot="visual-studio"

## <a name="explore-teams-toolkit-for-visual-studio"></a>Обзор набора средств Teams для Visual Studio

После установки Набора средств Teams можно просмотреть параметры набора средств Teams двумя разными способами:

# <a name="project"></a>[Проект](#tab/prj)

Доступ к набору средств Teams можно получить в **разделе Project**.

1. Выберите **Набор средств Project** > **Teams**.
1. Теперь вы можете получить доступ к различным параметрам набора средств Teams.

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu_1.png" alt-text="Меню операций набора средств Teams":::

# <a name="solution-explorer"></a>[Обозреватель решений](#tab/solutionexplorer)

   Вы можете получить доступ к набору средств Teams **в разделе Обозреватель решений**.

1. Выберите **Вид** >  **Обозреватель решений**, чтобы просмотреть панель Обозреватель решений.
1. Щелкните **правой** кнопкой мыши проект.
1. Выберите **Набор средств Teams** , чтобы получить доступ к различным параметрам набора средств Teams.

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu1_1.png" alt-text="Операции с набором средств Teams из Project":::

   > [!NOTE]
   > В этом сценарии проект называется **MyTeamsApp1**.

---

После создания проекта Teams вы можете выполнять следующие функции в наборе средств Teams для Visual Studio:

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-menu-options.png"alt-text="Операции с набором средств Teams из меню &quot;Проект&quot;":::

|Функция  |Описание  |
|---------|---------|
|Подготовка зависимостей приложений Teams     |Перед выполнением локальной отладки выполните этот шаг, он поможет вам настроить локальные зависимости отладки и зарегистрировать приложение Teams на платформе Teams. Вам нужна учетная запись Microsoft 365. Дополнительные сведения см. в статье [Локальная отладка приложения Teams с помощью Visual Studio.](debug-local.md)         |
|Открыть файл манифеста     |Чтобы открыть файл манифеста Teams, можно навести указатель мыши на параметры, чтобы просмотреть значения. Дополнительные сведения см. в разделе [Изменение манифеста приложения Teams с помощью Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md).         |
|Обновление манифеста на портале разработчика Teams     |При обновлении файла манифеста только после этого файл манифеста можно повторно развернуть в Azure без повторного развертывания всего проекта. Используйте эту команду, чтобы обновить изменения в удаленном режиме. Дополнительные сведения см. в разделе [Изменение манифеста приложения Teams с помощью Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md).       |
|Подготовка в облако     |Этот параметр позволяет создавать ресурсы Azure, в которых размещается приложение Teams. Дополнительные сведения см. в статье [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md).        |
|Развертывание в облаке     |Этот параметр позволяет скопировать код в ресурсы Azure, созданные при выполнении "Подготовка в облако". Дополнительные сведения см. [в статье Развертывание приложения Teams в облаке с помощью Visual Studio](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio).        |
|Предварительный просмотр в Teams     |Этот параметр запускает веб-клиент Teams и позволяет просматривать приложение Teams в браузере.         |
|Zip-пакет приложения     |Этот параметр создает пакет приложения Teams в папке `Build` в проекте. Вы можете отправить пакет в клиент Teams и запустить приложение Teams.         |

::: zone-end

## <a name="see-also"></a>См. также

* [Установка набора средств Teams](install-Teams-Toolkit.md)
* [Создание нового приложения Teams с помощью "Инструментов Teams"](create-new-project.md)
* [Подготовка к созданию приложений с помощью Microsoft Teams Toolkit](build-environments.md)
* [Подготовка облачных ресурсов с помощью набора средств Teams](provision.md)
* [Создание приложения Teams в Visual Studio](create-new-project.md#create-new-teams-app-in-visual-studio)
* [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
* [Развертывание приложения Teams в облаке с помощью Visual Studio](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)

<!--  
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ui-elements.png" alt-text="UI Elements":::

|Section|Features|Details
|---------|---------|--------|
| **1. ACCOUNTS** | &nbsp; | &nbsp; |
| &nbsp; |Microsoft 365 account|  Use your Microsoft 365 account with a valid E5 subscription for building your app.|
| &nbsp; | Azure Account |  Use your Azure account for deploying app on Azure. You can [create a free Azure account](https://azure.microsoft.com/free/) before you start.|
|**2.ENVIRONMENT** |  &nbsp; | &nbsp;|
| &nbsp; |Local |Deploy your app in the default local environment with local machine environment configurations.|
| &nbsp; | Dev |Deploy your app in the default dev environment with remote or cloud environment configurations. You can create more environments, as you need.|
| **3.DEVELOPMENT** | &nbsp; | &nbsp; |
| &nbsp; | Create a new Teams app | Teams Toolkit helps you to create and customize your Teams app project that makes the Teams app development work simpler. Create a new Teams app helps you to start with Teams app development by creating new Teams project using Teams Toolkit either by using **Create new project**|
| &nbsp; | View Samples | Select any of Teams Toolkit's sample apps. The toolkit downloads the app code from GitHub, and you can build the sample app.|
| &nbsp; | Add Features | It helps you to add additional Teams capabilities such as **Tab** or **Bot** or **Message extension** or **Command bot** or **Notification bot**, or **SSO enabled tab** optionally add Azure resources such as **Azure SQL Database** or **Azure Key Vault**, or **Azure function** or **Azure API Management** which fits your development needs to your current Teams app. You can also add **API connection** or **Single Sign-on** or **CI/CD workflows** for your Teams app.
| &nbsp; | Edit Manifest file | It helps you customize manifest file based on the app requirements |
| **4.DEPLOYMENT** | &nbsp; | &nbsp; |
| &nbsp;| Provision in the cloud | Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager.|
| &nbsp; | Zip Teams metadata package| Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons. |
| &nbsp; | Deploy to the cloud| Deploy the source code to Azure.|
| &nbsp; | Publish to Teams| Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization.|
| &nbsp; | Developer Portal for Teams| It is the primary tool for configuring, distributing, and managing your Microsoft Teams apps. You can collaborate with colleagues on your app, set up runtime environments, and much more. |
| **5.HELP AND FEEDBACK** | &nbsp; | &nbsp; |
| &nbsp; | Get Started |  View the Teams Toolkit Get started help within Visual Studio Code.|
| &nbsp; | Tutorials| Select to access different tutorials.|
| &nbsp; | Documentation| Select to access the Microsoft Teams Developer Documentation.|
| &nbsp; | Report issues on GitHub| It helps to get **Quick support** from product expert. Browse the existing issues before you create a new one, or visit [StackOverflow tag `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) to submit feedback.|
| **6.Explorer** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | It helps to view the directory structure of your app.|
| **7.Run and Debug** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | To start the local or remote debug process.|
-->
