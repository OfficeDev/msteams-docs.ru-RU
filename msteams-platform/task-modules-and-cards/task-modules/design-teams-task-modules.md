---
title: Разработка модулей задач
author: heath-hamilton
description: Сведения о проектировании модулей задач для приложений Teams и получении набора UI Microsoft Teams.
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 41584ecf58ca7718290e58e5845549e4579dac64
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606417"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a><span data-ttu-id="ce3ac-103">Разработка модулей задач для приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ce3ac-103">Designing task modules for your Microsoft Teams app</span></span>

<span data-ttu-id="ce3ac-104">Вы можете создавать модальные контекстные меню в приложении Teams с помощью модулей задач.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-104">You can create modal popup experiences in your Teams app with task modules.</span></span> <span data-ttu-id="ce3ac-105">Эта возможность предназначена для отображения мультимедийных данных и данных или выполнения сложной задачи.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-105">Use this capability to display rich media and information or complete a complex task.</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="В примере показан модуль задачи." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="ce3ac-107">Набор элементов пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ce3ac-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="ce3ac-108">Вы можете найти более полные рекомендации по проектированию модулей задач, в том числе элементы, которые можно прихватить и изменить при необходимости, в наборе UI Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-108">You can find more comprehensive task module design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ce3ac-109">Получение набора элементов пользовательского интерфейса Microsoft Teams (фигма)</span><span class="sxs-lookup"><span data-stu-id="ce3ac-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a><span data-ttu-id="ce3ac-110">Открытие модуля задачи</span><span class="sxs-lookup"><span data-stu-id="ce3ac-110">Open a task module</span></span>

<span data-ttu-id="ce3ac-111">Модули задач можно запускать практически из любого места в приложении.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-111">Task modules can be launched from almost anywhere in your app.</span></span>

* <span data-ttu-id="ce3ac-112">**Tab**: модуль задачи можно запустить из любой ссылки на вкладке или в IFRAME.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-112">**Tab**: A task module can be launched from any link within a tab or iframe.</span></span> <span data-ttu-id="ce3ac-113">Используйте в сценариях, где пользователь должен сосредоточиться на взаимодействии.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-113">Use in scenarios where you want the user to focus on an interaction.</span></span>
* <span data-ttu-id="ce3ac-114">**Bot**: модуль задачи можно запустить из ссылки внутри сообщения Bot.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-114">**Bot**: A task module can be launched from a link inside a bot message.</span></span>
* <span data-ttu-id="ce3ac-115">**Адаптивная карта**: модуль задачи можно запустить из адаптивной карточки (отправляемой с помощью расширения обмена сообщениями или с помощью Bot), когда пользователь нажимает кнопку.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-115">**Adaptive Card**: A task module can be launched from an Adaptive Card (sent with a messaging extension or by a bot) when a user selects a button.</span></span>
* <span data-ttu-id="ce3ac-116">**Расширение системы обмена сообщениями (команды действий)**: расширения обмена сообщениями позволяют выполнять определенные действия с содержимым сообщения.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-116">**Messaging extension (action commands)**: Messaging extensions allow you to take a particular action on message content.</span></span> <span data-ttu-id="ce3ac-117">При выборе действия открывается модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-117">Selecting an action opens a task module.</span></span>
* <span data-ttu-id="ce3ac-118">**Расширение системы обмена сообщениями (контекст окна создания)**: в поле Создать можно создать расширение для обмена сообщениями, чтобы открыть модуль задач вместо типичного всплывающего меню.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-118">**Messaging extension (compose box context)**: In the compose box, you can design a messaging extension to open a task module instead of the typical flyout.</span></span> <span data-ttu-id="ce3ac-119">Резервирование модулей задач для сложных взаимодействий, таких как заполнение формы.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-119">Reserve task modules for complex interactions, such as completing a form.</span></span>

## <a name="anatomy"></a><span data-ttu-id="ce3ac-120">Составляющие</span><span class="sxs-lookup"><span data-stu-id="ce3ac-120">Anatomy</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Иллюстрация, демонстрирующая пользовательский интерфейс Анатомия модуля задачи." border="false":::

<span data-ttu-id="ce3ac-122">Модули задач являются очень гибкими поверхностями.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-122">Task modules are very flexible surfaces.</span></span> <span data-ttu-id="ce3ac-123">Они могут быть созданы с помощью iframes, изменяя другие шаблоны пользовательского интерфейса для размещения опыта, созданного партнером.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-123">They can be built with iframes, pulling in other UI templates, to host partner-built experiences.</span></span> <span data-ttu-id="ce3ac-124">Это предпочтительно для наиболее комфортного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-124">This is preferred for the most polished experience.</span></span>

<span data-ttu-id="ce3ac-125">Кроме того, они могут быть созданы с помощью инфраструктуры [адаптивных карт](../../task-modules-and-cards/cards/design-effective-cards.md) , что может быть простым и быстрым способом выполнения распространенных сценариев (таких как формы).</span><span class="sxs-lookup"><span data-stu-id="ce3ac-125">They can also be built with the [Adaptive Card](../../task-modules-and-cards/cards/design-effective-cards.md) framework, which can be a simpler and faster way to execute common scenarios (such as forms).</span></span>

|<span data-ttu-id="ce3ac-126">Счетчик</span><span class="sxs-lookup"><span data-stu-id="ce3ac-126">Counter</span></span>|<span data-ttu-id="ce3ac-127">Описание</span><span class="sxs-lookup"><span data-stu-id="ce3ac-127">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ce3ac-128">1</span><span class="sxs-lookup"><span data-stu-id="ce3ac-128">1</span></span>|<span data-ttu-id="ce3ac-129">**Значок приложения**</span><span class="sxs-lookup"><span data-stu-id="ce3ac-129">**App icon**</span></span>|
|<span data-ttu-id="ce3ac-130">2 </span><span class="sxs-lookup"><span data-stu-id="ce3ac-130">2</span></span>|<span data-ttu-id="ce3ac-131">**Имя приложения**: полное имя приложения.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-131">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="ce3ac-132">3 </span><span class="sxs-lookup"><span data-stu-id="ce3ac-132">3</span></span>|<span data-ttu-id="ce3ac-133">**Верхний колонтитул**: Сделайте заголовки четкими и краткими.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-133">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="ce3ac-134">Опишите задачу, которую должны выполнить пользователи.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-134">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="ce3ac-135">4 </span><span class="sxs-lookup"><span data-stu-id="ce3ac-135">4</span></span>|<span data-ttu-id="ce3ac-136">**Кнопка "Закрыть"**: позволяет пользователям находить контент приложений, которые они хотят вставить.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-136">**Close button**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="ce3ac-137">5 </span><span class="sxs-lookup"><span data-stu-id="ce3ac-137">5</span></span>|<span data-ttu-id="ce3ac-138">**IFRAME**: пространство для ответа, в котором размещается контент вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-138">**iframe**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="ce3ac-139">6 </span><span class="sxs-lookup"><span data-stu-id="ce3ac-139">6</span></span>|<span data-ttu-id="ce3ac-140">**Actions (необязательно)**: кнопки, связанные с контентом приложения.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-140">**Actions (optional)**: Buttons related to your app content.</span></span>|

## <a name="designing-with-ui-templates"></a><span data-ttu-id="ce3ac-141">Разработка с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ce3ac-141">Designing with UI templates</span></span>

<span data-ttu-id="ce3ac-142">Рекомендуется использовать шаблоны для общих макетов внутри модулей задач.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-142">Consider using templates for common layouts inside your task modules.</span></span> <span data-ttu-id="ce3ac-143">Каждый из них состоит из меньших компонентов, чтобы создать элегантный, быстро реагирующий проект, который можно использовать для вашего сценария или для вашего фирменного оформления и оформления.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-143">Each one is made up of smaller components to create an elegant, responsive design that can be used out of the box or customized for your scenario or with your brand look and feel.</span></span>

* <span data-ttu-id="ce3ac-144">[Список](../../concepts/design/design-teams-app-ui-templates.md#list): списки могут отображать связанные элементы в формате с возможностью записи, а пользователи выполнять действия для всего списка или отдельных элементов.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-144">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="ce3ac-145">[Форма](../../concepts/design/design-teams-app-ui-templates.md#form): формы предназначены для сбора, проверки и отправки пользовательских данных структурированным способом.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-145">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="ce3ac-146">[Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state): шаблон пустое состояние можно использовать для многих сценариев, в том числе входа в систему, первого запуска, сообщений об ошибках и многого другого.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-146">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="examples"></a><span data-ttu-id="ce3ac-147">Примеры</span><span class="sxs-lookup"><span data-stu-id="ce3ac-147">Examples</span></span>

### <a name="list"></a><span data-ttu-id="ce3ac-148">Список</span><span class="sxs-lookup"><span data-stu-id="ce3ac-148">List</span></span>

<span data-ttu-id="ce3ac-149">Списки работают хорошо в модуле задачи, так как они просты в сканировании.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-149">Lists work nicely in a task module because they’re easy to scan.</span></span>

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Пример списка в модуле задачи." border="false":::

### <a name="form"></a><span data-ttu-id="ce3ac-151">Form</span><span class="sxs-lookup"><span data-stu-id="ce3ac-151">Form</span></span>

<span data-ttu-id="ce3ac-152">Модули задач — это отличное место для отображения форм с последовательными пользовательскими входными данными и встроенной проверкой.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-152">Task modules are a great place to surface forms with sequential user inputs and inline validation.</span></span> <span data-ttu-id="ce3ac-153">Можно использовать адаптивные карты, чтобы внедрять элементы формы.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-153">You can leverage Adaptive Cards as a way to embed form elements.</span></span>

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Пример формы в модуле задачи." border="false":::

### <a name="sign-in"></a><span data-ttu-id="ce3ac-155">Вход</span><span class="sxs-lookup"><span data-stu-id="ce3ac-155">Sign in</span></span>

<span data-ttu-id="ce3ac-156">С помощью ряда модулей задач создайте сортировку или процесс входа с помощью ряда модулей задач, позволяя пользователям легко перемещаться по последовательным этапам.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-156">Create a focused sign in or sign-up flow with a series of task modules, letting users move easily through sequential steps.</span></span>

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Пример входа в модуле задачи." border="false":::

### <a name="media"></a><span data-ttu-id="ce3ac-158">СМИ</span><span class="sxs-lookup"><span data-stu-id="ce3ac-158">Media</span></span>

<span data-ttu-id="ce3ac-159">Внедрение мультимедийного контента в модуль задач для удобства просмотра.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-159">Embed media content in a task module for a focused viewing experience.</span></span>

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Пример мультимедийного контента в модуле задачи." border="false":::

### <a name="empty-state"></a><span data-ttu-id="ce3ac-161">Пустое состояние</span><span class="sxs-lookup"><span data-stu-id="ce3ac-161">Empty state</span></span>

<span data-ttu-id="ce3ac-162">Используется для сообщений Welcome, Error и Success.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-162">Use for welcome, error, and success messages.</span></span>

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Пример пустого состояния в модуле задачи." border="false":::

### <a name="image-gallery"></a><span data-ttu-id="ce3ac-164">Коллекция изображений</span><span class="sxs-lookup"><span data-stu-id="ce3ac-164">Image gallery</span></span>

<span data-ttu-id="ce3ac-165">Внедрите обойму коллекции в IFRAME.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-165">Embed a gallery carousel inside an iframe.</span></span>

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Пример коллекции изображений в модуле задачи." border="false":::

### <a name="poll"></a><span data-ttu-id="ce3ac-167">Предмет</span><span class="sxs-lookup"><span data-stu-id="ce3ac-167">Poll</span></span>

<span data-ttu-id="ce3ac-168">В этом примере показаны результаты опроса, запущенные из адаптивной карточки.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-168">This example shows poll results launched from an Adaptive Card.</span></span>

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Пример опроса в модуле задачи." border="false":::

## <a name="best-practices"></a><span data-ttu-id="ce3ac-170">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="ce3ac-170">Best practices</span></span>

### <a name="usability"></a><span data-ttu-id="ce3ac-171">Многократ</span><span class="sxs-lookup"><span data-stu-id="ce3ac-171">Usability</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Пример, в котором показана рекомендуемая практика для модуля задачи." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a><span data-ttu-id="ce3ac-173">Do: одновременный использование одного модуля задач</span><span class="sxs-lookup"><span data-stu-id="ce3ac-173">Do: Use one task module at a time</span></span>

<span data-ttu-id="ce3ac-174">Цель состоит в том, чтобы уделить внимание пользователю по завершении задачи.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-174">The goal is to focus the user on completing a task after all!</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Пример, в котором показана рекомендуемая практика для модуля задачи." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a><span data-ttu-id="ce3ac-176">Не: POP диалоговое окно над модулем задач</span><span class="sxs-lookup"><span data-stu-id="ce3ac-176">Don't: Pop a dialog on top of a task module</span></span>

<span data-ttu-id="ce3ac-177">При этом создается несфокусированный, понятный пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-177">This creates an unfocused, confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive"></a><span data-ttu-id="ce3ac-178">Оперативно</span><span class="sxs-lookup"><span data-stu-id="ce3ac-178">Responsive</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Пример, в котором показана рекомендуемая практика для модуля задачи." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a><span data-ttu-id="ce3ac-180">Do: Убедитесь, что содержимое отвечает</span><span class="sxs-lookup"><span data-stu-id="ce3ac-180">Do: Make sure the content is responsive</span></span>

<span data-ttu-id="ce3ac-181">Хотя адаптивные карты, размещенные в модуле задачи, хорошо отображаются на мобильных устройствах, если вы решили использовать iframe для размещения контента приложения, убедитесь, что пользовательский интерфейс отвечает и прекрасно работает на разных устройствах.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-181">While Adaptive Cards hosted in a task module render well on mobile devices, if you choose to use an iframe to host app content, make sure the UI is responsive and works well across devices.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Пример, в котором показана рекомендуемая практика для модуля задачи." border="false":::

#### <a name="dont-use-horizontal-scrollbars"></a><span data-ttu-id="ce3ac-183">Не: использовать горизонтальные полосы прокрутки</span><span class="sxs-lookup"><span data-stu-id="ce3ac-183">Don't: Use horizontal scrollbars</span></span>

<span data-ttu-id="ce3ac-184">Рекомендуется хранить содержание и не слишком много времени.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-184">It's a best practice to keep content focused and not too lengthy.</span></span> <span data-ttu-id="ce3ac-185">При необходимости прокрутки прокрутите вертикально и не горизонтально.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-185">If a scroll is necessary, scroll vertically and not horizontally.</span></span>

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a><span data-ttu-id="ce3ac-186">Простоты</span><span class="sxs-lookup"><span data-stu-id="ce3ac-186">Simplicity</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Пример, в котором показана рекомендуемая практика для модуля задачи." border="false":::

#### <a name="do-keep-it-short"></a><span data-ttu-id="ce3ac-188">Do: оставьте это краткое</span><span class="sxs-lookup"><span data-stu-id="ce3ac-188">Do: Keep it short</span></span>

<span data-ttu-id="ce3ac-189">Вы можете легко создать многошаговый мастер, но это не обязательно означает!</span><span class="sxs-lookup"><span data-stu-id="ce3ac-189">You can easily create a multi-step wizard, but that doesn't necessarily mean you should!</span></span> <span data-ttu-id="ce3ac-190">Многоэкранный модуль задач может вызывать проблемы, так как входящие сообщения отправляются из-за нежелательных пользователей.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-190">A multi-screen task module can be problematic because incoming messages are distracting and tempt users to exit.</span></span> <span data-ttu-id="ce3ac-191">Если ваша задача на самом деле затронута, выйдите на всю веб-страницу, а не на ее модуль.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-191">If your task is really involved, pop out to a full webpage instead of a task module.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Пример, в котором показана рекомендуемая практика для модуля задачи." border="false":::

#### <a name="dont-do-long-interactions"></a><span data-ttu-id="ce3ac-193">Не: выполнение длительных действий</span><span class="sxs-lookup"><span data-stu-id="ce3ac-193">Don't: Do long interactions</span></span>

<span data-ttu-id="ce3ac-194">Постарайтесь оставить свои взаимодействия короче и в точке.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-194">Try to keep your interactions short and to the point.</span></span>

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a><span data-ttu-id="ce3ac-195">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="ce3ac-195">Error messages</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Пример, в котором показана рекомендуемая практика для модуля задачи." border="false":::

#### <a name="do-use-inline-error-messages"></a><span data-ttu-id="ce3ac-197">Do: использовать встроенные сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="ce3ac-197">Do: Use inline error messages</span></span>

<span data-ttu-id="ce3ac-198">Ознакомьтесь с рекомендациями по встроенной обработке ошибок в шаблоне пользовательского интерфейса форм.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-198">See the forms UI template for guidelines on inline error handling.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Пример, в котором показана рекомендуемая практика для модуля задачи." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a><span data-ttu-id="ce3ac-200">Не: помещать сообщения об ошибках в диалоговых окнах</span><span class="sxs-lookup"><span data-stu-id="ce3ac-200">Don't: Put error messages in dialogs</span></span>

<span data-ttu-id="ce3ac-201">Не выявление сообщения об ошибке в диалоговом окне в начале модулей задач.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-201">Don't pop an error message in a dialog on top of a task modules.</span></span> <span data-ttu-id="ce3ac-202">Она создает непонятный пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="ce3ac-202">It creates a confusing user experience.</span></span>

   :::column-end:::
:::row-end:::
