---
title: Отправка и получение файлов с помощью Bot
description: Сведения о том, как отправлять и получать файлы с ленты.
keywords: Teams Боты Files Send Receive
ms.date: 05/20/2019
ms.openlocfilehash: ee26b4031c6022ab30ec5b2b58b42105c2dc6b0f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675650"
---
# <a name="send-and-receive-files-through-your-bot"></a><span data-ttu-id="6b45c-104">Отправка и получение файлов через Bot</span><span class="sxs-lookup"><span data-stu-id="6b45c-104">Send and receive files through your bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="6b45c-105">Существует два способа отправки файлов с помощью Bot:</span><span class="sxs-lookup"><span data-stu-id="6b45c-105">There are two ways to send files to and from a bot:</span></span>

* <span data-ttu-id="6b45c-106">С помощью API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="6b45c-106">Using the Microsoft Graph APIs.</span></span> <span data-ttu-id="6b45c-107">Этот метод работает для Боты во всех областях в teams:</span><span class="sxs-lookup"><span data-stu-id="6b45c-107">This method works for bots in all scopes in Teams:</span></span>
  * `personal`
  * `channel`
  * `groupchat`
* <span data-ttu-id="6b45c-108">Использование API Teams.</span><span class="sxs-lookup"><span data-stu-id="6b45c-108">Using the Teams APIs.</span></span> <span data-ttu-id="6b45c-109">Эти файлы поддерживаются только в одном контексте:</span><span class="sxs-lookup"><span data-stu-id="6b45c-109">These only support files in one context:</span></span>
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a><span data-ttu-id="6b45c-110">Использование API Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="6b45c-110">Using the Microsoft Graph APIs</span></span>

<span data-ttu-id="6b45c-111">Вы можете размещать сообщения с вложениями карточек, ссылающиеся на существующие файлы SharePoint, с помощью API Microsoft Graph для [OneDrive и SharePoint](/onedrive/developer/rest-api/).</span><span class="sxs-lookup"><span data-stu-id="6b45c-111">You can post messages with card attachments referencing existing SharePoint files using the Microsoft Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="6b45c-112">Для использования API Graph требуется получение доступа к папке OneDrive пользователя (для `personal` файлов и `groupchat` файлов) или файлам в каналах группы (для `channel` файлов) через стандартный процесс авторизации OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="6b45c-112">Using the Graph APIs requires obtaining access to a user's OneDrive folder (for `personal` and `groupchat` files) or the files in a team's channels (for `channel` files) through the standard OAuth 2.0 authorization flow.</span></span> <span data-ttu-id="6b45c-113">Этот метод работает во всех областях Teams.</span><span class="sxs-lookup"><span data-stu-id="6b45c-113">This method works in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="6b45c-114">Использование API-интерфейсов Bot для Teams</span><span class="sxs-lookup"><span data-stu-id="6b45c-114">Using the Teams Bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="6b45c-115">Этот метод работает только в `personal` контексте.</span><span class="sxs-lookup"><span data-stu-id="6b45c-115">This method works only in the `personal` context.</span></span> <span data-ttu-id="6b45c-116">Он не работает в контексте `channel` или. `groupchat`</span><span class="sxs-lookup"><span data-stu-id="6b45c-116">It does not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="6b45c-117">С помощью API Teams вы можете напрямую отправлять и получать файлы `personal` с пользователями в контексте, также называемом личными беседами.</span><span class="sxs-lookup"><span data-stu-id="6b45c-117">Your bot can directly send and receive files with users in the `personal` context, also known as personal chats, using Teams APIs.</span></span> <span data-ttu-id="6b45c-118">Это позволяет реализовать отчеты о расходах, распознавание изображений, архивацию файлов, электронные подписи и другие сценарии, затрагивающие прямую обработку содержимого файлов.</span><span class="sxs-lookup"><span data-stu-id="6b45c-118">This lets you implement expense reporting, image recognition, file archival, e-signatures, and other scenarios involving direct manipulation of file content.</span></span> <span data-ttu-id="6b45c-119">Файлы, к которым предоставлен общий доступ в Teams, обычно отображаются в виде карточек и позволяют просматривать расширенные возможности просмотра в приложении.</span><span class="sxs-lookup"><span data-stu-id="6b45c-119">Files shared in Teams typically appear as cards, and allow rich in-app viewing.</span></span>

<span data-ttu-id="6b45c-120">В следующих разделах описано, как это сделать для отправки содержимого файлов в результате прямого взаимодействия с пользователем, например для отправки сообщения.</span><span class="sxs-lookup"><span data-stu-id="6b45c-120">The following sections describe how to do this to send file content as a result of direct user interaction, like sending a message.</span></span> <span data-ttu-id="6b45c-121">Этот API предоставляется как часть платформы ленты Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="6b45c-121">This API is provided as part of the Microsoft Teams Bot Platform.</span></span>

### <a name="configure-your-bot-to-support-files"></a><span data-ttu-id="6b45c-122">Настройка ленты для поддержки файлов</span><span class="sxs-lookup"><span data-stu-id="6b45c-122">Configure your bot to support files</span></span>

<span data-ttu-id="6b45c-123">Чтобы отправлять и получать файлы в Bot, необходимо задать для `supportsFiles` `true`свойства в манифесте значение.</span><span class="sxs-lookup"><span data-stu-id="6b45c-123">In order to send and receive files in your bot, you have to set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="6b45c-124">Это свойство описывается в разделе [Боты](~/resources/schema/manifest-schema.md#bots) ссылки на манифест.</span><span class="sxs-lookup"><span data-stu-id="6b45c-124">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="6b45c-125">Определение будет выглядеть следующим образом: `"supportsFiles": true`.</span><span class="sxs-lookup"><span data-stu-id="6b45c-125">The definition will look like this: `"supportsFiles": true`.</span></span> <span data-ttu-id="6b45c-126">Если вы не включили `supportsFiles`ваш робот, указанные ниже функции не будут работать.</span><span class="sxs-lookup"><span data-stu-id="6b45c-126">If your bot does not enable `supportsFiles`, the following features will not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="6b45c-127">Получение файлов в личном чате</span><span class="sxs-lookup"><span data-stu-id="6b45c-127">Receiving files in personal chat</span></span>

<span data-ttu-id="6b45c-128">Когда пользователь отправляет файл в Bot, сначала он отправляется в хранилище OneDrive для бизнеса пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b45c-128">When a user sends a file to your bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="6b45c-129">Затем ваш робот будет получать сообщение о том, что пользователь отправляет сообщение.</span><span class="sxs-lookup"><span data-stu-id="6b45c-129">Your bot will then receive a message activity notifying you of the user upload.</span></span> <span data-ttu-id="6b45c-130">Действие будет содержать метаданные файлов, такие как имя и URL-адрес контента.</span><span class="sxs-lookup"><span data-stu-id="6b45c-130">The activity will contain file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="6b45c-131">Вы можете напрямую прочитать этот URL-адрес, чтобы получить его двоичное содержимое.</span><span class="sxs-lookup"><span data-stu-id="6b45c-131">You can directly read from this URL to fetch its binary content.</span></span>

### <a name="send-and-receive-files-through-bot-on-teams-mobile-app"></a><span data-ttu-id="6b45c-132">Отправка и получение файлов через Bot в мобильном приложении Teams</span><span class="sxs-lookup"><span data-stu-id="6b45c-132">Send and receive files through bot on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="6b45c-133">Отправка и получение файлов в боты на мобильных устройствах не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="6b45c-133">Sending and receiving files to bots on mobile devices is not supported.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="6b45c-134">Пример активности сообщений с вложенным файлом</span><span class="sxs-lookup"><span data-stu-id="6b45c-134">Message activity with file attachment example</span></span>

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

<span data-ttu-id="6b45c-135">В следующей таблице описываются свойства содержимого вложения:</span><span class="sxs-lookup"><span data-stu-id="6b45c-135">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="6b45c-136">Свойство</span><span class="sxs-lookup"><span data-stu-id="6b45c-136">Property</span></span> | <span data-ttu-id="6b45c-137">Назначение</span><span class="sxs-lookup"><span data-stu-id="6b45c-137">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="6b45c-138">URL-адрес OneDrive для извлечения содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="6b45c-138">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="6b45c-139">Вы можете выпустить URL-адрес `HTTP GET` непосредственно из этого URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="6b45c-139">You can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="6b45c-140">Уникальный идентификатор файла.</span><span class="sxs-lookup"><span data-stu-id="6b45c-140">Unique file ID.</span></span> <span data-ttu-id="6b45c-141">Это будет идентификатор элемента диска OneDrive, если пользователь отправит файл в устройство Bot.</span><span class="sxs-lookup"><span data-stu-id="6b45c-141">This will be the OneDrive drive item ID, in the case of the user sending a file to your bot.</span></span> |
| `fileType` | <span data-ttu-id="6b45c-142">Тип расширения файла, например PDF или DOCX.</span><span class="sxs-lookup"><span data-stu-id="6b45c-142">File extension type, such as pdf or docx.</span></span> |

<span data-ttu-id="6b45c-143">Рекомендуется отправить файл, отправив пользователю сообщение...</span><span class="sxs-lookup"><span data-stu-id="6b45c-143">As a best practice, you should acknowledge the file upload by sending back a message to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="6b45c-144">Отправка файлов в личный чат</span><span class="sxs-lookup"><span data-stu-id="6b45c-144">Uploading files to personal chat</span></span>

<span data-ttu-id="6b45c-145">Отправка файла пользователю состоит из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="6b45c-145">Uploading a file to a user involves the following steps:</span></span>

1. <span data-ttu-id="6b45c-146">Отправить пользователю сообщение, запрашивающее разрешение на запись файла.</span><span class="sxs-lookup"><span data-stu-id="6b45c-146">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="6b45c-147">Это сообщение должно содержать `FileConsentCard` вложение с именем файла, который необходимо отправить.</span><span class="sxs-lookup"><span data-stu-id="6b45c-147">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="6b45c-148">Если пользователь принимает загрузку файла, он будет получать действие *Invoke* с URL-адресом расположения.</span><span class="sxs-lookup"><span data-stu-id="6b45c-148">If the user accepts the file download, your bot will receive an *Invoke* activity with a location URL.</span></span>
3. <span data-ttu-id="6b45c-149">Чтобы передать файл, ваш Bot `HTTP POST` напрямую выполняет в указанном URL-адресе расположения.</span><span class="sxs-lookup"><span data-stu-id="6b45c-149">To transfer the file, your bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="6b45c-150">Кроме того, вы можете удалить исходную открытку, если вы не хотите разрешить пользователю принимать дальнейшую отправку того же файла.</span><span class="sxs-lookup"><span data-stu-id="6b45c-150">Optionally, you can remove the original consent card if you do not want to allow the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="6b45c-151">Сообщение, запрашивающее разрешение на отправку</span><span class="sxs-lookup"><span data-stu-id="6b45c-151">Message requesting permission to upload</span></span>

<span data-ttu-id="6b45c-152">Это сообщение содержит простой объект вложения, запрашивающий разрешение пользователя на отправку файла.</span><span class="sxs-lookup"><span data-stu-id="6b45c-152">This message contains a simple attachment object requesting user permission to upload the file.</span></span>

![Снимок экрана с картой согласия, запрашивающей разрешение пользователя на отправку файла](~/assets/images/bots/bot-file-consent-card.png)

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

<span data-ttu-id="6b45c-154">В следующей таблице описываются свойства содержимого вложения:</span><span class="sxs-lookup"><span data-stu-id="6b45c-154">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="6b45c-155">Свойство</span><span class="sxs-lookup"><span data-stu-id="6b45c-155">Property</span></span> | <span data-ttu-id="6b45c-156">Назначение</span><span class="sxs-lookup"><span data-stu-id="6b45c-156">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="6b45c-157">Описание файла.</span><span class="sxs-lookup"><span data-stu-id="6b45c-157">Description of the file.</span></span> <span data-ttu-id="6b45c-158">Может отображаться для пользователя, чтобы описать его назначение или сводную информацию.</span><span class="sxs-lookup"><span data-stu-id="6b45c-158">May be shown to the user to describe its purpose or to summarize its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="6b45c-159">Предоставляет пользователю оценку размера файла и объема дискового пространства, которое займет OneDrive.</span><span class="sxs-lookup"><span data-stu-id="6b45c-159">Provides the user an estimate of the file size and the amount of space it will take in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="6b45c-160">Дополнительный контекст, который будет автоматически передаваться в систему робота, когда пользователь принимает файл.</span><span class="sxs-lookup"><span data-stu-id="6b45c-160">Additional context that will be silently transmitted to your bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="6b45c-161">Дополнительный контекст, который будет автоматически передаваться в файл робота, когда пользователь отклоняет файл.</span><span class="sxs-lookup"><span data-stu-id="6b45c-161">Additional context that will be silently transmitted to your bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="6b45c-162">Вызвать действие, когда пользователь принимает файл</span><span class="sxs-lookup"><span data-stu-id="6b45c-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="6b45c-163">Действие Invoke отправляется в Bot в том случае, когда пользователь принимает файл.</span><span class="sxs-lookup"><span data-stu-id="6b45c-163">An invoke activity is sent to your bot if and when the user accepts the file.</span></span> <span data-ttu-id="6b45c-164">Он содержит URL-адрес заполнителя OneDrive для бизнеса, который может быть связан с `PUT` назначением, чтобы перенести содержимое файла.</span><span class="sxs-lookup"><span data-stu-id="6b45c-164">It contains the OneDrive for Business placeholder URL that your bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="6b45c-165">для получения сведений об отправке на URL-адрес OneDrive прочитайте эту статью: [Отправка байтов в сеанс отправки](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span><span class="sxs-lookup"><span data-stu-id="6b45c-165">for information on uploading to the OneDrive URL read this article: [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="6b45c-166">В приведенном ниже примере показана версия абриджед действия Invoke, которое будет получать ваш робот.</span><span class="sxs-lookup"><span data-stu-id="6b45c-166">The following example shows an abridged version of the invoke activity that your bot will receive:</span></span>

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

<span data-ttu-id="6b45c-167">Аналогичным образом, если пользователь отклоняет файл, ваш робот получит следующее событие с таким же общим именем действия:</span><span class="sxs-lookup"><span data-stu-id="6b45c-167">Similarly, if the user declines the file, your bot will receive the following event, with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="6b45c-168">Уведомление пользователя о отправленном файле</span><span class="sxs-lookup"><span data-stu-id="6b45c-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="6b45c-169">После отправки файла в OneDrive пользователя независимо от того, используется ли механизм, описанный выше, или API, делегированные пользовательские API OneDrive, необходимо отправить пользователю сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="6b45c-169">After uploading a file to the user's OneDrive, whether you use the mechanism described above or OneDrive user delegated APIs, you should send a confirmation message to the user.</span></span> <span data-ttu-id="6b45c-170">Это сообщение должно содержать `FileCard` вложение, которое пользователь может щелкнуть, чтобы просмотреть его, открыть в OneDrive или скачать локально.</span><span class="sxs-lookup"><span data-stu-id="6b45c-170">This message should contain  a `FileCard` attachment that the user can click on, either to preview it, open it in OneDrive, or download locally.</span></span>

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

<span data-ttu-id="6b45c-171">В следующей таблице описываются свойства содержимого вложения:</span><span class="sxs-lookup"><span data-stu-id="6b45c-171">The following table describes the content properties of the attachment:</span></span> 

| <span data-ttu-id="6b45c-172">Свойство</span><span class="sxs-lookup"><span data-stu-id="6b45c-172">Property</span></span> | <span data-ttu-id="6b45c-173">Назначение</span><span class="sxs-lookup"><span data-stu-id="6b45c-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="6b45c-174">Идентификатор элемента диска OneDrive или SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6b45c-174">OneDrive/SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="6b45c-175">Тип файла, например PDF или DOCX.</span><span class="sxs-lookup"><span data-stu-id="6b45c-175">File type, such as pdf or docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="6b45c-176">Базовый пример в C #</span><span class="sxs-lookup"><span data-stu-id="6b45c-176">Basic example in C#</span></span>

<span data-ttu-id="6b45c-177">В следующем примере показано, как можно обрабатывать отправку файлов и отправлять запросы на согласие на предоставление файлов в диалоговом окне Bot.</span><span class="sxs-lookup"><span data-stu-id="6b45c-177">The following sample shows how you can handle file uploads and send file consent requests in your bot's dialog.</span></span>

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
