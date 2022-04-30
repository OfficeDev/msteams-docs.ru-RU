---
title: Проверка подлинности пользователей приложения
description: Описывает проверку подлинности в Teams и способы ее использования в приложениях.
ms.topic: conceptual
ms.localizationpriority: high
keywords: вкладки проверка подлинности Teams OAuth SSO Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: f5aecf2791d03795229d3b37c5fc8784de992326
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111404"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Проверка подлинности пользователей в Microsoft Teams

> [!Note]
> Для веб-проверки подлинности на мобильных клиентах требуется версия 1.4.1 или более поздняя версия пакета SDK клиента Teams JavaScript.

Чтобы получить доступ к пользовательским сведениям, защищенным Azure AD, и получить доступ к данным из таких служб, как Facebook и Twitter, приложение устанавливает доверенное соединение с этими поставщиками. Если приложение использует API-интерфейсы Microsoft Graph в области пользователя, выполните проверку подлинности пользователя, чтобы получить соответствующие токены проверки подлинности.

В Teams для приложения существует два разных потока проверки подлинности. Выполните традиционный поток проверки подлинности через Интернет на [странице содержимого](~/tabs/how-to/create-tab-pages/content-page.md), встроенной во вкладку, страницу конфигурации или модуль задачи. Если приложение содержит бот бесед, используйте поток OAuthPrompt и при желании службу маркеров Azure Bot Framework для проверки подлинности пользователя в ходе беседы.

## <a name="web-based-authentication-flow"></a>Поток проверки подлинности через Интернет

Используйте поток проверки подлинности через Интернет для [вкладок](~/tabs/what-are-tabs.md) и выберите его использование с[ ботами бесед](~/bots/what-are-bots.md) или [расширениями сообщений](~/messaging-extensions/what-are-messaging-extensions.md). Испоьзуйте пакет [SDK клиента Microsoft Teams JavaScript](/javascript/api/overview/msteams-client) на странице веб-материалов, чтобы включить проверку подлинности. После включения проверки подлинности вставьте страницу содержимого во вкладку, страницу конфигурации или модуль задачи. Дополнительные сведения о потоке веб-проверки подлинности в следующих разделах:

* [Добавление проверки подлинности в бот Teamss](~/bots/how-to/authentication/add-authentication.md) описывает, как использовать поток проверки подлинности через Интернет с ботом беседы.
* [Поток проверки подлинности на вкладках](~/tabs/how-to/authentication/auth-flow-tab.md) описывает, как работает проверка подлинности на вкладках в Teams. Здесь показан типичный веб-поток проверки подлинности, используемый для вкладок.
* [Проверка подлинности Azure AD на вкладках](~/tabs/how-to/authentication/auth-tab-AAD.md) описывает, как подключиться к Azure AD из вкладки в приложении в Teams.
* [Автоматическая проверка подлинности Azure AD](~/tabs/how-to/authentication/auth-silent-AAD.md) описывает, как уменьшить количество запросов на вход или согласие в приложении, использующем Azure AD.
* [.Net, C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp), [JavaScript или Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) предоставляют образцы для веб-проверки подлинности.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Поток OAuthPrompt для ботов беседы

OAuthPrompt платформы Azure Bot Framework упрощает проверку подлинности для приложений с помощью ботов бесед. Используйте службу маркеров Azure Bot Framework для кэширования маркеров.

Подробнее об использовании OAuthPrompt см.:

* [Обзор процесса проверки подлинности бота](~/bots/how-to/authentication/auth-flow-bot.md) описывает, как проверка подлинности работает в боте в приложении в Teams. Здесь показан поток проверки подлинности без веб-интерфейса, используемый для ботов в веб-приложениях, настольных и мобильных приложениях Teams.
* [Проверка подлинности бота](~/bots/how-to/authentication/add-authentication.md) описывает, как добавить проверку подлинности OAuth в бот Teams.

## <a name="code-sample"></a>Пример кода

предоставляет образец пакета SDK для проверки подлинности бота v3.

| **Название примера** | **Описание** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Проверка подлинности бота | В этом примере показано, как начать работу с проверкой подлинности в боте для Microsoft Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Вкладка, бот и расширение сообщений (ME) SSO | В этом примере показана система единого входа для Tab, Bot и ME — поиск, действие, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | Недоступно |

## <a name="configure-the-identity-provider"></a>Настройка поставщика удостоверений

Независимо от потока проверки подлинности приложения настройте поставщика удостоверений для связи с приложением Teams. Большинство примеров и пошаговых инструкций касаются использования Azure AD в качестве поставщика удостоверений. Однако концепции применяются независимо от поставщика удостоверений.

Подробнее в статье [Настройка поставщика удостоверений](~/concepts/authentication/configure-identity-provider.md).

## <a name="third-party-cookies-on-ios"></a>Сторонние файлы cookie на iOS

После обновления iOS 14 Apple по умолчанию заблокировала доступ [сторонних файлов cookie](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/) для всех приложений. Таким образом, приложения, использующие сторонние файлы cookie для проверки подлинности на вкладках канала или чата, а также в личных приложениях, не смогут выполнять свои рабочие процессы проверки подлинности на клиентах Teams iOS. Чтобы соответствовать требованиям конфиденциальности и безопасности, вы должны перейти на систему на основе токенов или использовать собственные файлы cookie для рабочих процессов проверки подлинности пользователей.

## <a name="see-also"></a>Дополнительные ресурсы

* [Проверка подлинности Microsoft Teams для вкладок](~/tabs/how-to/authentication/auth-flow-tab.md)
* [Поддержка единого входа для ботов](~/bots/how-to/authentication/auth-aad-sso-bots.md)
* [Добавление проверки подлинности в расширение для сообщений](~/messaging-extensions/how-to/add-authentication.md)
