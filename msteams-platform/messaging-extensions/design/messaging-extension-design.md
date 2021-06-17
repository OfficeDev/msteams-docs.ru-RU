---
title: Проектирование расширения обмена сообщениями
description: Узнайте, как создать расширение Teams обмена сообщениями и получить Microsoft Teams пользовательского интерфейса.
keywords: Рекомендации по разработке рекомендаций по расширению справочных сообщений в командах советы по рекомендациям по рекомендациям
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: fd870d8e10ef74c36f8f6d145d48980f53e9303c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631074"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>Разработка расширения Microsoft Teams обмена сообщениями

Расширения обмена сообщениями — это ярлыки для вставки контента приложения или действия в сообщении, не переходя от беседы.
Для руководства разработкой приложения в следующих сведениях описывается и иллюстрируется возможность добавления, использования и управления расширениями обмена сообщениями в Teams.

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

В наборе пользовательского интерфейса можно найти всесторонние рекомендации по расширению обмена сообщениями Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>Добавление расширения обмена сообщениями

Расширение обмена сообщениями можно добавить в следующих Teams контекстах:

* Из Teams магазина.
* В канале, чате или собрании (до, во время и после) рядом с полем составить. Стоит отметить, что если в одном из этих мест добавлено расширение обмена сообщениями, его можно использовать только в этом контексте.

В следующем примере показано, как добавить расширение обмена сообщениями в канале:

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="В примере показано, как добавить расширение обмена сообщениями рядом с окне составить в канале." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="В примере показано, как добавить расширение обмена сообщениями рядом с окне составить в канале на мобильном телефоне." border="false":::

---

## <a name="set-up-a-messaging-extension"></a>Настройка расширения обмена сообщениями

Проверка подлинности не является обязательной, но если ваше приложение является чем-то вроде средства отслеживания билетов, для использования расширения обмена сообщениями могут потребоваться люди.

Чтобы обеспечить согласованность Teams приложений, нельзя настроить экран входного знака. При использовании проверки подлинности с одним входом (SSO) пользователи автоматически подписываются.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="В примере показан экран установки расширения обмена сообщениями с кнопкой вход." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="В примере показан экран установки расширения обмена сообщениями с кнопкой вход на мобильный телефон." border="false":::

---

## <a name="types-of-messaging-extensions"></a>Типы расширений обмена сообщениями

Расширения обмена сообщениями могут иметь команды поиска, команды действий или оба. Ваши команды зависят от функций приложения и от того, как они подходят Teams случаях.

### <a name="search-commands"></a>Команды поиска

С помощью команд поиска люди могут использовать расширение обмена сообщениями для быстрого поиска внешнего контента и вставки в сообщение. Команды поиска обычно доступны в окне составить. Например, вы можете начать или добавить в обсуждение, поделившись частью контента, не покидая Teams.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="В примере показано расширение обмена сообщениями на основе поиска, запущенное из окна составить." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="В примере показано расширение обмена сообщениями на основе поиска, запущенное из окна составить на мобильных устройствах." border="false":::

---

#### <a name="compose-box-layout-options"></a>Параметры композитного макета полей

У вас есть несколько вариантов отображения результатов поиска расширения обмена сообщениями, включая [представления списков и сетки.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="На иллюстрациях показаны параметры макета результатов поиска расширения обмена сообщениями." border="false":::

### <a name="action-commands"></a>Команды действий

Команды действий позволяют пользователям запускать действия и обрабатывать запросы во внешних службах в Teams. Например, если приложение отслеживает заказы, пользователь может создать новый порядок с помощью содержимого сообщения коллеги прямо в чате.

Расширения обмена сообщениями на основе действий часто требуют, чтобы пользователи заполняли форму или другую конфигурацию в модале. Эти возможности можно создавать с помощью [модулей задач.](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="open-a-messaging-extension"></a>Откройте расширение обмена сообщениями

Основной контекст, в котором люди используют расширения обмена сообщениями, — это шкатулка, а также сообщения или сообщения.

### <a name="from-the-compose-box"></a>Из окне композит

После добавления пользователи могут открыть расширение обмена сообщениями, выбрав значок приложения под полем составить. В этих примерах расширение имеет команды поиска и действий.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из окна составить." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из окна составить на мобильном телефоне." border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a>Из сообщения чата или сообщения канала

После добавления пользователи могут выбрать значок **More** в сообщении чата или сообщении канала, чтобы найти команды действий :::image type="icon" source="../../assets/icons/teams-client-more.png"::: вашего расширения. Расширение может быть перечислены в **статье Дополнительные действия,** основанные на использовании.

> [!NOTE]
> Поддержка дополнительных действий из сообщения чата или сообщения канала недоступна на Microsoft Teams платформе. 

#### <a name="chat-message"></a>Сообщение чата

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из сообщения чата." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из сообщения чата на мобильном телефоне." border="false":::

---

#### Channel post

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false":::

---

## <a name="use-a-messaging-extension"></a>Использование расширения обмена сообщениями

В следующих сценариях покажут основные способы использования расширений обмена сообщениями.

### <a name="insert-content-into-a-message"></a>Вставка контента в сообщение

**1. Выберите расширение обмена сообщениями.** Пользователи могут искать содержимое, которое они хотят поделиться из окна составить.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="В примере показано, как пользователь ищет содержимое для вставки из окне композитной записи." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="В примере показано, как пользователь ищет контент для вставки из окна записи на мобильном телефоне." border="false":::

---

**2. Вставьте содержимое**. После публикации другие могут отвечать или выбирать содержимое, чтобы увидеть дополнительные сведения в приложении.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="В примере показана публикация контента пользователя в разговоре с каналом." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="В примере показана публикация контента пользователя в разговоре по каналу на мобильном телефоне." border="false":::

---

### <a name="take-action-on-a-message"></a>Действие по сообщению

**1. Выберите расширение обмена сообщениями.** Ваше приложение может включать одну или несколько команд действий.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="В примере показано, как пользователь выбирает команду действий по расширению обмена сообщениями." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="В примере показано, как пользователь выбирает команду действий по расширению обмена сообщениями на мобильном телефоне." border="false":::

---

**2. Завершить действие**. Ваше приложение может получать и обрабатывать любое содержимое или данные, отправленные действием сообщения. Это позволяет пользователям оставаться в беседе и, в следующем примере, не беспокоиться о вводе сведений непосредственно в вашем приложении.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Пример действий по сообщению." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="Пример действий по сообщению на мобильных устройствах." border="false":::

---

### <a name="preview-links"></a>Предварительные ссылки

Расширения обмена сообщениями также позволяют вставлять богатые ссылки из распознаемого URL-адреса в сообщение (эта возможность называется [unfurling link unfurling.)](../../messaging-extensions/how-to/link-unfurling.md)

**1. Вклеить распознаемую ссылку** в поле составить.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="В примере показано, как пользователь вклеит ссылку в поле компоста." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="В примере показано, как пользователь вклеит ссылку в поле компоста на мобильный телефон." border="false":::

---

**2. Вставьте содержимое**. Если ваше приложение распознает URL-адрес в окне композит, оно отрисовка ссылки в качестве карточки, которая обеспечивает богатый контентом предварительный просмотр веб-контента. [(Дополнительные сведения](../../task-modules-and-cards/cards/design-effective-cards.md) см. в рекомендациях по разработке адаптивных карт.)

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="В примере показано, как URL-адрес, так как он распознается вашим приложением, содержит в окне композитного контента некоторое содержимое." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="В примере показано, как URL-адрес, так как он распознается вашим приложением, содержит некоторые материалы в поле составить на мобильных устройствах." border="false":::

---

## <a name="manage-a-messaging-extension"></a>Управление расширением обмена сообщениями

Щелкнув правой кнопкой мыши значок, пользователи могут прикрепить, удалить или настроить расширение обмена сообщениями.

## <a name="anatomy"></a>Анатомия

### <a name="messaging-extension-in-the-compose-box"></a>Расширение обмена сообщениями в окне составить

В следующем примере можно привести расширение обмена сообщениями, открытое из окна составить.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса расширения обмена сообщениями в окне составить." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Логотип приложения.** Значок цвета логотипа приложения.|
|2|**Имя приложения.** Полное имя вашего приложения.|
|3|**Значок меню action commands (необязательный)**: Открывает список команд действий для расширения обмена сообщениями (если вы указываете их).
|4 |**Поле поиска.** Позволяет пользователям находить содержимое приложения, которое они хотят вставить.|
|5 |**Меню Tab (необязательный)**: предоставляет несколько категорий контента.|
|6 |**Меню команд действий (необязательный)**: отображает список команд действий (если указаны какие-либо).|
|7 |**Содержимое приложения.** В первую очередь для отображения результатов поиска. В этом примере используется макет списка (макет сетки — это другой вариант).|
|8 |**Логотип приложения.** Значок контура логотипа приложения.|

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса расширения обмена сообщениями в поле составить на мобильных устройствах." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Имя приложения.** Полное имя вашего приложения.|
|2|**Значок меню action commands (необязательный)**: Открывает список команд действий для расширения обмена сообщениями (если вы указываете их).
|3|**Поле поиска.** Позволяет пользователям находить содержимое приложения, которое они хотят вставить.|
|4 |**Меню Tab (необязательный)**: предоставляет несколько категорий контента.|
|5 |**Меню команд действий (необязательный)**: отображает список команд действий (если указаны какие-либо).|
|6 |**Содержимое приложения.** В первую очередь для отображения результатов поиска.|

---

### <a name="messaging-extension-management-menu"></a>Меню управления расширением обмена сообщениями

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса меню управления расширением обмена сообщениями." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Unpin.** Доступно, если пользователь прикрепил приложение.|
|2|**Удаление.** Удаляет расширение обмена сообщениями из канала, чата или собрания.|

## <a name="best-practices"></a>Рекомендации

Используйте эти рекомендации для создания качественного приложения.

### <a name="setup-and-general-usage"></a>Настройка и общее использование

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Пример установки и общего использования." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>Do: Интеграция с одним входом

SSO упрощает процесс регистрации, быстрее и обеспечивает безопасность. Кроме того, если пользователь уже зарегистрировался в вашем личном приложении, для доступа к расширению обмена сообщениями также не нужно снова входить.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Пример интеграции с одним входом." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>Не: отбирайте пользователей из беседы

Расширения обмена сообщениями — это ярлыки, которые, как предполагается, уменьшают переключение контекста. Например, расширение не должно направлять пользователей на веб-страницу за пределами Teams.

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>Do: Highlight your messaging extension

Расширения обмена сообщениями не всегда легко найти. Включите скриншоты использования этого приложения на странице сведения о приложении. Если в вашем приложении также есть бот, вы можете включить документацию по расширению обмена сообщениями в приветственный тур бота.

### <a name="templating"></a>Templating

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Пример шаблона." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>Do: по возможности Teams некоторые работы по проектированию

Если это имеет смысл для случаев использования, рассмотрите возможность создания расширения обмена сообщениями на основе поиска. Teams эти типы расширений со встроенной темой и доступностью.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Пример обработки работ по проектированию." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>Не: встраить все приложение в модуль задач

Если расширение обмена сообщениями требует команд действий, сохраняйте простой модуль задач и отображайте только компоненты, необходимые для выполнения действия.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Темы

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Пример на теме." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Do: Воспользоваться преимуществами Teams цветовых маркеров

Каждая Teams имеет свою цветовую схему. Чтобы автоматически обрабатывать изменения темы, используйте маркеры цвета <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(Fluent UI)</a> в своем дизайне.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Пример с цветными маркерами." border="false":::

#### <a name="dont-hard-code-color-values"></a>Не: значения цвета жесткого кода

Если вы не используете маркеры Teams цвета, ваши проекты будут менее масштабируемыми и у вас будет больше времени для управления.

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Действия

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Пример действий." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>Do: Включить команды действий, которые в контексте являются смыслом

Действия сообщения должны относиться к тем, на что смотрит пользователь. Например, укажи пользователям ярлык для создания проблемы или рабочих элементов с помощью текста в чьей-либо публикации.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Пример команд действий." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>Не: включайте не контекстуальные команды действий

Действие сообщения для **просмотра панели мониторинга** может показаться отключенным от большинства бесед.

   :::column-end:::
:::row-end:::

### <a name="searches"></a>Поиск

#### <a name="do-show-search-results-while-typing"></a>Do: Показать результаты поиска при вводе

Предоставление предлагаемых результатов поиска при введите пользователей. Они могут быстрее находить нужный контент с минимальным количеством символов.

#### <a name="dont-require-users-to-submit-a-query"></a>Не: требовать от пользователей отправки запроса

Вы можете заставить пользователей нажать клавишу или выбрать кнопку для отправки запросов в ваше приложение. Хотя это может быть проще в службе служб приложений, люди могут быть смущены тем, что они не видят результатов поиска в режиме реального времени, как они введите.

#### <a name="do-consider-zero-term-queries"></a>Do: Рассмотрите запросы с нулевым сроком

Например, перед тем, как пользователь записывает что-либо в поле поиска, отобразите то, что он последний раз просматривал в вашем приложении. Вполне возможно, что они хотят вставить этот контент в беседу.
