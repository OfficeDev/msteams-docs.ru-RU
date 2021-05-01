---
title: Пакет приложения
description: Узнайте, как упаковировать Microsoft Teams для тестирования, загрузки и публикации в магазине.
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: e477539a9b8eaa0c869a2070fcd20b74aecfe490
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101704"
---
# <a name="create-a-microsoft-teams-app-package"></a><span data-ttu-id="57820-103">Создание пакета Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="57820-103">Create a Microsoft Teams app package</span></span>

<span data-ttu-id="57820-104">Вам нужен пакет приложений, однако вы планируете распространять Microsoft Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="57820-104">You need an app package however you plan to distribute your Microsoft Teams app.</span></span> <span data-ttu-id="57820-105">Допустимый пакет — это файл ZIP, содержащий следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="57820-105">A valid package is a ZIP file that contains the following:</span></span>

* <span data-ttu-id="57820-106">**Манифест приложения.** Описывается настройка приложения, включая его возможности, необходимые ресурсы и другие важные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="57820-106">**App manifest**: Describes how your app is configured, including its capabilities, required resources, and other important attributes.</span></span>
* <span data-ttu-id="57820-107">**Значки** приложения. Для каждого пакета требуется значок цвета и контура для приложения.</span><span class="sxs-lookup"><span data-stu-id="57820-107">**App icons**: Each package requires a color and outline icon for your app.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="57820-108">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="57820-108">App manifest</span></span>

<span data-ttu-id="57820-109">Файл манифеста приложения должен быть на верхнем уровне пакета с `manifest.json` именем.</span><span class="sxs-lookup"><span data-stu-id="57820-109">Your app manifest file must be at the top level of the package with the name `manifest.json`.</span></span> 

<span data-ttu-id="57820-110">При публикации в Teams убедитесь, что манифест ссылается на последнюю [схему.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="57820-110">When publishing to the Teams store, make sure your manifest references the latest [schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="app-icons"></a><span data-ttu-id="57820-111">Значки приложений</span><span class="sxs-lookup"><span data-stu-id="57820-111">App icons</span></span>

<span data-ttu-id="57820-112">Пакет приложения должен включать две PNG-версии значка приложения: цветную и очертания.</span><span class="sxs-lookup"><span data-stu-id="57820-112">Your app package must include two PNG versions of your app icon: A color and outline version.</span></span>

> [!Note]
> <span data-ttu-id="57820-113">Если у приложения есть расширение бота или обмена сообщениями, значки также будут включены в Microsoft Azure службы ботов.</span><span class="sxs-lookup"><span data-stu-id="57820-113">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

<span data-ttu-id="57820-114">Чтобы приложение прошло проверку Teams магазина, эти значки должны соответствовать следующим требованиям к размеру.</span><span class="sxs-lookup"><span data-stu-id="57820-114">For your app to pass Teams store review, these icons must meet the following size requirements.</span></span>

### <a name="color-icon"></a><span data-ttu-id="57820-115">Значок цвета</span><span class="sxs-lookup"><span data-stu-id="57820-115">Color icon</span></span>

<span data-ttu-id="57820-116">Цветная версия значка отображается в большинстве Teams и должна быть 192x192 пикселей.</span><span class="sxs-lookup"><span data-stu-id="57820-116">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="57820-117">Символ значка (96x96 пикселей) может быть любого цвета, но он должен сидеть на сплошном или полностью прозрачном квадратном фоне.</span><span class="sxs-lookup"><span data-stu-id="57820-117">Your icon symbol (96x96 pixels) can be any color, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="57820-118">Teams автоматически обнажает значок для отображения квадрата с закругленными углами в нескольких сценариях и шестиугольной формы в сценариях ботов.</span><span class="sxs-lookup"><span data-stu-id="57820-118">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="57820-119">Чтобы обрезать символ без потери деталей, включите 48 пикселей обивки вокруг символа.</span><span class="sxs-lookup"><span data-stu-id="57820-119">To crop the symbol without losing any detail, include 48 pixels of padding around your symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams значок цвета и руководство по дизайну." border="false":::

### <a name="outline-icon"></a><span data-ttu-id="57820-121">Значок Outline</span><span class="sxs-lookup"><span data-stu-id="57820-121">Outline icon</span></span>

<span data-ttu-id="57820-122">Значок плана отображает в двух сценариях:</span><span class="sxs-lookup"><span data-stu-id="57820-122">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="57820-123">Когда приложение используется и "подъехалось" на панели приложения слева от Teams.</span><span class="sxs-lookup"><span data-stu-id="57820-123">When your app is in use and “hoisted” on the app bar on the left side of Teams.</span></span>
* <span data-ttu-id="57820-124">Когда пользователь пин-коды расширения обмена сообщениями вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="57820-124">When a user pins your app's messaging extension.</span></span>

<span data-ttu-id="57820-125">Значок должен быть 32x32 пикселей.</span><span class="sxs-lookup"><span data-stu-id="57820-125">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="57820-126">Он может быть белым с прозрачным фоном или прозрачным с белым фоном (другие цвета не допускаются).</span><span class="sxs-lookup"><span data-stu-id="57820-126">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="57820-127">Значок outline не должен иметь дополнительных обивок вокруг символа.</span><span class="sxs-lookup"><span data-stu-id="57820-127">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams руководство по проектированию значков." border="false":::

### <a name="best-practices"></a><span data-ttu-id="57820-129">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="57820-129">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Иллюстрация, показывающая, как создать значки приложения." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="57820-131">Do: Следуйте указаниям по точным значкам плана</span><span class="sxs-lookup"><span data-stu-id="57820-131">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="57820-132">Значения RGB белого цвета, используемые в значке, должны быть красными: 255, Зеленым: 255, Синим: 255.</span><span class="sxs-lookup"><span data-stu-id="57820-132">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="57820-133">Все остальные части значка контура должны быть полностью прозрачными, а альфа-каналу установлено 0.</span><span class="sxs-lookup"><span data-stu-id="57820-133">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Иллюстрация, показывающая, как не проектировать значки приложения." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="57820-135">Не: Обрезать в круговой или округлой квадратной форме</span><span class="sxs-lookup"><span data-stu-id="57820-135">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="57820-136">Значок цвета, представленный в пакете приложения, должен быть квадратным.</span><span class="sxs-lookup"><span data-stu-id="57820-136">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="57820-137">Не закругляйте углы значка.</span><span class="sxs-lookup"><span data-stu-id="57820-137">Don’t round the corners of your icon.</span></span> <span data-ttu-id="57820-138">Teams автоматически регулирует радиус угла.</span><span class="sxs-lookup"><span data-stu-id="57820-138">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a><span data-ttu-id="57820-139">Не: скопируйте другие бренды</span><span class="sxs-lookup"><span data-stu-id="57820-139">Don't: Copy other brands</span></span>

<span data-ttu-id="57820-140">Значки не должны имитировать любые продукты, которые не принадлежат вам (например, дизайн, аналогичный продукту или бренду Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="57820-140">Your icons must not mimic any copyrighted products that you don't own (for example, a design similar to a Microsoft product or brand).</span></span>

### <a name="examples"></a><span data-ttu-id="57820-141">Примеры</span><span class="sxs-lookup"><span data-stu-id="57820-141">Examples</span></span>

<span data-ttu-id="57820-142">Вот как значки приложений отображаются в разных Teams и контекстах.</span><span class="sxs-lookup"><span data-stu-id="57820-142">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="57820-143">Личное приложение</span><span class="sxs-lookup"><span data-stu-id="57820-143">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Пример, показывающий внешний вид значка приложения в личном приложении." border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="57820-145">Бот (канал)</span><span class="sxs-lookup"><span data-stu-id="57820-145">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Пример, показывающий, как значок приложения выглядит на боте внутри канала." border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="57820-147">Расширение для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="57820-147">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<alt text>" border="false":::

## <a name="next-step"></a><span data-ttu-id="57820-149">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="57820-149">Next step</span></span>

<span data-ttu-id="57820-150">Выберите, как вы планируете распространять приложение:</span><span class="sxs-lookup"><span data-stu-id="57820-150">Choose how you plan to distribute your app:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57820-151">Sideload ваше приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="57820-151">Sideload your app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="57820-152">Публикация приложения в вашей организации</span><span class="sxs-lookup"><span data-stu-id="57820-152">Publish your app to your org</span></span>](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [<span data-ttu-id="57820-153">Публикация приложения в магазине</span><span class="sxs-lookup"><span data-stu-id="57820-153">Publish your app to the store</span></span>](~/concepts/deploy-and-publish/appsource/publish.md)
