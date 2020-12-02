---
title: Справочник по схеме манифеста
description: Описание схемы манифеста для Microsoft Teams
keywords: Схема манифеста Teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: 26c6ca0ed6edceb9b34c84c28a43a63f65a348de
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552558"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="e165f-104">Ссылка: схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e165f-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="e165f-105">Манифест Microsoft Teams описывает, как приложение интегрируется в продукт Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e165f-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="e165f-106">Манифест должен соответствовать схеме, размещенной в [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="e165f-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="e165f-107">Также поддерживаются предыдущие версии 1.0-1.4 (в URL-адресе используется "v1. x").</span><span class="sxs-lookup"><span data-stu-id="e165f-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="e165f-108">В приведенном ниже примере схемы показаны все варианты расширения.</span><span class="sxs-lookup"><span data-stu-id="e165f-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="e165f-109">Пример полного манифеста</span><span class="sxs-lookup"><span data-stu-id="e165f-109">Sample full manifest</span></span>

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

<span data-ttu-id="e165f-110">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="e165f-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="e165f-111">$schema</span><span class="sxs-lookup"><span data-stu-id="e165f-111">$schema</span></span>

<span data-ttu-id="e165f-112">*Необязательно, но рекомендуется* — строка</span><span class="sxs-lookup"><span data-stu-id="e165f-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="e165f-113">URL-адрес https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="e165f-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="e165f-114">Версия манифеста</span><span class="sxs-lookup"><span data-stu-id="e165f-114">manifestVersion</span></span>

<span data-ttu-id="e165f-115">**Обязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="e165f-115">**Required** — string</span></span>

<span data-ttu-id="e165f-116">Версия схемы манифеста, используемая манифестом.</span><span class="sxs-lookup"><span data-stu-id="e165f-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="e165f-117">Он должен иметь значения "1,7".</span><span class="sxs-lookup"><span data-stu-id="e165f-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="e165f-118">version</span><span class="sxs-lookup"><span data-stu-id="e165f-118">version</span></span>

<span data-ttu-id="e165f-119">**Обязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="e165f-119">**Required** — string</span></span>

<span data-ttu-id="e165f-120">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="e165f-120">The version of the specific app.</span></span> <span data-ttu-id="e165f-121">Если вы обновите какой-либо элемент в манифесте, необходимо также увеличить номер версии.</span><span class="sxs-lookup"><span data-stu-id="e165f-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="e165f-122">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="e165f-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="e165f-123">Если это приложение было отправлено в хранилище, новый манифест необходимо будет повторно отправить и проверить повторно.</span><span class="sxs-lookup"><span data-stu-id="e165f-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="e165f-124">После этого пользователи этого приложения автоматически получат новый обновленный манифест в течение нескольких часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="e165f-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="e165f-125">Если приложение запросило изменение разрешений, пользователям будет предложено выполнить обновление и повторное согласие на доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="e165f-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="e165f-126">Эта строка версии должна соответствовать стандарту [semver](http://semver.org/) (Major. Значительные. PATCH).</span><span class="sxs-lookup"><span data-stu-id="e165f-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="e165f-127">id</span><span class="sxs-lookup"><span data-stu-id="e165f-127">id</span></span>

<span data-ttu-id="e165f-128">**Обязательный** — идентификатор приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="e165f-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="e165f-129">Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="e165f-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="e165f-130">Если вы зарегистрировали Bot с помощью Microsoft Bot Framework, или веб-приложение вашей вкладки уже входит в Microsoft, у вас уже должен быть идентификатор, и его следует ввести здесь.</span><span class="sxs-lookup"><span data-stu-id="e165f-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="e165f-131">В противном случае необходимо создать новый идентификатор на портале регистрации приложений ([Мои приложения](https://apps.dev.microsoft.com)) Майкрософт, ввести его здесь, а затем повторно использовать его при добавлении ленты. Note: Если вы отправляете обновление существующему приложению в AppSource, идентификатор в манифесте не должен изменяться.</span><span class="sxs-lookup"><span data-stu-id="e165f-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="e165f-132">developer</span><span class="sxs-lookup"><span data-stu-id="e165f-132">developer</span></span>

<span data-ttu-id="e165f-133">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="e165f-133">**Required** — object</span></span>

<span data-ttu-id="e165f-134">Указывает сведения о компании.</span><span class="sxs-lookup"><span data-stu-id="e165f-134">Specifies information about your company.</span></span> <span data-ttu-id="e165f-135">Для приложений, отправляемых в AppSource (ранее — магазин Office), эти значения должны быть сопоставлены со сведениями в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="e165f-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="e165f-136">Ознакомьтесь с нашими [рекомендациями по публикации](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="e165f-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="e165f-137">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-137">Name</span></span>| <span data-ttu-id="e165f-138">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-138">Maximum size</span></span> | <span data-ttu-id="e165f-139">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-139">Required</span></span> | <span data-ttu-id="e165f-140">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="e165f-141">32 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-141">32 characters</span></span>|<span data-ttu-id="e165f-142">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-142">✔</span></span>|<span data-ttu-id="e165f-143">Отображаемое имя разработчика.</span><span class="sxs-lookup"><span data-stu-id="e165f-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="e165f-144">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-144">2048 characters</span></span>|<span data-ttu-id="e165f-145">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-145">✔</span></span>|<span data-ttu-id="e165f-146">URL-адрес https://на веб-сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="e165f-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="e165f-147">Эта ссылка должна принять участие у пользователей в вашей компании или целевой странице для конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="e165f-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="e165f-148">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-148">2048 characters</span></span>|<span data-ttu-id="e165f-149">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-149">✔</span></span>|<span data-ttu-id="e165f-150">URL-адрес https://для политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="e165f-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="e165f-151">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-151">2048 characters</span></span>|<span data-ttu-id="e165f-152">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-152">✔</span></span>|<span data-ttu-id="e165f-153">URL-адрес https://для условий использования разработчиком.</span><span class="sxs-lookup"><span data-stu-id="e165f-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="e165f-154">10 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-154">10 characters</span></span>| |<span data-ttu-id="e165f-155">**Необязательное требование** Идентификатор сети партнера Майкрософт, определяющий партнерскую организацию, которая создает приложение.</span><span class="sxs-lookup"><span data-stu-id="e165f-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="e165f-156">name</span><span class="sxs-lookup"><span data-stu-id="e165f-156">name</span></span>

<span data-ttu-id="e165f-157">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="e165f-157">**Required** — object</span></span>

<span data-ttu-id="e165f-158">Имя приложения, отображаемое для пользователей в интерфейсе Teams.</span><span class="sxs-lookup"><span data-stu-id="e165f-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="e165f-159">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="e165f-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="e165f-160">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="e165f-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="e165f-161">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-161">Name</span></span>| <span data-ttu-id="e165f-162">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-162">Maximum size</span></span> | <span data-ttu-id="e165f-163">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-163">Required</span></span> | <span data-ttu-id="e165f-164">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="e165f-165">30 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-165">30 characters</span></span>|<span data-ttu-id="e165f-166">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-166">✔</span></span>|<span data-ttu-id="e165f-167">Краткое отображаемое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="e165f-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="e165f-168">100 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-168">100 characters</span></span>||<span data-ttu-id="e165f-169">Полное имя приложения, используемое, если имя полного приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="e165f-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="e165f-170">description</span><span class="sxs-lookup"><span data-stu-id="e165f-170">description</span></span>

<span data-ttu-id="e165f-171">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="e165f-171">**Required** — object</span></span>

<span data-ttu-id="e165f-172">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="e165f-172">Describes your app to users.</span></span> <span data-ttu-id="e165f-173">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="e165f-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="e165f-174">Убедитесь, что ваше описание точно описывает ваш интерфейс и предоставляет сведения, помогающие потенциальным клиентам определить, что делает ваш интерфейс.</span><span class="sxs-lookup"><span data-stu-id="e165f-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="e165f-175">Кроме того, в полном описании следует отметить, если для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="e165f-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="e165f-176">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="e165f-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="e165f-177">Краткое описание не должно повторяться в длинном описании и не должно включать имя другого приложения.</span><span class="sxs-lookup"><span data-stu-id="e165f-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="e165f-178">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-178">Name</span></span>| <span data-ttu-id="e165f-179">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-179">Maximum size</span></span> | <span data-ttu-id="e165f-180">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-180">Required</span></span> | <span data-ttu-id="e165f-181">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="e165f-182">80 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-182">80 characters</span></span>|<span data-ttu-id="e165f-183">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-183">✔</span></span>|<span data-ttu-id="e165f-184">Краткое описание интерфейса приложения, используемое при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="e165f-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="e165f-185">4000 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-185">4000 characters</span></span>|<span data-ttu-id="e165f-186">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-186">✔</span></span>|<span data-ttu-id="e165f-187">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="e165f-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="e165f-188">паккаженаме</span><span class="sxs-lookup"><span data-stu-id="e165f-188">packageName</span></span>

<span data-ttu-id="e165f-189">**Необязательное** — строка</span><span class="sxs-lookup"><span data-stu-id="e165f-189">**Optional** — string</span></span>

<span data-ttu-id="e165f-190">Уникальный идентификатор для этого приложения в обратной нотации домена; Пример: com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="e165f-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="e165f-191">Максимальная длина: 64 символа.</span><span class="sxs-lookup"><span data-stu-id="e165f-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="e165f-192">локализатионинфо</span><span class="sxs-lookup"><span data-stu-id="e165f-192">localizationInfo</span></span>

<span data-ttu-id="e165f-193">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="e165f-193">**Optional** — object</span></span>

<span data-ttu-id="e165f-194">Разрешает спецификацию языка по умолчанию, а также указателей на дополнительные языковые файлы.</span><span class="sxs-lookup"><span data-stu-id="e165f-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="e165f-195">См.: [Локализация](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="e165f-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="e165f-196">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-196">Name</span></span>| <span data-ttu-id="e165f-197">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-197">Maximum size</span></span> | <span data-ttu-id="e165f-198">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-198">Required</span></span> | <span data-ttu-id="e165f-199">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="e165f-200">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-200">✔</span></span>|<span data-ttu-id="e165f-201">Тег языка строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="e165f-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="e165f-202">Локализатионинфо. Аддитионаллангуажес</span><span class="sxs-lookup"><span data-stu-id="e165f-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="e165f-203">Массив объектов, задающий дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="e165f-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="e165f-204">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-204">Name</span></span>| <span data-ttu-id="e165f-205">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-205">Maximum size</span></span> | <span data-ttu-id="e165f-206">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-206">Required</span></span> | <span data-ttu-id="e165f-207">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="e165f-208">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-208">✔</span></span>|<span data-ttu-id="e165f-209">Тег языка строк в указанном файле.</span><span class="sxs-lookup"><span data-stu-id="e165f-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="e165f-210">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-210">✔</span></span>|<span data-ttu-id="e165f-211">Относительный путь к файлу. JSON, содержащему переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="e165f-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="e165f-212">icons</span><span class="sxs-lookup"><span data-stu-id="e165f-212">icons</span></span>

<span data-ttu-id="e165f-213">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="e165f-213">**Required** — object</span></span>

<span data-ttu-id="e165f-214">Значки, используемые в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="e165f-214">Icons used within the Teams app.</span></span> <span data-ttu-id="e165f-215">Файлы значков должны быть включены в состав пакета отправки.</span><span class="sxs-lookup"><span data-stu-id="e165f-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="e165f-216">Дополнительные сведения можно найти в разделе [значки](~/concepts/build-and-test/apps-package.md#icons) .</span><span class="sxs-lookup"><span data-stu-id="e165f-216">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="e165f-217">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-217">Name</span></span>| <span data-ttu-id="e165f-218">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-218">Maximum size</span></span> | <span data-ttu-id="e165f-219">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-219">Required</span></span> | <span data-ttu-id="e165f-220">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="e165f-221">32 x 32 пикселей</span><span class="sxs-lookup"><span data-stu-id="e165f-221">32 x 32 pixels</span></span>|<span data-ttu-id="e165f-222">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-222">✔</span></span>|<span data-ttu-id="e165f-223">Относительный путь к файлу с прозрачным значком изображения в формате 32x32 PNG.</span><span class="sxs-lookup"><span data-stu-id="e165f-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="e165f-224">192 x 192 пикселей</span><span class="sxs-lookup"><span data-stu-id="e165f-224">192 x 192 pixels</span></span>|<span data-ttu-id="e165f-225">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-225">✔</span></span>|<span data-ttu-id="e165f-226">Относительный путь к файлу полного цветового значка PNG 192x192.</span><span class="sxs-lookup"><span data-stu-id="e165f-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="e165f-227">акцентколор</span><span class="sxs-lookup"><span data-stu-id="e165f-227">accentColor</span></span>

<span data-ttu-id="e165f-228">**Необязательное** — шестнадцатеричный код цвета HTML</span><span class="sxs-lookup"><span data-stu-id="e165f-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="e165f-229">Цвет, используемый в сочетании с фоном для значков структуры.</span><span class="sxs-lookup"><span data-stu-id="e165f-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="e165f-230">Значение должно быть допустимым цветом HTML-кода, начинающимся с "#", например `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="e165f-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="e165f-231">конфигураблетабс</span><span class="sxs-lookup"><span data-stu-id="e165f-231">configurableTabs</span></span>

<span data-ttu-id="e165f-232">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="e165f-232">**Optional** — array</span></span>

<span data-ttu-id="e165f-233">Используется, когда у вашего приложения есть вкладка "канал группы", требующая дополнительной настройки перед добавлением.</span><span class="sxs-lookup"><span data-stu-id="e165f-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="e165f-234">Настраиваемые вкладки поддерживаются только в области Teams (не личное), и в настоящее время поддерживается только **одна** вкладка на приложение.</span><span class="sxs-lookup"><span data-stu-id="e165f-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="e165f-235">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-235">Name</span></span>| <span data-ttu-id="e165f-236">Тип</span><span class="sxs-lookup"><span data-stu-id="e165f-236">Type</span></span>| <span data-ttu-id="e165f-237">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-237">Maximum size</span></span> | <span data-ttu-id="e165f-238">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-238">Required</span></span> | <span data-ttu-id="e165f-239">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="e165f-240">string</span><span class="sxs-lookup"><span data-stu-id="e165f-240">string</span></span>|<span data-ttu-id="e165f-241">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-241">2048 characters</span></span>|<span data-ttu-id="e165f-242">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-242">✔</span></span>|<span data-ttu-id="e165f-243">URL-адрес https://, используемый при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="e165f-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="e165f-244">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="e165f-244">array of enums</span></span>|<span data-ttu-id="e165f-245">1,1</span><span class="sxs-lookup"><span data-stu-id="e165f-245">1</span></span>|<span data-ttu-id="e165f-246">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-246">✔</span></span>|<span data-ttu-id="e165f-247">В настоящее время настраиваемые вкладки поддерживают только `team` области и `groupchat` области.</span><span class="sxs-lookup"><span data-stu-id="e165f-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="e165f-248">boolean</span><span class="sxs-lookup"><span data-stu-id="e165f-248">boolean</span></span>|||<span data-ttu-id="e165f-249">Значение, указывающее, может ли пользователь обновлять экземпляр конфигурации вкладки после создания.</span><span class="sxs-lookup"><span data-stu-id="e165f-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="e165f-250">Значение по умолчанию: **true**.</span><span class="sxs-lookup"><span data-stu-id="e165f-250">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="e165f-251">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="e165f-251">array of enums</span></span>|<span data-ttu-id="e165f-252">6 </span><span class="sxs-lookup"><span data-stu-id="e165f-252">6</span></span>||<span data-ttu-id="e165f-253">Набор областей, в `contextItem` которых поддерживается вкладка.</span><span class="sxs-lookup"><span data-stu-id="e165f-253">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="e165f-254">Значение по умолчанию: **[чаннелтаб, приватечаттаб, митингчаттаб, митингдетаилстаб]**.</span><span class="sxs-lookup"><span data-stu-id="e165f-254">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="e165f-255">string</span><span class="sxs-lookup"><span data-stu-id="e165f-255">string</span></span>|<span data-ttu-id="e165f-256">2048</span><span class="sxs-lookup"><span data-stu-id="e165f-256">2048</span></span>||<span data-ttu-id="e165f-257">Относительный путь к изображению вкладки для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e165f-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="e165f-258">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="e165f-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="e165f-259">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="e165f-259">array of enums</span></span>|<span data-ttu-id="e165f-260">1,1</span><span class="sxs-lookup"><span data-stu-id="e165f-260">1</span></span>||<span data-ttu-id="e165f-261">Определяет, как будет предоставляться вкладка в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e165f-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="e165f-262">Параметры `sharePointFullPage``sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="e165f-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="e165f-263">статиктабс</span><span class="sxs-lookup"><span data-stu-id="e165f-263">staticTabs</span></span>

<span data-ttu-id="e165f-264">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="e165f-264">**Optional** — array</span></span>

<span data-ttu-id="e165f-265">Определяет набор вкладок, которые по умолчанию можно закреплять, не добавляя пользователей вручную.</span><span class="sxs-lookup"><span data-stu-id="e165f-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="e165f-266">Статические вкладки, объявляемые в `personal` области, всегда фиксируются в личном интерфейсе приложения.</span><span class="sxs-lookup"><span data-stu-id="e165f-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="e165f-267">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="e165f-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="e165f-268">Этот элемент является массивом (не более 16 элементов) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="e165f-268">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="e165f-269">Этот блок необходим только для решений, предоставляющих статическое решение для вкладок.</span><span class="sxs-lookup"><span data-stu-id="e165f-269">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="e165f-270">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-270">Name</span></span>| <span data-ttu-id="e165f-271">Тип</span><span class="sxs-lookup"><span data-stu-id="e165f-271">Type</span></span>| <span data-ttu-id="e165f-272">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-272">Maximum size</span></span> | <span data-ttu-id="e165f-273">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-273">Required</span></span> | <span data-ttu-id="e165f-274">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-274">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="e165f-275">string</span><span class="sxs-lookup"><span data-stu-id="e165f-275">string</span></span>|<span data-ttu-id="e165f-276">64 символа</span><span class="sxs-lookup"><span data-stu-id="e165f-276">64 characters</span></span>|<span data-ttu-id="e165f-277">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-277">✔</span></span>|<span data-ttu-id="e165f-278">Уникальный идентификатор объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="e165f-278">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="e165f-279">string</span><span class="sxs-lookup"><span data-stu-id="e165f-279">string</span></span>|<span data-ttu-id="e165f-280">128 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-280">128 characters</span></span>|<span data-ttu-id="e165f-281">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-281">✔</span></span>|<span data-ttu-id="e165f-282">Отображаемое имя вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="e165f-282">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="e165f-283">string</span><span class="sxs-lookup"><span data-stu-id="e165f-283">string</span></span>||<span data-ttu-id="e165f-284">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-284">✔</span></span>|<span data-ttu-id="e165f-285">URL-адрес https://, указывающий на пользовательский интерфейс сущности, который будет отображаться в полотне Teams.</span><span class="sxs-lookup"><span data-stu-id="e165f-285">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="e165f-286">string</span><span class="sxs-lookup"><span data-stu-id="e165f-286">string</span></span>|||<span data-ttu-id="e165f-287">URL-адрес https://, указывающий на просмотр в браузере пользователем.</span><span class="sxs-lookup"><span data-stu-id="e165f-287">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="e165f-288">string</span><span class="sxs-lookup"><span data-stu-id="e165f-288">string</span></span>|||<span data-ttu-id="e165f-289">URL-адрес https://, указывающий на поисковые запросы пользователя.</span><span class="sxs-lookup"><span data-stu-id="e165f-289">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="e165f-290">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="e165f-290">array of enums</span></span>|<span data-ttu-id="e165f-291">1,1</span><span class="sxs-lookup"><span data-stu-id="e165f-291">1</span></span>|<span data-ttu-id="e165f-292">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-292">✔</span></span>|<span data-ttu-id="e165f-293">В настоящее время статические вкладки поддерживают только `personal` область, что означает, что ее можно подготовить только в рамках личного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e165f-293">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="e165f-294">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="e165f-294">array of enums</span></span>| <span data-ttu-id="e165f-295">2</span><span class="sxs-lookup"><span data-stu-id="e165f-295">2</span></span>|| <span data-ttu-id="e165f-296">Набор областей, в `contextItem` которых поддерживается вкладка.</span><span class="sxs-lookup"><span data-stu-id="e165f-296">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="e165f-297">Если на вкладках требуются контекстно зависимые сведения для отображения релевантного контента или для инициализации процесса проверки подлинности, *обратитесь к разделу* [Получение контекста для вкладки Microsoft Teams](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="e165f-297">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="e165f-298">Боты</span><span class="sxs-lookup"><span data-stu-id="e165f-298">bots</span></span>

<span data-ttu-id="e165f-299">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="e165f-299">**Optional** — array</span></span>

<span data-ttu-id="e165f-300">Определяет одноэлементное решение, а также дополнительные сведения, такие как свойства команды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e165f-300">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="e165f-301">Элемент является массивом ( &mdash; в настоящее время для каждого приложения допускается только один элемент "bot" для каждого приложения) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="e165f-301">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="e165f-302">Этот блок необходим только для решений, предоставляющих интерфейс Bot.</span><span class="sxs-lookup"><span data-stu-id="e165f-302">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="e165f-303">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-303">Name</span></span>| <span data-ttu-id="e165f-304">Тип</span><span class="sxs-lookup"><span data-stu-id="e165f-304">Type</span></span>| <span data-ttu-id="e165f-305">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-305">Maximum size</span></span> | <span data-ttu-id="e165f-306">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-306">Required</span></span> | <span data-ttu-id="e165f-307">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-307">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="e165f-308">string</span><span class="sxs-lookup"><span data-stu-id="e165f-308">string</span></span>|<span data-ttu-id="e165f-309">64 символа</span><span class="sxs-lookup"><span data-stu-id="e165f-309">64 characters</span></span>|<span data-ttu-id="e165f-310">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-310">✔</span></span>|<span data-ttu-id="e165f-311">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e165f-311">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="e165f-312">Это может быть так же, как и общий [идентификатор приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="e165f-312">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="e165f-313">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="e165f-313">array of enums</span></span>|<span data-ttu-id="e165f-314">4</span><span class="sxs-lookup"><span data-stu-id="e165f-314">3</span></span>|<span data-ttu-id="e165f-315">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-315">✔</span></span>|<span data-ttu-id="e165f-316">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="e165f-316">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="e165f-317">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="e165f-317">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="e165f-318">boolean</span><span class="sxs-lookup"><span data-stu-id="e165f-318">boolean</span></span>|||<span data-ttu-id="e165f-319">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="e165f-319">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="e165f-320">Умолчани **`false`**</span><span class="sxs-lookup"><span data-stu-id="e165f-320">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="e165f-321">boolean</span><span class="sxs-lookup"><span data-stu-id="e165f-321">boolean</span></span>|||<span data-ttu-id="e165f-322">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="e165f-322">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="e165f-323">Умолчани `**false**`</span><span class="sxs-lookup"><span data-stu-id="e165f-323">Default: `**false**`</span></span>|
|`supportsFiles`|<span data-ttu-id="e165f-324">boolean</span><span class="sxs-lookup"><span data-stu-id="e165f-324">boolean</span></span>|||<span data-ttu-id="e165f-325">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="e165f-325">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="e165f-326">Умолчани **`false`**</span><span class="sxs-lookup"><span data-stu-id="e165f-326">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="e165f-327">boolean</span><span class="sxs-lookup"><span data-stu-id="e165f-327">boolean</span></span>|||<span data-ttu-id="e165f-328">Значение, указывающее, где канал Bot поддерживает голосовой вызов.</span><span class="sxs-lookup"><span data-stu-id="e165f-328">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="e165f-329">**Важно!** в настоящее время это свойство является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="e165f-329">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="e165f-330">Экспериментальные свойства могут быть неполными и могут изменяться, прежде чем стать полностью доступным.</span><span class="sxs-lookup"><span data-stu-id="e165f-330">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="e165f-331">Он предоставляется только для целей проверки и не должен использоваться в рабочих приложениях.</span><span class="sxs-lookup"><span data-stu-id="e165f-331">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="e165f-332">Умолчани **`false`**</span><span class="sxs-lookup"><span data-stu-id="e165f-332">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="e165f-333">boolean</span><span class="sxs-lookup"><span data-stu-id="e165f-333">boolean</span></span>|||<span data-ttu-id="e165f-334">Значение, указывающее, где в канале Bot поддерживается видеовызов.</span><span class="sxs-lookup"><span data-stu-id="e165f-334">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="e165f-335">**Важно!** в настоящее время это свойство является экспериментальным.</span><span class="sxs-lookup"><span data-stu-id="e165f-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="e165f-336">Экспериментальные свойства могут быть неполными и могут изменяться, прежде чем стать полностью доступным.</span><span class="sxs-lookup"><span data-stu-id="e165f-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="e165f-337">Он предоставляется только для целей проверки и не должен использоваться в рабочих приложениях.</span><span class="sxs-lookup"><span data-stu-id="e165f-337">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="e165f-338">Умолчани **`false`**</span><span class="sxs-lookup"><span data-stu-id="e165f-338">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="e165f-339">Боты. Коммандлистс</span><span class="sxs-lookup"><span data-stu-id="e165f-339">bots.commandLists</span></span>

<span data-ttu-id="e165f-340">Необязательный список команд, которые ваш робот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="e165f-340">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="e165f-341">Объект является массивом (не более 2 элементов) со всеми элементами типа `object` ; необходимо определить отдельный список команд для каждой области, которую поддерживает Bot.</span><span class="sxs-lookup"><span data-stu-id="e165f-341">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="e165f-342">Дополнительные сведения содержатся в [меню Bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="e165f-342">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="e165f-343">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-343">Name</span></span>| <span data-ttu-id="e165f-344">Тип</span><span class="sxs-lookup"><span data-stu-id="e165f-344">Type</span></span>| <span data-ttu-id="e165f-345">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-345">Maximum size</span></span> | <span data-ttu-id="e165f-346">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-346">Required</span></span> | <span data-ttu-id="e165f-347">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-347">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="e165f-348">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="e165f-348">array of enums</span></span>|<span data-ttu-id="e165f-349">4</span><span class="sxs-lookup"><span data-stu-id="e165f-349">3</span></span>|<span data-ttu-id="e165f-350">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-350">✔</span></span>|<span data-ttu-id="e165f-351">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="e165f-351">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="e165f-352">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="e165f-352">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="e165f-353">массив объектов</span><span class="sxs-lookup"><span data-stu-id="e165f-353">array of objects</span></span>|<span data-ttu-id="e165f-354">10 </span><span class="sxs-lookup"><span data-stu-id="e165f-354">10</span></span>|<span data-ttu-id="e165f-355">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-355">✔</span></span>|<span data-ttu-id="e165f-356">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="e165f-356">An array of commands the bot supports:</span></span><br><span data-ttu-id="e165f-357">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="e165f-357">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="e165f-358">`description`: простое описание или пример синтаксиса команды и ее аргумента (строка, 128)</span><span class="sxs-lookup"><span data-stu-id="e165f-358">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="e165f-359">Боты. Коммандлистс. Commands</span><span class="sxs-lookup"><span data-stu-id="e165f-359">bots.commandLists.commands</span></span>

|<span data-ttu-id="e165f-360">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-360">Name</span></span>| <span data-ttu-id="e165f-361">Тип</span><span class="sxs-lookup"><span data-stu-id="e165f-361">Type</span></span>| <span data-ttu-id="e165f-362">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-362">Maximum size</span></span> | <span data-ttu-id="e165f-363">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-363">Required</span></span> | <span data-ttu-id="e165f-364">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-364">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="e165f-365">title</span><span class="sxs-lookup"><span data-stu-id="e165f-365">title</span></span>|<span data-ttu-id="e165f-366">string</span><span class="sxs-lookup"><span data-stu-id="e165f-366">string</span></span>|<span data-ttu-id="e165f-367">12 </span><span class="sxs-lookup"><span data-stu-id="e165f-367">12</span></span>|<span data-ttu-id="e165f-368">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-368">✔</span></span>|<span data-ttu-id="e165f-369">Имя команды Bot</span><span class="sxs-lookup"><span data-stu-id="e165f-369">The bot command name</span></span>|
|<span data-ttu-id="e165f-370">description</span><span class="sxs-lookup"><span data-stu-id="e165f-370">description</span></span>|<span data-ttu-id="e165f-371">string</span><span class="sxs-lookup"><span data-stu-id="e165f-371">string</span></span>|<span data-ttu-id="e165f-372">128 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-372">128 characters</span></span>|<span data-ttu-id="e165f-373">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-373">✔</span></span>|<span data-ttu-id="e165f-374">Простое текстовое описание или пример синтаксиса команды и его аргументов.</span><span class="sxs-lookup"><span data-stu-id="e165f-374">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="e165f-375">аудиовыход</span><span class="sxs-lookup"><span data-stu-id="e165f-375">connectors</span></span>

<span data-ttu-id="e165f-376">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="e165f-376">**Optional** — array</span></span>

<span data-ttu-id="e165f-377">`connectors`Блок определяет соединитель Office 365 для приложения.</span><span class="sxs-lookup"><span data-stu-id="e165f-377">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="e165f-378">Объект является массивом (не более 1 элемента) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="e165f-378">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="e165f-379">Этот блок необходим только для решений, предоставляющих соединитель.</span><span class="sxs-lookup"><span data-stu-id="e165f-379">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="e165f-380">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-380">Name</span></span>| <span data-ttu-id="e165f-381">Тип</span><span class="sxs-lookup"><span data-stu-id="e165f-381">Type</span></span>| <span data-ttu-id="e165f-382">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-382">Maximum size</span></span> | <span data-ttu-id="e165f-383">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-383">Required</span></span> | <span data-ttu-id="e165f-384">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-384">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="e165f-385">string</span><span class="sxs-lookup"><span data-stu-id="e165f-385">string</span></span>|<span data-ttu-id="e165f-386">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-386">2048 characters</span></span>|<span data-ttu-id="e165f-387">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-387">✔</span></span>|<span data-ttu-id="e165f-388">URL-адрес https://, используемый при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="e165f-388">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="e165f-389">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="e165f-389">array of enums</span></span>|<span data-ttu-id="e165f-390">1,1</span><span class="sxs-lookup"><span data-stu-id="e165f-390">1</span></span>|<span data-ttu-id="e165f-391">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-391">✔</span></span>|<span data-ttu-id="e165f-392">Указывает, будет ли соединитель работать в контексте канала в `team` или в интерфейсе для отдельного пользователя ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="e165f-392">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="e165f-393">В настоящее время `team` поддерживается только область действия.</span><span class="sxs-lookup"><span data-stu-id="e165f-393">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="e165f-394">string</span><span class="sxs-lookup"><span data-stu-id="e165f-394">string</span></span>|<span data-ttu-id="e165f-395">64 символа</span><span class="sxs-lookup"><span data-stu-id="e165f-395">64 characters</span></span>|<span data-ttu-id="e165f-396">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-396">✔</span></span>|<span data-ttu-id="e165f-397">Уникальный идентификатор соединителя, который соответствует ИДЕНТИФИКАТОРу в [панели мониторинга разработчика соединителей](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="e165f-397">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="e165f-398">компосикстенсионс</span><span class="sxs-lookup"><span data-stu-id="e165f-398">composeExtensions</span></span>

<span data-ttu-id="e165f-399">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="e165f-399">**Optional** — array</span></span>

<span data-ttu-id="e165f-400">Определяет расширение системы обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="e165f-400">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="e165f-401">Имя компонента изменилось с "расширение составления" на "расширение обмена сообщениями" в ноябре 2017, но имя манифеста остается без изменений, поэтому все существующие расширения продолжают работать.</span><span class="sxs-lookup"><span data-stu-id="e165f-401">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="e165f-402">Элемент является массивом (не более 1 элемента) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="e165f-402">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="e165f-403">Этот блок необходим только для решений, предоставляющих расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e165f-403">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="e165f-404">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-404">Name</span></span>| <span data-ttu-id="e165f-405">Тип</span><span class="sxs-lookup"><span data-stu-id="e165f-405">Type</span></span> | <span data-ttu-id="e165f-406">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-406">Maximum Size</span></span> | <span data-ttu-id="e165f-407">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-407">Required</span></span> | <span data-ttu-id="e165f-408">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-408">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="e165f-409">string</span><span class="sxs-lookup"><span data-stu-id="e165f-409">string</span></span>|<span data-ttu-id="e165f-410">64</span><span class="sxs-lookup"><span data-stu-id="e165f-410">64</span></span>|<span data-ttu-id="e165f-411">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-411">✔</span></span>|<span data-ttu-id="e165f-412">Уникальный идентификатор приложения для ленты, который выполняет резервное копирование расширения обмена сообщениями, как зарегистрировано в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e165f-412">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="e165f-413">Это может быть так же, как и общий идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="e165f-413">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="e165f-414">массив объектов</span><span class="sxs-lookup"><span data-stu-id="e165f-414">array of objects</span></span>|<span data-ttu-id="e165f-415">10 </span><span class="sxs-lookup"><span data-stu-id="e165f-415">10</span></span>|<span data-ttu-id="e165f-416">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-416">✔</span></span>|<span data-ttu-id="e165f-417">массив команд, поддерживающих расширение системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="e165f-417">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="e165f-418">boolean</span><span class="sxs-lookup"><span data-stu-id="e165f-418">boolean</span></span>|||<span data-ttu-id="e165f-419">Значение, указывающее, может ли пользователь изменять конфигурацию расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e165f-419">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="e165f-420">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="e165f-420">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="e165f-421">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="e165f-421">array of Objects</span></span>|<span data-ttu-id="e165f-422">5 </span><span class="sxs-lookup"><span data-stu-id="e165f-422">5</span></span>||<span data-ttu-id="e165f-423">Список обработчиков, позволяющих вызывать приложения при выполнении определенных условий.</span><span class="sxs-lookup"><span data-stu-id="e165f-423">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="e165f-424">Домены также должны быть перечислены в `validDomains`</span><span class="sxs-lookup"><span data-stu-id="e165f-424">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="e165f-425">string</span><span class="sxs-lookup"><span data-stu-id="e165f-425">string</span></span>|||<span data-ttu-id="e165f-426">Тип обработчика сообщений.</span><span class="sxs-lookup"><span data-stu-id="e165f-426">The type of message handler.</span></span> <span data-ttu-id="e165f-427">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="e165f-427">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="e165f-428">Массив строк</span><span class="sxs-lookup"><span data-stu-id="e165f-428">array of Strings</span></span>|||<span data-ttu-id="e165f-429">массив доменов, для которых может регистрироваться обработчик сообщений ссылки.</span><span class="sxs-lookup"><span data-stu-id="e165f-429">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="e165f-430">Компосикстенсионс. Commands</span><span class="sxs-lookup"><span data-stu-id="e165f-430">composeExtensions.commands</span></span>

<span data-ttu-id="e165f-431">Ваш модуль обмена сообщениями должен объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="e165f-431">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="e165f-432">Каждая команда отображается в Microsoft Teams в качестве потенциального взаимодействия от точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e165f-432">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="e165f-433">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="e165f-433">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="e165f-434">Каждый элемент команды представляет собой объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="e165f-434">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="e165f-435">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-435">Name</span></span>| <span data-ttu-id="e165f-436">Тип</span><span class="sxs-lookup"><span data-stu-id="e165f-436">Type</span></span>| <span data-ttu-id="e165f-437">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-437">Maximum size</span></span> | <span data-ttu-id="e165f-438">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-438">Required</span></span> | <span data-ttu-id="e165f-439">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-439">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="e165f-440">string</span><span class="sxs-lookup"><span data-stu-id="e165f-440">string</span></span>|<span data-ttu-id="e165f-441">64 символа</span><span class="sxs-lookup"><span data-stu-id="e165f-441">64 characters</span></span>|<span data-ttu-id="e165f-442">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-442">✔</span></span>|<span data-ttu-id="e165f-443">Идентификатор команды.</span><span class="sxs-lookup"><span data-stu-id="e165f-443">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="e165f-444">string</span><span class="sxs-lookup"><span data-stu-id="e165f-444">string</span></span>|<span data-ttu-id="e165f-445">32 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-445">32 characters</span></span>|<span data-ttu-id="e165f-446">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-446">✔</span></span>|<span data-ttu-id="e165f-447">Понятное имя команды.</span><span class="sxs-lookup"><span data-stu-id="e165f-447">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="e165f-448">string</span><span class="sxs-lookup"><span data-stu-id="e165f-448">string</span></span>|<span data-ttu-id="e165f-449">64 символа</span><span class="sxs-lookup"><span data-stu-id="e165f-449">64 characters</span></span>||<span data-ttu-id="e165f-450">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="e165f-450">Type of the command.</span></span> <span data-ttu-id="e165f-451">Один из `query` или `action` .</span><span class="sxs-lookup"><span data-stu-id="e165f-451">One of `query` or `action`.</span></span> <span data-ttu-id="e165f-452">Значение по умолчанию: **Query**.</span><span class="sxs-lookup"><span data-stu-id="e165f-452">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="e165f-453">string</span><span class="sxs-lookup"><span data-stu-id="e165f-453">string</span></span>|<span data-ttu-id="e165f-454">128 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-454">128 characters</span></span>||<span data-ttu-id="e165f-455">Описание, которое отображается для пользователей, чтобы указать назначение этой команды.</span><span class="sxs-lookup"><span data-stu-id="e165f-455">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="e165f-456">boolean</span><span class="sxs-lookup"><span data-stu-id="e165f-456">boolean</span></span>|||<span data-ttu-id="e165f-457">Логическое значение, которое указывает, следует ли выполнять команду изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="e165f-457">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="e165f-458">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="e165f-458">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="e165f-459">Массив строк</span><span class="sxs-lookup"><span data-stu-id="e165f-459">array of Strings</span></span>|<span data-ttu-id="e165f-460">4</span><span class="sxs-lookup"><span data-stu-id="e165f-460">3</span></span>||<span data-ttu-id="e165f-461">Определяет, откуда можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="e165f-461">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="e165f-462">Любое сочетание `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="e165f-462">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="e165f-463">Значение по умолчанию: `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="e165f-463">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="e165f-464">boolean</span><span class="sxs-lookup"><span data-stu-id="e165f-464">boolean</span></span>|||<span data-ttu-id="e165f-465">Логическое значение, которое указывает, следует ли выполнять динамическое извлечение модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="e165f-465">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="e165f-466">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="e165f-466">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="e165f-467">объект</span><span class="sxs-lookup"><span data-stu-id="e165f-467">object</span></span>|||<span data-ttu-id="e165f-468">Укажите модуль задач для предварительной загрузки при использовании команды расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e165f-468">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="e165f-469">string</span><span class="sxs-lookup"><span data-stu-id="e165f-469">string</span></span>|<span data-ttu-id="e165f-470">64 символа</span><span class="sxs-lookup"><span data-stu-id="e165f-470">64 characters</span></span>||<span data-ttu-id="e165f-471">Заголовок начального диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="e165f-471">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="e165f-472">string</span><span class="sxs-lookup"><span data-stu-id="e165f-472">string</span></span>|||<span data-ttu-id="e165f-473">Ширина диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый".</span><span class="sxs-lookup"><span data-stu-id="e165f-473">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="e165f-474">string</span><span class="sxs-lookup"><span data-stu-id="e165f-474">string</span></span>|||<span data-ttu-id="e165f-475">Высота диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый".</span><span class="sxs-lookup"><span data-stu-id="e165f-475">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="e165f-476">string</span><span class="sxs-lookup"><span data-stu-id="e165f-476">string</span></span>|||<span data-ttu-id="e165f-477">Исходный URL-адрес вебвиев.</span><span class="sxs-lookup"><span data-stu-id="e165f-477">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="e165f-478">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="e165f-478">array of object</span></span>|<span data-ttu-id="e165f-479">5 элементов</span><span class="sxs-lookup"><span data-stu-id="e165f-479">5 items</span></span>|<span data-ttu-id="e165f-480">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-480">✔</span></span>|<span data-ttu-id="e165f-481">Список параметров, которые выполняет команда.</span><span class="sxs-lookup"><span data-stu-id="e165f-481">The list of parameters the command takes.</span></span> <span data-ttu-id="e165f-482">Минимум: 1; максимум: 5.</span><span class="sxs-lookup"><span data-stu-id="e165f-482">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="e165f-483">string</span><span class="sxs-lookup"><span data-stu-id="e165f-483">string</span></span>|<span data-ttu-id="e165f-484">64 символа</span><span class="sxs-lookup"><span data-stu-id="e165f-484">64 characters</span></span>|<span data-ttu-id="e165f-485">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-485">✔</span></span>|<span data-ttu-id="e165f-486">Имя параметра в том виде, в котором оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="e165f-486">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="e165f-487">Он включен в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="e165f-487">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="e165f-488">string</span><span class="sxs-lookup"><span data-stu-id="e165f-488">string</span></span>|<span data-ttu-id="e165f-489">32 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-489">32 characters</span></span>|<span data-ttu-id="e165f-490">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-490">✔</span></span>|<span data-ttu-id="e165f-491">Удобное для пользователя название параметра.</span><span class="sxs-lookup"><span data-stu-id="e165f-491">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="e165f-492">string</span><span class="sxs-lookup"><span data-stu-id="e165f-492">string</span></span>|<span data-ttu-id="e165f-493">128 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-493">128 characters</span></span>||<span data-ttu-id="e165f-494">Понятная пользователю строка, описывающая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="e165f-494">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="e165f-495">string</span><span class="sxs-lookup"><span data-stu-id="e165f-495">string</span></span>|<span data-ttu-id="e165f-496">512 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-496">512 characters</span></span>||<span data-ttu-id="e165f-497">Начальное значение параметра.</span><span class="sxs-lookup"><span data-stu-id="e165f-497">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="e165f-498">string</span><span class="sxs-lookup"><span data-stu-id="e165f-498">string</span></span>|<span data-ttu-id="e165f-499">128 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-499">128 characters</span></span>||<span data-ttu-id="e165f-500">Определяет тип элемента управления, отображаемого в модуле задачи для `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="e165f-500">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="e165f-501">Один из `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="e165f-501">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="e165f-502">массив объектов</span><span class="sxs-lookup"><span data-stu-id="e165f-502">array of objects</span></span>|<span data-ttu-id="e165f-503">10 элементов</span><span class="sxs-lookup"><span data-stu-id="e165f-503">10 items</span></span>||<span data-ttu-id="e165f-504">Варианты выбора для `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="e165f-504">The choice options for the`choiceset`.</span></span> <span data-ttu-id="e165f-505">Используйте только при `parameter.inputType` наличии `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="e165f-505">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="e165f-506">string</span><span class="sxs-lookup"><span data-stu-id="e165f-506">string</span></span>|<span data-ttu-id="e165f-507">128 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-507">128 characters</span></span>|<span data-ttu-id="e165f-508">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-508">✔</span></span>|<span data-ttu-id="e165f-509">Название выбора.</span><span class="sxs-lookup"><span data-stu-id="e165f-509">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="e165f-510">string</span><span class="sxs-lookup"><span data-stu-id="e165f-510">string</span></span>|<span data-ttu-id="e165f-511">512 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-511">512 characters</span></span>|<span data-ttu-id="e165f-512">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-512">✔</span></span>|<span data-ttu-id="e165f-513">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="e165f-513">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="e165f-514">permissions</span><span class="sxs-lookup"><span data-stu-id="e165f-514">permissions</span></span>

<span data-ttu-id="e165f-515">**Необязательное** — массив строк</span><span class="sxs-lookup"><span data-stu-id="e165f-515">**Optional** — array of strings</span></span>

<span data-ttu-id="e165f-516">Массив, `string` определяющий, какие разрешения запрашиваются приложением, что позволяет конечным пользователям знать, как будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="e165f-516">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="e165f-517">Следующие параметры неисключительны:</span><span class="sxs-lookup"><span data-stu-id="e165f-517">The following options are non-exclusive:</span></span>

* <span data-ttu-id="e165f-518">`identity`&emsp;Требуются сведения об удостоверении пользователя</span><span class="sxs-lookup"><span data-stu-id="e165f-518">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="e165f-519">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений участникам группы</span><span class="sxs-lookup"><span data-stu-id="e165f-519">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="e165f-520">Изменение этих разрешений при обновлении приложения приводит к тому, что пользователи будут повторять процесс разрешения при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="e165f-520">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="e165f-521">Дополнительные сведения см. [в разделе Обновление приложения](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) .</span><span class="sxs-lookup"><span data-stu-id="e165f-521">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="e165f-522">девицепермиссионс</span><span class="sxs-lookup"><span data-stu-id="e165f-522">devicePermissions</span></span>

<span data-ttu-id="e165f-523">**Необязательное** — массив строк</span><span class="sxs-lookup"><span data-stu-id="e165f-523">**Optional** — array of strings</span></span>

<span data-ttu-id="e165f-524">Указывает собственные функции на устройстве пользователя, к которым приложение может запрашивать доступ.</span><span class="sxs-lookup"><span data-stu-id="e165f-524">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="e165f-525">Возможные варианты:</span><span class="sxs-lookup"><span data-stu-id="e165f-525">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="e165f-526">валиддомаинс</span><span class="sxs-lookup"><span data-stu-id="e165f-526">validDomains</span></span>

<span data-ttu-id="e165f-527">**Необязательно**, за исключением **обязательного** места, где отмечено</span><span class="sxs-lookup"><span data-stu-id="e165f-527">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="e165f-528">Список допустимых доменов для веб-сайтов, которые приложение ожидает загружать в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="e165f-528">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="e165f-529">Примеры доменов могут включать подстановочные знаки `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="e165f-529">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="e165f-530">Это соответствует только одному сегменту домена; Если вам нужно использовать этот параметр `a.b.example.com` `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="e165f-530">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="e165f-531">Если конфигурация вкладки или контентный пользовательский интерфейс должны перейти к любому другому домену, Кроме того, что используется для настройки вкладок, этот домен необходимо указать здесь.</span><span class="sxs-lookup"><span data-stu-id="e165f-531">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="e165f-532">Тем не менее, **не** нужно включать домены поставщиков удостоверений, которые требуется поддерживать в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="e165f-532">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="e165f-533">Например, для проверки подлинности с помощью идентификатора Google необходимо перенаправить на accounts.google.com, но не следует включать accounts.google.com в `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="e165f-533">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="e165f-534">Приложения Teams, которым для правильной работы требуются собственные URL-адреса SharePoint, могут содержать "{теамситедомаин}" в допустимом списке доменов.</span><span class="sxs-lookup"><span data-stu-id="e165f-534">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e165f-535">Не добавляйте домены за предельный элемент управления (напрямую или с помощью подстановочных знаков).</span><span class="sxs-lookup"><span data-stu-id="e165f-535">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="e165f-536">Например, `yourapp.onmicrosoft.com` является допустимым, но `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="e165f-536">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="e165f-537">Объект является массивом со всеми элементами типа `string` .</span><span class="sxs-lookup"><span data-stu-id="e165f-537">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="e165f-538">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="e165f-538">webApplicationInfo</span></span>

<span data-ttu-id="e165f-539">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="e165f-539">**Optional** — object</span></span>

<span data-ttu-id="e165f-540">Укажите идентификатор приложения Azure Active Directory (Azure AD) и сведения Microsoft Graph, чтобы помочь пользователям легко войти в приложение.</span><span class="sxs-lookup"><span data-stu-id="e165f-540">Specify your Azure Active Directory (Azure AD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="e165f-541">Если ваше приложение зарегистрировано в Azure AD, необходимо указать идентификатор приложения, чтобы администраторы могли легко проверить разрешения и предоставить согласие в центре администрирования Teams.</span><span class="sxs-lookup"><span data-stu-id="e165f-541">If your app is registered in Azure AD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="e165f-542">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-542">Name</span></span>| <span data-ttu-id="e165f-543">Тип</span><span class="sxs-lookup"><span data-stu-id="e165f-543">Type</span></span>| <span data-ttu-id="e165f-544">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-544">Maximum size</span></span> | <span data-ttu-id="e165f-545">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-545">Required</span></span> | <span data-ttu-id="e165f-546">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-546">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="e165f-547">string</span><span class="sxs-lookup"><span data-stu-id="e165f-547">string</span></span>|<span data-ttu-id="e165f-548">36 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-548">36 characters</span></span>|<span data-ttu-id="e165f-549">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-549">✔</span></span>|<span data-ttu-id="e165f-550">Идентификатор приложения AAD приложения.</span><span class="sxs-lookup"><span data-stu-id="e165f-550">AAD application id of the app.</span></span> <span data-ttu-id="e165f-551">Этот идентификатор должен быть идентификатором GUID.</span><span class="sxs-lookup"><span data-stu-id="e165f-551">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="e165f-552">string</span><span class="sxs-lookup"><span data-stu-id="e165f-552">string</span></span>|<span data-ttu-id="e165f-553">2048 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-553">2048 characters</span></span>|<span data-ttu-id="e165f-554">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-554">✔</span></span>|<span data-ttu-id="e165f-555">URL-адрес ресурса приложения для получения маркера проверки подлинности для единого входа.</span><span class="sxs-lookup"><span data-stu-id="e165f-555">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="e165f-556">массив строк</span><span class="sxs-lookup"><span data-stu-id="e165f-556">array of strings</span></span>|<span data-ttu-id="e165f-557">128 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-557">128 characters</span></span>||<span data-ttu-id="e165f-558">Определение разрешения на уровне [отдельных ресурсов](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="e165f-558">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="e165f-559">шовлоадингиндикатор</span><span class="sxs-lookup"><span data-stu-id="e165f-559">showLoadingIndicator</span></span>

<span data-ttu-id="e165f-560">**Необязательный** — логический</span><span class="sxs-lookup"><span data-stu-id="e165f-560">**Optional** — boolean</span></span>

<span data-ttu-id="e165f-561">Указывает, следует ли отображать индикатор загрузки при загрузке приложения или вкладки.</span><span class="sxs-lookup"><span data-stu-id="e165f-561">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="e165f-562">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="e165f-562">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="e165f-563">Если в манифесте приложения задано значение "Шовлоадингиндикатор: true", то для правильной загрузки страницы необходимо изменить страницы содержимого вкладок и модулей задач в соответствии с протоколом, описанным в статье [Показать встроенный документ с индикатором загрузки](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) .</span><span class="sxs-lookup"><span data-stu-id="e165f-563">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="e165f-564">в полноэкранном режим</span><span class="sxs-lookup"><span data-stu-id="e165f-564">isFullScreen</span></span>

 <span data-ttu-id="e165f-565">**Необязательный** — логический</span><span class="sxs-lookup"><span data-stu-id="e165f-565">**Optional** — boolean</span></span>

<span data-ttu-id="e165f-566">Указывает, где отображается личное приложение с панелью заголовков вкладок или без нее.</span><span class="sxs-lookup"><span data-stu-id="e165f-566">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="e165f-567">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="e165f-567">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="e165f-568">activities</span><span class="sxs-lookup"><span data-stu-id="e165f-568">activities</span></span>

<span data-ttu-id="e165f-569">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="e165f-569">**Optional** — object</span></span>

<span data-ttu-id="e165f-570">Определите свойства, которые ваше приложение будет использовать для публикации в канал активности пользователя.</span><span class="sxs-lookup"><span data-stu-id="e165f-570">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="e165f-571">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-571">Name</span></span>| <span data-ttu-id="e165f-572">Тип</span><span class="sxs-lookup"><span data-stu-id="e165f-572">Type</span></span>| <span data-ttu-id="e165f-573">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-573">Maximum size</span></span> | <span data-ttu-id="e165f-574">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-574">Required</span></span> | <span data-ttu-id="e165f-575">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-575">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="e165f-576">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="e165f-576">array of Objects</span></span>|<span data-ttu-id="e165f-577">128 элементов</span><span class="sxs-lookup"><span data-stu-id="e165f-577">128 items</span></span>| | <span data-ttu-id="e165f-578">Укажите типы действий, которые ваше приложение может отправлять в канал активности пользователей.</span><span class="sxs-lookup"><span data-stu-id="e165f-578">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="e165f-579">действия. Активититипес</span><span class="sxs-lookup"><span data-stu-id="e165f-579">activities.activityTypes</span></span>

|<span data-ttu-id="e165f-580">Имя</span><span class="sxs-lookup"><span data-stu-id="e165f-580">Name</span></span>| <span data-ttu-id="e165f-581">Тип</span><span class="sxs-lookup"><span data-stu-id="e165f-581">Type</span></span>| <span data-ttu-id="e165f-582">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="e165f-582">Maximum size</span></span> | <span data-ttu-id="e165f-583">Обязательный</span><span class="sxs-lookup"><span data-stu-id="e165f-583">Required</span></span> | <span data-ttu-id="e165f-584">Описание</span><span class="sxs-lookup"><span data-stu-id="e165f-584">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="e165f-585">string</span><span class="sxs-lookup"><span data-stu-id="e165f-585">string</span></span>|<span data-ttu-id="e165f-586">32 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-586">32 characters</span></span>|<span data-ttu-id="e165f-587">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-587">✔</span></span>|<span data-ttu-id="e165f-588">Тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="e165f-588">The notification type.</span></span> <span data-ttu-id="e165f-589">*Ознакомьтесь* с разделом ниже.</span><span class="sxs-lookup"><span data-stu-id="e165f-589">*See below*.</span></span>|
|`description`|<span data-ttu-id="e165f-590">string</span><span class="sxs-lookup"><span data-stu-id="e165f-590">string</span></span>|<span data-ttu-id="e165f-591">128 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-591">128 characters</span></span>|<span data-ttu-id="e165f-592">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-592">✔</span></span>|<span data-ttu-id="e165f-593">Краткое описание уведомления.</span><span class="sxs-lookup"><span data-stu-id="e165f-593">A brief description of the notification.</span></span> <span data-ttu-id="e165f-594">*Ознакомьтесь* с разделом ниже.</span><span class="sxs-lookup"><span data-stu-id="e165f-594">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="e165f-595">string</span><span class="sxs-lookup"><span data-stu-id="e165f-595">string</span></span>|<span data-ttu-id="e165f-596">128 символов</span><span class="sxs-lookup"><span data-stu-id="e165f-596">128 characters</span></span>|<span data-ttu-id="e165f-597">✔</span><span class="sxs-lookup"><span data-stu-id="e165f-597">✔</span></span>|<span data-ttu-id="e165f-598">Пример: "{Actor} создал задачу {taskId} для вас"</span><span class="sxs-lookup"><span data-stu-id="e165f-598">Ex: "{actor} created task {taskId} for you"</span></span>|

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
