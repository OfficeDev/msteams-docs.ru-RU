---
title: Проверка подлинности пользователей приложения
description: Описание проверки подлинности в Teams и ее использования в приложениях
ms.topic: conceptual
keywords: AAD для проверки подлинности OAuth для SSO teams
ms.openlocfilehash: 6ddcd8a9e847d9216b7e2dcc12733a6cd413b48e
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014294"
---
# <a name="authenticating-users-in-microsoft-teams"></a>Проверка подлинности пользователей в Microsoft Teams

> [!Note]
> Для веб-проверки подлинности на мобильных клиентах требуется версия 1.4.1 или более поздней версии SDK JavaScript для Teams.

Чтобы ваше приложение было получать доступ к сведениям о пользователях, защищенным с помощью Azure Active Directory, а также к данным из других служб, таких как Facebook и Twitter, приложению необходимо установить надежное подключение к этим поставщикам. Если ваше приложение должно использовать API Microsoft Graph в области действия пользователя, вам также потребуется проверить подлинность пользователя, чтобы получить соответствующие маркеры проверки подлинности.

В Microsoft Teams существует два различных потока проверки подлинности, которые ваше приложение может использовать. Вы можете выполнить традиционный веб-поток [](~/tabs/how-to/create-tab-pages/content-page.md) проверки подлинности на странице контента, встроенной в вкладку, страницу конфигурации или модуль задачи. Если ваше приложение содержит бота для беседы, вы можете использовать поток OAuthPrompt (и при желании службу маркеров Azure Bot Framework) для проверки подлинности пользователя в рамках беседы.

## <a name="web-based-authentication-flow"></a>Поток веб-проверки подлинности

Вам потребуется использовать веб-поток проверки подлинности для вкладок [и](~/tabs/what-are-tabs.md)выбрать [](~/bots/what-are-bots.md) его для использования с ботами или расширениями обмена [сообщениями.](~/messaging-extensions/what-are-messaging-extensions.md) Вы будете использовать клиентский [SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client) на странице веб-контента, чтобы включить проверку подлинности, а затем встраить эту страницу контента во вкладку, страницу конфигурации или модуль задачи. Если вы хотите использовать поток веб-проверки подлинности с ботом для беседы, необходимо использовать модуль задачи [с ботом.](~/task-modules-and-cards/task-modules/task-modules-bots.md)

* [Поток проверки подлинности на вкладке](~/tabs/how-to/authentication/auth-flow-tab.md) описывает работу проверки подлинности вкладок в Teams. Здесь показан типичный веб-поток проверки подлинности, используемый для вкладок.
* [Проверка подлинности Azure AD](~/tabs/how-to/authentication/auth-tab-AAD.md) на вкладке описывает, как подключиться к Azure Active Directory с помощью вкладки в приложении в Teams.
* [В этой статье](~/tabs/how-to/authentication/auth-silent-AAD.md) описывается, как уменьшить количество входов и получения согласия в приложении с помощью Azure Active Directory.
* Веб-проверка подлинности в [dotnet/C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) или [JavaScript/Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Поток OAuthPrompt для беседальных ботов

OAuthPrompt платформы Azure Bot Framework упрощает проверку подлинности для приложений, использующих ботов для бесед. Вы можете воспользоваться преимуществами службы маркеров Azure Bot Framework, чтобы помочь в кэшинге маркеров.

Дополнительные сведения об использовании OAuthPrompt см. в:

* [Обзор потока проверки подлинности ботов](~/bots/how-to/authentication/auth-flow-bot.md) описывает работу проверки подлинности в боте в вашем приложении в Teams. Здесь показан поток проверки подлинности не из Интернета, используемый для ботов во всех версиях Teams (веб-приложения, классические приложения и мобильные приложения)
* [Проверка подлинности бота](~/bots/how-to/authentication/add-authentication.md)
* Пример проверки подлинности бота (V3 SDK) в [dotnet/C#](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) или [JavaScript/Node.js](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth)

## <a name="configure-your-identity-provider"></a>Настройка поставщика удостоверений

Независимо от того, какой поток проверки подлинности использует ваше приложение (возможно, вы даже используете оба этих потока), вам потребуется настроить поставщика удостоверений для взаимодействия с приложением Teams. Большинство примеров и по walkthroughs, которые вы найдете здесь, в основном связаны с использованием Azure Active Directory в качестве поставщика удостоверений. Однако концепции применяются независимо от используемого поставщика удостоверений.

Дополнительные сведения [см. в настройке поставщика удостоверений](~/concepts/authentication/configure-identity-provider.md)
