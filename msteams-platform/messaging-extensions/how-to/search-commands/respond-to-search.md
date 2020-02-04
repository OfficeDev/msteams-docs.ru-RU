---
title: Команда "ответить на Поиск"
author: clearab
description: Ответ на команду поиска из расширения обмена сообщениями в приложении Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: e8b40dd8f422ffbd2537e8fa76a38c15eb6208de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675664"
---
# <a name="respond-to-the-search-command"></a>Ответ на команду поиска

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Веб-служба получает сообщение о `composeExtension/query` вызове, которое содержит `value` объект с параметрами поиска. Этот вызов инициируется следующим образом:

* По мере ввода символов в поле поиска.
* Если `initialRun` для манифеста приложения задано значение true, вы получите сообщение Invoke сразу же после вызова команды поиска. Просмотр [запроса по умолчанию](#default-query).

Собственно параметры запроса находятся в `value` объекте в запросе, который включает следующие свойства:

| Имя свойства | Назначение |
|---|---|
| `commandId` | Имя команды, вызываемой пользователем, которая соответствует одной из команд, объявленных в манифесте приложения. |
| `parameters` | Массив параметров. Каждый объект Parameter содержит имя параметра вместе со значением параметра, предоставленным пользователем. |
| `queryOptions` | Параметры разбивки на страницы: <br>`skip`: количество пропусков для этого запроса <br>`count`: число возвращаемых элементов |

# <a name="cnettabdotnet"></a>[ЯЗЫК C#/.НЕТ](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/Node. js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

Приведенный ниже код JSON сокращен для выделения наиболее релевантных разделов.

```json
{
  "type": "invoke",
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
...
}
```

* * *

## <a name="respond-to-user-requests"></a>Ответ на запросы пользователей

Когда пользователь выполняет запрос, Microsoft Teams отправляет службе синхронный HTTP-запрос. В этот момент код имеет 5 секунд, чтобы предоставить HTTP-ответ на запрос. В течение этого времени служба может выполнять дополнительные операции поиска или любую другую бизнес-логику, необходимую для обслуживания запроса.

Служба должна отвечать на результаты, соответствующие запросу пользователя. Ответ должен указывать код состояния HTTP `200 OK` и допустимый объект Application/JSON следующего основного текста:

|Имя свойства|Назначение|
|---|---|
|`composeExtension`|Конверт отклика верхнего уровня.|
|`composeExtension.type`|Тип ответа. Поддерживаются следующие типы: <br>`result`: отображает список результатов поиска <br>`auth`: запрос на проверку подлинности пользователя <br>`config`: запрашивает у пользователя установку расширения для обмена сообщениями <br>`message`: отображается обычное текстовое сообщение |
|`composeExtension.attachmentLayout`|Задает макет вложений. Используется для ответов типа `result`. <br>В настоящее время поддерживаются следующие типы: <br>`list`: список объектов карточек, содержащих поля эскиза, заголовка и текста. <br>`grid`: сетка эскизов изображений |
|`composeExtension.attachments`|Массив допустимых объектов вложений. Используется для ответов типа `result`. <br>В настоящее время поддерживаются следующие типы: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Предложенные действия. Используется для ответов типа `auth` или. `config` |
|`composeExtension.text`|Сообщение для отображения. Используется для ответов типа `message`. |

### <a name="response-card-types-and-previews"></a>Типы карточек ответа и предварительный просмотр

Поддерживаются следующие типы вложений:

* [Карточка эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карточка главный Имиджевый баннер](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Соединительная карта Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карта](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Посмотрите [, что представляют собой карточки](~/task-modules-and-cards/what-are-cards.md) для обзора.

Сведения о том, как использовать типы карт эскизов и главный Имиджевый баннер, приведены в разделе [Add cards and Card Actions](~/task-modules-and-cards/cards/cards-actions.md).

Дополнительную документацию по карте соединителей Office 365 можно узнать в статье [Использование соединителей карт office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

Список результатов отображается в пользовательском интерфейсе Microsoft Teams с предварительным просмотром каждого элемента. Предварительный просмотр создается одним из двух способов:

* Использование `preview` свойства в `attachment` объекте. `preview` Вложение может быть только картой главный Имиджевый баннер или эскиза.
* Извлекается из базового `title` `text`свойства и `image` свойства вложения. Они используются только в `preview` том случае, если свойство не задано, а эти свойства доступны.

Вы можете отобразить предварительный просмотр адаптивной карточки или карты соединителя Office 365 в списке результатов просто с помощью его свойства Preview. Это не требуется, если результаты уже главный Имиджевый баннер или эскизы страниц. Если вы используете предварительный просмотр вложения, это должна быть карта главный Имиджевый баннер или эскиза. Если свойство Preview не указано, предварительный просмотр карты завершается с ошибками, и ничего не отображается.

### <a name="response-example"></a>Пример ответа

# <a name="cnettabdotnet"></a>[ЯЗЫК C#/.НЕТ](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken) 
{
  var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

  //searches NuGet for a package
  var obj = JObject.Parse(await (new HttpClient()).GetStringAsync($"https://azuresearch-usnc.nuget.org/query?q=id:{text}&prerelease=true"));
  var packages = obj["data"].Select(item => (item["id"].ToString(), item["version"].ToString(), item["description"].ToString()));

  // We take every row of the results and wrap them in cards wrapped in in MessagingExtensionAttachment objects.
  // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
  var attachments = packages.Select(package => new MessagingExtensionAttachment
      {
          ContentType = HeroCard.ContentType,
          Content = new HeroCard { Title = package.Item1 },
          Preview = new HeroCard { Title = package.Item1, Tap = new CardAction { Type = "invoke", Value = package } }.ToAttachment()
      })
      .ToList();

  // The list of MessagingExtensionAttachments must we wrapped in a MessagingExtensionResult wrapped in a MessagingExtensionResponse.
  return new MessagingExtensionResponse
  {
      ComposeExtension = new MessagingExtensionResult
      {
          Type = "result",
          AttachmentLayout = "list",
          Attachments = attachments
      }
  };
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/Node. js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearchBot extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;
        const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);

        const attachments = [];
        response.data.objects.forEach(obj => {
            const heroCard = CardFactory.heroCard(obj.package.name);
            const preview = CardFactory.heroCard(obj.package.name);
            const attachment = { ...heroCard, preview };
            attachments.push(attachment);
        });

        return {
            composeExtension: {
                type: 'result',
                attachmentLayout: 'list',
                attachments: attachments
            }
        };
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

* * *

## <a name="default-query"></a>Запрос по умолчанию

Если для `initialRun` `true` манифеста задано значение в манифесте, Microsoft Teams по умолчанию выдает запрос "по умолчанию", когда пользователь впервые открывает расширение системы обмена сообщениями. Служба может ответить на этот запрос с помощью набора предварительно заполненных результатов. Это может быть полезно, если для команды поиска требуется проверка подлинности или Настройка, отображение недавно просмотренных элементов, избранного или любой другой информации, не зависящей от вводимых пользователем данных.

Запрос по умолчанию имеет ту же структуру, что и любой обычный запрос пользователя `name` , и `initialRun` `value` `true` для поля задано значение, равное приведенному ниже объекту.

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

## <a name="next-steps"></a>Дальнейшие действия

Добавление проверки подлинности и/или конфигурации

* [Добавление проверки подлинности к расширению системы обмена сообщениями](~/messaging-extensions/how-to/add-authentication.md)
* [Добавление конфигурации к расширению обмена сообщениями](~/messaging-extensions/how-to/add-configuration-page.md)

Развертывание конфигурации

* [Развертывание пакета приложений](~/concepts/deploy-and-publish/apps-upload.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
