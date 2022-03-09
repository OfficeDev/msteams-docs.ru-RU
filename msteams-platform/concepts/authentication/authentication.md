---
title: Проверка подлинности пользователей приложений
description: Описывает проверку подлинности в Teams и ее использование в приложениях
ms.topic: conceptual
ms.localizationpriority: medium
keywords: группы проверки подлинности OAuth SSO Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: efc065f317d0877b3e5f158566cba6d5d095505f
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399347"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Проверка подлинности пользователей в Microsoft Teams

> [!Note]
> Веб-проверка подлинности для мобильных клиентов требует версии 1.4.1 или более поздней версии Teams клиента JavaScript.

Чтобы получить доступ к данным пользователей, защищенным Azure AD, и получить доступ к данным из таких служб, как Facebook и Twitter, приложение устанавливает надежное подключение к этим поставщикам. Если приложение использует API microsoft Graph в области пользователей, проверка подлинности пользователя для получения соответствующих маркеров проверки подлинности.

В Teams есть два разных потока проверки подлинности для приложения. Выполните традиционный поток проверки подлинности на веб-сайте на странице контента, встроенной в вкладку, страницу конфигурации или модуль задач.[](~/tabs/how-to/create-tab-pages/content-page.md) Если приложение содержит бот бесед, используйте поток OAuthPrompt и при желании службу маркеров Azure Bot Framework для проверки подлинности пользователя в ходе беседы.

## <a name="web-based-authentication-flow"></a>Поток проверки подлинности через Интернет

Используйте поток веб-проверки подлинности [для](~/tabs/what-are-tabs.md) вкладок и выберите его с помощью разговорных [ботов](~/bots/what-are-bots.md) или [расширений обмена сообщениями](~/messaging-extensions/what-are-messaging-extensions.md). Используйте [SDK Microsoft Teams JavaScript](/javascript/api/overview/msteams-client) на странице веб-контента, чтобы включить проверку подлинности. После включения проверки подлинности вставьте страницу содержимого во вкладку, страницу конфигурации или модуль задачи. Дополнительные сведения о потоке проверки подлинности на веб-основе см. в этой странице.

* [Добавление проверки подлинности в Teams бот](~/bots/how-to/authentication/add-authentication.md) описывает использование потока проверки подлинности на основе веб-данных с помощью диалогового бота.
* [Поток проверки подлинности на вкладке](~/tabs/how-to/authentication/auth-flow-tab.md) описывает работу проверки подлинности вкладок в Teams. Это показывает типичный поток проверки подлинности на веб-основе, используемый для вкладок.
* [Проверка подлинности Azure AD](~/tabs/how-to/authentication/auth-tab-AAD.md) на вкладке описывает подключение к Azure AD из вкладки в приложении в Teams.
* [Silent authentication Azure AD](~/tabs/how-to/authentication/auth-silent-AAD.md) описывает, как уменьшить количество подсказок для регистрации или согласия в приложении с помощью Azure AD.
* [.Net или C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [JavaScript или Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) предоставляет образцы для веб-проверки подлинности.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Поток OAuthPrompt для разговорных ботов

OAuthPrompt платформы Azure Bot Framework упрощает проверку подлинности для приложений с помощью ботов бесед. Используйте службу маркеров Azure Bot Framework для кэширования маркеров.

Дополнительные сведения об использовании OAuthPrompt см.:

* [Обзор потока проверки подлинности ботов](~/bots/how-to/authentication/auth-flow-bot.md) описывает работу проверки подлинности в боте в приложении в Teams. Это показывает не веб-поток проверки подлинности, используемый для ботов в Teams, настольном приложении и мобильных приложениях.
* [Проверка подлинности ботов](~/bots/how-to/authentication/add-authentication.md) описывает добавление проверки подлинности OAuth в Teams бота.

## <a name="code-sample"></a>Пример кода

предоставляет образец проверки подлинности бота v3 SDK.

| **Название примера** | **Описание** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Проверка подлинности ботов | В этом примере показано, как начать проверку подлинности в боте для Microsoft Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Tab, Bot and Messaging Extension (ME) SSO | В этом примере показаны SSO для tab, Bot и ME — поиск, действие, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | Недоступно |

## <a name="configure-the-identity-provider"></a>Настройка поставщика удостоверений

Независимо от потока проверки подлинности приложения настройте поставщика удостоверений для связи с Teams приложением. Большинство примеров и пройдите по ним, в основном, с использованием Azure AD в качестве поставщика удостоверений. Однако концепции применяются независимо от поставщика удостоверений.

Дополнительные сведения см. [в примере настройки поставщика удостоверений](~/concepts/authentication/configure-identity-provider.md).

## <a name="third-party-cookies-on-ios"></a>Сторонние файлы cookie на iOS

После обновления iOS 14 Apple заблокировала сторонний доступ к файлам [cookie](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/) для всех приложений по умолчанию. Поэтому приложения, которые используют сторонние файлы cookie для проверки подлинности в вкладке Channel или Chat и личные приложения, не смогут завершить свои процессы проверки подлинности на Teams клиентах iOS. Чтобы соответствовать требованиям конфиденциальности и безопасности, необходимо перейти к системе, основанной на маркерах, или использовать первопартийные файлы cookie для рабочего процесса проверки подлинности пользователей.

## <a name="see-also"></a>См. также

* [Проверка подлинности Microsoft Teams для вкладок](~/tabs/how-to/authentication/auth-flow-tab.md)
* [Поддержка единого входа для ботов](~/bots/how-to/authentication/auth-aad-sso-bots.md)
* [Добавление проверки подлинности в расширение для сообщений](~/messaging-extensions/how-to/add-authentication.md)
