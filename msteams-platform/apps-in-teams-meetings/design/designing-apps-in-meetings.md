---
title: Проектирование расширения собрания
author: heath-hamilton
description: Узнайте, как создать приложения Teams собраниях и получить Microsoft Teams пользовательского интерфейса.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 0a888c333305e9caafcd0bac0e5549bf08ead424
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566028"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Проектирование расширения Microsoft Teams собрания

Вы можете создавать приложения, чтобы сделать собрания более продуктивными. Например, попросите людей выполнить опрос во время вызова или отправить быстрое напоминание, которое не прерывает поток собрания.

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

В наборе пользовательского интерфейса можно найти более исчерпывающие рекомендации по проектированию Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Добавление расширения собрания

Вы можете добавить расширение собрания до и во время собраний. Вы также можете добавить приложение для определенной встречи непосредственно из Teams магазина (AppSource).

### <a name="add-before-a-meeting"></a>Добавление перед собранием

В сведениях о собрании выберите Добавить вкладку **+,** чтобы открыть вылет приложения и найти приложения, оптимизированные для собраний.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="В примере показано, как добавить расширение собрания перед собранием." border="false":::

### <a name="add-during-a-meeting"></a>Добавление во время собрания

На собрании выберите **дополнительные** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **добавления приложения** и выберите нужное приложение.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="В примере показано, как добавить расширение собрания во время собрания." border="false":::

## <a name="before-a-meeting"></a>Перед собранием

Перед собранием можно добавить содержимое на вкладке. В следующем примере показан проект опроса, на который люди ответят во время вызова.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="В примере показано, как приложение содержимым в сведениях о собрании перед вызовом." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Анатомия: вкладка "Собрание" (до и после собраний)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="В примере показана структурная анатомия вкладки собрания до и после собрания." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Имя вкладки.** Метка навигации для вкладки.|
|2|**Переполнение вкладки:** открывает действия вкладки, такие как переименование и удаление.|
|3|**iframe:** отображает содержимое приложения.|

### <a name="designing-with-ui-templates"></a>Проектирование с помощью шаблонов пользовательского интерфейса

Используйте один из следующих Teams пользовательского интерфейса для разработки вкладки собраний:

* [Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.
* [Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.
* [Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.
* [Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.
* [Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.
* [Левый nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav). Шаблон левого nav может помочь если ваша вкладка требует некоторой навигации. В общем, вы должны сохранить навигацию вкладок до минимума.

## <a name="use-an-in-meeting-tab"></a>Использование вкладки в собрании

Вкладка на собрании — это холст для расширения совместной работы во время собраний. Участники могут видеть и взаимодействовать с контентом приложения в выделенном пространстве за пределами стадии собраний с помощью общих представлений или представлений на основе ролей.

### <a name="use-cases"></a>Варианты использования

Люди могут использовать вкладку на собрании, чтобы:

* Предоставление подробных отзывов. Например, оцените кандидата на работу.
* Создайте элемент опроса, опроса или задачи для участников собрания.
* Отображение заметок, соответствующих собранию. Например, сведения о лидере продаж.

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="В примере показано, как можно представить содержимое опроса на вкладке на собрании." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Anatomy: In-meeting tab

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="В примере показана структурная анатомия вкладки на собрании." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Значок приложения (выбранный)**: 16-пиксельный прозрачный логотип приложения.|
|2|**Имя приложения**|
|3|**Заглавное** имя. Включает имя приложения.|
|4 |**Кнопка закрыть:** отклонять вкладку. Всегда используйте значок верхнего правого закрытия вместо действия в подножке.|
|5 |**Панели** уведомлений. Оповещения об ошибках отображаются непосредственно под заголовком и толкают содержимое iframe вниз на 20 пикселей.|
|6 |**iframe:** отображает содержимое приложения.|

### <a name="spacing"></a>Интервал

Оптимизируйте вкладку в собрании, чтобы поместиться по краям в области iframe шириной 280 пикселей. На левой и правой сторонах iframe и между загонами вкладок имеется 20 пикселей. Iframe полностью кровотока в нижней части вкладки.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="В примере показаны размеры интервала между вкладками в собрании." border="false":::

### <a name="scrolling"></a>Прокрутка

Содержимое Iframe должно прокручиваться вертикально. Вы можете видеть только содержимое, которое вы прокрутите (ничего выше или ниже). Панель прокрутки является частью контента iframe.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="В примере показано, как прокручивается вкладка на собрании." border="false":::

### <a name="navigation"></a>Навигация

Для сценариев со слоями навигации или тяжелым контентом рекомендуется разрешить пользователям переходить на вторичный уровень. Пользователи должны иметь возможность вернуться к предыдущему слою.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="В примере показана навигация в собрании." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Использование диалогового номера на собрании

Диалоги на собрании отображаются на Teams собрания. Они требуют внимания пользователя, подтверждения или взаимодействия, но являются тонкими и не прерывают собрание. Эти сценарии следует использовать экономно и для сценариев, ориентированных на легкие и задачи.

### <a name="use-cases"></a>Варианты использования

Диалоговые точки на собрании запускаются пользователем (например, организатором собрания), который может потребовать от участников:

* Предоставление кратких отзывов
* Краткий опрос или опрос
* Отправка утверждений
* Получать напоминания

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="В примере показано, как можно использовать диалоговое окно на собрании." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Анатомия: диалоговое окно на собрании

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="В примере показана структурная анатомия диалогов на собрании." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Заглавная** строка: включает значок приложения, имя, строку действия и значок закрытия.|
|2|**iframe:** отображает содержимое приложения.|

### <a name="anatomy-in-meeting-dialog-header"></a>Анатомия: диалоговое заглавное окно в собрании

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="В примере показана структурная анатомия диалогового загона на собрании." border="false":::

Существует два варианта загона. По возможности используйте вариант с аватаром, чтобы подчеркнуть, что диалоговое окно идет от человека.

|Счетчик|Описание|
|----------|-----------|
|1|**Аватар:** человек, который инициирует диалоговое окно на собрании.|
|2|**Значок приложения**|
|3|**Имя приложения**|
|4 |**Кнопка Закрыть:** отклонять диалоговое окно.|
|5 |**Строка** действия. Обычно описывается, кто инициировал диалоговое окно.|

### <a name="responsive-behavior"></a>Адаптируемое поведение

Диалоги на собрании могут отличаться по размеру для учета различных сценариев. Убедитесь, что поддерживается обивка и размеры компонентов.

* **Ширина.** Можно указать ширину iframe диалогов в любом месте в поддерживаемом диапазоне размеров.
* **Высота.** Вы можете указать высоту iframe диалогов в любом месте в поддерживаемом диапазоне размеров. Вы также можете разрешить пользователям прокрутку по вертикали, если содержимое приложения превышает максимальную высоту.

Чтобы реализовать, укажите ширину и высоту с помощью [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) ключа.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="В примере показан диалоговое окно на собрании. Ширина: min--280 пикселей (248 пикселей iframe). Max--460 пикселей (428 пикселей iframe). Высота: 300 пикселей (iframe)." border="false":::

## <a name="after-a-meeting"></a>После собрания

Вы можете вернуться к собранию после его окончания и просмотреть содержимое приложения. В этом примере организатор собрания может посмотреть результаты опроса на вкладке **Contoso.** (Примечание. С точки зрения дизайна нет разницы между опытом вкладки до и после собрания.)

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="В примере показана вкладка после собрания." border="false":::

## <a name="best-practices"></a>Рекомендации

Используйте эти рекомендации для создания качественного приложения.

### <a name="interactions"></a>Взаимодействие

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Пример, показывающий, как ограничить количество взаимодействий." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>Do: Ограничение количества взаимодействий

Для диалогов на собраниях удалите ненужный контент, который не поможет пользователям быстро выполнить свою задачу.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Пример, показывающий, как не вводить ненужные элементы." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>Не: вводить ненужные элементы

Один диалоговое окно с несколькими взаимодействиями может отвлечь от вызова.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Макет

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Пример, показывающий использование макета диалогов с одним столбцом." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a>Do: Использование макета диалогов с одним столбцом

Так как диалоги находятся в центре стадии собрания, завершение задачи должно быть быстрым и простым, чтобы избежать разочарования пользователей.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Пример, показывающий, что не следует загромождать пространство расширения собрания." border="false":::

#### <a name="dont-clutter-the-space"></a>Не: загромождать пространство

Плотный или чрезмерно структурированный контент может отвлекать и ошеломить, особенно во время собрания.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Пример макета вкладки с одним столбцом." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a>Do: Использование макета вкладок с одним столбцом

Учитывая узкий характер вкладки на собрании, настоятельно рекомендуется отображать содержимое в одном столбце.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Пример, показывающий вкладку с несколькими столбцами." border="false":::

#### <a name="dont-use-multiple-columns"></a>Не используйте несколько столбцов

Из-за ограниченного пространства вкладки в собрании макеты с более чем одним столбцом не рекомендуется.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Элементы управления

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Пример, показывающий, как правильно выравнивать основные элементы управления." border="false":::

#### <a name="do-right-align-the-primary-action"></a>Do: правильно выравнивание основного действия

Рекомендуется расположить наиболее визуально тяжелое действие в нужном месте.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Пример, показывающий, как не следует выровнять основные элементы управления." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>Не: действия левого или центрального выравнивания

Это отклоняется от стандартного шаблона Teams для размещения управления в диалоговом окте и может противоречить диалоговику за верхней.

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Прокрутка

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Пример, показывающий вертикальную прокрутку на вкладке в собрании." border="false":::

#### <a name="do-scroll-vertically"></a>Do: Прокрутите по вертикали

Пользователи ожидают вертикального прокрутки Teams (и в других местах).

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Пример, показывающий горизонтальную прокрутку на вкладке на собрании." border="false":::

#### <a name="dont-scroll-horizontally"></a>Не: прокрутите по горизонтали

Горизонтальная прокрутка не является ожидаемым поведением в Teams. Другие холсты в среде собраний прокрутки вертикально.

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>Рабочие процессы

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Пример, показывающий сложный сценарий на вкладке на собрании." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Do: Surface complex scenarios in the in-meeting tab

Если ваше приложение включает несколько задач, настоятельно рекомендуется использовать вкладку на собрании с макетом с одним столбцом.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Пример, показывающий сложные сценарии в диалоговом окантове встречи." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>Don't: Make in-meeting dialogs complex

Диалоги на собраниях предназначены для кратких взаимодействий.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Темы

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Пример, показывающий расширение собрания с темной темой." border="false":::

#### <a name="do-use-teams-color-tokens"></a>Do: использование Teams маркеров цвета

Teams для темного режима оптимизированы, чтобы уменьшить визуальный и когнитивный шум, чтобы пользователи могли сосредоточиться на обсуждении и совместном контенте. Узнайте об использовании <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">маркеров цвета (fluent UI).</a>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Пример, показывающий расширение собрания с темой по умолчанию (светлая)." border="false":::

#### <a name="dont-hard-code-hex-values"></a>Don't: Hard code hex values

Если вы не используете маркеры Teams цвета, ваши проекты будут менее масштабируемыми и у вас будет больше времени для управления.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Навигация

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Пример, показывающий расширение собрания с кнопкой &quot;Назад&quot;." border="false":::

#### <a name="do-have-a-back-button"></a>Do: Есть кнопка "Назад"

Если на вкладке на собрании имеется несколько уровней навигации, пользователи должны иметь возможность вернуться к своим предыдущим представлениям.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Пример, показывающий расширение собрания с двумя кнопками увольнения." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>Не: включи еще одну кнопку увольнения

Предоставление возможности закрыть содержимое вкладки в собрании может вызвать проблемы, так как в загонах уже есть кнопка, чтобы отклонять сам вкладку в собрании.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Пример, показывающий модули (или модули задач) в вкладке на собрании." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>Внимание. Избегайте модалов в вкладке в собрании

Модули (также известные как модули задач) на уже узкой вкладке в собрании могут обернуть содержимое и скрыть его.

   :::column-end:::
:::row-end:::
