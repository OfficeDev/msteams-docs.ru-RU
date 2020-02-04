---
title: Справочные материалы по проектированию
description: Описывает рекомендации по использованию диалоговых окон в приложениях
keywords: рекомендации по проектированию Teams Справочник по компонентам
ms.openlocfilehash: d244eedde66085d41b1f356176a7775de304aaf4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675245"
---
# <a name="dialogs"></a><span data-ttu-id="1a73e-104">Диалоги</span><span class="sxs-lookup"><span data-stu-id="1a73e-104">Dialogs</span></span>

<span data-ttu-id="1a73e-105">Диалоговые окна следует использовать экономно, так как они могут нарушить работу, и у пользователя должен быть очевидный способ выхода.</span><span class="sxs-lookup"><span data-stu-id="1a73e-105">Dialogs should be used sparingly since they can be disruptive, and should have a clear way for the user to exit.</span></span>

---

## <a name="sizes"></a><span data-ttu-id="1a73e-106">Масштаба</span><span class="sxs-lookup"><span data-stu-id="1a73e-106">Sizes</span></span>

<span data-ttu-id="1a73e-107">У нас есть 3 варианта размеров диалоговых окон.</span><span class="sxs-lookup"><span data-stu-id="1a73e-107">We have 3 dialog sizes to choose from.</span></span> <span data-ttu-id="1a73e-108">Выберите размер, который подходит для имеющегося содержимого.</span><span class="sxs-lookup"><span data-stu-id="1a73e-108">Choose the size that is appropriate for the content you have.</span></span>
[!include[Dialog sizes](~/includes/design/dialogs-image-sizes.html)]

---

## <a name="buttons"></a><span data-ttu-id="1a73e-109">Кнопки</span><span class="sxs-lookup"><span data-stu-id="1a73e-109">Buttons</span></span>

<span data-ttu-id="1a73e-110">Кнопки выравниваются по правому краю.</span><span class="sxs-lookup"><span data-stu-id="1a73e-110">Buttons are right-justified.</span></span>
<span data-ttu-id="1a73e-111">Все остальные элементы (флажки, текст справки и т. д.) должны быть выровнены по левому краю.</span><span class="sxs-lookup"><span data-stu-id="1a73e-111">All other elements (checkboxes, help text, etc.) should be left-justified.</span></span>
<span data-ttu-id="1a73e-112">Не повторяйте отрицательные действия (никогда не предоставляйте кнопку ' X ' и ' Cancel ' одновременно).</span><span class="sxs-lookup"><span data-stu-id="1a73e-112">Don’t duplicate negative actions (Never provide an ‘X’ and a ‘Cancel’ button at the same time.).</span></span>
<span data-ttu-id="1a73e-113">Кнопки "Применить" должны быть связаны с кнопками "Отмена".</span><span class="sxs-lookup"><span data-stu-id="1a73e-113">‘Apply’ buttons should be paired with ‘Cancel’ buttons.</span></span>
[!include[Dialog buttons](~/includes/design/dialogs-image-buttons.html)]

---

## <a name="scrolling"></a><span data-ttu-id="1a73e-114">Прокрутки</span><span class="sxs-lookup"><span data-stu-id="1a73e-114">Scrolling</span></span>

<span data-ttu-id="1a73e-115">В некоторых случаях содержимое будет прокручено.</span><span class="sxs-lookup"><span data-stu-id="1a73e-115">In some cases, content will scroll.</span></span> <span data-ttu-id="1a73e-116">Заголовок диалогового окна и другие важные сведения остаются на месте.</span><span class="sxs-lookup"><span data-stu-id="1a73e-116">The dialog title and other important information remains in place.</span></span>
[!include[Dialog scrolling](~/includes/design/dialogs-image-scrolling.html)]

---

## <a name="padding"></a><span data-ttu-id="1a73e-117">Внутренние поля</span><span class="sxs-lookup"><span data-stu-id="1a73e-117">Padding</span></span>

<span data-ttu-id="1a73e-118">Заполнение всеми четырьмя сторонами диалогового окна должно быть интервалами по 32.</span><span class="sxs-lookup"><span data-stu-id="1a73e-118">The padding around all four sides of the dialog should be 32px.</span></span>
[!include[Dialog padding](~/includes/design/dialogs-image-padding.html)]

---

## <a name="typography"></a><span data-ttu-id="1a73e-119">Шрифтовое оформление</span><span class="sxs-lookup"><span data-stu-id="1a73e-119">Typography</span></span>

<span data-ttu-id="1a73e-120">Мы используем Семиболд UI в 18pt (title2) и $app-Black для заголовков диалоговых окон.</span><span class="sxs-lookup"><span data-stu-id="1a73e-120">We use Segoe UI SemiBold at 18pt (title2) and $app-black for dialog titles.</span></span> <span data-ttu-id="1a73e-121">Для основного текста мы используем регулярный пользовательский интерфейс в 14pt (Base) и $app-Black.</span><span class="sxs-lookup"><span data-stu-id="1a73e-121">For body text, we use Segoe UI Regular at 14pt (base) and $app-black.</span></span>
[!include[Dialog typography](~/includes/design/dialogs-image-typography.html)]