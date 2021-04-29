---
title: Тестирование разрешений на согласие для определенных ресурсов в Teams
description: Подробные сведения о тестировании согласия на использование ресурсов в Teams с помощью postman
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: команды авторизации OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 328be5b4f1e3597457afb9ce1413eb35aa2df71e
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075621"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a><span data-ttu-id="b928a-104">Тестирование разрешений на согласие для определенных ресурсов в Teams</span><span class="sxs-lookup"><span data-stu-id="b928a-104">Test resource-specific consent permissions in Teams</span></span>

<span data-ttu-id="b928a-105">Согласие на использование ресурсов — это интеграция Microsoft Teams и Graph API, которая позволяет приложению использовать конечные точки API для управления определенными группами в организации.</span><span class="sxs-lookup"><span data-stu-id="b928a-105">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="b928a-106">Дополнительные сведения см. в [сайте Resource-specific consent (RSC) — API Microsoft Teams Graph.](resource-specific-consent.md)</span><span class="sxs-lookup"><span data-stu-id="b928a-106">For more information, see [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b928a-107">Чтобы проверить разрешения RSC, файл манифеста приложения Teams должен включать ключ **webApplicationInfo,** населённый следующими полями:</span><span class="sxs-lookup"><span data-stu-id="b928a-107">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="b928a-108">**id.** ID приложения Azure AD см. в приложении [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="b928a-108">**id**: Your Azure AD app ID, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="b928a-109">**ресурс.** Любая строка см. в заметке [в манифесте Обновления приложения Teams.](resource-specific-consent.md#update-your-teams-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="b928a-109">**resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span></span>
> - <span data-ttu-id="b928a-110">**Разрешения приложения:** разрешения RSC для вашего приложения см. в [приложении Resource-specific Permissions.](resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="b928a-110">**application permissions**: RSC permissions for  your app, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

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

> [!IMPORTANT]
> <span data-ttu-id="b928a-111">В манифесте приложения включите только разрешения RSC, которые необходимо иметь вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="b928a-111">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

## <a name="test-added-rsc-permissions-using-the-postman-app"></a><span data-ttu-id="b928a-112">Тестирование добавленных разрешений RSC с помощью приложения Postman</span><span class="sxs-lookup"><span data-stu-id="b928a-112">Test added RSC permissions using the Postman app</span></span>

<span data-ttu-id="b928a-113">Чтобы проверить, чтят ли разрешения RSC полезной нагрузкой запроса API, необходимо скопировать тестовый код [RSC JSON](test-rsc-json-file.md) в локальной среде и обновить следующие значения:</span><span class="sxs-lookup"><span data-stu-id="b928a-113">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code](test-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="b928a-114">`azureADAppId`: ID приложения Azure AD в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="b928a-114">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="b928a-115">`azureADAppSecret`Пароль приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b928a-115">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="b928a-116">`token_scope`. Область требуется для получения маркера.</span><span class="sxs-lookup"><span data-stu-id="b928a-116">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="b928a-117">установите значение https://graph.microsoft.com/.default .</span><span class="sxs-lookup"><span data-stu-id="b928a-117">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="b928a-118">`teamGroupId`: Вы можете получить id группы группы из клиента Teams следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b928a-118">`teamGroupId`: You can get the team group id from the Teams client as follows:</span></span>

    1. <span data-ttu-id="b928a-119">В клиенте Teams выберите **Teams из** левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="b928a-119">In the Teams client, select **Teams** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="b928a-120">Выберите команду, в которой установлено приложение из отсевного меню.</span><span class="sxs-lookup"><span data-stu-id="b928a-120">Select the team where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="b928a-121">Выберите **значок Дополнительные** параметры (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="b928a-121">Select the **More options** icon (&#8943;).</span></span>
    4. <span data-ttu-id="b928a-122">Выберите **Получить ссылку на команду**.</span><span class="sxs-lookup"><span data-stu-id="b928a-122">Select **Get link to team**.</span></span> 
    5. <span data-ttu-id="b928a-123">Скопируйте и сохраните **значение groupId** из строки.</span><span class="sxs-lookup"><span data-stu-id="b928a-123">Copy and save the **groupId** value from the string.</span></span>

### <a name="use-postman"></a><span data-ttu-id="b928a-124">Использование Postman</span><span class="sxs-lookup"><span data-stu-id="b928a-124">Use Postman</span></span>

1. <span data-ttu-id="b928a-125">Откройте [приложение Postman.](https://www.postman.com)</span><span class="sxs-lookup"><span data-stu-id="b928a-125">Open the [Postman](https://www.postman.com) app.</span></span>
2. <span data-ttu-id="b928a-126">Выберите **файл импорта**  >    >  **файлов,** чтобы загрузить обновленный JSON-файл из среды.</span><span class="sxs-lookup"><span data-stu-id="b928a-126">Select **File** > **Import** > **Import file** to upload the updated JSON file from your environment.</span></span>  
3. <span data-ttu-id="b928a-127">Выберите **вкладку Collections.**</span><span class="sxs-lookup"><span data-stu-id="b928a-127">Select the **Collections** tab.</span></span> 
4. <span data-ttu-id="b928a-128">Выберите шеврон **>** рядом с **тестом RSC,** чтобы расширить представление сведений и просмотреть запросы API.</span><span class="sxs-lookup"><span data-stu-id="b928a-128">Select the chevron **>** next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="b928a-129">Выполните всю коллекцию разрешений для каждого вызова API.</span><span class="sxs-lookup"><span data-stu-id="b928a-129">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="b928a-130">Разрешения, указанные в манифесте приложения, должны быть успешными, а те, которые не указаны, должны не работать с кодом состояния HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="b928a-130">The permissions that you specified in your app manifest must succeed, while those not specified must fail with an HTTP 403 status code.</span></span> <span data-ttu-id="b928a-131">Проверьте все коды состояния отклика, чтобы подтвердить, что поведение разрешений RSC в вашем приложении соответствует ожиданиям.</span><span class="sxs-lookup"><span data-stu-id="b928a-131">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

> [!NOTE]
> <span data-ttu-id="b928a-132">Чтобы протестировать конкретные вызовы DELETE и READ API, добавьте эти сценарии экземпляров в файл JSON.</span><span class="sxs-lookup"><span data-stu-id="b928a-132">To test specific DELETE and READ API calls, add those instance scenarios to the JSON file.</span></span>

## <a name="test-revoked-rsc-permissions-using-postman"></a><span data-ttu-id="b928a-133">Тестирование отозванных разрешений RSC с помощью [Postman](https://www.postman.com/)</span><span class="sxs-lookup"><span data-stu-id="b928a-133">Test revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

1. <span data-ttu-id="b928a-134">Удалить приложение из определенной группы.</span><span class="sxs-lookup"><span data-stu-id="b928a-134">Uninstall the app from the specific team.</span></span>
2. <span data-ttu-id="b928a-135">Следуйте шагам [для тестовых добавленных разрешений RSC с помощью Postman](#test-added-rsc-permissions-using-the-postman-app).</span><span class="sxs-lookup"><span data-stu-id="b928a-135">Follow the steps for [Test added RSC permissions using Postman](#test-added-rsc-permissions-using-the-postman-app).</span></span>
3. <span data-ttu-id="b928a-136">Проверьте все коды состояния отклика, чтобы подтвердить, что конкретные вызовы API успешно сбой с **кодом состояния HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="b928a-136">Check all the response status codes to confirm that the specific API calls, **succeeded, have failed with an HTTP 403 status code**.</span></span>

## <a name="see-also"></a><span data-ttu-id="b928a-137">См. также</span><span class="sxs-lookup"><span data-stu-id="b928a-137">See also</span></span>

[<span data-ttu-id="b928a-138">API и команды Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="b928a-138">Microsoft Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

