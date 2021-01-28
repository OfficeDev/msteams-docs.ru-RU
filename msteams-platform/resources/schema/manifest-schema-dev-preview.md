---
title: Developer Preview схемы манифеста
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams
ms.topic: reference
keywords: Схема манифеста teams Developer Preview
ms.date: 05/20/2019
ms.openlocfilehash: 0776ced1704f46c95054308c8a1898ed938e47cb
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014105"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="f3e13-104">Схема манифеста предварительной версии для разработчиков для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f3e13-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="f3e13-105">Сведения [о Developer Preview](~/resources/dev-preview/developer-preview-intro.md) и о том, как можно присоединиться, см. в Developer Preview.</span><span class="sxs-lookup"><span data-stu-id="f3e13-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="f3e13-106">Если вы не используете предварительную версию для разработчиков, не следует использовать эту версию манифеста.</span><span class="sxs-lookup"><span data-stu-id="f3e13-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="f3e13-107">См. [справку. Схема манифеста для Microsoft Teams](~/resources/schema/manifest-schema.md) для общедоступных версий манифеста.</span><span class="sxs-lookup"><span data-stu-id="f3e13-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="f3e13-108">В манифесте Microsoft Teams описывается, как приложение интегрируется с продуктом Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f3e13-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="f3e13-109">Манифест должен соответствовать схеме, которая есть в [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="f3e13-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="f3e13-110">Дополнительные сведения о доступных функций см. в Developer Preview [в Microsoft Teams.](~/resources/dev-preview/developer-preview-features.md)</span><span class="sxs-lookup"><span data-stu-id="f3e13-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="f3e13-111">Пример полного манифеста</span><span class="sxs-lookup"><span data-stu-id="f3e13-111">Sample full manifest</span></span>

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
  ]
}
```

<span data-ttu-id="f3e13-112">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="f3e13-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="f3e13-113">$schema</span><span class="sxs-lookup"><span data-stu-id="f3e13-113">$schema</span></span>

<span data-ttu-id="f3e13-114">*Необязательный, но рекомендуемый* &ndash; Строка</span><span class="sxs-lookup"><span data-stu-id="f3e13-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="f3e13-115">URL-https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="f3e13-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="f3e13-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="f3e13-116">manifestVersion</span></span>

<span data-ttu-id="f3e13-117">**Обязательное** &ndash; Строка</span><span class="sxs-lookup"><span data-stu-id="f3e13-117">**Required** &ndash; String</span></span>

<span data-ttu-id="f3e13-118">Версия схемы манифеста, используемая этим манифестом.</span><span class="sxs-lookup"><span data-stu-id="f3e13-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="f3e13-119">Это должно быть "devPreview".</span><span class="sxs-lookup"><span data-stu-id="f3e13-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="f3e13-120">version</span><span class="sxs-lookup"><span data-stu-id="f3e13-120">version</span></span>

<span data-ttu-id="f3e13-121">**Обязательное** &ndash; Строка</span><span class="sxs-lookup"><span data-stu-id="f3e13-121">**Required** &ndash; String</span></span>

<span data-ttu-id="f3e13-122">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-122">The version of the specific app.</span></span> <span data-ttu-id="f3e13-123">Если вы что-то обновляете в манифесте, необходимо также приращение версии.</span><span class="sxs-lookup"><span data-stu-id="f3e13-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="f3e13-124">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="f3e13-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="f3e13-125">Если это приложение было отправлено в Магазин, новый манифест необходимо повторно представить и проверить повторно.</span><span class="sxs-lookup"><span data-stu-id="f3e13-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="f3e13-126">Затем пользователи этого приложения получат новый обновленный манифест автоматически через несколько часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="f3e13-127">Если приложение запрашивает изменение разрешений, пользователям будет предложено обновить приложение и повторно согласиться на его использование.</span><span class="sxs-lookup"><span data-stu-id="f3e13-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="f3e13-128">Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="f3e13-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="f3e13-129">id</span><span class="sxs-lookup"><span data-stu-id="f3e13-129">id</span></span>

<span data-ttu-id="f3e13-130">**Обязательное** &ndash; ИД приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="f3e13-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="f3e13-131">Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="f3e13-132">Если вы зарегистрировали бота с помощью Microsoft Bot Framework или веб-приложение вашей вкладки уже входит в microsoft, у вас должен быть уже свой ИД, и он должен ввести здесь.</span><span class="sxs-lookup"><span data-stu-id="f3e13-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="f3e13-133">В противном случае необходимо создать новый ИД на портале регистрации приложений Майкрософт[(Мои](https://apps.dev.microsoft.com)приложения), ввести его здесь, а затем повторно использовать при добавлении [бота.](~/bots/how-to/create-a-bot-for-teams.md)</span><span class="sxs-lookup"><span data-stu-id="f3e13-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="f3e13-134">packageName</span><span class="sxs-lookup"><span data-stu-id="f3e13-134">packageName</span></span>

<span data-ttu-id="f3e13-135">**Обязательно** &ndash; Строка</span><span class="sxs-lookup"><span data-stu-id="f3e13-135">**Required** &ndash; String</span></span>

<span data-ttu-id="f3e13-136">Уникальный идентификатор для этого приложения в нотации обратного домена; например, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="f3e13-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="f3e13-137">developer</span><span class="sxs-lookup"><span data-stu-id="f3e13-137">developer</span></span>

<span data-ttu-id="f3e13-138">**Required**</span><span class="sxs-lookup"><span data-stu-id="f3e13-138">**Required**</span></span>

<span data-ttu-id="f3e13-139">Указывает сведения о вашей компании.</span><span class="sxs-lookup"><span data-stu-id="f3e13-139">Specifies information about your company.</span></span> <span data-ttu-id="f3e13-140">Для приложений, отправленных в AppSource (прежнее значение — Магазин Office), эти значения должны соответствовать сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="f3e13-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="f3e13-141">Name</span><span class="sxs-lookup"><span data-stu-id="f3e13-141">Name</span></span>| <span data-ttu-id="f3e13-142">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-142">Maximum size</span></span> | <span data-ttu-id="f3e13-143">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-143">Required</span></span> | <span data-ttu-id="f3e13-144">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="f3e13-145">32 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-145">32 characters</span></span>|<span data-ttu-id="f3e13-146">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-146">✔</span></span>|<span data-ttu-id="f3e13-147">Отображаемая имя для разработчика.</span><span class="sxs-lookup"><span data-stu-id="f3e13-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="f3e13-148">2048 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-148">2048 characters</span></span>|<span data-ttu-id="f3e13-149">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-149">✔</span></span>|<span data-ttu-id="f3e13-150">Url https:// URL-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="f3e13-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="f3e13-151">По этой ссылке пользователи должны перенабираться на страницу вашей компании или конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="f3e13-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="f3e13-152">2048 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-152">2048 characters</span></span>|<span data-ttu-id="f3e13-153">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-153">✔</span></span>|<span data-ttu-id="f3e13-154">Url https:// URL-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="f3e13-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="f3e13-155">2048 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-155">2048 characters</span></span>|<span data-ttu-id="f3e13-156">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-156">✔</span></span>|<span data-ttu-id="f3e13-157">В https:// URL-адрес условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="f3e13-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="f3e13-158">10 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-158">10 characters</span></span>|<span data-ttu-id="f3e13-159">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-159">✔</span></span>|<span data-ttu-id="f3e13-160">**Необязательный** Идентификатор Microsoft Partner Network, который определяет партнерской организации, которая строит приложение.</span><span class="sxs-lookup"><span data-stu-id="f3e13-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="f3e13-161">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="f3e13-161">localizationInfo</span></span>

<span data-ttu-id="f3e13-162">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="f3e13-162">**Optional**</span></span>

<span data-ttu-id="f3e13-163">Разрешает спецификацию языка по умолчанию, а также указатели на дополнительные языковые файлы.</span><span class="sxs-lookup"><span data-stu-id="f3e13-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="f3e13-164">См. [локализацию.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="f3e13-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="f3e13-165">Name</span><span class="sxs-lookup"><span data-stu-id="f3e13-165">Name</span></span>| <span data-ttu-id="f3e13-166">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-166">Maximum size</span></span> | <span data-ttu-id="f3e13-167">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-167">Required</span></span> | <span data-ttu-id="f3e13-168">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="f3e13-169">4 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-169">4 characters</span></span>|<span data-ttu-id="f3e13-170">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-170">✔</span></span>|<span data-ttu-id="f3e13-171">Тег языка строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="f3e13-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="f3e13-172">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="f3e13-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="f3e13-173">Массив объектов, определяющих дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="f3e13-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="f3e13-174">Name</span><span class="sxs-lookup"><span data-stu-id="f3e13-174">Name</span></span>| <span data-ttu-id="f3e13-175">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-175">Maximum size</span></span> | <span data-ttu-id="f3e13-176">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-176">Required</span></span> | <span data-ttu-id="f3e13-177">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="f3e13-178">4 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-178">4 characters</span></span>|<span data-ttu-id="f3e13-179">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-179">✔</span></span>|<span data-ttu-id="f3e13-180">Тег языка строк в предоставленной файле.</span><span class="sxs-lookup"><span data-stu-id="f3e13-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="f3e13-181">4 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-181">4 characters</span></span>|<span data-ttu-id="f3e13-182">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-182">✔</span></span>|<span data-ttu-id="f3e13-183">Относительный путь к JSON-файлу, содержащего переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="f3e13-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="f3e13-184">name</span><span class="sxs-lookup"><span data-stu-id="f3e13-184">name</span></span>

<span data-ttu-id="f3e13-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="f3e13-185">**Required**</span></span>

<span data-ttu-id="f3e13-186">Имя вашего приложения, отображаемого для пользователей в teams.</span><span class="sxs-lookup"><span data-stu-id="f3e13-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="f3e13-187">Для приложений, отправленных в AppSource, эти значения должны соответствовать сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="f3e13-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="f3e13-188">Значения и `short` не `full` должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="f3e13-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="f3e13-189">Name</span><span class="sxs-lookup"><span data-stu-id="f3e13-189">Name</span></span>| <span data-ttu-id="f3e13-190">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-190">Maximum size</span></span> | <span data-ttu-id="f3e13-191">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-191">Required</span></span> | <span data-ttu-id="f3e13-192">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="f3e13-193">30 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-193">30 characters</span></span>|<span data-ttu-id="f3e13-194">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-194">✔</span></span>|<span data-ttu-id="f3e13-195">Краткое отображаемом имени приложения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="f3e13-196">100 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-196">100 characters</span></span>||<span data-ttu-id="f3e13-197">Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="f3e13-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="f3e13-198">description</span><span class="sxs-lookup"><span data-stu-id="f3e13-198">description</span></span>

<span data-ttu-id="f3e13-199">**Required**</span><span class="sxs-lookup"><span data-stu-id="f3e13-199">**Required**</span></span>

<span data-ttu-id="f3e13-200">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="f3e13-200">Describes your app to users.</span></span> <span data-ttu-id="f3e13-201">Для приложений, отправленных в AppSource, эти значения должны соответствовать сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="f3e13-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="f3e13-202">Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, которые помогут потенциальным клиентам понять, что делает ваш опыт.</span><span class="sxs-lookup"><span data-stu-id="f3e13-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="f3e13-203">В полном описании также следует отметить, требуется ли для использования внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="f3e13-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="f3e13-204">Значения и `short` не `full` должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="f3e13-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="f3e13-205">Краткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="f3e13-206">Name</span><span class="sxs-lookup"><span data-stu-id="f3e13-206">Name</span></span>| <span data-ttu-id="f3e13-207">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-207">Maximum size</span></span> | <span data-ttu-id="f3e13-208">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-208">Required</span></span> | <span data-ttu-id="f3e13-209">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="f3e13-210">80 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-210">80 characters</span></span>|<span data-ttu-id="f3e13-211">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-211">✔</span></span>|<span data-ttu-id="f3e13-212">Краткое описание работы приложения, используемое при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="f3e13-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="f3e13-213">4000 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-213">4000 characters</span></span>|<span data-ttu-id="f3e13-214">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-214">✔</span></span>|<span data-ttu-id="f3e13-215">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="f3e13-216">icons</span><span class="sxs-lookup"><span data-stu-id="f3e13-216">icons</span></span>

<span data-ttu-id="f3e13-217">**Required**</span><span class="sxs-lookup"><span data-stu-id="f3e13-217">**Required**</span></span>

<span data-ttu-id="f3e13-218">Значки, используемые в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="f3e13-218">Icons used within the Teams app.</span></span> <span data-ttu-id="f3e13-219">Файлы значков должны быть включены в пакет отправки.</span><span class="sxs-lookup"><span data-stu-id="f3e13-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="f3e13-220">Name</span><span class="sxs-lookup"><span data-stu-id="f3e13-220">Name</span></span>| <span data-ttu-id="f3e13-221">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-221">Maximum size</span></span> | <span data-ttu-id="f3e13-222">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-222">Required</span></span> | <span data-ttu-id="f3e13-223">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="f3e13-224">2048 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-224">2048 characters</span></span>|<span data-ttu-id="f3e13-225">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-225">✔</span></span>|<span data-ttu-id="f3e13-226">Относительный путь к прозрачному значку контура PNG размером 32x32.</span><span class="sxs-lookup"><span data-stu-id="f3e13-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="f3e13-227">2048 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-227">2048 characters</span></span>|<span data-ttu-id="f3e13-228">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-228">✔</span></span>|<span data-ttu-id="f3e13-229">Относительный путь к полному значку PNG размером 192x192.</span><span class="sxs-lookup"><span data-stu-id="f3e13-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="f3e13-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="f3e13-230">accentColor</span></span>

<span data-ttu-id="f3e13-231">**Обязательно** &ndash; Строка</span><span class="sxs-lookup"><span data-stu-id="f3e13-231">**Required** &ndash; String</span></span>

<span data-ttu-id="f3e13-232">Цвет, который будет применяться в сочетании с значками структур и в качестве фона.</span><span class="sxs-lookup"><span data-stu-id="f3e13-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="f3e13-233">Значением должен быть допустимый htmL-код цвета, начинающаяся с "#", например `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="f3e13-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="f3e13-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="f3e13-234">configurableTabs</span></span>

<span data-ttu-id="f3e13-235">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="f3e13-235">**Optional**</span></span>

<span data-ttu-id="f3e13-236">Используется, когда в вашем приложении есть вкладка канала команды, которая требует дополнительной настройки перед его добавлением.</span><span class="sxs-lookup"><span data-stu-id="f3e13-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="f3e13-237">Настраиваемые вкладки поддерживаются только в области групп, и в настоящее время поддерживается только одна вкладка для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="f3e13-238">Объект является массивом со всеми элементами этого `object` типа.</span><span class="sxs-lookup"><span data-stu-id="f3e13-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="f3e13-239">Этот блок требуется только для решений, которые предоставляют настраиваемое решение для вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="f3e13-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="f3e13-240">Имя</span><span class="sxs-lookup"><span data-stu-id="f3e13-240">Name</span></span>| <span data-ttu-id="f3e13-241">Тип</span><span class="sxs-lookup"><span data-stu-id="f3e13-241">Type</span></span>| <span data-ttu-id="f3e13-242">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-242">Maximum size</span></span> | <span data-ttu-id="f3e13-243">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-243">Required</span></span> | <span data-ttu-id="f3e13-244">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="f3e13-245">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-245">String</span></span>|<span data-ttu-id="f3e13-246">2048 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-246">2048 characters</span></span>|<span data-ttu-id="f3e13-247">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-247">✔</span></span>|<span data-ttu-id="f3e13-248">URL-https://, который будет применяться при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="f3e13-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="f3e13-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="f3e13-249">Boolean</span></span>|||<span data-ttu-id="f3e13-250">Значение, указывающее, может ли пользователь обновить экземпляр конфигурации вкладки после создания.</span><span class="sxs-lookup"><span data-stu-id="f3e13-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="f3e13-251">По умолчанию: `true`</span><span class="sxs-lookup"><span data-stu-id="f3e13-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="f3e13-252">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="f3e13-252">Array of enum</span></span>|<span data-ttu-id="f3e13-253">1 </span><span class="sxs-lookup"><span data-stu-id="f3e13-253">1</span></span>|<span data-ttu-id="f3e13-254">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-254">✔</span></span>|<span data-ttu-id="f3e13-255">В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области.</span><span class="sxs-lookup"><span data-stu-id="f3e13-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="f3e13-256">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-256">String</span></span>|<span data-ttu-id="f3e13-257">2048</span><span class="sxs-lookup"><span data-stu-id="f3e13-257">2048</span></span>||<span data-ttu-id="f3e13-258">Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f3e13-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="f3e13-259">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="f3e13-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="f3e13-260">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="f3e13-260">Array of enum</span></span>|<span data-ttu-id="f3e13-261">1 </span><span class="sxs-lookup"><span data-stu-id="f3e13-261">1</span></span>||<span data-ttu-id="f3e13-262">Определяет, как вкладка будет доступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f3e13-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="f3e13-263">Возможные `sharePointFullPage` варианты `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="f3e13-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="f3e13-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="f3e13-264">staticTabs</span></span>

<span data-ttu-id="f3e13-265">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="f3e13-265">**Optional**</span></span>

<span data-ttu-id="f3e13-266">Определяет набор вкладок, которые можно "закрепить" по умолчанию без добавления пользователем вручную.</span><span class="sxs-lookup"><span data-stu-id="f3e13-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="f3e13-267">Статические вкладки, объявленные в области, всегда закреплены в личном режиме `personal` приложения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="f3e13-268">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="f3e13-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="f3e13-269">Объект является массивом (не более 16 элементов) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="f3e13-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="f3e13-270">Этот блок требуется только для решений, которые предоставляют статическое решение вкладок.</span><span class="sxs-lookup"><span data-stu-id="f3e13-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="f3e13-271">Имя</span><span class="sxs-lookup"><span data-stu-id="f3e13-271">Name</span></span>| <span data-ttu-id="f3e13-272">Тип</span><span class="sxs-lookup"><span data-stu-id="f3e13-272">Type</span></span>| <span data-ttu-id="f3e13-273">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-273">Maximum size</span></span> | <span data-ttu-id="f3e13-274">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-274">Required</span></span> | <span data-ttu-id="f3e13-275">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="f3e13-276">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-276">String</span></span>|<span data-ttu-id="f3e13-277">64 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-277">64 characters</span></span>|<span data-ttu-id="f3e13-278">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-278">✔</span></span>|<span data-ttu-id="f3e13-279">Уникальный идентификатор сущности, отображаемой на вкладке.</span><span class="sxs-lookup"><span data-stu-id="f3e13-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="f3e13-280">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-280">String</span></span>|<span data-ttu-id="f3e13-281">128 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-281">128 characters</span></span>|<span data-ttu-id="f3e13-282">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-282">✔</span></span>|<span data-ttu-id="f3e13-283">Отображаемого имени вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="f3e13-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="f3e13-284">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-284">String</span></span>|<span data-ttu-id="f3e13-285">2048 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-285">2048 characters</span></span>|<span data-ttu-id="f3e13-286">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-286">✔</span></span>|<span data-ttu-id="f3e13-287">URL-https://, который указывает на пользовательский интерфейс сущности, который будет отображаться на холсте Teams.</span><span class="sxs-lookup"><span data-stu-id="f3e13-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="f3e13-288">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-288">String</span></span>|<span data-ttu-id="f3e13-289">2048 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-289">2048 characters</span></span>||<span data-ttu-id="f3e13-290">Url https:// URL-адрес, на который нужно указать, если пользователь выбирает просмотр в браузере.</span><span class="sxs-lookup"><span data-stu-id="f3e13-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="f3e13-291">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="f3e13-291">Array of enum</span></span>|<span data-ttu-id="f3e13-292">1 </span><span class="sxs-lookup"><span data-stu-id="f3e13-292">1</span></span>|<span data-ttu-id="f3e13-293">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-293">✔</span></span>|<span data-ttu-id="f3e13-294">В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в рамках личного `personal` опыта.</span><span class="sxs-lookup"><span data-stu-id="f3e13-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="f3e13-295">bots</span><span class="sxs-lookup"><span data-stu-id="f3e13-295">bots</span></span>

<span data-ttu-id="f3e13-296">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="f3e13-296">**Optional**</span></span>

<span data-ttu-id="f3e13-297">Определяет бот-решение, а также необязательные сведения, такие как свойства команды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f3e13-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="f3e13-298">Объект является массивом (не более 1 элемента в настоящее время разрешено использовать только один бот для каждого приложения) со всеми элементами &mdash; этого `object` типа.</span><span class="sxs-lookup"><span data-stu-id="f3e13-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="f3e13-299">Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.</span><span class="sxs-lookup"><span data-stu-id="f3e13-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="f3e13-300">Имя</span><span class="sxs-lookup"><span data-stu-id="f3e13-300">Name</span></span>| <span data-ttu-id="f3e13-301">Тип</span><span class="sxs-lookup"><span data-stu-id="f3e13-301">Type</span></span>| <span data-ttu-id="f3e13-302">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-302">Maximum size</span></span> | <span data-ttu-id="f3e13-303">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-303">Required</span></span> | <span data-ttu-id="f3e13-304">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="f3e13-305">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-305">String</span></span>|<span data-ttu-id="f3e13-306">64 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-306">64 characters</span></span>|<span data-ttu-id="f3e13-307">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-307">✔</span></span>|<span data-ttu-id="f3e13-308">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="f3e13-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="f3e13-309">Вполне возможно, что он будет таким же, как и [общий ИД приложения.](#id)</span><span class="sxs-lookup"><span data-stu-id="f3e13-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="f3e13-310">Логический</span><span class="sxs-lookup"><span data-stu-id="f3e13-310">Boolean</span></span>|||<span data-ttu-id="f3e13-311">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="f3e13-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="f3e13-312">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="f3e13-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="f3e13-313">Логический</span><span class="sxs-lookup"><span data-stu-id="f3e13-313">Boolean</span></span>|||<span data-ttu-id="f3e13-314">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="f3e13-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="f3e13-315">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="f3e13-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="f3e13-316">Логический</span><span class="sxs-lookup"><span data-stu-id="f3e13-316">Boolean</span></span>|||<span data-ttu-id="f3e13-317">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="f3e13-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="f3e13-318">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="f3e13-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="f3e13-319">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="f3e13-319">Array of enum</span></span>|<span data-ttu-id="f3e13-320">3</span><span class="sxs-lookup"><span data-stu-id="f3e13-320">3</span></span>|<span data-ttu-id="f3e13-321">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-321">✔</span></span>|<span data-ttu-id="f3e13-322">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="f3e13-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="f3e13-323">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="f3e13-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="f3e13-324">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="f3e13-324">bots.commandLists</span></span>

<span data-ttu-id="f3e13-325">Необязательный список команд, которые бот может порекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="f3e13-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="f3e13-326">Объект является массивом (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом.</span><span class="sxs-lookup"><span data-stu-id="f3e13-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="f3e13-327">Дополнительные [сведения см. в](~/bots/how-to/create-a-bot-commands-menu.md) меню бота.</span><span class="sxs-lookup"><span data-stu-id="f3e13-327">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="f3e13-328">Имя</span><span class="sxs-lookup"><span data-stu-id="f3e13-328">Name</span></span>| <span data-ttu-id="f3e13-329">Тип</span><span class="sxs-lookup"><span data-stu-id="f3e13-329">Type</span></span>| <span data-ttu-id="f3e13-330">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-330">Maximum size</span></span> | <span data-ttu-id="f3e13-331">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-331">Required</span></span> | <span data-ttu-id="f3e13-332">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="f3e13-333">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="f3e13-333">array of enum</span></span>|<span data-ttu-id="f3e13-334">3</span><span class="sxs-lookup"><span data-stu-id="f3e13-334">3</span></span>|<span data-ttu-id="f3e13-335">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-335">✔</span></span>|<span data-ttu-id="f3e13-336">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="f3e13-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="f3e13-337">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="f3e13-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="f3e13-338">массив объектов</span><span class="sxs-lookup"><span data-stu-id="f3e13-338">array of objects</span></span>|<span data-ttu-id="f3e13-339">10 </span><span class="sxs-lookup"><span data-stu-id="f3e13-339">10</span></span>|<span data-ttu-id="f3e13-340">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-340">✔</span></span>|<span data-ttu-id="f3e13-341">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="f3e13-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="f3e13-342">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="f3e13-342">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="f3e13-343">`description`: простое описание или пример синтаксиса команды и ее аргумента (строка, 128)</span><span class="sxs-lookup"><span data-stu-id="f3e13-343">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="f3e13-344">соединители</span><span class="sxs-lookup"><span data-stu-id="f3e13-344">connectors</span></span>

<span data-ttu-id="f3e13-345">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="f3e13-345">**Optional**</span></span>

<span data-ttu-id="f3e13-346">Этот `connectors` блок определяет соединители Office 365 для приложения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="f3e13-347">Объект является массивом (не более 1 элемента) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="f3e13-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="f3e13-348">Этот блок требуется только для решений, которые предоставляют соединители.</span><span class="sxs-lookup"><span data-stu-id="f3e13-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="f3e13-349">Имя</span><span class="sxs-lookup"><span data-stu-id="f3e13-349">Name</span></span>| <span data-ttu-id="f3e13-350">Тип</span><span class="sxs-lookup"><span data-stu-id="f3e13-350">Type</span></span>| <span data-ttu-id="f3e13-351">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-351">Maximum size</span></span> | <span data-ttu-id="f3e13-352">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-352">Required</span></span> | <span data-ttu-id="f3e13-353">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="f3e13-354">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-354">String</span></span>|<span data-ttu-id="f3e13-355">2048 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-355">2048 characters</span></span>|<span data-ttu-id="f3e13-356">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-356">✔</span></span>|<span data-ttu-id="f3e13-357">URL https:// URL-адрес, который будет применяться при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="f3e13-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="f3e13-358">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-358">String</span></span>|<span data-ttu-id="f3e13-359">64 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-359">64 characters</span></span>|<span data-ttu-id="f3e13-360">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-360">✔</span></span>|<span data-ttu-id="f3e13-361">Уникальный идентификатор соединители, который соответствует его идентификатору в информационной панели разработчика [соединителок.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="f3e13-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="f3e13-362">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="f3e13-362">Array of enum</span></span>|<span data-ttu-id="f3e13-363">1 </span><span class="sxs-lookup"><span data-stu-id="f3e13-363">1</span></span>|<span data-ttu-id="f3e13-364">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-364">✔</span></span>|<span data-ttu-id="f3e13-365">Указывает, предоставляет ли соединители интерфейс в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="f3e13-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="f3e13-366">В настоящее время `team` поддерживается только область.</span><span class="sxs-lookup"><span data-stu-id="f3e13-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="f3e13-367">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="f3e13-367">composeExtensions</span></span>

<span data-ttu-id="f3e13-368">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="f3e13-368">**Optional**</span></span>

<span data-ttu-id="f3e13-369">Определяет расширение обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="f3e13-370">В ноябре 2017 г. имя функции было изменено с "расширения составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжают функционировать.</span><span class="sxs-lookup"><span data-stu-id="f3e13-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="f3e13-371">Объект является массивом (не более 1 элемента) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="f3e13-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="f3e13-372">Этот блок необходим только для решений, которые предоставляют расширение для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="f3e13-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="f3e13-373">Имя</span><span class="sxs-lookup"><span data-stu-id="f3e13-373">Name</span></span>| <span data-ttu-id="f3e13-374">Тип</span><span class="sxs-lookup"><span data-stu-id="f3e13-374">Type</span></span> | <span data-ttu-id="f3e13-375">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-375">Maximum Size</span></span> | <span data-ttu-id="f3e13-376">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-376">Required</span></span> | <span data-ttu-id="f3e13-377">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="f3e13-378">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-378">String</span></span>|<span data-ttu-id="f3e13-379">64</span><span class="sxs-lookup"><span data-stu-id="f3e13-379">64</span></span>|<span data-ttu-id="f3e13-380">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-380">✔</span></span>|<span data-ttu-id="f3e13-381">Уникальный ИД приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрировано в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="f3e13-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="f3e13-382">Вполне возможно, что он будет таким же, как и общий [ИД приложения.](#id)</span><span class="sxs-lookup"><span data-stu-id="f3e13-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="f3e13-383">Boolean</span><span class="sxs-lookup"><span data-stu-id="f3e13-383">Boolean</span></span>|||<span data-ttu-id="f3e13-384">Значение, указывающее, может ли пользователь обновлять конфигурацию расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="f3e13-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="f3e13-385">Значение по `false` умолчанию: .</span><span class="sxs-lookup"><span data-stu-id="f3e13-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="f3e13-386">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="f3e13-386">Array of object</span></span>|<span data-ttu-id="f3e13-387">10 </span><span class="sxs-lookup"><span data-stu-id="f3e13-387">10</span></span>|<span data-ttu-id="f3e13-388">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-388">✔</span></span>|<span data-ttu-id="f3e13-389">Массив команд, поддерживаемых расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="f3e13-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="f3e13-390">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="f3e13-390">composeExtensions.commands</span></span>

<span data-ttu-id="f3e13-391">Расширение обмена сообщениями должно объявлять одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="f3e13-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="f3e13-392">Каждая команда отображается в Microsoft Teams как потенциальное взаимодействие с точкой входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f3e13-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="f3e13-393">Максимум 10 команд.</span><span class="sxs-lookup"><span data-stu-id="f3e13-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="f3e13-394">Каждый элемент команды является объектом со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="f3e13-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="f3e13-395">Имя</span><span class="sxs-lookup"><span data-stu-id="f3e13-395">Name</span></span>| <span data-ttu-id="f3e13-396">Тип</span><span class="sxs-lookup"><span data-stu-id="f3e13-396">Type</span></span>| <span data-ttu-id="f3e13-397">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-397">Maximum size</span></span> | <span data-ttu-id="f3e13-398">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-398">Required</span></span> | <span data-ttu-id="f3e13-399">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="f3e13-400">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-400">String</span></span>|<span data-ttu-id="f3e13-401">64 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-401">64 characters</span></span>|<span data-ttu-id="f3e13-402">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-402">✔</span></span>|<span data-ttu-id="f3e13-403">ИД команды</span><span class="sxs-lookup"><span data-stu-id="f3e13-403">The ID for the command</span></span>|
|`type`|<span data-ttu-id="f3e13-404">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-404">String</span></span>|<span data-ttu-id="f3e13-405">64 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-405">64 characters</span></span>||<span data-ttu-id="f3e13-406">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="f3e13-406">Type of the command.</span></span> <span data-ttu-id="f3e13-407">Один из `query` или `action` .</span><span class="sxs-lookup"><span data-stu-id="f3e13-407">One of `query` or `action`.</span></span> <span data-ttu-id="f3e13-408">По умолчанию: `query`</span><span class="sxs-lookup"><span data-stu-id="f3e13-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="f3e13-409">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-409">String</span></span>|<span data-ttu-id="f3e13-410">32 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-410">32 characters</span></span>|<span data-ttu-id="f3e13-411">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-411">✔</span></span>|<span data-ttu-id="f3e13-412">Удобное имя команды</span><span class="sxs-lookup"><span data-stu-id="f3e13-412">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="f3e13-413">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-413">String</span></span>|<span data-ttu-id="f3e13-414">128 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-414">128 characters</span></span>||<span data-ttu-id="f3e13-415">Описание, которое отображается для пользователей, чтобы указать назначение этой команды</span><span class="sxs-lookup"><span data-stu-id="f3e13-415">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="f3e13-416">Boolean</span><span class="sxs-lookup"><span data-stu-id="f3e13-416">Boolean</span></span>|||<span data-ttu-id="f3e13-417">Boolean value that indicates whether the command should be run initially with no parameters.</span><span class="sxs-lookup"><span data-stu-id="f3e13-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="f3e13-418">По умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="f3e13-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="f3e13-419">Массив строк</span><span class="sxs-lookup"><span data-stu-id="f3e13-419">Array of Strings</span></span>|<span data-ttu-id="f3e13-420">3</span><span class="sxs-lookup"><span data-stu-id="f3e13-420">3</span></span>||<span data-ttu-id="f3e13-421">Определяет, откуда можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="f3e13-422">Любое сочетание `compose` , `commandBox` . `message`</span><span class="sxs-lookup"><span data-stu-id="f3e13-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="f3e13-423">Значение по умолчанию: `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="f3e13-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="f3e13-424">Boolean</span><span class="sxs-lookup"><span data-stu-id="f3e13-424">Boolean</span></span>|||<span data-ttu-id="f3e13-425">Boolean value that indicates if it should fetch the task module dynamically</span><span class="sxs-lookup"><span data-stu-id="f3e13-425">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="f3e13-426">Объект</span><span class="sxs-lookup"><span data-stu-id="f3e13-426">Object</span></span>|||<span data-ttu-id="f3e13-427">Указание модуля задачи для предварительной загрузки при использовании команды расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="f3e13-427">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="f3e13-428">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-428">String</span></span>|<span data-ttu-id="f3e13-429">64</span><span class="sxs-lookup"><span data-stu-id="f3e13-429">64</span></span>||<span data-ttu-id="f3e13-430">Заголовок начального диалоговое окно</span><span class="sxs-lookup"><span data-stu-id="f3e13-430">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="f3e13-431">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-431">String</span></span>|||<span data-ttu-id="f3e13-432">Ширина диалогов — число в пикселях или макет по умолчанию, например"большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="f3e13-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="f3e13-433">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-433">String</span></span>|||<span data-ttu-id="f3e13-434">Высота диалогов — число в пикселях или макет по умолчанию, например"большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="f3e13-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="f3e13-435">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-435">String</span></span>|||<span data-ttu-id="f3e13-436">Исходный URL-адрес веб-приложения</span><span class="sxs-lookup"><span data-stu-id="f3e13-436">Initial webview URL</span></span>|
|`messageHandlers`|<span data-ttu-id="f3e13-437">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="f3e13-437">Array of Objects</span></span>|<span data-ttu-id="f3e13-438">5 </span><span class="sxs-lookup"><span data-stu-id="f3e13-438">5</span></span>||<span data-ttu-id="f3e13-439">Список обработчиков, которые позволяют вызывать приложения при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="f3e13-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="f3e13-440">Домены также должны быть указаны в списке `validDomains`</span><span class="sxs-lookup"><span data-stu-id="f3e13-440">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="f3e13-441">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-441">String</span></span>|||<span data-ttu-id="f3e13-442">Тип обработера сообщений.</span><span class="sxs-lookup"><span data-stu-id="f3e13-442">The type of message handler.</span></span> <span data-ttu-id="f3e13-443">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="f3e13-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="f3e13-444">Массив строк</span><span class="sxs-lookup"><span data-stu-id="f3e13-444">Array of Strings</span></span>|||<span data-ttu-id="f3e13-445">Массив доменов, для которые может регистрироваться обработник сообщений ссылок.</span><span class="sxs-lookup"><span data-stu-id="f3e13-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="f3e13-446">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="f3e13-446">Array of object</span></span>|<span data-ttu-id="f3e13-447">5 </span><span class="sxs-lookup"><span data-stu-id="f3e13-447">5</span></span>|<span data-ttu-id="f3e13-448">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-448">✔</span></span>|<span data-ttu-id="f3e13-449">Список параметров, которые принимает команда.</span><span class="sxs-lookup"><span data-stu-id="f3e13-449">The list of parameters the command takes.</span></span> <span data-ttu-id="f3e13-450">Минимум: 1; максимум: 5</span><span class="sxs-lookup"><span data-stu-id="f3e13-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="f3e13-451">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-451">String</span></span>|<span data-ttu-id="f3e13-452">64 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-452">64 characters</span></span>|<span data-ttu-id="f3e13-453">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-453">✔</span></span>|<span data-ttu-id="f3e13-454">Имя параметра, которое отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="f3e13-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="f3e13-455">Это включается в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="f3e13-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="f3e13-456">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-456">String</span></span>|<span data-ttu-id="f3e13-457">32 символа</span><span class="sxs-lookup"><span data-stu-id="f3e13-457">32 characters</span></span>|<span data-ttu-id="f3e13-458">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-458">✔</span></span>|<span data-ttu-id="f3e13-459">Удобное название параметра.</span><span class="sxs-lookup"><span data-stu-id="f3e13-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="f3e13-460">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-460">String</span></span>|<span data-ttu-id="f3e13-461">128 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-461">128 characters</span></span>||<span data-ttu-id="f3e13-462">Пользовательская строка, описывая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="f3e13-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="f3e13-463">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-463">String</span></span>|<span data-ttu-id="f3e13-464">128 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-464">128 characters</span></span>||<span data-ttu-id="f3e13-465">Определяет тип управления, отображаемого в модуле задачи для `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="f3e13-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="f3e13-466">Один из `text` `textarea` , , , `number` `date` `time` , `toggle``choiceset`</span><span class="sxs-lookup"><span data-stu-id="f3e13-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="f3e13-467">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="f3e13-467">Array of Objects</span></span>|<span data-ttu-id="f3e13-468">10 </span><span class="sxs-lookup"><span data-stu-id="f3e13-468">10</span></span>||<span data-ttu-id="f3e13-469">Варианты выбора для `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="f3e13-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="f3e13-470">Используйте только в том `parameter.inputType` случае, если это `choiceset`</span><span class="sxs-lookup"><span data-stu-id="f3e13-470">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="f3e13-471">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-471">String</span></span>|<span data-ttu-id="f3e13-472">128</span><span class="sxs-lookup"><span data-stu-id="f3e13-472">128</span></span>||<span data-ttu-id="f3e13-473">Заголовок выбора</span><span class="sxs-lookup"><span data-stu-id="f3e13-473">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="f3e13-474">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-474">String</span></span>|<span data-ttu-id="f3e13-475">512</span><span class="sxs-lookup"><span data-stu-id="f3e13-475">512</span></span>||<span data-ttu-id="f3e13-476">Значение выбора</span><span class="sxs-lookup"><span data-stu-id="f3e13-476">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="f3e13-477">permissions</span><span class="sxs-lookup"><span data-stu-id="f3e13-477">permissions</span></span>

<span data-ttu-id="f3e13-478">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="f3e13-478">**Optional**</span></span>

<span data-ttu-id="f3e13-479">Массив, в котором указывается, какие разрешения запрашивает приложение, что позволяет конечным пользователям узнать, как `string` будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="f3e13-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="f3e13-480">Следующие параметры являются неисключающими:</span><span class="sxs-lookup"><span data-stu-id="f3e13-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="f3e13-481">`identity`&emsp;Требуется информация об удостоверении пользователя</span><span class="sxs-lookup"><span data-stu-id="f3e13-481">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="f3e13-482">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений участникам группы</span><span class="sxs-lookup"><span data-stu-id="f3e13-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="f3e13-483">Изменение этих разрешений при обновлении приложения приведет к повтору пользователями процесса получения согласия при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="f3e13-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="f3e13-484">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="f3e13-484">devicePermissions</span></span>

<span data-ttu-id="f3e13-485">**Необязательный** Массив строк</span><span class="sxs-lookup"><span data-stu-id="f3e13-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="f3e13-486">Указывает нативные функции на устройстве пользователя, к которые ваше приложение может запросить доступ.</span><span class="sxs-lookup"><span data-stu-id="f3e13-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="f3e13-487">Возможные варианты:</span><span class="sxs-lookup"><span data-stu-id="f3e13-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="f3e13-488">validDomains</span><span class="sxs-lookup"><span data-stu-id="f3e13-488">validDomains</span></span>

<span data-ttu-id="f3e13-489">**Необязательный**, за **исключением обязательного,** если отмечено</span><span class="sxs-lookup"><span data-stu-id="f3e13-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="f3e13-490">Список действительных доменов, из которых приложение ожидает загрузки любого содержимого.</span><span class="sxs-lookup"><span data-stu-id="f3e13-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="f3e13-491">В списки доменов могут включались поддеревные знаки, `*.example.com` например.</span><span class="sxs-lookup"><span data-stu-id="f3e13-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="f3e13-492">Это соответствует только одному сегменту домена; если вам нужно найти `a.b.example.com` соответствие, используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="f3e13-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="f3e13-493">Если конфигурации вкладок или пользовательскому интерфейсу содержимого требуется перейти к любому другому домену, кроме того, который используется для настройки вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="f3e13-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="f3e13-494">Однако нет **необходимости** включать в приложение домены поставщиков удостоверений, которые вы хотите поддерживать.</span><span class="sxs-lookup"><span data-stu-id="f3e13-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="f3e13-495">Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить его на accounts.google.com, но не следует включать `validDomains[]` accounts.google.com.</span><span class="sxs-lookup"><span data-stu-id="f3e13-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3e13-496">Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью поддиагром.</span><span class="sxs-lookup"><span data-stu-id="f3e13-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="f3e13-497">Например, `yourapp.onmicrosoft.com` допустимо, но `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="f3e13-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="f3e13-498">Объект является массивом со всеми элементами этого `string` типа.</span><span class="sxs-lookup"><span data-stu-id="f3e13-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="f3e13-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="f3e13-499">webApplicationInfo</span></span>

<span data-ttu-id="f3e13-500">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="f3e13-500">**Optional**</span></span>

<span data-ttu-id="f3e13-501">Укажите свой ИД приложения AAD и данные Graph, чтобы пользователи легко влияли на ваше приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="f3e13-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="f3e13-502">Имя</span><span class="sxs-lookup"><span data-stu-id="f3e13-502">Name</span></span>| <span data-ttu-id="f3e13-503">Тип</span><span class="sxs-lookup"><span data-stu-id="f3e13-503">Type</span></span>| <span data-ttu-id="f3e13-504">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="f3e13-504">Maximum size</span></span> | <span data-ttu-id="f3e13-505">Обязательный</span><span class="sxs-lookup"><span data-stu-id="f3e13-505">Required</span></span> | <span data-ttu-id="f3e13-506">Описание</span><span class="sxs-lookup"><span data-stu-id="f3e13-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="f3e13-507">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-507">String</span></span>|<span data-ttu-id="f3e13-508">36 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-508">36 characters</span></span>|<span data-ttu-id="f3e13-509">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-509">✔</span></span>|<span data-ttu-id="f3e13-510">ИД приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="f3e13-510">AAD application id of the app.</span></span> <span data-ttu-id="f3e13-511">Этот ид должен быть GUID.</span><span class="sxs-lookup"><span data-stu-id="f3e13-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="f3e13-512">String</span><span class="sxs-lookup"><span data-stu-id="f3e13-512">String</span></span>|<span data-ttu-id="f3e13-513">2048 символов</span><span class="sxs-lookup"><span data-stu-id="f3e13-513">2048 characters</span></span>|<span data-ttu-id="f3e13-514">✔</span><span class="sxs-lookup"><span data-stu-id="f3e13-514">✔</span></span>|<span data-ttu-id="f3e13-515">URL-адрес ресурса приложения для получения маркера auth для SSO.</span><span class="sxs-lookup"><span data-stu-id="f3e13-515">Resource url of app for acquiring auth token for SSO.</span></span>|