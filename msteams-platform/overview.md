---
title: Создание приложений для Microsoft Teams платформы
author: heath-hamilton
description: Получите обзор того, как разработчики могут расширить Microsoft Teams с пользовательскими приложениями.
ms.topic: overview
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 8724b669476b11aa8cb1aca6d9586fc7ea42587d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566511"
---
# <a name="build-apps-for-microsoft-teams"></a>Создание приложений для Microsoft Teams

Microsoft Teams приложения приносят ключевую информацию, общие инструменты и доверенные процессы туда, где люди все чаще собираются, учатся и работают.

Приложения – это способ расширения Teams в соответствует вашим потребностям. Создайте что-то совершенно новое Teams или интегрируйте существующее приложение.

> [!div class="nextstepaction"]
> [Начните отсюда](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>Что такое Teams приложения?

Teams приложения представляет собой сочетание [возможностей и](concepts/capabilities-overview.md) [точек входа.](concepts/extensibility-points.md) Например, люди могут общаться с ботом вашего *приложения* (возможностью) в *канале* (точка входа).

Некоторые приложения просты (отправить уведомления), в то время как другие являются сложными (управлять записями пациентов). При планировании приложения помните, что Teams является центром совместной работы. Лучшие приложения Teams люди выражают себя и лучше работать вместе.

:::row:::
   :::column span="":::

### <a name="tabs"></a>Вкладки

**Получить информацию более удобно:** Иногда вам просто нужно сделать вещи проще найти. Отображение важной веб-страницы [в вкладке](tabs/what-are-tabs.md), которая обеспечивает полноэкранный веб-опыт для статического и динамического контента в Teams.

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Концептуальное представление о том, как выглядят вкладки в Teams клиента." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>Боты

**Превратите слова в действия:** Разговоры часто приводят к необходимости сделать что-то (создать заказ, просмотреть мой код, проверить статус билета, и так далее). Бот [может](bots/what-are-bots.md) начать такого рода рабочие процессы прямо внутри Teams.

:::image type="content" source="assets/images/overview-bots.png" alt-text="Концептуальное представление о том, как выглядят боты в Teams клиента." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>Расширения для система обмена сообщениями

**Упростите многозадачность: с расширением** обмена [сообщениями вы можете](messaging-extensions/what-are-messaging-extensions.md)быстро обмениваться внешней информацией в разговоре. Вы также можете действовать на сообщение, например, создание справки билет на основе содержания канала пост.

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Концептуальное представление о том, как выглядят расширения обмена сообщениями Teams клиента." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>веб-перехватчики

**Общайтесь с внешними** [приложениями: Входящие](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) веб-хуки являются простым способом автоматической отправки уведомлений из другого приложения Teams канал. С [исходящими webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), сообщение вашей веб-службы с @mention.

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Концептуальное представление о том, как выглядят разъемы в Teams клиента." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph для Teams

**Используйте Teams** данные: [API Microsoft Graph для Teams предоставляет](/graph/teams-concept-overview) доступ к информации о командах, каналах, пользователях и сообщениях, которые могут помочь вам создавать или улучшить функции для вашего приложения.

:::image type="content" source="assets/images/overview-graph.png" alt-text="Концептуальное представление API Microsoft Graph для Teams." border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>Начало строительства

Быстро ознакомитесь со созданием Teams, создав простое приложение.

> [!div class="nextstepaction"]
> [Создание первого приложения](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Интеграция с Teams

Смешайте функции, которые пользователи любят в существующем веб-приложении, сервисе или системе, с функциями совместной работы Teams.

> [!div class="nextstepaction"]
> [Интеграция существующего приложения](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>Маленький код проходит долгий путь

Вам не нужно быть экспертом программистом, чтобы построить большой Teams приложение. Попробуйте одно из нескольких решений с низким кодом.

> [!div class="nextstepaction"]
> [Создание приложения с низким кодом](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a>Получите идеи для вашего приложения

Ищете вдохновение для разработки приложений? Просмотрите наш список реальных сценариев и отраслевых решений с высокой точностью концепции макеты, чтобы понять различные способы Teams приложения могут помочь вашим пользователям.

> [!div class="nextstepaction"]
> [Посмотреть сценарии приложений](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>См. также

* [Добавьте кнопку «Поделиться Teams» на свой сайт](concepts/build-and-test/share-to-teams.md)
* [Создайте свое Teams приложение](concepts/design/design-teams-app-overview.md)
* [Microsoft Teams Клиент JavaScript SDK](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* Bot Framework SDK для [JavaScript](https://github.com/Microsoft/botbuilder-js) и [.NET](https://github.com/Microsoft/botbuilder-dotnet/)
* [Распространение приложения Teams с Teams](concepts/deploy-and-publish/apps-publish-overview.md)
