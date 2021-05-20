---
title: Проектирование расширения собрания
author: heath-hamilton
description: Узнайте, как разрабатывать приложения на Teams собраниях и получить Microsoft Teams пользовательского интерфейса.
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
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Проектирование Microsoft Teams собрания

Вы можете создавать приложения, чтобы сделать собрания более продуктивными. Например, попросите людей заполнить опрос во время звонка или отправить быстрое напоминание, которое не прерывает поток собрания.

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

Более полные рекомендации по проектированию, включая элементы, которые можно захватить и изменить по мере необходимости, можно найти в Microsoft Teams пользовательского интерфейса.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Добавление расширения собрания

Можно добавить продление собрания до и во время собраний. Вы также можете добавить приложение для конкретной встречи непосредственно из Teams (AppSource).

### <a name="add-before-a-meeting"></a>Добавить перед собранием

В деталях собрания выберите **Добавить вкладку, чтобы** открыть вылет приложения и найти приложения, оптимизированные для собраний.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="Пример показывает, как добавить продление собрания перед собранием." border="false":::

### <a name="add-during-a-meeting"></a>Добавить во время собрания

На собрании выберите **больше добавить** приложение :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **и выбрать** нужное приложение.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="Пример показывает, как добавить расширение собрания во время собрания." border="false":::

## <a name="before-a-meeting"></a>Перед собранием

Перед собранием можно добавить содержимое во вкладку. В следующем примере показан проект опроса, на который люди ответят во время звонка.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="Пример показывает, как использовать содержимое в деталях собрания перед вызовом." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Анатомия: Вкладка собрания (до и после встреч)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="Пример показывает структурную анатомию вкладки собрания до и после собрания." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Название вкладки**: Навигационный ярлык для вкладки.|
|2|**Переполняем** вкладок: открывается вкладка действий, таких как переименование и удаление.|
|3|**iframe**: Отображает содержимое приложения.|

### <a name="designing-with-ui-templates"></a>Проектирование с шаблонами пользовательского интерфейса

Используйте один из следующих шаблонов Teams пользовательского интерфейса, чтобы помочь спроектировать вкладку собрания:

* [Список](../../concepts/design/design-teams-app-ui-templates.md#list): Списки могут отображать связанные элементы в сканируемом формате и позволяют пользователям принимать меры по всему списку или отдельным элементам.
* [Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): Целевая доска, иногда называемая доска kanban или плавательные дорожки, представляет собой набор карт, часто используемых для отслеживания состояния рабочих предметов или билетов.
* [Панель мониторинга](../../concepts/design/design-teams-app-ui-templates.md#dashboard): Панель мониторинга — это холст, содержащий несколько карт, которые обеспечивают обзор данных или содержимого.
* [Форма](../../concepts/design/design-teams-app-ui-templates.md#form): Формы для сбора, проверки и отправки пользовательского ввода структурированным способом.
* [Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state): Пустой шаблон состояния может быть использован для многих сценариев, включая войти в него, первый запуск, сообщения об ошибках и многое другое.
* [Левый навигатор](../../concepts/design/design-teams-app-ui-templates.md#left-nav): Левый шаблон навигации может помочь, если ваша вкладка требует некоторой навигации. Как правило, следует с минимумом следить за навигацией.

## <a name="use-an-in-meeting-tab"></a>Использование вкладки «Встреча»

Вкладка встречи — это холст для расширения совместной работы во время собраний. Участники могут видеть и взаимодействовать с контентом приложения в специальном пространстве за пределами стадии собрания с помощью общих или ролевых представлений.

### <a name="use-cases"></a>Варианты использования

Люди могут использовать вкладку на собрании для:

* Предоставьте подробную обратную связь. Например, оцените кандидата на работу.
* Создайте элемент опроса, опроса или задачи для участников собрания.
* Отображение заметок, имеющих отношение к собранию. Например, информация о лидере продаж.

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="Пример показывает, как можно представить содержимое опроса во вкладке &quot;Встреча&quot;." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Анатомия: Вкладка встречи

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="Пример показывает структурную анатомию вкладки в собрании." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Значок приложения (выбранный)**: 16-пиксельный прозрачный логотип приложения.|
|2|**Имя приложения**|
|3|**Заголовок**: Включает имя приложения.|
|4 |**Кнопка закрытия**: Отклоняет вкладку. Всегда используйте верхнюю правую близкую иконку вместо действия в подножке.|
|5 |**Бар уведомлений**: Предупреждения об ошибках отображаются прямо под заголовком и нажимают содержимое iframe вниз на 20 пикселей.|
|6 |**iframe**: Отображает содержимое приложения.|

### <a name="spacing"></a>Интервал

Оптимизируйте вкладку в собрании, чтобы соответствовать от края до края в области iframe шириной 280 пикселей. Есть 20 пикселей обивка на левой и правой сторонах iframe и между заголовком вкладки. iframe полна кровотечения в нижней части вкладки.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="Пример показывает размеры интервалов вкладок во встрече." border="false":::

### <a name="scrolling"></a>прокрутка

Содержимое Iframe должно прокручиваться вертикально. Вы можете видеть только содержимое, в которое вы прокрутили (ничего выше или ниже). Прокрутка является частью содержимого iframe.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="Пример показывает, как прокручивается вкладка в собрании." border="false":::

### <a name="navigation"></a>Навигация

Для сценариев с навигационными слоями или тяжелым содержанием мы рекомендуем разрешить пользователям переходить на вторичный слой. Пользователи должны иметь возможность вернуться к предыдущему уровеньу.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Пример показывает во встрече навигацию." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Используйте диалог на встрече

Диалоги на встрече отображаются на Teams собрания. Они требуют внимания, подтверждения или взаимодействия пользователя, но являются тонкими и не прерывают встречу. Вы должны использовать их экономно и для сценариев, которые являются легкими и ориентированными на задачи.

### <a name="use-cases"></a>Варианты использования

Диалоги на собрании запускаются пользователем (например, организатором собрания), который может захотеть, чтобы участники:

* Предоставьте краткую обратную связь
* Краткое обследование или опрос
* Отправить утверждения
* Получай напоминания

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="Пример показывает, как можно использовать диалог на собрании." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Анатомия: Диалог на встрече

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="Пример показывает структурную анатомию диалога на встрече." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Заголовок**: Включает значок приложения, имя, строку действия и близкий значок.|
|2|**iframe**: Отображает содержимое приложения.|

### <a name="anatomy-in-meeting-dialog-header"></a>Анатомия: Заголовок диалога на встрече

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="Пример показывает структурную анатомию заголовка диалога на собрании." border="false":::

Существует два варианта заголовка. Когда это возможно, используйте вариант с аватаром, чтобы укрепить, что диалог исходит от человека.

|Счетчик|Описание|
|----------|-----------|
|1|**Аватар**: Человек, который инициирует диалог на встрече.|
|2|**Значок приложения**|
|3|**Имя приложения**|
|4 |**Закрыть кнопку**: Увольняет диалог.|
|5 |**Строка действия**: Обычно описывает, кто инициировал диалог.|

### <a name="responsive-behavior"></a>Адаптируемое поведение

Диалоги на собраниях могут различаться по размеру для учета различных сценариев. Убедитесь в том, чтобы поддерживать обивку и размеры компонентов.

* **Ширина**: Вы можете указать ширину iframe диалога в любом месте в пределах поддерживаемого диапазона размеров.
* **Высота**: Вы можете указать высоту iframe диалога в любом месте в пределах поддерживаемого диапазона размеров. Вы также можете разрешить пользователям прокрутку вертикально, если содержимое приложения превышает максимальную высоту.

Для реализации укажите ширину и высоту с помощью [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) ключа.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Пример показывает диалог на встрече. Ширина: Мин--280 пикселей (248 пикселей iframe). Макс--460 пикселей (428 пикселей iframe). Высота: 300 пикселей (iframe)." border="false":::

## <a name="after-a-meeting"></a>После собрания

Вы можете вернуться к собранию после его окончания и просмотреть содержимое приложения. В этом примере организатор собрания может посмотреть на результаты опроса во **вкладке Contoso.** (Примечание: С точки зрения проектирования нет никакой разницы между вкладкой до и после собрания).)

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="На примере иллюстрации показана вкладка после собрания." border="false":::

## <a name="best-practices"></a>Рекомендации

Используйте эти рекомендации для создания качественного приложения.

### <a name="interactions"></a>Взаимодействия

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Пример, показывающий, как ограничить количество взаимодействий." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>У: Ограничьте количество взаимодействий

Для диалогов на собрании удалите ненужный контент, который не поможет пользователям быстро что-то сделать.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Пример, показывающий, как не вводить ненужные элементы." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>Не: Ввеся ненужные элементы

Один диалог на встрече с несколькими взаимодействиями может отвлечь от вызова.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Макет

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Пример, показывающий, как следует использовать макет диалога с одной колонкой." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a>У: Используйте одноко колготок диалог макет

Поскольку диалоги находятся в центре стадии собрания, завершение задачи должно быть быстрым и простым, чтобы избежать разочарования пользователей.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Пример, показывающий, что не следует загромождать пространство расширения собрания." border="false":::

#### <a name="dont-clutter-the-space"></a>Не: Загромождать пространство

Плотный или чрезмерно структурированный контент может отвлекать и подавлять, особенно во время собрания.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Пример, показывающий макет вкладки с одной колонкой." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a>У: Используйте макет вкладки с одной колонкой

Учитывая узкий характер вкладки в заседании, мы настоятельно рекомендуем отображать содержимое в одном столбце.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Пример отображения вкладки с несколькими столбцами." border="false":::

#### <a name="dont-use-multiple-columns"></a>Не: Используйте несколько столбцов

Из-за ограниченного пространства вкладки в собрании макеты с более чем одним столбецом не рекомендуются.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Элементы управления

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Пример, показывающий, как правильно выровнять основные элементы управления." border="false":::

#### <a name="do-right-align-the-primary-action"></a>Do: Право выровнять первичное действие

Рекомендуем позиционировать наиболее визуально тяжелые действия в нужном месте.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Пример, показывающий, как не следует левая выравнивание основных элементов управления." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>Не: Левые или центральные действия выравнивания

Это отклоняется от стандартной Teams для размещения элементов управления в диалоге и может в конфликте с диалогом за верхним.

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Прокрутка

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Пример, показывающий вертикальную прокрутку во вкладке &quot;Встреча&quot;." border="false":::

#### <a name="do-scroll-vertically"></a>У: Прокрутите вертикально

Пользователи ожидают вертикальной прокрутки в Teams (и в других местах).

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Пример, показывающий горизонтальную прокрутку во вкладке &quot;Встреча&quot;." border="false":::

#### <a name="dont-scroll-horizontally"></a>Не: Прокрутите горизонтально

Горизонтальная прокрутка не является ожидаемым поведением в Teams. Другие полотна в среде собрания прокрутки по вертикали.

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>Рабочие процессы

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Пример, показывающий сложный сценарий во вкладке &quot;Встреча&quot;." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>У: Сценарии поверхностного комплекса во вкладке "Встреча"

Если ваше приложение включает в себя несколько задач, мы настоятельно рекомендуем использовать вкладку в собрании с макетом одной колонки.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Пример, показывающий сложные сценарии в диалоге на встрече." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>Не: Сделать на встрече диалоги сложными

Диалоги на встрече предназначены для краткого взаимодействия.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Темы

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Пример, показывающий расширение собрания с темной темой." border="false":::

#### <a name="do-use-teams-color-tokens"></a>У: Используйте Teams цветные жетоны

Teams оптимизированы для темного режима, чтобы помочь уменьшить визуальный и когнитивный шум, чтобы пользователи могли сосредоточиться на обсуждении и общем контенте. Узнайте об использовании <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">цветовых жетонов (Fluent UI).</a>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Пример, показывающий расширение собрания с темой по умолчанию (свет)." border="false":::

#### <a name="dont-hard-code-hex-values"></a>Не: Жесткий код hex значения

Если вы не используете Teams, ваши проекты будут менее масштабируемыми и потребуется больше времени для управления.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Навигация

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Пример, показывающий расширение собрания с кнопкой &quot;Назад&quot;." border="false":::

#### <a name="do-have-a-back-button"></a>У: Иметь кнопку "Назад"

Если во вкладке собрания находится более одного уровня навигации, пользователи должны иметь возможность вернуться к прежним представлениям.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Пример, показывающий расширение собрания с двумя кнопками увольнения." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>Не: Включите еще одну кнопку увольнения

Предоставление опции закрытия содержимого вкладки в заседании может вызвать проблемы, так как в заголовке уже есть кнопка для увольнения самой вкладки в собрании.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Пример отображения модалов (или модулей задач) во вкладке &quot;Встреча&quot;." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>Внимание: Избегайте модалей в вкладке "Встреча"

Модалы (также известные как модули задач) в и без того узкой вкладке в собрании могут обернуть и скрыть содержимое.

   :::column-end:::
:::row-end:::
