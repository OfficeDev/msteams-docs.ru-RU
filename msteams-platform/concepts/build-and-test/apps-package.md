---
title: Пакет приложения
description: Узнайте, как упаковировать приложение Microsoft Teams для тестирования, загрузки и публикации в магазине.
ms.topic: conceptual
ms.openlocfilehash: 222ea5459b3496c00b1186f15a68c3288ce419f7
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922512"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="a601f-103">Создание пакета приложений для приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a601f-103">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="a601f-104">Приложения в Teams определяются файлом JSON манифеста приложения и упаковываются в пакет приложений с их значками.</span><span class="sxs-lookup"><span data-stu-id="a601f-104">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="a601f-105">Вам потребуется пакет приложений для загрузки и установки приложения в Teams и публикации в каталоге бизнес-приложений или в AppSource.</span><span class="sxs-lookup"><span data-stu-id="a601f-105">You'll need an app package to upload and install your app in Teams and publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="a601f-106">Пакет приложений Teams — это файл .zip, содержащий следующие:</span><span class="sxs-lookup"><span data-stu-id="a601f-106">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="a601f-107">Файл манифеста с именем , который указывает атрибуты вашего приложения и указывает на необходимые ресурсы для вашего опыта, например расположение страницы конфигурации вкладок или ID приложения Майкрософт для `manifest.json` своего бота.</span><span class="sxs-lookup"><span data-stu-id="a601f-107">A manifest file named `manifest.json`, which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="a601f-108">[Цвет и значки контура для вашего приложения](#app-icons).</span><span class="sxs-lookup"><span data-stu-id="a601f-108">[Color and outline icons for your app](#app-icons).</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="a601f-109">Создание манифеста</span><span class="sxs-lookup"><span data-stu-id="a601f-109">Creating a manifest</span></span>

<span data-ttu-id="a601f-110">**Teams App Studio** может помочь настроить манифест.</span><span class="sxs-lookup"><span data-stu-id="a601f-110">**Teams App Studio** can help configure your manifest.</span></span> <span data-ttu-id="a601f-111">Оно также содержит библиотеку элементов управления React и настраиваемые примеры для карточек.</span><span class="sxs-lookup"><span data-stu-id="a601f-111">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="a601f-112">Дополнительные сведения см. в [обзоре App Studio.](~/concepts/build-and-test/app-studio-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a601f-112">For more information, see [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="a601f-113">Файл манифеста должен быть manifest.jsи быть на верхнем уровне пакета отправки.</span><span class="sxs-lookup"><span data-stu-id="a601f-113">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="a601f-114">Обратите внимание, что манифесты и пакеты, построенные ранее, могут поддерживать старую версию схемы.</span><span class="sxs-lookup"><span data-stu-id="a601f-114">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="a601f-115">Для командных приложений и особенно отправки AppSource (ранее Office Store) необходимо использовать текущую [схему манифеста.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="a601f-115">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="a601f-116">Укажите схему в начале манифеста, чтобы включить IntelliSense или аналогичную поддержку редактора кода:</span><span class="sxs-lookup"><span data-stu-id="a601f-116">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",`
 
## <a name="app-icons"></a><span data-ttu-id="a601f-117">Значки приложений</span><span class="sxs-lookup"><span data-stu-id="a601f-117">App icons</span></span>

<span data-ttu-id="a601f-118">Пакет приложения должен включать две версии значка приложения PNG — значок цвета и значок контура.</span><span class="sxs-lookup"><span data-stu-id="a601f-118">Your app package must include two PNG versions of your app icon—a color icon and an outline icon.</span></span> <span data-ttu-id="a601f-119">Чтобы приложение прошло обзор AppSource, эти значки должны соответствовать следующим требованиям к размеру.</span><span class="sxs-lookup"><span data-stu-id="a601f-119">For your app to pass the AppSource review, these icons must meet the following size requirements.</span></span>

> [!Note]
> <span data-ttu-id="a601f-120">Если в вашем приложении есть расширение бота или обмена сообщениями, значки также будут включены в регистрацию Microsoft Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="a601f-120">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

### <a name="color-icon"></a><span data-ttu-id="a601f-121">Значок цвета</span><span class="sxs-lookup"><span data-stu-id="a601f-121">Color icon</span></span>

<span data-ttu-id="a601f-122">Цветная версия значка отображается в большинстве сценариев Teams и должна быть 192x192 пикселей.</span><span class="sxs-lookup"><span data-stu-id="a601f-122">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="a601f-123">Символ значка (96x96 пикселей) может быть любым цветом или цветом, но он должен сидеть на твердом или полностью прозрачном квадратном фоне.</span><span class="sxs-lookup"><span data-stu-id="a601f-123">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="a601f-124">Команды автоматически обнажают значок для отображения квадрата с закругленными углами в нескольких сценариях и шестиугольной формы в сценариях ботов.</span><span class="sxs-lookup"><span data-stu-id="a601f-124">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="a601f-125">Включите 48 пикселей обивки вокруг символа, чтобы эти культуры можно было сделать без потери деталей.</span><span class="sxs-lookup"><span data-stu-id="a601f-125">Include 48 pixels of padding around your symbol so these crops can be made without losing any detail.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Руководство по проектированию значков цвета Teams." border="false":::

### <a name="outline-icon"></a><span data-ttu-id="a601f-127">Значок Outline</span><span class="sxs-lookup"><span data-stu-id="a601f-127">Outline icon</span></span>

<span data-ttu-id="a601f-128">Значок плана отображает в двух сценариях:</span><span class="sxs-lookup"><span data-stu-id="a601f-128">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="a601f-129">Когда приложение используется и "подъехали" на панели приложений слева от Teams.</span><span class="sxs-lookup"><span data-stu-id="a601f-129">When your app is in use and “hoisted” on the app bar on the left of Teams.</span></span>
* <span data-ttu-id="a601f-130">когда пользователь пин-коды расширения обмена сообщениями вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a601f-130">when a user pins your app's messaging extension.</span></span>

<span data-ttu-id="a601f-131">Значок должен быть 32x32 пикселей.</span><span class="sxs-lookup"><span data-stu-id="a601f-131">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="a601f-132">Он может быть белым с прозрачным фоном или прозрачным с белым фоном (другие цвета не допускаются).</span><span class="sxs-lookup"><span data-stu-id="a601f-132">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="a601f-133">Значок outline не должен иметь дополнительных обивок вокруг символа.</span><span class="sxs-lookup"><span data-stu-id="a601f-133">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams outline icon design guidance." border="false":::

### <a name="best-practices"></a><span data-ttu-id="a601f-135">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="a601f-135">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Иллюстрация, показывающая, как создать значки приложения." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="a601f-137">Do: Следуйте указаниям по точным значкам плана</span><span class="sxs-lookup"><span data-stu-id="a601f-137">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="a601f-138">Значения RGB белого цвета, используемые в значке, должны быть красными: 255, Зеленым: 255, Синим: 255.</span><span class="sxs-lookup"><span data-stu-id="a601f-138">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="a601f-139">Все остальные части значка контура должны быть полностью прозрачными, а альфа-каналу установлено 0.</span><span class="sxs-lookup"><span data-stu-id="a601f-139">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Иллюстрация, показывающая, как не проектировать значки приложения." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="a601f-141">Не: Обрезать в круговой или округлой квадратной форме</span><span class="sxs-lookup"><span data-stu-id="a601f-141">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="a601f-142">Значок цвета, представленный в пакете приложения, должен быть квадратным.</span><span class="sxs-lookup"><span data-stu-id="a601f-142">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="a601f-143">Не закругляйте углы значка.</span><span class="sxs-lookup"><span data-stu-id="a601f-143">Don’t round the corners of your icon.</span></span> <span data-ttu-id="a601f-144">Команды автоматически настраивают радиус угла.</span><span class="sxs-lookup"><span data-stu-id="a601f-144">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

### <a name="examples"></a><span data-ttu-id="a601f-145">Примеры</span><span class="sxs-lookup"><span data-stu-id="a601f-145">Examples</span></span>

<span data-ttu-id="a601f-146">Вот как значки приложений отображаются в различных возможностях и контекстах Teams.</span><span class="sxs-lookup"><span data-stu-id="a601f-146">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="a601f-147">Личное приложение</span><span class="sxs-lookup"><span data-stu-id="a601f-147">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Пример, показывающий внешний вид значка приложения в личном приложении." border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="a601f-149">Бот (канал)</span><span class="sxs-lookup"><span data-stu-id="a601f-149">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Пример, показывающий, как значок приложения выглядит на боте внутри канала." border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="a601f-151">Расширение для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a601f-151">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<alt text>" border="false":::
