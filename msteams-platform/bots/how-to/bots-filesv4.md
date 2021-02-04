---
title: Отправка и получение файлов с помощью бота
description: Описывает, как отправлять и получать файлы с помощью бота
keywords: отправка файлов ботов teams
ms.date: 05/20/2019
ms.topic: how-to
ms.openlocfilehash: 07967ba4ce6d7e15e64c6f925fa588585f5a2c1d
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093281"
---
# <a name="send-and-receive-files-through-the-bot"></a>Отправка и получение файлов с помощью бота

> [!IMPORTANT]
> Статьи в этом документе основаны на пакете SDK Bot Framework v4.

Существует два способа отправки и получения файлов от бота:

* **Использование API Microsoft Graph:** Этот метод работает для ботов во всех области Microsoft Teams:
  * `personal`
  * `channel`
  * `groupchat`

* **Использование API ботов Teams:** Они поддерживают только файлы в `personal` контексте.

## <a name="using-the-graph-apis"></a>Использование API Graph

Публикация сообщений с вложениями карт, которые ссылаются на существующие файлы SharePoint, с помощью API Graph для [OneDrive и SharePoint.](/onedrive/developer/rest-api/) Чтобы использовать API Graph, получите доступ к любой из следующих типов с помощью стандартного потока авторизации OAuth 2.0:
* Папка oneDrive пользователя и `personal` `groupchat` файлы.
* Файлы в канале команды для `channel` файлов.

API Graph работают во всех области Teams.

## <a name="using-the-teams-bot-apis"></a>Использование API ботов Teams

> [!NOTE]
> API ботов Teams работают только в `personal` контексте. Они не работают в `channel` контексте или в `groupchat` контексте.

С помощью API Teams бот может напрямую отправлять и получать файлы с пользователями в контексте, также известном как `personal` личные чаты. Реализуют такие функции, как отчеты о расходах, распознавание изображений, архив файлов и электронные подписи, включающие редактирование содержимого файла. Файлы, к совместному доступу в Teams, как правило, отображаются как карточки и позволяют просматривать их в приложении.

В следующих разделах описывается, как отправлять содержимое файла как непосредственное взаимодействие с пользователем, например отправка сообщения. Этот API предоставляется в составе платформы ботов Teams.

### <a name="configuring-the-bot-to-support-files"></a>Настройка бота для поддержки файлов

Чтобы отправлять и получать файлы в боте, установите для свойства `supportsFiles` в манифесте его свойство `true` . Это свойство описано в разделе [ботов](~/resources/schema/manifest-schema.md#bots) в справочнике по манифесту.

Определение выглядит `"supportsFiles": true` так: Если бот не включает, `supportsFiles` функции, перечисленные в этом разделе, не работают.

### <a name="receiving-files-in-personal-chat"></a>Получение файлов в личном чате

Когда пользователь отправляет файл боту, он сначала отправляется в хранилище OneDrive для бизнеса пользователя. После этого бот получает сообщение с уведомлением о отправке пользователем. Действие содержит метаданные файла, такие как его имя и URL-адрес контента. Пользователь может напрямую считывать данные с этого URL-адреса, чтобы получить двоичное содержимое.

#### <a name="message-activity-with-file-attachment-example"></a>Пример действий с сообщением с вложенным файлом

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

В следующей таблице описываются свойства содержимого вложения:

| Свойство | Назначение |
| --- | --- |
| `downloadUrl` | URL-адрес OneDrive для получения содержимого файла. Пользователь может выдавать адрес `HTTP GET` непосредственно с этого URL-адреса. |
| `uniqueId` | Уникальный ИД файла. Это ИД элемента диска OneDrive, если пользователь отправляет файл боту. |
| `fileType` | Тип файла, например PDF или DOCX. |

Как лучше всего, подтвердите отправку файла, отправив сообщение обратно пользователю.

### <a name="uploading-files-to-personal-chat"></a>Отправка файлов в личный чат

Для отправки файла пользователю необходимо следующее:

1. Отправьте сообщение пользователю, запрашивая разрешение на написание файла. Это сообщение должно содержать `FileConsentCard` вложение с именем файла, который необходимо отправить.
2. Если пользователь принимает загрузку файла, бот получает действие вызова с URL-адресом расположения.
3. Для передачи файла бот выполняет прямой `HTTP POST` url-адрес расположения.
4. При желании удалите исходную карточку согласия, если вы не хотите, чтобы пользователь мог принимать дальнейшие отправки того же файла.

#### <a name="message-requesting-permission-to-upload"></a>Сообщение, запрашивающие разрешение на отправку

Следующее сообщение на рабочем столе содержит простой объект вложения, запрашивающий разрешение пользователя на отправку файла:

![Карточка согласия с запросом разрешения пользователя на отправку файла](../../assets/images/bots/bot-file-consent-card.png)

Следующее мобильное сообщение содержит объект вложения, запрашивающий разрешение пользователя на отправку файла:

![Карточка согласия с запросом разрешения пользователя на отправку файла на мобильных устройствах](../../assets/images/bots/mobile-bot-file-consent-card.png)

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

В следующей таблице описываются свойства содержимого вложения:

| Свойство | Назначение |
| --- | --- |
| `description` | Описывает назначение файла или суммирует его содержимое. |
| `sizeInBytes` | Предоставляет пользователю оценку размера файла и объема пространства, необходимого в OneDrive. |
| `acceptContext` | Дополнительный контекст, который автоматически передается боту, когда пользователь принимает файл. |
| `declineContext` | Дополнительный контекст, который автоматически передается боту, когда пользователь отклочивает файл. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Вызов действия, когда пользователь принимает файл

Боту отправляется действие вызова, если и когда пользователь принимает файл. Он содержит URL-адрес-замессера OneDrive для бизнеса, который бот может затем выдать для передачи `PUT` содержимого файла. Сведения о загрузке на URL-адрес OneDrive см. в сведениях о отправке [в сеанс отправки.](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)

В следующем примере показана краткий версия действия вызова, получаемого ботом:

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

Аналогично, если пользователь отклонит файл, бот получит следующее событие с таким же общим именем действия:

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

После отправки файла в OneDrive пользователя отправьте пользователю подтверждение. Сообщение должно содержать следующее вложение, которое пользователь может выбрать для предварительного просмотра или открытия в OneDrive, или для `FileCard` локальной загрузки:

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

В следующей таблице описываются свойства содержимого вложения:

| Свойство | Назначение |
| --- | --- |
| `uniqueId` | ИД элемента диска OneDrive или SharePoint. |
| `fileType` | Тип файла, например PDF или DOCX. |

### <a name="fetching-inline-images-from-message"></a>Извлечение в текстовом тексте изображений из сообщения

Получать в тексте изображения, которые являются частью сообщения, с помощью маркера доступа бота.

![Inline image](../../assets/images/bots/inline-image.png)

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

В следующем примере показано, как обрабатывать отправку файлов и отправлять запросы на согласие файла в диалоговом окке бота:

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

### <a name="code-sample"></a>Пример кода

|**Имя примера** | **Описание** | **. NETCore** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| File upload | Демонстрирует, как получить согласие на файл и отправить файлы в Teams от бота. Кроме того, как получить файл, отправленный боту. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |
