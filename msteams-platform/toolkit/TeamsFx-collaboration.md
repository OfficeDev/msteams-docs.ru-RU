---
title: Совместное использование Project TeamsFx с Teams набор средств
author: yanjiang
description: Совместное использование Project TeamsFx с Teams набор средств
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9a39b84c3cfa94c410df5774d4a177535e1cfdd6
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212351"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>Совместное использование Teams с помощью Teams набор средств

Несколько разработчиков могут совместно отладить, разработать и развернуть один и тот же проект TeamsFx, но для этого необходимо вручную установить нужные разрешения Teams App и Azure AD App.Teams набор средств поддерживает функцию совместной работы, позволяющую разработчикам и владельцу проекта приглашать других разработчиков или сотрудников в проект TeamsFx для отладки, предоставления и развертывания одного и того же проекта TeamsFx.

## <a name="prerequisites"></a>Предварительные требования

* Предпосылки учетной записи

    Для предоставления облачных ресурсов необходимо иметь следующие учетные записи. Дополнительные сведения см. в приложении подготовка учетных записей [для создания Teams приложения.](accounts.md)

  * Подписка на Microsoft 365
  * Azure с допустимой подпиской

* [Установка Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии v3.0.0+.

> [!TIP]
> Убедитесь, что Teams приложения открыт в коде VS.

## <a name="collaborate-with-other-developers"></a>Сотрудничество с другими разработчиками

В следующем списке мы понимаем процесс совместной работы и его ограничения:

### <a name="as-project-owner"></a>Как владелец проекта

> [!NOTE]
> Прежде чем добавлять сотрудников в среду, владельцу проекта необходимо [сначала обуявить](provision.md) проект.

* В **разделе ENVIRONMENT** на Teams набор средств выберите **сотрудников.** В нем отображаются параметры Add **M365 Teams App (с AAD App)** Owners и **List M365 Teams App (с** AAD App), как показано на следующих изображениях:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="сотрудники":::

* Выберите **Add M365 Teams App (с AAD App) и** добавьте другой адрес электронной почты учетной записи M365 в качестве соавтора. Добавленная учетная запись должна быть на том же клиенте, что и владелец проекта для удаленного отладки, как показано на изображении:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="добавление envi":::

* Чтобы просмотреть сотрудников в текущей среде, выберите list **M365 Teams App (с AAD App) Owners,** после чего сотрудники перечислены в канале вывода, как показано на следующем изображении:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="list":::

* Нажмите кнопку GitHub.

> [!NOTE]
> Только что добавленный сотрудник не получает уведомлений. Project должен уведомить об этом коллегу.

### <a name="as-project-collaborator"></a>Как сотрудник проекта

* Клонировать проект из GitHub.
* Войдите в учетную запись M365.
* Войдите в учетную запись Azure, которая имеет разрешение участника для всех ресурсов Azure, используемых в этом проекте.
* Чтобы просмотреть Teams приложение, разверните проект на удаленный.
* Запустите удаленный доступ, чтобы просмотреть Teams приложения.

Дополнительные сведения см. в [приложении build and run your Teams в удаленной среде.](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch)

> [!NOTE]
> Сотрудники должны войти в систему с помощью учетной записи, добавленной владельцем проекта, которая находится под тем же клиентом с владельцем проекта.

### <a name="limitation"></a>Ограничение

Вы не можете удалить сотрудников непосредственно из Teams набор средств расширения. Выполните следующие действия, чтобы удалить сотрудников вручную:

  1. Перейдите Teams портал разработчика и выберите Teams приложение по имени или ID приложения.
  2. Выберите **Owners** с левой панели.
  3. Выберите и удалите соавтора.
  4. Перейдите [Azure Active Directory,](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)выберите **регистрацию приложения** с левой панели и найдите приложение Azure AD.
  5. Выберите **Owners** из левой панели на странице управления приложениями Azure AD.
  6. Выберите и удалите соавтора.

> [!NOTE]
> * Сотрудник, добавленный в проект, не будет получать никаких уведомлений. Project должен уведомить об этом коллегу в автономном режиме.
> * Соответствующие разрешения Azure должны устанавливаться администратором подписки Azure вручную на портале Azure. Учетная запись Azure должна иметь роль участника для подписки, чтобы разработчики могли работать вместе для обеспечения и развертывания проекта TeamsFx.

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов](provision.md)
* [Развертывание приложения Teams в облаке](deploy.md)
* [Управление несколькими средами](TeamsFx-multi-env.md)
