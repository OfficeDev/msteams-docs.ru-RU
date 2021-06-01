---
title: Локализация для приложения
description: Описывает соображения по локализации Microsoft Teams приложения.
ms.topic: conceptual
localization_priority: Normal
keywords: команды публикуют язык локализации AppSource в офисе магазина
ms.date: 05/15/2018
ms.openlocfilehash: 6dbdeb6d16c99aada23f8d74a92d958f9c29b69d
ms.sourcegitcommit: 118f7261d313feeac5b398fef56a44bd90104b2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2021
ms.locfileid: "52709630"
---
# <a name="localization-for-microsoft-teams-apps"></a>Локализация Microsoft Teams приложений

При локализации Microsoft Teams приложения необходимо учитывать следующее:

1. Список Teams магазина (если применимо).
1. Строки, стоящие перед конечным пользователем в манифесте приложения. Например, команды ботов.
1. Реагирование на локализованный текст, отправленный от пользователей.

## <a name="localizing-your-appsource-listing"></a>Локализация списка AppSource

При публикации в магазине необходимо знать, что локализация списка AppSource еще не поддерживается. Однако при подготовке к поддержке локализованных списков в магазине приложений можно добавить в список дополнительные языки. В настоящее время в списке [](/office/dev/store/submit-to-appsource-via-partner-center) веб-сайта [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) для вашего приложения будут отображаться только языковые сведения по умолчанию ,которые вы предоставляете в Центре партнеров для вашего списка.

### <a name="example-of-configuring-localization"></a>Пример настройки локализации

Чтобы настроить дополнительный язык для приложения, в [Центре](/office/dev/store/submit-to-appsource-via-partner-center)партнеров выберите английский и дополнительный язык приложения. Французский язык используется в этом примере:

1. Добавление английского языка
    * Заполните имя приложения.
    * Заполните краткое описание приложения на английском языке.
    * Заполните длинное описание приложения на английском языке.
    * В длинном описании также добавьте строку "Это приложение доступно на французском языке".
    * Upload изображения пользовательского интерфейса приложения (на английском языке).
2. Добавление французского языка
    * Заполните имя приложения.
    * Заполните краткое описание приложения на французском языке.
    * Заполните длинное описание приложения на французском языке.
    * Upload изображения пользовательского интерфейса приложения (на французском языке).

Изображения, которые вы загружаете на английском языке, будут использоваться в AppSource.

## <a name="localizing-the-strings-in-your-app-manifest"></a>Локализация строк в манифесте приложения

Чтобы правильно локализовать приложение, необходимо использовать схему Microsoft Teams v1.5+. Это можно сделать, установив атрибут в файле manifest.js'и обновив свойство manifestVersion до `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json '1.7'.

### <a name="example-manifestjson-change"></a>Пример manifest.jsизменения

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

Затем необходимо добавить свойство "локализацияInfo" с языком по умолчанию, который поддерживает ваше приложение. Язык по умолчанию используется в качестве конечного языка отката, если параметры клиента пользователя не совпадают ни с одним из дополнительных языков.

### <a name="example-manifestjson-change"></a>Пример manifest.jsизменения

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

Вы можете предоставить дополнительные файлы json с переводами всех строк пользователя, стоящих перед вами в манифесте. Эти файлы должны соответствовать схеме [JSON-файла](../../resources/schema/localization-schema.md) локализации, и они должны быть добавлены в свойство "локализацияИнфо" манифеста. Каждый файл соотносится с языковым тегом, который Teams клиент для выбора соответствующих строк. Тег языка принимает форму, но рекомендуется опустить часть для всех регионов, которые поддерживают <language> - <region> <region> нужный язык.

Клиент Teams применяет строки в этом порядке: языковые строки по умолчанию —> языка пользователя только строки -> языка пользователя + строки области пользователя.

Например, по умолчанию вы предоставляете язык "fr" (французский, все регионы) и дополнительные языковые файлы для "en" (английский язык, все регионы) и "en-GB" (английский, Великобритания). Если язык пользователя настроен на "en-GB":

1. Клиент Teams будет переписать строки "fr" со строками "en".
2. Переопиши их со строками "en-GB".

Если язык пользователя настроен на "en-ca": 

1. Клиент Teams будет переписать строки "fr" со строками "en".
2. Поскольку локализация "en-ca" не поставляется, будут использоваться локализации "en".

Если язык пользователя задан для "es-es", клиент Teams берет строки "fr" и не переопределит их ни с одним из языковых файлов.

Поэтому настоятельно рекомендуется предоставлять в манифесте переводы только на языке верхнего уровня (вместо "en-ru") и предоставлять переопределения на уровне региона только для нескольких строк, которые в них нуждаются.

### <a name="example-manifestjson-change"></a>Пример manifest.jsизменения

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

## <a name="handling-localized-text-submissions-from-your-users"></a>Обработка локализованных текстовых сообщений от пользователей

Если у вас есть локализованные версии приложения, очень вероятно, что пользователи будут отвечать на них одним и тем же языком. Teams не переводит отправки пользователей обратно на язык по умолчанию, поэтому вашему приложению потребуется это сделать. Например, если вы предоставляете локализованный, ответом на бот будет локализованный текст команды, а не `commandList` язык по умолчанию. Вашему приложению необходимо соответствующим образом реагировать.

## <a name="code-sample"></a>Пример кода

| Пример имени | Описание | .NET | Node.js |
|-------------|-------------|------|------|
| Локализация приложений | Microsoft Teams для локализации приложений с помощью бота и вкладки. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |


