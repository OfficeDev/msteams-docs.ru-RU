---
title: Работа с несколькими средами TeamsFX в наборе средств Teams
author: surbhigupta
description: В этом модуле вы узнаете о нескольких средах TeamsFX, таких как создание среды, выбор целевой среды и т. д.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 11/29/2021
ms.openlocfilehash: 964e7d8ad6e643d26178e04fb9ce706bb177f1d1
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780998"
---
# <a name="manage-multiple-environments"></a>Управление несколькими средами

 Microsoft Teams Toolkit предоставляет простой способ создания и управления несколькими средами, подготовки и развертывания артефактов в целевой среде для приложения Microsoft Teams.

 В нескольких средах можно выполнить следующие действия:

1. **Тестирование перед** рабочей средой. Вы можете настроить несколько сред, таких как разработка, тестирование и промежуточное хранение, перед публикацией приложения Teams в рабочей среде в современном жизненном цикле разработки приложений.

2. **Управление поведением приложений в разных средах**. Вы можете настроить различные поведения приложений для нескольких сред, таких как включение телеметрии в рабочей среде.

   > [!NOTE]
   > Убедитесь, что данные телеметрии отключены в среде разработки.

   > [!TIP]
   > Откройте проект приложения Teams в Visual Studio Code.

## <a name="create-new-environment"></a>Создание среды

После создания проекта Набор средств Teams по умолчанию настраивает:

* Одна `local` среда, представляющая конфигурацию среды локального компьютера.
* Одна `dev` среда, представляющая конфигурацию удаленной или облачной среды.

> [!NOTE]
> Каждый проект может иметь только одну среду `local`, но несколько удаленных сред.

**Добавьте удаленную среду**:

1. Выберите набор **средств Teams** :::image type="content" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png" alt-text="на панели действий"::: на панели действий.
2. Выберите **+Teams: create new environment** under the **ENVIRONMENT** section as shown in the following image:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="создание среды":::

> [!Note]
> Если у вас несколько сред, необходимо выбрать существующую среду, чтобы создать ту же среду. Эта команда копирует содержимое файла `config.<newEnv>.json` `azure.parameters.<newEnv>.json` из существующей среды, выбранной вами, и из нее в созданную среду.

## <a name="target-environment"></a>Целевая среда

Вы можете выбрать целевую среду. Набор средств Teams предложит выбрать целевую среду при наличии нескольких удаленных сред:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="add env":::

## <a name="project-folder-structure"></a>Структура папки проекта

После создания проекта можно просмотреть папки и файлы проекта в **обозревателе** в Visual Studio Code. Помимо пользовательских кодов, Набор средств Teams `configs``states``templates` использует некоторые файлы для обслуживания приложения и приложения. Следующий список перечисляет файлы и описывает их связь с несколькими средами.

* `.fx/configs`: настраивает файлы, которые пользователь может настроить для приложения Teams.
  * `config.<envName>.json`: файл конфигурации для каждой среды.
  * `azure.parameters.<envName>.json`: файл параметров для подготовки Azure bicep для каждой среды.
  * `projectSettings.json`: глобальные параметры проекта, которые применяются ко всем средам.
* `.fx/states`: подготовка результата, созданного набором средств Teams.
  * `state.<envName>.json`: подготовка выходного файла для каждой среды.
  * `<env>.userdata`: пользовательские данные для выходных данных подготовки для каждой среды.
* `templates`
  * `appPackage`: файлы шаблонов манифеста приложения.
  * `azure`: файлы шаблонов Bicep.

## <a name="customize-resource-provision"></a>Настройка подготовки ресурсов

Набор средств Teams позволяет изменять файлы конфигурации и файлы шаблонов для настройки подготовки ресурсов в каждой среде.

В следующей таблице перечислены распространенные сценарии подготовки настраиваемых ресурсов.

| Сценарии | Расположение| Описание |
| --- | --- | --- |
| Настройка ресурса Azure |Файлы Bicep в `templates/azure` `.fx/azure.parameters.<envName>.json` | [Настройка параметров и шаблонов ARM](provision.md#customize-arm-template-files) |
| Повторное использование существующего приложения Azure AD для приложения Teams  | Раздел `auth` в `.fx/config.<envName>.json`|  [Использование существующего приложения Azure AD для приложения Teams](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| Повторное использование существующего приложения Azure AD для бота |Раздел `bot` в `.fx/config.<envName>.json`| [Использование существующего приложения Azure AD для бота](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| Пропустить добавление пользователя во время подготовки SQL |Свойство `skipAddingSqlUser` в `.fx/config.<envName>.json`| [Пропустить добавление пользователя для базы данных SQL](provision.md#skip-adding-user-for-sql-database) |
| Настройка манифеста приложения |`templates/manifest.template.json` файл в разделе `manifest` в `.fx/config.<envName>.json`| [Предварительный просмотр манифеста приложения в наборе средств](TeamsFx-preview-and-customize-app-manifest.md)|

## <a name="scenarios"></a>Сценарии

Ниже приведены сценарии настройки подготовки ресурсов в разных средах.
<br>

<br><details>
<summary><b>Сценарий 1. Настройка имени приложения Teams для разных сред </b></summary>

В качестве имени приложения Teams можно `myapp(dev)` задать среду по `dev` умолчанию и `myapp(staging)` промежуточную среду `staging`.

Действия по настройке:

1. Откройте файл конфигурации `.fx/configs/config.dev.json`.
2. Обновите свойство **short****`appName`** > **`manifest`** >  до .**`myapp(dev)`**

  Обновления:`.fx/configs/config.dev.json`

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

3. Вы можете создать новую среду и указать ее имя `staging` , если она не существует.
4. Откройте файл конфигурации `.fx/configs/config.staging.json`.
5. Обновите то же свойство `myapp(staging)`.
6. Теперь можно выполнить команду подготовки в среде `dev` `staging` и обновить имя приложения в удаленных средах. Сведения о выполнении команды подготовки с помощью Набора средств Teams см. в [разделе "Подготовка"](provision.md#provision-using-teams-toolkit-in-visual-studio-code).

</details>

<details>
<summary><b>Сценарий 2. Настройка описания приложения Teams для разных сред</b></summary>

Вы можете задать разные описания приложений Teams для разных сред:

* Для среды по умолчанию `dev`описание равно `my app description for dev`.
* Для промежуточной среды `staging`описанием является `my app description for staging`.

Действия по настройке:

1. Откройте файл конфигурации `.fx/configs/config.dev.json`.
2. Добавление нового свойства со **`manifest`** > **`short`** > **`description`** значением.**`my app description for dev`**

  Обновления:`.fx/configs/config.dev.json`

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
7. Обновите свойство, **`description`** > **`short`** чтобы использовать **переменную,** определенную в настройках файлов с синтаксисом кэша **`{{config.manifest.description.short}}`**.
  
  Обновления:`manifest.template.json`

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

8. Теперь можно выполнить команду подготовки в среде `dev` `staging` и в среде, чтобы обновить имя приложения в удаленных средах.

</details>

<details>
<summary><b>Сценарий 3. Настройка описания приложения Teams для всех сред</b></summary>

В описании приложения Teams можно задать `my app description` значение для всех сред.

Так как шаблон манифеста приложения Teams используется во всех средах, мы можем обновить в нем значение описания для нашей целевой среды:

1. Откройте шаблон манифеста приложения `templates/appPackage/manifest.template.json`Teams.
2. Обновите свойство **`description`** > **`short`** с жестко заданной строкой.**`my app description`**
  
  Обновления:`manifest.template.json`

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

3. Теперь можно выполнить команду подготовки во всех  средах, чтобы обновить имя приложения в удаленных средах.

</details>

<details>
<br><summary><b>Сценарий 4. Настройка ресурсов Azure для разных сред</b></summary>

Вы можете настроить ресурсы Azure для каждой среды, например изменить среду, соответствующую fx/configs/azure.parameters. {env}.json-файл для указания имени функции Azure.

Дополнительные сведения о файлах шаблонов и параметров Bicep см. в разделе ["Подготовка облачных ресурсов"](provision.md).
</details>
</br>

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов](provision.md)
* [Добавление дополнительных облачных ресурсов](add-resource.md)
* [Совместная работа с другими разработчиками в проекте Teams](TeamsFx-collaboration.md)
* [Тестирование поведения приложения в разных средах](test-app-behavior.md)
