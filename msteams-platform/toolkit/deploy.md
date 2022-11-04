---
title: Развертывание в облаке
author: MuyangAmigo
description: В этом модуле вы узнаете, как развернуть приложение в облаке, Azure или SharePoint и развернуть приложения Teams с помощью набора средств Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 17d4d1d80f9ffd634e2fdae815b8504bb6c0ca99
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833137"
---
# <a name="deploy-teams-app-to-the-cloud"></a>Развертывание приложения Teams в облаке

Набор средств Teams помогает развернуть или передать интерфейсный и внутренний код в приложении в подготовленные облачные ресурсы в Azure.

::: zone pivot="visual-studio-code"

## <a name="deploy-teams-app-to-the-cloud-using-visual-studio-code"></a>Развертывание приложения Teams в облаке с помощью Visual Studio Code

В облаке можно развернуть следующие компоненты:

* Вкладка, например интерфейсные приложения, развертывается в службе хранилища Azure и настраивается для статического веб-размещения или сайта sharepoint.
* Интерфейсы API серверной части развертываются в Функции Azure.
* Расширение бота или сообщения развертывается в Служба приложений Azure.

  > [!NOTE]
  > Перед развертыванием кода приложения в облаке Azure необходимо успешно завершить [подготовку облачных ресурсов](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Развертывание приложений Teams с помощью набора средств Teams

Руководства по началу работы помогут выполнить развертывание с помощью набора средств Teams. Для развертывания приложения Teams можно использовать следующие руководства.

* [Развертывание приложения в Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Развертывание приложения в SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Сведения о рабочей нагрузке приложения Teams

| Рабочая нагрузка приложения Teams | Исходный код | Артефакт сборки| Целевой ресурс |
|-------------|----------|---------------|---------------|
|Вкладки с React </br> Рабочая нагрузка интерфейсной части| `yourProjectFolder/tabs`| `tabs/build` |Хранилище Azure |
|Вкладки с SharePoint </br> Рабочая нагрузка интерфейсной части | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |Каталог приложений SharePoint |
|API на Функции Azure </br> Рабочая нагрузка серверной части | `yourProjectFolder/api`| Неприменимо |Функции Azure |
|Расширения для сообщений и ботов </br> Рабочая нагрузка серверной части | `yourProjectFolder/bot` | Неприменимо | Служба приложений Azure |

> [!NOTE]
> Если вы включаете ресурс управления API Azure в проект и активируете развертывание, вы можете опубликовать API в Функции Azure в службе управления API Azure.

::: zone-end

::: zone pivot="visual-studio"

## <a name="deploy-teams-app-to-the-cloud-using-visual-studio"></a>Развертывание приложения Teams в облаке с помощью Visual Studio

В Visual Studio можно развернуть следующие приложения:

* Приложение-вкладка, например интерфейсные приложения, развертывается в службе хранилища Azure и настроено для статического веб-размещения.
* Приложение бота уведомлений с Функции Azure триггерами можно развернуть в Функции Azure.
* Приложение бота или расширение для сообщений можно развернуть в службах приложение Azure.

После развертывания вы можете просмотреть приложение в клиенте Teams или в веб-браузере, прежде чем приступить к использованию.

## <a name="deploy-teams-app-using-teams-toolkit"></a>Развертывание приложения Teams с помощью набора средств Teams

1. Откройте Visual Studio.
1. Выберите **Создать проект** или откройте существующий проект из списка.
1. Щелкните правой кнопкой мыши проект **MyTeamsApp1** > **Teams Toolkit** > **Deploy to the cloud**.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-cloud.png" alt-text="развертывание в облаке":::

   > [!NOTE]
   > В этом сценарии проект называется MyTeamsApp1.

1. Выберите **Развернуть** в диалоговом окне подтверждения.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-confirmation.png" alt-text="Диалоговое окно подтверждения развертывания в облаке":::

   После завершения процесса развертывания вы увидите всплывающее окно с подтверждением успешного развертывания. Вы также можете проверить состояние в окне вывода.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/VS-deploy-popup.png" alt-text="Всплывающее окно &quot;Развертывание в облаке&quot;":::

### <a name="preview-your-app"></a>Предварительный просмотр приложения

Для предварительного просмотра приложения необходимо сначала создать пакет zip-приложения и загрузить неопубликованное приложение в клиент Teams.

1. Выберите **Пакет zip-приложения** **набора средств** >  **Project** >  Teams.
1. Выберите параметр **Локальный** или **Для Azure** , чтобы создать пакет приложения Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-ZipApp-package1.png" alt-text="Создание пакета приложения Teams":::

**Предварительный просмотр приложения в клиенте Teams**

1. Выберите **Предварительная версия набора средств** >  **Project** >  Teams **в Teams**.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams2.png" alt-text="Предварительная версия приложения Teams в клиенте Teams":::

   Теперь приложение загружено в Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/sideload-teams.png" alt-text="Загрузка неопубликованного приложения Teams в клиенте Teams":::

Другой способ предварительного просмотра приложения:

1. Щелкните правой кнопкой мыши проект **MyTeamsApp1** в **разделе Обозреватель решений**.
1. Выберите **Предварительная версия набора средств** >  Teams **в Teams**, чтобы запустить приложение Teams в веб-браузере.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams.png" alt-text="Предварительная версия приложения Teams в веб-браузере":::

   > [!NOTE]
   > Те же параметры меню доступны в меню Проект.

   Теперь приложение загружено в Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/sideload-teams.png" alt-text="Загрузка неопубликованного приложения Teams в клиенте Teams":::

::: zone-end

## <a name="see-also"></a>См. также

* [Создание и развертывание облачной службы Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Создание приложений Teams с несколькими возможностями](add-capability.md)
* [Добавление облачных ресурсов в приложение Microsoft Teams](add-resource.md)
* [Создание приложения Teams в Visual Studio](create-new-project.md#create-new-teams-app-in-visual-studio)
* [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
* [Изменение манифеста приложения Teams с помощью Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Локальная отладка приложения Teams с помощью Visual Studio](debug-local.md#debug-your-teams-app-locally-using-visual-studio)
