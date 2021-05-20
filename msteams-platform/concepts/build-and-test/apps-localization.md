---
title: Локализация для приложения
description: Описывает соображения для локализации вашего Microsoft Teams приложения.
ms.topic: conceptual
localization_priority: Normal
keywords: команды публикуют магазин офис публикации AppSource язык локализации
ms.date: 05/15/2018
ms.openlocfilehash: a55b8af97e5306843858e5844a017dd402ab3516
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566049"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="a49a2-104">Локализация для Microsoft Teams приложений</span><span class="sxs-lookup"><span data-stu-id="a49a2-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="a49a2-105">При локализации Microsoft Teams приложения необходимо учитывать следующее:</span><span class="sxs-lookup"><span data-stu-id="a49a2-105">When localizing your Microsoft Teams app, you must consider the following:</span></span>

1. <span data-ttu-id="a49a2-106">Ваш Teams (если это применимо).</span><span class="sxs-lookup"><span data-stu-id="a49a2-106">Your Teams store listing (if applicable).</span></span>
1. <span data-ttu-id="a49a2-107">Строка, обращенная к конечному пользователю в вашем приложении, проявляется.</span><span class="sxs-lookup"><span data-stu-id="a49a2-107">The end-user facing strings in your app manifest.</span></span> <span data-ttu-id="a49a2-108">Например, команды ботов.</span><span class="sxs-lookup"><span data-stu-id="a49a2-108">For example bot commands.</span></span>
1. <span data-ttu-id="a49a2-109">Реагирование на локализованный текст, представленный пользователями.</span><span class="sxs-lookup"><span data-stu-id="a49a2-109">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="a49a2-110">Локализация списка AppSource</span><span class="sxs-lookup"><span data-stu-id="a49a2-110">Localizing your AppSource listing</span></span>

<span data-ttu-id="a49a2-111">Если вы публикуете в магазине, вы должны знать, что локализация вашего списка AppSource еще не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="a49a2-111">If you're publishing to the store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="a49a2-112">Однако в рамках подготовки к поддержке локализованных объявлений в магазине приложений вы можете добавить дополнительные языки в свой список.</span><span class="sxs-lookup"><span data-stu-id="a49a2-112">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="a49a2-113">В настоящее время в [списке веб-сайта AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) для вашего приложения появится только информация о языке по умолчанию (английский), которую вы предоставляете в Партнер-центре для вашего объявления. [](/office/dev/store/submit-to-appsource-via-partner-center)</span><span class="sxs-lookup"><span data-stu-id="a49a2-113">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

### <a name="example-of-configuring-localization"></a><span data-ttu-id="a49a2-114">Пример настройки локализации</span><span class="sxs-lookup"><span data-stu-id="a49a2-114">Example of configuring localization</span></span>

<span data-ttu-id="a49a2-115">Чтобы настроить дополнительный язык для вашего приложения, в [Партнер-центре,](/office/dev/store/submit-to-appsource-via-partner-center)выберите как английский, так и дополнительный язык приложения.</span><span class="sxs-lookup"><span data-stu-id="a49a2-115">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="a49a2-116">Французский язык используется в этом примере:</span><span class="sxs-lookup"><span data-stu-id="a49a2-116">French is used in this example:</span></span>

1. <span data-ttu-id="a49a2-117">Добавить английский язык</span><span class="sxs-lookup"><span data-stu-id="a49a2-117">Add English language</span></span>
    * <span data-ttu-id="a49a2-118">Заполните имя приложения.</span><span class="sxs-lookup"><span data-stu-id="a49a2-118">Fill in the app name.</span></span>
    * <span data-ttu-id="a49a2-119">Заполните краткое описание приложения на английском языке.</span><span class="sxs-lookup"><span data-stu-id="a49a2-119">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="a49a2-120">Заполните длинное описание приложения на английском языке.</span><span class="sxs-lookup"><span data-stu-id="a49a2-120">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="a49a2-121">В длинном описании, пожалуйста, также добавьте строку "Это приложение доступно на французском языке".</span><span class="sxs-lookup"><span data-stu-id="a49a2-121">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="a49a2-122">Upload изображения пользовательского интерфейса приложения (на английском языке).</span><span class="sxs-lookup"><span data-stu-id="a49a2-122">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="a49a2-123">Добавить французский язык</span><span class="sxs-lookup"><span data-stu-id="a49a2-123">Add French language</span></span>
    * <span data-ttu-id="a49a2-124">Заполните имя приложения.</span><span class="sxs-lookup"><span data-stu-id="a49a2-124">Fill in the app name.</span></span>
    * <span data-ttu-id="a49a2-125">Заполните краткое описание приложения на французском языке.</span><span class="sxs-lookup"><span data-stu-id="a49a2-125">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="a49a2-126">Заполните длинное описание приложения на французском языке.</span><span class="sxs-lookup"><span data-stu-id="a49a2-126">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="a49a2-127">Upload изображения пользовательского интерфейса приложения (на французском языке).</span><span class="sxs-lookup"><span data-stu-id="a49a2-127">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="a49a2-128">Изображения, которые вы загружаете на английском языке, будут использоваться в AppSource.</span><span class="sxs-lookup"><span data-stu-id="a49a2-128">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="a49a2-129">Локализация строк в манифесте приложения</span><span class="sxs-lookup"><span data-stu-id="a49a2-129">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="a49a2-130">Вы должны использовать схему Microsoft Teams приложения v1.5 ", чтобы правильно локализовать приложение.</span><span class="sxs-lookup"><span data-stu-id="a49a2-130">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="a49a2-131">Вы можете сделать это, установив `$schema` атрибут в вашем manifest.jsфайле на https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json '' и обновление 'manifestVersion' собственности на '1.7'.</span><span class="sxs-lookup"><span data-stu-id="a49a2-131">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="a49a2-132">Пример manifest.jsоб изменениях</span><span class="sxs-lookup"><span data-stu-id="a49a2-132">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="a49a2-133">Затем вы захотите добавить свойство 'localizationInfo' с языком по умолчанию, который поддерживает ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="a49a2-133">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="a49a2-134">Язык по умолчанию используется в качестве последнего языка возврата, если настройки клиента пользователя не соответствуют ни одному из ваших дополнительных языков.</span><span class="sxs-lookup"><span data-stu-id="a49a2-134">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="a49a2-135">Пример manifest.jsоб изменениях</span><span class="sxs-lookup"><span data-stu-id="a49a2-135">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="a49a2-136">Вы можете предоставить дополнительные файлы .json с переводами всех пользователей, сталкиваются строки в вашем манифесте.</span><span class="sxs-lookup"><span data-stu-id="a49a2-136">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="a49a2-137">Эти файлы должны придерживаться [схемы локализации файла JSON,](../../resources/schema/localization-schema.md) и они должны быть добавлены к свойству 'localizationInfo' вашего манифеста.</span><span class="sxs-lookup"><span data-stu-id="a49a2-137">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="a49a2-138">Каждый файл коррелирует с тегом языка, который Teams клиент использует для выбора соответствующих строк.</span><span class="sxs-lookup"><span data-stu-id="a49a2-138">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="a49a2-139">Тег языка принимает форму, но <language> - <region> рекомендуется опустить часть для <region> таргетинга на все регионы, которые поддерживают нужный язык.</span><span class="sxs-lookup"><span data-stu-id="a49a2-139">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="a49a2-140">Клиент Teams будет применять строки в этом порядке: строки языка по умолчанию -> язык пользователя только строки -> язык пользователя и строки региона пользователя.</span><span class="sxs-lookup"><span data-stu-id="a49a2-140">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="a49a2-141">Например, вы предоставляете язык по умолчанию 'fr' (французский, все регионы), а также дополнительные языковые файлы для 'en' (английский, все регионы) и 'en-gb' (английский, Великобритания).</span><span class="sxs-lookup"><span data-stu-id="a49a2-141">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="a49a2-142">Если язык пользователя настроен на 'en-gb':</span><span class="sxs-lookup"><span data-stu-id="a49a2-142">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="a49a2-143">Клиент Teams будет принимать строки 'fr' перезаписать их с 'en' строки.</span><span class="sxs-lookup"><span data-stu-id="a49a2-143">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="a49a2-144">Перезаписать тех, с "ан-гб" строки.</span><span class="sxs-lookup"><span data-stu-id="a49a2-144">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="a49a2-145">Если язык пользователя настроен на 'en-ca':</span><span class="sxs-lookup"><span data-stu-id="a49a2-145">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="a49a2-146">Клиент Teams будет принимать строки 'fr' перезаписать их с 'en' строки.</span><span class="sxs-lookup"><span data-stu-id="a49a2-146">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="a49a2-147">Поскольку локализация "en-ca" не обеспечивается, будут использоваться локализации "en".</span><span class="sxs-lookup"><span data-stu-id="a49a2-147">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="a49a2-148">Если язык пользователя настроен на 'es-es', клиент Teams примет строки 'fr' и не переопределит их ни с одним из языковых файлов.</span><span class="sxs-lookup"><span data-stu-id="a49a2-148">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="a49a2-149">Поэтому настоятельно рекомендуется предоставлять переводы только на высшем уровне в вашем манифесте ('en' вместо 'en-us') и предоставлять переопределения только на уровне региона для нескольких строк, которые в них нуждаются.</span><span class="sxs-lookup"><span data-stu-id="a49a2-149">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="a49a2-150">Пример manifest.jsоб изменениях</span><span class="sxs-lookup"><span data-stu-id="a49a2-150">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="a49a2-151">Пример локализации файла .json</span><span class="sxs-lookup"><span data-stu-id="a49a2-151">Example localization .json file</span></span>

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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="a49a2-152">Обработка локализованных текстовых сообщений от пользователей</span><span class="sxs-lookup"><span data-stu-id="a49a2-152">Handling localized text submissions from your users</span></span>

<span data-ttu-id="a49a2-153">Если вы предоставите локализованные версии приложения, то весьма вероятно, что пользователи ответят тем же языком.</span><span class="sxs-lookup"><span data-stu-id="a49a2-153">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="a49a2-154">Teams не переводит представления пользователей обратно на язык по умолчанию, поэтому вашему приложению нужно будет справиться с этим.</span><span class="sxs-lookup"><span data-stu-id="a49a2-154">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="a49a2-155">Например, если вы предоставляете `commandList` локализованный, ответы на ваш бот будет локализованный текст команды, а не язык по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a49a2-155">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="a49a2-156">Ваше приложение должно будет реагировать соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="a49a2-156">Your app will need to respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="a49a2-157">Пример кода</span><span class="sxs-lookup"><span data-stu-id="a49a2-157">Code sample</span></span>

| <span data-ttu-id="a49a2-158">Название образца</span><span class="sxs-lookup"><span data-stu-id="a49a2-158">Sample name</span></span> | <span data-ttu-id="a49a2-159">Описание</span><span class="sxs-lookup"><span data-stu-id="a49a2-159">Description</span></span> | <span data-ttu-id="a49a2-160">.NET</span><span class="sxs-lookup"><span data-stu-id="a49a2-160">.NET</span></span> |
|-------------|-------------|------|
| <span data-ttu-id="a49a2-161">Локализация приложений</span><span class="sxs-lookup"><span data-stu-id="a49a2-161">App Localization</span></span> | <span data-ttu-id="a49a2-162">Microsoft Teams приложения с помощью бота и вкладки.</span><span class="sxs-lookup"><span data-stu-id="a49a2-162">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="a49a2-163">View</span><span class="sxs-lookup"><span data-stu-id="a49a2-163">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


