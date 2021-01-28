---
title: Локализация приложения
description: В этой статье описываются вопросы локализации приложения Microsoft Teams.
ms.topic: conceptual
keywords: Команды публикуют язык локализации AppSource для публикации Office в Магазине
ms.date: 05/15/2018
ms.openlocfilehash: 69bee0ee11238dc0e461e4fddf8ed01f0cfcccde
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014301"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="118c4-104">Локализация приложений Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="118c4-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="118c4-105">При локализации приложения Microsoft Teams необходимо учитывать три основных области.</span><span class="sxs-lookup"><span data-stu-id="118c4-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="118c4-106">Описание в AppSource (если вы публикуете в Магазине приложений).</span><span class="sxs-lookup"><span data-stu-id="118c4-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="118c4-107">Строки, с которыми сталкиваются конечные пользователи, в манифесте приложения (например, команды ботов).</span><span class="sxs-lookup"><span data-stu-id="118c4-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="118c4-108">Реагирование на локализованный текст, отправленный пользователями.</span><span class="sxs-lookup"><span data-stu-id="118c4-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="118c4-109">Локализация списка AppSource</span><span class="sxs-lookup"><span data-stu-id="118c4-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="118c4-110">При публикации в Магазине приложений необходимо помнить, что локализация вашего списка AppSource пока не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="118c4-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="118c4-111">Однако во время подготовки к поддержке локализованных объявлений в магазине приложений вы можете добавить в описание дополнительные языки.</span><span class="sxs-lookup"><span data-stu-id="118c4-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="118c4-112">В настоящее время в списке [](/office/dev/store/submit-to-appsource-via-partner-center) веб-сайта [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) для вашего приложения будут отображаться только сведения о языке по умолчанию (английский), которые вы предоставляете в Центре партнеров для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="118c4-112">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="118c4-113">Чтобы настроить дополнительный язык для [](/office/dev/store/submit-to-appsource-via-partner-center)приложения, в Центре партнеров выберите английский и дополнительный язык приложения.</span><span class="sxs-lookup"><span data-stu-id="118c4-113">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="118c4-114">В этом примере используется французский язык.</span><span class="sxs-lookup"><span data-stu-id="118c4-114">French is used in this example.</span></span>

1. <span data-ttu-id="118c4-115">Добавление английского языка</span><span class="sxs-lookup"><span data-stu-id="118c4-115">Add English language</span></span>
    * <span data-ttu-id="118c4-116">В заполните имя приложения.</span><span class="sxs-lookup"><span data-stu-id="118c4-116">Fill in the app name.</span></span>
    * <span data-ttu-id="118c4-117">Заполните краткое описание приложения на английском языке.</span><span class="sxs-lookup"><span data-stu-id="118c4-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="118c4-118">Заполните длинное описание приложения на английском языке.</span><span class="sxs-lookup"><span data-stu-id="118c4-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="118c4-119">В длинном описании также добавьте строку "Это приложение доступно на французском языке".</span><span class="sxs-lookup"><span data-stu-id="118c4-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="118c4-120">Отправка изображений пользовательского интерфейса приложения (на английском языке).</span><span class="sxs-lookup"><span data-stu-id="118c4-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="118c4-121">Добавление французского языка</span><span class="sxs-lookup"><span data-stu-id="118c4-121">Add French language</span></span>
    * <span data-ttu-id="118c4-122">В заполните имя приложения.</span><span class="sxs-lookup"><span data-stu-id="118c4-122">Fill in the app name.</span></span>
    * <span data-ttu-id="118c4-123">Заполните краткое описание приложения на французском языке.</span><span class="sxs-lookup"><span data-stu-id="118c4-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="118c4-124">Заполните длинное описание приложения на французском языке.</span><span class="sxs-lookup"><span data-stu-id="118c4-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="118c4-125">Отправка изображений пользовательского интерфейса приложения (на французском языке).</span><span class="sxs-lookup"><span data-stu-id="118c4-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="118c4-126">Изображения, отложенные с английским языком, будут использоваться в AppSource.</span><span class="sxs-lookup"><span data-stu-id="118c4-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="118c4-127">Локализация строк в манифесте приложения</span><span class="sxs-lookup"><span data-stu-id="118c4-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="118c4-128">Для правильной локализации приложения необходимо использовать схему приложения Microsoft Teams 1.5 и более.</span><span class="sxs-lookup"><span data-stu-id="118c4-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="118c4-129">Это можно сделать, установив для атрибута в файле manifest.js'' и обновив свойство `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json 'manifestVersion' на '1.7'.</span><span class="sxs-lookup"><span data-stu-id="118c4-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="118c4-130">Пример manifest.jsпри изменении</span><span class="sxs-lookup"><span data-stu-id="118c4-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="118c4-131">Затем необходимо добавить свойство "localizationInfo" с языком по умолчанию, поддерживаемым приложением.</span><span class="sxs-lookup"><span data-stu-id="118c4-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="118c4-132">Язык по умолчанию используется в качестве конечного языка для отката, если параметры клиента пользователя не соответствуют ни одному из дополнительных языков.</span><span class="sxs-lookup"><span data-stu-id="118c4-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="118c4-133">Пример manifest.jsпри изменении</span><span class="sxs-lookup"><span data-stu-id="118c4-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="118c4-134">В манифесте можно предоставить дополнительные JSON-файлы с переводами всех строк, с которыми сталкиваются пользователи.</span><span class="sxs-lookup"><span data-stu-id="118c4-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="118c4-135">Эти файлы должны соответствовать схеме [JSON](../../resources/schema/localization-schema.md) файла локализации и добавляться в свойство localizationInfo манифеста.</span><span class="sxs-lookup"><span data-stu-id="118c4-135">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="118c4-136">Каждый файл сопоставляется с языковым тегом, который клиент Teams использует для выбора соответствующих строк.</span><span class="sxs-lookup"><span data-stu-id="118c4-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="118c4-137">Тег языка имеет форму, но рекомендуется опустить часть для всех регионов, которые поддерживают <language> - <region> <region> нужный язык.</span><span class="sxs-lookup"><span data-stu-id="118c4-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="118c4-138">Клиент Teams будет применять строки в этом порядке: строки языка по умолчанию -> только строки языка пользователя -> язык пользователя + строки области пользователя.</span><span class="sxs-lookup"><span data-stu-id="118c4-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="118c4-139">Например, вы предоставляете язык по умолчанию fr (французский, все регионы) и дополнительные языковые файлы для en (английский, все регионы) и en-gb (английский, Великобритания).</span><span class="sxs-lookup"><span data-stu-id="118c4-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="118c4-140">Если для языка пользователя установлено "en-gb":</span><span class="sxs-lookup"><span data-stu-id="118c4-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="118c4-141">Клиент Teams будет переописывать строки "fr" строками en.</span><span class="sxs-lookup"><span data-stu-id="118c4-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="118c4-142">Переописывание строк en-gb.</span><span class="sxs-lookup"><span data-stu-id="118c4-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="118c4-143">Если для языка пользователя установлено "en-ca":</span><span class="sxs-lookup"><span data-stu-id="118c4-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="118c4-144">Клиент Teams будет переописывать строки "fr" строками en.</span><span class="sxs-lookup"><span data-stu-id="118c4-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="118c4-145">Так как локализация en-ca не предоставляется, будет использоваться локализация en.</span><span class="sxs-lookup"><span data-stu-id="118c4-145">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="118c4-146">Если для языка пользователя задан "es-es", клиент Teams будет принимать строки fr и не переопределять их с помощью языковых файлов.</span><span class="sxs-lookup"><span data-stu-id="118c4-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="118c4-147">Поэтому настоятельно рекомендуется предоставлять в манифесте переводы только на языке верхнего уровня (en, а не en-us) и переопределять только те строки, которые в них нуждаются.</span><span class="sxs-lookup"><span data-stu-id="118c4-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="118c4-148">Пример manifest.jsпри изменении</span><span class="sxs-lookup"><span data-stu-id="118c4-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="118c4-149">Пример JSON-файла локализации</span><span class="sxs-lookup"><span data-stu-id="118c4-149">Example localization .json file</span></span>

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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="118c4-150">Обработка локализованных текстовых отгрузок от пользователей</span><span class="sxs-lookup"><span data-stu-id="118c4-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="118c4-151">Если у вас есть локализованные версии приложения, весьма вероятно, что пользователи будут отвечать на один и тот же язык.</span><span class="sxs-lookup"><span data-stu-id="118c4-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="118c4-152">Teams не переводит отправки пользователей обратно на язык по умолчанию, поэтому ваше приложение будет обрабатывать это.</span><span class="sxs-lookup"><span data-stu-id="118c4-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="118c4-153">Например, если у вас есть локализованный текст, ответом бота будет локализованный текст команды, а не `commandList` язык по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="118c4-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="118c4-154">Ваше приложение будет реагировать соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="118c4-154">Your app will need to respond appropriately.</span></span>
