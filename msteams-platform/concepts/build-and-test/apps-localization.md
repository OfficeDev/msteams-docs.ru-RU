---
title: Локализация для групповых приложений
description: Описание проблем, связанных с локализацией приложения
keywords: Teams Publishing Store Office Publishing AppSource Language Localization
ms.date: 05/15/2018
ms.openlocfilehash: 138b6d66808fc5ed212f1cb0eed8579faea6f764
ms.sourcegitcommit: bac0226d9048c363d96bbaf6f5395388c5f5c45a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/06/2020
ms.locfileid: "45039274"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="eabda-104">Локализация приложений Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="eabda-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="eabda-105">При локализации приложения Microsoft Teams необходимо учитывать три основных аспекта.</span><span class="sxs-lookup"><span data-stu-id="eabda-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="eabda-106">Список AppSource (если выполняется публикация в магазине приложений).</span><span class="sxs-lookup"><span data-stu-id="eabda-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="eabda-107">Строки конечного пользователя в манифесте приложения (например, команды Bot).</span><span class="sxs-lookup"><span data-stu-id="eabda-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="eabda-108">Реагирование на локализованный текст, отправленный пользователями;</span><span class="sxs-lookup"><span data-stu-id="eabda-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="eabda-109">Локализация списка AppSource</span><span class="sxs-lookup"><span data-stu-id="eabda-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="eabda-110">Если вы публикуете в магазине приложений, вам необходимо знать, что локализация вашего списка AppSource пока не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="eabda-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="eabda-111">Однако в процессе подготовки к поддержке локализованных вхождений в магазине App можно добавить в список дополнительные языки.</span><span class="sxs-lookup"><span data-stu-id="eabda-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="eabda-112">В настоящее время только сведения о языке по умолчанию (Английская версия), которые вы предоставляете в [центре партнеров](/dev/store/use-partner-center-to-submit-to-appsource) для вашего списка, будут отображаться в списке [веб-сайтов AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="eabda-112">Currently only the default (English) language information you provide in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="eabda-113">Чтобы настроить дополнительный язык для приложения, в [центре партнеров](/dev/store/use-partner-center-to-submit-to-appsource)выберите английский и дополнительный язык приложения.</span><span class="sxs-lookup"><span data-stu-id="eabda-113">To configure an additional language for your app, in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource), select both English and the additional language of the app.</span></span> <span data-ttu-id="eabda-114">В этом примере используется французский язык.</span><span class="sxs-lookup"><span data-stu-id="eabda-114">French is used in this example.</span></span>

1. <span data-ttu-id="eabda-115">Добавление английского языка</span><span class="sxs-lookup"><span data-stu-id="eabda-115">Add English language</span></span>
    * <span data-ttu-id="eabda-116">Введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="eabda-116">Fill in the app name.</span></span>
    * <span data-ttu-id="eabda-117">Заполните краткое описание приложения на английском языке.</span><span class="sxs-lookup"><span data-stu-id="eabda-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="eabda-118">Заполните подробное описание приложения на английском языке.</span><span class="sxs-lookup"><span data-stu-id="eabda-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="eabda-119">В подробном описании добавьте также строку "это приложение доступно на французском языке".</span><span class="sxs-lookup"><span data-stu-id="eabda-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="eabda-120">Отправьте изображения пользовательского интерфейса приложения (на английском языке).</span><span class="sxs-lookup"><span data-stu-id="eabda-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="eabda-121">Добавление французского языка</span><span class="sxs-lookup"><span data-stu-id="eabda-121">Add French language</span></span>
    * <span data-ttu-id="eabda-122">Введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="eabda-122">Fill in the app name.</span></span>
    * <span data-ttu-id="eabda-123">Заполните краткое описание приложения на французском языке.</span><span class="sxs-lookup"><span data-stu-id="eabda-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="eabda-124">Заполните подробное описание приложения на французском языке.</span><span class="sxs-lookup"><span data-stu-id="eabda-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="eabda-125">Отправьте изображения пользовательского интерфейса приложения (на французском языке).</span><span class="sxs-lookup"><span data-stu-id="eabda-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="eabda-126">Изображения, которые вы отправляете с английским языком, будут использоваться в AppSource.</span><span class="sxs-lookup"><span data-stu-id="eabda-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="eabda-127">Локализация строк в манифесте приложения</span><span class="sxs-lookup"><span data-stu-id="eabda-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="eabda-128">Для правильной локализации приложения необходимо использовать схему приложения Microsoft Teams версии 1.5 +.</span><span class="sxs-lookup"><span data-stu-id="eabda-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="eabda-129">Это можно сделать, присвоив `$schema` атрибуту в manifest.jsфайла значение ' https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json ' и обновив свойство ' версия манифеста ' до ' 1,7 '.</span><span class="sxs-lookup"><span data-stu-id="eabda-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="eabda-130">Пример manifest.jsпри изменении</span><span class="sxs-lookup"><span data-stu-id="eabda-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="eabda-131">Затем необходимо добавить свойство "Локализатионинфо" с языком по умолчанию, который поддерживает ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="eabda-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="eabda-132">В качестве последнего базового языка используется язык по умолчанию, если параметры клиента пользователя не совпадают с какими-либо из дополнительных языков.</span><span class="sxs-lookup"><span data-stu-id="eabda-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="eabda-133">Пример manifest.jsпри изменении</span><span class="sxs-lookup"><span data-stu-id="eabda-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="eabda-134">Вы можете предоставить дополнительные файлы JSON с переводом всех строк, отличных от пользователя, в манифесте.</span><span class="sxs-lookup"><span data-stu-id="eabda-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="eabda-135">Эти файлы должны соответствовать [схеме JSON файла локализации](../../resources/schema/localization-schema.md) , и их необходимо добавить в свойство "локализатионинфо" манифеста.</span><span class="sxs-lookup"><span data-stu-id="eabda-135">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="eabda-136">Каждый файл соответствует тегу языка, который клиент Teams использует для выбора соответствующих строк.</span><span class="sxs-lookup"><span data-stu-id="eabda-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="eabda-137">Тег Language имеет форму, <language> - <region> но мы не рекомендуем опустить <region> часть для всех регионов, поддерживающих нужный язык.</span><span class="sxs-lookup"><span data-stu-id="eabda-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="eabda-138">Клиент Teams будет применять строки в указанном порядке: строки языка по умолчанию — строки языка по умолчанию — > только строки > язык пользователя и строки области пользователя.</span><span class="sxs-lookup"><span data-stu-id="eabda-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="eabda-139">Например, вы предоставляете язык по умолчанию: "fr" (французский, все регионы) и дополнительные языковые файлы для "en" (английский, все регионы) и "en-GB" (английский, Великобритания).</span><span class="sxs-lookup"><span data-stu-id="eabda-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="eabda-140">Если для языка пользователя задано значение "en-GB":</span><span class="sxs-lookup"><span data-stu-id="eabda-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="eabda-141">Клиент Teams получит строки "fr", заменяя их строками "en".</span><span class="sxs-lookup"><span data-stu-id="eabda-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="eabda-142">Перезаписать их строками "en – GB".</span><span class="sxs-lookup"><span data-stu-id="eabda-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="eabda-143">Если для языка пользователя задано значение "en-CA":</span><span class="sxs-lookup"><span data-stu-id="eabda-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="eabda-144">Клиент Teams получит строки "fr", заменяя их строками "en".</span><span class="sxs-lookup"><span data-stu-id="eabda-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="eabda-145">Так как не указана локализация "en-CA", будут использоваться локализации "en".</span><span class="sxs-lookup"><span data-stu-id="eabda-145">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="eabda-146">Если для языка пользователя задано значение "es-ES", клиент Teams будет принимать строки "fr" и не будет переопределять их с помощью языковых файлов.</span><span class="sxs-lookup"><span data-stu-id="eabda-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="eabda-147">Таким образом, настоятельно рекомендуется предоставлять в манифесте только верхние и языковые переводы в манифесте ("en" вместо "en-US"), а также предоставлять переопределение на уровне области только для тех строк, которые им нужны.</span><span class="sxs-lookup"><span data-stu-id="eabda-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="eabda-148">Пример manifest.jsпри изменении</span><span class="sxs-lookup"><span data-stu-id="eabda-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="eabda-149">Пример файла Localization. JSON</span><span class="sxs-lookup"><span data-stu-id="eabda-149">Example localization .json file</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="eabda-150">Обработка локализованных текстов, отправленных пользователями</span><span class="sxs-lookup"><span data-stu-id="eabda-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="eabda-151">Если вы предоставляете локализованные версии вашего приложения, то, скорее всего, ваши пользователи будут отвечать на один и тот же язык.</span><span class="sxs-lookup"><span data-stu-id="eabda-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="eabda-152">Команды не переводятся обратно на язык по умолчанию, поэтому ваше приложение должно их обработать.</span><span class="sxs-lookup"><span data-stu-id="eabda-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="eabda-153">Например, если вы задаете локализованные сообщения `commandList` , ответы на ваш Bot будут иметь локализованный текст команды, а не язык по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="eabda-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="eabda-154">Ваше приложение должно будет отвечать соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="eabda-154">Your app will need to respond appropriately.</span></span>
