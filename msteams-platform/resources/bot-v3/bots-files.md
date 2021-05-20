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
# <a name="send-and-receive-files-through-your-bot"></a><span data-ttu-id="5a1bd-104">Отправка и получение файлов через бота</span><span class="sxs-lookup"><span data-stu-id="5a1bd-104">Send and receive files through your bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="5a1bd-105">Существует два способа отправки файлов боту и от него:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-105">There are two ways to send files to and from a bot:</span></span>

* <span data-ttu-id="5a1bd-106">Использование API-Graph Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-106">Using the Microsoft Graph APIs.</span></span> <span data-ttu-id="5a1bd-107">Этот метод работает для ботов во всех сферах Teams:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-107">This method works for bots in all scopes in Teams:</span></span>
  * `personal`
  * `channel`
  * `groupchat`
* <span data-ttu-id="5a1bd-108">Использование Teams API.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-108">Using the Teams APIs.</span></span> <span data-ttu-id="5a1bd-109">Эти файлы поддержки только в одном контексте:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-109">These only support files in one context:</span></span>
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a><span data-ttu-id="5a1bd-110">Использование API-Graph Майкрософт</span><span class="sxs-lookup"><span data-stu-id="5a1bd-110">Using the Microsoft Graph APIs</span></span>

<span data-ttu-id="5a1bd-111">Вы можете отправлять сообщения с вложениями карт, ссылаясь на существующие SharePoint файлы, используя API-Graph Майкрософт [для OneDrive и SharePoint](/onedrive/developer/rest-api/).</span><span class="sxs-lookup"><span data-stu-id="5a1bd-111">You can post messages with card attachments referencing existing SharePoint files using the Microsoft Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="5a1bd-112">Использование Graph API требует получения доступа к папке OneDrive пользователя (для и файлов) или файлам `personal` `groupchat` в каналах команды (для `channel` файлов) через стандартный поток авторизации OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-112">Using the Graph APIs requires obtaining access to a user's OneDrive folder (for `personal` and `groupchat` files) or the files in a team's channels (for `channel` files) through the standard OAuth 2.0 authorization flow.</span></span> <span data-ttu-id="5a1bd-113">Этот метод работает во Teams сферах.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-113">This method works in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="5a1bd-114">Использование Teams Bot</span><span class="sxs-lookup"><span data-stu-id="5a1bd-114">Using the Teams Bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="5a1bd-115">Этот метод работает только в `personal` контексте.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-115">This method works only in the `personal` context.</span></span> <span data-ttu-id="5a1bd-116">Он не работает в `channel` `groupchat` контексте или контексте.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-116">It does not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="5a1bd-117">Ваш бот может напрямую отправлять и получать файлы с пользователями в `personal` контексте, также известном как личные чаты, используя Teams API.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-117">Your bot can directly send and receive files with users in the `personal` context, also known as personal chats, using Teams APIs.</span></span> <span data-ttu-id="5a1bd-118">Это позволяет реализовать отчетность о расходах, распознавание изображений, архив файлов, электронные подписи и другие сценарии, связанные с прямым манипулированием содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-118">This lets you implement expense reporting, image recognition, file archival, e-signatures, and other scenarios involving direct manipulation of file content.</span></span> <span data-ttu-id="5a1bd-119">Файлы, Teams обычно отображаются в качестве карт, и позволяют богатые в приложении просмотра.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-119">Files shared in Teams typically appear as cards, and allow rich in-app viewing.</span></span>

<span data-ttu-id="5a1bd-120">Следующие разделы описывают, как это сделать, чтобы отправить содержимое файла в результате прямого взаимодействия с пользователем, например отправки сообщения.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-120">The following sections describe how to do this to send file content as a result of direct user interaction, like sending a message.</span></span> <span data-ttu-id="5a1bd-121">Этот API предоставляется в рамках платформы Microsoft Teams Bot.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-121">This API is provided as part of the Microsoft Teams Bot Platform.</span></span>

### <a name="configure-your-bot-to-support-files"></a><span data-ttu-id="5a1bd-122">Настройте бота для поддержки файлов</span><span class="sxs-lookup"><span data-stu-id="5a1bd-122">Configure your bot to support files</span></span>

<span data-ttu-id="5a1bd-123">Для того, чтобы отправить и получить файлы в вашем боте, вы должны `supportsFiles` установить свойство в манифесте `true` .</span><span class="sxs-lookup"><span data-stu-id="5a1bd-123">In order to send and receive files in your bot, you have to set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="5a1bd-124">Это свойство описано в [разделе ботов](~/resources/schema/manifest-schema.md#bots) ссылки Manifest.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-124">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="5a1bd-125">Определение будет выглядеть так: `"supportsFiles": true` .</span><span class="sxs-lookup"><span data-stu-id="5a1bd-125">The definition will look like this: `"supportsFiles": true`.</span></span> <span data-ttu-id="5a1bd-126">Если ваш бот не `supportsFiles` включает, следующие функции не будут работать.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-126">If your bot does not enable `supportsFiles`, the following features will not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="5a1bd-127">Получение файлов в личном чате</span><span class="sxs-lookup"><span data-stu-id="5a1bd-127">Receiving files in personal chat</span></span>

<span data-ttu-id="5a1bd-128">Когда пользователь отправляет файл вашему боту, файл сначала загружается в хранилище OneDrive для бизнеса пользователя.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-128">When a user sends a file to your bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="5a1bd-129">Ваш бот получит сообщение о загрузке.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-129">Your bot will then receive a message activity notifying you of the user upload.</span></span> <span data-ttu-id="5a1bd-130">Действие будет содержать метаданные файлов, такие как его имя и URL-адрес содержимого.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-130">The activity will contain file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="5a1bd-131">Вы можете непосредственно прочитать из этого URL, чтобы получить его двоичное содержание.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-131">You can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="5a1bd-132">Активность сообщений с примером вложения файла</span><span class="sxs-lookup"><span data-stu-id="5a1bd-132">Message activity with file attachment example</span></span>

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

<span data-ttu-id="5a1bd-133">В следующей таблице описаны свойства содержимого приложения:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-133">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="5a1bd-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="5a1bd-134">Property</span></span> | <span data-ttu-id="5a1bd-135">Назначение</span><span class="sxs-lookup"><span data-stu-id="5a1bd-135">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="5a1bd-136">OneDrive URL для извлечения содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-136">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="5a1bd-137">Вы можете выдать `HTTP GET` непосредственно из этого URL.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-137">You can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="5a1bd-138">Уникальный идентификатор файла.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-138">Unique file ID.</span></span> <span data-ttu-id="5a1bd-139">Это будет OneDrive идентификатор элемента диска, в случае, если пользователь отправляет файл вашему боту.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-139">This will be the OneDrive drive item ID, in the case of the user sending a file to your bot.</span></span> |
| `fileType` | <span data-ttu-id="5a1bd-140">Тип расширения файла, например pdf или docx.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-140">File extension type, such as pdf or docx.</span></span> |

<span data-ttu-id="5a1bd-141">Как наилучшее решение, вы должны признать загрузку файла, отправив обратно сообщение пользователю.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-141">As a best practice, you should acknowledge the file upload by sending back a message to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="5a1bd-142">Загрузка файлов в личный чат</span><span class="sxs-lookup"><span data-stu-id="5a1bd-142">Uploading files to personal chat</span></span>

<span data-ttu-id="5a1bd-143">Загрузка файла пользователю включает в себя следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-143">Uploading a file to a user involves the following steps:</span></span>

1. <span data-ttu-id="5a1bd-144">Отправить сообщение пользователю с просьбой разрешить его написать.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-144">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="5a1bd-145">Это сообщение должно содержать `FileConsentCard` вложение с именем файла, который будет загружен.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-145">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="5a1bd-146">Если пользователь принимает загрузку файла, ваш бот получит действие *Invoke* с URL-адресом местоположения.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-146">If the user accepts the file download, your bot will receive an *Invoke* activity with a location URL.</span></span>
3. <span data-ttu-id="5a1bd-147">Чтобы передать файл, ваш бот выполняет непосредственно `HTTP POST` в предоставленный URL-адрес местоположения.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-147">To transfer the file, your bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="5a1bd-148">По желанию, вы можете удалить оригинал карты согласия, если вы не хотите, чтобы позволить пользователю принять дальнейшие загрузки того же файла.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-148">Optionally, you can remove the original consent card if you do not want to allow the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="5a1bd-149">Сообщение с просьбой разрешить загрузку</span><span class="sxs-lookup"><span data-stu-id="5a1bd-149">Message requesting permission to upload</span></span>

<span data-ttu-id="5a1bd-150">Это настольное сообщение содержит простой объект вложения с просьбой разрешить пользователю загрузить файл:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-150">This desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![Скриншот карты согласия с просьбой разрешить пользователю загружать файл](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="5a1bd-152">Это мобильное сообщение содержит объект вложения с просьбой разрешить пользователю загрузить файл:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-152">This mobile message contains an attachment object requesting user permission to upload the file:</span></span>

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

<span data-ttu-id="5a1bd-154">В следующей таблице описаны свойства содержимого приложения:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-154">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="5a1bd-155">Свойство</span><span class="sxs-lookup"><span data-stu-id="5a1bd-155">Property</span></span> | <span data-ttu-id="5a1bd-156">Назначение</span><span class="sxs-lookup"><span data-stu-id="5a1bd-156">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="5a1bd-157">Описание файла.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-157">Description of the file.</span></span> <span data-ttu-id="5a1bd-158">Может быть показан пользователю, чтобы описать его цель или обобщить его содержание.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-158">May be shown to the user to describe its purpose or to summarize its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="5a1bd-159">Предоставляет пользователю оценку размера файла и количества места, которое он займет в OneDrive.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-159">Provides the user an estimate of the file size and the amount of space it will take in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="5a1bd-160">Дополнительный контекст, который будет молча передаваться вашему боту, когда пользователь принимает файл.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-160">Additional context that will be silently transmitted to your bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="5a1bd-161">Дополнительный контекст, который будет молча передаваться вашему боту, когда пользователь откажется от файла.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-161">Additional context that will be silently transmitted to your bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="5a1bd-162">Вызвать действие, когда пользователь принимает файл</span><span class="sxs-lookup"><span data-stu-id="5a1bd-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="5a1bd-163">Действие вызова отправляется вашему боту, если пользователь принимает файл.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-163">An invoke activity is sent to your bot if and when the user accepts the file.</span></span> <span data-ttu-id="5a1bd-164">Он содержит OneDrive для бизнеса- и заполнителя URL, который ваш бот может `PUT` затем выдать для передачи содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-164">It contains the OneDrive for Business placeholder URL that your bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="5a1bd-165">для получения информации о загрузке на OneDrive URL прочитайте эту [статью: Upload байты на сессию загрузки](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span><span class="sxs-lookup"><span data-stu-id="5a1bd-165">for information on uploading to the OneDrive URL read this article: [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="5a1bd-166">В следующем примере показана сокращенная версия действия вызова, которую получит ваш бот:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-166">The following example shows an abridged version of the invoke activity that your bot will receive:</span></span>

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

<span data-ttu-id="5a1bd-167">Аналогичным образом, если пользователь отклоняет файл, ваш бот получит следующее событие с тем же общим именем активности:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-167">Similarly, if the user declines the file, your bot will receive the following event, with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="5a1bd-168">Уведомление пользователя о загруженном файле</span><span class="sxs-lookup"><span data-stu-id="5a1bd-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="5a1bd-169">После загрузки файла в сайт пользователя OneDrive используете ли вы описанный выше механизм или OneDrive делегированных API, вы должны отправить пользователю сообщение о подтверждении.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-169">After uploading a file to the user's OneDrive, whether you use the mechanism described above or OneDrive user delegated APIs, you should send a confirmation message to the user.</span></span> <span data-ttu-id="5a1bd-170">Это сообщение должно содержать `FileCard` вложение, на которое пользователь может нажать, либо для его просмотра, открыть его в OneDrive, либо загрузить локально.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-170">This message should contain  a `FileCard` attachment that the user can click on, either to preview it, open it in OneDrive, or download locally.</span></span>

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

<span data-ttu-id="5a1bd-171">В следующей таблице описаны свойства содержимого приложения:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-171">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="5a1bd-172">Свойство</span><span class="sxs-lookup"><span data-stu-id="5a1bd-172">Property</span></span> | <span data-ttu-id="5a1bd-173">Назначение</span><span class="sxs-lookup"><span data-stu-id="5a1bd-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="5a1bd-174">OneDrive/SharePoint идентификатор элемента диска.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-174">OneDrive/SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="5a1bd-175">Тип файла, например pdf или docx.</span><span class="sxs-lookup"><span data-stu-id="5a1bd-175">File type, such as pdf or docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="5a1bd-176">Основной пример в C #</span><span class="sxs-lookup"><span data-stu-id="5a1bd-176">Basic example in C#</span></span>

<span data-ttu-id="5a1bd-177">Следующий пример показывает, как вы можете обрабатывать загрузки файлов и отправлять запросы на согласие файлов в диалоге вашего бота:</span><span class="sxs-lookup"><span data-stu-id="5a1bd-177">The following sample shows how you can handle file uploads and send file consent requests in your bot's dialog:</span></span>

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
