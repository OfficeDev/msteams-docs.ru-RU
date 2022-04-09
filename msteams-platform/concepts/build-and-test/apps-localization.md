---
title: Локализация приложения
description: Описание рекомендаций по локализации Microsoft Teams приложения.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Teams publish store office publishing AppSource localization language
ms.date: 05/15/2018
ms.openlocfilehash: 25a7694017cc8002ac23cf7075c59488ceb9773d
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737040"
---
# <a name="localize-your-app"></a>Локализация приложения

Чтобы локализовать приложение Microsoft Teams, учитывайте следующие факторы.

1. [Локализация описания AppSource](#localize-your-appsource-listing).
1. [Локализация строк в манифесте приложения](#localize-strings-in-your-app-manifest).
1. [Обработка локализованных текстовых отправлений от пользователей](#handle-localized-text-submissions-from-your-users).

## <a name="localize-your-appsource-listing"></a>Локализация описания AppSource

При публикации приложения в Магазине укажите метаданные (описания, снимки экрана, имя) на языках, на которых должно быть указано ваше приложение, и явно укажите эти языки на странице описаний **Marketplace** в Центре партнеров. Дополнительные сведения см. в [локализованных интерфейсах Microsoft AppSource](/office/dev/store/prepare-localized-solutions#localized-microsoft-appsource-fronts). Чтобы поддерживать локализованные описания в магазине приложений, можно добавить в описание дополнительные языки. Сведения о языке по умолчанию, которые вы предоставляете в [Центре партнеров](/office/dev/store/submit-to-appsource-via-partner-center) для вашего описания, отображаются в списке веб-сайтов [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource — это одно место для всех потребностей вашей команды. объедиайте все, включая чаты, собрания, звонки, файлы и инструменты, чтобы обеспечить более эффективную командную работу.") для вашего приложения. В настоящее время языком по умолчанию является английский.

### <a name="configure-localization"></a>Настройка локализации

Чтобы настроить дополнительный язык для приложения [, в Центре](/office/dev/store/submit-to-appsource-via-partner-center) партнеров выберите английский и дополнительный язык приложения. Французский язык используется в качестве дополнительного языка в следующем примере:

1. Добавление английского языка
    * Введите имя приложения.
    * Введите краткое описание приложения на английском языке.
    * Введите длинное описание приложения на английском языке.
    * В длинном описании введите: **это приложение доступно на французском языке**.
    * Upload изображения пользовательского интерфейса приложения (на английском языке).
2. Добавление французского языка
    * Введите имя приложения.
    * Введите краткое описание приложения на французском языке.
    * Введите длинное описание приложения на французском языке.
    * Upload изображения пользовательского интерфейса приложения (на французском языке).

Изображения, отправляемые на английском языке, используются в AppSource.

## <a name="localize-strings-in-your-app-manifest"></a>Локализация строк в манифесте приложения

Используйте схему Microsoft Teams и `v1.5` более поздней версии для локализации приложения. Это можно сделать, `$schema` занив для атрибута в файле manifest.json `manifestVersion` `https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json` значение или выше и обновив свойство до `$schema` версии (`1.5`в данном случае).

Добавьте свойство `localizationInfo` с языком по умолчанию, поддерживаемым приложением. Язык по умолчанию используется в качестве конечного резервного языка, если параметры клиента пользователя не соответствуют ни одному из дополнительных языков.

### <a name="example-manifestjson-change"></a>Пример изменения manifest.json

Ниже показано `manifest.json` , как добавить свойство `localizationInfo` с языком по умолчанию, который поддерживает приложение, а также `additionalLanguages`:

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

### <a name="example-localization-json-change"></a>Пример изменения json локализации

Ниже приведен пример локализации JSON.

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```

Вы можете предоставить дополнительные JSON-файлы с переводами всех строк, доступных пользователю, в манифесте. Эти файлы должны соответствовать схеме [JSON](../../resources/schema/localization-schema.md) `localizationInfo` файла локализации и добавляться в свойство манифеста. Каждый файл сопоставляется с тегом языка, который Teams клиент для выбора соответствующих строк. Тег языка имеет форму, `<language>-<region>` `<region>` но вы можете опустить часть, чтобы выбрать все регионы, поддерживающие нужный язык.

Клиент Teams применяет строки в следующем порядке: строки языка по умолчанию — > строки языка пользователя —> язык пользователя + строки региона пользователя.

Например, вы предоставляете язык по умолчанию fr (французский, все регионы) и дополнительные языковые файлы для "en" (английский, все регионы) и "en-gb" (английский, Great Uk), язык пользователя имеет значение "en-gb". Следующие изменения внося в зависимости от выбранного языка:

1. Клиент Teams принимает строки fr и перезаписывает их строками en.
1. Перезапишите строки en строками en-gb.

Если для языка пользователя задано значение "en-ca", в зависимости от выбранного языка будут внесены следующие изменения:

1. Клиент Teams принимает строки fr и перезаписывает их строками en.
1. Так как локализация en-ca не предоставляется, используются локализации en.

Если для языка пользователя задано значение es-es, Teams принимает строки fr. Клиент Teams не переопределяет строки с любыми языковыми файлами, так как перевод "es" или "es-es" не предоставляется.

Поэтому в манифесте необходимо предоставить переводы только на языке верхнего уровня. Например, вместо `en` `en-us`. Необходимо предоставить переопределения на уровне региона только для нескольких строк, для которых они нужны.

### <a name="example-manifestjson-change"></a>Пример изменения manifest.json

Изменение `manifest.json` показано в следующем примере:

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

### <a name="example-localization-json-file"></a>Пример JSON-файла локализации

 Изменение `localization.json` показано в следующем примере:

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

## <a name="handle-localized-text-submissions-from-your-users"></a>Обработка локализованных отправок текста от пользователей

Если вы предоставляете локализованные версии приложения, пользователи отвечают на них на одном языке. Так Teams не переводит отправленные пользователем сообщения обратно на язык по умолчанию, ваше приложение должно обрабатывать локализованные языковые ответы. Например, если вы предоставляете `commandList`локализованный текст, ответом бота будет локализованный текст команды, а не язык по умолчанию. Ваше приложение должно отвечать соответствующим образом.

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | .NET | Node.js |
|-------------|-------------|------|------|
| Локализация приложений | Microsoft Teams локализации приложения с помощью бота и вкладки. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

[Справочные материалы по локализации схемы JSON](~/resources/schema/localization-schema.md)
