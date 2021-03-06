---
title: Проектирование модулей задач
author: heath-hamilton
description: Узнайте, как разработать модули задач для Teams приложений и получить Microsoft Teams пользовательского интерфейса.
localization_priority: Normal
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 48e47a6c0bde0f0a3fefb8fcbfb362687ce58947
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629923"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>Проектирование модулей задач для Microsoft Teams приложения

Вы можете создавать в приложении модальные всплывающие Teams с помощью модулей задач. Используйте эту возможность для отображения богатых мультимедиа и информации или выполнения сложной задачи.

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="В примере показан модуль задач." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

Дополнительные рекомендации по разработке модулей задач, в том числе элементы, которые можно захватить и изменить по мере необходимости, можно найти в Microsoft Teams пользовательского интерфейса.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>Откройте модуль задач

Модули задач можно запускать практически из любой точки вашего приложения.

* **Вкладка.** Модуль задач можно запускать по любой ссылке в вкладке. Используйте в сценариях, в которых пользователь должен сосредоточиться на взаимодействии.
* **Бот.** Модуль задач можно запускать по ссылке внутри сообщения бота.
* **Адаптивная карта.** Модуль задач можно запускать с адаптивной карты (отправленной с расширением обмена сообщениями или ботом), когда пользователь выбирает кнопку.
* **Расширение обмена сообщениями (команды действий)**: Расширения обмена сообщениями позволяют принимать определенные меры по контенту сообщений. Выбор действия открывает модуль задач.
* **Расширение обмена сообщениями (контекст** композитного окна). В окне составить можно создать расширение обмена сообщениями, чтобы открыть модуль задач вместо обычного флайка. Резервировать модули задач для сложных взаимодействий, таких как заполнение формы.

## <a name="anatomy"></a>Анатомия

Модули задач обеспечивают гибкую поверхность для работы с хост-приложениями. Они построены с помощью iframe (desktop) или webview (мобильный), поэтому вы можете проектировать модули задач с помощью шаблонов пользовательского интерфейса (рекомендуется) или с нуля.

Они также могут быть построены с помощью базы [адаптивных](../../task-modules-and-cards/cards/design-effective-cards.md) карт, которая может быть более простым и быстрым способом облегчения распространенных сценариев (например, форм).

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса модуля задач." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Значок приложения**|
|2|**Имя приложения.** Полное имя вашего приложения.|
|3|**Заглавная:** Сделать заглавные заготки четкими и краткими. Опишите задачу, которую необходимо выполнить пользователям.
|4 |**Кнопка Закрыть:** закрывает модуль задач. Не применяет неавтные изменения в контенте приложения.|
|5 |**iframe**: Гибкое пространство, в котором размещено содержимое приложения.|
|6 |**Действия (необязательные)**: кнопки, связанные с контентом приложения.|

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-task-module-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса модуля задач на мобильных устройствах." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Заглавная:** Сделать заглавные заготки четкими и краткими. Опишите задачу, которую необходимо выполнить пользователям.
|2|**Имя приложения.** Полное имя вашего приложения.|
|3|**Кнопка Закрыть:** закрывает модуль задач. Не применяет неавтные изменения в контенте приложения.|
|4 |**веб-просмотр.** Отзывчивое пространство, в котором размещено содержимое приложения.|
|5 |**Действия (необязательные)**: кнопки, связанные с контентом приложения.|

---

## <a name="designing-with-ui-templates"></a>Проектирование с помощью шаблонов пользовательского интерфейса

Рассмотрите возможность использования шаблонов для общих макетов внутри модулей задач. Каждый из них состоит из небольших компонентов, чтобы создать элегантный, отзывчивый дизайн, который можно использовать из коробки или настроить для вашего сценария или с вашим брендом внешний вид.

* [Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.
* [Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.
* [Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.

## <a name="examples"></a>Примеры

### <a name="list"></a>List

Списки хорошо работают в модуле задач, так как их легко сканировать.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Пример списка в модуле задач." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-list.png" alt-text="Пример списка в модуле задач на мобильных устройствах." border="false":::

---

### <a name="form"></a>Form

Модули задач — отличное место для поверхности форм с последовательной вводной и входной проверкой пользователей. Адаптивные карты можно использовать как способ встраить элементы формы.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Пример формы в модуле задач." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-form.png" alt-text="Пример формы в модуле задач на мобильных устройствах." border="false":::

---

### <a name="sign-in"></a>Вход

Создайте целенаправленный поток входов или регистрации с помощью ряда модулей задач, что позволяет пользователям легко перемещаться по последовательному шагу.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Например, во время работы в модуле задач." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-sign-in.png" alt-text="Например, во время работы в модуле задач на мобильных устройствах." border="false":::

---

### <a name="media"></a>Мультимедиа

Встраить медиаконтент в модуль задач для целенаправленного просмотра.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Пример содержимого мультимедиа в модуле задач." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-media.png" alt-text="Пример содержимого мультимедиа в модуле задач на мобильных устройствах." border="false":::

---

### <a name="empty-state"></a>Пустое состояние

Используйте для приветствия, ошибок и сообщений об успехе.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Пример пустого состояния в модуле задач." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-empty-state.png" alt-text="Пример пустого состояния в модуле задач на мобильных устройствах." border="false":::

---

### <a name="image-gallery"></a>Коллекция изображений

Встраить карусель галереи в iframe (настольный) или веб-просмотр (мобильный).

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Пример галереи изображений в модуле задач." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-image-gallery.png" alt-text="Пример галереи изображений в модуле задач на мобильных устройствах." border="false":::

---

### <a name="poll"></a>Опрос

В этом примере показаны результаты опроса, запущенные с адаптивной карты. Опрос также можно поместить в модуль задач.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Пример опроса в модуле задач." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-poll.png" alt-text="Пример опроса в модуле задач на мобильных устройствах." border="false":::

---

## <a name="best-practices"></a>Рекомендации

Используйте эти рекомендации для создания качественного приложения.

### <a name="usability"></a>Usability

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Пример, показывающий передовую практику модуля задач (по одному модульу задач одновременно)." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a>Do: Используйте один модуль задач одновременно

Цель заключается в том, чтобы сосредоточить внимание пользователя на выполнении задачи в конце концов!

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (всплывает диалоговое окно в верхней части модуля задач)." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>Не: всплывай диалоговое окно поверх модуля задач

Это создает неоконченный, запутанный пользовательский интерфейс.

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>Оперативно

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Пример, показывающий передовую практику модуля задач (убедитесь, что содержимое отвечает)." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a>Do: Убедитесь, что содержимое отвечает на запросы

Несмотря на то, что адаптивные карты, которые хорошо отрисовываться в модуле задач на мобильных устройствах, если вы решите использовать iframe для содержимого приложения, убедитесь, что пользовательский интерфейс является отзывчивым и хорошо работает на всех устройствах.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (не используйте горизонтальные полоски прокрутки)." border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a>Не используйте горизонтальные столбики прокрутки

Это лучшая практика, чтобы держать контент сосредоточенным и не слишком длительным. Если прокрутка необходима, прокрутите по вертикали, а не по горизонтали.

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>Простота

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Пример, показывающий передовую практику модуля задач (не нужно его кратко)." border="false":::

#### <a name="do-keep-it-short"></a>Do: Keep it short

Вы можете легко создать многоступенчатый мастер, но это не обязательно означает, что вы должны! Многоэкранный модуль задач может быть проблематичным, так как входящие сообщения отвлекают и соблазняют пользователей выйти. Если ваша задача действительно задействована, выполните полную веб-страницу, а не модуль задач.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (не имеют длительных взаимодействий)." border="false":::

#### <a name="dont-have-long-interactions"></a>Don't: Have long interactions

Постарайтесь сохранить ваши взаимодействия короткими и до точки.

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>Сообщения об ошибках

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Пример, показывающий передовую практику модуля задач (использование сообщений об ошибках)." border="false":::

#### <a name="do-use-inline-error-messages"></a>Do: Использование сообщений об ошибках с помощью inline

См. шаблон пользовательского интерфейса форм для инструкций по обработке ошибок.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (поместить сообщения об ошибке в диалоги)." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a>Не: помещай сообщения об ошибках в диалоговые личные

Не всплывай сообщение об ошибке в диалоговом окну над модулем задач. Это создает запутанный пользовательский интерфейс.

   :::column-end:::
:::row-end:::
