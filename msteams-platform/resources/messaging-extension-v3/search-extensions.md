---
title: Поиск с расширениями обмена сообщениями
description: Описание разработки расширений для обмена сообщениями на основе поиска
keywords: службы расширения обмена сообщениями Teams.
ms.date: 05/20/2019
ms.openlocfilehash: 7baf55d7184784a436ac5a3d6b82db233389bca7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675454"
---
# <a name="search-with-messaging-extensions"></a><span data-ttu-id="8a982-104">Поиск с расширениями обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="8a982-104">Search with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="8a982-105">Расширения обмена сообщениями на основе поиска позволяют запросить службу и отправить эти сведения в виде карточки, прямо в сообщение.</span><span class="sxs-lookup"><span data-stu-id="8a982-105">Search based messaging extensions allow you to query your service and post that information in the form of a card, right into your message</span></span>

![Пример карточки расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="8a982-107">В следующих разделах описано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="8a982-107">The following sections describe how to do this.</span></span>

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a><span data-ttu-id="8a982-108">Расширения сообщений для типа поиска</span><span class="sxs-lookup"><span data-stu-id="8a982-108">Search type message extensions</span></span>

<span data-ttu-id="8a982-109">Для расширения системы обмена сообщениями на `type` основе поиска `query`задайте для параметра значение.</span><span class="sxs-lookup"><span data-stu-id="8a982-109">For search based messaging extension set the `type` parameter to `query`.</span></span> <span data-ttu-id="8a982-110">Ниже приведен пример манифеста с одной командой поиска.</span><span class="sxs-lookup"><span data-stu-id="8a982-110">Below is an example of a manifest with a single search command.</span></span> <span data-ttu-id="8a982-111">Одно расширение обмена сообщениями может иметь до 10 различных команд, связанных с ней.</span><span class="sxs-lookup"><span data-stu-id="8a982-111">A single messaging extension can have up to 10 different commands associated with it.</span></span> <span data-ttu-id="8a982-112">Сюда могут входить как несколько команд поиска, так и несколько команд, основанных на действиях.</span><span class="sxs-lookup"><span data-stu-id="8a982-112">This can include both multiple search and multiple Action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="8a982-113">Пример полного манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="8a982-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.bing",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://bingbotservice.azurewebsites.net/",
    "privacyUrl": "http://bingbotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://bingbotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "Bing",
    "full": "Bing"
  },
  "description": {
    "short": "Find Bing search results",
    "full": "Find Bing search results and share them with your team members."
  },
  "icons": {
    "outline": "bing-outline.jpg",
    "color": "bing-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "bingbotservice.azurewebsites.net",
    "*.bingbotservice.azurewebsites.net"
  ]
}
```

### <a name="test-via-uploading"></a><span data-ttu-id="8a982-114">Тестирование через отправку</span><span class="sxs-lookup"><span data-stu-id="8a982-114">Test via uploading</span></span>

<span data-ttu-id="8a982-115">Вы можете проверить расширение системы обмена сообщениями, отправив свое приложение.</span><span class="sxs-lookup"><span data-stu-id="8a982-115">You can test your messaging extension by uploading your app.</span></span>

<span data-ttu-id="8a982-116">Чтобы открыть расширение системы обмена сообщениями, перейдите к любому из бесед или каналов.</span><span class="sxs-lookup"><span data-stu-id="8a982-116">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="8a982-117">Нажмите кнопку **Дополнительные параметры** (**&#8943;**) в поле создать и выберите ваш добавочный номер для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8a982-117">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="add-event-handlers"></a><span data-ttu-id="8a982-118">Добавление обработчиков событий</span><span class="sxs-lookup"><span data-stu-id="8a982-118">Add event handlers</span></span>

<span data-ttu-id="8a982-119">Большая часть работы включает `onQuery` событие, которое обрабатывает все взаимодействия в окне расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8a982-119">Most of your work involves the `onQuery` event, which handles all interactions in the messaging extension window.</span></span>

<span data-ttu-id="8a982-120">Если вы задаете значение `canUpdateConfiguration` `true` в манифесте, вы включаете элемент меню **Параметры** для расширения системы обмена сообщениями `onQuerySettingsUrl` , `onSettingsUpdate`а также обрабатывает и.</span><span class="sxs-lookup"><span data-stu-id="8a982-120">If you set `canUpdateConfiguration` to `true` in the manifest, you enable the **Settings** menu item for your messaging extension and must also handle `onQuerySettingsUrl` and `onSettingsUpdate`.</span></span>

### <a name="handle-onquery-events"></a><span data-ttu-id="8a982-121">Обработка событий onquery</span><span class="sxs-lookup"><span data-stu-id="8a982-121">Handle onQuery events</span></span>

<span data-ttu-id="8a982-122">Расширение системы обмена сообщениями `onQuery` получает событие, когда что-то происходит в окне расширения обмена сообщениями или отправляется в окно.</span><span class="sxs-lookup"><span data-stu-id="8a982-122">A messaging extension receives an `onQuery` event when anything happens in the messaging extension window or is sent to the window.</span></span>

<span data-ttu-id="8a982-123">Если расширение системы обмена сообщениями использует страницу конфигурации, обработчик `onQuery` должен сначала проверить наличие сохраненных сведений о конфигурации; Если модуль обмена сообщениями не настроен, возвратите `config` ответ со ссылкой на страницу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8a982-123">If your messaging extension uses a configuration page, your handler for `onQuery` should first check for any stored configuration information; if the messaging extension isn't configured, return a `config` response with a link to your configuration page.</span></span> <span data-ttu-id="8a982-124">Помните, что ответ на странице конфигурации также обрабатывается `onQuery`.</span><span class="sxs-lookup"><span data-stu-id="8a982-124">Be aware that the response from the configuration page is also handled by `onQuery`.</span></span> <span data-ttu-id="8a982-125">(Единственное исключение — при вызове страницы конфигурации обработчиком `onQuerySettingsUrl`; см. следующий раздел.)</span><span class="sxs-lookup"><span data-stu-id="8a982-125">(The sole exception is when the configuration page is called by the handler for `onQuerySettingsUrl`; see the following section.)</span></span>

<span data-ttu-id="8a982-126">Если для расширения системы обмена сообщениями требуется проверка подлинности, проверьте сведения о состоянии пользователя; Если пользователь не вошел в систему, следуйте инструкциям в разделе [authentication (проверка подлинности](#authentication) ) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="8a982-126">If your messaging extension requires authentication, check the user state information; if the user isn't signed in, follow the instructions in the [Authentication](#authentication) section later in this topic.</span></span>

<span data-ttu-id="8a982-127">Затем проверьте, установлен `initialRun` ли параметр; Если это так, выполните соответствующие действия, такие как предоставление инструкций или списка ответов.</span><span class="sxs-lookup"><span data-stu-id="8a982-127">Next, check whether `initialRun` is set; if so, take appropriate action, such as providing instructions or a list of responses.</span></span>

<span data-ttu-id="8a982-128">В оставшейся части обработчика `onQuery` запрашивается информация для пользователя, отображается список карточек предварительного просмотра и возвращается карточка, выбранная пользователем.</span><span class="sxs-lookup"><span data-stu-id="8a982-128">The remainder of your handler for `onQuery` prompts the user for information, displays a list of preview cards, and returns the card selected by the user.</span></span>

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a><span data-ttu-id="8a982-129">Обработка событий Онкуерисеттингсурл и Онсеттингсупдате</span><span class="sxs-lookup"><span data-stu-id="8a982-129">Handle onQuerySettingsUrl and onSettingsUpdate events</span></span>

<span data-ttu-id="8a982-130">События `onQuerySettingsUrl` and `onSettingsUpdate` работают вместе, чтобы включить элемент меню **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="8a982-130">The `onQuerySettingsUrl` and `onSettingsUpdate` events work together to enable the **Settings** menu item.</span></span>

![Снимки экрана расположения элемента меню параметров](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

<span data-ttu-id="8a982-132">Обработчик `onQuerySettingsUrl` возвращает URL-адрес страницы конфигурации; После закрытия страницы конфигурации обработчик `onSettingsUpdate` принимает и сохраняет возвращенное состояние.</span><span class="sxs-lookup"><span data-stu-id="8a982-132">Your handler for `onQuerySettingsUrl` returns the URL for the configuration page; after the configuration page closes, your handler for `onSettingsUpdate` accepts and saves the returned state.</span></span> <span data-ttu-id="8a982-133">(Это тот случай, когда `onQuery` он *не* получает ответ со страницы Configuration.)</span><span class="sxs-lookup"><span data-stu-id="8a982-133">(This is the one case in which `onQuery` *doesn't* receive the response from the configuration page.)</span></span>

## <a name="receive-and-respond-to-queries"></a><span data-ttu-id="8a982-134">Получение запросов и реагирование на них</span><span class="sxs-lookup"><span data-stu-id="8a982-134">Receive and respond to queries</span></span>

<span data-ttu-id="8a982-135">Каждый запрос к своему расширению обмена сообщениями выполняется `Activity` через объект, который отправляется на URL-адрес обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="8a982-135">Every request to your messaging extension is done via an `Activity` object that is posted to your callback URL.</span></span> <span data-ttu-id="8a982-136">Запрос содержит сведения о команде User, такие как идентификатор и значения параметров.</span><span class="sxs-lookup"><span data-stu-id="8a982-136">The request contains information about the user command, such as ID and parameter values.</span></span> <span data-ttu-id="8a982-137">В запросе также предоставляются метаданные о контексте, в котором был вызван ваш добавочный номер, включая ИДЕНТИФИКАТОРы пользователей и клиентов, а также ИДЕНТИФИКАТОРы и идентификаторы каналов и групп.</span><span class="sxs-lookup"><span data-stu-id="8a982-137">The request also supplies metadata about the context in which your extension was invoked, including user and tenant ID, along with chat ID or channel and team IDs.</span></span>

### <a name="receive-user-requests"></a><span data-ttu-id="8a982-138">Получение запросов пользователей</span><span class="sxs-lookup"><span data-stu-id="8a982-138">Receive user requests</span></span>

<span data-ttu-id="8a982-139">Когда пользователь выполняет запрос, Microsoft Teams отправляет службу стандартным объектом Bot Framework `Activity` .</span><span class="sxs-lookup"><span data-stu-id="8a982-139">When a user performs a query, Microsoft Teams sends your service a standard Bot Framework `Activity` object.</span></span> <span data-ttu-id="8a982-140">Служба должна выполнять свою логику для параметра `Activity` , для `type` которого установлено `invoke` `name` значение поддерживаемого `composeExtension` типа, как показано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="8a982-140">Your service should perform its logic for an `Activity` that has `type` set to `invoke` and `name` set to a supported `composeExtension` type, as shown in the following table.</span></span>

<span data-ttu-id="8a982-141">В дополнение к стандартным свойствам действия Bot полезные данные содержат следующие метаданные запроса:</span><span class="sxs-lookup"><span data-stu-id="8a982-141">In addition to the standard bot activity properties, the payload contains the following request metadata:</span></span>

|<span data-ttu-id="8a982-142">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="8a982-142">Property name</span></span>|<span data-ttu-id="8a982-143">Назначение</span><span class="sxs-lookup"><span data-stu-id="8a982-143">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="8a982-144">Тип запроса; должно быть `invoke`.</span><span class="sxs-lookup"><span data-stu-id="8a982-144">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="8a982-145">Тип команды, выданной службе.</span><span class="sxs-lookup"><span data-stu-id="8a982-145">Type of command that is issued to your service.</span></span> <span data-ttu-id="8a982-146">В настоящее время поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="8a982-146">Currently the following types are supported:</span></span> <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| <span data-ttu-id="8a982-147">Идентификатор пользователя, отправившего запрос.</span><span class="sxs-lookup"><span data-stu-id="8a982-147">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="8a982-148">Имя пользователя, отправившего запрос.</span><span class="sxs-lookup"><span data-stu-id="8a982-148">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="8a982-149">Идентификатор объекта Azure Active Directory пользователя, отправившего запрос.</span><span class="sxs-lookup"><span data-stu-id="8a982-149">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="8a982-150">Идентификатор клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8a982-150">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="8a982-151">Идентификатор канала (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="8a982-151">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="8a982-152">Идентификатор группы (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="8a982-152">Team ID (if the request was made in a channel).</span></span> |
|<span data-ttu-id="8a982-153">`clientInfo`лицо</span><span class="sxs-lookup"><span data-stu-id="8a982-153">`clientInfo` entity</span></span> | <span data-ttu-id="8a982-154">Дополнительные метаданные о клиенте, такие как языковой стандарт/язык и тип клиента.</span><span class="sxs-lookup"><span data-stu-id="8a982-154">Additional metadata about the client, such as locale/language and type of client.</span></span> |

<span data-ttu-id="8a982-155">Собственно параметры запроса находятся в объекте value, который включает следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="8a982-155">The request parameters itself are found in the value object, which includes the following properties:</span></span>

| <span data-ttu-id="8a982-156">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="8a982-156">Property name</span></span> | <span data-ttu-id="8a982-157">Назначение</span><span class="sxs-lookup"><span data-stu-id="8a982-157">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="8a982-158">Имя команды, вызываемой пользователем, которая соответствует одной из команд, объявленных в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="8a982-158">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="8a982-159">Массив параметров.</span><span class="sxs-lookup"><span data-stu-id="8a982-159">Array of parameters.</span></span> <span data-ttu-id="8a982-160">Каждый объект Parameter содержит имя параметра вместе со значением параметра, предоставленным пользователем.</span><span class="sxs-lookup"><span data-stu-id="8a982-160">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="8a982-161">Параметры разбивки на страницы:</span><span class="sxs-lookup"><span data-stu-id="8a982-161">Pagination parameters:</span></span> <br><span data-ttu-id="8a982-162">`skip`: количество пропусков для этого запроса</span><span class="sxs-lookup"><span data-stu-id="8a982-162">`skip`: skip count for this query</span></span> <br><span data-ttu-id="8a982-163">`count`: число возвращаемых элементов</span><span class="sxs-lookup"><span data-stu-id="8a982-163">`count`: number of elements to return</span></span> |

#### <a name="request-example"></a><span data-ttu-id="8a982-164">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="8a982-164">Request example</span></span>

```json
{
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  "type": "invoke",
  "timestamp": "2017-05-01T15:45:51.876Z",
  "localTimestamp": "2017-05-01T08:45:51.876-07:00",
  "id": "f:622749630322482883",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
    "name": "Larry Jin",
    "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
  },
  "conversation": {
    "id": "19:skypespaces_8198cfe0dd2647ae91930f0974768a40@thread.skype"
  },
  "recipient": {
    "id": "28:b4922ea1-5315-4fd0-9b21-d941ab06e39f",
    "name": "TheComposeExtensionDev"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "timezone": "America/Los_Angeles",
      "type": "clientInfo"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a><span data-ttu-id="8a982-165">Получение запросов от ссылок, вставленных в окно сообщения создания</span><span class="sxs-lookup"><span data-stu-id="8a982-165">Receive requests from links inserted into the compose message box</span></span>

<span data-ttu-id="8a982-166">В качестве альтернативы (или дополнительно) для поиска во внешней службе можно использовать URL-адрес, вставленный в поле создать сообщение, чтобы отправить запрос в службу и возвратить карточку.</span><span class="sxs-lookup"><span data-stu-id="8a982-166">As an alternative (or in addition) to searching your external service, you can use a URL inserted into the compose message box to query your service and return a card.</span></span> <span data-ttu-id="8a982-167">На снимке экрана после вставки пользователя в URL-адрес рабочего элемента в Azure DevOps, который разрешал расширение обмена сообщениями в карточке.</span><span class="sxs-lookup"><span data-stu-id="8a982-167">In the screenshot below a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Пример ссылки унфурлинг](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

<span data-ttu-id="8a982-169">Чтобы разрешить своему расширению обмена сообщениями взаимодействовать с ссылками таким способом, сначала необходимо добавить `messageHandlers` массив в манифест приложения, как показано в примере ниже:</span><span class="sxs-lookup"><span data-stu-id="8a982-169">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below:</span></span>

```json
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
]
```

<span data-ttu-id="8a982-170">Добавив домен для прослушивания манифеста приложения, вам потребуется изменить код ленты, чтобы [ответить](#respond-to-user-requests) на следующий запрос Invoke.</span><span class="sxs-lookup"><span data-stu-id="8a982-170">Once you've added the domain to listen on to the app manifest, you'll need to change your bot code to [respond](#respond-to-user-requests) to the below invoke request.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="8a982-171">Если ваше приложение возвращает несколько элементов, будет использоваться только первый.</span><span class="sxs-lookup"><span data-stu-id="8a982-171">If your app returns multiple items only the first will be used.</span></span>

### <a name="respond-to-user-requests"></a><span data-ttu-id="8a982-172">Ответ на запросы пользователей</span><span class="sxs-lookup"><span data-stu-id="8a982-172">Respond to user requests</span></span>

<span data-ttu-id="8a982-173">Когда пользователь выполняет запрос, Microsoft Teams отправляет службе синхронный HTTP-запрос.</span><span class="sxs-lookup"><span data-stu-id="8a982-173">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="8a982-174">В этот момент код имеет 5 секунд, чтобы предоставить HTTP-ответ на запрос.</span><span class="sxs-lookup"><span data-stu-id="8a982-174">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="8a982-175">В течение этого времени служба может выполнять дополнительные операции поиска или любую другую бизнес-логику, необходимую для обслуживания запроса.</span><span class="sxs-lookup"><span data-stu-id="8a982-175">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="8a982-176">Служба должна отвечать на результаты, соответствующие запросу пользователя.</span><span class="sxs-lookup"><span data-stu-id="8a982-176">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="8a982-177">Ответ должен указывать код состояния HTTP `200 OK` и допустимый объект Application/JSON следующего основного текста:</span><span class="sxs-lookup"><span data-stu-id="8a982-177">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="8a982-178">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="8a982-178">Property name</span></span>|<span data-ttu-id="8a982-179">Назначение</span><span class="sxs-lookup"><span data-stu-id="8a982-179">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="8a982-180">Конверт отклика верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="8a982-180">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="8a982-181">Тип ответа.</span><span class="sxs-lookup"><span data-stu-id="8a982-181">Type of response.</span></span> <span data-ttu-id="8a982-182">Поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="8a982-182">The following types are supported:</span></span> <br><span data-ttu-id="8a982-183">`result`: отображает список результатов поиска</span><span class="sxs-lookup"><span data-stu-id="8a982-183">`result`: displays a list of search results</span></span> <br><span data-ttu-id="8a982-184">`auth`: запрос на проверку подлинности пользователя</span><span class="sxs-lookup"><span data-stu-id="8a982-184">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="8a982-185">`config`: запрашивает у пользователя установку расширения для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="8a982-185">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="8a982-186">`message`: отображается обычное текстовое сообщение</span><span class="sxs-lookup"><span data-stu-id="8a982-186">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="8a982-187">Задает макет вложений.</span><span class="sxs-lookup"><span data-stu-id="8a982-187">Specifies the layout of the attachments.</span></span> <span data-ttu-id="8a982-188">Используется для ответов типа `result`.</span><span class="sxs-lookup"><span data-stu-id="8a982-188">Used for responses of type `result`.</span></span> <br><span data-ttu-id="8a982-189">В настоящее время поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="8a982-189">Currently the following types are supported:</span></span> <br><span data-ttu-id="8a982-190">`list`: список объектов карточек, содержащих поля эскиза, заголовка и текста.</span><span class="sxs-lookup"><span data-stu-id="8a982-190">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="8a982-191">`grid`: сетка эскизов изображений</span><span class="sxs-lookup"><span data-stu-id="8a982-191">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="8a982-192">Массив допустимых объектов вложений.</span><span class="sxs-lookup"><span data-stu-id="8a982-192">Array of valid attachment objects.</span></span> <span data-ttu-id="8a982-193">Используется для ответов типа `result`.</span><span class="sxs-lookup"><span data-stu-id="8a982-193">Used for responses of type `result`.</span></span> <br><span data-ttu-id="8a982-194">В настоящее время поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="8a982-194">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="8a982-195">Предложенные действия.</span><span class="sxs-lookup"><span data-stu-id="8a982-195">Suggested actions.</span></span> <span data-ttu-id="8a982-196">Используется для ответов типа `auth` или. `config`</span><span class="sxs-lookup"><span data-stu-id="8a982-196">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="8a982-197">Сообщение для отображения.</span><span class="sxs-lookup"><span data-stu-id="8a982-197">Message to display.</span></span> <span data-ttu-id="8a982-198">Используется для ответов типа `message`.</span><span class="sxs-lookup"><span data-stu-id="8a982-198">Used for responses of type `message`.</span></span> |

#### <a name="response-card-types-and-previews"></a><span data-ttu-id="8a982-199">Типы карточек ответа и предварительный просмотр</span><span class="sxs-lookup"><span data-stu-id="8a982-199">Response card types and previews</span></span>

<span data-ttu-id="8a982-200">Поддерживаются следующие типы вложений:</span><span class="sxs-lookup"><span data-stu-id="8a982-200">We support the following attachment types:</span></span>

* [<span data-ttu-id="8a982-201">Карточка эскиза</span><span class="sxs-lookup"><span data-stu-id="8a982-201">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="8a982-202">Карточка главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="8a982-202">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="8a982-203">Соединительная карта Office 365</span><span class="sxs-lookup"><span data-stu-id="8a982-203">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="8a982-204">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="8a982-204">Adaptive card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="8a982-205">Общие сведения приведены в [карточки](~/task-modules-and-cards/what-are-cards.md) .</span><span class="sxs-lookup"><span data-stu-id="8a982-205">See [Cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="8a982-206">Сведения о том, как использовать типы карт эскизов и главный Имиджевый баннер, приведены в разделе [Add cards and Card Actions](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="8a982-206">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="8a982-207">Дополнительную документацию по карте соединителей Office 365 можно узнать в статье [Использование соединителей карт office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="8a982-207">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="8a982-208">Список результатов отображается в пользовательском интерфейсе Microsoft Teams с предварительным просмотром каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="8a982-208">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="8a982-209">Предварительный просмотр создается одним из двух способов:</span><span class="sxs-lookup"><span data-stu-id="8a982-209">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="8a982-210">Использование `preview` свойства в `attachment` объекте.</span><span class="sxs-lookup"><span data-stu-id="8a982-210">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="8a982-211">`preview` Вложение может быть только картой главный Имиджевый баннер или эскиза.</span><span class="sxs-lookup"><span data-stu-id="8a982-211">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="8a982-212">Извлекается из базового `title` `text`свойства и `image` свойства вложения.</span><span class="sxs-lookup"><span data-stu-id="8a982-212">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="8a982-213">Они используются только в `preview` том случае, если свойство не задано, а эти свойства доступны.</span><span class="sxs-lookup"><span data-stu-id="8a982-213">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="8a982-214">Вы можете просмотреть предварительный просмотр адаптивной карты или карты Office 365 в списке результатов, просто задав свойство Preview; Это не требуется, если результаты уже главный Имиджевый баннер или эскизы страниц.</span><span class="sxs-lookup"><span data-stu-id="8a982-214">You can display a preview of an Adaptive or Office 365 Connector card in the result list simply by setting its preview property; this is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="8a982-215">Если вы используете предварительный просмотр вложения, это должна быть карта главный Имиджевый баннер или эскиза.</span><span class="sxs-lookup"><span data-stu-id="8a982-215">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="8a982-216">Если свойство Preview не указано, предварительный просмотр карты завершается с ошибками, и ничего не отображается.</span><span class="sxs-lookup"><span data-stu-id="8a982-216">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

#### <a name="response-example"></a><span data-ttu-id="8a982-217">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="8a982-217">Response example</span></span>

<span data-ttu-id="8a982-218">В этом примере показан ответ с двумя результатами, смешивание разных форматов карт: Office 365 Connector и адаптивный.</span><span class="sxs-lookup"><span data-stu-id="8a982-218">This example shows a response with two results, mixing different card formats: Office 365 Connector and Adaptive.</span></span> <span data-ttu-id="8a982-219">Хотя вы, скорее всего, захотите прикрепить к одному формату карточки в своем ответе, он показывает, `preview` как `attachments` свойство каждого элемента в коллекции должно явно определять предварительный просмотр в формате главный Имиджевый баннер или эскиза, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="8a982-219">While you'll likely want to stick with one card format in your response, it shows how the `preview` property of each element in the `attachments` collection must explicitly define a preview in hero or thumbnail format as described above.</span></span>

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

### <a name="default-query"></a><span data-ttu-id="8a982-220">Запрос по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8a982-220">Default query</span></span>

<span data-ttu-id="8a982-221">Если для `initialRun` `true` манифеста задано значение в манифесте, Microsoft Teams по умолчанию выдает запрос "по умолчанию", когда пользователь впервые открывает расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8a982-221">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="8a982-222">Служба может ответить на этот запрос с помощью набора предварительно заполненных результатов.</span><span class="sxs-lookup"><span data-stu-id="8a982-222">Your service can respond to this query with a set of prepopulated results.</span></span> <span data-ttu-id="8a982-223">Это может быть полезно для отображения, например, недавно просмотренных элементов, избранного или любой другой информации, которая не зависит от вводимых пользователем данных.</span><span class="sxs-lookup"><span data-stu-id="8a982-223">This can be useful for displaying, for instance, recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="8a982-224">Запрос по умолчанию имеет ту же структуру, что и любой запрос обычного пользователя, за `initialRun` исключением параметра, `true`строковое значение которого равно.</span><span class="sxs-lookup"><span data-stu-id="8a982-224">The default query has the same structure as any regular user query, except with a parameter `initialRun` whose string value is `true`.</span></span>

#### <a name="request-example-for-a-default-query"></a><span data-ttu-id="8a982-225">Пример запроса для запроса по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8a982-225">Request example for a default query</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="identify-the-user"></a><span data-ttu-id="8a982-226">Идентификация пользователя</span><span class="sxs-lookup"><span data-stu-id="8a982-226">Identify the user</span></span>

<span data-ttu-id="8a982-227">Каждый запрос к службам включает в себя идентификатор пользователя, который выполнил запрос, а также отображаемое имя пользователя и идентификатор объекта Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8a982-227">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="8a982-228">Гарантируется, что значения `id` и `aadObjectId` значения для пользователя Teams прошли проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="8a982-228">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="8a982-229">Они могут использоваться в качестве ключей для поиска учетных данных или любого кэшированного состояния в службе.</span><span class="sxs-lookup"><span data-stu-id="8a982-229">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="8a982-230">Кроме того, каждый запрос содержит идентификатор клиента Azure Active Directory для пользователя, который можно использовать для определения организации пользователя.</span><span class="sxs-lookup"><span data-stu-id="8a982-230">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="8a982-231">Если это возможно, запрос также содержит идентификаторы команд и каналов, из которых поступил запрос.</span><span class="sxs-lookup"><span data-stu-id="8a982-231">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="8a982-232">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="8a982-232">Authentication</span></span>

<span data-ttu-id="8a982-233">Если для вашей службы требуется проверка подлинности пользователя, необходимо войти в систему, прежде чем ее сможет использовать расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8a982-233">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="8a982-234">Если вы написали робот или вкладку, которые подписываются пользователю, этот раздел должен быть знаком.</span><span class="sxs-lookup"><span data-stu-id="8a982-234">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="8a982-235">Последовательность выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8a982-235">The sequence is as follows:</span></span>

1. <span data-ttu-id="8a982-236">Пользователь выдает запрос, или запрос по умолчанию автоматически отправляется в службу.</span><span class="sxs-lookup"><span data-stu-id="8a982-236">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="8a982-237">Служба проверяет, прошел ли пользователь проверку подлинности, проверив идентификатор пользователя Teams.</span><span class="sxs-lookup"><span data-stu-id="8a982-237">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="8a982-238">Если пользователь не прошел проверку подлинности, отправьте `auth` ответ с `openUrl` предложенным действием, включая URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8a982-238">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="8a982-239">Клиент Microsoft Teams запускает всплывающее окно, в котором размещается веб-страница, используя указанный URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8a982-239">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="8a982-240">После входа пользователя необходимо закрыть окно и отправить ему код проверки подлинности в клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="8a982-240">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="8a982-241">Затем клиент Teams повторно отправляет запрос в службу, который включает код проверки подлинности, переданный на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="8a982-241">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="8a982-242">Ваша служба должна проверить, что код проверки подлинности, полученный на шаге 6, соответствует тому, что получено на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="8a982-242">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="8a982-243">Это гарантирует, что злоумышленник не будет пытаться подменить или ослабить процесс входа в систему.</span><span class="sxs-lookup"><span data-stu-id="8a982-243">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="8a982-244">Это фактически "закрывает цикл" для завершения безопасной последовательности проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8a982-244">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="8a982-245">Ответ с действием входа</span><span class="sxs-lookup"><span data-stu-id="8a982-245">Respond with a sign-in action</span></span>

<span data-ttu-id="8a982-246">Чтобы выдать запрос пользователю, не прошедшему проверку подлинности, выполните ответ с `openUrl` предложенным действием типа, которое включает URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8a982-246">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="8a982-247">Пример отклика для действия при входе</span><span class="sxs-lookup"><span data-stu-id="8a982-247">Response example for a sign-in action</span></span>

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
> <span data-ttu-id="8a982-248">Для того чтобы при входе в систему можно было размещаться в всплывающем окне Teams, в списке допустимых доменов приложения должен находиться домен, являющийся частью URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="8a982-248">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="8a982-249">(См. раздел [валиддомаинс](~/resources/schema/manifest-schema.md#validdomains) в схеме манифеста.)</span><span class="sxs-lookup"><span data-stu-id="8a982-249">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="8a982-250">Запуск процесса входа</span><span class="sxs-lookup"><span data-stu-id="8a982-250">Start the sign-in flow</span></span>

<span data-ttu-id="8a982-251">Ваш интерфейс пользователя должен отвечать на запросы и размещаться в всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="8a982-251">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="8a982-252">Он должен интегрироваться с [клиентским пакетом SDK для Microsoft Teams JavaScript](/javascript/api/overview/msteams-client), который использует передачу сообщений.</span><span class="sxs-lookup"><span data-stu-id="8a982-252">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="8a982-253">Как и другие встроенные возможности, выполняемые в Microsoft Teams, код в окне должен вызываться `microsoftTeams.initialize()`первым.</span><span class="sxs-lookup"><span data-stu-id="8a982-253">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="8a982-254">Если ваш код выполняет процесс OAuth, можно передать идентификатор пользователя Teams в ваше окно, которое затем может передать его в URL-адрес входа OAuth.</span><span class="sxs-lookup"><span data-stu-id="8a982-254">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="8a982-255">Завершение процесса входа</span><span class="sxs-lookup"><span data-stu-id="8a982-255">Complete the sign-in flow</span></span>

<span data-ttu-id="8a982-256">Когда запрос на вход завершается и перенаправляется обратно на страницу, он должен выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8a982-256">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="8a982-257">Создайте код безопасности.</span><span class="sxs-lookup"><span data-stu-id="8a982-257">Generate a security code.</span></span> <span data-ttu-id="8a982-258">(Это может быть случайное число.) Необходимо кэшировать этот код в службе, а также учетные данные, полученные с помощью процесса входа (например, OAuth 2,0 tokens).</span><span class="sxs-lookup"><span data-stu-id="8a982-258">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="8a982-259">Позвоните `microsoftTeams.authentication.notifySuccess` и передайте код безопасности.</span><span class="sxs-lookup"><span data-stu-id="8a982-259">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="8a982-260">На этом шаге окно закрывается и управление передается клиенту Teams.</span><span class="sxs-lookup"><span data-stu-id="8a982-260">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="8a982-261">Теперь клиент может повторно отправить исходный запрос пользователя, а также код безопасности в `state` свойстве.</span><span class="sxs-lookup"><span data-stu-id="8a982-261">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="8a982-262">Код может использовать код безопасности для поиска ранее сохраненных учетных данных, чтобы выполнить последовательность проверки подлинности, а затем выполнить запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="8a982-262">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="8a982-263">Пример повторной выданной заявки</span><span class="sxs-lookup"><span data-stu-id="8a982-263">Reissued request example</span></span>

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "locale": "en-US",
        "country": "US",
        "platform": "Web",
        "type": "clientInfo"
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="sdk-support"></a><span data-ttu-id="8a982-264">Поддержка SDK</span><span class="sxs-lookup"><span data-stu-id="8a982-264">SDK support</span></span>

### <a name="net"></a><span data-ttu-id="8a982-265">.NET</span><span class="sxs-lookup"><span data-stu-id="8a982-265">.NET</span></span>

<span data-ttu-id="8a982-266">Для получения и обработки запросов с помощью пакета SDK построителя построителя для .NET можно проверить тип `invoke` действия для входящего действия и затем использовать вспомогательный метод в пакете NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) , чтобы определить, является ли он действием расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8a982-266">To receive and handle queries with the Bot Builder SDK for .NET, you can check for the `invoke` action type on the incoming activity and then use the helper method in the NuGet package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) to determine whether it’s a messaging extension activity.</span></span>

#### <a name="example-code-in-net"></a><span data-ttu-id="8a982-267">Пример кода в .NET</span><span class="sxs-lookup"><span data-stu-id="8a982-267">Example code in .NET</span></span>

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
    if (activity.Type == ActivityTypes.Invoke) // Received an invoke
    {
        if (activity.IsComposeExtensionQuery())
        {
            // This is the response object that will get sent back to the messaging extension request.
            ComposeExtensionResponse invokeResponse = null;

            // This helper method gets the query as an object.
            var query = activity.GetComposeExtensionQueryData();

            if (query.CommandId != null && query.Parameters != null && query.Parameters.Count > 0)
            {
                // query.Parameters has the parameters sent by client
                var results = new ComposeExtensionResult()
                {
                    AttachmentLayout = "list",
                    Type = "result",
                    Attachments = new List<ComposeExtensionAttachment>(),
                };
                invokeResponse.ComposeExtension = results;
            }

            // Return the response
            return Request.CreateResponse<ComposeExtensionResponse>(HttpStatusCode.OK, invokeResponse);
        } else
        {
            // Handle other types of Invoke activities here.
        }
    } else {
      // Failure case catch-all.
      var response = Request.CreateResponse(HttpStatusCode.BadRequest);
      response.Content = new StringContent("Invalid request! This API supports only messaging extension requests. Check your query and try again");
      return response;
    }
}
```

### <a name="nodejs"></a><span data-ttu-id="8a982-268">Node.js</span><span class="sxs-lookup"><span data-stu-id="8a982-268">Node.js</span></span>

<span data-ttu-id="8a982-269">[Расширения Teams](https://www.npmjs.com/package/botbuilder-teams) для пакета SDK построителя для Node. js предоставляют вспомогательные объекты и методы для упрощения приема, обработки и реагирования на запросы расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8a982-269">The [Teams extensions](https://www.npmjs.com/package/botbuilder-teams) for the Bot Builder SDK for Node.js provide helper objects and methods to simplify receiving, processing, and responding to messaging extension requests.</span></span>

#### <a name="example-code-in-nodejs"></a><span data-ttu-id="8a982-270">Пример кода в Node. js</span><span class="sxs-lookup"><span data-stu-id="8a982-270">Example code in Node.js</span></span>

```javascript
require('dotenv').config();

import * as restify from 'restify';
import * as builder from 'botbuilder';
import * as teamBuilder from 'botbuilder-teams';

class App {
    run() {
        const server = restify.createServer();
        let teamChatConnector = new teamBuilder.TeamsChatConnector({
            appId: process.env.MICROSOFT_APP_ID,
            appPassword: process.env.MICROSOFT_APP_PASSWORD
        });

        // Command ID must match what's defined in manifest
        teamChatConnector.onQuery('<%= commandId %>',
            (event: builder.IEvent,
            query: teamBuilder.ComposeExtensionQuery,
            callback: (err: Error, result: teamBuilder.IComposeExtensionResponse, statusCode: number) => void) => {
                // Check for initialRun; i.e., when you should return default results
                // if (query.parameters[0].name === 'initialRun') {}

                // Check query.queryOptions.count and query.queryOptions.skip for paging

                // Return auth response
                // let response = teamBuilder.ComposeExtensionResponse.auth().actions([
                //     builder.CardAction.openUrl(null, 'https://authUrl', 'Please sign in')
                // ]).toResponse();

                // Return config response
                // let response = teamBuilder.ComposeExtensionResponse.config().actions([
                //     builder.CardAction.openUrl(null, 'https://configUrl', 'Please sign in')
                // ]).toResponse();

                // Return result response
                let response = teamBuilder.ComposeExtensionResponse.result('list').attachments([
                    new builder.ThumbnailCard()
                        .title('Test thumbnail card')
                        .text('This is a test thumbnail card')
                        .images([new builder.CardImage().url('https://bot-framework.azureedge.net/bot-icons-v1/bot-framework-default-9.png')])
                        .toAttachment()
                ]).toResponse();
                callback(null, response, 200);
            });
        server.post('/api/composeExtension', teamChatConnector.listen());
        server.listen(process.env.PORT, () => console.log(`listening to port:` + process.env.PORT));
    }
}

const app = new App();
app.run();
```
