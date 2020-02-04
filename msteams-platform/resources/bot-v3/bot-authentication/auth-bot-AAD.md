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
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>Проверка подлинности пользователя в роботе Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Существует множество служб, которые вы можете использовать в приложении Teams, а большинство этих служб требуют проверки подлинности и авторизации для получения доступа к службе. Службы включают в себя Facebook, Twitter и учебные группы. Сведения о профилях пользователей в Teams хранятся в Azure Active Directory (Azure AD) с помощью Microsoft Graph. Эта статья посвящена проверке подлинности с помощью Azure AD для получения доступа к этим сведениям.

OAuth 2,0 — это открытый стандарт проверки подлинности, используемый Azure AD, и многие другие поставщики услуг. Общие сведения о OAuth 2,0 является необходимым условием для работы с проверкой подлинности в Teams и Azure AD. В приведенных ниже примерах используется неявный поток предоставления OAuth 2,0 с целью последующего считывания сведений профиля пользователя из Azure AD и Microsoft Graph.

Процесс проверки подлинности, описанный в этой статье, очень похож на тот, что используется для вкладок, за исключением того, что вкладки могут использовать веб-процесс проверки подлинности на основе веб-сервера, а Боты требует от кода Понятия, описанные в этой статье, также будут использоваться при реализации проверки подлинности на мобильной платформе.

Общий обзор процесса проверки подлинности для Боты представлен в разделе [Flow Authentication Flow in Боты](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

## <a name="configuring-identity-providers"></a>Настройка поставщиков удостоверений

В разделе [Настройка поставщиков удостоверений](~/concepts/authentication/configure-identity-provider.md) подробные указания по настройке URL-адресов перенаправления для обратного вызова OAuth 2,0 при использовании Azure Active Directory в качестве поставщика удостоверений.

## <a name="initiate-authentication-flow"></a>Запуск процесса проверки подлинности

Процесс проверки подлинности должен инициироваться действием пользователя. Не следует открывать всплывающую подсказку проверки подлинности автоматически, так как это может вызвать блокирование всплывающих окон в браузере, а также запутать пользователя.

## <a name="add-ui-to-start-authentication"></a>Добавление пользовательского интерфейса для запуска проверки подлинности

Добавление пользовательского интерфейса к элементу ленты, чтобы разрешить пользователю выполнять вход при необходимости. Здесь это делается с помощью карточки эскиза в TypeScript:

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

В карточку главный Имиджевый баннер добавлены три кнопки: войти, Показать профиль и выйти.

## <a name="sign-the-user-in"></a>Подпишите пользователя в

Из-за проверки, которая должна быть выполнена из соображений безопасности и поддержки версий Teams для мобильных устройств, код не показан здесь, но [здесь приведен пример кода, который запускает процесс, когда пользователь нажимает кнопку входа.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)..

Проверка и поддержка для мобильных устройств описаны в разделе [Flow Authentication Flow in Боты](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

Не забудьте добавить домен URL-адреса перенаправления проверки подлинности в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) раздел манифеста. В противном случае всплывающее окно входа не появится.

## <a name="showing-user-profile-information"></a>Показ сведений о профилях пользователей

Несмотря на то, что получение маркера доступа затрудняется, так как все переходы передаются по разным веб-сайтам и проблемы безопасности, которые необходимо устранить, при наличии маркера получение информации из Azure Active Directory является простым. Bot выполняет вызов конечной точки `me` Graph с помощью маркера доступа. Graph отвечает сведениям пользователя о пользователе, который вошел в систему. Информация из отклика используется для создания и отправки почтовых карточек.

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

Если пользователь не вошел в систему, вам будет предложено сделать это.

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

Пример кода, демонстрирующий процесс создания подлинности на Bot, см.

* [Пример проверки подлинности с помощью кода ленты Microsoft Teams](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
