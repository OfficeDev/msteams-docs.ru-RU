---
title: Добавление проверки подлинности к своему расширению обмена сообщениями
author: clearab
description: Добавление проверки подлинности к расширению системы обмена сообщениями
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f7ebbcd99b1ec35900de7ec2f54f93263918e945
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675231"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="0d97d-103">Добавление проверки подлинности к своему расширению обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0d97d-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="0d97d-104">Идентификация пользователя</span><span class="sxs-lookup"><span data-stu-id="0d97d-104">Identify the user</span></span>

<span data-ttu-id="0d97d-105">Каждый запрос к службам включает в себя идентификатор пользователя, который выполнил запрос, а также отображаемое имя пользователя и идентификатор объекта Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0d97d-105">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="0d97d-106">Гарантируется, что значения `id` и `aadObjectId` значения для пользователя Teams прошли проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="0d97d-106">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="0d97d-107">Они могут использоваться в качестве ключей для поиска учетных данных или любого кэшированного состояния в службе.</span><span class="sxs-lookup"><span data-stu-id="0d97d-107">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="0d97d-108">Кроме того, каждый запрос содержит идентификатор клиента Azure Active Directory для пользователя, который можно использовать для определения организации пользователя.</span><span class="sxs-lookup"><span data-stu-id="0d97d-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="0d97d-109">Если это возможно, запрос также содержит идентификаторы команд и каналов, из которых поступил запрос.</span><span class="sxs-lookup"><span data-stu-id="0d97d-109">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="0d97d-110">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="0d97d-110">Authentication</span></span>

<span data-ttu-id="0d97d-111">Если для вашей службы требуется проверка подлинности пользователя, необходимо войти в систему, прежде чем ее сможет использовать расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="0d97d-111">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="0d97d-112">Если вы написали робот или вкладку, которые подписываются пользователю, этот раздел должен быть знаком.</span><span class="sxs-lookup"><span data-stu-id="0d97d-112">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="0d97d-113">Последовательность выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0d97d-113">The sequence is as follows:</span></span>

1. <span data-ttu-id="0d97d-114">Пользователь выдает запрос, или запрос по умолчанию автоматически отправляется в службу.</span><span class="sxs-lookup"><span data-stu-id="0d97d-114">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="0d97d-115">Служба проверяет, прошел ли пользователь проверку подлинности, проверив идентификатор пользователя Teams.</span><span class="sxs-lookup"><span data-stu-id="0d97d-115">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="0d97d-116">Если пользователь не прошел проверку подлинности, отправьте `auth` ответ с `openUrl` предложенным действием, включая URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0d97d-116">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="0d97d-117">Клиент Microsoft Teams запускает всплывающее окно, в котором размещается веб-страница, используя указанный URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0d97d-117">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="0d97d-118">После входа пользователя необходимо закрыть окно и отправить ему код проверки подлинности в клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="0d97d-118">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="0d97d-119">Затем клиент Teams повторно отправляет запрос в службу, который включает код проверки подлинности, переданный на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="0d97d-119">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="0d97d-120">Ваша служба должна проверить, что код проверки подлинности, полученный на шаге 6, соответствует тому, что получено на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="0d97d-120">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="0d97d-121">Это гарантирует, что злоумышленник не будет пытаться подменить или ослабить процесс входа в систему.</span><span class="sxs-lookup"><span data-stu-id="0d97d-121">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="0d97d-122">Это фактически "закрывает цикл" для завершения безопасной последовательности проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0d97d-122">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="0d97d-123">Ответ с действием входа</span><span class="sxs-lookup"><span data-stu-id="0d97d-123">Respond with a sign-in action</span></span>

<span data-ttu-id="0d97d-124">Чтобы выдать запрос пользователю, не прошедшему проверку подлинности, выполните ответ с `openUrl` предложенным действием типа, которое включает URL-адрес проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0d97d-124">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="0d97d-125">Пример отклика для действия при входе</span><span class="sxs-lookup"><span data-stu-id="0d97d-125">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="0d97d-126">Для того чтобы при входе в систему можно было размещаться в всплывающем окне Teams, в списке допустимых доменов приложения должен находиться домен, являющийся частью URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="0d97d-126">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="0d97d-127">(См. раздел [валиддомаинс](~/resources/schema/manifest-schema.md#validdomains) в схеме манифеста.)</span><span class="sxs-lookup"><span data-stu-id="0d97d-127">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="0d97d-128">Запуск процесса входа</span><span class="sxs-lookup"><span data-stu-id="0d97d-128">Start the sign-in flow</span></span>

<span data-ttu-id="0d97d-129">Ваш интерфейс пользователя должен отвечать на запросы и размещаться в всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="0d97d-129">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="0d97d-130">Он должен интегрироваться с [клиентским пакетом SDK для Microsoft Teams JavaScript](/javascript/api/overview/msteams-client), который использует передачу сообщений.</span><span class="sxs-lookup"><span data-stu-id="0d97d-130">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="0d97d-131">Как и другие встроенные возможности, выполняемые в Microsoft Teams, код в окне должен вызываться `microsoftTeams.initialize()`первым.</span><span class="sxs-lookup"><span data-stu-id="0d97d-131">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="0d97d-132">Если ваш код выполняет процесс OAuth, можно передать идентификатор пользователя Teams в ваше окно, которое затем может передать его в URL-адрес входа OAuth.</span><span class="sxs-lookup"><span data-stu-id="0d97d-132">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="0d97d-133">Завершение процесса входа</span><span class="sxs-lookup"><span data-stu-id="0d97d-133">Complete the sign-in flow</span></span>

<span data-ttu-id="0d97d-134">Когда запрос на вход завершается и перенаправляется обратно на страницу, он должен выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0d97d-134">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="0d97d-135">Создайте код безопасности.</span><span class="sxs-lookup"><span data-stu-id="0d97d-135">Generate a security code.</span></span> <span data-ttu-id="0d97d-136">(Это может быть случайное число.) Необходимо кэшировать этот код в службе, а также учетные данные, полученные с помощью процесса входа (например, OAuth 2,0 tokens).</span><span class="sxs-lookup"><span data-stu-id="0d97d-136">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="0d97d-137">Позвоните `microsoftTeams.authentication.notifySuccess` и передайте код безопасности.</span><span class="sxs-lookup"><span data-stu-id="0d97d-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="0d97d-138">На этом шаге окно закрывается и управление передается клиенту Teams.</span><span class="sxs-lookup"><span data-stu-id="0d97d-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="0d97d-139">Теперь клиент может повторно отправить исходный запрос пользователя, а также код безопасности в `state` свойстве.</span><span class="sxs-lookup"><span data-stu-id="0d97d-139">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="0d97d-140">Код может использовать код безопасности для поиска ранее сохраненных учетных данных, чтобы выполнить последовательность проверки подлинности, а затем выполнить запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="0d97d-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="0d97d-141">Пример повторной выданной заявки</span><span class="sxs-lookup"><span data-stu-id="0d97d-141">Reissued request example</span></span>

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

