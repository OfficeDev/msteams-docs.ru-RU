---
title: Развертывание в облаке
author: MuyangAmigo
description: Развертывание приложения в облаке, Azure или SharePoint
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 1d0ade9abed4be212abfb96068626172c4f0f03e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104149"
---
# <a name="deploy-to-the-cloud"></a>Развертывание в облаке

Teams набор средств помогает развертывать и отправлять интерфейсный и внутренний код в приложении в подготовленные облачные ресурсы в Azure.

* Вкладка, например интерфейсные приложения, развертывается в службе хранилища Azure и настраивается для статического веб-размещения или сайта SharePoint.
* Серверные API развертываются в функциях Azure.
* Расширение бота или сообщения развертывается в службе приложений Azure.

## <a name="prerequisite"></a>Предварительное условие

* [Установите Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии 3.0.0 и выше.

> [!NOTE]
>
> * Убедитесь, что Teams открыт проект приложения в VS Code.
> * Перед развертыванием кода проекта в облаке [подготовьте облачные ресурсы](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Развертывание Teams с помощью Teams набор средств

Руководства по началу работы помогут вам выполнить развертывание с помощью Teams набор средств. Чтобы развернуть приложение Teams, можно использовать следующее:

* [Развертывание приложения в Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Развертывание приложения в SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Сведения о рабочей нагрузке Teams приложения

| Teams приложения | Исходный код | Артефакт сборки| Целевой ресурс |
|-------------|----------|---------------|---------------|
|Вкладки с React </br> Интерфейсная рабочая нагрузка| `yourProjectFolder/tabs`| `tabs/build` |Служба хранилища Azure |
|Вкладки с SharePoint </br> Интерфейсная рабочая нагрузка | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint приложения |
|API-интерфейсы в функциях Azure </br> Рабочая нагрузка серверной части | `yourProjectFolder/api`| Неприменимо |Функции Azure |
|Боты и расширения сообщений </br> Рабочая нагрузка серверной части | `yourProjectFolder/bot` | Неприменимо | Служба приложений Azure |

> [!NOTE]
> При включите ресурс управления API Azure в проект и активируете развертывание. API-интерфейсы можно опубликовать в функциях Azure в службе управления API Azure.

## <a name="see-also"></a>См. также

* [Добавление дополнительных облачных ресурсов](add-resource.md)
* [Создание и развертывание облачной службы Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Добавление дополнительных Teams приложений](add-capability.md)
* [Развертывание кода проекта с помощью конвейеров CI/CD](use-CICD-template.md)
* [Управление несколькими средами](TeamsFx-multi-env.md)
* [Совместная работа с другими разработчиками в проекте Teams](TeamsFx-collaboration.md)
