---
title: Развертывание приложения Teams в облаке с помощью Visual Studio
author: surbhigupta
description: В этом модуле вы узнаете, как развернуть приложение в облаке, Azure или SharePoint и развернуть приложения Teams с помощью Набора средств Teams в Visual Studio.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 4cf2267f4392289f14c3ec3438abd66cf9fb1769
ms.sourcegitcommit: 60484634f38642048e9a9a1465ac0c3322c8229a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2022
ms.locfileid: "67290122"
---
# <a name="deploy-teams-app-to-the-cloud-using-visual-studio"></a>Развертывание приложения Teams в облаке с помощью Visual Studio

Набор средств Teams помогает развертывать или отправлять интерфейсный и внутренний код приложения в подготовленные облачные ресурсы в подписке Azure. После развертывания вы можете просмотреть приложение в клиенте Teams или веб-браузере, прежде чем приступить к использованию. В Visual Studio можно развернуть следующие приложения:

* Приложение вкладки, например интерфейсные приложения, развертывается в службе хранилища Azure, настроенное для статического веб-размещения.
* Приложение бота уведомлений с триггерами функций Azure можно развернуть в функциях Azure.
* Приложение бота или расширение сообщения можно развернуть в службах приложений Azure.

## <a name="prerequisite"></a>Предварительное условие

Ниже приведен список средств, необходимых для создания и развертывания приложений.

| &nbsp; | Установка | Для использования... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 2022 версии 17.3 | Вы можете установить корпоративный выпуск Visual Studio и установить рабочую нагрузку ASP.NET и средства разработки Microsoft Teams. |
| &nbsp; | Набор средств Teams | Расширение Visual Studio, которое создает шаблон проекта для вашего приложения. Используйте последнюю версию. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams для взаимодействия в одном месте со всеми пользователями, с которыми вы работаете, с помощью приложений для чата, собраний и звонков. |
| &nbsp; | Средства Azure и [Интерфейс командной строки Microsoft Azure](/cli/azure/install-azure-cli) | Средства Azure для доступа к хранимых данных или развертывания облачной серверной части для приложения Teams в Azure. |

  > [!NOTE]
  > Перед развертыванием кода проекта в облаке [подготовьте облачные ресурсы для TTK Visual Studio](provision VS.md).

## <a name="deploy-teams-app-using-teams-toolkit"></a>Развертывание приложения Teams с помощью Набора средств Teams

1. Запустите Visual Studio.
1. Выберите **"Создать новый проект** " или откройте существующий проект из списка.
1. Щелкните правой кнопкой мыши проект **MyTeamsApp1**.
1. Выберите **Набор средств Teams**.
1. Выберите **"Развернуть в облаке"...**

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-cloud.png" alt-text="развертывание в облаке":::

   > [!NOTE]
   > В этом сценарии имя проекта — MyTeamsApp1.

6. Выберите **"Развернуть** " в диалоговом окне подтверждения.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-confirmation.png" alt-text="Диалоговое окно подтверждения развертывания в облаке":::

7. После активации и завершения процесса развертывания вы увидите всплывающее окно с подтверждением успешного развертывания. Вы также можете проверить состояние в окне вывода.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/VS-deploy-popup.png" alt-text="Всплывающее окно развертывания в облаке":::

После успешного развертывания проекта в Azure существует несколько способов предварительного просмотра приложения в Наборе средств Teams.

1. Выберите **пакет zip-приложения Project** > **Teams Toolkit** > **,** чтобы создать пакет приложения Teams.
1. Выберите параметр **"Локальный"** или **"Для Azure"** и отправьте его в клиент Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-ZipApp-package.png" alt-text="Создание пакета приложения Teams":::

**Предварительный просмотр приложения в клиенте Teams**

1. Выбор **проекта**
1. Выберите **Набор средств Teams**.
1. Выберите **предварительный просмотр в Teams**.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams1.png" alt-text="Предварительная версия приложения Teams в клиенте Teams":::

Другой способ предварительного просмотра приложения:

1. Щелкните правой кнопкой мыши проект **MyTeamsApp1** на Обозреватель решений панели.
1. Выберите **Набор средств Teams**.
1. Выберите **"Предварительный просмотр" в Teams** , чтобы запустить приложение Teams в веб-браузере.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams.png" alt-text="Предварительный просмотр приложения Teams в веб-браузере":::

   > [!NOTE]
   > Те же параметры меню доступны в меню "Проект".

## <a name="see-also"></a>См. также

* [Создание приложения Teams в Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Подготовка облачных ресурсов с помощью Visual Studio](Provision%20cloud%20resources%20using%20Visual%20Studio.md)
* [Изменение манифеста приложения Teams с помощью Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Локальная отладка приложения Teams с помощью Visual Studio](debug-teams-app-visual-studio.md)
