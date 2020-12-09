---
title: Упаковка приложения
description: Узнайте, как упаковать приложение Microsoft Teams для тестирования, отправки и хранения публикации.
ms.topic: conceptual
ms.openlocfilehash: 6929375c8d6a1602f01d83d15bfa0dab7f02a664
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605290"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="17208-103">Создание пакета приложений для приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="17208-103">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="17208-104">Приложения в Teams определяются с помощью JSON манифеста приложения и упаковываются в пакет приложения со своими значками.</span><span class="sxs-lookup"><span data-stu-id="17208-104">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="17208-105">Вам потребуется пакет приложения для отправки и установки приложения в Teams и публикации в каталоге бизнес-приложений или в AppSource.</span><span class="sxs-lookup"><span data-stu-id="17208-105">You'll need an app package to upload and install your app in Teams and publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="17208-106">Пакет приложения Teams — это ZIP-файл со следующими разделом:</span><span class="sxs-lookup"><span data-stu-id="17208-106">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="17208-107">Файл манифеста с именем `manifest.json` , который определяет атрибуты приложения и указывает на необходимые ресурсы для вашего интерфейса, например расположение страницы настройки вкладки или идентификатор приложения Microsoft для ленты.</span><span class="sxs-lookup"><span data-stu-id="17208-107">A manifest file named `manifest.json`, which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="17208-108">[Значки цвета и структуры приложения](#app-icons).</span><span class="sxs-lookup"><span data-stu-id="17208-108">[Color and outline icons for your app](#app-icons).</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="17208-109">Создание манифеста</span><span class="sxs-lookup"><span data-stu-id="17208-109">Creating a manifest</span></span>

<span data-ttu-id="17208-110">*Приложение Teams Studio* помогает настроить манифест.</span><span class="sxs-lookup"><span data-stu-id="17208-110">*Teams App Studio* can help configure your manifest.</span></span> <span data-ttu-id="17208-111">Оно также содержит библиотеку элементов управления React и настраиваемые примеры для карточек.</span><span class="sxs-lookup"><span data-stu-id="17208-111">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="17208-112">Ознакомьтесь с [обзором App Studio](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="17208-112">See [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="17208-113">Файл манифеста должен иметь имя "manifest.json" и быть на верхнем уровне пакета отправки.</span><span class="sxs-lookup"><span data-stu-id="17208-113">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="17208-114">Обратите внимание, что манифесты и пакеты, созданные ранее, могут поддерживать более старую версию схемы.</span><span class="sxs-lookup"><span data-stu-id="17208-114">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="17208-115">Для приложений Teams, особенно отправок AppSource (прежнее хранилище Office), необходимо использовать текущую [схему манифеста](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="17208-115">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="17208-116">Укажите схему в начале манифеста, чтобы включить поддержку IntelliSense или аналогичную поддержку в редакторе кода:</span><span class="sxs-lookup"><span data-stu-id="17208-116">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="app-icons"></a><span data-ttu-id="17208-117">Значки приложений</span><span class="sxs-lookup"><span data-stu-id="17208-117">App icons</span></span>

<span data-ttu-id="17208-118">Ваш пакет приложения должен включать две версии PNG значка приложения, цветовой значок и значок структуры.</span><span class="sxs-lookup"><span data-stu-id="17208-118">Your app package must include two PNG versions of your app icon—a color icon and an outline icon.</span></span> <span data-ttu-id="17208-119">Чтобы ваше приложение проходило проверку AppSource, эти значки должны соответствовать следующим требованиям к размеру.</span><span class="sxs-lookup"><span data-stu-id="17208-119">For your app to pass the AppSource review, these icons must meet the following size requirements.</span></span>

> [!Note]
> <span data-ttu-id="17208-120">Если у приложения есть почтовое приложение или модуль обмена сообщениями, значки также будут включены в регистрацию службы Microsoft Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="17208-120">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

### <a name="color-icon"></a><span data-ttu-id="17208-121">Значок цвета</span><span class="sxs-lookup"><span data-stu-id="17208-121">Color icon</span></span>

<span data-ttu-id="17208-122">Цветовая версия значка отображается в большинстве сценариев Teams и должна быть 192x192 пикселями.</span><span class="sxs-lookup"><span data-stu-id="17208-122">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="17208-123">Символ значка (96x96 пикселей) может быть любым цветом или цветом, но должен размещаться на сплошном или полностью прозрачном квадратном фоне.</span><span class="sxs-lookup"><span data-stu-id="17208-123">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="17208-124">Команды автоматически обрезает значок, чтобы отобразить квадрат со скругленными углами в нескольких сценариях, и фигуру шестиугольника в сценариях Bot.</span><span class="sxs-lookup"><span data-stu-id="17208-124">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="17208-125">Включите 48 точек заполнения вокруг символа, чтобы эти кадрирования можно было создавать без потери сведений.</span><span class="sxs-lookup"><span data-stu-id="17208-125">Include 48 pixels of padding around your symbol so these crops can be made without losing any detail.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Руководство по проектированию цветовой пиктограммы для рабочих групп." border="false":::

### <a name="outline-icon"></a><span data-ttu-id="17208-127">Значок структуры</span><span class="sxs-lookup"><span data-stu-id="17208-127">Outline icon</span></span>

<span data-ttu-id="17208-128">Значок структуры отображается в двух сценариях:</span><span class="sxs-lookup"><span data-stu-id="17208-128">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="17208-129">Когда ваше приложение используется и "поднято" на панели приложений слева от Teams.</span><span class="sxs-lookup"><span data-stu-id="17208-129">When your app is in use and “hoisted” on the app bar on the left of Teams.</span></span>
* <span data-ttu-id="17208-130">Когда пользователь закрепляет расширение обмена сообщениями приложения.</span><span class="sxs-lookup"><span data-stu-id="17208-130">when a user pins your app's messaging extension.</span></span>

<span data-ttu-id="17208-131">Значок должен быть 32x32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="17208-131">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="17208-132">Он может быть белым с прозрачным фоном или прозрачным для белого фона (другие цвета не разрешены).</span><span class="sxs-lookup"><span data-stu-id="17208-132">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="17208-133">Значок структуры не должен содержать лишних внутренних полей вокруг символа.</span><span class="sxs-lookup"><span data-stu-id="17208-133">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Руководство по проектированию цветовой пиктограммы для рабочих групп." border="false":::

### <a name="best-practices"></a><span data-ttu-id="17208-135">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="17208-135">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Иллюстрация, в которой показано, как проектировать значки приложений." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="17208-137">Do: следуйте рекомендациям относительного значка структуры</span><span class="sxs-lookup"><span data-stu-id="17208-137">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="17208-138">Значения RGB белого цвета, используемого в значке, должны иметь красный цвет: 255, зеленый: 255, синий: 255.</span><span class="sxs-lookup"><span data-stu-id="17208-138">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="17208-139">Все остальные части значка структуры должны быть полностью прозрачными, при этом для альфа-канала устанавливается значение 0.</span><span class="sxs-lookup"><span data-stu-id="17208-139">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Иллюстрация, на которой показано, как не разрабатывать значки приложений." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="17208-141">Не: обрезать фигуру с квадратом и круглым квадратом</span><span class="sxs-lookup"><span data-stu-id="17208-141">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="17208-142">Цветовой значок, отправленный в пакете приложения, должен быть квадратным.</span><span class="sxs-lookup"><span data-stu-id="17208-142">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="17208-143">Не округляйте углы значка.</span><span class="sxs-lookup"><span data-stu-id="17208-143">Don’t round the corners of your icon.</span></span> <span data-ttu-id="17208-144">Teams автоматически настраивает радиус преломления.</span><span class="sxs-lookup"><span data-stu-id="17208-144">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

### <a name="examples"></a><span data-ttu-id="17208-145">Примеры</span><span class="sxs-lookup"><span data-stu-id="17208-145">Examples</span></span>

<span data-ttu-id="17208-146">Вот как значки приложений отображаются в различных возможностях и контекстах Teams.</span><span class="sxs-lookup"><span data-stu-id="17208-146">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="17208-147">Личное приложение</span><span class="sxs-lookup"><span data-stu-id="17208-147">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Пример, в котором показано, как выглядит значок приложения в личном приложении." border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="17208-149">Bot (канал)</span><span class="sxs-lookup"><span data-stu-id="17208-149">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Пример, в котором показано, как выглядит значок приложения на канале Bot в канале." border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="17208-151">Расширение системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="17208-151">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<замещающий текст>" border="false":::
