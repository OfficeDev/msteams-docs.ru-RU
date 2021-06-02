---
title: Справка о схеме манифеста
description: Описывает схему манифеста для Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: Схема манифеста команд
ms.openlocfilehash: d8427d23ba2caa73cecd173f6d1ef0d041252b3b
ms.sourcegitcommit: e50cdeb6b7f481e12911b2bb74a8da22af0bffac
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/01/2021
ms.locfileid: "52710629"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="d3ec8-104">Справка: схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d3ec8-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="d3ec8-105">Манифест Teams описывает, как приложение интегрируется в Microsoft Teams продукт.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="d3ec8-106">Манифест должен соответствовать схеме, которая была на [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) уровне .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="d3ec8-107">Поддерживаются и предыдущие версии 1.0, 1.1,..., 1.6 и так далее (с помощью "v1.x" в URL-адресе).</span><span class="sxs-lookup"><span data-stu-id="d3ec8-107">Previous versions 1.0, 1.1,..., 1.6, and so on are also supported (using "v1.x" in the URL).</span></span>
<span data-ttu-id="d3ec8-108">Дополнительные сведения об изменениях, внесенных в каждой версии, см. в [журнале изменений манифеста.](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-108">For more information on the changes made in each version, see [manifest change log](https://github.com/OfficeDev/microsoft-teams-app-schema/releases).</span></span>

<span data-ttu-id="d3ec8-109">В следующем примере схемы показаны все параметры экстензивности:</span><span class="sxs-lookup"><span data-stu-id="d3ec8-109">The following schema sample shows all extensibility options:</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="d3ec8-110">Образец полного манифеста</span><span class="sxs-lookup"><span data-stu-id="d3ec8-110">Sample full manifest</span></span>

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

<span data-ttu-id="d3ec8-111">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="d3ec8-111">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="d3ec8-112">$schema</span><span class="sxs-lookup"><span data-stu-id="d3ec8-112">$schema</span></span>

<span data-ttu-id="d3ec8-113">Необязательный, но рекомендуемый — строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-113">Optional, but recommended — string</span></span>

<span data-ttu-id="d3ec8-114">URL https:// ссылки на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-114">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="d3ec8-115">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="d3ec8-115">manifestVersion</span></span>

<span data-ttu-id="d3ec8-116">**Обязательно —** строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-116">**Required** — string</span></span>

<span data-ttu-id="d3ec8-117">Версия схемы манифеста, используемая этим манифестом.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-117">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="d3ec8-118">Должно быть 1.10.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-118">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="d3ec8-119">version</span><span class="sxs-lookup"><span data-stu-id="d3ec8-119">version</span></span>

<span data-ttu-id="d3ec8-120">**Обязательно —** строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-120">**Required** — string</span></span>

<span data-ttu-id="d3ec8-121">Версия определенного приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-121">The version of a specific app.</span></span> <span data-ttu-id="d3ec8-122">Если вы что-то обновите в манифесте, версия также должна быть приумножная.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-122">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="d3ec8-123">Таким образом, при установке нового манифеста он переописает существующий и пользователь получает новые функции.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-123">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="d3ec8-124">Если это приложение было отправлено в магазин, новый манифест должен быть повторно отправлен и повторно проверен.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-124">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="d3ec8-125">Пользователи приложения получают новый обновленный манифест автоматически в течение нескольких часов после утверждения манифеста.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-125">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="d3ec8-126">Если приложение запрашивает разрешения на изменение, пользователям будет предложено обновить и повторно согласиться на приложение.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-126">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="d3ec8-127">Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="d3ec8-127">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="d3ec8-128">id</span><span class="sxs-lookup"><span data-stu-id="d3ec8-128">id</span></span>

<span data-ttu-id="d3ec8-129">**Обязательно —** ID приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d3ec8-129">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="d3ec8-130">Идентификатор — уникальный идентификатор, созданный Корпорацией Майкрософт для приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-130">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="d3ec8-131">У вас есть ID, если бот зарегистрирован через Microsoft Bot Framework или веб-приложение вкладки уже вошел в Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-131">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="d3ec8-132">Здесь необходимо ввести ID.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-132">You must enter the ID here.</span></span> <span data-ttu-id="d3ec8-133">В противном случае необходимо создать новый ID на портале [регистрации приложений Майкрософт.](https://aka.ms/appregistrations)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-133">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="d3ec8-134">При добавлении бота используйте тот же ID.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-134">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="d3ec8-135">Если вы передаете обновление существующему приложению в AppSource, ID в манифесте не должен изменяться.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-135">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="d3ec8-136">developer</span><span class="sxs-lookup"><span data-stu-id="d3ec8-136">developer</span></span>

<span data-ttu-id="d3ec8-137">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="d3ec8-137">**Required** — object</span></span>

<span data-ttu-id="d3ec8-138">Указывает сведения о вашей компании.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-138">Specifies information about your company.</span></span> <span data-ttu-id="d3ec8-139">Для приложений, представленных в Teams магазине, эти значения должны соответствовать сведениям в списке магазина.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-139">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="d3ec8-140">Дополнительные сведения см. [в Teams руководства по публикации в магазине.](~/concepts/deploy-and-publish/appsource/publish.md)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-140">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="d3ec8-141">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-141">Name</span></span>| <span data-ttu-id="d3ec8-142">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-142">Maximum size</span></span> | <span data-ttu-id="d3ec8-143">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-143">Required</span></span> | <span data-ttu-id="d3ec8-144">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="d3ec8-145">32 символа</span><span class="sxs-lookup"><span data-stu-id="d3ec8-145">32 characters</span></span>|<span data-ttu-id="d3ec8-146">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-146">✔</span></span>|<span data-ttu-id="d3ec8-147">Имя отображения для разработчика.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="d3ec8-148">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-148">2048 characters</span></span>|<span data-ttu-id="d3ec8-149">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-149">✔</span></span>|<span data-ttu-id="d3ec8-150">Url https:// url-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="d3ec8-151">Эта ссылка должна принимать пользователей на страницу вашей компании или конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-151">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="d3ec8-152">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-152">2048 characters</span></span>|<span data-ttu-id="d3ec8-153">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-153">✔</span></span>|<span data-ttu-id="d3ec8-154">Url https:// url-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="d3ec8-155">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-155">2048 characters</span></span>|<span data-ttu-id="d3ec8-156">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-156">✔</span></span>|<span data-ttu-id="d3ec8-157">Url https:// url-адрес для условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="d3ec8-158">10 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-158">10 characters</span></span>| |<span data-ttu-id="d3ec8-159">**Необязательный** Идентификатор Сети партнеров Майкрософт, который определяет организацию-партнер, которая строит приложение.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-159">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="d3ec8-160">name</span><span class="sxs-lookup"><span data-stu-id="d3ec8-160">name</span></span>

<span data-ttu-id="d3ec8-161">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="d3ec8-161">**Required** — object</span></span>

<span data-ttu-id="d3ec8-162">Имя приложения, отображаемого пользователям в Teams.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-162">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="d3ec8-163">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-163">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="d3ec8-164">Значения и `short` должны `full` быть разными.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-164">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="d3ec8-165">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-165">Name</span></span>| <span data-ttu-id="d3ec8-166">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-166">Maximum size</span></span> | <span data-ttu-id="d3ec8-167">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-167">Required</span></span> | <span data-ttu-id="d3ec8-168">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-168">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="d3ec8-169">30 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-169">30 characters</span></span>|<span data-ttu-id="d3ec8-170">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-170">✔</span></span>|<span data-ttu-id="d3ec8-171">Короткое имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-171">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="d3ec8-172">100 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-172">100 characters</span></span>||<span data-ttu-id="d3ec8-173">Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-173">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="d3ec8-174">description</span><span class="sxs-lookup"><span data-stu-id="d3ec8-174">description</span></span>

<span data-ttu-id="d3ec8-175">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="d3ec8-175">**Required** — object</span></span>

<span data-ttu-id="d3ec8-176">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-176">Describes your app to users.</span></span> <span data-ttu-id="d3ec8-177">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-177">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="d3ec8-178">Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, чтобы помочь потенциальным клиентам понять, что делает ваш опыт.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-178">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="d3ec8-179">В полном описании необходимо учтите, что для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-179">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="d3ec8-180">Значения и `short` должны `full` быть разными.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-180">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="d3ec8-181">Короткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-181">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="d3ec8-182">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-182">Name</span></span>| <span data-ttu-id="d3ec8-183">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-183">Maximum size</span></span> | <span data-ttu-id="d3ec8-184">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-184">Required</span></span> | <span data-ttu-id="d3ec8-185">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-185">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="d3ec8-186">80 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-186">80 characters</span></span>|<span data-ttu-id="d3ec8-187">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-187">✔</span></span>|<span data-ttu-id="d3ec8-188">Краткое описание работы приложения, используемого при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-188">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="d3ec8-189">4000 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-189">4000 characters</span></span>|<span data-ttu-id="d3ec8-190">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-190">✔</span></span>|<span data-ttu-id="d3ec8-191">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-191">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="d3ec8-192">packageName</span><span class="sxs-lookup"><span data-stu-id="d3ec8-192">packageName</span></span>

<span data-ttu-id="d3ec8-193">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-193">**Optional** — string</span></span>

<span data-ttu-id="d3ec8-194">Уникальный идентификатор для приложения в обратной нотации домена; например, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-194">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="d3ec8-195">Максимальная длина: 64 символа.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-195">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="d3ec8-196">локализацияInfo</span><span class="sxs-lookup"><span data-stu-id="d3ec8-196">localizationInfo</span></span>

<span data-ttu-id="d3ec8-197">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="d3ec8-197">**Optional** — object</span></span>

<span data-ttu-id="d3ec8-198">Позволяет спецификацию языка по умолчанию, а также указатели для дополнительных языковых файлов.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-198">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="d3ec8-199">Дополнительные сведения см. в [деле локализации.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-199">For more information, see [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="d3ec8-200">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-200">Name</span></span>| <span data-ttu-id="d3ec8-201">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-201">Maximum size</span></span> | <span data-ttu-id="d3ec8-202">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-202">Required</span></span> | <span data-ttu-id="d3ec8-203">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-203">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="d3ec8-204">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-204">✔</span></span>|<span data-ttu-id="d3ec8-205">Языковой тег строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-205">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="d3ec8-206">локализацияInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="d3ec8-206">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="d3ec8-207">Массив объектов, указывающих дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-207">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="d3ec8-208">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-208">Name</span></span>| <span data-ttu-id="d3ec8-209">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-209">Maximum size</span></span> | <span data-ttu-id="d3ec8-210">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-210">Required</span></span> | <span data-ttu-id="d3ec8-211">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-211">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="d3ec8-212">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-212">✔</span></span>|<span data-ttu-id="d3ec8-213">Языковой тег строки в предоставленного файла.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-213">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="d3ec8-214">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-214">✔</span></span>|<span data-ttu-id="d3ec8-215">Относительный путь к файлу .json, содержащим переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-215">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="d3ec8-216">icons</span><span class="sxs-lookup"><span data-stu-id="d3ec8-216">icons</span></span>

<span data-ttu-id="d3ec8-217">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="d3ec8-217">**Required** — object</span></span>

<span data-ttu-id="d3ec8-218">Значки, используемые в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-218">Icons used within the Teams app.</span></span> <span data-ttu-id="d3ec8-219">Файлы значков должны быть включены в пакет отправки.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-219">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="d3ec8-220">Дополнительные сведения см. в [значках.](../../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-220">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="d3ec8-221">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-221">Name</span></span>| <span data-ttu-id="d3ec8-222">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-222">Maximum size</span></span> | <span data-ttu-id="d3ec8-223">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-223">Required</span></span> | <span data-ttu-id="d3ec8-224">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-224">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="d3ec8-225">32 x 32 пикселя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-225">32 x 32 pixels</span></span>|<span data-ttu-id="d3ec8-226">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-226">✔</span></span>|<span data-ttu-id="d3ec8-227">Относительный путь к прозрачному значку контура PNG 32x32.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-227">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="d3ec8-228">192 x 192 пикселя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-228">192 x 192 pixels</span></span>|<span data-ttu-id="d3ec8-229">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-229">✔</span></span>|<span data-ttu-id="d3ec8-230">Относительный путь к значку PNG полного цвета 192x192.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-230">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="d3ec8-231">accentColor</span><span class="sxs-lookup"><span data-stu-id="d3ec8-231">accentColor</span></span>

<span data-ttu-id="d3ec8-232">**Необязательный** — цветовой код HTML Hex</span><span class="sxs-lookup"><span data-stu-id="d3ec8-232">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="d3ec8-233">Цвет, который можно использовать в сочетании с и в качестве фона для значков контура.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-233">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="d3ec8-234">Значение должно быть допустимым цветовым кодом HTML, начиная, например, с `#4464ee` "#".</span><span class="sxs-lookup"><span data-stu-id="d3ec8-234">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="d3ec8-235">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="d3ec8-235">configurableTabs</span></span>

<span data-ttu-id="d3ec8-236">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="d3ec8-236">**Optional** — array</span></span>

<span data-ttu-id="d3ec8-237">Используется, когда в вашем приложении есть опыт работы с вкладками канала команды, которая требует дополнительной конфигурации перед ее добавлением.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-237">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="d3ec8-238">Настраиваемые вкладки поддерживаются только в области команд, и вы можете настроить те же вкладки несколько раз.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-238">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="d3ec8-239">Однако определить его в манифесте можно только один раз.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-239">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="d3ec8-240">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-240">Name</span></span>| <span data-ttu-id="d3ec8-241">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-241">Type</span></span>| <span data-ttu-id="d3ec8-242">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-242">Maximum size</span></span> | <span data-ttu-id="d3ec8-243">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-243">Required</span></span> | <span data-ttu-id="d3ec8-244">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="d3ec8-245">string</span><span class="sxs-lookup"><span data-stu-id="d3ec8-245">string</span></span>|<span data-ttu-id="d3ec8-246">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-246">2048 characters</span></span>|<span data-ttu-id="d3ec8-247">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-247">✔</span></span>|<span data-ttu-id="d3ec8-248">URL-https://, который можно использовать при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-248">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="d3ec8-249">массив enums</span><span class="sxs-lookup"><span data-stu-id="d3ec8-249">array of enums</span></span>|<span data-ttu-id="d3ec8-250">1</span><span class="sxs-lookup"><span data-stu-id="d3ec8-250">1</span></span>|<span data-ttu-id="d3ec8-251">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-251">✔</span></span>|<span data-ttu-id="d3ec8-252">В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-252">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="d3ec8-253">boolean</span><span class="sxs-lookup"><span data-stu-id="d3ec8-253">boolean</span></span>|||<span data-ttu-id="d3ec8-254">Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-254">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="d3ec8-255">По умолчанию: **true**.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-255">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="d3ec8-256">массив enums</span><span class="sxs-lookup"><span data-stu-id="d3ec8-256">array of enums</span></span>|<span data-ttu-id="d3ec8-257">6 </span><span class="sxs-lookup"><span data-stu-id="d3ec8-257">6</span></span>||<span data-ttu-id="d3ec8-258">Набор `contextItem` областей, в которых [вкладка поддерживается.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-258">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="d3ec8-259">По умолчанию: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-259">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="d3ec8-260">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-260">string</span></span>|<span data-ttu-id="d3ec8-261">2048</span><span class="sxs-lookup"><span data-stu-id="d3ec8-261">2048</span></span>||<span data-ttu-id="d3ec8-262">Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-262">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="d3ec8-263">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-263">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="d3ec8-264">массив enums</span><span class="sxs-lookup"><span data-stu-id="d3ec8-264">array of enums</span></span>|<span data-ttu-id="d3ec8-265">1</span><span class="sxs-lookup"><span data-stu-id="d3ec8-265">1</span></span>||<span data-ttu-id="d3ec8-266">Определяет, как вкладка доступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-266">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="d3ec8-267">Параметры `sharePointFullPage` и `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="d3ec8-267">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="d3ec8-268">staticTabs</span><span class="sxs-lookup"><span data-stu-id="d3ec8-268">staticTabs</span></span>

<span data-ttu-id="d3ec8-269">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="d3ec8-269">**Optional** — array</span></span>

<span data-ttu-id="d3ec8-270">Определяет набор вкладок, которые можно "прикрепить" по умолчанию, не добавляя их вручную.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-270">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="d3ec8-271">Статические вкладки, объявленные в области, всегда прикрепяются к личному опыту `personal` приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-271">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="d3ec8-272">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-272">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="d3ec8-273">Этот элемент — массив (не более 16 элементов) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-273">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="d3ec8-274">Этот блок требуется только для решений, которые предоставляют статическое решение вкладки.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-274">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="d3ec8-275">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-275">Name</span></span>| <span data-ttu-id="d3ec8-276">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-276">Type</span></span>| <span data-ttu-id="d3ec8-277">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-277">Maximum size</span></span> | <span data-ttu-id="d3ec8-278">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-278">Required</span></span> | <span data-ttu-id="d3ec8-279">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-279">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="d3ec8-280">string</span><span class="sxs-lookup"><span data-stu-id="d3ec8-280">string</span></span>|<span data-ttu-id="d3ec8-281">64 символа</span><span class="sxs-lookup"><span data-stu-id="d3ec8-281">64 characters</span></span>|<span data-ttu-id="d3ec8-282">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-282">✔</span></span>|<span data-ttu-id="d3ec8-283">Уникальный идентификатор для объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-283">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="d3ec8-284">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-284">string</span></span>|<span data-ttu-id="d3ec8-285">128 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-285">128 characters</span></span>|<span data-ttu-id="d3ec8-286">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-286">✔</span></span>|<span data-ttu-id="d3ec8-287">Отображение имени вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-287">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="d3ec8-288">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-288">string</span></span>||<span data-ttu-id="d3ec8-289">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-289">✔</span></span>|<span data-ttu-id="d3ec8-290">URL https://, который указывает на пользовательский интерфейс объекта, отображаемого на Teams холсте.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-290">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="d3ec8-291">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-291">string</span></span>|||<span data-ttu-id="d3ec8-292">Url https://, чтобы указать, выбирает ли пользователь просмотр в браузере.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-292">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="d3ec8-293">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-293">string</span></span>|||<span data-ttu-id="d3ec8-294">Url https://, на который нужно указать для поисковых запросов пользователя.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-294">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="d3ec8-295">массив enums</span><span class="sxs-lookup"><span data-stu-id="d3ec8-295">array of enums</span></span>|<span data-ttu-id="d3ec8-296">1</span><span class="sxs-lookup"><span data-stu-id="d3ec8-296">1</span></span>|<span data-ttu-id="d3ec8-297">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-297">✔</span></span>|<span data-ttu-id="d3ec8-298">В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в `personal` рамках личного опыта.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-298">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="d3ec8-299">массив enums</span><span class="sxs-lookup"><span data-stu-id="d3ec8-299">array of enums</span></span>| <span data-ttu-id="d3ec8-300">2</span><span class="sxs-lookup"><span data-stu-id="d3ec8-300">2</span></span>|| <span data-ttu-id="d3ec8-301">Набор `contextItem` областей, в которых поддерживается вкладка.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-301">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="d3ec8-302">Функция searchUrl недоступна сторонним разработчикам.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-302">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="d3ec8-303">Если для отображения соответствующего контента или для инициации потока проверки подлинности в вкладке Get context для вашей вкладки Microsoft Teams контексте, дополнительные сведения см. в статье Get context for [your Microsoft Teams.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-303">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="d3ec8-304">боты</span><span class="sxs-lookup"><span data-stu-id="d3ec8-304">bots</span></span>

<span data-ttu-id="d3ec8-305">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="d3ec8-305">**Optional** — array</span></span>

<span data-ttu-id="d3ec8-306">Определяет решение бота, а также необязательные сведения, такие как свойства команд по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-306">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="d3ec8-307">Элемент — массив (максимум 1 элемент в настоящее время разрешен только для одного бота в приложении) со всеми элементами &mdash; типа `object` .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-307">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="d3ec8-308">Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-308">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="d3ec8-309">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-309">Name</span></span>| <span data-ttu-id="d3ec8-310">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-310">Type</span></span>| <span data-ttu-id="d3ec8-311">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-311">Maximum size</span></span> | <span data-ttu-id="d3ec8-312">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-312">Required</span></span> | <span data-ttu-id="d3ec8-313">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-313">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="d3ec8-314">string</span><span class="sxs-lookup"><span data-stu-id="d3ec8-314">string</span></span>|<span data-ttu-id="d3ec8-315">64 символа</span><span class="sxs-lookup"><span data-stu-id="d3ec8-315">64 characters</span></span>|<span data-ttu-id="d3ec8-316">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-316">✔</span></span>|<span data-ttu-id="d3ec8-317">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-317">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="d3ec8-318">Это вполне может быть таким же, как общий [ID приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="d3ec8-318">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="d3ec8-319">массив enums</span><span class="sxs-lookup"><span data-stu-id="d3ec8-319">array of enums</span></span>|<span data-ttu-id="d3ec8-320">3</span><span class="sxs-lookup"><span data-stu-id="d3ec8-320">3</span></span>|<span data-ttu-id="d3ec8-321">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-321">✔</span></span>|<span data-ttu-id="d3ec8-322">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="d3ec8-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="d3ec8-323">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-323">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="d3ec8-324">boolean</span><span class="sxs-lookup"><span data-stu-id="d3ec8-324">boolean</span></span>|||<span data-ttu-id="d3ec8-325">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-325">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="d3ec8-326">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="d3ec8-326">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="d3ec8-327">boolean</span><span class="sxs-lookup"><span data-stu-id="d3ec8-327">boolean</span></span>|||<span data-ttu-id="d3ec8-328">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-328">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="d3ec8-329">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="d3ec8-329">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="d3ec8-330">boolean</span><span class="sxs-lookup"><span data-stu-id="d3ec8-330">boolean</span></span>|||<span data-ttu-id="d3ec8-331">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-331">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="d3ec8-332">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="d3ec8-332">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="d3ec8-333">boolean</span><span class="sxs-lookup"><span data-stu-id="d3ec8-333">boolean</span></span>|||<span data-ttu-id="d3ec8-334">Значение, указывающее, где бот поддерживает звуковые вызовы.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-334">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="d3ec8-335">**ВАЖНО.** Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="d3ec8-336">Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="d3ec8-337">Она предоставляется только для тестирования и разведки и не должна использоваться в производственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-337">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="d3ec8-338">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="d3ec8-338">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="d3ec8-339">boolean</span><span class="sxs-lookup"><span data-stu-id="d3ec8-339">boolean</span></span>|||<span data-ttu-id="d3ec8-340">Значение, указывающее, где бот поддерживает видеозвонков.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-340">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="d3ec8-341">**ВАЖНО.** Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-341">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="d3ec8-342">Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-342">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="d3ec8-343">Она предоставляется только для тестирования и разведки и не должна использоваться в производственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-343">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="d3ec8-344">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="d3ec8-344">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="d3ec8-345">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="d3ec8-345">bots.commandLists</span></span>

<span data-ttu-id="d3ec8-346">Необязательный список команд, которые бот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-346">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="d3ec8-347">Объект — массив (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-347">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="d3ec8-348">Дополнительные [сведения см. в](~/bots/how-to/create-a-bot-commands-menu.md) меню Bot.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-348">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="d3ec8-349">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-349">Name</span></span>| <span data-ttu-id="d3ec8-350">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-350">Type</span></span>| <span data-ttu-id="d3ec8-351">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-351">Maximum size</span></span> | <span data-ttu-id="d3ec8-352">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-352">Required</span></span> | <span data-ttu-id="d3ec8-353">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-353">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="d3ec8-354">массив enums</span><span class="sxs-lookup"><span data-stu-id="d3ec8-354">array of enums</span></span>|<span data-ttu-id="d3ec8-355">3</span><span class="sxs-lookup"><span data-stu-id="d3ec8-355">3</span></span>|<span data-ttu-id="d3ec8-356">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-356">✔</span></span>|<span data-ttu-id="d3ec8-357">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-357">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="d3ec8-358">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-358">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="d3ec8-359">массив объектов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-359">array of objects</span></span>|<span data-ttu-id="d3ec8-360">10 </span><span class="sxs-lookup"><span data-stu-id="d3ec8-360">10</span></span>|<span data-ttu-id="d3ec8-361">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-361">✔</span></span>|<span data-ttu-id="d3ec8-362">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="d3ec8-362">An array of commands the bot supports:</span></span><br><span data-ttu-id="d3ec8-363">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-363">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="d3ec8-364">`description`: простое описание или пример синтаксиса команды и его аргумента (строка, 128).</span><span class="sxs-lookup"><span data-stu-id="d3ec8-364">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="d3ec8-365">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="d3ec8-365">bots.commandLists.commands</span></span>

|<span data-ttu-id="d3ec8-366">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-366">Name</span></span>| <span data-ttu-id="d3ec8-367">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-367">Type</span></span>| <span data-ttu-id="d3ec8-368">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-368">Maximum size</span></span> | <span data-ttu-id="d3ec8-369">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-369">Required</span></span> | <span data-ttu-id="d3ec8-370">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-370">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="d3ec8-371">title</span><span class="sxs-lookup"><span data-stu-id="d3ec8-371">title</span></span>|<span data-ttu-id="d3ec8-372">string</span><span class="sxs-lookup"><span data-stu-id="d3ec8-372">string</span></span>|<span data-ttu-id="d3ec8-373">12 </span><span class="sxs-lookup"><span data-stu-id="d3ec8-373">12</span></span>|<span data-ttu-id="d3ec8-374">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-374">✔</span></span>|<span data-ttu-id="d3ec8-375">Имя команды бота.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-375">The bot command name.</span></span>|
|<span data-ttu-id="d3ec8-376">description</span><span class="sxs-lookup"><span data-stu-id="d3ec8-376">description</span></span>|<span data-ttu-id="d3ec8-377">string</span><span class="sxs-lookup"><span data-stu-id="d3ec8-377">string</span></span>|<span data-ttu-id="d3ec8-378">128 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-378">128 characters</span></span>|<span data-ttu-id="d3ec8-379">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-379">✔</span></span>|<span data-ttu-id="d3ec8-380">Простое текстовое описание или пример синтаксиса команд и его аргументов.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-380">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="d3ec8-381">соединители</span><span class="sxs-lookup"><span data-stu-id="d3ec8-381">connectors</span></span>

<span data-ttu-id="d3ec8-382">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="d3ec8-382">**Optional** — array</span></span>

<span data-ttu-id="d3ec8-383">Блок `connectors` определяет Office 365 соединители для приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-383">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="d3ec8-384">Объект — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-384">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="d3ec8-385">Этот блок необходим только для решений, которые предоставляют соединители.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-385">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="d3ec8-386">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-386">Name</span></span>| <span data-ttu-id="d3ec8-387">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-387">Type</span></span>| <span data-ttu-id="d3ec8-388">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-388">Maximum size</span></span> | <span data-ttu-id="d3ec8-389">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-389">Required</span></span> | <span data-ttu-id="d3ec8-390">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-390">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="d3ec8-391">string</span><span class="sxs-lookup"><span data-stu-id="d3ec8-391">string</span></span>|<span data-ttu-id="d3ec8-392">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-392">2048 characters</span></span>|<span data-ttu-id="d3ec8-393">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-393">✔</span></span>|<span data-ttu-id="d3ec8-394">URL https://, который необходимо использовать при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-394">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="d3ec8-395">массив enums</span><span class="sxs-lookup"><span data-stu-id="d3ec8-395">array of enums</span></span>|<span data-ttu-id="d3ec8-396">1</span><span class="sxs-lookup"><span data-stu-id="d3ec8-396">1</span></span>|<span data-ttu-id="d3ec8-397">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-397">✔</span></span>|<span data-ttu-id="d3ec8-398">Указывает, предоставляет ли соединители опыт в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="d3ec8-398">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="d3ec8-399">В настоящее время `team` поддерживается только область.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-399">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="d3ec8-400">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-400">string</span></span>|<span data-ttu-id="d3ec8-401">64 символа</span><span class="sxs-lookup"><span data-stu-id="d3ec8-401">64 characters</span></span>|<span data-ttu-id="d3ec8-402">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-402">✔</span></span>|<span data-ttu-id="d3ec8-403">Уникальный идентификатор соединитетеля, который соответствует его идентификатору в панели мониторинга разработчиков [соединителок.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-403">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="d3ec8-404">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="d3ec8-404">composeExtensions</span></span>

<span data-ttu-id="d3ec8-405">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="d3ec8-405">**Optional** — array</span></span>

<span data-ttu-id="d3ec8-406">Определяет расширение обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-406">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="d3ec8-407">В ноябре 2017 г. имя функции было изменено с "расширение составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжили функционировать.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-407">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="d3ec8-408">Элемент — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-408">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="d3ec8-409">Этот блок необходим только для решений, которые предоставляют расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-409">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="d3ec8-410">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-410">Name</span></span>| <span data-ttu-id="d3ec8-411">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-411">Type</span></span> | <span data-ttu-id="d3ec8-412">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-412">Maximum Size</span></span> | <span data-ttu-id="d3ec8-413">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-413">Required</span></span> | <span data-ttu-id="d3ec8-414">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-414">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="d3ec8-415">string</span><span class="sxs-lookup"><span data-stu-id="d3ec8-415">string</span></span>|<span data-ttu-id="d3ec8-416">64</span><span class="sxs-lookup"><span data-stu-id="d3ec8-416">64</span></span>|<span data-ttu-id="d3ec8-417">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-417">✔</span></span>|<span data-ttu-id="d3ec8-418">Уникальный ID приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрирован в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-418">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="d3ec8-419">Это вполне может быть таким же, как и общий ID приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-419">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="d3ec8-420">массив объектов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-420">array of objects</span></span>|<span data-ttu-id="d3ec8-421">10 </span><span class="sxs-lookup"><span data-stu-id="d3ec8-421">10</span></span>|<span data-ttu-id="d3ec8-422">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-422">✔</span></span>|<span data-ttu-id="d3ec8-423">Массив команд, поддерживаемых расширением обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-423">Array of commands the messaging extension supports.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="d3ec8-424">boolean</span><span class="sxs-lookup"><span data-stu-id="d3ec8-424">boolean</span></span>|||<span data-ttu-id="d3ec8-425">Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-425">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="d3ec8-426">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-426">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="d3ec8-427">массив объектов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-427">array of Objects</span></span>|<span data-ttu-id="d3ec8-428">5 </span><span class="sxs-lookup"><span data-stu-id="d3ec8-428">5</span></span>||<span data-ttu-id="d3ec8-429">Список обработчиков, которые позволяют вызывать приложения при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-429">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="d3ec8-430">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-430">string</span></span>|||<span data-ttu-id="d3ec8-431">Тип обработка сообщений.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-431">The type of message handler.</span></span> <span data-ttu-id="d3ec8-432">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-432">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="d3ec8-433">массив строк</span><span class="sxs-lookup"><span data-stu-id="d3ec8-433">array of Strings</span></span>|||<span data-ttu-id="d3ec8-434">Массив доменов, для которые обработник сообщений ссылок может зарегистрироваться.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-434">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="d3ec8-435">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="d3ec8-435">composeExtensions.commands</span></span>

<span data-ttu-id="d3ec8-436">Расширение обмена сообщениями должно объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-436">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="d3ec8-437">Каждая команда отображается Microsoft Teams как потенциальное взаимодействие с точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-437">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="d3ec8-438">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-438">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="d3ec8-439">Каждый элемент команды — это объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="d3ec8-439">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="d3ec8-440">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-440">Name</span></span>| <span data-ttu-id="d3ec8-441">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-441">Type</span></span>| <span data-ttu-id="d3ec8-442">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-442">Maximum size</span></span> | <span data-ttu-id="d3ec8-443">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-443">Required</span></span> | <span data-ttu-id="d3ec8-444">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-444">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="d3ec8-445">string</span><span class="sxs-lookup"><span data-stu-id="d3ec8-445">string</span></span>|<span data-ttu-id="d3ec8-446">64 символа</span><span class="sxs-lookup"><span data-stu-id="d3ec8-446">64 characters</span></span>|<span data-ttu-id="d3ec8-447">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-447">✔</span></span>|<span data-ttu-id="d3ec8-448">ID для команды.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-448">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="d3ec8-449">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-449">string</span></span>|<span data-ttu-id="d3ec8-450">32 символа</span><span class="sxs-lookup"><span data-stu-id="d3ec8-450">32 characters</span></span>|<span data-ttu-id="d3ec8-451">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-451">✔</span></span>|<span data-ttu-id="d3ec8-452">Удобное имя команды.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-452">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="d3ec8-453">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-453">string</span></span>|<span data-ttu-id="d3ec8-454">64 символа</span><span class="sxs-lookup"><span data-stu-id="d3ec8-454">64 characters</span></span>||<span data-ttu-id="d3ec8-455">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-455">Type of the command.</span></span> <span data-ttu-id="d3ec8-456">Один `query` из или `action` .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-456">One of `query` or `action`.</span></span> <span data-ttu-id="d3ec8-457">По умолчанию: **запрос**.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-457">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="d3ec8-458">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-458">string</span></span>|<span data-ttu-id="d3ec8-459">128 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-459">128 characters</span></span>||<span data-ttu-id="d3ec8-460">В описании, которое отображается пользователями, указывается назначение этой команды.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-460">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="d3ec8-461">boolean</span><span class="sxs-lookup"><span data-stu-id="d3ec8-461">boolean</span></span>|||<span data-ttu-id="d3ec8-462">Значение boolean указывает, выполняется ли команда изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-462">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="d3ec8-463">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-463">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="d3ec8-464">массив строк</span><span class="sxs-lookup"><span data-stu-id="d3ec8-464">array of Strings</span></span>|<span data-ttu-id="d3ec8-465">3</span><span class="sxs-lookup"><span data-stu-id="d3ec8-465">3</span></span>||<span data-ttu-id="d3ec8-466">Определяет, из чего можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-466">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="d3ec8-467">Любое сочетание `compose` `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-467">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="d3ec8-468">Значение по умолчанию: `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-468">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="d3ec8-469">boolean</span><span class="sxs-lookup"><span data-stu-id="d3ec8-469">boolean</span></span>|||<span data-ttu-id="d3ec8-470">Значение boolean, которое указывает, должен ли он динамически получать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-470">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="d3ec8-471">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-471">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="d3ec8-472">объект</span><span class="sxs-lookup"><span data-stu-id="d3ec8-472">object</span></span>|||<span data-ttu-id="d3ec8-473">Укажите модуль задач для предварительной загрузки при использовании команды расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-473">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="d3ec8-474">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-474">string</span></span>|<span data-ttu-id="d3ec8-475">64 символа</span><span class="sxs-lookup"><span data-stu-id="d3ec8-475">64 characters</span></span>||<span data-ttu-id="d3ec8-476">Начальное название диалогов.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-476">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="d3ec8-477">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-477">string</span></span>|||<span data-ttu-id="d3ec8-478">Ширина диалогов — число в пикселях или макет по умолчанию, такие как "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="d3ec8-478">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="d3ec8-479">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-479">string</span></span>|||<span data-ttu-id="d3ec8-480">Высота диалогов — число пикселей или макет по умолчанию, например "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="d3ec8-480">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="d3ec8-481">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-481">string</span></span>|||<span data-ttu-id="d3ec8-482">Начальный URL-адрес веб-просмотров.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-482">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="d3ec8-483">массив объекта</span><span class="sxs-lookup"><span data-stu-id="d3ec8-483">array of object</span></span>|<span data-ttu-id="d3ec8-484">5 элементов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-484">5 items</span></span>|<span data-ttu-id="d3ec8-485">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-485">✔</span></span>|<span data-ttu-id="d3ec8-486">Список параметров, которые принимает команда.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-486">The list of parameters the command takes.</span></span> <span data-ttu-id="d3ec8-487">Минимум: 1; максимум: 5.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-487">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="d3ec8-488">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-488">string</span></span>|<span data-ttu-id="d3ec8-489">64 символа</span><span class="sxs-lookup"><span data-stu-id="d3ec8-489">64 characters</span></span>|<span data-ttu-id="d3ec8-490">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-490">✔</span></span>|<span data-ttu-id="d3ec8-491">Имя параметра, как оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-491">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="d3ec8-492">Это включено в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-492">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="d3ec8-493">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-493">string</span></span>|<span data-ttu-id="d3ec8-494">32 символа</span><span class="sxs-lookup"><span data-stu-id="d3ec8-494">32 characters</span></span>|<span data-ttu-id="d3ec8-495">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-495">✔</span></span>|<span data-ttu-id="d3ec8-496">Удобное название для параметра.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-496">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="d3ec8-497">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-497">string</span></span>|<span data-ttu-id="d3ec8-498">128 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-498">128 characters</span></span>||<span data-ttu-id="d3ec8-499">Удобное для пользователя строка, описываемая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-499">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="d3ec8-500">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-500">string</span></span>|<span data-ttu-id="d3ec8-501">512 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-501">512 characters</span></span>||<span data-ttu-id="d3ec8-502">Начальное значение для параметра.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-502">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="d3ec8-503">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-503">string</span></span>|<span data-ttu-id="d3ec8-504">128 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-504">128 characters</span></span>||<span data-ttu-id="d3ec8-505">Определяет тип управления, отображаемого в модуле задач `fetchTask: true` для .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-505">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="d3ec8-506">Один из `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-506">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="d3ec8-507">массив объектов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-507">array of objects</span></span>|<span data-ttu-id="d3ec8-508">10 элементов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-508">10 items</span></span>||<span data-ttu-id="d3ec8-509">Параметры выбора `choiceset` для .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-509">The choice options for the`choiceset`.</span></span> <span data-ttu-id="d3ec8-510">Используйте только `parameter.inputType` тогда, когда `choiceset` это .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-510">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="d3ec8-511">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-511">string</span></span>|<span data-ttu-id="d3ec8-512">128 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-512">128 characters</span></span>|<span data-ttu-id="d3ec8-513">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-513">✔</span></span>|<span data-ttu-id="d3ec8-514">Название выбора.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-514">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="d3ec8-515">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-515">string</span></span>|<span data-ttu-id="d3ec8-516">512 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-516">512 characters</span></span>|<span data-ttu-id="d3ec8-517">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-517">✔</span></span>|<span data-ttu-id="d3ec8-518">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-518">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="d3ec8-519">permissions</span><span class="sxs-lookup"><span data-stu-id="d3ec8-519">permissions</span></span>

<span data-ttu-id="d3ec8-520">**Необязательный** — массив строк</span><span class="sxs-lookup"><span data-stu-id="d3ec8-520">**Optional** — array of strings</span></span>

<span data-ttu-id="d3ec8-521">Массив, в котором указывается, какие разрешения запрашивает приложение, что позволяет конечным пользователям `string` знать, как выполняется расширение.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-521">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="d3ec8-522">Следующие параметры не являются эксклюзивными:</span><span class="sxs-lookup"><span data-stu-id="d3ec8-522">The following options are non-exclusive:</span></span>

* <span data-ttu-id="d3ec8-523">`identity`&emsp;Требуется информация о удостоверении пользователя.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-523">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="d3ec8-524">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам группы.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-524">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="d3ec8-525">Изменение этих разрешений во время обновления приложения заставляет пользователей повторять процесс согласия после запуска обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-525">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="d3ec8-526">Дополнительные [сведения см. в обновлении](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-526">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="d3ec8-527">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="d3ec8-527">devicePermissions</span></span>

<span data-ttu-id="d3ec8-528">**Необязательный** — массив строк</span><span class="sxs-lookup"><span data-stu-id="d3ec8-528">**Optional** — array of strings</span></span>

<span data-ttu-id="d3ec8-529">Предоставляет родных функций на устройстве пользователя, к которое ваше приложение запрашивает доступ.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-529">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="d3ec8-530">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="d3ec8-530">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="d3ec8-531">validDomains</span><span class="sxs-lookup"><span data-stu-id="d3ec8-531">validDomains</span></span>

<span data-ttu-id="d3ec8-532">**Необязательный,** **за исключением обязательного,** где отмечено.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-532">**Optional**, except **Required** where noted.</span></span>

<span data-ttu-id="d3ec8-533">Список допустимого домена для веб-сайтов, которые приложение ожидает загрузить в Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-533">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="d3ec8-534">Списки домена могут включать, например, поддиайки. `*.example.com`</span><span class="sxs-lookup"><span data-stu-id="d3ec8-534">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="d3ec8-535">Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-535">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="d3ec8-536">Если конфигурации вкладок или пользовательскому интерфейсу контента необходимо перейти к любому другому домену, кроме одного использования для конфигурации вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-536">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="d3ec8-537">Не обязательно **включать** в приложение домены поставщиков удостоверений, которые необходимо поддерживать.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-537">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="d3ec8-538">Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить accounts.google.com, однако не следует включать accounts.google.com `validDomains[]` в .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-538">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="d3ec8-539">Teams приложения, которые требуют нормальной работы собственных URL-адресов sharepoint, включают в допустимый список доменов "{teamsitedomain}".</span><span class="sxs-lookup"><span data-stu-id="d3ec8-539">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3ec8-540">Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью подкрентов.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-540">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="d3ec8-541">Например, `yourapp.onmicrosoft.com` допустимо, однако, `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-541">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="d3ec8-542">Объект — массив со всеми элементами `string` типа.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-542">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="d3ec8-543">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="d3ec8-543">webApplicationInfo</span></span>

<span data-ttu-id="d3ec8-544">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="d3ec8-544">**Optional** — object</span></span>

<span data-ttu-id="d3ec8-545">Предопишите Azure Active Directory (AAD) App ID и microsoft Graph, чтобы помочь пользователям без проблем войти в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-545">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="d3ec8-546">Если ваше приложение зарегистрировано в AAD, необходимо предоставить ID приложения, чтобы администраторы могли легко просмотреть разрешения и предоставить согласие Teams центре администрирования.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-546">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="d3ec8-547">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-547">Name</span></span>| <span data-ttu-id="d3ec8-548">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-548">Type</span></span>| <span data-ttu-id="d3ec8-549">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-549">Maximum size</span></span> | <span data-ttu-id="d3ec8-550">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-550">Required</span></span> | <span data-ttu-id="d3ec8-551">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-551">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="d3ec8-552">string</span><span class="sxs-lookup"><span data-stu-id="d3ec8-552">string</span></span>|<span data-ttu-id="d3ec8-553">36 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-553">36 characters</span></span>|<span data-ttu-id="d3ec8-554">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-554">✔</span></span>|<span data-ttu-id="d3ec8-555">AAD-id приложения приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-555">AAD application id of the app.</span></span> <span data-ttu-id="d3ec8-556">Этот id должен быть GUID.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-556">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="d3ec8-557">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-557">string</span></span>|<span data-ttu-id="d3ec8-558">2048 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-558">2048 characters</span></span>|<span data-ttu-id="d3ec8-559">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-559">✔</span></span>|<span data-ttu-id="d3ec8-560">URL-адрес ресурса приложения для приобретения маркера auth для SSO.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-560">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="d3ec8-561">**ПРИМЕЧАНИЕ:** Если вы не используете SSO, убедитесь, что вы вводите значение строки в этом поле в манифест приложения, например, чтобы избежать ответа https://notapplicable на ошибку.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-561">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="d3ec8-562">массив строк</span><span class="sxs-lookup"><span data-stu-id="d3ec8-562">array of strings</span></span>|<span data-ttu-id="d3ec8-563">128 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-563">128 characters</span></span>||<span data-ttu-id="d3ec8-564">Укажите [конкретное согласие конкретного ресурса.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-564">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="d3ec8-565">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="d3ec8-565">showLoadingIndicator</span></span>

<span data-ttu-id="d3ec8-566">**Необязательный** — boolean</span><span class="sxs-lookup"><span data-stu-id="d3ec8-566">**Optional** — boolean</span></span>

<span data-ttu-id="d3ec8-567">Указывает, следует ли показывать индикатор загрузки при загрузке приложения или вкладки.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-567">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="d3ec8-568">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-568">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="d3ec8-569">Если в манифесте приложения выбрано как верное, чтобы правильно загрузить страницу, измените страницы контента вкладок и модулей задач, как описано в документе Показать документ индикатора `showLoadingIndicator` загрузки. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-569">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="d3ec8-570">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="d3ec8-570">isFullScreen</span></span>

 <span data-ttu-id="d3ec8-571">**Необязательный** — boolean</span><span class="sxs-lookup"><span data-stu-id="d3ec8-571">**Optional** — boolean</span></span>

<span data-ttu-id="d3ec8-572">Указать, где отрисовка личного приложения с панели заголовки вкладок или без нее.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-572">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="d3ec8-573">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-573">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="d3ec8-574">activities</span><span class="sxs-lookup"><span data-stu-id="d3ec8-574">activities</span></span>

<span data-ttu-id="d3ec8-575">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="d3ec8-575">**Optional** — object</span></span>

<span data-ttu-id="d3ec8-576">Определите свойства, которые приложение использует для публикации ленты действий пользователя.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-576">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="d3ec8-577">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-577">Name</span></span>| <span data-ttu-id="d3ec8-578">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-578">Type</span></span>| <span data-ttu-id="d3ec8-579">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-579">Maximum size</span></span> | <span data-ttu-id="d3ec8-580">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-580">Required</span></span> | <span data-ttu-id="d3ec8-581">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-581">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="d3ec8-582">массив объектов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-582">array of Objects</span></span>|<span data-ttu-id="d3ec8-583">128 элементов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-583">128 items</span></span>| | <span data-ttu-id="d3ec8-584">Укапитайте типы действий, которые ваше приложение может размещать в канале действий пользователей.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-584">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="d3ec8-585">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="d3ec8-585">activities.activityTypes</span></span>

|<span data-ttu-id="d3ec8-586">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-586">Name</span></span>| <span data-ttu-id="d3ec8-587">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-587">Type</span></span>| <span data-ttu-id="d3ec8-588">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-588">Maximum size</span></span> | <span data-ttu-id="d3ec8-589">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-589">Required</span></span> | <span data-ttu-id="d3ec8-590">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-590">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="d3ec8-591">string</span><span class="sxs-lookup"><span data-stu-id="d3ec8-591">string</span></span>|<span data-ttu-id="d3ec8-592">32 символа</span><span class="sxs-lookup"><span data-stu-id="d3ec8-592">32 characters</span></span>|<span data-ttu-id="d3ec8-593">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-593">✔</span></span>|<span data-ttu-id="d3ec8-594">Тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-594">The notification type.</span></span> <span data-ttu-id="d3ec8-595">*См. ниже*.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-595">*See below*.</span></span>|
|`description`|<span data-ttu-id="d3ec8-596">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-596">string</span></span>|<span data-ttu-id="d3ec8-597">128 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-597">128 characters</span></span>|<span data-ttu-id="d3ec8-598">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-598">✔</span></span>|<span data-ttu-id="d3ec8-599">Краткое описание уведомления.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-599">A brief description of the notification.</span></span> <span data-ttu-id="d3ec8-600">*См. ниже*.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-600">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="d3ec8-601">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-601">string</span></span>|<span data-ttu-id="d3ec8-602">128 символов</span><span class="sxs-lookup"><span data-stu-id="d3ec8-602">128 characters</span></span>|<span data-ttu-id="d3ec8-603">✔</span><span class="sxs-lookup"><span data-stu-id="d3ec8-603">✔</span></span>|<span data-ttu-id="d3ec8-604">Ex: "{actor} создал задачу {taskId} для вас"</span><span class="sxs-lookup"><span data-stu-id="d3ec8-604">Ex: "{actor} created task {taskId} for you"</span></span>|

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

## <a name="defaultinstallscope"></a><span data-ttu-id="d3ec8-605">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="d3ec8-605">defaultInstallScope</span></span>

<span data-ttu-id="d3ec8-606">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-606">**Optional** - string</span></span>

<span data-ttu-id="d3ec8-607">Указывает область установки, определяемую для этого приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-607">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="d3ec8-608">Определенным областью будет параметр, отображаемый на кнопке при добавлении приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-608">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="d3ec8-609">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="d3ec8-609">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="d3ec8-610">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="d3ec8-610">defaultGroupCapability</span></span>

<span data-ttu-id="d3ec8-611">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="d3ec8-611">**Optional** - object</span></span>

<span data-ttu-id="d3ec8-612">Когда будет выбрана область установки группы, она определит возможности по умолчанию при установке приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-612">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="d3ec8-613">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="d3ec8-613">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="d3ec8-614">Имя</span><span class="sxs-lookup"><span data-stu-id="d3ec8-614">Name</span></span>| <span data-ttu-id="d3ec8-615">Тип</span><span class="sxs-lookup"><span data-stu-id="d3ec8-615">Type</span></span>| <span data-ttu-id="d3ec8-616">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="d3ec8-616">Maximum size</span></span> | <span data-ttu-id="d3ec8-617">Обязательный</span><span class="sxs-lookup"><span data-stu-id="d3ec8-617">Required</span></span> | <span data-ttu-id="d3ec8-618">Описание</span><span class="sxs-lookup"><span data-stu-id="d3ec8-618">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="d3ec8-619">string</span><span class="sxs-lookup"><span data-stu-id="d3ec8-619">string</span></span>|||<span data-ttu-id="d3ec8-620">Если выбрана область установки, это поле указывает доступные возможности `team` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-620">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="d3ec8-621">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-621">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="d3ec8-622">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-622">string</span></span>|||<span data-ttu-id="d3ec8-623">Если выбрана область установки, это поле указывает доступные возможности `groupchat` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-623">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="d3ec8-624">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-624">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="d3ec8-625">Строка</span><span class="sxs-lookup"><span data-stu-id="d3ec8-625">string</span></span>|||<span data-ttu-id="d3ec8-626">Если выбрана область установки, это поле указывает доступные возможности `meetings` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-626">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="d3ec8-627">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="d3ec8-627">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="d3ec8-628">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="d3ec8-628">configurableProperties</span></span>

<span data-ttu-id="d3ec8-629">**Необязательный** - массив</span><span class="sxs-lookup"><span data-stu-id="d3ec8-629">**Optional** - array</span></span>

<span data-ttu-id="d3ec8-630">Блок определяет свойства приложений, которые может `configurableProperties` Teams администратор.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-630">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="d3ec8-631">Дополнительные сведения см. [в Microsoft Teams.](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="d3ec8-631">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="d3ec8-632">Необходимо определить как минимум одно свойство.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-632">A minimum of one property must be defined.</span></span> <span data-ttu-id="d3ec8-633">В этом блоке можно определить максимум девять свойств.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-633">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="d3ec8-634">В качестве наилучшей практики необходимо предоставить рекомендации по настройке для пользователей и клиентов приложений, которые следует соблюдать при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-634">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span>

<span data-ttu-id="d3ec8-635">Можно определить любое из следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="d3ec8-635">You can define any of the following properties:</span></span>
* <span data-ttu-id="d3ec8-636">`name`: Позволяет администратору изменять имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-636">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="d3ec8-637">`shortDescription`: Позволяет администратору изменить краткое описание приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-637">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="d3ec8-638">`longDescription`: Позволяет администратору изменять подробное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-638">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="d3ec8-639">`smallImageUrl`. Это `outline` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-639">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="d3ec8-640">`largeImageUrl`. Это `color` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-640">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="d3ec8-641">`accentColor`. Это цвет, который можно использовать в сочетании с и в качестве фона для значков плана.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-641">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="d3ec8-642">`websiteUrl`. Это https:// URL-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-642">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="d3ec8-643">`privacyUrl`. Это https:// url-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-643">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="d3ec8-644">`termsOfUseUrl`. Это https:// URL-адрес для условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="d3ec8-644">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>


