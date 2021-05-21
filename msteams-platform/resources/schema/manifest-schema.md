---
title: Справка о схеме манифеста
description: Описывает схему манифеста для Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: Схема манифеста команд
ms.openlocfilehash: 6c7cd02480f78d19aed269b5d78d0c6f470621d2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566448"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="e5529-104">Справка: схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e5529-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="e5529-105">Манифест Teams описывает, как приложение интегрируется в Microsoft Teams продукт.</span><span class="sxs-lookup"><span data-stu-id="e5529-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="e5529-106">Манифест должен соответствовать схеме, которая была на [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) уровне .</span><span class="sxs-lookup"><span data-stu-id="e5529-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="e5529-107">Поддерживаются и предыдущие версии 1.0, 1.1,..., 1.6 и так далее (с помощью "v1.x" в URL-адресе).</span><span class="sxs-lookup"><span data-stu-id="e5529-107">Previous versions 1.0, 1.1,..., 1.6, and so on are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="e5529-108">В следующем примере схемы показаны все параметры экстензивности:</span><span class="sxs-lookup"><span data-stu-id="e5529-108">The following schema sample shows all extensibility options:</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="e5529-109">Образец полного манифеста</span><span class="sxs-lookup"><span data-stu-id="e5529-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json",
  "manifestVersion": "1.10",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters (<=100 chars)"
  },
  "description": {
    "short": "Short description of your app (<= 80 chars)",
    "full": "Full description of your app (<= 4000 chars)"
  },
  "icons": {
    "outline": "A relative path to a transparent .png icon — 32px X 32px",
    "color": "A relative path to a full color .png icon — 192px X 192px"
  },
  "accentColor": "A valid HTML color code.",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "scopes": [
        "team",
        "groupchat"
      ],
      "canUpdateConfiguration": true,
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
      ],
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": [
         "sharePointFullPage",
         "sharePointWebPart"
      ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "context":[
        "personalTab",
        "channelTab"
        ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser)",
       "searchUrl":  "https://contoso.com/content (displayed in web browser)"
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "scopes": [
        "team",
        "personal",
        "groupchat"
      ],
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "supportsFiles": true,
      "supportsCalling": false,
      "supportsVideo": true,
      "commandLists": [
        {
          "scopes": [
            "team",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command 2",
              "description": "Description of Command 2"
            }
          ]
        },
        {
          "scopes": [
            "personal",
            "groupchat"
          ],
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
      "scopes": [
        "team"
      ],
      "configurationUrl": "https://contoso.com/teamsconnector/configure"
    }
  ],
  "composeExtensions": [
    {
      "canUpdateConfiguration": true,
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "type": "query",
          "context": [
            "compose",
            "commandBox"
          ],
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "fetchTask": false,
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "inputType": "text",
              "description": "Enter the keywords to search for",
              "value": "Initial value for the parameter",
              "choices": [
                {
                  "title": "Title of the choice",
                  "value": "Value of the choice"
                }
              ]
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "type": "action",
          "context": [
            "message"
          ],
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "fetchTask": true,
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType": "text"
            }
          ]
        }
      ],
      "taskInfo": {
        "title": "Initial dialog title",
        "width": "Dialog width",
        "height": "Dialog height",
        "url": "Initial webview URL"
      },
      "messageHandlers": [
        {
          "type": "link",
          "value": {
            "domains": [
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
  "devicePermissions": [
    "geolocation",
    "media",
    "notifications",
    "midi",
    "openExternal"
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
  "showLoadingIndicator": false,
  "isFullScreen": false,
  "activities": {
    "activityTypes": [
      {
        "type": "taskCreated",
        "description": "Task created activity",
        "templateText": "<team member> created task <taskId> for you"
      },
      {
        "type": "userMention",
        "description": "Personal mention activity",
        "templateText": "<team member> mentioned you"
      }
    ]
  },
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
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
  ]              
}
```

<span data-ttu-id="e5529-110">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="e5529-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="e5529-111">$schema</span><span class="sxs-lookup"><span data-stu-id="e5529-111">$schema</span></span>

<span data-ttu-id="e5529-112">Необязательный, но рекомендуемый — строка</span><span class="sxs-lookup"><span data-stu-id="e5529-112">Optional, but recommended — string</span></span>

<span data-ttu-id="e5529-113">URL https:// ссылки на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="e5529-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="e5529-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="e5529-114">manifestVersion</span></span>

<span data-ttu-id="e5529-115">**Обязательно —** строка</span><span class="sxs-lookup"><span data-stu-id="e5529-115">**Required** — string</span></span>

<span data-ttu-id="e5529-116">Версия схемы манифеста, используемая этим манифестом.</span><span class="sxs-lookup"><span data-stu-id="e5529-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="e5529-117">Должно быть 1.10.</span><span class="sxs-lookup"><span data-stu-id="e5529-117">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="e5529-118">version</span><span class="sxs-lookup"><span data-stu-id="e5529-118">version</span></span>

<span data-ttu-id="e5529-119">**Обязательно —** строка</span><span class="sxs-lookup"><span data-stu-id="e5529-119">**Required** — string</span></span>

<span data-ttu-id="e5529-120">Версия определенного приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-120">The version of a specific app.</span></span> <span data-ttu-id="e5529-121">Если вы что-то обновите в манифесте, версия также должна быть приумножная.</span><span class="sxs-lookup"><span data-stu-id="e5529-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="e5529-122">Таким образом, при установке нового манифеста он переописает существующий и пользователь получает новые функции.</span><span class="sxs-lookup"><span data-stu-id="e5529-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="e5529-123">Если это приложение было отправлено в магазин, новый манифест должен быть повторно отправлен и повторно проверен.</span><span class="sxs-lookup"><span data-stu-id="e5529-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="e5529-124">Пользователи приложения получают новый обновленный манифест автоматически в течение нескольких часов после утверждения манифеста.</span><span class="sxs-lookup"><span data-stu-id="e5529-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="e5529-125">Если приложение запрашивает разрешения на изменение, пользователям будет предложено обновить и повторно согласиться на приложение.</span><span class="sxs-lookup"><span data-stu-id="e5529-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="e5529-126">Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="e5529-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="e5529-127">id</span><span class="sxs-lookup"><span data-stu-id="e5529-127">id</span></span>

<span data-ttu-id="e5529-128">**Обязательно —** ID приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="e5529-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="e5529-129">Идентификатор — уникальный идентификатор, созданный Корпорацией Майкрософт для приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="e5529-130">У вас есть ID, если бот зарегистрирован через Microsoft Bot Framework или веб-приложение вкладки уже вошел в Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e5529-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="e5529-131">Здесь необходимо ввести ID.</span><span class="sxs-lookup"><span data-stu-id="e5529-131">You must enter the ID here.</span></span> <span data-ttu-id="e5529-132">В противном случае необходимо создать новый ID на портале [регистрации приложений Майкрософт.](https://aka.ms/appregistrations)</span><span class="sxs-lookup"><span data-stu-id="e5529-132">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="e5529-133">При добавлении бота используйте тот же ID.</span><span class="sxs-lookup"><span data-stu-id="e5529-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="e5529-134">Если вы передаете обновление существующему приложению в AppSource, ID в манифесте не должен изменяться.</span><span class="sxs-lookup"><span data-stu-id="e5529-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="e5529-135">developer</span><span class="sxs-lookup"><span data-stu-id="e5529-135">developer</span></span>

<span data-ttu-id="e5529-136">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="e5529-136">**Required** — object</span></span>

<span data-ttu-id="e5529-137">Указывает сведения о вашей компании.</span><span class="sxs-lookup"><span data-stu-id="e5529-137">Specifies information about your company.</span></span> <span data-ttu-id="e5529-138">Для приложений, представленных в Teams магазине, эти значения должны соответствовать сведениям в списке магазина.</span><span class="sxs-lookup"><span data-stu-id="e5529-138">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="e5529-139">Дополнительные сведения см. [в Teams руководства по публикации в магазине.](~/concepts/deploy-and-publish/appsource/publish.md)</span><span class="sxs-lookup"><span data-stu-id="e5529-139">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="e5529-140">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-140">Name</span></span>| <span data-ttu-id="e5529-141">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-141">Maximum size</span></span> | <span data-ttu-id="e5529-142">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-142">Required</span></span> | <span data-ttu-id="e5529-143">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="e5529-144">32 символа</span><span class="sxs-lookup"><span data-stu-id="e5529-144">32 characters</span></span>|<span data-ttu-id="e5529-145">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-145">✔</span></span>|<span data-ttu-id="e5529-146">Имя отображения для разработчика.</span><span class="sxs-lookup"><span data-stu-id="e5529-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="e5529-147">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-147">2048 characters</span></span>|<span data-ttu-id="e5529-148">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-148">✔</span></span>|<span data-ttu-id="e5529-149">Url https:// url-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="e5529-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="e5529-150">Эта ссылка должна принимать пользователей на страницу вашей компании или конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="e5529-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="e5529-151">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-151">2048 characters</span></span>|<span data-ttu-id="e5529-152">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-152">✔</span></span>|<span data-ttu-id="e5529-153">Url https:// url-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="e5529-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="e5529-154">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-154">2048 characters</span></span>|<span data-ttu-id="e5529-155">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-155">✔</span></span>|<span data-ttu-id="e5529-156">Url https:// url-адрес для условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="e5529-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="e5529-157">10 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-157">10 characters</span></span>| |<span data-ttu-id="e5529-158">**Необязательный** Идентификатор Сети партнеров Майкрософт, который определяет организацию-партнер, которая строит приложение.</span><span class="sxs-lookup"><span data-stu-id="e5529-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="e5529-159">name</span><span class="sxs-lookup"><span data-stu-id="e5529-159">name</span></span>

<span data-ttu-id="e5529-160">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="e5529-160">**Required** — object</span></span>

<span data-ttu-id="e5529-161">Имя приложения, отображаемого пользователям в Teams.</span><span class="sxs-lookup"><span data-stu-id="e5529-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="e5529-162">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="e5529-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="e5529-163">Значения и `short` должны `full` быть разными.</span><span class="sxs-lookup"><span data-stu-id="e5529-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="e5529-164">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-164">Name</span></span>| <span data-ttu-id="e5529-165">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-165">Maximum size</span></span> | <span data-ttu-id="e5529-166">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-166">Required</span></span> | <span data-ttu-id="e5529-167">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="e5529-168">30 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-168">30 characters</span></span>|<span data-ttu-id="e5529-169">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-169">✔</span></span>|<span data-ttu-id="e5529-170">Короткое имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="e5529-171">100 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-171">100 characters</span></span>||<span data-ttu-id="e5529-172">Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="e5529-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="e5529-173">description</span><span class="sxs-lookup"><span data-stu-id="e5529-173">description</span></span>

<span data-ttu-id="e5529-174">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="e5529-174">**Required** — object</span></span>

<span data-ttu-id="e5529-175">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="e5529-175">Describes your app to users.</span></span> <span data-ttu-id="e5529-176">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="e5529-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="e5529-177">Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, чтобы помочь потенциальным клиентам понять, что делает ваш опыт.</span><span class="sxs-lookup"><span data-stu-id="e5529-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="e5529-178">В полном описании необходимо учтите, что для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="e5529-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="e5529-179">Значения и `short` должны `full` быть разными.</span><span class="sxs-lookup"><span data-stu-id="e5529-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="e5529-180">Короткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="e5529-181">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-181">Name</span></span>| <span data-ttu-id="e5529-182">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-182">Maximum size</span></span> | <span data-ttu-id="e5529-183">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-183">Required</span></span> | <span data-ttu-id="e5529-184">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="e5529-185">80 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-185">80 characters</span></span>|<span data-ttu-id="e5529-186">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-186">✔</span></span>|<span data-ttu-id="e5529-187">Краткое описание работы приложения, используемого при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="e5529-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="e5529-188">4000 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-188">4000 characters</span></span>|<span data-ttu-id="e5529-189">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-189">✔</span></span>|<span data-ttu-id="e5529-190">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="e5529-191">packageName</span><span class="sxs-lookup"><span data-stu-id="e5529-191">packageName</span></span>

<span data-ttu-id="e5529-192">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="e5529-192">**Optional** — string</span></span>

<span data-ttu-id="e5529-193">Уникальный идентификатор для приложения в обратной нотации домена; например, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="e5529-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="e5529-194">Максимальная длина: 64 символа.</span><span class="sxs-lookup"><span data-stu-id="e5529-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="e5529-195">локализацияInfo</span><span class="sxs-lookup"><span data-stu-id="e5529-195">localizationInfo</span></span>

<span data-ttu-id="e5529-196">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="e5529-196">**Optional** — object</span></span>

<span data-ttu-id="e5529-197">Позволяет спецификацию языка по умолчанию, а также указатели для дополнительных языковых файлов.</span><span class="sxs-lookup"><span data-stu-id="e5529-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="e5529-198">Дополнительные сведения см. в [деле локализации.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="e5529-198">For more information, see [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="e5529-199">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-199">Name</span></span>| <span data-ttu-id="e5529-200">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-200">Maximum size</span></span> | <span data-ttu-id="e5529-201">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-201">Required</span></span> | <span data-ttu-id="e5529-202">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="e5529-203">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-203">✔</span></span>|<span data-ttu-id="e5529-204">Языковой тег строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="e5529-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="e5529-205">локализацияInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="e5529-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="e5529-206">Массив объектов, указывающих дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="e5529-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="e5529-207">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-207">Name</span></span>| <span data-ttu-id="e5529-208">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-208">Maximum size</span></span> | <span data-ttu-id="e5529-209">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-209">Required</span></span> | <span data-ttu-id="e5529-210">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="e5529-211">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-211">✔</span></span>|<span data-ttu-id="e5529-212">Языковой тег строки в предоставленного файла.</span><span class="sxs-lookup"><span data-stu-id="e5529-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="e5529-213">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-213">✔</span></span>|<span data-ttu-id="e5529-214">Относительный путь к файлу .json, содержащим переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="e5529-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="e5529-215">icons</span><span class="sxs-lookup"><span data-stu-id="e5529-215">icons</span></span>

<span data-ttu-id="e5529-216">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="e5529-216">**Required** — object</span></span>

<span data-ttu-id="e5529-217">Значки, используемые в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="e5529-217">Icons used within the Teams app.</span></span> <span data-ttu-id="e5529-218">Файлы значков должны быть включены в пакет отправки.</span><span class="sxs-lookup"><span data-stu-id="e5529-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="e5529-219">Дополнительные сведения см. в [значках.](../../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="e5529-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="e5529-220">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-220">Name</span></span>| <span data-ttu-id="e5529-221">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-221">Maximum size</span></span> | <span data-ttu-id="e5529-222">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-222">Required</span></span> | <span data-ttu-id="e5529-223">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="e5529-224">32 x 32 пикселя</span><span class="sxs-lookup"><span data-stu-id="e5529-224">32 x 32 pixels</span></span>|<span data-ttu-id="e5529-225">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-225">✔</span></span>|<span data-ttu-id="e5529-226">Относительный путь к прозрачному значку контура PNG 32x32.</span><span class="sxs-lookup"><span data-stu-id="e5529-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="e5529-227">192 x 192 пикселя</span><span class="sxs-lookup"><span data-stu-id="e5529-227">192 x 192 pixels</span></span>|<span data-ttu-id="e5529-228">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-228">✔</span></span>|<span data-ttu-id="e5529-229">Относительный путь к значку PNG полного цвета 192x192.</span><span class="sxs-lookup"><span data-stu-id="e5529-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="e5529-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="e5529-230">accentColor</span></span>

<span data-ttu-id="e5529-231">**Необязательный** — цветовой код HTML Hex</span><span class="sxs-lookup"><span data-stu-id="e5529-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="e5529-232">Цвет, который можно использовать в сочетании с и в качестве фона для значков контура.</span><span class="sxs-lookup"><span data-stu-id="e5529-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="e5529-233">Значение должно быть допустимым цветовым кодом HTML, начиная, например, с `#4464ee` "#".</span><span class="sxs-lookup"><span data-stu-id="e5529-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="e5529-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="e5529-234">configurableTabs</span></span>

<span data-ttu-id="e5529-235">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="e5529-235">**Optional** — array</span></span>

<span data-ttu-id="e5529-236">Используется, когда в вашем приложении есть опыт работы с вкладками канала команды, которая требует дополнительной конфигурации перед ее добавлением.</span><span class="sxs-lookup"><span data-stu-id="e5529-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="e5529-237">Настраиваемые вкладки поддерживаются только в области команд, и вы можете настроить те же вкладки несколько раз.</span><span class="sxs-lookup"><span data-stu-id="e5529-237">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="e5529-238">Однако определить его в манифесте можно только один раз.</span><span class="sxs-lookup"><span data-stu-id="e5529-238">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="e5529-239">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-239">Name</span></span>| <span data-ttu-id="e5529-240">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-240">Type</span></span>| <span data-ttu-id="e5529-241">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-241">Maximum size</span></span> | <span data-ttu-id="e5529-242">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-242">Required</span></span> | <span data-ttu-id="e5529-243">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="e5529-244">string</span><span class="sxs-lookup"><span data-stu-id="e5529-244">string</span></span>|<span data-ttu-id="e5529-245">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-245">2048 characters</span></span>|<span data-ttu-id="e5529-246">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-246">✔</span></span>|<span data-ttu-id="e5529-247">URL-https://, который можно использовать при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="e5529-247">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="e5529-248">массив enums</span><span class="sxs-lookup"><span data-stu-id="e5529-248">array of enums</span></span>|<span data-ttu-id="e5529-249">1</span><span class="sxs-lookup"><span data-stu-id="e5529-249">1</span></span>|<span data-ttu-id="e5529-250">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-250">✔</span></span>|<span data-ttu-id="e5529-251">В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области.</span><span class="sxs-lookup"><span data-stu-id="e5529-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="e5529-252">boolean</span><span class="sxs-lookup"><span data-stu-id="e5529-252">boolean</span></span>|||<span data-ttu-id="e5529-253">Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания.</span><span class="sxs-lookup"><span data-stu-id="e5529-253">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="e5529-254">По умолчанию: **true**.</span><span class="sxs-lookup"><span data-stu-id="e5529-254">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="e5529-255">массив enums</span><span class="sxs-lookup"><span data-stu-id="e5529-255">array of enums</span></span>|<span data-ttu-id="e5529-256">6 </span><span class="sxs-lookup"><span data-stu-id="e5529-256">6</span></span>||<span data-ttu-id="e5529-257">Набор `contextItem` областей, в которых [вкладка поддерживается.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="e5529-257">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="e5529-258">По умолчанию: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="e5529-258">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="e5529-259">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-259">string</span></span>|<span data-ttu-id="e5529-260">2048</span><span class="sxs-lookup"><span data-stu-id="e5529-260">2048</span></span>||<span data-ttu-id="e5529-261">Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e5529-261">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="e5529-262">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="e5529-262">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="e5529-263">массив enums</span><span class="sxs-lookup"><span data-stu-id="e5529-263">array of enums</span></span>|<span data-ttu-id="e5529-264">1</span><span class="sxs-lookup"><span data-stu-id="e5529-264">1</span></span>||<span data-ttu-id="e5529-265">Определяет, как вкладка доступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e5529-265">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="e5529-266">Параметры `sharePointFullPage` и `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="e5529-266">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="e5529-267">staticTabs</span><span class="sxs-lookup"><span data-stu-id="e5529-267">staticTabs</span></span>

<span data-ttu-id="e5529-268">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="e5529-268">**Optional** — array</span></span>

<span data-ttu-id="e5529-269">Определяет набор вкладок, которые можно "прикрепить" по умолчанию, не добавляя их вручную.</span><span class="sxs-lookup"><span data-stu-id="e5529-269">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="e5529-270">Статические вкладки, объявленные в области, всегда прикрепяются к личному опыту `personal` приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-270">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="e5529-271">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="e5529-271">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="e5529-272">Этот элемент — массив (не более 16 элементов) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="e5529-272">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="e5529-273">Этот блок требуется только для решений, которые предоставляют статическое решение вкладки.</span><span class="sxs-lookup"><span data-stu-id="e5529-273">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="e5529-274">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-274">Name</span></span>| <span data-ttu-id="e5529-275">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-275">Type</span></span>| <span data-ttu-id="e5529-276">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-276">Maximum size</span></span> | <span data-ttu-id="e5529-277">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-277">Required</span></span> | <span data-ttu-id="e5529-278">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-278">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="e5529-279">string</span><span class="sxs-lookup"><span data-stu-id="e5529-279">string</span></span>|<span data-ttu-id="e5529-280">64 символа</span><span class="sxs-lookup"><span data-stu-id="e5529-280">64 characters</span></span>|<span data-ttu-id="e5529-281">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-281">✔</span></span>|<span data-ttu-id="e5529-282">Уникальный идентификатор для объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="e5529-282">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="e5529-283">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-283">string</span></span>|<span data-ttu-id="e5529-284">128 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-284">128 characters</span></span>|<span data-ttu-id="e5529-285">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-285">✔</span></span>|<span data-ttu-id="e5529-286">Отображение имени вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="e5529-286">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="e5529-287">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-287">string</span></span>||<span data-ttu-id="e5529-288">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-288">✔</span></span>|<span data-ttu-id="e5529-289">URL https://, который указывает на пользовательский интерфейс объекта, отображаемого на Teams холсте.</span><span class="sxs-lookup"><span data-stu-id="e5529-289">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="e5529-290">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-290">string</span></span>|||<span data-ttu-id="e5529-291">Url https://, чтобы указать, выбирает ли пользователь просмотр в браузере.</span><span class="sxs-lookup"><span data-stu-id="e5529-291">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="e5529-292">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-292">string</span></span>|||<span data-ttu-id="e5529-293">Url https://, на который нужно указать для поисковых запросов пользователя.</span><span class="sxs-lookup"><span data-stu-id="e5529-293">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="e5529-294">массив enums</span><span class="sxs-lookup"><span data-stu-id="e5529-294">array of enums</span></span>|<span data-ttu-id="e5529-295">1</span><span class="sxs-lookup"><span data-stu-id="e5529-295">1</span></span>|<span data-ttu-id="e5529-296">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-296">✔</span></span>|<span data-ttu-id="e5529-297">В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в `personal` рамках личного опыта.</span><span class="sxs-lookup"><span data-stu-id="e5529-297">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="e5529-298">массив enums</span><span class="sxs-lookup"><span data-stu-id="e5529-298">array of enums</span></span>| <span data-ttu-id="e5529-299">2</span><span class="sxs-lookup"><span data-stu-id="e5529-299">2</span></span>|| <span data-ttu-id="e5529-300">Набор `contextItem` областей, в которых поддерживается вкладка.</span><span class="sxs-lookup"><span data-stu-id="e5529-300">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="e5529-301">Функция searchUrl недоступна сторонним разработчикам.</span><span class="sxs-lookup"><span data-stu-id="e5529-301">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="e5529-302">Если для отображения соответствующего контента или для инициации потока проверки подлинности в вкладке Get context для вашей вкладки Microsoft Teams контексте, дополнительные сведения см. в статье Get context for [your Microsoft Teams.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="e5529-302">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="e5529-303">боты</span><span class="sxs-lookup"><span data-stu-id="e5529-303">bots</span></span>

<span data-ttu-id="e5529-304">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="e5529-304">**Optional** — array</span></span>

<span data-ttu-id="e5529-305">Определяет решение бота, а также необязательные сведения, такие как свойства команд по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e5529-305">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="e5529-306">Элемент — массив (максимум 1 элемент в настоящее время разрешен только для одного бота в приложении) со всеми элементами &mdash; типа `object` .</span><span class="sxs-lookup"><span data-stu-id="e5529-306">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="e5529-307">Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.</span><span class="sxs-lookup"><span data-stu-id="e5529-307">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="e5529-308">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-308">Name</span></span>| <span data-ttu-id="e5529-309">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-309">Type</span></span>| <span data-ttu-id="e5529-310">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-310">Maximum size</span></span> | <span data-ttu-id="e5529-311">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-311">Required</span></span> | <span data-ttu-id="e5529-312">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-312">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="e5529-313">string</span><span class="sxs-lookup"><span data-stu-id="e5529-313">string</span></span>|<span data-ttu-id="e5529-314">64 символа</span><span class="sxs-lookup"><span data-stu-id="e5529-314">64 characters</span></span>|<span data-ttu-id="e5529-315">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-315">✔</span></span>|<span data-ttu-id="e5529-316">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e5529-316">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="e5529-317">Это вполне может быть таким же, как общий [ID приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="e5529-317">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="e5529-318">массив enums</span><span class="sxs-lookup"><span data-stu-id="e5529-318">array of enums</span></span>|<span data-ttu-id="e5529-319">3</span><span class="sxs-lookup"><span data-stu-id="e5529-319">3</span></span>|<span data-ttu-id="e5529-320">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-320">✔</span></span>|<span data-ttu-id="e5529-321">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="e5529-321">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="e5529-322">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="e5529-322">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="e5529-323">boolean</span><span class="sxs-lookup"><span data-stu-id="e5529-323">boolean</span></span>|||<span data-ttu-id="e5529-324">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="e5529-324">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="e5529-325">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="e5529-325">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="e5529-326">boolean</span><span class="sxs-lookup"><span data-stu-id="e5529-326">boolean</span></span>|||<span data-ttu-id="e5529-327">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="e5529-327">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="e5529-328">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="e5529-328">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="e5529-329">boolean</span><span class="sxs-lookup"><span data-stu-id="e5529-329">boolean</span></span>|||<span data-ttu-id="e5529-330">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="e5529-330">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="e5529-331">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="e5529-331">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="e5529-332">boolean</span><span class="sxs-lookup"><span data-stu-id="e5529-332">boolean</span></span>|||<span data-ttu-id="e5529-333">Значение, указывающее, где бот поддерживает звуковые вызовы.</span><span class="sxs-lookup"><span data-stu-id="e5529-333">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="e5529-334">**ВАЖНО.** Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="e5529-334">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="e5529-335">Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="e5529-335">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="e5529-336">Она предоставляется только для тестирования и разведки и не должна использоваться в производственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="e5529-336">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="e5529-337">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="e5529-337">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="e5529-338">boolean</span><span class="sxs-lookup"><span data-stu-id="e5529-338">boolean</span></span>|||<span data-ttu-id="e5529-339">Значение, указывающее, где бот поддерживает видеозвонков.</span><span class="sxs-lookup"><span data-stu-id="e5529-339">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="e5529-340">**ВАЖНО.** Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="e5529-340">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="e5529-341">Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="e5529-341">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="e5529-342">Она предоставляется только для тестирования и разведки и не должна использоваться в производственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="e5529-342">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="e5529-343">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="e5529-343">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="e5529-344">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="e5529-344">bots.commandLists</span></span>

<span data-ttu-id="e5529-345">Необязательный список команд, которые бот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="e5529-345">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="e5529-346">Объект — массив (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом.</span><span class="sxs-lookup"><span data-stu-id="e5529-346">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="e5529-347">Дополнительные [сведения см. в](~/bots/how-to/create-a-bot-commands-menu.md) меню Bot.</span><span class="sxs-lookup"><span data-stu-id="e5529-347">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="e5529-348">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-348">Name</span></span>| <span data-ttu-id="e5529-349">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-349">Type</span></span>| <span data-ttu-id="e5529-350">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-350">Maximum size</span></span> | <span data-ttu-id="e5529-351">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-351">Required</span></span> | <span data-ttu-id="e5529-352">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-352">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="e5529-353">массив enums</span><span class="sxs-lookup"><span data-stu-id="e5529-353">array of enums</span></span>|<span data-ttu-id="e5529-354">3</span><span class="sxs-lookup"><span data-stu-id="e5529-354">3</span></span>|<span data-ttu-id="e5529-355">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-355">✔</span></span>|<span data-ttu-id="e5529-356">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="e5529-356">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="e5529-357">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="e5529-357">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="e5529-358">массив объектов</span><span class="sxs-lookup"><span data-stu-id="e5529-358">array of objects</span></span>|<span data-ttu-id="e5529-359">10 </span><span class="sxs-lookup"><span data-stu-id="e5529-359">10</span></span>|<span data-ttu-id="e5529-360">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-360">✔</span></span>|<span data-ttu-id="e5529-361">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="e5529-361">An array of commands the bot supports:</span></span><br><span data-ttu-id="e5529-362">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="e5529-362">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="e5529-363">`description`: простое описание или пример синтаксиса команды и его аргумента (строка, 128).</span><span class="sxs-lookup"><span data-stu-id="e5529-363">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="e5529-364">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="e5529-364">bots.commandLists.commands</span></span>

|<span data-ttu-id="e5529-365">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-365">Name</span></span>| <span data-ttu-id="e5529-366">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-366">Type</span></span>| <span data-ttu-id="e5529-367">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-367">Maximum size</span></span> | <span data-ttu-id="e5529-368">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-368">Required</span></span> | <span data-ttu-id="e5529-369">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-369">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="e5529-370">title</span><span class="sxs-lookup"><span data-stu-id="e5529-370">title</span></span>|<span data-ttu-id="e5529-371">string</span><span class="sxs-lookup"><span data-stu-id="e5529-371">string</span></span>|<span data-ttu-id="e5529-372">12 </span><span class="sxs-lookup"><span data-stu-id="e5529-372">12</span></span>|<span data-ttu-id="e5529-373">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-373">✔</span></span>|<span data-ttu-id="e5529-374">Имя команды бота.</span><span class="sxs-lookup"><span data-stu-id="e5529-374">The bot command name.</span></span>|
|<span data-ttu-id="e5529-375">description</span><span class="sxs-lookup"><span data-stu-id="e5529-375">description</span></span>|<span data-ttu-id="e5529-376">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-376">string</span></span>|<span data-ttu-id="e5529-377">128 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-377">128 characters</span></span>|<span data-ttu-id="e5529-378">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-378">✔</span></span>|<span data-ttu-id="e5529-379">Простое текстовое описание или пример синтаксиса команд и его аргументов.</span><span class="sxs-lookup"><span data-stu-id="e5529-379">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="e5529-380">соединители</span><span class="sxs-lookup"><span data-stu-id="e5529-380">connectors</span></span>

<span data-ttu-id="e5529-381">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="e5529-381">**Optional** — array</span></span>

<span data-ttu-id="e5529-382">Блок `connectors` определяет Office 365 соединители для приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-382">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="e5529-383">Объект — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="e5529-383">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="e5529-384">Этот блок необходим только для решений, которые предоставляют соединители.</span><span class="sxs-lookup"><span data-stu-id="e5529-384">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="e5529-385">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-385">Name</span></span>| <span data-ttu-id="e5529-386">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-386">Type</span></span>| <span data-ttu-id="e5529-387">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-387">Maximum size</span></span> | <span data-ttu-id="e5529-388">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-388">Required</span></span> | <span data-ttu-id="e5529-389">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-389">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="e5529-390">string</span><span class="sxs-lookup"><span data-stu-id="e5529-390">string</span></span>|<span data-ttu-id="e5529-391">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-391">2048 characters</span></span>|<span data-ttu-id="e5529-392">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-392">✔</span></span>|<span data-ttu-id="e5529-393">URL https://, который необходимо использовать при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="e5529-393">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="e5529-394">массив enums</span><span class="sxs-lookup"><span data-stu-id="e5529-394">array of enums</span></span>|<span data-ttu-id="e5529-395">1</span><span class="sxs-lookup"><span data-stu-id="e5529-395">1</span></span>|<span data-ttu-id="e5529-396">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-396">✔</span></span>|<span data-ttu-id="e5529-397">Указывает, предоставляет ли соединители опыт в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="e5529-397">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="e5529-398">В настоящее время `team` поддерживается только область.</span><span class="sxs-lookup"><span data-stu-id="e5529-398">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="e5529-399">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-399">string</span></span>|<span data-ttu-id="e5529-400">64 символа</span><span class="sxs-lookup"><span data-stu-id="e5529-400">64 characters</span></span>|<span data-ttu-id="e5529-401">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-401">✔</span></span>|<span data-ttu-id="e5529-402">Уникальный идентификатор соединитетеля, который соответствует его идентификатору в панели мониторинга разработчиков [соединителок.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="e5529-402">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="e5529-403">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="e5529-403">composeExtensions</span></span>

<span data-ttu-id="e5529-404">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="e5529-404">**Optional** — array</span></span>

<span data-ttu-id="e5529-405">Определяет расширение обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-405">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="e5529-406">В ноябре 2017 г. имя функции было изменено с "расширение составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжили функционировать.</span><span class="sxs-lookup"><span data-stu-id="e5529-406">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="e5529-407">Элемент — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="e5529-407">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="e5529-408">Этот блок необходим только для решений, которые предоставляют расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e5529-408">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="e5529-409">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-409">Name</span></span>| <span data-ttu-id="e5529-410">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-410">Type</span></span> | <span data-ttu-id="e5529-411">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-411">Maximum Size</span></span> | <span data-ttu-id="e5529-412">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-412">Required</span></span> | <span data-ttu-id="e5529-413">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-413">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="e5529-414">string</span><span class="sxs-lookup"><span data-stu-id="e5529-414">string</span></span>|<span data-ttu-id="e5529-415">64</span><span class="sxs-lookup"><span data-stu-id="e5529-415">64</span></span>|<span data-ttu-id="e5529-416">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-416">✔</span></span>|<span data-ttu-id="e5529-417">Уникальный ID приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрирован в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e5529-417">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="e5529-418">Это вполне может быть таким же, как и общий ID приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-418">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="e5529-419">массив объектов</span><span class="sxs-lookup"><span data-stu-id="e5529-419">array of objects</span></span>|<span data-ttu-id="e5529-420">10 </span><span class="sxs-lookup"><span data-stu-id="e5529-420">10</span></span>|<span data-ttu-id="e5529-421">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-421">✔</span></span>|<span data-ttu-id="e5529-422">Массив команд, поддерживаемых расширением обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e5529-422">Array of commands the messaging extension supports.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="e5529-423">boolean</span><span class="sxs-lookup"><span data-stu-id="e5529-423">boolean</span></span>|||<span data-ttu-id="e5529-424">Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e5529-424">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="e5529-425">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="e5529-425">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="e5529-426">массив объектов</span><span class="sxs-lookup"><span data-stu-id="e5529-426">array of Objects</span></span>|<span data-ttu-id="e5529-427">5 </span><span class="sxs-lookup"><span data-stu-id="e5529-427">5</span></span>||<span data-ttu-id="e5529-428">Список обработчиков, которые позволяют вызывать приложения при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="e5529-428">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="e5529-429">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-429">string</span></span>|||<span data-ttu-id="e5529-430">Тип обработка сообщений.</span><span class="sxs-lookup"><span data-stu-id="e5529-430">The type of message handler.</span></span> <span data-ttu-id="e5529-431">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="e5529-431">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="e5529-432">массив строк</span><span class="sxs-lookup"><span data-stu-id="e5529-432">array of Strings</span></span>|||<span data-ttu-id="e5529-433">Массив доменов, для которые обработник сообщений ссылок может зарегистрироваться.</span><span class="sxs-lookup"><span data-stu-id="e5529-433">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="e5529-434">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="e5529-434">composeExtensions.commands</span></span>

<span data-ttu-id="e5529-435">Расширение обмена сообщениями должно объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="e5529-435">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="e5529-436">Каждая команда отображается Microsoft Teams как потенциальное взаимодействие с точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e5529-436">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="e5529-437">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="e5529-437">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="e5529-438">Каждый элемент команды — это объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="e5529-438">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="e5529-439">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-439">Name</span></span>| <span data-ttu-id="e5529-440">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-440">Type</span></span>| <span data-ttu-id="e5529-441">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-441">Maximum size</span></span> | <span data-ttu-id="e5529-442">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-442">Required</span></span> | <span data-ttu-id="e5529-443">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-443">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="e5529-444">string</span><span class="sxs-lookup"><span data-stu-id="e5529-444">string</span></span>|<span data-ttu-id="e5529-445">64 символа</span><span class="sxs-lookup"><span data-stu-id="e5529-445">64 characters</span></span>|<span data-ttu-id="e5529-446">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-446">✔</span></span>|<span data-ttu-id="e5529-447">ID для команды.</span><span class="sxs-lookup"><span data-stu-id="e5529-447">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="e5529-448">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-448">string</span></span>|<span data-ttu-id="e5529-449">32 символа</span><span class="sxs-lookup"><span data-stu-id="e5529-449">32 characters</span></span>|<span data-ttu-id="e5529-450">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-450">✔</span></span>|<span data-ttu-id="e5529-451">Удобное имя команды.</span><span class="sxs-lookup"><span data-stu-id="e5529-451">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="e5529-452">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-452">string</span></span>|<span data-ttu-id="e5529-453">64 символа</span><span class="sxs-lookup"><span data-stu-id="e5529-453">64 characters</span></span>||<span data-ttu-id="e5529-454">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="e5529-454">Type of the command.</span></span> <span data-ttu-id="e5529-455">Один `query` из или `action` .</span><span class="sxs-lookup"><span data-stu-id="e5529-455">One of `query` or `action`.</span></span> <span data-ttu-id="e5529-456">По умолчанию: **запрос**.</span><span class="sxs-lookup"><span data-stu-id="e5529-456">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="e5529-457">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-457">string</span></span>|<span data-ttu-id="e5529-458">128 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-458">128 characters</span></span>||<span data-ttu-id="e5529-459">В описании, которое отображается пользователями, указывается назначение этой команды.</span><span class="sxs-lookup"><span data-stu-id="e5529-459">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="e5529-460">boolean</span><span class="sxs-lookup"><span data-stu-id="e5529-460">boolean</span></span>|||<span data-ttu-id="e5529-461">Значение boolean указывает, выполняется ли команда изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="e5529-461">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="e5529-462">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="e5529-462">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="e5529-463">массив строк</span><span class="sxs-lookup"><span data-stu-id="e5529-463">array of Strings</span></span>|<span data-ttu-id="e5529-464">3</span><span class="sxs-lookup"><span data-stu-id="e5529-464">3</span></span>||<span data-ttu-id="e5529-465">Определяет, из чего можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="e5529-465">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="e5529-466">Любое сочетание `compose` `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="e5529-466">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="e5529-467">Значение по умолчанию: `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="e5529-467">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="e5529-468">boolean</span><span class="sxs-lookup"><span data-stu-id="e5529-468">boolean</span></span>|||<span data-ttu-id="e5529-469">Значение boolean, которое указывает, должен ли он динамически получать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="e5529-469">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="e5529-470">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="e5529-470">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="e5529-471">объект</span><span class="sxs-lookup"><span data-stu-id="e5529-471">object</span></span>|||<span data-ttu-id="e5529-472">Укажите модуль задач для предварительной загрузки при использовании команды расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e5529-472">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="e5529-473">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-473">string</span></span>|<span data-ttu-id="e5529-474">64 символа</span><span class="sxs-lookup"><span data-stu-id="e5529-474">64 characters</span></span>||<span data-ttu-id="e5529-475">Начальное название диалогов.</span><span class="sxs-lookup"><span data-stu-id="e5529-475">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="e5529-476">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-476">string</span></span>|||<span data-ttu-id="e5529-477">Ширина диалогов — число в пикселях или макет по умолчанию, такие как "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="e5529-477">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="e5529-478">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-478">string</span></span>|||<span data-ttu-id="e5529-479">Высота диалогов — число пикселей или макет по умолчанию, например "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="e5529-479">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="e5529-480">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-480">string</span></span>|||<span data-ttu-id="e5529-481">Начальный URL-адрес веб-просмотров.</span><span class="sxs-lookup"><span data-stu-id="e5529-481">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="e5529-482">массив объекта</span><span class="sxs-lookup"><span data-stu-id="e5529-482">array of object</span></span>|<span data-ttu-id="e5529-483">5 элементов</span><span class="sxs-lookup"><span data-stu-id="e5529-483">5 items</span></span>|<span data-ttu-id="e5529-484">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-484">✔</span></span>|<span data-ttu-id="e5529-485">Список параметров, которые принимает команда.</span><span class="sxs-lookup"><span data-stu-id="e5529-485">The list of parameters the command takes.</span></span> <span data-ttu-id="e5529-486">Минимум: 1; максимум: 5.</span><span class="sxs-lookup"><span data-stu-id="e5529-486">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="e5529-487">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-487">string</span></span>|<span data-ttu-id="e5529-488">64 символа</span><span class="sxs-lookup"><span data-stu-id="e5529-488">64 characters</span></span>|<span data-ttu-id="e5529-489">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-489">✔</span></span>|<span data-ttu-id="e5529-490">Имя параметра, как оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="e5529-490">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="e5529-491">Это включено в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="e5529-491">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="e5529-492">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-492">string</span></span>|<span data-ttu-id="e5529-493">32 символа</span><span class="sxs-lookup"><span data-stu-id="e5529-493">32 characters</span></span>|<span data-ttu-id="e5529-494">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-494">✔</span></span>|<span data-ttu-id="e5529-495">Удобное название для параметра.</span><span class="sxs-lookup"><span data-stu-id="e5529-495">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="e5529-496">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-496">string</span></span>|<span data-ttu-id="e5529-497">128 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-497">128 characters</span></span>||<span data-ttu-id="e5529-498">Удобное для пользователя строка, описываемая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="e5529-498">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="e5529-499">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-499">string</span></span>|<span data-ttu-id="e5529-500">512 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-500">512 characters</span></span>||<span data-ttu-id="e5529-501">Начальное значение для параметра.</span><span class="sxs-lookup"><span data-stu-id="e5529-501">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="e5529-502">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-502">string</span></span>|<span data-ttu-id="e5529-503">128 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-503">128 characters</span></span>||<span data-ttu-id="e5529-504">Определяет тип управления, отображаемого в модуле задач `fetchTask: true` для .</span><span class="sxs-lookup"><span data-stu-id="e5529-504">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="e5529-505">Один из `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="e5529-505">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="e5529-506">массив объектов</span><span class="sxs-lookup"><span data-stu-id="e5529-506">array of objects</span></span>|<span data-ttu-id="e5529-507">10 элементов</span><span class="sxs-lookup"><span data-stu-id="e5529-507">10 items</span></span>||<span data-ttu-id="e5529-508">Параметры выбора `choiceset` для .</span><span class="sxs-lookup"><span data-stu-id="e5529-508">The choice options for the`choiceset`.</span></span> <span data-ttu-id="e5529-509">Используйте только `parameter.inputType` тогда, когда `choiceset` это .</span><span class="sxs-lookup"><span data-stu-id="e5529-509">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="e5529-510">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-510">string</span></span>|<span data-ttu-id="e5529-511">128 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-511">128 characters</span></span>|<span data-ttu-id="e5529-512">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-512">✔</span></span>|<span data-ttu-id="e5529-513">Название выбора.</span><span class="sxs-lookup"><span data-stu-id="e5529-513">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="e5529-514">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-514">string</span></span>|<span data-ttu-id="e5529-515">512 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-515">512 characters</span></span>|<span data-ttu-id="e5529-516">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-516">✔</span></span>|<span data-ttu-id="e5529-517">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="e5529-517">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="e5529-518">permissions</span><span class="sxs-lookup"><span data-stu-id="e5529-518">permissions</span></span>

<span data-ttu-id="e5529-519">**Необязательный** — массив строк</span><span class="sxs-lookup"><span data-stu-id="e5529-519">**Optional** — array of strings</span></span>

<span data-ttu-id="e5529-520">Массив, в котором указывается, какие разрешения запрашивает приложение, что позволяет конечным пользователям `string` знать, как выполняется расширение.</span><span class="sxs-lookup"><span data-stu-id="e5529-520">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="e5529-521">Следующие параметры не являются эксклюзивными:</span><span class="sxs-lookup"><span data-stu-id="e5529-521">The following options are non-exclusive:</span></span>

* <span data-ttu-id="e5529-522">`identity`&emsp;Требуется информация о удостоверении пользователя.</span><span class="sxs-lookup"><span data-stu-id="e5529-522">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="e5529-523">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам группы.</span><span class="sxs-lookup"><span data-stu-id="e5529-523">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="e5529-524">Изменение этих разрешений во время обновления приложения заставляет пользователей повторять процесс согласия после запуска обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-524">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="e5529-525">Дополнительные [сведения см. в обновлении](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-525">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="e5529-526">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="e5529-526">devicePermissions</span></span>

<span data-ttu-id="e5529-527">**Необязательный** — массив строк</span><span class="sxs-lookup"><span data-stu-id="e5529-527">**Optional** — array of strings</span></span>

<span data-ttu-id="e5529-528">Предоставляет родных функций на устройстве пользователя, к которое ваше приложение запрашивает доступ.</span><span class="sxs-lookup"><span data-stu-id="e5529-528">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="e5529-529">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="e5529-529">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="e5529-530">validDomains</span><span class="sxs-lookup"><span data-stu-id="e5529-530">validDomains</span></span>

<span data-ttu-id="e5529-531">**Необязательный,** **за исключением обязательного,** где отмечено.</span><span class="sxs-lookup"><span data-stu-id="e5529-531">**Optional**, except **Required** where noted.</span></span>

<span data-ttu-id="e5529-532">Список допустимого домена для веб-сайтов, которые приложение ожидает загрузить в Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="e5529-532">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="e5529-533">Списки домена могут включать, например, поддиайки. `*.example.com`</span><span class="sxs-lookup"><span data-stu-id="e5529-533">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="e5529-534">Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="e5529-534">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="e5529-535">Если конфигурации вкладок или пользовательскому интерфейсу контента необходимо перейти к любому другому домену, кроме одного использования для конфигурации вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="e5529-535">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="e5529-536">Не обязательно **включать** в приложение домены поставщиков удостоверений, которые необходимо поддерживать.</span><span class="sxs-lookup"><span data-stu-id="e5529-536">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="e5529-537">Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить accounts.google.com, однако не следует включать accounts.google.com `validDomains[]` в .</span><span class="sxs-lookup"><span data-stu-id="e5529-537">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="e5529-538">Teams приложения, которые требуют нормальной работы собственных URL-адресов sharepoint, включают в допустимый список доменов "{teamsitedomain}".</span><span class="sxs-lookup"><span data-stu-id="e5529-538">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5529-539">Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью подкрентов.</span><span class="sxs-lookup"><span data-stu-id="e5529-539">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="e5529-540">Например, `yourapp.onmicrosoft.com` допустимо, однако, `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="e5529-540">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="e5529-541">Объект — массив со всеми элементами `string` типа.</span><span class="sxs-lookup"><span data-stu-id="e5529-541">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="e5529-542">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="e5529-542">webApplicationInfo</span></span>

<span data-ttu-id="e5529-543">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="e5529-543">**Optional** — object</span></span>

<span data-ttu-id="e5529-544">Предопишите Azure Active Directory (AAD) App ID и microsoft Graph, чтобы помочь пользователям без проблем войти в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="e5529-544">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="e5529-545">Если ваше приложение зарегистрировано в AAD, необходимо предоставить ID приложения, чтобы администраторы могли легко просмотреть разрешения и предоставить согласие Teams центре администрирования.</span><span class="sxs-lookup"><span data-stu-id="e5529-545">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="e5529-546">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-546">Name</span></span>| <span data-ttu-id="e5529-547">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-547">Type</span></span>| <span data-ttu-id="e5529-548">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-548">Maximum size</span></span> | <span data-ttu-id="e5529-549">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-549">Required</span></span> | <span data-ttu-id="e5529-550">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-550">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="e5529-551">string</span><span class="sxs-lookup"><span data-stu-id="e5529-551">string</span></span>|<span data-ttu-id="e5529-552">36 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-552">36 characters</span></span>|<span data-ttu-id="e5529-553">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-553">✔</span></span>|<span data-ttu-id="e5529-554">AAD-id приложения приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-554">AAD application id of the app.</span></span> <span data-ttu-id="e5529-555">Этот id должен быть GUID.</span><span class="sxs-lookup"><span data-stu-id="e5529-555">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="e5529-556">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-556">string</span></span>|<span data-ttu-id="e5529-557">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-557">2048 characters</span></span>|<span data-ttu-id="e5529-558">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-558">✔</span></span>|<span data-ttu-id="e5529-559">URL-адрес ресурса приложения для приобретения маркера auth для SSO.</span><span class="sxs-lookup"><span data-stu-id="e5529-559">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="e5529-560">**ПРИМЕЧАНИЕ:** Если вы не используете SSO, убедитесь, что вы вводите значение строки в этом поле в манифест приложения, например, чтобы избежать ответа https://notapplicable на ошибку.</span><span class="sxs-lookup"><span data-stu-id="e5529-560">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="e5529-561">массив строк</span><span class="sxs-lookup"><span data-stu-id="e5529-561">array of strings</span></span>|<span data-ttu-id="e5529-562">128 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-562">128 characters</span></span>||<span data-ttu-id="e5529-563">Укажите [конкретное согласие конкретного ресурса.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="e5529-563">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="e5529-564">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="e5529-564">showLoadingIndicator</span></span>

<span data-ttu-id="e5529-565">**Необязательный** — boolean</span><span class="sxs-lookup"><span data-stu-id="e5529-565">**Optional** — boolean</span></span>

<span data-ttu-id="e5529-566">Указывает, следует ли показывать индикатор загрузки при загрузке приложения или вкладки.</span><span class="sxs-lookup"><span data-stu-id="e5529-566">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="e5529-567">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="e5529-567">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="e5529-568">Если в манифесте приложения выбрано как верное, чтобы правильно загрузить страницу, измените страницы контента вкладок и модулей задач, как описано в документе Показать документ индикатора `showLoadingIndicator` загрузки. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="e5529-568">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="e5529-569">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="e5529-569">isFullScreen</span></span>

 <span data-ttu-id="e5529-570">**Необязательный** — boolean</span><span class="sxs-lookup"><span data-stu-id="e5529-570">**Optional** — boolean</span></span>

<span data-ttu-id="e5529-571">Указать, где отрисовка личного приложения с панели заголовки вкладок или без нее.</span><span class="sxs-lookup"><span data-stu-id="e5529-571">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="e5529-572">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="e5529-572">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="e5529-573">activities</span><span class="sxs-lookup"><span data-stu-id="e5529-573">activities</span></span>

<span data-ttu-id="e5529-574">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="e5529-574">**Optional** — object</span></span>

<span data-ttu-id="e5529-575">Определите свойства, которые приложение использует для публикации ленты действий пользователя.</span><span class="sxs-lookup"><span data-stu-id="e5529-575">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="e5529-576">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-576">Name</span></span>| <span data-ttu-id="e5529-577">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-577">Type</span></span>| <span data-ttu-id="e5529-578">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-578">Maximum size</span></span> | <span data-ttu-id="e5529-579">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-579">Required</span></span> | <span data-ttu-id="e5529-580">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-580">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="e5529-581">массив объектов</span><span class="sxs-lookup"><span data-stu-id="e5529-581">array of Objects</span></span>|<span data-ttu-id="e5529-582">128 элементов</span><span class="sxs-lookup"><span data-stu-id="e5529-582">128 items</span></span>| | <span data-ttu-id="e5529-583">Укапитайте типы действий, которые ваше приложение может размещать в канале действий пользователей.</span><span class="sxs-lookup"><span data-stu-id="e5529-583">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="e5529-584">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="e5529-584">activities.activityTypes</span></span>

|<span data-ttu-id="e5529-585">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-585">Name</span></span>| <span data-ttu-id="e5529-586">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-586">Type</span></span>| <span data-ttu-id="e5529-587">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-587">Maximum size</span></span> | <span data-ttu-id="e5529-588">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-588">Required</span></span> | <span data-ttu-id="e5529-589">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-589">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="e5529-590">string</span><span class="sxs-lookup"><span data-stu-id="e5529-590">string</span></span>|<span data-ttu-id="e5529-591">32 символа</span><span class="sxs-lookup"><span data-stu-id="e5529-591">32 characters</span></span>|<span data-ttu-id="e5529-592">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-592">✔</span></span>|<span data-ttu-id="e5529-593">Тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="e5529-593">The notification type.</span></span> <span data-ttu-id="e5529-594">*См. ниже*.</span><span class="sxs-lookup"><span data-stu-id="e5529-594">*See below*.</span></span>|
|`description`|<span data-ttu-id="e5529-595">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-595">string</span></span>|<span data-ttu-id="e5529-596">128 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-596">128 characters</span></span>|<span data-ttu-id="e5529-597">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-597">✔</span></span>|<span data-ttu-id="e5529-598">Краткое описание уведомления.</span><span class="sxs-lookup"><span data-stu-id="e5529-598">A brief description of the notification.</span></span> <span data-ttu-id="e5529-599">*См. ниже*.</span><span class="sxs-lookup"><span data-stu-id="e5529-599">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="e5529-600">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-600">string</span></span>|<span data-ttu-id="e5529-601">128 символов</span><span class="sxs-lookup"><span data-stu-id="e5529-601">128 characters</span></span>|<span data-ttu-id="e5529-602">✔</span><span class="sxs-lookup"><span data-stu-id="e5529-602">✔</span></span>|<span data-ttu-id="e5529-603">Ex: "{actor} создал задачу {taskId} для вас"</span><span class="sxs-lookup"><span data-stu-id="e5529-603">Ex: "{actor} created task {taskId} for you"</span></span>|

```json
{
   "activities":{
      "activityTypes":[
         {
            "type":"taskCreated",
            "description":"Task Created Activity",
            "templateText":"{actor} created task {taskId} for you"
         },
         {
            "type":"teamMention",
            "description":"Team Mention Activity",
            "templateText":"{actor} mentioned team"
         },
         {
            "type":"channelMention",
            "description":"Channel Mention Activity",
            "templateText":"{actor} mentioned channel"
         },
         {
            "type":"userMention",
            "description":"Personal Mention Activity",
            "templateText":"{actor} mentioned user"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"creatorTaskCreated",
            "description":"Created Task Created",
            "templateText":"The Creator created task {taskId} for you"
         }
      ]
   }
}
```

***

## <a name="defaultinstallscope"></a><span data-ttu-id="e5529-604">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="e5529-604">defaultInstallScope</span></span>

<span data-ttu-id="e5529-605">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="e5529-605">**Optional** - string</span></span>

<span data-ttu-id="e5529-606">Указывает область установки, определяемую для этого приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e5529-606">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="e5529-607">Определенным областью будет параметр, отображаемый на кнопке при добавлении приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="e5529-607">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="e5529-608">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="e5529-608">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="e5529-609">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="e5529-609">defaultGroupCapability</span></span>

<span data-ttu-id="e5529-610">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="e5529-610">**Optional** - object</span></span>

<span data-ttu-id="e5529-611">Когда будет выбрана область установки группы, она определит возможности по умолчанию при установке приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="e5529-611">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="e5529-612">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="e5529-612">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="e5529-613">Имя</span><span class="sxs-lookup"><span data-stu-id="e5529-613">Name</span></span>| <span data-ttu-id="e5529-614">Тип</span><span class="sxs-lookup"><span data-stu-id="e5529-614">Type</span></span>| <span data-ttu-id="e5529-615">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e5529-615">Maximum size</span></span> | <span data-ttu-id="e5529-616">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e5529-616">Required</span></span> | <span data-ttu-id="e5529-617">Описание</span><span class="sxs-lookup"><span data-stu-id="e5529-617">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="e5529-618">string</span><span class="sxs-lookup"><span data-stu-id="e5529-618">string</span></span>|||<span data-ttu-id="e5529-619">Если выбрана область установки, это поле указывает доступные возможности `team` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e5529-619">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="e5529-620">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="e5529-620">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="e5529-621">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-621">string</span></span>|||<span data-ttu-id="e5529-622">Если выбрана область установки, это поле указывает доступные возможности `groupchat` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e5529-622">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="e5529-623">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="e5529-623">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="e5529-624">строка</span><span class="sxs-lookup"><span data-stu-id="e5529-624">string</span></span>|||<span data-ttu-id="e5529-625">Если выбрана область установки, это поле указывает доступные возможности `meetings` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e5529-625">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="e5529-626">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="e5529-626">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="e5529-627">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="e5529-627">configurableProperties</span></span>

<span data-ttu-id="e5529-628">**Необязательный** - массив</span><span class="sxs-lookup"><span data-stu-id="e5529-628">**Optional** - array</span></span>

<span data-ttu-id="e5529-629">Блок определяет свойства приложений, которые может `configurableProperties` Teams администратор.</span><span class="sxs-lookup"><span data-stu-id="e5529-629">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="e5529-630">Дополнительные сведения см. [в Microsoft Teams.](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="e5529-630">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="e5529-631">Необходимо определить как минимум одно свойство.</span><span class="sxs-lookup"><span data-stu-id="e5529-631">A minimum of one property must be defined.</span></span> <span data-ttu-id="e5529-632">В этом блоке можно определить максимум девять свойств.</span><span class="sxs-lookup"><span data-stu-id="e5529-632">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="e5529-633">В качестве наилучшей практики необходимо предоставить рекомендации по настройке для пользователей и клиентов приложений, которые следует соблюдать при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-633">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span>

<span data-ttu-id="e5529-634">Можно определить любое из следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="e5529-634">You can define any of the following properties:</span></span>
* <span data-ttu-id="e5529-635">`name`: Позволяет администратору изменять имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-635">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="e5529-636">`shortDescription`: Позволяет администратору изменить краткое описание приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-636">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="e5529-637">`longDescription`: Позволяет администратору изменять подробное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="e5529-637">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="e5529-638">`smallImageUrl`. Это `outline` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="e5529-638">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="e5529-639">`largeImageUrl`. Это `color` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="e5529-639">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="e5529-640">`accentColor`. Это цвет, который можно использовать в сочетании с и в качестве фона для значков плана.</span><span class="sxs-lookup"><span data-stu-id="e5529-640">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="e5529-641">`websiteUrl`. Это https:// URL-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="e5529-641">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="e5529-642">`privacyUrl`. Это https:// url-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="e5529-642">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="e5529-643">`termsOfUseUrl`. Это https:// URL-адрес для условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="e5529-643">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>


