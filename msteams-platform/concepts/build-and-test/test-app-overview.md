---
title: Проверка обзора приложения
description: Описывает процесс тестирования настраиваемого Teams в Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Настройка Microsoft 365 клиента Teams загрузки тестового приложения
ms.openlocfilehash: 2c9f23a5c6ae286ff4b7d911f370bd45b854a647
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565188"
---
# <a name="test-your-app"></a><span data-ttu-id="8081b-104">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="8081b-104">Test your app</span></span>

<span data-ttu-id="8081b-105">После интеграции приложения с Microsoft Teams необходимо протестировать приложение перед его публикацией.</span><span class="sxs-lookup"><span data-stu-id="8081b-105">After integrating your app with Microsoft Teams, you must test your app before publishing it.</span></span> <span data-ttu-id="8081b-106">Конечная цель состоит в том, чтобы получить как можно больше пользователей для вашего приложения, поэтому убедитесь, что приложение тестировать на нескольких устройствах, которые пользователи могут использовать.</span><span class="sxs-lookup"><span data-stu-id="8081b-106">The ultimate goal is to get as many users for your app, therefore, ensure to test the app on multiple devices that users could use.</span></span> <span data-ttu-id="8081b-107">Для тестирования приложения:</span><span class="sxs-lookup"><span data-stu-id="8081b-107">For testing your app:</span></span>

* <span data-ttu-id="8081b-108">Подготовка Microsoft 365 клиента.</span><span class="sxs-lookup"><span data-stu-id="8081b-108">Prepare your Microsoft 365 tenant.</span></span>
* <span data-ttu-id="8081b-109">Выберите рабочее пространство для тестирования и отлаговки приложения.</span><span class="sxs-lookup"><span data-stu-id="8081b-109">Choose a workspace to test and debug your app.</span></span>
* <span data-ttu-id="8081b-110">Добавьте тестовые данные в Microsoft 365 клиента.</span><span class="sxs-lookup"><span data-stu-id="8081b-110">Add test data to your Microsoft 365 tenant.</span></span>

## <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="8081b-111">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="8081b-111">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="8081b-112">Прежде чем приступить к тестированию приложения, Microsoft 365 тестовый клиент и включить настраиваемые Teams, которые позволяют загружать приложение.</span><span class="sxs-lookup"><span data-stu-id="8081b-112">Before you start testing your app, prepare your Microsoft 365 test tenant and enable custom Teams app allow you to upload your app.</span></span> <span data-ttu-id="8081b-113">Необходимо зарегистрироваться для Microsoft 365 разработчика и управлять Teams параметров для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8081b-113">You must sign-up for Microsoft 365 developer program and manage the Teams settings for your organization.</span></span> <span data-ttu-id="8081b-114">Настройте подписку разработчика и настройте ее путем [подготовки Microsoft 365 клиента.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="8081b-114">Set up your developer subscription and configure it through [prepare your Microsoft 365 Tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

## <a name="test-and-debug"></a><span data-ttu-id="8081b-115">Тестирование и отладка</span><span class="sxs-lookup"><span data-stu-id="8081b-115">Test and debug</span></span>

<span data-ttu-id="8081b-116">Чтобы протестировать и отлагировать приложение, необходимо создать хотя бы одно рабочее пространство.</span><span class="sxs-lookup"><span data-stu-id="8081b-116">To test and debug your app, you must create at least one workspace.</span></span> <span data-ttu-id="8081b-117">Вы можете выбрать тестовую установку, например локальный хост или облачный хост для тестирования и отлаговки приложения.</span><span class="sxs-lookup"><span data-stu-id="8081b-117">You can select a test setup, such as local host or cloud-based host to test and debug the app.</span></span> <span data-ttu-id="8081b-118">Рекомендации по отлажению Teams приложения для загрузки и запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="8081b-118">Guidance to debug your Teams app is provided to load and run your app experience.</span></span> <span data-ttu-id="8081b-119">Дополнительные сведения см. [в дополнительных сведениях о](~/concepts/build-and-test/debug.md)настройках и запуске Microsoft Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="8081b-119">For more information, see [choose a set up and run your Microsoft Teams app](~/concepts/build-and-test/debug.md).</span></span>

<span data-ttu-id="8081b-120">Протестировать бот локально.</span><span class="sxs-lookup"><span data-stu-id="8081b-120">Test your bot locally.</span></span> <span data-ttu-id="8081b-121">Дополнительные сведения см. [в примере отламывка](~/bots/how-to/debug/locally-with-an-ide.md)бота локально с помощью IDE.</span><span class="sxs-lookup"><span data-stu-id="8081b-121">For more information, see [debug your bot locally with an IDE](~/bots/how-to/debug/locally-with-an-ide.md).</span></span> <span data-ttu-id="8081b-122">Вы также можете отстраить бота с помощью [среднего поверки и](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) [адаптивного средства проверки.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8081b-122">You can also debug your bot with [inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) and [adaptive tools](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).</span></span> 

<span data-ttu-id="8081b-123">Чтобы просмотреть журналы консоли, просмотреть или изменить запросы html, css и сетевые запросы во время выполнения, добавьте точки разрывов в код JavaScript и выполните интерактивный отладки доступа к DevTools.</span><span class="sxs-lookup"><span data-stu-id="8081b-123">To view the console logs, view or modify html, css, and network requests during runtime, add breakpoints to your JavaScript code, and perform interactive debugging access the DevTools.</span></span> <span data-ttu-id="8081b-124">Дополнительные сведения см. [в вкладки Access the DevTools для Teams.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="8081b-124">For more information, see [Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md).</span></span> 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a><span data-ttu-id="8081b-125">Добавление тестовых данных в Microsoft 365 клиента</span><span class="sxs-lookup"><span data-stu-id="8081b-125">Add test data to your Microsoft 365 tenant</span></span>

<span data-ttu-id="8081b-126">Добавьте тестовые данные в Microsoft 365 тестовый клиент.</span><span class="sxs-lookup"><span data-stu-id="8081b-126">Add the test data to Microsoft 365 test tenant.</span></span> <span data-ttu-id="8081b-127">Дополнительные сведения см. в дополнительных сведениях о добавлении [тестовых](~/concepts/build-and-test/test-data.md)данных в Office 365 тестовый клиент и выполните все необходимые условия перед отправкой тестовых данных.</span><span class="sxs-lookup"><span data-stu-id="8081b-127">For more information, see [add test data to your Office 365 test tenant](~/concepts/build-and-test/test-data.md), and complete all the prerequisites before you start uploading your test data.</span></span>

## <a name="see-also"></a><span data-ttu-id="8081b-128">См. также</span><span class="sxs-lookup"><span data-stu-id="8081b-128">See also</span></span>

- [<span data-ttu-id="8081b-129">Отламывка вкладки</span><span class="sxs-lookup"><span data-stu-id="8081b-129">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
 
- [<span data-ttu-id="8081b-130">Отламывка ботов</span><span class="sxs-lookup"><span data-stu-id="8081b-130">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)

- [<span data-ttu-id="8081b-131">Тестирование разрешений RSC</span><span class="sxs-lookup"><span data-stu-id="8081b-131">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a><span data-ttu-id="8081b-132">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="8081b-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8081b-133">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="8081b-133">Prepare your Microsoft 365 tenant</span></span>](~/concepts/build-and-test/prepare-your-o365-tenant.md)
