---
title: Ссылка на схему JSON файла локализации
description: Описывает схему локализации, поддерживаемую файлом локализации для Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: группы проявляют локализацию схемы
ms.date: 05/20/2019
ms.openlocfilehash: 3e4207fb3e862eac18c80ffc49e7c5648ae05c28
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019708"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="4a78c-104">Справка: схема JSON-файла локализации</span><span class="sxs-lookup"><span data-stu-id="4a78c-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="4a78c-105">В файле локализации Microsoft Teams описываются языковые переводы, которые будут поданы в зависимости от параметров языка клиента.</span><span class="sxs-lookup"><span data-stu-id="4a78c-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="4a78c-106">Файл должен соответствовать схеме, которая была на уровне [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="4a78c-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="4a78c-107">Дополнительные сведения см. [в сведениях о локализации приложений.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="4a78c-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="4a78c-108">Пример</span><span class="sxs-lookup"><span data-stu-id="4a78c-108">Sample</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "name.short": "Le App Studio",
  "name.full": "App Studio pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App Studio.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App Studio.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

<span data-ttu-id="4a78c-109">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="4a78c-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="4a78c-110">$schema</span><span class="sxs-lookup"><span data-stu-id="4a78c-110">$schema</span></span>

<span data-ttu-id="4a78c-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="4a78c-111">**URI**</span></span>

<span data-ttu-id="4a78c-112">URL https:// ссылки на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="4a78c-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="4a78c-113">Укажите схему в начале манифеста, чтобы включить IntelliSense или аналогичную поддержку редактора кода: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="4a78c-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="4a78c-114">name.short</span><span class="sxs-lookup"><span data-stu-id="4a78c-114">name.short</span></span>

<span data-ttu-id="4a78c-115">**String, Max Length 30**</span><span class="sxs-lookup"><span data-stu-id="4a78c-115">**String, Max Length 30**</span></span>

<span data-ttu-id="4a78c-116">Заменяет соответствующую строку из манифеста приложения значением, которое здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="4a78c-117">name.full</span><span class="sxs-lookup"><span data-stu-id="4a78c-117">name.full</span></span>

<span data-ttu-id="4a78c-118">**String, Max Length 100**</span><span class="sxs-lookup"><span data-stu-id="4a78c-118">**String, Max Length 100**</span></span>

<span data-ttu-id="4a78c-119">Заменяет соответствующую строку из манифеста приложения значением, которое здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="4a78c-120">description.short</span><span class="sxs-lookup"><span data-stu-id="4a78c-120">description.short</span></span>

<span data-ttu-id="4a78c-121">**String, Max Length 80**</span><span class="sxs-lookup"><span data-stu-id="4a78c-121">**String, Max Length 80**</span></span>

<span data-ttu-id="4a78c-122">Заменяет соответствующую строку из манифеста приложения значением, которое здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="4a78c-123">description.full</span><span class="sxs-lookup"><span data-stu-id="4a78c-123">description.full</span></span>

<span data-ttu-id="4a78c-124">**String, Max Length 4000**</span><span class="sxs-lookup"><span data-stu-id="4a78c-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="4a78c-125">Заменяет соответствующую строку из манифеста приложения значением, которое здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="4a78c-126">staticTabs \\ [[[0-9]|1[0-5]] \\ ] \\ .name</span><span class="sxs-lookup"><span data-stu-id="4a78c-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="4a78c-127">**String, Max Length 128**</span><span class="sxs-lookup"><span data-stu-id="4a78c-127">**String, Max Length 128**</span></span>

<span data-ttu-id="4a78c-128">Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="4a78c-129">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ ].title</span><span class="sxs-lookup"><span data-stu-id="4a78c-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="4a78c-130">**String, Max Length 32**</span><span class="sxs-lookup"><span data-stu-id="4a78c-130">**String, Max Length 32**</span></span>

<span data-ttu-id="4a78c-131">Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="4a78c-132">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="4a78c-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="4a78c-133">**String, Max Length 128**</span><span class="sxs-lookup"><span data-stu-id="4a78c-133">**String, Max Length 128**</span></span>

<span data-ttu-id="4a78c-134">Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="4a78c-135">composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="4a78c-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="4a78c-136">**String, Max Length 32**</span><span class="sxs-lookup"><span data-stu-id="4a78c-136">**String, Max Length 32**</span></span>

<span data-ttu-id="4a78c-137">Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="4a78c-138">composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="4a78c-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="4a78c-139">**String, Max Length 128**</span><span class="sxs-lookup"><span data-stu-id="4a78c-139">**String, Max Length 128**</span></span>

<span data-ttu-id="4a78c-140">Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="4a78c-141">composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="4a78c-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="4a78c-142">**String, Max Length 32**</span><span class="sxs-lookup"><span data-stu-id="4a78c-142">**String, Max Length 32**</span></span>

<span data-ttu-id="4a78c-143">Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="4a78c-144">composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="4a78c-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="4a78c-145">**String, Max Length 128**</span><span class="sxs-lookup"><span data-stu-id="4a78c-145">**String, Max Length 128**</span></span>

<span data-ttu-id="4a78c-146">Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="4a78c-147">composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value</span><span class="sxs-lookup"><span data-stu-id="4a78c-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="4a78c-148">**String, Max Length 512**</span><span class="sxs-lookup"><span data-stu-id="4a78c-148">**String, Max Length 512**</span></span>

<span data-ttu-id="4a78c-149">Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="4a78c-150">composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ ].parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="4a78c-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="4a78c-151">**String, Max Length 128**</span><span class="sxs-lookup"><span data-stu-id="4a78c-151">**String, Max Length 128**</span></span>

<span data-ttu-id="4a78c-152">Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="4a78c-153">composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title</span><span class="sxs-lookup"><span data-stu-id="4a78c-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="4a78c-154">**String, Max Length 64**</span><span class="sxs-lookup"><span data-stu-id="4a78c-154">**String, Max Length 64**</span></span>

<span data-ttu-id="4a78c-155">Заменяет соответствующую строку (ы) из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="4a78c-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
