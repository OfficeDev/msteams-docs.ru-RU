---
title: Развертывание ссылки
author: surbhigupta
description: Добавьте раскройку ссылки с помощью расширения для обмена сообщениями в приложении Microsoft Teams с манифестом приложения или вручную. Добавьте распаковку ссылки с помощью портала разработчика. Обновление кода веб-службы для обработки запроса на вызов.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: c706bd4caf8ab7859fb0c8f9b5b9e8f337a3b269
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820152"
---
# <a name="add-link-unfurling"></a>Добавление разворачивающейся ссылки

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

В этом документе описывается, как добавить распаковку ссылок в манифест приложения с помощью портала разработчика или вручную. Развертывание ссылки позволяет приложению получать действие `invoke` при вставке в область создания сообщения URL-адресов с определенным доменом. Содержит `invoke` полный URL-адрес, который был вставлен в область создания сообщения. Вы можете ответить карточкой, которую пользователь может разворачивать для получения дополнительных сведений или действий. Это работает как команда поиска с URL-адресом в качестве условия поиска.

> [!NOTE]
>
> * В настоящее время развертывание ссылок не поддерживается мобильными клиентами.
> * Результат развертывания ссылки кэшируется в течение 30 минут.
> * Команды расширения обмена сообщениями не требуются для распаковки связи. Однако в манифесте должна быть по крайней мере одна команда, так как она является обязательным свойством в расширениях обмена сообщениями. Дополнительные сведения см. в разделе [Создание расширений](/microsoftteams/platform/resources/schema/manifest-schema).

Расширение для сообщений Azure DevOps использует развертывание ссылок для поиска URL-адресов, вставленных в область создания сообщений, указывающих на рабочий элемент. На следующем рисунке пользователь вставил URL-адрес элемента в Azure DevOps, который расширение сообщения разрешило в карточку:

:::image type="content" source="~/assets/images/compose-extensions/messagingextensions_linkunfurling.png" alt-text="Пример развертывания ссылки":::

Дополнительные сведения о раскрое ссылок см. в следующем видео:
<br>
> [!VIDEO <https://www.microsoft.com/en-us/videoplayer/embed/RE4OFZG>]
<br>

## <a name="add-link-unfurling-to-your-app-manifest"></a>Добавление развертывания ссылок в манифест приложения

Чтобы добавить развертывание ссылок в манифест приложения, добавьте новый массив `messageHandlers` в раздел `composeExtensions` манифеста приложения JSON. Массив можно добавить с помощью портала разработчика или вручную. Списки доменов могут включать подстановочные знаки, например `*.example.com`. Это соответствует ровно одному сегменту домена. Если вам нужно сопоставить, `a.b.example.com`, используйте `*.*.example.com`.

> [!NOTE]
> Не добавляйте домены, которые не находятся в вашем контроле напрямую или с помощью подстановочных знаков. Например, `yourapp.onmicrosoft.com` допустимо, а `*.onmicrosoft.com` не допускается. Домены верхнего уровня запрещены, например `*.com`, `*.org`.

### <a name="add-link-unfurling-using-developer-portal"></a>Добавление распаковки ссылок с помощью портала разработчика

1. Откройте **портал разработчика** в клиенте Microsoft Teams и выберите вкладку **Приложения** .
1. Загрузите манифест вашего приложения.
1. На странице **Расширение для обмена сообщениями** в разделе **Функции приложения** выберите существующего бота или создайте бот.
1. Нажмите кнопку **Сохранить**.
1. Выберите **Добавить домен в** разделе **Ссылки предварительного просмотра** и введите допустимый домен.
1. Нажмите **Добавить**. На изображении ниже даны пояснения по этому процессу.

   :::image type="content" source="../../assets/images/tdp/add-domain-button.PNG" alt-text="Снимок экрана: раздел обработчиков сообщений на портале разработчика." lightbox="../../assets/images/tdp/add-domain.PNG":::

### <a name="add-link-unfurling-manually"></a>Добавление развертывания ссылок вручную

> [!NOTE]
> Если проверка подлинности добавлена через Azure AD, [разворачивайте ссылки в Teams с помощью бота](/microsoftteams/platform/sbs-botbuilder-linkunfurling?tabs=vs&tutorial-step=4).

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

* [Расширения для сообщений](../what-are-messaging-extensions.md)
* [Адаптивные карточки](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Развертывание ссылок вкладок и представление "Экран"](../../tabs/tabs-link-unfurling.md)
* [composeExtensions](../../resources/schema/manifest-schema.md#composeextensions)
