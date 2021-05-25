---
title: Разработка приложения с помощью расширенных компонентов пользовательского интерфейса
author: heath-hamilton
description: Узнайте о компонентах пользовательского интерфейса, используемых в Teams.
ms.author: surbhigupta
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: ae1c2793586dc638d56051e105482aac92e01091
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644944"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a><span data-ttu-id="94c6a-103">Разработка приложения Microsoft Teams с расширенными компонентами пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="94c6a-103">Designing your Microsoft Teams app with advanced UI components</span></span>

<span data-ttu-id="94c6a-104">Следующие компоненты — это сочетание базовых [компонентов пользовательского](~/concepts/design/design-teams-app-basic-ui-components.md) интерфейса, которые можно использовать для общих Teams проектирования, таких как навигация.</span><span class="sxs-lookup"><span data-stu-id="94c6a-104">The following components are a combination of [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md) that you can use for common Teams design situations, such as navigation.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="94c6a-105">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="94c6a-105">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="94c6a-106">На основе пользовательского интерфейса <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent</a>Microsoft Teams пользовательского интерфейса включает компоненты и шаблоны, разработанные специально для создания Teams приложений.</span><span class="sxs-lookup"><span data-stu-id="94c6a-106">Based on <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a>, the Microsoft Teams UI Kit includes components and patterns that are designed specifically for building Teams apps.</span></span> <span data-ttu-id="94c6a-107">В наборе пользовательского интерфейса можно захватить и вставить компоненты, перечисленные здесь непосредственно в дизайн, и увидеть дополнительные примеры использования каждого компонента.</span><span class="sxs-lookup"><span data-stu-id="94c6a-107">In the UI kit, you can grab and insert the components listed here directly into your design and see more examples of how to use each component.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94c6a-108">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="94c6a-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a><span data-ttu-id="94c6a-109">Breadcrumb</span><span class="sxs-lookup"><span data-stu-id="94c6a-109">Breadcrumb</span></span>

<span data-ttu-id="94c6a-110">Breadcrumbs — это навигационный помощник, который передает иерархию приложения.</span><span class="sxs-lookup"><span data-stu-id="94c6a-110">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="94c6a-111">Они помогают пользователям понять, как просматриваемая страница вписывается в общий опыт и позволяет одним щелчком мыши получить доступ к более высоким уровням в этой иерархии.</span><span class="sxs-lookup"><span data-stu-id="94c6a-111">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="94c6a-112">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="94c6a-112">Top use cases</span></span>

* <span data-ttu-id="94c6a-113">Иерархия связи</span><span class="sxs-lookup"><span data-stu-id="94c6a-113">Communicate hierarchy</span></span>
* <span data-ttu-id="94c6a-114">Навигация</span><span class="sxs-lookup"><span data-stu-id="94c6a-114">Navigation</span></span>

# <a name="desktop"></a>[<span data-ttu-id="94c6a-115">Desktop</span><span class="sxs-lookup"><span data-stu-id="94c6a-115">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="В примере показан шаблон breadcrumb на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="94c6a-117">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="94c6a-117">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="В примере показан шаблон breadcrumb на мобильных устройствах." border="false":::

---

## <a name="left-nav"></a><span data-ttu-id="94c6a-119">Левый nav</span><span class="sxs-lookup"><span data-stu-id="94c6a-119">Left nav</span></span>

<span data-ttu-id="94c6a-120">Используйте левый nav для просмотра нескольких страниц в Teams вкладке. В следующем примере левый nav находится между списком каналов и контентом вкладок.</span><span class="sxs-lookup"><span data-stu-id="94c6a-120">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="94c6a-121">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="94c6a-121">Top use cases</span></span>

* <span data-ttu-id="94c6a-122">Просмотрите несколько страниц в Teams вкладке.</span><span class="sxs-lookup"><span data-stu-id="94c6a-122">Browse multiple pages within a Teams tab.</span></span>
* <span data-ttu-id="94c6a-123">Разбить сложные приложения на несколько страниц.</span><span class="sxs-lookup"><span data-stu-id="94c6a-123">Break down complex apps into multiple pages.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="94c6a-124">Desktop</span><span class="sxs-lookup"><span data-stu-id="94c6a-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="В примере показан левый шаблон nav на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="94c6a-126">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="94c6a-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="В примере показан левый шаблон nav на мобильных устройствах." border="false":::

---

## <a name="notification-bar"></a><span data-ttu-id="94c6a-128">Панель уведомлений</span><span class="sxs-lookup"><span data-stu-id="94c6a-128">Notification bar</span></span>

<span data-ttu-id="94c6a-129">Панели уведомлений — это выделенная область для отображения кратких важных сообщений, не требующих от пользователя немедленных действий.</span><span class="sxs-lookup"><span data-stu-id="94c6a-129">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="94c6a-130">Определенные фоновые цвета и значки связаны с определенными типами сообщений (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="94c6a-130">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="94c6a-131">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="94c6a-131">Top use cases</span></span>

* <span data-ttu-id="94c6a-132">Критически важные сообщения, ошибки и предупреждения</span><span class="sxs-lookup"><span data-stu-id="94c6a-132">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="94c6a-133">Сообщения об успехе</span><span class="sxs-lookup"><span data-stu-id="94c6a-133">Success messages</span></span>
* <span data-ttu-id="94c6a-134">Информационные или рекламные сообщения</span><span class="sxs-lookup"><span data-stu-id="94c6a-134">Informational or promotional messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="94c6a-135">Desktop</span><span class="sxs-lookup"><span data-stu-id="94c6a-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="В примере показаны шаблоны пользовательского интерфейса панели уведомлений на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="94c6a-137">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="94c6a-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="В примере показан шаблон пользовательского интерфейса панели уведомлений на мобильных устройствах." border="false":::

---

## <a name="stage"></a><span data-ttu-id="94c6a-139">Этап</span><span class="sxs-lookup"><span data-stu-id="94c6a-139">Stage</span></span>

<span data-ttu-id="94c6a-140">Stage предоставляет пользователям возможность открыть объект — например, изображение, файл или веб-Teams, а не открывать его в другом приложении или браузере.</span><span class="sxs-lookup"><span data-stu-id="94c6a-140">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="94c6a-141">Основной пример использования стадии — просмотр; поверхность не должна использоваться для сложных взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="94c6a-141">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="94c6a-142">(Примечание реализации. Создайте этап с помощью большого [модуля задач.)](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="94c6a-142">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="94c6a-143">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="94c6a-143">Top use cases</span></span>

* <span data-ttu-id="94c6a-144">Откройте объект в Teams вместо другого приложения или браузера</span><span class="sxs-lookup"><span data-stu-id="94c6a-144">Open an entity in Teams instead of another app or browser</span></span>
* <span data-ttu-id="94c6a-145">Прожектор мультимедиа или другой контент</span><span class="sxs-lookup"><span data-stu-id="94c6a-145">Spotlight media or other content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="94c6a-146">Desktop</span><span class="sxs-lookup"><span data-stu-id="94c6a-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="В примере показан шаблон сцены на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="94c6a-148">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="94c6a-148">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="94c6a-149">Ваше приложение может запускать этап из адаптивной карты, общих ссылок или визуальных компонентов (например, диаграммы).</span><span class="sxs-lookup"><span data-stu-id="94c6a-149">Your app can launch a stage from an Adaptive Card, shared link, or visual components (such as a chart).</span></span>

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="В примере показан шаблон сцены на мобильных устройствах." border="false":::

---

## <a name="toolbar"></a><span data-ttu-id="94c6a-151">Панель инструментов</span><span class="sxs-lookup"><span data-stu-id="94c6a-151">Toolbar</span></span>

<span data-ttu-id="94c6a-152">Панель инструментов — это контейнер для группировки набора элементов управления.</span><span class="sxs-lookup"><span data-stu-id="94c6a-152">A toolbar is a container for grouping a set of controls.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="94c6a-153">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="94c6a-153">Top use cases</span></span>

* <span data-ttu-id="94c6a-154">Контекстные действия в контенте приложения</span><span class="sxs-lookup"><span data-stu-id="94c6a-154">Contextual actions on app content</span></span>
* <span data-ttu-id="94c6a-155">Контекстный фильтр и поиск</span><span class="sxs-lookup"><span data-stu-id="94c6a-155">Contextual filter and find</span></span>
* <span data-ttu-id="94c6a-156">Навигация и сухари</span><span class="sxs-lookup"><span data-stu-id="94c6a-156">Navigation and breadcrumbs</span></span>

# <a name="desktop"></a>[<span data-ttu-id="94c6a-157">Desktop</span><span class="sxs-lookup"><span data-stu-id="94c6a-157">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="В примере показан шаблон панели инструментов на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="94c6a-159">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="94c6a-159">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="В примере показан шаблон панели инструментов на мобильных устройствах." border="false":::

---
