---
title: Проверка подлинности для ботов с Azure Active Directory
description: Описывает проверку подлинности Azure AD в Teams и ее использование в ботах
keywords: команды- боты проверки подлинности AAD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: c3f2f7fe3eb6b10faef2b24b3212081a881d6f8f
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157292"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>Проверка подлинности пользователя в Microsoft Teams боте

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Существует множество служб, которые можно использовать в приложении Teams, и большинство из них требуют проверки подлинности и авторизации для получения доступа к службе. Службы включают Facebook, Twitter и, конечно, Teams. Пользователи Teams имеют сведения о профиле пользователей, хранимые в Azure Active Directory (Azure AD) с помощью Microsoft Graph. В этой статье основное внимание будет уделялось проверке подлинности с помощью Azure AD для получения доступа к этой информации.

OAuth 2.0 — это открытый стандарт проверки подлинности, используемый Azure AD и многими другими поставщиками услуг. Понимание OAuth 2.0 является обязательным условием для работы с проверкой подлинности в Teams Azure AD. В примерах ниже используется поток неявных грантов OAuth 2.0 с целью в конечном итоге прочитать сведения о профиле пользователя из Azure AD и Microsoft Graph.

Поток проверки подлинности, описанный в этой статье, очень похож на поток вкладок, за исключением того, что вкладки могут использовать поток проверки подлинности на веб-основе, а ботам требуется проверка подлинности из кода. Концепции в этой статье также будут полезны при реализации проверки подлинности с мобильной платформы.

Общий обзор потока проверки подлинности для ботов см. в разделе Поток проверки подлинности [в ботах.](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)

## <a name="configuring-identity-providers"></a>Настройка поставщиков удостоверений

См. [](~/concepts/authentication/configure-identity-provider.md) в разделе Настройка поставщиков удостоверений для подробных действий по настройке URL-адреса перенаправления вызовов OAuth 2.0 при использовании Azure Active Directory в качестве поставщика удостоверений.

## <a name="initiate-authentication-flow"></a>Начало потока проверки подлинности

Поток проверки подлинности должен быть вызван действием пользователя. Не следует автоматически открывать всплывающее всплывающее окна проверки подлинности, так как это, скорее всего, вызовет блокировку всплывающее окна браузера, а также запутает пользователя.

## <a name="add-ui-to-start-authentication"></a>Добавление пользовательского интерфейса для начала проверки подлинности

Добавьте пользовательский интерфейс в бот, чтобы пользователь при необходимости войду. Здесь это делается с карты Thumbnail в TypeScript:

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

В карточку героя добавлены три кнопки: Вход, Показать профиль и выйти.

## <a name="sign-the-user-in"></a>Впишите пользователя в

Из-за проверки, которая должна выполняться из соображений безопасности и поддержки мобильных версий Teams, код здесь не отображается, но вот пример кода, который запускает процесс, когда пользователь нажимает кнопку [Вход.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195). .

Проверка и поддержка мобильных устройств объясняются в потоке проверки подлинности [темы в ботах.](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)

Обязательно добавьте url-адрес перенаправления домена проверки подлинности в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) раздел манифеста. Если этого не делать, всплывающее поле входа не появится.

## <a name="showing-user-profile-information"></a>Отображение сведений о профиле пользователя

Хотя получение маркера доступа затруднено из-за всех переходов взад и вперед на разных веб-сайтах и проблем безопасности, которые необходимо устранить, когда у вас есть маркер, получение информации из Azure Active Directory просто. Бот звонит в конечную точку `me` Graph с маркером доступа. Graph отвечает сведениями пользователя для пользователя, во входившего в систему. Сведения из ответа используются для создания бот-карты и отправлены.

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

Если пользователь не подписан, он должен сделать это.

## <a name="sign-the-user-out"></a>Выход пользователя

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

## <a name="other-samples"></a>Другие примеры

Пример кода, показывающий процесс проверки подлинности ботов, см. в примере:

* [Microsoft Teams проверки подлинности ботов](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
