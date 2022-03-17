---
title: Развертывание в облаке
author: MuyangAmigo
description: Развертывание приложения в облаке, Azure или SharePoint
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 2e2d288340f3a806857f1e62ae832be0e6c4068c
ms.sourcegitcommit: f9dc32566e87ffc1b2d2bd45f1388aae8f5c9083
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2022
ms.locfileid: "63558819"
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
* [Добавление дополнительных Teams приложений](add-capability.md)
* [Развертывание кода проекта с конвейерами CI/CD](use-CICD-template.md)
* [Управление несколькими средами](TeamsFx-multi-env.md)
* [Совместная работа с другими разработчиками в проекте Teams](TeamsFx-collaboration.md)
