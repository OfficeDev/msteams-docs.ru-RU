---
title: Настройка Teams приложения в Teams набор средств
author: zyxiaoyuer
description: Настройка манифеста приложения Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: de85674891a53c1e87b43ae1d472daf35716c348
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073542"
---
# <a name="customize-app-manifest-in-toolkit"></a>Настройка манифеста приложения в набор средств

Teams набор средств состоит из следующих файлов шаблона `manifest.template.json` манифеста в папке в локальных и удаленных средах:

* `manifest.template.json`
* `templates/appPackage`


## <a name="prerequisite"></a>Предварительное условие

* Установка [последней версии набора средств Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Убедитесь, что Teams приложение открыто в Visual Studio Code.

Во время локальной отладки или подготовки Teams набор средств загружает `manifest.template.json`манифест из, `state.{env}.json``config.{env}.json`с конфигурациями из и создает приложение Teams на [портале разработки](https://dev.teams.microsoft.com/apps).


## <a name="placeholders-supported-in-manifesttemplatejson"></a>Заполнители, поддерживаемые в manifest.template.json

* `{{state.xx}}`является предопределенный заполнитель, и его значение разрешается Teams набор средств, определенных в `state.{env}.json`. Не изменяйте значения в состоянии. {env}.json
* `{{config.manifest.xx}}` настраивается заполнитель, и его значение разрешается из `config.{env}.json`

  1. Настраиваемый параметр можно добавить следующим образом:
      1. Добавьте заполнитель в manifest.template.json с шаблоном: `{{config.manifest.xx}}`
      2. Добавьте значение конфигурации в конфигурацию. {env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

   2. Вы можете перейти к файлу конфигурации, выбрав любой из заполнителей конфигурации Перейти к  файлу конфигурации или **просмотреть файл состояния** в`manifest.template.json`

## <a name="see-also"></a>См. также

[Предварительный Teams приложения в Teams набор средств](TeamsFx-manifest-preview.md)
