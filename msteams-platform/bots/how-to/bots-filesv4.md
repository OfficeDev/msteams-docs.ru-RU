---
title: Отправка и получение файлов с помощью бота
description: Узнайте, как отправлять и получать файлы через бот с помощью API Graph для личной области, области канала и области группового чата.
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 20dc421531864cf88f55932bc85ae7979f7992ff
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2022
ms.locfileid: "67605049"
---
# <a name="send-and-receive-files-using-bot"></a>Отправка и получение файлов с помощью бота

> [!IMPORTANT]
> Статьи в этом документе основаны на данных пакета SDK Bot Framework версии 4.

Существует два способа отправки файлов в бот и из бота:

* [**Использование API Microsoft Graph.**](#use-the-graph-apis) Этот метод работает для ботов во всех областях Microsoft Teams.
  * `personal`
  * `channel`
  * `groupchat`

* [**Использование API бота Teams.**](#use-the-teams-bot-apis) Поддерживают только файлы в контексте`personal`.

## <a name="use-the-graph-apis"></a>Использование API Graph

Публикуйте сообщения с вложенными карточками, которые ссылаются на существующие файлы SharePoint, с помощью API Graph для [OneDrive и SharePoint](/onedrive/developer/rest-api/). Чтобы использовать API Graph, получите доступ к одному из следующих элементов с помощью стандартного потока авторизации OAuth 2.0:

* папка OneDrive пользователя для файлов `personal` и `groupchat`;
* файлы в канале команды для файлов `channel`.

API Graph работают во всех областях Teams. Дополнительные сведения см. в статье [Отправка файлов, вложенных в сообщения чата](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true).

Кроме того, вы можете отправлять файлы в бот и из бота с помощью API бота Teams.

## <a name="use-the-teams-bot-apis"></a>Использование API бота Teams

> [!NOTE]
> API бота Teams работают только в контексте `personal`. Они не работают в контексте `channel` или `groupchat`.

С помощью API Teams бот может напрямую отправлять и получать файлы для пользователей в контексте `personal`, также известном как личные чаты. Реализуйте такие функции, как отчеты о расходах, распознавание изображений, архивация файлов и электронные подписи с редактированием содержимого файла. Файлы, опубликованные в Teams, обычно отображаются в виде карточек и поддерживают расширенный просмотр в приложении.

В следующих разделах описано, как отправить содержимое файла при непосредственном участии пользователя, например при отправке сообщения. Этот API предоставляется в рамках платформы для ботов Teams.

### <a name="configure-the-bot-to-support-files"></a>Настройка поддержки файлов в боте

Чтобы отправлять файлы в бот и из бота, настройте для свойства `supportsFiles` в манифесте значение `true`. Это свойство описано в разделе [Боты](~/resources/schema/manifest-schema.md#bots) в справочнике по манифесту.

Определение выглядит следующим образом: `"supportsFiles": true`. Если бот не включает `supportsFiles`, функции, указанные в этом разделе, не работают.

### <a name="receive-files-in-personal-chat"></a>Получение файлов в личном чате

Когда пользователь отправляет файл в бот, файл сначала отправляется в хранилище "OneDrive для бизнеса" пользователя. Затем бот получает действие с сообщением, уведомляющее пользователя об отправке. Оно содержит метаданные файла, например его имя и URL-адрес содержимого. Пользователь может напрямую считывать данные из этого URL-адреса, чтобы получить его двоичное содержимое.

#### <a name="message-activity-with-file-attachment-example"></a>Пример действия с сообщением с вложенным файлом

В следующем коде показан пример действия с сообщением с вложенным файлом:

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.file.download.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "downloadUrl" : "https://download.link",
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C9D",
      "fileType": "txt",
      "etag": "123"
    }
  }]
}
```

В следующей таблице описаны свойства содержимого вложения.

| Свойство | Назначение |
| --- | --- |
| `downloadUrl` | URL-адрес OneDrive для получения содержимого файла. Пользователь может выдать запрос `HTTP GET` непосредственно с этого URL-адреса. |
| `uniqueId` | Уникальный идентификатор файла. Это идентификатор элемента диска OneDrive для отправки файла в бот. |
| `fileType` | Тип файла, например PDF или DOCX. |

Рекомендуется подтвердить отправку файла, отправив сообщение обратно пользователю.

### <a name="upload-files-to-personal-chat"></a>Отправка файлов в личный чат

Чтобы отправить файл пользователю, выполните следующие действия.

1. Отправьте сообщение пользователю, запросив разрешение на запись файла. Это сообщение должно содержать вложение `FileConsentCard` с именем файла для отправки.
2. Если пользователь разрешает скачивание файла, бот получает действие вызова с URL-адресом расположения.
3. Чтобы передать файл, бот выполняет запрос `HTTP POST` непосредственно в указанном URL-адресе расположения.
4. Вы можете удалить исходную карточку согласия, если не хотите, чтобы пользователь принимал дальнейшие отправки того же файла.

#### <a name="message-requesting-permission-to-upload"></a>Сообщение с запросом разрешения на отправку

Следующее сообщение в классическом интерфейсе содержит простой объект вложения с запросом разрешения пользователя на отправку файла:

:::image type="content" source="../../assets/images/bots/bot-file-consent-card.png" alt-text="Карточка согласия с запросом разрешения пользователя на отправку файла"lightbox="../../assets/images/bots/bot-file-consent-card.png"border="true":::

Следующее сообщение в мобильном интерфейсе содержит объект вложения с запросом разрешения пользователя на отправку файла:

<img src="../../assets/images/bots/mobile-bot-file-consent-card.png" alt="Consent card requesting user permission to upload file on mobile" width="350"/>

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.consent",
    "name": "file_example.txt",
    "content": {
      "description": "<Purpose of the file, such as: this is your monthly expense report>",
      "sizeInBytes": 1029393,
      "acceptContext": {
      },
      "declineContext": {
      }
    }
  }]
}
```

В следующей таблице описаны свойства содержимого вложения.

| Свойство | Назначение |
| --- | --- |
| `description` | Описывает назначение файла или суммирует его содержимое. |
| `sizeInBytes` | Предоставляет пользователю оценку размера файла и объема пространства, которое он занимает в OneDrive. |
| `acceptContext` | Дополнительный контекст, который автоматически передается в бот, когда пользователь принимает файл. |
| `declineContext` | Дополнительный контекст, который автоматически передается в бот, когда пользователь отклоняет файл. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Действие вызова при принятии файла пользователем

Действие вызова отправляется в бот, если и когда пользователь принимает файл. Оно содержит URL-адрес заполнителя OneDrive для бизнеса, для которого ваш бот может выдать запрос `PUT`, чтобы передать содержимое файла. Сведения об отправке на URL-адрес OneDrive см. в статье [Отправка байтов в сеанс отправки](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).

В следующем коде показан пример краткой версии действия вызова, получаемого ботом:

```json
{
  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "accept",
    "context": {
    },
    "uploadInfo": {
      "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
      "name": "file_example.txt",
      "uploadUrl": "https://upload.link",
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C8C",
      "fileType": "txt",
      "etag": "123"
    }
  }
}
```

Аналогичным образом, если пользователь отклоняет файл, бот получает следующее событие с таким же именем общего действия:

```json
{
  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "decline",
    "context": {
    }
  }
}
```

### <a name="notifying-the-user-about-an-uploaded-file"></a>Уведомление пользователя об отправленном файле

Отправив файл в хранилище OneDrive пользователя, отправьте пользователю сообщение с подтверждением. Сообщение должно содержать следующее вложение `FileCard`, которое пользователь может щелкнуть для предварительного просмотра, открыть в OneDrive или скачать локально:

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C8C",
      "fileType": "txt",
    }
  }]
}
```

В следующей таблице описаны свойства содержимого вложения.

| Свойство | Назначение |
| --- | --- |
| `uniqueId` | Идентификатор элемента диска OneDrive или SharePoint. |
| `fileType` | Тип файла, например PDF или DOCX. |

### <a name="fetch-inline-images-from-message"></a>Получение встроенных изображений из сообщения

Получите встроенные изображения, которые являются частью сообщения, с помощью маркера доступа бота.

:::image type="content" source="../../assets/images/bots/inline-image.png" alt-text="Встроенное изображение"border="true":::

В следующем коде показан пример получения встроенных изображений из сообщения:

```csharp
private async Task ProcessInlineImage(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var attachment = turnContext.Activity.Attachments[0];
    var client = _clientFactory.CreateClient();
    // Get Bot's access token to fetch inline image. 
    var token = await new MicrosoftAppCredentials(microsoftAppId, microsoftAppPassword).GetTokenAsync();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    var responseMessage = await client.GetAsync(attachment.ContentUrl);
    // Save the inline image to Files directory.
    var filePath = Path.Combine("Files", "ImageFromUser.png");
    using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
    {
        await responseMessage.Content.CopyToAsync(fileStream);
    }
    // Create reply with image.
    var reply = MessageFactory.Text($"Attachment of {attachment.ContentType} type and size of {responseMessage.Content.Headers.ContentLength} bytes received.");
    reply.Attachments = new List<Attachment>() { 
        GetInlineAttachment() 
    };
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
private static Attachment GetInlineAttachment()
{
    var imagePath = Path.Combine("Files", "ImageFromUser.png");
    var imageData = Convert.ToBase64String(File.ReadAllBytes(imagePath));
    return new Attachment
    {
        Name = @"ImageFromUser.png",
        ContentType = "image/png",
        ContentUrl = $"data:image/png;base64,{imageData}",
    };
}
```

### <a name="basic-example-in-c"></a>Основной пример в C# #

В следующем коде показан пример обработки отправки файла и отправки запроса на согласие для файла в диалоговом окне бота:

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    if (turnContext.Activity.Attachments?[0].ContentType.Contains("image/*") == true)
    {
        // Inline image.
        await ProcessInlineImage(turnContext, cancellationToken);
    }
    else
    {
        string filename = "teams-logo.png";
        string filePath = Path.Combine("Files", filename);
        long fileSize = new FileInfo(filePath).Length;
        await SendFileCardAsync(turnContext, filename, fileSize, cancellationToken);
    }
}
private async Task ProcessInlineImage(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var attachment = turnContext.Activity.Attachments[0];
    var client = _clientFactory.CreateClient();
    // Get Bot's access token to fetch inline image. 
    var token = await new MicrosoftAppCredentials(microsoftAppId, microsoftAppPassword).GetTokenAsync();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    var responseMessage = await client.GetAsync(attachment.ContentUrl);
    // Save the inline image to Files directory.
    var filePath = Path.Combine("Files", "ImageFromUser.png");
    using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
    {
        await responseMessage.Content.CopyToAsync(fileStream);
    }
    // Create reply with image.
    var reply = MessageFactory.Text($"Attachment of {attachment.ContentType} type and size of {responseMessage.Content.Headers.ContentLength} bytes received.");
    reply.Attachments = new List<Attachment>() { GetInlineAttachment() };
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
private static Attachment GetInlineAttachment()
{
    var imagePath = Path.Combine("Files", "ImageFromUser.png");
    var imageData = Convert.ToBase64String(File.ReadAllBytes(imagePath));
    return new Attachment
    {
        Name = @"ImageFromUser.png",
        ContentType = "image/png",
        ContentUrl = $"data:image/png;base64,{imageData}",
    };
}
private async Task SendFileCardAsync(ITurnContext turnContext, string filename, long filesize, CancellationToken cancellationToken)
{
    var consentContext = new Dictionary<string, string>
    {
        { 
            "filename", filename 
        },
    };
    var fileCard = new FileConsentCard
    {
        Description = "This is the file I want to send you",
        SizeInBytes = filesize,
        AcceptContext = consentContext,
        DeclineContext = consentContext,
    };
    var asAttachment = new Attachment
    {
        Content = fileCard,
        ContentType = FileConsentCard.ContentType,
        Name = filename,
    };
    var replyActivity = turnContext.Activity.CreateReply();
    replyActivity.Attachments = new List<Attachment>() { asAttachment };
    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

## <a name="code-sample"></a>Пример кода

В следующем примере кода показано, как получить согласие для файла и отправить файлы в Teams из бота:

|**Название примера** | **Описание** | **.NET** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| File upload | Показывает, как получить согласие для файла и отправить файлы в Teams из бота. Также показывает, как получить файл, отправленный в бот. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте [пошаговым инструкциям](../../sbs-file-handling-in-bot.yml) по отправке файла в Teams с помощью бота.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Оптимизация бота с ограничением скорости в Teams](~/bots/how-to/rate-limit.md)

## <a name="see-also"></a>См. также

[Защищенные API в Microsoft Teams](/graph/teams-protected-apis)
