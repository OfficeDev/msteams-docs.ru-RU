---
title: Отправка и получение файлов с помощью Bot
description: Сведения о том, как отправлять и получать файлы с ленты.
keywords: Teams Боты Files Send Receive
ms.date: 05/20/2019
ms.openlocfilehash: b61e7f6934846b3abb1cfc16283cec1d264d7ecc
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452782"
---
# <a name="send-and-receive-files-through-your-bot"></a>Отправка и получение файлов через Bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Существует два способа отправки файлов с помощью Bot:

* С помощью API Microsoft Graph. Этот метод работает для Боты во всех областях в teams:
  * `personal`
  * `channel`
  * `groupchat`
* Использование API Teams. Эти файлы поддерживаются только в одном контексте:
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>Использование API Microsoft Graph

Вы можете размещать сообщения с вложениями карточек, ссылающиеся на существующие файлы SharePoint, с помощью API Microsoft Graph для [OneDrive и SharePoint](/onedrive/developer/rest-api/). Для использования API Graph требуется получение доступа к папке OneDrive пользователя (для `personal` `groupchat` файлов и файлов) или файлам в каналах группы (для `channel` файлов) через стандартный процесс авторизации OAuth 2,0. Этот метод работает во всех областях Teams.

## <a name="using-the-teams-bot-apis"></a>Использование API-интерфейсов Bot для Teams

> [!NOTE]
> Этот метод работает только в `personal` контексте. Он не работает в `channel` `groupchat` контексте или.

С помощью API Teams вы можете напрямую отправлять и получать файлы с пользователями в `personal` контексте, также называемом личными беседами. Это позволяет реализовать отчеты о расходах, распознавание изображений, архивацию файлов, электронные подписи и другие сценарии, затрагивающие прямую обработку содержимого файлов. Файлы, к которым предоставлен общий доступ в Teams, обычно отображаются в виде карточек и позволяют просматривать расширенные возможности просмотра в приложении.

В следующих разделах описано, как это сделать для отправки содержимого файлов в результате прямого взаимодействия с пользователем, например для отправки сообщения. Этот API предоставляется как часть платформы ленты Microsoft Teams.

### <a name="configure-your-bot-to-support-files"></a>Настройка ленты для поддержки файлов

Чтобы отправлять и получать файлы в Bot, необходимо задать `supportsFiles` для свойства в манифесте значение `true` . Это свойство описывается в разделе [Боты](~/resources/schema/manifest-schema.md#bots) ссылки на манифест.

Определение будет выглядеть следующим образом: `"supportsFiles": true` . Если вы не включили ваш робот `supportsFiles` , указанные ниже функции не будут работать.

### <a name="receiving-files-in-personal-chat"></a>Получение файлов в личном чате

Когда пользователь отправляет файл в Bot, сначала он отправляется в хранилище OneDrive для бизнеса пользователя. Затем ваш робот будет получать сообщение о том, что пользователь отправляет сообщение. Действие будет содержать метаданные файлов, такие как имя и URL-адрес контента. Вы можете напрямую прочитать этот URL-адрес, чтобы получить его двоичное содержимое.

#### <a name="message-activity-with-file-attachment-example"></a>Пример активности сообщений с вложенным файлом

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
| `downloadUrl` | URL-адрес OneDrive для извлечения содержимого файла. Вы можете выпустить `HTTP GET` URL-адрес непосредственно из этого URL-адреса. |
| `uniqueId` | Уникальный идентификатор файла. Это будет идентификатор элемента диска OneDrive, если пользователь отправит файл в устройство Bot. |
| `fileType` | Тип расширения файла, например PDF или DOCX. |

Рекомендуется отправить файл, отправив пользователю сообщение...

### <a name="uploading-files-to-personal-chat"></a>Отправка файлов в личный чат

Отправка файла пользователю состоит из следующих этапов:

1. Отправить пользователю сообщение, запрашивающее разрешение на запись файла. Это сообщение должно содержать `FileConsentCard` вложение с именем файла, который необходимо отправить.
2. Если пользователь принимает загрузку файла, он будет получать действие *Invoke* с URL-адресом расположения.
3. Чтобы передать файл, ваш Bot `HTTP POST` напрямую выполняет в указанном URL-адресе расположения.
4. Кроме того, вы можете удалить исходную открытку, если вы не хотите разрешить пользователю принимать дальнейшую отправку того же файла.

#### <a name="message-requesting-permission-to-upload"></a>Сообщение, запрашивающее разрешение на отправку

Это сообщение на рабочем столе содержит простой объект вложения, запрашивающий разрешение пользователя на отправку файла:

![Снимок экрана с картой согласия, запрашивающей разрешение пользователя на отправку файла](../../assets/images/bots/bot-file-consent-card.png)

Это мобильное сообщение содержит объект вложения, запрашивающий разрешение пользователя на отправку файла:

![Снимок экрана с картой согласия, запрашивающей разрешение пользователя на отправку файла на мобильных устройствах](../../assets/images/bots/mobile-bot-file-consent-card.png)

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
| `description` | Описание файла. Может отображаться для пользователя, чтобы описать его назначение или сводную информацию. |
| `sizeInBytes` | Предоставляет пользователю оценку размера файла и объема дискового пространства, которое займет OneDrive. |
| `acceptContext` | Дополнительный контекст, который будет автоматически передаваться в систему робота, когда пользователь принимает файл. |
| `declineContext` | Дополнительный контекст, который будет автоматически передаваться в файл робота, когда пользователь отклоняет файл. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Вызвать действие, когда пользователь принимает файл

Действие Invoke отправляется в Bot в том случае, когда пользователь принимает файл. Он содержит URL-адрес заполнителя OneDrive для бизнеса, который может быть связан с назначением, `PUT` чтобы перенести содержимое файла. для получения сведений об отправке на URL-адрес OneDrive прочитайте эту статью: [Отправка байтов в сеанс отправки](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).

В приведенном ниже примере показана версия абриджед действия Invoke, которое будет получать ваш робот.

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

Аналогичным образом, если пользователь отклоняет файл, ваш робот получит следующее событие с таким же общим именем действия:

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

### <a name="notifying-the-user-about-an-uploaded-file"></a>Уведомление пользователя о отправленном файле

После отправки файла в OneDrive пользователя независимо от того, используется ли механизм, описанный выше, или API, делегированные пользовательские API OneDrive, необходимо отправить пользователю сообщение с подтверждением. Это сообщение должно содержать `FileCard` вложение, которое пользователь может щелкнуть, чтобы просмотреть его, открыть в OneDrive или скачать локально.

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
| `uniqueId` | Идентификатор элемента диска OneDrive или SharePoint. |
| `fileType` | Тип файла, например PDF или DOCX. |

### <a name="basic-example-in-c"></a>Базовый пример в C #

В следующем примере показано, как можно обрабатывать отправку файлов и отправлять запросы на согласие на предоставление файлов в диалоговом окне Bot.

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
