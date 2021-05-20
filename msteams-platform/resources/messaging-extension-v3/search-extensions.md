---
title: Поиск с расширением обмена сообщениями
description: Описывает, как разрабатывать расширения обмена сообщениями на основе поиска
keywords: команды обмена сообщениями расширения обмена сообщениями поиск
ms.topic: how-to
localization_priority: Normal
ms.date: 07/20/2019
ms.openlocfilehash: 515472838ff2ad35ef5dd295043ec27c53edb4f1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566734"
---
# <a name="search-with-messaging-extensions"></a><span data-ttu-id="9af7a-104">Поиск с расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9af7a-104">Search with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="9af7a-105">Расширение обмена сообщениями на основе поиска позволяет запрашивать вашу службу и размещать эту информацию в виде карты, прямо в ваше сообщение.</span><span class="sxs-lookup"><span data-stu-id="9af7a-105">Search based messaging extensions allow you to query your service and post that information in the form of a card, right into your message.</span></span>

![Пример карты расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="9af7a-107">Следующие разделы описывают, как это сделать:</span><span class="sxs-lookup"><span data-stu-id="9af7a-107">The following sections describe how to do this:</span></span>

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a><span data-ttu-id="9af7a-108">Расширение сообщений типа поиска</span><span class="sxs-lookup"><span data-stu-id="9af7a-108">Search type message extensions</span></span>

<span data-ttu-id="9af7a-109">Для расширения обмена сообщениями на основе поиска `type` установите параметр `query` .</span><span class="sxs-lookup"><span data-stu-id="9af7a-109">For search based messaging extension set the `type` parameter to `query`.</span></span> <span data-ttu-id="9af7a-110">Ниже приведен пример манифеста с одной командой поиска.</span><span class="sxs-lookup"><span data-stu-id="9af7a-110">Below is an example of a manifest with a single search command.</span></span> <span data-ttu-id="9af7a-111">Одно расширение обмена сообщениями может иметь до 10 различных команд, связанных с ним.</span><span class="sxs-lookup"><span data-stu-id="9af7a-111">A single messaging extension can have up to 10 different commands associated with it.</span></span> <span data-ttu-id="9af7a-112">Это может включать в себя как несколько поисковых, так и несколько команд на основе действий.</span><span class="sxs-lookup"><span data-stu-id="9af7a-112">This can include both multiple search and multiple Action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="9af7a-113">Полный пример манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="9af7a-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
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

### <a name="test-via-uploading"></a><span data-ttu-id="9af7a-114">Тест через загрузку</span><span class="sxs-lookup"><span data-stu-id="9af7a-114">Test via uploading</span></span>

<span data-ttu-id="9af7a-115">Вы можете протестировать расширение обмена сообщениями, загрузив приложение.</span><span class="sxs-lookup"><span data-stu-id="9af7a-115">You can test your messaging extension by uploading your app.</span></span>

<span data-ttu-id="9af7a-116">Чтобы открыть расширение обмена сообщениями, перейдите на любой из ваших чатов или каналов.</span><span class="sxs-lookup"><span data-stu-id="9af7a-116">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="9af7a-117">Выберите **кнопку «Больше** **&#8943;»**(подробнее) в поле для составления и выберите расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9af7a-117">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="add-event-handlers"></a><span data-ttu-id="9af7a-118">Добавление обработчиков событий</span><span class="sxs-lookup"><span data-stu-id="9af7a-118">Add event handlers</span></span>

<span data-ttu-id="9af7a-119">Большая часть вашей работы связана `onQuery` с событием, которое обрабатывает все взаимодействия в окне расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9af7a-119">Most of your work involves the `onQuery` event, which handles all interactions in the messaging extension window.</span></span>

<span data-ttu-id="9af7a-120">Если вы `canUpdateConfiguration` `true` устанавливаете в манифесте, вы включаете **элемент Параметры** меню для расширения обмена сообщениями, а также должны обрабатывать `onQuerySettingsUrl` и `onSettingsUpdate` .</span><span class="sxs-lookup"><span data-stu-id="9af7a-120">If you set `canUpdateConfiguration` to `true` in the manifest, you enable the **Settings** menu item for your messaging extension and must also handle `onQuerySettingsUrl` and `onSettingsUpdate`.</span></span>

### <a name="handle-onquery-events"></a><span data-ttu-id="9af7a-121">Ручка на событиях Квери</span><span class="sxs-lookup"><span data-stu-id="9af7a-121">Handle onQuery events</span></span>

<span data-ttu-id="9af7a-122">Расширение обмена сообщениями получает `onQuery` событие, когда что-либо происходит в окне расширения обмена сообщениями или отправляется в окно.</span><span class="sxs-lookup"><span data-stu-id="9af7a-122">A messaging extension receives an `onQuery` event when anything happens in the messaging extension window or is sent to the window.</span></span>

<span data-ttu-id="9af7a-123">Если расширение обмена сообщениями использует страницу конфигурации, обработчик должен сначала проверить `onQuery` любую сохраненную информацию о конфигурации; если расширение обмена сообщениями не настроено, `config` верните ответ со ссылкой на страницу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9af7a-123">If your messaging extension uses a configuration page, your handler for `onQuery` should first check for any stored configuration information; if the messaging extension isn't configured, return a `config` response with a link to your configuration page.</span></span> <span data-ttu-id="9af7a-124">Имейте в виду, что ответ со страницы конфигурации также обрабатывается `onQuery` .</span><span class="sxs-lookup"><span data-stu-id="9af7a-124">Be aware that the response from the configuration page is also handled by `onQuery`.</span></span> <span data-ttu-id="9af7a-125">Единственным исключением является, когда страница конфигурации вызывается обработчиком `onQuerySettingsUrl` для; см. следующий раздел:</span><span class="sxs-lookup"><span data-stu-id="9af7a-125">The sole exception is when the configuration page is called by the handler for `onQuerySettingsUrl`; see the following section:</span></span>

<span data-ttu-id="9af7a-126">Если расширение обмена сообщениями требует проверки подлинности, проверьте информацию о состоянии пользователя; если пользователь не ввеся, следуйте инструкциям в разделе [Аутентификация](#authentication) позже в этой теме.</span><span class="sxs-lookup"><span data-stu-id="9af7a-126">If your messaging extension requires authentication, check the user state information; if the user isn't signed in, follow the instructions in the [Authentication](#authentication) section later in this topic.</span></span>

<span data-ttu-id="9af7a-127">Далее проверьте, `initialRun` установлен ли набор; если да, то принять соответствующие меры, такие как предоставление инструкций или список ответов.</span><span class="sxs-lookup"><span data-stu-id="9af7a-127">Next, check whether `initialRun` is set; if so, take appropriate action, such as providing instructions or a list of responses.</span></span>

<span data-ttu-id="9af7a-128">Остальная часть обработчика `onQuery` для запросов пользователя к информации, отображает список карт предварительного просмотра и возвращает карту, выбранную пользователем.</span><span class="sxs-lookup"><span data-stu-id="9af7a-128">The remainder of your handler for `onQuery` prompts the user for information, displays a list of preview cards, and returns the card selected by the user.</span></span>

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a><span data-ttu-id="9af7a-129">Ручка на событиях КвериSettingsUrl и onSettingsUpdate</span><span class="sxs-lookup"><span data-stu-id="9af7a-129">Handle onQuerySettingsUrl and onSettingsUpdate events</span></span>

<span data-ttu-id="9af7a-130">События `onQuerySettingsUrl` и `onSettingsUpdate` события работают вместе, чтобы **Параметры пункт** меню.</span><span class="sxs-lookup"><span data-stu-id="9af7a-130">The `onQuerySettingsUrl` and `onSettingsUpdate` events work together to enable the **Settings** menu item.</span></span>

![Скриншоты местонахождения Параметры пункта меню](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

<span data-ttu-id="9af7a-132">Обработчик возвращает `onQuerySettingsUrl` URL для страницы конфигурации; после закрытия страницы конфигурации обработчик принимает и сохраняет `onSettingsUpdate` возвращенный состояние.</span><span class="sxs-lookup"><span data-stu-id="9af7a-132">Your handler for `onQuerySettingsUrl` returns the URL for the configuration page; after the configuration page closes, your handler for `onSettingsUpdate` accepts and saves the returned state.</span></span> <span data-ttu-id="9af7a-133">Это тот случай, когда `onQuery` *не получает* ответа со страницы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9af7a-133">This is the one case in which `onQuery` *doesn't* receive the response from the configuration page.</span></span>

## <a name="receive-and-respond-to-queries"></a><span data-ttu-id="9af7a-134">Получать и отвечать на запросы</span><span class="sxs-lookup"><span data-stu-id="9af7a-134">Receive and respond to queries</span></span>

<span data-ttu-id="9af7a-135">Каждый запрос на расширение обмена сообщениями делается через `Activity` объект, который размещен на ваш URL-адрес обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="9af7a-135">Every request to your messaging extension is done via an `Activity` object that is posted to your callback URL.</span></span> <span data-ttu-id="9af7a-136">Запрос содержит информацию о команде пользователя, такую как значения идентификатора и параметра.</span><span class="sxs-lookup"><span data-stu-id="9af7a-136">The request contains information about the user command, such as ID and parameter values.</span></span> <span data-ttu-id="9af7a-137">Запрос также поставляет метаданные о контексте, в котором было вызвано ваше расширение, включая идентификатор пользователя и арендатора, а также идентификатор чата или идентификаторы чата или канала и команды.</span><span class="sxs-lookup"><span data-stu-id="9af7a-137">The request also supplies metadata about the context in which your extension was invoked, including user and tenant ID, along with chat ID or channel and team IDs.</span></span>

### <a name="receive-user-requests"></a><span data-ttu-id="9af7a-138">Получение запросов пользователей</span><span class="sxs-lookup"><span data-stu-id="9af7a-138">Receive user requests</span></span>

<span data-ttu-id="9af7a-139">Когда пользователь выполняет запрос, Microsoft Teams отправляет вашу службу стандартному объекту Bot `Activity` Framework.</span><span class="sxs-lookup"><span data-stu-id="9af7a-139">When a user performs a query, Microsoft Teams sends your service a standard Bot Framework `Activity` object.</span></span> <span data-ttu-id="9af7a-140">Служба должна выполнять свою логику для набора `Activity` и `type` настройки `invoke` `name` поддерживаемого `composeExtension` типа, как показано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="9af7a-140">Your service should perform its logic for an `Activity` that has `type` set to `invoke` and `name` set to a supported `composeExtension` type, as shown in the following table.</span></span>

<span data-ttu-id="9af7a-141">В дополнение к стандартным свойствам активности бота, полезная нагрузка содержит следующие метаданные запроса:</span><span class="sxs-lookup"><span data-stu-id="9af7a-141">In addition to the standard bot activity properties, the payload contains the following request metadata:</span></span>

|<span data-ttu-id="9af7a-142">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="9af7a-142">Property name</span></span>|<span data-ttu-id="9af7a-143">Назначение</span><span class="sxs-lookup"><span data-stu-id="9af7a-143">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="9af7a-144">Тип запроса; должно быть `invoke` .</span><span class="sxs-lookup"><span data-stu-id="9af7a-144">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="9af7a-145">Тип команды, которая выдается службе.</span><span class="sxs-lookup"><span data-stu-id="9af7a-145">Type of command that is issued to your service.</span></span> <span data-ttu-id="9af7a-146">В настоящее время поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="9af7a-146">Currently the following types are supported:</span></span> <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| <span data-ttu-id="9af7a-147">Идентификатор пользователя, который отправил запрос.</span><span class="sxs-lookup"><span data-stu-id="9af7a-147">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="9af7a-148">Имя пользователя, отправленное запросом.</span><span class="sxs-lookup"><span data-stu-id="9af7a-148">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="9af7a-149">Azure Active Directory идентификатор пользователя, который отправил запрос.</span><span class="sxs-lookup"><span data-stu-id="9af7a-149">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="9af7a-150">Идентификатор клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9af7a-150">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="9af7a-151">Идентификатор канала (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="9af7a-151">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="9af7a-152">Идентификатор команды (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="9af7a-152">Team ID (if the request was made in a channel).</span></span> |
|`clientInfo`|<span data-ttu-id="9af7a-153">Дополнительные метаданные о клиентском программном обеспечении, используемом для отправки сообщения пользователя.</span><span class="sxs-lookup"><span data-stu-id="9af7a-153">Optional metadata about the client software used to send a user's message.</span></span> <span data-ttu-id="9af7a-154">Сущность может содержать два свойства:</span><span class="sxs-lookup"><span data-stu-id="9af7a-154">The entity can contain two properties:</span></span><br><span data-ttu-id="9af7a-155">`country`Поле содержит обнаруженное местоположение пользователя.</span><span class="sxs-lookup"><span data-stu-id="9af7a-155">The `country` field contains the user's detected location.</span></span><br><span data-ttu-id="9af7a-156">Поле `platform` описывает клиентскую платформу обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9af7a-156">The `platform` field describes the messaging client platform.</span></span> <br><span data-ttu-id="9af7a-157">Для получения дополнительной информации, *пожалуйста,* [смотрите типы не-IRI entity - clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span><span class="sxs-lookup"><span data-stu-id="9af7a-157">For additional information, please *see* [Non-IRI entity types — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>|

<span data-ttu-id="9af7a-158">Параметры запроса сами по себе находятся в объекте значения, который включает в себя следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="9af7a-158">The request parameters itself are found in the value object, which includes the following properties:</span></span>

| <span data-ttu-id="9af7a-159">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="9af7a-159">Property name</span></span> | <span data-ttu-id="9af7a-160">Назначение</span><span class="sxs-lookup"><span data-stu-id="9af7a-160">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="9af7a-161">Имя команды, вызываемой пользователем, соответствующее одной из команд, заявленных в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="9af7a-161">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="9af7a-162">Массив параметров: Каждый объект параметра содержит имя параметра, а также значение параметра, предоставляемое пользователем.</span><span class="sxs-lookup"><span data-stu-id="9af7a-162">Array of parameters: Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="9af7a-163">Параметры пагинации:</span><span class="sxs-lookup"><span data-stu-id="9af7a-163">Pagination parameters:</span></span> <br><span data-ttu-id="9af7a-164">`skip`: пропустить подсчет для этого запроса</span><span class="sxs-lookup"><span data-stu-id="9af7a-164">`skip`: skip count for this query</span></span> <br><span data-ttu-id="9af7a-165">`count`: количество элементов для возврата</span><span class="sxs-lookup"><span data-stu-id="9af7a-165">`count`: number of elements to return</span></span> |

#### <a name="request-example"></a><span data-ttu-id="9af7a-166">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="9af7a-166">Request example</span></span>

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
    "type": "clientInfo",
      "country": "US",
      "platform": "Windows"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a><span data-ttu-id="9af7a-167">Получение запросов от ссылок, вставленных в поле сообщений compose</span><span class="sxs-lookup"><span data-stu-id="9af7a-167">Receive requests from links inserted into the compose message box</span></span>

<span data-ttu-id="9af7a-168">В качестве альтернативы (или в дополнение) к поиску внешнего сервиса, вы можете использовать URL-адрес, вставленный в поле для составления сообщений, чтобы запросить услугу и вернуть карту.</span><span class="sxs-lookup"><span data-stu-id="9af7a-168">As an alternative (or in addition) to searching your external service, you can use a URL inserted into the compose message box to query your service and return a card.</span></span> <span data-ttu-id="9af7a-169">На скриншоте ниже пользователь вставить в URL для рабочего элемента в Azure DevOps который расширение обмена сообщениями решил в карту.</span><span class="sxs-lookup"><span data-stu-id="9af7a-169">In the screenshot below a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Пример разворачивания ссылки](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

<span data-ttu-id="9af7a-171">Чтобы расширение обмена сообщениями взаимодействовать со ссылками таким образом, сначала необходимо добавить массив в `messageHandlers` манифест приложения, как в приведенной ниже примере:</span><span class="sxs-lookup"><span data-stu-id="9af7a-171">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below:</span></span>

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

<span data-ttu-id="9af7a-172">После того как вы добавили домен для прослушивания манифеста приложения, вам нужно изменить код бота, чтобы [ответить на](#respond-to-user-requests) нижеувленный запрос вызова.</span><span class="sxs-lookup"><span data-stu-id="9af7a-172">Once you've added the domain to listen on to the app manifest, you'll need to change your bot code to [respond](#respond-to-user-requests) to the below invoke request.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="9af7a-173">Если приложение возвращает несколько элементов, будет использован только первый.</span><span class="sxs-lookup"><span data-stu-id="9af7a-173">If your app returns multiple items only the first will be used.</span></span>

### <a name="respond-to-user-requests"></a><span data-ttu-id="9af7a-174">Отвечайте на запросы пользователей</span><span class="sxs-lookup"><span data-stu-id="9af7a-174">Respond to user requests</span></span>

<span data-ttu-id="9af7a-175">Когда пользователь выполняет запрос, Microsoft Teams выдает синхронный запрос HTTP в службу.</span><span class="sxs-lookup"><span data-stu-id="9af7a-175">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="9af7a-176">На этом этапе у кода есть 5 секунд, чтобы дать ответ на запрос HTTP.</span><span class="sxs-lookup"><span data-stu-id="9af7a-176">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="9af7a-177">За это время служба может выполнить дополнительный осмотр или любую другую бизнес-логику, необходимую для обслуживания запроса.</span><span class="sxs-lookup"><span data-stu-id="9af7a-177">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="9af7a-178">Служба должна отвечать результатами, соответствующими запросу пользователя.</span><span class="sxs-lookup"><span data-stu-id="9af7a-178">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="9af7a-179">В ответе должен быть указан код статуса HTTP `200 OK` и действительный объект приложения/json со следующим органом:</span><span class="sxs-lookup"><span data-stu-id="9af7a-179">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="9af7a-180">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="9af7a-180">Property name</span></span>|<span data-ttu-id="9af7a-181">Назначение</span><span class="sxs-lookup"><span data-stu-id="9af7a-181">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="9af7a-182">Конверт ответа верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="9af7a-182">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="9af7a-183">Тип ответа.</span><span class="sxs-lookup"><span data-stu-id="9af7a-183">Type of response.</span></span> <span data-ttu-id="9af7a-184">Поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="9af7a-184">The following types are supported:</span></span> <br><span data-ttu-id="9af7a-185">`result`: отображает список результатов поиска</span><span class="sxs-lookup"><span data-stu-id="9af7a-185">`result`: displays a list of search results</span></span> <br><span data-ttu-id="9af7a-186">`auth`: просит пользователя проверить подлинность</span><span class="sxs-lookup"><span data-stu-id="9af7a-186">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="9af7a-187">`config`: просит пользователя настроить расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9af7a-187">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="9af7a-188">`message`: показывает обычное текстовое сообщение</span><span class="sxs-lookup"><span data-stu-id="9af7a-188">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="9af7a-189">Определяет расположение вложений.</span><span class="sxs-lookup"><span data-stu-id="9af7a-189">Specifies the layout of the attachments.</span></span> <span data-ttu-id="9af7a-190">Используется для ответов типа `result` .</span><span class="sxs-lookup"><span data-stu-id="9af7a-190">Used for responses of type `result`.</span></span> <br><span data-ttu-id="9af7a-191">В настоящее время поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="9af7a-191">Currently the following types are supported:</span></span> <br><span data-ttu-id="9af7a-192">`list`: список карточных объектов, содержащих эскизы, заголовки и текстовые поля</span><span class="sxs-lookup"><span data-stu-id="9af7a-192">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="9af7a-193">`grid`: сетка эскизных изображений</span><span class="sxs-lookup"><span data-stu-id="9af7a-193">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="9af7a-194">Массив действительных объектов вложений.</span><span class="sxs-lookup"><span data-stu-id="9af7a-194">Array of valid attachment objects.</span></span> <span data-ttu-id="9af7a-195">Используется для ответов типа `result` .</span><span class="sxs-lookup"><span data-stu-id="9af7a-195">Used for responses of type `result`.</span></span> <br><span data-ttu-id="9af7a-196">В настоящее время поддерживаются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="9af7a-196">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="9af7a-197">Предлагаемые действия.</span><span class="sxs-lookup"><span data-stu-id="9af7a-197">Suggested actions.</span></span> <span data-ttu-id="9af7a-198">Используется для ответов типа `auth` или `config` .</span><span class="sxs-lookup"><span data-stu-id="9af7a-198">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="9af7a-199">Сообщение для отображения.</span><span class="sxs-lookup"><span data-stu-id="9af7a-199">Message to display.</span></span> <span data-ttu-id="9af7a-200">Используется для ответов типа `message` .</span><span class="sxs-lookup"><span data-stu-id="9af7a-200">Used for responses of type `message`.</span></span> |

#### <a name="response-card-types-and-previews"></a><span data-ttu-id="9af7a-201">Типы карт реагирования и предварительные просмотры</span><span class="sxs-lookup"><span data-stu-id="9af7a-201">Response card types and previews</span></span>

<span data-ttu-id="9af7a-202">Мы поддерживаем следующие типы вложений:</span><span class="sxs-lookup"><span data-stu-id="9af7a-202">We support the following attachment types:</span></span>

* [<span data-ttu-id="9af7a-203">Thumbnail карты</span><span class="sxs-lookup"><span data-stu-id="9af7a-203">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="9af7a-204">Карта героя</span><span class="sxs-lookup"><span data-stu-id="9af7a-204">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="9af7a-205">Office 365 Коннекторная карта</span><span class="sxs-lookup"><span data-stu-id="9af7a-205">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="9af7a-206">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="9af7a-206">Adaptive card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="9af7a-207">Для получения дополнительной информации [см.](~/task-modules-and-cards/what-are-cards.md)</span><span class="sxs-lookup"><span data-stu-id="9af7a-207">For more information, see [Cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="9af7a-208">Чтобы узнать, как использовать эскизы и типы карт героя, [см.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="9af7a-208">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="9af7a-209">Дополнительную документацию, касающуюся Office 365 Connector, [можно Office 365 карт Connector.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="9af7a-209">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="9af7a-210">Список результатов отображается в пользовательском интерфейсе Microsoft Teams с предварительным просмотром каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="9af7a-210">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="9af7a-211">Предварительный просмотр генерируется одним из двух способов:</span><span class="sxs-lookup"><span data-stu-id="9af7a-211">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="9af7a-212">Использование `preview` свойства внутри `attachment` объекта.</span><span class="sxs-lookup"><span data-stu-id="9af7a-212">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="9af7a-213">Вложение `preview` может быть только герой или Thumbnail карты.</span><span class="sxs-lookup"><span data-stu-id="9af7a-213">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="9af7a-214">Извлечено из `title` `text` основных, `image` и свойства крепления.</span><span class="sxs-lookup"><span data-stu-id="9af7a-214">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="9af7a-215">Они используются только в том `preview` случае, если свойство не установлено и эти свойства доступны.</span><span class="sxs-lookup"><span data-stu-id="9af7a-215">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="9af7a-216">Вы можете отобразить предварительный просмотр адаптивной или Office 365 Connector в списке результатов, просто установив его свойство предварительного просмотра; это не обязательно, если результаты уже герой или эскиз карты.</span><span class="sxs-lookup"><span data-stu-id="9af7a-216">You can display a preview of an Adaptive or Office 365 Connector card in the result list simply by setting its preview property; this is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="9af7a-217">Если вы используете вложение предварительного просмотра, это должна быть либо карта Героя, либо Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="9af7a-217">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="9af7a-218">Если не указано свойство предварительного просмотра, предварительный просмотр карты потерпит неудачу и ничего не будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="9af7a-218">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

#### <a name="response-example"></a><span data-ttu-id="9af7a-219">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="9af7a-219">Response example</span></span>

<span data-ttu-id="9af7a-220">Этот пример показывает ответ с двумя результатами, смешивая различные форматы карт: Office 365 Connector и Adaptive.</span><span class="sxs-lookup"><span data-stu-id="9af7a-220">This example shows a response with two results, mixing different card formats: Office 365 Connector and Adaptive.</span></span> <span data-ttu-id="9af7a-221">Хотя вы, вероятно, захотите придерживаться формата одной карты в своем ответе, он показывает, `preview` как свойство каждого элемента в коллекции должно четко определить `attachments` предварительный просмотр в формате героя или эскиза, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="9af7a-221">While you'll likely want to stick with one card format in your response, it shows how the `preview` property of each element in the `attachments` collection must explicitly define a preview in hero or thumbnail format as described above.</span></span>

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
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
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

### <a name="default-query"></a><span data-ttu-id="9af7a-222">Запрос по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9af7a-222">Default query</span></span>

<span data-ttu-id="9af7a-223">Если вы `initialRun` устанавливаете `true` в манифесте, Microsoft Teams выдает "по умолчанию" запрос, когда пользователь впервые открывает расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9af7a-223">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="9af7a-224">Служба может ответить на этот запрос набором заранее заселенных результатов.</span><span class="sxs-lookup"><span data-stu-id="9af7a-224">Your service can respond to this query with a set of prepopulated results.</span></span> <span data-ttu-id="9af7a-225">Это может быть полезно для отображения, например, недавно просмотренных элементов, избранных или любой другой информации, которая не зависит от пользовательского ввода.</span><span class="sxs-lookup"><span data-stu-id="9af7a-225">This can be useful for displaying, for instance, recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="9af7a-226">Запрос по умолчанию имеет ту же структуру, что и любой обычный запрос пользователя, за исключением `initialRun` параметра, значение строки `true` которого.</span><span class="sxs-lookup"><span data-stu-id="9af7a-226">The default query has the same structure as any regular user query, except with a parameter `initialRun` whose string value is `true`.</span></span>

#### <a name="request-example-for-a-default-query"></a><span data-ttu-id="9af7a-227">Запрос примера запроса по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9af7a-227">Request example for a default query</span></span>

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

## <a name="identify-the-user"></a><span data-ttu-id="9af7a-228">Идентификация пользователя</span><span class="sxs-lookup"><span data-stu-id="9af7a-228">Identify the user</span></span>

<span data-ttu-id="9af7a-229">Каждый запрос на ваши службы включает в себя запутанное удостоверение пользователя, выдвив которое выполнило запрос, а также имя дисплея пользователя и идентификатор Azure Active Directory объекта.</span><span class="sxs-lookup"><span data-stu-id="9af7a-229">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="9af7a-230">Значения `id` `aadObjectId` и значения гарантированно являются ценностями аутентифицированного Teams пользователя.</span><span class="sxs-lookup"><span data-stu-id="9af7a-230">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="9af7a-231">Они могут быть использованы в качестве ключей для выглядеть учетные данные или любое кэшированные состояния в вашем сервисе.</span><span class="sxs-lookup"><span data-stu-id="9af7a-231">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="9af7a-232">Кроме того, каждый запрос содержит Azure Active Directory идентификатор пользователя, который может быть использован для идентификации организации пользователя.</span><span class="sxs-lookup"><span data-stu-id="9af7a-232">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="9af7a-233">Если это применимо, запрос также содержит ID команды и канала, из которых возник запрос.</span><span class="sxs-lookup"><span data-stu-id="9af7a-233">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="9af7a-234">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="9af7a-234">Authentication</span></span>

<span data-ttu-id="9af7a-235">Если ваша служба требует проверки подлинности пользователя, необходимо войти в систему пользователя, прежде чем он или она смогла использовать расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9af7a-235">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="9af7a-236">Если вы написали бота или вкладку, которая подписывается на пользователя, этот раздел должен быть знаком.</span><span class="sxs-lookup"><span data-stu-id="9af7a-236">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="9af7a-237">Последовательность заключается в следующем:</span><span class="sxs-lookup"><span data-stu-id="9af7a-237">The sequence is as follows:</span></span>

1. <span data-ttu-id="9af7a-238">Пользователь выдает запрос, или запрос по умолчанию автоматически отправляется в службу.</span><span class="sxs-lookup"><span data-stu-id="9af7a-238">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="9af7a-239">Служба проверяет, проверил ли пользователь сначала подлинность, проверив Teams идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="9af7a-239">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="9af7a-240">Если пользователь не подтвердил подлинность, отправьте ответ с предлагаемым `auth` `openUrl` действием, включая URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9af7a-240">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="9af7a-241">Клиент Microsoft Teams всплывающее окно, на хостинге веб-страницы, используя данный URL-адрес аутентификации.</span><span class="sxs-lookup"><span data-stu-id="9af7a-241">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="9af7a-242">После того, как пользователь войтыт, вы должны закрыть окно и отправить "код аутентификации" Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="9af7a-242">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="9af7a-243">Затем Teams переоформляет запрос на ваш сервис, который включает код проверки подлинности, пройденный в шаге 5.</span><span class="sxs-lookup"><span data-stu-id="9af7a-243">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="9af7a-244">Служба должна убедиться, что код проверки подлинности, полученный в шаге 6, совпадает с кодом шага 5.</span><span class="sxs-lookup"><span data-stu-id="9af7a-244">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="9af7a-245">Это гарантирует, что злоумышленник не пытается подделать или скомпрометировать поток ва-банк.</span><span class="sxs-lookup"><span data-stu-id="9af7a-245">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="9af7a-246">Это фактически "закрывает цикл", чтобы закончить безопасную последовательность проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9af7a-246">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="9af7a-247">Ответить с ва-воють</span><span class="sxs-lookup"><span data-stu-id="9af7a-247">Respond with a sign-in action</span></span>

<span data-ttu-id="9af7a-248">Чтобы побудить неодохновленного пользователя войти в систему, ответьте предложенным действием типа, `openUrl` которое включает URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9af7a-248">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="9af7a-249">Пример ответа для действия в действии</span><span class="sxs-lookup"><span data-stu-id="9af7a-249">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="9af7a-250">Для того, чтобы во всплывающем компьютере Teams, доменная часть URL-адреса должна быть в списке действительных доменов вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="9af7a-250">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="9af7a-251">Для получения дополнительной информации [см.](~/resources/schema/manifest-schema.md#validdomains)</span><span class="sxs-lookup"><span data-stu-id="9af7a-251">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="9af7a-252">Запуск потока ва-в</span><span class="sxs-lookup"><span data-stu-id="9af7a-252">Start the sign-in flow</span></span>

<span data-ttu-id="9af7a-253">Ваш опыт регистрации должен быть отзывчивым и вписываться в всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="9af7a-253">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="9af7a-254">Он должен интегрироваться с [Microsoft Teams JavaScript SDK](/javascript/api/overview/msteams-client), который использует передачу сообщений.</span><span class="sxs-lookup"><span data-stu-id="9af7a-254">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="9af7a-255">Как и в случае с другими встроенными Microsoft Teams, код внутри окна должен быть первым `microsoftTeams.initialize()` вызовом.</span><span class="sxs-lookup"><span data-stu-id="9af7a-255">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="9af7a-256">Если ваш код выполняет поток OAuth, вы можете передать идентификатор пользователя Teams в окно, который затем может передать его на URL-адрес регистрации OAuth.</span><span class="sxs-lookup"><span data-stu-id="9af7a-256">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="9af7a-257">Завершите поток ва-вв</span><span class="sxs-lookup"><span data-stu-id="9af7a-257">Complete the sign-in flow</span></span>

<span data-ttu-id="9af7a-258">Когда запрос на регистрацию завершается и перенаправляется обратно на страницу, он должен выполнить следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9af7a-258">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="9af7a-259">Создание кода безопасности.</span><span class="sxs-lookup"><span data-stu-id="9af7a-259">Generate a security code.</span></span> <span data-ttu-id="9af7a-260">(Это может быть случайное число.) Вам необходимо кэшировать этот код на службе, а также учетные данные, полученные через поток входа, такие как токены OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="9af7a-260">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow such as, OAuth 2.0 tokens.</span></span>
2. <span data-ttu-id="9af7a-261">Звоните `microsoftTeams.authentication.notifySuccess` и перевезье кода безопасности.</span><span class="sxs-lookup"><span data-stu-id="9af7a-261">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="9af7a-262">В этот момент окно закрывается и управление передается Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="9af7a-262">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="9af7a-263">Клиент теперь может переиздать исходный пользовательский запрос вместе с кодом безопасности в `state` свойстве.</span><span class="sxs-lookup"><span data-stu-id="9af7a-263">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="9af7a-264">Код может использовать код безопасности для проверки учетных данных, хранящихся ранее, для завершения последовательности проверки подлинности, а затем для выполнения запроса пользователя.</span><span class="sxs-lookup"><span data-stu-id="9af7a-264">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="9af7a-265">Пример переизданного запроса</span><span class="sxs-lookup"><span data-stu-id="9af7a-265">Reissued request example</span></span>

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
        "type": "clientInfo",
        "country": "US",
        "platform": "Web",
        
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

## <a name="sdk-support"></a><span data-ttu-id="9af7a-266">Поддержка SDK</span><span class="sxs-lookup"><span data-stu-id="9af7a-266">SDK support</span></span>

### <a name="net"></a><span data-ttu-id="9af7a-267">.NET</span><span class="sxs-lookup"><span data-stu-id="9af7a-267">.NET</span></span>

<span data-ttu-id="9af7a-268">Для получения и обработки запросов с Bot Builder SDK для .NET, вы можете проверить тип `invoke` действия на входящий деятельности, а затем использовать метод помощников в пакете NuGet [Microsoft.Bot.Connector.Teams,](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) чтобы определить, является ли это расширение деятельности обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9af7a-268">To receive and handle queries with the Bot Builder SDK for .NET, you can check for the `invoke` action type on the incoming activity and then use the helper method in the NuGet package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) to determine whether it’s a messaging extension activity.</span></span>

#### <a name="example-code-in-net"></a><span data-ttu-id="9af7a-269">Пример кода в .NET</span><span class="sxs-lookup"><span data-stu-id="9af7a-269">Example code in .NET</span></span>

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

### <a name="nodejs"></a><span data-ttu-id="9af7a-270">Node.js</span><span class="sxs-lookup"><span data-stu-id="9af7a-270">Node.js</span></span>

#### <a name="example-code-in-nodejs"></a><span data-ttu-id="9af7a-271">Пример кода в Node.js</span><span class="sxs-lookup"><span data-stu-id="9af7a-271">Example code in Node.js</span></span>

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

## <a name="see-also"></a><span data-ttu-id="9af7a-272">См. также</span><span class="sxs-lookup"><span data-stu-id="9af7a-272">See also</span></span>

<span data-ttu-id="9af7a-273">[Образцы Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="9af7a-273">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
