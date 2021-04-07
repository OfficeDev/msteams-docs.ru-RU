---
title: Шаблоны приложений Microsoft Teams
description: Ссылки и описания шаблонов приложений для платформы Microsoft Teams
ms.topic: reference
keywords: Шаблоны Microsoft Teams примеры демонстрации
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 53355b4a22ae9ace5dec36a97183ddc1f6bf05fb
ms.sourcegitcommit: 82bda0599ba2676ab9348c2f4284f73c7dad0838
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596690"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="a424d-104">Шаблоны приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a424d-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="a424d-105">Шаблоны приложений — это примеры полных приложений для Microsoft Teams с открытым исходным кодом и доступных в GitHub.</span><span class="sxs-lookup"><span data-stu-id="a424d-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="a424d-106">Каждый шаблон приложения содержит подробные инструкции по развертыванию и установке этого приложения для организации.</span><span class="sxs-lookup"><span data-stu-id="a424d-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="a424d-107">Он также предоставляет пример приложения, которое можно установить и начать использовать немедленно.</span><span class="sxs-lookup"><span data-stu-id="a424d-107">It also provides a sample app that you can install and begin using immediately.</span></span> <span data-ttu-id="a424d-108">Кроме того, доступен полный исходный код, который позволяет подробно изучить его или раздвоить код и изменить его, чтобы соответствовать определенным требованиям.</span><span class="sxs-lookup"><span data-stu-id="a424d-108">The complete source code is available too, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="a424d-109">Все шаблоны приложений предоставляются в соответствии с [условиями лицензии MIT.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)</span><span class="sxs-lookup"><span data-stu-id="a424d-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>
> [!NOTE] 
> <span data-ttu-id="a424d-110">Необходимо лицензировать и поддерживать приложения, созданные из шаблонов приложений для пользователей и организаций.</span><span class="sxs-lookup"><span data-stu-id="a424d-110">You must license and support apps created from app templates for your users and organizations.</span></span> <span data-ttu-id="a424d-111">Корпорация Майкрософт не несет ответственности за лицензии и поддержку.</span><span class="sxs-lookup"><span data-stu-id="a424d-111">Microsoft is not responsible for licenses and support.</span></span>

<span data-ttu-id="a424d-112">**&#9734; указывает только что выпущенные шаблоны приложений.**</span><span class="sxs-lookup"><span data-stu-id="a424d-112">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="a424d-113">Основные преимущества</span><span class="sxs-lookup"><span data-stu-id="a424d-113">Key benefits</span></span>

* <span data-ttu-id="a424d-114">**Развертывание непосредственно в облаке:** Все шаблоны приложений включают сценарии развертывания, которые позволяют развертывать все необходимые службы в Microsoft Azure или Power Platform.</span><span class="sxs-lookup"><span data-stu-id="a424d-114">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="a424d-115">**Рекомендуемый пример кода:** Шаблоны приложений соответствуют рекомендуемой рекомендации по безопасности и инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="a424d-115">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="a424d-116">Все внесенные сообществом изменения в шаблоны приложений проверяются для обеспечения соответствия.</span><span class="sxs-lookup"><span data-stu-id="a424d-116">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="a424d-117">**Настраиваемые и размязывные:** Несмотря на то, что все шаблоны приложений можно развернуть с минимальной конфигурацией, мы предоставляем всю базу кода и сценарии развертывания, чтобы вы могли легко настраивать или расширять их, чтобы соответствовать вашим уникальным потребностям.</span><span class="sxs-lookup"><span data-stu-id="a424d-117">**Customizable and extensible:** While all app templates can be deployed with minimal configuration, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="a424d-118">**Подробные документы:** Все шаблоны приложений сопровождаются документацией по архитектуре решений, развертыванию и этапам конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a424d-118">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot"></a><span data-ttu-id="a424d-119">Бот по внедрению</span><span class="sxs-lookup"><span data-stu-id="a424d-119">Adoption Bot</span></span> 

<span data-ttu-id="a424d-120">Средство принятия — это чат-бот по уходу за пользователями, построенный с помощью power Virtual Agent for Teams (PVA).</span><span class="sxs-lookup"><span data-stu-id="a424d-120">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams (PVA).</span></span> <span data-ttu-id="a424d-121">Его можно считать PVA-версией FAQPlus.</span><span class="sxs-lookup"><span data-stu-id="a424d-121">It can be considered as the PVA version of FAQPlus.</span></span> <span data-ttu-id="a424d-122">Бот-принятия отвечает на 100+ распространенных вопросов о Microsoft 365 и Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-122">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="a424d-123">Можно редактировать существующие темы, добавлять собственные темы и гнать существующие вопросы.</span><span class="sxs-lookup"><span data-stu-id="a424d-123">You can edit the existing topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="a424d-124">Если пользователям нужна дополнительная помощь, Бот-пользователь может подключить их к экспертам или даже расширить доступ к билетам на обслуживание с соединиттелями потока премиум-класса. Этот бот может быть установлен самостоятельно или встроен в настраиваемого приложения, например [концентратора принятия.](https://github.com/akporzondek/adoption_hub)</span><span class="sxs-lookup"><span data-stu-id="a424d-124">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.This bot can be installed on it's own or built into a custom app like the [Adoption Hub](https://github.com/akporzondek/adoption_hub).</span></span>

[<span data-ttu-id="a424d-125">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-125">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="adoption-tool-9734"></a><span data-ttu-id="a424d-126">Средство принятия &#9734;</span><span class="sxs-lookup"><span data-stu-id="a424d-126">Adoption Tool &#9734;</span></span>

<span data-ttu-id="a424d-127">Средство принятия состоит из следующих двух шаблонов приложений:</span><span class="sxs-lookup"><span data-stu-id="a424d-127">Adoption Tool consists of the following two app templates:</span></span>

### <a name="champion-management-platform"></a><span data-ttu-id="a424d-128">Платформа управления чемпионами</span><span class="sxs-lookup"><span data-stu-id="a424d-128">Champion Management Platform</span></span>

<span data-ttu-id="a424d-129">Шаблон приложения Платформы управления чемпионами (CMP) помогает управлять, масштабировать и вдохновлять чемпионов командной работы, чтобы добиться большего.</span><span class="sxs-lookup"><span data-stu-id="a424d-129">The Champion Management Platform (CMP) app template helps you manage, scale, and inspire your teamwork champions to achieve more.</span></span> <span data-ttu-id="a424d-130">Этот шаблон приложения построен на SharePoint Framework и загружается на вкладку в команде.</span><span class="sxs-lookup"><span data-stu-id="a424d-130">This app template is built on the SharePoint Framework and loaded into a tab within a team.</span></span> <span data-ttu-id="a424d-131">Группы могут использовать этот инструмент для управления членством в программе, предоставления лидеров и типов событий для ведения журнала, а также инструментов для наложения цифровых значков для участников программы.</span><span class="sxs-lookup"><span data-stu-id="a424d-131">Groups can leverage this tool to help manage program membership, provide a leaderboard and event types for logging, and tools to overlay digital badges to program participants.</span></span>

[<span data-ttu-id="a424d-132">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-132">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

### <a name="get-started"></a><span data-ttu-id="a424d-133">Начало работы</span><span class="sxs-lookup"><span data-stu-id="a424d-133">Get Started</span></span>

<span data-ttu-id="a424d-134">Шаблон приложения Get Started позволяет использовать в microsoft 365 обучающие пути в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-134">The Get Started app template allows you to bring the power of Microsoft 365 learning pathways inside of Microsoft Teams.</span></span> <span data-ttu-id="a424d-135">Этот шаблон приложения позволяет легко получить доступ к определенным страницам обучения или другим интрасетям и загрузить содержимое непосредственно в Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-135">This app template allows you to grant easy access to specific training pages or other intranet assets and load the content directly within Teams.</span></span> <span data-ttu-id="a424d-136">Вы также можете изменить имя или логотип приложения, чтобы соответствовать брендингу вашей компании.</span><span class="sxs-lookup"><span data-stu-id="a424d-136">You can also change the app name or logo to match your company branding.</span></span>

[<span data-ttu-id="a424d-137">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-137">Get it on GitHub</span></span>](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="appointment-manager"></a><span data-ttu-id="a424d-138">Менеджер по встречам</span><span class="sxs-lookup"><span data-stu-id="a424d-138">Appointment Manager</span></span> 

<span data-ttu-id="a424d-139">Диспетчер назначений — это шаблон приложений Teams, который помогает предприятиям создавать, управлять и проводить виртуальные встречи с потребителями через Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-139">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="a424d-140">Новые запросы на прием от потребителей видны в каналах Teams, где их можно быстро назначить и переназначить сотрудникам в команде.</span><span class="sxs-lookup"><span data-stu-id="a424d-140">New appointment requests from consumers are visible in Teams channels, where they can quickly be assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="a424d-141">Запросы на встречу можно просматривать на командном или личном уровнях с помощью настраиваемой вкладки.</span><span class="sxs-lookup"><span data-stu-id="a424d-141">Appointment requests can be viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="a424d-142">Каждая встреча связана с онлайн-собранием Teams, поэтому сотрудники и потребители могут легко присоединиться к собранию в запланированное время.</span><span class="sxs-lookup"><span data-stu-id="a424d-142">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="a424d-143">Шаблон приложения интегрируется с Microsoft Bookings для простого управления назначением.</span><span class="sxs-lookup"><span data-stu-id="a424d-143">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="a424d-144">Запланированные встречи автоматически отображаются в календарях назначенного персонала, а потребители получают настраиваемые уведомления электронной почты и напоминания со встроенными ссылками на собрания.</span><span class="sxs-lookup"><span data-stu-id="a424d-144">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="a424d-145">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-145">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="a424d-146">![Менеджер по обзору ](../assets/images/appointment-manager-overview.png)
 ![ назначений диспетчера назначений в teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="a424d-146">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="a424d-147">Ask Away</span><span class="sxs-lookup"><span data-stu-id="a424d-147">Ask Away</span></span>

<span data-ttu-id="a424d-148">Ask Away — это [бот Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям проводить сеансы Q&(вопросы и ответы) в Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-148">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Q&A (Question and Answer) sessions within Teams.</span></span> <span data-ttu-id="a424d-149">С помощью бота Ask Away участники группы могут отправлять и задавать вопросы до голосования, общие коллегами, что позволяет Q&A-хостов для легкого сбора вопросов в канале или чате.</span><span class="sxs-lookup"><span data-stu-id="a424d-149">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="a424d-150">Бот может использоваться для проведения сеанса Q&в режиме реального времени на собрании Teams и позволяет участникам отправлять вопросы в режиме реального времени в чате.</span><span class="sxs-lookup"><span data-stu-id="a424d-150">The bot can be used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live via chat.</span></span>

[<span data-ttu-id="a424d-151">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-151">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Просмотр всплывающее окно в таблице лидеров для голосования пользователей по вопросам](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="a424d-153">Вспомогательная аналитика</span><span class="sxs-lookup"><span data-stu-id="a424d-153">Associate Insights</span></span>

<span data-ttu-id="a424d-154">Associate Insights — это шаблон [Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) который позволяет сотрудникам firstline напрямую фиксировать и отправлять мнения клиентов, настроения и восприятие.</span><span class="sxs-lookup"><span data-stu-id="a424d-154">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="a424d-155">Работники Firstline часто являются первым представителем компании, который может взаимодействовать с клиентами в контактной точке один к одному.</span><span class="sxs-lookup"><span data-stu-id="a424d-155">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="a424d-156">Собранные данные можно совместно использовать бизнес-группами, например, с помощью вкладки Power BI Teams для улучшения продукта и улучшения работы с клиентами.</span><span class="sxs-lookup"><span data-stu-id="a424d-156">The collected data can be shared and used collaboratively by business teams, e.g., via a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="a424d-157">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-157">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

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

## <a name="attendance"></a><span data-ttu-id="a424d-160">Присутствие</span><span class="sxs-lookup"><span data-stu-id="a424d-160">Attendance</span></span>

<span data-ttu-id="a424d-161">Приложение Для участия — это [вкладка Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) которую можно закрепить в команде.</span><span class="sxs-lookup"><span data-stu-id="a424d-161">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that can be pinned in a team.</span></span> <span data-ttu-id="a424d-162">Он предназначен для записи присутствия, как правило, в таких параметрах, как среда обучения и обучения.</span><span class="sxs-lookup"><span data-stu-id="a424d-162">It is designed to record presence, typically in settings such as learning and training environments.</span></span> <span data-ttu-id="a424d-163">Пользователи могут отмечать или изменять посещаемость в течение до 30 дней в прошлом и просматривать обобщенные отчеты о посещаемости для всей группы или отдельных участников.</span><span class="sxs-lookup"><span data-stu-id="a424d-163">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span>

[<span data-ttu-id="a424d-164">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-164">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![Демонстрация приложения для посещаемости](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="a424d-166">Book-a-room</span><span class="sxs-lookup"><span data-stu-id="a424d-166">Book-a-room</span></span>

<span data-ttu-id="a424d-167">Book-a-room — это бот [Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям быстро находить и резервировать зал собраний в течение 30 (по умолчанию), 60 или 90 минут начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="a424d-167">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="a424d-168">Область бота Book-a-room для личных или 1:1 бесед.</span><span class="sxs-lookup"><span data-stu-id="a424d-168">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

[<span data-ttu-id="a424d-169">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-169">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![Демонстрация book-a-room](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="a424d-171">Доступ к зданиям</span><span class="sxs-lookup"><span data-stu-id="a424d-171">Building Access</span></span>

<span data-ttu-id="a424d-172">Building Access — это приложение, основанное на платформе Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)которое поддерживает администрирование пороговых значений заполняемости зданий и норм социального расстановки, позволяя директорам объектов управлять, отслеживать и сообщать о присутствии сотрудников на месте.</span><span class="sxs-lookup"><span data-stu-id="a424d-172">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="a424d-173">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview)и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams и позволяет организациям определять готовность к созданию, устанавливать критерии приемлемости для доступа на месте и собирать сведения для планирования в будущем.</span><span class="sxs-lookup"><span data-stu-id="a424d-173">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="a424d-174">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-174">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Карта резервирования доступа к зданию](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Представление ключа "Создание доступа"](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="a424d-177">Праздники</span><span class="sxs-lookup"><span data-stu-id="a424d-177">Celebrations</span></span>

<span data-ttu-id="a424d-178">Celebrations — это приложение Teams, которое помогает участникам группы отмечать дни рождения, юбилеи и другие повторяющиеся события.</span><span class="sxs-lookup"><span data-stu-id="a424d-178">Celebrations is a Teams app that helps team members celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="a424d-179">Он запоминает особые случаи всех членов команды и отправляет приветственное сообщение во всех командах, выбранных во время создания событий, чтобы участники группы чувствовали себя особенными в свой день.</span><span class="sxs-lookup"><span data-stu-id="a424d-179">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="a424d-180">Приложение предоставляет простой интерфейс для всех членов группы, чтобы лично добавить и просмотреть свои события, а также позволяет пользователю выбрать команды, в которых события получают общий доступ.</span><span class="sxs-lookup"><span data-stu-id="a424d-180">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="a424d-181">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-181">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="a424d-182">Контрольный список</span><span class="sxs-lookup"><span data-stu-id="a424d-182">Checklist</span></span>

<span data-ttu-id="a424d-183">Контрольный список — это настраиваемая программа расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которая позволяет вам сотрудничать со своей командой, создавая общий контрольный список в чате или канале.</span><span class="sxs-lookup"><span data-stu-id="a424d-183">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="a424d-184">Приложение поддерживается во всех клиентах платформы Teams — настольных компьютерах, браузерах, iOS и Android — и готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="a424d-184">The app is supported across all Teams platform clients —  desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="a424d-185">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-185">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![Создание контрольного списка в представлении Teams](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in"></a><span data-ttu-id="a424d-187">Заехав в класс</span><span class="sxs-lookup"><span data-stu-id="a424d-187">Classroom Drop-in</span></span> 

<span data-ttu-id="a424d-188">В классе drop-in — это приложение на основе платформы Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)которое позволяет руководителям систем находить группы классов (виртуальные классы) и добавлять себя или других в эти группы класса в течение указанного периода при необходимости.</span><span class="sxs-lookup"><span data-stu-id="a424d-188">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams (virtual classrooms) and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="a424d-189">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview) и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams, чтобы убедиться, что учебные заведения могут оптимизировать свои операции в гибридной среде обучения, предоставляя доступ к соответствующим заинтересованным сторонам для групп классов по бизнес-требованиям.</span><span class="sxs-lookup"><span data-stu-id="a424d-189">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="a424d-190">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-190">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Запрос на отсев класса](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="a424d-192">Корпоративный Communicator</span><span class="sxs-lookup"><span data-stu-id="a424d-192">Company Communicator</span></span>

<span data-ttu-id="a424d-193">Приложение Communicator позволяет корпоративным группам создавать и отправлять сообщения, предназначенные для нескольких групп или большого числа сотрудников в чате, позволяя организации достигать сотрудников прямо там, где они сотрудничают.</span><span class="sxs-lookup"><span data-stu-id="a424d-193">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="a424d-194">Используйте этот шаблон для нескольких сценариев, таких как новые объявления об инициативе, учет сотрудников, современное обучение и разработка или широкомасштабные трансляции.</span><span class="sxs-lookup"><span data-stu-id="a424d-194">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="a424d-195">Приложение обеспечивает простой интерфейс для назначенных пользователей для создания, предварительного просмотра, совместной работы и отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="a424d-195">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="a424d-196">Он создает основу для создания настраиваемой целевой системы связи, например настраиваемой телеметрии, о том, сколько пользователей было признано или взаимодействует с сообщением.</span><span class="sxs-lookup"><span data-stu-id="a424d-196">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="a424d-197">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-197">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator составить представление окна](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="a424d-199">Lookup контактной группы</span><span class="sxs-lookup"><span data-stu-id="a424d-199">Contact Group Lookup</span></span>

<span data-ttu-id="a424d-200">Приложение Lookup контактной группы предоставляет удобный и полезный подход к созданию, доступу и управлению контактной группой организации (ранее известной как списки рассылки или группы связи).</span><span class="sxs-lookup"><span data-stu-id="a424d-200">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups (formerly known as distribution lists or communication groups).</span></span> <span data-ttu-id="a424d-201">Пользователи могут быстро просматривать и общаться с участниками группы, просматривать состояние участников и создавать групповой чат с выбранными участниками контактной группы, все в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-201">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="a424d-202">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-202">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

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

## <a name="co-worker-appreciation"></a><span data-ttu-id="a424d-205">Оценка сотрудников</span><span class="sxs-lookup"><span data-stu-id="a424d-205">Co-worker Appreciation</span></span> 

<span data-ttu-id="a424d-206">Используя шаблон оценки сотрудников в Microsoft Teams, пользователи могут распознавать достижения своих коллег в контексте Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-206">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="a424d-207">Когда сотрудники выбирают для вознаграждения коллегу, получатели и другие члены группы помечены в разговоре на канале, и они получают уведомление о вручениях канала.</span><span class="sxs-lookup"><span data-stu-id="a424d-207">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="a424d-208">Награды записывают в приложении Teams, которое является безопасным, переносным и легкодоступным.</span><span class="sxs-lookup"><span data-stu-id="a424d-208">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="a424d-209">Это можно считать версией приложения Open Badges, основанной на PowerApps, с таблицей лидеров.</span><span class="sxs-lookup"><span data-stu-id="a424d-209">This can be considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="a424d-210">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-210">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![В целом](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="a424d-212">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="a424d-212">CrowdSourcer</span></span>

<span data-ttu-id="a424d-213">CrowdSourcer — это [бот Microsoft Teams,](../bots/what-are-bots.md) который предоставляет группам запрашиваемую информацию, которую совместно запрашивают члены группы.</span><span class="sxs-lookup"><span data-stu-id="a424d-213">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="a424d-214">Это отличный способ ответить на часто задамые вопросы, позволяя участникам активно участвовать и вносить вклад в интересный и полезный информационный ресурс.</span><span class="sxs-lookup"><span data-stu-id="a424d-214">It's a great way to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="a424d-215">Get it on Github</span><span class="sxs-lookup"><span data-stu-id="a424d-215">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Взаимодействие с конечным пользователем crowdsource](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="a424d-217">Пользовательские наклейки</span><span class="sxs-lookup"><span data-stu-id="a424d-217">Custom Stickers</span></span>

<span data-ttu-id="a424d-218">Самовыражение является основой здоровой культуры команды.</span><span class="sxs-lookup"><span data-stu-id="a424d-218">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="a424d-219">Этот шаблон приложения — это расширение [обмена](~/messaging-extensions/what-are-messaging-extensions.md) сообщениями, которое позволяет пользователям использовать настраиваемые наклейки и GIF-решения в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-219">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="a424d-220">Этот шаблон предоставляет простой веб-опыт настройки, где любой пользователь с доступом к конфигурации может загружать GIF-ы/наклейки/изображения, которые должны иметь конечные пользователи, что позволяет всей вашей команде использовать любой набор стикеров, которые вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="a424d-220">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs/stickers/images they want their end-users to have, allowing your entire team to use any set of stickers you chose.</span></span>

<span data-ttu-id="a424d-221">Это приложение также позволяет легко обмениваться изображениями/GIF-файлами/наклейками между группами без доступа к сайтам SharePoint или отдельным каналам в качестве механизмов хранения и общего доступа.</span><span class="sxs-lookup"><span data-stu-id="a424d-221">This app also enables easy sharing of images/GIFs/stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="a424d-222">Например, группы продуктов могут легко обмениваться изображениями продуктов и GIF-изображениями с группами социальных сетей, маркетинга и продаж программным образом.</span><span class="sxs-lookup"><span data-stu-id="a424d-222">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="a424d-223">Можно также расширить это приложение, запуская поток уведомлений для определенных групп/отдельных лиц, когда будут доступны новые изображения/GIF-изображения.</span><span class="sxs-lookup"><span data-stu-id="a424d-223">One can also extend this app by triggering a notification flow to specific teams/individuals when new images/GIFs are made available.</span></span>

[<span data-ttu-id="a424d-224">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-224">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Приложение Стикеры](../assets/images/stickers.png)

## <a name="employee-ideas"></a><span data-ttu-id="a424d-226">Идеи сотрудников</span><span class="sxs-lookup"><span data-stu-id="a424d-226">Employee Ideas</span></span>

<span data-ttu-id="a424d-227">Приложение "Идеи сотрудников" — это версия PowerApps шаблона приложения Great Ideas на основе Azure.</span><span class="sxs-lookup"><span data-stu-id="a424d-227">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="a424d-228">Приложение позволяет пользователям Teams настраивать и настраивать кампанию идей.</span><span class="sxs-lookup"><span data-stu-id="a424d-228">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="a424d-229">Кампания идей — это категория для группировки идей вокруг общих тем.</span><span class="sxs-lookup"><span data-stu-id="a424d-229">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="a424d-230">Пользователи teams также могут выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a424d-230">Teams users can also perform following activities:</span></span>
* <span data-ttu-id="a424d-231">Настройте стандартную форму отправки, которую сотрудники должны отправить для каждой идеи.</span><span class="sxs-lookup"><span data-stu-id="a424d-231">Configure a standard submission form that employees need to submit for each idea.</span></span> 
* <span data-ttu-id="a424d-232">Просмотрите и управляйте идеями и списком кампаний.</span><span class="sxs-lookup"><span data-stu-id="a424d-232">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="a424d-233">Изменение и удаление кампаний.</span><span class="sxs-lookup"><span data-stu-id="a424d-233">Modify and delete campaigns.</span></span>
* <span data-ttu-id="a424d-234">Просмотрите советы лидеров идей.</span><span class="sxs-lookup"><span data-stu-id="a424d-234">Review leader boards of ideas.</span></span>
* <span data-ttu-id="a424d-235">Голосуйте за и делитесь приоритетными идеями.</span><span class="sxs-lookup"><span data-stu-id="a424d-235">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="a424d-236">Отправка идей для кампании.</span><span class="sxs-lookup"><span data-stu-id="a424d-236">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="a424d-237">Просмотр идеи другого члена группы.</span><span class="sxs-lookup"><span data-stu-id="a424d-237">View other team member's idea.</span></span>
* <span data-ttu-id="a424d-238">Голосуйте за наиболее понравились идеи.</span><span class="sxs-lookup"><span data-stu-id="a424d-238">Vote on most liked ideas.</span></span>
* <span data-ttu-id="a424d-239">Просмотрите производительность их идей по сравнению с другими в рамках кампании.</span><span class="sxs-lookup"><span data-stu-id="a424d-239">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="a424d-240">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-240">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Управление представлением кампании](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="a424d-242">Электронные рецепты</span><span class="sxs-lookup"><span data-stu-id="a424d-242">E-Prescriptions</span></span> 

<span data-ttu-id="a424d-243">E-Prescriptions — это приложение на основе power [Apps,](/powerapps/maker/canvas-apps/embed-teams-app)которое улучшает телемедицину и виртуальную помощь путем автоматизации процесса выдачи электронных рецептов пациентам.</span><span class="sxs-lookup"><span data-stu-id="a424d-243">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)-based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="a424d-244">Медицинские специалисты могут быстро пересматривать встречи, создавать электронные рецепты и отправлять электронные письма с вложениями по электронному рецепту пациентам непосредственно на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-244">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="a424d-245">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-245">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

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

## <a name="employee-training"></a><span data-ttu-id="a424d-250">Обучение сотрудников</span><span class="sxs-lookup"><span data-stu-id="a424d-250">Employee Training</span></span> 

<span data-ttu-id="a424d-251">Обучение сотрудников — это приложение Microsoft Teams, которое позволяет организаторам легко публиковать, отслеживать и содействовать обучению и учебным мероприятиям для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="a424d-251">Employee training is a Microsoft Teams app that enables organizers to easily publish,  track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="a424d-252">С помощью приложения организаторы событий могут отправлять напоминания и уведомления регистраторам событий, а сотрудники могут указывать на интерес к предстоящим событиям, обновлять текущие события и делиться сведениями о событиях с коллегами через расширение обмена сообщениями Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-252">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues via the Teams messaging extension.</span></span>

[<span data-ttu-id="a424d-253">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-253">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="a424d-254">**Просмотр событий обучения сотрудников** ![ Изображение вкладки подготовки сотрудников](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="a424d-254">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="a424d-255">**Создание события подготовки сотрудников** ![ Обучение сотрудников создает форму событий](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="a424d-255">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="a424d-256">Эксперт finder</span><span class="sxs-lookup"><span data-stu-id="a424d-256">Expert Finder</span></span>

<span data-ttu-id="a424d-257">Expert Finder — это [бот Microsoft Teams,](../bots/what-are-bots.md) который определяет конкретных членов организации на основе их навыков, интересов и атрибутов образования.</span><span class="sxs-lookup"><span data-stu-id="a424d-257">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="a424d-258">Участники находят экспертов в организации, которые соответствуют поиску ключевых слов профилей пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a424d-258">Members find experts within an organization  that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="a424d-259">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-259">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Демонстрация результатов поиска expert Finder](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="a424d-261">Вопросы и ответы плюс</span><span class="sxs-lookup"><span data-stu-id="a424d-261">FAQ Plus</span></span>

<span data-ttu-id="a424d-262">Диалоговая&боты — это простой способ предоставления ответов на часто задамые пользователями вопросы.</span><span class="sxs-lookup"><span data-stu-id="a424d-262">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="a424d-263">Однако большинство ботов не могут эффективно взаимодействовать с пользователями, так как при сбойе бота в цикле нет человека.</span><span class="sxs-lookup"><span data-stu-id="a424d-263">However, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="a424d-264">FaQ bot — это дружественный Q&бот, который приводит человека в цикл, когда он не в состоянии помочь.</span><span class="sxs-lookup"><span data-stu-id="a424d-264">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="a424d-265">Можно задать боту вопрос, и бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="a424d-265">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="a424d-266">Если нет, бот позволяет пользователю отправлять запрос, который затем передается предварительно настроенной группе экспертов, которые помогают обеспечить поддержку, действуя на уведомления из самой группы.</span><span class="sxs-lookup"><span data-stu-id="a424d-266">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="a424d-267">Последний выпуск **FAQ Plus** поддерживает улучшенные решения Q&, позволяя группе экспертов выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a424d-267">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="a424d-268">&#x2714; Q&как непосредственно в базу знаний с помощью расширений сообщений.</span><span class="sxs-lookup"><span data-stu-id="a424d-268">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="a424d-269">&#x2714; изменить и удалить Q&пары, добавленные ботом.</span><span class="sxs-lookup"><span data-stu-id="a424d-269">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="a424d-270">&#x2714; отслеживание истории пересмотра Q&As.</span><span class="sxs-lookup"><span data-stu-id="a424d-270">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="a424d-271">&#x2714; настройка ответа с дополнительными сведениями для отображения в качестве [адаптивной карты.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="a424d-271">&#x2714; Configure an answer with additional details to display as an [adaptive card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="a424d-272">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-272">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Gif FAQ Plus](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app"></a><span data-ttu-id="a424d-274">Получить приложение поддержки</span><span class="sxs-lookup"><span data-stu-id="a424d-274">Get Support App</span></span>

<span data-ttu-id="a424d-275">Приложение Get Support можно использовать организациями, использующими Microsoft Teams, чтобы позволить любому набору пользователей запрашивать помощь у руководителей.</span><span class="sxs-lookup"><span data-stu-id="a424d-275">The Get Support app can be used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="a424d-276">Это приложение включает в себя различные функции, такие как:</span><span class="sxs-lookup"><span data-stu-id="a424d-276">This app includes various features, such as:</span></span>
-   <span data-ttu-id="a424d-277">Запрос помощи для разных категорий в приложении Power</span><span class="sxs-lookup"><span data-stu-id="a424d-277">Requesting assistance on different categories from a Power App</span></span>
-   <span data-ttu-id="a424d-278">Уведомления, отправленные запросчикам, информирующие их о том, кому назначено</span><span class="sxs-lookup"><span data-stu-id="a424d-278">Notifications sent to requestors informing them of who has been assigned</span></span> 
-   <span data-ttu-id="a424d-279">Уведомления, отправленные назначенному руководителю, информирующие их о том, кому нужна помощь</span><span class="sxs-lookup"><span data-stu-id="a424d-279">Notifications sent to assigned supervisors informing them of who needs assistance</span></span> 
-   <span data-ttu-id="a424d-280">Анализ эскалаций и шаблонов в SharePoint и PowerBI</span><span class="sxs-lookup"><span data-stu-id="a424d-280">Analyzing escalations and patterns in SharePoint and PowerBI</span></span>

[<span data-ttu-id="a424d-281">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-281">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Get Support Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="a424d-283">Отслеживание целей</span><span class="sxs-lookup"><span data-stu-id="a424d-283">Goal Tracker</span></span>

<span data-ttu-id="a424d-284">Приложение Goal Tracker — это комплексное решение для организации, которое поддерживает установление целей, наблюдение за прогрессом и признание успеха в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-284">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="a424d-285">Приложение позволяет пользователям устанавливать, отслеживать и обновлять цели на профессиональном, личном и командном уровне.</span><span class="sxs-lookup"><span data-stu-id="a424d-285">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="a424d-286">Члены группы также получают вовремя напоминания и обновления состояния, чтобы оставаться сосредоточенными и оставаться в курсе.</span><span class="sxs-lookup"><span data-stu-id="a424d-286">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="a424d-287">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-287">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

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

## <a name="great-ideas"></a><span data-ttu-id="a424d-290">Великие идеи</span><span class="sxs-lookup"><span data-stu-id="a424d-290">Great Ideas</span></span>

<span data-ttu-id="a424d-291">Приложение Great Ideas поддерживает и расширяет возможности инноваций и творчества в организации.</span><span class="sxs-lookup"><span data-stu-id="a424d-291">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="a424d-292">Приложение позволяет сотрудникам обмениваться идеями с коллегами и руководством, открывать новые материалы, делать акценты на одноранговом рассмотрении и голосовать за лучшие предложения в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-292">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="a424d-293">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-293">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a><span data-ttu-id="a424d-296">Групповые действия</span><span class="sxs-lookup"><span data-stu-id="a424d-296">Group Activities</span></span>

<span data-ttu-id="a424d-297">Групповые действия — это приложение Microsoft Teams, которое позволяет владельцам групп быстро создавать группы действий и управлять рабочими процессами совместной работы в контексте Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-297">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="a424d-298">Авторы действий могут создавать действия, случайным образом распределять членов группы по группам и необязательно отправлять напоминания боту до завершения действий.</span><span class="sxs-lookup"><span data-stu-id="a424d-298">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="a424d-299">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-299">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

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

## <a name="grow-your-skills"></a><span data-ttu-id="a424d-302">Вырастите свои навыки</span><span class="sxs-lookup"><span data-stu-id="a424d-302">Grow Your Skills</span></span>

<span data-ttu-id="a424d-303">Приложение Grow Your Skills поддерживает профессиональный рост и развитие, позволяя сотрудникам вносить вклад в дополнительные проекты для вашей организации, одновременно изучая новые навыки.</span><span class="sxs-lookup"><span data-stu-id="a424d-303">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="a424d-304">Сотрудники могут использовать приложение для поиска возможностей, которые отвечают их интересам, эффективного взаимодействия с коллегами и получения новых уровней знаний и возможностей, все в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-304">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="a424d-305">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-305">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

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

## <a name="hr-support"></a><span data-ttu-id="a424d-308">Поддержка управления персоналом</span><span class="sxs-lookup"><span data-stu-id="a424d-308">HR Support</span></span>

<span data-ttu-id="a424d-309">Бот поддержки кадров — это дружественный Q&бот, который привозит профессионала поддержки или эксперта из группы hr в цикл, когда он не в состоянии помочь.</span><span class="sxs-lookup"><span data-stu-id="a424d-309">HR Support bot is a friendly Q&A bot that brings a support professional/expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="a424d-310">Можно задать боту вопрос, и бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="a424d-310">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="a424d-311">Если нет, бот позволяет пользователю отправить запрос, который затем будет размещен в предварительно настроенной группе экспертов, которые помогают оказывать поддержку, действуя на уведомления из самой команды.</span><span class="sxs-lookup"><span data-stu-id="a424d-311">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="a424d-312">Кроме того, бот предлагает ссылки на рекомендуемые политики и вопросы по персоналу, ища предварительно настроенные теги в этом вопросе.</span><span class="sxs-lookup"><span data-stu-id="a424d-312">Additionally, the bot suggests links to recommended HR policies/questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="a424d-313">Эти плитки также можно найти на связанной вкладке в качестве быстрой ссылки.</span><span class="sxs-lookup"><span data-stu-id="a424d-313">These tiles can also be found in the associated tab as a quick reference.</span></span> <span data-ttu-id="a424d-314">Поддержка кадров хорошо работает для легкого веса QnA и обеспечивает быструю поддержку при запуске новых проектов и инициатив в организации.</span><span class="sxs-lookup"><span data-stu-id="a424d-314">HR Support works well for light weight QnA and to provide quick support when launching new projects/initiatives in the organization.</span></span>

[<span data-ttu-id="a424d-315">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-315">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Поддержка управления персоналом](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="a424d-317">Точки соприкосновения</span><span class="sxs-lookup"><span data-stu-id="a424d-317">Icebreaker</span></span>

<span data-ttu-id="a424d-318">Icebreaker — это [бот Microsoft Teams,](../bots/what-are-bots.md) который помогает вашей команде приблизиться, спарив двух случайных членов команды каждую неделю для встречи.</span><span class="sxs-lookup"><span data-stu-id="a424d-318">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="a424d-319">Бот упрощает планирование, автоматически предлагая свободное время, которое работает для обоих участников.</span><span class="sxs-lookup"><span data-stu-id="a424d-319">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="a424d-320">Укрепляйте личные связи и создайте тесное сообщество с помощью этого приложения.</span><span class="sxs-lookup"><span data-stu-id="a424d-320">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="a424d-321">Помимо поощрения личных подключений всей вашей команды, приложение Icebreaker может помочь развивать сообщества, основанные на интересах вашей организации.</span><span class="sxs-lookup"><span data-stu-id="a424d-321">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="a424d-322">Например, это приложение можно использовать для группы по интересам DevOps, чтобы помочь идеям и лучшим практикам органично распространяться по всей организации.</span><span class="sxs-lookup"><span data-stu-id="a424d-322">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="a424d-323">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-323">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Приложение Icebreaker](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="a424d-325">Стимулы</span><span class="sxs-lookup"><span data-stu-id="a424d-325">Incentives</span></span>

<span data-ttu-id="a424d-326">Стимулы — это шаблон [Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) который управляет и отслеживает стимулирование участия сотрудников в назначенных мероприятиях, таких как тренинги и инициативы по управлению изменениями.</span><span class="sxs-lookup"><span data-stu-id="a424d-326">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities such as trainings and change management initiatives.</span></span> <span data-ttu-id="a424d-327">Администраторы используют приложение для создания назначенных действий, назначения точек для завершения и указания необходимых уровней точки права на вознаграждение.</span><span class="sxs-lookup"><span data-stu-id="a424d-327">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="a424d-328">Сотрудники используют приложение для просмотра накопленных баллов и по достижении допустимости запрашивать и требовать выкупаемых вознаграждений.</span><span class="sxs-lookup"><span data-stu-id="a424d-328">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="a424d-329">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-329">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Демонстрация приложения incentives](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="a424d-331">Репортер инцидентов</span><span class="sxs-lookup"><span data-stu-id="a424d-331">Incident Reporter</span></span>

<span data-ttu-id="a424d-332">Incident Reporter — это [бот Microsoft Teams,](../bots/what-are-bots.md)  который оптимизирует управление инцидентами в организации.</span><span class="sxs-lookup"><span data-stu-id="a424d-332">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="a424d-333">Бот упрощает автоматизированный сбор данных об инцидентах, настраиваемые отчеты об инцидентах, соответствующие уведомления заинтересованных лиц и отслеживание инцидентов в конце концов.</span><span class="sxs-lookup"><span data-stu-id="a424d-333">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="a424d-334">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-334">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

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

## <a name="inspection"></a><span data-ttu-id="a424d-337">Проверка</span><span class="sxs-lookup"><span data-stu-id="a424d-337">Inspection</span></span> 

 <span data-ttu-id="a424d-338">Inspection — это приложение Microsoft Teams, которое позволяет сотрудникам передней линии проверять все, что угодно от расположения до активов и оборудования.</span><span class="sxs-lookup"><span data-stu-id="a424d-338">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="a424d-339">Например, розничный магазин, завод по производству или транспортные средства и машины.</span><span class="sxs-lookup"><span data-stu-id="a424d-339">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="a424d-340">В этом решении есть два приложения, каждое из которых предназначено для разных типов пользователей.</span><span class="sxs-lookup"><span data-stu-id="a424d-340">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="a424d-341">Приложение предоставляет сотрудникам передней линии возможность проверять актив или область, управлять качеством продуктов и услуг или поддерживать безопасность на рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="a424d-341">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="a424d-342">Это облегчает связь между членами группы для решения проблем, найденных во время проверки.</span><span class="sxs-lookup"><span data-stu-id="a424d-342">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="a424d-343">Приложение предоставляет простые отчеты для руководителей, чтобы ускорить решение проблем и выделить тенденции.</span><span class="sxs-lookup"><span data-stu-id="a424d-343">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="a424d-344">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-344">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Обзор инспекции](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a><span data-ttu-id="a424d-346">Отчеты о проблемах</span><span class="sxs-lookup"><span data-stu-id="a424d-346">Issue Reporting</span></span>

<span data-ttu-id="a424d-347">Приложение Отчеты о проблемах позволяет сотрудникам и руководителям поднимать и управлять вопросами.</span><span class="sxs-lookup"><span data-stu-id="a424d-347">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="a424d-348">Она состоит из двух приложений: приложения для отчетов о проблемах и приложения "Управление вопросами" для управления вопросами.</span><span class="sxs-lookup"><span data-stu-id="a424d-348">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="a424d-349">Руководители групп используют приложение Manage Issues для настройки приложения, в том числе канала, в котором приложения создают сообщения Microsoft Teams и задачи планировщика.</span><span class="sxs-lookup"><span data-stu-id="a424d-349">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="a424d-350">Менеджеры также используют приложение для создания форм шаблонов для сбора сведений, когда пользователь сообщает о проблеме.</span><span class="sxs-lookup"><span data-stu-id="a424d-350">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="a424d-351">Например, просмотрите, отредактируете или удалите формы шаблона проблем.</span><span class="sxs-lookup"><span data-stu-id="a424d-351">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="a424d-352">Приложение также можно использовать для рассмотрения проблем группы, отчета об истории проблем и эффективного управления решением проблем.</span><span class="sxs-lookup"><span data-stu-id="a424d-352">The app can also be used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="a424d-353">Сотрудники используют приложение отчетов о проблемах для журналов проблем и сведений, необходимых для их устранения.</span><span class="sxs-lookup"><span data-stu-id="a424d-353">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="a424d-354">Приложение также используется для изменения и решения существующих проблем и получения высокого уровня представления об отдельных или командных проблемах.</span><span class="sxs-lookup"><span data-stu-id="a424d-354">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="a424d-355">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-355">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Представление группы отчетов о проблемах](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="a424d-357">Новые возможности для сотрудников</span><span class="sxs-lookup"><span data-stu-id="a424d-357">New Employee Onboarding</span></span> 

<span data-ttu-id="a424d-358">Новая интеграция сотрудников — это интегрированное решение microsoft Teams и [SharePoint New Employee Onboarding,](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) которое позволяет организации предоставлять сотрудникам в пути по новому найму согласованный и высококачественный опыт работы с бортовой командой.</span><span class="sxs-lookup"><span data-stu-id="a424d-358">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="a424d-359">Приложение может быть использовано группами кадров и менеджерами по найму для предоставления соответствующих сведений в процессе ориентации и индукции, а также для обмена отзывами, предоставления вводных данных и выполнения задач бортового ввода.</span><span class="sxs-lookup"><span data-stu-id="a424d-359">The app can be used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="a424d-360">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-360">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="a424d-361">**Новая приветствие сотрудника** ![ Изображение новой приветствия сотрудника](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="a424d-361">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="a424d-362">**Новый контрольный список сотрудников** ![ Изображение нового контрольного списка сотрудников](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="a424d-362">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="a424d-363">Открыть значки</span><span class="sxs-lookup"><span data-stu-id="a424d-363">Open Badges</span></span>

<span data-ttu-id="a424d-364">Open Badges — это приложение Microsoft Teams, которое позволяет пользователям получать цифровые значки учетных данных для обучения в контексте Teams и делиться ими во всем мире.</span><span class="sxs-lookup"><span data-stu-id="a424d-364">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="a424d-365">Использование возможностей сторонних органов по выдаче цифровых значков [Badgr](https://badgr.org/), отмеченных значками, записывается в профиле Badgr получателя и доступно для создания и обмена богатой картиной путешествий по обучению в течение всей жизни.</span><span class="sxs-lookup"><span data-stu-id="a424d-365">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="a424d-366">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-366">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

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

## <a name="poll"></a><span data-ttu-id="a424d-369">Опрос</span><span class="sxs-lookup"><span data-stu-id="a424d-369">Poll</span></span> 

<span data-ttu-id="a424d-370">Poll — это настраиваемая программа расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которая позволяет быстро создавать и отправлять опросы в чате или канале для сбора мнений и предпочтений группы.</span><span class="sxs-lookup"><span data-stu-id="a424d-370">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="a424d-371">Приложение поддерживается во всех клиентах платформы Teams — настольных компьютерах, браузерах, iOS и Android — и готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="a424d-371">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android  — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="a424d-372">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-372">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Создание опроса в представлении Teams](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="a424d-374">Быстрые ответы</span><span class="sxs-lookup"><span data-stu-id="a424d-374">Quick Responses</span></span>

<span data-ttu-id="a424d-375">Quick Responses — это приложение Microsoft Teams, которое предоставляет надежное решение для эффективного ответа на часто задаваемые вопросы пользователей (часто задаваемые вопросы).</span><span class="sxs-lookup"><span data-stu-id="a424d-375">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions (FAQs).</span></span> <span data-ttu-id="a424d-376">Вместо того, чтобы отвечать на каждый запрос вручную и непрерывно повторять информацию, приложение будет создавать библиотеку ответов для интерактивного пользовательского интерфейса с помощью расширений обмена сообщениями [Teams.](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="a424d-376">Instead of answering each query manually and  continuously repeating information, the app will build a library of responses for an interactive user experience via Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="a424d-377">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-377">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Пример представления ответов](../assets/images/quick-responses.png)


## <a name="rapid-assist"></a><span data-ttu-id="a424d-379">Rapid Assist</span><span class="sxs-lookup"><span data-stu-id="a424d-379">Rapid Assist</span></span>

<span data-ttu-id="a424d-380">Rapid Assist — это приложение, основанное на платформе Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) которое позволяет партнерам с клиентами быстро подключаться к экспертам, получать быстрые ответы, искать информацию, выполнять открытые запросы и получать уведомления, чтобы быстро получить вызов, чтобы помочь ответить на вопросы.</span><span class="sxs-lookup"><span data-stu-id="a424d-380">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="a424d-381">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview) и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams, чтобы организации могли легко подключать сотрудников передней линии связи с корпоративными связями для решения запросов клиентов и обеспечения отличного обслуживания клиентов.</span><span class="sxs-lookup"><span data-stu-id="a424d-381">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="a424d-382">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-382">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Интерфейс запроса конечных пользователей](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Представление запроса эксперта](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="a424d-385">Отражение</span><span class="sxs-lookup"><span data-stu-id="a424d-385">Reflect</span></span> 

<span data-ttu-id="a424d-386">Reflect — это настраиваемая программа расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которая предоставляет безопасный и инклюзивный ресурс для членов вашей команды, чтобы поделиться состоянием своего эмоционального благополучия с коллегами и/или руководителями групп непосредственно в Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-386">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues and/or group leaders directly within Teams.</span></span> <span data-ttu-id="a424d-387">Приложение доступно в чатах каналов, групп, собраний и 1:1, а ответ на регистрацию можно настроить на общедоступный, частный или полностью анонимный.</span><span class="sxs-lookup"><span data-stu-id="a424d-387">The app is available in channel, group, meeting, and 1:1 chats and the check-in response can be set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="a424d-388">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-388">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="a424d-389">**Опрос благополучия**</span><span class="sxs-lookup"><span data-stu-id="a424d-389">**Well-being poll**</span></span>
    
    ![Отражение опроса пользователей приложения](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="a424d-391">Удаленная поддержка</span><span class="sxs-lookup"><span data-stu-id="a424d-391">Remote Support</span></span>

<span data-ttu-id="a424d-392">Удаленная поддержка — это [бот Microsoft Teams,](../bots/what-are-bots.md) который обеспечивает целенаправленный интерфейс между запрашивателями поддержки по всей организации и внутренней группе поддержки.</span><span class="sxs-lookup"><span data-stu-id="a424d-392">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="a424d-393">Конечные пользователи могут отправлять, редактировать или отзывать запросы на поддержку, а группа поддержки может отвечать, управлять и обновлять запросы на все запросы на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-393">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="a424d-394">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-394">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

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

## <a name="request-a-team"></a><span data-ttu-id="a424d-397">Request-a-team</span><span class="sxs-lookup"><span data-stu-id="a424d-397">Request-a-team</span></span>

<span data-ttu-id="a424d-398">Request-a-team — это приложение Microsoft Teams, которое оптимизирует создание новых групп для организации предприятия.</span><span class="sxs-lookup"><span data-stu-id="a424d-398">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="a424d-399">Приложение поддерживает стандартизацию и передовую практику при создании новых экземпляров группы с помощью интеграции формы запроса с управляемым мастером, встроенного процесса утверждения, панели мониторинга состояния запроса и создания автоматизированной группы.</span><span class="sxs-lookup"><span data-stu-id="a424d-399">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="a424d-400">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-400">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

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

## <a name="scrums-for-channels"></a><span data-ttu-id="a424d-403">Scrums для каналов</span><span class="sxs-lookup"><span data-stu-id="a424d-403">Scrums for Channels</span></span>

<span data-ttu-id="a424d-404">Scrums for Channels — это приложение-помощник scrum, которое позволяет пользователям планировать и запускать scrums в каналах в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-404">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="a424d-405">Приложение отлично подходит для удаленных групп и групп, состоящих из участников из различных географических расположений и часовых поясов, чтобы обмениваться ежедневными обновлениями и обеспечивать участие в заседаниях стендап scrum.</span><span class="sxs-lookup"><span data-stu-id="a424d-405">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="a424d-406">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-406">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="a424d-407">Для проведения собраний по scrum в групповом чате см. в нашем шаблоне [приложения Scrums for Group Chat.](#scrums-for-group-chat)</span><span class="sxs-lookup"><span data-stu-id="a424d-407">To conduct scrum meetings in a group chat, please see our [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

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

## <a name="scrums-for-group-chat"></a><span data-ttu-id="a424d-410">Scrums для группового чата</span><span class="sxs-lookup"><span data-stu-id="a424d-410">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="a424d-411">Шаблон приложения Состояния Scrums был обновлен и теперь является Scrums для группового чата.</span><span class="sxs-lookup"><span data-stu-id="a424d-411">The Scrums Status app template has been updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="a424d-412">Scrums для группового чата является вспомогательным помощником scrum, который позволяет участникам группового чата запускать асинхронные собрания и легко делиться своими ежедневными обновлениями.</span><span class="sxs-lookup"><span data-stu-id="a424d-412">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="a424d-413">Это позволяет всем участникам группового чата вносить вклад в схватку и просматривать обновления, сделанные другими пользователями в рабочей схватке.</span><span class="sxs-lookup"><span data-stu-id="a424d-413">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="a424d-414">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-414">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Scrums для демонстрации группового чата](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="a424d-416">Share Now</span><span class="sxs-lookup"><span data-stu-id="a424d-416">Share Now</span></span> 

<span data-ttu-id="a424d-417">Приложение Share Now способствует позитивному обмену информацией между коллегами, позволяя пользователям легко обмениваться контентом в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-417">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="a424d-418">Пользователи вовлекли приложение в обмен элементами, которые интересуют участников группы, обнаруживая новое общее содержимое, задав предпочтения и закладки для более позднего чтения.</span><span class="sxs-lookup"><span data-stu-id="a424d-418">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="a424d-419">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-419">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Выбор представления контента](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="a424d-421">Поиск в списке SharePoint</span><span class="sxs-lookup"><span data-stu-id="a424d-421">SharePoint List Search</span></span>

<span data-ttu-id="a424d-422">Совместная работа в Microsoft Teams часто ссылается на сведения, содержащиеся в элементов в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a424d-422">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="a424d-423">Простое вклейка ссылки на этот элемент заставляет всех переключать контекст из беседы, находить необходимые сведения, а затем возвращаться в Teams, чтобы продолжить беседу.</span><span class="sxs-lookup"><span data-stu-id="a424d-423">Simply pasting a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="a424d-424">По мере того как беседа продолжается, обычно людям придется несколько раз переключаться на справочный элемент, чтобы проверить новые комментарии и обновить свои воспоминания о сведениях, содержащихся в элементе.</span><span class="sxs-lookup"><span data-stu-id="a424d-424">As the conversation continues typically people will have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="a424d-425">Это переключение контекста создает барьер для плавного взаимодействия и является рецептом для вещей, попадающих в трещины.</span><span class="sxs-lookup"><span data-stu-id="a424d-425">This context switching creates a barrier to smooth collaboration, and is a recipe for things falling through the cracks.</span></span>

<span data-ttu-id="a424d-426">Чтобы облегчить эту боль, мы с радостью привнося вам шаблон приложения поиска списка.</span><span class="sxs-lookup"><span data-stu-id="a424d-426">To help alleviate this pain, we are happy to bring to you the List Search app template.</span></span> <span data-ttu-id="a424d-427">Миллионы пользователей используют SharePoint для питания некоторых основных процессов в своих организациях.</span><span class="sxs-lookup"><span data-stu-id="a424d-427">Millions of users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="a424d-428">Однако совместная работа со списками может быть особенно утомительной.</span><span class="sxs-lookup"><span data-stu-id="a424d-428">However, collaborating around lists can be especially tedious.</span></span> <span data-ttu-id="a424d-429">Используя шаблон приложения поиска списков в Microsoft Teams, пользователи могут вставлять сведения из элементов списка SharePoint непосредственно в чате, чтобы облегчить переключение контекста, вызванное при простом включении ссылки в чат.</span><span class="sxs-lookup"><span data-stu-id="a424d-429">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="a424d-430">Эти сведения вставляются в виде легко читаемой автоформатной карты, помогая пользователям оставаться в стороне от беседы.</span><span class="sxs-lookup"><span data-stu-id="a424d-430">The information is inserted as an easy-to-read auto-formatted card, helping your users stay engaged in the conversation.</span></span>

[<span data-ttu-id="a424d-431">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-431">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Приложение Поиска списка](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="a424d-433">Регистрация персонала</span><span class="sxs-lookup"><span data-stu-id="a424d-433">Staff Check-ins</span></span>

<span data-ttu-id="a424d-434">Регистрация сотрудников — это приложение на основе [power Apps,](/powerapps/powerapps-overview)которое позволяет контролировать связь между бизнесом и сотрудниками на местах.</span><span class="sxs-lookup"><span data-stu-id="a424d-434">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview)-based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="a424d-435">Сотрудники могут легко предоставлять критически важные для времени сведения и обновления состояния непосредственно из Teams на запланированной или разной основе.</span><span class="sxs-lookup"><span data-stu-id="a424d-435">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="a424d-436">Приложение поддерживает расположение, фотографии и заметки в режиме реального времени, а также уведомления о напоминаниях и автоматизированные процессы.</span><span class="sxs-lookup"><span data-stu-id="a424d-436">The app supports real-time location, photos, and notes as well as reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="a424d-437">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-437">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Создание представления регистрации](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="a424d-439">Опрос</span><span class="sxs-lookup"><span data-stu-id="a424d-439">Survey</span></span>

<span data-ttu-id="a424d-440">Survey — это настраиваемое приложение для расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которое позволяет создавать опрос в чате или канале для сбора данных и получения информации.</span><span class="sxs-lookup"><span data-stu-id="a424d-440">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span>  <span data-ttu-id="a424d-441">Приложение поддерживается во всех клиентах платформы Teams — настольных компьютерах, браузерах, iOS и Android — и готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="a424d-441">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="a424d-442">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-442">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Создание опроса в представлении Teams](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally"></a><span data-ttu-id="a424d-444">Время Tally</span><span class="sxs-lookup"><span data-stu-id="a424d-444">Time Tally</span></span> 

<span data-ttu-id="a424d-445">Проект может включать несколько задач, а сотрудникам могут быть назначены различные проекты.</span><span class="sxs-lookup"><span data-stu-id="a424d-445">A project can include multiple tasks, and various projects can be assigned to employees.</span></span> <span data-ttu-id="a424d-446">Руководители должны понимать ход выполнения проекта за время, затраченное сотрудниками на выполнение этих задач.</span><span class="sxs-lookup"><span data-stu-id="a424d-446">Managers are required to understand the project progress through the time spent by the employees on these tasks.</span></span> <span data-ttu-id="a424d-447">Это может быть громоздким действием, так как сотрудникам необходимо заполнить таблицы.</span><span class="sxs-lookup"><span data-stu-id="a424d-447">This can be a cumbersome activity, as the employees need to fill in the timesheets.</span></span> <span data-ttu-id="a424d-448">Приложение Time Tally позволяет сотрудникам быстро заполнять свои таблицы с помощью мобильного устройства, а руководителям не нужно следить за сотрудниками во время записи.</span><span class="sxs-lookup"><span data-stu-id="a424d-448">Time Tally app enables employees to fill their timesheets quickly, using the mobile device, and managers do not have to follow up with employees on the timesheet entry.</span></span> <span data-ttu-id="a424d-449">Руководители получают возможность просматривать использование проекта на основе ресурсов и могут утверждать или отклонить записи.</span><span class="sxs-lookup"><span data-stu-id="a424d-449">Managers get to view the project utilization based on resources, and they can approve or reject the entries.</span></span> <span data-ttu-id="a424d-450">Уведомления о напоминаниях отправляются для обеспечения соответствия времени.</span><span class="sxs-lookup"><span data-stu-id="a424d-450">Reminder notifications are sent to ensure timesheet compliance.</span></span> <span data-ttu-id="a424d-451">Кроме того, для аналитики доступны исторические данные и использование.</span><span class="sxs-lookup"><span data-stu-id="a424d-451">Also, historical data and utilizations are available for analytics.</span></span>

[<span data-ttu-id="a424d-452">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-452">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Время Tally](../assets/images/11zon_gif.gif)

## <a name="virtual-rounding"></a><span data-ttu-id="a424d-454">Виртуальное округление</span><span class="sxs-lookup"><span data-stu-id="a424d-454">Virtual Rounding</span></span>

<span data-ttu-id="a424d-455">Поставщики больничных и экстренных служб делают десятки, а зачастую и сотни **обходов** в день.</span><span class="sxs-lookup"><span data-stu-id="a424d-455">Hospital and emergency room providers make dozens, and often hundreds of **rounds** per day.</span></span> <span data-ttu-id="a424d-456">Эти быстрые проверки для пациентов предназначены для проверки состояния пациента и обеспечения решения проблем пациента.</span><span class="sxs-lookup"><span data-stu-id="a424d-456">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="a424d-457">Хотя округление является важной практикой, чтобы обеспечить наблюдение за пациентами со стороны нескольких типов поставщиков, они представляют собой огромную утечку на PPE, так как для каждого посещения, от каждого поставщика, новая маска, и новый набор перчаток должны быть использованы.</span><span class="sxs-lookup"><span data-stu-id="a424d-457">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves must be used.</span></span> <span data-ttu-id="a424d-458">С помощью этих шаблонов приложений медицинские работники могут легко проводить обходы практически через собрание Microsoft Teams между поставщиком и пациентом.</span><span class="sxs-lookup"><span data-stu-id="a424d-458">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="a424d-459">Решение виртуального округлиния также ссылается в блоге Microsoft Health and Life [Sciences.](https://aka.ms/teamsvirtualrounding)</span><span class="sxs-lookup"><span data-stu-id="a424d-459">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="a424d-460">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-460">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Виртуальное округление](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="a424d-462">Управление посетителями</span><span class="sxs-lookup"><span data-stu-id="a424d-462">Visitor Management</span></span>

<span data-ttu-id="a424d-463">Приложение Управления посетителями позволяет вашей организации и сотрудникам легко и эффективно управлять процессом посетителей на месте непосредственно из Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a424d-463">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="a424d-464">Приложение позволяет сотрудникам создавать запросы посетителей, централизованно отслеживать состояние запроса через панель мониторинга посетителей и получать уведомления в режиме реального времени при прибытии посетителя.</span><span class="sxs-lookup"><span data-stu-id="a424d-464">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="a424d-465">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-465">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

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

## <a name="workplace-awards"></a><span data-ttu-id="a424d-468">Награды на рабочем месте</span><span class="sxs-lookup"><span data-stu-id="a424d-468">Workplace Awards</span></span>

<span data-ttu-id="a424d-469">Workplace Awards — это шаблон приложений Teams, который обеспечивает положительные рамки, которые способствуют признанию и поощряют культуру оценки сотрудников на современном рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="a424d-469">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="a424d-470">Приложение позволяет настроить и управлять программой поощрения и распознавания сотрудников (R&R), в которой сотрудники могут легко назначать и поддерживать коллег, а лидер R&R может просматривать представленные номинации, гранты и объявлять получателей.</span><span class="sxs-lookup"><span data-stu-id="a424d-470">The app enables you to setup and manage an employee rewards and recognition (R&R) program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="a424d-471">Получите его в GitHub</span><span class="sxs-lookup"><span data-stu-id="a424d-471">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="a424d-472">Карточка номинации На рабочем месте</span><span class="sxs-lookup"><span data-stu-id="a424d-472">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Вкладка "Список наград на рабочем месте"](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="a424d-474">Есть идея шаблона приложения, который вы хотите увидеть?</span><span class="sxs-lookup"><span data-stu-id="a424d-474">Have an idea for an app template you'd like to see?</span></span> <span data-ttu-id="a424d-475">[Пожалуйста, дайте нам знать](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span><span class="sxs-lookup"><span data-stu-id="a424d-475">[Please let us know](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>
