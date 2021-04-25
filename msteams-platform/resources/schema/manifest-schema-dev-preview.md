---
title: Developer Preview схемы манифеста
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams
ms.topic: reference
keywords: команды проявляют схему Developer Preview
ms.date: 05/20/2019
ms.openlocfilehash: adb178000d909c9031e4b4df187bbf6f74f6e783
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946475"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="deaef-104">Схема манифеста предварительного просмотра разработчика для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="deaef-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="deaef-105">Сведения [о Developer Preview](~/resources/dev-preview/developer-preview-intro.md) и о том, как можно присоединиться, см. в Developer Preview.</span><span class="sxs-lookup"><span data-stu-id="deaef-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="deaef-106">Если вы не используете предварительный просмотр разработчика, не следует использовать эту версию манифеста.</span><span class="sxs-lookup"><span data-stu-id="deaef-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="deaef-107">См. [справку. Схема манифеста для Microsoft Teams](~/resources/schema/manifest-schema.md) для общедоступных версий манифеста.</span><span class="sxs-lookup"><span data-stu-id="deaef-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="deaef-108">Манифест Microsoft Teams описывает, как приложение интегрируется в продукт Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="deaef-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="deaef-109">Манифест должен соответствовать схеме, которая была на [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) уровне .</span><span class="sxs-lookup"><span data-stu-id="deaef-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="deaef-110">Дополнительные сведения о доступных функциях см. в фото: [Features in the Public Developer Preview для Microsoft Teams.](~/resources/dev-preview/developer-preview-features.md)</span><span class="sxs-lookup"><span data-stu-id="deaef-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="deaef-111">Образец полного манифеста</span><span class="sxs-lookup"><span data-stu-id="deaef-111">Sample full manifest</span></span>

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
   "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "websiteUrl",
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

<span data-ttu-id="deaef-112">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="deaef-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="deaef-113">$schema</span><span class="sxs-lookup"><span data-stu-id="deaef-113">$schema</span></span>

<span data-ttu-id="deaef-114">*Необязательный, но рекомендуемый* &ndash; String</span><span class="sxs-lookup"><span data-stu-id="deaef-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="deaef-115">URL https:// ссылки на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="deaef-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="deaef-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="deaef-116">manifestVersion</span></span>

<span data-ttu-id="deaef-117">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="deaef-117">**Required** &ndash; String</span></span>

<span data-ttu-id="deaef-118">Версия схемы манифеста, используемая этим манифестом.</span><span class="sxs-lookup"><span data-stu-id="deaef-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="deaef-119">Это должно быть "devPreview".</span><span class="sxs-lookup"><span data-stu-id="deaef-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="deaef-120">version</span><span class="sxs-lookup"><span data-stu-id="deaef-120">version</span></span>

<span data-ttu-id="deaef-121">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="deaef-121">**Required** &ndash; String</span></span>

<span data-ttu-id="deaef-122">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-122">The version of the specific app.</span></span> <span data-ttu-id="deaef-123">Если вы что-то обновляете в манифесте, необходимо также приумножная версия.</span><span class="sxs-lookup"><span data-stu-id="deaef-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="deaef-124">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="deaef-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="deaef-125">Если это приложение было отправлено в магазин, новый манифест должен быть повторно отправлен и повторно проверен.</span><span class="sxs-lookup"><span data-stu-id="deaef-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="deaef-126">Затем пользователи этого приложения получат новый обновленный манифест автоматически через несколько часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="deaef-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="deaef-127">Если приложение запрашивает разрешения изменить, пользователям будет предложено обновить и повторно согласиться на приложение.</span><span class="sxs-lookup"><span data-stu-id="deaef-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="deaef-128">Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="deaef-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="deaef-129">id</span><span class="sxs-lookup"><span data-stu-id="deaef-129">id</span></span>

<span data-ttu-id="deaef-130">**Обязательно** &ndash; ID приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="deaef-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="deaef-131">Уникальный идентификатор, созданный Корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="deaef-132">Если вы зарегистрировали бота через Microsoft Bot Framework или веб-приложение вашей вкладки уже входит в Microsoft, у вас уже должен быть ID, который необходимо ввести здесь.</span><span class="sxs-lookup"><span data-stu-id="deaef-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="deaef-133">В противном случае необходимо создать новый ID на портале регистрации приложений Microsoft[(Мои](https://apps.dev.microsoft.com)приложения), введите его здесь, а затем повторно использовать при добавлении [бота.](~/bots/how-to/create-a-bot-for-teams.md)</span><span class="sxs-lookup"><span data-stu-id="deaef-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="deaef-134">packageName</span><span class="sxs-lookup"><span data-stu-id="deaef-134">packageName</span></span>

<span data-ttu-id="deaef-135">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="deaef-135">**Required** &ndash; String</span></span>

<span data-ttu-id="deaef-136">Уникальный идентификатор для этого приложения в обратной нотации домена; например, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="deaef-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="deaef-137">developer</span><span class="sxs-lookup"><span data-stu-id="deaef-137">developer</span></span>

<span data-ttu-id="deaef-138">**Required**</span><span class="sxs-lookup"><span data-stu-id="deaef-138">**Required**</span></span>

<span data-ttu-id="deaef-139">Указывает сведения о вашей компании.</span><span class="sxs-lookup"><span data-stu-id="deaef-139">Specifies information about your company.</span></span> <span data-ttu-id="deaef-140">Для приложений, представленных в AppSource (ранее Office Store), эти значения должны соответствовать сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="deaef-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="deaef-141">Name</span><span class="sxs-lookup"><span data-stu-id="deaef-141">Name</span></span>| <span data-ttu-id="deaef-142">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-142">Maximum size</span></span> | <span data-ttu-id="deaef-143">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-143">Required</span></span> | <span data-ttu-id="deaef-144">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="deaef-145">32 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-145">32 characters</span></span>|<span data-ttu-id="deaef-146">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-146">✔</span></span>|<span data-ttu-id="deaef-147">Имя отображения для разработчика.</span><span class="sxs-lookup"><span data-stu-id="deaef-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="deaef-148">2048 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-148">2048 characters</span></span>|<span data-ttu-id="deaef-149">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-149">✔</span></span>|<span data-ttu-id="deaef-150">Url https:// url-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="deaef-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="deaef-151">Эта ссылка должна принимать пользователей на страницу вашей компании или конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="deaef-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="deaef-152">2048 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-152">2048 characters</span></span>|<span data-ttu-id="deaef-153">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-153">✔</span></span>|<span data-ttu-id="deaef-154">Url https:// url-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="deaef-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="deaef-155">2048 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-155">2048 characters</span></span>|<span data-ttu-id="deaef-156">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-156">✔</span></span>|<span data-ttu-id="deaef-157">Url https:// url-адрес для условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="deaef-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="deaef-158">10 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-158">10 characters</span></span>|<span data-ttu-id="deaef-159">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-159">✔</span></span>|<span data-ttu-id="deaef-160">**Необязательный** Идентификатор Сети партнеров Майкрософт, который определяет организацию-партнер, которая строит приложение.</span><span class="sxs-lookup"><span data-stu-id="deaef-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="deaef-161">локализацияInfo</span><span class="sxs-lookup"><span data-stu-id="deaef-161">localizationInfo</span></span>

<span data-ttu-id="deaef-162">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="deaef-162">**Optional**</span></span>

<span data-ttu-id="deaef-163">Позволяет спецификацию языка по умолчанию, а также указатели для дополнительных языковых файлов.</span><span class="sxs-lookup"><span data-stu-id="deaef-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="deaef-164">См. [локализацию.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="deaef-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="deaef-165">Name</span><span class="sxs-lookup"><span data-stu-id="deaef-165">Name</span></span>| <span data-ttu-id="deaef-166">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-166">Maximum size</span></span> | <span data-ttu-id="deaef-167">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-167">Required</span></span> | <span data-ttu-id="deaef-168">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="deaef-169">4 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-169">4 characters</span></span>|<span data-ttu-id="deaef-170">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-170">✔</span></span>|<span data-ttu-id="deaef-171">Языковой тег строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="deaef-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="deaef-172">локализацияInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="deaef-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="deaef-173">Массив объектов, указывающих дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="deaef-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="deaef-174">Name</span><span class="sxs-lookup"><span data-stu-id="deaef-174">Name</span></span>| <span data-ttu-id="deaef-175">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-175">Maximum size</span></span> | <span data-ttu-id="deaef-176">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-176">Required</span></span> | <span data-ttu-id="deaef-177">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="deaef-178">4 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-178">4 characters</span></span>|<span data-ttu-id="deaef-179">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-179">✔</span></span>|<span data-ttu-id="deaef-180">Языковой тег строки в предоставленного файла.</span><span class="sxs-lookup"><span data-stu-id="deaef-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="deaef-181">4 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-181">4 characters</span></span>|<span data-ttu-id="deaef-182">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-182">✔</span></span>|<span data-ttu-id="deaef-183">Относительный путь к файлу .json, содержащим переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="deaef-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="deaef-184">name</span><span class="sxs-lookup"><span data-stu-id="deaef-184">name</span></span>

<span data-ttu-id="deaef-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="deaef-185">**Required**</span></span>

<span data-ttu-id="deaef-186">Имя приложения, отображаемого пользователям в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="deaef-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="deaef-187">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="deaef-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="deaef-188">Значения и `short` не `full` должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="deaef-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="deaef-189">Name</span><span class="sxs-lookup"><span data-stu-id="deaef-189">Name</span></span>| <span data-ttu-id="deaef-190">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-190">Maximum size</span></span> | <span data-ttu-id="deaef-191">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-191">Required</span></span> | <span data-ttu-id="deaef-192">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="deaef-193">30 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-193">30 characters</span></span>|<span data-ttu-id="deaef-194">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-194">✔</span></span>|<span data-ttu-id="deaef-195">Короткое имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="deaef-196">100 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-196">100 characters</span></span>||<span data-ttu-id="deaef-197">Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="deaef-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="deaef-198">description</span><span class="sxs-lookup"><span data-stu-id="deaef-198">description</span></span>

<span data-ttu-id="deaef-199">**Required**</span><span class="sxs-lookup"><span data-stu-id="deaef-199">**Required**</span></span>

<span data-ttu-id="deaef-200">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="deaef-200">Describes your app to users.</span></span> <span data-ttu-id="deaef-201">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="deaef-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="deaef-202">Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, чтобы помочь потенциальным клиентам понять, что делает ваш опыт.</span><span class="sxs-lookup"><span data-stu-id="deaef-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="deaef-203">В полном описании также следует отметить, если для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="deaef-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="deaef-204">Значения и `short` не `full` должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="deaef-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="deaef-205">Короткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="deaef-206">Name</span><span class="sxs-lookup"><span data-stu-id="deaef-206">Name</span></span>| <span data-ttu-id="deaef-207">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-207">Maximum size</span></span> | <span data-ttu-id="deaef-208">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-208">Required</span></span> | <span data-ttu-id="deaef-209">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="deaef-210">80 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-210">80 characters</span></span>|<span data-ttu-id="deaef-211">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-211">✔</span></span>|<span data-ttu-id="deaef-212">Краткое описание работы приложения, используемого при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="deaef-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="deaef-213">4000 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-213">4000 characters</span></span>|<span data-ttu-id="deaef-214">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-214">✔</span></span>|<span data-ttu-id="deaef-215">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="deaef-216">icons</span><span class="sxs-lookup"><span data-stu-id="deaef-216">icons</span></span>

<span data-ttu-id="deaef-217">**Required**</span><span class="sxs-lookup"><span data-stu-id="deaef-217">**Required**</span></span>

<span data-ttu-id="deaef-218">Значки, используемые в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="deaef-218">Icons used within the Teams app.</span></span> <span data-ttu-id="deaef-219">Файлы значков должны быть включены в пакет отправки.</span><span class="sxs-lookup"><span data-stu-id="deaef-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="deaef-220">Name</span><span class="sxs-lookup"><span data-stu-id="deaef-220">Name</span></span>| <span data-ttu-id="deaef-221">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-221">Maximum size</span></span> | <span data-ttu-id="deaef-222">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-222">Required</span></span> | <span data-ttu-id="deaef-223">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="deaef-224">2048 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-224">2048 characters</span></span>|<span data-ttu-id="deaef-225">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-225">✔</span></span>|<span data-ttu-id="deaef-226">Относительный путь к прозрачному значку контура PNG 32x32.</span><span class="sxs-lookup"><span data-stu-id="deaef-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="deaef-227">2048 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-227">2048 characters</span></span>|<span data-ttu-id="deaef-228">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-228">✔</span></span>|<span data-ttu-id="deaef-229">Относительный путь к значку PNG полного цвета 192x192.</span><span class="sxs-lookup"><span data-stu-id="deaef-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="deaef-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="deaef-230">accentColor</span></span>

<span data-ttu-id="deaef-231">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="deaef-231">**Required** &ndash; String</span></span>

<span data-ttu-id="deaef-232">Цвет, который можно использовать в сочетании с и в качестве фона для значков контура.</span><span class="sxs-lookup"><span data-stu-id="deaef-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="deaef-233">Значение должно быть допустимым цветовым кодом HTML, начиная, например, с `#4464ee` "#".</span><span class="sxs-lookup"><span data-stu-id="deaef-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="deaef-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="deaef-234">configurableTabs</span></span>

<span data-ttu-id="deaef-235">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="deaef-235">**Optional**</span></span>

<span data-ttu-id="deaef-236">Используется, когда в вашем приложении есть опыт работы с вкладками канала команды, которая требует дополнительной конфигурации перед ее добавлением.</span><span class="sxs-lookup"><span data-stu-id="deaef-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="deaef-237">Настраиваемые вкладки поддерживаются только в области команд, и в настоящее время поддерживается только одна вкладка для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="deaef-238">Объект — массив со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="deaef-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="deaef-239">Этот блок требуется только для решений, которые предоставляют настраиваемое решение вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="deaef-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="deaef-240">Имя</span><span class="sxs-lookup"><span data-stu-id="deaef-240">Name</span></span>| <span data-ttu-id="deaef-241">Тип</span><span class="sxs-lookup"><span data-stu-id="deaef-241">Type</span></span>| <span data-ttu-id="deaef-242">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-242">Maximum size</span></span> | <span data-ttu-id="deaef-243">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-243">Required</span></span> | <span data-ttu-id="deaef-244">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="deaef-245">String</span><span class="sxs-lookup"><span data-stu-id="deaef-245">String</span></span>|<span data-ttu-id="deaef-246">2048 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-246">2048 characters</span></span>|<span data-ttu-id="deaef-247">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-247">✔</span></span>|<span data-ttu-id="deaef-248">URL-https://, который можно использовать при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="deaef-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="deaef-249">Логический</span><span class="sxs-lookup"><span data-stu-id="deaef-249">Boolean</span></span>|||<span data-ttu-id="deaef-250">Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания.</span><span class="sxs-lookup"><span data-stu-id="deaef-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="deaef-251">По умолчанию: `true`</span><span class="sxs-lookup"><span data-stu-id="deaef-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="deaef-252">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="deaef-252">Array of enum</span></span>|<span data-ttu-id="deaef-253">1</span><span class="sxs-lookup"><span data-stu-id="deaef-253">1</span></span>|<span data-ttu-id="deaef-254">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-254">✔</span></span>|<span data-ttu-id="deaef-255">В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области.</span><span class="sxs-lookup"><span data-stu-id="deaef-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="deaef-256">String</span><span class="sxs-lookup"><span data-stu-id="deaef-256">String</span></span>|<span data-ttu-id="deaef-257">2048</span><span class="sxs-lookup"><span data-stu-id="deaef-257">2048</span></span>||<span data-ttu-id="deaef-258">Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="deaef-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="deaef-259">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="deaef-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="deaef-260">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="deaef-260">Array of enum</span></span>|<span data-ttu-id="deaef-261">1</span><span class="sxs-lookup"><span data-stu-id="deaef-261">1</span></span>||<span data-ttu-id="deaef-262">Определяет, как вкладка будет доступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="deaef-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="deaef-263">Параметры `sharePointFullPage` и `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="deaef-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="deaef-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="deaef-264">staticTabs</span></span>

<span data-ttu-id="deaef-265">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="deaef-265">**Optional**</span></span>

<span data-ttu-id="deaef-266">Определяет набор вкладок, которые можно "прикрепить" по умолчанию, не добавляя их вручную.</span><span class="sxs-lookup"><span data-stu-id="deaef-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="deaef-267">Статические вкладки, объявленные в области, всегда прикрепяются к личному опыту `personal` приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="deaef-268">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="deaef-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="deaef-269">Объект — массив (не более 16 элементов) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="deaef-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="deaef-270">Этот блок требуется только для решений, которые предоставляют статическое решение вкладки.</span><span class="sxs-lookup"><span data-stu-id="deaef-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="deaef-271">Имя</span><span class="sxs-lookup"><span data-stu-id="deaef-271">Name</span></span>| <span data-ttu-id="deaef-272">Тип</span><span class="sxs-lookup"><span data-stu-id="deaef-272">Type</span></span>| <span data-ttu-id="deaef-273">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-273">Maximum size</span></span> | <span data-ttu-id="deaef-274">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-274">Required</span></span> | <span data-ttu-id="deaef-275">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="deaef-276">String</span><span class="sxs-lookup"><span data-stu-id="deaef-276">String</span></span>|<span data-ttu-id="deaef-277">64 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-277">64 characters</span></span>|<span data-ttu-id="deaef-278">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-278">✔</span></span>|<span data-ttu-id="deaef-279">Уникальный идентификатор для объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="deaef-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="deaef-280">String</span><span class="sxs-lookup"><span data-stu-id="deaef-280">String</span></span>|<span data-ttu-id="deaef-281">128 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-281">128 characters</span></span>|<span data-ttu-id="deaef-282">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-282">✔</span></span>|<span data-ttu-id="deaef-283">Отображение имени вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="deaef-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="deaef-284">String</span><span class="sxs-lookup"><span data-stu-id="deaef-284">String</span></span>|<span data-ttu-id="deaef-285">2048 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-285">2048 characters</span></span>|<span data-ttu-id="deaef-286">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-286">✔</span></span>|<span data-ttu-id="deaef-287">URL https://, который указывает на пользовательский интерфейс объекта, отображаемого на холсте Teams.</span><span class="sxs-lookup"><span data-stu-id="deaef-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="deaef-288">String</span><span class="sxs-lookup"><span data-stu-id="deaef-288">String</span></span>|<span data-ttu-id="deaef-289">2048 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-289">2048 characters</span></span>||<span data-ttu-id="deaef-290">В https:// нужно указать URL-адрес, если пользователь выбирает просмотр в браузере.</span><span class="sxs-lookup"><span data-stu-id="deaef-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="deaef-291">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="deaef-291">Array of enum</span></span>|<span data-ttu-id="deaef-292">1</span><span class="sxs-lookup"><span data-stu-id="deaef-292">1</span></span>|<span data-ttu-id="deaef-293">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-293">✔</span></span>|<span data-ttu-id="deaef-294">В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в `personal` рамках личного опыта.</span><span class="sxs-lookup"><span data-stu-id="deaef-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="deaef-295">боты</span><span class="sxs-lookup"><span data-stu-id="deaef-295">bots</span></span>

<span data-ttu-id="deaef-296">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="deaef-296">**Optional**</span></span>

<span data-ttu-id="deaef-297">Определяет решение бота, а также необязательные сведения, такие как свойства команд по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="deaef-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="deaef-298">Объект — массив (максимум 1 элемент в настоящее время разрешен только для одного бота в приложении) со всеми &mdash; элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="deaef-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="deaef-299">Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.</span><span class="sxs-lookup"><span data-stu-id="deaef-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="deaef-300">Имя</span><span class="sxs-lookup"><span data-stu-id="deaef-300">Name</span></span>| <span data-ttu-id="deaef-301">Тип</span><span class="sxs-lookup"><span data-stu-id="deaef-301">Type</span></span>| <span data-ttu-id="deaef-302">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-302">Maximum size</span></span> | <span data-ttu-id="deaef-303">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-303">Required</span></span> | <span data-ttu-id="deaef-304">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="deaef-305">String</span><span class="sxs-lookup"><span data-stu-id="deaef-305">String</span></span>|<span data-ttu-id="deaef-306">64 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-306">64 characters</span></span>|<span data-ttu-id="deaef-307">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-307">✔</span></span>|<span data-ttu-id="deaef-308">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="deaef-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="deaef-309">Это вполне может быть таким же, как общий [ID приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="deaef-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="deaef-310">Логический</span><span class="sxs-lookup"><span data-stu-id="deaef-310">Boolean</span></span>|||<span data-ttu-id="deaef-311">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="deaef-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="deaef-312">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="deaef-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="deaef-313">Логический</span><span class="sxs-lookup"><span data-stu-id="deaef-313">Boolean</span></span>|||<span data-ttu-id="deaef-314">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="deaef-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="deaef-315">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="deaef-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="deaef-316">Логический</span><span class="sxs-lookup"><span data-stu-id="deaef-316">Boolean</span></span>|||<span data-ttu-id="deaef-317">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="deaef-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="deaef-318">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="deaef-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="deaef-319">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="deaef-319">Array of enum</span></span>|<span data-ttu-id="deaef-320">3</span><span class="sxs-lookup"><span data-stu-id="deaef-320">3</span></span>|<span data-ttu-id="deaef-321">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-321">✔</span></span>|<span data-ttu-id="deaef-322">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="deaef-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="deaef-323">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="deaef-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="deaef-324">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="deaef-324">bots.commandLists</span></span>

<span data-ttu-id="deaef-325">Необязательный список команд, которые бот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="deaef-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="deaef-326">Объект — массив (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом.</span><span class="sxs-lookup"><span data-stu-id="deaef-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="deaef-327">Дополнительные [сведения см. в](~/bots/how-to/create-a-bot-commands-menu.md) меню Bot.</span><span class="sxs-lookup"><span data-stu-id="deaef-327">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="deaef-328">Имя</span><span class="sxs-lookup"><span data-stu-id="deaef-328">Name</span></span>| <span data-ttu-id="deaef-329">Тип</span><span class="sxs-lookup"><span data-stu-id="deaef-329">Type</span></span>| <span data-ttu-id="deaef-330">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-330">Maximum size</span></span> | <span data-ttu-id="deaef-331">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-331">Required</span></span> | <span data-ttu-id="deaef-332">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="deaef-333">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="deaef-333">array of enum</span></span>|<span data-ttu-id="deaef-334">3</span><span class="sxs-lookup"><span data-stu-id="deaef-334">3</span></span>|<span data-ttu-id="deaef-335">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-335">✔</span></span>|<span data-ttu-id="deaef-336">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="deaef-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="deaef-337">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="deaef-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="deaef-338">массив объектов</span><span class="sxs-lookup"><span data-stu-id="deaef-338">array of objects</span></span>|<span data-ttu-id="deaef-339">10 </span><span class="sxs-lookup"><span data-stu-id="deaef-339">10</span></span>|<span data-ttu-id="deaef-340">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-340">✔</span></span>|<span data-ttu-id="deaef-341">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="deaef-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="deaef-342">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="deaef-342">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="deaef-343">`description`: простое описание или пример синтаксиса команды и ее аргумента (строка, 128)</span><span class="sxs-lookup"><span data-stu-id="deaef-343">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="deaef-344">соединители</span><span class="sxs-lookup"><span data-stu-id="deaef-344">connectors</span></span>

<span data-ttu-id="deaef-345">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="deaef-345">**Optional**</span></span>

<span data-ttu-id="deaef-346">Блок `connectors` определяет соединители Office 365 для приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="deaef-347">Объект — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="deaef-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="deaef-348">Этот блок необходим только для решений, которые предоставляют соединители.</span><span class="sxs-lookup"><span data-stu-id="deaef-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="deaef-349">Имя</span><span class="sxs-lookup"><span data-stu-id="deaef-349">Name</span></span>| <span data-ttu-id="deaef-350">Тип</span><span class="sxs-lookup"><span data-stu-id="deaef-350">Type</span></span>| <span data-ttu-id="deaef-351">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-351">Maximum size</span></span> | <span data-ttu-id="deaef-352">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-352">Required</span></span> | <span data-ttu-id="deaef-353">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="deaef-354">String</span><span class="sxs-lookup"><span data-stu-id="deaef-354">String</span></span>|<span data-ttu-id="deaef-355">2048 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-355">2048 characters</span></span>|<span data-ttu-id="deaef-356">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-356">✔</span></span>|<span data-ttu-id="deaef-357">URL https://, который необходимо использовать при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="deaef-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="deaef-358">String</span><span class="sxs-lookup"><span data-stu-id="deaef-358">String</span></span>|<span data-ttu-id="deaef-359">64 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-359">64 characters</span></span>|<span data-ttu-id="deaef-360">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-360">✔</span></span>|<span data-ttu-id="deaef-361">Уникальный идентификатор соединитетеля, который соответствует его идентификатору в панели мониторинга разработчиков [соединителок.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="deaef-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="deaef-362">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="deaef-362">Array of enum</span></span>|<span data-ttu-id="deaef-363">1</span><span class="sxs-lookup"><span data-stu-id="deaef-363">1</span></span>|<span data-ttu-id="deaef-364">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-364">✔</span></span>|<span data-ttu-id="deaef-365">Указывает, предоставляет ли соединители опыт в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="deaef-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="deaef-366">В настоящее время `team` поддерживается только область.</span><span class="sxs-lookup"><span data-stu-id="deaef-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="deaef-367">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="deaef-367">composeExtensions</span></span>

<span data-ttu-id="deaef-368">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="deaef-368">**Optional**</span></span>

<span data-ttu-id="deaef-369">Определяет расширение обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="deaef-370">В ноябре 2017 г. имя функции было изменено с "расширение составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжили функционировать.</span><span class="sxs-lookup"><span data-stu-id="deaef-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="deaef-371">Объект — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="deaef-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="deaef-372">Этот блок необходим только для решений, которые предоставляют расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="deaef-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="deaef-373">Имя</span><span class="sxs-lookup"><span data-stu-id="deaef-373">Name</span></span>| <span data-ttu-id="deaef-374">Тип</span><span class="sxs-lookup"><span data-stu-id="deaef-374">Type</span></span> | <span data-ttu-id="deaef-375">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-375">Maximum Size</span></span> | <span data-ttu-id="deaef-376">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-376">Required</span></span> | <span data-ttu-id="deaef-377">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="deaef-378">String</span><span class="sxs-lookup"><span data-stu-id="deaef-378">String</span></span>|<span data-ttu-id="deaef-379">64</span><span class="sxs-lookup"><span data-stu-id="deaef-379">64</span></span>|<span data-ttu-id="deaef-380">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-380">✔</span></span>|<span data-ttu-id="deaef-381">Уникальный ID приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрирован в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="deaef-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="deaef-382">Это вполне может быть таким же, как общий [ID приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="deaef-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="deaef-383">Логический</span><span class="sxs-lookup"><span data-stu-id="deaef-383">Boolean</span></span>|||<span data-ttu-id="deaef-384">Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="deaef-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="deaef-385">Значение по умолчанию: `false`.</span><span class="sxs-lookup"><span data-stu-id="deaef-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="deaef-386">Массив объекта</span><span class="sxs-lookup"><span data-stu-id="deaef-386">Array of object</span></span>|<span data-ttu-id="deaef-387">10 </span><span class="sxs-lookup"><span data-stu-id="deaef-387">10</span></span>|<span data-ttu-id="deaef-388">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-388">✔</span></span>|<span data-ttu-id="deaef-389">Массив команд, поддерживаемых расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="deaef-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="deaef-390">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="deaef-390">composeExtensions.commands</span></span>

<span data-ttu-id="deaef-391">Расширение обмена сообщениями должно объявлять одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="deaef-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="deaef-392">Каждая команда отображается в Microsoft Teams в качестве потенциального взаимодействия с точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="deaef-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="deaef-393">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="deaef-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="deaef-394">Каждый элемент команды — это объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="deaef-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="deaef-395">Имя</span><span class="sxs-lookup"><span data-stu-id="deaef-395">Name</span></span>| <span data-ttu-id="deaef-396">Тип</span><span class="sxs-lookup"><span data-stu-id="deaef-396">Type</span></span>| <span data-ttu-id="deaef-397">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-397">Maximum size</span></span> | <span data-ttu-id="deaef-398">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-398">Required</span></span> | <span data-ttu-id="deaef-399">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="deaef-400">String</span><span class="sxs-lookup"><span data-stu-id="deaef-400">String</span></span>|<span data-ttu-id="deaef-401">64 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-401">64 characters</span></span>|<span data-ttu-id="deaef-402">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-402">✔</span></span>|<span data-ttu-id="deaef-403">ID для команды</span><span class="sxs-lookup"><span data-stu-id="deaef-403">The ID for the command</span></span>|
|`type`|<span data-ttu-id="deaef-404">String</span><span class="sxs-lookup"><span data-stu-id="deaef-404">String</span></span>|<span data-ttu-id="deaef-405">64 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-405">64 characters</span></span>||<span data-ttu-id="deaef-406">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="deaef-406">Type of the command.</span></span> <span data-ttu-id="deaef-407">Один `query` из или `action` .</span><span class="sxs-lookup"><span data-stu-id="deaef-407">One of `query` or `action`.</span></span> <span data-ttu-id="deaef-408">По умолчанию: `query`</span><span class="sxs-lookup"><span data-stu-id="deaef-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="deaef-409">String</span><span class="sxs-lookup"><span data-stu-id="deaef-409">String</span></span>|<span data-ttu-id="deaef-410">32 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-410">32 characters</span></span>|<span data-ttu-id="deaef-411">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-411">✔</span></span>|<span data-ttu-id="deaef-412">Удобное имя команды</span><span class="sxs-lookup"><span data-stu-id="deaef-412">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="deaef-413">String</span><span class="sxs-lookup"><span data-stu-id="deaef-413">String</span></span>|<span data-ttu-id="deaef-414">128 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-414">128 characters</span></span>||<span data-ttu-id="deaef-415">Описание, которое отображается пользователям, чтобы указать цель этой команды</span><span class="sxs-lookup"><span data-stu-id="deaef-415">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="deaef-416">Логический</span><span class="sxs-lookup"><span data-stu-id="deaef-416">Boolean</span></span>|||<span data-ttu-id="deaef-417">Значение Boolean, которое указывает, следует ли запускать команду изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="deaef-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="deaef-418">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="deaef-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="deaef-419">Массив строк</span><span class="sxs-lookup"><span data-stu-id="deaef-419">Array of Strings</span></span>|<span data-ttu-id="deaef-420">3</span><span class="sxs-lookup"><span data-stu-id="deaef-420">3</span></span>||<span data-ttu-id="deaef-421">Определяет, из чего можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="deaef-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="deaef-422">Любое сочетание `compose` `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="deaef-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="deaef-423">Значение по умолчанию: `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="deaef-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="deaef-424">Логический</span><span class="sxs-lookup"><span data-stu-id="deaef-424">Boolean</span></span>|||<span data-ttu-id="deaef-425">Значение boolean, которое указывает, следует ли динамически получать модуль задач</span><span class="sxs-lookup"><span data-stu-id="deaef-425">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="deaef-426">Объект</span><span class="sxs-lookup"><span data-stu-id="deaef-426">Object</span></span>|||<span data-ttu-id="deaef-427">Укажите модуль задач для предварительной загрузки при использовании команды расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="deaef-427">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="deaef-428">String</span><span class="sxs-lookup"><span data-stu-id="deaef-428">String</span></span>|<span data-ttu-id="deaef-429">64</span><span class="sxs-lookup"><span data-stu-id="deaef-429">64</span></span>||<span data-ttu-id="deaef-430">Начальное название диалогов</span><span class="sxs-lookup"><span data-stu-id="deaef-430">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="deaef-431">String</span><span class="sxs-lookup"><span data-stu-id="deaef-431">String</span></span>|||<span data-ttu-id="deaef-432">Ширина диалогов — число пикселей или макет по умолчанию, такие как "большой", "средний" или "маленький"</span><span class="sxs-lookup"><span data-stu-id="deaef-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="deaef-433">String</span><span class="sxs-lookup"><span data-stu-id="deaef-433">String</span></span>|||<span data-ttu-id="deaef-434">Высота диалогов — число в пикселях или макет по умолчанию, такие как "большой", "средний" или "маленький"</span><span class="sxs-lookup"><span data-stu-id="deaef-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="deaef-435">String</span><span class="sxs-lookup"><span data-stu-id="deaef-435">String</span></span>|||<span data-ttu-id="deaef-436">Начальный URL-адрес веб-просмотров</span><span class="sxs-lookup"><span data-stu-id="deaef-436">Initial webview URL</span></span>|
|`messageHandlers`|<span data-ttu-id="deaef-437">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="deaef-437">Array of Objects</span></span>|<span data-ttu-id="deaef-438">5 </span><span class="sxs-lookup"><span data-stu-id="deaef-438">5</span></span>||<span data-ttu-id="deaef-439">Список обработчиков, которые позволяют вызывать приложения при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="deaef-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="deaef-440">Домены также должны быть указаны в `validDomains`</span><span class="sxs-lookup"><span data-stu-id="deaef-440">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="deaef-441">String</span><span class="sxs-lookup"><span data-stu-id="deaef-441">String</span></span>|||<span data-ttu-id="deaef-442">Тип обработка сообщений.</span><span class="sxs-lookup"><span data-stu-id="deaef-442">The type of message handler.</span></span> <span data-ttu-id="deaef-443">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="deaef-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="deaef-444">Массив строк</span><span class="sxs-lookup"><span data-stu-id="deaef-444">Array of Strings</span></span>|||<span data-ttu-id="deaef-445">Массив доменов, для которые обработник сообщений ссылок может зарегистрироваться.</span><span class="sxs-lookup"><span data-stu-id="deaef-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="deaef-446">Массив объекта</span><span class="sxs-lookup"><span data-stu-id="deaef-446">Array of object</span></span>|<span data-ttu-id="deaef-447">5 </span><span class="sxs-lookup"><span data-stu-id="deaef-447">5</span></span>|<span data-ttu-id="deaef-448">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-448">✔</span></span>|<span data-ttu-id="deaef-449">Список параметров, которые принимает команда.</span><span class="sxs-lookup"><span data-stu-id="deaef-449">The list of parameters the command takes.</span></span> <span data-ttu-id="deaef-450">Минимум: 1; максимум: 5</span><span class="sxs-lookup"><span data-stu-id="deaef-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="deaef-451">String</span><span class="sxs-lookup"><span data-stu-id="deaef-451">String</span></span>|<span data-ttu-id="deaef-452">64 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-452">64 characters</span></span>|<span data-ttu-id="deaef-453">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-453">✔</span></span>|<span data-ttu-id="deaef-454">Имя параметра, как оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="deaef-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="deaef-455">Это включено в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="deaef-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="deaef-456">String</span><span class="sxs-lookup"><span data-stu-id="deaef-456">String</span></span>|<span data-ttu-id="deaef-457">32 символа</span><span class="sxs-lookup"><span data-stu-id="deaef-457">32 characters</span></span>|<span data-ttu-id="deaef-458">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-458">✔</span></span>|<span data-ttu-id="deaef-459">Удобное название для параметра.</span><span class="sxs-lookup"><span data-stu-id="deaef-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="deaef-460">String</span><span class="sxs-lookup"><span data-stu-id="deaef-460">String</span></span>|<span data-ttu-id="deaef-461">128 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-461">128 characters</span></span>||<span data-ttu-id="deaef-462">Удобное для пользователя строка, описываемая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="deaef-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="deaef-463">String</span><span class="sxs-lookup"><span data-stu-id="deaef-463">String</span></span>|<span data-ttu-id="deaef-464">128 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-464">128 characters</span></span>||<span data-ttu-id="deaef-465">Определяет тип управления, отображаемого в модуле задач `fetchTask: true` для .</span><span class="sxs-lookup"><span data-stu-id="deaef-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="deaef-466">Один `text` из `textarea` , , , `number` , `date` `time` `toggle` , `choiceset`</span><span class="sxs-lookup"><span data-stu-id="deaef-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="deaef-467">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="deaef-467">Array of Objects</span></span>|<span data-ttu-id="deaef-468">10 </span><span class="sxs-lookup"><span data-stu-id="deaef-468">10</span></span>||<span data-ttu-id="deaef-469">Параметры выбора `choiceset` для .</span><span class="sxs-lookup"><span data-stu-id="deaef-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="deaef-470">Использование только в том `parameter.inputType` случае, если `choiceset`</span><span class="sxs-lookup"><span data-stu-id="deaef-470">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="deaef-471">String</span><span class="sxs-lookup"><span data-stu-id="deaef-471">String</span></span>|<span data-ttu-id="deaef-472">128</span><span class="sxs-lookup"><span data-stu-id="deaef-472">128</span></span>||<span data-ttu-id="deaef-473">Название выбора</span><span class="sxs-lookup"><span data-stu-id="deaef-473">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="deaef-474">String</span><span class="sxs-lookup"><span data-stu-id="deaef-474">String</span></span>|<span data-ttu-id="deaef-475">512</span><span class="sxs-lookup"><span data-stu-id="deaef-475">512</span></span>||<span data-ttu-id="deaef-476">Значение выбора</span><span class="sxs-lookup"><span data-stu-id="deaef-476">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="deaef-477">permissions</span><span class="sxs-lookup"><span data-stu-id="deaef-477">permissions</span></span>

<span data-ttu-id="deaef-478">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="deaef-478">**Optional**</span></span>

<span data-ttu-id="deaef-479">Массив указывает, какие разрешения запрашивает приложение, что позволяет конечным пользователям узнать, как `string` будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="deaef-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="deaef-480">Следующие параметры не являются эксклюзивными:</span><span class="sxs-lookup"><span data-stu-id="deaef-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="deaef-481">`identity`&emsp;Требует сведений о удостоверениях пользователей</span><span class="sxs-lookup"><span data-stu-id="deaef-481">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="deaef-482">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам группы</span><span class="sxs-lookup"><span data-stu-id="deaef-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="deaef-483">Изменение этих разрешений при обновлении приложения приведет к тому, что пользователи повторят процесс согласия при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="deaef-484">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="deaef-484">devicePermissions</span></span>

<span data-ttu-id="deaef-485">**Необязательный** Массив строк</span><span class="sxs-lookup"><span data-stu-id="deaef-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="deaef-486">Указывает родных функций на устройстве пользователя, к которое ваше приложение может запрашивать доступ.</span><span class="sxs-lookup"><span data-stu-id="deaef-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="deaef-487">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="deaef-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="deaef-488">validDomains</span><span class="sxs-lookup"><span data-stu-id="deaef-488">validDomains</span></span>

<span data-ttu-id="deaef-489">**Необязательный,** за **исключением обязательного,** где отмечено</span><span class="sxs-lookup"><span data-stu-id="deaef-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="deaef-490">Список допустимого домена, из которого приложение ожидает загрузки любого контента.</span><span class="sxs-lookup"><span data-stu-id="deaef-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="deaef-491">Списки домена могут включать, например, поддиайки. `*.example.com`</span><span class="sxs-lookup"><span data-stu-id="deaef-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="deaef-492">Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="deaef-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="deaef-493">Если конфигурации вкладок или пользовательскому интерфейсу контента необходимо перейти к любому другому домену, кроме одного использования для конфигурации вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="deaef-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="deaef-494">Однако не **обязательно** включать в приложение домены поставщиков удостоверений, которые вы хотите поддерживать.</span><span class="sxs-lookup"><span data-stu-id="deaef-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="deaef-495">Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить на accounts.google.com, но не следует включать accounts.google.com `validDomains[]` в .</span><span class="sxs-lookup"><span data-stu-id="deaef-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="deaef-496">Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью подкрентов.</span><span class="sxs-lookup"><span data-stu-id="deaef-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="deaef-497">Например, `yourapp.onmicrosoft.com` допустимо, `*.onmicrosoft.com` но не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="deaef-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="deaef-498">Объект — массив со всеми элементами `string` типа.</span><span class="sxs-lookup"><span data-stu-id="deaef-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="deaef-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="deaef-499">webApplicationInfo</span></span>

<span data-ttu-id="deaef-500">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="deaef-500">**Optional**</span></span>

<span data-ttu-id="deaef-501">Укажите свой AAD App ID и Graph, чтобы помочь пользователям беспрепятственно войти в ваше приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="deaef-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="deaef-502">Имя</span><span class="sxs-lookup"><span data-stu-id="deaef-502">Name</span></span>| <span data-ttu-id="deaef-503">Тип</span><span class="sxs-lookup"><span data-stu-id="deaef-503">Type</span></span>| <span data-ttu-id="deaef-504">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-504">Maximum size</span></span> | <span data-ttu-id="deaef-505">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-505">Required</span></span> | <span data-ttu-id="deaef-506">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="deaef-507">String</span><span class="sxs-lookup"><span data-stu-id="deaef-507">String</span></span>|<span data-ttu-id="deaef-508">36 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-508">36 characters</span></span>|<span data-ttu-id="deaef-509">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-509">✔</span></span>|<span data-ttu-id="deaef-510">AAD-id приложения приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-510">AAD application id of the app.</span></span> <span data-ttu-id="deaef-511">Этот id должен быть GUID.</span><span class="sxs-lookup"><span data-stu-id="deaef-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="deaef-512">String</span><span class="sxs-lookup"><span data-stu-id="deaef-512">String</span></span>|<span data-ttu-id="deaef-513">2048 символов</span><span class="sxs-lookup"><span data-stu-id="deaef-513">2048 characters</span></span>|<span data-ttu-id="deaef-514">✔</span><span class="sxs-lookup"><span data-stu-id="deaef-514">✔</span></span>|<span data-ttu-id="deaef-515">URL-адрес ресурса приложения для приобретения маркера auth для SSO.</span><span class="sxs-lookup"><span data-stu-id="deaef-515">Resource url of app for acquiring auth token for SSO.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="deaef-516">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="deaef-516">configurableProperties</span></span>

<span data-ttu-id="deaef-517">**Необязательный** - массив</span><span class="sxs-lookup"><span data-stu-id="deaef-517">**Optional** - array</span></span>

<span data-ttu-id="deaef-518">Блок `configurableProperties` определяет свойства приложений, которые администратор Teams может настроить.</span><span class="sxs-lookup"><span data-stu-id="deaef-518">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="deaef-519">Дополнительные сведения см. [в дополнительных сведениях о настройке приложений в Microsoft Teams.](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="deaef-519">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="deaef-520">Необходимо определить как минимум одно свойство.</span><span class="sxs-lookup"><span data-stu-id="deaef-520">A minimum of one property must be defined.</span></span> <span data-ttu-id="deaef-521">В этом блоке можно определить максимум девять свойств.</span><span class="sxs-lookup"><span data-stu-id="deaef-521">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="deaef-522">В качестве наилучшей практики необходимо предоставить рекомендации по настройке для пользователей и клиентов приложений, которые следует соблюдать при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-522">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> 

<span data-ttu-id="deaef-523">Можно определить любое из следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="deaef-523">You can define any of the following properties:</span></span>
* <span data-ttu-id="deaef-524">`name`: Позволяет администратору изменять имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-524">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="deaef-525">`shortDescription`: Позволяет администратору изменить краткое описание приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-525">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="deaef-526">`longDescription`: Позволяет администратору изменять подробное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="deaef-526">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="deaef-527">`smallImageUrl`. Это `outline` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="deaef-527">`smallImageUrl`: It is `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="deaef-528">`largeImageUrl`. Это `color` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="deaef-528">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="deaef-529">`accentColor`. Это цвет, который можно использовать в сочетании с и в качестве фона для значков плана.</span><span class="sxs-lookup"><span data-stu-id="deaef-529">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="deaef-530">`developerUrl`. Это https:// URL-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="deaef-530">`developerUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="deaef-531">`privacyUrl`. Это https:// url-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="deaef-531">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="deaef-532">`termsOfUseUrl`. Это https:// URL-адрес для условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="deaef-532">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="deaef-533">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="deaef-533">defaultInstallScope</span></span>

<span data-ttu-id="deaef-534">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="deaef-534">**Optional** - string</span></span>

<span data-ttu-id="deaef-535">Указывает область установки, определяемую для этого приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="deaef-535">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="deaef-536">Определенным областью будет параметр, отображаемый на кнопке при добавлении приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="deaef-536">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="deaef-537">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="deaef-537">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="deaef-538">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="deaef-538">defaultGroupCapability</span></span>

<span data-ttu-id="deaef-539">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="deaef-539">**Optional** - object</span></span>

<span data-ttu-id="deaef-540">Когда будет выбрана область установки группы, она определит возможности по умолчанию при установке приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="deaef-540">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="deaef-541">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="deaef-541">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="deaef-542">Имя</span><span class="sxs-lookup"><span data-stu-id="deaef-542">Name</span></span>| <span data-ttu-id="deaef-543">Тип</span><span class="sxs-lookup"><span data-stu-id="deaef-543">Type</span></span>| <span data-ttu-id="deaef-544">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="deaef-544">Maximum size</span></span> | <span data-ttu-id="deaef-545">Обязательный</span><span class="sxs-lookup"><span data-stu-id="deaef-545">Required</span></span> | <span data-ttu-id="deaef-546">Описание</span><span class="sxs-lookup"><span data-stu-id="deaef-546">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="deaef-547">string</span><span class="sxs-lookup"><span data-stu-id="deaef-547">string</span></span>|||<span data-ttu-id="deaef-548">Если выбрана область установки, это поле указывает доступные возможности `team` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="deaef-548">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="deaef-549">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="deaef-549">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="deaef-550">String</span><span class="sxs-lookup"><span data-stu-id="deaef-550">string</span></span>|||<span data-ttu-id="deaef-551">Если выбрана область установки, это поле указывает доступные возможности `groupchat` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="deaef-551">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="deaef-552">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="deaef-552">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="deaef-553">String</span><span class="sxs-lookup"><span data-stu-id="deaef-553">string</span></span>|||<span data-ttu-id="deaef-554">Если выбрана область установки, это поле указывает доступные возможности `meetings` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="deaef-554">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="deaef-555">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="deaef-555">Options: `tab`, `bot`, or `connector`.</span></span>|

