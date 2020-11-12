---
title: Поиск с расширениями обмена сообщениями
description: Описание разработки расширений для обмена сообщениями на основе поиска
keywords: службы расширения обмена сообщениями Teams.
ms.date: 07/20/2019
ms.openlocfilehash: f46548d2e7e03ecebd8bc0fb6685aeb82b8eec6e
ms.sourcegitcommit: 0aeb60027f423d8ceff3b377db8c3efbb6da4d17
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/11/2020
ms.locfileid: "48998002"
---
# <a name="search-with-messaging-extensions"></a>Поиск с расширениями обмена сообщениями

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Расширения обмена сообщениями на основе поиска позволяют запросить службу и отправить эти сведения в виде карточки, прямо в сообщение.

![Пример карточки расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

В следующих разделах описано, как это сделать.

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a>Расширения сообщений для типа поиска

Для расширения системы обмена сообщениями на основе поиска задайте `type` для параметра значение `query` . Ниже приведен пример манифеста с одной командой поиска. Одно расширение обмена сообщениями может иметь до 10 различных команд, связанных с ней. Сюда могут входить как несколько команд поиска, так и несколько команд, основанных на действиях.

#### <a name="complete-app-manifest-example"></a>Пример полного манифеста приложения

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.bing",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://bingbotservice.azurewebsites.net/",
    "privacyUrl": "http://bingbotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://bingbotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "Bing",
    "full": "Bing"
  },
  "description": {
    "short": "Find Bing search results",
    "full": "Find Bing search results and share them with your team members."
  },
  "icons": {
    "outline": "bing-outline.jpg",
    "color": "bing-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "bingbotservice.azurewebsites.net",
    "*.bingbotservice.azurewebsites.net"
  ]
}
```

### <a name="test-via-uploading"></a>Тестирование через отправку

Вы можете проверить расширение системы обмена сообщениями, отправив свое приложение.

Чтобы открыть расширение системы обмена сообщениями, перейдите к любому из бесед или каналов. Нажмите кнопку **Дополнительные параметры** ( **&#8943;** ) в поле создать и выберите ваш добавочный номер для обмена сообщениями.

## <a name="add-event-handlers"></a>Добавление обработчиков событий

Большая часть работы включает `onQuery` событие, которое обрабатывает все взаимодействия в окне расширения системы обмена сообщениями.

Если вы задаете значение `canUpdateConfiguration` `true` в манифесте, вы включаете элемент меню **Параметры** для расширения системы обмена сообщениями, а также обрабатывает `onQuerySettingsUrl` и `onSettingsUpdate` .

### <a name="handle-onquery-events"></a>Обработка событий onquery

Расширение системы обмена сообщениями получает `onQuery` событие, когда что-то происходит в окне расширения обмена сообщениями или отправляется в окно.

Если расширение системы обмена сообщениями использует страницу конфигурации, обработчик `onQuery` должен сначала проверить наличие сохраненных сведений о конфигурации; если расширение системы обмена сообщениями не настроено, возвращайте `config` ответ со ссылкой на страницу конфигурации. Помните, что ответ на странице конфигурации также обрабатывается `onQuery` . (Единственное исключение — при вызове страницы конфигурации обработчиком `onQuerySettingsUrl` ; в следующем разделе.)

Если для расширения системы обмена сообщениями требуется проверка подлинности, проверьте сведения о состоянии пользователя; Если пользователь не вошел в систему, следуйте инструкциям в разделе [authentication (проверка подлинности](#authentication) ) далее в этом разделе.

Затем проверьте, `initialRun` установлено ли значение; если это так, выполните соответствующие действия, такие как предоставление инструкций или списка ответов.

В оставшейся части обработчика `onQuery` запрашивается информация для пользователя, отображается список карточек предварительного просмотра и возвращается карточка, выбранная пользователем.

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>Обработка событий Онкуерисеттингсурл и Онсеттингсупдате

`onQuerySettingsUrl`События and `onSettingsUpdate` работают вместе, чтобы включить элемент меню **Параметры** .

![Снимки экрана расположения элемента меню параметров](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

Обработчик `onQuerySettingsUrl` возвращает URL-адрес страницы конфигурации; после закрытия страницы конфигурации обработчик `onSettingsUpdate` принимает и сохраняет возвращенное состояние. (Это тот случай, когда `onQuery` *не* получает ответ на страницу настройки.)

## <a name="receive-and-respond-to-queries"></a>Получение запросов и реагирование на них

Каждый запрос к своему расширению обмена сообщениями выполняется через `Activity` объект, который отправляется на URL-адрес обратного вызова. Запрос содержит сведения о команде User, такие как идентификатор и значения параметров. В запросе также предоставляются метаданные о контексте, в котором был вызван ваш добавочный номер, включая ИДЕНТИФИКАТОРы пользователей и клиентов, а также ИДЕНТИФИКАТОРы и идентификаторы каналов и групп.

### <a name="receive-user-requests"></a>Получение запросов пользователей

Когда пользователь выполняет запрос, Microsoft Teams отправляет службу стандартным объектом Bot Framework `Activity` . Служба должна выполнять свою логику для параметра `Activity` , для которого `type` установлено `invoke` значение `name` поддерживаемого `composeExtension` типа, как показано в следующей таблице.

В дополнение к стандартным свойствам действия Bot полезные данные содержат следующие метаданные запроса:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса; должно быть `invoke` . |
|`name`| Тип команды, выданной службе. В настоящее время поддерживаются следующие типы: <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| Идентификатор пользователя, отправившего запрос. |
|`from.name`| Имя пользователя, отправившего запрос. |
|`from.aadObjectId`| Идентификатор объекта Azure Active Directory пользователя, отправившего запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| Идентификатор канала (если запрос был сделан в канале). |
|`channelData.team.id`| Идентификатор группы (если запрос был сделан в канале). |
|`clientInfo`|Необязательные метаданные о клиентском программном обеспечении, используемом для отправки сообщения пользователя. Сущность может содержать два свойства:<br>В этом `country` поле содержится обнаруженное пользователем расположение.<br>`platform`Поле описывает клиентскую платформу обмена сообщениями. <br>Дополнительную информацию можно *узнать* в статье [типы не-IRI, клиентинфо](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).|

Собственно параметры запроса находятся в объекте value, который включает следующие свойства:

| Имя свойства | Назначение |
|---|---|
| `commandId` | Имя команды, вызываемой пользователем, которая соответствует одной из команд, объявленных в манифесте приложения. |
| `parameters` | Массив параметров. Каждый объект Parameter содержит имя параметра вместе со значением параметра, предоставленным пользователем. |
| `queryOptions` | Параметры разбивки на страницы: <br>`skip`: количество пропусков для этого запроса <br>`count`: число возвращаемых элементов |

#### <a name="request-example"></a>Пример запроса

```json
{
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  "type": "invoke",
  "timestamp": "2017-05-01T15:45:51.876Z",
  "localTimestamp": "2017-05-01T08:45:51.876-07:00",
  "id": "f:622749630322482883",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
    "name": "Larry Jin",
    "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
  },
  "conversation": {
    "id": "19:skypespaces_8198cfe0dd2647ae91930f0974768a40@thread.skype"
  },
  "recipient": {
    "id": "28:b4922ea1-5315-4fd0-9b21-d941ab06e39f",
    "name": "TheComposeExtensionDev"
  },
  "entities": [
    {
    "type": "clientInfo",
      "country": "US",
      "platform": "Windows"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>Получение запросов от ссылок, вставленных в окно сообщения создания

В качестве альтернативы (или дополнительно) для поиска во внешней службе можно использовать URL-адрес, вставленный в поле создать сообщение, чтобы отправить запрос в службу и возвратить карточку. На снимке экрана после вставки пользователя в URL-адрес рабочего элемента в Azure DevOps, который разрешал расширение обмена сообщениями в карточке.

![Пример ссылки унфурлинг](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

Чтобы разрешить своему расширению обмена сообщениями взаимодействовать с ссылками таким способом, сначала необходимо добавить `messageHandlers` массив в манифест приложения, как показано в примере ниже:

```json
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
]
```

Добавив домен для прослушивания манифеста приложения, вам потребуется изменить код ленты, чтобы [ответить](#respond-to-user-requests) на следующий запрос Invoke.

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Если ваше приложение возвращает несколько элементов, будет использоваться только первый.

### <a name="respond-to-user-requests"></a>Ответ на запросы пользователей

Когда пользователь выполняет запрос, Microsoft Teams отправляет службе синхронный HTTP-запрос. В этот момент код имеет 5 секунд, чтобы предоставить HTTP-ответ на запрос. В течение этого времени служба может выполнять дополнительные операции поиска или любую другую бизнес-логику, необходимую для обслуживания запроса.

Служба должна отвечать на результаты, соответствующие запросу пользователя. Ответ должен указывать код состояния HTTP `200 OK` и допустимый объект Application/JSON следующего основного текста:

|Имя свойства|Назначение|
|---|---|
|`composeExtension`|Конверт отклика верхнего уровня.|
|`composeExtension.type`|Тип ответа. Поддерживаются следующие типы: <br>`result`: отображает список результатов поиска <br>`auth`: запрос на проверку подлинности пользователя <br>`config`: запрашивает у пользователя установку расширения для обмена сообщениями <br>`message`: отображается обычное текстовое сообщение |
|`composeExtension.attachmentLayout`|Задает макет вложений. Используется для ответов типа `result` . <br>В настоящее время поддерживаются следующие типы: <br>`list`: список объектов карточек, содержащих поля эскиза, заголовка и текста. <br>`grid`: сетка эскизов изображений |
|`composeExtension.attachments`|Массив допустимых объектов вложений. Используется для ответов типа `result` . <br>В настоящее время поддерживаются следующие типы: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Предложенные действия. Используется для ответов типа `auth` или `config` . |
|`composeExtension.text`|Сообщение для отображения. Используется для ответов типа `message` . |

#### <a name="response-card-types-and-previews"></a>Типы карточек ответа и предварительный просмотр

Поддерживаются следующие типы вложений:

* [Карточка эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карточка главный Имиджевый баннер](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Соединительная карта Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карта](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Общие сведения приведены в [карточки](~/task-modules-and-cards/what-are-cards.md) .

Сведения о том, как использовать типы карт эскизов и главный Имиджевый баннер, приведены в разделе [Add cards and Card Actions](~/task-modules-and-cards/cards/cards-actions.md).

Дополнительную документацию по карте соединителей Office 365 можно узнать в статье [Использование соединителей карт office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

Список результатов отображается в пользовательском интерфейсе Microsoft Teams с предварительным просмотром каждого элемента. Предварительный просмотр создается одним из двух способов:

* Использование `preview` свойства в `attachment` объекте. `preview`Вложение может быть только картой главный Имиджевый баннер или эскиза.
* Извлекается из базового `title` `text` `image` Свойства и свойства вложения. Они используются только в том случае, если `preview` свойство не задано, а эти свойства доступны.

Вы можете просмотреть предварительный просмотр адаптивной карты или карты Office 365 в списке результатов, просто задав свойство Preview; Это не требуется, если результаты уже главный Имиджевый баннер или эскизы страниц. Если вы используете предварительный просмотр вложения, это должна быть карта главный Имиджевый баннер или эскиза. Если свойство Preview не указано, предварительный просмотр карты завершается с ошибками, и ничего не отображается.

#### <a name="response-example"></a>Пример ответа

В этом примере показан ответ с двумя результатами, смешивание разных форматов карт: Office 365 Connector и адаптивный. Хотя вы, скорее всего, захотите прикрепить к одному формату карточки в своем ответе, он показывает, как `preview` свойство каждого элемента в `attachments` коллекции должно явно определять предварительный просмотр в формате главный Имиджевый баннер или эскиза, как описано выше.

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

### <a name="default-query"></a>Запрос по умолчанию

Если `initialRun` для манифеста задано значение `true` в манифесте, Microsoft Teams по умолчанию выдает запрос "по умолчанию", когда пользователь впервые открывает расширение системы обмена сообщениями. Служба может ответить на этот запрос с помощью набора предварительно заполненных результатов. Это может быть полезно для отображения, например, недавно просмотренных элементов, избранного или любой другой информации, которая не зависит от вводимых пользователем данных.

Запрос по умолчанию имеет ту же структуру, что и любой запрос обычного пользователя, за исключением параметра `initialRun` , строковое значение которого равно `true` .

#### <a name="request-example-for-a-default-query"></a>Пример запроса для запроса по умолчанию

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="identify-the-user"></a>Идентификация пользователя

Каждый запрос к службам включает в себя идентификатор пользователя, который выполнил запрос, а также отображаемое имя пользователя и идентификатор объекта Azure Active Directory.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

`id` `aadObjectId` Гарантируется, что значения и значения для пользователя Teams прошли проверку подлинности. Они могут использоваться в качестве ключей для поиска учетных данных или любого кэшированного состояния в службе. Кроме того, каждый запрос содержит идентификатор клиента Azure Active Directory для пользователя, который можно использовать для определения организации пользователя. Если это возможно, запрос также содержит идентификаторы команд и каналов, из которых поступил запрос.

## <a name="authentication"></a>Проверка подлинности

Если для вашей службы требуется проверка подлинности пользователя, необходимо войти в систему, прежде чем ее сможет использовать расширение системы обмена сообщениями. Если вы написали робот или вкладку, которые подписываются пользователю, этот раздел должен быть знаком.

Последовательность выглядит следующим образом:

1. Пользователь выдает запрос, или запрос по умолчанию автоматически отправляется в службу.
2. Служба проверяет, прошел ли пользователь проверку подлинности, проверив идентификатор пользователя Teams.
3. Если пользователь не прошел проверку подлинности, отправьте `auth` ответ с `openUrl` предложенным действием, включая URL-адрес проверки подлинности.
4. Клиент Microsoft Teams запускает всплывающее окно, в котором размещается веб-страница, используя указанный URL-адрес проверки подлинности.
5. После входа пользователя необходимо закрыть окно и отправить ему код проверки подлинности в клиент Teams.
6. Затем клиент Teams повторно отправляет запрос в службу, который включает код проверки подлинности, переданный на шаге 5.

Ваша служба должна проверить, что код проверки подлинности, полученный на шаге 6, соответствует тому, что получено на шаге 5. Это гарантирует, что злоумышленник не будет пытаться подменить или ослабить процесс входа в систему. Это фактически "закрывает цикл" для завершения безопасной последовательности проверки подлинности.

### <a name="respond-with-a-sign-in-action"></a>Ответ с действием входа

Чтобы выдать запрос пользователю, не прошедшему проверку подлинности, выполните ответ с предложенным действием типа `openUrl` , которое включает URL-адрес проверки подлинности.

#### <a name="response-example-for-a-sign-in-action"></a>Пример отклика для действия при входе

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
> Для того чтобы при входе в систему можно было размещаться в всплывающем окне Teams, в списке допустимых доменов приложения должен находиться домен, являющийся частью URL-адреса. (См. раздел [валиддомаинс](~/resources/schema/manifest-schema.md#validdomains) в схеме манифеста.)

### <a name="start-the-sign-in-flow"></a>Запуск процесса входа

Ваш интерфейс пользователя должен отвечать на запросы и размещаться в всплывающем окне. Он должен интегрироваться с [клиентским пакетом SDK для Microsoft Teams JavaScript](/javascript/api/overview/msteams-client), который использует передачу сообщений.

Как и другие встроенные возможности, выполняемые в Microsoft Teams, код в окне должен вызываться первым `microsoftTeams.initialize()` . Если ваш код выполняет процесс OAuth, можно передать идентификатор пользователя Teams в ваше окно, которое затем может передать его в URL-адрес входа OAuth.

### <a name="complete-the-sign-in-flow"></a>Завершение процесса входа

Когда запрос на вход завершается и перенаправляется обратно на страницу, он должен выполнить следующие действия:

1. Создайте код безопасности. (Это может быть случайное число.) Необходимо кэшировать этот код в службе, а также учетные данные, полученные с помощью процесса входа (например, OAuth 2,0 tokens).
2. Позвоните `microsoftTeams.authentication.notifySuccess` и передайте код безопасности.

На этом шаге окно закрывается и управление передается клиенту Teams. Теперь клиент может повторно отправить исходный запрос пользователя, а также код безопасности в `state` свойстве. Код может использовать код безопасности для поиска ранее сохраненных учетных данных, чтобы выполнить последовательность проверки подлинности, а затем выполнить запрос пользователя.

#### <a name="reissued-request-example"></a>Пример повторной выданной заявки

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "type": "clientInfo",
        "country": "US",
        "platform": "Web",
        
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="sdk-support"></a>Поддержка SDK

### <a name="net"></a>.NET

Для получения и обработки запросов с помощью пакета SDK построителя построителя для .NET можно проверить `invoke` тип действия для входящего действия и затем использовать вспомогательный метод в пакете NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) , чтобы определить, является ли он действием расширения системы обмена сообщениями.

#### <a name="example-code-in-net"></a>Пример кода в .NET

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
    if (activity.Type == ActivityTypes.Invoke) // Received an invoke
    {
        if (activity.IsComposeExtensionQuery())
        {
            // This is the response object that will get sent back to the messaging extension request.
            ComposeExtensionResponse invokeResponse = null;

            // This helper method gets the query as an object.
            var query = activity.GetComposeExtensionQueryData();

            if (query.CommandId != null && query.Parameters != null && query.Parameters.Count > 0)
            {
                // query.Parameters has the parameters sent by client
                var results = new ComposeExtensionResult()
                {
                    AttachmentLayout = "list",
                    Type = "result",
                    Attachments = new List<ComposeExtensionAttachment>(),
                };
                invokeResponse.ComposeExtension = results;
            }

            // Return the response
            return Request.CreateResponse<ComposeExtensionResponse>(HttpStatusCode.OK, invokeResponse);
        } else
        {
            // Handle other types of Invoke activities here.
        }
    } else {
      // Failure case catch-all.
      var response = Request.CreateResponse(HttpStatusCode.BadRequest);
      response.Content = new StringContent("Invalid request! This API supports only messaging extension requests. Check your query and try again");
      return response;
    }
}
```

### <a name="nodejs"></a>Node.js

#### <a name="example-code-in-nodejs"></a>Пример кода в Node.js

```javascript
require('dotenv').config();

import * as restify from 'restify';
import * as builder from 'botbuilder';
import * as teamBuilder from 'botbuilder-teams';

class App {
    run() {
        const server = restify.createServer();
        let teamChatConnector = new teamBuilder.TeamsChatConnector({
            appId: process.env.MICROSOFT_APP_ID,
            appPassword: process.env.MICROSOFT_APP_PASSWORD
        });

        // Command ID must match what's defined in manifest
        teamChatConnector.onQuery('<%= commandId %>',
            (event: builder.IEvent,
            query: teamBuilder.ComposeExtensionQuery,
            callback: (err: Error, result: teamBuilder.IComposeExtensionResponse, statusCode: number) => void) => {
                // Check for initialRun; i.e., when you should return default results
                // if (query.parameters[0].name === 'initialRun') {}

                // Check query.queryOptions.count and query.queryOptions.skip for paging

                // Return auth response
                // let response = teamBuilder.ComposeExtensionResponse.auth().actions([
                //     builder.CardAction.openUrl(null, 'https://authUrl', 'Please sign in')
                // ]).toResponse();

                // Return config response
                // let response = teamBuilder.ComposeExtensionResponse.config().actions([
                //     builder.CardAction.openUrl(null, 'https://configUrl', 'Please sign in')
                // ]).toResponse();

                // Return result response
                let response = teamBuilder.ComposeExtensionResponse.result('list').attachments([
                    new builder.ThumbnailCard()
                        .title('Test thumbnail card')
                        .text('This is a test thumbnail card')
                        .images([new builder.CardImage().url('https://bot-framework.azureedge.net/bot-icons-v1/bot-framework-default-9.png')])
                        .toAttachment()
                ]).toResponse();
                callback(null, response, 200);
            });
        server.post('/api/composeExtension', teamChatConnector.listen());
        server.listen(process.env.PORT, () => console.log(`listening to port:` + process.env.PORT));
    }
}

const app = new App();
app.run();
```
В этой статье *также приведены* [примеры кода Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
