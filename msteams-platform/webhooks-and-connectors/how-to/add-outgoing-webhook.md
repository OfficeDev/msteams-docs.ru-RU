---
title: Создание исходятого веб-окка
author: laujan
description: описывает, как создать исходяющий веб-сайт
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
keywords: teams tabs outgoing webhook actionable message verify webhook
ms.openlocfilehash: 8dabf78cd27f0f59bd8ce617eb83ded24ecc3dc92478e7233bf8f8bb6a2a4e19
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2021
ms.locfileid: "57704319"
---
# <a name="create-outgoing-webhook"></a>Создание исходятого веб-сайта

Исходящем веб-ок действует как бот и поиск сообщений в каналах с помощью **@mention**. Он отправляет уведомления внешним веб-службам и отвечает богатыми сообщениями, в том числе карточками и изображениями. Это помогает пропустить процесс создания ботов через [Microsoft Bot Framework](https://dev.botframework.com/).

## <a name="key-features-of-outgoing-webhook"></a>Ключевые функции исходя из webhook

В следующей таблице представлены функции и описание исходяющих веб-ок:

| Возможности | Описание |
| ------- | ----------- |
| Конфигурация scoped| Webhooks имеют область действия на уровне группы. Обязательный процесс создания для каждого добавляет исходяющий веб-ок. |
| Реактивное сообщение| Пользователи должны использовать @mention для получения сообщений для веб-пользователя. В настоящее время пользователи могут отправлять сообщения об исходяшем веб-окне только в общедоступных каналах, а не в личной или частной области. |
|Стандартный обмен сообщениями HTTP|Ответы отображаются в той же цепочке, что и исходное сообщение запроса, и могут включать любое содержимое сообщения Bot Framework, например богатый текст, изображения, карты и эмодзи. Несмотря на то, что исходяющие веб-пользователи могут использовать карты, они не могут использовать любые действия, за исключением `openURL` .|
| Teams Поддержка метода API|Исходяющие веб-окки отправляют СООБЩЕНИЕ HTTP в веб-службу и получают ответ. Они не могут получить доступ к другим API, например получить список или список каналов в команде.|

## <a name="create-outgoing-webhooks"></a>Создание исходящих веб-перехватчиков

Создание исходяющих веб-ок и добавление пользовательских ботов в Teams.

**Создание исходятого веб-сайта**

1. Выберите **Teams** с левой области. На **Teams** отображается страница:

    ![Канал Teams ](~/assets/images/teamschannel.png)

1. На **Teams** выберите требуемую команду для создания исходятого веб-окка и выберите &#8226;&#8226;&#8226;. В меню dropdown выберите **команду Manage:**

    ![Создание исходятого веб-сайта](~/assets/images/outgoingwebhook1.png)

1. Выберите **вкладку Apps** на странице канала:

    ![Создание исходятого веб-окка](~/assets/images/outgoingwebhook2.png)

1. Выберите **Создать исходяющий веб-сайт:**

    ![Создание исходящих веб-перехватчиков](~/assets/images/outgoingwebhook3.png)

1. Введите следующие сведения на странице **Создание исходятого веб-сайта:**

    * **Имя.** Название веб-страницы и вкладка @mention веб@mention.
    * **URL-адрес** вызова: конечная точка HTTPS, которая принимает полезной нагрузки JSON и получает запросы POST из Teams.
    * **Описание.** Подробная строка, которая отображается в карточке профиля и панели мониторинга приложений на уровне команды.
    * **Изображение профиля:** значок приложения для веб-пользователя, который является необязательным.

1. Нажмите **Создать**. Исходяющий веб-сайт добавляется в канал текущей команды:

    ![создание исходятого веб-окка](~/assets/images/outgoingwebhook.png)

Появляется поле диалогов на основе хэш-кода проверки подлинности сообщений [(HMAC).](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) Это маркер безопасности, используемый для проверки подлинности вызовов между Teams и назначенной внешней службой.

>[!NOTE]
> Исходяющий веб-ок доступен пользователям команды, только если URL-адрес действителен, а маркеры проверки подлинности сервера и клиента равны. Например, рукопожатие HMAC.

Следующий сценарий содержит сведения о добавлении исходя из webhook:

* Сценарий. Нажмите уведомления об изменении состояния на сервере Teams канала в приложение.
* Пример. У вас есть строка бизнес-приложения, отслеживает все операции CRUD, такие как создание, чтение, обновление и удаление. Эти операции для записей сотрудников Teams пользователей отдела кадров по всему Office 365 аренды.

# <a name="url-json-payload"></a>[Полезной нагрузки URL-адреса JSON](#tab/urljsonpayload)
**Создайте URL-адрес на сервере приложения, чтобы принять и обработать запрос POST с помощью полезной нагрузки JSON**

Ваша служба получает сообщения в стандартной схеме обмена сообщениями службы ботов Azure. Соединитель Bot Framework — это служба RESTful, которая позволяет обрабатывать обмен отформатированными сообщениями JSON с помощью протоколов HTTPS, как описано в [API службы Azure Bot.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference) Кроме того, вы можете следовать Microsoft Bot Framework SDK для обработки и размыва сообщений. Дополнительные сведения см. [в обзоре Службы ботов Azure.](/azure/bot-service/bot-service-overview-introduction)

Исходяющие веб-окки имеют область действия до уровня и видны `team` всем участникам группы. Чтобы вызвать **\@ его** в канале, пользователям необходимо упомянуть имя исходятого веб-пользователя.

# <a name="verify-hmac-token"></a>[Проверка маркера HMAC](#tab/verifyhmactoken)
**Создание метода проверки исходятого маркера HMAC Веб-окка**

Использование примера входящие сообщения и ID: "contoso" signingKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhHH3hKKk/N2bOmlM31zaA=" }.

Используйте значение "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" в авторизации загона запроса.

Чтобы убедиться, что служба получает вызовы только от Teams клиентов, Teams код HMAC в заговорке авторизации `hmac` HTTP. Всегда включите код в протокол проверки подлинности.

Код всегда должен проверять подпись HMAC, включенную в запрос, следующим образом:

* Создание маркера HMAC из тела запроса сообщения. Существуют стандартные библиотеки для этого на большинстве платформ, таких как [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) для Node.js и [Teams](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) веб-страницы для C \# ). Microsoft Teams использует стандартную криптографию HMAC SHA256. Необходимо преобразовать тело в массив byte в UTF8.
* Вычисляйте хаш из массива byte маркера безопасности, предоставляемого Teams при регистрации исходяшего веб-сайта в Teams клиенте. См. [статью Создание исходятого веб-окка](#create-outgoing-webhook).
* Преобразование hash в строку с помощью кодификации UTF-8.
* Сравните строковую величину сгенерированного hash со значением, заданным в запросе HTTP.

# <a name="method-to-respond"></a>[Способ ответа](#tab/methodtorespond)
**Создание метода для отправки ответа на ошибку или успешность**

Ответы из исходяющих веб-сайтов отображаются в той же цепочке ответов, что и исходное сообщение. Когда пользователь выполняет запрос, Microsoft Teams выполняет синхронный http-запрос в службу, и код получает пять секунд для ответа на сообщение до времени и прекращения подключения.

### <a name="example-response"></a>Пример отклика

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```
---

> [!NOTE]
> * Вы можете отправлять адаптивную карту, карточку героя и текстовые сообщения в виде вложений с исходяшим веб-сайтом.
> * Форматирование поддержки карт. Дополнительные сведения см. в [виде карт формата с разметками.](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown)

Ниже приводится пример ответа адаптивной карты:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
string content = await this.Request.Content.ReadAsStringAsync();
Activity incomingActivity = JsonConvert.DeserializeObject<Activity>(content);

var Card = new AdaptiveCard(new AdaptiveSchemaVersion("1.4"))
{
    Body = new List<AdaptiveElement>()
    {
        new AdaptiveTextBlock(){Text= $"Request sent by: {incomingActivity.From.Name}"},
        new AdaptiveImage(){Url=new Uri("https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6")},
        new AdaptiveTextBlock(){Text="Sample image for Adaptive Card.."}
    }
};

var attachment = new Attachment()
{
    ContentType = AdaptiveCard.ContentType,
    Content = Card
};

var sampleResponseActivity = new Activity
{
    Attachments = new [] { attachment }
};

return sampleResponseActivity;
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
var receivedMsg = JSON.parse(payload);
var responseMsg = JSON.stringify({
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "contentUrl": null,
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: " + receivedMsg.from.name
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card."
                    }
                ]
            },
            "name": null,
            "thumbnailUrl": null
        }
    ]
});
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: Megan"
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card.."
                    }
                ]
            }
        }
    ]
}
```

* * *

## <a name="code-sample"></a>Пример кода

|**Название примера** | **Описание** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Исходяние веб-ок | Образцы для создания пользовательских ботов, которые будут использоваться в Microsoft Teams.| [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="see-also"></a>Дополнительные ресурсы
* [Создание входящих веб-ок](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Создание соединителя Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Создание и отправка сообщений](~/webhooks-and-connectors/how-to/connectors-using.md)
