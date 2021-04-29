---
title: Ответ на команду поиска
author: clearab
description: Как реагировать на команду поиска из расширения обмена сообщениями в приложении Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 76bccc10763b99d7373e98e6e153c4f4aa51373a
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075635"
---
# <a name="respond-to-search-command"></a>Ответ на команду поиска

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

После отправки команды поиска веб-служба получает сообщение об вызове, содержащем объект `composeExtension/query` `value` с параметрами поиска. Этот вызов запускается при следующих условиях:

* Как символы вписались в поле поиска.
* `initialRun` установлено, что в манифесте приложения вы получите сообщение вызова, как только будет вызвана команда поиска. Дополнительные сведения см. в [запросе по умолчанию.](#default-query)

В этом документе вы можете узнать, как реагировать на запросы пользователей в виде карт и предварительных просмотров, а также условия, при которых Microsoft Teams выдает запрос по умолчанию.

Параметры запроса находятся в объекте в запросе, который включает `value` следующие свойства:

| Имя свойства | Назначение |
|---|---|
| `commandId` | Имя команды, вызываемой пользователем, совпадает с одной из команд, объявленных в манифесте приложения. |
| `parameters` | Массив параметров. Каждый объект параметра содержит имя параметра, а также значение параметра, предоставленное пользователем. |
| `queryOptions` | Параметры pagination: <br>`skip`: Пропустить количество для этого запроса <br>`count`: Количество возвращаемого элемента. |

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

Ниже JSON сокращается, чтобы выделить наиболее релевантные разделы.

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

## <a name="respond-to-user-requests"></a>Ответы на запросы пользователей

Когда пользователь выполняет запрос, Microsoft Teams выдает синхронный http-запрос в службу. В этот момент у кода есть `5` секунды, чтобы предоставить http-ответ на запрос. За это время служба может выполнять дополнительный просмотр или любую другую бизнес-логику, необходимую для обслуживания запроса.

Служба должна отвечать результатами, совпадающие с запросом пользователя. Ответ должен указывать код состояния HTTP и допустимый объект приложения или JSON со `200 OK` следующими свойствами:

|Имя свойства|Назначение|
|---|---|
|`composeExtension`|Конверт ответа верхнего уровня.|
|`composeExtension.type`|Тип ответа. Поддерживаются следующие типы: <br>`result`: Отображает список результатов поиска <br>`auth`: Просит пользователя проверить подлинность <br>`config`: Просит пользователя настроить расширение обмена сообщениями <br>`message`: Отображает простое текстовое сообщение |
|`composeExtension.attachmentLayout`|Указывает макет вложений. Используется для ответов типа `result` . <br>В настоящее время поддерживаются следующие типы: <br>`list`: Список объектов карт, содержащих эскизы, заголовки и текстовые поля <br>`grid`: Сетка изображений эскизов |
|`composeExtension.attachments`|Массив допустимых объектов вложений. Используется для ответов типа `result` . <br>В настоящее время поддерживаются следующие типы: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Предлагаемые действия. Используется для ответов типа `auth` или `config` . |
|`composeExtension.text`|Отображение сообщения. Используется для ответов типа `message` . |

### <a name="response-card-types-and-previews"></a>Типы и предварительные просмотры карт отклика

Teams поддерживает следующие типы карт:

* [Карта эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карта hero](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Соединитечная карта Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карта](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Чтобы лучше понимать карты и их обзор, см. в этом [обзоре.](~/task-modules-and-cards/what-are-cards.md)

Чтобы узнать, как использовать эскизы и типы карт героев, см. в добавлении [карт и действий карт.](~/task-modules-and-cards/cards/cards-actions.md)

Дополнительные сведения о карточке Соединители Office 365 см. в руб. [Использование карт соединители Office 365.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)

Список результатов отображается в пользовательском интерфейсе Microsoft Teams с предварительным просмотром каждого элемента. Предварительный просмотр создается одним из двух способов:

* Использование `preview` свойства в `attachment` объекте. Вложение `preview` может быть только карточкой Hero или Thumbnail.
* Извлечено из основных свойств и `title` `text` свойств `image` вложения. Они используются только в том случае, если свойство не установлено и `preview` эти свойства доступны.
* Кнопка карточки Hero или Thumbnail и действия касания, за исключением вызова, не поддерживаются в карточке предварительного просмотра.

Вы можете отобразить предварительный просмотр адаптивной карты или соединителя Office 365 в списке результатов с помощью свойства предварительного просмотра. Свойство предварительного просмотра не требуется, если результаты уже являются картами Hero или Thumbnail. Если вы используете вложение предварительного просмотра, оно должно быть либо карточкой Hero, либо Thumbnail. Если не указано свойство предварительного просмотра, предварительный просмотр карты не удается, и ничего не отображается.

### <a name="response-example"></a>Пример ответа

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

# <a name="json"></a>[JSON](#tab/json)

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
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
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

Если вы `initialRun` заданы в манифесте, Microsoft Teams выдает запрос по умолчанию при первом открываемом пользователем `true` расширении обмена сообщениями.  Служба может отвечать на этот запрос набором предварительно заполненных результатов. Это полезно, когда команда поиска требует проверки подлинности или конфигурации, отображая недавно просмотримые элементы, избранное или любую другую информацию, которая не зависит от ввода пользователя.

Запрос по умолчанию имеет ту же структуру, что и любой обычный запрос пользователя, при этом поле заказано и заказано, как показано `name` `initialRun` в следующем `value` `true` объекте:

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

## <a name="code-sample"></a>Пример кода

| Имя образца           | Описание | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Действие расширения обмена сообщениями teams| Описывает, как определить команды действий, создать модуль задач и реагировать на отправку действия модуля задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Командный поиск расширения обмена сообщениями   |  Описывает, как определить команды поиска и реагировать на поиски.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a>См. также

[Добавление конфигурации в расширение обмена сообщениями](~/messaging-extensions/how-to/add-configuration-page.md)
 
## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Добавление проверки подлинности в расширение обмена сообщениями](~/messaging-extensions/how-to/add-authentication.md)



