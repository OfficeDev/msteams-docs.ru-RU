---
title: Предварительные требования
author: surbhigupta
description: Каждая вкладка в Microsoft Teams должна соответствовать этим требованиям.
keywords: команды вкладки группового канала настраиваются
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: fe72691465ca785cefb6a96c8eb4005a64601a17
ms.sourcegitcommit: 3dc9b539c6f7fbfb844c47a78e3b4d2200dabdad
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/31/2022
ms.locfileid: "64571518"
---
# <a name="prerequisites"></a>Предварительные требования

Убедитесь, что вы придерживались следующих предварительных условий при создании личной Teams или вкладки канала или группы:

* Разрешить обнаружение страниц вкладок в iFrame с помощью заглавных таблиц http-ответов X-Frame-Options и Content-Security-Policy HTTP.
  * Установите заглавную: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Для совместимости Internet Explorer 11 установите `X-Content-Security-Policy`.
  * Поочередно установите заглавную .`X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` Этот заголовок является обесценим, но по-прежнему принимается большинством браузеров.

* Страницы входа не отрисовка в iFrames, как защита от clickjacking. Логике проверки подлинности необходимо использовать метод, не перенаправление. Например, используйте проверку подлинности на основе маркеров или файлов cookie.

    > [!NOTE]
    > Рекомендуется установить предназначенное использование для файлов cookie, а не полагаться на поведение браузера по умолчанию. Дополнительные сведения см. в [атрибуте cookie SameSite](../../resources/samesite-cookie-update.md).

* Ограничение политики браузеров одного и того же происхождения не позволяет веб-страницам делать запросы в различные домены, чем обслуживаемая веб-страница. Таким образом, вы можете перенаправить конфигурацию или страницу контента в другой домен или поддомен. Логика навигации `validDomains` между доменами должна позволить клиенту Teams проверить происхождение со статическим списком в манифесте приложения при загрузке или общении с вкладкой.

* Стиль вкладок на основе Teams темы, дизайна и намерения клиента. Вкладки лучше всего работают, когда они построены для решения определенных потребностей и фокуса на небольшом наборе задач или подмножество данных, которые имеют отношение к расположению канала вкладки.

* На своей странице контента добавьте ссылку на Microsoft Teams [клиента JavaScript с](/javascript/api/overview/msteams-client) помощью тегов скриптов. После загрузки страницы сделайте вызов `microsoftTeams.initialize()`, в противном случае страница не отображается.

* Для проверки подлинности для мобильных клиентов необходимо обновить Teams JavaScript SDK 1.4.1 и более поздней.

* Если вы хотите, чтобы вкладка канала или группы Teams мобильном клиенте, `setSettings()` конфигурация должна иметь значение для `websiteUrl` свойства.

* Microsoft Teams поддерживает возможность загрузки веб-сайтов интрасети с самозаверяемой подписью.

## <a name="tools-to-build-tabs"></a>Инструменты для создания вкладок

| &nbsp; | Установка | Для использования... |
| --- | --- | --- |
| **Required** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | Среда запуска JavaScript с задней среду. Используйте последний выпуск LTS v14.|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge) (рекомендуется) или [Google Chrome](https://www.google.com/chrome/) | Браузер с средствами разработчика. |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | Среды сборки JavaScript, TypeScript или SharePoint Framework (SPFx) |
| &nbsp; | [Visual Studio 2019](https://visualstudio.com/download) г **., ASP.NET и веб-разработки** или рабочей нагрузки на межплатформу **.NET Core** | .NET. Вы можете установить бесплатное издание сообщества Visual Studio 2019. |
| &nbsp; | [Git](https://git-scm.com/downloads) | Git для использования репо примера приложений из GitHub. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app) | Microsoft Teams сотрудничать со всеми, с чем вы работаете, с помощью приложений для чата, собраний, зовов — все в одном месте. |
| &nbsp; | [ngrok](https://ngrok.com/download) | Ngrok — это средство обратного прокси-программного обеспечения. Ngrok создает туннель для общедоступных конечных точек HTTPS локального веб-сервера. Веб-точки сервера доступны во время текущего сеанса на компьютере. Когда компьютер выключен или заснул, служба перестает быть доступной. |
| &nbsp; | [Портал разработчика Teams](https://dev.teams.microsoft.com/) | Веб-портал для настройки, управления и распространения Teams в том числе в организации или Teams магазине. |

### <a name="build-your-teams-tab"></a>Создание вкладки Teams

Теперь давайте построим вкладку. Но сначала выберите выбор вкладки для создания:

> [!div class="nextstepaction"]
> [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
> [!div class="nextstepaction"]
> [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>См. также

* [Teams вкладки](~/tabs/what-are-tabs.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)