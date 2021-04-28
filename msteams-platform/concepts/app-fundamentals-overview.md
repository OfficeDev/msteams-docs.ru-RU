---
title: Обзор основ разработки приложений
author: heath-hamilton
description: Опишите основные концепции разработки платформы Teams.
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 6d0c22049e828426cfe963da6631b4c289566bf0
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058462"
---
# <a name="microsoft-teams-app-development-fundamentals"></a><span data-ttu-id="9dfe2-103">Основы разработки приложений Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9dfe2-103">Microsoft Teams app development fundamentals</span></span>

<span data-ttu-id="9dfe2-104">Основы приложения Microsoft Teams дают направление, необходимое для создания настраиваемой команды приложения.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-104">Microsoft Teams app fundamentals give the direction you need to create your custom Teams app.</span></span> <span data-ttu-id="9dfe2-105">Вы можете распознать рамки, необходимые для планирования приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-105">You can recognize the framework required to plan your Teams app.</span></span> <span data-ttu-id="9dfe2-106">Документ помогает понять коммуникацию пользователя и приложения и выяснить, какие поверхности приложения необходимо использовать или API, которые могут потребоваться вашему приложению в процессе.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-106">The document helps you to understand the user-app communication and figure out the kind of app surfaces you need to use or the APIs your app might require in the process.</span></span> <span data-ttu-id="9dfe2-107">Получите некоторое вдохновение, чтобы принять интерактивность, которая может углубить взаимодействие с приложением при интеграции с Teams.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-107">Get some inspiration to embrace interactivity that can deepen the app experience when you integrate with Teams.</span></span>

## <a name="capabilities-and-entry-points"></a><span data-ttu-id="9dfe2-108">Возможности и точки входа</span><span class="sxs-lookup"><span data-stu-id="9dfe2-108">Capabilities and entry points</span></span>

<span data-ttu-id="9dfe2-109">Вы можете расширить приложение Teams несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-109">You can extend your Teams app in multiple ways.</span></span> <span data-ttu-id="9dfe2-110">Чтобы расширить приложение, необходимо понимать все основные возможности и точки входа, которые работают в совместном пространстве.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-110">To be able to extend your app you must understand all the core capabilities and the entry points that work in a collaborative space.</span></span> <span data-ttu-id="9dfe2-111">Вы можете поэкспериментировать с точками расширения для создания приложений.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-111">You can experiment with the extension points for building your apps.</span></span> <span data-ttu-id="9dfe2-112">Важные компоненты проекта приложения помогают правильно настроить страницу приложения.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-112">Important app project components help you to correctly configure your app page.</span></span> <span data-ttu-id="9dfe2-113">Приложение Teams может иметь [несколько возможностей и](../concepts/capabilities-overview.md) [точки входа.](../concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="9dfe2-113">Teams app can have [multiple capabilities](../concepts/capabilities-overview.md) and [entry points](../concepts/extensibility-points.md).</span></span>

## <a name="understand-your-use-cases"></a><span data-ttu-id="9dfe2-114">Анализ вариантов использования</span><span class="sxs-lookup"><span data-stu-id="9dfe2-114">Understand your use cases</span></span>

<span data-ttu-id="9dfe2-115">Вы можете распознать проблемы пользователей и определить ответы на некоторые распространенные проблемы, с которыми сталкиваются пользователи.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-115">You can recognize user issues and identify the answers to some common problems the users face.</span></span> <span data-ttu-id="9dfe2-116">Вы можете создать приложение Teams, найдя правильное сочетание для удовлетворения потребностей пользователя.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-116">You can build your Teams app by finding the right combination to meet your user's needs.</span></span> <span data-ttu-id="9dfe2-117">[Используйте случаи,](../concepts/design/understand-use-cases.md) чтобы узнать, как конечный пользователь взаимодействует с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-117">[Understand use cases](../concepts/design/understand-use-cases.md) to know how an end-user interacts with your app.</span></span> <span data-ttu-id="9dfe2-118">Вы научитесь понимать пользователя и его проблему.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-118">You learn to understand the user and their problem.</span></span> <span data-ttu-id="9dfe2-119">Ответы на некоторые распространенные вопросы следуют следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9dfe2-119">Some common questions answered are as follows:</span></span>

* <span data-ttu-id="9dfe2-120">Нужна ли проверка подлинности?</span><span class="sxs-lookup"><span data-stu-id="9dfe2-120">Do you need authentication?</span></span>
* <span data-ttu-id="9dfe2-121">Какие проблемы будет решать ваше приложение?</span><span class="sxs-lookup"><span data-stu-id="9dfe2-121">What problem is your app going to solve?</span></span>
* <span data-ttu-id="9dfe2-122">Кто конечные пользователи приложения?</span><span class="sxs-lookup"><span data-stu-id="9dfe2-122">Who are the end-users of the app?</span></span>
* <span data-ttu-id="9dfe2-123">Каким должен быть опыт работы с бортом и что еще может сделать приложение?</span><span class="sxs-lookup"><span data-stu-id="9dfe2-123">How should the onboarding experience be and what else the app can do?</span></span>

## <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="9dfe2-124">Соединая карта случаев использования с возможностями приложений Teams</span><span class="sxs-lookup"><span data-stu-id="9dfe2-124">Map your use cases to Teams app capabilities</span></span>

<span data-ttu-id="9dfe2-125">[Карта случаев использования охватывает](../concepts/design/map-use-cases.md) некоторые распространенные сценарии и выбор возможностей приложения.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-125">[Map your use cases](../concepts/design/map-use-cases.md) covers some common scenarios and how to choose your app's capabilities.</span></span> <span data-ttu-id="9dfe2-126">Предоставляются сведения для совместной работы приложения и совместной работы с элементами во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-126">Information to share your app and collaborate on items in an external system is provided.</span></span> <span data-ttu-id="9dfe2-127">Вы также можете узнать, как инициировать рабочий процесс и отправлять уведомления пользователям.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-127">You can also learn how to initiate workflows and send notifications to users.</span></span> <span data-ttu-id="9dfe2-128">Дополнительные советы о том, с чего начать, как получить социальные связи с пользователями, беседующие боты и сочетание нескольких функций.</span><span class="sxs-lookup"><span data-stu-id="9dfe2-128">Get additional tips on where to start, how to get social with users, conversational bots, and combining multiple features.</span></span>

## <a name="see-also"></a><span data-ttu-id="9dfe2-129">См. также</span><span class="sxs-lookup"><span data-stu-id="9dfe2-129">See also</span></span>

- [<span data-ttu-id="9dfe2-130">Интеграция веб-приложений с Teams</span><span class="sxs-lookup"><span data-stu-id="9dfe2-130">Integrate web apps with Teams</span></span>](../samples/integrating-web-apps.md)

- [<span data-ttu-id="9dfe2-131">Создайте свое первое приложение Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9dfe2-131">Build your first Microsoft Teams app</span></span>](../build-your-first-app/build-first-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="9dfe2-132">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="9dfe2-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9dfe2-133">Понимание возможностей приложений Teams</span><span class="sxs-lookup"><span data-stu-id="9dfe2-133">Understand Teams app capabilities</span></span>](capabilities-overview.md)

