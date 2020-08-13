---
title: Платформа для разработчиков Teams
author: clearab
description: Общие сведения о том, как разработчики могут расширять и настраивать функции Microsoft Teams с помощью платформы Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d127acb33212f23dff9cf0dd83a1936044c10d5e
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652119"
---
# <a name="building-for-microsoft-teams"></a>Создание для Microsoft Teams

Приложения Microsoft Teams обеспечивают ключевые сведения, общие инструменты и надежные процессы, где люди все еще собирают, изученируют и работают.

Приложения — это то, как вы расширяете Teams в соответствии со своими потребностями. Вы можете создать новую фирменную символику для Teams или просто интегрировать функции в избранные приложения и службы.

## <a name="what-can-teams-apps-do"></a>Что могут делать приложения Teams?

Люди обнаруживают и используют приложения Teams через набор [возможностей](capabilities-overview.md)платформы.

Некоторые приложения просты (уведомления об отправке), а другие — сложным (Просмотр записей пациента). При планировании приложения помните, что Teams — это центр для совместной работы. Лучшие приложения Teams помогают людям выразить себя и лучше работают вместе.

### <a name="get-information-more-conveniently"></a>Более удобное получение информации

Иногда вам нужно просто упростить поиск. Отображение важной веб-страницы на [вкладке](doc-links/what-are-tabs.md), которая предоставляет полноэкранный веб-интерфейс для статического и динамического контента в Teams.

![Концептуальное представление вкладок, которые выглядят как в клиенте Teams.](doc-links/images/overview-tabs.png)

### <a name="share-links-without-switching-context"></a>Совместное использование ссылок без переключения контекста

Извлекать информацию в беседу и никогда не оставлять Teams. Например, с [расширениями обмена сообщениями](doc-links/what-are-messaging-extensions.md) вы можете поделиться богатыми и легко дижестибле контентом из внешней системы с помощью поля "Создание сообщения".

![Концептуальное представление расширений обмена сообщениями, которые выглядят как в клиенте Teams](doc-links\images\overview-messaging.png)

### <a name="turn-words-into-actions"></a>Включение слов в действия

Беседы часто приводят к необходимости выполнения каких-либо действий (создание заказа, просмотр кода и т. д.). С помощью [Bot](doc-links/what-are-bots.md) можно запускать эти рабочие процессы прямо в Teams.

![Концептуальное представление того, как боты выглядит в клиенте Teams](doc-links/images/overview-bots.png)

### <a name="communicate-with-external-apps-and-services"></a>Обмен данными с внешними приложениями и службами

[Входящие веб-перехватчики](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) это простой способ автоматически отправлять оповещения из другого приложения в канал команд или чат. С помощью [исходящих веб-перехватчиков](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks)вы можете отправить сообщение в веб-службу с помощью @mention.

![Концептуальное представление соединителей, имеющих вид в клиенте Teams.](doc-links/images/overview-connectors.png)

### <a name="utilize-teams-data"></a>Использование данных Teams

[REST API Microsoft Graph для Teams](https://docs.microsoft.com/graph/teams-concept-overview) предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить возможности приложения.

!["Концептуальное представление REST API Microsoft Graph для Teams](doc-links/images/overview-graph.png)
  
## <a name="start-building"></a>Начало создания

   Быстро ознакомьтесь со сборкой для Teams, создав простое приложение и добавив пару часто используемых возможностей.

   > [!div class="nextstepaction"]
   > [Создайте свое первое приложение сейчас](build-your-first-app/build-real-world-app.md)

### <a name="bring-it-all-together"></a>Совместное объединение

   Упрощение процессов и рабочих процессов для пользователей путем перехода к избранным веб-приложениям, службам и системам Организации с помощью функций совместной работы в Teams.

   > [!div class="nextstepaction"]
   > [Интеграция существующего приложения](doc-links/integrating-web-apps.md)

### <a name="trust-the-process"></a>Доверие процессу

   Узнайте, как весь процесс разработки платформы Teams для эффективного планирования, проектирования, построения и публикации приложения для вашей организации или для любого пользователя.

   > [!div class="nextstepaction"]
   > [Начало планирования приложения](doc-links/extensibility-points.md)

### <a name="no-code-no-worries"></a>Нет кода, нет проблем

   Вам не нужно быть программистом, чтобы создать отличное приложение. Создайте приложение Teams с минимальным количеством кода, используя платформу Microsoft Power.

   > [!div class="nextstepaction"]
   > [Импорт приложения Power Platform](doc-links/importing-custom-microsoft-apps.md)

## <a name="resources"></a>Ресурсы

* [Добавление на веб-сайт кнопки "общий доступ" в Teams](doc-links/share-to-teams.md)
* [Создание приложения с использованием рекомендуемых рекомендаций](doc-links/designing-overview.md)
* [Система дизайна пользовательского интерфейса Fluent](https://fluentsite.z22.web.core.windows.net/)
* [Пакет SDK для клиента Microsoft Teams JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)
* [Пакет SDK Bot Framework для JavaScript](https://github.com/Microsoft/botbuilder-js) и [пакет SDK для Bot Framework для .NET](https://github.com/Microsoft/botbuilder-dotnet/)
