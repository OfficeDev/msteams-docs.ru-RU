---
title: Отправка и получение файлов от бота
description: Описание отправки и получения файлов от бота
keywords: командные файлы ботов отправляют получение
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: c5ee32d10e5a6adc5a08d1a0556a18be8367460a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020655"
---
# <a name="send-and-receive-files-through-your-bot"></a><span data-ttu-id="d616d-104">Отправка и получение файлов через бот</span><span class="sxs-lookup"><span data-stu-id="d616d-104">Send and receive files through your bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="d616d-105">Существует два способа отправки файлов в бот и из него:</span><span class="sxs-lookup"><span data-stu-id="d616d-105">There are two ways to send files to and from a bot:</span></span>

* <span data-ttu-id="d616d-106">Использование API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d616d-106">Using the Microsoft Graph APIs.</span></span> <span data-ttu-id="d616d-107">Этот метод работает для ботов во всех сферах в Teams:</span><span class="sxs-lookup"><span data-stu-id="d616d-107">This method works for bots in all scopes in Teams:</span></span>
  * `personal`
  * `channel`
  * `groupchat`
* <span data-ttu-id="d616d-108">Использование API Teams.</span><span class="sxs-lookup"><span data-stu-id="d616d-108">Using the Teams APIs.</span></span> <span data-ttu-id="d616d-109">Эти файлы поддерживаются только в одном контексте:</span><span class="sxs-lookup"><span data-stu-id="d616d-109">These only support files in one context:</span></span>
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a><span data-ttu-id="d616d-110">Использование API Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="d616d-110">Using the Microsoft Graph APIs</span></span>

<span data-ttu-id="d616d-111">Вы можете отправлять сообщения с вложениями карт, ссылаясь на существующие файлы SharePoint с помощью API Microsoft Graph для [OneDrive и SharePoint.](/onedrive/developer/rest-api/)</span><span class="sxs-lookup"><span data-stu-id="d616d-111">You can post messages with card attachments referencing existing SharePoint files using the Microsoft Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="d616d-112">Использование API graph требует получения доступа к папке OneDrive пользователя (для и файлов) или файлам в каналах группы (для файлов) через стандартный поток авторизации `personal` `groupchat` `channel` OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d616d-112">Using the Graph APIs requires obtaining access to a user's OneDrive folder (for `personal` and `groupchat` files) or the files in a team's channels (for `channel` files) through the standard OAuth 2.0 authorization flow.</span></span> <span data-ttu-id="d616d-113">Этот метод работает во всех сферах Teams.</span><span class="sxs-lookup"><span data-stu-id="d616d-113">This method works in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="d616d-114">Использование API bot teams</span><span class="sxs-lookup"><span data-stu-id="d616d-114">Using the Teams Bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="d616d-115">Этот метод работает только в `personal` контексте.</span><span class="sxs-lookup"><span data-stu-id="d616d-115">This method works only in the `personal` context.</span></span> <span data-ttu-id="d616d-116">Он не работает в `channel` контексте или `groupchat` в контексте.</span><span class="sxs-lookup"><span data-stu-id="d616d-116">It does not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="d616d-117">Ваш бот может напрямую отправлять и получать файлы с пользователями в контексте, также известном как личные `personal` чаты, с помощью API Teams.</span><span class="sxs-lookup"><span data-stu-id="d616d-117">Your bot can directly send and receive files with users in the `personal` context, also known as personal chats, using Teams APIs.</span></span> <span data-ttu-id="d616d-118">Это позволяет реализовать отчеты о расходах, распознавание изображений, архивация файлов, электронные подписи и другие сценарии, связанные с прямыми манипуляциями с контентом файлов.</span><span class="sxs-lookup"><span data-stu-id="d616d-118">This lets you implement expense reporting, image recognition, file archival, e-signatures, and other scenarios involving direct manipulation of file content.</span></span> <span data-ttu-id="d616d-119">Файлы, общие в Teams, как правило, отображаются как карты и позволяют просматривать в приложении.</span><span class="sxs-lookup"><span data-stu-id="d616d-119">Files shared in Teams typically appear as cards, and allow rich in-app viewing.</span></span>

<span data-ttu-id="d616d-120">В следующих разделах описано, как это сделать для отправки контента файла в результате прямого взаимодействия с пользователем, например отправки сообщения.</span><span class="sxs-lookup"><span data-stu-id="d616d-120">The following sections describe how to do this to send file content as a result of direct user interaction, like sending a message.</span></span> <span data-ttu-id="d616d-121">Этот API предоставляется в рамках бот-платформы Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d616d-121">This API is provided as part of the Microsoft Teams Bot Platform.</span></span>

### <a name="configure-your-bot-to-support-files"></a><span data-ttu-id="d616d-122">Настройка бота для поддержки файлов</span><span class="sxs-lookup"><span data-stu-id="d616d-122">Configure your bot to support files</span></span>

<span data-ttu-id="d616d-123">Для отправки и получения файлов в боте необходимо заказать свойство `supportsFiles` в манифесте `true` .</span><span class="sxs-lookup"><span data-stu-id="d616d-123">In order to send and receive files in your bot, you have to set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="d616d-124">Это свойство описано в разделе [боты](~/resources/schema/manifest-schema.md#bots) в справке Манифест.</span><span class="sxs-lookup"><span data-stu-id="d616d-124">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="d616d-125">Определение будет выглядеть так: `"supportsFiles": true` .</span><span class="sxs-lookup"><span data-stu-id="d616d-125">The definition will look like this: `"supportsFiles": true`.</span></span> <span data-ttu-id="d616d-126">Если бот не `supportsFiles` включает, следующие функции не будут работать.</span><span class="sxs-lookup"><span data-stu-id="d616d-126">If your bot does not enable `supportsFiles`, the following features will not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="d616d-127">Получение файлов в личном чате</span><span class="sxs-lookup"><span data-stu-id="d616d-127">Receiving files in personal chat</span></span>

<span data-ttu-id="d616d-128">Когда пользователь отправляет файл боту, он сначала отправляется в хранилище OneDrive для бизнеса пользователя.</span><span class="sxs-lookup"><span data-stu-id="d616d-128">When a user sends a file to your bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="d616d-129">После этого бот получит сообщение о загрузке пользователя.</span><span class="sxs-lookup"><span data-stu-id="d616d-129">Your bot will then receive a message activity notifying you of the user upload.</span></span> <span data-ttu-id="d616d-130">Действие будет содержать метаданные файлов, такие как его имя и URL-адрес контента.</span><span class="sxs-lookup"><span data-stu-id="d616d-130">The activity will contain file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="d616d-131">Вы можете напрямую читать с этого URL-адреса, чтобы получить его двоичный контент.</span><span class="sxs-lookup"><span data-stu-id="d616d-131">You can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="d616d-132">Действие сообщения с примером вложения файлов</span><span class="sxs-lookup"><span data-stu-id="d616d-132">Message activity with file attachment example</span></span>

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

<span data-ttu-id="d616d-133">В следующей таблице описываются свойства контента вложения:</span><span class="sxs-lookup"><span data-stu-id="d616d-133">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="d616d-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="d616d-134">Property</span></span> | <span data-ttu-id="d616d-135">Назначение</span><span class="sxs-lookup"><span data-stu-id="d616d-135">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="d616d-136">URL-адрес OneDrive для получения содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="d616d-136">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="d616d-137">Вы можете `HTTP GET` выдать прямо из этого URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="d616d-137">You can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="d616d-138">Уникальный файл ID.</span><span class="sxs-lookup"><span data-stu-id="d616d-138">Unique file ID.</span></span> <span data-ttu-id="d616d-139">Это будет ID элемента диска OneDrive, если пользователь отправляет файл боту.</span><span class="sxs-lookup"><span data-stu-id="d616d-139">This will be the OneDrive drive item ID, in the case of the user sending a file to your bot.</span></span> |
| `fileType` | <span data-ttu-id="d616d-140">Тип расширения файлов, например pdf или docx.</span><span class="sxs-lookup"><span data-stu-id="d616d-140">File extension type, such as pdf or docx.</span></span> |

<span data-ttu-id="d616d-141">В качестве наилучшей практики следует признать отправку файла, отправив сообщение пользователю.</span><span class="sxs-lookup"><span data-stu-id="d616d-141">As a best practice, you should acknowledge the file upload by sending back a message to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="d616d-142">Отправка файлов в личный чат</span><span class="sxs-lookup"><span data-stu-id="d616d-142">Uploading files to personal chat</span></span>

<span data-ttu-id="d616d-143">Отправка файла пользователю включает в себя следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d616d-143">Uploading a file to a user involves the following steps:</span></span>

1. <span data-ttu-id="d616d-144">Отправьте сообщение пользователю с запросом разрешения на написание файла.</span><span class="sxs-lookup"><span data-stu-id="d616d-144">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="d616d-145">Это сообщение должно содержать `FileConsentCard` вложение с именем загружаемого файла.</span><span class="sxs-lookup"><span data-stu-id="d616d-145">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="d616d-146">Если пользователь принимает загрузку файла, ваш бот получит действие *Invoke* с URL-адресом расположения.</span><span class="sxs-lookup"><span data-stu-id="d616d-146">If the user accepts the file download, your bot will receive an *Invoke* activity with a location URL.</span></span>
3. <span data-ttu-id="d616d-147">Чтобы передать файл, бот выполняет непосредственно `HTTP POST` в url-адрес предоставленного расположения.</span><span class="sxs-lookup"><span data-stu-id="d616d-147">To transfer the file, your bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="d616d-148">Кроме того, вы можете удалить исходную карту согласия, если вы не хотите разрешить пользователю принимать дальнейшие загрузки того же файла.</span><span class="sxs-lookup"><span data-stu-id="d616d-148">Optionally, you can remove the original consent card if you do not want to allow the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="d616d-149">Сообщение с запросом разрешения на отправку</span><span class="sxs-lookup"><span data-stu-id="d616d-149">Message requesting permission to upload</span></span>

<span data-ttu-id="d616d-150">Это настольное сообщение содержит простой объект вложения, запрашивающий разрешение пользователя на отправку файла:</span><span class="sxs-lookup"><span data-stu-id="d616d-150">This desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![Снимок экрана карты согласия с запросом разрешения пользователя на отправку файла](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="d616d-152">Это мобильное сообщение содержит объект вложения с запросом разрешения пользователя на отправку файла:</span><span class="sxs-lookup"><span data-stu-id="d616d-152">This mobile message contains an attachment object requesting user permission to upload the file:</span></span>

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

<span data-ttu-id="d616d-154">В следующей таблице описываются свойства контента вложения:</span><span class="sxs-lookup"><span data-stu-id="d616d-154">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="d616d-155">Свойство</span><span class="sxs-lookup"><span data-stu-id="d616d-155">Property</span></span> | <span data-ttu-id="d616d-156">Назначение</span><span class="sxs-lookup"><span data-stu-id="d616d-156">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="d616d-157">Описание файла.</span><span class="sxs-lookup"><span data-stu-id="d616d-157">Description of the file.</span></span> <span data-ttu-id="d616d-158">Может быть показано пользователю, чтобы описать его назначение или обобщить его содержимое.</span><span class="sxs-lookup"><span data-stu-id="d616d-158">May be shown to the user to describe its purpose or to summarize its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="d616d-159">Предоставляет пользователю оценку размера файла и объема пространства, который он займет в OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d616d-159">Provides the user an estimate of the file size and the amount of space it will take in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="d616d-160">Дополнительный контекст, который будет безмолвно передан вашему боту при приеме файла пользователем.</span><span class="sxs-lookup"><span data-stu-id="d616d-160">Additional context that will be silently transmitted to your bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="d616d-161">Дополнительный контекст, который будет безмолвно передан вашему боту при отклонении файла пользователем.</span><span class="sxs-lookup"><span data-stu-id="d616d-161">Additional context that will be silently transmitted to your bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="d616d-162">Вызов активности при приеме файла пользователем</span><span class="sxs-lookup"><span data-stu-id="d616d-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="d616d-163">Действие вызова отправляется боту, если пользователь принимает файл и когда он принимает его.</span><span class="sxs-lookup"><span data-stu-id="d616d-163">An invoke activity is sent to your bot if and when the user accepts the file.</span></span> <span data-ttu-id="d616d-164">В нем содержится URL-адрес для места для бизнеса OneDrive, который бот может затем выдать для передачи `PUT` содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="d616d-164">It contains the OneDrive for Business placeholder URL that your bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="d616d-165">сведения о загрузке в URL-адрес OneDrive читайте в этой статье: [Отправка bytes в сеанс загрузки](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span><span class="sxs-lookup"><span data-stu-id="d616d-165">for information on uploading to the OneDrive URL read this article: [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="d616d-166">В следующем примере показана сокращенная версия действия вызова, которую получит бот:</span><span class="sxs-lookup"><span data-stu-id="d616d-166">The following example shows an abridged version of the invoke activity that your bot will receive:</span></span>

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

<span data-ttu-id="d616d-167">Аналогично, если пользователь отклонит файл, ваш бот получит следующее событие с таким же общим именем действий:</span><span class="sxs-lookup"><span data-stu-id="d616d-167">Similarly, if the user declines the file, your bot will receive the following event, with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="d616d-168">Уведомление пользователя о загруженных файлах</span><span class="sxs-lookup"><span data-stu-id="d616d-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="d616d-169">После отправки файла в OneDrive пользователя, независимо от того, используете ли вы механизм, описанный выше, или делегированную API пользователя OneDrive, следует отправить пользователю сообщение подтверждения.</span><span class="sxs-lookup"><span data-stu-id="d616d-169">After uploading a file to the user's OneDrive, whether you use the mechanism described above or OneDrive user delegated APIs, you should send a confirmation message to the user.</span></span> <span data-ttu-id="d616d-170">Это сообщение должно содержать вложение, на которое пользователь может нажать, чтобы просмотреть его, открыть его в OneDrive или скачать `FileCard` локально.</span><span class="sxs-lookup"><span data-stu-id="d616d-170">This message should contain  a `FileCard` attachment that the user can click on, either to preview it, open it in OneDrive, or download locally.</span></span>

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

<span data-ttu-id="d616d-171">В следующей таблице описываются свойства контента вложения:</span><span class="sxs-lookup"><span data-stu-id="d616d-171">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="d616d-172">Свойство</span><span class="sxs-lookup"><span data-stu-id="d616d-172">Property</span></span> | <span data-ttu-id="d616d-173">Назначение</span><span class="sxs-lookup"><span data-stu-id="d616d-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="d616d-174">ID элемента диска OneDrive/SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d616d-174">OneDrive/SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="d616d-175">Тип файла, например pdf или docx.</span><span class="sxs-lookup"><span data-stu-id="d616d-175">File type, such as pdf or docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="d616d-176">Базовый пример в C #</span><span class="sxs-lookup"><span data-stu-id="d616d-176">Basic example in C#</span></span>

<span data-ttu-id="d616d-177">В следующем примере показано, как обрабатывать отправку файлов и отправлять запросы на согласие на файл в диалоговом окантовке бота.</span><span class="sxs-lookup"><span data-stu-id="d616d-177">The following sample shows how you can handle file uploads and send file consent requests in your bot's dialog.</span></span>

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
