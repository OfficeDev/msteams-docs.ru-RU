---
title: Удаление полей вкладок в Microsoft Teams
author: laujan
description: Описывает, как удаление полей вкладок повысит качество работы разработчика.
keywords: удаление полей вкладки
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 78d97dca73e7fce2bf4b911f5ea4588525667378
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019715"
---
# <a name="tab-margin-changes"></a><span data-ttu-id="06e18-104">Изменения полей вкладок</span><span class="sxs-lookup"><span data-stu-id="06e18-104">Tab margin changes</span></span>

<span data-ttu-id="06e18-105">В этом документе описывается, как удаление полей вокруг всех вкладок в Microsoft Teams повысит возможности разработчика при создании приложений.</span><span class="sxs-lookup"><span data-stu-id="06e18-105">This document describes how the removal of margins around all tabs in Microsoft Teams will enhance the developer's experience when building apps.</span></span> <span data-ttu-id="06e18-106">Это усовершенствование, введено в Microsoft Teams 2021 году.</span><span class="sxs-lookup"><span data-stu-id="06e18-106">This is an enhancement introduced in Microsoft Teams in 2021.</span></span>
<span data-ttu-id="06e18-107">Удаление полей вокруг всех вкладок позволит разработчикам создавать приложения, которые выглядят более родными для Teams.</span><span class="sxs-lookup"><span data-stu-id="06e18-107">Removing the margins around all tabs will allow developers to build apps that look more native to Teams.</span></span> <span data-ttu-id="06e18-108">Это также согласуется с нашими [проектами комплекта пользовательского интерфейса.](~/tabs/design/tabs.md)</span><span class="sxs-lookup"><span data-stu-id="06e18-108">This will also align with our [UI kit designs](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="06e18-109">Большинство приложений уже выглядят лучше без полей, окружающих их опытом.</span><span class="sxs-lookup"><span data-stu-id="06e18-109">Most apps already look better without the margins surrounding their experiences.</span></span> <span data-ttu-id="06e18-110">Однако некоторые вкладки визуально влияют на это изменение, и разработчики должны внести необходимые изменения.</span><span class="sxs-lookup"><span data-stu-id="06e18-110">However, some tabs are visually affected by this change, and developers must make the necessary changes.</span></span>

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Вкладка остроумие и без маржи" border="false":::

> [!NOTE]
> <span data-ttu-id="06e18-112">Эта функция не применима к мобильным клиентам, так как вкладки, просматриваемые в мобильных клиентах, не имеют маржи.</span><span class="sxs-lookup"><span data-stu-id="06e18-112">This feature is not applicable to mobile clients, as the tabs viewed in the mobile clients do not have margins.</span></span> 

## <a name="timelines"></a><span data-ttu-id="06e18-113">Сроки</span><span class="sxs-lookup"><span data-stu-id="06e18-113">Timelines</span></span>

* <span data-ttu-id="06e18-114">5 марта 2021 г. — Поля, удалены в [общедоступных](~/resources/dev-preview/developer-preview-intro.md)Developer Preview .</span><span class="sxs-lookup"><span data-stu-id="06e18-114">March 5, 2021 - Margins removed in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
* <span data-ttu-id="06e18-115">15 июня 2021 г. Маржи будут удалены в производстве.</span><span class="sxs-lookup"><span data-stu-id="06e18-115">June 15, 2021 - Margins will be removed in production.</span></span>

## <a name="guidelines"></a><span data-ttu-id="06e18-116">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="06e18-116">Guidelines</span></span>

<span data-ttu-id="06e18-117">Microsoft Teams приложения, которые используют вкладки, будут затронуты этим изменением.</span><span class="sxs-lookup"><span data-stu-id="06e18-117">Microsoft Teams apps that use tabs will be affected by this change.</span></span> <span data-ttu-id="06e18-118">Разработчики должны перейти на общедоступные [Developer Preview,](~/resources/dev-preview/developer-preview-intro.md) чтобы определить, как влияют их вкладки и внести необходимые изменения.</span><span class="sxs-lookup"><span data-stu-id="06e18-118">Developers must switch to [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) in order to determine how their tabs are affected and make the necessary changes.</span></span>

<span data-ttu-id="06e18-119">Разработчики вкладок не должны полагаться на Teams, чтобы предоставлять поля, окружающие их вкладки.</span><span class="sxs-lookup"><span data-stu-id="06e18-119">Tab developers must not rely on Teams to provide margins surrounding their tabs.</span></span> <span data-ttu-id="06e18-120">Разработчикам рекомендуется добавлять поля вокруг их проектов вкладок там, где это необходимо.</span><span class="sxs-lookup"><span data-stu-id="06e18-120">Developers are encouraged to add margins around their tab designs where it is required.</span></span> <span data-ttu-id="06e18-121">Проекты приложений в производстве могут выглядеть так, как будто существует дополнительная обивка, то есть поля, предоставляемые Teams и поля, предоставляемые вкладкой. Однако дополнительная обивка является временной и пройдет через несколько недель, оставив только предоставленную обивку приложения.</span><span class="sxs-lookup"><span data-stu-id="06e18-121">App designs in production can look like there is extra padding, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and will go away in a few weeks, leaving only the app's provided padding.</span></span>

## <a name="faq"></a><span data-ttu-id="06e18-122">Вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="06e18-122">FAQ</span></span>

<span data-ttu-id="06e18-123">**Можно ли для хрома приложения, например панели заголовки или панели задач, прикасаться к краям наших проектов?**</span><span class="sxs-lookup"><span data-stu-id="06e18-123">**Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?**</span></span>

<span data-ttu-id="06e18-124">Да, это нормально и поощряется.</span><span class="sxs-lookup"><span data-stu-id="06e18-124">Yes, this is fine and encouraged.</span></span> <span data-ttu-id="06e18-125">Это помогает приложению чувствовать себя родным.</span><span class="sxs-lookup"><span data-stu-id="06e18-125">This helps the app feel native.</span></span>

<span data-ttu-id="06e18-126">**Нормально ли для контента приложения, например текста, логотипов и изображений, прикасаться к левым и правым краям наших проектов?**</span><span class="sxs-lookup"><span data-stu-id="06e18-126">**Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?**</span></span>

<span data-ttu-id="06e18-127">Нет, необходимо предоставить собственную обивку или поля слева и справа от всего контента приложения, чтобы он не касался краев пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="06e18-127">No, you must provide your own padding or margins to the left and right of all app content to ensure it does not touch the edges of your UI.</span></span> <span data-ttu-id="06e18-128">При необходимости можно также добавить поля в верхней части вкладки.</span><span class="sxs-lookup"><span data-stu-id="06e18-128">You can also add margins at the top of your tab, if required.</span></span>

<span data-ttu-id="06e18-129">**Каков размер ранее примененных Teams?**</span><span class="sxs-lookup"><span data-stu-id="06e18-129">**What's the size of the margins Teams previously applied?**</span></span>

* <span data-ttu-id="06e18-130">Слева и справа: 20px</span><span class="sxs-lookup"><span data-stu-id="06e18-130">Left and right: 20px</span></span>
* <span data-ttu-id="06e18-131">Топ: 16px</span><span class="sxs-lookup"><span data-stu-id="06e18-131">Top: 16px</span></span>
* <span data-ttu-id="06e18-132">Нижний: 0px</span><span class="sxs-lookup"><span data-stu-id="06e18-132">Bottom: 0px</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="06e18-133">Все вкладки имеют свои поля удалены: личные вкладки, (групповые) вкладки чата, вкладки собраний и вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="06e18-133">All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.</span></span>
> * <span data-ttu-id="06e18-134">Нет способа отказаться от этого изменения или отказаться от этого изменения.</span><span class="sxs-lookup"><span data-stu-id="06e18-134">There is no way to opt-in or opt-out of this change.</span></span> <span data-ttu-id="06e18-135">Он будет применяться для всех вкладок.</span><span class="sxs-lookup"><span data-stu-id="06e18-135">It will apply to all tabs.</span></span>
> * <span data-ttu-id="06e18-136">Это изменение может повлиять на вкладки, которые Microsoft Teams для предоставления полей вокруг пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="06e18-136">This change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.</span></span>
