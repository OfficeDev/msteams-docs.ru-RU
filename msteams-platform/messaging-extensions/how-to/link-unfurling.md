---
title: Развернуть ссылку
author: clearab
description: Как выполнить размевание ссылок с расширением обмена сообщениями в приложении Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 0d488638e63b8ec78bfa5bed8cf6f4f037883fb1
ms.sourcegitcommit: bf61ae5ad2afa4efdb0311158184d0cbb9c40174
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/13/2021
ms.locfileid: "49845639"
---
# <a name="link-unfurling"></a><span data-ttu-id="96f3d-103">Развернуть ссылку</span><span class="sxs-lookup"><span data-stu-id="96f3d-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> <span data-ttu-id="96f3d-104">В настоящее время unfurling ссылок не поддерживается на мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="96f3d-104">Currently, Link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="96f3d-105">При отображении ссылки ваше приложение может зарегистрироваться для получения действия, когда URL-адреса с определенным доменом в pasted в область `invoke` составить сообщение.</span><span class="sxs-lookup"><span data-stu-id="96f3d-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="96f3d-106">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl,* providing additional information or actions.</span><span class="sxs-lookup"><span data-stu-id="96f3d-106">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="96f3d-107">Это очень похоже на команду поиска [с](~/messaging-extensions/how-to/search-commands/define-search-command.md)URL-адресом, который служит термином поиска.</span><span class="sxs-lookup"><span data-stu-id="96f3d-107">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="96f3d-108">Расширение обмена сообщениями Azure DevOps использует размежевание ссылок для искомых URL-адресов, вкопив их в область сообщения составить, указывав на рабочий элемент.</span><span class="sxs-lookup"><span data-stu-id="96f3d-108">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="96f3d-109">На снимке экрана ниже пользователь вошел в URL-адрес для элемента работы в Azure DevOps, который расширение обмена сообщениями разрешено в карточку.</span><span class="sxs-lookup"><span data-stu-id="96f3d-109">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Пример стирки ссылок](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="96f3d-111">Добавление unfurling ссылки в манифест приложения</span><span class="sxs-lookup"><span data-stu-id="96f3d-111">Add link unfurling to your app manifest</span></span>

 <span data-ttu-id="96f3d-112">Чтобы добавить размечение ссылок в манифест приложения, добавьте новый массив в раздел манифеста `messageHandlers` `composeExtensions` приложения JSON.</span><span class="sxs-lookup"><span data-stu-id="96f3d-112">To add link unfurling to your app manifest add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="96f3d-113">Вы можете добавить массив с помощью App Studio или вручную.</span><span class="sxs-lookup"><span data-stu-id="96f3d-113">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="96f3d-114">В списки доменов могут включались поддеревные знаки, `*.example.com` например.</span><span class="sxs-lookup"><span data-stu-id="96f3d-114">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="96f3d-115">Это соответствует только одному сегменту домена; если вам нужно найти `a.b.example.com` соответствие, используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="96f3d-115">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="96f3d-116">Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью поддиаконов.</span><span class="sxs-lookup"><span data-stu-id="96f3d-116">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="96f3d-117">Например, yourapp.onmicrosoft.com допустимый, но \*.onmicrosoft.com не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="96f3d-117">For example, yourapp.onmicrosoft.com is valid, but \*.onmicrosoft.com is not valid.</span></span> <span data-ttu-id="96f3d-118">Кроме того, домены верхнего уровня запрещены.</span><span class="sxs-lookup"><span data-stu-id="96f3d-118">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="96f3d-119">Например, \*.com, \*.org.</span><span class="sxs-lookup"><span data-stu-id="96f3d-119">For example, \*.com, \*.org.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="96f3d-120">Использование App Studio</span><span class="sxs-lookup"><span data-stu-id="96f3d-120">Using App Studio</span></span>

1. <span data-ttu-id="96f3d-121">В App Studio на вкладке редактора манифеста загрузите манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="96f3d-121">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="96f3d-122">На странице **"Расширение обмена** сообщениями" добавьте домен,  который нужно найти, в разделе "Обработчики сообщений", как по снимку экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="96f3d-122">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![Раздел обработчиков сообщений в App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="96f3d-124">Вручную</span><span class="sxs-lookup"><span data-stu-id="96f3d-124">Manually</span></span>

<span data-ttu-id="96f3d-125">Чтобы расширение обмена сообщениями таким образом взаимодействовало со ссылками, сначала необходимо добавить массив в манифест приложения, как по примеру `messageHandlers` ниже.</span><span class="sxs-lookup"><span data-stu-id="96f3d-125">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="96f3d-126">Этот пример не является полным [](~/resources/schema/manifest-schema.md) манифестом. Полный пример манифеста см. в справке по манифесту.</span><span class="sxs-lookup"><span data-stu-id="96f3d-126">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

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

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="96f3d-127">Обработка `composeExtension/queryLink` вызова</span><span class="sxs-lookup"><span data-stu-id="96f3d-127">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="96f3d-128">После того как вы добавите домен для прослушивания манифеста приложения, вам потребуется обновить код веб-службы для обработки запроса на вызов.</span><span class="sxs-lookup"><span data-stu-id="96f3d-128">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="96f3d-129">Используйте URL-адрес, который вы получаете, чтобы найти службу и создать ответ на карточку.</span><span class="sxs-lookup"><span data-stu-id="96f3d-129">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="96f3d-130">Если вы отвечаете с помощью более одной карточки, будет использоваться только первая.</span><span class="sxs-lookup"><span data-stu-id="96f3d-130">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="96f3d-131">Поддерживаются следующие типы карт:</span><span class="sxs-lookup"><span data-stu-id="96f3d-131">We support the following card types:</span></span>

* [<span data-ttu-id="96f3d-132">Эскиз карточки</span><span class="sxs-lookup"><span data-stu-id="96f3d-132">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="96f3d-133">Карточка "Главного"</span><span class="sxs-lookup"><span data-stu-id="96f3d-133">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="96f3d-134">Карточка соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="96f3d-134">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="96f3d-135">Адаптивная карточка</span><span class="sxs-lookup"><span data-stu-id="96f3d-135">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="96f3d-136">См. [обзор карточек.](~/task-modules-and-cards/what-are-cards.md)</span><span class="sxs-lookup"><span data-stu-id="96f3d-136">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="96f3d-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="96f3d-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var card = new HeroCard
    {
        Title = "Hero Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, card);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="96f3d-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="96f3d-138">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="96f3d-139">JSON</span><span class="sxs-lookup"><span data-stu-id="96f3d-139">JSON</span></span>](#tab/json)

<span data-ttu-id="96f3d-140">Это пример отправленного `invoke` боту.</span><span class="sxs-lookup"><span data-stu-id="96f3d-140">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="96f3d-141">Ниже приведен пример отклика.</span><span class="sxs-lookup"><span data-stu-id="96f3d-141">An example of the response is shown below.</span></span>

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
