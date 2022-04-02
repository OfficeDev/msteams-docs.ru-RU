---
title: Развертывание в облаке
author: MuyangAmigo
description: Развертывание приложения в облаке, Azure или SharePoint
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 35a60e718bb97cdcc24de66729e3929b2d21a59f
ms.sourcegitcommit: 2236204ff710f4eca606ceffb233572981f6edbe
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/01/2022
ms.locfileid: "64614532"
---
# <a name="deploy-to-the-cloud"></a>Развертывание в облаке

Teams набор средств позволяет развертывать или загружать код frontend и backend в приложении на предварительно заданные облачные ресурсы в Azure.

* Вкладка, например frontend-приложения, развернута в хранилище Azure и настроена для статического веб-хостинга или сайта sharepoint.
* Дополнительные API развернуты в функциях Azure.
* Расширение бота или обмена сообщениями развернуто в службе приложений Azure.

## <a name="prerequisite"></a>Предварительное условие

* [Установка Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии v3.0.0+.

> [!NOTE]
>
> * Убедитесь, что Teams проекта приложения открыт в коде VS.
> * Перед развертыванием кода проекта в облаке [закачаем облачные ресурсы](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Развертывание Teams с помощью Teams набор средств

Руководства по началу работы помогают развернуть с помощью Teams набор средств. Вы можете использовать следующее для развертывания Teams приложения:

* [Развертывание приложения в Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Развертывание приложения в SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Сведения о рабочей нагрузке Teams приложения

| Teams рабочей нагрузки приложения | Исходный код | Создание артефакта| Целевой ресурс |
|-------------|----------|---------------|---------------|
|Вкладки с React </br> Фронтальная рабочая нагрузка| `yourProjectFolder/tabs`| `tabs/build` |Хранилище Azure |
|Вкладки с SharePoint </br> Фронтальная рабочая нагрузка | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint каталога приложений |
|API на функциях Azure </br> Рабочая нагрузка в задней части | `yourProjectFolder/api`| Неприменимо |Функции Azure |
|Расширения ботов и сообщений </br> Рабочая нагрузка в задней части | `yourProjectFolder/bot` | Неприменимо | Служба приложений Azure |

> [!NOTE]
> Если вы включаете ресурс управления API Azure в проект и запускаете развертывание. Вы можете опубликовать API в функциях Azure в службе управления API Azure.

## <a name="see-also"></a>См. также

* [Добавление дополнительных облачных ресурсов](add-resource.md)
* [Создание и развертывание облачной службы Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Добавление дополнительных Teams приложений](add-capability.md)
* [Развертывание кода проекта с конвейерами CI/CD](use-CICD-template.md)
* [Управление несколькими средами](TeamsFx-multi-env.md)
* [Совместная работа с другими разработчиками в проекте Teams](TeamsFx-collaboration.md)
