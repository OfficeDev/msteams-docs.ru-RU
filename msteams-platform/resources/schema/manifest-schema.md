---
title: Справочник по схеме манифеста
description: Описывает схему, поддерживаемую манифестом для Microsoft Teams.
keywords: Схема манифеста Teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: b514bbe8e04e674f5aafb3dff3acfe08072d814f
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452738"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="50435-104">Ссылка: схема манифеста для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="50435-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="50435-105">Манифест Microsoft Teams описывает, как приложение интегрируется в продукт Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="50435-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="50435-106">Манифест должен соответствовать схеме, размещенной в [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="50435-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="50435-107">Также поддерживаются предыдущие версии 1.0-1.6 (в URL-адресе используется "v1. x").</span><span class="sxs-lookup"><span data-stu-id="50435-107">Previous versions 1.0-1.6 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="50435-108">В приведенном ниже примере схемы показаны все варианты расширения.</span><span class="sxs-lookup"><span data-stu-id="50435-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="50435-109">Пример полного манифеста</span><span class="sxs-lookup"><span data-stu-id="50435-109">Sample full manifest</span></span>

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

<span data-ttu-id="50435-110">Схема определяет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="50435-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="50435-111">$schema</span><span class="sxs-lookup"><span data-stu-id="50435-111">$schema</span></span>

<span data-ttu-id="50435-112">*Необязательно, но рекомендуется* — строка</span><span class="sxs-lookup"><span data-stu-id="50435-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="50435-113">URL-адрес https://, ссылающийся на схему JSON для манифеста.</span><span class="sxs-lookup"><span data-stu-id="50435-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="50435-114">Версия манифеста</span><span class="sxs-lookup"><span data-stu-id="50435-114">manifestVersion</span></span>

<span data-ttu-id="50435-115">**Обязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="50435-115">**Required** — string</span></span>

<span data-ttu-id="50435-116">Версия схемы манифеста, используемая манифестом.</span><span class="sxs-lookup"><span data-stu-id="50435-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="50435-117">Он должен иметь значения "1,7".</span><span class="sxs-lookup"><span data-stu-id="50435-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="50435-118">version</span><span class="sxs-lookup"><span data-stu-id="50435-118">version</span></span>

<span data-ttu-id="50435-119">**Обязательный** — строка</span><span class="sxs-lookup"><span data-stu-id="50435-119">**Required** — string</span></span>

<span data-ttu-id="50435-120">Версия конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="50435-120">The version of the specific app.</span></span> <span data-ttu-id="50435-121">Если вы обновите какой-либо элемент в манифесте, необходимо также увеличить номер версии.</span><span class="sxs-lookup"><span data-stu-id="50435-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="50435-122">Благодаря этому при установке нового манифеста будет переписан существующий, а пользователь получит новые функции.</span><span class="sxs-lookup"><span data-stu-id="50435-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="50435-123">Если это приложение было отправлено в хранилище, новый манифест необходимо будет повторно отправить и проверить повторно.</span><span class="sxs-lookup"><span data-stu-id="50435-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="50435-124">После этого пользователи этого приложения автоматически получат новый обновленный манифест в течение нескольких часов после его утверждения.</span><span class="sxs-lookup"><span data-stu-id="50435-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="50435-125">Если приложение запросило изменение разрешений, пользователям будет предложено выполнить обновление и повторное согласие на доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="50435-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="50435-126">Эта строка версии должна соответствовать стандарту [semver](http://semver.org/) (Major. Значительные. PATCH).</span><span class="sxs-lookup"><span data-stu-id="50435-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="50435-127">id</span><span class="sxs-lookup"><span data-stu-id="50435-127">id</span></span>

<span data-ttu-id="50435-128">**Обязательный** — идентификатор приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="50435-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="50435-129">Уникальный идентификатор, созданный корпорацией Майкрософт для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="50435-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="50435-130">Если вы зарегистрировали Bot с помощью Microsoft Bot Framework, или веб-приложение вашей вкладки уже входит в Microsoft, у вас уже должен быть идентификатор, и его следует ввести здесь.</span><span class="sxs-lookup"><span data-stu-id="50435-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="50435-131">В противном случае необходимо создать новый идентификатор на портале регистрации приложений ([Мои приложения](https://apps.dev.microsoft.com)) Майкрософт, ввести его здесь, а затем повторно использовать его при добавлении ленты. Note: Если вы отправляете обновление существующему приложению в AppSource, идентификатор в манифесте не должен изменяться.</span><span class="sxs-lookup"><span data-stu-id="50435-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="50435-132">developer</span><span class="sxs-lookup"><span data-stu-id="50435-132">developer</span></span>

<span data-ttu-id="50435-133">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="50435-133">**Required** — object</span></span>

<span data-ttu-id="50435-134">Указывает сведения о компании.</span><span class="sxs-lookup"><span data-stu-id="50435-134">Specifies information about your company.</span></span> <span data-ttu-id="50435-135">Для приложений, отправляемых в AppSource (ранее — магазин Office), эти значения должны быть сопоставлены со сведениями в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="50435-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="50435-136">Ознакомьтесь с нашими [рекомендациями по публикации](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="50435-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="50435-137">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-137">Name</span></span>| <span data-ttu-id="50435-138">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-138">Maximum size</span></span> | <span data-ttu-id="50435-139">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-139">Required</span></span> | <span data-ttu-id="50435-140">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="50435-141">32 символов</span><span class="sxs-lookup"><span data-stu-id="50435-141">32 characters</span></span>|<span data-ttu-id="50435-142">✔</span><span class="sxs-lookup"><span data-stu-id="50435-142">✔</span></span>|<span data-ttu-id="50435-143">Отображаемое имя разработчика.</span><span class="sxs-lookup"><span data-stu-id="50435-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="50435-144">2048 символов</span><span class="sxs-lookup"><span data-stu-id="50435-144">2048 characters</span></span>|<span data-ttu-id="50435-145">✔</span><span class="sxs-lookup"><span data-stu-id="50435-145">✔</span></span>|<span data-ttu-id="50435-146">URL-адрес https://на веб-сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="50435-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="50435-147">Эта ссылка должна принять участие у пользователей в вашей компании или целевой странице для конкретного продукта.</span><span class="sxs-lookup"><span data-stu-id="50435-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="50435-148">2048 символов</span><span class="sxs-lookup"><span data-stu-id="50435-148">2048 characters</span></span>|<span data-ttu-id="50435-149">✔</span><span class="sxs-lookup"><span data-stu-id="50435-149">✔</span></span>|<span data-ttu-id="50435-150">URL-адрес https://для политики конфиденциальности разработчика.</span><span class="sxs-lookup"><span data-stu-id="50435-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="50435-151">2048 символов</span><span class="sxs-lookup"><span data-stu-id="50435-151">2048 characters</span></span>|<span data-ttu-id="50435-152">✔</span><span class="sxs-lookup"><span data-stu-id="50435-152">✔</span></span>|<span data-ttu-id="50435-153">URL-адрес https://для условий использования разработчиком.</span><span class="sxs-lookup"><span data-stu-id="50435-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="50435-154">10 символов</span><span class="sxs-lookup"><span data-stu-id="50435-154">10 characters</span></span>| |<span data-ttu-id="50435-155">**Необязательное требование** Идентификатор сети партнера Майкрософт, определяющий партнерскую организацию, которая создает приложение.</span><span class="sxs-lookup"><span data-stu-id="50435-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="50435-156">name</span><span class="sxs-lookup"><span data-stu-id="50435-156">name</span></span>

<span data-ttu-id="50435-157">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="50435-157">**Required** — object</span></span>

<span data-ttu-id="50435-158">Имя приложения, отображаемое для пользователей в интерфейсе Teams.</span><span class="sxs-lookup"><span data-stu-id="50435-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="50435-159">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="50435-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="50435-160">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="50435-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="50435-161">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-161">Name</span></span>| <span data-ttu-id="50435-162">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-162">Maximum size</span></span> | <span data-ttu-id="50435-163">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-163">Required</span></span> | <span data-ttu-id="50435-164">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="50435-165">30 символов</span><span class="sxs-lookup"><span data-stu-id="50435-165">30 characters</span></span>|<span data-ttu-id="50435-166">✔</span><span class="sxs-lookup"><span data-stu-id="50435-166">✔</span></span>|<span data-ttu-id="50435-167">Краткое отображаемое имя приложения.</span><span class="sxs-lookup"><span data-stu-id="50435-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="50435-168">100 символов</span><span class="sxs-lookup"><span data-stu-id="50435-168">100 characters</span></span>||<span data-ttu-id="50435-169">Полное имя приложения, используемое, если имя полного приложения превышает 30 символов.</span><span class="sxs-lookup"><span data-stu-id="50435-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="50435-170">description</span><span class="sxs-lookup"><span data-stu-id="50435-170">description</span></span>

<span data-ttu-id="50435-171">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="50435-171">**Required** — object</span></span>

<span data-ttu-id="50435-172">Описывает приложение для пользователей.</span><span class="sxs-lookup"><span data-stu-id="50435-172">Describes your app to users.</span></span> <span data-ttu-id="50435-173">Для приложений, отправляемых в AppSource, эти значения должны быть соответствующими сведениям в записи AppSource.</span><span class="sxs-lookup"><span data-stu-id="50435-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="50435-174">Убедитесь, что ваше описание точно описывает ваш интерфейс и предоставляет сведения, помогающие потенциальным клиентам определить, что делает ваш интерфейс.</span><span class="sxs-lookup"><span data-stu-id="50435-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="50435-175">Кроме того, в полном описании следует отметить, если для использования требуется внешняя учетная запись.</span><span class="sxs-lookup"><span data-stu-id="50435-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="50435-176">Значения `short` и `full` не должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="50435-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="50435-177">Краткое описание не должно повторяться в длинном описании и не должно включать имя другого приложения.</span><span class="sxs-lookup"><span data-stu-id="50435-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="50435-178">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-178">Name</span></span>| <span data-ttu-id="50435-179">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-179">Maximum size</span></span> | <span data-ttu-id="50435-180">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-180">Required</span></span> | <span data-ttu-id="50435-181">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="50435-182">80 символов</span><span class="sxs-lookup"><span data-stu-id="50435-182">80 characters</span></span>|<span data-ttu-id="50435-183">✔</span><span class="sxs-lookup"><span data-stu-id="50435-183">✔</span></span>|<span data-ttu-id="50435-184">Краткое описание интерфейса приложения, используемое при ограниченном пространстве.</span><span class="sxs-lookup"><span data-stu-id="50435-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="50435-185">4000 символов</span><span class="sxs-lookup"><span data-stu-id="50435-185">4000 characters</span></span>|<span data-ttu-id="50435-186">✔</span><span class="sxs-lookup"><span data-stu-id="50435-186">✔</span></span>|<span data-ttu-id="50435-187">Полное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="50435-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="50435-188">паккаженаме</span><span class="sxs-lookup"><span data-stu-id="50435-188">packageName</span></span>

<span data-ttu-id="50435-189">**Необязательное** — строка</span><span class="sxs-lookup"><span data-stu-id="50435-189">**Optional** — string</span></span>

<span data-ttu-id="50435-190">Уникальный идентификатор для этого приложения в обратной нотации домена; Пример: com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="50435-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="50435-191">Максимальная длина: 64 символа.</span><span class="sxs-lookup"><span data-stu-id="50435-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="50435-192">локализатионинфо</span><span class="sxs-lookup"><span data-stu-id="50435-192">localizationInfo</span></span>

<span data-ttu-id="50435-193">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="50435-193">**Optional** — object</span></span>

<span data-ttu-id="50435-194">Разрешает спецификацию языка по умолчанию, а также указателей на дополнительные языковые файлы.</span><span class="sxs-lookup"><span data-stu-id="50435-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="50435-195">См.: [Локализация](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="50435-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="50435-196">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-196">Name</span></span>| <span data-ttu-id="50435-197">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-197">Maximum size</span></span> | <span data-ttu-id="50435-198">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-198">Required</span></span> | <span data-ttu-id="50435-199">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="50435-200">✔</span><span class="sxs-lookup"><span data-stu-id="50435-200">✔</span></span>|<span data-ttu-id="50435-201">Тег языка строк в этом файле манифеста верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="50435-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="50435-202">Локализатионинфо. Аддитионаллангуажес</span><span class="sxs-lookup"><span data-stu-id="50435-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="50435-203">Массив объектов, задающий дополнительные языковые переводы.</span><span class="sxs-lookup"><span data-stu-id="50435-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="50435-204">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-204">Name</span></span>| <span data-ttu-id="50435-205">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-205">Maximum size</span></span> | <span data-ttu-id="50435-206">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-206">Required</span></span> | <span data-ttu-id="50435-207">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="50435-208">✔</span><span class="sxs-lookup"><span data-stu-id="50435-208">✔</span></span>|<span data-ttu-id="50435-209">Тег языка строк в указанном файле.</span><span class="sxs-lookup"><span data-stu-id="50435-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="50435-210">✔</span><span class="sxs-lookup"><span data-stu-id="50435-210">✔</span></span>|<span data-ttu-id="50435-211">Относительный путь к файлу. JSON, содержащему переведенные строки.</span><span class="sxs-lookup"><span data-stu-id="50435-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="50435-212">icons</span><span class="sxs-lookup"><span data-stu-id="50435-212">icons</span></span>

<span data-ttu-id="50435-213">**Обязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="50435-213">**Required** — object</span></span>

<span data-ttu-id="50435-214">Значки, используемые в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="50435-214">Icons used within the Teams app.</span></span> <span data-ttu-id="50435-215">Файлы значков должны быть включены в состав пакета отправки.</span><span class="sxs-lookup"><span data-stu-id="50435-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="50435-216">Дополнительные сведения можно найти в разделе [значки](~/concepts/build-and-test/apps-package.md#icons) .</span><span class="sxs-lookup"><span data-stu-id="50435-216">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="50435-217">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-217">Name</span></span>| <span data-ttu-id="50435-218">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-218">Maximum size</span></span> | <span data-ttu-id="50435-219">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-219">Required</span></span> | <span data-ttu-id="50435-220">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="50435-221">32 x 32 пикселей</span><span class="sxs-lookup"><span data-stu-id="50435-221">32 x 32 pixels</span></span>|<span data-ttu-id="50435-222">✔</span><span class="sxs-lookup"><span data-stu-id="50435-222">✔</span></span>|<span data-ttu-id="50435-223">Относительный путь к файлу с прозрачным значком изображения в формате 32x32 PNG.</span><span class="sxs-lookup"><span data-stu-id="50435-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="50435-224">192 x 192 пикселей</span><span class="sxs-lookup"><span data-stu-id="50435-224">192 x 192 pixels</span></span>|<span data-ttu-id="50435-225">✔</span><span class="sxs-lookup"><span data-stu-id="50435-225">✔</span></span>|<span data-ttu-id="50435-226">Относительный путь к файлу полного цветового значка PNG 192x192.</span><span class="sxs-lookup"><span data-stu-id="50435-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="50435-227">акцентколор</span><span class="sxs-lookup"><span data-stu-id="50435-227">accentColor</span></span>

<span data-ttu-id="50435-228">**Необязательное** — шестнадцатеричный код цвета HTML</span><span class="sxs-lookup"><span data-stu-id="50435-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="50435-229">Цвет, используемый в сочетании с фоном для значков структуры.</span><span class="sxs-lookup"><span data-stu-id="50435-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="50435-230">Значение должно быть допустимым цветом HTML-кода, начинающимся с "#", например `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="50435-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="50435-231">конфигураблетабс</span><span class="sxs-lookup"><span data-stu-id="50435-231">configurableTabs</span></span>

<span data-ttu-id="50435-232">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="50435-232">**Optional** — array</span></span>

<span data-ttu-id="50435-233">Используется, когда у вашего приложения есть вкладка "канал группы", требующая дополнительной настройки перед добавлением.</span><span class="sxs-lookup"><span data-stu-id="50435-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="50435-234">Настраиваемые вкладки поддерживаются только в области Teams (не личное), и в настоящее время поддерживается только **одна** вкладка на приложение.</span><span class="sxs-lookup"><span data-stu-id="50435-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="50435-235">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-235">Name</span></span>| <span data-ttu-id="50435-236">Тип</span><span class="sxs-lookup"><span data-stu-id="50435-236">Type</span></span>| <span data-ttu-id="50435-237">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-237">Maximum size</span></span> | <span data-ttu-id="50435-238">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-238">Required</span></span> | <span data-ttu-id="50435-239">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="50435-240">string</span><span class="sxs-lookup"><span data-stu-id="50435-240">string</span></span>|<span data-ttu-id="50435-241">2048 символов</span><span class="sxs-lookup"><span data-stu-id="50435-241">2048 characters</span></span>|<span data-ttu-id="50435-242">✔</span><span class="sxs-lookup"><span data-stu-id="50435-242">✔</span></span>|<span data-ttu-id="50435-243">URL-адрес https://, используемый при настройке вкладки.</span><span class="sxs-lookup"><span data-stu-id="50435-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="50435-244">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="50435-244">array of enum</span></span>|<span data-ttu-id="50435-245">1,1</span><span class="sxs-lookup"><span data-stu-id="50435-245">1</span></span>|<span data-ttu-id="50435-246">✔</span><span class="sxs-lookup"><span data-stu-id="50435-246">✔</span></span>|<span data-ttu-id="50435-247">В настоящее время настраиваемые вкладки поддерживают только `team` области и `groupchat` области.</span><span class="sxs-lookup"><span data-stu-id="50435-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="50435-248">boolean</span><span class="sxs-lookup"><span data-stu-id="50435-248">boolean</span></span>|||<span data-ttu-id="50435-249">Значение, указывающее, может ли пользователь обновлять экземпляр конфигурации вкладки после создания.</span><span class="sxs-lookup"><span data-stu-id="50435-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="50435-250">Значение по умолчанию: **true**.</span><span class="sxs-lookup"><span data-stu-id="50435-250">Default: **true**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="50435-251">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-251">string</span></span>|<span data-ttu-id="50435-252">2048</span><span class="sxs-lookup"><span data-stu-id="50435-252">2048</span></span>||<span data-ttu-id="50435-253">Относительный путь к изображению вкладки для использования в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="50435-253">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="50435-254">Размер 1024x768.</span><span class="sxs-lookup"><span data-stu-id="50435-254">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="50435-255">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="50435-255">array of enum</span></span>|<span data-ttu-id="50435-256">1,1</span><span class="sxs-lookup"><span data-stu-id="50435-256">1</span></span>||<span data-ttu-id="50435-257">Определяет, как будет предоставляться вкладка в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="50435-257">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="50435-258">Параметры `sharePointFullPage``sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="50435-258">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="50435-259">статиктабс</span><span class="sxs-lookup"><span data-stu-id="50435-259">staticTabs</span></span>

<span data-ttu-id="50435-260">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="50435-260">**Optional** — array</span></span>

<span data-ttu-id="50435-261">Определяет набор вкладок, которые по умолчанию можно закреплять, не добавляя пользователей вручную.</span><span class="sxs-lookup"><span data-stu-id="50435-261">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="50435-262">Статические вкладки, объявляемые в `personal` области, всегда фиксируются в личном интерфейсе приложения.</span><span class="sxs-lookup"><span data-stu-id="50435-262">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="50435-263">Статические вкладки, объявленные в `team` области, в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="50435-263">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="50435-264">Этот элемент является массивом (не более 16 элементов) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="50435-264">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="50435-265">Этот блок необходим только для решений, предоставляющих статическое решение для вкладок.</span><span class="sxs-lookup"><span data-stu-id="50435-265">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="50435-266">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-266">Name</span></span>| <span data-ttu-id="50435-267">Тип</span><span class="sxs-lookup"><span data-stu-id="50435-267">Type</span></span>| <span data-ttu-id="50435-268">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-268">Maximum size</span></span> | <span data-ttu-id="50435-269">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-269">Required</span></span> | <span data-ttu-id="50435-270">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-270">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="50435-271">string</span><span class="sxs-lookup"><span data-stu-id="50435-271">string</span></span>|<span data-ttu-id="50435-272">64 символа</span><span class="sxs-lookup"><span data-stu-id="50435-272">64 characters</span></span>|<span data-ttu-id="50435-273">✔</span><span class="sxs-lookup"><span data-stu-id="50435-273">✔</span></span>|<span data-ttu-id="50435-274">Уникальный идентификатор объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="50435-274">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="50435-275">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-275">string</span></span>|<span data-ttu-id="50435-276">128 символов</span><span class="sxs-lookup"><span data-stu-id="50435-276">128 characters</span></span>|<span data-ttu-id="50435-277">✔</span><span class="sxs-lookup"><span data-stu-id="50435-277">✔</span></span>|<span data-ttu-id="50435-278">Отображаемое имя вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="50435-278">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="50435-279">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-279">string</span></span>|<span data-ttu-id="50435-280">2048 символов</span><span class="sxs-lookup"><span data-stu-id="50435-280">2048 characters</span></span>|<span data-ttu-id="50435-281">✔</span><span class="sxs-lookup"><span data-stu-id="50435-281">✔</span></span>|<span data-ttu-id="50435-282">URL-адрес https://, указывающий на пользовательский интерфейс сущности, который будет отображаться в полотне Teams.</span><span class="sxs-lookup"><span data-stu-id="50435-282">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="50435-283">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-283">string</span></span>|<span data-ttu-id="50435-284">2048 символов</span><span class="sxs-lookup"><span data-stu-id="50435-284">2048 characters</span></span>||<span data-ttu-id="50435-285">URL-адрес https://, указывающий, когда пользователь попытается просмотреть его в браузере.</span><span class="sxs-lookup"><span data-stu-id="50435-285">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="50435-286">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="50435-286">array of enum</span></span>|<span data-ttu-id="50435-287">1,1</span><span class="sxs-lookup"><span data-stu-id="50435-287">1</span></span>|<span data-ttu-id="50435-288">✔</span><span class="sxs-lookup"><span data-stu-id="50435-288">✔</span></span>|<span data-ttu-id="50435-289">В настоящее время статические вкладки поддерживают только `personal` область, что означает, что ее можно подготовить только в рамках личного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="50435-289">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

> [!NOTE]
> <span data-ttu-id="50435-290">Если на вкладках требуются контекстно зависимые сведения для отображения релевантного контента или для инициализации процесса проверки подлинности, *обратитесь к разделу* [Получение контекста для вкладки Microsoft Teams](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="50435-290">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="50435-291">Боты</span><span class="sxs-lookup"><span data-stu-id="50435-291">bots</span></span>

<span data-ttu-id="50435-292">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="50435-292">**Optional** — array</span></span>

<span data-ttu-id="50435-293">Определяет одноэлементное решение, а также дополнительные сведения, такие как свойства команды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="50435-293">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="50435-294">Элемент является массивом ( &mdash; в настоящее время для каждого приложения допускается только один элемент "bot" для каждого приложения) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="50435-294">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="50435-295">Этот блок необходим только для решений, предоставляющих интерфейс Bot.</span><span class="sxs-lookup"><span data-stu-id="50435-295">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="50435-296">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-296">Name</span></span>| <span data-ttu-id="50435-297">Тип</span><span class="sxs-lookup"><span data-stu-id="50435-297">Type</span></span>| <span data-ttu-id="50435-298">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-298">Maximum size</span></span> | <span data-ttu-id="50435-299">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-299">Required</span></span> | <span data-ttu-id="50435-300">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-300">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="50435-301">string</span><span class="sxs-lookup"><span data-stu-id="50435-301">string</span></span>|<span data-ttu-id="50435-302">64 символа</span><span class="sxs-lookup"><span data-stu-id="50435-302">64 characters</span></span>|<span data-ttu-id="50435-303">✔</span><span class="sxs-lookup"><span data-stu-id="50435-303">✔</span></span>|<span data-ttu-id="50435-304">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="50435-304">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="50435-305">Это может быть так же, как и общий [идентификатор приложения](#id).</span><span class="sxs-lookup"><span data-stu-id="50435-305">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="50435-306">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="50435-306">array of enum</span></span>|<span data-ttu-id="50435-307">4</span><span class="sxs-lookup"><span data-stu-id="50435-307">3</span></span>|<span data-ttu-id="50435-308">✔</span><span class="sxs-lookup"><span data-stu-id="50435-308">✔</span></span>|<span data-ttu-id="50435-309">Указывает, предлагает ли бот функции в контексте канала в `team`, в групповом чате (`groupchat`) или функции, ограниченные только отдельным пользователем (`personal`).</span><span class="sxs-lookup"><span data-stu-id="50435-309">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="50435-310">Эти параметры не являются исключающими.</span><span class="sxs-lookup"><span data-stu-id="50435-310">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="50435-311">boolean</span><span class="sxs-lookup"><span data-stu-id="50435-311">boolean</span></span>|||<span data-ttu-id="50435-312">Описывает, использует ли бот пользовательское указание для добавления бота в определенный канал.</span><span class="sxs-lookup"><span data-stu-id="50435-312">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="50435-313">Умолчани **`false`**</span><span class="sxs-lookup"><span data-stu-id="50435-313">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="50435-314">boolean</span><span class="sxs-lookup"><span data-stu-id="50435-314">boolean</span></span>|||<span data-ttu-id="50435-315">Указывает, является ли бот односторонним и только для уведомлений, в отличие от бота для беседы.</span><span class="sxs-lookup"><span data-stu-id="50435-315">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="50435-316">Умолчани `**false**`</span><span class="sxs-lookup"><span data-stu-id="50435-316">Default: `**false**`</span></span>|
|`supportsFiles`|<span data-ttu-id="50435-317">boolean</span><span class="sxs-lookup"><span data-stu-id="50435-317">boolean</span></span>|||<span data-ttu-id="50435-318">Указывает, поддерживает ли бот возможность отправки и скачивания файлов в личном чате.</span><span class="sxs-lookup"><span data-stu-id="50435-318">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="50435-319">Умолчани **`false`**</span><span class="sxs-lookup"><span data-stu-id="50435-319">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="50435-320">Боты. Коммандлистс</span><span class="sxs-lookup"><span data-stu-id="50435-320">bots.commandLists</span></span>

<span data-ttu-id="50435-321">Необязательный список команд, которые ваш робот может рекомендовать пользователям.</span><span class="sxs-lookup"><span data-stu-id="50435-321">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="50435-322">Объект является массивом (не более 2 элементов) со всеми элементами типа `object` ; необходимо определить отдельный список команд для каждой области, которую поддерживает Bot.</span><span class="sxs-lookup"><span data-stu-id="50435-322">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="50435-323">Дополнительные сведения содержатся в [меню Bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="50435-323">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="50435-324">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-324">Name</span></span>| <span data-ttu-id="50435-325">Тип</span><span class="sxs-lookup"><span data-stu-id="50435-325">Type</span></span>| <span data-ttu-id="50435-326">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-326">Maximum size</span></span> | <span data-ttu-id="50435-327">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-327">Required</span></span> | <span data-ttu-id="50435-328">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-328">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="50435-329">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="50435-329">array of enum</span></span>|<span data-ttu-id="50435-330">4</span><span class="sxs-lookup"><span data-stu-id="50435-330">3</span></span>|<span data-ttu-id="50435-331">✔</span><span class="sxs-lookup"><span data-stu-id="50435-331">✔</span></span>|<span data-ttu-id="50435-332">Указывает область, для которой действует список команд.</span><span class="sxs-lookup"><span data-stu-id="50435-332">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="50435-333">Возможны значения `team`, `personal` и `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="50435-333">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="50435-334">массив объектов</span><span class="sxs-lookup"><span data-stu-id="50435-334">array of objects</span></span>|<span data-ttu-id="50435-335">10 </span><span class="sxs-lookup"><span data-stu-id="50435-335">10</span></span>|<span data-ttu-id="50435-336">✔</span><span class="sxs-lookup"><span data-stu-id="50435-336">✔</span></span>|<span data-ttu-id="50435-337">Массив команд, поддерживаемых ботом:</span><span class="sxs-lookup"><span data-stu-id="50435-337">An array of commands the bot supports:</span></span><br><span data-ttu-id="50435-338">`title`: имя команды бота (строка, 32)</span><span class="sxs-lookup"><span data-stu-id="50435-338">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="50435-339">`description`: простое описание или пример синтаксиса команды и ее аргумента (строка, 128)</span><span class="sxs-lookup"><span data-stu-id="50435-339">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="50435-340">Боты. Коммандлистс. Commands</span><span class="sxs-lookup"><span data-stu-id="50435-340">bots.commandLists.commands</span></span>

|<span data-ttu-id="50435-341">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-341">Name</span></span>| <span data-ttu-id="50435-342">Тип</span><span class="sxs-lookup"><span data-stu-id="50435-342">Type</span></span>| <span data-ttu-id="50435-343">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-343">Maximum size</span></span> | <span data-ttu-id="50435-344">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-344">Required</span></span> | <span data-ttu-id="50435-345">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-345">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="50435-346">title</span><span class="sxs-lookup"><span data-stu-id="50435-346">title</span></span>|<span data-ttu-id="50435-347">string</span><span class="sxs-lookup"><span data-stu-id="50435-347">string</span></span>|<span data-ttu-id="50435-348">12 </span><span class="sxs-lookup"><span data-stu-id="50435-348">12</span></span>|<span data-ttu-id="50435-349">✔</span><span class="sxs-lookup"><span data-stu-id="50435-349">✔</span></span>|<span data-ttu-id="50435-350">Имя команды Bot</span><span class="sxs-lookup"><span data-stu-id="50435-350">The bot command name</span></span>|
|<span data-ttu-id="50435-351">description</span><span class="sxs-lookup"><span data-stu-id="50435-351">description</span></span>|<span data-ttu-id="50435-352">string</span><span class="sxs-lookup"><span data-stu-id="50435-352">string</span></span>|<span data-ttu-id="50435-353">128 символов</span><span class="sxs-lookup"><span data-stu-id="50435-353">128 characters</span></span>|<span data-ttu-id="50435-354">✔</span><span class="sxs-lookup"><span data-stu-id="50435-354">✔</span></span>|<span data-ttu-id="50435-355">Простое текстовое описание или пример синтаксиса команды и его аргументов.</span><span class="sxs-lookup"><span data-stu-id="50435-355">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="50435-356">аудиовыход</span><span class="sxs-lookup"><span data-stu-id="50435-356">connectors</span></span>

<span data-ttu-id="50435-357">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="50435-357">**Optional** — array</span></span>

<span data-ttu-id="50435-358">`connectors`Блок определяет соединитель Office 365 для приложения.</span><span class="sxs-lookup"><span data-stu-id="50435-358">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="50435-359">Объект является массивом (не более 1 элемента) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="50435-359">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="50435-360">Этот блок необходим только для решений, предоставляющих соединитель.</span><span class="sxs-lookup"><span data-stu-id="50435-360">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="50435-361">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-361">Name</span></span>| <span data-ttu-id="50435-362">Тип</span><span class="sxs-lookup"><span data-stu-id="50435-362">Type</span></span>| <span data-ttu-id="50435-363">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-363">Maximum size</span></span> | <span data-ttu-id="50435-364">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-364">Required</span></span> | <span data-ttu-id="50435-365">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-365">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="50435-366">string</span><span class="sxs-lookup"><span data-stu-id="50435-366">string</span></span>|<span data-ttu-id="50435-367">2048 символов</span><span class="sxs-lookup"><span data-stu-id="50435-367">2048 characters</span></span>|<span data-ttu-id="50435-368">✔</span><span class="sxs-lookup"><span data-stu-id="50435-368">✔</span></span>|<span data-ttu-id="50435-369">URL-адрес https://, используемый при настройке соединителя.</span><span class="sxs-lookup"><span data-stu-id="50435-369">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="50435-370">массив перечислений</span><span class="sxs-lookup"><span data-stu-id="50435-370">array of enum</span></span>|<span data-ttu-id="50435-371">1,1</span><span class="sxs-lookup"><span data-stu-id="50435-371">1</span></span>|<span data-ttu-id="50435-372">✔</span><span class="sxs-lookup"><span data-stu-id="50435-372">✔</span></span>|<span data-ttu-id="50435-373">Указывает, будет ли соединитель работать в контексте канала в `team` или в интерфейсе для отдельного пользователя ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="50435-373">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="50435-374">В настоящее время `team` поддерживается только область действия.</span><span class="sxs-lookup"><span data-stu-id="50435-374">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="50435-375">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-375">string</span></span>|<span data-ttu-id="50435-376">64 символа</span><span class="sxs-lookup"><span data-stu-id="50435-376">64 characters</span></span>|<span data-ttu-id="50435-377">✔</span><span class="sxs-lookup"><span data-stu-id="50435-377">✔</span></span>|<span data-ttu-id="50435-378">Уникальный идентификатор соединителя, который соответствует ИДЕНТИФИКАТОРу в [панели мониторинга разработчика соединителей](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="50435-378">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="50435-379">компосикстенсионс</span><span class="sxs-lookup"><span data-stu-id="50435-379">composeExtensions</span></span>

<span data-ttu-id="50435-380">**Необязательный** — массив</span><span class="sxs-lookup"><span data-stu-id="50435-380">**Optional** — array</span></span>

<span data-ttu-id="50435-381">Определяет расширение системы обмена сообщениями для приложения.</span><span class="sxs-lookup"><span data-stu-id="50435-381">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="50435-382">Имя компонента изменилось с "расширение составления" на "расширение обмена сообщениями" в ноябре 2017, но имя манифеста остается без изменений, поэтому все существующие расширения продолжают работать.</span><span class="sxs-lookup"><span data-stu-id="50435-382">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="50435-383">Элемент является массивом (не более 1 элемента) со всеми элементами типа `object` .</span><span class="sxs-lookup"><span data-stu-id="50435-383">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="50435-384">Этот блок необходим только для решений, предоставляющих расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="50435-384">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="50435-385">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-385">Name</span></span>| <span data-ttu-id="50435-386">Тип</span><span class="sxs-lookup"><span data-stu-id="50435-386">Type</span></span> | <span data-ttu-id="50435-387">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-387">Maximum Size</span></span> | <span data-ttu-id="50435-388">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-388">Required</span></span> | <span data-ttu-id="50435-389">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-389">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="50435-390">string</span><span class="sxs-lookup"><span data-stu-id="50435-390">string</span></span>|<span data-ttu-id="50435-391">64</span><span class="sxs-lookup"><span data-stu-id="50435-391">64</span></span>|<span data-ttu-id="50435-392">✔</span><span class="sxs-lookup"><span data-stu-id="50435-392">✔</span></span>|<span data-ttu-id="50435-393">Уникальный идентификатор приложения для ленты, который выполняет резервное копирование расширения обмена сообщениями, как зарегистрировано в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="50435-393">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="50435-394">Это может быть так же, как и общий идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="50435-394">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="50435-395">массив объектов</span><span class="sxs-lookup"><span data-stu-id="50435-395">array of objects</span></span>|<span data-ttu-id="50435-396">10 </span><span class="sxs-lookup"><span data-stu-id="50435-396">10</span></span>|<span data-ttu-id="50435-397">✔</span><span class="sxs-lookup"><span data-stu-id="50435-397">✔</span></span>|<span data-ttu-id="50435-398">массив команд, поддерживающих расширение системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="50435-398">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="50435-399">boolean</span><span class="sxs-lookup"><span data-stu-id="50435-399">boolean</span></span>|||<span data-ttu-id="50435-400">Значение, указывающее, может ли пользователь изменять конфигурацию расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="50435-400">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="50435-401">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="50435-401">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="50435-402">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="50435-402">array of Objects</span></span>|<span data-ttu-id="50435-403">5 </span><span class="sxs-lookup"><span data-stu-id="50435-403">5</span></span>||<span data-ttu-id="50435-404">Список обработчиков, позволяющих вызывать приложения при выполнении определенных условий.</span><span class="sxs-lookup"><span data-stu-id="50435-404">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="50435-405">Домены также должны быть перечислены в `validDomains`</span><span class="sxs-lookup"><span data-stu-id="50435-405">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="50435-406">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-406">string</span></span>|||<span data-ttu-id="50435-407">Тип обработчика сообщений.</span><span class="sxs-lookup"><span data-stu-id="50435-407">The type of message handler.</span></span> <span data-ttu-id="50435-408">Должно быть задано значение `"link"`.</span><span class="sxs-lookup"><span data-stu-id="50435-408">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="50435-409">Массив строк</span><span class="sxs-lookup"><span data-stu-id="50435-409">array of Strings</span></span>|||<span data-ttu-id="50435-410">массив доменов, для которых может регистрироваться обработчик сообщений ссылки.</span><span class="sxs-lookup"><span data-stu-id="50435-410">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="50435-411">Компосикстенсионс. Commands</span><span class="sxs-lookup"><span data-stu-id="50435-411">composeExtensions.commands</span></span>

<span data-ttu-id="50435-412">Ваш модуль обмена сообщениями должен объявить одну или несколько команд.</span><span class="sxs-lookup"><span data-stu-id="50435-412">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="50435-413">Каждая команда отображается в Microsoft Teams в качестве потенциального взаимодействия от точки входа на основе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="50435-413">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="50435-414">Существует не более 10 команд.</span><span class="sxs-lookup"><span data-stu-id="50435-414">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="50435-415">Каждый элемент команды представляет собой объект со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="50435-415">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="50435-416">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-416">Name</span></span>| <span data-ttu-id="50435-417">Тип</span><span class="sxs-lookup"><span data-stu-id="50435-417">Type</span></span>| <span data-ttu-id="50435-418">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-418">Maximum size</span></span> | <span data-ttu-id="50435-419">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-419">Required</span></span> | <span data-ttu-id="50435-420">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-420">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="50435-421">string</span><span class="sxs-lookup"><span data-stu-id="50435-421">string</span></span>|<span data-ttu-id="50435-422">64 символа</span><span class="sxs-lookup"><span data-stu-id="50435-422">64 characters</span></span>|<span data-ttu-id="50435-423">✔</span><span class="sxs-lookup"><span data-stu-id="50435-423">✔</span></span>|<span data-ttu-id="50435-424">Идентификатор команды.</span><span class="sxs-lookup"><span data-stu-id="50435-424">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="50435-425">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-425">string</span></span>|<span data-ttu-id="50435-426">32 символов</span><span class="sxs-lookup"><span data-stu-id="50435-426">32 characters</span></span>|<span data-ttu-id="50435-427">✔</span><span class="sxs-lookup"><span data-stu-id="50435-427">✔</span></span>|<span data-ttu-id="50435-428">Понятное имя команды.</span><span class="sxs-lookup"><span data-stu-id="50435-428">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="50435-429">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-429">string</span></span>|<span data-ttu-id="50435-430">64 символа</span><span class="sxs-lookup"><span data-stu-id="50435-430">64 characters</span></span>||<span data-ttu-id="50435-431">Тип команды.</span><span class="sxs-lookup"><span data-stu-id="50435-431">Type of the command.</span></span> <span data-ttu-id="50435-432">Один из `query` или `action` .</span><span class="sxs-lookup"><span data-stu-id="50435-432">One of `query` or `action`.</span></span> <span data-ttu-id="50435-433">Значение по умолчанию: **Query**.</span><span class="sxs-lookup"><span data-stu-id="50435-433">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="50435-434">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-434">string</span></span>|<span data-ttu-id="50435-435">128 символов</span><span class="sxs-lookup"><span data-stu-id="50435-435">128 characters</span></span>||<span data-ttu-id="50435-436">Описание, которое отображается для пользователей, чтобы указать назначение этой команды.</span><span class="sxs-lookup"><span data-stu-id="50435-436">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="50435-437">boolean</span><span class="sxs-lookup"><span data-stu-id="50435-437">boolean</span></span>|||<span data-ttu-id="50435-438">Логическое значение, которое указывает, следует ли выполнять команду изначально без параметров.</span><span class="sxs-lookup"><span data-stu-id="50435-438">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="50435-439">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="50435-439">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="50435-440">Массив строк</span><span class="sxs-lookup"><span data-stu-id="50435-440">array of Strings</span></span>|<span data-ttu-id="50435-441">4</span><span class="sxs-lookup"><span data-stu-id="50435-441">3</span></span>||<span data-ttu-id="50435-442">Определяет, откуда можно вызвать расширение сообщения.</span><span class="sxs-lookup"><span data-stu-id="50435-442">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="50435-443">Любое сочетание `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="50435-443">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="50435-444">Значение по умолчанию: `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="50435-444">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="50435-445">boolean</span><span class="sxs-lookup"><span data-stu-id="50435-445">boolean</span></span>|||<span data-ttu-id="50435-446">Логическое значение, которое указывает, следует ли выполнять динамическое извлечение модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="50435-446">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="50435-447">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="50435-447">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="50435-448">объект</span><span class="sxs-lookup"><span data-stu-id="50435-448">object</span></span>|||<span data-ttu-id="50435-449">Укажите модуль задач для предварительной загрузки при использовании команды расширения системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="50435-449">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="50435-450">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-450">string</span></span>|<span data-ttu-id="50435-451">64 символа</span><span class="sxs-lookup"><span data-stu-id="50435-451">64 characters</span></span>||<span data-ttu-id="50435-452">Заголовок начального диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="50435-452">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="50435-453">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-453">string</span></span>|||<span data-ttu-id="50435-454">Ширина диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый".</span><span class="sxs-lookup"><span data-stu-id="50435-454">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="50435-455">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-455">string</span></span>|||<span data-ttu-id="50435-456">Высота диалогового окна — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый".</span><span class="sxs-lookup"><span data-stu-id="50435-456">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="50435-457">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-457">string</span></span>|||<span data-ttu-id="50435-458">Исходный URL-адрес вебвиев.</span><span class="sxs-lookup"><span data-stu-id="50435-458">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="50435-459">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="50435-459">array of object</span></span>|<span data-ttu-id="50435-460">5 элементов</span><span class="sxs-lookup"><span data-stu-id="50435-460">5 items</span></span>|<span data-ttu-id="50435-461">✔</span><span class="sxs-lookup"><span data-stu-id="50435-461">✔</span></span>|<span data-ttu-id="50435-462">Список параметров, которые выполняет команда.</span><span class="sxs-lookup"><span data-stu-id="50435-462">The list of parameters the command takes.</span></span> <span data-ttu-id="50435-463">Минимум: 1; максимум: 5.</span><span class="sxs-lookup"><span data-stu-id="50435-463">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="50435-464">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-464">string</span></span>|<span data-ttu-id="50435-465">64 символа</span><span class="sxs-lookup"><span data-stu-id="50435-465">64 characters</span></span>|<span data-ttu-id="50435-466">✔</span><span class="sxs-lookup"><span data-stu-id="50435-466">✔</span></span>|<span data-ttu-id="50435-467">Имя параметра в том виде, в котором оно отображается в клиенте.</span><span class="sxs-lookup"><span data-stu-id="50435-467">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="50435-468">Он включен в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="50435-468">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="50435-469">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-469">string</span></span>|<span data-ttu-id="50435-470">32 символов</span><span class="sxs-lookup"><span data-stu-id="50435-470">32 characters</span></span>|<span data-ttu-id="50435-471">✔</span><span class="sxs-lookup"><span data-stu-id="50435-471">✔</span></span>|<span data-ttu-id="50435-472">Удобное для пользователя название параметра.</span><span class="sxs-lookup"><span data-stu-id="50435-472">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="50435-473">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-473">string</span></span>|<span data-ttu-id="50435-474">128 символов</span><span class="sxs-lookup"><span data-stu-id="50435-474">128 characters</span></span>||<span data-ttu-id="50435-475">Понятная пользователю строка, описывающая назначение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="50435-475">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="50435-476">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-476">string</span></span>|<span data-ttu-id="50435-477">512 символов</span><span class="sxs-lookup"><span data-stu-id="50435-477">512 characters</span></span>||<span data-ttu-id="50435-478">Начальное значение параметра.</span><span class="sxs-lookup"><span data-stu-id="50435-478">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="50435-479">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-479">string</span></span>|<span data-ttu-id="50435-480">128 символов</span><span class="sxs-lookup"><span data-stu-id="50435-480">128 characters</span></span>||<span data-ttu-id="50435-481">Определяет тип элемента управления, отображаемого в модуле задачи для `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="50435-481">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="50435-482">Один из `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="50435-482">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="50435-483">массив объектов</span><span class="sxs-lookup"><span data-stu-id="50435-483">array of objects</span></span>|<span data-ttu-id="50435-484">10 элементов</span><span class="sxs-lookup"><span data-stu-id="50435-484">10 items</span></span>||<span data-ttu-id="50435-485">Варианты выбора для `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="50435-485">The choice options for the`choiceset`.</span></span> <span data-ttu-id="50435-486">Используйте только при `parameter.inputType` наличии `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="50435-486">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="50435-487">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-487">string</span></span>|<span data-ttu-id="50435-488">128 символов</span><span class="sxs-lookup"><span data-stu-id="50435-488">128 characters</span></span>|<span data-ttu-id="50435-489">✔</span><span class="sxs-lookup"><span data-stu-id="50435-489">✔</span></span>|<span data-ttu-id="50435-490">Название выбора.</span><span class="sxs-lookup"><span data-stu-id="50435-490">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="50435-491">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-491">string</span></span>|<span data-ttu-id="50435-492">512 символов</span><span class="sxs-lookup"><span data-stu-id="50435-492">512 characters</span></span>|<span data-ttu-id="50435-493">✔</span><span class="sxs-lookup"><span data-stu-id="50435-493">✔</span></span>|<span data-ttu-id="50435-494">Значение выбора.</span><span class="sxs-lookup"><span data-stu-id="50435-494">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="50435-495">разрешения</span><span class="sxs-lookup"><span data-stu-id="50435-495">permissions</span></span>

<span data-ttu-id="50435-496">**Необязательное** — массив строк</span><span class="sxs-lookup"><span data-stu-id="50435-496">**Optional** — array of strings</span></span>

<span data-ttu-id="50435-497">Массив, `string` определяющий, какие разрешения запрашиваются приложением, что позволяет конечным пользователям знать, как будет выполняться расширение.</span><span class="sxs-lookup"><span data-stu-id="50435-497">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="50435-498">Следующие параметры неисключительны:</span><span class="sxs-lookup"><span data-stu-id="50435-498">The following options are non-exclusive:</span></span>

* <span data-ttu-id="50435-499">`identity`&emsp;Требуются сведения об удостоверении пользователя</span><span class="sxs-lookup"><span data-stu-id="50435-499">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="50435-500">`messageTeamMembers`&emsp;Требуется разрешение на отправку прямых сообщений участникам группы</span><span class="sxs-lookup"><span data-stu-id="50435-500">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="50435-501">Изменение этих разрешений при обновлении приложения приводит к тому, что пользователи будут повторять процесс разрешения при первом запуске обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="50435-501">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="50435-502">Дополнительные сведения см. [в разделе Обновление приложения](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) .</span><span class="sxs-lookup"><span data-stu-id="50435-502">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="50435-503">девицепермиссионс</span><span class="sxs-lookup"><span data-stu-id="50435-503">devicePermissions</span></span>

<span data-ttu-id="50435-504">**Необязательное** — массив строк</span><span class="sxs-lookup"><span data-stu-id="50435-504">**Optional** — array of strings</span></span>

<span data-ttu-id="50435-505">Указывает собственные функции на устройстве пользователя, к которым приложение может запрашивать доступ.</span><span class="sxs-lookup"><span data-stu-id="50435-505">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="50435-506">Возможные варианты:</span><span class="sxs-lookup"><span data-stu-id="50435-506">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="50435-507">валиддомаинс</span><span class="sxs-lookup"><span data-stu-id="50435-507">validDomains</span></span>

<span data-ttu-id="50435-508">**Необязательно**, за исключением **обязательного** места, где отмечено</span><span class="sxs-lookup"><span data-stu-id="50435-508">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="50435-509">Список допустимых доменов для веб-сайтов, которые приложение ожидает загружать в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="50435-509">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="50435-510">Примеры доменов могут включать подстановочные знаки `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="50435-510">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="50435-511">Это соответствует только одному сегменту домена; Если вам нужно использовать этот параметр `a.b.example.com` `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="50435-511">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="50435-512">Если конфигурация вкладки или контентный пользовательский интерфейс должны перейти к любому другому домену, Кроме того, что используется для настройки вкладок, этот домен необходимо указать здесь.</span><span class="sxs-lookup"><span data-stu-id="50435-512">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="50435-513">Тем не менее, **не** нужно включать домены поставщиков удостоверений, которые требуется поддерживать в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="50435-513">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="50435-514">Например, для проверки подлинности с помощью идентификатора Google необходимо перенаправить на accounts.google.com, но не следует включать accounts.google.com в `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="50435-514">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="50435-515">Приложения Teams, которым для правильной работы требуются собственные URL-адреса SharePoint, могут содержать "{теамситедомаин}" в допустимом списке доменов.</span><span class="sxs-lookup"><span data-stu-id="50435-515">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50435-516">Не добавляйте домены за предельный элемент управления (напрямую или с помощью подстановочных знаков).</span><span class="sxs-lookup"><span data-stu-id="50435-516">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="50435-517">Например, `yourapp.onmicrosoft.com` является допустимым, но `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="50435-517">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="50435-518">Объект является массивом со всеми элементами типа `string` .</span><span class="sxs-lookup"><span data-stu-id="50435-518">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="50435-519">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="50435-519">webApplicationInfo</span></span>

<span data-ttu-id="50435-520">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="50435-520">**Optional** — object</span></span>

<span data-ttu-id="50435-521">Указание идентификатора приложения и графического объекта AAD для упрощения входа пользователей в приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="50435-521">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="50435-522">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-522">Name</span></span>| <span data-ttu-id="50435-523">Тип</span><span class="sxs-lookup"><span data-stu-id="50435-523">Type</span></span>| <span data-ttu-id="50435-524">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-524">Maximum size</span></span> | <span data-ttu-id="50435-525">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-525">Required</span></span> | <span data-ttu-id="50435-526">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-526">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="50435-527">string</span><span class="sxs-lookup"><span data-stu-id="50435-527">string</span></span>|<span data-ttu-id="50435-528">36 символов</span><span class="sxs-lookup"><span data-stu-id="50435-528">36 characters</span></span>|<span data-ttu-id="50435-529">✔</span><span class="sxs-lookup"><span data-stu-id="50435-529">✔</span></span>|<span data-ttu-id="50435-530">Идентификатор приложения AAD приложения.</span><span class="sxs-lookup"><span data-stu-id="50435-530">AAD application id of the app.</span></span> <span data-ttu-id="50435-531">Этот идентификатор должен быть идентификатором GUID.</span><span class="sxs-lookup"><span data-stu-id="50435-531">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="50435-532">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-532">string</span></span>|<span data-ttu-id="50435-533">2048 символов</span><span class="sxs-lookup"><span data-stu-id="50435-533">2048 characters</span></span>||<span data-ttu-id="50435-534">URL-адрес ресурса приложения для получения маркера проверки подлинности для единого входа.</span><span class="sxs-lookup"><span data-stu-id="50435-534">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="50435-535">массив строк</span><span class="sxs-lookup"><span data-stu-id="50435-535">array of strings</span></span>|<span data-ttu-id="50435-536">128 символов</span><span class="sxs-lookup"><span data-stu-id="50435-536">128 characters</span></span>||<span data-ttu-id="50435-537">Определение разрешения на уровне [отдельных ресурсов](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="50435-537">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="50435-538">шовлоадингиндикатор</span><span class="sxs-lookup"><span data-stu-id="50435-538">showLoadingIndicator</span></span>

<span data-ttu-id="50435-539">**Необязательный** — логический</span><span class="sxs-lookup"><span data-stu-id="50435-539">**Optional** — boolean</span></span>

<span data-ttu-id="50435-540">Указывает, следует ли отображать индикатор загрузки при загрузке приложения или вкладки.</span><span class="sxs-lookup"><span data-stu-id="50435-540">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="50435-541">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="50435-541">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="50435-542">Если в манифесте приложения задано значение "Шовлоадингиндикатор: true", то для правильной загрузки страницы необходимо изменить страницы содержимого вкладок и модулей задач в соответствии с протоколом, описанным в статье [Показать встроенный документ с индикатором загрузки](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) .</span><span class="sxs-lookup"><span data-stu-id="50435-542">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="50435-543">в полноэкранном режим</span><span class="sxs-lookup"><span data-stu-id="50435-543">isFullScreen</span></span>

 <span data-ttu-id="50435-544">**Необязательный** — логический</span><span class="sxs-lookup"><span data-stu-id="50435-544">**Optional** — boolean</span></span>

<span data-ttu-id="50435-545">Указывает, где отображается личное приложение с панелью заголовков вкладок или без нее.</span><span class="sxs-lookup"><span data-stu-id="50435-545">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="50435-546">По умолчанию: **false**.</span><span class="sxs-lookup"><span data-stu-id="50435-546">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="50435-547">activities</span><span class="sxs-lookup"><span data-stu-id="50435-547">activities</span></span>

<span data-ttu-id="50435-548">**Необязательный** — объект</span><span class="sxs-lookup"><span data-stu-id="50435-548">**Optional** — object</span></span>

<span data-ttu-id="50435-549">Определите свойства, которые ваше приложение будет использовать для публикации в канал активности пользователя.</span><span class="sxs-lookup"><span data-stu-id="50435-549">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="50435-550">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-550">Name</span></span>| <span data-ttu-id="50435-551">Тип</span><span class="sxs-lookup"><span data-stu-id="50435-551">Type</span></span>| <span data-ttu-id="50435-552">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-552">Maximum size</span></span> | <span data-ttu-id="50435-553">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-553">Required</span></span> | <span data-ttu-id="50435-554">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-554">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="50435-555">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="50435-555">array of Objects</span></span>|<span data-ttu-id="50435-556">128 элементов</span><span class="sxs-lookup"><span data-stu-id="50435-556">128 items</span></span>| | <span data-ttu-id="50435-557">Укажите типы действий, которые ваше приложение может отправлять в канал активности пользователей.</span><span class="sxs-lookup"><span data-stu-id="50435-557">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="50435-558">действия. Активититипес</span><span class="sxs-lookup"><span data-stu-id="50435-558">activities.activityTypes</span></span>

|<span data-ttu-id="50435-559">Имя</span><span class="sxs-lookup"><span data-stu-id="50435-559">Name</span></span>| <span data-ttu-id="50435-560">Тип</span><span class="sxs-lookup"><span data-stu-id="50435-560">Type</span></span>| <span data-ttu-id="50435-561">Максимальный размер</span><span class="sxs-lookup"><span data-stu-id="50435-561">Maximum size</span></span> | <span data-ttu-id="50435-562">Обязательный</span><span class="sxs-lookup"><span data-stu-id="50435-562">Required</span></span> | <span data-ttu-id="50435-563">Описание</span><span class="sxs-lookup"><span data-stu-id="50435-563">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="50435-564">string</span><span class="sxs-lookup"><span data-stu-id="50435-564">string</span></span>|<span data-ttu-id="50435-565">32 символов</span><span class="sxs-lookup"><span data-stu-id="50435-565">32 characters</span></span>|<span data-ttu-id="50435-566">✔</span><span class="sxs-lookup"><span data-stu-id="50435-566">✔</span></span>|<span data-ttu-id="50435-567">Тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="50435-567">The notification type.</span></span> <span data-ttu-id="50435-568">*Ознакомьтесь*с разделом ниже.</span><span class="sxs-lookup"><span data-stu-id="50435-568">*See below*.</span></span>|
|`description`|<span data-ttu-id="50435-569">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-569">string</span></span>|<span data-ttu-id="50435-570">128 символов</span><span class="sxs-lookup"><span data-stu-id="50435-570">128 characters</span></span>|<span data-ttu-id="50435-571">✔</span><span class="sxs-lookup"><span data-stu-id="50435-571">✔</span></span>|<span data-ttu-id="50435-572">Краткое описание уведомления.</span><span class="sxs-lookup"><span data-stu-id="50435-572">A brief description of the notification.</span></span> <span data-ttu-id="50435-573">*Ознакомьтесь*с разделом ниже.</span><span class="sxs-lookup"><span data-stu-id="50435-573">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="50435-574">Строка</span><span class="sxs-lookup"><span data-stu-id="50435-574">string</span></span>|<span data-ttu-id="50435-575">128 символов</span><span class="sxs-lookup"><span data-stu-id="50435-575">128 characters</span></span>|<span data-ttu-id="50435-576">✔</span><span class="sxs-lookup"><span data-stu-id="50435-576">✔</span></span>|<span data-ttu-id="50435-577">Пример: "{Actor} создал задачу {taskId} для вас"</span><span class="sxs-lookup"><span data-stu-id="50435-577">Ex: "{actor} created task {taskId} for you"</span></span>|

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
