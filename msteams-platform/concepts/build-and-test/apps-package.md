---
title: Пакет приложения
description: Узнайте, как упаковать Microsoft Teams приложение для тестирования, загрузки и публикации в магазине.
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 219e2d5341707ed51b7e0a3a8077f93df9eac640
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565216"
---
# <a name="create-a-microsoft-teams-app-package"></a><span data-ttu-id="0ede0-103">Создание пакета Microsoft Teams приложений</span><span class="sxs-lookup"><span data-stu-id="0ede0-103">Create a Microsoft Teams app package</span></span>

<span data-ttu-id="0ede0-104">Вам нужен пакет приложений, однако вы планируете распространять свои Microsoft Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="0ede0-104">You need an app package however you plan to distribute your Microsoft Teams app.</span></span> <span data-ttu-id="0ede0-105">Действительный пакет является файлом, который содержит следующее:</span><span class="sxs-lookup"><span data-stu-id="0ede0-105">A valid package is a ZIP file that contains the following:</span></span>

* <span data-ttu-id="0ede0-106">**Манифест приложения**: Описывает, как настроено ваше приложение, включая его возможности, необходимые ресурсы и другие важные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="0ede0-106">**App manifest**: Describes how your app is configured, including its capabilities, required resources, and other important attributes.</span></span>
* <span data-ttu-id="0ede0-107">**Значки приложений**: Каждый пакет требует значка цвета и контура для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="0ede0-107">**App icons**: Each package requires a color and outline icon for your app.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="0ede0-108">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="0ede0-108">App manifest</span></span>

<span data-ttu-id="0ede0-109">Файл манифеста приложения должен быть на верхнем уровне пакета с `manifest.json` именем.</span><span class="sxs-lookup"><span data-stu-id="0ede0-109">Your app manifest file must be at the top level of the package with the name `manifest.json`.</span></span> 

<span data-ttu-id="0ede0-110">При публикации в Teams, убедитесь, что ваш манифест ссылки на последнюю [схему](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="0ede0-110">When publishing to the Teams store, make sure your manifest references the latest [schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="app-icons"></a><span data-ttu-id="0ede0-111">Значки приложений</span><span class="sxs-lookup"><span data-stu-id="0ede0-111">App icons</span></span>

<span data-ttu-id="0ede0-112">Пакет приложений должен включать две версии значка приложения PNG: цвет и наброски версии.</span><span class="sxs-lookup"><span data-stu-id="0ede0-112">Your app package must include two PNG versions of your app icon: A color and outline version.</span></span>

> [!Note]
> <span data-ttu-id="0ede0-113">Если в вашем приложении есть бот или расширение обмена сообщениями, ваши значки также будут включены в Microsoft Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="0ede0-113">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

<span data-ttu-id="0ede0-114">Чтобы ваше приложение Teams обзор магазина, эти значки должны соответствовать следующим требованиям к размеру.</span><span class="sxs-lookup"><span data-stu-id="0ede0-114">For your app to pass Teams store review, these icons must meet the following size requirements.</span></span>

### <a name="color-icon"></a><span data-ttu-id="0ede0-115">Значок цвета</span><span class="sxs-lookup"><span data-stu-id="0ede0-115">Color icon</span></span>

<span data-ttu-id="0ede0-116">Цветовая версия значка отображается в большинстве сценариев Teams должна быть 192x192 пикселей.</span><span class="sxs-lookup"><span data-stu-id="0ede0-116">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="0ede0-117">Символ значка (96x96 пикселей) может быть любого цвета, но он должен сидеть на твердом или полностью прозрачном квадратном фоне.</span><span class="sxs-lookup"><span data-stu-id="0ede0-117">Your icon symbol (96x96 pixels) can be any color, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="0ede0-118">Teams автоматически обуборляет значок, чтобы отображать квадрат с закругленными углами в нескольких сценариях и шестиугольной формой в сценариях ботов.</span><span class="sxs-lookup"><span data-stu-id="0ede0-118">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="0ede0-119">Чтобы обрезать символ, не теряя деталей, включите 48 пикселей обивки вокруг вашего символа.</span><span class="sxs-lookup"><span data-stu-id="0ede0-119">To crop the symbol without losing any detail, include 48 pixels of padding around your symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams цвет и руководство по дизайну." border="false":::

### <a name="outline-icon"></a><span data-ttu-id="0ede0-121">Значок контура</span><span class="sxs-lookup"><span data-stu-id="0ede0-121">Outline icon</span></span>

<span data-ttu-id="0ede0-122">Значок контура отображается в двух сценариях:</span><span class="sxs-lookup"><span data-stu-id="0ede0-122">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="0ede0-123">Когда приложение используется и «поднимается» на бар приложения на левой стороне Teams.</span><span class="sxs-lookup"><span data-stu-id="0ede0-123">When your app is in use and “hoisted” on the app bar on the left side of Teams.</span></span>
* <span data-ttu-id="0ede0-124">Когда пользователь прижимает расширение обмена сообщениями вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="0ede0-124">When a user pins your app's messaging extension.</span></span>

<span data-ttu-id="0ede0-125">Значок должен быть 32x32 пикселей.</span><span class="sxs-lookup"><span data-stu-id="0ede0-125">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="0ede0-126">Он может быть белым с прозрачным фоном или прозрачным с белым фоном (никакие другие цвета не допускаются).</span><span class="sxs-lookup"><span data-stu-id="0ede0-126">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="0ede0-127">Значок контура не должен иметь дополнительной обивки вокруг символа.</span><span class="sxs-lookup"><span data-stu-id="0ede0-127">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams наброски руководства по проектированию иконок." border="false":::

### <a name="best-practices"></a><span data-ttu-id="0ede0-129">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="0ede0-129">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Иллюстрация, показывающая, как проектировать значки приложений." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="0ede0-131">У: Следуйте точным рекомендациям значок контура</span><span class="sxs-lookup"><span data-stu-id="0ede0-131">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="0ede0-132">Значения RGB белого, используемого в вашей иконке, должны быть красными: 255, зелеными: 255, синими: 255.</span><span class="sxs-lookup"><span data-stu-id="0ede0-132">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="0ede0-133">Все остальные части значка контура должны быть полностью прозрачными, а альфа-канал установлен на 0.</span><span class="sxs-lookup"><span data-stu-id="0ede0-133">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Иллюстрация, показывающая, как не проектировать значки приложений." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="0ede0-135">Не: Урожай в круглой или округлой квадратной форме</span><span class="sxs-lookup"><span data-stu-id="0ede0-135">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="0ede0-136">Значок цвета, представленный в пакете приложения, должен быть квадратным.</span><span class="sxs-lookup"><span data-stu-id="0ede0-136">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="0ede0-137">Не обгоните углы иконы.</span><span class="sxs-lookup"><span data-stu-id="0ede0-137">Don’t round the corners of your icon.</span></span> <span data-ttu-id="0ede0-138">Teams автоматически регулирует радиус угла.</span><span class="sxs-lookup"><span data-stu-id="0ede0-138">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a><span data-ttu-id="0ede0-139">Не: Копировать другие бренды</span><span class="sxs-lookup"><span data-stu-id="0ede0-139">Don't: Copy other brands</span></span>

<span data-ttu-id="0ede0-140">Ваши значки не должны имитировать любые защищенные авторским правом продукты, которые вы не владеете.</span><span class="sxs-lookup"><span data-stu-id="0ede0-140">Your icons must not mimic any copyrighted products that you don't own.</span></span> <span data-ttu-id="0ede0-141">Например, дизайн, похожий на продукт или бренд корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0ede0-141">For example, a design similar to a Microsoft product or brand.</span></span>

### <a name="examples"></a><span data-ttu-id="0ede0-142">Примеры</span><span class="sxs-lookup"><span data-stu-id="0ede0-142">Examples</span></span>

<span data-ttu-id="0ede0-143">Вот как значки приложений отображаются в различных Teams и контекстах.</span><span class="sxs-lookup"><span data-stu-id="0ede0-143">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="0ede0-144">Личное приложение</span><span class="sxs-lookup"><span data-stu-id="0ede0-144">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Пример, показывающий, как значок приложения выглядит в личном приложении." border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="0ede0-146">Бот (канал)</span><span class="sxs-lookup"><span data-stu-id="0ede0-146">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Пример, показывающий, как значок приложения выглядит на боте внутри канала." border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="0ede0-148">Расширение для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0ede0-148">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<альт текстовых>" border="false":::

## <a name="next-step"></a><span data-ttu-id="0ede0-150">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="0ede0-150">Next step</span></span>

<span data-ttu-id="0ede0-151">Выберите способ распространения приложения:</span><span class="sxs-lookup"><span data-stu-id="0ede0-151">Choose how you plan to distribute your app:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0ede0-152">Загрузка приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="0ede0-152">Sideload your app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="0ede0-153">Опубликовать приложение на сайте org</span><span class="sxs-lookup"><span data-stu-id="0ede0-153">Publish your app to your org</span></span>](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [<span data-ttu-id="0ede0-154">Публикация приложения в магазине</span><span class="sxs-lookup"><span data-stu-id="0ede0-154">Publish your app to the store</span></span>](~/concepts/deploy-and-publish/appsource/publish.md)
