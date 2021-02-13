---
title: Шаблоны приложений Microsoft Teams
description: Ссылки и описания шаблонов приложений для платформы Microsoft Teams
ms.topic: reference
keywords: Демонстрация примеров шаблонов Microsoft Teams
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 21721848ba7893380ac217b5f47ce6a6e669e869
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231640"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="e5f12-104">Шаблоны приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e5f12-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="e5f12-105">Шаблоны приложений — это примеры полных приложений для Microsoft Teams, доступных с открытым кодом и доступных на GitHub.</span><span class="sxs-lookup"><span data-stu-id="e5f12-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="e5f12-106">Каждый шаблон приложения содержит подробные инструкции по развертыванию и установке этого приложения для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="e5f12-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="e5f12-107">Он также предоставляет пример приложения, которое можно установить и начать использовать немедленно.</span><span class="sxs-lookup"><span data-stu-id="e5f12-107">It also provides a sample app that you can install and begin using immediately.</span></span> <span data-ttu-id="e5f12-108">Кроме того, доступен полный исходный код, который позволяет подробно изучить его или разветвить код и изменить его в удовлетворении конкретных требований.</span><span class="sxs-lookup"><span data-stu-id="e5f12-108">The complete source code is available too, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="e5f12-109">Все шаблоны приложений предоставляются на условиях лицензии [MIT.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)</span><span class="sxs-lookup"><span data-stu-id="e5f12-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>
>[!NOTE] 
><span data-ttu-id="e5f12-110">Вам, а не корпорации Майкрософт необходимо лицензировать и поддерживать приложения, созданные из шаблонов приложений для пользователей и организаций.</span><span class="sxs-lookup"><span data-stu-id="e5f12-110">You, not Microsoft must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="e5f12-111">**&#9734; указывает только что выпущенные шаблоны приложений.**</span><span class="sxs-lookup"><span data-stu-id="e5f12-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="e5f12-112">Основные преимущества</span><span class="sxs-lookup"><span data-stu-id="e5f12-112">Key benefits</span></span>

* <span data-ttu-id="e5f12-113">**Развертывание непосредственно в облаке:** Все шаблоны приложений включают сценарии развертывания, которые позволяют вам размещение всех необходимых служб в Microsoft Azure или Power Platform.</span><span class="sxs-lookup"><span data-stu-id="e5f12-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="e5f12-114">**Рекомендуемый пример кода:** Шаблоны приложений соответствуют рекомендациям по безопасности и инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="e5f12-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="e5f12-115">Все изменения шаблонов приложений, отправленные сообществом, проверяются на соответствие требованиям.</span><span class="sxs-lookup"><span data-stu-id="e5f12-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="e5f12-116">**Настраиваемые и extensible:** Хотя все шаблоны приложений можно развернуть с минимальной конфигурацией, мы предоставляем всю базу кода и скрипты развертывания, чтобы вы могли легко настраивать или расширять их в своих уникальных потребностях.</span><span class="sxs-lookup"><span data-stu-id="e5f12-116">**Customizable and extensible:** While all app templates can be deployed with minimal configuration, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="e5f12-117">**Подробная документация:** Все шаблоны приложений сопровождаются всей документацией по архитектуре, развертыванию и настройке решения.</span><span class="sxs-lookup"><span data-stu-id="e5f12-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot-9734"></a><span data-ttu-id="e5f12-118">Бот по внедрению &#9734;</span><span class="sxs-lookup"><span data-stu-id="e5f12-118">Adoption Bot &#9734;</span></span>

<span data-ttu-id="e5f12-119">Бот по внедрению — это бот чата для обслуживания пользователей, построенный с помощью виртуального агента Power Для Teams (PVA).</span><span class="sxs-lookup"><span data-stu-id="e5f12-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams (PVA).</span></span> <span data-ttu-id="e5f12-120">Его можно рассматривать как версию PVA faQPlus.</span><span class="sxs-lookup"><span data-stu-id="e5f12-120">It can be considered as the PVA version of FAQPlus.</span></span> <span data-ttu-id="e5f12-121">Бот по внедрению отвечает на 100 и более распространенных вопросов о Microsoft 365 и Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="e5f12-122">Вы можете редактировать включенные темы, добавлять собственные темы и использовать существующие вопросы и вопросы и вопросы.</span><span class="sxs-lookup"><span data-stu-id="e5f12-122">You can edit the included topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="e5f12-123">Если пользователям нужна дополнительная помощь, бот по внедрению может подключить их к экспертам или даже расширить, чтобы открыть билеты в службу с расширенными соединитетелями потока.</span><span class="sxs-lookup"><span data-stu-id="e5f12-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.</span></span>

[<span data-ttu-id="e5f12-124">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-124">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="appointment-manager-9734"></a><span data-ttu-id="e5f12-125">Диспетчер &#9734;</span><span class="sxs-lookup"><span data-stu-id="e5f12-125">Appointment Manager &#9734;</span></span>

<span data-ttu-id="e5f12-126">Диспетчер встреч — это шаблон приложения Teams, который помогает предприятиям создавать, управлять и проводить виртуальные встречи с клиентами через Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-126">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="e5f12-127">Новые запросы на встречи от потребителей видны в каналах Teams, где их можно быстро назначить и переназначить сотрудникам в команде.</span><span class="sxs-lookup"><span data-stu-id="e5f12-127">New appointment requests from consumers are visible in Teams channels, where they can quickly be assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="e5f12-128">Запросы на встречи можно просматривать на уровне команды или на личном уровне с помощью настраиваемой вкладки.</span><span class="sxs-lookup"><span data-stu-id="e5f12-128">Appointment requests can be viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="e5f12-129">Каждая встреча связана с онлайн-собранием Teams, поэтому сотрудники и пользователи могут легко присоединиться к собранию в запланированное время.</span><span class="sxs-lookup"><span data-stu-id="e5f12-129">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="e5f12-130">Шаблон приложения интегрируется с Microsoft Bookings для простого управления встречами.</span><span class="sxs-lookup"><span data-stu-id="e5f12-130">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="e5f12-131">Запланированные встречи автоматически отображаются в календарях сотрудников, а пользователи получают настраиваемые уведомления и напоминания по электронной почте с внедренными ссылками на собрания.</span><span class="sxs-lookup"><span data-stu-id="e5f12-131">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="e5f12-132">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-132">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="e5f12-133">![Обзор диспетчера встреч ](../assets/images/appointment-manager-overview.png)
 ![ в Teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="e5f12-133">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="e5f12-134">Ask Away</span><span class="sxs-lookup"><span data-stu-id="e5f12-134">Ask Away</span></span>

<span data-ttu-id="e5f12-135">Ask Away — это [бот Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям проводить&вопросов и ответов в Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-135">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Q&A (Question and Answer) sessions within Teams.</span></span> <span data-ttu-id="e5f12-136">С помощью бота Ask Away участники команды могут отправлять и голосовать вопросы, общие коллегами, позволяя Q&Ведущих, чтобы легко собирать вопросы с самых разных ответов в канале или чате.</span><span class="sxs-lookup"><span data-stu-id="e5f12-136">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="e5f12-137">Бот можно использовать для проведения q-&в режиме реального времени в собрании Teams и позволяет участникам отправлять вопросы в режиме реального времени через чат.</span><span class="sxs-lookup"><span data-stu-id="e5f12-137">The bot can be used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live via chat.</span></span>

[<span data-ttu-id="e5f12-138">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-138">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Просмотр всплывающее диалоговое окно в области лидеров для пользователей, которые будут отвечать на вопросы](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="e5f12-140">Вспомогательная аналитика</span><span class="sxs-lookup"><span data-stu-id="e5f12-140">Associate Insights</span></span>

<span data-ttu-id="e5f12-141">Associate Insights — это шаблон [Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) который позволяет сотрудникам без труда напрямую фиксировать и отправлять отзывы клиентов, тональности и восприятие.</span><span class="sxs-lookup"><span data-stu-id="e5f12-141">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="e5f12-142">Сотрудники firstline часто являются первым представителем компании, который участвует с клиентами в контактной точке "один к одному".</span><span class="sxs-lookup"><span data-stu-id="e5f12-142">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="e5f12-143">Собранные данные могут совместно использоваться бизнес-командами, например с помощью вкладки Power BI Teams, для улучшения продукта и улучшения качества взаимодействия с клиентом.</span><span class="sxs-lookup"><span data-stu-id="e5f12-143">The collected data can be shared and used collaboratively by business teams, e.g., via a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="e5f12-144">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-144">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![Представление отзывов о статистике, сгенерированной приложением](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Power BI view of app generated insights](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="e5f12-147">Присутствие</span><span class="sxs-lookup"><span data-stu-id="e5f12-147">Attendance</span></span>

<span data-ttu-id="e5f12-148">Приложение "Присутствие" — это [вкладка Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) которую можно закрепить в команде.</span><span class="sxs-lookup"><span data-stu-id="e5f12-148">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that can be pinned in a team.</span></span> <span data-ttu-id="e5f12-149">Он предназначен для записи присутствия, как правило, в таких параметрах, как учебные и учебные среды.</span><span class="sxs-lookup"><span data-stu-id="e5f12-149">It is designed to record presence, typically in settings such as learning and training environments.</span></span> <span data-ttu-id="e5f12-150">Пользователи могут пометить или изменить присутствие в течение 30 дней в прошлом и просматривать итоги отчетов о посещении для всей группы или отдельных участников.</span><span class="sxs-lookup"><span data-stu-id="e5f12-150">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span>

[<span data-ttu-id="e5f12-151">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-151">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![Демонстрация приложения "Посещаемость"](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="e5f12-153">Book-a-room</span><span class="sxs-lookup"><span data-stu-id="e5f12-153">Book-a-room</span></span>

<span data-ttu-id="e5f12-154">Book-a-room — это бот [Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям быстро находить и резервировать комнату для собраний на 30 (по умолчанию), 60 или 90 минут, начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="e5f12-154">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="e5f12-155">Бот book-a-room имеет область личных или 1:1 бесед.</span><span class="sxs-lookup"><span data-stu-id="e5f12-155">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

[<span data-ttu-id="e5f12-156">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-156">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![Демонстрация "Книга в комнате"](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="e5f12-158">Доступ к построению</span><span class="sxs-lookup"><span data-stu-id="e5f12-158">Building Access</span></span>

<span data-ttu-id="e5f12-159">Building Access — это приложение на основе Платформы Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)которое поддерживает администрирование порогов занятости и социальных сетей, позволяя директорам объектов управлять присутствием сотрудников на сайте, отслеживать и сообщать о них.</span><span class="sxs-lookup"><span data-stu-id="e5f12-159">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="e5f12-160">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview)и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams и позволяет организациям определять готовность к построению, устанавливать критерии соответствия для доступа на сайте и собирать сведения для планирования в будущем.</span><span class="sxs-lookup"><span data-stu-id="e5f12-160">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="e5f12-161">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-161">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Создание карты резервирования доступа](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Создание представления клавиши Access](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="e5f12-164">Праздники</span><span class="sxs-lookup"><span data-stu-id="e5f12-164">Celebrations</span></span>

<span data-ttu-id="e5f12-165">Праздники — это приложение Teams, которое помогает участникам команды отмечать дни рождения, годовщины и другие повторяющиеся события.</span><span class="sxs-lookup"><span data-stu-id="e5f12-165">Celebrations is a Teams app that helps team members celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="e5f12-166">Он запоминает особые случаи для всех участников команды и отправляет приветственное сообщение во всех командах, выбранных на момент создания события, чтобы участники команды были особенными в свой день.</span><span class="sxs-lookup"><span data-stu-id="e5f12-166">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="e5f12-167">Приложение предоставляет простой интерфейс для всех участников команды, которые могут добавлять и просматривать свои события, а также позволяет пользователю выбирать команды, в которых будут делиться событиями.</span><span class="sxs-lookup"><span data-stu-id="e5f12-167">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="e5f12-168">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-168">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="e5f12-169">Контрольный список</span><span class="sxs-lookup"><span data-stu-id="e5f12-169">Checklist</span></span>

<span data-ttu-id="e5f12-170">Контрольный список — это пользовательское приложение расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которое позволяет вам сотрудничать с командой путем создания общего контрольного списка в чате или канале.</span><span class="sxs-lookup"><span data-stu-id="e5f12-170">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="e5f12-171">Приложение поддерживается во всех клиентах платформы Teams ( настольных компьютерах, браузерах, iOS и Android) и готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="e5f12-171">The app is supported across all Teams platform clients —  desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="e5f12-172">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-172">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![Создание контрольного списка в представлении Teams](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in-9734"></a><span data-ttu-id="e5f12-174">Классный класс для &#9734;</span><span class="sxs-lookup"><span data-stu-id="e5f12-174">Classroom Drop-in &#9734;</span></span>

<span data-ttu-id="e5f12-175">"Класс" — это приложение на основе Платформы Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)которое позволяет руководителям систем находить группы класса (виртуальные аудитории) и добавлять себя или других в эти группы класса в течение указанного периода, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="e5f12-175">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams (virtual classrooms) and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="e5f12-176">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview) и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams, чтобы убедиться, что образовательные учреждения могут оптимизировать свою работу в гибридной среде обучения, предоставив доступ соответствующим заинтересованным лицам для учебных групп по бизнес-требованиям.</span><span class="sxs-lookup"><span data-stu-id="e5f12-176">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="e5f12-177">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-177">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Запрос на впадаемую аудиторию](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="e5f12-179">Корпоративный Communicator</span><span class="sxs-lookup"><span data-stu-id="e5f12-179">Company Communicator</span></span>

<span data-ttu-id="e5f12-180">Приложение корпоративной Communicator позволяет корпоративным командам создавать и отправлять сообщения, предназначенные для нескольких команд или большого количества сотрудников, через чат, позволяя организации связаться с сотрудниками прямо там, где они взаимодействуют.</span><span class="sxs-lookup"><span data-stu-id="e5f12-180">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="e5f12-181">Используйте этот шаблон для нескольких сценариев, таких как новые объявления по инициативе, въеха сотрудников, современное обучение и разработка или широковещательные трансляции на всей организации.</span><span class="sxs-lookup"><span data-stu-id="e5f12-181">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="e5f12-182">Приложение предоставляет простой интерфейс для создания, предварительного просмотра, совместной работы и отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="e5f12-182">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="e5f12-183">Он предоставляет основу для создания специальных целевых возможностей связи, таких как настраиваемая телеметрия, о том, сколько пользователей подтверждали или взаимодействовали с сообщением.</span><span class="sxs-lookup"><span data-stu-id="e5f12-183">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="e5f12-184">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-184">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![представление Communicator jCompany](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="e5f12-186">Подыском группы контактов</span><span class="sxs-lookup"><span data-stu-id="e5f12-186">Contact Group Lookup</span></span>

<span data-ttu-id="e5f12-187">Приложение "Подыском группы контактов" предоставляет удобный и полезный подход к созданию, доступу и управлению группами контактов организации (прежнее название — списки рассылки или группы связи).</span><span class="sxs-lookup"><span data-stu-id="e5f12-187">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups (formerly known as distribution lists or communication groups).</span></span> <span data-ttu-id="e5f12-188">Пользователи могут быстро просматривать и общаться в чате с участниками группы, просматривать состояние участников и создавать групповой чат с выбранными участниками в группе контактов в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-188">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="e5f12-189">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-189">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![Представление "Закрепленные избранное" для группы контактов](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Демонстрация запуска чата для группы контактов](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="co-worker-appreciation-9734"></a><span data-ttu-id="e5f12-192">Совместное рабочего &#9734;</span><span class="sxs-lookup"><span data-stu-id="e5f12-192">Co-worker Appreciation &#9734;</span></span>

<span data-ttu-id="e5f12-193">С помощью шаблона шаблона рабочего процесса в Microsoft Teams пользователи могут распознавать достижения коллег в контексте Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-193">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="e5f12-194">Когда коллеги выбирают, чтобы вознаградить коллегу, получатели и другие участники команды помечаются в беседе канала и получают уведомление о сведениях о награде канала.</span><span class="sxs-lookup"><span data-stu-id="e5f12-194">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="e5f12-195">Эти данные записывают в приложение Teams, которое является безопасным, переносимым и легкодоступным.</span><span class="sxs-lookup"><span data-stu-id="e5f12-195">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="e5f12-196">Это может рассматриваться как версия шаблона приложения "Открытые индикаторы событий" на основе PowerApps с таблицей лидеров.</span><span class="sxs-lookup"><span data-stu-id="e5f12-196">This can be considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="e5f12-197">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-197">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![В целом](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="e5f12-199">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="e5f12-199">CrowdSourcer</span></span>

<span data-ttu-id="e5f12-200">CrowdSourcer — это бот [Microsoft Teams,](../bots/what-are-bots.md) который предоставляет участникам группы запрашиваемую информацию, которую совместно запрашивают участники группы.</span><span class="sxs-lookup"><span data-stu-id="e5f12-200">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="e5f12-201">Это отличный способ ответить на часто задамые вопросы, позволяя участникам активно участвовать и вносить свой вклад в интересный и полезный информационный ресурс.</span><span class="sxs-lookup"><span data-stu-id="e5f12-201">It's a great way to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="e5f12-202">Get it on Github</span><span class="sxs-lookup"><span data-stu-id="e5f12-202">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Взаимодействие с конечными пользователями в Краудсорсе](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="e5f12-204">Пользовательские наклейки</span><span class="sxs-lookup"><span data-stu-id="e5f12-204">Custom Stickers</span></span>

<span data-ttu-id="e5f12-205">Самостоятельное выражение является основой для правильной культуры команды.</span><span class="sxs-lookup"><span data-stu-id="e5f12-205">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="e5f12-206">Этот шаблон приложения является расширением [обмена](~/messaging-extensions/what-are-messaging-extensions.md) сообщениями, которое позволяет пользователям использовать пользовательские стикеры и GIF в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-206">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="e5f12-207">Этот шаблон обеспечивает простую веб-настройку, в которой любой пользователь с доступом к конфигурации может отправить GIF- или стикеры/изображения, которые должны иметь конечные пользователи, что позволяет всей команде использовать любой выбранный вами набор стикеров.</span><span class="sxs-lookup"><span data-stu-id="e5f12-207">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs/stickers/images they want their end-users to have, allowing your entire team to use any set of stickers you chose.</span></span>

<span data-ttu-id="e5f12-208">Это приложение также обеспечивает простой общий доступ к изображениям, GIF-изображениям и стикерам в командах без доступа к сайтам SharePoint или отдельным каналам в качестве механизмов хранения и общего доступа.</span><span class="sxs-lookup"><span data-stu-id="e5f12-208">This app also enables easy sharing of images/GIFs/stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="e5f12-209">Например, группы продуктов могут легко делиться изображениями продуктов и GIF-изображениями с социальными медиа, маркетингом и группами продаж программными средствами.</span><span class="sxs-lookup"><span data-stu-id="e5f12-209">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="e5f12-210">Вы также можете расширить это приложение, активив поток уведомлений для определенных групп или отдельных пользователей, когда будут доступны новые изображения или GIF-изображения.</span><span class="sxs-lookup"><span data-stu-id="e5f12-210">One can also extend this app by triggering a notification flow to specific teams/individuals when new images/GIFs are made available.</span></span>

[<span data-ttu-id="e5f12-211">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-211">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Приложение "Стикеры"](../assets/images/stickers.png)

## <a name="employee-ideas-9734"></a><span data-ttu-id="e5f12-213">Идеи сотрудников &#9734;</span><span class="sxs-lookup"><span data-stu-id="e5f12-213">Employee Ideas &#9734;</span></span>

<span data-ttu-id="e5f12-214">Приложение "Идеи сотрудников" — это версия PowerApps шаблона приложения "Отличные идеи" на основе Azure.</span><span class="sxs-lookup"><span data-stu-id="e5f12-214">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="e5f12-215">Приложение позволяет пользователям Teams настраивать и настраивать кампанию идей.</span><span class="sxs-lookup"><span data-stu-id="e5f12-215">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="e5f12-216">Идею кампании — это категория для группировки идей по общим темам.</span><span class="sxs-lookup"><span data-stu-id="e5f12-216">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="e5f12-217">Пользователи Teams также могут выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e5f12-217">Teams users can also perform following activities:</span></span>
* <span data-ttu-id="e5f12-218">Настройте стандартную форму отправки, которую сотрудники должны отправить для каждой идеи.</span><span class="sxs-lookup"><span data-stu-id="e5f12-218">Configure a standard submission form that employees need to submit for each idea.</span></span> 
* <span data-ttu-id="e5f12-219">Просмотрите идеи и список кампаний и управляйте ими.</span><span class="sxs-lookup"><span data-stu-id="e5f12-219">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="e5f12-220">Изменение и удаление кампаний.</span><span class="sxs-lookup"><span data-stu-id="e5f12-220">Modify and delete campaigns.</span></span>
* <span data-ttu-id="e5f12-221">Просмотрите советы лидеров по идеям.</span><span class="sxs-lookup"><span data-stu-id="e5f12-221">Review leader boards of ideas.</span></span>
* <span data-ttu-id="e5f12-222">Проголосуйте за и поделитесь приоритетными идеями.</span><span class="sxs-lookup"><span data-stu-id="e5f12-222">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="e5f12-223">Отправка идей для кампании.</span><span class="sxs-lookup"><span data-stu-id="e5f12-223">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="e5f12-224">Просмотр идеи другого участника команды.</span><span class="sxs-lookup"><span data-stu-id="e5f12-224">View other team member's idea.</span></span>
* <span data-ttu-id="e5f12-225">Проголосуйте за наиболее понравились идеи.</span><span class="sxs-lookup"><span data-stu-id="e5f12-225">Vote on most liked ideas.</span></span>
* <span data-ttu-id="e5f12-226">Просмотрите эффективность их идей по сравнению с другими в рамках кампании.</span><span class="sxs-lookup"><span data-stu-id="e5f12-226">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="e5f12-227">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-227">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Управление представлением кампании](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="e5f12-229">Электронные рецепты</span><span class="sxs-lookup"><span data-stu-id="e5f12-229">E-Prescriptions</span></span> 

<span data-ttu-id="e5f12-230">E-Рецепты — это приложение на основе [Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app)которое улучшает телеметрию и виртуальную помощь, автоматизирующее процесс выдачи рецептов для пациентов.</span><span class="sxs-lookup"><span data-stu-id="e5f12-230">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)-based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="e5f12-231">Медицинские специалисты могут быстро просмотреть встречи, создать электронные рецепты и отправлять письма с вложениями по электронной почте непосредственно на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-231">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="e5f12-232">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-232">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![Снимок экрана: приложение "Рецепты по электронной почте".](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Снимок экрана: приложение "Рецепты по электронной почте".](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training"></a><span data-ttu-id="e5f12-237">Обучение сотрудников</span><span class="sxs-lookup"><span data-stu-id="e5f12-237">Employee Training</span></span> 

<span data-ttu-id="e5f12-238">Обучение сотрудников — это приложение Microsoft Teams, которое позволяет организаторам легко публиковать, отслеживать и продвигать учебные мероприятия для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="e5f12-238">Employee training is a Microsoft Teams app that enables organizers to easily publish,  track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="e5f12-239">С помощью приложения планировщики событий могут отправлять напоминания и уведомления регистраторам событий, а сотрудники могут указывать на интерес к предстоящим событиям, обновлять текущие события и делиться сведениями о событиях с коллегами через расширение обмена сообщениями Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-239">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues via the Teams messaging extension.</span></span>

[<span data-ttu-id="e5f12-240">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-240">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="e5f12-241">**Просмотр событий обучения сотрудников** ![ Изображение вкладки "Обучение сотрудников"](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="e5f12-241">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="e5f12-242">**Создание обучающего события для сотрудников** ![ Форма создания событий для обучения сотрудников](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="e5f12-242">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="e5f12-243">Expert Finder</span><span class="sxs-lookup"><span data-stu-id="e5f12-243">Expert Finder</span></span>

<span data-ttu-id="e5f12-244">"Поиск экспертов" — это бот [Microsoft Teams,](../bots/what-are-bots.md) который идентифицирует определенных членов организации на основе их навыков, интересов и атрибутов обучения.</span><span class="sxs-lookup"><span data-stu-id="e5f12-244">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="e5f12-245">Участники находят в организации экспертов, которые соответствуют поиску по ключевым словам профилей пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5f12-245">Members find experts within an organization  that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="e5f12-246">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-246">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Демонстрация результатов поиска "Поиск экспертов"](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="e5f12-248">Вопросы и ответы плюс</span><span class="sxs-lookup"><span data-stu-id="e5f12-248">FAQ Plus</span></span>

<span data-ttu-id="e5f12-249">Вопросы и ответы&боты — это простой способ предоставления ответов на часто задамые вопросы пользователей.</span><span class="sxs-lookup"><span data-stu-id="e5f12-249">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="e5f12-250">Однако большинство ботов не могут осмысленно взаимодействовать с пользователями, так как при сбойе бота в цикле нет человека.</span><span class="sxs-lookup"><span data-stu-id="e5f12-250">However, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="e5f12-251">Бот вопросы и вопросы — это&бот, который вызывает человека в цикле, когда не может помочь.</span><span class="sxs-lookup"><span data-stu-id="e5f12-251">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="e5f12-252">Можно задать боту вопрос, а бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="e5f12-252">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="e5f12-253">В этом случае бот позволяет пользователю отправить запрос, который затем будет опубликован предварительно настроенной группе экспертов, которые помогут обеспечить поддержку, выступая на основе уведомлений из самой команды.</span><span class="sxs-lookup"><span data-stu-id="e5f12-253">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="e5f12-254">Последний выпуск **faq Plus** поддерживает улучшенные вопросы и&решения, позволяя группе экспертов выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e5f12-254">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="e5f12-255">&#x2714; добавить новые вопросы&как непосредственно в базу знаний с помощью расширений сообщений.</span><span class="sxs-lookup"><span data-stu-id="e5f12-255">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="e5f12-256">&#x2714; изменения и удаления Q&пары, добавленные ботом.</span><span class="sxs-lookup"><span data-stu-id="e5f12-256">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="e5f12-257">&#x2714; отслеживание истории редакций Q&As.</span><span class="sxs-lookup"><span data-stu-id="e5f12-257">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="e5f12-258">&#x2714; настроить ответ с дополнительными сведениями для отображения в качестве [адаптивной карточки.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="e5f12-258">&#x2714; Configure an answer with additional details to display as an [adaptive card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="e5f12-259">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-259">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Gif faq Plus](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app-9734"></a><span data-ttu-id="e5f12-261">Получить поддержку приложения &#9734;</span><span class="sxs-lookup"><span data-stu-id="e5f12-261">Get Support App &#9734;</span></span>

<span data-ttu-id="e5f12-262">Приложение "Получить поддержку" можно использовать в организациях, использующих Microsoft Teams, чтобы позволить любому набору пользователей запрашивать помощь у руководителей.</span><span class="sxs-lookup"><span data-stu-id="e5f12-262">The Get Support app can be used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="e5f12-263">Это приложение включает различные функции, например:</span><span class="sxs-lookup"><span data-stu-id="e5f12-263">This app includes various features, such as:</span></span>
-   <span data-ttu-id="e5f12-264">Запрос помощи по различным категориям из Power App</span><span class="sxs-lookup"><span data-stu-id="e5f12-264">Requesting assistance on different categories from a Power App</span></span>
-   <span data-ttu-id="e5f12-265">Уведомления, от отправленные инициаторам запроса с уведомлением о том, кому назначено</span><span class="sxs-lookup"><span data-stu-id="e5f12-265">Notifications sent to requestors informing them of who has been assigned</span></span> 
-   <span data-ttu-id="e5f12-266">Уведомления, от отправленные назначенному руководителю с уведомлением о том, кому нужна помощь</span><span class="sxs-lookup"><span data-stu-id="e5f12-266">Notifications sent to assigned supervisors informing them of who needs assistance</span></span> 
-   <span data-ttu-id="e5f12-267">Анализ эскалаций и шаблонов в SharePoint и PowerBI</span><span class="sxs-lookup"><span data-stu-id="e5f12-267">Analyzing escalations and patterns in SharePoint and PowerBI</span></span>

[<span data-ttu-id="e5f12-268">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-268">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Get Support Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="e5f12-270">Отслеживание цели</span><span class="sxs-lookup"><span data-stu-id="e5f12-270">Goal Tracker</span></span>

<span data-ttu-id="e5f12-271">Приложение "Отслеживание целей" — это комплексное решение для вашей организации, которое поддерживает установление целей, отслеживание хода выполнения и подтверждение успеха в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-271">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="e5f12-272">Приложение позволяет пользователям устанавливать, отслеживать и обновлять цели на профессиональном, личном и командном уровне.</span><span class="sxs-lookup"><span data-stu-id="e5f12-272">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="e5f12-273">Участники группы также получают уведомления и обновления состояния, чтобы оставаться в фокусе и отслеживать их.</span><span class="sxs-lookup"><span data-stu-id="e5f12-273">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="e5f12-274">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![Настройка целей](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр целей набора](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a><span data-ttu-id="e5f12-277">Отличные идеи</span><span class="sxs-lookup"><span data-stu-id="e5f12-277">Great Ideas</span></span>

<span data-ttu-id="e5f12-278">Приложение "Отличные идеи" поддерживает и расширяет возможности инноваций и творчества в организации.</span><span class="sxs-lookup"><span data-stu-id="e5f12-278">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="e5f12-279">Это приложение позволяет вашим сотрудникам обмениваться идеями с коллегами и руководством, обнаруживая новые отправки, вклад в прожекторную работу для одноранговой работы и голосуя за лучшие предложения в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-279">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="e5f12-280">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-280">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

:::row:::
  :::column span="2":::
    ![Просмотр отправленных идей](../assets/images/great-ideas-all-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр идей](../assets/images/great-ideas-digest-view.png)
:::column-end:::
:::row-end:::

## <a name="group-activities"></a><span data-ttu-id="e5f12-283">Групповые действия</span><span class="sxs-lookup"><span data-stu-id="e5f12-283">Group Activities</span></span>

<span data-ttu-id="e5f12-284">Групповые действия — это приложение Microsoft Teams, которое позволяет владельцам команд быстро создавать группы действий и управлять рабочими процессами совместной работы в контексте Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-284">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="e5f12-285">Авторы действий могут создавать действия, случайным образом распределять участников команды по группам и при желании отправлять напоминания боту, пока действия не будут завершены.</span><span class="sxs-lookup"><span data-stu-id="e5f12-285">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="e5f12-286">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-286">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Список действий в группах в Teams](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Уведомление о групповой активности в канале](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="grow-your-skills"></a><span data-ttu-id="e5f12-289">Развивать навыки</span><span class="sxs-lookup"><span data-stu-id="e5f12-289">Grow Your Skills</span></span>

<span data-ttu-id="e5f12-290">Приложение "Развитие навыков" поддерживает профессиональный рост и развитие, позволяя сотрудникам участвовать в дополнительных проектах для вашей организации, одновременно изучая новые навыки.</span><span class="sxs-lookup"><span data-stu-id="e5f12-290">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="e5f12-291">Сотрудники могут использовать приложение, чтобы находить возможности, которые соответствуют их интересам, получать осмысленные возможности совместной работы с коллегами и получать новые уровни знаний и возможностей в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-291">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="e5f12-292">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-292">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![Представление доступных проектов](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр навыков, полученных у просматриваемой точки зрения](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a><span data-ttu-id="e5f12-295">Поддержка управления персоналом</span><span class="sxs-lookup"><span data-stu-id="e5f12-295">HR Support</span></span>

<span data-ttu-id="e5f12-296">Бот службы поддержки отдела кадров — это удобное решение для&бота, который вызывает специалистов и экспертов из отдела кадров в цикле, когда не может помочь.</span><span class="sxs-lookup"><span data-stu-id="e5f12-296">HR Support bot is a friendly Q&A bot that brings a support professional/expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="e5f12-297">Можно задать боту вопрос, а бот отвечает ответом, если он содержится в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="e5f12-297">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="e5f12-298">Если это не так, бот позволяет пользователю отправить запрос, который затем будет опубликован в предварительно настроенной группе экспертов, которые помогают предоставлять поддержку, действуя на основе уведомлений из самой команды.</span><span class="sxs-lookup"><span data-stu-id="e5f12-298">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="e5f12-299">Кроме того, бот предлагает ссылки на рекомендуемые политики и вопросы отдела кадров путем поиска предварительно настроенных тегов в вопросе.</span><span class="sxs-lookup"><span data-stu-id="e5f12-299">Additionally, the bot suggests links to recommended HR policies/questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="e5f12-300">Эти плитки также можно найти на связанной вкладке в качестве краткой ссылки.</span><span class="sxs-lookup"><span data-stu-id="e5f12-300">These tiles can also be found in the associated tab as a quick reference.</span></span> <span data-ttu-id="e5f12-301">Поддержка отдела кадров хорошо работает для легкого QnA и быстрой поддержки при запуске новых проектов и инициатив в организации.</span><span class="sxs-lookup"><span data-stu-id="e5f12-301">HR Support works well for light weight QnA and to provide quick support when launching new projects/initiatives in the organization.</span></span>

[<span data-ttu-id="e5f12-302">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-302">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Поддержка управления персоналом](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="e5f12-304">Точки соприкосновения</span><span class="sxs-lookup"><span data-stu-id="e5f12-304">Icebreaker</span></span>

<span data-ttu-id="e5f12-305">Icebreaker — это бот [Microsoft Teams,](../bots/what-are-bots.md) который помогает команде сближаться путем сопряжения двух случайных участников команды каждую неделю для встречи.</span><span class="sxs-lookup"><span data-stu-id="e5f12-305">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="e5f12-306">Бот упрощает планирование, автоматически предлагая свободное время для обоих участников.</span><span class="sxs-lookup"><span data-stu-id="e5f12-306">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="e5f12-307">Укрепляйте личные подключения и создайте тесное сообщество с помощью этого приложения.</span><span class="sxs-lookup"><span data-stu-id="e5f12-307">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="e5f12-308">Помимо поощрения личных подключений во всей команде, приложение Icebreaker помогает развивать сообщества, основанные на интересах, в организации.</span><span class="sxs-lookup"><span data-stu-id="e5f12-308">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="e5f12-309">Например, вы можете использовать это приложение для группы по интересам DevOps, чтобы помочь идеи и лучшие методики органично распространяться по всей организации.</span><span class="sxs-lookup"><span data-stu-id="e5f12-309">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="e5f12-310">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-310">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Приложение Icebreaker](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="e5f12-312">Поощрения</span><span class="sxs-lookup"><span data-stu-id="e5f12-312">Incentives</span></span>

<span data-ttu-id="e5f12-313">Программы поощрений — это шаблон [Power Apps,](/powerapps/maker/canvas-apps/embed-teams-app) который управляет и отслеживает участие сотрудников в назначенных мероприятиях, таких как учебные курсы и инициативы по управлению изменениями.</span><span class="sxs-lookup"><span data-stu-id="e5f12-313">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities such as trainings and change management initiatives.</span></span> <span data-ttu-id="e5f12-314">Администраторы используют приложение для создания назначенных действий, назначения баллов для завершения и указания необходимых уровней точки приемлемости для поощрения.</span><span class="sxs-lookup"><span data-stu-id="e5f12-314">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="e5f12-315">Сотрудники используют приложение для просмотра своих накопившихся баллов и, по достижении приемлемости, запрашивают и запрашивают выкупаемые поощрения.</span><span class="sxs-lookup"><span data-stu-id="e5f12-315">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="e5f12-316">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-316">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Демонстрация приложения "Программы поощрений"](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="e5f12-318">Incident Reporter</span><span class="sxs-lookup"><span data-stu-id="e5f12-318">Incident Reporter</span></span>

<span data-ttu-id="e5f12-319">Incident Reporter — это [бот Microsoft Teams,](../bots/what-are-bots.md)  который оптимизирует управление инцидентами в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="e5f12-319">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="e5f12-320">Бот упрощает автоматическое сбор данных об инциденте, настраиваемые отчеты об инцидентах, соответствующие уведомления заинтересованных лиц и комплексную процедуру отслеживания инцидентов.</span><span class="sxs-lookup"><span data-stu-id="e5f12-320">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="e5f12-321">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-321">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![Представление области группы "Корреспондент инцидентов"](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Представление личных областей "Корреспондент инцидентов"](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="inspection-9734"></a><span data-ttu-id="e5f12-324">Проверка &#9734;</span><span class="sxs-lookup"><span data-stu-id="e5f12-324">Inspection &#9734;</span></span>

 <span data-ttu-id="e5f12-325">Проверка — это приложение Microsoft Teams, которое позволяет сотрудникам переднего линия проверять все, начиная с местоположений и до активов и оборудования.</span><span class="sxs-lookup"><span data-stu-id="e5f12-325">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="e5f12-326">Например, розничный магазин, производственный комбинат, транспортные средства и компьютеры.</span><span class="sxs-lookup"><span data-stu-id="e5f12-326">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="e5f12-327">В этом решении есть два приложения, каждое из которых предназначено для разных типов пользователей.</span><span class="sxs-lookup"><span data-stu-id="e5f12-327">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="e5f12-328">Приложение позволяет сотрудникам переднего уровня проверять ресурс или область, управлять качеством продуктов и услуг или поддерживать безопасность на рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="e5f12-328">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="e5f12-329">Это упрощает взаимодействие между участниками группы для решения проблем, найденных во время проверки.</span><span class="sxs-lookup"><span data-stu-id="e5f12-329">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="e5f12-330">Приложение предоставляет менеджерам простые отчеты для ускорения решения проблем и выделения тенденций.</span><span class="sxs-lookup"><span data-stu-id="e5f12-330">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="e5f12-331">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-331">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Обзор проверки](../assets/images/inspection-app.png)  


## <a name="issue-reporting-9734"></a><span data-ttu-id="e5f12-333">Отчеты о проблемах &#9734;</span><span class="sxs-lookup"><span data-stu-id="e5f12-333">Issue Reporting &#9734;</span></span>

<span data-ttu-id="e5f12-334">Приложение "Отчеты о проблемах" позволяет сотрудникам и менеджерам повышать уровень проблем и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="e5f12-334">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="e5f12-335">Она состоит из двух приложений: приложения "Отчеты о проблемах" для отчетов о проблемах и приложения "Управление вопросами" для управления ими.</span><span class="sxs-lookup"><span data-stu-id="e5f12-335">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="e5f12-336">Руководители групп используют приложение "Управление вопросами" для настройки работы приложения, включая канал, в котором приложение создает сообщения Microsoft Teams и задачи Планировщика.</span><span class="sxs-lookup"><span data-stu-id="e5f12-336">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="e5f12-337">Менеджеры также используют приложение для создания форм шаблонов для сбора сведений, когда пользователь сообщает о проблеме.</span><span class="sxs-lookup"><span data-stu-id="e5f12-337">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="e5f12-338">Например, просмотрите, отредактируете или удалите формы шаблонов проблем.</span><span class="sxs-lookup"><span data-stu-id="e5f12-338">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="e5f12-339">Приложение также можно использовать для просмотра вопросов группы, отчетов об истории проблем и эффективного управления решением проблем.</span><span class="sxs-lookup"><span data-stu-id="e5f12-339">The app can also be used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="e5f12-340">Сотрудники используют приложение "Отчеты о проблемах" для регистрации проблем и сведений, необходимых для их устранения.</span><span class="sxs-lookup"><span data-stu-id="e5f12-340">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="e5f12-341">Приложение также используется для изменения и устранения существующих проблем, а также для получения высокоуровневого представления отдельных или командных проблем.</span><span class="sxs-lookup"><span data-stu-id="e5f12-341">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="e5f12-342">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-342">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Представление команды "Выдача отчетов"](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="e5f12-344">Новая подменая для сотрудников</span><span class="sxs-lookup"><span data-stu-id="e5f12-344">New Employee Onboarding</span></span> 

<span data-ttu-id="e5f12-345">Новая въеха сотрудников — это интегрированное решение microsoft Teams и [SharePoint](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) Для новых сотрудников, которое позволяет организации обеспечить единую и качественную веху для сотрудников при приеме на работу.</span><span class="sxs-lookup"><span data-stu-id="e5f12-345">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="e5f12-346">Приложение может использоваться группами управления персоналом и менеджерами по найму для предоставления релевантной информации на протяжении всего процесса ориентации и ввода, а также новыми наемными персоналами для обмена отзывами, предоставления введение и выполнения задач по внедрению.</span><span class="sxs-lookup"><span data-stu-id="e5f12-346">The app can be used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="e5f12-347">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-347">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="e5f12-348">**Карточка приветствия нового сотрудника** ![ Изображение карточки приветствия нового сотрудника](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="e5f12-348">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="e5f12-349">**Контрольный список новых сотрудников** ![ Изображение контрольного списка новых сотрудников](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="e5f12-349">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="e5f12-350">Открытые индикаторы событий</span><span class="sxs-lookup"><span data-stu-id="e5f12-350">Open Badges</span></span>

<span data-ttu-id="e5f12-351">Открытые индикаторы событий — это приложение Microsoft Teams, которое позволяет пользователям получать цифровые эмблемы учетных данных обучения в контексте Teams и делиться ими везде.</span><span class="sxs-lookup"><span data-stu-id="e5f12-351">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="e5f12-352">Использование возможностей сторонних служб выдачи цифровых индикаторов событий, [Badgr](https://badgr.org/), отмеченных индикаторов событий, записываются в профиль Badgr получателя и доступны для создания и обмена богатыми возможностями жизненного обучения.</span><span class="sxs-lookup"><span data-stu-id="e5f12-352">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="e5f12-353">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![Изображение доступных индикаторов событий](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Представление значков, отмеченных значками](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="poll"></a><span data-ttu-id="e5f12-356">Опрос</span><span class="sxs-lookup"><span data-stu-id="e5f12-356">Poll</span></span> 

<span data-ttu-id="e5f12-357">Опрос — это пользовательское приложение расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которое позволяет быстро создавать и отправлять опросы в чате или канале для сбора мнений и предпочтений команды.</span><span class="sxs-lookup"><span data-stu-id="e5f12-357">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="e5f12-358">Приложение поддерживается во всех клиентах платформы Teams ( настольных компьютерах, браузерах, iOS и Android) и готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="e5f12-358">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android  — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="e5f12-359">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-359">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Создание опроса в представлении Teams](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="e5f12-361">Быстрые ответы</span><span class="sxs-lookup"><span data-stu-id="e5f12-361">Quick Responses</span></span>

<span data-ttu-id="e5f12-362">Быстрые ответы — это приложение Microsoft Teams, которое предоставляет надежное решение для эффективного ответа на часто задаваемые вопросы и ответы пользователей.</span><span class="sxs-lookup"><span data-stu-id="e5f12-362">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions (FAQs).</span></span> <span data-ttu-id="e5f12-363">Вместо того чтобы отвечать на каждый запрос вручную и постоянно повторяясь сведения, приложение создает библиотеку ответов для интерактивного пользовательского интерфейса с помощью расширений обмена сообщениями [Teams.](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="e5f12-363">Instead of answering each query manually and  continuously repeating information, the app will build a library of responses for an interactive user experience via Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="e5f12-364">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Пример представления ответов](../assets/images/quick-responses.png)

## <a name="rapid-assist-9734"></a><span data-ttu-id="e5f12-366">Быстрая помощь &#9734;</span><span class="sxs-lookup"><span data-stu-id="e5f12-366">Rapid Assist &#9734;</span></span>

<span data-ttu-id="e5f12-367">Быстрая поддержка — это приложение на основе Платформы Microsoft [Power Platform,](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) которое позволяет клиентам быстро общаться со специалистами, получать быстрые ответы, искать информацию, выполнять открытые запросы и позволять экспертам получать уведомления, чтобы быстро получать ответы на вопросы.</span><span class="sxs-lookup"><span data-stu-id="e5f12-367">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="e5f12-368">Приложение, построенное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview) и [Power Automate,](/power-automate/getting-started)глубоко интегрируется с Microsoft Teams, что позволяет организациям легко подключаться к сотрудникам переднего звена с корпоративными связями, разрешать запросы клиентов и предоставлять отличный опыт работы с клиентами.</span><span class="sxs-lookup"><span data-stu-id="e5f12-368">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="e5f12-369">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-369">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Интерфейс запроса конечных пользователей](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Представление запроса эксперта](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="e5f12-372">Reflect</span><span class="sxs-lookup"><span data-stu-id="e5f12-372">Reflect</span></span> 

<span data-ttu-id="e5f12-373">Reflect — это пользовательское приложение расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которое предоставляет участникам команды безопасный и инклюзивный ресурс, который позволяет делиться своим состоянием с коллегами и/или руководителями групп непосредственно в Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-373">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues and/or group leaders directly within Teams.</span></span> <span data-ttu-id="e5f12-374">Приложение доступно в каналах, группах, собраниях и чатах 1:1, а для ответа на регистрацию можно установить общедоступный, закрытый или полностью анонимный.</span><span class="sxs-lookup"><span data-stu-id="e5f12-374">The app is available in channel, group, meeting, and 1:1 chats and the check-in response can be set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="e5f12-375">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="e5f12-376">**Опрос для well-being**</span><span class="sxs-lookup"><span data-stu-id="e5f12-376">**Well-being poll**</span></span>
    
    ![Отраженный опрос пользователей приложения](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="e5f12-378">Удаленная поддержка</span><span class="sxs-lookup"><span data-stu-id="e5f12-378">Remote Support</span></span>

<span data-ttu-id="e5f12-379">Удаленная поддержка — это [бот Microsoft Teams,](../bots/what-are-bots.md) который обеспечивает сфокусированный интерфейс между запросителями поддержки во всей организации и внутренней командой поддержки.</span><span class="sxs-lookup"><span data-stu-id="e5f12-379">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="e5f12-380">Конечные пользователи могут отправлять, редактировать или отзывать запросы на поддержку, а группа поддержки может отвечать на запросы, управлять ими и обновлять их на всех платформах Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-380">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="e5f12-381">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-381">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![Форма запроса поддержки](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Запрос сведений о поддержке](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a><span data-ttu-id="e5f12-384">Request-a-team</span><span class="sxs-lookup"><span data-stu-id="e5f12-384">Request-a-team</span></span>

<span data-ttu-id="e5f12-385">Request-a-team — это приложение Microsoft Teams, которое оптимизирует создание новой команды для вашей корпоративной организации.</span><span class="sxs-lookup"><span data-stu-id="e5f12-385">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="e5f12-386">Приложение поддерживает стандартизацию и лучшие методики при создании новых экземпляров группы с помощью интеграции формы запроса, управляемой мастером, внедренного процесса утверждения, панели мониторинга состояния запроса и автоматизированных сборок группы.</span><span class="sxs-lookup"><span data-stu-id="e5f12-386">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="e5f12-387">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-387">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![Представление страницы "Запрос с командой"](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Представление страницы мастера "Запрос в команду"](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a><span data-ttu-id="e5f12-390">Scrums for Channels</span><span class="sxs-lookup"><span data-stu-id="e5f12-390">Scrums for Channels</span></span>

<span data-ttu-id="e5f12-391">Scrums for Channels — это приложение помощника по скайму, которое позволяет пользователям планировать и запускать scrum-команды в каналах в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-391">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="e5f12-392">Приложение отлично подходит для удаленных команд и групп, состоящих из участников из различных географических расположений и часовых поясов, чтобы обмениваться ежедневными обновлениями и обеспечивать участие в собраниях скайма.</span><span class="sxs-lookup"><span data-stu-id="e5f12-392">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="e5f12-393">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-393">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="e5f12-394">Чтобы провести собрания скаймы в групповом чате, см. шаблон приложения [Scrums for Group Chat.](#scrums-for-group-chat)</span><span class="sxs-lookup"><span data-stu-id="e5f12-394">To conduct scrum meetings in a group chat, please see our [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

:::row:::
  :::column span="2":::
    ![Scrums for channels settings view](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Scrums for channels team member status view](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a><span data-ttu-id="e5f12-397">Scrums for Group Chat</span><span class="sxs-lookup"><span data-stu-id="e5f12-397">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="e5f12-398">Шаблон приложения "Состояние scrums" обновлен и теперь является scrums для группового чата.</span><span class="sxs-lookup"><span data-stu-id="e5f12-398">The Scrums Status app template has been updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="e5f12-399">Scrums for Group Chat is a supporting scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span><span class="sxs-lookup"><span data-stu-id="e5f12-399">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="e5f12-400">Он позволяет всем участникам группового чата внести свой вклад в скайп и просматривать обновления, сделанные другими участниками в запущенном скайме.</span><span class="sxs-lookup"><span data-stu-id="e5f12-400">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="e5f12-401">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-401">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Scrums for Group Chat demo](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="e5f12-403">Теперь поделитесь</span><span class="sxs-lookup"><span data-stu-id="e5f12-403">Share Now</span></span> 

<span data-ttu-id="e5f12-404">Приложение "Поделиться теперь" способствует положительному обмену информацией между коллегами, позволяя пользователям легко обмениваться содержимым в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-404">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="e5f12-405">Пользователи привяжет приложение к совместному доступу к интересуым элементами с участниками группы, обнаружению нового общего содержимого, задают параметры и закладки избранного для более позднего чтения.</span><span class="sxs-lookup"><span data-stu-id="e5f12-405">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="e5f12-406">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-406">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Выбор представления содержимого](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="e5f12-408">Поиск в списке SharePoint</span><span class="sxs-lookup"><span data-stu-id="e5f12-408">SharePoint List Search</span></span>

<span data-ttu-id="e5f12-409">Совместная работа в Microsoft Teams довольно часто ссылается на сведения, содержащиеся в элементов в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e5f12-409">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="e5f12-410">Простое включении ссылки на нужный элемент заставляет всех переключиться с контекста на беседу, найти необходимые сведения, а затем вернуться в Teams, чтобы продолжить беседу.</span><span class="sxs-lookup"><span data-stu-id="e5f12-410">Simply pasting a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="e5f12-411">По мере того как беседа продолжается, обычно людям придется вернуться к эталонным элементам несколько раз, чтобы проверить новые комментарии и обновить свои впечатления от сведений, содержащихся в элементе.</span><span class="sxs-lookup"><span data-stu-id="e5f12-411">As the conversation continues typically people will have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="e5f12-412">Такое переключение контекста создает барьер для плавной совместной работы и является рецептом для того, что проходит через взломы.</span><span class="sxs-lookup"><span data-stu-id="e5f12-412">This context switching creates a barrier to smooth collaboration, and is a recipe for things falling through the cracks.</span></span>

<span data-ttu-id="e5f12-413">Чтобы облегчить эту проблему, мы рады сообщить вам шаблон приложения поиска списков.</span><span class="sxs-lookup"><span data-stu-id="e5f12-413">To help alleviate this pain, we are happy to bring to you the List Search app template.</span></span> <span data-ttu-id="e5f12-414">Миллионы пользователей используют SharePoint для ключевых процессов в своих организациях.</span><span class="sxs-lookup"><span data-stu-id="e5f12-414">Millions of users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="e5f12-415">Однако совместная работа над списками может быть особенно трудоемкой.</span><span class="sxs-lookup"><span data-stu-id="e5f12-415">However, collaborating around lists can be especially tedious.</span></span> <span data-ttu-id="e5f12-416">С помощью шаблона приложения "Поиск списка" в Microsoft Teams пользователи могут вставлять сведения из элементов списка SharePoint непосредственно в беседе чата, чтобы уменьшить переключение контекста, вызванное простой вставкой ссылки в чат.</span><span class="sxs-lookup"><span data-stu-id="e5f12-416">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="e5f12-417">Эти сведения вставляются в виде легко читаемой карточки с автоматическим форматированием, помогая пользователям оставаться в диалоге.</span><span class="sxs-lookup"><span data-stu-id="e5f12-417">The information is inserted as an easy-to-read auto-formatted card, helping your users stay engaged in the conversation.</span></span>

[<span data-ttu-id="e5f12-418">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-418">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Приложение поиска списка](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="e5f12-420">Проверка сотрудников</span><span class="sxs-lookup"><span data-stu-id="e5f12-420">Staff Check-ins</span></span>

<span data-ttu-id="e5f12-421">Проверки персонала — это приложение на основе [Power Apps,](/powerapps/powerapps-overview)которое позволяет контролировать взаимодействие между вашим бизнес-персоналом и сотрудниками на местах.</span><span class="sxs-lookup"><span data-stu-id="e5f12-421">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview)-based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="e5f12-422">Сотрудники могут легко предоставлять критически важные сведения и обновления состояния как по расписанию, так и по расписанию непосредственно из Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-422">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="e5f12-423">Приложение поддерживает расположение, фотографии и заметки в режиме реального времени, а также уведомления напоминаний и автоматизированные процессы.</span><span class="sxs-lookup"><span data-stu-id="e5f12-423">The app supports real-time location, photos, and notes as well as reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="e5f12-424">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-424">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Создание представления для регистрации](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="e5f12-426">Опрос</span><span class="sxs-lookup"><span data-stu-id="e5f12-426">Survey</span></span>

<span data-ttu-id="e5f12-427">Опрос — это пользовательское приложение расширения обмена сообщениями Microsoft [Teams,](../messaging-extensions/what-are-messaging-extensions.md) которое позволяет создавать опрос в чате или канале для сбора данных и получения информации о действиях.</span><span class="sxs-lookup"><span data-stu-id="e5f12-427">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span>  <span data-ttu-id="e5f12-428">Приложение поддерживается во всех клиентах платформы Teams ( настольных компьютерах, браузерах, iOS и Android) и готово к развертыванию в рамках подписки на Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="e5f12-428">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="e5f12-429">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-429">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Создание опроса в представлении Teams](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="virtual-rounding-9734"></a><span data-ttu-id="e5f12-431">Виртуальные &#9734;</span><span class="sxs-lookup"><span data-stu-id="e5f12-431">Virtual Rounding &#9734;</span></span>

<span data-ttu-id="e5f12-432">Поставщики услуг здравоохранения и экстренных служб делают десятки и сотни "кругов" в день.</span><span class="sxs-lookup"><span data-stu-id="e5f12-432">Hospital and emergency room providers make dozens, and often hundreds of “rounds” per day.</span></span> <span data-ttu-id="e5f12-433">Эти быстрые проверки состояния пациентов призваны предоставить проверку состояния и убедиться, что проблемы с этим человеком решены.</span><span class="sxs-lookup"><span data-stu-id="e5f12-433">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="e5f12-434">Хотя округление является важной практикой для отслеживания пациентов несколькими типами поставщиков, они представляют собой огромное сток на PPE, так как для каждого посещения, от каждого поставщика, необходимо использовать новую маску и новый набор перчаток.</span><span class="sxs-lookup"><span data-stu-id="e5f12-434">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves must be used.</span></span> <span data-ttu-id="e5f12-435">С помощью этих шаблонов приложений медицинские работники могут без труда проводить круги виртуально через собрание Microsoft Teams между поставщиком и пациентов.</span><span class="sxs-lookup"><span data-stu-id="e5f12-435">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="e5f12-436">На решение virtual Rounding также ссылается запись блога Microsoft Health and Life [Sciences.](https://aka.ms/teamsvirtualrounding)</span><span class="sxs-lookup"><span data-stu-id="e5f12-436">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="e5f12-437">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-437">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Виртуальное округление](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="e5f12-439">Управление посетителями</span><span class="sxs-lookup"><span data-stu-id="e5f12-439">Visitor Management</span></span>

<span data-ttu-id="e5f12-440">Приложение "Управление посетителями" позволяет вашей организации и сотрудникам легко и эффективно управлять процессом посетителей на сайте непосредственно из Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e5f12-440">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="e5f12-441">Приложение позволяет сотрудникам создавать запросы посетителей, централизованно отслеживать состояние запроса через панель мониторинга посетителей и получать уведомления в режиме реального времени, когда посетитель поступает.</span><span class="sxs-lookup"><span data-stu-id="e5f12-441">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="e5f12-442">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-442">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

:::row:::
  :::column span="2":::
    ![Создание представления запроса](../assets/images/visitor-management-create-request.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Уведомление о поступлении посетителей](../assets/images/visitor-management-notify-host.png)
:::column-end:::
:::row-end:::

## <a name="workplace-awards"></a><span data-ttu-id="e5f12-445">WorkplaceS</span><span class="sxs-lookup"><span data-stu-id="e5f12-445">Workplace Awards</span></span>

<span data-ttu-id="e5f12-446">Рабочая компания — это шаблон приложения Teams, который обеспечивает положительные основы для распознавания и поощрения культуры сотрудников на современном рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="e5f12-446">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="e5f12-447">Приложение позволяет настроить программу поощрений и распознавания сотрудников (R&R), в которой сотрудники могут легко назначать и поддерживать коллег, а ваш лидер R&R может просматривать отправленные назначения, предоставлять награды и объявлять получателей.</span><span class="sxs-lookup"><span data-stu-id="e5f12-447">The app enables you to setup and manage an employee rewards and recognition (R&R) program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="e5f12-448">Get it on GitHub</span><span class="sxs-lookup"><span data-stu-id="e5f12-448">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="e5f12-449">Карточка назначения рабочих мест</span><span class="sxs-lookup"><span data-stu-id="e5f12-449">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Вкладка "Список рабочих мест"](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="e5f12-451">Есть идеи о шаблоне приложения, который вы хотите увидеть?</span><span class="sxs-lookup"><span data-stu-id="e5f12-451">Have an idea for an app template you'd like to see?</span></span> <span data-ttu-id="e5f12-452">[Сообщите нам.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)</span><span class="sxs-lookup"><span data-stu-id="e5f12-452">[Please let us know](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>
