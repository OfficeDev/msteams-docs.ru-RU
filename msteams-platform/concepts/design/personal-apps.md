---
title: Проектирование личного приложения
description: Узнайте, как создать личное приложение Teams и получить набор пользовательского интерфейса Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 8302f3768034014ef5a446effeee0603afe4a5f4
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020760"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Разработка личного приложения для Microsoft Teams

Персональным приложением может быть бот, частное рабочее пространство или и то, и другое. Иногда он функционирует как место для создания или просмотра контента, в других случаях он предлагает пользователю вид с высоты птичьего полета на все, что у них, когда приложение было настроено как вкладка в нескольких каналах.

Чтобы направлять разработку приложения, в следующих сведениях описывается и иллюстрируется, как люди могут добавлять, использовать и управлять личными приложениями в Teams.

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

В наборе пользовательского интерфейса Microsoft Teams можно найти исчерпывающие рекомендации по разработке персональных приложений, в том числе элементы, которые можно захватить и изменить по мере необходимости. Набор пользовательского интерфейса также имеет важные темы, такие как доступность и размер отзывчивый, которые здесь не охватываются.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Добавление личного приложения

Вы можете добавить личное приложение из магазина Teams (AppSource) или вылет приложения, выбрав значок **More** на левой стороне Teams (показано в следующем примере).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="В примере показано, как добавить личное приложение из вылета приложения." border="false":::

## <a name="use-a-personal-app-private-workspace"></a>Использование личного приложения (личное рабочее пространство)

С помощью частного рабочего пространства можно просматривать содержимое приложения, которое имеет значение для вас в центре расположения, не покидая Teams.

(Примечание реализации. Личное рабочее пространство основано на возможностях [*личной*](../../build-your-first-app/build-personal-tab.md) вкладки.)

### <a name="anatomy-personal-app-private-workspace"></a>Анатомия: Личное приложение (личное рабочее пространство)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="В примере показана анатомия компонентов личной вкладки." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Присвоение приложения:** логотип и имя приложения.|
|B|**Вкладки.** Обеспечивает навигацию для личного приложения. Например, включаем **вкладку "О"** или **"Справка".**|
|C|**Представление всплывающих** окон: отодвигает содержимое приложения из родительского окна в автономный детский окне.|
|D|**Дополнительные меню:** включает дополнительные сведения о приложении и параметры. (Можно также сделать **параметры** вкладками.)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="В примере показана структурная анатомия личной вкладки." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Вкладки.** Обеспечивает навигацию для личного приложения.|
|1|**iframe:** отображает содержимое приложения.|

### <a name="designing-with-ui-templates"></a>Проектирование с помощью шаблонов пользовательского интерфейса

Для разработки личной вкладки используйте один из следующих шаблонов пользовательского интерфейса Teams:

* [Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.
* [Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.
* [Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.
* [Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.
* [Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.
* [Левый nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav). Шаблон левого nav может помочь если ваша вкладка требует некоторой навигации. В общем, вы должны сохранить навигацию вкладок до минимума.

## <a name="use-a-personal-app-bot"></a>Использование личного приложения (бота)

Личные приложения могут включать бот для индивидуальных бесед и частных уведомлений (например, когда коллега публикует комментарий на вашей доске). Бот доступен на указанной вкладке.

### <a name="anatomy-personal-app-bot"></a>Анатомия: личное приложение (бот)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="В примере показана анатомия компонентов персональных ботов." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Вкладка Бот.** Например, включаем вкладку **Chat** для доступа к беседам и уведомлениям ботов.|
|B|**Сообщение бота.** Боты часто отправляют сообщения и уведомления в виде карты (например, адаптивной карты).|
|C|**Compose box**: Вводное поле для отправки сообщений боту.|

## <a name="best-practices"></a>Рекомендации

### <a name="tab-priority"></a>Приоритет tab

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>Do: Показать наиболее релевантный контент на первой вкладке

При гибком размере вкладки справа могут быть усечены или невещены.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>Не: руководство со вторичным контентом или метаданными

Как и стандартное веб-приложение, навигация вкладок должна развиваться в порядке, который помогает понять основные функции приложения.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="Пример наилучшей практики личного приложения." border="false":::

### <a name="tab-hierarchy"></a>Иерархия вкладок

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>Do: Tabs should be of equal hierarchy and represent key app pages

Ваши вкладки должны классифицировать основные функции и содержимое приложения. При гибком размере содержимое справа может стать усеченным или невыясненным.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>Не: включайте различные уровни иерархии

Ваше содержимое должно развиваться в логическом порядке, что помогает пользователям понять его. Если у вас есть две вкладки, которые тесно связаны, рассмотрите возможность их объединения в одну вкладку.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

### <a name="first-run-experience"></a>Интерфейс при первом запуске

#### <a name="do-include-a-first-run-experience"></a>Do: Включите первый запуск

При первом использовании личного приложения должен быть по крайней мере приветственный экран. Для ботов опишите, что может сделать ваш бот, и предопишите быстрые действия, например кнопку вход.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="На рисунке показана лучшая практика личного приложения." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Пример наилучшей практики личного приложения." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>Не: начните с пустого экрана

Пользователи могут быть сбиты с толку, если при первом запуске приложения ничего не отображается.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="На рисунке показана лучшая практика личного приложения." border="false":::

### <a name="personalized-content"></a>Персонализированный контент

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>Do: Совокупный контент приложения, релевантный пользователю

Будь то личная вкладка или бот, отображайте содержимое, связанное только с действиями пользователя в вашем приложении.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="В примере приводится пример наилучшей практики личного приложения." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>Не: показывать несвязанные или чрезмерно широкий контент

В личных контекстах не отображайте контент для групп, в которые пользователь не входит. Личное содержимое бота должно фокусироваться на личности, а не на группе.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="Раскрыт пример наилучшей практики личного приложения." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

### <a name="complex-app-features"></a>Сложные функции приложения

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>Do: Разрешить пользователям доступ к сложным функциям в браузере

Ваше приложение должно сосредоточиться на основных задачах в Teams, но вы все равно можете просматривать полное, автономные приложения в браузере.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

#### <a name="dont-include-your-entire-app"></a>Не: включите все приложение

Если вы не создали приложение специально для Teams, возможно, у вас есть функции, которые не имеют смысла в средстве совместной работы.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="Иллюстрация предоставляет личные приложения наилучшей практики." border="false":::

## <a name="manage-a-personal-tab"></a>Управление личной вкладке

В левой части Teams пользователи могут правой кнопкой мыши личные приложения, чтобы закрепить, удалить и настроить другие параметры приложения.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="В примере показаны параметры управления личным приложением." border="false":::

## <a name="learn-more"></a>Подробнее

Эти другие рекомендации по проектированию могут помочь в зависимости от области вашего личного приложения:

* [Проектирование вкладки](../../tabs/design/tabs.md)
* [Проектирование бота](../../bots/design/bots.md)

## <a name="validate-your-design"></a>Проверка приложения

Если вы планируете опубликовать приложение в AppSource, следует понимать проблемы проектирования, из-за которых отправка приложения часто бывает неудачной.

> [!div class="nextstepaction"]
> [Ознакомьтесь с рекомендациями по проверке дизайна](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
