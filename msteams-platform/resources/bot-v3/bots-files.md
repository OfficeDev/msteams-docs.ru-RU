---
title: Отправка и получение файлов от бота
description: Описание отправки и получения файлов от бота
keywords: командные файлы ботов отправляют получение
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
# <a name="send-and-receive-files-through-your-bot"></a>Отправка и получение файлов через бот

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Существует два способа отправки файлов в бот и из него:

* Использование API Graph Microsoft. Этот метод работает для ботов во всех Teams:
  * `personal`
  * `channel`
  * `groupchat`
* Использование Teams API. Эти файлы поддерживаются только в одном контексте:
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>Использование API Graph Microsoft

Вы можете отправлять сообщения с привязкой к существующим файлам SharePoint с помощью API Microsoft Graph для OneDrive [и SharePoint](/onedrive/developer/rest-api/). Использование Graph API требует получения доступа к папке OneDrive пользователя (для и файлов) или файлам в каналах группы (для файлов) через стандартный поток авторизации `personal` `groupchat` `channel` OAuth 2.0. Этот метод работает во всех Teams области.

## <a name="using-the-teams-bot-apis"></a>Использование API Teams бота

> [!NOTE]
> Этот метод работает только в `personal` контексте. Он не работает в `channel` контексте или `groupchat` в контексте.

Бот может напрямую отправлять и получать файлы с пользователями в контексте, также известном как `personal` личные чаты, Teams API. Это позволяет реализовать отчеты о расходах, распознавание изображений, архивация файлов, электронные подписи и другие сценарии, связанные с прямыми манипуляциями с контентом файлов. Файлы, Teams обычно отображаются в качестве карт и позволяют просматривать в приложении.

В следующих разделах описано, как это сделать для отправки контента файла в результате прямого взаимодействия с пользователем, например отправки сообщения. Этот API предоставляется в рамках платформы Microsoft Teams Бота.

### <a name="configure-your-bot-to-support-files"></a>Настройка бота для поддержки файлов

Для отправки и получения файлов в боте необходимо заказать свойство `supportsFiles` в манифесте `true` . Это свойство описано в разделе [боты](~/resources/schema/manifest-schema.md#bots) в справке Манифест.

Определение будет выглядеть так: `"supportsFiles": true` . Если бот не `supportsFiles` включает, следующие функции не будут работать.

### <a name="receiving-files-in-personal-chat"></a>Получение файлов в личном чате

Когда пользователь отправляет файл боту, он сначала отправляется в хранилище OneDrive для бизнеса пользователя. После этого бот получит сообщение о загрузке пользователя. Действие будет содержать метаданные файлов, такие как его имя и URL-адрес контента. Вы можете напрямую читать с этого URL-адреса, чтобы получить его двоичный контент.

#### <a name="message-activity-with-file-attachment-example"></a>Действие сообщения с примером вложения файлов

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
| `downloadUrl` | OneDrive URL-адрес для получения содержимого файла. Вы можете `HTTP GET` выдать прямо из этого URL-адреса. |
| `uniqueId` | Уникальный файл ID. Это будет OneDrive элемента диска, если пользователь отправляет файл боту. |
| `fileType` | Тип расширения файлов, например pdf или docx. |

В качестве наилучшей практики следует признать отправку файла, отправив сообщение пользователю.

### <a name="uploading-files-to-personal-chat"></a>Отправка файлов в личный чат

Отправка файла пользователю включает в себя следующие действия:

1. Отправьте сообщение пользователю с запросом разрешения на написание файла. Это сообщение должно содержать `FileConsentCard` вложение с именем загружаемого файла.
2. Если пользователь принимает загрузку файла, ваш бот получит действие *Invoke* с URL-адресом расположения.
3. Чтобы передать файл, бот выполняет непосредственно `HTTP POST` в url-адрес предоставленного расположения.
4. Кроме того, вы можете удалить исходную карту согласия, если вы не хотите разрешить пользователю принимать дальнейшие загрузки того же файла.

#### <a name="message-requesting-permission-to-upload"></a>Сообщение с запросом разрешения на отправку

Это настольное сообщение содержит простой объект вложения, запрашивающий разрешение пользователя на отправку файла:

![Снимок экрана карты согласия с запросом разрешения пользователя на отправку файла](../../assets/images/bots/bot-file-consent-card.png)

Это мобильное сообщение содержит объект вложения с запросом разрешения пользователя на отправку файла:

![Снимок экрана карты согласия с запросом разрешения пользователя на отправку файла на мобильный телефон](../../assets/images/bots/mobile-bot-file-consent-card.png)

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
| `description` | Описание файла. Может быть показано пользователю, чтобы описать его назначение или обобщить его содержимое. |
| `sizeInBytes` | Предоставляет пользователю оценку размера файла и объема пространства, который он займет в OneDrive. |
| `acceptContext` | Дополнительный контекст, который будет безмолвно передан вашему боту при приеме файла пользователем. |
| `declineContext` | Дополнительный контекст, который будет безмолвно передан вашему боту при отклонении файла пользователем. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Вызов активности при приеме файла пользователем

Действие вызова отправляется боту, если пользователь принимает файл и когда он принимает его. Он содержит URL-OneDrive для бизнеса, который затем может выдать бот для передачи `PUT` содержимого файла. сведения о загрузке в URL OneDrive прочитайте эту статью: Upload к [сеансу загрузки.](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)

В следующем примере показана сокращенная версия действия вызова, которую получит бот:

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

Аналогично, если пользователь отклонит файл, ваш бот получит следующее событие с таким же общим именем действий:

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

После отправки файла в OneDrive пользователя, независимо от того, используете ли вы механизм, описанный выше, или OneDrive делегированную API пользователя, следует отправить пользователю сообщение подтверждения. Это сообщение должно содержать вложение, на которое пользователь может нажать, чтобы просмотреть его, открыть его в OneDrive или скачать `FileCard` локально.

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
| `uniqueId` | OneDrive/SharePoint элемента диска. |
| `fileType` | Тип файла, например pdf или docx. |

### <a name="basic-example-in-c"></a>Базовый пример в C #

В следующем примере показано, как обрабатывать отправку файлов и отправлять запросы на согласие на файл в диалоговом окте бота:

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
