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
# <a name="respond-to-the-search-command"></a><span data-ttu-id="22b8f-103">Ответ на команду поиска</span><span class="sxs-lookup"><span data-stu-id="22b8f-103">Respond to the search command</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="22b8f-104">Веб-служба получает сообщение о `composeExtension/query` вызове, которое содержит `value` объект с параметрами поиска.</span><span class="sxs-lookup"><span data-stu-id="22b8f-104">Your web service will receive a `composeExtension/query` invoke message that contains a `value` object with the search parameters.</span></span> <span data-ttu-id="22b8f-105">Этот вызов инициируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="22b8f-105">This invoke is triggered:</span></span>

* <span data-ttu-id="22b8f-106">По мере ввода символов в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="22b8f-106">As characters are entered into the search box.</span></span>
* <span data-ttu-id="22b8f-107">Если `initialRun` для манифеста приложения задано значение true, вы получите сообщение Invoke сразу же после вызова команды поиска.</span><span class="sxs-lookup"><span data-stu-id="22b8f-107">If `initialRun` is set to true in your app manifest, you'll receive the invoke message as soon as the search command is invoked.</span></span> <span data-ttu-id="22b8f-108">Просмотр [запроса по умолчанию](#default-query).</span><span class="sxs-lookup"><span data-stu-id="22b8f-108">See [default query](#default-query).</span></span>

<span data-ttu-id="22b8f-109">Собственно параметры запроса находятся в `value` объекте в запросе, который включает следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="22b8f-109">The request parameters itself are found in the `value` object in the request, which includes the following properties:</span></span>

| <span data-ttu-id="22b8f-110">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="22b8f-110">Property name</span></span> | <span data-ttu-id="22b8f-111">Назначение</span><span class="sxs-lookup"><span data-stu-id="22b8f-111">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="22b8f-112">Имя команды, вызываемой пользователем, которая соответствует одной из команд, объявленных в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="22b8f-112">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="22b8f-113">Массив параметров.</span><span class="sxs-lookup"><span data-stu-id="22b8f-113">Array of parameters.</span></span> <span data-ttu-id="22b8f-114">Каждый объект Parameter содержит имя параметра вместе со значением параметра, предоставленным пользователем.</span><span class="sxs-lookup"><span data-stu-id="22b8f-114">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="22b8f-115">Параметры разбивки на страницы:</span><span class="sxs-lookup"><span data-stu-id="22b8f-115">Pagination parameters:</span></span> <br><span data-ttu-id="22b8f-116">`skip`: количество пропусков для этого запроса</span><span class="sxs-lookup"><span data-stu-id="22b8f-116">`skip`: skip count for this query</span></span> <br><span data-ttu-id="22b8f-117">`count`: число возвращаемых элементов</span><span class="sxs-lookup"><span data-stu-id="22b8f-117">`count`: number of elements to return</span></span> |

# <a name="cnettabdotnet"></a>[<span data-ttu-id="22b8f-118">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="22b8f-118">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="22b8f-119">TypeScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="22b8f-119">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="22b8f-120">JSON</span><span class="sxs-lookup"><span data-stu-id="22b8f-120">JSON</span></span>](#tab/json)

<span data-ttu-id="22b8f-121">Приведенный ниже код JSON сокращен для выделения наиболее релевантных разделов.</span><span class="sxs-lookup"><span data-stu-id="22b8f-121">The JSON below is shortened to highlight the most relevant sections.</span></span>

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

## <a name="respond-to-user-requests"></a><span data-ttu-id="22b8f-122">Ответ на запросы пользователей</span><span class="sxs-lookup"><span data-stu-id="22b8f-122">Respond to user requests</span></span>

<span data-ttu-id="22b8f-123">Когда пользователь выполняет запрос, Microsoft Teams отправляет службе синхронный HTTP-запрос.</span><span class="sxs-lookup"><span data-stu-id="22b8f-123">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="22b8f-124">В этот момент код имеет 5 секунд, чтобы предоставить HTTP-ответ на запрос.</span><span class="sxs-lookup"><span data-stu-id="22b8f-124">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="22b8f-125">В течение этого времени служба может выполнять дополнительные операции поиска или любую другую бизнес-логику, необходимую для обслуживания запроса.</span><span class="sxs-lookup"><span data-stu-id="22b8f-125">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="22b8f-126">Служба должна отвечать на результаты, соответствующие запросу пользователя.</span><span class="sxs-lookup"><span data-stu-id="22b8f-126">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="22b8f-127">Ответ должен указывать код состояния HTTP `200 OK` и допустимый объект Application/JSON следующего основного текста:</span><span class="sxs-lookup"><span data-stu-id="22b8f-127">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="22b8f-128">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="22b8f-128">Property name</span></span>|<span data-ttu-id="22b8f-129">Назначение</span><span class="sxs-lookup"><span data-stu-id="22b8f-129">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="22b8f-130">Конверт отклика верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="22b8f-130">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="22b8f-131">Тип ответа.</span><span class="sxs-lookup"><span data-stu-id="22b8f-131">Type of response.</span></span> <span data-ttu-id="22b8f-132">Поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="22b8f-132">The following types are supported:</span></span> <br><span data-ttu-id="22b8f-133">`result`: отображает список результатов поиска</span><span class="sxs-lookup"><span data-stu-id="22b8f-133">`result`: displays a list of search results</span></span> <br><span data-ttu-id="22b8f-134">`auth`: запрос на проверку подлинности пользователя</span><span class="sxs-lookup"><span data-stu-id="22b8f-134">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="22b8f-135">`config`: запрашивает у пользователя установку расширения для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="22b8f-135">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="22b8f-136">`message`: отображается обычное текстовое сообщение</span><span class="sxs-lookup"><span data-stu-id="22b8f-136">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="22b8f-137">Задает макет вложений.</span><span class="sxs-lookup"><span data-stu-id="22b8f-137">Specifies the layout of the attachments.</span></span> <span data-ttu-id="22b8f-138">Используется для ответов типа `result`.</span><span class="sxs-lookup"><span data-stu-id="22b8f-138">Used for responses of type `result`.</span></span> <br><span data-ttu-id="22b8f-139">В настоящее время поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="22b8f-139">Currently the following types are supported:</span></span> <br><span data-ttu-id="22b8f-140">`list`: список объектов карточек, содержащих поля эскиза, заголовка и текста.</span><span class="sxs-lookup"><span data-stu-id="22b8f-140">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="22b8f-141">`grid`: сетка эскизов изображений</span><span class="sxs-lookup"><span data-stu-id="22b8f-141">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="22b8f-142">Массив допустимых объектов вложений.</span><span class="sxs-lookup"><span data-stu-id="22b8f-142">Array of valid attachment objects.</span></span> <span data-ttu-id="22b8f-143">Используется для ответов типа `result`.</span><span class="sxs-lookup"><span data-stu-id="22b8f-143">Used for responses of type `result`.</span></span> <br><span data-ttu-id="22b8f-144">В настоящее время поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="22b8f-144">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="22b8f-145">Предложенные действия.</span><span class="sxs-lookup"><span data-stu-id="22b8f-145">Suggested actions.</span></span> <span data-ttu-id="22b8f-146">Используется для ответов типа `auth` или. `config`</span><span class="sxs-lookup"><span data-stu-id="22b8f-146">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="22b8f-147">Сообщение для отображения.</span><span class="sxs-lookup"><span data-stu-id="22b8f-147">Message to display.</span></span> <span data-ttu-id="22b8f-148">Используется для ответов типа `message`.</span><span class="sxs-lookup"><span data-stu-id="22b8f-148">Used for responses of type `message`.</span></span> |

### <a name="response-card-types-and-previews"></a><span data-ttu-id="22b8f-149">Типы карточек ответа и предварительный просмотр</span><span class="sxs-lookup"><span data-stu-id="22b8f-149">Response card types and previews</span></span>

<span data-ttu-id="22b8f-150">Поддерживаются следующие типы вложений:</span><span class="sxs-lookup"><span data-stu-id="22b8f-150">We support the following attachment types:</span></span>

* [<span data-ttu-id="22b8f-151">Карточка эскиза</span><span class="sxs-lookup"><span data-stu-id="22b8f-151">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="22b8f-152">Карточка главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="22b8f-152">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="22b8f-153">Соединительная карта Office 365</span><span class="sxs-lookup"><span data-stu-id="22b8f-153">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="22b8f-154">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="22b8f-154">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="22b8f-155">Посмотрите [, что представляют собой карточки](~/task-modules-and-cards/what-are-cards.md) для обзора.</span><span class="sxs-lookup"><span data-stu-id="22b8f-155">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="22b8f-156">Сведения о том, как использовать типы карт эскизов и главный Имиджевый баннер, приведены в разделе [Add cards and Card Actions](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="22b8f-156">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="22b8f-157">Дополнительную документацию по карте соединителей Office 365 можно узнать в статье [Использование соединителей карт office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="22b8f-157">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="22b8f-158">Список результатов отображается в пользовательском интерфейсе Microsoft Teams с предварительным просмотром каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="22b8f-158">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="22b8f-159">Предварительный просмотр создается одним из двух способов:</span><span class="sxs-lookup"><span data-stu-id="22b8f-159">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="22b8f-160">Использование `preview` свойства в `attachment` объекте.</span><span class="sxs-lookup"><span data-stu-id="22b8f-160">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="22b8f-161">`preview` Вложение может быть только картой главный Имиджевый баннер или эскиза.</span><span class="sxs-lookup"><span data-stu-id="22b8f-161">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="22b8f-162">Извлекается из базового `title` `text`свойства и `image` свойства вложения.</span><span class="sxs-lookup"><span data-stu-id="22b8f-162">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="22b8f-163">Они используются только в `preview` том случае, если свойство не задано, а эти свойства доступны.</span><span class="sxs-lookup"><span data-stu-id="22b8f-163">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="22b8f-164">Вы можете отобразить предварительный просмотр адаптивной карточки или карты соединителя Office 365 в списке результатов просто с помощью его свойства Preview.</span><span class="sxs-lookup"><span data-stu-id="22b8f-164">You can display a preview of an Adaptive Card or Office 365 Connector card in the result list simply by its preview property.</span></span> <span data-ttu-id="22b8f-165">Это не требуется, если результаты уже главный Имиджевый баннер или эскизы страниц.</span><span class="sxs-lookup"><span data-stu-id="22b8f-165">This is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="22b8f-166">Если вы используете предварительный просмотр вложения, это должна быть карта главный Имиджевый баннер или эскиза.</span><span class="sxs-lookup"><span data-stu-id="22b8f-166">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="22b8f-167">Если свойство Preview не указано, предварительный просмотр карты завершается с ошибками, и ничего не отображается.</span><span class="sxs-lookup"><span data-stu-id="22b8f-167">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

### <a name="response-example"></a><span data-ttu-id="22b8f-168">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="22b8f-168">Response example</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="22b8f-169">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="22b8f-169">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="22b8f-170">TypeScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="22b8f-170">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="22b8f-171">JSON</span><span class="sxs-lookup"><span data-stu-id="22b8f-171">JSON</span></span>](#tab/json)

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

## <a name="default-query"></a><span data-ttu-id="22b8f-172">Запрос по умолчанию</span><span class="sxs-lookup"><span data-stu-id="22b8f-172">Default query</span></span>

<span data-ttu-id="22b8f-173">Если для `initialRun` `true` манифеста задано значение в манифесте, Microsoft Teams по умолчанию выдает запрос "по умолчанию", когда пользователь впервые открывает расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="22b8f-173">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="22b8f-174">Служба может ответить на этот запрос с помощью набора предварительно заполненных результатов.</span><span class="sxs-lookup"><span data-stu-id="22b8f-174">Your service can respond to this query with a set of pre-populated results.</span></span> <span data-ttu-id="22b8f-175">Это может быть полезно, если для команды поиска требуется проверка подлинности или Настройка, отображение недавно просмотренных элементов, избранного или любой другой информации, не зависящей от вводимых пользователем данных.</span><span class="sxs-lookup"><span data-stu-id="22b8f-175">This can be useful when your search command requires authentication or configuration, displaying recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="22b8f-176">Запрос по умолчанию имеет ту же структуру, что и любой обычный запрос пользователя `name` , и `initialRun` `value` `true` для поля задано значение, равное приведенному ниже объекту.</span><span class="sxs-lookup"><span data-stu-id="22b8f-176">The default query has the same structure as any regular user query, with the `name` field set to `initialRun` and `value` set to `true` as in the object below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="22b8f-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22b8f-177">Next Steps</span></span>

<span data-ttu-id="22b8f-178">Добавление проверки подлинности и/или конфигурации</span><span class="sxs-lookup"><span data-stu-id="22b8f-178">Add authentication and/or configuration</span></span>

* [<span data-ttu-id="22b8f-179">Добавление проверки подлинности к расширению системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="22b8f-179">Add authentication to a messaging extension</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="22b8f-180">Добавление конфигурации к расширению обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="22b8f-180">Add configuration to a messaging extension</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="22b8f-181">Развертывание конфигурации</span><span class="sxs-lookup"><span data-stu-id="22b8f-181">Deploy configuration</span></span>

* [<span data-ttu-id="22b8f-182">Развертывание пакета приложений</span><span class="sxs-lookup"><span data-stu-id="22b8f-182">Deploy your app package</span></span>](~/concepts/deploy-and-publish/apps-upload.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
