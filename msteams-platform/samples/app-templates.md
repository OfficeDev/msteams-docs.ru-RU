---
title: Шаблоны приложений Microsoft Teams
description: Ссылки и описания шаблонов приложений для платформы Microsoft Teams
ms.topic: reference
keywords: Шаблоны Microsoft Teams примеры демонстрации
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 04f32e7f35863d7c4b3e8744984eb6e27ec63396
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075761"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="627fe-104">Шаблоны приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="627fe-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="627fe-105">Шаблоны приложений — это примеры полных приложений для Microsoft Teams с открытым исходным кодом и доступных в GitHub.</span><span class="sxs-lookup"><span data-stu-id="627fe-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="627fe-106">Каждый шаблон приложения содержит подробные инструкции по развертыванию и установке этого приложения для организации.</span><span class="sxs-lookup"><span data-stu-id="627fe-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="627fe-107">Он также предоставляет пример приложения, которое можно установить и начать использовать немедленно.</span><span class="sxs-lookup"><span data-stu-id="627fe-107">It also provides a sample app that you can install and start using immediately.</span></span> <span data-ttu-id="627fe-108">Кроме того, доступен полный исходный код, который позволяет подробно изучить его или раздвоить код и изменить его, чтобы соответствовать определенным требованиям.</span><span class="sxs-lookup"><span data-stu-id="627fe-108">The complete source code is also available, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="627fe-109">Все шаблоны приложений предоставляются в соответствии с [условиями лицензии MIT.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)</span><span class="sxs-lookup"><span data-stu-id="627fe-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>

> [!NOTE] 
> <span data-ttu-id="627fe-110">Необходимо лицензировать и поддерживать приложения, созданные из шаблонов приложений для пользователей и организаций.</span><span class="sxs-lookup"><span data-stu-id="627fe-110">You must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="627fe-111">**&#9734; указывает только что выпущенные шаблоны приложений.**</span><span class="sxs-lookup"><span data-stu-id="627fe-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="627fe-112">Основные преимущества</span><span class="sxs-lookup"><span data-stu-id="627fe-112">Key benefits</span></span>

* <span data-ttu-id="627fe-113">**Развертывание непосредственно в облаке:** Все шаблоны приложений включают сценарии развертывания, которые позволяют развертывать все необходимые службы в Microsoft Azure или Power Platform.</span><span class="sxs-lookup"><span data-stu-id="627fe-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="627fe-114">**Рекомендуемый пример кода:** Шаблоны приложений соответствуют рекомендуемой рекомендации по безопасности и инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="627fe-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="627fe-115">Все внесенные сообществом изменения в шаблоны приложений проверяются для обеспечения соответствия.</span><span class="sxs-lookup"><span data-stu-id="627fe-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="627fe-116">**Настраиваемые и размязывные:** Несмотря на то, что все шаблоны приложений развернуты с минимальной конфигурацией, предоставляется вся база кода и сценарии развертывания, чтобы их можно было легко настроить или расширить, чтобы соответствовать вашим уникальным потребностям.</span><span class="sxs-lookup"><span data-stu-id="627fe-116">**Customizable and extensible:** While all app templates are deployed with minimal configuration, the entire code base and deployment scripts are provided, so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="627fe-117">**Подробные документы:** Все шаблоны приложений сопровождаются документацией по архитектуре решений, развертыванию и этапам конфигурации.</span><span class="sxs-lookup"><span data-stu-id="627fe-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot"></a><span data-ttu-id="627fe-118">Бот по внедрению</span><span class="sxs-lookup"><span data-stu-id="627fe-118">Adoption Bot</span></span> 

<span data-ttu-id="627fe-119">Средство принятия — это чат-бот по уходу за пользователями, построенный с помощью виртуального агента Power для Teams PVA.</span><span class="sxs-lookup"><span data-stu-id="627fe-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams PVA.</span></span> <span data-ttu-id="627fe-120">Он считается PVA-версией FAQ Plus.</span><span class="sxs-lookup"><span data-stu-id="627fe-120">It is considered as the PVA version of FAQ Plus.</span></span> <span data-ttu-id="627fe-121">Бот-принятия отвечает на 100+ распространенных вопросов о Microsoft 365 и Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="627fe-122">Можно редактировать существующие темы, добавлять собственные темы и гнать существующие вопросы.</span><span class="sxs-lookup"><span data-stu-id="627fe-122">You can edit the existing topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="627fe-123">Если пользователям нужна дополнительная помощь, Бот-пользователь может подключить их к экспертам или даже расширить доступ к билетам на обслуживание с соединиттелями потока премиум-класса.</span><span class="sxs-lookup"><span data-stu-id="627fe-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.</span></span> <span data-ttu-id="627fe-124">Этот бот самостоятельно установлен или встроен в пользовательское приложение, например концентратор [принятия.](https://github.com/akporzondek/adoption_hub)</span><span class="sxs-lookup"><span data-stu-id="627fe-124">This bot is self-installed or built into a custom app, such as the [Adoption Hub](https://github.com/akporzondek/adoption_hub).</span></span>

[<span data-ttu-id="627fe-125">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-125">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="adoption-tool--champion-management-platform-9734"></a><span data-ttu-id="627fe-126">Платформа управления средствами принятия и &#9734;</span><span class="sxs-lookup"><span data-stu-id="627fe-126">Adoption Tool- Champion Management Platform &#9734;</span></span>

<span data-ttu-id="627fe-127">Шаблон приложения Платформы управления чемпионами (CMP) помогает управлять, масштабировать и вдохновлять чемпионов командной работы, чтобы добиться большего.</span><span class="sxs-lookup"><span data-stu-id="627fe-127">The Champion Management Platform (CMP) app template helps you manage, scale, and inspire your teamwork champions to achieve more.</span></span> <span data-ttu-id="627fe-128">Этот шаблон приложения построен на SharePoint Framework и загружается на вкладку в команде.</span><span class="sxs-lookup"><span data-stu-id="627fe-128">This app template is built on the SharePoint Framework and loaded into a tab within a team.</span></span> <span data-ttu-id="627fe-129">Группы могут использовать этот инструмент для управления членством в программе, предоставления лидеров и типов событий для ведения журнала, а также инструментов для наложения цифровых значков для участников программы.</span><span class="sxs-lookup"><span data-stu-id="627fe-129">Groups can leverage this tool to help manage program membership, provide a leaderboard and event types for logging, and tools to overlay digital badges to program participants.</span></span>

[<span data-ttu-id="627fe-130">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-130">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started-9734"></a><span data-ttu-id="627fe-131">Средство принятия — пути обучения Microsoft 365 (Начало работы) &#9734;</span><span class="sxs-lookup"><span data-stu-id="627fe-131">Adoption Tool- Microsoft 365 Learning Pathways (Get Started) &#9734;</span></span>

<span data-ttu-id="627fe-132">Шаблон приложения Get Started позволяет использовать в microsoft 365 обучающие пути в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-132">The Get Started app template allows you to bring the power of Microsoft 365 learning pathways inside of Microsoft Teams.</span></span> <span data-ttu-id="627fe-133">Этот шаблон приложения позволяет легко получить доступ к определенным страницам обучения или другим интрасетям и загрузить содержимое непосредственно в Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-133">This app template allows you to grant easy access to specific training pages or other intranet assets and load the content directly within Teams.</span></span> <span data-ttu-id="627fe-134">Вы также можете изменить имя или логотип приложения, чтобы соответствовать брендингу вашей компании.</span><span class="sxs-lookup"><span data-stu-id="627fe-134">You can also change the app name or logo to match your company branding.</span></span>

[<span data-ttu-id="627fe-135">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-135">Get it on GitHub</span></span>](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="appointment-manager"></a><span data-ttu-id="627fe-136">Менеджер по встречам</span><span class="sxs-lookup"><span data-stu-id="627fe-136">Appointment Manager</span></span> 

<span data-ttu-id="627fe-137">Диспетчер назначений — это шаблон приложений Teams, который помогает предприятиям создавать, управлять и проводить виртуальные встречи с потребителями через Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-137">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="627fe-138">Новые запросы на прием от потребителей видны в каналах Teams, где они быстро назначены и назначены сотрудникам в команде.</span><span class="sxs-lookup"><span data-stu-id="627fe-138">New appointment requests from consumers are visible in Teams channels, where they are quickly assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="627fe-139">Запросы на назначение рассматриваются на командном или личном уровнях с помощью настраиваемой вкладки.</span><span class="sxs-lookup"><span data-stu-id="627fe-139">Appointment requests are viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="627fe-140">Каждая встреча связана с онлайн-собранием Teams, поэтому сотрудники и потребители могут легко присоединиться к собранию в запланированное время.</span><span class="sxs-lookup"><span data-stu-id="627fe-140">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="627fe-141">Шаблон приложения интегрируется с Microsoft Bookings для простого управления назначением.</span><span class="sxs-lookup"><span data-stu-id="627fe-141">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="627fe-142">Запланированные встречи автоматически отображаются в календарях назначенного персонала, а потребители получают настраиваемые уведомления электронной почты и напоминания со встроенными ссылками на собрания.</span><span class="sxs-lookup"><span data-stu-id="627fe-142">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="627fe-143">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-143">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="627fe-144">![Менеджер по обзору ](../assets/images/appointment-manager-overview.png)
 ![ назначений диспетчера назначений в teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="627fe-144">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="627fe-145">Ask Away</span><span class="sxs-lookup"><span data-stu-id="627fe-145">Ask Away</span></span>

<span data-ttu-id="627fe-146">Ask Away — это [бот Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям проводить сеансы вопросов и ответов, называемые Q&A в Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-146">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Question and Answer, called Q&A sessions within Teams.</span></span> <span data-ttu-id="627fe-147">С помощью бота Ask Away участники группы могут отправлять и задавать вопросы до голосования, общие коллегами, что позволяет Q&A-хостов для легкого сбора вопросов в канале или чате.</span><span class="sxs-lookup"><span data-stu-id="627fe-147">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="627fe-148">Бот используется для проведения сеанса Q&в режиме реального времени на собрании Teams и позволяет участникам отправлять вопросы в режиме реального времени в чате.</span><span class="sxs-lookup"><span data-stu-id="627fe-148">The bot is used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live through chat.</span></span>

[<span data-ttu-id="627fe-149">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-149">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Просмотр всплывающее окно в таблице лидеров для голосования пользователей по вопросам](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="627fe-151">Вспомогательная аналитика</span><span class="sxs-lookup"><span data-stu-id="627fe-151">Associate Insights</span></span>

<span data-ttu-id="627fe-152">Associate Insights — это шаблон [Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) который позволяет сотрудникам firstline напрямую фиксировать и отправлять мнения клиентов, настроения и восприятие.</span><span class="sxs-lookup"><span data-stu-id="627fe-152">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="627fe-153">Работники Firstline часто являются первым представителем компании, который может взаимодействовать с клиентами в контактной точке один к одному.</span><span class="sxs-lookup"><span data-stu-id="627fe-153">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="627fe-154">Собранные данные совместно используются бизнес-группами, например с помощью вкладки Power BI Teams, для улучшения продукта и улучшения взаимодействия с клиентами.</span><span class="sxs-lookup"><span data-stu-id="627fe-154">The collected data are shared and used collaboratively by business teams, such as through a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="627fe-155">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-155">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![Представление отзывов о созданных приложениях сведениях](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Power BI view of app generated insights](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="627fe-158">Присутствие</span><span class="sxs-lookup"><span data-stu-id="627fe-158">Attendance</span></span>

<span data-ttu-id="627fe-159">Приложение Для участия — это [вкладка Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) закрепленная в команде.</span><span class="sxs-lookup"><span data-stu-id="627fe-159">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that are pinned in a team.</span></span> <span data-ttu-id="627fe-160">Он предназначен для записи присутствия в таких параметрах, как среды обучения и обучения.</span><span class="sxs-lookup"><span data-stu-id="627fe-160">It is designed to record presence in settings, such as learning and training environments.</span></span> <span data-ttu-id="627fe-161">Пользователи могут отмечать или изменять посещаемость в течение до 30 дней в прошлом и просматривать обобщенные отчеты о посещаемости для всей группы или отдельных участников.</span><span class="sxs-lookup"><span data-stu-id="627fe-161">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span> <span data-ttu-id="627fe-162">Дополнительные сведения о посещаемости команд [см. в сайте Get it on GitHub.](https://github.com/OfficeDev/microsoft-teams-apps-attendance)</span><span class="sxs-lookup"><span data-stu-id="627fe-162">For more information on teams attendance, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance).</span></span>

<span data-ttu-id="627fe-163">На следующем изображении отображается демонстрация приложения для посещаемости:</span><span class="sxs-lookup"><span data-stu-id="627fe-163">The following image displays the attendance app demo:</span></span>  

![Демонстрация приложения для посещаемости](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="627fe-165">Book-a-room</span><span class="sxs-lookup"><span data-stu-id="627fe-165">Book-a-room</span></span>

<span data-ttu-id="627fe-166">Book-a-room — это бот [Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям быстро находить и резервировать зал собраний на 30, 60 или 90 минут начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="627fe-166">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="627fe-167">Время по умолчанию — 30 минут.</span><span class="sxs-lookup"><span data-stu-id="627fe-167">The default time is 30 minutes.</span></span> <span data-ttu-id="627fe-168">Область бота Book-a-room для личных или 1:1 бесед.</span><span class="sxs-lookup"><span data-stu-id="627fe-168">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="627fe-169">Дополнительные сведения о приложении Book-a-room см. в книге [Get it on GitHub.](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)</span><span class="sxs-lookup"><span data-stu-id="627fe-169">For more information on Book-a-room app, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom).</span></span>  
<span data-ttu-id="627fe-170">На следующем изображении отображается демо Book-a-room:</span><span class="sxs-lookup"><span data-stu-id="627fe-170">The following image displays the Book-a-room demo:</span></span>

![Демонстрация book-a-room](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="627fe-172">Доступ к зданиям</span><span class="sxs-lookup"><span data-stu-id="627fe-172">Building Access</span></span>

<span data-ttu-id="627fe-173">Building Access — это приложение, основанное на платформе Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) которое поддерживает администрирование пороговых значений заполняемости зданий и норм социального расстановки, позволяя директорам объектов управлять присутствием сотрудников на месте, отслеживать и сообщать о них.</span><span class="sxs-lookup"><span data-stu-id="627fe-173">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="627fe-174">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview)и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams и позволяет организациям определять готовность к созданию, устанавливать критерии приемлемости для доступа на месте и собирать сведения для планирования в будущем.</span><span class="sxs-lookup"><span data-stu-id="627fe-174">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="627fe-175">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-175">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Карта резервирования доступа к зданию](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Представление ключа "Создание доступа"](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="627fe-178">Праздники</span><span class="sxs-lookup"><span data-stu-id="627fe-178">Celebrations</span></span>

<span data-ttu-id="627fe-179">Celebrations — это приложение Teams, которое помогает участникам группы отмечать дни рождения, юбилеи и другие повторяющиеся события.</span><span class="sxs-lookup"><span data-stu-id="627fe-179">Celebrations is a Teams app that helps team members to celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="627fe-180">Он запоминает особые случаи всех членов команды и отправляет приветственное сообщение во всех командах, выбранных во время создания событий, чтобы участники группы чувствовали себя особенными в свой день.</span><span class="sxs-lookup"><span data-stu-id="627fe-180">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="627fe-181">Приложение предоставляет простой интерфейс для всех членов группы, чтобы лично добавить и просмотреть свои события, а также позволяет пользователю выбрать команды, в которых события получают общий доступ.</span><span class="sxs-lookup"><span data-stu-id="627fe-181">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="627fe-182">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-182">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="627fe-183">Контрольный список</span><span class="sxs-lookup"><span data-stu-id="627fe-183">Checklist</span></span>

<span data-ttu-id="627fe-184">Контрольный список — это настраиваемая программа расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которая позволяет вам сотрудничать со своей командой, создавая общий контрольный список в чате или канале.</span><span class="sxs-lookup"><span data-stu-id="627fe-184">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="627fe-185">Приложение поддерживается во всех клиентах платформы Teams, таких как настольный браузер, iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="627fe-185">The app is supported across all Teams platform clients, such as desktop browser, iOS, and Android.</span></span> <span data-ttu-id="627fe-186">Приложение готово к развертыванию в рамках подписки Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="627fe-186">The app is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="627fe-187">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-187">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app)

:::row:::
:::column span="2":::
    ![Создание контрольного списка в представлении Teams](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in"></a><span data-ttu-id="627fe-189">Заехав в класс</span><span class="sxs-lookup"><span data-stu-id="627fe-189">Classroom Drop-in</span></span> 

<span data-ttu-id="627fe-190">В классе Drop-in — это приложение на основе платформы Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)которое позволяет руководителям систем находить группы классов, означает виртуальные классы и добавлять себя или других в эти группы класса в течение указанного периода при необходимости.</span><span class="sxs-lookup"><span data-stu-id="627fe-190">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams, means virtual classrooms and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="627fe-191">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview) и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams, чтобы убедиться, что учебные заведения могут оптимизировать свои операции в гибридной среде обучения, предоставляя доступ к соответствующим заинтересованным сторонам для групп классов по бизнес-требованиям.</span><span class="sxs-lookup"><span data-stu-id="627fe-191">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="627fe-192">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-192">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Запрос на отсев класса](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="627fe-194">Корпоративный Communicator</span><span class="sxs-lookup"><span data-stu-id="627fe-194">Company Communicator</span></span>

<span data-ttu-id="627fe-195">Приложение Communicator позволяет корпоративным группам создавать и отправлять сообщения, предназначенные для нескольких групп или большого числа сотрудников в чате, позволяя организации достигать сотрудников прямо там, где они сотрудничают.</span><span class="sxs-lookup"><span data-stu-id="627fe-195">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="627fe-196">Используйте этот шаблон для нескольких сценариев, таких как новые объявления об инициативе, учет сотрудников, современное обучение и разработка или широкомасштабные трансляции.</span><span class="sxs-lookup"><span data-stu-id="627fe-196">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="627fe-197">Приложение обеспечивает простой интерфейс для назначенных пользователей для создания, предварительного просмотра, совместной работы и отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="627fe-197">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="627fe-198">Он создает основу для создания настраиваемой целевой системы связи, например настраиваемой телеметрии, о том, сколько пользователей было признано или взаимодействует с сообщением.</span><span class="sxs-lookup"><span data-stu-id="627fe-198">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="627fe-199">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-199">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator составить представление окна](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="627fe-201">Lookup контактной группы</span><span class="sxs-lookup"><span data-stu-id="627fe-201">Contact Group Lookup</span></span>

<span data-ttu-id="627fe-202">Приложение Lookup контактной группы предоставляет удобный и полезный подход к созданию, доступу и управлению контакт-группами организации, ранее известными как списки рассылки или группы связи.</span><span class="sxs-lookup"><span data-stu-id="627fe-202">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups, formerly known as distribution lists or communication groups.</span></span> <span data-ttu-id="627fe-203">Пользователи могут быстро просматривать и общаться с участниками группы, просматривать состояние участников и создавать групповой чат с выбранными участниками контактной группы, все в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-203">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="627fe-204">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-204">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![Просмотр контактной группы с закрепленным просмотром избранного](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Демонстрация запуска чата в контактной группе](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="co-worker-appreciation"></a><span data-ttu-id="627fe-207">Оценка сотрудников</span><span class="sxs-lookup"><span data-stu-id="627fe-207">Co-worker Appreciation</span></span> 

<span data-ttu-id="627fe-208">Используя шаблон оценки сотрудников в Microsoft Teams, пользователи могут распознавать достижения своих коллег в контексте Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-208">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="627fe-209">Когда сотрудники выбирают для вознаграждения коллегу, получатели и другие члены группы помечены в разговоре на канале, и они получают уведомление о вручениях канала.</span><span class="sxs-lookup"><span data-stu-id="627fe-209">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="627fe-210">Награды записывают в приложении Teams, которое является безопасным, переносным и легкодоступным.</span><span class="sxs-lookup"><span data-stu-id="627fe-210">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="627fe-211">Это рассматривается как версия шаблона приложения Open Badges на основе PowerApps с таблицей лидеров.</span><span class="sxs-lookup"><span data-stu-id="627fe-211">This is considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="627fe-212">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-212">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![В целом](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="627fe-214">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="627fe-214">CrowdSourcer</span></span>

<span data-ttu-id="627fe-215">CrowdSourcer — это [бот Microsoft Teams,](../bots/what-are-bots.md) который предоставляет группам запрашиваемую информацию, которую совместно запрашивают члены группы.</span><span class="sxs-lookup"><span data-stu-id="627fe-215">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="627fe-216">Это помогает отвечать на часто задамые вопросы, позволяя участникам активно участвовать и вносить вклад в интересный и полезный информационный ресурс.</span><span class="sxs-lookup"><span data-stu-id="627fe-216">It helps to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="627fe-217">Get it on Github</span><span class="sxs-lookup"><span data-stu-id="627fe-217">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Взаимодействие с конечным пользователем crowdsource](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="627fe-219">Пользовательские наклейки</span><span class="sxs-lookup"><span data-stu-id="627fe-219">Custom Stickers</span></span>

<span data-ttu-id="627fe-220">Самовыражение является основой здоровой культуры команды.</span><span class="sxs-lookup"><span data-stu-id="627fe-220">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="627fe-221">Этот шаблон приложения — это расширение [обмена](~/messaging-extensions/what-are-messaging-extensions.md) сообщениями, которое позволяет пользователям использовать настраиваемые наклейки и GIF-решения в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-221">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="627fe-222">Этот шаблон предоставляет простой веб-опыт конфигурации, где любой пользователь с доступом к конфигурации может загружать GIF-изображения, giF,наклейки и изображения, которые они хотят иметь, что позволяет всей вашей команде использовать любой набор стикеров, которые вы выбираете.</span><span class="sxs-lookup"><span data-stu-id="627fe-222">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs, stickers, and images they want their users to have, allowing your entire team to use any set of stickers you choose.</span></span>

<span data-ttu-id="627fe-223">Это приложение также позволяет легко обмениваться изображениями, GIF-файлами, наклейками между группами без доступа к сайтам SharePoint или отдельным каналам в качестве механизмов хранения и общего доступа.</span><span class="sxs-lookup"><span data-stu-id="627fe-223">This app also enables easy sharing of images, GIFs, stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="627fe-224">Например, группы продуктов могут легко обмениваться изображениями продуктов и GIF-изображениями с группами социальных сетей, маркетинга и продаж программным образом.</span><span class="sxs-lookup"><span data-stu-id="627fe-224">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="627fe-225">Можно также расширить это приложение, запуская поток уведомлений для определенных групп или отдельных лиц, когда новые изображения и GIF-изображения доступны.</span><span class="sxs-lookup"><span data-stu-id="627fe-225">One can also extend this app by triggering a notification flow to specific teams or individuals when new images, and GIFs are made available.</span></span>

[<span data-ttu-id="627fe-226">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-226">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Приложение Стикеры](../assets/images/stickers.png)

## <a name="employee-ideas"></a><span data-ttu-id="627fe-228">Идеи сотрудников</span><span class="sxs-lookup"><span data-stu-id="627fe-228">Employee Ideas</span></span>

<span data-ttu-id="627fe-229">Приложение "Идеи сотрудников" — это версия PowerApps шаблона приложения Great Ideas на основе Azure.</span><span class="sxs-lookup"><span data-stu-id="627fe-229">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="627fe-230">Приложение позволяет пользователям Teams настраивать и настраивать кампанию идей.</span><span class="sxs-lookup"><span data-stu-id="627fe-230">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="627fe-231">Кампания идей — это категория для группировки идей вокруг общих тем.</span><span class="sxs-lookup"><span data-stu-id="627fe-231">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="627fe-232">Пользователи teams также могут выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="627fe-232">Teams users can also perform the following activities:</span></span>

* <span data-ttu-id="627fe-233">Настройте стандартную форму отправки, которую сотрудники должны отправить для каждой идеи.</span><span class="sxs-lookup"><span data-stu-id="627fe-233">Configure a standard submission form that employees must submit for each idea.</span></span> 
* <span data-ttu-id="627fe-234">Просмотрите и управляйте идеями и списком кампаний.</span><span class="sxs-lookup"><span data-stu-id="627fe-234">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="627fe-235">Изменение и удаление кампаний.</span><span class="sxs-lookup"><span data-stu-id="627fe-235">Modify and delete campaigns.</span></span>
* <span data-ttu-id="627fe-236">Просмотрите советы лидеров идей.</span><span class="sxs-lookup"><span data-stu-id="627fe-236">Review leader boards of ideas.</span></span>
* <span data-ttu-id="627fe-237">Голосуйте за и делитесь приоритетными идеями.</span><span class="sxs-lookup"><span data-stu-id="627fe-237">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="627fe-238">Отправка идей для кампании.</span><span class="sxs-lookup"><span data-stu-id="627fe-238">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="627fe-239">Просмотр идеи другого члена группы.</span><span class="sxs-lookup"><span data-stu-id="627fe-239">View other team member's idea.</span></span>
* <span data-ttu-id="627fe-240">Голосуйте за наиболее понравились идеи.</span><span class="sxs-lookup"><span data-stu-id="627fe-240">Vote on most liked ideas.</span></span>
* <span data-ttu-id="627fe-241">Просмотрите производительность их идей по сравнению с другими в рамках кампании.</span><span class="sxs-lookup"><span data-stu-id="627fe-241">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="627fe-242">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-242">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Управление представлением кампании](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="627fe-244">Электронные рецепты</span><span class="sxs-lookup"><span data-stu-id="627fe-244">E-Prescriptions</span></span> 

<span data-ttu-id="627fe-245">E-Prescriptions — это приложение на основе [power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) которое улучшает телемедицину и виртуальную помощь путем автоматизации процесса выдачи электронных рецептов пациентам.</span><span class="sxs-lookup"><span data-stu-id="627fe-245">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="627fe-246">Медицинские специалисты могут быстро пересматривать встречи, создавать электронные рецепты и отправлять электронные письма с вложениями по электронному рецепту пациентам непосредственно на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-246">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="627fe-247">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-247">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![Снимок экрана приложения E-Prescriptions.](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Снимок экрана приложения E-Prescriptions.](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training"></a><span data-ttu-id="627fe-252">Обучение сотрудников</span><span class="sxs-lookup"><span data-stu-id="627fe-252">Employee Training</span></span> 

<span data-ttu-id="627fe-253">Обучение сотрудников — это приложение Microsoft Teams, которое позволяет организаторам легко публиковать, отслеживать и содействовать обучению и учебным мероприятиям для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="627fe-253">Employee training is a Microsoft Teams app that enables organizers to easily publish, track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="627fe-254">С помощью приложения организаторы событий могут отправлять напоминания и уведомления регистрантам событий, а сотрудники могут указывать на интерес к предстоящим событиям, обновлять текущие события и делиться сведениями о событиях с коллегами через расширение обмена сообщениями Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-254">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues through the Teams messaging extension.</span></span>

[<span data-ttu-id="627fe-255">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-255">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="627fe-256">**Просмотр событий обучения сотрудников** ![ Изображение вкладки подготовки сотрудников](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="627fe-256">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="627fe-257">**Создание события подготовки сотрудников** ![ Обучение сотрудников создает форму событий](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="627fe-257">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="627fe-258">Эксперт finder</span><span class="sxs-lookup"><span data-stu-id="627fe-258">Expert Finder</span></span>

<span data-ttu-id="627fe-259">Expert Finder — это [бот Microsoft Teams,](../bots/what-are-bots.md) который определяет конкретных членов организации на основе их навыков, интересов и атрибутов образования.</span><span class="sxs-lookup"><span data-stu-id="627fe-259">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="627fe-260">Участники находят экспертов в организации, которые соответствуют поиску ключевых слов профилей пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="627fe-260">Members find experts within an organization that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="627fe-261">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-261">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Демонстрация результатов поиска expert Finder](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="627fe-263">Вопросы и ответы плюс</span><span class="sxs-lookup"><span data-stu-id="627fe-263">FAQ Plus</span></span>

<span data-ttu-id="627fe-264">Диалоговая&боты — это простой способ предоставления ответов на часто задамые пользователями вопросы.</span><span class="sxs-lookup"><span data-stu-id="627fe-264">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="627fe-265">Но большинство ботов не могут эффективно взаимодействовать с пользователями, так как при сбойе бота в цикле нет человека.</span><span class="sxs-lookup"><span data-stu-id="627fe-265">But, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="627fe-266">FaQ bot — это дружественный Q&бот, который приводит человека в цикл, когда он не в состоянии помочь.</span><span class="sxs-lookup"><span data-stu-id="627fe-266">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="627fe-267">Можно задать боту вопрос, и бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="627fe-267">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="627fe-268">Если нет, бот позволяет пользователю отправлять запрос, который затем передается предварительно настроенной группе экспертов, которые помогают обеспечить поддержку, действуя на уведомления из самой группы.</span><span class="sxs-lookup"><span data-stu-id="627fe-268">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="627fe-269">Последний выпуск **FAQ Plus** поддерживает улучшенные решения Q&, позволяя группе экспертов выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="627fe-269">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="627fe-270">&#x2714; Q&как непосредственно в базу знаний с помощью расширений сообщений.</span><span class="sxs-lookup"><span data-stu-id="627fe-270">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="627fe-271">&#x2714; изменить и удалить Q&пары, добавленные ботом.</span><span class="sxs-lookup"><span data-stu-id="627fe-271">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="627fe-272">&#x2714; отслеживание истории пересмотра Q&As.</span><span class="sxs-lookup"><span data-stu-id="627fe-272">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="627fe-273">&#x2714; настройка ответа с дополнительными сведениями для отображения в качестве [адаптивной карты.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="627fe-273">&#x2714; Configure an answer with additional details to display as an [Adaptive Card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="627fe-274">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Gif FAQ Plus](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app"></a><span data-ttu-id="627fe-276">Получить приложение поддержки</span><span class="sxs-lookup"><span data-stu-id="627fe-276">Get Support App</span></span>

<span data-ttu-id="627fe-277">Приложение Get Support используется организациями, использующими Microsoft Teams, чтобы позволить любому набору пользователей запрашивать помощь у руководителей.</span><span class="sxs-lookup"><span data-stu-id="627fe-277">The Get Support app is used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="627fe-278">Это приложение включает следующие функции:</span><span class="sxs-lookup"><span data-stu-id="627fe-278">This app includes the following features:</span></span>
* <span data-ttu-id="627fe-279">Запрос помощи для разных категорий в приложении Power.</span><span class="sxs-lookup"><span data-stu-id="627fe-279">Requesting assistance on different categories from a Power App.</span></span>
* <span data-ttu-id="627fe-280">Уведомления, отправленные запросчикам, информирующие их о том, кому назначен заяц.</span><span class="sxs-lookup"><span data-stu-id="627fe-280">Notifications sent to requestors informing them of who hare assigned.</span></span>
* <span data-ttu-id="627fe-281">Уведомления, отосланные назначенному руководителю, информирующие их о том, кому нужна помощь.</span><span class="sxs-lookup"><span data-stu-id="627fe-281">Notifications sent to assigned supervisors informing them of who needs assistance.</span></span> 
* <span data-ttu-id="627fe-282">Анализ эскалаций и шаблонов в SharePoint и PowerBI.S</span><span class="sxs-lookup"><span data-stu-id="627fe-282">Analyzing escalations and patterns in SharePoint and PowerBI.S</span></span>

[<span data-ttu-id="627fe-283">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-283">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Get Support Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="627fe-285">Отслеживание целей</span><span class="sxs-lookup"><span data-stu-id="627fe-285">Goal Tracker</span></span>

<span data-ttu-id="627fe-286">Приложение Goal Tracker — это комплексное решение для организации, которое поддерживает установление целей, наблюдение за прогрессом и признание успеха в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-286">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="627fe-287">Приложение позволяет пользователям устанавливать, отслеживать и обновлять цели на профессиональном, личном и командном уровне.</span><span class="sxs-lookup"><span data-stu-id="627fe-287">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="627fe-288">Члены группы также получают вовремя напоминания и обновления состояния, чтобы оставаться сосредоточенными и оставаться в курсе.</span><span class="sxs-lookup"><span data-stu-id="627fe-288">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="627fe-289">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-289">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![Набор целей](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр поставленных целей](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a><span data-ttu-id="627fe-292">Великие идеи</span><span class="sxs-lookup"><span data-stu-id="627fe-292">Great Ideas</span></span>

<span data-ttu-id="627fe-293">Приложение Great Ideas поддерживает и расширяет возможности инноваций и творчества в организации.</span><span class="sxs-lookup"><span data-stu-id="627fe-293">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="627fe-294">Приложение позволяет сотрудникам обмениваться идеями с коллегами и руководством, открывать новые материалы, делать акценты на одноранговом рассмотрении и голосовать за лучшие предложения в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-294">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="627fe-295">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-295">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a><span data-ttu-id="627fe-298">Групповые действия</span><span class="sxs-lookup"><span data-stu-id="627fe-298">Group Activities</span></span>

<span data-ttu-id="627fe-299">Групповые действия — это приложение Microsoft Teams, которое позволяет владельцам групп быстро создавать группы действий и управлять рабочими процессами совместной работы в контексте Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-299">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="627fe-300">Авторы действий могут создавать действия, случайным образом распределять членов группы по группам и необязательно отправлять напоминания боту до завершения действий.</span><span class="sxs-lookup"><span data-stu-id="627fe-300">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="627fe-301">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-301">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Список групповых действий в Teams](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Сообщение об уведомлении о групповой активности в канале](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="grow-your-skills"></a><span data-ttu-id="627fe-304">Вырастите свои навыки</span><span class="sxs-lookup"><span data-stu-id="627fe-304">Grow Your Skills</span></span>

<span data-ttu-id="627fe-305">Приложение Grow Your Skills поддерживает профессиональный рост и развитие, позволяя сотрудникам вносить вклад в дополнительные проекты для вашей организации, одновременно изучая новые навыки.</span><span class="sxs-lookup"><span data-stu-id="627fe-305">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="627fe-306">Сотрудники могут использовать приложение для поиска возможностей, которые отвечают их интересам, эффективного взаимодействия с коллегами и получения новых уровней знаний и возможностей, все в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-306">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="627fe-307">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-307">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![Представление доступных проектов](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр приобретенных навыков зрителя](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a><span data-ttu-id="627fe-310">Поддержка управления персоналом</span><span class="sxs-lookup"><span data-stu-id="627fe-310">HR Support</span></span>

<span data-ttu-id="627fe-311">Бот поддержки кадров — это дружественный Q&бот, который привозит специалиста или специалиста по поддержке из группы hr в цикл, когда он не может помочь.</span><span class="sxs-lookup"><span data-stu-id="627fe-311">HR Support bot is a friendly Q&A bot that brings a support professional or expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="627fe-312">Можно задать боту вопрос, и бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="627fe-312">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="627fe-313">Если нет, бот позволяет пользователю отправить запрос, который затем будет размещен в предварительно настроенной группе экспертов, которые помогают оказывать поддержку, действуя на уведомления из самой команды.</span><span class="sxs-lookup"><span data-stu-id="627fe-313">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="627fe-314">Кроме того, бот предлагает ссылки на рекомендуемые политики кадров или вопросы, ища предварительно настроенные теги в этом вопросе.</span><span class="sxs-lookup"><span data-stu-id="627fe-314">Additionally, the bot suggests links to recommended HR policies or questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="627fe-315">Эти плитки находятся на связанной вкладке в качестве быстрой ссылки.</span><span class="sxs-lookup"><span data-stu-id="627fe-315">These tiles are found in the associated tab as a quick reference.</span></span> <span data-ttu-id="627fe-316">Поддержка отдела кадров хорошо работает для&Q&A и обеспечивает быструю поддержку при запуске новых проектов или инициатив в организации.</span><span class="sxs-lookup"><span data-stu-id="627fe-316">HR Support works well for light weight Q&A and to provide quick support when launching new projects or initiatives in the organization.</span></span>

[<span data-ttu-id="627fe-317">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-317">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Поддержка управления персоналом](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="627fe-319">Точки соприкосновения</span><span class="sxs-lookup"><span data-stu-id="627fe-319">Icebreaker</span></span>

<span data-ttu-id="627fe-320">Icebreaker — это [бот Microsoft Teams,](../bots/what-are-bots.md) который помогает вашей команде приблизиться, спарив двух случайных членов команды каждую неделю для встречи.</span><span class="sxs-lookup"><span data-stu-id="627fe-320">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="627fe-321">Бот упрощает планирование, автоматически предлагая свободное время, которое работает для обоих участников.</span><span class="sxs-lookup"><span data-stu-id="627fe-321">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="627fe-322">Укрепляйте личные связи и создайте тесное сообщество с помощью этого приложения.</span><span class="sxs-lookup"><span data-stu-id="627fe-322">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="627fe-323">Помимо поощрения личных подключений всей вашей команды, приложение Icebreaker может помочь развивать сообщества, основанные на интересах вашей организации.</span><span class="sxs-lookup"><span data-stu-id="627fe-323">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="627fe-324">Например, это приложение можно использовать для группы по интересам DevOps, чтобы помочь идеям и лучшим практикам органично распространяться по всей организации.</span><span class="sxs-lookup"><span data-stu-id="627fe-324">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="627fe-325">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-325">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Приложение Icebreaker](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="627fe-327">Стимулы</span><span class="sxs-lookup"><span data-stu-id="627fe-327">Incentives</span></span>

<span data-ttu-id="627fe-328">Стимулы — это шаблон [Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) который управляет и отслеживает стимулирование участия сотрудников в назначенных мероприятиях, таких как тренинги и инициативы по управлению изменениями.</span><span class="sxs-lookup"><span data-stu-id="627fe-328">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities, such as trainings and change management initiatives.</span></span> <span data-ttu-id="627fe-329">Администраторы используют приложение для создания назначенных действий, назначения точек для завершения и указания необходимых уровней точки права на вознаграждение.</span><span class="sxs-lookup"><span data-stu-id="627fe-329">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="627fe-330">Сотрудники используют приложение для просмотра накопленных баллов и по достижении допустимости запрашивать и требовать выкупаемых вознаграждений.</span><span class="sxs-lookup"><span data-stu-id="627fe-330">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="627fe-331">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-331">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Демонстрация приложения incentives](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="627fe-333">Репортер инцидентов</span><span class="sxs-lookup"><span data-stu-id="627fe-333">Incident Reporter</span></span>

<span data-ttu-id="627fe-334">Incident Reporter — это [бот Microsoft Teams,](../bots/what-are-bots.md)  который оптимизирует управление инцидентами в организации.</span><span class="sxs-lookup"><span data-stu-id="627fe-334">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="627fe-335">Бот упрощает автоматизированный сбор данных об инцидентах, настраиваемые отчеты об инцидентах, соответствующие уведомления заинтересованных лиц и отслеживание инцидентов в конце концов.</span><span class="sxs-lookup"><span data-stu-id="627fe-335">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="627fe-336">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-336">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![Представление области области группы репортеров инцидентов](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр личных областей репортера инцидентов](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="inspection"></a><span data-ttu-id="627fe-339">Проверка</span><span class="sxs-lookup"><span data-stu-id="627fe-339">Inspection</span></span> 

 <span data-ttu-id="627fe-340">Inspection — это приложение Microsoft Teams, которое позволяет сотрудникам передней линии проверять все, что угодно от расположения до активов и оборудования.</span><span class="sxs-lookup"><span data-stu-id="627fe-340">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="627fe-341">Например, розничный магазин, завод по производству или транспортные средства и машины.</span><span class="sxs-lookup"><span data-stu-id="627fe-341">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="627fe-342">В этом решении есть два приложения, каждое из которых предназначено для разных типов пользователей.</span><span class="sxs-lookup"><span data-stu-id="627fe-342">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="627fe-343">Приложение предоставляет сотрудникам передней линии возможность проверять актив или область, управлять качеством продуктов и услуг или поддерживать безопасность на рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="627fe-343">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="627fe-344">Это облегчает связь между членами группы для решения проблем, найденных во время проверки.</span><span class="sxs-lookup"><span data-stu-id="627fe-344">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="627fe-345">Приложение предоставляет простые отчеты для руководителей, чтобы ускорить решение проблем и выделить тенденции.</span><span class="sxs-lookup"><span data-stu-id="627fe-345">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="627fe-346">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-346">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Обзор инспекции](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a><span data-ttu-id="627fe-348">Отчеты о проблемах</span><span class="sxs-lookup"><span data-stu-id="627fe-348">Issue Reporting</span></span>

<span data-ttu-id="627fe-349">Приложение Отчеты о проблемах позволяет сотрудникам и руководителям поднимать и управлять вопросами.</span><span class="sxs-lookup"><span data-stu-id="627fe-349">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="627fe-350">Она состоит из двух приложений: приложения для отчетов о проблемах и приложения "Управление вопросами" для управления вопросами.</span><span class="sxs-lookup"><span data-stu-id="627fe-350">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="627fe-351">Руководители групп используют приложение Manage Issues для настройки приложения, в том числе канала, в котором приложения создают сообщения Microsoft Teams и задачи планировщика.</span><span class="sxs-lookup"><span data-stu-id="627fe-351">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="627fe-352">Менеджеры также используют приложение для создания форм шаблонов для сбора сведений, когда пользователь сообщает о проблеме.</span><span class="sxs-lookup"><span data-stu-id="627fe-352">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="627fe-353">Например, просмотрите, отредактируете или удалите формы шаблона проблем.</span><span class="sxs-lookup"><span data-stu-id="627fe-353">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="627fe-354">Приложение также используется для проверки проблем группы, отчета об истории проблем и эффективного управления решением проблем.</span><span class="sxs-lookup"><span data-stu-id="627fe-354">The app is also used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="627fe-355">Сотрудники используют приложение отчетов о проблемах для журналов проблем и сведений, необходимых для их устранения.</span><span class="sxs-lookup"><span data-stu-id="627fe-355">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="627fe-356">Приложение также используется для изменения и решения существующих проблем и получения высокого уровня представления об отдельных или командных проблемах.</span><span class="sxs-lookup"><span data-stu-id="627fe-356">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="627fe-357">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-357">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Представление группы отчетов о проблемах](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="627fe-359">Новые возможности для сотрудников</span><span class="sxs-lookup"><span data-stu-id="627fe-359">New Employee Onboarding</span></span> 

<span data-ttu-id="627fe-360">Новая интеграция сотрудников — это интегрированное решение microsoft Teams и [SharePoint New Employee Onboarding,](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) которое позволяет организации предоставлять сотрудникам в пути по новому найму согласованный и высококачественный опыт работы с бортовой командой.</span><span class="sxs-lookup"><span data-stu-id="627fe-360">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="627fe-361">Приложение используется группами кадров и менеджерами по найму для предоставления соответствующих сведений в процессе ориентации и индукции, а также для обмена отзывами, предоставления представлений и выполнения задач бортового ввода.</span><span class="sxs-lookup"><span data-stu-id="627fe-361">The app is used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="627fe-362">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-362">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="627fe-363">**Новая приветствие сотрудника** ![ Изображение новой приветствия сотрудника](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="627fe-363">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="627fe-364">**Новый контрольный список сотрудников** ![ Изображение нового контрольного списка сотрудников](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="627fe-364">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="627fe-365">Открыть значки</span><span class="sxs-lookup"><span data-stu-id="627fe-365">Open Badges</span></span>

<span data-ttu-id="627fe-366">Open Badges — это приложение Microsoft Teams, которое позволяет пользователям получать цифровые значки учетных данных для обучения в контексте Teams и делиться ими во всем мире.</span><span class="sxs-lookup"><span data-stu-id="627fe-366">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="627fe-367">Использование возможностей сторонних органов по выдаче цифровых значков [Badgr](https://badgr.org/), отмеченных значками, записывается в профиле Badgr получателя и доступно для создания и обмена богатой картиной путешествий по обучению в течение всей жизни.</span><span class="sxs-lookup"><span data-stu-id="627fe-367">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="627fe-368">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-368">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![Изображение доступных значков](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр отмеченных значков](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="poll"></a><span data-ttu-id="627fe-371">Опрос</span><span class="sxs-lookup"><span data-stu-id="627fe-371">Poll</span></span> 

<span data-ttu-id="627fe-372">Poll — это настраиваемая программа расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которая позволяет быстро создавать и отправлять опросы в чате или канале для сбора мнений и предпочтений группы.</span><span class="sxs-lookup"><span data-stu-id="627fe-372">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="627fe-373">Приложение поддерживается во всех клиентах платформы Teams, таких как настольный компьютер, браузер, iOS и Android, и готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="627fe-373">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="627fe-374">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-374">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Создание опроса в представлении Teams](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="627fe-376">Быстрые ответы</span><span class="sxs-lookup"><span data-stu-id="627fe-376">Quick Responses</span></span>

<span data-ttu-id="627fe-377">Quick Responses — это приложение Microsoft Teams, которое предоставляет надежное решение для эффективного ответа на часто задаваемые вопросы.</span><span class="sxs-lookup"><span data-stu-id="627fe-377">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions FAQs.</span></span> <span data-ttu-id="627fe-378">Вместо того, чтобы отвечать на каждый запрос вручную и непрерывно повторять информацию, приложение создает библиотеку ответов для интерактивного пользовательского интерфейса с помощью расширений обмена сообщениями [Teams.](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="627fe-378">Instead of answering each query manually and continuously repeating information, the app builds a library of responses for an interactive user experience through Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="627fe-379">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-379">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Пример представления ответов](../assets/images/quick-responses.png)

## <a name="quiz--9734"></a><span data-ttu-id="627fe-381">Тест &#9734;</span><span class="sxs-lookup"><span data-stu-id="627fe-381">Quiz  &#9734;</span></span>

<span data-ttu-id="627fe-382">Quiz — это настраиваемая программа расширения обмена сообщениями [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которая позволяет создавать викторину в чате или канале проверки знаний и мгновенных результатов.</span><span class="sxs-lookup"><span data-stu-id="627fe-382">Quiz is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a quiz within a chat or a channel for knowledge check and instantaneous results.</span></span> <span data-ttu-id="627fe-383">Вы можете использовать тесты для экзаменов в классе и автономном режиме, проверку знаний в команде и забавные викторины в команде.</span><span class="sxs-lookup"><span data-stu-id="627fe-383">You can use Quiz for, In-class and offline exams, Knowledge check within team, and for fun quizzes within a team.</span></span> <span data-ttu-id="627fe-384">Приложение викторины поддерживается на нескольких платформах, таких как настольные компьютеры Teams, браузеры, iOS и Android-клиенты.</span><span class="sxs-lookup"><span data-stu-id="627fe-384">Quiz app is supported across multiple platforms, such as Teams desktop, browser, iOS, and Android clients.</span></span> <span data-ttu-id="627fe-385">Это приложение готово к развертыванию в рамках существующей подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="627fe-385">This app is ready for deployment as part of your existing Microsoft 365 subscription.</span></span>

[<span data-ttu-id="627fe-386">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-386">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quiz)

:::row:::
  :::column span="1":::
    ![Создание викторины в представлении Teams](../assets/images/quiz-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="rapid-assist"></a><span data-ttu-id="627fe-388">Rapid Assist</span><span class="sxs-lookup"><span data-stu-id="627fe-388">Rapid Assist</span></span>

<span data-ttu-id="627fe-389">Rapid Assist — это приложение, основанное на платформе Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) которое позволяет партнерам с клиентами быстро подключаться к экспертам, получать быстрые ответы, искать информацию, выполнять открытые запросы и получать уведомления, чтобы быстро получить вызов, чтобы помочь ответить на вопросы.</span><span class="sxs-lookup"><span data-stu-id="627fe-389">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="627fe-390">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview) и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams, чтобы организации могли легко подключать сотрудников передней линии связи с корпоративными связями для решения запросов клиентов и обеспечения отличного обслуживания клиентов.</span><span class="sxs-lookup"><span data-stu-id="627fe-390">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="627fe-391">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-391">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Интерфейс запроса конечных пользователей](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Представление запроса эксперта](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="627fe-394">Отражение</span><span class="sxs-lookup"><span data-stu-id="627fe-394">Reflect</span></span> 

<span data-ttu-id="627fe-395">Reflect — это настраиваемая программа расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которая предоставляет безопасный и инклюзивный ресурс для членов вашей команды, чтобы поделиться состоянием своего эмоционального благополучия с коллегами или руководителями групп непосредственно в Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-395">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues or group leaders directly within Teams.</span></span> <span data-ttu-id="627fe-396">Приложение доступно в чатах каналов, групп, собраний и 1:1, а ответ на регистрацию устанавливается для общедоступных, частных и полностью анонимных.</span><span class="sxs-lookup"><span data-stu-id="627fe-396">The app is available in channel, group, meeting, and 1:1 chats and the check-in response is set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="627fe-397">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-397">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="627fe-398">**Опрос благополучия**</span><span class="sxs-lookup"><span data-stu-id="627fe-398">**Well-being poll**</span></span>
    
    ![Отражение опроса пользователей приложения](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="627fe-400">Удаленная поддержка</span><span class="sxs-lookup"><span data-stu-id="627fe-400">Remote Support</span></span>

<span data-ttu-id="627fe-401">Удаленная поддержка — это [бот Microsoft Teams,](../bots/what-are-bots.md) который обеспечивает целенаправленный интерфейс между запрашивателями поддержки по всей организации и внутренней группе поддержки.</span><span class="sxs-lookup"><span data-stu-id="627fe-401">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="627fe-402">Конечные пользователи могут отправлять, редактировать или отзывать запросы на поддержку, а группа поддержки может отвечать, управлять и обновлять запросы на все запросы на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-402">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="627fe-403">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-403">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![Форма поддержки запроса](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Запрос сведений о поддержке](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a><span data-ttu-id="627fe-406">Request-a-team</span><span class="sxs-lookup"><span data-stu-id="627fe-406">Request-a-team</span></span>

<span data-ttu-id="627fe-407">Request-a-team — это приложение Microsoft Teams, которое оптимизирует создание новых групп для организации предприятия.</span><span class="sxs-lookup"><span data-stu-id="627fe-407">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="627fe-408">Приложение поддерживает стандартизацию и передовую практику при создании новых экземпляров группы с помощью интеграции формы запроса с управляемым мастером, встроенного процесса утверждения, панели мониторинга состояния запроса и создания автоматизированной группы.</span><span class="sxs-lookup"><span data-stu-id="627fe-408">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="627fe-409">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-409">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![Представление страницы запуска запроса с командой](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Представление страницы мастера запроса с командой](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a><span data-ttu-id="627fe-412">Scrums для каналов</span><span class="sxs-lookup"><span data-stu-id="627fe-412">Scrums for Channels</span></span>

<span data-ttu-id="627fe-413">Scrums for Channels — это приложение-помощник scrum, которое позволяет пользователям планировать и запускать scrums в каналах в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-413">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="627fe-414">Приложение отлично подходит для удаленных групп и групп, состоящих из участников из различных географических расположений и часовых поясов, чтобы обмениваться ежедневными обновлениями и обеспечивать участие в заседаниях стендап scrum.</span><span class="sxs-lookup"><span data-stu-id="627fe-414">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="627fe-415">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-415">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="627fe-416">Для проведения собраний по scrum в групповом чате см. [шаблон приложения Scrums for Group Chat.](#scrums-for-group-chat)</span><span class="sxs-lookup"><span data-stu-id="627fe-416">To conduct scrum meetings in a group chat, see [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

:::row:::
  :::column span="2":::
    ![Scrums для просмотра параметров каналов](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Scrums для просмотра состояния участника группы каналов](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a><span data-ttu-id="627fe-419">Scrums для группового чата</span><span class="sxs-lookup"><span data-stu-id="627fe-419">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="627fe-420">Шаблон приложения Состояния Scrums обновляется и теперь является Scrums для группового чата.</span><span class="sxs-lookup"><span data-stu-id="627fe-420">The Scrums Status app template is updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="627fe-421">Scrums для группового чата является вспомогательным помощником scrum, который позволяет участникам группового чата запускать асинхронные собрания и легко делиться своими ежедневными обновлениями.</span><span class="sxs-lookup"><span data-stu-id="627fe-421">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="627fe-422">Это позволяет всем участникам группового чата вносить вклад в схватку и просматривать обновления, сделанные другими пользователями в рабочей схватке.</span><span class="sxs-lookup"><span data-stu-id="627fe-422">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="627fe-423">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-423">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Scrums для демонстрации группового чата](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="627fe-425">Share Now</span><span class="sxs-lookup"><span data-stu-id="627fe-425">Share Now</span></span> 

<span data-ttu-id="627fe-426">Приложение Share Now способствует позитивному обмену информацией между коллегами, позволяя пользователям легко обмениваться контентом в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-426">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="627fe-427">Пользователи вовлекли приложение в обмен элементами, которые интересуют участников группы, обнаруживая новое общее содержимое, задав предпочтения и закладки для более позднего чтения.</span><span class="sxs-lookup"><span data-stu-id="627fe-427">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="627fe-428">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-428">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Выбор представления контента](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="627fe-430">Поиск в списке SharePoint</span><span class="sxs-lookup"><span data-stu-id="627fe-430">SharePoint List Search</span></span>

<span data-ttu-id="627fe-431">Совместная работа в Microsoft Teams часто ссылается на сведения, содержащиеся в элементов в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="627fe-431">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="627fe-432">Вклей ссылку на этот элемент заставляет всех переключать контекст из беседы, находить необходимые сведения, а затем возвращаться в Teams, чтобы продолжить беседу.</span><span class="sxs-lookup"><span data-stu-id="627fe-432">Paste a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="627fe-433">По мере того как беседа продолжается, люди должны несколько раз переключаться на справочный элемент, чтобы проверить новые комментарии и обновить воспоминания о сведениях, содержащихся в элементе.</span><span class="sxs-lookup"><span data-stu-id="627fe-433">As the conversation continues  people have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="627fe-434">Это переключение контекста создает барьер для плавного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="627fe-434">This context switching creates a barrier to smooth collaboration.</span></span>
<span data-ttu-id="627fe-435">Для решения этой проблемы используется шаблон приложения поиска списков.</span><span class="sxs-lookup"><span data-stu-id="627fe-435">To resolve this problem, the List Search app template is used.</span></span> <span data-ttu-id="627fe-436">Многие пользователи используют SharePoint для питания некоторых основных процессов в своих организациях.</span><span class="sxs-lookup"><span data-stu-id="627fe-436">Many users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="627fe-437">Однако совместная работа со списками затруднена.</span><span class="sxs-lookup"><span data-stu-id="627fe-437">However, collaborating around lists is difficult.</span></span> <span data-ttu-id="627fe-438">Используя шаблон приложения поиска списков в Microsoft Teams, пользователи могут вставлять сведения из элементов списка SharePoint непосредственно в чате, чтобы облегчить переключение контекста, вызванное при простом включении ссылки в чат.</span><span class="sxs-lookup"><span data-stu-id="627fe-438">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="627fe-439">Эти сведения вставляются в виде легко читаемой автоформатной карты, помогая пользователям оставаться в стороне от беседы.</span><span class="sxs-lookup"><span data-stu-id="627fe-439">The information is inserted as an easy-to-read auto-formatted card, helping the users stay engaged in the conversation.</span></span>

[<span data-ttu-id="627fe-440">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-440">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Приложение Поиска списка](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="627fe-442">Регистрация персонала</span><span class="sxs-lookup"><span data-stu-id="627fe-442">Staff Check-ins</span></span>

<span data-ttu-id="627fe-443">Регистрация сотрудников — это приложение на основе [power Apps,](/powerapps/powerapps-overview) которое позволяет контролировать связь между бизнесом и персоналом на местах.</span><span class="sxs-lookup"><span data-stu-id="627fe-443">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview) based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="627fe-444">Сотрудники могут легко предоставлять критически важные для времени сведения и обновления состояния непосредственно из Teams на запланированной или разной основе.</span><span class="sxs-lookup"><span data-stu-id="627fe-444">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="627fe-445">Приложение поддерживает расположение в режиме реального времени, фотографии, заметки, уведомления о напоминаниях и автоматизированные процессы работы.</span><span class="sxs-lookup"><span data-stu-id="627fe-445">The app supports real-time location, photos, notes, reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="627fe-446">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-446">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Создание представления регистрации](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="627fe-448">Опрос</span><span class="sxs-lookup"><span data-stu-id="627fe-448">Survey</span></span>

<span data-ttu-id="627fe-449">Survey — это настраиваемое приложение для расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которое позволяет создавать опрос в чате или канале для сбора данных и получения информации.</span><span class="sxs-lookup"><span data-stu-id="627fe-449">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span> <span data-ttu-id="627fe-450">Приложение поддерживается во всех клиентах платформы Teams, таких как настольный компьютер, браузер, iOS и Android, и готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="627fe-450">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="627fe-451">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-451">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Создание опроса в представлении Teams](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally"></a><span data-ttu-id="627fe-453">Время Tally</span><span class="sxs-lookup"><span data-stu-id="627fe-453">Time Tally</span></span> 

<span data-ttu-id="627fe-454">Проект может включать несколько задач, а сотрудникам могут быть назначены различные проекты.</span><span class="sxs-lookup"><span data-stu-id="627fe-454">A project can include multiple tasks, and various projects can be assigned to employees.</span></span> <span data-ttu-id="627fe-455">Руководители должны понимать ход выполнения проекта за время, затраченное сотрудниками на выполнение этих задач.</span><span class="sxs-lookup"><span data-stu-id="627fe-455">Managers are required to understand the project progress through the time spent by the employees on these tasks.</span></span> <span data-ttu-id="627fe-456">Это может быть громоздким действием, так как сотрудникам необходимо заполнить таблицы.</span><span class="sxs-lookup"><span data-stu-id="627fe-456">This can be a cumbersome activity, as the employees need to fill in the timesheets.</span></span> <span data-ttu-id="627fe-457">Приложение Time Tally позволяет сотрудникам быстро заполнять свои таблицы с помощью мобильного устройства, а руководителям не нужно следить за сотрудниками во время записи.</span><span class="sxs-lookup"><span data-stu-id="627fe-457">Time Tally app enables employees to fill their timesheets quickly, using the mobile device, and managers do not have to follow up with employees on the timesheet entry.</span></span> <span data-ttu-id="627fe-458">Руководители получают возможность просматривать использование проекта на основе ресурсов и могут утверждать или отклонить записи.</span><span class="sxs-lookup"><span data-stu-id="627fe-458">Managers get to view the project utilization based on resources, and they can approve or reject the entries.</span></span> <span data-ttu-id="627fe-459">Уведомления о напоминаниях отправляются для обеспечения соответствия времени.</span><span class="sxs-lookup"><span data-stu-id="627fe-459">Reminder notifications are sent to ensure timesheet compliance.</span></span> <span data-ttu-id="627fe-460">Кроме того, для аналитики доступны исторические данные и использование.</span><span class="sxs-lookup"><span data-stu-id="627fe-460">Also, historical data and utilizations are available for analytics.</span></span>

[<span data-ttu-id="627fe-461">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-461">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Время Tally](../assets/images/11zon_gif.gif)

## <a name="training--9734"></a><span data-ttu-id="627fe-463">Обучение &#9734;</span><span class="sxs-lookup"><span data-stu-id="627fe-463">Training  &#9734;</span></span>

<span data-ttu-id="627fe-464">Обучение — это настраиваемая программа расширения обмена сообщениями [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которая позволяет пользователям публиковать обучение в чате или канале для автономного обмена знаниями и upskilling.</span><span class="sxs-lookup"><span data-stu-id="627fe-464">Training is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables users to publish a training within a chat or a channel for offline knowledge sharing and upskilling.</span></span> <span data-ttu-id="627fe-465">Приложение поддерживается несколькими клиентами платформы Teams, такими как настольный компьютер, браузер, iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="627fe-465">The app is supported across multiple Teams platform clients, such as desktop, browser, iOS, and Android.</span></span> <span data-ttu-id="627fe-466">Это приложение готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="627fe-466">This app is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="627fe-467">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-467">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-training)

:::row:::
  :::column span="1":::
    ![Создание представления "Обучение в командах"](../assets/images/training-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="virtual-rounding"></a><span data-ttu-id="627fe-469">Виртуальное округление</span><span class="sxs-lookup"><span data-stu-id="627fe-469">Virtual Rounding</span></span>

<span data-ttu-id="627fe-470">Поставщики больничных и экстренных служб делают много **обходов** в день.</span><span class="sxs-lookup"><span data-stu-id="627fe-470">Hospital and emergency room providers make many **rounds** per day.</span></span> <span data-ttu-id="627fe-471">Эти быстрые проверки для пациентов предназначены для проверки состояния пациента и обеспечения решения проблем пациента.</span><span class="sxs-lookup"><span data-stu-id="627fe-471">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="627fe-472">Хотя округление является важной практикой для обеспечения контроля за пациентами несколькими типами поставщиков, они представляют собой огромную утечку на PPE, так как для каждого посещения, от каждого поставщика, новая маска и новый набор перчаток используются.</span><span class="sxs-lookup"><span data-stu-id="627fe-472">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves are used.</span></span> <span data-ttu-id="627fe-473">С помощью этих шаблонов приложений медицинские работники могут легко проводить обходы практически через собрание Microsoft Teams между поставщиком и пациентом.</span><span class="sxs-lookup"><span data-stu-id="627fe-473">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="627fe-474">Решение виртуального округлиния также ссылается в блоге Microsoft Health and Life [Sciences.](https://aka.ms/teamsvirtualrounding)</span><span class="sxs-lookup"><span data-stu-id="627fe-474">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="627fe-475">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-475">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Виртуальное округление](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="627fe-477">Управление посетителями</span><span class="sxs-lookup"><span data-stu-id="627fe-477">Visitor Management</span></span>

<span data-ttu-id="627fe-478">Приложение Управления посетителями позволяет вашей организации и сотрудникам легко и эффективно управлять процессом посетителей на месте непосредственно из Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="627fe-478">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="627fe-479">Приложение позволяет сотрудникам создавать запросы посетителей, централизованно отслеживать состояние запроса через панель мониторинга посетителей и получать уведомления в режиме реального времени при прибытии посетителя.</span><span class="sxs-lookup"><span data-stu-id="627fe-479">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="627fe-480">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-480">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

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

## <a name="workplace-awards"></a><span data-ttu-id="627fe-483">Награды на рабочем месте</span><span class="sxs-lookup"><span data-stu-id="627fe-483">Workplace Awards</span></span>

<span data-ttu-id="627fe-484">Workplace Awards — это шаблон приложений Teams, который обеспечивает положительные рамки, которые способствуют признанию и поощряют культуру оценки сотрудников на современном рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="627fe-484">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="627fe-485">Приложение позволяет настроить и управлять наградами и распознаванием сотрудников под названием R&R, где сотрудники могут легко назначать и поддерживать коллег, а лидер R&R может просматривать представленные номинации, гранты и объявлять получателей.</span><span class="sxs-lookup"><span data-stu-id="627fe-485">The app enables you to setup and manage an employee rewards and recognition, called R&R program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="627fe-486">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="627fe-486">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="627fe-487">Карточка номинации На рабочем месте</span><span class="sxs-lookup"><span data-stu-id="627fe-487">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Вкладка "Список наград на рабочем месте"](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="627fe-489">Дополнительные сведения о шаблоне приложений см. в [шаблоне App.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)</span><span class="sxs-lookup"><span data-stu-id="627fe-489">For more information on app template, see [App template](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>

## <a name="see-also"></a><span data-ttu-id="627fe-490">См. также</span><span class="sxs-lookup"><span data-stu-id="627fe-490">See also</span></span>

[<span data-ttu-id="627fe-491">Интеграция веб-приложений</span><span class="sxs-lookup"><span data-stu-id="627fe-491">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
