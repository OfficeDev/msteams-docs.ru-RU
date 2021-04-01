---
title: Создание приложений для платформы Microsoft Teams
author: heath-hamilton
description: Сведения о том, как разработчики могут расширять функции Microsoft Teams с помощью настраиваемого приложения.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e40d2b0d8b0d12e6275b97f79d103310d22f9720
ms.sourcegitcommit: 3bd2627b7a334568f61ccc606395e3d89aa521d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475930"
---
# <a name="build-apps-for-microsoft-teams"></a>Создание приложений для Microsoft Teams

Приложения Microsoft Teams приносят ключевые сведения, общие инструменты и доверенные процессы в места, где люди все чаще собираются, учатся и работают.

Приложения — это то, как вы расширяете Teams, чтобы соответствовать вашим потребностям. Создайте что-то совершенно новое для Teams или интегрируете существующее приложение.

> [!div class="nextstepaction"]
> [Начните отсюда](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>Что такое приложения Teams?

Приложения teams — это сочетание [возможностей и](concepts/capabilities-overview.md) [точек входа.](concepts/extensibility-points.md) Например, люди могут общаться с  ботом (возможностью) вашего приложения в *канале* (точка входа).

Некоторые приложения просты (отправка уведомлений), а другие сложны (управление записями пациентов). При планировании приложения помните, что Teams — это центр совместной работы. Лучшие приложения Teams помогают людям лучше выражать себя и работать вместе.

:::row:::
   :::column span="":::

### <a name="tabs"></a>Вкладки

**Получите сведения более удобно.** Иногда вам просто нужно упростить поиск. Отображение важной веб-страницы [](tabs/what-are-tabs.md)на вкладке, которая обеспечивает полноэкранный веб-опыт для статического и динамического контента в Teams.

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Концептуальное представление о том, как выглядят вкладки в клиенте Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>Боты

**Превратите** слова в действия: беседы часто приводит к необходимости что-то делать (создать заказ, просмотреть код, проверить состояние билета и т.д.). Бот [может](bots/what-are-bots.md) скинуть эти типы рабочего процесса прямо внутри Teams.

:::image type="content" source="assets/images/overview-bots.png" alt-text="Концептуальное представление того, как выглядят боты в клиенте Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>Расширения для система обмена сообщениями

**Упростите многозадачную** работу. [С](messaging-extensions/what-are-messaging-extensions.md)помощью расширений обмена сообщениями можно быстро обмениваться внешней информацией в беседе. Вы также можете действовать по сообщению, например, создать билет справки на основе контента сообщения канала.

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Концептуальное представление о том, как выглядят расширения обмена сообщениями в клиенте Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>Веб-перехватчики

**Связь с внешними приложениями.** [Входящие веб-сайты](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) — это простой способ автоматической отправки уведомлений из другого приложения в канал Teams. В [исходяющих веб-сайтах](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)сообщение веб-службы с помощью @mention.

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Концептуальное представление того, как выглядят соединители в клиенте Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph для teams

**Использование данных Teams.** [API Microsoft Graph для Teams](https://docs.microsoft.com/graph/teams-concept-overview) предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить функции для вашего приложения.

:::image type="content" source="assets/images/overview-graph.png" alt-text="Концептуальное представление API Microsoft Graph для Teams." border="false":::

   :::column-end:::
   :::column span="":::

:::row:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

## <a name="build-solutions-for-microsoft-teams-apps"></a>Создание решений для приложений Microsoft Teams
 
Корпорация Майкрософт предлагает книгу extensibility look , библиотеку сценариев для приложений Teams, организованных промышленностью. Эта книга помогает создавать приложения на платформе Teams и понимать различные возможные сценарии с помощью различных возможностей платформы Teams. Сценарии книги look начинаются с бизнес-проблемы, лиц, вовлеченных вместе со своими проблемами, и заканчиваются решением приложения Teams для решения бизнес-потребностей.

Каждый сценарий в этой библиотеке сопровождается набором макетов концепции проектирования высокой верности, которые могут служить вдохновением для разработки приложений и улучшения пользовательского интерфейса. Кроме того, в книге "Внешний вид" освещаются лучшие практики проектирования и архитектуры при создании каждого приложения. Дополнительные сведения см. в книге extensibility look. Дополнительные сведения см. [в книге extensibility look book.](https://adoption.microsoft.com/extensibility-look-book/scenarios/) 

## <a name="start-building"></a>Начало создания

Быстро ознакомьтесь со зданием для Teams, создав простое приложение и добавив некоторые часто используемые возможности.

> [!div class="nextstepaction"]
> [Создайте свое первое приложение сейчас](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Интеграция с Teams

Сочетание функций, которые пользователи любят в существующем веб-приложении, службе или системе, с функциями совместной работы Teams.

> [!div class="nextstepaction"]
> [Интеграция существующего приложения](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>Маленький код проходит долгий путь

Вам не нужно быть программистом-экспертом, чтобы создать отличное приложение Teams. Попробуйте одно из нескольких решений с низким кодом.

> [!div class="nextstepaction"]
> [Создание приложения с низким кодом](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a>Ресурсы

* [Добавление кнопки Share-to-Teams на веб-сайт](concepts/build-and-test/share-to-teams.md)
* [Разработка приложения Teams](concepts/design/design-teams-app-overview.md)
* [Клиент Microsoft Teams JavaScript SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* Bot Framework SDK для [JavaScript](https://github.com/Microsoft/botbuilder-js) и [.NET](https://github.com/Microsoft/botbuilder-dotnet/)
* [Публикация приложения Teams](concepts/deploy-and-publish/overview.md)
