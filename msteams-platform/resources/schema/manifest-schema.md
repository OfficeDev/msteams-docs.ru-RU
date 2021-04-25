---
title: Справка о схеме манифеста
description: Описывает схему манифеста для Microsoft Teams
ms.topic: reference
ms.author: lajanuar
keywords: Схема манифеста команд
ms.openlocfilehash: d4dd299a9e848820e81f87361460b5b8b14f15b7
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946447"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="ba8df-104">Справка. Схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ba8df-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="ba8df-105">Манифест Teams описывает интеграцию приложения в продукт Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ba8df-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="ba8df-106">Манифест должен соответствовать схеме, которая была на [`https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json) уровне .</span><span class="sxs-lookup"><span data-stu-id="ba8df-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="ba8df-107">Поддерживаются и предыдущие версии 1.0-1.4 (с помощью "v1.x" в URL-адресе).</span><span class="sxs-lookup"><span data-stu-id="ba8df-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="ba8df-108">В следующем примере схемы показаны все варианты раздвивемости.</span><span class="sxs-lookup"><span data-stu-id="ba8df-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="ba8df-109">Образец полного манифеста</span><span class="sxs-lookup"><span data-stu-id="ba8df-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",
  "manifestVersion": "1.9",
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
  }
}
```

<span data-ttu-id="ba8df-110">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="ba8df-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="ba8df-111">$schema</span><span class="sxs-lookup"><span data-stu-id="ba8df-111">$schema</span></span>

<span data-ttu-id="ba8df-112">Необязательный, но рекомендуемый — строка</span><span class="sxs-lookup"><span data-stu-id="ba8df-112">Optional, but recommended — string</span></span>

<span data-ttu-id="ba8df-113">URL https:// ссылки на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="ba8df-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="ba8df-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="ba8df-114">manifestVersion</span></span>

<span data-ttu-id="ba8df-115">**Обязательно —** строка</span><span class="sxs-lookup"><span data-stu-id="ba8df-115">**Required** — string</span></span>

<span data-ttu-id="ba8df-116">Версия схемы манифеста, используемая этим манифестом.</span><span class="sxs-lookup"><span data-stu-id="ba8df-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="ba8df-117">Должно быть 1,9.</span><span class="sxs-lookup"><span data-stu-id="ba8df-117">It must be 1.9.</span></span>

## <a name="version"></a><span data-ttu-id="ba8df-118">version</span><span class="sxs-lookup"><span data-stu-id="ba8df-118">version</span></span>

<span data-ttu-id="ba8df-119">**Обязательно —** строка</span><span class="sxs-lookup"><span data-stu-id="ba8df-119">**Required** — string</span></span>

<span data-ttu-id="ba8df-120">Версия определенного приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-120">The version of a specific app.</span></span> <span data-ttu-id="ba8df-121">Если вы что-то обновите в манифесте, версия также должна быть приумножная.</span><span class="sxs-lookup"><span data-stu-id="ba8df-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="ba8df-122">Таким образом, при установке нового манифеста он переописает существующий и пользователь получает новые функции.</span><span class="sxs-lookup"><span data-stu-id="ba8df-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="ba8df-123">Если это приложение было отправлено в магазин, новый манифест должен быть повторно отправлен и повторно проверен.</span><span class="sxs-lookup"><span data-stu-id="ba8df-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="ba8df-124">Пользователи приложения получают новый обновленный манифест автоматически в течение нескольких часов после утверждения манифеста.</span><span class="sxs-lookup"><span data-stu-id="ba8df-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="ba8df-125">Если приложение запрашивает разрешения на изменение, пользователям будет предложено обновить и повторно согласиться на приложение.</span><span class="sxs-lookup"><span data-stu-id="ba8df-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="ba8df-126">Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="ba8df-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="ba8df-127">id</span><span class="sxs-lookup"><span data-stu-id="ba8df-127">id</span></span>

<span data-ttu-id="ba8df-128">**Обязательно —** ID приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="ba8df-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="ba8df-129">Идентификатор — уникальный идентификатор, созданный Корпорацией Майкрософт для приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="ba8df-130">У вас есть ID, если бот зарегистрирован через Microsoft Bot Framework или веб-приложение вкладки уже вошел в Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ba8df-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="ba8df-131">Здесь необходимо ввести ID.</span><span class="sxs-lookup"><span data-stu-id="ba8df-131">You must enter the ID here.</span></span> <span data-ttu-id="ba8df-132">В противном случае необходимо создать новый ID на портале [регистрации приложений Майкрософт.](https://aka.ms/appregistrations)</span><span class="sxs-lookup"><span data-stu-id="ba8df-132">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="ba8df-133">При добавлении бота используйте тот же ID.</span><span class="sxs-lookup"><span data-stu-id="ba8df-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="ba8df-134">Если вы передаете обновление существующему приложению в AppSource, ID в манифесте не должен изменяться.</span><span class="sxs-lookup"><span data-stu-id="ba8df-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="ba8df-135">developer</span><span class="sxs-lookup"><span data-stu-id="ba8df-135">developer</span></span>

<span data-ttu-id="ba8df-136">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="ba8df-136">**Required** — object</span></span>

<span data-ttu-id="ba8df-137">Предоставляет сведения о вашей компании.</span><span class="sxs-lookup"><span data-stu-id="ba8df-137">Gives information about your company.</span></span> <span data-ttu-id="ba8df-138">Для приложений, представленных в AppSource (ранее Office Store), эти значения должны соответствовать сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="ba8df-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="ba8df-139">Дополнительные [сведения см. в](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) руководстве по публикации.</span><span class="sxs-lookup"><span data-stu-id="ba8df-139">See the [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="ba8df-140">Name</span><span class="sxs-lookup"><span data-stu-id="ba8df-140">Name</span></span>| <span data-ttu-id="ba8df-141">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-141">Maximum size</span></span> | <span data-ttu-id="ba8df-142">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-142">Required</span></span> | <span data-ttu-id="ba8df-143">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="ba8df-144">32 символа</span><span class="sxs-lookup"><span data-stu-id="ba8df-144">32 characters</span></span>|<span data-ttu-id="ba8df-145">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-145">✔</span></span>|<span data-ttu-id="ba8df-146">Имя отображения для разработчика.</span><span class="sxs-lookup"><span data-stu-id="ba8df-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="ba8df-147">2048 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-147">2048 characters</span></span>|<span data-ttu-id="ba8df-148">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-148">✔</span></span>|<span data-ttu-id="ba8df-149">Url https:// url-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="ba8df-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="ba8df-150">Эта ссылка должна принимать пользователей на страницу вашей компании или конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="ba8df-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="ba8df-151">2048 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-151">2048 characters</span></span>|<span data-ttu-id="ba8df-152">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-152">✔</span></span>|<span data-ttu-id="ba8df-153">Url https:// url-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="ba8df-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="ba8df-154">2048 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-154">2048 characters</span></span>|<span data-ttu-id="ba8df-155">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-155">✔</span></span>|<span data-ttu-id="ba8df-156">Url https:// url-адрес для условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="ba8df-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="ba8df-157">10 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-157">10 characters</span></span>| |<span data-ttu-id="ba8df-158">**Необязательный** Идентификатор Сети партнеров Майкрософт, который определяет организацию-партнер, которая строит приложение.</span><span class="sxs-lookup"><span data-stu-id="ba8df-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="ba8df-159">name</span><span class="sxs-lookup"><span data-stu-id="ba8df-159">name</span></span>

<span data-ttu-id="ba8df-160">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="ba8df-160">**Required** — object</span></span>

<span data-ttu-id="ba8df-161">Имя приложения, отображаемого пользователям в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="ba8df-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="ba8df-162">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="ba8df-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="ba8df-163">Значения и `short` должны `full` быть разными.</span><span class="sxs-lookup"><span data-stu-id="ba8df-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="ba8df-164">Name</span><span class="sxs-lookup"><span data-stu-id="ba8df-164">Name</span></span>| <span data-ttu-id="ba8df-165">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-165">Maximum size</span></span> | <span data-ttu-id="ba8df-166">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-166">Required</span></span> | <span data-ttu-id="ba8df-167">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="ba8df-168">30 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-168">30 characters</span></span>|<span data-ttu-id="ba8df-169">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-169">✔</span></span>|<span data-ttu-id="ba8df-170">Короткое имя отображения приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="ba8df-171">100 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-171">100 characters</span></span>||<span data-ttu-id="ba8df-172">Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="ba8df-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="ba8df-173">description</span><span class="sxs-lookup"><span data-stu-id="ba8df-173">description</span></span>

<span data-ttu-id="ba8df-174">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="ba8df-174">**Required** — object</span></span>

<span data-ttu-id="ba8df-175">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="ba8df-175">Describes your app to users.</span></span> <span data-ttu-id="ba8df-176">Для приложений, представленных в AppSource, эти значения должны соответствовать сведениям, указанным в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="ba8df-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="ba8df-177">Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, чтобы помочь потенциальным клиентам понять, что делает ваш опыт.</span><span class="sxs-lookup"><span data-stu-id="ba8df-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="ba8df-178">В полном описании необходимо учтите, что для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="ba8df-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="ba8df-179">Значения и `short` должны `full` быть разными.</span><span class="sxs-lookup"><span data-stu-id="ba8df-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="ba8df-180">Короткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="ba8df-181">Name</span><span class="sxs-lookup"><span data-stu-id="ba8df-181">Name</span></span>| <span data-ttu-id="ba8df-182">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-182">Maximum size</span></span> | <span data-ttu-id="ba8df-183">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-183">Required</span></span> | <span data-ttu-id="ba8df-184">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="ba8df-185">80 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-185">80 characters</span></span>|<span data-ttu-id="ba8df-186">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-186">✔</span></span>|<span data-ttu-id="ba8df-187">Краткое описание работы приложения, используемого при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="ba8df-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="ba8df-188">4000 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-188">4000 characters</span></span>|<span data-ttu-id="ba8df-189">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-189">✔</span></span>|<span data-ttu-id="ba8df-190">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="ba8df-191">packageName</span><span class="sxs-lookup"><span data-stu-id="ba8df-191">packageName</span></span>

<span data-ttu-id="ba8df-192">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="ba8df-192">**Optional** — string</span></span>

<span data-ttu-id="ba8df-193">Уникальный идентификатор для приложения в обратной нотации домена; например, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="ba8df-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="ba8df-194">Максимальная длина: 64 символа.</span><span class="sxs-lookup"><span data-stu-id="ba8df-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="ba8df-195">локализацияInfo</span><span class="sxs-lookup"><span data-stu-id="ba8df-195">localizationInfo</span></span>

<span data-ttu-id="ba8df-196">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="ba8df-196">**Optional** — object</span></span>

<span data-ttu-id="ba8df-197">Позволяет спецификацию языка по умолчанию, а также указатели для дополнительных языковых файлов.</span><span class="sxs-lookup"><span data-stu-id="ba8df-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="ba8df-198">См. [локализацию.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="ba8df-198">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="ba8df-199">Name</span><span class="sxs-lookup"><span data-stu-id="ba8df-199">Name</span></span>| <span data-ttu-id="ba8df-200">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-200">Maximum size</span></span> | <span data-ttu-id="ba8df-201">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-201">Required</span></span> | <span data-ttu-id="ba8df-202">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="ba8df-203">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-203">✔</span></span>|<span data-ttu-id="ba8df-204">Языковой тег строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="ba8df-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="ba8df-205">локализацияInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="ba8df-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="ba8df-206">Массив объектов, указывающих дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="ba8df-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="ba8df-207">Name</span><span class="sxs-lookup"><span data-stu-id="ba8df-207">Name</span></span>| <span data-ttu-id="ba8df-208">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-208">Maximum size</span></span> | <span data-ttu-id="ba8df-209">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-209">Required</span></span> | <span data-ttu-id="ba8df-210">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="ba8df-211">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-211">✔</span></span>|<span data-ttu-id="ba8df-212">Языковой тег строки в предоставленного файла.</span><span class="sxs-lookup"><span data-stu-id="ba8df-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="ba8df-213">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-213">✔</span></span>|<span data-ttu-id="ba8df-214">Относительный путь к файлу .json, содержащим переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="ba8df-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="ba8df-215">icons</span><span class="sxs-lookup"><span data-stu-id="ba8df-215">icons</span></span>

<span data-ttu-id="ba8df-216">**Обязательно —** объект</span><span class="sxs-lookup"><span data-stu-id="ba8df-216">**Required** — object</span></span>

<span data-ttu-id="ba8df-217">Значки, используемые в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="ba8df-217">Icons used within the Teams app.</span></span> <span data-ttu-id="ba8df-218">Файлы значков должны быть включены в пакет отправки.</span><span class="sxs-lookup"><span data-stu-id="ba8df-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="ba8df-219">Дополнительные сведения см. в [значках.](../../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="ba8df-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="ba8df-220">Name</span><span class="sxs-lookup"><span data-stu-id="ba8df-220">Name</span></span>| <span data-ttu-id="ba8df-221">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-221">Maximum size</span></span> | <span data-ttu-id="ba8df-222">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-222">Required</span></span> | <span data-ttu-id="ba8df-223">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="ba8df-224">32 x 32 пикселя</span><span class="sxs-lookup"><span data-stu-id="ba8df-224">32 x 32 pixels</span></span>|<span data-ttu-id="ba8df-225">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-225">✔</span></span>|<span data-ttu-id="ba8df-226">Относительный путь к прозрачному значку контура PNG 32x32.</span><span class="sxs-lookup"><span data-stu-id="ba8df-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="ba8df-227">192 x 192 пикселя</span><span class="sxs-lookup"><span data-stu-id="ba8df-227">192 x 192 pixels</span></span>|<span data-ttu-id="ba8df-228">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-228">✔</span></span>|<span data-ttu-id="ba8df-229">Относительный путь к значку PNG полного цвета 192x192.</span><span class="sxs-lookup"><span data-stu-id="ba8df-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="ba8df-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="ba8df-230">accentColor</span></span>

<span data-ttu-id="ba8df-231">**Необязательный** — цветовой код HTML Hex</span><span class="sxs-lookup"><span data-stu-id="ba8df-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="ba8df-232">Цвет, который можно использовать в сочетании с и в качестве фона для значков контура.</span><span class="sxs-lookup"><span data-stu-id="ba8df-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="ba8df-233">Значение должно быть допустимым цветовым кодом HTML, начиная, например, с `#4464ee` "#".</span><span class="sxs-lookup"><span data-stu-id="ba8df-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="ba8df-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="ba8df-234">configurableTabs</span></span>

<span data-ttu-id="ba8df-235">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="ba8df-235">**Optional** — array</span></span>

<span data-ttu-id="ba8df-236">Используется, когда в вашем приложении есть опыт работы с вкладками канала команды, которая требует дополнительной конфигурации перед ее добавлением.</span><span class="sxs-lookup"><span data-stu-id="ba8df-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="ba8df-237">Настраиваемые вкладки поддерживаются только в области команд (не личной), и в настоящее время поддерживается только одна вкладка для каждого приложения. </span><span class="sxs-lookup"><span data-stu-id="ba8df-237">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="ba8df-238">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-238">Name</span></span>| <span data-ttu-id="ba8df-239">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-239">Type</span></span>| <span data-ttu-id="ba8df-240">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-240">Maximum size</span></span> | <span data-ttu-id="ba8df-241">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-241">Required</span></span> | <span data-ttu-id="ba8df-242">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-242">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="ba8df-243">string</span><span class="sxs-lookup"><span data-stu-id="ba8df-243">string</span></span>|<span data-ttu-id="ba8df-244">2048 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-244">2048 characters</span></span>|<span data-ttu-id="ba8df-245">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-245">✔</span></span>|<span data-ttu-id="ba8df-246">URL-https://, который можно использовать при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="ba8df-246">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="ba8df-247">массив enums</span><span class="sxs-lookup"><span data-stu-id="ba8df-247">array of enums</span></span>|<span data-ttu-id="ba8df-248">1</span><span class="sxs-lookup"><span data-stu-id="ba8df-248">1</span></span>|<span data-ttu-id="ba8df-249">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-249">✔</span></span>|<span data-ttu-id="ba8df-250">В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области.</span><span class="sxs-lookup"><span data-stu-id="ba8df-250">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="ba8df-251">boolean</span><span class="sxs-lookup"><span data-stu-id="ba8df-251">boolean</span></span>|||<span data-ttu-id="ba8df-252">Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания.</span><span class="sxs-lookup"><span data-stu-id="ba8df-252">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="ba8df-253">По умолчанию: **true**.</span><span class="sxs-lookup"><span data-stu-id="ba8df-253">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="ba8df-254">массив enums</span><span class="sxs-lookup"><span data-stu-id="ba8df-254">array of enums</span></span>|<span data-ttu-id="ba8df-255">6 </span><span class="sxs-lookup"><span data-stu-id="ba8df-255">6</span></span>||<span data-ttu-id="ba8df-256">Набор `contextItem` областей, в которых поддерживается вкладка.</span><span class="sxs-lookup"><span data-stu-id="ba8df-256">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="ba8df-257">По умолчанию: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="ba8df-257">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="ba8df-258">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-258">string</span></span>|<span data-ttu-id="ba8df-259">2048</span><span class="sxs-lookup"><span data-stu-id="ba8df-259">2048</span></span>||<span data-ttu-id="ba8df-260">Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ba8df-260">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="ba8df-261">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="ba8df-261">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="ba8df-262">массив enums</span><span class="sxs-lookup"><span data-stu-id="ba8df-262">array of enums</span></span>|<span data-ttu-id="ba8df-263">1</span><span class="sxs-lookup"><span data-stu-id="ba8df-263">1</span></span>||<span data-ttu-id="ba8df-264">Определяет, как вкладка доступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ba8df-264">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="ba8df-265">Параметры `sharePointFullPage` и `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="ba8df-265">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="ba8df-266">staticTabs</span><span class="sxs-lookup"><span data-stu-id="ba8df-266">staticTabs</span></span>

<span data-ttu-id="ba8df-267">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="ba8df-267">**Optional** — array</span></span>

<span data-ttu-id="ba8df-268">Определяет набор вкладок, которые можно "прикрепить" по умолчанию, не добавляя их вручную.</span><span class="sxs-lookup"><span data-stu-id="ba8df-268">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="ba8df-269">Статические вкладки, объявленные в области, всегда прикрепяются к личному опыту `personal` приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-269">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="ba8df-270">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="ba8df-270">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="ba8df-271">Этот элемент — массив (не более 16 элементов) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="ba8df-271">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="ba8df-272">Этот блок требуется только для решений, которые предоставляют статическое решение вкладки.</span><span class="sxs-lookup"><span data-stu-id="ba8df-272">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="ba8df-273">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-273">Name</span></span>| <span data-ttu-id="ba8df-274">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-274">Type</span></span>| <span data-ttu-id="ba8df-275">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-275">Maximum size</span></span> | <span data-ttu-id="ba8df-276">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-276">Required</span></span> | <span data-ttu-id="ba8df-277">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-277">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="ba8df-278">string</span><span class="sxs-lookup"><span data-stu-id="ba8df-278">string</span></span>|<span data-ttu-id="ba8df-279">64 символа</span><span class="sxs-lookup"><span data-stu-id="ba8df-279">64 characters</span></span>|<span data-ttu-id="ba8df-280">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-280">✔</span></span>|<span data-ttu-id="ba8df-281">Уникальный идентификатор для объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="ba8df-281">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="ba8df-282">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-282">string</span></span>|<span data-ttu-id="ba8df-283">128 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-283">128 characters</span></span>|<span data-ttu-id="ba8df-284">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-284">✔</span></span>|<span data-ttu-id="ba8df-285">Отображение имени вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="ba8df-285">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="ba8df-286">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-286">string</span></span>||<span data-ttu-id="ba8df-287">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-287">✔</span></span>|<span data-ttu-id="ba8df-288">URL https://, который указывает на пользовательский интерфейс объекта, отображаемого на холсте Teams.</span><span class="sxs-lookup"><span data-stu-id="ba8df-288">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="ba8df-289">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-289">string</span></span>|||<span data-ttu-id="ba8df-290">Url https://, чтобы указать, выбирает ли пользователь просмотр в браузере.</span><span class="sxs-lookup"><span data-stu-id="ba8df-290">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="ba8df-291">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-291">string</span></span>|||<span data-ttu-id="ba8df-292">Url https://, на который нужно указать для поисковых запросов пользователя.</span><span class="sxs-lookup"><span data-stu-id="ba8df-292">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="ba8df-293">массив enums</span><span class="sxs-lookup"><span data-stu-id="ba8df-293">array of enums</span></span>|<span data-ttu-id="ba8df-294">1</span><span class="sxs-lookup"><span data-stu-id="ba8df-294">1</span></span>|<span data-ttu-id="ba8df-295">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-295">✔</span></span>|<span data-ttu-id="ba8df-296">В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в `personal` рамках личного опыта.</span><span class="sxs-lookup"><span data-stu-id="ba8df-296">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="ba8df-297">массив enums</span><span class="sxs-lookup"><span data-stu-id="ba8df-297">array of enums</span></span>| <span data-ttu-id="ba8df-298">2</span><span class="sxs-lookup"><span data-stu-id="ba8df-298">2</span></span>|| <span data-ttu-id="ba8df-299">Набор `contextItem` областей, в которых поддерживается вкладка.</span><span class="sxs-lookup"><span data-stu-id="ba8df-299">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="ba8df-300">Если для отображения соответствующего контента или инициации потока проверки подлинности на вкладке Microsoft Teams требуются сведения, зависящие от  [контекста,](../../tabs/how-to/access-teams-context.md)см. в статье Get context for your Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ba8df-300">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="ba8df-301">боты</span><span class="sxs-lookup"><span data-stu-id="ba8df-301">bots</span></span>

<span data-ttu-id="ba8df-302">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="ba8df-302">**Optional** — array</span></span>

<span data-ttu-id="ba8df-303">Определяет решение бота, а также необязательные сведения, такие как свойства команд по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ba8df-303">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="ba8df-304">Элемент — массив (максимум 1 элемент в настоящее время разрешен только для одного бота в приложении) со всеми элементами &mdash; типа `object` .</span><span class="sxs-lookup"><span data-stu-id="ba8df-304">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="ba8df-305">Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.</span><span class="sxs-lookup"><span data-stu-id="ba8df-305">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="ba8df-306">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-306">Name</span></span>| <span data-ttu-id="ba8df-307">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-307">Type</span></span>| <span data-ttu-id="ba8df-308">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-308">Maximum size</span></span> | <span data-ttu-id="ba8df-309">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-309">Required</span></span> | <span data-ttu-id="ba8df-310">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-310">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="ba8df-311">string</span><span class="sxs-lookup"><span data-stu-id="ba8df-311">string</span></span>|<span data-ttu-id="ba8df-312">64 символа</span><span class="sxs-lookup"><span data-stu-id="ba8df-312">64 characters</span></span>|<span data-ttu-id="ba8df-313">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-313">✔</span></span>|<span data-ttu-id="ba8df-314">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="ba8df-314">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="ba8df-315">Это вполне может быть таким же, как общий [ID приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="ba8df-315">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="ba8df-316">массив enums</span><span class="sxs-lookup"><span data-stu-id="ba8df-316">array of enums</span></span>|<span data-ttu-id="ba8df-317">3</span><span class="sxs-lookup"><span data-stu-id="ba8df-317">3</span></span>|<span data-ttu-id="ba8df-318">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-318">✔</span></span>|<span data-ttu-id="ba8df-319">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="ba8df-319">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="ba8df-320">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="ba8df-320">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="ba8df-321">boolean</span><span class="sxs-lookup"><span data-stu-id="ba8df-321">boolean</span></span>|||<span data-ttu-id="ba8df-322">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="ba8df-322">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="ba8df-323">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="ba8df-323">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="ba8df-324">boolean</span><span class="sxs-lookup"><span data-stu-id="ba8df-324">boolean</span></span>|||<span data-ttu-id="ba8df-325">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="ba8df-325">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="ba8df-326">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="ba8df-326">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="ba8df-327">boolean</span><span class="sxs-lookup"><span data-stu-id="ba8df-327">boolean</span></span>|||<span data-ttu-id="ba8df-328">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="ba8df-328">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="ba8df-329">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="ba8df-329">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="ba8df-330">boolean</span><span class="sxs-lookup"><span data-stu-id="ba8df-330">boolean</span></span>|||<span data-ttu-id="ba8df-331">Значение, указывающее, где бот поддерживает звуковые вызовы.</span><span class="sxs-lookup"><span data-stu-id="ba8df-331">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="ba8df-332">**ВАЖНО.** Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="ba8df-332">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="ba8df-333">Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="ba8df-333">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="ba8df-334">Она предоставляется только для тестирования и разведки и не должна использоваться в производственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="ba8df-334">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="ba8df-335">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="ba8df-335">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="ba8df-336">boolean</span><span class="sxs-lookup"><span data-stu-id="ba8df-336">boolean</span></span>|||<span data-ttu-id="ba8df-337">Значение, указывающее, где бот поддерживает видеозвонков.</span><span class="sxs-lookup"><span data-stu-id="ba8df-337">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="ba8df-338">**ВАЖНО.** Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="ba8df-338">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="ba8df-339">Экспериментальные свойства могут быть не завершены и могут претерпеть изменения, прежде чем стать полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="ba8df-339">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="ba8df-340">Она предоставляется только для тестирования и разведки и не должна использоваться в производственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="ba8df-340">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="ba8df-341">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="ba8df-341">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="ba8df-342">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="ba8df-342">bots.commandLists</span></span>

<span data-ttu-id="ba8df-343">Необязательный список команд, которые бот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="ba8df-343">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="ba8df-344">Объект — массив (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом.</span><span class="sxs-lookup"><span data-stu-id="ba8df-344">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="ba8df-345">Дополнительные [сведения см. в](~/bots/how-to/create-a-bot-commands-menu.md) меню Bot.</span><span class="sxs-lookup"><span data-stu-id="ba8df-345">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="ba8df-346">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-346">Name</span></span>| <span data-ttu-id="ba8df-347">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-347">Type</span></span>| <span data-ttu-id="ba8df-348">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-348">Maximum size</span></span> | <span data-ttu-id="ba8df-349">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-349">Required</span></span> | <span data-ttu-id="ba8df-350">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-350">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="ba8df-351">массив enums</span><span class="sxs-lookup"><span data-stu-id="ba8df-351">array of enums</span></span>|<span data-ttu-id="ba8df-352">3</span><span class="sxs-lookup"><span data-stu-id="ba8df-352">3</span></span>|<span data-ttu-id="ba8df-353">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-353">✔</span></span>|<span data-ttu-id="ba8df-354">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="ba8df-354">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="ba8df-355">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="ba8df-355">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="ba8df-356">массив объектов</span><span class="sxs-lookup"><span data-stu-id="ba8df-356">array of objects</span></span>|<span data-ttu-id="ba8df-357">10 </span><span class="sxs-lookup"><span data-stu-id="ba8df-357">10</span></span>|<span data-ttu-id="ba8df-358">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-358">✔</span></span>|<span data-ttu-id="ba8df-359">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="ba8df-359">An array of commands the bot supports:</span></span><br><span data-ttu-id="ba8df-360">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="ba8df-360">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="ba8df-361">`description`: простое описание или пример синтаксиса команды и ее аргумента (строка, 128)</span><span class="sxs-lookup"><span data-stu-id="ba8df-361">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="ba8df-362">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="ba8df-362">bots.commandLists.commands</span></span>

|<span data-ttu-id="ba8df-363">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-363">Name</span></span>| <span data-ttu-id="ba8df-364">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-364">Type</span></span>| <span data-ttu-id="ba8df-365">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-365">Maximum size</span></span> | <span data-ttu-id="ba8df-366">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-366">Required</span></span> | <span data-ttu-id="ba8df-367">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-367">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="ba8df-368">title</span><span class="sxs-lookup"><span data-stu-id="ba8df-368">title</span></span>|<span data-ttu-id="ba8df-369">string</span><span class="sxs-lookup"><span data-stu-id="ba8df-369">string</span></span>|<span data-ttu-id="ba8df-370">12 </span><span class="sxs-lookup"><span data-stu-id="ba8df-370">12</span></span>|<span data-ttu-id="ba8df-371">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-371">✔</span></span>|<span data-ttu-id="ba8df-372">Имя команды бота</span><span class="sxs-lookup"><span data-stu-id="ba8df-372">The bot command name</span></span>|
|<span data-ttu-id="ba8df-373">description</span><span class="sxs-lookup"><span data-stu-id="ba8df-373">description</span></span>|<span data-ttu-id="ba8df-374">string</span><span class="sxs-lookup"><span data-stu-id="ba8df-374">string</span></span>|<span data-ttu-id="ba8df-375">128 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-375">128 characters</span></span>|<span data-ttu-id="ba8df-376">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-376">✔</span></span>|<span data-ttu-id="ba8df-377">Простое текстовое описание или пример синтаксиса команд и его аргументов.</span><span class="sxs-lookup"><span data-stu-id="ba8df-377">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="ba8df-378">соединители</span><span class="sxs-lookup"><span data-stu-id="ba8df-378">connectors</span></span>

<span data-ttu-id="ba8df-379">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="ba8df-379">**Optional** — array</span></span>

<span data-ttu-id="ba8df-380">Блок `connectors` определяет соединители Office 365 для приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-380">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="ba8df-381">Объект — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="ba8df-381">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="ba8df-382">Этот блок необходим только для решений, которые предоставляют соединители.</span><span class="sxs-lookup"><span data-stu-id="ba8df-382">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="ba8df-383">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-383">Name</span></span>| <span data-ttu-id="ba8df-384">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-384">Type</span></span>| <span data-ttu-id="ba8df-385">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-385">Maximum size</span></span> | <span data-ttu-id="ba8df-386">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-386">Required</span></span> | <span data-ttu-id="ba8df-387">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-387">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="ba8df-388">string</span><span class="sxs-lookup"><span data-stu-id="ba8df-388">string</span></span>|<span data-ttu-id="ba8df-389">2048 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-389">2048 characters</span></span>|<span data-ttu-id="ba8df-390">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-390">✔</span></span>|<span data-ttu-id="ba8df-391">URL https://, который необходимо использовать при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="ba8df-391">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="ba8df-392">массив enums</span><span class="sxs-lookup"><span data-stu-id="ba8df-392">array of enums</span></span>|<span data-ttu-id="ba8df-393">1</span><span class="sxs-lookup"><span data-stu-id="ba8df-393">1</span></span>|<span data-ttu-id="ba8df-394">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-394">✔</span></span>|<span data-ttu-id="ba8df-395">Указывает, предоставляет ли соединители опыт в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="ba8df-395">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="ba8df-396">В настоящее время `team` поддерживается только область.</span><span class="sxs-lookup"><span data-stu-id="ba8df-396">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="ba8df-397">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-397">string</span></span>|<span data-ttu-id="ba8df-398">64 символа</span><span class="sxs-lookup"><span data-stu-id="ba8df-398">64 characters</span></span>|<span data-ttu-id="ba8df-399">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-399">✔</span></span>|<span data-ttu-id="ba8df-400">Уникальный идентификатор соединитетеля, который соответствует его идентификатору в панели мониторинга разработчиков [соединителок.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="ba8df-400">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="ba8df-401">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="ba8df-401">composeExtensions</span></span>

<span data-ttu-id="ba8df-402">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="ba8df-402">**Optional** — array</span></span>

<span data-ttu-id="ba8df-403">Определяет расширение обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-403">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="ba8df-404">В ноябре 2017 г. имя функции было изменено с "расширение составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжили функционировать.</span><span class="sxs-lookup"><span data-stu-id="ba8df-404">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="ba8df-405">Элемент — массив (максимум 1 элемент) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="ba8df-405">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="ba8df-406">Этот блок необходим только для решений, которые предоставляют расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="ba8df-406">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="ba8df-407">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-407">Name</span></span>| <span data-ttu-id="ba8df-408">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-408">Type</span></span> | <span data-ttu-id="ba8df-409">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-409">Maximum Size</span></span> | <span data-ttu-id="ba8df-410">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-410">Required</span></span> | <span data-ttu-id="ba8df-411">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-411">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="ba8df-412">string</span><span class="sxs-lookup"><span data-stu-id="ba8df-412">string</span></span>|<span data-ttu-id="ba8df-413">64</span><span class="sxs-lookup"><span data-stu-id="ba8df-413">64</span></span>|<span data-ttu-id="ba8df-414">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-414">✔</span></span>|<span data-ttu-id="ba8df-415">Уникальный ID приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрирован в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="ba8df-415">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="ba8df-416">Это вполне может быть таким же, как и общий ID приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-416">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="ba8df-417">массив объектов</span><span class="sxs-lookup"><span data-stu-id="ba8df-417">array of objects</span></span>|<span data-ttu-id="ba8df-418">10 </span><span class="sxs-lookup"><span data-stu-id="ba8df-418">10</span></span>|<span data-ttu-id="ba8df-419">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-419">✔</span></span>|<span data-ttu-id="ba8df-420">Массив команд, поддерживаемых расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="ba8df-420">Array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="ba8df-421">boolean</span><span class="sxs-lookup"><span data-stu-id="ba8df-421">boolean</span></span>|||<span data-ttu-id="ba8df-422">Значение, указывающее, может ли пользователь обновить конфигурацию расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="ba8df-422">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="ba8df-423">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="ba8df-423">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="ba8df-424">массив объектов</span><span class="sxs-lookup"><span data-stu-id="ba8df-424">array of Objects</span></span>|<span data-ttu-id="ba8df-425">5 </span><span class="sxs-lookup"><span data-stu-id="ba8df-425">5</span></span>||<span data-ttu-id="ba8df-426">Список обработчиков, которые позволяют вызывать приложения при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="ba8df-426">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="ba8df-427">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-427">string</span></span>|||<span data-ttu-id="ba8df-428">Тип обработка сообщений.</span><span class="sxs-lookup"><span data-stu-id="ba8df-428">The type of message handler.</span></span> <span data-ttu-id="ba8df-429">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="ba8df-429">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="ba8df-430">массив строк</span><span class="sxs-lookup"><span data-stu-id="ba8df-430">array of Strings</span></span>|||<span data-ttu-id="ba8df-431">Массив доменов, для которые обработник сообщений ссылок может зарегистрироваться.</span><span class="sxs-lookup"><span data-stu-id="ba8df-431">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="ba8df-432">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="ba8df-432">composeExtensions.commands</span></span>

<span data-ttu-id="ba8df-433">Расширение обмена сообщениями должно объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="ba8df-433">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="ba8df-434">Каждая команда отображается в Microsoft Teams в качестве потенциального взаимодействия с точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="ba8df-434">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="ba8df-435">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="ba8df-435">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="ba8df-436">Каждый элемент команды — это объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="ba8df-436">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="ba8df-437">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-437">Name</span></span>| <span data-ttu-id="ba8df-438">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-438">Type</span></span>| <span data-ttu-id="ba8df-439">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-439">Maximum size</span></span> | <span data-ttu-id="ba8df-440">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-440">Required</span></span> | <span data-ttu-id="ba8df-441">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-441">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="ba8df-442">string</span><span class="sxs-lookup"><span data-stu-id="ba8df-442">string</span></span>|<span data-ttu-id="ba8df-443">64 символа</span><span class="sxs-lookup"><span data-stu-id="ba8df-443">64 characters</span></span>|<span data-ttu-id="ba8df-444">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-444">✔</span></span>|<span data-ttu-id="ba8df-445">ID для команды.</span><span class="sxs-lookup"><span data-stu-id="ba8df-445">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="ba8df-446">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-446">string</span></span>|<span data-ttu-id="ba8df-447">32 символа</span><span class="sxs-lookup"><span data-stu-id="ba8df-447">32 characters</span></span>|<span data-ttu-id="ba8df-448">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-448">✔</span></span>|<span data-ttu-id="ba8df-449">Удобное имя команды.</span><span class="sxs-lookup"><span data-stu-id="ba8df-449">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="ba8df-450">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-450">string</span></span>|<span data-ttu-id="ba8df-451">64 символа</span><span class="sxs-lookup"><span data-stu-id="ba8df-451">64 characters</span></span>||<span data-ttu-id="ba8df-452">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="ba8df-452">Type of the command.</span></span> <span data-ttu-id="ba8df-453">Один `query` из или `action` .</span><span class="sxs-lookup"><span data-stu-id="ba8df-453">One of `query` or `action`.</span></span> <span data-ttu-id="ba8df-454">По умолчанию: **запрос**.</span><span class="sxs-lookup"><span data-stu-id="ba8df-454">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="ba8df-455">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-455">string</span></span>|<span data-ttu-id="ba8df-456">128 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-456">128 characters</span></span>||<span data-ttu-id="ba8df-457">В описании, которое отображается пользователями, указывается назначение этой команды.</span><span class="sxs-lookup"><span data-stu-id="ba8df-457">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="ba8df-458">boolean</span><span class="sxs-lookup"><span data-stu-id="ba8df-458">boolean</span></span>|||<span data-ttu-id="ba8df-459">Значение boolean указывает, выполняется ли команда изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="ba8df-459">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="ba8df-460">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="ba8df-460">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="ba8df-461">массив строк</span><span class="sxs-lookup"><span data-stu-id="ba8df-461">array of Strings</span></span>|<span data-ttu-id="ba8df-462">3</span><span class="sxs-lookup"><span data-stu-id="ba8df-462">3</span></span>||<span data-ttu-id="ba8df-463">Определяет, из чего можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-463">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="ba8df-464">Любое сочетание `compose` `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="ba8df-464">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="ba8df-465">Значение по умолчанию: `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="ba8df-465">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="ba8df-466">boolean</span><span class="sxs-lookup"><span data-stu-id="ba8df-466">boolean</span></span>|||<span data-ttu-id="ba8df-467">Значение boolean, которое указывает, должен ли он динамически получать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="ba8df-467">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="ba8df-468">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="ba8df-468">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="ba8df-469">объект</span><span class="sxs-lookup"><span data-stu-id="ba8df-469">object</span></span>|||<span data-ttu-id="ba8df-470">Укажите модуль задач для предварительной загрузки при использовании команды расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="ba8df-470">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="ba8df-471">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-471">string</span></span>|<span data-ttu-id="ba8df-472">64 символа</span><span class="sxs-lookup"><span data-stu-id="ba8df-472">64 characters</span></span>||<span data-ttu-id="ba8df-473">Начальное название диалогов.</span><span class="sxs-lookup"><span data-stu-id="ba8df-473">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="ba8df-474">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-474">string</span></span>|||<span data-ttu-id="ba8df-475">Ширина диалогов — число в пикселях или макет по умолчанию, такие как "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="ba8df-475">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="ba8df-476">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-476">string</span></span>|||<span data-ttu-id="ba8df-477">Высота диалогов — число пикселей или макет по умолчанию, например "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="ba8df-477">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="ba8df-478">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-478">string</span></span>|||<span data-ttu-id="ba8df-479">Начальный URL-адрес веб-просмотров.</span><span class="sxs-lookup"><span data-stu-id="ba8df-479">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="ba8df-480">массив объекта</span><span class="sxs-lookup"><span data-stu-id="ba8df-480">array of object</span></span>|<span data-ttu-id="ba8df-481">5 элементов</span><span class="sxs-lookup"><span data-stu-id="ba8df-481">5 items</span></span>|<span data-ttu-id="ba8df-482">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-482">✔</span></span>|<span data-ttu-id="ba8df-483">Список параметров, которые принимает команда.</span><span class="sxs-lookup"><span data-stu-id="ba8df-483">The list of parameters the command takes.</span></span> <span data-ttu-id="ba8df-484">Минимум: 1; максимум: 5.</span><span class="sxs-lookup"><span data-stu-id="ba8df-484">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="ba8df-485">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-485">string</span></span>|<span data-ttu-id="ba8df-486">64 символа</span><span class="sxs-lookup"><span data-stu-id="ba8df-486">64 characters</span></span>|<span data-ttu-id="ba8df-487">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-487">✔</span></span>|<span data-ttu-id="ba8df-488">Имя параметра, как оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="ba8df-488">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="ba8df-489">Это включено в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="ba8df-489">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="ba8df-490">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-490">string</span></span>|<span data-ttu-id="ba8df-491">32 символа</span><span class="sxs-lookup"><span data-stu-id="ba8df-491">32 characters</span></span>|<span data-ttu-id="ba8df-492">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-492">✔</span></span>|<span data-ttu-id="ba8df-493">Удобное название для параметра.</span><span class="sxs-lookup"><span data-stu-id="ba8df-493">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="ba8df-494">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-494">string</span></span>|<span data-ttu-id="ba8df-495">128 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-495">128 characters</span></span>||<span data-ttu-id="ba8df-496">Удобное для пользователя строка, описываемая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="ba8df-496">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="ba8df-497">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-497">string</span></span>|<span data-ttu-id="ba8df-498">512 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-498">512 characters</span></span>||<span data-ttu-id="ba8df-499">Начальное значение для параметра.</span><span class="sxs-lookup"><span data-stu-id="ba8df-499">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="ba8df-500">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-500">string</span></span>|<span data-ttu-id="ba8df-501">128 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-501">128 characters</span></span>||<span data-ttu-id="ba8df-502">Определяет тип управления, отображаемого в модуле задач `fetchTask: true` для .</span><span class="sxs-lookup"><span data-stu-id="ba8df-502">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="ba8df-503">Один из `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="ba8df-503">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="ba8df-504">массив объектов</span><span class="sxs-lookup"><span data-stu-id="ba8df-504">array of objects</span></span>|<span data-ttu-id="ba8df-505">10 элементов</span><span class="sxs-lookup"><span data-stu-id="ba8df-505">10 items</span></span>||<span data-ttu-id="ba8df-506">Параметры выбора `choiceset` для .</span><span class="sxs-lookup"><span data-stu-id="ba8df-506">The choice options for the`choiceset`.</span></span> <span data-ttu-id="ba8df-507">Используйте только `parameter.inputType` тогда, когда `choiceset` это .</span><span class="sxs-lookup"><span data-stu-id="ba8df-507">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="ba8df-508">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-508">string</span></span>|<span data-ttu-id="ba8df-509">128 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-509">128 characters</span></span>|<span data-ttu-id="ba8df-510">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-510">✔</span></span>|<span data-ttu-id="ba8df-511">Название выбора.</span><span class="sxs-lookup"><span data-stu-id="ba8df-511">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="ba8df-512">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-512">string</span></span>|<span data-ttu-id="ba8df-513">512 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-513">512 characters</span></span>|<span data-ttu-id="ba8df-514">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-514">✔</span></span>|<span data-ttu-id="ba8df-515">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="ba8df-515">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="ba8df-516">permissions</span><span class="sxs-lookup"><span data-stu-id="ba8df-516">permissions</span></span>

<span data-ttu-id="ba8df-517">**Необязательный** — массив строк</span><span class="sxs-lookup"><span data-stu-id="ba8df-517">**Optional** — array of strings</span></span>

<span data-ttu-id="ba8df-518">Массив, в котором указывается, какие разрешения запрашивает приложение, что позволяет конечным пользователям `string` знать, как выполняется расширение.</span><span class="sxs-lookup"><span data-stu-id="ba8df-518">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="ba8df-519">Следующие параметры не являются эксклюзивными:</span><span class="sxs-lookup"><span data-stu-id="ba8df-519">The following options are non-exclusive:</span></span>

* <span data-ttu-id="ba8df-520">`identity`&emsp;Требует сведений о удостоверениях пользователей</span><span class="sxs-lookup"><span data-stu-id="ba8df-520">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="ba8df-521">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений членам группы</span><span class="sxs-lookup"><span data-stu-id="ba8df-521">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="ba8df-522">Изменение этих разрешений во время обновления приложения заставляет пользователей повторять процесс согласия после запуска обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-522">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="ba8df-523">Дополнительные [сведения см. в обновлении](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-523">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="ba8df-524">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="ba8df-524">devicePermissions</span></span>

<span data-ttu-id="ba8df-525">**Необязательный** — массив строк</span><span class="sxs-lookup"><span data-stu-id="ba8df-525">**Optional** — array of strings</span></span>

<span data-ttu-id="ba8df-526">Предоставляет родных функций на устройстве пользователя, к которое ваше приложение запрашивает доступ.</span><span class="sxs-lookup"><span data-stu-id="ba8df-526">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="ba8df-527">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="ba8df-527">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="ba8df-528">validDomains</span><span class="sxs-lookup"><span data-stu-id="ba8df-528">validDomains</span></span>

<span data-ttu-id="ba8df-529">**Необязательный,** за **исключением обязательного,** где отмечено</span><span class="sxs-lookup"><span data-stu-id="ba8df-529">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="ba8df-530">Список допустимого домена для веб-сайтов, которые приложение ожидает загрузить в клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="ba8df-530">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="ba8df-531">Списки домена могут включать, например, поддиайки. `*.example.com`</span><span class="sxs-lookup"><span data-stu-id="ba8df-531">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="ba8df-532">Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="ba8df-532">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="ba8df-533">Если конфигурации вкладок или пользовательскому интерфейсу контента необходимо перейти к любому другому домену, кроме одного использования для конфигурации вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="ba8df-533">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="ba8df-534">Не обязательно **включать** в приложение домены поставщиков удостоверений, которые необходимо поддерживать.</span><span class="sxs-lookup"><span data-stu-id="ba8df-534">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="ba8df-535">Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить accounts.google.com, однако не следует включать accounts.google.com `validDomains[]` в .</span><span class="sxs-lookup"><span data-stu-id="ba8df-535">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="ba8df-536">Команды приложений, которые требуют, чтобы их собственные URL-адреса sharepoint функционировали хорошо, включает "{teamsitedomain}" в допустимый список доменов.</span><span class="sxs-lookup"><span data-stu-id="ba8df-536">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba8df-537">Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью подкрентов.</span><span class="sxs-lookup"><span data-stu-id="ba8df-537">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="ba8df-538">Например, `yourapp.onmicrosoft.com` допустимо, однако, `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="ba8df-538">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="ba8df-539">Объект — массив со всеми элементами `string` типа.</span><span class="sxs-lookup"><span data-stu-id="ba8df-539">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="ba8df-540">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="ba8df-540">webApplicationInfo</span></span>

<span data-ttu-id="ba8df-541">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="ba8df-541">**Optional** — object</span></span>

<span data-ttu-id="ba8df-542">Предопишите свои сведения о приложении Azure Active Directory (AAD) и Microsoft Graph, чтобы помочь пользователям легко войти в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="ba8df-542">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="ba8df-543">Если ваше приложение зарегистрировано в AAD, необходимо предоставить ID приложения, чтобы администраторы могли легко просмотреть разрешения и предоставить согласие в центре администрирования Teams.</span><span class="sxs-lookup"><span data-stu-id="ba8df-543">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="ba8df-544">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-544">Name</span></span>| <span data-ttu-id="ba8df-545">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-545">Type</span></span>| <span data-ttu-id="ba8df-546">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-546">Maximum size</span></span> | <span data-ttu-id="ba8df-547">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-547">Required</span></span> | <span data-ttu-id="ba8df-548">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-548">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="ba8df-549">string</span><span class="sxs-lookup"><span data-stu-id="ba8df-549">string</span></span>|<span data-ttu-id="ba8df-550">36 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-550">36 characters</span></span>|<span data-ttu-id="ba8df-551">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-551">✔</span></span>|<span data-ttu-id="ba8df-552">AAD-id приложения приложения.</span><span class="sxs-lookup"><span data-stu-id="ba8df-552">AAD application id of the app.</span></span> <span data-ttu-id="ba8df-553">Этот id должен быть GUID.</span><span class="sxs-lookup"><span data-stu-id="ba8df-553">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="ba8df-554">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-554">string</span></span>|<span data-ttu-id="ba8df-555">2048 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-555">2048 characters</span></span>|<span data-ttu-id="ba8df-556">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-556">✔</span></span>|<span data-ttu-id="ba8df-557">URL-адрес ресурса приложения для приобретения маркера auth для SSO.</span><span class="sxs-lookup"><span data-stu-id="ba8df-557">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="ba8df-558">**ПРИМЕЧАНИЕ:** Если вы не используете SSO, убедитесь, что вы вводите значение строки в этом поле в манифест приложения, например, чтобы избежать ответа https://notapplicable на ошибку.</span><span class="sxs-lookup"><span data-stu-id="ba8df-558">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="ba8df-559">массив строк</span><span class="sxs-lookup"><span data-stu-id="ba8df-559">array of strings</span></span>|<span data-ttu-id="ba8df-560">128 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-560">128 characters</span></span>||<span data-ttu-id="ba8df-561">Укажите [конкретное согласие конкретного ресурса.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="ba8df-561">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="ba8df-562">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="ba8df-562">showLoadingIndicator</span></span>

<span data-ttu-id="ba8df-563">**Необязательный** — boolean</span><span class="sxs-lookup"><span data-stu-id="ba8df-563">**Optional** — boolean</span></span>

<span data-ttu-id="ba8df-564">Указывает, следует ли показывать индикатор загрузки при загрузке приложения или вкладки.</span><span class="sxs-lookup"><span data-stu-id="ba8df-564">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="ba8df-565">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="ba8df-565">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="ba8df-566">Если в манифесте приложения выбрано как верное, чтобы правильно загрузить страницу, измените страницы контента вкладок и модулей задач, как описано в документе Показать документ индикатора `showLoadingIndicator` загрузки. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="ba8df-566">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="ba8df-567">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="ba8df-567">isFullScreen</span></span>

 <span data-ttu-id="ba8df-568">**Необязательный** — boolean</span><span class="sxs-lookup"><span data-stu-id="ba8df-568">**Optional** — boolean</span></span>

<span data-ttu-id="ba8df-569">Указать, где отрисовка личного приложения с панели заголовки вкладок или без нее.</span><span class="sxs-lookup"><span data-stu-id="ba8df-569">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="ba8df-570">Значение по умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="ba8df-570">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="ba8df-571">activities</span><span class="sxs-lookup"><span data-stu-id="ba8df-571">activities</span></span>

<span data-ttu-id="ba8df-572">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="ba8df-572">**Optional** — object</span></span>

<span data-ttu-id="ba8df-573">Определите свойства, которые приложение использует для публикации ленты действий пользователя.</span><span class="sxs-lookup"><span data-stu-id="ba8df-573">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="ba8df-574">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-574">Name</span></span>| <span data-ttu-id="ba8df-575">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-575">Type</span></span>| <span data-ttu-id="ba8df-576">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-576">Maximum size</span></span> | <span data-ttu-id="ba8df-577">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-577">Required</span></span> | <span data-ttu-id="ba8df-578">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-578">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="ba8df-579">массив объектов</span><span class="sxs-lookup"><span data-stu-id="ba8df-579">array of Objects</span></span>|<span data-ttu-id="ba8df-580">128 элементов</span><span class="sxs-lookup"><span data-stu-id="ba8df-580">128 items</span></span>| | <span data-ttu-id="ba8df-581">Укапитайте типы действий, которые ваше приложение может размещать в канале действий пользователей.</span><span class="sxs-lookup"><span data-stu-id="ba8df-581">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="ba8df-582">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="ba8df-582">activities.activityTypes</span></span>

|<span data-ttu-id="ba8df-583">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-583">Name</span></span>| <span data-ttu-id="ba8df-584">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-584">Type</span></span>| <span data-ttu-id="ba8df-585">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-585">Maximum size</span></span> | <span data-ttu-id="ba8df-586">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-586">Required</span></span> | <span data-ttu-id="ba8df-587">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-587">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="ba8df-588">string</span><span class="sxs-lookup"><span data-stu-id="ba8df-588">string</span></span>|<span data-ttu-id="ba8df-589">32 символа</span><span class="sxs-lookup"><span data-stu-id="ba8df-589">32 characters</span></span>|<span data-ttu-id="ba8df-590">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-590">✔</span></span>|<span data-ttu-id="ba8df-591">Тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="ba8df-591">The notification type.</span></span> <span data-ttu-id="ba8df-592">*См. ниже*.</span><span class="sxs-lookup"><span data-stu-id="ba8df-592">*See below*.</span></span>|
|`description`|<span data-ttu-id="ba8df-593">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-593">string</span></span>|<span data-ttu-id="ba8df-594">128 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-594">128 characters</span></span>|<span data-ttu-id="ba8df-595">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-595">✔</span></span>|<span data-ttu-id="ba8df-596">Краткое описание уведомления.</span><span class="sxs-lookup"><span data-stu-id="ba8df-596">A brief description of the notification.</span></span> <span data-ttu-id="ba8df-597">*См. ниже*.</span><span class="sxs-lookup"><span data-stu-id="ba8df-597">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="ba8df-598">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-598">string</span></span>|<span data-ttu-id="ba8df-599">128 символов</span><span class="sxs-lookup"><span data-stu-id="ba8df-599">128 characters</span></span>|<span data-ttu-id="ba8df-600">✔</span><span class="sxs-lookup"><span data-stu-id="ba8df-600">✔</span></span>|<span data-ttu-id="ba8df-601">Ex: "{actor} создал задачу {taskId} для вас"</span><span class="sxs-lookup"><span data-stu-id="ba8df-601">Ex: "{actor} created task {taskId} for you"</span></span>|

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

## <a name="defaultinstallscope"></a><span data-ttu-id="ba8df-602">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="ba8df-602">defaultInstallScope</span></span>

<span data-ttu-id="ba8df-603">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="ba8df-603">**Optional** - string</span></span>

<span data-ttu-id="ba8df-604">Указывает область установки, определяемую для этого приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ba8df-604">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="ba8df-605">Определенным областью будет параметр, отображаемый на кнопке при добавлении приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="ba8df-605">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="ba8df-606">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="ba8df-606">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="ba8df-607">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="ba8df-607">defaultGroupCapability</span></span>

<span data-ttu-id="ba8df-608">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="ba8df-608">**Optional** - object</span></span>

<span data-ttu-id="ba8df-609">Когда будет выбрана область установки группы, она определит возможности по умолчанию при установке приложения пользователем.</span><span class="sxs-lookup"><span data-stu-id="ba8df-609">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="ba8df-610">Доступные варианты:</span><span class="sxs-lookup"><span data-stu-id="ba8df-610">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="ba8df-611">Имя</span><span class="sxs-lookup"><span data-stu-id="ba8df-611">Name</span></span>| <span data-ttu-id="ba8df-612">Тип</span><span class="sxs-lookup"><span data-stu-id="ba8df-612">Type</span></span>| <span data-ttu-id="ba8df-613">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="ba8df-613">Maximum size</span></span> | <span data-ttu-id="ba8df-614">Обязательный</span><span class="sxs-lookup"><span data-stu-id="ba8df-614">Required</span></span> | <span data-ttu-id="ba8df-615">Описание</span><span class="sxs-lookup"><span data-stu-id="ba8df-615">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="ba8df-616">string</span><span class="sxs-lookup"><span data-stu-id="ba8df-616">string</span></span>|||<span data-ttu-id="ba8df-617">Если выбрана область установки, это поле указывает доступные возможности `team` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ba8df-617">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="ba8df-618">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="ba8df-618">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="ba8df-619">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-619">string</span></span>|||<span data-ttu-id="ba8df-620">Если выбрана область установки, это поле указывает доступные возможности `groupchat` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ba8df-620">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="ba8df-621">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="ba8df-621">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="ba8df-622">String</span><span class="sxs-lookup"><span data-stu-id="ba8df-622">string</span></span>|||<span data-ttu-id="ba8df-623">Если выбрана область установки, это поле указывает доступные возможности `meetings` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ba8df-623">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="ba8df-624">Параметры: `tab` `bot` , или `connector` .</span><span class="sxs-lookup"><span data-stu-id="ba8df-624">Options: `tab`, `bot`, or `connector`.</span></span>|


