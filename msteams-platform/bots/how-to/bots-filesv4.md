---
title: Отправка и получение файлов через бот
description: Узнайте, как отправлять и получать файлы через бота, используйте Graph API для всех Teams области, используйте API Teams с помощью примеров кода и примеров.
keywords: командные файлы ботов отправляют получение
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: ec77aeff3771efd648b77215ca2eb53a4bcad8e9
ms.sourcegitcommit: bfa9d24f736fb8915a9e3ef09c47dbe29a950cb5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/14/2022
ms.locfileid: "62801357"
---
# <a name="send-and-receive-files-through-the-bot"></a>Отправка и получение файлов через бот

> [!IMPORTANT]
> Статьи в этом документе основаны на SDK bot Framework v4.

Существует два способа отправки файлов и получения файлов от бота:

* [**Используйте API microsoft Graph:**](#use-the-graph-apis) этот метод работает для ботов во всех Microsoft Teams области:
  * `personal`
  * `channel`
  * `groupchat`

* [**Используйте API Teams бота:**](#use-the-teams-bot-apis) это только файлы поддержки в контексте`personal`.

## <a name="use-the-graph-apis"></a>Использование Graph API

Отправлять сообщения с вложениями карт, которые относятся к существующим SharePoint файлам, используя Graph API для OneDrive [и SharePoint](/onedrive/developer/rest-api/). Чтобы использовать Graph API, получите доступ к следующему через стандартный поток авторизации OAuth 2.0:

* Папка OneDrive и `personal` файлы `groupchat` пользователя.
* Файлы в канале группы для файлов `channel` .

Graph API работают во всех Teams области. Дополнительные сведения см. в [сообщении отправки вложений в файл чата](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true).

Кроме того, вы можете отправлять файлы и получать файлы от бота с помощью API Teams бота.

## <a name="use-the-teams-bot-apis"></a>Использование API Teams бота

> [!NOTE]
> Teams API бота работают только в контексте`personal`. Они не работают в контексте `channel` или в `groupchat` контексте.

С Teams API бот `personal` может напрямую отправлять и получать файлы с пользователями в контексте, также известном как личные чаты. Реализуют такие функции, как отчет о расходах, распознавание изображений, архивные файлы и электронные подписи, связанные с редактированием контента файлов. Файлы, Teams обычно отображаются в качестве карт и позволяют просматривать в приложении.

В следующих разделах описывается отправка контента файлов в качестве прямого взаимодействия с пользователем, например отправки сообщения. Этот API предоставляется в рамках платформы Teams бота.

### <a name="configure-the-bot-to-support-files"></a>Настройка бота для поддержки файлов

Чтобы отправить и получить файлы в боте, установите `supportsFiles` свойство в манифесте `true`. Это свойство описано в разделе [боты](~/resources/schema/manifest-schema.md#bots) в справке Манифест.

Определение выглядит так. `"supportsFiles": true` Если бот не включает `supportsFiles`, функции, перечисленные в этом разделе, не работают.

### <a name="receive-files-in-personal-chat"></a>Получение файлов в личном чате

Когда пользователь отправляет файл боту, он сначала отправляется в OneDrive для бизнес-хранилища. Затем бот получает сообщение, уведомляя пользователя о загрузке пользователя. Действие содержит метаданные файлов, такие как его имя и URL-адрес контента. Пользователь может напрямую читать с этого URL-адреса, чтобы получить двоичный контент.

#### <a name="message-activity-with-file-attachment-example"></a>Действие сообщения с примером вложения файлов

В следующем коде показан пример активности сообщения с вложением файлов:

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

В следующей таблице описываются свойства контента вложения:

| Свойство | Назначение |
| --- | --- |
| `downloadUrl` | OneDrive URL-адрес для получения контента файла. Пользователь может выдавать прямо из `HTTP GET` этого URL-адреса. |
| `uniqueId` | Уникальный файл ID. Это — OneDrive элемента диска, если пользователь отправляет файл боту. |
| `fileType` | Тип файла, например .pdf или .docx. |

В качестве наилучшей практики подтвердите отправку файла, отправив сообщение пользователю.

### <a name="upload-files-to-personal-chat"></a>Upload в личный чат

**Отправка файла пользователю**

1. Отправьте сообщение пользователю с запросом разрешения на написание файла. Это сообщение должно содержать вложение `FileConsentCard` с именем загружаемого файла.
2. Если пользователь принимает загрузку файла, бот получает действие вызова с URL-адресом расположения.
3. Чтобы передать файл, бот выполняет непосредственно в `HTTP POST` предоставленный URL-адрес расположения.
4. Необязательно удалите исходную карточку согласия, если вы не хотите, чтобы пользователь принял дальнейшие загрузки того же файла.

#### <a name="message-requesting-permission-to-upload"></a>Сообщение с запросом разрешения на отправку

В следующем сообщении рабочего стола содержится простой объект вложения, запрашивающий разрешение пользователя на отправку файла:

![Карточка согласия, запрашивающие разрешение пользователя на отправку файла](../../assets/images/bots/bot-file-consent-card.png)

Следующее мобильное сообщение содержит объект вложения, запрашивающий разрешение пользователя на отправку файла:

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

В следующей таблице описываются свойства контента вложения:

| Свойство | Назначение |
| --- | --- |
| `description` | Описывает назначение файла или суммирует его содержимое. |
| `sizeInBytes` | Предоставляет пользователю оценку размера файла и количества места, необходимого для OneDrive. |
| `acceptContext` | Дополнительный контекст, который безмолвно передается боту, когда пользователь принимает файл. |
| `declineContext` | Дополнительный контекст, который безмолвно передается боту при отклонении файла пользователем. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Вызов активности при приеме файла пользователем

Действие вызова отправляется боту, если и когда пользователь принимает файл. В нем OneDrive для бизнеса URL-адрес, `PUT` который бот может затем выдать для передачи содержимого файла. Сведения о загрузке в URL-адрес OneDrive см. в [ссылке upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).

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

Аналогично, если пользователь отклонив файл, бот получает следующее событие с таким же общим именем действий:

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

### <a name="notifying-the-user-about-an-uploaded-file"></a>Уведомление пользователя о загруженных файлах

После отправки файла в OneDrive отправьте пользователю сообщение подтверждения. Сообщение должно содержать следующее `FileCard` вложение, которое пользователь может выбрать для предварительного просмотра или открытия OneDrive или локальной загрузки:

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

В следующей таблице описываются свойства контента вложения:

| Свойство | Назначение |
| --- | --- |
| `uniqueId` | OneDrive или SharePoint элемента диска. |
| `fileType` | Тип файла, например .pdf или .docx. |

### <a name="fetch-inline-images-from-message"></a>Извлечение нестантных изображений из сообщения

Извлекай в линию изображения, которые являются частью сообщения с помощью маркера доступа Бота.

![Inline image](../../assets/images/bots/inline-image.png)

В следующем коде показан пример получения изображений из сообщения:

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

### <a name="basic-example-in-c"></a>Базовый пример в C #

В следующем коде показан пример обработки отправки файлов и отправки запросов на согласие на файл в диалоговом окте бота:

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

В следующем примере кода показано, как получить согласие на файл и загрузить Teams с бота:

|**Название примера** | **Описание** | **.NET** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| File upload | Демонстрирует, как получить согласие на файл и загрузить Teams с бота. Кроме того, как получить файл, отправленный боту. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте [пошаговом](../../sbs-file-handling-in-bot.yml) руководстве, чтобы загрузить файлы Teams из бота.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Оптимизация бота с ограничением скорости в Teams](~/bots/how-to/rate-limit.md)
