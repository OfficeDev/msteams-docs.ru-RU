---
title: Справочные материалы по локализации схемы JSON
description: Описание схемы локализации, поддерживаемой файлом локализации для Microsoft Teams, на примере схемы
ms.topic: reference
ms.localizationpriority: high
keywords: teams манифест схема локализация; teams manifest schema localization
ms.date: 05/20/2019
ms.openlocfilehash: cf55754b5f9b30508bc01184d75f489dc2a5b7b7
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111915"
---
# <a name="localize-json-schema-reference"></a>Справочные материалы по локализации схемы JSON

В файле локализации Microsoft Teams описаны переводы, которые обслуживаются на основе языковых параметров клиента. Файл должен соответствовать схеме, размещенной по адресу [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).

> [!TIP]
> Укажите схему в начале манифеста, чтобы включить `IntelliSense` или аналогичную поддержку в редакторе кода: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="example"></a>Пример

Ниже приведен пример схемы JSON для локализации.

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

|Свойство|Тип|Максимальная длина|Описание|
|---------------|--------|---------|------------------|
|`$schema`|URI|Н/Д|URL-адрес со ссылкой на схему JSON для манифеста (https://).|
|`name.short`|String|30|Заменяет соответствующую строку из манифеста приложения на указанное здесь значение.|
|`name.full`|Строка|100|Заменяет соответствующую строку из манифеста приложения на указанное здесь значение.|
|`description.short`|String|80|Заменяет соответствующую строку из манифеста приложения на указанное здесь значение.|
|`description.full`|String|4000|Заменяет соответствующую строку из манифеста приложения на указанное здесь значение.|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|String|128|Заменяет соответствующие строки из манифеста приложения на указанное здесь значение.|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|String|32|Заменяет соответствующие строки из манифеста приложения на указанное здесь значение.|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|String|128|Заменяет соответствующие строки из манифеста приложения на указанное здесь значение.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|String|32|Заменяет соответствующие строки из манифеста приложения на указанное здесь значение.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|String|128|Заменяет соответствующие строки из манифеста приложения на указанное здесь значение.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|String|32|Заменяет соответствующую строку из манифеста приложения на указанное здесь значение.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|String|128|Заменяет соответствующие строки из манифеста приложения на указанное здесь значение.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|String|512|Заменяет соответствующую строку из манифеста приложения на указанное здесь значение.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|String|128|Заменяет соответствующие строки из манифеста приложения на указанное здесь значение.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|String|64|Заменяет соответствующие строки из манифеста приложения на указанное здесь значение.|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.description`|String|128|Краткое описание уведомления|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.templateText`|String|128|Пример: "Пользователь {actor} создал для вас задачу {taskId}"|

## <a name="see-also"></a>Дополнительные ресурсы

[Локализация приложения](~/concepts/build-and-test/apps-localization.md)
