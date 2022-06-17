---
title: Справочник по схеме манифеста общедоступной предварительной версии для разработчиков
description: Изучите пример файла манифеста и описание всех его компонентов, которые поддерживаются Microsoft Teams.
ms.topic: reference
ms.localizationpriority: medium
ms.date: 11/15/2021
ms.openlocfilehash: deaf094ab18ddd2ebe70ea9594f41c108398bf32
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142739"
---
# <a name="reference-public-developer-preview-manifest-schema-for-microsoft-teams"></a>Ссылка: схема манифеста общедоступной предварительной версии для разработчиков для Microsoft Teams

Как включить предварительную версию для разработчиков, см. в статье [Общедоступная предварительная версия для разработчиков для Microsoft Teams.](~/resources/dev-preview/developer-preview-intro.md).

> [!NOTE]
> Если вы не используете функции предварительного просмотра для разработчиков, в том числе запуск [личных вкладок Teams и расширения для обмена сообщениями в Outlook и Office](../../m365-apps/overview.md), используйте вместо этого [манифест приложения для функций GA](~/resources/schema/manifest-schema.md).

Манифест Microsoft Teams описывает, как приложение интегрируется с платформой Microsoft Teams. Манифест должен соответствовать схеме, размещенной по адресу [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).

## <a name="sample-full-manifest"></a>Пример полного манифеста

```json
{
    "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion": "devPreview",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "packageName": "com.example.myapp",
    "devicePermissions": [
        "geolocation",
        "media"
    ],
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
            "scopes": [
                "team",
                "groupchat"
            ]"context": []
        }
    ],
    "staticTabs": [
        {
            "entityId": "idForPage",
            "name": "Display name of tab",
            "contentUrl": "https://contoso.com/content?host=msteams",
            "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
            "websiteUrl": "https://contoso.com/content",
            "scopes": [
                "personal"
            ]
        }
    ],
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "needsChannelSelector": false,
            "isNotificationOnly": false,
            "scopes": [
                "team",
                "personal",
                "groupchat"
            ],
            "supportsFiles": true,
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
                            "title": "Command N",
                            "description": "Description of Command N"
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
            "configurationUrl": "https://contoso.com/teamsconnector/configure",
            "scopes": [
                "team"
            ]
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
                    "type": "search",
                    "context": [
                        "compose",
                        "commandBox"
                    ],
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
                    "type": "action",
                    "fetchTask": true,
                    "context": [
                        "message"
                    ],
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
                    "id": "exampleMessageHandler",
                    "title": "Message Handler",
                    "description": "Domains that will create a preview when pasted into the compose box",
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
            ]
        }
    ],
    "permissions": [
        "identity",
        "messageTeamMembers"
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
    },
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

*Необязательная, но рекомендуемая* &ndash; Строка

`https://` URL-адрес, ссылающийся на схему JSON для манифеста.

## <a name="manifestversion"></a>manifestVersion

**Обязательная** &ndash; Строка

Версия схемы манифеста, используемая этим манифестом.

## <a name="version"></a>version

**Обязательная** &ndash; Строка

Версия конкретного приложения. При обновлении чего-либо в манифесте необходимо также увеличить версию. Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции. Если это приложение было отправлено в магазин, новый манифест необходимо будет повторно отправить и проверить повторно. Затем пользователи этого приложения автоматически получают обновленный манифест через несколько часов после его утверждения.

Если разрешения, запрошенные приложением, изменятся, пользователям будет предложено обновить и возобновить свое согласие на использование приложения.

Строка версии должна соответствовать стандарту [semver](http://semver.org/)(ОСНОВНАЯ_ВЕРСИЯ.ДОПОЛНИТЕЛЬНАЯ_ВЕРСИЯ.ИСПРАВЛЕНИЕ).

## <a name="id"></a>id

**Обязательный** &ndash;идентификатор приложения Майкрософт

Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения. Если вы зарегистрировали бот через Microsoft Bot Framework или веб-приложение вашей вкладки уже входит в систему в корпорации Майкрософт, у вас уже должен быть идентификатор, который необходимо ввести здесь. В противном случае необходимо создать новый идентификатор на портале регистрации [приложений (мои](https://apps.dev.microsoft.com) приложения), ввести его здесь, а затем повторно использовать при добавлении [бота](~/bots/how-to/create-a-bot-for-teams.md).

## <a name="packagename"></a>packageName

**Обязательная** &ndash; Строка

Уникальный идентификатор этого приложения в обратной нотации домена; например, com.example.myapp.

## <a name="developer"></a>developer

Обязательно:

Указывает сведения о вашей компании. Для приложений, отправленных в AppSource (ранее Office Store), эти значения должны соответствовать данным в вашей записи AppSource.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`name`|32 символа|✔️|Отображаемое имя для разработчика.|
|`websiteUrl`|2048 символов|✔️|URL-адрес веб-сайта разработчика (https://). Эта ссылка должна вести пользователей на целевую страницу вашей компании или продукта.|
|`privacyUrl`|2048 символов|✔️|URL-адрес политики конфиденциальности разработчика (https://).|
|`termsOfUseUrl`|2048 символов|✔️|URL-адрес условий использования разработчика (https://).|
|`mpnId`|10 символов|✔️|**Необязательно** — идентификатор партнерской организации, создавшей приложение, в Microsoft Partner Network.|

## <a name="localizationinfo"></a>localizationInfo

Необязательно:

Разрешает спецификацию языка по умолчанию и указатели на дополнительные языковые файлы. См.[Локализация](~/concepts/build-and-test/apps-localization.md)

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`defaultLanguageTag`|4 символа|✔️|Языковой тег строк в этом файле манифеста верхнего уровня.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Массив объектов, указывающих дополнительные языковые переводы.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`languageTag`|4 символа|✔️|Тег языка строк в предоставленном файле.|
|`file`|4 символа|✔️|Относительный путь к файлу .JSON с переведенными строками.|

## <a name="name"></a>name

Обязательно:

Имя интерфейса приложения, отображаемое для пользователей в интерфейсе Teams. Для приложений, отправляемых в AppSource, эти значения должны совпадать с данными в записи AppSource. Значения и не `short` `full` должны совпадать.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|30 символов|✔️|Краткое отображаемое имя приложения.|
|`full`|100 символов||Полное имя приложения. Используется, если длина полного имени приложения превышает 30 символов.|

## <a name="description"></a>description

Обязательно:

Описывает приложение для пользователей. Для приложений, отправляемых в AppSource, эти значения должны совпадать с данными в записи AppSource.

Убедитесь, что ваше описание в точности соответствует вашей функции и предоставляет сведения, которые помогут потенциальным клиентам понять, что эта функция делает. В полном описании также необходимо указать, требуется ли для использования внешняя учетная запись. Значения и не `short` `full` должны совпадать.  Ваше краткое описание не должно дублироваться в длинном описании и не должно включать какое-либо другое название приложения.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`short`|80 символов|✔️|Краткое описание возможностей приложения. Используется, когда доступно ограниченное пространство.|
|`full`|4000 символов|✔️|Полное описание приложения.|

## <a name="icons"></a>icons

Обязательно:

Значки, используемые в приложении Teams. Файлы значков должны быть включены в отправляемый пакет.

|Имя| Максимальный размер | Обязательный | Описание|
|---|---|---|---|
|`outline`|2048 символов|✔️|Относительный путь к прозрачному значку контура размером 32x32 пикселя в формате PNG.|
|`color`|2048 символов|✔️|Относительный путь к полноцветному значку размером 192x192 пикселя в формате PNG.|

## <a name="accentcolor"></a>accentColor

**Обязательная** &ndash; Строка

Цвет, используемый в качестве фона для значков структуры.

Значение должно быть допустимым шестнадцатеричным кодом цвета HTML и должно начинаться с "#". Пример: `#4464ee`.

## <a name="configurabletabs"></a>configurableTabs

Необязательно:

Используется, когда в интерфейсе приложения есть вкладка канала группы, которая требует дополнительной настройки перед добавлением. Настраиваемые вкладки поддерживаются только в области Teams, и сейчас поддерживается только одна вкладка для каждого приложения.

Объект — массив со всеми элементами типа `object`. Этот блок требуется только для решений, предоставляющих решение с настраиваемой вкладкой канала.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|String|2048 символов|✔️|URL-адрес, используемый при настройке вкладки (https://).|
|`canUpdateConfiguration`|Boolean|||Значение, указывающее, может ли экземпляр конфигурации вкладки быть обновлен пользователем после создания. По умолчанию: `true`.|
|`scopes`|Массив перечислений|1|✔️|В настоящее время настраиваемые вкладки поддерживают только области `team` и `groupchat`. |
|`context` |массив элементов enum|6 ||Набор областей `contextItem`, в которых [поддерживается вкладка](../../tabs/how-to/access-teams-context.md). По умолчанию: `channelTab`, `privateChatTab`, `meetingChatTab`, `meetingDetailsTab`, `meetingSidePanel` и `meetingStage`.|
|`sharePointPreviewImage`|String|2048||Относительный путь к изображению предварительного просмотра вкладки для использования в SharePoint. Размер: 1024x768. |
|`supportedSharePointHosts`|Массив перечислений|1||Определяет, каким образом вкладка становится доступна в SharePoint. Варианты: `sharePointFullPage` и `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

Необязательно:

Это набор вкладок, который можно закрепить по умолчанию без добавления их вручную пользователем. Статические вкладки,объявляемые в области `personal`, всегда закрепляются в личном интерфейсе приложения. Статические вкладки,объявляемые в области `team`, сейчас не поддерживаются.

Преобразовать для просмотра вкладки с помощью адаптивных карточек, указав`contentBotId` вместо этого`contentUrl` блок **staticTabs**

Объект является массивом (не более 16 элементов) со всеми элементами типа.`object`. Этот блок требуется только для решений со статическими вкладками.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`entityId`|Строка|64 символа|✔️|Уникальный идентификатор сущности, отображаемый на вкладке.|
|`name`|String|128 символов|✔️|Отображаемое имя вкладки в интерфейсе канала.|
|`contentUrl`|String|2048 символов|✔️|URL-адрес, указывающий на пользовательский интерфейс объекта для отображения на холсте Microsoft Teams (https://).|
|`contentBotId`|   | | | Идентификатор приложения Microsoft Teams, указанный для бота на портале Bot Framework. |
|`websiteUrl`|String|2048 символов||URL-адрес https:// для указания при выборе просмотра в браузере.|
|`scopes`|Массив перечислений|1|✔️|В настоящее время статические вкладки поддерживаются только для области `personal`, поэтому их можно подготовить только в личном интерфейсе.|

## <a name="bots"></a>bots

Необязательно:

Определяет решение бота, а также дополнительные сведения, такие как свойства команды по умолчанию.

Объект является массивом (не более 1 элемента&mdash;, сейчас разрешен только один бот для каждого приложения) со всеми элементами типа `object`. Этот блок требуется только для решений, предоставляющих возможности бота.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|Строка|64 символа|✔️|Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework. Это вполне может совпадать с общим [идентификатором приложения](#id).|
|`needsChannelSelector`|Логическое|||Описывает, использует ли бот подсказку пользователя для добавления бота на определенный канал. По умолчанию:`false`|
|`isNotificationOnly`|Логическое|||Указывает, является ли бот односторонним и только для уведомлений в отличие от бота для беседы. По умолчанию: `false`|
|`supportsFiles`|Boolean|||Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате. По умолчанию: `false`|
|`scopes`|Массив перечислений|3|✔️|Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или только для отдельных пользователей (`personal`). Эти параметры не являются взаимоисключающими.|

### <a name="botscommandlists"></a>bots.commandLists

Необязательный список команд, которые бот может рекомендовать пользователям. Объект является массивом (не более 2 элементов) со всеми элементами типа `object`; вы должны определить отдельный список команд для каждой области, которую поддерживает ваш бот. Подробнее см. в статье [Меню ботов](~/bots/how-to/create-a-bot-commands-menu.md).

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`items.scopes`|массив перечислений|3|✔️|Указывает область, для которой действует список команд. Доступные варианты: `team`, `personal` и `groupchat`.|
|`items.commands`|массив объектов|10|✔️|Массив команд, поддерживаемых ботом:<br>`title`: имя команды бота (строка, 32).<br>`description`: простое описание или пример синтаксиса команды и ее аргументов (строка, 128).|

## <a name="connectors"></a>connectors

Необязательно:

Блок `connectors` определяет соединитель Office 365 для приложения.

Объект является массивом (не более 1 элемента), и все элементы относятся к типу `object`. Этот блок необходим только для решений, предоставляющих соединители.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`configurationUrl`|String|2048 символов|✔️|URL-адрес, используемый при настройке соединителя (https://).|
|`connectorId`|String|64 символа|✔️|Уникальный идентификатор соединителя, соответствующий его идентификатору на [информационной панели разработчиков соединителей](https://aka.ms/connectorsdashboard).|
|`scopes`|Массив перечислений|1|✔️|Указывает, предоставляет ли соединитель функции в контексте канала в `team` или только для отдельных пользователей (`personal`). В настоящий момент поддерживается только область `team`.|

## <a name="composeextensions"></a>composeExtensions

Необязательно:

Определяет расширение для обмена сообщениями для приложения.

> [!NOTE]
> Название функции было изменено с ''расширение для составления сообщений'' на ''расширение для обмена сообщениями'' в ноябре 2017 г., но имя в манифесте осталось прежним, чтобы существующие расширения продолжали работать.

Объект является массивом (не более 1 элемента), и все элементы относятся к типу `object`. Этот блок необходим только для решений, предоставляющих расширение для сообщений.

|Имя| Тип | Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`botId`|String|64|✔️|Уникальный идентификатор приложения Microsoft для бота, поддерживающего расширение для обмена сообщениями, в соответствии с регистрацией в Bot Framework. Это вполне может совпадать с общим [идентификатором приложения](#id).|
|`canUpdateConfiguration`|Логическое|||Значение, указывающее, может ли пользователь обновлять конфигурацию расширения сообщения. Значение по умолчанию:`false`.|
|`commands`|Массив объекта|10|✔️|Массив команд, поддерживаемых расширением для обмена сообщениями.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Ваше расширение для обмена сообщениями должно объявлять одну или несколько команд. Каждая команда отображается в Microsoft Teams как потенциальное взаимодействие с точки входа на основе пользовательского интерфейса. Существует не более 10 команд.

Каждый элемент команды представляет собой объект со следующей структурой:

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|Строка|64 символа|✔️|ИД команды.|
|`type`|String|64 символа||Тип команды. Либо `query`, либо `action`. По умолчанию: `query`|
|`title`|String|32 символа|✔️|Понятное имя команды.|
|`description`|String|128 символов||Описание назначения команды, которое отображается для пользователей.|
|`initialRun`|Boolean|||Логическое значение, указывающее, следует ли изначально запускать команду без параметров. По умолчанию: `false`|
|`context`|Массив строк|3||Определяет, откуда можно вызвать расширение сообщения. Любое сочетание `compose`, `commandBox`, `message`. Значение по умолчанию: `["compose", "commandBox"]`|
|`fetchTask`|Логическое|||Логическое значение, указывающее, следует ли динамически извлекать модуль задачи.|
|`taskInfo`|Объект|||Укажите модуль задачи для предварительной загрузки при использовании команды расширения для обмена сообщениями.|
|`taskInfo.title`|String|64||Начальное название диалогового окна|
|`taskInfo.width`|String|||Ширина диалогового окна — количество пикселей или макет по умолчанию, например "large", "medium" или "small".|
|`taskInfo.height`|String|||Высота диалогового окна — количество пикселей или макет по умолчанию, например "large", "medium" или "small".|
|`taskInfo.url`|String|||Начальный URL-адрес веб-представления.|
|`messageHandlers`|Массив объектов|5||Список обработчиков, которые позволяют вызывать приложения при выполнении определенных условий. Домены также должны быть указаны в`validDomains`.|
|`messageHandlers.type`|String|||Тип обработчика сообщений. Обязательно: `"link"`.|
|`messageHandlers.value.domains`|Массив строк|||Массив доменов, на которые может зарегистрироваться обработчик сообщений ссылок.|
|`parameters`|Массив объекта|5|✔️|Список параметров, которые принимает команда. Минимум: 1; максимум: 5.|
|`parameter.name`|String|64 символа|✔️|Имя параметра в том виде, в котором оно отображается в клиенте. Это включено в запрос пользователя.|
|`parameter.title`|String|32 символа|✔️|Понятное название параметра.|
|`parameter.description`|String|128 символов||Понятное описание назначения параметра.|
|`parameter.inputType`|String|128 символов||Определяет тип элемента управления, отображаемого в модуле задач для `fetchTask: true`. Один из `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.|
|`parameter.choices`|Массив объектов|10||Варианты выбора для`choiceset`. Используйте только если `parameter.inputType` является `choiceset`.|
|`parameter.choices.title`|String|128||Название выбора.|
|`parameter.choices.value`|String|512||Значение выбора.|

## <a name="permissions"></a>permissions

Необязательно:

Массив, указывающий `string`разрешения, запрашиваемые приложением, которые позволяют конечным пользователям знать, как будет выполняться расширение. Следующие параметры не являются взаимоисключающими:

* `identity` &emsp; Требуются сведения удостоверения пользователя.
* `messageTeamMembers` &emsp; Требуется разрешение на отправку прямых сообщений участникам группы.

Изменение этих разрешений при обновлении вашего приложения потребует от ваших пользователей повторного предоставления этих разрешений при запуске обновленного приложения.

## <a name="devicepermissions"></a>devicePermissions

**Необязательный** Массив строк

Определяет собственные функции на устройстве пользователя, к которым ваше приложение может запросить доступ. Варианты:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Необязательно**, за исключением **Обязательно** где указано

Список допустимых доменов, с которых приложение ожидает загрузки содержимого. Списки доменов могут включать подстановочные знаки, например `*.example.com`. Это соответствует ровно одному сегменту домена. Если вам нужно сопоставить, `a.b.example.com`, используйте `*.*.example.com`. Если конфигурация вкладок или пользовательский интерфейс содержимого должны перейти к любому другому домену, кроме того, который используется для конфигурации вкладок, этот домен должен быть указан здесь.

Однако **нет** необходимости включать домены поставщиков удостоверений, которые вы хотите поддерживать в своем приложении. Например, для проверки подлинности с помощью идентификатора Google необходимо перенаправить accounts.google.com, но не следует включать accounts.google.com.`validDomains[]`

> [!IMPORTANT]
> Не добавляйте неподконтрольные вам домены ни напрямую, ни с помощью подстановочных знаков. Например, `yourapp.onmicrosoft.com` допустимо, а `*.onmicrosoft.com` не допускается.

Объект — массив со всеми элементами типа `string`.

## <a name="webapplicationinfo"></a>webApplicationInfo

Необязательно:

Укажите Microsoft Azure Active Directory (Azure AD) приложения и Graph, чтобы пользователи могли легко входить в Azure AD приложения.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`id`|String|36 символов|✔️|Идентификатор приложения в Microsoft Azure Active Directory (Azure AD). Этот идентификатор должен быть глобальным уникальным идентификатором.|
|`resource`|String|2048 символов|✔️|URL-адрес ресурса приложения для получения токена аутентификации для единого входа.|
|`applicationPermissions`|Array|Не более 100 элементов|✔️|Разрешения ресурсов для приложения.|

## <a name="graphconnector"></a>graphConnector

**Необязательно** — объект

Укажите конфигурацию соединителя Graph приложения. Если он присутствует, то [webApplicationInfo.id](#webapplicationinfo) также необходимо указать.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`notificationUrl`|string|2048 символов|✔️|URL-адрес, по которому должны отправляться уведомления Graph-соединителя для приложения.|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Необязательно** — логическое значение

Указывает, следует ли отображать индикатор загрузки при загрузке приложения или вкладки. Значение по умолчанию: **false**.
> [!NOTE]
> Если для `showLoadingIndicator` в манифесте приложения установлен значение "true", измените страницы содержимого на вкладках и в модулях задач, как описано в документе [Отображение собственного индикатора загрузки](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator).

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
|`type`|string|32 символа|✔️|Тип уведомления. *См. ниже*.|
|`description`|string|128 символов|✔️|Краткое описание уведомления. *См. ниже*.|
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

## <a name="configurableproperties"></a>configurableProperties

**Необязательно** — массив

Блок `configurableProperties` определяет свойства приложений, доступные для настройки администраторам Teams. Дополнительные сведения см. в разделе [включение настройки приложения](~/concepts/design/enable-app-customization.md).

> [!NOTE]
> Необходимо определить хотя бы одно свойство. В этом блоке можно определить не более 9 свойств.

Можно определить любое из следующих свойств:

* `name`: отображаемое имя приложения.
* `shortDescription`: краткое описание приложения.
* `longDescription`: подробное описание приложения.
* `smallImageUrl`: значок контура приложения.
* `largeImageUrl`: значок цвета приложения.
* `accentColor`: цвет, используемый в качестве фона для значков структуры.
* `developerUrl`: URL-адрес веб-сайта разработчика (HTTPS).
* `privacyUrl`: URL-адрес политики конфиденциальности разработчика (HTTPS).
* `termsOfUseUrl`: URL-адрес условий использование разработчика (HTTPS).

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

## <a name="subscriptionoffer"></a>subscriptionOffer

**Необязательно** — объект

Указывает предложение SaaS, связанное с приложением.

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`offerId`| string | 2048 символов | ✔️ | Уникальный идентификатор, включающий идентификатор Publisher и идентификатор предложения, которые можно найти в [Центре партнеров](https://partner.microsoft.com/dashboard). Обязательный формат строки: `publisherId.offerId`.|

## <a name="meetingextensiondefinition"></a>meetingExtensionDefinition

**Необязательно** — объект

Укажите определение расширения для собраний. Дополнительные сведения см. в статье [Настраиваемые сцены режима "Вместе" в Teams](../../apps-in-teams-meetings/teams-together-mode.md).

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`scenes`|массив объектов| 5 элементов||Сцены, поддерживаемые собранием.|

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
|`type`|string||✔️| Тип разрешения для конкретного ресурса. Возможные варианты: `Application` и `Delegated`.|
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

* **Разрешения для конкретных ресурсов для Teams общей папки**

   |Имя| Описание |
   | ----- | ----- |
   |`LiveShareSession.ReadWrite.Chat`|<!--- need info --->|
   |`LiveShareSession.ReadWrite.Channel`|<!--- need info --->|
   |`MeetingStage.Write.Chat`|<!--- need info --->|
   |`OnlineMeetingIncomingAudio.Detect.Chat`|<!--- need info --->|

## <a name="see-also"></a>См. также

* [Понимание структуры приложений Microsoft Teams](~/concepts/design/app-structure.md)
* [Разрешение настройки приложения](~/concepts/design/enable-app-customization.md)
* [Локализация приложения](~/concepts/build-and-test/apps-localization.md)
* [Интеграция возможностей мультимедиа](~/concepts/device-capabilities/media-capabilities.md)
