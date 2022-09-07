---
title: Развертывание в облаке
author: MuyangAmigo
description: В этом модуле вы узнаете, как развернуть приложение в облаке, Azure или SharePoint и развернуть приложения Teams с помощью Набора средств Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9ad2c9d16901990344ca521599b94b84b0e76217
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616928"
---
# <a name="deploy-teams-app-to-the-cloud"></a>Развертывание приложения Teams в облаке

Набор средств Teams позволяет развертывать и загружать код интерфейсной и серверной частей вашего приложения в ваши подготовленные ресурсы в облаке Azure. В облаке можно развернуть следующее:

* Вкладка, например серверные приложения, развертывается в хранилище Azure и настраивается для статического размещения веб-сайтов или сайта SharePoint.
* Для функций Azure развертываются серверные API.
* Бот или расширение для сообщений развертываются в службе приложений Azure.

  > [!NOTE]
  > Перед развертыванием кода приложения в облаке Azure необходимо успешно завершить подготовку [облачных ресурсов](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Развертывание приложений Teams с помощью набора средств Teams

Руководства по началу работы помогут вам выполнить развертывание с помощью Набора средств Teams. Для развертывания приложения Teams можно использовать следующие руководства.

* [Развертывание приложения в Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Развертывание приложения в SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Сведения о рабочей нагрузке приложения Teams

| Рабочая нагрузка приложения Teams | Исходный код | Артефакт сборки| Целевой ресурс |
|-------------|----------|---------------|---------------|
|Вкладки с React </br> Рабочая нагрузка интерфейсной части| `yourProjectFolder/tabs`| `tabs/build` |Хранилище Azure |
|Вкладки с SharePoint </br> Рабочая нагрузка интерфейсной части | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |Каталог приложений SharePoint |
|API в функциях Azure </br> Рабочая нагрузка серверной части | `yourProjectFolder/api`| Неприменимо |Функции Azure |
|Расширения для сообщений и ботов </br> Рабочая нагрузка серверной части | `yourProjectFolder/bot` | Неприменимо | Служба приложений Azure |

> [!NOTE]
> Когда вы включаете ресурс управления API Azure в проект и активируете развертывание, вы можете опубликовать API-интерфейсы в функциях Azure в службе управления API Azure.

## <a name="see-also"></a>См. также

* [Создание и развертывание облачной службы Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Создание многопользовательских приложений Teams](add-capability.md)
* [Добавление облачных ресурсов в приложение Microsoft Teams](add-resource.md)
