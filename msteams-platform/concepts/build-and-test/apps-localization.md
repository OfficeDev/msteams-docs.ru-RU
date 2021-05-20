---
title: Локализация для приложения
description: Описывает соображения для локализации вашего Microsoft Teams приложения.
ms.topic: conceptual
localization_priority: Normal
keywords: команды публикуют магазин офис публикации AppSource язык локализации
ms.date: 05/15/2018
ms.openlocfilehash: a55b8af97e5306843858e5844a017dd402ab3516
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566049"
---
# <a name="localization-for-microsoft-teams-apps"></a>Локализация для Microsoft Teams приложений

При локализации Microsoft Teams приложения необходимо учитывать следующее:

1. Ваш Teams (если это применимо).
1. Строка, обращенная к конечному пользователю в вашем приложении, проявляется. Например, команды ботов.
1. Реагирование на локализованный текст, представленный пользователями.

## <a name="localizing-your-appsource-listing"></a>Локализация списка AppSource

Если вы публикуете в магазине, вы должны знать, что локализация вашего списка AppSource еще не поддерживается. Однако в рамках подготовки к поддержке локализованных объявлений в магазине приложений вы можете добавить дополнительные языки в свой список. В настоящее время в [списке веб-сайта AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) для вашего приложения появится только информация о языке по умолчанию (английский), которую вы предоставляете в Партнер-центре для вашего объявления. [](/office/dev/store/submit-to-appsource-via-partner-center)

### <a name="example-of-configuring-localization"></a>Пример настройки локализации

Чтобы настроить дополнительный язык для вашего приложения, в [Партнер-центре,](/office/dev/store/submit-to-appsource-via-partner-center)выберите как английский, так и дополнительный язык приложения. Французский язык используется в этом примере:

1. Добавить английский язык
    * Заполните имя приложения.
    * Заполните краткое описание приложения на английском языке.
    * Заполните длинное описание приложения на английском языке.
    * В длинном описании, пожалуйста, также добавьте строку "Это приложение доступно на французском языке".
    * Upload изображения пользовательского интерфейса приложения (на английском языке).
2. Добавить французский язык
    * Заполните имя приложения.
    * Заполните краткое описание приложения на французском языке.
    * Заполните длинное описание приложения на французском языке.
    * Upload изображения пользовательского интерфейса приложения (на французском языке).

Изображения, которые вы загружаете на английском языке, будут использоваться в AppSource.

## <a name="localizing-the-strings-in-your-app-manifest"></a>Локализация строк в манифесте приложения

Вы должны использовать схему Microsoft Teams приложения v1.5 ", чтобы правильно локализовать приложение. Вы можете сделать это, установив `$schema` атрибут в вашем manifest.jsфайле на https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json '' и обновление 'manifestVersion' собственности на '1.7'.

### <a name="example-manifestjson-change"></a>Пример manifest.jsоб изменениях

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

Затем вы захотите добавить свойство 'localizationInfo' с языком по умолчанию, который поддерживает ваше приложение. Язык по умолчанию используется в качестве последнего языка возврата, если настройки клиента пользователя не соответствуют ни одному из ваших дополнительных языков.

### <a name="example-manifestjson-change"></a>Пример manifest.jsоб изменениях

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

Вы можете предоставить дополнительные файлы .json с переводами всех пользователей, сталкиваются строки в вашем манифесте. Эти файлы должны придерживаться [схемы локализации файла JSON,](../../resources/schema/localization-schema.md) и они должны быть добавлены к свойству 'localizationInfo' вашего манифеста. Каждый файл коррелирует с тегом языка, который Teams клиент использует для выбора соответствующих строк. Тег языка принимает форму, но <language> - <region> рекомендуется опустить часть для <region> таргетинга на все регионы, которые поддерживают нужный язык.

Клиент Teams будет применять строки в этом порядке: строки языка по умолчанию -> язык пользователя только строки -> язык пользователя и строки региона пользователя.

Например, вы предоставляете язык по умолчанию 'fr' (французский, все регионы), а также дополнительные языковые файлы для 'en' (английский, все регионы) и 'en-gb' (английский, Великобритания). Если язык пользователя настроен на 'en-gb':

1. Клиент Teams будет принимать строки 'fr' перезаписать их с 'en' строки.
2. Перезаписать тех, с "ан-гб" строки.

Если язык пользователя настроен на 'en-ca': 

1. Клиент Teams будет принимать строки 'fr' перезаписать их с 'en' строки.
2. Поскольку локализация "en-ca" не обеспечивается, будут использоваться локализации "en".

Если язык пользователя настроен на 'es-es', клиент Teams примет строки 'fr' и не переопределит их ни с одним из языковых файлов.

Поэтому настоятельно рекомендуется предоставлять переводы только на высшем уровне в вашем манифесте ('en' вместо 'en-us') и предоставлять переопределения только на уровне региона для нескольких строк, которые в них нуждаются.

### <a name="example-manifestjson-change"></a>Пример manifest.jsоб изменениях

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

Если вы предоставите локализованные версии приложения, то весьма вероятно, что пользователи ответят тем же языком. Teams не переводит представления пользователей обратно на язык по умолчанию, поэтому вашему приложению нужно будет справиться с этим. Например, если вы предоставляете `commandList` локализованный, ответы на ваш бот будет локализованный текст команды, а не язык по умолчанию. Ваше приложение должно будет реагировать соответствующим образом.

## <a name="code-sample"></a>Пример кода

| Название образца | Описание | .NET |
|-------------|-------------|------|
| Локализация приложений | Microsoft Teams приложения с помощью бота и вкладки. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


