---
title: Удаление полей вкладок в Microsoft Teams
author: laujan
description: Описывает, как удаление полей вкладок повысит качество работы разработчика.
keywords: удаление полей вкладки
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: 87766a40730fdaa2da80c2e0031eab655a993c33
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479963"
---
# <a name="tab-margin-changes"></a><span data-ttu-id="efc5e-104">Изменения полей вкладок</span><span class="sxs-lookup"><span data-stu-id="efc5e-104">Tab margin changes</span></span>

<span data-ttu-id="efc5e-105">В этом документе описывается, как удаление полей вокруг всех вкладок в Microsoft Teams повысит возможности разработчика при создании приложений.</span><span class="sxs-lookup"><span data-stu-id="efc5e-105">This document describes how the removal of margins around all tabs in Microsoft Teams will enhance the developer's experience when building apps.</span></span> <span data-ttu-id="efc5e-106">Это усовершенствование, введено в Microsoft Teams в 2021 году.</span><span class="sxs-lookup"><span data-stu-id="efc5e-106">This is an enhancement introduced in Microsoft Teams in 2021.</span></span>
<span data-ttu-id="efc5e-107">Удаление полей вокруг всех вкладок позволит разработчикам создавать приложения, которые выглядят более родными для Teams.</span><span class="sxs-lookup"><span data-stu-id="efc5e-107">Removing the margins around all tabs will allow developers to build apps that look more native to Teams.</span></span> <span data-ttu-id="efc5e-108">Это также согласуется с нашими [проектами комплекта пользовательского интерфейса.](~/tabs/design/tabs.md)</span><span class="sxs-lookup"><span data-stu-id="efc5e-108">This will also align with our [UI kit designs](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="efc5e-109">Большинство приложений уже выглядят лучше без полей, окружающих их опытом.</span><span class="sxs-lookup"><span data-stu-id="efc5e-109">Most apps already look better without the margins surrounding their experiences.</span></span> <span data-ttu-id="efc5e-110">Однако некоторые вкладки визуально влияют на это изменение, и разработчики должны внести необходимые изменения.</span><span class="sxs-lookup"><span data-stu-id="efc5e-110">However, some tabs are visually affected by this change, and developers must make the necessary changes.</span></span>

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Вкладка остроумие и без маржи" border="false":::

## <a name="timelines"></a><span data-ttu-id="efc5e-112">Сроки</span><span class="sxs-lookup"><span data-stu-id="efc5e-112">Timelines</span></span>

* <span data-ttu-id="efc5e-113">5 марта 2021 г. — Поля, удалены в [общедоступных](~/resources/dev-preview/developer-preview-intro.md)Developer Preview .</span><span class="sxs-lookup"><span data-stu-id="efc5e-113">March 5, 2021 - Margins removed in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
* <span data-ttu-id="efc5e-114">1 мая 2021 г. Поля будут удалены в производстве.</span><span class="sxs-lookup"><span data-stu-id="efc5e-114">May 1, 2021 - Margins will be removed in production.</span></span>

## <a name="guidelines"></a><span data-ttu-id="efc5e-115">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="efc5e-115">Guidelines</span></span>

<span data-ttu-id="efc5e-116">Это изменение влияет на приложения Microsoft Teams, которые используют вкладки.</span><span class="sxs-lookup"><span data-stu-id="efc5e-116">Microsoft Teams apps that use tabs will be affected by this change.</span></span> <span data-ttu-id="efc5e-117">Разработчикам следует перейти на общедоступные [Developer Preview,](~/resources/dev-preview/developer-preview-intro.md) чтобы определить, как влияют их вкладки и внести необходимые изменения.</span><span class="sxs-lookup"><span data-stu-id="efc5e-117">Developers should switch to [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) in order to determine how their tabs are affected and make the necessary changes.</span></span>

<span data-ttu-id="efc5e-118">Разработчики вкладок не должны полагаться на Teams, чтобы предоставлять поля, окружающие их вкладки.</span><span class="sxs-lookup"><span data-stu-id="efc5e-118">Tab developers must not rely on Teams to provide margins surrounding their tabs.</span></span> <span data-ttu-id="efc5e-119">Разработчикам рекомендуется добавлять поля вокруг их проектов вкладок там, где это необходимо.</span><span class="sxs-lookup"><span data-stu-id="efc5e-119">Developers are encouraged to add margins around their tab designs where it is required.</span></span> <span data-ttu-id="efc5e-120">Проекты приложений в производстве могут выглядеть так, что существует дополнительная обивка, то есть поля, предоставляемые Teams, и поля, предоставляемые вкладкой. Однако дополнительная обивка является временной и пройдет через несколько недель, оставив только предоставленную обивку приложения.</span><span class="sxs-lookup"><span data-stu-id="efc5e-120">App designs in production can look like there is extra padding, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and will go away in a few weeks, leaving only the app's provided padding.</span></span>

## <a name="faq"></a><span data-ttu-id="efc5e-121">Вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="efc5e-121">FAQ</span></span>

<span data-ttu-id="efc5e-122">**Можно ли для хрома приложения, например панели заголовки или панели задач, прикасаться к краям наших проектов?**</span><span class="sxs-lookup"><span data-stu-id="efc5e-122">**Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?**</span></span>

<span data-ttu-id="efc5e-123">Да, это нормально и поощряется.</span><span class="sxs-lookup"><span data-stu-id="efc5e-123">Yes, this is fine and encouraged.</span></span> <span data-ttu-id="efc5e-124">Это помогает приложению чувствовать себя родным.</span><span class="sxs-lookup"><span data-stu-id="efc5e-124">This helps the app feel native.</span></span>

<span data-ttu-id="efc5e-125">**Нормально ли для контента приложения, например текста, логотипов и изображений, прикасаться к левым и правым краям наших проектов?**</span><span class="sxs-lookup"><span data-stu-id="efc5e-125">**Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?**</span></span>

<span data-ttu-id="efc5e-126">Нет, необходимо предоставить собственную обивку или поля слева и справа от всего контента приложения, чтобы он не касался краев пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="efc5e-126">No, you must provide your own padding or margins to the left and right of all app content to ensure it does not touch the edges of your UI.</span></span> <span data-ttu-id="efc5e-127">При необходимости можно также добавить поля в верхней части вкладки.</span><span class="sxs-lookup"><span data-stu-id="efc5e-127">You can also add margins at the top of your tab, if required.</span></span>

<span data-ttu-id="efc5e-128">**Каков размер ранее примененных команд полей?**</span><span class="sxs-lookup"><span data-stu-id="efc5e-128">**What's the size of the margins Teams previously applied?**</span></span>

* <span data-ttu-id="efc5e-129">Слева и справа: 20px</span><span class="sxs-lookup"><span data-stu-id="efc5e-129">Left and right: 20px</span></span>
* <span data-ttu-id="efc5e-130">Топ: 16px</span><span class="sxs-lookup"><span data-stu-id="efc5e-130">Top: 16px</span></span>
* <span data-ttu-id="efc5e-131">Нижний: 0px</span><span class="sxs-lookup"><span data-stu-id="efc5e-131">Bottom: 0px</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="efc5e-132">Все вкладки имеют свои поля удалены: личные вкладки, (групповые) вкладки чата, вкладки собраний и вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="efc5e-132">All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.</span></span>
> * <span data-ttu-id="efc5e-133">Нет способа отказаться от этого изменения или отказаться от этого изменения.</span><span class="sxs-lookup"><span data-stu-id="efc5e-133">There is no way to opt-in or opt-out of this change.</span></span> <span data-ttu-id="efc5e-134">Он будет применяться для всех вкладок.</span><span class="sxs-lookup"><span data-stu-id="efc5e-134">It will apply to all tabs.</span></span>
> * <span data-ttu-id="efc5e-135">Это изменение может повлиять на вкладки, которые полагаются на Microsoft Teams, чтобы предоставить поля, окружающие их пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="efc5e-135">This change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.</span></span>
