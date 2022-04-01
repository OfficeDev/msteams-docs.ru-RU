---
title: Справочник по схеме манифеста
description: Описывает схему манифеста для Microsoft Teams
ms.topic: reference
ms.author: lajanuar
ms.localizationpriority: high
keywords: схема манифеста teams
ms.openlocfilehash: 3117195b697061b4199ac629f73d8ffd2d93cd6a
ms.sourcegitcommit: 52af681132e496a57b18f468c5b73265a49a5f44
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/31/2022
ms.locfileid: "64590747"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Справочник: схема манифеста для Microsoft Teams

Манифест Teams описывает, каким образом приложение интегрируется с продуктом Microsoft Teams. Манифест должен соответствовать схеме, размещенной по адресу [`https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json). Поддерживаются также предыдущие версии 1.0, 1.1,... и 1.12 (с использованием "v1.x" в URL-адресе).
Дополнительные сведения об изменениях в каждой версии, см. в разделе [журнал изменений манифеста](https://github.com/OfficeDev/microsoft-teams-app-schema/releases).

В следующем примере схемы показаны все варианты расширяемости:

## <a name="sample-full-manifest"></a>Пример полного манифеста

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json",
    "manifestVersion": "1.12",
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

Версия схемы манифеста, используемая этим манифестом.

## <a name="version"></a>version

**Обязательно** — строка

Версия определенного приложения. При обновлении каких-либо данных в манифесте необходимо также увеличить номер версии. За счет этого при установке нового манифеста он заменит прежний, а пользователь получит новую функциональность. При отправке этого приложения в магазин необходимо повторно отправить и проверить новый манифест. Приложение автоматически получит новый обновленный манифест через несколько часов после утверждения манифеста.

Если приложение запрашивает изменение разрешений, пользователям будет предложено обновить приложение и заново предоставить ему согласие.

Строка версии должна соответствовать стандарту [semver](http://semver.org/)(ОСНОВНАЯ_ВЕРСИЯ.ДОПОЛНИТЕЛЬНАЯ_ВЕРСИЯ.ИСПРАВЛЕНИЕ).

## <a name="id"></a>id

**Обязательно** — идентификатор приложения Майкрософт

Это уникальный идентификатор, сформированный для приложения корпорацией Майкрософт. У вас есть идентификатор, если бот зарегистрирован с помощью Microsoft Bot Framework. У вас есть идентификатор, если веб-приложение вашей вкладке уже входит в систему с учетной записью Майкрософт. Здесь необходимо ввести этот идентификатор. В противном случае необходимо создать новый идентификатор на [портале регистрации приложений Майкрософт](https://aka.ms/appregistrations). При добавлении бота используйте этот же идентификатор.

> [!NOTE]
> Если вы отправляете обновление для существующего приложения в AppSource, то нельзя изменять идентификатор в манифесте.

## <a name="developer"></a>developer

**Обязательно** — объект

Указывает сведения о вашей компании. Для приложений, отправленных в магазин Teams, эти значения должны совпадать с данными в описании в магазине. Дополнительные сведения см. в статье [правила публикации в магазине Teams](~/concepts/deploy-and-publish/appsource/publish.md).

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`name`|32 символа|✔|Отображаемое имя для разработчика.|
|`websiteUrl`|2048 символов|✔|URL-адрес веб-сайта разработчика (https://). По этой ссылке пользователи должны переходить на целевую страницу вашей компании или конкретного продукта.|
|`privacyUrl`|2048 символов|✔|URL-адрес политики конфиденциальности разработчика (https://).|
|`termsOfUseUrl`|2048 символов|✔|URL-адрес условий использования разработчика (https://).|
|`mpnId`|10 символов| |**Необязательно** — идентификатор партнерской организации, создавшей приложение, в Microsoft Partner Network.|

## <a name="name"></a>name

**Обязательно** — объект

Имя интерфейса приложения, отображаемое для пользователей в интерфейсе Teams. Для приложений, отправляемых в AppSource, эти значения должны совпадать с данными в записи AppSource. Значения `short` и `full` должны отличаться.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|30 символов|✔|Краткое отображаемое имя приложения.|
|`full`|100 символов||Полное имя приложения. Используется, если длина полного имени приложения превышает 30 символов.|

## <a name="description"></a>description

**Обязательно** — объект

Описывает приложение для пользователей. Для приложений, отправляемых в AppSource, эти значения должны совпадать с данными в записи AppSource.

Убедитесь, что описание включает возможности приложения и его назначение для потенциальных клиентов. В полном описании также необходимо указать, нужно ли использовать внешнюю учетную запись. Значения `short` и `full` должны отличаться. Краткое описание не должно повторяться в длинном описании и не должно включать имена других приложений.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|80 символов|✔|Краткое описание возможностей приложения. Используется, когда доступно ограниченное пространство.|
|`full`|4000 символов|✔|Полное описание приложения.|

## <a name="packagename"></a>packageName

**Необязательно** — строка

Уникальный идентификатор приложения в обратной нотации домена, например, com.example.myapp. Максимальная длина: 64 символа.

## <a name="localizationinfo"></a>localizationInfo

**Необязательно** — объект

Позволяет указать язык по умолчанию и содержит указатели на другие языковые файлы. Дополнительные сведения см. в разделе [Локализация](~/concepts/build-and-test/apps-localization.md).

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`defaultLanguageTag`||✔|Тег язык строк в этом файле манифеста верхнего уровня.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Массив объектов, указывающих дополнительные переводы.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`languageTag`||✔|Тег языка строк в предоставленном файле.|
|`file`||✔|Относительный путь к файлу .JSON с переведенными строками.|

## <a name="icons"></a>icons

**Обязательно** — объект

Значки, используемые в приложении Teams. Файлы значков должны быть включены в отправляемый пакет. Дополнительные сведения см. в статье [Значки](../../concepts/build-and-test/apps-package.md#app-icons).

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`outline`|32 x 32 пикселя|✔|Относительный путь к прозрачному значку контура размером 32x32 пикселя в формате PNG.|
|`color`|192 x 192 пикселя|✔|Относительный путь к полноцветному значку размером 192x192 пикселя в формате PNG.|

## <a name="accentcolor"></a>accentColor

**Обязательно** — шестнадцатеричный код цвета HTML

Цвет, который нужно использовать в качестве фона для значков контура.

Значение должно быть допустимым шестнадцатеричным кодом цвета HTML и должно начинаться с "#". Пример: `#4464ee`.

## <a name="configurabletabs"></a>configurableTabs

**Необязательно** — массив

Используется, когда в интерфейсе приложения есть интерфейс вкладки канала команды, для которого требуется дополнительная настройка перед добавлением. Настраиваемые вкладки поддерживаются только в областях `team` и `groupchat`. Одни и те же вкладки можно настраивать несколько раз. Но определить их в манифесте можно только один раз.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|string|2048 символов|✔|URL-адрес, используемый при настройке вкладки (https://).|
|`scopes`|массив элементов enum|1|✔|В настоящее время настраиваемые вкладки поддерживают только области `team` и `groupchat`. |
|`canUpdateConfiguration`|Boolean|||Значение, указывающее, может ли пользователь обновлять конфигурацию экземпляра вкладки после его создания. По умолчанию: **true**.|
|`context` |массив элементов enum|6 ||Набор областей `contextItem`, в которых [поддерживается вкладка](../../tabs/how-to/access-teams-context.md). По умолчанию: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|string|2048||Относительный путь к изображению предварительного просмотра вкладки для использования в SharePoint. Размер: 1024x768. |
|`supportedSharePointHosts`|массив элементов enum|1||Определяет, каким образом вкладка становится доступна в SharePoint. Варианты: `sharePointFullPage` и `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Необязательно** — массив

Это набор вкладок, который можно закрепить по умолчанию без добавления их вручную пользователем. Статические вкладки,объявляемые в области `personal`, всегда закрепляются в личном интерфейсе приложения. Статические вкладки,объявляемые в области `team`, сейчас не поддерживаются.

Этот элемент — массив (не более 16 элементов) со всеми элементами типа `object`. Этот блок требуется только для решений со статическими вкладками.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`entityId`|string|64 символа|✔|Уникальный идентификатор сущности, отображаемый на вкладке.|
|`name`|string|128 символов|✔|Отображаемое имя вкладки в интерфейсе канала.|
|`contentUrl`|string||✔|URL-адрес, указывающий на пользовательский интерфейс объекта для отображения на холсте Microsoft Teams (https://).|
|`websiteUrl`|string|||URL-адрес, используемый, если пользователь выбирает просмотр в браузере (https://).|
|`searchUrl`|string|||URL-адрес, используемый для поисковых запросов пользователя (https://).|
|`scopes`|массив элементов enum|1|✔|В настоящее время статические вкладки поддерживаются только для области `personal`, поэтому их можно подготовить только в личном интерфейсе.|
|`context` | массив элементов enum| 2|| Набор областей `contextItem`, в которых поддерживается вкладка.|

> [!NOTE]
> Функция searchUrl недоступна сторонним разработчикам. Если вкладкам требуется контекстно-зависимая информация для отображения соответствующего содержимого или для запуска потока проверки подлинности, см. дополнительные сведения в статье [Получение контекста для вкладок Microsoft Teams](../../tabs/how-to/access-teams-context.md).

## <a name="bots"></a>bots

**Необязательно** — массив

Определяет решение бота, а также дополнительные сведения, такие как свойства команды по умолчанию.

Этот элемент — массив (не более одного элемента&mdash;в настоящее время поддерживается только один бот на приложение) со всеми элементами типа `object`. Этот блок требуется только для решений, предоставляющих возможности бота.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|string|64 символа|✔|Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework. Этот идентификатор может совпадать с общим [идентификатором приложения](#id).|
|`scopes`|массив элементов enum|3|✔|Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или только для отдельных пользователей (`personal`). Эти параметры не являются взаимоисключающими.|
|`needsChannelSelector`|Boolean|||Описывает, использует ли бот пользовательскую подсказку для добавления бота в определенный канал. По умолчанию: **`false`**|
|`isNotificationOnly`|Boolean|||Указывает, является ли бот односторонним и только для уведомлений в отличие от бота для беседы. По умолчанию: **`false`**|
|`supportsFiles`|Boolean|||Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате. По умолчанию: **`false`**|
|`supportsCalling`|Boolean|||Значение, указывающее, поддерживает ли бот голосовые звонки. **ВАЖНО.** Это свойство в настоящее время является экспериментальным. Экспериментальные свойства могут быть неполными, а также могут быть изменены до полной доступности.  Это свойство предоставлено только для тестирования и исследования, его не следует использовать в рабочих приложениях. По умолчанию: **`false`**|
|`supportsVideo`|Boolean|||Значение, указывающее, поддерживает ли бот видеозвонки. **ВАЖНО.** Это свойство в настоящее время является экспериментальным. Экспериментальные свойства могут быть неполными, а также могут быть изменены до полной доступности.  Это свойство предоставлено только для тестирования и исследования, его не следует использовать в рабочих приложениях. По умолчанию: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Необязательный список команд, которые бот может рекомендовать пользователям. Объект — массив (не более двух элементов) со всеми элементами типа `object`; необходимо определить отдельный список команд для каждой области, поддерживаемой ботом. Дополнительные сведения см. в статье [Меню ботов](~/bots/how-to/create-a-bot-commands-menu.md).

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`items.scopes`|массив элементов enum|3|✔|Указывает область, для которой действует список команд. Доступные варианты: `team`, `personal` и `groupchat`.|
|`items.commands`|массив объектов|10 |✔|Массив команд, поддерживаемых ботом:<br>`title`: имя команды бота (строка, 32)<br>`description`: простое описание или пример синтаксиса команды и ее аргументов (строка, 128).|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|title|string|12 |✔|Имя команды бота.|
|description|string|128 символов|✔|Простое текстовое описание или пример синтаксиса команды и ее аргументов.|

## <a name="connectors"></a>connectors

**Необязательно** — массив

Блок `connectors` определяет соединитель Office 365 для приложения.

Объект — массив (не более одного элемента) со всеми элементами типа `object`. Этот блок необходим только для решений, предоставляющих соединители.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|string|2048 символов|✔|URL-адрес, используемый при настройке соединителя (https://).|
|`scopes`|массив элементов enum|1|✔|Указывает, предоставляет ли соединитель функции в контексте канала в `team` или только для отдельных пользователей (`personal`). В настоящий момент поддерживается только область `team`.|
|`connectorId`|string|64 символа|✔|Уникальный идентификатор соединителя, соответствующий его идентификатору на [информационной панели разработчиков соединителей](https://aka.ms/connectorsdashboard).|

## <a name="composeextensions"></a>composeExtensions

**Необязательно** — массив

Определяет расширение для сообщений для приложения.

> [!NOTE]
> В ноябре 2017 г. эта функция была переименована из "расширение составления" в "расширение для сообщений", но имя в манифесте остается прежним, чтобы существующие расширения не перестали работать.

Этот элемент — массив (не более одного элемента) со всеми элементами типа `object`. Этот блок необходим только для решений, которые предоставляют расширение для сообщений.

|Имя| Тип | Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|string|64|✔|Уникальный идентификатор приложения Майкрософт для бота, поддерживающего расширение для сообщений, в соответствии с регистрацией в Bot Framework. Этот идентификатор может совпадать с общим идентификатором приложения.|
|`commands`|массив объектов|10 |✔|Массив команд, поддерживаемых расширением для сообщений.|
|`canUpdateConfiguration`|Boolean|||Значение, указывающее, может ли пользователь обновлять конфигурацию расширения для сообщений. По умолчанию: **false**.|
|`messageHandlers`|массив объектов |5||Список обработчиков, которые позволяют вызывать приложение при выполнении определенных условий.|
|`messageHandlers.type`|string|||Тип обработчика сообщений. Обязательно: `"link"`.|
|`messageHandlers.value.domains`|массив строк|||Массив доменов, на которые может зарегистрироваться обработчик сообщений ссылок.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Расширение для сообщений должно объявить одну или несколько команд, но не более 10 команд. Каждая команда отображается в Microsoft Teams как потенциальное взаимодействие с точки входа на основе пользовательского интерфейса.

Каждый элемент команды представляет собой объект со следующей структурой:

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|string|64 символа|✔|ИД команды.|
|`title`|string|32 символа|✔|Понятное имя команды.|
|`type`|string|64 символа||Тип команды. Либо `query`, либо `action`. По умолчанию: **query**.|
|`description`|string|128 символов||Описание назначения команды, которое отображается для пользователей.|
|`initialRun`|Boolean|||Логическое значение, указывающее, выполняется ли команда изначально без параметров. По умолчанию: **false**.|
|`context`|массив строк|3||Определяет, откуда можно вызвать расширение сообщения. Любое сочетание `compose`, `commandBox` и `message`. Значение по умолчанию: `["compose","commandBox"]`.|
|`fetchTask`|Boolean|||Логическое значение, указывающее, нужно ли получать модуль задач динамически. По умолчанию: **false**.|
|`taskInfo`|объект|||Укажите модуль задачи для предварительной загрузки при использовании команды расширения для сообщений.|
|`taskInfo.title`|string|64 символа||Начальное название диалогового окна|
|`taskInfo.width`|string|||Ширина диалогового окна — количество пикселей или макет по умолчанию, например "large", "medium" или "small".|
|`taskInfo.height`|string|||Высота диалогового окна — количество пикселей или макет по умолчанию, например "large", "medium" или "small".|
|`taskInfo.url`|string|||Начальный URL-адрес веб-представления.|
|`parameters`|массив объекта|5 элементов|✔|Список параметров, которые принимает команда. Минимум: 1; максимум: 5.|
|`parameters.name`|string|64 символа|✔|Имя параметра в том виде, в котором оно отображается в клиенте. Имя параметра включено в запрос пользователя.|
|`parameters.title`|string|32 символа|✔|Понятное название параметра.|
|`parameters.description`|string|128 символов||Понятное описание назначения параметра.|
|`parameters.value`|string|512 символов||Начальное значение параметра. Это значение сейчас не поддерживается|
|`parameters.inputType`|string|128 символов||Определяет тип элемента управления, отображаемого в модуле задач для `fetchTask: true`. Один из `text, textarea, number, date, time, toggle, choiceset`.|
|`parameters.choices`|массив объектов|10 элементов||Варианты для `choiceset`. Используйте, только `parameter.inputType` равно `choiceset`.|
|`parameters.choices.title`|string|128 символов|✔|Название выбора.|
|`parameters.choices.value`|string|512 символов|✔|Значение выбора.|

## <a name="permissions"></a>permissions

**Необязательно** — массив строк

Массив элементов `string`, указывающий, какие разрешения запрашивает приложения, что дает возможность пользователям определить, что именно делает расширение. Следующие параметры не являются взаимоисключающими:

* `identity` &emsp; Требуются сведения удостоверения пользователя.
* `messageTeamMembers` &emsp; Требуется разрешение на отправку прямых сообщений участникам группы.

Если изменить эти разрешения при обновлении приложения, пользователям потребуется вновь согласиться на предоставление этих разрешений при запуске обновленного приложения. Подробнее см. в статье [Обновление приложения](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).

## <a name="devicepermissions"></a>devicePermissions

**Необязательно** — массив строк

Предоставляет собственные функции на устройстве пользователя, к которому приложение запрашивает доступ. Доступные варианты:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Необязательно** кроме случаев, когда указано **Обязательно**.

Список допустимых доменов для веб-сайтов, которые приложение может загружать в клиенте Teams. Списки доменов могут включать подстановочные знаки, например `*.example.com`. Допустимый домен соответствует только одному сегменту домена. Если нужно соответствие `a.b.example.com`, то используйте `*.*.example.com`. Если конфигурация вкладки или пользовательский интерфейс контента переходит на любой другой домен, отличный от конфигурации вкладки, то этот домен нужно указать здесь.

**Не** включайте домены поставщиков удостоверений, которые необходимо поддерживать в приложении. Например, чтобы проверить подлинность с помощью Google ID, требуется перенаправление на accounts.google.com, но не следует включать accounts.google.com в `validDomains[]`.

Приложения Teams, которым для правильной работы требуются собственные URL-адреса SharePoint, включают "{teamsitedomain}" в список допустимых доменов.

> [!IMPORTANT]
> Не добавляйте неподконтрольные вам домены (напрямую или с помощью подстановочных знаков). Например, `yourapp.onmicrosoft.com` — допустимое значение, а `*.onmicrosoft.com` — недопустимое.

Объект — массив со всеми элементами типа `string`.

## <a name="webapplicationinfo"></a>webApplicationInfo

**Необязательно** — объект

Укажите идентификатор приложения Azure Active Directory и сведения Microsoft Graph, чтобы помочь пользователям легко входить в приложение. Если приложение зарегистрировано в Microsoft Azure Active Directory (Azure AD), вы должны предоставить ID этого приложения. Администраторы могут проверять разрешения и предоставлять согласие в центре администрирования Teams.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|string|36 символов|✔|Идентификатор приложения в Azure Active Directory. Этот идентификатор должен быть глобальным уникальным идентификатором.|
|`resource`|string|2048 символов|✔|URL-адрес ресурса приложения для получения маркера проверки подлинности для единого входа. </br> **ПРИМЕЧАНИЕ.** Если вы не используете единый вход, убедитесь, что в это поле в манифесте приложения введена фиктивная строка, например https://notapplicable, чтобы избежать получения ошибки в качестве отклика. |

## <a name="showloadingindicator"></a>showLoadingIndicator

**Необязательно** — логическое значение

Указывает, следует ли отображать индикатор загрузки при загрузке приложения или вкладки. По умолчанию: **false**.
>[!NOTE]
>Если для `showLoadingIndicator` в манифесте приложения установлен значение "true", измените страницы содержимого на вкладках и в модулях задач, как описано в документе [Отображение собственного индикатора загрузки](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator).

## <a name="isfullscreen"></a>isFullScreen

 **Необязательно** — логическое значение

Указывает, отображается ли личное приложение с панелью заголовка вкладки. По умолчанию: **false**.

> [!NOTE]
> `isFullScreen` действует только для приложений, опубликованных в вашей организации.

## <a name="activities"></a>activities

**Необязательно** — объект

Определите свойства, которые приложение использует для публикаций в ленте новостей пользователя.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`activityTypes`|массив объектов |128 элементов| | Укажите типы действий, которые приложение может публиковать в канале новостей пользователей.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`type`|string|32 символа|✔|Тип уведомления. *См. ниже*.|
|`description`|string|128 символов|✔|Краткое описание уведомления. *См. ниже*.|
|`templateText`|string|128 символов|✔|Пример: "Пользователь {actor} создал для вас задачу {taskId}"|

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

Когда будет выбрана область установки группы, этот параметр будет определять емкость по умолчанию при установке приложения пользователем. Доступные варианты:

* `team`
* `groupchat`
* `meetings`

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`team`|string|||Если выбрана область установки `team`, в этом поле указывается доступная по умолчанию емкость. Возможные варианты: `tab`, `bot` или `connector`.|
|`groupchat`|string|||Если выбрана область установки `groupchat`, в этом поле указывается доступная по умолчанию емкость. Возможные варианты: `tab`, `bot` или `connector`.|
|`meetings`|string|||Если выбрана область установки `meetings`, в этом поле указывается доступная по умолчанию емкость. Возможные варианты: `tab`, `bot` или `connector`.|

## <a name="configurableproperties"></a>configurableProperties

**Необязательно** — массив

Блок `configurableProperties` определяет свойства приложений, доступные для настройки администраторам Teams. Дополнительные сведения см. в разделе [включение настройки приложения](~/concepts/design/enable-app-customization.md). Функция настройки приложения не поддерживается в пользовательских приложениях и в бизнес-приложениях.

> [!NOTE]
> Необходимо определить хотя бы одно свойство. В этом блоке можно определить не более 9 свойств.

Можно определить любое из следующих свойств:

* `name`: отображаемое имя приложения.
* `shortDescription`: краткое описание приложения.
* `longDescription`: длинное описание приложения.
* `smallImageUrl`: значок контура приложения.
* `largeImageUrl`: значок цвета приложения.
* `accentColor`: используемый цвет фона для значков контура.
* `developerUrl`: URL-адрес веб-сайта разработчика (HTTPS).
* `privacyUrl`: URL-адрес политики конфиденциальности разработчика (HTTPS).
* `termsOfUseUrl`: URL-адрес условий использование разработчика (HTTPS).

## <a name="defaultblockuntiladminaction"></a>defaultBlockUntilAdminAction

**Необязательно** — логическое значение

Если для свойства `defaultBlockUntilAdminAction` установлено значение **true**, приложение по умолчанию будет скрыто от пользователей, пока администратор не разрешит его. Если установлено значение **true**, приложение будет скрыто для всех клиентов и конечных пользователей. Администраторы клиента видят приложение в центре администрирования Teams и могут разрешить или заблокировать приложение. Значение по умолчанию — **false**. Дополнительные сведения о блоке приложений по умолчанию см. в статье [Скрытие приложения Teams до утверждения администратором](~/concepts/design/enable-app-customization.md#hide-teams-app-until-admin-approves).

## <a name="publisherdocsurl"></a>publisherDocsUrl

**Необязательно** — строка

**Максимальный размер** — 128 символов

`publisherDocsUrl` — URL-адрес (HTTPS) информационной страницы, на которой администраторы могут получить рекомендации перед скачиванием приложение, которое по умолчанию заблокировано. На этой странице также можно указать инструкции или сведения о приложении, полезные для администратора клиента.

## <a name="subscriptionoffer"></a>subscriptionOffer

**Необязательно** — объект

Указывает предложение SaaS, связанное с приложением.

|Имя| Тип|Максимальный размер|Обязательный|Описание|
|---|---|---|---|---|
|`offerId`| string | 2048 символов | ✔ | Уникальный идентификатор, включающий идентификатор Publisher и идентификатор предложения, которые можно найти в [Центре партнеров](https://partner.microsoft.com/dashboard). Обязательный формат строки: `publisherId.offerId`.|

## <a name="meetingextensiondefinition"></a>meetingExtensionDefinition

**Необязательно** — объект

Укажите определение расширения для собраний. Дополнительные сведения см. в статье [Настраиваемые сцены режима "Вместе" в Teams](../../apps-in-teams-meetings/teams-together-mode.md).

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`scenes`|массив объектов| 5 элементов||Сцены, поддерживаемые собранием.|

### <a name="meetingextensiondefinitionscenes"></a>meetingExtensionDefinition.scenes

|Имя| Тип|Максимальный размер|Обязательный |Описание|
|---|---|---|---|---|
|`id`|||✔| Уникальный идентификатор сцены. Этот идентификатор должен быть глобальным уникальным идентификатором. |
|`name`| string | 128 символов |✔| Имя сцены. |
|`file`|||✔| Относительный путь к файлу JSON метаданных сцен. |
|`preview`|||✔| Относительный путь к файлу значка предварительного просмотра PNG сцен. |
|`maxAudience`| integer | 50  |✔| Максимальное количество аудиторий, поддерживаемых в сцене. |
|`seatsReservedForOrganizersOrPresenters`| integer | 50 |✔| Количество мест, зарезервированных для организаторов или докладчиков.|

## <a name="authorization"></a>авторизация

**Необязательно** — объект

> [!NOTE]
> Если свойству `manifestVersion` присвоено значение **1.12**, свойство авторизации несовместимо с более ранними версиями манифеста. Авторизация поддерживается для манифеста версии 1.12.

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
|`type`|string||✔| Тип разрешения для конкретного ресурса. Возможные варианты: `Application` и `Delegated`.|
|`name`|string|128 символов|✔|Имя разрешения для определенного ресурса. Дополнительные сведения см. в разделе [Разрешения приложений для конкретных ресурсов](#resource-specific-application-permissions) и [Делегированные разрешения для конкретных ресурсов](#resource-specific-delegated-permissions)|

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

* **Делегированные разрешения на использование конкретных ресурсов для чатов или собраний**

    |**Имя**|**Описание**|
    |---|---|
    |`InAppPurchase.Allow.Chat`|Позволяет приложению отображать предложения в Marketplace в этом чате и связанных собраниях и совершать покупки в приложении от имени выполнившего вход пользователя.|
    |`MeetingStage.Write.Chat`|Позволяет приложению отображать содержимое на этапе собрания в собраниях, связанных с этим чатом, от имени выполнившего вход пользователя.|
    |`OnlineMeetingParticipant.Read.Chat`|Позволяет приложению читать сведения об участниках, включая имя, роль, идентификатор, время присоединения и ухода, собрания, связанные с этим чатом, от имени выполнившего вход пользователя.|
    |`OnlineMeetingParticipant.ToggleIncomingAudio.Chat`|Позволяет приложению переключать входящий звук для участников собраний, связанных с этим чатом, от имени выполнившего вход пользователя.|

* **Делегированные разрешения на использование конкретных ресурсов для пользователей**

    |**Имя**|**Описание**|
    |---|---|
    |`InAppPurchase.Allow.User`|Позволяет приложению отображать предложения в Marketplace и совершать покупки в приложении от имени выполнившего вход пользователя.|

## <a name="see-also"></a>См. также

* [Понимание структуры приложений Microsoft Teams](~/concepts/design/app-structure.md)
* [Разрешение настройки приложения](~/concepts/design/enable-app-customization.md)
* [Локализация приложения](~/concepts/build-and-test/apps-localization.md)
* [Интеграция возможностей мультимедиа](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Схема манифеста предварительной общедоступной версии для разработчиков для Microsoft Teams](manifest-schema-dev-preview.md)
