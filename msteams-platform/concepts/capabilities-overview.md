---
title: Обзор функций приложения
author: heath-hamilton
description: Описание возможностей приложения Teams, таких как вкладки, боты, расширения для сообщений, а также веб-перехватчики и соединители; область приложения, например личные и общие приложения
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 09/22/2020
keywords: Вкладки, боты, расширения для обмена сообщениями, веб-перехватчики и соединители
ms.openlocfilehash: 53ee8ffb0fdf51b5c4069cc79ff7022dbc46777d
ms.sourcegitcommit: 3d7b34e7032b6d379eca8f580d432b365c8be840
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/18/2022
ms.locfileid: "62897972"
---
# <a name="understand-microsoft-teams-app-features"></a>Понимание функций приложения Microsoft Teams

Каждое приложение уникально благодаря нескольким способам расширения Teams. Приложение Teams может отображаться для пользователя по-разному. Функции приложения Teams включают:

- Возможности приложений
- Область приложения

Например, пользователь может взаимодействовать с приложением на вкладке холста, чтобы выполнить действие, или может сделать то же самое с помощью диалогового бота. Вы можете использовать только одну функцию, например веб-перехватчик, в то время как у других есть более одной функции, чтобы предоставить пользователям различные варианты.

Эти возможности могут существовать в разных областях. Например, приложение может отображать данные в центральном общем расположении, то есть на вкладке, и предоставлять те же сведения через персональный диалоговый интерфейс, то есть бот.

## <a name="app-capabilities"></a>Возможности приложений

Чтобы расширить возможности приложения, необходимо понимать все основные возможности и точки входа, которые работают в пространстве для совместной работы. Вы можете поэкспериментировать с точками расширения для создания приложений. Важные компоненты проекта приложения помогают правильно настроить страницу приложения.

Ваши приложения Teams имеют одну или все из следующих основных возможностей:

:::row:::
   :::column span="":::
### <a name="personal-apps"></a>Персональные приложения

[Личное приложение](../concepts/design/personal-apps.md) — это выделенное пространство или бот, помогающие пользователю сосредоточиться на собственных задачах или просматривать важные действия.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-personal-apps-2021.png" alt-text="Концептуальное представление того, как выглядят персональные приложения в клиенте Microsoft Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

### <a name="tabs"></a>Вкладки

Отображение веб-контента на [вкладке](../tabs/what-are-tabs.md), где пользователи могут обсуждать и совместно работать над ним.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-channel-chat-apps-2021.png" alt-text="Концептуальное представление того, как выглядят вкладки в клиенте Microsoft Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a>Боты

Результатом беседы часто становится необходимость что-то сделать (создать заказ, проверить код, узнать статус запроса и так далее). [Бот](../bots/what-are-bots.md) может выполнять эти рабочие процессы прямо в Microsoft Teams.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-bots-2021.png" alt-text="Концептуальное представление того, как выглядят боты в клиенте Microsoft Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>Расширения для система обмена сообщениями

С помощью [расширений для сообщений](../messaging-extensions/what-are-messaging-extensions.md) можно быстро обмениваться информацией из внешних источников в беседе. Также с сообщениями можно выполнять различные действия, например, создать запрос в службу поддержки на основе публикации на канале.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-messaging-extensions-2021.png" alt-text="Концептуальное представление того, как выглядят расширения для сообщений в клиенте Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="meeting-extensions"></a>Расширения для собраний

[Включить приложение в функционал Teams для звонков](../apps-in-teams-meetings/design/designing-apps-in-meetings.md) можно разными способами.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-meeting-extensions-2021.png" alt-text="Концептуальное представление того, как выглядят расширения для собраний в клиенте Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="webhooks-and-connectors"></a>Веб-перехватчики и соединительные линии

[Входящие веб-перехватчики](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) — это простой способ автоматической отправки уведомлений из другого приложения на канал Microsoft Teams. С помощью [исходящих веб-перехватчиков](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks) можно отправлять сообщения веб-службам через @упоминание.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-connectors.png" alt-text="Концептуальное представление того, как выглядят соединители в клиенте Microsoft Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph для Teams

[API Microsoft Graph для Teams](/graph/teams-concept-overview) предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут создавать или улучшать функции вашего приложения (например, расширенные уведомления).

   :::column-end:::

> [!NOTE]
> Магазин Teams развивается:
> 
> Ранее бизнес-приложения обновлялись путем выбора многоточия на плитке. Благодаря обновленной версии Магазина Teams вы можете обновить бизнес-приложения, выполнив вход в [Центр администрирования Teams](https://admin.teams.microsoft.com).

:::image type="content" source="../assets/images/overview-graph.png" alt-text="Концептуальное представление API Microsoft Graph для Teams." border="false":::

   :::column-end:::
:::row-end:::

## <a name="choose-the-correct-scope-for-your-app"></a>Выберите правильную область для приложения

Область приложения можно выбрать из следующих вариантов:

- Личное приложение. Личное приложение — это бот или специальная область, помогающая пользователям сосредоточиться на своих задачах или просматривать важные для них события.
- Общее приложение. Команды, каналы и чат — пространства для совместной работы. Приложения в этих контекстах доступны всем в этом пространстве. Пространства для совместной работы обычно ориентированы на рабочий процесс для взаимодействия с приложением или разблокировки новых социальных взаимодействий.

## <a name="see-also"></a>См. также

* [Создание приложений для Teams](../overview.md)
* [Сборка первого приложения Microsoft Teams](../build-your-first-app/build-first-app-overview.md)