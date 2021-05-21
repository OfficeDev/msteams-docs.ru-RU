---
title: Microsoft Teams шаблоны приложений
description: Ссылки и описания шаблонов приложений для Microsoft Teams платформы
ms.topic: reference
keywords: Microsoft Teams примеры демонстрации шаблонов
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
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="30fa6-104">Шаблоны приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="30fa6-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="30fa6-105">Шаблоны приложений — это примеры полных приложений для Microsoft Teams с открытым исходным кодом и доступных GitHub.</span><span class="sxs-lookup"><span data-stu-id="30fa6-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="30fa6-106">Каждый шаблон приложения содержит подробные инструкции по развертыванию и установке этого приложения для организации.</span><span class="sxs-lookup"><span data-stu-id="30fa6-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="30fa6-107">Он также предоставляет пример приложения, которое можно установить и начать использовать немедленно.</span><span class="sxs-lookup"><span data-stu-id="30fa6-107">It also provides a sample app that you can install and start using immediately.</span></span> <span data-ttu-id="30fa6-108">Кроме того, доступен полный исходный код, который позволяет подробно изучить его или раздвоить код и изменить его, чтобы соответствовать определенным требованиям.</span><span class="sxs-lookup"><span data-stu-id="30fa6-108">The complete source code is also available, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="30fa6-109">Все шаблоны приложений предоставляются в соответствии с [условиями лицензии MIT.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)</span><span class="sxs-lookup"><span data-stu-id="30fa6-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>

> [!NOTE] 
> <span data-ttu-id="30fa6-110">Необходимо лицензировать и поддерживать приложения, созданные из шаблонов приложений для пользователей и организаций.</span><span class="sxs-lookup"><span data-stu-id="30fa6-110">You must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="30fa6-111">**&#9734; указывает только что выпущенные шаблоны приложений.**</span><span class="sxs-lookup"><span data-stu-id="30fa6-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="30fa6-112">Основные преимущества</span><span class="sxs-lookup"><span data-stu-id="30fa6-112">Key benefits</span></span>

* <span data-ttu-id="30fa6-113">**Развертывание непосредственно в облаке:** Все шаблоны приложений включают сценарии развертывания, которые позволяют развертывать все необходимые службы в Microsoft Azure или на платформе Power.</span><span class="sxs-lookup"><span data-stu-id="30fa6-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="30fa6-114">**Рекомендуемый пример кода:** Шаблоны приложений соответствуют рекомендуемой рекомендации по безопасности и инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="30fa6-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="30fa6-115">Все внесенные сообществом изменения в шаблоны приложений проверяются для обеспечения соответствия.</span><span class="sxs-lookup"><span data-stu-id="30fa6-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="30fa6-116">**Настраиваемые и размязывные:** Несмотря на то, что все шаблоны приложений развернуты с минимальной конфигурацией, предоставляется вся база кода и сценарии развертывания, чтобы их можно было легко настроить или расширить, чтобы соответствовать вашим уникальным потребностям.</span><span class="sxs-lookup"><span data-stu-id="30fa6-116">**Customizable and extensible:** While all app templates are deployed with minimal configuration, the entire code base and deployment scripts are provided, so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="30fa6-117">**Подробные документы:** Все шаблоны приложений сопровождаются документацией по архитектуре решений, развертыванию и этапам конфигурации.</span><span class="sxs-lookup"><span data-stu-id="30fa6-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot"></a><span data-ttu-id="30fa6-118">Бот по внедрению</span><span class="sxs-lookup"><span data-stu-id="30fa6-118">Adoption Bot</span></span> 

<span data-ttu-id="30fa6-119">Adoption Bot — это чат-бот по уходу за пользователями, построенный с помощью виртуального агента power для Teams PVA.</span><span class="sxs-lookup"><span data-stu-id="30fa6-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams PVA.</span></span> <span data-ttu-id="30fa6-120">Он считается PVA-версией FAQ Plus.</span><span class="sxs-lookup"><span data-stu-id="30fa6-120">It is considered as the PVA version of FAQ Plus.</span></span> <span data-ttu-id="30fa6-121">Бот-принятия отвечает на более 100 общих вопросов о Microsoft 365 и Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="30fa6-122">Можно редактировать существующие темы, добавлять собственные темы и гнать существующие вопросы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-122">You can edit the existing topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="30fa6-123">Если пользователям нужна дополнительная помощь, Бот-пользователь может подключить их к экспертам или даже расширить доступ к билетам на обслуживание с соединиттелями потока премиум-класса.</span><span class="sxs-lookup"><span data-stu-id="30fa6-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.</span></span> <span data-ttu-id="30fa6-124">Этот бот самостоятельно установлен или встроен в пользовательское приложение, например концентратор [принятия.](https://github.com/akporzondek/adoption_hub)</span><span class="sxs-lookup"><span data-stu-id="30fa6-124">This bot is self-installed or built into a custom app, such as the [Adoption Hub](https://github.com/akporzondek/adoption_hub).</span></span>

[<span data-ttu-id="30fa6-125">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-125">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="adoption-tool--champion-management-platform-9734"></a><span data-ttu-id="30fa6-126">Платформа управления средствами принятия и &#9734;</span><span class="sxs-lookup"><span data-stu-id="30fa6-126">Adoption Tool- Champion Management Platform &#9734;</span></span>

<span data-ttu-id="30fa6-127">Шаблон приложения Платформы управления чемпионами (CMP) помогает управлять, масштабировать и вдохновлять чемпионов командной работы, чтобы добиться большего.</span><span class="sxs-lookup"><span data-stu-id="30fa6-127">The Champion Management Platform (CMP) app template helps you manage, scale, and inspire your teamwork champions to achieve more.</span></span> <span data-ttu-id="30fa6-128">Этот шаблон приложения строится на SharePoint Framework и загружается на вкладку в команде.</span><span class="sxs-lookup"><span data-stu-id="30fa6-128">This app template is built on the SharePoint Framework and loaded into a tab within a team.</span></span> <span data-ttu-id="30fa6-129">Группы могут использовать этот инструмент для управления членством в программе, предоставления лидеров и типов событий для ведения журнала, а также инструментов для наложения цифровых значков для участников программы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-129">Groups can leverage this tool to help manage program membership, provide a leaderboard and event types for logging, and tools to overlay digital badges to program participants.</span></span>

[<span data-ttu-id="30fa6-130">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-130">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started-9734"></a><span data-ttu-id="30fa6-131">Средства принятия Microsoft 365 (Начало работы) &#9734;</span><span class="sxs-lookup"><span data-stu-id="30fa6-131">Adoption Tool- Microsoft 365 Learning Pathways (Get Started) &#9734;</span></span>

<span data-ttu-id="30fa6-132">Шаблон Начало работы позволяет вам использовать Microsoft 365 пути обучения внутри Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-132">The Get Started app template allows you to bring the power of Microsoft 365 learning pathways inside of Microsoft Teams.</span></span> <span data-ttu-id="30fa6-133">Этот шаблон приложения позволяет легко получить доступ к определенным страницам обучения или другим активам интрасети и загрузить содержимое непосредственно в Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-133">This app template allows you to grant easy access to specific training pages or other intranet assets and load the content directly within Teams.</span></span> <span data-ttu-id="30fa6-134">Вы также можете изменить имя или логотип приложения, чтобы соответствовать брендингу вашей компании.</span><span class="sxs-lookup"><span data-stu-id="30fa6-134">You can also change the app name or logo to match your company branding.</span></span>

[<span data-ttu-id="30fa6-135">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-135">Get it on GitHub</span></span>](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="appointment-manager"></a><span data-ttu-id="30fa6-136">Менеджер по встречам</span><span class="sxs-lookup"><span data-stu-id="30fa6-136">Appointment Manager</span></span> 

<span data-ttu-id="30fa6-137">Диспетчер назначений — это шаблон Teams, который помогает предприятиям создавать, управлять и проводить виртуальные встречи с потребителями через Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-137">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="30fa6-138">Новые запросы на прием от потребителей видны в Teams каналах, где они быстро назначены и назначены сотрудникам в команде.</span><span class="sxs-lookup"><span data-stu-id="30fa6-138">New appointment requests from consumers are visible in Teams channels, where they are quickly assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="30fa6-139">Запросы на назначение рассматриваются на командном или личном уровнях с помощью настраиваемой вкладки.</span><span class="sxs-lookup"><span data-stu-id="30fa6-139">Appointment requests are viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="30fa6-140">Каждое собрание связано с Teams, поэтому сотрудники и потребители могут легко присоединиться к собранию в запланированное время.</span><span class="sxs-lookup"><span data-stu-id="30fa6-140">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="30fa6-141">Шаблон приложения интегрируется с Microsoft Bookings для простого управления назначением.</span><span class="sxs-lookup"><span data-stu-id="30fa6-141">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="30fa6-142">Запланированные встречи автоматически отображаются в календарях назначенного персонала, а потребители получают настраиваемые уведомления электронной почты и напоминания со встроенными ссылками на собрания.</span><span class="sxs-lookup"><span data-stu-id="30fa6-142">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="30fa6-143">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-143">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="30fa6-144">![Менеджер по обзору ](../assets/images/appointment-manager-overview.png)
 ![ назначений диспетчера Teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="30fa6-144">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="30fa6-145">Ask Away</span><span class="sxs-lookup"><span data-stu-id="30fa6-145">Ask Away</span></span>

<span data-ttu-id="30fa6-146">Ask Away — это [Microsoft Teams бот,](../bots/what-are-bots.md) который позволяет пользователям проводить сеансы вопросы и ответы, называемые Q&A в Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-146">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Question and Answer, called Q&A sessions within Teams.</span></span> <span data-ttu-id="30fa6-147">С помощью бота Ask Away участники группы могут отправлять и задавать вопросы до голосования, общие коллегами, что позволяет Q&A-хостов для легкого сбора вопросов в канале или чате.</span><span class="sxs-lookup"><span data-stu-id="30fa6-147">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="30fa6-148">Бот используется для проведения сеанса Q&в режиме Teams в режиме реального времени и позволяет участникам отправлять вопросы в чате.</span><span class="sxs-lookup"><span data-stu-id="30fa6-148">The bot is used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live through chat.</span></span>

[<span data-ttu-id="30fa6-149">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-149">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Просмотр всплывающее окно в таблице лидеров для голосования пользователей по вопросам](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="30fa6-151">Вспомогательная аналитика</span><span class="sxs-lookup"><span data-stu-id="30fa6-151">Associate Insights</span></span>

<span data-ttu-id="30fa6-152">Associate Insights — это [Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) который позволяет сотрудникам firstline напрямую фиксировать и отправлять мнение клиентов, настроения и восприятие.</span><span class="sxs-lookup"><span data-stu-id="30fa6-152">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="30fa6-153">Работники Firstline часто являются первым представителем компании, который может взаимодействовать с клиентами в контактной точке один к одному.</span><span class="sxs-lookup"><span data-stu-id="30fa6-153">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="30fa6-154">Собранные данные совместно используются бизнес-группами, например с помощью вкладки Power BI Teams, для улучшения продукта и улучшения взаимодействия с клиентами.</span><span class="sxs-lookup"><span data-stu-id="30fa6-154">The collected data are shared and used collaboratively by business teams, such as through a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="30fa6-155">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-155">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![Представление отзывов о созданных приложениях сведениях](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Power BI представлений о созданных приложениях](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="30fa6-158">Присутствие</span><span class="sxs-lookup"><span data-stu-id="30fa6-158">Attendance</span></span>

<span data-ttu-id="30fa6-159">Приложение Для участия — это [вкладка Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) закрепленная в команде.</span><span class="sxs-lookup"><span data-stu-id="30fa6-159">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that are pinned in a team.</span></span> <span data-ttu-id="30fa6-160">Он предназначен для записи присутствия в таких параметрах, как среды обучения и обучения.</span><span class="sxs-lookup"><span data-stu-id="30fa6-160">It is designed to record presence in settings, such as learning and training environments.</span></span> <span data-ttu-id="30fa6-161">Пользователи могут отмечать или изменять посещаемость в течение до 30 дней в прошлом и просматривать обобщенные отчеты о посещаемости для всей группы или отдельных участников.</span><span class="sxs-lookup"><span data-stu-id="30fa6-161">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span> <span data-ttu-id="30fa6-162">Дополнительные сведения о посещаемости команд см. в [GitHub.](https://github.com/OfficeDev/microsoft-teams-apps-attendance)</span><span class="sxs-lookup"><span data-stu-id="30fa6-162">For more information on teams attendance, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance).</span></span>

<span data-ttu-id="30fa6-163">На следующем изображении отображается демонстрация приложения для посещаемости:</span><span class="sxs-lookup"><span data-stu-id="30fa6-163">The following image displays the attendance app demo:</span></span>  

![Демонстрация приложения для посещаемости](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="30fa6-165">Book-a-room</span><span class="sxs-lookup"><span data-stu-id="30fa6-165">Book-a-room</span></span>

<span data-ttu-id="30fa6-166">Book-a-room — [](../bots/what-are-bots.md) это Microsoft Teams бот, который позволяет пользователям быстро находить и резервировать зал собраний на 30, 60 или 90 минут начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="30fa6-166">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="30fa6-167">Время по умолчанию — 30 минут.</span><span class="sxs-lookup"><span data-stu-id="30fa6-167">The default time is 30 minutes.</span></span> <span data-ttu-id="30fa6-168">Область бота Book-a-room для личных или 1:1 бесед.</span><span class="sxs-lookup"><span data-stu-id="30fa6-168">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="30fa6-169">Дополнительные сведения о приложении Book-a-room см. в [GitHub.](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)</span><span class="sxs-lookup"><span data-stu-id="30fa6-169">For more information on Book-a-room app, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom).</span></span>  
<span data-ttu-id="30fa6-170">На следующем изображении отображается демо Book-a-room:</span><span class="sxs-lookup"><span data-stu-id="30fa6-170">The following image displays the Book-a-room demo:</span></span>

![Демонстрация book-a-room](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="30fa6-172">Доступ к зданиям</span><span class="sxs-lookup"><span data-stu-id="30fa6-172">Building Access</span></span>

<span data-ttu-id="30fa6-173">Building Access — это приложение, основанное на платформе Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) которое поддерживает администрирование пороговых значений заполняемости зданий и норм социального расстановки, позволяя директорам объектов управлять присутствием сотрудников на месте, отслеживать и сообщать о них.</span><span class="sxs-lookup"><span data-stu-id="30fa6-173">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="30fa6-174">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview)и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams и позволяет организациям определять готовность к созданию, устанавливать критерии соответствия требованиям для доступа на сайте и собирать сведения о будущем планировании.</span><span class="sxs-lookup"><span data-stu-id="30fa6-174">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="30fa6-175">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-175">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Карта резервирования доступа к зданию](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Представление ключа "Создание доступа"](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="30fa6-178">Праздники</span><span class="sxs-lookup"><span data-stu-id="30fa6-178">Celebrations</span></span>

<span data-ttu-id="30fa6-179">Celebrations — это приложение Teams, которое помогает участникам группы отмечать дни рождения, юбилеи и другие повторяющиеся события.</span><span class="sxs-lookup"><span data-stu-id="30fa6-179">Celebrations is a Teams app that helps team members to celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="30fa6-180">Он запоминает особые случаи всех членов команды и отправляет приветственное сообщение во всех командах, выбранных во время создания событий, чтобы участники группы чувствовали себя особенными в свой день.</span><span class="sxs-lookup"><span data-stu-id="30fa6-180">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="30fa6-181">Приложение предоставляет простой интерфейс для всех членов группы, чтобы лично добавить и просмотреть свои события, а также позволяет пользователю выбрать команды, в которых события получают общий доступ.</span><span class="sxs-lookup"><span data-stu-id="30fa6-181">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="30fa6-182">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-182">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="30fa6-183">Контрольный список</span><span class="sxs-lookup"><span data-stu-id="30fa6-183">Checklist</span></span>

<span data-ttu-id="30fa6-184">Контрольный список — это [](../messaging-extensions/what-are-messaging-extensions.md) настраиваемая программа расширения Microsoft Teams обмена сообщениями, которая позволяет вам сотрудничать с командой, создавая общий контрольный список в чате или канале.</span><span class="sxs-lookup"><span data-stu-id="30fa6-184">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="30fa6-185">Приложение поддерживается во всех клиентах Teams платформы, таких как настольный браузер, iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="30fa6-185">The app is supported across all Teams platform clients, such as desktop browser, iOS, and Android.</span></span> <span data-ttu-id="30fa6-186">Приложение готово к развертыванию в рамках Microsoft 365 подписки.</span><span class="sxs-lookup"><span data-stu-id="30fa6-186">The app is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="30fa6-187">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-187">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app)

:::row:::
:::column span="2":::
    ![Создание контрольного списка в Teams представлении](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in"></a><span data-ttu-id="30fa6-189">Заехав в класс</span><span class="sxs-lookup"><span data-stu-id="30fa6-189">Classroom Drop-in</span></span> 

<span data-ttu-id="30fa6-190">В классе Drop-in — это приложение на основе платформы Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)которое позволяет руководителям систем находить группы классов, означает виртуальные классы и добавлять себя или других в эти группы класса в течение указанного периода при необходимости.</span><span class="sxs-lookup"><span data-stu-id="30fa6-190">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams, means virtual classrooms and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="30fa6-191">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview) [и Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams для обеспечения того, чтобы учебные заведения могли оптимизировать свои операции в гибридной среде обучения, предоставляя доступ к соответствующим заинтересованным сторонам для групп классов по бизнес-требованиям.</span><span class="sxs-lookup"><span data-stu-id="30fa6-191">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="30fa6-192">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-192">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Запрос на отсев класса](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="30fa6-194">Корпоративный Communicator</span><span class="sxs-lookup"><span data-stu-id="30fa6-194">Company Communicator</span></span>

<span data-ttu-id="30fa6-195">Приложение Communicator позволяет корпоративным командам создавать и отправлять сообщения, предназначенные для нескольких групп или большого числа сотрудников в чате, позволяя организации достигать сотрудников прямо там, где они сотрудничают.</span><span class="sxs-lookup"><span data-stu-id="30fa6-195">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="30fa6-196">Используйте этот шаблон для нескольких сценариев, таких как новые объявления об инициативе, учет сотрудников, современное обучение и разработка или широкомасштабные трансляции.</span><span class="sxs-lookup"><span data-stu-id="30fa6-196">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning, and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="30fa6-197">Приложение обеспечивает простой интерфейс для назначенных пользователей для создания, предварительного просмотра, совместной работы и отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="30fa6-197">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="30fa6-198">Он создает основу для создания настраиваемой целевой системы связи, например настраиваемой телеметрии, о том, сколько пользователей было признано или взаимодействует с сообщением.</span><span class="sxs-lookup"><span data-stu-id="30fa6-198">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="30fa6-199">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-199">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator составить представление окна](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="30fa6-201">Lookup контактной группы</span><span class="sxs-lookup"><span data-stu-id="30fa6-201">Contact Group Lookup</span></span>

<span data-ttu-id="30fa6-202">Приложение Lookup контактной группы предоставляет удобный и полезный подход к созданию, доступу и управлению контакт-группами организации, ранее известными как списки рассылки или группы связи.</span><span class="sxs-lookup"><span data-stu-id="30fa6-202">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups, formerly known as distribution lists or communication groups.</span></span> <span data-ttu-id="30fa6-203">Пользователи могут быстро просматривать и общаться с участниками группы, просматривать состояние участников и создавать групповой чат с выбранными участниками контактной группы, Teams среде.</span><span class="sxs-lookup"><span data-stu-id="30fa6-203">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="30fa6-204">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-204">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

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

## <a name="co-worker-appreciation"></a><span data-ttu-id="30fa6-207">Оценка сотрудников</span><span class="sxs-lookup"><span data-stu-id="30fa6-207">Co-worker Appreciation</span></span> 

<span data-ttu-id="30fa6-208">Используя шаблон оценки коллег в Microsoft Teams, пользователи могут распознавать достижения коллег в контексте Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-208">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="30fa6-209">Когда сотрудники выбирают для вознаграждения коллегу, получатели и другие члены группы помечены в разговоре на канале, и они получают уведомление о вручениях канала.</span><span class="sxs-lookup"><span data-stu-id="30fa6-209">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="30fa6-210">Награды записывают в приложении Teams, которое безопасно, портативно и легко доступно для обмена.</span><span class="sxs-lookup"><span data-stu-id="30fa6-210">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="30fa6-211">Это рассматривается как версия шаблона приложения Open Badges на основе PowerApps с таблицей лидеров.</span><span class="sxs-lookup"><span data-stu-id="30fa6-211">This is considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="30fa6-212">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-212">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![В целом](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="30fa6-214">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="30fa6-214">CrowdSourcer</span></span>

<span data-ttu-id="30fa6-215">CrowdSourcer — это [Microsoft Teams бот,](../bots/what-are-bots.md) который предоставляет группам запрашиваемую информацию, которая была совместно источником от участников группы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-215">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="30fa6-216">Это помогает отвечать на часто задамые вопросы, позволяя участникам активно участвовать и вносить вклад в интересный и полезный информационный ресурс.</span><span class="sxs-lookup"><span data-stu-id="30fa6-216">It helps to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="30fa6-217">Get it on Github</span><span class="sxs-lookup"><span data-stu-id="30fa6-217">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Взаимодействие с конечным пользователем crowdsource](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="30fa6-219">Пользовательские наклейки</span><span class="sxs-lookup"><span data-stu-id="30fa6-219">Custom Stickers</span></span>

<span data-ttu-id="30fa6-220">Самовыражение является основой здоровой культуры команды.</span><span class="sxs-lookup"><span data-stu-id="30fa6-220">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="30fa6-221">Этот шаблон приложения — это расширение [обмена](~/messaging-extensions/what-are-messaging-extensions.md) сообщениями, которое позволяет пользователям использовать настраиваемые наклейки и GIF-Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-221">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="30fa6-222">Этот шаблон предоставляет простой веб-опыт конфигурации, где любой пользователь с доступом к конфигурации может загружать GIF-изображения, giF,наклейки и изображения, которые они хотят иметь, что позволяет всей вашей команде использовать любой набор стикеров, которые вы выбираете.</span><span class="sxs-lookup"><span data-stu-id="30fa6-222">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs, stickers, and images they want their users to have, allowing your entire team to use any set of stickers you choose.</span></span>

<span data-ttu-id="30fa6-223">Это приложение также позволяет легко обмениваться изображениями, GIF-файлами, наклейками между группами без доступа к SharePoint сайтам или отдельным каналам в качестве механизмов хранения и общего доступа.</span><span class="sxs-lookup"><span data-stu-id="30fa6-223">This app also enables easy sharing of images, GIFs, stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="30fa6-224">Например, группы продуктов могут легко обмениваться изображениями продуктов и GIF-изображениями в социальных сетях, маркетинге и продажах программным образом.</span><span class="sxs-lookup"><span data-stu-id="30fa6-224">For example, product teams can easily share product images and GIFs to social media, marketing, and sales teams programmatically.</span></span> <span data-ttu-id="30fa6-225">Можно также расширить это приложение, запуская поток уведомлений для определенных групп или отдельных лиц, когда новые изображения и GIF-изображения доступны.</span><span class="sxs-lookup"><span data-stu-id="30fa6-225">One can also extend this app by triggering a notification flow to specific teams or individuals when new images, and GIFs are made available.</span></span>

[<span data-ttu-id="30fa6-226">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-226">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Приложение Стикеры](../assets/images/stickers.png)

## <a name="employee-ideas"></a><span data-ttu-id="30fa6-228">Идеи сотрудников</span><span class="sxs-lookup"><span data-stu-id="30fa6-228">Employee Ideas</span></span>

<span data-ttu-id="30fa6-229">Приложение "Идеи сотрудников" — это версия PowerApps шаблона приложения Great Ideas на основе Azure.</span><span class="sxs-lookup"><span data-stu-id="30fa6-229">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="30fa6-230">Приложение позволяет пользователям Teams настраивать идею кампании.</span><span class="sxs-lookup"><span data-stu-id="30fa6-230">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="30fa6-231">Кампания идей — это категория для группировки идей вокруг общих тем.</span><span class="sxs-lookup"><span data-stu-id="30fa6-231">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="30fa6-232">Teams пользователи также могут выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="30fa6-232">Teams users can also perform the following activities:</span></span>

* <span data-ttu-id="30fa6-233">Настройте стандартную форму отправки, которую сотрудники должны отправить для каждой идеи.</span><span class="sxs-lookup"><span data-stu-id="30fa6-233">Configure a standard submission form that employees must submit for each idea.</span></span> 
* <span data-ttu-id="30fa6-234">Просмотрите и управляйте идеями и списком кампаний.</span><span class="sxs-lookup"><span data-stu-id="30fa6-234">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="30fa6-235">Изменение и удаление кампаний.</span><span class="sxs-lookup"><span data-stu-id="30fa6-235">Modify and delete campaigns.</span></span>
* <span data-ttu-id="30fa6-236">Просмотрите советы лидеров идей.</span><span class="sxs-lookup"><span data-stu-id="30fa6-236">Review leader boards of ideas.</span></span>
* <span data-ttu-id="30fa6-237">Голосуйте за и делитесь приоритетными идеями.</span><span class="sxs-lookup"><span data-stu-id="30fa6-237">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="30fa6-238">Отправка идей для кампании.</span><span class="sxs-lookup"><span data-stu-id="30fa6-238">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="30fa6-239">Просмотр идеи другого члена группы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-239">View other team member's idea.</span></span>
* <span data-ttu-id="30fa6-240">Голосуйте за наиболее понравились идеи.</span><span class="sxs-lookup"><span data-stu-id="30fa6-240">Vote on most liked ideas.</span></span>
* <span data-ttu-id="30fa6-241">Просмотрите производительность их идей по сравнению с другими в рамках кампании.</span><span class="sxs-lookup"><span data-stu-id="30fa6-241">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="30fa6-242">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-242">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Управление представлением кампании](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="30fa6-244">Электронные рецепты</span><span class="sxs-lookup"><span data-stu-id="30fa6-244">E-Prescriptions</span></span> 

<span data-ttu-id="30fa6-245">E-Prescriptions — [](/powerapps/maker/canvas-apps/embed-teams-app) это Power Apps приложение, которое улучшает телемедицину и виртуальную помощь путем автоматизации процесса выдачи электронных рецептов пациентам.</span><span class="sxs-lookup"><span data-stu-id="30fa6-245">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="30fa6-246">Медицинские специалисты могут быстро пересматривать встречи, создавать электронные рецепты и отправлять сообщения электронной почты с вложениями по электронному рецепту пациентам непосредственно в Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="30fa6-246">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="30fa6-247">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-247">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

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

## <a name="employee-training"></a><span data-ttu-id="30fa6-252">Обучение сотрудников</span><span class="sxs-lookup"><span data-stu-id="30fa6-252">Employee Training</span></span> 

<span data-ttu-id="30fa6-253">Обучение сотрудников — это Microsoft Teams, которое позволяет организаторам легко публиковать, отслеживать и содействовать обучению и учебным мероприятиям для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="30fa6-253">Employee training is a Microsoft Teams app that enables organizers to easily publish, track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="30fa6-254">С помощью приложения организаторы событий могут отправлять напоминания и уведомления регистрантам событий, а сотрудники могут указывать на интерес к предстоящим событиям, обновлять текущие события и делиться сведениями о событиях с коллегами через расширение Teams сообщений.</span><span class="sxs-lookup"><span data-stu-id="30fa6-254">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues through the Teams messaging extension.</span></span>

[<span data-ttu-id="30fa6-255">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-255">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="30fa6-256">**Просмотр событий обучения сотрудников** ![ Изображение вкладки подготовки сотрудников](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="30fa6-256">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="30fa6-257">**Создание события подготовки сотрудников** ![ Обучение сотрудников создает форму событий](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="30fa6-257">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="30fa6-258">Эксперт finder</span><span class="sxs-lookup"><span data-stu-id="30fa6-258">Expert Finder</span></span>

<span data-ttu-id="30fa6-259">Expert Finder — это [Microsoft Teams,](../bots/what-are-bots.md) который определяет конкретных членов организации на основе их навыков, интересов и атрибутов образования.</span><span class="sxs-lookup"><span data-stu-id="30fa6-259">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="30fa6-260">Участники находят экспертов в организации, которые соответствуют поиску ключевых слов Azure Active Directory профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="30fa6-260">Members find experts within an organization that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="30fa6-261">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-261">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Демонстрация результатов поиска expert Finder](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="30fa6-263">Вопросы и ответы плюс</span><span class="sxs-lookup"><span data-stu-id="30fa6-263">FAQ Plus</span></span>

<span data-ttu-id="30fa6-264">Диалоговая&боты — это простой способ предоставления ответов на часто задамые пользователями вопросы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-264">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="30fa6-265">Но большинство ботов не могут эффективно взаимодействовать с пользователями, так как при сбойе бота в цикле нет человека.</span><span class="sxs-lookup"><span data-stu-id="30fa6-265">But, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="30fa6-266">FaQ bot — это дружественный Q&бот, который приводит человека в цикл, когда он не в состоянии помочь.</span><span class="sxs-lookup"><span data-stu-id="30fa6-266">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="30fa6-267">Можно задать боту вопрос, и бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="30fa6-267">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="30fa6-268">Если нет, бот позволяет пользователю отправлять запрос, который затем передается предварительно настроенной группе экспертов, которые помогают обеспечить поддержку, действуя на уведомления из самой группы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-268">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="30fa6-269">Последний выпуск **FAQ Plus** поддерживает улучшенные решения Q&, позволяя группе экспертов выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="30fa6-269">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="30fa6-270">&#x2714; Q&как непосредственно в базу знаний с помощью расширений сообщений.</span><span class="sxs-lookup"><span data-stu-id="30fa6-270">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="30fa6-271">&#x2714; изменить и удалить Q&пары, добавленные ботом.</span><span class="sxs-lookup"><span data-stu-id="30fa6-271">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="30fa6-272">&#x2714; отслеживание истории пересмотра Q&As.</span><span class="sxs-lookup"><span data-stu-id="30fa6-272">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="30fa6-273">&#x2714; настройка ответа с дополнительными сведениями для отображения в качестве [адаптивной карты.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="30fa6-273">&#x2714; Configure an answer with additional details to display as an [Adaptive Card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="30fa6-274">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Gif FAQ Plus](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app"></a><span data-ttu-id="30fa6-276">Получить приложение поддержки</span><span class="sxs-lookup"><span data-stu-id="30fa6-276">Get Support App</span></span>

<span data-ttu-id="30fa6-277">Приложение Get Support используется организациями, использующими Microsoft Teams, чтобы позволить любому набору пользователей запрашивать помощь у руководителей.</span><span class="sxs-lookup"><span data-stu-id="30fa6-277">The Get Support app is used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="30fa6-278">Это приложение включает следующие функции:</span><span class="sxs-lookup"><span data-stu-id="30fa6-278">This app includes the following features:</span></span>
* <span data-ttu-id="30fa6-279">Запрос помощи для разных категорий в приложении Power.</span><span class="sxs-lookup"><span data-stu-id="30fa6-279">Requesting assistance on different categories from a Power App.</span></span>
* <span data-ttu-id="30fa6-280">Уведомления, отправленные запросчикам, информирующие их о том, кому назначен заяц.</span><span class="sxs-lookup"><span data-stu-id="30fa6-280">Notifications sent to requestors informing them of who hare assigned.</span></span>
* <span data-ttu-id="30fa6-281">Уведомления, отосланные назначенному руководителю, информирующие их о том, кому нужна помощь.</span><span class="sxs-lookup"><span data-stu-id="30fa6-281">Notifications sent to assigned supervisors informing them of who needs assistance.</span></span> 
* <span data-ttu-id="30fa6-282">Анализ эскалаций и шаблонов в SharePoint и PowerBI.S.</span><span class="sxs-lookup"><span data-stu-id="30fa6-282">Analyzing escalations and patterns in SharePoint and PowerBI.S.</span></span>

[<span data-ttu-id="30fa6-283">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-283">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Get Support Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="30fa6-285">Отслеживание целей</span><span class="sxs-lookup"><span data-stu-id="30fa6-285">Goal Tracker</span></span>

<span data-ttu-id="30fa6-286">Приложение Goal Tracker — это комплексное решение для организации, которое поддерживает установление целей, наблюдение за прогрессом и признание успеха в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-286">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="30fa6-287">Приложение позволяет пользователям устанавливать, отслеживать и обновлять цели на профессиональном, личном и командном уровне.</span><span class="sxs-lookup"><span data-stu-id="30fa6-287">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="30fa6-288">Члены группы также получают вовремя напоминания и обновления состояния, чтобы оставаться сосредоточенными и оставаться в курсе.</span><span class="sxs-lookup"><span data-stu-id="30fa6-288">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="30fa6-289">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-289">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

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

## <a name="great-ideas"></a><span data-ttu-id="30fa6-292">Великие идеи</span><span class="sxs-lookup"><span data-stu-id="30fa6-292">Great Ideas</span></span>

<span data-ttu-id="30fa6-293">Приложение Great Ideas поддерживает и расширяет возможности инноваций и творчества в организации.</span><span class="sxs-lookup"><span data-stu-id="30fa6-293">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="30fa6-294">Приложение позволяет сотрудникам обмениваться идеями с коллегами и руководством, обнаруживая новые материалы, вклады внимания для одноранговой оценки и голосуя за лучшие предложения в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-294">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="30fa6-295">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-295">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a><span data-ttu-id="30fa6-298">Групповые действия</span><span class="sxs-lookup"><span data-stu-id="30fa6-298">Group Activities</span></span>

<span data-ttu-id="30fa6-299">Group Activities — это Microsoft Teams приложение, которое позволяет владельцам групп быстро создавать группы действий и управлять рабочими процессами совместной работы в контексте Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-299">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="30fa6-300">Авторы действий могут создавать действия, случайным образом распределять членов группы по группам и необязательно отправлять напоминания боту до завершения действий.</span><span class="sxs-lookup"><span data-stu-id="30fa6-300">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="30fa6-301">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-301">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

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

## <a name="group-connect-9734"></a><span data-ttu-id="30fa6-304">Групповой Подключение &#9734;</span><span class="sxs-lookup"><span data-stu-id="30fa6-304">Group Connect &#9734;</span></span>

<span data-ttu-id="30fa6-305">Group Подключение — это Microsoft Teams, которое помогает участникам организации находить группы сотрудников и находить сведения, соответствующие группам сотрудников.</span><span class="sxs-lookup"><span data-stu-id="30fa6-305">Group Connect is a Microsoft Teams app that helps organization members discover employee groups and find information relevant to employee groups.</span></span> <span data-ttu-id="30fa6-306">Приложение встроено с богатыми возможностями для руководителей организаций для общения со своими сотрудниками в отношении групп, событий и ресурсов.</span><span class="sxs-lookup"><span data-stu-id="30fa6-306">The app comes built-in with rich capabilities for organization leaders to communicate with their employees regarding groups, events, and resources.</span></span> <span data-ttu-id="30fa6-307">Приложение Group Подключение также совпадает с участниками группы на их нужной частоте, чтобы стимулировать сетевое взаимодействие и сплоченность в группе.</span><span class="sxs-lookup"><span data-stu-id="30fa6-307">The Group Connect app also matches group members with each other at their desired frequency to encourage networking and cohesion within a group.</span></span> <span data-ttu-id="30fa6-308">Дополнительные сведения о том, как использовать приложение Group Подключение, чтобы помочь группам сотрудников развиваться в организации, см. в GitHub.</span><span class="sxs-lookup"><span data-stu-id="30fa6-308">For more information on how you can leverage the Group Connect app to help employee groups foster within your organization, see the app on GitHub.</span></span>

[<span data-ttu-id="30fa6-309">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-309">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupconnect)

![Обнаружение групп D&I](https://github.com/OfficeDev/microsoft-teams-apps-diversityandinclusion/wiki/Images/temp_group_connect_landing.png)

## <a name="grow-your-skills"></a><span data-ttu-id="30fa6-311">Вырастите свои навыки</span><span class="sxs-lookup"><span data-stu-id="30fa6-311">Grow Your Skills</span></span>

<span data-ttu-id="30fa6-312">Приложение Grow Your Skills поддерживает профессиональный рост и развитие, позволяя сотрудникам вносить вклад в дополнительные проекты для вашей организации, одновременно изучая новые навыки.</span><span class="sxs-lookup"><span data-stu-id="30fa6-312">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="30fa6-313">Сотрудники могут использовать приложение для поиска возможностей, которые отвечают их интересам, эффективного взаимодействия с коллегами и приобретения новых уровней знаний и возможностей в Teams среде.</span><span class="sxs-lookup"><span data-stu-id="30fa6-313">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="30fa6-314">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-314">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

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

## <a name="hr-support"></a><span data-ttu-id="30fa6-317">Поддержка управления персоналом</span><span class="sxs-lookup"><span data-stu-id="30fa6-317">HR Support</span></span>

<span data-ttu-id="30fa6-318">Бот поддержки кадров — это дружественный Q&бот, который привозит специалиста или специалиста по поддержке из группы hr в цикл, когда он не может помочь.</span><span class="sxs-lookup"><span data-stu-id="30fa6-318">HR Support bot is a friendly Q&A bot that brings a support professional or expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="30fa6-319">Можно задать боту вопрос, и бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="30fa6-319">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="30fa6-320">Если нет, бот позволяет пользователю отправить запрос, который затем будет размещен в предварительно настроенной группе экспертов, которые помогают оказывать поддержку, действуя на уведомления из самой команды.</span><span class="sxs-lookup"><span data-stu-id="30fa6-320">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="30fa6-321">Кроме того, бот предлагает ссылки на рекомендуемые политики кадров или вопросы, ища предварительно настроенные теги в этом вопросе.</span><span class="sxs-lookup"><span data-stu-id="30fa6-321">Additionally, the bot suggests links to recommended HR policies or questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="30fa6-322">Эти плитки находятся на связанной вкладке в качестве быстрой ссылки.</span><span class="sxs-lookup"><span data-stu-id="30fa6-322">These tiles are found in the associated tab as a quick reference.</span></span> <span data-ttu-id="30fa6-323">Поддержка отдела кадров хорошо работает для&Q&A и обеспечивает быструю поддержку при запуске новых проектов или инициатив в организации.</span><span class="sxs-lookup"><span data-stu-id="30fa6-323">HR Support works well for light weight Q&A and to provide quick support when launching new projects or initiatives in the organization.</span></span>

[<span data-ttu-id="30fa6-324">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-324">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Поддержка управления персоналом](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="30fa6-326">Точки соприкосновения</span><span class="sxs-lookup"><span data-stu-id="30fa6-326">Icebreaker</span></span>

<span data-ttu-id="30fa6-327">Icebreaker — это [Microsoft Teams,](../bots/what-are-bots.md) который помогает вашей команде приблизиться, спарив двух случайных членов команды каждую неделю для встречи.</span><span class="sxs-lookup"><span data-stu-id="30fa6-327">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="30fa6-328">Бот упрощает планирование, автоматически предлагая свободное время, которое работает для обоих участников.</span><span class="sxs-lookup"><span data-stu-id="30fa6-328">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="30fa6-329">Укрепляйте личные связи и создайте тесное сообщество с помощью этого приложения.</span><span class="sxs-lookup"><span data-stu-id="30fa6-329">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="30fa6-330">Помимо поощрения личных подключений всей вашей команды, приложение Icebreaker может помочь развивать сообщества, основанные на интересах вашей организации.</span><span class="sxs-lookup"><span data-stu-id="30fa6-330">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="30fa6-331">Например, это приложение можно использовать для группы DevOps, чтобы помочь идеям и лучшим практикам органично распространяться по всей организации.</span><span class="sxs-lookup"><span data-stu-id="30fa6-331">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="30fa6-332">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-332">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Приложение Icebreaker](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="30fa6-334">Стимулы</span><span class="sxs-lookup"><span data-stu-id="30fa6-334">Incentives</span></span>

<span data-ttu-id="30fa6-335">Стимулы — это шаблон [Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) который управляет и отслеживает стимулирование участия сотрудников в назначенных мероприятиях, таких как тренинги и инициативы по управлению изменениями.</span><span class="sxs-lookup"><span data-stu-id="30fa6-335">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities, such as trainings and change management initiatives.</span></span> <span data-ttu-id="30fa6-336">Администраторы используют приложение для создания назначенных действий, назначения точек для завершения и указания необходимых уровней точки права на вознаграждение.</span><span class="sxs-lookup"><span data-stu-id="30fa6-336">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="30fa6-337">Сотрудники используют приложение для просмотра накопленных баллов и по достижении допустимости запрашивать и требовать выкупаемых вознаграждений.</span><span class="sxs-lookup"><span data-stu-id="30fa6-337">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="30fa6-338">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-338">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Демонстрация приложения incentives](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="30fa6-340">Репортер инцидентов</span><span class="sxs-lookup"><span data-stu-id="30fa6-340">Incident Reporter</span></span>

<span data-ttu-id="30fa6-341">Incident Reporter — это [Microsoft Teams бот,](../bots/what-are-bots.md) который оптимизирует управление инцидентами в организации.</span><span class="sxs-lookup"><span data-stu-id="30fa6-341">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="30fa6-342">Бот упрощает автоматизированный сбор данных об инцидентах, настраиваемые отчеты об инцидентах, соответствующие уведомления заинтересованных лиц и отслеживание инцидентов в конце концов.</span><span class="sxs-lookup"><span data-stu-id="30fa6-342">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="30fa6-343">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-343">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

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

## <a name="inspection"></a><span data-ttu-id="30fa6-346">Проверка</span><span class="sxs-lookup"><span data-stu-id="30fa6-346">Inspection</span></span> 

 <span data-ttu-id="30fa6-347">Inspection — это Microsoft Teams приложение, которое позволяет сотрудникам первой линии проверять все, что угодно от расположения до активов и оборудования.</span><span class="sxs-lookup"><span data-stu-id="30fa6-347">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="30fa6-348">Например, розничный магазин, завод по производству или транспортные средства и машины.</span><span class="sxs-lookup"><span data-stu-id="30fa6-348">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="30fa6-349">В этом решении есть два приложения, каждое из которых предназначено для разных типов пользователей.</span><span class="sxs-lookup"><span data-stu-id="30fa6-349">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="30fa6-350">Приложение предоставляет сотрудникам передней линии возможность проверять актив или область, управлять качеством продуктов и услуг или поддерживать безопасность на рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="30fa6-350">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="30fa6-351">Это облегчает связь между членами группы для решения проблем, найденных во время проверки.</span><span class="sxs-lookup"><span data-stu-id="30fa6-351">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="30fa6-352">Приложение предоставляет простые отчеты для руководителей, чтобы ускорить решение проблем и выделить тенденции.</span><span class="sxs-lookup"><span data-stu-id="30fa6-352">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="30fa6-353">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Обзор инспекции](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a><span data-ttu-id="30fa6-355">Отчеты о проблемах</span><span class="sxs-lookup"><span data-stu-id="30fa6-355">Issue Reporting</span></span>

<span data-ttu-id="30fa6-356">Приложение Отчеты о проблемах позволяет сотрудникам и руководителям поднимать и управлять вопросами.</span><span class="sxs-lookup"><span data-stu-id="30fa6-356">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="30fa6-357">Она состоит из двух приложений: приложения для отчетов о проблемах и приложения "Управление вопросами" для управления вопросами.</span><span class="sxs-lookup"><span data-stu-id="30fa6-357">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="30fa6-358">Руководители группы используют приложение Manage Issues для настройки приложения, в том числе канала, в котором Microsoft Teams сообщений и задач планировщика, созданных приложением.</span><span class="sxs-lookup"><span data-stu-id="30fa6-358">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="30fa6-359">Менеджеры также используют приложение для создания форм шаблонов для сбора сведений, когда пользователь сообщает о проблеме.</span><span class="sxs-lookup"><span data-stu-id="30fa6-359">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="30fa6-360">Например, просмотрите, отредактируете или удалите формы шаблона проблем.</span><span class="sxs-lookup"><span data-stu-id="30fa6-360">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="30fa6-361">Приложение также используется для проверки проблем группы, отчета об истории проблем и эффективного управления решением проблем.</span><span class="sxs-lookup"><span data-stu-id="30fa6-361">The app is also used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="30fa6-362">Сотрудники используют приложение отчетов о проблемах для журналов проблем и сведений, необходимых для их устранения.</span><span class="sxs-lookup"><span data-stu-id="30fa6-362">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="30fa6-363">Приложение также используется для изменения и решения существующих проблем и получения высокого уровня представления об отдельных или командных проблемах.</span><span class="sxs-lookup"><span data-stu-id="30fa6-363">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="30fa6-364">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Представление группы отчетов о проблемах](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="30fa6-366">Новые возможности для сотрудников</span><span class="sxs-lookup"><span data-stu-id="30fa6-366">New Employee Onboarding</span></span> 

<span data-ttu-id="30fa6-367">Новая интеграция сотрудников — это интегрированное решение Microsoft Teams [и SharePoint](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) для новых сотрудников, которое позволяет вашей организации предоставлять сотрудникам последовательную и качественную интеграцию во время их нового путешествия по службе.</span><span class="sxs-lookup"><span data-stu-id="30fa6-367">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="30fa6-368">Приложение используется группами кадров и менеджерами по найму для предоставления соответствующих сведений в процессе ориентации и индукции, а также для обмена отзывами, предоставления представлений и выполнения задач бортового ввода.</span><span class="sxs-lookup"><span data-stu-id="30fa6-368">The app is used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="30fa6-369">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-369">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="30fa6-370">**Новая приветствие сотрудника** ![ Изображение новой приветствия сотрудника](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="30fa6-370">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="30fa6-371">**Новый контрольный список сотрудников** ![ Изображение нового контрольного списка сотрудников](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="30fa6-371">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="30fa6-372">Открыть значки</span><span class="sxs-lookup"><span data-stu-id="30fa6-372">Open Badges</span></span>

<span data-ttu-id="30fa6-373">Open Badges — это Microsoft Teams, которое позволяет пользователям получать цифровые значки учетных данных для обучения в контексте Teams и делиться ими во всем мире.</span><span class="sxs-lookup"><span data-stu-id="30fa6-373">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="30fa6-374">Использование возможностей сторонних органов по выдаче цифровых значков [Badgr](https://badgr.org/), отмеченных значками, записывается в профиле Badgr получателя и доступно для создания и обмена богатой картиной путешествий по обучению в течение всей жизни.</span><span class="sxs-lookup"><span data-stu-id="30fa6-374">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="30fa6-375">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

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

## <a name="poll"></a><span data-ttu-id="30fa6-378">Опрос</span><span class="sxs-lookup"><span data-stu-id="30fa6-378">Poll</span></span> 

<span data-ttu-id="30fa6-379">Poll — это настраиваемая программа расширения Microsoft Teams обмена сообщениями, которая позволяет быстро создавать и отправлять опросы в чате или канале для сбора мнений и предпочтений группы. [](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="30fa6-379">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="30fa6-380">Приложение поддерживается во всех Teams платформах, таких как настольный компьютер, браузер, iOS и Android, и готово к развертыванию в рамках Microsoft 365 подписки.</span><span class="sxs-lookup"><span data-stu-id="30fa6-380">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="30fa6-381">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-381">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Создание опроса в Teams представлении](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="30fa6-383">Быстрые ответы</span><span class="sxs-lookup"><span data-stu-id="30fa6-383">Quick Responses</span></span>

<span data-ttu-id="30fa6-384">Quick Responses — это Microsoft Teams приложение, которое предоставляет надежное решение для эффективного ответа на часто задаваемые вопросы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-384">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions FAQs.</span></span> <span data-ttu-id="30fa6-385">Вместо того, чтобы отвечать на каждый запрос вручную и непрерывно повторять информацию, приложение создает библиотеку ответов для интерактивного пользовательского интерфейса с помощью Teams [расширений обмена сообщениями.](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="30fa6-385">Instead of answering each query manually and continuously repeating information, the app builds a library of responses for an interactive user experience through Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="30fa6-386">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-386">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Пример представления ответов](../assets/images/quick-responses.png)

## <a name="quiz--9734"></a><span data-ttu-id="30fa6-388">Тест &#9734;</span><span class="sxs-lookup"><span data-stu-id="30fa6-388">Quiz  &#9734;</span></span>

<span data-ttu-id="30fa6-389">Quiz — это настраиваемая [Teams](../messaging-extensions/what-are-messaging-extensions.md) приложение для расширения обмена сообщениями, которое позволяет создавать викторину в чате или канале проверки знаний и мгновенных результатов.</span><span class="sxs-lookup"><span data-stu-id="30fa6-389">Quiz is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a quiz within a chat or a channel for knowledge check and instantaneous results.</span></span> <span data-ttu-id="30fa6-390">Вы можете использовать тесты для экзаменов в классе и автономном режиме, проверку знаний в команде и забавные викторины в команде.</span><span class="sxs-lookup"><span data-stu-id="30fa6-390">You can use Quiz for, In-class and offline exams, Knowledge check within team, and for fun quizzes within a team.</span></span> <span data-ttu-id="30fa6-391">Приложение викторины поддерживается на нескольких платформах, таких как Teams, браузер, iOS и Android-клиенты.</span><span class="sxs-lookup"><span data-stu-id="30fa6-391">Quiz app is supported across multiple platforms, such as Teams desktop, browser, iOS, and Android clients.</span></span> <span data-ttu-id="30fa6-392">Это приложение готово к развертыванию в рамках существующей Microsoft 365 подписки.</span><span class="sxs-lookup"><span data-stu-id="30fa6-392">This app is ready for deployment as part of your existing Microsoft 365 subscription.</span></span>

[<span data-ttu-id="30fa6-393">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-393">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quiz)

:::row:::
  :::column span="1":::
    ![Создание викторины в Teams представлении](../assets/images/quiz-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="rapid-assist"></a><span data-ttu-id="30fa6-395">Rapid Assist</span><span class="sxs-lookup"><span data-stu-id="30fa6-395">Rapid Assist</span></span>

<span data-ttu-id="30fa6-396">Rapid Assist — это приложение, основанное на платформе Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) которое позволяет партнерам с клиентами быстро подключаться к экспертам, получать быстрые ответы, искать информацию, выполнять открытые запросы и получать уведомления, чтобы быстро получить вызов, чтобы помочь ответить на вопросы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-396">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="30fa6-397">Приложение, построенное [](/powerapps/powerapps-overview) с Power Apps и [Power Automate](/power-automate/getting-started)Microsoft, глубоко интегрируется с Microsoft Teams, чтобы организации могли легко подключать сотрудников frontline с корпоративными связями для решения запросов клиентов и предоставления отличного обслуживания клиентов.</span><span class="sxs-lookup"><span data-stu-id="30fa6-397">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="30fa6-398">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-398">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Интерфейс запроса конечных пользователей](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Представление запроса эксперта](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="30fa6-401">Отражение</span><span class="sxs-lookup"><span data-stu-id="30fa6-401">Reflect</span></span> 

<span data-ttu-id="30fa6-402">Reflect — это настраиваемая программа расширения Microsoft Teams обмена сообщениями, которая предоставляет безопасный и инклюзивный ресурс для членов вашей команды, чтобы поделиться состоянием своего эмоционального благополучия с коллегами или руководителями групп непосредственно в Teams. [](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="30fa6-402">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues or group leaders directly within Teams.</span></span> <span data-ttu-id="30fa6-403">Приложение доступно в чатах каналов, групп, собраний и 1:1, а ответ на регистрацию устанавливается для общедоступных, частных и полностью анонимных.</span><span class="sxs-lookup"><span data-stu-id="30fa6-403">The app is available in channel, group, meeting, and 1:1 chats and the check-in response is set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="30fa6-404">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-404">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="30fa6-405">**Опрос благополучия**</span><span class="sxs-lookup"><span data-stu-id="30fa6-405">**Well-being poll**</span></span>
    
    ![Отражение опроса пользователей приложения](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="30fa6-407">Удаленная поддержка</span><span class="sxs-lookup"><span data-stu-id="30fa6-407">Remote Support</span></span>

<span data-ttu-id="30fa6-408">Remote Support — это [Microsoft Teams бот,](../bots/what-are-bots.md) который обеспечивает целенаправленный интерфейс между запрашивателями поддержки по всей организации и внутренней группе поддержки.</span><span class="sxs-lookup"><span data-stu-id="30fa6-408">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="30fa6-409">Конечные пользователи могут отправлять, редактировать или отзывать запросы на поддержку, а группа поддержки может отвечать, управлять и обновлять запросы в Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="30fa6-409">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="30fa6-410">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-410">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

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

## <a name="request-a-team"></a><span data-ttu-id="30fa6-413">Request-a-team</span><span class="sxs-lookup"><span data-stu-id="30fa6-413">Request-a-team</span></span>

<span data-ttu-id="30fa6-414">Request-a-team — это приложение Microsoft Teams которое оптимизирует создание новых команд для организации предприятия.</span><span class="sxs-lookup"><span data-stu-id="30fa6-414">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="30fa6-415">Приложение поддерживает стандартизацию и передовую практику при создании новых экземпляров группы с помощью интеграции формы запроса с управляемым мастером, встроенного процесса утверждения, панели мониторинга состояния запроса и создания автоматизированной группы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-415">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="30fa6-416">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-416">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

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

## <a name="scrums-for-channels"></a><span data-ttu-id="30fa6-419">Scrums для каналов</span><span class="sxs-lookup"><span data-stu-id="30fa6-419">Scrums for Channels</span></span>

<span data-ttu-id="30fa6-420">Scrums for Channels — это приложение-помощник scrum, которое позволяет пользователям планировать и запускать scrums в каналах в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-420">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="30fa6-421">Приложение отлично подходит для удаленных групп и групп, состоящих из участников из различных географических расположений и часовых поясов, чтобы обмениваться ежедневными обновлениями и обеспечивать участие в заседаниях стендап scrum.</span><span class="sxs-lookup"><span data-stu-id="30fa6-421">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="30fa6-422">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-422">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="30fa6-423">Для проведения собраний по scrum в групповом чате см. [шаблон приложения Scrums for Group Chat.](#scrums-for-group-chat)</span><span class="sxs-lookup"><span data-stu-id="30fa6-423">To conduct scrum meetings in a group chat, see [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

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

## <a name="scrums-for-group-chat"></a><span data-ttu-id="30fa6-426">Scrums для группового чата</span><span class="sxs-lookup"><span data-stu-id="30fa6-426">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="30fa6-427">Шаблон приложения Состояния Scrums обновляется и теперь является Scrums для группового чата.</span><span class="sxs-lookup"><span data-stu-id="30fa6-427">The Scrums Status app template is updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="30fa6-428">Scrums для группового чата является вспомогательным помощником scrum, который позволяет участникам группового чата запускать асинхронные собрания и легко делиться своими ежедневными обновлениями.</span><span class="sxs-lookup"><span data-stu-id="30fa6-428">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="30fa6-429">Это позволяет всем участникам группового чата вносить вклад в схватку и просматривать обновления, сделанные другими пользователями в рабочей схватке.</span><span class="sxs-lookup"><span data-stu-id="30fa6-429">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="30fa6-430">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-430">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Scrums для демонстрации группового чата](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="30fa6-432">Share Now</span><span class="sxs-lookup"><span data-stu-id="30fa6-432">Share Now</span></span> 

<span data-ttu-id="30fa6-433">Приложение Share Now способствует позитивному обмену информацией между коллегами, позволяя пользователям легко обмениваться контентом в Teams среде.</span><span class="sxs-lookup"><span data-stu-id="30fa6-433">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="30fa6-434">Пользователи вовлекли приложение в обмен элементами, которые интересуют участников группы, обнаруживая новое общее содержимое, задав предпочтения и закладки для более позднего чтения.</span><span class="sxs-lookup"><span data-stu-id="30fa6-434">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="30fa6-435">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-435">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Выбор представления контента](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="30fa6-437">Поиск в списке SharePoint</span><span class="sxs-lookup"><span data-stu-id="30fa6-437">SharePoint List Search</span></span>

<span data-ttu-id="30fa6-438">Совместная Microsoft Teams часто ссылается на сведения, содержащиеся в элементов в SharePoint списке.</span><span class="sxs-lookup"><span data-stu-id="30fa6-438">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="30fa6-439">Вклей ссылку на этот элемент заставляет всех переключать контекст из беседы, находить необходимые сведения, а затем возвращаться Teams для продолжения беседы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-439">Paste a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="30fa6-440">По мере того как беседа продолжается, люди должны несколько раз переключаться на справочный элемент, чтобы проверить новые комментарии и обновить воспоминания о сведениях, содержащихся в элементе.</span><span class="sxs-lookup"><span data-stu-id="30fa6-440">As the conversation continues  people have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="30fa6-441">Это переключение контекста создает барьер для плавного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="30fa6-441">This context switching creates a barrier to smooth collaboration.</span></span>
<span data-ttu-id="30fa6-442">Для решения этой проблемы используется шаблон приложения поиска списков.</span><span class="sxs-lookup"><span data-stu-id="30fa6-442">To resolve this problem, the List Search app template is used.</span></span> <span data-ttu-id="30fa6-443">Многие пользователи используют SharePoint для питания некоторых основных процессов в своих организациях.</span><span class="sxs-lookup"><span data-stu-id="30fa6-443">Many users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="30fa6-444">Однако совместная работа со списками затруднена.</span><span class="sxs-lookup"><span data-stu-id="30fa6-444">However, collaborating around lists is difficult.</span></span> <span data-ttu-id="30fa6-445">Используя шаблон приложения поиска списка в Microsoft Teams, пользователи могут вставлять сведения из SharePoint элементов списка непосредственно в чате, чтобы облегчить переключение контекста, вызванное при простом включении ссылки в чат.</span><span class="sxs-lookup"><span data-stu-id="30fa6-445">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="30fa6-446">Эти сведения вставляются в виде легко читаемой автоформатной карты, помогая пользователям оставаться в стороне от беседы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-446">The information is inserted as an easy-to-read auto-formatted card, helping the users stay engaged in the conversation.</span></span>

[<span data-ttu-id="30fa6-447">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-447">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Приложение Поиска списка](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="30fa6-449">Регистрация персонала</span><span class="sxs-lookup"><span data-stu-id="30fa6-449">Staff Check-ins</span></span>

<span data-ttu-id="30fa6-450">Регистрация персонала — это приложение [на](/powerapps/powerapps-overview) Power Apps, которое позволяет контролировать связь между бизнесом и персоналом на местах.</span><span class="sxs-lookup"><span data-stu-id="30fa6-450">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview) based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="30fa6-451">Сотрудники могут легко предоставлять критически важные для времени сведения и обновления состояния непосредственно из Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-451">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="30fa6-452">Приложение поддерживает расположение в режиме реального времени, фотографии, заметки, уведомления о напоминаниях и автоматизированные процессы работы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-452">The app supports real-time location, photos, notes, reminder notifications, and automated workflows.</span></span>

[<span data-ttu-id="30fa6-453">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-453">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Создание представления регистрации](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="30fa6-455">Опрос</span><span class="sxs-lookup"><span data-stu-id="30fa6-455">Survey</span></span>

<span data-ttu-id="30fa6-456">Survey — это настраиваемое приложение Microsoft Teams для расширения обмена сообщениями, которое позволяет создавать опрос в чате или канале для сбора данных и получения информации. [](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="30fa6-456">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span> <span data-ttu-id="30fa6-457">Приложение поддерживается во всех Teams платформах, таких как настольный компьютер, браузер, iOS и Android, и готово к развертыванию в рамках Microsoft 365 подписки.</span><span class="sxs-lookup"><span data-stu-id="30fa6-457">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="30fa6-458">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-458">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Создание опроса в Teams представлении](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally"></a><span data-ttu-id="30fa6-460">Время Tally</span><span class="sxs-lookup"><span data-stu-id="30fa6-460">Time Tally</span></span> 

<span data-ttu-id="30fa6-461">Проект может включать несколько задач, а сотрудникам могут быть назначены различные проекты.</span><span class="sxs-lookup"><span data-stu-id="30fa6-461">A project can include multiple tasks, and various projects can be assigned to employees.</span></span> <span data-ttu-id="30fa6-462">Руководители должны понимать ход выполнения проекта за время, затраченное сотрудниками на выполнение этих задач.</span><span class="sxs-lookup"><span data-stu-id="30fa6-462">Managers are required to understand the project progress through the time spent by the employees on these tasks.</span></span> <span data-ttu-id="30fa6-463">Это может быть громоздким действием, так как сотрудникам необходимо заполнить таблицы.</span><span class="sxs-lookup"><span data-stu-id="30fa6-463">This can be a cumbersome activity, as the employees need to fill in the timesheets.</span></span> <span data-ttu-id="30fa6-464">Приложение Time Tally позволяет сотрудникам быстро заполнять свои таблицы с помощью мобильного устройства, а руководителям не нужно следить за сотрудниками во время записи.</span><span class="sxs-lookup"><span data-stu-id="30fa6-464">Time Tally app enables employees to fill their timesheets quickly, using the mobile device, and managers do not have to follow up with employees on the timesheet entry.</span></span> <span data-ttu-id="30fa6-465">Руководители получают возможность просматривать использование проекта на основе ресурсов и могут утверждать или отклонить записи.</span><span class="sxs-lookup"><span data-stu-id="30fa6-465">Managers get to view the project utilization based on resources, and they can approve or reject the entries.</span></span> <span data-ttu-id="30fa6-466">Уведомления о напоминаниях отправляются для обеспечения соответствия времени.</span><span class="sxs-lookup"><span data-stu-id="30fa6-466">Reminder notifications are sent to ensure timesheet compliance.</span></span> <span data-ttu-id="30fa6-467">Кроме того, для аналитики доступны исторические данные и использование.</span><span class="sxs-lookup"><span data-stu-id="30fa6-467">Also, historical data and utilizations are available for analytics.</span></span>

[<span data-ttu-id="30fa6-468">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-468">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Время Tally](../assets/images/11zon_gif.gif)

## <a name="training--9734"></a><span data-ttu-id="30fa6-470">Обучение &#9734;</span><span class="sxs-lookup"><span data-stu-id="30fa6-470">Training  &#9734;</span></span>

<span data-ttu-id="30fa6-471">Обучение — это настраиваемая программа расширения [Teams](../messaging-extensions/what-are-messaging-extensions.md) обмена сообщениями, которая позволяет пользователям публиковать обучение в чате или канале для автономного обмена знаниями и upskilling.</span><span class="sxs-lookup"><span data-stu-id="30fa6-471">Training is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables users to publish a training within a chat or a channel for offline knowledge sharing and upskilling.</span></span> <span data-ttu-id="30fa6-472">Приложение поддерживается несколькими Teams платформами, такими как настольный компьютер, браузер, iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="30fa6-472">The app is supported across multiple Teams platform clients, such as desktop, browser, iOS, and Android.</span></span> <span data-ttu-id="30fa6-473">Это приложение готово к развертыванию в рамках Microsoft 365 подписки.</span><span class="sxs-lookup"><span data-stu-id="30fa6-473">This app is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="30fa6-474">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-474">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-training)

:::row:::
  :::column span="1":::
    ![Создание обучения в Teams представлении](../assets/images/training-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="virtual-rounding"></a><span data-ttu-id="30fa6-476">Виртуальное округление</span><span class="sxs-lookup"><span data-stu-id="30fa6-476">Virtual Rounding</span></span>

<span data-ttu-id="30fa6-477">Поставщики больничных и экстренных служб делают много **обходов** в день.</span><span class="sxs-lookup"><span data-stu-id="30fa6-477">Hospital and emergency room providers make many **rounds** per day.</span></span> <span data-ttu-id="30fa6-478">Эти быстрые проверки для пациентов предназначены для проверки состояния пациента и обеспечения решения проблем пациента.</span><span class="sxs-lookup"><span data-stu-id="30fa6-478">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="30fa6-479">Хотя округление является важной практикой для обеспечения контроля за пациентами несколькими типами поставщиков, они представляют собой огромную утечку на PPE, так как для каждого посещения, от каждого поставщика, новая маска и новый набор перчаток используются.</span><span class="sxs-lookup"><span data-stu-id="30fa6-479">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves are used.</span></span> <span data-ttu-id="30fa6-480">С помощью этих шаблонов приложений медицинские работники могут легко проводить обходы виртуально, Microsoft Teams встречу между поставщиком и пациентом.</span><span class="sxs-lookup"><span data-stu-id="30fa6-480">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="30fa6-481">Решение виртуального округлиния также ссылается в блоге Microsoft Health и Life [Sciences.](https://aka.ms/teamsvirtualrounding)</span><span class="sxs-lookup"><span data-stu-id="30fa6-481">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="30fa6-482">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-482">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Виртуальное округление](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="30fa6-484">Управление посетителями</span><span class="sxs-lookup"><span data-stu-id="30fa6-484">Visitor Management</span></span>

<span data-ttu-id="30fa6-485">Приложение Управления посетителями позволяет вашей организации и сотрудникам легко и эффективно управлять процессом посетителей на месте непосредственно из Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="30fa6-485">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="30fa6-486">Приложение позволяет сотрудникам создавать запросы посетителей, централизованно отслеживать состояние запроса через панель мониторинга посетителей и получать уведомления в режиме реального времени при прибытии посетителя.</span><span class="sxs-lookup"><span data-stu-id="30fa6-486">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="30fa6-487">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-487">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

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

## <a name="workplace-awards"></a><span data-ttu-id="30fa6-490">Награды на рабочем месте</span><span class="sxs-lookup"><span data-stu-id="30fa6-490">Workplace Awards</span></span>

<span data-ttu-id="30fa6-491">Workplace Awards — это шаблон Teams, который обеспечивает положительные рамки, которые способствуют признанию и развитию культуры оценки сотрудников на современном рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="30fa6-491">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="30fa6-492">Приложение позволяет настроить и управлять наградами и распознаванием сотрудников под названием R&R, где сотрудники могут легко назначать и поддерживать коллег, а лидер R&R может просматривать представленные номинации, гранты и объявлять получателей.</span><span class="sxs-lookup"><span data-stu-id="30fa6-492">The app enables you to setup and manage an employee rewards and recognition, called R&R program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="30fa6-493">Получите его на GitHub</span><span class="sxs-lookup"><span data-stu-id="30fa6-493">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="30fa6-494">Карточка номинации На рабочем месте</span><span class="sxs-lookup"><span data-stu-id="30fa6-494">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Вкладка "Список наград на рабочем месте"](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="30fa6-496">Дополнительные сведения о шаблоне приложений см. в [шаблоне App.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)</span><span class="sxs-lookup"><span data-stu-id="30fa6-496">For more information on app template, see [App template](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>

## <a name="see-also"></a><span data-ttu-id="30fa6-497">См. также</span><span class="sxs-lookup"><span data-stu-id="30fa6-497">See also</span></span>

[<span data-ttu-id="30fa6-498">Интеграция веб-приложений</span><span class="sxs-lookup"><span data-stu-id="30fa6-498">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
