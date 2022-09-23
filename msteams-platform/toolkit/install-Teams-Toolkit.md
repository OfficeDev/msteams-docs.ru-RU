---
title: Установка Набора средств Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете об установке Набора средств Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 9b6492efed353e2f3228a04da292141679401e66
ms.sourcegitcommit: ef545fac5c0dbe970d81f53b1631930e9196eba3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/23/2022
ms.locfileid: "67991658"
---
# <a name="install-teams-toolkit"></a>Установка Набора средств Teams

Набор средств Teams — это расширение как в Visual Studio, так и Visual Studio Code. В этом документе описано, как установить Набор средств Teams.

::: zone pivot="visual-studio-code"

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Установка набора средств Teams для Visual Studio Code

Перед началом установки необходимо установить Visual Studio Code и клиента Teams.

## <a name="steps-to-install-teams-toolkit"></a>Действия по установке Набора средств Teams

Набор средств Teams можно установить из расширения в Visual Studio Code и Visual Studio Code Marketplace. Следующие шаги помогают установить Набор средств Teams:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Откройте **Visual Studio Code**.
1. Выберите представление расширений (**CTRL+SHIFT+X** / **⌘⇧-X** или **view > Extensions**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="установка":::

1. **Введите Набор средств Teams** в поле поиска.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="Набор средств":::

1. Нажмите кнопку **Установить**.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="install toolkit 4.0.0":::

   После успешной установки Набора средств Teams в Visual Studio Code на Visual Studio Code панели инструментов появится значок Набора средств Teams.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="После установки":::

# <a name="marketplace"></a>[Рынке](#tab/marketplace)

1. Откройте [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

   Появится следующую страницу.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-ttk-marketplace.png" alt-text="установка TTK Marketplace":::

1. Нажмите кнопку **Установить**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Install-ttk.png" alt-text="установка TTK":::

1. Во всплывающем окне выберите " **Открыть"**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-open.png" alt-text="Выбор открытого":::

   Появится Visual Studio Code ниже.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ttk-in-vsc.png" alt-text="Выбор TTK в VSC":::

1. Нажмите кнопку **Установить**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="Выберите &quot;Установить TTK&quot; в VSC":::

   После успешной установки Набора средств Teams в Visual Studio Code на Visual Studio Code панели инструментов появится значок Набора средств Teams.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="После установки":::

---

#### <a name="upgrade-teams-toolkit"></a>Обновление набора средств Teams

Набор средств Teams по умолчанию обновляется до последней версии. Следующие действия помогают установить другую версию:

* Щелкните значок "Расширения :::image type="icon" source="../assets/images/teams-toolkit-v2/extension icon.PNG"::: ".
* **Введите Набор средств Teams** в поле поиска.
* В расширении Набора средств Teams щелкните значок :::image type="icon" source="../assets/images/teams-toolkit-v2/setting icon.PNG"::: .
* Выберите **"Установить другую версию** " для обновления до последней версии Набора средств Teams.

::: zone-end

::: zone pivot="visual-studio"

## <a name="install-teams-toolkit-for-visual-studio"></a>Установка набора средств Teams для Visual Studio

Перед началом установки необходимо установить Visual Studio Installer.

Вы можете скачать последнюю версию Visual Studio Installer со страницы [скачивания Visual Studio](https://visualstudio.microsoft.com).

## <a name="steps-to-install-teams-toolkit"></a>Действия по установке Набора средств Teams

После открытия Visual Studio Installer во всплывающем окне "Рабочие нагрузки":

1. Выберите рабочую нагрузку **ASP.NET и разработка веб-приложений**.
1. Выберите средства **разработки Microsoft Teams на** панели **сведений об установке** .
1. Нажмите кнопку **Установить**.

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install_1.png" alt-text="Установка Visual Studio":::

1. Нажмите **кнопку "** Запустить", чтобы открыть Visual Studio.

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch_1.png" alt-text="Запуск Visual Studio":::

   > [!IMPORTANT]
   > Рекомендуется скачать Visual Studio 2022 версии 17.3.3, так как Набор средств Teams для Visual Studio является общедоступным в этой версии. Эта статья написана для Visual Studio 2022 версии 17.3.3. Набор средств Teams версии 17.3.* или более поздней.

::: zone-end

## <a name="see-also"></a>См. также

* [Обзор набора средств Teams](explore-Teams-Toolkit.md)
* [Создание нового приложения Teams с помощью "Инструментов Teams"](create-new-project.md)
* [Подготовка к созданию приложений с помощью Microsoft Teams Toolkit](build-environments.md)
* [Подготовка облачных ресурсов с помощью Набора средств Teams](provision.md)
* [Развертывание приложения Teams в облаке](deploy.md)
* [Создание приложения Teams в Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
* [Развертывание приложения Teams в облаке с помощью Visual Studio](deploy-teams-app.md)
