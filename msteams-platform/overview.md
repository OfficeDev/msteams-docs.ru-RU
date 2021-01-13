---
title: Создание приложений для платформы Microsoft Teams
author: heath-hamilton
description: Получите обзор того, как разработчики могут расширить возможности Microsoft Teams с помощью пользовательских приложений.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 45be2dd7d0e421ac331cfc02703f0b81eab3dfe5
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797773"
---
# <a name="build-apps-for-microsoft-teams"></a>Создание приложений для Microsoft Teams

Приложения Microsoft Teams используют ключевую информацию, общие инструменты и доверенные процессы, в которые все чаще собираются, учитесь и работают люди.

Приложения — это то, как вы расширяете Teams в своих потребностях. Создайте что-то совершенно новое для Teams или интегрируем существующее приложение.

> [!div class="nextstepaction"]
> [Начните отсюда](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>Что такое приложения Teams?

Приложения Teams — это сочетание [возможностей и](concepts/capabilities-overview.md) [точек входа.](concepts/extensibility-points.md) Например, люди могут общаться в  чате с ботом (возможностью) вашего приложения в *канале* (точке входа).

Некоторые приложения простые (отправка уведомлений), а другие сложные (управление записями пациентов). При планировании приложения помните, что Teams — это центр совместной работы. Лучшие приложения Teams помогают людям самовыражаться и работать вместе.

:::row:::
   :::column span="":::

### <a name="tabs"></a>Вкладки

**Более удобный способ получения** информации: иногда требуется упростить поиск. Отображение важной веб-страницы [](tabs/what-are-tabs.md)на вкладке, которая обеспечивает полноэкранное веб-изображение для статического и динамического содержимого в Teams.

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Концептуальное представление вкладки в клиенте Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>Боты

**Превратить слова в действия:** беседы часто приводит к необходимости что-то делать (создать заказ, просмотреть мой код, проверить состояние билета и т. д.). Бот [может](bots/what-are-bots.md) прикатить эти типы рабочего процесса прямо в Teams.

:::image type="content" source="assets/images/overview-bots.png" alt-text="Концептуальное представление того, как боты выглядят в клиенте Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>Расширения для обмена сообщениями

**Упростить** многозадачи: с [](messaging-extensions/what-are-messaging-extensions.md)помощью расширений обмена сообщениями можно быстро обмениваться внешней информацией в беседе. Вы также можете действовать над сообщением, например создавать обращение в справку на основе содержимого публикации в канале.

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Концептуальное представление расширений обмена сообщениями в клиенте Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>веб-перехватчики

**Общение с внешними приложениями:** входящие [веб-hooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) — это простой способ автоматической отправки уведомлений из другого приложения в канал Teams. С [помощью исходяющих веб-hooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)сообщение веб-службы с помощью @mention.

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Концептуальное представление того, как выглядят соединители в клиенте Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph для Teams

**Использование данных Teams:** [API Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview) для Teams предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить функции для вашего приложения.

:::image type="content" source="assets/images/overview-graph.png" alt-text="Концептуальное представление API Microsoft Graph для Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>Начало построения

   Быстро ознакомьтесь с процессом создания для Teams, создав простое приложение и добавив некоторые часто используемые возможности.

   > [!div class="nextstepaction"]
   > [Создайте свое первое приложение сейчас](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Интеграция с Teams

   Смешивайте функции, которые нравится пользователям в существующем веб-приложении, службе или системе, с функциями совместной работы Teams.

   > [!div class="nextstepaction"]
   > [Интеграция существующего приложения](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>Небольшой код проходит длинный путь

   Для создания отличного приложения Teams не требуется быть экспертом-программистом. Попробуйте одно из нескольких решений с низким кодом.

   > [!div class="nextstepaction"]
   > [Создание приложения с низким кодом](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a>Ресурсы

* [Добавление кнопки "Поделиться в Teams" на веб-сайт](concepts/build-and-test/share-to-teams.md)
* <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Пользовательский интерфейс Fluent</a>
* [Microsoft Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Bot Framework SDK для JavaScript](https://github.com/Microsoft/botbuilder-js) и [Bot Framework SDK для .NET](https://github.com/Microsoft/botbuilder-dotnet/)
* [Публикация приложения в организации или AppSource](concepts/deploy-and-publish/overview.md)
