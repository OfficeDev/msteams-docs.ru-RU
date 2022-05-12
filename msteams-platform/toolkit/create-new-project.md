---
title: Создание нового приложения Teams с помощью "Инструментов Teams"
author: zyxiaoyuer
description: Создание нового приложения Teams с помощью "Инструментов Teams"
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: e287d6251af6d44b78010449dce751b938f390bd
ms.sourcegitcommit: 05285653b2548e0b39e788cd07d414ac87ba3eaf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2022
ms.locfileid: "65191266"
---
# <a name="create-a-new-teams-app-using-teams-toolkit"></a>Создание нового приложения Teams с помощью "Инструментов Teams"

Чтобы создать новое приложение Teams с помощью инструментов Teams, можно выбрать один из следующих вариантов:

* [Создание нового приложения Teams](create-new-project.md#create-a-new-teams-app)
* [Просмотр образцов](create-new-project.md#create-a-new-teams-app-using-view-samples)

### <a name="create-a-new-teams-app"></a>Создание нового приложения Teams

1. Откройте Visual Studio Code.
1. Выберите значок Набор инструментов Teams:::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG" border="true"::: на боковой панели Visual Studio Code.
1. Выберите **Создать приложение Teams**.
1. Выберите на вкладке доступных возможностей бот, расширение сообщений или вкладку с использованием SharePoint Framework (SPFx). 
1. Выберите хотя бы один вариант, чтобы начать создание приложения Teams.

### <a name="create-a-new-teams-app-using-view-samples"></a>Создание нового приложения Teams с помощью образцов представлений

Вы можете создать новое приложение, просмотрев **Просмотр образцов** и выбрав существующий образец. Выбранный образец может уже иметь некоторые функции, например список дел с серверной частью Azure или интеграцию с Microsoft Graph Toolkit.

 1. Откройте **набор средств Teams** из Microsoft Visual Studio Code.
 1. Выберите раздел **РАЗРАБОТКА** в дереве.
 1. Выберите **Просмотр образцов**. Коллекция образцов выглядит так, как показано на следующем изображении.

    :::image type="content" source="../assets/images/teams-toolkit-v2/view-samples.png" alt-text="Просмотр образцов":::

Вы можете просматривать и загружать образцы и запускать приложение локально или удаленно для предварительного просмотра в веб-клиенте Teams. Следуйте инструкциям для каждого примера или выберите **Просмотреть на GitHub**, чтобы открыть образец в `TeamsFx Samples repository` и просмотреть исходный код.

Дополнительные сведения см. в разделе [Создание нового приложения на вкладке Teams (React)](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=2).

## <a name="step-by-step-guides-using-teams-toolkit"></a>Пошаговые инструкции по использованию набора средств Teams

* [Создание приложения Teams с помощью Blazor](../sbs-gs-blazorupdate.yml)
* [Создание приложения Teams с помощью JavaScript с использованием React](../sbs-gs-javascript.yml)
* [Создание приложения Teams с помощью SPFx](../sbs-gs-spfx.yml)
* [Создание приложения Teams с помощью C# или .NET](../sbs-gs-csharp.yml)

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов](provision.md)
* [Развертывание приложения Teams в облаке](deploy.md)
* [Публикация приложения Microsoft Teams](../concepts/deploy-and-publish/appsource/publish.md)
* [Управление несколькими средами](TeamsFx-multi-env.md)
* [Совместная работа с другими разработчиками в проекте Teams](TeamsFx-collaboration.md)