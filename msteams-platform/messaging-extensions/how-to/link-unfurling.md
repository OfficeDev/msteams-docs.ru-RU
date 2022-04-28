---
title: Развертывание ссылки
author: surbhigupta
description: Узнайте, как добавить размыкание ссылок с расширением сообщения в Microsoft Teams с манифестом приложения или вручную с помощью примеров кода и примеров.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 2dee02545a522b202e9cc695f7099848269e8944
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104408"
---
# <a name="link-unfurling"></a>Развертывание ссылки

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

В этом документе описывается, как добавить размыкание ссылок в манифест приложения с помощью App Studio и вручную. При отмене ссылки `invoke` приложение может зарегистрироваться для получения действия при вставке URL-адресов с определенным доменом в область сообщения создания. Содержит `invoke` полный URL-адрес, вставленный в область сообщения создания, и вы можете ответить карточкой, которую пользователь может отменить, предоставив дополнительные сведения или действия. Это похоже на команду поиска с URL-адресом, который используется в качестве условия поиска.

> [!NOTE]
>
> * В настоящее время размыкание ссылок не поддерживается на мобильных клиентах.
> * Результат отмены переключения ссылок кэшируется в течение 30 минут.

Расширение Azure DevOps сообщений использует размыкание ссылок для поиска URL-адресов, вставленных в область сообщения создания, указывающей на рабочий элемент. На следующем рисунке пользователь вставляет URL-адрес рабочего элемента в Azure DevOps, который расширение сообщения разрешает в карточку:

![Пример размыкания ссылок](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Добавление ссылки в манифест приложения

Чтобы добавить ссылку на манифест приложения, `messageHandlers` `composeExtensions` добавьте новый массив в раздел JSON манифеста приложения. Массив можно добавить с помощью App Studio или вручную. Например, в списках доменов могут быть подстановочные знаки `*.example.com`. Это соответствует только одному сегменту домена. Если вам нужно сопоставить, `a.b.example.com` используйте `*.*.example.com`.

> [!NOTE]
> Не добавляйте домены, которые не находятся в вашем элементе управления, напрямую или с помощью подстановочных знаков. Например, допустимо `yourapp.onmicrosoft.com` , но `*.onmicrosoft.com` недопустимо. Кроме того, домены верхнего уровня запрещены. For example, `*.com`, `*.org`.

### <a name="add-link-unfurling-using-app-studio"></a>Добавление размыкания ссылок с помощью App Studio

1. Откройте **App Studio** в клиенте Microsoft Teams и перейдите на вкладку **редактора манифеста**.
1. Загрузите манифест приложения.
1. На странице **расширения сообщений** добавьте домен, который требуется найти в разделе **"Обработчики сообщений** ". Процесс описан на следующем рисунке:

    ![Раздел обработчиков сообщений в App Studio](~/assets/images/link-unfurling.png)

### <a name="add-link-unfurling-manually"></a>Добавление размыкания ссылок вручную

Чтобы расширение сообщения взаимодействовать со ссылками, `messageHandlers` сначала необходимо добавить массив в манифест приложения. В следующем примере объясняется, как вручную добавить размыкание ссылок:

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

Полный пример манифеста см. в [справочнике по манифестам](~/resources/schema/manifest-schema.md).

## <a name="handle-the-composeextensionquerylink-invoke"></a>Обработка вызова `composeExtension/queryLink`

После добавления домена в манифест приложения необходимо обновить код веб-службы для обработки запроса на вызов. Используйте полученный URL-адрес для поиска в службе и создания ответа карточки. Если вы отвечаете несколькими карточками, используется только первый ответ.

Поддерживаются следующие типы карточек:

* [Карточка эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карточка главного имиджевого баннера](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Карточка соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карточка](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Дополнительные сведения см. в разделе ["Вызов типа действия"](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke).

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

Ниже приведен пример отправленного `invoke` боту.

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Ниже приведен пример ответа:

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

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Выполните [пошаговое руководство по](../../sbs-botbuilder-linkunfurling.yml) распаковывате ссылки в Teams с помощью бота.

## <a name="see-also"></a>См. также

* [Карточки](~/task-modules-and-cards/what-are-cards.md)
* [Предварительный просмотр для ссылки "Вкладки" и представление стадий](~/tabs/tabs-link-unfurling.md)