---
title: Проектирование вкладки для настольных компьютеров и веб-страниц
description: Узнайте, как разработать Teams (рабочий стол и веб) и получить Microsoft Teams пользовательского интерфейса.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: baa17cd97ff4e2cad91615dced5c4e4cf5e533c8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566882"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="fba31-103">Проектирование вкладки для Microsoft Teams и веб-страниц</span><span class="sxs-lookup"><span data-stu-id="fba31-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="fba31-104">Вкладка - это большое полотно для содержимого.</span><span class="sxs-lookup"><span data-stu-id="fba31-104">A tab is a large canvas for your content.</span></span> <span data-ttu-id="fba31-105">Чтобы направлять дизайн приложения, следующая информация описывает и иллюстрирует, как люди могут добавлять, использовать и управлять вкладками в Teams.</span><span class="sxs-lookup"><span data-stu-id="fba31-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="fba31-106">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fba31-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="fba31-107">В наборе пользовательского интерфейса можно найти всеобъемлющие рекомендации по проектированию вкладок, включая элементы, Microsoft Teams которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="fba31-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="fba31-108">Комплект пользовательского интерфейса также имеет важные темы, такие как доступность и отзывчивые размеры, которые не охвачены здесь.</span><span class="sxs-lookup"><span data-stu-id="fba31-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fba31-109">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="fba31-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="fba31-110">Добавление вкладки</span><span class="sxs-lookup"><span data-stu-id="fba31-110">Add a tab</span></span>

<span data-ttu-id="fba31-111">Вы можете добавить вкладку из Teams (AppSource) или в одном из следующих контекстов:</span><span class="sxs-lookup"><span data-stu-id="fba31-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="fba31-112">Чат</span><span class="sxs-lookup"><span data-stu-id="fba31-112">Chat</span></span>
* <span data-ttu-id="fba31-113">Канал</span><span class="sxs-lookup"><span data-stu-id="fba31-113">Channel</span></span>
* <span data-ttu-id="fba31-114">Совещание (до, во время или после собрания)</span><span class="sxs-lookup"><span data-stu-id="fba31-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="fba31-115">В следующем примере показано, как вкладка добавляется в канал:</span><span class="sxs-lookup"><span data-stu-id="fba31-115">The following example shows how a tab is added in a channel:</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="Пример показывает вкладку, добавленную в канал." border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="fba31-117">Настройка вкладки</span><span class="sxs-lookup"><span data-stu-id="fba31-117">Set up a tab</span></span>

<span data-ttu-id="fba31-118">Существует короткий процесс настройки приложения в качестве канала, чата или вкладки собрания. Опыт в значительной степени до вас.</span><span class="sxs-lookup"><span data-stu-id="fba31-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="fba31-119">Например, можно получить описание того, как использовать приложение, и некоторые дополнительные настройки.</span><span class="sxs-lookup"><span data-stu-id="fba31-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="fba31-120">Включите шаг ва-а-си, если вам нужно проверить подлинность пользователей.</span><span class="sxs-lookup"><span data-stu-id="fba31-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="fba31-121">Модальный конфигурация вкладок</span><span class="sxs-lookup"><span data-stu-id="fba31-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="Пример показывает модальный конфигурацию вкладки." border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="fba31-123">Анатомия: Модальный конфигурация вкладок</span><span class="sxs-lookup"><span data-stu-id="fba31-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса модала конфигурации вкладки." border="false":::

|<span data-ttu-id="fba31-125">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fba31-125">Counter</span></span>|<span data-ttu-id="fba31-126">Описание</span><span class="sxs-lookup"><span data-stu-id="fba31-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fba31-127">1</span><span class="sxs-lookup"><span data-stu-id="fba31-127">1</span></span>|<span data-ttu-id="fba31-128">**Логотип приложения**: Логотип приложения полного цвета вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="fba31-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="fba31-129">2</span><span class="sxs-lookup"><span data-stu-id="fba31-129">2</span></span>|<span data-ttu-id="fba31-130">**Название приложения**: Полное название приложения.</span><span class="sxs-lookup"><span data-stu-id="fba31-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="fba31-131">3</span><span class="sxs-lookup"><span data-stu-id="fba31-131">3</span></span>|<span data-ttu-id="fba31-132">**iframe**: Ответственное пространство для содержимого приложения.</span><span class="sxs-lookup"><span data-stu-id="fba31-132">**iframe**: Responsive space for your app’s content.</span></span> <span data-ttu-id="fba31-133">Например, настройки вкладок или аутентификация.</span><span class="sxs-lookup"><span data-stu-id="fba31-133">For example, tab settings or authentication.</span></span>|
|<span data-ttu-id="fba31-134">4 </span><span class="sxs-lookup"><span data-stu-id="fba31-134">4</span></span>|<span data-ttu-id="fba31-135">**О ссылке**: Открывается диалог, показывающий больше информации о приложении, например, полное описание, разрешения, требуемые приложением, и ссылки на вашу политику конфиденциальности и условия обслуживания.</span><span class="sxs-lookup"><span data-stu-id="fba31-135">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="fba31-136">5 </span><span class="sxs-lookup"><span data-stu-id="fba31-136">5</span></span>|<span data-ttu-id="fba31-137">**Кнопка закрытия**: Закрывает модальный.</span><span class="sxs-lookup"><span data-stu-id="fba31-137">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="fba31-138">6 </span><span class="sxs-lookup"><span data-stu-id="fba31-138">6</span></span>|<span data-ttu-id="fba31-139">**Сообщите членам команды вариант:** Модал спрашивает, если вы хотите создать сообщение давая другим знать, что вы добавили вкладку.</span><span class="sxs-lookup"><span data-stu-id="fba31-139">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="fba31-140">7 </span><span class="sxs-lookup"><span data-stu-id="fba31-140">7</span></span>|<span data-ttu-id="fba31-141">**Кнопка «Назад»:** Переходит к предыдущему шагу в зависимости от того, где открылся диалог.</span><span class="sxs-lookup"><span data-stu-id="fba31-141">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="fba31-142">8 </span><span class="sxs-lookup"><span data-stu-id="fba31-142">8</span></span>|<span data-ttu-id="fba31-143">**Сохранить кнопку**: Завершает настройку вкладок.</span><span class="sxs-lookup"><span data-stu-id="fba31-143">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="fba31-144">Проверка подлинности вкладок с одним ва-пом.</span><span class="sxs-lookup"><span data-stu-id="fba31-144">Tab authentication with single sign-on</span></span>

<span data-ttu-id="fba31-145">Можно добавить шаг, в котором пользователи должны сначала войти в систему со своими учетными данными Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="fba31-145">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="fba31-146">Этот метод проверки подлинности называется единым ва-по (SSO).</span><span class="sxs-lookup"><span data-stu-id="fba31-146">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="Пример показывает экран проверки подлинности вкладки." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="fba31-148">Проектирование настройки вкладок с шаблонами пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="fba31-148">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="fba31-149">Используйте один из следующих шаблонов Teams пользовательского интерфейса, чтобы помочь спроектировать интерфейс настройки вкладок:</span><span class="sxs-lookup"><span data-stu-id="fba31-149">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="fba31-150">[Список](../../concepts/design/design-teams-app-ui-templates.md#list): Списки могут отображать связанные элементы в сканируемом формате и позволяют пользователям принимать меры по всему списку или отдельным элементам.</span><span class="sxs-lookup"><span data-stu-id="fba31-150">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="fba31-151">[Форма](../../concepts/design/design-teams-app-ui-templates.md#form): Формы для сбора, проверки и отправки пользовательского ввода структурированным способом.</span><span class="sxs-lookup"><span data-stu-id="fba31-151">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="fba31-152">[Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state): Пустой шаблон состояния может быть использован для многих сценариев, включая войти в него, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="fba31-152">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="fba31-153">Просмотр вкладки</span><span class="sxs-lookup"><span data-stu-id="fba31-153">View a tab</span></span>

<span data-ttu-id="fba31-154">Вкладки обеспечивают полноэкранный веб-опыт в Teams где вы можете отображать совместное содержание- такие доски задач и панели мониторинга, и важную информацию.</span><span class="sxs-lookup"><span data-stu-id="fba31-154">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="Пример показывает вкладку с доской задач." border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="fba31-156">Анатомия: Вкладка</span><span class="sxs-lookup"><span data-stu-id="fba31-156">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса вкладки." border="false":::

|<span data-ttu-id="fba31-158">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fba31-158">Counter</span></span>|<span data-ttu-id="fba31-159">Описание</span><span class="sxs-lookup"><span data-stu-id="fba31-159">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fba31-160">1</span><span class="sxs-lookup"><span data-stu-id="fba31-160">1</span></span>|<span data-ttu-id="fba31-161">**Название вкладки**: Навигационный ярлык для вкладки.</span><span class="sxs-lookup"><span data-stu-id="fba31-161">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="fba31-162">2</span><span class="sxs-lookup"><span data-stu-id="fba31-162">2</span></span>|<span data-ttu-id="fba31-163">**Переполняем** вкладок: открывается вкладка действий, таких как переименование и удаление.</span><span class="sxs-lookup"><span data-stu-id="fba31-163">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="fba31-164">3</span><span class="sxs-lookup"><span data-stu-id="fba31-164">3</span></span>|<span data-ttu-id="fba31-165">**Tab чат**: Открывает поток чата справа, что позволяет пользователям иметь разговор рядом с содержанием.</span><span class="sxs-lookup"><span data-stu-id="fba31-165">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="fba31-166">4 </span><span class="sxs-lookup"><span data-stu-id="fba31-166">4</span></span>|<span data-ttu-id="fba31-167">**iframe**: Отображает содержимое вкладки.</span><span class="sxs-lookup"><span data-stu-id="fba31-167">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="fba31-168">Проектирование вкладки с шаблонами пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="fba31-168">Designing a tab with UI templates</span></span>

<span data-ttu-id="fba31-169">Используйте один из следующих шаблонов Teams пользовательского интерфейса, чтобы помочь спроектировать интерфейс вкладки:</span><span class="sxs-lookup"><span data-stu-id="fba31-169">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="fba31-170">[Список](../../concepts/design/design-teams-app-ui-templates.md#list): Списки могут отображать связанные элементы в сканируемом формате и позволяют пользователям принимать меры по всему списку или отдельным элементам.</span><span class="sxs-lookup"><span data-stu-id="fba31-170">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="fba31-171">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): Целевая доска, иногда называемая доска kanban или плавательные дорожки, представляет собой набор карт, часто используемых для отслеживания состояния рабочих предметов или билетов.</span><span class="sxs-lookup"><span data-stu-id="fba31-171">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="fba31-172">[Панель мониторинга](../../concepts/design/design-teams-app-ui-templates.md#dashboard): Панель мониторинга — это холст, содержащий несколько карт, которые обеспечивают обзор данных или содержимого.</span><span class="sxs-lookup"><span data-stu-id="fba31-172">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="fba31-173">[Форма](../../concepts/design/design-teams-app-ui-templates.md#form): Формы для сбора, проверки и отправки пользовательского ввода структурированным способом.</span><span class="sxs-lookup"><span data-stu-id="fba31-173">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="fba31-174">[Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state): Пустой шаблон состояния может быть использован для многих сценариев, включая войти в него, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="fba31-174">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="fba31-175">[Левый навигатор](../../concepts/design/design-teams-app-ui-templates.md#left-nav): Левый шаблон навигации может помочь, если ваша вкладка требует некоторой навигации.</span><span class="sxs-lookup"><span data-stu-id="fba31-175">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="fba31-176">Как правило, следует с минимумом следить за навигацией.</span><span class="sxs-lookup"><span data-stu-id="fba31-176">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="fba31-177">Используйте вкладку для совместной работы</span><span class="sxs-lookup"><span data-stu-id="fba31-177">Use a tab to collaborate</span></span>

<span data-ttu-id="fba31-178">Вкладки помогают облегчить разговоры о содержании в центральном месте.</span><span class="sxs-lookup"><span data-stu-id="fba31-178">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="fba31-179">Обсуждение темы</span><span class="sxs-lookup"><span data-stu-id="fba31-179">Thread discussion</span></span>

<span data-ttu-id="fba31-180">Пользователи могут автоматически размещать на канале или в чате, как только они добавили новую вкладку. Это не только уведомляет членов команды о новом контенте и предоставляет ссылку на вкладку, это позволяет людям начать говорить о вкладке.</span><span class="sxs-lookup"><span data-stu-id="fba31-180">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="Пример показывает вкладку, обсуждаемую в потоке канала." border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="fba31-182">Бок о бок обсуждение</span><span class="sxs-lookup"><span data-stu-id="fba31-182">Side-by-side discussion</span></span>

<span data-ttu-id="fba31-183">Пользователи могут иметь беседу дальше во время просмотра содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="fba31-183">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="Пример показывает вкладку с открытым чатом на правой стороне." border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="fba31-185">Разрешения и представления, основанные на роли</span><span class="sxs-lookup"><span data-stu-id="fba31-185">Permissions and role-based views</span></span>

<span data-ttu-id="fba31-186">Опыт работы с вкладками может отличаться для пользователей в зависимости от их разрешений.</span><span class="sxs-lookup"><span data-stu-id="fba31-186">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="fba31-187">Например, один пользователь может получить доступ к вкладке без необходимости вовсяка.</span><span class="sxs-lookup"><span data-stu-id="fba31-187">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="fba31-188">Другой пользователь, однако, должен подписать и увидит несколько иное содержание.</span><span class="sxs-lookup"><span data-stu-id="fba31-188">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="fba31-189">Управление вкладкой</span><span class="sxs-lookup"><span data-stu-id="fba31-189">Manage a tab</span></span>

<span data-ttu-id="fba31-190">Можно включить параметры для переименования, удаления или изменения вкладки.</span><span class="sxs-lookup"><span data-stu-id="fba31-190">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="fba31-191">Анатомия: Вкладка меню</span><span class="sxs-lookup"><span data-stu-id="fba31-191">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса меню вкладок." border="false":::

|<span data-ttu-id="fba31-193">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fba31-193">Counter</span></span>|<span data-ttu-id="fba31-194">Описание</span><span class="sxs-lookup"><span data-stu-id="fba31-194">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fba31-195">1</span><span class="sxs-lookup"><span data-stu-id="fba31-195">1</span></span>|<span data-ttu-id="fba31-196">**Параметры**: (Опционально) позволяет пользователям изменять настройки вкладки после ее добавления.</span><span class="sxs-lookup"><span data-stu-id="fba31-196">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="fba31-197">2</span><span class="sxs-lookup"><span data-stu-id="fba31-197">2</span></span>|<span data-ttu-id="fba31-198">**Переименование**: Позволяет пользователям дать вкладке имя, которое является более значимым для команды.</span><span class="sxs-lookup"><span data-stu-id="fba31-198">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="fba31-199">3</span><span class="sxs-lookup"><span data-stu-id="fba31-199">3</span></span>|<span data-ttu-id="fba31-200">**Удалить**: Удаляет вкладку из канала, чата или собрания.</span><span class="sxs-lookup"><span data-stu-id="fba31-200">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="fba31-201">Уведомления о вкладке и глубокая связь</span><span class="sxs-lookup"><span data-stu-id="fba31-201">Tab notifications and deep linking</span></span>

<span data-ttu-id="fba31-202">Вы можете отправить сообщение с глубокой ссылкой на вкладку. Например, карта показывает резюме данных об ошибках, которые пользователь может выбрать, чтобы увидеть всю ошибку во вкладке. Отправка сообщений о деятельности вкладок повышает осведомленность без прямого уведомления всех (т.е. активности без шума).</span><span class="sxs-lookup"><span data-stu-id="fba31-202">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="fba31-203">Вы также можете @mention пользователей, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="fba31-203">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="fba31-204">Сообщите пользователям о деятельности вкладок одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="fba31-204">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="fba31-205">**Бот**: Этот метод является предпочтительным, особенно если поток вкладок является целевым.</span><span class="sxs-lookup"><span data-stu-id="fba31-205">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="fba31-206">Резьбовая беседа вкладки перемещается в поле зрения как недавно активная.</span><span class="sxs-lookup"><span data-stu-id="fba31-206">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="fba31-207">Этот метод также позволяет некоторое у сложности в том, как уведомление отправляется.</span><span class="sxs-lookup"><span data-stu-id="fba31-207">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="fba31-208">**Сообщение**: Сообщение появляется в ленте активности пользователя с глубокой [ссылкой на вкладку.](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="fba31-208">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="fba31-209">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="fba31-209">Best practices</span></span>

<span data-ttu-id="fba31-210">Используйте эти рекомендации для создания качественного приложения:</span><span class="sxs-lookup"><span data-stu-id="fba31-210">Use these recommendations to create a quality app experience:</span></span>

### <a name="collaboration"></a><span data-ttu-id="fba31-211">Совместная работа</span><span class="sxs-lookup"><span data-stu-id="fba31-211">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="Иллюстрация показывает, что делать с дизайном навигации вкладок." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="fba31-213">У: Облегчить разговор</span><span class="sxs-lookup"><span data-stu-id="fba31-213">Do: Facilitate conversation</span></span>

<span data-ttu-id="fba31-214">Включите содержимое и компоненты, о которых люди могут говорить.</span><span class="sxs-lookup"><span data-stu-id="fba31-214">Include content and components people can talk about.</span></span> <span data-ttu-id="fba31-215">Если он не вписывается в контекст чата, канала или собрания, он не входит в вашу вкладку.</span><span class="sxs-lookup"><span data-stu-id="fba31-215">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="Пример показывает, что не делать с дизайном навигации вкладок." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="fba31-217">Не: Относитесь к вкладке, как и к любой другой веб-странице</span><span class="sxs-lookup"><span data-stu-id="fba31-217">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="fba31-218">Вкладка не является веб-страницей, которая может просматривать один раз.</span><span class="sxs-lookup"><span data-stu-id="fba31-218">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="fba31-219">Вкладка должна отображать наиболее важные, соответствующие содержание, что люди должны выполнить что-то вместе.</span><span class="sxs-lookup"><span data-stu-id="fba31-219">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="fba31-220">Навигация</span><span class="sxs-lookup"><span data-stu-id="fba31-220">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Пример, показывающий, что делать с дизайном навигации вкладок." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="fba31-222">У: Ограничьте задачи и данные</span><span class="sxs-lookup"><span data-stu-id="fba31-222">Do: Limit tasks and data</span></span>

<span data-ttu-id="fba31-223">Вкладки работают лучше всего, когда они отвечает конкретным потребностям.</span><span class="sxs-lookup"><span data-stu-id="fba31-223">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="fba31-224">Включите ограниченный набор задач и данных, отвеяных для группы или группы.</span><span class="sxs-lookup"><span data-stu-id="fba31-224">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Иллюстрация, показывающая, что не делать с дизайном навигации вкладок." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="fba31-226">Не встраивайте все приложение</span><span class="sxs-lookup"><span data-stu-id="fba31-226">Don't: Embed your entire app</span></span>

<span data-ttu-id="fba31-227">Использование вкладки для отображения всего приложения с многоуровневой навигацией и сложным взаимодействием приводит к информационной перегрузке.</span><span class="sxs-lookup"><span data-stu-id="fba31-227">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="fba31-228">Настройка</span><span class="sxs-lookup"><span data-stu-id="fba31-228">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Иллюстрация, показывающая, что делать с дизайном настройки вкладок." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="fba31-230">У: Держите его простым</span><span class="sxs-lookup"><span data-stu-id="fba31-230">Do: Keep it simple</span></span>

<span data-ttu-id="fba31-231">Если ваше приложение требует проверки подлинности, попробуйте интегрировать единый в системе поддержки Майкрософт (SSO) для более беспрепятственного вовсякого взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="fba31-231">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="fba31-232">Кроме того, только включите важную информацию и шаги, чтобы добавить вкладку.</span><span class="sxs-lookup"><span data-stu-id="fba31-232">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Иллюстрация, показывающая, что не делать с дизайном настройки вкладок." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="fba31-234">Не: Есть слишком много шагов</span><span class="sxs-lookup"><span data-stu-id="fba31-234">Don't: Have too many steps</span></span>

<span data-ttu-id="fba31-235">Удалите ненужные шаги для добавления вкладки.</span><span class="sxs-lookup"><span data-stu-id="fba31-235">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="fba31-236">Темы</span><span class="sxs-lookup"><span data-stu-id="fba31-236">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Иллюстрация, показывающая, что делать с вкладкой theming." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="fba31-238">Do: Воспользуйтесь Teams цветных жетонов</span><span class="sxs-lookup"><span data-stu-id="fba31-238">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="fba31-239">Каждая Teams имеет свою цветовую гамму.</span><span class="sxs-lookup"><span data-stu-id="fba31-239">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="fba31-240">Для автоматического обработки изменений темы <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">используйте цветовые жетоны (Fluent UI)</a> в своем дизайне.</span><span class="sxs-lookup"><span data-stu-id="fba31-240">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Иллюстрация, показывающая, что не делать с вкладкой theming." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="fba31-242">Не: Значения цвета жесткого кода</span><span class="sxs-lookup"><span data-stu-id="fba31-242">Don't: Hard code color values</span></span>

<span data-ttu-id="fba31-243">Если вы не используете Teams, ваши проекты будут менее масштабируемыми и потребуется больше времени для управления.</span><span class="sxs-lookup"><span data-stu-id="fba31-243">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::
