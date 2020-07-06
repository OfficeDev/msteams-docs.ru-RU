---
title: Справочные материалы по схеме JSON файла локализации
description: Описывает схему локализации, поддерживаемую файлом локализации для Microsoft Teams.
keywords: Локализация схемы манифеста Teams
ms.date: 05/20/2019
ms.openlocfilehash: 061729ecb5110c99d8f85f144796f1a78b266c3d
ms.sourcegitcommit: bac0226d9048c363d96bbaf6f5395388c5f5c45a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/06/2020
ms.locfileid: "45039281"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="e1465-104">Ссылка: Схема файла локализации JSON</span><span class="sxs-lookup"><span data-stu-id="e1465-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="e1465-105">Файл локализации Microsoft Teams описывает переводы языка, которые будут обрабатываться в соответствии с языковыми параметрами клиента.</span><span class="sxs-lookup"><span data-stu-id="e1465-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="e1465-106">Файл должен соответствовать схеме, размещенной на сайте [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="e1465-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="e1465-107">Дополнительные сведения см. в разделе [локализация приложений](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="e1465-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="e1465-108">Пример</span><span class="sxs-lookup"><span data-stu-id="e1465-108">Sample</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

<span data-ttu-id="e1465-109">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="e1465-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="e1465-110">$schema</span><span class="sxs-lookup"><span data-stu-id="e1465-110">$schema</span></span>

<span data-ttu-id="e1465-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="e1465-111">**URI**</span></span>

<span data-ttu-id="e1465-112">URL-адрес https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="e1465-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="e1465-113">Укажите схему в начале манифеста, чтобы включить поддержку IntelliSense или аналогичную поддержку в редакторе кода:`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="e1465-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="e1465-114">Name. Short</span><span class="sxs-lookup"><span data-stu-id="e1465-114">name.short</span></span>

<span data-ttu-id="e1465-115">**Строка, максимальная длина — 30**</span><span class="sxs-lookup"><span data-stu-id="e1465-115">**String, Max Length 30**</span></span>

<span data-ttu-id="e1465-116">Заменяет соответствующую строку из манифеста приложения указанным здесь значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="e1465-117">Name. Full</span><span class="sxs-lookup"><span data-stu-id="e1465-117">name.full</span></span>

<span data-ttu-id="e1465-118">**Строка, максимальная длина 100**</span><span class="sxs-lookup"><span data-stu-id="e1465-118">**String, Max Length 100**</span></span>

<span data-ttu-id="e1465-119">Заменяет соответствующую строку из манифеста приложения указанным здесь значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="e1465-120">Description. Short</span><span class="sxs-lookup"><span data-stu-id="e1465-120">description.short</span></span>

<span data-ttu-id="e1465-121">**Строка, максимальная длина 80**</span><span class="sxs-lookup"><span data-stu-id="e1465-121">**String, Max Length 80**</span></span>

<span data-ttu-id="e1465-122">Заменяет соответствующую строку из манифеста приложения указанным здесь значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="e1465-123">Description. Full</span><span class="sxs-lookup"><span data-stu-id="e1465-123">description.full</span></span>

<span data-ttu-id="e1465-124">**Строка, максимальная длина 4000**</span><span class="sxs-lookup"><span data-stu-id="e1465-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="e1465-125">Заменяет соответствующую строку из манифеста приложения указанным здесь значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="e1465-126">Статиктабс \\ [([0-9] | 1 [0-5]) \\ ] \\ . Name</span><span class="sxs-lookup"><span data-stu-id="e1465-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="e1465-127">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="e1465-127">**String, Max Length 128**</span></span>

<span data-ttu-id="e1465-128">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="e1465-129">Боты \\ [0 \\ ] \\ . коммандлистс \\ [[0-2] \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . Title</span><span class="sxs-lookup"><span data-stu-id="e1465-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="e1465-130">**Строка, максимальная длина 32**</span><span class="sxs-lookup"><span data-stu-id="e1465-130">**String, Max Length 32**</span></span>

<span data-ttu-id="e1465-131">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="e1465-132">Боты \\ [0 \\ ] \\ . коммандлистс \\ [[0-2] \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . Description</span><span class="sxs-lookup"><span data-stu-id="e1465-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="e1465-133">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="e1465-133">**String, Max Length 128**</span></span>

<span data-ttu-id="e1465-134">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="e1465-135">компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . Title</span><span class="sxs-lookup"><span data-stu-id="e1465-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="e1465-136">**Строка, максимальная длина 32**</span><span class="sxs-lookup"><span data-stu-id="e1465-136">**String, Max Length 32**</span></span>

<span data-ttu-id="e1465-137">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="e1465-138">компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . Description</span><span class="sxs-lookup"><span data-stu-id="e1465-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="e1465-139">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="e1465-139">**String, Max Length 128**</span></span>

<span data-ttu-id="e1465-140">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="e1465-141">компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . Title</span><span class="sxs-lookup"><span data-stu-id="e1465-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="e1465-142">**Строка, максимальная длина 32**</span><span class="sxs-lookup"><span data-stu-id="e1465-142">**String, Max Length 32**</span></span>

<span data-ttu-id="e1465-143">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="e1465-144">компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . Description</span><span class="sxs-lookup"><span data-stu-id="e1465-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="e1465-145">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="e1465-145">**String, Max Length 128**</span></span>

<span data-ttu-id="e1465-146">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="e1465-147">компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . Value</span><span class="sxs-lookup"><span data-stu-id="e1465-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="e1465-148">**Строка, максимальная длина 512**</span><span class="sxs-lookup"><span data-stu-id="e1465-148">**String, Max Length 512**</span></span>

<span data-ttu-id="e1465-149">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="e1465-150">компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . parameters \\ [[0-4]]. варианты [[ \\ \\ \\ 0-9] \\ ] \\ . Title</span><span class="sxs-lookup"><span data-stu-id="e1465-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="e1465-151">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="e1465-151">**String, Max Length 128**</span></span>

<span data-ttu-id="e1465-152">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="e1465-153">компосикстенсионс \\ [0 \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . таскинфо \\ . Title</span><span class="sxs-lookup"><span data-stu-id="e1465-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="e1465-154">**Строка, максимальная длина 64**</span><span class="sxs-lookup"><span data-stu-id="e1465-154">**String, Max Length 64**</span></span>

<span data-ttu-id="e1465-155">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="e1465-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
