---
title: Проверка подлинности пользователей приложений
description: Описывает проверку подлинности в Teams и ее использование в приложениях
ms.topic: conceptual
ms.localizationpriority: medium
keywords: группы проверки подлинности OAuth SSO AAD
ms.openlocfilehash: 1705e85843fbe8d75af978da8baff081b58c6ca1
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720310"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Проверка подлинности пользователей в Microsoft Teams

> [!Note]
> Веб-проверка подлинности для мобильных клиентов требует версии 1.4.1 или более поздней версии Teams Клиента JavaScript.

Чтобы получить доступ к данным пользователей, защищенным Azure Active Directory (AAD) и получить доступ к данным из таких служб, как Facebook и Twitter, приложение устанавливает надежное подключение к этим поставщикам. Если приложение использует API microsoft Graph в области пользователя, проверка подлинности пользователя для получения соответствующих маркеров проверки подлинности.

В Teams есть два разных потока проверки подлинности для приложения. Выполните традиционный поток проверки [](~/tabs/how-to/create-tab-pages/content-page.md) подлинности на веб-сайте на странице контента, встроенной в вкладку, страницу конфигурации или модуль задач. Если приложение содержит бот бесед, используйте поток OAuthPrompt и при желании службу маркеров Azure Bot Framework для проверки подлинности пользователя в ходе беседы.

## <a name="web-based-authentication-flow"></a>Поток проверки подлинности через Интернет

Используйте веб-поток проверки подлинности [для](~/tabs/what-are-tabs.md) вкладок и выберите его с помощью разговорных [ботов](~/bots/what-are-bots.md) или [расширений обмена сообщениями.](~/messaging-extensions/what-are-messaging-extensions.md) Используйте [SDK Microsoft Teams JavaScript](/javascript/api/overview/msteams-client) на странице веб-контента, чтобы включить проверку подлинности. После включения проверки подлинности вставьте страницу содержимого во вкладку, страницу конфигурации или модуль задачи. Дополнительные сведения о потоке проверки подлинности на веб-основе см. в этой странице.

* [Добавление проверки подлинности](~/bots/how-to/authentication/add-authentication.md) в Teams бот описывает использование потока веб-проверки подлинности с помощью разговорного бота.
* [Поток проверки подлинности на вкладке](~/tabs/how-to/authentication/auth-flow-tab.md) описывает работу проверки подлинности вкладок в Teams. Это показывает типичный поток проверки подлинности на веб-основе, используемый для вкладок.
* [AAD проверки](~/tabs/how-to/authentication/auth-tab-AAD.md) подлинности на вкладке описывает, как подключиться к AAD из вкладки в приложении в Teams.
* [В немом AAD](~/tabs/how-to/authentication/auth-silent-AAD.md) описывается, как уменьшить количество подсказок для регистрации или согласия в приложении с помощью AAD.
* [.Net или C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [JavaScript ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) или Node.jsпредоставляет образцы для проверки подлинности на основе веб-сайтов.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Поток OAuthPrompt для разговорных ботов

OAuthPrompt платформы Azure Bot Framework упрощает проверку подлинности для приложений с помощью ботов бесед. Используйте службу маркеров Azure Bot Framework для кэширования маркеров.

Дополнительные сведения об использовании OAuthPrompt см.:

* [Обзор потока проверки подлинности ботов](~/bots/how-to/authentication/auth-flow-bot.md) описывает работу проверки подлинности в боте в приложении в Teams. Это показывает не веб-поток проверки подлинности, используемый для ботов в Teams, настольном приложении и мобильных приложениях.
* [Проверка подлинности ботов](~/bots/how-to/authentication/add-authentication.md) описывает, как добавить проверку подлинности OAuth в Teams бота.

## <a name="code-sample"></a>Пример кода

предоставляет образец проверки подлинности бота v3 SDK.

| **Название примера** | **Описание** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Проверка подлинности ботов | В этом примере показано, как начать проверку подлинности в боте для Microsoft Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Tab, Bot and Messaging Extension (ME) SSO | В этом примере показаны SSO для tab, Bot и ME — поиск, действие, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | Недоступно |


## <a name="configure-the-identity-provider"></a>Настройка поставщика удостоверений

Независимо от потока проверки подлинности приложения настройте поставщика удостоверений для связи с Teams приложением. Большинство примеров и погон в основном связаны с использованием AAD в качестве поставщика удостоверений. Однако концепции применяются независимо от поставщика удостоверений. 

Дополнительные сведения см. [в примере настройки поставщика удостоверений.](~/concepts/authentication/configure-identity-provider.md)

## <a name="third-party-cookies-on-ios"></a>Сторонние файлы cookie на iOS

После обновления iOS 14 Apple заблокировала сторонний доступ к файлам [cookie](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/) для всех приложений по умолчанию. Поэтому приложения, которые используют сторонние файлы cookie для проверки подлинности в вкладке Channel или Chat и личные приложения, не смогут завершить процессы проверки подлинности на Teams iOS-клиентах. Чтобы соответствовать требованиям конфиденциальности и безопасности, необходимо перейти к системе, основанной на маркерах, или использовать первопартийные файлы cookie для рабочего процесса проверки подлинности пользователей.
