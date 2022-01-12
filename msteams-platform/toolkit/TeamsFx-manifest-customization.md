---
title: Настройка манифеста Teams в Teams набор средств
author: zyxiaoyuer
description: Настройка манифеста приложения Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d9f2ea49ece8728101a738129e45dd8155887ebc
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768079"
---
# <a name="customize-app-manifest-in-teams-toolkit"></a>Настройка манифеста приложения в Teams набор средств

Teams набор средств состоит из следующих файлов шаблона манифеста в `templates/appPackage` папке:

- `manifest.local.template.json` - локальное приложение команд отлаговки
- `manifest.remote.template.json` — общий доступ во всех средах

## <a name="prerequisite"></a>Предварительное условие

* [Установка Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии v3.0.0+.

> [!TIP]
> Убедитесь, Teams проект приложения открыт в VS Code.

Во время предоставления Teams набор средств от , в сочетании с конфигурациями из и `manifest.remote.template.json` `state.{env}.json` создает `config.{env}.json` командное приложение на [портале Dev.](https://dev.teams.microsoft.com/apps)

Во время локального отлажений Teams набор средств нагрузки проявляются в сочетании с конфигурациями из и создает командное приложение `manifest.local.template.json` `localSettings.json` на [портале Dev.](https://dev.teams.microsoft.com/apps)

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>Поддерживаемый placeholder в manifest.remote.template.json

- `{{state.xx}}`является заранее определенным местоопределителям, значение которого определяется Teams набор средств, определенным в `state.{env}.json` . Убедитесь, что значения в состоянии не изменяются. {env}.json.
- `{{config.manifest.xx}}` является настраиваемым местообладателям, значение которого решается из `config.{env}.json` .
  - Настраиваемый параметр можно добавить следующим образом:
    - Добавьте местообладатель в manifest.remote.template.json с шаблоном: `{{config.manifest.xx}}`
    - Добавьте значение config в config. {env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

    Кроме каждого замещать config в `manifest.remote.template.json` , есть `Go to config file` . Вы можете перейти к файлу конфигурации, выбрав его.

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>Поддерживаемый placeholder в manifest.local.template.json

`{{localSettings.xx}}`является заранее определенным местоопределителям, значение которого определяется Teams набор средств, определенным в `localSettings.json` . Убедитесь, что значения в localSettings.json не изменяются.

 > [!NOTE]
 > Убедитесь, что не нужно настраивать локальный манифест.

## <a name="see-also"></a>См. также

[Предварительный Teams Манифест приложения в Teams набор средств](TeamsFx-manifest-preview.md)
