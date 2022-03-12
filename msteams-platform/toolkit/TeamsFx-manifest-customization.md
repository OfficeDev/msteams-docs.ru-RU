---
title: Настройка манифеста Teams приложения в Teams набор средств
author: zyxiaoyuer
description: Настройка манифеста приложения Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 047cd9bcd86c103c3c9cab22793fb7d187f7493d
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453602"
---
# <a name="customize-app-manifest-in-teams-toolkit"></a>Настройка манифеста приложения в Teams набор средств

Teams набор средств состоит из следующих файлов шаблона манифеста в папке`templates/appPackage`:

* `manifest.local.template.json` - локальное приложение команд отлаговки
* `manifest.remote.template.json` — общий доступ во всех средах

## <a name="prerequisite"></a>Предварительное условие

* [Установка Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии v3.0.0+.

> [!TIP]
> Убедитесь, что Teams в Visual Studio Code.

Во время предоставления Teams набор средств от `manifest.remote.template.json`, `state.{env}.json` `config.{env}.json`в сочетании с конфигурациями из и создает командное приложение на [портале Dev](https://dev.teams.microsoft.com/apps).

Во время локального отлажений Teams набор средств `manifest.local.template.json`нагрузки проявляются в сочетании `localSettings.json`с конфигурациями из и создает командное приложение на [портале Dev](https://dev.teams.microsoft.com/apps).

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>Поддерживаемый placeholder в manifest.remote.template.json

* `{{state.xx}}`является заранее определенным местоопределителям, значение которого определяется Teams набор средств, определенным в `state.{env}.json`. Убедитесь, что значения в состоянии не изменяются. {env}.json.
* `{{config.manifest.xx}}` является настраиваемым местообладателям, значение которого решается из `config.{env}.json`.
  * Настраиваемый параметр можно добавить следующим образом:
    * Добавьте местообладатель в manifest.remote.template.json с шаблоном: `{{config.manifest.xx}}`
    * Добавьте значение config в config. {env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

    Кроме каждого замещать config в `manifest.remote.template.json`, есть `Go to config file`. Вы можете перейти к файлу конфигурации, выбрав его.

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>Поддерживаемый placeholder в manifest.local.template.json

`{{localSettings.xx}}`является заранее определенным местоопределителям, значение которого определяется Teams набор средств, определенным в `localSettings.json`. Убедитесь, что значения в localSettings.json не изменяются.

 > [!NOTE]
 > Убедитесь, что не нужно настраивать локальный манифест.

## <a name="see-also"></a>См. также

[Предварительный Teams Манифест приложения в Teams набор средств](TeamsFx-manifest-preview.md)
