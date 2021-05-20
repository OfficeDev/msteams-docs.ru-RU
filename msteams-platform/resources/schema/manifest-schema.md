---
title: Ссылка на схему манифеста
description: Описывает явную схему для Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: команды проявляют схему
ms.openlocfilehash: 6c7cd02480f78d19aed269b5d78d0c6f470621d2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566448"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="a87e3-104">Справка: Схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a87e3-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="a87e3-105">В Teams манифесте описывается, как приложение интегрируется в Microsoft Teams продукт.</span><span class="sxs-lookup"><span data-stu-id="a87e3-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="a87e3-106">Ваш манифест должен соответствовать схеме, размещенным на [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="a87e3-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="a87e3-107">Предыдущие версии 1.0, 1.1,..., 1.6 и так далее также поддерживаются (с помощью "v1.x" в URL).</span><span class="sxs-lookup"><span data-stu-id="a87e3-107">Previous versions 1.0, 1.1,..., 1.6, and so on are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="a87e3-108">В следующем образце схемы показаны все параметры разгибаемости:</span><span class="sxs-lookup"><span data-stu-id="a87e3-108">The following schema sample shows all extensibility options:</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="a87e3-109">Образец полного манифеста</span><span class="sxs-lookup"><span data-stu-id="a87e3-109">Sample full manifest</span></span>

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

<span data-ttu-id="a87e3-110">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a87e3-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="a87e3-111">$schema</span><span class="sxs-lookup"><span data-stu-id="a87e3-111">$schema</span></span>

<span data-ttu-id="a87e3-112">Необязательно, но рекомендуется - строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-112">Optional, but recommended — string</span></span>

<span data-ttu-id="a87e3-113">В https:// URL-адрес, ссылаясь на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="a87e3-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="a87e3-114">манифестВерсия</span><span class="sxs-lookup"><span data-stu-id="a87e3-114">manifestVersion</span></span>

<span data-ttu-id="a87e3-115">**Требуется** - строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-115">**Required** — string</span></span>

<span data-ttu-id="a87e3-116">Версия манифеста схема этого манифеста использует.</span><span class="sxs-lookup"><span data-stu-id="a87e3-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="a87e3-117">Это должно быть 1.10.</span><span class="sxs-lookup"><span data-stu-id="a87e3-117">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="a87e3-118">version</span><span class="sxs-lookup"><span data-stu-id="a87e3-118">version</span></span>

<span data-ttu-id="a87e3-119">**Требуется** - строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-119">**Required** — string</span></span>

<span data-ttu-id="a87e3-120">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-120">The version of a specific app.</span></span> <span data-ttu-id="a87e3-121">Если вы обновите что-то в манифесте, версия должна быть приращена тоже.</span><span class="sxs-lookup"><span data-stu-id="a87e3-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="a87e3-122">Таким образом, при установке нового манифеста он перезахохорит существующий и пользователь получит новую функциональность.</span><span class="sxs-lookup"><span data-stu-id="a87e3-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="a87e3-123">Если это приложение было представлено в магазин, новый манифест должен быть повторно представлен и повторно проверен.</span><span class="sxs-lookup"><span data-stu-id="a87e3-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="a87e3-124">Пользователи приложения получают новый обновленный манифест автоматически в течение нескольких часов после утверждения манифеста.</span><span class="sxs-lookup"><span data-stu-id="a87e3-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="a87e3-125">Если приложение запрашивает изменения разрешений, пользователям предлагается обновить и повторно дать согласие на приложение.</span><span class="sxs-lookup"><span data-stu-id="a87e3-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="a87e3-126">Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. несовершеннолетний. ПАТЧ).</span><span class="sxs-lookup"><span data-stu-id="a87e3-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="a87e3-127">id</span><span class="sxs-lookup"><span data-stu-id="a87e3-127">id</span></span>

<span data-ttu-id="a87e3-128">**Требуется** - идентификатор приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="a87e3-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="a87e3-129">Идентификатор является уникальным идентификатором Microsoft для приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="a87e3-130">У вас есть идентификатор, если ваш бот зарегистрирован через Microsoft Bot Framework или веб-приложение вашей вкладки уже входят в систему Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="a87e3-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="a87e3-131">Вы должны ввести id здесь.</span><span class="sxs-lookup"><span data-stu-id="a87e3-131">You must enter the ID here.</span></span> <span data-ttu-id="a87e3-132">В противном случае необходимо создать новый идентификатор на портале [регистрации приложений Майкрософт.](https://aka.ms/appregistrations)</span><span class="sxs-lookup"><span data-stu-id="a87e3-132">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="a87e3-133">Используйте тот же идентификатор, если вы добавляете бота.</span><span class="sxs-lookup"><span data-stu-id="a87e3-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="a87e3-134">Если вы отправляете обновление существующего приложения в AppSource, идентификатор в вашем манифесте не должен быть изменен.</span><span class="sxs-lookup"><span data-stu-id="a87e3-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="a87e3-135">developer</span><span class="sxs-lookup"><span data-stu-id="a87e3-135">developer</span></span>

<span data-ttu-id="a87e3-136">**Требуется** - объект</span><span class="sxs-lookup"><span data-stu-id="a87e3-136">**Required** — object</span></span>

<span data-ttu-id="a87e3-137">Уточняет информацию о вашей компании.</span><span class="sxs-lookup"><span data-stu-id="a87e3-137">Specifies information about your company.</span></span> <span data-ttu-id="a87e3-138">Для приложений, представленных в Teams, эти значения должны соответствовать информации в объявлении магазина.</span><span class="sxs-lookup"><span data-stu-id="a87e3-138">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="a87e3-139">Для получения дополнительной информации [см Teams.](~/concepts/deploy-and-publish/appsource/publish.md)</span><span class="sxs-lookup"><span data-stu-id="a87e3-139">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="a87e3-140">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-140">Name</span></span>| <span data-ttu-id="a87e3-141">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-141">Maximum size</span></span> | <span data-ttu-id="a87e3-142">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-142">Required</span></span> | <span data-ttu-id="a87e3-143">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="a87e3-144">32 символа</span><span class="sxs-lookup"><span data-stu-id="a87e3-144">32 characters</span></span>|<span data-ttu-id="a87e3-145">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-145">✔</span></span>|<span data-ttu-id="a87e3-146">Имя дисплея для разработчика.</span><span class="sxs-lookup"><span data-stu-id="a87e3-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="a87e3-147">2048 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-147">2048 characters</span></span>|<span data-ttu-id="a87e3-148">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-148">✔</span></span>|<span data-ttu-id="a87e3-149">Данный https:// URL на веб-сайте разработчика.</span><span class="sxs-lookup"><span data-stu-id="a87e3-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="a87e3-150">Эта ссылка должна принимать пользователей к вашей компании или продукта конкретных страниц посадки.</span><span class="sxs-lookup"><span data-stu-id="a87e3-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="a87e3-151">2048 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-151">2048 characters</span></span>|<span data-ttu-id="a87e3-152">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-152">✔</span></span>|<span data-ttu-id="a87e3-153">Веб https:// адрес для политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="a87e3-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="a87e3-154">2048 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-154">2048 characters</span></span>|<span data-ttu-id="a87e3-155">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-155">✔</span></span>|<span data-ttu-id="a87e3-156">Данный https:// URL-адресу к условиям использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="a87e3-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="a87e3-157">10 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-157">10 characters</span></span>| |<span data-ttu-id="a87e3-158">**Необязательно** Идентификатор партнерской сети Майкрософт, который идентифицирует организацию-партнера, строя приложение.</span><span class="sxs-lookup"><span data-stu-id="a87e3-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="a87e3-159">name</span><span class="sxs-lookup"><span data-stu-id="a87e3-159">name</span></span>

<span data-ttu-id="a87e3-160">**Требуется** - объект</span><span class="sxs-lookup"><span data-stu-id="a87e3-160">**Required** — object</span></span>

<span data-ttu-id="a87e3-161">Название приложения, отображаемое пользователям в приложении, Teams опыт.</span><span class="sxs-lookup"><span data-stu-id="a87e3-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="a87e3-162">Для приложений, представленных в AppSource, эти значения должны соответствовать информации в вашей записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="a87e3-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="a87e3-163">Ценности и `short` должны `full` быть разными.</span><span class="sxs-lookup"><span data-stu-id="a87e3-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="a87e3-164">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-164">Name</span></span>| <span data-ttu-id="a87e3-165">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-165">Maximum size</span></span> | <span data-ttu-id="a87e3-166">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-166">Required</span></span> | <span data-ttu-id="a87e3-167">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="a87e3-168">30 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-168">30 characters</span></span>|<span data-ttu-id="a87e3-169">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-169">✔</span></span>|<span data-ttu-id="a87e3-170">Краткое название дисплея для приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="a87e3-171">100 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-171">100 characters</span></span>||<span data-ttu-id="a87e3-172">Полное название приложения, используемое, если полное имя приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="a87e3-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="a87e3-173">description</span><span class="sxs-lookup"><span data-stu-id="a87e3-173">description</span></span>

<span data-ttu-id="a87e3-174">**Требуется** - объект</span><span class="sxs-lookup"><span data-stu-id="a87e3-174">**Required** — object</span></span>

<span data-ttu-id="a87e3-175">Описывает ваше приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="a87e3-175">Describes your app to users.</span></span> <span data-ttu-id="a87e3-176">Для приложений, представленных в AppSource, эти значения должны соответствовать информации в вашей записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="a87e3-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="a87e3-177">Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет информацию, чтобы помочь потенциальным клиентам понять, что ваш опыт делает.</span><span class="sxs-lookup"><span data-stu-id="a87e3-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="a87e3-178">Вы должны отметить в полном описании, если внешний счет требуется для использования.</span><span class="sxs-lookup"><span data-stu-id="a87e3-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="a87e3-179">Ценности и `short` должны `full` быть разными.</span><span class="sxs-lookup"><span data-stu-id="a87e3-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="a87e3-180">Ваше краткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="a87e3-181">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-181">Name</span></span>| <span data-ttu-id="a87e3-182">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-182">Maximum size</span></span> | <span data-ttu-id="a87e3-183">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-183">Required</span></span> | <span data-ttu-id="a87e3-184">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="a87e3-185">80 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-185">80 characters</span></span>|<span data-ttu-id="a87e3-186">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-186">✔</span></span>|<span data-ttu-id="a87e3-187">Краткое описание вашего приложения, используемого при ограничении пространства.</span><span class="sxs-lookup"><span data-stu-id="a87e3-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="a87e3-188">4000 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-188">4000 characters</span></span>|<span data-ttu-id="a87e3-189">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-189">✔</span></span>|<span data-ttu-id="a87e3-190">Полное описание вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="a87e3-191">пакетИмя</span><span class="sxs-lookup"><span data-stu-id="a87e3-191">packageName</span></span>

<span data-ttu-id="a87e3-192">**Необязательно** - строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-192">**Optional** — string</span></span>

<span data-ttu-id="a87e3-193">Уникальный идентификатор приложения в обратных доменных нотациях; например, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="a87e3-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="a87e3-194">Максимальная длина: 64 символа.</span><span class="sxs-lookup"><span data-stu-id="a87e3-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="a87e3-195">локализацияИнфо</span><span class="sxs-lookup"><span data-stu-id="a87e3-195">localizationInfo</span></span>

<span data-ttu-id="a87e3-196">**Факультативно** - объект</span><span class="sxs-lookup"><span data-stu-id="a87e3-196">**Optional** — object</span></span>

<span data-ttu-id="a87e3-197">Позволяет спецификацию языка по умолчанию, а также указатели на дополнительные языковые файлы.</span><span class="sxs-lookup"><span data-stu-id="a87e3-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="a87e3-198">Для получения дополнительной информации [см.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="a87e3-198">For more information, see [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="a87e3-199">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-199">Name</span></span>| <span data-ttu-id="a87e3-200">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-200">Maximum size</span></span> | <span data-ttu-id="a87e3-201">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-201">Required</span></span> | <span data-ttu-id="a87e3-202">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="a87e3-203">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-203">✔</span></span>|<span data-ttu-id="a87e3-204">Языковая метка строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="a87e3-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="a87e3-205">локализацияИнфо.дополнительныеАнгуажи</span><span class="sxs-lookup"><span data-stu-id="a87e3-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="a87e3-206">Массив объектов, определяющих дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="a87e3-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="a87e3-207">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-207">Name</span></span>| <span data-ttu-id="a87e3-208">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-208">Maximum size</span></span> | <span data-ttu-id="a87e3-209">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-209">Required</span></span> | <span data-ttu-id="a87e3-210">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="a87e3-211">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-211">✔</span></span>|<span data-ttu-id="a87e3-212">Языковая метка строк в предоставленном файле.</span><span class="sxs-lookup"><span data-stu-id="a87e3-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="a87e3-213">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-213">✔</span></span>|<span data-ttu-id="a87e3-214">Относительный путь файла к файлу .json, содержащем переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="a87e3-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="a87e3-215">icons</span><span class="sxs-lookup"><span data-stu-id="a87e3-215">icons</span></span>

<span data-ttu-id="a87e3-216">**Требуется** - объект</span><span class="sxs-lookup"><span data-stu-id="a87e3-216">**Required** — object</span></span>

<span data-ttu-id="a87e3-217">Иконки, используемые в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="a87e3-217">Icons used within the Teams app.</span></span> <span data-ttu-id="a87e3-218">Файлы значков должны быть включены в пакет загрузки.</span><span class="sxs-lookup"><span data-stu-id="a87e3-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="a87e3-219">Для [получения дополнительной](../../concepts/build-and-test/apps-package.md#app-icons) информации можно получить подробную информацию.</span><span class="sxs-lookup"><span data-stu-id="a87e3-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="a87e3-220">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-220">Name</span></span>| <span data-ttu-id="a87e3-221">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-221">Maximum size</span></span> | <span data-ttu-id="a87e3-222">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-222">Required</span></span> | <span data-ttu-id="a87e3-223">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="a87e3-224">32 x 32 пикселей</span><span class="sxs-lookup"><span data-stu-id="a87e3-224">32 x 32 pixels</span></span>|<span data-ttu-id="a87e3-225">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-225">✔</span></span>|<span data-ttu-id="a87e3-226">Относительный путь файла к прозрачному значку контура 32x32 PNG.</span><span class="sxs-lookup"><span data-stu-id="a87e3-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="a87e3-227">192 x 192 пикселей</span><span class="sxs-lookup"><span data-stu-id="a87e3-227">192 x 192 pixels</span></span>|<span data-ttu-id="a87e3-228">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-228">✔</span></span>|<span data-ttu-id="a87e3-229">Относительный путь файла к полноцветной иконке 192x192 PNG.</span><span class="sxs-lookup"><span data-stu-id="a87e3-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="a87e3-230">акцентКолор</span><span class="sxs-lookup"><span data-stu-id="a87e3-230">accentColor</span></span>

<span data-ttu-id="a87e3-231">**Дополнительно** - HTML hex цветовой код</span><span class="sxs-lookup"><span data-stu-id="a87e3-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="a87e3-232">Цвет для использования в сочетании с и в качестве фона для вашего контура иконки.</span><span class="sxs-lookup"><span data-stu-id="a87e3-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="a87e3-233">Значение должно быть действительным HTML цветового кода, начиная с 'я', `#4464ee` например.</span><span class="sxs-lookup"><span data-stu-id="a87e3-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="a87e3-234">настраиваемыеTabs</span><span class="sxs-lookup"><span data-stu-id="a87e3-234">configurableTabs</span></span>

<span data-ttu-id="a87e3-235">**Необязательно** - массив</span><span class="sxs-lookup"><span data-stu-id="a87e3-235">**Optional** — array</span></span>

<span data-ttu-id="a87e3-236">Используется, когда ваш опыт работы с приложением имеет опыт вкладки командных каналов, который требует дополнительной конфигурации, прежде чем он будет добавлен.</span><span class="sxs-lookup"><span data-stu-id="a87e3-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="a87e3-237">Настраиваемые вкладки поддерживаются только в области команд, и вы можете настроить те же вкладки несколько раз.</span><span class="sxs-lookup"><span data-stu-id="a87e3-237">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="a87e3-238">Тем не менее, вы можете определить его в манифесте только один раз.</span><span class="sxs-lookup"><span data-stu-id="a87e3-238">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="a87e3-239">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-239">Name</span></span>| <span data-ttu-id="a87e3-240">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-240">Type</span></span>| <span data-ttu-id="a87e3-241">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-241">Maximum size</span></span> | <span data-ttu-id="a87e3-242">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-242">Required</span></span> | <span data-ttu-id="a87e3-243">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="a87e3-244">string</span><span class="sxs-lookup"><span data-stu-id="a87e3-244">string</span></span>|<span data-ttu-id="a87e3-245">2048 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-245">2048 characters</span></span>|<span data-ttu-id="a87e3-246">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-246">✔</span></span>|<span data-ttu-id="a87e3-247">Url https:// для использования при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="a87e3-247">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="a87e3-248">массив enums</span><span class="sxs-lookup"><span data-stu-id="a87e3-248">array of enums</span></span>|<span data-ttu-id="a87e3-249">1</span><span class="sxs-lookup"><span data-stu-id="a87e3-249">1</span></span>|<span data-ttu-id="a87e3-250">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-250">✔</span></span>|<span data-ttu-id="a87e3-251">В настоящее время настраиваемые вкладки поддерживают `team` только `groupchat` области и области.</span><span class="sxs-lookup"><span data-stu-id="a87e3-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="a87e3-252">boolean</span><span class="sxs-lookup"><span data-stu-id="a87e3-252">boolean</span></span>|||<span data-ttu-id="a87e3-253">Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания.</span><span class="sxs-lookup"><span data-stu-id="a87e3-253">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="a87e3-254">По умолчанию: **верно**.</span><span class="sxs-lookup"><span data-stu-id="a87e3-254">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="a87e3-255">массив enums</span><span class="sxs-lookup"><span data-stu-id="a87e3-255">array of enums</span></span>|<span data-ttu-id="a87e3-256">6 </span><span class="sxs-lookup"><span data-stu-id="a87e3-256">6</span></span>||<span data-ttu-id="a87e3-257">Набор `contextItem` областей, в которых [поддерживается вкладка.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="a87e3-257">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="a87e3-258">По **умолчанию: «каналТаб, privateChatTab, встречаChatTab, встреча сDetailsTab».**</span><span class="sxs-lookup"><span data-stu-id="a87e3-258">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="a87e3-259">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-259">string</span></span>|<span data-ttu-id="a87e3-260">2048</span><span class="sxs-lookup"><span data-stu-id="a87e3-260">2048</span></span>||<span data-ttu-id="a87e3-261">Относительный путь файла к изображению предварительного просмотра вкладок для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a87e3-261">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="a87e3-262">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="a87e3-262">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="a87e3-263">массив enums</span><span class="sxs-lookup"><span data-stu-id="a87e3-263">array of enums</span></span>|<span data-ttu-id="a87e3-264">1</span><span class="sxs-lookup"><span data-stu-id="a87e3-264">1</span></span>||<span data-ttu-id="a87e3-265">Определяет, как ваша вкладка доступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a87e3-265">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="a87e3-266">Варианты `sharePointFullPage` и `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="a87e3-266">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="a87e3-267">статическиеTabs</span><span class="sxs-lookup"><span data-stu-id="a87e3-267">staticTabs</span></span>

<span data-ttu-id="a87e3-268">**Необязательно** - массив</span><span class="sxs-lookup"><span data-stu-id="a87e3-268">**Optional** — array</span></span>

<span data-ttu-id="a87e3-269">Определяет набор вкладок, которые могут быть "закреплены" по умолчанию, без добавления пользователем их вручную.</span><span class="sxs-lookup"><span data-stu-id="a87e3-269">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="a87e3-270">Статические вкладки, `personal` заявленные в области, всегда прикрепляются к личному опыту приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-270">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="a87e3-271">Статические вкладки, заявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="a87e3-271">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="a87e3-272">Этот элемент является массив (максимум 16 элементов) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-272">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="a87e3-273">Этот блок необходим только для решений, которые обеспечивают статическое решение вкладки.</span><span class="sxs-lookup"><span data-stu-id="a87e3-273">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="a87e3-274">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-274">Name</span></span>| <span data-ttu-id="a87e3-275">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-275">Type</span></span>| <span data-ttu-id="a87e3-276">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-276">Maximum size</span></span> | <span data-ttu-id="a87e3-277">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-277">Required</span></span> | <span data-ttu-id="a87e3-278">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-278">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="a87e3-279">string</span><span class="sxs-lookup"><span data-stu-id="a87e3-279">string</span></span>|<span data-ttu-id="a87e3-280">64 символа</span><span class="sxs-lookup"><span data-stu-id="a87e3-280">64 characters</span></span>|<span data-ttu-id="a87e3-281">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-281">✔</span></span>|<span data-ttu-id="a87e3-282">Уникальный идентификатор сущности, отображаемой вкладкой.</span><span class="sxs-lookup"><span data-stu-id="a87e3-282">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="a87e3-283">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-283">string</span></span>|<span data-ttu-id="a87e3-284">128 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-284">128 characters</span></span>|<span data-ttu-id="a87e3-285">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-285">✔</span></span>|<span data-ttu-id="a87e3-286">Название отображения вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="a87e3-286">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="a87e3-287">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-287">string</span></span>||<span data-ttu-id="a87e3-288">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-288">✔</span></span>|<span data-ttu-id="a87e3-289">В https:// URL-адрес, который указывает на пользовательский интерфейс сущности, который будет отображаться в Teams холсте.</span><span class="sxs-lookup"><span data-stu-id="a87e3-289">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="a87e3-290">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-290">string</span></span>|||<span data-ttu-id="a87e3-291">Веб https:// адрес, чтобы указать, если пользователь выбирает для просмотра в браузере.</span><span class="sxs-lookup"><span data-stu-id="a87e3-291">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="a87e3-292">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-292">string</span></span>|||<span data-ttu-id="a87e3-293">Веб https:// адрес, чтобы указать на поисковые запросы пользователя.</span><span class="sxs-lookup"><span data-stu-id="a87e3-293">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="a87e3-294">массив enums</span><span class="sxs-lookup"><span data-stu-id="a87e3-294">array of enums</span></span>|<span data-ttu-id="a87e3-295">1</span><span class="sxs-lookup"><span data-stu-id="a87e3-295">1</span></span>|<span data-ttu-id="a87e3-296">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-296">✔</span></span>|<span data-ttu-id="a87e3-297">В настоящее время статические вкладки поддерживают только `personal` область, что означает, что она может быть предусмотрена только как часть личного опыта.</span><span class="sxs-lookup"><span data-stu-id="a87e3-297">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="a87e3-298">массив enums</span><span class="sxs-lookup"><span data-stu-id="a87e3-298">array of enums</span></span>| <span data-ttu-id="a87e3-299">2</span><span class="sxs-lookup"><span data-stu-id="a87e3-299">2</span></span>|| <span data-ttu-id="a87e3-300">Набор `contextItem` областей, в которых поддерживается вкладка.</span><span class="sxs-lookup"><span data-stu-id="a87e3-300">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="a87e3-301">Функция searchUrl недоступна для сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="a87e3-301">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="a87e3-302">Если вкладки требуют контексто-зависимой информации для отображения соответствующего содержимого или для инициирования потока аутентификации, для получения дополнительно [Microsoft Teams й](../../tabs/how-to/access-teams-context.md)информации см.</span><span class="sxs-lookup"><span data-stu-id="a87e3-302">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="a87e3-303">Ботов</span><span class="sxs-lookup"><span data-stu-id="a87e3-303">bots</span></span>

<span data-ttu-id="a87e3-304">**Необязательно** - массив</span><span class="sxs-lookup"><span data-stu-id="a87e3-304">**Optional** — array</span></span>

<span data-ttu-id="a87e3-305">Определяет решение для бота, а также дополнительную информацию, такую как свойства команды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a87e3-305">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="a87e3-306">Элемент массива (максимум только 1 элемент в &mdash; настоящее время только один бот допускается в приложении) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-306">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="a87e3-307">Этот блок необходим только для решений, которые обеспечивают бот опыт.</span><span class="sxs-lookup"><span data-stu-id="a87e3-307">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="a87e3-308">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-308">Name</span></span>| <span data-ttu-id="a87e3-309">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-309">Type</span></span>| <span data-ttu-id="a87e3-310">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-310">Maximum size</span></span> | <span data-ttu-id="a87e3-311">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-311">Required</span></span> | <span data-ttu-id="a87e3-312">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-312">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a87e3-313">string</span><span class="sxs-lookup"><span data-stu-id="a87e3-313">string</span></span>|<span data-ttu-id="a87e3-314">64 символа</span><span class="sxs-lookup"><span data-stu-id="a87e3-314">64 characters</span></span>|<span data-ttu-id="a87e3-315">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-315">✔</span></span>|<span data-ttu-id="a87e3-316">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a87e3-316">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="a87e3-317">Это вполне может быть так же, как общий [идентификатор приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="a87e3-317">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="a87e3-318">массив enums</span><span class="sxs-lookup"><span data-stu-id="a87e3-318">array of enums</span></span>|<span data-ttu-id="a87e3-319">3</span><span class="sxs-lookup"><span data-stu-id="a87e3-319">3</span></span>|<span data-ttu-id="a87e3-320">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-320">✔</span></span>|<span data-ttu-id="a87e3-321">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="a87e3-321">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a87e3-322">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="a87e3-322">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="a87e3-323">boolean</span><span class="sxs-lookup"><span data-stu-id="a87e3-323">boolean</span></span>|||<span data-ttu-id="a87e3-324">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="a87e3-324">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="a87e3-325">по умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="a87e3-325">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="a87e3-326">boolean</span><span class="sxs-lookup"><span data-stu-id="a87e3-326">boolean</span></span>|||<span data-ttu-id="a87e3-327">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="a87e3-327">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="a87e3-328">по умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="a87e3-328">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="a87e3-329">boolean</span><span class="sxs-lookup"><span data-stu-id="a87e3-329">boolean</span></span>|||<span data-ttu-id="a87e3-330">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="a87e3-330">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="a87e3-331">по умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="a87e3-331">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="a87e3-332">boolean</span><span class="sxs-lookup"><span data-stu-id="a87e3-332">boolean</span></span>|||<span data-ttu-id="a87e3-333">Значение, указывающее, где бот поддерживает аудиозвонки.</span><span class="sxs-lookup"><span data-stu-id="a87e3-333">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="a87e3-334">**IMPORTANT**: Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="a87e3-334">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="a87e3-335">Экспериментальные свойства могут быть не завершены, и могут претерпеть изменения, прежде чем стать полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="a87e3-335">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="a87e3-336">Он предоставляется только для целей тестирования и разведки и не должен использоваться в производственных целях.</span><span class="sxs-lookup"><span data-stu-id="a87e3-336">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="a87e3-337">по умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="a87e3-337">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="a87e3-338">boolean</span><span class="sxs-lookup"><span data-stu-id="a87e3-338">boolean</span></span>|||<span data-ttu-id="a87e3-339">Значение, указывающее, где бот поддерживает видеозвонки.</span><span class="sxs-lookup"><span data-stu-id="a87e3-339">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="a87e3-340">**IMPORTANT**: Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="a87e3-340">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="a87e3-341">Экспериментальные свойства могут быть не завершены, и могут претерпеть изменения, прежде чем стать полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="a87e3-341">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="a87e3-342">Он предоставляется только для целей тестирования и разведки и не должен использоваться в производственных целях.</span><span class="sxs-lookup"><span data-stu-id="a87e3-342">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="a87e3-343">по умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="a87e3-343">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="a87e3-344">боты.commandLists</span><span class="sxs-lookup"><span data-stu-id="a87e3-344">bots.commandLists</span></span>

<span data-ttu-id="a87e3-345">Дополнительный список команд, которые ваш бот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="a87e3-345">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="a87e3-346">Объект — это массив (максимум 2 элемента) со всеми элементами `object` типа; вы должны определить отдельный список команд для каждой области, которую поддерживает ваш бот.</span><span class="sxs-lookup"><span data-stu-id="a87e3-346">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="a87e3-347">Дополнительную [информацию можно](~/bots/how-to/create-a-bot-commands-menu.md) получить в меню Bot.</span><span class="sxs-lookup"><span data-stu-id="a87e3-347">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="a87e3-348">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-348">Name</span></span>| <span data-ttu-id="a87e3-349">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-349">Type</span></span>| <span data-ttu-id="a87e3-350">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-350">Maximum size</span></span> | <span data-ttu-id="a87e3-351">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-351">Required</span></span> | <span data-ttu-id="a87e3-352">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-352">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="a87e3-353">массив enums</span><span class="sxs-lookup"><span data-stu-id="a87e3-353">array of enums</span></span>|<span data-ttu-id="a87e3-354">3</span><span class="sxs-lookup"><span data-stu-id="a87e3-354">3</span></span>|<span data-ttu-id="a87e3-355">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-355">✔</span></span>|<span data-ttu-id="a87e3-356">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="a87e3-356">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="a87e3-357">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="a87e3-357">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="a87e3-358">массив объектов</span><span class="sxs-lookup"><span data-stu-id="a87e3-358">array of objects</span></span>|<span data-ttu-id="a87e3-359">10 </span><span class="sxs-lookup"><span data-stu-id="a87e3-359">10</span></span>|<span data-ttu-id="a87e3-360">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-360">✔</span></span>|<span data-ttu-id="a87e3-361">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="a87e3-361">An array of commands the bot supports:</span></span><br><span data-ttu-id="a87e3-362">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="a87e3-362">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="a87e3-363">`description`: простое описание или пример синтаксиса команды и его аргумента (строка, 128).</span><span class="sxs-lookup"><span data-stu-id="a87e3-363">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="a87e3-364">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="a87e3-364">bots.commandLists.commands</span></span>

|<span data-ttu-id="a87e3-365">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-365">Name</span></span>| <span data-ttu-id="a87e3-366">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-366">Type</span></span>| <span data-ttu-id="a87e3-367">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-367">Maximum size</span></span> | <span data-ttu-id="a87e3-368">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-368">Required</span></span> | <span data-ttu-id="a87e3-369">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-369">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="a87e3-370">title</span><span class="sxs-lookup"><span data-stu-id="a87e3-370">title</span></span>|<span data-ttu-id="a87e3-371">string</span><span class="sxs-lookup"><span data-stu-id="a87e3-371">string</span></span>|<span data-ttu-id="a87e3-372">12 </span><span class="sxs-lookup"><span data-stu-id="a87e3-372">12</span></span>|<span data-ttu-id="a87e3-373">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-373">✔</span></span>|<span data-ttu-id="a87e3-374">Имя команды бота.</span><span class="sxs-lookup"><span data-stu-id="a87e3-374">The bot command name.</span></span>|
|<span data-ttu-id="a87e3-375">description</span><span class="sxs-lookup"><span data-stu-id="a87e3-375">description</span></span>|<span data-ttu-id="a87e3-376">string</span><span class="sxs-lookup"><span data-stu-id="a87e3-376">string</span></span>|<span data-ttu-id="a87e3-377">128 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-377">128 characters</span></span>|<span data-ttu-id="a87e3-378">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-378">✔</span></span>|<span data-ttu-id="a87e3-379">Простое текстовое описание или пример командного синтаксиса и его аргументов.</span><span class="sxs-lookup"><span data-stu-id="a87e3-379">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="a87e3-380">Соединители</span><span class="sxs-lookup"><span data-stu-id="a87e3-380">connectors</span></span>

<span data-ttu-id="a87e3-381">**Необязательно** - массив</span><span class="sxs-lookup"><span data-stu-id="a87e3-381">**Optional** — array</span></span>

<span data-ttu-id="a87e3-382">Блок `connectors` определяет Office 365 разъем для приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-382">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="a87e3-383">Объект является массивом (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="a87e3-383">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="a87e3-384">Этот блок необходим только для решений, которые обеспечивают разъем.</span><span class="sxs-lookup"><span data-stu-id="a87e3-384">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="a87e3-385">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-385">Name</span></span>| <span data-ttu-id="a87e3-386">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-386">Type</span></span>| <span data-ttu-id="a87e3-387">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-387">Maximum size</span></span> | <span data-ttu-id="a87e3-388">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-388">Required</span></span> | <span data-ttu-id="a87e3-389">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-389">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="a87e3-390">string</span><span class="sxs-lookup"><span data-stu-id="a87e3-390">string</span></span>|<span data-ttu-id="a87e3-391">2048 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-391">2048 characters</span></span>|<span data-ttu-id="a87e3-392">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-392">✔</span></span>|<span data-ttu-id="a87e3-393"> Https:// URL для использования при настройке разъема.</span><span class="sxs-lookup"><span data-stu-id="a87e3-393">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="a87e3-394">массив enums</span><span class="sxs-lookup"><span data-stu-id="a87e3-394">array of enums</span></span>|<span data-ttu-id="a87e3-395">1</span><span class="sxs-lookup"><span data-stu-id="a87e3-395">1</span></span>|<span data-ttu-id="a87e3-396">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-396">✔</span></span>|<span data-ttu-id="a87e3-397">Определяет, предлагает ли Connector опыт в контексте канала в , или `team` опыт, установленный для отдельного пользователя в одиночку ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="a87e3-397">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a87e3-398">В настоящее время `team` поддерживается только область охвата.</span><span class="sxs-lookup"><span data-stu-id="a87e3-398">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="a87e3-399">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-399">string</span></span>|<span data-ttu-id="a87e3-400">64 символа</span><span class="sxs-lookup"><span data-stu-id="a87e3-400">64 characters</span></span>|<span data-ttu-id="a87e3-401">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-401">✔</span></span>|<span data-ttu-id="a87e3-402">Уникальный идентификатор разъема, который соответствует его идентификатору в панели [разработчиков connectors.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="a87e3-402">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="a87e3-403">составьтеЭкстрасты</span><span class="sxs-lookup"><span data-stu-id="a87e3-403">composeExtensions</span></span>

<span data-ttu-id="a87e3-404">**Необязательно** - массив</span><span class="sxs-lookup"><span data-stu-id="a87e3-404">**Optional** — array</span></span>

<span data-ttu-id="a87e3-405">Определяет расширение обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-405">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="a87e3-406">Название функции было изменено с "составить расширение" на "расширение обмена сообщениями" в ноябре 2017 года, но имя манифеста остается прежним, так что существующие расширения продолжают функционировать.</span><span class="sxs-lookup"><span data-stu-id="a87e3-406">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="a87e3-407">Элемент массив (максимум 1 элемент) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-407">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="a87e3-408">Этот блок необходим только для решений, которые обеспечивают расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="a87e3-408">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="a87e3-409">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-409">Name</span></span>| <span data-ttu-id="a87e3-410">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-410">Type</span></span> | <span data-ttu-id="a87e3-411">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-411">Maximum Size</span></span> | <span data-ttu-id="a87e3-412">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-412">Required</span></span> | <span data-ttu-id="a87e3-413">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-413">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a87e3-414">string</span><span class="sxs-lookup"><span data-stu-id="a87e3-414">string</span></span>|<span data-ttu-id="a87e3-415">64</span><span class="sxs-lookup"><span data-stu-id="a87e3-415">64</span></span>|<span data-ttu-id="a87e3-416">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-416">✔</span></span>|<span data-ttu-id="a87e3-417">Уникальный идентификатор приложения Microsoft для бота, который поддерживает расширение обмена сообщениями, как зарегистрировано в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a87e3-417">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="a87e3-418">Это вполне может быть так же, как общий идентификатор App.</span><span class="sxs-lookup"><span data-stu-id="a87e3-418">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="a87e3-419">массив объектов</span><span class="sxs-lookup"><span data-stu-id="a87e3-419">array of objects</span></span>|<span data-ttu-id="a87e3-420">10 </span><span class="sxs-lookup"><span data-stu-id="a87e3-420">10</span></span>|<span data-ttu-id="a87e3-421">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-421">✔</span></span>|<span data-ttu-id="a87e3-422">Массив команд, которые поддерживает расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="a87e3-422">Array of commands the messaging extension supports.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="a87e3-423">boolean</span><span class="sxs-lookup"><span data-stu-id="a87e3-423">boolean</span></span>|||<span data-ttu-id="a87e3-424">Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="a87e3-424">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="a87e3-425">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="a87e3-425">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="a87e3-426">массив объектов</span><span class="sxs-lookup"><span data-stu-id="a87e3-426">array of Objects</span></span>|<span data-ttu-id="a87e3-427">5 </span><span class="sxs-lookup"><span data-stu-id="a87e3-427">5</span></span>||<span data-ttu-id="a87e3-428">Список обработчиков, позволяющих вызывать приложения при работах определенных условий.</span><span class="sxs-lookup"><span data-stu-id="a87e3-428">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="a87e3-429">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-429">string</span></span>|||<span data-ttu-id="a87e3-430">Тип обработчика сообщений.</span><span class="sxs-lookup"><span data-stu-id="a87e3-430">The type of message handler.</span></span> <span data-ttu-id="a87e3-431">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="a87e3-431">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="a87e3-432">массив струнных</span><span class="sxs-lookup"><span data-stu-id="a87e3-432">array of Strings</span></span>|||<span data-ttu-id="a87e3-433">Массив доменов, на которые может зарегистрироваться обработчик ссылок.</span><span class="sxs-lookup"><span data-stu-id="a87e3-433">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="a87e3-434">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="a87e3-434">composeExtensions.commands</span></span>

<span data-ttu-id="a87e3-435">Расширение обмена сообщениями должно объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="a87e3-435">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="a87e3-436">Каждая команда отображается Microsoft Teams в качестве потенциального взаимодействия из точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a87e3-436">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="a87e3-437">Существует максимум 10 команд.</span><span class="sxs-lookup"><span data-stu-id="a87e3-437">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="a87e3-438">Каждый элемент команды является объектом со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="a87e3-438">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="a87e3-439">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-439">Name</span></span>| <span data-ttu-id="a87e3-440">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-440">Type</span></span>| <span data-ttu-id="a87e3-441">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-441">Maximum size</span></span> | <span data-ttu-id="a87e3-442">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-442">Required</span></span> | <span data-ttu-id="a87e3-443">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-443">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="a87e3-444">string</span><span class="sxs-lookup"><span data-stu-id="a87e3-444">string</span></span>|<span data-ttu-id="a87e3-445">64 символа</span><span class="sxs-lookup"><span data-stu-id="a87e3-445">64 characters</span></span>|<span data-ttu-id="a87e3-446">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-446">✔</span></span>|<span data-ttu-id="a87e3-447">Идентификатор команды.</span><span class="sxs-lookup"><span data-stu-id="a87e3-447">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="a87e3-448">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-448">string</span></span>|<span data-ttu-id="a87e3-449">32 символа</span><span class="sxs-lookup"><span data-stu-id="a87e3-449">32 characters</span></span>|<span data-ttu-id="a87e3-450">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-450">✔</span></span>|<span data-ttu-id="a87e3-451">Удобное для пользователя название команды.</span><span class="sxs-lookup"><span data-stu-id="a87e3-451">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="a87e3-452">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-452">string</span></span>|<span data-ttu-id="a87e3-453">64 символа</span><span class="sxs-lookup"><span data-stu-id="a87e3-453">64 characters</span></span>||<span data-ttu-id="a87e3-454">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="a87e3-454">Type of the command.</span></span> <span data-ttu-id="a87e3-455">Один из `query` или `action` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-455">One of `query` or `action`.</span></span> <span data-ttu-id="a87e3-456">По умолчанию: **запрос**.</span><span class="sxs-lookup"><span data-stu-id="a87e3-456">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="a87e3-457">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-457">string</span></span>|<span data-ttu-id="a87e3-458">128 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-458">128 characters</span></span>||<span data-ttu-id="a87e3-459">Описание, которое отображается пользователям, чтобы указать цель этой команды.</span><span class="sxs-lookup"><span data-stu-id="a87e3-459">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="a87e3-460">boolean</span><span class="sxs-lookup"><span data-stu-id="a87e3-460">boolean</span></span>|||<span data-ttu-id="a87e3-461">Значение boolean указывает, работает ли команда изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="a87e3-461">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="a87e3-462">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="a87e3-462">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="a87e3-463">массив струнных</span><span class="sxs-lookup"><span data-stu-id="a87e3-463">array of Strings</span></span>|<span data-ttu-id="a87e3-464">3</span><span class="sxs-lookup"><span data-stu-id="a87e3-464">3</span></span>||<span data-ttu-id="a87e3-465">Определяет, откуда можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-465">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="a87e3-466">Любое сочетание `compose` `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-466">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="a87e3-467">Значение по умолчанию: `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="a87e3-467">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="a87e3-468">boolean</span><span class="sxs-lookup"><span data-stu-id="a87e3-468">boolean</span></span>|||<span data-ttu-id="a87e3-469">Boolean значение, которое указывает, если он должен получить модуль задачи динамически.</span><span class="sxs-lookup"><span data-stu-id="a87e3-469">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="a87e3-470">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="a87e3-470">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="a87e3-471">объект</span><span class="sxs-lookup"><span data-stu-id="a87e3-471">object</span></span>|||<span data-ttu-id="a87e3-472">Укажите модуль задачи для предварительной загрузки при использовании команды расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="a87e3-472">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="a87e3-473">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-473">string</span></span>|<span data-ttu-id="a87e3-474">64 символа</span><span class="sxs-lookup"><span data-stu-id="a87e3-474">64 characters</span></span>||<span data-ttu-id="a87e3-475">Начальное название диалога.</span><span class="sxs-lookup"><span data-stu-id="a87e3-475">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="a87e3-476">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-476">string</span></span>|||<span data-ttu-id="a87e3-477">Ширина Dialog - либо число пикселей, либо макет по умолчанию, такой как "большой", "средний" или "малый".</span><span class="sxs-lookup"><span data-stu-id="a87e3-477">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="a87e3-478">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-478">string</span></span>|||<span data-ttu-id="a87e3-479">Высота Dialog - либо число пикселей, либо макет по умолчанию, такой как "большой", "средний" или "малый".</span><span class="sxs-lookup"><span data-stu-id="a87e3-479">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="a87e3-480">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-480">string</span></span>|||<span data-ttu-id="a87e3-481">Первоначальный URL веб-адреса.</span><span class="sxs-lookup"><span data-stu-id="a87e3-481">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="a87e3-482">массив объекта</span><span class="sxs-lookup"><span data-stu-id="a87e3-482">array of object</span></span>|<span data-ttu-id="a87e3-483">5 наименований</span><span class="sxs-lookup"><span data-stu-id="a87e3-483">5 items</span></span>|<span data-ttu-id="a87e3-484">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-484">✔</span></span>|<span data-ttu-id="a87e3-485">Список параметров, которые принимает команда.</span><span class="sxs-lookup"><span data-stu-id="a87e3-485">The list of parameters the command takes.</span></span> <span data-ttu-id="a87e3-486">Минимум: 1; максимум: 5.</span><span class="sxs-lookup"><span data-stu-id="a87e3-486">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="a87e3-487">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-487">string</span></span>|<span data-ttu-id="a87e3-488">64 символа</span><span class="sxs-lookup"><span data-stu-id="a87e3-488">64 characters</span></span>|<span data-ttu-id="a87e3-489">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-489">✔</span></span>|<span data-ttu-id="a87e3-490">Название параметра, как оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="a87e3-490">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="a87e3-491">Это включено в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="a87e3-491">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="a87e3-492">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-492">string</span></span>|<span data-ttu-id="a87e3-493">32 символа</span><span class="sxs-lookup"><span data-stu-id="a87e3-493">32 characters</span></span>|<span data-ttu-id="a87e3-494">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-494">✔</span></span>|<span data-ttu-id="a87e3-495">Удобное название для параметра.</span><span class="sxs-lookup"><span data-stu-id="a87e3-495">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="a87e3-496">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-496">string</span></span>|<span data-ttu-id="a87e3-497">128 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-497">128 characters</span></span>||<span data-ttu-id="a87e3-498">Удобный строка, описывая цель этого параметра.</span><span class="sxs-lookup"><span data-stu-id="a87e3-498">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="a87e3-499">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-499">string</span></span>|<span data-ttu-id="a87e3-500">512 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-500">512 characters</span></span>||<span data-ttu-id="a87e3-501">Начальное значение параметра.</span><span class="sxs-lookup"><span data-stu-id="a87e3-501">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="a87e3-502">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-502">string</span></span>|<span data-ttu-id="a87e3-503">128 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-503">128 characters</span></span>||<span data-ttu-id="a87e3-504">Определяет тип управления, отображаемый на модуле задачи для `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-504">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="a87e3-505">Один из `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-505">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="a87e3-506">массив объектов</span><span class="sxs-lookup"><span data-stu-id="a87e3-506">array of objects</span></span>|<span data-ttu-id="a87e3-507">10 наименований</span><span class="sxs-lookup"><span data-stu-id="a87e3-507">10 items</span></span>||<span data-ttu-id="a87e3-508">Варианты выбора для `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-508">The choice options for the`choiceset`.</span></span> <span data-ttu-id="a87e3-509">Использовать только тогда, `parameter.inputType` когда `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-509">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="a87e3-510">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-510">string</span></span>|<span data-ttu-id="a87e3-511">128 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-511">128 characters</span></span>|<span data-ttu-id="a87e3-512">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-512">✔</span></span>|<span data-ttu-id="a87e3-513">Название выбора.</span><span class="sxs-lookup"><span data-stu-id="a87e3-513">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="a87e3-514">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-514">string</span></span>|<span data-ttu-id="a87e3-515">512 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-515">512 characters</span></span>|<span data-ttu-id="a87e3-516">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-516">✔</span></span>|<span data-ttu-id="a87e3-517">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="a87e3-517">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="a87e3-518">permissions</span><span class="sxs-lookup"><span data-stu-id="a87e3-518">permissions</span></span>

<span data-ttu-id="a87e3-519">**Необязательно** - массив строк</span><span class="sxs-lookup"><span data-stu-id="a87e3-519">**Optional** — array of strings</span></span>

<span data-ttu-id="a87e3-520">Массив, в `string` котором указывается, какие разрешения запрашивает приложение, что позволяет конечной пользователям знать, как выполняет расширение.</span><span class="sxs-lookup"><span data-stu-id="a87e3-520">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="a87e3-521">Следующие варианты не являются эксклюзивными:</span><span class="sxs-lookup"><span data-stu-id="a87e3-521">The following options are non-exclusive:</span></span>

* <span data-ttu-id="a87e3-522">`identity`&emsp;Требуется идентификационная информация пользователя.</span><span class="sxs-lookup"><span data-stu-id="a87e3-522">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="a87e3-523">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам команды.</span><span class="sxs-lookup"><span data-stu-id="a87e3-523">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="a87e3-524">Изменение этих разрешений во время обновления приложения приводит к тому, что пользователи повторяют процесс согласия после запуска обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-524">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="a87e3-525">Дополнительную [информацию можно получить](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) в обновлении приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-525">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="a87e3-526">устройствоПермиссии</span><span class="sxs-lookup"><span data-stu-id="a87e3-526">devicePermissions</span></span>

<span data-ttu-id="a87e3-527">**Необязательно** - массив строк</span><span class="sxs-lookup"><span data-stu-id="a87e3-527">**Optional** — array of strings</span></span>

<span data-ttu-id="a87e3-528">Предоставляет родные функции на устройстве пользователя, к которые ваше приложение запрашивает доступ.</span><span class="sxs-lookup"><span data-stu-id="a87e3-528">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="a87e3-529">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="a87e3-529">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="a87e3-530">действительныйДомайнс</span><span class="sxs-lookup"><span data-stu-id="a87e3-530">validDomains</span></span>

<span data-ttu-id="a87e3-531">**Дополнительно,** за исключением **Требуется,** где отметил.</span><span class="sxs-lookup"><span data-stu-id="a87e3-531">**Optional**, except **Required** where noted.</span></span>

<span data-ttu-id="a87e3-532">Список действительных доменов для веб-сайтов, которые приложение планирует загрузить в Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="a87e3-532">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="a87e3-533">Списки доменов могут включать подстановочные знаки, `*.example.com` например.</span><span class="sxs-lookup"><span data-stu-id="a87e3-533">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="a87e3-534">Это соответствует ровно одному сегменту домена; если вам нужно, чтобы `a.b.example.com` соответствовать затем использовать `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-534">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="a87e3-535">Если конфигурация вкладок или пользовательский интерфейс содержимого должны перемещаться в любой другой домен, кроме того, который используется для конфигурации вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="a87e3-535">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="a87e3-536">Нет **необходимости включать** в приложение домены поставщиков идентификации, которые вы хотите поддержать.</span><span class="sxs-lookup"><span data-stu-id="a87e3-536">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="a87e3-537">Например, для проверки подлинности с помощью Идентификатора Google необходимо перенаправить на accounts.google.com, однако, вы не должны включать accounts.google.com в `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-537">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="a87e3-538">Teams приложения, которые требуют, чтобы их собственные URL-адреса с точкой обмена функционировали хорошо, включают в свой действительный список доменов «teamsitedomain».</span><span class="sxs-lookup"><span data-stu-id="a87e3-538">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a87e3-539">Не добавляйте домены, которые находятся вне вашего контроля, ни непосредственно, ни через подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="a87e3-539">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="a87e3-540">Например, `yourapp.onmicrosoft.com` является действительным, однако, `*.onmicrosoft.com` не является действительным.</span><span class="sxs-lookup"><span data-stu-id="a87e3-540">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="a87e3-541">Объект является массивом со всеми элементами `string` типа.</span><span class="sxs-lookup"><span data-stu-id="a87e3-541">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="a87e3-542">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="a87e3-542">webApplicationInfo</span></span>

<span data-ttu-id="a87e3-543">**Факультативно** - объект</span><span class="sxs-lookup"><span data-stu-id="a87e3-543">**Optional** — object</span></span>

<span data-ttu-id="a87e3-544">Предоставьте свой Azure Active Directory (AAD) App ID и Microsoft Graph, чтобы помочь пользователям беспрепятственно войти в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="a87e3-544">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="a87e3-545">Если ваше приложение зарегистрировано в AAD, вы должны предоставить идентификатор App ID, чтобы администраторы могли легко просмотреть разрешения и дать согласие в Teams центре.</span><span class="sxs-lookup"><span data-stu-id="a87e3-545">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="a87e3-546">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-546">Name</span></span>| <span data-ttu-id="a87e3-547">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-547">Type</span></span>| <span data-ttu-id="a87e3-548">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-548">Maximum size</span></span> | <span data-ttu-id="a87e3-549">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-549">Required</span></span> | <span data-ttu-id="a87e3-550">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-550">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="a87e3-551">string</span><span class="sxs-lookup"><span data-stu-id="a87e3-551">string</span></span>|<span data-ttu-id="a87e3-552">36 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-552">36 characters</span></span>|<span data-ttu-id="a87e3-553">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-553">✔</span></span>|<span data-ttu-id="a87e3-554">Идентификатор приложения AAD приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-554">AAD application id of the app.</span></span> <span data-ttu-id="a87e3-555">Этот идентификатор должен быть GUID.</span><span class="sxs-lookup"><span data-stu-id="a87e3-555">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="a87e3-556">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-556">string</span></span>|<span data-ttu-id="a87e3-557">2048 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-557">2048 characters</span></span>|<span data-ttu-id="a87e3-558">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-558">✔</span></span>|<span data-ttu-id="a87e3-559">URL-адрес ресурса приложения для приобретения auth токена для SSO.</span><span class="sxs-lookup"><span data-stu-id="a87e3-559">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="a87e3-560">**ПРИМЕЧАНИЕ:** Если вы не используете SSO, убедитесь, что вы вводите значение строки манекена в этой области в манифест приложения, например, https://notapplicable чтобы избежать ответа на ошибку.</span><span class="sxs-lookup"><span data-stu-id="a87e3-560">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="a87e3-561">массив строк</span><span class="sxs-lookup"><span data-stu-id="a87e3-561">array of strings</span></span>|<span data-ttu-id="a87e3-562">128 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-562">128 characters</span></span>||<span data-ttu-id="a87e3-563">Укажите конкретное [согласие гранулированного ресурса.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="a87e3-563">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="a87e3-564">showLoadingИндикатор</span><span class="sxs-lookup"><span data-stu-id="a87e3-564">showLoadingIndicator</span></span>

<span data-ttu-id="a87e3-565">**Факультативно** - булеан</span><span class="sxs-lookup"><span data-stu-id="a87e3-565">**Optional** — boolean</span></span>

<span data-ttu-id="a87e3-566">Указывает, следует ли показывать индикатор загрузки при загрузке приложения или вкладки.</span><span class="sxs-lookup"><span data-stu-id="a87e3-566">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="a87e3-567">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="a87e3-567">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="a87e3-568">Если вы `showLoadingIndicator` выберете такую же истинную в манифесте приложения, чтобы правильно загрузить страницу, измените страницы содержимого вкладок и модулей задач, описанные [в документе индикатора загрузки.](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="a87e3-568">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="a87e3-569">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="a87e3-569">isFullScreen</span></span>

 <span data-ttu-id="a87e3-570">**Факультативно** - булеан</span><span class="sxs-lookup"><span data-stu-id="a87e3-570">**Optional** — boolean</span></span>

<span data-ttu-id="a87e3-571">Укажите, где личное приложение отображается с баром заголовка вкладок или без него.</span><span class="sxs-lookup"><span data-stu-id="a87e3-571">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="a87e3-572">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="a87e3-572">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="a87e3-573">activities</span><span class="sxs-lookup"><span data-stu-id="a87e3-573">activities</span></span>

<span data-ttu-id="a87e3-574">**Факультативно** - объект</span><span class="sxs-lookup"><span data-stu-id="a87e3-574">**Optional** — object</span></span>

<span data-ttu-id="a87e3-575">Определите свойства, которые приложение использует для размещения канала активности пользователя.</span><span class="sxs-lookup"><span data-stu-id="a87e3-575">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="a87e3-576">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-576">Name</span></span>| <span data-ttu-id="a87e3-577">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-577">Type</span></span>| <span data-ttu-id="a87e3-578">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-578">Maximum size</span></span> | <span data-ttu-id="a87e3-579">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-579">Required</span></span> | <span data-ttu-id="a87e3-580">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-580">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="a87e3-581">массив объектов</span><span class="sxs-lookup"><span data-stu-id="a87e3-581">array of Objects</span></span>|<span data-ttu-id="a87e3-582">128 наименований</span><span class="sxs-lookup"><span data-stu-id="a87e3-582">128 items</span></span>| | <span data-ttu-id="a87e3-583">Предоставьте типы действий, которые ваше приложение может опубликовать в ленте действий пользователей.</span><span class="sxs-lookup"><span data-stu-id="a87e3-583">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="a87e3-584">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="a87e3-584">activities.activityTypes</span></span>

|<span data-ttu-id="a87e3-585">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-585">Name</span></span>| <span data-ttu-id="a87e3-586">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-586">Type</span></span>| <span data-ttu-id="a87e3-587">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-587">Maximum size</span></span> | <span data-ttu-id="a87e3-588">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-588">Required</span></span> | <span data-ttu-id="a87e3-589">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-589">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="a87e3-590">string</span><span class="sxs-lookup"><span data-stu-id="a87e3-590">string</span></span>|<span data-ttu-id="a87e3-591">32 символа</span><span class="sxs-lookup"><span data-stu-id="a87e3-591">32 characters</span></span>|<span data-ttu-id="a87e3-592">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-592">✔</span></span>|<span data-ttu-id="a87e3-593">Тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="a87e3-593">The notification type.</span></span> <span data-ttu-id="a87e3-594">*Смотрите ниже*.</span><span class="sxs-lookup"><span data-stu-id="a87e3-594">*See below*.</span></span>|
|`description`|<span data-ttu-id="a87e3-595">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-595">string</span></span>|<span data-ttu-id="a87e3-596">128 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-596">128 characters</span></span>|<span data-ttu-id="a87e3-597">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-597">✔</span></span>|<span data-ttu-id="a87e3-598">Краткое описание уведомления.</span><span class="sxs-lookup"><span data-stu-id="a87e3-598">A brief description of the notification.</span></span> <span data-ttu-id="a87e3-599">*Смотрите ниже*.</span><span class="sxs-lookup"><span data-stu-id="a87e3-599">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="a87e3-600">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-600">string</span></span>|<span data-ttu-id="a87e3-601">128 символов</span><span class="sxs-lookup"><span data-stu-id="a87e3-601">128 characters</span></span>|<span data-ttu-id="a87e3-602">✔</span><span class="sxs-lookup"><span data-stu-id="a87e3-602">✔</span></span>|<span data-ttu-id="a87e3-603">Например: «Актер» создал задачу «задачаИд» для вас»</span><span class="sxs-lookup"><span data-stu-id="a87e3-603">Ex: "{actor} created task {taskId} for you"</span></span>|

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

## <a name="defaultinstallscope"></a><span data-ttu-id="a87e3-604">по умолчаниюИнсталлСкоп</span><span class="sxs-lookup"><span data-stu-id="a87e3-604">defaultInstallScope</span></span>

<span data-ttu-id="a87e3-605">**Необязательно** - строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-605">**Optional** - string</span></span>

<span data-ttu-id="a87e3-606">Определяет область установки, определяемую для этого приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a87e3-606">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="a87e3-607">Определенная область будет параметр, отображаемый на кнопке, когда пользователь пытается добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="a87e3-607">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="a87e3-608">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="a87e3-608">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="a87e3-609">по умолчаниюГруппаКапабельность</span><span class="sxs-lookup"><span data-stu-id="a87e3-609">defaultGroupCapability</span></span>

<span data-ttu-id="a87e3-610">**Необязательно** - объект</span><span class="sxs-lookup"><span data-stu-id="a87e3-610">**Optional** - object</span></span>

<span data-ttu-id="a87e3-611">При выборе области установки группы она определяет возможности по умолчанию при установке приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-611">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="a87e3-612">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="a87e3-612">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="a87e3-613">Имя</span><span class="sxs-lookup"><span data-stu-id="a87e3-613">Name</span></span>| <span data-ttu-id="a87e3-614">Тип</span><span class="sxs-lookup"><span data-stu-id="a87e3-614">Type</span></span>| <span data-ttu-id="a87e3-615">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="a87e3-615">Maximum size</span></span> | <span data-ttu-id="a87e3-616">Обязательный</span><span class="sxs-lookup"><span data-stu-id="a87e3-616">Required</span></span> | <span data-ttu-id="a87e3-617">Описание</span><span class="sxs-lookup"><span data-stu-id="a87e3-617">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="a87e3-618">string</span><span class="sxs-lookup"><span data-stu-id="a87e3-618">string</span></span>|||<span data-ttu-id="a87e3-619">Когда выбрана область `team` установки, это поле определяет доступную возможность по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a87e3-619">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="a87e3-620">Варианты: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-620">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="a87e3-621">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-621">string</span></span>|||<span data-ttu-id="a87e3-622">Когда выбрана область `groupchat` установки, это поле определяет доступную возможность по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a87e3-622">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="a87e3-623">Варианты: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-623">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="a87e3-624">Строка</span><span class="sxs-lookup"><span data-stu-id="a87e3-624">string</span></span>|||<span data-ttu-id="a87e3-625">Когда выбрана область `meetings` установки, это поле определяет доступную возможность по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a87e3-625">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="a87e3-626">Варианты: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="a87e3-626">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="a87e3-627">настраиваемыеПредложения</span><span class="sxs-lookup"><span data-stu-id="a87e3-627">configurableProperties</span></span>

<span data-ttu-id="a87e3-628">**Дополнительно** - массив</span><span class="sxs-lookup"><span data-stu-id="a87e3-628">**Optional** - array</span></span>

<span data-ttu-id="a87e3-629">Блок `configurableProperties` определяет свойства приложения, которые Teams администратор может настроить.</span><span class="sxs-lookup"><span data-stu-id="a87e3-629">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="a87e3-630">Для получения дополнительной [информации, смотрите настроить приложения в Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="a87e3-630">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="a87e3-631">Необходимо определить минимум одно свойство.</span><span class="sxs-lookup"><span data-stu-id="a87e3-631">A minimum of one property must be defined.</span></span> <span data-ttu-id="a87e3-632">Вы можете определить максимум девять свойств в этом блоке.</span><span class="sxs-lookup"><span data-stu-id="a87e3-632">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="a87e3-633">В качестве наилучшей практики необходимо предоставить рекомендации по настройке для пользователей и клиентов приложений, чтобы следовать при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-633">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span>

<span data-ttu-id="a87e3-634">Вы можете определить любое из следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="a87e3-634">You can define any of the following properties:</span></span>
* <span data-ttu-id="a87e3-635">`name`: Позволяет администратору изменить имя дисплея приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-635">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="a87e3-636">`shortDescription`: Позволяет администратору изменить краткое описание приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-636">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="a87e3-637">`longDescription`: Позволяет администратору изменить подробное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="a87e3-637">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="a87e3-638">`smallImageUrl`: Это `outline` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="a87e3-638">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="a87e3-639">`largeImageUrl`: Это `color` свойство в `icons` блоке манифеста.</span><span class="sxs-lookup"><span data-stu-id="a87e3-639">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="a87e3-640">`accentColor`: Это цвет для использования в сочетании с и в качестве фона для вашего контура иконки.</span><span class="sxs-lookup"><span data-stu-id="a87e3-640">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="a87e3-641">`websiteUrl`: Это https:// URL на веб-сайте разработчика.</span><span class="sxs-lookup"><span data-stu-id="a87e3-641">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="a87e3-642">`privacyUrl`: Это https:// URL-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="a87e3-642">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="a87e3-643">`termsOfUseUrl`: Это https:// URL-адрес к условиям использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="a87e3-643">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>


