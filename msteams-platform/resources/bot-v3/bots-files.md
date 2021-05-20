---
title: Отправка и получение файлов от бота
description: Описывает, как отправлять и получать файлы от бота
keywords: команды ботов файлы отправить получить
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: f69a6ca9cfcdf3b1e559fbe8cf569accf3166f69
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566483"
---
# <a name="send-and-receive-files-through-your-bot"></a>Отправка и получение файлов через бота

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Существует два способа отправки файлов боту и от него:

* Использование API-Graph Майкрософт. Этот метод работает для ботов во всех сферах Teams:
  * `personal`
  * `channel`
  * `groupchat`
* Использование Teams API. Эти файлы поддержки только в одном контексте:
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>Использование API-Graph Майкрософт

Вы можете отправлять сообщения с вложениями карт, ссылаясь на существующие SharePoint файлы, используя API-Graph Майкрософт [для OneDrive и SharePoint](/onedrive/developer/rest-api/). Использование Graph API требует получения доступа к папке OneDrive пользователя (для и файлов) или файлам `personal` `groupchat` в каналах команды (для `channel` файлов) через стандартный поток авторизации OAuth 2.0. Этот метод работает во Teams сферах.

## <a name="using-the-teams-bot-apis"></a>Использование Teams Bot

> [!NOTE]
> Этот метод работает только в `personal` контексте. Он не работает в `channel` `groupchat` контексте или контексте.

Ваш бот может напрямую отправлять и получать файлы с пользователями в `personal` контексте, также известном как личные чаты, используя Teams API. Это позволяет реализовать отчетность о расходах, распознавание изображений, архив файлов, электронные подписи и другие сценарии, связанные с прямым манипулированием содержимого файла. Файлы, Teams обычно отображаются в качестве карт, и позволяют богатые в приложении просмотра.

Следующие разделы описывают, как это сделать, чтобы отправить содержимое файла в результате прямого взаимодействия с пользователем, например отправки сообщения. Этот API предоставляется в рамках платформы Microsoft Teams Bot.

### <a name="configure-your-bot-to-support-files"></a>Настройте бота для поддержки файлов

Для того, чтобы отправить и получить файлы в вашем боте, вы должны `supportsFiles` установить свойство в манифесте `true` . Это свойство описано в [разделе ботов](~/resources/schema/manifest-schema.md#bots) ссылки Manifest.

Определение будет выглядеть так: `"supportsFiles": true` . Если ваш бот не `supportsFiles` включает, следующие функции не будут работать.

### <a name="receiving-files-in-personal-chat"></a>Получение файлов в личном чате

Когда пользователь отправляет файл вашему боту, файл сначала загружается в хранилище OneDrive для бизнеса пользователя. Ваш бот получит сообщение о загрузке. Действие будет содержать метаданные файлов, такие как его имя и URL-адрес содержимого. Вы можете непосредственно прочитать из этого URL, чтобы получить его двоичное содержание.

#### <a name="message-activity-with-file-attachment-example"></a>Активность сообщений с примером вложения файла

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

В следующей таблице описаны свойства содержимого приложения:

| Свойство | Назначение |
| --- | --- |
| `downloadUrl` | OneDrive URL для извлечения содержимого файла. Вы можете выдать `HTTP GET` непосредственно из этого URL. |
| `uniqueId` | Уникальный идентификатор файла. Это будет OneDrive идентификатор элемента диска, в случае, если пользователь отправляет файл вашему боту. |
| `fileType` | Тип расширения файла, например pdf или docx. |

Как наилучшее решение, вы должны признать загрузку файла, отправив обратно сообщение пользователю.

### <a name="uploading-files-to-personal-chat"></a>Загрузка файлов в личный чат

Загрузка файла пользователю включает в себя следующие шаги:

1. Отправить сообщение пользователю с просьбой разрешить его написать. Это сообщение должно содержать `FileConsentCard` вложение с именем файла, который будет загружен.
2. Если пользователь принимает загрузку файла, ваш бот получит действие *Invoke* с URL-адресом местоположения.
3. Чтобы передать файл, ваш бот выполняет непосредственно `HTTP POST` в предоставленный URL-адрес местоположения.
4. По желанию, вы можете удалить оригинал карты согласия, если вы не хотите, чтобы позволить пользователю принять дальнейшие загрузки того же файла.

#### <a name="message-requesting-permission-to-upload"></a>Сообщение с просьбой разрешить загрузку

Это настольное сообщение содержит простой объект вложения с просьбой разрешить пользователю загрузить файл:

![Скриншот карты согласия с просьбой разрешить пользователю загружать файл](../../assets/images/bots/bot-file-consent-card.png)

Это мобильное сообщение содержит объект вложения с просьбой разрешить пользователю загрузить файл:

![Скриншот карты согласия с просьбой разрешить пользователю загружать файл на мобильный](../../assets/images/bots/mobile-bot-file-consent-card.png)

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

В следующей таблице описаны свойства содержимого приложения:

| Свойство | Назначение |
| --- | --- |
| `description` | Описание файла. Может быть показан пользователю, чтобы описать его цель или обобщить его содержание. |
| `sizeInBytes` | Предоставляет пользователю оценку размера файла и количества места, которое он займет в OneDrive. |
| `acceptContext` | Дополнительный контекст, который будет молча передаваться вашему боту, когда пользователь принимает файл. |
| `declineContext` | Дополнительный контекст, который будет молча передаваться вашему боту, когда пользователь откажется от файла. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Вызвать действие, когда пользователь принимает файл

Действие вызова отправляется вашему боту, если пользователь принимает файл. Он содержит OneDrive для бизнеса- и заполнителя URL, который ваш бот может `PUT` затем выдать для передачи содержимого файла. для получения информации о загрузке на OneDrive URL прочитайте эту [статью: Upload байты на сессию загрузки](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).

В следующем примере показана сокращенная версия действия вызова, которую получит ваш бот:

```json
{
  ...

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

Аналогичным образом, если пользователь отклоняет файл, ваш бот получит следующее событие с тем же общим именем активности:

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

### <a name="notifying-the-user-about-an-uploaded-file"></a>Уведомление пользователя о загруженном файле

После загрузки файла в сайт пользователя OneDrive используете ли вы описанный выше механизм или OneDrive делегированных API, вы должны отправить пользователю сообщение о подтверждении. Это сообщение должно содержать `FileCard` вложение, на которое пользователь может нажать, либо для его просмотра, открыть его в OneDrive, либо загрузить локально.

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

В следующей таблице описаны свойства содержимого приложения:

| Свойство | Назначение |
| --- | --- |
| `uniqueId` | OneDrive/SharePoint идентификатор элемента диска. |
| `fileType` | Тип файла, например pdf или docx. |

### <a name="basic-example-in-c"></a>Основной пример в C #

Следующий пример показывает, как вы можете обрабатывать загрузки файлов и отправлять запросы на согласие файлов в диалоге вашего бота:

```csharp

// This sample dialog shows two simple flows:
// 1) A silly example of receiving a file from the user, processing the key elements,
//    and then constructing the attachment and sending it back.
// 2) Creating a new file consent card requesting user permission to upload a file.
private async Task MessageReceivedAsync(IDialogContext context, IAwaitable<object> result)
{
    var replyMessage = context.MakeMessage();
    Attachment returnCard;

    var message = await result as Activity;

    // Check to see if the user is sending the bot a file.
    if (message.Attachments != null && message.Attachments.Any())
    {
        var attachment = message.Attachments.First();

        if (attachment.ContentType == FileDownloadInfo.ContentType)
        {
            FileDownloadInfo downloadInfo = (attachment.Content as JObject).ToObject<FileDownloadInfo>();
            if (downloadInfo != null)
            {
                returnCard = CreateFileInfoAttachment(downloadInfo, attachment.Name, attachment.ContentUrl);
                replyMessage.Attachments.Add(returnCard);
            }
        }
    }
    else
    {
        // Illustrates creating a file consent card.
        returnCard = CreateFileConsentAttachment();
        replyMessage.Attachments.Add(returnCard);
    }
    await context.PostAsync(replyMessage);
}


private static Attachment CreateFileInfoAttachment(FileDownloadInfo downloadInfo, string name, string contentUrl)
{
    FileInfoCard card = new FileInfoCard()
    {
        FileType = downloadInfo.FileType,
        UniqueId = downloadInfo.UniqueId
    };

    Attachment att = card.ToAttachment();
    att.ContentUrl = contentUrl;
    att.Name = name;

    return att;
}

private static Attachment CreateFileConsentAttachment()
{
    JObject acceptContext = new JObject();
    // Fill in any additional context to be sent back when the user accepts the file.

    JObject declineContext = new JObject();
    // Fill in any additional context to be sent back when the user declines the file.

    FileConsentCard card = new FileConsentCard()
    {
        AcceptContext = acceptContext,
        DeclineContext = declineContext,
        SizeInBytes = 102635,
        Description = "File description"
    };

    Attachment att = card.ToAttachment();
    att.Name = "Example file";

    return att;
}
```
