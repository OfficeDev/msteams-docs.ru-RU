---
title: Локализация для групповых приложений
description: Описание проблем, связанных с локализацией приложения
keywords: Teams Publishing Store Office Publishing AppSource Language Localization
ms.date: 05/15/2018
ms.openlocfilehash: 138b6d66808fc5ed212f1cb0eed8579faea6f764
ms.sourcegitcommit: bac0226d9048c363d96bbaf6f5395388c5f5c45a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/06/2020
ms.locfileid: "45039274"
---
# <a name="localization-for-microsoft-teams-apps"></a>Локализация приложений Microsoft Teams

При локализации приложения Microsoft Teams необходимо учитывать три основных аспекта.

1. Список AppSource (если выполняется публикация в магазине приложений).
1. Строки конечного пользователя в манифесте приложения (например, команды Bot).
1. Реагирование на локализованный текст, отправленный пользователями;

## <a name="localizing-your-appsource-listing"></a>Локализация списка AppSource

Если вы публикуете в магазине приложений, вам необходимо знать, что локализация вашего списка AppSource пока не поддерживается. Однако в процессе подготовки к поддержке локализованных вхождений в магазине App можно добавить в список дополнительные языки. В настоящее время только сведения о языке по умолчанию (Английская версия), которые вы предоставляете в [центре партнеров](/dev/store/use-partner-center-to-submit-to-appsource) для вашего списка, будут отображаться в списке [веб-сайтов AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) для вашего приложения.

Чтобы настроить дополнительный язык для приложения, в [центре партнеров](/dev/store/use-partner-center-to-submit-to-appsource)выберите английский и дополнительный язык приложения. В этом примере используется французский язык.

1. Добавление английского языка
    * Введите имя приложения.
    * Заполните краткое описание приложения на английском языке.
    * Заполните подробное описание приложения на английском языке.
    * В подробном описании добавьте также строку "это приложение доступно на французском языке".
    * Отправьте изображения пользовательского интерфейса приложения (на английском языке).
2. Добавление французского языка
    * Введите имя приложения.
    * Заполните краткое описание приложения на французском языке.
    * Заполните подробное описание приложения на французском языке.
    * Отправьте изображения пользовательского интерфейса приложения (на французском языке).

Изображения, которые вы отправляете с английским языком, будут использоваться в AppSource.

## <a name="localizing-the-strings-in-your-app-manifest"></a>Локализация строк в манифесте приложения

Для правильной локализации приложения необходимо использовать схему приложения Microsoft Teams версии 1.5 +. Это можно сделать, присвоив `$schema` атрибуту в manifest.jsфайла значение ' https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json ' и обновив свойство ' версия манифеста ' до ' 1,7 '.

### <a name="example-manifestjson-change"></a>Пример manifest.jsпри изменении

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

Затем необходимо добавить свойство "Локализатионинфо" с языком по умолчанию, который поддерживает ваше приложение. В качестве последнего базового языка используется язык по умолчанию, если параметры клиента пользователя не совпадают с какими-либо из дополнительных языков.

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

Вы можете предоставить дополнительные файлы JSON с переводом всех строк, отличных от пользователя, в манифесте. Эти файлы должны соответствовать [схеме JSON файла локализации](../../resources/schema/localization-schema.md) , и их необходимо добавить в свойство "локализатионинфо" манифеста. Каждый файл соответствует тегу языка, который клиент Teams использует для выбора соответствующих строк. Тег Language имеет форму, <language> - <region> но мы не рекомендуем опустить <region> часть для всех регионов, поддерживающих нужный язык.

Клиент Teams будет применять строки в указанном порядке: строки языка по умолчанию — строки языка по умолчанию — > только строки > язык пользователя и строки области пользователя.

Например, вы предоставляете язык по умолчанию: "fr" (французский, все регионы) и дополнительные языковые файлы для "en" (английский, все регионы) и "en-GB" (английский, Великобритания). Если для языка пользователя задано значение "en-GB":

1. Клиент Teams получит строки "fr", заменяя их строками "en".
2. Перезаписать их строками "en – GB".

Если для языка пользователя задано значение "en-CA": 

1. Клиент Teams получит строки "fr", заменяя их строками "en".
2. Так как не указана локализация "en-CA", будут использоваться локализации "en".

Если для языка пользователя задано значение "es-ES", клиент Teams будет принимать строки "fr" и не будет переопределять их с помощью языковых файлов.

Таким образом, настоятельно рекомендуется предоставлять в манифесте только верхние и языковые переводы в манифесте ("en" вместо "en-US"), а также предоставлять переопределение на уровне области только для тех строк, которые им нужны.

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

### <a name="example-localization-json-file"></a>Пример файла Localization. JSON

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a>Обработка локализованных текстов, отправленных пользователями

Если вы предоставляете локализованные версии вашего приложения, то, скорее всего, ваши пользователи будут отвечать на один и тот же язык. Команды не переводятся обратно на язык по умолчанию, поэтому ваше приложение должно их обработать. Например, если вы задаете локализованные сообщения `commandList` , ответы на ваш Bot будут иметь локализованный текст команды, а не язык по умолчанию. Ваше приложение должно будет отвечать соответствующим образом.
