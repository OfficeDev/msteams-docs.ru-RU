---
title: Разработка вкладки для настольных компьютеров и веб-страниц
description: Узнайте, как создать вкладку Teams (настольный компьютер и веб) и получить Microsoft Teams пользовательского интерфейса.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 38eb7e400de63beb0d2840ee573bbfd16299cfbd
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644743"
---
# <a name="designing-your-tab-for-microsoft-teams"></a><span data-ttu-id="fb581-103">Разработка вкладки для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fb581-103">Designing your tab for Microsoft Teams</span></span>

<span data-ttu-id="fb581-104">Вкладка — это большое полотно для контента приложения.</span><span class="sxs-lookup"><span data-stu-id="fb581-104">A tab is a large canvas for your app content.</span></span> <span data-ttu-id="fb581-105">Для руководства разработкой приложения в следующих сведениях описывается и иллюстрируется, как люди могут добавлять, использовать и управлять вкладками в Teams.</span><span class="sxs-lookup"><span data-stu-id="fb581-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="fb581-106">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fb581-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="fb581-107">В наборе пользовательского интерфейса можно найти всесторонние рекомендации по разработке вкладок Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="fb581-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="fb581-108">Набор пользовательского интерфейса также имеет важные темы, такие как доступность и размер отзывчивый, которые здесь не охватываются.</span><span class="sxs-lookup"><span data-stu-id="fb581-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb581-109">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="fb581-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="fb581-110">Добавление вкладки</span><span class="sxs-lookup"><span data-stu-id="fb581-110">Add a tab</span></span>

<span data-ttu-id="fb581-111">Вы можете добавить вкладку из Teams магазина (AppSource) или в одном из следующих контекстов:</span><span class="sxs-lookup"><span data-stu-id="fb581-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="fb581-112">Чат</span><span class="sxs-lookup"><span data-stu-id="fb581-112">Chat</span></span>
* <span data-ttu-id="fb581-113">Канал</span><span class="sxs-lookup"><span data-stu-id="fb581-113">Channel</span></span>
* <span data-ttu-id="fb581-114">Собрание (до, во время или после собрания)</span><span class="sxs-lookup"><span data-stu-id="fb581-114">Meeting (before, during, or after the meeting)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fb581-115">Desktop</span><span class="sxs-lookup"><span data-stu-id="fb581-115">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="fb581-116">В следующем примере показано, как пользователи могут добавлять вкладку в канал.</span><span class="sxs-lookup"><span data-stu-id="fb581-116">The following example shows how users can add a tab in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="В примере показана вкладка, добавляемая в канал." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fb581-118">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="fb581-118">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="fb581-119">Пользователи могут получить доступ к вкладками, выбрав кнопку **More** в канале (пример ниже) или чат, в котором они были добавлены.</span><span class="sxs-lookup"><span data-stu-id="fb581-119">Users can access tabs by selecting the **More** button in the channel (example below) or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-design-access-tab.png" alt-text="В примере показана вкладка для мобильных устройств, добавляемая в канал." border="false":::

---

## <a name="set-up-a-tab"></a><span data-ttu-id="fb581-121">Настройка вкладки</span><span class="sxs-lookup"><span data-stu-id="fb581-121">Set up a tab</span></span>

<span data-ttu-id="fb581-122">Существует короткий процесс настройки, чтобы добавить приложение в качестве канала, чата или вкладки для собраний. Это зависит в основном от вас.</span><span class="sxs-lookup"><span data-stu-id="fb581-122">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="fb581-123">Например, вы можете иметь описание использования приложения и некоторых необязательных параметров.</span><span class="sxs-lookup"><span data-stu-id="fb581-123">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="fb581-124">Если необходимо проверить подлинность пользователей, включив здесь шаг для регистрации.</span><span class="sxs-lookup"><span data-stu-id="fb581-124">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-dialog"></a><span data-ttu-id="fb581-125">Диалоговое окно конфигурации вкладок</span><span class="sxs-lookup"><span data-stu-id="fb581-125">Tab configuration dialog</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="В примере показан модальный способ конфигурации вкладок." border="false":::

### <a name="anatomy-tab-configuration-dialog"></a><span data-ttu-id="fb581-127">Анатомия: диалоговое окно конфигурации tab</span><span class="sxs-lookup"><span data-stu-id="fb581-127">Anatomy: Tab configuration dialog</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса модуля конфигурации вкладок." border="false":::

|<span data-ttu-id="fb581-129">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fb581-129">Counter</span></span>|<span data-ttu-id="fb581-130">Описание</span><span class="sxs-lookup"><span data-stu-id="fb581-130">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fb581-131">1</span><span class="sxs-lookup"><span data-stu-id="fb581-131">1</span></span>|<span data-ttu-id="fb581-132">**Логотип приложения:** логотип приложения полного цвета вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="fb581-132">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="fb581-133">2</span><span class="sxs-lookup"><span data-stu-id="fb581-133">2</span></span>|<span data-ttu-id="fb581-134">**Имя приложения.** Полное имя вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="fb581-134">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="fb581-135">3</span><span class="sxs-lookup"><span data-stu-id="fb581-135">3</span></span>|<span data-ttu-id="fb581-136">**iframe:** адаптивный пробел для контента приложения (например, параметры вкладки или проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="fb581-136">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="fb581-137">4 </span><span class="sxs-lookup"><span data-stu-id="fb581-137">4</span></span>|<span data-ttu-id="fb581-138">**О ссылке.** Открывает диалоговое окно, в котором отображаются дополнительные сведения о приложении, такие как полное описание, разрешения, необходимые приложению, а также ссылки на политику конфиденциальности и условия службы.</span><span class="sxs-lookup"><span data-stu-id="fb581-138">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>|
|<span data-ttu-id="fb581-139">5 </span><span class="sxs-lookup"><span data-stu-id="fb581-139">5</span></span>|<span data-ttu-id="fb581-140">**Кнопка Закрыть:** закрывает диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="fb581-140">**Close button**: Closes the dialog.</span></span>|
|<span data-ttu-id="fb581-141">6 </span><span class="sxs-lookup"><span data-stu-id="fb581-141">6</span></span>|<span data-ttu-id="fb581-142">**Оповещайте** членов группы: диалоговое окно спрашивает пользователей, хотят ли они создать сообщение, позволяя другим узнать, что они добавили вкладку.</span><span class="sxs-lookup"><span data-stu-id="fb581-142">**Notify team members option**: The dialog asks users if they want to create a post letting others know they added a tab.</span></span>|
|<span data-ttu-id="fb581-143">7 </span><span class="sxs-lookup"><span data-stu-id="fb581-143">7</span></span>|<span data-ttu-id="fb581-144">**Кнопка**"Назад": переходит к предыдущему шагу в зависимости от того, где открылся диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="fb581-144">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="fb581-145">8 </span><span class="sxs-lookup"><span data-stu-id="fb581-145">8</span></span>|<span data-ttu-id="fb581-146">**Сохранить кнопку**: Завершает установку вкладок.</span><span class="sxs-lookup"><span data-stu-id="fb581-146">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="fb581-147">Проверка подлинности вкладок с одним входом</span><span class="sxs-lookup"><span data-stu-id="fb581-147">Tab authentication with single sign-on</span></span>

<span data-ttu-id="fb581-148">Вы можете добавить шаг, на котором пользователи должны сначала войти с учетными данными Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="fb581-148">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="fb581-149">Этот метод проверки подлинности называется одним входом (SSO).</span><span class="sxs-lookup"><span data-stu-id="fb581-149">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="В примере показан экран проверки подлинности вкладок." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="fb581-151">Проектирование установки вкладок с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="fb581-151">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="fb581-152">Используйте один из следующих Teams пользовательского интерфейса для разработки интерфейса установки вкладок:</span><span class="sxs-lookup"><span data-stu-id="fb581-152">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="fb581-153">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="fb581-153">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="fb581-154">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="fb581-154">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="fb581-155">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="fb581-155">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="fb581-156">Просмотр вкладки</span><span class="sxs-lookup"><span data-stu-id="fb581-156">View a tab</span></span>

<span data-ttu-id="fb581-157">Вкладки предоставляют полноэкранный веб-опыт в Teams, где можно отобразить совместное содержимое— такие доски задач и панели мониторинга и важные сведения.</span><span class="sxs-lookup"><span data-stu-id="fb581-157">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fb581-158">Desktop</span><span class="sxs-lookup"><span data-stu-id="fb581-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="В примере показана вкладка с доской задач." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fb581-160">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="fb581-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab.png" alt-text="В примере показана вкладка для мобильных устройств с доской задач." border="false":::

---

### <a name="anatomy-tab"></a><span data-ttu-id="fb581-162">Анатомия: Вкладка</span><span class="sxs-lookup"><span data-stu-id="fb581-162">Anatomy: Tab</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fb581-163">Desktop</span><span class="sxs-lookup"><span data-stu-id="fb581-163">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса вкладки." border="false":::

|<span data-ttu-id="fb581-165">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fb581-165">Counter</span></span>|<span data-ttu-id="fb581-166">Описание</span><span class="sxs-lookup"><span data-stu-id="fb581-166">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fb581-167">1</span><span class="sxs-lookup"><span data-stu-id="fb581-167">1</span></span>|<span data-ttu-id="fb581-168">**Имя вкладки.** Метка навигации для вкладки.</span><span class="sxs-lookup"><span data-stu-id="fb581-168">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="fb581-169">2</span><span class="sxs-lookup"><span data-stu-id="fb581-169">2</span></span>|<span data-ttu-id="fb581-170">**Переполнение вкладки:** открывает действия вкладки, такие как переименование и удаление.</span><span class="sxs-lookup"><span data-stu-id="fb581-170">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="fb581-171">3</span><span class="sxs-lookup"><span data-stu-id="fb581-171">3</span></span>|<span data-ttu-id="fb581-172">**Чат tab:** открывает чат справа, позволяя пользователям беседовать рядом с содержимым.</span><span class="sxs-lookup"><span data-stu-id="fb581-172">**Tab chat**: Opens a chat to the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="fb581-173">4 </span><span class="sxs-lookup"><span data-stu-id="fb581-173">4</span></span>|<span data-ttu-id="fb581-174">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="fb581-174">**iframe**: Displays your app content.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="fb581-175">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="fb581-175">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса вкладки." border="false":::

|<span data-ttu-id="fb581-177">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fb581-177">Counter</span></span>|<span data-ttu-id="fb581-178">Описание</span><span class="sxs-lookup"><span data-stu-id="fb581-178">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fb581-179">1</span><span class="sxs-lookup"><span data-stu-id="fb581-179">1</span></span>|<span data-ttu-id="fb581-180">**Имя вкладки.** Метка навигации для вкладки.</span><span class="sxs-lookup"><span data-stu-id="fb581-180">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="fb581-181">2</span><span class="sxs-lookup"><span data-stu-id="fb581-181">2</span></span>|<span data-ttu-id="fb581-182">**Вкладка чат**: Открывает чат, который позволяет пользователям иметь беседу рядом с содержимым.</span><span class="sxs-lookup"><span data-stu-id="fb581-182">**Tab chat**: Opens a chat that allows users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="fb581-183">3</span><span class="sxs-lookup"><span data-stu-id="fb581-183">3</span></span>|<span data-ttu-id="fb581-184">**веб-просмотр.** Отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="fb581-184">**webview**: Displays your app content.</span></span>|

---

### <a name="designing-a-tab-with-ui-templates-and-advanced-components"></a><span data-ttu-id="fb581-185">Разработка вкладки с шаблонами пользовательского интерфейса и расширенными компонентами</span><span class="sxs-lookup"><span data-stu-id="fb581-185">Designing a tab with UI templates and advanced components</span></span>

<span data-ttu-id="fb581-186">Используйте один из следующих Teams и компонентов для разработки работы вкладки:</span><span class="sxs-lookup"><span data-stu-id="fb581-186">Use one of the following Teams templates and components to help design your tab experience:</span></span>

* <span data-ttu-id="fb581-187">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="fb581-187">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="fb581-188">[Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="fb581-188">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="fb581-189">[Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.</span><span class="sxs-lookup"><span data-stu-id="fb581-189">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="fb581-190">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="fb581-190">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="fb581-191">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="fb581-191">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="fb581-192">[Левый nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav). Компонент левого nav может помочь если ваша вкладка требует некоторой навигации.</span><span class="sxs-lookup"><span data-stu-id="fb581-192">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="fb581-193">В общем, вы должны сохранить навигацию вкладок до минимума.</span><span class="sxs-lookup"><span data-stu-id="fb581-193">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="fb581-194">Использование вкладки для совместной работы</span><span class="sxs-lookup"><span data-stu-id="fb581-194">Use a tab to collaborate</span></span>

<span data-ttu-id="fb581-195">Вкладки помогают упростить беседы о контенте в центральном расположении.</span><span class="sxs-lookup"><span data-stu-id="fb581-195">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="fb581-196">Обсуждение потоков</span><span class="sxs-lookup"><span data-stu-id="fb581-196">Thread discussion</span></span>

<span data-ttu-id="fb581-197">Пользователи могут автоматически размещать сообщения в канале или чате после того, как они добавит новую вкладку. Это не только сообщает членам команды о новом содержимом и предоставляет ссылку на вкладку, но и позволяет пользователям начать говорить о вкладке.</span><span class="sxs-lookup"><span data-stu-id="fb581-197">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fb581-198">Desktop</span><span class="sxs-lookup"><span data-stu-id="fb581-198">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="В примере показана вкладка, обсуждаемая в потоке канала." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fb581-200">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="fb581-200">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-channel.png" alt-text="В примере показана вкладка для мобильных устройств, которая обсуждается в потоке канала." border="false":::

---

### <a name="tab-chat"></a><span data-ttu-id="fb581-202">Чат Tab</span><span class="sxs-lookup"><span data-stu-id="fb581-202">Tab chat</span></span>

<span data-ttu-id="fb581-203">Пользователи могут беседуть рядом с просматриваемым контентом вкладок.</span><span class="sxs-lookup"><span data-stu-id="fb581-203">Users can have a conversation next to the tab content they're viewing.</span></span> <span data-ttu-id="fb581-204">На рабочем столе чат открывается на стороне контента приложения.</span><span class="sxs-lookup"><span data-stu-id="fb581-204">On desktop, the chat opens to the side of the app content.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fb581-205">Desktop</span><span class="sxs-lookup"><span data-stu-id="fb581-205">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="В примере показана вкладка с открытой в правой части чатом." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fb581-207">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="fb581-207">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-side-chat.png" alt-text="В примере показана вкладка для мобильных устройств с областью чата в контексте." border="false":::

---

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="fb581-209">Разрешения и представления на основе ролей</span><span class="sxs-lookup"><span data-stu-id="fb581-209">Permissions and role-based views</span></span>

<span data-ttu-id="fb581-210">Опыт вкладки может быть разным для пользователей в зависимости от их разрешений.</span><span class="sxs-lookup"><span data-stu-id="fb581-210">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="fb581-211">Например, один пользователь может получить доступ к вкладке, не входя.</span><span class="sxs-lookup"><span data-stu-id="fb581-211">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="fb581-212">Другой пользователь, однако, должен подписать и увидит немного другое содержимое.</span><span class="sxs-lookup"><span data-stu-id="fb581-212">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="fb581-213">Управление вкладками</span><span class="sxs-lookup"><span data-stu-id="fb581-213">Manage a tab</span></span>

<span data-ttu-id="fb581-214">Можно включить параметры переименования, удаления или изменения вкладки.</span><span class="sxs-lookup"><span data-stu-id="fb581-214">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="fb581-215">Анатомия: меню Tab</span><span class="sxs-lookup"><span data-stu-id="fb581-215">Anatomy: Tab menu</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fb581-216">Desktop</span><span class="sxs-lookup"><span data-stu-id="fb581-216">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса меню вкладок." border="false":::

|<span data-ttu-id="fb581-218">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fb581-218">Counter</span></span>|<span data-ttu-id="fb581-219">Описание</span><span class="sxs-lookup"><span data-stu-id="fb581-219">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fb581-220">1</span><span class="sxs-lookup"><span data-stu-id="fb581-220">1</span></span>|<span data-ttu-id="fb581-221">**Параметры:**(Необязательный) позволяет пользователям изменять параметры вкладки после ее добавления.</span><span class="sxs-lookup"><span data-stu-id="fb581-221">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="fb581-222">2</span><span class="sxs-lookup"><span data-stu-id="fb581-222">2</span></span>|<span data-ttu-id="fb581-223">**Переименование.** Пользователи могут дать вкладке имя, значимое каналу, чату или собранию.</span><span class="sxs-lookup"><span data-stu-id="fb581-223">**Rename**: Users can give the tab a name that’s meaningful to the channel, chat, or meeting.</span></span>|
|<span data-ttu-id="fb581-224">3</span><span class="sxs-lookup"><span data-stu-id="fb581-224">3</span></span>|<span data-ttu-id="fb581-225">**Удаление.** Удаляет вкладку из канала, чата или собрания.</span><span class="sxs-lookup"><span data-stu-id="fb581-225">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="fb581-226">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="fb581-226">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-manage-tab-menu-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса меню вкладок для мобильных устройств." border="false":::

|<span data-ttu-id="fb581-228">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fb581-228">Counter</span></span>|<span data-ttu-id="fb581-229">Описание</span><span class="sxs-lookup"><span data-stu-id="fb581-229">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fb581-230">1</span><span class="sxs-lookup"><span data-stu-id="fb581-230">1</span></span>|<span data-ttu-id="fb581-231">**Откройте в браузере**: Открывает приложение в браузере по умолчанию устройства.</span><span class="sxs-lookup"><span data-stu-id="fb581-231">**Open in browser**: Opens the app in the device’s default browser.</span></span>|
|<span data-ttu-id="fb581-232">2</span><span class="sxs-lookup"><span data-stu-id="fb581-232">2</span></span>|<span data-ttu-id="fb581-233">**Скопируйте** ссылку. Пользователи могут копировать и делиться ссылкой на вкладку.</span><span class="sxs-lookup"><span data-stu-id="fb581-233">**Copy link**: Users can copy and share a link to the tab.</span></span>|
|<span data-ttu-id="fb581-234">3</span><span class="sxs-lookup"><span data-stu-id="fb581-234">3</span></span>|<span data-ttu-id="fb581-235">**Параметры:**(Необязательный) Изменение параметров вкладки после ее добавления.</span><span class="sxs-lookup"><span data-stu-id="fb581-235">**Settings**: (Optional) Modify a tab’s settings after it's been added.</span></span>|
|<span data-ttu-id="fb581-236">4 </span><span class="sxs-lookup"><span data-stu-id="fb581-236">4</span></span>|<span data-ttu-id="fb581-237">**Переименование.** Пользователи могут дать вкладке имя, значимое каналу, чату или собранию.</span><span class="sxs-lookup"><span data-stu-id="fb581-237">**Rename**: Users can give the tab a name that's meaningful to the channel, chat, or meeting.</span></span>|
|<span data-ttu-id="fb581-238">5 </span><span class="sxs-lookup"><span data-stu-id="fb581-238">5</span></span>|<span data-ttu-id="fb581-239">**Удаление.** Удаляет вкладку из канала, чата или собрания.</span><span class="sxs-lookup"><span data-stu-id="fb581-239">**Delete**: Removes the tab from the channel, chat, or meeting.</span></span>|

---

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="fb581-240">Уведомления вкладки и глубокая связь</span><span class="sxs-lookup"><span data-stu-id="fb581-240">Tab notifications and deep linking</span></span>

<span data-ttu-id="fb581-241">Вы можете отправить сообщение с глубокой ссылкой на вкладку. Например, на карточке показан сводка данных об ошибках, которые пользователь может выбрать, чтобы увидеть всю ошибку на вкладке. Отправка сообщений об активности вкладок повышает осведомленность без явного уведомления всех пользователей (например, действий без шума).</span><span class="sxs-lookup"><span data-stu-id="fb581-241">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="fb581-242">Вы также можете @mention определенных пользователей, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="fb581-242">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="fb581-243">Уведомлять пользователей о действии вкладок одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="fb581-243">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="fb581-244">**Бот.** Этот метод предпочтительный, особенно если поток вкладок ориентирован.</span><span class="sxs-lookup"><span data-stu-id="fb581-244">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="fb581-245">Беседа с потоками вкладки перемещается в вид как недавно активная.</span><span class="sxs-lookup"><span data-stu-id="fb581-245">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="fb581-246">Этот метод также позволяет ухищрения при отправлении уведомления.</span><span class="sxs-lookup"><span data-stu-id="fb581-246">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="fb581-247">**Сообщение.** Сообщение появляется в ленте действий пользователя с глубокой [ссылкой на вкладку](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="fb581-247">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="fb581-248">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="fb581-248">Best practices</span></span>

<span data-ttu-id="fb581-249">Используйте эти рекомендации для создания качественного приложения:</span><span class="sxs-lookup"><span data-stu-id="fb581-249">Use these recommendations to create a quality app experience:</span></span>

### <a name="collaboration"></a><span data-ttu-id="fb581-250">Совместная работа</span><span class="sxs-lookup"><span data-stu-id="fb581-250">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="На рисунке показано, что делать с дизайном навигации вкладок." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="fb581-252">Do: Облегчить беседу</span><span class="sxs-lookup"><span data-stu-id="fb581-252">Do: Facilitate conversation</span></span>

<span data-ttu-id="fb581-253">Включай содержимое и компоненты, о которых можно говорить.</span><span class="sxs-lookup"><span data-stu-id="fb581-253">Include content and components people can talk about.</span></span> <span data-ttu-id="fb581-254">Если он не вписывается в контекст чата, канала или собрания, он не входит в вкладку.</span><span class="sxs-lookup"><span data-stu-id="fb581-254">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="В примере показано, что не нужно делать с дизайном навигации вкладок." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="fb581-256">Не: Обрабатывайте вкладку, как и любую другую веб-страницу</span><span class="sxs-lookup"><span data-stu-id="fb581-256">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="fb581-257">Вкладка — это не веб-страницы, которые кто-то может просматривать один раз.</span><span class="sxs-lookup"><span data-stu-id="fb581-257">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="fb581-258">Вкладка должна отображать наиболее важные и релевантные материалы, необходимые для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="fb581-258">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="fb581-259">Навигация</span><span class="sxs-lookup"><span data-stu-id="fb581-259">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Пример, показывающий, что делать с дизайном навигации вкладок." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="fb581-261">Do: Ограничение задач и данных</span><span class="sxs-lookup"><span data-stu-id="fb581-261">Do: Limit tasks and data</span></span>

<span data-ttu-id="fb581-262">Вкладки работают лучше всего, если они уламывкают конкретные потребности.</span><span class="sxs-lookup"><span data-stu-id="fb581-262">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="fb581-263">Включаем ограниченный набор задач и данных, соответствующих группе или группе.</span><span class="sxs-lookup"><span data-stu-id="fb581-263">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Иллюстрация, показывающая, что не нужно делать с дизайном навигации вкладок." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="fb581-265">Не: встраить все приложение</span><span class="sxs-lookup"><span data-stu-id="fb581-265">Don't: Embed your entire app</span></span>

<span data-ttu-id="fb581-266">Использование вкладки для отображения всего приложения с многоуровневой навигацией и сложными взаимодействиями приводит к перегрузке информации.</span><span class="sxs-lookup"><span data-stu-id="fb581-266">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="fb581-267">Настройка</span><span class="sxs-lookup"><span data-stu-id="fb581-267">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Иллюстрация, показывающая, что делать с дизайном установки вкладок." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="fb581-269">Do: Keep it simple</span><span class="sxs-lookup"><span data-stu-id="fb581-269">Do: Keep it simple</span></span>

<span data-ttu-id="fb581-270">Если вашему приложению требуется проверка подлинности, попробуйте интегрировать microsoft single sign-on (SSO) для более плавного входного опытом.</span><span class="sxs-lookup"><span data-stu-id="fb581-270">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="fb581-271">Кроме того, только включить необходимые сведения и шаги, чтобы добавить вкладку.</span><span class="sxs-lookup"><span data-stu-id="fb581-271">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Иллюстрация, показывающая, что не нужно делать с дизайном установки вкладок." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="fb581-273">Не: слишком много действий</span><span class="sxs-lookup"><span data-stu-id="fb581-273">Don't: Have too many steps</span></span>

<span data-ttu-id="fb581-274">Удалите ненужные действия для добавления вкладки.</span><span class="sxs-lookup"><span data-stu-id="fb581-274">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="fb581-275">Темы</span><span class="sxs-lookup"><span data-stu-id="fb581-275">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Иллюстрация, показывающая, что делать с темой вкладок." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="fb581-277">Do: Воспользоваться преимуществами Teams цветовых маркеров</span><span class="sxs-lookup"><span data-stu-id="fb581-277">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="fb581-278">Каждая Teams имеет свою цветовую схему.</span><span class="sxs-lookup"><span data-stu-id="fb581-278">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="fb581-279">Чтобы автоматически обрабатывать изменения темы, используйте маркеры цвета <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(Fluent UI)</a> в своем дизайне.</span><span class="sxs-lookup"><span data-stu-id="fb581-279">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Иллюстрация, показывающая, что не нужно делать с темой вкладок." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="fb581-281">Не: значения цвета жесткого кода</span><span class="sxs-lookup"><span data-stu-id="fb581-281">Don't: Hard code color values</span></span>

<span data-ttu-id="fb581-282">Если вы не используете маркеры Teams цвета, ваши проекты будут менее масштабируемыми и у вас будет больше времени для управления.</span><span class="sxs-lookup"><span data-stu-id="fb581-282">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::
