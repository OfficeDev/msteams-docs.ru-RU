---
title: Developer Preview схемы манифеста
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams
ms.topic: reference
keywords: команды проявляют схему Developer Preview
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: c2009038341a22664b0f055fa9756a9d1eba87b9
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915092"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="2fa5b-104">Схема манифеста предварительного просмотра разработчика для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2fa5b-104">Developer preview manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="2fa5b-105">Сведения о том, как включить предварительный просмотр разработчика, см. в [Microsoft Teams.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="2fa5b-105">For information on how to enable developer preview, see [public developer preview for Microsoft Teams](~/resources/dev-preview/developer-preview-intro.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="2fa5b-106">Если вы не используете функции предварительного просмотра разработчика, используйте манифест приложения [для функций GA.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="2fa5b-106">If you aren't using developer preview features, use the [app manifest for GA features](~/resources/schema/manifest-schema.md) instead.</span></span>

<span data-ttu-id="2fa5b-107">Манифест Microsoft Teams описывает интеграцию приложения в продукт Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-107">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="2fa5b-108">Манифест должен соответствовать схеме, которая была на [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) уровне .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-108">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="2fa5b-109">Дополнительные сведения о доступных функциях см. в фото: [Features in the Public Developer Preview for Microsoft Teams.](~/resources/dev-preview/developer-preview-features.md)</span><span class="sxs-lookup"><span data-stu-id="2fa5b-109">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="2fa5b-110">Образец полного манифеста</span><span class="sxs-lookup"><span data-stu-id="2fa5b-110">Sample full manifest</span></span>

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "devPreview",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "devicePermissions" : [ "geolocation", "media" ],
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "localizationInfo": {
    "defaultLanguageTag": "es-es",
    "additionalLanguages": [
      {
        "languageTag": "en-us",
        "file": "en-us.json"
      }
    ]
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters"
  },
  "description": {
    "short": "Short description of your app",
    "full": "Full description of your app"
  },
  "icons": {
    "outline": "%FILENAME-32x32px%",
    "color": "%FILENAME-192x192px"
  },
  "accentColor": "%HEX-COLOR%",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content?host=msteams",
      "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
      "websiteUrl": "https://contoso.com/content",
      "scopes": [ "personal" ]
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
  "connectors": [
    {
      "connectorId": "GUID-FROM-CONNECTOR-DEV-PORTAL%",
      "configurationUrl": "https://contoso.com/teamsconnector/configure",
      "scopes": [ "team"]
    }
  ],
  "composeExtensions": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "type" : "search",
          "context" : ["compose", "commandBox"],
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "description": "Enter the keywords to search for"
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "type" : "action",
          "fetchTask" : true,
          "context" : ["message"],
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType" : "text"
            }
          ]
        },
        {
          "id": "exampleMessageHandler",
          "title": "Message Handler",
          "description": "Domains that will create a preview when pasted into the compose box",
          "messageHandlers": [
            {
              "type" : "link",
              "value" : {
                "domains" : [
                  "mysite.someplace.com",
                  "othersite.someplace.com"
                ]
              }
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers",
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ],
  "webApplicationInfo": {
    "id": "AAD App ID",
    "resource": "Resource URL for acquiring auth token for SSO",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelSettings.Read.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "ChannelMessage.Read.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group",
      "Member.ReadWrite.Group",
      "Owner.ReadWrite.Group"
    ],
  },
   "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "developerUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ],
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  }
}
```

<span data-ttu-id="2fa5b-111">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="2fa5b-111">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="2fa5b-112">$schema</span><span class="sxs-lookup"><span data-stu-id="2fa5b-112">$schema</span></span>

<span data-ttu-id="2fa5b-113">*Необязательный, но рекомендуемый* &ndash; String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-113">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="2fa5b-114">URL https:// ссылки на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-114">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="2fa5b-115">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="2fa5b-115">manifestVersion</span></span>

<span data-ttu-id="2fa5b-116">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-116">**Required** &ndash; String</span></span>

<span data-ttu-id="2fa5b-117">Версия схемы манифеста, используемая этим манифестом.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-117">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="2fa5b-118">Это должно быть "devPreview".</span><span class="sxs-lookup"><span data-stu-id="2fa5b-118">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="2fa5b-119">version</span><span class="sxs-lookup"><span data-stu-id="2fa5b-119">version</span></span>

<span data-ttu-id="2fa5b-120">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-120">**Required** &ndash; String</span></span>

<span data-ttu-id="2fa5b-121">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-121">The version of the specific app.</span></span> <span data-ttu-id="2fa5b-122">Если вы что-то обновляете в манифесте, необходимо также приумножная версия.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-122">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="2fa5b-123">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-123">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="2fa5b-124">Если это приложение было отправлено в магазин, новый манифест должен быть повторно отправлен и повторно проверен.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-124">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="2fa5b-125">Затем пользователи этого приложения получат новый обновленный манифест автоматически через несколько часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-125">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="2fa5b-126">Если приложение запрашивает разрешения изменить, пользователям будет предложено обновить и повторно согласиться на приложение.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-126">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="2fa5b-127">Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="2fa5b-127">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="2fa5b-128">id</span><span class="sxs-lookup"><span data-stu-id="2fa5b-128">id</span></span>

<span data-ttu-id="2fa5b-129">**Обязательно** &ndash; ID приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="2fa5b-129">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="2fa5b-130">Уникальный идентификатор, созданный Корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-130">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="2fa5b-131">Если вы зарегистрировали бота через Microsoft Bot Framework или веб-приложение вашей вкладки уже входит в Microsoft, вы уже должны иметь ID и ввести его здесь.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-131">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="2fa5b-132">В противном случае необходимо создать новый ID на портале регистрации приложений Microsoft[(Мои](https://apps.dev.microsoft.com)приложения), введите его здесь, а затем повторно использовать при добавлении [бота.](~/bots/how-to/create-a-bot-for-teams.md)</span><span class="sxs-lookup"><span data-stu-id="2fa5b-132">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="2fa5b-133">packageName</span><span class="sxs-lookup"><span data-stu-id="2fa5b-133">packageName</span></span>

<span data-ttu-id="2fa5b-134">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-134">**Required** &ndash; String</span></span>

<span data-ttu-id="2fa5b-135">Уникальный идентификатор для этого приложения в обратной нотации домена; например, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-135">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="2fa5b-136">developer</span><span class="sxs-lookup"><span data-stu-id="2fa5b-136">developer</span></span>

<span data-ttu-id="2fa5b-137">**Required**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-137">**Required**</span></span>

<span data-ttu-id="2fa5b-138">Указывает сведения о вашей компании.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-138">Specifies information about your company.</span></span> <span data-ttu-id="2fa5b-139">Для приложений, представленных в AppSource (ранее Office Store), эти значения должны соответствовать сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-139">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="2fa5b-140">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-140">Name</span></span>| <span data-ttu-id="2fa5b-141">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-141">Maximum size</span></span> | <span data-ttu-id="2fa5b-142">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-142">Required</span></span> | <span data-ttu-id="2fa5b-143">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="2fa5b-144">32 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-144">32 characters</span></span>|<span data-ttu-id="2fa5b-145">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-145">✔</span></span>|<span data-ttu-id="2fa5b-146">Имя отображения для разработчика.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="2fa5b-147">2048 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-147">2048 characters</span></span>|<span data-ttu-id="2fa5b-148">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-148">✔</span></span>|<span data-ttu-id="2fa5b-149">Url https:// url-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="2fa5b-150">Эта ссылка должна принимать пользователей на страницу вашей компании или конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="2fa5b-151">2048 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-151">2048 characters</span></span>|<span data-ttu-id="2fa5b-152">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-152">✔</span></span>|<span data-ttu-id="2fa5b-153">Url https:// url-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="2fa5b-154">2048 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-154">2048 characters</span></span>|<span data-ttu-id="2fa5b-155">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-155">✔</span></span>|<span data-ttu-id="2fa5b-156">Url https:// url-адрес для условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="2fa5b-157">10 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-157">10 characters</span></span>|<span data-ttu-id="2fa5b-158">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-158">✔</span></span>|<span data-ttu-id="2fa5b-159">**Необязательный** Идентификатор Сети партнеров Майкрософт, который определяет организацию-партнер, которая строит приложение.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-159">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="2fa5b-160">локализацияInfo</span><span class="sxs-lookup"><span data-stu-id="2fa5b-160">localizationInfo</span></span>

<span data-ttu-id="2fa5b-161">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-161">**Optional**</span></span>

<span data-ttu-id="2fa5b-162">Позволяет спецификацию языка по умолчанию, а также указатели для дополнительных языковых файлов.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-162">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="2fa5b-163">См. [локализацию.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="2fa5b-163">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="2fa5b-164">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-164">Name</span></span>| <span data-ttu-id="2fa5b-165">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-165">Maximum size</span></span> | <span data-ttu-id="2fa5b-166">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-166">Required</span></span> | <span data-ttu-id="2fa5b-167">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-167">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="2fa5b-168">4 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-168">4 characters</span></span>|<span data-ttu-id="2fa5b-169">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-169">✔</span></span>|<span data-ttu-id="2fa5b-170">Языковой тег строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-170">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="2fa5b-171">локализацияInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="2fa5b-171">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="2fa5b-172">Массив объектов, указывающих дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-172">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="2fa5b-173">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-173">Name</span></span>| <span data-ttu-id="2fa5b-174">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-174">Maximum size</span></span> | <span data-ttu-id="2fa5b-175">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-175">Required</span></span> | <span data-ttu-id="2fa5b-176">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-176">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="2fa5b-177">4 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-177">4 characters</span></span>|<span data-ttu-id="2fa5b-178">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-178">✔</span></span>|<span data-ttu-id="2fa5b-179">Языковой тег строки в предоставленного файла.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-179">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="2fa5b-180">4 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-180">4 characters</span></span>|<span data-ttu-id="2fa5b-181">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-181">✔</span></span>|<span data-ttu-id="2fa5b-182">Относительный путь к файлу .json, содержащим переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-182">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="2fa5b-183">name</span><span class="sxs-lookup"><span data-stu-id="2fa5b-183">name</span></span>

<span data-ttu-id="2fa5b-184">**Required**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-184">**Required**</span></span>

<span data-ttu-id="2fa5b-185">Имя приложения, отображаемого пользователям в Teams.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-185">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="2fa5b-186">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-186">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="2fa5b-187">Значения и `short` не `full` должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-187">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="2fa5b-188">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-188">Name</span></span>| <span data-ttu-id="2fa5b-189">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-189">Maximum size</span></span> | <span data-ttu-id="2fa5b-190">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-190">Required</span></span> | <span data-ttu-id="2fa5b-191">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-191">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="2fa5b-192">30 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-192">30 characters</span></span>|<span data-ttu-id="2fa5b-193">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-193">✔</span></span>|<span data-ttu-id="2fa5b-194">Короткое имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-194">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="2fa5b-195">100 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-195">100 characters</span></span>||<span data-ttu-id="2fa5b-196">Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-196">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="2fa5b-197">description</span><span class="sxs-lookup"><span data-stu-id="2fa5b-197">description</span></span>

<span data-ttu-id="2fa5b-198">**Required**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-198">**Required**</span></span>

<span data-ttu-id="2fa5b-199">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-199">Describes your app to users.</span></span> <span data-ttu-id="2fa5b-200">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-200">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="2fa5b-201">Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, чтобы помочь потенциальным клиентам понять, что делает ваш опыт.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-201">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="2fa5b-202">В полном описании также следует отметить, если для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-202">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="2fa5b-203">Значения и `short` не `full` должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-203">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="2fa5b-204">Короткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-204">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="2fa5b-205">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-205">Name</span></span>| <span data-ttu-id="2fa5b-206">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-206">Maximum size</span></span> | <span data-ttu-id="2fa5b-207">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-207">Required</span></span> | <span data-ttu-id="2fa5b-208">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-208">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="2fa5b-209">80 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-209">80 characters</span></span>|<span data-ttu-id="2fa5b-210">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-210">✔</span></span>|<span data-ttu-id="2fa5b-211">Краткое описание работы приложения, используемого при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-211">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="2fa5b-212">4000 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-212">4000 characters</span></span>|<span data-ttu-id="2fa5b-213">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-213">✔</span></span>|<span data-ttu-id="2fa5b-214">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-214">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="2fa5b-215">icons</span><span class="sxs-lookup"><span data-stu-id="2fa5b-215">icons</span></span>

<span data-ttu-id="2fa5b-216">**Required**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-216">**Required**</span></span>

<span data-ttu-id="2fa5b-217">Значки, используемые в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-217">Icons used within the Teams app.</span></span> <span data-ttu-id="2fa5b-218">Файлы значков должны быть включены в пакет отправки.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-218">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="2fa5b-219">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-219">Name</span></span>| <span data-ttu-id="2fa5b-220">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-220">Maximum size</span></span> | <span data-ttu-id="2fa5b-221">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-221">Required</span></span> | <span data-ttu-id="2fa5b-222">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-222">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="2fa5b-223">2048 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-223">2048 characters</span></span>|<span data-ttu-id="2fa5b-224">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-224">✔</span></span>|<span data-ttu-id="2fa5b-225">Относительный путь к прозрачному значку контура PNG 32x32.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-225">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="2fa5b-226">2048 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-226">2048 characters</span></span>|<span data-ttu-id="2fa5b-227">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-227">✔</span></span>|<span data-ttu-id="2fa5b-228">Относительный путь к значку PNG полного цвета 192x192.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-228">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="2fa5b-229">accentColor</span><span class="sxs-lookup"><span data-stu-id="2fa5b-229">accentColor</span></span>

<span data-ttu-id="2fa5b-230">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-230">**Required** &ndash; String</span></span>

<span data-ttu-id="2fa5b-231">Цвет, который можно использовать в сочетании с и в качестве фона для значков контура.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-231">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="2fa5b-232">Значение должно быть допустимым цветовым кодом HTML, начиная, например, с `#4464ee` "#".</span><span class="sxs-lookup"><span data-stu-id="2fa5b-232">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="2fa5b-233">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="2fa5b-233">configurableTabs</span></span>

<span data-ttu-id="2fa5b-234">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-234">**Optional**</span></span>

<span data-ttu-id="2fa5b-235">Используется, когда в вашем приложении есть опыт работы с вкладками канала команды, которая требует дополнительной конфигурации перед ее добавлением.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-235">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="2fa5b-236">Настраиваемые вкладки поддерживаются только в области команд, и в настоящее время поддерживается только одна вкладка для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-236">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="2fa5b-237">Объект — массив со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-237">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="2fa5b-238">Этот блок требуется только для решений, которые предоставляют настраиваемое решение вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-238">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="2fa5b-239">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-239">Name</span></span>| <span data-ttu-id="2fa5b-240">Тип</span><span class="sxs-lookup"><span data-stu-id="2fa5b-240">Type</span></span>| <span data-ttu-id="2fa5b-241">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-241">Maximum size</span></span> | <span data-ttu-id="2fa5b-242">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-242">Required</span></span> | <span data-ttu-id="2fa5b-243">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="2fa5b-244">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-244">String</span></span>|<span data-ttu-id="2fa5b-245">2048 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-245">2048 characters</span></span>|<span data-ttu-id="2fa5b-246">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-246">✔</span></span>|<span data-ttu-id="2fa5b-247">URL-https://, который можно использовать при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-247">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="2fa5b-248">Логический</span><span class="sxs-lookup"><span data-stu-id="2fa5b-248">Boolean</span></span>|||<span data-ttu-id="2fa5b-249">Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="2fa5b-250">По умолчанию: `true`</span><span class="sxs-lookup"><span data-stu-id="2fa5b-250">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="2fa5b-251">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="2fa5b-251">Array of enum</span></span>|<span data-ttu-id="2fa5b-252">1</span><span class="sxs-lookup"><span data-stu-id="2fa5b-252">1</span></span>|<span data-ttu-id="2fa5b-253">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-253">✔</span></span>|<span data-ttu-id="2fa5b-254">В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-254">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="2fa5b-255">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-255">String</span></span>|<span data-ttu-id="2fa5b-256">2048</span><span class="sxs-lookup"><span data-stu-id="2fa5b-256">2048</span></span>||<span data-ttu-id="2fa5b-257">Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="2fa5b-258">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="2fa5b-259">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="2fa5b-259">Array of enum</span></span>|<span data-ttu-id="2fa5b-260">1</span><span class="sxs-lookup"><span data-stu-id="2fa5b-260">1</span></span>||<span data-ttu-id="2fa5b-261">Определяет, как вкладка будет доступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="2fa5b-262">Параметры `sharePointFullPage` и `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="2fa5b-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="2fa5b-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="2fa5b-263">staticTabs</span></span>

<span data-ttu-id="2fa5b-264">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-264">**Optional**</span></span>

<span data-ttu-id="2fa5b-265">Определяет набор вкладок, которые можно "прикрепить" по умолчанию, не добавляя их вручную.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="2fa5b-266">Статические вкладки, объявленные в области, всегда прикрепяются к личному опыту `personal` приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="2fa5b-267">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="2fa5b-268">Отрисуйка вкладок с адаптивными картами, указав вместо в `contentBotId` `contentUrl` **блоке staticTabs.**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-268">Render tabs with Adaptive Cards by specifying `contentBotId` instead of `contentUrl` in the **staticTabs** block.</span></span>

<span data-ttu-id="2fa5b-269">Объект — массив (не более 16 элементов) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="2fa5b-270">Этот блок требуется только для решений, которые предоставляют статическое решение вкладки.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-270">This block is required only for solutions that provide a static tab solution.</span></span>


|<span data-ttu-id="2fa5b-271">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-271">Name</span></span>| <span data-ttu-id="2fa5b-272">Тип</span><span class="sxs-lookup"><span data-stu-id="2fa5b-272">Type</span></span>| <span data-ttu-id="2fa5b-273">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-273">Maximum size</span></span> | <span data-ttu-id="2fa5b-274">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-274">Required</span></span> | <span data-ttu-id="2fa5b-275">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="2fa5b-276">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-276">String</span></span>|<span data-ttu-id="2fa5b-277">64 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-277">64 characters</span></span>|<span data-ttu-id="2fa5b-278">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-278">✔</span></span>|<span data-ttu-id="2fa5b-279">Уникальный идентификатор для объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="2fa5b-280">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-280">String</span></span>|<span data-ttu-id="2fa5b-281">128 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-281">128 characters</span></span>|<span data-ttu-id="2fa5b-282">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-282">✔</span></span>|<span data-ttu-id="2fa5b-283">Отображение имени вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="2fa5b-284">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-284">String</span></span>|<span data-ttu-id="2fa5b-285">2048 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-285">2048 characters</span></span>|<span data-ttu-id="2fa5b-286">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-286">✔</span></span>|<span data-ttu-id="2fa5b-287">URL https://, который указывает на пользовательский интерфейс объекта, отображаемого на Teams холсте.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`contentBotId`|   | | | <span data-ttu-id="2fa5b-288">ID Microsoft Teams, указанный для бота на портале Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-288">The Microsoft Teams app ID specified for the bot in the Bot Framework portal.</span></span> |
|`websiteUrl`|<span data-ttu-id="2fa5b-289">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-289">String</span></span>|<span data-ttu-id="2fa5b-290">2048 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-290">2048 characters</span></span>||<span data-ttu-id="2fa5b-291">В https:// нужно указать URL-адрес, если пользователь выбирает просмотр в браузере.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-291">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="2fa5b-292">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="2fa5b-292">Array of enum</span></span>|<span data-ttu-id="2fa5b-293">1</span><span class="sxs-lookup"><span data-stu-id="2fa5b-293">1</span></span>|<span data-ttu-id="2fa5b-294">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-294">✔</span></span>|<span data-ttu-id="2fa5b-295">В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в `personal` рамках личного опыта.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-295">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="2fa5b-296">боты</span><span class="sxs-lookup"><span data-stu-id="2fa5b-296">bots</span></span>

<span data-ttu-id="2fa5b-297">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-297">**Optional**</span></span>

<span data-ttu-id="2fa5b-298">Определяет решение бота, а также необязательные сведения, такие как свойства команд по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-298">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="2fa5b-299">Объект — массив (максимум 1 элемент в настоящее время разрешен только для одного бота в приложении) со всеми &mdash; элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-299">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="2fa5b-300">Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-300">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="2fa5b-301">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-301">Name</span></span>| <span data-ttu-id="2fa5b-302">Тип</span><span class="sxs-lookup"><span data-stu-id="2fa5b-302">Type</span></span>| <span data-ttu-id="2fa5b-303">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-303">Maximum size</span></span> | <span data-ttu-id="2fa5b-304">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-304">Required</span></span> | <span data-ttu-id="2fa5b-305">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-305">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="2fa5b-306">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-306">String</span></span>|<span data-ttu-id="2fa5b-307">64 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-307">64 characters</span></span>|<span data-ttu-id="2fa5b-308">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-308">✔</span></span>|<span data-ttu-id="2fa5b-309">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-309">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="2fa5b-310">Это вполне может быть таким же, как общий [ID приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="2fa5b-310">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="2fa5b-311">Логический</span><span class="sxs-lookup"><span data-stu-id="2fa5b-311">Boolean</span></span>|||<span data-ttu-id="2fa5b-312">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-312">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="2fa5b-313">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="2fa5b-313">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="2fa5b-314">Логический</span><span class="sxs-lookup"><span data-stu-id="2fa5b-314">Boolean</span></span>|||<span data-ttu-id="2fa5b-315">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-315">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="2fa5b-316">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="2fa5b-316">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="2fa5b-317">Логический</span><span class="sxs-lookup"><span data-stu-id="2fa5b-317">Boolean</span></span>|||<span data-ttu-id="2fa5b-318">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-318">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="2fa5b-319">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="2fa5b-319">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="2fa5b-320">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="2fa5b-320">Array of enum</span></span>|<span data-ttu-id="2fa5b-321">3</span><span class="sxs-lookup"><span data-stu-id="2fa5b-321">3</span></span>|<span data-ttu-id="2fa5b-322">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-322">✔</span></span>|<span data-ttu-id="2fa5b-323">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="2fa5b-323">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="2fa5b-324">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-324">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="2fa5b-325">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="2fa5b-325">bots.commandLists</span></span>

<span data-ttu-id="2fa5b-326">Необязательный список команд, которые бот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-326">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="2fa5b-327">Объект — массив (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-327">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="2fa5b-328">Дополнительные сведения см. в [меню Bot.](~/bots/how-to/create-a-bot-commands-menu.md)</span><span class="sxs-lookup"><span data-stu-id="2fa5b-328">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="2fa5b-329">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-329">Name</span></span>| <span data-ttu-id="2fa5b-330">Тип</span><span class="sxs-lookup"><span data-stu-id="2fa5b-330">Type</span></span>| <span data-ttu-id="2fa5b-331">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-331">Maximum size</span></span> | <span data-ttu-id="2fa5b-332">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-332">Required</span></span> | <span data-ttu-id="2fa5b-333">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-333">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="2fa5b-334">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="2fa5b-334">array of enum</span></span>|<span data-ttu-id="2fa5b-335">3</span><span class="sxs-lookup"><span data-stu-id="2fa5b-335">3</span></span>|<span data-ttu-id="2fa5b-336">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-336">✔</span></span>|<span data-ttu-id="2fa5b-337">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-337">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="2fa5b-338">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-338">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="2fa5b-339">массив объектов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-339">array of objects</span></span>|<span data-ttu-id="2fa5b-340">10 </span><span class="sxs-lookup"><span data-stu-id="2fa5b-340">10</span></span>|<span data-ttu-id="2fa5b-341">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-341">✔</span></span>|<span data-ttu-id="2fa5b-342">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="2fa5b-342">An array of commands the bot supports:</span></span><br><span data-ttu-id="2fa5b-343">`title`: имя команды бота (строка, 32).</span><span class="sxs-lookup"><span data-stu-id="2fa5b-343">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="2fa5b-344">`description`: простое описание или пример синтаксиса команды и его аргумента (строка, 128).</span><span class="sxs-lookup"><span data-stu-id="2fa5b-344">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="2fa5b-345">соединители</span><span class="sxs-lookup"><span data-stu-id="2fa5b-345">connectors</span></span>

<span data-ttu-id="2fa5b-346">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-346">**Optional**</span></span>

<span data-ttu-id="2fa5b-347">Блок `connectors` определяет Office 365 соединители для приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-347">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="2fa5b-348">Объект — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-348">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="2fa5b-349">Этот блок необходим только для решений, которые предоставляют соединители.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-349">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="2fa5b-350">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-350">Name</span></span>| <span data-ttu-id="2fa5b-351">Тип</span><span class="sxs-lookup"><span data-stu-id="2fa5b-351">Type</span></span>| <span data-ttu-id="2fa5b-352">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-352">Maximum size</span></span> | <span data-ttu-id="2fa5b-353">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-353">Required</span></span> | <span data-ttu-id="2fa5b-354">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-354">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="2fa5b-355">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-355">String</span></span>|<span data-ttu-id="2fa5b-356">2048 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-356">2048 characters</span></span>|<span data-ttu-id="2fa5b-357">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-357">✔</span></span>|<span data-ttu-id="2fa5b-358">URL https://, который необходимо использовать при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-358">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="2fa5b-359">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-359">String</span></span>|<span data-ttu-id="2fa5b-360">64 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-360">64 characters</span></span>|<span data-ttu-id="2fa5b-361">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-361">✔</span></span>|<span data-ttu-id="2fa5b-362">Уникальный идентификатор соединитетеля, который соответствует его идентификатору в панели мониторинга разработчиков [соединителок.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="2fa5b-362">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="2fa5b-363">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="2fa5b-363">Array of enum</span></span>|<span data-ttu-id="2fa5b-364">1</span><span class="sxs-lookup"><span data-stu-id="2fa5b-364">1</span></span>|<span data-ttu-id="2fa5b-365">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-365">✔</span></span>|<span data-ttu-id="2fa5b-366">Указывает, предоставляет ли соединители опыт в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="2fa5b-366">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="2fa5b-367">В настоящее время `team` поддерживается только область.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-367">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="2fa5b-368">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="2fa5b-368">composeExtensions</span></span>

<span data-ttu-id="2fa5b-369">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-369">**Optional**</span></span>

<span data-ttu-id="2fa5b-370">Определяет расширение обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-370">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa5b-371">В ноябре 2017 г. имя функции было изменено с "расширение составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжили функционировать.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-371">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="2fa5b-372">Объект — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-372">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="2fa5b-373">Этот блок необходим только для решений, которые предоставляют расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-373">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="2fa5b-374">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-374">Name</span></span>| <span data-ttu-id="2fa5b-375">Тип</span><span class="sxs-lookup"><span data-stu-id="2fa5b-375">Type</span></span> | <span data-ttu-id="2fa5b-376">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-376">Maximum Size</span></span> | <span data-ttu-id="2fa5b-377">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-377">Required</span></span> | <span data-ttu-id="2fa5b-378">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-378">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="2fa5b-379">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-379">String</span></span>|<span data-ttu-id="2fa5b-380">64</span><span class="sxs-lookup"><span data-stu-id="2fa5b-380">64</span></span>|<span data-ttu-id="2fa5b-381">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-381">✔</span></span>|<span data-ttu-id="2fa5b-382">Уникальный ID приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрирован в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-382">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="2fa5b-383">Это вполне может быть таким же, как общий [ID приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="2fa5b-383">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="2fa5b-384">Логический</span><span class="sxs-lookup"><span data-stu-id="2fa5b-384">Boolean</span></span>|||<span data-ttu-id="2fa5b-385">Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-385">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="2fa5b-386">Значение по умолчанию: `false`.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-386">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="2fa5b-387">Массив объекта</span><span class="sxs-lookup"><span data-stu-id="2fa5b-387">Array of object</span></span>|<span data-ttu-id="2fa5b-388">10 </span><span class="sxs-lookup"><span data-stu-id="2fa5b-388">10</span></span>|<span data-ttu-id="2fa5b-389">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-389">✔</span></span>|<span data-ttu-id="2fa5b-390">Массив команд, поддерживаемых расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="2fa5b-390">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="2fa5b-391">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="2fa5b-391">composeExtensions.commands</span></span>

<span data-ttu-id="2fa5b-392">Расширение обмена сообщениями должно объявлять одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-392">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="2fa5b-393">Каждая команда отображается Microsoft Teams как потенциальное взаимодействие с точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-393">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="2fa5b-394">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-394">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="2fa5b-395">Каждый элемент команды — это объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="2fa5b-395">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="2fa5b-396">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-396">Name</span></span>| <span data-ttu-id="2fa5b-397">Тип</span><span class="sxs-lookup"><span data-stu-id="2fa5b-397">Type</span></span>| <span data-ttu-id="2fa5b-398">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-398">Maximum size</span></span> | <span data-ttu-id="2fa5b-399">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-399">Required</span></span> | <span data-ttu-id="2fa5b-400">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-400">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="2fa5b-401">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-401">String</span></span>|<span data-ttu-id="2fa5b-402">64 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-402">64 characters</span></span>|<span data-ttu-id="2fa5b-403">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-403">✔</span></span>|<span data-ttu-id="2fa5b-404">ID для команды.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-404">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="2fa5b-405">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-405">String</span></span>|<span data-ttu-id="2fa5b-406">64 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-406">64 characters</span></span>||<span data-ttu-id="2fa5b-407">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-407">Type of the command.</span></span> <span data-ttu-id="2fa5b-408">Один `query` из или `action` .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-408">One of `query` or `action`.</span></span> <span data-ttu-id="2fa5b-409">По умолчанию: `query`</span><span class="sxs-lookup"><span data-stu-id="2fa5b-409">Default: `query`</span></span>|
|`title`|<span data-ttu-id="2fa5b-410">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-410">String</span></span>|<span data-ttu-id="2fa5b-411">32 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-411">32 characters</span></span>|<span data-ttu-id="2fa5b-412">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-412">✔</span></span>|<span data-ttu-id="2fa5b-413">Удобное имя команды.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-413">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="2fa5b-414">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-414">String</span></span>|<span data-ttu-id="2fa5b-415">128 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-415">128 characters</span></span>||<span data-ttu-id="2fa5b-416">В описании, которое отображается пользователями, указывается назначение этой команды.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-416">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="2fa5b-417">Логический</span><span class="sxs-lookup"><span data-stu-id="2fa5b-417">Boolean</span></span>|||<span data-ttu-id="2fa5b-418">Значение Boolean, которое указывает, следует ли запускать команду изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-418">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="2fa5b-419">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="2fa5b-419">Default: `false`</span></span>|
|`context`|<span data-ttu-id="2fa5b-420">Массив строк</span><span class="sxs-lookup"><span data-stu-id="2fa5b-420">Array of Strings</span></span>|<span data-ttu-id="2fa5b-421">3</span><span class="sxs-lookup"><span data-stu-id="2fa5b-421">3</span></span>||<span data-ttu-id="2fa5b-422">Определяет, из чего можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-422">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="2fa5b-423">Любое сочетание `compose` `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-423">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="2fa5b-424">Значение по умолчанию: `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="2fa5b-424">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="2fa5b-425">Логический</span><span class="sxs-lookup"><span data-stu-id="2fa5b-425">Boolean</span></span>|||<span data-ttu-id="2fa5b-426">Значение boolean, которое указывает, следует ли динамически получать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-426">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="2fa5b-427">Объект</span><span class="sxs-lookup"><span data-stu-id="2fa5b-427">Object</span></span>|||<span data-ttu-id="2fa5b-428">Укажите модуль задач для предварительной загрузки при использовании команды расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-428">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="2fa5b-429">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-429">String</span></span>|<span data-ttu-id="2fa5b-430">64</span><span class="sxs-lookup"><span data-stu-id="2fa5b-430">64</span></span>||<span data-ttu-id="2fa5b-431">Начальное название диалогов.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-431">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="2fa5b-432">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-432">String</span></span>|||<span data-ttu-id="2fa5b-433">Ширина диалогов — число в пикселях или макет по умолчанию, такие как "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="2fa5b-433">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="2fa5b-434">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-434">String</span></span>|||<span data-ttu-id="2fa5b-435">Высота диалогов — число пикселей или макет по умолчанию, например "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="2fa5b-435">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="2fa5b-436">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-436">String</span></span>|||<span data-ttu-id="2fa5b-437">Начальный URL-адрес веб-просмотров.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-437">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="2fa5b-438">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-438">Array of Objects</span></span>|<span data-ttu-id="2fa5b-439">5 </span><span class="sxs-lookup"><span data-stu-id="2fa5b-439">5</span></span>||<span data-ttu-id="2fa5b-440">Список обработчиков, которые позволяют вызывать приложения при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-440">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="2fa5b-441">Домены также должны быть указаны в `validDomains` .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-441">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="2fa5b-442">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-442">String</span></span>|||<span data-ttu-id="2fa5b-443">Тип обработка сообщений.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-443">The type of message handler.</span></span> <span data-ttu-id="2fa5b-444">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-444">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="2fa5b-445">Массив строк</span><span class="sxs-lookup"><span data-stu-id="2fa5b-445">Array of Strings</span></span>|||<span data-ttu-id="2fa5b-446">Массив доменов, для которые обработник сообщений ссылок может зарегистрироваться.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-446">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="2fa5b-447">Массив объекта</span><span class="sxs-lookup"><span data-stu-id="2fa5b-447">Array of object</span></span>|<span data-ttu-id="2fa5b-448">5 </span><span class="sxs-lookup"><span data-stu-id="2fa5b-448">5</span></span>|<span data-ttu-id="2fa5b-449">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-449">✔</span></span>|<span data-ttu-id="2fa5b-450">Список параметров, которые принимает команда.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-450">The list of parameters the command takes.</span></span> <span data-ttu-id="2fa5b-451">Минимум: 1; максимум: 5</span><span class="sxs-lookup"><span data-stu-id="2fa5b-451">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="2fa5b-452">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-452">String</span></span>|<span data-ttu-id="2fa5b-453">64 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-453">64 characters</span></span>|<span data-ttu-id="2fa5b-454">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-454">✔</span></span>|<span data-ttu-id="2fa5b-455">Имя параметра, как оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-455">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="2fa5b-456">Это включено в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-456">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="2fa5b-457">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-457">String</span></span>|<span data-ttu-id="2fa5b-458">32 символа</span><span class="sxs-lookup"><span data-stu-id="2fa5b-458">32 characters</span></span>|<span data-ttu-id="2fa5b-459">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-459">✔</span></span>|<span data-ttu-id="2fa5b-460">Удобное название для параметра.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-460">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="2fa5b-461">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-461">String</span></span>|<span data-ttu-id="2fa5b-462">128 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-462">128 characters</span></span>||<span data-ttu-id="2fa5b-463">Удобное для пользователя строка, описываемая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-463">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="2fa5b-464">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-464">String</span></span>|<span data-ttu-id="2fa5b-465">128 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-465">128 characters</span></span>||<span data-ttu-id="2fa5b-466">Определяет тип управления, отображаемого в модуле задач `fetchTask: true` для .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-466">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="2fa5b-467">Один `text` из `textarea` , , , , , `number` `date` `time` `toggle` `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-467">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="2fa5b-468">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-468">Array of Objects</span></span>|<span data-ttu-id="2fa5b-469">10 </span><span class="sxs-lookup"><span data-stu-id="2fa5b-469">10</span></span>||<span data-ttu-id="2fa5b-470">Параметры выбора `choiceset` для .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-470">The choice options for the `choiceset`.</span></span> <span data-ttu-id="2fa5b-471">Используйте только `parameter.inputType` тогда, когда `choiceset` это .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-471">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="2fa5b-472">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-472">String</span></span>|<span data-ttu-id="2fa5b-473">128</span><span class="sxs-lookup"><span data-stu-id="2fa5b-473">128</span></span>||<span data-ttu-id="2fa5b-474">Название выбора.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-474">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="2fa5b-475">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-475">String</span></span>|<span data-ttu-id="2fa5b-476">512</span><span class="sxs-lookup"><span data-stu-id="2fa5b-476">512</span></span>||<span data-ttu-id="2fa5b-477">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-477">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="2fa5b-478">permissions</span><span class="sxs-lookup"><span data-stu-id="2fa5b-478">permissions</span></span>

<span data-ttu-id="2fa5b-479">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-479">**Optional**</span></span>

<span data-ttu-id="2fa5b-480">Массив указывает, какие разрешения запрашивает приложение, что позволяет конечным пользователям узнать, как `string` будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-480">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="2fa5b-481">Следующие параметры не являются эксклюзивными:</span><span class="sxs-lookup"><span data-stu-id="2fa5b-481">The following options are non-exclusive:</span></span>

* <span data-ttu-id="2fa5b-482">`identity`&emsp;Требуется информация о удостоверении пользователя.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-482">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="2fa5b-483">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам группы.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-483">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="2fa5b-484">Изменение этих разрешений при обновлении приложения приведет к тому, что пользователи повторят процесс согласия при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-484">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="2fa5b-485">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="2fa5b-485">devicePermissions</span></span>

<span data-ttu-id="2fa5b-486">**Необязательный** Массив строк</span><span class="sxs-lookup"><span data-stu-id="2fa5b-486">**Optional** Array of Strings</span></span>

<span data-ttu-id="2fa5b-487">Указывает родных функций на устройстве пользователя, к которое ваше приложение может запрашивать доступ.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-487">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="2fa5b-488">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="2fa5b-488">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="2fa5b-489">validDomains</span><span class="sxs-lookup"><span data-stu-id="2fa5b-489">validDomains</span></span>

<span data-ttu-id="2fa5b-490">**Необязательный,** за **исключением обязательного,** где отмечено</span><span class="sxs-lookup"><span data-stu-id="2fa5b-490">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="2fa5b-491">Список допустимого домена, из которого приложение ожидает загрузки любого контента.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-491">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="2fa5b-492">Списки домена могут включать, например, поддиайки. `*.example.com`</span><span class="sxs-lookup"><span data-stu-id="2fa5b-492">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="2fa5b-493">Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-493">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="2fa5b-494">Если конфигурации вкладок или пользовательскому интерфейсу контента необходимо перейти к любому другому домену, кроме одного использования для конфигурации вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-494">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="2fa5b-495">Однако не **обязательно** включать в приложение домены поставщиков удостоверений, которые вы хотите поддерживать.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-495">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="2fa5b-496">Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить на accounts.google.com, но не следует включать accounts.google.com `validDomains[]` в .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-496">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fa5b-497">Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью подкрентов.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-497">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="2fa5b-498">Например, `yourapp.onmicrosoft.com` допустимо, `*.onmicrosoft.com` но не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-498">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="2fa5b-499">Объект — массив со всеми элементами `string` типа.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-499">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="2fa5b-500">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="2fa5b-500">webApplicationInfo</span></span>

<span data-ttu-id="2fa5b-501">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="2fa5b-501">**Optional**</span></span>

<span data-ttu-id="2fa5b-502">Укажите свой AAD-ID и Graph, чтобы помочь пользователям легко войти в ваше приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-502">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="2fa5b-503">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-503">Name</span></span>| <span data-ttu-id="2fa5b-504">Тип</span><span class="sxs-lookup"><span data-stu-id="2fa5b-504">Type</span></span>| <span data-ttu-id="2fa5b-505">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-505">Maximum size</span></span> | <span data-ttu-id="2fa5b-506">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-506">Required</span></span> | <span data-ttu-id="2fa5b-507">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-507">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="2fa5b-508">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-508">String</span></span>|<span data-ttu-id="2fa5b-509">36 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-509">36 characters</span></span>|<span data-ttu-id="2fa5b-510">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-510">✔</span></span>|<span data-ttu-id="2fa5b-511">AAD-id приложения приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-511">AAD application id of the app.</span></span> <span data-ttu-id="2fa5b-512">Этот id должен быть GUID.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-512">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="2fa5b-513">String</span><span class="sxs-lookup"><span data-stu-id="2fa5b-513">String</span></span>|<span data-ttu-id="2fa5b-514">2048 символов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-514">2048 characters</span></span>|<span data-ttu-id="2fa5b-515">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-515">✔</span></span>|<span data-ttu-id="2fa5b-516">URL-адрес ресурса приложения для приобретения маркера auth для SSO.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-516">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="2fa5b-517">Массив</span><span class="sxs-lookup"><span data-stu-id="2fa5b-517">Array</span></span>|<span data-ttu-id="2fa5b-518">Не более 100 элементов</span><span class="sxs-lookup"><span data-stu-id="2fa5b-518">Maximum 100 items</span></span>|<span data-ttu-id="2fa5b-519">✔</span><span class="sxs-lookup"><span data-stu-id="2fa5b-519">✔</span></span>|<span data-ttu-id="2fa5b-520">Разрешения ресурсов для приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-520">Resource permissions for application.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="2fa5b-521">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="2fa5b-521">configurableProperties</span></span>

<span data-ttu-id="2fa5b-522">**Необязательный** - массив</span><span class="sxs-lookup"><span data-stu-id="2fa5b-522">**Optional** - array</span></span>

<span data-ttu-id="2fa5b-523">Блок определяет свойства приложений, которые могут `configurableProperties` Teams администраторы.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-523">The `configurableProperties` block defines the app properties that Teams admins can customize.</span></span> <span data-ttu-id="2fa5b-524">Дополнительные сведения см. в [приложении Enable customization.](~/concepts/design/enable-app-customization.md)</span><span class="sxs-lookup"><span data-stu-id="2fa5b-524">For more information, see [enable app customization](~/concepts/design/enable-app-customization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2fa5b-525">Необходимо определить как минимум одно свойство.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-525">A minimum of one property must be defined.</span></span> <span data-ttu-id="2fa5b-526">В этом блоке можно определить максимум девять свойств.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-526">You can define a maximum of nine properties in this block.</span></span>

<span data-ttu-id="2fa5b-527">Можно определить любое из следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="2fa5b-527">You can define any of the following properties:</span></span>

* <span data-ttu-id="2fa5b-528">`name`: Имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-528">`name`: The app's display name.</span></span>
* <span data-ttu-id="2fa5b-529">`shortDescription`Краткое описание приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-529">`shortDescription`: The app's short description.</span></span>
* <span data-ttu-id="2fa5b-530">`longDescription`Подробное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-530">`longDescription`: The app's detailed description.</span></span>
* <span data-ttu-id="2fa5b-531">`smallImageUrl`: Значок контура приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-531">`smallImageUrl`: The app's outline icon.</span></span>
* <span data-ttu-id="2fa5b-532">`largeImageUrl`: Значок цвета приложения.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-532">`largeImageUrl`: The app's color icon.</span></span>
* <span data-ttu-id="2fa5b-533">`accentColor`: Цвет, который нужно использовать в сочетании с и в качестве фона для значков контура.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-533">`accentColor`: The color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="2fa5b-534">`developerUrl`URL-адрес HTTPS веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-534">`developerUrl`: The HTTPS URL of the developer's website.</span></span>
* <span data-ttu-id="2fa5b-535">`privacyUrl`: URL-адрес HTTPS политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-535">`privacyUrl`: The HTTPS URL of the developer's privacy policy.</span></span>
* <span data-ttu-id="2fa5b-536">`termsOfUseUrl`: URL-адрес HTTPS условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-536">`termsOfUseUrl`: The HTTPS URL of the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="2fa5b-537">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="2fa5b-537">defaultInstallScope</span></span>

<span data-ttu-id="2fa5b-538">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="2fa5b-538">**Optional** - string</span></span>

<span data-ttu-id="2fa5b-539">Указывает область установки, определяемую для этого приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-539">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="2fa5b-540">Определенным областью будет параметр, отображаемый на кнопке при добавлении приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-540">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="2fa5b-541">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="2fa5b-541">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="2fa5b-542">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="2fa5b-542">defaultGroupCapability</span></span>

<span data-ttu-id="2fa5b-543">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="2fa5b-543">**Optional** - object</span></span>

<span data-ttu-id="2fa5b-544">Когда будет выбрана область установки группы, она определит возможности по умолчанию при установке приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-544">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="2fa5b-545">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="2fa5b-545">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="2fa5b-546">Имя</span><span class="sxs-lookup"><span data-stu-id="2fa5b-546">Name</span></span>| <span data-ttu-id="2fa5b-547">Тип</span><span class="sxs-lookup"><span data-stu-id="2fa5b-547">Type</span></span>| <span data-ttu-id="2fa5b-548">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="2fa5b-548">Maximum size</span></span> | <span data-ttu-id="2fa5b-549">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2fa5b-549">Required</span></span> | <span data-ttu-id="2fa5b-550">Описание</span><span class="sxs-lookup"><span data-stu-id="2fa5b-550">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="2fa5b-551">string</span><span class="sxs-lookup"><span data-stu-id="2fa5b-551">string</span></span>|||<span data-ttu-id="2fa5b-552">Если выбрана область установки, это поле указывает доступные возможности `team` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-552">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="2fa5b-553">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-553">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="2fa5b-554">строка</span><span class="sxs-lookup"><span data-stu-id="2fa5b-554">string</span></span>|||<span data-ttu-id="2fa5b-555">Если выбрана область установки, это поле указывает доступные возможности `groupchat` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-555">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="2fa5b-556">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-556">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="2fa5b-557">строка</span><span class="sxs-lookup"><span data-stu-id="2fa5b-557">string</span></span>|||<span data-ttu-id="2fa5b-558">Если выбрана область установки, это поле указывает доступные возможности `meetings` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2fa5b-558">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="2fa5b-559">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="2fa5b-559">Options: `tab`, `bot`, or `connector`.</span></span>|
