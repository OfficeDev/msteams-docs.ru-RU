---
title: Справка о схеме манифеста
description: Описывает схему манифеста для Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: Схема манифеста команд
ms.openlocfilehash: 75c29a1cf9c2897d7b419b45bfc1a4f0447c7aa3
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853531"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="bfe22-104">Справка: схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bfe22-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="bfe22-105">Манифест Teams описывает, как приложение интегрируется в Microsoft Teams продукт.</span><span class="sxs-lookup"><span data-stu-id="bfe22-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="bfe22-106">Манифест должен соответствовать схеме, которая была на [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) уровне .</span><span class="sxs-lookup"><span data-stu-id="bfe22-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="bfe22-107">Поддерживаются и предыдущие версии 1.0, 1.1,..., 1.6 и так далее (с помощью "v1.x" в URL-адресе).</span><span class="sxs-lookup"><span data-stu-id="bfe22-107">Previous versions 1.0, 1.1,..., 1.6, and so on are also supported (using "v1.x" in the URL).</span></span>
<span data-ttu-id="bfe22-108">Дополнительные сведения об изменениях, внесенных в каждой версии, см. в [журнале изменений манифеста.](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)</span><span class="sxs-lookup"><span data-stu-id="bfe22-108">For more information on the changes made in each version, see [manifest change log](https://github.com/OfficeDev/microsoft-teams-app-schema/releases).</span></span>

<span data-ttu-id="bfe22-109">В следующем примере схемы показаны все параметры экстензивности:</span><span class="sxs-lookup"><span data-stu-id="bfe22-109">The following schema sample shows all extensibility options:</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="bfe22-110">Образец полного манифеста</span><span class="sxs-lookup"><span data-stu-id="bfe22-110">Sample full manifest</span></span>

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
     "developerUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ]              
}
```

<span data-ttu-id="bfe22-111">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="bfe22-111">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="bfe22-112">$schema</span><span class="sxs-lookup"><span data-stu-id="bfe22-112">$schema</span></span>

<span data-ttu-id="bfe22-113">Необязательный, но рекомендуемый — строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-113">Optional, but recommended — string</span></span>

<span data-ttu-id="bfe22-114">URL https:// ссылки на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="bfe22-114">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="bfe22-115">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="bfe22-115">manifestVersion</span></span>

<span data-ttu-id="bfe22-116">**Обязательно —** строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-116">**Required** — string</span></span>

<span data-ttu-id="bfe22-117">Версия схемы манифеста, используемая этим манифестом.</span><span class="sxs-lookup"><span data-stu-id="bfe22-117">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="bfe22-118">Должно быть 1.10.</span><span class="sxs-lookup"><span data-stu-id="bfe22-118">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="bfe22-119">version</span><span class="sxs-lookup"><span data-stu-id="bfe22-119">version</span></span>

<span data-ttu-id="bfe22-120">**Обязательно —** строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-120">**Required** — string</span></span>

<span data-ttu-id="bfe22-121">Версия определенного приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-121">The version of a specific app.</span></span> <span data-ttu-id="bfe22-122">Если вы что-то обновите в манифесте, версия также должна быть приумножная.</span><span class="sxs-lookup"><span data-stu-id="bfe22-122">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="bfe22-123">Таким образом, при установке нового манифеста он переописает существующий и пользователь получает новые функции.</span><span class="sxs-lookup"><span data-stu-id="bfe22-123">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="bfe22-124">Если это приложение было отправлено в магазин, новый манифест должен быть повторно отправлен и повторно проверен.</span><span class="sxs-lookup"><span data-stu-id="bfe22-124">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="bfe22-125">Пользователи приложения получают новый обновленный манифест автоматически в течение нескольких часов после утверждения манифеста.</span><span class="sxs-lookup"><span data-stu-id="bfe22-125">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="bfe22-126">Если приложение запрашивает разрешения на изменение, пользователям будет предложено обновить и повторно согласиться на приложение.</span><span class="sxs-lookup"><span data-stu-id="bfe22-126">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="bfe22-127">Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="bfe22-127">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="bfe22-128">id</span><span class="sxs-lookup"><span data-stu-id="bfe22-128">id</span></span>

<span data-ttu-id="bfe22-129">**Обязательно —** ID приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="bfe22-129">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="bfe22-130">Идентификатор — уникальный идентификатор, созданный Корпорацией Майкрософт для приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-130">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="bfe22-131">У вас есть ID, если бот зарегистрирован через Microsoft Bot Framework или веб-приложение вкладки уже вошел в Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bfe22-131">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="bfe22-132">Здесь необходимо ввести ID.</span><span class="sxs-lookup"><span data-stu-id="bfe22-132">You must enter the ID here.</span></span> <span data-ttu-id="bfe22-133">В противном случае необходимо создать новый ID на портале [регистрации приложений Майкрософт.](https://aka.ms/appregistrations)</span><span class="sxs-lookup"><span data-stu-id="bfe22-133">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="bfe22-134">При добавлении бота используйте тот же ID.</span><span class="sxs-lookup"><span data-stu-id="bfe22-134">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="bfe22-135">Если вы передаете обновление существующему приложению в AppSource, ID в манифесте не должен изменяться.</span><span class="sxs-lookup"><span data-stu-id="bfe22-135">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="bfe22-136">developer</span><span class="sxs-lookup"><span data-stu-id="bfe22-136">developer</span></span>

<span data-ttu-id="bfe22-137">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="bfe22-137">**Required** — object</span></span>

<span data-ttu-id="bfe22-138">Указывает сведения о вашей компании.</span><span class="sxs-lookup"><span data-stu-id="bfe22-138">Specifies information about your company.</span></span> <span data-ttu-id="bfe22-139">Для приложений, представленных в Teams магазине, эти значения должны соответствовать сведениям в списке магазина.</span><span class="sxs-lookup"><span data-stu-id="bfe22-139">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="bfe22-140">Дополнительные сведения см. [в Teams руководства по публикации в магазине.](~/concepts/deploy-and-publish/appsource/publish.md)</span><span class="sxs-lookup"><span data-stu-id="bfe22-140">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="bfe22-141">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-141">Name</span></span>| <span data-ttu-id="bfe22-142">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-142">Maximum size</span></span> | <span data-ttu-id="bfe22-143">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-143">Required</span></span> | <span data-ttu-id="bfe22-144">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="bfe22-145">32 символа</span><span class="sxs-lookup"><span data-stu-id="bfe22-145">32 characters</span></span>|<span data-ttu-id="bfe22-146">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-146">✔</span></span>|<span data-ttu-id="bfe22-147">Имя отображения для разработчика.</span><span class="sxs-lookup"><span data-stu-id="bfe22-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="bfe22-148">2048 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-148">2048 characters</span></span>|<span data-ttu-id="bfe22-149">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-149">✔</span></span>|<span data-ttu-id="bfe22-150">Url https:// url-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="bfe22-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="bfe22-151">Эта ссылка должна принимать пользователей на страницу вашей компании или конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="bfe22-151">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="bfe22-152">2048 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-152">2048 characters</span></span>|<span data-ttu-id="bfe22-153">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-153">✔</span></span>|<span data-ttu-id="bfe22-154">Url https:// url-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="bfe22-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="bfe22-155">2048 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-155">2048 characters</span></span>|<span data-ttu-id="bfe22-156">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-156">✔</span></span>|<span data-ttu-id="bfe22-157">Url https:// url-адрес для условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="bfe22-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="bfe22-158">10 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-158">10 characters</span></span>| |<span data-ttu-id="bfe22-159">**Необязательный** Идентификатор Сети партнеров Майкрософт, который определяет организацию-партнер, которая строит приложение.</span><span class="sxs-lookup"><span data-stu-id="bfe22-159">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="bfe22-160">name</span><span class="sxs-lookup"><span data-stu-id="bfe22-160">name</span></span>

<span data-ttu-id="bfe22-161">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="bfe22-161">**Required** — object</span></span>

<span data-ttu-id="bfe22-162">Имя приложения, отображаемого пользователям в Teams.</span><span class="sxs-lookup"><span data-stu-id="bfe22-162">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="bfe22-163">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="bfe22-163">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="bfe22-164">Значения и `short` должны `full` быть разными.</span><span class="sxs-lookup"><span data-stu-id="bfe22-164">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="bfe22-165">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-165">Name</span></span>| <span data-ttu-id="bfe22-166">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-166">Maximum size</span></span> | <span data-ttu-id="bfe22-167">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-167">Required</span></span> | <span data-ttu-id="bfe22-168">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-168">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="bfe22-169">30 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-169">30 characters</span></span>|<span data-ttu-id="bfe22-170">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-170">✔</span></span>|<span data-ttu-id="bfe22-171">Короткое имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-171">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="bfe22-172">100 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-172">100 characters</span></span>||<span data-ttu-id="bfe22-173">Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="bfe22-173">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="bfe22-174">description</span><span class="sxs-lookup"><span data-stu-id="bfe22-174">description</span></span>

<span data-ttu-id="bfe22-175">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="bfe22-175">**Required** — object</span></span>

<span data-ttu-id="bfe22-176">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="bfe22-176">Describes your app to users.</span></span> <span data-ttu-id="bfe22-177">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="bfe22-177">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="bfe22-178">Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, чтобы помочь потенциальным клиентам понять, что делает ваш опыт.</span><span class="sxs-lookup"><span data-stu-id="bfe22-178">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="bfe22-179">В полном описании необходимо учтите, что для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="bfe22-179">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="bfe22-180">Значения и `short` должны `full` быть разными.</span><span class="sxs-lookup"><span data-stu-id="bfe22-180">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="bfe22-181">Короткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-181">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="bfe22-182">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-182">Name</span></span>| <span data-ttu-id="bfe22-183">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-183">Maximum size</span></span> | <span data-ttu-id="bfe22-184">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-184">Required</span></span> | <span data-ttu-id="bfe22-185">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-185">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="bfe22-186">80 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-186">80 characters</span></span>|<span data-ttu-id="bfe22-187">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-187">✔</span></span>|<span data-ttu-id="bfe22-188">Краткое описание работы приложения, используемого при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="bfe22-188">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="bfe22-189">4000 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-189">4000 characters</span></span>|<span data-ttu-id="bfe22-190">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-190">✔</span></span>|<span data-ttu-id="bfe22-191">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-191">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="bfe22-192">packageName</span><span class="sxs-lookup"><span data-stu-id="bfe22-192">packageName</span></span>

<span data-ttu-id="bfe22-193">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-193">**Optional** — string</span></span>

<span data-ttu-id="bfe22-194">Уникальный идентификатор для приложения в обратной нотации домена; например, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="bfe22-194">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="bfe22-195">Максимальная длина: 64 символа.</span><span class="sxs-lookup"><span data-stu-id="bfe22-195">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="bfe22-196">локализацияInfo</span><span class="sxs-lookup"><span data-stu-id="bfe22-196">localizationInfo</span></span>

<span data-ttu-id="bfe22-197">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="bfe22-197">**Optional** — object</span></span>

<span data-ttu-id="bfe22-198">Позволяет спецификацию языка по умолчанию, а также указатели для дополнительных языковых файлов.</span><span class="sxs-lookup"><span data-stu-id="bfe22-198">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="bfe22-199">Дополнительные сведения см. в [деле локализации.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="bfe22-199">For more information, see [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="bfe22-200">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-200">Name</span></span>| <span data-ttu-id="bfe22-201">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-201">Maximum size</span></span> | <span data-ttu-id="bfe22-202">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-202">Required</span></span> | <span data-ttu-id="bfe22-203">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-203">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="bfe22-204">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-204">✔</span></span>|<span data-ttu-id="bfe22-205">Языковой тег строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="bfe22-205">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="bfe22-206">локализацияInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="bfe22-206">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="bfe22-207">Массив объектов, указывающих дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="bfe22-207">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="bfe22-208">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-208">Name</span></span>| <span data-ttu-id="bfe22-209">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-209">Maximum size</span></span> | <span data-ttu-id="bfe22-210">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-210">Required</span></span> | <span data-ttu-id="bfe22-211">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-211">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="bfe22-212">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-212">✔</span></span>|<span data-ttu-id="bfe22-213">Языковой тег строки в предоставленного файла.</span><span class="sxs-lookup"><span data-stu-id="bfe22-213">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="bfe22-214">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-214">✔</span></span>|<span data-ttu-id="bfe22-215">Относительный путь к файлу .json, содержащим переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="bfe22-215">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="bfe22-216">icons</span><span class="sxs-lookup"><span data-stu-id="bfe22-216">icons</span></span>

<span data-ttu-id="bfe22-217">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="bfe22-217">**Required** — object</span></span>

<span data-ttu-id="bfe22-218">Значки, используемые в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="bfe22-218">Icons used within the Teams app.</span></span> <span data-ttu-id="bfe22-219">Файлы значков должны быть включены в пакет отправки.</span><span class="sxs-lookup"><span data-stu-id="bfe22-219">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="bfe22-220">Дополнительные сведения см. в [значках.](../../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="bfe22-220">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="bfe22-221">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-221">Name</span></span>| <span data-ttu-id="bfe22-222">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-222">Maximum size</span></span> | <span data-ttu-id="bfe22-223">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-223">Required</span></span> | <span data-ttu-id="bfe22-224">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-224">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="bfe22-225">32 x 32 пикселя</span><span class="sxs-lookup"><span data-stu-id="bfe22-225">32 x 32 pixels</span></span>|<span data-ttu-id="bfe22-226">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-226">✔</span></span>|<span data-ttu-id="bfe22-227">Относительный путь к прозрачному значку контура PNG 32x32.</span><span class="sxs-lookup"><span data-stu-id="bfe22-227">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="bfe22-228">192 x 192 пикселя</span><span class="sxs-lookup"><span data-stu-id="bfe22-228">192 x 192 pixels</span></span>|<span data-ttu-id="bfe22-229">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-229">✔</span></span>|<span data-ttu-id="bfe22-230">Относительный путь к значку PNG полного цвета 192x192.</span><span class="sxs-lookup"><span data-stu-id="bfe22-230">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="bfe22-231">accentColor</span><span class="sxs-lookup"><span data-stu-id="bfe22-231">accentColor</span></span>

<span data-ttu-id="bfe22-232">**Необязательный** — цветовой код HTML Hex</span><span class="sxs-lookup"><span data-stu-id="bfe22-232">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="bfe22-233">Цвет, который можно использовать в сочетании с и в качестве фона для значков контура.</span><span class="sxs-lookup"><span data-stu-id="bfe22-233">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="bfe22-234">Значение должно быть допустимым цветовым кодом HTML, начиная, например, с `#4464ee` "#".</span><span class="sxs-lookup"><span data-stu-id="bfe22-234">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="bfe22-235">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="bfe22-235">configurableTabs</span></span>

<span data-ttu-id="bfe22-236">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="bfe22-236">**Optional** — array</span></span>

<span data-ttu-id="bfe22-237">Используется, когда в вашем приложении есть опыт работы с вкладками канала команды, которая требует дополнительной конфигурации перед ее добавлением.</span><span class="sxs-lookup"><span data-stu-id="bfe22-237">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="bfe22-238">Настраиваемые вкладки поддерживаются только в области команд, и вы можете настроить те же вкладки несколько раз.</span><span class="sxs-lookup"><span data-stu-id="bfe22-238">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="bfe22-239">Однако определить его в манифесте можно только один раз.</span><span class="sxs-lookup"><span data-stu-id="bfe22-239">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="bfe22-240">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-240">Name</span></span>| <span data-ttu-id="bfe22-241">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-241">Type</span></span>| <span data-ttu-id="bfe22-242">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-242">Maximum size</span></span> | <span data-ttu-id="bfe22-243">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-243">Required</span></span> | <span data-ttu-id="bfe22-244">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="bfe22-245">string</span><span class="sxs-lookup"><span data-stu-id="bfe22-245">string</span></span>|<span data-ttu-id="bfe22-246">2048 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-246">2048 characters</span></span>|<span data-ttu-id="bfe22-247">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-247">✔</span></span>|<span data-ttu-id="bfe22-248">URL-https://, который можно использовать при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="bfe22-248">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="bfe22-249">массив enums</span><span class="sxs-lookup"><span data-stu-id="bfe22-249">array of enums</span></span>|<span data-ttu-id="bfe22-250">1</span><span class="sxs-lookup"><span data-stu-id="bfe22-250">1</span></span>|<span data-ttu-id="bfe22-251">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-251">✔</span></span>|<span data-ttu-id="bfe22-252">В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области.</span><span class="sxs-lookup"><span data-stu-id="bfe22-252">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="bfe22-253">boolean</span><span class="sxs-lookup"><span data-stu-id="bfe22-253">boolean</span></span>|||<span data-ttu-id="bfe22-254">Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания.</span><span class="sxs-lookup"><span data-stu-id="bfe22-254">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="bfe22-255">По умолчанию: **true**.</span><span class="sxs-lookup"><span data-stu-id="bfe22-255">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="bfe22-256">массив enums</span><span class="sxs-lookup"><span data-stu-id="bfe22-256">array of enums</span></span>|<span data-ttu-id="bfe22-257">6 </span><span class="sxs-lookup"><span data-stu-id="bfe22-257">6</span></span>||<span data-ttu-id="bfe22-258">Набор `contextItem` областей, в которых [вкладка поддерживается.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="bfe22-258">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="bfe22-259">По умолчанию: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="bfe22-259">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="bfe22-260">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-260">string</span></span>|<span data-ttu-id="bfe22-261">2048</span><span class="sxs-lookup"><span data-stu-id="bfe22-261">2048</span></span>||<span data-ttu-id="bfe22-262">Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bfe22-262">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="bfe22-263">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="bfe22-263">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="bfe22-264">массив enums</span><span class="sxs-lookup"><span data-stu-id="bfe22-264">array of enums</span></span>|<span data-ttu-id="bfe22-265">1</span><span class="sxs-lookup"><span data-stu-id="bfe22-265">1</span></span>||<span data-ttu-id="bfe22-266">Определяет, как вкладка доступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bfe22-266">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="bfe22-267">Параметры `sharePointFullPage` и `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="bfe22-267">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="bfe22-268">staticTabs</span><span class="sxs-lookup"><span data-stu-id="bfe22-268">staticTabs</span></span>

<span data-ttu-id="bfe22-269">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="bfe22-269">**Optional** — array</span></span>

<span data-ttu-id="bfe22-270">Определяет набор вкладок, которые можно "прикрепить" по умолчанию, не добавляя их вручную.</span><span class="sxs-lookup"><span data-stu-id="bfe22-270">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="bfe22-271">Статические вкладки, объявленные в области, всегда прикрепяются к личному опыту `personal` приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-271">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="bfe22-272">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="bfe22-272">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="bfe22-273">Этот элемент — массив (не более 16 элементов) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="bfe22-273">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="bfe22-274">Этот блок требуется только для решений, которые предоставляют статическое решение вкладки.</span><span class="sxs-lookup"><span data-stu-id="bfe22-274">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="bfe22-275">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-275">Name</span></span>| <span data-ttu-id="bfe22-276">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-276">Type</span></span>| <span data-ttu-id="bfe22-277">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-277">Maximum size</span></span> | <span data-ttu-id="bfe22-278">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-278">Required</span></span> | <span data-ttu-id="bfe22-279">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-279">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="bfe22-280">string</span><span class="sxs-lookup"><span data-stu-id="bfe22-280">string</span></span>|<span data-ttu-id="bfe22-281">64 символа</span><span class="sxs-lookup"><span data-stu-id="bfe22-281">64 characters</span></span>|<span data-ttu-id="bfe22-282">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-282">✔</span></span>|<span data-ttu-id="bfe22-283">Уникальный идентификатор для объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="bfe22-283">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="bfe22-284">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-284">string</span></span>|<span data-ttu-id="bfe22-285">128 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-285">128 characters</span></span>|<span data-ttu-id="bfe22-286">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-286">✔</span></span>|<span data-ttu-id="bfe22-287">Отображение имени вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="bfe22-287">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="bfe22-288">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-288">string</span></span>||<span data-ttu-id="bfe22-289">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-289">✔</span></span>|<span data-ttu-id="bfe22-290">URL https://, который указывает на пользовательский интерфейс объекта, отображаемого на Teams холсте.</span><span class="sxs-lookup"><span data-stu-id="bfe22-290">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="bfe22-291">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-291">string</span></span>|||<span data-ttu-id="bfe22-292">Url https://, чтобы указать, выбирает ли пользователь просмотр в браузере.</span><span class="sxs-lookup"><span data-stu-id="bfe22-292">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="bfe22-293">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-293">string</span></span>|||<span data-ttu-id="bfe22-294">Url https://, на который нужно указать для поисковых запросов пользователя.</span><span class="sxs-lookup"><span data-stu-id="bfe22-294">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="bfe22-295">массив enums</span><span class="sxs-lookup"><span data-stu-id="bfe22-295">array of enums</span></span>|<span data-ttu-id="bfe22-296">1</span><span class="sxs-lookup"><span data-stu-id="bfe22-296">1</span></span>|<span data-ttu-id="bfe22-297">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-297">✔</span></span>|<span data-ttu-id="bfe22-298">В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в `personal` рамках личного опыта.</span><span class="sxs-lookup"><span data-stu-id="bfe22-298">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="bfe22-299">массив enums</span><span class="sxs-lookup"><span data-stu-id="bfe22-299">array of enums</span></span>| <span data-ttu-id="bfe22-300">2</span><span class="sxs-lookup"><span data-stu-id="bfe22-300">2</span></span>|| <span data-ttu-id="bfe22-301">Набор `contextItem` областей, в которых поддерживается вкладка.</span><span class="sxs-lookup"><span data-stu-id="bfe22-301">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="bfe22-302">Функция searchUrl недоступна сторонним разработчикам.</span><span class="sxs-lookup"><span data-stu-id="bfe22-302">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="bfe22-303">Если для отображения соответствующего контента или для инициации потока проверки подлинности в вкладке Get context для вашей вкладки Microsoft Teams контексте, дополнительные сведения см. в статье Get context for [your Microsoft Teams.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="bfe22-303">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="bfe22-304">боты</span><span class="sxs-lookup"><span data-stu-id="bfe22-304">bots</span></span>

<span data-ttu-id="bfe22-305">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="bfe22-305">**Optional** — array</span></span>

<span data-ttu-id="bfe22-306">Определяет решение бота, а также необязательные сведения, такие как свойства команд по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bfe22-306">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="bfe22-307">Элемент — массив (максимум 1 элемент в настоящее время разрешен только для одного бота в приложении) со всеми элементами &mdash; типа `object` .</span><span class="sxs-lookup"><span data-stu-id="bfe22-307">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="bfe22-308">Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.</span><span class="sxs-lookup"><span data-stu-id="bfe22-308">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="bfe22-309">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-309">Name</span></span>| <span data-ttu-id="bfe22-310">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-310">Type</span></span>| <span data-ttu-id="bfe22-311">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-311">Maximum size</span></span> | <span data-ttu-id="bfe22-312">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-312">Required</span></span> | <span data-ttu-id="bfe22-313">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-313">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="bfe22-314">string</span><span class="sxs-lookup"><span data-stu-id="bfe22-314">string</span></span>|<span data-ttu-id="bfe22-315">64 символа</span><span class="sxs-lookup"><span data-stu-id="bfe22-315">64 characters</span></span>|<span data-ttu-id="bfe22-316">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-316">✔</span></span>|<span data-ttu-id="bfe22-317">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="bfe22-317">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="bfe22-318">Это вполне может быть таким же, как общий [ID приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="bfe22-318">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="bfe22-319">массив enums</span><span class="sxs-lookup"><span data-stu-id="bfe22-319">array of enums</span></span>|<span data-ttu-id="bfe22-320">3</span><span class="sxs-lookup"><span data-stu-id="bfe22-320">3</span></span>|<span data-ttu-id="bfe22-321">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-321">✔</span></span>|<span data-ttu-id="bfe22-322">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="bfe22-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="bfe22-323">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="bfe22-323">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="bfe22-324">boolean</span><span class="sxs-lookup"><span data-stu-id="bfe22-324">boolean</span></span>|||<span data-ttu-id="bfe22-325">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="bfe22-325">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="bfe22-326">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="bfe22-326">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="bfe22-327">boolean</span><span class="sxs-lookup"><span data-stu-id="bfe22-327">boolean</span></span>|||<span data-ttu-id="bfe22-328">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="bfe22-328">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="bfe22-329">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="bfe22-329">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="bfe22-330">boolean</span><span class="sxs-lookup"><span data-stu-id="bfe22-330">boolean</span></span>|||<span data-ttu-id="bfe22-331">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="bfe22-331">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="bfe22-332">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="bfe22-332">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="bfe22-333">boolean</span><span class="sxs-lookup"><span data-stu-id="bfe22-333">boolean</span></span>|||<span data-ttu-id="bfe22-334">Значение, указывающее, где бот поддерживает звуковые вызовы.</span><span class="sxs-lookup"><span data-stu-id="bfe22-334">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="bfe22-335">**ВАЖНО.** Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="bfe22-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="bfe22-336">Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="bfe22-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="bfe22-337">Она предоставляется только для тестирования и разведки и не должна использоваться в производственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="bfe22-337">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="bfe22-338">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="bfe22-338">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="bfe22-339">boolean</span><span class="sxs-lookup"><span data-stu-id="bfe22-339">boolean</span></span>|||<span data-ttu-id="bfe22-340">Значение, указывающее, где бот поддерживает видеозвонков.</span><span class="sxs-lookup"><span data-stu-id="bfe22-340">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="bfe22-341">**ВАЖНО.** Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="bfe22-341">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="bfe22-342">Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="bfe22-342">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="bfe22-343">Она предоставляется только для тестирования и разведки и не должна использоваться в производственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="bfe22-343">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="bfe22-344">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="bfe22-344">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="bfe22-345">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="bfe22-345">bots.commandLists</span></span>

<span data-ttu-id="bfe22-346">Необязательный список команд, которые бот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="bfe22-346">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="bfe22-347">Объект — массив (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом.</span><span class="sxs-lookup"><span data-stu-id="bfe22-347">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="bfe22-348">Дополнительные [сведения см. в](~/bots/how-to/create-a-bot-commands-menu.md) меню Bot.</span><span class="sxs-lookup"><span data-stu-id="bfe22-348">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="bfe22-349">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-349">Name</span></span>| <span data-ttu-id="bfe22-350">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-350">Type</span></span>| <span data-ttu-id="bfe22-351">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-351">Maximum size</span></span> | <span data-ttu-id="bfe22-352">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-352">Required</span></span> | <span data-ttu-id="bfe22-353">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-353">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="bfe22-354">массив enums</span><span class="sxs-lookup"><span data-stu-id="bfe22-354">array of enums</span></span>|<span data-ttu-id="bfe22-355">3</span><span class="sxs-lookup"><span data-stu-id="bfe22-355">3</span></span>|<span data-ttu-id="bfe22-356">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-356">✔</span></span>|<span data-ttu-id="bfe22-357">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="bfe22-357">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="bfe22-358">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="bfe22-358">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="bfe22-359">массив объектов</span><span class="sxs-lookup"><span data-stu-id="bfe22-359">array of objects</span></span>|<span data-ttu-id="bfe22-360">10 </span><span class="sxs-lookup"><span data-stu-id="bfe22-360">10</span></span>|<span data-ttu-id="bfe22-361">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-361">✔</span></span>|<span data-ttu-id="bfe22-362">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="bfe22-362">An array of commands the bot supports:</span></span><br><span data-ttu-id="bfe22-363">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="bfe22-363">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="bfe22-364">`description`: простое описание или пример синтаксиса команды и его аргумента (строка, 128).</span><span class="sxs-lookup"><span data-stu-id="bfe22-364">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="bfe22-365">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="bfe22-365">bots.commandLists.commands</span></span>

|<span data-ttu-id="bfe22-366">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-366">Name</span></span>| <span data-ttu-id="bfe22-367">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-367">Type</span></span>| <span data-ttu-id="bfe22-368">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-368">Maximum size</span></span> | <span data-ttu-id="bfe22-369">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-369">Required</span></span> | <span data-ttu-id="bfe22-370">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-370">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="bfe22-371">title</span><span class="sxs-lookup"><span data-stu-id="bfe22-371">title</span></span>|<span data-ttu-id="bfe22-372">string</span><span class="sxs-lookup"><span data-stu-id="bfe22-372">string</span></span>|<span data-ttu-id="bfe22-373">12 </span><span class="sxs-lookup"><span data-stu-id="bfe22-373">12</span></span>|<span data-ttu-id="bfe22-374">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-374">✔</span></span>|<span data-ttu-id="bfe22-375">Имя команды бота.</span><span class="sxs-lookup"><span data-stu-id="bfe22-375">The bot command name.</span></span>|
|<span data-ttu-id="bfe22-376">description</span><span class="sxs-lookup"><span data-stu-id="bfe22-376">description</span></span>|<span data-ttu-id="bfe22-377">string</span><span class="sxs-lookup"><span data-stu-id="bfe22-377">string</span></span>|<span data-ttu-id="bfe22-378">128 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-378">128 characters</span></span>|<span data-ttu-id="bfe22-379">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-379">✔</span></span>|<span data-ttu-id="bfe22-380">Простое текстовое описание или пример синтаксиса команд и его аргументов.</span><span class="sxs-lookup"><span data-stu-id="bfe22-380">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="bfe22-381">соединители</span><span class="sxs-lookup"><span data-stu-id="bfe22-381">connectors</span></span>

<span data-ttu-id="bfe22-382">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="bfe22-382">**Optional** — array</span></span>

<span data-ttu-id="bfe22-383">Блок `connectors` определяет Office 365 соединители для приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-383">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="bfe22-384">Объект — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="bfe22-384">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="bfe22-385">Этот блок необходим только для решений, которые предоставляют соединители.</span><span class="sxs-lookup"><span data-stu-id="bfe22-385">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="bfe22-386">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-386">Name</span></span>| <span data-ttu-id="bfe22-387">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-387">Type</span></span>| <span data-ttu-id="bfe22-388">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-388">Maximum size</span></span> | <span data-ttu-id="bfe22-389">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-389">Required</span></span> | <span data-ttu-id="bfe22-390">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-390">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="bfe22-391">string</span><span class="sxs-lookup"><span data-stu-id="bfe22-391">string</span></span>|<span data-ttu-id="bfe22-392">2048 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-392">2048 characters</span></span>|<span data-ttu-id="bfe22-393">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-393">✔</span></span>|<span data-ttu-id="bfe22-394">URL https://, который необходимо использовать при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="bfe22-394">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="bfe22-395">массив enums</span><span class="sxs-lookup"><span data-stu-id="bfe22-395">array of enums</span></span>|<span data-ttu-id="bfe22-396">1</span><span class="sxs-lookup"><span data-stu-id="bfe22-396">1</span></span>|<span data-ttu-id="bfe22-397">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-397">✔</span></span>|<span data-ttu-id="bfe22-398">Указывает, предоставляет ли соединители опыт в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="bfe22-398">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="bfe22-399">В настоящее время `team` поддерживается только область.</span><span class="sxs-lookup"><span data-stu-id="bfe22-399">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="bfe22-400">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-400">string</span></span>|<span data-ttu-id="bfe22-401">64 символа</span><span class="sxs-lookup"><span data-stu-id="bfe22-401">64 characters</span></span>|<span data-ttu-id="bfe22-402">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-402">✔</span></span>|<span data-ttu-id="bfe22-403">Уникальный идентификатор соединитетеля, который соответствует его идентификатору в панели мониторинга разработчиков [соединителок.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="bfe22-403">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="bfe22-404">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="bfe22-404">composeExtensions</span></span>

<span data-ttu-id="bfe22-405">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="bfe22-405">**Optional** — array</span></span>

<span data-ttu-id="bfe22-406">Определяет расширение обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-406">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="bfe22-407">В ноябре 2017 г. имя функции было изменено с "расширение составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжили функционировать.</span><span class="sxs-lookup"><span data-stu-id="bfe22-407">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="bfe22-408">Элемент — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="bfe22-408">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="bfe22-409">Этот блок необходим только для решений, которые предоставляют расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="bfe22-409">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="bfe22-410">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-410">Name</span></span>| <span data-ttu-id="bfe22-411">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-411">Type</span></span> | <span data-ttu-id="bfe22-412">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-412">Maximum Size</span></span> | <span data-ttu-id="bfe22-413">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-413">Required</span></span> | <span data-ttu-id="bfe22-414">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-414">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="bfe22-415">string</span><span class="sxs-lookup"><span data-stu-id="bfe22-415">string</span></span>|<span data-ttu-id="bfe22-416">64</span><span class="sxs-lookup"><span data-stu-id="bfe22-416">64</span></span>|<span data-ttu-id="bfe22-417">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-417">✔</span></span>|<span data-ttu-id="bfe22-418">Уникальный ID приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрирован в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="bfe22-418">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="bfe22-419">Это вполне может быть таким же, как и общий ID приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-419">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="bfe22-420">массив объектов</span><span class="sxs-lookup"><span data-stu-id="bfe22-420">array of objects</span></span>|<span data-ttu-id="bfe22-421">10 </span><span class="sxs-lookup"><span data-stu-id="bfe22-421">10</span></span>|<span data-ttu-id="bfe22-422">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-422">✔</span></span>|<span data-ttu-id="bfe22-423">Массив команд, поддерживаемых расширением обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="bfe22-423">Array of commands the messaging extension supports.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="bfe22-424">boolean</span><span class="sxs-lookup"><span data-stu-id="bfe22-424">boolean</span></span>|||<span data-ttu-id="bfe22-425">Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="bfe22-425">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="bfe22-426">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="bfe22-426">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="bfe22-427">массив объектов</span><span class="sxs-lookup"><span data-stu-id="bfe22-427">array of Objects</span></span>|<span data-ttu-id="bfe22-428">5 </span><span class="sxs-lookup"><span data-stu-id="bfe22-428">5</span></span>||<span data-ttu-id="bfe22-429">Список обработчиков, которые позволяют вызывать приложения при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="bfe22-429">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="bfe22-430">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-430">string</span></span>|||<span data-ttu-id="bfe22-431">Тип обработка сообщений.</span><span class="sxs-lookup"><span data-stu-id="bfe22-431">The type of message handler.</span></span> <span data-ttu-id="bfe22-432">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="bfe22-432">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="bfe22-433">массив строк</span><span class="sxs-lookup"><span data-stu-id="bfe22-433">array of Strings</span></span>|||<span data-ttu-id="bfe22-434">Массив доменов, для которые обработник сообщений ссылок может зарегистрироваться.</span><span class="sxs-lookup"><span data-stu-id="bfe22-434">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="bfe22-435">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="bfe22-435">composeExtensions.commands</span></span>

<span data-ttu-id="bfe22-436">Расширение обмена сообщениями должно объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="bfe22-436">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="bfe22-437">Каждая команда отображается Microsoft Teams как потенциальное взаимодействие с точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="bfe22-437">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="bfe22-438">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="bfe22-438">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="bfe22-439">Каждый элемент команды — это объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="bfe22-439">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="bfe22-440">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-440">Name</span></span>| <span data-ttu-id="bfe22-441">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-441">Type</span></span>| <span data-ttu-id="bfe22-442">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-442">Maximum size</span></span> | <span data-ttu-id="bfe22-443">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-443">Required</span></span> | <span data-ttu-id="bfe22-444">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-444">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="bfe22-445">string</span><span class="sxs-lookup"><span data-stu-id="bfe22-445">string</span></span>|<span data-ttu-id="bfe22-446">64 символа</span><span class="sxs-lookup"><span data-stu-id="bfe22-446">64 characters</span></span>|<span data-ttu-id="bfe22-447">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-447">✔</span></span>|<span data-ttu-id="bfe22-448">ID для команды.</span><span class="sxs-lookup"><span data-stu-id="bfe22-448">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="bfe22-449">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-449">string</span></span>|<span data-ttu-id="bfe22-450">32 символа</span><span class="sxs-lookup"><span data-stu-id="bfe22-450">32 characters</span></span>|<span data-ttu-id="bfe22-451">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-451">✔</span></span>|<span data-ttu-id="bfe22-452">Удобное имя команды.</span><span class="sxs-lookup"><span data-stu-id="bfe22-452">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="bfe22-453">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-453">string</span></span>|<span data-ttu-id="bfe22-454">64 символа</span><span class="sxs-lookup"><span data-stu-id="bfe22-454">64 characters</span></span>||<span data-ttu-id="bfe22-455">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="bfe22-455">Type of the command.</span></span> <span data-ttu-id="bfe22-456">Один `query` из или `action` .</span><span class="sxs-lookup"><span data-stu-id="bfe22-456">One of `query` or `action`.</span></span> <span data-ttu-id="bfe22-457">По умолчанию: **запрос**.</span><span class="sxs-lookup"><span data-stu-id="bfe22-457">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="bfe22-458">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-458">string</span></span>|<span data-ttu-id="bfe22-459">128 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-459">128 characters</span></span>||<span data-ttu-id="bfe22-460">В описании, которое отображается пользователями, указывается назначение этой команды.</span><span class="sxs-lookup"><span data-stu-id="bfe22-460">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="bfe22-461">boolean</span><span class="sxs-lookup"><span data-stu-id="bfe22-461">boolean</span></span>|||<span data-ttu-id="bfe22-462">Значение boolean указывает, выполняется ли команда изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="bfe22-462">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="bfe22-463">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="bfe22-463">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="bfe22-464">массив строк</span><span class="sxs-lookup"><span data-stu-id="bfe22-464">array of Strings</span></span>|<span data-ttu-id="bfe22-465">3</span><span class="sxs-lookup"><span data-stu-id="bfe22-465">3</span></span>||<span data-ttu-id="bfe22-466">Определяет, из чего можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-466">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="bfe22-467">Любое сочетание `compose` `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="bfe22-467">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="bfe22-468">Значение по умолчанию: `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="bfe22-468">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="bfe22-469">boolean</span><span class="sxs-lookup"><span data-stu-id="bfe22-469">boolean</span></span>|||<span data-ttu-id="bfe22-470">Значение boolean, которое указывает, должен ли он динамически получать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="bfe22-470">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="bfe22-471">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="bfe22-471">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="bfe22-472">объект</span><span class="sxs-lookup"><span data-stu-id="bfe22-472">object</span></span>|||<span data-ttu-id="bfe22-473">Укажите модуль задач для предварительной загрузки при использовании команды расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="bfe22-473">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="bfe22-474">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-474">string</span></span>|<span data-ttu-id="bfe22-475">64 символа</span><span class="sxs-lookup"><span data-stu-id="bfe22-475">64 characters</span></span>||<span data-ttu-id="bfe22-476">Начальное название диалогов.</span><span class="sxs-lookup"><span data-stu-id="bfe22-476">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="bfe22-477">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-477">string</span></span>|||<span data-ttu-id="bfe22-478">Ширина диалогов — число в пикселях или макет по умолчанию, такие как "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="bfe22-478">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="bfe22-479">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-479">string</span></span>|||<span data-ttu-id="bfe22-480">Высота диалогов — число пикселей или макет по умолчанию, например "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="bfe22-480">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="bfe22-481">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-481">string</span></span>|||<span data-ttu-id="bfe22-482">Начальный URL-адрес веб-просмотров.</span><span class="sxs-lookup"><span data-stu-id="bfe22-482">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="bfe22-483">массив объекта</span><span class="sxs-lookup"><span data-stu-id="bfe22-483">array of object</span></span>|<span data-ttu-id="bfe22-484">5 элементов</span><span class="sxs-lookup"><span data-stu-id="bfe22-484">5 items</span></span>|<span data-ttu-id="bfe22-485">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-485">✔</span></span>|<span data-ttu-id="bfe22-486">Список параметров, которые принимает команда.</span><span class="sxs-lookup"><span data-stu-id="bfe22-486">The list of parameters the command takes.</span></span> <span data-ttu-id="bfe22-487">Минимум: 1; максимум: 5.</span><span class="sxs-lookup"><span data-stu-id="bfe22-487">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="bfe22-488">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-488">string</span></span>|<span data-ttu-id="bfe22-489">64 символа</span><span class="sxs-lookup"><span data-stu-id="bfe22-489">64 characters</span></span>|<span data-ttu-id="bfe22-490">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-490">✔</span></span>|<span data-ttu-id="bfe22-491">Имя параметра, как оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="bfe22-491">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="bfe22-492">Это включено в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="bfe22-492">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="bfe22-493">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-493">string</span></span>|<span data-ttu-id="bfe22-494">32 символа</span><span class="sxs-lookup"><span data-stu-id="bfe22-494">32 characters</span></span>|<span data-ttu-id="bfe22-495">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-495">✔</span></span>|<span data-ttu-id="bfe22-496">Удобное название для параметра.</span><span class="sxs-lookup"><span data-stu-id="bfe22-496">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="bfe22-497">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-497">string</span></span>|<span data-ttu-id="bfe22-498">128 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-498">128 characters</span></span>||<span data-ttu-id="bfe22-499">Удобное для пользователя строка, описываемая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="bfe22-499">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="bfe22-500">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-500">string</span></span>|<span data-ttu-id="bfe22-501">512 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-501">512 characters</span></span>||<span data-ttu-id="bfe22-502">Начальное значение для параметра.</span><span class="sxs-lookup"><span data-stu-id="bfe22-502">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="bfe22-503">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-503">string</span></span>|<span data-ttu-id="bfe22-504">128 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-504">128 characters</span></span>||<span data-ttu-id="bfe22-505">Определяет тип управления, отображаемого в модуле задач `fetchTask: true` для .</span><span class="sxs-lookup"><span data-stu-id="bfe22-505">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="bfe22-506">Один из `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="bfe22-506">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="bfe22-507">массив объектов</span><span class="sxs-lookup"><span data-stu-id="bfe22-507">array of objects</span></span>|<span data-ttu-id="bfe22-508">10 элементов</span><span class="sxs-lookup"><span data-stu-id="bfe22-508">10 items</span></span>||<span data-ttu-id="bfe22-509">Параметры выбора `choiceset` для .</span><span class="sxs-lookup"><span data-stu-id="bfe22-509">The choice options for the`choiceset`.</span></span> <span data-ttu-id="bfe22-510">Используйте только `parameter.inputType` тогда, когда `choiceset` это .</span><span class="sxs-lookup"><span data-stu-id="bfe22-510">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="bfe22-511">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-511">string</span></span>|<span data-ttu-id="bfe22-512">128 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-512">128 characters</span></span>|<span data-ttu-id="bfe22-513">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-513">✔</span></span>|<span data-ttu-id="bfe22-514">Название выбора.</span><span class="sxs-lookup"><span data-stu-id="bfe22-514">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="bfe22-515">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-515">string</span></span>|<span data-ttu-id="bfe22-516">512 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-516">512 characters</span></span>|<span data-ttu-id="bfe22-517">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-517">✔</span></span>|<span data-ttu-id="bfe22-518">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="bfe22-518">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="bfe22-519">permissions</span><span class="sxs-lookup"><span data-stu-id="bfe22-519">permissions</span></span>

<span data-ttu-id="bfe22-520">**Необязательный** — массив строк</span><span class="sxs-lookup"><span data-stu-id="bfe22-520">**Optional** — array of strings</span></span>

<span data-ttu-id="bfe22-521">Массив, в котором указывается, какие разрешения запрашивает приложение, что позволяет конечным пользователям `string` знать, как выполняется расширение.</span><span class="sxs-lookup"><span data-stu-id="bfe22-521">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="bfe22-522">Следующие параметры не являются эксклюзивными:</span><span class="sxs-lookup"><span data-stu-id="bfe22-522">The following options are non-exclusive:</span></span>

* <span data-ttu-id="bfe22-523">`identity`&emsp;Требуется информация о удостоверении пользователя.</span><span class="sxs-lookup"><span data-stu-id="bfe22-523">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="bfe22-524">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам группы.</span><span class="sxs-lookup"><span data-stu-id="bfe22-524">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="bfe22-525">Изменение этих разрешений во время обновления приложения заставляет пользователей повторять процесс согласия после запуска обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-525">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="bfe22-526">Дополнительные [сведения см. в обновлении](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-526">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="bfe22-527">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="bfe22-527">devicePermissions</span></span>

<span data-ttu-id="bfe22-528">**Необязательный** — массив строк</span><span class="sxs-lookup"><span data-stu-id="bfe22-528">**Optional** — array of strings</span></span>

<span data-ttu-id="bfe22-529">Предоставляет родных функций на устройстве пользователя, к которое ваше приложение запрашивает доступ.</span><span class="sxs-lookup"><span data-stu-id="bfe22-529">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="bfe22-530">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="bfe22-530">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="bfe22-531">validDomains</span><span class="sxs-lookup"><span data-stu-id="bfe22-531">validDomains</span></span>

<span data-ttu-id="bfe22-532">**Необязательный,** **за исключением обязательного,** где отмечено.</span><span class="sxs-lookup"><span data-stu-id="bfe22-532">**Optional**, except **Required** where noted.</span></span>

<span data-ttu-id="bfe22-533">Список допустимого домена для веб-сайтов, которые приложение ожидает загрузить в Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="bfe22-533">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="bfe22-534">Списки домена могут включать, например, поддиайки. `*.example.com`</span><span class="sxs-lookup"><span data-stu-id="bfe22-534">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="bfe22-535">Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="bfe22-535">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="bfe22-536">Если конфигурации вкладок или пользовательскому интерфейсу контента необходимо перейти к любому другому домену, кроме одного использования для конфигурации вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="bfe22-536">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="bfe22-537">Не обязательно **включать** в приложение домены поставщиков удостоверений, которые необходимо поддерживать.</span><span class="sxs-lookup"><span data-stu-id="bfe22-537">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="bfe22-538">Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить accounts.google.com, однако не следует включать accounts.google.com `validDomains[]` в .</span><span class="sxs-lookup"><span data-stu-id="bfe22-538">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="bfe22-539">Teams приложения, которые требуют нормальной работы собственных URL-адресов sharepoint, включают в допустимый список доменов "{teamsitedomain}".</span><span class="sxs-lookup"><span data-stu-id="bfe22-539">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bfe22-540">Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью подкрентов.</span><span class="sxs-lookup"><span data-stu-id="bfe22-540">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="bfe22-541">Например, `yourapp.onmicrosoft.com` допустимо, однако, `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="bfe22-541">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="bfe22-542">Объект — массив со всеми элементами `string` типа.</span><span class="sxs-lookup"><span data-stu-id="bfe22-542">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="bfe22-543">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="bfe22-543">webApplicationInfo</span></span>

<span data-ttu-id="bfe22-544">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="bfe22-544">**Optional** — object</span></span>

<span data-ttu-id="bfe22-545">Предопишите Azure Active Directory (AAD) App ID и microsoft Graph, чтобы помочь пользователям без проблем войти в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="bfe22-545">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="bfe22-546">Если ваше приложение зарегистрировано в AAD, необходимо предоставить ID приложения, чтобы администраторы могли легко просмотреть разрешения и предоставить согласие Teams центре администрирования.</span><span class="sxs-lookup"><span data-stu-id="bfe22-546">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="bfe22-547">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-547">Name</span></span>| <span data-ttu-id="bfe22-548">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-548">Type</span></span>| <span data-ttu-id="bfe22-549">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-549">Maximum size</span></span> | <span data-ttu-id="bfe22-550">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-550">Required</span></span> | <span data-ttu-id="bfe22-551">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-551">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="bfe22-552">string</span><span class="sxs-lookup"><span data-stu-id="bfe22-552">string</span></span>|<span data-ttu-id="bfe22-553">36 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-553">36 characters</span></span>|<span data-ttu-id="bfe22-554">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-554">✔</span></span>|<span data-ttu-id="bfe22-555">AAD-id приложения приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-555">AAD application id of the app.</span></span> <span data-ttu-id="bfe22-556">Этот id должен быть GUID.</span><span class="sxs-lookup"><span data-stu-id="bfe22-556">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="bfe22-557">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-557">string</span></span>|<span data-ttu-id="bfe22-558">2048 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-558">2048 characters</span></span>|<span data-ttu-id="bfe22-559">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-559">✔</span></span>|<span data-ttu-id="bfe22-560">URL-адрес ресурса приложения для приобретения маркера auth для SSO.</span><span class="sxs-lookup"><span data-stu-id="bfe22-560">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="bfe22-561">**ПРИМЕЧАНИЕ:** Если вы не используете SSO, убедитесь, что вы вводите значение строки в этом поле в манифест приложения, например, чтобы избежать ответа https://notapplicable на ошибку.</span><span class="sxs-lookup"><span data-stu-id="bfe22-561">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="bfe22-562">массив строк</span><span class="sxs-lookup"><span data-stu-id="bfe22-562">array of strings</span></span>|<span data-ttu-id="bfe22-563">128 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-563">128 characters</span></span>||<span data-ttu-id="bfe22-564">Укажите [конкретное согласие конкретного ресурса.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="bfe22-564">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="bfe22-565">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="bfe22-565">showLoadingIndicator</span></span>

<span data-ttu-id="bfe22-566">**Необязательный** — boolean</span><span class="sxs-lookup"><span data-stu-id="bfe22-566">**Optional** — boolean</span></span>

<span data-ttu-id="bfe22-567">Указывает, следует ли показывать индикатор загрузки при загрузке приложения или вкладки.</span><span class="sxs-lookup"><span data-stu-id="bfe22-567">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="bfe22-568">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="bfe22-568">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="bfe22-569">Если в манифесте приложения выбрано как верное, чтобы правильно загрузить страницу, измените страницы контента вкладок и модулей задач, как описано в документе Показать документ индикатора `showLoadingIndicator` загрузки. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="bfe22-569">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="bfe22-570">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="bfe22-570">isFullScreen</span></span>

 <span data-ttu-id="bfe22-571">**Необязательный** — boolean</span><span class="sxs-lookup"><span data-stu-id="bfe22-571">**Optional** — boolean</span></span>

<span data-ttu-id="bfe22-572">Указать, где отрисовка личного приложения с панели заголовки вкладок или без нее.</span><span class="sxs-lookup"><span data-stu-id="bfe22-572">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="bfe22-573">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="bfe22-573">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="bfe22-574">activities</span><span class="sxs-lookup"><span data-stu-id="bfe22-574">activities</span></span>

<span data-ttu-id="bfe22-575">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="bfe22-575">**Optional** — object</span></span>

<span data-ttu-id="bfe22-576">Определите свойства, которые приложение использует для публикации ленты действий пользователя.</span><span class="sxs-lookup"><span data-stu-id="bfe22-576">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="bfe22-577">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-577">Name</span></span>| <span data-ttu-id="bfe22-578">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-578">Type</span></span>| <span data-ttu-id="bfe22-579">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-579">Maximum size</span></span> | <span data-ttu-id="bfe22-580">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-580">Required</span></span> | <span data-ttu-id="bfe22-581">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-581">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="bfe22-582">массив объектов</span><span class="sxs-lookup"><span data-stu-id="bfe22-582">array of Objects</span></span>|<span data-ttu-id="bfe22-583">128 элементов</span><span class="sxs-lookup"><span data-stu-id="bfe22-583">128 items</span></span>| | <span data-ttu-id="bfe22-584">Укапитайте типы действий, которые ваше приложение может размещать в канале действий пользователей.</span><span class="sxs-lookup"><span data-stu-id="bfe22-584">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="bfe22-585">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="bfe22-585">activities.activityTypes</span></span>

|<span data-ttu-id="bfe22-586">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-586">Name</span></span>| <span data-ttu-id="bfe22-587">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-587">Type</span></span>| <span data-ttu-id="bfe22-588">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-588">Maximum size</span></span> | <span data-ttu-id="bfe22-589">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-589">Required</span></span> | <span data-ttu-id="bfe22-590">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-590">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="bfe22-591">string</span><span class="sxs-lookup"><span data-stu-id="bfe22-591">string</span></span>|<span data-ttu-id="bfe22-592">32 символа</span><span class="sxs-lookup"><span data-stu-id="bfe22-592">32 characters</span></span>|<span data-ttu-id="bfe22-593">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-593">✔</span></span>|<span data-ttu-id="bfe22-594">Тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="bfe22-594">The notification type.</span></span> <span data-ttu-id="bfe22-595">*См. ниже*.</span><span class="sxs-lookup"><span data-stu-id="bfe22-595">*See below*.</span></span>|
|`description`|<span data-ttu-id="bfe22-596">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-596">string</span></span>|<span data-ttu-id="bfe22-597">128 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-597">128 characters</span></span>|<span data-ttu-id="bfe22-598">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-598">✔</span></span>|<span data-ttu-id="bfe22-599">Краткое описание уведомления.</span><span class="sxs-lookup"><span data-stu-id="bfe22-599">A brief description of the notification.</span></span> <span data-ttu-id="bfe22-600">*См. ниже*.</span><span class="sxs-lookup"><span data-stu-id="bfe22-600">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="bfe22-601">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-601">string</span></span>|<span data-ttu-id="bfe22-602">128 символов</span><span class="sxs-lookup"><span data-stu-id="bfe22-602">128 characters</span></span>|<span data-ttu-id="bfe22-603">✔</span><span class="sxs-lookup"><span data-stu-id="bfe22-603">✔</span></span>|<span data-ttu-id="bfe22-604">Ex: "{actor} создал задачу {taskId} для вас"</span><span class="sxs-lookup"><span data-stu-id="bfe22-604">Ex: "{actor} created task {taskId} for you"</span></span>|

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

## <a name="defaultinstallscope"></a><span data-ttu-id="bfe22-605">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="bfe22-605">defaultInstallScope</span></span>

<span data-ttu-id="bfe22-606">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-606">**Optional** - string</span></span>

<span data-ttu-id="bfe22-607">Указывает область установки, определяемую для этого приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bfe22-607">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="bfe22-608">Определенным областью будет параметр, отображаемый на кнопке при добавлении приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="bfe22-608">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="bfe22-609">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="bfe22-609">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="bfe22-610">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="bfe22-610">defaultGroupCapability</span></span>

<span data-ttu-id="bfe22-611">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="bfe22-611">**Optional** - object</span></span>

<span data-ttu-id="bfe22-612">Когда будет выбрана область установки группы, она определит возможности по умолчанию при установке приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="bfe22-612">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="bfe22-613">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="bfe22-613">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="bfe22-614">Имя</span><span class="sxs-lookup"><span data-stu-id="bfe22-614">Name</span></span>| <span data-ttu-id="bfe22-615">Тип</span><span class="sxs-lookup"><span data-stu-id="bfe22-615">Type</span></span>| <span data-ttu-id="bfe22-616">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="bfe22-616">Maximum size</span></span> | <span data-ttu-id="bfe22-617">Обязательный</span><span class="sxs-lookup"><span data-stu-id="bfe22-617">Required</span></span> | <span data-ttu-id="bfe22-618">Описание</span><span class="sxs-lookup"><span data-stu-id="bfe22-618">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="bfe22-619">string</span><span class="sxs-lookup"><span data-stu-id="bfe22-619">string</span></span>|||<span data-ttu-id="bfe22-620">Если выбрана область установки, это поле указывает доступные возможности `team` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bfe22-620">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="bfe22-621">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="bfe22-621">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="bfe22-622">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-622">string</span></span>|||<span data-ttu-id="bfe22-623">Если выбрана область установки, это поле указывает доступные возможности `groupchat` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bfe22-623">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="bfe22-624">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="bfe22-624">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="bfe22-625">Строка</span><span class="sxs-lookup"><span data-stu-id="bfe22-625">string</span></span>|||<span data-ttu-id="bfe22-626">Если выбрана область установки, это поле указывает доступные возможности `meetings` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bfe22-626">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="bfe22-627">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="bfe22-627">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="bfe22-628">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="bfe22-628">configurableProperties</span></span>

<span data-ttu-id="bfe22-629">**Необязательный** - массив</span><span class="sxs-lookup"><span data-stu-id="bfe22-629">**Optional** - array</span></span>

<span data-ttu-id="bfe22-630">Блок определяет свойства приложений, которые могут `configurableProperties` Teams администраторы.</span><span class="sxs-lookup"><span data-stu-id="bfe22-630">The `configurableProperties` block defines the app properties that Teams admins can customize.</span></span> <span data-ttu-id="bfe22-631">Дополнительные сведения см. в [приложении Enable customization.](~/concepts/design/enable-app-customization.md)</span><span class="sxs-lookup"><span data-stu-id="bfe22-631">For more information, see [enable app customization](~/concepts/design/enable-app-customization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bfe22-632">Необходимо определить как минимум одно свойство.</span><span class="sxs-lookup"><span data-stu-id="bfe22-632">A minimum of one property must be defined.</span></span> <span data-ttu-id="bfe22-633">В этом блоке можно определить максимум девять свойств.</span><span class="sxs-lookup"><span data-stu-id="bfe22-633">You can define a maximum of nine properties in this block.</span></span>

<span data-ttu-id="bfe22-634">Можно определить любое из следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="bfe22-634">You can define any of the following properties:</span></span>

* <span data-ttu-id="bfe22-635">`name`: Имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-635">`name`: The app's display name.</span></span>
* <span data-ttu-id="bfe22-636">`shortDescription`Краткое описание приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-636">`shortDescription`: The app's short description.</span></span>
* <span data-ttu-id="bfe22-637">`longDescription`Подробное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-637">`longDescription`: The app's detailed description.</span></span>
* <span data-ttu-id="bfe22-638">`smallImageUrl`: Значок контура приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-638">`smallImageUrl`: The app's outline icon.</span></span>
* <span data-ttu-id="bfe22-639">`largeImageUrl`: Значок цвета приложения.</span><span class="sxs-lookup"><span data-stu-id="bfe22-639">`largeImageUrl`: The app's color icon.</span></span>
* <span data-ttu-id="bfe22-640">`accentColor`: Цвет, который нужно использовать в сочетании с и в качестве фона для значков контура.</span><span class="sxs-lookup"><span data-stu-id="bfe22-640">`accentColor`: The color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="bfe22-641">`developerUrl`URL-адрес HTTPS веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="bfe22-641">`developerUrl`: The HTTPS URL of the developer's website.</span></span>
* <span data-ttu-id="bfe22-642">`privacyUrl`: URL-адрес HTTPS политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="bfe22-642">`privacyUrl`: The HTTPS URL of the developer's privacy policy.</span></span>
* <span data-ttu-id="bfe22-643">`termsOfUseUrl`: URL-адрес HTTPS условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="bfe22-643">`termsOfUseUrl`: The HTTPS URL of the developer's terms of use.</span></span>
