---
title: Отправка и получение файлов от бота
description: Узнайте, как отправлять и получать файлы через бота с использованием API Graph для личной области, области канала и группового чата. Используйте API бота Teams с помощью примеров кода на основе пакета SDK Bot Framework версии 3.
keywords: отправка и получение файлов ботов Teams
ms.topic: how-to
ms.localizationpriority: high
ms.date: 05/20/2019
ms.openlocfilehash: b12e8e79e7d8d5180803004b4e0f238446a8fc98
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65110360"
---
# <a name="send-and-receive-files-through-your-bot"></a>Отправка и получение файлов через бот

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Существует два способа отправки файлов в бот и из бота:

* Использование API Microsoft Graph. Этот метод поддерживается для ботов во всех областях Teams:
  * `personal`
  * `channel`
  * `groupchat`
* Использование API-интерфейсов Teams. Они поддерживают файлы только в одном контексте:
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>Использование API Microsoft Graph

Вы можете публиковать сообщения с вложенными карточками, ссылаясь на существующие файлы SharePoint с помощью API Microsoft Graph для [OneDrive и SharePoint](/onedrive/developer/rest-api/). Для использования API Graph требуется получить доступ к папке OneDrive пользователя (для файлов `personal` и `groupchat`) или файлам в каналах команды (для файлов `channel`) через стандартный поток авторизации OAuth 2.0. Этот метод поддерживается во всех областях Teams.

## <a name="using-the-teams-bot-apis"></a>Использование API бота Teams

> [!NOTE]
> Этот метод поддерживается только в контексте `personal`. Он не поддерживается в контексте `channel` или `groupchat`.

Бот может напрямую отправлять и получать файлы с пользователями в контексте `personal`, также известном как личные чаты, с помощью API Teams. Это позволяет реализовать отчеты о расходах, распознавание изображений, архивацию файлов, электронные подписи и другие сценарии, включающие непосредственное взаимодействие с содержимым файла. Файлы, опубликованные в Teams, обычно отображаются в виде карточек и поддерживают расширенный просмотр в приложении.

В следующих разделах описано, как отправить содержимое файла в результате прямого взаимодействия с пользователем, например при отправке сообщения. Этот API предоставляется в составе Microsoft Teams Bot Platform.

### <a name="configure-your-bot-to-support-files"></a>Настройка бота для поддержки файлов

Чтобы отправлять и получать файлы в боте, настройте для свойства `supportsFiles` в манифесте значение `true`. Это свойство описано в разделе [ботов](~/resources/schema/manifest-schema.md#bots) в справочнике по манифесту.

Определение будет выглядеть следующим образом: `"supportsFiles": true`. Если бот не включает `supportsFiles`, следующие функции не будут работать.

### <a name="receiving-files-in-personal-chat"></a>Получение файлов в личном чате

Когда пользователь отправляет файл вашему боту, файл сначала отправляется в хранилище OneDrive для бизнеса пользователя. Затем бот получает сообщение с уведомлением об отправке пользователем. Оно будет содержать метаданные файла, например его имя и URL-адрес содержимого. Вы можете напрямую считать данные из этого URL-адреса, чтобы получить его двоичное содержимое.

#### <a name="message-activity-with-file-attachment-example"></a>Пример сообщения с вложенным файлом

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
| `downloadUrl` | URL-адрес OneDrive для получения содержимого файла. Вы можете выполнить запрос `HTTP GET` непосредственно из этого URL-адреса. |
| `uniqueId` | Уникальный идентификатор файла. Это идентификатор элемента диска OneDrive, если пользователь отправляет файл вашему боту. |
| `fileType` | Тип расширения файла, например PDF или DOCX. |

Рекомендуется подтвердить отправку файла, отправив обратное сообщение пользователю.

### <a name="uploading-files-to-personal-chat"></a>Отправка файлов в личный чат

Отправка файла пользователю включает в себя следующие действия.

1. Отправка сообщения пользователю с запросом разрешения на запись файла. Это сообщение должно содержать вложение `FileConsentCard` с именем файла для отправки.
2. Если пользователь разрешает скачивание файла, бот получит действие *Invoke* с URL-адресом расположения.
3. Чтобы передать файл, ваш бот выполняет запрос `HTTP POST` непосредственно в указанном URL-адресе расположения.
4. При необходимости вы можете удалить исходную карточку согласия, если не хотите разрешать пользователю принимать дальнейшие отправки того же файла.

#### <a name="message-requesting-permission-to-upload"></a>Сообщение с запросом разрешения на отправку

Это сообщение в классическом интерфейсе содержит простой объект вложения с запросом разрешения пользователя на отправку файла:

![Снимок экрана: карточка согласия с запросом разрешения пользователя на отправку файла](../../assets/images/bots/bot-file-consent-card.png)

Это сообщение в мобильном интерфейсе содержит объект вложения с запросом разрешения пользователя на отправку файла:

![Снимок экрана: карточка согласия с запросом разрешения пользователя на отправку файла на мобильном устройстве](../../assets/images/bots/mobile-bot-file-consent-card.png)

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
| `description` | Описание файла. Может отображаться пользователю для описания назначения или обобщения содержимого. |
| `sizeInBytes` | Предоставляет пользователю оценку размера файла и объема, который он займет в OneDrive. |
| `acceptContext` | Дополнительный контекст, который будет автоматически передан боту, когда пользователь примет файл. |
| `declineContext` | Дополнительный контекст, который будет автоматически передан боту, когда пользователь отклонит файл. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Действие вызова, когда пользователь принимает файл

Действие вызова отправляется боту, если и когда пользователь принимает файл. Оно содержит URL-адрес заполнителя OneDrive для бизнеса, для которого ваш бот может выпустить запрос `PUT`, чтобы передать содержимое файла. Дополнительные сведения об отправке на URL-адрес OneDrive см. в статье [Отправка байтов в сеанс отправки](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).

В следующем примере показана сокращенная версия действия вызова, которое получит ваш бот.

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

Аналогичным образом, если пользователь отклоняет файл, бот получит следующее событие с тем же именем общего действия.

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

После отправки файла в хранилище OneDrive пользователя, если вы используете механизм, описанный выше, или делегированные пользователем API в OneDrive, необходимо отправить пользователю сообщение с подтверждением. Это сообщение должно содержать вложение `FileCard`, которое пользователь может щелкнуть для предварительного просмотра, открыть в OneDrive или скачать локально.

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
| `uniqueId` | Идентификатор элемента диска OneDrive/SharePoint |
| `fileType` | Тип файла, например PDF или DOCX. |

### <a name="basic-example-in-c"></a>Основной пример в C#

В следующем примере показано, как обрабатывать отправку файлов и отправлять запросы согласия на получение файлов в диалоговом окне бота.

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
