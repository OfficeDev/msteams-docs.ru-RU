---
title: Проверка подлинности пользователей приложения
description: Описание проверки подлинности в Teams и ее использования в приложениях
ms.topic: conceptual
keywords: AAD для проверки подлинности OAuth для SSO teams
ms.openlocfilehash: 88b2098b7d45444cf47bebdfccc22fae772b7c22
ms.sourcegitcommit: 843da1730443ff8474a05295f60a6b376ed140da
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2021
ms.locfileid: "50073105"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Проверка подлинности пользователей в Microsoft Teams

> [!NOTE]
> Для веб-проверки подлинности на мобильных клиентах требуется версия 1.4.1 или более поздней версии SDK JavaScript для Microsoft Teams.

Для доступа к сведениям пользователей, защищенным с помощью Azure Active Directory (AAD) и для доступа к данным из таких служб, как Facebook и Twitter, приложение устанавливает надежное соединение с этими поставщиками. Если приложение использует API Microsoft Graph в области действия пользователя, необходимо проверить подлинность пользователя, чтобы получить соответствующие маркеры проверки подлинности.

В Teams существует два разных потока проверки подлинности для приложения. Выполнение традиционного веб-потока проверки [](~/tabs/how-to/create-tab-pages/content-page.md) подлинности на странице контента, встроенной в вкладку, страницу конфигурации или модуль задачи. Если приложение содержит бота для беседы, используйте поток OAuthPrompt и при желании службу маркеров Azure Bot Framework для проверки подлинности пользователя в рамках беседы.

## <a name="web-based-authentication-flow"></a>Поток веб-проверки подлинности

Используйте веб-поток проверки [](~/tabs/what-are-tabs.md) подлинности для вкладок [](~/bots/what-are-bots.md) и выберите его для использования с ботами или [расширениями обмена сообщениями.](~/messaging-extensions/what-are-messaging-extensions.md) Используйте [клиентский SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client) на странице веб-контента, чтобы включить проверку подлинности. После включения проверки подлинности встраить страницу контента на вкладку, страницу конфигурации или модуль задачи. Дополнительные сведения о потоке веб-проверки подлинности см. в:

* [Добавление проверки подлинности в бот Teams](~/bots/how-to/authentication/add-authentication.md) описывает использование веб-потока проверки подлинности с ботом для беседы.
* [Поток проверки подлинности на вкладке](~/tabs/how-to/authentication/auth-flow-tab.md) описывает работу проверки подлинности вкладок в Teams. Здесь показан типичный веб-поток проверки подлинности, используемый для вкладок.
* [Проверка подлинности AAD](~/tabs/how-to/authentication/auth-tab-AAD.md) на вкладке описывает, как подключиться к AAD из вкладки в приложении в Teams.
* [AAD для проверки](~/tabs/how-to/authentication/auth-silent-AAD.md) подлинности в режиме тихой проверки подлинности описывает, как уменьшить количество входов или получения согласия в приложении с помощью AAD.
* [.Net, C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) или [JavaScript или Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) предоставляет примеры для веб-проверки подлинности.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Поток OAuthPrompt для ботов для бесед

OAuthPrompt платформы Azure Bot Framework упрощает проверку подлинности для приложений, использующих ботов для бесед. Используйте службу маркеров Azure Bot Framework для помощи в кэшинге маркеров.

Дополнительные сведения об использовании OAuthPrompt см. в:

* [Обзор потока проверки подлинности ботов](~/bots/how-to/authentication/auth-flow-bot.md) описывает работу проверки подлинности в боте в приложении в Teams. Здесь показан поток проверки подлинности не из Интернета, используемый для ботов в веб-приложениях Teams, классических приложениях и мобильных приложениях.
* [Проверка подлинности бота](~/bots/how-to/authentication/add-authentication.md) описывает добавление проверки подлинности OAuth в бот Teams.
* [.Net, C#](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) или [JavaScript или Node.js](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) предоставляет пример SDK для проверки подлинности ботов v3.

## <a name="configure-the-identity-provider"></a>Настройка поставщика удостоверений

Независимо от потока проверки подлинности приложения настройте поставщика удостоверений для взаимодействия с приложением Teams. Большинство примеров и по walkthroughs в основном связаны с использованием AAD в качестве поставщика удостоверений. Однако концепции применяются независимо от поставщика удостоверений.

Дополнительные сведения [см. в настройке поставщика удостоверений.](~/concepts/authentication/configure-identity-provider.md)
