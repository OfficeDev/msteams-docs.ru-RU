---
title: Учебник . Команды обновления с помощью генератора Yeoman Microsoft Teams
description: Узнайте, как использовать генератор Microsoft Teams Yeoman для обновления Teams.
ms.topic: tutorial
ms.openlocfilehash: 0c52dd15703000a1c0f99ddd28401dd686e1b1bb
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449626"
---
# <a name="upgrade-teams-using-microsoft-teams-yeoman-generator"></a><span data-ttu-id="34d2e-103">Upgrade Teams с помощью генератора Yeoman Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="34d2e-103">Upgrade Teams using Microsoft Teams Yeoman generator</span></span>
<span data-ttu-id="34d2e-104">Этот учебник поможет вам обновить текущую версию приложения Microsoft Teams до последней версии с помощью генератора Yeoman Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="34d2e-104">This tutorial helps you to upgrade your current Microsoft Teams app version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

## <a name="get-current-version-of-teams"></a><span data-ttu-id="34d2e-105">Получить текущую версию Teams</span><span class="sxs-lookup"><span data-stu-id="34d2e-105">Get current version of Teams</span></span>
```PowerShell
 yo teams --version
```

## <a name="update-teams"></a><span data-ttu-id="34d2e-106">Update Teams</span><span class="sxs-lookup"><span data-stu-id="34d2e-106">Update Teams</span></span>
<span data-ttu-id="34d2e-107">Команда yo перечисляет различные варианты: от создания проекта до обновления генератора.</span><span class="sxs-lookup"><span data-stu-id="34d2e-107">The yo command lists out various options ranging from creating project to updating generator.</span></span> <span data-ttu-id="34d2e-108">Для выбора генератора обновлений используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="34d2e-108">Use the following command to select update generator:</span></span>
```PowerShell
 yo
```

<span data-ttu-id="34d2e-109">Используйте клавиши стрелки, чтобы **выбрать генераторы обновления.**</span><span class="sxs-lookup"><span data-stu-id="34d2e-109">Use the arrow keys to choose **Update Generators**.</span></span>
<span data-ttu-id="34d2e-110">![изображение YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span><span class="sxs-lookup"><span data-stu-id="34d2e-110">![image of YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span></span>

<span data-ttu-id="34d2e-111">В списке отображаются все доступные генераторы.</span><span class="sxs-lookup"><span data-stu-id="34d2e-111">The list displays all the available generators.</span></span> <span data-ttu-id="34d2e-112">Чтобы выбрать или отобрать версию Teams  из доступных параметров, используйте пробел и выберите определенный генератор.</span><span class="sxs-lookup"><span data-stu-id="34d2e-112">To select or unselect Teams version from the available options, use the **space bar** and choose a specific generator.</span></span>
<span data-ttu-id="34d2e-113">![изображение useSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span><span class="sxs-lookup"><span data-stu-id="34d2e-113">![image of UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span></span>

<span data-ttu-id="34d2e-114">Для завершения установки Teams требуется от нескольких секунд до нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="34d2e-114">It takes few seconds to minutes for Teams installation to complete.</span></span>

<span data-ttu-id="34d2e-115">После завершения установки используйте следующую команду для проверки установленной версии:</span><span class="sxs-lookup"><span data-stu-id="34d2e-115">After the installation is complete, use the following command to check the installed version:</span></span>

```PowerShell
yo teams --version
```

![изображение FindVersionAfterInstallation](~/assets/images/Update-Teams/FindVersionAfterInstallation.png)

<span data-ttu-id="34d2e-117">Поздравляю!</span><span class="sxs-lookup"><span data-stu-id="34d2e-117">Congrats!</span></span> <span data-ttu-id="34d2e-118">Вы обновили Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="34d2e-118">You have upgraded Microsoft Teams.</span></span>

