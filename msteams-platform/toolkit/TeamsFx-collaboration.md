---
title: Совместная работа над teamsFx Project с помощью Teams Toolkit
author: yanjiang
description: Из этой статьи вы узнаете, как совместно работать над TeamsFx Project с помощью Teams Toolkit и совместной работы с другими разработчиками.
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 0f81990603b3e0275a057c489d7fac44ee0127cc
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142061"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>Совместная работа над проектом Teams с помощью набора средств Teams

Несколько разработчиков могут совместно выполнять отладку, подготовку и развертывание для одного проекта TeamsFx, но для этого необходимо вручную задать соответствующие разрешения приложения Teams и Microsoft Azure Active Directory (Azure AD). Teams Toolkit поддерживает функцию совместной работы, позволяющую разработчикам и владельцу проекта приглашать других разработчиков или участников совместной работы в проект TeamsFx для отладки, подготовки и развертывания того же проекта TeamsFx.

## <a name="prerequisites"></a>Предварительные условия

* Подписка на Microsoft 365
* Azure с действительной подпиской
  
  Дополнительные сведения о разных учетных записях см. в статье о подготовке учетных записей к [созданию Teams приложения](accounts.md).

* [Установка Teams Toolkit версии](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) 3.0.0 и выше

> [!TIP]
> Убедитесь, что в Teams открыт проект приложения Visual Studio Code.

## <a name="collaborate-with-other-developers"></a>Совместная работа с другими разработчиками

Следующие списки помогут нам понять процесс совместной работы и его ограничения.

* Владелец проекта

  > [!NOTE]
  > Перед добавлением участников совместной работы для среды владельцу проекта необходимо [сначала](provision.md) подготовить проект.

  1. В **разделе ENVIRONMENT** в Teams Toolkit выберите **участников совместной работы**. В нем отображаются параметры добавления **Microsoft 365 Teams App (с Azure AD App)** Owners и **List Microsoft 365 Teams App (с Azure AD App) Owners**, как показано на следующих изображениях:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="Сотрудников":::

  2. Выберите **add Microsoft 365 Teams App (with Azure AD App) Owners** (Добавить Azure AD App) и добавьте другой адрес электронной почты Microsoft 365 учетной записи в качестве участника совместной работы. Добавляемая учетная запись должна находиться в том же клиенте, что и владелец проекта, для удаленной отладки, как показано на рисунке:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="добавление envi":::

  3. Чтобы просмотреть участников совместной работы в текущей среде, выберите "Список Microsoft 365 Teams **App( с Azure AD App)** "Владельцы", а затем участники совместной работы будут перечислены в выходном канале, как показано на следующем рисунке:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="list":::

  4. Отправка проекта в GitHub

     > [!NOTE]
     > Добавленные участники совместной работы не получают никаких уведомлений. Владелец Project должен уведомить участника совместной работы.

* Как участник совместной работы над проектом

  1. Клонируйте проект из GitHub.
  2. Войдите в Microsoft 365 учетной записи.
  3. Войдите в учетную запись Azure с разрешением участника для всех ресурсов Azure, используемых в проекте.
  4. Чтобы просмотреть Teams, разверните проект на удаленном компьютере.
  5. Запустите удаленный компьютер, чтобы получить предварительную версию Teams приложения.

     > [!NOTE]
     > Участники совместной работы должны войти с помощью учетной записи, добавляемой владельцем проекта в одном клиенте с владельцем проекта. Дополнительные сведения см. в [статье о сборке и запуске Teams в удаленной среде](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch).

### <a name="limitations"></a>Ограничения

Если вы хотите удалить участников совместной работы из Teams Toolkit, необходимо удалить их вручную, так как вы не можете удалить их напрямую. Чтобы удалить участников совместной работы вручную, сделайте следующее:

* Использование портала разработчика

  * Перейдите [на Teams разработчика](https://dev.teams.microsoft.com/home) и выберите Teams по имени или идентификатору приложения.
  * Выберите **"Владельцы** " на левой панели.
  * Выберите и удалите участника совместной работы.

* Использование Azure Active Directory

  * Перейдите [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), выберите **регистрацию** приложения на левой панели и найдите Azure AD App.
  * Выберите **"Владельцы**" на левой панели Azure AD странице управления приложениями.
  * Выберите и удалите участника совместной работы.

   > [!NOTE]
   >
   > * Участник совместной работы, добавленный в проект, не получает никаких уведомлений. Project владелец должен уведомить участника совместной работы в автономном режиме.
   > * Разрешения, связанные с Azure, должны быть задано администратором подписки Azure вручную в портал Azure. Учетная запись Azure должна иметь роль участника для подписки, чтобы разработчики могли совместно подготавливать и развертывать проект TeamsFx.

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов](provision.md)
* [Развертывание приложения Teams в облаке](deploy.md)
* [Управление несколькими средами](TeamsFx-multi-env.md)
