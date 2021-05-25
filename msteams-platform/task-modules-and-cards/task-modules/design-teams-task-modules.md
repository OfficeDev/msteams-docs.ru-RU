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
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a><span data-ttu-id="d3b6c-103">Проектирование модулей задач для Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="d3b6c-103">Designing task modules for your Microsoft Teams app</span></span>

<span data-ttu-id="d3b6c-104">Вы можете создавать в приложении модальные всплывающие Teams с помощью модулей задач.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-104">You can create modal popup experiences in your Teams app with task modules.</span></span> <span data-ttu-id="d3b6c-105">Используйте эту возможность для отображения богатых мультимедиа и информации или выполнения сложной задачи.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-105">Use this capability to display rich media and information or complete a complex task.</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="В примере показан модуль задач." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d3b6c-107">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d3b6c-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d3b6c-108">Дополнительные рекомендации по разработке модулей задач, в том числе элементы, которые можно захватить и изменить по мере необходимости, можно найти в Microsoft Teams пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-108">You can find more comprehensive task module design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d3b6c-109">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="d3b6c-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a><span data-ttu-id="d3b6c-110">Откройте модуль задач</span><span class="sxs-lookup"><span data-stu-id="d3b6c-110">Open a task module</span></span>

<span data-ttu-id="d3b6c-111">Модули задач можно запускать практически из любой точки вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-111">Task modules can be launched from almost anywhere in your app.</span></span>

* <span data-ttu-id="d3b6c-112">**Вкладка.** Модуль задач можно запускать по любой ссылке в вкладке. Используйте в сценариях, в которых пользователь должен сосредоточиться на взаимодействии.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-112">**Tab**: A task module can be launched from any link within a tab. Use in scenarios where you want the user to focus on an interaction.</span></span>
* <span data-ttu-id="d3b6c-113">**Бот.** Модуль задач можно запускать по ссылке внутри сообщения бота.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-113">**Bot**: A task module can be launched from a link inside a bot message.</span></span>
* <span data-ttu-id="d3b6c-114">**Адаптивная карта.** Модуль задач можно запускать с адаптивной карты (отправленной с расширением обмена сообщениями или ботом), когда пользователь выбирает кнопку.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-114">**Adaptive Card**: A task module can be launched from an Adaptive Card (sent with a messaging extension or by a bot) when a user selects a button.</span></span>
* <span data-ttu-id="d3b6c-115">**Расширение обмена сообщениями (команды действий)**: Расширения обмена сообщениями позволяют принимать определенные меры по контенту сообщений.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-115">**Messaging extension (action commands)**: Messaging extensions allow you to take a particular action on message content.</span></span> <span data-ttu-id="d3b6c-116">Выбор действия открывает модуль задач.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-116">Selecting an action opens a task module.</span></span>
* <span data-ttu-id="d3b6c-117">**Расширение обмена сообщениями (контекст** композитного окна). В окне составить можно создать расширение обмена сообщениями, чтобы открыть модуль задач вместо обычного флайка.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-117">**Messaging extension (compose box context)**: In the compose box, you can design a messaging extension to open a task module instead of the typical flyout.</span></span> <span data-ttu-id="d3b6c-118">Резервировать модули задач для сложных взаимодействий, таких как заполнение формы.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-118">Reserve task modules for complex interactions, such as completing a form.</span></span>

## <a name="anatomy"></a><span data-ttu-id="d3b6c-119">Анатомия</span><span class="sxs-lookup"><span data-stu-id="d3b6c-119">Anatomy</span></span>

<span data-ttu-id="d3b6c-120">Модули задач обеспечивают гибкую поверхность для работы с хост-приложениями.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-120">Task modules provide a flexible surface for hosted app experiences.</span></span> <span data-ttu-id="d3b6c-121">Они построены с помощью iframe (desktop) или webview (мобильный), поэтому вы можете проектировать модули задач с помощью шаблонов пользовательского интерфейса (рекомендуется) или с нуля.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-121">They're built using an iframe (desktop) or webview (mobile), so you can design task modules with our UI templates (recommended) or from scratch.</span></span>

<span data-ttu-id="d3b6c-122">Они также могут быть построены с помощью базы [адаптивных](../../task-modules-and-cards/cards/design-effective-cards.md) карт, которая может быть более простым и быстрым способом облегчения распространенных сценариев (например, форм).</span><span class="sxs-lookup"><span data-stu-id="d3b6c-122">They can also be built with the [Adaptive Cards](../../task-modules-and-cards/cards/design-effective-cards.md) framework, which can be a simpler and faster way to facilitate common scenarios (such as forms).</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d3b6c-123">Desktop</span><span class="sxs-lookup"><span data-stu-id="d3b6c-123">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса модуля задач." border="false":::

|<span data-ttu-id="d3b6c-125">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d3b6c-125">Counter</span></span>|<span data-ttu-id="d3b6c-126">Описание</span><span class="sxs-lookup"><span data-stu-id="d3b6c-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d3b6c-127">1</span><span class="sxs-lookup"><span data-stu-id="d3b6c-127">1</span></span>|<span data-ttu-id="d3b6c-128">**Значок приложения**</span><span class="sxs-lookup"><span data-stu-id="d3b6c-128">**App icon**</span></span>|
|<span data-ttu-id="d3b6c-129">2</span><span class="sxs-lookup"><span data-stu-id="d3b6c-129">2</span></span>|<span data-ttu-id="d3b6c-130">**Имя приложения.** Полное имя вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="d3b6c-131">3</span><span class="sxs-lookup"><span data-stu-id="d3b6c-131">3</span></span>|<span data-ttu-id="d3b6c-132">**Заглавная:** Сделать заглавные заготки четкими и краткими.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-132">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="d3b6c-133">Опишите задачу, которую необходимо выполнить пользователям.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-133">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="d3b6c-134">4 </span><span class="sxs-lookup"><span data-stu-id="d3b6c-134">4</span></span>|<span data-ttu-id="d3b6c-135">**Кнопка Закрыть:** закрывает модуль задач.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-135">**Close button**: Closes the task module.</span></span> <span data-ttu-id="d3b6c-136">Не применяет неавтные изменения в контенте приложения.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-136">Does not apply unsaved changes in the app content.</span></span>|
|<span data-ttu-id="d3b6c-137">5 </span><span class="sxs-lookup"><span data-stu-id="d3b6c-137">5</span></span>|<span data-ttu-id="d3b6c-138">**iframe**: Гибкое пространство, в котором размещено содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-138">**iframe**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="d3b6c-139">6 </span><span class="sxs-lookup"><span data-stu-id="d3b6c-139">6</span></span>|<span data-ttu-id="d3b6c-140">**Действия (необязательные)**: кнопки, связанные с контентом приложения.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-140">**Actions (optional)**: Buttons related to your app content.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="d3b6c-141">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="d3b6c-141">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-task-module-anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса модуля задач на мобильных устройствах." border="false":::

|<span data-ttu-id="d3b6c-143">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d3b6c-143">Counter</span></span>|<span data-ttu-id="d3b6c-144">Описание</span><span class="sxs-lookup"><span data-stu-id="d3b6c-144">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d3b6c-145">1</span><span class="sxs-lookup"><span data-stu-id="d3b6c-145">1</span></span>|<span data-ttu-id="d3b6c-146">**Заглавная:** Сделать заглавные заготки четкими и краткими.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-146">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="d3b6c-147">Опишите задачу, которую необходимо выполнить пользователям.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-147">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="d3b6c-148">2</span><span class="sxs-lookup"><span data-stu-id="d3b6c-148">2</span></span>|<span data-ttu-id="d3b6c-149">**Имя приложения.** Полное имя вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-149">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="d3b6c-150">3</span><span class="sxs-lookup"><span data-stu-id="d3b6c-150">3</span></span>|<span data-ttu-id="d3b6c-151">**Кнопка Закрыть:** закрывает модуль задач.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-151">**Close button**: Closes the task module.</span></span> <span data-ttu-id="d3b6c-152">Не применяет неавтные изменения в контенте приложения.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-152">Does not apply unsaved changes in the app content.</span></span>|
|<span data-ttu-id="d3b6c-153">4 </span><span class="sxs-lookup"><span data-stu-id="d3b6c-153">4</span></span>|<span data-ttu-id="d3b6c-154">**веб-просмотр.** Отзывчивое пространство, в котором размещено содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-154">**webview**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="d3b6c-155">5 </span><span class="sxs-lookup"><span data-stu-id="d3b6c-155">5</span></span>|<span data-ttu-id="d3b6c-156">**Действия (необязательные)**: кнопки, связанные с контентом приложения.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-156">**Actions (optional)**: Buttons related to your app content.</span></span>|

---

## <a name="designing-with-ui-templates"></a><span data-ttu-id="d3b6c-157">Проектирование с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="d3b6c-157">Designing with UI templates</span></span>

<span data-ttu-id="d3b6c-158">Рассмотрите возможность использования шаблонов для общих макетов внутри модулей задач.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-158">Consider using templates for common layouts inside your task modules.</span></span> <span data-ttu-id="d3b6c-159">Каждый из них состоит из небольших компонентов, чтобы создать элегантный, отзывчивый дизайн, который можно использовать из коробки или настроить для вашего сценария или с вашим брендом внешний вид.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-159">Each one is made up of smaller components to create an elegant, responsive design that can be used out of the box or customized for your scenario or with your brand look and feel.</span></span>

* <span data-ttu-id="d3b6c-160">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-160">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="d3b6c-161">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-161">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="d3b6c-162">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-162">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="examples"></a><span data-ttu-id="d3b6c-163">Примеры</span><span class="sxs-lookup"><span data-stu-id="d3b6c-163">Examples</span></span>

### <a name="list"></a><span data-ttu-id="d3b6c-164">List</span><span class="sxs-lookup"><span data-stu-id="d3b6c-164">List</span></span>

<span data-ttu-id="d3b6c-165">Списки хорошо работают в модуле задач, так как их легко сканировать.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-165">Lists work nicely in a task module because they're easy to scan.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d3b6c-166">Desktop</span><span class="sxs-lookup"><span data-stu-id="d3b6c-166">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Пример списка в модуле задач." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d3b6c-168">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="d3b6c-168">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-list.png" alt-text="Пример списка в модуле задач на мобильных устройствах." border="false":::

---

### <a name="form"></a><span data-ttu-id="d3b6c-170">Form</span><span class="sxs-lookup"><span data-stu-id="d3b6c-170">Form</span></span>

<span data-ttu-id="d3b6c-171">Модули задач — отличное место для поверхности форм с последовательной вводной и входной проверкой пользователей.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-171">Task modules are a great place to surface forms with sequential user inputs and inline validation.</span></span> <span data-ttu-id="d3b6c-172">Адаптивные карты можно использовать как способ встраить элементы формы.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-172">You can leverage Adaptive Cards as a way to embed form elements.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d3b6c-173">Desktop</span><span class="sxs-lookup"><span data-stu-id="d3b6c-173">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Пример формы в модуле задач." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d3b6c-175">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="d3b6c-175">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-form.png" alt-text="Пример формы в модуле задач на мобильных устройствах." border="false":::

---

### <a name="sign-in"></a><span data-ttu-id="d3b6c-177">Вход</span><span class="sxs-lookup"><span data-stu-id="d3b6c-177">Sign in</span></span>

<span data-ttu-id="d3b6c-178">Создайте целенаправленный поток входов или регистрации с помощью ряда модулей задач, что позволяет пользователям легко перемещаться по последовательному шагу.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-178">Create a focused sign in or sign-up flow with a series of task modules, letting users move easily through sequential steps.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d3b6c-179">Desktop</span><span class="sxs-lookup"><span data-stu-id="d3b6c-179">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Например, во время работы в модуле задач." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d3b6c-181">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="d3b6c-181">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-sign-in.png" alt-text="Например, во время работы в модуле задач на мобильных устройствах." border="false":::

---

### <a name="media"></a><span data-ttu-id="d3b6c-183">Мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d3b6c-183">Media</span></span>

<span data-ttu-id="d3b6c-184">Встраить медиаконтент в модуль задач для целенаправленного просмотра.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-184">Embed media content in a task module for a focused viewing experience.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d3b6c-185">Desktop</span><span class="sxs-lookup"><span data-stu-id="d3b6c-185">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Пример содержимого мультимедиа в модуле задач." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d3b6c-187">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="d3b6c-187">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-media.png" alt-text="Пример содержимого мультимедиа в модуле задач на мобильных устройствах." border="false":::

---

### <a name="empty-state"></a><span data-ttu-id="d3b6c-189">Пустое состояние</span><span class="sxs-lookup"><span data-stu-id="d3b6c-189">Empty state</span></span>

<span data-ttu-id="d3b6c-190">Используйте для приветствия, ошибок и сообщений об успехе.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-190">Use for welcome, error, and success messages.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d3b6c-191">Desktop</span><span class="sxs-lookup"><span data-stu-id="d3b6c-191">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Пример пустого состояния в модуле задач." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d3b6c-193">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="d3b6c-193">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-empty-state.png" alt-text="Пример пустого состояния в модуле задач на мобильных устройствах." border="false":::

---

### <a name="image-gallery"></a><span data-ttu-id="d3b6c-195">Коллекция изображений</span><span class="sxs-lookup"><span data-stu-id="d3b6c-195">Image gallery</span></span>

<span data-ttu-id="d3b6c-196">Встраить карусель галереи в iframe (настольный) или веб-просмотр (мобильный).</span><span class="sxs-lookup"><span data-stu-id="d3b6c-196">Embed a gallery carousel in an iframe (desktop) or webview (mobile).</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d3b6c-197">Desktop</span><span class="sxs-lookup"><span data-stu-id="d3b6c-197">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Пример галереи изображений в модуле задач." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d3b6c-199">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="d3b6c-199">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-image-gallery.png" alt-text="Пример галереи изображений в модуле задач на мобильных устройствах." border="false":::

---

### <a name="poll"></a><span data-ttu-id="d3b6c-201">Опрос</span><span class="sxs-lookup"><span data-stu-id="d3b6c-201">Poll</span></span>

<span data-ttu-id="d3b6c-202">В этом примере показаны результаты опроса, запущенные с адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-202">This example shows poll results launched from an Adaptive Card.</span></span> <span data-ttu-id="d3b6c-203">Опрос также можно поместить в модуль задач.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-203">The poll can be placed inside a task module, too.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d3b6c-204">Desktop</span><span class="sxs-lookup"><span data-stu-id="d3b6c-204">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Пример опроса в модуле задач." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d3b6c-206">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="d3b6c-206">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-poll.png" alt-text="Пример опроса в модуле задач на мобильных устройствах." border="false":::

---

## <a name="best-practices"></a><span data-ttu-id="d3b6c-208">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="d3b6c-208">Best practices</span></span>

<span data-ttu-id="d3b6c-209">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-209">Use these recommendations to create a quality app experience.</span></span>

### <a name="usability"></a><span data-ttu-id="d3b6c-210">Usability</span><span class="sxs-lookup"><span data-stu-id="d3b6c-210">Usability</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Пример, показывающий передовую практику модуля задач (по одному модульу задач одновременно)." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a><span data-ttu-id="d3b6c-212">Do: Используйте один модуль задач одновременно</span><span class="sxs-lookup"><span data-stu-id="d3b6c-212">Do: Use one task module at a time</span></span>

<span data-ttu-id="d3b6c-213">Цель заключается в том, чтобы сосредоточить внимание пользователя на выполнении задачи в конце концов!</span><span class="sxs-lookup"><span data-stu-id="d3b6c-213">The goal is to focus the user on completing a task after all!</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (всплывает диалоговое окно в верхней части модуля задач)." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a><span data-ttu-id="d3b6c-215">Не: всплывай диалоговое окно поверх модуля задач</span><span class="sxs-lookup"><span data-stu-id="d3b6c-215">Don't: Pop a dialog on top of a task module</span></span>

<span data-ttu-id="d3b6c-216">Это создает неоконченный, запутанный пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-216">This creates an unfocused, confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive"></a><span data-ttu-id="d3b6c-217">Оперативно</span><span class="sxs-lookup"><span data-stu-id="d3b6c-217">Responsive</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Пример, показывающий передовую практику модуля задач (убедитесь, что содержимое отвечает)." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a><span data-ttu-id="d3b6c-219">Do: Убедитесь, что содержимое отвечает на запросы</span><span class="sxs-lookup"><span data-stu-id="d3b6c-219">Do: Make sure the content is responsive</span></span>

<span data-ttu-id="d3b6c-220">Несмотря на то, что адаптивные карты, которые хорошо отрисовываться в модуле задач на мобильных устройствах, если вы решите использовать iframe для содержимого приложения, убедитесь, что пользовательский интерфейс является отзывчивым и хорошо работает на всех устройствах.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-220">While Adaptive Cards hosted in a task module render well on mobile devices, if you choose to use an iframe to host app content, make sure the UI is responsive and works well across devices.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (не используйте горизонтальные полоски прокрутки)." border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a><span data-ttu-id="d3b6c-222">Не используйте горизонтальные столбики прокрутки</span><span class="sxs-lookup"><span data-stu-id="d3b6c-222">Don't: Use horizontal scroll bars</span></span>

<span data-ttu-id="d3b6c-223">Это лучшая практика, чтобы держать контент сосредоточенным и не слишком длительным.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-223">It's a best practice to keep content focused and not too lengthy.</span></span> <span data-ttu-id="d3b6c-224">Если прокрутка необходима, прокрутите по вертикали, а не по горизонтали.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-224">If a scroll is necessary, scroll vertically and not horizontally.</span></span>

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a><span data-ttu-id="d3b6c-225">Простота</span><span class="sxs-lookup"><span data-stu-id="d3b6c-225">Simplicity</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Пример, показывающий передовую практику модуля задач (не нужно его кратко)." border="false":::

#### <a name="do-keep-it-short"></a><span data-ttu-id="d3b6c-227">Do: Keep it short</span><span class="sxs-lookup"><span data-stu-id="d3b6c-227">Do: Keep it short</span></span>

<span data-ttu-id="d3b6c-228">Вы можете легко создать многоступенчатый мастер, но это не обязательно означает, что вы должны!</span><span class="sxs-lookup"><span data-stu-id="d3b6c-228">You can easily create a multi-step wizard, but that doesn't necessarily mean you should!</span></span> <span data-ttu-id="d3b6c-229">Многоэкранный модуль задач может быть проблематичным, так как входящие сообщения отвлекают и соблазняют пользователей выйти.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-229">A multi-screen task module can be problematic because incoming messages are distracting and tempt users to exit.</span></span> <span data-ttu-id="d3b6c-230">Если ваша задача действительно задействована, выполните полную веб-страницу, а не модуль задач.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-230">If your task is really involved, pop out to a full webpage instead of a task module.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (не имеют длительных взаимодействий)." border="false":::

#### <a name="dont-have-long-interactions"></a><span data-ttu-id="d3b6c-232">Don't: Have long interactions</span><span class="sxs-lookup"><span data-stu-id="d3b6c-232">Don't: Have long interactions</span></span>

<span data-ttu-id="d3b6c-233">Постарайтесь сохранить ваши взаимодействия короткими и до точки.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-233">Try to keep your interactions short and to the point.</span></span>

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a><span data-ttu-id="d3b6c-234">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="d3b6c-234">Error messages</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Пример, показывающий передовую практику модуля задач (использование сообщений об ошибках)." border="false":::

#### <a name="do-use-inline-error-messages"></a><span data-ttu-id="d3b6c-236">Do: Использование сообщений об ошибках с помощью inline</span><span class="sxs-lookup"><span data-stu-id="d3b6c-236">Do: Use inline error messages</span></span>

<span data-ttu-id="d3b6c-237">См. шаблон пользовательского интерфейса форм для инструкций по обработке ошибок.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-237">See the forms UI template for guidelines on inline error handling.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Пример, показывающий передовую практику модуля задач (поместить сообщения об ошибке в диалоги)." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a><span data-ttu-id="d3b6c-239">Не: помещай сообщения об ошибках в диалоговые личные</span><span class="sxs-lookup"><span data-stu-id="d3b6c-239">Don't: Put error messages in dialogs</span></span>

<span data-ttu-id="d3b6c-240">Не всплывай сообщение об ошибке в диалоговом окну над модулем задач.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-240">Don't pop an error message in a dialog on top of a task module.</span></span> <span data-ttu-id="d3b6c-241">Это создает запутанный пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="d3b6c-241">It creates a confusing user experience.</span></span>

   :::column-end:::
:::row-end:::
