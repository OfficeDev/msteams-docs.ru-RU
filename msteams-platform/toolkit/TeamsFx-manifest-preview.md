---
title: Предварительный просмотр манифеста приложения Teams в наборе средств Teams
author: zyxiaoyuer
description: Предварительный просмотр манифеста приложения Teams
ms.author: nliu
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 91bc070d30136ce1f004676172594f26ca37dea5
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111873"
---
# <a name="preview-app-manifest-in-toolkit"></a>Предварительный просмотр манифеста приложения в наборе средств

Файл шаблона манифеста `manifest.template.json` доступен в папке `templates/appPackage` после скаффолдинга. Файл шаблона использует заполнители, а фактические значения разрешаются набором средств Teams из файлов в папке `.fx/configs` и `.fx/states` для разных сред.

## <a name="prerequisite"></a>Предварительное условие

* Установка [последней версии набора средств Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Откройте проект приложения Teams в Visual Studio Code.

## <a name="preview-manifest"></a>Предварительный просмотр манифеста

Чтобы предварительно просмотреть манифест с реальным содержимым, набор средств Teams создает файлы манифеста предварительного просмотра в папке `build/appPackage`:

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>Предварительный просмотр локального файла манифеста

Чтобы просмотреть файл манифеста локального приложения Teams, можно нажать **F5** для запуска локальной отладки. Будут созданы локальные параметры по умолчанию, а затем пакет приложения и предварительные сборки манифеста в папке `build/appPackage`.

Чтобы просмотреть локальный манифест, выполните следующие действия.

1. Выберите **Предварительный просмотр** в CodeLens файла `manifest.template.json` и выберите **Локальный**
2. Выберите **Просмотр файла манифеста** в меню файла `manifest.template.json`
3. Выберите **Добавить пакет метаданных Teams в ZIP-файл** в Treeview и выберите **Локальный**

Локальный предварительный просмотр отображается, как показано на изображении.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Предварительная версия":::

### <a name="preview-manifest-in-remote-environment"></a>Предварительный просмотр манифеста в удаленной среде

Чтобы просмотреть файл манифеста удаленного приложения Teams, выберите **Подготовка в облаке** на панели **РАЗРАБОТКА** в расширений набора средств Teams или запустите **Teams: подготовка в облаке** из палитры команд. Будет создана конфигурацию для удаленного приложения Teams, а также пакет и манифест предварительного просмотра в папке `build/appPackage`.

Вы также можете просмотреть манифест в удаленной среде. Для этого сделайте следующее.

1. Выберите **Предварительный просмотр** в CodeLens файла `manifest.template.json`
2. Выберите **Просмотр файла манифеста** в меню файла `manifest.template.json`
3. Выберите **Добавить пакет метаданных Teams в ZIP-файл** в Treeview
4. Выберите среду

Если есть несколько сред, необходимо выбрать среду для предварительного просмотра, как показано на изображении:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Add env":::

## <a name="sync-local-changes-to-developer-portal"></a>Синхронизация локальных изменений с порталом разработчика

После предварительного просмотра файла манифеста вы можете синхронизировать локальные изменения с порталом разработчика, выполнив следующие действия.

1. Выберите **Обновить на платформе Teams** в левом верхнем углу в `manifest.{env}.json`
2. Выберите **Teams: обновление манифеста на платформе Teams** в меню `manifest.{env}.json`

 Вы также можете **Teams: обновление манифеста на платформе Teams** из палитры команд:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="представление в виде дерева":::

> [!NOTE]
> Триггер из редактора CodeLens или **заголовок** обновляет текущий файл манифеста на платформе Teams. Триггер из палитры команд требует выбора целевой среды

  

Если файл манифеста устарел из-за изменения файла конфигурации или изменения шаблона, выберите одно из следующих действий.

* **Только предварительный просмотр**: локальный файл манифеста перезаписывается в соответствии с текущей конфигурацией
* **Предварительный просмотр и обновление**: локальный файл манифеста перезаписывается в соответствии с текущей конфигурацией и также обновляется на платформе Teams
* **Отмена**: никакие действия не предпринимаются

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::



> [!NOTE]
> Изменения обновляются на портале разработчика. Все обновления вручную на портале разработчика перезаписываются.

## <a name="see-also"></a>Дополнительные ресурсы

[Настройка манифеста приложения Teams в наборе средств Teams](TeamsFx-manifest-customization.md)
