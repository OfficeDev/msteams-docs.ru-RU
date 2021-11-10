---
title: Проектирование расширения собрания
author: heath-hamilton
description: Узнайте, как создать приложения в Teams собраниях и получить Microsoft Teams пользовательского интерфейса, вкладку в собрании и использовать случаи, отзывчивое поведение и общий этап собраний, а также тему и навигацию.
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: conceptual
keywords: Шаблон набора пользовательского интерфейса на собрании с отзывчивым поведением на общем этапе собраний
ms.openlocfilehash: 39d0ef00d6a012726f2a3645f3d8e2bf00ebaf33
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887847"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Проектирование расширения Microsoft Teams собрания

Вы можете создавать приложения, чтобы сделать собрания более продуктивными. Например, попросите людей выполнить опрос во время собрания или отправить быстрое напоминание, которое не прерывает поток собрания.

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

В наборе пользовательского интерфейса можно найти более исчерпывающие рекомендации по проектированию Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Добавление расширения собрания

Пользователи могут добавлять расширение собрания до и во время собраний. Они также могут добавлять приложение для определенной встречи непосредственно из Teams магазина.

### <a name="add-before-a-meeting"></a>Добавление перед собранием

В сведениях о собрании пользователи могут выбрать Добавить вкладку **+,** чтобы открыть вылет приложения и найти приложения, оптимизированные для собраний.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="В примере показано, как добавить расширение собрания перед собранием." border="false":::

### <a name="add-during-a-meeting"></a>Добавление во время собрания

#### <a name="mobile"></a>Мобильная версия

После того как приложение было добавлено (например, на рабочем столе), пользователи могут получить доступ к приложению на собрании, выбрав **Подробнее** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: .

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="В примере показано, как добавить расширение собрания во время собрания на мобильном телефоне." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

На собрании пользователи могут выбрать **дополнительные** добавления :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **приложения** и выбрать нужное приложение.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="В примере показано, как добавить расширение собрания во время собрания." border="false":::

## <a name="before-a-meeting"></a>Перед собранием

Перед собранием приложение доступно пользователям на вкладке. В следующем примере показан проект вопроса опроса, на который люди ответят во время собрания.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="В примере показано, как приложение содержимым в сведениях о собрании перед вызовом." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Анатомия: вкладка "Собрание" (до и после собраний)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="В примере показана структурная анатомия вкладки собрания до и после собрания." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Имя вкладки.** Метка навигации для вкладки.|
|2|**Переполнение вкладки.** Открывает действия вкладки, такие как переименование и удаление.|
|3|**iframe.** Отображает содержимое приложения.|

### <a name="design-with-ui-templates"></a>Проектирование с помощью шаблонов пользовательского интерфейса

Используйте один из следующих Teams пользовательского интерфейса для разработки вкладки собраний:

* [Список](../../concepts/design/design-teams-app-ui-templates.md#list). Списки могут отображать связанные элементы в формате, доступном для сканирования, и позволяют пользователям выполнять действия со всем списком или отдельными элементами.
* [Доска задач.](../../concepts/design/design-teams-app-ui-templates.md#task-board) Доска задач, иногда называемая канбан-доской или трассой, представляет собой набор карточек, часто используемых для отслеживания состояния рабочих элементов или билетов.
* [Панель мониторинга](../../concepts/design/design-teams-app-ui-templates.md#dashboard): панель мониторинга — это холст, содержащий несколько карточек, которые предоставляют обзор данных или содержимого.
* [Форма](../../concepts/design/design-teams-app-ui-templates.md#form). Формы предназначены для сбора, проверки и отправки данных пользовательского ввода в структурированном виде.
* [Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state). Шаблон пустого состояния можно использовать для различных сценариев, включая вход, первый запуск, сообщения об ошибках и т. д.
* [Навигация слева.](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav) Компонент навигации слева может помочь если вкладка требует некоторой навигации. В общем, необходимо сохранить навигацию до минимума.

## <a name="use-an-in-meeting-tab"></a>Использование вкладки в собрании

Вкладка на собрании — это холст для расширения совместной работы во время собраний. Участники могут видеть и взаимодействовать с контентом приложения в выделенном пространстве за пределами стадии собраний с помощью общих представлений или представлений на основе ролей.

### <a name="use-cases"></a>Варианты использования

Люди могут использовать вкладку на собрании, чтобы:

* Предоставление подробных отзывов. Например, оцените кандидата на работу.
* Создайте элемент опроса, опроса или задачи для участников собрания.
* Отображение заметок, соответствующих собранию. Например, сведения о лидере продаж.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="В примере показано, как можно представить содержимое опроса в вкладке на собрании на мобильном телефоне." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="В примере показано, как можно представить содержимое опроса на вкладке на собрании." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Anatomy: In-meeting tab

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="В примере показана структурная анатомия вкладки на собрании." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Значок приложения (выбранный)**: 16-пиксельный прозрачный логотип приложения.|
|2|**Название приложения**|
|3|**Заглавное** имя. Включает имя приложения.|
|4|**Кнопка закрыть:** отклонять вкладку. Всегда используйте значок верхнего правого закрытия вместо действия в подножке.|
|5|**Панели** уведомлений. Оповещения об ошибках отображаются непосредственно под заголовком и толкают содержимое iframe вниз на 20 пикселей.|
|6 |**iframe.** Отображает содержимое приложения.|

### <a name="spacing"></a>Интервал

Оптимизируйте вкладку в собрании, чтобы поместиться по краям в области iframe шириной 280 пикселей. На левой и правой сторонах iframe и между загонами вкладок имеется 20 пикселей. Iframe полностью кровотока в нижней части вкладки.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="В примере показаны размеры интервала между вкладками в собрании." border="false":::

### <a name="scrolling"></a>Прокрутка

Помните следующее, если вы разрешаете прокрутку:

* Содержимое в содержимом iframe должно прокручиваться только по вертикали.
* Пользователи должны видеть только прокрутку контента (ничего выше или ниже). 
* Панель прокрутки является частью контента iframe.

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

### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="В примере показано, как можно использовать диалоговое окно на собрании на мобильном телефоне." border="false":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="В примере показано, как можно использовать диалоговое окно на собрании." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Анатомия: диалоговое окно на собрании

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="В примере показана структурная анатомия диалогов на собрании." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Заглавная** строка: включает значок приложения, имя, строку действия и значок закрытия.|
|2|**iframe.** Отображает содержимое приложения.|

### <a name="anatomy-in-meeting-dialog-header"></a>Анатомия: диалоговое заглавное окно в собрании

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="В примере показана структурная анатомия диалогового загона на собрании." border="false":::

Существует два варианта загона. По возможности используйте вариант с аватаром, чтобы подчеркнуть, что диалоговое окно идет от человека.

|Счетчик|Описание|
|----------|-----------|
|1|**Аватар:** человек, который инициирует диалоговое окно на собрании.|
|2|**Значок приложения**|
|3|**Название приложения**|
|4|**Кнопка Закрыть:** отклонять диалоговое окно.|
|5|**Строка** действия. Обычно описывается, кто инициировал диалоговое окно.|

### <a name="responsive-behavior-in-meeting-dialogs"></a>Отзывчивое поведение: диалоговые логи на собрании

Диалоги на собрании могут отличаться по размеру для учета различных сценариев. Должны сохраняться размеры полей и компонентов.

* **Ширина.** Можно указать ширину iframe диалогов в любом месте в поддерживаемом диапазоне размеров.
* **Высота.** Вы можете указать высоту iframe диалогов в любом месте в поддерживаемом диапазоне размеров. Вы также можете разрешить пользователям прокрутку по вертикали, если содержимое приложения превышает максимальную высоту.

Чтобы реализовать, укажите ширину и высоту с помощью [`externalResourceUrl`](~/apps-in-teams-meetings/API-references.md#notificationsignal-api) ключа.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="В примере показан диалоговое окно на собрании. Ширина: min--280 пикселей (248 пикселей iframe). Max--460 пикселей (428 пикселей iframe). Высота: 300 пикселей (iframe)." border="false":::

## <a name="use-the-shared-meeting-stage"></a>Использование общего этапа собраний

Общая стадия собраний помогает участникам собраний взаимодействовать и сотрудничать с контентом приложения в режиме реального времени. Например, пользователи могут сосредоточиться на редактировании документа, мозговом штурме с помощью доски или просмотре панели мониторинга.

Приложения, общие на этапе собрания, занимают то же место, что и общий экран. Этап переориентирован для всех участников собрания.

> [!NOTE]
> Все пользователи на собрании могут видеть приложение при совместном доступе с рабочего стола. Однако в настоящее время возможности для обмена приложением с мобильными устройствами недоступны.
 
### <a name="use-cases"></a>Варианты использования

Общий этап собраний — это совместная работа и участие. Вот несколько примеров сценариев, которые помогут вам начать работу.

:::row:::
   :::column span="1":::

**Редактирование и обзор.** Погрузитесь в панели мониторинга и планирование со всеми на собрании.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="В примере показана панель мониторинга, которая просматривается на общей стадии собрания." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**Доска.** Рисуйте и идеи вместе на общем холсте.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="В примере показана доска на общем этапе собрания." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**Викторина:** Проверка знаний и получение информации с помощью интерактивных материалов.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="В примере показана викторина на общей стадии собрания." border="false":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-shared-meeting-stage"></a>Анатомия: общий этап собраний

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="На изображении показана анатомия дизайна общей стадии собраний." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Значок** приложения. Выделенная значок указывает, что вкладка приложения на собрании открыта.|
|2|**Кнопка "Share to meeting stage":** точка входа, чтобы поделиться приложением со стадией собрания. Отображает, если настроить приложение для использования общей стадии собраний.|
|3|**iframe.** Отображает содержимое приложения.|
|4|Остановка доступа к **кнопке**: Перестает делиться приложением со стадией собрания. Отображает только участника, который запустил долю.|
|5|**Атрибуция presenter:** отображает имя участника, который поделился приложением.|

### <a name="responsive-behavior-shared-meeting-stage"></a>Отзывчивое поведение: общая стадия собрания

Приложения, общие на этапе собрания, различаются по размеру в зависимости от состояния собрания и размера окна. Поддерживать обивку и реагировать на навигацию и элементы управления так же, как и в браузере.

* **Боковая** панель. Пользователь может открыть боковую панель в любое время во время собрания, чтобы пообщаться, просмотреть список или использовать приложение (например, вкладку на собрании). Этап динамически перестановки, когда панель открыта.
* **Сетка видео и аудио:** видео- и аудиосистемы всегда видны для демонстрации участников собрания. Если пользователь прожекторы или пин-коды кого-то на собрании, это увеличивает высоту или ширину сетки участников в зависимости от ориентации.

#### <a name="meeting-stage-without-side-panel"></a>Этап собрания (без боковой панели)

Если боковая панель не открыта, уровень собрания по умолчанию составляет 994x678 пикселей и может быть не менее 792x382 пикселей.

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="Изображение, на котором показана отзывчивость общей стадии собрания с закрытой боковой панелью." border="false":::

#### <a name="meeting-stage-with-side-panel"></a>Этап собрания (с боковой панелью)

При открытой боковой панели уровень собрания по умолчанию составляет 918x540 пикселей и может быть не менее 472x382 пикселей.

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="Изображение, показывающая отзывчивость общей стадии собрания с открытой боковой панелью." border="false":::

## <a name="after-a-meeting"></a>После собрания

Вы можете вернуться к собранию после его окончания и просмотреть содержимое приложения. В этом примере организатор собрания может посмотреть результаты опроса на вкладке **Contoso.** (Примечание. С точки зрения дизайна нет разницы между опытом вкладки до и после собрания.)

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="В примере показана вкладка после собрания." border="false":::

## <a name="best-practices"></a>Рекомендации

Используйте эти рекомендации для создания качественных приложений.

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

Один диалог с несколькими взаимодействиями может отвлечь от собрания.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="Пример, показывающий, как создать сфокусированную среду." border="false":::

#### <a name="do-create-a-focused-environment"></a>Do: Создание сфокусированной среды

Рекомендуется сохранить область действия приложения только на стадии собрания. Вы можете использовать вкладку на собрании в боковой панели в качестве дополнительного закрытого представления для определенных сценариев.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="Пример, показывающий, как не включать конкурирующие поверхности во время собраний." border="false":::

#### <a name="dont-include-competing-surfaces"></a>Не: включайте конкурирующие поверхности

Ваше приложение должно задавать пользователям фокусироваться только на одной поверхности, независимо от того, сотрудничает ли оно на сцене или отвечает на диалоговое окно на собрании. (Примечание. Нельзя, чтобы диалоговые диалоги запускались другими приложениями, пока ваше приложение находится на стадии.) 

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Макет

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Пример, показывающий использование макета диалогов с одним столбцом." border="false":::

#### <a name="do-use-a-one-column-dialog"></a>Do: Используйте диалоговое окно с одним столбцом

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

#### <a name="do-use-a-one-column-tab"></a>Do: Используйте вкладку с одним столбцом

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

### <a name="scrolling"></a>Прокрутка

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Пример, показывающий вертикальную прокрутку на вкладке в собрании." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="Пример, показывающий вертикальную прокрутку на общем этапе собрания." border="false":::

#### <a name="do-scroll-vertically"></a>Do: Прокрутите по вертикали

Пользователи ожидают вертикального прокрутки Teams (и в других местах). Это может не применяться, если у вас есть творческий холст, например доска, которую пользователи могут панорамирование по оси x и y.

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Пример, показывающий горизонтальную прокрутку на вкладке на собрании." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="Пример, показывающий горизонтальную прокрутку на общем этапе собрания." border="false":::

#### <a name="dont-scroll-horizontally"></a>Не: прокрутите по горизонтали

Горизонтальная прокрутка не является ожидаемым поведением в Teams (включая среду собраний).

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

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="Другой пример, показывающий расширение собрания с темной темой." border="false":::

#### <a name="do-focus-on-dark-theme"></a>Do: Фокус на темной теме

Teams для темной темы, чтобы уменьшить визуальный и когнитивный шум, чтобы пользователи могли сосредоточиться на обсуждении и совместном контенте. Помните, что некоторым типам приложений (например, доска и редактирование документов) не требуется темное полотно.

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Пример, показывающий расширение собрания с цветами, которые не соответствуют теме собрания." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="Другой пример, показывающий расширение собрания с цветами, не совпадать с темой собрания." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a>Не используйте незнакомые цвета

Цвета, конфликтующие с средой собраний, могут отвлекать и казаться менее родными для Teams. Узнайте о рампе [Teams,](https://developer.microsoft.com/fluentui#/styles/web/colors/products)включая нейтральные темы вызовов.

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

### <a name="responsive-behavior"></a>Адаптируемое поведение

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="Пример, показывающий, как правильно использовать расширение собрания." border="false":::

#### <a name="do-resize-and-scale-your-app-responsively"></a>Do: Resize and scale your app responsively

Содержимое приложения должно динамически меняться и конденсироваться в небольших окнах. Сохраняйте основные навигации вашего приложения и все плавающие элементы управления видимыми.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="Пример, показывающий, как не правильно использовать расширение собрания." border="false":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a>Не: Обрезать или обрезать основные компоненты пользовательского интерфейса

Плавающая навигация и элементы управления с экрана и поиск свитка могут привести к путанице для пользователей. Содержимое приложения не должно прокручиваться горизонтально, если оно не может поместиться в iframe.

   :::column-end:::
:::row-end:::

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Настройка приложения для собраний](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
