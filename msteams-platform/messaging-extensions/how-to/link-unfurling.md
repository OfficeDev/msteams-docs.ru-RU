---
title: Ссылка унфурлинг
author: clearab
description: Порядок выполнения ссылок унфурлинг с расширением обмена сообщениями в приложении Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5b20ea303a2c3d085651a53b01af4bb449d386de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675667"
---
# <a name="link-unfurling"></a><span data-ttu-id="f4c29-103">Ссылка унфурлинг</span><span class="sxs-lookup"><span data-stu-id="f4c29-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="f4c29-104">С помощью Link унфурлинг приложение может зарегистрироваться для получения `invoke` действия при вставке URL-адресов с определенным доменом в область "Создание сообщения".</span><span class="sxs-lookup"><span data-stu-id="f4c29-104">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="f4c29-105">В `invoke` нем будет содержаться полный URL-адрес, который был вставлен в область сообщений, и вы можете ответить на карточку, которая может *унфурл*пользователь, предоставляя дополнительные сведения или действия.</span><span class="sxs-lookup"><span data-stu-id="f4c29-105">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="f4c29-106">Это аналогично [команде поиска](~/messaging-extensions/how-to/search-commands/define-search-command.md)с URL-адресом в качестве условия поиска.</span><span class="sxs-lookup"><span data-stu-id="f4c29-106">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="f4c29-107">Модуль обмена сообщениями Azure DevOps использует Link унфурлинг для поиска URL-адресов, вставленных в область сообщений, указывающую на рабочий элемент.</span><span class="sxs-lookup"><span data-stu-id="f4c29-107">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="f4c29-108">На снимке экрана ниже пользователь вставил в URL-адрес рабочего элемента в Azure DevOps, который разрешал расширение обмена сообщениями в карточке.</span><span class="sxs-lookup"><span data-stu-id="f4c29-108">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Пример ссылки унфурлинг](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="f4c29-110">Добавление ссылки унфурлинг к манифесту приложения</span><span class="sxs-lookup"><span data-stu-id="f4c29-110">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="f4c29-111">Для этого мы добавим новый `messageHandlers` массив в `composeExtensions` раздел JSON манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="f4c29-111">To do this you'll add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="f4c29-112">Это можно сделать с помощью App Studio или вручную.</span><span class="sxs-lookup"><span data-stu-id="f4c29-112">You can either do so with the help of App Studio, or manually.</span></span> <span data-ttu-id="f4c29-113">Примеры доменов могут включать подстановочные знаки `*.example.com`.</span><span class="sxs-lookup"><span data-stu-id="f4c29-113">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="f4c29-114">Это соответствует только одному сегменту домена; Если вам нужно использовать `a.b.example.com` `*.*.example.com`этот параметр.</span><span class="sxs-lookup"><span data-stu-id="f4c29-114">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="f4c29-115">Использование App Studio</span><span class="sxs-lookup"><span data-stu-id="f4c29-115">Using App Studio</span></span>

1. <span data-ttu-id="f4c29-116">В App Studio на вкладке редактор манифеста Загрузите манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="f4c29-116">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="f4c29-117">На странице **расширение системы обмена сообщениями** добавьте домен, который вы хотите найти, в раздел **обработчики сообщений** , как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="f4c29-117">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![раздел обработчиков сообщений в App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="f4c29-119">Вручную</span><span class="sxs-lookup"><span data-stu-id="f4c29-119">Manually</span></span>

<span data-ttu-id="f4c29-120">Чтобы разрешить своему расширению обмена сообщениями взаимодействовать с ссылками таким способом, сначала необходимо добавить `messageHandlers` массив в манифест приложения, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="f4c29-120">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="f4c29-121">Этот пример не является полным манифестом, в статье [Справочник по манифесту](~/resources/schema/manifest-schema.md) представлен полный пример манифеста.</span><span class="sxs-lookup"><span data-stu-id="f4c29-121">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

```json
...
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
],
...
```

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="f4c29-122">Обработка `composeExtension/queryLink` вызова</span><span class="sxs-lookup"><span data-stu-id="f4c29-122">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="f4c29-123">Добавив домен для прослушивания манифеста приложения, вам потребуется обновить код веб-службы, чтобы обработать запрос Invoke.</span><span class="sxs-lookup"><span data-stu-id="f4c29-123">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="f4c29-124">Используйте полученный URL-адрес для поиска службы и создания ответа на карту.</span><span class="sxs-lookup"><span data-stu-id="f4c29-124">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="f4c29-125">Если вы отдаете ответ с несколькими картами, будет использоваться только первый из них.</span><span class="sxs-lookup"><span data-stu-id="f4c29-125">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="f4c29-126">Поддерживаются следующие типы карточек:</span><span class="sxs-lookup"><span data-stu-id="f4c29-126">We support the following card types:</span></span>

* [<span data-ttu-id="f4c29-127">Карточка эскиза</span><span class="sxs-lookup"><span data-stu-id="f4c29-127">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="f4c29-128">Карточка главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="f4c29-128">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="f4c29-129">Соединительная карта Office 365</span><span class="sxs-lookup"><span data-stu-id="f4c29-129">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="f4c29-130">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="f4c29-130">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="f4c29-131">Посмотрите [, что представляют собой карточки](~/task-modules-and-cards/what-are-cards.md) для обзора.</span><span class="sxs-lookup"><span data-stu-id="f4c29-131">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="f4c29-132">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="f4c29-132">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var heroCard = new ThumbnailCard
    {
        Title = "Thumbnail Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, heroCard);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="f4c29-133">JavaScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="f4c29-133">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsLinkUnfurlingBot extends TeamsActivityHandler {
  handleTeamsAppBasedLinkQuery(context, query) {
    const attachment = CardFactory.thumbnailCard('Thumbnail Card',
      query.url,
      ['https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png']);

    const result = {
      attachmentLayout: 'list',
      type: 'result',
      attachments: [attachment]
    };

    const response = {
      composeExtension: result
    };
    return response;
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="f4c29-134">JSON</span><span class="sxs-lookup"><span data-stu-id="f4c29-134">JSON</span></span>](#tab/json)

<span data-ttu-id="f4c29-135">Это пример сообщения, `invoke` отправленного в Bot.</span><span class="sxs-lookup"><span data-stu-id="f4c29-135">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="f4c29-136">Ниже приведен пример отклика.</span><span class="sxs-lookup"><span data-stu-id="f4c29-136">An example of the response is shown below.</span></span>

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
        }
      }
    ]
  }
}
```

* * *
