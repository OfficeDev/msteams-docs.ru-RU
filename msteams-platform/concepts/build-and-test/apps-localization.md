---
title: Локализация приложения
description: Описание вопросов локализации приложения Microsoft Teams.
ms.topic: conceptual
ms.localizationpriority: high
keywords: teams публикация магазин office публиковать AppSource локализация язык
ms.date: 05/15/2018
ms.openlocfilehash: 000a448a467e3ed8244413be0c3b68c7eee02ea5
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111978"
---
# <a name="localize-your-app"></a>Локализация приложения

При локализации приложения Microsoft Teams учитывайте следующие факторы.

1. [Локализация описания в AppSource](#localize-your-appsource-listing).
1. [Локализация строк в манифесте приложения](#localize-strings-in-your-app-manifest).
1. [Обработка отправленного пользователями локализованного текста](#handle-localized-text-submissions-from-your-users).

## <a name="localize-your-appsource-listing"></a>Локализация описания в AppSource

Если вы публикуете приложение в магазине, укажите метаданные (описания, снимки экрана, имя) на языках, на которых должно быть опубликовано ваше приложение, и явно укажите эти языки на странице **описания для магазина** в Центре партнеров. Дополнительные сведения см. в статье [Локализованные шрифты Microsoft AppSource](/office/dev/store/prepare-localized-solutions#localized-microsoft-appsource-fronts). Чтобы поддерживать локализованные описания в магазине приложений, вы можете добавить в описание дополнительные языки. Сведения о языке по умолчанию, которые вы предоставляете в [Центре партнеров](/office/dev/store/submit-to-appsource-via-partner-center) для вашего описания, отображаются в описании на [сайте AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource — это единое место для всех потребностей вашей команды. Он объединяет все, включая чаты, собрания, звонки, файлы и инструменты, чтобы обеспечить более продуктивную командную работу.") для вашего приложения. В настоящее время языком по умолчанию является английский.

### <a name="configure-localization"></a>Настройка локализации

Чтобы настроить дополнительный язык для приложения, в [Центре партнеров](/office/dev/store/submit-to-appsource-via-partner-center) выберите английский и дополнительный язык приложения. В следующем примере в качестве дополнительного языка используется французский.

1. Добавление английского языка
    * Введите имя приложения.
    * Введите краткое описание приложения на английском языке.
    * Введите длинное описание приложения на английском языке.
    * В длинном описании введите: **This app is available in French**.
    * Загрузите изображения пользовательского интерфейса приложения (на английском языке).
2. Добавление французского языка
    * Введите имя приложения.
    * Введите краткое описание приложения на французском языке.
    * Введите длинное описание приложения на французском языке.
    * Загрузите изображения пользовательского интерфейса приложения (на французском языке).

Изображения, которые вы загружаете на английском языке, используются в AppSource.

## <a name="localize-strings-in-your-app-manifest"></a>Локализация строк в манифесте приложения

Чтобы локализовать приложение, используйте схему приложения Microsoft Teams `v1.5` и более поздние версии. Это можно сделать, задав для атрибута `$schema` в файле manifest.json значение `https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json` или выше и обновив свойство `manifestVersion` до версии `$schema` (в данном случае `1.5`).

Добавьте свойство `localizationInfo` с языком по умолчанию, поддерживаемым приложением. Язык по умолчанию используется в качестве конечного резервного языка, если параметры клиента пользователя не соответствуют ни одному из дополнительных языков.

### <a name="example-manifestjson-change"></a>Пример изменения manifest.json

Следующий `manifest.json` помогает добавить свойство `localizationInfo` с языком по умолчанию, поддерживаемым приложением вместе с `additionalLanguages`:

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "localizationInfo": {
  "defaultLanguageTag": "en",
  "additionalLanguages": [
   {
    "languageTag": "es-mx",
    "file": "es-mx.json"
   }
  ]
 }
  ...
}
```

### <a name="example-localization-json-change"></a>Пример изменения JSON локализации

Ниже приводится пример JSON локализации:

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```

Вы можете предоставить дополнительные JSON-файлы с переводами всех строк с интерфейсом пользователя в манифесте. Эти файлы должны соответствовать [схеме JSON файла локализации](../../resources/schema/localization-schema.md) и их необходимо добавить в свойство `localizationInfo` манифеста. Каждый файл коррелирует с языковым тегом, который клиент Teams использует для выбора соответствующих строк. Тег языка имеет вид `<language>-<region>`, но вы можете опустить часть `<region>` для всех регионов, которые поддерживают нужный язык.

Клиент Teams применяет строки в следующем порядке: строки языка по умолчанию -> строки языка пользователя -> язык пользователя + строки региона пользователя.

Например, вы предоставляете язык по умолчанию fr (французский, все регионы) и дополнительные языковые файлы для en (английский, все регионы) и en-gb (английский, Великобритания), язык пользователя имеет значение en-gb. В зависимости от выбора языка происходят следующие изменения.

1. Клиент Teams берет строки fr и переписывает их на строки en.
1. Перепишите строки en на строки en-gb.

Если для языка пользователя установлено значение en-ca, зависимости от выбора языка происходят следующие изменения:

1. Клиент Teams берет строки fr и переписывает их на строки en.
1. Так как локализация en-ca не предоставляется, используются локализации en.

Если для языка пользователя установлено es-es, клиент Teams берет строки fr. Клиент Teams не переопределяет строки с какими-либо языковыми файлами, так как перевод es или es-es не предоставляется.

Таким образом, в манифесте должны быть переведены только языки верхнего уровня. Например, вместо `en` используйте `en-us`. Переопределения уровня региона необходимо предоставлять только для нескольких строк, которые в них нужны.

### <a name="example-manifestjson-change"></a>Пример изменения manifest.json

В следующем примере показано изменение `manifest.json`.

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en",
    "additionalLanguages": [
      {
        "languageTag": "en-gb",
        "file": "en-gb.json"
      },
      {
        "languageTag": "fr",
        "file": "fr.json"
      },
      {
        "languageTag": "pl",
        "file": "pl.json"
      }
    ]
  }
  ...
}
```

### <a name="example-localization-json-file"></a>Пример файла JSON локализации

 В следующем примере показано изменение `localization.json`.

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "name.short": "Le App",
  "name.full": "App pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

## <a name="handle-localized-text-submissions-from-your-users"></a>Обработка отправленного пользователями локализованного текста

Если у вас есть локализованные версии приложения, пользователи отвечают на одном языке. Так как Teams не переводит отправления пользователей обратно на язык по умолчанию, ваше приложение должно обрабатывать локализованные ответы на язык. Например, если у вас есть локализованный `commandList`, то ответами бота будет локализованный текст команды, а не язык по умолчанию. Ваше приложение должно отвечать соответствующим образом.

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | .NET | Node.js |
|-------------|-------------|------|------|
| Локализация приложений | Локализация приложений Microsoft Teams с помощью бота и вкладки. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

[Справочные материалы по локализации схемы JSON](~/resources/schema/localization-schema.md)
