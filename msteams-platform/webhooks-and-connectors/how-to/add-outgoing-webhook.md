---
title: Создание исходящего веб-перехватчика
author: laujan
description: Узнайте, как создать исходящий веб-перехватчик в Microsoft Teams, его ключевые функции и пример кода (.NET, Node.js) для создания пользовательских ботов, которые будут использоваться в Teams.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: 8e4e097d20986badc2ca014156f33772d1b997dd
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100492"
---
# <a name="create-outgoing-webhooks"></a>Создание исходящих веб-перехватчиков

Исходящий веб-перехватчик действует как бот и ищет сообщения в каналах с помощью **@упоминания**. Он отправляет уведомления внешним веб-службам и отвечает с помощью информативных сообщений, включающих карточки и изображения. Это помогает пропустить процесс создания ботов с помощью [Microsoft Bot Framework](https://dev.botframework.com/).

<!--- TBD: Edit this article.
* Admonitions/alerts may be overused in this article. Check once.
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* Some screenshots like teamschannel.png may be redundant. Check once.
* Some headings use title case. We use sentence case for titles.
* Check for markdownlint errors. 
* Try using &nbsp; to add spaces in codeblocks for indentation and remove the hard tabs.
* Table with just a row is not really needed. Provide the content without tabulating it.
--->

Чтобы узнать, как создать исходящие веб-перехватчики, посмотрите следующее видео:
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OIzu]
<br>

## <a name="key-features-of-outgoing-webhook"></a>Основные функции исходящего веб-перехватчика

В следующей таблице представлены функции и описание исходящих веб-перехватчиков.

| Возможности | Описание |
| ------- | ----------- |
| Конфигурация с заданная областью| Веб-перехватчики имеют область действия на уровне группы. Обязательный процесс создания для каждого из них добавляет исходящий веб-перехватчик. |
| Реактивный обмен сообщениями| Пользователи должны использовать @упоминание, чтобы веб-перехватчик получил сообщение. В настоящее время пользователи могут отправлять сообщения только исходящим веб-перехватчикам в общедоступных каналах, но не в пределах личных или частных областей. |
|Стандартный обмен сообщениями HTTP|Ответы появятся в той же цепочке, что и исходное сообщение-запрос, и могут содержать все, что содержат сообщения Bot Framework. Например, форматированный текст, изображения, карточки и эмодзи. Хотя исходящие веб-перехватчики могут использовать карточки, они не могут использовать никакие действия с карточками, кроме `openURL`.|
| Поддержка метода API Teams|Исходящие веб-перехватчики отправляют HTTP POST в веб-службу и получают ответ. Они не могут получить доступ к другим API, таким как извлечение списка сотрудников или списка каналов в команде.|

## <a name="create-outgoing-webhooks"></a>Создание исходящих веб-перехватчиков

Создание исходящих веб-перехватчиков и добавление пользовательских ботов в Teams.

Чтобы создать исходящий веб-перехватчик, выполните следующие действия.

1. Выберите **Teams** в левой области. Появится страница **Teams**.

    ![Канал Teams ](~/assets/images/teamschannel.png)

1. In the **Teams** page, select the required team to create an Outgoing Webhook and select the &#8226;&#8226;&#8226;. In the dropdown menu, select **Manage team**:

    ![Создание исходящего веб-перехватчика](~/assets/images/outgoingwebhook1.png)

1. Выберите вкладку **Приложения** на странице канала:

    ![Создание исходящего веб-перехватчика](~/assets/images/outgoingwebhook2.png)

1. Выберите **Создать исходящий веб-перехватчик**.

    ![Создание исходящих веб-перехватчиков](~/assets/images/outgoingwebhook3.png)

1. Введите следующие сведения на странице **Создать исходящий веб-перехватчик**.

    * **Имя**: название веб-перехватчика и вкладки @упоминаний.
    * **URL-адрес обратного вызова**: конечная точка HTTPS, которая принимает полезную нагрузку JSON и получает запросы POST от Teams.
    * **Описание**: подробная строка, которая отображается в карточке профиля и на панели управления приложения на уровне группы.
    * **Аватар**: необязательный значок приложения для веб-перехватчика.

1. Select **Create**. The Outgoing Webhook is added to the current team's channel:

    ![Создание исходящего веб-перехватчика](~/assets/images/outgoingwebhook.png)

Появится диалоговое окно [Код проверки подлинности сообщений с помощью хэш-функций (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301). Это маркер безопасности, используемый для проверки подлинности звонков между Teams и назначенной внешней службой. Маркер безопасности HMAC не истекает и является уникальным для каждой конфигурации.

>[!NOTE]
> The Outgoing Webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal. For example, an HMAC handshake.

В следующем сценарии даны подробные сведения о добавлении исходящего веб-перехватчика.

* Сценарий: push-уведомления об изменении состояния на сервере базы данных канала Teams в ваше приложение.
* Пример: у вас есть бизнес-приложение, которое отслеживает все операции создания, чтения, обновления и удаления (CRUD). Эти операции с записями сотрудников выполняются пользователями канала Teams из отдела кадров в области клиента Office 365.

# <a name="url-json-payload"></a>[Полезная нагрузка URL в JSON](#tab/urljsonpayload)

**Создайте URL-адрес на сервере приложения, чтобы принять и обработать POST-запрос с помощью полезной нагрузки JSON**

Ваша служба получает сообщения в стандартной схеме обмена сообщениями службы Azure Bot. Соединитель Bot Framework — это служба RESTful, которая позволяет обрабатывать обмен сообщениями в формате JSON с помощью протоколов HTTPS, как описано в [API службы Azure Bot](/bot-framework/rest-api/bot-framework-rest-connector-api-reference). Кроме того, вы можете использовать пакет SDK Microsoft Bot Framework для обработки и анализа сообщений. Дополнительные сведения см. в разделе с [обзором службы Azure Bot](/azure/bot-service/bot-service-overview-introduction).

Исходящие веб-перехватчики имеют область действия на уровне `team` и видны всем участникам команды. Пользователям необходимо **\@упомянуть** имя исходящего веб-перехватчика для его вызова в канал.

# <a name="verify-hmac-token"></a>[Проверка маркера HMAC](#tab/verifyhmactoken)

**Создание метода проверки токена HMAC исходящего веб-перехватчика**

Использование примера входящие сообщения и идентификатора: "contoso" из SigningKeyDictionary из {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.

Используйте значение "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" в авторизации заголовка запроса.

To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` authorization header. Always include the code in your authentication protocol.

Код всегда должен проверять подпись HMAC, включенную в запрос, следующим образом.

* Создание маркера HMAC из текста запроса сообщения. Для этого в большинстве платформ существуют стандартные библиотеки, например, [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) для Node.js и [пример веб-перехватчика Teams](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) для C\#. В Microsoft Teams используется стандартное шифрование HMAC SHA256. Необходимо преобразовать тело в массив байтов в UTF8.
* Compute the hash from the byte array of the security token provided by Teams when you registered the Outgoing Webhook in the Teams client. See [create an Outgoing Webhook](#create-outgoing-webhooks).
* Преобразуйте хэш-значение в строку с помощью кодировки UTF-8.
* Сравните строковое значение сгенерированного хэш-значения со значением, предоставленным в HTTP-запросе.

# <a name="method-to-respond"></a>[Метод ответа](#tab/methodtorespond)

**Создание метода отправки ответа о выполнении или ошибке**

Ответы от исходящих веб-перехватчиков отображаются в той же цепочке ответов, что и исходное сообщение. При выполнении запроса пользователем, Teams отправляет синхронный HTTP-запрос к вашей службе, после чего у вашего кода есть пять секунд, чтобы ответить на сообщение, прежде чем время ожидания соединения истечет и оно прервется.

### <a name="example-response"></a>Пример отклика

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

---

> [!NOTE]
>
> * Можно отправлять адаптивные карточки, карточки главного имиджевого баннера и текстовые сообщения в виде вложений с помощью исходящего веб-перехватчика.
> * Cards support formatting. For more information, see [format cards with markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).
> * Адаптивная карточка в исходящих веб-перехватчиках поддерживает только действия карточки `openURL`.

Следующие части кода являются примерами отклика адаптивной карточки:

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

---

## <a name="code-sample"></a>Пример кода

|**Название примера** | **Описание** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Исходящие веб-перехватчики | Примеры создания пользовательских ботов для использования в Microsoft Teams.| [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте [пошаговой инструкции](../../sbs-outgoing-webhooks.yml), чтобы создать исходящие веб-перехватчики в Teams.

## <a name="see-also"></a>См. также

* [Создание входящего веб-перехватчика](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Создание соединителя Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Создание и отправка сообщений](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Создание бота уведомлений с помощью JavaScript](../../sbs-gs-notificationbot.yml)
* [Создание первого приложения бота с помощью JavaScript](../../sbs-gs-bot.yml)
