---
title: Справочные материалы по схеме JSON файла локализации
description: Описывает схему локализации, поддерживаемую файлом локализации для Microsoft Teams.
keywords: Локализация схемы манифеста Teams
ms.date: 05/20/2019
ms.openlocfilehash: 1a800ad514633455da8f4fb116e2a55c46cd39c7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675444"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="3f386-104">Ссылка: Схема файла локализации JSON</span><span class="sxs-lookup"><span data-stu-id="3f386-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="3f386-105">Файл локализации Microsoft Teams описывает переводы языка, которые будут обрабатываться в соответствии с языковыми параметрами клиента.</span><span class="sxs-lookup"><span data-stu-id="3f386-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="3f386-106">Файл должен соответствовать схеме, размещенной на сайте [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json).</span><span class="sxs-lookup"><span data-stu-id="3f386-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="3f386-107">Дополнительные сведения см. в разделе [локализация приложений](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="3f386-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="3f386-108">Пример</span><span class="sxs-lookup"><span data-stu-id="3f386-108">Sample</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
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

<span data-ttu-id="3f386-109">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="3f386-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="3f386-110">$schema</span><span class="sxs-lookup"><span data-stu-id="3f386-110">$schema</span></span>

<span data-ttu-id="3f386-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="3f386-111">**URI**</span></span>

<span data-ttu-id="3f386-112">URL-адрес https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="3f386-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="3f386-113">Укажите схему в начале манифеста, чтобы включить поддержку IntelliSense или аналогичную поддержку в редакторе кода:`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="3f386-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="3f386-114">Name. Short</span><span class="sxs-lookup"><span data-stu-id="3f386-114">name.short</span></span>

<span data-ttu-id="3f386-115">**Строка, максимальная длина — 30**</span><span class="sxs-lookup"><span data-stu-id="3f386-115">**String, Max Length 30**</span></span>

<span data-ttu-id="3f386-116">Заменяет соответствующую строку из манифеста приложения указанным здесь значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="3f386-117">Name. Full</span><span class="sxs-lookup"><span data-stu-id="3f386-117">name.full</span></span>

<span data-ttu-id="3f386-118">**Строка, максимальная длина 100**</span><span class="sxs-lookup"><span data-stu-id="3f386-118">**String, Max Length 100**</span></span>

<span data-ttu-id="3f386-119">Заменяет соответствующую строку из манифеста приложения указанным здесь значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="3f386-120">Description. Short</span><span class="sxs-lookup"><span data-stu-id="3f386-120">description.short</span></span>

<span data-ttu-id="3f386-121">**Строка, максимальная длина 80**</span><span class="sxs-lookup"><span data-stu-id="3f386-121">**String, Max Length 80**</span></span>

<span data-ttu-id="3f386-122">Заменяет соответствующую строку из манифеста приложения указанным здесь значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="3f386-123">Description. Full</span><span class="sxs-lookup"><span data-stu-id="3f386-123">description.full</span></span>

<span data-ttu-id="3f386-124">**Строка, максимальная длина 4000**</span><span class="sxs-lookup"><span data-stu-id="3f386-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="3f386-125">Заменяет соответствующую строку из манифеста приложения указанным здесь значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="3f386-126">статиктабс\\[([0-9] | 1 [0-5])\\]\\. Name</span><span class="sxs-lookup"><span data-stu-id="3f386-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="3f386-127">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="3f386-127">**String, Max Length 128**</span></span>

<span data-ttu-id="3f386-128">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="3f386-129">Боты\\[0\\]\\. коммандлистс\\[[0-2]\\]\\. Commands\\[[0-9\\]\\]. Title</span><span class="sxs-lookup"><span data-stu-id="3f386-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="3f386-130">**Строка, максимальная длина 32**</span><span class="sxs-lookup"><span data-stu-id="3f386-130">**String, Max Length 32**</span></span>

<span data-ttu-id="3f386-131">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="3f386-132">Боты\\[0\\]\\. коммандлистс\\[[0-2]\\]\\. Commands\\[[0-9\\]\\]. Description</span><span class="sxs-lookup"><span data-stu-id="3f386-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="3f386-133">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="3f386-133">**String, Max Length 128**</span></span>

<span data-ttu-id="3f386-134">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="3f386-135">компосикстенсионс\\[0\\]\\. Commands\\[[0-9\\]\\]. Title</span><span class="sxs-lookup"><span data-stu-id="3f386-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="3f386-136">**Строка, максимальная длина 32**</span><span class="sxs-lookup"><span data-stu-id="3f386-136">**String, Max Length 32**</span></span>

<span data-ttu-id="3f386-137">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="3f386-138">компосикстенсионс\\[0\\]\\. Commands\\[[0-9\\]\\]. Description</span><span class="sxs-lookup"><span data-stu-id="3f386-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="3f386-139">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="3f386-139">**String, Max Length 128**</span></span>

<span data-ttu-id="3f386-140">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="3f386-141">компосикстенсионс\\[0\\]\\. Commands\\[[0-9\\]\\].\\Parameters [[0-4\\]\\]. Title</span><span class="sxs-lookup"><span data-stu-id="3f386-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="3f386-142">**Строка, максимальная длина 32**</span><span class="sxs-lookup"><span data-stu-id="3f386-142">**String, Max Length 32**</span></span>

<span data-ttu-id="3f386-143">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="3f386-144">компосикстенсионс\\[0\\]\\. Commands\\[[0-9\\]\\].\\Parameters [[0-4\\]\\]. Description</span><span class="sxs-lookup"><span data-stu-id="3f386-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="3f386-145">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="3f386-145">**String, Max Length 128**</span></span>

<span data-ttu-id="3f386-146">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="3f386-147">компосикстенсионс\\[0\\]\\. Commands\\[[0-9\\]\\].\\Parameters [[0-4\\]\\]. Value</span><span class="sxs-lookup"><span data-stu-id="3f386-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="3f386-148">**Строка, максимальная длина 512**</span><span class="sxs-lookup"><span data-stu-id="3f386-148">**String, Max Length 512**</span></span>

<span data-ttu-id="3f386-149">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="3f386-150">компосикстенсионс\\[0\\]\\. Commands\\[[0-9\\]\\].\\Parameters [[0-4\\]\\].\\варианты [[0-9\\]\\]. Title</span><span class="sxs-lookup"><span data-stu-id="3f386-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="3f386-151">**Строка, максимальная длина 128**</span><span class="sxs-lookup"><span data-stu-id="3f386-151">**String, Max Length 128**</span></span>

<span data-ttu-id="3f386-152">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="3f386-153">компосикстенсионс\\[0\\]\\. Commands\\[[0-9\\]\\].\\таскинфо. Title</span><span class="sxs-lookup"><span data-stu-id="3f386-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="3f386-154">**Строка, максимальная длина 64**</span><span class="sxs-lookup"><span data-stu-id="3f386-154">**String, Max Length 64**</span></span>

<span data-ttu-id="3f386-155">Заменяет соответствующие строки в манифесте приложения указанным значением.</span><span class="sxs-lookup"><span data-stu-id="3f386-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>