---
title: Локализация приложения
description: Описывает соображения по локализации Microsoft Teams приложения.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: команды публикуют язык локализации AppSource в офисе магазина
ms.date: 05/15/2018
ms.openlocfilehash: 13325d323ec1d4d87f6cd5ff64c4a6c71552e01c
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452699"
---
# <a name="localize-your-app"></a>Локализация приложения

Рассмотрим следующие факторы, чтобы локализовать Microsoft Teams приложение:

1. [Локализовать список AppSource](#localize-your-appsource-listing).
1. [Локализовать строки в манифесте приложения](#localize-strings-in-your-app-manifest).
1. [Обработка локализованных текстовых сообщений от пользователей](#handle-localized-text-submissions-from-your-users).

## <a name="localize-your-appsource-listing"></a>Локализация списка AppSource

Если вы публикуете приложение в магазине, укажите метаданные (описания, снимки экрана, имя) на языках, которые вы хотите, чтобы ваше приложение было включено в список, и четко укажите эти языки на странице Списки **Marketplace** в Центре партнеров. Дополнительные сведения см. [в локальных фронтах Microsoft AppSource](/office/dev/store/prepare-localized-solutions#localized-microsoft-appsource-fronts). Чтобы поддерживать локализованные списки в магазине приложений, в список можно добавить дополнительные языки. Языковые сведения по умолчанию, которые вы предоставляете в [Центре партнеров](/office/dev/store/submit-to-appsource-via-partner-center) для вашего списка, появляются в списке веб-сайта [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource — это одно место для всех потребностей вашей команды. свести все вместе, включая чаты, собрания, вызовы, файлы и инструменты, чтобы обеспечить более продуктивную командную работу.") для вашего приложения. В настоящее время языком по умолчанию является английский.

### <a name="configure-localization"></a>Настройка локализации

Чтобы настроить дополнительный язык для приложения в Центре партнеров [, выберите](/office/dev/store/submit-to-appsource-via-partner-center) английский и дополнительный язык приложения. Французский язык используется в качестве дополнительного языка в следующем примере:

1. Добавление английского языка
    * Введите имя приложения.
    * Введите краткое описание приложения на английском языке.
    * Введите длинное описание приложения на английском языке.
    * В длинном описании введите: **Это приложение доступно на французском языке**.
    * Upload изображения пользовательского интерфейса приложения (на английском языке).
2. Добавление французского языка
    * Введите имя приложения.
    * Введите краткое описание приложения на французском языке.
    * Введите длинное описание приложения на французском языке.
    * Upload изображения пользовательского интерфейса приложения (на французском языке).

Изображения, которые вы загружаете на английском языке, используются в AppSource.

## <a name="localize-strings-in-your-app-manifest"></a>Локализация строк в манифесте приложения

Необходимо использовать схему Microsoft Teams, `v1.5` а затем локализовать приложение. Это можно сделать, установив `$schema` атрибут в файле manifest.json `$schema` **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** `manifestVersion` или более высокий и обновив свойство до версии (`1.5`в данном случае).

Необходимо добавить свойство с `localizationInfo` языком по умолчанию, который поддерживает приложение. Язык по умолчанию используется в качестве конечного языка отката, если параметры клиента пользователя не совпадают ни с одним из дополнительных языков.

### <a name="example-manifestjson-change"></a>Пример изменения manifest.json

Следующий манифест.json `localizationInfo` помогает добавить свойство с языком по умолчанию, который поддерживает ваше приложение вместе с `additionalLanguages`:

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

### <a name="example-localization-json-change"></a>Пример изменения локализации .json

Ниже приводится пример локализации .json:

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```

Вы можете предоставить дополнительные файлы json с переводами всех строк пользователя, стоящих перед вами в манифесте. Эти файлы должны соответствовать схеме [JSON-файла](../../resources/schema/localization-schema.md) `localizationInfo` локализации, и они должны быть добавлены в свойство манифеста. Каждый файл соотносится с языковым тегом, который Teams клиент для выбора соответствующих строк. Тег языка принимает форму, `<language>-<region>` но вы можете опустить `<region>` часть для всех регионов, поддерживаюных нужный язык.

Клиент Teams применяет строки в следующем порядке: строки языка по умолчанию —> языка пользователя только строки -> языка пользователя + строки области пользователя.

Например, по умолчанию вы предоставляете язык "fr" (французский язык, все регионы) и дополнительные языковые файлы для "en" (английский, все регионы) и "en-GB" (английский, Великобритания), язык пользователя установлен на "en-GB". Следующие изменения происходят в зависимости от выбора языка:

1. Клиент Teams берет строки "fr" и переописывает их строками "en".
1. Переопиши строки "en" со строками "en-GB".

Если язык пользователя настроен на "en-ca", в зависимости от выбора языка происходят следующие изменения:

1. Клиент Teams берет строки "fr" и переописывает их строками "en".
1. Так как локализация "en-ca" не поставляется, используется локализация "en".

Если язык пользователя настроен на "es-es", Teams клиент принимает строки "fr". Клиент Teams не переопределяет строки ни с одним из языковых файлов, так как не предоставляется перевод "es" или "es-es".

Поэтому в манифесте необходимо предоставить только переводы верхнего уровня, языка. Например, "en" вместо "en-ru". Необходимо предоставить переопределения уровня региона только для нескольких строк, которые в них нуждаются.

### <a name="example-manifestjson-change"></a>Пример изменения manifest.json

Изменение manifest.json показано в следующем примере:

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

### <a name="example-localization-json-file"></a>Пример локализации файла .json

 Изменение localization.json показано в следующем примере:

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
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

## <a name="handle-localized-text-submissions-from-your-users"></a>Обработка локализованных текстовых сообщений от пользователей

Если вы предоставляете локализованные версии приложения, пользователи отвечают на них одним и тем же языком. Поскольку Teams не переводит отправки пользователей на язык по умолчанию, приложение должно обрабатывать локализованные языковые ответы. Например, если вы предоставляете `commandList`локализованный, ответы на бота являются локализованным текстом команды, а не языком по умолчанию. Ваше приложение должно отвечать соответствующим образом.

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | .NET | Node.js |
|-------------|-------------|------|------|
| Локализация приложений | Microsoft Teams с помощью бота и вкладки. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

[Справочные материалы по локализации схемы JSON](~/resources/schema/localization-schema.md)
