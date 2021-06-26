---
title: Локализация ссылки на схему JSON
description: Описывает схему локализации, поддерживаемую файлом локализации для Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: группы проявляют локализацию схемы
ms.date: 05/20/2019
ms.openlocfilehash: 6e8f666cc6bfa693d7f2f469fc58fd6ee4860a80
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140515"
---
# <a name="localize-json-schema-reference"></a>Локализация ссылки на схему JSON

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

|Свойство|Тип|Максимальная длина|Description|
|---------------|--------|---------|------------------|
|`$schema`|URI|Н/Д|URL https:// ссылки на схему JSON для манифеста.|
|`name.short`|String|30|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`name.full`|Строка|100|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`description.short`|String|80|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`description.full`|String|4000|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|String|128|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|String|32|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`## bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|String|128|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|String|32|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|String|128|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|String|32|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|String|128|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|String|512|Заменяет соответствующую строку из манифеста приложения значением, которое здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|String|128|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|String|64|Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.|

## <a name="see-also"></a>См. также

> [Локализация приложения](~/concepts/build-and-test/apps-localization.md)
