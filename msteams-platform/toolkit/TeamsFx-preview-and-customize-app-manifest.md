---
title: Teams манифеста приложения в Teams Toolkit
author: zyxiaoyuer
description: В этом модуле вы узнаете, как изменять, просматривать и настраивать Teams приложения в другой среде.
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
ms.openlocfilehash: 505f5aeaf6cdae995efd182535c4d5a8814f9ea1
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143874"
---
# <a name="edit-teams-app-manifest"></a>Изменение Teams приложения

Файл шаблона манифеста `manifest.template.json` доступен в папке `templates/appPackage` после скаффолдинга. Файл шаблона с заполнителями и фактическими значениями разрешается Teams toolkit `.fx/configs` `.fx/states` с помощью файлов в разных средах и для разных сред.

**Чтобы просмотреть манифест с фактическим содержимым, Teams Toolkit создает файлы манифеста предварительного просмотра в `build/appPackage` папке**:

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote Teams app
        ├───appPackage.local.zip - Zipped app package of local Teams app
        ├───manifest.{env}.json  - Previewed manifest of remote Teams app
        └───manifest.local.json  - Previewed manifest of local Teams app
```

Вы можете просмотреть файл манифеста в локальных и удаленных средах.

* [Предварительный просмотр файла манифеста в локальной среде](#preview-manifest-file-in-local-environment)
* [Предварительный просмотр файла манифеста в удаленной среде](#preview-manifest-file-in-remote-environment)

## <a name="preview-manifest-file-in-local-environment"></a>Предварительный просмотр файла манифеста в локальной среде

Чтобы просмотреть файл манифеста в локальной среде, можно нажать **клавишу F5** , чтобы запустить локальную отладку. Будут созданы локальные параметры по умолчанию, а затем пакет приложения и предварительные сборки манифеста в папке `build/appPackage`.

Вы также можете просмотреть локальный файл манифеста, выполнив следующие действия.

1. Выберите **"Предварительный** просмотр" в коде файла `manifest.template.json` и выберите **локальный**.
2. Выберите **файл манифеста предварительного просмотра** в строке меню `manifest.template.json` файла.
3. Выберите **zip Teams пакет метаданных** в Treeview и выберите **локальный**.

Локальный предварительный просмотр отображается, как показано на изображении.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Предварительная версия":::

## <a name="preview-manifest-file-in-remote-environment"></a>Предварительный просмотр файла манифеста в удаленной среде

**Просмотр файла манифеста в удаленной среде**

* Выберите **"Подготовка в облаке"** в разделе **"РАЗРАБОТКА**" в Teams Toolkit или
* **Триггер Teams: подготовка в облаке из** палитры команд.

Он создает конфигурацию для удаленного Teams приложения, а также создает пакет и манифест предварительного просмотра в папке`build/appPackage`.

Вы также можете просмотреть файл манифеста в удаленной среде, выполнив следующие действия.

1. Выберите **"Предварительный** просмотр" в коде файла `manifest.template.json` .
2. Выберите **файл манифеста предварительного просмотра** в строке меню `manifest.template.json` файла.
3. Выберите **zip Teams пакет метаданных в** Treeview.
4. Выберите среду.

> [!NOTE]
> Если есть несколько сред, необходимо выбрать среду для предварительного просмотра, как показано на изображении:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Add env":::

## <a name="sync-local-changes-to-dev-portal"></a>Синхронизация локальных изменений на портале разработки

После предварительного просмотра файла манифеста можно синхронизировать локальные изменения с порталом разработчика следующими способами:

1. Разверните Teams приложения.

   Развернуть манифест Teams приложения можно любым из следующих способов:

   * Перейдите к `manifest.template.json` файлу и щелкните правой кнопкой мыши, чтобы выбрать его `Deploy Teams app manifest` из контекстного меню.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="Развертывание манифеста":::

   * Триггер `Teams: Deploy Teams app manifest` из палитры команд.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="Развертывание из палитры команд":::

2. Обновление до Teams платформы.

   Вы можете обновить платформу Teams любым из следующих способов:

   * Выберите **обновление Teams платформы** в левом верхнем углу `manifest.{env}.json`окна .

   * Активация Teams: обновление манифеста **Teams платформы в** строке меню `manifest.{env}.json`.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="Обновление для команд":::

Вы также можете **активировать Teams: обновление манифеста для Teams платформы** из палитры команд:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="представление в виде дерева":::

> [!NOTE]
> Триггер из codelens редактора или строки меню обновляет текущий файл манифеста Teams платформе. Для триггера из палитры команд требуется выбрать целевую среду.

 Команда CLI:

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> Изменения обновляются на портале разработки. Любые обновления вручную на портале разработчика перезаписываются.

Если файл манифеста устарел из-за изменения файла конфигурации или изменения шаблона, выберите одно из следующих действий:

* **Только предварительная** версия: локальный файл манифеста перезаписывается в соответствии с текущей конфигурацией.
* **Предварительный просмотр и обновление**: локальный файл манифеста перезаписывается в соответствии с текущей конфигурацией, а также обновляется до Teams платформы.
* **Отмена**: никаких действий не выполняется.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre" border="true":::

## <a name="customize-teams-app-manifest"></a>Настройка манифеста приложения Teams

Набор средств Teams состоит из следующих файлов шаблона манифеста в папке `manifest.template.json` в локальных и удаленных средах.

* `manifest.template.json`
* `templates/appPackage`

Во время локальной отладки или подготовки Teams Toolkit `manifest.template.json``state.{env}.json``config.{env}.json`загружает манифест с конфигурациями из и создает Teams на [портале разработки](https://dev.teams.microsoft.com/apps).

## <a name="supported-placeholders-in-manifesttemplatejson"></a>Поддерживаемые заполнители в manifest.template.json

В следующем списке приведены поддерживаемые заполнители в следующих разделах `manifest.template.json`:

* `{{state.xx}}` — это предопределенный заполнитель, и его значение разрешается набором средств Teams с определением в `state.{env}.json`. Не изменяйте значения в `state.{env}.json`
* `{{config.manifest.xx}}` — это настраиваемый заполнитель, и его значение разрешается из `config.{env}.json`

**Добавление настраиваемого параметра**

1. Добавьте настраиваемый параметр следующим образом:</br>
   а. Добавьте заполнитель с шаблоном `manifest.template.json` `{{config.manifest.xx}}`.</br>
   б. Добавьте значение конфигурации в `config.{env}.json`.

     ```json
     {
         "manifest": {
          "KEY": "VALUE"
          }
     }
     ```

2. Чтобы перейти к файлу конфигурации, выберите любой из заполнителей конфигурации **"** Перейти к файлу конфигурации" или "Просмотреть **файл состояния** " `manifest.template.json`.

### <a name="validate-manifest"></a>Проверка манифеста

Во время таких операций, как **zip Teams** пакет метаданных, Teams Toolkit проверяет манифест на соответствие его схеме. В следующем списке приведены различные способы проверки манифеста.

* В VSC запустите триггер из `Teams: Validate manifest file` палитры команд:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="Проверка файла":::

* В интерфейсе командной строки используйте команду:

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## Codelenses and hovers

In `manifest.template.json`, you can navigate to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Preview values":::

> [!NOTE]
> Provision the environment or execute local debug to generate values for placeholders.

You can navigate to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Select your environment":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Preview all values":::

## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)
