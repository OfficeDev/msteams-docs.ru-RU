---
title: Справочник по схеме манифеста для предварительного просмотра для разработчиков
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams.
keywords: Предварительная версия для разработчиков схемы манифеста Teams
ms.date: 05/20/2019
ms.openlocfilehash: b99e1ae99b7fd1edd4c695f43f3ac25270f0c710
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675190"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="9e5ea-104">Схема манифеста предварительной версии для разработчиков Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9e5ea-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="9e5ea-105">Сведения о программе и способе присоединения можно найти в разделе [Preview Developer](~/resources/dev-preview/developer-preview-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="9e5ea-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="9e5ea-106">Если вы не используете предварительный просмотр разработчика, не следует использовать эту версию манифеста.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="9e5ea-107">Ознакомьтесь со статьей [reference: schema manifest для Microsoft Teams](~/resources/schema/manifest-schema.md) для общедоступной версии манифеста.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="9e5ea-108">Манифест Microsoft Teams описывает, как приложение интегрируется в продукт Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="9e5ea-109">Манифест должен соответствовать схеме, размещенной в [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="9e5ea-110">Дополнительные сведения о доступных функциях: [функции в общедоступной предварительной версии для разработчиков Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="9e5ea-111">Пример полного манифеста</span><span class="sxs-lookup"><span data-stu-id="9e5ea-111">Sample full manifest</span></span>

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

<span data-ttu-id="9e5ea-112">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="9e5ea-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="9e5ea-113">$schema</span><span class="sxs-lookup"><span data-stu-id="9e5ea-113">$schema</span></span>

<span data-ttu-id="9e5ea-114">*Необязательная, но рекомендуемая* &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="9e5ea-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="9e5ea-115">URL-адрес https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="9e5ea-116">Версия манифеста</span><span class="sxs-lookup"><span data-stu-id="9e5ea-116">manifestVersion</span></span>

<span data-ttu-id="9e5ea-117">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="9e5ea-117">**Required** &ndash; String</span></span>

<span data-ttu-id="9e5ea-118">Версия схемы манифеста, используемая манифестом.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="9e5ea-119">Он должен иметь слово "Девпревиев".</span><span class="sxs-lookup"><span data-stu-id="9e5ea-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="9e5ea-120">version</span><span class="sxs-lookup"><span data-stu-id="9e5ea-120">version</span></span>

<span data-ttu-id="9e5ea-121">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="9e5ea-121">**Required** &ndash; String</span></span>

<span data-ttu-id="9e5ea-122">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-122">The version of the specific app.</span></span> <span data-ttu-id="9e5ea-123">Если вы обновите какой-либо элемент в манифесте, необходимо также увеличить номер версии.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="9e5ea-124">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="9e5ea-125">Если это приложение было отправлено в хранилище, новый манифест необходимо будет повторно отправить и проверить повторно.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="9e5ea-126">После этого пользователи этого приложения автоматически получат новый обновленный манифест в течение нескольких часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="9e5ea-127">Если приложение запросило изменение разрешений, пользователям будет предложено выполнить обновление и повторное согласие на доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="9e5ea-128">Эта строка версии должна соответствовать стандарту [semver](http://semver.org/) (Major. Значительные. PATCH).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="9e5ea-129">id</span><span class="sxs-lookup"><span data-stu-id="9e5ea-129">id</span></span>

<span data-ttu-id="9e5ea-130">**Обязательный** &ndash; идентификатор приложения Microsoft</span><span class="sxs-lookup"><span data-stu-id="9e5ea-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="9e5ea-131">Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="9e5ea-132">Если вы зарегистрировали Bot с помощью Microsoft Bot Framework, или веб-приложение вашей вкладки уже входит в Microsoft, у вас уже должен быть идентификатор, и его следует ввести здесь.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="9e5ea-133">В противном случае необходимо создать новый идентификатор на портале регистрации приложений ([Мои приложения](https://apps.dev.microsoft.com)) Майкрософт, ввести его здесь, а затем повторно использовать его при [добавлении ленты](~/bots/how-to/create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="9e5ea-134">паккаженаме</span><span class="sxs-lookup"><span data-stu-id="9e5ea-134">packageName</span></span>

<span data-ttu-id="9e5ea-135">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="9e5ea-135">**Required** &ndash; String</span></span>

<span data-ttu-id="9e5ea-136">Уникальный идентификатор для этого приложения в обратной нотации домена; Пример: com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="9e5ea-137">developer</span><span class="sxs-lookup"><span data-stu-id="9e5ea-137">developer</span></span>

<span data-ttu-id="9e5ea-138">**Required**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-138">**Required**</span></span>

<span data-ttu-id="9e5ea-139">Указывает сведения о компании.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-139">Specifies information about your company.</span></span> <span data-ttu-id="9e5ea-140">Для приложений, отправляемых в AppSource (ранее — магазин Office), эти значения должны быть сопоставлены со сведениями в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="9e5ea-141">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-141">Name</span></span>| <span data-ttu-id="9e5ea-142">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-142">Maximum size</span></span> | <span data-ttu-id="9e5ea-143">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-143">Required</span></span> | <span data-ttu-id="9e5ea-144">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="9e5ea-145">32 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-145">32 characters</span></span>|<span data-ttu-id="9e5ea-146">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-146">✔</span></span>|<span data-ttu-id="9e5ea-147">Отображаемое имя разработчика.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="9e5ea-148">2048 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-148">2048 characters</span></span>|<span data-ttu-id="9e5ea-149">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-149">✔</span></span>|<span data-ttu-id="9e5ea-150">URL-адрес https://на веб-сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="9e5ea-151">Эта ссылка должна принять участие у пользователей в вашей компании или целевой странице для конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="9e5ea-152">2048 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-152">2048 characters</span></span>|<span data-ttu-id="9e5ea-153">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-153">✔</span></span>|<span data-ttu-id="9e5ea-154">URL-адрес https://для политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="9e5ea-155">2048 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-155">2048 characters</span></span>|<span data-ttu-id="9e5ea-156">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-156">✔</span></span>|<span data-ttu-id="9e5ea-157">URL-адрес https://для условий использования разработчиком.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="9e5ea-158">10 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-158">10 characters</span></span>|<span data-ttu-id="9e5ea-159">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-159">✔</span></span>|<span data-ttu-id="9e5ea-160">**Необязательное требование** Идентификатор сети партнера Майкрософт, определяющий партнерскую организацию, которая создает приложение.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="9e5ea-161">локализатионинфо</span><span class="sxs-lookup"><span data-stu-id="9e5ea-161">localizationInfo</span></span>

<span data-ttu-id="9e5ea-162">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-162">**Optional**</span></span>

<span data-ttu-id="9e5ea-163">Разрешает спецификацию языка по умолчанию, а также указателей на дополнительные языковые файлы.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="9e5ea-164">См.: [Локализация](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="9e5ea-165">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-165">Name</span></span>| <span data-ttu-id="9e5ea-166">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-166">Maximum size</span></span> | <span data-ttu-id="9e5ea-167">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-167">Required</span></span> | <span data-ttu-id="9e5ea-168">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="9e5ea-169">4 символа</span><span class="sxs-lookup"><span data-stu-id="9e5ea-169">4 characters</span></span>|<span data-ttu-id="9e5ea-170">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-170">✔</span></span>|<span data-ttu-id="9e5ea-171">Тег языка строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="9e5ea-172">Локализатионинфо. Аддитионаллангуажес</span><span class="sxs-lookup"><span data-stu-id="9e5ea-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="9e5ea-173">Массив объектов, задающий дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="9e5ea-174">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-174">Name</span></span>| <span data-ttu-id="9e5ea-175">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-175">Maximum size</span></span> | <span data-ttu-id="9e5ea-176">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-176">Required</span></span> | <span data-ttu-id="9e5ea-177">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="9e5ea-178">4 символа</span><span class="sxs-lookup"><span data-stu-id="9e5ea-178">4 characters</span></span>|<span data-ttu-id="9e5ea-179">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-179">✔</span></span>|<span data-ttu-id="9e5ea-180">Тег языка строк в указанном файле.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="9e5ea-181">4 символа</span><span class="sxs-lookup"><span data-stu-id="9e5ea-181">4 characters</span></span>|<span data-ttu-id="9e5ea-182">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-182">✔</span></span>|<span data-ttu-id="9e5ea-183">Относительный путь к файлу. JSON, содержащему переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="9e5ea-184">name</span><span class="sxs-lookup"><span data-stu-id="9e5ea-184">name</span></span>

<span data-ttu-id="9e5ea-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-185">**Required**</span></span>

<span data-ttu-id="9e5ea-186">Имя приложения, отображаемое для пользователей в интерфейсе Teams.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="9e5ea-187">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="9e5ea-188">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="9e5ea-189">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-189">Name</span></span>| <span data-ttu-id="9e5ea-190">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-190">Maximum size</span></span> | <span data-ttu-id="9e5ea-191">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-191">Required</span></span> | <span data-ttu-id="9e5ea-192">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="9e5ea-193">30 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-193">30 characters</span></span>|<span data-ttu-id="9e5ea-194">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-194">✔</span></span>|<span data-ttu-id="9e5ea-195">Краткое отображаемое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="9e5ea-196">100 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-196">100 characters</span></span>||<span data-ttu-id="9e5ea-197">Полное имя приложения, используемое, если имя полного приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="9e5ea-198">description</span><span class="sxs-lookup"><span data-stu-id="9e5ea-198">description</span></span>

<span data-ttu-id="9e5ea-199">**Required**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-199">**Required**</span></span>

<span data-ttu-id="9e5ea-200">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-200">Describes your app to users.</span></span> <span data-ttu-id="9e5ea-201">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="9e5ea-202">Убедитесь, что ваше описание точно описывает ваш интерфейс и предоставляет сведения, помогающие потенциальным клиентам определить, что делает ваш интерфейс.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="9e5ea-203">Кроме того, в полном описании следует отметить, если для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="9e5ea-204">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="9e5ea-205">Краткое описание не должно повторяться в длинном описании и не должно включать имя другого приложения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="9e5ea-206">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-206">Name</span></span>| <span data-ttu-id="9e5ea-207">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-207">Maximum size</span></span> | <span data-ttu-id="9e5ea-208">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-208">Required</span></span> | <span data-ttu-id="9e5ea-209">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="9e5ea-210">80 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-210">80 characters</span></span>|<span data-ttu-id="9e5ea-211">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-211">✔</span></span>|<span data-ttu-id="9e5ea-212">Краткое описание интерфейса приложения, используемое при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="9e5ea-213">4000 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-213">4000 characters</span></span>|<span data-ttu-id="9e5ea-214">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-214">✔</span></span>|<span data-ttu-id="9e5ea-215">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="9e5ea-216">icons</span><span class="sxs-lookup"><span data-stu-id="9e5ea-216">icons</span></span>

<span data-ttu-id="9e5ea-217">**Required**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-217">**Required**</span></span>

<span data-ttu-id="9e5ea-218">Значки, используемые в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-218">Icons used within the Teams app.</span></span> <span data-ttu-id="9e5ea-219">Файлы значков должны быть включены в состав пакета отправки.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="9e5ea-220">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-220">Name</span></span>| <span data-ttu-id="9e5ea-221">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-221">Maximum size</span></span> | <span data-ttu-id="9e5ea-222">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-222">Required</span></span> | <span data-ttu-id="9e5ea-223">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="9e5ea-224">2048 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-224">2048 characters</span></span>|<span data-ttu-id="9e5ea-225">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-225">✔</span></span>|<span data-ttu-id="9e5ea-226">Относительный путь к файлу с прозрачным значком изображения в формате 32x32 PNG.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="9e5ea-227">2048 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-227">2048 characters</span></span>|<span data-ttu-id="9e5ea-228">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-228">✔</span></span>|<span data-ttu-id="9e5ea-229">Относительный путь к файлу полного цветового значка PNG 192x192.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="9e5ea-230">акцентколор</span><span class="sxs-lookup"><span data-stu-id="9e5ea-230">accentColor</span></span>

<span data-ttu-id="9e5ea-231">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="9e5ea-231">**Required** &ndash; String</span></span>

<span data-ttu-id="9e5ea-232">Цвет, используемый в сочетании с фоном для значков структуры.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="9e5ea-233">Значение должно быть допустимым цветом HTML-кода, начинающимся с "#", `#4464ee`например.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="9e5ea-234">конфигураблетабс</span><span class="sxs-lookup"><span data-stu-id="9e5ea-234">configurableTabs</span></span>

<span data-ttu-id="9e5ea-235">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-235">**Optional**</span></span>

<span data-ttu-id="9e5ea-236">Используется, когда у вашего приложения есть вкладка "канал группы", требующая дополнительной настройки перед добавлением.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="9e5ea-237">Настраиваемые вкладки поддерживаются только в области Teams, и в настоящее время поддерживается только одна вкладка для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="9e5ea-238">Объект является массивом со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="9e5ea-239">Этот блок необходим только для решений, которые предоставляют настраиваемое решение для вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="9e5ea-240">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-240">Name</span></span>| <span data-ttu-id="9e5ea-241">Тип</span><span class="sxs-lookup"><span data-stu-id="9e5ea-241">Type</span></span>| <span data-ttu-id="9e5ea-242">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-242">Maximum size</span></span> | <span data-ttu-id="9e5ea-243">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-243">Required</span></span> | <span data-ttu-id="9e5ea-244">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="9e5ea-245">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-245">String</span></span>|<span data-ttu-id="9e5ea-246">2048 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-246">2048 characters</span></span>|<span data-ttu-id="9e5ea-247">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-247">✔</span></span>|<span data-ttu-id="9e5ea-248">URL-адрес https://, используемый при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="9e5ea-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="9e5ea-249">Boolean</span></span>|||<span data-ttu-id="9e5ea-250">Значение, указывающее, может ли пользователь обновлять экземпляр конфигурации вкладки после создания.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="9e5ea-251">Умолчани`true`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="9e5ea-252">Массив перечисления</span><span class="sxs-lookup"><span data-stu-id="9e5ea-252">Array of enum</span></span>|<span data-ttu-id="9e5ea-253">1 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-253">1</span></span>|<span data-ttu-id="9e5ea-254">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-254">✔</span></span>|<span data-ttu-id="9e5ea-255">В настоящее время настраиваемые вкладки поддерживают только области `team` и `groupchat` области.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="9e5ea-256">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-256">String</span></span>|<span data-ttu-id="9e5ea-257">2048</span><span class="sxs-lookup"><span data-stu-id="9e5ea-257">2048</span></span>||<span data-ttu-id="9e5ea-258">Относительный путь к изображению вкладки для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="9e5ea-259">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="9e5ea-260">Массив перечисления</span><span class="sxs-lookup"><span data-stu-id="9e5ea-260">Array of enum</span></span>|<span data-ttu-id="9e5ea-261">1 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-261">1</span></span>||<span data-ttu-id="9e5ea-262">Определяет, как будет предоставляться вкладка в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="9e5ea-263">`sharePointFullPage` Параметры`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="9e5ea-264">статиктабс</span><span class="sxs-lookup"><span data-stu-id="9e5ea-264">staticTabs</span></span>

<span data-ttu-id="9e5ea-265">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-265">**Optional**</span></span>

<span data-ttu-id="9e5ea-266">Определяет набор вкладок, которые по умолчанию можно закреплять, не добавляя пользователей вручную.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="9e5ea-267">Статические вкладки, `personal` объявляемые в области, всегда фиксируются в личном интерфейсе приложения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="9e5ea-268">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="9e5ea-269">Объект является массивом (не более 16 элементов) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="9e5ea-270">Этот блок необходим только для решений, предоставляющих статическое решение для вкладок.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="9e5ea-271">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-271">Name</span></span>| <span data-ttu-id="9e5ea-272">Тип</span><span class="sxs-lookup"><span data-stu-id="9e5ea-272">Type</span></span>| <span data-ttu-id="9e5ea-273">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-273">Maximum size</span></span> | <span data-ttu-id="9e5ea-274">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-274">Required</span></span> | <span data-ttu-id="9e5ea-275">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="9e5ea-276">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-276">String</span></span>|<span data-ttu-id="9e5ea-277">64 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-277">64 characters</span></span>|<span data-ttu-id="9e5ea-278">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-278">✔</span></span>|<span data-ttu-id="9e5ea-279">Уникальный идентификатор объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="9e5ea-280">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-280">String</span></span>|<span data-ttu-id="9e5ea-281">128 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-281">128 characters</span></span>|<span data-ttu-id="9e5ea-282">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-282">✔</span></span>|<span data-ttu-id="9e5ea-283">Отображаемое имя вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="9e5ea-284">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-284">String</span></span>|<span data-ttu-id="9e5ea-285">2048 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-285">2048 characters</span></span>|<span data-ttu-id="9e5ea-286">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-286">✔</span></span>|<span data-ttu-id="9e5ea-287">URL-адрес https://, указывающий на пользовательский интерфейс сущности, который будет отображаться в полотне Teams.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="9e5ea-288">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-288">String</span></span>|<span data-ttu-id="9e5ea-289">2048 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-289">2048 characters</span></span>||<span data-ttu-id="9e5ea-290">URL-адрес https://, указывающий, когда пользователь попытается просмотреть его в браузере.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="9e5ea-291">Массив перечисления</span><span class="sxs-lookup"><span data-stu-id="9e5ea-291">Array of enum</span></span>|<span data-ttu-id="9e5ea-292">1 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-292">1</span></span>|<span data-ttu-id="9e5ea-293">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-293">✔</span></span>|<span data-ttu-id="9e5ea-294">В настоящее время статические вкладки поддерживают `personal` только область, что означает, что ее можно подготовить только в рамках личного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="9e5ea-295">Боты</span><span class="sxs-lookup"><span data-stu-id="9e5ea-295">bots</span></span>

<span data-ttu-id="9e5ea-296">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-296">**Optional**</span></span>

<span data-ttu-id="9e5ea-297">Определяет одноэлементное решение, а также дополнительные сведения, такие как свойства команды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="9e5ea-298">Объект является массивом (в настоящее время для каждого приложения&mdash;допускается только один элемент "bot" для каждого приложения) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="9e5ea-299">Этот блок необходим только для решений, предоставляющих интерфейс Bot.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="9e5ea-300">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-300">Name</span></span>| <span data-ttu-id="9e5ea-301">Тип</span><span class="sxs-lookup"><span data-stu-id="9e5ea-301">Type</span></span>| <span data-ttu-id="9e5ea-302">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-302">Maximum size</span></span> | <span data-ttu-id="9e5ea-303">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-303">Required</span></span> | <span data-ttu-id="9e5ea-304">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="9e5ea-305">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-305">String</span></span>|<span data-ttu-id="9e5ea-306">64 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-306">64 characters</span></span>|<span data-ttu-id="9e5ea-307">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-307">✔</span></span>|<span data-ttu-id="9e5ea-308">Уникальный идентификатор приложения для ленты, зарегистрированный с помощью Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="9e5ea-309">Это может быть так же, как и общий [идентификатор приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="9e5ea-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="9e5ea-310">Boolean</span></span>|||<span data-ttu-id="9e5ea-311">Описывает, использует ли пользователь почтовые подсказка для добавления ленты к определенному каналу.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="9e5ea-312">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="9e5ea-313">Boolean</span><span class="sxs-lookup"><span data-stu-id="9e5ea-313">Boolean</span></span>|||<span data-ttu-id="9e5ea-314">Указывает, является ли Bot односторонним, только для уведомления, а не с сообщением Bot.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="9e5ea-315">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="9e5ea-316">Boolean</span><span class="sxs-lookup"><span data-stu-id="9e5ea-316">Boolean</span></span>|||<span data-ttu-id="9e5ea-317">Указывает, поддерживает ли Bot возможность загрузки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="9e5ea-318">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="9e5ea-319">Массив перечисления</span><span class="sxs-lookup"><span data-stu-id="9e5ea-319">Array of enum</span></span>|<span data-ttu-id="9e5ea-320">3 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-320">3</span></span>|<span data-ttu-id="9e5ea-321">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-321">✔</span></span>|<span data-ttu-id="9e5ea-322">Указывает `team`, является ли Bot интерфейсом пользователя в контексте канала в, в разделе "участие в группах" (`groupchat`) или взаимодействия с областью действия только для отдельного пользователя (`personal`).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="9e5ea-323">Эти параметры не являются монопольными.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="9e5ea-324">Боты. Коммандлистс</span><span class="sxs-lookup"><span data-stu-id="9e5ea-324">bots.commandLists</span></span>

<span data-ttu-id="9e5ea-325">Необязательный список команд, которые ваш робот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="9e5ea-326">Объект является массивом (не более 2 элементов) со всеми элементами типа `object`; необходимо определить отдельный список команд для каждой области, которую поддерживает Bot.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="9e5ea-327">Дополнительные сведения содержатся в [меню Bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="9e5ea-327">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="9e5ea-328">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-328">Name</span></span>| <span data-ttu-id="9e5ea-329">Тип</span><span class="sxs-lookup"><span data-stu-id="9e5ea-329">Type</span></span>| <span data-ttu-id="9e5ea-330">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-330">Maximum size</span></span> | <span data-ttu-id="9e5ea-331">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-331">Required</span></span> | <span data-ttu-id="9e5ea-332">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="9e5ea-333">массив перечисления</span><span class="sxs-lookup"><span data-stu-id="9e5ea-333">array of enum</span></span>|<span data-ttu-id="9e5ea-334">3 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-334">3</span></span>|<span data-ttu-id="9e5ea-335">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-335">✔</span></span>|<span data-ttu-id="9e5ea-336">Задает область действия, для которой список команд является допустимым.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="9e5ea-337">Параметры: `team`, `personal`, и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="9e5ea-338">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-338">array of objects</span></span>|<span data-ttu-id="9e5ea-339">10 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-339">10</span></span>|<span data-ttu-id="9e5ea-340">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-340">✔</span></span>|<span data-ttu-id="9e5ea-341">Массив команд, поддерживаемых в Bot:</span><span class="sxs-lookup"><span data-stu-id="9e5ea-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="9e5ea-342">`title`: имя команды Bot (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="9e5ea-342">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="9e5ea-343">`description`: простое описание или пример синтаксиса команды и его аргумента (строка, 128).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-343">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="9e5ea-344">аудиовыход</span><span class="sxs-lookup"><span data-stu-id="9e5ea-344">connectors</span></span>

<span data-ttu-id="9e5ea-345">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-345">**Optional**</span></span>

<span data-ttu-id="9e5ea-346">`connectors` Блок определяет соединитель Office 365 для приложения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="9e5ea-347">Объект является массивом (не более 1 элемента) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="9e5ea-348">Этот блок необходим только для решений, предоставляющих соединитель.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="9e5ea-349">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-349">Name</span></span>| <span data-ttu-id="9e5ea-350">Тип</span><span class="sxs-lookup"><span data-stu-id="9e5ea-350">Type</span></span>| <span data-ttu-id="9e5ea-351">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-351">Maximum size</span></span> | <span data-ttu-id="9e5ea-352">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-352">Required</span></span> | <span data-ttu-id="9e5ea-353">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="9e5ea-354">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-354">String</span></span>|<span data-ttu-id="9e5ea-355">2048 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-355">2048 characters</span></span>|<span data-ttu-id="9e5ea-356">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-356">✔</span></span>|<span data-ttu-id="9e5ea-357">URL-адрес https://, используемый при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="9e5ea-358">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-358">String</span></span>|<span data-ttu-id="9e5ea-359">64 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-359">64 characters</span></span>|<span data-ttu-id="9e5ea-360">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-360">✔</span></span>|<span data-ttu-id="9e5ea-361">Уникальный идентификатор соединителя, который соответствует ИДЕНТИФИКАТОРу в [панели мониторинга разработчика соединителей](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="9e5ea-362">Массив перечисления</span><span class="sxs-lookup"><span data-stu-id="9e5ea-362">Array of enum</span></span>|<span data-ttu-id="9e5ea-363">1 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-363">1</span></span>|<span data-ttu-id="9e5ea-364">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-364">✔</span></span>|<span data-ttu-id="9e5ea-365">Указывает `team`, будет ли соединитель работать в контексте канала в или в интерфейсе для отдельного пользователя (`personal`).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="9e5ea-366">В настоящее время поддерживается `team` только область действия.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="9e5ea-367">компосикстенсионс</span><span class="sxs-lookup"><span data-stu-id="9e5ea-367">composeExtensions</span></span>

<span data-ttu-id="9e5ea-368">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-368">**Optional**</span></span>

<span data-ttu-id="9e5ea-369">Определяет расширение системы обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="9e5ea-370">Имя компонента изменилось с "расширение составления" на "расширение обмена сообщениями" в ноябре 2017, но имя манифеста остается без изменений, поэтому все существующие расширения продолжают работать.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="9e5ea-371">Объект является массивом (не более 1 элемента) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="9e5ea-372">Этот блок необходим только для решений, предоставляющих расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="9e5ea-373">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-373">Name</span></span>| <span data-ttu-id="9e5ea-374">Тип</span><span class="sxs-lookup"><span data-stu-id="9e5ea-374">Type</span></span> | <span data-ttu-id="9e5ea-375">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-375">Maximum Size</span></span> | <span data-ttu-id="9e5ea-376">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-376">Required</span></span> | <span data-ttu-id="9e5ea-377">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="9e5ea-378">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-378">String</span></span>|<span data-ttu-id="9e5ea-379">64</span><span class="sxs-lookup"><span data-stu-id="9e5ea-379">64</span></span>|<span data-ttu-id="9e5ea-380">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-380">✔</span></span>|<span data-ttu-id="9e5ea-381">Уникальный идентификатор приложения для ленты, который выполняет резервное копирование расширения обмена сообщениями, как зарегистрировано в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="9e5ea-382">Это может быть так же, как и общий [идентификатор приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="9e5ea-383">Boolean</span><span class="sxs-lookup"><span data-stu-id="9e5ea-383">Boolean</span></span>|||<span data-ttu-id="9e5ea-384">Значение, указывающее, может ли пользователь изменять конфигурацию расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="9e5ea-385">Значение по умолчанию: `false`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="9e5ea-386">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-386">Array of object</span></span>|<span data-ttu-id="9e5ea-387">10 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-387">10</span></span>|<span data-ttu-id="9e5ea-388">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-388">✔</span></span>|<span data-ttu-id="9e5ea-389">Массив команд, поддерживающих расширение системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9e5ea-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="9e5ea-390">Компосикстенсионс. Commands</span><span class="sxs-lookup"><span data-stu-id="9e5ea-390">composeExtensions.commands</span></span>

<span data-ttu-id="9e5ea-391">Ваш модуль обмена сообщениями должен объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="9e5ea-392">Каждая команда отображается в Microsoft Teams в качестве потенциального взаимодействия от точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="9e5ea-393">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="9e5ea-394">Каждый элемент команды представляет собой объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="9e5ea-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="9e5ea-395">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-395">Name</span></span>| <span data-ttu-id="9e5ea-396">Тип</span><span class="sxs-lookup"><span data-stu-id="9e5ea-396">Type</span></span>| <span data-ttu-id="9e5ea-397">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-397">Maximum size</span></span> | <span data-ttu-id="9e5ea-398">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-398">Required</span></span> | <span data-ttu-id="9e5ea-399">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="9e5ea-400">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-400">String</span></span>|<span data-ttu-id="9e5ea-401">64 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-401">64 characters</span></span>|<span data-ttu-id="9e5ea-402">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-402">✔</span></span>|<span data-ttu-id="9e5ea-403">Идентификатор команды</span><span class="sxs-lookup"><span data-stu-id="9e5ea-403">The ID for the command</span></span>|
|`type`|<span data-ttu-id="9e5ea-404">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-404">String</span></span>|<span data-ttu-id="9e5ea-405">64 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-405">64 characters</span></span>||<span data-ttu-id="9e5ea-406">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-406">Type of the command.</span></span> <span data-ttu-id="9e5ea-407">Один из `query` или `action`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-407">One of `query` or `action`.</span></span> <span data-ttu-id="9e5ea-408">Умолчани`query`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="9e5ea-409">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-409">String</span></span>|<span data-ttu-id="9e5ea-410">32 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-410">32 characters</span></span>|<span data-ttu-id="9e5ea-411">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-411">✔</span></span>|<span data-ttu-id="9e5ea-412">Понятное имя команды</span><span class="sxs-lookup"><span data-stu-id="9e5ea-412">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="9e5ea-413">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-413">String</span></span>|<span data-ttu-id="9e5ea-414">128 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-414">128 characters</span></span>||<span data-ttu-id="9e5ea-415">Описание, которое отображается пользователям для указания цели этой команды</span><span class="sxs-lookup"><span data-stu-id="9e5ea-415">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="9e5ea-416">Boolean</span><span class="sxs-lookup"><span data-stu-id="9e5ea-416">Boolean</span></span>|||<span data-ttu-id="9e5ea-417">Логическое значение, которое указывает, следует ли выполнять команду изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="9e5ea-418">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="9e5ea-419">Массив строк</span><span class="sxs-lookup"><span data-stu-id="9e5ea-419">Array of Strings</span></span>|<span data-ttu-id="9e5ea-420">3 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-420">3</span></span>||<span data-ttu-id="9e5ea-421">Определяет, откуда можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="9e5ea-422">Любое сочетание `compose`, `commandBox`,. `message`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="9e5ea-423">Значение по умолчанию:`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="9e5ea-424">Boolean</span><span class="sxs-lookup"><span data-stu-id="9e5ea-424">Boolean</span></span>|||<span data-ttu-id="9e5ea-425">Логическое значение, указывающее, должен ли он динамически получать модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-425">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="9e5ea-426">Объект</span><span class="sxs-lookup"><span data-stu-id="9e5ea-426">Object</span></span>|||<span data-ttu-id="9e5ea-427">Указание модуля задач для предварительной загрузки при использовании команды расширения системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9e5ea-427">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="9e5ea-428">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-428">String</span></span>|<span data-ttu-id="9e5ea-429">64</span><span class="sxs-lookup"><span data-stu-id="9e5ea-429">64</span></span>||<span data-ttu-id="9e5ea-430">Заголовок начального диалогового окна</span><span class="sxs-lookup"><span data-stu-id="9e5ea-430">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="9e5ea-431">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-431">String</span></span>|||<span data-ttu-id="9e5ea-432">Ширина диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый"</span><span class="sxs-lookup"><span data-stu-id="9e5ea-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="9e5ea-433">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-433">String</span></span>|||<span data-ttu-id="9e5ea-434">Высота диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый"</span><span class="sxs-lookup"><span data-stu-id="9e5ea-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="9e5ea-435">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-435">String</span></span>|||<span data-ttu-id="9e5ea-436">Исходный URL-адрес вебвиев</span><span class="sxs-lookup"><span data-stu-id="9e5ea-436">Initial webview URL</span></span>|
|`messageHandlers`|<span data-ttu-id="9e5ea-437">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-437">Array of Objects</span></span>|<span data-ttu-id="9e5ea-438">5 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-438">5</span></span>||<span data-ttu-id="9e5ea-439">Список обработчиков, позволяющих вызывать приложения при выполнении определенных условий.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="9e5ea-440">Домены также должны быть перечислены в`validDomains`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-440">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="9e5ea-441">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-441">String</span></span>|||<span data-ttu-id="9e5ea-442">Тип обработчика сообщений.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-442">The type of message handler.</span></span> <span data-ttu-id="9e5ea-443">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="9e5ea-444">Массив строк</span><span class="sxs-lookup"><span data-stu-id="9e5ea-444">Array of Strings</span></span>|||<span data-ttu-id="9e5ea-445">Массив доменов, для которых может регистрироваться обработчик сообщений ссылки.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="9e5ea-446">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-446">Array of object</span></span>|<span data-ttu-id="9e5ea-447">5 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-447">5</span></span>|<span data-ttu-id="9e5ea-448">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-448">✔</span></span>|<span data-ttu-id="9e5ea-449">Список параметров, которые выполняет команда.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-449">The list of parameters the command takes.</span></span> <span data-ttu-id="9e5ea-450">Минимум: 1; максимум: 5</span><span class="sxs-lookup"><span data-stu-id="9e5ea-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="9e5ea-451">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-451">String</span></span>|<span data-ttu-id="9e5ea-452">64 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-452">64 characters</span></span>|<span data-ttu-id="9e5ea-453">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-453">✔</span></span>|<span data-ttu-id="9e5ea-454">Имя параметра в том виде, в котором оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="9e5ea-455">Он включен в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="9e5ea-456">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-456">String</span></span>|<span data-ttu-id="9e5ea-457">32 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-457">32 characters</span></span>|<span data-ttu-id="9e5ea-458">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-458">✔</span></span>|<span data-ttu-id="9e5ea-459">Удобное для пользователя название параметра.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="9e5ea-460">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-460">String</span></span>|<span data-ttu-id="9e5ea-461">128 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-461">128 characters</span></span>||<span data-ttu-id="9e5ea-462">Понятная пользователю строка, описывающая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="9e5ea-463">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-463">String</span></span>|<span data-ttu-id="9e5ea-464">128 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-464">128 characters</span></span>||<span data-ttu-id="9e5ea-465">Определяет тип элемента управления, отображаемого в модуле задачи для `fetchTask: true`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="9e5ea-466">Один из `text`, `textarea`, `number`, `date` `time`,, `toggle`,`choiceset`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="9e5ea-467">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-467">Array of Objects</span></span>|<span data-ttu-id="9e5ea-468">10 </span><span class="sxs-lookup"><span data-stu-id="9e5ea-468">10</span></span>||<span data-ttu-id="9e5ea-469">Варианты выбора для `choiceset`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="9e5ea-470">Используйте только в `parameter.inputType` том случае, если`choiceset`</span><span class="sxs-lookup"><span data-stu-id="9e5ea-470">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="9e5ea-471">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-471">String</span></span>|<span data-ttu-id="9e5ea-472">128</span><span class="sxs-lookup"><span data-stu-id="9e5ea-472">128</span></span>||<span data-ttu-id="9e5ea-473">Название варианта</span><span class="sxs-lookup"><span data-stu-id="9e5ea-473">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="9e5ea-474">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-474">String</span></span>|<span data-ttu-id="9e5ea-475">512</span><span class="sxs-lookup"><span data-stu-id="9e5ea-475">512</span></span>||<span data-ttu-id="9e5ea-476">Выбор значения</span><span class="sxs-lookup"><span data-stu-id="9e5ea-476">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="9e5ea-477">permissions</span><span class="sxs-lookup"><span data-stu-id="9e5ea-477">permissions</span></span>

<span data-ttu-id="9e5ea-478">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-478">**Optional**</span></span>

<span data-ttu-id="9e5ea-479">Массив `string` , определяющий, какие разрешения запрашиваются приложением, что позволяет конечным пользователям знать, как будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="9e5ea-480">Следующие параметры неисключительны:</span><span class="sxs-lookup"><span data-stu-id="9e5ea-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="9e5ea-481">`identity`&emsp; Требуются сведения об удостоверении пользователя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-481">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="9e5ea-482">`messageTeamMembers`&emsp; Требуется разрешение на отправку прямых сообщений участникам группы</span><span class="sxs-lookup"><span data-stu-id="9e5ea-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="9e5ea-483">Изменение этих разрешений при обновлении приложения приводит к тому, что пользователи будут повторять процесс разрешения при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="9e5ea-484">девицепермиссионс</span><span class="sxs-lookup"><span data-stu-id="9e5ea-484">devicePermissions</span></span>

<span data-ttu-id="9e5ea-485">**Необязательное требование** Массив строк</span><span class="sxs-lookup"><span data-stu-id="9e5ea-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="9e5ea-486">Указывает собственные функции на устройстве пользователя, к которым приложение может запрашивать доступ.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="9e5ea-487">Возможные варианты:</span><span class="sxs-lookup"><span data-stu-id="9e5ea-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="9e5ea-488">валиддомаинс</span><span class="sxs-lookup"><span data-stu-id="9e5ea-488">validDomains</span></span>

<span data-ttu-id="9e5ea-489">**Необязательно**, за исключением **обязательного** места, где отмечено</span><span class="sxs-lookup"><span data-stu-id="9e5ea-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="9e5ea-490">Список допустимых доменов, из которых приложение ожидает загрузки какого бы то ни было содержимого.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="9e5ea-491">Примеры доменов могут включать подстановочные знаки `*.example.com`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="9e5ea-492">Это соответствует только одному сегменту домена; Если вам нужно использовать `a.b.example.com` `*.*.example.com`этот параметр.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="9e5ea-493">Если конфигурация вкладки или контентный пользовательский интерфейс должны перейти к любому другому домену, Кроме того, что используется для настройки вкладок, этот домен необходимо указать здесь.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="9e5ea-494">Тем не менее, **не** нужно включать домены поставщиков удостоверений, которые требуется поддерживать в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="9e5ea-495">Например, для проверки подлинности с помощью идентификатора Google необходимо перенаправить на accounts.google.com, но не следует включать accounts.google.com в `validDomains[]`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e5ea-496">Не добавляйте домены за предельный элемент управления (напрямую или с помощью подстановочных знаков).</span><span class="sxs-lookup"><span data-stu-id="9e5ea-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="9e5ea-497">Например, `yourapp.onmicrosoft.com` является допустимым, но `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="9e5ea-498">Объект является массивом со всеми элементами типа `string`.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="9e5ea-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="9e5ea-499">webApplicationInfo</span></span>

<span data-ttu-id="9e5ea-500">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="9e5ea-500">**Optional**</span></span>

<span data-ttu-id="9e5ea-501">Указание идентификатора приложения и графического объекта AAD для упрощения входа пользователей в приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="9e5ea-502">Имя</span><span class="sxs-lookup"><span data-stu-id="9e5ea-502">Name</span></span>| <span data-ttu-id="9e5ea-503">Тип</span><span class="sxs-lookup"><span data-stu-id="9e5ea-503">Type</span></span>| <span data-ttu-id="9e5ea-504">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="9e5ea-504">Maximum size</span></span> | <span data-ttu-id="9e5ea-505">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9e5ea-505">Required</span></span> | <span data-ttu-id="9e5ea-506">Описание</span><span class="sxs-lookup"><span data-stu-id="9e5ea-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="9e5ea-507">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-507">String</span></span>|<span data-ttu-id="9e5ea-508">36 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-508">36 characters</span></span>|<span data-ttu-id="9e5ea-509">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-509">✔</span></span>|<span data-ttu-id="9e5ea-510">Идентификатор приложения AAD приложения.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-510">AAD application id of the app.</span></span> <span data-ttu-id="9e5ea-511">Этот идентификатор должен быть идентификатором GUID.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="9e5ea-512">String</span><span class="sxs-lookup"><span data-stu-id="9e5ea-512">String</span></span>|<span data-ttu-id="9e5ea-513">2048 символов</span><span class="sxs-lookup"><span data-stu-id="9e5ea-513">2048 characters</span></span>|<span data-ttu-id="9e5ea-514">✔</span><span class="sxs-lookup"><span data-stu-id="9e5ea-514">✔</span></span>|<span data-ttu-id="9e5ea-515">URL-адрес ресурса приложения для получения маркера проверки подлинности для единого входа.</span><span class="sxs-lookup"><span data-stu-id="9e5ea-515">Resource url of app for acquiring auth token for SSO.</span></span>|