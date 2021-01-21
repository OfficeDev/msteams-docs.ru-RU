---
title: Добавление проверки подлинности в расширение обмена сообщениями
author: clearab
description: Добавление проверки подлинности в расширение обмена сообщениями
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 4ebe65af06240d13ceb99fe3b7640ab402d716c5
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911872"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="bb9f7-103">Добавление проверки подлинности в расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="bb9f7-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="bb9f7-104">Идентификация пользователя</span><span class="sxs-lookup"><span data-stu-id="bb9f7-104">Identify the user</span></span>

<span data-ttu-id="bb9f7-105">Каждый запрос к вашим службам включает в себя запутывавный ИД пользователя, выполнив запрос, а также отображаемого имени пользователя и ИД объекта Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-105">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="bb9f7-106">Эти значения гарантированно будут у пользователя Teams с проверкой `id` `aadObjectId` подлинности.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-106">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="bb9f7-107">Их можно использовать в качестве ключей для иска учетных данных или любого кэшного состояния в службе.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-107">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="bb9f7-108">Кроме того, каждый запрос содержит ИД клиента Azure Active Directory пользователя, который можно использовать для идентификации организации пользователя.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="bb9f7-109">Если применимо, запрос также содержит команды и каналы, из которых был произведен запрос.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-109">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="bb9f7-110">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="bb9f7-110">Authentication</span></span>

<span data-ttu-id="bb9f7-111">Если служба требует проверки подлинности пользователя, необходимо войти в систему пользователя, прежде чем он сможет использовать расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-111">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="bb9f7-112">Если вы написали бот или вкладку, которая подписывает пользователя, этот раздел должен быть знаком.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-112">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="bb9f7-113">Последовательность действий:</span><span class="sxs-lookup"><span data-stu-id="bb9f7-113">The sequence is as follows:</span></span>

1. <span data-ttu-id="bb9f7-114">Пользователь отправляет запрос или автоматически отправляет запрос по умолчанию в вашу службу.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-114">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="bb9f7-115">Ваша служба проверяет, впервые ли пользователь проверил подлинность, проверив его ИД пользователя Teams.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-115">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="bb9f7-116">Если пользователь не прошла проверку подлинности, отправьте ответ с рекомендуемым действием, включая `auth` `openUrl` URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-116">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="bb9f7-117">Клиент Microsoft Teams запускает всплывающее окно с веб-страницей с использованием заданного URL-адреса проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-117">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="bb9f7-118">После того как пользователь войдет, необходимо закрыть окно и отправить "код проверки подлинности" клиенту Teams.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-118">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="bb9f7-119">Затем клиент Teams повторно выдает запрос службе, в том числе код проверки подлинности, переданный на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-119">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="bb9f7-120">Ваша служба должна убедиться, что код проверки подлинности, полученный на шаге 6, соответствует коду, полученному на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-120">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="bb9f7-121">Это гарантирует, что злоумышленник не попытается подменить или нарушить поток входов.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-121">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="bb9f7-122">Это фактически "закрывает цикл", чтобы завершить последовательность безопасной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-122">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="bb9f7-123">Ответ с помощью действия для регистрации</span><span class="sxs-lookup"><span data-stu-id="bb9f7-123">Respond with a sign-in action</span></span>

<span data-ttu-id="bb9f7-124">Чтобы предложить пользователю, не подлинность пользователя, войти, ответьте предлагаемым действием типа, которое включает `openUrl` URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-124">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="bb9f7-125">Пример ответа для действия при входе</span><span class="sxs-lookup"><span data-stu-id="bb9f7-125">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="bb9f7-126">Чтобы во всплывающее приложение Teams можно было войти во всплывающее приложение, доменная часть URL-адреса должна быть указана в списке допустимого домена вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-126">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="bb9f7-127">[(См. validDomains](~/resources/schema/manifest-schema.md#validdomains) в схеме манифеста.)</span><span class="sxs-lookup"><span data-stu-id="bb9f7-127">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="bb9f7-128">Запуск потока входов</span><span class="sxs-lookup"><span data-stu-id="bb9f7-128">Start the sign-in flow</span></span>

<span data-ttu-id="bb9f7-129">Во всплывающее окно должна отвечать и умещаться ваша возможность входов.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-129">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="bb9f7-130">Он должен интегрироваться с [клиентским SDK JavaScript для Microsoft Teams,](/javascript/api/overview/msteams-client)который использует передачу сообщений.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-130">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="bb9f7-131">Как и в других встроенных решениях, работающих в Microsoft Teams, код в окне должен сначала `microsoftTeams.initialize()` вызываться.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-131">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="bb9f7-132">Если код выполняет поток OAuth, вы можете передать в окно ИД пользователя Teams, который затем может передать его на URL-адрес для входов в OAuth.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-132">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="bb9f7-133">Завершение потока входов</span><span class="sxs-lookup"><span data-stu-id="bb9f7-133">Complete the sign-in flow</span></span>

<span data-ttu-id="bb9f7-134">Когда запрос на вход завершается и перенаправляется обратно на страницу, он должен выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bb9f7-134">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="bb9f7-135">Создание кода безопасности.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-135">Generate a security code.</span></span> <span data-ttu-id="bb9f7-136">(Это может быть случайное число.) Этот код необходимо кэшировать в службе, а также учетные данные, полученные в потоке входа (например, маркеры OAuth 2.0).</span><span class="sxs-lookup"><span data-stu-id="bb9f7-136">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="bb9f7-137">Вызовите `microsoftTeams.authentication.notifySuccess` и передав код безопасности.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="bb9f7-138">На этом этапе окно закрывается и управление передается клиенту Teams.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="bb9f7-139">Теперь клиент может повторно использовать исходный запрос пользователя вместе с кодом безопасности в `state` свойстве.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-139">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="bb9f7-140">Код безопасности может использовать код безопасности, чтобы найти учетные данные, сохраненные ранее, чтобы завершить последовательность проверки подлинности, а затем выполнить запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="bb9f7-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="bb9f7-141">Пример повторного выдачи запроса</span><span class="sxs-lookup"><span data-stu-id="bb9f7-141">Reissued request example</span></span>

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

## <a name="samples"></a><span data-ttu-id="bb9f7-142">Примеры</span><span class="sxs-lookup"><span data-stu-id="bb9f7-142">Samples</span></span>
<span data-ttu-id="bb9f7-143">Пример кода, показывающий процесс проверки подлинности с расширениями обмена сообщениями, см. в:</span><span class="sxs-lookup"><span data-stu-id="bb9f7-143">For sample code showing the messaging-extensions authentication process, see:</span></span>

[<span data-ttu-id="bb9f7-144">Пример проверки подлинности расширений обмена сообщениями Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bb9f7-144">Microsoft Teams messaging-extensions authentication sample</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)

 
