---
title: Общие сведения о наборе средств Teams
author: zyxiaoyuer
description: Общие сведения о наборе средств Teams, установке набора средств Teams и обзор функций набора средств
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
ms.openlocfilehash: f0c09d605e63118755f28804689aa6659ebbb657
ms.sourcegitcommit: 09ee0305b827ad6d1368d892db3824c5dbad886f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2022
ms.locfileid: "65759671"
---
# <a name="teams-toolkit-overview"></a>Общие сведения о наборе средств Teams

Набор средств Teams для Microsoft Visual Studio Code помогает создавать и развертывать приложения Teams с интегрированными удостоверениями, доступом к облачному хранилищу, данным из Microsoft Graph и другим службам в Azure и Microsoft 365 с помощью подхода нулевой конфигурации. Для разработки приложений Teams, аналогичной набору средств Teams для Visual Studio, вы можете использовать средство [CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), состоящее из `teamsfx` набора средств.
Набор средств Teams позволяет создавать, отлаживать и развертывать приложения Teams непосредственно из Visual Studio Code. Разработка приложения с помощью набора средств имеет следующие преимущества.

* Интегрированное удостоверение
* Доступ к облачному хранилищу
* Данные из Microsoft Graph
* Службы Azure и Microsoft 365 с использованием подхода с нулевой конфигурацией

Набор средств Teams объединяет в одном месте все инструменты, необходимые для создания приложения Teams.

## <a name="user-journey-of-teams-toolkit"></a>Путь пользователя при применении набора средств Teams

Набор средств Teams автоматизирует ручную работу и обеспечивает отличную интеграцию ресурсов Teams и Azure. На следующем изображении показан путь пользователя при применении набора средств Teams.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey.png" alt-text="Путь пользователя в наборе средств Teams" border="true":::

Основные вехи этого пути:

1. Начало работы с создания проекта или применения примера приложения Teams.
1. Добавление возможностей или изменение файла манифеста при необходимости.
1. Использование учетной записи Microsoft 365 для создания и отладки приложения Teams.
1. Использование учетной записи Azure для подготовки и развертывания приложения в облаке.
1. Публикация приложения в Teams.

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Установка набора средств Teams для Visual Studio Code

1. Откройте **Visual Studio Code.**
1. Выберите представление расширений (**CTRL+SHIFT+X** / **⌘⇧-X** или **view > Extensions**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="установка":::

1. **Введите Teams Toolkit** в поле поиска.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="Набор средств":::

1. Нажмите кнопку **Установить**.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit.png" alt-text="install toolkit 4.0.0":::

> [!TIP]
> Вы можете установить набор средств Teams из [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

## <a name="take-a-tour-of-teams-toolkit"></a>Обзор набора средств Teams

После установки набора средств вы увидите пользовательский интерфейс набора средств Teams, как показано на следующем изображении.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/Teams-toolkit.png" alt-text="мини-функции":::

Вы **можете выбрать Начало работы**, чтобы изучить Teams Toolkit, или выбрать команду "Создать Teams **App**", чтобы создать Teams проекта. Если у вас есть проект Teams, созданный Teams Toolkit, открытый в Visual Studio Code, вы увидите пользовательский интерфейс Teams Toolkit со всеми функциональными возможностями, как показано на следующем рисунке:

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamstookit1.png" alt-text="Снимок экрана: набор средствteams":::

Давайте рассмотрим темы, рассматриваемые в этом документе.

## <a name="accounts"></a>Учетные записи

Для разработки приложения Teams требуется по крайней мере одна учетная запись Microsoft 365 с действительной подпиской. Если вы хотите разместить свои серверные ресурсы в Azure, также требуется учетная запись Azure. Teams Toolkit поддерживает интегрированный интерфейс для входа, подготовки и развертывания ресурсов Azure. Вы можете [создать бесплатную учетную запись Azure](https://azure.microsoft.com/free/) перед началом работы.

## <a name="environment"></a>Среда

Набор средств Teams помогает создать несколько сред и управлять ими, подготовить и развернуть артефакты в целевой среде для приложения Teams.

### <a name="teamsfx-collaboration"></a>Совместная работа в TeamsFx

Позволяет разработчикам и владельцу проекта приглашать других участников совместной работы в проект TeamsFx для отладки, подготовки и развертывания того же проекта TeamsFx.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamsfx.png" alt-text="Проект Teamsfx":::

## <a name="development"></a>Разработка

Набор средств Teams помогает создавать и настраивать приложения Teams, что упрощает разработку приложений Teams.

### <a name="create-a-new-teams-app"></a>Создание нового приложения Teams

Это поможет начать с разработки Teams, создав новый проект Teams с помощью Teams Toolkit с помощью create **new project** или **Start from a sample**.

### <a name="add-features"></a>Добавление компонентов

Она помогает постепенно добавлять дополнительные Teams, такие как tab или **Bot**, или при необходимости  добавлять ресурсы Azure, такие как **База данных SQL Azure** или **Azure Key Vault**, которые соответствуют вашим потребностям разработки в текущем приложении Teams. Вы также можете добавить рабочие процессы **единого** входа или **CI/CD** для Teams приложения. 

### <a name="edit-manifest-file"></a>Изменение файла манифеста

Помогает изменить интеграцию приложения Teams и клиента Teams.

## <a name="deployment"></a>Развертывание

Во время или после разработки необходимо подготовить, развернуть и опубликовать приложение Teams, прежде чем оно станет доступно пользователям.

### <a name="provision-in-the-cloud"></a>Подготовка в облаке

Интегрируется с диспетчером ресурсов Azure, что позволяет подготавливать ресурсы Azure, необходимые приложению для подхода с использованием кода.

### <a name="deploy-to-the-cloud"></a>Развертывание в облаке

 Помогает развернуть исходный код в Azure.

### <a name="publish-to-teams"></a>Публикация в Teams

После создания приложения вы можете распространять его в разных областях, например для отдельных пользователей, команд, организаций или для всех. Публикация в Teams помогает опубликовать разработанное приложение.

#### <a name="teamsfx-cli"></a>TeamsFx CLI

Это текстовый интерфейс командной строки, который ускоряет разработку приложения Teams, а также включает сценарий CI/CD, в котором можно интегрировать CLI в сценарии для автоматизации.

#### <a name="teamsfx-sdk"></a>Пакет SDK TeamsFx

Позволяет сократить задачи по внедрению удостоверений и доступа к облачным ресурсам до однострочных операторов с нулевой конфигурацией.

## <a name="help-and-feedback"></a>Справка и обратная связь

В этом разделе вы найдете необходимую документацию и ресурсы. Вы можете выбрать **Сообщить о проблемах в GitHub** в наборе средств Teams, чтобы получить **быструю поддержку** от эксперта по продукту. Просмотрите проблемы перед созданием новой проблемы или посетите сайт [StackOverflow с тегом `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit), чтобы отправить отзыв.
<!--  
Let's explore Teams Toolkit features.

| Teams Toolkit Features | Includes | What you can do |
| --- | --- | --- |
| **Accounts** | &nbsp; | &nbsp; |
| &nbsp; | Microsoft 365 account | Use your Microsoft 365 account with a valid E5 subscription for building your app. |
| &nbsp; | Azure account | Use your Azure account for deploying app on Azure. |
| **Environment** | &nbsp; | &nbsp; |
| &nbsp; | local | Deploy your app in the default local environment with local machine environment configurations. |
| &nbsp; | dev | Deploy your app in the default dev environment with remote or cloud environment configurations. You can create more environments, as you need. |
| **Development** | &nbsp; | &nbsp; |
| &nbsp; | Create a new Teams app | Use the toolkit wizard to prepare project scaffolding for app development. |
| &nbsp; | View samples | Select any of Teams Toolkit's 12 sample apps. The toolkit downloads the app code from GitHub, and you can build the sample app. |
| &nbsp; | Add Features | - Add other required Teams capabilities to Teams app during development process. </br> - Add optional cloud resources suitable for your app. |
| &nbsp; | Edit manifest file | Edit the Teams app integration with Teams client. |
| **Deployment** | &nbsp; | &nbsp; |
| &nbsp; | Provision in the cloud | Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager. |
| &nbsp; | Zip Teams metadata package | Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons.  |
| &nbsp; | Deploy to the cloud | Deploy the source code to Azure. |
| &nbsp; | Publish to Teams | Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization. |
| &nbsp; | Developer Portal for Teams | Use Developer Portal to configure and manage your Teams app. |
| **Help and Feedback** | &nbsp; | &nbsp; |
| &nbsp; | Quick start | View the Teams Toolkit Quick start help within Visual Studio Code.  |
| &nbsp; | Tutorial | Select to access different tutorials. |
| &nbsp; | Documentation | Select to access the Microsoft Teams Developer Documentation. |
| &nbsp; | Report issues on GitHub | Select to access GitHub page and raise any issues. |

-->
> [!TIP]
> Просмотрите существующие проблемы перед созданием новой или посетите сайт [StackOverflow с тегом `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit), чтобы отправить отзыв.

## <a name="see-also"></a>Дополнительные ресурсы

* [Создание проекта с помощью набора средств Teams](create-new-project.md)
* [Подготовка учетных записей для создания приложений Teams](accounts.md)
* [Публикация приложений Teams с помощью набора средств Teams](publish.md)
* [Подготовка облачных ресурсов с помощью набора средств Teams](provision.md)
* [Развертывание в облаке](deploy.md)
