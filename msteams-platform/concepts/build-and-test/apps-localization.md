---
title: Локализация приложения
description: В этой статье описываются вопросы локализации приложения Microsoft Teams.
ms.topic: conceptual
keywords: Команды публикуют язык локализации AppSource для публикации Office в Магазине
ms.date: 05/15/2018
ms.openlocfilehash: 69bee0ee11238dc0e461e4fddf8ed01f0cfcccde
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014301"
---
# <a name="localization-for-microsoft-teams-apps"></a>Локализация приложений Microsoft Teams

При локализации приложения Microsoft Teams необходимо учитывать три основных области.

1. Описание в AppSource (если вы публикуете в Магазине приложений).
1. Строки, с которыми сталкиваются конечные пользователи, в манифесте приложения (например, команды ботов).
1. Реагирование на локализованный текст, отправленный пользователями.

## <a name="localizing-your-appsource-listing"></a>Локализация списка AppSource

При публикации в Магазине приложений необходимо помнить, что локализация вашего списка AppSource пока не поддерживается. Однако во время подготовки к поддержке локализованных объявлений в магазине приложений вы можете добавить в описание дополнительные языки. В настоящее время в списке [](/office/dev/store/submit-to-appsource-via-partner-center) веб-сайта [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) для вашего приложения будут отображаться только сведения о языке по умолчанию (английский), которые вы предоставляете в Центре партнеров для вашего приложения.

Чтобы настроить дополнительный язык для [](/office/dev/store/submit-to-appsource-via-partner-center)приложения, в Центре партнеров выберите английский и дополнительный язык приложения. В этом примере используется французский язык.

1. Добавление английского языка
    * В заполните имя приложения.
    * Заполните краткое описание приложения на английском языке.
    * Заполните длинное описание приложения на английском языке.
    * В длинном описании также добавьте строку "Это приложение доступно на французском языке".
    * Отправка изображений пользовательского интерфейса приложения (на английском языке).
2. Добавление французского языка
    * В заполните имя приложения.
    * Заполните краткое описание приложения на французском языке.
    * Заполните длинное описание приложения на французском языке.
    * Отправка изображений пользовательского интерфейса приложения (на французском языке).

Изображения, отложенные с английским языком, будут использоваться в AppSource.

## <a name="localizing-the-strings-in-your-app-manifest"></a>Локализация строк в манифесте приложения

Для правильной локализации приложения необходимо использовать схему приложения Microsoft Teams 1.5 и более. Это можно сделать, установив для атрибута в файле manifest.js'' и обновив свойство `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json 'manifestVersion' на '1.7'.

### <a name="example-manifestjson-change"></a>Пример manifest.jsпри изменении

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

Затем необходимо добавить свойство "localizationInfo" с языком по умолчанию, поддерживаемым приложением. Язык по умолчанию используется в качестве конечного языка для отката, если параметры клиента пользователя не соответствуют ни одному из дополнительных языков.

### <a name="example-manifestjson-change"></a>Пример manifest.jsпри изменении

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

В манифесте можно предоставить дополнительные JSON-файлы с переводами всех строк, с которыми сталкиваются пользователи. Эти файлы должны соответствовать схеме [JSON](../../resources/schema/localization-schema.md) файла локализации и добавляться в свойство localizationInfo манифеста. Каждый файл сопоставляется с языковым тегом, который клиент Teams использует для выбора соответствующих строк. Тег языка имеет форму, но рекомендуется опустить часть для всех регионов, которые поддерживают <language> - <region> <region> нужный язык.

Клиент Teams будет применять строки в этом порядке: строки языка по умолчанию -> только строки языка пользователя -> язык пользователя + строки области пользователя.

Например, вы предоставляете язык по умолчанию fr (французский, все регионы) и дополнительные языковые файлы для en (английский, все регионы) и en-gb (английский, Великобритания). Если для языка пользователя установлено "en-gb":

1. Клиент Teams будет переописывать строки "fr" строками en.
2. Переописывание строк en-gb.

Если для языка пользователя установлено "en-ca": 

1. Клиент Teams будет переописывать строки "fr" строками en.
2. Так как локализация en-ca не предоставляется, будет использоваться локализация en.

Если для языка пользователя задан "es-es", клиент Teams будет принимать строки fr и не переопределять их с помощью языковых файлов.

Поэтому настоятельно рекомендуется предоставлять в манифесте переводы только на языке верхнего уровня (en, а не en-us) и переопределять только те строки, которые в них нуждаются.

### <a name="example-manifestjson-change"></a>Пример manifest.jsпри изменении

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

## <a name="handling-localized-text-submissions-from-your-users"></a>Обработка локализованных текстовых отгрузок от пользователей

Если у вас есть локализованные версии приложения, весьма вероятно, что пользователи будут отвечать на один и тот же язык. Teams не переводит отправки пользователей обратно на язык по умолчанию, поэтому ваше приложение будет обрабатывать это. Например, если у вас есть локализованный текст, ответом бота будет локализованный текст команды, а не `commandList` язык по умолчанию. Ваше приложение будет реагировать соответствующим образом.
