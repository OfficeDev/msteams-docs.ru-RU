---
title: Обзор набора средств Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете об изучении набора средств Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: 0ef95064a1715a64d8f719c54aced7cdc74ecb23
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617352"
---
# <a name="explore-teams-toolkit"></a>Обзор набора средств Teams

В этом документе описаны различные элементы пользовательского интерфейса, а также описание и базовое использование в Наборе средств Teams.

## <a name="teams-toolkit-basic-ui-elements"></a>Базовые элементы пользовательского интерфейса Набора средств Teams

После установки Набора средств Teams вы увидите пользовательский интерфейс Набора средств Teams, как показано на следующем рисунке:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/overview1.png" alt-text="Общие сведения о Наборе средств Teams":::

| Серийный нет | Элементы пользовательского интерфейса | Определение |
| --- | --- |
| 1 | **Начало работы** | Изучите набор средств Teams. |
| &nbsp; | **Учебники** | Доступ к различным руководствам. |
| &nbsp; | **Документация** | Доступ к документации разработчика Microsoft Teams. |
| 2 | **Создание нового приложения Teams** | Создайте новое приложение Teams в соответствии с вашими требованиями. |
| 3 | **Просмотр примеров** | Создавайте различные типы приложений на основе существующих примеров. |
| 4 | **Открыть папку** | Откройте существующее приложение Teams. |
| 5 | **Новый файл** | Создайте файл. |
| &nbsp; | **Открыть файл** | Откройте существующий файл. |
| &nbsp; | **Открыть папку** | Откройте существующую папку. |
| 6 | **Последние** | Просмотрите последние файлы. |

### <a name="exploring-the-teams-toolkit-task-pane"></a>Изучение области задач "Набор средств Teams"

Дополнительные элементы пользовательского интерфейса можно просмотреть в области задач в Наборе средств Teams. Область задач отображается только после создания приложения с помощью Набора средств Teams. В следующем видео показано, как создать приложение Teams, и после этого вы сможете просмотреть область задач в Наборе средств Teams.

   ![Создание приложения Teams](~/assets/videos/javascript-tab-app1.gif)

После создания нового приложения Teams структура каталогов приложения отображается на левой панели, а файл сведений — на правой панели.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/first-page.png" alt-text="Первая страница набора средств Teams":::

Давайте рассмотрим пользовательский интерфейс Набора средств Teams.

 На Visual Studio Code панели инструментов следующие значки относятся к набору средств Teams:

| Значок | Описание |
| --- | --- |
| **Обозреватель** :::image type="icon" source="../assets/images/teams-toolkit-v2/file-explorer-icon.PNG":::  | Просмотр структуры каталогов приложения. |
| **Запуск и отладка** :::image type="icon" source="../assets/images/teams-toolkit-v2/run-debug-icon.PNG":::  | Запуск локального или удаленного процесса отладки. |
| **Набор средств Teams** :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: | Просмотр области задач в Наборе средств Teams. |

В области задач можно просмотреть следующие разделы:

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/accounts1.png" alt-text="Раздел &quot;Учетные записи&quot;":::
   :::column-end:::
   :::column span="":::

        Для разработки приложения Teams вам потребуются следующие учетные записи:
        
        * **Войдите в M365**: используйте учетную запись Microsoft 365 с действительной подпиской E5 для создания приложения.

        * **Войдите в Azure**: используйте учетную запись Azure для развертывания приложения в Azure. Вы можете [создать бесплатную учетную запись Azure](https://azure.microsoft.com/free/) перед началом работы.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/environment1.png" alt-text="Раздел &quot;Среда&quot;":::
   :::column-end:::
   :::column span="":::

        Чтобы развернуть приложение Teams, вам потребуются следующие среды:
        
       * **local**: развертывание приложения в локальной среде по умолчанию с конфигурациями среды локального компьютера.

        * **dev**: развертывание приложения в среде разработки по умолчанию с конфигурациями удаленной или облачной среды. При необходимости вы можете создать дополнительные среды.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/development.png" alt-text="Раздел &quot;Разработка&quot;":::
   :::column-end:::
   :::column span="":::

        Чтобы создать и настроить приложение Teams, вам потребуются следующие функции:
        
       * **Создание нового приложения Teams**. Используйте мастер набора средств для подготовки шаблонов проектов для разработки приложений.

        * **Просмотрите примеры**: выберите любое из примеров приложений Teams Toolkit. Набор средств скачивает код приложения из GitHub, и вы можете создать пример приложения.
        
        * **Добавление функций**. Добавьте другие необходимые возможности Teams в приложение Teams во время разработки и добавьте необязательные облачные ресурсы, подходящие для вашего приложения.
       
        * **Изменение файла манифеста**: изменение интеграции приложений Teams с клиентом Teams.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deployment1.png" alt-text="Раздел &quot;Развертывание&quot;":::
   :::column-end:::
   :::column span="":::

        Чтобы подготовить, развернуть и опубликовать приложение Teams, вам потребуются следующие функции:
        
        * **Подготовка в облаке**. Выделите ресурсы Azure для приложения. Набор средств Teams интегрирован с Azure Resource Manager.

        * **Zip Teams metadata package**: Create the app package that can be uploaded to Teams or Developer Portal. Он содержит манифест приложения и значки приложения.
        
        * **Развертывание в облаке**: развертывание исходного кода в Azure.
       
        * **Публикация в Teams**: публикация разработанного приложения и его распространение в таких областях, как личная, команда, канал или организация.
        
        * **Портал разработчика для Teams**: используйте портал разработчика для настройки приложения Teams и управления ими. 
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/help-and-feedback1.png" alt-text="Раздел справки и отзывов":::
   :::column-end:::
   :::column span="":::

        Чтобы получить дополнительные сведения о Наборе средств Teams. Вам потребуется следующую документацию и ресурсы.
        
        * **Начало работы**. Просмотрите справку по началу работы с Набором средств Teams в Visual Studio Code.

        * **Руководства.** Выберите для доступа к различным руководствам.
        
        * **Документация**. Выберите, чтобы получить доступ к документации разработчика Microsoft Teams.
       
        * **Ведите отчет о проблемах на GitHub**: выберите для доступа к странице GitHub и создайте любые проблемы.
   :::column-end:::
:::row-end:::

## <a name="see-also"></a>См. также

* [Установка Набора средств Teams](install-Teams-Toolkit.md)
* [Создание нового приложения Teams с помощью "Инструментов Teams"](create-new-project.md)
* [Подготовка к созданию приложений с помощью Microsoft Teams Toolkit](build-environments.md)
* [Подготовка облачных ресурсов с помощью Набора средств Teams](provision.md)

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
