---
title: Разработка приложения . Понимание системы проектирования
description: Узнайте об основах разработки Microsoft Teams, включая макет, цветовую схему и другие.
author: heath-hamilton
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0af2a22200e62be9289f167b0306c9769366e46a
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630844"
---
# <a name="microsoft-teams-app-design-system"></a><span data-ttu-id="ac7b5-103">Microsoft Teams системы разработки приложений</span><span class="sxs-lookup"><span data-stu-id="ac7b5-103">Microsoft Teams app design system</span></span>

<span data-ttu-id="ac7b5-104">Быстро узнайте об основах разработки Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-104">Quickly learn about the fundamentals of Teams app design.</span></span> <span data-ttu-id="ac7b5-105">Всесторонние рекомендации и примеры можно найти в <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams пользовательского интерфейса (Figma).</a></span><span class="sxs-lookup"><span data-stu-id="ac7b5-105">You can find comprehensive guidance and examples in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma)</a>.</span></span>

## <a name="layout"></a><span data-ttu-id="ac7b5-106">Макет</span><span class="sxs-lookup"><span data-stu-id="ac7b5-106">Layout</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="ac7b5-107">Teams для обеспечения последовательных и элегантных связей между компонентами дизайна зависит от макета сетки.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-107">Teams relies on a grid layout to ensure consistent and elegant relationships between design components.</span></span> <span data-ttu-id="ac7b5-108">Базовый блок сетки с 4 пикселями позволяет компонентам последовательно масштабироваться во всех размерах отображения в Teams.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-108">The grid’s 4-pixel base unit allows components to scale consistently across all display sizes in Teams.</span></span>

      * [<span data-ttu-id="ac7b5-109">Полное руководство по макету (Figma)</span><span class="sxs-lookup"><span data-stu-id="ac7b5-109">See full layout guidelines (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)
      * [<span data-ttu-id="ac7b5-110">Реализация макета (fluent UI)</span><span class="sxs-lookup"><span data-stu-id="ac7b5-110">Implement layout (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/layout)

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-layout.png" alt-text="Концептуальное изображение Teams макета." border="false":::
   :::column-end:::

:::row-end:::

## <a name="avatars"></a><span data-ttu-id="ac7b5-112">Аватары</span><span class="sxs-lookup"><span data-stu-id="ac7b5-112">Avatars</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="ac7b5-113">Аватар — это графическое представление человека, команды, бота или объекта в Teams.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-113">An avatar is a graphical representation of a person, team, bot, or entity in Teams.</span></span> <span data-ttu-id="ac7b5-114">Группа аватаров часто используется для передачи живой активности или представления реестра таким образом, чтобы сохранить вертикальное пространство.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-114">An avatar group is often used to convey live activity or a represent a roster in a way that preserves vertical space.</span></span> 

      * <span data-ttu-id="ac7b5-115"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Полное руководство по аватарам (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="ac7b5-115"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full avatar guidelines (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-avatars.png" alt-text="Концептуальное изображение Teams аватаров." border="false":::

   :::column-end:::
:::row-end:::

## <a name="icons"></a><span data-ttu-id="ac7b5-117">Значки</span><span class="sxs-lookup"><span data-stu-id="ac7b5-117">Icons</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="ac7b5-118">Основной значок приложения может пройти долгий путь для передачи вашего бренда Teams пользователям.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-118">Your app's primary icon can go a long way in conveying your brand to Teams users.</span></span> <span data-ttu-id="ac7b5-119">Получение правильного оформления значка также важно для [публикации](../../concepts/build-and-test/apps-package.md) приложения в Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-119">Getting your icon design right is also important for [publishing your app](../../concepts/build-and-test/apps-package.md) to the Teams store.</span></span>

      <span data-ttu-id="ac7b5-120">Вы также можете использовать значки пользовательского интерфейса Fluent во всем приложении:</span><span class="sxs-lookup"><span data-stu-id="ac7b5-120">You also can use Fluent UI icons throughout your app:</span></span>

      * <span data-ttu-id="ac7b5-121"><a href="https://www.figma.com/community/file/836835755999342788" target="_blank">Получите последний набор значков Fluent (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="ac7b5-121"><a href="https://www.figma.com/community/file/836835755999342788" target="_blank">Get the latest Fluent icon set (Figma)</a></span></span>
      * [<span data-ttu-id="ac7b5-122">Реализация значков (fluent UI)</span><span class="sxs-lookup"><span data-stu-id="ac7b5-122">Implement the icons (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/icons)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-iconography.png" alt-text="Концептуальное изображение Teams значков." border="false":::

   :::column-end:::
:::row-end:::

## <a name="type"></a><span data-ttu-id="ac7b5-124">Тип</span><span class="sxs-lookup"><span data-stu-id="ac7b5-124">Type</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="ac7b5-125">Teams использует пользовательский интерфейс Segoe для своей рампы типа и различных размеров шрифтов и весов для создания иерархии и обеспечения читаемости.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-125">Teams uses Segoe UI for its type ramp and different font sizes and weights to help create hierarchy and ensure readability.</span></span>

      * <span data-ttu-id="ac7b5-126"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">См. рекомендации по полному типу (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="ac7b5-126"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full type guidelines (Figma)</a></span></span>
      * [<span data-ttu-id="ac7b5-127">Реализация типографии (fluent UI)</span><span class="sxs-lookup"><span data-stu-id="ac7b5-127">Implement typography (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/typography)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-typography.png" alt-text="Концептуальный образ Teams типографии." border="false":::

   :::column-end:::
:::row-end:::

## <a name="colors"></a><span data-ttu-id="ac7b5-129">цвета;</span><span class="sxs-lookup"><span data-stu-id="ac7b5-129">Colors</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="ac7b5-130">Teams и настольные компьютеры поддерживают темы по умолчанию (светлые), темные и высоко контрастные, а Teams поддерживают светлые и темные темы.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-130">Teams web and desktop supports default (light), dark, and high-contrast themes, while Teams mobile supports light and dark themes.</span></span> <span data-ttu-id="ac7b5-131">Каждая тема имеет свою цветовую схему.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-131">Each theme has its own color scheme.</span></span>

      * <span data-ttu-id="ac7b5-132"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Полное руководство по цвету и доступные маркеры цвета (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="ac7b5-132"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full color guidelines and available color tokens (Figma)</a></span></span>
      * [<span data-ttu-id="ac7b5-133">Реализация цветов (fluent UI)</span><span class="sxs-lookup"><span data-stu-id="ac7b5-133">Implement colors (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/0.51.7/colors)

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-color.png" alt-text="Образ концепции Teams цветов." border="false":::
   :::column-end:::

:::row-end:::

## <a name="shape-and-elevation"></a><span data-ttu-id="ac7b5-135">Форма и высота</span><span class="sxs-lookup"><span data-stu-id="ac7b5-135">Shape and elevation</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="ac7b5-136">Вы можете использовать форму и высоту для создания дополнительной иерархии в приложении.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-136">You can use shape and elevation to create additional hierarchy in your app.</span></span> 

      * <span data-ttu-id="ac7b5-137"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">См. инструкции по полной форме и высоте (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="ac7b5-137"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full shape and elevation guidelines (Figma)</a></span></span>
      * [<span data-ttu-id="ac7b5-138">Реализация формы и высоты (fluent UI)</span><span class="sxs-lookup"><span data-stu-id="ac7b5-138">Implement shape and elevation (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/elevation)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/shape-and-elevation.png" alt-text="Концептуальные формы и высоты." border="false":::

   :::column-end:::
:::row-end:::

## <a name="copy-and-content"></a><span data-ttu-id="ac7b5-140">Копирование и контент</span><span class="sxs-lookup"><span data-stu-id="ac7b5-140">Copy and content</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="ac7b5-141">Чтобы почувствовать себя частью Teams, ваша копия приложения в целом должна следовать этим принципам голосовой поддержки [Майкрософт:](/style-guide/brand-voice-above-all-simple-human)теплый и расслабленный, четкий и ясный, и готовы протянуть руку.</span><span class="sxs-lookup"><span data-stu-id="ac7b5-141">To feel part of Teams, your app copy in general should follow these [Microsoft voice principles](/style-guide/brand-voice-above-all-simple-human): warm and relaxed, crisp and clear, and ready to lend hand.</span></span>

      * <span data-ttu-id="ac7b5-142"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Полное руководство по копированию и контенту, включая написание для ботов (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="ac7b5-142"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full copy and content guidelines—including writing for bots (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-copy-and-content.png" alt-text="Концептуальное изображение копирования и контента." border="false":::

   :::column-end:::
:::row-end:::
