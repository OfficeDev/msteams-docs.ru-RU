---
title: Разработка приложения с помощью расширенных компонентов пользовательского интерфейса
author: heath-hamilton
description: Узнайте о компонентах пользовательского интерфейса, используемых в Teams.
ms.author: surbhigupta
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 6f2bd9cd237751adb15db45bbd6e3cdfea35ce09
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328081"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a><span data-ttu-id="db3b3-103">Разработка приложения Microsoft Teams с расширенными компонентами пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="db3b3-103">Designing your Microsoft Teams app with advanced UI components</span></span>

<span data-ttu-id="db3b3-104">Следующие компоненты — это сочетание базовых [компонентов пользовательского](~/concepts/design/design-teams-app-basic-ui-components.md) интерфейса, которые можно использовать для общих Teams проектирования, таких как навигация.</span><span class="sxs-lookup"><span data-stu-id="db3b3-104">The following components are a combination of [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md) that you can use for common Teams design situations, such as navigation.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="db3b3-105">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="db3b3-105">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="db3b3-106">На основе <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent</a>пользовательского интерфейса Microsoft Teams набор пользовательского интерфейса включает компоненты и шаблоны, разработанные специально для Teams приложений.</span><span class="sxs-lookup"><span data-stu-id="db3b3-106">Based on <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a>, the Microsoft Teams UI Kit includes components and patterns that are designed specifically for building Teams apps.</span></span> <span data-ttu-id="db3b3-107">В наборе пользовательского интерфейса можно захватить и вставить компоненты, перечисленные здесь непосредственно в дизайн, и увидеть дополнительные примеры использования каждого компонента.</span><span class="sxs-lookup"><span data-stu-id="db3b3-107">In the UI kit, you can grab and insert the components listed here directly into your design and see more examples of how to use each component.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db3b3-108">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="db3b3-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a><span data-ttu-id="db3b3-109">Breadcrumb</span><span class="sxs-lookup"><span data-stu-id="db3b3-109">Breadcrumb</span></span>

<span data-ttu-id="db3b3-110">Breadcrumbs — это навигационный помощник, который передает иерархию приложения.</span><span class="sxs-lookup"><span data-stu-id="db3b3-110">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="db3b3-111">Они помогают пользователям понять, как просматриваемая страница вписывается в общий опыт и позволяет одним щелчком мыши получить доступ к более высоким уровням в этой иерархии.</span><span class="sxs-lookup"><span data-stu-id="db3b3-111">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="db3b3-112">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="db3b3-112">Top use cases</span></span>

* <span data-ttu-id="db3b3-113">Иерархия связи</span><span class="sxs-lookup"><span data-stu-id="db3b3-113">Communicate hierarchy</span></span>
* <span data-ttu-id="db3b3-114">Навигация</span><span class="sxs-lookup"><span data-stu-id="db3b3-114">Navigation</span></span>

# <a name="desktop"></a>[<span data-ttu-id="db3b3-115">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="db3b3-115">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="В примере показан шаблон breadcrumb на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="db3b3-117">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="db3b3-117">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="В примере показан шаблон breadcrumb на мобильных устройствах." border="false":::

---

## <a name="left-nav"></a><span data-ttu-id="db3b3-119">Левый nav</span><span class="sxs-lookup"><span data-stu-id="db3b3-119">Left nav</span></span>

<span data-ttu-id="db3b3-120">Используйте левый nav для просмотра нескольких страниц в Teams вкладке. В следующем примере левый nav находится между списком каналов и контентом вкладок.</span><span class="sxs-lookup"><span data-stu-id="db3b3-120">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="db3b3-121">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="db3b3-121">Top use cases</span></span>

* <span data-ttu-id="db3b3-122">Просмотрите несколько страниц в Teams вкладке.</span><span class="sxs-lookup"><span data-stu-id="db3b3-122">Browse multiple pages within a Teams tab.</span></span>
* <span data-ttu-id="db3b3-123">Разбить сложные приложения на несколько страниц.</span><span class="sxs-lookup"><span data-stu-id="db3b3-123">Break down complex apps into multiple pages.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="db3b3-124">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="db3b3-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="В примере показан левый шаблон nav на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="db3b3-126">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="db3b3-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="В примере показан левый шаблон nav на мобильных устройствах." border="false":::

---

## <a name="notification-bar"></a><span data-ttu-id="db3b3-128">Панель уведомлений</span><span class="sxs-lookup"><span data-stu-id="db3b3-128">Notification bar</span></span>

<span data-ttu-id="db3b3-129">Панели уведомлений — это выделенная область для отображения кратких важных сообщений, не требующих от пользователя немедленных действий.</span><span class="sxs-lookup"><span data-stu-id="db3b3-129">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="db3b3-130">Определенные фоновые цвета и значки связаны с определенными типами сообщений (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="db3b3-130">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="db3b3-131">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="db3b3-131">Top use cases</span></span>

* <span data-ttu-id="db3b3-132">Критически важные сообщения, ошибки и предупреждения</span><span class="sxs-lookup"><span data-stu-id="db3b3-132">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="db3b3-133">Сообщения об успехе</span><span class="sxs-lookup"><span data-stu-id="db3b3-133">Success messages</span></span>
* <span data-ttu-id="db3b3-134">Информационные или рекламные сообщения</span><span class="sxs-lookup"><span data-stu-id="db3b3-134">Informational or promotional messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="db3b3-135">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="db3b3-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="В примере показаны шаблоны пользовательского интерфейса панели уведомлений на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="db3b3-137">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="db3b3-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="В примере показан шаблон пользовательского интерфейса панели уведомлений на мобильных устройствах." border="false":::

---

## <a name="stage"></a><span data-ttu-id="db3b3-139">Этап</span><span class="sxs-lookup"><span data-stu-id="db3b3-139">Stage</span></span>

<span data-ttu-id="db3b3-140">Stage позволяет пользователям просматривать контент, например изображение, файл или веб-сайт, на большой поверхности Teams без переключения контекста.</span><span class="sxs-lookup"><span data-stu-id="db3b3-140">Stage lets users view content—like an image, file, or website—on a large surface in Teams without switching context.</span></span> <span data-ttu-id="db3b3-141">Этап предназначен в первую очередь для просмотра контента.</span><span class="sxs-lookup"><span data-stu-id="db3b3-141">Stage is primarily for viewing content.</span></span> <span data-ttu-id="db3b3-142">Не используйте этап для сложных взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="db3b3-142">Don’t use stage for complex interactions.</span></span>

<span data-ttu-id="db3b3-143">Узнайте, как реализовать [этап](~/tabs/tabs-link-unfurling.md).</span><span class="sxs-lookup"><span data-stu-id="db3b3-143">Learn how to implement [stage](~/tabs/tabs-link-unfurling.md).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="db3b3-144">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="db3b3-144">Top use cases</span></span>

* <span data-ttu-id="db3b3-145">Отображение контента на большой поверхности в Teams вместо другого приложения или браузера</span><span class="sxs-lookup"><span data-stu-id="db3b3-145">Display content in a large surface within Teams instead of another app or browser</span></span>
* <span data-ttu-id="db3b3-146">Прожектор мультимедиа или другой контент с богатыми данными</span><span class="sxs-lookup"><span data-stu-id="db3b3-146">Spotlight media or other rich content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="db3b3-147">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="db3b3-147">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="В примере показан шаблон сцены на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="db3b3-149">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="db3b3-149">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="db3b3-150">Ваше приложение может запускать этап из адаптивной карты, общих ссылок или визуальных компонентов (например, диаграммы).</span><span class="sxs-lookup"><span data-stu-id="db3b3-150">Your app can launch a stage from an Adaptive Card, shared link, or visual components (such as a chart).</span></span>

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="В примере показан шаблон сцены на мобильных устройствах." border="false":::

---

## <a name="toolbar"></a><span data-ttu-id="db3b3-152">Панель инструментов</span><span class="sxs-lookup"><span data-stu-id="db3b3-152">Toolbar</span></span>

<span data-ttu-id="db3b3-153">Панель инструментов — это контейнер для группировки набора элементов управления.</span><span class="sxs-lookup"><span data-stu-id="db3b3-153">A toolbar is a container for grouping a set of controls.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="db3b3-154">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="db3b3-154">Top use cases</span></span>

* <span data-ttu-id="db3b3-155">Контекстные действия в контенте приложения</span><span class="sxs-lookup"><span data-stu-id="db3b3-155">Contextual actions on app content</span></span>
* <span data-ttu-id="db3b3-156">Контекстный фильтр и поиск</span><span class="sxs-lookup"><span data-stu-id="db3b3-156">Contextual filter and find</span></span>
* <span data-ttu-id="db3b3-157">Навигация и сухари</span><span class="sxs-lookup"><span data-stu-id="db3b3-157">Navigation and breadcrumbs</span></span>

# <a name="desktop"></a>[<span data-ttu-id="db3b3-158">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="db3b3-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="В примере показан шаблон панели инструментов на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="db3b3-160">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="db3b3-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="В примере показан шаблон панели инструментов на мобильных устройствах." border="false":::

---
