---
title: Создание нового приложения Teams с помощью "Инструментов Teams"
author: zyxiaoyuer
description: Создание нового приложения Teams с помощью "Инструментов Teams"
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: 55596671f6799145e5bd3de0d9ee4fb1b9ad4942
ms.sourcegitcommit: 6189ca81099452a3ab2ff4fff4fb1ded5ba6dcfe
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2022
ms.locfileid: "64498219"
---
# <a name="create-a-new-teams-app-using-teams-toolkit"></a>Создание нового приложения Teams с помощью "Инструментов Teams"

Чтобы создать новое приложение Teams с помощью инструментов Teams, можно выбрать один из следующих вариантов:

* [Создание нового приложения Teams](create-new-project.md#create-a-new-teams-app)
* [Просмотр образцов](create-new-project.md#create-a-new-teams-app-using-view-samples)

### <a name="create-a-new-teams-app"></a>Создание нового приложения Teams

1. Откройте Visual Studio Code.
1. Выберите значок Набор инструментов Teams:::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG" border="true"::: на боковой панели Visual Studio Code.
1. Выберите **Создать приложение Teams**.
1. Выберите на вкладке доступных возможностей бот, расширение для обмена сообщениями или вкладку с использованием SharePoint Framework (SPFx). 
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

* [Создание приложения Teams с помощью Blazor](../sbs-gs-blazorapp.yml)
* [Создание приложения Teams с помощью JavaScript с использованием React](../sbs-gs-javascript.yml)
* [Создание приложения Teams с помощью SPFx](../sbs-gs-spfx.yml)
* [Создание приложения Teams с помощью C# или .NET](../sbs-gs-csharp.yml)

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов](provision.md)
* [Развертывание приложения Teams в облаке](deploy.md)
* [Публикация приложения Microsoft Teams](TeamsFx-collaboration.md)
* [Управление несколькими средами](TeamsFx-multi-env.md)
* [Совместная работа с другими разработчиками в проекте Teams](TeamsFx-collaboration.md)