---
title: Развертывание в облаке
author: MuyangAmigo
description: Развертывание в облаке
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 3f7dc4b320bccfa8a6017f87045b27a37d8199f7
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227735"
---
# <a name="deploy-to-the-cloud"></a>Развертывание в облаке

Teams набор средств позволяет развертывать или загружать код frontend и backend в приложении на предварительно заданные облачные ресурсы в Azure.

* Вкладка, например frontend-приложения, развертывается в хранилище Azure и настраивается для статического веб-хостинга или SharePoint сайта.
* Дополнительные API развернуты в Azure Functions.
* Расширение бота или обмена сообщениями развернуто в службе приложений Azure.

## <a name="prerequisite"></a>Предварительное условие

* [Установка Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии v3.0.0+.

> [!TIP]
> Вы уже должны иметь проект Teams приложения, открытый в коде VS.

> [!NOTE]
> Прежде чем развертывать код проекта в облаке, сначала [выполните шаги по обеспечению облачных](provision.md) ресурсов.


## <a name="deploy-teams-apps-using-teams-toolkit"></a>Развертывание Teams с помощью Teams набор средств

В учебных пособиях Пошаговая инструкция по развертыванию с помощью Teams набор средств. Вы можете использовать следующее, чтобы развернуть Teams приложение:

* [Развертывание приложения в Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Развертывание приложения для SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workloads"></a>Сведения о рабочих Teams приложения

| Teams рабочих нагрузок приложений| Исходный код | Сборка Artifacts| Целевые ресурсы |
|-------------|----------|---------------|---------------|
|Вкладки с React </br> Фронтальная рабочая нагрузка| `yourProjectFolder/tabs`| `tabs/build` |Хранилище Azure |
|Вкладки с SharePoint </br> Фронтальная рабочая нагрузка | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint каталога приложений |
|API на функциях Azure </br> Рабочая нагрузка в задней части | `yourProjectFolder/api`| Недоступно |Функции Azure |
|Расширения ботов и сообщений </br> Рабочая нагрузка в задней части | `yourProjectFolder/bot` | Недоступно | Служба приложений Azure |

> [!NOTE]
> Если вы включаете ресурс управления API Azure в проект и запускаете развертывание. API можно опубликовать в Azure Functions в службе управления API Azure.

## <a name="see-also"></a>См. также

> [!div class="nextstepaction"]
> [Добавление дополнительных облачных ресурсов](add-resource.md)

> [!div class="nextstepaction"]
> [Добавление дополнительных Teams приложений](add-capability.md)

> [!div class="nextstepaction"]
> [Развертывание кода проекта с конвейерами CI/CD](use-CICD-template.md)

> [!div class="nextstepaction"]
> [Управление несколькими средами](TeamsFx-multi-env.md)

> [!div class="nextstepaction"]
> [Сотрудничество с другими разработчиками в Teams проекте](TeamsFx-collaboration.md)
