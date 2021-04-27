---
title: Проверка подлинности пользователей приложений
description: Описывает проверку подлинности в Teams и ее использование в приложениях
ms.topic: conceptual
localization_priority: Normal
keywords: группы проверки подлинности OAuth SSO AAD
ms.openlocfilehash: 23e0e500ee041afa191e9381b6f69b4c3881c391
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019974"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Проверка подлинности пользователей в Microsoft Teams

> [!NOTE]
> Веб-проверка подлинности для мобильных клиентов требует версии 1.4.1 или более поздней версии SDK JavaScript Microsoft Teams.

Чтобы получить доступ к данным пользователей, защищенным Azure Active Directory (AAD) и получить доступ к данным из таких служб, как Facebook и Twitter, приложение устанавливает надежное подключение к этим поставщикам. Если приложение использует API Microsoft Graph в области пользователя, проверка подлинности пользователя для получения соответствующих маркеров проверки подлинности.

В Teams существует два разных потока проверки подлинности для приложения. Выполните традиционный поток проверки [](~/tabs/how-to/create-tab-pages/content-page.md) подлинности на веб-сайте на странице контента, встроенной в вкладку, страницу конфигурации или модуль задач. Если приложение содержит разговорный бот, используйте поток OAuthPrompt и необязательно службу маркеров Azure Bot Framework для проверки подлинности пользователя в рамках беседы.

## <a name="web-based-authentication-flow"></a>Поток проверки подлинности на веб-основе

Используйте веб-поток проверки подлинности [для](~/tabs/what-are-tabs.md) вкладок и выберите его с помощью разговорных [ботов](~/bots/what-are-bots.md) или [расширений обмена сообщениями.](~/messaging-extensions/what-are-messaging-extensions.md) Используйте [SDK](/javascript/api/overview/msteams-client) клиента Microsoft Teams JavaScript на странице веб-контента, чтобы включить проверку подлинности. После включения проверки подлинности встраить страницу контента в вкладку, страницу конфигурации или модуль задач. Дополнительные сведения о потоке проверки подлинности на веб-основе см. в этой странице.

* [Добавление проверки подлинности в бот Teams](~/bots/how-to/authentication/add-authentication.md) описывает использование потока веб-проверки подлинности с помощью беседного бота.
* [Поток проверки подлинности на вкладке](~/tabs/how-to/authentication/auth-flow-tab.md) описывает работу проверки подлинности вкладок в Teams. Это показывает типичный поток проверки подлинности на веб-основе, используемый для вкладок.
* [Проверка подлинности AAD на вкладке](~/tabs/how-to/authentication/auth-tab-AAD.md) описывает, как подключиться к AAD из вкладки в приложении Teams.
* [Silent authentication AAD](~/tabs/how-to/authentication/auth-silent-AAD.md) describes how to reduce sign-in or consent prompts in the app using AAD.
* [.Net или C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [JavaScript ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) или Node.jsпредоставляет образцы для проверки подлинности на основе веб-сайтов.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Поток OAuthPrompt для разговорных ботов

OAuthPrompt Azure Bot Framework упрощает проверку подлинности для приложений с помощью разговорных ботов. Используйте службу маркеров Azure Bot Framework для помощи кэшингу маркеров.

Дополнительные сведения об использовании OAuthPrompt см.:

* [Обзор потока проверки подлинности ботов](~/bots/how-to/authentication/auth-flow-bot.md) описывает работу проверки подлинности в боте в приложении в Teams. Здесь показан не веб-поток проверки подлинности, используемый для ботов в веб-, настольных приложениях и мобильных приложениях Teams.
* [Проверка подлинности ботов](~/bots/how-to/authentication/add-authentication.md) описывает добавление проверки подлинности OAuth в бот Teams.

## <a name="code-sample"></a>Пример кода

предоставляет образец проверки подлинности бота v3 SDK.

| **Пример имени** | **Описание** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Проверка подлинности ботов | В этом примере показано, как начать проверку подлинности в боте для Microsoft Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |

## <a name="configure-the-identity-provider"></a>Настройка поставщика удостоверений

Независимо от потока проверки подлинности приложения настройте поставщика удостоверений для связи с приложением Teams. Большинство примеров и поуча-ов в основном связаны с использованием AAD в качестве поставщика удостоверений. Однако концепции применяются независимо от поставщика удостоверений.

Дополнительные сведения см. [в примере настройки поставщика удостоверений.](~/concepts/authentication/configure-identity-provider.md)
