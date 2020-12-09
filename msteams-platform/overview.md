---
title: Создание приложений для платформы Microsoft Teams
author: heath-hamilton
description: Общие сведения о том, как разработчики могут расширять и настраивать функции Microsoft Teams с помощью настраиваемых приложений.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 6f5f3454885320669ef42383529d39fcfcfdfee8
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604789"
---
# <a name="build-apps-for-microsoft-teams"></a>Создание приложений для Microsoft Teams

Приложения Microsoft Teams обеспечивают ключевые сведения, общие инструменты и надежные процессы, где люди все еще собирают, изученируют и работают.

Приложения — это то, как вы расширяете Teams в соответствии со своими потребностями. Создание новой фирменной символики для Teams или интеграция существующего приложения.

> [!div class="nextstepaction"]
> [Начните отсюда](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>Что такое приложения Teams?

Приложения Teams представляют собой сочетание [возможностей](concepts/capabilities-overview.md) и [точек входа](concepts/extensibility-points.md). Например, люди могут общаться с *роботом* приложения (возможностями) в *канале* (точке входа).

Некоторые приложения просты (уведомления об отправке), а другие — сложными (Управление записями пациента). При планировании приложения помните, что Teams — это центр для совместной работы. Лучшие приложения Teams помогают людям выразить себя и лучше работают вместе.

:::row:::
   :::column span="":::

### <a name="tabs"></a>Вкладки

**Более удобное для получения сведений**: иногда вам нужно просто упростить поиск. Отображение важной веб-страницы на [вкладке](tabs/what-are-tabs.md), которая предоставляет полноэкранный веб-интерфейс для статического и динамического контента в Teams.

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Концептуальное представление вкладок, которые выглядят как в клиенте Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a>расширения для обмена сообщениями;

**Упрощение задач**: благодаря [расширениям обмена сообщениями](messaging-extensions/what-are-messaging-extensions.md)вы можете быстро поделиться внешними сведениями в беседе. Кроме того, можно выполнить действия с сообщением, например создать билет справки на основе контента канала POST.

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Концептуальное представление расширений обмена сообщениями в клиенте Teams выглядит как." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a>Боты

**Включение слов в действия**: беседы часто приводят к необходимости выполнять какие-либо действия (создание заказа, просмотр кода, проверка состояния билета и т. д.). С помощью [Bot](bots/what-are-bots.md) можно запускать эти рабочие процессы прямо в Teams.

:::image type="content" source="assets/images/overview-bots.png" alt-text="Концептуальное представление того, как боты выглядит в клиенте Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a>веб-перехватчики

**Обмен данными с внешними приложениями**: [Входящие веб-перехватчики](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) это простой способ автоматически отправлять уведомления из другого приложения в канал Teams. С [исходящими веб-перехватчиками](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)запросите у веб-службы @mention.

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Концептуальное представление соединителей, имеющих вид в клиенте Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph для Teams

**Использование данных Teams**: [API Microsoft Graph для Teams](https://docs.microsoft.com/graph/teams-concept-overview) предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить возможности приложения.

:::image type="content" source="assets/images/overview-graph.png" alt-text="Концептуальное представление API Microsoft Graph для Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a>Начало работы

Приступите к работе с нашими первыми приложениями и Узнайте, как интегрировать и импортировать существующие приложения.

:::row:::
   :::column span="2":::

### <a name="start-building"></a>Начало создания

   Быстро ознакомьтесь со сборкой для Teams, создав простое приложение и добавив некоторые часто используемые возможности.

   > [!div class="nextstepaction"]
   > [Создайте свое первое приложение сейчас](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a>Интеграция с Teams

   Функция смешения пользователи любовь о существующем веб-приложении, службе или системе с функциями совместной работы Teams.

   > [!div class="nextstepaction"]
   > [Интеграция существующего приложения](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a>Небольшой код проходит много времени

   Вам не нужно быть экспертным программистом, чтобы создать удобное приложение Teams. Попробуйте одно из нескольких решений с небольшим кодом.

   > [!div class="nextstepaction"]
   > [Создание приложения с небольшим кодом](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="resources"></a>Ресурсы

* [Добавление на веб-сайт кнопки "общий доступ" в Teams](concepts/build-and-test/share-to-teams.md)
* <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Пользовательский интерфейс Fluent</a>
* [Пакет SDK для клиента Microsoft Teams JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Пакет SDK Bot Framework для JavaScript](https://github.com/Microsoft/botbuilder-js) и [пакет SDK для Bot Framework для .NET](https://github.com/Microsoft/botbuilder-dotnet/)
* [Публикация приложения в организации или AppSource](concepts/deploy-and-publish/overview.md)
