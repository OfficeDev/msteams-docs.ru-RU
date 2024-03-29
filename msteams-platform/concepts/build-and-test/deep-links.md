---
title: Создание прямых ссылок
description: Из этой статьи вы узнаете, как создавать глубокие ссылки и перемещаться по ним в приложениях Microsoft Teams с помощью вкладок.
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: b1f9e7b58faeef7223a9bc9b9f9c26cab7bc73e5
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615193"
---
# <a name="create-deep-links"></a>Создание прямых ссылок

Прямые ссылки — это механизм навигации, который можно использовать для подключения пользователей к сведениям и функциям в Teams и приложениях Teams. Некоторые сценарии, в которых может быть полезно создание прямых ссылок:

* Навигация пользователя к содержимому на одной из вкладок приложения. Например, в вашем приложении может быть бот, который отправляет сообщения, уведомляющие пользователя о важном действии. Когда пользователь нажимает на уведомление, прямая ссылка переходит на вкладку, чтобы пользователь мог просмотреть более подробные сведения о действии.
* Ваше приложение автоматизирует или упрощает определенные пользовательские задачи. Вы можете создать чат или запланировать собрание, предварительно заполнив прямые ссылки необходимыми параметрами. Благодаря этому пользователям не потребуется вводить сведения вручную.

Клиентский пакет SDK JavaScript для Microsoft Teams (TeamsJS) упрощает процесс навигации. Во многих сценариях, таких как переход к содержимому и сведениям на вкладке или запуск диалогового окна чата. Пакет SDK предоставляет типизированные API, которые обеспечивают улучшенный интерфейс и могут заменить использование прямых ссылок. Эти API рекомендуются для приложений Teams, которые могут выполняться на других узлах (Outlook, Office), поскольку они также позволяют проверить, поддерживается ли используемая возможность этим узлом. В следующих разделах приведены сведения о создании прямых (глубинных) ссылок, а также показано, как сценарии, которые раньше требовали их, изменились в выпуске TeamsJS версии 2.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

> [!NOTE]
> Поведение прямых ссылок зависит от ряда факторов. В следующем списке описывается поведение прямых ссылок в сущностях Teams.
>
> **Вкладка**:  
> ✔ Непосредственно переходит к URL-адресу прямой ссылки.
>
> **Бот**:  
> ✔ Прямая ссылка в тексте карточки: сначала открывается в браузере.  
> ✔ Прямая ссылка добавлена к действию OpenURL в адаптивной карточке: прямой переход к URL-адресу прямой ссылки.  
> ✔ Текст с разметкой Markdown гиперссылки в карточке: сначала открывается в браузере.  
>
> **Чат**:  
> ✔ Разметка Markdown гиперссылки текстового сообщения: прямой переход к URL-адресу прямой ссылки.  
> ✔ Ссылка, вставленная в общий чат: прямой переход к URL-адресу прямой ссылки.
>
>
>Поведение навигации приложения Teams, расширенного в Microsoft 365 (Outlook/Office), зависит от двух факторов:
>
> * Целевой объект, на который указывает прямая ссылка.
> * Узел, в котором запущено приложение Teams.
>
> Если приложение Teams выполняется в узле, на который ведет прямая ссылка, ваше приложение откроется непосредственно в узле. Однако если приложение Teams запущено в другом узле, отличном от того, на который ведет прямая ссылка, приложение сначала откроется в браузере.

## <a name="deep-link-to-your-tab"></a>Прямая ссылка на вкладку

Можно создавать прямые ссылки на сущности в приложениях Teams. Этот метод используется для создания ссылок, которые переходят к содержимому и сведениям на вкладке. Например, если вкладка содержит список задач, участники группы могут создавать ссылки на отдельные задачи и делиться ими. При выборе ссылки она переходит на вкладку, которая фокусируется на конкретном элементе.

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

Для реализации необходимо добавить действие **копировать ссылку** к каждому элементу. Это можно сделать любым способом, доступным в пользовательском интерфейсе. Когда пользователь выполняет это действие, вызовите [pages.shareDeepLink()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-sharedeeplink&preserve-view=true) для отображения диалогового окна, содержащего ссылку, которую пользователь может скопировать в буфер обмена. При выполнении этого вызова передайте идентификатор элемента. Он будет возвращен в [контексте](~/tabs/how-to/access-teams-context.md) после перехода по ссылке и перезагрузке вкладки.

```javascript
pages.shareDeepLink({ subPageId: <subPageId>, subPageLabel: <subPageLabel>, subPageWebUrl: <subPageWebUrl> })
```

Вам нужно будет заменить поля соответствующими сведениями:

* `subPageId`: уникальный идентификатор элемента на странице, на который вы делаете прямую ссылку.
* `subPageLabel`: метка элемента, используемая для отображения прямой ссылки.
* `subPageWebUrl`: резервный URL-адрес для использования, если клиенту не удается отобразить страницу.

Дополнительные сведения см. на странице [pages.shareDeepLink()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-sharedeeplink&preserve-view=true).

# <a name="teamsjs-v1"></a>[TeamsJS версии 1](#tab/teamsjs-v1)

Чтобы реализовать это, необходимо добавить действие **копирования ссылки** к каждому элементу любым способом, который лучше всего подходит для пользовательского интерфейса. Когда пользователь выполняет это действие, вы вызываете `shareDeepLink()`для отображения диалогового окна, содержащего ссылку, которую пользователь может скопировать в буфер обмена. При выполнении этого вызова вы также передаете идентификатор для вашего элемента, который возвращается в [контексте](~/tabs/how-to/access-teams-context.md), при переходе по ссылке и перезагрузке вкладки.

```javascript
microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })
```

Вам нужно будет заменить поля соответствующими сведениями:

* `subEntityId`: уникальный идентификатор элемента на вкладке, на который вы делаете прямую ссылку.
* `subEntityLabel`: метка элемента, используемая для отображения прямой ссылки.
* `subEntityWebUrl`: необязательное поле с резервным URL-адресом для использования, если клиент не поддерживает отрисовку вкладки.

---

Кроме того, также можно создавать прямые ссылки программным образом, используя формат, указанный далее в этой статье. Вы можете использовать прямые ссылки в сообщениях [ботов](~/bots/what-are-bots.md) и [соединителей](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), которые сообщают пользователям об изменениях на вкладке или элементах в ней.

> [!NOTE]
> Эта прямая ссылка отличается от ссылок, предоставляемых пунктом меню **Копировать ссылку на вкладку**, который просто создает прямую ссылку, указывающую на эту вкладку.

>[!IMPORTANT]
> В настоящее время shareDeepLink не работает на мобильных платформах.

### <a name="consume-a-deep-link-from-a-tab"></a>Использование прямой ссылки из вкладки

При переходе по прямой ссылке Microsoft Teams просто переходит на вкладку и предоставляет механизм для получения идентификатора подстраницы, если он существует. Для этого используется библиотека JavaScript Teams.

Вызов [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) (`microsoftTeams.getContext()`) в TeamsJS версии 1 возвращает обещание, которое будет разрешено с контекстом, включающим свойство `subPageId` (subEntityId для TeamsJS версии 1), если на вкладку можно перейти по прямой ссылке. Дополнительные сведения см. в статье [Интерфейс PageInfo](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true).

### <a name="generate-a-deep-link-to-your-tab"></a>Создание прямой ссылки на вкладку

Хотя рекомендуется использовать `shareDeepLink()` для создания прямой ссылки на вашу вкладку, ее также можно создать вручную.

> [!NOTE]
>
> * Личные вкладки имеют область `personal`, а вкладки каналов и групп используют области `team` или `group`. Два типа вкладок имеют немного разный синтаксис, поскольку только настраиваемая вкладка имеет свойство `channel`, связанное с ее объектом контекста. Дополнительные сведения об областях вкладок см. в справочнике по [манифесту](~/resources/schema/manifest-schema.md).
> * Прямые ссылки работают правильно, только если вкладка была настроена с использованием библиотеки v0.4 или более поздней версии и поэтому имеет идентификатор объекта. Глубокие ссылки на вкладки без идентификаторов сущностей по-прежнему будут переходить на вкладку, но не могут предоставить идентификатор вложенной сущности на вкладке.

Используйте следующий формат для прямой ссылки, которую можно использовать в боте, соединителе или карточке расширения для сообщений:

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Если бот отправляет сообщение, содержащее `TextBlock` с прямой ссылкой, то при выборе пользователем ссылки открывается новая вкладка браузера. Это происходит в Chrome и в классическом приложении Teams, которые работают в Linux.
> Если бот отправляет тот же URL-адрес прямой ссылки в `Action.OpenUrl`, вкладка Teams открывается в текущей вкладке браузера, когда пользователь выбирает ссылку. Новая вкладка браузера не открыта.

<!--- TBD: Edit this article.
* Admonitions/alerts seem to be overused. 
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* List items in the table are not formatted well in output.
* Some headings use -ing verbs.
* Example values and some URLs should be in backticks and not emphasized.
* Codeblock are missing language.
* Check for markdownlint errors.
* Table with just a row isn't really needed. Provide the content without tabulating it.
--->

Параметры запроса:

| Имя параметра | Описание | Пример |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | Идентификатор из центра администрирования Teams. |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | Идентификатор элемента на вкладке, указанный при [настройке вкладки](~/tabs/how-to/create-tab-pages/configuration-page.md). При создании URL-адресов для прямых ссылок продолжайте использовать entityID в качестве имени параметра в URL-адресах. При настройке вкладки объект контекста ссылается на entityID как {page.id}. |Tasklist123|
| `entityWebUrl` или `subEntityWebUrl`&emsp; | Необязательное поле с резервным URL-адресом для использования, если клиент не поддерживает отрисовку вкладки. | `https://tasklist.example.com/123` или `https://tasklist.example.com/list123/task456` |
| `entityLabel` или `subEntityLabel`&emsp; | Метка для элемента на вкладке, используемая при отображении прямой ссылки. | Список задач 123 или "Задача 456" |
| `context.subEntityId`&emsp; | Идентификатор элемента на вкладке. При создании URL-адресов для прямых ссылок продолжайте использовать subEntityId в качестве имени параметра в URL-адресах. При настройке вкладки объект контекста ссылается на subEntityId как subPageID. |Task456 |
| `context.channelId`&emsp; | Идентификатор канала Microsoft Teams, доступный в [контексте](~/tabs/how-to/access-teams-context.md) вкладки. Это свойство доступно только на настраиваемых вкладках с областью **группы**. Оно недоступно на статических вкладках, которые имеют область **личные**.| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |
| `chatId`&emsp; | ИД чата, доступный в [контексте](~/tabs/how-to/access-teams-context.md) вкладки, для группового чата и чата собрания | 17:b42de192376346a7906a7dd5cb84b673@thread.v2 |
| `contextType`&emsp; |  Чат — это единственный поддерживаемый тип контекста для собраний | чат |

**Примеры:**

* Ссылка на статическую (личную) вкладку:

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`

* Ссылка на элемент задачи на статической (личной) вкладке:

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

* Ссылка на настраиваемую вкладку: 

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`

* Ссылка на элемент задачи на настраиваемой вкладке: 

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`

* Ссылка на приложение вкладки, добавленное в чат собрания или групповой чат:

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456?context={"chatId": "17:b42de192376346a7906a7dd5cb84b673@thread.v2","contextType":"chat"}`

> [!IMPORTANT]
> Убедитесь, что все параметры запроса правильно закодированы универсальным кодом ресурса (URI). Вы должны следовать предыдущим примерам, используя последний пример:
>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

## <a name="navigation-from-your-tab"></a>Навигация с вкладки

Вы можете переходить к содержимому в Teams со своей вкладки с помощью TeamsJS или прямых ссылок. Это удобно, если вкладка должна установить связь пользователей с другим содержимым в Teams, например с каналом, сообщением, другой вкладкой или даже для открытия диалогового окна планирования. Раньше для навигации могла требоваться прямая ссылка, но теперь во многих случаях это можно сделать с помощью пакета SDK. В следующих разделах демонстрируются оба метода, но там, где это возможно, рекомендуется использовать типизированные возможности пакета SDK.

Одно из преимуществ использования TeamsJS, особенно для приложения Teams, которое может работать на других узлах (Outlook и Office), заключается в том, что можно проверить, поддерживает ли узел возможности, которые вы пытаетесь использовать. Чтобы проверить поддержку возможности для узла, можно использовать функцию `isSupported()`, связанную с пространством имен API. Пакет SDK TeamsJS организует API в возможности посредством пространств имен. Например, перед использованием API в пространстве имен `pages` можно проверить логическое значение, возвращенное из `pages.isSupported()`, и предпринять соответствующие действия в контексте вашего приложения и пользовательского интерфейса приложений.  

Дополнительные сведения о возможностях и API-интерфейсах в TeamsJS см. в статье [Создание вкладок и других размещенных функций с помощью пакета SDK для клиента Microsoft Teams JavaScript](~/tabs/how-to/using-teams-client-sdk.md#apis-organized-into-capabilities).

### <a name="navigate-within-your-app"></a>Навигация в приложении

В приложении можно перемещаться с помощью TeamsJS. В следующем коде показано, как перейти к определенной сущности в приложении Teams.

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

Вы можете активировать навигацию со своей вкладки с помощью функции [pages.navigateToApp()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-navigatetoapp&preserve-view=true), как показано в следующем коде:

```javascript
if (pages.isSupported()) {
  const navPromise = pages.navigateToApp({ appId: <appId>, pageId: <pageId>, webUrl: <webUrl>, subPageId: <subPageId>, channelId:<channelId>});
  navPromise.
     then((result) => {/*Successful navigation*/}).
     catch((error) => {/*Failed navigation*/});
}
else { /* handle case where capability isn't supported */ }
```

Дополнительные сведения об использовании возможностей страниц см. в [pages.navigateToApp()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-navigatetoapp&preserve-view=true) и пространстве имен [страниц](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest&preserve-view=true) для других параметров навигации. При необходимости также можно напрямую открыть прямую ссылку с помощью функции [app.openLink()](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-openlink&preserve-view=true).

# <a name="teamsjs-v1"></a>[TeamsJS версии 1](#tab/teamsjs-v1)

Чтобы активировать прямую ссылку на вкладке, вызовите:

```javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

---

### <a name="open-a-scheduling-dialog"></a>Открытие диалогового окна планирования

> [!NOTE]
> Чтобы открыть диалоговое окно планирования в Teams, разработчикам необходимо продолжать использовать исходный метод на основе URL-адреса прямой ссылки, так как Teams пока не поддерживает возможность календаря.

Дополнительные сведения о работе с календарем см. в пространстве имен [календаря](/javascript/api/@microsoft/teams-js/calendar?view=msteams-client-js-latest&preserve-view=true) в справочной документации по API.

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

```javascript
// Open a scheduling dialog from your tab
if(calendar.isSupported()) {
   const calendarPromise = calendar.composeMeeting({
      attendees: ["joe@contoso.com", "bob@contoso.com"],
      content: "test content",
      endTime: "2018-10-24T10:30:00-07:00",
      startTime: "2018-10-24T10:00:00-07:00",
      subject: "test subject"});
   calendarPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

# <a name="teamsjs-v1"></a>[TeamsJS версии 1](#tab/teamsjs-v1)

```javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");
```

---

Также можно вручную создавать прямые ссылки на встроенное диалоговое окно планирования Teams.

#### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>Создание прямой ссылки на диалоговое окно планирования

Рекомендуется использовать типизированные API-интерфейсы TeamsJS, но можно вручную создать прямые ссылки на встроенный диалог планирования Teams. Используйте следующий формат для прямой ссылки, которую можно применять в боте, соединителе или карточке расширения для сообщений: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Пример: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

> [!NOTE]
> Параметры поиска не поддерживают сигнал `+` вместо пробела (``). Убедитесь, что код кодировки универсального кода ресурса (URI) возвращает `%20`, например, пробелы, `?subject=test%20subject` это хорошо, но `?subject=test+subject` — плохо.

Параметры запроса:

* `attendees`: необязательный список идентификаторов пользователей, разделенный запятыми, представляющий участников собрания. Пользователь, выполняющий действие, является организатором собрания. В настоящее время поле идентификатора пользователя поддерживает только UserPrincipalName Azure AD, обычно это адрес электронной почты.
* `startTime`: необязательное время начала события. Это должно быть в [длинном формате ISO 8601](https://en.wikipedia.org/wiki/ISO_8601), например *2018-03-12T23:55:25+02:00*.
* `endTime`: необязательное время окончания события, также в формате ISO 8601.
* `subject`: необязательное поле для темы собрания.
* `content`: необязательное поле для поля сведений о собрании.

> [!NOTE]
> Currently, specifying the location isn't supported. You must specify the UTC offset, it means time zones when generating your start and end times.

Чтобы использовать эту прямую ссылку с ботом, ее можно указать в качестве целевого URL-адреса на кнопке карточки или коснитесь действия через тип действия `openUrl`.

### <a name="open-an-app-install-dialog"></a>Открытие диалогового окна установки приложения

Диалоговое окно установки можно открыть из приложения Teams, как показано в следующем коде.

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

```javascript
// Open an app install dialog from your tab
if(appInstallDialog.isSupported()) {
    const dialogPromise = appInstallDialog.openAppInstallDialog({ appId: <appId>});
    dialogPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

Дополнительные сведения о диалоговом окне установки см. в описании функции [appInstallDialog.openAppInstallDialog()](/javascript/api/@microsoft/teams-js/appinstalldialog?view=msteams-client-js-latest#@microsoft-teams-js-appinstalldialog-openappinstalldialog&preserve-view=true) в справочной документации по API.

# <a name="teamsjs-v1"></a>[TeamsJS версии 1](#tab/teamsjs-v1)

```javascript
// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

---

### <a name="navigate-to-a-chat"></a>Переход к чату

Вы можете перейти к личным чатам или создать их между пользователями с помощью TeamsJS, указав набор участников. Если чат с указанными участниками не существует, пользователь будет перенаправлен в новый пустой чат. Новые чаты создаются в состоянии черновика, пока пользователь не отправит первое сообщение. Или же можно указать имя чата, если он еще не существует, вместе с текстом, который должен быть вставлен в поле создания сообщения пользователя. Эту функцию можно использовать в качестве ярлыка для пользователя, выполняющего ручное действие по навигации или созданию чата, а затем вводя сообщение.

Вариант использования: если вы возвращаете профиль пользователя Office 365 из бота в виде карточки, эта прямая ссылка позволит пользователю легко общаться с этим человеком. В следующем примере показано, как открыть сообщение чата для группы участников с исходным сообщением.

```javascript
if(chat.isSupported()) {
    const chatPromise = chat.openGroupChat({ users: ["joe@contoso.com","bob@contoso.com"], topic: "Prep For Meeting Tomorrow", message: "Hi folks kicking off chat about our meeting tomorrow"});
    chatPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

Рекомендуется использовать типизированные API, но также можно использовать следующий формат для созданной вручную прямой ссылки, которую можно использовать в боте, соединителе или карточке расширения для сообщений:

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Пример: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Параметры запроса:

* `users`: разделенный запятыми список идентификаторов пользователей, представляющих участников чата. Пользователь, выполняющий действие, всегда включен в качестве участника. В настоящее время поле ID пользователя поддерживает UserPrincipalName из Microsoft Azure Active Directory (Azure AD), например только адрес электронной почты.
* `topicName`: необязательное поле для отображаемого имени чата, если в чате участвуют хотя бы три пользователя. Если это поле не указано, отображаемое имя чата основывается на именах участников.
* `message`: необязательное поле для текста сообщения, которое необходимо вставить в поле создания текущего пользователя, когда чат находится в состоянии черновика.

Чтобы использовать эту прямую ссылку с ботом, укажите ее в качестве целевого URL-адреса на кнопке карточки или коснитесь действия через тип действия `openUrl`.

### <a name="generate-deep-links-to-channel-conversation"></a>Создавайте глубокие ссылки на беседу в канале

Используйте этот формат глубокой ссылки, чтобы перейти к определенной беседе в потоке канала:

`https://teams.microsoft.com/l/message/<channelId>/<parentMessageId>?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=<parentMessageId>&teamName=<teamName>&channelName=<channelName>&createdTime=<createdTime>`

Пример: `https://teams.microsoft.com/l/message/<channelId>/1648741500652?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=1648741500652&teamName=<teamName>&channelName=<channelName>&createdTime=1648741500652`

Параметры запроса:

* `channelId`: идентификатор канала беседы. Например, `19:3997a8734ee5432bb9cdedb7c432ae7d@thread.tacv2`.
* `tenantId`: ИД клиента, например `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `groupId`: идентификатор группы файла. Например, `3606f714-ec2e-41b3-9ad1-6afb331bd35d`.
* `parentMessageId`: идентификатор родительского сообщения в беседе.
* `teamName`: имя команды.
* `channelName`: название канала команды.

> [!NOTE]
> Вы можете увидеть `channelId` и `groupId` в URL-адресе канала.

### <a name="generate-deep-links-to-file-in-channel"></a>Создание прямых ссылок на файл в канале

Следующий формат прямой ссылки используется в карточке бота, соединителя или расширения для сообщений: 

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

Параметры запроса:

* `fileId`: Unique file ID from Sharepoint Online, also known as `sourcedoc`. For example,`1FA202A5-3762-4F10-B550-C04F81F6ACBD`.
* `tenantId`: ИД клиента, например `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `fileType`: поддерживаемый тип файла, например DOCX, PPTX, XLSX и PDF.
* `objectUrl`: URL-адрес объекта файла. Представлено в формате `https://{tenantName}.sharepoint.com/sites/{TeamName}/SharedDocuments/{ChannelName}/FileName.ext`. Например, `https://microsoft.sharepoint.com/teams/(filepath)`.
* `baseUrl`: базовый URL-адрес файла. Представлено в формате `https://{tenantName}.sharepoint.com/sites/{TeamName}`. Например, `https://microsoft.sharepoint.com/teams`.
* `serviceName`: имя службы, идентификатор приложения Например, `teams`.
* `threadId`: threadId — это идентификатор команды, в которой хранится файл. Это необязательно и не может быть установлено для файлов, хранящихся в пользовательской папке OneDrive. threadId — 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype.
* `groupId`: идентификатор группы файла. Например, `ae063b79-5315-4ddb-ba70-27328ba6c31e`.

> [!NOTE]
> Вы можете увидеть `threadId` и `groupId` в URL-адресе канала.  

Следующий формат прямой ссылки используется в карточке бота, соединителя или расширения для сообщений: 

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

Следующий пример формата иллюстрирует глубокую ссылку на файлы:

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

#### <a name="serialization-of-this-object"></a>Сериализация этого объекта

```javascript
{
fileId: "5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80",
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```

## <a name="deep-linking-to-an-app"></a>Создание прямых ссылок на приложение

Создайте прямую ссылку для приложения после того, как приложение появится в магазине Teams. Чтобы создать ссылку для запуска Teams, добавьте идентификатор приложения к следующему URL-адресу: `https://teams.microsoft.com/l/app/<your-app-id>`. Откроется диалоговое окно для установки или открытия приложения.

> [!NOTE]
> Если ваше приложение утверждено для мобильной платформы, вы можете создать прямую ссылку на приложение на мобильном устройстве. Идентификатор команды Apple App Store Connect требуется дополнительно для подробной ссылки на Teams-iOS. Дополнительные сведения см. в [статье об обновлении идентификатора команды Apple App Store Connect](../deploy-and-publish/appsource/prepare/update-apple-store-team-connect-id.md).

### <a name="deep-linking-for-sharepoint-framework-tabs"></a>Создание прямых ссылок для вкладок SharePoint Framework

Следующий формат прямой ссылки можно использовать в карточке бота, соединителя или расширения для сообщений: `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> Когда бот отправляет сообщение TextBlock с прямой ссылкой, новая вкладка браузера открывается, когда пользователи выбирают ссылку. Это происходит в настольных приложениях Chrome и Microsoft Teams, работающих в Linux.
> Если бот отправляет тот же URL-адрес прямой ссылки в `Action.OpenUrl`, вкладка Teams открывается в текущей вкладке браузера, когда пользователь выбирает ссылку. Новая вкладка браузера не открывается.

Параметры запроса:

* `appID`: ваш манифест, например `fe4a8eba-2a31-4737-8e33-e5fae6fee194`.

* `entityID`: идентификатор элемента, предоставленный при [настройке вкладки](~/tabs/how-to/create-tab-pages/configuration-page.md). Например, `tasklist123`.
* `entityWebUrl`: необязательное поле с резервным URL-адресом для использования, если клиент не поддерживает отрисовку вкладки `https://tasklist.example.com/123` или `https://tasklist.example.com/list123/task456`.
* `entityName`: метка для элемента на вкладке, используемая при отображении прямой ссылки, Task List 123 или Task 456.

Пример: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList`

## <a name="navigate-to-an-audio-or-audio-video-call"></a>Переход к аудио- или аудио-видео вызову

Вы можете совершать только голосовые вызовы или вызовы с аудио и видео для одного пользователя или группы пользователей, указав тип вызова и участников. Перед совершением вызова клиент Teams запрашивает подтверждение для его совершения. В случае группового вызова можно вызвать набор пользователей VoIP и набор пользователей ТСОП в том же вызове глубокой ссылки.

Во время видеовызова клиент запросит подтверждение и включит видео вызывающего абонента для вызова. Получатель звонка может ответить только через голосовой вызов или голосовой и видеовызов через окно уведомления о звонках Teams.

> [!NOTE]
> Этот метод не может быть использован для проведения собрания.

В следующем коде показано использование пакета SDK TeamsJS для начала вызова:

```javascript
if(call.isSupported()) {
    const callPromise = call.startCall({ targets: ["joe@contoso.com","bob@contoso.com","4:9876543210"], requestedModalities: [call.CallModalities.Audio], source: "demoApp"});
    callPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }

```

## <a name="generate-a-deep-link-to-a-call"></a>Создание прямой ссылки на звонок

Рекомендуется использовать типизированные API-интерфейсы TeamsJS, то также можно использовать созданную вручную прямую ссылку, чтобы начать звонок.

| Прямая ссылка | Формат | Пример |
|-----------|--------|---------|
| Совершение голосовых звонков | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com` |
| Совершение голосовых и видеозвонков | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true` |
|Совершение голосовых и видеозвонков с дополнительным источником параметров | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true&source=demoApp` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true&source=demoApp` |  
| Совершение голосовых и видеозвонков пользователям для пользователей протокола VoIP и ТСОП | `https://teams.microsoft.com/l/call/0/0?users=<user1>,4:<phonenumber>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210` |
  
Ниже приведены параметры запроса:

* `users`: разделенный запятыми список идентификаторов пользователей, представляющих участников звонка. Сейчас поле идентификатора пользователя поддерживает UserPrincipalName Azure AD, обычно это адрес электронной почты, или в случае вызова по ТСОП оно поддерживает pstn mri 4:&lt;phonenumber&gt;.
* `withVideo`: это необязательный параметр, который можно использовать для совершения видеовызова. Настройка этого параметра включит только камеру звонящего. Получатель звонка может ответить через голосовой вызов или голосовой и видеовызов через окно уведомления о звонках Teams.
* `Source`: это необязательный параметр, который сообщает об источнике прямой ссылки.

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | C# |Node.js|
|-------------|-------------|------|----|
|Прямая ссылка использует ИД подсущности  | Пример приложения Teams для демонстрации прямой ссылки из чата с ботом на вкладку, использующую ИД подсущности.|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>Дополнительные ресурсы

* [Интеграция веб-приложений](~/samples/integrate-web-apps-overview.md)
* [Moodle LMS](~/resources/moodleinstructions.md)
