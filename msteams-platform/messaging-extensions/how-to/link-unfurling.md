---
title: Развертывание ссылки
author: surbhigupta
description: Узнайте, как добавить развертывание ссылок с расширением для сообщений в приложении Microsoft Teams с манифестом приложения или вручную с помощью примеров кода и образцов.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b172320f6f116026fe5ea4b45c9c74da6ff82f07
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111250"
---
# <a name="link-unfurling"></a>Развертывание ссылки

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Этот документ содержит инструкции по добавлению ссылки на манифест приложения с помощью App Studio и вручную. Развертывание ссылки позволяет приложению получать действие `invoke` при вставке в область создания сообщения URL-адресов с определенным доменом. `invoke` содержит полный URL-адрес, вставленный в область создания сообщения, и вы можете показать карточку с дополнительной информацией или действиями, которую пользователь может развернуть. Это работает аналогично команде поиска, только в качестве условия поиска используется URL-адрес.

> [!NOTE]
>
> * В настоящее время развертывание ссылок не поддерживается мобильными клиентами.
> * Результат развертывания ссылки кэшируется в течение 30 минут.

Расширение для сообщений Azure DevOps использует развертывание ссылок для поиска URL-адресов, вставленных в область создания сообщений, указывающих на рабочий элемент. На следующем изображении пользователь вставил URL-адрес для рабочего элемента в Azure DevOps, который расширение для сообщения разрешило в карточку:

![Пример развертывания ссылки](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Добавление развертывания ссылок в манифест приложения

Чтобы добавить развертывание ссылок в манифест приложения, добавьте новый массив `messageHandlers` в раздел `composeExtensions` манифеста приложения JSON. Массив можно добавить с помощью App Studio или вручную. Списки доменов могут включать подстановочные знаки, например `*.example.com`. Это соответствует ровно одному сегменту домена. Если вам нужно сопоставить, `a.b.example.com`, используйте `*.*.example.com`.

> [!NOTE]
> Не добавляйте неподконтрольные вам домены (напрямую или с помощью подстановочных знаков). Например, `yourapp.onmicrosoft.com` допустимо, а `*.onmicrosoft.com` не допускается. Кроме того, домены верхнего уровня запрещены. Например: `*.com`, `*.org`.

### <a name="add-link-unfurling-using-app-studio"></a>Добавление развертывания ссылок с помощью App Studio

1. Откройте **App Studio** в клиенте Microsoft Teams и выберите вкладку **редактора манифеста**.
1. Загрузите манифест вашего приложения.
1. На странице **Расширения для сообщений** добавьте домен, который вы хотите найти, в разделе **Обработчики сообщений**. На изображении ниже даны пояснения по этому процессу.

    ![раздел обработчиков сообщений в App Studio](~/assets/images/link-unfurling.png)

### <a name="add-link-unfurling-manually"></a>Добавление развертывания ссылок вручную

Чтобы расширение для сообщений взаимодействовало со ссылками, сначала необходимо добавить массив `messageHandlers` в манифест приложения. В следующем примере объясняется, как вручную добавить развертывание ссылок.

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

Полный пример манифеста см. по [ссылке на манифест](~/resources/schema/manifest-schema.md).

## <a name="handle-the-composeextensionquerylink-invoke"></a>Обработка вызова `composeExtension/queryLink`

После добавления домена в манифест приложения необходимо обновить код веб-службы для обработки запроса на вызов. Используйте полученный URL-адрес для поиска в службе и создания ответа карточки. Если вы отвечаете с помощью более чем одной карточки, используется только первый ответ.

Поддерживаемые типы карточек представлены ниже.

* [Карточка эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карточка главного имиджевого баннера](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Карточка соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карточка](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Дополнительные сведения см. в статье [Вызов типа действия](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke).

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

Ниже приводится пример `invoke`, отправленного вашему боту.

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

Следуйте [пошаговым инструкциям](../../sbs-botbuilder-linkunfurling.yml) по развертыванию ссылок в Teams с помощью бота.

## <a name="see-also"></a>Дополнительные ресурсы

* [Карточки](~/task-modules-and-cards/what-are-cards.md)
* [Развертывание ссылок вкладок и представление "Экран"](~/tabs/tabs-link-unfurling.md)