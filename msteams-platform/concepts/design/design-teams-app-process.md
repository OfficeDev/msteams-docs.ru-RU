---
title: Процесс разработки приложения
author: heath-hamilton
description: Получите общее представление о том, как и когда можно использовать средства и ресурсы Майкрософт для разработки эффективного Microsoft Teams приложения.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 533d386db2aa784fc7de955f92f64d07789f0553
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631387"
---
# <a name="design-process-for-microsoft-teams-apps"></a><span data-ttu-id="a2276-103">Процесс разработки Microsoft Teams приложений</span><span class="sxs-lookup"><span data-stu-id="a2276-103">Design process for Microsoft Teams apps</span></span>

<span data-ttu-id="a2276-104">Существует несколько средств и ресурсов для разработки Microsoft Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="a2276-104">There are multiple tools and resources for designing your Microsoft Teams app.</span></span> <span data-ttu-id="a2276-105">В следующих действиях описывается, когда и как их можно использовать в процессе разработки.</span><span class="sxs-lookup"><span data-stu-id="a2276-105">The following steps describe when and how you might use these during the design process.</span></span> <span data-ttu-id="a2276-106">(Некоторые действия могут быть технически вне процесса разработки, но включены для дополнительного контекста.)</span><span class="sxs-lookup"><span data-stu-id="a2276-106">(Some of steps might be technically outside the design process but are included for additional context.)</span></span>

:::image type="content" source="~/assets/images/design-guidelines/teams-app-design-process.png" alt-text="Схема, показывающая пример процесса Teams приложения." border="false":::

## <a name="plan-your-app"></a><span data-ttu-id="a2276-108">Планирование приложения</span><span class="sxs-lookup"><span data-stu-id="a2276-108">Plan your app</span></span>

<span data-ttu-id="a2276-109">Разработка высококачественного приложения Teams требует понимания того, что вы хотите, чтобы приложение и как вы думаете, что люди будут его использовать.</span><span class="sxs-lookup"><span data-stu-id="a2276-109">Designing a high-quality Teams app requires understanding what you want the app to do and how you think people will use it.</span></span> <span data-ttu-id="a2276-110">Однако прежде чем приступить к разработке, ответьте на следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="a2276-110">Before you start designing, however, answer the following questions:</span></span>

* <span data-ttu-id="a2276-111">Кто ваши пользователи?</span><span class="sxs-lookup"><span data-stu-id="a2276-111">Who are your users?</span></span>
* <span data-ttu-id="a2276-112">В чем их проблема?</span><span class="sxs-lookup"><span data-stu-id="a2276-112">What’s their problem?</span></span>
* <span data-ttu-id="a2276-113">Как ваше приложение может решить их проблему?</span><span class="sxs-lookup"><span data-stu-id="a2276-113">How can your app solve their problem?</span></span>
* <span data-ttu-id="a2276-114">Как часто будет использоваться ваше приложение?</span><span class="sxs-lookup"><span data-stu-id="a2276-114">How often will your app be used?</span></span>
* <span data-ttu-id="a2276-115">Сколько людей будет использовать ваше приложение?</span><span class="sxs-lookup"><span data-stu-id="a2276-115">How many people will use your app?</span></span>
* <span data-ttu-id="a2276-116">Какую доходность от инвестиций может предоставить ваше приложение?</span><span class="sxs-lookup"><span data-stu-id="a2276-116">What kind of return on investment can your app provide?</span></span>

<span data-ttu-id="a2276-117">Дополнительные сведения см. [в дополнительных](~/concepts/design/understand-use-cases.md) сведениях о случаях использования приложения, а также о случаях использования [Teams.](~/concepts/design/map-use-cases.md)</span><span class="sxs-lookup"><span data-stu-id="a2276-117">For more information, see [understand your app’s use cases](~/concepts/design/understand-use-cases.md) and [map use cases to Teams](~/concepts/design/map-use-cases.md).</span></span>

## <a name="get-teams-design-tools"></a><span data-ttu-id="a2276-118">Получить Teams средства разработки</span><span class="sxs-lookup"><span data-stu-id="a2276-118">Get Teams design tools</span></span>

<span data-ttu-id="a2276-119">Корпорация Майкрософт предоставляет средства, упрощая разработку Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="a2276-119">Microsoft provides tools to make it easier to design your Teams app.</span></span> <span data-ttu-id="a2276-120">По крайней мере, настоятельно рекомендуется использовать Microsoft Teams пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a2276-120">At minimum, we strongly recommend using the Microsoft Teams UI Kit.</span></span>

### <a name="get-the-microsoft-teams-ui-kit"></a><span data-ttu-id="a2276-121">Получите Microsoft Teams пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="a2276-121">Get the Microsoft Teams UI Kit</span></span>

<span data-ttu-id="a2276-122">Набор Microsoft Teams пользовательского интерфейса поможет вам разработать эффективное приложение Teams в кратчайшие сроки.</span><span class="sxs-lookup"><span data-stu-id="a2276-122">The Microsoft Teams UI Kit can help you develop an effective Teams app in the shortest amount of time.</span></span> <span data-ttu-id="a2276-123">Набор пользовательского интерфейса имеет все, что вы видите в этих документы, связанные с Teams разработкой приложения и многое другое, включая обширные примеры и варианты.</span><span class="sxs-lookup"><span data-stu-id="a2276-123">The UI kit has everything you see in these docs related to Teams app design and much more, including extensive examples and variations.</span></span>

<span data-ttu-id="a2276-124">В комплекте пользовательского интерфейса также есть предварительно построенные шаблоны и компоненты, которые можно скопировать и изменить по мере необходимости, поэтому можно тратить больше времени на разработку наилучшего пользовательского интерфейса, а не беспокоиться о том, как должна выглядеть кнопка.</span><span class="sxs-lookup"><span data-stu-id="a2276-124">The UI kit also has pre-built templates and components that you can copy and modify as needed, so you can spend more time designing the best user experience instead worrying about what a button should look like.</span></span>

> [!TIP]
> <span data-ttu-id="a2276-125">**Является ли набор пользовательского интерфейса для меня?**</span><span class="sxs-lookup"><span data-stu-id="a2276-125">**Is the UI kit for me?**</span></span> <span data-ttu-id="a2276-126">Если у вас есть какие-либо участие в создании Teams приложения, да.</span><span class="sxs-lookup"><span data-stu-id="a2276-126">If you have any part in creating a Teams app, yes.</span></span> <span data-ttu-id="a2276-127">Понимание того, как создать приложение Teams, полезно не только разработчикам, но и руководителям продуктов, разработчикам, использующим IDEs, и разработчикам, создателям с помощью инструментов с низким кодом (например, платформы Microsoft Power).</span><span class="sxs-lookup"><span data-stu-id="a2276-127">Understanding how to craft a Teams app is not only helpful to designers but product managers, developers using IDEs, and makers building with low-code tools (such as the Microsoft Power Platform).</span></span>

1. <span data-ttu-id="a2276-128">Перейдите на [страницу Microsoft Teams UI Kit Figma](https://www.figma.com/community/file/916836509871353159).</span><span class="sxs-lookup"><span data-stu-id="a2276-128">Go to the [Microsoft Teams UI Kit Figma page](https://www.figma.com/community/file/916836509871353159).</span></span>
1. <span data-ttu-id="a2276-129">Выберите **Дубликат,** чтобы открыть набор пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a2276-129">Select **Duplicate** to open the UI kit.</span></span> <span data-ttu-id="a2276-130">(Возможно, сначала необходимо создать учетную запись Figma.)</span><span class="sxs-lookup"><span data-stu-id="a2276-130">(You may have to first create a Figma account.)</span></span>

### <a name="try-the-sample-app"></a><span data-ttu-id="a2276-131">Попробуйте пример приложения</span><span class="sxs-lookup"><span data-stu-id="a2276-131">Try the sample app</span></span>

<span data-ttu-id="a2276-132">Вы можете загрузить пример приложения, чтобы узнать, как приложения должны выглядеть и вести себя в Teams клиенте.</span><span class="sxs-lookup"><span data-stu-id="a2276-132">You can upload a sample app to see how apps should look and behave in the Teams client.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a2276-133">Получить пример приложения (GitHub)</span><span class="sxs-lookup"><span data-stu-id="a2276-133">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="learn-teams-design-system"></a><span data-ttu-id="a2276-134">Узнайте Teams системы проектирования</span><span class="sxs-lookup"><span data-stu-id="a2276-134">Learn Teams design system</span></span>

<span data-ttu-id="a2276-135">Подробно ознакомьтесь с основами разработки Teams, в том числе [макетом,](design-teams-app-fundamentals.md)цветовой гаммой и другими.</span><span class="sxs-lookup"><span data-stu-id="a2276-135">Read in depth about or at least familiarize yourself with the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="choose-app-capabilities"></a><span data-ttu-id="a2276-136">Выбор возможностей приложения</span><span class="sxs-lookup"><span data-stu-id="a2276-136">Choose app capabilities</span></span>

<span data-ttu-id="a2276-137">После этапа планирования можно определить, Teams возможности соответствуют случаям использования приложения.</span><span class="sxs-lookup"><span data-stu-id="a2276-137">After the planning phase, you can determine which Teams capabilities fit your app’s use cases.</span></span> <span data-ttu-id="a2276-138">Например, если вы хотите упреждающий оповещать людей, бот может быть правильной возможностью.</span><span class="sxs-lookup"><span data-stu-id="a2276-138">For example, if you want to proactively notify people, a bot might be the right capability.</span></span>

<span data-ttu-id="a2276-139">Набор пользовательского интерфейса имеет предварительно построенные проекты, которые показывают, как обычно люди добавляют, устанавливают, используют и управляют каждой возможностью.</span><span class="sxs-lookup"><span data-stu-id="a2276-139">The UI kit has pre-built designs that show you how people typically add, set up, use, and manage each capability.</span></span> <span data-ttu-id="a2276-140">Эта информация также находится в этих документах, но с помощью набора пользовательского интерфейса можно скопировать и вклеить любой из этих проектов в дизайн приложения.</span><span class="sxs-lookup"><span data-stu-id="a2276-140">For quick reference, this information is also in these docs, but with the UI kit you can copy and paste any of these designs into your app’s design.</span></span>

1. <span data-ttu-id="a2276-141">В левом nav комплекта пользовательского интерфейса перейдите к возможностям **Приложения** и выберите нужные возможности для приложения.</span><span class="sxs-lookup"><span data-stu-id="a2276-141">In the UI kit’s left nav, go to **App capabilities** and select the capability you want for your app.</span></span>
1. <span data-ttu-id="a2276-142">Скопируйте то, что необходимо на этой странице для разработки приложения.</span><span class="sxs-lookup"><span data-stu-id="a2276-142">Copy what you need from that page to design your app.</span></span><br />
   <span data-ttu-id="a2276-143">Например, если приложение поддерживает проверку подлинности с помощью одного входного знака, скопируйте и вклейте проект для обработки этого точного сценария.</span><span class="sxs-lookup"><span data-stu-id="a2276-143">For example, if your app supports authentication with single sign-on, copy and paste the design for handling that exact scenario.</span></span>

## <a name="design-your-ux-flow"></a><span data-ttu-id="a2276-144">Разработка потока UX</span><span class="sxs-lookup"><span data-stu-id="a2276-144">Design your UX flow</span></span>

<span data-ttu-id="a2276-145">После разработки базового приложения вы можете изменять и уточнять его столько, сколько хотите (и быстро), копируя Teams шаблоны пользовательского интерфейса и основные компоненты из набора пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a2276-145">Once you have a basic app design, you can modify and refine it as much as you want (and quickly) by copying Teams UI templates and basic components from the UI kit.</span></span>

### <a name="design-with-ui-templates"></a><span data-ttu-id="a2276-146">Проектирование с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="a2276-146">Design with UI templates</span></span>

<span data-ttu-id="a2276-147">Шаблоны пользовательского интерфейса — это сложные и высококачественные проекты для общих Teams и рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="a2276-147">UI templates are complex, high-fidelity designs for common Teams use cases and workflows.</span></span> <span data-ttu-id="a2276-148">Вместо того чтобы начинать снизу вверх с базовыми компонентами, рекомендуется использовать эти шаблоны для упрощения и ускорения процесса разработки.</span><span class="sxs-lookup"><span data-stu-id="a2276-148">Instead of starting from the bottom up with basic components, we recommend you use these templates to simplify and speed up the design process.</span></span>

1. <span data-ttu-id="a2276-149">В левом nav набора пользовательского интерфейса перейдите к **шаблонам пользовательского интерфейса.**</span><span class="sxs-lookup"><span data-stu-id="a2276-149">In the UI kit’s left nav, go to **UI templates**.</span></span>
1. <span data-ttu-id="a2276-150">Скопируйте шаблоны, которые могут быть доступны для разработки приложения.</span><span class="sxs-lookup"><span data-stu-id="a2276-150">Copy templates that make sense for your app design.</span></span><br />
   <span data-ttu-id="a2276-151">Например, при разработке личного приложения может потребоваться использовать шаблон Панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a2276-151">For example, if you’re designing a personal app, you may want to use a Dashboard template.</span></span>

### <a name="design-with-basic-ui-components"></a><span data-ttu-id="a2276-152">Разработка с базовыми компонентами пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="a2276-152">Design with basic UI components</span></span>

<span data-ttu-id="a2276-153">На основе пользовательского интерфейса Fluent это основные элементы для создания знакомых Teams интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="a2276-153">Based on Fluent UI, these are the core elements for creating familiar Teams interfaces.</span></span> <span data-ttu-id="a2276-154">Используйте эти компоненты, если в шаблоне пользовательского интерфейса отсутствует что-то необходимое или вы просто хотите создать приложение с нуля.</span><span class="sxs-lookup"><span data-stu-id="a2276-154">Use these components if a UI template is missing something you need or you just want to design your app from scratch.</span></span>

1. <span data-ttu-id="a2276-155">В левом nav набора пользовательского интерфейса перейдите к **компонентам базового пользовательского интерфейса.**</span><span class="sxs-lookup"><span data-stu-id="a2276-155">In the UI kit’s left nav, go to **Basic UI components**.</span></span>
1. <span data-ttu-id="a2276-156">Скопируйте компоненты, необходимые для разработки приложения (например, кнопку или перегной).</span><span class="sxs-lookup"><span data-stu-id="a2276-156">Copy the components you need for your app design (for example, a button or toggle).</span></span>

## <a name="implement-your-design"></a><span data-ttu-id="a2276-157">Реализация дизайна</span><span class="sxs-lookup"><span data-stu-id="a2276-157">Implement your design</span></span>

<span data-ttu-id="a2276-158">Проектирование готово, и вы готовы приступить к построению.</span><span class="sxs-lookup"><span data-stu-id="a2276-158">The design is done and you’re ready to start building.</span></span> <span data-ttu-id="a2276-159">Следующие средства помогут упростить разработку приложения на переднем конце.</span><span class="sxs-lookup"><span data-stu-id="a2276-159">The following tools can help simplify the front-end development of your app.</span></span>

### <a name="build-with-ui-templates"></a><span data-ttu-id="a2276-160">Сборка с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="a2276-160">Build with UI templates</span></span>

<span data-ttu-id="a2276-161">Если вы использовали шаблоны пользовательского интерфейса в своей разработке, эти шаблоны можно реализовать в библиотеке пользовательского интерфейса Microsoft Teams (библиотека компонентов React на основе пользовательского интерфейса Fluent).</span><span class="sxs-lookup"><span data-stu-id="a2276-161">If you used UI templates in your design, you can implement these templates with the Microsoft Teams UI Library (a React component library based on Fluent UI).</span></span>

<span data-ttu-id="a2276-162">В настоящее время не все шаблоны, перечисленные в наборе пользовательского интерфейса, доступны в библиотеке.</span><span class="sxs-lookup"><span data-stu-id="a2276-162">Currently, not all templates listed in the UI kit are available in the library.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a2276-163">Получить библиотеку (GitHub)</span><span class="sxs-lookup"><span data-stu-id="a2276-163">Get the library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="build-with-basic-ui-components"></a><span data-ttu-id="a2276-164">Сборка с базовыми компонентами пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="a2276-164">Build with basic UI components</span></span>

<span data-ttu-id="a2276-165">Не в отличие от этапа разработки, эти компоненты пользовательского интерфейса Fluent можно использовать в проекте приложения, если шаблон пользовательского интерфейса не хватает необходимого или вы просто хотите создать приложение с нуля.</span><span class="sxs-lookup"><span data-stu-id="a2276-165">Not unlike the design phase, you can use these Fluent UI components in your app project if a UI template is missing something you need, or you just want to build the app from scratch.</span></span> 

<span data-ttu-id="a2276-166">(Примечание. Если вы заметили что-то пропавшее или у вас есть идея для шаблона, рассмотрите возможность внести вклад в репо Teams библиотеки пользовательского интерфейса.)</span><span class="sxs-lookup"><span data-stu-id="a2276-166">(Note: If you notice something missing or have an idea for a template, consider contributing to the Teams UI Library repo.)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a2276-167">Get the library (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="a2276-167">Get the library (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

## <a name="review-design-resources"></a><span data-ttu-id="a2276-168">Просмотр ресурсов разработки</span><span class="sxs-lookup"><span data-stu-id="a2276-168">Review design resources</span></span>

<span data-ttu-id="a2276-169">Если вы только начинаете работать с приложением или рядом с готовым к производству приложением, рекомендуем периодически пересматривать следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="a2276-169">Whether you’re just starting on your app or close to a production-ready app, we recommend that you periodically review the following resources:</span></span>

* <span data-ttu-id="a2276-170">**Microsoft Teams** хранения: предоставляет стандарты, к которые должны стремиться все Teams приложения (а не только приложения, перечисленные в магазине).</span><span class="sxs-lookup"><span data-stu-id="a2276-170">**Microsoft Teams store validation guidelines**: Provides standards that all Teams apps should strive for (not just apps listed in the store).</span></span> <span data-ttu-id="a2276-171">Дополнительные сведения см. в [инструкциях.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)</span><span class="sxs-lookup"><span data-stu-id="a2276-171">For more information, see the [guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).</span></span>
* <span data-ttu-id="a2276-172">**Разработка лучших практик.** Эти документы и набор пользовательского интерфейса предоставляют лучшие практики для разработки высококачественных приложений.</span><span class="sxs-lookup"><span data-stu-id="a2276-172">**Design best practices**: These docs and the UI kit provide best practices for designing high-quality apps.</span></span> <span data-ttu-id="a2276-173">Например, см. лучшие [практики разработки ботов.](~/bots/design/bots.md#best-practices)</span><span class="sxs-lookup"><span data-stu-id="a2276-173">For example, see the [best practices for designing bots](~/bots/design/bots.md#best-practices).</span></span>
