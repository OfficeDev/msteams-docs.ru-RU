---
title: Справочные материалы по схеме JSON файла локализации
description: Описывает схему локализации, поддерживаемую файлом локализации для Microsoft Teams.
keywords: Локализация схемы манифеста Teams
ms.date: 05/20/2019
ms.openlocfilehash: 2c0f449ef0b018e0ed377ea8f5d79b285b36e829
ms.sourcegitcommit: 0aeb60027f423d8ceff3b377db8c3efbb6da4d17
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/11/2020
ms.locfileid: "48997967"
---
# <a name="reference-localization-file-json-schema"></a>Ссылка: Схема файла локализации JSON

Файл локализации Microsoft Teams описывает переводы языка, которые будут обрабатываться в соответствии с языковыми параметрами клиента. Файл должен соответствовать схеме, размещенной на сайте [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) . Дополнительные сведения см. в разделе [локализация приложений](~/concepts/build-and-test/apps-localization.md).

## <a name="sample"></a>Пример

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "name.short": "Le App Studio",
  "name.full": "App Studio pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App Studio.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App Studio.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

Схема определяет следующие свойства:

## <a name="schema"></a>$schema

**URI**

URL-адрес https://, ссылающийся на схему JSON для манифеста.

> [!TIP]
> Укажите схему в начале манифеста, чтобы включить поддержку IntelliSense или аналогичную поддержку в редакторе кода: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>Name. Short

**Строка, максимальная длина — 30**

Заменяет соответствующую строку из манифеста приложения указанным здесь значением.

## <a name="namefull"></a>Name. Full

**Строка, максимальная длина 100**

Заменяет соответствующую строку из манифеста приложения указанным здесь значением.

## <a name="descriptionshort"></a>Description. Short

**Строка, максимальная длина 80**

Заменяет соответствующую строку из манифеста приложения указанным здесь значением.

## <a name="descriptionfull"></a>Description. Full

**Строка, максимальная длина 4000**

Заменяет соответствующую строку из манифеста приложения указанным здесь значением.

## <a name="statictabs0-910-5name"></a>Статиктабс \\ [([0-9] | 1 [0-5]) \\ ] \\ . Name

**Строка, максимальная длина 128**

Заменяет соответствующие строки в манифесте приложения указанным значением.

## <a name="bots0commandlists0-2commands0-9title"></a>Боты \\ [0 \\ ] \\ . коммандлистс \\ [[0-2] \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . Title

**Строка, максимальная длина 32**

Заменяет соответствующие строки в манифесте приложения указанным значением.

## <a name="bots0commandlists0-2commands0-9description"></a>Боты \\ [0 \\ ] \\ . коммандлистс \\ [[0-2] \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . Description

**Строка, максимальная длина 128**

Заменяет соответствующие строки в манифесте приложения указанным значением.

## <a name="composeextensions0commands0-9title"></a>компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . Title

**Строка, максимальная длина 32**

Заменяет соответствующие строки в манифесте приложения указанным значением.

## <a name="composeextensions0commands0-9description"></a>компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . Description

**Строка, максимальная длина 128**

Заменяет соответствующие строки в манифесте приложения указанным значением.

## <a name="composeextensions0commands0-9parameters0-4title"></a>компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . Title

**Строка, максимальная длина 32**

Заменяет соответствующие строки в манифесте приложения указанным значением.

## <a name="composeextensions0commands0-9parameters0-4description"></a>компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . Description

**Строка, максимальная длина 128**

Заменяет соответствующие строки в манифесте приложения указанным значением.

## <a name="composeextensions0commands0-9parameters0-4value"></a>компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . Value

**Строка, максимальная длина 512**

Заменяет соответствующие строки в манифесте приложения указанным значением.

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . parameters \\ [[0-4]]. варианты [[ \\ \\ \\ 0-9] \\ ] \\ . Title

**Строка, максимальная длина 128**

Заменяет соответствующие строки в манифесте приложения указанным значением.

## <a name="composeextensions0commands0-9taskinfotitle"></a>компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . таскинфо \\ . Title

**Строка, максимальная длина 64**

Заменяет соответствующие строки в манифесте приложения указанным значением.
