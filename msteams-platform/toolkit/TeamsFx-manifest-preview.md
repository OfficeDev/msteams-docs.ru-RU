---
title: Предварительный Teams приложения в Teams набор средств
author: zyxiaoyuer
description: Предварительный просмотр манифеста приложения Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 57dc719f872d502beded14c30a09d72c27ee74c3
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073286"
---
# <a name="preview-app-manifest-in-toolkit"></a>Предварительный просмотр манифеста приложения в набор средств

Файл шаблона манифеста `manifest.template.json` доступен в папке `templates/appPackage` после формирования шаблонов. Файл шаблона с заполнителями и `.fx/configs` `.fx/states` фактическими значениями разрешается Teams набор средств из файлов в разных средах и для разных сред.

## <a name="prerequisite"></a>Предварительное условие

* Установите последнюю [версию Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Убедитесь, что Teams приложение открыто в Visual Studio коде.

## <a name="preview-manifest"></a>Манифест предварительной версии

Чтобы просмотреть манифест с реальным содержимым, Teams набор средств создает файлы манифеста предварительного просмотра в `build/appPackage` папке:

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>Предварительный просмотр локального файла манифеста

Чтобы просмотреть файл манифеста локального приложения teams, можно нажать **клавишу F5** , чтобы запустить локальную отладку. Он создает локальные параметры по умолчанию, а затем пакет приложения и манифест предварительного просмотра создаются в папке `build/appPackage` .

Вы также можете просмотреть локальный манифест, выполнив следующие действия:

1. Выберите **"Предварительный** просмотр" в коде файла `manifest.template.json` и выберите **локальный**
2. Выбор **файла манифеста предварительного просмотра** в строке меню `manifest.template.json` файла
3. Выберите **пакет метаданных zip Teams в** Treeview и выберите **локальный**

Локальный предварительный просмотр отображается, как показано на изображении:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Предварительная версия":::

### <a name="preview-manifest-in-remote-environment"></a>Предварительный просмотр манифеста в удаленной среде

Чтобы просмотреть файл манифеста удаленного приложения teams, выберите "Подготовка в  облаке" на панели разработки Teams набор средств Treeview расширения или активировать Teams **:** Подготовка в облаке из палитры команд. Он создает конфигурацию для удаленного приложения Teams и создает пакет и манифест предварительного просмотра в папке `build/appPackage` .

Вы также можете просмотреть манифест в удаленной среде, выполнив следующие действия:

1. Выберите **"Предварительный** просмотр" в коде файла `manifest.template.json`
2. Выбор **файла манифеста предварительного просмотра** в строке меню `manifest.template.json` файла
3. Выбор **пакета метаданных zip Teams** в Treeview
4. Выбор среды

Если имеется несколько сред, необходимо выбрать среду для предварительного просмотра, как показано на рисунке:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Добавление env":::

## <a name="sync-local-changes-to-developer-portal"></a>Синхронизация локальных изменений на портале разработчика

После предварительного просмотра файла манифеста можно синхронизировать локальные изменения с порталом разработчика, выполнив следующие действия.

1. Выберите **"Обновить для Teams"** в левом верхнем углу окна`manifest.{env}.json`
2. Выберите **Teams: обновление манифеста для Teams платформы** в строке меню`manifest.{env}.json`

 Вы также можете **активировать Teams: обновление манифеста для Teams платформы** из палитры команд:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="представление в виде дерева":::

> [!NOTE]
> Триггер из codelens редактора или **заголовка** обновляет текущий файл манифеста Teams платформе. Для триггера из палитры команд требуется выбрать целевую среду

  

Если файл манифеста устарел из-за изменения файла конфигурации или изменения шаблона, выберите одно из следующих действий:

* **Только предварительная** версия: локальный файл манифеста перезаписывается в соответствии с текущей конфигурацией
* **Предварительный просмотр и обновление**: локальный файл манифеста перезаписывается в соответствии с текущей конфигурацией, а также обновляется до Teams платформы
* **Отмена**: никаких действий не выполняется

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::



> [!NOTE]
> Изменения обновляются на портале разработчика. Все обновления вручную на портале разработки перезаписываются.

## <a name="see-also"></a>См. также

[Настройка Teams приложения в Teams набор средств](TeamsFx-manifest-customization.md)
