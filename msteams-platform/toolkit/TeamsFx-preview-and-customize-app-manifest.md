---
title: Настройка манифеста приложения Teams в наборе средств Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете, как изменять, просматривать и настраивать манифест приложений Teams в другой среде.
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 02bbcc86c769f8ebff87803b6a12bf882e214bf6
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780711"
---
# <a name="customize-teams-app-manifest"></a>Настройка манифеста приложения Teams

Манифест приложения Teams описывает, как ваше приложение интегрируется в продукт Microsoft Teams.

::: zone pivot="visual-studio-code"

## <a name="customize-teams-app-manifest-for-visual-studio-code"></a>Настройка манифеста приложения Teams для Visual Studio Code

Манифест приложения Teams описывает, как ваше приложение интегрируется в продукт Microsoft Teams. Дополнительные сведения о манифесте см. в схеме [манифеста приложения для Teams](../resources/schema/manifest-schema.md). Содержание раздела:

* [Предварительный просмотр файла манифеста в локальной среде](#preview-manifest-file-in-local-environment)
* [Предварительный просмотр файла манифеста в удаленной среде](#preview-manifest-file-in-remote-environment)
* [Синхронизация локальных изменений с порталом разработчика](#sync-local-changes-to-developer-portal)
* [Настройка манифеста приложения Teams](#customize-your-teams-app-manifest)
* [Проверка манифеста](#validate-manifest)

Файл шаблона манифеста `manifest.template.json` доступен в папке `templates/appPackage` после скаффолдинга. Файл шаблона с заполнителями и фактическими значениями разрешается набором средств Teams `.fx/configs` `.fx/states` с помощью файлов в разных средах и для разных сред.

Чтобы просмотреть манифест с фактическим содержимым, Teams Toolkit создает файлы манифеста предварительной версии в папке `build/appPackage` :

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

Вы также можете просмотреть локальный файл манифеста двумя способами.

* Использование параметра предварительного просмотра в codelens
* Использование параметра **пакета метаданных Zip Teams**

Ниже приведены инструкции по предварительному просмотру локального файла манифеста с помощью параметра предварительного просмотра в codelens.

1. Выберите **"Предварительный** просмотр" в коде файла `manifest.template.json` .

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Предварительный просмотр":::

1. Выберите **локальный**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="Выбор среды1":::

Ниже приведены инструкции по предварительному просмотру локального файла манифеста с помощью параметра пакета **метаданных Zip Teams** :

1. Выберите `manifest.template.json` файл.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Выберите манифест":::

1. Щелкните значок Набора средств :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams на Visual Studio Code панели инструментов.

1. Выберите **пакет метаданных Zip Teams в** разделе **DEPLOYMENT**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Выбор пакета метаданных Teams":::

1. Выберите **локальный**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="Выбор среды":::

Локальный предварительный просмотр отображается, как показано на изображении.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Предварительная версия":::

## <a name="preview-manifest-file-in-remote-environment"></a>Предварительный просмотр файла манифеста в удаленной среде

Чтобы просмотреть файл манифеста с помощью Visual Studio Code:

* Выберите **"Подготовка в облаке"** в разделе **"РАЗРАБОТКА** " в расширении Набора средств Teams
  
  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/provision.png" alt-text="Подготовка облачного ресурса":::

Чтобы просмотреть файл манифеста с помощью командыtte:

* **Триггер Teams: подготовка в облаке из** палитры команд.

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/command palatte.png" alt-text="Подготовка облачного ресурса с помощью команды azure":::

Он создает конфигурацию для удаленного приложения Teams и создает пакет и манифест предварительного просмотра в папке `build/appPackage` .

Вы также можете просмотреть файл манифеста двумя методами в удаленной среде.

* Использование параметра предварительного просмотра в codelens
* Использование параметра **пакета метаданных Zip Teams**

Следующие шаги помогают просмотреть файл манифеста с помощью параметра предварительного просмотра в codelens:

1. Выберите **"Предварительный** просмотр" в коде файла `manifest.template.json` .

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Предварительный просмотр":::

1. Выберите среду.

   > [!NOTE]
   > Если есть несколько сред, необходимо выбрать среду для предварительного просмотра, как показано на изображении:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Add env":::

Следующие шаги помогают предварительно просмотреть файл манифеста с помощью параметра пакета метаданных **Zip Teams** в удаленной среде:

1. Выберите `manifest.template.json` файл.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Выберите манифест":::

1. Щелкните значок Набора средств :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams на Visual Studio Code панели инструментов.

1. Выберите **пакет метаданных Zip Teams в** разделе **DEPLOYMENT**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Выбор пакета метаданных Teams":::

1. Выберите среду.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Add env":::

   > [!NOTE]
   > Если есть несколько сред, необходимо выбрать среду для предварительного просмотра, как показано на изображении:

## <a name="sync-local-changes-to-developer-portal"></a>Синхронизация локальных изменений с порталом разработчика

После предварительного просмотра файла манифеста можно синхронизировать локальные изменения с порталом разработчика следующими способами:

> [!NOTE]
> Дополнительные сведения о портале разработчика см. на [портале разработчика для Teams](../concepts/build-and-test/teams-developer-portal.md).

1. Развертывание манифеста приложения Teams.

   Манифест приложения Teams можно развернуть любым из следующих способов:

   * Перейдите к `manifest.template.json` файлу и щелкните правой кнопкой мыши, чтобы выбрать его `Deploy Teams app manifest` из контекстного меню.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="Развертывание манифеста":::

   * Триггер `Teams: Deploy Teams app manifest` из палитры команд.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="Развертывание из палитры команд":::

2. Обновление до платформы Teams.

   Вы можете выполнить обновление до платформы Teams любым из следующих способов:

   * Выберите **"Обновить до платформы Teams** " в левом верхнем углу `manifest.{env}.json`окна .

   * Trigger **Teams: Update manifest to Teams platform** on the menu bar of `manifest.{env}.json`.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="Обновление для команд":::

Вы также можете активировать **Teams: обновление манифеста для платформы Teams** из палитры команд:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="представление в виде дерева":::

> [!NOTE]
> Триггер из codelens редактора или строки меню обновляет текущий файл манифеста на платформу Teams. Для триггера из палитры команд требуется выбрать целевую среду.

 Команда CLI:

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> Изменения обновляются на портале разработки. Любые обновления вручную на портале разработчика перезаписываются.

Если файл манифеста устарел из-за изменения файла конфигурации или изменения шаблона, выберите одно из следующих действий:

* **Только предварительная** версия: локальный файл манифеста перезаписывается в соответствии с текущей конфигурацией.
* **Предварительный просмотр и обновление**: локальный файл манифеста перезаписывается в соответствии с текущей конфигурацией, а также обновляется до платформы Teams.
* **Отмена**: никаких действий не выполняется.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::

## <a name="customize-your-teams-app-manifest"></a>Настройка манифеста приложения Teams

Набор средств Teams состоит из следующих файлов шаблона манифеста в папке `manifest.template.json` в локальных и удаленных средах.

* `manifest.template.json`
* `templates/appPackage`

Во время локальной отладки или подготовки Набор средств Teams `manifest.template.json``state.{env}.json``config.{env}.json`загружает манифест из конфигураций и создает приложение Teams на [портале разработки](https://dev.teams.microsoft.com/apps).

### <a name="supported-placeholders-in-manifesttemplatejson"></a>Поддерживаемые заполнители в manifest.template.json

В следующем списке приведены поддерживаемые заполнители в следующих разделах `manifest.template.json`:

* `{{state.xx}}` — это предопределенный заполнитель, и его значение разрешается набором средств Teams с определением в `state.{env}.json`. Не изменяйте значения в `state.{env}.json`
* `{{config.manifest.xx}}` — это настраиваемый заполнитель, и его значение разрешается из `config.{env}.json`

**Добавление настраиваемого параметра**

1. Добавьте настраиваемый параметр следующим образом:</br>
   А. Добавьте заполнитель с шаблоном `manifest.template.json` `{{config.manifest.xx}}`.</br>
   Б. Добавьте значение конфигурации в `config.{env}.json`.

     ```json
     {
         "manifest": {
          "KEY": "VALUE"
          }
     }
     ```

2. Чтобы перейти к файлу конфигурации, выберите любой из заполнителей конфигурации **"** Перейти к файлу конфигурации" или "Просмотреть **файл состояния** " `manifest.template.json`.

### <a name="validate-manifest"></a>Проверка манифеста

Во время таких операций, как пакет **метаданных Zip Teams**, Набор средств Teams проверяет манифест на соответствие своей схеме. В следующем списке приведены различные способы проверки манифеста.

* В VSC запустите триггер из `Teams: Validate manifest file` палитры команд:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="Проверка файла":::

* В интерфейсе командной строки используйте команду:

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## To preview values for local and dev environment

In `manifest.template.json`, you can navigate to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Preview values":::

> [!NOTE]
> Provision the environment or execute local debug to generate values for placeholders.

You can navigate to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Select your environment":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Preview all values":::

::: zone-end

::: zone pivot="visual-studio"

## Edit Teams app manifest using Visual Studio

Teams Toolkit in Visual Studio loads manifest from `manifest.template.json` with configurations from `state.{env}.json` and `config.{env}.json` while provisioning and preparing app dependencies. You can also create Microsoft Teams app in [Developer Portal](https://dev.teams.microsoft.com/apps) with the manifest.

After scaffolding, in the manifest template file under `templates/appPackage` folder,
`manifest.template.json` is shared between local and remote environment.

In the manifest template, select **Project** > **Teams Toolkit** > **Open Manifest File**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="Open manifest file" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png":::

### Customize app manifest in Teams Toolkit

There are two types of placeholders in `manifest.template.json`:

* `{{state.xx}}` is pre-defined placeholder, whose value is resolved by Teams Toolkit, defined in `state.{env}.json`. It's recommended to not modify the values in `state.{env}.json`.
* `{{config.manifest.xx}}` is customized placeholder, whose value is resolved from `config.{env}.json`.

You can add a customized parameter by:

* Adding a placeholder in `manifest.template.json` with pattern: `{{config.manifest.xx}}`.
* Adding a config value in `config.{env}.json`.

    ```
        {
            "manifest": {
            "KEY": "VALUE"
            }
    }
    ```

### Preview app manifest in Teams Toolkit

You can preview values in app manifest in two ways:

* When you hover over the placeholder in `manifest.template.json`, then you can see the values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="Hover over placeholder" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png":::

* You can also hover over the key besides each placeholder in `manifest.template.json`, and you can see the same values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="Hover over key beside placeholder" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png":::

   > [!NOTE]
   > If the environment has not been provisioned, or the Teams app dependencies have not been prepared, it indicates that the values for placeholder have not been generated. Please follow the guidance inside hover to generate corresponding values.

### Preview manifest file

To preview the manifest file, you can sideload for local or deploy for Azure. You can preview the manifest file by performing the following step:

* Select **Project** > **Teams Toolkit** and trigger **Prepare Teams App Dependencies** or **Provision in the Cloud** that generates configuration for local or remote Teams app.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="Preview manifest file" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png":::

There are two other ways to upload zip app package before you can preview manifest file:

1. From the list of menu select **Project** > **Teams Toolkit** > **Zip App Package**, and select **For Local** or **For Azure**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Zip app package" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png":::

1. You can also upload zip app package from Solution Explorer, if you right-click on **MyTeamsApp1** and then select **Teams Toolkit** > **Zip App Package** > **For Local** or **For Azure**.

  > [!NOTE]
  > In this scenario the project name is **MyTeamsApp1**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="List of Teams Toolkit menus from solution explorer" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png":::

Teams Toolkit generates the zip app package, and to preview manifest file content you can follow the step below:

* Right-click on **manifest.template.json** under **appPackage** folder, select **Preview Manifest File** > **For Local** or **For Azure**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="Preview context menu" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png":::

This displays the preview of the manifest file in Visual Studio.

### Sync local changes to Developer Portal

After you've previewed the manifest file in Visual Studio, you can now sync the local changes to the Developer Portal. Select **Project** > **Teams Toolkit** > **Update Manifest in Teams Developer Portal**, or context menu from Solution Explorer. You can now preview the manifest file in Developer Portal as a result of syncing the local changes.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Update manifest in teams developer portal" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png":::

> [!NOTE]
> The changes are updated to Teams Developer Portal. If you have some manual updates in Developer Portal, that can be overwritten. In the **Warning** dialog box you can select **Overwrite and update** or **Cancel**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="Update warning" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png":::

::: zone-end

## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)

* [Provision cloud resources using Visual Studio](provision-cloud-resources.md)

* [Deploy Teams app to the cloud using Visual Studio](deploy-teams-app.md)
