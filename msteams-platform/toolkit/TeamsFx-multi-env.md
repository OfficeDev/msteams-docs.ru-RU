---
title: Несколько сред TeamsFX в Teams набор средств
author: MuyangAmigo
description: О многоадресной среде TeamsFX
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 194c31d02424d08080dca981bb9fe6d963d0a416
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073085"
---
# <a name="manage-multiple-environments"></a>Управление несколькими средами

 Teams набор средств предоставляет простой способ создания и управления несколькими средами, подготовки и развертывания артефактов в целевой среде для Teams App.

 С несколькими средами можно выполнить следующие действия:

1. **Тестирование перед** рабочей средой. Вы можете настроить несколько сред, таких как разработка, тестирование и промежуточное хранение, перед публикацией приложения Teams в рабочей среде в современном жизненном цикле разработки приложений

2. **Управление поведением** приложений в разных средах. Вы можете настроить различные поведения для нескольких сред, например включить телеметрию в рабочей среде, но отключить ее в среде разработки.

## <a name="prerequisite"></a>Предварительное условие

* Установка [последней версии набора средств Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Убедитесь, что Teams приложение открыто в Microsoft Visual Studio коде.

## <a name="create-a-new-environment"></a>Создание среды

После создания нового проекта Teams набор средств по умолчанию создает:

* Одна `local` среда для представления конфигураций среды локального компьютера
* Одна `dev` среда для представления конфигураций удаленной или облачной среды

> [!NOTE]
> Каждый проект может иметь только одну `local` среду, но несколько удаленных сред.

**Чтобы добавить другую удаленную среду, с помощью этой функции можно выполнить следующее**:

1. Щелкните **значок Teams** на боковой панели
2. Выберите **+Teams: Создать среду** в разделе "Среда", как показано на следующем рисунке:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="создать":::

Если у вас несколько сред, необходимо выбрать существующую среду, чтобы создать ту же среду. Эта команда копирует содержимое файла `config.<newEnv>.json` `azure.parameters.<newEnv>.json` из существующей среды, выбранной вами, и из нее в созданную среду.

## <a name="select-target-environment"></a>Выбор целевой среды

Вы можете выбрать целевую среду для всех операций, связанных со средой. Служба набор средств запрашивает целевую среду при наличии нескольких удаленных сред, как показано на следующем рисунке:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="добавить env":::

## <a name="project-folder-structure"></a>Project папки

После создания проекта можно просмотреть папки и файлы проекта в области обозревателя Visual Studio Code. Помимо пользовательских кодов, некоторые файлы используются Teams набор средств для поддержки конфигурации, состояния и шаблона приложения. Следующий список содержит файлы и описывает их связь с несколькими средами.

* `.fx/configs`: настройте файлы, которые пользователь может настроить для Teams приложения.
  * `config.<envName>.json`: файл конфигурации для каждой среды 
  * `azure.parameters.<envName>.json`: для каждого файла параметров среды для подготовки Azure bicep
  * `projectSettings.json`: глобальные параметры проекта, которые применяются ко всем средам
* `.fx/states`: подготовка результата, созданного набор средств
  * `state.<envName>.json`: выходной файл подготовки для каждой среды
  * `<env>.userdata`: конфиденциальные данные пользователя для каждой среды для выходных данных подготовки
* `templates`
  * `appPackage`: файлы шаблона манифеста приложения
  * `azure`: файлы шаблонов Bicep

## <a name="customize-resource-provision"></a>Настройка подготовки ресурсов

Teams набор средств позволяет изменять файлы конфигурации и файлы шаблонов для настройки подготовки ресурсов в каждой среде.

В следующей таблице перечислены распространенные сценарии подготовки настраиваемых ресурсов.

| Сценарии | Местоположение| Описание |
| --- | --- | --- |
| Настройка ресурса Azure | <ul> <li>Файлы Bicep в разделе `templates/azure`</li> <li>`.fx/azure.parameters.<envName>.json`</li></ul> | [Настройка параметров и шаблонов ARM](provision.md#customize-arm-parameters-and-templates) |
| Повторное использование существующего приложения Azure AD для Teams приложения | <ul> <li>`auth` Раздел `.fx/config.<envName>.json`</li> </ul> |  [Использование существующего приложения Azure AD для Teams приложения](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| Повторное использование существующего приложения Azure AD для бота | <ul> <li>`bot` Раздел `.fx/config.<envName>.json`</li> </ul> | [Использование существующего приложения Azure AD для бота](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| Пропустить добавление пользователя во время подготовки SQL | <ul> <li>`skipAddingSqlUser` Свойство `.fx/config.<envName>.json`</li> </ul> | [Пропустить добавление пользователя для SQL базы данных](provision.md#skip-adding-user-for-sql-database) |
| Настройка манифеста приложения | <ul> <li>`templates/manifest.template.json`</li> <li>`manifest` Раздел `.fx/config.<envName>.json`</li>  </ul> | [Настройка Teams приложения в Teams набор средств](TeamsFx-manifest-customization.md) |

## <a name="scenarios"></a>Сценарии

Существует четыре сценария настройки подготовки ресурсов в разных средах.
<br>

<br><details>
<summary><b>Сценарий 1. Настройка Teams приложения для разных сред</b></summary>

Можно задать имя Teams для `myapp(dev)` `dev` `myapp(staging)` среды по умолчанию и промежуточной среды.`staging`

Выполните следующие действия для настройки:

1. Открытие файла конфигурации `.fx/configs/config.dev.json`
2. Обновите свойство *манифеста > appName > на*`myapp(dev)`

  Обновления будут `.fx/configs/config.dev.json` выглядеть следующим образом:

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

3. Создайте новую среду и приведите `staging` ее имя, если она не существует
4. Открытие файла конфигурации `.fx/configs/config.staging.json`
5. Обновление того же свойства `myapp(staging)`
6. Выполните команду подготовки в `dev` среде `staging` и обновите имя приложения в удаленных средах. Чтобы выполнить команду подготовки с Teams набор средств, см. [раздел "Подготовка".](provision.md#provision-using-teams-toolkit)
</details>
<br>


<details>
<summary><b>Сценарий 2. Настройка Teams приложения для разных сред</b></summary>

В этом сценарии вы узнаете, как задать различные Teams приложения для разных сред:

* Для среды по умолчанию `dev`описанием является `my app description for dev`
* Для промежуточной среды `staging`описание: `my app description for staging`

Выполните следующие действия для настройки:

1. Открытие файла конфигурации `.fx/configs/config.dev.json`
2. Добавление нового свойства манифеста *> описания > с коротким* значением `my app description for dev`

  Обновления будут `.fx/configs/config.dev.json` выглядеть следующим образом:

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

3. Создайте новую среду и приведите `staging` ее имя, если она не существует
4. Открытие файла конфигурации `.fx/configs/config.staging.json`
5. Добавьте то же свойство в `my app description for staging`
6. Открытие Teams манифеста приложения`templates/appPackage/manifest.template.json`
7. Обновите свойство, `description > short` чтобы использовать **переменную** , определенную в настройках файлов с синтаксисом кэша `{{config.manifest.description.short}}`
  
  Обновления будут `manifest.template.json` выглядеть следующим образом:

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

8. Выполните команду подготовки в `dev` среде `staging` и в среде, чтобы обновить имя приложения в удаленных средах. Чтобы выполнить команду подготовки с Teams набор средств, см. [раздел "Подготовка".](provision.md#provision-using-teams-toolkit)

</details>
<br>

<details>
<summary><b>Сценарий 3. Настройка Teams приложения для всех сред</b></summary>

В этом сценарии вы узнаете, как задать описание Teams для `my app description` всех сред.

Так как Teams манифеста приложения используется во всех средах, мы можем обновить в нем значение описания для нашего целевого объекта:

1. Открытие Teams манифеста приложения`templates/appPackage/manifest.template.json`
2. Обновление свойства с помощью `description > short` **жестко заданной строки** `my app description`
  
  Обновления будут `manifest.template.json` выглядеть следующим образом:

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
 ```
3. Выполните команду подготовки для **всех сред** , чтобы обновить имя приложения в удаленных средах. Чтобы выполнить команду подготовки с Teams набор средств, см. [раздел "Подготовка".](provision.md#provision-using-teams-toolkit)
<br></details>
<br>
<details>
<br><summary><b>Сценарий 4. Настройка ресурсов Azure для разных сред</b></summary>
Вы можете настроить ресурсы Azure для каждой среды, например указать имя функции Azure, отредактировать среду, соответствующую fx/configs/azure.parameters. {env}.json. Файл.

Дополнительные сведения о файлах шаблонов и параметров Bicep см 
</details> . в статье о подготовке облачных [ресурсов <](provision.md) br



## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов](provision.md)
* [Добавление дополнительных облачных ресурсов](add-resource.md)
* [Совместная работа с другими разработчиками в проекте Teams](TeamsFx-collaboration.md)