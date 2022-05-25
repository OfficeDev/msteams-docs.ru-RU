---
title: Предварительные требования
author: surbhigupta
description: Каждая вкладка в Microsoft Teams должна соответствовать этим требованиям.
keywords: настраиваемый канал группы вкладок Teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 92b03146200af978f3fa5d6dc2c5e6ad27a12200
ms.sourcegitcommit: 929391b6c04d53ea84a93145e2f29d6b96a64d37
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2022
ms.locfileid: "65672931"
---
# <a name="prerequisites"></a>Предварительные требования

Соблюдайте указанные ниже предварительные требования при создании личных вкладок, вкладок каналов или групповых вкладок Teams.

* Разрешите обнаружение страниц вашей вкладки в iFrame с помощью заголовков HTTP-отклика X-Frame-Options и Content-Security-Policy.
  * Настройте заголовок: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Для совместимости с Internet Explorer 11 настройте `X-Content-Security-Policy`
  * Или настройте заголовок `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`. Этот заголовок является устаревшим, но по-прежнему принимается большинством браузеров.

* Страницы входа не отображаются в iFrames в качестве меры защиты от кликджекинга. Ваша логика проверки подлинности должна использовать метод, отличный от перенаправления. Например, используйте проверку подлинности на основе маркеров или файлов cookie.

    > [!NOTE]
    > Рекомендуется настроить использование файлов cookie в явном виде, а не полагаться на поведение браузера по умолчанию. Дополнительные сведения см. в статье [Атрибут cookie-файла SameSite](../../resources/samesite-cookie-update.md).

* Ограничение политики одинакового источника браузеров запрещает веб-страницам выполнять запросы к доменам, отличным от обслуживаемой веб-страницы. Поэтому вы можете перенаправить страницу конфигурации или содержимого в другой домен или поддомен. Ваша логика навигации между доменами должна позволять клиенту Teams проверить источник на соответствие статическому списку `validDomains` в манифесте приложения при загрузке или взаимодействии со вкладкой.

* Создайте стиль вкладок на основе темы, дизайна и назначения клиента Teams. Вкладки лучше всего работают, когда они создаются для решения конкретных потребностей и сфокусированы на небольшом наборе задач или подмножестве данных, относящихся к расположению канала вкладки.

* На странице содержимого добавьте ссылку на [клиентский пакет SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client) с помощью тегов сценариев. После загрузки страницы выполните вызов `app.initialize()`, в противном случае страница не будет отображаться.

* Для проверки подлинности на мобильных клиентах необходимо перейти на SDK JavaScript для Teams 1.4.1 или более поздней версии.

* Если вы выбрали вариант отображения вкладки канала или группы в мобильном клиенте Teams, конфигурация `setConfig()` должна содержать значение для свойства `websiteUrl`.

* Microsoft Teams не поддерживает возможность загрузки веб-сайтов интрасети, использующих самозаверяющие сертификаты.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="tools-to-build-tabs"></a>Инструменты для создания вкладок

| &nbsp; | Установка | Для использования... |
| --- | --- | --- |
| **Required** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | Серверной среды выполнения JavaScript. Используйте последнюю версию версии 16 LTS.|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge) (рекомендуется) или [Google Chrome](https://www.google.com/chrome/) | Браузера со средствами разработчика. |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download); | Сред сборки JavaScript, TypeScript или SharePoint Framework (SPFx). |
| &nbsp; | Рабочая нагрузка [Visual Studio 2019](https://visualstudio.com/download), **ASP.NET и веб-разработки** или **кроссплатформенной разработки .NET Core** | .NET. Вы можете установить бесплатный выпуск Visual Studio Community 2019. |
| &nbsp; | [Git](https://git-scm.com/downloads) | Git для применения репозитория примеров приложений из GitHub. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app) | Microsoft Teams для взаимодействия в одном месте со всеми пользователями, с которыми вы работаете, с помощью приложений для чата, собраний и звонков. |
| &nbsp; | [ngrok](https://ngrok.com/download) | Ngrok — это программное средство обратного прокси-сервера. Ngrok создает туннель для общедоступных конечных точек HTTPS локального веб-сервера. Конечные веб-точки вашего сервера доступны во время текущего сеанса на компьютере. Когда компьютер выключается или переходит в спящий режим, служба становится недоступной. |
| &nbsp; | [Портал разработчика Teams](https://dev.teams.microsoft.com/) | Веб-портала для настройки, управления и распространения приложений Teams, в том числе в вашей организации или магазине Teams. |

### <a name="build-your-teams-tab"></a>Создание вкладки Teams

Теперь давайте создадим вкладку. Но сначала выберите вкладку для создания:

> [!div class="nextstepaction"]
> [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
> [!div class="nextstepaction"]
> [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)