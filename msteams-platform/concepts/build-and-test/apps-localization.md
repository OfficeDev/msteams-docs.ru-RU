---
title: Локализация приложения
description: Описывает соображения по локализации Microsoft Teams приложения.
ms.topic: conceptual
localization_priority: Normal
keywords: команды публикуют язык локализации AppSource в офисе магазина
ms.date: 05/15/2018
ms.openlocfilehash: c73188bb24960b9ef0706955d09d23b618c04e5c
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140042"
---
# <a name="localize-your-app"></a><span data-ttu-id="c5315-104">Локализация приложения</span><span class="sxs-lookup"><span data-stu-id="c5315-104">Localize your app</span></span>

<span data-ttu-id="c5315-105">Чтобы локализовать ваше Microsoft Teams, необходимо учитывать следующие факторы:</span><span class="sxs-lookup"><span data-stu-id="c5315-105">You must consider the following factors to localize your Microsoft Teams app:</span></span>

1. <span data-ttu-id="c5315-106">[Локализовать список AppSource.](#localize-your-appsource-listing)</span><span class="sxs-lookup"><span data-stu-id="c5315-106">[Localize your AppSource listing](#localize-your-appsource-listing).</span></span>
1. <span data-ttu-id="c5315-107">[Локализовать строки в манифесте приложения.](#localize-strings-in-your-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="c5315-107">[Localize strings in your app manifest](#localize-strings-in-your-app-manifest).</span></span> 
1. <span data-ttu-id="c5315-108">[Обработка локализованных текстовых сообщений от пользователей.](#handle-localized-text-submissions-from-your-users)</span><span class="sxs-lookup"><span data-stu-id="c5315-108">[Handle localized text submissions from your users](#handle-localized-text-submissions-from-your-users).</span></span>

## <a name="localize-your-appsource-listing"></a><span data-ttu-id="c5315-109">Локализация списка AppSource</span><span class="sxs-lookup"><span data-stu-id="c5315-109">Localize your AppSource listing</span></span>

<span data-ttu-id="c5315-110">Если вы публикуете приложение в магазине, вы должны знать, что локализация списка AppSource еще не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c5315-110">If you are publishing the app to the store, you must be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="c5315-111">Чтобы поддерживать локализованные списки в магазине приложений, в список можно добавить дополнительные языки.</span><span class="sxs-lookup"><span data-stu-id="c5315-111">To support localized listings in the app store, you can add additional languages to your listing.</span></span> <span data-ttu-id="c5315-112">Языковые сведения по умолчанию, которые вы предоставляете в [Центре партнеров](/office/dev/store/submit-to-appsource-via-partner-center) для вашего списка, появляются в списке веб-сайта [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="c5315-112">The default language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing appears in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span> <span data-ttu-id="c5315-113">В настоящее время языком по умолчанию является английский.</span><span class="sxs-lookup"><span data-stu-id="c5315-113">Currently, the default language is English.</span></span>

### <a name="configure-localization"></a><span data-ttu-id="c5315-114">Настройка локализации</span><span class="sxs-lookup"><span data-stu-id="c5315-114">Configure localization</span></span>

<span data-ttu-id="c5315-115">Чтобы настроить дополнительный язык для приложения, в [Центре](/office/dev/store/submit-to-appsource-via-partner-center)партнеров выберите английский и дополнительный язык приложения.</span><span class="sxs-lookup"><span data-stu-id="c5315-115">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="c5315-116">Французский язык используется в качестве дополнительного языка в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="c5315-116">French is used as an additional language in the following example:</span></span>

1. <span data-ttu-id="c5315-117">Добавление английского языка</span><span class="sxs-lookup"><span data-stu-id="c5315-117">Add English language</span></span>
    * <span data-ttu-id="c5315-118">Введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="c5315-118">Enter the app name.</span></span>
    * <span data-ttu-id="c5315-119">Введите краткое описание приложения на английском языке.</span><span class="sxs-lookup"><span data-stu-id="c5315-119">Enter a short description of the app in English.</span></span>
    * <span data-ttu-id="c5315-120">Введите длинное описание приложения на английском языке.</span><span class="sxs-lookup"><span data-stu-id="c5315-120">Enter the long description of the app in English.</span></span>
    * <span data-ttu-id="c5315-121">В длинном описании введите: **Это приложение доступно на французском языке.**</span><span class="sxs-lookup"><span data-stu-id="c5315-121">In the long description, enter: **This app is available in French**.</span></span>
    * <span data-ttu-id="c5315-122">Upload изображения пользовательского интерфейса приложения (на английском языке).</span><span class="sxs-lookup"><span data-stu-id="c5315-122">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="c5315-123">Добавление французского языка</span><span class="sxs-lookup"><span data-stu-id="c5315-123">Add French language</span></span>
    * <span data-ttu-id="c5315-124">Введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="c5315-124">Enter the app name.</span></span>
    * <span data-ttu-id="c5315-125">Введите краткое описание приложения на французском языке.</span><span class="sxs-lookup"><span data-stu-id="c5315-125">Enter a short description of the app in French.</span></span>
    * <span data-ttu-id="c5315-126">Введите длинное описание приложения на французском языке.</span><span class="sxs-lookup"><span data-stu-id="c5315-126">Enter the long description of the app in French.</span></span>
    * <span data-ttu-id="c5315-127">Upload изображения пользовательского интерфейса приложения (на французском языке).</span><span class="sxs-lookup"><span data-stu-id="c5315-127">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="c5315-128">Изображения, которые вы загружаете на английском языке, используются в AppSource.</span><span class="sxs-lookup"><span data-stu-id="c5315-128">The images that you upload with the English language are used in AppSource.</span></span>

## <a name="localize-strings-in-your-app-manifest"></a><span data-ttu-id="c5315-129">Локализация строк в манифесте приложения</span><span class="sxs-lookup"><span data-stu-id="c5315-129">Localize strings in your app manifest</span></span>

<span data-ttu-id="c5315-130">Необходимо использовать схему Microsoft Teams, а затем `v1.5` локализовать приложение.</span><span class="sxs-lookup"><span data-stu-id="c5315-130">You must use the Microsoft Teams app schema `v1.5` and later to localize your app.</span></span> <span data-ttu-id="c5315-131">Это можно сделать, установив атрибут в файле manifest.jsили выше и обновив свойство до `$schema` **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** версии `manifestVersion` `$schema` `1.5` (в данном случае).</span><span class="sxs-lookup"><span data-stu-id="c5315-131">You can do this by setting the `$schema` attribute in your manifest.json file to **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** or higher and updating the `manifestVersion` property to `$schema` version (`1.5` in this case).</span></span> 

<span data-ttu-id="c5315-132">Необходимо добавить свойство с языком по `localizationInfo` умолчанию, который поддерживает приложение.</span><span class="sxs-lookup"><span data-stu-id="c5315-132">You must add the `localizationInfo` property with the default language that your application supports.</span></span> <span data-ttu-id="c5315-133">Язык по умолчанию используется в качестве конечного языка отката, если параметры клиента пользователя не совпадают ни с одним из дополнительных языков.</span><span class="sxs-lookup"><span data-stu-id="c5315-133">The default language is used as the final fallback language if the user's client settings do not match with any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="c5315-134">Пример manifest.jsизменения</span><span class="sxs-lookup"><span data-stu-id="c5315-134">Example manifest.json change</span></span>

<span data-ttu-id="c5315-135">Следующие manifest.jsпомогают добавить свойство с языком по умолчанию, который поддерживает ваше приложение вместе `localizationInfo` `additionalLanguages` с:</span><span class="sxs-lookup"><span data-stu-id="c5315-135">The following manifest.json helps to add the `localizationInfo` property with the default language that your application supports along with `additionalLanguages`:</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "localizationInfo": {
        "defaultLanguageTag": "en",
        "additionalLanguages": [
            {
                "languageTag": "es-mx",
                "file": "es-mx.json"
            }
        ]
    }
  ...
}
```

### <a name="example-localization-json-change"></a><span data-ttu-id="c5315-136">Пример изменения локализации .json</span><span class="sxs-lookup"><span data-stu-id="c5315-136">Example localization .json change</span></span>

<span data-ttu-id="c5315-137">Ниже приводится пример локализации .json:</span><span class="sxs-lookup"><span data-stu-id="c5315-137">Following is an example for localization .json:</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```


<span data-ttu-id="c5315-138">Вы можете предоставить дополнительные файлы json с переводами всех строк пользователя, стоящих перед вами в манифесте.</span><span class="sxs-lookup"><span data-stu-id="c5315-138">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="c5315-139">Эти файлы должны соответствовать схеме [JSON-файла](../../resources/schema/localization-schema.md) локализации, и они должны быть добавлены в свойство `localizationInfo` манифеста.</span><span class="sxs-lookup"><span data-stu-id="c5315-139">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the `localizationInfo` property of your manifest.</span></span> <span data-ttu-id="c5315-140">Каждый файл соотносится с языковым тегом, который Teams клиент использует для выбора соответствующих строк.</span><span class="sxs-lookup"><span data-stu-id="c5315-140">Each file correlates to a language tag, which the Teams client uses to select the appropriate strings.</span></span> <span data-ttu-id="c5315-141">Тег языка принимает форму, но вы можете опустить часть для всех регионов, поддерживаюных `<language>-<region>` `<region>` нужный язык.</span><span class="sxs-lookup"><span data-stu-id="c5315-141">The language tag takes the form of `<language>-<region>` but you can omit the `<region>` portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="c5315-142">Клиент Teams применяет строки в следующем порядке: языковые строки по умолчанию —> языка пользователя только строки -> языка пользователя + строки области пользователя.</span><span class="sxs-lookup"><span data-stu-id="c5315-142">The Teams client applies the strings in the following order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="c5315-143">Например, по умолчанию вы предоставляете язык "fr" (французский язык, все регионы) и дополнительные языковые файлы для "en" (английский, все регионы) и "en-GB" (английский, Великобритания), язык пользователя установлен на "en-GB".</span><span class="sxs-lookup"><span data-stu-id="c5315-143">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain), the user's language is set to 'en-gb'.</span></span> <span data-ttu-id="c5315-144">Следующие изменения происходят в зависимости от выбора языка:</span><span class="sxs-lookup"><span data-stu-id="c5315-144">The following changes take place based on the language selection:</span></span>

1. <span data-ttu-id="c5315-145">Клиент Teams берет строки "fr" и переописывает их строками "en".</span><span class="sxs-lookup"><span data-stu-id="c5315-145">The Teams client takes the 'fr' strings and overwrite them with the 'en' strings.</span></span>
1. <span data-ttu-id="c5315-146">Переопиши строки "en" со строками "en-GB".</span><span class="sxs-lookup"><span data-stu-id="c5315-146">Overwrite the 'en' strings with the 'en-gb' strings.</span></span>

<span data-ttu-id="c5315-147">Если язык пользователя настроен на "en-ca", в зависимости от выбора языка происходят следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="c5315-147">If the user's language is set to 'en-ca', the following changes take place based on the language selection:</span></span> 

1. <span data-ttu-id="c5315-148">Клиент Teams берет строки "fr" и переописывает их строками "en".</span><span class="sxs-lookup"><span data-stu-id="c5315-148">The Teams client takes the 'fr' strings and overwrite them with the 'en' strings.</span></span>
1. <span data-ttu-id="c5315-149">Так как локализация "en-ca" не поставляется, используется локализация "en".</span><span class="sxs-lookup"><span data-stu-id="c5315-149">Since no 'en-ca' localization is supplied, the 'en\` localizations are used.</span></span>

<span data-ttu-id="c5315-150">Если язык пользователя настроен на "es-es", Teams принимает строки "fr".</span><span class="sxs-lookup"><span data-stu-id="c5315-150">If the user's language is set to 'es-es', the Teams client takes the 'fr' strings.</span></span> <span data-ttu-id="c5315-151">Клиент Teams не переопределяет строки ни с одним из языковых файлов, так как не предоставляется перевод "es" или "es-es".</span><span class="sxs-lookup"><span data-stu-id="c5315-151">The Teams client does not override the strings with any of the language files as no 'es' or 'es-es' translation is provided.</span></span>

<span data-ttu-id="c5315-152">Поэтому в манифесте необходимо предоставить только переводы верхнего уровня, языка.</span><span class="sxs-lookup"><span data-stu-id="c5315-152">Therefore, you must provide top level, language only translations in your manifest.</span></span> <span data-ttu-id="c5315-153">Например, "en" вместо "en-ru".</span><span class="sxs-lookup"><span data-stu-id="c5315-153">For example, 'en' instead of 'en-us'.</span></span> <span data-ttu-id="c5315-154">Необходимо предоставить переопределения уровня региона только для нескольких строк, которые в них нуждаются.</span><span class="sxs-lookup"><span data-stu-id="c5315-154">You must provide region level overrides only for the few strings that need them.</span></span> 

### <a name="example-manifestjson-change"></a><span data-ttu-id="c5315-155">Пример manifest.jsизменения</span><span class="sxs-lookup"><span data-stu-id="c5315-155">Example manifest.json change</span></span>

<span data-ttu-id="c5315-156">Пример manifest.jsизменения показан в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="c5315-156">The manifest.json change is shown in the following example:</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en",
    "additionalLanguages": [
      {
        "languageTag": "en-gb",
        "file": "en-gb.json"
      },
      {
        "languageTag": "fr",
        "file": "fr.json"
      },
      {
        "languageTag": "pl",
        "file": "pl.json"
      }
    ]
  }
  ...
}
```

### <a name="example-localization-json-file"></a><span data-ttu-id="c5315-157">Пример локализации файла .json</span><span class="sxs-lookup"><span data-stu-id="c5315-157">Example localization .json file</span></span>

 <span data-ttu-id="c5315-158">Пример localization.jsизменения показан в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="c5315-158">The localization.json change is shown in the following example:</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "name.short": "Le App",
  "name.full": "App pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

## <a name="handle-localized-text-submissions-from-your-users"></a><span data-ttu-id="c5315-159">Обработка локализованных текстовых сообщений от пользователей</span><span class="sxs-lookup"><span data-stu-id="c5315-159">Handle localized text submissions from your users</span></span>

<span data-ttu-id="c5315-160">Если вы предоставляете локализованные версии приложения, пользователи отвечают на них одним и тем же языком.</span><span class="sxs-lookup"><span data-stu-id="c5315-160">If your provide localized versions of your application, the users respond with the same language.</span></span> <span data-ttu-id="c5315-161">Поскольку Teams не переводит отправки пользователей на язык по умолчанию, приложение должно обрабатывать локализованные языковые ответы.</span><span class="sxs-lookup"><span data-stu-id="c5315-161">As Teams does not translate the user submissions back to the default language, your app must handle the localized language responses.</span></span> <span data-ttu-id="c5315-162">Например, если вы предоставляете локализованный, ответы на бота являются локализованным текстом команды, а не `commandList` языком по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c5315-162">For example, if you provide a localized `commandList`, the responses to your bot are the localized text of the command, not the default language.</span></span> <span data-ttu-id="c5315-163">Ваше приложение должно отвечать соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="c5315-163">Your app must respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="c5315-164">Пример кода</span><span class="sxs-lookup"><span data-stu-id="c5315-164">Code sample</span></span>

| <span data-ttu-id="c5315-165">Пример имени</span><span class="sxs-lookup"><span data-stu-id="c5315-165">Sample name</span></span> | <span data-ttu-id="c5315-166">Description</span><span class="sxs-lookup"><span data-stu-id="c5315-166">Description</span></span> | <span data-ttu-id="c5315-167">.NET</span><span class="sxs-lookup"><span data-stu-id="c5315-167">.NET</span></span> | <span data-ttu-id="c5315-168">Node.js</span><span class="sxs-lookup"><span data-stu-id="c5315-168">Node.js</span></span> |
|-------------|-------------|------|------|
| <span data-ttu-id="c5315-169">Локализация приложений</span><span class="sxs-lookup"><span data-stu-id="c5315-169">App Localization</span></span> | <span data-ttu-id="c5315-170">Microsoft Teams для локализации приложений с помощью бота и вкладки.</span><span class="sxs-lookup"><span data-stu-id="c5315-170">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="c5315-171">View</span><span class="sxs-lookup"><span data-stu-id="c5315-171">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[<span data-ttu-id="c5315-172">View</span><span class="sxs-lookup"><span data-stu-id="c5315-172">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

