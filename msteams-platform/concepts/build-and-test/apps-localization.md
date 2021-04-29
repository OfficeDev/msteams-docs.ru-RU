---
title: Локализация для приложения
description: Описывает соображения по локализации приложения Microsoft Teams.
ms.topic: conceptual
localization_priority: Normal
keywords: команды публикуют язык локализации AppSource в офисе магазина
ms.date: 05/15/2018
ms.openlocfilehash: 6c63bd5c71934d0a3342b31bc10feda38b8ae0d1
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075747"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="faabb-104">Локализация приложений Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="faabb-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="faabb-105">При локализации приложения Microsoft Teams необходимо учитывать три основные области.</span><span class="sxs-lookup"><span data-stu-id="faabb-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="faabb-106">Список AppSource (если вы публикуете в магазине приложений).</span><span class="sxs-lookup"><span data-stu-id="faabb-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="faabb-107">Строки, стоящие перед конечным пользователем в манифесте приложения (например, команды ботов).</span><span class="sxs-lookup"><span data-stu-id="faabb-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="faabb-108">Реагирование на локализованный текст, отправленный от пользователей.</span><span class="sxs-lookup"><span data-stu-id="faabb-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="faabb-109">Локализация списка AppSource</span><span class="sxs-lookup"><span data-stu-id="faabb-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="faabb-110">При публикации в магазине приложений необходимо знать, что локализация списка AppSource еще не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="faabb-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="faabb-111">Однако при подготовке к поддержке локализованных списков в магазине приложений можно добавить в список дополнительные языки.</span><span class="sxs-lookup"><span data-stu-id="faabb-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="faabb-112">В настоящее время в списке [](/office/dev/store/submit-to-appsource-via-partner-center) веб-сайта [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) для вашего приложения будут отображаться только языковые сведения по умолчанию ,которые вы предоставляете в Центре партнеров для вашего списка.</span><span class="sxs-lookup"><span data-stu-id="faabb-112">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="faabb-113">Чтобы настроить дополнительный язык для приложения, в [Центре](/office/dev/store/submit-to-appsource-via-partner-center)партнеров выберите английский и дополнительный язык приложения.</span><span class="sxs-lookup"><span data-stu-id="faabb-113">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="faabb-114">Французский язык используется в этом примере.</span><span class="sxs-lookup"><span data-stu-id="faabb-114">French is used in this example.</span></span>

1. <span data-ttu-id="faabb-115">Добавление английского языка</span><span class="sxs-lookup"><span data-stu-id="faabb-115">Add English language</span></span>
    * <span data-ttu-id="faabb-116">Заполните имя приложения.</span><span class="sxs-lookup"><span data-stu-id="faabb-116">Fill in the app name.</span></span>
    * <span data-ttu-id="faabb-117">Заполните краткое описание приложения на английском языке.</span><span class="sxs-lookup"><span data-stu-id="faabb-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="faabb-118">Заполните длинное описание приложения на английском языке.</span><span class="sxs-lookup"><span data-stu-id="faabb-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="faabb-119">В длинном описании также добавьте строку "Это приложение доступно на французском языке".</span><span class="sxs-lookup"><span data-stu-id="faabb-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="faabb-120">Загрузите изображения пользовательского интерфейса приложения (на английском языке).</span><span class="sxs-lookup"><span data-stu-id="faabb-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="faabb-121">Добавление французского языка</span><span class="sxs-lookup"><span data-stu-id="faabb-121">Add French language</span></span>
    * <span data-ttu-id="faabb-122">Заполните имя приложения.</span><span class="sxs-lookup"><span data-stu-id="faabb-122">Fill in the app name.</span></span>
    * <span data-ttu-id="faabb-123">Заполните краткое описание приложения на французском языке.</span><span class="sxs-lookup"><span data-stu-id="faabb-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="faabb-124">Заполните длинное описание приложения на французском языке.</span><span class="sxs-lookup"><span data-stu-id="faabb-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="faabb-125">Загрузите изображения пользовательского интерфейса приложения (на французском языке).</span><span class="sxs-lookup"><span data-stu-id="faabb-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="faabb-126">Изображения, которые вы загружаете на английском языке, будут использоваться в AppSource.</span><span class="sxs-lookup"><span data-stu-id="faabb-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="faabb-127">Локализация строк в манифесте приложения</span><span class="sxs-lookup"><span data-stu-id="faabb-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="faabb-128">Чтобы правильно локализовать приложение, необходимо использовать схему приложения Microsoft Teams v1.5+.</span><span class="sxs-lookup"><span data-stu-id="faabb-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="faabb-129">Это можно сделать, установив атрибут в файле manifest.js'и обновив свойство manifestVersion до `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json '1.7'.</span><span class="sxs-lookup"><span data-stu-id="faabb-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="faabb-130">Пример manifest.jsизменения</span><span class="sxs-lookup"><span data-stu-id="faabb-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="faabb-131">Затем необходимо добавить свойство "локализацияInfo" с языком по умолчанию, который поддерживает ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="faabb-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="faabb-132">Язык по умолчанию используется в качестве конечного языка отката, если параметры клиента пользователя не совпадают ни с одним из дополнительных языков.</span><span class="sxs-lookup"><span data-stu-id="faabb-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="faabb-133">Пример manifest.jsизменения</span><span class="sxs-lookup"><span data-stu-id="faabb-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="faabb-134">Вы можете предоставить дополнительные файлы json с переводами всех строк пользователя, стоящих перед вами в манифесте.</span><span class="sxs-lookup"><span data-stu-id="faabb-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="faabb-135">Эти файлы должны соответствовать схеме [JSON-файла](../../resources/schema/localization-schema.md) локализации, и они должны быть добавлены в свойство "локализацияИнфо" манифеста.</span><span class="sxs-lookup"><span data-stu-id="faabb-135">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="faabb-136">Каждый файл соотносится с языковым тегом, который клиент Teams использует для выбора соответствующих строк.</span><span class="sxs-lookup"><span data-stu-id="faabb-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="faabb-137">Тег языка принимает форму, но рекомендуется опустить часть для всех регионов, которые поддерживают <language> - <region> <region> нужный язык.</span><span class="sxs-lookup"><span data-stu-id="faabb-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="faabb-138">Клиент Teams применяет строки в этом порядке: языковые строки по умолчанию —> языка пользователя только строки -> языка пользователя + строки области пользователя.</span><span class="sxs-lookup"><span data-stu-id="faabb-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="faabb-139">Например, по умолчанию вы предоставляете язык "fr" (французский, все регионы) и дополнительные языковые файлы для "en" (английский язык, все регионы) и "en-GB" (английский, Великобритания).</span><span class="sxs-lookup"><span data-stu-id="faabb-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="faabb-140">Если язык пользователя настроен на "en-GB":</span><span class="sxs-lookup"><span data-stu-id="faabb-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="faabb-141">Клиент Teams будет переописывать строки "fr" строками "en".</span><span class="sxs-lookup"><span data-stu-id="faabb-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="faabb-142">Переопиши их со строками "en-GB".</span><span class="sxs-lookup"><span data-stu-id="faabb-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="faabb-143">Если язык пользователя настроен на "en-ca":</span><span class="sxs-lookup"><span data-stu-id="faabb-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="faabb-144">Клиент Teams будет переописывать строки "fr" строками "en".</span><span class="sxs-lookup"><span data-stu-id="faabb-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="faabb-145">Поскольку локализация "en-ca" не поставляется, будут использоваться локализации "en".</span><span class="sxs-lookup"><span data-stu-id="faabb-145">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="faabb-146">Если язык пользователя настроен на "es-es", клиент Teams берет строки "fr" и не переопределит их ни с одним из языковых файлов.</span><span class="sxs-lookup"><span data-stu-id="faabb-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="faabb-147">Поэтому настоятельно рекомендуется предоставлять в манифесте переводы только на языке верхнего уровня (вместо "en-ru") и предоставлять переопределения на уровне региона только для нескольких строк, которые в них нуждаются.</span><span class="sxs-lookup"><span data-stu-id="faabb-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="faabb-148">Пример manifest.jsизменения</span><span class="sxs-lookup"><span data-stu-id="faabb-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="faabb-149">Пример локализации файла .json</span><span class="sxs-lookup"><span data-stu-id="faabb-149">Example localization .json file</span></span>

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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="faabb-150">Обработка локализованных текстовых сообщений от пользователей</span><span class="sxs-lookup"><span data-stu-id="faabb-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="faabb-151">Если у вас есть локализованные версии приложения, очень вероятно, что пользователи будут отвечать на них одним и тем же языком.</span><span class="sxs-lookup"><span data-stu-id="faabb-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="faabb-152">Teams не переводит пользовательские отправки обратно на язык по умолчанию, поэтому вашему приложению потребуется это сделать.</span><span class="sxs-lookup"><span data-stu-id="faabb-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="faabb-153">Например, если вы предоставляете локализованный, ответом на бот будет локализованный текст команды, а не `commandList` язык по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="faabb-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="faabb-154">Вашему приложению необходимо соответствующим образом реагировать.</span><span class="sxs-lookup"><span data-stu-id="faabb-154">Your app will need to respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="faabb-155">Пример кода</span><span class="sxs-lookup"><span data-stu-id="faabb-155">Code sample</span></span>

| <span data-ttu-id="faabb-156">Пример имени</span><span class="sxs-lookup"><span data-stu-id="faabb-156">Sample name</span></span> | <span data-ttu-id="faabb-157">Описание</span><span class="sxs-lookup"><span data-stu-id="faabb-157">Description</span></span> | <span data-ttu-id="faabb-158">.NET</span><span class="sxs-lookup"><span data-stu-id="faabb-158">.NET</span></span> |
|-------------|-------------|------|
| <span data-ttu-id="faabb-159">Локализация приложений</span><span class="sxs-lookup"><span data-stu-id="faabb-159">App Localization</span></span> | <span data-ttu-id="faabb-160">Локализация приложений Microsoft Teams с помощью бота и вкладки.</span><span class="sxs-lookup"><span data-stu-id="faabb-160">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="faabb-161">View</span><span class="sxs-lookup"><span data-stu-id="faabb-161">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


