---
title: Проверка подлинности для ботов с Azure Active Directory
description: Описывает проверку подлинности Azure AD в Teams и ее использование в ботах
keywords: команды- боты проверки подлинности AAD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: c3f2f7fe3eb6b10faef2b24b3212081a881d6f8f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020690"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a><span data-ttu-id="1d58a-104">Проверка подлинности пользователя в Microsoft Teams боте</span><span class="sxs-lookup"><span data-stu-id="1d58a-104">Authenticate a user in a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="1d58a-105">Существует множество служб, которые можно использовать в приложении Teams, и большинство из них требуют проверки подлинности и авторизации для получения доступа к службе.</span><span class="sxs-lookup"><span data-stu-id="1d58a-105">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="1d58a-106">Службы включают Facebook, Twitter и, конечно, Teams.</span><span class="sxs-lookup"><span data-stu-id="1d58a-106">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="1d58a-107">Пользователи Teams имеют сведения о профиле пользователей, хранимые в Azure Active Directory (Azure AD) с помощью Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1d58a-107">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph.</span></span> <span data-ttu-id="1d58a-108">В этой статье основное внимание будет уделялось проверке подлинности с помощью Azure AD для получения доступа к этой информации.</span><span class="sxs-lookup"><span data-stu-id="1d58a-108">This article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="1d58a-109">OAuth 2.0 — это открытый стандарт проверки подлинности, используемый Azure AD и многими другими поставщиками услуг.</span><span class="sxs-lookup"><span data-stu-id="1d58a-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="1d58a-110">Понимание OAuth 2.0 является обязательным условием для работы с проверкой подлинности в Teams Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d58a-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="1d58a-111">В примерах ниже используется поток неявных грантов OAuth 2.0 с целью в конечном итоге прочитать сведения о профиле пользователя из Azure AD и Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1d58a-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="1d58a-112">Поток проверки подлинности, описанный в этой статье, очень похож на поток вкладок, за исключением того, что вкладки могут использовать поток проверки подлинности на веб-основе, а ботам требуется проверка подлинности из кода.</span><span class="sxs-lookup"><span data-stu-id="1d58a-112">The authentication flow described in this article is very similar to that of tabs except that tabs can use web based authentication flow, and bots require authentication to be driven from code.</span></span> <span data-ttu-id="1d58a-113">Концепции в этой статье также будут полезны при реализации проверки подлинности с мобильной платформы.</span><span class="sxs-lookup"><span data-stu-id="1d58a-113">The concepts in this article will also be useful when implementing authentication from the mobile platform.</span></span>

<span data-ttu-id="1d58a-114">Общий обзор потока проверки подлинности для ботов см. в разделе Поток проверки подлинности [в ботах.](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="1d58a-114">For a general overview of authentication flow for bots see the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="1d58a-115">Настройка поставщиков удостоверений</span><span class="sxs-lookup"><span data-stu-id="1d58a-115">Configuring identity providers</span></span>

<span data-ttu-id="1d58a-116">См. [](~/concepts/authentication/configure-identity-provider.md) в разделе Настройка поставщиков удостоверений для подробных действий по настройке URL-адреса перенаправления вызовов OAuth 2.0 при использовании Azure Active Directory в качестве поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="1d58a-116">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="1d58a-117">Начало потока проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="1d58a-117">Initiate authentication flow</span></span>

<span data-ttu-id="1d58a-118">Поток проверки подлинности должен быть вызван действием пользователя.</span><span class="sxs-lookup"><span data-stu-id="1d58a-118">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="1d58a-119">Не следует автоматически открывать всплывающее всплывающее окна проверки подлинности, так как это, скорее всего, вызовет блокировку всплывающее окна браузера, а также запутает пользователя.</span><span class="sxs-lookup"><span data-stu-id="1d58a-119">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

## <a name="add-ui-to-start-authentication"></a><span data-ttu-id="1d58a-120">Добавление пользовательского интерфейса для начала проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="1d58a-120">Add UI to start authentication</span></span>

<span data-ttu-id="1d58a-121">Добавьте пользовательский интерфейс в бот, чтобы пользователь при необходимости войду.</span><span class="sxs-lookup"><span data-stu-id="1d58a-121">Add UI to the bot to enable the user to sign in when needed.</span></span> <span data-ttu-id="1d58a-122">Здесь это делается с карты Thumbnail в TypeScript:</span><span class="sxs-lookup"><span data-stu-id="1d58a-122">Here it is done from a Thumbnail card, in TypeScript:</span></span>

```typescript
// Show prompt of options
protected async promptForAction(session: builder.Session): Promise<void> {
    let msg = new builder.Message(session)
        .addAttachment(new builder.ThumbnailCard(session)
            .title(this.providerDisplayName)
            .buttons([
                 builder.CardAction.messageBack(session, "{}", "Sign in")
                     .text("SignIn")
                     .displayText("Sign in"),
                  builder.CardAction.messageBack(session, "{}", "Show profile")
                     .text("ShowProfile")
                     .displayText("Show profile"),
                  builder.CardAction.messageBack(session, "{}", "Sign out")
                     .text("SignOut")
                     .displayText("Sign out"),
            ]));
    session.send(msg);
}
```

<span data-ttu-id="1d58a-123">В карточку героя добавлены три кнопки: Вход, Показать профиль и выйти.</span><span class="sxs-lookup"><span data-stu-id="1d58a-123">Three buttons have been added to the Hero Card: Sign in, Show Profile, and Sign out.</span></span>

## <a name="sign-the-user-in"></a><span data-ttu-id="1d58a-124">Впишите пользователя в</span><span class="sxs-lookup"><span data-stu-id="1d58a-124">Sign the user in</span></span>

<span data-ttu-id="1d58a-125">Из-за проверки, которая должна выполняться из соображений безопасности и поддержки мобильных версий Teams, код здесь не отображается, но вот пример кода, который запускает процесс, когда пользователь нажимает кнопку [Вход.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195). .</span><span class="sxs-lookup"><span data-stu-id="1d58a-125">Because of the validation that must be performed for security reasons and the support for the mobile versions of Teams, the code isn't shown here, but [here's an example of the code that kicks off the process when the user presses the Sign in button.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).</span></span>

<span data-ttu-id="1d58a-126">Проверка и поддержка мобильных устройств объясняются в потоке проверки подлинности [темы в ботах.](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="1d58a-126">The validation and mobile support are explained in the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="1d58a-127">Обязательно добавьте url-адрес перенаправления домена проверки подлинности в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) раздел манифеста.</span><span class="sxs-lookup"><span data-stu-id="1d58a-127">Be sure to add the domain of your authentication redirect URL to the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="1d58a-128">Если этого не делать, всплывающее поле входа не появится.</span><span class="sxs-lookup"><span data-stu-id="1d58a-128">If you don't, the login popup will not appear.</span></span>

## <a name="showing-user-profile-information"></a><span data-ttu-id="1d58a-129">Отображение сведений о профиле пользователя</span><span class="sxs-lookup"><span data-stu-id="1d58a-129">Showing user profile information</span></span>

<span data-ttu-id="1d58a-130">Хотя получение маркера доступа затруднено из-за всех переходов взад и вперед на разных веб-сайтах и проблем безопасности, которые необходимо устранить, когда у вас есть маркер, получение информации из Azure Active Directory просто.</span><span class="sxs-lookup"><span data-stu-id="1d58a-130">Although getting an access token is difficult because of all the transitions back and forth across different websites and the security issues that must be addressed, once you have a token, obtaining information from Azure Active Directory is straightforward.</span></span> <span data-ttu-id="1d58a-131">Бот звонит в конечную точку `me` Graph с маркером доступа.</span><span class="sxs-lookup"><span data-stu-id="1d58a-131">The bot makes a call to the `me` Graph endpoint with the access token.</span></span> <span data-ttu-id="1d58a-132">Graph отвечает сведениями пользователя для пользователя, во входившего в систему.</span><span class="sxs-lookup"><span data-stu-id="1d58a-132">Graph responds with the user information for the person who logged in.</span></span> <span data-ttu-id="1d58a-133">Сведения из ответа используются для создания бот-карты и отправлены.</span><span class="sxs-lookup"><span data-stu-id="1d58a-133">Information from the response is used to construct a bot card and sent.</span></span>

```typescript
// Show user profile
protected async showUserProfile(session: builder.Session): Promise<void> {
    let azureADApi = this.authProvider as AzureADv1Provider;
    let userToken = this.getUserToken(session);

    if (userToken) {
        let profile = await azureADApi.getProfileAsync(userToken.accessToken);
        let profileCard = new builder.ThumbnailCard()
            .title(profile.displayName)
            .subtitle(profile.mail)
            .text(`${profile.jobTitle}<br/> ${profile.officeLocation}`);
        session.send(new builder.Message().addAttachment(profileCard));
    } else {
        session.send("Please sign in to AzureAD so I can access your profile.");
    }

    await this.promptForAction(session);
}

// Helper function to make the Graph API call
public async getProfileAsync(accessToken: string): Promise<any> {
    let options = {
        url: "https://graph.microsoft.com/v1.0/me",
        json: true,
        headers: {
            "Authorization": `Bearer ${accessToken}`,
        },
    };
    return await request.get(options);
}
```

<span data-ttu-id="1d58a-134">Если пользователь не подписан, он должен сделать это.</span><span class="sxs-lookup"><span data-stu-id="1d58a-134">If the user is not signed in they are prompted to do so.</span></span>

## <a name="sign-the-user-out"></a><span data-ttu-id="1d58a-135">Выход пользователя</span><span class="sxs-lookup"><span data-stu-id="1d58a-135">Sign the user out</span></span>

```typescript
// Handle user logout request
private async handleLogout(session: builder.Session): Promise<void> {
    if (!utils.getUserToken(session, this.providerName)) {
        session.send(`You're already signed out of ${this.providerDisplayName}.`);
    } else {
        utils.setUserToken(session, this.providerName, null);
        session.send(`You're now signed out of ${this.providerDisplayName}.`);
    }

    await this.promptForAction(session);
}
```

## <a name="other-samples"></a><span data-ttu-id="1d58a-136">Другие примеры</span><span class="sxs-lookup"><span data-stu-id="1d58a-136">Other samples</span></span>

<span data-ttu-id="1d58a-137">Пример кода, показывающий процесс проверки подлинности ботов, см. в примере:</span><span class="sxs-lookup"><span data-stu-id="1d58a-137">For sample code showing the bot authentication process see:</span></span>

* [<span data-ttu-id="1d58a-138">Microsoft Teams проверки подлинности ботов</span><span class="sxs-lookup"><span data-stu-id="1d58a-138">Microsoft Teams bot authentication sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
