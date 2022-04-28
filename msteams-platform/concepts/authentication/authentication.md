---
title: Проверка подлинности пользователей приложения
description: Описывает проверку подлинности в Teams и способы ее использования в приложениях
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Проверка подлинности teams OAuth SSO Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 811b8917297ad8fe1420f4887983b93f43cd73b3
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103960"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Проверка подлинности пользователей в Microsoft Teams

> [!Note]
> Для веб-проверки подлинности на мобильных клиентах требуется версия 1.4.1 или более поздняя Teams пакета SDK клиента JavaScript.

Чтобы получить доступ к сведениям о пользователях, защищенных с помощью Azure AD, и получить доступ к данным из таких служб, как Facebook и Twitter, приложение устанавливает надежное подключение к этим поставщикам. Если приложение использует API microsoft Graph в области пользователя, выполните проверку подлинности пользователя, чтобы получить соответствующие маркеры проверки подлинности.

В Teams есть два разных потока проверки подлинности для приложения. Выполнение традиционного веб-потока проверки подлинности на странице [](~/tabs/how-to/create-tab-pages/content-page.md) содержимого, внедренной на вкладку, страницу конфигурации или модуль задачи. Если приложение содержит бот бесед, используйте поток OAuthPrompt и при желании службу маркеров Azure Bot Framework для проверки подлинности пользователя в ходе беседы.

## <a name="web-based-authentication-flow"></a>Поток проверки подлинности через Интернет

Используйте веб-поток проверки подлинности для [вкладок](~/tabs/what-are-tabs.md) и выберите его для использования с [](~/bots/what-are-bots.md) чат-ботами или [расширениями сообщений](~/messaging-extensions/what-are-messaging-extensions.md). Используйте пакет [SDK Microsoft Teams JavaScript](/javascript/api/overview/msteams-client) на странице веб-содержимого, чтобы включить проверку подлинности. После включения проверки подлинности вставьте страницу содержимого во вкладку, страницу конфигурации или модуль задачи. Дополнительные сведения о веб-потоке проверки подлинности см. в следующих статьях:

* [Добавление проверки подлинности в Teams бота](~/bots/how-to/authentication/add-authentication.md) описывает использование веб-потока проверки подлинности с ботом беседы.
* [Поток проверки подлинности на вкладке](~/tabs/how-to/authentication/auth-flow-tab.md) описывает, как работает проверка подлинности на вкладке в Teams. Здесь показан типичный веб-поток проверки подлинности, используемый для вкладок.
* [Проверка подлинности Azure AD](~/tabs/how-to/authentication/auth-tab-AAD.md) на вкладке описывает, как подключиться к Azure AD из вкладки в приложении Teams.
* [Автоматическая проверка подлинности Azure AD](~/tabs/how-to/authentication/auth-silent-AAD.md) описывает, как уменьшить количество запросов на вход или согласие в приложении с помощью Azure AD.
* [.Net, C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) , [JavaScript или Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) предоставляет примеры для веб-проверки подлинности.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Поток OAuthPrompt для чат-ботов

OAuthPrompt платформы Azure Bot Framework упрощает проверку подлинности для приложений с помощью ботов бесед. Используйте службу маркеров Azure Bot Framework для кэширования маркеров.

Дополнительные сведения об использовании OAuthPrompt см. в следующих статьях:

* [Обзор потока проверки подлинности](~/bots/how-to/authentication/auth-flow-bot.md) бота описывает, как работает проверка подлинности в боте в приложении в Teams. Здесь показан не веб-поток проверки подлинности, используемый для ботов в веб-Teams, классических приложениях и мобильных приложениях.
* [Проверка подлинности бота](~/bots/how-to/authentication/add-authentication.md) описывает добавление проверки подлинности OAuth в Teams бота.

## <a name="code-sample"></a>Пример кода

предоставляет пример пакета SDK для проверки подлинности бота версии 3.

| **Название примера** | **Описание** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Проверка подлинности бота | В этом примере показано, как приступить к проверке подлинности в боте для Microsoft Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Единый вход табуляции, бота и расширения сообщений (ME) | В этом примере показан единый вход для Tab, Bot и ME — поиск, действие, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | Недоступно |

## <a name="configure-the-identity-provider"></a>Настройка поставщика удостоверений

Независимо от потока проверки подлинности приложения настройте поставщик удостоверений для взаимодействия с Teams приложения. Большинство примеров и пошаговые инструкции в основном предназначены для использования Azure AD в качестве поставщика удостоверений. Однако эти понятия применяются независимо от поставщика удостоверений.

Дополнительные сведения см. [в статье о настройке поставщика удостоверений](~/concepts/authentication/configure-identity-provider.md).

## <a name="third-party-cookies-on-ios"></a>Сторонние файлы cookie в iOS

После обновления iOS 14 Apple по умолчанию заблокируют сторонний доступ к файлам [cookie](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/) для всех приложений. Таким образом, приложения, использующие сторонние файлы cookie для проверки подлинности на вкладке "Канал" или "Чат" и "Личные приложения", не смогут выполнять рабочие процессы проверки подлинности на Teams iOS. Чтобы обеспечить соответствие требованиям к конфиденциальности и безопасности, необходимо перейти в систему на основе маркеров или использовать файлы cookie от первого производителя для рабочих процессов проверки подлинности пользователей.

## <a name="see-also"></a>См. также

* [Проверка подлинности Microsoft Teams для вкладок](~/tabs/how-to/authentication/auth-flow-tab.md)
* [Поддержка единого входа для ботов](~/bots/how-to/authentication/auth-aad-sso-bots.md)
* [Добавление проверки подлинности в расширение сообщения](~/messaging-extensions/how-to/add-authentication.md)
