---
title: Разработка личного приложения
description: Узнайте, как разработать личное приложение Teams и получить набор пользовательских интерфейсов Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 971071be9f345815f5461646d7970efdf05fd5c4
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605022"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Разработка личного приложения для Microsoft Teams

Личное приложение может представлять собой Bot, частные рабочие области или и то, и другое. Иногда она работает так же, как место для создания или просмотра контента, а также в других случаях, когда приложение настроено как вкладка в нескольких каналах.

В следующей статье описываются и демонстрируются способы добавления и использования персональных приложений в Teams, а также управления ими.

## <a name="microsoft-teams-ui-kit"></a>Набор элементов пользовательского интерфейса Microsoft Teams

Вы можете найти подробные рекомендации по проектированию личных приложений, в том числе элементы, которые можно изменять и изменять при необходимости, в наборе UI Microsoft Teams. Кроме того, в наборе элементов пользовательского интерфейса есть важные темы, такие как специальные возможности и размеры отклика, которые не рассматриваются здесь.

> [!div class="nextstepaction"]
> [Получение набора элементов пользовательского интерфейса Microsoft Teams (фигма)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Добавление личного приложения

Вы можете добавить личное приложение из приложения Store (AppSource) или из всплывающего меню приложения, щелкнув значок **More (дополнительно** ) в левой части Teams (показано в следующем примере).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="Пример показывает, как добавить личное приложение из всплывающего меню приложения." border="false":::

## <a name="use-a-personal-app-private-workspace"></a>Использование личного приложения (личная рабочая область)

С помощью частной рабочей области вы можете просматривать контент приложений, который имеет смысл в централизованном расположении, не выходя из Teams.

(Примечание о реализации. Частная Рабочая область основана на возможности [*вкладки "личные"*](../../build-your-first-app/build-personal-tab.md) .)

### <a name="anatomy-personal-app-private-workspace"></a>Структура: личное приложение (личная рабочая область)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="В примере показана структура компонента личной вкладки." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Атрибуты приложений**: ваш логотип и имя приложения.|
|B|**Вкладки**: предоставляет навигацию для личного приложения. Например, включите вкладку " **о программе** " или " **Справка** ".|
|C|**Всплывающем окне View**: помещение контента приложения из родительского окна в автономное дочернее окно.|
|D|**Другое меню**: включает дополнительные сведения о приложении и другие параметры. (Можно также сделать **Параметры** вкладкой.)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="В примере показана структура структуры личной вкладки." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Вкладки**: предоставляет навигацию для личного приложения.|
|1 |**IFRAME**: отображение контента приложения.|

### <a name="designing-with-ui-templates"></a>Разработка с помощью шаблонов пользовательского интерфейса

Используйте один из следующих шаблонов пользовательского интерфейса Teams для создания личной вкладки:

* [Список](../../concepts/design/design-teams-app-ui-templates.md#list): списки могут отображать связанные элементы в формате с возможностью записи, а пользователи выполнять действия для всего списка или отдельных элементов.
* [Доска задач](../../concepts/design/design-teams-app-ui-templates.md#task-board): доска задач, иногда называемая доской Канбан или свим желобами, — это коллекция карточек, часто используемых для отслеживания состояния рабочих элементов или билетов.
* [Панель мониторинга](../../concepts/design/design-teams-app-ui-templates.md#dashboard): панель мониторинга — это холст, содержащий несколько карточек, которые предоставляют обзор данных или контента.
* [Форма](../../concepts/design/design-teams-app-ui-templates.md#form): формы предназначены для сбора, проверки и отправки пользовательских данных структурированным способом.
* [Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state): шаблон пустое состояние можно использовать для многих сценариев, в том числе входа в систему, первого запуска, сообщений об ошибках и многого другого.
* [Левая панель навигации](../../concepts/design/design-teams-app-ui-templates.md#left-nav): левая панель навигации может помочь вам, если на вкладке требуется выполнить некоторую навигацию. Как правило, переход по клавише Tab должен быть минимальным.

## <a name="use-a-personal-app-bot"></a>Использование личного приложения (Bot)

Персональные приложения могут включать робота для однообъектных бесед и частных уведомлений (например, когда коллега публикует комментарий в монтажной области). Элемент Bot доступен на заданной вкладке.

### <a name="anatomy-personal-app-bot"></a>Структура: личное приложение (Bot)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="В примере показана структура персональных компонентов Bot." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Вкладка "bot"**: например, включите вкладку **Chat** , чтобы получить доступ к беседам и уведомлениям в Bot.|
|B|**Сообщение Bot**: Боты часто отправляет сообщения и уведомления в виде карточки (например, адаптивной карты).|
|C|**Поле создания**: поле ввода для отправки сообщений в Bot.|

## <a name="best-practices"></a>Рекомендации

### <a name="tab-priority"></a>Приоритет вкладки

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>Do: отображение наиболее релевантного содержимого на первой вкладке

При быстром масштабировании вкладки справа могут быть усечены или отображаться.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>Не: интерес с дополнительным содержимым или метаданными

Как и в случае со стандартным веб-приложением, Навигация по табуляции должна быть продолжена в порядке, позволяющем понять основные функции приложения.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

### <a name="tab-hierarchy"></a>Иерархия вкладок

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>Do: вкладки должны иметь одинаковую иерархию и представлять ключевые страницы приложений

Вкладки должны классифицировать основные компоненты и содержимое приложения. При быстром масштабировании содержимое в правой части может быть усечено или не отображаться.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>Не используйте разные уровни иерархии.

Контент должен продвигается в логическом порядке, который поможет пользователям понять его. Если у вас есть две вкладки, которые тесно связаны друг с другом, рассмотрите их объединение на одной вкладке.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

### <a name="first-run-experience"></a>Интерфейс при первом запуске

#### <a name="do-include-a-first-run-experience"></a>Do: Включение интерфейса первого запуска

При первом использовании личного приложения должен отображаться по крайней мере экран приветствия. В Боты опишите действия, которые может выполнять Bot, и предоставляя быстрые действия, такие как кнопка входа.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>Не совсем: начало с пустого экрана

Пользователи могут запутаться, если при первом запуске приложения ничего не отображается.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

### <a name="personalized-content"></a>Персонализированное содержимое

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>Do: Объединение контента приложения, относящегося к пользователю

Независимо от того, является ли это личная вкладка или Bot, отображается содержимое, связанное только с действиями пользователя в вашем приложении.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>Не: показывать несвязанный или слишком большой контент

В личных контекстах не отображать контент для Teams, не входящих в состав. Личное содержимое Bot должно сосредоточиться на индивидуальной, а не группе.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

### <a name="complex-app-features"></a>Функции сложных приложений

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>Do: разрешает пользователям получать доступ к сложным функциям в браузере

Ваше приложение должно сосредоточиться на основных задачах в Teams, но вы по-прежнему можете просматривать полное автономное приложение в браузере.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

#### <a name="dont-include-your-entire-app"></a>Не включайте свое приложение целиком.

Если вы не создали приложение специально для Teams, вероятно, у вас есть функции, которые не имеют смысла в средстве совместной работы.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

## <a name="manage-a-personal-tab"></a>Управление вкладкой "личные"

В левой части Teams пользователи могут щелкнуть личное приложение, чтобы закрепить, удалить и настроить другие параметры приложения.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="В примере показаны параметры для управления личным приложением." border="false":::

## <a name="learn-more"></a>Дополнительные сведения

Другие рекомендации по проектированию могут пригодиться в зависимости от области личных приложений:

* [Разработка вкладки](../../tabs/design/tabs.md)
* [Разработка ленты](../../bots/design/bots.md)

## <a name="validate-your-design"></a>Проверка проекта

Если вы планируете опубликовать свое приложение в AppSource, следует изучить проблемы, которые обычно приводят к сбою приложений во время отправки.

> [!div class="nextstepaction"]
> [Проверка рекомендаций по проверке макета](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
