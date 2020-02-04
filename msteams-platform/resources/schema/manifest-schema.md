---
title: Справочник по схеме манифеста
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams.
keywords: Схема манифеста Teams
ms.openlocfilehash: d4a2864c18a5066673bafab42a46733a0ab5f116
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675443"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="870d4-104">Ссылка: схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="870d4-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="870d4-105">Манифест Microsoft Teams описывает, как приложение интегрируется в продукт Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="870d4-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="870d4-106">Манифест должен соответствовать схеме, размещенной в [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span><span class="sxs-lookup"><span data-stu-id="870d4-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="870d4-107">Также поддерживаются предыдущие версии 1.0-1.4 (в URL-адресе используется "v1. x").</span><span class="sxs-lookup"><span data-stu-id="870d4-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="870d4-108">В приведенном ниже примере схемы показаны все варианты расширения.</span><span class="sxs-lookup"><span data-stu-id="870d4-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="870d4-109">Пример полного манифеста</span><span class="sxs-lookup"><span data-stu-id="870d4-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
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
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
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
        }
      ],
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
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ]
}
```

<span data-ttu-id="870d4-110">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="870d4-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="870d4-111">$schema</span><span class="sxs-lookup"><span data-stu-id="870d4-111">$schema</span></span>

<span data-ttu-id="870d4-112">*Необязательная, но рекомендуемая* &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="870d4-112">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="870d4-113">URL-адрес https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="870d4-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="870d4-114">Версия манифеста</span><span class="sxs-lookup"><span data-stu-id="870d4-114">manifestVersion</span></span>

<span data-ttu-id="870d4-115">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="870d4-115">**Required** &ndash; String</span></span>

<span data-ttu-id="870d4-116">Версия схемы манифеста, используемая манифестом.</span><span class="sxs-lookup"><span data-stu-id="870d4-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="870d4-117">Он должен иметь значения "1,5".</span><span class="sxs-lookup"><span data-stu-id="870d4-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="870d4-118">version</span><span class="sxs-lookup"><span data-stu-id="870d4-118">version</span></span>

<span data-ttu-id="870d4-119">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="870d4-119">**Required** &ndash; String</span></span>

<span data-ttu-id="870d4-120">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-120">The version of the specific app.</span></span> <span data-ttu-id="870d4-121">Если вы обновите какой-либо элемент в манифесте, необходимо также увеличить номер версии.</span><span class="sxs-lookup"><span data-stu-id="870d4-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="870d4-122">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="870d4-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="870d4-123">Если это приложение было отправлено в хранилище, новый манифест необходимо будет повторно отправить и проверить повторно.</span><span class="sxs-lookup"><span data-stu-id="870d4-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="870d4-124">После этого пользователи этого приложения автоматически получат новый обновленный манифест в течение нескольких часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="870d4-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="870d4-125">Если приложение запросило изменение разрешений, пользователям будет предложено выполнить обновление и повторное согласие на доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="870d4-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="870d4-126">Эта строка версии должна соответствовать стандарту [semver](http://semver.org/) (Major. Значительные. PATCH).</span><span class="sxs-lookup"><span data-stu-id="870d4-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="870d4-127">id</span><span class="sxs-lookup"><span data-stu-id="870d4-127">id</span></span>

<span data-ttu-id="870d4-128">**Обязательный** &ndash; идентификатор приложения Microsoft</span><span class="sxs-lookup"><span data-stu-id="870d4-128">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="870d4-129">Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="870d4-130">Если вы зарегистрировали Bot с помощью Microsoft Bot Framework, или веб-приложение вашей вкладки уже входит в Microsoft, у вас уже должен быть идентификатор, и его следует ввести здесь.</span><span class="sxs-lookup"><span data-stu-id="870d4-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="870d4-131">В противном случае необходимо создать новый идентификатор на портале регистрации приложений ([Мои приложения](https://apps.dev.microsoft.com)) Майкрософт, ввести его здесь, а затем повторно использовать его при добавлении ленты. Note: Если вы отправляете обновление существующему приложению в AppSource, идентификатор в манифесте не должен изменяться.</span><span class="sxs-lookup"><span data-stu-id="870d4-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="packagename"></a><span data-ttu-id="870d4-132">паккаженаме</span><span class="sxs-lookup"><span data-stu-id="870d4-132">packageName</span></span>

<span data-ttu-id="870d4-133">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="870d4-133">**Required** &ndash; String</span></span>

<span data-ttu-id="870d4-134">Уникальный идентификатор для этого приложения в обратной нотации домена; Пример: com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="870d4-134">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="870d4-135">developer</span><span class="sxs-lookup"><span data-stu-id="870d4-135">developer</span></span>

<span data-ttu-id="870d4-136">**Required**</span><span class="sxs-lookup"><span data-stu-id="870d4-136">**Required**</span></span>

<span data-ttu-id="870d4-137">Указывает сведения о компании.</span><span class="sxs-lookup"><span data-stu-id="870d4-137">Specifies information about your company.</span></span> <span data-ttu-id="870d4-138">Для приложений, отправляемых в AppSource (ранее — магазин Office), эти значения должны быть сопоставлены со сведениями в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="870d4-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="870d4-139">Ознакомьтесь с нашими [рекомендациями по публикации](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="870d4-139">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="870d4-140">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-140">Name</span></span>| <span data-ttu-id="870d4-141">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-141">Maximum size</span></span> | <span data-ttu-id="870d4-142">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-142">Required</span></span> | <span data-ttu-id="870d4-143">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="870d4-144">32 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-144">32 characters</span></span>|<span data-ttu-id="870d4-145">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-145">✔</span></span>|<span data-ttu-id="870d4-146">Отображаемое имя разработчика.</span><span class="sxs-lookup"><span data-stu-id="870d4-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="870d4-147">2048 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-147">2048 characters</span></span>|<span data-ttu-id="870d4-148">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-148">✔</span></span>|<span data-ttu-id="870d4-149">URL-адрес https://на веб-сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="870d4-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="870d4-150">Эта ссылка должна принять участие у пользователей в вашей компании или целевой странице для конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="870d4-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="870d4-151">2048 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-151">2048 characters</span></span>|<span data-ttu-id="870d4-152">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-152">✔</span></span>|<span data-ttu-id="870d4-153">URL-адрес https://для политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="870d4-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="870d4-154">2048 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-154">2048 characters</span></span>|<span data-ttu-id="870d4-155">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-155">✔</span></span>|<span data-ttu-id="870d4-156">URL-адрес https://для условий использования разработчиком.</span><span class="sxs-lookup"><span data-stu-id="870d4-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="870d4-157">10 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-157">10 characters</span></span>| |<span data-ttu-id="870d4-158">**Необязательное требование** Идентификатор сети партнера Майкрософт, определяющий партнерскую организацию, которая создает приложение.</span><span class="sxs-lookup"><span data-stu-id="870d4-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="870d4-159">локализатионинфо</span><span class="sxs-lookup"><span data-stu-id="870d4-159">localizationInfo</span></span>

<span data-ttu-id="870d4-160">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="870d4-160">**Optional**</span></span>

<span data-ttu-id="870d4-161">Разрешает спецификацию языка по умолчанию, а также указателей на дополнительные языковые файлы.</span><span class="sxs-lookup"><span data-stu-id="870d4-161">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="870d4-162">См.: [Локализация](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="870d4-162">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="870d4-163">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-163">Name</span></span>| <span data-ttu-id="870d4-164">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-164">Maximum size</span></span> | <span data-ttu-id="870d4-165">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-165">Required</span></span> | <span data-ttu-id="870d4-166">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-166">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="870d4-167">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-167">✔</span></span>|<span data-ttu-id="870d4-168">Тег языка строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="870d4-168">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="870d4-169">Локализатионинфо. Аддитионаллангуажес</span><span class="sxs-lookup"><span data-stu-id="870d4-169">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="870d4-170">Массив объектов, задающий дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="870d4-170">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="870d4-171">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-171">Name</span></span>| <span data-ttu-id="870d4-172">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-172">Maximum size</span></span> | <span data-ttu-id="870d4-173">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-173">Required</span></span> | <span data-ttu-id="870d4-174">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-174">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="870d4-175">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-175">✔</span></span>|<span data-ttu-id="870d4-176">Тег языка строк в указанном файле.</span><span class="sxs-lookup"><span data-stu-id="870d4-176">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="870d4-177">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-177">✔</span></span>|<span data-ttu-id="870d4-178">Относительный путь к файлу. JSON, содержащему переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="870d4-178">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="870d4-179">name</span><span class="sxs-lookup"><span data-stu-id="870d4-179">name</span></span>

<span data-ttu-id="870d4-180">**Required**</span><span class="sxs-lookup"><span data-stu-id="870d4-180">**Required**</span></span>

<span data-ttu-id="870d4-181">Имя приложения, отображаемое для пользователей в интерфейсе Teams.</span><span class="sxs-lookup"><span data-stu-id="870d4-181">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="870d4-182">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="870d4-182">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="870d4-183">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="870d4-183">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="870d4-184">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-184">Name</span></span>| <span data-ttu-id="870d4-185">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-185">Maximum size</span></span> | <span data-ttu-id="870d4-186">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-186">Required</span></span> | <span data-ttu-id="870d4-187">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-187">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="870d4-188">30 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-188">30 characters</span></span>|<span data-ttu-id="870d4-189">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-189">✔</span></span>|<span data-ttu-id="870d4-190">Краткое отображаемое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-190">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="870d4-191">100 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-191">100 characters</span></span>||<span data-ttu-id="870d4-192">Полное имя приложения, используемое, если имя полного приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="870d4-192">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="870d4-193">description</span><span class="sxs-lookup"><span data-stu-id="870d4-193">description</span></span>

<span data-ttu-id="870d4-194">**Required**</span><span class="sxs-lookup"><span data-stu-id="870d4-194">**Required**</span></span>

<span data-ttu-id="870d4-195">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="870d4-195">Describes your app to users.</span></span> <span data-ttu-id="870d4-196">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="870d4-196">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="870d4-197">Убедитесь, что ваше описание точно описывает ваш интерфейс и предоставляет сведения, помогающие потенциальным клиентам определить, что делает ваш интерфейс.</span><span class="sxs-lookup"><span data-stu-id="870d4-197">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="870d4-198">Кроме того, в полном описании следует отметить, если для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="870d4-198">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="870d4-199">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="870d4-199">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="870d4-200">Краткое описание не должно повторяться в длинном описании и не должно включать имя другого приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-200">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="870d4-201">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-201">Name</span></span>| <span data-ttu-id="870d4-202">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-202">Maximum size</span></span> | <span data-ttu-id="870d4-203">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-203">Required</span></span> | <span data-ttu-id="870d4-204">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-204">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="870d4-205">80 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-205">80 characters</span></span>|<span data-ttu-id="870d4-206">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-206">✔</span></span>|<span data-ttu-id="870d4-207">Краткое описание интерфейса приложения, используемое при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="870d4-207">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="870d4-208">4000 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-208">4000 characters</span></span>|<span data-ttu-id="870d4-209">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-209">✔</span></span>|<span data-ttu-id="870d4-210">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-210">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="870d4-211">icons</span><span class="sxs-lookup"><span data-stu-id="870d4-211">icons</span></span>

<span data-ttu-id="870d4-212">**Required**</span><span class="sxs-lookup"><span data-stu-id="870d4-212">**Required**</span></span>

<span data-ttu-id="870d4-213">Значки, используемые в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="870d4-213">Icons used within the Teams app.</span></span> <span data-ttu-id="870d4-214">Файлы значков должны быть включены в состав пакета отправки.</span><span class="sxs-lookup"><span data-stu-id="870d4-214">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="870d4-215">Дополнительные сведения можно найти в разделе [значки](~/concepts/build-and-test/apps-package.md#icons) .</span><span class="sxs-lookup"><span data-stu-id="870d4-215">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="870d4-216">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-216">Name</span></span>| <span data-ttu-id="870d4-217">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-217">Maximum size</span></span> | <span data-ttu-id="870d4-218">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-218">Required</span></span> | <span data-ttu-id="870d4-219">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-219">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="870d4-220">2048 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-220">2048 characters</span></span>|<span data-ttu-id="870d4-221">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-221">✔</span></span>|<span data-ttu-id="870d4-222">Относительный путь к файлу с прозрачным значком изображения в формате 32x32 PNG.</span><span class="sxs-lookup"><span data-stu-id="870d4-222">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="870d4-223">2048 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-223">2048 characters</span></span>|<span data-ttu-id="870d4-224">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-224">✔</span></span>|<span data-ttu-id="870d4-225">Относительный путь к файлу полного цветового значка PNG 192x192.</span><span class="sxs-lookup"><span data-stu-id="870d4-225">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="870d4-226">акцентколор</span><span class="sxs-lookup"><span data-stu-id="870d4-226">accentColor</span></span>

<span data-ttu-id="870d4-227">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="870d4-227">**Required** &ndash; String</span></span>

<span data-ttu-id="870d4-228">Цвет, используемый в сочетании с фоном для значков структуры.</span><span class="sxs-lookup"><span data-stu-id="870d4-228">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="870d4-229">Значение должно быть допустимым цветом HTML-кода, начинающимся с "#", `#4464ee`например.</span><span class="sxs-lookup"><span data-stu-id="870d4-229">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="870d4-230">конфигураблетабс</span><span class="sxs-lookup"><span data-stu-id="870d4-230">configurableTabs</span></span>

<span data-ttu-id="870d4-231">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="870d4-231">**Optional**</span></span>

<span data-ttu-id="870d4-232">Используется, когда у вашего приложения есть вкладка "канал группы", требующая дополнительной настройки перед добавлением.</span><span class="sxs-lookup"><span data-stu-id="870d4-232">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="870d4-233">Настраиваемые вкладки поддерживаются только в области Teams, и в настоящее время поддерживается только одна вкладка для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-233">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="870d4-234">Объект является массивом со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="870d4-234">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="870d4-235">Этот блок необходим только для решений, которые предоставляют настраиваемое решение для вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="870d4-235">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="870d4-236">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-236">Name</span></span>| <span data-ttu-id="870d4-237">Тип</span><span class="sxs-lookup"><span data-stu-id="870d4-237">Type</span></span>| <span data-ttu-id="870d4-238">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-238">Maximum size</span></span> | <span data-ttu-id="870d4-239">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-239">Required</span></span> | <span data-ttu-id="870d4-240">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-240">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="870d4-241">String</span><span class="sxs-lookup"><span data-stu-id="870d4-241">String</span></span>|<span data-ttu-id="870d4-242">2048 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-242">2048 characters</span></span>|<span data-ttu-id="870d4-243">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-243">✔</span></span>|<span data-ttu-id="870d4-244">URL-адрес https://, используемый при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="870d4-244">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="870d4-245">Boolean</span><span class="sxs-lookup"><span data-stu-id="870d4-245">Boolean</span></span>|||<span data-ttu-id="870d4-246">Значение, указывающее, может ли пользователь обновлять экземпляр конфигурации вкладки после создания.</span><span class="sxs-lookup"><span data-stu-id="870d4-246">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="870d4-247">Умолчани`true`</span><span class="sxs-lookup"><span data-stu-id="870d4-247">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="870d4-248">Массив перечисления</span><span class="sxs-lookup"><span data-stu-id="870d4-248">Array of enum</span></span>|<span data-ttu-id="870d4-249">1 </span><span class="sxs-lookup"><span data-stu-id="870d4-249">1</span></span>|<span data-ttu-id="870d4-250">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-250">✔</span></span>|<span data-ttu-id="870d4-251">В настоящее время настраиваемые вкладки поддерживают только области `team` и `groupchat` области.</span><span class="sxs-lookup"><span data-stu-id="870d4-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="870d4-252">String</span><span class="sxs-lookup"><span data-stu-id="870d4-252">String</span></span>|<span data-ttu-id="870d4-253">2048</span><span class="sxs-lookup"><span data-stu-id="870d4-253">2048</span></span>||<span data-ttu-id="870d4-254">Относительный путь к изображению вкладки для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="870d4-254">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="870d4-255">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="870d4-255">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="870d4-256">Массив перечисления</span><span class="sxs-lookup"><span data-stu-id="870d4-256">Array of enum</span></span>|<span data-ttu-id="870d4-257">1 </span><span class="sxs-lookup"><span data-stu-id="870d4-257">1</span></span>||<span data-ttu-id="870d4-258">Определяет, как будет предоставляться вкладка в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="870d4-258">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="870d4-259">`sharePointFullPage` Параметры`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="870d4-259">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="870d4-260">статиктабс</span><span class="sxs-lookup"><span data-stu-id="870d4-260">staticTabs</span></span>

<span data-ttu-id="870d4-261">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="870d4-261">**Optional**</span></span>

<span data-ttu-id="870d4-262">Определяет набор вкладок, которые по умолчанию можно закреплять, не добавляя пользователей вручную.</span><span class="sxs-lookup"><span data-stu-id="870d4-262">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="870d4-263">Статические вкладки, `personal` объявляемые в области, всегда фиксируются в личном интерфейсе приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-263">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="870d4-264">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="870d4-264">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="870d4-265">Объект является массивом (не более 16 элементов) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="870d4-265">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="870d4-266">Этот блок необходим только для решений, предоставляющих статическое решение для вкладок.</span><span class="sxs-lookup"><span data-stu-id="870d4-266">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="870d4-267">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-267">Name</span></span>| <span data-ttu-id="870d4-268">Тип</span><span class="sxs-lookup"><span data-stu-id="870d4-268">Type</span></span>| <span data-ttu-id="870d4-269">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-269">Maximum size</span></span> | <span data-ttu-id="870d4-270">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-270">Required</span></span> | <span data-ttu-id="870d4-271">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-271">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="870d4-272">String</span><span class="sxs-lookup"><span data-stu-id="870d4-272">String</span></span>|<span data-ttu-id="870d4-273">64 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-273">64 characters</span></span>|<span data-ttu-id="870d4-274">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-274">✔</span></span>|<span data-ttu-id="870d4-275">Уникальный идентификатор объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="870d4-275">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="870d4-276">String</span><span class="sxs-lookup"><span data-stu-id="870d4-276">String</span></span>|<span data-ttu-id="870d4-277">128 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-277">128 characters</span></span>|<span data-ttu-id="870d4-278">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-278">✔</span></span>|<span data-ttu-id="870d4-279">Отображаемое имя вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="870d4-279">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="870d4-280">String</span><span class="sxs-lookup"><span data-stu-id="870d4-280">String</span></span>|<span data-ttu-id="870d4-281">2048 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-281">2048 characters</span></span>|<span data-ttu-id="870d4-282">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-282">✔</span></span>|<span data-ttu-id="870d4-283">URL-адрес https://, указывающий на пользовательский интерфейс сущности, который будет отображаться в полотне Teams.</span><span class="sxs-lookup"><span data-stu-id="870d4-283">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="870d4-284">String</span><span class="sxs-lookup"><span data-stu-id="870d4-284">String</span></span>|<span data-ttu-id="870d4-285">2048 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-285">2048 characters</span></span>||<span data-ttu-id="870d4-286">URL-адрес https://, указывающий, когда пользователь попытается просмотреть его в браузере.</span><span class="sxs-lookup"><span data-stu-id="870d4-286">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="870d4-287">Массив перечисления</span><span class="sxs-lookup"><span data-stu-id="870d4-287">Array of enum</span></span>|<span data-ttu-id="870d4-288">1 </span><span class="sxs-lookup"><span data-stu-id="870d4-288">1</span></span>|<span data-ttu-id="870d4-289">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-289">✔</span></span>|<span data-ttu-id="870d4-290">В настоящее время статические вкладки поддерживают `personal` только область, что означает, что ее можно подготовить только в рамках личного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="870d4-290">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="870d4-291">Боты</span><span class="sxs-lookup"><span data-stu-id="870d4-291">bots</span></span>

<span data-ttu-id="870d4-292">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="870d4-292">**Optional**</span></span>

<span data-ttu-id="870d4-293">Определяет одноэлементное решение, а также дополнительные сведения, такие как свойства команды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="870d4-293">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="870d4-294">Объект является массивом (в настоящее время для каждого приложения&mdash;допускается только один элемент "bot" для каждого приложения) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="870d4-294">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="870d4-295">Этот блок необходим только для решений, предоставляющих интерфейс Bot.</span><span class="sxs-lookup"><span data-stu-id="870d4-295">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="870d4-296">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-296">Name</span></span>| <span data-ttu-id="870d4-297">Тип</span><span class="sxs-lookup"><span data-stu-id="870d4-297">Type</span></span>| <span data-ttu-id="870d4-298">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-298">Maximum size</span></span> | <span data-ttu-id="870d4-299">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-299">Required</span></span> | <span data-ttu-id="870d4-300">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-300">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="870d4-301">String</span><span class="sxs-lookup"><span data-stu-id="870d4-301">String</span></span>|<span data-ttu-id="870d4-302">64 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-302">64 characters</span></span>|<span data-ttu-id="870d4-303">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-303">✔</span></span>|<span data-ttu-id="870d4-304">Уникальный идентификатор приложения для ленты, зарегистрированный с помощью Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="870d4-304">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="870d4-305">Это может быть так же, как и общий [идентификатор приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="870d4-305">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="870d4-306">Boolean</span><span class="sxs-lookup"><span data-stu-id="870d4-306">Boolean</span></span>|||<span data-ttu-id="870d4-307">Описывает, использует ли пользователь почтовые подсказка для добавления ленты к определенному каналу.</span><span class="sxs-lookup"><span data-stu-id="870d4-307">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="870d4-308">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="870d4-308">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="870d4-309">Boolean</span><span class="sxs-lookup"><span data-stu-id="870d4-309">Boolean</span></span>|||<span data-ttu-id="870d4-310">Указывает, является ли Bot односторонним, только для уведомления, а не с сообщением Bot.</span><span class="sxs-lookup"><span data-stu-id="870d4-310">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="870d4-311">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="870d4-311">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="870d4-312">Boolean</span><span class="sxs-lookup"><span data-stu-id="870d4-312">Boolean</span></span>|||<span data-ttu-id="870d4-313">Указывает, поддерживает ли Bot возможность загрузки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="870d4-313">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="870d4-314">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="870d4-314">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="870d4-315">Массив перечисления</span><span class="sxs-lookup"><span data-stu-id="870d4-315">Array of enum</span></span>|<span data-ttu-id="870d4-316">3 </span><span class="sxs-lookup"><span data-stu-id="870d4-316">3</span></span>|<span data-ttu-id="870d4-317">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-317">✔</span></span>|<span data-ttu-id="870d4-318">Указывает `team`, является ли Bot интерфейсом пользователя в контексте канала в, в разделе "участие в группах" (`groupchat`) или взаимодействия с областью действия только для отдельного пользователя (`personal`).</span><span class="sxs-lookup"><span data-stu-id="870d4-318">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="870d4-319">Эти параметры не являются монопольными.</span><span class="sxs-lookup"><span data-stu-id="870d4-319">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="870d4-320">Боты. Коммандлистс</span><span class="sxs-lookup"><span data-stu-id="870d4-320">bots.commandLists</span></span>

<span data-ttu-id="870d4-321">Необязательный список команд, которые ваш робот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="870d4-321">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="870d4-322">Объект является массивом (не более 2 элементов) со всеми элементами типа `object`; необходимо определить отдельный список команд для каждой области, которую поддерживает Bot.</span><span class="sxs-lookup"><span data-stu-id="870d4-322">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="870d4-323">Дополнительные сведения содержатся в [меню Bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="870d4-323">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="870d4-324">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-324">Name</span></span>| <span data-ttu-id="870d4-325">Тип</span><span class="sxs-lookup"><span data-stu-id="870d4-325">Type</span></span>| <span data-ttu-id="870d4-326">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-326">Maximum size</span></span> | <span data-ttu-id="870d4-327">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-327">Required</span></span> | <span data-ttu-id="870d4-328">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-328">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="870d4-329">массив перечисления</span><span class="sxs-lookup"><span data-stu-id="870d4-329">array of enum</span></span>|<span data-ttu-id="870d4-330">3 </span><span class="sxs-lookup"><span data-stu-id="870d4-330">3</span></span>|<span data-ttu-id="870d4-331">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-331">✔</span></span>|<span data-ttu-id="870d4-332">Задает область действия, для которой список команд является допустимым.</span><span class="sxs-lookup"><span data-stu-id="870d4-332">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="870d4-333">Параметры: `team`, `personal`, и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="870d4-333">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="870d4-334">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="870d4-334">array of objects</span></span>|<span data-ttu-id="870d4-335">10 </span><span class="sxs-lookup"><span data-stu-id="870d4-335">10</span></span>|<span data-ttu-id="870d4-336">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-336">✔</span></span>|<span data-ttu-id="870d4-337">Массив команд, поддерживаемых в Bot:</span><span class="sxs-lookup"><span data-stu-id="870d4-337">An array of commands the bot supports:</span></span><br><span data-ttu-id="870d4-338">`title`: имя команды Bot (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="870d4-338">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="870d4-339">`description`: простое описание или пример синтаксиса команды и его аргумента (строка, 128).</span><span class="sxs-lookup"><span data-stu-id="870d4-339">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="870d4-340">аудиовыход</span><span class="sxs-lookup"><span data-stu-id="870d4-340">connectors</span></span>

<span data-ttu-id="870d4-341">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="870d4-341">**Optional**</span></span>

<span data-ttu-id="870d4-342">`connectors` Блок определяет соединитель Office 365 для приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-342">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="870d4-343">Объект является массивом (не более 1 элемента) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="870d4-343">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="870d4-344">Этот блок необходим только для решений, предоставляющих соединитель.</span><span class="sxs-lookup"><span data-stu-id="870d4-344">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="870d4-345">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-345">Name</span></span>| <span data-ttu-id="870d4-346">Тип</span><span class="sxs-lookup"><span data-stu-id="870d4-346">Type</span></span>| <span data-ttu-id="870d4-347">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-347">Maximum size</span></span> | <span data-ttu-id="870d4-348">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-348">Required</span></span> | <span data-ttu-id="870d4-349">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-349">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="870d4-350">String</span><span class="sxs-lookup"><span data-stu-id="870d4-350">String</span></span>|<span data-ttu-id="870d4-351">2048 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-351">2048 characters</span></span>|<span data-ttu-id="870d4-352">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-352">✔</span></span>|<span data-ttu-id="870d4-353">URL-адрес https://, используемый при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="870d4-353">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="870d4-354">String</span><span class="sxs-lookup"><span data-stu-id="870d4-354">String</span></span>|<span data-ttu-id="870d4-355">64 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-355">64 characters</span></span>|<span data-ttu-id="870d4-356">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-356">✔</span></span>|<span data-ttu-id="870d4-357">Уникальный идентификатор соединителя, который соответствует ИДЕНТИФИКАТОРу в [панели мониторинга разработчика соединителей](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="870d4-357">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="870d4-358">Массив перечисления</span><span class="sxs-lookup"><span data-stu-id="870d4-358">Array of enum</span></span>|<span data-ttu-id="870d4-359">1 </span><span class="sxs-lookup"><span data-stu-id="870d4-359">1</span></span>|<span data-ttu-id="870d4-360">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-360">✔</span></span>|<span data-ttu-id="870d4-361">Указывает `team`, будет ли соединитель работать в контексте канала в или в интерфейсе для отдельного пользователя (`personal`).</span><span class="sxs-lookup"><span data-stu-id="870d4-361">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="870d4-362">В настоящее время поддерживается `team` только область действия.</span><span class="sxs-lookup"><span data-stu-id="870d4-362">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="870d4-363">компосикстенсионс</span><span class="sxs-lookup"><span data-stu-id="870d4-363">composeExtensions</span></span>

<span data-ttu-id="870d4-364">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="870d4-364">**Optional**</span></span>

<span data-ttu-id="870d4-365">Определяет расширение системы обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-365">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="870d4-366">Имя компонента изменилось с "расширение составления" на "расширение обмена сообщениями" в ноябре 2017, но имя манифеста остается без изменений, поэтому все существующие расширения продолжают работать.</span><span class="sxs-lookup"><span data-stu-id="870d4-366">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="870d4-367">Объект является массивом (не более 1 элемента) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="870d4-367">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="870d4-368">Этот блок необходим только для решений, предоставляющих расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="870d4-368">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="870d4-369">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-369">Name</span></span>| <span data-ttu-id="870d4-370">Тип</span><span class="sxs-lookup"><span data-stu-id="870d4-370">Type</span></span> | <span data-ttu-id="870d4-371">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-371">Maximum Size</span></span> | <span data-ttu-id="870d4-372">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-372">Required</span></span> | <span data-ttu-id="870d4-373">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-373">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="870d4-374">String</span><span class="sxs-lookup"><span data-stu-id="870d4-374">String</span></span>|<span data-ttu-id="870d4-375">64</span><span class="sxs-lookup"><span data-stu-id="870d4-375">64</span></span>|<span data-ttu-id="870d4-376">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-376">✔</span></span>|<span data-ttu-id="870d4-377">Уникальный идентификатор приложения для ленты, который выполняет резервное копирование расширения обмена сообщениями, как зарегистрировано в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="870d4-377">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="870d4-378">Это может быть так же, как и общий идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-378">This may well be the same as the overall App ID.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="870d4-379">Boolean</span><span class="sxs-lookup"><span data-stu-id="870d4-379">Boolean</span></span>|||<span data-ttu-id="870d4-380">Значение, указывающее, может ли пользователь изменять конфигурацию расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="870d4-380">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="870d4-381">Значение по умолчанию: `false`.</span><span class="sxs-lookup"><span data-stu-id="870d4-381">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="870d4-382">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="870d4-382">Array of object</span></span>|<span data-ttu-id="870d4-383">10 </span><span class="sxs-lookup"><span data-stu-id="870d4-383">10</span></span>|<span data-ttu-id="870d4-384">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-384">✔</span></span>|<span data-ttu-id="870d4-385">Массив команд, поддерживающих расширение системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="870d4-385">Array of commands the messaging extension supports</span></span>|
|`messageHandlers`|<span data-ttu-id="870d4-386">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="870d4-386">Array of Objects</span></span>|<span data-ttu-id="870d4-387">5 </span><span class="sxs-lookup"><span data-stu-id="870d4-387">5</span></span>||<span data-ttu-id="870d4-388">Список обработчиков, позволяющих вызывать приложения при выполнении определенных условий.</span><span class="sxs-lookup"><span data-stu-id="870d4-388">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="870d4-389">Домены также должны быть перечислены в`validDomains`</span><span class="sxs-lookup"><span data-stu-id="870d4-389">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="870d4-390">String</span><span class="sxs-lookup"><span data-stu-id="870d4-390">String</span></span>|||<span data-ttu-id="870d4-391">Тип обработчика сообщений.</span><span class="sxs-lookup"><span data-stu-id="870d4-391">The type of message handler.</span></span> <span data-ttu-id="870d4-392">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="870d4-392">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="870d4-393">Массив строк</span><span class="sxs-lookup"><span data-stu-id="870d4-393">Array of Strings</span></span>|||<span data-ttu-id="870d4-394">Массив доменов, для которых может регистрироваться обработчик сообщений ссылки.</span><span class="sxs-lookup"><span data-stu-id="870d4-394">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="870d4-395">Компосикстенсионс. Commands</span><span class="sxs-lookup"><span data-stu-id="870d4-395">composeExtensions.commands</span></span>

<span data-ttu-id="870d4-396">Ваш модуль обмена сообщениями должен объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="870d4-396">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="870d4-397">Каждая команда отображается в Microsoft Teams в качестве потенциального взаимодействия от точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="870d4-397">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="870d4-398">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="870d4-398">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="870d4-399">Каждый элемент команды представляет собой объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="870d4-399">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="870d4-400">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-400">Name</span></span>| <span data-ttu-id="870d4-401">Тип</span><span class="sxs-lookup"><span data-stu-id="870d4-401">Type</span></span>| <span data-ttu-id="870d4-402">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-402">Maximum size</span></span> | <span data-ttu-id="870d4-403">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-403">Required</span></span> | <span data-ttu-id="870d4-404">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-404">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="870d4-405">String</span><span class="sxs-lookup"><span data-stu-id="870d4-405">String</span></span>|<span data-ttu-id="870d4-406">64 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-406">64 characters</span></span>|<span data-ttu-id="870d4-407">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-407">✔</span></span>|<span data-ttu-id="870d4-408">Идентификатор команды</span><span class="sxs-lookup"><span data-stu-id="870d4-408">The ID for the command</span></span>|
|`type`|<span data-ttu-id="870d4-409">String</span><span class="sxs-lookup"><span data-stu-id="870d4-409">String</span></span>|<span data-ttu-id="870d4-410">64 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-410">64 characters</span></span>||<span data-ttu-id="870d4-411">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="870d4-411">Type of the command.</span></span> <span data-ttu-id="870d4-412">Один из `query` или `action`.</span><span class="sxs-lookup"><span data-stu-id="870d4-412">One of `query` or `action`.</span></span> <span data-ttu-id="870d4-413">Умолчани`query`</span><span class="sxs-lookup"><span data-stu-id="870d4-413">Default: `query`</span></span>|
|`title`|<span data-ttu-id="870d4-414">String</span><span class="sxs-lookup"><span data-stu-id="870d4-414">String</span></span>|<span data-ttu-id="870d4-415">32 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-415">32 characters</span></span>|<span data-ttu-id="870d4-416">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-416">✔</span></span>|<span data-ttu-id="870d4-417">Понятное имя команды</span><span class="sxs-lookup"><span data-stu-id="870d4-417">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="870d4-418">String</span><span class="sxs-lookup"><span data-stu-id="870d4-418">String</span></span>|<span data-ttu-id="870d4-419">128 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-419">128 characters</span></span>||<span data-ttu-id="870d4-420">Описание, которое отображается пользователям для указания цели этой команды</span><span class="sxs-lookup"><span data-stu-id="870d4-420">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="870d4-421">Boolean</span><span class="sxs-lookup"><span data-stu-id="870d4-421">Boolean</span></span>|||<span data-ttu-id="870d4-422">Логическое значение, которое указывает, следует ли выполнять команду изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="870d4-422">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="870d4-423">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="870d4-423">Default: `false`</span></span>|
|`context`|<span data-ttu-id="870d4-424">Массив строк</span><span class="sxs-lookup"><span data-stu-id="870d4-424">Array of Strings</span></span>|<span data-ttu-id="870d4-425">3 </span><span class="sxs-lookup"><span data-stu-id="870d4-425">3</span></span>||<span data-ttu-id="870d4-426">Определяет, откуда можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="870d4-426">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="870d4-427">Любое сочетание `compose`, `commandBox`,. `message`</span><span class="sxs-lookup"><span data-stu-id="870d4-427">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="870d4-428">Значение по умолчанию:`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="870d4-428">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="870d4-429">Boolean</span><span class="sxs-lookup"><span data-stu-id="870d4-429">Boolean</span></span>|||<span data-ttu-id="870d4-430">Логическое значение, указывающее, должен ли он динамически получать модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="870d4-430">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="870d4-431">Объект</span><span class="sxs-lookup"><span data-stu-id="870d4-431">Object</span></span>|||<span data-ttu-id="870d4-432">Указание модуля задач для предварительной загрузки при использовании команды расширения системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="870d4-432">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="870d4-433">String</span><span class="sxs-lookup"><span data-stu-id="870d4-433">String</span></span>|<span data-ttu-id="870d4-434">64</span><span class="sxs-lookup"><span data-stu-id="870d4-434">64</span></span>||<span data-ttu-id="870d4-435">Заголовок начального диалогового окна</span><span class="sxs-lookup"><span data-stu-id="870d4-435">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="870d4-436">String</span><span class="sxs-lookup"><span data-stu-id="870d4-436">String</span></span>|||<span data-ttu-id="870d4-437">Ширина диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый"</span><span class="sxs-lookup"><span data-stu-id="870d4-437">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="870d4-438">String</span><span class="sxs-lookup"><span data-stu-id="870d4-438">String</span></span>|||<span data-ttu-id="870d4-439">Высота диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый"</span><span class="sxs-lookup"><span data-stu-id="870d4-439">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="870d4-440">String</span><span class="sxs-lookup"><span data-stu-id="870d4-440">String</span></span>|||<span data-ttu-id="870d4-441">Исходный URL-адрес вебвиев</span><span class="sxs-lookup"><span data-stu-id="870d4-441">Initial webview URL</span></span>|
|`parameters`|<span data-ttu-id="870d4-442">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="870d4-442">Array of object</span></span>|<span data-ttu-id="870d4-443">5 </span><span class="sxs-lookup"><span data-stu-id="870d4-443">5</span></span>|<span data-ttu-id="870d4-444">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-444">✔</span></span>|<span data-ttu-id="870d4-445">Список параметров, которые выполняет команда.</span><span class="sxs-lookup"><span data-stu-id="870d4-445">The list of parameters the command takes.</span></span> <span data-ttu-id="870d4-446">Минимум: 1; максимум: 5</span><span class="sxs-lookup"><span data-stu-id="870d4-446">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="870d4-447">String</span><span class="sxs-lookup"><span data-stu-id="870d4-447">String</span></span>|<span data-ttu-id="870d4-448">64 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-448">64 characters</span></span>|<span data-ttu-id="870d4-449">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-449">✔</span></span>|<span data-ttu-id="870d4-450">Имя параметра в том виде, в котором оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="870d4-450">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="870d4-451">Он включен в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="870d4-451">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="870d4-452">String</span><span class="sxs-lookup"><span data-stu-id="870d4-452">String</span></span>|<span data-ttu-id="870d4-453">32 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-453">32 characters</span></span>|<span data-ttu-id="870d4-454">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-454">✔</span></span>|<span data-ttu-id="870d4-455">Удобное для пользователя название параметра.</span><span class="sxs-lookup"><span data-stu-id="870d4-455">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="870d4-456">String</span><span class="sxs-lookup"><span data-stu-id="870d4-456">String</span></span>|<span data-ttu-id="870d4-457">128 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-457">128 characters</span></span>||<span data-ttu-id="870d4-458">Понятная пользователю строка, описывающая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="870d4-458">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="870d4-459">String</span><span class="sxs-lookup"><span data-stu-id="870d4-459">String</span></span>|<span data-ttu-id="870d4-460">128 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-460">128 characters</span></span>||<span data-ttu-id="870d4-461">Определяет тип элемента управления, отображаемого в модуле задачи для `fetchTask: true`.</span><span class="sxs-lookup"><span data-stu-id="870d4-461">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="870d4-462">Один из `text`, `textarea`, `number`, `date` `time`,, `toggle`,`choiceset`</span><span class="sxs-lookup"><span data-stu-id="870d4-462">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="870d4-463">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="870d4-463">Array of Objects</span></span>|<span data-ttu-id="870d4-464">10 </span><span class="sxs-lookup"><span data-stu-id="870d4-464">10</span></span>||<span data-ttu-id="870d4-465">Варианты выбора для `choiceset`.</span><span class="sxs-lookup"><span data-stu-id="870d4-465">The choice options for the `choiceset`.</span></span> <span data-ttu-id="870d4-466">Используйте только в `parameter.inputType` том случае, если`choiceset`</span><span class="sxs-lookup"><span data-stu-id="870d4-466">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="870d4-467">String</span><span class="sxs-lookup"><span data-stu-id="870d4-467">String</span></span>|<span data-ttu-id="870d4-468">128</span><span class="sxs-lookup"><span data-stu-id="870d4-468">128</span></span>||<span data-ttu-id="870d4-469">Название варианта</span><span class="sxs-lookup"><span data-stu-id="870d4-469">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="870d4-470">String</span><span class="sxs-lookup"><span data-stu-id="870d4-470">String</span></span>|<span data-ttu-id="870d4-471">512</span><span class="sxs-lookup"><span data-stu-id="870d4-471">512</span></span>||<span data-ttu-id="870d4-472">Выбор значения</span><span class="sxs-lookup"><span data-stu-id="870d4-472">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="870d4-473">permissions</span><span class="sxs-lookup"><span data-stu-id="870d4-473">permissions</span></span>

<span data-ttu-id="870d4-474">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="870d4-474">**Optional**</span></span>

<span data-ttu-id="870d4-475">Массив `string` , определяющий, какие разрешения запрашиваются приложением, что позволяет конечным пользователям знать, как будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="870d4-475">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="870d4-476">Следующие параметры неисключительны:</span><span class="sxs-lookup"><span data-stu-id="870d4-476">The following options are non-exclusive:</span></span>

* <span data-ttu-id="870d4-477">`identity`&emsp; Требуются сведения об удостоверении пользователя</span><span class="sxs-lookup"><span data-stu-id="870d4-477">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="870d4-478">`messageTeamMembers`&emsp; Требуется разрешение на отправку прямых сообщений участникам группы</span><span class="sxs-lookup"><span data-stu-id="870d4-478">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="870d4-479">Изменение этих разрешений при обновлении приложения приводит к тому, что пользователи будут повторять процесс разрешения при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-479">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="870d4-480">Дополнительные сведения см. [в разделе Обновление приложения](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) .</span><span class="sxs-lookup"><span data-stu-id="870d4-480">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="870d4-481">девицепермиссионс</span><span class="sxs-lookup"><span data-stu-id="870d4-481">devicePermissions</span></span>

<span data-ttu-id="870d4-482">**Необязательное требование** Массив строк</span><span class="sxs-lookup"><span data-stu-id="870d4-482">**Optional** Array of Strings</span></span>

<span data-ttu-id="870d4-483">Указывает собственные функции на устройстве пользователя, к которым приложение может запрашивать доступ.</span><span class="sxs-lookup"><span data-stu-id="870d4-483">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="870d4-484">Возможные варианты:</span><span class="sxs-lookup"><span data-stu-id="870d4-484">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="870d4-485">валиддомаинс</span><span class="sxs-lookup"><span data-stu-id="870d4-485">validDomains</span></span>

<span data-ttu-id="870d4-486">**Необязательно**, за исключением **обязательного** места, где отмечено</span><span class="sxs-lookup"><span data-stu-id="870d4-486">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="870d4-487">Список допустимых доменов для веб-сайтов, которые приложение ожидает загружать в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="870d4-487">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="870d4-488">Примеры доменов могут включать подстановочные знаки `*.example.com`.</span><span class="sxs-lookup"><span data-stu-id="870d4-488">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="870d4-489">Это соответствует только одному сегменту домена; Если вам нужно использовать `a.b.example.com` `*.*.example.com`этот параметр.</span><span class="sxs-lookup"><span data-stu-id="870d4-489">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="870d4-490">Если конфигурация вкладки или контентный пользовательский интерфейс должны перейти к любому другому домену, Кроме того, что используется для настройки вкладок, этот домен необходимо указать здесь.</span><span class="sxs-lookup"><span data-stu-id="870d4-490">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="870d4-491">Тем не менее, **не** нужно включать домены поставщиков удостоверений, которые требуется поддерживать в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="870d4-491">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="870d4-492">Например, для проверки подлинности с помощью идентификатора Google необходимо перенаправить на accounts.google.com, но не следует включать accounts.google.com в `validDomains[]`.</span><span class="sxs-lookup"><span data-stu-id="870d4-492">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="870d4-493">Приложения Teams, которым для правильной работы требуются собственные URL-адреса SharePoint, могут содержать "{теамситедомаин}" в допустимом списке доменов.</span><span class="sxs-lookup"><span data-stu-id="870d4-493">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="870d4-494">Не добавляйте домены за предельный элемент управления (напрямую или с помощью подстановочных знаков).</span><span class="sxs-lookup"><span data-stu-id="870d4-494">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="870d4-495">Например, `yourapp.onmicrosoft.com` является допустимым, но `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="870d4-495">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="870d4-496">Объект является массивом со всеми элементами типа `string`.</span><span class="sxs-lookup"><span data-stu-id="870d4-496">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="870d4-497">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="870d4-497">webApplicationInfo</span></span>

<span data-ttu-id="870d4-498">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="870d4-498">**Optional**</span></span>

<span data-ttu-id="870d4-499">Указание идентификатора приложения и графического объекта AAD для упрощения входа пользователей в приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="870d4-499">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="870d4-500">Имя</span><span class="sxs-lookup"><span data-stu-id="870d4-500">Name</span></span>| <span data-ttu-id="870d4-501">Тип</span><span class="sxs-lookup"><span data-stu-id="870d4-501">Type</span></span>| <span data-ttu-id="870d4-502">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="870d4-502">Maximum size</span></span> | <span data-ttu-id="870d4-503">Обязательный</span><span class="sxs-lookup"><span data-stu-id="870d4-503">Required</span></span> | <span data-ttu-id="870d4-504">Описание</span><span class="sxs-lookup"><span data-stu-id="870d4-504">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="870d4-505">String</span><span class="sxs-lookup"><span data-stu-id="870d4-505">String</span></span>|<span data-ttu-id="870d4-506">36 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-506">36 characters</span></span>|<span data-ttu-id="870d4-507">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-507">✔</span></span>|<span data-ttu-id="870d4-508">Идентификатор приложения AAD приложения.</span><span class="sxs-lookup"><span data-stu-id="870d4-508">AAD application id of the app.</span></span> <span data-ttu-id="870d4-509">Этот идентификатор должен быть идентификатором GUID.</span><span class="sxs-lookup"><span data-stu-id="870d4-509">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="870d4-510">String</span><span class="sxs-lookup"><span data-stu-id="870d4-510">String</span></span>|<span data-ttu-id="870d4-511">2048 символов</span><span class="sxs-lookup"><span data-stu-id="870d4-511">2048 characters</span></span>|<span data-ttu-id="870d4-512">✔</span><span class="sxs-lookup"><span data-stu-id="870d4-512">✔</span></span>|<span data-ttu-id="870d4-513">URL-адрес ресурса приложения для получения маркера проверки подлинности для единого входа.</span><span class="sxs-lookup"><span data-stu-id="870d4-513">Resource url of app for acquiring auth token for SSO.</span></span>|
