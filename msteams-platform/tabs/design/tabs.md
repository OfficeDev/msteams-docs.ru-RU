---
title: Разработка вкладки для настольного компьютера и веб-сайта
description: Узнайте, как разработать вкладку Teams (Desktop and Web) и получить набор пользовательских интерфейсов Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 692a21c78dc86cbca5bf248e55d0332bd71c6b92
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604703"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="ce15f-103">Разработка вкладки для настольных и веб-приложений Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ce15f-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="ce15f-104">Вкладка — это большой холст для контента, который упрощает совместную работу.</span><span class="sxs-lookup"><span data-stu-id="ce15f-104">A tab is a large canvas for content that facilitates collaboration.</span></span> <span data-ttu-id="ce15f-105">В следующей статье описываются способы добавления, использования и управления вкладками в Teams для разработки приложений.</span><span class="sxs-lookup"><span data-stu-id="ce15f-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="ce15f-106">Набор элементов пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ce15f-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="ce15f-107">Вы можете найти подробные рекомендации по проектированию вкладок, в том числе элементы, которые можно прихватить и изменить при необходимости, в наборе UI Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ce15f-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="ce15f-108">Кроме того, в наборе элементов пользовательского интерфейса есть важные темы, такие как специальные возможности и размеры отклика, которые не рассматриваются здесь.</span><span class="sxs-lookup"><span data-stu-id="ce15f-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ce15f-109">Получение набора элементов пользовательского интерфейса Microsoft Teams (фигма)</span><span class="sxs-lookup"><span data-stu-id="ce15f-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="ce15f-110">Добавление вкладки</span><span class="sxs-lookup"><span data-stu-id="ce15f-110">Add a tab</span></span>

<span data-ttu-id="ce15f-111">Вы можете добавить вкладку из хранилища Teams (AppSource) или из одного из следующих контекстов:</span><span class="sxs-lookup"><span data-stu-id="ce15f-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="ce15f-112">Чат</span><span class="sxs-lookup"><span data-stu-id="ce15f-112">Chat</span></span>
* <span data-ttu-id="ce15f-113">Канал</span><span class="sxs-lookup"><span data-stu-id="ce15f-113">Channel</span></span>
* <span data-ttu-id="ce15f-114">Собрание (до, во время или после собрания)</span><span class="sxs-lookup"><span data-stu-id="ce15f-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="ce15f-115">В приведенном ниже примере показано, как в канал добавляется вкладка.</span><span class="sxs-lookup"><span data-stu-id="ce15f-115">The following example shows how a tab is added in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="В примере показана вкладка, добавляемая в канал." border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="ce15f-117">Настройка вкладки</span><span class="sxs-lookup"><span data-stu-id="ce15f-117">Set up a tab</span></span>

<span data-ttu-id="ce15f-118">Для добавления приложения в качестве вкладки "канал", "чат" или "собрание" существует короткий процесс установки. Процесс работы практически не отличается.</span><span class="sxs-lookup"><span data-stu-id="ce15f-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="ce15f-119">Например, вы можете получить описание использования приложения и некоторых необязательных параметров.</span><span class="sxs-lookup"><span data-stu-id="ce15f-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="ce15f-120">Включите здесь шаг входа, если необходимо выполнить проверку подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="ce15f-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="ce15f-121">Модальная Конфигурация вкладки</span><span class="sxs-lookup"><span data-stu-id="ce15f-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="В примере показана модальность конфигурации вкладки." border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="ce15f-123">Структура: модальная Конфигурация вкладки</span><span class="sxs-lookup"><span data-stu-id="ce15f-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Иллюстрация, на которой показана структура пользовательского интерфейса модальной конфигурации вкладки." border="false":::

|<span data-ttu-id="ce15f-125">Счетчик</span><span class="sxs-lookup"><span data-stu-id="ce15f-125">Counter</span></span>|<span data-ttu-id="ce15f-126">Описание</span><span class="sxs-lookup"><span data-stu-id="ce15f-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ce15f-127">1</span><span class="sxs-lookup"><span data-stu-id="ce15f-127">1</span></span>|<span data-ttu-id="ce15f-128">**Логотип приложения**: полный цвет логотипа приложения для приложения.</span><span class="sxs-lookup"><span data-stu-id="ce15f-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="ce15f-129">2 </span><span class="sxs-lookup"><span data-stu-id="ce15f-129">2</span></span>|<span data-ttu-id="ce15f-130">**Имя приложения**: полное имя приложения.</span><span class="sxs-lookup"><span data-stu-id="ce15f-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="ce15f-131">3 </span><span class="sxs-lookup"><span data-stu-id="ce15f-131">3</span></span>|<span data-ttu-id="ce15f-132">**IFRAME**: область отклика для контента приложения (например, параметры вкладки или проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="ce15f-132">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="ce15f-133">4 </span><span class="sxs-lookup"><span data-stu-id="ce15f-133">4</span></span>|<span data-ttu-id="ce15f-134">**Ссылка**: открывает диалоговое окно, содержащее дополнительные сведения о приложении, такие как полное описание, разрешения, необходимые приложению, а также ссылки на политику конфиденциальности и условия предоставления услуг.</span><span class="sxs-lookup"><span data-stu-id="ce15f-134">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="ce15f-135">5 </span><span class="sxs-lookup"><span data-stu-id="ce15f-135">5</span></span>|<span data-ttu-id="ce15f-136">**Кнопка "Закрыть"**: закрывает модальное окно.</span><span class="sxs-lookup"><span data-stu-id="ce15f-136">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="ce15f-137">6 </span><span class="sxs-lookup"><span data-stu-id="ce15f-137">6</span></span>|<span data-ttu-id="ce15f-138">**Уведомить участников группы**: в модальных запросах вы хотите создать сообщение, которое уведомить других пользователей о том, что вы добавили вкладку.</span><span class="sxs-lookup"><span data-stu-id="ce15f-138">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="ce15f-139">7 </span><span class="sxs-lookup"><span data-stu-id="ce15f-139">7</span></span>|<span data-ttu-id="ce15f-140">**Кнопка "назад"**: переход к предыдущему этапу в зависимости от того, где открыто диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="ce15f-140">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="ce15f-141">8 </span><span class="sxs-lookup"><span data-stu-id="ce15f-141">8</span></span>|<span data-ttu-id="ce15f-142">**Кнопка "Сохранить"**: завершает настройку вкладки.</span><span class="sxs-lookup"><span data-stu-id="ce15f-142">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="ce15f-143">Проверка подлинности с помощью единого входа</span><span class="sxs-lookup"><span data-stu-id="ce15f-143">Tab authentication with single sign-on</span></span>

<span data-ttu-id="ce15f-144">Вы можете добавить шаг, в котором пользователи должны сначала войти в систему, используя свои учетные данные Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ce15f-144">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="ce15f-145">Этот способ проверки подлинности называется единым входом (SSO).</span><span class="sxs-lookup"><span data-stu-id="ce15f-145">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="В примере показан экран проверки подлинности вкладки." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="ce15f-147">Разработка настройки вкладки с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ce15f-147">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="ce15f-148">Используйте один из следующих шаблонов пользовательского интерфейса Teams, чтобы упростить процесс настройки вкладок:</span><span class="sxs-lookup"><span data-stu-id="ce15f-148">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="ce15f-149">[Список](../../concepts/design/design-teams-app-ui-templates.md#list): списки могут отображать связанные элементы в формате с возможностью записи, а пользователи выполнять действия для всего списка или отдельных элементов.</span><span class="sxs-lookup"><span data-stu-id="ce15f-149">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="ce15f-150">[Форма](../../concepts/design/design-teams-app-ui-templates.md#form): формы предназначены для сбора, проверки и отправки пользовательских данных структурированным способом.</span><span class="sxs-lookup"><span data-stu-id="ce15f-150">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="ce15f-151">[Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state): шаблон пустое состояние можно использовать для многих сценариев, в том числе входа в систему, первого запуска, сообщений об ошибках и многого другого.</span><span class="sxs-lookup"><span data-stu-id="ce15f-151">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="ce15f-152">Просмотр вкладки</span><span class="sxs-lookup"><span data-stu-id="ce15f-152">View a tab</span></span>

<span data-ttu-id="ce15f-153">Вкладки предоставляют доступ к полноэкранному веб-интерфейсу в Teams, где вы можете отображать контент для сотрудничества — такие доски задач и панели мониторинга, а также важную информацию.</span><span class="sxs-lookup"><span data-stu-id="ce15f-153">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="В примере показана вкладка с доской задач." border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="ce15f-155">Структура: Tab</span><span class="sxs-lookup"><span data-stu-id="ce15f-155">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Иллюстрация, демонстрирующая пользовательский интерфейс Анатомия вкладки." border="false":::

|<span data-ttu-id="ce15f-157">Счетчик</span><span class="sxs-lookup"><span data-stu-id="ce15f-157">Counter</span></span>|<span data-ttu-id="ce15f-158">Описание</span><span class="sxs-lookup"><span data-stu-id="ce15f-158">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ce15f-159">1</span><span class="sxs-lookup"><span data-stu-id="ce15f-159">1</span></span>|<span data-ttu-id="ce15f-160">**Имя вкладки**: "Метка навигации" для вкладки.</span><span class="sxs-lookup"><span data-stu-id="ce15f-160">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="ce15f-161">2 </span><span class="sxs-lookup"><span data-stu-id="ce15f-161">2</span></span>|<span data-ttu-id="ce15f-162">**Переполнение табуляции**: открывает действия вкладки, такие как переименование и удаление.</span><span class="sxs-lookup"><span data-stu-id="ce15f-162">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="ce15f-163">3 </span><span class="sxs-lookup"><span data-stu-id="ce15f-163">3</span></span>|<span data-ttu-id="ce15f-164">**Чат**: открывает поток чата справа, позволяя пользователям вести беседу рядом с содержимым.</span><span class="sxs-lookup"><span data-stu-id="ce15f-164">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="ce15f-165">4 </span><span class="sxs-lookup"><span data-stu-id="ce15f-165">4</span></span>|<span data-ttu-id="ce15f-166">**IFRAME**: отображение содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="ce15f-166">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="ce15f-167">Разработка вкладки с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ce15f-167">Designing a tab with UI templates</span></span>

<span data-ttu-id="ce15f-168">Используйте один из следующих шаблонов пользовательского интерфейса Teams, чтобы упростить разработку вкладок:</span><span class="sxs-lookup"><span data-stu-id="ce15f-168">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="ce15f-169">[Список](../../concepts/design/design-teams-app-ui-templates.md#list): списки могут отображать связанные элементы в формате с возможностью записи, а пользователи выполнять действия для всего списка или отдельных элементов.</span><span class="sxs-lookup"><span data-stu-id="ce15f-169">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="ce15f-170">[Доска задач](../../concepts/design/design-teams-app-ui-templates.md#task-board): доска задач, иногда называемая доской Канбан или свим желобами, — это коллекция карточек, часто используемых для отслеживания состояния рабочих элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="ce15f-170">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="ce15f-171">[Панель мониторинга](../../concepts/design/design-teams-app-ui-templates.md#dashboard): панель мониторинга — это холст, содержащий несколько карточек, которые предоставляют обзор данных или контента.</span><span class="sxs-lookup"><span data-stu-id="ce15f-171">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="ce15f-172">[Форма](../../concepts/design/design-teams-app-ui-templates.md#form): формы предназначены для сбора, проверки и отправки пользовательских данных структурированным способом.</span><span class="sxs-lookup"><span data-stu-id="ce15f-172">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="ce15f-173">[Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state): шаблон пустое состояние можно использовать для многих сценариев, в том числе входа в систему, первого запуска, сообщений об ошибках и многого другого.</span><span class="sxs-lookup"><span data-stu-id="ce15f-173">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="ce15f-174">[Левая панель навигации](../../concepts/design/design-teams-app-ui-templates.md#left-nav): левая панель навигации может помочь вам, если на вкладке требуется выполнить некоторую навигацию.</span><span class="sxs-lookup"><span data-stu-id="ce15f-174">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="ce15f-175">Как правило, переход по клавише Tab должен быть минимальным.</span><span class="sxs-lookup"><span data-stu-id="ce15f-175">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="ce15f-176">Использование вкладки для взаимодействия</span><span class="sxs-lookup"><span data-stu-id="ce15f-176">Use a tab to collaborate</span></span>

<span data-ttu-id="ce15f-177">Вкладки помогают упростить беседы с контентом в центральном расположении.</span><span class="sxs-lookup"><span data-stu-id="ce15f-177">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="ce15f-178">Обсуждение обсуждений</span><span class="sxs-lookup"><span data-stu-id="ce15f-178">Thread discussion</span></span>

<span data-ttu-id="ce15f-179">Пользователи могут автоматически отправлять сообщения в канал или чат после добавления новой вкладки. Это не только уведомляет участников группы о новом содержимом и предоставляет ссылку на вкладку, что позволяет пользователям начать говорить об этой вкладке.</span><span class="sxs-lookup"><span data-stu-id="ce15f-179">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="В примере показана вкладка, обсуждаемая в потоке канала." border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="ce15f-181">Параллельное обсуждение</span><span class="sxs-lookup"><span data-stu-id="ce15f-181">Side-by-side discussion</span></span>

<span data-ttu-id="ce15f-182">При просмотре содержимого вкладки Пользователи могут приступить к беседе.</span><span class="sxs-lookup"><span data-stu-id="ce15f-182">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="В примере показана вкладка с разговором, открытой в правой части окна." border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="ce15f-184">Разрешения и представления на основе ролей</span><span class="sxs-lookup"><span data-stu-id="ce15f-184">Permissions and role-based views</span></span>

<span data-ttu-id="ce15f-185">Режим вкладки может различаться для пользователей в зависимости от их разрешений.</span><span class="sxs-lookup"><span data-stu-id="ce15f-185">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="ce15f-186">Например, один пользователь может получить доступ к вкладке, не выполняя вход в систему.</span><span class="sxs-lookup"><span data-stu-id="ce15f-186">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="ce15f-187">Тем не менее, другой пользователь должен подписать и увидеть немного другое содержимое.</span><span class="sxs-lookup"><span data-stu-id="ce15f-187">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="ce15f-188">Управление вкладкой</span><span class="sxs-lookup"><span data-stu-id="ce15f-188">Manage a tab</span></span>

<span data-ttu-id="ce15f-189">Можно включить параметры для переименования, удаления или изменения вкладки.</span><span class="sxs-lookup"><span data-stu-id="ce15f-189">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="ce15f-190">Структура: меню вкладок</span><span class="sxs-lookup"><span data-stu-id="ce15f-190">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Иллюстрация, на которой показана структура пользовательского интерфейса меню вкладок." border="false":::

|<span data-ttu-id="ce15f-192">Счетчик</span><span class="sxs-lookup"><span data-stu-id="ce15f-192">Counter</span></span>|<span data-ttu-id="ce15f-193">Описание</span><span class="sxs-lookup"><span data-stu-id="ce15f-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ce15f-194">1</span><span class="sxs-lookup"><span data-stu-id="ce15f-194">1</span></span>|<span data-ttu-id="ce15f-195">**Параметры**: (необязательно) — позволяет пользователям изменять параметры вкладки после ее добавления.</span><span class="sxs-lookup"><span data-stu-id="ce15f-195">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="ce15f-196">2 </span><span class="sxs-lookup"><span data-stu-id="ce15f-196">2</span></span>|<span data-ttu-id="ce15f-197">**Rename**: позволяет пользователям присваивать вкладке Имя, которое более понятно команде.</span><span class="sxs-lookup"><span data-stu-id="ce15f-197">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="ce15f-198">3 </span><span class="sxs-lookup"><span data-stu-id="ce15f-198">3</span></span>|<span data-ttu-id="ce15f-199">**Удалить**: удаляет вкладку из канала, чата или собрания.</span><span class="sxs-lookup"><span data-stu-id="ce15f-199">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="ce15f-200">Уведомления вкладок и глубокое связывание</span><span class="sxs-lookup"><span data-stu-id="ce15f-200">Tab notifications and deep linking</span></span>

<span data-ttu-id="ce15f-201">Вы можете отправить сообщение с помощью ссылки на вкладку. Например, на карточке представлена сводка данных об ошибках, которую пользователь может выбрать для просмотра всей ошибки на вкладке. Отправка сообщений об активности вкладок увеличивает осведомленность без явного уведомления всех (то есть активности без шума).</span><span class="sxs-lookup"><span data-stu-id="ce15f-201">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="ce15f-202">Кроме того, при необходимости можно @mention определенных пользователей.</span><span class="sxs-lookup"><span data-stu-id="ce15f-202">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="ce15f-203">Уведомлять пользователей об активности вкладки одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="ce15f-203">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="ce15f-204">**Bot**: Этот метод предпочтителен, особенно если выбран целевой поток вкладок.</span><span class="sxs-lookup"><span data-stu-id="ce15f-204">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="ce15f-205">Цепочка обсуждений вкладки перемещается в представление "недавно активные".</span><span class="sxs-lookup"><span data-stu-id="ce15f-205">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="ce15f-206">Этот метод также позволяет использовать некоторые сложности при отправке уведомления.</span><span class="sxs-lookup"><span data-stu-id="ce15f-206">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="ce15f-207">**Сообщение**: в веб-канале активности пользователя появляется [ссылка на вкладку](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="ce15f-207">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="ce15f-208">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="ce15f-208">Best practices</span></span>

### <a name="collaboration"></a><span data-ttu-id="ce15f-209">Совместная работа</span><span class="sxs-lookup"><span data-stu-id="ce15f-209">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="Иллюстрация, на которой показано, что нужно сделать с макетом навигации по вкладкам." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="ce15f-211">Do: Упростите беседу</span><span class="sxs-lookup"><span data-stu-id="ce15f-211">Do: Facilitate conversation</span></span>

<span data-ttu-id="ce15f-212">Включить контент и компоненты люди могут говорить о них.</span><span class="sxs-lookup"><span data-stu-id="ce15f-212">Include content and components people can talk about.</span></span> <span data-ttu-id="ce15f-213">Если он не помещается в контексте разговора, канала или собрания, он не входит в состав вкладки.</span><span class="sxs-lookup"><span data-stu-id="ce15f-213">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="Иллюстрация, на которой показано, что не следует делать с навигацией по вкладкам." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="ce15f-215">Не следует рассматривать вкладку как любую другую веб-страницу</span><span class="sxs-lookup"><span data-stu-id="ce15f-215">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="ce15f-216">Вкладка — это не веб-страница, которую может просматривать один раз.</span><span class="sxs-lookup"><span data-stu-id="ce15f-216">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="ce15f-217">На вкладке должно отображаться наиболее важное, соответствующее содержимое, необходимое для совместной реализации.</span><span class="sxs-lookup"><span data-stu-id="ce15f-217">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="ce15f-218">Навигация</span><span class="sxs-lookup"><span data-stu-id="ce15f-218">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Иллюстрация, на которой показано, что нужно сделать с макетом навигации по вкладкам." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="ce15f-220">Do: Ограничьте задачи и данные</span><span class="sxs-lookup"><span data-stu-id="ce15f-220">Do: Limit tasks and data</span></span>

<span data-ttu-id="ce15f-221">Вкладки работают наилучшим образом, когда они устраняют конкретные потребности.</span><span class="sxs-lookup"><span data-stu-id="ce15f-221">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="ce15f-222">Включает в себя ограниченный набор задач и данных, относящихся к группе или группе.</span><span class="sxs-lookup"><span data-stu-id="ce15f-222">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Иллюстрация, на которой показано, что не следует делать с навигацией по вкладкам." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="ce15f-224">Не: внедрите приложение целиком</span><span class="sxs-lookup"><span data-stu-id="ce15f-224">Don't: Embed your entire app</span></span>

<span data-ttu-id="ce15f-225">Использование вкладки для отображения всего приложения с многоуровневой навигацией и сложных взаимодействий приводит к перегрузке информации.</span><span class="sxs-lookup"><span data-stu-id="ce15f-225">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="ce15f-226">Настройка</span><span class="sxs-lookup"><span data-stu-id="ce15f-226">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Иллюстрация, на которой показано, что нужно сделать с макетом настройки вкладок." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="ce15f-228">Do: Сделайте это простым</span><span class="sxs-lookup"><span data-stu-id="ce15f-228">Do: Keep it simple</span></span>

<span data-ttu-id="ce15f-229">Если приложение требует проверки подлинности, попытайтесь интегрировать единый вход в Microsoft (SSO), чтобы обеспечить более гладкую работу при входе.</span><span class="sxs-lookup"><span data-stu-id="ce15f-229">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="ce15f-230">Кроме того, включайте только существенные сведения и действия по добавлению вкладки.</span><span class="sxs-lookup"><span data-stu-id="ce15f-230">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Иллюстрация, на которой показано, что не следует делать с помощью конструкции настройки вкладок." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="ce15f-232">Не: слишком много шагов</span><span class="sxs-lookup"><span data-stu-id="ce15f-232">Don't: Have too many steps</span></span>

<span data-ttu-id="ce15f-233">Удалите все ненужные действия для добавления вкладки.</span><span class="sxs-lookup"><span data-stu-id="ce15f-233">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="ce15f-234">Темы</span><span class="sxs-lookup"><span data-stu-id="ce15f-234">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Иллюстрация, на которой показано, что делать с вкладками." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="ce15f-236">Do: Воспользуйтесь преимуществами цветовых маркеров для Teams</span><span class="sxs-lookup"><span data-stu-id="ce15f-236">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="ce15f-237">У каждой темы Teams есть своя цветовая схема.</span><span class="sxs-lookup"><span data-stu-id="ce15f-237">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="ce15f-238">Для автоматической обработки изменений темы используйте <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">маркеры цветов (пользовательский интерфейс Fluent)</a> .</span><span class="sxs-lookup"><span data-stu-id="ce15f-238">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Иллюстрация, на которой показано, что не следует делать с вкладками." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="ce15f-240">Не: значения цвета жесткого кода</span><span class="sxs-lookup"><span data-stu-id="ce15f-240">Don't: Hard code color values</span></span>

<span data-ttu-id="ce15f-241">Если вы не используете цветовые маркеры для работы с группами, ваши макеты будут менее масштабируемыми и занимать больше времени на управление.</span><span class="sxs-lookup"><span data-stu-id="ce15f-241">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="ce15f-242">Проверка проекта</span><span class="sxs-lookup"><span data-stu-id="ce15f-242">Validate your design</span></span>

<span data-ttu-id="ce15f-243">Если вы планируете опубликовать свое приложение в AppSource, следует изучить проблемы, которые обычно приводят к сбою приложений во время отправки.</span><span class="sxs-lookup"><span data-stu-id="ce15f-243">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ce15f-244">Проверка рекомендаций по проверке макета</span><span class="sxs-lookup"><span data-stu-id="ce15f-244">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
