---
title: Проектирование личного приложения
description: Узнайте, как создать Teams и получить Microsoft Teams пользовательского интерфейса.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 83fad746d71dd196f6efa6526f5c6c28ceac9e20
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644897"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Разработка личного приложения для Microsoft Teams

Персональным приложением может быть бот, частное рабочее пространство или и то, и другое. Иногда он функционирует как место для создания или просмотра контента, в других случаях он предлагает пользователю вид с высоты птичьего полета на все, что у них, когда приложение было настроено как вкладка в нескольких каналах.

Для руководства разработкой приложения в следующих сведениях описывается и иллюстрируется, как люди могут добавлять, использовать и управлять личными приложениями в Teams.

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

В наборе пользовательского интерфейса можно найти исчерпывающие рекомендации по разработке персональных приложений Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости. Набор пользовательского интерфейса также имеет важные темы, такие как доступность и размер отзывчивый, которые здесь не охватываются.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Добавление личного приложения

Вы можете добавить личное приложение из Teams магазина (AppSource) или вылет  приложения, выбрав значок More слева от Teams (показано в следующем примере).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="В примере показано, как добавить личное приложение из вылета приложения." border="false":::

## <a name="use-a-personal-app-private-workspace"></a>Использование личного приложения (личное рабочее пространство)

С помощью частного рабочего пространства вы можете просматривать содержимое приложения, содержательное для вас в центре, не Teams.

(Примечание реализации. Личное рабочее пространство основано на возможностях [*личной*](../../build-your-first-app/build-personal-tab.md) вкладки.)

### <a name="anatomy-personal-app-private-workspace"></a>Анатомия: Личное приложение (личное рабочее пространство)

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="В примере показана анатомия компонентов личной вкладки." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Присвоение приложения:** логотип и имя приложения.|
|B|**Вкладки.** Обеспечивает навигацию для личного приложения.|
|C|**Представление всплывающих** окон: отодвигает содержимое приложения из родительского окна в автономный детский окне.|
|D|**Дополнительные меню.** Включает дополнительные параметры приложения и сведения. (Можно также сделать **Параметры** вкладку.)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="В примере показана структурная анатомия личной вкладки." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Вкладки.** Обеспечивает навигацию для личного приложения.|
|1|**iframe:** отображает содержимое приложения.|

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="В примере показана анатомия компонентов личной вкладки." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Присвоение приложения:** имя приложения.|
|B|**Вкладки.** Обеспечивает навигацию для личного приложения.|
|C|**Дополнительные меню.** Включает дополнительные параметры приложения и сведения.|
|D|**Основная навигация.** Обеспечивает навигацию для приложения другими основными Teams функциями.|

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="В примере показана структурная анатомия личной вкладки." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Вкладки.** Обеспечивает навигацию для личного приложения.|
|1|**веб-просмотр.** Отображает содержимое приложения.|

---

### <a name="designing-with-ui-templates-and-advanced-components"></a>Проектирование с помощью шаблонов пользовательского интерфейса и расширенных компонентов

Используйте один из следующих Teams и компонентов для разработки личной вкладки:

* [Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.
* [Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.
* [Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.
* [Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.
* [Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.
* [Левый nav:](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav)компонент левого nav может помочь, если ваше личное приложение требует некоторой навигации. В общем, необходимо сохранить навигацию до минимума.

## <a name="use-a-personal-app-bot"></a>Использование личного приложения (бота)

Личные приложения могут включать бот для индивидуальных бесед и частных уведомлений (например, когда коллега публикует комментарий на вашей доске). Бот доступен на указанной вкладке.

### <a name="anatomy-personal-app-bot"></a>Анатомия: личное приложение (бот)

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="В примере показана анатомия компонентов персональных ботов." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Вкладка Бот.** Например, включаем вкладку **Chat** для доступа к беседам и уведомлениям ботов.|
|B|**Сообщение бота.** Боты часто отправляют сообщения и уведомления в виде карты (например, адаптивной карты).|
|C|**Compose box**: Вводное поле для отправки сообщений боту.|

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="В примере показана анатомия компонентов персональных ботов." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Точка входа бота.** Точка входа для доступа пользователей к функции бота в личном приложении.|
|B|**Кнопка**"Назад": возвращает пользователей в личное рабочее пространство.|
|C|**Сообщение бота.** Боты часто отправляют сообщения и уведомления в виде карты (например, адаптивной карты).|
|D|**Compose box**: Вводное поле для отправки сообщений боту.|

---

## <a name="manage-a-personal-tab"></a>Управление личной вкладке

На левой стороне Teams пользователи могут правой кнопкой мыши личного приложения, чтобы закрепить, удалить и настроить другие параметры приложения.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="В примере показаны параметры управления личным приложением." border="false":::

## <a name="best-practices"></a>Рекомендации

Используйте эти рекомендации для создания качественного приложения.

### <a name="tab-priority"></a>Приоритет tab

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>Do: Показать наиболее релевантный контент на первой вкладке

При гибком размере вкладки справа могут быть усечены или невещены.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="В примере показано, как личное приложение отображает наиболее релевантный контент на первой вкладке." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>Не: руководство со вторичным контентом или метаданными

Как и стандартное веб-приложение, навигация вкладок должна развиваться в порядке, который помогает понять основные функции приложения.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="В примере показано личное приложение, ведущее со вторичным контентом или метаданными." border="false":::

### <a name="tab-hierarchy"></a>Иерархия вкладок

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>Do: Tabs should be of equal hierarchy and represent key app pages

Ваши вкладки должны классифицировать основные функции и содержимое приложения. При гибком размере содержимое справа может стать усеченным или невыясненным.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="В примере показано личное приложение с вкладками равной иерархии." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>Не: включайте различные уровни иерархии

Ваше содержимое должно развиваться в логическом порядке, что помогает пользователям понять его. Если у вас есть две вкладки, которые тесно связаны, рассмотрите возможность их объединения в одну вкладку.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="В примере показано личное приложение с различными уровнями иерархии." border="false":::

### <a name="first-run-experience"></a>Интерфейс при первом запуске

#### <a name="do-include-a-first-run-experience"></a>Do: Включите первый запуск

При первом использовании личного приложения должен быть по крайней мере приветственный экран. Для ботов опишите, что может сделать ваш бот, и предопишите быстрые действия, например кнопку вход.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="В примере показано, что нужно делать во время личного опыта запуска приложения." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="В другом примере показано, что нужно делать во время работы с личным приложением в первом запуске." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>Не: начните с пустого экрана

Пользователи могут быть сбиты с толку, если при первом запуске приложения ничего не отображается.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="В примере показано, что не нужно делать во время первого запуска личного приложения." border="false":::

### <a name="personalized-content"></a>Персонализированный контент

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>Do: Совокупный контент приложения, релевантный пользователю

Будь то личная вкладка или бот, отображайте содержимое, связанное только с действиями пользователя в вашем приложении.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="В примере показано, что делать с личным приложением и персонализированным контентом." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Другой пример показывает, что делать с личным приложением и персонализированным контентом." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>Не: показывать несвязанные или чрезмерно широкий контент

В личных контекстах не отображайте контент для групп, в которые пользователь не входит. Личное содержимое бота должно фокусироваться на личности, а не на группе.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="В примере показано, что не нужно делать с личным приложением и персонализированным контентом." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Другой пример показывает, что не нужно делать с личным приложением и персонализированным контентом." border="false":::

### <a name="complex-app-features"></a>Сложные функции приложения

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>Do: Разрешить пользователям доступ к сложным функциям в браузере

Ваше приложение должно сосредоточиться на основных задачах в Teams, но вы все равно можете просматривать полное, автономные приложения в браузере.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="В примере показано, как обрабатывать сложные функции приложения с помощью личного приложения." border="false":::

#### <a name="dont-include-your-entire-app"></a>Не: включите все приложение

Если вы не создали приложение специально для Teams, возможно, у вас есть функции, которые не имеют смысла в средстве совместной работы.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="В примере показано, как не обрабатывать сложные функции приложения с помощью личного приложения." border="false":::

## <a name="see-also"></a>См. также

Эти другие рекомендации по проектированию могут помочь в зависимости от области вашего личного приложения:

* [Проектирование вкладки](../../tabs/design/tabs.md)
* [Проектирование бота](../../bots/design/bots.md)
