---
title: Справочные материалы по проектированию
description: Описывает рекомендации по использованию полей и всплывающих подменю в приложениях
keywords: рекомендации по проектированию Teams ссылаются на поля и всплывающие элементы
ms.openlocfilehash: 0f62d38bf961ae79b05c599638cefb3c76f46ed4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675597"
---
# <a name="fields-and-flyouts"></a><span data-ttu-id="b2ddc-104">Поля и всплывающие окна</span><span class="sxs-lookup"><span data-stu-id="b2ddc-104">Fields and flyouts</span></span>

---

## <a name="fields"></a><span data-ttu-id="b2ddc-105">Fields</span><span class="sxs-lookup"><span data-stu-id="b2ddc-105">Fields</span></span>

<span data-ttu-id="b2ddc-106">Поля — это области, в которых пользователи могут вводить текст.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-106">Fields are areas where users can input text.</span></span>

### <a name="padding-and-size"></a><span data-ttu-id="b2ddc-107">Заполнение и размер</span><span class="sxs-lookup"><span data-stu-id="b2ddc-107">Padding and size</span></span>

<span data-ttu-id="b2ddc-108">Однострочные текстовые поля — это фиксированная высота интервалами по 32, соответствующая высоте других компонентов.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-108">Single-line text fields are a fixed height of 32px to match the height of other components.</span></span> <span data-ttu-id="b2ddc-109">Некоторые текстовые поля, такие как поля описания, могут быть вертикально вертикально, что позволяет увеличить количество текста.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-109">Some text fields such as description fields may be taller vertically to allow more text.</span></span>
[!include[Padding and size](~/includes/design/fields-image-padding.html)]

### <a name="states"></a><span data-ttu-id="b2ddc-110">Состояния</span><span class="sxs-lookup"><span data-stu-id="b2ddc-110">States</span></span>

<span data-ttu-id="b2ddc-111">Ниже приведены состояния наших текстовых полей.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-111">These are the states of our text fields.</span></span> <span data-ttu-id="b2ddc-112">Текстовые поля существуют в разных состояниях.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-112">Text fields exist in different states.</span></span> <span data-ttu-id="b2ddc-113">У нас есть определенные макеты, предназначенные для девяти возможных сценариев, включая (сверху вниз): размещает текстовое поле, клавиатуру в фокусе и курсоре внутри поля, клавиатуры в фокусе с введенным текстом, обработка ошибок завершена, ошибка обработки, очистка текста поле (включая значок X), поле поиска (включая значок поиска), загрузку поля и отключенное поле.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-113">We have specific designs dedicated to nine possible scenarios, including (top to bottom): Resting text field, Keyboard in focus and cursor inside the field, Keyboard in focus with text entered, Error handling has succeeded, Error handling has failed, Clear text field (including an X icon), Search field (including a Search icon), Loading field, and a Disabled field.</span></span>
[!include[Field states](~/includes/design/fields-image-states.html)]

### <a name="formatting-help-text-and-labels"></a><span data-ttu-id="b2ddc-114">Форматирование текста справки и меток</span><span class="sxs-lookup"><span data-stu-id="b2ddc-114">Formatting help text and labels</span></span>

<span data-ttu-id="b2ddc-115">Поля могут содержать замещающий текст, чтобы получить пример требуемого типа информации.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-115">Fields can contain placeholder text to give an example of the kind of information that is required.</span></span> <span data-ttu-id="b2ddc-116">Кроме того, они могут содержать метки, которые предоставляют пользователю дополнительные контексты.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-116">They can also hold labels that give the user more context.</span></span> <span data-ttu-id="b2ddc-117">В поле текст всегда должен быть выровнен по левому краю.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-117">Within a field, your text should always be justified left.</span></span> <span data-ttu-id="b2ddc-118">Кроме того, мы используем прописные и строчные буквы.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-118">We use sentence casing throughout here, as well.</span></span>

<span data-ttu-id="b2ddc-119">Мы используем регулярный пользовательский интерфейс в 12 пт (заголовок) и $app-серый-02 для меток.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-119">We use Segoe UI Regular at 12 pt (caption) and $app-gray-02 for labels.</span></span> <span data-ttu-id="b2ddc-120">Чтобы получить текст справки, мы используем пользовательский интерфейс Segoe с частотой 14 пт (базовый) и $app-серый-02.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-120">For help text, we use Segoe UI Regular at 14 pt (base) and $app-gray-02.</span></span>
[!include[Fields typography](~/includes/design/fields-image-typography.html)]

---

## <a name="flyouts"></a><span data-ttu-id="b2ddc-121">Всплывающие окна</span><span class="sxs-lookup"><span data-stu-id="b2ddc-121">Flyouts</span></span>

<span data-ttu-id="b2ddc-122">Всплывающие окна являются более легковесными, чем диалоговые окна, и их можно быстро закрыть.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-122">Flyouts are more lightweight than dialogs and can be dismissed quickly.</span></span> <span data-ttu-id="b2ddc-123">Они могут содержать кнопки, поля и другие компоненты.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-123">They can contain buttons, fields, and other components.</span></span>
[!include[Flyouts](~/includes/design/flyouts-image.html)]

### <a name="sizing-and-padding"></a><span data-ttu-id="b2ddc-124">Размер и заполнение</span><span class="sxs-lookup"><span data-stu-id="b2ddc-124">Sizing and padding</span></span>

<span data-ttu-id="b2ddc-125">Рекомендуется использовать заполнение 16px слева и справа от содержимого.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-125">We recommend a 16px padding to the left and right of the content.</span></span>
[!include[Flyouts size and padding](~/includes/design/flyouts-image-sizepadding.html)]

### <a name="placement"></a><span data-ttu-id="b2ddc-126">Размещение</span><span class="sxs-lookup"><span data-stu-id="b2ddc-126">Placement</span></span>

<span data-ttu-id="b2ddc-127">Всплывающие окна являются контекстными, и их следует поместить над элементом, вызвавшим его, под ним или рядом с ним.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-127">Flyouts are contextual and should be placed above, below, or beside the element that triggered it.</span></span>

### <a name="scrolling"></a><span data-ttu-id="b2ddc-128">Прокрутки</span><span class="sxs-lookup"><span data-stu-id="b2ddc-128">Scrolling</span></span>

<span data-ttu-id="b2ddc-129">Верхний колонтитул остается на месте, чтобы предоставить контекст для прокручиваемого контента.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-129">The header remains in place to give context to the content being scrolled.</span></span>
[!include[Flyouts scrolling](~/includes/design/flyouts-image-scrolling.html)]

## <a name="mobile"></a><span data-ttu-id="b2ddc-130">Mobile</span><span class="sxs-lookup"><span data-stu-id="b2ddc-130">Mobile</span></span>

<span data-ttu-id="b2ddc-131">Поля — это поля ввода текста, которые принимают ввод от пользователей.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-131">Fields are text-entry boxes that accept input from users.</span></span> <span data-ttu-id="b2ddc-132">Всплывающие меню — это горизонтальные всплывающие окна, отображаемые в верхней области и которые можно использовать для отображения более подробных сведений об элементе.</span><span class="sxs-lookup"><span data-stu-id="b2ddc-132">Flyout menus are horizontal pop-up windows that appear from the top pane and can be used to show more detail about an item.</span></span>

### <a name="field-controls"></a><span data-ttu-id="b2ddc-133">Элементы управления поля</span><span class="sxs-lookup"><span data-stu-id="b2ddc-133">Field Controls</span></span>

[!include[Mobile fields](~/includes/design/fields-mobile-image.html)]

### <a name="flyout-menu-list-controls"></a><span data-ttu-id="b2ddc-134">Элементы управления списком всплывающих меню</span><span class="sxs-lookup"><span data-stu-id="b2ddc-134">Flyout menu list controls</span></span>

[!include[Mobile flyout menu controls](~/includes/design/flyout-menu-mobile-image.html)]
