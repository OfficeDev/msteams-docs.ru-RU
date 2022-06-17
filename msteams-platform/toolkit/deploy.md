---
title: Развертывание в облаке
author: MuyangAmigo
description: В этом модуле вы узнаете, как развернуть приложение в облаке, Azure или SharePoint и развернуть Teams с помощью Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: f7870a81c221182c98a0619d99c7cce255fcc170
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142054"
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
