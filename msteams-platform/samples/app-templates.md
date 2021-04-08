---
title: Шаблоны приложений Microsoft Teams
description: Ссылки и описания шаблонов приложений для платформы Microsoft Teams
ms.topic: reference
keywords: Шаблоны Microsoft Teams примеры демонстрации
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 47fb1748f0c88edd2233c4e17aa50d235818d609
ms.sourcegitcommit: 2de062dd2258147cff8d6a3cadd8839890d9791a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2021
ms.locfileid: "51612646"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="97444-104">Шаблоны приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="97444-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="97444-105">Шаблоны приложений — это примеры полных приложений для Microsoft Teams с открытым исходным кодом и доступных в GitHub.</span><span class="sxs-lookup"><span data-stu-id="97444-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="97444-106">Каждый шаблон приложения содержит подробные инструкции по развертыванию и установке этого приложения для организации.</span><span class="sxs-lookup"><span data-stu-id="97444-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="97444-107">Он также предоставляет пример приложения, которое можно установить и начать использовать немедленно.</span><span class="sxs-lookup"><span data-stu-id="97444-107">It also provides a sample app that you can install and begin using immediately.</span></span> <span data-ttu-id="97444-108">Кроме того, доступен полный исходный код, который позволяет подробно изучить его или раздвоить код и изменить его, чтобы соответствовать определенным требованиям.</span><span class="sxs-lookup"><span data-stu-id="97444-108">The complete source code is available too, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="97444-109">Все шаблоны приложений предоставляются в соответствии с [условиями лицензии MIT.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)</span><span class="sxs-lookup"><span data-stu-id="97444-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>
> [!NOTE] 
> <span data-ttu-id="97444-110">Необходимо лицензировать и поддерживать приложения, созданные из шаблонов приложений для пользователей и организаций.</span><span class="sxs-lookup"><span data-stu-id="97444-110">You must license and support apps created from app templates for your users and organizations.</span></span> <span data-ttu-id="97444-111">Корпорация Майкрософт не несет ответственности за лицензии и поддержку.</span><span class="sxs-lookup"><span data-stu-id="97444-111">Microsoft is not responsible for licenses and support.</span></span>

<span data-ttu-id="97444-112">**&#9734; указывает только что выпущенные шаблоны приложений.**</span><span class="sxs-lookup"><span data-stu-id="97444-112">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="97444-113">Основные преимущества</span><span class="sxs-lookup"><span data-stu-id="97444-113">Key benefits</span></span>

* <span data-ttu-id="97444-114">**Развертывание непосредственно в облаке:** Все шаблоны приложений включают сценарии развертывания, которые позволяют развертывать все необходимые службы в Microsoft Azure или Power Platform.</span><span class="sxs-lookup"><span data-stu-id="97444-114">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="97444-115">**Рекомендуемый пример кода:** Шаблоны приложений соответствуют рекомендуемой рекомендации по безопасности и инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="97444-115">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="97444-116">Все внесенные сообществом изменения в шаблоны приложений проверяются для обеспечения соответствия.</span><span class="sxs-lookup"><span data-stu-id="97444-116">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="97444-117">**Настраиваемые и размязывные:** Несмотря на то, что все шаблоны приложений можно развернуть с минимальной конфигурацией, мы предоставляем всю базу кода и сценарии развертывания, чтобы вы могли легко настраивать или расширять их, чтобы соответствовать вашим уникальным потребностям.</span><span class="sxs-lookup"><span data-stu-id="97444-117">**Customizable and extensible:** While all app templates can be deployed with minimal configuration, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="97444-118">**Подробные документы:** Все шаблоны приложений сопровождаются документацией по архитектуре решений, развертыванию и этапам конфигурации.</span><span class="sxs-lookup"><span data-stu-id="97444-118">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot"></a><span data-ttu-id="97444-119">Бот по внедрению</span><span class="sxs-lookup"><span data-stu-id="97444-119">Adoption Bot</span></span> 

<span data-ttu-id="97444-120">Средство принятия — это чат-бот по уходу за пользователями, построенный с помощью power Virtual Agent for Teams (PVA).</span><span class="sxs-lookup"><span data-stu-id="97444-120">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams (PVA).</span></span> <span data-ttu-id="97444-121">Его можно считать PVA-версией FAQPlus.</span><span class="sxs-lookup"><span data-stu-id="97444-121">It can be considered as the PVA version of FAQPlus.</span></span> <span data-ttu-id="97444-122">Бот-принятия отвечает на 100+ распространенных вопросов о Microsoft 365 и Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-122">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="97444-123">Можно редактировать существующие темы, добавлять собственные темы и гнать существующие вопросы.</span><span class="sxs-lookup"><span data-stu-id="97444-123">You can edit the existing topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="97444-124">Если пользователям нужна дополнительная помощь, Бот-пользователь может подключить их к экспертам или даже расширить доступ к билетам на обслуживание с соединиттелями потока премиум-класса. Этот бот может быть установлен самостоятельно или встроен в настраиваемого приложения, например [концентратора принятия.](https://github.com/akporzondek/adoption_hub)</span><span class="sxs-lookup"><span data-stu-id="97444-124">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.This bot can be installed on it's own or built into a custom app like the [Adoption Hub](https://github.com/akporzondek/adoption_hub).</span></span>

[<span data-ttu-id="97444-125">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-125">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="adoption-tool--champion-management-platform-9734"></a><span data-ttu-id="97444-126">Платформа управления средствами принятия и &#9734;</span><span class="sxs-lookup"><span data-stu-id="97444-126">Adoption Tool- Champion Management Platform &#9734;</span></span>

<span data-ttu-id="97444-127">Шаблон приложения Платформы управления чемпионами (CMP) помогает управлять, масштабировать и вдохновлять чемпионов командной работы, чтобы добиться большего.</span><span class="sxs-lookup"><span data-stu-id="97444-127">The Champion Management Platform (CMP) app template helps you manage, scale, and inspire your teamwork champions to achieve more.</span></span> <span data-ttu-id="97444-128">Этот шаблон приложения построен на SharePoint Framework и загружается на вкладку в команде.</span><span class="sxs-lookup"><span data-stu-id="97444-128">This app template is built on the SharePoint Framework and loaded into a tab within a team.</span></span> <span data-ttu-id="97444-129">Группы могут использовать этот инструмент для управления членством в программе, предоставления лидеров и типов событий для ведения журнала, а также инструментов для наложения цифровых значков для участников программы.</span><span class="sxs-lookup"><span data-stu-id="97444-129">Groups can leverage this tool to help manage program membership, provide a leaderboard and event types for logging, and tools to overlay digital badges to program participants.</span></span>

[<span data-ttu-id="97444-130">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-130">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started-9734"></a><span data-ttu-id="97444-131">Средство принятия — пути обучения Microsoft 365 (Начало работы) &#9734;</span><span class="sxs-lookup"><span data-stu-id="97444-131">Adoption Tool- Microsoft 365 Learning Pathways (Get Started) &#9734;</span></span>

<span data-ttu-id="97444-132">Шаблон приложения Get Started позволяет использовать в microsoft 365 обучающие пути в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-132">The Get Started app template allows you to bring the power of Microsoft 365 learning pathways inside of Microsoft Teams.</span></span> <span data-ttu-id="97444-133">Этот шаблон приложения позволяет легко получить доступ к определенным страницам обучения или другим интрасетям и загрузить содержимое непосредственно в Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-133">This app template allows you to grant easy access to specific training pages or other intranet assets and load the content directly within Teams.</span></span> <span data-ttu-id="97444-134">Вы также можете изменить имя или логотип приложения, чтобы соответствовать брендингу вашей компании.</span><span class="sxs-lookup"><span data-stu-id="97444-134">You can also change the app name or logo to match your company branding.</span></span>

[<span data-ttu-id="97444-135">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-135">Get it on GitHub</span></span>](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="appointment-manager"></a><span data-ttu-id="97444-136">Менеджер по встречам</span><span class="sxs-lookup"><span data-stu-id="97444-136">Appointment Manager</span></span> 

<span data-ttu-id="97444-137">Диспетчер назначений — это шаблон приложений Teams, который помогает предприятиям создавать, управлять и проводить виртуальные встречи с потребителями через Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-137">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="97444-138">Новые запросы на прием от потребителей видны в каналах Teams, где их можно быстро назначить и переназначить сотрудникам в команде.</span><span class="sxs-lookup"><span data-stu-id="97444-138">New appointment requests from consumers are visible in Teams channels, where they can quickly be assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="97444-139">Запросы на встречу можно просматривать на командном или личном уровнях с помощью настраиваемой вкладки.</span><span class="sxs-lookup"><span data-stu-id="97444-139">Appointment requests can be viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="97444-140">Каждая встреча связана с онлайн-собранием Teams, поэтому сотрудники и потребители могут легко присоединиться к собранию в запланированное время.</span><span class="sxs-lookup"><span data-stu-id="97444-140">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="97444-141">Шаблон приложения интегрируется с Microsoft Bookings для простого управления назначением.</span><span class="sxs-lookup"><span data-stu-id="97444-141">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="97444-142">Запланированные встречи автоматически отображаются в календарях назначенного персонала, а потребители получают настраиваемые уведомления электронной почты и напоминания со встроенными ссылками на собрания.</span><span class="sxs-lookup"><span data-stu-id="97444-142">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="97444-143">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-143">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="97444-144">![Менеджер по обзору ](../assets/images/appointment-manager-overview.png)
 ![ назначений диспетчера назначений в teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="97444-144">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="97444-145">Ask Away</span><span class="sxs-lookup"><span data-stu-id="97444-145">Ask Away</span></span>

<span data-ttu-id="97444-146">Ask Away — это [бот Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям проводить сеансы Q&(вопросы и ответы) в Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-146">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Q&A (Question and Answer) sessions within Teams.</span></span> <span data-ttu-id="97444-147">С помощью бота Ask Away участники группы могут отправлять и задавать вопросы до голосования, общие коллегами, что позволяет Q&A-хостов для легкого сбора вопросов в канале или чате.</span><span class="sxs-lookup"><span data-stu-id="97444-147">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="97444-148">Бот может использоваться для проведения сеанса Q&в режиме реального времени на собрании Teams и позволяет участникам отправлять вопросы в режиме реального времени в чате.</span><span class="sxs-lookup"><span data-stu-id="97444-148">The bot can be used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live via chat.</span></span>

[<span data-ttu-id="97444-149">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-149">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Просмотр всплывающее окно в таблице лидеров для голосования пользователей по вопросам](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="97444-151">Вспомогательная аналитика</span><span class="sxs-lookup"><span data-stu-id="97444-151">Associate Insights</span></span>

<span data-ttu-id="97444-152">Associate Insights — это шаблон [Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) который позволяет сотрудникам firstline напрямую фиксировать и отправлять мнения клиентов, настроения и восприятие.</span><span class="sxs-lookup"><span data-stu-id="97444-152">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="97444-153">Работники Firstline часто являются первым представителем компании, который может взаимодействовать с клиентами в контактной точке один к одному.</span><span class="sxs-lookup"><span data-stu-id="97444-153">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="97444-154">Собранные данные можно совместно использовать бизнес-группами, например, с помощью вкладки Power BI Teams для улучшения продукта и улучшения работы с клиентами.</span><span class="sxs-lookup"><span data-stu-id="97444-154">The collected data can be shared and used collaboratively by business teams, e.g., via a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="97444-155">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-155">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

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

## <a name="attendance"></a><span data-ttu-id="97444-158">Присутствие</span><span class="sxs-lookup"><span data-stu-id="97444-158">Attendance</span></span>

<span data-ttu-id="97444-159">Приложение Для участия — это [вкладка Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) которую можно закрепить в команде.</span><span class="sxs-lookup"><span data-stu-id="97444-159">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that can be pinned in a team.</span></span> <span data-ttu-id="97444-160">Он предназначен для записи присутствия, как правило, в таких параметрах, как среда обучения и обучения.</span><span class="sxs-lookup"><span data-stu-id="97444-160">It is designed to record presence, typically in settings such as learning and training environments.</span></span> <span data-ttu-id="97444-161">Пользователи могут отмечать или изменять посещаемость в течение до 30 дней в прошлом и просматривать обобщенные отчеты о посещаемости для всей группы или отдельных участников.</span><span class="sxs-lookup"><span data-stu-id="97444-161">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span>

[<span data-ttu-id="97444-162">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-162">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![Демонстрация приложения для посещаемости](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="97444-164">Book-a-room</span><span class="sxs-lookup"><span data-stu-id="97444-164">Book-a-room</span></span>

<span data-ttu-id="97444-165">Book-a-room — это бот [Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям быстро находить и резервировать зал собраний в течение 30 (по умолчанию), 60 или 90 минут начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="97444-165">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="97444-166">Область бота Book-a-room для личных или 1:1 бесед.</span><span class="sxs-lookup"><span data-stu-id="97444-166">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

[<span data-ttu-id="97444-167">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-167">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![Демонстрация book-a-room](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="97444-169">Доступ к зданиям</span><span class="sxs-lookup"><span data-stu-id="97444-169">Building Access</span></span>

<span data-ttu-id="97444-170">Building Access — это приложение, основанное на платформе Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)которое поддерживает администрирование пороговых значений заполняемости зданий и норм социального расстановки, позволяя директорам объектов управлять, отслеживать и сообщать о присутствии сотрудников на месте.</span><span class="sxs-lookup"><span data-stu-id="97444-170">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="97444-171">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview)и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams и позволяет организациям определять готовность к созданию, устанавливать критерии приемлемости для доступа на месте и собирать сведения для планирования в будущем.</span><span class="sxs-lookup"><span data-stu-id="97444-171">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="97444-172">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-172">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Карта резервирования доступа к зданию](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Представление ключа "Создание доступа"](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="97444-175">Праздники</span><span class="sxs-lookup"><span data-stu-id="97444-175">Celebrations</span></span>

<span data-ttu-id="97444-176">Celebrations — это приложение Teams, которое помогает участникам группы отмечать дни рождения, юбилеи и другие повторяющиеся события.</span><span class="sxs-lookup"><span data-stu-id="97444-176">Celebrations is a Teams app that helps team members celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="97444-177">Он запоминает особые случаи всех членов команды и отправляет приветственное сообщение во всех командах, выбранных во время создания событий, чтобы участники группы чувствовали себя особенными в свой день.</span><span class="sxs-lookup"><span data-stu-id="97444-177">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="97444-178">Приложение предоставляет простой интерфейс для всех членов группы, чтобы лично добавить и просмотреть свои события, а также позволяет пользователю выбрать команды, в которых события получают общий доступ.</span><span class="sxs-lookup"><span data-stu-id="97444-178">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="97444-179">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-179">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="97444-180">Контрольный список</span><span class="sxs-lookup"><span data-stu-id="97444-180">Checklist</span></span>

<span data-ttu-id="97444-181">Контрольный список — это настраиваемая программа расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которая позволяет вам сотрудничать со своей командой, создавая общий контрольный список в чате или канале.</span><span class="sxs-lookup"><span data-stu-id="97444-181">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="97444-182">Приложение поддерживается во всех клиентах платформы Teams — настольных компьютерах, браузерах, iOS и Android — и готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="97444-182">The app is supported across all Teams platform clients —  desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="97444-183">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-183">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![Создание контрольного списка в представлении Teams](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in"></a><span data-ttu-id="97444-185">Заехав в класс</span><span class="sxs-lookup"><span data-stu-id="97444-185">Classroom Drop-in</span></span> 

<span data-ttu-id="97444-186">В классе drop-in — это приложение на основе платформы Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)которое позволяет руководителям систем находить группы классов (виртуальные классы) и добавлять себя или других в эти группы класса в течение указанного периода при необходимости.</span><span class="sxs-lookup"><span data-stu-id="97444-186">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams (virtual classrooms) and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="97444-187">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview) и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams, чтобы убедиться, что учебные заведения могут оптимизировать свои операции в гибридной среде обучения, предоставляя доступ к соответствующим заинтересованным сторонам для групп классов по бизнес-требованиям.</span><span class="sxs-lookup"><span data-stu-id="97444-187">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="97444-188">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-188">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Запрос на отсев класса](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="97444-190">Корпоративный Communicator</span><span class="sxs-lookup"><span data-stu-id="97444-190">Company Communicator</span></span>

<span data-ttu-id="97444-191">Приложение Communicator позволяет корпоративным группам создавать и отправлять сообщения, предназначенные для нескольких групп или большого числа сотрудников в чате, позволяя организации достигать сотрудников прямо там, где они сотрудничают.</span><span class="sxs-lookup"><span data-stu-id="97444-191">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="97444-192">Используйте этот шаблон для нескольких сценариев, таких как новые объявления об инициативе, учет сотрудников, современное обучение и разработка или широкомасштабные трансляции.</span><span class="sxs-lookup"><span data-stu-id="97444-192">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="97444-193">Приложение обеспечивает простой интерфейс для назначенных пользователей для создания, предварительного просмотра, совместной работы и отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="97444-193">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="97444-194">Он создает основу для создания настраиваемой целевой системы связи, например настраиваемой телеметрии, о том, сколько пользователей было признано или взаимодействует с сообщением.</span><span class="sxs-lookup"><span data-stu-id="97444-194">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="97444-195">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-195">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator составить представление окна](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="97444-197">Lookup контактной группы</span><span class="sxs-lookup"><span data-stu-id="97444-197">Contact Group Lookup</span></span>

<span data-ttu-id="97444-198">Приложение Lookup контактной группы предоставляет удобный и полезный подход к созданию, доступу и управлению контактной группой организации (ранее известной как списки рассылки или группы связи).</span><span class="sxs-lookup"><span data-stu-id="97444-198">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups (formerly known as distribution lists or communication groups).</span></span> <span data-ttu-id="97444-199">Пользователи могут быстро просматривать и общаться с участниками группы, просматривать состояние участников и создавать групповой чат с выбранными участниками контактной группы, все в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-199">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="97444-200">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-200">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

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

## <a name="co-worker-appreciation"></a><span data-ttu-id="97444-203">Оценка сотрудников</span><span class="sxs-lookup"><span data-stu-id="97444-203">Co-worker Appreciation</span></span> 

<span data-ttu-id="97444-204">Используя шаблон оценки сотрудников в Microsoft Teams, пользователи могут распознавать достижения своих коллег в контексте Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-204">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="97444-205">Когда сотрудники выбирают для вознаграждения коллегу, получатели и другие члены группы помечены в разговоре на канале, и они получают уведомление о вручениях канала.</span><span class="sxs-lookup"><span data-stu-id="97444-205">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="97444-206">Награды записывают в приложении Teams, которое является безопасным, переносным и легкодоступным.</span><span class="sxs-lookup"><span data-stu-id="97444-206">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="97444-207">Это можно считать версией приложения Open Badges, основанной на PowerApps, с таблицей лидеров.</span><span class="sxs-lookup"><span data-stu-id="97444-207">This can be considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="97444-208">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-208">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![В целом](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="97444-210">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="97444-210">CrowdSourcer</span></span>

<span data-ttu-id="97444-211">CrowdSourcer — это [бот Microsoft Teams,](../bots/what-are-bots.md) который предоставляет группам запрашиваемую информацию, которую совместно запрашивают члены группы.</span><span class="sxs-lookup"><span data-stu-id="97444-211">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="97444-212">Это отличный способ ответить на часто задамые вопросы, позволяя участникам активно участвовать и вносить вклад в интересный и полезный информационный ресурс.</span><span class="sxs-lookup"><span data-stu-id="97444-212">It's a great way to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="97444-213">Get it on Github</span><span class="sxs-lookup"><span data-stu-id="97444-213">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Взаимодействие с конечным пользователем crowdsource](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="97444-215">Пользовательские наклейки</span><span class="sxs-lookup"><span data-stu-id="97444-215">Custom Stickers</span></span>

<span data-ttu-id="97444-216">Самовыражение является основой здоровой культуры команды.</span><span class="sxs-lookup"><span data-stu-id="97444-216">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="97444-217">Этот шаблон приложения — это расширение [обмена](~/messaging-extensions/what-are-messaging-extensions.md) сообщениями, которое позволяет пользователям использовать настраиваемые наклейки и GIF-решения в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-217">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="97444-218">Этот шаблон предоставляет простой веб-опыт настройки, где любой пользователь с доступом к конфигурации может загружать GIF-ы/наклейки/изображения, которые должны иметь конечные пользователи, что позволяет всей вашей команде использовать любой набор стикеров, которые вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="97444-218">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs/stickers/images they want their end-users to have, allowing your entire team to use any set of stickers you chose.</span></span>

<span data-ttu-id="97444-219">Это приложение также позволяет легко обмениваться изображениями/GIF-файлами/наклейками между группами без доступа к сайтам SharePoint или отдельным каналам в качестве механизмов хранения и общего доступа.</span><span class="sxs-lookup"><span data-stu-id="97444-219">This app also enables easy sharing of images/GIFs/stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="97444-220">Например, группы продуктов могут легко обмениваться изображениями продуктов и GIF-изображениями с группами социальных сетей, маркетинга и продаж программным образом.</span><span class="sxs-lookup"><span data-stu-id="97444-220">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="97444-221">Можно также расширить это приложение, запуская поток уведомлений для определенных групп/отдельных лиц, когда будут доступны новые изображения/GIF-изображения.</span><span class="sxs-lookup"><span data-stu-id="97444-221">One can also extend this app by triggering a notification flow to specific teams/individuals when new images/GIFs are made available.</span></span>

[<span data-ttu-id="97444-222">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-222">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Приложение Стикеры](../assets/images/stickers.png)

## <a name="employee-ideas"></a><span data-ttu-id="97444-224">Идеи сотрудников</span><span class="sxs-lookup"><span data-stu-id="97444-224">Employee Ideas</span></span>

<span data-ttu-id="97444-225">Приложение "Идеи сотрудников" — это версия PowerApps шаблона приложения Great Ideas на основе Azure.</span><span class="sxs-lookup"><span data-stu-id="97444-225">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="97444-226">Приложение позволяет пользователям Teams настраивать и настраивать кампанию идей.</span><span class="sxs-lookup"><span data-stu-id="97444-226">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="97444-227">Кампания идей — это категория для группировки идей вокруг общих тем.</span><span class="sxs-lookup"><span data-stu-id="97444-227">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="97444-228">Пользователи teams также могут выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="97444-228">Teams users can also perform following activities:</span></span>
* <span data-ttu-id="97444-229">Настройте стандартную форму отправки, которую сотрудники должны отправить для каждой идеи.</span><span class="sxs-lookup"><span data-stu-id="97444-229">Configure a standard submission form that employees need to submit for each idea.</span></span> 
* <span data-ttu-id="97444-230">Просмотрите и управляйте идеями и списком кампаний.</span><span class="sxs-lookup"><span data-stu-id="97444-230">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="97444-231">Изменение и удаление кампаний.</span><span class="sxs-lookup"><span data-stu-id="97444-231">Modify and delete campaigns.</span></span>
* <span data-ttu-id="97444-232">Просмотрите советы лидеров идей.</span><span class="sxs-lookup"><span data-stu-id="97444-232">Review leader boards of ideas.</span></span>
* <span data-ttu-id="97444-233">Голосуйте за и делитесь приоритетными идеями.</span><span class="sxs-lookup"><span data-stu-id="97444-233">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="97444-234">Отправка идей для кампании.</span><span class="sxs-lookup"><span data-stu-id="97444-234">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="97444-235">Просмотр идеи другого члена группы.</span><span class="sxs-lookup"><span data-stu-id="97444-235">View other team member's idea.</span></span>
* <span data-ttu-id="97444-236">Голосуйте за наиболее понравились идеи.</span><span class="sxs-lookup"><span data-stu-id="97444-236">Vote on most liked ideas.</span></span>
* <span data-ttu-id="97444-237">Просмотрите производительность их идей по сравнению с другими в рамках кампании.</span><span class="sxs-lookup"><span data-stu-id="97444-237">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="97444-238">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-238">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Управление представлением кампании](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="97444-240">Электронные рецепты</span><span class="sxs-lookup"><span data-stu-id="97444-240">E-Prescriptions</span></span> 

<span data-ttu-id="97444-241">E-Prescriptions — это приложение на основе power [Apps,](/powerapps/maker/canvas-apps/embed-teams-app)которое улучшает телемедицину и виртуальную помощь путем автоматизации процесса выдачи электронных рецептов пациентам.</span><span class="sxs-lookup"><span data-stu-id="97444-241">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)-based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="97444-242">Медицинские специалисты могут быстро пересматривать встречи, создавать электронные рецепты и отправлять электронные письма с вложениями по электронному рецепту пациентам непосредственно на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-242">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="97444-243">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-243">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

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

## <a name="employee-training"></a><span data-ttu-id="97444-248">Обучение сотрудников</span><span class="sxs-lookup"><span data-stu-id="97444-248">Employee Training</span></span> 

<span data-ttu-id="97444-249">Обучение сотрудников — это приложение Microsoft Teams, которое позволяет организаторам легко публиковать, отслеживать и содействовать обучению и учебным мероприятиям для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="97444-249">Employee training is a Microsoft Teams app that enables organizers to easily publish,  track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="97444-250">С помощью приложения организаторы событий могут отправлять напоминания и уведомления регистраторам событий, а сотрудники могут указывать на интерес к предстоящим событиям, обновлять текущие события и делиться сведениями о событиях с коллегами через расширение обмена сообщениями Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-250">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues via the Teams messaging extension.</span></span>

[<span data-ttu-id="97444-251">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-251">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="97444-252">**Просмотр событий обучения сотрудников** ![ Изображение вкладки подготовки сотрудников](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="97444-252">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="97444-253">**Создание события подготовки сотрудников** ![ Обучение сотрудников создает форму событий](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="97444-253">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="97444-254">Эксперт finder</span><span class="sxs-lookup"><span data-stu-id="97444-254">Expert Finder</span></span>

<span data-ttu-id="97444-255">Expert Finder — это [бот Microsoft Teams,](../bots/what-are-bots.md) который определяет конкретных членов организации на основе их навыков, интересов и атрибутов образования.</span><span class="sxs-lookup"><span data-stu-id="97444-255">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="97444-256">Участники находят экспертов в организации, которые соответствуют поиску ключевых слов профилей пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="97444-256">Members find experts within an organization  that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="97444-257">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-257">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Демонстрация результатов поиска expert Finder](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="97444-259">Вопросы и ответы плюс</span><span class="sxs-lookup"><span data-stu-id="97444-259">FAQ Plus</span></span>

<span data-ttu-id="97444-260">Диалоговая&боты — это простой способ предоставления ответов на часто задамые пользователями вопросы.</span><span class="sxs-lookup"><span data-stu-id="97444-260">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="97444-261">Однако большинство ботов не могут эффективно взаимодействовать с пользователями, так как при сбойе бота в цикле нет человека.</span><span class="sxs-lookup"><span data-stu-id="97444-261">However, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="97444-262">FaQ bot — это дружественный Q&бот, который приводит человека в цикл, когда он не в состоянии помочь.</span><span class="sxs-lookup"><span data-stu-id="97444-262">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="97444-263">Можно задать боту вопрос, и бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="97444-263">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="97444-264">Если нет, бот позволяет пользователю отправлять запрос, который затем передается предварительно настроенной группе экспертов, которые помогают обеспечить поддержку, действуя на уведомления из самой группы.</span><span class="sxs-lookup"><span data-stu-id="97444-264">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="97444-265">Последний выпуск **FAQ Plus** поддерживает улучшенные решения Q&, позволяя группе экспертов выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="97444-265">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="97444-266">&#x2714; Q&как непосредственно в базу знаний с помощью расширений сообщений.</span><span class="sxs-lookup"><span data-stu-id="97444-266">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="97444-267">&#x2714; изменить и удалить Q&пары, добавленные ботом.</span><span class="sxs-lookup"><span data-stu-id="97444-267">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="97444-268">&#x2714; отслеживание истории пересмотра Q&As.</span><span class="sxs-lookup"><span data-stu-id="97444-268">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="97444-269">&#x2714; настройка ответа с дополнительными сведениями для отображения в качестве [адаптивной карты.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="97444-269">&#x2714; Configure an answer with additional details to display as an [adaptive card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="97444-270">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-270">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Gif FAQ Plus](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app"></a><span data-ttu-id="97444-272">Получить приложение поддержки</span><span class="sxs-lookup"><span data-stu-id="97444-272">Get Support App</span></span>

<span data-ttu-id="97444-273">Приложение Get Support можно использовать организациями, использующими Microsoft Teams, чтобы позволить любому набору пользователей запрашивать помощь у руководителей.</span><span class="sxs-lookup"><span data-stu-id="97444-273">The Get Support app can be used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="97444-274">Это приложение включает в себя различные функции, такие как:</span><span class="sxs-lookup"><span data-stu-id="97444-274">This app includes various features, such as:</span></span>
-   <span data-ttu-id="97444-275">Запрос помощи для разных категорий в приложении Power</span><span class="sxs-lookup"><span data-stu-id="97444-275">Requesting assistance on different categories from a Power App</span></span>
-   <span data-ttu-id="97444-276">Уведомления, отправленные запросчикам, информирующие их о том, кому назначено</span><span class="sxs-lookup"><span data-stu-id="97444-276">Notifications sent to requestors informing them of who has been assigned</span></span> 
-   <span data-ttu-id="97444-277">Уведомления, отправленные назначенному руководителю, информирующие их о том, кому нужна помощь</span><span class="sxs-lookup"><span data-stu-id="97444-277">Notifications sent to assigned supervisors informing them of who needs assistance</span></span> 
-   <span data-ttu-id="97444-278">Анализ эскалаций и шаблонов в SharePoint и PowerBI</span><span class="sxs-lookup"><span data-stu-id="97444-278">Analyzing escalations and patterns in SharePoint and PowerBI</span></span>

[<span data-ttu-id="97444-279">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-279">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Get Support Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="97444-281">Отслеживание целей</span><span class="sxs-lookup"><span data-stu-id="97444-281">Goal Tracker</span></span>

<span data-ttu-id="97444-282">Приложение Goal Tracker — это комплексное решение для организации, которое поддерживает установление целей, наблюдение за прогрессом и признание успеха в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-282">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="97444-283">Приложение позволяет пользователям устанавливать, отслеживать и обновлять цели на профессиональном, личном и командном уровне.</span><span class="sxs-lookup"><span data-stu-id="97444-283">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="97444-284">Члены группы также получают вовремя напоминания и обновления состояния, чтобы оставаться сосредоточенными и оставаться в курсе.</span><span class="sxs-lookup"><span data-stu-id="97444-284">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="97444-285">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-285">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

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

## <a name="great-ideas"></a><span data-ttu-id="97444-288">Великие идеи</span><span class="sxs-lookup"><span data-stu-id="97444-288">Great Ideas</span></span>

<span data-ttu-id="97444-289">Приложение Great Ideas поддерживает и расширяет возможности инноваций и творчества в организации.</span><span class="sxs-lookup"><span data-stu-id="97444-289">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="97444-290">Приложение позволяет сотрудникам обмениваться идеями с коллегами и руководством, открывать новые материалы, делать акценты на одноранговом рассмотрении и голосовать за лучшие предложения в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-290">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="97444-291">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-291">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a><span data-ttu-id="97444-294">Групповые действия</span><span class="sxs-lookup"><span data-stu-id="97444-294">Group Activities</span></span>

<span data-ttu-id="97444-295">Групповые действия — это приложение Microsoft Teams, которое позволяет владельцам групп быстро создавать группы действий и управлять рабочими процессами совместной работы в контексте Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-295">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="97444-296">Авторы действий могут создавать действия, случайным образом распределять членов группы по группам и необязательно отправлять напоминания боту до завершения действий.</span><span class="sxs-lookup"><span data-stu-id="97444-296">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="97444-297">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-297">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

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

## <a name="grow-your-skills"></a><span data-ttu-id="97444-300">Вырастите свои навыки</span><span class="sxs-lookup"><span data-stu-id="97444-300">Grow Your Skills</span></span>

<span data-ttu-id="97444-301">Приложение Grow Your Skills поддерживает профессиональный рост и развитие, позволяя сотрудникам вносить вклад в дополнительные проекты для вашей организации, одновременно изучая новые навыки.</span><span class="sxs-lookup"><span data-stu-id="97444-301">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="97444-302">Сотрудники могут использовать приложение для поиска возможностей, которые отвечают их интересам, эффективного взаимодействия с коллегами и получения новых уровней знаний и возможностей, все в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-302">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="97444-303">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-303">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

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

## <a name="hr-support"></a><span data-ttu-id="97444-306">Поддержка управления персоналом</span><span class="sxs-lookup"><span data-stu-id="97444-306">HR Support</span></span>

<span data-ttu-id="97444-307">Бот поддержки кадров — это дружественный Q&бот, который привозит профессионала поддержки или эксперта из группы hr в цикл, когда он не в состоянии помочь.</span><span class="sxs-lookup"><span data-stu-id="97444-307">HR Support bot is a friendly Q&A bot that brings a support professional/expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="97444-308">Можно задать боту вопрос, и бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="97444-308">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="97444-309">Если нет, бот позволяет пользователю отправить запрос, который затем будет размещен в предварительно настроенной группе экспертов, которые помогают оказывать поддержку, действуя на уведомления из самой команды.</span><span class="sxs-lookup"><span data-stu-id="97444-309">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="97444-310">Кроме того, бот предлагает ссылки на рекомендуемые политики и вопросы по персоналу, ища предварительно настроенные теги в этом вопросе.</span><span class="sxs-lookup"><span data-stu-id="97444-310">Additionally, the bot suggests links to recommended HR policies/questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="97444-311">Эти плитки также можно найти на связанной вкладке в качестве быстрой ссылки.</span><span class="sxs-lookup"><span data-stu-id="97444-311">These tiles can also be found in the associated tab as a quick reference.</span></span> <span data-ttu-id="97444-312">Поддержка кадров хорошо работает для легкого веса QnA и обеспечивает быструю поддержку при запуске новых проектов и инициатив в организации.</span><span class="sxs-lookup"><span data-stu-id="97444-312">HR Support works well for light weight QnA and to provide quick support when launching new projects/initiatives in the organization.</span></span>

[<span data-ttu-id="97444-313">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-313">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Поддержка управления персоналом](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="97444-315">Точки соприкосновения</span><span class="sxs-lookup"><span data-stu-id="97444-315">Icebreaker</span></span>

<span data-ttu-id="97444-316">Icebreaker — это [бот Microsoft Teams,](../bots/what-are-bots.md) который помогает вашей команде приблизиться, спарив двух случайных членов команды каждую неделю для встречи.</span><span class="sxs-lookup"><span data-stu-id="97444-316">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="97444-317">Бот упрощает планирование, автоматически предлагая свободное время, которое работает для обоих участников.</span><span class="sxs-lookup"><span data-stu-id="97444-317">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="97444-318">Укрепляйте личные связи и создайте тесное сообщество с помощью этого приложения.</span><span class="sxs-lookup"><span data-stu-id="97444-318">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="97444-319">Помимо поощрения личных подключений всей вашей команды, приложение Icebreaker может помочь развивать сообщества, основанные на интересах вашей организации.</span><span class="sxs-lookup"><span data-stu-id="97444-319">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="97444-320">Например, это приложение можно использовать для группы по интересам DevOps, чтобы помочь идеям и лучшим практикам органично распространяться по всей организации.</span><span class="sxs-lookup"><span data-stu-id="97444-320">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="97444-321">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-321">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Приложение Icebreaker](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="97444-323">Стимулы</span><span class="sxs-lookup"><span data-stu-id="97444-323">Incentives</span></span>

<span data-ttu-id="97444-324">Стимулы — это шаблон [Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) который управляет и отслеживает стимулирование участия сотрудников в назначенных мероприятиях, таких как тренинги и инициативы по управлению изменениями.</span><span class="sxs-lookup"><span data-stu-id="97444-324">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities such as trainings and change management initiatives.</span></span> <span data-ttu-id="97444-325">Администраторы используют приложение для создания назначенных действий, назначения точек для завершения и указания необходимых уровней точки права на вознаграждение.</span><span class="sxs-lookup"><span data-stu-id="97444-325">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="97444-326">Сотрудники используют приложение для просмотра накопленных баллов и по достижении допустимости запрашивать и требовать выкупаемых вознаграждений.</span><span class="sxs-lookup"><span data-stu-id="97444-326">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="97444-327">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-327">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Демонстрация приложения incentives](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="97444-329">Репортер инцидентов</span><span class="sxs-lookup"><span data-stu-id="97444-329">Incident Reporter</span></span>

<span data-ttu-id="97444-330">Incident Reporter — это [бот Microsoft Teams,](../bots/what-are-bots.md)  который оптимизирует управление инцидентами в организации.</span><span class="sxs-lookup"><span data-stu-id="97444-330">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="97444-331">Бот упрощает автоматизированный сбор данных об инцидентах, настраиваемые отчеты об инцидентах, соответствующие уведомления заинтересованных лиц и отслеживание инцидентов в конце концов.</span><span class="sxs-lookup"><span data-stu-id="97444-331">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="97444-332">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-332">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

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

## <a name="inspection"></a><span data-ttu-id="97444-335">Проверка</span><span class="sxs-lookup"><span data-stu-id="97444-335">Inspection</span></span> 

 <span data-ttu-id="97444-336">Inspection — это приложение Microsoft Teams, которое позволяет сотрудникам передней линии проверять все, что угодно от расположения до активов и оборудования.</span><span class="sxs-lookup"><span data-stu-id="97444-336">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="97444-337">Например, розничный магазин, завод по производству или транспортные средства и машины.</span><span class="sxs-lookup"><span data-stu-id="97444-337">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="97444-338">В этом решении есть два приложения, каждое из которых предназначено для разных типов пользователей.</span><span class="sxs-lookup"><span data-stu-id="97444-338">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="97444-339">Приложение предоставляет сотрудникам передней линии возможность проверять актив или область, управлять качеством продуктов и услуг или поддерживать безопасность на рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="97444-339">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="97444-340">Это облегчает связь между членами группы для решения проблем, найденных во время проверки.</span><span class="sxs-lookup"><span data-stu-id="97444-340">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="97444-341">Приложение предоставляет простые отчеты для руководителей, чтобы ускорить решение проблем и выделить тенденции.</span><span class="sxs-lookup"><span data-stu-id="97444-341">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="97444-342">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-342">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Обзор инспекции](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a><span data-ttu-id="97444-344">Отчеты о проблемах</span><span class="sxs-lookup"><span data-stu-id="97444-344">Issue Reporting</span></span>

<span data-ttu-id="97444-345">Приложение Отчеты о проблемах позволяет сотрудникам и руководителям поднимать и управлять вопросами.</span><span class="sxs-lookup"><span data-stu-id="97444-345">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="97444-346">Она состоит из двух приложений: приложения для отчетов о проблемах и приложения "Управление вопросами" для управления вопросами.</span><span class="sxs-lookup"><span data-stu-id="97444-346">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="97444-347">Руководители групп используют приложение Manage Issues для настройки приложения, в том числе канала, в котором приложения создают сообщения Microsoft Teams и задачи планировщика.</span><span class="sxs-lookup"><span data-stu-id="97444-347">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="97444-348">Менеджеры также используют приложение для создания форм шаблонов для сбора сведений, когда пользователь сообщает о проблеме.</span><span class="sxs-lookup"><span data-stu-id="97444-348">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="97444-349">Например, просмотрите, отредактируете или удалите формы шаблона проблем.</span><span class="sxs-lookup"><span data-stu-id="97444-349">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="97444-350">Приложение также можно использовать для рассмотрения проблем группы, отчета об истории проблем и эффективного управления решением проблем.</span><span class="sxs-lookup"><span data-stu-id="97444-350">The app can also be used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="97444-351">Сотрудники используют приложение отчетов о проблемах для журналов проблем и сведений, необходимых для их устранения.</span><span class="sxs-lookup"><span data-stu-id="97444-351">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="97444-352">Приложение также используется для изменения и решения существующих проблем и получения высокого уровня представления об отдельных или командных проблемах.</span><span class="sxs-lookup"><span data-stu-id="97444-352">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="97444-353">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Представление группы отчетов о проблемах](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="97444-355">Новые возможности для сотрудников</span><span class="sxs-lookup"><span data-stu-id="97444-355">New Employee Onboarding</span></span> 

<span data-ttu-id="97444-356">Новая интеграция сотрудников — это интегрированное решение microsoft Teams и [SharePoint New Employee Onboarding,](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) которое позволяет организации предоставлять сотрудникам в пути по новому найму согласованный и высококачественный опыт работы с бортовой командой.</span><span class="sxs-lookup"><span data-stu-id="97444-356">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="97444-357">Приложение может быть использовано группами кадров и менеджерами по найму для предоставления соответствующих сведений в процессе ориентации и индукции, а также для обмена отзывами, предоставления вводных данных и выполнения задач бортового ввода.</span><span class="sxs-lookup"><span data-stu-id="97444-357">The app can be used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="97444-358">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-358">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="97444-359">**Новая приветствие сотрудника** ![ Изображение новой приветствия сотрудника](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="97444-359">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="97444-360">**Новый контрольный список сотрудников** ![ Изображение нового контрольного списка сотрудников](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="97444-360">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="97444-361">Открыть значки</span><span class="sxs-lookup"><span data-stu-id="97444-361">Open Badges</span></span>

<span data-ttu-id="97444-362">Open Badges — это приложение Microsoft Teams, которое позволяет пользователям получать цифровые значки учетных данных для обучения в контексте Teams и делиться ими во всем мире.</span><span class="sxs-lookup"><span data-stu-id="97444-362">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="97444-363">Использование возможностей сторонних органов по выдаче цифровых значков [Badgr](https://badgr.org/), отмеченных значками, записывается в профиле Badgr получателя и доступно для создания и обмена богатой картиной путешествий по обучению в течение всей жизни.</span><span class="sxs-lookup"><span data-stu-id="97444-363">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="97444-364">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

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

## <a name="poll"></a><span data-ttu-id="97444-367">Опрос</span><span class="sxs-lookup"><span data-stu-id="97444-367">Poll</span></span> 

<span data-ttu-id="97444-368">Poll — это настраиваемая программа расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которая позволяет быстро создавать и отправлять опросы в чате или канале для сбора мнений и предпочтений группы.</span><span class="sxs-lookup"><span data-stu-id="97444-368">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="97444-369">Приложение поддерживается во всех клиентах платформы Teams — настольных компьютерах, браузерах, iOS и Android — и готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="97444-369">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android  — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="97444-370">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-370">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Создание опроса в представлении Teams](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="97444-372">Быстрые ответы</span><span class="sxs-lookup"><span data-stu-id="97444-372">Quick Responses</span></span>

<span data-ttu-id="97444-373">Quick Responses — это приложение Microsoft Teams, которое предоставляет надежное решение для эффективного ответа на часто задаваемые вопросы пользователей (часто задаваемые вопросы).</span><span class="sxs-lookup"><span data-stu-id="97444-373">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions (FAQs).</span></span> <span data-ttu-id="97444-374">Вместо того, чтобы отвечать на каждый запрос вручную и непрерывно повторять информацию, приложение будет создавать библиотеку ответов для интерактивного пользовательского интерфейса с помощью расширений обмена сообщениями [Teams.](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="97444-374">Instead of answering each query manually and  continuously repeating information, the app will build a library of responses for an interactive user experience via Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="97444-375">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Пример представления ответов](../assets/images/quick-responses.png)


## <a name="rapid-assist"></a><span data-ttu-id="97444-377">Rapid Assist</span><span class="sxs-lookup"><span data-stu-id="97444-377">Rapid Assist</span></span>

<span data-ttu-id="97444-378">Rapid Assist — это приложение, основанное на платформе Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) которое позволяет партнерам с клиентами быстро подключаться к экспертам, получать быстрые ответы, искать информацию, выполнять открытые запросы и получать уведомления, чтобы быстро получить вызов, чтобы помочь ответить на вопросы.</span><span class="sxs-lookup"><span data-stu-id="97444-378">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="97444-379">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview) и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams, чтобы организации могли легко подключать сотрудников передней линии связи с корпоративными связями для решения запросов клиентов и обеспечения отличного обслуживания клиентов.</span><span class="sxs-lookup"><span data-stu-id="97444-379">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="97444-380">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-380">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Интерфейс запроса конечных пользователей](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Представление запроса эксперта](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="97444-383">Отражение</span><span class="sxs-lookup"><span data-stu-id="97444-383">Reflect</span></span> 

<span data-ttu-id="97444-384">Reflect — это настраиваемая программа расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которая предоставляет безопасный и инклюзивный ресурс для членов вашей команды, чтобы поделиться состоянием своего эмоционального благополучия с коллегами и/или руководителями групп непосредственно в Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-384">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues and/or group leaders directly within Teams.</span></span> <span data-ttu-id="97444-385">Приложение доступно в чатах каналов, групп, собраний и 1:1, а ответ на регистрацию можно настроить на общедоступный, частный или полностью анонимный.</span><span class="sxs-lookup"><span data-stu-id="97444-385">The app is available in channel, group, meeting, and 1:1 chats and the check-in response can be set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="97444-386">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-386">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="97444-387">**Опрос благополучия**</span><span class="sxs-lookup"><span data-stu-id="97444-387">**Well-being poll**</span></span>
    
    ![Отражение опроса пользователей приложения](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="97444-389">Удаленная поддержка</span><span class="sxs-lookup"><span data-stu-id="97444-389">Remote Support</span></span>

<span data-ttu-id="97444-390">Удаленная поддержка — это [бот Microsoft Teams,](../bots/what-are-bots.md) который обеспечивает целенаправленный интерфейс между запрашивателями поддержки по всей организации и внутренней группе поддержки.</span><span class="sxs-lookup"><span data-stu-id="97444-390">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="97444-391">Конечные пользователи могут отправлять, редактировать или отзывать запросы на поддержку, а группа поддержки может отвечать, управлять и обновлять запросы на все запросы на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-391">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="97444-392">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-392">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

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

## <a name="request-a-team"></a><span data-ttu-id="97444-395">Request-a-team</span><span class="sxs-lookup"><span data-stu-id="97444-395">Request-a-team</span></span>

<span data-ttu-id="97444-396">Request-a-team — это приложение Microsoft Teams, которое оптимизирует создание новых групп для организации предприятия.</span><span class="sxs-lookup"><span data-stu-id="97444-396">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="97444-397">Приложение поддерживает стандартизацию и передовую практику при создании новых экземпляров группы с помощью интеграции формы запроса с управляемым мастером, встроенного процесса утверждения, панели мониторинга состояния запроса и создания автоматизированной группы.</span><span class="sxs-lookup"><span data-stu-id="97444-397">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="97444-398">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-398">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

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

## <a name="scrums-for-channels"></a><span data-ttu-id="97444-401">Scrums для каналов</span><span class="sxs-lookup"><span data-stu-id="97444-401">Scrums for Channels</span></span>

<span data-ttu-id="97444-402">Scrums for Channels — это приложение-помощник scrum, которое позволяет пользователям планировать и запускать scrums в каналах в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-402">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="97444-403">Приложение отлично подходит для удаленных групп и групп, состоящих из участников из различных географических расположений и часовых поясов, чтобы обмениваться ежедневными обновлениями и обеспечивать участие в заседаниях стендап scrum.</span><span class="sxs-lookup"><span data-stu-id="97444-403">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="97444-404">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-404">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="97444-405">Для проведения собраний по scrum в групповом чате см. в нашем шаблоне [приложения Scrums for Group Chat.](#scrums-for-group-chat)</span><span class="sxs-lookup"><span data-stu-id="97444-405">To conduct scrum meetings in a group chat, please see our [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

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

## <a name="scrums-for-group-chat"></a><span data-ttu-id="97444-408">Scrums для группового чата</span><span class="sxs-lookup"><span data-stu-id="97444-408">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="97444-409">Шаблон приложения Состояния Scrums был обновлен и теперь является Scrums для группового чата.</span><span class="sxs-lookup"><span data-stu-id="97444-409">The Scrums Status app template has been updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="97444-410">Scrums для группового чата является вспомогательным помощником scrum, который позволяет участникам группового чата запускать асинхронные собрания и легко делиться своими ежедневными обновлениями.</span><span class="sxs-lookup"><span data-stu-id="97444-410">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="97444-411">Это позволяет всем участникам группового чата вносить вклад в схватку и просматривать обновления, сделанные другими пользователями в рабочей схватке.</span><span class="sxs-lookup"><span data-stu-id="97444-411">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="97444-412">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-412">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Scrums для демонстрации группового чата](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="97444-414">Share Now</span><span class="sxs-lookup"><span data-stu-id="97444-414">Share Now</span></span> 

<span data-ttu-id="97444-415">Приложение Share Now способствует позитивному обмену информацией между коллегами, позволяя пользователям легко обмениваться контентом в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-415">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="97444-416">Пользователи вовлекли приложение в обмен элементами, которые интересуют участников группы, обнаруживая новое общее содержимое, задав предпочтения и закладки для более позднего чтения.</span><span class="sxs-lookup"><span data-stu-id="97444-416">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="97444-417">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-417">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Выбор представления контента](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="97444-419">Поиск в списке SharePoint</span><span class="sxs-lookup"><span data-stu-id="97444-419">SharePoint List Search</span></span>

<span data-ttu-id="97444-420">Совместная работа в Microsoft Teams часто ссылается на сведения, содержащиеся в элементов в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="97444-420">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="97444-421">Простое вклейка ссылки на этот элемент заставляет всех переключать контекст из беседы, находить необходимые сведения, а затем возвращаться в Teams, чтобы продолжить беседу.</span><span class="sxs-lookup"><span data-stu-id="97444-421">Simply pasting a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="97444-422">По мере того как беседа продолжается, обычно людям придется несколько раз переключаться на справочный элемент, чтобы проверить новые комментарии и обновить свои воспоминания о сведениях, содержащихся в элементе.</span><span class="sxs-lookup"><span data-stu-id="97444-422">As the conversation continues typically people will have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="97444-423">Это переключение контекста создает барьер для плавного взаимодействия и является рецептом для вещей, попадающих в трещины.</span><span class="sxs-lookup"><span data-stu-id="97444-423">This context switching creates a barrier to smooth collaboration, and is a recipe for things falling through the cracks.</span></span>

<span data-ttu-id="97444-424">Чтобы облегчить эту боль, мы с радостью привнося вам шаблон приложения поиска списка.</span><span class="sxs-lookup"><span data-stu-id="97444-424">To help alleviate this pain, we are happy to bring to you the List Search app template.</span></span> <span data-ttu-id="97444-425">Миллионы пользователей используют SharePoint для питания некоторых основных процессов в своих организациях.</span><span class="sxs-lookup"><span data-stu-id="97444-425">Millions of users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="97444-426">Однако совместная работа со списками может быть особенно утомительной.</span><span class="sxs-lookup"><span data-stu-id="97444-426">However, collaborating around lists can be especially tedious.</span></span> <span data-ttu-id="97444-427">Используя шаблон приложения поиска списков в Microsoft Teams, пользователи могут вставлять сведения из элементов списка SharePoint непосредственно в чате, чтобы облегчить переключение контекста, вызванное при простом включении ссылки в чат.</span><span class="sxs-lookup"><span data-stu-id="97444-427">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="97444-428">Эти сведения вставляются в виде легко читаемой автоформатной карты, помогая пользователям оставаться в стороне от беседы.</span><span class="sxs-lookup"><span data-stu-id="97444-428">The information is inserted as an easy-to-read auto-formatted card, helping your users stay engaged in the conversation.</span></span>

[<span data-ttu-id="97444-429">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-429">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Приложение Поиска списка](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="97444-431">Регистрация персонала</span><span class="sxs-lookup"><span data-stu-id="97444-431">Staff Check-ins</span></span>

<span data-ttu-id="97444-432">Регистрация сотрудников — это приложение на основе [power Apps,](/powerapps/powerapps-overview)которое позволяет контролировать связь между бизнесом и сотрудниками на местах.</span><span class="sxs-lookup"><span data-stu-id="97444-432">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview)-based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="97444-433">Сотрудники могут легко предоставлять критически важные для времени сведения и обновления состояния непосредственно из Teams на запланированной или разной основе.</span><span class="sxs-lookup"><span data-stu-id="97444-433">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="97444-434">Приложение поддерживает расположение, фотографии и заметки в режиме реального времени, а также уведомления о напоминаниях и автоматизированные процессы.</span><span class="sxs-lookup"><span data-stu-id="97444-434">The app supports real-time location, photos, and notes as well as reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="97444-435">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-435">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Создание представления регистрации](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="97444-437">Опрос</span><span class="sxs-lookup"><span data-stu-id="97444-437">Survey</span></span>

<span data-ttu-id="97444-438">Survey — это настраиваемое приложение для расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которое позволяет создавать опрос в чате или канале для сбора данных и получения информации.</span><span class="sxs-lookup"><span data-stu-id="97444-438">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span>  <span data-ttu-id="97444-439">Приложение поддерживается во всех клиентах платформы Teams — настольных компьютерах, браузерах, iOS и Android — и готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="97444-439">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="97444-440">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-440">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Создание опроса в представлении Teams](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally"></a><span data-ttu-id="97444-442">Время Tally</span><span class="sxs-lookup"><span data-stu-id="97444-442">Time Tally</span></span> 

<span data-ttu-id="97444-443">Проект может включать несколько задач, а сотрудникам могут быть назначены различные проекты.</span><span class="sxs-lookup"><span data-stu-id="97444-443">A project can include multiple tasks, and various projects can be assigned to employees.</span></span> <span data-ttu-id="97444-444">Руководители должны понимать ход выполнения проекта за время, затраченное сотрудниками на выполнение этих задач.</span><span class="sxs-lookup"><span data-stu-id="97444-444">Managers are required to understand the project progress through the time spent by the employees on these tasks.</span></span> <span data-ttu-id="97444-445">Это может быть громоздким действием, так как сотрудникам необходимо заполнить таблицы.</span><span class="sxs-lookup"><span data-stu-id="97444-445">This can be a cumbersome activity, as the employees need to fill in the timesheets.</span></span> <span data-ttu-id="97444-446">Приложение Time Tally позволяет сотрудникам быстро заполнять свои таблицы с помощью мобильного устройства, а руководителям не нужно следить за сотрудниками во время записи.</span><span class="sxs-lookup"><span data-stu-id="97444-446">Time Tally app enables employees to fill their timesheets quickly, using the mobile device, and managers do not have to follow up with employees on the timesheet entry.</span></span> <span data-ttu-id="97444-447">Руководители получают возможность просматривать использование проекта на основе ресурсов и могут утверждать или отклонить записи.</span><span class="sxs-lookup"><span data-stu-id="97444-447">Managers get to view the project utilization based on resources, and they can approve or reject the entries.</span></span> <span data-ttu-id="97444-448">Уведомления о напоминаниях отправляются для обеспечения соответствия времени.</span><span class="sxs-lookup"><span data-stu-id="97444-448">Reminder notifications are sent to ensure timesheet compliance.</span></span> <span data-ttu-id="97444-449">Кроме того, для аналитики доступны исторические данные и использование.</span><span class="sxs-lookup"><span data-stu-id="97444-449">Also, historical data and utilizations are available for analytics.</span></span>

[<span data-ttu-id="97444-450">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-450">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Время Tally](../assets/images/11zon_gif.gif)

## <a name="virtual-rounding"></a><span data-ttu-id="97444-452">Виртуальное округление</span><span class="sxs-lookup"><span data-stu-id="97444-452">Virtual Rounding</span></span>

<span data-ttu-id="97444-453">Поставщики больничных и экстренных служб делают десятки, а зачастую и сотни **обходов** в день.</span><span class="sxs-lookup"><span data-stu-id="97444-453">Hospital and emergency room providers make dozens, and often hundreds of **rounds** per day.</span></span> <span data-ttu-id="97444-454">Эти быстрые проверки для пациентов предназначены для проверки состояния пациента и обеспечения решения проблем пациента.</span><span class="sxs-lookup"><span data-stu-id="97444-454">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="97444-455">Хотя округление является важной практикой, чтобы обеспечить наблюдение за пациентами со стороны нескольких типов поставщиков, они представляют собой огромную утечку на PPE, так как для каждого посещения, от каждого поставщика, новая маска, и новый набор перчаток должны быть использованы.</span><span class="sxs-lookup"><span data-stu-id="97444-455">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves must be used.</span></span> <span data-ttu-id="97444-456">С помощью этих шаблонов приложений медицинские работники могут легко проводить обходы практически через собрание Microsoft Teams между поставщиком и пациентом.</span><span class="sxs-lookup"><span data-stu-id="97444-456">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="97444-457">Решение виртуального округлиния также ссылается в блоге Microsoft Health and Life [Sciences.](https://aka.ms/teamsvirtualrounding)</span><span class="sxs-lookup"><span data-stu-id="97444-457">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="97444-458">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-458">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Виртуальное округление](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="97444-460">Управление посетителями</span><span class="sxs-lookup"><span data-stu-id="97444-460">Visitor Management</span></span>

<span data-ttu-id="97444-461">Приложение Управления посетителями позволяет вашей организации и сотрудникам легко и эффективно управлять процессом посетителей на месте непосредственно из Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="97444-461">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="97444-462">Приложение позволяет сотрудникам создавать запросы посетителей, централизованно отслеживать состояние запроса через панель мониторинга посетителей и получать уведомления в режиме реального времени при прибытии посетителя.</span><span class="sxs-lookup"><span data-stu-id="97444-462">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="97444-463">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-463">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

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

## <a name="workplace-awards"></a><span data-ttu-id="97444-466">Награды на рабочем месте</span><span class="sxs-lookup"><span data-stu-id="97444-466">Workplace Awards</span></span>

<span data-ttu-id="97444-467">Workplace Awards — это шаблон приложений Teams, который обеспечивает положительные рамки, которые способствуют признанию и поощряют культуру оценки сотрудников на современном рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="97444-467">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="97444-468">Приложение позволяет настроить и управлять программой поощрения и распознавания сотрудников (R&R), в которой сотрудники могут легко назначать и поддерживать коллег, а лидер R&R может просматривать представленные номинации, гранты и объявлять получателей.</span><span class="sxs-lookup"><span data-stu-id="97444-468">The app enables you to setup and manage an employee rewards and recognition (R&R) program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="97444-469">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="97444-469">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="97444-470">Карточка номинации На рабочем месте</span><span class="sxs-lookup"><span data-stu-id="97444-470">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Вкладка "Список наград на рабочем месте"](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="97444-472">Есть идея шаблона приложения, который вы хотите увидеть?</span><span class="sxs-lookup"><span data-stu-id="97444-472">Have an idea for an app template you'd like to see?</span></span> <span data-ttu-id="97444-473">[Пожалуйста, дайте нам знать](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span><span class="sxs-lookup"><span data-stu-id="97444-473">[Please let us know](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>
