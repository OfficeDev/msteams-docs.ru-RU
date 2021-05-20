---
title: Microsoft Teams шаблоны приложений
description: Ссылки и описания шаблонов приложений для Microsoft Teams платформы
ms.topic: reference
keywords: Microsoft Teams шаблонов демо
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 8cfb066ee3c202fb8611a61bbde3058207a62a35
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566344"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="8ea4c-104">Шаблоны приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8ea4c-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="8ea4c-105">Шаблоны приложений являются примерами полных приложений для Microsoft Teams которые с открытым исходным кодом и доступны на GitHub.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="8ea4c-106">Каждый шаблон приложения содержит подробные инструкции по развертыванию и установке этого приложения для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="8ea4c-107">Он также предоставляет образец приложения, которое можно установить и начать использовать немедленно.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-107">It also provides a sample app that you can install and start using immediately.</span></span> <span data-ttu-id="8ea4c-108">Также доступен полный исходный код, который позволяет детально изучить его или раскошелиться на код и изменить его в соответствии с вашими конкретными требованиями.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-108">The complete source code is also available, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="8ea4c-109">Все шаблоны приложений предоставляются в соответствии с [условиями лицензии MIT.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>

> [!NOTE] 
> <span data-ttu-id="8ea4c-110">Необходимо лицензировать и поддерживать приложения, созданные из шаблонов приложений для пользователей и организаций.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-110">You must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="8ea4c-111">**&#9734; указывает на недавно выпущенные шаблоны приложений.**</span><span class="sxs-lookup"><span data-stu-id="8ea4c-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="8ea4c-112">Основные преимущества</span><span class="sxs-lookup"><span data-stu-id="8ea4c-112">Key benefits</span></span>

* <span data-ttu-id="8ea4c-113">**Развертывание непосредственно в облаке:** Все шаблоны приложений включают скрипты развертывания, которые позволяют разместить все необходимые службы в Microsoft Azure или Power Platform.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="8ea4c-114">**Рекомендуемый пример кода:** Шаблоны приложений соответствуют рекомендуемой рекомендации по безопасности и инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="8ea4c-115">Все сообщества, представленные изменения в шаблоны приложений, рассматриваются для обеспечения соответствия.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="8ea4c-116">**Настраиваемый и смягчающий:** В то время как все шаблоны приложений развернуты с минимальной конфигурацией, вся база кода и сценарии развертывания предоставляются, так что вы можете легко настроить или расширить их в соответствует вашим уникальным потребностям.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-116">**Customizable and extensible:** While all app templates are deployed with minimal configuration, the entire code base and deployment scripts are provided, so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="8ea4c-117">**Подробная документация:** Все шаблоны приложений сопровождаются (по-к-к-к-к-) документацией по архитектуре решений, развертыванию и шагам конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot"></a><span data-ttu-id="8ea4c-118">Усыновление Бот</span><span class="sxs-lookup"><span data-stu-id="8ea4c-118">Adoption Bot</span></span> 

<span data-ttu-id="8ea4c-119">Adoption Bot - это чат-бот для ухода за пользователями, построенный с помощью Power Virtual Agent для Teams PVA.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams PVA.</span></span> <span data-ttu-id="8ea4c-120">Он рассматривается как PVA версия часто задаваемых вопросов Плюс.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-120">It is considered as the PVA version of FAQ Plus.</span></span> <span data-ttu-id="8ea4c-121">Усыновление Бот отвечает на 100 "общие вопросы о Microsoft 365 и Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="8ea4c-122">Вы можете редактировать существующие темы, добавлять свои собственные темы и заиметь существующие часто задаваемые вопросы.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-122">You can edit the existing topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="8ea4c-123">Если пользователи нуждаются в дополнительной помощи, Adoption Bot может подключить их к экспертам или даже быть расширена, чтобы открыть сервисные билеты с премиум разъемы потока.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.</span></span> <span data-ttu-id="8ea4c-124">Этот бот самостоятельно установлен или встроен в пользовательское приложение, например, [концентратор усыновления.](https://github.com/akporzondek/adoption_hub)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-124">This bot is self-installed or built into a custom app, such as the [Adoption Hub](https://github.com/akporzondek/adoption_hub).</span></span>

[<span data-ttu-id="8ea4c-125">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-125">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="adoption-tool--champion-management-platform-9734"></a><span data-ttu-id="8ea4c-126">Инструмент принятия - Платформа управления чемпионом &#9734;</span><span class="sxs-lookup"><span data-stu-id="8ea4c-126">Adoption Tool- Champion Management Platform &#9734;</span></span>

<span data-ttu-id="8ea4c-127">Шаблон приложения Champion Management Platform (CMP) помогает управлять, масштабировать и вдохновлять чемпионов по командной работе на достижение большего.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-127">The Champion Management Platform (CMP) app template helps you manage, scale, and inspire your teamwork champions to achieve more.</span></span> <span data-ttu-id="8ea4c-128">Этот шаблон приложения построен на SharePoint Framework и загружается во вкладку в команде.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-128">This app template is built on the SharePoint Framework and loaded into a tab within a team.</span></span> <span data-ttu-id="8ea4c-129">Группы могут использовать этот инструмент, чтобы помочь управлять членством в программе, предоставить лидеров и типы событий для регистрации, а также инструменты для наложения цифровых значков для участников программы.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-129">Groups can leverage this tool to help manage program membership, provide a leaderboard and event types for logging, and tools to overlay digital badges to program participants.</span></span>

[<span data-ttu-id="8ea4c-130">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-130">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started-9734"></a><span data-ttu-id="8ea4c-131">Усыновление Инструмент-Microsoft 365 Пути обучения (Начало работы) &#9734;</span><span class="sxs-lookup"><span data-stu-id="8ea4c-131">Adoption Tool- Microsoft 365 Learning Pathways (Get Started) &#9734;</span></span>

<span data-ttu-id="8ea4c-132">Шаблон Начало работы приложения позволяет привнести в Microsoft 365 пути обучения Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-132">The Get Started app template allows you to bring the power of Microsoft 365 learning pathways inside of Microsoft Teams.</span></span> <span data-ttu-id="8ea4c-133">Этот шаблон приложения позволяет предоставить легкий доступ к определенным учебным страницам или другим интрасети активы и загрузить содержимое непосредственно в Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-133">This app template allows you to grant easy access to specific training pages or other intranet assets and load the content directly within Teams.</span></span> <span data-ttu-id="8ea4c-134">Вы также можете изменить название приложения или логотип в соответствует брендингу вашей компании.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-134">You can also change the app name or logo to match your company branding.</span></span>

[<span data-ttu-id="8ea4c-135">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-135">Get it on GitHub</span></span>](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="appointment-manager"></a><span data-ttu-id="8ea4c-136">Менеджер по назначениям</span><span class="sxs-lookup"><span data-stu-id="8ea4c-136">Appointment Manager</span></span> 

<span data-ttu-id="8ea4c-137">Appointment Manager – это Teams приложения, помогая компаниям создавать, управлять и проводить виртуальные встречи с потребителями через Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-137">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="8ea4c-138">Новые запросы о назначении от потребителей видны Teams каналах, где они быстро назначаются и переназначаются сотрудникам группы.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-138">New appointment requests from consumers are visible in Teams channels, where they are quickly assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="8ea4c-139">Запросы на прием рассматриваются на уровне команды или личных уровней с помощью пользовательских вкладок.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-139">Appointment requests are viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="8ea4c-140">Каждое назначение связано с Teams онлайн-встречи, поэтому персонал и потребители могут легко присоединиться к собранию в запланированное время.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-140">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="8ea4c-141">Шаблон приложения интегрируется с Microsoft Bookings для легкого управления назначением.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-141">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="8ea4c-142">Запланированные встречи автоматически отображаются в календарях назначенных сотрудников, а потребители получают настраиваемые уведомления по электронной почте и напоминания со встроенными ссылками на собрания.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-142">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="8ea4c-143">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-143">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="8ea4c-144">![Менеджер по назначению ](../assets/images/appointment-manager-overview.png)
 ![ Обзор назначения менеджера в Teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-144">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="8ea4c-145">Спросите в сторону</span><span class="sxs-lookup"><span data-stu-id="8ea4c-145">Ask Away</span></span>

<span data-ttu-id="8ea4c-146">Ask Away - это [Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям проводить сеансы вопросов и ответов под названием&A в течение Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-146">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Question and Answer, called Q&A sessions within Teams.</span></span> <span data-ttu-id="8ea4c-147">Используя бот Ask Away, члены команды могут отправлять и до голосования вопросы, разделяемые коллегами, что позволяет&Хосты легко собирать топ-в-ум вопросы в канале или чате.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-147">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="8ea4c-148">Бот используется для проведения сеанса в режиме реального времени&A на Teams и позволяет участникам задавать вопросы в прямом эфире через чат.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-148">The bot is used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live through chat.</span></span>

[<span data-ttu-id="8ea4c-149">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-149">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Просмотр всплывающего диалога лидеров для голосования пользователей по вопросам](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="8ea4c-151">Вспомогательная аналитика</span><span class="sxs-lookup"><span data-stu-id="8ea4c-151">Associate Insights</span></span>

<span data-ttu-id="8ea4c-152">Associate Insights – это [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) шаблон, который позволяет работникам первой линии непосредственно захватывать и представлять мнение клиентов, настроения и восприятие.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-152">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="8ea4c-153">Работники первой линии часто являются первым представителем компании, который взаимодействует с клиентами в контакте один на один.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-153">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="8ea4c-154">Собранные данные совместно используются бизнес-группами, например, через Power BI Teams, для улучшения продукта и повышения качества обслуживания клиентов.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-154">The collected data are shared and used collaboratively by business teams, such as through a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="8ea4c-155">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-155">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![Представление отзывов о приложениях, генерируемых информацией](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Power BI представления о приложениях, генерируемых идеями](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="8ea4c-158">Присутствие</span><span class="sxs-lookup"><span data-stu-id="8ea4c-158">Attendance</span></span>

<span data-ttu-id="8ea4c-159">Приложение "Посещаемость" [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) вкладкой, закрепленной в команде.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-159">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that are pinned in a team.</span></span> <span data-ttu-id="8ea4c-160">Он предназначен для записи присутствия в настройках, таких как обучение и обучение среды.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-160">It is designed to record presence in settings, such as learning and training environments.</span></span> <span data-ttu-id="8ea4c-161">Пользователи могут отмечать или редактировать посещаемость в течение 30 дней в прошлом и просматривать обобщенные отчеты о посещаемости для всей группы или отдельных участников.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-161">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span> <span data-ttu-id="8ea4c-162">Для получения дополнительной информации о посещаемости команд, [см GitHub.](https://github.com/OfficeDev/microsoft-teams-apps-attendance)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-162">For more information on teams attendance, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance).</span></span>

<span data-ttu-id="8ea4c-163">Следующее изображение отображает демо посещаемости приложения:</span><span class="sxs-lookup"><span data-stu-id="8ea4c-163">The following image displays the attendance app demo:</span></span>  

![Демонстрация приложения для посещений](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="8ea4c-165">Книга-комната</span><span class="sxs-lookup"><span data-stu-id="8ea4c-165">Book-a-room</span></span>

<span data-ttu-id="8ea4c-166">Book-a-room — это [бот Microsoft Teams который](../bots/what-are-bots.md) позволяет пользователям быстро находить и резервировать зал заседаний на 30, 60 или 90 минут, начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-166">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="8ea4c-167">Время по умолчанию составляет 30 минут.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-167">The default time is 30 minutes.</span></span> <span data-ttu-id="8ea4c-168">Бот-комната в книге прицелы для личных или 1:1 разговоров.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-168">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="8ea4c-169">Для получения дополнительной информации о Book-a-room приложение, [см GitHub.](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-169">For more information on Book-a-room app, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom).</span></span>  
<span data-ttu-id="8ea4c-170">Следующее изображение отображает демо-версию Book-a-room:</span><span class="sxs-lookup"><span data-stu-id="8ea4c-170">The following image displays the Book-a-room demo:</span></span>

![Демонстрация книги-комнаты](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="8ea4c-172">Доступ к зданию</span><span class="sxs-lookup"><span data-stu-id="8ea4c-172">Building Access</span></span>

<span data-ttu-id="8ea4c-173">Building Access — это приложение на базе Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) которое поддерживает администрирование пороговых значений заполняемости зданий и норм социального дистанцирования, позволяя директорам объектов управлять, отслеживать и сообщать о присутствии сотрудников на месте.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-173">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="8ea4c-174">Приложение, построенное с [использованием](/powerapps/powerapps-overview)Microsoft Power Apps и [Power Automate](/power-automate/getting-started), глубоко интегрируется с Microsoft Teams и позволяет организациям определять готовность к построению, устанавливать критерии отбора для доступа на месте, и собирать информацию для будущего планирования.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-174">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="8ea4c-175">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-175">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Карта бронирования доступа к зданию](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Представление ключа доступа к зданию](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="8ea4c-178">Праздники</span><span class="sxs-lookup"><span data-stu-id="8ea4c-178">Celebrations</span></span>

<span data-ttu-id="8ea4c-179">Celebrations – это Teams приложение, которое помогает членам команды отмечать дни рождения, юбилеи и другие повторяющиеся события друг друга.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-179">Celebrations is a Teams app that helps team members to celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="8ea4c-180">Он помнит особые случаи всех членов команды и посылает дружеское послание во всех командах, отобранных во время создания мероприятия, чтобы члены команды чувствовали себя особенными в свой день.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-180">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="8ea4c-181">Приложение обеспечивает простой интерфейс для всех членов команды, чтобы лично добавить и просмотреть свои события, а также позволяет пользователю выбрать команды, в которых события получает общий доступ.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-181">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="8ea4c-182">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-182">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="8ea4c-183">Контрольный список</span><span class="sxs-lookup"><span data-stu-id="8ea4c-183">Checklist</span></span>

<span data-ttu-id="8ea4c-184">Контрольный список является пользовательским Microsoft Teams [приложения для расширения обмена](../messaging-extensions/what-are-messaging-extensions.md) сообщениями, которое позволяет вам сотрудничать с вашей командой, создавая общий контрольный список в чате или канале.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-184">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="8ea4c-185">Приложение поддерживается во всех Teams платформы, таких как настольный браузер, iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-185">The app is supported across all Teams platform clients, such as desktop browser, iOS, and Android.</span></span> <span data-ttu-id="8ea4c-186">Приложение готово к развертыванию в рамках вашей Microsoft 365 подписки.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-186">The app is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="8ea4c-187">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-187">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app)

:::row:::
:::column span="2":::
    ![Создание контрольного списка Teams представлении](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in"></a><span data-ttu-id="8ea4c-189">Класс Drop-in</span><span class="sxs-lookup"><span data-stu-id="8ea4c-189">Classroom Drop-in</span></span> 

<span data-ttu-id="8ea4c-190">Класс Drop-in — это приложение на базе Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)которое позволяет руководителям систем найти классные группы, означает виртуальные классы и при необходимости добавить себя или других в эти классные группы в течение определенного периода.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-190">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams, means virtual classrooms and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="8ea4c-191">Приложение, построенное с [использованием](/powerapps/powerapps-overview) Microsoft Power Apps [и Power Automate](/power-automate/getting-started), глубоко интегрируется с Microsoft Teams для обеспечения того, чтобы учебные заведения могли оптимизировать свою деятельность в гибридной среде обучения, предоставляя доступ к соответствующим заинтересованным сторонам для классовых групп в соответствии с бизнес-требованиями.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-191">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="8ea4c-192">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-192">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Класс дроп-в запросе](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="8ea4c-194">Корпоративный Communicator</span><span class="sxs-lookup"><span data-stu-id="8ea4c-194">Company Communicator</span></span>

<span data-ttu-id="8ea4c-195">Приложение «Communicator» позволяет корпоративным командам создавать и отправлять сообщения, предназначенные для нескольких групп или большого количества сотрудников в чате, что позволяет организации охватить сотрудников там, где они сотрудничают.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-195">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="8ea4c-196">Используйте этот шаблон для нескольких сценариев, таких как новые инициативные объявления, бортовое обучение сотрудников, современное обучение, а также программы разработки или всей организации.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-196">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning, and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="8ea4c-197">Приложение обеспечивает простой интерфейс для назначенных пользователей для создания, предварительного просмотра, совместной работы и отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-197">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="8ea4c-198">Он обеспечивает основу для создания пользовательских целевых коммуникационных возможностей, таких как пользовательские телеметрии о том, сколько пользователей признали или взаимодействовали с сообщением.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-198">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="8ea4c-199">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-199">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator составляют окно зрения](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="8ea4c-201">Контактная группа Lookup</span><span class="sxs-lookup"><span data-stu-id="8ea4c-201">Contact Group Lookup</span></span>

<span data-ttu-id="8ea4c-202">Приложение Contact Group Lookup предоставляет удобный и полезный подход к созданию, доступу и управлению контактными группами вашей организации, ранее известными как списки рассылки или группы связи.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-202">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups, formerly known as distribution lists or communication groups.</span></span> <span data-ttu-id="8ea4c-203">Пользователи могут быстро просматривать и общаться с членами группы, просматривать статус участника и создавать групповой чат с выбранными членами контактной группы, все в Teams среды.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-203">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="8ea4c-204">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-204">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![Контактная группа Lookup возлагали избранное представление](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Контактная группа Lookup начать чат демо](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="co-worker-appreciation"></a><span data-ttu-id="8ea4c-207">Благодарность коллег</span><span class="sxs-lookup"><span data-stu-id="8ea4c-207">Co-worker Appreciation</span></span> 

<span data-ttu-id="8ea4c-208">Используя шаблон оценки сотрудников в Microsoft Teams, пользователи могут распознавать достижения своих коллег в Teams в контексте.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-208">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="8ea4c-209">Когда сотрудники выбирают вознаграждение коллеге, получатели и другие члены команды помечаются в разговоре на канале и получают уведомление о деталях награды канала.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-209">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="8ea4c-210">Награды записаны в приложении Teams, которое является безопасным, портативным и легко можно делиться.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-210">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="8ea4c-211">Это считается версией приложения Open Badges на основе PowerApps с таблицей лидеров.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-211">This is considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="8ea4c-212">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-212">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![полный](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="8ea4c-214">КраудИсточникр</span><span class="sxs-lookup"><span data-stu-id="8ea4c-214">CrowdSourcer</span></span>

<span data-ttu-id="8ea4c-215">CrowdSourcer является [Microsoft Teams, который](../bots/what-are-bots.md) предоставляет командам запрошенную информацию, полученную совместно от членов группы.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-215">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="8ea4c-216">Это помогает отвечать на часто задаваемые вопросы, позволяя участникам активно участвовать и вносить свой вклад в интересный и полезный информационный ресурс.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-216">It helps to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="8ea4c-217">Получить его на Github</span><span class="sxs-lookup"><span data-stu-id="8ea4c-217">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Взаимодействие с конечных пользователей краудсорсингом](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="8ea4c-219">Пользовательские наклейки</span><span class="sxs-lookup"><span data-stu-id="8ea4c-219">Custom Stickers</span></span>

<span data-ttu-id="8ea4c-220">Самовыражение является основой здоровой командной культуры.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-220">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="8ea4c-221">Этот шаблон приложения является [расширением обмена сообщениями,](~/messaging-extensions/what-are-messaging-extensions.md) которое позволяет пользователям использовать пользовательские наклейки и GIF-файлы в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-221">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="8ea4c-222">Этот шаблон обеспечивает простой веб-конфигурации опыт, где любой человек с конфигурацией доступ может загрузить GIF-файлы, наклейки и изображения, которые они хотят, чтобы их пользователи, что позволяет всей вашей команде использовать любой набор наклейки вы выбираете.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-222">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs, stickers, and images they want their users to have, allowing your entire team to use any set of stickers you choose.</span></span>

<span data-ttu-id="8ea4c-223">Это приложение также позволяет легко делиться изображениями, GIF-изображениями, наклейками между командами без доступа к SharePoint сайтам или отдельным каналам в качестве механизмов хранения и обмена.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-223">This app also enables easy sharing of images, GIFs, stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="8ea4c-224">Например, группы продуктов могут легко обмениваться изображениями продуктов и GIF-изображениями в социальных сетях, маркетинговых и торговых отделах.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-224">For example, product teams can easily share product images and GIFs to social media, marketing, and sales teams programmatically.</span></span> <span data-ttu-id="8ea4c-225">Можно также расширить это приложение, запуская поток уведомлений для конкретных групп или отдельных лиц, когда новые изображения, и GIF-файлы доступны.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-225">One can also extend this app by triggering a notification flow to specific teams or individuals when new images, and GIFs are made available.</span></span>

[<span data-ttu-id="8ea4c-226">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-226">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Приложение наклейки](../assets/images/stickers.png)

## <a name="employee-ideas"></a><span data-ttu-id="8ea4c-228">Идеи сотрудников</span><span class="sxs-lookup"><span data-stu-id="8ea4c-228">Employee Ideas</span></span>

<span data-ttu-id="8ea4c-229">Приложение «Идеи сотрудников» — это версия приложения Для PowerApps на основе шаблона приложения Great Ideas.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-229">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="8ea4c-230">Приложение позволяет Teams пользователям настроить и настроить кампанию идей.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-230">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="8ea4c-231">Идея кампании является категорией для группировки идей вокруг общих тем.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-231">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="8ea4c-232">Teams пользователи могут выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8ea4c-232">Teams users can also perform the following activities:</span></span>

* <span data-ttu-id="8ea4c-233">Настройте стандартную форму представления, которую сотрудники должны представить для каждой идеи.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-233">Configure a standard submission form that employees must submit for each idea.</span></span> 
* <span data-ttu-id="8ea4c-234">Просмотрите и управляйте идеями и списком кампаний.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-234">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="8ea4c-235">Изменение и удаление кампаний.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-235">Modify and delete campaigns.</span></span>
* <span data-ttu-id="8ea4c-236">Обзор лидеров советов идей.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-236">Review leader boards of ideas.</span></span>
* <span data-ttu-id="8ea4c-237">Голосуйте за приоритетные идеи и делитесь ими.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-237">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="8ea4c-238">Отправить идеи для кампании.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-238">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="8ea4c-239">Посмотреть идею другого члена команды.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-239">View other team member's idea.</span></span>
* <span data-ttu-id="8ea4c-240">Голосуйте за самые популярные идеи.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-240">Vote on most liked ideas.</span></span>
* <span data-ttu-id="8ea4c-241">Просмотрите эффективность своих идей по сравнению с другими в рамках кампании.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-241">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="8ea4c-242">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-242">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Управление представлением кампании](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="8ea4c-244">Электронные рецепты</span><span class="sxs-lookup"><span data-stu-id="8ea4c-244">E-Prescriptions</span></span> 

<span data-ttu-id="8ea4c-245">E-Prescriptions — [это Power Apps на](/powerapps/maker/canvas-apps/embed-teams-app) основе электронных технологий, которое улучшает телемедицину и виртуальную помощь, автоматизируя процесс выдачи электронных рецептов пациентам.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-245">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="8ea4c-246">Медицинские работники могут быстро рассматривать назначения, генерировать электронные рецепты, и отправлять электронные письма с электронным рецептом вложений для пациентов непосредственно в Teams платформы.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-246">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="8ea4c-247">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-247">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![Скриншот приложения E-Prescriptions.](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Скриншот приложения E-Prescriptions.](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training"></a><span data-ttu-id="8ea4c-252">Обучение сотрудников</span><span class="sxs-lookup"><span data-stu-id="8ea4c-252">Employee Training</span></span> 

<span data-ttu-id="8ea4c-253">Обучение сотрудников – это Microsoft Teams, которое позволяет организаторам легко публиковать, отслеживать и продвигать учебные и учебные мероприятия для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-253">Employee training is a Microsoft Teams app that enables organizers to easily publish, track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="8ea4c-254">С помощью приложения организаторы мероприятий могут отправлять напоминания и уведомления регистраторам событий, а сотрудники могут указывать интерес к предстоящим событиям, обновляться о текущих событиях и делиться подробностями событий с коллегами через расширение обмена сообщениями Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-254">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues through the Teams messaging extension.</span></span>

[<span data-ttu-id="8ea4c-255">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-255">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="8ea4c-256">**Просмотр учебных мероприятий для сотрудников** ![ Изображение вкладки обучения сотрудников](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-256">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="8ea4c-257">**Создание учебного мероприятия для сотрудников** ![ Обучение сотрудников создает форму событий](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-257">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="8ea4c-258">Эксперт-finder</span><span class="sxs-lookup"><span data-stu-id="8ea4c-258">Expert Finder</span></span>

<span data-ttu-id="8ea4c-259">Expert Finder – это [Microsoft Teams, который](../bots/what-are-bots.md) определяет конкретных членов организации на основе их навыков, интересов и качеств образования.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-259">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="8ea4c-260">Участники находят экспертов в организации, которые соответствуют поиску ключевых слов Azure Active Directory профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-260">Members find experts within an organization that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="8ea4c-261">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-261">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Эксперт Поиск результаты поиска демо](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="8ea4c-263">Вопросы и ответы плюс</span><span class="sxs-lookup"><span data-stu-id="8ea4c-263">FAQ Plus</span></span>

<span data-ttu-id="8ea4c-264">Разговорные&боты являются простым способом дать ответы на часто задаваемые вопросы пользователей.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-264">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="8ea4c-265">Но, большинство ботов не в состоянии взаимодействовать с пользователями в значимым образом, потому что нет человека в цикле, когда бот не удается.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-265">But, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="8ea4c-266">Бот часто задаваемых вопросов является дружественным&бот, который приносит человека в петлю, когда он не в состоянии помочь.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-266">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="8ea4c-267">Можно задать боту вопрос, и бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-267">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="8ea4c-268">В случае нет, бот позволяет пользователю отправить запрос, который затем получает размещены на предварительно настроенной группы экспертов, которые помогают оказывать поддержку, действуя на уведомления из самой команды.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-268">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="8ea4c-269">Последний выпуск часто **задаваемых вопросов Плюс поддерживает** улучшенные&резолюции, позволяя команде экспертов для завершения следующих:</span><span class="sxs-lookup"><span data-stu-id="8ea4c-269">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="8ea4c-270">&#x2714; Добавляем новые&Как непосредственно к базе знаний, используя расширения сообщений.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-270">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="8ea4c-271">&#x2714; редактировать и удалять&пара, добавленную ботом.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-271">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="8ea4c-272">&#x2714; Отслеживайте историю пересмотра q&As.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-272">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="8ea4c-273">&#x2714; настраивайте ответ с дополнительными деталями для отображения в качестве [адаптивной карты.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-273">&#x2714; Configure an answer with additional details to display as an [Adaptive Card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="8ea4c-274">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Часто задаваемые вопросы Плюс GIF](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app"></a><span data-ttu-id="8ea4c-276">Получить приложение поддержки</span><span class="sxs-lookup"><span data-stu-id="8ea4c-276">Get Support App</span></span>

<span data-ttu-id="8ea4c-277">Приложение Get Support используется организациями, использующими Microsoft Teams, чтобы любой набор пользователей мог запрашивать помощь у руководителей.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-277">The Get Support app is used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="8ea4c-278">Это приложение включает в себя следующие функции:</span><span class="sxs-lookup"><span data-stu-id="8ea4c-278">This app includes the following features:</span></span>
* <span data-ttu-id="8ea4c-279">Запрос помощи по различным категориям из приложения Power.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-279">Requesting assistance on different categories from a Power App.</span></span>
* <span data-ttu-id="8ea4c-280">Запросы направляются запрашивающим, информирующим их о том, кому назначен заяц.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-280">Notifications sent to requestors informing them of who hare assigned.</span></span>
* <span data-ttu-id="8ea4c-281">Уведомления, отправленные назначенным руководителям, информирующие их о том, кто нуждается в помощи.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-281">Notifications sent to assigned supervisors informing them of who needs assistance.</span></span> 
* <span data-ttu-id="8ea4c-282">Анализ эскалации и закономерностей в SharePoint и PowerBI.S.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-282">Analyzing escalations and patterns in SharePoint and PowerBI.S.</span></span>

[<span data-ttu-id="8ea4c-283">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-283">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Получить поддержку Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="8ea4c-285">Отслеживание целей</span><span class="sxs-lookup"><span data-stu-id="8ea4c-285">Goal Tracker</span></span>

<span data-ttu-id="8ea4c-286">Приложение Goal Tracker является комплексным решением для вашей организации для поддержки установления целей, наблюдения за прогрессом и признания успеха в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-286">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="8ea4c-287">Приложение позволяет пользователям устанавливать, отслеживать и обновлять цели на профессиональном, личном и командном уровне.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-287">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="8ea4c-288">Члены группы также получают своевременные напоминания и обновления статуса, чтобы оставаться сосредоточенными и оставаться на пути.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-288">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="8ea4c-289">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-289">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![Установить цели](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр поставленных целей](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a><span data-ttu-id="8ea4c-292">Великие идеи</span><span class="sxs-lookup"><span data-stu-id="8ea4c-292">Great Ideas</span></span>

<span data-ttu-id="8ea4c-293">Приложение Great Ideas поддерживает и расширяет возможности инноваций и творчества в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-293">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="8ea4c-294">Приложение позволяет вашим сотрудникам обмениваться идеями с коллегами и руководством, открывать новые материалы, прожектор вклад для рассмотрения коллегами, и отдать свой голос за лучшие предложения в течение Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-294">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="8ea4c-295">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-295">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

:::row:::
  :::column span="2":::
    ![Просмотр представленных идей](../assets/images/great-ideas-all-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр идей](../assets/images/great-ideas-digest-view.png)
:::column-end:::
:::row-end:::

## <a name="group-activities"></a><span data-ttu-id="8ea4c-298">Групповые мероприятия</span><span class="sxs-lookup"><span data-stu-id="8ea4c-298">Group Activities</span></span>

<span data-ttu-id="8ea4c-299">Group Activities – это Microsoft Teams приложение, которое упрощает быстрое создание групп активности и управление рабочими процессами совместной работы в контексте Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-299">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="8ea4c-300">Авторы действий имеют возможность создавать действия, случайным образом распределять членов команды в группах и, по желанию, отправлять напоминания бота до завершения действий.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-300">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="8ea4c-301">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-301">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Перечень групповых мероприятий в Teams](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Сообщение уведомления о групповой активности в канале](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="group-connect-9734"></a><span data-ttu-id="8ea4c-304">Групповой Подключение &#9734;</span><span class="sxs-lookup"><span data-stu-id="8ea4c-304">Group Connect &#9734;</span></span>

<span data-ttu-id="8ea4c-305">Group Подключение это приложение Microsoft Teams которое помогает членам организации обнаружить группы сотрудников и найти информацию, относящуюся к группам сотрудников.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-305">Group Connect is a Microsoft Teams app that helps organization members discover employee groups and find information relevant to employee groups.</span></span> <span data-ttu-id="8ea4c-306">Приложение поставляется встроенный с богатыми возможностями для руководителей организации общаться со своими сотрудниками в отношении групп, событий и ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-306">The app comes built-in with rich capabilities for organization leaders to communicate with their employees regarding groups, events, and resources.</span></span> <span data-ttu-id="8ea4c-307">Приложение Group Подключение также соответствует членам группы друг с другом на желаемой частоте, чтобы поощрять общение и сплоченность внутри группы.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-307">The Group Connect app also matches group members with each other at their desired frequency to encourage networking and cohesion within a group.</span></span> <span data-ttu-id="8ea4c-308">Для получения дополнительной информации о том, как можно использовать приложение Group Подключение, чтобы помочь группам сотрудников укрепиться в вашей организации, смотрите приложение на GitHub.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-308">For more information on how you can leverage the Group Connect app to help employee groups foster within your organization, see the app on GitHub.</span></span>

[<span data-ttu-id="8ea4c-309">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-309">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupconnect)

![Откройте для себя группы D&I](https://github.com/OfficeDev/microsoft-teams-apps-diversityandinclusion/wiki/Images/temp_group_connect_landing.png)

## <a name="grow-your-skills"></a><span data-ttu-id="8ea4c-311">Расти ваши навыки</span><span class="sxs-lookup"><span data-stu-id="8ea4c-311">Grow Your Skills</span></span>

<span data-ttu-id="8ea4c-312">Приложение Grow Your Skills поддерживает профессиональный рост и развитие, позволяя сотрудникам вносить свой вклад в дополнительные проекты для вашей организации, одновременно изучая новые навыки.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-312">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="8ea4c-313">Сотрудники могут использовать приложение, чтобы найти возможности, которые отвечают их интересам, наслаждаться значимым сотрудничеством с коллегами, и приобрести новые уровни знаний и возможностей, все в Teams среде.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-313">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="8ea4c-314">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-314">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![Доступное представление проектов](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр приобретенных навыков зрителя](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a><span data-ttu-id="8ea4c-317">Поддержка управления персоналом</span><span class="sxs-lookup"><span data-stu-id="8ea4c-317">HR Support</span></span>

<span data-ttu-id="8ea4c-318">Бот поддержки hr является дружественным&бот, который приносит поддержку профессионала или эксперта из HR команды в цикле, когда он не в состоянии помочь.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-318">HR Support bot is a friendly Q&A bot that brings a support professional or expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="8ea4c-319">Можно задать боту вопрос, и бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-319">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="8ea4c-320">В случае нет, бот позволяет пользователю отправлять запрос, который затем получает размещены в предварительно настроенной группы экспертов, которые помогают оказывать поддержку, действуя на уведомления из своей команды себя.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-320">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="8ea4c-321">Кроме того, бот предлагает ссылки на рекомендуемые политики в области управления персоналом или вопросы, ища предварительно настроенные теги в этом вопросе.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-321">Additionally, the bot suggests links to recommended HR policies or questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="8ea4c-322">Эти плитки находятся в связанной вкладке в качестве быстрой ссылки.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-322">These tiles are found in the associated tab as a quick reference.</span></span> <span data-ttu-id="8ea4c-323">Поддержка персонала хорошо работает для легкого веса&А и для обеспечения быстрой поддержки при запуске новых проектов или инициатив в организации.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-323">HR Support works well for light weight Q&A and to provide quick support when launching new projects or initiatives in the organization.</span></span>

[<span data-ttu-id="8ea4c-324">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-324">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Поддержка управления персоналом](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="8ea4c-326">Точки соприкосновения</span><span class="sxs-lookup"><span data-stu-id="8ea4c-326">Icebreaker</span></span>

<span data-ttu-id="8ea4c-327">Icebreaker является одним [Microsoft Teams, который помогает](../bots/what-are-bots.md) вашей команде стать ближе путем сопряжения двух случайных членов команды каждую неделю, чтобы встретиться.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-327">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="8ea4c-328">Бот упрощает планирование, автоматически предлагая свободное время, которое работает для обоих членов.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-328">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="8ea4c-329">Укрепляйте личные связи и создавайте тесное сообщество с помощью этого приложения.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-329">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="8ea4c-330">В дополнение к поощрению личных связей во всей вашей команде, приложение Icebreaker может помочь развивать сообщества, основанные на интересах в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-330">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="8ea4c-331">Например, вы можете использовать это приложение для группы DevOps, чтобы помочь идеям и передовой практике органично распространиться по всей организации.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-331">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="8ea4c-332">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-332">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Ледокол приложение](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="8ea4c-334">Стимулы</span><span class="sxs-lookup"><span data-stu-id="8ea4c-334">Incentives</span></span>

<span data-ttu-id="8ea4c-335">Стимулы — это [Power Apps который](/powerapps/maker/canvas-apps/embed-teams-app) управляет и отслеживает стимулируемое участие сотрудников в определенных мероприятиях, таких как тренинги и инициативы по управлению изменениями.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-335">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities, such as trainings and change management initiatives.</span></span> <span data-ttu-id="8ea4c-336">Администраторы используют приложение для создания назначенных действий, присвоения баллов для завершения и указать требуемые уровни баллов за вознаграждение.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-336">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="8ea4c-337">Сотрудники используют приложение для просмотра накопленных баллов и, по достижении права, запрашивают и требуют вознаграждение.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-337">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="8ea4c-338">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-338">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Стимулы демо-версии приложения](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="8ea4c-340">Репортер инцидента</span><span class="sxs-lookup"><span data-stu-id="8ea4c-340">Incident Reporter</span></span>

<span data-ttu-id="8ea4c-341">Incident Reporter - это [Microsoft Teams бот,](../bots/what-are-bots.md) оптимизирует управление инцидентами в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-341">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="8ea4c-342">Бот облегчает автоматизированный сбор данных об инцидентах, индивидуальные отчеты об инцидентах, соответствующие уведомления заинтересованных сторон и отслеживание инцидентов в конце.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-342">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="8ea4c-343">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-343">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![Представление сферы охвата группы репортеров инцидента](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Инцидент репортер личный вид сферы](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="inspection"></a><span data-ttu-id="8ea4c-346">осмотр</span><span class="sxs-lookup"><span data-stu-id="8ea4c-346">Inspection</span></span> 

 <span data-ttu-id="8ea4c-347">Инспекция является одним Microsoft Teams, которое позволяет фронтовики работников для проверки ничего из мест для активов и оборудования.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-347">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="8ea4c-348">Например, розничный магазин, завод по производству или транспортные средства и машины.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-348">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="8ea4c-349">В этом решении есть два приложения, каждое из которых предназначено для разных типов пользователей.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-349">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="8ea4c-350">Приложение дает возможность работникам линии фронта проверять актив или область, управлять качеством продуктов и услуг или поддерживать безопасность на рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-350">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="8ea4c-351">Это облегчает общение между членами группы для решения вопросов, обнаруженных в ходе инспекции.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-351">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="8ea4c-352">Приложение предоставляет простые отчеты для менеджеров, чтобы ускорить решение проблемы и выделить тенденции.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-352">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="8ea4c-353">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Обзор инспекции](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a><span data-ttu-id="8ea4c-355">Отчет о выпуске</span><span class="sxs-lookup"><span data-stu-id="8ea4c-355">Issue Reporting</span></span>

<span data-ttu-id="8ea4c-356">Приложение Issue Reporting предоставляет сотрудникам и менеджерам возможность поднимать и управлять проблемами.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-356">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="8ea4c-357">Он состоит из двух приложений, приложение для отчетов о проблемах и приложение «Управление проблемами» для управления проблемами.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-357">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="8ea4c-358">Руководители групп используют приложение «Управление проблемами» для настройки приложения, включая канал, в котором Microsoft Teams, и задачи планировщика создаются приложением.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-358">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="8ea4c-359">Менеджеры также используют приложение для создания форм шаблонов для сбора информации, когда пользователь сообщает о проблеме.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-359">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="8ea4c-360">Например, просмотреть, отредактировать или удалить формы шаблонов проблем.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-360">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="8ea4c-361">Приложение также используется для рассмотрения проблем команды, отчета об истории проблем и эффективного управления разрешением проблем.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-361">The app is also used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="8ea4c-362">Сотрудники используют приложение для регистрации проблем и деталей, необходимых для их устранения.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-362">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="8ea4c-363">Приложение также используется для изменения и решения существующих проблем и получить представление высокого уровня отдельных или командных проблем.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-363">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="8ea4c-364">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Представление группы отчетов о выпуске](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="8ea4c-366">Новый сотрудник на борту</span><span class="sxs-lookup"><span data-stu-id="8ea4c-366">New Employee Onboarding</span></span> 

<span data-ttu-id="8ea4c-367">New Employee Onboarding — это интегрированное Microsoft Teams [и SharePoint New Employee Onboarding Solution,](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) которое позволяет вашей организации предоставлять сотрудникам, нанимаемые на новую работу, последовательный и качественный опыт в области бортового обслуживания.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-367">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="8ea4c-368">Приложение используется группами по персоналу и менеджерами по найму для предоставления соответствующей информации на протяжении всего процесса ориентации и индукции, а также новых сотрудников для обмена отзывами, предоставления интродукций и выполнения задач по посадке.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-368">The app is used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="8ea4c-369">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-369">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="8ea4c-370">**Новая приветственная карточка сотрудника** ![ Изображение новой приветственной карточки сотрудника](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-370">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="8ea4c-371">**Новый контрольный список сотрудников** ![ Изображение нового контрольного списка сотрудников](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-371">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="8ea4c-372">Открытые значки</span><span class="sxs-lookup"><span data-stu-id="8ea4c-372">Open Badges</span></span>

<span data-ttu-id="8ea4c-373">Open Badges - это Microsoft Teams, которое позволяет людям получать значки учетных данных цифрового обучения в Teams и делиться ими повсюду.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-373">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="8ea4c-374">Используя возможности от сторонних цифровых значков выдачи власти, [Badgr](https://badgr.org/), награжден значки регистрируются в профиле Получателя Badgr и доступны для создания и обмена богатую картину жизни обучения путешествий.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-374">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="8ea4c-375">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![Изображение доступных значков](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Представление награжденных значков](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="poll"></a><span data-ttu-id="8ea4c-378">опрос</span><span class="sxs-lookup"><span data-stu-id="8ea4c-378">Poll</span></span> 

<span data-ttu-id="8ea4c-379">Опрос является пользовательским приложением Microsoft Teams [обмена сообщениями,](../messaging-extensions/what-are-messaging-extensions.md) которое позволяет быстро создавать и отправлять опросы в чате или канале для сбора мнений и предпочтений команды.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-379">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="8ea4c-380">Приложение поддерживается во всех Teams платформы, таких как настольный компьютер, браузер, iOS и Android, и готово к развертыванию в рамках вашей Microsoft 365 подписки.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-380">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="8ea4c-381">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-381">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Создание опроса в Teams представлении](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="8ea4c-383">Быстрые ответы</span><span class="sxs-lookup"><span data-stu-id="8ea4c-383">Quick Responses</span></span>

<span data-ttu-id="8ea4c-384">Быстрый ответ является Microsoft Teams приложение, которое обеспечивает надежное решение для эффективного ответа пользователей часто задаваемые вопросы часто задаваемые вопросы.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-384">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions FAQs.</span></span> <span data-ttu-id="8ea4c-385">Вместо того, чтобы отвечать на каждый запрос вручную и непрерывно повторяя информацию, приложение создает библиотеку ответов для интерактивного пользовательского интерфейса через Teams [расширения сообщений.](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-385">Instead of answering each query manually and continuously repeating information, the app builds a library of responses for an interactive user experience through Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="8ea4c-386">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-386">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Пример представления ответов](../assets/images/quick-responses.png)

## <a name="quiz--9734"></a><span data-ttu-id="8ea4c-388">Викторина &#9734;</span><span class="sxs-lookup"><span data-stu-id="8ea4c-388">Quiz  &#9734;</span></span>

<span data-ttu-id="8ea4c-389">Викторина является [пользовательским Teams для обмена сообщениями](../messaging-extensions/what-are-messaging-extensions.md) приложение, которое позволяет создавать викторины в чате или канал для проверки знаний и мгновенных результатов.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-389">Quiz is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a quiz within a chat or a channel for knowledge check and instantaneous results.</span></span> <span data-ttu-id="8ea4c-390">Вы можете использовать викторину для экзаменов в классе и в автономном режиме, проверку знаний в команде, а также для забавных викторин в команде.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-390">You can use Quiz for, In-class and offline exams, Knowledge check within team, and for fun quizzes within a team.</span></span> <span data-ttu-id="8ea4c-391">Приложение викторины поддерживается на нескольких платформах, таких как Teams, браузер, iOS и Android-клиенты.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-391">Quiz app is supported across multiple platforms, such as Teams desktop, browser, iOS, and Android clients.</span></span> <span data-ttu-id="8ea4c-392">Это приложение готово к развертыванию в рамках существующей Microsoft 365 подписки.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-392">This app is ready for deployment as part of your existing Microsoft 365 subscription.</span></span>

[<span data-ttu-id="8ea4c-393">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-393">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quiz)

:::row:::
  :::column span="1":::
    ![Создание викторины в Teams представлении](../assets/images/quiz-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="rapid-assist"></a><span data-ttu-id="8ea4c-395">Быстрая помощь</span><span class="sxs-lookup"><span data-stu-id="8ea4c-395">Rapid Assist</span></span>

<span data-ttu-id="8ea4c-396">Rapid Assist - это приложение на базе Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) которое позволяет партнерам, стоящим перед клиентами, быстро связываться с экспертами, чтобы получить быстрые ответы, искать информацию, следить за открытыми запросами и позволять экспертам получать уведомления, чтобы быстро получить вызов, чтобы помочь ответить на вопросы.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-396">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="8ea4c-397">Приложение, построенное с [использованием](/powerapps/powerapps-overview) Microsoft Power Apps [и Power Automate](/power-automate/getting-started), глубоко интегрируется с Microsoft Teams, чтобы организации могли легко подключить фронтовых работников с корпоративными связями для решения запросов клиентов и обеспечить большой опыт клиентов.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-397">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="8ea4c-398">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-398">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Интерфейс запроса конечных пользователей](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Представление запросов экспертов](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="8ea4c-401">отражать</span><span class="sxs-lookup"><span data-stu-id="8ea4c-401">Reflect</span></span> 

<span data-ttu-id="8ea4c-402">Reflect — это пользовательское приложение Microsoft Teams [для расширения обмена сообщениями,](../messaging-extensions/what-are-messaging-extensions.md) которое предоставляет безопасный и инклюзивный ресурс для членов вашей команды, чтобы поделиться состоянием своего эмоционального благополучия с коллегами или лидерами групп непосредственно в Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-402">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues or group leaders directly within Teams.</span></span> <span data-ttu-id="8ea4c-403">Приложение доступно в чате канала, группы, собрания и 1:1, и ответ на регистрацию устанавливается для публичных, частных отправителей или полностью анонимных.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-403">The app is available in channel, group, meeting, and 1:1 chats and the check-in response is set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="8ea4c-404">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-404">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="8ea4c-405">**Опрос о благополучии**</span><span class="sxs-lookup"><span data-stu-id="8ea4c-405">**Well-being poll**</span></span>
    
    ![Отражение опроса пользователей приложений](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="8ea4c-407">Удаленная поддержка</span><span class="sxs-lookup"><span data-stu-id="8ea4c-407">Remote Support</span></span>

<span data-ttu-id="8ea4c-408">Удаленная поддержка является [Microsoft Teams, который](../bots/what-are-bots.md) обеспечивает целенаправленный интерфейс между запросами поддержки по всей организации и внутренней группой поддержки.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-408">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="8ea4c-409">Конечные пользователи могут отправлять, редактировать или отзывать запросы на поддержку, а группа поддержки может отвечать, управлять и обновлять запросы на Teams платформы.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-409">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="8ea4c-410">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-410">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![Форма поддержки запроса](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Подробная информация о поддержке запроса](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a><span data-ttu-id="8ea4c-413">Запрос-а-команда</span><span class="sxs-lookup"><span data-stu-id="8ea4c-413">Request-a-team</span></span>

<span data-ttu-id="8ea4c-414">Request-a-team — это Microsoft Teams, которое оптимизирует создание новой команды для вашей корпоративной организации.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-414">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="8ea4c-415">Приложение поддерживает стандартизацию и передовой опыт при создании новых экземпляров команды путем интеграции формы запроса, управляемой мастером, встроенного процесса утверждения, панели мониторинга статуса запроса и автоматизированных построениях команды.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-415">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="8ea4c-416">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-416">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![Представление стартовых страниц запроса-команды](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Представление страницы мастера запроса-команды](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a><span data-ttu-id="8ea4c-419">Скрамы для каналов</span><span class="sxs-lookup"><span data-stu-id="8ea4c-419">Scrums for Channels</span></span>

<span data-ttu-id="8ea4c-420">Scrums for Channels - это приложение для помощников схватки, которое позволяет пользователям планировать и запускать схватки в каналах в течение Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-420">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="8ea4c-421">Приложение отлично подходит для удаленных групп и групп, состоящих из членов из различных географических мест и часовых поясов, чтобы делиться ежедневными обновлениями и обеспечить участие в схватке стоячих встреч.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-421">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="8ea4c-422">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-422">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="8ea4c-423">Для проведения встреч схватки в групповом чате [см.](#scrums-for-group-chat)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-423">To conduct scrum meetings in a group chat, see [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

:::row:::
  :::column span="2":::
    ![Scrums для просмотра настроек каналов](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Scrums для представления статуса члена группы каналов](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a><span data-ttu-id="8ea4c-426">Скрамы для группового чата</span><span class="sxs-lookup"><span data-stu-id="8ea4c-426">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="8ea4c-427">Шаблон приложения Scrums Status обновляется и теперь является Scrums для группового чата.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-427">The Scrums Status app template is updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="8ea4c-428">Scrums for Group Chat — это поддерживающий помощник по схватке, который позволяет участникам группового чата запускать асинхронные стоячие встречи и легко делиться своими ежедневными обновлениями.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-428">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="8ea4c-429">Это позволяет всем членам группового чата вносить свой вклад в схватку и просматривать обновления, сделанные другими в бегущей схватке.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-429">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="8ea4c-430">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-430">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Scrums для демонстрации группового чата](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="8ea4c-432">Поделиться сейчас</span><span class="sxs-lookup"><span data-stu-id="8ea4c-432">Share Now</span></span> 

<span data-ttu-id="8ea4c-433">Приложение Share Now способствует позитивному обмену информацией между коллегами, позволяя пользователям легко обмениваться контентом в Teams среде.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-433">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="8ea4c-434">Пользователи привлекают приложение для обмена предметами, представляющими интерес, с членами команды, обнаружения нового общего контента, настройки предпочтений и избранных закладок для более поздних чтений.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-434">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="8ea4c-435">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-435">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Выбор представления содержимого](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="8ea4c-437">Поиск в списке SharePoint</span><span class="sxs-lookup"><span data-stu-id="8ea4c-437">SharePoint List Search</span></span>

<span data-ttu-id="8ea4c-438">Сотрудничество в Microsoft Teams довольно часто ссылается на информацию, содержащуюся в пунктах SharePoint списка.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-438">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="8ea4c-439">Вставьте ссылку на данный элемент заставляет всех переключить контекст от разговора, найти необходимую информацию, а затем вернуться к Teams, чтобы продолжить разговор.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-439">Paste a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="8ea4c-440">По мере того как переговор продолжается люди должны переключить назад к пункту справки множественные времена для того чтобы проверить новые комментарии и освежить их памяти информации, котор содержат внутри деталь.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-440">As the conversation continues  people have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="8ea4c-441">Переключение этого контекста создает барьер для бесперебойного сотрудничества.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-441">This context switching creates a barrier to smooth collaboration.</span></span>
<span data-ttu-id="8ea4c-442">Для решения этой проблемы используется шаблон приложения «Поиск списка».</span><span class="sxs-lookup"><span data-stu-id="8ea4c-442">To resolve this problem, the List Search app template is used.</span></span> <span data-ttu-id="8ea4c-443">Многие пользователи используют SharePoint для питания некоторых основных рабочих процессов в своих организациях.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-443">Many users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="8ea4c-444">Тем не менее, сотрудничество вокруг списков трудно.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-444">However, collaborating around lists is difficult.</span></span> <span data-ttu-id="8ea4c-445">Используя шаблон приложения «Список» в Microsoft Teams году, пользователи могут вставлять информацию из списка SharePoint непосредственно в чате, чтобы облегчить переключение контекста, вызванное простой вставкой ссылки в чат.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-445">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="8ea4c-446">Информация вставляется в качестве легко читаемой автоматической форматной карты, помогая пользователям оставаться вовлеченными в разговор.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-446">The information is inserted as an easy-to-read auto-formatted card, helping the users stay engaged in the conversation.</span></span>

[<span data-ttu-id="8ea4c-447">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-447">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Список Поиск приложения](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="8ea4c-449">Регистрация персонала</span><span class="sxs-lookup"><span data-stu-id="8ea4c-449">Staff Check-ins</span></span>

<span data-ttu-id="8ea4c-450">Регистрация персонала — это [приложение, Power Apps на основе](/powerapps/powerapps-overview) системы, позволяющее осуществлять надзор за общением между вашим бизнесом и персоналом на местах.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-450">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview) based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="8ea4c-451">Сотрудники могут легко предоставлять критически важную для времени информацию и обновления статуса либо на регулярной, либо на специальной основе непосредственно Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-451">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="8ea4c-452">Приложение поддерживает местоположение в режиме реального времени, фотографии, заметки, уведомления о напоминаниях и автоматизированные рабочие процессы.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-452">The app supports real-time location, photos, notes, reminder notifications, and automated workflows.</span></span>

[<span data-ttu-id="8ea4c-453">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-453">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Создание представления регистрации](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="8ea4c-455">Опрос</span><span class="sxs-lookup"><span data-stu-id="8ea4c-455">Survey</span></span>

<span data-ttu-id="8ea4c-456">Опрос является пользовательским приложением Microsoft Teams [обмена сообщениями,](../messaging-extensions/what-are-messaging-extensions.md) которое позволяет создавать опрос в чате или канале для сбора данных и получения информации.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-456">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span> <span data-ttu-id="8ea4c-457">Приложение поддерживается во всех Teams платформы, таких как настольный компьютер, браузер, iOS и Android, и готово к развертыванию в рамках вашей Microsoft 365 подписки.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-457">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="8ea4c-458">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-458">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Создание опроса в Teams представлении](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally"></a><span data-ttu-id="8ea4c-460">Время Талли</span><span class="sxs-lookup"><span data-stu-id="8ea4c-460">Time Tally</span></span> 

<span data-ttu-id="8ea4c-461">Проект может включать в себя несколько задач, и различные проекты могут быть назначены сотрудникам.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-461">A project can include multiple tasks, and various projects can be assigned to employees.</span></span> <span data-ttu-id="8ea4c-462">Руководители должны понимать ход проекта в течение времени, затученного сотрудниками на решение этих задач.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-462">Managers are required to understand the project progress through the time spent by the employees on these tasks.</span></span> <span data-ttu-id="8ea4c-463">Это может быть громоздким действием, так как сотрудники должны заполнить расписания.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-463">This can be a cumbersome activity, as the employees need to fill in the timesheets.</span></span> <span data-ttu-id="8ea4c-464">Приложение Time Tally позволяет сотрудникам быстро заполнять свои расписания с помощью мобильного устройства, а менеджерам не нужно следить за сотрудниками в расписании.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-464">Time Tally app enables employees to fill their timesheets quickly, using the mobile device, and managers do not have to follow up with employees on the timesheet entry.</span></span> <span data-ttu-id="8ea4c-465">Менеджеры получают возможность просматривать использование проекта на основе ресурсов, и они могут утвердить или отклонить записи.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-465">Managers get to view the project utilization based on resources, and they can approve or reject the entries.</span></span> <span data-ttu-id="8ea4c-466">Уведомления напоминания отправляются для обеспечения соответствия расписанию.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-466">Reminder notifications are sent to ensure timesheet compliance.</span></span> <span data-ttu-id="8ea4c-467">Кроме того, исторические данные и использования доступны для аналитики.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-467">Also, historical data and utilizations are available for analytics.</span></span>

[<span data-ttu-id="8ea4c-468">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-468">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Время Талли](../assets/images/11zon_gif.gif)

## <a name="training--9734"></a><span data-ttu-id="8ea4c-470">Учебные &#9734;</span><span class="sxs-lookup"><span data-stu-id="8ea4c-470">Training  &#9734;</span></span>

<span data-ttu-id="8ea4c-471">Обучение является пользовательским [приложением Teams обмена сообщениями,](../messaging-extensions/what-are-messaging-extensions.md) которое позволяет пользователям публиковать обучение в чате или канале для обмена знаниями в автономном режиме и upskilling.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-471">Training is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables users to publish a training within a chat or a channel for offline knowledge sharing and upskilling.</span></span> <span data-ttu-id="8ea4c-472">Приложение поддерживается несколькими клиентами Teams платформы, такими как настольный компьютер, браузер, iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-472">The app is supported across multiple Teams platform clients, such as desktop, browser, iOS, and Android.</span></span> <span data-ttu-id="8ea4c-473">Это приложение готово к развертыванию в рамках вашей Microsoft 365 подписки.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-473">This app is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="8ea4c-474">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-474">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-training)

:::row:::
  :::column span="1":::
    ![Создание обучения в Teams представлении](../assets/images/training-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="virtual-rounding"></a><span data-ttu-id="8ea4c-476">Виртуальное округние</span><span class="sxs-lookup"><span data-stu-id="8ea4c-476">Virtual Rounding</span></span>

<span data-ttu-id="8ea4c-477">Поставщики больничных и отделения неотложной помощи **делают много** раундов в день.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-477">Hospital and emergency room providers make many **rounds** per day.</span></span> <span data-ttu-id="8ea4c-478">Эти быстрые регистрации на пациентов предназначены для обеспечения проверки статуса о том, как пациент делает и убедитесь, что проблемы пациента будут решены.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-478">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="8ea4c-479">Хотя округливание является важной практикой для обеспечения пациентов в настоящее время контролируется несколькими типами поставщиков, они представляют собой огромный утечки на СИЗ, потому что для каждого визита, от каждого поставщика, новая маска, и новый набор перчаток используются.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-479">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves are used.</span></span> <span data-ttu-id="8ea4c-480">С помощью шаблонов этого приложения, медицинские работники могут легко проводить раунды виртуально, Microsoft Teams встречи между поставщиком и пациентом.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-480">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="8ea4c-481">Виртуальное решение округливания также упоминается в Microsoft Health и наук [о жизни блога](https://aka.ms/teamsvirtualrounding).</span><span class="sxs-lookup"><span data-stu-id="8ea4c-481">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="8ea4c-482">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-482">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Виртуальное округние](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="8ea4c-484">Управление посетительами</span><span class="sxs-lookup"><span data-stu-id="8ea4c-484">Visitor Management</span></span>

<span data-ttu-id="8ea4c-485">Приложение «Управление посетителями» позволяет вашей организации и сотрудникам легко и эффективно управлять процессом посетителей на месте, непосредственно с Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-485">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="8ea4c-486">Приложение позволяет сотрудникам создавать запросы посетителей, централизованно отслеживать статус запроса через панель мониторинга посетителей и получать уведомления в режиме реального времени, когда посетитель прибывает.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-486">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="8ea4c-487">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-487">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

:::row:::
  :::column span="2":::
    ![Создание представления запроса](../assets/images/visitor-management-create-request.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Уведомление о прибытии посетителей](../assets/images/visitor-management-notify-host.png)
:::column-end:::
:::row-end:::

## <a name="workplace-awards"></a><span data-ttu-id="8ea4c-490">Награды на рабочем месте</span><span class="sxs-lookup"><span data-stu-id="8ea4c-490">Workplace Awards</span></span>

<span data-ttu-id="8ea4c-491">Workplace Awards – это Teams приложения, который обеспечивает позитивную основу для поощрения признания и поощрения культуры оценки сотрудников на современном рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-491">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="8ea4c-492">Приложение позволяет настроить и управлять вознаграждением и признанием сотрудников, называемой программой R&R, где сотрудники могут легко назначить и одобрить коллег, а ваш лидер R&R может просматривать представленные номинации, предоставлять награды и объявлять получателей.</span><span class="sxs-lookup"><span data-stu-id="8ea4c-492">The app enables you to setup and manage an employee rewards and recognition, called R&R program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="8ea4c-493">Получить его на GitHub</span><span class="sxs-lookup"><span data-stu-id="8ea4c-493">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="8ea4c-494">Карта номинации наград на рабочем месте</span><span class="sxs-lookup"><span data-stu-id="8ea4c-494">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Вкладка списка наград на рабочем месте](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="8ea4c-496">Для получения дополнительной информации о шаблоне приложения [см.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)</span><span class="sxs-lookup"><span data-stu-id="8ea4c-496">For more information on app template, see [App template](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>

## <a name="see-also"></a><span data-ttu-id="8ea4c-497">См. также</span><span class="sxs-lookup"><span data-stu-id="8ea4c-497">See also</span></span>

[<span data-ttu-id="8ea4c-498">Интеграция веб-приложений</span><span class="sxs-lookup"><span data-stu-id="8ea4c-498">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
