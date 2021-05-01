---
title: Проектирование модулей задач
author: heath-hamilton
description: Узнайте, как разработать модули задач для Teams приложений и получить Microsoft Teams пользовательского интерфейса.
localization_priority: Normal
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 347ce42c41706f698e2f8897a0518aae0850a275
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101732"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a><span data-ttu-id="b4522-103">Проектирование модулей задач для Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="b4522-103">Designing task modules for your Microsoft Teams app</span></span>

<span data-ttu-id="b4522-104">Вы можете создавать в приложении модальные всплывающие Teams с помощью модулей задач.</span><span class="sxs-lookup"><span data-stu-id="b4522-104">You can create modal popup experiences in your Teams app with task modules.</span></span> <span data-ttu-id="b4522-105">Используйте эту возможность для отображения богатых мультимедиа и информации или выполнения сложной задачи.</span><span class="sxs-lookup"><span data-stu-id="b4522-105">Use this capability to display rich media and information or complete a complex task.</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="В примере показан модуль задач." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="b4522-107">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b4522-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="b4522-108">Дополнительные рекомендации по разработке модулей задач, в том числе элементы, которые можно захватить и изменить по мере необходимости, можно найти в Microsoft Teams пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b4522-108">You can find more comprehensive task module design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4522-109">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="b4522-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a><span data-ttu-id="b4522-110">Откройте модуль задач</span><span class="sxs-lookup"><span data-stu-id="b4522-110">Open a task module</span></span>

<span data-ttu-id="b4522-111">Модули задач можно запускать практически из любой точки вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="b4522-111">Task modules can be launched from almost anywhere in your app.</span></span>

* <span data-ttu-id="b4522-112">**Вкладка.** Модуль задач можно запускать по любой ссылке в вкладке. Используйте в сценариях, в которых пользователь должен сосредоточиться на взаимодействии.</span><span class="sxs-lookup"><span data-stu-id="b4522-112">**Tab**: A task module can be launched from any link within a tab. Use in scenarios where you want the user to focus on an interaction.</span></span>
* <span data-ttu-id="b4522-113">**Бот.** Модуль задач можно запускать по ссылке внутри сообщения бота.</span><span class="sxs-lookup"><span data-stu-id="b4522-113">**Bot**: A task module can be launched from a link inside a bot message.</span></span>
* <span data-ttu-id="b4522-114">**Адаптивная карта.** Модуль задач можно запускать с адаптивной карты (отправленной с расширением обмена сообщениями или ботом), когда пользователь выбирает кнопку.</span><span class="sxs-lookup"><span data-stu-id="b4522-114">**Adaptive Card**: A task module can be launched from an Adaptive Card (sent with a messaging extension or by a bot) when a user selects a button.</span></span>
* <span data-ttu-id="b4522-115">**Расширение обмена сообщениями (команды действий)**: Расширения обмена сообщениями позволяют принимать определенные меры по контенту сообщений.</span><span class="sxs-lookup"><span data-stu-id="b4522-115">**Messaging extension (action commands)**: Messaging extensions allow you to take a particular action on message content.</span></span> <span data-ttu-id="b4522-116">Выбор действия открывает модуль задач.</span><span class="sxs-lookup"><span data-stu-id="b4522-116">Selecting an action opens a task module.</span></span>
* <span data-ttu-id="b4522-117">**Расширение обмена сообщениями (контекст** композитного окна). В окне составить можно создать расширение обмена сообщениями, чтобы открыть модуль задач вместо обычного флайка.</span><span class="sxs-lookup"><span data-stu-id="b4522-117">**Messaging extension (compose box context)**: In the compose box, you can design a messaging extension to open a task module instead of the typical flyout.</span></span> <span data-ttu-id="b4522-118">Резервировать модули задач для сложных взаимодействий, таких как заполнение формы.</span><span class="sxs-lookup"><span data-stu-id="b4522-118">Reserve task modules for complex interactions, such as completing a form.</span></span>

## <a name="anatomy"></a><span data-ttu-id="b4522-119">Анатомия</span><span class="sxs-lookup"><span data-stu-id="b4522-119">Anatomy</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса модуля задач." border="false":::

<span data-ttu-id="b4522-121">Модули задач — это очень гибкие поверхности.</span><span class="sxs-lookup"><span data-stu-id="b4522-121">Task modules are very flexible surfaces.</span></span> <span data-ttu-id="b4522-122">Они могут быть построены с помощью iframes, потянув в другие шаблоны пользовательского интерфейса, для хост-партнеров, построенных опытом.</span><span class="sxs-lookup"><span data-stu-id="b4522-122">They can be built with iframes, pulling in other UI templates, to host partner-built experiences.</span></span> <span data-ttu-id="b4522-123">Это предпочтительнее для наиболее отполированной работы.</span><span class="sxs-lookup"><span data-stu-id="b4522-123">This is preferred for the most polished experience.</span></span>

<span data-ttu-id="b4522-124">Они также могут быть [](../../task-modules-and-cards/cards/design-effective-cards.md) построены с помощью адаптивной карты, которая может быть проще и быстрее для выполнения общих сценариев (например, форм).</span><span class="sxs-lookup"><span data-stu-id="b4522-124">They can also be built with the [Adaptive Card](../../task-modules-and-cards/cards/design-effective-cards.md) framework, which can be a simpler and faster way to execute common scenarios (such as forms).</span></span>

|<span data-ttu-id="b4522-125">Счетчик</span><span class="sxs-lookup"><span data-stu-id="b4522-125">Counter</span></span>|<span data-ttu-id="b4522-126">Описание</span><span class="sxs-lookup"><span data-stu-id="b4522-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b4522-127">1</span><span class="sxs-lookup"><span data-stu-id="b4522-127">1</span></span>|<span data-ttu-id="b4522-128">**Значок приложения**</span><span class="sxs-lookup"><span data-stu-id="b4522-128">**App icon**</span></span>|
|<span data-ttu-id="b4522-129">2</span><span class="sxs-lookup"><span data-stu-id="b4522-129">2</span></span>|<span data-ttu-id="b4522-130">**Имя приложения.** Полное имя вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="b4522-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="b4522-131">3</span><span class="sxs-lookup"><span data-stu-id="b4522-131">3</span></span>|<span data-ttu-id="b4522-132">**Заглавная:** Сделать заглавные заготки четкими и краткими.</span><span class="sxs-lookup"><span data-stu-id="b4522-132">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="b4522-133">Опишите задачу, которую необходимо выполнить пользователям.</span><span class="sxs-lookup"><span data-stu-id="b4522-133">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="b4522-134">4 </span><span class="sxs-lookup"><span data-stu-id="b4522-134">4</span></span>|<span data-ttu-id="b4522-135">**Кнопка Закрыть.** Позволяет пользователям находить содержимое приложения, которое они хотят вставить.</span><span class="sxs-lookup"><span data-stu-id="b4522-135">**Close button**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="b4522-136">5 </span><span class="sxs-lookup"><span data-stu-id="b4522-136">5</span></span>|<span data-ttu-id="b4522-137">**iframe**: Гибкое пространство, в котором размещено содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="b4522-137">**iframe**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="b4522-138">6 </span><span class="sxs-lookup"><span data-stu-id="b4522-138">6</span></span>|<span data-ttu-id="b4522-139">**Действия (необязательные)**: кнопки, связанные с контентом приложения.</span><span class="sxs-lookup"><span data-stu-id="b4522-139">**Actions (optional)**: Buttons related to your app content.</span></span>|

## <a name="designing-with-ui-templates"></a><span data-ttu-id="b4522-140">Проектирование с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="b4522-140">Designing with UI templates</span></span>

<span data-ttu-id="b4522-141">Рассмотрите возможность использования шаблонов для общих макетов внутри модулей задач.</span><span class="sxs-lookup"><span data-stu-id="b4522-141">Consider using templates for common layouts inside your task modules.</span></span> <span data-ttu-id="b4522-142">Каждый из них состоит из небольших компонентов, чтобы создать элегантный, отзывчивый дизайн, который можно использовать из коробки или настроить для вашего сценария или с вашим брендом внешний вид.</span><span class="sxs-lookup"><span data-stu-id="b4522-142">Each one is made up of smaller components to create an elegant, responsive design that can be used out of the box or customized for your scenario or with your brand look and feel.</span></span>

* <span data-ttu-id="b4522-143">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="b4522-143">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="b4522-144">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="b4522-144">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="b4522-145">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="b4522-145">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="examples"></a><span data-ttu-id="b4522-146">Примеры</span><span class="sxs-lookup"><span data-stu-id="b4522-146">Examples</span></span>

### <a name="list"></a><span data-ttu-id="b4522-147">List</span><span class="sxs-lookup"><span data-stu-id="b4522-147">List</span></span>

<span data-ttu-id="b4522-148">Списки хорошо работают в модуле задач, так как их легко сканировать.</span><span class="sxs-lookup"><span data-stu-id="b4522-148">Lists work nicely in a task module because they’re easy to scan.</span></span>

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Пример списка в модуле задач." border="false":::

### <a name="form"></a><span data-ttu-id="b4522-150">Форма</span><span class="sxs-lookup"><span data-stu-id="b4522-150">Form</span></span>

<span data-ttu-id="b4522-151">Модули задач — отличное место для поверхности форм с последовательной вводной и входной проверкой пользователей.</span><span class="sxs-lookup"><span data-stu-id="b4522-151">Task modules are a great place to surface forms with sequential user inputs and inline validation.</span></span> <span data-ttu-id="b4522-152">Адаптивные карты можно использовать как способ встраить элементы формы.</span><span class="sxs-lookup"><span data-stu-id="b4522-152">You can leverage Adaptive Cards as a way to embed form elements.</span></span>

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Пример формы в модуле задач." border="false":::

### <a name="sign-in"></a><span data-ttu-id="b4522-154">Вход</span><span class="sxs-lookup"><span data-stu-id="b4522-154">Sign in</span></span>

<span data-ttu-id="b4522-155">Создайте целенаправленный поток входов или регистрации с помощью ряда модулей задач, что позволяет пользователям легко перемещаться по последовательному шагу.</span><span class="sxs-lookup"><span data-stu-id="b4522-155">Create a focused sign in or sign-up flow with a series of task modules, letting users move easily through sequential steps.</span></span>

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Например, во время работы в модуле задач." border="false":::

### <a name="media"></a><span data-ttu-id="b4522-157">Media</span><span class="sxs-lookup"><span data-stu-id="b4522-157">Media</span></span>

<span data-ttu-id="b4522-158">Встраить медиаконтент в модуль задач для целенаправленного просмотра.</span><span class="sxs-lookup"><span data-stu-id="b4522-158">Embed media content in a task module for a focused viewing experience.</span></span>

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Пример содержимого мультимедиа в модуле задач." border="false":::

### <a name="empty-state"></a><span data-ttu-id="b4522-160">Пустое состояние</span><span class="sxs-lookup"><span data-stu-id="b4522-160">Empty state</span></span>

<span data-ttu-id="b4522-161">Используйте для приветствия, ошибок и сообщений об успехе.</span><span class="sxs-lookup"><span data-stu-id="b4522-161">Use for welcome, error, and success messages.</span></span>

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Пример пустого состояния в модуле задач." border="false":::

### <a name="image-gallery"></a><span data-ttu-id="b4522-163">Коллекция изображений</span><span class="sxs-lookup"><span data-stu-id="b4522-163">Image gallery</span></span>

<span data-ttu-id="b4522-164">Встраить карусель галереи в iframe.</span><span class="sxs-lookup"><span data-stu-id="b4522-164">Embed a gallery carousel in an iframe.</span></span>

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Пример галереи изображений в модуле задач." border="false":::

### <a name="poll"></a><span data-ttu-id="b4522-166">Опрос</span><span class="sxs-lookup"><span data-stu-id="b4522-166">Poll</span></span>

<span data-ttu-id="b4522-167">В этом примере показаны результаты опроса, запущенные с адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="b4522-167">This example shows poll results launched from an Adaptive Card.</span></span> <span data-ttu-id="b4522-168">Опрос также можно поместить в модуль задач.</span><span class="sxs-lookup"><span data-stu-id="b4522-168">The poll can be placed inside a task module, too.</span></span>

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Пример опроса в модуле задач." border="false":::

## <a name="best-practices"></a><span data-ttu-id="b4522-170">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="b4522-170">Best practices</span></span>

<span data-ttu-id="b4522-171">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="b4522-171">Use these recommendations to create a quality app experience.</span></span>

### <a name="usability"></a><span data-ttu-id="b4522-172">Usability</span><span class="sxs-lookup"><span data-stu-id="b4522-172">Usability</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Пример, показывающий передовую практику модуля задач (по одному модульу задач одновременно)." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a><span data-ttu-id="b4522-174">Do: Используйте один модуль задач одновременно</span><span class="sxs-lookup"><span data-stu-id="b4522-174">Do: Use one task module at a time</span></span>

<span data-ttu-id="b4522-175">Цель заключается в том, чтобы сосредоточить внимание пользователя на выполнении задачи в конце концов!</span><span class="sxs-lookup"><span data-stu-id="b4522-175">The goal is to focus the user on completing a task after all!</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (всплывает диалоговое окно в верхней части модуля задач)." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a><span data-ttu-id="b4522-177">Не: всплывай диалоговое окно поверх модуля задач</span><span class="sxs-lookup"><span data-stu-id="b4522-177">Don't: Pop a dialog on top of a task module</span></span>

<span data-ttu-id="b4522-178">Это создает неоконченный, запутанный пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="b4522-178">This creates an unfocused, confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive"></a><span data-ttu-id="b4522-179">Оперативно</span><span class="sxs-lookup"><span data-stu-id="b4522-179">Responsive</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Пример, показывающий передовую практику модуля задач (убедитесь, что содержимое отвечает)." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a><span data-ttu-id="b4522-181">Do: Убедитесь, что содержимое отвечает на запросы</span><span class="sxs-lookup"><span data-stu-id="b4522-181">Do: Make sure the content is responsive</span></span>

<span data-ttu-id="b4522-182">Несмотря на то, что адаптивные карты, которые хорошо отрисовываться в модуле задач на мобильных устройствах, если вы решите использовать iframe для содержимого приложения, убедитесь, что пользовательский интерфейс является отзывчивым и хорошо работает на всех устройствах.</span><span class="sxs-lookup"><span data-stu-id="b4522-182">While Adaptive Cards hosted in a task module render well on mobile devices, if you choose to use an iframe to host app content, make sure the UI is responsive and works well across devices.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (не используйте горизонтальные полоски прокрутки)." border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a><span data-ttu-id="b4522-184">Не используйте горизонтальные столбики прокрутки</span><span class="sxs-lookup"><span data-stu-id="b4522-184">Don't: Use horizontal scroll bars</span></span>

<span data-ttu-id="b4522-185">Это лучшая практика, чтобы держать контент сосредоточенным и не слишком длительным.</span><span class="sxs-lookup"><span data-stu-id="b4522-185">It's a best practice to keep content focused and not too lengthy.</span></span> <span data-ttu-id="b4522-186">Если прокрутка необходима, прокрутите по вертикали, а не по горизонтали.</span><span class="sxs-lookup"><span data-stu-id="b4522-186">If a scroll is necessary, scroll vertically and not horizontally.</span></span>

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a><span data-ttu-id="b4522-187">Простота</span><span class="sxs-lookup"><span data-stu-id="b4522-187">Simplicity</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Пример, показывающий передовую практику модуля задач (не нужно его кратко)." border="false":::

#### <a name="do-keep-it-short"></a><span data-ttu-id="b4522-189">Do: Keep it short</span><span class="sxs-lookup"><span data-stu-id="b4522-189">Do: Keep it short</span></span>

<span data-ttu-id="b4522-190">Вы можете легко создать многоступенчатый мастер, но это не обязательно означает, что вы должны!</span><span class="sxs-lookup"><span data-stu-id="b4522-190">You can easily create a multi-step wizard, but that doesn't necessarily mean you should!</span></span> <span data-ttu-id="b4522-191">Многоэкранный модуль задач может быть проблематичным, так как входящие сообщения отвлекают и соблазняют пользователей выйти.</span><span class="sxs-lookup"><span data-stu-id="b4522-191">A multi-screen task module can be problematic because incoming messages are distracting and tempt users to exit.</span></span> <span data-ttu-id="b4522-192">Если ваша задача действительно задействована, выполните полную веб-страницу, а не модуль задач.</span><span class="sxs-lookup"><span data-stu-id="b4522-192">If your task is really involved, pop out to a full webpage instead of a task module.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (не имеют длительных взаимодействий)." border="false":::

#### <a name="dont-have-long-interactions"></a><span data-ttu-id="b4522-194">Don't: Have long interactions</span><span class="sxs-lookup"><span data-stu-id="b4522-194">Don't: Have long interactions</span></span>

<span data-ttu-id="b4522-195">Постарайтесь сохранить ваши взаимодействия короткими и до точки.</span><span class="sxs-lookup"><span data-stu-id="b4522-195">Try to keep your interactions short and to the point.</span></span>

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a><span data-ttu-id="b4522-196">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="b4522-196">Error messages</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Пример, показывающий передовую практику модуля задач (использование сообщений об ошибках)." border="false":::

#### <a name="do-use-inline-error-messages"></a><span data-ttu-id="b4522-198">Do: Использование сообщений об ошибках с помощью inline</span><span class="sxs-lookup"><span data-stu-id="b4522-198">Do: Use inline error messages</span></span>

<span data-ttu-id="b4522-199">См. шаблон пользовательского интерфейса форм для инструкций по обработке ошибок.</span><span class="sxs-lookup"><span data-stu-id="b4522-199">See the forms UI template for guidelines on inline error handling.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (поместить сообщения об ошибке в диалоги)." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a><span data-ttu-id="b4522-201">Не: помещай сообщения об ошибках в диалоговые личные</span><span class="sxs-lookup"><span data-stu-id="b4522-201">Don't: Put error messages in dialogs</span></span>

<span data-ttu-id="b4522-202">Не всплывай сообщение об ошибке в диалоговом окну поверх модулей задач.</span><span class="sxs-lookup"><span data-stu-id="b4522-202">Don't pop an error message in a dialog on top of a task modules.</span></span> <span data-ttu-id="b4522-203">Это создает запутанный пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="b4522-203">It creates a confusing user experience.</span></span>

   :::column-end:::
:::row-end:::
