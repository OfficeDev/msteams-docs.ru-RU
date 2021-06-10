---
title: Ссылка на схему JSON файла локализации
description: Описывает схему локализации, поддерживаемую файлом локализации для Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: группы проявляют локализацию схемы
ms.date: 05/20/2019
ms.openlocfilehash: 3e4207fb3e862eac18c80ffc49e7c5648ae05c28
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019708"
---
# <a name="reference-localization-file-json-schema"></a>Справка: схема JSON-файла локализации

В Microsoft Teams локализации описываются языковые переводы, которые будут подаваться в зависимости от параметров языка клиента. Файл должен соответствовать схеме, которая была на уровне [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) . Дополнительные сведения см. [в сведениях о локализации приложений.](~/concepts/build-and-test/apps-localization.md)

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

URL https:// ссылки на схему JSON для манифеста.

> [!TIP]
> Укажите схему в начале манифеста, чтобы включить IntelliSense или аналогичную поддержку редактора кода:`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>name.short

**String, Max Length 30**

Заменяет соответствующую строку из манифеста приложения значением, которое здесь.

## <a name="namefull"></a>name.full

**String, Max Length 100**

Заменяет соответствующую строку из манифеста приложения значением, которое здесь.

## <a name="descriptionshort"></a>description.short

**String, Max Length 80**

Заменяет соответствующую строку из манифеста приложения значением, которое здесь.

## <a name="descriptionfull"></a>description.full

**String, Max Length 4000**

Заменяет соответствующую строку из манифеста приложения значением, которое здесь.

## <a name="statictabs0-910-5name"></a>staticTabs \\ [[[0-9]|1[0-5]] \\ ] \\ .name

**String, Max Length 128**

Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.

## <a name="bots0commandlists0-2commands0-9title"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ ].title

**String, Max Length 32**

Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.

## <a name="bots0commandlists0-2commands0-9description"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**String, Max Length 128**

Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.

## <a name="composeextensions0commands0-9title"></a>composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .title

**String, Max Length 32**

Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.

## <a name="composeextensions0commands0-9description"></a>composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .description

**String, Max Length 128**

Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.

## <a name="composeextensions0commands0-9parameters0-4title"></a>composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title

**String, Max Length 32**

Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.

## <a name="composeextensions0commands0-9parameters0-4description"></a>composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description

**String, Max Length 128**

Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.

## <a name="composeextensions0commands0-9parameters0-4value"></a>composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value

**String, Max Length 512**

Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ ].parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title

**String, Max Length 128**

Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.

## <a name="composeextensions0commands0-9taskinfotitle"></a>composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title

**String, Max Length 64**

Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.
