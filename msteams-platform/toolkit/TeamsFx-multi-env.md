---
title: TeamsFX несколько сред в Teams набор средств
author: MuyangAmigo
description: О многоуровневой среде TeamsFX
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 27172617db35126fb086d8691486e86c2946f0bd
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453588"
---
# <a name="manage-multiple-environments-in-teams-toolkit"></a>Управление несколькими средами в Teams набор средств

 Teams набор средств предоставляет простой способ создания и управления несколькими средами, предоставлением и развертыванием артефактов в целевой среде для Teams App.

 С несколькими средами можно выполнить следующие функции:

1. **Тест** перед производством. Это распространенная практика, чтобы настроить несколько сред, таких как dev, test и staging перед публикацией приложения Teams для производственной среды в современном жизненном цикле разработки приложений.

2. **Управление поведением приложений в** разных средах: можно настроить различные действия для нескольких сред, например включить телеметрию в производственной среде, но отключить ее в среде разработки.

## <a name="prerequisite"></a>Предварительное условие

* [Установка Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии v3.0.0+.

> [!TIP]
> Убедитесь, что Teams проект приложения открыт в Microsoft Visual Studio коде.

## <a name="create-a-new-environment"></a>Создание новой среды

После создания нового проекта Teams набор средств по умолчанию создает:

* Одна `local` среда для представления конфигураций локальной компьютерной среды.
* Одна `dev` среда для представления конфигураций удаленной или облачной среды.

> [!NOTE]
> Каждый проект может иметь только одну `local` среду, но несколько удаленных сред.

Чтобы добавить другую удаленную среду, выберите значок Teams на боковой панели, выберите создание новой среды в разделе Окружающая среда, как показано на следующем изображении:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="создать":::

> [!NOTE]
> Если у вас несколько существующих сред, необходимо выбрать существующую среду, чтобы создать ту же. Команда будет копировать содержимое `config.<newEnv>.json` `azure.parameters.<newEnv>.json` файла из выбранной среды и из нее в создаемую новую среду.

## <a name="select-target-environment"></a>Выбор целевой среды

Можно выбрать целевую среду для всех операций, связанных с окружающей средой. Набор инструментов подсказок и запрос целевой среды, если у вас есть несколько удаленных сред, как показано на следующем изображении:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="добавление env":::

## <a name="project-folder-structure"></a>Project папки

После создания проекта можно просмотреть папки и файлы проекта в области обозревателя Visual Studio Code. Помимо пользовательских кодов, некоторые файлы используются Teams набор средств для поддержания config, состояния и шаблона приложения. Следующий список содержит файлы и описывает их связь с несколькими средами.

* `.fx/configs`: настройка файлов, которые пользователь может настроить для Teams приложения.
  * `config.<envName>.json`: файл конфигурации среды.
  * `azure.parameters.<envName>.json`Файл параметров среды для обеспечения бицепса Azure.
  * `projectSettings.json`: глобальные параметры проекта, применимые к всем средам.
  * `localSettings.json`: локальный файл конфигурации отлаговки.
* `.fx/states`: результат предоставления, который создается набор средств.
  * `state.<envName>.json`: файл вывода для обеспечения среды.
  * `<env>.userdata`: конфиденциальные пользовательские данные для среды для выпуска.
* `templates`
  * `appPackage`: файлы шаблонов манифеста приложений.
  * `azure`: Файлы шаблонов Bicep.

## <a name="customize-the-provision"></a>Настройка положения

Teams набор средств позволяет изменять файлы конфигурации и файлы шаблонов для настройки предоставления ресурсов в каждой среде.

В следующей таблице перечислены общие сценарии, поддерживаемые для настраиваемой реализации, а также места настройки:

| Сценарии | Расположение| Описание |
| --- | --- | --- |
| Настройка ресурса Azure | <ul> <li>Bicep files under `templates/azure`.</li> <li>`.fx/azure.parameters.<envName>.json`.</li></ul> | [Настройка ARM параметров и шаблонов](provision.md#customize-arm-parameters-and-templates). |
| Повторное использование существующего приложения Azure AD для Teams приложения | <ul> <li>`auth` раздел в`.fx/config.<envName>.json`.</li> </ul> |  [Используйте существующее приложение Azure AD для Teams приложения](provision.md#use-an-existing-azure-ad-app-for-your-teams-app). |
| Повторное использование существующего приложения Azure AD для бота | <ul> <li>`bot` раздел в`.fx/config.<envName>.json`.</li> </ul> | [Используйте существующее приложение Azure AD для бота](provision.md#use-an-existing-azure-ad-app-for-your-bot). |
| Пропустить добавление пользователя при SQL | <ul> <li>`skipAddingSqlUser`свойство.`.fx/config.<envName>.json`</li> </ul> | [Пропустить добавление пользователя для SQL базы данных](provision.md#skip-adding-user-for-sql-database). |
| Настройка манифеста приложения | <ul> <li>`templates/manifest.remote.template.json`.</li> <li>`manifest` раздел в`.fx/config.<envName>.json`.</li>  </ul> | [Настройка манифеста Teams в Teams набор средств](TeamsFx-manifest-customization.md). |

## <a name="scenarios"></a>Сценарии

### <a name="scenario-1-customize-teams-app-name-for-different-environment"></a>Сценарий 1: настройка Teams имени приложения для различных сред

Вы можете Teams имя приложения `myapp(dev)` `dev` `myapp(staging)` для среды по умолчанию и среды постановок.`staging`

Выполните следующие действия для настройки:

* 1. Откройте файл config `.fx/configs/config.dev.json`.
* 2. Обновление свойства *манифеста > appName > для*`myapp(dev)`

  Обновления будут `.fx/configs/config.dev.json` следующими:

  ```json
  {
      "$schema": "https://aka.ms/teamsfx-env-config-schema",
      "description": "You can customize the TeamsFx config for different environments.   Visit https://aka.ms/teamsfx-env-config to learn more about this.",
      "manifest": {
          "appName": {
              "short": "myapp(dev)"
              ...
          }
      }
      ...
  }
  ```

* 3. Создайте новую среду и назови `staging` ее, если она не существует.
* 4. Откройте файл config `.fx/configs/config.staging.json`.
* 5. Обнови это же свойство `myapp(staging)`.
* 6. Запустите команду обеспечения и `dev` `staging` среду для обновления имени приложения в удаленных средах. Чтобы выполнить команду обеспечения с Teams набор средств, см. [положение](provision.md#provision-using-teams-toolkit).

### <a name="scenario-2-customize-teams-app-description-for-different-environment"></a>Сценарий 2. настройка Teams приложения для различных сред

В этом сценарии вы узнаете, как Teams описание приложения для различных сред:

* Для среды по умолчанию `dev`описание будет;`my app description for dev`
* Для промежуточной среды `staging`описание будет;`my app description for staging`

Выполните следующие действия для настройки:

* 1. Откройте файл config `.fx/configs/config.dev.json`.
* 2. Добавьте новое свойство *манифеста > описание > с* значением `my app description for dev`.

  Обновления будут `.fx/configs/config.dev.json` следующими:

  ```json
  {
      "$schema": "https://aka.ms/teamsfx-env-config-schema",
      "description": "You can customize the TeamsFx config for different environments.   Visit https://aka.ms/teamsfx-env-config to learn more about this.",
      "manifest": {
          ...
          "description": {
              "short": "`my app description for dev"
              ...
          }
      }
      ...
  }
  ```

* 3. Создайте новую среду и назови `staging` ее, если она не существует.
* 4. Откройте файл config `.fx/configs/config.staging.json`.
* 5. Добавьте одно и то же свойство в `my app description for staging`.
* 6. Откройте Teams манифест приложения для удаленного.`templates/appPackage/manifest.remote.template.json`
* 7. Обнови свойство, `description > short` чтобы использовать **переменную,** определяемую в настройках файлов с синтаксис усов `{{config.manifest.description.short}}`.
  
  Обновления будут `manifest.remote.template.json` следующими:

  ```json
  {
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    ...
    "description": {
      "short": "{{config.manifest.description.short}}", 
      ...
    },
    ...
  }
  ```

* 8. Запустите команду обеспечения и `dev` `staging` среду для обновления имени приложения в удаленных средах. Чтобы выполнить команду обеспечения с Teams набор средств, см. [положение](provision.md#provision-using-teams-toolkit).

### <a name="scenario-3-customize-teams-app-description-for-all-environments"></a>Сценарий 3: настройка Teams приложения для всех сред

В этом сценарии вы узнаете, как настроить описание Teams для `my app description` всех сред.

Так как Teams манифеста приложения является общим для всех сред, мы можем обновить в нем значение описания для нашего целевого значения:

* 1. Откройте Teams манифест приложения для удаленного.`templates/appPackage/manifest.remote.template.json`
* 2. Обновление свойства с `description > short` **помощью строки с жесткой кодией**`my app description`.
  
  Обновления будут `manifest.remote.template.json` следующими:

  ```json
  {
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    ...
    "description": {
      "short": "my app description",
      ...
    },
    ...
  }

* 3. Run provision command against **all** environment to update the app name in remote environments. To run provision command with Teams Toolkit, see [provision](provision.md#provision-using-teams-toolkit).

### Scenario 4: customize Azure resources for different environment

You can customize Azure resources for each environment, for example specify Azure Function name, by editing the environment corresponding to `.fx/configs/azure.parameters.{env}.json` file.

For more information on Bicep template and parameter files, see [provision cloud resources](provision.md)

## See also

* [Provision cloud resources](provision.md)
* [Add more cloud resources](add-resource.md)
* [Collaborate with other developers on Teams project](TeamsFx-collaboration.md)
