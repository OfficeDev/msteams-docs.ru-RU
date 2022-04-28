---
title: Отправка и получение файлов с помощью бота
description: Узнайте, как отправлять и получать файлы с помощью бота с Graph API для личных, каналов и областей groupchat. Используйте Teams API бота, используя примеры кода на основе пакета SDK Bot Framework версии 4.
keywords: teams bots files send receive
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 22c88a435628c34942eb8f5652b9170f861a0446
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102538"
---
# <a name="send-and-receive-files-through-the-bot"></a>Отправка и получение файлов с помощью бота

> [!IMPORTANT]
> Статьи в этом документе основаны на пакете SDK Bot Framework версии 4.

Существует два способа отправки файлов и получения файлов от бота:

* [**Используйте API Graph Майкрософт:**](#use-the-graph-apis) этот метод работает для ботов во всех Microsoft Teams областях:
  * `personal`
  * `channel`
  * `groupchat`

* [**Используйте API Teams бота: они**](#use-the-teams-bot-apis) поддерживают только файлы в контексте`personal`.

## <a name="use-the-graph-apis"></a>Использование Graph API

Публикация сообщений с вложениями карточек, которые ссылаются на существующие SharePoint, с помощью Graph API для OneDrive [и SharePoint](/onedrive/developer/rest-api/). Чтобы использовать Graph API, получите доступ к следующему через стандартный поток авторизации OAuth 2.0:

* Папка OneDrive и `personal` файлы `groupchat` пользователя.
* Файлы в канале команды для файлов `channel` .

Graph API работают во всех Teams областях. Дополнительные сведения см. в [статье "Отправка вложений в файл сообщений чата"](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true).

Кроме того, вы можете отправлять и получать файлы от бота с помощью Teams API бота.

## <a name="use-the-teams-bot-apis"></a>Использование API Teams бота

> [!NOTE]
> Teams API бота работают только в контексте`personal`. Они не работают в контексте `channel` или в контексте `groupchat` .

С Teams API бот `personal` может напрямую отправлять и получать файлы с пользователями в контексте, также известном как личные чаты. Реализуйте такие функции, как отчеты о расходах, распознавание изображений, архивация файлов и электронные подписи, включающие редактирование содержимого файла. Файлы, к Teams обычно отображаются в виде карточек и позволяют просматривать в приложении широкие возможности.

В следующих разделах описывается отправка содержимого файла в виде прямого взаимодействия с пользователем, например отправки сообщения. Этот API предоставляется как часть платформы Teams бота.

### <a name="configure-the-bot-to-support-files"></a>Настройка бота для поддержки файлов

Чтобы отправлять и получать файлы в боте, `supportsFiles` задайте для свойства в манифесте значение `true`. Это свойство описано в разделе [ботов](~/resources/schema/manifest-schema.md#bots) в справочнике по манифесту.

Определение выглядит следующим образом. `"supportsFiles": true` Если бот не включается `supportsFiles`, функции, перечисленные в этом разделе, не работают.

### <a name="receive-files-in-personal-chat"></a>Получение файлов в личном чате

Когда пользователь отправляет файл боту, он сначала отправляется в хранилище OneDrive для бизнеса. Затем бот получает сообщение о действии, уведомляя пользователя об отправке пользователем. Действие содержит метаданные файла, такие как его имя и URL-адрес содержимого. Пользователь может напрямую считывать данные из этого URL-адреса, чтобы получить двоичное содержимое.

#### <a name="message-activity-with-file-attachment-example"></a>Пример действия сообщения с вложением файла

В следующем коде показан пример действия сообщения с вложением файла:

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

В следующей таблице описаны свойства содержимого вложения:

| Свойство | Назначение |
| --- | --- |
| `downloadUrl` | OneDrive URL-адрес для получения содержимого файла. Пользователь может выполнить запрос непосредственно `HTTP GET` из этого URL-адреса. |
| `uniqueId` | Уникальный идентификатор файла. Это идентификатор OneDrive диска, если пользователь отправляет файл боту. |
| `fileType` | Тип файла, например .pdf или .docx. |

Рекомендуется подтвердить отправку файла, отправив сообщение пользователю.

### <a name="upload-files-to-personal-chat"></a>Upload в личный чат

Чтобы отправить файл пользователю:

1. Отправьте сообщение пользователю, запрашивая разрешение на запись файла. Это сообщение должно содержать вложение `FileConsentCard` с именем файла для отправки.
2. Если пользователь принимает скачивание файла, бот получает действие вызова с URL-адресом расположения.
3. Для передачи файла бот выполняет запрос `HTTP POST` непосредственно в указанный URL-адрес расположения.
4. При необходимости удалите исходную карточку согласия, если вы не хотите, чтобы пользователь принял дальнейшие отправки того же файла.

#### <a name="message-requesting-permission-to-upload"></a>Сообщение с запросом разрешения на отправку

Следующее сообщение рабочего стола содержит простой объект вложения с запросом разрешения пользователя на отправку файла:

:::image type="content" source="../../assets/images/bots/bot-file-consent-card.png" alt-text="Карточка согласия с запросом разрешения пользователя на отправку файла"lightbox="../../assets/images/bots/bot-file-consent-card.png"border="true":::

Следующее мобильное сообщение содержит объект вложения с запросом разрешения пользователя на отправку файла:

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

В следующей таблице описаны свойства содержимого вложения:

| Свойство | Назначение |
| --- | --- |
| `description` | Описывает назначение файла или суммирует его содержимое. |
| `sizeInBytes` | Предоставляет пользователю оценку размера файла и объема места, затрачиваемого на OneDrive. |
| `acceptContext` | Дополнительный контекст, который автоматически передается боту, когда пользователь принимает файл. |
| `declineContext` | Дополнительный контекст, который автоматически передается боту, когда пользователь отклоняет файл. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Вызов действия, когда пользователь принимает файл

Действие вызова отправляется боту, если и когда пользователь принимает файл. Он содержит OneDrive для бизнеса URL-адрес `PUT` заполнителя, который бот может затем передать для передачи содержимого файла. Сведения об отправке по URL-адресу OneDrive см. в разделе "Отправка [байтов в сеанс отправки"](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).

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

Аналогичным образом, если пользователь отклоняет файл, бот получает следующее событие с таким же общим именем действия:

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

После отправки файла в OneDrive пользователя отправьте пользователю сообщение с подтверждением. Сообщение должно содержать следующее `FileCard` вложение, которое пользователь может выбрать для предварительного просмотра или открытия в OneDrive или скачать локально:

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

В следующей таблице описаны свойства содержимого вложения:

| Свойство | Назначение |
| --- | --- |
| `uniqueId` | OneDrive или SharePoint диска. |
| `fileType` | Тип файла, например .pdf или .docx. |

### <a name="fetch-inline-images-from-message"></a>Получение встроенных изображений из сообщения

Получение встроенных изображений, которые являются частью сообщения, с помощью маркера доступа бота.

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

### <a name="basic-example-in-c"></a>Базовый пример в C #

В следующем коде показан пример обработки отправки файлов и отправки запросов на согласие файлов в диалоговом окне бота:

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

В следующем примере кода показано, как получить согласие на файл и отправить файлы Teams от бота:

|**Название примера** | **Описание** | **.NET** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| File upload | Демонстрирует, как получить согласие на файл и отправить файлы в Teams от бота. Кроме того, как получить файл, отправленный боту. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Выполните [пошаговое руководство по](../../sbs-file-handling-in-bot.yml) отправке файла в Teams с помощью бота.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Оптимизация бота с ограничением скорости в Teams](~/bots/how-to/rate-limit.md)
