---
title: Проверьте обзор приложения
description: Описывает процесс проверки пользовательского Teams в Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Настройка Microsoft 365 для Teams тестирования приложения
ms.openlocfilehash: 2c9f23a5c6ae286ff4b7d911f370bd45b854a647
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565188"
---
# <a name="test-your-app"></a><span data-ttu-id="f4824-104">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="f4824-104">Test your app</span></span>

<span data-ttu-id="f4824-105">После интеграции приложения с Microsoft Teams, вы должны проверить свое приложение перед публикацией.</span><span class="sxs-lookup"><span data-stu-id="f4824-105">After integrating your app with Microsoft Teams, you must test your app before publishing it.</span></span> <span data-ttu-id="f4824-106">Конечная цель состоит в том, чтобы получить как можно больше пользователей для вашего приложения, поэтому убедитесь, что тестирование приложения на нескольких устройствах, которые пользователи могут использовать.</span><span class="sxs-lookup"><span data-stu-id="f4824-106">The ultimate goal is to get as many users for your app, therefore, ensure to test the app on multiple devices that users could use.</span></span> <span data-ttu-id="f4824-107">Для тестирования приложения:</span><span class="sxs-lookup"><span data-stu-id="f4824-107">For testing your app:</span></span>

* <span data-ttu-id="f4824-108">Подготовь Microsoft 365 арендатора.</span><span class="sxs-lookup"><span data-stu-id="f4824-108">Prepare your Microsoft 365 tenant.</span></span>
* <span data-ttu-id="f4824-109">Выберите рабочее пространство для тестирования и отладки приложения.</span><span class="sxs-lookup"><span data-stu-id="f4824-109">Choose a workspace to test and debug your app.</span></span>
* <span data-ttu-id="f4824-110">Добавьте тестовые данные к Microsoft 365 арендатору.</span><span class="sxs-lookup"><span data-stu-id="f4824-110">Add test data to your Microsoft 365 tenant.</span></span>

## <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="f4824-111">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="f4824-111">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="f4824-112">Перед началом тестирования приложения подготовьте Microsoft 365 и включите пользовательские Teams, позволяющие загружать приложение.</span><span class="sxs-lookup"><span data-stu-id="f4824-112">Before you start testing your app, prepare your Microsoft 365 test tenant and enable custom Teams app allow you to upload your app.</span></span> <span data-ttu-id="f4824-113">Вы должны зарегистрироваться для Microsoft 365 разработчика и управлять настройками Teams для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="f4824-113">You must sign-up for Microsoft 365 developer program and manage the Teams settings for your organization.</span></span> <span data-ttu-id="f4824-114">Настройте подписку разработчика и настройте ее через [подготовку Microsoft 365 арендатора.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="f4824-114">Set up your developer subscription and configure it through [prepare your Microsoft 365 Tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

## <a name="test-and-debug"></a><span data-ttu-id="f4824-115">Тестирование и отладка</span><span class="sxs-lookup"><span data-stu-id="f4824-115">Test and debug</span></span>

<span data-ttu-id="f4824-116">Чтобы протестировать и отладить приложение, необходимо создать по крайней мере одно рабочее пространство.</span><span class="sxs-lookup"><span data-stu-id="f4824-116">To test and debug your app, you must create at least one workspace.</span></span> <span data-ttu-id="f4824-117">Вы можете выбрать настройку тестирования, например локального хоста или облачного хоста, чтобы протестировать и отладить приложение.</span><span class="sxs-lookup"><span data-stu-id="f4824-117">You can select a test setup, such as local host or cloud-based host to test and debug the app.</span></span> <span data-ttu-id="f4824-118">Руководство по отладке Teams приложения предоставляется для загрузки и запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="f4824-118">Guidance to debug your Teams app is provided to load and run your app experience.</span></span> <span data-ttu-id="f4824-119">Для получения дополнительной [информации можно выбрать настройку и запустить Microsoft Teams приложение.](~/concepts/build-and-test/debug.md)</span><span class="sxs-lookup"><span data-stu-id="f4824-119">For more information, see [choose a set up and run your Microsoft Teams app](~/concepts/build-and-test/debug.md).</span></span>

<span data-ttu-id="f4824-120">Проверьте своего бота локально.</span><span class="sxs-lookup"><span data-stu-id="f4824-120">Test your bot locally.</span></span> <span data-ttu-id="f4824-121">Для получения дополнительной информации [см.](~/bots/how-to/debug/locally-with-an-ide.md)</span><span class="sxs-lookup"><span data-stu-id="f4824-121">For more information, see [debug your bot locally with an IDE](~/bots/how-to/debug/locally-with-an-ide.md).</span></span> <span data-ttu-id="f4824-122">Вы также можете отладить ваш бот с [инспекцией среднего программного обеспечения и](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) [адаптивных инструментов.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f4824-122">You can also debug your bot with [inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) and [adaptive tools](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).</span></span> 

<span data-ttu-id="f4824-123">Для просмотра журналов консолей, просмотра или изменения HTML, css и сетевых запросов во время выполнения добавьте точки разрыва в код JavaScript и выполните интерактивную отладку доступа к DevTools.</span><span class="sxs-lookup"><span data-stu-id="f4824-123">To view the console logs, view or modify html, css, and network requests during runtime, add breakpoints to your JavaScript code, and perform interactive debugging access the DevTools.</span></span> <span data-ttu-id="f4824-124">Для получения дополнительной [информации, см. Доступ к DevTools для Teams вкладок](~/tabs/how-to/developer-tools.md).</span><span class="sxs-lookup"><span data-stu-id="f4824-124">For more information, see [Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md).</span></span> 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a><span data-ttu-id="f4824-125">Добавление тестовых данных к Microsoft 365 арендатору</span><span class="sxs-lookup"><span data-stu-id="f4824-125">Add test data to your Microsoft 365 tenant</span></span>

<span data-ttu-id="f4824-126">Добавьте тестовые данные Microsoft 365 тест-арендатора.</span><span class="sxs-lookup"><span data-stu-id="f4824-126">Add the test data to Microsoft 365 test tenant.</span></span> <span data-ttu-id="f4824-127">Для получения дополнительной [информации, с Office 365 м.](~/concepts/build-and-test/test-data.md)</span><span class="sxs-lookup"><span data-stu-id="f4824-127">For more information, see [add test data to your Office 365 test tenant](~/concepts/build-and-test/test-data.md), and complete all the prerequisites before you start uploading your test data.</span></span>

## <a name="see-also"></a><span data-ttu-id="f4824-128">См. также</span><span class="sxs-lookup"><span data-stu-id="f4824-128">See also</span></span>

- [<span data-ttu-id="f4824-129">Отладить вкладку</span><span class="sxs-lookup"><span data-stu-id="f4824-129">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
 
- [<span data-ttu-id="f4824-130">Отладить ботов</span><span class="sxs-lookup"><span data-stu-id="f4824-130">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)

- [<span data-ttu-id="f4824-131">Тестовые разрешения RSC</span><span class="sxs-lookup"><span data-stu-id="f4824-131">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a><span data-ttu-id="f4824-132">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="f4824-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4824-133">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="f4824-133">Prepare your Microsoft 365 tenant</span></span>](~/concepts/build-and-test/prepare-your-o365-tenant.md)
