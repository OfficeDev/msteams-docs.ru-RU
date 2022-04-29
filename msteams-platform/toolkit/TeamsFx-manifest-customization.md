---
title: Настройка манифеста приложения Teams в наборе средств Teams
author: zyxiaoyuer
description: Настройка манифеста приложения Teams
ms.author: nliu
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 28a06da170ee52e4340aa3d401d39ad08f58e2ba
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65110262"
---
# <a name="customize-app-manifest-in-toolkit"></a>Настройка манифеста приложения в наборе средств

Набор средств Teams состоит из следующих файлов шаблона манифеста в папке `manifest.template.json` в локальных и удаленных средах.

* `manifest.template.json`
* `templates/appPackage`


## <a name="prerequisite"></a>Предварительное условие

* Установка [последней версии набора средств Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Откройте проект приложения Teams в Visual Studio Code.

Во время локальной отладки или подготовки набор средств Teams загружает манифест из `manifest.template.json` (с конфигурациями из `state.{env}.json`, `config.{env}.json`) и создает приложение Teams на [портале разработчика](https://dev.teams.microsoft.com/apps).


## <a name="placeholders-supported-in-manifesttemplatejson"></a>Заполнители, поддерживаемые в manifest.template.json

* `{{state.xx}}` — это предопределенный заполнитель, и его значение разрешается набором средств Teams с определением в `state.{env}.json`. Не изменяйте значения в state.{env}.json
* `{{config.manifest.xx}}` — настраиваемый заполнитель, а его значение разрешается из `config.{env}.json`

  1. Вы можете добавить настраиваемый параметр следующим образом.
      1. Добавьте заполнитель в manifest.template.json с шаблоном: `{{config.manifest.xx}}`
      2. Добавьте значение конфигурации в config.{env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

   2. Вы можете перейти к файлу конфигурации, выбрав любой из заполнителей конфигурации **Перейти к файлу конфигурации** или **Просмотреть файл состояния** в `manifest.template.json`

## <a name="see-also"></a>Дополнительные ресурсы

[Предварительный просмотр манифеста приложения Teams в наборе средств Teams](TeamsFx-manifest-preview.md)
