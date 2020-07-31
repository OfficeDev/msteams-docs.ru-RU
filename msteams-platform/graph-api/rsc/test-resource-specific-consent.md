---
title: Тестирование согласия конкретного ресурса в Teams
description: Details проверка согласия конкретного ресурса в Teams с использованием POST
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: How-to
keywords: Диаграмма Microsoft Teams SSO единого входа OAuth RSC POST
ms.openlocfilehash: a7384222e5e4cba164f918186ce53b4c1b702016
ms.sourcegitcommit: 3e94edba28e9e1252b6a6ba35d4df32710dfc5d4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/31/2020
ms.locfileid: "46531268"
---
# <a name="test-resource-specific-consent-permissions--in-teams"></a><span data-ttu-id="ba782-104">Проверка разрешений согласия для определенных ресурсов в Teams</span><span class="sxs-lookup"><span data-stu-id="ba782-104">Test resource-specific consent permissions  in Teams</span></span>

<span data-ttu-id="ba782-105">Согласие с конкретными ресурсами (RSC) — это интеграция Microsoft Teams и Graph API, которая позволяет приложению использовать конечные точки API для управления определенными командами в Организации.</span><span class="sxs-lookup"><span data-stu-id="ba782-105">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="ba782-106">*Ознакомьтесь*с разделом[согласия для определенных ресурсов (RSC) — API Microsoft Teams Graph](resource-specific-consent.md).  </span><span class="sxs-lookup"><span data-stu-id="ba782-106">Please *see*  [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
><span data-ttu-id="ba782-107">Для тестирования разрешений RSC файл манифеста приложения Teams должен содержать ключ **webApplicationInfo** , заполненный следующими полями:</span><span class="sxs-lookup"><span data-stu-id="ba782-107">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="ba782-108">**ID** — идентификатор приложения Azure AD, *см* . [Регистрация приложения на портале Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="ba782-108">**id**  — your Azure AD app id, *see* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="ba782-109">**ресурс** — любая строка, *просмотрев* заметку в [статье обновление манифеста приложения Teams](resource-specific-consent.md#update-your-teams-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="ba782-109">**resource**  — any string, *see* the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest)</span></span>
> - <span data-ttu-id="ba782-110">**разрешения приложения** — сведения о разрешениях RSC для вашего *приложения: сведения* о разрешениях для [ресурсов](resource-specific-consent.md#resource-specific-permissions).</span><span class="sxs-lookup"><span data-stu-id="ba782-110">**application permissions** — RSC permissions for  your app, *see* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

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

>[!IMPORTANT]
><span data-ttu-id="ba782-111">В манифесте приложения включите только разрешения RSC, которые должно иметь ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="ba782-111">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

## <a name="test-added-rsc-permissions-using-the-postman-app"></a><span data-ttu-id="ba782-112">Тестирование добавленных разрешений RSC с использованием почтовых приложений</span><span class="sxs-lookup"><span data-stu-id="ba782-112">Test added RSC permissions using the Postman app</span></span>

<span data-ttu-id="ba782-113">Чтобы проверить, учитываются ли разрешения RSC в полезных данных запроса API, необходимо скопировать [код теста RSC JSON](test-rsc-json-file.md) в локальную среду и обновить следующие значения:</span><span class="sxs-lookup"><span data-stu-id="ba782-113">To check whether the RSC permissions are being honored by the API request payload, you'll need to copy the [RSC JSON test code](test-rsc-json-file.md) into your local environment and update the following values:</span></span>

1. <span data-ttu-id="ba782-114">`azureADAppId`— Идентификатор приложения Azure AD в приложении.</span><span class="sxs-lookup"><span data-stu-id="ba782-114">`azureADAppId`  — your app's Azure AD app id.</span></span>
1. <span data-ttu-id="ba782-115">`azureADAppSecret`— ваш секрет приложения Azure AD (пароль)</span><span class="sxs-lookup"><span data-stu-id="ba782-115">`azureADAppSecret`  — your Azure AD app secret (password)</span></span>
1. <span data-ttu-id="ba782-116">`token_scope`— область требуется для получения маркера, чтобы задать значениеhttps://graph.microsoft.com/.default</span><span class="sxs-lookup"><span data-stu-id="ba782-116">`token_scope`  — the scope is required to get a token - set the value to https://graph.microsoft.com/.default</span></span>
1. <span data-ttu-id="ba782-117">`teamGroupId`— Идентификатор группы Teams можно получить из клиента Teams следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ba782-117">`teamGroupId` — you can get the team group id from the Teams client as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ba782-118">В клиенте Teams выберите **Teams (Teams** ) в крайней левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="ba782-118">In the Teams client, select **Teams** from the far left nav bar .</span></span>
> * <span data-ttu-id="ba782-119">Выберите из раскрывающегося меню команду, в которой установлено приложение.</span><span class="sxs-lookup"><span data-stu-id="ba782-119">Select the team where the app is installed from the dropdown menu.</span></span>
> * <span data-ttu-id="ba782-120">Выбор значка " **Дополнительные параметры** " (&#8943;)</span><span class="sxs-lookup"><span data-stu-id="ba782-120">Select the **More options** icon (&#8943;)</span></span>
> * <span data-ttu-id="ba782-121">Выберите команду " **получить ссылку на группу** "</span><span class="sxs-lookup"><span data-stu-id="ba782-121">Select **Get link to team**</span></span> 
> * <span data-ttu-id="ba782-122">Скопируйте и сохраните значение **groupId** из строки.</span><span class="sxs-lookup"><span data-stu-id="ba782-122">Copy and save the **groupId** value from the string.</span></span>

### <a name="using-postman"></a><span data-ttu-id="ba782-123">Использование POST</span><span class="sxs-lookup"><span data-stu-id="ba782-123">Using Postman</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ba782-124">Откройте приложение [POST](https://www.postman.com) .</span><span class="sxs-lookup"><span data-stu-id="ba782-124">Open the [Postman](https://www.postman.com) app.</span></span>
> * <span data-ttu-id="ba782-125">Выберите **файл импорт файла**  =>  **Import**  =>  **импорта** , чтобы отправить обновленный файл JSON из вашей среды.</span><span class="sxs-lookup"><span data-stu-id="ba782-125">Select **File** => **Import** => **Import file** to upload the updated JSON file from your environment.</span></span>  
> * <span data-ttu-id="ba782-126">Перейдите на вкладку **коллекции** .</span><span class="sxs-lookup"><span data-stu-id="ba782-126">Select the **Collections** tab.</span></span> 
> * <span data-ttu-id="ba782-127">Выберите Шеврон (>) рядом с элементом **тест RSC** , чтобы развернуть представление сведений и просмотреть запросы API.</span><span class="sxs-lookup"><span data-stu-id="ba782-127">Select the chevron (>) next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="ba782-128">Выполните всю коллекцию разрешений для каждого вызова API.</span><span class="sxs-lookup"><span data-stu-id="ba782-128">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="ba782-129">Разрешения, указанные в манифесте приложения, должны выполняться успешно, в то время как они не задаются должным образом, с кодом состояния HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="ba782-129">The permissions that you specified in your app manifest should succeed, while those not specified should fail with an HTTP 403 status code.</span></span> <span data-ttu-id="ba782-130">Проверьте все коды состояния ответа, чтобы убедиться в том, что поведение RSC в вашем приложении соответствует ожиданиям.</span><span class="sxs-lookup"><span data-stu-id="ba782-130">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

>[!NOTE]
><span data-ttu-id="ba782-131">Чтобы протестировать конкретные вызовы API для удаления и чтения, добавьте эти сценарии в JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="ba782-131">To test specific DELETE and READ API calls, please add those instance scenarios to the JSON file.</span></span>

## <a name="test--revoked-rsc-permissions-using-postman"></a><span data-ttu-id="ba782-132">Проверка отозванных разрешений RSC с помощью [POST](https://www.postman.com/)</span><span class="sxs-lookup"><span data-stu-id="ba782-132">Test  revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ba782-133">Удаление приложения из определенной команды.</span><span class="sxs-lookup"><span data-stu-id="ba782-133">Uninstall the app from the specific team.</span></span>
> * <span data-ttu-id="ba782-134">Выполните описанные выше действия для теста, чтобы [Добавить разрешения RSC с помощью POST](#test-added-rsc-permissions-using-the-postman-app).</span><span class="sxs-lookup"><span data-stu-id="ba782-134">Follow the steps above for [Test added RSC permissions using Postman](#test-added-rsc-permissions-using-the-postman-app).</span></span>
> * <span data-ttu-id="ba782-135">Проверьте все коды состояния ответа, чтобы убедиться в том, что определенные вызовы API, которые завершились успешно, с кодом состояния HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="ba782-135">Check all of the response status codes to confirm that the specific API calls that succeeded have failed with an HTTP 403 status code.</span></span>

> [!div class="nextstepaction"]
>
> [<span data-ttu-id="ba782-136">Дополнительные сведения о API Graph и Teams</span><span class="sxs-lookup"><span data-stu-id="ba782-136">Learn more about the Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0)
