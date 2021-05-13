---
title: Справка о схеме манифеста
description: Описывает схему манифеста для Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: Схема манифеста команд
ms.openlocfilehash: c0b8b6f5baa163d2292227f7d361b6d12849edec
ms.sourcegitcommit: 3475927e1c7964dc25c363d0d2026e5c898c97c7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2021
ms.locfileid: "52336519"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Справка: схема манифеста для Microsoft Teams

Манифест Teams описывает, как приложение интегрируется в Microsoft Teams продукт. Манифест должен соответствовать схеме, которая была на [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) уровне . Поддерживаются и предыдущие версии 1.0, 1.1,..., 1.6 и так далее (с помощью "v1.x" в URL-адресе).

В следующем примере схемы показаны все варианты раздвивемости.

## <a name="sample-full-manifest"></a>Образец полного манифеста

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json",
  "manifestVersion": "1.10",
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
          "description": "Command Description; e.g., Search for a customer",
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
        }
      ],
      "taskInfo": {
        "title": "Initial dialog title",
        "width": "Dialog width",
        "height": "Dialog height",
        "url": "Initial webview URL"
      },
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
    ],
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
     "websiteUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ]              
}
```

Схема определяет следующие свойства:

## <a name="schema"></a>$schema

Необязательный, но рекомендуемый — строка

URL https:// ссылки на схему JSON для манифеста.

## <a name="manifestversion"></a>manifestVersion

**Обязательно —** строка

Версия схемы манифеста, используемая этим манифестом. Должно быть 1.10.

## <a name="version"></a>version

**Обязательно —** строка

Версия определенного приложения. Если вы что-то обновите в манифесте, версия также должна быть приумножная. Таким образом, при установке нового манифеста он переописает существующий и пользователь получает новые функции. Если это приложение было отправлено в магазин, новый манифест должен быть повторно отправлен и повторно проверен. Пользователи приложения получают новый обновленный манифест автоматически в течение нескольких часов после утверждения манифеста.

Если приложение запрашивает разрешения на изменение, пользователям будет предложено обновить и повторно согласиться на приложение.

Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. MINOR. PATCH).

## <a name="id"></a>id

**Обязательно —** ID приложения Майкрософт

Идентификатор — уникальный идентификатор, созданный Корпорацией Майкрософт для приложения. У вас есть ID, если бот зарегистрирован через Microsoft Bot Framework или веб-приложение вкладки уже вошел в Microsoft. Здесь необходимо ввести ID. В противном случае необходимо создать новый ID на портале [регистрации приложений Майкрософт.](https://aka.ms/appregistrations) При добавлении бота используйте тот же ID.

> [!NOTE]
> Если вы передаете обновление существующему приложению в AppSource, ID в манифесте не должен изменяться.

## <a name="developer"></a>developer

**Обязательно —** объект

Указывает сведения о вашей компании. Для приложений, представленных в Teams магазине, эти значения должны соответствовать сведениям в списке магазина. Дополнительные сведения см. [в Teams руководства по публикации в магазине.](~/concepts/deploy-and-publish/appsource/publish.md)

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`name`|32 символа|✔|Имя отображения для разработчика.|
|`websiteUrl`|2048 символов|✔|Url https:// url-адрес веб-сайта разработчика. Эта ссылка должна принимать пользователей на страницу вашей компании или конкретного продукта.|
|`privacyUrl`|2048 символов|✔|Url https:// url-адрес политики конфиденциальности разработчика.|
|`termsOfUseUrl`|2048 символов|✔|Url https:// url-адрес для условий использования разработчика.|
|`mpnId`|10 символов| |**Необязательный** Идентификатор Сети партнеров Майкрософт, который определяет организацию-партнер, которая строит приложение.|

## <a name="name"></a>name

**Обязательно —** объект

Имя приложения, отображаемого пользователям в Teams. Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource. Значения и `short` должны `full` быть разными.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|30 символов|✔|Короткое имя отображения приложения.|
|`full`|100 символов||Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.|

## <a name="description"></a>description

**Обязательно —** объект

Описывает приложение для пользователей. Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.

Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, чтобы помочь потенциальным клиентам понять, что делает ваш опыт. В полном описании необходимо учтите, что для использования требуется внешняя учетная запись. Значения и `short` должны `full` быть разными. Короткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|80 символов|✔|Краткое описание работы приложения, используемого при ограниченном пространстве.|
|`full`|4000 символов|✔|Полное описание приложения.|

## <a name="packagename"></a>packageName

**Необязательный** — строка

Уникальный идентификатор для приложения в обратной нотации домена; например, com.example.myapp. Максимальная длина: 64 символа.

## <a name="localizationinfo"></a>локализацияInfo

**Необязательный** — объект

Позволяет спецификацию языка по умолчанию, а также указатели для дополнительных языковых файлов. См. [локализацию.](~/concepts/build-and-test/apps-localization.md)

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

**Обязательно —** объект

Значки, используемые в Teams приложении. Файлы значков должны быть включены в пакет отправки. Дополнительные сведения см. в [значках.](../../concepts/build-and-test/apps-package.md#app-icons)

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`outline`|32 x 32 пикселя|✔|Относительный путь к прозрачному значку контура PNG 32x32.|
|`color`|192 x 192 пикселя|✔|Относительный путь к значку PNG полного цвета 192x192.|

## <a name="accentcolor"></a>accentColor

**Необязательный** — цветовой код HTML Hex

Цвет, который можно использовать в сочетании с и в качестве фона для значков контура.

Значение должно быть допустимым цветовым кодом HTML, начиная, например, с `#4464ee` "#".

## <a name="configurabletabs"></a>configurableTabs

**Необязательный** — массив

Используется, когда в вашем приложении есть опыт работы с вкладками канала команды, которая требует дополнительной конфигурации перед ее добавлением. Настраиваемые вкладки поддерживаются только в области команд, и вы можете настроить те же вкладки несколько раз. Однако определить его в манифесте можно только один раз.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|string|2048 символов|✔|URL-https://, который можно использовать при настройке вкладки.|
|`scopes`|массив enums|1|✔|В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области. |
|`canUpdateConfiguration`|boolean|||Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания. По умолчанию: **true**.|
|`context` |массив enums|6 ||Набор `contextItem` областей, в которых [вкладка поддерживается.](../../tabs/how-to/access-teams-context.md) По умолчанию: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|Строка|2048||Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint. Размер 1024x768. |
|`supportedSharePointHosts`|массив enums|1||Определяет, как вкладка доступна в SharePoint. Параметры `sharePointFullPage` и `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Необязательный** — массив

Определяет набор вкладок, которые можно "прикрепить" по умолчанию, не добавляя их вручную. Статические вкладки, объявленные в области, всегда прикрепяются к личному опыту `personal` приложения. Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.

Этот элемент — массив (не более 16 элементов) со всеми элементами `object` типа. Этот блок требуется только для решений, которые предоставляют статическое решение вкладки.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`entityId`|string|64 символа|✔|Уникальный идентификатор для объекта, отображаемого на вкладке.|
|`name`|Строка|128 символов|✔|Отображение имени вкладки в интерфейсе канала.|
|`contentUrl`|Строка||✔|URL https://, который указывает на пользовательский интерфейс объекта, отображаемого на Teams холсте.|
|`websiteUrl`|Строка|||Url https://, чтобы указать, выбирает ли пользователь просмотр в браузере.|
|`searchUrl`|Строка|||Url https://, на который нужно указать для поисковых запросов пользователя.|
|`scopes`|массив enums|1|✔|В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в `personal` рамках личного опыта.|
|`context` | массив enums| 2|| Набор `contextItem` областей, в которых поддерживается вкладка.|

> [!NOTE]
>  Функция searchUrl недоступна сторонним разработчикам.
> Если для отображения соответствующего контента или инициации потока проверки подлинности на вкладке Get context для Microsoft Teams вкладки  [требуются сведения, зависящие от контекста.](../../tabs/how-to/access-teams-context.md)

## <a name="bots"></a>боты

**Необязательный** — массив

Определяет решение бота, а также необязательные сведения, такие как свойства команд по умолчанию.

Элемент — массив (максимум 1 элемент в настоящее время разрешен только для одного бота в приложении) со всеми элементами &mdash; типа `object` . Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|string|64 символа|✔|Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework. Это вполне может быть таким же, как общий [ID приложения](#id).|
|`scopes`|массив enums|3|✔|Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`). Эти параметры не являются исключающими.|
|`needsChannelSelector`|boolean|||Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал. По умолчанию: **`false`**|
|`isNotificationOnly`|boolean|||Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы. По умолчанию: **`false`**|
|`supportsFiles`|boolean|||Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате. По умолчанию: **`false`**|
|`supportsCalling`|boolean|||Значение, указывающее, где бот поддерживает звуковые вызовы. **ВАЖНО.** Это свойство в настоящее время является экспериментальным. Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.  Она предоставляется только для тестирования и разведки и не должна использоваться в производственных приложениях. По умолчанию: **`false`**|
|`supportsVideo`|boolean|||Значение, указывающее, где бот поддерживает видеозвонков. **ВАЖНО.** Это свойство в настоящее время является экспериментальным. Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.  Она предоставляется только для тестирования и разведки и не должна использоваться в производственных приложениях. По умолчанию: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Необязательный список команд, которые бот может рекомендовать пользователям. Объект — массив (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом. Дополнительные [сведения см. в](~/bots/how-to/create-a-bot-commands-menu.md) меню Bot.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`items.scopes`|массив enums|3|✔|Указывает область, для которой действует список команд. Возможны значения `team`, `personal` и `groupchat`.|
|`items.commands`|массив объектов|10 |✔|Массив команд, поддерживаемых ботом:<br>`title`: имя команды бота (строка, 32)<br>`description`: простое описание или пример синтаксиса команды и ее аргумента (строка, 128)|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|title|string|12 |✔|Имя команды бота|
|description|string|128 символов|✔|Простое текстовое описание или пример синтаксиса команд и его аргументов.|

## <a name="connectors"></a>соединители

**Необязательный** — массив

Блок `connectors` определяет Office 365 соединители для приложения.

Объект — массив (максимум 1 элемент) со всеми элементами `object` типа. Этот блок необходим только для решений, которые предоставляют соединители.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|string|2048 символов|✔|URL https://, который необходимо использовать при настройке соединителя.|
|`scopes`|массив enums|1|✔|Указывает, предоставляет ли соединители опыт в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ). В настоящее время `team` поддерживается только область.|
|`connectorId`|Строка|64 символа|✔|Уникальный идентификатор соединитетеля, который соответствует его идентификатору в панели мониторинга разработчиков [соединителок.](https://aka.ms/connectorsdashboard)|

## <a name="composeextensions"></a>composeExtensions

**Необязательный** — массив

Определяет расширение обмена сообщениями для приложения.

> [!NOTE]
> В ноябре 2017 г. имя функции было изменено с "расширение составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжили функционировать.

Элемент — массив (максимум 1 элемент) со всеми элементами `object` типа. Этот блок необходим только для решений, которые предоставляют расширение обмена сообщениями.

|Имя| Тип | Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|string|64|✔|Уникальный ID приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрирован в Bot Framework. Это вполне может быть таким же, как и общий ID приложения.|
|`commands`|массив объектов|10 |✔|Массив команд, поддерживаемых расширением обмена сообщениями|
|`canUpdateConfiguration`|boolean|||Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями. По умолчанию: **false**.|
|`messageHandlers`|массив объектов|5 ||Список обработчиков, которые позволяют вызывать приложения при определенных условиях.|
|`messageHandlers.type`|Строка|||Тип обработка сообщений. Должно быть задано значение `"link"`.|
|`messageHandlers.value.domains`|массив строк|||Массив доменов, для которые обработник сообщений ссылок может зарегистрироваться.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Расширение обмена сообщениями должно объявить одну или несколько команд. Каждая команда отображается Microsoft Teams как потенциальное взаимодействие с точки входа на основе пользовательского интерфейса. Существует не более 10 команд.

Каждый элемент команды — это объект со следующей структурой:

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|string|64 символа|✔|ID для команды.|
|`title`|Строка|32 символа|✔|Удобное имя команды.|
|`type`|Строка|64 символа||Тип команды. Один `query` из или `action` . По умолчанию: **запрос**.|
|`description`|Строка|128 символов||В описании, которое отображается пользователями, указывается назначение этой команды.|
|`initialRun`|boolean|||Значение boolean указывает, выполняется ли команда изначально без параметров. Значение по умолчанию: **false**.|
|`context`|массив строк|3||Определяет, из чего можно вызвать расширение сообщения. Любое сочетание `compose` `commandBox` , `message` . Значение по умолчанию: `["compose","commandBox"]`.|
|`fetchTask`|boolean|||Значение boolean, которое указывает, должен ли он динамически получать модуль задач. Значение по умолчанию: **false**.|
|`taskInfo`|объект|||Укажите модуль задач для предварительной загрузки при использовании команды расширения обмена сообщениями.|
|`taskInfo.title`|Строка|64 символа||Начальное название диалогов.|
|`taskInfo.width`|Строка|||Ширина диалогов — число в пикселях или макет по умолчанию, такие как "большой", "средний" или "маленький".|
|`taskInfo.height`|Строка|||Высота диалогов — число пикселей или макет по умолчанию, например "большой", "средний" или "маленький".|
|`taskInfo.url`|Строка|||Начальный URL-адрес веб-просмотров.|
|`parameters`|массив объекта|5 элементов|✔|Список параметров, которые принимает команда. Минимум: 1; максимум: 5.|
|`parameters.name`|Строка|64 символа|✔|Имя параметра, как оно отображается в клиенте. Это включено в запрос пользователя.|
|`parameters.title`|Строка|32 символа|✔|Удобное название для параметра.|
|`parameters.description`|Строка|128 символов||Удобное для пользователя строка, описываемая назначение этого параметра.|
|`parameters.value`|Строка|512 символов||Начальное значение для параметра.|
|`parameters.inputType`|Строка|128 символов||Определяет тип управления, отображаемого в модуле задач `fetchTask: true` для . Один из `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|массив объектов|10 элементов||Параметры выбора `choiceset` для . Используйте только `parameter.inputType` тогда, когда `choiceset` это .|
|`parameters.choices.title`|Строка|128 символов|✔|Название выбора.|
|`parameters.choices.value`|Строка|512 символов|✔|Значение выбора.|

## <a name="permissions"></a>permissions

**Необязательный** — массив строк

Массив, в котором указывается, какие разрешения запрашивает приложение, что позволяет конечным пользователям `string` знать, как выполняется расширение. Следующие параметры не являются эксклюзивными:

* `identity`&emsp;Требует сведений о удостоверениях пользователей
* `messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам группы

Изменение этих разрешений во время обновления приложения заставляет пользователей повторять процесс согласия после запуска обновленного приложения. Дополнительные [сведения см. в обновлении](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) приложения.

## <a name="devicepermissions"></a>devicePermissions

**Необязательный** — массив строк

Предоставляет родных функций на устройстве пользователя, к которое ваше приложение запрашивает доступ. Доступные варианты:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Необязательный,** за **исключением обязательного,** где отмечено

Список допустимого домена для веб-сайтов, которые приложение ожидает загрузить в Teams клиента. Списки домена могут включать, например, поддиайки. `*.example.com` Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` . Если конфигурации вкладок или пользовательскому интерфейсу контента необходимо перейти к любому другому домену, кроме одного использования для конфигурации вкладок, этот домен должен быть указан здесь.

Не обязательно **включать** в приложение домены поставщиков удостоверений, которые необходимо поддерживать. Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить accounts.google.com, однако не следует включать accounts.google.com `validDomains[]` в .

Teams приложения, которые требуют нормальной работы собственных URL-адресов sharepoint, включают в допустимый список доменов "{teamsitedomain}".

> [!IMPORTANT]
> Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью подкрентов. Например, `yourapp.onmicrosoft.com` допустимо, однако, `*.onmicrosoft.com` не является допустимым.

Объект — массив со всеми элементами `string` типа.

## <a name="webapplicationinfo"></a>webApplicationInfo

**Необязательный** — объект

Предопишите Azure Active Directory (AAD) App ID и microsoft Graph, чтобы помочь пользователям без проблем войти в ваше приложение. Если ваше приложение зарегистрировано в AAD, необходимо предоставить ID приложения, чтобы администраторы могли легко просмотреть разрешения и предоставить согласие Teams центре администрирования.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|string|36 символов|✔|AAD-id приложения приложения. Этот id должен быть GUID.|
|`resource`|Строка|2048 символов|✔|URL-адрес ресурса приложения для приобретения маркера auth для SSO. </br> **ПРИМЕЧАНИЕ:** Если вы не используете SSO, убедитесь, что вы вводите значение строки в этом поле в манифест приложения, например, чтобы избежать ответа https://notapplicable на ошибку. |
|`applicationPermissions`|массив строк|128 символов||Укажите [конкретное согласие конкретного ресурса.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Необязательный** — boolean

Указывает, следует ли показывать индикатор загрузки при загрузке приложения или вкладки. Значение по умолчанию: **false**.
>[!NOTE]
>Если в манифесте приложения выбрано как верное, чтобы правильно загрузить страницу, измените страницы контента вкладок и модулей задач, как описано в документе Показать документ индикатора `showLoadingIndicator` загрузки. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)


## <a name="isfullscreen"></a>isFullScreen

 **Необязательный** — boolean

Указать, где отрисовка личного приложения с панели заголовки вкладок или без нее. Значение по умолчанию: **false**.

## <a name="activities"></a>activities

**Необязательный** — объект

Определите свойства, которые приложение использует для публикации ленты действий пользователя.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`activityTypes`|массив объектов|128 элементов| | Укапитайте типы действий, которые ваше приложение может размещать в канале действий пользователей.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`type`|string|32 символа|✔|Тип уведомления. *См. ниже*.|
|`description`|Строка|128 символов|✔|Краткое описание уведомления. *См. ниже*.|
|`templateText`|Строка|128 символов|✔|Ex: "{actor} создал задачу {taskId} для вас"|

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
|`groupchat`|Строка|||Если выбрана область установки, это поле указывает доступные возможности `groupchat` по умолчанию. Параметры: `tab` `bot` , или `connector` .|
|`meetings`|Строка|||Если выбрана область установки, это поле указывает доступные возможности `meetings` по умолчанию. Параметры: `tab` `bot` , или `connector` .|

## <a name="configurableproperties"></a>configurableProperties

**Необязательный** - массив

Блок определяет свойства приложений, которые может `configurableProperties` Teams администратор. Дополнительные сведения см. [в Microsoft Teams.](/MicrosoftTeams/customize-apps)

> [!NOTE]
> Необходимо определить как минимум одно свойство. В этом блоке можно определить максимум девять свойств.
> В качестве наилучшей практики необходимо предоставить рекомендации по настройке для пользователей и клиентов приложений, которые следует соблюдать при настройке приложения.

Можно определить любое из следующих свойств:
* `name`: Позволяет администратору изменять имя отображения приложения.
* `shortDescription`: Позволяет администратору изменить краткое описание приложения.
* `longDescription`: Позволяет администратору изменять подробное описание приложения.
* `smallImageUrl`. Это `outline` свойство в `icons` блоке манифеста.
* `largeImageUrl`. Это `color` свойство в `icons` блоке манифеста.
* `accentColor`. Это цвет, который можно использовать в сочетании с и в качестве фона для значков плана.
* `websiteUrl`. Это https:// URL-адрес веб-сайта разработчика.
* `privacyUrl`. Это https:// url-адрес политики конфиденциальности разработчика.
* `termsOfUseUrl`. Это https:// URL-адрес для условий использования разработчика.


