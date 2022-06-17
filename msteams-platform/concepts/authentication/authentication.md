---
title: Проверка подлинности пользователей приложения
description: В этом модуле вы узнаете, как Teams в приложениях, веб-потоке проверки подлинности и потоке OAuthPrompt для чат-ботов.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 0ea8813d8428036521cc4488668a30d82470a8d0
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143468"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Проверка подлинности пользователей в Microsoft Teams

Проверка подлинности — это проверка пользователей приложения и защита пользователей приложений от несанкционированного доступа. Вы можете использовать метод проверки подлинности, подходящий для вашего приложения, для проверки пользователей приложения, которые хотят использовать Teams приложения.

Выберите добавление проверки подлинности для приложения одним из двух способов:

- Включение единого входа **(SSO)** в приложении Teams: единый вход в Teams — это метод проверки подлинности, который использует удостоверение пользователя приложения Teams для предоставления ему доступа к приложению. Пользователю, выполнившего вход Teams, не нужно повторно вошел в приложение в Teams среде. Если пользователю приложения требуется только согласие, Teams получает сведения о доступе к ним из Azure Active Directory (AD). После того как пользователь приложения предоставил согласие, он может получить доступ к приложению даже с других устройств без повторной проверки.

- **Включение проверки** подлинности с помощью стороннего поставщика OAuth. Вы можете использовать сторонний поставщик удостоверений OAuth (IdP) для проверки подлинности пользователей приложения. Пользователь приложения зарегистрирован в поставщике удостоверений, который имеет отношение доверия с вашим приложением. Когда пользователь пытается войти в систему, поставщик удостоверений проверяет пользователя приложения и предоставляет ему доступ к приложению. Azure AD является одним из таких сторонних поставщиков OAuth. Вы можете использовать другие поставщики, такие как Google, Facebook, GitHub или любой другой поставщик.

## <a name="select-authentication-method"></a>Выбор метода проверки подлинности

Включите проверку подлинности с помощью единого входа или сторонних поставщиков удостоверений OAuth в приложении вкладок, приложении бота и приложении расширения для обмена сообщениями. Выберите один из двух способов добавления проверки подлинности в приложение:

:::row:::
    :::column span="1":::
        Единый вход
    :::column-end:::
    :::column span="1":::
        &nbsp;
    :::column-end:::
    :::column span="1":::
        OAuth
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/tab-sso-icon.png" alt-text="Единый вход для приложения табуляции" link="../../tabs/how-to/authentication/tab-sso-overview.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **Приложение tab**  
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/tab-app-idp.png" alt-text="Проверка подлинности с помощью стороннего поставщика OAuth для приложения табуляции." link="../../tabs/how-to/authentication/auth-tab-aad.md" border="false":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-sso-icon.png" alt-text="Единый вход для приложения-бота" link="../../bots/how-to/authentication/auth-aad-sso-bots.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **Приложение-бот**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-app-idp.png" alt-text="Проверка подлинности с помощью стороннего поставщика OAuth для приложения-бота." link="../../bots/how-to/authentication/add-authentication.md" border="false":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-sso-icon.png" alt-text="Единый вход для приложения расширения для обмена сообщениями" link="../../messaging-extensions/how-to/enable-SSO-auth-me.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; **Приложение расширения сообщения**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-app-idp.png" alt-text="Проверка подлинности с помощью сторонних поставщиков удостоверений oAuth для приложения расширения для обмена сообщениями." link="../../messaging-extensions/how-to/add-authentication.md" border="false":::
    :::column-end:::
:::row-end:::

> [!NOTE]
> Страница автоматической проверки подлинности перемещается в модуль "Ресурсы". Дополнительные сведения см. в [разделе "Автоматическая проверка подлинности"](../../tabs/how-to/authentication/auth-silent-aad.md).

## <a name="see-also"></a>См. также

- [Включение единого входа в приложении табуляции](../../tabs/how-to/authentication/tab-sso-overview.md)
- [Проверка подлинности Microsoft Teams для вкладок](~/tabs/how-to/authentication/auth-flow-tab.md)
- [Поддержка единого входа для ботов](~/bots/how-to/authentication/auth-aad-sso-bots.md)
- [Добавление проверки подлинности в расширение для сообщений](~/messaging-extensions/how-to/add-authentication.md)
