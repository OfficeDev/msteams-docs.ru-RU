---
title: Developer Preview схемы манифеста
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams
ms.topic: reference
keywords: команды проявляют схему Developer Preview
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: a5c75046b950484a897fa2720444899c4817989c
ms.sourcegitcommit: 25c02757fe207cdff916ba63aa215f88e24e1d6f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/26/2021
ms.locfileid: "52667421"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="c0b3f-104">Схема манифеста предварительного просмотра разработчика для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c0b3f-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="c0b3f-105">Дополнительные сведения о программе и о том, как можно присоединиться, см. в [Developer Preview.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c0b3f-105">For more information on the program and how you can join,see [Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
> <span data-ttu-id="c0b3f-106">Если вы не используете предварительный просмотр разработчика, не следует использовать эту версию манифеста.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="c0b3f-107">См. [справку.](~/resources/schema/manifest-schema.md) Схема манифеста Microsoft Teams для публичной версии манифеста.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="c0b3f-108">Манифест Microsoft Teams описывает интеграцию приложения в продукт Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="c0b3f-109">Манифест должен соответствовать схеме, которая была на [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) уровне .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="c0b3f-110">Дополнительные сведения о доступных функциях см. в фото: [Features in the Public Developer Preview for Microsoft Teams.](~/resources/dev-preview/developer-preview-features.md)</span><span class="sxs-lookup"><span data-stu-id="c0b3f-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="c0b3f-111">Образец полного манифеста</span><span class="sxs-lookup"><span data-stu-id="c0b3f-111">Sample full manifest</span></span>

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

<span data-ttu-id="c0b3f-112">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="c0b3f-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="c0b3f-113">$schema</span><span class="sxs-lookup"><span data-stu-id="c0b3f-113">$schema</span></span>

<span data-ttu-id="c0b3f-114">*Необязательный, но рекомендуемый* &ndash; String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="c0b3f-115">URL https:// ссылки на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="c0b3f-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="c0b3f-116">manifestVersion</span></span>

<span data-ttu-id="c0b3f-117">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-117">**Required** &ndash; String</span></span>

<span data-ttu-id="c0b3f-118">Версия схемы манифеста, используемая этим манифестом.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="c0b3f-119">Это должно быть "devPreview".</span><span class="sxs-lookup"><span data-stu-id="c0b3f-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="c0b3f-120">version</span><span class="sxs-lookup"><span data-stu-id="c0b3f-120">version</span></span>

<span data-ttu-id="c0b3f-121">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-121">**Required** &ndash; String</span></span>

<span data-ttu-id="c0b3f-122">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-122">The version of the specific app.</span></span> <span data-ttu-id="c0b3f-123">Если вы что-то обновляете в манифесте, необходимо также приумножная версия.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="c0b3f-124">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="c0b3f-125">Если это приложение было отправлено в магазин, новый манифест должен быть повторно отправлен и повторно проверен.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="c0b3f-126">Затем пользователи этого приложения получат новый обновленный манифест автоматически через несколько часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="c0b3f-127">Если приложение запрашивает разрешения изменить, пользователям будет предложено обновить и повторно согласиться на приложение.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="c0b3f-128">Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="c0b3f-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="c0b3f-129">id</span><span class="sxs-lookup"><span data-stu-id="c0b3f-129">id</span></span>

<span data-ttu-id="c0b3f-130">**Обязательно** &ndash; ID приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="c0b3f-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="c0b3f-131">Уникальный идентификатор, созданный Корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="c0b3f-132">Если вы зарегистрировали бота через Microsoft Bot Framework или веб-приложение вашей вкладки уже входит в Microsoft, вы уже должны иметь ID и ввести его здесь.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="c0b3f-133">В противном случае необходимо создать новый ID на портале регистрации приложений Microsoft[(Мои](https://apps.dev.microsoft.com)приложения), введите его здесь, а затем повторно использовать при добавлении [бота.](~/bots/how-to/create-a-bot-for-teams.md)</span><span class="sxs-lookup"><span data-stu-id="c0b3f-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="c0b3f-134">packageName</span><span class="sxs-lookup"><span data-stu-id="c0b3f-134">packageName</span></span>

<span data-ttu-id="c0b3f-135">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-135">**Required** &ndash; String</span></span>

<span data-ttu-id="c0b3f-136">Уникальный идентификатор для этого приложения в обратной нотации домена; например, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="c0b3f-137">developer</span><span class="sxs-lookup"><span data-stu-id="c0b3f-137">developer</span></span>

<span data-ttu-id="c0b3f-138">**Required**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-138">**Required**</span></span>

<span data-ttu-id="c0b3f-139">Указывает сведения о вашей компании.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-139">Specifies information about your company.</span></span> <span data-ttu-id="c0b3f-140">Для приложений, представленных в AppSource (ранее Office Store), эти значения должны соответствовать сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="c0b3f-141">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-141">Name</span></span>| <span data-ttu-id="c0b3f-142">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-142">Maximum size</span></span> | <span data-ttu-id="c0b3f-143">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-143">Required</span></span> | <span data-ttu-id="c0b3f-144">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="c0b3f-145">32 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-145">32 characters</span></span>|<span data-ttu-id="c0b3f-146">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-146">✔</span></span>|<span data-ttu-id="c0b3f-147">Имя отображения для разработчика.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="c0b3f-148">2048 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-148">2048 characters</span></span>|<span data-ttu-id="c0b3f-149">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-149">✔</span></span>|<span data-ttu-id="c0b3f-150">Url https:// url-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="c0b3f-151">Эта ссылка должна принимать пользователей на страницу вашей компании или конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="c0b3f-152">2048 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-152">2048 characters</span></span>|<span data-ttu-id="c0b3f-153">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-153">✔</span></span>|<span data-ttu-id="c0b3f-154">Url https:// url-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="c0b3f-155">2048 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-155">2048 characters</span></span>|<span data-ttu-id="c0b3f-156">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-156">✔</span></span>|<span data-ttu-id="c0b3f-157">Url https:// url-адрес для условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="c0b3f-158">10 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-158">10 characters</span></span>|<span data-ttu-id="c0b3f-159">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-159">✔</span></span>|<span data-ttu-id="c0b3f-160">**Необязательный** Идентификатор Сети партнеров Майкрософт, который определяет организацию-партнер, которая строит приложение.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="c0b3f-161">локализацияInfo</span><span class="sxs-lookup"><span data-stu-id="c0b3f-161">localizationInfo</span></span>

<span data-ttu-id="c0b3f-162">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-162">**Optional**</span></span>

<span data-ttu-id="c0b3f-163">Позволяет спецификацию языка по умолчанию, а также указатели для дополнительных языковых файлов.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="c0b3f-164">См. [локализацию.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="c0b3f-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="c0b3f-165">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-165">Name</span></span>| <span data-ttu-id="c0b3f-166">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-166">Maximum size</span></span> | <span data-ttu-id="c0b3f-167">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-167">Required</span></span> | <span data-ttu-id="c0b3f-168">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="c0b3f-169">4 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-169">4 characters</span></span>|<span data-ttu-id="c0b3f-170">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-170">✔</span></span>|<span data-ttu-id="c0b3f-171">Языковой тег строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="c0b3f-172">локализацияInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="c0b3f-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="c0b3f-173">Массив объектов, указывающих дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="c0b3f-174">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-174">Name</span></span>| <span data-ttu-id="c0b3f-175">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-175">Maximum size</span></span> | <span data-ttu-id="c0b3f-176">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-176">Required</span></span> | <span data-ttu-id="c0b3f-177">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="c0b3f-178">4 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-178">4 characters</span></span>|<span data-ttu-id="c0b3f-179">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-179">✔</span></span>|<span data-ttu-id="c0b3f-180">Языковой тег строки в предоставленного файла.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="c0b3f-181">4 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-181">4 characters</span></span>|<span data-ttu-id="c0b3f-182">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-182">✔</span></span>|<span data-ttu-id="c0b3f-183">Относительный путь к файлу .json, содержащим переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="c0b3f-184">name</span><span class="sxs-lookup"><span data-stu-id="c0b3f-184">name</span></span>

<span data-ttu-id="c0b3f-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-185">**Required**</span></span>

<span data-ttu-id="c0b3f-186">Имя приложения, отображаемого пользователям в Teams.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="c0b3f-187">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="c0b3f-188">Значения и `short` не `full` должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="c0b3f-189">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-189">Name</span></span>| <span data-ttu-id="c0b3f-190">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-190">Maximum size</span></span> | <span data-ttu-id="c0b3f-191">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-191">Required</span></span> | <span data-ttu-id="c0b3f-192">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="c0b3f-193">30 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-193">30 characters</span></span>|<span data-ttu-id="c0b3f-194">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-194">✔</span></span>|<span data-ttu-id="c0b3f-195">Короткое имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="c0b3f-196">100 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-196">100 characters</span></span>||<span data-ttu-id="c0b3f-197">Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="c0b3f-198">(описание)</span><span class="sxs-lookup"><span data-stu-id="c0b3f-198">description</span></span>

<span data-ttu-id="c0b3f-199">**Required**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-199">**Required**</span></span>

<span data-ttu-id="c0b3f-200">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-200">Describes your app to users.</span></span> <span data-ttu-id="c0b3f-201">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="c0b3f-202">Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, чтобы помочь потенциальным клиентам понять, что делает ваш опыт.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="c0b3f-203">В полном описании также следует отметить, если для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="c0b3f-204">Значения и `short` не `full` должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="c0b3f-205">Короткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="c0b3f-206">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-206">Name</span></span>| <span data-ttu-id="c0b3f-207">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-207">Maximum size</span></span> | <span data-ttu-id="c0b3f-208">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-208">Required</span></span> | <span data-ttu-id="c0b3f-209">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="c0b3f-210">80 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-210">80 characters</span></span>|<span data-ttu-id="c0b3f-211">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-211">✔</span></span>|<span data-ttu-id="c0b3f-212">Краткое описание работы приложения, используемого при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="c0b3f-213">4000 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-213">4000 characters</span></span>|<span data-ttu-id="c0b3f-214">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-214">✔</span></span>|<span data-ttu-id="c0b3f-215">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="c0b3f-216">icons</span><span class="sxs-lookup"><span data-stu-id="c0b3f-216">icons</span></span>

<span data-ttu-id="c0b3f-217">**Required**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-217">**Required**</span></span>

<span data-ttu-id="c0b3f-218">Значки, используемые в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-218">Icons used within the Teams app.</span></span> <span data-ttu-id="c0b3f-219">Файлы значков должны быть включены в пакет отправки.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="c0b3f-220">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-220">Name</span></span>| <span data-ttu-id="c0b3f-221">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-221">Maximum size</span></span> | <span data-ttu-id="c0b3f-222">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-222">Required</span></span> | <span data-ttu-id="c0b3f-223">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="c0b3f-224">2048 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-224">2048 characters</span></span>|<span data-ttu-id="c0b3f-225">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-225">✔</span></span>|<span data-ttu-id="c0b3f-226">Относительный путь к прозрачному значку контура PNG 32x32.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="c0b3f-227">2048 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-227">2048 characters</span></span>|<span data-ttu-id="c0b3f-228">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-228">✔</span></span>|<span data-ttu-id="c0b3f-229">Относительный путь к значку PNG полного цвета 192x192.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="c0b3f-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="c0b3f-230">accentColor</span></span>

<span data-ttu-id="c0b3f-231">**Обязательно** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-231">**Required** &ndash; String</span></span>

<span data-ttu-id="c0b3f-232">Цвет, который можно использовать в сочетании с и в качестве фона для значков контура.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="c0b3f-233">Значение должно быть допустимым цветовым кодом HTML, начиная, например, с `#4464ee` "#".</span><span class="sxs-lookup"><span data-stu-id="c0b3f-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="c0b3f-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="c0b3f-234">configurableTabs</span></span>

<span data-ttu-id="c0b3f-235">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-235">**Optional**</span></span>

<span data-ttu-id="c0b3f-236">Используется, когда в вашем приложении есть опыт работы с вкладками канала команды, которая требует дополнительной конфигурации перед ее добавлением.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="c0b3f-237">Настраиваемые вкладки поддерживаются только в области команд, и в настоящее время поддерживается только одна вкладка для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="c0b3f-238">Объект — массив со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="c0b3f-239">Этот блок требуется только для решений, которые предоставляют настраиваемое решение вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="c0b3f-240">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-240">Name</span></span>| <span data-ttu-id="c0b3f-241">Тип</span><span class="sxs-lookup"><span data-stu-id="c0b3f-241">Type</span></span>| <span data-ttu-id="c0b3f-242">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-242">Maximum size</span></span> | <span data-ttu-id="c0b3f-243">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-243">Required</span></span> | <span data-ttu-id="c0b3f-244">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="c0b3f-245">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-245">String</span></span>|<span data-ttu-id="c0b3f-246">2048 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-246">2048 characters</span></span>|<span data-ttu-id="c0b3f-247">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-247">✔</span></span>|<span data-ttu-id="c0b3f-248">URL-https://, который можно использовать при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="c0b3f-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="c0b3f-249">Boolean</span></span>|||<span data-ttu-id="c0b3f-250">Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="c0b3f-251">По умолчанию: `true`</span><span class="sxs-lookup"><span data-stu-id="c0b3f-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="c0b3f-252">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="c0b3f-252">Array of enum</span></span>|<span data-ttu-id="c0b3f-253">1</span><span class="sxs-lookup"><span data-stu-id="c0b3f-253">1</span></span>|<span data-ttu-id="c0b3f-254">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-254">✔</span></span>|<span data-ttu-id="c0b3f-255">В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="c0b3f-256">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-256">String</span></span>|<span data-ttu-id="c0b3f-257">2048</span><span class="sxs-lookup"><span data-stu-id="c0b3f-257">2048</span></span>||<span data-ttu-id="c0b3f-258">Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="c0b3f-259">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="c0b3f-260">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="c0b3f-260">Array of enum</span></span>|<span data-ttu-id="c0b3f-261">1</span><span class="sxs-lookup"><span data-stu-id="c0b3f-261">1</span></span>||<span data-ttu-id="c0b3f-262">Определяет, как вкладка будет доступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="c0b3f-263">Параметры `sharePointFullPage` и `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="c0b3f-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="c0b3f-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="c0b3f-264">staticTabs</span></span>

<span data-ttu-id="c0b3f-265">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-265">**Optional**</span></span>

<span data-ttu-id="c0b3f-266">Определяет набор вкладок, которые можно "прикрепить" по умолчанию, не добавляя их вручную.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="c0b3f-267">Статические вкладки, объявленные в области, всегда прикрепяются к личному опыту `personal` приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="c0b3f-268">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="c0b3f-269">Отрисуйка вкладок с адаптивными картами, указав вместо в `contentBotId` `contentUrl` **блоке staticTabs.**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-269">Render tabs with Adaptive Cards by specifying `contentBotId` instead of `contentUrl` in the **staticTabs** block.</span></span>

<span data-ttu-id="c0b3f-270">Объект — массив (не более 16 элементов) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-270">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="c0b3f-271">Этот блок требуется только для решений, которые предоставляют статическое решение вкладки.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-271">This block is required only for solutions that provide a static tab solution.</span></span>


|<span data-ttu-id="c0b3f-272">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-272">Name</span></span>| <span data-ttu-id="c0b3f-273">Тип</span><span class="sxs-lookup"><span data-stu-id="c0b3f-273">Type</span></span>| <span data-ttu-id="c0b3f-274">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-274">Maximum size</span></span> | <span data-ttu-id="c0b3f-275">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-275">Required</span></span> | <span data-ttu-id="c0b3f-276">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-276">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="c0b3f-277">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-277">String</span></span>|<span data-ttu-id="c0b3f-278">64 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-278">64 characters</span></span>|<span data-ttu-id="c0b3f-279">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-279">✔</span></span>|<span data-ttu-id="c0b3f-280">Уникальный идентификатор для объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-280">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="c0b3f-281">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-281">String</span></span>|<span data-ttu-id="c0b3f-282">128 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-282">128 characters</span></span>|<span data-ttu-id="c0b3f-283">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-283">✔</span></span>|<span data-ttu-id="c0b3f-284">Отображение имени вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-284">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="c0b3f-285">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-285">String</span></span>|<span data-ttu-id="c0b3f-286">2048 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-286">2048 characters</span></span>|<span data-ttu-id="c0b3f-287">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-287">✔</span></span>|<span data-ttu-id="c0b3f-288">URL https://, который указывает на пользовательский интерфейс объекта, отображаемого на Teams холсте.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-288">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`contentBotId`|   | | | <span data-ttu-id="c0b3f-289">ID Microsoft Teams, указанный для бота на портале Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-289">The Microsoft Teams app ID specified for the bot in the Bot Framework portal.</span></span> |
|`websiteUrl`|<span data-ttu-id="c0b3f-290">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-290">String</span></span>|<span data-ttu-id="c0b3f-291">2048 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-291">2048 characters</span></span>||<span data-ttu-id="c0b3f-292">В https:// нужно указать URL-адрес, если пользователь выбирает просмотр в браузере.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-292">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="c0b3f-293">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="c0b3f-293">Array of enum</span></span>|<span data-ttu-id="c0b3f-294">1</span><span class="sxs-lookup"><span data-stu-id="c0b3f-294">1</span></span>|<span data-ttu-id="c0b3f-295">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-295">✔</span></span>|<span data-ttu-id="c0b3f-296">В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в `personal` рамках личного опыта.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-296">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="c0b3f-297">боты</span><span class="sxs-lookup"><span data-stu-id="c0b3f-297">bots</span></span>

<span data-ttu-id="c0b3f-298">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-298">**Optional**</span></span>

<span data-ttu-id="c0b3f-299">Определяет решение бота, а также необязательные сведения, такие как свойства команд по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-299">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="c0b3f-300">Объект — массив (максимум 1 элемент в настоящее время разрешен только для одного бота в приложении) со всеми &mdash; элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-300">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="c0b3f-301">Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-301">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="c0b3f-302">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-302">Name</span></span>| <span data-ttu-id="c0b3f-303">Тип</span><span class="sxs-lookup"><span data-stu-id="c0b3f-303">Type</span></span>| <span data-ttu-id="c0b3f-304">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-304">Maximum size</span></span> | <span data-ttu-id="c0b3f-305">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-305">Required</span></span> | <span data-ttu-id="c0b3f-306">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-306">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="c0b3f-307">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-307">String</span></span>|<span data-ttu-id="c0b3f-308">64 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-308">64 characters</span></span>|<span data-ttu-id="c0b3f-309">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-309">✔</span></span>|<span data-ttu-id="c0b3f-310">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-310">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="c0b3f-311">Это вполне может быть таким же, как общий [ID приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="c0b3f-311">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="c0b3f-312">Логический</span><span class="sxs-lookup"><span data-stu-id="c0b3f-312">Boolean</span></span>|||<span data-ttu-id="c0b3f-313">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-313">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="c0b3f-314">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="c0b3f-314">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="c0b3f-315">Логический</span><span class="sxs-lookup"><span data-stu-id="c0b3f-315">Boolean</span></span>|||<span data-ttu-id="c0b3f-316">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-316">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="c0b3f-317">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="c0b3f-317">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="c0b3f-318">Логический</span><span class="sxs-lookup"><span data-stu-id="c0b3f-318">Boolean</span></span>|||<span data-ttu-id="c0b3f-319">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-319">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="c0b3f-320">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="c0b3f-320">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="c0b3f-321">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="c0b3f-321">Array of enum</span></span>|<span data-ttu-id="c0b3f-322">3</span><span class="sxs-lookup"><span data-stu-id="c0b3f-322">3</span></span>|<span data-ttu-id="c0b3f-323">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-323">✔</span></span>|<span data-ttu-id="c0b3f-324">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="c0b3f-324">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="c0b3f-325">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-325">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="c0b3f-326">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="c0b3f-326">bots.commandLists</span></span>

<span data-ttu-id="c0b3f-327">Необязательный список команд, которые бот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-327">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="c0b3f-328">Объект — массив (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-328">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="c0b3f-329">Дополнительные сведения см. в [меню Bot.](~/bots/how-to/create-a-bot-commands-menu.md)</span><span class="sxs-lookup"><span data-stu-id="c0b3f-329">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="c0b3f-330">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-330">Name</span></span>| <span data-ttu-id="c0b3f-331">Тип</span><span class="sxs-lookup"><span data-stu-id="c0b3f-331">Type</span></span>| <span data-ttu-id="c0b3f-332">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-332">Maximum size</span></span> | <span data-ttu-id="c0b3f-333">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-333">Required</span></span> | <span data-ttu-id="c0b3f-334">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-334">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="c0b3f-335">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="c0b3f-335">array of enum</span></span>|<span data-ttu-id="c0b3f-336">3</span><span class="sxs-lookup"><span data-stu-id="c0b3f-336">3</span></span>|<span data-ttu-id="c0b3f-337">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-337">✔</span></span>|<span data-ttu-id="c0b3f-338">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-338">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="c0b3f-339">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-339">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="c0b3f-340">массив объектов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-340">array of objects</span></span>|<span data-ttu-id="c0b3f-341">10 </span><span class="sxs-lookup"><span data-stu-id="c0b3f-341">10</span></span>|<span data-ttu-id="c0b3f-342">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-342">✔</span></span>|<span data-ttu-id="c0b3f-343">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="c0b3f-343">An array of commands the bot supports:</span></span><br><span data-ttu-id="c0b3f-344">`title`: имя команды бота (строка, 32).</span><span class="sxs-lookup"><span data-stu-id="c0b3f-344">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="c0b3f-345">`description`: простое описание или пример синтаксиса команды и его аргумента (строка, 128).</span><span class="sxs-lookup"><span data-stu-id="c0b3f-345">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="c0b3f-346">соединители</span><span class="sxs-lookup"><span data-stu-id="c0b3f-346">connectors</span></span>

<span data-ttu-id="c0b3f-347">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-347">**Optional**</span></span>

<span data-ttu-id="c0b3f-348">Блок `connectors` определяет Office 365 соединители для приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-348">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="c0b3f-349">Объект — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-349">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="c0b3f-350">Этот блок необходим только для решений, которые предоставляют соединители.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-350">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="c0b3f-351">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-351">Name</span></span>| <span data-ttu-id="c0b3f-352">Тип</span><span class="sxs-lookup"><span data-stu-id="c0b3f-352">Type</span></span>| <span data-ttu-id="c0b3f-353">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-353">Maximum size</span></span> | <span data-ttu-id="c0b3f-354">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-354">Required</span></span> | <span data-ttu-id="c0b3f-355">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-355">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="c0b3f-356">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-356">String</span></span>|<span data-ttu-id="c0b3f-357">2048 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-357">2048 characters</span></span>|<span data-ttu-id="c0b3f-358">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-358">✔</span></span>|<span data-ttu-id="c0b3f-359">URL https://, который необходимо использовать при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-359">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="c0b3f-360">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-360">String</span></span>|<span data-ttu-id="c0b3f-361">64 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-361">64 characters</span></span>|<span data-ttu-id="c0b3f-362">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-362">✔</span></span>|<span data-ttu-id="c0b3f-363">Уникальный идентификатор соединитетеля, который соответствует его идентификатору в панели мониторинга разработчиков [соединителок.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="c0b3f-363">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="c0b3f-364">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="c0b3f-364">Array of enum</span></span>|<span data-ttu-id="c0b3f-365">1</span><span class="sxs-lookup"><span data-stu-id="c0b3f-365">1</span></span>|<span data-ttu-id="c0b3f-366">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-366">✔</span></span>|<span data-ttu-id="c0b3f-367">Указывает, предоставляет ли соединители опыт в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="c0b3f-367">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="c0b3f-368">В настоящее время `team` поддерживается только область.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-368">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="c0b3f-369">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="c0b3f-369">composeExtensions</span></span>

<span data-ttu-id="c0b3f-370">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-370">**Optional**</span></span>

<span data-ttu-id="c0b3f-371">Определяет расширение обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-371">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="c0b3f-372">В ноябре 2017 г. имя функции было изменено с "расширение составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжили функционировать.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-372">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="c0b3f-373">Объект — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-373">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="c0b3f-374">Этот блок необходим только для решений, которые предоставляют расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-374">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="c0b3f-375">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-375">Name</span></span>| <span data-ttu-id="c0b3f-376">Тип</span><span class="sxs-lookup"><span data-stu-id="c0b3f-376">Type</span></span> | <span data-ttu-id="c0b3f-377">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-377">Maximum Size</span></span> | <span data-ttu-id="c0b3f-378">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-378">Required</span></span> | <span data-ttu-id="c0b3f-379">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-379">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="c0b3f-380">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-380">String</span></span>|<span data-ttu-id="c0b3f-381">64</span><span class="sxs-lookup"><span data-stu-id="c0b3f-381">64</span></span>|<span data-ttu-id="c0b3f-382">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-382">✔</span></span>|<span data-ttu-id="c0b3f-383">Уникальный ID приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрирован в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-383">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="c0b3f-384">Это вполне может быть таким же, как общий [ID приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="c0b3f-384">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="c0b3f-385">Boolean</span><span class="sxs-lookup"><span data-stu-id="c0b3f-385">Boolean</span></span>|||<span data-ttu-id="c0b3f-386">Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-386">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="c0b3f-387">Значение по умолчанию: `false`.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-387">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="c0b3f-388">Массив объекта</span><span class="sxs-lookup"><span data-stu-id="c0b3f-388">Array of object</span></span>|<span data-ttu-id="c0b3f-389">10 </span><span class="sxs-lookup"><span data-stu-id="c0b3f-389">10</span></span>|<span data-ttu-id="c0b3f-390">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-390">✔</span></span>|<span data-ttu-id="c0b3f-391">Массив команд, поддерживаемых расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c0b3f-391">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="c0b3f-392">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="c0b3f-392">composeExtensions.commands</span></span>

<span data-ttu-id="c0b3f-393">Расширение обмена сообщениями должно объявлять одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-393">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="c0b3f-394">Каждая команда отображается Microsoft Teams как потенциальное взаимодействие с точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-394">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="c0b3f-395">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-395">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="c0b3f-396">Каждый элемент команды — это объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="c0b3f-396">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="c0b3f-397">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-397">Name</span></span>| <span data-ttu-id="c0b3f-398">Тип</span><span class="sxs-lookup"><span data-stu-id="c0b3f-398">Type</span></span>| <span data-ttu-id="c0b3f-399">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-399">Maximum size</span></span> | <span data-ttu-id="c0b3f-400">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-400">Required</span></span> | <span data-ttu-id="c0b3f-401">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-401">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="c0b3f-402">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-402">String</span></span>|<span data-ttu-id="c0b3f-403">64 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-403">64 characters</span></span>|<span data-ttu-id="c0b3f-404">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-404">✔</span></span>|<span data-ttu-id="c0b3f-405">ID для команды.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-405">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="c0b3f-406">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-406">String</span></span>|<span data-ttu-id="c0b3f-407">64 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-407">64 characters</span></span>||<span data-ttu-id="c0b3f-408">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-408">Type of the command.</span></span> <span data-ttu-id="c0b3f-409">Один `query` из или `action` .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-409">One of `query` or `action`.</span></span> <span data-ttu-id="c0b3f-410">По умолчанию: `query`</span><span class="sxs-lookup"><span data-stu-id="c0b3f-410">Default: `query`</span></span>|
|`title`|<span data-ttu-id="c0b3f-411">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-411">String</span></span>|<span data-ttu-id="c0b3f-412">32 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-412">32 characters</span></span>|<span data-ttu-id="c0b3f-413">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-413">✔</span></span>|<span data-ttu-id="c0b3f-414">Удобное имя команды.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-414">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="c0b3f-415">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-415">String</span></span>|<span data-ttu-id="c0b3f-416">128 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-416">128 characters</span></span>||<span data-ttu-id="c0b3f-417">В описании, которое отображается пользователями, указывается назначение этой команды.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-417">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="c0b3f-418">Boolean</span><span class="sxs-lookup"><span data-stu-id="c0b3f-418">Boolean</span></span>|||<span data-ttu-id="c0b3f-419">Значение Boolean, которое указывает, следует ли запускать команду изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-419">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="c0b3f-420">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="c0b3f-420">Default: `false`</span></span>|
|`context`|<span data-ttu-id="c0b3f-421">Массив строк</span><span class="sxs-lookup"><span data-stu-id="c0b3f-421">Array of Strings</span></span>|<span data-ttu-id="c0b3f-422">3</span><span class="sxs-lookup"><span data-stu-id="c0b3f-422">3</span></span>||<span data-ttu-id="c0b3f-423">Определяет, из чего можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-423">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="c0b3f-424">Любое сочетание `compose` `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-424">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="c0b3f-425">Значение по умолчанию: `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="c0b3f-425">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="c0b3f-426">Boolean</span><span class="sxs-lookup"><span data-stu-id="c0b3f-426">Boolean</span></span>|||<span data-ttu-id="c0b3f-427">Значение boolean, которое указывает, следует ли динамически получать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-427">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="c0b3f-428">Объект</span><span class="sxs-lookup"><span data-stu-id="c0b3f-428">Object</span></span>|||<span data-ttu-id="c0b3f-429">Укажите модуль задач для предварительной загрузки при использовании команды расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-429">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="c0b3f-430">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-430">String</span></span>|<span data-ttu-id="c0b3f-431">64</span><span class="sxs-lookup"><span data-stu-id="c0b3f-431">64</span></span>||<span data-ttu-id="c0b3f-432">Начальное название диалогов.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-432">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="c0b3f-433">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-433">String</span></span>|||<span data-ttu-id="c0b3f-434">Ширина диалогов — число в пикселях или макет по умолчанию, такие как "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="c0b3f-434">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="c0b3f-435">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-435">String</span></span>|||<span data-ttu-id="c0b3f-436">Высота диалогов — число пикселей или макет по умолчанию, например "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="c0b3f-436">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="c0b3f-437">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-437">String</span></span>|||<span data-ttu-id="c0b3f-438">Начальный URL-адрес веб-просмотров.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-438">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="c0b3f-439">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-439">Array of Objects</span></span>|<span data-ttu-id="c0b3f-440">5 </span><span class="sxs-lookup"><span data-stu-id="c0b3f-440">5</span></span>||<span data-ttu-id="c0b3f-441">Список обработчиков, которые позволяют вызывать приложения при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-441">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="c0b3f-442">Домены также должны быть указаны в `validDomains` .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-442">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="c0b3f-443">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-443">String</span></span>|||<span data-ttu-id="c0b3f-444">Тип обработка сообщений.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-444">The type of message handler.</span></span> <span data-ttu-id="c0b3f-445">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-445">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="c0b3f-446">Массив строк</span><span class="sxs-lookup"><span data-stu-id="c0b3f-446">Array of Strings</span></span>|||<span data-ttu-id="c0b3f-447">Массив доменов, для которые обработник сообщений ссылок может зарегистрироваться.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-447">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="c0b3f-448">Массив объекта</span><span class="sxs-lookup"><span data-stu-id="c0b3f-448">Array of object</span></span>|<span data-ttu-id="c0b3f-449">5 </span><span class="sxs-lookup"><span data-stu-id="c0b3f-449">5</span></span>|<span data-ttu-id="c0b3f-450">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-450">✔</span></span>|<span data-ttu-id="c0b3f-451">Список параметров, которые принимает команда.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-451">The list of parameters the command takes.</span></span> <span data-ttu-id="c0b3f-452">Минимум: 1; максимум: 5</span><span class="sxs-lookup"><span data-stu-id="c0b3f-452">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="c0b3f-453">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-453">String</span></span>|<span data-ttu-id="c0b3f-454">64 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-454">64 characters</span></span>|<span data-ttu-id="c0b3f-455">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-455">✔</span></span>|<span data-ttu-id="c0b3f-456">Имя параметра, как оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-456">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="c0b3f-457">Это включено в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-457">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="c0b3f-458">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-458">String</span></span>|<span data-ttu-id="c0b3f-459">32 символа</span><span class="sxs-lookup"><span data-stu-id="c0b3f-459">32 characters</span></span>|<span data-ttu-id="c0b3f-460">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-460">✔</span></span>|<span data-ttu-id="c0b3f-461">Удобное название для параметра.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-461">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="c0b3f-462">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-462">String</span></span>|<span data-ttu-id="c0b3f-463">128 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-463">128 characters</span></span>||<span data-ttu-id="c0b3f-464">Удобное для пользователя строка, описываемая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-464">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="c0b3f-465">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-465">String</span></span>|<span data-ttu-id="c0b3f-466">128 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-466">128 characters</span></span>||<span data-ttu-id="c0b3f-467">Определяет тип управления, отображаемого в модуле задач `fetchTask: true` для .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-467">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="c0b3f-468">Один `text` из `textarea` , , , , , `number` `date` `time` `toggle` `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-468">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="c0b3f-469">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-469">Array of Objects</span></span>|<span data-ttu-id="c0b3f-470">10 </span><span class="sxs-lookup"><span data-stu-id="c0b3f-470">10</span></span>||<span data-ttu-id="c0b3f-471">Параметры выбора `choiceset` для .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-471">The choice options for the `choiceset`.</span></span> <span data-ttu-id="c0b3f-472">Используйте только `parameter.inputType` тогда, когда `choiceset` это .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-472">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="c0b3f-473">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-473">String</span></span>|<span data-ttu-id="c0b3f-474">128</span><span class="sxs-lookup"><span data-stu-id="c0b3f-474">128</span></span>||<span data-ttu-id="c0b3f-475">Название выбора.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-475">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="c0b3f-476">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-476">String</span></span>|<span data-ttu-id="c0b3f-477">512</span><span class="sxs-lookup"><span data-stu-id="c0b3f-477">512</span></span>||<span data-ttu-id="c0b3f-478">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-478">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="c0b3f-479">permissions</span><span class="sxs-lookup"><span data-stu-id="c0b3f-479">permissions</span></span>

<span data-ttu-id="c0b3f-480">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-480">**Optional**</span></span>

<span data-ttu-id="c0b3f-481">Массив указывает, какие разрешения запрашивает приложение, что позволяет конечным пользователям узнать, как `string` будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-481">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="c0b3f-482">Следующие параметры не являются эксклюзивными:</span><span class="sxs-lookup"><span data-stu-id="c0b3f-482">The following options are non-exclusive:</span></span>

* <span data-ttu-id="c0b3f-483">`identity`&emsp;Требуется информация о удостоверении пользователя.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-483">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="c0b3f-484">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам группы.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-484">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="c0b3f-485">Изменение этих разрешений при обновлении приложения приведет к тому, что пользователи повторят процесс согласия при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-485">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="c0b3f-486">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="c0b3f-486">devicePermissions</span></span>

<span data-ttu-id="c0b3f-487">**Необязательный** Массив строк</span><span class="sxs-lookup"><span data-stu-id="c0b3f-487">**Optional** Array of Strings</span></span>

<span data-ttu-id="c0b3f-488">Указывает родных функций на устройстве пользователя, к которое ваше приложение может запрашивать доступ.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-488">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="c0b3f-489">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="c0b3f-489">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="c0b3f-490">validDomains</span><span class="sxs-lookup"><span data-stu-id="c0b3f-490">validDomains</span></span>

<span data-ttu-id="c0b3f-491">**Необязательный,** за **исключением обязательного,** где отмечено</span><span class="sxs-lookup"><span data-stu-id="c0b3f-491">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="c0b3f-492">Список допустимого домена, из которого приложение ожидает загрузки любого контента.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-492">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="c0b3f-493">Списки домена могут включать, например, поддиайки. `*.example.com`</span><span class="sxs-lookup"><span data-stu-id="c0b3f-493">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="c0b3f-494">Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-494">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="c0b3f-495">Если конфигурации вкладок или пользовательскому интерфейсу контента необходимо перейти к любому другому домену, кроме одного использования для конфигурации вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-495">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="c0b3f-496">Однако не **обязательно** включать в приложение домены поставщиков удостоверений, которые вы хотите поддерживать.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-496">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="c0b3f-497">Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить на accounts.google.com, но не следует включать accounts.google.com `validDomains[]` в .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-497">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0b3f-498">Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью подкрентов.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-498">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="c0b3f-499">Например, `yourapp.onmicrosoft.com` допустимо, `*.onmicrosoft.com` но не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-499">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="c0b3f-500">Объект — массив со всеми элементами `string` типа.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-500">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="c0b3f-501">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="c0b3f-501">webApplicationInfo</span></span>

<span data-ttu-id="c0b3f-502">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="c0b3f-502">**Optional**</span></span>

<span data-ttu-id="c0b3f-503">Укажите свой AAD-ID и Graph, чтобы помочь пользователям легко войти в ваше приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-503">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="c0b3f-504">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-504">Name</span></span>| <span data-ttu-id="c0b3f-505">Тип</span><span class="sxs-lookup"><span data-stu-id="c0b3f-505">Type</span></span>| <span data-ttu-id="c0b3f-506">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-506">Maximum size</span></span> | <span data-ttu-id="c0b3f-507">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-507">Required</span></span> | <span data-ttu-id="c0b3f-508">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-508">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="c0b3f-509">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-509">String</span></span>|<span data-ttu-id="c0b3f-510">36 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-510">36 characters</span></span>|<span data-ttu-id="c0b3f-511">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-511">✔</span></span>|<span data-ttu-id="c0b3f-512">AAD-id приложения приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-512">AAD application id of the app.</span></span> <span data-ttu-id="c0b3f-513">Этот id должен быть GUID.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-513">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="c0b3f-514">String</span><span class="sxs-lookup"><span data-stu-id="c0b3f-514">String</span></span>|<span data-ttu-id="c0b3f-515">2048 символов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-515">2048 characters</span></span>|<span data-ttu-id="c0b3f-516">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-516">✔</span></span>|<span data-ttu-id="c0b3f-517">URL-адрес ресурса приложения для приобретения маркера auth для SSO.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-517">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="c0b3f-518">Массив</span><span class="sxs-lookup"><span data-stu-id="c0b3f-518">Array</span></span>|<span data-ttu-id="c0b3f-519">Не более 100 элементов</span><span class="sxs-lookup"><span data-stu-id="c0b3f-519">Maximum 100 items</span></span>|<span data-ttu-id="c0b3f-520">✔</span><span class="sxs-lookup"><span data-stu-id="c0b3f-520">✔</span></span>|<span data-ttu-id="c0b3f-521">Разрешения ресурсов для приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-521">Resource permissions for application.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="c0b3f-522">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="c0b3f-522">configurableProperties</span></span>

<span data-ttu-id="c0b3f-523">**Необязательный** - массив</span><span class="sxs-lookup"><span data-stu-id="c0b3f-523">**Optional** - array</span></span>

<span data-ttu-id="c0b3f-524">Блок определяет свойства приложений, которые может `configurableProperties` Teams администратор.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-524">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="c0b3f-525">Дополнительные сведения см. [в Microsoft Teams.](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="c0b3f-525">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="c0b3f-526">Необходимо определить как минимум одно свойство.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-526">A minimum of one property must be defined.</span></span> <span data-ttu-id="c0b3f-527">В этом блоке можно определить максимум девять свойств.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-527">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="c0b3f-528">В качестве наилучшей практики необходимо предоставить рекомендации по настройке для пользователей и клиентов приложений, которые следует соблюдать при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-528">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> 

<span data-ttu-id="c0b3f-529">Можно определить любое из следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="c0b3f-529">You can define any of the following properties:</span></span>
* <span data-ttu-id="c0b3f-530">`name`: Позволяет администратору изменять имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-530">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="c0b3f-531">`shortDescription`: Позволяет администратору изменить краткое описание приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-531">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="c0b3f-532">`longDescription`: Позволяет администратору изменять подробное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-532">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="c0b3f-533">`smallImageUrl`. Это `outline` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-533">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="c0b3f-534">`largeImageUrl`. Это `color` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-534">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="c0b3f-535">`accentColor`. Это цвет, который можно использовать в сочетании с и в качестве фона для значков плана.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-535">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="c0b3f-536">`websiteUrl`. Это https:// URL-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-536">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="c0b3f-537">`privacyUrl`. Это https:// url-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-537">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="c0b3f-538">`termsOfUseUrl`. Это https:// URL-адрес для условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-538">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="c0b3f-539">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="c0b3f-539">defaultInstallScope</span></span>

<span data-ttu-id="c0b3f-540">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="c0b3f-540">**Optional** - string</span></span>

<span data-ttu-id="c0b3f-541">Указывает область установки, определяемую для этого приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-541">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="c0b3f-542">Определенным областью будет параметр, отображаемый на кнопке при добавлении приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-542">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="c0b3f-543">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="c0b3f-543">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="c0b3f-544">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="c0b3f-544">defaultGroupCapability</span></span>

<span data-ttu-id="c0b3f-545">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="c0b3f-545">**Optional** - object</span></span>

<span data-ttu-id="c0b3f-546">Когда будет выбрана область установки группы, она определит возможности по умолчанию при установке приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-546">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="c0b3f-547">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="c0b3f-547">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="c0b3f-548">Имя</span><span class="sxs-lookup"><span data-stu-id="c0b3f-548">Name</span></span>| <span data-ttu-id="c0b3f-549">Тип</span><span class="sxs-lookup"><span data-stu-id="c0b3f-549">Type</span></span>| <span data-ttu-id="c0b3f-550">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="c0b3f-550">Maximum size</span></span> | <span data-ttu-id="c0b3f-551">Обязательный</span><span class="sxs-lookup"><span data-stu-id="c0b3f-551">Required</span></span> | <span data-ttu-id="c0b3f-552">Описание</span><span class="sxs-lookup"><span data-stu-id="c0b3f-552">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="c0b3f-553">string</span><span class="sxs-lookup"><span data-stu-id="c0b3f-553">string</span></span>|||<span data-ttu-id="c0b3f-554">Если выбрана область установки, это поле указывает доступные возможности `team` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-554">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="c0b3f-555">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-555">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="c0b3f-556">string</span><span class="sxs-lookup"><span data-stu-id="c0b3f-556">string</span></span>|||<span data-ttu-id="c0b3f-557">Если выбрана область установки, это поле указывает доступные возможности `groupchat` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-557">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="c0b3f-558">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-558">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="c0b3f-559">string</span><span class="sxs-lookup"><span data-stu-id="c0b3f-559">string</span></span>|||<span data-ttu-id="c0b3f-560">Если выбрана область установки, это поле указывает доступные возможности `meetings` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c0b3f-560">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="c0b3f-561">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="c0b3f-561">Options: `tab`, `bot`, or `connector`.</span></span>|

