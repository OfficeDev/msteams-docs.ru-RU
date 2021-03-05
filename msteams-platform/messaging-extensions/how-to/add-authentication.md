---
title: Добавление проверки подлинности в расширение обмена сообщениями
author: clearab
description: Добавление проверки подлинности в расширение обмена сообщениями
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: d673f52e63ba845675f6631470af68d65c7297ad
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449572"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="7f50d-103">Добавление проверки подлинности в расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="7f50d-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="7f50d-104">Определение пользователя</span><span class="sxs-lookup"><span data-stu-id="7f50d-104">Identify the user</span></span>

<span data-ttu-id="7f50d-105">Каждый запрос к вашим службам включает запутываный ID пользователя, который выполнил запрос, а также имя отображения пользователя и объектный ИД Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7f50d-105">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="7f50d-106">Значения `id` `aadObjectId` и значения гарантируются пользователю teams с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="7f50d-106">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="7f50d-107">Они могут использоваться в качестве ключей для иска учетных данных или любого кэшного состояния в службе.</span><span class="sxs-lookup"><span data-stu-id="7f50d-107">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="7f50d-108">Кроме того, каждый запрос содержит ID клиента Azure Active Directory пользователя, который можно использовать для идентификации организации пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f50d-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="7f50d-109">Если это применимо, запрос также содержит командные и канальные ИД, из которых был зародился запрос.</span><span class="sxs-lookup"><span data-stu-id="7f50d-109">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="7f50d-110">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="7f50d-110">Authentication</span></span>

<span data-ttu-id="7f50d-111">Если ваша служба требует проверки подлинности пользователя, необходимо войти в пользователя, прежде чем он сможет использовать расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="7f50d-111">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="7f50d-112">Если вы написали бот или вкладку, которая подписывает пользователя, этот раздел должен быть знаком.</span><span class="sxs-lookup"><span data-stu-id="7f50d-112">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="7f50d-113">Последовательность будет следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7f50d-113">The sequence is as follows:</span></span>

1. <span data-ttu-id="7f50d-114">Пользователь выдает запрос, или запрос по умолчанию автоматически отправляется в службу.</span><span class="sxs-lookup"><span data-stu-id="7f50d-114">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="7f50d-115">Служба проверяет, был ли пользователь впервые проверен на подлинность, проверив идентификацию пользователя Teams.</span><span class="sxs-lookup"><span data-stu-id="7f50d-115">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="7f50d-116">Если пользователь не сдал проверку подлинности, отправьте ответ с предложенным действием, включая `auth` `openUrl` URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7f50d-116">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="7f50d-117">Клиент Microsoft Teams запускает всплывающее окно с размещением веб-страницы с помощью данного URL-адреса проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7f50d-117">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="7f50d-118">После того как пользователь войдет, необходимо закрыть окно и отправить клиенту Teams "код проверки подлинности".</span><span class="sxs-lookup"><span data-stu-id="7f50d-118">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="7f50d-119">Затем клиент Teams переиздает запрос в службу, которая включает код проверки подлинности, переданный в шаге 5.</span><span class="sxs-lookup"><span data-stu-id="7f50d-119">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="7f50d-120">Служба должна убедиться, что код проверки подлинности, полученный на шаге 6, соответствует коду из шага 5.</span><span class="sxs-lookup"><span data-stu-id="7f50d-120">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="7f50d-121">Это гарантирует, что вредоносный пользователь не пытается подменить или скомпрометировать поток входных данных.</span><span class="sxs-lookup"><span data-stu-id="7f50d-121">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="7f50d-122">Это эффективно "закрывает цикл", чтобы завершить безопасную последовательность проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7f50d-122">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="7f50d-123">Ответ с помощью действия для регистрации</span><span class="sxs-lookup"><span data-stu-id="7f50d-123">Respond with a sign-in action</span></span>

<span data-ttu-id="7f50d-124">Чтобы подсказывать неавентированному пользователю войти, ответьте предложенным действием типа, которое включает URL-адрес проверки `openUrl` подлинности.</span><span class="sxs-lookup"><span data-stu-id="7f50d-124">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="7f50d-125">Пример ответа для действия входного знака</span><span class="sxs-lookup"><span data-stu-id="7f50d-125">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="7f50d-126">Чтобы возможность регистрации была организована в всплывающее всплывающее приложение Teams, доменная часть URL-адреса должна быть в списке допустимого домена вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7f50d-126">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="7f50d-127">[(См. validDomains](~/resources/schema/manifest-schema.md#validdomains) в схеме манифеста.)</span><span class="sxs-lookup"><span data-stu-id="7f50d-127">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="7f50d-128">Запуск потока входов</span><span class="sxs-lookup"><span data-stu-id="7f50d-128">Start the sign-in flow</span></span>

<span data-ttu-id="7f50d-129">Ваш опыт регистрации должен быть отзывчивым и соответствовать в окне всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="7f50d-129">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="7f50d-130">Он должен интегрироваться с [клиентом Microsoft Teams JavaScript SDK,](/javascript/api/overview/msteams-client)который использует передачу сообщений.</span><span class="sxs-lookup"><span data-stu-id="7f50d-130">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="7f50d-131">Как и в других встроенных опытом, запущенных в Microsoft Teams, коду в окне необходимо сначала вызвать `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="7f50d-131">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="7f50d-132">Если код выполняет поток OAuth, вы можете передать код пользователя Teams в окно, который затем может передать его URL-адресу для регистрации OAuth.</span><span class="sxs-lookup"><span data-stu-id="7f50d-132">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="7f50d-133">Завершение потока входов</span><span class="sxs-lookup"><span data-stu-id="7f50d-133">Complete the sign-in flow</span></span>

<span data-ttu-id="7f50d-134">Когда запрос на вход завершается и перенаправляется обратно на страницу, он должен выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7f50d-134">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="7f50d-135">Создание кода безопасности.</span><span class="sxs-lookup"><span data-stu-id="7f50d-135">Generate a security code.</span></span> <span data-ttu-id="7f50d-136">(Это может быть случайное число.) Этот код необходимо кэшировать в службе вместе с учетными данными, полученными в потоке входа (например, маркерами OAuth 2.0).</span><span class="sxs-lookup"><span data-stu-id="7f50d-136">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="7f50d-137">Вызов `microsoftTeams.authentication.notifySuccess` и пропуск кода безопасности.</span><span class="sxs-lookup"><span data-stu-id="7f50d-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="7f50d-138">На этом этапе окно закрывается и управление передается клиенту Teams.</span><span class="sxs-lookup"><span data-stu-id="7f50d-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="7f50d-139">Теперь клиент может переопросить исходный запрос пользователя вместе с кодом безопасности в `state` свойстве.</span><span class="sxs-lookup"><span data-stu-id="7f50d-139">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="7f50d-140">Код безопасности может использовать код безопасности для проверки учетных данных, хранимых ранее, для завершения последовательности проверки подлинности и выполнения запроса пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f50d-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="7f50d-141">Пример повторного запроса</span><span class="sxs-lookup"><span data-stu-id="7f50d-141">Reissued request example</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="7f50d-142">Пример кода</span><span class="sxs-lookup"><span data-stu-id="7f50d-142">Code sample</span></span>
|<span data-ttu-id="7f50d-143">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="7f50d-143">**Sample name**</span></span> | <span data-ttu-id="7f50d-144">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7f50d-144">**Description**</span></span> |<span data-ttu-id="7f50d-145">**.NET**</span><span class="sxs-lookup"><span data-stu-id="7f50d-145">**.NET**</span></span> | <span data-ttu-id="7f50d-146">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="7f50d-146">**Node.js**</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="7f50d-147">Расширения обмена сообщениями — auth и config</span><span class="sxs-lookup"><span data-stu-id="7f50d-147">Messaging extensions - auth and config</span></span> | <span data-ttu-id="7f50d-148">Расширение обмена сообщениями, которое имеет страницу конфигурации, принимает запросы на поиск и возвращает результаты после того, как пользователь войт.</span><span class="sxs-lookup"><span data-stu-id="7f50d-148">A Messaging Extension that has a configuration page, accepts search requests, and returns results after the user has signed in.</span></span> |[<span data-ttu-id="7f50d-149">View</span><span class="sxs-lookup"><span data-stu-id="7f50d-149">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[<span data-ttu-id="7f50d-150">View</span><span class="sxs-lookup"><span data-stu-id="7f50d-150">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)| 

 
