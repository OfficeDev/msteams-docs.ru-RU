---
title: Создание нового приложения Teams с помощью "Инструментов Teams"
author: zyxiaoyuer
description: Создание нового приложения Teams с помощью "Инструментов Teams"
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: d44f757141d31faaf4639a58fbbd31e5729e6f02
ms.sourcegitcommit: 1e77573e47fad51a19545949fdac1241b13052e2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656154"
---
# <a name="create-a-new-teams-app-using-teams-toolkit"></a>Создание нового приложения Teams с помощью "Инструментов Teams"

Чтобы создать новое приложение Teams с помощью инструментов Teams, можно выбрать один из следующих вариантов:

* [Создание нового приложения Teams](create-new-project.md#create-a-new-teams-app)
* [Просмотр образцов](create-new-project.md#create-a-new-teams-app-using-view-samples)

### <a name="create-a-new-teams-app"></a>Создание нового приложения Teams

1. Откройте Visual Studio Code.
1. Выберите значок Набор инструментов Teams:::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG" border="true"::: на боковой панели Visual Studio Code.
1. Выберите **Создать приложение Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar.png" alt-text="Боковая панель наборов средств Teams":::

1. Вы можете выбрать **Создать новое приложение Teams** или **Начать с помощью примера**.
   
   :::image type="content" source="../assets/images/teams-toolkit-v2/select-create-app.png" alt-text="Создать приложение":::
   
1. При выборе параметра **Создать новое приложение Teams** появится следующее изображение с шаблонами из трех категорий: приложение Teams на основе сценариев, приложение Basic Teams и расширенные приложения Teams в Microsoft 365: 

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams-capabilities.png" alt-text="Ограничения для приложения Teams":::

1. Выберите хотя бы один вариант, чтобы начать создание приложения Teams.


### <a name="create-a-new-teams-app-using-view-samples"></a>Создание нового приложения Teams с помощью образцов представлений

Вы можете создать новое приложение, просмотрев **Просмотр образцов** и выбрав существующий образец. Выбранный образец может уже иметь некоторые функции, например список дел с серверной частью Azure или интеграцию с Microsoft Graph Toolkit.

 1. Откройте **набор средств Teams** из Microsoft Visual Studio Code.
 1. Выберите раздел **РАЗРАБОТКА** в дереве.
 1. Выберите **Образцы представления**. 

    :::image type="content" source="../assets/images/teams-toolkit-v2/view-samples.png" alt-text="Просмотр образцов":::

    Примеры образцов выглядит так, как показано на следующем изображении:
   
    :::image type="content" source="../assets/images/teams-toolkit-v2/sample-gallery.png" alt-text="Коллекция образцов":::

  Коллекцию образцов можно изучить следующим образом:

  1. Выберите пример для просмотра подробных сведений.
  1. Выберите **Создать** на странице сведений каждого примера, чтобы скачать его. 
  1. Запустите приложение локально или удаленно для предварительного просмотра в веб-клиенте Teams, следуя инструкциям, которые автоматически открываются после загрузки примера.
  1. Если вы не хотите загружать примеры, вы можете выбрать **Просмотр на GitHub**, чтобы открыть образец в репозитории GitHub Samples и просмотреть исходный код.

## <a name="step-by-step-guides-using-teams-toolkit"></a>Пошаговые инструкции по использованию набора средств Teams

* [Создание приложения Teams с помощью Blazor](../sbs-gs-blazorupdate.yml)
* [Создание приложения Teams с помощью JavaScript с использованием React](../sbs-gs-javascript.yml)
* [Создание приложения Teams с помощью SPFx](../sbs-gs-spfx.yml)
* [Создание приложения Teams с помощью C# или .NET](../sbs-gs-csharp.yml)
* [Отправка уведомления в Teams](../sbs-gs-notificationbot.yml)
* [Бот командной сборки](../sbs-gs-commandbot.yml)

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов](provision.md)
* [Развертывание приложения Teams в облаке](deploy.md)
* [Публикация приложения Microsoft Teams](../concepts/deploy-and-publish/appsource/publish.md)
* [Управление несколькими средами](TeamsFx-multi-env.md)
* [Совместная работа с другими разработчиками в проекте Teams](TeamsFx-collaboration.md)