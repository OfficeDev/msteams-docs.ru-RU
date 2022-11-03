---
title: Установка набора средств Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете об установке набора средств Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: e079f023d931af48d5c06151c585a059c3f7f803
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833081"
---
# <a name="install-teams-toolkit"></a>Установка набора средств Teams

В этой статье описывается установка расширения Teams Toolkit.

## <a name="prerequisites"></a>Предварительные требования

::: zone pivot="visual-studio-code"

Перед установкой Набора средств Teams для Visual Studio Code необходимо [скачать и установить Visual Studio Code](https://code.visualstudio.com/Download).

::: zone-end

::: zone pivot="visual-studio"

Перед установкой Набора средств Teams для Visual Studio необходимо [скачать и установить Visual Studio 2022](https://aka.ms/VSDownload) с помощью Visual Studio Installer.

::: zone-end

::: zone pivot="visual-studio-code"

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Установка набора средств Teams для Visual Studio Code

Набор средств Teams можно установить с помощью окна Расширения в Visual Studio Code или из Visual Studio Marketplace.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Запустите **Visual Studio Code**.
1. Откройте окно Расширения (**CTRL+SHIFT+X️** / **⇧-X** или **Просмотр расширений >**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="Снимок экрана: установка.":::

1. В поле поиска введите **Набор средств Teams** .

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="Снимок экрана: набор средств.":::

1. Нажмите кнопку **Установить**.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="Снимок экрана: установка набора средств 4.0.0.":::

   После успешной установки набора средств Teams в Visual Studio Code на панели инструментов Visual Studio Code появится значок Набора средств Teams.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Снимок экрана: представление после установки.":::

# <a name="marketplace"></a>[Рынке](#tab/marketplace)

1. Перейдите в [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) в веб-браузере.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-ttk-marketplace.png" alt-text="Снимок экрана: установка TTK Marketplace.":::

1. Нажмите кнопку **Установить**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Install-ttk.png" alt-text="Снимок экрана: установка TTK.":::

1. Во всплывающем окне выберите **Открыть**, чтобы запустить Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-open.png" alt-text="Снимок экрана: выбор открытого окна.":::

   Страница расширения Набора средств Teams отображается в Visual Studio Code:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ttk-in-vsc.png" alt-text="Снимок экрана: выбор TTK в VSC.":::

1. Нажмите кнопку **Установить**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="Снимок экрана: выбор параметра Установить TTK в VSC.":::

   После успешной установки набора средств Teams в Visual Studio Code на панели инструментов Visual Studio Code появится значок Набора средств Teams.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Снимок экрана: представление после установки.":::

---

## <a name="installing-a-different-release-version"></a>Установка другой версии выпуска

По умолчанию Visual Studio Code автоматически обновляет набор средств Teams. Если вы хотите установить другую версию, выполните следующие действия:

* Щелкните значок Расширения (:::image type="icon" source="../assets/images/teams-toolkit-v2/extension icon.PNG":::) на панели инструментов Visual Studio Code.
* В поле поиска введите **Набор средств Teams**  .
* На странице Набор средств Teams щелкните стрелку раскрывающегося списка рядом с кнопкой **Удалить** .
* Выберите **Установить другую версию...** в меню и выберите версию для установки.

## <a name="installing-a-pre-release-version"></a>Установка предварительной версии

Расширение Набора средств Teams для Visual Studio Code также доступно на сайте GitHub. Чтобы скачать предварительные выпуски, перейдите [на страницу Выпуски на сайте GitHub](https://github.com/OfficeDev/TeamsFx/releases) и найдите скачиваемые расширения, помеченные как предварительные.

::: zone-end

::: zone pivot="visual-studio"

## <a name="install-teams-toolkit-for-visual-studio"></a>Установка набора средств Teams для Visual Studio

   > [!IMPORTANT]
   > Мы рекомендуем использовать Visual Studio 2022 версии 17.3.3 или более поздней для Набора средств Teams, который является последним выпуском для устранения нескольких известных проблем в предыдущих версиях Visual Studio.

1. [Скачайте установщик Visual Studio](https://aka.ms/VSDownload) или откройте его, если он уже установлен.
2. Выберите **Установить** или **Изменить** , если Visual Studio уже установлен.
3. Перейдите на вкладку **Рабочие нагрузки** , а затем выберите **рабочую нагрузку ASP.NET и веб-разработка** .
4. Справа выберите **средства разработки Microsoft Teams** в разделе **Необязательно** на панели **Сведения об установке** .
5. Выберите **Изменить** или **Установить** , чтобы завершить установку.

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install_1.png" alt-text="Снимок экрана: установка Visual Studio.":::

6. После завершения установки нажмите кнопку **Запустить** , чтобы открыть Visual Studio.

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch_1.png" alt-text="Снимок экрана: запуск Visual Studio.":::

::: zone-end

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда набор средств Teams установлен, см [. раздел Создание проекта Teams](create-new-project.md) , чтобы приступить к работе.

## <a name="see-also"></a>См. также

* [Обзор набора средств Teams](explore-Teams-Toolkit.md)
* [Создание нового приложения Teams с помощью "Инструментов Teams"](create-new-project.md)
* [Подготовка к созданию приложений с помощью Microsoft Teams Toolkit](build-environments.md)
* [Подготовка облачных ресурсов с помощью набора средств Teams](provision.md)
* [Развертывание приложения Teams в облаке](deploy.md)
* [Создание приложения Teams в Visual Studio](create-new-project.md#create-new-teams-app-in-visual-studio)
* [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
* [Развертывание приложения Teams в облаке с помощью Visual Studio](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)
