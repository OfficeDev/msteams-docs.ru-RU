---
title: Проверка подлинности для боты с помощью Azure Active Directory
description: Описание проверки подлинности Azure AD в Teams и ее использования в Боты
keywords: Проверка подлинности в Teams Боты AAD
ms.date: 03/01/2018
ms.openlocfilehash: 268af02c51b21b65214bce4673b54ac564a125ae
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675473"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a><span data-ttu-id="b4c86-104">Проверка подлинности пользователя в роботе Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b4c86-104">Authenticate a user in a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="b4c86-105">Существует множество служб, которые вы можете использовать в приложении Teams, а большинство этих служб требуют проверки подлинности и авторизации для получения доступа к службе.</span><span class="sxs-lookup"><span data-stu-id="b4c86-105">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="b4c86-106">Службы включают в себя Facebook, Twitter и учебные группы.</span><span class="sxs-lookup"><span data-stu-id="b4c86-106">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="b4c86-107">Сведения о профилях пользователей в Teams хранятся в Azure Active Directory (Azure AD) с помощью Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b4c86-107">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph.</span></span> <span data-ttu-id="b4c86-108">Эта статья посвящена проверке подлинности с помощью Azure AD для получения доступа к этим сведениям.</span><span class="sxs-lookup"><span data-stu-id="b4c86-108">This article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="b4c86-109">OAuth 2,0 — это открытый стандарт проверки подлинности, используемый Azure AD, и многие другие поставщики услуг.</span><span class="sxs-lookup"><span data-stu-id="b4c86-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="b4c86-110">Общие сведения о OAuth 2,0 является необходимым условием для работы с проверкой подлинности в Teams и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4c86-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="b4c86-111">В приведенных ниже примерах используется неявный поток предоставления OAuth 2,0 с целью последующего считывания сведений профиля пользователя из Azure AD и Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b4c86-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="b4c86-112">Процесс проверки подлинности, описанный в этой статье, очень похож на тот, что используется для вкладок, за исключением того, что вкладки могут использовать веб-процесс проверки подлинности на основе веб-сервера, а Боты требует от кода</span><span class="sxs-lookup"><span data-stu-id="b4c86-112">The authentication flow described in this article is very similar to that of tabs except that tabs can use web based authentication flow, and bots require authentication to be driven from code.</span></span> <span data-ttu-id="b4c86-113">Понятия, описанные в этой статье, также будут использоваться при реализации проверки подлинности на мобильной платформе.</span><span class="sxs-lookup"><span data-stu-id="b4c86-113">The concepts in this article will also be useful when implementing authentication from the mobile platform.</span></span>

<span data-ttu-id="b4c86-114">Общий обзор процесса проверки подлинности для Боты представлен в разделе [Flow Authentication Flow in Боты](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="b4c86-114">For a general overview of authentication flow for bots see the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="b4c86-115">Настройка поставщиков удостоверений</span><span class="sxs-lookup"><span data-stu-id="b4c86-115">Configuring identity providers</span></span>

<span data-ttu-id="b4c86-116">В разделе [Настройка поставщиков удостоверений](~/concepts/authentication/configure-identity-provider.md) подробные указания по настройке URL-адресов перенаправления для обратного вызова OAuth 2,0 при использовании Azure Active Directory в качестве поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="b4c86-116">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="b4c86-117">Запуск процесса проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="b4c86-117">Initiate authentication flow</span></span>

<span data-ttu-id="b4c86-118">Процесс проверки подлинности должен инициироваться действием пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4c86-118">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="b4c86-119">Не следует открывать всплывающую подсказку проверки подлинности автоматически, так как это может вызвать блокирование всплывающих окон в браузере, а также запутать пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4c86-119">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

## <a name="add-ui-to-start-authentication"></a><span data-ttu-id="b4c86-120">Добавление пользовательского интерфейса для запуска проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="b4c86-120">Add UI to start authentication</span></span>

<span data-ttu-id="b4c86-121">Добавление пользовательского интерфейса к элементу ленты, чтобы разрешить пользователю выполнять вход при необходимости.</span><span class="sxs-lookup"><span data-stu-id="b4c86-121">Add UI to the bot to enable the user to sign in when needed.</span></span> <span data-ttu-id="b4c86-122">Здесь это делается с помощью карточки эскиза в TypeScript:</span><span class="sxs-lookup"><span data-stu-id="b4c86-122">Here it is done from a Thumbnail card, in TypeScript:</span></span>

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

<span data-ttu-id="b4c86-123">В карточку главный Имиджевый баннер добавлены три кнопки: войти, Показать профиль и выйти.</span><span class="sxs-lookup"><span data-stu-id="b4c86-123">Three buttons have been added to the Hero Card: Sign in, Show Profile, and Sign out.</span></span>

## <a name="sign-the-user-in"></a><span data-ttu-id="b4c86-124">Подпишите пользователя в</span><span class="sxs-lookup"><span data-stu-id="b4c86-124">Sign the user in</span></span>

<span data-ttu-id="b4c86-125">Из-за проверки, которая должна быть выполнена из соображений безопасности и поддержки версий Teams для мобильных устройств, код не показан здесь, но [здесь приведен пример кода, который запускает процесс, когда пользователь нажимает кнопку входа.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)..</span><span class="sxs-lookup"><span data-stu-id="b4c86-125">Because of the validation that must be performed for security reasons and the support for the mobile versions of Teams, the code isn't shown here, but [here's an example of the code that kicks off the process when the user presses the Sign in button.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).</span></span>

<span data-ttu-id="b4c86-126">Проверка и поддержка для мобильных устройств описаны в разделе [Flow Authentication Flow in Боты](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="b4c86-126">The validation and mobile support are explained in the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="b4c86-127">Не забудьте добавить домен URL-адреса перенаправления проверки подлинности в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) раздел манифеста.</span><span class="sxs-lookup"><span data-stu-id="b4c86-127">Be sure to add the domain of your authentication redirect URL to the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="b4c86-128">В противном случае всплывающее окно входа не появится.</span><span class="sxs-lookup"><span data-stu-id="b4c86-128">If you don't, the login popup will not appear.</span></span>

## <a name="showing-user-profile-information"></a><span data-ttu-id="b4c86-129">Показ сведений о профилях пользователей</span><span class="sxs-lookup"><span data-stu-id="b4c86-129">Showing user profile information</span></span>

<span data-ttu-id="b4c86-130">Несмотря на то, что получение маркера доступа затрудняется, так как все переходы передаются по разным веб-сайтам и проблемы безопасности, которые необходимо устранить, при наличии маркера получение информации из Azure Active Directory является простым.</span><span class="sxs-lookup"><span data-stu-id="b4c86-130">Although getting an access token is difficult because of all the transitions back and forth across different websites and the security issues that must be addressed, once you have a token, obtaining information from Azure Active Directory is straightforward.</span></span> <span data-ttu-id="b4c86-131">Bot выполняет вызов конечной точки `me` Graph с помощью маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="b4c86-131">The bot makes a call to the `me` Graph endpoint with the access token.</span></span> <span data-ttu-id="b4c86-132">Graph отвечает сведениям пользователя о пользователе, который вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="b4c86-132">Graph responds with the user information for the person who logged in.</span></span> <span data-ttu-id="b4c86-133">Информация из отклика используется для создания и отправки почтовых карточек.</span><span class="sxs-lookup"><span data-stu-id="b4c86-133">Information from the response is used to construct a bot card and sent.</span></span>

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

<span data-ttu-id="b4c86-134">Если пользователь не вошел в систему, вам будет предложено сделать это.</span><span class="sxs-lookup"><span data-stu-id="b4c86-134">If the user is not signed in they are prompted to do so.</span></span>

## <a name="sign-the-user-out"></a><span data-ttu-id="b4c86-135">Выход пользователя</span><span class="sxs-lookup"><span data-stu-id="b4c86-135">Sign the user out</span></span>

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

## <a name="other-samples"></a><span data-ttu-id="b4c86-136">Другие примеры</span><span class="sxs-lookup"><span data-stu-id="b4c86-136">Other samples</span></span>

<span data-ttu-id="b4c86-137">Пример кода, демонстрирующий процесс создания подлинности на Bot, см.</span><span class="sxs-lookup"><span data-stu-id="b4c86-137">For sample code showing the bot authentication process see:</span></span>

* [<span data-ttu-id="b4c86-138">Пример проверки подлинности с помощью кода ленты Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b4c86-138">Microsoft Teams bot authentication sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
