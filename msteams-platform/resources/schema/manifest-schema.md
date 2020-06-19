---
title: Справочник по схеме манифеста
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams.
keywords: Схема манифеста Teams
ms.openlocfilehash: 061b39430cf8eba229b4e0c3012a5bbf752a5e85
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2020
ms.locfileid: "44801552"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="df016-104">Ссылка: схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="df016-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="df016-105">Манифест Microsoft Teams описывает, как приложение интегрируется в продукт Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="df016-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="df016-106">Манифест должен соответствовать схеме, размещенной в [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="df016-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="df016-107">Также поддерживаются предыдущие версии 1.0-1.4 (в URL-адресе используется "v1. x").</span><span class="sxs-lookup"><span data-stu-id="df016-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="df016-108">В приведенном ниже примере схемы показаны все варианты расширения.</span><span class="sxs-lookup"><span data-stu-id="df016-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="df016-109">Пример полного манифеста</span><span class="sxs-lookup"><span data-stu-id="df016-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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
          "type" : "query",
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

<span data-ttu-id="df016-110">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="df016-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="df016-111">$schema</span><span class="sxs-lookup"><span data-stu-id="df016-111">$schema</span></span>

<span data-ttu-id="df016-112">*Необязательно, но рекомендуется* &ndash; Substring</span><span class="sxs-lookup"><span data-stu-id="df016-112">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="df016-113">URL-адрес https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="df016-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="df016-114">Версия манифеста</span><span class="sxs-lookup"><span data-stu-id="df016-114">manifestVersion</span></span>

<span data-ttu-id="df016-115">**Required (обязательный** &ndash; ) Substring</span><span class="sxs-lookup"><span data-stu-id="df016-115">**Required** &ndash; String</span></span>

<span data-ttu-id="df016-116">Версия схемы манифеста, используемая манифестом.</span><span class="sxs-lookup"><span data-stu-id="df016-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="df016-117">Он должен иметь значения "1,5".</span><span class="sxs-lookup"><span data-stu-id="df016-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="df016-118">version</span><span class="sxs-lookup"><span data-stu-id="df016-118">version</span></span>

<span data-ttu-id="df016-119">**Required (обязательный** &ndash; ) Substring</span><span class="sxs-lookup"><span data-stu-id="df016-119">**Required** &ndash; String</span></span>

<span data-ttu-id="df016-120">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-120">The version of the specific app.</span></span> <span data-ttu-id="df016-121">Если вы обновите какой-либо элемент в манифесте, необходимо также увеличить номер версии.</span><span class="sxs-lookup"><span data-stu-id="df016-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="df016-122">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="df016-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="df016-123">Если это приложение было отправлено в хранилище, новый манифест необходимо будет повторно отправить и проверить повторно.</span><span class="sxs-lookup"><span data-stu-id="df016-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="df016-124">После этого пользователи этого приложения автоматически получат новый обновленный манифест в течение нескольких часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="df016-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="df016-125">Если приложение запросило изменение разрешений, пользователям будет предложено выполнить обновление и повторное согласие на доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="df016-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="df016-126">Эта строка версии должна соответствовать стандарту [semver](http://semver.org/) (Major. Значительные. PATCH).</span><span class="sxs-lookup"><span data-stu-id="df016-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="df016-127">id</span><span class="sxs-lookup"><span data-stu-id="df016-127">id</span></span>

<span data-ttu-id="df016-128">**Required (обязательный** &ndash; ) Идентификатор приложения Microsoft</span><span class="sxs-lookup"><span data-stu-id="df016-128">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="df016-129">Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="df016-130">Если вы зарегистрировали Bot с помощью Microsoft Bot Framework, или веб-приложение вашей вкладки уже входит в Microsoft, у вас уже должен быть идентификатор, и его следует ввести здесь.</span><span class="sxs-lookup"><span data-stu-id="df016-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="df016-131">В противном случае необходимо создать новый идентификатор на портале регистрации приложений ([Мои приложения](https://apps.dev.microsoft.com)) Майкрософт, ввести его здесь, а затем повторно использовать его при добавлении ленты. Note: Если вы отправляете обновление существующему приложению в AppSource, идентификатор в манифесте не должен изменяться.</span><span class="sxs-lookup"><span data-stu-id="df016-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="packagename"></a><span data-ttu-id="df016-132">паккаженаме</span><span class="sxs-lookup"><span data-stu-id="df016-132">packageName</span></span>

<span data-ttu-id="df016-133">**Required (обязательный** &ndash; ) Substring</span><span class="sxs-lookup"><span data-stu-id="df016-133">**Required** &ndash; String</span></span>

<span data-ttu-id="df016-134">Уникальный идентификатор для этого приложения в обратной нотации домена; Пример: com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="df016-134">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="df016-135">developer</span><span class="sxs-lookup"><span data-stu-id="df016-135">developer</span></span>

<span data-ttu-id="df016-136">**Required**</span><span class="sxs-lookup"><span data-stu-id="df016-136">**Required**</span></span>

<span data-ttu-id="df016-137">Указывает сведения о компании.</span><span class="sxs-lookup"><span data-stu-id="df016-137">Specifies information about your company.</span></span> <span data-ttu-id="df016-138">Для приложений, отправляемых в AppSource (ранее — магазин Office), эти значения должны быть сопоставлены со сведениями в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="df016-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="df016-139">Ознакомьтесь с нашими [рекомендациями по публикации](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="df016-139">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="df016-140">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-140">Name</span></span>| <span data-ttu-id="df016-141">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-141">Maximum size</span></span> | <span data-ttu-id="df016-142">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-142">Required</span></span> | <span data-ttu-id="df016-143">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="df016-144">32 символов</span><span class="sxs-lookup"><span data-stu-id="df016-144">32 characters</span></span>|<span data-ttu-id="df016-145">✔</span><span class="sxs-lookup"><span data-stu-id="df016-145">✔</span></span>|<span data-ttu-id="df016-146">Отображаемое имя разработчика.</span><span class="sxs-lookup"><span data-stu-id="df016-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="df016-147">2048 символов</span><span class="sxs-lookup"><span data-stu-id="df016-147">2048 characters</span></span>|<span data-ttu-id="df016-148">✔</span><span class="sxs-lookup"><span data-stu-id="df016-148">✔</span></span>|<span data-ttu-id="df016-149">URL-адрес https://на веб-сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="df016-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="df016-150">Эта ссылка должна принять участие у пользователей в вашей компании или целевой странице для конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="df016-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="df016-151">2048 символов</span><span class="sxs-lookup"><span data-stu-id="df016-151">2048 characters</span></span>|<span data-ttu-id="df016-152">✔</span><span class="sxs-lookup"><span data-stu-id="df016-152">✔</span></span>|<span data-ttu-id="df016-153">URL-адрес https://для политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="df016-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="df016-154">2048 символов</span><span class="sxs-lookup"><span data-stu-id="df016-154">2048 characters</span></span>|<span data-ttu-id="df016-155">✔</span><span class="sxs-lookup"><span data-stu-id="df016-155">✔</span></span>|<span data-ttu-id="df016-156">URL-адрес https://для условий использования разработчиком.</span><span class="sxs-lookup"><span data-stu-id="df016-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="df016-157">10 символов</span><span class="sxs-lookup"><span data-stu-id="df016-157">10 characters</span></span>| |<span data-ttu-id="df016-158">**Необязательное требование** Идентификатор сети партнера Майкрософт, определяющий партнерскую организацию, которая создает приложение.</span><span class="sxs-lookup"><span data-stu-id="df016-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="df016-159">локализатионинфо</span><span class="sxs-lookup"><span data-stu-id="df016-159">localizationInfo</span></span>

<span data-ttu-id="df016-160">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="df016-160">**Optional**</span></span>

<span data-ttu-id="df016-161">Разрешает спецификацию языка по умолчанию, а также указателей на дополнительные языковые файлы.</span><span class="sxs-lookup"><span data-stu-id="df016-161">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="df016-162">См.: [Локализация](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="df016-162">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="df016-163">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-163">Name</span></span>| <span data-ttu-id="df016-164">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-164">Maximum size</span></span> | <span data-ttu-id="df016-165">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-165">Required</span></span> | <span data-ttu-id="df016-166">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-166">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="df016-167">✔</span><span class="sxs-lookup"><span data-stu-id="df016-167">✔</span></span>|<span data-ttu-id="df016-168">Тег языка строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="df016-168">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="df016-169">Локализатионинфо. Аддитионаллангуажес</span><span class="sxs-lookup"><span data-stu-id="df016-169">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="df016-170">Массив объектов, задающий дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="df016-170">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="df016-171">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-171">Name</span></span>| <span data-ttu-id="df016-172">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-172">Maximum size</span></span> | <span data-ttu-id="df016-173">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-173">Required</span></span> | <span data-ttu-id="df016-174">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-174">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="df016-175">✔</span><span class="sxs-lookup"><span data-stu-id="df016-175">✔</span></span>|<span data-ttu-id="df016-176">Тег языка строк в указанном файле.</span><span class="sxs-lookup"><span data-stu-id="df016-176">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="df016-177">✔</span><span class="sxs-lookup"><span data-stu-id="df016-177">✔</span></span>|<span data-ttu-id="df016-178">Относительный путь к файлу. JSON, содержащему переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="df016-178">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="df016-179">name</span><span class="sxs-lookup"><span data-stu-id="df016-179">name</span></span>

<span data-ttu-id="df016-180">**Required**</span><span class="sxs-lookup"><span data-stu-id="df016-180">**Required**</span></span>

<span data-ttu-id="df016-181">Имя приложения, отображаемое для пользователей в интерфейсе Teams.</span><span class="sxs-lookup"><span data-stu-id="df016-181">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="df016-182">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="df016-182">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="df016-183">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="df016-183">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="df016-184">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-184">Name</span></span>| <span data-ttu-id="df016-185">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-185">Maximum size</span></span> | <span data-ttu-id="df016-186">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-186">Required</span></span> | <span data-ttu-id="df016-187">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-187">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="df016-188">30 символов</span><span class="sxs-lookup"><span data-stu-id="df016-188">30 characters</span></span>|<span data-ttu-id="df016-189">✔</span><span class="sxs-lookup"><span data-stu-id="df016-189">✔</span></span>|<span data-ttu-id="df016-190">Краткое отображаемое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-190">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="df016-191">100 символов</span><span class="sxs-lookup"><span data-stu-id="df016-191">100 characters</span></span>||<span data-ttu-id="df016-192">Полное имя приложения, используемое, если имя полного приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="df016-192">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="df016-193">description</span><span class="sxs-lookup"><span data-stu-id="df016-193">description</span></span>

<span data-ttu-id="df016-194">**Required**</span><span class="sxs-lookup"><span data-stu-id="df016-194">**Required**</span></span>

<span data-ttu-id="df016-195">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="df016-195">Describes your app to users.</span></span> <span data-ttu-id="df016-196">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="df016-196">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="df016-197">Убедитесь, что ваше описание точно описывает ваш интерфейс и предоставляет сведения, помогающие потенциальным клиентам определить, что делает ваш интерфейс.</span><span class="sxs-lookup"><span data-stu-id="df016-197">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="df016-198">Кроме того, в полном описании следует отметить, если для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="df016-198">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="df016-199">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="df016-199">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="df016-200">Краткое описание не должно повторяться в длинном описании и не должно включать имя другого приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-200">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="df016-201">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-201">Name</span></span>| <span data-ttu-id="df016-202">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-202">Maximum size</span></span> | <span data-ttu-id="df016-203">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-203">Required</span></span> | <span data-ttu-id="df016-204">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-204">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="df016-205">80 символов</span><span class="sxs-lookup"><span data-stu-id="df016-205">80 characters</span></span>|<span data-ttu-id="df016-206">✔</span><span class="sxs-lookup"><span data-stu-id="df016-206">✔</span></span>|<span data-ttu-id="df016-207">Краткое описание интерфейса приложения, используемое при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="df016-207">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="df016-208">4000 символов</span><span class="sxs-lookup"><span data-stu-id="df016-208">4000 characters</span></span>|<span data-ttu-id="df016-209">✔</span><span class="sxs-lookup"><span data-stu-id="df016-209">✔</span></span>|<span data-ttu-id="df016-210">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-210">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="df016-211">icons</span><span class="sxs-lookup"><span data-stu-id="df016-211">icons</span></span>

<span data-ttu-id="df016-212">**Required**</span><span class="sxs-lookup"><span data-stu-id="df016-212">**Required**</span></span>

<span data-ttu-id="df016-213">Значки, используемые в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="df016-213">Icons used within the Teams app.</span></span> <span data-ttu-id="df016-214">Файлы значков должны быть включены в состав пакета отправки.</span><span class="sxs-lookup"><span data-stu-id="df016-214">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="df016-215">Дополнительные сведения можно найти в разделе [значки](~/concepts/build-and-test/apps-package.md#icons) .</span><span class="sxs-lookup"><span data-stu-id="df016-215">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="df016-216">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-216">Name</span></span>| <span data-ttu-id="df016-217">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-217">Maximum size</span></span> | <span data-ttu-id="df016-218">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-218">Required</span></span> | <span data-ttu-id="df016-219">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-219">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="df016-220">2048 символов</span><span class="sxs-lookup"><span data-stu-id="df016-220">2048 characters</span></span>|<span data-ttu-id="df016-221">✔</span><span class="sxs-lookup"><span data-stu-id="df016-221">✔</span></span>|<span data-ttu-id="df016-222">Относительный путь к файлу с прозрачным значком изображения в формате 32x32 PNG.</span><span class="sxs-lookup"><span data-stu-id="df016-222">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="df016-223">2048 символов</span><span class="sxs-lookup"><span data-stu-id="df016-223">2048 characters</span></span>|<span data-ttu-id="df016-224">✔</span><span class="sxs-lookup"><span data-stu-id="df016-224">✔</span></span>|<span data-ttu-id="df016-225">Относительный путь к файлу полного цветового значка PNG 192x192.</span><span class="sxs-lookup"><span data-stu-id="df016-225">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="df016-226">акцентколор</span><span class="sxs-lookup"><span data-stu-id="df016-226">accentColor</span></span>

<span data-ttu-id="df016-227">**Required (обязательный** &ndash; ) Substring</span><span class="sxs-lookup"><span data-stu-id="df016-227">**Required** &ndash; String</span></span>

<span data-ttu-id="df016-228">Цвет, используемый в сочетании с фоном для значков структуры.</span><span class="sxs-lookup"><span data-stu-id="df016-228">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="df016-229">Значение должно быть допустимым цветом HTML-кода, начинающимся с "#", например `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="df016-229">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="df016-230">конфигураблетабс</span><span class="sxs-lookup"><span data-stu-id="df016-230">configurableTabs</span></span>

<span data-ttu-id="df016-231">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="df016-231">**Optional**</span></span>

<span data-ttu-id="df016-232">Используется, когда у вашего приложения есть вкладка "канал группы", требующая дополнительной настройки перед добавлением.</span><span class="sxs-lookup"><span data-stu-id="df016-232">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="df016-233">Настраиваемые вкладки поддерживаются только в области Teams, и в настоящее время поддерживается только одна вкладка для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-233">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="df016-234">Объект является массивом со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="df016-234">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="df016-235">Этот блок необходим только для решений, которые предоставляют настраиваемое решение для вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="df016-235">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="df016-236">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-236">Name</span></span>| <span data-ttu-id="df016-237">Тип</span><span class="sxs-lookup"><span data-stu-id="df016-237">Type</span></span>| <span data-ttu-id="df016-238">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-238">Maximum size</span></span> | <span data-ttu-id="df016-239">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-239">Required</span></span> | <span data-ttu-id="df016-240">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-240">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="df016-241">String</span><span class="sxs-lookup"><span data-stu-id="df016-241">String</span></span>|<span data-ttu-id="df016-242">2048 символов</span><span class="sxs-lookup"><span data-stu-id="df016-242">2048 characters</span></span>|<span data-ttu-id="df016-243">✔</span><span class="sxs-lookup"><span data-stu-id="df016-243">✔</span></span>|<span data-ttu-id="df016-244">URL-адрес https://, используемый при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="df016-244">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="df016-245">Boolean</span><span class="sxs-lookup"><span data-stu-id="df016-245">Boolean</span></span>|||<span data-ttu-id="df016-246">Значение, указывающее, может ли пользователь обновлять экземпляр конфигурации вкладки после создания.</span><span class="sxs-lookup"><span data-stu-id="df016-246">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="df016-247">Умолчани`true`</span><span class="sxs-lookup"><span data-stu-id="df016-247">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="df016-248">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="df016-248">Array of enum</span></span>|<span data-ttu-id="df016-249">1 </span><span class="sxs-lookup"><span data-stu-id="df016-249">1</span></span>|<span data-ttu-id="df016-250">✔</span><span class="sxs-lookup"><span data-stu-id="df016-250">✔</span></span>|<span data-ttu-id="df016-251">В настоящее время настраиваемые вкладки поддерживают только `team` области и `groupchat` области.</span><span class="sxs-lookup"><span data-stu-id="df016-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="df016-252">String</span><span class="sxs-lookup"><span data-stu-id="df016-252">String</span></span>|<span data-ttu-id="df016-253">2048</span><span class="sxs-lookup"><span data-stu-id="df016-253">2048</span></span>||<span data-ttu-id="df016-254">Относительный путь к изображению вкладки для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="df016-254">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="df016-255">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="df016-255">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="df016-256">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="df016-256">Array of enum</span></span>|<span data-ttu-id="df016-257">1 </span><span class="sxs-lookup"><span data-stu-id="df016-257">1</span></span>||<span data-ttu-id="df016-258">Определяет, как будет предоставляться вкладка в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="df016-258">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="df016-259">Параметры `sharePointFullPage``sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="df016-259">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="df016-260">статиктабс</span><span class="sxs-lookup"><span data-stu-id="df016-260">staticTabs</span></span>

<span data-ttu-id="df016-261">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="df016-261">**Optional**</span></span>

<span data-ttu-id="df016-262">Определяет набор вкладок, которые по умолчанию можно закреплять, не добавляя пользователей вручную.</span><span class="sxs-lookup"><span data-stu-id="df016-262">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="df016-263">Статические вкладки, объявляемые в `personal` области, всегда фиксируются в личном интерфейсе приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-263">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="df016-264">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="df016-264">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="df016-265">Объект является массивом (не более 16 элементов) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="df016-265">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="df016-266">Этот блок необходим только для решений, предоставляющих статическое решение для вкладок.</span><span class="sxs-lookup"><span data-stu-id="df016-266">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="df016-267">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-267">Name</span></span>| <span data-ttu-id="df016-268">Тип</span><span class="sxs-lookup"><span data-stu-id="df016-268">Type</span></span>| <span data-ttu-id="df016-269">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-269">Maximum size</span></span> | <span data-ttu-id="df016-270">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-270">Required</span></span> | <span data-ttu-id="df016-271">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-271">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="df016-272">Строка</span><span class="sxs-lookup"><span data-stu-id="df016-272">String</span></span>|<span data-ttu-id="df016-273">64 символа</span><span class="sxs-lookup"><span data-stu-id="df016-273">64 characters</span></span>|<span data-ttu-id="df016-274">✔</span><span class="sxs-lookup"><span data-stu-id="df016-274">✔</span></span>|<span data-ttu-id="df016-275">Уникальный идентификатор объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="df016-275">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="df016-276">String</span><span class="sxs-lookup"><span data-stu-id="df016-276">String</span></span>|<span data-ttu-id="df016-277">128 символов</span><span class="sxs-lookup"><span data-stu-id="df016-277">128 characters</span></span>|<span data-ttu-id="df016-278">✔</span><span class="sxs-lookup"><span data-stu-id="df016-278">✔</span></span>|<span data-ttu-id="df016-279">Отображаемое имя вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="df016-279">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="df016-280">String</span><span class="sxs-lookup"><span data-stu-id="df016-280">String</span></span>|<span data-ttu-id="df016-281">2048 символов</span><span class="sxs-lookup"><span data-stu-id="df016-281">2048 characters</span></span>|<span data-ttu-id="df016-282">✔</span><span class="sxs-lookup"><span data-stu-id="df016-282">✔</span></span>|<span data-ttu-id="df016-283">URL-адрес https://, указывающий на пользовательский интерфейс сущности, который будет отображаться в полотне Teams.</span><span class="sxs-lookup"><span data-stu-id="df016-283">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="df016-284">String</span><span class="sxs-lookup"><span data-stu-id="df016-284">String</span></span>|<span data-ttu-id="df016-285">2048 символов</span><span class="sxs-lookup"><span data-stu-id="df016-285">2048 characters</span></span>||<span data-ttu-id="df016-286">URL-адрес https://, указывающий, когда пользователь попытается просмотреть его в браузере.</span><span class="sxs-lookup"><span data-stu-id="df016-286">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="df016-287">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="df016-287">Array of enum</span></span>|<span data-ttu-id="df016-288">1 </span><span class="sxs-lookup"><span data-stu-id="df016-288">1</span></span>|<span data-ttu-id="df016-289">✔</span><span class="sxs-lookup"><span data-stu-id="df016-289">✔</span></span>|<span data-ttu-id="df016-290">В настоящее время статические вкладки поддерживают только `personal` область, что означает, что ее можно подготовить только в рамках личного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="df016-290">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

> [!NOTE]
> <span data-ttu-id="df016-291">Если на вкладках требуются контекстно зависимые сведения для отображения релевантного контента или для инициализации процесса проверки подлинности, *обратитесь к разделу* [Получение контекста для вкладки Microsoft Teams](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="df016-291">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="df016-292">Боты</span><span class="sxs-lookup"><span data-stu-id="df016-292">bots</span></span>

<span data-ttu-id="df016-293">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="df016-293">**Optional**</span></span>

<span data-ttu-id="df016-294">Определяет одноэлементное решение, а также дополнительные сведения, такие как свойства команды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="df016-294">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="df016-295">Объект является массивом ( &mdash; в настоящее время для каждого приложения допускается только один элемент "bot" для каждого приложения) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="df016-295">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="df016-296">Этот блок необходим только для решений, предоставляющих интерфейс Bot.</span><span class="sxs-lookup"><span data-stu-id="df016-296">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="df016-297">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-297">Name</span></span>| <span data-ttu-id="df016-298">Тип</span><span class="sxs-lookup"><span data-stu-id="df016-298">Type</span></span>| <span data-ttu-id="df016-299">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-299">Maximum size</span></span> | <span data-ttu-id="df016-300">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-300">Required</span></span> | <span data-ttu-id="df016-301">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-301">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="df016-302">Строка</span><span class="sxs-lookup"><span data-stu-id="df016-302">String</span></span>|<span data-ttu-id="df016-303">64 символа</span><span class="sxs-lookup"><span data-stu-id="df016-303">64 characters</span></span>|<span data-ttu-id="df016-304">✔</span><span class="sxs-lookup"><span data-stu-id="df016-304">✔</span></span>|<span data-ttu-id="df016-305">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="df016-305">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="df016-306">Это может быть так же, как и общий [идентификатор приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="df016-306">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="df016-307">Boolean</span><span class="sxs-lookup"><span data-stu-id="df016-307">Boolean</span></span>|||<span data-ttu-id="df016-308">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="df016-308">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="df016-309">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="df016-309">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="df016-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="df016-310">Boolean</span></span>|||<span data-ttu-id="df016-311">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="df016-311">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="df016-312">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="df016-312">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="df016-313">Логический</span><span class="sxs-lookup"><span data-stu-id="df016-313">Boolean</span></span>|||<span data-ttu-id="df016-314">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="df016-314">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="df016-315">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="df016-315">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="df016-316">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="df016-316">Array of enum</span></span>|<span data-ttu-id="df016-317">4</span><span class="sxs-lookup"><span data-stu-id="df016-317">3</span></span>|<span data-ttu-id="df016-318">✔</span><span class="sxs-lookup"><span data-stu-id="df016-318">✔</span></span>|<span data-ttu-id="df016-319">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="df016-319">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="df016-320">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="df016-320">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="df016-321">Боты. Коммандлистс</span><span class="sxs-lookup"><span data-stu-id="df016-321">bots.commandLists</span></span>

<span data-ttu-id="df016-322">Необязательный список команд, которые ваш робот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="df016-322">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="df016-323">Объект является массивом (не более 2 элементов) со всеми элементами типа `object` ; необходимо определить отдельный список команд для каждой области, которую поддерживает Bot.</span><span class="sxs-lookup"><span data-stu-id="df016-323">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="df016-324">Дополнительные сведения содержатся в [меню Bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="df016-324">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="df016-325">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-325">Name</span></span>| <span data-ttu-id="df016-326">Тип</span><span class="sxs-lookup"><span data-stu-id="df016-326">Type</span></span>| <span data-ttu-id="df016-327">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-327">Maximum size</span></span> | <span data-ttu-id="df016-328">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-328">Required</span></span> | <span data-ttu-id="df016-329">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-329">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="df016-330">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="df016-330">array of enum</span></span>|<span data-ttu-id="df016-331">4</span><span class="sxs-lookup"><span data-stu-id="df016-331">3</span></span>|<span data-ttu-id="df016-332">✔</span><span class="sxs-lookup"><span data-stu-id="df016-332">✔</span></span>|<span data-ttu-id="df016-333">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="df016-333">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="df016-334">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="df016-334">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="df016-335">массив объектов</span><span class="sxs-lookup"><span data-stu-id="df016-335">array of objects</span></span>|<span data-ttu-id="df016-336">10 </span><span class="sxs-lookup"><span data-stu-id="df016-336">10</span></span>|<span data-ttu-id="df016-337">✔</span><span class="sxs-lookup"><span data-stu-id="df016-337">✔</span></span>|<span data-ttu-id="df016-338">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="df016-338">An array of commands the bot supports:</span></span><br><span data-ttu-id="df016-339">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="df016-339">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="df016-340">`description`: простое описание или пример синтаксиса команды и ее аргумента (строка, 128)</span><span class="sxs-lookup"><span data-stu-id="df016-340">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="df016-341">аудиовыход</span><span class="sxs-lookup"><span data-stu-id="df016-341">connectors</span></span>

<span data-ttu-id="df016-342">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="df016-342">**Optional**</span></span>

<span data-ttu-id="df016-343">`connectors`Блок определяет соединитель Office 365 для приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-343">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="df016-344">Объект является массивом (не более 1 элемента) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="df016-344">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="df016-345">Этот блок необходим только для решений, предоставляющих соединитель.</span><span class="sxs-lookup"><span data-stu-id="df016-345">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="df016-346">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-346">Name</span></span>| <span data-ttu-id="df016-347">Тип</span><span class="sxs-lookup"><span data-stu-id="df016-347">Type</span></span>| <span data-ttu-id="df016-348">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-348">Maximum size</span></span> | <span data-ttu-id="df016-349">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-349">Required</span></span> | <span data-ttu-id="df016-350">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-350">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="df016-351">String</span><span class="sxs-lookup"><span data-stu-id="df016-351">String</span></span>|<span data-ttu-id="df016-352">2048 символов</span><span class="sxs-lookup"><span data-stu-id="df016-352">2048 characters</span></span>|<span data-ttu-id="df016-353">✔</span><span class="sxs-lookup"><span data-stu-id="df016-353">✔</span></span>|<span data-ttu-id="df016-354">URL-адрес https://, используемый при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="df016-354">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="df016-355">Строка</span><span class="sxs-lookup"><span data-stu-id="df016-355">String</span></span>|<span data-ttu-id="df016-356">64 символа</span><span class="sxs-lookup"><span data-stu-id="df016-356">64 characters</span></span>|<span data-ttu-id="df016-357">✔</span><span class="sxs-lookup"><span data-stu-id="df016-357">✔</span></span>|<span data-ttu-id="df016-358">Уникальный идентификатор соединителя, который соответствует ИДЕНТИФИКАТОРу в [панели мониторинга разработчика соединителей](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="df016-358">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="df016-359">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="df016-359">Array of enum</span></span>|<span data-ttu-id="df016-360">1 </span><span class="sxs-lookup"><span data-stu-id="df016-360">1</span></span>|<span data-ttu-id="df016-361">✔</span><span class="sxs-lookup"><span data-stu-id="df016-361">✔</span></span>|<span data-ttu-id="df016-362">Указывает, будет ли соединитель работать в контексте канала в `team` или в интерфейсе для отдельного пользователя ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="df016-362">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="df016-363">В настоящее время `team` поддерживается только область действия.</span><span class="sxs-lookup"><span data-stu-id="df016-363">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="df016-364">компосикстенсионс</span><span class="sxs-lookup"><span data-stu-id="df016-364">composeExtensions</span></span>

<span data-ttu-id="df016-365">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="df016-365">**Optional**</span></span>

<span data-ttu-id="df016-366">Определяет расширение системы обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-366">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="df016-367">Имя компонента изменилось с "расширение составления" на "расширение обмена сообщениями" в ноябре 2017, но имя манифеста остается без изменений, поэтому все существующие расширения продолжают работать.</span><span class="sxs-lookup"><span data-stu-id="df016-367">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="df016-368">Объект является массивом (не более 1 элемента) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="df016-368">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="df016-369">Этот блок необходим только для решений, предоставляющих расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="df016-369">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="df016-370">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-370">Name</span></span>| <span data-ttu-id="df016-371">Тип</span><span class="sxs-lookup"><span data-stu-id="df016-371">Type</span></span> | <span data-ttu-id="df016-372">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-372">Maximum Size</span></span> | <span data-ttu-id="df016-373">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-373">Required</span></span> | <span data-ttu-id="df016-374">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-374">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="df016-375">String</span><span class="sxs-lookup"><span data-stu-id="df016-375">String</span></span>|<span data-ttu-id="df016-376">64</span><span class="sxs-lookup"><span data-stu-id="df016-376">64</span></span>|<span data-ttu-id="df016-377">✔</span><span class="sxs-lookup"><span data-stu-id="df016-377">✔</span></span>|<span data-ttu-id="df016-378">Уникальный идентификатор приложения для ленты, который выполняет резервное копирование расширения обмена сообщениями, как зарегистрировано в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="df016-378">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="df016-379">Это может быть так же, как и общий идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-379">This may well be the same as the overall App ID.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="df016-380">Boolean</span><span class="sxs-lookup"><span data-stu-id="df016-380">Boolean</span></span>|||<span data-ttu-id="df016-381">Значение, указывающее, может ли пользователь изменять конфигурацию расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="df016-381">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="df016-382">Значение по умолчанию: `false` .</span><span class="sxs-lookup"><span data-stu-id="df016-382">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="df016-383">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="df016-383">Array of object</span></span>|<span data-ttu-id="df016-384">10 </span><span class="sxs-lookup"><span data-stu-id="df016-384">10</span></span>|<span data-ttu-id="df016-385">✔</span><span class="sxs-lookup"><span data-stu-id="df016-385">✔</span></span>|<span data-ttu-id="df016-386">Массив команд, поддерживающих расширение системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="df016-386">Array of commands the messaging extension supports</span></span>|
|`messageHandlers`|<span data-ttu-id="df016-387">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="df016-387">Array of Objects</span></span>|<span data-ttu-id="df016-388">5 </span><span class="sxs-lookup"><span data-stu-id="df016-388">5</span></span>||<span data-ttu-id="df016-389">Список обработчиков, позволяющих вызывать приложения при выполнении определенных условий.</span><span class="sxs-lookup"><span data-stu-id="df016-389">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="df016-390">Домены также должны быть перечислены в`validDomains`</span><span class="sxs-lookup"><span data-stu-id="df016-390">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="df016-391">String</span><span class="sxs-lookup"><span data-stu-id="df016-391">String</span></span>|||<span data-ttu-id="df016-392">Тип обработчика сообщений.</span><span class="sxs-lookup"><span data-stu-id="df016-392">The type of message handler.</span></span> <span data-ttu-id="df016-393">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="df016-393">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="df016-394">Массив строк</span><span class="sxs-lookup"><span data-stu-id="df016-394">Array of Strings</span></span>|||<span data-ttu-id="df016-395">Массив доменов, для которых может регистрироваться обработчик сообщений ссылки.</span><span class="sxs-lookup"><span data-stu-id="df016-395">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="df016-396">Компосикстенсионс. Commands</span><span class="sxs-lookup"><span data-stu-id="df016-396">composeExtensions.commands</span></span>

<span data-ttu-id="df016-397">Ваш модуль обмена сообщениями должен объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="df016-397">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="df016-398">Каждая команда отображается в Microsoft Teams в качестве потенциального взаимодействия от точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="df016-398">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="df016-399">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="df016-399">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="df016-400">Каждый элемент команды представляет собой объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="df016-400">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="df016-401">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-401">Name</span></span>| <span data-ttu-id="df016-402">Тип</span><span class="sxs-lookup"><span data-stu-id="df016-402">Type</span></span>| <span data-ttu-id="df016-403">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-403">Maximum size</span></span> | <span data-ttu-id="df016-404">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-404">Required</span></span> | <span data-ttu-id="df016-405">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-405">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="df016-406">Строка</span><span class="sxs-lookup"><span data-stu-id="df016-406">String</span></span>|<span data-ttu-id="df016-407">64 символа</span><span class="sxs-lookup"><span data-stu-id="df016-407">64 characters</span></span>|<span data-ttu-id="df016-408">✔</span><span class="sxs-lookup"><span data-stu-id="df016-408">✔</span></span>|<span data-ttu-id="df016-409">Идентификатор команды</span><span class="sxs-lookup"><span data-stu-id="df016-409">The ID for the command</span></span>|
|`type`|<span data-ttu-id="df016-410">Строка</span><span class="sxs-lookup"><span data-stu-id="df016-410">String</span></span>|<span data-ttu-id="df016-411">64 символа</span><span class="sxs-lookup"><span data-stu-id="df016-411">64 characters</span></span>||<span data-ttu-id="df016-412">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="df016-412">Type of the command.</span></span> <span data-ttu-id="df016-413">Один из `query` или `action` .</span><span class="sxs-lookup"><span data-stu-id="df016-413">One of `query` or `action`.</span></span> <span data-ttu-id="df016-414">Умолчани`query`</span><span class="sxs-lookup"><span data-stu-id="df016-414">Default: `query`</span></span>|
|`title`|<span data-ttu-id="df016-415">String</span><span class="sxs-lookup"><span data-stu-id="df016-415">String</span></span>|<span data-ttu-id="df016-416">32 символов</span><span class="sxs-lookup"><span data-stu-id="df016-416">32 characters</span></span>|<span data-ttu-id="df016-417">✔</span><span class="sxs-lookup"><span data-stu-id="df016-417">✔</span></span>|<span data-ttu-id="df016-418">Понятное имя команды</span><span class="sxs-lookup"><span data-stu-id="df016-418">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="df016-419">String</span><span class="sxs-lookup"><span data-stu-id="df016-419">String</span></span>|<span data-ttu-id="df016-420">128 символов</span><span class="sxs-lookup"><span data-stu-id="df016-420">128 characters</span></span>||<span data-ttu-id="df016-421">Описание, которое отображается пользователям для указания цели этой команды</span><span class="sxs-lookup"><span data-stu-id="df016-421">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="df016-422">Boolean</span><span class="sxs-lookup"><span data-stu-id="df016-422">Boolean</span></span>|||<span data-ttu-id="df016-423">Логическое значение, которое указывает, следует ли выполнять команду изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="df016-423">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="df016-424">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="df016-424">Default: `false`</span></span>|
|`context`|<span data-ttu-id="df016-425">Массив строк</span><span class="sxs-lookup"><span data-stu-id="df016-425">Array of Strings</span></span>|<span data-ttu-id="df016-426">4</span><span class="sxs-lookup"><span data-stu-id="df016-426">3</span></span>||<span data-ttu-id="df016-427">Определяет, откуда можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="df016-427">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="df016-428">Любое сочетание `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="df016-428">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="df016-429">Значение по умолчанию:`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="df016-429">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="df016-430">Boolean</span><span class="sxs-lookup"><span data-stu-id="df016-430">Boolean</span></span>|||<span data-ttu-id="df016-431">Логическое значение, указывающее, должен ли он динамически получать модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="df016-431">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="df016-432">Объект</span><span class="sxs-lookup"><span data-stu-id="df016-432">Object</span></span>|||<span data-ttu-id="df016-433">Указание модуля задач для предварительной загрузки при использовании команды расширения системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="df016-433">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="df016-434">String</span><span class="sxs-lookup"><span data-stu-id="df016-434">String</span></span>|<span data-ttu-id="df016-435">64</span><span class="sxs-lookup"><span data-stu-id="df016-435">64</span></span>||<span data-ttu-id="df016-436">Заголовок начального диалогового окна</span><span class="sxs-lookup"><span data-stu-id="df016-436">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="df016-437">String</span><span class="sxs-lookup"><span data-stu-id="df016-437">String</span></span>|||<span data-ttu-id="df016-438">Ширина диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый"</span><span class="sxs-lookup"><span data-stu-id="df016-438">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="df016-439">String</span><span class="sxs-lookup"><span data-stu-id="df016-439">String</span></span>|||<span data-ttu-id="df016-440">Высота диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый"</span><span class="sxs-lookup"><span data-stu-id="df016-440">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="df016-441">String</span><span class="sxs-lookup"><span data-stu-id="df016-441">String</span></span>|||<span data-ttu-id="df016-442">Исходный URL-адрес вебвиев</span><span class="sxs-lookup"><span data-stu-id="df016-442">Initial webview URL</span></span>|
|`parameters`|<span data-ttu-id="df016-443">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="df016-443">Array of object</span></span>|<span data-ttu-id="df016-444">5 </span><span class="sxs-lookup"><span data-stu-id="df016-444">5</span></span>|<span data-ttu-id="df016-445">✔</span><span class="sxs-lookup"><span data-stu-id="df016-445">✔</span></span>|<span data-ttu-id="df016-446">Список параметров, которые выполняет команда.</span><span class="sxs-lookup"><span data-stu-id="df016-446">The list of parameters the command takes.</span></span> <span data-ttu-id="df016-447">Минимум: 1; максимум: 5</span><span class="sxs-lookup"><span data-stu-id="df016-447">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="df016-448">Строка</span><span class="sxs-lookup"><span data-stu-id="df016-448">String</span></span>|<span data-ttu-id="df016-449">64 символа</span><span class="sxs-lookup"><span data-stu-id="df016-449">64 characters</span></span>|<span data-ttu-id="df016-450">✔</span><span class="sxs-lookup"><span data-stu-id="df016-450">✔</span></span>|<span data-ttu-id="df016-451">Имя параметра в том виде, в котором оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="df016-451">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="df016-452">Он включен в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="df016-452">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="df016-453">String</span><span class="sxs-lookup"><span data-stu-id="df016-453">String</span></span>|<span data-ttu-id="df016-454">32 символов</span><span class="sxs-lookup"><span data-stu-id="df016-454">32 characters</span></span>|<span data-ttu-id="df016-455">✔</span><span class="sxs-lookup"><span data-stu-id="df016-455">✔</span></span>|<span data-ttu-id="df016-456">Удобное для пользователя название параметра.</span><span class="sxs-lookup"><span data-stu-id="df016-456">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="df016-457">String</span><span class="sxs-lookup"><span data-stu-id="df016-457">String</span></span>|<span data-ttu-id="df016-458">128 символов</span><span class="sxs-lookup"><span data-stu-id="df016-458">128 characters</span></span>||<span data-ttu-id="df016-459">Понятная пользователю строка, описывающая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="df016-459">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="df016-460">String</span><span class="sxs-lookup"><span data-stu-id="df016-460">String</span></span>|<span data-ttu-id="df016-461">128 символов</span><span class="sxs-lookup"><span data-stu-id="df016-461">128 characters</span></span>||<span data-ttu-id="df016-462">Определяет тип элемента управления, отображаемого в модуле задачи для `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="df016-462">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="df016-463">Один из `text` ,,,,, `textarea` `number` `date` `time` `toggle` ,`choiceset`</span><span class="sxs-lookup"><span data-stu-id="df016-463">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="df016-464">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="df016-464">Array of Objects</span></span>|<span data-ttu-id="df016-465">10 </span><span class="sxs-lookup"><span data-stu-id="df016-465">10</span></span>||<span data-ttu-id="df016-466">Варианты выбора для `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="df016-466">The choice options for the `choiceset`.</span></span> <span data-ttu-id="df016-467">Используйте только в том случае `parameter.inputType` , если`choiceset`</span><span class="sxs-lookup"><span data-stu-id="df016-467">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="df016-468">String</span><span class="sxs-lookup"><span data-stu-id="df016-468">String</span></span>|<span data-ttu-id="df016-469">128</span><span class="sxs-lookup"><span data-stu-id="df016-469">128</span></span>||<span data-ttu-id="df016-470">Название варианта</span><span class="sxs-lookup"><span data-stu-id="df016-470">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="df016-471">String</span><span class="sxs-lookup"><span data-stu-id="df016-471">String</span></span>|<span data-ttu-id="df016-472">512</span><span class="sxs-lookup"><span data-stu-id="df016-472">512</span></span>||<span data-ttu-id="df016-473">Выбор значения</span><span class="sxs-lookup"><span data-stu-id="df016-473">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="df016-474">permissions</span><span class="sxs-lookup"><span data-stu-id="df016-474">permissions</span></span>

<span data-ttu-id="df016-475">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="df016-475">**Optional**</span></span>

<span data-ttu-id="df016-476">Массив, `string` определяющий, какие разрешения запрашиваются приложением, что позволяет конечным пользователям знать, как будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="df016-476">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="df016-477">Следующие параметры неисключительны:</span><span class="sxs-lookup"><span data-stu-id="df016-477">The following options are non-exclusive:</span></span>

* <span data-ttu-id="df016-478">`identity`&emsp;Требуются сведения об удостоверении пользователя</span><span class="sxs-lookup"><span data-stu-id="df016-478">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="df016-479">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений участникам группы</span><span class="sxs-lookup"><span data-stu-id="df016-479">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="df016-480">Изменение этих разрешений при обновлении приложения приводит к тому, что пользователи будут повторять процесс разрешения при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-480">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="df016-481">Дополнительные сведения см. [в разделе Обновление приложения](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) .</span><span class="sxs-lookup"><span data-stu-id="df016-481">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="df016-482">девицепермиссионс</span><span class="sxs-lookup"><span data-stu-id="df016-482">devicePermissions</span></span>

<span data-ttu-id="df016-483">**Необязательное требование** Массив строк</span><span class="sxs-lookup"><span data-stu-id="df016-483">**Optional** Array of Strings</span></span>

<span data-ttu-id="df016-484">Указывает собственные функции на устройстве пользователя, к которым приложение может запрашивать доступ.</span><span class="sxs-lookup"><span data-stu-id="df016-484">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="df016-485">Возможные варианты:</span><span class="sxs-lookup"><span data-stu-id="df016-485">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="df016-486">валиддомаинс</span><span class="sxs-lookup"><span data-stu-id="df016-486">validDomains</span></span>

<span data-ttu-id="df016-487">**Необязательно**, за исключением **обязательного** места, где отмечено</span><span class="sxs-lookup"><span data-stu-id="df016-487">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="df016-488">Список допустимых доменов для веб-сайтов, которые приложение ожидает загружать в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="df016-488">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="df016-489">Примеры доменов могут включать подстановочные знаки `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="df016-489">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="df016-490">Это соответствует только одному сегменту домена; Если вам нужно использовать этот параметр `a.b.example.com` `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="df016-490">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="df016-491">Если конфигурация вкладки или контентный пользовательский интерфейс должны перейти к любому другому домену, Кроме того, что используется для настройки вкладок, этот домен необходимо указать здесь.</span><span class="sxs-lookup"><span data-stu-id="df016-491">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="df016-492">Тем не менее, **не** нужно включать домены поставщиков удостоверений, которые требуется поддерживать в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="df016-492">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="df016-493">Например, для проверки подлинности с помощью идентификатора Google необходимо перенаправить на accounts.google.com, но не следует включать accounts.google.com в `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="df016-493">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="df016-494">Приложения Teams, которым для правильной работы требуются собственные URL-адреса SharePoint, могут содержать "{теамситедомаин}" в допустимом списке доменов.</span><span class="sxs-lookup"><span data-stu-id="df016-494">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df016-495">Не добавляйте домены за предельный элемент управления (напрямую или с помощью подстановочных знаков).</span><span class="sxs-lookup"><span data-stu-id="df016-495">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="df016-496">Например, `yourapp.onmicrosoft.com` является допустимым, но `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="df016-496">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="df016-497">Объект является массивом со всеми элементами типа `string` .</span><span class="sxs-lookup"><span data-stu-id="df016-497">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="df016-498">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="df016-498">webApplicationInfo</span></span>

<span data-ttu-id="df016-499">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="df016-499">**Optional**</span></span>

<span data-ttu-id="df016-500">Указание идентификатора приложения и графического объекта AAD для упрощения входа пользователей в приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="df016-500">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="df016-501">Имя</span><span class="sxs-lookup"><span data-stu-id="df016-501">Name</span></span>| <span data-ttu-id="df016-502">Тип</span><span class="sxs-lookup"><span data-stu-id="df016-502">Type</span></span>| <span data-ttu-id="df016-503">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="df016-503">Maximum size</span></span> | <span data-ttu-id="df016-504">Обязательный</span><span class="sxs-lookup"><span data-stu-id="df016-504">Required</span></span> | <span data-ttu-id="df016-505">Описание</span><span class="sxs-lookup"><span data-stu-id="df016-505">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="df016-506">String</span><span class="sxs-lookup"><span data-stu-id="df016-506">String</span></span>|<span data-ttu-id="df016-507">36 символов</span><span class="sxs-lookup"><span data-stu-id="df016-507">36 characters</span></span>|<span data-ttu-id="df016-508">✔</span><span class="sxs-lookup"><span data-stu-id="df016-508">✔</span></span>|<span data-ttu-id="df016-509">Идентификатор приложения AAD приложения.</span><span class="sxs-lookup"><span data-stu-id="df016-509">AAD application id of the app.</span></span> <span data-ttu-id="df016-510">Этот идентификатор должен быть идентификатором GUID.</span><span class="sxs-lookup"><span data-stu-id="df016-510">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="df016-511">String</span><span class="sxs-lookup"><span data-stu-id="df016-511">String</span></span>|<span data-ttu-id="df016-512">2048 символов</span><span class="sxs-lookup"><span data-stu-id="df016-512">2048 characters</span></span>|<span data-ttu-id="df016-513">✔</span><span class="sxs-lookup"><span data-stu-id="df016-513">✔</span></span>|<span data-ttu-id="df016-514">URL-адрес ресурса приложения для получения маркера проверки подлинности для единого входа.</span><span class="sxs-lookup"><span data-stu-id="df016-514">Resource url of app for acquiring auth token for SSO.</span></span>|
