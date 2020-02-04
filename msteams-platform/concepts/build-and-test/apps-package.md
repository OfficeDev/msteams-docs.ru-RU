---
title: Упаковка приложения
description: Узнайте, как упаковать приложение для тестирования, отправки и публикации в Microsoft Teams.
keywords: Упаковка приложений Teams
ms.topic: conceptual
ms.openlocfilehash: b76041b129e766dba2b401aaac0e12958a4e9b0d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675537"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="80e4b-104">Создание пакета приложений для приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="80e4b-104">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="80e4b-105">Приложения в Teams определяются с помощью JSON манифеста приложения и упаковываются в пакет приложения со своими значками.</span><span class="sxs-lookup"><span data-stu-id="80e4b-105">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="80e4b-106">Вам потребуется пакет приложения для отправки и установки приложения в Teams, а также для публикации в каталоге бизнес-приложений или в AppSource.</span><span class="sxs-lookup"><span data-stu-id="80e4b-106">You'll need an app package to upload and install your app in Teams, and to publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="80e4b-107">Пакет приложения Teams — это ZIP-файл со следующими разделом:</span><span class="sxs-lookup"><span data-stu-id="80e4b-107">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="80e4b-108">Файл манифеста с именем manifest. JSON, задающий атрибуты приложения и указывающий на необходимые ресурсы для вашего интерфейса, такие как расположение страницы настройки вкладки или идентификатор приложения Microsoft для ленты.</span><span class="sxs-lookup"><span data-stu-id="80e4b-108">A manifest file named "manifest.json", which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="80e4b-109">Прозрачный значок "контур" и полный значок "цвет".</span><span class="sxs-lookup"><span data-stu-id="80e4b-109">A transparent "outline" icon and a full "color" icon.</span></span> <span data-ttu-id="80e4b-110">Для получения дополнительных сведений просмотрите [значки](#icons) , приведенные далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="80e4b-110">See [Icons](#icons) later in this topic for more information.</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="80e4b-111">Создание манифеста</span><span class="sxs-lookup"><span data-stu-id="80e4b-111">Creating a manifest</span></span>

<span data-ttu-id="80e4b-112">*Приложение Teams Studio* помогает настроить манифест.</span><span class="sxs-lookup"><span data-stu-id="80e4b-112">*Teams App Studio* can help configure your manifest.</span></span> <span data-ttu-id="80e4b-113">Кроме того, она содержит библиотеку элементов управления реагируем и настраиваемые примеры для карточек.</span><span class="sxs-lookup"><span data-stu-id="80e4b-113">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="80e4b-114">Ознакомьтесь с [обзором App Studio](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="80e4b-114">See [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="80e4b-115">Файл манифеста должен иметь имя manifest. JSON и находиться на верхнем уровне пакета отправки.</span><span class="sxs-lookup"><span data-stu-id="80e4b-115">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="80e4b-116">Обратите внимание, что манифесты и пакеты, созданные ранее, могут поддерживать более старую версию схемы.</span><span class="sxs-lookup"><span data-stu-id="80e4b-116">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="80e4b-117">Для приложений Teams, особенно отправок AppSource (прежнее хранилище Office), необходимо использовать текущую [схему манифеста](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="80e4b-117">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="80e4b-118">Укажите схему в начале манифеста, чтобы включить поддержку IntelliSense или аналогичную поддержку в редакторе кода:</span><span class="sxs-lookup"><span data-stu-id="80e4b-118">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`

## <a name="icons"></a><span data-ttu-id="80e4b-119">Значки</span><span class="sxs-lookup"><span data-stu-id="80e4b-119">Icons</span></span>

> [!Note]
> <span data-ttu-id="80e4b-120">Если приложение содержит почтовое расширение или почтовое приложение, используются значки, которые передаются в регистрацию Bot в среде Bot.</span><span class="sxs-lookup"><span data-stu-id="80e4b-120">If your app contains a bot or messaging extension, the icons used will be the icons uploaded to your bot registration in the Bot Framework.</span></span>

<span data-ttu-id="80e4b-121">Microsoft Teams требует два значка для своего приложения, чтобы их можно было использовать в рамках продукта.</span><span class="sxs-lookup"><span data-stu-id="80e4b-121">Microsoft Teams requires two icons for your app experience, to be used within the product.</span></span> <span data-ttu-id="80e4b-122">Значки должны быть включены в пакет и ссылаться на них с помощью относительных путей в манифесте.</span><span class="sxs-lookup"><span data-stu-id="80e4b-122">Icons must be included in the package and referenced via relative paths in the manifest.</span></span> <span data-ttu-id="80e4b-123">Максимальная длина каждого пути составляет 2048 байт, а формат значка —. png.</span><span class="sxs-lookup"><span data-stu-id="80e4b-123">The maximum length of each path is 2048 bytes, and the format of the icon is .png.</span></span>

### <a name="color"></a><span data-ttu-id="80e4b-124">color</span><span class="sxs-lookup"><span data-stu-id="80e4b-124">color</span></span>

<span data-ttu-id="80e4b-125">`color` Значок используется во всех Microsoft Teams (в галереях приложений и вкладок, Боты, всплывающих меню и т. д.).</span><span class="sxs-lookup"><span data-stu-id="80e4b-125">The `color` icon is used throughout Microsoft Teams (in app and tab galleries, bots, flyouts, and so on).</span></span> <span data-ttu-id="80e4b-126">Этот значок должен быть 192x192 пикселями.</span><span class="sxs-lookup"><span data-stu-id="80e4b-126">This icon should be 192x192 pixels.</span></span> <span data-ttu-id="80e4b-127">Ваш значок может быть любым цветом (или цветом), но фоном должен быть контрастный цвет.</span><span class="sxs-lookup"><span data-stu-id="80e4b-127">Your icon can be any color (or colors), but the background should be your branded accent color.</span></span> <span data-ttu-id="80e4b-128">Кроме того, он должен иметь небольшое количество заполнений, окружающих значок, чтобы вместить шестиугольники в виде шестиугольника для повернутой версии значка.</span><span class="sxs-lookup"><span data-stu-id="80e4b-128">It should also have a small amount of padding surrounding the icon to accommodate the hexagonal cropping for the bot version of the icon.</span></span>

### <a name="outline"></a><span data-ttu-id="80e4b-129">outline</span><span class="sxs-lookup"><span data-stu-id="80e4b-129">outline</span></span>

<span data-ttu-id="80e4b-130">Этот `outline` значок используется в следующих местах: панели приложений и расширения обмена сообщениями, помеченные пользователем как "Избранное".</span><span class="sxs-lookup"><span data-stu-id="80e4b-130">The `outline` icon is used in these places: the app bar and messaging extensions the user has marked as a "favorite."</span></span> <span data-ttu-id="80e4b-131">Этот значок должен быть 32x32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="80e4b-131">This icon must be 32x32 pixels.</span></span> <span data-ttu-id="80e4b-132">Значок структуры должен содержать только белый цвет и прозрачность (без других цветов).</span><span class="sxs-lookup"><span data-stu-id="80e4b-132">Your outline icon must contain only white and transparency (no other colors).</span></span> <span data-ttu-id="80e4b-133">Значок может быть белым с прозрачным фоном или прозрачным для белого фона.</span><span class="sxs-lookup"><span data-stu-id="80e4b-133">The icon can be white with transparent background or transparent with a white background.</span></span> <span data-ttu-id="80e4b-134">Значок структуры не должен содержать дополнительные внутренние поля, окружающие значок, и должен быть обрезаться по мере возможности, при этом сохраняя размеры 32x32.</span><span class="sxs-lookup"><span data-stu-id="80e4b-134">The outline icon should not have extra padding surrounding the icon and should be as tightly cropped as possible while still maintaining the 32x32 dimensions.</span></span> <span data-ttu-id="80e4b-135">Вот несколько хороших примеров:</span><span class="sxs-lookup"><span data-stu-id="80e4b-135">Here are a few good examples:</span></span>

![Пример значков структуры](~/assets/images/icons/sample20x20s.png)

<span data-ttu-id="80e4b-137">Например, предположим, что ваша компания — Contoso.</span><span class="sxs-lookup"><span data-stu-id="80e4b-137">For example, say your company is Contoso.</span></span> <span data-ttu-id="80e4b-138">Вы отправите два значка:</span><span class="sxs-lookup"><span data-stu-id="80e4b-138">You'd submit two icons:</span></span>

![Демонстрация значков](~/assets/images/framework/framework_submit_icon.png)

<span data-ttu-id="80e4b-140">Ниже показано, как будут выглядеть значки в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="80e4b-140">Here's how the icons would appear in the UI:</span></span>

#### <a name="bot-and-chiclet-in-channel-view"></a><span data-ttu-id="80e4b-141">Bot и чиклет в представлении канала</span><span class="sxs-lookup"><span data-stu-id="80e4b-141">Bot and chiclet in Channel view</span></span>

![Интерфейс Bot и чиклет](~/assets/images/icons/botandchiclet.png)

#### <a name="flyout"></a><span data-ttu-id="80e4b-143">Всплывающих</span><span class="sxs-lookup"><span data-stu-id="80e4b-143">Flyout</span></span>

![Примеры значков contoso](~/assets/images/icons/flyout.png)

#### <a name="app-bar-and-home-screen"></a><span data-ttu-id="80e4b-145">Панель приложений и начальный экран</span><span class="sxs-lookup"><span data-stu-id="80e4b-145">App bar and home screen</span></span>

![Примеры значков contoso](~/assets/images/icons/appbarhomescreen.png)