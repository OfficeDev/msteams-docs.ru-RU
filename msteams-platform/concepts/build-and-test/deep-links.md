---
title: Создание глубоких ссылок на контент
description: Описывает глубокие ссылки и их использование в приложениях
ms.topic: how-to
keywords: deeplink teams deep link
ms.openlocfilehash: afcb079873f97055c4af43323d12846294861f74
ms.sourcegitcommit: ee8c4800da3b3569d80c6f3661a2f20aa1f2c5e2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/19/2021
ms.locfileid: "51885061"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a>Создание глубоких ссылок на контент и функции в Microsoft Teams

В Teams можно создавать ссылки на сведения и функции. Примеры полезного создания глубоких ссылок:

* Перемещение пользователя к содержимому в одной из вкладок приложения. Например, в вашем приложении может быть бот, который отправляет сообщения, уведомляющие пользователя о важном действии. Когда пользователь нажмет на уведомление, глубокая ссылка переходит на вкладку, чтобы пользователь может просмотреть дополнительные сведения о действии.
* Ваше приложение автоматизирует или упрощает определенные пользовательские задачи, например создание чата или планирование собрания, предварительно заполнив глубокие ссылки с требуемыми параметрами. Это позволяет избежать необходимости вручную вводить сведения.

> [!NOTE]
>
> Deeplink запускает браузер сначала перед переходом на контент и сведения следующим образом:
>
> **Вкладка:**  
> ✔ непосредственно переходит на URL-адрес deeplink.
>
> **Bot:**  
> ✔ Deeplink в теле карты: сначала откроется в браузере.  
> ✔ Deeplink добавлена к действию OpenURL в адаптивной карте: непосредственно переходит на URL-адрес deeplink.  
> ✔ разметка гиперссылки в карточке: сначала откроется в браузере.  
>
> **Чат:**  
> ✔ разметка текстовых сообщений: непосредственно переходит на url-адрес deeplink.  
> ✔ ссылку, вклеитую в общий чат: непосредственно переходит на url-адрес deeplink.

## <a name="deep-linking-to-your-tab"></a>Глубокая ссылка на вкладку

Можно создавать глубокие ссылки на сущности в Teams. Как правило, это используется для создания ссылок, которые переходят к содержимому и сведениям в вкладке. Например, если вкладка содержит список задач, члены группы могут создавать и обмениваться ссылками на отдельные задачи. При выборе ссылки она переходит на вкладку, которая фокусируется на конкретном элементе. Для реализации этого в каждый элемент добавляется действие "ссылка на копирование", которое наилучшим образом подходит вашему пользовательскому интерфейсу. Когда пользователь принимает это действие, вы звоните, чтобы отобразить диалоговое окно, содержащее ссылку, которую пользователь может скопировать `shareDeepLink()` в буфер обмена. При этом вызове вы также передаете ID для элемента, [](~/tabs/how-to/access-teams-context.md) который возвращается в контексте, когда будет следовать ссылка и ваша вкладка будет перезагружена.

Кроме того, вы также можете создавать глубокие ссылки программным образом, используя формат, указанный позже в этом разделе. Эти сообщения можно использовать [](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) в [сообщениях бота](~/bots/what-are-bots.md) и соединители, информируя пользователей об изменениях на вкладке или элементов внутри нее.

> [!NOTE]
> Эта глубокая ссылка отличается от ссылок, предоставляемых ссылкой **Копию** на элемент меню вкладки, которая только создает глубокую ссылку, которая указывает на эту вкладку.

>[!NOTE]
> В настоящее время shareDeepLink не работает на мобильных платформах.

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a>Отображение глубокой ссылки на элемент в вкладке

Чтобы показать диалоговое окно, содержаное глубокую ссылку на элемент в вкладке, позвоните `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`

Предоставление этих полей:

* `subEntityId`&emsp;Уникальный идентификатор элемента в вкладке, с которым вы связываете глубокую связь
* `subEntityLabel`&emsp;Метка для элемента, используемая для отображения глубокой ссылки
* `subEntityWebUrl`&emsp;Необязательное поле с откатным URL-адресом для использования, если клиент не поддерживает отрисовку вкладки

### <a name="generating-a-deep-link-to-your-tab"></a>Создание глубокой ссылки на вкладку

> [!NOTE]
> Личные вкладки имеют область, в то время как вкладки каналов и групп `personal` используют `team` или `group` области. Два типа вкладок имеют несколько другой синтаксис, так как только настраиваемая вкладка имеет свойство, связанное `channel` с объектом контекста. Дополнительные [сведения](~/resources/schema/manifest-schema.md) о области вкладок см. в справке манифеста.

> [!NOTE]
> Глубокие ссылки работают должным образом только в том случае, если вкладка была настроена с помощью библиотеки v0.4 или более поздней библиотеки и поэтому имеет ID сущности. Глубокие ссылки на вкладки без ИД сущности по-прежнему переходят на вкладку, но не могут предоставить на вкладку ИД суб-сущности.

Используйте следующий формат для глубокой ссылки, которую можно использовать в карточке расширения бота, соединитетеля или обмена сообщениями:

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Если бот отправляет сообщение, содержащее глубокую ссылку, откроется новая вкладка браузера, когда пользователь выбирает `TextBlock` ссылку. Это происходит в Chrome и в настольном приложении Microsoft Teams, которое работает на Linux.
> Если бот отправляет один и тот же URL-адрес глубокой ссылки в вкладку Teams, вкладка Teams открывается на текущей вкладке браузера, когда пользователь выбирает `Action.OpenUrl` ссылку. Новая вкладка браузера не открывается.

Параметры запроса:

* `appId`&emsp;ID из манифеста; например, "fe4a8eba-2a31-4737-8e33-e5fae6fee194"
* `entityId`&emsp;ID для элемента на вкладке, который вы предоставили при [настройке вкладки;](~/tabs/how-to/create-tab-pages/configuration-page.md) например, "tasklist123"
* `entityWebUrl`или необязательный url-адрес, который можно использовать, если клиент не поддерживает отрисовку `subEntityWebUrl` &emsp; вкладки; например, https://tasklist.example.com/123 "" или https://tasklist.example.com/list123/task456 ""
* `entityLabel`или метка для элемента на вкладке для отображения глубокой `subEntityLabel` &emsp; ссылки; например, "Список задач 123" или "Задача 456"
* `context`&emsp;Объект JSON, содержащий следующие поля:
  * `subEntityId`&emsp;ID для элемента в _вкладке;_ например, "task456"
  * `channelId`&emsp;ID канала Microsoft Teams, доступный из контекста [вкладки;](~/tabs/how-to/access-teams-context.md) например, "19:cbe3683f25094106b826c9cada3afbe0@thread.skype". Это свойство доступно только в настраиваемых вкладок с областью "team". Он не доступен в статических вкладок, которые имеют область "личный".

Примеры:

* Ссылка на настраиваемую вкладку: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Ссылка на элемент задачи в настраиваемой вкладке: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Ссылка на статическую вкладку: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* Ссылка на элемент задачи в статической вкладке: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> Убедитесь, что все параметры запроса правильно закодированы. Вы должны следовать предварительным примерам, используя последний пример:
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a>Потребление глубокой ссылки со вкладки

При переходе на глубокую ссылку Microsoft Teams просто переходит на вкладку и предоставляет механизм через библиотеку JavaScript Microsoft Teams для получения кода суб-сущности, если он существует.

Вызов возвращает контекст, который включает поле, если вкладка передается [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) `subEntityId` по глубокой ссылке.

## <a name="deep-linking-from-your-tab"></a>Глубокая связь с вкладки

Вы можете глубоко ссылаться на контент в Teams со своей вкладки. Это полезно, если вкладке необходимо связаться с другим контентом в Teams, например с каналом, сообщением, другой вкладке или даже открыть диалоговое окно планирования. Чтобы вызвать глубокую ссылку с вкладки, необходимо вызвать:

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Этот вызов перемещает вас по правильному URL-адресу или запускает действие клиента, например открытие диалоговой даты или установки приложения. Пример приведен в следующей статье:

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Глубокая связь с чатом

Вы можете создать глубокие ссылки на частные чаты между пользователями, указав набор участников. Если чат не существует с указанными участниками, ссылка перемещает пользователя в пустой новый чат. Новые чаты создаются в состоянии черновика, пока пользователь не отправит первое сообщение. В противном случае можно указать имя чата, если он еще не существует, а также текст, который должен быть вставлен в поле сочинения пользователя. Эту функцию можно использовать в качестве ярлыка для пользователя, который будет вручную перемещаться в чат или создавать его, а затем вводить сообщение.

В качестве примера используйте случай, если вы возвращаете профиль пользователя Office 365 из бота в качестве карты, эта глубокая ссылка может позволить пользователю легко общаться с этим человеком.

### <a name="generate-a-deep-link-to-a-chat"></a>Создание глубокой ссылки на чат

Используйте этот формат для глубокой ссылки, которую можно использовать в карточке расширения бота, соединитетеля или обмена сообщениями:

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Пример: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Параметры запроса:

* `users`: Разделенный запятой список пользовательских ИД, представляющих участников чата. Пользователь, который выполняет действие, всегда включен в качестве участника. В настоящее время поле User ID поддерживает Azure AD UserPrincipalName, обычно только адрес электронной почты.
* `topicName`. Необязательное поле для отображения имени чата в случае чата с 3 или более пользователями. Если это поле не указано, имя отображения чата основано на именах участников.
* `message`. Необязательное поле для текста сообщения, которое необходимо вставить в поле записи текущего пользователя, пока чат находится в состоянии черновика.

Чтобы использовать эту глубокую ссылку с ботом, вы можете указать это в качестве целевого URL-адреса на кнопке карточки или нажмите действие через `openUrl` тип действия.

## <a name="generate-deep-links-to-file-in-channel"></a>Создание глубоких ссылок для файла в канале

Следующий формат глубокой ссылки можно использовать в карточке расширения бота, соединитетеля или обмена сообщениями:

`https://teams.microsoft.com/I/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

Параметры запроса:

* `tenantId`: Пример ID клиента, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb
* `fileType`: Поддерживаемый тип файла, например docx, pptx, xlsx и pdf
* `objectUrl`: URL-адрес объекта файла, https://microsoft.sharepoint.com/teams/(filepath)
* `baseUrl`: Базовый URL-адрес файла, https://microsoft.sharepoint.com/teams
* `serviceName`: Имя службы, ID приложения
* `threadId`. ThreadId — это командный ID команды, в которой хранится файл. Она необязательна и не может быть установлена для файлов, хранимых в папке OneDrive пользователя. threadId — 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype
* `groupId`: Групповой ID файла ae063b79-5315-4ddb-ba70-27328ba6c31e

Ниже приводится пример формата deeplink к файлам:

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80 ?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

### <a name="serialization-of-this-object"></a>Сериализация этого объекта:
```
{
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```
## <a name="deep-links-for-sharepoint-framework-tabs"></a>Глубокие ссылки для вкладок SharePoint Framework

Следующий формат глубокой ссылки можно использовать в карточке расширения бота, соединитетеля или обмена сообщениями: `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> Когда бот отправляет сообщение TextBlock с глубокой ссылкой, при выборе ссылки открывается новая вкладка браузера. Это происходит в настольном приложении Chrome и Microsoft Teams, которое работает на Linux.
> Если бот отправляет один и тот же URL-адрес глубокой ссылки в вкладку Teams, открываемую в текущем браузере, когда пользователь выбирает `Action.OpenUrl` ссылку. Новая вкладка браузера не открывается.

Параметры запроса:

* `appID`: Ваш манифест fe4a8eba-2a31-4737-8e33-e5fae6fee194.
* `entityID`: ID элемента, который вы предоставили [при настройке вкладки](~/tabs/how-to/create-tab-pages/configuration-page.md). Например, **tasklist123**.
* `entityWebUrl`. Необязательный url-адрес с откатным URL-адресом, который можно использовать, если клиент не поддерживает отрисовку вкладки или https://tasklist.example.com/123 https://tasklist.example.com/list123/task456 .
* `entityName`: Метка для элемента на вкладке, используемая при отображе глубокой ссылки, список задач 123 или задача 456.

Пример: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList

## <a name="linking-to-the-scheduling-dialog"></a>Ссылка на диалоговое окно планирования

> [!Note]
> Эта функция в настоящее время находится в предварительном просмотре разработчика.

Можно создать глубокие ссылки на встроенный диалоговое окно планирования Teams. Это особенно полезно, если приложение помогает пользователю выполнять задачи, связанные с календарем или планированием.

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a>Создание глубокой ссылки на диалоговое окно планирования

Используйте следующий формат для глубокой ссылки, которую можно использовать в карточке расширения бота, соединитетеля или обмена сообщениями: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Пример: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

Параметры запроса:

* `attendees`. Необязательный список пользовательских ИД, разделенных запятой, представляющих участников собрания. Пользователь, исполняющий действие, является организатором собрания. В настоящее время поле ID пользователя поддерживает только Azure AD UserPrincipalName, как правило, адрес электронной почты.
* `startTime`. Необязательное время начала события. Это должно быть в [длинном формате ISO 8601,](https://en.wikipedia.org/wiki/ISO_8601)например *2018-03-12T23:55:25+02:00*.
* `endTime`: Необязательное время окончания события, также в формате ISO 8601.
* `subject`. Необязательный поле для темы собрания.
* `content`. Необязательное поле для поля сведений о собраниях.

> [!NOTE]
> В настоящее время указание расположения не поддерживается. Необходимо указать смещение UTC, это означает часовые пояса при создании времени начала и окончания.

Чтобы использовать эту глубокую ссылку с ботом, вы можете указать это в качестве целевого URL-адреса на кнопке карточки или нажмите действие через `openUrl` тип действия.
