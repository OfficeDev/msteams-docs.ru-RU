---
title: Справочник по схеме манифеста
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams.
keywords: Схема манифеста Teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: b67b23278a2d2bbb2b24c0e828f01cf1789c6191
ms.sourcegitcommit: bac0226d9048c363d96bbaf6f5395388c5f5c45a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/06/2020
ms.locfileid: "45039288"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="49378-104">Ссылка: схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="49378-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="49378-105">Манифест Microsoft Teams описывает, как приложение интегрируется в продукт Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="49378-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="49378-106">Манифест должен соответствовать схеме, размещенной в [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="49378-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="49378-107">Также поддерживаются предыдущие версии 1.0-1.4 (в URL-адресе используется "v1. x").</span><span class="sxs-lookup"><span data-stu-id="49378-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="49378-108">В приведенном ниже примере схемы показаны все варианты расширения.</span><span class="sxs-lookup"><span data-stu-id="49378-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="49378-109">Пример полного манифеста</span><span class="sxs-lookup"><span data-stu-id="49378-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.7",
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
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": "Define how your tab wil be made available in SharePoint (full page or web part)"
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser"
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

<span data-ttu-id="49378-110">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="49378-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="49378-111">$schema</span><span class="sxs-lookup"><span data-stu-id="49378-111">$schema</span></span>

<span data-ttu-id="49378-112">*Необязательно, но рекомендуется* — строка</span><span class="sxs-lookup"><span data-stu-id="49378-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="49378-113">URL-адрес https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="49378-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="49378-114">Версия манифеста</span><span class="sxs-lookup"><span data-stu-id="49378-114">manifestVersion</span></span>

<span data-ttu-id="49378-115">**Обязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="49378-115">**Required** — string</span></span>

<span data-ttu-id="49378-116">Версия схемы манифеста, используемая манифестом.</span><span class="sxs-lookup"><span data-stu-id="49378-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="49378-117">Он должен иметь значения "1,5".</span><span class="sxs-lookup"><span data-stu-id="49378-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="49378-118">version</span><span class="sxs-lookup"><span data-stu-id="49378-118">version</span></span>

<span data-ttu-id="49378-119">**Обязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="49378-119">**Required** — string</span></span>

<span data-ttu-id="49378-120">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="49378-120">The version of the specific app.</span></span> <span data-ttu-id="49378-121">Если вы обновите какой-либо элемент в манифесте, необходимо также увеличить номер версии.</span><span class="sxs-lookup"><span data-stu-id="49378-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="49378-122">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="49378-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="49378-123">Если это приложение было отправлено в хранилище, новый манифест необходимо будет повторно отправить и проверить повторно.</span><span class="sxs-lookup"><span data-stu-id="49378-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="49378-124">После этого пользователи этого приложения автоматически получат новый обновленный манифест в течение нескольких часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="49378-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="49378-125">Если приложение запросило изменение разрешений, пользователям будет предложено выполнить обновление и повторное согласие на доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="49378-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="49378-126">Эта строка версии должна соответствовать стандарту [semver](http://semver.org/) (Major. Значительные. PATCH).</span><span class="sxs-lookup"><span data-stu-id="49378-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="49378-127">id</span><span class="sxs-lookup"><span data-stu-id="49378-127">id</span></span>

<span data-ttu-id="49378-128">**Обязательный** — идентификатор приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="49378-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="49378-129">Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="49378-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="49378-130">Если вы зарегистрировали Bot с помощью Microsoft Bot Framework, или веб-приложение вашей вкладки уже входит в Microsoft, у вас уже должен быть идентификатор, и его следует ввести здесь.</span><span class="sxs-lookup"><span data-stu-id="49378-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="49378-131">В противном случае необходимо создать новый идентификатор на портале регистрации приложений ([Мои приложения](https://apps.dev.microsoft.com)) Майкрософт, ввести его здесь, а затем повторно использовать его при добавлении ленты. Note: Если вы отправляете обновление существующему приложению в AppSource, идентификатор в манифесте не должен изменяться.</span><span class="sxs-lookup"><span data-stu-id="49378-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="49378-132">developer</span><span class="sxs-lookup"><span data-stu-id="49378-132">developer</span></span>

<span data-ttu-id="49378-133">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="49378-133">**Required** — object</span></span>

<span data-ttu-id="49378-134">Указывает сведения о компании.</span><span class="sxs-lookup"><span data-stu-id="49378-134">Specifies information about your company.</span></span> <span data-ttu-id="49378-135">Для приложений, отправляемых в AppSource (ранее — магазин Office), эти значения должны быть сопоставлены со сведениями в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="49378-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="49378-136">Ознакомьтесь с нашими [рекомендациями по публикации](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="49378-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="49378-137">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-137">Name</span></span>| <span data-ttu-id="49378-138">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-138">Maximum size</span></span> | <span data-ttu-id="49378-139">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-139">Required</span></span> | <span data-ttu-id="49378-140">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="49378-141">32 символов</span><span class="sxs-lookup"><span data-stu-id="49378-141">32 characters</span></span>|<span data-ttu-id="49378-142">✔</span><span class="sxs-lookup"><span data-stu-id="49378-142">✔</span></span>|<span data-ttu-id="49378-143">Отображаемое имя разработчика.</span><span class="sxs-lookup"><span data-stu-id="49378-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="49378-144">2048 символов</span><span class="sxs-lookup"><span data-stu-id="49378-144">2048 characters</span></span>|<span data-ttu-id="49378-145">✔</span><span class="sxs-lookup"><span data-stu-id="49378-145">✔</span></span>|<span data-ttu-id="49378-146">URL-адрес https://на веб-сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="49378-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="49378-147">Эта ссылка должна принять участие у пользователей в вашей компании или целевой странице для конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="49378-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="49378-148">2048 символов</span><span class="sxs-lookup"><span data-stu-id="49378-148">2048 characters</span></span>|<span data-ttu-id="49378-149">✔</span><span class="sxs-lookup"><span data-stu-id="49378-149">✔</span></span>|<span data-ttu-id="49378-150">URL-адрес https://для политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="49378-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="49378-151">2048 символов</span><span class="sxs-lookup"><span data-stu-id="49378-151">2048 characters</span></span>|<span data-ttu-id="49378-152">✔</span><span class="sxs-lookup"><span data-stu-id="49378-152">✔</span></span>|<span data-ttu-id="49378-153">URL-адрес https://для условий использования разработчиком.</span><span class="sxs-lookup"><span data-stu-id="49378-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="49378-154">10 символов</span><span class="sxs-lookup"><span data-stu-id="49378-154">10 characters</span></span>| |<span data-ttu-id="49378-155">**Необязательное требование** Идентификатор сети партнера Майкрософт, определяющий партнерскую организацию, которая создает приложение.</span><span class="sxs-lookup"><span data-stu-id="49378-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="49378-156">name</span><span class="sxs-lookup"><span data-stu-id="49378-156">name</span></span>

<span data-ttu-id="49378-157">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="49378-157">**Required** — object</span></span>

<span data-ttu-id="49378-158">Имя приложения, отображаемое для пользователей в интерфейсе Teams.</span><span class="sxs-lookup"><span data-stu-id="49378-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="49378-159">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="49378-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="49378-160">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="49378-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="49378-161">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-161">Name</span></span>| <span data-ttu-id="49378-162">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-162">Maximum size</span></span> | <span data-ttu-id="49378-163">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-163">Required</span></span> | <span data-ttu-id="49378-164">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="49378-165">30 символов</span><span class="sxs-lookup"><span data-stu-id="49378-165">30 characters</span></span>|<span data-ttu-id="49378-166">✔</span><span class="sxs-lookup"><span data-stu-id="49378-166">✔</span></span>|<span data-ttu-id="49378-167">Краткое отображаемое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="49378-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="49378-168">100 символов</span><span class="sxs-lookup"><span data-stu-id="49378-168">100 characters</span></span>||<span data-ttu-id="49378-169">Полное имя приложения, используемое, если имя полного приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="49378-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="49378-170">description</span><span class="sxs-lookup"><span data-stu-id="49378-170">description</span></span>

<span data-ttu-id="49378-171">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="49378-171">**Required** — object</span></span>

<span data-ttu-id="49378-172">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="49378-172">Describes your app to users.</span></span> <span data-ttu-id="49378-173">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="49378-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="49378-174">Убедитесь, что ваше описание точно описывает ваш интерфейс и предоставляет сведения, помогающие потенциальным клиентам определить, что делает ваш интерфейс.</span><span class="sxs-lookup"><span data-stu-id="49378-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="49378-175">Кроме того, в полном описании следует отметить, если для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="49378-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="49378-176">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="49378-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="49378-177">Краткое описание не должно повторяться в длинном описании и не должно включать имя другого приложения.</span><span class="sxs-lookup"><span data-stu-id="49378-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="49378-178">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-178">Name</span></span>| <span data-ttu-id="49378-179">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-179">Maximum size</span></span> | <span data-ttu-id="49378-180">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-180">Required</span></span> | <span data-ttu-id="49378-181">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="49378-182">80 символов</span><span class="sxs-lookup"><span data-stu-id="49378-182">80 characters</span></span>|<span data-ttu-id="49378-183">✔</span><span class="sxs-lookup"><span data-stu-id="49378-183">✔</span></span>|<span data-ttu-id="49378-184">Краткое описание интерфейса приложения, используемое при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="49378-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="49378-185">4000 символов</span><span class="sxs-lookup"><span data-stu-id="49378-185">4000 characters</span></span>|<span data-ttu-id="49378-186">✔</span><span class="sxs-lookup"><span data-stu-id="49378-186">✔</span></span>|<span data-ttu-id="49378-187">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="49378-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="49378-188">паккаженаме</span><span class="sxs-lookup"><span data-stu-id="49378-188">packageName</span></span>

<span data-ttu-id="49378-189">**Необязательное** — строка</span><span class="sxs-lookup"><span data-stu-id="49378-189">**Optional** — string</span></span>

<span data-ttu-id="49378-190">Уникальный идентификатор для этого приложения в обратной нотации домена; Пример: com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="49378-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="49378-191">Максимальная длина: 64 символа.</span><span class="sxs-lookup"><span data-stu-id="49378-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="49378-192">локализатионинфо</span><span class="sxs-lookup"><span data-stu-id="49378-192">localizationInfo</span></span>

<span data-ttu-id="49378-193">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="49378-193">**Optional** — object</span></span>

<span data-ttu-id="49378-194">Разрешает спецификацию языка по умолчанию, а также указателей на дополнительные языковые файлы.</span><span class="sxs-lookup"><span data-stu-id="49378-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="49378-195">См.: [Локализация](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="49378-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="49378-196">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-196">Name</span></span>| <span data-ttu-id="49378-197">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-197">Maximum size</span></span> | <span data-ttu-id="49378-198">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-198">Required</span></span> | <span data-ttu-id="49378-199">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="49378-200">✔</span><span class="sxs-lookup"><span data-stu-id="49378-200">✔</span></span>|<span data-ttu-id="49378-201">Тег языка строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="49378-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="49378-202">Локализатионинфо. Аддитионаллангуажес</span><span class="sxs-lookup"><span data-stu-id="49378-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="49378-203">Массив объектов, задающий дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="49378-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="49378-204">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-204">Name</span></span>| <span data-ttu-id="49378-205">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-205">Maximum size</span></span> | <span data-ttu-id="49378-206">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-206">Required</span></span> | <span data-ttu-id="49378-207">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="49378-208">✔</span><span class="sxs-lookup"><span data-stu-id="49378-208">✔</span></span>|<span data-ttu-id="49378-209">Тег языка строк в указанном файле.</span><span class="sxs-lookup"><span data-stu-id="49378-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="49378-210">✔</span><span class="sxs-lookup"><span data-stu-id="49378-210">✔</span></span>|<span data-ttu-id="49378-211">Относительный путь к файлу. JSON, содержащему переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="49378-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="49378-212">icons</span><span class="sxs-lookup"><span data-stu-id="49378-212">icons</span></span>

<span data-ttu-id="49378-213">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="49378-213">**Required** — object</span></span>

<span data-ttu-id="49378-214">Значки, используемые в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="49378-214">Icons used within the Teams app.</span></span> <span data-ttu-id="49378-215">Файлы значков должны быть включены в состав пакета отправки.</span><span class="sxs-lookup"><span data-stu-id="49378-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="49378-216">Дополнительные сведения можно найти в разделе [значки](~/concepts/build-and-test/apps-package.md#icons) .</span><span class="sxs-lookup"><span data-stu-id="49378-216">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="49378-217">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-217">Name</span></span>| <span data-ttu-id="49378-218">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-218">Maximum size</span></span> | <span data-ttu-id="49378-219">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-219">Required</span></span> | <span data-ttu-id="49378-220">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="49378-221">32 x 32 пикселей</span><span class="sxs-lookup"><span data-stu-id="49378-221">32 x 32 pixels</span></span>|<span data-ttu-id="49378-222">✔</span><span class="sxs-lookup"><span data-stu-id="49378-222">✔</span></span>|<span data-ttu-id="49378-223">Относительный путь к файлу с прозрачным значком изображения в формате 32x32 PNG.</span><span class="sxs-lookup"><span data-stu-id="49378-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="49378-224">192 x 192 пикселей</span><span class="sxs-lookup"><span data-stu-id="49378-224">192 x 192 pixels</span></span>|<span data-ttu-id="49378-225">✔</span><span class="sxs-lookup"><span data-stu-id="49378-225">✔</span></span>|<span data-ttu-id="49378-226">Относительный путь к файлу полного цветового значка PNG 192x192.</span><span class="sxs-lookup"><span data-stu-id="49378-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="49378-227">акцентколор</span><span class="sxs-lookup"><span data-stu-id="49378-227">accentColor</span></span>

<span data-ttu-id="49378-228">**Необязательное** — шестнадцатеричный код цвета HTML</span><span class="sxs-lookup"><span data-stu-id="49378-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="49378-229">Цвет, используемый в сочетании с фоном для значков структуры.</span><span class="sxs-lookup"><span data-stu-id="49378-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="49378-230">Значение должно быть допустимым цветом HTML-кода, начинающимся с "#", например `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="49378-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="49378-231">конфигураблетабс</span><span class="sxs-lookup"><span data-stu-id="49378-231">configurableTabs</span></span>

<span data-ttu-id="49378-232">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="49378-232">**Optional** — array</span></span>

<span data-ttu-id="49378-233">Используется, когда у вашего приложения есть вкладка "канал группы", требующая дополнительной настройки перед добавлением.</span><span class="sxs-lookup"><span data-stu-id="49378-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="49378-234">Настраиваемые вкладки поддерживаются только в области Teams (не личное), и в настоящее время поддерживается только **одна** вкладка на приложение.</span><span class="sxs-lookup"><span data-stu-id="49378-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="49378-235">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-235">Name</span></span>| <span data-ttu-id="49378-236">Тип</span><span class="sxs-lookup"><span data-stu-id="49378-236">Type</span></span>| <span data-ttu-id="49378-237">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-237">Maximum size</span></span> | <span data-ttu-id="49378-238">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-238">Required</span></span> | <span data-ttu-id="49378-239">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="49378-240">string</span><span class="sxs-lookup"><span data-stu-id="49378-240">string</span></span>|<span data-ttu-id="49378-241">2048 символов</span><span class="sxs-lookup"><span data-stu-id="49378-241">2048 characters</span></span>|<span data-ttu-id="49378-242">✔</span><span class="sxs-lookup"><span data-stu-id="49378-242">✔</span></span>|<span data-ttu-id="49378-243">URL-адрес https://, используемый при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="49378-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="49378-244">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="49378-244">array of enum</span></span>|<span data-ttu-id="49378-245">1 </span><span class="sxs-lookup"><span data-stu-id="49378-245">1</span></span>|<span data-ttu-id="49378-246">✔</span><span class="sxs-lookup"><span data-stu-id="49378-246">✔</span></span>|<span data-ttu-id="49378-247">В настоящее время настраиваемые вкладки поддерживают только `team` области и `groupchat` области.</span><span class="sxs-lookup"><span data-stu-id="49378-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="49378-248">boolean</span><span class="sxs-lookup"><span data-stu-id="49378-248">boolean</span></span>|||<span data-ttu-id="49378-249">Значение, указывающее, может ли пользователь обновлять экземпляр конфигурации вкладки после создания.</span><span class="sxs-lookup"><span data-stu-id="49378-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="49378-250">Значение по умолчанию: **true**.</span><span class="sxs-lookup"><span data-stu-id="49378-250">Default: **true**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="49378-251">string</span><span class="sxs-lookup"><span data-stu-id="49378-251">string</span></span>|<span data-ttu-id="49378-252">2048</span><span class="sxs-lookup"><span data-stu-id="49378-252">2048</span></span>||<span data-ttu-id="49378-253">Относительный путь к изображению вкладки для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="49378-253">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="49378-254">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="49378-254">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="49378-255">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="49378-255">array of enum</span></span>|<span data-ttu-id="49378-256">1 </span><span class="sxs-lookup"><span data-stu-id="49378-256">1</span></span>||<span data-ttu-id="49378-257">Определяет, как будет предоставляться вкладка в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="49378-257">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="49378-258">Параметры `sharePointFullPage``sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="49378-258">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="49378-259">статиктабс</span><span class="sxs-lookup"><span data-stu-id="49378-259">staticTabs</span></span>

<span data-ttu-id="49378-260">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="49378-260">**Optional** — array</span></span>

<span data-ttu-id="49378-261">Определяет набор вкладок, которые по умолчанию можно закреплять, не добавляя пользователей вручную.</span><span class="sxs-lookup"><span data-stu-id="49378-261">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="49378-262">Статические вкладки, объявляемые в `personal` области, всегда фиксируются в личном интерфейсе приложения.</span><span class="sxs-lookup"><span data-stu-id="49378-262">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="49378-263">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="49378-263">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="49378-264">Этот элемент является массивом (не более 16 элементов) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="49378-264">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="49378-265">Этот блок необходим только для решений, предоставляющих статическое решение для вкладок.</span><span class="sxs-lookup"><span data-stu-id="49378-265">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="49378-266">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-266">Name</span></span>| <span data-ttu-id="49378-267">Тип</span><span class="sxs-lookup"><span data-stu-id="49378-267">Type</span></span>| <span data-ttu-id="49378-268">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-268">Maximum size</span></span> | <span data-ttu-id="49378-269">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-269">Required</span></span> | <span data-ttu-id="49378-270">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-270">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="49378-271">string</span><span class="sxs-lookup"><span data-stu-id="49378-271">string</span></span>|<span data-ttu-id="49378-272">64 символа</span><span class="sxs-lookup"><span data-stu-id="49378-272">64 characters</span></span>|<span data-ttu-id="49378-273">✔</span><span class="sxs-lookup"><span data-stu-id="49378-273">✔</span></span>|<span data-ttu-id="49378-274">Уникальный идентификатор объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="49378-274">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="49378-275">string</span><span class="sxs-lookup"><span data-stu-id="49378-275">string</span></span>|<span data-ttu-id="49378-276">128 символов</span><span class="sxs-lookup"><span data-stu-id="49378-276">128 characters</span></span>|<span data-ttu-id="49378-277">✔</span><span class="sxs-lookup"><span data-stu-id="49378-277">✔</span></span>|<span data-ttu-id="49378-278">Отображаемое имя вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="49378-278">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="49378-279">string</span><span class="sxs-lookup"><span data-stu-id="49378-279">string</span></span>|<span data-ttu-id="49378-280">2048 символов</span><span class="sxs-lookup"><span data-stu-id="49378-280">2048 characters</span></span>|<span data-ttu-id="49378-281">✔</span><span class="sxs-lookup"><span data-stu-id="49378-281">✔</span></span>|<span data-ttu-id="49378-282">URL-адрес https://, указывающий на пользовательский интерфейс сущности, который будет отображаться в полотне Teams.</span><span class="sxs-lookup"><span data-stu-id="49378-282">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="49378-283">string</span><span class="sxs-lookup"><span data-stu-id="49378-283">string</span></span>|<span data-ttu-id="49378-284">2048 символов</span><span class="sxs-lookup"><span data-stu-id="49378-284">2048 characters</span></span>||<span data-ttu-id="49378-285">URL-адрес https://, указывающий, когда пользователь попытается просмотреть его в браузере.</span><span class="sxs-lookup"><span data-stu-id="49378-285">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="49378-286">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="49378-286">array of enum</span></span>|<span data-ttu-id="49378-287">1 </span><span class="sxs-lookup"><span data-stu-id="49378-287">1</span></span>|<span data-ttu-id="49378-288">✔</span><span class="sxs-lookup"><span data-stu-id="49378-288">✔</span></span>|<span data-ttu-id="49378-289">В настоящее время статические вкладки поддерживают только `personal` область, что означает, что ее можно подготовить только в рамках личного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="49378-289">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

> [!NOTE]
> <span data-ttu-id="49378-290">Если на вкладках требуются контекстно зависимые сведения для отображения релевантного контента или для инициализации процесса проверки подлинности, *обратитесь к разделу* [Получение контекста для вкладки Microsoft Teams](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="49378-290">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="49378-291">Боты</span><span class="sxs-lookup"><span data-stu-id="49378-291">bots</span></span>

<span data-ttu-id="49378-292">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="49378-292">**Optional** — array</span></span>

<span data-ttu-id="49378-293">Определяет одноэлементное решение, а также дополнительные сведения, такие как свойства команды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="49378-293">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="49378-294">Элемент является массивом ( &mdash; в настоящее время для каждого приложения допускается только один элемент "bot" для каждого приложения) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="49378-294">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="49378-295">Этот блок необходим только для решений, предоставляющих интерфейс Bot.</span><span class="sxs-lookup"><span data-stu-id="49378-295">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="49378-296">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-296">Name</span></span>| <span data-ttu-id="49378-297">Тип</span><span class="sxs-lookup"><span data-stu-id="49378-297">Type</span></span>| <span data-ttu-id="49378-298">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-298">Maximum size</span></span> | <span data-ttu-id="49378-299">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-299">Required</span></span> | <span data-ttu-id="49378-300">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-300">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="49378-301">string</span><span class="sxs-lookup"><span data-stu-id="49378-301">string</span></span>|<span data-ttu-id="49378-302">64 символа</span><span class="sxs-lookup"><span data-stu-id="49378-302">64 characters</span></span>|<span data-ttu-id="49378-303">✔</span><span class="sxs-lookup"><span data-stu-id="49378-303">✔</span></span>|<span data-ttu-id="49378-304">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="49378-304">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="49378-305">Это может быть так же, как и общий [идентификатор приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="49378-305">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="49378-306">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="49378-306">array of enum</span></span>|<span data-ttu-id="49378-307">3 </span><span class="sxs-lookup"><span data-stu-id="49378-307">3</span></span>|<span data-ttu-id="49378-308">✔</span><span class="sxs-lookup"><span data-stu-id="49378-308">✔</span></span>|<span data-ttu-id="49378-309">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="49378-309">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="49378-310">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="49378-310">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="49378-311">boolean</span><span class="sxs-lookup"><span data-stu-id="49378-311">boolean</span></span>|||<span data-ttu-id="49378-312">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="49378-312">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="49378-313">Умолчани**`false`**</span><span class="sxs-lookup"><span data-stu-id="49378-313">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="49378-314">boolean</span><span class="sxs-lookup"><span data-stu-id="49378-314">boolean</span></span>|||<span data-ttu-id="49378-315">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="49378-315">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="49378-316">Умолчани`**false**`</span><span class="sxs-lookup"><span data-stu-id="49378-316">Default: `**false**`</span></span>|
|`supportsFiles`|<span data-ttu-id="49378-317">boolean</span><span class="sxs-lookup"><span data-stu-id="49378-317">boolean</span></span>|||<span data-ttu-id="49378-318">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="49378-318">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="49378-319">Умолчани**`false`**</span><span class="sxs-lookup"><span data-stu-id="49378-319">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="49378-320">Боты. Коммандлистс</span><span class="sxs-lookup"><span data-stu-id="49378-320">bots.commandLists</span></span>

<span data-ttu-id="49378-321">Необязательный список команд, которые ваш робот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="49378-321">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="49378-322">Объект является массивом (не более 2 элементов) со всеми элементами типа `object` ; необходимо определить отдельный список команд для каждой области, которую поддерживает Bot.</span><span class="sxs-lookup"><span data-stu-id="49378-322">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="49378-323">Дополнительные сведения содержатся в [меню Bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="49378-323">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="49378-324">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-324">Name</span></span>| <span data-ttu-id="49378-325">Тип</span><span class="sxs-lookup"><span data-stu-id="49378-325">Type</span></span>| <span data-ttu-id="49378-326">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-326">Maximum size</span></span> | <span data-ttu-id="49378-327">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-327">Required</span></span> | <span data-ttu-id="49378-328">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-328">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="49378-329">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="49378-329">array of enum</span></span>|<span data-ttu-id="49378-330">3 </span><span class="sxs-lookup"><span data-stu-id="49378-330">3</span></span>|<span data-ttu-id="49378-331">✔</span><span class="sxs-lookup"><span data-stu-id="49378-331">✔</span></span>|<span data-ttu-id="49378-332">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="49378-332">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="49378-333">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="49378-333">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="49378-334">массив объектов</span><span class="sxs-lookup"><span data-stu-id="49378-334">array of objects</span></span>|<span data-ttu-id="49378-335">10 </span><span class="sxs-lookup"><span data-stu-id="49378-335">10</span></span>|<span data-ttu-id="49378-336">✔</span><span class="sxs-lookup"><span data-stu-id="49378-336">✔</span></span>|<span data-ttu-id="49378-337">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="49378-337">An array of commands the bot supports:</span></span><br><span data-ttu-id="49378-338">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="49378-338">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="49378-339">`description`: простое описание или пример синтаксиса команды и ее аргумента (строка, 128)</span><span class="sxs-lookup"><span data-stu-id="49378-339">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="49378-340">Боты. Коммандлистс. Commands</span><span class="sxs-lookup"><span data-stu-id="49378-340">bots.commandLists.commands</span></span>

|<span data-ttu-id="49378-341">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-341">Name</span></span>| <span data-ttu-id="49378-342">Тип</span><span class="sxs-lookup"><span data-stu-id="49378-342">Type</span></span>| <span data-ttu-id="49378-343">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-343">Maximum size</span></span> | <span data-ttu-id="49378-344">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-344">Required</span></span> | <span data-ttu-id="49378-345">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-345">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="49378-346">title</span><span class="sxs-lookup"><span data-stu-id="49378-346">title</span></span>|<span data-ttu-id="49378-347">string</span><span class="sxs-lookup"><span data-stu-id="49378-347">string</span></span>|<span data-ttu-id="49378-348">12 </span><span class="sxs-lookup"><span data-stu-id="49378-348">12</span></span>|<span data-ttu-id="49378-349">✔</span><span class="sxs-lookup"><span data-stu-id="49378-349">✔</span></span>|<span data-ttu-id="49378-350">Имя команды Bot</span><span class="sxs-lookup"><span data-stu-id="49378-350">The bot command name</span></span>|
|<span data-ttu-id="49378-351">description</span><span class="sxs-lookup"><span data-stu-id="49378-351">description</span></span>|<span data-ttu-id="49378-352">string</span><span class="sxs-lookup"><span data-stu-id="49378-352">string</span></span>|<span data-ttu-id="49378-353">128 символов</span><span class="sxs-lookup"><span data-stu-id="49378-353">128 characters</span></span>|<span data-ttu-id="49378-354">✔</span><span class="sxs-lookup"><span data-stu-id="49378-354">✔</span></span>|<span data-ttu-id="49378-355">Простое текстовое описание или пример синтаксиса команды и его аргументов.</span><span class="sxs-lookup"><span data-stu-id="49378-355">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="49378-356">аудиовыход</span><span class="sxs-lookup"><span data-stu-id="49378-356">connectors</span></span>

<span data-ttu-id="49378-357">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="49378-357">**Optional** — array</span></span>

<span data-ttu-id="49378-358">`connectors`Блок определяет соединитель Office 365 для приложения.</span><span class="sxs-lookup"><span data-stu-id="49378-358">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="49378-359">Объект является массивом (не более 1 элемента) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="49378-359">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="49378-360">Этот блок необходим только для решений, предоставляющих соединитель.</span><span class="sxs-lookup"><span data-stu-id="49378-360">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="49378-361">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-361">Name</span></span>| <span data-ttu-id="49378-362">Тип</span><span class="sxs-lookup"><span data-stu-id="49378-362">Type</span></span>| <span data-ttu-id="49378-363">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-363">Maximum size</span></span> | <span data-ttu-id="49378-364">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-364">Required</span></span> | <span data-ttu-id="49378-365">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-365">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="49378-366">string</span><span class="sxs-lookup"><span data-stu-id="49378-366">string</span></span>|<span data-ttu-id="49378-367">2048 символов</span><span class="sxs-lookup"><span data-stu-id="49378-367">2048 characters</span></span>|<span data-ttu-id="49378-368">✔</span><span class="sxs-lookup"><span data-stu-id="49378-368">✔</span></span>|<span data-ttu-id="49378-369">URL-адрес https://, используемый при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="49378-369">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="49378-370">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="49378-370">array of enum</span></span>|<span data-ttu-id="49378-371">1 </span><span class="sxs-lookup"><span data-stu-id="49378-371">1</span></span>|<span data-ttu-id="49378-372">✔</span><span class="sxs-lookup"><span data-stu-id="49378-372">✔</span></span>|<span data-ttu-id="49378-373">Указывает, будет ли соединитель работать в контексте канала в `team` или в интерфейсе для отдельного пользователя ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="49378-373">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="49378-374">В настоящее время `team` поддерживается только область действия.</span><span class="sxs-lookup"><span data-stu-id="49378-374">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="49378-375">string</span><span class="sxs-lookup"><span data-stu-id="49378-375">string</span></span>|<span data-ttu-id="49378-376">64 символа</span><span class="sxs-lookup"><span data-stu-id="49378-376">64 characters</span></span>|<span data-ttu-id="49378-377">✔</span><span class="sxs-lookup"><span data-stu-id="49378-377">✔</span></span>|<span data-ttu-id="49378-378">Уникальный идентификатор соединителя, который соответствует ИДЕНТИФИКАТОРу в [панели мониторинга разработчика соединителей](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="49378-378">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="49378-379">компосикстенсионс</span><span class="sxs-lookup"><span data-stu-id="49378-379">composeExtensions</span></span>

<span data-ttu-id="49378-380">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="49378-380">**Optional** — array</span></span>

<span data-ttu-id="49378-381">Определяет расширение системы обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="49378-381">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="49378-382">Имя компонента изменилось с "расширение составления" на "расширение обмена сообщениями" в ноябре 2017, но имя манифеста остается без изменений, поэтому все существующие расширения продолжают работать.</span><span class="sxs-lookup"><span data-stu-id="49378-382">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="49378-383">Элемент является массивом (не более 1 элемента) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="49378-383">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="49378-384">Этот блок необходим только для решений, предоставляющих расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="49378-384">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="49378-385">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-385">Name</span></span>| <span data-ttu-id="49378-386">Тип</span><span class="sxs-lookup"><span data-stu-id="49378-386">Type</span></span> | <span data-ttu-id="49378-387">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-387">Maximum Size</span></span> | <span data-ttu-id="49378-388">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-388">Required</span></span> | <span data-ttu-id="49378-389">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-389">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="49378-390">string</span><span class="sxs-lookup"><span data-stu-id="49378-390">string</span></span>|<span data-ttu-id="49378-391">64</span><span class="sxs-lookup"><span data-stu-id="49378-391">64</span></span>|<span data-ttu-id="49378-392">✔</span><span class="sxs-lookup"><span data-stu-id="49378-392">✔</span></span>|<span data-ttu-id="49378-393">Уникальный идентификатор приложения для ленты, который выполняет резервное копирование расширения обмена сообщениями, как зарегистрировано в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="49378-393">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="49378-394">Это может быть так же, как и общий идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="49378-394">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="49378-395">массив объектов</span><span class="sxs-lookup"><span data-stu-id="49378-395">array of objects</span></span>|<span data-ttu-id="49378-396">10 </span><span class="sxs-lookup"><span data-stu-id="49378-396">10</span></span>|<span data-ttu-id="49378-397">✔</span><span class="sxs-lookup"><span data-stu-id="49378-397">✔</span></span>|<span data-ttu-id="49378-398">массив команд, поддерживающих расширение системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="49378-398">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="49378-399">boolean</span><span class="sxs-lookup"><span data-stu-id="49378-399">boolean</span></span>|||<span data-ttu-id="49378-400">Значение, указывающее, может ли пользователь изменять конфигурацию расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="49378-400">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="49378-401">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="49378-401">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="49378-402">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="49378-402">array of Objects</span></span>|<span data-ttu-id="49378-403">5 </span><span class="sxs-lookup"><span data-stu-id="49378-403">5</span></span>||<span data-ttu-id="49378-404">Список обработчиков, позволяющих вызывать приложения при выполнении определенных условий.</span><span class="sxs-lookup"><span data-stu-id="49378-404">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="49378-405">Домены также должны быть перечислены в`validDomains`</span><span class="sxs-lookup"><span data-stu-id="49378-405">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="49378-406">string</span><span class="sxs-lookup"><span data-stu-id="49378-406">string</span></span>|||<span data-ttu-id="49378-407">Тип обработчика сообщений.</span><span class="sxs-lookup"><span data-stu-id="49378-407">The type of message handler.</span></span> <span data-ttu-id="49378-408">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="49378-408">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="49378-409">Массив строк</span><span class="sxs-lookup"><span data-stu-id="49378-409">array of Strings</span></span>|||<span data-ttu-id="49378-410">массив доменов, для которых может регистрироваться обработчик сообщений ссылки.</span><span class="sxs-lookup"><span data-stu-id="49378-410">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="49378-411">Компосикстенсионс. Commands</span><span class="sxs-lookup"><span data-stu-id="49378-411">composeExtensions.commands</span></span>

<span data-ttu-id="49378-412">Ваш модуль обмена сообщениями должен объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="49378-412">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="49378-413">Каждая команда отображается в Microsoft Teams в качестве потенциального взаимодействия от точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="49378-413">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="49378-414">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="49378-414">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="49378-415">Каждый элемент команды представляет собой объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="49378-415">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="49378-416">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-416">Name</span></span>| <span data-ttu-id="49378-417">Тип</span><span class="sxs-lookup"><span data-stu-id="49378-417">Type</span></span>| <span data-ttu-id="49378-418">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-418">Maximum size</span></span> | <span data-ttu-id="49378-419">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-419">Required</span></span> | <span data-ttu-id="49378-420">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-420">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="49378-421">string</span><span class="sxs-lookup"><span data-stu-id="49378-421">string</span></span>|<span data-ttu-id="49378-422">64 символа</span><span class="sxs-lookup"><span data-stu-id="49378-422">64 characters</span></span>|<span data-ttu-id="49378-423">✔</span><span class="sxs-lookup"><span data-stu-id="49378-423">✔</span></span>|<span data-ttu-id="49378-424">Идентификатор команды.</span><span class="sxs-lookup"><span data-stu-id="49378-424">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="49378-425">string</span><span class="sxs-lookup"><span data-stu-id="49378-425">string</span></span>|<span data-ttu-id="49378-426">32 символов</span><span class="sxs-lookup"><span data-stu-id="49378-426">32 characters</span></span>|<span data-ttu-id="49378-427">✔</span><span class="sxs-lookup"><span data-stu-id="49378-427">✔</span></span>|<span data-ttu-id="49378-428">Понятное имя команды.</span><span class="sxs-lookup"><span data-stu-id="49378-428">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="49378-429">string</span><span class="sxs-lookup"><span data-stu-id="49378-429">string</span></span>|<span data-ttu-id="49378-430">64 символа</span><span class="sxs-lookup"><span data-stu-id="49378-430">64 characters</span></span>||<span data-ttu-id="49378-431">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="49378-431">Type of the command.</span></span> <span data-ttu-id="49378-432">Один из `query` или `action` .</span><span class="sxs-lookup"><span data-stu-id="49378-432">One of `query` or `action`.</span></span> <span data-ttu-id="49378-433">Значение по умолчанию: **Query**.</span><span class="sxs-lookup"><span data-stu-id="49378-433">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="49378-434">string</span><span class="sxs-lookup"><span data-stu-id="49378-434">string</span></span>|<span data-ttu-id="49378-435">128 символов</span><span class="sxs-lookup"><span data-stu-id="49378-435">128 characters</span></span>||<span data-ttu-id="49378-436">Описание, которое отображается для пользователей, чтобы указать назначение этой команды.</span><span class="sxs-lookup"><span data-stu-id="49378-436">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="49378-437">boolean</span><span class="sxs-lookup"><span data-stu-id="49378-437">boolean</span></span>|||<span data-ttu-id="49378-438">Логическое значение, которое указывает, следует ли выполнять команду изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="49378-438">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="49378-439">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="49378-439">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="49378-440">Массив строк</span><span class="sxs-lookup"><span data-stu-id="49378-440">array of Strings</span></span>|<span data-ttu-id="49378-441">3 </span><span class="sxs-lookup"><span data-stu-id="49378-441">3</span></span>||<span data-ttu-id="49378-442">Определяет, откуда можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="49378-442">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="49378-443">Любое сочетание `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="49378-443">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="49378-444">Значение по умолчанию: `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="49378-444">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="49378-445">boolean</span><span class="sxs-lookup"><span data-stu-id="49378-445">boolean</span></span>|||<span data-ttu-id="49378-446">Логическое значение, которое указывает, следует ли выполнять динамическое извлечение модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="49378-446">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="49378-447">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="49378-447">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="49378-448">объект</span><span class="sxs-lookup"><span data-stu-id="49378-448">object</span></span>|||<span data-ttu-id="49378-449">Укажите модуль задач для предварительной загрузки при использовании команды расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="49378-449">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="49378-450">string</span><span class="sxs-lookup"><span data-stu-id="49378-450">string</span></span>|<span data-ttu-id="49378-451">64 символа</span><span class="sxs-lookup"><span data-stu-id="49378-451">64 characters</span></span>||<span data-ttu-id="49378-452">Заголовок начального диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="49378-452">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="49378-453">string</span><span class="sxs-lookup"><span data-stu-id="49378-453">string</span></span>|||<span data-ttu-id="49378-454">Ширина диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый".</span><span class="sxs-lookup"><span data-stu-id="49378-454">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="49378-455">string</span><span class="sxs-lookup"><span data-stu-id="49378-455">string</span></span>|||<span data-ttu-id="49378-456">Высота диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый".</span><span class="sxs-lookup"><span data-stu-id="49378-456">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="49378-457">string</span><span class="sxs-lookup"><span data-stu-id="49378-457">string</span></span>|||<span data-ttu-id="49378-458">Исходный URL-адрес вебвиев.</span><span class="sxs-lookup"><span data-stu-id="49378-458">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="49378-459">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="49378-459">array of object</span></span>|<span data-ttu-id="49378-460">5 элементов</span><span class="sxs-lookup"><span data-stu-id="49378-460">5 items</span></span>|<span data-ttu-id="49378-461">✔</span><span class="sxs-lookup"><span data-stu-id="49378-461">✔</span></span>|<span data-ttu-id="49378-462">Список параметров, которые выполняет команда.</span><span class="sxs-lookup"><span data-stu-id="49378-462">The list of parameters the command takes.</span></span> <span data-ttu-id="49378-463">Минимум: 1; максимум: 5.</span><span class="sxs-lookup"><span data-stu-id="49378-463">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="49378-464">string</span><span class="sxs-lookup"><span data-stu-id="49378-464">string</span></span>|<span data-ttu-id="49378-465">64 символа</span><span class="sxs-lookup"><span data-stu-id="49378-465">64 characters</span></span>|<span data-ttu-id="49378-466">✔</span><span class="sxs-lookup"><span data-stu-id="49378-466">✔</span></span>|<span data-ttu-id="49378-467">Имя параметра в том виде, в котором оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="49378-467">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="49378-468">Он включен в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="49378-468">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="49378-469">string</span><span class="sxs-lookup"><span data-stu-id="49378-469">string</span></span>|<span data-ttu-id="49378-470">32 символов</span><span class="sxs-lookup"><span data-stu-id="49378-470">32 characters</span></span>|<span data-ttu-id="49378-471">✔</span><span class="sxs-lookup"><span data-stu-id="49378-471">✔</span></span>|<span data-ttu-id="49378-472">Удобное для пользователя название параметра.</span><span class="sxs-lookup"><span data-stu-id="49378-472">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="49378-473">string</span><span class="sxs-lookup"><span data-stu-id="49378-473">string</span></span>|<span data-ttu-id="49378-474">128 символов</span><span class="sxs-lookup"><span data-stu-id="49378-474">128 characters</span></span>||<span data-ttu-id="49378-475">Понятная пользователю строка, описывающая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="49378-475">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="49378-476">string</span><span class="sxs-lookup"><span data-stu-id="49378-476">string</span></span>|<span data-ttu-id="49378-477">512 символов</span><span class="sxs-lookup"><span data-stu-id="49378-477">512 characters</span></span>||<span data-ttu-id="49378-478">Начальное значение параметра.</span><span class="sxs-lookup"><span data-stu-id="49378-478">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="49378-479">string</span><span class="sxs-lookup"><span data-stu-id="49378-479">string</span></span>|<span data-ttu-id="49378-480">128 символов</span><span class="sxs-lookup"><span data-stu-id="49378-480">128 characters</span></span>||<span data-ttu-id="49378-481">Определяет тип элемента управления, отображаемого в модуле задачи для `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="49378-481">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="49378-482">Один из `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="49378-482">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="49378-483">массив объектов</span><span class="sxs-lookup"><span data-stu-id="49378-483">array of objects</span></span>|<span data-ttu-id="49378-484">10 элементов</span><span class="sxs-lookup"><span data-stu-id="49378-484">10 items</span></span>||<span data-ttu-id="49378-485">Варианты выбора для `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="49378-485">The choice options for the`choiceset`.</span></span> <span data-ttu-id="49378-486">Используйте только при `parameter.inputType` наличии `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="49378-486">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="49378-487">string</span><span class="sxs-lookup"><span data-stu-id="49378-487">string</span></span>|<span data-ttu-id="49378-488">128 символов</span><span class="sxs-lookup"><span data-stu-id="49378-488">128 characters</span></span>|<span data-ttu-id="49378-489">✔</span><span class="sxs-lookup"><span data-stu-id="49378-489">✔</span></span>|<span data-ttu-id="49378-490">Название выбора.</span><span class="sxs-lookup"><span data-stu-id="49378-490">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="49378-491">string</span><span class="sxs-lookup"><span data-stu-id="49378-491">string</span></span>|<span data-ttu-id="49378-492">512 символов</span><span class="sxs-lookup"><span data-stu-id="49378-492">512 characters</span></span>|<span data-ttu-id="49378-493">✔</span><span class="sxs-lookup"><span data-stu-id="49378-493">✔</span></span>|<span data-ttu-id="49378-494">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="49378-494">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="49378-495">permissions</span><span class="sxs-lookup"><span data-stu-id="49378-495">permissions</span></span>

<span data-ttu-id="49378-496">**Необязательное** — массив строк</span><span class="sxs-lookup"><span data-stu-id="49378-496">**Optional** — array of strings</span></span>

<span data-ttu-id="49378-497">Массив, `string` определяющий, какие разрешения запрашиваются приложением, что позволяет конечным пользователям знать, как будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="49378-497">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="49378-498">Следующие параметры неисключительны:</span><span class="sxs-lookup"><span data-stu-id="49378-498">The following options are non-exclusive:</span></span>

* <span data-ttu-id="49378-499">`identity`&emsp;Требуются сведения об удостоверении пользователя</span><span class="sxs-lookup"><span data-stu-id="49378-499">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="49378-500">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений участникам группы</span><span class="sxs-lookup"><span data-stu-id="49378-500">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="49378-501">Изменение этих разрешений при обновлении приложения приводит к тому, что пользователи будут повторять процесс разрешения при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="49378-501">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="49378-502">Дополнительные сведения см. [в разделе Обновление приложения](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) .</span><span class="sxs-lookup"><span data-stu-id="49378-502">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="49378-503">девицепермиссионс</span><span class="sxs-lookup"><span data-stu-id="49378-503">devicePermissions</span></span>

<span data-ttu-id="49378-504">**Необязательное** — массив строк</span><span class="sxs-lookup"><span data-stu-id="49378-504">**Optional** — array of strings</span></span>

<span data-ttu-id="49378-505">Указывает собственные функции на устройстве пользователя, к которым приложение может запрашивать доступ.</span><span class="sxs-lookup"><span data-stu-id="49378-505">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="49378-506">Возможные варианты:</span><span class="sxs-lookup"><span data-stu-id="49378-506">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="49378-507">валиддомаинс</span><span class="sxs-lookup"><span data-stu-id="49378-507">validDomains</span></span>

<span data-ttu-id="49378-508">**Необязательно**, за исключением **обязательного** места, где отмечено</span><span class="sxs-lookup"><span data-stu-id="49378-508">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="49378-509">Список допустимых доменов для веб-сайтов, которые приложение ожидает загружать в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="49378-509">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="49378-510">Примеры доменов могут включать подстановочные знаки `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="49378-510">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="49378-511">Это соответствует только одному сегменту домена; Если вам нужно использовать этот параметр `a.b.example.com` `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="49378-511">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="49378-512">Если конфигурация вкладки или контентный пользовательский интерфейс должны перейти к любому другому домену, Кроме того, что используется для настройки вкладок, этот домен необходимо указать здесь.</span><span class="sxs-lookup"><span data-stu-id="49378-512">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="49378-513">Тем не менее, **не** нужно включать домены поставщиков удостоверений, которые требуется поддерживать в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="49378-513">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="49378-514">Например, для проверки подлинности с помощью идентификатора Google необходимо перенаправить на accounts.google.com, но не следует включать accounts.google.com в `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="49378-514">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="49378-515">Приложения Teams, которым для правильной работы требуются собственные URL-адреса SharePoint, могут содержать "{теамситедомаин}" в допустимом списке доменов.</span><span class="sxs-lookup"><span data-stu-id="49378-515">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49378-516">Не добавляйте домены за предельный элемент управления (напрямую или с помощью подстановочных знаков).</span><span class="sxs-lookup"><span data-stu-id="49378-516">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="49378-517">Например, `yourapp.onmicrosoft.com` является допустимым, но `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="49378-517">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="49378-518">Объект является массивом со всеми элементами типа `string` .</span><span class="sxs-lookup"><span data-stu-id="49378-518">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="49378-519">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="49378-519">webApplicationInfo</span></span>

<span data-ttu-id="49378-520">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="49378-520">**Optional** — object</span></span>

<span data-ttu-id="49378-521">Указание идентификатора приложения и графического объекта AAD для упрощения входа пользователей в приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="49378-521">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="49378-522">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-522">Name</span></span>| <span data-ttu-id="49378-523">Тип</span><span class="sxs-lookup"><span data-stu-id="49378-523">Type</span></span>| <span data-ttu-id="49378-524">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-524">Maximum size</span></span> | <span data-ttu-id="49378-525">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-525">Required</span></span> | <span data-ttu-id="49378-526">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-526">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="49378-527">string</span><span class="sxs-lookup"><span data-stu-id="49378-527">string</span></span>|<span data-ttu-id="49378-528">36 символов</span><span class="sxs-lookup"><span data-stu-id="49378-528">36 characters</span></span>|<span data-ttu-id="49378-529">✔</span><span class="sxs-lookup"><span data-stu-id="49378-529">✔</span></span>|<span data-ttu-id="49378-530">Идентификатор приложения AAD приложения.</span><span class="sxs-lookup"><span data-stu-id="49378-530">AAD application id of the app.</span></span> <span data-ttu-id="49378-531">Этот идентификатор должен быть идентификатором GUID.</span><span class="sxs-lookup"><span data-stu-id="49378-531">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="49378-532">string</span><span class="sxs-lookup"><span data-stu-id="49378-532">string</span></span>|<span data-ttu-id="49378-533">2048 символов</span><span class="sxs-lookup"><span data-stu-id="49378-533">2048 characters</span></span>||<span data-ttu-id="49378-534">URL-адрес ресурса приложения для получения маркера проверки подлинности для единого входа.</span><span class="sxs-lookup"><span data-stu-id="49378-534">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="49378-535">массив строк</span><span class="sxs-lookup"><span data-stu-id="49378-535">array of strings</span></span>|<span data-ttu-id="49378-536">128 символов</span><span class="sxs-lookup"><span data-stu-id="49378-536">128 characters</span></span>||<span data-ttu-id="49378-537">Определение разрешения на уровне [отдельных ресурсов](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="49378-537">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="49378-538">шовлоадингиндикатор</span><span class="sxs-lookup"><span data-stu-id="49378-538">showLoadingIndicator</span></span>

<span data-ttu-id="49378-539">**Необязательный** — логический</span><span class="sxs-lookup"><span data-stu-id="49378-539">**Optional** — boolean</span></span>

<span data-ttu-id="49378-540">Указывает, где или не показывать индикатор загрузки при загрузке приложения или вкладки.</span><span class="sxs-lookup"><span data-stu-id="49378-540">Indicate where or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="49378-541">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="49378-541">Default: **false**.</span></span>

## <a name="isfullscreen"></a><span data-ttu-id="49378-542">в полноэкранном режим</span><span class="sxs-lookup"><span data-stu-id="49378-542">isFullScreen</span></span>

 <span data-ttu-id="49378-543">**Необязательный** — логический</span><span class="sxs-lookup"><span data-stu-id="49378-543">**Optional** — boolean</span></span>

<span data-ttu-id="49378-544">Указывает, где отображается личное приложение с панелью заголовков вкладок или без нее.</span><span class="sxs-lookup"><span data-stu-id="49378-544">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="49378-545">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="49378-545">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="49378-546">activities</span><span class="sxs-lookup"><span data-stu-id="49378-546">activities</span></span>

<span data-ttu-id="49378-547">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="49378-547">**Optional** — object</span></span>

<span data-ttu-id="49378-548">Определите свойства, которые ваше приложение будет использовать для публикации в канал активности пользователя.</span><span class="sxs-lookup"><span data-stu-id="49378-548">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="49378-549">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-549">Name</span></span>| <span data-ttu-id="49378-550">Тип</span><span class="sxs-lookup"><span data-stu-id="49378-550">Type</span></span>| <span data-ttu-id="49378-551">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-551">Maximum size</span></span> | <span data-ttu-id="49378-552">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-552">Required</span></span> | <span data-ttu-id="49378-553">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-553">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="49378-554">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="49378-554">array of Objects</span></span>|<span data-ttu-id="49378-555">128 элементов</span><span class="sxs-lookup"><span data-stu-id="49378-555">128 items</span></span>| | <span data-ttu-id="49378-556">Укажите типы действий, которые ваше приложение может отправлять в канал активности пользователей.</span><span class="sxs-lookup"><span data-stu-id="49378-556">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="49378-557">действия. Активититипес</span><span class="sxs-lookup"><span data-stu-id="49378-557">activities.activityTypes</span></span>

|<span data-ttu-id="49378-558">Имя</span><span class="sxs-lookup"><span data-stu-id="49378-558">Name</span></span>| <span data-ttu-id="49378-559">Тип</span><span class="sxs-lookup"><span data-stu-id="49378-559">Type</span></span>| <span data-ttu-id="49378-560">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="49378-560">Maximum size</span></span> | <span data-ttu-id="49378-561">Обязательный</span><span class="sxs-lookup"><span data-stu-id="49378-561">Required</span></span> | <span data-ttu-id="49378-562">Описание</span><span class="sxs-lookup"><span data-stu-id="49378-562">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="49378-563">string</span><span class="sxs-lookup"><span data-stu-id="49378-563">string</span></span>|<span data-ttu-id="49378-564">32 символов</span><span class="sxs-lookup"><span data-stu-id="49378-564">32 characters</span></span>|<span data-ttu-id="49378-565">✔</span><span class="sxs-lookup"><span data-stu-id="49378-565">✔</span></span>|<span data-ttu-id="49378-566">Тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="49378-566">The notification type.</span></span> <span data-ttu-id="49378-567">*Ознакомьтесь*с разделом ниже.</span><span class="sxs-lookup"><span data-stu-id="49378-567">*See below*.</span></span>|
|`description`|<span data-ttu-id="49378-568">string</span><span class="sxs-lookup"><span data-stu-id="49378-568">string</span></span>|<span data-ttu-id="49378-569">128 символов</span><span class="sxs-lookup"><span data-stu-id="49378-569">128 characters</span></span>|<span data-ttu-id="49378-570">✔</span><span class="sxs-lookup"><span data-stu-id="49378-570">✔</span></span>|<span data-ttu-id="49378-571">Краткое описание уведомления.</span><span class="sxs-lookup"><span data-stu-id="49378-571">A brief description of the notification.</span></span> <span data-ttu-id="49378-572">*Ознакомьтесь*с разделом ниже.</span><span class="sxs-lookup"><span data-stu-id="49378-572">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="49378-573">string</span><span class="sxs-lookup"><span data-stu-id="49378-573">string</span></span>|<span data-ttu-id="49378-574">128 символов</span><span class="sxs-lookup"><span data-stu-id="49378-574">128 characters</span></span>|<span data-ttu-id="49378-575">✔</span><span class="sxs-lookup"><span data-stu-id="49378-575">✔</span></span>|<span data-ttu-id="49378-576">Пример: "{Actor} создал задачу {taskId} для вас"</span><span class="sxs-lookup"><span data-stu-id="49378-576">Ex: "{actor} created task {taskId} for you"</span></span>|

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
