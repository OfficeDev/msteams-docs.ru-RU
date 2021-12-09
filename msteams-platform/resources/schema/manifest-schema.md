---
title: Справка о схеме манифеста
description: Описывает схему манифеста для Microsoft Teams
ms.topic: reference
ms.author: lajanuar
ms.localizationpriority: medium
keywords: Схема манифеста команд
ms.openlocfilehash: 7847aa123687605a94cb2c83819b1ef8b67f8b65
ms.sourcegitcommit: 0aa50ade5a044385eceff5e6b62333a78a1f8968
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2021
ms.locfileid: "61392374"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Справка: схема манифеста для Microsoft Teams

Манифест Teams описывает, как приложение интегрируется в Microsoft Teams продукт. Манифест должен соответствовать схеме, которая была на [`https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json) уровне . Поддерживаются также предыдущие версии 1.0, 1.1,..., и 1.11 (с помощью "v1.x" в URL-адресе).
Дополнительные сведения об изменениях, внесенных в каждой версии, см. в [журнале изменений манифеста.](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)

В следующем примере схемы показаны все параметры экстензивности:

## <a name="sample-full-manifest"></a>Образец полного манифеста

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
  "manifestVersion": "1.11",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters (<=100 chars)"
  },
  "description": {
    "short": "Short description of your app (<= 80 chars)",
    "full": "Full description of your app (<= 4000 chars)"
  },
  "icons": {
    "outline": "A relative path to a transparent .png icon — 32px X 32px",
    "color": "A relative path to a full color .png icon — 192px X 192px"
  },
  "accentColor": "A valid HTML color code.",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "scopes": [
        "team",
        "groupchat"
      ],
      "canUpdateConfiguration": true,
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
      ],
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": [
         "sharePointFullPage",
         "sharePointWebPart"
      ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "context":[
        "personalTab",
        "channelTab"
        ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser)",
       "searchUrl":  "https://contoso.com/content (displayed in web browser)"
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "scopes": [
        "team",
        "personal",
        "groupchat"
      ],
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "supportsFiles": true,
      "supportsCalling": false,
      "supportsVideo": true,
      "commandLists": [
        {
          "scopes": [
            "team",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command 2",
              "description": "Description of Command 2"
            }
          ]
        },
        {
          "scopes": [
            "personal",
            "groupchat"
          ],
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
      "scopes": [
        "team"
      ],
      "configurationUrl": "https://contoso.com/teamsconnector/configure"
    }
  ],
  "composeExtensions": [
    {
      "canUpdateConfiguration": true,
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "type": "query",
          "context": [
            "compose",
            "commandBox"
          ],
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "fetchTask": false,
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "inputType": "text",
              "description": "Enter the keywords to search for",
              "value": "Initial value for the parameter",
              "choices": [
                {
                  "title": "Title of the choice",
                  "value": "Value of the choice"
                }
              ]
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "type": "action",
          "context": [
            "message"
          ],
          "description": "Command Description; e.g., Add a customer",
          "initialRun": true,
          "fetchTask": true,
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType": "text"
            }
          ]
        },
         {
          "id": "exampleCmd3",
          "title": "Example Command 3",
          "type": "action",
          "context": [
            "compose",
            "commandBox",
            "message"
          ],
          "description": "Command Description; e.g., Add a customer",
          "fetchTask": false,
          "taskInfo": {
            "title": "Initial dialog title",
            "width": "Dialog width",
            "height": "Dialog height",
            "url": "Initial webview URL"
          }
        }
      ],
      "messageHandlers": [
        {
          "type": "link",
          "value": {
            "domains": [
              "mysite.someplace.com",
              "othersite.someplace.com"
            ]
          }
        }
      ]
    }
  ],
"permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "devicePermissions": [
    "geolocation",
    "media",
    "notifications",
    "midi",
    "openExternal"
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
    ]
  },
  "showLoadingIndicator": false,
  "isFullScreen": false,
  "activities": {
    "activityTypes": [
      {
        "type": "taskCreated",
        "description": "Task created activity",
        "templateText": "<team member> created task <taskId> for you"
      },
      {
        "type": "userMention",
        "description": "Personal mention activity",
        "templateText": "<team member> mentioned you"
      }
    ]
  },
  "defaultBlockUntilAdminAction": true,
  "publisherDocsUrl": "https://website.com/app-info",
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
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
  "subscriptionOffer": {
    "offerId": "publisherId.offerId"
  }
}
```

Схема определяет следующие свойства:

## <a name="schema"></a>$schema

Необязательный, но рекомендуемый строка

URL https:// ссылки на схему JSON для манифеста.

## <a name="manifestversion"></a>manifestVersion

**Обязательно —строка**

Версия схемы манифеста, используемая этим манифестом. Должно быть 1.10.

## <a name="version"></a>version

**Обязательно —строка**

Версия определенного приложения. При обновлении чего-либо в манифесте необходимо также приумношать версию. Таким образом, при установке нового манифеста он переописает существующий и пользователь получает новые функции. Когда это приложение было отправлено в магазин, новый манифест должен быть повторно отправлен и переоценен. Пользователи приложения получают новый обновленный манифест автоматически в течение нескольких часов после утверждения манифеста.

Если приложение запрашивает разрешения на изменение, пользователям будет предложено обновить и повторно перейти к приложению.

Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. MINOR. PATCH).

## <a name="id"></a>id

**Required**—Microsoft app ID

Идентификатор — уникальный идентификатор, созданный Корпорацией Майкрософт для приложения. У вас есть ID, если бот зарегистрирован через Microsoft Bot Framework. У вас есть ID, если веб-приложение вкладки уже впишется в Microsoft. Здесь необходимо ввести ID. В противном случае необходимо создать новый ID на портале [регистрации приложений Майкрософт.](https://aka.ms/appregistrations) При добавлении бота используйте тот же ID.

> [!NOTE]
> Если вы передаете обновление существующему приложению в AppSource, ID в манифесте не должен изменяться.

## <a name="developer"></a>developer

**Required**—object

Указывает сведения о вашей компании. Для приложений, представленных в Teams магазине, эти значения должны соответствовать сведениям в списке магазина. Дополнительные сведения см. [в Teams руководства по публикации в магазине.](~/concepts/deploy-and-publish/appsource/publish.md)

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`name`|32 символа|✔|Имя отображения для разработчика.|
|`websiteUrl`|2048 символов|✔|Url https:// url-адрес веб-сайта разработчика. Эта ссылка должна принимать пользователей на страницу вашей компании или конкретного продукта.|
|`privacyUrl`|2048 символов|✔|Url https:// url-адрес политики конфиденциальности разработчика.|
|`termsOfUseUrl`|2048 символов|✔|Url https:// url-адрес для условий использования разработчика.|
|`mpnId`|10 символов| |**Необязательный** Идентификатор Сети партнеров Майкрософт, который определяет организацию-партнер, которая строит приложение.|

## <a name="name"></a>name

**Required**—object

Имя приложения, отображаемого пользователям в Teams. Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource. Значения и `short` должны `full` быть разными.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|30 символов|✔|Короткое имя отображения приложения.|
|`full`|100 символов||Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.|

## <a name="description"></a>description

**Required**—object

Описывает приложение для пользователей. Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.

Убедитесь, что ваше описание описывает ваш опыт и помогает потенциальным клиентам понять, что делает ваш опыт. В полном описании необходимо учтите, что для использования требуется внешняя учетная запись. Значения и `short` должны `full` быть разными. Ваше краткое описание не может повторяться в длинном описании и не должно включать любое другое имя приложения.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|80 символов|✔|Краткое описание работы приложения, используемого при ограниченном пространстве.|
|`full`|4000 символов|✔|Полное описание приложения.|

## <a name="packagename"></a>packageName

**Необязательный**— строка

Уникальный идентификатор для приложения в обратной нотации домена; например, com.example.myapp. Максимальная длина: 64 символа.

## <a name="localizationinfo"></a>локализацияInfo

**Необязательный**— объект

Позволяет спецификацию языка по умолчанию и предоставляет указатели для большего количество языковых файлов. Дополнительные сведения см. в [деле локализации.](~/concepts/build-and-test/apps-localization.md)

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`defaultLanguageTag`||✔|Языковой тег строк в этом файле манифеста верхнего уровня.|

### <a name="localizationinfoadditionallanguages"></a>локализацияInfo.additionalLanguages

Массив объектов, указывающих дополнительные языковые переводы.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`languageTag`||✔|Языковой тег строки в предоставленного файла.|
|`file`||✔|Относительный путь к файлу .json, содержащим переведенные строки.|

## <a name="icons"></a>icons

**Required**—object

Значки, используемые в Teams приложении. Файлы значков должны быть включены в пакет отправки. Дополнительные сведения см. в [книге Icons](../../concepts/build-and-test/apps-package.md#app-icons).

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`outline`|32 x 32 пикселя|✔|Относительный путь к прозрачному значку контура PNG 32x32.|
|`color`|192 x 192 пикселя|✔|Относительный путь к значку PNG полного цвета 192x192.|

## <a name="accentcolor"></a>accentColor

**Необходимый** цветовой код HTML Hex

Цвет, который нужно использовать и в качестве фона для значков контура.

Значение должно быть допустимым цветовым кодом HTML, начиная, например, с `#4464ee` "#".

## <a name="configurabletabs"></a>configurableTabs

**Необязательный**— массив

Используется, когда в вашем приложении есть опыт работы с вкладками канала команды, которая требует дополнительной конфигурации перед ее добавлением. Настраиваемые вкладки поддерживаются только в области и области, и вы можете настроить те же `team` `groupchat` вкладки несколько раз. Однако определить его в манифесте можно только один раз.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|string|2048 символов|✔|URL-https://, который можно использовать при настройке вкладки.|
|`scopes`|массив enums|1|✔|В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области. |
|`canUpdateConfiguration`|boolean|||Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания. По умолчанию: **true**.|
|`context` |массив enums|6 ||Набор `contextItem` областей, в которых [вкладка поддерживается.](../../tabs/how-to/access-teams-context.md) По умолчанию: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|String|2048||Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint. Размер 1024x768. |
|`supportedSharePointHosts`|массив enums|1||Определяет, как вкладка доступна в SharePoint. Параметры `sharePointFullPage` и `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Необязательный**— массив

Определяет набор вкладок, которые можно "прикрепить" по умолчанию, не добавляя их вручную. Статические вкладки, объявленные в области, всегда прикрепяются к личному опыту `personal` приложения. Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.

Этот элемент — массив (не более 16 элементов) со всеми элементами `object` типа. Этот блок требуется только для решений, которые предоставляют статическое решение вкладки.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`entityId`|string|64 символа|✔|Уникальный идентификатор для объекта, отображаемого на вкладке.|
|`name`|String|128 символов|✔|Отображение имени вкладки в интерфейсе канала.|
|`contentUrl`|String||✔|URL https://, который указывает на пользовательский интерфейс объекта, отображаемого на Teams холсте.|
|`websiteUrl`|String|||Url https://, чтобы указать, выбирает ли пользователь просмотр в браузере.|
|`searchUrl`|String|||Url https://, на который нужно указать для поисковых запросов пользователя.|
|`scopes`|массив enums|1|✔|В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в `personal` рамках личного опыта.|
|`context` | массив enums| 2|| Набор `contextItem` областей, в которых поддерживается вкладка.|

> [!NOTE]
>  Функция searchUrl недоступна сторонним разработчикам.
> Если для отображения соответствующего контента или для инициации потока проверки подлинности в вкладке Get context для вашей вкладки Microsoft Teams контексте, дополнительные сведения см. в статье Get context for [your Microsoft Teams.](../../tabs/how-to/access-teams-context.md)

## <a name="bots"></a>боты

**Необязательный**— массив

Определяет решение бота, а также необязательные сведения, такие как свойства команд по умолчанию.

Элемент — массив (в настоящее время допускается только один элемент для каждого приложения) со всеми элементами &mdash; `object` типа. Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|string|64 символа|✔|Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework. ID может быть таким же, как и общий [ID приложения](#id).|
|`scopes`|массив enums|3|✔|Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`). Эти параметры не являются исключающими.|
|`needsChannelSelector`|boolean|||Описывает, использует ли бот подсказку пользователя для добавления бота в определенный канал. По умолчанию: **`false`**|
|`isNotificationOnly`|boolean|||Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы. По умолчанию: **`false`**|
|`supportsFiles`|boolean|||Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате. По умолчанию: **`false`**|
|`supportsCalling`|boolean|||Значение, указывающее, где бот поддерживает звуковые вызовы. **ВАЖНО.** Это свойство в настоящее время является экспериментальным. Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.  Свойство предоставляется только для тестирования и разведки и не должно использоваться в производственных приложениях. По умолчанию: **`false`**|
|`supportsVideo`|boolean|||Значение, указывающее, где бот поддерживает видеозвонков. **ВАЖНО.** Это свойство в настоящее время является экспериментальным. Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.  Свойство предоставляется только для тестирования и разведки и не должно использоваться в производственных приложениях. По умолчанию: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Необязательный список команд, которые бот может рекомендовать пользователям. Объект — массив (не более двух элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом. Дополнительные сведения см. [в меню Bot.](~/bots/how-to/create-a-bot-commands-menu.md)

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`items.scopes`|массив enums|3|✔|Указывает область, для которой действует список команд. Возможны значения `team`, `personal` и `groupchat`.|
|`items.commands`|массив объектов|10 |✔|Массив команд, поддерживаемых ботом:<br>`title`: имя команды бота (строка, 32)<br>`description`: простое описание или пример синтаксиса команды и его аргумента (строка, 128).|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|title|string|12 |✔|Имя команды бота.|
|description|string|128 символов|✔|Простое текстовое описание или пример синтаксиса команд и его аргументов.|

## <a name="connectors"></a>соединители

**Необязательный**— массив

Блок `connectors` определяет Office 365 соединители для приложения.

Объект — массив (максимум один элемент) со всеми элементами `object` типа. Этот блок необходим только для решений, которые предоставляют соединители.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|string|2048 символов|✔|URL https://, который необходимо использовать при настройке соединителя.|
|`scopes`|массив enums|1|✔|Указывает, предоставляет ли соединители опыт в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ). В настоящее время `team` поддерживается только область.|
|`connectorId`|String|64 символа|✔|Уникальный идентификатор соединитетеля, который соответствует его идентификатору в панели мониторинга разработчиков [соединителок.](https://aka.ms/connectorsdashboard)|

## <a name="composeextensions"></a>composeExtensions

**Необязательный**— массив

Определяет расширение обмена сообщениями для приложения.

> [!NOTE]
> В ноябре 2017 г. имя функции было изменено с "расширение составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжили функционировать.

Элемент — массив (максимум один элемент) со всеми элементами `object` типа. Этот блок необходим только для решений, которые предоставляют расширение обмена сообщениями.

|Имя| Тип | Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|string|64|✔|Уникальный ID приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрирован в Bot Framework. ID может быть таким же, как и общий ID приложения.|
|`commands`|массив объектов|10 |✔|Массив команд, поддерживаемых расширением обмена сообщениями.|
|`canUpdateConfiguration`|boolean|||Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями. По умолчанию: **false**.|
|`messageHandlers`|массив объектов|5||Список обработчиков, которые позволяют вызывать приложения при определенных условиях.|
|`messageHandlers.type`|String|||Тип обработка сообщений. Должно быть задано значение `"link"`.|
|`messageHandlers.value.domains`|массив строк|||Массив доменов, для которые обработник сообщений ссылок может зарегистрироваться.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Расширение обмена сообщениями должно объявить одну или несколько команд с максимум 10 командами. Каждая команда отображается Microsoft Teams как потенциальное взаимодействие с точки входа на основе пользовательского интерфейса.

Каждый элемент команды — это объект со следующей структурой:

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|string|64 символа|✔|ID для команды.|
|`title`|String|32 символа|✔|Удобное имя команды.|
|`type`|String|64 символа||Тип команды. Один `query` из или `action` . По умолчанию: **запрос**.|
|`description`|String|128 символов||В описании, которое отображается пользователями, указывается назначение этой команды.|
|`initialRun`|boolean|||Значение boolean указывает, выполняется ли команда изначально без параметров. Значение по умолчанию: **false**.|
|`context`|массив строк|3||Определяет, из чего можно вызвать расширение сообщения. Любое сочетание `compose` `commandBox` , `message` . Значение по умолчанию: `["compose","commandBox"]`.|
|`fetchTask`|boolean|||Значение boolean, которое указывает, должен ли он динамически получать модуль задач. Значение по умолчанию: **false**.|
|`taskInfo`|объект|||Укажите модуль задач для предварительной загрузки при использовании команды расширения обмена сообщениями.|
|`taskInfo.title`|String|64 символа||Начальное название диалогов.|
|`taskInfo.width`|String|||Ширина диалогов — число в пикселях или макет по умолчанию, такие как "большой", "средний" или "маленький".|
|`taskInfo.height`|String|||Высота диалогов — число пикселей или макет по умолчанию, например "большой", "средний" или "маленький".|
|`taskInfo.url`|String|||Начальный URL-адрес веб-просмотров.|
|`parameters`|массив объекта|5 элементов|✔|Список параметров, которые принимает команда. Минимум: 1; максимум: 5.|
|`parameters.name`|String|64 символа|✔|Имя параметра, как оно отображается в клиенте. Имя параметра включено в запрос пользователя.|
|`parameters.title`|String|32 символа|✔|Удобное название для параметра.|
|`parameters.description`|String|128 символов||Удобное для пользователя строка, описываемая назначение этого параметра.|
|`parameters.value`|String|512 символов||Начальное значение для параметра. В настоящее время значение не поддерживается|
|`parameters.inputType`|String|128 символов||Определяет тип управления, отображаемого в модуле задач `fetchTask: true` для . Один из `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|массив объектов|10 элементов||Параметры выбора `choiceset` для . Используйте только `parameter.inputType` тогда, когда `choiceset` это .|
|`parameters.choices.title`|String|128 символов|✔|Название выбора.|
|`parameters.choices.value`|String|512 символов|✔|Значение выбора.|

## <a name="permissions"></a>permissions

**Необязательный**— массив строк

Массив, который указывает, какие разрешения запрашивает приложение, который позволяет конечным пользователям `string` знать, как это расширение. Следующие параметры не являются эксклюзивными:

* `identity`&emsp;Требуется информация о удостоверении пользователя.
* `messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам группы.

Изменение этих разрешений во время обновления приложения заставляет пользователей повторять процесс согласия после запуска обновленного приложения. Дополнительные сведения см. в [дополнительных сведениях об обновлении приложения.](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)

## <a name="devicepermissions"></a>devicePermissions

**Необязательный**— массив строк

Предоставляет родных функций на устройстве пользователя, к которое ваше приложение запрашивает доступ. Доступные варианты:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Необязательный,** **за исключением обязательного,** где отмечено.

Список допустимого домена для веб-сайтов, которые приложение ожидает загрузить в Teams клиента. Списки домена могут включать, например, поддиайки. `*.example.com` Допустимый домен соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` . Если конфигурация вкладки или пользовательский интерфейс контента перемещаются в любой другой домен, кроме конфигурации вкладок, этот домен должен быть указан здесь.

Не **включите** домены поставщиков удостоверений, которые необходимо поддерживать в приложении. Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить accounts.google.com, однако не следует включать accounts.google.com `validDomains[]` в .

Teams приложения, которые требуют SharePoint url-адресов для нормальной работы, включают в допустимый список доменов "{teamsitedomain}".

> [!IMPORTANT]
> Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью подкрентов. Например, `yourapp.onmicrosoft.com` допустимо, однако, `*.onmicrosoft.com` не является допустимым.

Объект — массив со всеми элементами `string` типа.

## <a name="webapplicationinfo"></a>webApplicationInfo

**Необязательный**— объект

Предопишите Azure Active Directory (AAD) ID приложения и microsoft Graph, чтобы помочь пользователям легко войти в ваше приложение. Если приложение зарегистрировано в AAD, необходимо предоставить ID приложения. Администраторы могут легко просмотреть разрешения и предоставить согласие в Teams центре администрирования.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|string|36 символов|✔|AAD ID приложения. Этот ID должен быть GUID.|
|`resource`|String|2048 символов|✔|URL-адрес ресурса приложения для приобретения маркера auth для SSO. </br> **ПРИМЕЧАНИЕ:** Если вы не используете SSO, убедитесь, что вы вводите значение строки в этом поле в манифест приложения, например, чтобы избежать ответа https://notapplicable на ошибку. |
|`applicationPermissions`|массив строк|128 символов||Укажите [конкретное согласие конкретного ресурса.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Необязательный**- boolean

Указывает, следует ли показывать индикатор загрузки при загрузке приложения или вкладки. Значение по умолчанию: **false**.
>[!NOTE]
>Если в манифесте приложения выбрано как верное, чтобы правильно загрузить страницу, измените страницы контента вкладок и модулей задач, как описано в документе Показать документ индикатора `showLoadingIndicator` загрузки. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)


## <a name="isfullscreen"></a>isFullScreen

 **Необязательный**- boolean

Указать, где отрисовка личного приложения с панели заголовки вкладок или без нее. Значение по умолчанию: **false**.

> [!NOTE]
> `isFullScreen`работает только с SharePoint вкладками и приложениями для хранения.

## <a name="activities"></a>activities

**Необязательный**— объект

Определите свойства, которые приложение использует для публикации ленты действий пользователя.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`activityTypes`|массив объектов|128 элементов| | Укапитайте типы действий, которые ваше приложение может размещать в канале действий пользователей.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`type`|string|32 символа|✔|Тип уведомления. *См. ниже*.|
|`description`|String|128 символов|✔|Краткое описание уведомления. *См. ниже*.|
|`templateText`|String|128 символов|✔|Ex: "{actor} создал задачу {taskId} для вас"|

```json
{
   "activities":{
      "activityTypes":[
         {
            "type":"taskCreated",
            "description":"Task Created Activity",
            "templateText":"{actor} created task {taskId} for you"
         },
         {
            "type":"teamMention",
            "description":"Team Mention Activity",
            "templateText":"{actor} mentioned team"
         },
         {
            "type":"channelMention",
            "description":"Channel Mention Activity",
            "templateText":"{actor} mentioned channel"
         },
         {
            "type":"userMention",
            "description":"Personal Mention Activity",
            "templateText":"{actor} mentioned user"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"creatorTaskCreated",
            "description":"Created Task Created",
            "templateText":"The Creator created task {taskId} for you"
         }
      ]
   }
}
```

***

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
|`groupchat`|String|||Если выбрана область установки, это поле указывает доступные возможности `groupchat` по умолчанию. Параметры: `tab` `bot` , или `connector` .|
|`meetings`|String|||Если выбрана область установки, это поле указывает доступные возможности `meetings` по умолчанию. Параметры: `tab` `bot` , или `connector` .|

## <a name="configurableproperties"></a>configurableProperties

**Необязательный** - массив

Блок определяет свойства приложений, которые могут `configurableProperties` Teams администраторы. Дополнительные сведения см. в [приложении Enable customization.](~/concepts/design/enable-app-customization.md) Функция настройки приложения не поддерживается в настраиваемых или LOB-приложениях.

> [!NOTE]
> Необходимо определить как минимум одно свойство. В этом блоке можно определить максимум девять свойств.

Можно определить любое из следующих свойств:

* `name`: Имя отображения приложения.
* `shortDescription`Краткое описание приложения.
* `longDescription`: Длинное описание приложения.
* `smallImageUrl`: Значок контура приложения.
* `largeImageUrl`: Значок цвета приложения.
* `accentColor`: Цвет для использования и фон для значков контура.
* `developerUrl`URL-адрес HTTPS веб-сайта разработчика.
* `privacyUrl`: URL-адрес HTTPS политики конфиденциальности разработчика.
* `termsOfUseUrl`: URL-адрес HTTPS условий использования разработчика.

## <a name="defaultblockuntiladminaction"></a>defaultBlockUntilAdminAction

**Необязательный**- boolean
 
Если свойство настроено на значение true, приложение скрыто от пользователей по умолчанию до тех пор, пока `defaultBlockUntilAdminAction` администратор не разрешит его. Если **задается true,** приложение скрыто для всех клиентов и конечных пользователей. Администраторы клиента могут видеть приложение в центре администрирования Teams и принимать меры, чтобы разрешить или заблокировать приложение. Значение по умолчанию — **false**. Дополнительные сведения о блоке приложений по умолчанию см. в [Teams, пока администратор не утвердит.](~/concepts/design/enable-app-customization.md#hide-teams-app-until-admin-approves)

## <a name="publisherdocsurl"></a>publisherDocsUrl

**Необязательный** — строка

**Максимальный размер** — 128 символов

URL-адрес HTTPS для информационной страницы для администраторов, чтобы получить рекомендации перед разрешением приложения, которое `publisherDocsUrl` заблокировано по умолчанию. Он также может использоваться для предоставления инструкций или сведений о приложении, которые могут быть полезны для администратора клиента.

## <a name="subscriptionoffer"></a>subscriptionOffer

**Необязательный** — объект

Указывает предложение SaaS, связанное с вашим приложением.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`offerId`| string | 2048 символов | ✔ | Уникальный идентификатор, который включает идентификатор Publisher и идентификатор предложения, которые можно найти в [Центре партнеров.](https://partner.microsoft.com/dashboard) Строку необходимо форматить как `publisherId.offerId` .|

## <a name="see-also"></a>См. также

* [Понимание структуры Microsoft Teams приложения](~/concepts/design/app-structure.md)
* [Разрешение настройки приложения](~/concepts/design/enable-app-customization.md)
* [Локализация приложения](~/concepts/build-and-test/apps-localization.md)
* [Интеграция возможностей мультимедиа](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Developer Preview схемы манифеста — Teams](~/resources/schema/manifest-schema-dev-preview.md)
