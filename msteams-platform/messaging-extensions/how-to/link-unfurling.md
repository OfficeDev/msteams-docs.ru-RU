---
title: Развертывание ссылки
author: clearab
description: Выполнение разгрузки ссылок с расширением обмена сообщениями в приложении Microsoft Teams.
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 352de159871069896088559487df2fb94c83e2f9
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075719"
---
# <a name="link-unfurling"></a><span data-ttu-id="a112f-103">Развертывание ссылки</span><span class="sxs-lookup"><span data-stu-id="a112f-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="a112f-104">В этом документе вы можете узнать, как добавить разгрузку ссылки в манифест приложения с помощью студии Приложения и вручную.</span><span class="sxs-lookup"><span data-stu-id="a112f-104">This document guides you on how to add link unfurling to your app manifest using App studio and manually.</span></span> <span data-ttu-id="a112f-105">Развертывание ссылки позволяет приложению получать действие `invoke` при вставке в область создания сообщения URL-адресов с определенным доменом.</span><span class="sxs-lookup"><span data-stu-id="a112f-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="a112f-106">Полный URL-адрес, который был вклеен в область составить сообщение, и вы можете ответить карточкой, которую пользователь может разкрутить, предоставив дополнительные сведения `invoke` или действия.</span><span class="sxs-lookup"><span data-stu-id="a112f-106">The `invoke` contains the full URL that was pasted into the compose message area, and you can respond with a card that the user can unfurl, providing additional information or actions.</span></span> <span data-ttu-id="a112f-107">Это работает по аналогии с командой поиска с URL-адресом, который служит термином поиска.</span><span class="sxs-lookup"><span data-stu-id="a112f-107">This works similar to a search command with the URL serving as the search term.</span></span>

> [!NOTE]
> <span data-ttu-id="a112f-108">В настоящее время разгрузка ссылок не поддерживается в мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="a112f-108">Currently, link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="a112f-109">Расширение Azure DevOps сообщений использует разгрузку ссылок, чтобы искать URL-адреса, вклеив их в область составить сообщение, указывав на рабочий элемент.</span><span class="sxs-lookup"><span data-stu-id="a112f-109">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="a112f-110">На следующем изображении пользователь вклеил URL-адрес для элемента работы в Azure DevOps, который расширение обмена сообщениями решило в карточку:</span><span class="sxs-lookup"><span data-stu-id="a112f-110">In the following image, a user has pasted a URL for a work item in Azure DevOps, which the messaging extension has resolved into a card:</span></span>

![Пример разгрузки ссылок](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="a112f-112">Добавление разгрузки ссылок в манифест приложения</span><span class="sxs-lookup"><span data-stu-id="a112f-112">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="a112f-113">Чтобы добавить разгрузку ссылок в манифест приложения, добавьте новый массив в раздел `messageHandlers` `composeExtensions` манифеста приложения JSON.</span><span class="sxs-lookup"><span data-stu-id="a112f-113">To add link unfurling to your app manifest, add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="a112f-114">Массив можно добавлять либо с помощью App Studio, либо вручную.</span><span class="sxs-lookup"><span data-stu-id="a112f-114">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="a112f-115">Списки домена могут включать, например, поддиайки. `*.example.com`</span><span class="sxs-lookup"><span data-stu-id="a112f-115">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="a112f-116">Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="a112f-116">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="a112f-117">Donot добавить домены, которые не находятся в вашем контроле, непосредственно или с помощью подкрентов.</span><span class="sxs-lookup"><span data-stu-id="a112f-117">Donot add domains that are not in your control, either directly or through wildcards.</span></span> <span data-ttu-id="a112f-118">Например, `yourapp.onmicrosoft.com` допустимо, `*.onmicrosoft.com` но не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="a112f-118">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span> <span data-ttu-id="a112f-119">Кроме того, домены верхнего уровня запрещены.</span><span class="sxs-lookup"><span data-stu-id="a112f-119">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="a112f-120">Например, `*.com` `*.org` .</span><span class="sxs-lookup"><span data-stu-id="a112f-120">For example, `*.com`, `*.org`.</span></span>

### <a name="add-link-unfurling-using-app-studio"></a><span data-ttu-id="a112f-121">Добавление разгрузки ссылок с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="a112f-121">Add link unfurling using App Studio</span></span>

1. <span data-ttu-id="a112f-122">Откройте **App Studio** Microsoft Teams клиента и выберите вкладку Редактор **Манифеста.**</span><span class="sxs-lookup"><span data-stu-id="a112f-122">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1. <span data-ttu-id="a112f-123">Загрузите манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="a112f-123">Load your app manifest.</span></span>
1. <span data-ttu-id="a112f-124">На странице **Расширение обмена сообщениями** добавьте домен, который необходимо искать в разделе **Обработчики сообщений.**</span><span class="sxs-lookup"><span data-stu-id="a112f-124">On the **Messaging Extension** page, add the domain that you want to look for in the **Message handlers** section.</span></span> <span data-ttu-id="a112f-125">В следующем изображении объясняется процесс:</span><span class="sxs-lookup"><span data-stu-id="a112f-125">The following image explains the process:</span></span>

    ![Раздел обработчики сообщений в App Studio](~/assets/images/link-unfurling.png)
    
### <a name="add-link-unfurling-manually"></a><span data-ttu-id="a112f-127">Добавление разгрузки ссылок вручную</span><span class="sxs-lookup"><span data-stu-id="a112f-127">Add link unfurling manually</span></span>

<span data-ttu-id="a112f-128">Чтобы расширение обмена сообщениями взаимодействовало со ссылками, сначала необходимо добавить массив `messageHandlers` в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="a112f-128">To enable your messaging extension to interact with links, first you must add the `messageHandlers` array to your app manifest.</span></span> <span data-ttu-id="a112f-129">В следующем примере объясняется, как вручную добавлять разгрузку ссылок:</span><span class="sxs-lookup"><span data-stu-id="a112f-129">The following example explains how to add link unfurling manually:</span></span> 


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

<span data-ttu-id="a112f-130">Полный пример манифеста см. в [справке об манифесте.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="a112f-130">For a complete manifest example, see [manifest reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="a112f-131">Обработка `composeExtension/queryLink` вызова</span><span class="sxs-lookup"><span data-stu-id="a112f-131">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="a112f-132">После добавления домена в манифест приложения необходимо обновить код веб-службы для обработки запроса на вызов.</span><span class="sxs-lookup"><span data-stu-id="a112f-132">After adding the domain to the app manifest, you must update your web service code to handle the invoke request.</span></span> <span data-ttu-id="a112f-133">Используйте полученный URL-адрес для поиска службы и создания ответа на карточку.</span><span class="sxs-lookup"><span data-stu-id="a112f-133">Use the received URL to search your service and create a card response.</span></span> <span data-ttu-id="a112f-134">Если вы отвечаете более чем одной картой, используется только первый ответ.</span><span class="sxs-lookup"><span data-stu-id="a112f-134">If you respond with more than one card, only the first card response is used.</span></span>

<span data-ttu-id="a112f-135">Поддерживаются следующие типы карт:</span><span class="sxs-lookup"><span data-stu-id="a112f-135">The following card types are supported:</span></span>

* [<span data-ttu-id="a112f-136">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="a112f-136">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="a112f-137">Карта hero</span><span class="sxs-lookup"><span data-stu-id="a112f-137">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="a112f-138">Office 365 Карта Connector</span><span class="sxs-lookup"><span data-stu-id="a112f-138">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="a112f-139">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="a112f-139">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

### <a name="example"></a><span data-ttu-id="a112f-140">Пример</span><span class="sxs-lookup"><span data-stu-id="a112f-140">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="a112f-141">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="a112f-141">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="a112f-142">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="a112f-142">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="a112f-143">JSON</span><span class="sxs-lookup"><span data-stu-id="a112f-143">JSON</span></span>](#tab/json)

<span data-ttu-id="a112f-144">Ниже приводится пример `invoke` отправленного боту:</span><span class="sxs-lookup"><span data-stu-id="a112f-144">Following is an example of the `invoke` sent to your bot:</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="a112f-145">Ниже приводится пример ответа:</span><span class="sxs-lookup"><span data-stu-id="a112f-145">Following is an example of the response:</span></span>

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
        }
      }
    ]
  }
}
```

* * *

## <a name="see-also"></a><span data-ttu-id="a112f-146">См. также</span><span class="sxs-lookup"><span data-stu-id="a112f-146">See also</span></span> 

[<span data-ttu-id="a112f-147">Карточки</span><span class="sxs-lookup"><span data-stu-id="a112f-147">Cards</span></span>](~/task-modules-and-cards/what-are-cards.md)
