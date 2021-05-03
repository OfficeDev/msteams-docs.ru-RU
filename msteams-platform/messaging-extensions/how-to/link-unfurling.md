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
# <a name="link-unfurling"></a>Развертывание ссылки

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

В этом документе вы можете узнать, как добавить разгрузку ссылки в манифест приложения с помощью студии Приложения и вручную. Развертывание ссылки позволяет приложению получать действие `invoke` при вставке в область создания сообщения URL-адресов с определенным доменом. Полный URL-адрес, который был вклеен в область составить сообщение, и вы можете ответить карточкой, которую пользователь может разкрутить, предоставив дополнительные сведения `invoke` или действия. Это работает по аналогии с командой поиска с URL-адресом, который служит термином поиска.

> [!NOTE]
> В настоящее время разгрузка ссылок не поддерживается в мобильных клиентах.

Расширение Azure DevOps сообщений использует разгрузку ссылок, чтобы искать URL-адреса, вклеив их в область составить сообщение, указывав на рабочий элемент. На следующем изображении пользователь вклеил URL-адрес для элемента работы в Azure DevOps, который расширение обмена сообщениями решило в карточку:

![Пример разгрузки ссылок](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Добавление разгрузки ссылок в манифест приложения

Чтобы добавить разгрузку ссылок в манифест приложения, добавьте новый массив в раздел `messageHandlers` `composeExtensions` манифеста приложения JSON. Массив можно добавлять либо с помощью App Studio, либо вручную. Списки домена могут включать, например, поддиайки. `*.example.com` Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` .

> [!NOTE]
> Donot добавить домены, которые не находятся в вашем контроле, непосредственно или с помощью подкрентов. Например, `yourapp.onmicrosoft.com` допустимо, `*.onmicrosoft.com` но не является допустимым. Кроме того, домены верхнего уровня запрещены. Например, `*.com` `*.org` .

### <a name="add-link-unfurling-using-app-studio"></a>Добавление разгрузки ссылок с помощью App Studio

1. Откройте **App Studio** Microsoft Teams клиента и выберите вкладку Редактор **Манифеста.**
1. Загрузите манифест приложения.
1. На странице **Расширение обмена сообщениями** добавьте домен, который необходимо искать в разделе **Обработчики сообщений.** В следующем изображении объясняется процесс:

    ![Раздел обработчики сообщений в App Studio](~/assets/images/link-unfurling.png)
    
### <a name="add-link-unfurling-manually"></a>Добавление разгрузки ссылок вручную

Чтобы расширение обмена сообщениями взаимодействовало со ссылками, сначала необходимо добавить массив `messageHandlers` в манифест приложения. В следующем примере объясняется, как вручную добавлять разгрузку ссылок: 


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

Полный пример манифеста см. в [справке об манифесте.](~/resources/schema/manifest-schema.md)

## <a name="handle-the-composeextensionquerylink-invoke"></a>Обработка `composeExtension/queryLink` вызова

После добавления домена в манифест приложения необходимо обновить код веб-службы для обработки запроса на вызов. Используйте полученный URL-адрес для поиска службы и создания ответа на карточку. Если вы отвечаете более чем одной картой, используется только первый ответ.

Поддерживаются следующие типы карт:

* [Карта эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карта hero](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 Карта Connector](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карта](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

### <a name="example"></a>Пример

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

Ниже приводится пример `invoke` отправленного боту:

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Ниже приводится пример ответа:

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

## <a name="see-also"></a>См. также 

[Карточки](~/task-modules-and-cards/what-are-cards.md)
