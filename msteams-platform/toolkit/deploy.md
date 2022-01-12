---
title: Развертывание в облаке
author: MuyangAmigo
description: Развертывание в облаке
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 0eeda4842ad3f0443d46b5075b1520b0042130ec
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768380"
---
# <a name="deploy-to-the-cloud"></a>Развертывание в облаке

Teams набор средств позволяет развертывать или загружать код frontend и backend в приложении на предварительно заданные облачные ресурсы в Azure.

* Вкладка, например frontend-приложения, развернута в хранилище Azure и настроена для статического веб-хостинга или сайта sharepoint.
* Дополнительные API развернуты в функциях Azure.
* Расширение бота или обмена сообщениями развернуто в службе приложений Azure.

## <a name="prerequisite"></a>Предварительное условие

* [Установка Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии v3.0.0+.

> [!NOTE]
> * Убедитесь, Teams проект приложения открыт в коде VS.
> * Перед развертыванием кода проекта в облаке [необходимо уместить облачные ресурсы.](provision.md)

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Развертывание Teams с помощью Teams набор средств

Руководства по началу работы помогают развернуть с помощью Teams набор средств. Вы можете использовать следующее, чтобы развернуть Teams приложение:
* [Развертывание приложения в Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Развертывание приложения для SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

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
* [Сотрудничество с другими разработчиками в Teams проекте](TeamsFx-collaboration.md)
