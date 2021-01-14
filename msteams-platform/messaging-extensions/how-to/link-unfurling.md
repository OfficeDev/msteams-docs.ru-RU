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
# <a name="link-unfurling"></a>Развернуть ссылку

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> В настоящее время unfurling ссылок не поддерживается на мобильных клиентах.

При отображении ссылки ваше приложение может зарегистрироваться для получения действия, когда URL-адреса с определенным доменом в pasted в область `invoke` составить сообщение. The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl,* providing additional information or actions. Это очень похоже на команду поиска [с](~/messaging-extensions/how-to/search-commands/define-search-command.md)URL-адресом, который служит термином поиска.

Расширение обмена сообщениями Azure DevOps использует размежевание ссылок для искомых URL-адресов, вкопив их в область сообщения составить, указывав на рабочий элемент. На снимке экрана ниже пользователь вошел в URL-адрес для элемента работы в Azure DevOps, который расширение обмена сообщениями разрешено в карточку.

![Пример стирки ссылок](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Добавление unfurling ссылки в манифест приложения

 Чтобы добавить размечение ссылок в манифест приложения, добавьте новый массив в раздел манифеста `messageHandlers` `composeExtensions` приложения JSON. Вы можете добавить массив с помощью App Studio или вручную. В списки доменов могут включались поддеревные знаки, `*.example.com` например. Это соответствует только одному сегменту домена; если вам нужно найти `a.b.example.com` соответствие, используйте `*.*.example.com` .

> [!NOTE]
> Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью поддиаконов. Например, yourapp.onmicrosoft.com допустимый, но *.onmicrosoft.com не является допустимым. Кроме того, домены верхнего уровня запрещены. Например, *.com, *.org.

### <a name="using-app-studio"></a>Использование App Studio

1. В App Studio на вкладке редактора манифеста загрузите манифест приложения.
1. На странице **"Расширение обмена** сообщениями" добавьте домен,  который нужно найти, в разделе "Обработчики сообщений", как по снимку экрана ниже.

![Раздел обработчиков сообщений в App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a>Вручную

Чтобы расширение обмена сообщениями таким образом взаимодействовало со ссылками, сначала необходимо добавить массив в манифест приложения, как по примеру `messageHandlers` ниже. Этот пример не является полным [](~/resources/schema/manifest-schema.md) манифестом. Полный пример манифеста см. в справке по манифесту.

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

## <a name="handle-the-composeextensionquerylink-invoke"></a>Обработка `composeExtension/queryLink` вызова

После того как вы добавите домен для прослушивания манифеста приложения, вам потребуется обновить код веб-службы для обработки запроса на вызов. Используйте URL-адрес, который вы получаете, чтобы найти службу и создать ответ на карточку. Если вы отвечаете с помощью более одной карточки, будет использоваться только первая.

Поддерживаются следующие типы карт:

* [Эскиз карточки](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карточка "Главного"](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Карточка соединители Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карточка](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

См. [обзор карточек.](~/task-modules-and-cards/what-are-cards.md)

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

Это пример отправленного `invoke` боту.

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Ниже приведен пример отклика.

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
