---
title: TeamsFX несколько сред в Teams набор средств
author: MuyangAmigo
description: О многоуровневой среде TeamsFX
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 0e53d90dd6ead30200dd1f07ba9a100a3d1f4ca1
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228182"
---
# <a name="manage-multiple-environments-in-teams-toolkit"></a>Управление несколькими средами в Teams набор средств

 Teams набор средств предоставляет разработчикам простой способ создания и управления несколькими средами, предоставлением и развертыванием артефактов в целевой среде для Teams App.

 С несколькими средами разработчики могут:

1. **Тест перед** производством . Это распространенная практика, чтобы настроить несколько сред (разработчик, тест, постановка) перед публикацией приложения Teams среды производства в современном жизненном цикле разработки приложений.

2. **Управление поведением** приложений в различных средах: разработчики могут устанавливать различные модели поведения для различных сред, например разработчики могут включить телеметрию в производственной среде, но отключить ее в среде разработки.

## <a name="prerequisite"></a>Предварительное условие

* [Установка Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии v3.0.0+.

>[!TIP]
> Вы уже должны иметь проект Teams приложения, открытый в коде VS.

## <a name="create-a-new-environment"></a>Создание новой среды

После создания нового проекта Teams набор средств по умолчанию создает:

- Одна `local` среда для представления конфигураций локальной компьютерной среды.
- Одна `dev` среда для представления конфигураций удаленной и облачной среды.

> [!NOTE]
> Каждый проект может иметь только одну `local` среду, но несколько удаленных сред.

Чтобы добавить еще одну удаленную среду, выберите значок Teams на боковой панели, нажмите кнопку Плюс в разделе Окружающая среда и выполните вопросы, чтобы создать, как показано на следующем изображении:

![add-env](./images/create-env.png)

> [!NOTE]
> Если у вас несколько существующих сред, необходимо выбрать существующую среду для создания среды. Команда будет копировать содержимое файла из выбранной среды и из нее в `config.<newEnv>.json` `azure.parameters.<newEnv>.json` создаемую новую среду.

## <a name="select-target-environment"></a>Выбор целевой среды 

С помощью концепции среды, Teams набор средств, для всех операций, связанных с окружающей средой, можно выбрать целевую среду для выполнения операций. В наборе инструментов будет предложена целевая среда, если у вас есть несколько удаленных сред, как показано на следующем изображении:

![выберите env](./images/select-env.png)

## <a name="project-folder-structure"></a>Project папки 

После создания проекта можно просмотреть папки и файлы проекта в области Explorer Visual Studio Code. Помимо пользовательских кодов, некоторые файлы используются Teams набор средств для поддержания конфиг, состояния и шаблона приложения. Ниже приводится список этих файлов и описаны их отношения с несколькими средами.

- `.fx/configs`: config-файлы, которые пользователь может настроить для Teams приложения.
  - `config.<envName>.json`: файл конфигурации среды.
  - `azure.parameters.<envName>.json`Файл параметров среды для обеспечения Azure BICEP.
  - `projectSettings.json`: глобальные параметры проекта, применимые к всем средам.
  - `localSettings.json`: локальный файл конфигурации отлаговки.
- `.fx/states`: результат предоставления, который создается набор средств.
  - `state.<envName>.json`: файл вывода для обеспечения среды.
  - `<env>.userdata`: конфиденциальные пользовательские данные для среды для выпуска.
- `templates`
  - `appPackage`: файлы шаблонов манифеста приложений.
  - `azure`: файлы шаблонов BICEP.

## <a name="customize-the-provision"></a>Настройка положения 

Teams набор средств позволяет изменять файлы и шаблоны config, чтобы настроить положение ресурсов в каждой среде.

В приведенной ниже таблице перечислены общие сценарии, поддерживаемые для настраиваемой реализации, а также места настройки:

| Сценарии | Где настроить | Настройка |
| --- | --- | --- |
| Настройка ресурса Azure | <ul> <li>ФАЙЛЫ BICEP под `templates/azure` .</li> <li>`.fx/azure.parameters.<envName>.json`.</li></ul> | Дополнительные [сведения можно ARM параметров](provision.md#customize-arm-parameters-and-templates) и шаблонов. |
| Повторное AAD приложения для Teams приложения | <ul> <li>`auth` раздел в `.fx/config.<envName>.json` .</li> </ul> | Дополнительные сведения можно найти AAD [приложения для](provision.md#use-an-existing-aad-app-for-your-teams-app) Teams приложения. |
| Повторное AAD приложения для бота | <ul> <li>`bot` раздел в `.fx/config.<envName>.json` .</li> </ul> | Дополнительные сведения можно найти [в AAD приложения для бота.](provision.md#use-an-existing-aad-app-for-your-bot) |
| Пропустить добавление пользователя при SQL | <ul> <li>`skipAddingSqlUser` свойство в `.fx/config.<envName>.json` .</li> </ul> | Для получения [дополнительных сведений обратитесь к SQL пользователя](provision.md#skip-adding-user-for-sql-database) для базы данных. |
| Настройка манифеста приложений | <ul> <li>`templates/manifest.remote.template.json`.</li> <li>`manifest` раздел в `.fx/config.<envName>.json` .</li>  </ul> | Дополнительные [сведения Teams App Manifest в Teams набор средств.](TeamsFx-manifest-customization.md) |

## <a name="scenarios"></a>Сценарии

### <a name="scenario-1-customize-teams-app-name-for-different-environment"></a>Сценарий 1: настройка Teams имени приложения для различных сред

В этом примере вы узнаете, как Teams имя приложения для среды по умолчанию и среды `myapp(dev)` `dev` `myapp(staging)` постановок. `staging`

Выполните действия по настройке:

- Шаг 1: открытый файл config `.fx/configs/config.dev.json` .
- Шаг 2: обновление свойства манифеста > *appName > для*`myapp(dev)`

  Обновления для `.fx/configs/config.dev.json` :

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

- Шаг 3. Создайте новую среду `staging` с именем, если она не существует.
- Шаг 4: открытый файл config `.fx/configs/config.staging.json` .
- Шаг 5: обновление того же свойства шага 2 до `myapp(staging)` .
- Шаг 6: запустите команду обеспечения и среду для обновления имени `dev` `staging` приложения в удаленных средах. Для запуска команды обеспечения с помощью Teams набор средств. Дополнительные сведения см. [в этом документе.](provision.md#provision-using-teams-toolkit)

### <a name="scenario-2-customize-teams-app-description-for-different-environment"></a>Сценарий 2. настройка Teams приложения для различных сред

В этом сценарии вы узнаете, как задать различные Teams приложения для различных сред:

- Для среды по умолчанию `dev` описание `my app description for dev` будет;
- Для промежуточной среды `staging` описание `my app description for staging` будет;

Действия по настройке:

- Шаг 1: открытый файл config `.fx/configs/config.dev.json` .
- Шаг 2. Добавление нового свойства описания манифеста > *> со* значением `my app description for dev` .

  Обновления для `.fx/configs/config.dev.json`

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

- Шаг 3. Создайте новую среду с `staging` именем, если она не существует.
- Шаг 4: открытый файл config `.fx/configs/config.staging.json` .
- Шаг 5. Добавьте одно и то же свойство шага 2 в `my app description for staging` .
- Шаг 6: откройте Teams шаблон манифеста приложения для удаленного `templates/appPackage/manifest.remote.template.json` .
- Шаг 7: обнови свойство, чтобы использовать переменную, определяемую в файлах `description > short` config с  синтаксис усов. `{{config.manifest.description.short}}`
  
  Обновления для `manifest.remote.template.json` :

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
- Шаг 8. Запустите команду обеспечения для обновления имени приложения в `dev` `staging` удаленных средах. Дополнительные сведения о том, как выполнить команду Teams набор средств с помощью Teams набор средств, можно обратиться к [этому документу.](provision.md#provision-using-teams-toolkit)

### <a name="scenario-3-customize-teams-app-description-for-all-environments"></a>Сценарий 3: настройка Teams приложения для всех сред

В этом сценарии вы узнаете, как настроить описание Teams для всех `my app description` сред.

Так как шаблон манифеста Teams является общим для всех сред, мы можем обновить в нем значение описания для нашей целевой цели:

- Шаг 1: откройте шаблон манифеста Teams для удаленного `templates/appPackage/manifest.remote.template.json` приложения.
- Шаг 2. Обновление свойства `description > short` строкой **с жесткой кодией.** `my app description`
  
  Обновления для `manifest.remote.template.json` :

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

- Step 3: run provision command against **all** environment to update the app name in remote environments. For how to run provision command with Teams Toolkit, you can refer to [this document](provision.md#provision-using-teams-toolkit) for more details.

### Scenario 4: customize Azure resources for different environment

You can customize Azure resources for each environment, for example specifying Azure Function name, by editing the environment corresponding `.fx/configs/azure.parameters.{env}.json` file.

For more information on BICEP template and parameter files, see [provision cloud resources](provision.md)

## See also

> [!div class="nextstepaction"]
> [Provision cloud resources](provision.md)

> [!div class="nextstepaction"]
> [Add more cloud resources](add-resource.md)

> [!div class="nextstepaction"]
> [Collaborate with other developers on Teams project](TeamsFx-collaboration.md)
