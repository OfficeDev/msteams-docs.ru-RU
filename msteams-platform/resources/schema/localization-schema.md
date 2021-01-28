---
title: Справка по схеме JSON файла локализации
description: Описывает схему локализации, поддерживаемую файлом локализации для Microsoft Teams
ms.topic: reference
keywords: Локализация схемы манифеста teams
ms.date: 05/20/2019
ms.openlocfilehash: 696a65de70a63e767f8fcdb040364fe90cde8716
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014602"
---
# <a name="reference-localization-file-json-schema"></a>Справка: схема JSON файла локализации

В файле локализации Microsoft Teams описываются переводы языков, которые будут обслуживаться на основе языковых параметров клиента. Файл должен соответствовать схеме, хранящейся в [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) папке . Дополнительные сведения [см. в локализации приложения.](~/concepts/build-and-test/apps-localization.md)

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

URL-https://, ссылающийся на схему JSON для манифеста.

> [!TIP]
> Укажите схему в начале манифеста, чтобы включить поддержку IntelliSense или аналогичную поддержку из редактора кода: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>name.short

**Строка, максимальная длина 30**

Заменяет соответствующую строку из манифеста приложения на значение, предоставленную здесь.

## <a name="namefull"></a>name.full

**Строка, максимальная длина 100**

Заменяет соответствующую строку из манифеста приложения на значение, предоставленную здесь.

## <a name="descriptionshort"></a>description.short

**Строка, максимальная длина 80**

Заменяет соответствующую строку из манифеста приложения на значение, предоставленную здесь.

## <a name="descriptionfull"></a>description.full

**Строка, максимальная длина 4000**

Заменяет соответствующую строку из манифеста приложения на значение, предоставленную здесь.

## <a name="statictabs0-910-5name"></a>staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name

**Строка, максимальная длина 128**

Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.

## <a name="bots0commandlists0-2commands0-9title"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ \\ .title

**Строка, максимальная длина 32**

Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.

## <a name="bots0commandlists0-2commands0-9description"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ \\ .description

**Строка, максимальная длина 128**

Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.

## <a name="composeextensions0commands0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title

**Строка, максимальная длина 32**

Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.

## <a name="composeextensions0commands0-9description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**Строка, максимальная длина 128**

Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.

## <a name="composeextensions0commands0-9parameters0-4title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title

**Строка, максимальная длина 32**

Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.

## <a name="composeextensions0commands0-9parameters0-4description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ \\ .description

**Строка, максимальная длина 128**

Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.

## <a name="composeextensions0commands0-9parameters0-4value"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ \\ .value

**Строка, максимальная длина 512**

Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ \\ .title

**Строка, максимальная длина 128**

Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.

## <a name="composeextensions0commands0-9taskinfotitle"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title

**Строка, максимальная длина 64**

Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.
