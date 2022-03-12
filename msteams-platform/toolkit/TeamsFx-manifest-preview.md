---
title: Предварительный Teams Манифест приложения в Teams набор средств
author: zyxiaoyuer
description: Предварительный просмотр манифеста приложения Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: aa80636a4fdb3c27d66bc08f9d308a009e183570
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453245"
---
# <a name="preview-teams-app-manifest-in-teams-toolkit"></a>Предварительный Teams манифест приложения в Teams набор средств

После строительных лесов в папке доступны следующие `templates/appPackage` файлы шаблона манифеста:

* `manifest.local.template.json` - локальное приложение групп отлаговки.
* `manifest.remote.template.json` - общий доступ между всеми удаленными средами.

Файлы Шаблона, состоящие из задатчиков, и фактические значения из Teams набор средств решаются в файлах под и `.fx/configs` `.fx/states`.

## <a name="prerequisite"></a>Предварительное условие

* [Установка Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии v3.0.0+.

> [!TIP]
> Убедитесь, Teams проект приложения открыт в Visual Studio коде.

## <a name="preview-manifest"></a>Манифест предварительного просмотра

Чтобы просмотреть манифест с реальным контентом, Teams набор средств создает файлы манифеста предварительного просмотра в папке`build/appPackage`:

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>Просмотр локального файла манифеста

Чтобы просмотреть файл манифеста приложения локальных групп, необходимо нажать **F5** для запуска локального отлаговки. Он создает локальные параметры по умолчанию для вас, а затем пакет приложений и манифест предварительного просмотра создается в **папке build/appPackage** .

Кроме того, можно просмотреть локальный манифест, следуя следующим шагам:

1. Выберите **Предварительный** просмотр в **коделенов файла manifest.local.template.json** .
2. Выберите **файл манифеста Preview** в панели меню **файла manifest.local.template.json** .
3. Выберите **пакет Teams zip в** Treeview и выберите **Локальный**.
Локальный предварительный просмотр отображается как показано на изображении:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-1.png" alt-text="Предварительная версия":::

### <a name="preview-manifest-in-remote-environment"></a>Манифест предварительного просмотра в удаленной среде

Чтобы просмотреть файл манифеста приложения удаленных групп, выберите Положение в облаке в панели разработки Teams набор средств Treeview или триггер **Teams: Подготовка** в облаке из палитры команд. Он создает конфигурацию для приложения удаленных групп и создает манифест пакета и предварительного просмотра в **папке build/appPackage** .

Вы также можете просмотреть манифест в удаленной среде, следуя следующим шагам:

1. Выберите **Предварительный** просмотр в **коделенов файла manifest.remote.template.json** .
2. Выберите **файл манифеста предварительного** просмотра в панели меню **файла manifest.remote.template.json** .
3. Выберите **пакет Teams zip в** Treeview.
4. Выберите среду.

Если существует несколько сред, необходимо выбрать среду, в которой необходимо предварительно просмотреть, как показано на изображении:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Добавление env":::

## <a name="sync-local-changes-to-dev-portal"></a>Синхронизация локальных изменений на портал Dev

После предварительного просмотра файла манифеста можно синхронизировать локальные изменения на портал Dev, следуя следующим шагам:

1. Выберите **обновление для Teams платформы** в левом верхнем углу`manifest.{env}.json`
2. Выберите **Teams: манифест обновления для Teams платформы** в панели меню`manifest.{env}.json`

 Вы также можете **запускать Teams: манифест обновления для Teams платформы** из палитры команд

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="представление в виде дерева":::

> [!NOTE]
> Триггер из коделенов редактора или **заголовка** обновляет текущий файл манифеста для Teams платформы. Триггер из палитры команд требует выбора целевой среды.

Если файл манифеста устарел из-за изменения конфигурации файла или изменения шаблона, убедитесь в следующем действии:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::

* **Просмотр только**: локальный файл манифеста будет перезаписан в соответствии с текущей конфигурацией
* **Предварительный просмотр и обновление**: локальный файл манифеста будет перезаписываться в соответствии с текущей конфигурацией, а также обновляться до Teams платформы
* **Отмена**: ничего не делать

> [!NOTE]
> Изменения будут обновлены до портала разработчиков. Если на портале разработчиков есть некоторые обновления вручную, они будут перезаписаны.

## <a name="see-also"></a>См. также

[Настройка манифеста Teams приложения в Teams набор средств](TeamsFx-manifest-customization.md)
