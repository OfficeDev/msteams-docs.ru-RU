---
title: Справочные материалы по проектированию
description: Описывает рекомендации по использованию цвета в приложениях
keywords: рекомендации по проектированию Teams на цвете компонентов
ms.openlocfilehash: c6c0a421abbfc23959c7873d95aa89ca7cc685f2
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675276"
---
# <a name="color"></a><span data-ttu-id="ee359-104">Цвет</span><span class="sxs-lookup"><span data-stu-id="ee359-104">Color</span></span>

<span data-ttu-id="ee359-105">Использование нашей утвержденной нейтральной палитры для фоновых рисунков, уведомлений, текста и кнопок поможет вам в работе над приложением в Teams.</span><span class="sxs-lookup"><span data-stu-id="ee359-105">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="ee359-106">Так как в Teams есть две цветные темы (светло-и темная), рекомендуется убедиться, что ваше приложение отлично выглядит в обеих темах.</span><span class="sxs-lookup"><span data-stu-id="ee359-106">Since Teams has two color themes (light and dark), it’s a good idea to make sure your app looks great in both themes.</span></span>

### <a name="app-black-252423"></a><span data-ttu-id="ee359-107">$app-Black (#252423)</span><span class="sxs-lookup"><span data-stu-id="ee359-107">$app-black (#252423)</span></span>

<span data-ttu-id="ee359-108">Мы наиболее часто используем цвет текста.</span><span class="sxs-lookup"><span data-stu-id="ee359-108">Our most commonly-used text color.</span></span> <span data-ttu-id="ee359-109">Мы используем его на пяти уровнях непрозрачности для текста.</span><span class="sxs-lookup"><span data-stu-id="ee359-109">We use it at five levels of opacity for text.</span></span> <span data-ttu-id="ee359-110">Текст в основном должен использоваться на уровне 100%, 74%, 64%, так как он доступен.</span><span class="sxs-lookup"><span data-stu-id="ee359-110">Text should mainly be used at 100%, 74%, 64% opacity since it is accessible.</span></span> <span data-ttu-id="ee359-111">Текст на 52% и 36% следует использовать экономно, так как он недоступен.</span><span class="sxs-lookup"><span data-stu-id="ee359-111">Text at 52% and 36% should be used sparingly since it is not accessible.</span></span>

[!include[Appblack color and text](~/includes/design/color-image-appblack-text.html)]

1. <span data-ttu-id="ee359-112">100% — заголовки и базовый текст</span><span class="sxs-lookup"><span data-stu-id="ee359-112">100% - Headers and base text</span></span>
2. <span data-ttu-id="ee359-113">74% — метки, подзаголовки, атрибуты и кнопки значков</span><span class="sxs-lookup"><span data-stu-id="ee359-113">74% - Labels, subheads, attributions, and icon buttons</span></span>
3. <span data-ttu-id="ee359-114">64%-просмотров сообщений, текст справки (не отображается)</span><span class="sxs-lookup"><span data-stu-id="ee359-114">64% - Message previews, help text (not shown)</span></span>
4. <span data-ttu-id="ee359-115">52% (метки времени)</span><span class="sxs-lookup"><span data-stu-id="ee359-115">52% - Timestamps</span></span>
5. <span data-ttu-id="ee359-116">36% — отключенный текст</span><span class="sxs-lookup"><span data-stu-id="ee359-116">36% - Disabled text</span></span>

<span data-ttu-id="ee359-117">Кроме того, `$app-black` для некоторых элементов пользовательского интерфейса используются другие опаЦитиес:</span><span class="sxs-lookup"><span data-stu-id="ee359-117">We also use `$app-black` at other opacities for some UI elements:</span></span>

[!include[Appblack color and text](~/includes/design/color-image-appblack-ui.html)]

1. <span data-ttu-id="ee359-118">14% фона баннера</span><span class="sxs-lookup"><span data-stu-id="ee359-118">14% - Banner backgrounds</span></span>
2. <span data-ttu-id="ee359-119">5% — отключена кнопка и границы карточек</span><span class="sxs-lookup"><span data-stu-id="ee359-119">5% - Disabled button and card borders</span></span>

### <a name="default-theme-color-ramp"></a><span data-ttu-id="ee359-120">Цветовая шкала темы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ee359-120">Default theme color ramp</span></span>

<span data-ttu-id="ee359-121">Ознакомьтесь с разделом "перо по [разработке Microsoft Teams" — Цветовая шкала темы по умолчанию](https://codepen.io/msteams/pen/KyPmqL/) на кодепен.</span><span class="sxs-lookup"><span data-stu-id="ee359-121">See the Pen [Microsoft Teams design guidelines - default theme color ramp](https://codepen.io/msteams/pen/KyPmqL/) on CodePen.</span></span>

<iframe height='620' scrolling='no' title='<span data-ttu-id="ee359-122">Рекомендации по проектированию Microsoft Teams — цветовая шкала темы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ee359-122">Microsoft Teams design guidelines - default theme color ramp</span></span>' src='//codepen.io/msteams/embed/KyPmqL/?height=682&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="ee359-123">Ознакомьтесь с разделом "перо по <a href='https://codepen.io/msteams/pen/KyPmqL/'>разработке Microsoft Teams" — Цветовая шкала по умолчанию</a> Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) на <a href='https://codepen.io'>кодепен</a>.</span><span class="sxs-lookup"><span data-stu-id="ee359-123">See the Pen <a href='https://codepen.io/msteams/pen/KyPmqL/'>Microsoft Teams design guidelines - default theme color ramp</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

### <a name="other-default-theme-colors"></a><span data-ttu-id="ee359-124">Другие цвета темы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ee359-124">Other default theme colors</span></span>

<span data-ttu-id="ee359-125">Ознакомьтесь с разделом "перо по [проектированию Microsoft Teams" — другие цвета темы по умолчанию](https://codepen.io/msteams/pen/zPOdYJ/) на кодепен.</span><span class="sxs-lookup"><span data-stu-id="ee359-125">See the Pen [Microsoft Teams design guidelines - other default theme colors](https://codepen.io/msteams/pen/zPOdYJ/) on CodePen.</span></span>

<iframe height='392' scrolling='no' title='<span data-ttu-id="ee359-126">Рекомендации по проектированию Microsoft Teams — другие цвета темы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ee359-126">Microsoft Teams design guidelines - other default theme colors</span></span>' src='//codepen.io/msteams/embed/zPOdYJ/?height=442&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="ee359-127">Ознакомьтесь с разделом "перо по <a href='https://codepen.io/msteams/pen/zPOdYJ/'>проектированию Microsoft Teams" — другие цвета темы по умолчанию</a> в Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) на <a href='https://codepen.io'>кодепен</a>.</span><span class="sxs-lookup"><span data-stu-id="ee359-127">See the Pen <a href='https://codepen.io/msteams/pen/zPOdYJ/'>Microsoft Teams design guidelines - other default theme colors</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

### <a name="dark-theme-color-ramp"></a><span data-ttu-id="ee359-128">Темная цветовая шкала темы</span><span class="sxs-lookup"><span data-stu-id="ee359-128">Dark theme color ramp</span></span>

<span data-ttu-id="ee359-129">Ознакомьтесь с разделом "перо [по проектированию Microsoft Teams — Темная цветовая шкала темы](https://codepen.io/msteams/pen/BmBwjx/) на кодепен".</span><span class="sxs-lookup"><span data-stu-id="ee359-129">See the Pen [Microsoft Teams design guidelines - dark theme color ramp](https://codepen.io/msteams/pen/BmBwjx/) on CodePen.</span></span>

<iframe height='798' scrolling='no' title='<span data-ttu-id="ee359-130">Рекомендации по проектированию Microsoft Teams — Темная цветовая шкала темы</span><span class="sxs-lookup"><span data-stu-id="ee359-130">Microsoft Teams design guidelines - dark theme color ramp</span></span>' src='//codepen.io/msteams/embed/BmBwjx/?height=846&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="ee359-131">Ознакомьтесь с разделом "перо <a href='https://codepen.io/msteams/pen/BmBwjx/'>по проектированию Microsoft Teams — Темная цветовая шкала</a> " Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) на <a href='https://codepen.io'>кодепен</a>.</span><span class="sxs-lookup"><span data-stu-id="ee359-131">See the Pen <a href='https://codepen.io/msteams/pen/BmBwjx/'>Microsoft Teams design guidelines - dark theme color ramp</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

### <a name="other-dark-theme-colors"></a><span data-ttu-id="ee359-132">Другие темные цвета темы</span><span class="sxs-lookup"><span data-stu-id="ee359-132">Other dark theme colors</span></span>

<span data-ttu-id="ee359-133">Ознакомьтесь с разделом "перо [по проектированию Microsoft Teams" — другие темные цвета темы](https://codepen.io/msteams/pen/zPOEXN/) в кодепен.</span><span class="sxs-lookup"><span data-stu-id="ee359-133">See the Pen [Microsoft Teams design guidelines - other dark theme colors](https://codepen.io/msteams/pen/zPOEXN/) on CodePen.</span></span>

<iframe height='390' scrolling='no' title='<span data-ttu-id="ee359-134">Рекомендации по проектированию Microsoft Teams — другие темные цвета темы</span><span class="sxs-lookup"><span data-stu-id="ee359-134">Microsoft Teams design guidelines - other dark theme colors</span></span>' src='//codepen.io/msteams/embed/zPOEXN/?height=442&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="ee359-135">Ознакомьтесь с разделом "перо по <a href='https://codepen.io/msteams/pen/zPOEXN/'>проектированию Microsoft Teams" — другие темные цвета темы</a> Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) на <a href='https://codepen.io'>кодепен</a>.</span><span class="sxs-lookup"><span data-stu-id="ee359-135">See the Pen <a href='https://codepen.io/msteams/pen/zPOEXN/'>Microsoft Teams design guidelines - other dark theme colors</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>