---
title: Справочник по схеме манифеста
description: Описание схемы манифеста для Microsoft Teams
keywords: Схема манифеста teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: cf80251abd22f0c89388cbe5a6287a02dedce1fb
ms.sourcegitcommit: bf61ae5ad2afa4efdb0311158184d0cbb9c40174
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/13/2021
ms.locfileid: "49845632"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="94b95-104">Справка: схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="94b95-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="94b95-105">В манифесте Microsoft Teams описывается, как приложение интегрируется с продуктом Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="94b95-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="94b95-106">Манифест должен соответствовать схеме, которая есть в [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="94b95-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="94b95-107">Поддерживаются также предыдущие версии 1.0-1.4 (с использованием "v1.x" в URL-адресе).</span><span class="sxs-lookup"><span data-stu-id="94b95-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="94b95-108">В следующем примере схемы показаны все параметры возможности для extensibility.</span><span class="sxs-lookup"><span data-stu-id="94b95-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="94b95-109">Пример полного манифеста</span><span class="sxs-lookup"><span data-stu-id="94b95-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.8",
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
  }
}
```

<span data-ttu-id="94b95-110">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="94b95-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="94b95-111">$schema</span><span class="sxs-lookup"><span data-stu-id="94b95-111">$schema</span></span>

<span data-ttu-id="94b95-112">*Необязательный, но рекомендуемый —* строка</span><span class="sxs-lookup"><span data-stu-id="94b95-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="94b95-113">URL-https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="94b95-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="94b95-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="94b95-114">manifestVersion</span></span>

<span data-ttu-id="94b95-115">**Обязательно —** строка</span><span class="sxs-lookup"><span data-stu-id="94b95-115">**Required** — string</span></span>

<span data-ttu-id="94b95-116">Версия схемы манифеста, используемая в этом манифесте.</span><span class="sxs-lookup"><span data-stu-id="94b95-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="94b95-117">Это должно быть "1.7".</span><span class="sxs-lookup"><span data-stu-id="94b95-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="94b95-118">version</span><span class="sxs-lookup"><span data-stu-id="94b95-118">version</span></span>

<span data-ttu-id="94b95-119">**Обязательно —** строка</span><span class="sxs-lookup"><span data-stu-id="94b95-119">**Required** — string</span></span>

<span data-ttu-id="94b95-120">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-120">The version of the specific app.</span></span> <span data-ttu-id="94b95-121">Если вы обновите что-либо в манифесте, необходимо также приумножная версия.</span><span class="sxs-lookup"><span data-stu-id="94b95-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="94b95-122">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="94b95-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="94b95-123">Если это приложение было отправлено в Магазин, новый манифест необходимо повторно представить и проверить повторно.</span><span class="sxs-lookup"><span data-stu-id="94b95-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="94b95-124">Затем пользователи этого приложения получат новый обновленный манифест автоматически через несколько часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="94b95-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="94b95-125">Если приложение запрашивает изменение разрешений, пользователям будет предложено обновить приложение и повторно согласиться на его использование.</span><span class="sxs-lookup"><span data-stu-id="94b95-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="94b95-126">Эта строка версии должна следовать [стандарту semver](http://semver.org/) (MAJOR). MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="94b95-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="94b95-127">id</span><span class="sxs-lookup"><span data-stu-id="94b95-127">id</span></span>

<span data-ttu-id="94b95-128">**Обязательное** — ИД приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="94b95-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="94b95-129">Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="94b95-130">Если вы зарегистрировали бота через Microsoft Bot Framework или веб-приложение вашей вкладки уже входит в Microsoft, у вас должен быть уже свой ИД, и он должен быть здесь.</span><span class="sxs-lookup"><span data-stu-id="94b95-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="94b95-131">В противном случае необходимо создать новый ИД на портале регистрации приложений Майкрософт[(Мои](https://apps.dev.microsoft.com)приложения), ввести его здесь, а затем повторно использовать при добавлении бота. Примечание. Если вы передаете обновление существующему приложению в AppSource, ИД манифеста не должен быть изменен.</span><span class="sxs-lookup"><span data-stu-id="94b95-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="94b95-132">developer</span><span class="sxs-lookup"><span data-stu-id="94b95-132">developer</span></span>

<span data-ttu-id="94b95-133">**Required** — object</span><span class="sxs-lookup"><span data-stu-id="94b95-133">**Required** — object</span></span>

<span data-ttu-id="94b95-134">Указывает сведения о вашей компании.</span><span class="sxs-lookup"><span data-stu-id="94b95-134">Specifies information about your company.</span></span> <span data-ttu-id="94b95-135">Для приложений, отправленных в AppSource (прежнее значение — Магазин Office), эти значения должны соответствовать сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="94b95-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="94b95-136">Дополнительные [сведения см. в](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) наших рекомендациях по публикации.</span><span class="sxs-lookup"><span data-stu-id="94b95-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="94b95-137">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-137">Name</span></span>| <span data-ttu-id="94b95-138">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-138">Maximum size</span></span> | <span data-ttu-id="94b95-139">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-139">Required</span></span> | <span data-ttu-id="94b95-140">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="94b95-141">32 символа</span><span class="sxs-lookup"><span data-stu-id="94b95-141">32 characters</span></span>|<span data-ttu-id="94b95-142">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-142">✔</span></span>|<span data-ttu-id="94b95-143">Отображаемая имя для разработчика.</span><span class="sxs-lookup"><span data-stu-id="94b95-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="94b95-144">2048 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-144">2048 characters</span></span>|<span data-ttu-id="94b95-145">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-145">✔</span></span>|<span data-ttu-id="94b95-146">Url https:// URL-адрес веб-сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="94b95-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="94b95-147">По этой ссылке пользователи должны перенабираться на страницу вашей компании или конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="94b95-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="94b95-148">2048 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-148">2048 characters</span></span>|<span data-ttu-id="94b95-149">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-149">✔</span></span>|<span data-ttu-id="94b95-150">Url https:// URL-адрес политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="94b95-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="94b95-151">2048 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-151">2048 characters</span></span>|<span data-ttu-id="94b95-152">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-152">✔</span></span>|<span data-ttu-id="94b95-153">В https:// URL-адрес условий использования разработчика.</span><span class="sxs-lookup"><span data-stu-id="94b95-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="94b95-154">10 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-154">10 characters</span></span>| |<span data-ttu-id="94b95-155">**Необязательный** Идентификатор Microsoft Partner Network, который определяет партнерской организации, которая строит приложение.</span><span class="sxs-lookup"><span data-stu-id="94b95-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="94b95-156">name</span><span class="sxs-lookup"><span data-stu-id="94b95-156">name</span></span>

<span data-ttu-id="94b95-157">**Required** — object</span><span class="sxs-lookup"><span data-stu-id="94b95-157">**Required** — object</span></span>

<span data-ttu-id="94b95-158">Имя вашего приложения, отображаемого для пользователей в teams.</span><span class="sxs-lookup"><span data-stu-id="94b95-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="94b95-159">Для приложений, отправленных в AppSource, эти значения должны соответствовать сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="94b95-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="94b95-160">Значения и `short` не `full` должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="94b95-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="94b95-161">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-161">Name</span></span>| <span data-ttu-id="94b95-162">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-162">Maximum size</span></span> | <span data-ttu-id="94b95-163">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-163">Required</span></span> | <span data-ttu-id="94b95-164">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="94b95-165">30 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-165">30 characters</span></span>|<span data-ttu-id="94b95-166">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-166">✔</span></span>|<span data-ttu-id="94b95-167">Краткое отображаемом имени приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="94b95-168">100 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-168">100 characters</span></span>||<span data-ttu-id="94b95-169">Полное имя приложения, используемого, если полное имя приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="94b95-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="94b95-170">description</span><span class="sxs-lookup"><span data-stu-id="94b95-170">description</span></span>

<span data-ttu-id="94b95-171">**Required** — object</span><span class="sxs-lookup"><span data-stu-id="94b95-171">**Required** — object</span></span>

<span data-ttu-id="94b95-172">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="94b95-172">Describes your app to users.</span></span> <span data-ttu-id="94b95-173">Для приложений, отправленных в AppSource, эти значения должны соответствовать сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="94b95-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="94b95-174">Убедитесь, что ваше описание точно описывает ваш опыт и предоставляет сведения, которые помогут потенциальным клиентам понять, что делает ваш опыт.</span><span class="sxs-lookup"><span data-stu-id="94b95-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="94b95-175">В полном описании также следует отметить, требуется ли для использования внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="94b95-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="94b95-176">Значения и `short` не `full` должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="94b95-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="94b95-177">Краткое описание не должно повторяться в длинном описании и не должно включать любое другое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="94b95-178">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-178">Name</span></span>| <span data-ttu-id="94b95-179">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-179">Maximum size</span></span> | <span data-ttu-id="94b95-180">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-180">Required</span></span> | <span data-ttu-id="94b95-181">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="94b95-182">80 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-182">80 characters</span></span>|<span data-ttu-id="94b95-183">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-183">✔</span></span>|<span data-ttu-id="94b95-184">Краткое описание работы приложения, используемое при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="94b95-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="94b95-185">4000 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-185">4000 characters</span></span>|<span data-ttu-id="94b95-186">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-186">✔</span></span>|<span data-ttu-id="94b95-187">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="94b95-188">packageName</span><span class="sxs-lookup"><span data-stu-id="94b95-188">packageName</span></span>

<span data-ttu-id="94b95-189">**Необязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="94b95-189">**Optional** — string</span></span>

<span data-ttu-id="94b95-190">Уникальный идентификатор для этого приложения в нотации обратного домена; например, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="94b95-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="94b95-191">Максимальная длина: 64 символа.</span><span class="sxs-lookup"><span data-stu-id="94b95-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="94b95-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="94b95-192">localizationInfo</span></span>

<span data-ttu-id="94b95-193">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="94b95-193">**Optional** — object</span></span>

<span data-ttu-id="94b95-194">Разрешает спецификацию языка по умолчанию, а также указатели на дополнительные языковые файлы.</span><span class="sxs-lookup"><span data-stu-id="94b95-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="94b95-195">См. [локализацию.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="94b95-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="94b95-196">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-196">Name</span></span>| <span data-ttu-id="94b95-197">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-197">Maximum size</span></span> | <span data-ttu-id="94b95-198">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-198">Required</span></span> | <span data-ttu-id="94b95-199">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="94b95-200">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-200">✔</span></span>|<span data-ttu-id="94b95-201">Тег языка строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="94b95-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="94b95-202">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="94b95-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="94b95-203">Массив объектов, определяющих дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="94b95-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="94b95-204">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-204">Name</span></span>| <span data-ttu-id="94b95-205">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-205">Maximum size</span></span> | <span data-ttu-id="94b95-206">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-206">Required</span></span> | <span data-ttu-id="94b95-207">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="94b95-208">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-208">✔</span></span>|<span data-ttu-id="94b95-209">Тег языка строк в предоставленной файле.</span><span class="sxs-lookup"><span data-stu-id="94b95-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="94b95-210">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-210">✔</span></span>|<span data-ttu-id="94b95-211">Относительный путь к JSON-файлу, содержащего переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="94b95-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="94b95-212">icons</span><span class="sxs-lookup"><span data-stu-id="94b95-212">icons</span></span>

<span data-ttu-id="94b95-213">**Required** — object</span><span class="sxs-lookup"><span data-stu-id="94b95-213">**Required** — object</span></span>

<span data-ttu-id="94b95-214">Значки, используемые в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="94b95-214">Icons used within the Teams app.</span></span> <span data-ttu-id="94b95-215">Файлы значков должны быть включены в пакет отправки.</span><span class="sxs-lookup"><span data-stu-id="94b95-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="94b95-216">Дополнительные [сведения см.](../../concepts/build-and-test/apps-package.md#app-icons) в значках.</span><span class="sxs-lookup"><span data-stu-id="94b95-216">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="94b95-217">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-217">Name</span></span>| <span data-ttu-id="94b95-218">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-218">Maximum size</span></span> | <span data-ttu-id="94b95-219">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-219">Required</span></span> | <span data-ttu-id="94b95-220">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="94b95-221">32 x 32 пикселя</span><span class="sxs-lookup"><span data-stu-id="94b95-221">32 x 32 pixels</span></span>|<span data-ttu-id="94b95-222">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-222">✔</span></span>|<span data-ttu-id="94b95-223">Относительный путь к прозрачному значку контура PNG размером 32x32.</span><span class="sxs-lookup"><span data-stu-id="94b95-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="94b95-224">192 x 192 пикселя</span><span class="sxs-lookup"><span data-stu-id="94b95-224">192 x 192 pixels</span></span>|<span data-ttu-id="94b95-225">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-225">✔</span></span>|<span data-ttu-id="94b95-226">Относительный путь к полному значку PNG размером 192x192.</span><span class="sxs-lookup"><span data-stu-id="94b95-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="94b95-227">accentColor</span><span class="sxs-lookup"><span data-stu-id="94b95-227">accentColor</span></span>

<span data-ttu-id="94b95-228">**Необязательный** — htmL-код цвета</span><span class="sxs-lookup"><span data-stu-id="94b95-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="94b95-229">Цвет, который будет применяться в сочетании с значками структур и в качестве фона.</span><span class="sxs-lookup"><span data-stu-id="94b95-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="94b95-230">Значением должен быть допустимый htmL-код цвета, начинающаяся с "#", например `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="94b95-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="94b95-231">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="94b95-231">configurableTabs</span></span>

<span data-ttu-id="94b95-232">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="94b95-232">**Optional** — array</span></span>

<span data-ttu-id="94b95-233">Используется, когда в вашем приложении есть вкладка канала команды, которая требует дополнительной настройки перед его добавлением.</span><span class="sxs-lookup"><span data-stu-id="94b95-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="94b95-234">Настраиваемые вкладки поддерживаются только в области команды (не личной), и в настоящее время поддерживается только одна вкладка для каждого приложения. </span><span class="sxs-lookup"><span data-stu-id="94b95-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="94b95-235">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-235">Name</span></span>| <span data-ttu-id="94b95-236">Тип</span><span class="sxs-lookup"><span data-stu-id="94b95-236">Type</span></span>| <span data-ttu-id="94b95-237">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-237">Maximum size</span></span> | <span data-ttu-id="94b95-238">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-238">Required</span></span> | <span data-ttu-id="94b95-239">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="94b95-240">string</span><span class="sxs-lookup"><span data-stu-id="94b95-240">string</span></span>|<span data-ttu-id="94b95-241">2048 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-241">2048 characters</span></span>|<span data-ttu-id="94b95-242">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-242">✔</span></span>|<span data-ttu-id="94b95-243">URL-https://, который будет применяться при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="94b95-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="94b95-244">массив enums</span><span class="sxs-lookup"><span data-stu-id="94b95-244">array of enums</span></span>|<span data-ttu-id="94b95-245">1 </span><span class="sxs-lookup"><span data-stu-id="94b95-245">1</span></span>|<span data-ttu-id="94b95-246">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-246">✔</span></span>|<span data-ttu-id="94b95-247">В настоящее время настраиваемые вкладки поддерживают только `team` области `groupchat` и области.</span><span class="sxs-lookup"><span data-stu-id="94b95-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="94b95-248">boolean</span><span class="sxs-lookup"><span data-stu-id="94b95-248">boolean</span></span>|||<span data-ttu-id="94b95-249">Значение, указывающее, может ли пользователь обновить экземпляр конфигурации вкладки после создания.</span><span class="sxs-lookup"><span data-stu-id="94b95-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="94b95-250">Значение по умолчанию: **true**.</span><span class="sxs-lookup"><span data-stu-id="94b95-250">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="94b95-251">массив enums</span><span class="sxs-lookup"><span data-stu-id="94b95-251">array of enums</span></span>|<span data-ttu-id="94b95-252">6 </span><span class="sxs-lookup"><span data-stu-id="94b95-252">6</span></span>||<span data-ttu-id="94b95-253">Набор `contextItem` областей, в которых поддерживается вкладка.</span><span class="sxs-lookup"><span data-stu-id="94b95-253">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="94b95-254">По умолчанию: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="94b95-254">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="94b95-255">string</span><span class="sxs-lookup"><span data-stu-id="94b95-255">string</span></span>|<span data-ttu-id="94b95-256">2048</span><span class="sxs-lookup"><span data-stu-id="94b95-256">2048</span></span>||<span data-ttu-id="94b95-257">Относительный путь к изображению предварительного просмотра вкладок для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="94b95-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="94b95-258">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="94b95-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="94b95-259">массив enums</span><span class="sxs-lookup"><span data-stu-id="94b95-259">array of enums</span></span>|<span data-ttu-id="94b95-260">1 </span><span class="sxs-lookup"><span data-stu-id="94b95-260">1</span></span>||<span data-ttu-id="94b95-261">Определяет, как вкладка будет доступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="94b95-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="94b95-262">`sharePointFullPage`Параметры: и`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="94b95-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="94b95-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="94b95-263">staticTabs</span></span>

<span data-ttu-id="94b95-264">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="94b95-264">**Optional** — array</span></span>

<span data-ttu-id="94b95-265">Определяет набор вкладок, которые можно "закрепить" по умолчанию без добавления пользователем вручную.</span><span class="sxs-lookup"><span data-stu-id="94b95-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="94b95-266">Статические вкладки, объявленные в области, всегда закреплены в личном `personal` режиме приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="94b95-267">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="94b95-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="94b95-268">Этот элемент является массивом (не более 16 элементов) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="94b95-268">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="94b95-269">Этот блок требуется только для решений, которые предоставляют статическое решение вкладок.</span><span class="sxs-lookup"><span data-stu-id="94b95-269">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="94b95-270">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-270">Name</span></span>| <span data-ttu-id="94b95-271">Тип</span><span class="sxs-lookup"><span data-stu-id="94b95-271">Type</span></span>| <span data-ttu-id="94b95-272">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-272">Maximum size</span></span> | <span data-ttu-id="94b95-273">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-273">Required</span></span> | <span data-ttu-id="94b95-274">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-274">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="94b95-275">string</span><span class="sxs-lookup"><span data-stu-id="94b95-275">string</span></span>|<span data-ttu-id="94b95-276">64 символа</span><span class="sxs-lookup"><span data-stu-id="94b95-276">64 characters</span></span>|<span data-ttu-id="94b95-277">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-277">✔</span></span>|<span data-ttu-id="94b95-278">Уникальный идентификатор сущности, отображаемой на вкладке.</span><span class="sxs-lookup"><span data-stu-id="94b95-278">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="94b95-279">string</span><span class="sxs-lookup"><span data-stu-id="94b95-279">string</span></span>|<span data-ttu-id="94b95-280">128 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-280">128 characters</span></span>|<span data-ttu-id="94b95-281">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-281">✔</span></span>|<span data-ttu-id="94b95-282">Отображаемого имени вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="94b95-282">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="94b95-283">string</span><span class="sxs-lookup"><span data-stu-id="94b95-283">string</span></span>||<span data-ttu-id="94b95-284">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-284">✔</span></span>|<span data-ttu-id="94b95-285">URL-https://, который указывает на пользовательский интерфейс сущности, который будет отображаться на холсте Teams.</span><span class="sxs-lookup"><span data-stu-id="94b95-285">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="94b95-286">string</span><span class="sxs-lookup"><span data-stu-id="94b95-286">string</span></span>|||<span data-ttu-id="94b95-287">Url https:// URL-адрес, на который будет указан пользователь, если пользователь выбрал просмотр в браузере.</span><span class="sxs-lookup"><span data-stu-id="94b95-287">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="94b95-288">string</span><span class="sxs-lookup"><span data-stu-id="94b95-288">string</span></span>|||<span data-ttu-id="94b95-289">Url https:// URL-адрес, на который нужно указать поисковые запросы пользователя.</span><span class="sxs-lookup"><span data-stu-id="94b95-289">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="94b95-290">массив enums</span><span class="sxs-lookup"><span data-stu-id="94b95-290">array of enums</span></span>|<span data-ttu-id="94b95-291">1 </span><span class="sxs-lookup"><span data-stu-id="94b95-291">1</span></span>|<span data-ttu-id="94b95-292">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-292">✔</span></span>|<span data-ttu-id="94b95-293">В настоящее время статические вкладки поддерживают только область, что означает, что она может быть предусмотрена только в рамках личного `personal` опыта.</span><span class="sxs-lookup"><span data-stu-id="94b95-293">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="94b95-294">массив enums</span><span class="sxs-lookup"><span data-stu-id="94b95-294">array of enums</span></span>| <span data-ttu-id="94b95-295">2 </span><span class="sxs-lookup"><span data-stu-id="94b95-295">2</span></span>|| <span data-ttu-id="94b95-296">Набор `contextItem` областей, в которых поддерживается вкладка.</span><span class="sxs-lookup"><span data-stu-id="94b95-296">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="94b95-297">Если для отображения релевантного контента или инициации потока проверки подлинности на вкладке требуются зависящие от контекста сведения, см. статью  ["Получить контекст"](../../tabs/how-to/access-teams-context.md)для вкладки Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="94b95-297">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="94b95-298">bots</span><span class="sxs-lookup"><span data-stu-id="94b95-298">bots</span></span>

<span data-ttu-id="94b95-299">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="94b95-299">**Optional** — array</span></span>

<span data-ttu-id="94b95-300">Определяет бот-решение, а также необязательные сведения, такие как свойства команды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="94b95-300">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="94b95-301">Элемент является массивом (не более 1 элемента в настоящее время разрешено использовать только один бот для каждого приложения) со всеми элементами &mdash; этого `object` типа.</span><span class="sxs-lookup"><span data-stu-id="94b95-301">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="94b95-302">Этот блок необходим только для решений, которые предоставляют возможность работы с ботом.</span><span class="sxs-lookup"><span data-stu-id="94b95-302">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="94b95-303">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-303">Name</span></span>| <span data-ttu-id="94b95-304">Тип</span><span class="sxs-lookup"><span data-stu-id="94b95-304">Type</span></span>| <span data-ttu-id="94b95-305">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-305">Maximum size</span></span> | <span data-ttu-id="94b95-306">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-306">Required</span></span> | <span data-ttu-id="94b95-307">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-307">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="94b95-308">string</span><span class="sxs-lookup"><span data-stu-id="94b95-308">string</span></span>|<span data-ttu-id="94b95-309">64 символа</span><span class="sxs-lookup"><span data-stu-id="94b95-309">64 characters</span></span>|<span data-ttu-id="94b95-310">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-310">✔</span></span>|<span data-ttu-id="94b95-311">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="94b95-311">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="94b95-312">Вполне возможно, что он будет таким же, как и общий [ИД приложения.](#id)</span><span class="sxs-lookup"><span data-stu-id="94b95-312">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="94b95-313">массив enums</span><span class="sxs-lookup"><span data-stu-id="94b95-313">array of enums</span></span>|<span data-ttu-id="94b95-314">3 </span><span class="sxs-lookup"><span data-stu-id="94b95-314">3</span></span>|<span data-ttu-id="94b95-315">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-315">✔</span></span>|<span data-ttu-id="94b95-316">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="94b95-316">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="94b95-317">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="94b95-317">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="94b95-318">boolean</span><span class="sxs-lookup"><span data-stu-id="94b95-318">boolean</span></span>|||<span data-ttu-id="94b95-319">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="94b95-319">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="94b95-320">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="94b95-320">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="94b95-321">boolean</span><span class="sxs-lookup"><span data-stu-id="94b95-321">boolean</span></span>|||<span data-ttu-id="94b95-322">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="94b95-322">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="94b95-323">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="94b95-323">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="94b95-324">boolean</span><span class="sxs-lookup"><span data-stu-id="94b95-324">boolean</span></span>|||<span data-ttu-id="94b95-325">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="94b95-325">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="94b95-326">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="94b95-326">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="94b95-327">boolean</span><span class="sxs-lookup"><span data-stu-id="94b95-327">boolean</span></span>|||<span data-ttu-id="94b95-328">Значение, указывающее, где бот поддерживает аудиозвук.</span><span class="sxs-lookup"><span data-stu-id="94b95-328">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="94b95-329">**ВАЖНО!** Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="94b95-329">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="94b95-330">Экспериментальные свойства могут быть не завершены и претерпит изменения, прежде чем они становятся полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="94b95-330">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="94b95-331">Она предназначена только для тестирования и исследования и не должна использоваться в производственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="94b95-331">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="94b95-332">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="94b95-332">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="94b95-333">boolean</span><span class="sxs-lookup"><span data-stu-id="94b95-333">boolean</span></span>|||<span data-ttu-id="94b95-334">Значение, указывающее, где бот поддерживает видеозвонков.</span><span class="sxs-lookup"><span data-stu-id="94b95-334">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="94b95-335">**ВАЖНО!** Это свойство в настоящее время является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="94b95-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="94b95-336">Экспериментальные свойства могут быть не завершены и претерпит изменения, прежде чем они становятся полностью доступными.</span><span class="sxs-lookup"><span data-stu-id="94b95-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="94b95-337">Она предназначена только для тестирования и исследования и не должна использоваться в производственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="94b95-337">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="94b95-338">По умолчанию: **`false`**</span><span class="sxs-lookup"><span data-stu-id="94b95-338">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="94b95-339">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="94b95-339">bots.commandLists</span></span>

<span data-ttu-id="94b95-340">Необязательный список команд, которые бот может порекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="94b95-340">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="94b95-341">Объект является массивом (не более 2 элементов) со всеми элементами типа; необходимо определить отдельный список команд для каждой области, поддерживаемой `object` ботом.</span><span class="sxs-lookup"><span data-stu-id="94b95-341">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="94b95-342">Дополнительные [сведения см. в](~/bots/how-to/create-a-bot-commands-menu.md) меню бота.</span><span class="sxs-lookup"><span data-stu-id="94b95-342">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="94b95-343">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-343">Name</span></span>| <span data-ttu-id="94b95-344">Тип</span><span class="sxs-lookup"><span data-stu-id="94b95-344">Type</span></span>| <span data-ttu-id="94b95-345">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-345">Maximum size</span></span> | <span data-ttu-id="94b95-346">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-346">Required</span></span> | <span data-ttu-id="94b95-347">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-347">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="94b95-348">массив enums</span><span class="sxs-lookup"><span data-stu-id="94b95-348">array of enums</span></span>|<span data-ttu-id="94b95-349">3 </span><span class="sxs-lookup"><span data-stu-id="94b95-349">3</span></span>|<span data-ttu-id="94b95-350">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-350">✔</span></span>|<span data-ttu-id="94b95-351">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="94b95-351">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="94b95-352">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="94b95-352">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="94b95-353">массив объектов</span><span class="sxs-lookup"><span data-stu-id="94b95-353">array of objects</span></span>|<span data-ttu-id="94b95-354">10 </span><span class="sxs-lookup"><span data-stu-id="94b95-354">10</span></span>|<span data-ttu-id="94b95-355">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-355">✔</span></span>|<span data-ttu-id="94b95-356">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="94b95-356">An array of commands the bot supports:</span></span><br><span data-ttu-id="94b95-357">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="94b95-357">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="94b95-358">`description`: простое описание или пример синтаксиса команды и ее аргумента (строка, 128)</span><span class="sxs-lookup"><span data-stu-id="94b95-358">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="94b95-359">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="94b95-359">bots.commandLists.commands</span></span>

|<span data-ttu-id="94b95-360">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-360">Name</span></span>| <span data-ttu-id="94b95-361">Тип</span><span class="sxs-lookup"><span data-stu-id="94b95-361">Type</span></span>| <span data-ttu-id="94b95-362">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-362">Maximum size</span></span> | <span data-ttu-id="94b95-363">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-363">Required</span></span> | <span data-ttu-id="94b95-364">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-364">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="94b95-365">title</span><span class="sxs-lookup"><span data-stu-id="94b95-365">title</span></span>|<span data-ttu-id="94b95-366">string</span><span class="sxs-lookup"><span data-stu-id="94b95-366">string</span></span>|<span data-ttu-id="94b95-367">12 </span><span class="sxs-lookup"><span data-stu-id="94b95-367">12</span></span>|<span data-ttu-id="94b95-368">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-368">✔</span></span>|<span data-ttu-id="94b95-369">Имя команды бота</span><span class="sxs-lookup"><span data-stu-id="94b95-369">The bot command name</span></span>|
|<span data-ttu-id="94b95-370">description</span><span class="sxs-lookup"><span data-stu-id="94b95-370">description</span></span>|<span data-ttu-id="94b95-371">string</span><span class="sxs-lookup"><span data-stu-id="94b95-371">string</span></span>|<span data-ttu-id="94b95-372">128 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-372">128 characters</span></span>|<span data-ttu-id="94b95-373">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-373">✔</span></span>|<span data-ttu-id="94b95-374">Простое текстовое описание или пример синтаксиса команды и его аргументов.</span><span class="sxs-lookup"><span data-stu-id="94b95-374">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="94b95-375">соединители</span><span class="sxs-lookup"><span data-stu-id="94b95-375">connectors</span></span>

<span data-ttu-id="94b95-376">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="94b95-376">**Optional** — array</span></span>

<span data-ttu-id="94b95-377">Этот `connectors` блок определяет соединители Office 365 для приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-377">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="94b95-378">Объект является массивом (не более 1 элемента) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="94b95-378">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="94b95-379">Этот блок требуется только для решений, которые предоставляют соединители.</span><span class="sxs-lookup"><span data-stu-id="94b95-379">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="94b95-380">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-380">Name</span></span>| <span data-ttu-id="94b95-381">Тип</span><span class="sxs-lookup"><span data-stu-id="94b95-381">Type</span></span>| <span data-ttu-id="94b95-382">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-382">Maximum size</span></span> | <span data-ttu-id="94b95-383">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-383">Required</span></span> | <span data-ttu-id="94b95-384">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-384">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="94b95-385">string</span><span class="sxs-lookup"><span data-stu-id="94b95-385">string</span></span>|<span data-ttu-id="94b95-386">2048 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-386">2048 characters</span></span>|<span data-ttu-id="94b95-387">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-387">✔</span></span>|<span data-ttu-id="94b95-388">URL https:// URL-адрес, который будет применяться при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="94b95-388">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="94b95-389">массив enums</span><span class="sxs-lookup"><span data-stu-id="94b95-389">array of enums</span></span>|<span data-ttu-id="94b95-390">1 </span><span class="sxs-lookup"><span data-stu-id="94b95-390">1</span></span>|<span data-ttu-id="94b95-391">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-391">✔</span></span>|<span data-ttu-id="94b95-392">Указывает, предоставляет ли соединители интерфейс в контексте канала в канале или только для отдельного пользователя `team` ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="94b95-392">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="94b95-393">В настоящее время `team` поддерживается только область.</span><span class="sxs-lookup"><span data-stu-id="94b95-393">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="94b95-394">string</span><span class="sxs-lookup"><span data-stu-id="94b95-394">string</span></span>|<span data-ttu-id="94b95-395">64 символа</span><span class="sxs-lookup"><span data-stu-id="94b95-395">64 characters</span></span>|<span data-ttu-id="94b95-396">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-396">✔</span></span>|<span data-ttu-id="94b95-397">Уникальный идентификатор соединители, который соответствует его идентификатору в информационной панели разработчика [соединителок.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="94b95-397">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="94b95-398">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="94b95-398">composeExtensions</span></span>

<span data-ttu-id="94b95-399">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="94b95-399">**Optional** — array</span></span>

<span data-ttu-id="94b95-400">Определяет расширение обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-400">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="94b95-401">В ноябре 2017 г. имя функции было изменено с "расширения составить" на "расширение обмена сообщениями", но имя манифеста остается таким же, чтобы существующие расширения продолжают функционировать.</span><span class="sxs-lookup"><span data-stu-id="94b95-401">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="94b95-402">Элемент является массивом (не более 1 элемента) со всеми элементами `object` типа.</span><span class="sxs-lookup"><span data-stu-id="94b95-402">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="94b95-403">Этот блок необходим только для решений, которые предоставляют расширение для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="94b95-403">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="94b95-404">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-404">Name</span></span>| <span data-ttu-id="94b95-405">Тип</span><span class="sxs-lookup"><span data-stu-id="94b95-405">Type</span></span> | <span data-ttu-id="94b95-406">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-406">Maximum Size</span></span> | <span data-ttu-id="94b95-407">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-407">Required</span></span> | <span data-ttu-id="94b95-408">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-408">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="94b95-409">string</span><span class="sxs-lookup"><span data-stu-id="94b95-409">string</span></span>|<span data-ttu-id="94b95-410">64</span><span class="sxs-lookup"><span data-stu-id="94b95-410">64</span></span>|<span data-ttu-id="94b95-411">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-411">✔</span></span>|<span data-ttu-id="94b95-412">Уникальный ИД приложения Майкрософт для бота, который возвращает расширение обмена сообщениями, как зарегистрировано в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="94b95-412">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="94b95-413">Вполне возможно, что он будет таким же, как и общий ИД приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-413">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="94b95-414">массив объектов</span><span class="sxs-lookup"><span data-stu-id="94b95-414">array of objects</span></span>|<span data-ttu-id="94b95-415">10 </span><span class="sxs-lookup"><span data-stu-id="94b95-415">10</span></span>|<span data-ttu-id="94b95-416">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-416">✔</span></span>|<span data-ttu-id="94b95-417">Массив команд, поддерживаемых расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="94b95-417">Array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="94b95-418">boolean</span><span class="sxs-lookup"><span data-stu-id="94b95-418">boolean</span></span>|||<span data-ttu-id="94b95-419">Значение, указывающее, может ли пользователь обновлять конфигурацию расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="94b95-419">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="94b95-420">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="94b95-420">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="94b95-421">массив объектов</span><span class="sxs-lookup"><span data-stu-id="94b95-421">array of Objects</span></span>|<span data-ttu-id="94b95-422">5 </span><span class="sxs-lookup"><span data-stu-id="94b95-422">5</span></span>||<span data-ttu-id="94b95-423">Список обработчиков, которые позволяют вызывать приложения при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="94b95-423">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="94b95-424">string</span><span class="sxs-lookup"><span data-stu-id="94b95-424">string</span></span>|||<span data-ttu-id="94b95-425">Тип обработера сообщений.</span><span class="sxs-lookup"><span data-stu-id="94b95-425">The type of message handler.</span></span> <span data-ttu-id="94b95-426">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="94b95-426">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="94b95-427">массив строк</span><span class="sxs-lookup"><span data-stu-id="94b95-427">array of Strings</span></span>|||<span data-ttu-id="94b95-428">Массив доменов, для которые может регистрироваться обработник сообщений ссылок.</span><span class="sxs-lookup"><span data-stu-id="94b95-428">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="94b95-429">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="94b95-429">composeExtensions.commands</span></span>

<span data-ttu-id="94b95-430">Расширение обмена сообщениями должно объявлять одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="94b95-430">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="94b95-431">Каждая команда отображается в Microsoft Teams как потенциальное взаимодействие с точкой входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="94b95-431">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="94b95-432">Максимум 10 команд.</span><span class="sxs-lookup"><span data-stu-id="94b95-432">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="94b95-433">Каждый элемент команды является объектом со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="94b95-433">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="94b95-434">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-434">Name</span></span>| <span data-ttu-id="94b95-435">Тип</span><span class="sxs-lookup"><span data-stu-id="94b95-435">Type</span></span>| <span data-ttu-id="94b95-436">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-436">Maximum size</span></span> | <span data-ttu-id="94b95-437">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-437">Required</span></span> | <span data-ttu-id="94b95-438">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-438">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="94b95-439">string</span><span class="sxs-lookup"><span data-stu-id="94b95-439">string</span></span>|<span data-ttu-id="94b95-440">64 символа</span><span class="sxs-lookup"><span data-stu-id="94b95-440">64 characters</span></span>|<span data-ttu-id="94b95-441">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-441">✔</span></span>|<span data-ttu-id="94b95-442">ИД команды.</span><span class="sxs-lookup"><span data-stu-id="94b95-442">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="94b95-443">string</span><span class="sxs-lookup"><span data-stu-id="94b95-443">string</span></span>|<span data-ttu-id="94b95-444">32 символа</span><span class="sxs-lookup"><span data-stu-id="94b95-444">32 characters</span></span>|<span data-ttu-id="94b95-445">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-445">✔</span></span>|<span data-ttu-id="94b95-446">Удобное имя команды.</span><span class="sxs-lookup"><span data-stu-id="94b95-446">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="94b95-447">string</span><span class="sxs-lookup"><span data-stu-id="94b95-447">string</span></span>|<span data-ttu-id="94b95-448">64 символа</span><span class="sxs-lookup"><span data-stu-id="94b95-448">64 characters</span></span>||<span data-ttu-id="94b95-449">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="94b95-449">Type of the command.</span></span> <span data-ttu-id="94b95-450">Один из `query` или `action` .</span><span class="sxs-lookup"><span data-stu-id="94b95-450">One of `query` or `action`.</span></span> <span data-ttu-id="94b95-451">По умолчанию: **запрос.**</span><span class="sxs-lookup"><span data-stu-id="94b95-451">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="94b95-452">string</span><span class="sxs-lookup"><span data-stu-id="94b95-452">string</span></span>|<span data-ttu-id="94b95-453">128 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-453">128 characters</span></span>||<span data-ttu-id="94b95-454">Описание, которое отображается для пользователей, чтобы указать назначение этой команды.</span><span class="sxs-lookup"><span data-stu-id="94b95-454">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="94b95-455">boolean</span><span class="sxs-lookup"><span data-stu-id="94b95-455">boolean</span></span>|||<span data-ttu-id="94b95-456">Boolean value that indicates whether the command should be run initially with no parameters.</span><span class="sxs-lookup"><span data-stu-id="94b95-456">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="94b95-457">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="94b95-457">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="94b95-458">массив строк</span><span class="sxs-lookup"><span data-stu-id="94b95-458">array of Strings</span></span>|<span data-ttu-id="94b95-459">3 </span><span class="sxs-lookup"><span data-stu-id="94b95-459">3</span></span>||<span data-ttu-id="94b95-460">Определяет, откуда можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="94b95-460">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="94b95-461">Любое сочетание `compose` , `commandBox` . `message`</span><span class="sxs-lookup"><span data-stu-id="94b95-461">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="94b95-462">Значение по умолчанию: `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="94b95-462">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="94b95-463">boolean</span><span class="sxs-lookup"><span data-stu-id="94b95-463">boolean</span></span>|||<span data-ttu-id="94b95-464">Boolean value that indicates if it should fetch the task module dynamically.</span><span class="sxs-lookup"><span data-stu-id="94b95-464">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="94b95-465">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="94b95-465">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="94b95-466">объект</span><span class="sxs-lookup"><span data-stu-id="94b95-466">object</span></span>|||<span data-ttu-id="94b95-467">Укажите модуль задачи для предварительной загрузки при использовании команды расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="94b95-467">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="94b95-468">string</span><span class="sxs-lookup"><span data-stu-id="94b95-468">string</span></span>|<span data-ttu-id="94b95-469">64 символа</span><span class="sxs-lookup"><span data-stu-id="94b95-469">64 characters</span></span>||<span data-ttu-id="94b95-470">Заголовок начального диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="94b95-470">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="94b95-471">string</span><span class="sxs-lookup"><span data-stu-id="94b95-471">string</span></span>|||<span data-ttu-id="94b95-472">Ширина диалогов — число в пикселях или макет по умолчанию, например "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="94b95-472">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="94b95-473">string</span><span class="sxs-lookup"><span data-stu-id="94b95-473">string</span></span>|||<span data-ttu-id="94b95-474">Высота диалогов — число в пикселях или макет по умолчанию, например "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="94b95-474">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="94b95-475">string</span><span class="sxs-lookup"><span data-stu-id="94b95-475">string</span></span>|||<span data-ttu-id="94b95-476">Исходный URL-адрес веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-476">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="94b95-477">массив объекта</span><span class="sxs-lookup"><span data-stu-id="94b95-477">array of object</span></span>|<span data-ttu-id="94b95-478">5 элементов</span><span class="sxs-lookup"><span data-stu-id="94b95-478">5 items</span></span>|<span data-ttu-id="94b95-479">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-479">✔</span></span>|<span data-ttu-id="94b95-480">Список параметров, которые принимает команда.</span><span class="sxs-lookup"><span data-stu-id="94b95-480">The list of parameters the command takes.</span></span> <span data-ttu-id="94b95-481">Минимум: 1; максимум: 5.</span><span class="sxs-lookup"><span data-stu-id="94b95-481">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="94b95-482">string</span><span class="sxs-lookup"><span data-stu-id="94b95-482">string</span></span>|<span data-ttu-id="94b95-483">64 символа</span><span class="sxs-lookup"><span data-stu-id="94b95-483">64 characters</span></span>|<span data-ttu-id="94b95-484">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-484">✔</span></span>|<span data-ttu-id="94b95-485">Имя параметра, которое отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="94b95-485">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="94b95-486">Это включается в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="94b95-486">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="94b95-487">string</span><span class="sxs-lookup"><span data-stu-id="94b95-487">string</span></span>|<span data-ttu-id="94b95-488">32 символа</span><span class="sxs-lookup"><span data-stu-id="94b95-488">32 characters</span></span>|<span data-ttu-id="94b95-489">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-489">✔</span></span>|<span data-ttu-id="94b95-490">Удобное название параметра.</span><span class="sxs-lookup"><span data-stu-id="94b95-490">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="94b95-491">string</span><span class="sxs-lookup"><span data-stu-id="94b95-491">string</span></span>|<span data-ttu-id="94b95-492">128 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-492">128 characters</span></span>||<span data-ttu-id="94b95-493">Пользовательская строка, описывая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="94b95-493">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="94b95-494">string</span><span class="sxs-lookup"><span data-stu-id="94b95-494">string</span></span>|<span data-ttu-id="94b95-495">512 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-495">512 characters</span></span>||<span data-ttu-id="94b95-496">Начальное значение параметра.</span><span class="sxs-lookup"><span data-stu-id="94b95-496">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="94b95-497">string</span><span class="sxs-lookup"><span data-stu-id="94b95-497">string</span></span>|<span data-ttu-id="94b95-498">128 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-498">128 characters</span></span>||<span data-ttu-id="94b95-499">Определяет тип управления, отображаемого в модуле задачи для `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="94b95-499">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="94b95-500">Один из `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="94b95-500">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="94b95-501">массив объектов</span><span class="sxs-lookup"><span data-stu-id="94b95-501">array of objects</span></span>|<span data-ttu-id="94b95-502">10 элементов</span><span class="sxs-lookup"><span data-stu-id="94b95-502">10 items</span></span>||<span data-ttu-id="94b95-503">Варианты выбора для `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="94b95-503">The choice options for the`choiceset`.</span></span> <span data-ttu-id="94b95-504">Используйте только в `parameter.inputType` том случае, если это `choiceset` так.</span><span class="sxs-lookup"><span data-stu-id="94b95-504">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="94b95-505">string</span><span class="sxs-lookup"><span data-stu-id="94b95-505">string</span></span>|<span data-ttu-id="94b95-506">128 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-506">128 characters</span></span>|<span data-ttu-id="94b95-507">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-507">✔</span></span>|<span data-ttu-id="94b95-508">Заголовок выбора.</span><span class="sxs-lookup"><span data-stu-id="94b95-508">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="94b95-509">string</span><span class="sxs-lookup"><span data-stu-id="94b95-509">string</span></span>|<span data-ttu-id="94b95-510">512 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-510">512 characters</span></span>|<span data-ttu-id="94b95-511">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-511">✔</span></span>|<span data-ttu-id="94b95-512">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="94b95-512">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="94b95-513">permissions</span><span class="sxs-lookup"><span data-stu-id="94b95-513">permissions</span></span>

<span data-ttu-id="94b95-514">**Необязательный** — массив строк</span><span class="sxs-lookup"><span data-stu-id="94b95-514">**Optional** — array of strings</span></span>

<span data-ttu-id="94b95-515">Массив, в котором указывается, какие разрешения запрашивает приложение, что позволяет конечным пользователям узнать, как `string` будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="94b95-515">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="94b95-516">Следующие параметры являются неисключиющими:</span><span class="sxs-lookup"><span data-stu-id="94b95-516">The following options are non-exclusive:</span></span>

* <span data-ttu-id="94b95-517">`identity`&emsp;Требуется информация об удостоверении пользователя</span><span class="sxs-lookup"><span data-stu-id="94b95-517">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="94b95-518">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений участникам группы</span><span class="sxs-lookup"><span data-stu-id="94b95-518">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="94b95-519">Изменение этих разрешений при обновлении приложения приведет к повтору пользователями процесса получения согласия при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-519">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="94b95-520">Дополнительные [сведения см. в](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) обновлении приложения.</span><span class="sxs-lookup"><span data-stu-id="94b95-520">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="94b95-521">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="94b95-521">devicePermissions</span></span>

<span data-ttu-id="94b95-522">**Необязательный** — массив строк</span><span class="sxs-lookup"><span data-stu-id="94b95-522">**Optional** — array of strings</span></span>

<span data-ttu-id="94b95-523">Указывает нативные функции на устройстве пользователя, к которые ваше приложение может запросить доступ.</span><span class="sxs-lookup"><span data-stu-id="94b95-523">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="94b95-524">Возможные варианты:</span><span class="sxs-lookup"><span data-stu-id="94b95-524">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="94b95-525">validDomains</span><span class="sxs-lookup"><span data-stu-id="94b95-525">validDomains</span></span>

<span data-ttu-id="94b95-526">**Необязательный**, за **исключением обязательного,** если отмечено</span><span class="sxs-lookup"><span data-stu-id="94b95-526">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="94b95-527">Список допустимого домена для веб-сайтов, которые приложение ожидает загрузить в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="94b95-527">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="94b95-528">В списки доменов могут включались поддеревные знаки, `*.example.com` например.</span><span class="sxs-lookup"><span data-stu-id="94b95-528">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="94b95-529">Это соответствует только одному сегменту домена; если вам нужно найти `a.b.example.com` соответствие, используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="94b95-529">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="94b95-530">Если конфигурации вкладок или пользовательскому интерфейсу содержимого требуется перейти к любому другому домену, кроме того, который используется для настройки вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="94b95-530">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="94b95-531">Однако нет **необходимости** включать в приложение домены поставщиков удостоверений, которые вы хотите поддерживать.</span><span class="sxs-lookup"><span data-stu-id="94b95-531">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="94b95-532">Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить его на accounts.google.com, но не следует включать `validDomains[]` accounts.google.com.</span><span class="sxs-lookup"><span data-stu-id="94b95-532">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="94b95-533">Приложения Teams, для работы с которые требуются собственные URL-адреса SharePoint, могут включать "{teamsitedomain}" в допустимый список доменов.</span><span class="sxs-lookup"><span data-stu-id="94b95-533">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94b95-534">Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью поддиагром.</span><span class="sxs-lookup"><span data-stu-id="94b95-534">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="94b95-535">Например, `yourapp.onmicrosoft.com` допустимо, но `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="94b95-535">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="94b95-536">Объект является массивом со всеми элементами этого `string` типа.</span><span class="sxs-lookup"><span data-stu-id="94b95-536">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="94b95-537">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="94b95-537">webApplicationInfo</span></span>

<span data-ttu-id="94b95-538">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="94b95-538">**Optional** — object</span></span>

<span data-ttu-id="94b95-539">Укажите свой ИД приложения Azure Active Directory (Azure AD) и сведения Microsoft Graph, чтобы пользователи легко влияли на ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="94b95-539">Specify your Azure Active Directory (Azure AD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="94b95-540">Если ваше приложение зарегистрировано в Azure AD, необходимо предоставить ИД приложения, чтобы администраторы могли легко просмотреть разрешения и предоставить согласие в Центре администрирования Teams.</span><span class="sxs-lookup"><span data-stu-id="94b95-540">If your app is registered in Azure AD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="94b95-541">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-541">Name</span></span>| <span data-ttu-id="94b95-542">Тип</span><span class="sxs-lookup"><span data-stu-id="94b95-542">Type</span></span>| <span data-ttu-id="94b95-543">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-543">Maximum size</span></span> | <span data-ttu-id="94b95-544">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-544">Required</span></span> | <span data-ttu-id="94b95-545">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-545">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="94b95-546">string</span><span class="sxs-lookup"><span data-stu-id="94b95-546">string</span></span>|<span data-ttu-id="94b95-547">36 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-547">36 characters</span></span>|<span data-ttu-id="94b95-548">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-548">✔</span></span>|<span data-ttu-id="94b95-549">ИД приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="94b95-549">AAD application id of the app.</span></span> <span data-ttu-id="94b95-550">Этот ид должен быть GUID.</span><span class="sxs-lookup"><span data-stu-id="94b95-550">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="94b95-551">string</span><span class="sxs-lookup"><span data-stu-id="94b95-551">string</span></span>|<span data-ttu-id="94b95-552">2048 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-552">2048 characters</span></span>|<span data-ttu-id="94b95-553">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-553">✔</span></span>|<span data-ttu-id="94b95-554">URL-адрес ресурса приложения для получения маркера auth для SSO.</span><span class="sxs-lookup"><span data-stu-id="94b95-554">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="94b95-555">**ПРИМЕЧАНИЕ.** Если вы не используете SSO, убедитесь, что в манифесте приложения введите фикаметричная строковая строка в этом поле, например, чтобы избежать https://notapplicable ошибки.</span><span class="sxs-lookup"><span data-stu-id="94b95-555">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="94b95-556">массив строк</span><span class="sxs-lookup"><span data-stu-id="94b95-556">array of strings</span></span>|<span data-ttu-id="94b95-557">128 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-557">128 characters</span></span>||<span data-ttu-id="94b95-558">Укажите согласие [для конкретного ресурса.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="94b95-558">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="94b95-559">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="94b95-559">showLoadingIndicator</span></span>

<span data-ttu-id="94b95-560">**Необязательный** — boolean</span><span class="sxs-lookup"><span data-stu-id="94b95-560">**Optional** — boolean</span></span>

<span data-ttu-id="94b95-561">Укажите, следует ли показывать индикатор загрузки при загрузке приложения или вкладки.</span><span class="sxs-lookup"><span data-stu-id="94b95-561">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="94b95-562">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="94b95-562">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="94b95-563">Если в манифесте приложения установлено "showLoadingIndicator : true", то для правильной загрузки страницы необходимо изменить страницы содержимого вкладок [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) и модулей задач в зависимости от протокола, описанного в описании документа индикатора загрузки.</span><span class="sxs-lookup"><span data-stu-id="94b95-563">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="94b95-564">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="94b95-564">isFullScreen</span></span>

 <span data-ttu-id="94b95-565">**Необязательный** — boolean</span><span class="sxs-lookup"><span data-stu-id="94b95-565">**Optional** — boolean</span></span>

<span data-ttu-id="94b95-566">Указать, где отрисовка личного приложения с помощью панели вкладок или без нее.</span><span class="sxs-lookup"><span data-stu-id="94b95-566">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="94b95-567">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="94b95-567">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="94b95-568">activities</span><span class="sxs-lookup"><span data-stu-id="94b95-568">activities</span></span>

<span data-ttu-id="94b95-569">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="94b95-569">**Optional** — object</span></span>

<span data-ttu-id="94b95-570">Определите свойства, которые ваше приложение будет использовать для публикации в веб-канале активности пользователя.</span><span class="sxs-lookup"><span data-stu-id="94b95-570">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="94b95-571">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-571">Name</span></span>| <span data-ttu-id="94b95-572">Тип</span><span class="sxs-lookup"><span data-stu-id="94b95-572">Type</span></span>| <span data-ttu-id="94b95-573">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-573">Maximum size</span></span> | <span data-ttu-id="94b95-574">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-574">Required</span></span> | <span data-ttu-id="94b95-575">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-575">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="94b95-576">массив объектов</span><span class="sxs-lookup"><span data-stu-id="94b95-576">array of Objects</span></span>|<span data-ttu-id="94b95-577">128 элементов</span><span class="sxs-lookup"><span data-stu-id="94b95-577">128 items</span></span>| | <span data-ttu-id="94b95-578">Укажите типы действий, которые ваше приложение может опубликовать на веб-канале активности пользователей.</span><span class="sxs-lookup"><span data-stu-id="94b95-578">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="94b95-579">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="94b95-579">activities.activityTypes</span></span>

|<span data-ttu-id="94b95-580">Имя</span><span class="sxs-lookup"><span data-stu-id="94b95-580">Name</span></span>| <span data-ttu-id="94b95-581">Тип</span><span class="sxs-lookup"><span data-stu-id="94b95-581">Type</span></span>| <span data-ttu-id="94b95-582">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="94b95-582">Maximum size</span></span> | <span data-ttu-id="94b95-583">Обязательный</span><span class="sxs-lookup"><span data-stu-id="94b95-583">Required</span></span> | <span data-ttu-id="94b95-584">Описание</span><span class="sxs-lookup"><span data-stu-id="94b95-584">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="94b95-585">string</span><span class="sxs-lookup"><span data-stu-id="94b95-585">string</span></span>|<span data-ttu-id="94b95-586">32 символа</span><span class="sxs-lookup"><span data-stu-id="94b95-586">32 characters</span></span>|<span data-ttu-id="94b95-587">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-587">✔</span></span>|<span data-ttu-id="94b95-588">Тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="94b95-588">The notification type.</span></span> <span data-ttu-id="94b95-589">*См. ниже.*</span><span class="sxs-lookup"><span data-stu-id="94b95-589">*See below*.</span></span>|
|`description`|<span data-ttu-id="94b95-590">string</span><span class="sxs-lookup"><span data-stu-id="94b95-590">string</span></span>|<span data-ttu-id="94b95-591">128 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-591">128 characters</span></span>|<span data-ttu-id="94b95-592">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-592">✔</span></span>|<span data-ttu-id="94b95-593">Краткое описание уведомления.</span><span class="sxs-lookup"><span data-stu-id="94b95-593">A brief description of the notification.</span></span> <span data-ttu-id="94b95-594">*См. ниже.*</span><span class="sxs-lookup"><span data-stu-id="94b95-594">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="94b95-595">string</span><span class="sxs-lookup"><span data-stu-id="94b95-595">string</span></span>|<span data-ttu-id="94b95-596">128 символов</span><span class="sxs-lookup"><span data-stu-id="94b95-596">128 characters</span></span>|<span data-ttu-id="94b95-597">✔</span><span class="sxs-lookup"><span data-stu-id="94b95-597">✔</span></span>|<span data-ttu-id="94b95-598">Например: "{actor} created task {taskId} for you"</span><span class="sxs-lookup"><span data-stu-id="94b95-598">Ex: "{actor} created task {taskId} for you"</span></span>|

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
>
>
