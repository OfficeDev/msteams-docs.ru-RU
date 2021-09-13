---
title: Создание приложений для Microsoft Teams платформы
author: heath-hamilton
description: Сведения о том, как разработчики могут расширять Microsoft Teams с помощью настраиваемого приложения.
ms.topic: overview
ms.localizationpriority: medium
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: e35393a2696ace22068e34566c3dad4a3109bd73
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157504"
---
# <a name="build-apps-for-microsoft-teams"></a>Создание приложений для Microsoft Teams

Microsoft Teams приложения приносят ключевые сведения, общие инструменты и доверенные процессы в места, где люди все чаще собираются, учатся и работают.

Приложения — это то, как Teams, чтобы соответствовать вашим потребностям. Создайте что-то новое для Teams или интегрируете существующее приложение.

> [!div class="nextstepaction"]
> [Начните отсюда](get-started/prerequisites.md)

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
> [Создание первого приложения](get-started/prerequisites.md)

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

## <a name="integrate-teams-in-your-external-app"></a>Интеграция Teams во внешнем приложении
На этой странице основное внимание уделяется встраив собственный опыт в Microsoft Teams путем создания Teams приложений. Если вы хотите  изменить эту модель и интегрировать Teams или другие возможности связи в собственный внешний опыт приложения, см. в [примере Azure Communication Services.](/azure/communication-services/overview) Службы связи Azure — это облачные службы с API REST и SDKs клиентской библиотеки, которые помогают интегрировать связь в собственные настраиваемые приложения. С помощью библиотеки пользовательского интерфейса можно в Teams или React веб-компоненты для вызова и [чата.](https://azure.github.io/communication-ui-library/)

Приложения Azure Communication Services могут использовать [](/azure/communication-services/concepts/teams-interop) функции предварительного просмотра для взаимодействия с Teams и позволяют настраиваемой приложению анонимно присоединяться к собраниям Teams. Например, можно интегрировать видеозвоз в приложение мобильного банкинга и разрешить конечным пользователям практически встречаться с сотрудниками банка с помощью Microsoft Teams. 

Вы также можете интегрировать Microsoft 365 для создания внешних приложений, в которые встраивалось видео и PSTN, вызывающего от имени Teams пользователя. Если вы использовали [Skype для бизнеса SDKs](/skype-sdk/appsdk/skypeappsdk) в прошлом, эти возможности в составе служб связи Azure рекомендуется использовать в качестве замены.

## <a name="see-also"></a>См. также

* [Добавьте кнопку Share-to-Teams на веб-сайте](concepts/build-and-test/share-to-teams.md)
* [Разработка Teams приложения](concepts/design/design-teams-app-overview.md)
* [Microsoft Teams SDK клиента JavaScript](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* Bot Framework SDK для [JavaScript](https://github.com/Microsoft/botbuilder-js) и [.NET](https://github.com/Microsoft/botbuilder-dotnet/)
* [Распространение приложения Teams](concepts/deploy-and-publish/apps-publish-overview.md)
