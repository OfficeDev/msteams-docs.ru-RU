---
title: Развертывание в облаке
author: MuyangAmigo
description: Развертывание приложения в облаке, Azure или SharePoint
ms.author: zhany
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 3e9368dcaa87003da2872a500ffaa281092774df
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111572"
---
# <a name="deploy-to-the-cloud"></a>Развертывание в облаке

Набор средств Teams позволяет развертывать и загружать код интерфейсной и серверной частей вашего приложения в ваши подготовленные ресурсы в облаке Azure.

* Вкладка, например серверные приложения, развертывается в хранилище Azure и настраивается для статического размещения веб-сайтов или сайта SharePoint.
* Для функций Azure развертываются серверные API.
* Бот или расширение для сообщений развертываются в службе приложений Azure.

## <a name="prerequisite"></a>Предварительное условие

* [Установите набор средств Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии не ниже 3.0.0.

> [!NOTE]
>
> * Убедитесь, что проект приложения Teams открыт в VS Code.
> * Перед развертывание кода проекта в облаке [подготовьте облачные ресурсы](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Развертывание приложений Teams с помощью набора средств Teams

Руководства по началу работы помогают развертывать с помощью набора средств Teams. Для развертывания приложения Teams можно использовать следующие руководства.

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
> При включении ресурса управления API Azure в проект и активации развертывания. Вы можете публиковать API в функциях Azure в службе управления API Azure.

## <a name="see-also"></a>Дополнительные ресурсы

* [Добавление дополнительных облачных ресурсов](add-resource.md)
* [Создание и развертывание облачной службы Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Добавление возможностей приложения Teams](add-capability.md)
* [Развертывание кода проекта с конвейерами CI/CD](use-CICD-template.md)
* [Управление несколькими средами](TeamsFx-multi-env.md)
* [Совместная работа с другими разработчиками в проекте Teams](TeamsFx-collaboration.md)
