---
title: Добавление проверки подлинности в расширение для сообщений
author: clearab
description: Добавление проверки подлинности в расширение обмена сообщениями
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 1670bcd68def5470f2a590b11f7c25a00ccd06b7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020711"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="26367-103">Добавление проверки подлинности в расширение для сообщений</span><span class="sxs-lookup"><span data-stu-id="26367-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="26367-104">Определение пользователя</span><span class="sxs-lookup"><span data-stu-id="26367-104">Identify the user</span></span>

<span data-ttu-id="26367-105">Каждый запрос в службы включает в себя пользовательский ИД, имя отображения пользователя и Azure Active Directory объекта.</span><span class="sxs-lookup"><span data-stu-id="26367-105">Every request to your services includes the user  ID, the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="26367-106">Данные и значения гарантируются для пользователя, `id` `aadObjectId` Teams проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="26367-106">The `id` and `aadObjectId` values are guaranteed for the authenticated Teams user.</span></span> <span data-ttu-id="26367-107">Они используются в качестве ключей для слежки за учетными данными или любым кэшным состоянием в службе.</span><span class="sxs-lookup"><span data-stu-id="26367-107">They are used as keys to look up the credentials or any cached state in your service.</span></span> <span data-ttu-id="26367-108">Кроме того, каждый запрос содержит Azure Active Directory клиента пользователя, который используется для идентификации организации пользователя.</span><span class="sxs-lookup"><span data-stu-id="26367-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which is used to identify the user’s organization.</span></span> <span data-ttu-id="26367-109">Если это применимо, запрос также содержит командный ИД и ИД канала, из которого был зародился запрос.</span><span class="sxs-lookup"><span data-stu-id="26367-109">If applicable, the request also contains the team Id and channel ID from which the request is originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="26367-110">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="26367-110">Authentication</span></span>

<span data-ttu-id="26367-111">Если ваша служба требует проверки подлинности пользователей, пользователи должны войти, прежде чем использовать расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="26367-111">If your service requires user authentication, the users must sign in before they use the messaging extension.</span></span> <span data-ttu-id="26367-112">Этапы проверки подлинности аналогичны шагам бота или вкладки. Последовательность будет следующим образом:</span><span class="sxs-lookup"><span data-stu-id="26367-112">The authentication steps are similar to that of a bot or tab. The sequence is as follows:</span></span>

1. <span data-ttu-id="26367-113">Пользователь выдает запрос, или запрос по умолчанию автоматически отправляется в службу.</span><span class="sxs-lookup"><span data-stu-id="26367-113">User issues a query, or the default query is automatically sent to your service.</span></span>
1. <span data-ttu-id="26367-114">Служба проверяет, проверяется ли проверка подлинности пользователя, проверяя Teams пользователя.</span><span class="sxs-lookup"><span data-stu-id="26367-114">Your service checks whether the user is authenticated by inspecting the Teams user ID.</span></span>
1. <span data-ttu-id="26367-115">Если пользователь не имеет проверки подлинности, отправьте ответ с предложенным действием, включая `auth` `openUrl` URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="26367-115">If the user is not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
1. <span data-ttu-id="26367-116">Клиент Microsoft Teams запускает диалоговое окно с размещением веб-страницы с помощью данного URL-адреса проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="26367-116">The Microsoft Teams client launches a dialog box hosting your webpage using the given authentication URL.</span></span>
1. <span data-ttu-id="26367-117">После того как пользователь войдет,  необходимо закрыть окно и отправить код проверки подлинности Teams клиенту.</span><span class="sxs-lookup"><span data-stu-id="26367-117">After the user signs in, you should close your window and send an **authentication code** to the Teams client.</span></span>
1. <span data-ttu-id="26367-118">Затем Teams переиздает запрос в службу, которая включает код проверки подлинности, переданный в шаге 5.</span><span class="sxs-lookup"><span data-stu-id="26367-118">The Teams client then reissues the query to your service, which includes the authentication code passed in Step 5.</span></span>

<span data-ttu-id="26367-119">Служба должна убедиться, что код проверки подлинности, полученный на шаге 6, соответствует коду из шага 5.</span><span class="sxs-lookup"><span data-stu-id="26367-119">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="26367-120">Это гарантирует, что злонамеренный пользователь не пытается подменить или скомпрометировать вход в потоке.</span><span class="sxs-lookup"><span data-stu-id="26367-120">This ensures that a malicious user does not try to spoof or compromise the sign in flow.</span></span> <span data-ttu-id="26367-121">Это эффективно "закрывает цикл", чтобы завершить безопасную последовательность проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="26367-121">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="26367-122">Ответ с помощью действия для регистрации</span><span class="sxs-lookup"><span data-stu-id="26367-122">Respond with a sign-in action</span></span>

<span data-ttu-id="26367-123">Чтобы подсказывать неавентированному пользователю войти, ответьте предложенным действием типа, которое включает URL-адрес проверки `openUrl` подлинности.</span><span class="sxs-lookup"><span data-stu-id="26367-123">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="26367-124">Пример ответа для действия входного знака</span><span class="sxs-lookup"><span data-stu-id="26367-124">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="26367-125">Чтобы вход в окне Teams, доменная часть URL-адреса должна быть в списке допустимого домена вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="26367-125">For the sign in experience to be hosted in a Teams pop-up window, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="26367-126">Дополнительные сведения см. [в схеме манифеста validDomains.](~/resources/schema/manifest-schema.md#validdomains)</span><span class="sxs-lookup"><span data-stu-id="26367-126">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="26367-127">Запуск знака в потоке</span><span class="sxs-lookup"><span data-stu-id="26367-127">Start the sign in flow</span></span>

<span data-ttu-id="26367-128">Ваш вход должен быть отзывчивым и соответствовать всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="26367-128">Your sign in experience must be responsive and fit within a pop-up window.</span></span> <span data-ttu-id="26367-129">Он должен интегрироваться с [клиентом Microsoft Teams JavaScript SDK,](/javascript/api/overview/msteams-client)который использует передачу сообщений.</span><span class="sxs-lookup"><span data-stu-id="26367-129">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="26367-130">Как и в других встроенных Microsoft Teams, коду в окне необходимо сначала `microsoftTeams.initialize()` позвонить.</span><span class="sxs-lookup"><span data-stu-id="26367-130">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="26367-131">Если код выполняет поток OAuth, вы можете передать Teams пользователя в окно, которое затем передает его в URL-адрес для регистрации OAuth.</span><span class="sxs-lookup"><span data-stu-id="26367-131">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then passes it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="26367-132">Завершить вход в поток</span><span class="sxs-lookup"><span data-stu-id="26367-132">Complete the sign in flow</span></span>

<span data-ttu-id="26367-133">Когда вход в запросе завершается и перенаправляется обратно на страницу, он должен выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="26367-133">When the sign in request completes and redirects back to your page, it must perform the following steps:</span></span>

1. <span data-ttu-id="26367-134">Создание кода безопасности.</span><span class="sxs-lookup"><span data-stu-id="26367-134">Generate a security code.</span></span> <span data-ttu-id="26367-135">Это случайное число.</span><span class="sxs-lookup"><span data-stu-id="26367-135">This is a random number.</span></span> <span data-ttu-id="26367-136">Необходимо кэшировать этот код в службе вместе с учетными данными, полученными через вход в поток, например маркерами OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="26367-136">You must cache this code on your service, along with the credentials obtained through the sign in flow, such as OAuth 2.0 tokens.</span></span>
1. <span data-ttu-id="26367-137">Вызов `microsoftTeams.authentication.notifySuccess` и пропуск кода безопасности.</span><span class="sxs-lookup"><span data-stu-id="26367-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="26367-138">На этом этапе окно закрывается и управление передается Teams клиенту.</span><span class="sxs-lookup"><span data-stu-id="26367-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="26367-139">Теперь клиент переизбирает исходный запрос пользователя вместе с кодом безопасности в `state` свойстве.</span><span class="sxs-lookup"><span data-stu-id="26367-139">The client now reissues the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="26367-140">Код безопасности может использовать код безопасности для проверки учетных данных, хранимых ранее, для завершения последовательности проверки подлинности и выполнения запроса пользователя.</span><span class="sxs-lookup"><span data-stu-id="26367-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="26367-141">Пример повторного запроса</span><span class="sxs-lookup"><span data-stu-id="26367-141">Reissued request example</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="26367-142">Пример кода</span><span class="sxs-lookup"><span data-stu-id="26367-142">Code sample</span></span>
|<span data-ttu-id="26367-143">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="26367-143">**Sample name**</span></span> | <span data-ttu-id="26367-144">**Description**</span><span class="sxs-lookup"><span data-stu-id="26367-144">**Description**</span></span> |<span data-ttu-id="26367-145">**.NET**</span><span class="sxs-lookup"><span data-stu-id="26367-145">**.NET**</span></span> | <span data-ttu-id="26367-146">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="26367-146">**Node.js**</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="26367-147">Расширения обмена сообщениями — auth и config</span><span class="sxs-lookup"><span data-stu-id="26367-147">Messaging extensions - auth and config</span></span> | <span data-ttu-id="26367-148">Расширение обмена сообщениями, которое имеет страницу конфигурации, принимает запросы на поиск и возвращает результаты после того, как пользователь войт.</span><span class="sxs-lookup"><span data-stu-id="26367-148">A Messaging Extension that has a configuration page, accepts search requests, and returns results after the user has signed in.</span></span> |[<span data-ttu-id="26367-149">View</span><span class="sxs-lookup"><span data-stu-id="26367-149">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[<span data-ttu-id="26367-150">View</span><span class="sxs-lookup"><span data-stu-id="26367-150">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)| 

 
