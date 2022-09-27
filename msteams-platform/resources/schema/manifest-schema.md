---
title: Справочник по схеме манифеста
description: В этой статье представлен справочник по схеме манифеста Microsoft Teams, схема и пример полного манифеста.
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: b1795af69256eec27e34917cad0b24924f490083
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2022
ms.locfileid: "68026971"
---
# <a name="app-manifest-schema-for-teams"></a>Схема манифеста приложения для Teams

В манифесте приложения Microsoft Teams описывается, как ваше приложение интегрируется с продуктом Microsoft Teams. Манифест приложения должен соответствовать схеме, размещенной по адресу [`https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json). Поддерживаются предыдущие версии 1.0, 1.1,...,1.13 и текущая версия 1.14 (в URL-адресе используется "v1.x").
Дополнительные сведения об изменениях в каждой версии, см. в разделе [журнал изменений манифеста](https://github.com/OfficeDev/microsoft-teams-app-schema/releases).

В следующей таблице перечислены версии TeamsJS и манифеста приложения в соответствии с различными сценариями приложений.

[!INCLUDE [pre-release-label](~/includes/teamjs-version-details.md)]

В следующем примере схемы показаны все варианты расширяемости:

## <a name="sample-full-manifest"></a>Пример полного манифеста

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json",
    "manifestVersion": "1.14",
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
            "context": [
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
            "context": [
                "personalTab",
                "channelTab"
            ],
            "name": "Display name of tab",
            "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
            "websiteUrl": "https://contoso.com/content (displayed in web browser)",
            "searchUrl": "https://contoso.com/content (displayed in web browser)"
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
                    "fetchTask": false ,
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
        "resource": "Resource URL for acquiring auth token for SSO"
    },
    "authorization": {
        "permissions": {
            "resourceSpecific": [
                {
                    "type": "Application",
                    "name": "ChannelSettings.Read.Group"
                },
                {
                    "type": "Delegated",
                    "name": "ChannelMeetingParticipant.Read.Group"
                }
            ]
        }
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
    },
    "meetingExtensionDefinition": {
        "scenes": [
            {
                "id": "9082c811-7e6a-4174-8173-6ccd57d377e6",
                "name": "Getting started sample",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 0
            },
            {
                "id": "afeaed22-f89b-48e1-98b4-46a514344e4a",
                "name": "Sample-1",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 3
            }
        ]
    }
}
```

Схема определяет следующие свойства:

## <a name="schema"></a>$schema

Необязательно, но рекомендуется — строка

URL-адрес со ссылкой на схему JSON для манифеста (https://).

## <a name="manifestversion"></a>manifestVersion

**Обязательно** — строка

Версия схемы манифеста, используемая этим манифестом. Используйте `1.13`, чтобы включить поддержку приложений Teams в Outlook и Office; используйте `1.12` (или более ранние версии) для приложений, доступных только для Teams.

## <a name="version"></a>version

**Обязательно** — строка

Версия определенного приложения. При обновлении каких-либо данных в манифесте необходимо также увеличить номер версии. За счет этого при установке нового манифеста он заменит прежний, а пользователь получит новую функциональность. При отправке этого приложения в магазин необходимо повторно отправить и проверить новый манифест. Приложение автоматически получит новый обновленный манифест через несколько часов после утверждения манифеста.

Если приложение запрашивает изменение разрешений, пользователям будет предложено обновить приложение и заново предоставить ему согласие.

Строка версии должна соответствовать стандарту [semver](http://semver.org/)(ОСНОВНАЯ_ВЕРСИЯ.ДОПОЛНИТЕЛЬНАЯ_ВЕРСИЯ.ИСПРАВЛЕНИЕ).

## <a name="id"></a>Идентификатор

**Обязательно** — идентификатор приложения Майкрософт

Это уникальный идентификатор, сформированный для приложения корпорацией Майкрософт. У вас есть идентификатор, если бот зарегистрирован с помощью Microsoft Bot Framework. У вас есть идентификатор, если веб-приложение вашей вкладке уже входит в систему с учетной записью Майкрософт. Здесь необходимо ввести этот идентификатор. В противном случае необходимо создать новый идентификатор на [портале регистрации приложений Майкрософт](https://aka.ms/appregistrations). При добавлении бота используйте этот же идентификатор.

> [!NOTE]
> Если вы отправляете обновление для существующего приложения в AppSource, то нельзя изменять идентификатор в манифесте.

## <a name="developer"></a>developer

**Обязательно** — объект

Указывает сведения о вашей компании. Для приложений, отправленных в магазин Teams, эти значения должны совпадать с данными в описании в магазине. Дополнительные сведения см. в статье [правила публикации в магазине Teams](~/concepts/deploy-and-publish/appsource/publish.md).

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`name`|32 символа|✔️|Отображаемое имя для разработчика.|
|`websiteUrl`|2048 символов|✔️|URL-адрес веб-сайта разработчика (https://). По этой ссылке пользователи должны переходить на целевую страницу вашей компании или конкретного продукта.|
|`privacyUrl`|2048 символов|✔️|URL-адрес политики конфиденциальности разработчика (https://).|
|`termsOfUseUrl`|2048 символов|✔️|URL-адрес условий использования разработчика (https://).|
|`mpnId`|10 символов| |**Необязательно** — идентификатор партнерской организации, создавшей приложение, в Microsoft Partner Network.|

## <a name="name"></a>name

**Обязательно** — объект

Имя интерфейса приложения, отображаемое для пользователей в интерфейсе Teams. Для приложений, отправляемых в AppSource, эти значения должны совпадать с данными в записи AppSource. Значения `short` и `full` должны отличаться.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|30 символов|✔️|Краткое отображаемое имя приложения.|
|`full`|100 символов||Полное имя приложения. Используется, если длина полного имени приложения превышает 30 символов.|

## <a name="description"></a>description

**Обязательно** — объект

Описывает приложение для пользователей. Для приложений, отправляемых в AppSource, эти значения должны совпадать с данными в записи AppSource.

Убедитесь, что описание включает возможности приложения и его назначение для потенциальных клиентов. В полном описании также необходимо указать, нужно ли использовать внешнюю учетную запись. Значения `short` и `full` должны отличаться. Краткое описание не может повторяться в длинном описании и не должно содержать имя другого приложения.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|80 символов|✔️|Краткое описание возможностей приложения. Используется, когда доступно ограниченное пространство.|
|`full`|4000 символов|✔️|Полное описание приложения.|

## <a name="packagename"></a>packageName

**Необязательно** — строка

A unique identifier for the app in reverse domain notation; for example, com.example.myapp. Maximum length: 64 characters.

## <a name="localizationinfo"></a>localizationInfo

**Необязательно** — объект

Allows the specification of a default language and provides pointers to more language files. For more information, see [localization](~/concepts/build-and-test/apps-localization.md).

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`defaultLanguageTag`||✔️|Тег язык строк в этом файле манифеста верхнего уровня.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Массив объектов, указывающих дополнительные переводы.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`languageTag`||✔️|Тег языка строк в предоставленном файле.|
|`file`||✔️|Относительный путь к файлу .JSON с переведенными строками.|

## <a name="icons"></a>icons

**Обязательно** — объект

Значки, используемые в приложении Teams. Файлы значков должны быть включены в отправляемый пакет. Дополнительные сведения см. в статье [Значки](../../concepts/build-and-test/apps-package.md#app-icons).

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`outline`|32 x 32 пикселя|✔️|Относительный путь к прозрачному значку контура размером 32x32 пикселя в формате PNG.|
|`color`|192 x 192 пикселя|✔️|Относительный путь к полноцветному значку размером 192x192 пикселя в формате PNG.|

## <a name="accentcolor"></a>accentColor

**Обязательно** — шестнадцатеричный код цвета HTML

Цвет, который нужно использовать в качестве фона для значков контура.

Значение должно быть допустимым шестнадцатеричным кодом цвета HTML и должно начинаться с "#". Пример: `#4464ee`.

## <a name="configurabletabs"></a>configurableTabs

**Необязательно** — массив

Используется, когда в интерфейсе приложения есть вкладка канала группы, которая требует дополнительной настройки перед добавлением. Настраиваемые вкладки поддерживаются только в областях `team` и `groupchat`. Одни и те же вкладки можно настраивать несколько раз. Но определить их в манифесте можно только один раз.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|string|2048 символов|✔️|URL-адрес, используемый при настройке вкладки (https://).|
|`scopes`|массив элементов enum|1|✔️|В настоящее время настраиваемые вкладки поддерживают только области `team` и `groupchat`. |
|`canUpdateConfiguration`|Boolean|||A value indicating whether an instance of the tab's configuration can be updated by the user after creation. Default: **true**.|
|`context` |массив элементов enum|6||Набор областей `contextItem`, в которых [поддерживается вкладка](../../tabs/how-to/access-teams-context.md). По умолчанию: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|string|2048||A relative file path to a tab preview image for use in SharePoint. Size 1024x768. |
|`supportedSharePointHosts`|массив элементов enum|1||Defines how your tab is made available in SharePoint. Options are `sharePointFullPage` and `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Необязательно** — массив

Это набор вкладок, который можно закрепить по умолчанию без добавления их вручную пользователем. Статические вкладки,объявляемые в области `personal`, всегда закрепляются в личном интерфейсе приложения. Статические вкладки,объявляемые в области `team`, сейчас не поддерживаются.

Этот элемент — массив (не более 16 элементов) со всеми элементами типа `object`. Этот блок требуется только для решений со статическими вкладками.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`entityId`|string|64 символа|✔️|Уникальный идентификатор сущности, отображаемый на вкладке.|
|`name`|string|128 символов|✔️|Отображаемое имя вкладки в интерфейсе канала.|
|`contentUrl`|string||✔️|URL-адрес, указывающий на пользовательский интерфейс объекта для отображения на холсте Microsoft Teams (https://).|
|`websiteUrl`|string|||URL-адрес, используемый, если пользователь выбирает просмотр в браузере (https://).|
|`searchUrl`|string|||URL-адрес, используемый для поисковых запросов пользователя (https://).|
|`scopes`|массив элементов enum|1|✔️|В настоящее время статические вкладки поддерживаются только для области `personal`, поэтому их можно подготовить только в личном интерфейсе.|
|`context` | массив элементов enum| 2|| Набор областей `contextItem`, в которых поддерживается вкладка.|

> [!NOTE]
> The searchUrl feature is not available for the third-party developers.
> If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).

## <a name="bots"></a>bots

**Необязательно** — массив

Определяет решение бота, а также дополнительные сведения, такие как свойства команды по умолчанию.

Этот элемент — массив (не более одного элемента&mdash;в настоящее время поддерживается только один бот на приложение) со всеми элементами типа `object`. Этот блок требуется только для решений, предоставляющих возможности бота.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|string|64 символа|✔️|Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework. Этот идентификатор может совпадать с общим [идентификатором приложения](#id).|
|`scopes`|массив элементов enum|3|✔️|Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`). These options are non-exclusive.|
|`needsChannelSelector`|Boolean|||Describes whether or not the bot uses a user hint to add the bot to a specific channel. Default: **`false`**|
|`isNotificationOnly`|Логический|||Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot. Default: **`false`**|
|`supportsFiles`|Логический|||Indicates whether the bot supports the ability to upload/download files in personal chat. Default: **`false`**|
|`supportsCalling`|Boolean|||Значение, указывающее, поддерживает ли бот голосовые звонки. **ВАЖНО.** Это свойство в настоящее время является экспериментальным. Экспериментальные свойства могут быть неполными, а также могут быть изменены до полной доступности.  Это свойство предоставлено только для тестирования и исследования, его не следует использовать в рабочих приложениях. По умолчанию: **`false`**|
|`supportsVideo`|Boolean|||Значение, указывающее, поддерживает ли бот видеозвонки. **ВАЖНО.** Это свойство в настоящее время является экспериментальным. Экспериментальные свойства могут быть неполными, а также могут быть изменены до полной доступности.  Это свойство предоставлено только для тестирования и исследования, его не следует использовать в рабочих приложениях. По умолчанию: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Список команд, которые ваш бот может рекомендовать пользователям. Объект — массив (не более двух элементов) со всеми элементами типа `object`; необходимо определить отдельный список команд для каждой области, поддерживаемой ботом. Дополнительные сведения см. в статье [Меню ботов](~/bots/how-to/create-a-bot-commands-menu.md).

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`items.scopes`|массив элементов enum|3|✔️|Specifies the scope for which the command list is valid. Options are `team`, `personal`, and `groupchat`.|
|`items.commands`|массив объектов|10|✔️|Массив команд, поддерживаемых ботом:<br>`title`: имя команды бота (строка, 32)<br>`description`: простое описание или пример синтаксиса команды и ее аргументов (строка, 128).|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|title|string|12 |✔️|Имя команды бота.|
|description|string|128 символов|✔️|Простое текстовое описание или пример синтаксиса команды и ее аргументов.|

## <a name="connectors"></a>connectors

**Необязательно** — массив

Блок `connectors` определяет соединитель Office 365 для приложения.

Объект — массив (не более одного элемента) со всеми элементами типа `object`. Этот блок необходим только для решений, предоставляющих соединители.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|string|2048 символов|✔️|URL-адрес, используемый при настройке соединителя (https://).|
|`scopes`|массив элементов enum|1|✔️|Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`). Currently, only the `team` scope is supported.|
|`connectorId`|string|64 символа|✔️|Уникальный идентификатор соединителя, соответствующий его идентификатору на [информационной панели разработчиков соединителей](https://aka.ms/connectorsdashboard).|

## <a name="composeextensions"></a>composeExtensions

**Необязательно** — массив

Определяет расширение для обмена сообщениями для приложения.

> [!NOTE]
> Название функции было изменено с ''расширение для составления сообщений'' на ''расширение для обмена сообщениями'' в ноябре 2017 г., но имя в манифесте осталось прежним, чтобы существующие расширения продолжали работать.

Этот элемент — массив (не более одного элемента) со всеми элементами типа `object`. Этот блок необходим только для решений, предоставляющих расширение для сообщений.

|Имя| Тип | Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|string|64|✔️|Уникальный идентификатор приложения Microsoft для бота, поддерживающего расширение для обмена сообщениями, в соответствии с регистрацией в Bot Framework. Этот идентификатор может совпадать с общим идентификатором приложения.|
|`commands`|массив объектов|10|✔️|Массив команд, поддерживаемых расширением для обмена сообщениями.|
|`canUpdateConfiguration`|Логическое|||A value indicating whether the configuration of a message extension can be updated by the user. Default: **false**.|
|`messageHandlers`|массив объектов |5||Список обработчиков, которые позволяют вызывать приложение при выполнении определенных условий.|
|`messageHandlers.type`|string|||The type of message handler. Must be `"link"`.|
|`messageHandlers.value.domains`|массив строк|||Массив доменов, на которые может зарегистрироваться обработчик сообщений ссылок.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Расширение для обмена сообщениями должно объявить одну или несколько, но не более 10 команд. Каждая команда отображается в Microsoft Teams как потенциальное взаимодействие с точки входа на основе пользовательского интерфейса.

Каждый элемент команды представляет собой объект со следующей структурой:

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|string|64 символа|✔️|ИД команды.|
|`title`|string|32 символа|✔️|Понятное имя команды.|
|`type`|string|64 символа||Тип команды. Либо `query`, либо `action`. По умолчанию: **query**.|
|`description`|string|128 символов||Описание назначения команды, которое отображается для пользователей.|
|`initialRun`|Boolean|||A Boolean value indicates whether the command runs initially with no parameters. Default is **false**.|
|`context`|массив строк|3||Определяет, откуда можно вызвать расширение сообщения. Любое сочетание `compose`, `commandBox` и `message`. Значение по умолчанию: `["compose","commandBox"]`.|
|`fetchTask`|Boolean|||A Boolean value that indicates if it must fetch the task module dynamically. Default is **false**.|
|`taskInfo`|объект|||Укажите модуль задачи для предварительной загрузки при использовании команды расширения для обмена сообщениями.|
|`taskInfo.title`|string|64 символа||Начальное название диалогового окна|
|`taskInfo.width`|string|||Ширина диалогового окна — количество пикселей или макет по умолчанию, например "large", "medium" или "small".|
|`taskInfo.height`|string|||Высота диалогового окна — количество пикселей или макет по умолчанию, например "large", "medium" или "small".|
|`taskInfo.url`|string|||Начальный URL-адрес веб-представления.|
|`parameters`|массив объекта|5 элементов|✔️|Список параметров, которые принимает команда. Минимум: 1; максимум: 5.|
|`parameters.name`|string|64 символа|✔️|The name of the parameter as it appears in the client. The parameter name is included in the user request.|
|`parameters.title`|string|32 символа|✔️|Понятное название параметра.|
|`parameters.description`|string|128 символов||Понятное описание назначения параметра.|
|`parameters.value`|string|512 символов||Начальное значение параметра. В настоящее время это значение не поддерживается|
|`parameters.inputType`|string|128 символов||Defines the type of control displayed on a task module for`fetchTask: false` . One of `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|массив объектов|10 элементов||Варианты для `choiceset`. Используйте, только `parameter.inputType` равно `choiceset`.|
|`parameters.choices.title`|string|128 символов|✔️|Название выбора.|
|`parameters.choices.value`|string|512 символов|✔️|Значение выбора.|

## <a name="permissions"></a>permissions

**Необязательно** — массив строк

An array of `string`, which specifies which permissions the app requests, which let end users know how the extension does. The following options are non-exclusive:

* `identity` &emsp; Требуются сведения удостоверения пользователя.
* `messageTeamMembers` &emsp; Требуется разрешение на отправку прямых сообщений участникам группы.

Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app. For more information, see [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).

> [!NOTE]
> Разрешения теперь являются нерекомендуемыми.

## <a name="devicepermissions"></a>devicePermissions

**Необязательно** — массив строк

Provides the native features on a user's device that your app requests access to. Options are:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Необязательно** кроме случаев, когда указано **Обязательно**.

Список допустимых доменов для веб-сайтов, которые приложение может загружать в клиенте Teams. Списки доменов могут включать подстановочные знаки, например `*.example.com`. Допустимый домен соответствует только одному сегменту домена. Если нужно соответствие `a.b.example.com`, то используйте `*.*.example.com`. Если конфигурация вкладки или пользовательский интерфейс контента переходит на любой другой домен, отличный от конфигурации вкладки, то этот домен нужно указать здесь.

**Не** включайте домены поставщиков удостоверений, которые необходимо поддерживать в приложении. Например, чтобы выполнить аутентификацию с помощью идентификатора Google, необходимо перенаправить accounts.google.com, однако не нужно включать accounts.google.com.`validDomains[]`

Приложения Teams, которым для правильной работы требуются собственные URL-адреса SharePoint, включают "{teamsitedomain}" в список допустимых доменов.

> [!IMPORTANT]
> Не добавляйте неподконтрольные вам домены (напрямую или с помощью подстановочных знаков). Например, `yourapp.onmicrosoft.com` — допустимое значение, а `*.onmicrosoft.com` — недопустимое.

Объект — массив со всеми элементами типа `string`.

## <a name="webapplicationinfo"></a>webApplicationInfo

**Необязательно** — объект

Укажите идентификатор приложения Azure Active Directory и сведения Microsoft Graph, чтобы помочь пользователям легко входить в приложение. Если приложение зарегистрировано в Microsoft Azure Active Directory (Azure AD), вы должны предоставить ID этого приложения. Администраторы могут проверять разрешения и предоставлять согласие в центре администрирования Teams.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|string|36 символов|✔️|Идентификатор приложения в Azure Active Directory. Этот идентификатор должен быть глобальным уникальным идентификатором.|
|`resource`|string|2048 символов|✔️|URL-адрес ресурса приложения для получения маркера проверки подлинности для единого входа. </br> **ПРИМЕЧАНИЕ:** Если вы не используете единый вход, убедитесь, что в манифесте приложения введите фиктивное строковое значение в этом поле, например, `https://notapplicable` чтобы избежать ошибки. |

## <a name="graphconnector"></a>graphConnector

**Необязательно** — объект

Укажите конфигурацию соединителя Graph приложения. Если он присутствует [, webApplicationInfo.id также](#webapplicationinfo) необходимо указать.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`notificationUrl`|string|2048 символов|✔️|URL-адрес, по которому должны отправляться уведомления Graph-соединителя для приложения.|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Необязательно** — логическое значение

Indicates if or not to show the loading indicator when an app or tab is loading. Default is **false**.
>[!NOTE]
>Если для `showLoadingIndicator` в манифесте приложения установлен значение "true", измените страницы содержимого на вкладках и в модулях задач, как описано в документе [Отображение собственного индикатора загрузки](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator).

## <a name="isfullscreen"></a>isFullScreen

 **Необязательно** — логическое значение

Указывает, отображается ли личное приложение без панели заголовка вкладки (что означает полноэкранный режим). Значение по умолчанию: **false**.

> [!NOTE]
>
> * `isFullScreen` работает только с приложениями, опубликованными в вашей организации. Загруженные и опубликованные сторонние приложения не могут использовать это свойство (оно игнорируется).
>
> * `isFullScreen=true` удаляет предоставленную Teams панель заголовка и заголовок из личных приложений и диалоговых окон модулей задач.

## <a name="activities"></a>activities

**Необязательно** — объект

Определите свойства, которые приложение использует для публикаций в ленте новостей пользователя.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`activityTypes`|массив объектов |128 элементов| | Укажите типы действий, которые приложение может публиковать в канале новостей пользователей.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`type`|string|32 символа|✔️|Тип уведомления. *См. ниже*.|
|`description`|string|128 символов|✔️|A brief description of the notification. *See below*.|
|`templateText`|string|128 символов|✔️|Пример: "Пользователь {actor} создал для вас задачу {taskId}"|

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

**Необязательно** — строка

Указывает область установки, заданную для этого приложения по умолчанию. Когда пользователь попытается добавить приложение, заданная область будет одним из вариантов, отображаемых на кнопке. Доступные варианты:

* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**Необязательно** — объект

When a group install scope is selected, it will define the default capability when the user installs the app. Options are:

* `team`
* `groupchat`
* `meetings`

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`team`|string|||When the install scope selected is `team`, this field specifies the default capability available. Options: `tab`, `bot`, or `connector`.|
|`groupchat`|string|||When the install scope selected is `groupchat`, this field specifies the default capability available. Options: `tab`, `bot`, or `connector`.|
|`meetings`|string|||When the install scope selected is `meetings`, this field specifies the default capability available. Options: `tab`, `bot`, or `connector`.|

## <a name="configurableproperties"></a>configurableProperties

**Необязательно** — массив

Блок `configurableProperties` определяет свойства приложений, доступные для настройки администраторам Teams. Дополнительные сведения см. в разделе [включение настройки приложения](~/concepts/design/enable-app-customization.md). Функция настройки приложения не поддерживается в пользовательских приложениях и в бизнес-приложениях.

> [!NOTE]
> Необходимо определить хотя бы одно свойство. В этом блоке можно определить не более 9 свойств.

Можно определить любое из следующих свойств:

* [name](#name): отображаемое имя приложения.
* [shortDescription](#description): краткое описание приложения.
* [longDescription](#description): длинное описание приложения.
* [smallImageUrl](#icons): значок структуры приложения.
* [largeImageUrl](#icons): значок цвета приложения.
* [accentColor](#accentcolor): используемый цвет и фон для значков структуры.
* [developerUrl](#developer): URL-адрес HTTPS веб-сайта разработчика.
* [privacyUrl](#developer): URL-адрес HTTPS политики конфиденциальности разработчика.
* [termsOfUseUrl](#developer): URL-адрес HTTPS условий использования разработчика.

## <a name="supportedchanneltypes"></a>supportedChannelTypes

**Необязательно** — массив

Включает приложение в нестандартных каналах. Если приложение поддерживает область группы и это свойство определено, то Teams соответствующим образом включает ваше приложение в каждом типе канала. В настоящее время поддерживаются частные и общие каналы.

> [!NOTE]
>
> * Если приложение поддерживает область группы, оно работает в стандартных каналах независимо от значений, определенных в этом свойстве.
> * Для правильной работы ваше приложение может учитывать уникальные свойства каждого типа канала. Чтобы включить вкладку для частных и общих каналов, см. раздел ["](~/tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels) Извлечение контекста в частных каналах" и получение [контекста в общих каналах](../../tabs/how-to/access-teams-context.md#get-context-in-shared-channels)

## <a name="defaultblockuntiladminaction"></a>defaultBlockUntilAdminAction

**Необязательно** — логическое значение

Если для свойства `defaultBlockUntilAdminAction` установлено значение **true**, приложение по умолчанию будет скрыто от пользователей, пока администратор не разрешит его. Если установлено значение **true**, приложение будет скрыто для всех клиентов и конечных пользователей. Администраторы клиента видят приложение в центре администрирования Teams и могут разрешить или заблокировать приложение. Значение по умолчанию — **false**. Дополнительные сведения о блоке приложений по умолчанию см. в разделе "Блокировка приложений по умолчанию [для пользователей до тех пор, пока администратор не утвердит его"](../../concepts/design/enable-app-customization.md#block-apps-by-default-for-users-until-an-admin-approves).

## <a name="publisherdocsurl"></a>publisherDocsUrl

**Необязательно** — строка

**Максимальный размер** — 128 символов

`publisherDocsUrl` — URL-адрес (HTTPS) информационной страницы, на которой администраторы могут получить рекомендации перед скачиванием приложение, которое по умолчанию заблокировано. На этой странице также можно указать инструкции или сведения о приложении, полезные для администратора клиента.

## <a name="subscriptionoffer"></a>subscriptionOffer

**Необязательно** — объект

Указывает предложение SaaS, связанное с приложением.

|Имя| Тип|Максимальный размер|Обязательный|Описание|
|---|---|---|---|---|
|`offerId`| string | 2048 символов | ✔️ | A unique identifier that includes your Publisher ID and Offer ID, which you can find in [Partner Center](https://partner.microsoft.com/dashboard). You must format the string as `publisherId.offerId`.|

## <a name="meetingextensiondefinition"></a>meetingExtensionDefinition

**Необязательно** — объект

Specify meeting extension definition. For more information, see [custom Together Mode scenes in Teams](../../apps-in-teams-meetings/teams-together-mode.md).

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`scenes`|массив объектов| 5 элементов||Сцены, поддерживаемые собранием.|
|`supportsStreaming`|Логическое|||Значение, указывающее, может ли приложение передавать звуковое и видеосодержимое собрания в конечную точку по протоколу RTMP. Значение по умолчанию — **false**.|

### <a name="meetingextensiondefinitionscenes"></a>meetingExtensionDefinition.scenes

|Имя| Тип|Максимальный размер|Обязательный |Описание|
|---|---|---|---|---|
|`id`|||✔️| Уникальный идентификатор сцены. Этот идентификатор должен быть глобальным уникальным идентификатором. |
|`name`| string | 128 символов |✔️| Имя сцены. |
|`file`|||✔️| Относительный путь к файлу JSON метаданных сцен. |
|`preview`|||✔️| Относительный путь к файлу значка предварительного просмотра PNG сцен. |
|`maxAudience`| integer | 50  |✔️| Максимальное количество аудиторий, поддерживаемых в сцене. |
|`seatsReservedForOrganizersOrPresenters`| integer | 50 |✔️| Количество мест, зарезервированных для организаторов или докладчиков.|

## <a name="authorization"></a>авторизация

**Необязательно** — объект

> [!NOTE]
> If you set the `manifestVersion` property to 1.12, the authorization property is incompatible with the older versions (version 1.11 or earlier) of the manifest. Authorization is supported for manifest version 1.12.

Укажите и консолидируйте сведения об авторизации для приложения.

|Имя| Тип|Максимальный размер|Обязательный |Описание|
|---|---|---|---|---|
|`permissions`||||Список разрешений, необходимых приложению для работы.|

### <a name="authorizationpermissions"></a>authorization.permissions

|Имя| Тип|Максимальный размер|Обязательный |Описание|
|---|---|---|---|---|
|`resourceSpecific`| массив объектов|16 элементов||Разрешения, защищающие доступ к данным на уровне экземпляров ресурсов.|

### <a name="authorizationpermissionsresourcespecific"></a>authorization.permissions.resourceSpecific

|Имя| Тип|Максимальный размер|Обязательный |Описание|
|---|---|---|---|---|
|`type`|string||✔️| The type of the resource-specific permission. Options: `Application` and `Delegated`.|
|`name`|string|128 символов|✔️|Имя разрешения для определенного ресурса. Дополнительные сведения см. в разделе [Разрешения приложений для конкретных ресурсов](#resource-specific-application-permissions) и [Делегированные разрешения для конкретных ресурсов](#resource-specific-delegated-permissions)|

#### <a name="resource-specific-application-permissions"></a>Разрешения приложений для конкретных ресурсов

Разрешения приложений позволяют приложению получать доступ к данным без необходимости входа пользователя. Сведения о разрешениях приложений см. в статье [Согласие на использование конкретных ресурсов для MS Graph и MS BotSDK](../../graph-api/rsc/resource-specific-consent.md).

#### <a name="resource-specific-delegated-permissions"></a>Делегированные разрешения для конкретных ресурсов

Делегированные разрешения позволяют приложению получать доступ к данным от имени вошедшего пользователя.

* **Делегированные разрешения на использование конкретных ресурсов для команд**

    |**Имя**|**Описание**|
    |---|---|
    |`ChannelMeetingParticipant.Read.Group`| Позволяет приложению читать сведения об участниках, включая имя, роль, идентификатор, время присоединения и ухода, собрания канала, связанные с этой командой, от имени выполнившего вход пользователя.|
    |`InAppPurchase.Allow.Group`| Позволяет приложению отображать предложения в Marketplace в этой команде и совершать покупки в приложении от имени выполнившего вход пользователя.|
    |`ChannelMeetingStage.Write.Group`| Позволяет приложению отображать содержимое на этапе собрания в собраниях канала, связанных с этой командой, от имени выполнившего вход пользователя.|
    |`LiveShareSession.ReadWrite.Group`|Позволяет приложению создавать и синхронизировать сеансы Live Share для собраний, связанных с этой командой, а также получать доступ к связанным сведениям о списке собраний, таким как роль участника собрания, от имени вошедвшего пользователя.|

* **Делегированные разрешения на использование конкретных ресурсов для чатов или собраний**

    |**Имя**|**Описание**|
    |---|---|
    |`InAppPurchase.Allow.Chat`|Позволяет приложению отображать предложения в Marketplace в этом чате и связанных собраниях и совершать покупки в приложении от имени выполнившего вход пользователя.|
    |`MeetingStage.Write.Chat`|Позволяет приложению отображать содержимое на этапе собрания в собраниях, связанных с этим чатом, от имени выполнившего вход пользователя.|
    |`OnlineMeetingParticipant.Read.Chat`|Позволяет приложению читать сведения об участниках, включая имя, роль, идентификатор, время присоединения и ухода, собрания, связанные с этим чатом, от имени выполнившего вход пользователя.|
    |`OnlineMeetingParticipant.ToggleIncomingAudio.Chat`|Позволяет приложению переключать входящий звук для участников собраний, связанных с этим чатом, от имени выполнившего вход пользователя.|
    |`LiveShareSession.ReadWrite.Chat`|Позволяет приложению создавать и синхронизировать сеансы Live Share для собраний, связанных с этим чатом, а также получать доступ к связанным сведениям о списке собраний, таким как роль участника собрания, от имени вошедшей в систему пользователя.|
   |`OnlineMeetingIncomingAudio.Detect.Chat`|Позволяет приложению обнаруживать изменения в состоянии входящего звука на собраниях, связанных с этим чатом, от имени вошедвшего пользователя.|

* **Делегированные разрешения на использование конкретных ресурсов для пользователей**

    |**Имя**|**Описание**|
    |---|---|
    |`InAppPurchase.Allow.User`|Позволяет приложению отображать предложения в Marketplace и совершать покупки в приложении от имени выполнившего вход пользователя.|

## <a name="create-a-manifest-file"></a>Создание файла манифеста

Если у вашего приложения нет файла манифеста приложения Teams, его необходимо создать.

Чтобы создать файл манифеста приложения Teams:

1. Используйте [пример схемы манифеста](#sample-full-manifest) для создания JSON-файла.
1. Сохраните его в корневой папке проекта как `manifest.json`.

<br>
<details>
<summary>Ниже приведен пример схемы манифеста для приложения вкладки с включенным единым входом.</summary>
<br>

> [!NOTE]
> Пример содержимого манифеста, показанный здесь, предназначен только для приложения вкладки. В нем используются примеры значений для URI поддомена и имени пакета. Дополнительные сведения см. в [примере схемы манифеста](#sample-full-manifest).

  ```json
{ 
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json", 
 "manifestVersion": "1.12", 
 "version": "1.0.0", 
 "id": "{new GUID for this Teams app - not the Azure AD App ID}", 
 "packageName": "com.contoso.teamsauthsso", 
 "developer": { 
 "name": "Microsoft", 
 "websiteUrl": "https://www.microsoft.com", 
 "privacyUrl": "https://www.microsoft.com/privacy", 
 "termsOfUseUrl": "https://www.microsoft.com/termsofuse" 
  }, 

  "name": { 
    "short": "Teams Auth SSO", 
    "full": "Teams Auth SSO" 
  }, 


  "description": { 
    "short": "Teams Auth SSO app", 
    "full": "The Teams Auth SSO app" 
  }, 

  "icons": { 
    "outline": "outline.png", 
    "color": "color.png" 
  }, 

  "accentColor": "#60A18E", 
  "staticTabs": [ 
    { 
     "entityId": "auth", 
     "name": "Auth", 
     "contentUrl": "https://https://subdomain.example.com/Home/Index", 
     "scopes": [ "personal" ] 
    } 
  ], 

  "configurableTabs": [ 
    { 
     "configurationUrl": "https://subdomain.example.com/Home/Configure", 
     "canUpdateConfiguration": true, 
     "scopes": [ 
     "team" 
      ] 
    } 
  ], 
  "permissions": [ "identity", "messageTeamMembers" ], 
  "validDomains": [ 
   "{subdomain or ngrok url}" 
  ], 
  "webApplicationInfo": { 
    "id": "{Azure AD AppId}", 
    "resource": "api://subdomain.example.com/{Azure AD AppId}" 
  }
} 
```

</details>

## <a name="see-also"></a>См. также

* [Понимание структуры приложений Microsoft Teams](~/concepts/design/app-structure.md)
* [Разрешение настройки приложения](~/concepts/design/enable-app-customization.md)
* [Локализация приложения](~/concepts/build-and-test/apps-localization.md)
* [Интеграция возможностей мультимедиа](~/concepts/device-capabilities/media-capabilities.md)
* [Схема манифеста предварительной общедоступной версии для разработчиков для Microsoft Teams](manifest-schema-dev-preview.md)
