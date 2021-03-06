---
title: Разработка вкладок для настольных компьютеров, веб-сайтов и мобильных устройств
description: Узнайте, как создать вкладку Teams для настольных, веб-и мобильных устройств и получить Microsoft Teams пользовательского интерфейса.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f1823a064cd182d0271aa97bef58ec724c7819b3
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721845"
---
# <a name="design-your-tab-for-microsoft-teams"></a>Разработка вкладки для Microsoft Teams

Вкладка — это большое полотно для контента приложения. Для руководства разработкой приложения в следующих сведениях описывается и иллюстрируется, как люди могут добавлять, использовать и управлять вкладками в Teams.

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

В наборе пользовательского интерфейса можно найти всесторонние рекомендации по разработке вкладок Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости. Набор пользовательского интерфейса также имеет важные темы, такие как доступность и размер отзывчивый, которые здесь не охватываются.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>Добавление вкладки

Вы можете добавить вкладку из Teams магазина (AppSource) или в одном из следующих контекстов:

* Чат
* Канал
* Собрание (до, во время или после собрания)

# <a name="desktop"></a>[Desktop](#tab/desktop)

В следующем примере показано, как пользователи могут добавлять вкладку в канал.

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="В примере показана вкладка, добавляемая в канал." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

Пользователи могут получить доступ к вкладками, выбрав кнопку **More** в канале (пример ниже) или чат, в котором они были добавлены.

:::image type="content" source="../../assets/images/tabs/mobile-design-access-tab.png" alt-text="В примере показана вкладка для мобильных устройств, добавляемая в канал." border="false":::

---

## <a name="set-up-a-tab"></a>Настройка вкладки

Существует короткий процесс настройки, чтобы добавить приложение в качестве канала, чата или вкладки для собраний. Это зависит в основном от вас. Например, вы можете иметь описание использования приложения и некоторых необязательных параметров. Если необходимо проверить подлинность пользователей, включив здесь шаг для регистрации.

### <a name="tab-configuration-dialog"></a>Диалоговое окно конфигурации вкладок

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="В примере показан модальный способ конфигурации вкладок." border="false":::

### <a name="anatomy-tab-configuration-dialog"></a>Анатомия: диалоговое окно конфигурации tab

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса модуля конфигурации вкладок." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Логотип приложения:** логотип приложения полного цвета вашего приложения.|
|2|**Имя приложения.** Полное имя вашего приложения.|
|3|**iframe:** адаптивный пробел для контента приложения (например, параметры вкладки или проверка подлинности).|
|4 |**О ссылке.** Открывает диалоговое окно, в котором отображаются дополнительные сведения о приложении, такие как полное описание, разрешения, необходимые приложению, а также ссылки на политику конфиденциальности и условия службы.|
|5 |**Кнопка Закрыть:** закрывает диалоговое окно.|
|6 |**Оповещайте** членов группы: диалоговое окно спрашивает пользователей, хотят ли они создать сообщение, позволяя другим узнать, что они добавили вкладку.|
|7 |**Кнопка**"Назад": переходит к предыдущему шагу в зависимости от того, где открылся диалоговое окно.|
|8 |**Сохранить кнопку**: Завершает установку вкладок.|

### <a name="tab-authentication-with-single-sign-on"></a>Проверка подлинности вкладок с одним входом

Вы можете добавить шаг, на котором пользователи должны сначала войти с учетными данными Майкрософт. Этот метод проверки подлинности называется одним входом (SSO).

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="В примере показан экран проверки подлинности вкладок." border="false":::

### <a name="design-a-tab-setup-with-ui-templates"></a>Разработка установки вкладок с помощью шаблонов пользовательского интерфейса

Используйте один из следующих Teams пользовательского интерфейса для разработки интерфейса установки вкладок:

* [Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.
* [Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.
* [Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.

## <a name="view-a-tab"></a>Просмотр вкладки

Вкладки предоставляют полноэкранный веб-опыт в Teams, где можно отобразить совместное содержимое— такие доски задач и панели мониторинга и важные сведения.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="В примере показана вкладка с доской задач." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab.png" alt-text="В примере показана вкладка для мобильных устройств с доской задач." border="false":::

---

### <a name="anatomy-tab"></a>Анатомия: Вкладка

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса вкладки." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Имя вкладки.** Метка навигации для вкладки.|
|2|**Переполнение вкладки:** открывает действия вкладки, такие как переименование и удаление.|
|3|**Чат tab:** открывает чат справа, позволяя пользователям беседовать рядом с содержимым.|
|4 |**iframe:** отображает содержимое приложения.|

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса вкладки." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Имя вкладки.** Метка навигации для вкладки.|
|2|**Вкладка чат**: Открывает чат, который позволяет пользователям иметь беседу рядом с содержимым.|
|3|**веб-просмотр.** Отображает содержимое приложения.|

---

### <a name="designing-a-tab-with-ui-templates-and-advanced-components"></a>Разработка вкладки с шаблонами пользовательского интерфейса и расширенными компонентами

Используйте один из следующих Teams и компонентов для разработки работы вкладки:

* [Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.
* [Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.
* [Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.
* [Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.
* [Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.
* [Левый nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav). Компонент левого nav может помочь если ваша вкладка требует некоторой навигации. В общем, вы должны сохранить навигацию вкладок до минимума.

## <a name="use-a-tab-to-collaborate"></a>Использование вкладки для совместной работы

Вкладки помогают упростить беседы о контенте в центральном расположении.

### <a name="thread-discussion"></a>Обсуждение потоков

Пользователи могут автоматически размещать сообщения в канале или чате после того, как они добавит новую вкладку. Это не только сообщает членам команды о новом содержимом и предоставляет ссылку на вкладку, но и позволяет пользователям начать говорить о вкладке.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="В примере показана вкладка, обсуждаемая в потоке канала." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-channel.png" alt-text="В примере показана вкладка для мобильных устройств, которая обсуждается в потоке канала." border="false":::

---

### <a name="tab-chat"></a>Чат Tab

Пользователи могут беседуть рядом с просматриваемым контентом вкладок. На рабочем столе чат открывается на стороне контента приложения.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="В примере показана вкладка с открытой в правой части чатом." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-side-chat.png" alt-text="В примере показана вкладка для мобильных устройств с областью чата в контексте." border="false":::

---

### <a name="permissions-and-role-based-views"></a>Разрешения и представления на основе ролей

Опыт вкладки может быть разным для пользователей в зависимости от их разрешений. Например, один пользователь может получить доступ к вкладке, не входя. Другой пользователь, однако, должен войти и увидеть немного другое содержимое.

## <a name="manage-a-tab"></a>Управление вкладками

Можно включить параметры переименования, удаления или изменения вкладки.

### <a name="anatomy-tab-menu"></a>Анатомия: меню Tab

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса меню вкладок." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Параметры:**(Необязательный) позволяет пользователям изменять параметры вкладки после ее добавления.|
|2|**Переименование.** Пользователи могут дать вкладке имя, значимое каналу, чату или собранию.|
|3|**Удаление.** Удаляет вкладку из канала, чата или собрания.|

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-manage-tab-menu-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса меню вкладок для мобильных устройств." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Откройте в браузере**: Открывает приложение в браузере по умолчанию устройства.|
|2|**Скопируйте** ссылку. Пользователи могут копировать и делиться ссылкой на вкладку.|
|3|**Параметры:**(Необязательный) Изменение параметров вкладки после ее добавления.|
|4 |**Переименование.** Пользователи могут дать вкладке имя, значимое каналу, чату или собранию.|
|5 |**Удаление.** Удаляет вкладку из канала, чата или собрания.|

---

## <a name="tab-notifications-and-deep-linking"></a>Уведомления вкладки и глубокая связь

Вы можете отправить сообщение с глубокой ссылкой на вкладку. Например, на карточке показан сводка данных об ошибках, которые пользователь может выбрать, чтобы увидеть всю ошибку на вкладке. Отправка сообщений об активности вкладок повышает осведомленность без явного уведомления всех пользователей (например, действий без шума). Вы также можете @mention определенных пользователей, если это необходимо.

Уведомлять пользователей о действии вкладок одним из следующих способов:

* **Бот.** Этот метод предпочтительный, особенно если поток вкладок ориентирован. Беседа с потоками вкладки перемещается в вид как недавно активная. Этот метод также позволяет ухищрения при отправлении уведомления.
* **Сообщение.** Сообщение появляется в ленте действий пользователя с глубокой [ссылкой на вкладку](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).

## <a name="best-practices"></a>Рекомендации

Используйте эти рекомендации для создания качественного приложения:

### <a name="collaboration"></a>Совместная работа

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="На рисунке показано, что делать с дизайном навигации вкладок." border="false":::

#### <a name="do-facilitate-conversation"></a>Do: Облегчить беседу

Включай содержимое и компоненты, о которых можно говорить. Если он не вписывается в контекст чата, канала или собрания, он не входит в вкладку.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="В примере показано, что не нужно делать с дизайном навигации вкладок." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>Не: Обрабатывайте вкладку, как и любую другую веб-страницу

Вкладка — это не веб-страницы, которые кто-то может просматривать один раз. Вкладка должна отображать наиболее важные и релевантные материалы, необходимые для совместной работы.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Навигация

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Пример, показывающий, что делать с дизайном навигации вкладок." border="false":::

#### <a name="do-limit-tasks-and-data"></a>Do: Ограничение задач и данных

Вкладки работают лучше всего, если они уламывкают конкретные потребности. Включаем ограниченный набор задач и данных, соответствующих группе или группе.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Иллюстрация, показывающая, что не нужно делать с дизайном навигации вкладок." border="false":::

#### <a name="dont-embed-your-entire-app"></a>Не: встраить все приложение

Использование вкладки для отображения всего приложения с многоуровневой навигацией и сложными взаимодействиями приводит к перегрузке информации.

   :::column-end:::
:::row-end:::

### <a name="setup"></a>Настройка

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Иллюстрация, показывающая, что делать с дизайном установки вкладок." border="false":::

#### <a name="do-keep-it-simple"></a>Do: Keep it simple

Если вашему приложению требуется проверка подлинности, попробуйте интегрировать microsoft single sign-on (SSO) для более плавного входного опытом. Кроме того, только включить необходимые сведения и шаги, чтобы добавить вкладку.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Иллюстрация, показывающая, что не нужно делать с дизайном установки вкладок." border="false":::

#### <a name="dont-have-too-many-steps"></a>Не: слишком много действий

Удалите ненужные действия для добавления вкладки.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Темы

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Иллюстрация, показывающая, что делать с темой вкладок." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Do: Воспользоваться преимуществами Teams цветовых маркеров

Каждая Teams имеет свою цветовую схему. Чтобы автоматически обрабатывать изменения темы, используйте маркеры цвета <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(Fluent UI)</a> в своем дизайне.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Иллюстрация, показывающая, что не нужно делать с темой вкладок." border="false":::

#### <a name="dont-hard-code-color-values"></a>Не: значения цвета жесткого кода

Если вы не используете маркеры Teams цвета, ваши проекты будут менее масштабируемыми и у вас будет больше времени для управления.

   :::column-end:::
:::row-end:::
