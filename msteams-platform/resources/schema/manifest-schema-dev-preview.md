---
title: Ссылка на схему предварительного просмотра разработчика
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams
ms.topic: reference
keywords: команды проявляют схему Предварительный просмотр разработчика
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: b52d52f96312dc2978844b07a0f7ebb1d817166d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566707"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="d255a-104">Схема манифеста предварительного просмотра разработчика для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d255a-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="d255a-105">Смотрите [Предварительный просмотр разработчика](~/resources/dev-preview/developer-preview-intro.md) для получения информации о программе и о том, как вы можете присоединиться.</span><span class="sxs-lookup"><span data-stu-id="d255a-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="d255a-106">Если вы не используете предварительный просмотр разработчика, вы не должны использовать эту версию манифеста.</span><span class="sxs-lookup"><span data-stu-id="d255a-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="d255a-107">[См. Справку: Microsoft Teams для](~/resources/schema/manifest-schema.md) публичной версии манифеста.</span><span class="sxs-lookup"><span data-stu-id="d255a-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="d255a-108">В Microsoft Teams описывается, как приложение интегрируется в Microsoft Teams продукт.</span><span class="sxs-lookup"><span data-stu-id="d255a-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="d255a-109">Ваш манифест должен соответствовать схеме, размещенным на [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="d255a-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="d255a-110">Для получения дополнительной информации о доступных функциях [см.: Особенности в публичном предварительном просмотре разработчика для Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span><span class="sxs-lookup"><span data-stu-id="d255a-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="d255a-111">Образец полного манифеста</span><span class="sxs-lookup"><span data-stu-id="d255a-111">Sample full manifest</span></span>

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

<span data-ttu-id="d255a-112">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="d255a-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="d255a-113">$schema</span><span class="sxs-lookup"><span data-stu-id="d255a-113">$schema</span></span>

<span data-ttu-id="d255a-114">*Необязательно, но рекомендуется* &ndash; струна</span><span class="sxs-lookup"><span data-stu-id="d255a-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="d255a-115">В https:// URL-адрес, ссылаясь на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="d255a-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="d255a-116">манифестВерсия</span><span class="sxs-lookup"><span data-stu-id="d255a-116">manifestVersion</span></span>

<span data-ttu-id="d255a-117">**Требуется** &ndash; струна</span><span class="sxs-lookup"><span data-stu-id="d255a-117">**Required** &ndash; String</span></span>

<span data-ttu-id="d255a-118">Версия манифеста схема этого манифеста использует.</span><span class="sxs-lookup"><span data-stu-id="d255a-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="d255a-119">Это должно быть "девПревью".</span><span class="sxs-lookup"><span data-stu-id="d255a-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="d255a-120">version</span><span class="sxs-lookup"><span data-stu-id="d255a-120">version</span></span>

<span data-ttu-id="d255a-121">**Требуется** &ndash; струна</span><span class="sxs-lookup"><span data-stu-id="d255a-121">**Required** &ndash; String</span></span>

<span data-ttu-id="d255a-122">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-122">The version of the specific app.</span></span> <span data-ttu-id="d255a-123">Если вы обновите что-то в манифесте, версия также должна быть приращена.</span><span class="sxs-lookup"><span data-stu-id="d255a-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="d255a-124">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="d255a-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="d255a-125">Если это приложение было представлено в магазин, новый манифест должен быть повторно представлен и повторно проверен.</span><span class="sxs-lookup"><span data-stu-id="d255a-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="d255a-126">Затем пользователи этого приложения получат новый обновленный манифест автоматически в течение нескольких часов, после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="d255a-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="d255a-127">Если приложение запросило изменение разрешений, пользователям будет предложено обновить и повторно дать согласие на приложение.</span><span class="sxs-lookup"><span data-stu-id="d255a-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="d255a-128">Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. несовершеннолетний. ПАТЧ).</span><span class="sxs-lookup"><span data-stu-id="d255a-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="d255a-129">id</span><span class="sxs-lookup"><span data-stu-id="d255a-129">id</span></span>

<span data-ttu-id="d255a-130">**Требуется** &ndash; Идентификатор приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d255a-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="d255a-131">Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="d255a-132">Если вы зарегистрировали бота через Microsoft Bot Framework, или веб-приложение вашей вкладки уже входит в Microsoft, вы уже должны иметь идентификатор и должны ввести его здесь.</span><span class="sxs-lookup"><span data-stu-id="d255a-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="d255a-133">В противном случае, вы должны создать новый идентификатор на портале регистрации приложений Майкрософт[(Мои приложения),](https://apps.dev.microsoft.com)введите его здесь, а затем повторно использовать его [при добавляют бота](~/bots/how-to/create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="d255a-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="d255a-134">пакетИмя</span><span class="sxs-lookup"><span data-stu-id="d255a-134">packageName</span></span>

<span data-ttu-id="d255a-135">**Требуется** &ndash; струна</span><span class="sxs-lookup"><span data-stu-id="d255a-135">**Required** &ndash; String</span></span>

<span data-ttu-id="d255a-136">Уникальный идентификатор для этого приложения в обратных нотациях домена; например, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="d255a-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="d255a-137">developer</span><span class="sxs-lookup"><span data-stu-id="d255a-137">developer</span></span>

<span data-ttu-id="d255a-138">**Required**</span><span class="sxs-lookup"><span data-stu-id="d255a-138">**Required**</span></span>

<span data-ttu-id="d255a-139">Уточняет информацию о вашей компании.</span><span class="sxs-lookup"><span data-stu-id="d255a-139">Specifies information about your company.</span></span> <span data-ttu-id="d255a-140">Для приложений, представленных в AppSource (ранее Office Store), эти значения должны соответствовать информации в вашей записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="d255a-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="d255a-141">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-141">Name</span></span>| <span data-ttu-id="d255a-142">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-142">Maximum size</span></span> | <span data-ttu-id="d255a-143">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-143">Required</span></span> | <span data-ttu-id="d255a-144">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="d255a-145">32 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-145">32 characters</span></span>|<span data-ttu-id="d255a-146">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-146">✔</span></span>|<span data-ttu-id="d255a-147">Имя дисплея для разработчика.</span><span class="sxs-lookup"><span data-stu-id="d255a-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="d255a-148">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-148">2048 characters</span></span>|<span data-ttu-id="d255a-149">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-149">✔</span></span>|<span data-ttu-id="d255a-150">Данный https:// URL на веб-сайте разработчика.</span><span class="sxs-lookup"><span data-stu-id="d255a-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="d255a-151">Эта ссылка должна принимать пользователей к вашей компании или продукта конкретных страниц посадки.</span><span class="sxs-lookup"><span data-stu-id="d255a-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="d255a-152">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-152">2048 characters</span></span>|<span data-ttu-id="d255a-153">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-153">✔</span></span>|<span data-ttu-id="d255a-154">Веб https:// адрес для политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="d255a-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="d255a-155">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-155">2048 characters</span></span>|<span data-ttu-id="d255a-156">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-156">✔</span></span>|<span data-ttu-id="d255a-157">Данный https:// URL-адресу к условиям использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="d255a-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="d255a-158">10 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-158">10 characters</span></span>|<span data-ttu-id="d255a-159">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-159">✔</span></span>|<span data-ttu-id="d255a-160">**Необязательно** Идентификатор партнерской сети Майкрософт, который идентифицирует организацию-партнера, строя приложение.</span><span class="sxs-lookup"><span data-stu-id="d255a-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="d255a-161">локализацияИнфо</span><span class="sxs-lookup"><span data-stu-id="d255a-161">localizationInfo</span></span>

<span data-ttu-id="d255a-162">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="d255a-162">**Optional**</span></span>

<span data-ttu-id="d255a-163">Позволяет спецификацию языка по умолчанию, а также указатели на дополнительные языковые файлы.</span><span class="sxs-lookup"><span data-stu-id="d255a-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="d255a-164">Посмотреть [локализацию](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="d255a-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="d255a-165">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-165">Name</span></span>| <span data-ttu-id="d255a-166">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-166">Maximum size</span></span> | <span data-ttu-id="d255a-167">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-167">Required</span></span> | <span data-ttu-id="d255a-168">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="d255a-169">4 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-169">4 characters</span></span>|<span data-ttu-id="d255a-170">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-170">✔</span></span>|<span data-ttu-id="d255a-171">Языковая метка строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="d255a-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="d255a-172">локализацияИнфо.дополнительныеАнгуажи</span><span class="sxs-lookup"><span data-stu-id="d255a-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="d255a-173">Массив объектов, определяющих дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="d255a-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="d255a-174">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-174">Name</span></span>| <span data-ttu-id="d255a-175">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-175">Maximum size</span></span> | <span data-ttu-id="d255a-176">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-176">Required</span></span> | <span data-ttu-id="d255a-177">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="d255a-178">4 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-178">4 characters</span></span>|<span data-ttu-id="d255a-179">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-179">✔</span></span>|<span data-ttu-id="d255a-180">Языковая метка строк в предоставленном файле.</span><span class="sxs-lookup"><span data-stu-id="d255a-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="d255a-181">4 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-181">4 characters</span></span>|<span data-ttu-id="d255a-182">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-182">✔</span></span>|<span data-ttu-id="d255a-183">Относительный путь файла к файлу .json, содержащем переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="d255a-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="d255a-184">name</span><span class="sxs-lookup"><span data-stu-id="d255a-184">name</span></span>

<span data-ttu-id="d255a-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="d255a-185">**Required**</span></span>

<span data-ttu-id="d255a-186">Название приложения, отображаемое пользователям в приложении, Teams опыт.</span><span class="sxs-lookup"><span data-stu-id="d255a-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="d255a-187">Для приложений, представленных в AppSource, эти значения должны соответствовать информации в вашей записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="d255a-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="d255a-188">Ценности `short` и `full` не должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="d255a-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="d255a-189">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-189">Name</span></span>| <span data-ttu-id="d255a-190">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-190">Maximum size</span></span> | <span data-ttu-id="d255a-191">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-191">Required</span></span> | <span data-ttu-id="d255a-192">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="d255a-193">30 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-193">30 characters</span></span>|<span data-ttu-id="d255a-194">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-194">✔</span></span>|<span data-ttu-id="d255a-195">Краткое название дисплея для приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="d255a-196">100 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-196">100 characters</span></span>||<span data-ttu-id="d255a-197">Полное название приложения, используемое, если полное имя приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="d255a-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="d255a-198">description</span><span class="sxs-lookup"><span data-stu-id="d255a-198">description</span></span>

<span data-ttu-id="d255a-199">**Required**</span><span class="sxs-lookup"><span data-stu-id="d255a-199">**Required**</span></span>

<span data-ttu-id="d255a-200">Описывает ваше приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="d255a-200">Describes your app to users.</span></span> <span data-ttu-id="d255a-201">Для приложений, представленных в AppSource, эти значения должны соответствовать информации в вашей записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="d255a-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="d255a-202">Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет информацию, чтобы помочь потенциальным клиентам понять, что ваш опыт делает.</span><span class="sxs-lookup"><span data-stu-id="d255a-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="d255a-203">Вы также должны отметить, в полном описании, если внешний счет требуется для использования.</span><span class="sxs-lookup"><span data-stu-id="d255a-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="d255a-204">Ценности `short` и `full` не должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="d255a-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="d255a-205">Ваше краткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="d255a-206">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-206">Name</span></span>| <span data-ttu-id="d255a-207">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-207">Maximum size</span></span> | <span data-ttu-id="d255a-208">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-208">Required</span></span> | <span data-ttu-id="d255a-209">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="d255a-210">80 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-210">80 characters</span></span>|<span data-ttu-id="d255a-211">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-211">✔</span></span>|<span data-ttu-id="d255a-212">Краткое описание вашего приложения, используемого при ограничении пространства.</span><span class="sxs-lookup"><span data-stu-id="d255a-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="d255a-213">4000 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-213">4000 characters</span></span>|<span data-ttu-id="d255a-214">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-214">✔</span></span>|<span data-ttu-id="d255a-215">Полное описание вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="d255a-216">icons</span><span class="sxs-lookup"><span data-stu-id="d255a-216">icons</span></span>

<span data-ttu-id="d255a-217">**Required**</span><span class="sxs-lookup"><span data-stu-id="d255a-217">**Required**</span></span>

<span data-ttu-id="d255a-218">Иконки, используемые в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="d255a-218">Icons used within the Teams app.</span></span> <span data-ttu-id="d255a-219">Файлы значков должны быть включены в пакет загрузки.</span><span class="sxs-lookup"><span data-stu-id="d255a-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="d255a-220">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-220">Name</span></span>| <span data-ttu-id="d255a-221">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-221">Maximum size</span></span> | <span data-ttu-id="d255a-222">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-222">Required</span></span> | <span data-ttu-id="d255a-223">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="d255a-224">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-224">2048 characters</span></span>|<span data-ttu-id="d255a-225">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-225">✔</span></span>|<span data-ttu-id="d255a-226">Относительный путь файла к прозрачному значку контура 32x32 PNG.</span><span class="sxs-lookup"><span data-stu-id="d255a-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="d255a-227">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-227">2048 characters</span></span>|<span data-ttu-id="d255a-228">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-228">✔</span></span>|<span data-ttu-id="d255a-229">Относительный путь файла к полноцветной иконке 192x192 PNG.</span><span class="sxs-lookup"><span data-stu-id="d255a-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="d255a-230">акцентКолор</span><span class="sxs-lookup"><span data-stu-id="d255a-230">accentColor</span></span>

<span data-ttu-id="d255a-231">**Требуется** &ndash; струна</span><span class="sxs-lookup"><span data-stu-id="d255a-231">**Required** &ndash; String</span></span>

<span data-ttu-id="d255a-232">Цвет для использования в сочетании с и в качестве фона для вашего контура иконки.</span><span class="sxs-lookup"><span data-stu-id="d255a-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="d255a-233">Значение должно быть действительным HTML цветового кода, начиная с 'я', `#4464ee` например.</span><span class="sxs-lookup"><span data-stu-id="d255a-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="d255a-234">настраиваемыеTabs</span><span class="sxs-lookup"><span data-stu-id="d255a-234">configurableTabs</span></span>

<span data-ttu-id="d255a-235">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="d255a-235">**Optional**</span></span>

<span data-ttu-id="d255a-236">Используется, когда ваш опыт работы с приложением имеет опыт вкладки командных каналов, который требует дополнительной конфигурации, прежде чем он будет добавлен.</span><span class="sxs-lookup"><span data-stu-id="d255a-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="d255a-237">Настраиваемые вкладки поддерживаются только в области групп, и в настоящее время поддерживается только одна вкладка на приложение.</span><span class="sxs-lookup"><span data-stu-id="d255a-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="d255a-238">Объект является массивом со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="d255a-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="d255a-239">Этот блок необходим только для решений, которые обеспечивают настраиваемое решение вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="d255a-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="d255a-240">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-240">Name</span></span>| <span data-ttu-id="d255a-241">Тип</span><span class="sxs-lookup"><span data-stu-id="d255a-241">Type</span></span>| <span data-ttu-id="d255a-242">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-242">Maximum size</span></span> | <span data-ttu-id="d255a-243">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-243">Required</span></span> | <span data-ttu-id="d255a-244">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="d255a-245">String</span><span class="sxs-lookup"><span data-stu-id="d255a-245">String</span></span>|<span data-ttu-id="d255a-246">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-246">2048 characters</span></span>|<span data-ttu-id="d255a-247">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-247">✔</span></span>|<span data-ttu-id="d255a-248">Url https:// для использования при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="d255a-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="d255a-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="d255a-249">Boolean</span></span>|||<span data-ttu-id="d255a-250">Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания.</span><span class="sxs-lookup"><span data-stu-id="d255a-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="d255a-251">по умолчанию: `true`</span><span class="sxs-lookup"><span data-stu-id="d255a-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="d255a-252">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="d255a-252">Array of enum</span></span>|<span data-ttu-id="d255a-253">1</span><span class="sxs-lookup"><span data-stu-id="d255a-253">1</span></span>|<span data-ttu-id="d255a-254">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-254">✔</span></span>|<span data-ttu-id="d255a-255">В настоящее время настраиваемые вкладки поддерживают `team` только `groupchat` области и области.</span><span class="sxs-lookup"><span data-stu-id="d255a-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="d255a-256">String</span><span class="sxs-lookup"><span data-stu-id="d255a-256">String</span></span>|<span data-ttu-id="d255a-257">2048</span><span class="sxs-lookup"><span data-stu-id="d255a-257">2048</span></span>||<span data-ttu-id="d255a-258">Относительный путь файла к изображению предварительного просмотра вкладок для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d255a-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="d255a-259">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="d255a-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="d255a-260">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="d255a-260">Array of enum</span></span>|<span data-ttu-id="d255a-261">1</span><span class="sxs-lookup"><span data-stu-id="d255a-261">1</span></span>||<span data-ttu-id="d255a-262">Определяет, как ваша вкладка будет доступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d255a-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="d255a-263">Варианты `sharePointFullPage` и `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="d255a-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="d255a-264">статическиеTabs</span><span class="sxs-lookup"><span data-stu-id="d255a-264">staticTabs</span></span>

<span data-ttu-id="d255a-265">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="d255a-265">**Optional**</span></span>

<span data-ttu-id="d255a-266">Определяет набор вкладок, которые могут быть "закреплены" по умолчанию, без добавления пользователем их вручную.</span><span class="sxs-lookup"><span data-stu-id="d255a-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="d255a-267">Статические вкладки, `personal` заявленные в области, всегда прикрепляются к личному опыту приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="d255a-268">Статические вкладки, заявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="d255a-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="d255a-269">Объект является массивом (максимум 16 элементов) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="d255a-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="d255a-270">Этот блок необходим только для решений, которые обеспечивают статическое решение вкладки.</span><span class="sxs-lookup"><span data-stu-id="d255a-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="d255a-271">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-271">Name</span></span>| <span data-ttu-id="d255a-272">Тип</span><span class="sxs-lookup"><span data-stu-id="d255a-272">Type</span></span>| <span data-ttu-id="d255a-273">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-273">Maximum size</span></span> | <span data-ttu-id="d255a-274">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-274">Required</span></span> | <span data-ttu-id="d255a-275">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="d255a-276">String</span><span class="sxs-lookup"><span data-stu-id="d255a-276">String</span></span>|<span data-ttu-id="d255a-277">64 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-277">64 characters</span></span>|<span data-ttu-id="d255a-278">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-278">✔</span></span>|<span data-ttu-id="d255a-279">Уникальный идентификатор сущности, отображаемой вкладкой.</span><span class="sxs-lookup"><span data-stu-id="d255a-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="d255a-280">String</span><span class="sxs-lookup"><span data-stu-id="d255a-280">String</span></span>|<span data-ttu-id="d255a-281">128 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-281">128 characters</span></span>|<span data-ttu-id="d255a-282">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-282">✔</span></span>|<span data-ttu-id="d255a-283">Название отображения вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="d255a-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="d255a-284">String</span><span class="sxs-lookup"><span data-stu-id="d255a-284">String</span></span>|<span data-ttu-id="d255a-285">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-285">2048 characters</span></span>|<span data-ttu-id="d255a-286">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-286">✔</span></span>|<span data-ttu-id="d255a-287">В https:// URL-адрес, который указывает на пользовательский интерфейс сущности, который будет отображаться в Teams холсте.</span><span class="sxs-lookup"><span data-stu-id="d255a-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="d255a-288">String</span><span class="sxs-lookup"><span data-stu-id="d255a-288">String</span></span>|<span data-ttu-id="d255a-289">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-289">2048 characters</span></span>||<span data-ttu-id="d255a-290">Веб https:// адрес, чтобы указать на если пользователь выбирает для просмотра в браузере.</span><span class="sxs-lookup"><span data-stu-id="d255a-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="d255a-291">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="d255a-291">Array of enum</span></span>|<span data-ttu-id="d255a-292">1</span><span class="sxs-lookup"><span data-stu-id="d255a-292">1</span></span>|<span data-ttu-id="d255a-293">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-293">✔</span></span>|<span data-ttu-id="d255a-294">В настоящее время статические вкладки поддерживают только `personal` область, что означает, что она может быть предусмотрена только как часть личного опыта.</span><span class="sxs-lookup"><span data-stu-id="d255a-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="d255a-295">Ботов</span><span class="sxs-lookup"><span data-stu-id="d255a-295">bots</span></span>

<span data-ttu-id="d255a-296">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="d255a-296">**Optional**</span></span>

<span data-ttu-id="d255a-297">Определяет решение для бота, а также дополнительную информацию, такую как свойства команды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d255a-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="d255a-298">Объект массив (максимум только 1 элемент в настоящее &mdash; время только один бот допускается в приложении) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="d255a-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="d255a-299">Этот блок необходим только для решений, которые обеспечивают бот опыт.</span><span class="sxs-lookup"><span data-stu-id="d255a-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="d255a-300">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-300">Name</span></span>| <span data-ttu-id="d255a-301">Тип</span><span class="sxs-lookup"><span data-stu-id="d255a-301">Type</span></span>| <span data-ttu-id="d255a-302">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-302">Maximum size</span></span> | <span data-ttu-id="d255a-303">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-303">Required</span></span> | <span data-ttu-id="d255a-304">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="d255a-305">String</span><span class="sxs-lookup"><span data-stu-id="d255a-305">String</span></span>|<span data-ttu-id="d255a-306">64 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-306">64 characters</span></span>|<span data-ttu-id="d255a-307">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-307">✔</span></span>|<span data-ttu-id="d255a-308">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d255a-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="d255a-309">Это вполне может быть так же, как общий [идентификатор приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="d255a-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="d255a-310">Логический</span><span class="sxs-lookup"><span data-stu-id="d255a-310">Boolean</span></span>|||<span data-ttu-id="d255a-311">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="d255a-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="d255a-312">по умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="d255a-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="d255a-313">Логический</span><span class="sxs-lookup"><span data-stu-id="d255a-313">Boolean</span></span>|||<span data-ttu-id="d255a-314">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="d255a-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="d255a-315">по умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="d255a-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="d255a-316">Логический</span><span class="sxs-lookup"><span data-stu-id="d255a-316">Boolean</span></span>|||<span data-ttu-id="d255a-317">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="d255a-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="d255a-318">по умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="d255a-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="d255a-319">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="d255a-319">Array of enum</span></span>|<span data-ttu-id="d255a-320">3</span><span class="sxs-lookup"><span data-stu-id="d255a-320">3</span></span>|<span data-ttu-id="d255a-321">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-321">✔</span></span>|<span data-ttu-id="d255a-322">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="d255a-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="d255a-323">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="d255a-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="d255a-324">боты.commandLists</span><span class="sxs-lookup"><span data-stu-id="d255a-324">bots.commandLists</span></span>

<span data-ttu-id="d255a-325">Дополнительный список команд, которые ваш бот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="d255a-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="d255a-326">Объект — это массив (максимум 2 элемента) со всеми элементами `object` типа; вы должны определить отдельный список команд для каждой области, которую поддерживает ваш бот.</span><span class="sxs-lookup"><span data-stu-id="d255a-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="d255a-327">Для получения дополнительной информации [см.](~/bots/how-to/create-a-bot-commands-menu.md)</span><span class="sxs-lookup"><span data-stu-id="d255a-327">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="d255a-328">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-328">Name</span></span>| <span data-ttu-id="d255a-329">Тип</span><span class="sxs-lookup"><span data-stu-id="d255a-329">Type</span></span>| <span data-ttu-id="d255a-330">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-330">Maximum size</span></span> | <span data-ttu-id="d255a-331">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-331">Required</span></span> | <span data-ttu-id="d255a-332">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="d255a-333">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="d255a-333">array of enum</span></span>|<span data-ttu-id="d255a-334">3</span><span class="sxs-lookup"><span data-stu-id="d255a-334">3</span></span>|<span data-ttu-id="d255a-335">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-335">✔</span></span>|<span data-ttu-id="d255a-336">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="d255a-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="d255a-337">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="d255a-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="d255a-338">массив объектов</span><span class="sxs-lookup"><span data-stu-id="d255a-338">array of objects</span></span>|<span data-ttu-id="d255a-339">10 </span><span class="sxs-lookup"><span data-stu-id="d255a-339">10</span></span>|<span data-ttu-id="d255a-340">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-340">✔</span></span>|<span data-ttu-id="d255a-341">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="d255a-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="d255a-342">`title`: имя команды бота (строка, 32).</span><span class="sxs-lookup"><span data-stu-id="d255a-342">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="d255a-343">`description`: простое описание или пример синтаксиса команды и его аргумента (строка, 128).</span><span class="sxs-lookup"><span data-stu-id="d255a-343">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="d255a-344">Соединители</span><span class="sxs-lookup"><span data-stu-id="d255a-344">connectors</span></span>

<span data-ttu-id="d255a-345">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="d255a-345">**Optional**</span></span>

<span data-ttu-id="d255a-346">Блок `connectors` определяет Office 365 разъем для приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="d255a-347">Объект является массивом (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="d255a-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="d255a-348">Этот блок необходим только для решений, которые обеспечивают разъем.</span><span class="sxs-lookup"><span data-stu-id="d255a-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="d255a-349">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-349">Name</span></span>| <span data-ttu-id="d255a-350">Тип</span><span class="sxs-lookup"><span data-stu-id="d255a-350">Type</span></span>| <span data-ttu-id="d255a-351">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-351">Maximum size</span></span> | <span data-ttu-id="d255a-352">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-352">Required</span></span> | <span data-ttu-id="d255a-353">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="d255a-354">String</span><span class="sxs-lookup"><span data-stu-id="d255a-354">String</span></span>|<span data-ttu-id="d255a-355">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-355">2048 characters</span></span>|<span data-ttu-id="d255a-356">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-356">✔</span></span>|<span data-ttu-id="d255a-357"> Https:// URL для использования при настройке разъема.</span><span class="sxs-lookup"><span data-stu-id="d255a-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="d255a-358">String</span><span class="sxs-lookup"><span data-stu-id="d255a-358">String</span></span>|<span data-ttu-id="d255a-359">64 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-359">64 characters</span></span>|<span data-ttu-id="d255a-360">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-360">✔</span></span>|<span data-ttu-id="d255a-361">Уникальный идентификатор разъема, который соответствует его идентификатору в панели [разработчиков connectors.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="d255a-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="d255a-362">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="d255a-362">Array of enum</span></span>|<span data-ttu-id="d255a-363">1</span><span class="sxs-lookup"><span data-stu-id="d255a-363">1</span></span>|<span data-ttu-id="d255a-364">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-364">✔</span></span>|<span data-ttu-id="d255a-365">Определяет, предлагает ли Connector опыт в контексте канала в , или `team` опыт, установленный для отдельного пользователя в одиночку ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="d255a-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="d255a-366">В настоящее время `team` поддерживается только область охвата.</span><span class="sxs-lookup"><span data-stu-id="d255a-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="d255a-367">составьтеЭкстрасты</span><span class="sxs-lookup"><span data-stu-id="d255a-367">composeExtensions</span></span>

<span data-ttu-id="d255a-368">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="d255a-368">**Optional**</span></span>

<span data-ttu-id="d255a-369">Определяет расширение обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="d255a-370">Название функции было изменено с "составить расширение" на "расширение обмена сообщениями" в ноябре 2017 года, но имя манифеста остается прежним, так что существующие расширения продолжают функционировать.</span><span class="sxs-lookup"><span data-stu-id="d255a-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="d255a-371">Объект является массивом (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="d255a-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="d255a-372">Этот блок необходим только для решений, которые обеспечивают расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d255a-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="d255a-373">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-373">Name</span></span>| <span data-ttu-id="d255a-374">Тип</span><span class="sxs-lookup"><span data-stu-id="d255a-374">Type</span></span> | <span data-ttu-id="d255a-375">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-375">Maximum Size</span></span> | <span data-ttu-id="d255a-376">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-376">Required</span></span> | <span data-ttu-id="d255a-377">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="d255a-378">String</span><span class="sxs-lookup"><span data-stu-id="d255a-378">String</span></span>|<span data-ttu-id="d255a-379">64</span><span class="sxs-lookup"><span data-stu-id="d255a-379">64</span></span>|<span data-ttu-id="d255a-380">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-380">✔</span></span>|<span data-ttu-id="d255a-381">Уникальный идентификатор приложения Microsoft для бота, который поддерживает расширение обмена сообщениями, как зарегистрировано в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d255a-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="d255a-382">Это вполне может быть так же, как общий [идентификатор приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="d255a-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="d255a-383">Boolean</span><span class="sxs-lookup"><span data-stu-id="d255a-383">Boolean</span></span>|||<span data-ttu-id="d255a-384">Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d255a-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="d255a-385">Значение по умолчанию: `false`.</span><span class="sxs-lookup"><span data-stu-id="d255a-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="d255a-386">Массив объекта</span><span class="sxs-lookup"><span data-stu-id="d255a-386">Array of object</span></span>|<span data-ttu-id="d255a-387">10 </span><span class="sxs-lookup"><span data-stu-id="d255a-387">10</span></span>|<span data-ttu-id="d255a-388">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-388">✔</span></span>|<span data-ttu-id="d255a-389">Массив команд, которые поддерживает расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d255a-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="d255a-390">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="d255a-390">composeExtensions.commands</span></span>

<span data-ttu-id="d255a-391">Расширение обмена сообщениями должно объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="d255a-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="d255a-392">Каждая команда отображается Microsoft Teams в качестве потенциального взаимодействия из точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d255a-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="d255a-393">Существует максимум 10 команд.</span><span class="sxs-lookup"><span data-stu-id="d255a-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="d255a-394">Каждый элемент команды является объектом со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="d255a-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="d255a-395">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-395">Name</span></span>| <span data-ttu-id="d255a-396">Тип</span><span class="sxs-lookup"><span data-stu-id="d255a-396">Type</span></span>| <span data-ttu-id="d255a-397">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-397">Maximum size</span></span> | <span data-ttu-id="d255a-398">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-398">Required</span></span> | <span data-ttu-id="d255a-399">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="d255a-400">String</span><span class="sxs-lookup"><span data-stu-id="d255a-400">String</span></span>|<span data-ttu-id="d255a-401">64 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-401">64 characters</span></span>|<span data-ttu-id="d255a-402">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-402">✔</span></span>|<span data-ttu-id="d255a-403">Идентификатор команды.</span><span class="sxs-lookup"><span data-stu-id="d255a-403">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="d255a-404">String</span><span class="sxs-lookup"><span data-stu-id="d255a-404">String</span></span>|<span data-ttu-id="d255a-405">64 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-405">64 characters</span></span>||<span data-ttu-id="d255a-406">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="d255a-406">Type of the command.</span></span> <span data-ttu-id="d255a-407">Один из `query` или `action` .</span><span class="sxs-lookup"><span data-stu-id="d255a-407">One of `query` or `action`.</span></span> <span data-ttu-id="d255a-408">по умолчанию: `query`</span><span class="sxs-lookup"><span data-stu-id="d255a-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="d255a-409">String</span><span class="sxs-lookup"><span data-stu-id="d255a-409">String</span></span>|<span data-ttu-id="d255a-410">32 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-410">32 characters</span></span>|<span data-ttu-id="d255a-411">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-411">✔</span></span>|<span data-ttu-id="d255a-412">Удобное для пользователя название команды.</span><span class="sxs-lookup"><span data-stu-id="d255a-412">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="d255a-413">String</span><span class="sxs-lookup"><span data-stu-id="d255a-413">String</span></span>|<span data-ttu-id="d255a-414">128 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-414">128 characters</span></span>||<span data-ttu-id="d255a-415">Описание, которое отображается пользователям, чтобы указать цель этой команды.</span><span class="sxs-lookup"><span data-stu-id="d255a-415">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="d255a-416">Boolean</span><span class="sxs-lookup"><span data-stu-id="d255a-416">Boolean</span></span>|||<span data-ttu-id="d255a-417">Значение Boolean, указывая, следует ли запускать команду изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="d255a-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="d255a-418">по умолчанию: `false`</span><span class="sxs-lookup"><span data-stu-id="d255a-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="d255a-419">Массив строк</span><span class="sxs-lookup"><span data-stu-id="d255a-419">Array of Strings</span></span>|<span data-ttu-id="d255a-420">3</span><span class="sxs-lookup"><span data-stu-id="d255a-420">3</span></span>||<span data-ttu-id="d255a-421">Определяет, откуда можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="d255a-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="d255a-422">Любое сочетание `compose` `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="d255a-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="d255a-423">Значение по умолчанию: `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="d255a-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="d255a-424">Boolean</span><span class="sxs-lookup"><span data-stu-id="d255a-424">Boolean</span></span>|||<span data-ttu-id="d255a-425">Boolean значение, которое указывает, если он должен получить модуль задачи динамически.</span><span class="sxs-lookup"><span data-stu-id="d255a-425">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="d255a-426">Объект</span><span class="sxs-lookup"><span data-stu-id="d255a-426">Object</span></span>|||<span data-ttu-id="d255a-427">Укажите модуль задачи для предварительной загрузки при использовании команды расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d255a-427">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="d255a-428">String</span><span class="sxs-lookup"><span data-stu-id="d255a-428">String</span></span>|<span data-ttu-id="d255a-429">64</span><span class="sxs-lookup"><span data-stu-id="d255a-429">64</span></span>||<span data-ttu-id="d255a-430">Начальное название диалога.</span><span class="sxs-lookup"><span data-stu-id="d255a-430">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="d255a-431">String</span><span class="sxs-lookup"><span data-stu-id="d255a-431">String</span></span>|||<span data-ttu-id="d255a-432">Ширина Dialog - либо число пикселей, либо макет по умолчанию, такой как "большой", "средний" или "малый".</span><span class="sxs-lookup"><span data-stu-id="d255a-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="d255a-433">String</span><span class="sxs-lookup"><span data-stu-id="d255a-433">String</span></span>|||<span data-ttu-id="d255a-434">Высота Dialog - либо число пикселей, либо макет по умолчанию, такой как "большой", "средний" или "малый".</span><span class="sxs-lookup"><span data-stu-id="d255a-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="d255a-435">String</span><span class="sxs-lookup"><span data-stu-id="d255a-435">String</span></span>|||<span data-ttu-id="d255a-436">Первоначальный URL веб-адреса.</span><span class="sxs-lookup"><span data-stu-id="d255a-436">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="d255a-437">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="d255a-437">Array of Objects</span></span>|<span data-ttu-id="d255a-438">5 </span><span class="sxs-lookup"><span data-stu-id="d255a-438">5</span></span>||<span data-ttu-id="d255a-439">Список обработчиков, позволяющих вызывать приложения при работах определенных условий.</span><span class="sxs-lookup"><span data-stu-id="d255a-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="d255a-440">Домены также должны быть перечислены в `validDomains` .</span><span class="sxs-lookup"><span data-stu-id="d255a-440">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="d255a-441">String</span><span class="sxs-lookup"><span data-stu-id="d255a-441">String</span></span>|||<span data-ttu-id="d255a-442">Тип обработчика сообщений.</span><span class="sxs-lookup"><span data-stu-id="d255a-442">The type of message handler.</span></span> <span data-ttu-id="d255a-443">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="d255a-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="d255a-444">Массив строк</span><span class="sxs-lookup"><span data-stu-id="d255a-444">Array of Strings</span></span>|||<span data-ttu-id="d255a-445">Массив доменов, на которые может зарегистрироваться обработчик ссылок.</span><span class="sxs-lookup"><span data-stu-id="d255a-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="d255a-446">Массив объекта</span><span class="sxs-lookup"><span data-stu-id="d255a-446">Array of object</span></span>|<span data-ttu-id="d255a-447">5 </span><span class="sxs-lookup"><span data-stu-id="d255a-447">5</span></span>|<span data-ttu-id="d255a-448">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-448">✔</span></span>|<span data-ttu-id="d255a-449">Список параметров, которые принимает команда.</span><span class="sxs-lookup"><span data-stu-id="d255a-449">The list of parameters the command takes.</span></span> <span data-ttu-id="d255a-450">Минимум: 1; максимум: 5</span><span class="sxs-lookup"><span data-stu-id="d255a-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="d255a-451">String</span><span class="sxs-lookup"><span data-stu-id="d255a-451">String</span></span>|<span data-ttu-id="d255a-452">64 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-452">64 characters</span></span>|<span data-ttu-id="d255a-453">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-453">✔</span></span>|<span data-ttu-id="d255a-454">Название параметра, как оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="d255a-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="d255a-455">Это включено в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="d255a-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="d255a-456">String</span><span class="sxs-lookup"><span data-stu-id="d255a-456">String</span></span>|<span data-ttu-id="d255a-457">32 символа</span><span class="sxs-lookup"><span data-stu-id="d255a-457">32 characters</span></span>|<span data-ttu-id="d255a-458">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-458">✔</span></span>|<span data-ttu-id="d255a-459">Удобное название для параметра.</span><span class="sxs-lookup"><span data-stu-id="d255a-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="d255a-460">String</span><span class="sxs-lookup"><span data-stu-id="d255a-460">String</span></span>|<span data-ttu-id="d255a-461">128 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-461">128 characters</span></span>||<span data-ttu-id="d255a-462">Удобный строка, описывая цель этого параметра.</span><span class="sxs-lookup"><span data-stu-id="d255a-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="d255a-463">String</span><span class="sxs-lookup"><span data-stu-id="d255a-463">String</span></span>|<span data-ttu-id="d255a-464">128 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-464">128 characters</span></span>||<span data-ttu-id="d255a-465">Определяет тип управления, отображаемый на модуле задачи для `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="d255a-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="d255a-466">Один `text` `textarea` из, `number` , , , , `date` `time` `toggle` `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="d255a-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="d255a-467">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="d255a-467">Array of Objects</span></span>|<span data-ttu-id="d255a-468">10 </span><span class="sxs-lookup"><span data-stu-id="d255a-468">10</span></span>||<span data-ttu-id="d255a-469">Варианты выбора для `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="d255a-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="d255a-470">Использовать только тогда, `parameter.inputType` когда `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="d255a-470">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="d255a-471">String</span><span class="sxs-lookup"><span data-stu-id="d255a-471">String</span></span>|<span data-ttu-id="d255a-472">128</span><span class="sxs-lookup"><span data-stu-id="d255a-472">128</span></span>||<span data-ttu-id="d255a-473">Название выбора.</span><span class="sxs-lookup"><span data-stu-id="d255a-473">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="d255a-474">String</span><span class="sxs-lookup"><span data-stu-id="d255a-474">String</span></span>|<span data-ttu-id="d255a-475">512</span><span class="sxs-lookup"><span data-stu-id="d255a-475">512</span></span>||<span data-ttu-id="d255a-476">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="d255a-476">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="d255a-477">permissions</span><span class="sxs-lookup"><span data-stu-id="d255a-477">permissions</span></span>

<span data-ttu-id="d255a-478">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="d255a-478">**Optional**</span></span>

<span data-ttu-id="d255a-479">Массив, в `string` котором указывается, какие разрешения запрашивает приложение, который позволяет конечной пользователям знать, как будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="d255a-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="d255a-480">Следующие варианты не являются эксклюзивными:</span><span class="sxs-lookup"><span data-stu-id="d255a-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="d255a-481">`identity`&emsp;Требуется идентификационная информация пользователя.</span><span class="sxs-lookup"><span data-stu-id="d255a-481">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="d255a-482">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам команды.</span><span class="sxs-lookup"><span data-stu-id="d255a-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="d255a-483">Изменение этих разрешений при обновлении приложения приведет к тому, что пользователи впервые повторят процесс согласия при запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="d255a-484">устройствоПермиссии</span><span class="sxs-lookup"><span data-stu-id="d255a-484">devicePermissions</span></span>

<span data-ttu-id="d255a-485">**Необязательно** Массив струн</span><span class="sxs-lookup"><span data-stu-id="d255a-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="d255a-486">Определяет родные функции на устройстве пользователя, к которые ваше приложение может запросить доступ.</span><span class="sxs-lookup"><span data-stu-id="d255a-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="d255a-487">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="d255a-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="d255a-488">действительныйДомайнс</span><span class="sxs-lookup"><span data-stu-id="d255a-488">validDomains</span></span>

<span data-ttu-id="d255a-489">**Дополнительно,** за исключением **Требуемые,** где отметил</span><span class="sxs-lookup"><span data-stu-id="d255a-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="d255a-490">Список действительных доменов, из которых приложение рассчитывает загрузить любой контент.</span><span class="sxs-lookup"><span data-stu-id="d255a-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="d255a-491">Списки доменов могут включать, например, подстановочные `*.example.com` знаки.</span><span class="sxs-lookup"><span data-stu-id="d255a-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="d255a-492">Это соответствует ровно одному сегменту домена; если вам нужно, чтобы `a.b.example.com` соответствовать затем использовать `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="d255a-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="d255a-493">Если конфигурация вкладок или пользовательский интерфейс содержимого должны перемещаться в любой другой домен, кроме того, который используется для конфигурации вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="d255a-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="d255a-494">Однако **нет** необходимости включать в приложение домены поставщиков идентификации, которые вы хотите поддержать.</span><span class="sxs-lookup"><span data-stu-id="d255a-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="d255a-495">Например, для проверки подлинности с помощью Идентификатора Google необходимо перенаправить на accounts.google.com, но вы не должны включать accounts.google.com в `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="d255a-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d255a-496">Не добавляйте домены, которые находятся вне вашего контроля, ни непосредственно, ни через подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="d255a-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="d255a-497">Например, `yourapp.onmicrosoft.com` действителен, `*.onmicrosoft.com` но не действителен.</span><span class="sxs-lookup"><span data-stu-id="d255a-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="d255a-498">Объект является массивом со всеми элементами `string` типа.</span><span class="sxs-lookup"><span data-stu-id="d255a-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="d255a-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="d255a-499">webApplicationInfo</span></span>

<span data-ttu-id="d255a-500">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="d255a-500">**Optional**</span></span>

<span data-ttu-id="d255a-501">Укажите свой идентификатор приложения AAD и Graph, чтобы помочь пользователям беспрепятственно войти в ваше приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="d255a-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="d255a-502">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-502">Name</span></span>| <span data-ttu-id="d255a-503">Тип</span><span class="sxs-lookup"><span data-stu-id="d255a-503">Type</span></span>| <span data-ttu-id="d255a-504">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-504">Maximum size</span></span> | <span data-ttu-id="d255a-505">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-505">Required</span></span> | <span data-ttu-id="d255a-506">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="d255a-507">String</span><span class="sxs-lookup"><span data-stu-id="d255a-507">String</span></span>|<span data-ttu-id="d255a-508">36 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-508">36 characters</span></span>|<span data-ttu-id="d255a-509">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-509">✔</span></span>|<span data-ttu-id="d255a-510">Идентификатор приложения AAD приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-510">AAD application id of the app.</span></span> <span data-ttu-id="d255a-511">Этот идентификатор должен быть GUID.</span><span class="sxs-lookup"><span data-stu-id="d255a-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="d255a-512">String</span><span class="sxs-lookup"><span data-stu-id="d255a-512">String</span></span>|<span data-ttu-id="d255a-513">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d255a-513">2048 characters</span></span>|<span data-ttu-id="d255a-514">✔</span><span class="sxs-lookup"><span data-stu-id="d255a-514">✔</span></span>|<span data-ttu-id="d255a-515">Ресурс URL приложения для приобретения auth токена для SSO.</span><span class="sxs-lookup"><span data-stu-id="d255a-515">Resource url of app for acquiring auth token for SSO.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="d255a-516">настраиваемыеПредложения</span><span class="sxs-lookup"><span data-stu-id="d255a-516">configurableProperties</span></span>

<span data-ttu-id="d255a-517">**Дополнительно** - массив</span><span class="sxs-lookup"><span data-stu-id="d255a-517">**Optional** - array</span></span>

<span data-ttu-id="d255a-518">Блок `configurableProperties` определяет свойства приложения, которые Teams администратор может настроить.</span><span class="sxs-lookup"><span data-stu-id="d255a-518">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="d255a-519">Для получения дополнительной [информации, смотрите настроить приложения в Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="d255a-519">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="d255a-520">Необходимо определить минимум одно свойство.</span><span class="sxs-lookup"><span data-stu-id="d255a-520">A minimum of one property must be defined.</span></span> <span data-ttu-id="d255a-521">Вы можете определить максимум девять свойств в этом блоке.</span><span class="sxs-lookup"><span data-stu-id="d255a-521">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="d255a-522">В качестве наилучшей практики необходимо предоставить рекомендации по настройке для пользователей и клиентов приложений, чтобы следовать при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-522">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> 

<span data-ttu-id="d255a-523">Вы можете определить любое из следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="d255a-523">You can define any of the following properties:</span></span>
* <span data-ttu-id="d255a-524">`name`: Позволяет администратору изменить имя дисплея приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-524">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="d255a-525">`shortDescription`: Позволяет администратору изменить краткое описание приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-525">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="d255a-526">`longDescription`: Позволяет администратору изменить подробное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-526">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="d255a-527">`smallImageUrl`: Это `outline` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="d255a-527">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="d255a-528">`largeImageUrl`: Это `color` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="d255a-528">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="d255a-529">`accentColor`: Это цвет для использования в сочетании с и в качестве фона для вашего контура иконки.</span><span class="sxs-lookup"><span data-stu-id="d255a-529">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="d255a-530">`websiteUrl`: Это https:// URL на веб-сайте разработчика.</span><span class="sxs-lookup"><span data-stu-id="d255a-530">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="d255a-531">`privacyUrl`: Это https:// URL-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="d255a-531">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="d255a-532">`termsOfUseUrl`: Это https:// URL-адрес к условиям использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="d255a-532">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="d255a-533">по умолчаниюИнсталлСкоп</span><span class="sxs-lookup"><span data-stu-id="d255a-533">defaultInstallScope</span></span>

<span data-ttu-id="d255a-534">**Необязательно** - строка</span><span class="sxs-lookup"><span data-stu-id="d255a-534">**Optional** - string</span></span>

<span data-ttu-id="d255a-535">Определяет область установки, определяемую для этого приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d255a-535">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="d255a-536">Определенная область будет параметр, отображаемый на кнопке, когда пользователь пытается добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="d255a-536">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="d255a-537">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="d255a-537">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="d255a-538">по умолчаниюГруппаКапабельность</span><span class="sxs-lookup"><span data-stu-id="d255a-538">defaultGroupCapability</span></span>

<span data-ttu-id="d255a-539">**Необязательно** - объект</span><span class="sxs-lookup"><span data-stu-id="d255a-539">**Optional** - object</span></span>

<span data-ttu-id="d255a-540">При выборе области установки группы она определяет возможности по умолчанию при установке приложения.</span><span class="sxs-lookup"><span data-stu-id="d255a-540">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="d255a-541">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="d255a-541">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="d255a-542">Имя</span><span class="sxs-lookup"><span data-stu-id="d255a-542">Name</span></span>| <span data-ttu-id="d255a-543">Тип</span><span class="sxs-lookup"><span data-stu-id="d255a-543">Type</span></span>| <span data-ttu-id="d255a-544">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d255a-544">Maximum size</span></span> | <span data-ttu-id="d255a-545">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d255a-545">Required</span></span> | <span data-ttu-id="d255a-546">Описание</span><span class="sxs-lookup"><span data-stu-id="d255a-546">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="d255a-547">string</span><span class="sxs-lookup"><span data-stu-id="d255a-547">string</span></span>|||<span data-ttu-id="d255a-548">Когда выбрана область `team` установки, это поле определяет доступную возможность по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d255a-548">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="d255a-549">Варианты: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="d255a-549">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="d255a-550">Строка</span><span class="sxs-lookup"><span data-stu-id="d255a-550">string</span></span>|||<span data-ttu-id="d255a-551">Когда выбрана область `groupchat` установки, это поле определяет доступную возможность по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d255a-551">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="d255a-552">Варианты: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="d255a-552">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="d255a-553">Строка</span><span class="sxs-lookup"><span data-stu-id="d255a-553">string</span></span>|||<span data-ttu-id="d255a-554">Когда выбрана область `meetings` установки, это поле определяет доступную возможность по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d255a-554">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="d255a-555">Варианты: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="d255a-555">Options: `tab`, `bot`, or `connector`.</span></span>|

