---
title: Учебник . Команды обновления с помощью генератора Yeoman Microsoft Teams
description: Узнайте, как использовать генератор Microsoft Teams Yeoman для обновления Teams.
ms.topic: tutorial
ms.openlocfilehash: 0c52dd15703000a1c0f99ddd28401dd686e1b1bb
ms.sourcegitcommit: afe4bc0336663e496d03c52e4b206217c02fae63
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/08/2021
ms.locfileid: "50528637"
---
# <a name="upgrade-teams-using-microsoft-teams-yeoman-generator"></a><span data-ttu-id="161ca-103">Upgrade Teams с помощью генератора Yeoman Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="161ca-103">Upgrade Teams using Microsoft Teams Yeoman generator</span></span>
<span data-ttu-id="161ca-104">Этот учебник поможет вам обновить текущую версию приложения Microsoft Teams до последней версии с помощью генератора Yeoman Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="161ca-104">This tutorial helps you to upgrade your current Microsoft Teams app version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

## <a name="get-current-version-of-teams"></a><span data-ttu-id="161ca-105">Получить текущую версию Teams</span><span class="sxs-lookup"><span data-stu-id="161ca-105">Get current version of Teams</span></span>
```PowerShell
 yo teams --version
```

## <a name="update-teams"></a><span data-ttu-id="161ca-106">Update Teams</span><span class="sxs-lookup"><span data-stu-id="161ca-106">Update Teams</span></span>
<span data-ttu-id="161ca-107">Команда yo перечисляет различные варианты: от создания проекта до обновления генератора.</span><span class="sxs-lookup"><span data-stu-id="161ca-107">The yo command lists out various options ranging from creating project to updating generator.</span></span> <span data-ttu-id="161ca-108">Для выбора генератора обновлений используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="161ca-108">Use the following command to select update generator:</span></span>
```PowerShell
 yo
```

<span data-ttu-id="161ca-109">Используйте клавиши стрелки, чтобы **выбрать генераторы обновления.**</span><span class="sxs-lookup"><span data-stu-id="161ca-109">Use the arrow keys to choose **Update Generators**.</span></span>
<span data-ttu-id="161ca-110">![изображение YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span><span class="sxs-lookup"><span data-stu-id="161ca-110">![image of YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span></span>

<span data-ttu-id="161ca-111">В списке отображаются все доступные генераторы.</span><span class="sxs-lookup"><span data-stu-id="161ca-111">The list displays all the available generators.</span></span> <span data-ttu-id="161ca-112">Чтобы выбрать или отобрать версию Teams  из доступных параметров, используйте пробел и выберите определенный генератор.</span><span class="sxs-lookup"><span data-stu-id="161ca-112">To select or unselect Teams version from the available options, use the **space bar** and choose a specific generator.</span></span>
<span data-ttu-id="161ca-113">![изображение useSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span><span class="sxs-lookup"><span data-stu-id="161ca-113">![image of UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span></span>

<span data-ttu-id="161ca-114">Для завершения установки Teams требуется от нескольких секунд до нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="161ca-114">It takes few seconds to minutes for Teams installation to complete.</span></span>

<span data-ttu-id="161ca-115">После завершения установки используйте следующую команду для проверки установленной версии:</span><span class="sxs-lookup"><span data-stu-id="161ca-115">After the installation is complete, use the following command to check the installed version:</span></span>

```PowerShell
yo teams --version
```

![изображение FindVersionAfterInstallation](~/assets/images/Update-Teams/FindVersionAfterInstallation.png)

<span data-ttu-id="161ca-117">Поздравляю!</span><span class="sxs-lookup"><span data-stu-id="161ca-117">Congrats!</span></span> <span data-ttu-id="161ca-118">Вы обновили Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="161ca-118">You have upgraded Microsoft Teams.</span></span>

