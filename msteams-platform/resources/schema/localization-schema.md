---
title: Справка по схеме JSON файла локализации
description: Описывает схему локализации, поддерживаемую файлом локализации для Microsoft Teams
ms.topic: reference
keywords: Локализация схемы манифеста teams
ms.date: 05/20/2019
ms.openlocfilehash: 696a65de70a63e767f8fcdb040364fe90cde8716
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014602"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="8c6e7-104">Справка: схема JSON файла локализации</span><span class="sxs-lookup"><span data-stu-id="8c6e7-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="8c6e7-105">В файле локализации Microsoft Teams описываются переводы языков, которые будут обслуживаться на основе языковых параметров клиента.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="8c6e7-106">Файл должен соответствовать схеме, хранящейся в [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) папке .</span><span class="sxs-lookup"><span data-stu-id="8c6e7-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="8c6e7-107">Дополнительные сведения [см. в локализации приложения.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="8c6e7-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="8c6e7-108">Пример</span><span class="sxs-lookup"><span data-stu-id="8c6e7-108">Sample</span></span>

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

<span data-ttu-id="8c6e7-109">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="8c6e7-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="8c6e7-110">$schema</span><span class="sxs-lookup"><span data-stu-id="8c6e7-110">$schema</span></span>

<span data-ttu-id="8c6e7-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-111">**URI**</span></span>

<span data-ttu-id="8c6e7-112">URL-https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="8c6e7-113">Укажите схему в начале манифеста, чтобы включить поддержку IntelliSense или аналогичную поддержку из редактора кода: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="8c6e7-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="8c6e7-114">name.short</span><span class="sxs-lookup"><span data-stu-id="8c6e7-114">name.short</span></span>

<span data-ttu-id="8c6e7-115">**Строка, максимальная длина 30**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-115">**String, Max Length 30**</span></span>

<span data-ttu-id="8c6e7-116">Заменяет соответствующую строку из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="8c6e7-117">name.full</span><span class="sxs-lookup"><span data-stu-id="8c6e7-117">name.full</span></span>

<span data-ttu-id="8c6e7-118">**Строка, максимальная длина 100**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-118">**String, Max Length 100**</span></span>

<span data-ttu-id="8c6e7-119">Заменяет соответствующую строку из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="8c6e7-120">description.short</span><span class="sxs-lookup"><span data-stu-id="8c6e7-120">description.short</span></span>

<span data-ttu-id="8c6e7-121">**Строка, максимальная длина 80**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-121">**String, Max Length 80**</span></span>

<span data-ttu-id="8c6e7-122">Заменяет соответствующую строку из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="8c6e7-123">description.full</span><span class="sxs-lookup"><span data-stu-id="8c6e7-123">description.full</span></span>

<span data-ttu-id="8c6e7-124">**Строка, максимальная длина 4000**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="8c6e7-125">Заменяет соответствующую строку из манифеста приложения на значение, предоставленную здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="8c6e7-126">staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name</span><span class="sxs-lookup"><span data-stu-id="8c6e7-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="8c6e7-127">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-127">**String, Max Length 128**</span></span>

<span data-ttu-id="8c6e7-128">Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="8c6e7-129">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ \\ .title</span><span class="sxs-lookup"><span data-stu-id="8c6e7-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="8c6e7-130">**Строка, максимальная длина 32**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-130">**String, Max Length 32**</span></span>

<span data-ttu-id="8c6e7-131">Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="8c6e7-132">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ \\ .description</span><span class="sxs-lookup"><span data-stu-id="8c6e7-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="8c6e7-133">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-133">**String, Max Length 128**</span></span>

<span data-ttu-id="8c6e7-134">Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="8c6e7-135">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="8c6e7-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="8c6e7-136">**Строка, максимальная длина 32**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-136">**String, Max Length 32**</span></span>

<span data-ttu-id="8c6e7-137">Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="8c6e7-138">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="8c6e7-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="8c6e7-139">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-139">**String, Max Length 128**</span></span>

<span data-ttu-id="8c6e7-140">Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="8c6e7-141">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="8c6e7-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="8c6e7-142">**Строка, максимальная длина 32**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-142">**String, Max Length 32**</span></span>

<span data-ttu-id="8c6e7-143">Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="8c6e7-144">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ \\ .description</span><span class="sxs-lookup"><span data-stu-id="8c6e7-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="8c6e7-145">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-145">**String, Max Length 128**</span></span>

<span data-ttu-id="8c6e7-146">Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="8c6e7-147">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ \\ .value</span><span class="sxs-lookup"><span data-stu-id="8c6e7-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="8c6e7-148">**Строка, максимальная длина 512**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-148">**String, Max Length 512**</span></span>

<span data-ttu-id="8c6e7-149">Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="8c6e7-150">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ \\ .title</span><span class="sxs-lookup"><span data-stu-id="8c6e7-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="8c6e7-151">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-151">**String, Max Length 128**</span></span>

<span data-ttu-id="8c6e7-152">Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="8c6e7-153">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title</span><span class="sxs-lookup"><span data-stu-id="8c6e7-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="8c6e7-154">**Строка, максимальная длина 64**</span><span class="sxs-lookup"><span data-stu-id="8c6e7-154">**String, Max Length 64**</span></span>

<span data-ttu-id="8c6e7-155">Заменяет соответствующие строки из манифеста приложения значением, предоставленным здесь.</span><span class="sxs-lookup"><span data-stu-id="8c6e7-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
