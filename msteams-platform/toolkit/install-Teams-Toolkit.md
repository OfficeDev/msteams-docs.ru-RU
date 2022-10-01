---
title: Установка Набора средств Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете об установке Набора средств Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 03d101df114d3f7564c78c433d01191172e180c9
ms.sourcegitcommit: 3aaccc48906fc6f6fbf79916af5664bf55537250
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/30/2022
ms.locfileid: "68295986"
---
# <a name="install-teams-toolkit"></a>Установка Набора средств Teams

В этой статье описывается установка расширения Набора средств Teams.

## <a name="prerequisites"></a>Предварительные требования

::: zone pivot="visual-studio-code"

Перед установкой Набора средств Teams для Visual Studio Code необходимо скачать и [установить Visual Studio Code](https://code.visualstudio.com/Download).

::: zone-end

::: zone pivot="visual-studio"

Перед установкой Набора средств Teams для Visual Studio необходимо скачать и установить [Visual Studio 2022](https://aka.ms/VSDownload) с помощью Visual Studio Installer.

::: zone-end

::: zone pivot="visual-studio-code"

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Установка набора средств Teams для Visual Studio Code

Набор средств Teams можно установить с помощью окна расширений в Visual Studio Code или установить из Visual Studio Marketplace.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. **Запустите Visual Studio Code**.
1. Откройте окно расширений (**CTRL+SHIFT+X** / **⌘⇧-X** или **view > Extensions**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="Снимок экрана: установка.":::

1. **Введите Набор средств Teams** в поле поиска.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="Снимок экрана: набор средств.":::

1. Нажмите кнопку **Установить**.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="Снимок экрана: набор средств установки 4.0.0.":::

   После успешной установки Набора средств Teams в Visual Studio Code на Visual Studio Code панели инструментов появится значок Набора средств Teams.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Снимок экрана: после представления установки.":::

# <a name="marketplace"></a>[Рынке](#tab/marketplace)

1. Перейдите [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) в веб-браузере.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-ttk-marketplace.png" alt-text="Снимок экрана: установка TTK Marketplace.":::

1. Нажмите кнопку **Установить**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Install-ttk.png" alt-text="Снимок экрана: установка TTK.":::

1. Во всплывающем окне нажмите кнопку **"** Открыть", чтобы Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-open.png" alt-text="Снимок экрана: выбор открытого экрана.":::

   Страница расширения Набора средств Teams отображается в Visual Studio Code:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ttk-in-vsc.png" alt-text="Снимок экрана: выбор TTK в VSC.":::

1. Нажмите кнопку **Установить**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="Снимок экрана: выбор параметра &quot;Установить TTK&quot; в VSC.":::

   После успешной установки Набора средств Teams в Visual Studio Code на Visual Studio Code панели инструментов появится значок Набора средств Teams.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Снимок экрана: представление после установки.":::

---

## <a name="installing-a-different-release-version"></a>Установка другой версии выпуска

По умолчанию Visual Studio Code автоматически поддерживает набор средств Teams в актуальном состоянии. Если вы хотите установить другую версию, выполните следующие действия.

* Щелкните значок расширений (:::image type="icon" source="../assets/images/teams-toolkit-v2/extension icon.PNG":::) на Visual Studio Code панели инструментов.
* **Введите Набор средств Teams** в поле поиска.
* На странице Набора средств Teams щелкните стрелку раскрывающегося списка рядом с кнопкой **"Удалить"** .
* Выберите **"Установить другую версию"...** в меню и выберите версию для установки.

## <a name="installing-a-pre-release-version"></a>Установка предварительной версии

Расширение Teams Toolkit for Visual Studio Code также доступно на сайте GitHub. Чтобы скачать предварительные выпуски, перейдите на страницу "Выпуски" на [GitHub](https://github.com/OfficeDev/TeamsFx/releases) и найдите скачиваемые расширения, помеченные как предварительные.

::: zone-end

::: zone pivot="visual-studio"

## <a name="install-teams-toolkit-for-visual-studio"></a>Установка набора средств Teams для Visual Studio

   > [!IMPORTANT]
   > Мы рекомендуем использовать Visual Studio 2022 версии 17.3.3 или более поздней для Набора средств Teams, который является последним выпуском для устранения нескольких известных проблем в предыдущих версиях Visual Studio.

1. [Скачайте установщик Visual Studio](https://aka.ms/VSDownload) или откройте его, если он уже установлен.
2. Выберите **"Установить**" **или "Изменить"** , если Visual Studio уже установлен.
3. Перейдите **на вкладку "** Рабочие нагрузки", а затем выберите рабочую **нагрузку ASP.NET и веб-разработки** .
4. Справа выберите средства разработки **Microsoft Teams** в разделе **"** Необязательно" панели сведений **об установке** .
5. Нажмите **кнопку "****Изменить" или "** Установить", чтобы завершить установку.

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install_1.png" alt-text="Снимок экрана: установка Visual Studio.":::

6. После завершения установки нажмите кнопку **"Запустить** ", чтобы открыть Visual Studio.

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch_1.png" alt-text="Снимок экрана: запуск Visual Studio.":::

::: zone-end

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда набор средств Teams установлен, перейдите к [разделу "Создание нового проекта Teams"](create-new-project.md) , чтобы приступить к работе.

## <a name="see-also"></a>См. также

* [Обзор набора средств Teams](explore-Teams-Toolkit.md)
* [Создание нового приложения Teams с помощью "Инструментов Teams"](create-new-project.md)
* [Подготовка к созданию приложений с помощью Microsoft Teams Toolkit](build-environments.md)
* [Подготовка облачных ресурсов с помощью Набора средств Teams](provision.md)
* [Развертывание приложения Teams в облаке](deploy.md)
* [Создание приложения Teams в Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
* [Развертывание приложения Teams в облаке с помощью Visual Studio](deploy-teams-app.md)
