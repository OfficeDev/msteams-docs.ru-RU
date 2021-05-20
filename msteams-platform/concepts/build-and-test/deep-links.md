---
title: Создание прямых ссылок
description: Описывает глубокие ссылки и как их использовать в приложениях
ms.topic: how-to
localization_priority: Normal
keywords: команды глубокая связь deeplink
ms.openlocfilehash: 837d180b06f69b9be49d898c62b9ab8ee64d51d0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566056"
---
# <a name="create-deep-links"></a>Создание прямых ссылок 

Вы можете создавать ссылки на информацию и функции в Teams. Сценарии, в которых создаются глубокие ссылки, являются следующими:

* Навигация пользователя по содержимому в одной из вкладок приложения. Например, в приложении может быть бот, который отправляет сообщения, уведомляющие пользователя о важном действии. Когда пользователь нажимает на уведомление, глубокая ссылка переходит на вкладку, так что пользователь может просматривать более подробную информацию о деятельности.
* Приложение автоматизирует или упрощает определенные пользовательские задачи, такие как создание чата или планирование собрания, предварительно засасыв глубокие ссылки с требуемыми параметрами. Это позволяет избежать необходимости для пользователей вручную вводить информацию.

> [!NOTE]
>
> Deeplink запускает браузер, прежде чем переориентаться на контент. Поведение глубоких связей на Teams сущностей:
>
> **Вкладка**:  
> ✔ непосредственно переходит к глубокой ссылке URL.
>
> **Бот**:  
> ✔ Deeplink в корпусе карты: открывается в браузере в первую очередь.  
> ✔ Deeplink добавлен в действие OpenURL в адаптивной карте: непосредственно переходит к url-адресу deeplink.  
> ✔ Hyperlink разметки текст в карте: Открывается в браузере в первую очередь.  
>
> **Чат**:  
> ✔ сообщение hyperlink разметки: Непосредственно переходит к deeplink URL.  
> ✔ ссылка вставить в общий разговор чат: Непосредственно переходит к deeplink URL.

## <a name="deep-linking-to-your-tab"></a>Глубокая ссылка на вкладку

Вы можете создать глубокие ссылки на сущности в Teams. Это используется для создания ссылок, которые перемещаются по содержанию и информации в вашей вкладке. Например, если вкладка содержит список задач, члены группы могут создавать и обмениваться ссылками на отдельные задачи. При выборе ссылки он переходит к вкладке, которая фокусируется на конкретном элементе. Для реализации этого, вы добавляете **копию ссылку** действий для каждого элемента, каким бы образом лучше всего подходит ваш пользовательский интерфейс. Когда пользователь принимает это действие, вы звоните, `shareDeepLink()` чтобы отобразить диалоговое окно, содержащее ссылку, которую пользователь может скопировать на буфер обмена. При этом вызове вы также проходите идентификатор для вашего товара, который вы получаете обратно в [контексте,](~/tabs/how-to/access-teams-context.md) когда ссылка следует и ваша вкладка перезагружается.

Кроме того, вы также можете создавать глубокие ссылки программно, используя формат, указанный позже в этой теме. Вы можете использовать глубокие ссылки в [сообщениях](~/bots/what-are-bots.md) [бота и](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) разъема, которые информируют пользователей об изменениях в вкладке или в ее предметах.

> [!NOTE]
> Эта глубокая ссылка отличается от ссылок, предоставляемых **copy ссылку на пункт меню** вкладки, которая просто генерирует глубокую ссылку, которая указывает на эту вкладку.

>[!NOTE]
> В настоящее время shareDeepLink не работает на мобильных платформах.

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a>Показать глубокую ссылку на элемент в вкладке

Чтобы показать диалоговое окно, которое содержит глубокую ссылку на элемент в вкладке, позвоните `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` .

Предоставьте следующие поля:

* `subEntityId`: Уникальный идентификатор элемента в вкладке, к которому вы глубоко связаны.
* `subEntityLabel`: Метка для элемента для отображения глубокой ссылке.
* `subEntityWebUrl`: Дополнительное поле с обратным URL для использования, если клиент не поддерживает визуализацию вкладки.

### <a name="generate-a-deep-link-to-your-tab"></a>Создание глубокой ссылки на вкладку

> [!NOTE]
> Личные вкладки имеют `personal` область, в то время как канал и группы вкладок `team` использования или `group` сферы. Эти два типа вкладок имеют несколько иной синтаксис, так как только настраиваемая вкладка имеет `channel` свойство, связанное с объектом контекста. Дополнительную [информацию о](~/resources/schema/manifest-schema.md) сферах вкладок можно получить в явном справочнике.

> [!NOTE]
> Глубокие ссылки работают должным образом только в том случае, если вкладка была настроена с помощью v0.4 или более поздней библиотеки и из-за этого имеет идентификатор сущности. Глубокие ссылки на вкладки без идентификаторов сущности по-прежнему перемещаются по вкладке, но не могут предоставить идентификатор подуком на вкладку.

Используйте следующий формат для глубокой ссылки, которую можно использовать в боте, разъеме или карточке расширения обмена сообщениями:

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Если бот отправляет сообщение, содержащее `TextBlock` глубокую ссылку, то новая вкладка браузера открыта, когда пользователь выбирает ссылку. Это происходит в Chrome и в приложении Microsoft Teams, как работает на Linux.
> Если бот отправляет тот же глубокий URL ссылки в `Action.OpenUrl` , то вкладка Teams открыта в текущей вкладке браузера, когда пользователь выбирает ссылку. Новая вкладка браузера не открыта.

Параметры запроса:

| Имя параметра | Описание | Пример |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | Идентификатор из твоего манифеста. |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | Идентификатор элемента во вкладке, который вы предоставили при [настройке вкладки.](~/tabs/how-to/create-tab-pages/configuration-page.md)|Целевой список123|
| `entityWebUrl` или `subEntityWebUrl`&emsp; | Дополнительное поле с обратным URL для использования, если клиент не поддерживает визуализацию вкладки. | https://tasklist.example.com/123 или https://tasklist.example.com/list123/task456 |
| `entityLabel` или `subEntityLabel`&emsp; | Метка для элемента в вкладке, чтобы использовать при отображении глубокой ссылке. | Список задач 123 или "Task 456 |
| `context`&emsp; </br></br>* `subEntityId`&emsp;</br></br> * `channelId`&emsp;| Объект JSON, содержащий следующие поля:</br></br> Идентификатор элемента во вкладке. </br></br> Идентификатор Microsoft Teams, который доступен в контексте [вкладки.](~/tabs/how-to/access-teams-context.md) | 
| `subEntityId`&emsp; | Идентификатор элемента во вкладке. |Задача456 |
| `channelId`&emsp; | Идентификатор Microsoft Teams, который доступен из контекста [вкладки.](~/tabs/how-to/access-teams-context.md) Это свойство доступно только в настраиваемых вкладок с областью **команды.** Он не доступен в статических вкладок, которые имеют область **личных**.| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |

Примеры:

* Ссылка на сам настраиваемый вкладку: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Ссылка на элемент задачи в настраиваемой вкладке: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Ссылка на сам статический вкладку: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* Ссылка на элемент задачи в статической вкладке: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> Убедитесь, что все параметры запроса должным образом закодированы URI. Вы должны следовать примерам preceeding, используя последний пример:

> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consume-a-deep-link-from-a-tab"></a>Потребляйте глубокую ссылку из вкладки

При переходе на глубокую ссылку Microsoft Teams просто переходит на вкладку и предоставляет механизм через библиотеку Microsoft Teams JavaScript для извлечения идентификатора подуком образования, если он существует.

Вызов [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) возвращает контекст, который включает в себя `subEntityId` поле, если вкладка перемещается по глубокой ссылке.

## <a name="deep-linking-from-your-tab"></a>Глубокая ссылка с вкладки

Вы можете глубоко ссылку на содержание в Teams из вашей вкладке. Это полезно, если вкладке необходимо ссылку на другое содержимое в Teams, например, на канал, сообщение, другую вкладку или даже открыть диалог планирования. Чтобы вызвать глубокую ссылку из вкладки, вы должны позвонить:

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Этот вызов переходит к правильному URL-адресу или запускает действия клиента, такие как открытие планирования или диалог установки приложения. Пример приведен в следующей статье:

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Глубокая ссылка на чат

Вы можете создать глубокие ссылки на приватные чаты между пользователями, указав набор участников. Если чата нет с указанными участниками, ссылка переходит пользователю в пустой новый чат. Новые чаты создаются в состоянии проекта до тех пор, пока пользователь не отправит первое сообщение. В противном случае можно указать имя чата, если его еще нет, а также текст, который должен быть вставлен в поле составления композиций пользователя. Вы можете думать об этой функции, как ярлык для пользователя, принимая ручное действие навигации или создания чата, а затем набрав сообщение.

В качестве примера использования случае, если вы возвращаете Office 365 профиля пользователя из вашего бота в качестве карты, эта глубокая ссылка может позволить пользователю легко общаться с этим человеком.

### <a name="generate-a-deep-link-to-a-chat"></a>Создание глубокой ссылки на чат

Используйте этот формат для глубокой ссылки, которую можно использовать в боте, разъеме или карте расширения обмена сообщениями:

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Пример: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Параметры запроса:

* `users`: Запятый список пользовательских iD,3, представляющих участников чата. Пользователь, который выполняет действие, всегда включается в качестве участника. В настоящее время поле User ID поддерживает Azure AD UserPrincipalName, например только адрес электронной почты.
* `topicName`: Дополнительное поле для отображения имени чата, в случае чата с 3 или более пользователями. Если это поле не указано, имя отображения чата основано на именах участников.
* `message`: Дополнительное поле для текста сообщения, которое вы хотите вставить в текущее поле композиции пользователя, пока чат находится в состоянии чернового проекта.

Чтобы использовать эту глубокую связь с ботом, укажите это в качестве цели URL в кнопке карты или нажмите действие через `openUrl` тип действия.

## <a name="generate-deep-links-to-file-in-channel"></a>Создание глубоких ссылок на файл в канале

Следующий формат глубокой ссылки может быть использован в боте, разъеме или карте расширения обмена сообщениями:

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

Параметры запроса:

* `tenantId`: Арендатор ID пример, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb
* `fileType`: Поддерживаемый тип файла, такие как docx, pptx, xlsx и pdf
* `objectUrl`: URL-адрес файла, https://microsoft.sharepoint.com/teams/(filepath)
* `baseUrl`: Базовый URL файла, https://microsoft.sharepoint.com/teams
* `serviceName`: Название службы, идентификатор приложения
* `threadId`: threadId является идентификатором команды команды, где хранится файл. Он не является обязательным и не может быть установлен для файлов, хранящихся в папке OneDrive пользователя. threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype
* `groupId`: Идентификатор группы файла, ae063b79-5315-4ddb-ba70-27328ba6c31e

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
## <a name="deep-linking-for-sharepoint-framework-tabs"></a>Глубокая ссылка для SharePoint Framework вкладок

Следующий формат глубокой ссылки может быть использован в боте, разъеме или карте расширения обмена сообщениями: `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> Когда бот отправляет сообщение TextBlock с глубокой ссылкой, новая вкладка браузера открывается, когда пользователи выбирают ссылку. Это происходит в Chrome и Microsoft Teams приложении, запущенной на Linux.
> Если бот отправляет тот же глубокий URL-адрес ссылки `Action.OpenUrl` в, Teams вкладка открывается в текущем браузере, когда пользователь выбирает ссылку. Новая вкладка браузера не открыта.

Параметры запроса:

* `appID`: Ваш манифест ID **fe4a8eba-2a31-4737-8e33-e5fae6fee194**.

* `entityID`: Идентификатор элемента, который вы предоставили при [настройке вкладки.](~/tabs/how-to/create-tab-pages/configuration-page.md) Например, **список задач123**.
* `entityWebUrl`: Дополнительное поле с обратным URL для использования, если клиент не поддерживает визуализацию вкладки - https://tasklist.example.com/123 или https://tasklist.example.com/list123/task456 .
* `entityName`: Метка для элемента во вкладке, для использования при отображении глубокой ссылки, список задач 123 или задача 456.

Пример: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList

## <a name="deep-linking-to-the-scheduling-dialog"></a>Глубокая ссылка на диалог планирования

> [!NOTE]
> Эта функция в настоящее время находится в предварительном просмотре разработчика.

Вы можете создать глубокие ссылки Teams встроенный диалог планирования. Это особенно полезно, если приложение помогает пользователю выполнять задачи, связанные с календарем или планированием.

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>Создание глубокой ссылки на диалог планирования

Используйте следующий формат для глубокой ссылки, которую можно использовать в карте расширения бота, разъема или обмена сообщениями: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Пример: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

Параметры запроса:

* `attendees`: Дополнительный запятый список пользовательских iD-интерфейсов, представляющих участников собрания. Пользователь, выполняющий действие, является организатором собрания. Поле идентификатора пользователя в настоящее время поддерживает только Azure AD UserPrincipalName, обычно адрес электронной почты.
* `startTime`: Дополнительное время начала мероприятия. Это должно быть в [длинном формате ISO 8601,](https://en.wikipedia.org/wiki/ISO_8601) *например 2018-03-12T23:55:25-02:00*.
* `endTime`: Дополнительное время окончания мероприятия, также в формате ISO 8601.
* `subject`: Дополнительное поле для темы встречи.
* `content`: Дополнительное поле для поля деталей собрания.

> [!NOTE]
> В настоящее время указание местоположения не поддерживается. Вы должны указать UTC смещения, это означает часовые пояса при генерации вашего начала и конца времени.

Чтобы использовать эту глубокую связь с ботом, вы можете указать это в качестве цели URL в кнопке карты или нажмите действие через `openUrl` тип действия.

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a>Глубокая ссылка на аудио- или аудио-видеозвонок

Вы можете создать глубокие ссылки для вызова аудио только или аудио-видео звонки для одного пользователя или группы пользователей, указав тип вызова, *как аудио* *или AV*, и участников. После вызова глубокой ссылки и перед размещением вызова Teams настольный клиент подсказывает подтверждение для звонка. В случае группового вызова можно вызвать набор пользователей VoIP и набор пользователей PSTN в том же глубоком вызове ссылки. 

В случае видеозвона клиент попросит подтверждения и включите видео вызывающего абонента для вызова. Получатель вызова имеет выбор ответить только через аудио или аудио и видео, через окно Teams вызова.

> [!NOTE]
> Эта глубокая ссылка не может быть использована для вызова собрания.

### <a name="generate-a-deep-link-to-a-call"></a>Создание глубокой ссылки на вызов

| Глубокая ссылка | Формат | Пример |
|-----------|--------|---------|
| Сделать аудиозвуок | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com |
| Сделать аудио- и видеозвонок | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&&gt; свидео-истинным | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true |
|Сделать аудио- и видеозвонок с дополнительным источником параметров | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&&gt; свидео-истинным&источником»demoApp | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true&source=demoApp |  
| Сделайте аудио- и видеозвонок для комбинации пользователей VoIP и PSTN | https://teams.microsoft.com/l/call/0/0?users=&lt&gt;;user1,4: &lt; phonenumber&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210 |
  
Ниже приведены параметры запроса:
* `users`: Запятый список пользовательских iD-данных, представляющих участников звонка. В настоящее время поле User ID поддерживает Azure AD UserPrincipalName, обычно адрес электронной почты, или в случае вызова PSTN, он поддерживает pstn mri 4: &lt; phonenumber &gt; .
* `Withvideo`: Это дополнительный параметр, который можно использовать для видеозвонок. Установка этого параметра будет только включить камеру вызывающего абонента. Получатель вызова имеет выбор ответить через аудио или аудио-и видеозвонок через окно Teams вызова. 
* `Source`: Это дополнительный параметр, который информирует об источнике глубокой ссылки.

## <a name="code-sample"></a>Пример кода

| Название образца | Описание | C# |Node.js|
|-------------|-------------|------|----|
|Глубокая ссылка потребляющих Идентификатор субентности  |Microsoft Teams для демонстрации deeplink от бот-чата к вкладке, потребляющей Идентификатор Subentity.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>См. также

[Интеграция веб-приложений](~/samples/integrate-web-apps-overview.md)

