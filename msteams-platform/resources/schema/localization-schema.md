---
title: Справочные материалы по локализации схемы JSON
description: Описывает схему локализации, поддерживаемую файлом локализации для Microsoft Teams с помощью примера схемы
ms.topic: reference
ms.localizationpriority: medium
keywords: группы проявляют локализацию схемы
ms.date: 05/20/2019
ms.openlocfilehash: 4b26c1d67a26a27e4c3c1738d508d81d67e74763
ms.sourcegitcommit: 58fe8a87b988850ae6219c55062ac34cd8bdbf66
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/12/2021
ms.locfileid: "60949595"
---
# <a name="localize-json-schema-reference"></a>Справочные материалы по локализации схемы JSON

Файл Microsoft Teams локализации описывает языковые переводы, которые обслуживаются в зависимости от параметров языка клиента. Файл должен соответствовать схеме, которая была на уровне [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json) .

> [!TIP]
> Укажите схему в начале манифеста, чтобы включить или аналогичную поддержку `IntelliSense` редактора кода: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`

## <a name="example"></a>Пример

Пример схемы локализации JSON:

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

|Свойство|Тип|Максимальная длина|Описание|
|---------------|--------|---------|------------------|
|`$schema`|URI|Н/Д|URL https:// ссылки на схему JSON для манифеста.|
|`name.short`|Строка|30|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`name.full`|Строка|100|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`description.short`|Строка|80|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`description.full`|Строка|4000|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|Строка|128|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|Строка|32|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`## bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|Строка|128|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|Строка|32|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|Строка|128|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|Строка|32|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|Строка|128|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|String|512|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|Строка|128|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|Строка|64|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|

## <a name="see-also"></a>См. также

[Локализация приложения](~/concepts/build-and-test/apps-localization.md)
