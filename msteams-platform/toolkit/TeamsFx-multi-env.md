---
title: Работа с несколькими средами TeamsFX в наборе средств Teams
author: MuyangAmigo
description: О множественной среде TeamsFX
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 284cc455cdbb7a0c5b859fd4909f0c3a1a99b037
ms.sourcegitcommit: ff31cbe4840191f004d8fc61dd4fd93d35fcaecb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2022
ms.locfileid: "65938954"
---
# <a name="manage-multiple-environments"></a>Управление несколькими средами

 Набор средств Teams предоставляет простой способ, чтобы создать несколько сред и управлять ими, подготовить и развернуть артефакты в целевой среде для приложения Teams.

 С несколькими средами можно выполнять следующие действия:

1. **Тестирование перед** рабочей средой. Вы можете настроить несколько сред, таких как разработка, тестирование и промежуточное хранение, перед публикацией приложения Teams в рабочей среде в современном жизненном цикле разработки приложений.

2. **Управление поведением** приложений в разных средах. Вы можете настроить различные поведения для нескольких сред, например включить телеметрию в рабочей среде, но отключить ее в среде разработки.

## <a name="prerequisite"></a>Предварительное условие

* Установка [последней версии набора средств Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Откройте проект приложения Teams в Visual Studio Code.

## <a name="create-a-new-environment"></a>Создайте новую среду

После создания нового проекта набор средств Teams по умолчанию создает всё нижеперечисленное:

* Одна среда `local`, представляющая конфигурации среды локального компьютера
* Одна среда `dev`, представляющая конфигурации удаленной или облачной среды

> [!NOTE]
> Каждый проект может иметь только одну среду `local`, но несколько удаленных сред.

**Чтобы добавить другую удаленную среду**:

1. Выберите панель **"Добавить** :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/teams-toolkit-sidebar-icon.png" alt-text="боковую панель"::: " для единого входа Teams на левой панели навигации.
2. Выберите **+Teams: Создайте среду в** разделе **"Среда** ", как показано на следующем рисунке:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="создать":::

   Если у вас несколько сред, необходимо выбрать существующую среду, чтобы создать ту же среду. Эта команда копирует содержимое `config.<newEnv>.json` и `azure.parameters.<newEnv>.json` из существующей среды, выбранной вами, в созданную среду.

## <a name="select-target-environment"></a>Выбор целевой среды

Вы можете выбрать целевую среду для всех операций, связанных со средой. При наличии нескольких удаленных сред набор средств просит указать целевую среду, как показано на следующем рисунке:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="add env":::

## <a name="project-folder-structure"></a>Структура папки проекта

После создания проекта можно просмотреть папки и файлы проекта в **обозревателе** в VS Code. Помимо пользовательских кодов, Набор средств Teams использует некоторые файлы для поддержки конфигурации, состояния и шаблона приложения. Следующий список перечисляет файлы и описывает их связь с несколькими средами.

* `.fx/configs`: настройте файлы, которые пользователь может настроить для приложения Teams.
  * `config.<envName>.json`: файл конфигурации для каждой среды
  * `azure.parameters.<envName>.json`: файл параметров для подготовки Azure bicep для каждой среды.
  * `projectSettings.json`: глобальные параметры проекта, которые применяются ко всем средам
* `.fx/states`: подготовка результата, созданного набором средств
  * `state.<envName>.json`: подготовка выходного файла для каждой среды;
  * `<env>.userdata`: пользовательские данные для выходных данных подготовки для каждой среды;
* `templates`
  * `appPackage`: файлы шаблонов манифеста приложения
  * `azure`: файлы шаблонов Bicep

## <a name="customize-resource-provision"></a>Настройка подготовки ресурсов

Набор средств Teams позволяет изменять файлы конфигурации и файлы шаблонов для настройки подготовки ресурсов в каждой среде.

В следующей таблице перечислены распространенные сценарии подготовки настраиваемых ресурсов.

| Сценарии | Расположение| Описание |
| --- | --- | --- |
| Настройка ресурса Azure | <ul> <li>Файлы Bicep в `templates/azure`</li> <li>`.fx/azure.parameters.<envName>.json`</li></ul> | [Настройка параметров и шаблонов ARM](provision.md#customize-arm-parameters-and-templates) |
| Повторное использование существующего приложения Azure AD для приложения Teams  | <ul> <li>Раздел `auth` в `.fx/config.<envName>.json`</li> </ul> |  [Использование существующего приложения Azure AD для приложения Teams](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| Повторное использование существующего приложения Azure AD для бота | <ul> <li>Раздел `bot` в `.fx/config.<envName>.json`</li> </ul> | [Использование существующего приложения Azure AD для бота](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| Пропустить добавление пользователя во время подготовки SQL | <ul> <li>Свойство `skipAddingSqlUser` в `.fx/config.<envName>.json`</li> </ul> | [Пропустить добавление пользователя для базы данных SQL](provision.md#skip-adding-user-for-sql-database) |
| Настройка манифеста приложения | <ul> <li>`templates/manifest.template.json`</li> <li>Раздел `manifest` в `.fx/config.<envName>.json`</li>  </ul> | [Предварительный просмотр манифеста приложения в наборе средств](TeamsFx-preview-and-customize-app-manifest.md)|

## <a name="scenarios"></a>Сценарии

Ниже приведены сценарии настройки подготовки ресурсов в разных средах.
<br>

<br><details>
<summary><b>Сценарий 1. Настройка имени приложения Teams для разных сред </b></summary>

В качестве имени приложения Teams можно `myapp(dev)` задать среду по `dev` умолчанию и `myapp(staging)` промежуточную среду `staging`.

Выполните действия по настройке:

1. Откройте файл конфигурации `.fx/configs/config.dev.json`.
2. Обновите свойство *манифеста > appName > на* `myapp(dev)`.

  Изменения `.fx/configs/config.dev.json` будут выглядеть следующим образом:

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

3. Создайте новую среду и приведите `staging` к ней имя, если она не существует.
4. Откройте файл конфигурации `.fx/configs/config.staging.json`.
5. Обновите то же свойство `myapp(staging)`.
6. Запустите команду подготовки для сред `dev` и `staging`, чтобы обновить имя приложения в удаленных средах. Сведения о выполнении команды подготовки с помощью Набора средств Teams см. в [разделе "Подготовка"](provision.md#provision-using-teams-toolkit).

</details>

<details>
<summary><b>Сценарий 2. Настройка описания приложения Teams для разных сред</b></summary>

Вы можете задать разные описания приложений Teams для разных сред:

* Для среды по умолчанию `dev` описанием является `my app description for dev`
* Для среды промежуточного размещения `staging` описанием является `my app description for staging`

Выполните действия по настройке:

1. Откройте файл конфигурации `.fx/configs/config.dev.json`.
2. Добавьте новое свойство манифеста *> описание > с* значением `my app description for dev`.

  Изменения `.fx/configs/config.dev.json` будут выглядеть следующим образом:

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

3. Создайте новую среду и приведите `staging` к ней имя, если она не существует.
4. Откройте файл конфигурации `.fx/configs/config.staging.json`.
5. Добавьте то же свойство в `my app description for staging`.
6. Откройте шаблон манифеста приложения `templates/appPackage/manifest.template.json`Teams.
7. Обновите свойство, `description > short` чтобы использовать **переменную,** определенную в настройках файлов с синтаксисом кэша `{{config.manifest.description.short}}`.
  
  Изменения `manifest.template.json` будут выглядеть следующим образом:

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

8. Выполните команду подготовки для сред `dev` и `staging`, чтобы обновить имя приложения в удаленных средах.

</details>

<details>
<summary><b>Сценарий 3. Настройка описания приложения Teams для всех сред</b></summary>

В описании приложения Teams можно задать `my app description` значение для всех сред.

Так как шаблон манифеста приложения Teams используется во всех средах, мы можем обновить в нем значение описания для нашей целевой среды:

1. Откройте шаблон манифеста приложения `templates/appPackage/manifest.template.json`Teams.
2. Обновите свойство `description > short` **с жестко заданной строкой**`my app description`.
  
  Изменения `manifest.template.json` будут выглядеть следующим образом:

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

3. Выполните команду подготовки для **всех сред**, чтобы обновить имя приложения в удаленных средах.

</details>

<details>
<br><summary><b>Сценарий 4. Настройка ресурсов Azure для разных сред</b></summary>
Вы можете настроить ресурсы Azure для каждой среды, например изменить среду, соответствующую fx/configs/azure.parameters. {env}.json-файл для указания имени функции Azure.

Дополнительные сведения о файлах шаблонов и параметров Bicep см. в разделе ["Подготовка облачных ресурсов".](provision.md)
</details>
</br>

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов](provision.md)
* [Добавление дополнительных облачных ресурсов](add-resource.md)
* [Совместная работа с другими разработчиками в проекте Teams](TeamsFx-collaboration.md)
