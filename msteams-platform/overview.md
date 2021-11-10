---
title: Создание приложений для Microsoft Teams платформы
author: heath-hamilton
description: Сведения о том, как разработчики могут расширять Microsoft Teams с помощью настраиваемого приложения.
ms.topic: overview
ms.localizationpriority: medium
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: 878b6fd22373edb8f9cbbf28c15c8d5dd10ee3e0
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888036"
---
# <a name="build-apps-for-microsoft-teams"></a>Создание приложений для Microsoft Teams

Microsoft Teams приложения приносят ключевые сведения, общие инструменты и доверенные процессы в места, где люди все чаще собираются, учатся и работают.

Приложения — это то, как Teams, чтобы соответствовать вашим потребностям. Создайте что-то новое для Teams или интегрируете существующее приложение.

> [!div class="nextstepaction"]
> [Начните отсюда](get-started/get-started-overview.md)

## <a name="what-are-teams-apps"></a>Что такое Teams приложения?

Teams приложения — это сочетание [возможностей.](concepts/capabilities-overview.md) Некоторые приложения просты (отправка уведомлений), а другие сложны (управление записями пациентов). При планировании приложения помните, что Teams является концентратором совместной работы. Лучшие Teams помогают людям лучше выражать себя и работать вместе.

### <a name="personal-apps"></a>Персональные приложения

:::row:::
   :::column span="1":::

**Помощь людям в фокусе:** [личное](concepts/design/personal-apps.md) приложение — это выделенное пространство или бот, чтобы помочь пользователям сосредоточиться на своих задачах или просмотреть важные для них действия.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-personal-apps-2021.png" alt-text="Концептуальное представление того, как личные приложения выглядят в Teams клиенте." border="false":::

   :::column-end:::

:::row-end:::

### <a name="tabs"></a>Вкладки

:::row:::
   :::column span="1":::

**Совместное взаимодействие более удобно:** отображение веб-контента на вкладке, на которой пользователи могут совместно обсуждать и работать над ними. [](tabs/what-are-tabs.md)

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-channel-chat-apps-2021.png" alt-text="Концептуальное представление того, как выглядят вкладки в Teams клиенте." border="false":::

   :::column-end:::

:::row-end:::

### <a name="bots"></a>боты;

:::row:::
   :::column span="1":::

**Превратите** слова в действия: беседы часто приводит к необходимости что-то делать (создать заказ, просмотреть код, проверить состояние билета и так далее). Бот [может](bots/what-are-bots.md) скинуть эти типы рабочего процесса прямо внутри Teams.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-bots-2021.png" alt-text="Концептуальное представление того, как выглядят боты в Teams клиенте." border="false":::

   :::column-end:::

:::row-end:::

### <a name="messaging-extensions"></a>расширения для обмена сообщениями;

:::row:::

   :::column span="1":::

**Упростите многозадачную** работу. [С](messaging-extensions/what-are-messaging-extensions.md)помощью расширений обмена сообщениями можно быстро обмениваться внешней информацией в беседе. Вы также можете действовать по сообщению, например, создать билет справки на основе контента сообщения канала.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-messaging-extensions-2021.png" alt-text="Концептуальное представление о том, как выглядят расширения обмена сообщениями в Teams клиенте." border="false":::

   :::column-end:::
:::row-end:::

### <a name="meeting-extensions"></a>Расширения для собраний

:::row:::

   :::column span="1":::

**Создание приложений для собраний.** Существует несколько вариантов включения приложения в Teams [звонков.](apps-in-teams-meetings/design/designing-apps-in-meetings.md)

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-meeting-extensions-2021.png" alt-text="Концептуальное представление о том, как выглядят расширения собраний в Teams клиенте." border="false":::

   :::column-end:::
:::row-end:::

### <a name="webhooks-and-connectors"></a>Веб-перехватчики и соединительные линии

:::row:::

   :::column span="":::

**Связь с внешними** приложениями. [Входящие веб-сайты](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) — это простой способ автоматической отправки уведомлений из другого приложения на Teams канал. В [исходяющих веб-сайтах](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)сообщение веб-службы с помощью @mention.

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Концептуальное представление о том, как выглядят соединители в Teams клиенте." border="false":::

   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph для Teams

:::row:::

   :::column span="":::

**Использование Teams** данных. [API microsoft Graph](/graph/teams-concept-overview) для Teams предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить функции для вашего приложения (например, богатые уведомления).

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-graph.png" alt-text="Концептуальное представление API microsoft Graph для Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>Начало создания

Быстро ознакомьтесь с созданием для Teams, настроив среду и создав простое приложение.

> [!div class="nextstepaction"]
> [Создание первого приложения](get-started/get-started-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Интеграция с Teams

Смешайте функции, которые пользователи любят в существующем веб-приложении, службе или системе с функциями совместной работы Teams.

> [!div class="nextstepaction"]
> [Интеграция существующего приложения](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>Маленький код проходит долгий путь

Вам не нужно быть программистом-экспертом, чтобы создать отличное Teams приложение. Попробуйте одно из нескольких решений с низким кодом.

> [!div class="nextstepaction"]
> [Создание приложения с низким кодом](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a>Получить идеи для приложения

Ищете вдохновение для разработки приложений? Просмотрите список реальных сценариев и отраслевых решений с помощью макетов концепции высокой верности, чтобы понять различные способы, Teams приложения могут помочь пользователям.

> [!div class="nextstepaction"]
> [См. сценарии приложений](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>См. также

* [Основные сведения о приложении](~/concepts/app-fundamentals-overview.md)
* [Разработка Teams приложения](~/concepts/design/design-teams-app-process.md)
* [Составить карту случаев использования для Teams возможностей приложения](~/concepts/design/map-use-cases.md)
