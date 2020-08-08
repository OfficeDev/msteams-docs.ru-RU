---
title: Развернуть ссылку
author: clearab
description: Порядок выполнения ссылок унфурлинг с расширением обмена сообщениями в приложении Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 32d19fcd44f2475047539350706d2745aeec3691
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587806"
---
# <a name="link-unfurling"></a>Развернуть ссылку

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> В настоящее время ссылки унфурлинг не поддерживаются на мобильных клиентах.

С помощью Link унфурлинг приложение может зарегистрироваться для получения `invoke` действия при вставке URL-адресов с определенным доменом в область "Создание сообщения". В нем `invoke` будет содержаться полный URL-адрес, который был вставлен в область сообщений, и вы можете ответить на карточку, которая может *унфурл*пользователь, предоставляя дополнительные сведения или действия. Это аналогично [команде поиска](~/messaging-extensions/how-to/search-commands/define-search-command.md)с URL-адресом в качестве условия поиска.

Модуль обмена сообщениями Azure DevOps использует Link унфурлинг для поиска URL-адресов, вставленных в область сообщений, указывающую на рабочий элемент. На снимке экрана ниже пользователь вставил в URL-адрес рабочего элемента в Azure DevOps, который разрешал расширение обмена сообщениями в карточке.

![Пример ссылки унфурлинг](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Добавление ссылки унфурлинг к манифесту приложения

Для этого мы добавим новый `messageHandlers` массив в `composeExtensions` раздел JSON манифеста приложения. Это можно сделать с помощью App Studio или вручную. Примеры доменов могут включать подстановочные знаки `*.example.com` . Это соответствует только одному сегменту домена; Если вам нужно использовать этот параметр `a.b.example.com` `*.*.example.com` .

### <a name="using-app-studio"></a>Использование App Studio

1. В App Studio на вкладке редактор манифеста Загрузите манифест приложения.
1. На странице **расширение системы обмена сообщениями** добавьте домен, который вы хотите найти, в раздел **обработчики сообщений** , как показано на снимке экрана ниже.

![раздел обработчиков сообщений в App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a>Вручную

Чтобы разрешить своему расширению обмена сообщениями взаимодействовать с ссылками таким способом, сначала необходимо добавить `messageHandlers` массив в манифест приложения, как показано в примере ниже. Этот пример не является полным манифестом, в статье [Справочник по манифесту](~/resources/schema/manifest-schema.md) представлен полный пример манифеста.

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

Добавив домен для прослушивания манифеста приложения, вам потребуется обновить код веб-службы, чтобы обработать запрос Invoke. Используйте полученный URL-адрес для поиска службы и создания ответа на карту. Если вы отдаете ответ с несколькими картами, будет использоваться только первый из них.

Поддерживаются следующие типы карточек:

* [Карточка эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карточка главный Имиджевый баннер](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Соединительная карта Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карта](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Посмотрите [, что представляют собой карточки](~/task-modules-and-cards/what-are-cards.md) для обзора.

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

Это пример `invoke` сообщения, отправленного в Bot.

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
