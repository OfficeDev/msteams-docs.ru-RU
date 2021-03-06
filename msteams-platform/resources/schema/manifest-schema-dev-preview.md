---
title: Developer Preview схемы манифеста
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams
ms.topic: reference
keywords: команды проявляют схему Developer Preview
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: c2009038341a22664b0f055fa9756a9d1eba87b9
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915092"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a>Схема манифеста предварительного просмотра разработчика для Microsoft Teams

Сведения о том, как включить предварительный просмотр разработчика, см. в [Microsoft Teams.](~/resources/dev-preview/developer-preview-intro.md)

> [!NOTE]
> * Если вы не используете функции предварительного просмотра разработчика, используйте манифест приложения [для функций GA.](~/resources/schema/manifest-schema.md)

Манифест Microsoft Teams описывает интеграцию приложения в продукт Microsoft Teams. Манифест должен соответствовать схеме, которая была на [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) уровне .

Дополнительные сведения о доступных функциях см. в фото: [Features in the Public Developer Preview for Microsoft Teams.](~/resources/dev-preview/developer-preview-features.md)

## <a name="sample-full-manifest"></a>Образец полного манифеста

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "devPreview",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "devicePermissions" : [ "geolocation", "media" ],
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "localizationInfo": {
    "defaultLanguageTag": "es-es",
    "additionalLanguages": [
      {
        "languageTag": "en-us",
        "file": "en-us.json"
      }
    ]
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters"
  },
  "description": {
    "short": "Short description of your app",
    "full": "Full description of your app"
  },
  "icons": {
    "outline": "%FILENAME-32x32px%",
    "color": "%FILENAME-192x192px"
  },
  "accentColor": "%HEX-COLOR%",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content?host=msteams",
      "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
      "websiteUrl": "https://contoso.com/content",
      "scopes": [ "personal" ]
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
  "connectors": [
    {
      "connectorId": "GUID-FROM-CONNECTOR-DEV-PORTAL%",
      "configurationUrl": "https://contoso.com/teamsconnector/configure",
      "scopes": [ "team"]
    }
  ],
  "composeExtensions": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "type" : "search",
          "context" : ["compose", "commandBox"],
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "description": "Enter the keywords to search for"
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "type" : "action",
          "fetchTask" : true,
          "context" : ["message"],
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType" : "text"
            }
          ]
        },
        {
          "id": "exampleMessageHandler",
          "title": "Message Handler",
          "description": "Domains that will create a preview when pasted into the compose box",
          "messageHandlers": [
            {
              "type" : "link",
              "value" : {
                "domains" : [
                  "mysite.someplace.com",
                  "othersite.someplace.com"
                ]
              }
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers",
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ],
  "webApplicationInfo": {
    "id": "AAD App ID",
    "resource": "Resource URL for acquiring auth token for SSO",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelSettings.Read.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "ChannelMessage.Read.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group",
      "Member.ReadWrite.Group",
      "Owner.ReadWrite.Group"
    ],
  },
   "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "developerUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ],
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  }
}
```

Схема определяет следующие свойства:

## <a name="schema"></a>$schema

*Необязательный, но рекомендуемый* &ndash; String

URL https:// ссылки на схему JSON для манифеста.

## <a name="manifestversion"></a>manifestVersion

**Обязательно** &ndash; String

Версия схемы манифеста, используемая этим манифестом. Это должно быть "devPreview".

## <a name="version"></a>version

**Обязательно** &ndash; String

Версия конкретного приложения. Если вы что-то обновляете в манифесте, необходимо также приумножная версия. Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции. Если это приложение было отправлено в магазин, новый манифест должен быть повторно отправлен и повторно проверен. Затем пользователи этого приложения получат новый обновленный манифест автоматически через несколько часов после его утверждения.

Если приложение запрашивает разрешения изменить, пользователям будет предложено обновить и повторно согласиться на приложение.

Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. MINOR. PATCH).

## <a name="id"></a>id

**Обязательно** &ndash; ID приложения Майкрософт

Уникальный идентификатор, созданный Корпорацией Майкрософт для этого приложения. Если вы зарегистрировали бота через Microsoft Bot Framework или веб-приложение вашей вкладки уже входит в Microsoft, вы уже должны иметь ID и ввести его здесь. В противном случае необходимо создать новый ID на портале регистрации приложений Microsoft[(Мои](https://apps.dev.microsoft.com)приложения), введите его здесь, а затем повторно использовать при добавлении [бота.](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="packagename"></a>packageName

**Обязательно** &ndash; String

Уникальный идентификатор для этого приложения в обратной нотации домена; например, com.example.myapp.

## <a name="developer"></a>developer

**Required**

Указывает сведения о вашей компании. Для приложений, представленных в AppSource (ранее Office Store), эти значения должны соответствовать сведениям в записи AppSource.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`name`|32 символа|✔|Имя отображения для разработчика.|
|`websiteUrl`|2048 символов|✔|Url https:// url-адрес веб-сайта разработчика. Эта ссылка должна принимать пользователей на страницу вашей компании или конкретного продукта.|
|`privacyUrl`|2048 символов|✔|Url https:// url-адрес политики конфиденциальности разработчика.|
|`termsOfUseUrl`|2048 символов|✔|Url https:// url-адрес для условий использования разработчика.|
|`mpnId`|10 символов|✔|**Необязательный** Идентификатор Сети партнеров Майкрософт, который определяет организацию-партнер, которая строит приложение.|

## <a name="localizationinfo"></a>локализацияInfo

**Необязательное**

Позволяет спецификацию языка по умолчанию, а также указатели для дополнительных языковых файлов. См. [локализацию.](~/concepts/build-and-test/apps-localization.md)

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`defaultLanguageTag`|4 символа|✔|Языковой тег строк в этом файле манифеста верхнего уровня.|

### <a name="localizationinfoadditionallanguages"></a>локализацияInfo.additionalLanguages

Массив объектов, указывающих дополнительные языковые переводы.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`languageTag`|4 символа|✔|Языковой тег строки в предоставленного файла.|
|`file`|4 символа|✔|Относительный путь к файлу .json, содержащим переведенные строки.|

## <a name="name"></a>name

**Required**

Имя приложения, отображаемого пользователям в Teams. Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource. Значения и `short` не `full` должны быть одинаковыми.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|30 символов|✔|Короткое имя отображения приложения.|
|`full`|100 символов||Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.|

## <a name="description"></a>description

**Required**

Описывает приложение для пользователей. Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.

Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, чтобы помочь потенциальным клиентам понять, что делает ваш опыт. В полном описании также следует отметить, если для использования требуется внешняя учетная запись. Значения и `short` не `full` должны быть одинаковыми.  Короткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|80 символов|✔|Краткое описание работы приложения, используемого при ограниченном пространстве.|
|`full`|4000 символов|✔|Полное описание приложения.|

## <a name="icons"></a>icons

**Required**

Значки, используемые в Teams приложении. Файлы значков должны быть включены в пакет отправки.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`outline`|2048 символов|✔|Относительный путь к прозрачному значку контура PNG 32x32.|
|`color`|2048 символов|✔|Относительный путь к значку PNG полного цвета 192x192.|

## <a name="accentcolor"></a>accentColor

**Обязательно** &ndash; String

Цвет, который можно использовать в сочетании с и в качестве фона для значков контура.

Значение должно быть допустимым цветовым кодом HTML, начиная, например, с `#4464ee` "#".

## <a name="configurabletabs"></a>configurableTabs

**Необязательное**

Используется, когда в вашем приложении есть опыт работы с вкладками канала команды, которая требует дополнительной конфигурации перед ее добавлением. Настраиваемые вкладки поддерживаются только в области команд, и в настоящее время поддерживается только одна вкладка для каждого приложения.

Объект — массив со всеми элементами `object` типа. Этот блок требуется только для решений, которые предоставляют настраиваемое решение вкладки канала.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|String|2048 символов|✔|URL-https://, который можно использовать при настройке вкладки.|
|`canUpdateConfiguration`|Логический|||Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания. По умолчанию: `true`|
|`scopes`|Массив перечислений|1|✔|В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области. |
|`sharePointPreviewImage`|String|2048||Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint. Размер 1024x768. |
|`supportedSharePointHosts`|Массив перечислений|1||Определяет, как вкладка будет доступна в SharePoint. Параметры `sharePointFullPage` и `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Необязательное**

Определяет набор вкладок, которые можно "прикрепить" по умолчанию, не добавляя их вручную. Статические вкладки, объявленные в области, всегда прикрепяются к личному опыту `personal` приложения. Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.

Отрисуйка вкладок с адаптивными картами, указав вместо в `contentBotId` `contentUrl` **блоке staticTabs.**

Объект — массив (не более 16 элементов) со всеми элементами `object` типа. Этот блок требуется только для решений, которые предоставляют статическое решение вкладки.


|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`entityId`|String|64 символа|✔|Уникальный идентификатор для объекта, отображаемого на вкладке.|
|`name`|String|128 символов|✔|Отображение имени вкладки в интерфейсе канала.|
|`contentUrl`|String|2048 символов|✔|URL https://, который указывает на пользовательский интерфейс объекта, отображаемого на Teams холсте.|
|`contentBotId`|   | | | ID Microsoft Teams, указанный для бота на портале Bot Framework. |
|`websiteUrl`|String|2048 символов||В https:// нужно указать URL-адрес, если пользователь выбирает просмотр в браузере.|
|`scopes`|Массив перечислений|1|✔|В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в `personal` рамках личного опыта.|

## <a name="bots"></a>боты

**Необязательное**

Определяет решение бота, а также необязательные сведения, такие как свойства команд по умолчанию.

Объект — массив (максимум 1 элемент в настоящее время разрешен только для одного бота в приложении) со всеми &mdash; элементами типа `object` . Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|String|64 символа|✔|Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework. Это вполне может быть таким же, как общий [ID приложения](#id).|
|`needsChannelSelector`|Логический|||Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал. По умолчанию: `false`|
|`isNotificationOnly`|Логический|||Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы. По умолчанию: `false`|
|`supportsFiles`|Логический|||Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате. По умолчанию: `false`|
|`scopes`|Массив перечислений|3|✔|Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`). Эти параметры не являются исключающими.|

### <a name="botscommandlists"></a>bots.commandLists

Необязательный список команд, которые бот может рекомендовать пользователям. Объект — массив (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом. Дополнительные сведения см. в [меню Bot.](~/bots/how-to/create-a-bot-commands-menu.md)

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`items.scopes`|массив перечислений|3|✔|Указывает область, для которой действует список команд. Возможны значения `team`, `personal` и `groupchat`.|
|`items.commands`|массив объектов|10 |✔|Массив команд, поддерживаемых ботом:<br>`title`: имя команды бота (строка, 32).<br>`description`: простое описание или пример синтаксиса команды и его аргумента (строка, 128).|

## <a name="connectors"></a>соединители

**Необязательное**

Блок `connectors` определяет Office 365 соединители для приложения.

Объект — массив (максимум 1 элемент) со всеми элементами `object` типа. Этот блок необходим только для решений, которые предоставляют соединители.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|String|2048 символов|✔|URL https://, который необходимо использовать при настройке соединителя.|
|`connectorId`|String|64 символа|✔|Уникальный идентификатор соединитетеля, который соответствует его идентификатору в панели мониторинга разработчиков [соединителок.](https://aka.ms/connectorsdashboard)|
|`scopes`|Массив перечислений|1|✔|Указывает, предоставляет ли соединители опыт в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ). В настоящее время `team` поддерживается только область.|

## <a name="composeextensions"></a>composeExtensions

**Необязательное**

Определяет расширение обмена сообщениями для приложения.

> [!NOTE]
> В ноябре 2017 г. имя функции было изменено с "расширение составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжили функционировать.

Объект — массив (максимум 1 элемент) со всеми элементами `object` типа. Этот блок необходим только для решений, которые предоставляют расширение обмена сообщениями.

|Имя| Тип | Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|String|64|✔|Уникальный ID приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрирован в Bot Framework. Это вполне может быть таким же, как общий [ID приложения](#id).|
|`canUpdateConfiguration`|Логический|||Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями. Значение по умолчанию: `false`.|
|`commands`|Массив объекта|10 |✔|Массив команд, поддерживаемых расширением обмена сообщениями|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Расширение обмена сообщениями должно объявлять одну или несколько команд. Каждая команда отображается Microsoft Teams как потенциальное взаимодействие с точки входа на основе пользовательского интерфейса. Существует не более 10 команд.

Каждый элемент команды — это объект со следующей структурой:

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|String|64 символа|✔|ID для команды.|
|`type`|String|64 символа||Тип команды. Один `query` из или `action` . По умолчанию: `query`|
|`title`|String|32 символа|✔|Удобное имя команды.|
|`description`|String|128 символов||В описании, которое отображается пользователями, указывается назначение этой команды.|
|`initialRun`|Логический|||Значение Boolean, которое указывает, следует ли запускать команду изначально без параметров. По умолчанию: `false`|
|`context`|Массив строк|3||Определяет, из чего можно вызвать расширение сообщения. Любое сочетание `compose` `commandBox` , `message` . Значение по умолчанию: `["compose", "commandBox"]`|
|`fetchTask`|Логический|||Значение boolean, которое указывает, следует ли динамически получать модуль задач.|
|`taskInfo`|Объект|||Укажите модуль задач для предварительной загрузки при использовании команды расширения обмена сообщениями.|
|`taskInfo.title`|String|64||Начальное название диалогов.|
|`taskInfo.width`|String|||Ширина диалогов — число в пикселях или макет по умолчанию, такие как "большой", "средний" или "маленький".|
|`taskInfo.height`|String|||Высота диалогов — число пикселей или макет по умолчанию, например "большой", "средний" или "маленький".|
|`taskInfo.url`|String|||Начальный URL-адрес веб-просмотров.|
|`messageHandlers`|Массив объектов|5 ||Список обработчиков, которые позволяют вызывать приложения при определенных условиях. Домены также должны быть указаны в `validDomains` .|
|`messageHandlers.type`|String|||Тип обработка сообщений. Должно быть задано значение `"link"`.|
|`messageHandlers.value.domains`|Массив строк|||Массив доменов, для которые обработник сообщений ссылок может зарегистрироваться.|
|`parameters`|Массив объекта|5 |✔|Список параметров, которые принимает команда. Минимум: 1; максимум: 5|
|`parameter.name`|String|64 символа|✔|Имя параметра, как оно отображается в клиенте. Это включено в запрос пользователя.|
|`parameter.title`|String|32 символа|✔|Удобное название для параметра.|
|`parameter.description`|String|128 символов||Удобное для пользователя строка, описываемая назначение этого параметра.|
|`parameter.inputType`|String|128 символов||Определяет тип управления, отображаемого в модуле задач `fetchTask: true` для . Один `text` из `textarea` , , , , , `number` `date` `time` `toggle` `choiceset` .|
|`parameter.choices`|Массив объектов|10 ||Параметры выбора `choiceset` для . Используйте только `parameter.inputType` тогда, когда `choiceset` это .|
|`parameter.choices.title`|String|128||Название выбора.|
|`parameter.choices.value`|String|512||Значение выбора.|

## <a name="permissions"></a>permissions

**Необязательное**

Массив указывает, какие разрешения запрашивает приложение, что позволяет конечным пользователям узнать, как `string` будет выполняться расширение. Следующие параметры не являются эксклюзивными:

* `identity`&emsp;Требуется информация о удостоверении пользователя.
* `messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам группы.

Изменение этих разрешений при обновлении приложения приведет к тому, что пользователи повторят процесс согласия при первом запуске обновленного приложения.

## <a name="devicepermissions"></a>devicePermissions

**Необязательный** Массив строк

Указывает родных функций на устройстве пользователя, к которое ваше приложение может запрашивать доступ. Доступные варианты:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Необязательный,** за **исключением обязательного,** где отмечено

Список допустимого домена, из которого приложение ожидает загрузки любого контента. Списки домена могут включать, например, поддиайки. `*.example.com` Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` . Если конфигурации вкладок или пользовательскому интерфейсу контента необходимо перейти к любому другому домену, кроме одного использования для конфигурации вкладок, этот домен должен быть указан здесь.

Однако не **обязательно** включать в приложение домены поставщиков удостоверений, которые вы хотите поддерживать. Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить на accounts.google.com, но не следует включать accounts.google.com `validDomains[]` в .

> [!IMPORTANT]
> Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью подкрентов. Например, `yourapp.onmicrosoft.com` допустимо, `*.onmicrosoft.com` но не является допустимым.

Объект — массив со всеми элементами `string` типа.

## <a name="webapplicationinfo"></a>webApplicationInfo

**Необязательное**

Укажите свой AAD-ID и Graph, чтобы помочь пользователям легко войти в ваше приложение AAD.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|String|36 символов|✔|AAD-id приложения приложения. Этот id должен быть GUID.|
|`resource`|String|2048 символов|✔|URL-адрес ресурса приложения для приобретения маркера auth для SSO.|
|`applicationPermissions`|Массив|Не более 100 элементов|✔|Разрешения ресурсов для приложения.|

## <a name="configurableproperties"></a>configurableProperties

**Необязательный** - массив

Блок определяет свойства приложений, которые могут `configurableProperties` Teams администраторы. Дополнительные сведения см. в [приложении Enable customization.](~/concepts/design/enable-app-customization.md)

> [!NOTE]
> Необходимо определить как минимум одно свойство. В этом блоке можно определить максимум девять свойств.

Можно определить любое из следующих свойств:

* `name`: Имя отображения приложения.
* `shortDescription`Краткое описание приложения.
* `longDescription`Подробное описание приложения.
* `smallImageUrl`: Значок контура приложения.
* `largeImageUrl`: Значок цвета приложения.
* `accentColor`: Цвет, который нужно использовать в сочетании с и в качестве фона для значков контура.
* `developerUrl`URL-адрес HTTPS веб-сайта разработчика.
* `privacyUrl`: URL-адрес HTTPS политики конфиденциальности разработчика.
* `termsOfUseUrl`: URL-адрес HTTPS условий использования разработчика.

## <a name="defaultinstallscope"></a>defaultInstallScope

**Необязательный** — строка

Указывает область установки, определяемую для этого приложения по умолчанию. Определенным областью будет параметр, отображаемый на кнопке при добавлении приложения пользователем. Доступные варианты:
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**Необязательный** — объект

Когда будет выбрана область установки группы, она определит возможности по умолчанию при установке приложения пользователем. Доступные варианты:
* `team`
* `groupchat`
* `meetings`
 
|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`team`|string|||Если выбрана область установки, это поле указывает доступные возможности `team` по умолчанию. Параметры: `tab` `bot` , или `connector` .|
|`groupchat`|строка|||Если выбрана область установки, это поле указывает доступные возможности `groupchat` по умолчанию. Параметры: `tab` `bot` , или `connector` .|
|`meetings`|строка|||Если выбрана область установки, это поле указывает доступные возможности `meetings` по умолчанию. Параметры: `tab` `bot` , или `connector` .|
