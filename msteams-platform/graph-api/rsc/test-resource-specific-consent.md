---
title: Тестирование разрешений на согласие для определенных ресурсов в Teams
description: Подробные сведения о тестировании согласия на использование ресурсов в Teams с помощью Postman
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: команды авторизации OAuth SSO AAD rsc postman Graph
ms.openlocfilehash: 92c6d5d96c103fb5e0da6afd91357b5887b2ba10
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069082"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a><span data-ttu-id="fb235-104">Тестирование разрешений на согласие для определенных ресурсов в Teams</span><span class="sxs-lookup"><span data-stu-id="fb235-104">Test resource-specific consent permissions in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="fb235-105">Согласие на доступ к области чата с конкретными ресурсами доступно только для [предварительного просмотра общедоступных](../../resources/dev-preview/developer-preview-intro.md) разработчиков.</span><span class="sxs-lookup"><span data-stu-id="fb235-105">Resource-specific consent for chat scope is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="fb235-106">Согласие на использование ресурсов — это интеграция Microsoft Teams и Graph API, которая позволяет приложению использовать конечные точки API для управления определенными ресурсами — группами или чатами — в организации.</span><span class="sxs-lookup"><span data-stu-id="fb235-106">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific resources—either teams or chats—within an organization.</span></span> <span data-ttu-id="fb235-107">Дополнительные сведения см. в [специальном для ресурса согласии (RSC) — Microsoft Teams Graph API.](resource-specific-consent.md)</span><span class="sxs-lookup"><span data-stu-id="fb235-107">For more information, see [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fb235-108">Чтобы проверить разрешения RSC, Teams манифест приложения должен включать ключ **webApplicationInfo,** населённый следующими полями:</span><span class="sxs-lookup"><span data-stu-id="fb235-108">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="fb235-109">**id.** ID приложения Azure AD см. в приложении [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="fb235-109">**id**: Your Azure AD app ID, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="fb235-110">**ресурс**. Любая строка, см. примечание в [обновлении манифеста Teams приложения](resource-specific-consent.md#update-your-teams-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="fb235-110">**resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span></span>
> - <span data-ttu-id="fb235-111">**Разрешения приложения:** разрешения RSC для вашего приложения см. в [приложении Resource-specific Permissions.](resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="fb235-111">**application permissions**: RSC permissions for  your app, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

## <a name="example-for-a-team"></a><span data-ttu-id="fb235-112">Пример для группы</span><span class="sxs-lookup"><span data-stu-id="fb235-112">Example for a team</span></span>
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
         "Channel.Create.Group",
         "Channel.Delete.Group",
         "ChannelMessage.Read.Group",
         "ChannelSettings.Read.Group",
         "ChannelSettings.Edit.Group",
         "Member.Read.Group",
         "Owner.Read.Group",
         "TeamsApp.Read.Group",
         "TeamsTab.Read.Group",
         "TeamsTab.Create.Group",
         "TeamsTab.Edit.Group",
         "TeamsTab.Delete.Group",
         "TeamSettings.Read.Group",
         "TeamSettings.Edit.Group"
      ]
   }
```

## <a name="example-for-a-chat"></a><span data-ttu-id="fb235-113">Пример для чата</span><span class="sxs-lookup"><span data-stu-id="fb235-113">Example for a chat</span></span>
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
          "ChatSettings.Read.Chat",
          "ChatSettings.ReadWrite.Chat",
          "ChatMessage.Read.Chat",
          "ChatMember.Read.Chat",
          "Chat.Manage.Chat",
          "TeamsTab.Read.Chat",
          "TeamsTab.Create.Chat",
          "TeamsTab.Delete.Chat",
          "TeamsTab.ReadWrite.Chat",
          "TeamsAppInstallation.Read.Chat",
          "OnlineMeeting.ReadBasic.Chat"
      ]
   }
```

> [!IMPORTANT]
> <span data-ttu-id="fb235-114">В манифесте приложения включите только разрешения RSC, которые необходимо иметь вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="fb235-114">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

>[!NOTE]
><span data-ttu-id="fb235-115">Если приложение предназначено для поддержки установки в командных и чатных сферах, в одном манифесте могут быть указаны разрешения как группы, так и `applicationPermissions` чата.</span><span class="sxs-lookup"><span data-stu-id="fb235-115">If the app is meant to support installation in both team and chat scopes, then both team and chat permissions can be specified in the same manifest under `applicationPermissions`.</span></span>

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a><span data-ttu-id="fb235-116">Test added RSC permissions to a team using the Postman app</span><span class="sxs-lookup"><span data-stu-id="fb235-116">Test added RSC permissions to a team using the Postman app</span></span>

<span data-ttu-id="fb235-117">Чтобы проверить, чтят ли разрешения RSC полезной нагрузкой запроса API, необходимо скопировать тестовый код [RSC JSON](test-team-rsc-json-file.md) для группы в локальной среде и обновить следующие значения:</span><span class="sxs-lookup"><span data-stu-id="fb235-117">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code for team](test-team-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="fb235-118">`azureADAppId`: ID приложения Azure AD в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="fb235-118">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="fb235-119">`azureADAppSecret`Пароль приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb235-119">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="fb235-120">`token_scope`. Область требуется для получения маркера.</span><span class="sxs-lookup"><span data-stu-id="fb235-120">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="fb235-121">установите значение https://graph.microsoft.com/.default .</span><span class="sxs-lookup"><span data-stu-id="fb235-121">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="fb235-122">`teamGroupId`: Вы можете получить id группы группы от клиента Teams следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fb235-122">`teamGroupId`: You can get the team group id from the Teams client as follows:</span></span>

    1. <span data-ttu-id="fb235-123">В клиенте Teams выберите **Teams** из левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="fb235-123">In the Teams client, select **Teams** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="fb235-124">Выберите команду, в которой установлено приложение из отсевного меню.</span><span class="sxs-lookup"><span data-stu-id="fb235-124">Select the team where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="fb235-125">Выберите **значок Дополнительные** параметры (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="fb235-125">Select the **More options** icon (&#8943;).</span></span>
    4. <span data-ttu-id="fb235-126">Выберите **Получить ссылку на команду**.</span><span class="sxs-lookup"><span data-stu-id="fb235-126">Select **Get link to team**.</span></span> 
    5. <span data-ttu-id="fb235-127">Скопируйте и сохраните **значение groupId** из строки.</span><span class="sxs-lookup"><span data-stu-id="fb235-127">Copy and save the **groupId** value from the string.</span></span>

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a><span data-ttu-id="fb235-128">Test added RSC permissions to a chat using the Postman app</span><span class="sxs-lookup"><span data-stu-id="fb235-128">Test added RSC permissions to a chat using the Postman app</span></span>

<span data-ttu-id="fb235-129">Чтобы проверить, чтят ли разрешения RSC полезной нагрузкой запроса API, необходимо скопировать тестовый код [RSC JSON](test-chat-rsc-json-file.md) для чатов в локальной среде и обновить следующие значения:</span><span class="sxs-lookup"><span data-stu-id="fb235-129">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code for chats](test-chat-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="fb235-130">`azureADAppId`: ID приложения Azure AD в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="fb235-130">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="fb235-131">`azureADAppSecret`Пароль приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb235-131">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="fb235-132">`token_scope`. Область требуется для получения маркера.</span><span class="sxs-lookup"><span data-stu-id="fb235-132">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="fb235-133">установите значение https://graph.microsoft.com/.default .</span><span class="sxs-lookup"><span data-stu-id="fb235-133">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="fb235-134">`tenantId`: Имя или ID объекта AAD клиента.</span><span class="sxs-lookup"><span data-stu-id="fb235-134">`tenantId`: The name or the AAD Object ID of your tenant.</span></span>
* <span data-ttu-id="fb235-135">`chatId`: Вы можете получить id потока чата из Teams *веб-клиента* следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fb235-135">`chatId`: You can get the chat thread id from the Teams *web* client as follows:</span></span>

    1. <span data-ttu-id="fb235-136">В веб Teams клиенте выберите **Чат из** левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="fb235-136">In the Teams web client, select **Chat** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="fb235-137">Выберите чат, в котором установлено приложение из меню отсев.</span><span class="sxs-lookup"><span data-stu-id="fb235-137">Select the chat where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="fb235-138">Скопируйте веб-URL-адрес и сохраните id потока чата из строки.</span><span class="sxs-lookup"><span data-stu-id="fb235-138">Copy the web URL and save the chat thread id from the string.</span></span>
<span data-ttu-id="fb235-139">![ID потока чата с веб-URL-адреса.](../../assets/images/chat-thread-id.png)</span><span class="sxs-lookup"><span data-stu-id="fb235-139">![Chat thread id from web URL.](../../assets/images/chat-thread-id.png)</span></span>

### <a name="use-postman"></a><span data-ttu-id="fb235-140">Использование Postman</span><span class="sxs-lookup"><span data-stu-id="fb235-140">Use Postman</span></span>

1. <span data-ttu-id="fb235-141">Откройте [приложение Postman.](https://www.postman.com)</span><span class="sxs-lookup"><span data-stu-id="fb235-141">Open the [Postman](https://www.postman.com) app.</span></span>
2. <span data-ttu-id="fb235-142">Выберите **файл импорта**  >    >  **файлов,** чтобы загрузить обновленный JSON-файл из среды.</span><span class="sxs-lookup"><span data-stu-id="fb235-142">Select **File** > **Import** > **Import file** to upload the updated JSON file from your environment.</span></span>  
3. <span data-ttu-id="fb235-143">Выберите **вкладку Collections.**</span><span class="sxs-lookup"><span data-stu-id="fb235-143">Select the **Collections** tab.</span></span> 
4. <span data-ttu-id="fb235-144">Выберите шеврон **>** рядом с **тестом RSC,** чтобы расширить представление сведений и просмотреть запросы API.</span><span class="sxs-lookup"><span data-stu-id="fb235-144">Select the chevron **>** next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="fb235-145">Выполните всю коллекцию разрешений для каждого вызова API.</span><span class="sxs-lookup"><span data-stu-id="fb235-145">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="fb235-146">Разрешения, указанные в манифесте приложения, должны быть успешными, а те, которые не указаны, должны не работать с кодом состояния HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="fb235-146">The permissions that you specified in your app manifest must succeed, while those not specified must fail with an HTTP 403 status code.</span></span> <span data-ttu-id="fb235-147">Проверьте все коды состояния отклика, чтобы подтвердить, что поведение разрешений RSC в вашем приложении соответствует ожиданиям.</span><span class="sxs-lookup"><span data-stu-id="fb235-147">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

> [!NOTE]
> <span data-ttu-id="fb235-148">Чтобы протестировать конкретные вызовы DELETE и READ API, добавьте эти сценарии экземпляров в файл JSON.</span><span class="sxs-lookup"><span data-stu-id="fb235-148">To test specific DELETE and READ API calls, add those instance scenarios to the JSON file.</span></span>

## <a name="test-revoked-rsc-permissions-using-postman"></a><span data-ttu-id="fb235-149">Тестирование отозванных разрешений RSC с помощью [Postman](https://www.postman.com/)</span><span class="sxs-lookup"><span data-stu-id="fb235-149">Test revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

1. <span data-ttu-id="fb235-150">Удалить приложение из определенного ресурса.</span><span class="sxs-lookup"><span data-stu-id="fb235-150">Uninstall the app from the specific resource.</span></span>
2. <span data-ttu-id="fb235-151">Выполните действия для чата или группы:</span><span class="sxs-lookup"><span data-stu-id="fb235-151">Follow the steps for either chat or team:</span></span> 
    1. <span data-ttu-id="fb235-152">[Test added RSC permissions to a team using Postman.](#test-added-rsc-permissions-to-a-team-using-the-postman-app)</span><span class="sxs-lookup"><span data-stu-id="fb235-152">[Test added RSC permissions to a team using Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).</span></span>
    2. <span data-ttu-id="fb235-153">[Test added RSC permissions to a chat using Postman.](#test-added-rsc-permissions-to-a-chat-using-the-postman-app)</span><span class="sxs-lookup"><span data-stu-id="fb235-153">[Test added RSC permissions to a chat using Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).</span></span>
3. <span data-ttu-id="fb235-154">Проверьте все коды состояния отклика, чтобы подтвердить, что конкретные вызовы API сбой с **кодом состояния HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="fb235-154">Check all the response status codes to confirm that the specific API calls **have failed with an HTTP 403 status code**.</span></span>

## <a name="see-also"></a><span data-ttu-id="fb235-155">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="fb235-155">See also</span></span>

[<span data-ttu-id="fb235-156">Microsoft Graph API и Teams</span><span class="sxs-lookup"><span data-stu-id="fb235-156">Microsoft Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

