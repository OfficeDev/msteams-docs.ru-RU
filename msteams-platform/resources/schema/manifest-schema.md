---
title: Справочник по схеме манифеста
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams.
keywords: Схема манифеста Teams
ms.openlocfilehash: 1a1a690e6e382dcad3ceb200ec02286e8c9171f8
ms.sourcegitcommit: 060b486c38b72a3e6b63b4d617b759174082a508
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2020
ms.locfileid: "41953490"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="8cc79-104">Ссылка: схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8cc79-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="8cc79-105">Манифест Microsoft Teams описывает, как приложение интегрируется в продукт Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8cc79-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="8cc79-106">Манифест должен соответствовать схеме, размещенной в [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span><span class="sxs-lookup"><span data-stu-id="8cc79-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="8cc79-107">Также поддерживаются предыдущие версии 1.0-1.4 (в URL-адресе используется "v1. x").</span><span class="sxs-lookup"><span data-stu-id="8cc79-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="8cc79-108">В приведенном ниже примере схемы показаны все варианты расширения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="8cc79-109">Пример полного манифеста</span><span class="sxs-lookup"><span data-stu-id="8cc79-109">Sample full manifest</span></span>

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

<span data-ttu-id="8cc79-110">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="8cc79-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="8cc79-111">$schema</span><span class="sxs-lookup"><span data-stu-id="8cc79-111">$schema</span></span>

<span data-ttu-id="8cc79-112">*Необязательная, но рекомендуемая* &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="8cc79-112">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="8cc79-113">URL-адрес https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="8cc79-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="8cc79-114">Версия манифеста</span><span class="sxs-lookup"><span data-stu-id="8cc79-114">manifestVersion</span></span>

<span data-ttu-id="8cc79-115">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="8cc79-115">**Required** &ndash; String</span></span>

<span data-ttu-id="8cc79-116">Версия схемы манифеста, используемая манифестом.</span><span class="sxs-lookup"><span data-stu-id="8cc79-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="8cc79-117">Он должен иметь значения "1,5".</span><span class="sxs-lookup"><span data-stu-id="8cc79-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="8cc79-118">version</span><span class="sxs-lookup"><span data-stu-id="8cc79-118">version</span></span>

<span data-ttu-id="8cc79-119">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="8cc79-119">**Required** &ndash; String</span></span>

<span data-ttu-id="8cc79-120">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-120">The version of the specific app.</span></span> <span data-ttu-id="8cc79-121">Если вы обновите какой-либо элемент в манифесте, необходимо также увеличить номер версии.</span><span class="sxs-lookup"><span data-stu-id="8cc79-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="8cc79-122">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="8cc79-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="8cc79-123">Если это приложение было отправлено в хранилище, новый манифест необходимо будет повторно отправить и проверить повторно.</span><span class="sxs-lookup"><span data-stu-id="8cc79-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="8cc79-124">После этого пользователи этого приложения автоматически получат новый обновленный манифест в течение нескольких часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="8cc79-125">Если приложение запросило изменение разрешений, пользователям будет предложено выполнить обновление и повторное согласие на доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="8cc79-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="8cc79-126">Эта строка версии должна соответствовать стандарту [semver](http://semver.org/) (Major. Значительные. PATCH).</span><span class="sxs-lookup"><span data-stu-id="8cc79-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="8cc79-127">id</span><span class="sxs-lookup"><span data-stu-id="8cc79-127">id</span></span>

<span data-ttu-id="8cc79-128">**Обязательный** &ndash; идентификатор приложения Microsoft</span><span class="sxs-lookup"><span data-stu-id="8cc79-128">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="8cc79-129">Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="8cc79-130">Если вы зарегистрировали Bot с помощью Microsoft Bot Framework, или веб-приложение вашей вкладки уже входит в Microsoft, у вас уже должен быть идентификатор, и его следует ввести здесь.</span><span class="sxs-lookup"><span data-stu-id="8cc79-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="8cc79-131">В противном случае необходимо создать новый идентификатор на портале регистрации приложений ([Мои приложения](https://apps.dev.microsoft.com)) Майкрософт, ввести его здесь, а затем повторно использовать его при добавлении ленты. Note: Если вы отправляете обновление существующему приложению в AppSource, идентификатор в манифесте не должен изменяться.</span><span class="sxs-lookup"><span data-stu-id="8cc79-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="packagename"></a><span data-ttu-id="8cc79-132">паккаженаме</span><span class="sxs-lookup"><span data-stu-id="8cc79-132">packageName</span></span>

<span data-ttu-id="8cc79-133">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="8cc79-133">**Required** &ndash; String</span></span>

<span data-ttu-id="8cc79-134">Уникальный идентификатор для этого приложения в обратной нотации домена; Пример: com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="8cc79-134">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="8cc79-135">developer</span><span class="sxs-lookup"><span data-stu-id="8cc79-135">developer</span></span>

<span data-ttu-id="8cc79-136">**Required**</span><span class="sxs-lookup"><span data-stu-id="8cc79-136">**Required**</span></span>

<span data-ttu-id="8cc79-137">Указывает сведения о компании.</span><span class="sxs-lookup"><span data-stu-id="8cc79-137">Specifies information about your company.</span></span> <span data-ttu-id="8cc79-138">Для приложений, отправляемых в AppSource (ранее — магазин Office), эти значения должны быть сопоставлены со сведениями в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="8cc79-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="8cc79-139">Ознакомьтесь с нашими [рекомендациями по публикации](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="8cc79-139">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="8cc79-140">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-140">Name</span></span>| <span data-ttu-id="8cc79-141">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-141">Maximum size</span></span> | <span data-ttu-id="8cc79-142">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-142">Required</span></span> | <span data-ttu-id="8cc79-143">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="8cc79-144">32 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-144">32 characters</span></span>|<span data-ttu-id="8cc79-145">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-145">✔</span></span>|<span data-ttu-id="8cc79-146">Отображаемое имя разработчика.</span><span class="sxs-lookup"><span data-stu-id="8cc79-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="8cc79-147">2048 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-147">2048 characters</span></span>|<span data-ttu-id="8cc79-148">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-148">✔</span></span>|<span data-ttu-id="8cc79-149">URL-адрес https://на веб-сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="8cc79-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="8cc79-150">Эта ссылка должна принять участие у пользователей в вашей компании или целевой странице для конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="8cc79-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="8cc79-151">2048 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-151">2048 characters</span></span>|<span data-ttu-id="8cc79-152">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-152">✔</span></span>|<span data-ttu-id="8cc79-153">URL-адрес https://для политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="8cc79-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="8cc79-154">2048 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-154">2048 characters</span></span>|<span data-ttu-id="8cc79-155">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-155">✔</span></span>|<span data-ttu-id="8cc79-156">URL-адрес https://для условий использования разработчиком.</span><span class="sxs-lookup"><span data-stu-id="8cc79-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="8cc79-157">10 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-157">10 characters</span></span>| |<span data-ttu-id="8cc79-158">**Необязательное требование** Идентификатор сети партнера Майкрософт, определяющий партнерскую организацию, которая создает приложение.</span><span class="sxs-lookup"><span data-stu-id="8cc79-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="8cc79-159">локализатионинфо</span><span class="sxs-lookup"><span data-stu-id="8cc79-159">localizationInfo</span></span>

<span data-ttu-id="8cc79-160">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="8cc79-160">**Optional**</span></span>

<span data-ttu-id="8cc79-161">Разрешает спецификацию языка по умолчанию, а также указателей на дополнительные языковые файлы.</span><span class="sxs-lookup"><span data-stu-id="8cc79-161">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="8cc79-162">См.: [Локализация](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="8cc79-162">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="8cc79-163">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-163">Name</span></span>| <span data-ttu-id="8cc79-164">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-164">Maximum size</span></span> | <span data-ttu-id="8cc79-165">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-165">Required</span></span> | <span data-ttu-id="8cc79-166">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-166">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="8cc79-167">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-167">✔</span></span>|<span data-ttu-id="8cc79-168">Тег языка строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="8cc79-168">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="8cc79-169">Локализатионинфо. Аддитионаллангуажес</span><span class="sxs-lookup"><span data-stu-id="8cc79-169">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="8cc79-170">Массив объектов, задающий дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="8cc79-170">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="8cc79-171">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-171">Name</span></span>| <span data-ttu-id="8cc79-172">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-172">Maximum size</span></span> | <span data-ttu-id="8cc79-173">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-173">Required</span></span> | <span data-ttu-id="8cc79-174">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-174">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="8cc79-175">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-175">✔</span></span>|<span data-ttu-id="8cc79-176">Тег языка строк в указанном файле.</span><span class="sxs-lookup"><span data-stu-id="8cc79-176">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="8cc79-177">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-177">✔</span></span>|<span data-ttu-id="8cc79-178">Относительный путь к файлу. JSON, содержащему переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="8cc79-178">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="8cc79-179">name</span><span class="sxs-lookup"><span data-stu-id="8cc79-179">name</span></span>

<span data-ttu-id="8cc79-180">**Required**</span><span class="sxs-lookup"><span data-stu-id="8cc79-180">**Required**</span></span>

<span data-ttu-id="8cc79-181">Имя приложения, отображаемое для пользователей в интерфейсе Teams.</span><span class="sxs-lookup"><span data-stu-id="8cc79-181">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="8cc79-182">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="8cc79-182">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="8cc79-183">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="8cc79-183">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="8cc79-184">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-184">Name</span></span>| <span data-ttu-id="8cc79-185">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-185">Maximum size</span></span> | <span data-ttu-id="8cc79-186">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-186">Required</span></span> | <span data-ttu-id="8cc79-187">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-187">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="8cc79-188">30 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-188">30 characters</span></span>|<span data-ttu-id="8cc79-189">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-189">✔</span></span>|<span data-ttu-id="8cc79-190">Краткое отображаемое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-190">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="8cc79-191">100 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-191">100 characters</span></span>||<span data-ttu-id="8cc79-192">Полное имя приложения, используемое, если имя полного приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="8cc79-192">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="8cc79-193">description</span><span class="sxs-lookup"><span data-stu-id="8cc79-193">description</span></span>

<span data-ttu-id="8cc79-194">**Required**</span><span class="sxs-lookup"><span data-stu-id="8cc79-194">**Required**</span></span>

<span data-ttu-id="8cc79-195">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="8cc79-195">Describes your app to users.</span></span> <span data-ttu-id="8cc79-196">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="8cc79-196">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="8cc79-197">Убедитесь, что ваше описание точно описывает ваш интерфейс и предоставляет сведения, помогающие потенциальным клиентам определить, что делает ваш интерфейс.</span><span class="sxs-lookup"><span data-stu-id="8cc79-197">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="8cc79-198">Кроме того, в полном описании следует отметить, если для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="8cc79-198">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="8cc79-199">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="8cc79-199">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="8cc79-200">Краткое описание не должно повторяться в длинном описании и не должно включать имя другого приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-200">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="8cc79-201">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-201">Name</span></span>| <span data-ttu-id="8cc79-202">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-202">Maximum size</span></span> | <span data-ttu-id="8cc79-203">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-203">Required</span></span> | <span data-ttu-id="8cc79-204">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-204">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="8cc79-205">80 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-205">80 characters</span></span>|<span data-ttu-id="8cc79-206">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-206">✔</span></span>|<span data-ttu-id="8cc79-207">Краткое описание интерфейса приложения, используемое при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="8cc79-207">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="8cc79-208">4000 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-208">4000 characters</span></span>|<span data-ttu-id="8cc79-209">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-209">✔</span></span>|<span data-ttu-id="8cc79-210">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-210">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="8cc79-211">icons</span><span class="sxs-lookup"><span data-stu-id="8cc79-211">icons</span></span>

<span data-ttu-id="8cc79-212">**Required**</span><span class="sxs-lookup"><span data-stu-id="8cc79-212">**Required**</span></span>

<span data-ttu-id="8cc79-213">Значки, используемые в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="8cc79-213">Icons used within the Teams app.</span></span> <span data-ttu-id="8cc79-214">Файлы значков должны быть включены в состав пакета отправки.</span><span class="sxs-lookup"><span data-stu-id="8cc79-214">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="8cc79-215">Дополнительные сведения можно найти в разделе [значки](~/concepts/build-and-test/apps-package.md#icons) .</span><span class="sxs-lookup"><span data-stu-id="8cc79-215">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="8cc79-216">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-216">Name</span></span>| <span data-ttu-id="8cc79-217">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-217">Maximum size</span></span> | <span data-ttu-id="8cc79-218">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-218">Required</span></span> | <span data-ttu-id="8cc79-219">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-219">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="8cc79-220">2048 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-220">2048 characters</span></span>|<span data-ttu-id="8cc79-221">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-221">✔</span></span>|<span data-ttu-id="8cc79-222">Относительный путь к файлу с прозрачным значком изображения в формате 32x32 PNG.</span><span class="sxs-lookup"><span data-stu-id="8cc79-222">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="8cc79-223">2048 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-223">2048 characters</span></span>|<span data-ttu-id="8cc79-224">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-224">✔</span></span>|<span data-ttu-id="8cc79-225">Относительный путь к файлу полного цветового значка PNG 192x192.</span><span class="sxs-lookup"><span data-stu-id="8cc79-225">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="8cc79-226">акцентколор</span><span class="sxs-lookup"><span data-stu-id="8cc79-226">accentColor</span></span>

<span data-ttu-id="8cc79-227">**Обязательная** &ndash; строка</span><span class="sxs-lookup"><span data-stu-id="8cc79-227">**Required** &ndash; String</span></span>

<span data-ttu-id="8cc79-228">Цвет, используемый в сочетании с фоном для значков структуры.</span><span class="sxs-lookup"><span data-stu-id="8cc79-228">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="8cc79-229">Значение должно быть допустимым цветом HTML-кода, начинающимся с "#", `#4464ee`например.</span><span class="sxs-lookup"><span data-stu-id="8cc79-229">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="8cc79-230">конфигураблетабс</span><span class="sxs-lookup"><span data-stu-id="8cc79-230">configurableTabs</span></span>

<span data-ttu-id="8cc79-231">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="8cc79-231">**Optional**</span></span>

<span data-ttu-id="8cc79-232">Используется, когда у вашего приложения есть вкладка "канал группы", требующая дополнительной настройки перед добавлением.</span><span class="sxs-lookup"><span data-stu-id="8cc79-232">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="8cc79-233">Настраиваемые вкладки поддерживаются только в области Teams, и в настоящее время поддерживается только одна вкладка для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-233">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="8cc79-234">Объект является массивом со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-234">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="8cc79-235">Этот блок необходим только для решений, которые предоставляют настраиваемое решение для вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="8cc79-235">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="8cc79-236">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-236">Name</span></span>| <span data-ttu-id="8cc79-237">Тип</span><span class="sxs-lookup"><span data-stu-id="8cc79-237">Type</span></span>| <span data-ttu-id="8cc79-238">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-238">Maximum size</span></span> | <span data-ttu-id="8cc79-239">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-239">Required</span></span> | <span data-ttu-id="8cc79-240">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-240">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="8cc79-241">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-241">String</span></span>|<span data-ttu-id="8cc79-242">2048 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-242">2048 characters</span></span>|<span data-ttu-id="8cc79-243">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-243">✔</span></span>|<span data-ttu-id="8cc79-244">URL-адрес https://, используемый при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="8cc79-244">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="8cc79-245">Boolean</span><span class="sxs-lookup"><span data-stu-id="8cc79-245">Boolean</span></span>|||<span data-ttu-id="8cc79-246">Значение, указывающее, может ли пользователь обновлять экземпляр конфигурации вкладки после создания.</span><span class="sxs-lookup"><span data-stu-id="8cc79-246">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="8cc79-247">Умолчани`true`</span><span class="sxs-lookup"><span data-stu-id="8cc79-247">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="8cc79-248">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="8cc79-248">Array of enum</span></span>|<span data-ttu-id="8cc79-249">1 </span><span class="sxs-lookup"><span data-stu-id="8cc79-249">1</span></span>|<span data-ttu-id="8cc79-250">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-250">✔</span></span>|<span data-ttu-id="8cc79-251">В настоящее время настраиваемые вкладки поддерживают только области `team` и `groupchat` области.</span><span class="sxs-lookup"><span data-stu-id="8cc79-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="8cc79-252">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-252">String</span></span>|<span data-ttu-id="8cc79-253">2048</span><span class="sxs-lookup"><span data-stu-id="8cc79-253">2048</span></span>||<span data-ttu-id="8cc79-254">Относительный путь к изображению вкладки для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8cc79-254">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="8cc79-255">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="8cc79-255">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="8cc79-256">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="8cc79-256">Array of enum</span></span>|<span data-ttu-id="8cc79-257">1 </span><span class="sxs-lookup"><span data-stu-id="8cc79-257">1</span></span>||<span data-ttu-id="8cc79-258">Определяет, как будет предоставляться вкладка в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8cc79-258">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="8cc79-259">`sharePointFullPage` Параметры`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="8cc79-259">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="8cc79-260">статиктабс</span><span class="sxs-lookup"><span data-stu-id="8cc79-260">staticTabs</span></span>

<span data-ttu-id="8cc79-261">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="8cc79-261">**Optional**</span></span>

<span data-ttu-id="8cc79-262">Определяет набор вкладок, которые по умолчанию можно закреплять, не добавляя пользователей вручную.</span><span class="sxs-lookup"><span data-stu-id="8cc79-262">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="8cc79-263">Статические вкладки, `personal` объявляемые в области, всегда фиксируются в личном интерфейсе приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-263">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="8cc79-264">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="8cc79-264">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="8cc79-265">Объект является массивом (не более 16 элементов) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-265">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="8cc79-266">Этот блок необходим только для решений, предоставляющих статическое решение для вкладок.</span><span class="sxs-lookup"><span data-stu-id="8cc79-266">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="8cc79-267">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-267">Name</span></span>| <span data-ttu-id="8cc79-268">Тип</span><span class="sxs-lookup"><span data-stu-id="8cc79-268">Type</span></span>| <span data-ttu-id="8cc79-269">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-269">Maximum size</span></span> | <span data-ttu-id="8cc79-270">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-270">Required</span></span> | <span data-ttu-id="8cc79-271">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-271">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="8cc79-272">Строка</span><span class="sxs-lookup"><span data-stu-id="8cc79-272">String</span></span>|<span data-ttu-id="8cc79-273">64 символа</span><span class="sxs-lookup"><span data-stu-id="8cc79-273">64 characters</span></span>|<span data-ttu-id="8cc79-274">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-274">✔</span></span>|<span data-ttu-id="8cc79-275">Уникальный идентификатор объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="8cc79-275">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="8cc79-276">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-276">String</span></span>|<span data-ttu-id="8cc79-277">128 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-277">128 characters</span></span>|<span data-ttu-id="8cc79-278">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-278">✔</span></span>|<span data-ttu-id="8cc79-279">Отображаемое имя вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="8cc79-279">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="8cc79-280">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-280">String</span></span>|<span data-ttu-id="8cc79-281">2048 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-281">2048 characters</span></span>|<span data-ttu-id="8cc79-282">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-282">✔</span></span>|<span data-ttu-id="8cc79-283">URL-адрес https://, указывающий на пользовательский интерфейс сущности, который будет отображаться в полотне Teams.</span><span class="sxs-lookup"><span data-stu-id="8cc79-283">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="8cc79-284">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-284">String</span></span>|<span data-ttu-id="8cc79-285">2048 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-285">2048 characters</span></span>||<span data-ttu-id="8cc79-286">URL-адрес https://, указывающий, когда пользователь попытается просмотреть его в браузере.</span><span class="sxs-lookup"><span data-stu-id="8cc79-286">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="8cc79-287">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="8cc79-287">Array of enum</span></span>|<span data-ttu-id="8cc79-288">1 </span><span class="sxs-lookup"><span data-stu-id="8cc79-288">1</span></span>|<span data-ttu-id="8cc79-289">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-289">✔</span></span>|<span data-ttu-id="8cc79-290">В настоящее время статические вкладки поддерживают `personal` только область, что означает, что ее можно подготовить только в рамках личного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="8cc79-290">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

> [!NOTE]
> <span data-ttu-id="8cc79-291">Если на вкладках требуются контекстно зависимые сведения для отображения релевантного контента или для инициализации процесса проверки подлинности, *обратитесь к разделу* [Получение контекста для вкладки Microsoft Teams](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="8cc79-291">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="8cc79-292">Боты</span><span class="sxs-lookup"><span data-stu-id="8cc79-292">bots</span></span>

<span data-ttu-id="8cc79-293">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="8cc79-293">**Optional**</span></span>

<span data-ttu-id="8cc79-294">Определяет одноэлементное решение, а также дополнительные сведения, такие как свойства команды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8cc79-294">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="8cc79-295">Объект является массивом (в настоящее время для каждого приложения&mdash;допускается только один элемент "bot" для каждого приложения) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-295">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="8cc79-296">Этот блок необходим только для решений, предоставляющих интерфейс Bot.</span><span class="sxs-lookup"><span data-stu-id="8cc79-296">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="8cc79-297">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-297">Name</span></span>| <span data-ttu-id="8cc79-298">Тип</span><span class="sxs-lookup"><span data-stu-id="8cc79-298">Type</span></span>| <span data-ttu-id="8cc79-299">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-299">Maximum size</span></span> | <span data-ttu-id="8cc79-300">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-300">Required</span></span> | <span data-ttu-id="8cc79-301">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-301">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="8cc79-302">Строка</span><span class="sxs-lookup"><span data-stu-id="8cc79-302">String</span></span>|<span data-ttu-id="8cc79-303">64 символа</span><span class="sxs-lookup"><span data-stu-id="8cc79-303">64 characters</span></span>|<span data-ttu-id="8cc79-304">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-304">✔</span></span>|<span data-ttu-id="8cc79-305">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="8cc79-305">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="8cc79-306">Это может быть так же, как и общий [идентификатор приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="8cc79-306">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="8cc79-307">Boolean</span><span class="sxs-lookup"><span data-stu-id="8cc79-307">Boolean</span></span>|||<span data-ttu-id="8cc79-308">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="8cc79-308">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="8cc79-309">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="8cc79-309">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="8cc79-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="8cc79-310">Boolean</span></span>|||<span data-ttu-id="8cc79-311">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="8cc79-311">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="8cc79-312">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="8cc79-312">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="8cc79-313">Логический</span><span class="sxs-lookup"><span data-stu-id="8cc79-313">Boolean</span></span>|||<span data-ttu-id="8cc79-314">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="8cc79-314">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="8cc79-315">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="8cc79-315">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="8cc79-316">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="8cc79-316">Array of enum</span></span>|<span data-ttu-id="8cc79-317">3 </span><span class="sxs-lookup"><span data-stu-id="8cc79-317">3</span></span>|<span data-ttu-id="8cc79-318">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-318">✔</span></span>|<span data-ttu-id="8cc79-319">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="8cc79-319">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="8cc79-320">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="8cc79-320">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="8cc79-321">Боты. Коммандлистс</span><span class="sxs-lookup"><span data-stu-id="8cc79-321">bots.commandLists</span></span>

<span data-ttu-id="8cc79-322">Необязательный список команд, которые ваш робот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="8cc79-322">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="8cc79-323">Объект является массивом (не более 2 элементов) со всеми элементами типа `object`; необходимо определить отдельный список команд для каждой области, которую поддерживает Bot.</span><span class="sxs-lookup"><span data-stu-id="8cc79-323">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="8cc79-324">Дополнительные сведения содержатся в [меню Bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="8cc79-324">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="8cc79-325">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-325">Name</span></span>| <span data-ttu-id="8cc79-326">Тип</span><span class="sxs-lookup"><span data-stu-id="8cc79-326">Type</span></span>| <span data-ttu-id="8cc79-327">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-327">Maximum size</span></span> | <span data-ttu-id="8cc79-328">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-328">Required</span></span> | <span data-ttu-id="8cc79-329">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-329">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="8cc79-330">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="8cc79-330">array of enum</span></span>|<span data-ttu-id="8cc79-331">3 </span><span class="sxs-lookup"><span data-stu-id="8cc79-331">3</span></span>|<span data-ttu-id="8cc79-332">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-332">✔</span></span>|<span data-ttu-id="8cc79-333">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="8cc79-333">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="8cc79-334">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-334">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="8cc79-335">массив объектов</span><span class="sxs-lookup"><span data-stu-id="8cc79-335">array of objects</span></span>|<span data-ttu-id="8cc79-336">10 </span><span class="sxs-lookup"><span data-stu-id="8cc79-336">10</span></span>|<span data-ttu-id="8cc79-337">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-337">✔</span></span>|<span data-ttu-id="8cc79-338">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="8cc79-338">An array of commands the bot supports:</span></span><br><span data-ttu-id="8cc79-339">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="8cc79-339">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="8cc79-340">`description`: простое описание или пример синтаксиса команды и ее аргумента (строка, 128)</span><span class="sxs-lookup"><span data-stu-id="8cc79-340">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="8cc79-341">аудиовыход</span><span class="sxs-lookup"><span data-stu-id="8cc79-341">connectors</span></span>

<span data-ttu-id="8cc79-342">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="8cc79-342">**Optional**</span></span>

<span data-ttu-id="8cc79-343">`connectors` Блок определяет соединитель Office 365 для приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-343">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="8cc79-344">Объект является массивом (не более 1 элемента) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-344">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="8cc79-345">Этот блок необходим только для решений, предоставляющих соединитель.</span><span class="sxs-lookup"><span data-stu-id="8cc79-345">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="8cc79-346">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-346">Name</span></span>| <span data-ttu-id="8cc79-347">Тип</span><span class="sxs-lookup"><span data-stu-id="8cc79-347">Type</span></span>| <span data-ttu-id="8cc79-348">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-348">Maximum size</span></span> | <span data-ttu-id="8cc79-349">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-349">Required</span></span> | <span data-ttu-id="8cc79-350">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-350">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="8cc79-351">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-351">String</span></span>|<span data-ttu-id="8cc79-352">2048 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-352">2048 characters</span></span>|<span data-ttu-id="8cc79-353">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-353">✔</span></span>|<span data-ttu-id="8cc79-354">URL-адрес https://, используемый при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="8cc79-354">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="8cc79-355">Строка</span><span class="sxs-lookup"><span data-stu-id="8cc79-355">String</span></span>|<span data-ttu-id="8cc79-356">64 символа</span><span class="sxs-lookup"><span data-stu-id="8cc79-356">64 characters</span></span>|<span data-ttu-id="8cc79-357">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-357">✔</span></span>|<span data-ttu-id="8cc79-358">Уникальный идентификатор соединителя, который соответствует ИДЕНТИФИКАТОРу в [панели мониторинга разработчика соединителей](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="8cc79-358">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="8cc79-359">Массив перечислений</span><span class="sxs-lookup"><span data-stu-id="8cc79-359">Array of enum</span></span>|<span data-ttu-id="8cc79-360">1 </span><span class="sxs-lookup"><span data-stu-id="8cc79-360">1</span></span>|<span data-ttu-id="8cc79-361">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-361">✔</span></span>|<span data-ttu-id="8cc79-362">Указывает `team`, будет ли соединитель работать в контексте канала в или в интерфейсе для отдельного пользователя (`personal`).</span><span class="sxs-lookup"><span data-stu-id="8cc79-362">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="8cc79-363">В настоящее время поддерживается `team` только область действия.</span><span class="sxs-lookup"><span data-stu-id="8cc79-363">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="8cc79-364">компосикстенсионс</span><span class="sxs-lookup"><span data-stu-id="8cc79-364">composeExtensions</span></span>

<span data-ttu-id="8cc79-365">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="8cc79-365">**Optional**</span></span>

<span data-ttu-id="8cc79-366">Определяет расширение системы обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-366">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="8cc79-367">Имя компонента изменилось с "расширение составления" на "расширение обмена сообщениями" в ноябре 2017, но имя манифеста остается без изменений, поэтому все существующие расширения продолжают работать.</span><span class="sxs-lookup"><span data-stu-id="8cc79-367">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="8cc79-368">Объект является массивом (не более 1 элемента) со всеми элементами типа `object`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-368">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="8cc79-369">Этот блок необходим только для решений, предоставляющих расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8cc79-369">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="8cc79-370">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-370">Name</span></span>| <span data-ttu-id="8cc79-371">Тип</span><span class="sxs-lookup"><span data-stu-id="8cc79-371">Type</span></span> | <span data-ttu-id="8cc79-372">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-372">Maximum Size</span></span> | <span data-ttu-id="8cc79-373">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-373">Required</span></span> | <span data-ttu-id="8cc79-374">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-374">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="8cc79-375">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-375">String</span></span>|<span data-ttu-id="8cc79-376">64</span><span class="sxs-lookup"><span data-stu-id="8cc79-376">64</span></span>|<span data-ttu-id="8cc79-377">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-377">✔</span></span>|<span data-ttu-id="8cc79-378">Уникальный идентификатор приложения для ленты, который выполняет резервное копирование расширения обмена сообщениями, как зарегистрировано в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="8cc79-378">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="8cc79-379">Это может быть так же, как и общий идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-379">This may well be the same as the overall App ID.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="8cc79-380">Boolean</span><span class="sxs-lookup"><span data-stu-id="8cc79-380">Boolean</span></span>|||<span data-ttu-id="8cc79-381">Значение, указывающее, может ли пользователь изменять конфигурацию расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8cc79-381">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="8cc79-382">Значение по умолчанию: `false`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-382">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="8cc79-383">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="8cc79-383">Array of object</span></span>|<span data-ttu-id="8cc79-384">10 </span><span class="sxs-lookup"><span data-stu-id="8cc79-384">10</span></span>|<span data-ttu-id="8cc79-385">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-385">✔</span></span>|<span data-ttu-id="8cc79-386">Массив команд, поддерживающих расширение системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="8cc79-386">Array of commands the messaging extension supports</span></span>|
|`messageHandlers`|<span data-ttu-id="8cc79-387">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="8cc79-387">Array of Objects</span></span>|<span data-ttu-id="8cc79-388">5 </span><span class="sxs-lookup"><span data-stu-id="8cc79-388">5</span></span>||<span data-ttu-id="8cc79-389">Список обработчиков, позволяющих вызывать приложения при выполнении определенных условий.</span><span class="sxs-lookup"><span data-stu-id="8cc79-389">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="8cc79-390">Домены также должны быть перечислены в`validDomains`</span><span class="sxs-lookup"><span data-stu-id="8cc79-390">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="8cc79-391">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-391">String</span></span>|||<span data-ttu-id="8cc79-392">Тип обработчика сообщений.</span><span class="sxs-lookup"><span data-stu-id="8cc79-392">The type of message handler.</span></span> <span data-ttu-id="8cc79-393">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-393">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="8cc79-394">Массив строк</span><span class="sxs-lookup"><span data-stu-id="8cc79-394">Array of Strings</span></span>|||<span data-ttu-id="8cc79-395">Массив доменов, для которых может регистрироваться обработчик сообщений ссылки.</span><span class="sxs-lookup"><span data-stu-id="8cc79-395">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="8cc79-396">Компосикстенсионс. Commands</span><span class="sxs-lookup"><span data-stu-id="8cc79-396">composeExtensions.commands</span></span>

<span data-ttu-id="8cc79-397">Ваш модуль обмена сообщениями должен объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="8cc79-397">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="8cc79-398">Каждая команда отображается в Microsoft Teams в качестве потенциального взаимодействия от точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="8cc79-398">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="8cc79-399">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="8cc79-399">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="8cc79-400">Каждый элемент команды представляет собой объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="8cc79-400">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="8cc79-401">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-401">Name</span></span>| <span data-ttu-id="8cc79-402">Тип</span><span class="sxs-lookup"><span data-stu-id="8cc79-402">Type</span></span>| <span data-ttu-id="8cc79-403">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-403">Maximum size</span></span> | <span data-ttu-id="8cc79-404">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-404">Required</span></span> | <span data-ttu-id="8cc79-405">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-405">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="8cc79-406">Строка</span><span class="sxs-lookup"><span data-stu-id="8cc79-406">String</span></span>|<span data-ttu-id="8cc79-407">64 символа</span><span class="sxs-lookup"><span data-stu-id="8cc79-407">64 characters</span></span>|<span data-ttu-id="8cc79-408">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-408">✔</span></span>|<span data-ttu-id="8cc79-409">Идентификатор команды</span><span class="sxs-lookup"><span data-stu-id="8cc79-409">The ID for the command</span></span>|
|`type`|<span data-ttu-id="8cc79-410">Строка</span><span class="sxs-lookup"><span data-stu-id="8cc79-410">String</span></span>|<span data-ttu-id="8cc79-411">64 символа</span><span class="sxs-lookup"><span data-stu-id="8cc79-411">64 characters</span></span>||<span data-ttu-id="8cc79-412">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="8cc79-412">Type of the command.</span></span> <span data-ttu-id="8cc79-413">Один из `query` или `action`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-413">One of `query` or `action`.</span></span> <span data-ttu-id="8cc79-414">Умолчани`query`</span><span class="sxs-lookup"><span data-stu-id="8cc79-414">Default: `query`</span></span>|
|`title`|<span data-ttu-id="8cc79-415">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-415">String</span></span>|<span data-ttu-id="8cc79-416">32 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-416">32 characters</span></span>|<span data-ttu-id="8cc79-417">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-417">✔</span></span>|<span data-ttu-id="8cc79-418">Понятное имя команды</span><span class="sxs-lookup"><span data-stu-id="8cc79-418">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="8cc79-419">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-419">String</span></span>|<span data-ttu-id="8cc79-420">128 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-420">128 characters</span></span>||<span data-ttu-id="8cc79-421">Описание, которое отображается пользователям для указания цели этой команды</span><span class="sxs-lookup"><span data-stu-id="8cc79-421">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="8cc79-422">Boolean</span><span class="sxs-lookup"><span data-stu-id="8cc79-422">Boolean</span></span>|||<span data-ttu-id="8cc79-423">Логическое значение, которое указывает, следует ли выполнять команду изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="8cc79-423">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="8cc79-424">Умолчани`false`</span><span class="sxs-lookup"><span data-stu-id="8cc79-424">Default: `false`</span></span>|
|`context`|<span data-ttu-id="8cc79-425">Массив строк</span><span class="sxs-lookup"><span data-stu-id="8cc79-425">Array of Strings</span></span>|<span data-ttu-id="8cc79-426">3 </span><span class="sxs-lookup"><span data-stu-id="8cc79-426">3</span></span>||<span data-ttu-id="8cc79-427">Определяет, откуда можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-427">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="8cc79-428">Любое сочетание `compose`, `commandBox`,. `message`</span><span class="sxs-lookup"><span data-stu-id="8cc79-428">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="8cc79-429">Значение по умолчанию:`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="8cc79-429">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="8cc79-430">Boolean</span><span class="sxs-lookup"><span data-stu-id="8cc79-430">Boolean</span></span>|||<span data-ttu-id="8cc79-431">Логическое значение, указывающее, должен ли он динамически получать модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="8cc79-431">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="8cc79-432">Объект</span><span class="sxs-lookup"><span data-stu-id="8cc79-432">Object</span></span>|||<span data-ttu-id="8cc79-433">Указание модуля задач для предварительной загрузки при использовании команды расширения системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="8cc79-433">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="8cc79-434">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-434">String</span></span>|<span data-ttu-id="8cc79-435">64</span><span class="sxs-lookup"><span data-stu-id="8cc79-435">64</span></span>||<span data-ttu-id="8cc79-436">Заголовок начального диалогового окна</span><span class="sxs-lookup"><span data-stu-id="8cc79-436">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="8cc79-437">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-437">String</span></span>|||<span data-ttu-id="8cc79-438">Ширина диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый"</span><span class="sxs-lookup"><span data-stu-id="8cc79-438">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="8cc79-439">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-439">String</span></span>|||<span data-ttu-id="8cc79-440">Высота диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый"</span><span class="sxs-lookup"><span data-stu-id="8cc79-440">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="8cc79-441">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-441">String</span></span>|||<span data-ttu-id="8cc79-442">Исходный URL-адрес вебвиев</span><span class="sxs-lookup"><span data-stu-id="8cc79-442">Initial webview URL</span></span>|
|`parameters`|<span data-ttu-id="8cc79-443">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="8cc79-443">Array of object</span></span>|<span data-ttu-id="8cc79-444">5 </span><span class="sxs-lookup"><span data-stu-id="8cc79-444">5</span></span>|<span data-ttu-id="8cc79-445">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-445">✔</span></span>|<span data-ttu-id="8cc79-446">Список параметров, которые выполняет команда.</span><span class="sxs-lookup"><span data-stu-id="8cc79-446">The list of parameters the command takes.</span></span> <span data-ttu-id="8cc79-447">Минимум: 1; максимум: 5</span><span class="sxs-lookup"><span data-stu-id="8cc79-447">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="8cc79-448">Строка</span><span class="sxs-lookup"><span data-stu-id="8cc79-448">String</span></span>|<span data-ttu-id="8cc79-449">64 символа</span><span class="sxs-lookup"><span data-stu-id="8cc79-449">64 characters</span></span>|<span data-ttu-id="8cc79-450">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-450">✔</span></span>|<span data-ttu-id="8cc79-451">Имя параметра в том виде, в котором оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="8cc79-451">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="8cc79-452">Он включен в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="8cc79-452">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="8cc79-453">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-453">String</span></span>|<span data-ttu-id="8cc79-454">32 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-454">32 characters</span></span>|<span data-ttu-id="8cc79-455">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-455">✔</span></span>|<span data-ttu-id="8cc79-456">Удобное для пользователя название параметра.</span><span class="sxs-lookup"><span data-stu-id="8cc79-456">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="8cc79-457">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-457">String</span></span>|<span data-ttu-id="8cc79-458">128 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-458">128 characters</span></span>||<span data-ttu-id="8cc79-459">Понятная пользователю строка, описывающая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="8cc79-459">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="8cc79-460">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-460">String</span></span>|<span data-ttu-id="8cc79-461">128 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-461">128 characters</span></span>||<span data-ttu-id="8cc79-462">Определяет тип элемента управления, отображаемого в модуле задачи для `fetchTask: true`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-462">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="8cc79-463">Один из `text`, `textarea`, `number`, `date` `time`,, `toggle`,`choiceset`</span><span class="sxs-lookup"><span data-stu-id="8cc79-463">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="8cc79-464">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="8cc79-464">Array of Objects</span></span>|<span data-ttu-id="8cc79-465">10 </span><span class="sxs-lookup"><span data-stu-id="8cc79-465">10</span></span>||<span data-ttu-id="8cc79-466">Варианты выбора для `choiceset`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-466">The choice options for the `choiceset`.</span></span> <span data-ttu-id="8cc79-467">Используйте только в `parameter.inputType` том случае, если`choiceset`</span><span class="sxs-lookup"><span data-stu-id="8cc79-467">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="8cc79-468">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-468">String</span></span>|<span data-ttu-id="8cc79-469">128</span><span class="sxs-lookup"><span data-stu-id="8cc79-469">128</span></span>||<span data-ttu-id="8cc79-470">Название варианта</span><span class="sxs-lookup"><span data-stu-id="8cc79-470">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="8cc79-471">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-471">String</span></span>|<span data-ttu-id="8cc79-472">512</span><span class="sxs-lookup"><span data-stu-id="8cc79-472">512</span></span>||<span data-ttu-id="8cc79-473">Выбор значения</span><span class="sxs-lookup"><span data-stu-id="8cc79-473">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="8cc79-474">permissions</span><span class="sxs-lookup"><span data-stu-id="8cc79-474">permissions</span></span>

<span data-ttu-id="8cc79-475">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="8cc79-475">**Optional**</span></span>

<span data-ttu-id="8cc79-476">Массив `string` , определяющий, какие разрешения запрашиваются приложением, что позволяет конечным пользователям знать, как будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="8cc79-476">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="8cc79-477">Следующие параметры неисключительны:</span><span class="sxs-lookup"><span data-stu-id="8cc79-477">The following options are non-exclusive:</span></span>

* <span data-ttu-id="8cc79-478">`identity`&emsp; Требуются сведения об удостоверении пользователя</span><span class="sxs-lookup"><span data-stu-id="8cc79-478">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="8cc79-479">`messageTeamMembers`&emsp; Требуется разрешение на отправку прямых сообщений участникам группы</span><span class="sxs-lookup"><span data-stu-id="8cc79-479">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="8cc79-480">Изменение этих разрешений при обновлении приложения приводит к тому, что пользователи будут повторять процесс разрешения при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-480">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="8cc79-481">Дополнительные сведения см. [в разделе Обновление приложения](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) .</span><span class="sxs-lookup"><span data-stu-id="8cc79-481">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="8cc79-482">девицепермиссионс</span><span class="sxs-lookup"><span data-stu-id="8cc79-482">devicePermissions</span></span>

<span data-ttu-id="8cc79-483">**Необязательное требование** Массив строк</span><span class="sxs-lookup"><span data-stu-id="8cc79-483">**Optional** Array of Strings</span></span>

<span data-ttu-id="8cc79-484">Указывает собственные функции на устройстве пользователя, к которым приложение может запрашивать доступ.</span><span class="sxs-lookup"><span data-stu-id="8cc79-484">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="8cc79-485">Возможные варианты:</span><span class="sxs-lookup"><span data-stu-id="8cc79-485">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="8cc79-486">валиддомаинс</span><span class="sxs-lookup"><span data-stu-id="8cc79-486">validDomains</span></span>

<span data-ttu-id="8cc79-487">**Необязательно**, за исключением **обязательного** места, где отмечено</span><span class="sxs-lookup"><span data-stu-id="8cc79-487">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="8cc79-488">Список допустимых доменов для веб-сайтов, которые приложение ожидает загружать в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="8cc79-488">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="8cc79-489">Примеры доменов могут включать подстановочные знаки `*.example.com`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-489">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="8cc79-490">Это соответствует только одному сегменту домена; Если вам нужно использовать `a.b.example.com` `*.*.example.com`этот параметр.</span><span class="sxs-lookup"><span data-stu-id="8cc79-490">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="8cc79-491">Если конфигурация вкладки или контентный пользовательский интерфейс должны перейти к любому другому домену, Кроме того, что используется для настройки вкладок, этот домен необходимо указать здесь.</span><span class="sxs-lookup"><span data-stu-id="8cc79-491">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="8cc79-492">Тем не менее, **не** нужно включать домены поставщиков удостоверений, которые требуется поддерживать в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="8cc79-492">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="8cc79-493">Например, для проверки подлинности с помощью идентификатора Google необходимо перенаправить на accounts.google.com, но не следует включать accounts.google.com в `validDomains[]`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-493">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="8cc79-494">Приложения Teams, которым для правильной работы требуются собственные URL-адреса SharePoint, могут содержать "{теамситедомаин}" в допустимом списке доменов.</span><span class="sxs-lookup"><span data-stu-id="8cc79-494">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8cc79-495">Не добавляйте домены за предельный элемент управления (напрямую или с помощью подстановочных знаков).</span><span class="sxs-lookup"><span data-stu-id="8cc79-495">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="8cc79-496">Например, `yourapp.onmicrosoft.com` является допустимым, но `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="8cc79-496">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="8cc79-497">Объект является массивом со всеми элементами типа `string`.</span><span class="sxs-lookup"><span data-stu-id="8cc79-497">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="8cc79-498">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="8cc79-498">webApplicationInfo</span></span>

<span data-ttu-id="8cc79-499">**Необязательное**</span><span class="sxs-lookup"><span data-stu-id="8cc79-499">**Optional**</span></span>

<span data-ttu-id="8cc79-500">Указание идентификатора приложения и графического объекта AAD для упрощения входа пользователей в приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="8cc79-500">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="8cc79-501">Имя</span><span class="sxs-lookup"><span data-stu-id="8cc79-501">Name</span></span>| <span data-ttu-id="8cc79-502">Тип</span><span class="sxs-lookup"><span data-stu-id="8cc79-502">Type</span></span>| <span data-ttu-id="8cc79-503">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="8cc79-503">Maximum size</span></span> | <span data-ttu-id="8cc79-504">Обязательный</span><span class="sxs-lookup"><span data-stu-id="8cc79-504">Required</span></span> | <span data-ttu-id="8cc79-505">Описание</span><span class="sxs-lookup"><span data-stu-id="8cc79-505">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="8cc79-506">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-506">String</span></span>|<span data-ttu-id="8cc79-507">36 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-507">36 characters</span></span>|<span data-ttu-id="8cc79-508">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-508">✔</span></span>|<span data-ttu-id="8cc79-509">Идентификатор приложения AAD приложения.</span><span class="sxs-lookup"><span data-stu-id="8cc79-509">AAD application id of the app.</span></span> <span data-ttu-id="8cc79-510">Этот идентификатор должен быть идентификатором GUID.</span><span class="sxs-lookup"><span data-stu-id="8cc79-510">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="8cc79-511">String</span><span class="sxs-lookup"><span data-stu-id="8cc79-511">String</span></span>|<span data-ttu-id="8cc79-512">2048 символов</span><span class="sxs-lookup"><span data-stu-id="8cc79-512">2048 characters</span></span>|<span data-ttu-id="8cc79-513">✔</span><span class="sxs-lookup"><span data-stu-id="8cc79-513">✔</span></span>|<span data-ttu-id="8cc79-514">URL-адрес ресурса приложения для получения маркера проверки подлинности для единого входа.</span><span class="sxs-lookup"><span data-stu-id="8cc79-514">Resource url of app for acquiring auth token for SSO.</span></span>|
