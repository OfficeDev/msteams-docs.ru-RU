---
title: Справочник по схеме манифеста
description: Описание схемы манифеста для Microsoft Teams
ms.topic: reference
keywords: Схема манифеста teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: 8fff56d229cc137df8356b06214893dc984396a0
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014609"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Справка: схема манифеста для Microsoft Teams

В манифесте Microsoft Teams описывается, как приложение интегрируется с продуктом Microsoft Teams. Манифест должен соответствовать схеме, которая есть в [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) . Поддерживаются также предыдущие версии 1.0-1.4 (с использованием "v1.x" в URL-адресе).

В следующем примере схемы показаны все параметры возможности для extensibility.

## <a name="sample-full-manifest"></a>Пример полного манифеста

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.8",
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
  }
}
```

Схема определяет следующие свойства:

## <a name="schema"></a>$schema

*Необязательный, но рекомендуемый —* строка

URL-https://, ссылающийся на схему JSON для манифеста.

## <a name="manifestversion"></a>manifestVersion

**Обязательно —** строка

Версия схемы манифеста, используемая этим манифестом. Это должно быть "1.7".

## <a name="version"></a>version

**Обязательно —** строка

Версия конкретного приложения. Если вы что-то обновляете в манифесте, необходимо также приращение версии. Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции. Если это приложение было отправлено в Магазин, новый манифест необходимо повторно представить и проверить повторно. Затем пользователи этого приложения получат новый обновленный манифест автоматически через несколько часов после его утверждения.

Если приложение запрашивает изменение разрешений, пользователям будет предложено обновить приложение и повторно согласиться на его использование.

Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR). MINOR. PATCH).

## <a name="id"></a>id

**Обязательное** — ИД приложения Майкрософт

Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения. Если вы зарегистрировали бота с помощью Microsoft Bot Framework или веб-приложение вашей вкладки уже входит в microsoft, у вас должен быть уже свой ИД, и он должен ввести здесь. В противном случае необходимо создать новый ИД на портале регистрации приложений Майкрософт[(Мои](https://apps.dev.microsoft.com)приложения), ввести его здесь, а затем повторно использовать при добавлении бота. Примечание. Если вы передаете обновление существующему приложению в AppSource, ИД манифеста не должен быть изменен.

## <a name="developer"></a>developer

**Required** — object

Указывает сведения о вашей компании. Для приложений, отправленных в AppSource (прежнее значение — Магазин Office), эти значения должны соответствовать сведениям в записи AppSource. Дополнительные [сведения см. в](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) наших рекомендациях по публикации.

|Name| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`name`|32 символа|✔|Отображаемая имя для разработчика.|
|`websiteUrl`|2048 символов|✔|Url https:// URL-адрес веб-сайта разработчика. По этой ссылке пользователи должны перенабираться на страницу вашей компании или конкретного продукта.|
|`privacyUrl`|2048 символов|✔|Url https:// URL-адрес политики конфиденциальности разработчика.|
|`termsOfUseUrl`|2048 символов|✔|В https:// URL-адрес условий использования разработчика.|
|`mpnId`|10 символов| |**Необязательный** Идентификатор Microsoft Partner Network, который определяет партнерской организации, которая строит приложение.|

## <a name="name"></a>name

**Required** — object

Имя вашего приложения, отображаемого для пользователей в teams. Для приложений, отправленных в AppSource, эти значения должны соответствовать сведениям в записи AppSource. Значения и `short` не `full` должны быть одинаковыми.

|Name| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|30 символов|✔|Краткое отображаемом имени приложения.|
|`full`|100 символов||Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.|

## <a name="description"></a>description

**Обязательно —** объект

Описывает приложение для пользователей. Для приложений, отправленных в AppSource, эти значения должны соответствовать сведениям в записи AppSource.

Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, которые помогут потенциальным клиентам понять, что делает ваш опыт. В полном описании также следует отметить, требуется ли для использования внешняя учетная запись. Значения и `short` не `full` должны быть одинаковыми.  Краткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.

|Name| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|80 символов|✔|Краткое описание работы приложения, используемое при ограниченном пространстве.|
|`full`|4000 символов|✔|Полное описание приложения.|

## <a name="packagename"></a>packageName

**Необязательный** — строка

Уникальный идентификатор для этого приложения в нотации обратного домена; например, com.example.myapp. Максимальная длина: 64 символа.

## <a name="localizationinfo"></a>localizationInfo

**Необязательный** — объект

Разрешает спецификацию языка по умолчанию, а также указатели на дополнительные языковые файлы. См. [локализацию.](~/concepts/build-and-test/apps-localization.md)

|Name| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`defaultLanguageTag`||✔|Тег языка строк в этом файле манифеста верхнего уровня.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Массив объектов, определяющих дополнительные языковые переводы.

|Name| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`languageTag`||✔|Тег языка строк в предоставленной файле.|
|`file`||✔|Относительный путь к JSON-файлу, содержащего переведенные строки.|

## <a name="icons"></a>icons

**Required** — object

Значки, используемые в приложении Teams. Файлы значков должны быть включены в пакет отправки. Дополнительные [сведения см.](../../concepts/build-and-test/apps-package.md#app-icons) в значках.

|Name| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`outline`|32 x 32 пикселя|✔|Относительный путь к прозрачному значку контура PNG размером 32x32.|
|`color`|192 x 192 пикселя|✔|Относительный путь к полному значку PNG размером 192x192.|

## <a name="accentcolor"></a>accentColor

**Необязательный** — htmL-код цвета

Цвет, который будет применяться в сочетании с значками структур и в качестве фона.

Значением должен быть допустимый htmL-код цвета, начинающаяся с "#", например `#4464ee` .

## <a name="configurabletabs"></a>configurableTabs

**Необязательный** — массив

Используется, когда в вашем приложении есть вкладка канала команды, которая требует дополнительной настройки перед его добавлением. Настраиваемые вкладки поддерживаются только в области команды (не личной), и в настоящее время поддерживается только одна вкладка для каждого приложения. 

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|string|2048 символов|✔|URL-https://, который будет применяться при настройке вкладки.|
|`scopes`|массив enums|1 |✔|В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области. |
|`canUpdateConfiguration`|boolean|||Значение, указывающее, может ли пользователь обновить экземпляр конфигурации вкладки после создания. Значение по умолчанию: **true.**|
|`context` |массив enums|6 ||Набор `contextItem` областей, в которых поддерживается вкладка. По умолчанию: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|string|2048||Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint. Размер 1024x768. |
|`supportedSharePointHosts`|массив enums|1 ||Определяет, как вкладка будет доступна в SharePoint. Возможные `sharePointFullPage` варианты `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Необязательный** — массив

Определяет набор вкладок, которые можно "закрепить" по умолчанию без добавления пользователем вручную. Статические вкладки, объявленные в области, всегда закреплены в личном режиме `personal` приложения. Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.

Этот элемент является массивом (не более 16 элементов) со всеми элементами `object` типа. Этот блок требуется только для решений, которые предоставляют статическое решение вкладок.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`entityId`|string|64 символа|✔|Уникальный идентификатор сущности, отображаемой на вкладке.|
|`name`|string|128 символов|✔|Отображаемого имени вкладки в интерфейсе канала.|
|`contentUrl`|string||✔|URL-https://, который указывает на пользовательский интерфейс сущности, который будет отображаться на холсте Teams.|
|`websiteUrl`|string|||Url https:// URL-адрес, на который будет указан пользователь, если пользователь выбрал просмотр в браузере.|
|`searchUrl`|string|||Url https:// URL-адрес, на который нужно указать поисковые запросы пользователя.|
|`scopes`|массив enums|1 |✔|В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в рамках личного `personal` опыта.|
|`context` | массив enums| 2 || Набор `contextItem` областей, в которых поддерживается вкладка.|

> [!NOTE]
> Если для отображения релевантного контента или инициации потока проверки подлинности на вкладке требуется контекстно-зависимая информация, см. статью  ["Получить контекст"](../../tabs/how-to/access-teams-context.md)для вкладки Microsoft Teams.

## <a name="bots"></a>bots

**Необязательный** — массив

Определяет бот-решение, а также необязательные сведения, такие как свойства команды по умолчанию.

Элемент является массивом (не более 1 элемента в настоящее время разрешено использовать только один бот для каждого приложения) со всеми элементами &mdash; этого `object` типа. Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|string|64 символа|✔|Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework. Вполне возможно, что он будет таким же, как и общий [ИД приложения.](#id)|
|`scopes`|массив enums|3|✔|Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`). Эти параметры не являются исключающими.|
|`needsChannelSelector`|boolean|||Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал. По умолчанию: **`false`**|
|`isNotificationOnly`|boolean|||Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы. По умолчанию: **`false`**|
|`supportsFiles`|boolean|||Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате. По умолчанию: **`false`**|
|`supportsCalling`|boolean|||Значение, указывающее, где бот поддерживает аудиозвук. **ВАЖНО!** Это свойство в настоящее время является экспериментальным. Экспериментальные свойства могут быть не завершены и претерпит изменения, прежде чем они становятся полностью доступными.  Она предназначена только для тестирования и исследования и не должна использоваться в производственных приложениях. По умолчанию: **`false`**|
|`supportsVideo`|boolean|||Значение, указывающее, где бот поддерживает видеозвонков. **ВАЖНО!** Это свойство в настоящее время является экспериментальным. Экспериментальные свойства могут быть не завершены и претерпит изменения, прежде чем они становятся полностью доступными.  Она предназначена только для тестирования и исследования и не должна использоваться в производственных приложениях. По умолчанию: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Необязательный список команд, которые бот может порекомендовать пользователям. Объект является массивом (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом. Дополнительные [сведения см. в](~/bots/how-to/create-a-bot-commands-menu.md) меню бота.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`items.scopes`|массив enums|3|✔|Указывает область, для которой действует список команд. Возможны значения `team`, `personal` и `groupchat`.|
|`items.commands`|массив объектов|10 |✔|Массив команд, поддерживаемых ботом:<br>`title`: имя команды бота (строка, 32)<br>`description`: простое описание или пример синтаксиса команды и ее аргумента (строка, 128)|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|title|string|12 |✔|Имя команды бота|
|description|string|128 символов|✔|Простое текстовое описание или пример синтаксиса команды и ее аргументов.|

## <a name="connectors"></a>соединители

**Необязательный** — массив

Этот `connectors` блок определяет соединители Office 365 для приложения.

Объект является массивом (не более 1 элемента) со всеми элементами `object` типа. Этот блок необходим только для решений, которые предоставляют соединители.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|string|2048 символов|✔|URL https:// URL-адрес, который будет применяться при настройке соединителя.|
|`scopes`|массив enums|1 |✔|Указывает, предоставляет ли соединители интерфейс в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ). В настоящее время `team` поддерживается только область.|
|`connectorId`|string|64 символа|✔|Уникальный идентификатор соединители, который соответствует его идентификатору в информационной панели разработчика [соединителок.](https://aka.ms/connectorsdashboard)|

## <a name="composeextensions"></a>composeExtensions

**Необязательный** — массив

Определяет расширение обмена сообщениями для приложения.

> [!NOTE]
> В ноябре 2017 г. имя функции было изменено с "расширения составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжают функционировать.

Элемент является массивом (не более 1 элемента) со всеми элементами `object` типа. Этот блок необходим только для решений, которые предоставляют расширение для обмена сообщениями.

|Имя| Тип | Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|string|64|✔|Уникальный ИД приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрировано в Bot Framework. Вполне возможно, что он будет таким же, как и общий ИД приложения.|
|`commands`|массив объектов|10 |✔|Массив команд, поддерживаемых расширением обмена сообщениями|
|`canUpdateConfiguration`|boolean|||Значение, указывающее, может ли пользователь обновлять конфигурацию расширения обмена сообщениями. По умолчанию: **false**.|
|`messageHandlers`|массив объектов|5 ||Список обработчиков, которые позволяют вызывать приложения при определенных условиях.|
|`messageHandlers.type`|string|||Тип обработера сообщений. Должно быть задано значение `"link"`.|
|`messageHandlers.value.domains`|массив строк|||Массив доменов, для которые может регистрироваться обработник сообщений ссылок.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Расширение обмена сообщениями должно объявлять одну или несколько команд. Каждая команда отображается в Microsoft Teams как потенциальное взаимодействие с точкой входа на основе пользовательского интерфейса. Максимум 10 команд.

Каждый элемент команды является объектом со следующей структурой:

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|string|64 символа|✔|ИД команды.|
|`title`|string|32 символа|✔|Удобное имя команды.|
|`type`|string|64 символа||Тип команды. Один из `query` или `action` . По умолчанию: **запрос.**|
|`description`|string|128 символов||Описание, которое отображается для пользователей, чтобы указать назначение этой команды.|
|`initialRun`|boolean|||Boolean value that indicates whether the command should be run initially with no parameters. По умолчанию: **false**.|
|`context`|массив строк|3||Определяет, откуда можно вызвать расширение сообщения. Любое сочетание `compose` , `commandBox` . `message` Значение по умолчанию: `["compose","commandBox"]`.|
|`fetchTask`|boolean|||Boolean value that indicates if it should fetch the task module dynamically. По умолчанию: **false**.|
|`taskInfo`|объект|||Укажите модуль задачи для предварительной загрузки при использовании команды расширения обмена сообщениями.|
|`taskInfo.title`|string|64 символа||Заголовок начального диалоговое окно.|
|`taskInfo.width`|string|||Ширина диалогов — число в пикселях или макет по умолчанию, например "большой", "средний" или "маленький".|
|`taskInfo.height`|string|||Высота диалогов — число в пикселях или макет по умолчанию, например "большой", "средний" или "маленький".|
|`taskInfo.url`|string|||Исходный URL-адрес веб-приложения.|
|`parameters`|массив объекта|5 элементов|✔|Список параметров, которые принимает команда. Минимум: 1; максимум: 5.|
|`parameters.name`|string|64 символа|✔|Имя параметра, которое отображается в клиенте. Это включается в запрос пользователя.|
|`parameters.title`|string|32 символа|✔|Удобное название параметра.|
|`parameters.description`|string|128 символов||Пользовательская строка, описывая назначение этого параметра.|
|`parameters.value`|string|512 символов||Начальное значение параметра.|
|`parameters.inputType`|string|128 символов||Определяет тип управления, отображаемого в модуле задачи для `fetchTask: true` . Один из `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|массив объектов|10 элементов||Варианты выбора для `choiceset` . Используйте только тогда, когда `parameter.inputType` это `choiceset` так.|
|`parameters.choices.title`|string|128 символов|✔|Заголовок выбора.|
|`parameters.choices.value`|string|512 символов|✔|Значение выбора.|

## <a name="permissions"></a>permissions

**Необязательный** — массив строк

Массив, в котором указывается, какие разрешения запрашивает приложение, что позволяет конечным пользователям узнать, как `string` будет выполняться расширение. Следующие параметры являются неисключающими:

* `identity`&emsp;Требуется информация об удостоверении пользователя
* `messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений участникам группы

Изменение этих разрешений при обновлении приложения приведет к повтору пользователями процесса получения согласия при первом запуске обновленного приложения. Дополнительные [сведения см. в](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) обновлении приложения.

## <a name="devicepermissions"></a>devicePermissions

**Необязательный** — массив строк

Указывает нативные функции на устройстве пользователя, к которые ваше приложение может запросить доступ. Возможные варианты:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Необязательный**, за **исключением обязательного,** если отмечено

Список допустимого домена для веб-сайтов, которые приложение ожидает загрузить в клиенте Teams. В списки доменов могут включались поддеревные знаки, `*.example.com` например. Это соответствует только одному сегменту домена; если вам нужно найти `a.b.example.com` соответствие, используйте `*.*.example.com` . Если конфигурации вкладок или пользовательскому интерфейсу содержимого требуется перейти к любому другому домену, кроме того, который используется для настройки вкладок, этот домен должен быть указан здесь.

Однако нет **необходимости** включать в приложение домены поставщиков удостоверений, которые вы хотите поддерживать. Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить его на accounts.google.com, но не следует включать `validDomains[]` accounts.google.com.

Приложения Teams, для работы с которые требуются собственные URL-адреса SharePoint, могут включать "{teamsitedomain}" в допустимый список доменов.

> [!IMPORTANT]
> Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью поддиагром. Например, `yourapp.onmicrosoft.com` допустимо, но `*.onmicrosoft.com` не является допустимым.

Объект является массивом со всеми элементами этого `string` типа.

## <a name="webapplicationinfo"></a>webApplicationInfo

**Необязательный** — объект

Укажите свой ИД приложения Azure Active Directory (Azure AD) и сведения Microsoft Graph, чтобы пользователи легко влияли на ваше приложение. Если ваше приложение зарегистрировано в Azure AD, необходимо предоставить его ИД, чтобы администраторы могли легко просмотреть разрешения и предоставить согласие в Центре администрирования Teams.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|string|36 символов|✔|ИД приложения AAD. Этот ид должен быть GUID.|
|`resource`|string|2048 символов|✔|URL-адрес ресурса приложения для получения маркера auth для SSO. </br> **ПРИМЕЧАНИЕ.** Если вы не используете SSO, убедитесь, что в манифесте приложения введите фикаметричная строковая строка в этом поле, например, чтобы избежать https://notapplicable ошибки. |
|`applicationPermissions`|массив строк|128 символов||Укажите согласие [для конкретного ресурса.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Необязательный** — boolean

Укажите, следует ли показывать индикатор загрузки при загрузке приложения или вкладки. По умолчанию: **false**.
>[!NOTE]
>Если в манифесте приложения установлено "showLoadingIndicator : true", то для правильной загрузки страницы необходимо изменить страницы содержимого вкладок [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) и модулей задач в зависимости от протокола, описанного в описании документа индикатора загрузки.


## <a name="isfullscreen"></a>isFullScreen

 **Необязательный** — boolean

Указать, где отрисовка личного приложения с помощью панели вкладок или без нее. По умолчанию: **false**.

## <a name="activities"></a>activities

**Необязательный** — объект

Определите свойства, которые ваше приложение будет использовать для публикации в веб-канале активности пользователя.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`activityTypes`|массив объектов|128 элементов| | Укажите типы действий, которые ваше приложение может опубликовать на веб-канале активности пользователей.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`type`|string|32 символа|✔|Тип уведомления. *См. ниже.*|
|`description`|string|128 символов|✔|Краткое описание уведомления. *См. ниже.*|
|`templateText`|string|128 символов|✔|Например: "{actor} created task {taskId} for you"|

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
>
>
