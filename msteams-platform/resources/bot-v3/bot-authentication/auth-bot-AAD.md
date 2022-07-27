---
title: Проверка подлинности для ботов с помощью Azure Active Directory
description: Описание Azure AD проверки подлинности в Teams и ее использования в ботах
keywords: боты проверки подлинности teams Azure AD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: 2b467f6a7b4678110dece3b54a67227df6beeaf7
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035165"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>Проверка подлинности пользователя в боте Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

В приложении Teams может потребоваться использовать множество служб, и большинство из них требуют проверки подлинности и авторизации для получения доступа. К службам относятся Facebook, Twitter и Teams. У пользователей в Teams есть сведения о профиле пользователя, хранящиеся в Azure Active Directory с помощью Microsoft Graph. В этом разделе основное внимание уделяется проверке подлинности Azure AD для получения доступа.
OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений. Понимание механизма OAuth 2.0 необходимо для работы с проверкой подлинности в Teams и Azure AD. В следующих примерах поток неявного предоставления OAuth 2.0 используется для считывания сведений о профиле пользователя из Azure AD Microsoft Graph.

Поток проверки подлинности, описанный в этом разделе, похож на вкладки, за исключением того, что вкладки могут использовать веб-поток проверки подлинности, а ботам требуется проверка подлинности на основе кода. Концепции в этом разделе также будут полезны при реализации проверки подлинности с мобильной платформы.

Общие сведения о потоке проверки подлинности для ботов см. в разделе "Поток проверки [подлинности в ботах"](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

## <a name="configuring-identity-providers"></a>Настройка поставщиков удостоверений

Подробные инструкции по настройке URL-адресов перенаправления обратного вызова OAuth 2.0 при использовании Azure Active Directory в качестве поставщика удостоверений см. в разделе "Настройка поставщиков удостоверений".[](~/concepts/authentication/configure-identity-provider.md)

## <a name="initiate-authentication-flow"></a>Запуск потока проверки подлинности

Поток проверки подлинности должен активироваться действием пользователя. Не открывайте всплывающее окно проверки подлинности автоматически, так как это может вызвать блокировку всплывающих элементов браузера и запутать пользователя.

## <a name="add-ui-to-start-authentication"></a>Добавление пользовательского интерфейса для запуска проверки подлинности

Добавьте пользовательский интерфейс в бот, чтобы пользователь при необходимости входить в систему. Вот как это делается на карточке эскиза в TypeScript:

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

В карточку главного имиджевого баннера добавлены три кнопки: "Вход", "Показать профиль" и "Выйти".

## <a name="sign-the-user-in"></a>Вход пользователя

Из-за проверки, которую необходимо выполнить из соображений безопасности и поддержки мобильных версий Teams, код здесь не отображается, но ниже приведен пример кода, который запускает процесс, когда пользователь нажимает кнопку входа[.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)

Проверка и поддержка мобильных устройств описаны в потоке проверки [подлинности раздела в ботах](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

Обязательно добавьте домен URL-адреса перенаправления проверки подлинности в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) раздел манифеста. Если вы не выполните вход, всплывающее окно не появится.

## <a name="showing-user-profile-information"></a>Отображение сведений о профиле пользователя

Хотя получение маркера доступа затруднено из-за всех переходов между различными веб-сайтами и проблем безопасности, которые необходимо устранить, после получения маркера получить сведения из Azure Active Directory очень просто. Бот вызывает конечную точку `me` Graph с маркером доступа. Graph отвечает сведениями о пользователе для пользователя, выполнившего вход. Сведения из ответа используются для создания карточки бота и отправки.

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

Если пользователь не выполнил вход, ему будет предложено сделать это.

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

Пример кода, демонстрирующий процесс проверки подлинности бота, см. в следующих статьях:

* [Пример проверки подлинности бота Microsoft Teams](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
