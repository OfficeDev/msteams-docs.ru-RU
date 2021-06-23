---
title: Готовые к работе соединители
description: Управление рабочей силой смещает соединители для Teams
ms.topic: reference
author: surbhigupta
ms.date: 03/09/2020
localization_priority: Normal
keywords: Microsoft Teams кронос соединители
ms.author: lajanuar
ms.openlocfilehash: 088c049342c36b4f126b4a9d2f788601378b7db4
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069144"
---
# <a name="production-ready-shifts-connectors"></a><span data-ttu-id="257a6-104">Готовые к работе соединители</span><span class="sxs-lookup"><span data-stu-id="257a6-104">Production-ready Shifts Connectors</span></span>  

<span data-ttu-id="257a6-105">Teams Соединители управления рабочей силой shifts (WFM) — это готовые к работе, открытые и управляемые сообществом интеграции, полезные для сотрудников firstline.</span><span class="sxs-lookup"><span data-stu-id="257a6-105">Teams Shifts Workforce management (WFM) connectors are production-ready, open-source, and community-driven integrations, useful for firstline workers.</span></span> <span data-ttu-id="257a6-106">Они обеспечивают бесперебойную обработку и быстрый процесс цифровой трансформации сотрудников firstline с помощью Teams Shifts.</span><span class="sxs-lookup"><span data-stu-id="257a6-106">They offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span> 

<span data-ttu-id="257a6-107">Каждый соединитатель предоставляет подробные рекомендации по развертыванию и интеграции в организации.</span><span class="sxs-lookup"><span data-stu-id="257a6-107">Each connector provides detailed guidance for deployment and integration to your organization.</span></span> <span data-ttu-id="257a6-108">Полный исходный код доступен в GitHub репозитории.</span><span class="sxs-lookup"><span data-stu-id="257a6-108">The complete source code is available in GitHub repository.</span></span> <span data-ttu-id="257a6-109">Вы можете подробно изучить или вилкой, а также настроить для удовлетворения ваших конкретных потребностей.</span><span class="sxs-lookup"><span data-stu-id="257a6-109">You can explore in detail or fork, and customize to meet your specific needs.</span></span>   

<span data-ttu-id="257a6-110">В этом документе представлен обзор ключевых преимуществ соединители WFM Teams Shifts, соединители Kronos-to-Teams Shifts и соединители JDA-к-Teams Shifts.</span><span class="sxs-lookup"><span data-stu-id="257a6-110">This document gives an overview of key benefits of Teams Shifts WFM connectors, Kronos-to-Teams Shifts connector, and JDA-to-Teams Shifts connector.</span></span>

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a><span data-ttu-id="257a6-111">Основные преимущества соединители Teams WFM</span><span class="sxs-lookup"><span data-stu-id="257a6-111">Key benefits of Teams Shifts WFM connectors</span></span>

<span data-ttu-id="257a6-112">Ниже ключевых преимуществ соединители Teams WFM:</span><span class="sxs-lookup"><span data-stu-id="257a6-112">Following are the key benefits of Teams Shifts WFM connectors:</span></span>

* <span data-ttu-id="257a6-113">**Подключение и воспроизведения:** Все соединители WFM Shifts включают ARM сценарии развертывания Azure, которые позволяют развертывать все необходимые службы в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="257a6-113">**Plug and play experience:** All Shifts WFM connectors include ARM Azure deployment scripts that allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="257a6-114">Для развертывания приложений не требуется кодирование.</span><span class="sxs-lookup"><span data-stu-id="257a6-114">No coding is required to deploy the apps.</span></span>

* <span data-ttu-id="257a6-115">**Код, готовый к производству:** Все соединители Shifts соответствуют рекомендуемой практике безопасности и инфраструктуры, и все внесенные в сообщество изменения рассматриваются для обеспечения дальнейшего соответствия.</span><span class="sxs-lookup"><span data-stu-id="257a6-115">**Production-ready code:** All  Shifts connectors conform to the recommended security and infrastructure best practices and all community-submitted changes are reviewed to ensure continued conformance.</span></span>

* <span data-ttu-id="257a6-116">**Настраиваемые и размязывные:**   Хотя все соединители WFM Shifts готовы к развертыванию для немедленного использования, вся база кода и сценарии развертывания доступны.</span><span class="sxs-lookup"><span data-stu-id="257a6-116">**Customizable and extensible:**  While all Shifts WFM connectors are ready to deploy for immediate use, with the entire code base and deployment scripts readily available.</span></span> <span data-ttu-id="257a6-117">Вы можете легко настроить или расширить их, чтобы соответствовать вашим уникальным потребностям.</span><span class="sxs-lookup"><span data-stu-id="257a6-117">You can easily customize or extend them to fit your unique needs.</span></span>

* <span data-ttu-id="257a6-118">**Подробная документация & поддержки:**   Все соединители WFM Shifts сопровождаются документацией по архитектуре решений, развертыванию и этапу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="257a6-118">**Detailed documentation & support:**  All Shifts WFM connectors are accompanied by end-to-end documentation for solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="257a6-119">Репозитории соединители отслеживаются, чтобы вы могли сообщать о любых проблемах, проблемах или трудностях, с которыми вы сталкиваетесь с помощью отслеживания GitHub проблем репо.</span><span class="sxs-lookup"><span data-stu-id="257a6-119">The connector repositories are monitored, so that you can report any issues, challenges or difficulties you encounter through the repo's GitHub Issues tracker.</span></span>

* <span data-ttu-id="257a6-120">**Бесшовная интеграция:** Интеграция решений WFM и Teams Shifts позволяет сотрудникам firstline использовать приложение Teams Shifts для просмотра или управления расписанием и временем смены, а также использовать все другие функции совместной работы, предоставляемые в Teams прямо с мобильного устройства или рабочего стола без необходимости переключения контекста на другое приложение.</span><span class="sxs-lookup"><span data-stu-id="257a6-120">**Seamless integration:** The integration between WFM solutions and Teams Shifts allows firstline workers to use the Teams Shifts app to view or manage their schedules and shift times, and use all the other rich collaboration features provided in Teams right from their mobile device or desktop without having to switch context to another app.</span></span>  

<span data-ttu-id="257a6-121">**Просмотр открытых сдвигов в Teams**</span><span class="sxs-lookup"><span data-stu-id="257a6-121">**Open shifts view in Teams**</span></span> 

<span data-ttu-id="257a6-122">Представление сдвигов в Teams отображается на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="257a6-122">The shifts view in Teams is shown in the following image:</span></span> 

![Открытые сдвиги в Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a><span data-ttu-id="257a6-124">Разъем Kronos-to-Teams Shifts</span><span class="sxs-lookup"><span data-stu-id="257a6-124">Kronos-to-Teams Shifts connector</span></span>

<span data-ttu-id="257a6-125">С помощью кода с открытым исходным кодом можно интегрировать центральную версию Kronos Workforce 8.1 и выше с помощью Teams Shifts, например, приложения для настольных компьютеров или мобильных Teams для следующих сценариев работы и руководителя первой линии:</span><span class="sxs-lookup"><span data-stu-id="257a6-125">With open-source code, you can integrate Kronos Workforce Central Version 8.1 and above, with Teams Shifts such as, desktop or mobile Teams app for the following firstline worker and manager scenarios:</span></span>

* <span data-ttu-id="257a6-126">Просмотр расписания.</span><span class="sxs-lookup"><span data-stu-id="257a6-126">View schedule.</span></span>

* <span data-ttu-id="257a6-127">Публикация и запрос открытых смен.</span><span class="sxs-lookup"><span data-stu-id="257a6-127">Publish and request open shifts.</span></span>

* <span data-ttu-id="257a6-128">Смены.</span><span class="sxs-lookup"><span data-stu-id="257a6-128">Swap shifts.</span></span>

* <span data-ttu-id="257a6-129">Запросить время отключки.</span><span class="sxs-lookup"><span data-stu-id="257a6-129">Request time off.</span></span>

* <span data-ttu-id="257a6-130">Предложение сдвигов.</span><span class="sxs-lookup"><span data-stu-id="257a6-130">Offer shifts.</span></span>

<span data-ttu-id="257a6-131">Дополнительные сведения о развертывании соединиттеля "Kronos-to-Teams Shifts" см. в [GitHub.](https://aka.ms/KronosShiftsConnector)</span><span class="sxs-lookup"><span data-stu-id="257a6-131">For more information on deployment of Kronos-to-Teams Shifts connector, see [Get it on GitHub](https://aka.ms/KronosShiftsConnector).</span></span>

## <a name="jda-to-teams-shifts-connector"></a><span data-ttu-id="257a6-132">Соединители JDA-Teams Shifts</span><span class="sxs-lookup"><span data-stu-id="257a6-132">JDA-to-Teams Shifts connector</span></span>

<span data-ttu-id="257a6-133">С открытым исходным кодом можно интегрировать JDA, например BlueYonder Version 17.2 и выше, с Teams Shifts such as, desktop or mobile Teams app для следующих сценариев сотрудников и менеджеров первой линии:</span><span class="sxs-lookup"><span data-stu-id="257a6-133">With open-source code, you can integrate JDA, such as BlueYonder Version 17.2 and above, with Teams Shifts  such as, desktop or mobile Teams app for the following firstline worker and manager scenarios:</span></span>

* <span data-ttu-id="257a6-134">Публикация смен и групп расписания в JDA и просмотр их в Teams.</span><span class="sxs-lookup"><span data-stu-id="257a6-134">Publish shifts and schedule groups in JDA and view them in Teams.</span></span>

* <span data-ttu-id="257a6-135">Включить богатые сценарии планирования, включая запрос смены и отопить.</span><span class="sxs-lookup"><span data-stu-id="257a6-135">Enable rich scheduling scenarios, including requesting shift swaps and time off.</span></span>

* <span data-ttu-id="257a6-136">Установите доступность пользователей с помощью [API microsoft Graph для Shifts.](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="257a6-136">Set user availability using the [Microsoft Graph API for Shifts](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true).</span></span>

<span data-ttu-id="257a6-137">Дополнительные сведения о вкладе и предложении см. в [GitHub.](https://aka.ms/JDAShiftsConnector)</span><span class="sxs-lookup"><span data-stu-id="257a6-137">For more information on contribution and suggestion, see [Get it on GitHub](https://aka.ms/JDAShiftsConnector).</span></span></br></br>

## <a name="see-also"></a><span data-ttu-id="257a6-138">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="257a6-138">See also</span></span>

[<span data-ttu-id="257a6-139">Интеграция веб-приложений</span><span class="sxs-lookup"><span data-stu-id="257a6-139">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
