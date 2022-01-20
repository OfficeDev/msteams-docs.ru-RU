---
title: Создание приложений для платформы Microsoft Teams
author: heath-hamilton
description: Обзор того, как разработчики могут расширять возможности Microsoft Teams с помощью собственных приложений.
ms.topic: overview
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: 1a7957c8ea6d889ffe5ab7e40c8a5bb1377b6ca5
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059625"
---
# <a name="build-apps-for-microsoft-teams"></a>Создание приложений для Microsoft Teams

Приложения Microsoft Teams собирают ключевую информацию, общие инструменты и доверенные процессы на платформе, где люди все чаще собираются, учатся и работают.

Эти приложения помогут адаптировать Teams к вашим нуждам. Создайте для Teams что-то новое или интегрируйте существующее приложение.

> [!div class="nextstepaction"]
> [Начните отсюда](get-started/get-started-overview.md)

## <a name="what-are-teams-apps"></a>Что такое приложения Microsoft Teams?

Приложения Microsoft Teams — это наборы [возможностей](concepts/capabilities-overview.md). Приложения бывают простыми (отправка уведомлений) и сложными (управление записями пациентов). Планируя свое приложение, помните, что Microsoft Teams — это центр совместной работы. Лучшие приложения Microsoft Teams помогают людям лучше координировать усилия и самовыражаться.

### <a name="personal-apps"></a>Персональные приложения

:::row:::
   :::column span="1":::

**Помощь в фокусировке внимания**. [Персональное приложение](concepts/design/personal-apps.md) — это бот или специальная область, помогающая пользователям сосредоточиться на своих задачах или просматривать важные для них события.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-personal-apps-2021.png" alt-text="Концептуальное представление того, как выглядят персональные приложения в клиенте Microsoft Teams." border="false":::

   :::column-end:::

:::row-end:::

### <a name="tabs"></a>Вкладки

:::row:::
   :::column span="1":::

**Удобство совместной работы**. Отображение веб-контента на [вкладке](tabs/what-are-tabs.md), на которой пользователи могут обсуждать и совместно работать над ним.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-channel-chat-apps-2021.png" alt-text="Концептуальное представление того, как выглядят вкладки в клиенте Microsoft Teams." border="false":::

   :::column-end:::

:::row-end:::

### <a name="bots"></a>Боты

:::row:::
   :::column span="1":::

**Воплощение слов в действия**. Результатом беседы часто становится необходимость что-то сделать (создать заказ, проверить код, узнать статус запроса и так далее). [Бот](bots/what-are-bots.md) может выполнять эти рабочие процессы прямо в Microsoft Teams.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-bots-2021.png" alt-text="Концептуальное представление того, как выглядят боты в клиенте Microsoft Teams." border="false":::

   :::column-end:::

:::row-end:::

### <a name="messaging-extensions"></a>Расширения для система обмена сообщениями

:::row:::

   :::column span="1":::

**Упрощение многозадачной работы**. С помощью [расширений для сообщений](messaging-extensions/what-are-messaging-extensions.md) можно быстро обмениваться информацией из внешних источников в беседе. Также с сообщениями можно выполнять различные действия, например, создать запрос в службу поддержки на основе публикации на канале.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-messaging-extensions-2021.png" alt-text="Концептуальное представление того, как выглядят расширения для сообщений в клиенте Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

### <a name="meeting-extensions"></a>Расширения для собраний

:::row:::

   :::column span="1":::

**Создание приложений для собраний**. [Включить приложение в функционал Microsoft Teams для звонков](apps-in-teams-meetings/design/designing-apps-in-meetings.md) можно разными способами.

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-meeting-extensions-2021.png" alt-text="Концептуальное представление того, как выглядят расширения для собраний в клиенте Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

### <a name="webhooks-and-connectors"></a>Веб-перехватчики и соединительные линии

:::row:::

   :::column span="":::

**Связь с внешними приложениями**. [Входящие веб-перехватчики](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) — это простой способ автоматической отправки уведомлений из другого приложения на канал Microsoft Teams. С помощью [исходящих веб-перехватчиков](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks) можно отправлять сообщения веб-службам через @упоминание.

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Концептуальное представление того, как выглядят соединители в клиенте Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph для Teams

:::row:::

   :::column span="":::

**Использование данных Teams**. [API Microsoft Graph для Teams](/graph/teams-concept-overview) предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут создавать или улучшать функции вашего приложения (например, расширенные уведомления).

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-graph.png" alt-text="Концептуальное представление API Microsoft Graph для Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>Начало разработки

Ознакомьтесь с разработкой для Teams, настроив среду и создав простое приложение.

> [!div class="nextstepaction"]
> [Создание первого приложения](get-started/get-started-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Интеграция с Teams

Совмещайте функции, которые нравятся пользователям в существующем веб-приложении, службе или системе с функциями совместной работы Microsoft Teams.

> [!div class="nextstepaction"]
> [Интеграция существующего приложения](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>Немного кода — много возможностей

Не нужно быть программистом-экспертом, чтобы создать отличное приложение для Teams. Попробуйте решения с малым использованием кода.

> [!div class="nextstepaction"]
> [Создание приложений с малым использованием кода](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a>Идеи для приложения

Ищете вдохновение для разработки приложений? Просмотрите список реальных сценариев и отраслевых решений с помощью достоверных концептуальных макетов, чтобы понять, как приложения Microsoft Teams могут помочь пользователям.

> [!div class="nextstepaction"]
> [См. сценарии приложений](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="test-your-app-running-across-microsoft-365"></a>Тестирование приложения, запущенного в Microsoft 365

С помощью функции предварительного просмотра пакета JavaScript SDK v2 в клиенте Microsoft Teams можно проверить работу приложения Microsoft Teams в других часто используемых службах Microsoft 365.

> [!div class="nextstepaction"]
> [Расширение приложения](m365-apps/overview.md)

## <a name="see-also"></a>См. также

* [Основные сведения о приложении](~/concepts/app-fundamentals-overview.md)
* [Разработка приложения Microsoft Teams](~/concepts/design/design-teams-app-process.md)
* [Сопоставление вариантов использования с возможностями приложения Teams](~/concepts/design/map-use-cases.md)
