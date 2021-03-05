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
# <a name="upgrade-teams-using-microsoft-teams-yeoman-generator"></a>Upgrade Teams с помощью генератора Yeoman Microsoft Teams
Этот учебник поможет вам обновить текущую версию приложения Microsoft Teams до последней версии с помощью генератора Yeoman Microsoft Teams.

## <a name="get-current-version-of-teams"></a>Получить текущую версию Teams
```PowerShell
 yo teams --version
```

## <a name="update-teams"></a>Update Teams
Команда yo перечисляет различные варианты: от создания проекта до обновления генератора. Для выбора генератора обновлений используйте следующую команду:
```PowerShell
 yo
```

Используйте клавиши стрелки, чтобы **выбрать генераторы обновления.**
![изображение YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

В списке отображаются все доступные генераторы. Чтобы выбрать или отобрать версию Teams  из доступных параметров, используйте пробел и выберите определенный генератор.
![изображение useSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)

Для завершения установки Teams требуется от нескольких секунд до нескольких минут.

После завершения установки используйте следующую команду для проверки установленной версии:

```PowerShell
yo teams --version
```

![изображение FindVersionAfterInstallation](~/assets/images/Update-Teams/FindVersionAfterInstallation.png)

Поздравляю! Вы обновили Microsoft Teams.

