---
title: Проектирование расширения собрания
author: heath-hamilton
description: Узнайте, как проектировать приложения на собраниях Teams и получать пакет пользовательского интерфейса Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: c6e76356b698da4e32e279b0842ab2cc35254e99
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886760"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Разработка расширения собрания Microsoft Teams

Вы можете создавать приложения, чтобы сделать собрания более эффективными. Например, попросите людей выполнить опрос во время вызова или отправить краткое напоминание, которое не прерывает поток собрания.

## <a name="microsoft-teams-ui-kit"></a>Пакет пользовательского интерфейса Microsoft Teams

В пакете пользовательского интерфейса Microsoft Teams можно найти более комплексные рекомендации по проектированию, включая элементы, которые можно захватить и изменить при необходимости.

> [!div class="nextstepaction"]
> [Get the Microsoft Teams UI Kit (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Добавление расширения собрания

Вы можете добавить расширение собрания до и во время собраний. Вы также можете добавить приложение для определенного собрания непосредственно из Магазина Teams (AppSource).

### <a name="add-before-a-meeting"></a>Добавить перед собранием

В сведениях о собрании выберите **"Добавить вкладку" +,** чтобы открыть войдите в приложение, и найдите приложения, оптимизированные для собраний.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="В примере показано, как добавить расширение собрания перед собранием." border="false":::

### <a name="add-during-a-meeting"></a>Добавление во время собрания

На собрании выберите **"Добавить** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **приложение" и** выберите нужное приложение.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="В примере показано, как добавить расширение собрания во время собрания." border="false":::

## <a name="before-a-meeting"></a>Перед собранием

Перед собранием можно добавить содержимое на вкладку. В следующем примере показан черновик вопроса опроса, на который люди ответят во время вызова.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="В примере показано, как приложение в сведениях о собрании перед вызовом." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Структура: вкладка "Собрание" (до и после собрания)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="В примере показана структурная структура вкладки собрания до и после собрания." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Имя вкладки:** метка навигации для вкладки.|
|2 |**Переполнение вкладки:** открывает действия с вкладками, например переименовывать и удалять.|
|3|**iframe**: отображает содержимое приложения.|

### <a name="designing-with-ui-templates"></a>Проектирование с помощью шаблонов пользовательского интерфейса

Используйте один из следующих шаблонов пользовательского интерфейса Teams для разработки вкладки для собраний:

* [Список:](../../concepts/design/design-teams-app-ui-templates.md#list)списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям делать действия со всем списком или отдельными элементами.
* [Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач: доска задач, иногда называемая доской канба или плаваемой, — это коллекция карточек, часто используемых для отслеживания состояния элементов или билетов.
* [Информационная](../../concepts/design/design-teams-app-ui-templates.md#dashboard)панель : панель мониторинга — это холст, содержащий несколько карточек, которые предоставляют обзор данных или содержимого.
* [Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.
* [Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние: пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.
* [Левый навигационный](../../concepts/design/design-teams-app-ui-templates.md#left-nav)шаблон : левый шаблон навигации может помочь, если вкладка требует определенной навигации. Как правило, навигация по вкладке должна быть минимальной.

## <a name="use-an-in-meeting-tab"></a>Использование вкладки "Собрание"

Вкладка "Собрание" — это холст для расширения совместной работы во время собраний. Участники могут видеть содержимое приложения и взаимодействовать с ним в выделенном пространстве вне стадии собрания с помощью общих представлений или представлений на основе ролей.

### <a name="use-cases"></a>Варианты использования

На вкладке "Собрание" можно:

* Предоставление подробных отзывов (например, оценка кандидата на должность)
* Быстрое создание опроса, опроса или элемента задачи для участников собрания
* Отображение заметок, релевантных для собрания (например, сведения о менеджере по продажам)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="В примере показано, как можно представить контент опроса на вкладке &quot;Собрание&quot;." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Структура: вкладка "Собрание"

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="В примере показана структурная структура вкладки на собрании." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Значок приложения (выбранный)**: прозрачный логотип приложения размером 16 пикселей.|
|2 |**Имя приложения**|
|3|**Заготовка:** включает имя приложения.|
|4 |**Кнопка закрытия:** закрывает вкладку. Всегда используйте верхний правый значок закрытия вместо действия в нижнем.|
|5 |**Гистометр** уведомлений: оповещения об ошибках отображаются непосредственно под заголовком и выдвигают содержимое iframe вниз на 20 пикселей.|
|6 |**iframe**: отображает содержимое приложения.|

### <a name="spacing"></a>Интервал

Оптимизируйте вкладку, вместив ее в область iframe размером 280 пикселей. Слева и справа от iframe и между заголом вкладки имеется 20 пикселей заполнения. The iframe is full bleed to the bottom of the tab.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="В примере показаны размеры интервала вкладок в собрании." border="false":::

### <a name="scrolling"></a>Прокрутка

Содержимое Iframe должно прокручиваться вертикально. Вы можете просмотреть только содержимое, которое вы прокрутите до (ничего выше или ниже). Панель прокрутки является частью содержимого iframe.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="В примере показано, как прокручивается вкладка &quot;Собрание&quot;." border="false":::

### <a name="navigation"></a>Навигация

В сценариях с уровнями навигации или большим содержимым мы рекомендуем разрешить пользователям переходить на дополнительный уровень. Пользователи должны иметь возможность вернуться на предыдущий уровень.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="В примере показана навигация в собрании." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Использование диалогового окно собрания

Диалоги собраний отображаются на стадии собрания Teams. Они требуют внимания пользователя, подтверждения или взаимодействия, но являются незначительными и не прерывают собрание. Их следует использовать экономно и для сценариев, ориентированных на светлые и ориентированные на задачи.

### <a name="use-cases"></a>Варианты использования

Диалоговые окно собрания инициирует пользователь (например, организатор собрания), который может потребовать от участников:

* Предоставление краткой обратной связи
* Краткий опрос
* Отправка утверждений
* Получать напоминания

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="В примере показано, как можно использовать диалоговое окно собрания." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Структура: диалоговое окно собрания

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="В примере показана структурная структура диалогового окно собрания." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Заглавная** строка: включает значок приложения, имя, строку действия и значок закрытия.|
|2 |**iframe**: отображает содержимое приложения.|

### <a name="anatomy-in-meeting-dialog-header"></a>Структура: загор. Диалоговое окно собрания

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="В примере показана структурная структура загона диалога собрания." border="false":::

Существует два варианта загона. По возможности используйте вариант с аватаром, чтобы подчеркнуть, что диалоговое окно идет от человека.

|Счетчик|Описание|
|----------|-----------|
|1|**Аватар:** человек, который инициирует диалоговое окно собрания.|
|2 |**Значок приложения**|
|3|**Имя приложения**|
|4 |**Кнопка закрытия:** закрывает диалоговое окно.|
|5 |**Строка** действия: обычно описывает, кто инициировал диалоговое окно.|

### <a name="responsive-behavior"></a>Адаптируемое поведение

Диалоги собраний могут различаться по размеру в зависимости от различных сценариев. Обязательно поддержив заполнение и размеры компонентов.

* **Width**:The iframe width is an absolute value within the range you specify.
* **Height**: высота диалогового окно определяется содержимым в iframe. Вертикальная прокрутка берет на себя содержимое, которое превышает максимальную высоту.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="В примере показано диалоговое окно собрания. Ширина: min--280 пикселей (iframe 248 пикселей). Max --460 пикселей (iframe 428 пикселей). Высота: 300 пикселей (iframe)." border="false":::

## <a name="after-a-meeting"></a>После собрания

Вы можете вернуться к собранию после его окончания и просмотреть содержимое приложения. В этом примере организатор собрания может посмотреть на результаты опроса на вкладке **Contoso.** (Примечание. С точки зрения проектирования нет разницы между вкладками до и после собрания.)

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="В примере показана вкладка после собрания." border="false":::

## <a name="best-practices"></a>Рекомендации

### <a name="interactions"></a>Взаимодействия

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Пример ограничения числа взаимодействий." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>Do: ограничение количества взаимодействий

В диалоговом окну собрания удалите ненужный контент, который не поможет пользователям быстро выполнить задачи.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Пример, показывающий, как не вводить ненужные элементы." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>Не: вводить ненужные элементы

Отдельное диалоговое окно собрания с несколькими взаимодействиями может отвлекать от звонка.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Макет

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Пример использования макета диалога с одним столбцом." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a>Do: Использование макета диалога с одним столбцом

Так как диалоги находятся в центре стадии собрания, выполнение задачи должно быть быстрым и простым во избежание проблем пользователей.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Пример, показывающий, что не следует засорять пространство расширения собрания." border="false":::

#### <a name="dont-clutter-the-space"></a>Don't: Clutter the space

Сильное или слишком структурированное содержимое может отвлекать и отвлекать, особенно во время собрания.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Пример макета вкладки с одним столбцом." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a>Do: Использование макета вкладки с одним столбцом

С учетом узкой природы вкладки на собрании настоятельно рекомендуется отображать содержимое в одном столбце.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Пример, на котором показана вкладка с несколькими столбцами." border="false":::

#### <a name="dont-use-multiple-columns"></a>Не используйте: используйте несколько столбцов

Из-за ограниченного пространства на вкладке собрания не рекомендуется использовать макеты с более чем одним столбцом.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Элементы управления

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Пример выравнивания основных элементов управления по правому правому направлению." border="false":::

#### <a name="do-right-align-the-primary-action"></a>Do: выравнивание по правому правому направлению основного действия

Мы рекомендуем расположить наиболее сильное визуальное действие в нужное место.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Пример, показывающий, как не следует выравнивать основные элементы управления левой стороной." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>Don't: Left or center align actions

Это отклоняется от стандартного шаблона Teams для размещения управления в диалоговом оке и может конфликтовть с диалогом за верхним.

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Прокрутка

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Пример вертикальной прокрутки на вкладке собрания." border="false":::

#### <a name="do-scroll-vertically"></a>Do: Прокрутка по вертикали

Пользователи ожидают вертикальной прокрутки в Teams (и в другом месте).

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Пример горизонтальной прокрутки на вкладке собрания." border="false":::

#### <a name="dont-scroll-horizontally"></a>Не: прокрутка по горизонтали

Горизонтальная прокрутка не является ожидаемым поведением в Teams. Другие холсты в среде собраний прокручивается вертикально.

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>Рабочие процессы

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Пример сложного сценария на вкладке &quot;Собрание&quot;." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Do: сложные сценарии Surface на вкладке "Собрание"

Если ваше приложение включает несколько задач, мы настоятельно рекомендуем использовать вкладку собрания с макетом из одного столбца.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Пример, показывающий сложные сценарии в диалоговом оке собрания." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>Не: сделать диалоговые окно собрания сложными

Диалоги на собрании предназначены для краткого взаимодействия.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Темы

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Пример расширения собрания с темной темой." border="false":::

#### <a name="do-use-teams-color-tokens"></a>Do: Use Teams color tokens

Собрания Teams оптимизированы для темного режима, чтобы уменьшить визуальный и познавательный шум, чтобы пользователи могли сосредоточиться на обсуждении и общем содержимом. Узнайте об использовании <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">маркеров цвета (пользовательский интерфейс Fluent).</a>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Пример расширения собрания с светлой темой по умолчанию." border="false":::

#### <a name="dont-hard-code-hex-values"></a>Don't: Hard code hex values

Если вы не используете маркеры цвета Teams, ваши макеты будут менее масштабируемыми и займет больше времени на управление.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Навигация

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Пример расширения собрания с кнопкой &quot;Назад&quot;." border="false":::

#### <a name="do-have-a-back-button"></a>Do: Have a Back button

Если на вкладке собрания имеется несколько уровней навигации, пользователи должны иметь возможность вернуться к своим предыдущим представлениям.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Пример расширения собрания с двумя кнопками с отклоняться." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>Не: включить еще одну кнопку "Отклонять"

Предоставление возможности закрыть содержимое вкладки собрания может вызвать проблемы, так как в заголке уже есть кнопка для закрытия самой вкладки собрания.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Пример, показывающий модальные модули (или модули задач) на вкладке собрания." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>Внимание! Избегайте модальных модалов на вкладке "Собрание"

Модальные модули (также известные как модули задач) на уже узкой вкладке собрания могут обтекать содержимое и скрывать его.

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>Проверка проекта

Если вы планируете опубликовать приложение в AppSource, следует понимать проблемы проектирования, которые часто приводят к сбойу приложений во время отправки.

> [!div class="nextstepaction"]
> [Проверка рекомендаций по проверке проекта](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
