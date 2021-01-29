---
title: Отправка и получение файлов с помощью бота
description: Описывает, как отправлять и получать файлы с помощью бота
keywords: отправка файлов ботов teams
ms.date: 05/20/2019
ms.topic: how-to
ms.openlocfilehash: 1699b9339bd6a49194240130d16795e8febcb76e
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037058"
---
# <a name="send-and-receive-files-through-the-bot"></a><span data-ttu-id="1b3bd-104">Отправка и получение файлов с помощью бота</span><span class="sxs-lookup"><span data-stu-id="1b3bd-104">Send and receive files through the bot</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b3bd-105">Статьи в этом документе основаны на пакете SDK Bot Framework v4.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-105">The articles in this document are based on the v4 Bot Framework SDK.</span></span>

<span data-ttu-id="1b3bd-106">Существует два способа отправки и получения файлов от бота:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-106">There are two ways to send files to and receive files from a bot:</span></span>

* <span data-ttu-id="1b3bd-107">**Использование API Microsoft Graph:** Этот метод работает для ботов во всех области Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-107">**Using the Microsoft Graph APIs:** This method works for bots in all Microsoft Teams scopes:</span></span>
  * `personal`
  * `channel`
  * `groupchat`

* <span data-ttu-id="1b3bd-108">**Использование API ботов Teams:** Они поддерживают только файлы в `personal` контексте.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-108">**Using the Teams bot APIs:** These only support files in `personal` context.</span></span>

## <a name="using-the-graph-apis"></a><span data-ttu-id="1b3bd-109">Использование API Graph</span><span class="sxs-lookup"><span data-stu-id="1b3bd-109">Using the Graph APIs</span></span>

<span data-ttu-id="1b3bd-110">Публикация сообщений с вложениями карт, которые ссылаются на существующие файлы SharePoint, с помощью API Graph для [OneDrive и SharePoint.](/onedrive/developer/rest-api/)</span><span class="sxs-lookup"><span data-stu-id="1b3bd-110">Post messages with card attachments that refer to existing SharePoint files, using the Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="1b3bd-111">Чтобы использовать API Graph, получите доступ к любой из следующих типов с помощью стандартного потока авторизации OAuth 2.0:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-111">To use the Graph APIs, obtain access to either of the following through the standard OAuth 2.0 authorization flow:</span></span>
* <span data-ttu-id="1b3bd-112">Папка oneDrive пользователя и `personal` `groupchat` файлы.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-112">A user's OneDrive folder for `personal` and `groupchat` files.</span></span>
* <span data-ttu-id="1b3bd-113">Файлы в канале команды для `channel` файлов.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-113">The files in a team's channel for `channel` files.</span></span>

<span data-ttu-id="1b3bd-114">API Graph работают во всех области Teams.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-114">Graph APIs work in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="1b3bd-115">Использование API ботов Teams</span><span class="sxs-lookup"><span data-stu-id="1b3bd-115">Using the Teams bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="1b3bd-116">API ботов Teams работают только в `personal` контексте.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-116">Teams bot APIs work only in the `personal` context.</span></span> <span data-ttu-id="1b3bd-117">Они не работают в `channel` контексте или в `groupchat` контексте.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-117">They do not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="1b3bd-118">С помощью API Teams бот может напрямую отправлять и получать файлы с пользователями в контексте, также известном как `personal` личные чаты.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-118">Using Teams APIs, the bot can directly send and receive files with users in the `personal` context, also known as personal chats.</span></span> <span data-ttu-id="1b3bd-119">Реализуют такие функции, как отчеты о расходах, распознавание изображений, архив файлов и электронные подписи, включающие редактирование содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-119">Implement features, such as expense reporting, image recognition, file archival, and e-signatures involving the editing of file content.</span></span> <span data-ttu-id="1b3bd-120">Файлы, к совместному доступу в Teams, как правило, отображаются в качестве карточек и позволяют просматривать их в приложении.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-120">Files shared in Teams typically appear as cards and allow rich in-app viewing.</span></span>

<span data-ttu-id="1b3bd-121">В следующих разделах описывается, как отправлять содержимое файла как непосредственное взаимодействие с пользователем, например отправка сообщения.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-121">The following sections describe how to send file content as a direct user interaction, like sending a message.</span></span> <span data-ttu-id="1b3bd-122">Этот API предоставляется в составе платформы ботов Teams.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-122">This API is provided as part of the Teams bot platform.</span></span>

### <a name="configuring-the-bot-to-support-files"></a><span data-ttu-id="1b3bd-123">Настройка бота для поддержки файлов</span><span class="sxs-lookup"><span data-stu-id="1b3bd-123">Configuring the bot to support files</span></span>

<span data-ttu-id="1b3bd-124">Чтобы отправлять и получать файлы в боте, за установите для свойства `supportsFiles` в манифесте свойство `true` ..</span><span class="sxs-lookup"><span data-stu-id="1b3bd-124">To send and receive files in the bot, set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="1b3bd-125">Это свойство описано в разделе [ботов](~/resources/schema/manifest-schema.md#bots) в справочнике по манифесту.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-125">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="1b3bd-126">Определение выглядит `"supportsFiles": true` так:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-126">The definition looks like this, `"supportsFiles": true`.</span></span> <span data-ttu-id="1b3bd-127">Если бот не включает, `supportsFiles` функции, перечисленные в этом разделе, не работают.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-127">If the bot does not enable `supportsFiles`, the features listed in this section do not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="1b3bd-128">Получение файлов в личном чате</span><span class="sxs-lookup"><span data-stu-id="1b3bd-128">Receiving files in personal chat</span></span>

<span data-ttu-id="1b3bd-129">Когда пользователь отправляет файл боту, он сначала отправляется в хранилище OneDrive для бизнеса пользователя.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-129">When a user sends a file to the bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="1b3bd-130">После этого бот получает сообщение об отправке пользователю уведомления.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-130">The bot then receives a message activity notifying the user about the user upload.</span></span> <span data-ttu-id="1b3bd-131">Действие содержит метаданные файла, такие как его имя и URL-адрес контента.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-131">The activity contains file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="1b3bd-132">Пользователь может напрямую считывать данные с этого URL-адреса, чтобы получить двоичное содержимое.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-132">The user can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="1b3bd-133">Пример действий с сообщением с вложенным файлом</span><span class="sxs-lookup"><span data-stu-id="1b3bd-133">Message activity with file attachment example</span></span>

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

<span data-ttu-id="1b3bd-134">В следующей таблице описываются свойства содержимого вложения:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-134">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="1b3bd-135">Свойство</span><span class="sxs-lookup"><span data-stu-id="1b3bd-135">Property</span></span> | <span data-ttu-id="1b3bd-136">Назначение</span><span class="sxs-lookup"><span data-stu-id="1b3bd-136">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="1b3bd-137">URL-адрес OneDrive для получения содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-137">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="1b3bd-138">Пользователь может выдавать адрес `HTTP GET` непосредственно с этого URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-138">The user can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="1b3bd-139">Уникальный ИД файла.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-139">Unique file ID.</span></span> <span data-ttu-id="1b3bd-140">Это ИД элемента диска OneDrive, если пользователь отправляет файл боту.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-140">This is the OneDrive drive item ID, in case the user sends a file to the bot.</span></span> |
| `fileType` | <span data-ttu-id="1b3bd-141">Тип файла, например PDF или DOCX.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-141">Type of file, such as .pdf or .docx.</span></span> |

<span data-ttu-id="1b3bd-142">Как лучше всего, подтвердите отправку файла, отправив сообщение пользователю.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-142">As a best practice, acknowledge the file upload by sending a message back to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="1b3bd-143">Отправка файлов в личный чат</span><span class="sxs-lookup"><span data-stu-id="1b3bd-143">Uploading files to personal chat</span></span>

<span data-ttu-id="1b3bd-144">Для отправки файла пользователю необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-144">The following steps are required to upload a file to a user:</span></span>

1. <span data-ttu-id="1b3bd-145">Отправьте сообщение пользователю, запрашивая разрешение на написание файла.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-145">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="1b3bd-146">Это сообщение должно содержать `FileConsentCard` вложение с именем файла, который необходимо отправить.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-146">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="1b3bd-147">Если пользователь принимает загрузку файла, бот получает действие вызова с URL-адресом расположения.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-147">If the user accepts the file download, the bot receives an invoke activity with a location URL.</span></span>
3. <span data-ttu-id="1b3bd-148">Для передачи файла бот выполняет прямой переход `HTTP POST` в предоставленный URL-адрес расположения.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-148">To transfer the file, the bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="1b3bd-149">При желании удалите исходную карточку согласия, если вы не хотите, чтобы пользователь мог принимать дополнительные отправки того же файла.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-149">Optionally, remove the original consent card if you do not want the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="1b3bd-150">Сообщение, запрашивающие разрешение на отправку</span><span class="sxs-lookup"><span data-stu-id="1b3bd-150">Message requesting permission to upload</span></span>

<span data-ttu-id="1b3bd-151">Следующее сообщение на рабочем столе содержит простой объект вложения, запрашивающий разрешение пользователя на отправку файла:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-151">The following desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![Карточка согласия с запросом разрешения пользователя на отправку файла](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="1b3bd-153">Следующее мобильное сообщение содержит объект вложения, запрашивающий разрешение пользователя на отправку файла:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-153">The following mobile message contains an attachment object requesting user permission to upload the file:</span></span>

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

<span data-ttu-id="1b3bd-155">В следующей таблице описываются свойства содержимого вложения:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-155">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="1b3bd-156">Свойство</span><span class="sxs-lookup"><span data-stu-id="1b3bd-156">Property</span></span> | <span data-ttu-id="1b3bd-157">Назначение</span><span class="sxs-lookup"><span data-stu-id="1b3bd-157">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="1b3bd-158">Описывает назначение файла или суммирует его содержимое.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-158">Describes the purpose of the file or summarizes its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="1b3bd-159">Предоставляет пользователю оценку размера файла и объема пространства, необходимого в OneDrive.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-159">Provides the user an estimate of the file size and the amount of space it takes in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="1b3bd-160">Дополнительный контекст, который автоматически передается боту, когда пользователь принимает файл.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-160">Additional context that is silently transmitted to the bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="1b3bd-161">Дополнительный контекст, который автоматически передается боту, когда пользователь отклочивает файл.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-161">Additional context that is silently transmitted to the bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="1b3bd-162">Вызов действия, когда пользователь принимает файл</span><span class="sxs-lookup"><span data-stu-id="1b3bd-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="1b3bd-163">Действие вызова отправляется боту, если и когда пользователь принимает файл.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-163">An invoke activity is sent to the bot if and when the user accepts the file.</span></span> <span data-ttu-id="1b3bd-164">Он содержит URL-адрес-замессера OneDrive для бизнеса, в который бот может передать содержимое `PUT` файла.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-164">It contains the OneDrive for Business placeholder URL that the bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="1b3bd-165">Сведения о загрузке на URL-адрес OneDrive см. в подзагонах отправки в [сеансе отправки.](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)</span><span class="sxs-lookup"><span data-stu-id="1b3bd-165">For information on uploading to the OneDrive URL, see [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="1b3bd-166">В следующем примере показана краткий версия действия вызова, которое получает бот:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-166">The following example shows a concise version of the invoke activity that the bot receives:</span></span>

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

<span data-ttu-id="1b3bd-167">Аналогично, если пользователь отклонит файл, бот получит следующее событие с таким же общим именем действия:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-167">Similarly, if the user declines the file, the bot receives the following event with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="1b3bd-168">Уведомление пользователя о загруженных файлах</span><span class="sxs-lookup"><span data-stu-id="1b3bd-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="1b3bd-169">После отправки файла в Хранилище OneDrive пользователя отправьте пользователю подтверждение.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-169">After uploading a file to the user's OneDrive, send a confirmation message to the user.</span></span> <span data-ttu-id="1b3bd-170">Сообщение должно содержать следующее вложение, которое пользователь может выбрать для предварительного просмотра или открытия в OneDrive, или для `FileCard` локальной загрузки:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-170">The message must contain the following `FileCard` attachment that the user can select, either to preview or open it in OneDrive, or download locally:</span></span>

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

<span data-ttu-id="1b3bd-171">В следующей таблице описываются свойства содержимого вложения:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-171">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="1b3bd-172">Свойство</span><span class="sxs-lookup"><span data-stu-id="1b3bd-172">Property</span></span> | <span data-ttu-id="1b3bd-173">Назначение</span><span class="sxs-lookup"><span data-stu-id="1b3bd-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="1b3bd-174">ИД элемента диска OneDrive или SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-174">OneDrive or SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="1b3bd-175">Тип файла, например PDF или DOCX.</span><span class="sxs-lookup"><span data-stu-id="1b3bd-175">Type of file, such as .pdf or .docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="1b3bd-176">Базовый пример в C #</span><span class="sxs-lookup"><span data-stu-id="1b3bd-176">Basic example in C#</span></span>

<span data-ttu-id="1b3bd-177">В следующем примере показано, как обрабатывать отправку файлов и отправлять запросы на согласие файлов в диалоговом окке бота:</span><span class="sxs-lookup"><span data-stu-id="1b3bd-177">The following sample shows how to handle file uploads and send file consent requests in the bot's dialog:</span></span>

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    string filename = "teams-logo.png";
    string filePath = Path.Combine("Files", filename);
    long fileSize = new FileInfo(filePath).Length;
    await SendFileCardAsync(turnContext, filename, fileSize, cancellationToken);
}

private async Task SendFileCardAsync(ITurnContext turnContext, string filename, long filesize, CancellationToken cancellationToken)
{
    var consentContext = new Dictionary<string, string>
    {
        { "filename", filename 
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
    replyActivity.Attachments = new List<Attachment>() { asAttachment 
    };
    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}

protected override async Task OnTeamsFileConsentAcceptAsync(ITurnContext<IInvokeActivity> turnContext, FileConsentCardResponse fileConsentCardResponse, CancellationToken cancellationToken)
{
    try
    {
        JToken context = JObject.FromObject(fileConsentCardResponse.Context);

        string filePath = Path.Combine("Files", context["filename"].ToString());
        long fileSize = new FileInfo(filePath).Length;
        var client = _clientFactory.CreateClient();
        using (var fileStream = File.OpenRead(filePath))
        {
            var fileContent = new StreamContent(fileStream);
            fileContent.Headers.ContentLength = fileSize;
            fileContent.Headers.ContentRange = new ContentRangeHeaderValue(0, fileSize - 1, fileSize);
            await client.PutAsync(fileConsentCardResponse.UploadInfo.UploadUrl, fileContent, cancellationToken);
        }

        await FileUploadCompletedAsync(turnContext, fileConsentCardResponse, cancellationToken);
    }
    catch (Exception e)
    {
        await FileUploadFailedAsync(turnContext, e.ToString(), cancellationToken);
    }
}

protected override async Task OnTeamsFileConsentDeclineAsync(ITurnContext<IInvokeActivity> turnContext, FileConsentCardResponse fileConsentCardResponse, CancellationToken cancellationToken)
{
    JToken context = JObject.FromObject(fileConsentCardResponse.Context);

    var reply = MessageFactory.Text($"Declined. We won't upload file <b>{context["filename"]}</b>.");
    reply.TextFormat = "xml";
    await turnContext.SendActivityAsync(reply, cancellationToken);
}

private async Task FileUploadCompletedAsync(ITurnContext turnContext, FileConsentCardResponse fileConsentCardResponse, CancellationToken cancellationToken)
{
    var downloadCard = new FileInfoCard
    {
        UniqueId = fileConsentCardResponse.UploadInfo.UniqueId,
        FileType = fileConsentCardResponse.UploadInfo.FileType,
    };

    var asAttachment = new Attachment
    {
        Content = downloadCard,
        ContentType = FileInfoCard.ContentType,
        Name = fileConsentCardResponse.UploadInfo.Name,
        ContentUrl = fileConsentCardResponse.UploadInfo.ContentUrl,
    };

    var reply = MessageFactory.Text($"<b>File uploaded.</b> Your file <b>{fileConsentCardResponse.UploadInfo.Name}</b> is ready to download");
    reply.TextFormat = "xml";
    reply.Attachments = new List<Attachment> { asAttachment 
    };

    await turnContext.SendActivityAsync(reply, cancellationToken);
}

private async Task FileUploadFailedAsync(ITurnContext turnContext, string error, CancellationToken cancellationToken)
{
    var reply = MessageFactory.Text($"<b>File upload failed.</b> Error: <pre>{error}</pre>");
    reply.TextFormat = "xml";
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
```
