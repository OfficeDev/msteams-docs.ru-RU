---
title: Проверка обзора приложения
description: Описывает процесс тестирования настраиваемого приложения Teams в Microsoft 365
ms.topic: how-to
keywords: Настройка microsoft 365 tenant Teams для загрузки тестового приложения
ms.openlocfilehash: b199ca4be31b546364091b754cdb890c8c0dd7d0
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634781"
---
# <a name="test-your-app"></a><span data-ttu-id="d4dc2-104">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="d4dc2-104">Test your app</span></span>

<span data-ttu-id="d4dc2-105">После интеграции приложения с Microsoft Teams необходимо протестировать приложение перед его публикацией.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-105">After integrating your app with Microsoft Teams, you must test your app before publishing it.</span></span> <span data-ttu-id="d4dc2-106">Конечная цель состоит в том, чтобы получить как можно больше пользователей для вашего приложения, поэтому убедитесь, что приложение тестировать на нескольких устройствах, которые пользователи могут использовать.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-106">The ultimate goal is to get as many users for your app, therefore, ensure to test the app on multiple devices that users could use.</span></span> <span data-ttu-id="d4dc2-107">Для тестирования приложения:</span><span class="sxs-lookup"><span data-stu-id="d4dc2-107">For testing your app:</span></span>

* <span data-ttu-id="d4dc2-108">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="d4dc2-108">Prepare your Microsoft 365 tenant</span></span>
* <span data-ttu-id="d4dc2-109">Выберите рабочее пространство для тестирования и отлаговки приложения</span><span class="sxs-lookup"><span data-stu-id="d4dc2-109">Choose a workspace to test and debug your app</span></span>
* <span data-ttu-id="d4dc2-110">Добавление тестовых данных в клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="d4dc2-110">Add test data to your Microsoft 365 tenant</span></span>

## <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="d4dc2-111">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="d4dc2-111">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="d4dc2-112">Прежде чем приступить к тестированию приложения, подготовьте тестовый клиент Microsoft 365 и впустите настраиваемые приложения Teams, позволяющие загружать приложение.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-112">Before you start testing your app, prepare your Microsoft 365 test tenant and enable custom Teams app allow you to upload your app.</span></span> <span data-ttu-id="d4dc2-113">Необходимо зарегистрироваться в программе разработчика Microsoft 365 и управлять настройками Teams для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-113">You must sign-up for Microsoft 365 developer program and manage the Teams settings for your organization.</span></span> <span data-ttu-id="d4dc2-114">Настройте подписку на разработчика и настройте ее с [помощью подготовки клиента Microsoft 365.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="d4dc2-114">Set up your developer subscription and configure it through [prepare your Microsoft 365 Tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

## <a name="test-and-debug"></a><span data-ttu-id="d4dc2-115">Тестирование и отладка</span><span class="sxs-lookup"><span data-stu-id="d4dc2-115">Test and debug</span></span>

<span data-ttu-id="d4dc2-116">Чтобы протестировать и отлагировать приложение, необходимо создать хотя бы одно рабочее пространство.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-116">To test and debug your app, you must create at least one workspace.</span></span> <span data-ttu-id="d4dc2-117">Вы можете выбрать тестовую установку, например локальный хост или облачный хост для тестирования и отлаговки приложения.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-117">You can select a test setup, such as local host or cloud-based host to test and debug the app.</span></span> <span data-ttu-id="d4dc2-118">Рекомендации по отлажению приложения Teams предоставляются для загрузки и запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-118">Guidance to debug your Teams app is provided to load and run your app experience.</span></span> <span data-ttu-id="d4dc2-119">Дополнительные сведения см. в дополнительных сведениях о настройках и запуске приложения [Microsoft Teams.](~/concepts/build-and-test/debug.md)</span><span class="sxs-lookup"><span data-stu-id="d4dc2-119">For more information, see [choose a set up and run your Microsoft Teams app](~/concepts/build-and-test/debug.md).</span></span>

<span data-ttu-id="d4dc2-120">Протестировать бот локально.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-120">Test your bot locally.</span></span> <span data-ttu-id="d4dc2-121">Дополнительные сведения см. [в примере отламывка](~/bots/how-to/debug/locally-with-an-ide.md)бота локально с помощью IDE.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-121">For more information, see [debug your bot locally with an IDE](~/bots/how-to/debug/locally-with-an-ide.md).</span></span> <span data-ttu-id="d4dc2-122">Вы также можете отстраить бота с помощью [среднего поверки и](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) [адаптивного средства проверки.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="d4dc2-122">You can also debug your bot with [inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) and [adaptive tools](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).</span></span> 

<span data-ttu-id="d4dc2-123">Чтобы просмотреть журналы консоли, просмотреть или изменить запросы html, css и сетевые запросы во время выполнения, добавьте точки разрывов в код JavaScript и выполните интерактивный отладки доступа к DevTools.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-123">To view the console logs, view or modify html, css, and network requests during runtime, add breakpoints to your JavaScript code, and perform interactive debugging access the DevTools.</span></span> <span data-ttu-id="d4dc2-124">Дополнительные сведения см. в [вкладке Access the DevTools for Teams.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="d4dc2-124">For more information, see [Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md).</span></span> 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a><span data-ttu-id="d4dc2-125">Добавление тестовых данных в клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="d4dc2-125">Add test data to your Microsoft 365 tenant</span></span>

<span data-ttu-id="d4dc2-126">Добавьте тестовые данные в тестовый клиент Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-126">Add the test data to Microsoft 365 test tenant.</span></span> <span data-ttu-id="d4dc2-127">Дополнительные сведения см. в дополнительных сведениях о добавлении тестовых данных в тестовый клиент [Office 365](~/concepts/build-and-test/test-data.md)и выполните все необходимые условия перед отправкой тестовых данных.</span><span class="sxs-lookup"><span data-stu-id="d4dc2-127">For more information, see [add test data to your Office 365 test tenant](~/concepts/build-and-test/test-data.md), and complete all the prerequisites before you start uploading your test data.</span></span>

## <a name="see-also"></a><span data-ttu-id="d4dc2-128">См. также</span><span class="sxs-lookup"><span data-stu-id="d4dc2-128">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d4dc2-129">Отламывка вкладки</span><span class="sxs-lookup"><span data-stu-id="d4dc2-129">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="d4dc2-130">Отламывка ботов</span><span class="sxs-lookup"><span data-stu-id="d4dc2-130">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="d4dc2-131">Тестирование разрешений RSC</span><span class="sxs-lookup"><span data-stu-id="d4dc2-131">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a><span data-ttu-id="d4dc2-132">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="d4dc2-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d4dc2-133">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="d4dc2-133">Prepare your Microsoft 365 tenant</span></span>](~/concepts/build-and-test/prepare-your-o365-tenant.md)