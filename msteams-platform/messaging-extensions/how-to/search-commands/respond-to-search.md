---
title: Ответ на команду поиска
author: clearab
description: Как реагировать на команду поиска из расширения обмена сообщениями в приложении Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 2cc53796deddb47e8dbce86a5b02f4d80a1b91e0
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696194"
---
# <a name="respond-to-search-command"></a><span data-ttu-id="1d3bf-103">Ответ на команду поиска</span><span class="sxs-lookup"><span data-stu-id="1d3bf-103">Respond to search command</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="1d3bf-104">После отправки команды поиска веб-служба получает сообщение об вызове, содержащем объект `composeExtension/query` `value` с параметрами поиска.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-104">After the user submits the search command, your web service receives a `composeExtension/query` invoke message that contains a `value` object with the search parameters.</span></span> <span data-ttu-id="1d3bf-105">Этот вызов запускается при следующих условиях:</span><span class="sxs-lookup"><span data-stu-id="1d3bf-105">This invoke is triggered with the following conditions:</span></span>

* <span data-ttu-id="1d3bf-106">Как символы вписались в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-106">As characters are entered into the search box.</span></span>
* <span data-ttu-id="1d3bf-107">`initialRun` установлено, что в манифесте приложения вы получите сообщение вызова, как только будет вызвана команда поиска.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-107">`initialRun` is set to true in your app manifest, you receive the invoke message as soon as the search command is invoked.</span></span> <span data-ttu-id="1d3bf-108">Дополнительные сведения см. в [запросе по умолчанию.](#default-query)</span><span class="sxs-lookup"><span data-stu-id="1d3bf-108">For more information, see [default query](#default-query).</span></span>

<span data-ttu-id="1d3bf-109">В этом документе вы можете узнать, как реагировать на запросы пользователей в виде карт и предварительных просмотров, а также условия, при которых Microsoft Teams выдает запрос по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-109">This document guides you on how to respond to user requests in the form of cards and previews, and the conditions under which Microsoft Teams issues a default query.</span></span>

<span data-ttu-id="1d3bf-110">Параметры запроса находятся в объекте в запросе, который включает `value` следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="1d3bf-110">The request parameters are found in the `value` object in the request, which includes the following properties:</span></span>

| <span data-ttu-id="1d3bf-111">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="1d3bf-111">Property name</span></span> | <span data-ttu-id="1d3bf-112">Назначение</span><span class="sxs-lookup"><span data-stu-id="1d3bf-112">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="1d3bf-113">Имя команды, вызываемой пользователем, совпадает с одной из команд, объявленных в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-113">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="1d3bf-114">Массив параметров.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-114">Array of parameters.</span></span> <span data-ttu-id="1d3bf-115">Каждый объект параметра содержит имя параметра, а также значение параметра, предоставленное пользователем.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-115">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="1d3bf-116">Параметры pagination:</span><span class="sxs-lookup"><span data-stu-id="1d3bf-116">Pagination parameters:</span></span> <br><span data-ttu-id="1d3bf-117">`skip`: Пропустить количество для этого запроса</span><span class="sxs-lookup"><span data-stu-id="1d3bf-117">`skip`: Skip count for this query</span></span> <br><span data-ttu-id="1d3bf-118">`count`: Количество возвращаемого элемента.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-118">`count`: Number of elements to return.</span></span> |

# <a name="cnet"></a>[<span data-ttu-id="1d3bf-119">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="1d3bf-119">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="1d3bf-120">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1d3bf-120">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="json"></a>[<span data-ttu-id="1d3bf-121">JSON</span><span class="sxs-lookup"><span data-stu-id="1d3bf-121">JSON</span></span>](#tab/json)

<span data-ttu-id="1d3bf-122">Ниже JSON сокращается, чтобы выделить наиболее релевантные разделы.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-122">The JSON below is shortened to highlight the most relevant sections.</span></span>

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

## <a name="respond-to-user-requests"></a><span data-ttu-id="1d3bf-123">Ответы на запросы пользователей</span><span class="sxs-lookup"><span data-stu-id="1d3bf-123">Respond to user requests</span></span>

<span data-ttu-id="1d3bf-124">Когда пользователь выполняет запрос, Microsoft Teams выдает синхронный http-запрос в службу.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-124">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="1d3bf-125">В этот момент у кода есть `5` секунды, чтобы предоставить http-ответ на запрос.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-125">At that point, your code has `5` seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="1d3bf-126">За это время служба может выполнять дополнительный просмотр или любую другую бизнес-логику, необходимую для обслуживания запроса.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-126">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="1d3bf-127">Служба должна отвечать результатами, совпадающие с запросом пользователя.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-127">Your service must respond with the results matching the user query.</span></span> <span data-ttu-id="1d3bf-128">Ответ должен указывать код состояния HTTP и допустимый объект приложения или JSON со `200 OK` следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="1d3bf-128">The response must indicate an HTTP status code of `200 OK` and a valid application or JSON object with the following properties:</span></span>

|<span data-ttu-id="1d3bf-129">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="1d3bf-129">Property name</span></span>|<span data-ttu-id="1d3bf-130">Назначение</span><span class="sxs-lookup"><span data-stu-id="1d3bf-130">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="1d3bf-131">Конверт ответа верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-131">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="1d3bf-132">Тип ответа.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-132">Type of response.</span></span> <span data-ttu-id="1d3bf-133">Поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="1d3bf-133">The following types are supported:</span></span> <br><span data-ttu-id="1d3bf-134">`result`: Отображает список результатов поиска</span><span class="sxs-lookup"><span data-stu-id="1d3bf-134">`result`: Displays a list of search results</span></span> <br><span data-ttu-id="1d3bf-135">`auth`: Просит пользователя проверить подлинность</span><span class="sxs-lookup"><span data-stu-id="1d3bf-135">`auth`: Asks the user to authenticate</span></span> <br><span data-ttu-id="1d3bf-136">`config`: Просит пользователя настроить расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="1d3bf-136">`config`: Asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="1d3bf-137">`message`: Отображает простое текстовое сообщение</span><span class="sxs-lookup"><span data-stu-id="1d3bf-137">`message`: Displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="1d3bf-138">Указывает макет вложений.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-138">Specifies the layout of the attachments.</span></span> <span data-ttu-id="1d3bf-139">Используется для ответов типа `result` .</span><span class="sxs-lookup"><span data-stu-id="1d3bf-139">Used for responses of type `result`.</span></span> <br><span data-ttu-id="1d3bf-140">В настоящее время поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="1d3bf-140">Currently, the following types are supported:</span></span> <br><span data-ttu-id="1d3bf-141">`list`: Список объектов карт, содержащих эскизы, заголовки и текстовые поля</span><span class="sxs-lookup"><span data-stu-id="1d3bf-141">`list`: A list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="1d3bf-142">`grid`: Сетка изображений эскизов</span><span class="sxs-lookup"><span data-stu-id="1d3bf-142">`grid`: A grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="1d3bf-143">Массив допустимых объектов вложений.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-143">Array of valid attachment objects.</span></span> <span data-ttu-id="1d3bf-144">Используется для ответов типа `result` .</span><span class="sxs-lookup"><span data-stu-id="1d3bf-144">Used for responses of type `result`.</span></span> <br><span data-ttu-id="1d3bf-145">В настоящее время поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="1d3bf-145">Currently, the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="1d3bf-146">Предлагаемые действия.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-146">Suggested actions.</span></span> <span data-ttu-id="1d3bf-147">Используется для ответов типа `auth` или `config` .</span><span class="sxs-lookup"><span data-stu-id="1d3bf-147">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="1d3bf-148">Отображение сообщения.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-148">Message to display.</span></span> <span data-ttu-id="1d3bf-149">Используется для ответов типа `message` .</span><span class="sxs-lookup"><span data-stu-id="1d3bf-149">Used for responses of type `message`.</span></span> |

### <a name="response-card-types-and-previews"></a><span data-ttu-id="1d3bf-150">Типы и предварительные просмотры карт отклика</span><span class="sxs-lookup"><span data-stu-id="1d3bf-150">Response card types and previews</span></span>

<span data-ttu-id="1d3bf-151">Teams поддерживает следующие типы карт:</span><span class="sxs-lookup"><span data-stu-id="1d3bf-151">Teams supports the following card types:</span></span>

* [<span data-ttu-id="1d3bf-152">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="1d3bf-152">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="1d3bf-153">Карта hero</span><span class="sxs-lookup"><span data-stu-id="1d3bf-153">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="1d3bf-154">Соединитечная карта Office 365</span><span class="sxs-lookup"><span data-stu-id="1d3bf-154">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="1d3bf-155">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="1d3bf-155">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="1d3bf-156">Чтобы лучше понимать карты и их обзор, см. в этом [обзоре.](~/task-modules-and-cards/what-are-cards.md)</span><span class="sxs-lookup"><span data-stu-id="1d3bf-156">To have a better understanding and overview on cards, see [what are cards](~/task-modules-and-cards/what-are-cards.md).</span></span>

<span data-ttu-id="1d3bf-157">Чтобы узнать, как использовать эскизы и типы карт героев, см. в добавлении [карт и действий карт.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="1d3bf-157">To learn how to use the thumbnail and hero card types, see [add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="1d3bf-158">Дополнительные сведения о карточке Соединители Office 365 см. в руб. [Использование карт соединители Office 365.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="1d3bf-158">For additional information regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="1d3bf-159">Список результатов отображается в пользовательском интерфейсе Microsoft Teams с предварительным просмотром каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-159">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="1d3bf-160">Предварительный просмотр создается одним из двух способов:</span><span class="sxs-lookup"><span data-stu-id="1d3bf-160">The preview is generated in one of the two ways:</span></span>

* <span data-ttu-id="1d3bf-161">Использование `preview` свойства в `attachment` объекте.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-161">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="1d3bf-162">Вложение `preview` может быть только карточкой Hero или Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-162">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="1d3bf-163">Извлечено из основных свойств и `title` `text` свойств `image` вложения.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-163">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="1d3bf-164">Они используются только в том случае, если свойство не установлено и `preview` эти свойства доступны.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-164">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="1d3bf-165">Вы можете отобразить предварительный просмотр адаптивной карты или соединителя Office 365 в списке результатов с помощью свойства предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-165">You can display a preview of an Adaptive Card or Office 365 Connector card in the result list using its preview property.</span></span> <span data-ttu-id="1d3bf-166">Свойство предварительного просмотра не требуется, если результаты уже являются картами Hero или Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-166">The preview property is not necessary if the results are already Hero or Thumbnail cards.</span></span> <span data-ttu-id="1d3bf-167">Если вы используете вложение предварительного просмотра, оно должно быть либо карточкой Hero, либо Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-167">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="1d3bf-168">Если не указано свойство предварительного просмотра, предварительный просмотр карты не удается, и ничего не отображается.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-168">If no preview property is specified, the preview of the card fails and nothing is displayed.</span></span>

### <a name="response-example"></a><span data-ttu-id="1d3bf-169">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="1d3bf-169">Response example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="1d3bf-170">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="1d3bf-170">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="1d3bf-171">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1d3bf-171">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1d3bf-172">JSON</span><span class="sxs-lookup"><span data-stu-id="1d3bf-172">JSON</span></span>](#tab/json)

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

## <a name="default-query"></a><span data-ttu-id="1d3bf-173">Запрос по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1d3bf-173">Default query</span></span>

<span data-ttu-id="1d3bf-174">Если вы `initialRun` заданы в манифесте, Microsoft Teams выдает запрос по умолчанию при первом открываемом пользователем `true` расширении обмена сообщениями. </span><span class="sxs-lookup"><span data-stu-id="1d3bf-174">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a **default** query when the user first opens the messaging extension.</span></span> <span data-ttu-id="1d3bf-175">Служба может отвечать на этот запрос набором предварительно заполненных результатов.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-175">Your service can respond to this query with a set of pre-populated results.</span></span> <span data-ttu-id="1d3bf-176">Это полезно, когда команда поиска требует проверки подлинности или конфигурации, отображая недавно просмотримые элементы, избранное или любую другую информацию, которая не зависит от ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-176">This is useful when your search command requires authentication or configuration, displaying recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="1d3bf-177">Запрос по умолчанию имеет ту же структуру, что и любой обычный запрос пользователя, при этом поле заказано и заказано, как показано `name` `initialRun` в следующем `value` `true` объекте:</span><span class="sxs-lookup"><span data-stu-id="1d3bf-177">The default query has the same structure as any regular user query, with the `name` field set to `initialRun` and `value` set to `true` as shown in the following object:</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="1d3bf-178">Пример кода</span><span class="sxs-lookup"><span data-stu-id="1d3bf-178">Code sample</span></span>

| <span data-ttu-id="1d3bf-179">Имя образца</span><span class="sxs-lookup"><span data-stu-id="1d3bf-179">Sample Name</span></span>           | <span data-ttu-id="1d3bf-180">Описание</span><span class="sxs-lookup"><span data-stu-id="1d3bf-180">Description</span></span> | <span data-ttu-id="1d3bf-181">.NET</span><span class="sxs-lookup"><span data-stu-id="1d3bf-181">.NET</span></span>    | <span data-ttu-id="1d3bf-182">Node.js</span><span class="sxs-lookup"><span data-stu-id="1d3bf-182">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="1d3bf-183">Действие расширения обмена сообщениями teams</span><span class="sxs-lookup"><span data-stu-id="1d3bf-183">Teams messaging extension action</span></span>| <span data-ttu-id="1d3bf-184">Описывает, как определить команды действий, создать модуль задач и реагировать на отправку действия модуля задач.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-184">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="1d3bf-185">View</span><span class="sxs-lookup"><span data-stu-id="1d3bf-185">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="1d3bf-186">View</span><span class="sxs-lookup"><span data-stu-id="1d3bf-186">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="1d3bf-187">Командный поиск расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="1d3bf-187">Teams messaging extension search</span></span>   |  <span data-ttu-id="1d3bf-188">Описывает, как определить команды поиска и реагировать на поиски.</span><span class="sxs-lookup"><span data-stu-id="1d3bf-188">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="1d3bf-189">View</span><span class="sxs-lookup"><span data-stu-id="1d3bf-189">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="1d3bf-190">View</span><span class="sxs-lookup"><span data-stu-id="1d3bf-190">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a><span data-ttu-id="1d3bf-191">См. также</span><span class="sxs-lookup"><span data-stu-id="1d3bf-191">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1d3bf-192">Добавление конфигурации в расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="1d3bf-192">Add configuration to a messaging extension</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)
 
## <a name="next-step"></a><span data-ttu-id="1d3bf-193">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="1d3bf-193">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1d3bf-194">Добавление проверки подлинности в расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="1d3bf-194">Add authentication to a messaging extension</span></span>](~/messaging-extensions/how-to/add-authentication.md)



