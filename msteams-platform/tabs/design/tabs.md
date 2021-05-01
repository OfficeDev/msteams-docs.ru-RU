---
title: Разработка вкладки для настольных компьютеров и веб-страниц
description: Узнайте, как создать вкладку Teams (настольный компьютер и веб) и получить Microsoft Teams пользовательского интерфейса.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 9dc5489f4a6a4c6f0e1188250a9e2a9bc5793690
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101851"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="87ddb-103">Разработка вкладки для Microsoft Teams рабочего стола и веб-страницы</span><span class="sxs-lookup"><span data-stu-id="87ddb-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="87ddb-104">Вкладка — это большое полотно для контента.</span><span class="sxs-lookup"><span data-stu-id="87ddb-104">A tab is a large canvas for your content.</span></span> <span data-ttu-id="87ddb-105">Для руководства разработкой приложения в следующих сведениях описывается и иллюстрируется, как люди могут добавлять, использовать и управлять вкладками в Teams.</span><span class="sxs-lookup"><span data-stu-id="87ddb-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="87ddb-106">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="87ddb-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="87ddb-107">В наборе пользовательского интерфейса можно найти всесторонние рекомендации по разработке вкладок Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="87ddb-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="87ddb-108">Набор пользовательского интерфейса также имеет важные темы, такие как доступность и размер отзывчивый, которые здесь не охватываются.</span><span class="sxs-lookup"><span data-stu-id="87ddb-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="87ddb-109">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="87ddb-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="87ddb-110">Добавление вкладки</span><span class="sxs-lookup"><span data-stu-id="87ddb-110">Add a tab</span></span>

<span data-ttu-id="87ddb-111">Вы можете добавить вкладку из Teams магазина (AppSource) или в одном из следующих контекстов:</span><span class="sxs-lookup"><span data-stu-id="87ddb-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="87ddb-112">Чат</span><span class="sxs-lookup"><span data-stu-id="87ddb-112">Chat</span></span>
* <span data-ttu-id="87ddb-113">Канал</span><span class="sxs-lookup"><span data-stu-id="87ddb-113">Channel</span></span>
* <span data-ttu-id="87ddb-114">Собрание (до, во время или после собрания)</span><span class="sxs-lookup"><span data-stu-id="87ddb-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="87ddb-115">В следующем примере показано, как вкладка добавляется в канал.</span><span class="sxs-lookup"><span data-stu-id="87ddb-115">The following example shows how a tab is added in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="В примере показана вкладка, добавляемая в канал." border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="87ddb-117">Настройка вкладки</span><span class="sxs-lookup"><span data-stu-id="87ddb-117">Set up a tab</span></span>

<span data-ttu-id="87ddb-118">Существует короткий процесс настройки, чтобы добавить приложение в качестве канала, чата или вкладки для собраний. Это зависит в основном от вас.</span><span class="sxs-lookup"><span data-stu-id="87ddb-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="87ddb-119">Например, вы можете иметь описание использования приложения и некоторых необязательных параметров.</span><span class="sxs-lookup"><span data-stu-id="87ddb-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="87ddb-120">Если необходимо проверить подлинность пользователей, включив здесь шаг для регистрации.</span><span class="sxs-lookup"><span data-stu-id="87ddb-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="87ddb-121">Модуль конфигурации вкладок</span><span class="sxs-lookup"><span data-stu-id="87ddb-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="В примере показан модальный способ конфигурации вкладок." border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="87ddb-123">Анатомия: модуль конфигурации вкладок</span><span class="sxs-lookup"><span data-stu-id="87ddb-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса модуля конфигурации вкладок." border="false":::

|<span data-ttu-id="87ddb-125">Счетчик</span><span class="sxs-lookup"><span data-stu-id="87ddb-125">Counter</span></span>|<span data-ttu-id="87ddb-126">Описание</span><span class="sxs-lookup"><span data-stu-id="87ddb-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="87ddb-127">1</span><span class="sxs-lookup"><span data-stu-id="87ddb-127">1</span></span>|<span data-ttu-id="87ddb-128">**Логотип приложения:** логотип приложения полного цвета вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="87ddb-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="87ddb-129">2</span><span class="sxs-lookup"><span data-stu-id="87ddb-129">2</span></span>|<span data-ttu-id="87ddb-130">**Имя приложения.** Полное имя вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="87ddb-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="87ddb-131">3</span><span class="sxs-lookup"><span data-stu-id="87ddb-131">3</span></span>|<span data-ttu-id="87ddb-132">**iframe:** адаптивный пробел для контента приложения (например, параметры вкладки или проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="87ddb-132">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="87ddb-133">4 </span><span class="sxs-lookup"><span data-stu-id="87ddb-133">4</span></span>|<span data-ttu-id="87ddb-134">**О ссылке.** Открывает диалоговое окно, в котором отображаются дополнительные сведения о приложении, такие как полное описание, разрешения, необходимые приложению, а также ссылки на политику конфиденциальности и условия службы.</span><span class="sxs-lookup"><span data-stu-id="87ddb-134">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="87ddb-135">5 </span><span class="sxs-lookup"><span data-stu-id="87ddb-135">5</span></span>|<span data-ttu-id="87ddb-136">**Кнопка Закрыть:** закрывает модал.</span><span class="sxs-lookup"><span data-stu-id="87ddb-136">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="87ddb-137">6 </span><span class="sxs-lookup"><span data-stu-id="87ddb-137">6</span></span>|<span data-ttu-id="87ddb-138">**Оповещайте членов** группы. Модальный спрашивает, хотите ли вы создать сообщение, позволяя другим узнать, что вы добавили вкладку.</span><span class="sxs-lookup"><span data-stu-id="87ddb-138">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="87ddb-139">7 </span><span class="sxs-lookup"><span data-stu-id="87ddb-139">7</span></span>|<span data-ttu-id="87ddb-140">**Кнопка**"Назад": переходит к предыдущему шагу в зависимости от того, где открылся диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="87ddb-140">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="87ddb-141">8 </span><span class="sxs-lookup"><span data-stu-id="87ddb-141">8</span></span>|<span data-ttu-id="87ddb-142">**Сохранить кнопку**: Завершает установку вкладок.</span><span class="sxs-lookup"><span data-stu-id="87ddb-142">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="87ddb-143">Проверка подлинности вкладок с одним входом</span><span class="sxs-lookup"><span data-stu-id="87ddb-143">Tab authentication with single sign-on</span></span>

<span data-ttu-id="87ddb-144">Вы можете добавить шаг, на котором пользователи должны сначала войти с учетными данными Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="87ddb-144">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="87ddb-145">Этот метод проверки подлинности называется одним входом (SSO).</span><span class="sxs-lookup"><span data-stu-id="87ddb-145">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="В примере показан экран проверки подлинности вкладок." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="87ddb-147">Проектирование установки вкладок с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="87ddb-147">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="87ddb-148">Используйте один из следующих Teams пользовательского интерфейса для разработки интерфейса установки вкладок:</span><span class="sxs-lookup"><span data-stu-id="87ddb-148">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="87ddb-149">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="87ddb-149">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="87ddb-150">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="87ddb-150">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="87ddb-151">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="87ddb-151">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="87ddb-152">Просмотр вкладки</span><span class="sxs-lookup"><span data-stu-id="87ddb-152">View a tab</span></span>

<span data-ttu-id="87ddb-153">Вкладки предоставляют полноэкранный веб-опыт в Teams, где можно отобразить совместное содержимое— такие доски задач и панели мониторинга и важные сведения.</span><span class="sxs-lookup"><span data-stu-id="87ddb-153">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="В примере показана вкладка с доской задач." border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="87ddb-155">Анатомия: Вкладка</span><span class="sxs-lookup"><span data-stu-id="87ddb-155">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса вкладки." border="false":::

|<span data-ttu-id="87ddb-157">Счетчик</span><span class="sxs-lookup"><span data-stu-id="87ddb-157">Counter</span></span>|<span data-ttu-id="87ddb-158">Описание</span><span class="sxs-lookup"><span data-stu-id="87ddb-158">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="87ddb-159">1</span><span class="sxs-lookup"><span data-stu-id="87ddb-159">1</span></span>|<span data-ttu-id="87ddb-160">**Имя вкладки.** Метка навигации для вкладки.</span><span class="sxs-lookup"><span data-stu-id="87ddb-160">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="87ddb-161">2</span><span class="sxs-lookup"><span data-stu-id="87ddb-161">2</span></span>|<span data-ttu-id="87ddb-162">**Переполнение вкладки:** открывает действия вкладки, такие как переименование и удаление.</span><span class="sxs-lookup"><span data-stu-id="87ddb-162">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="87ddb-163">3</span><span class="sxs-lookup"><span data-stu-id="87ddb-163">3</span></span>|<span data-ttu-id="87ddb-164">**Tab chat**: Открывает поток чата справа, позволяя пользователям беседовать рядом с содержимым.</span><span class="sxs-lookup"><span data-stu-id="87ddb-164">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="87ddb-165">4 </span><span class="sxs-lookup"><span data-stu-id="87ddb-165">4</span></span>|<span data-ttu-id="87ddb-166">**iframe:** отображает содержимое вкладки.</span><span class="sxs-lookup"><span data-stu-id="87ddb-166">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="87ddb-167">Проектирование вкладки с шаблонами пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="87ddb-167">Designing a tab with UI templates</span></span>

<span data-ttu-id="87ddb-168">Используйте один из следующих Teams пользовательского интерфейса для разработки интерфейса вкладки:</span><span class="sxs-lookup"><span data-stu-id="87ddb-168">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="87ddb-169">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="87ddb-169">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="87ddb-170">[Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="87ddb-170">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="87ddb-171">[Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.</span><span class="sxs-lookup"><span data-stu-id="87ddb-171">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="87ddb-172">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="87ddb-172">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="87ddb-173">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="87ddb-173">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="87ddb-174">[Левый nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav). Шаблон левого nav может помочь если ваша вкладка требует некоторой навигации.</span><span class="sxs-lookup"><span data-stu-id="87ddb-174">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="87ddb-175">В общем, вы должны сохранить навигацию вкладок до минимума.</span><span class="sxs-lookup"><span data-stu-id="87ddb-175">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="87ddb-176">Использование вкладки для совместной работы</span><span class="sxs-lookup"><span data-stu-id="87ddb-176">Use a tab to collaborate</span></span>

<span data-ttu-id="87ddb-177">Вкладки помогают упростить беседы о контенте в центральном расположении.</span><span class="sxs-lookup"><span data-stu-id="87ddb-177">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="87ddb-178">Обсуждение потоков</span><span class="sxs-lookup"><span data-stu-id="87ddb-178">Thread discussion</span></span>

<span data-ttu-id="87ddb-179">Пользователи могут автоматически размещать сообщения в канале или чате после того, как они добавит новую вкладку. Это не только сообщает членам команды о новом содержимом и предоставляет ссылку на вкладку, но и позволяет пользователям начать говорить о вкладке.</span><span class="sxs-lookup"><span data-stu-id="87ddb-179">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="В примере показана вкладка, обсуждаемая в потоке канала." border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="87ddb-181">Боковая дискуссия</span><span class="sxs-lookup"><span data-stu-id="87ddb-181">Side-by-side discussion</span></span>

<span data-ttu-id="87ddb-182">Пользователи могут беседу далее во время просмотра контента вкладки.</span><span class="sxs-lookup"><span data-stu-id="87ddb-182">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="В примере показана вкладка с открытой в правой части чатом." border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="87ddb-184">Разрешения и представления на основе ролей</span><span class="sxs-lookup"><span data-stu-id="87ddb-184">Permissions and role-based views</span></span>

<span data-ttu-id="87ddb-185">Опыт вкладки может быть разным для пользователей в зависимости от их разрешений.</span><span class="sxs-lookup"><span data-stu-id="87ddb-185">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="87ddb-186">Например, один пользователь может получить доступ к вкладке, не входя.</span><span class="sxs-lookup"><span data-stu-id="87ddb-186">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="87ddb-187">Другой пользователь, однако, должен подписать и увидит немного другое содержимое.</span><span class="sxs-lookup"><span data-stu-id="87ddb-187">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="87ddb-188">Управление вкладками</span><span class="sxs-lookup"><span data-stu-id="87ddb-188">Manage a tab</span></span>

<span data-ttu-id="87ddb-189">Можно включить параметры переименования, удаления или изменения вкладки.</span><span class="sxs-lookup"><span data-stu-id="87ddb-189">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="87ddb-190">Анатомия: меню Tab</span><span class="sxs-lookup"><span data-stu-id="87ddb-190">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса меню вкладок." border="false":::

|<span data-ttu-id="87ddb-192">Счетчик</span><span class="sxs-lookup"><span data-stu-id="87ddb-192">Counter</span></span>|<span data-ttu-id="87ddb-193">Описание</span><span class="sxs-lookup"><span data-stu-id="87ddb-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="87ddb-194">1</span><span class="sxs-lookup"><span data-stu-id="87ddb-194">1</span></span>|<span data-ttu-id="87ddb-195">**Параметры:**(Необязательный) позволяет пользователям изменять параметры вкладки после ее добавления.</span><span class="sxs-lookup"><span data-stu-id="87ddb-195">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="87ddb-196">2</span><span class="sxs-lookup"><span data-stu-id="87ddb-196">2</span></span>|<span data-ttu-id="87ddb-197">**Переименовать.** Позволяет пользователям давать вкладке имя, которое более значимо для команды.</span><span class="sxs-lookup"><span data-stu-id="87ddb-197">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="87ddb-198">3</span><span class="sxs-lookup"><span data-stu-id="87ddb-198">3</span></span>|<span data-ttu-id="87ddb-199">**Удаление.** Удаляет вкладку из канала, чата или собрания.</span><span class="sxs-lookup"><span data-stu-id="87ddb-199">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="87ddb-200">Уведомления вкладки и глубокая связь</span><span class="sxs-lookup"><span data-stu-id="87ddb-200">Tab notifications and deep linking</span></span>

<span data-ttu-id="87ddb-201">Вы можете отправить сообщение с глубокой ссылкой на вкладку. Например, на карточке показан сводка данных об ошибках, которые пользователь может выбрать, чтобы увидеть всю ошибку на вкладке. Отправка сообщений об активности вкладок повышает осведомленность без явного уведомления всех пользователей (например, действий без шума).</span><span class="sxs-lookup"><span data-stu-id="87ddb-201">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="87ddb-202">Вы также можете @mention определенных пользователей, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="87ddb-202">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="87ddb-203">Уведомлять пользователей о действии вкладок одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="87ddb-203">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="87ddb-204">**Бот.** Этот метод предпочтительный, особенно если поток вкладок ориентирован.</span><span class="sxs-lookup"><span data-stu-id="87ddb-204">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="87ddb-205">Беседа с потоками вкладки перемещается в вид как недавно активная.</span><span class="sxs-lookup"><span data-stu-id="87ddb-205">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="87ddb-206">Этот метод также позволяет ухищрения при отправлении уведомления.</span><span class="sxs-lookup"><span data-stu-id="87ddb-206">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="87ddb-207">**Сообщение.** Сообщение появляется в ленте действий пользователя с глубокой [ссылкой на вкладку](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="87ddb-207">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="87ddb-208">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="87ddb-208">Best practices</span></span>

<span data-ttu-id="87ddb-209">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="87ddb-209">Use these recommendations to create a quality app experience.</span></span>

### <a name="collaboration"></a><span data-ttu-id="87ddb-210">Совместная работа</span><span class="sxs-lookup"><span data-stu-id="87ddb-210">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="На рисунке показано, что делать с дизайном навигации вкладок." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="87ddb-212">Do: Облегчить беседу</span><span class="sxs-lookup"><span data-stu-id="87ddb-212">Do: Facilitate conversation</span></span>

<span data-ttu-id="87ddb-213">Включай содержимое и компоненты, о которых можно говорить.</span><span class="sxs-lookup"><span data-stu-id="87ddb-213">Include content and components people can talk about.</span></span> <span data-ttu-id="87ddb-214">Если он не вписывается в контекст чата, канала или собрания, он не входит в вкладку.</span><span class="sxs-lookup"><span data-stu-id="87ddb-214">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="В примере показано, что не нужно делать с дизайном навигации вкладок." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="87ddb-216">Не: Обрабатывайте вкладку, как и любую другую веб-страницу</span><span class="sxs-lookup"><span data-stu-id="87ddb-216">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="87ddb-217">Вкладка — это не веб-страницы, которые кто-то может просматривать один раз.</span><span class="sxs-lookup"><span data-stu-id="87ddb-217">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="87ddb-218">Вкладка должна отображать наиболее важные и релевантные материалы, необходимые для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="87ddb-218">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="87ddb-219">Навигация</span><span class="sxs-lookup"><span data-stu-id="87ddb-219">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Пример, показывающий, что делать с дизайном навигации вкладок." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="87ddb-221">Do: Ограничение задач и данных</span><span class="sxs-lookup"><span data-stu-id="87ddb-221">Do: Limit tasks and data</span></span>

<span data-ttu-id="87ddb-222">Вкладки работают лучше всего, если они уламывкают конкретные потребности.</span><span class="sxs-lookup"><span data-stu-id="87ddb-222">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="87ddb-223">Включаем ограниченный набор задач и данных, соответствующих группе или группе.</span><span class="sxs-lookup"><span data-stu-id="87ddb-223">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Иллюстрация, показывающая, что не нужно делать с дизайном навигации вкладок." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="87ddb-225">Не: встраить все приложение</span><span class="sxs-lookup"><span data-stu-id="87ddb-225">Don't: Embed your entire app</span></span>

<span data-ttu-id="87ddb-226">Использование вкладки для отображения всего приложения с многоуровневой навигацией и сложными взаимодействиями приводит к перегрузке информации.</span><span class="sxs-lookup"><span data-stu-id="87ddb-226">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="87ddb-227">Настройка</span><span class="sxs-lookup"><span data-stu-id="87ddb-227">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Иллюстрация, показывающая, что делать с дизайном установки вкладок." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="87ddb-229">Do: Keep it simple</span><span class="sxs-lookup"><span data-stu-id="87ddb-229">Do: Keep it simple</span></span>

<span data-ttu-id="87ddb-230">Если вашему приложению требуется проверка подлинности, попробуйте интегрировать microsoft single sign-on (SSO) для более плавного входного опытом.</span><span class="sxs-lookup"><span data-stu-id="87ddb-230">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="87ddb-231">Кроме того, только включить необходимые сведения и шаги, чтобы добавить вкладку.</span><span class="sxs-lookup"><span data-stu-id="87ddb-231">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Иллюстрация, показывающая, что не нужно делать с дизайном установки вкладок." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="87ddb-233">Не: слишком много действий</span><span class="sxs-lookup"><span data-stu-id="87ddb-233">Don't: Have too many steps</span></span>

<span data-ttu-id="87ddb-234">Удалите ненужные действия для добавления вкладки.</span><span class="sxs-lookup"><span data-stu-id="87ddb-234">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="87ddb-235">Темы</span><span class="sxs-lookup"><span data-stu-id="87ddb-235">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Иллюстрация, показывающая, что делать с темой вкладок." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="87ddb-237">Do: Воспользоваться преимуществами Teams цветовых маркеров</span><span class="sxs-lookup"><span data-stu-id="87ddb-237">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="87ddb-238">Каждая Teams имеет свою цветовую схему.</span><span class="sxs-lookup"><span data-stu-id="87ddb-238">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="87ddb-239">Чтобы автоматически обрабатывать изменения темы, используйте маркеры цвета <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(Fluent UI)</a> в своем дизайне.</span><span class="sxs-lookup"><span data-stu-id="87ddb-239">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Иллюстрация, показывающая, что не нужно делать с темой вкладок." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="87ddb-241">Не: значения цвета жесткого кода</span><span class="sxs-lookup"><span data-stu-id="87ddb-241">Don't: Hard code color values</span></span>

<span data-ttu-id="87ddb-242">Если вы не используете маркеры Teams цвета, ваши проекты будут менее масштабируемыми и у вас будет больше времени для управления.</span><span class="sxs-lookup"><span data-stu-id="87ddb-242">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::
