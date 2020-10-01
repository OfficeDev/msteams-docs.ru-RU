---
title: Шаблоны приложений Microsoft Teams
description: Ссылки и описания шаблонов приложений для платформы Microsoft Teams
ms.topic: reference
keywords: Демонстрация примеров шаблонов Microsoft Teams
ms.openlocfilehash: a3f9090526a92fba3f6cebe13a973cebeb056889
ms.sourcegitcommit: e92408e751a8f51028908ab7e2415a8051a536c0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2020
ms.locfileid: "48326368"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="eaabf-104">Шаблоны приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="eaabf-104">App Templates for Microsoft Teams</span></span>

<span data-ttu-id="eaabf-105">Шаблоны приложений — это готовые к работе приложения для Microsoft Teams, которые основаны на сообществах, Открытый источник и доступны на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="eaabf-105">App templates are production-ready apps for Microsoft Teams that are community driven, open-source, and available on GitHub.</span></span> <span data-ttu-id="eaabf-106">Каждый из них содержит подробные инструкции по развертыванию и установке этого приложения для вашей организации, предоставляя готовые к использованию приложение, которое можно установить и приступить к работе немедленно.</span><span class="sxs-lookup"><span data-stu-id="eaabf-106">Each contains detailed instructions for deploying and installing that app for your organization, providing a ready-to-use app that you can install and begin using immediately.</span></span> <span data-ttu-id="eaabf-107">Полный исходный код также доступен, поэтому вы можете изучить его подробно или разветвление кода и измените его в соответствии с вашими потребностями.</span><span class="sxs-lookup"><span data-stu-id="eaabf-107">The complete source code is available as well, so you can explore it in detail, or fork the code and alter it to meet your specific needs.</span></span>

<span data-ttu-id="eaabf-108">**&#9734; указывает на новые выпущенные шаблоны приложений.**</span><span class="sxs-lookup"><span data-stu-id="eaabf-108">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="eaabf-109">Основные преимущества</span><span class="sxs-lookup"><span data-stu-id="eaabf-109">Key benefits</span></span>

* <span data-ttu-id="eaabf-110">**Интерфейс Plug and Play:** Все шаблоны приложений включают в себя сценарии развертывания, позволяющие размещать все необходимые службы в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eaabf-110">**Plug and play experience:** All app templates include deployments scripts that will allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="eaabf-111">Для развертывания приложений не требуется написания кода.</span><span class="sxs-lookup"><span data-stu-id="eaabf-111">No coding is required to deploy the apps.</span></span>
* <span data-ttu-id="eaabf-112">**Код, готовый для производства:** Шаблоны приложений соответствуют рекомендуемым рекомендациям по безопасности и инфраструктуре, а все отправленные в них изменения проверяются на предмет продолженности.</span><span class="sxs-lookup"><span data-stu-id="eaabf-112">**Production-ready code:** The app templates conform to recommended best practices around security and infrastructure, and all community submitted changes to them are reviewed to ensure continued conformance.</span></span>
* <span data-ttu-id="eaabf-113">**Настраиваемые и расширяемые:** Несмотря на то, что все шаблоны приложений готовы к развертыванию в соответствии с этим, мы предоставляем полные базы кода и сценарии развертывания, чтобы вы могли легко настраивать их и расширять их в соответствии с вашими потребностями.</span><span class="sxs-lookup"><span data-stu-id="eaabf-113">**Customizable and extensible:** While all app templates are ready to deploy as they are, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="eaabf-114">**Подробная документация & поддержки:** Все шаблоны приложений сопровождаются сквозной документацией по архитектуре, развертыванию и этапам настройки решения.</span><span class="sxs-lookup"><span data-stu-id="eaabf-114">**Detailed documentation & support:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="eaabf-115">Репозитории также отслеживаются, поэтому сообщите о возникших проблемах, вызывая проблему в GitHub.</span><span class="sxs-lookup"><span data-stu-id="eaabf-115">The repositories are monitored as well, so please report any issues you encounter by raising an Issue on GitHub.</span></span>

## <a name="ask-away-9734"></a><span data-ttu-id="eaabf-116">Запрос "нет на месте" &#9734;</span><span class="sxs-lookup"><span data-stu-id="eaabf-116">Ask Away &#9734;</span></span>

<span data-ttu-id="eaabf-117">Ask — это [робот Microsoft Teams](../bots/what-are-bots.md) , который позволяет пользователям выполнять сеансы связи в Teams с помощью Q&(вопросов и ответов).</span><span class="sxs-lookup"><span data-stu-id="eaabf-117">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Q&A (Question and Answer) sessions within Teams.</span></span> <span data-ttu-id="eaabf-118">С помощью ленты "запрос отсутствия" участники группы могут отсылать и получать вопросы, предоставляемые коллегами, позволяя Q&ведущим узлам легко собирать свои вопросы в канале или чате.</span><span class="sxs-lookup"><span data-stu-id="eaabf-118">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="eaabf-119">Bot можно использовать для проведения реального времени Q&сеанса в собрании Teams и позволяет участникам передавать вопросы через чат.</span><span class="sxs-lookup"><span data-stu-id="eaabf-119">The bot can be used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live via chat.</span></span>

[<span data-ttu-id="eaabf-120">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-120">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Представление всплывающего диалогового окна леадербоард, в котором пользователи могут голосовать по вопросам](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="eaabf-122">Вспомогательная аналитика</span><span class="sxs-lookup"><span data-stu-id="eaabf-122">Associate Insights</span></span>

<span data-ttu-id="eaabf-123">Сопоставить Insights — это шаблон [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) , который позволяет сотрудникам задействование напрямую собирать и передавать мнения пользователей, мнений и восприятия.</span><span class="sxs-lookup"><span data-stu-id="eaabf-123">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="eaabf-124">Задействование сотрудники часто являются первым представителем компании для общения с клиентами из одной точки контакта "один к одному".</span><span class="sxs-lookup"><span data-stu-id="eaabf-124">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="eaabf-125">Собранные данные можно совместно использовать и совместно использовать в бизнес-группах, например, с помощью вкладки Power BI Teams, чтобы улучшить продукт и улучшить взаимодействие с пользователем.</span><span class="sxs-lookup"><span data-stu-id="eaabf-125">The collected data can be shared and used collaboratively by business teams, e.g., via a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="eaabf-126">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-126">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![Представление отзывов о созданном приложении](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Представление Power BI, созданное приложением](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="eaabf-129">Присутствие</span><span class="sxs-lookup"><span data-stu-id="eaabf-129">Attendance</span></span>

<span data-ttu-id="eaabf-130">Приложение для посещения — это вкладка " [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) ", которую можно закрепить в команде.</span><span class="sxs-lookup"><span data-stu-id="eaabf-130">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that can be pinned in a team.</span></span> <span data-ttu-id="eaabf-131">Он предназначен для записи сведений о присутствии, как правило, в настройках, таких как среды обучения и обучения.</span><span class="sxs-lookup"><span data-stu-id="eaabf-131">It is designed to record presence, typically in settings such as learning and training environments.</span></span> <span data-ttu-id="eaabf-132">Пользователи могут пометить или изменить сведения о присутствии в течение 30 дней, а также просмотреть обобщенные отчеты о посещаемости для целой группы или отдельных участников.</span><span class="sxs-lookup"><span data-stu-id="eaabf-132">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span>

[<span data-ttu-id="eaabf-133">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-133">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![Демонстрация приложения для посещения](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="eaabf-135">Книга — a — комната</span><span class="sxs-lookup"><span data-stu-id="eaabf-135">Book-a-room</span></span>

<span data-ttu-id="eaabf-136">Book-a-комната — это [робот Microsoft Teams](../bots/what-are-bots.md) , который позволяет пользователям быстро находить и зарезервировать комнату для собраний в течение 30 (по умолчанию), 60 или 90 минут, начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="eaabf-136">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="eaabf-137">Области Bot "книга — комната" для личных или 1:1 бесед.</span><span class="sxs-lookup"><span data-stu-id="eaabf-137">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

[<span data-ttu-id="eaabf-138">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-138">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![Пример книги "a – комната"](../assets/images/book-a-room.png)

## <a name="building-access-9734"></a><span data-ttu-id="eaabf-140">&#9734; доступа для построения</span><span class="sxs-lookup"><span data-stu-id="eaabf-140">Building Access &#9734;</span></span>

<span data-ttu-id="eaabf-141">Сборка Access — это приложение на основе Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/), которое поддерживает администрирование пороговых значений для заполнения и норм дистанЦинг, позволяя директорам по управлению, отслеживать и сообщать о присутствии на сайтах сотрудников.</span><span class="sxs-lookup"><span data-stu-id="eaabf-141">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="eaabf-142">Приложение, созданное с помощью Microsoft [Power Apps](/powerapps/powerapps-overview)и [Автоматизация управления питанием](/power-automate/getting-started), глубоко интегрируется с Microsoft Teams и позволяет организациям определять готовность к построению, устанавливать критерии приемлемости для доступа на уровне сайта и собирать ценные сведения для будущего планирования.</span><span class="sxs-lookup"><span data-stu-id="eaabf-142">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="eaabf-143">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-143">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Построение карточки резервирования Access](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Представление ключа доступа для построения](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="eaabf-146">Праздники</span><span class="sxs-lookup"><span data-stu-id="eaabf-146">Celebrations</span></span>

<span data-ttu-id="eaabf-147">Целебратионс — это приложение Teams, помогающее участникам группы отпраздновать все дни рождения, годовщины и другие повторяющиеся события.</span><span class="sxs-lookup"><span data-stu-id="eaabf-147">Celebrations is a Teams app that helps team members celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="eaabf-148">Он запоминает особые события всех участников группы и отправляет понятное сообщение во всех командах, выбранных во время создания события, чтобы сделать участников группы особенными в течение дня.</span><span class="sxs-lookup"><span data-stu-id="eaabf-148">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="eaabf-149">Приложение предоставляет простой интерфейс для всех участников группы, позволяющий лично добавлять и просматривать события, а также позволяет пользователю выбирать команды, к которым эти события имеют общий доступ.</span><span class="sxs-lookup"><span data-stu-id="eaabf-149">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="eaabf-150">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-150">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="company-communicator"></a><span data-ttu-id="eaabf-151">Корпоративный Communicator</span><span class="sxs-lookup"><span data-stu-id="eaabf-151">Company Communicator</span></span>

<span data-ttu-id="eaabf-152">Приложение Communicator позволяет корпоративным командам создавать и отправлять сообщения, предназначенные для нескольких групп или большого количества сотрудников, с помощью чата, позволяя организациям достигать сотрудников, где они работают.</span><span class="sxs-lookup"><span data-stu-id="eaabf-152">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="eaabf-153">Используйте этот шаблон для нескольких сценариев, таких как новые объявления о инициативах, подключение сотрудников, современные обучающие и разработки, а также широковещательные рассылки по всей Организации.</span><span class="sxs-lookup"><span data-stu-id="eaabf-153">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="eaabf-154">Приложение предоставляет удобный интерфейс для пользователей, которые могут создавать, просматривать, сотрудничать и отправлять сообщения.</span><span class="sxs-lookup"><span data-stu-id="eaabf-154">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="eaabf-155">Он предоставляет основу для создания настраиваемых целевых возможностей взаимодействия, таких как настраиваемая телеметрии, количество пользователей, подтвержденных или взаимодействующих с сообщением.</span><span class="sxs-lookup"><span data-stu-id="eaabf-155">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="eaabf-156">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-156">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![представление Жкомпани Communicator "создание"](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup-9734"></a><span data-ttu-id="eaabf-158">&#9734; подстановки группы контактов</span><span class="sxs-lookup"><span data-stu-id="eaabf-158">Contact Group Lookup &#9734;</span></span>

<span data-ttu-id="eaabf-159">Приложение для поиска групп контактов предоставляет удобный и удобный подход для создания групп контактов Организации, доступа к ним и управления ими (ранее назывался списками рассылки или группами связи), а также для управления ими.</span><span class="sxs-lookup"><span data-stu-id="eaabf-159">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups (formerly known as distribution lists or communication groups).</span></span> <span data-ttu-id="eaabf-160">Пользователи могут быстро просматривать и общаться с участниками группы, просматривать состояние участника и создавать групповые беседы с выбранными участниками в группе контактов в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-160">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="eaabf-161">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-161">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![Просмотр закрепленных элементов списка контактов группы контактов](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр группы контактов начать демонстрацию чата](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="crowdsourcer"></a><span data-ttu-id="eaabf-164">кровдсаурцер</span><span class="sxs-lookup"><span data-stu-id="eaabf-164">CrowdSourcer</span></span>

<span data-ttu-id="eaabf-165">Кровдсаурцер — это [робот Microsoft Teams](../bots/what-are-bots.md) , с помощью которого в Teams запрашиваются сведения, предназначенные для сотрудничества из членов группы.</span><span class="sxs-lookup"><span data-stu-id="eaabf-165">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="eaabf-166">Это отличный способ ответить на часто задаваемые вопросы, в то же время позволяя участникам активно привлекать участие в информационных ресурсах и привлекать к ним.</span><span class="sxs-lookup"><span data-stu-id="eaabf-166">It's a great way to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="eaabf-167">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-167">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Взаимодействие с пользователем выносите](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="eaabf-169">Пользовательские наклейки</span><span class="sxs-lookup"><span data-stu-id="eaabf-169">Custom Stickers</span></span>

<span data-ttu-id="eaabf-170">Само выражение является ядром для работоспособного командного языка.</span><span class="sxs-lookup"><span data-stu-id="eaabf-170">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="eaabf-171">Этот шаблон приложения — это [расширение системы обмена сообщениями](~/messaging-extensions/what-are-messaging-extensions.md) , которое позволяет пользователям использовать настраиваемые наклейки и GIF в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-171">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="eaabf-172">Этот шаблон предоставляет простую веб-конфигурацию, где любой пользователь, имеющий доступ к настройке, может отправлять GIF-файлы, наклейки и изображения, которые должны иметь пользователи, позволяя всей группе использовать любой выбранный набор наклеек.</span><span class="sxs-lookup"><span data-stu-id="eaabf-172">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs/stickers/images they want their end-users to have, allowing your entire team to use any set of stickers you chose.</span></span>

<span data-ttu-id="eaabf-173">Кроме того, это приложение позволяет легко предоставлять общий доступ к изображениям/GIF/наклеек в Teams, не требуя доступа к сайтам SharePoint или отдельным каналам в качестве механизмов хранения и совместного использования.</span><span class="sxs-lookup"><span data-stu-id="eaabf-173">This app also enables easy sharing of images/GIFs/stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="eaabf-174">Например, Teams могут легко совместно использовать изображения и изображения для социальных сетей, отделов маркетинга и сбыта программными продуктами.</span><span class="sxs-lookup"><span data-stu-id="eaabf-174">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="eaabf-175">Кроме того, можно расширить это приложение, выполнив процесс обработки уведомлений определенным группам или отдельным пользователям, если доступны новые изображения/GIF-файлы.</span><span class="sxs-lookup"><span data-stu-id="eaabf-175">One can also extend this app by triggering a notification flow to specific teams/individuals when new images/GIFs are made available.</span></span>

[<span data-ttu-id="eaabf-176">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-176">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Приложение для наклеек](../assets/images/stickers.png)

## <a name="e-prescriptions-9734"></a><span data-ttu-id="eaabf-178">&#9734; для создания отделой электронной почты</span><span class="sxs-lookup"><span data-stu-id="eaabf-178">E-Prescriptions &#9734;</span></span> 

<span data-ttu-id="eaabf-179">E-сценарии — это приложение на основе [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app), расширяющее телемедиЦине и виртуальную осторожность путем автоматизации процесса выдачи электронных данных в пострадавшие.</span><span class="sxs-lookup"><span data-stu-id="eaabf-179">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)-based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="eaabf-180">Медицинские специалисты могут быстро просматривать встречи, создавать электронную расправку и отправлять электронные сообщения с вложениями e-рецептов непосредственно в платформу Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-180">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="eaabf-181">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-181">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![Снимок экрана приложения "электронное письмо".](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Снимок экрана приложения "электронное письмо".](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="eaabf-186">Экспертный поиск</span><span class="sxs-lookup"><span data-stu-id="eaabf-186">Expert Finder</span></span>

<span data-ttu-id="eaabf-187">"Экспертный Поиск" — это [робот Microsoft Teams](../bots/what-are-bots.md) , который определяет конкретные элементы Организации на основе их навыков, интересов и образовательных атрибутов.</span><span class="sxs-lookup"><span data-stu-id="eaabf-187">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="eaabf-188">Участники находит экспертов в Организации, которые отвечают за поиск по ключевым словам в профилях пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eaabf-188">Members find experts within an organization  that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="eaabf-189">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-189">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Пример результатов поиска для экспертного поиска](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="eaabf-191">Вопросы и ответы плюс</span><span class="sxs-lookup"><span data-stu-id="eaabf-191">FAQ Plus</span></span>

<span data-ttu-id="eaabf-192">Сеанс Q&Боты — это простой способ предоставления ответов на часто задаваемые вопросы для пользователей.</span><span class="sxs-lookup"><span data-stu-id="eaabf-192">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="eaabf-193">Тем не менее, большинство Боты не приведут к работе с пользователями, так как в цикле произойдет сбой ленты.</span><span class="sxs-lookup"><span data-stu-id="eaabf-193">However, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="eaabf-194">"Вопросы и ответы" — это удобный Q&Bot, который присоединяется к циклу, когда он не может помочь.</span><span class="sxs-lookup"><span data-stu-id="eaabf-194">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="eaabf-195">Один может попросить присвоить ему ответ и ответить на него, если он присутствует в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="eaabf-195">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="eaabf-196">В противном случае, Bot позволяет пользователю отправить запрос, который затем отправляется в предварительно настроенную группу экспертов, которые помогают обеспечить поддержку, действуя с уведомлениями от самой команды.</span><span class="sxs-lookup"><span data-stu-id="eaabf-196">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="eaabf-197">Последний выпуск **часто задаваемых вопросов, а также** усовершенствованный выпуск Q&решения, позволяющий группе экспертов выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="eaabf-197">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="eaabf-198">&#x2714; добавить новые&Q непосредственно в базу знаний с помощью расширений сообщений.</span><span class="sxs-lookup"><span data-stu-id="eaabf-198">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="eaabf-199">&#x2714; изменить и удалить Q&пары, добавленные с помощью Bot.</span><span class="sxs-lookup"><span data-stu-id="eaabf-199">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="eaabf-200">&#x2714; отслеживания истории изменений Q&AS.</span><span class="sxs-lookup"><span data-stu-id="eaabf-200">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="eaabf-201">&#x2714; настроить ответ с дополнительными сведениями для отображения в виде [адаптивной карточки](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span><span class="sxs-lookup"><span data-stu-id="eaabf-201">&#x2714; Configure an answer with additional details to display as an [adaptive card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="eaabf-202">**Получение на сайте GitHub**</span><span class="sxs-lookup"><span data-stu-id="eaabf-202">**Get it on GitHub**</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![Вопросы и ответы в формате GIF](../assets/images/FAQPlusEndUser.gif)

## <a name="goal-tracker"></a><span data-ttu-id="eaabf-204">Средство отслеживания целей</span><span class="sxs-lookup"><span data-stu-id="eaabf-204">Goal Tracker</span></span>

<span data-ttu-id="eaabf-205">Приложение-средство отслеживания целей — это комплексное решение, которое позволяет вашей организации поддерживать целевые задачи, наблюдать за ходом выполнения и подтверждать успех в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-205">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="eaabf-206">Приложение позволяет пользователям устанавливать, отслеживать и обновлять цели на профессиональном, персональном уровне и уровне группы.</span><span class="sxs-lookup"><span data-stu-id="eaabf-206">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="eaabf-207">Участники групп также получают своевременные напоминания и обновления состояния, которые остаются неизменными и постоянно отслеживаются.</span><span class="sxs-lookup"><span data-stu-id="eaabf-207">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="eaabf-208">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-208">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![Задание целей](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Задачи набора представлений](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a><span data-ttu-id="eaabf-211">Великолепные идеи</span><span class="sxs-lookup"><span data-stu-id="eaabf-211">Great Ideas</span></span>

<span data-ttu-id="eaabf-212">Приложение с замечательными идеями поддерживает инновации и творческие возможности в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="eaabf-212">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="eaabf-213">Приложение позволяет вашим сотрудникам обмениваться идеями с коллегами и лидерами, находить новые отправки, полезные сведения о недоходе и приводить их голосование для лучших предложений в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-213">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="eaabf-214">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-214">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a><span data-ttu-id="eaabf-217">Групповые действия</span><span class="sxs-lookup"><span data-stu-id="eaabf-217">Group Activities</span></span>

<span data-ttu-id="eaabf-218">Групповые действия — это приложение Microsoft Teams, которое упрощает владельцам команд быстрое создание групп действий и управление рабочими процессами совместной работы в контексте Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-218">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="eaabf-219">Авторы действий имеют возможность создавать действия, случайным образом распределять участников групп в группах и при необходимости отправлять напоминания от ленты до завершения действий.</span><span class="sxs-lookup"><span data-stu-id="eaabf-219">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="eaabf-220">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-220">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Список групповых действий в Teams](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Сообщение об активности группы в канале](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="grow-your-skills"></a><span data-ttu-id="eaabf-223">Развивайте свои навыки</span><span class="sxs-lookup"><span data-stu-id="eaabf-223">Grow Your Skills</span></span>

<span data-ttu-id="eaabf-224">Приложение "расширение навыков" обеспечивает профессиональный рост и разработку, позволяя сотрудникам участвовать в дополнительных проектах Организации, одновременно изучении новых навыков.</span><span class="sxs-lookup"><span data-stu-id="eaabf-224">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="eaabf-225">Сотрудники могут использовать приложение для обнаружения возможностей, соответствующих интересам, для совместной работы с коллегами и получения новых уровней опыта и возможностей в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-225">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="eaabf-226">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-226">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![Представление доступных проектов](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Представление навыков, полученное в средстве просмотра](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a><span data-ttu-id="eaabf-229">Поддержка управления персоналом</span><span class="sxs-lookup"><span data-stu-id="eaabf-229">HR Support</span></span>

<span data-ttu-id="eaabf-230">"Поддержка отдела кадров" — это удобный Q&Bot, который применяет специалист по поддержке и эксперт в цикле в цикле, когда он не может помочь.</span><span class="sxs-lookup"><span data-stu-id="eaabf-230">HR Support bot is a friendly Q&A bot that brings a support professional/expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="eaabf-231">Один может попросить присвоить ему ответ и ответить на него, если он присутствует в базе знаний.</span><span class="sxs-lookup"><span data-stu-id="eaabf-231">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="eaabf-232">В противном случае, Bot позволяет пользователю отправить запрос, который затем публикуется в предварительно настроенной группе экспертов, которые помогают обеспечить поддержку, действуя с уведомлениями от самой команды.</span><span class="sxs-lookup"><span data-stu-id="eaabf-232">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="eaabf-233">Кроме того, он предлагает ссылки на Рекомендуемые вопросы и вопросы отдела кадров, выполняя поиск предварительно настроенных тегов в вопросе.</span><span class="sxs-lookup"><span data-stu-id="eaabf-233">Additionally, the bot suggests links to recommended HR policies/questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="eaabf-234">Эти плитки также можно найти в соответствующей вкладке в качестве краткого справочника.</span><span class="sxs-lookup"><span data-stu-id="eaabf-234">These tiles can also be found in the associated tab as a quick reference.</span></span> <span data-ttu-id="eaabf-235">Поддержка отдела кадров хорошо подходит для легких КНА и обеспечения быстрой поддержки при запуске новых проектов и инициатив в Организации.</span><span class="sxs-lookup"><span data-stu-id="eaabf-235">HR Support works well for light weight QnA and to provide quick support when launching new projects/initiatives in the organization.</span></span>

[<span data-ttu-id="eaabf-236">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-236">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Поддержка управления персоналом](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="eaabf-238">Точки соприкосновения</span><span class="sxs-lookup"><span data-stu-id="eaabf-238">Icebreaker</span></span>

<span data-ttu-id="eaabf-239">Ицебреакер — это [робот Microsoft](../bots/what-are-bots.md) Teams, который помогает команде получить более тесное соединение двух случайных участников группы за каждую неделю.</span><span class="sxs-lookup"><span data-stu-id="eaabf-239">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="eaabf-240">С помощью ленты Bot легко планироваться, автоматически предлагая свободное время работы для обоих участников.</span><span class="sxs-lookup"><span data-stu-id="eaabf-240">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="eaabf-241">Укрепите личные подключения и создавайте тесно кните сообщество с этим приложением.</span><span class="sxs-lookup"><span data-stu-id="eaabf-241">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="eaabf-242">В дополнение к поощрению персональных подключений во всей команде приложение Ицебреакер может помочь култивате в организации сообщества на основе процентов.</span><span class="sxs-lookup"><span data-stu-id="eaabf-242">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="eaabf-243">Например, вы можете использовать это приложение для группы процентов DevOps, чтобы помочь идеям и рекомендациям по распределению в Организации.</span><span class="sxs-lookup"><span data-stu-id="eaabf-243">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="eaabf-244">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-244">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Приложение ицебреакер](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="eaabf-246">Стимул</span><span class="sxs-lookup"><span data-stu-id="eaabf-246">Incentives</span></span>

<span data-ttu-id="eaabf-247">Поощрения — это шаблон [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) , который управляет и отслеживает участие сотрудников инцентивизед в назначенных действиях, например обучение и инициативах по управлению изменениями.</span><span class="sxs-lookup"><span data-stu-id="eaabf-247">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities such as trainings and change management initiatives.</span></span> <span data-ttu-id="eaabf-248">Администраторы используют приложение для установки назначенных действий, назначения баллов для завершения и указания необходимых уровней точки соответствия для вознаграждения.</span><span class="sxs-lookup"><span data-stu-id="eaabf-248">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="eaabf-249">Сотрудники используют приложение для просмотра накопленных баллов и, при достижении требований приемлемости, запросов и утверждений.</span><span class="sxs-lookup"><span data-stu-id="eaabf-249">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="eaabf-250">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-250">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Демонстрация приложения поощрения](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="eaabf-252">Средство отчетов об инцидентах</span><span class="sxs-lookup"><span data-stu-id="eaabf-252">Incident Reporter</span></span> 

<span data-ttu-id="eaabf-253">Служба происшествий — это [робот Microsoft Teams](../bots/what-are-bots.md)  , который оптимизирует управление происшествиями в Организации.</span><span class="sxs-lookup"><span data-stu-id="eaabf-253">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="eaabf-254">Bot облегчает автоматическое сбор данных об инцидентах, настраиваемых отчетах об инцидентах, соответствующих уведомлениях заинтересованных лиц и Сквозное отслеживание инцидентов.</span><span class="sxs-lookup"><span data-stu-id="eaabf-254">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="eaabf-255">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-255">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![Представление "область группы инцидентов"](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Представление "личная область инцидентов"](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="eaabf-258">Открытые эмблемы</span><span class="sxs-lookup"><span data-stu-id="eaabf-258">Open Badges</span></span>

<span data-ttu-id="eaabf-259">Открытые эмблемы это приложение Microsoft Teams, которое позволяет сотрудникам получать цифровые обучающие эмблемы в контексте Teams и делиться ими везде.</span><span class="sxs-lookup"><span data-stu-id="eaabf-259">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="eaabf-260">С помощью возможностей, предоставляемых сторонним цифровым цифровым логотипом, [бадгр](https://badgr.org/), выдаваемые эмблемы записываются в профиле бадгр получателя и доступны для создания привлекательного изображения жизненного цикла обучения.</span><span class="sxs-lookup"><span data-stu-id="eaabf-260">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="eaabf-261">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-261">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![Изображение доступных эмблем](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Просмотр карточек с выдачами](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="eaabf-264">Быстрые ответы</span><span class="sxs-lookup"><span data-stu-id="eaabf-264">Quick Responses</span></span>

<span data-ttu-id="eaabf-265">Быстрые ответы — это приложение Microsoft Teams, которое предоставляет надежное решение для эффективного ответа на часто задаваемые вопросы о пользователях (FAQ).</span><span class="sxs-lookup"><span data-stu-id="eaabf-265">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions (FAQs).</span></span> <span data-ttu-id="eaabf-266">Вместо того чтобы отвечать на запросы вручную и непрерывно повторять сведения, приложение будет создавать библиотеку ответов для интерактивного взаимодействия с пользователем с помощью [расширений системы обмена сообщениями](../messaging-extensions/what-are-messaging-extensions.md)Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-266">Instead of answering each query manually and  continuously repeating information, the app will build a library of responses for an interactive user experience via Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="eaabf-267">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-267">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Пример представления ответов](../assets/images/quick-responses.png)

## <a name="remote-support"></a><span data-ttu-id="eaabf-269">Удаленная поддержка</span><span class="sxs-lookup"><span data-stu-id="eaabf-269">Remote Support</span></span>

<span data-ttu-id="eaabf-270">Удаленная поддержка это [робот Microsoft Teams](../bots/what-are-bots.md) , который обеспечивает сфокусированный интерфейс между специалистами службы поддержки в Организации и группой внутренней поддержки.</span><span class="sxs-lookup"><span data-stu-id="eaabf-270">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="eaabf-271">Конечные пользователи могут отправлять, изменять и отзывать запросы для поддержки, а группа поддержки может отвечать на запросы, управлять ими и обновлять их на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-271">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="eaabf-272">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-272">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![Запрос формы поддержки](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Сведения о поддержке запросов](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a><span data-ttu-id="eaabf-275">Запрос от a до команды</span><span class="sxs-lookup"><span data-stu-id="eaabf-275">Request-a-team</span></span>

<span data-ttu-id="eaabf-276">Request-a-Team — это приложение Microsoft Teams, которое оптимизирует создание группы в Организации.</span><span class="sxs-lookup"><span data-stu-id="eaabf-276">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="eaabf-277">Приложение поддерживает стандартизацию и рекомендации при создании новых экземпляров групп с помощью интеграции формы запроса с помощью мастера, встроенного процесса утверждения, панели мониторинга состояния запроса и автоматизированных командных построений.</span><span class="sxs-lookup"><span data-stu-id="eaabf-277">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="eaabf-278">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-278">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![Представление "запрос" — представление начальной страницы для команды](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Представление страницы мастера запросов-a-Team](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a><span data-ttu-id="eaabf-281">Scrum для каналов</span><span class="sxs-lookup"><span data-stu-id="eaabf-281">Scrums for Channels</span></span>

<span data-ttu-id="eaabf-282">Scrum-каналы — это приложение Scrum Assistant, которое позволяет пользователям планировать и запускать Scrum-каналы в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-282">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="eaabf-283">Приложение отлично подходит для удаленных Teams и Teams, состоящих из различных географических мест и часовых поясов, которые позволяют обмениваться ежедневными обновлениями и обеспечивать участие в собрании Scrum.</span><span class="sxs-lookup"><span data-stu-id="eaabf-283">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="eaabf-284">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-284">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="eaabf-285">Для проведения Scrum собраний в разделе "чат" обратитесь к статье [Scrum для шаблона приложения группового чата](#scrums-for-group-chat) .</span><span class="sxs-lookup"><span data-stu-id="eaabf-285">To conduct scrum meetings in a group chat, please see our [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

:::row:::
  :::column span="2":::
    ![Scrum для представления параметров каналов](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Scrum для представления состояния участников группы "каналы"](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a><span data-ttu-id="eaabf-288">Scrum для группового чата</span><span class="sxs-lookup"><span data-stu-id="eaabf-288">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="eaabf-289">Шаблон приложения "состояние Scrum" обновлен и теперь является Scrum-Scrum для группового чата.</span><span class="sxs-lookup"><span data-stu-id="eaabf-289">The Scrums Status app template has been updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="eaabf-290">Scrum-сообщения для группового чата — это вспомогательный помощник Scrum, который позволяет участникам группового чата выполнять асинхронные автономные собрания и легко совместно использовать их ежедневное обновление.</span><span class="sxs-lookup"><span data-stu-id="eaabf-290">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="eaabf-291">Он позволяет всем участникам группового чата вносить изменения в Scrum и просматривать изменения, внесенные другими пользователями в запущенном Scrum.</span><span class="sxs-lookup"><span data-stu-id="eaabf-291">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="eaabf-292">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-292">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Scrum для демонстрации для группового чата](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now-9734"></a><span data-ttu-id="eaabf-294">Поделиться сейчас &#9734;</span><span class="sxs-lookup"><span data-stu-id="eaabf-294">Share Now &#9734;</span></span>

<span data-ttu-id="eaabf-295">Приложение Share Now способствует положительному обмену данными между коллегами, позволяя пользователям легко обмениваться контентом в среде Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-295">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="eaabf-296">Пользователи применяют приложение для обмена интересующими элементами с участниками группы, обнаружения нового общего контента, установки предпочтений и избранных закладок для последующего просмотра.</span><span class="sxs-lookup"><span data-stu-id="eaabf-296">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="eaabf-297">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-297">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Выбор представления контента](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="eaabf-299">Поиск в списке SharePoint</span><span class="sxs-lookup"><span data-stu-id="eaabf-299">SharePoint List Search</span></span>

<span data-ttu-id="eaabf-300">Совместная работа в Microsoft Teams довольно часто ссылается на информацию, содержащуюся в элементах списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="eaabf-300">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="eaabf-301">При простом вставке ссылки на элемент в вопросе всем пользователям переключается контекст из беседы, находятся необходимые сведения, а затем возвращается в Teams для продолжения беседы.</span><span class="sxs-lookup"><span data-stu-id="eaabf-301">Simply pasting a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="eaabf-302">По мере продолжения беседы обычно пользователям потребуется несколько раз вернуться к элементу ссылки, чтобы проверить новые комментарии и обновить их воспоминания.</span><span class="sxs-lookup"><span data-stu-id="eaabf-302">As the conversation continues typically people will have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="eaabf-303">Это контекстное переключение создает барьер для упрощения совместной работы и является рецептом для действий, которые можно выполнить с помощью краккс.</span><span class="sxs-lookup"><span data-stu-id="eaabf-303">This context switching creates a barrier to smooth collaboration, and is a recipe for things falling through the cracks.</span></span>

<span data-ttu-id="eaabf-304">Чтобы решить эту проблему, мы будем рады открыть шаблон приложения поиска списка.</span><span class="sxs-lookup"><span data-stu-id="eaabf-304">To help alleviate this pain, we are happy to bring to you the List Search app template.</span></span> <span data-ttu-id="eaabf-305">Миллионы пользователей используют SharePoint для управления некоторыми основными рабочими процессами в их организациях.</span><span class="sxs-lookup"><span data-stu-id="eaabf-305">Millions of users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="eaabf-306">Тем не менее, сотрудничество со списками может быть особенно утомительным.</span><span class="sxs-lookup"><span data-stu-id="eaabf-306">However, collaborating around lists can be especially tedious.</span></span> <span data-ttu-id="eaabf-307">С помощью шаблона приложения поиска списка в Microsoft Teams пользователи могут вставлять сведения из элементов списка SharePoint непосредственно в беседе чата для облегчения контекстного переключения, вызванного просто вставкой ссылки в чат.</span><span class="sxs-lookup"><span data-stu-id="eaabf-307">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="eaabf-308">Информация вставляется в виде простой для чтения карточки с автоматическим форматированием, что позволяет пользователям оставаться в беседе.</span><span class="sxs-lookup"><span data-stu-id="eaabf-308">The information is inserted as an easy-to-read auto-formatted card, helping your users stay engaged in the conversation.</span></span>

[<span data-ttu-id="eaabf-309">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-309">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Список приложений поиска](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="eaabf-311">Возвраты сотрудников</span><span class="sxs-lookup"><span data-stu-id="eaabf-311">Staff Check-ins</span></span>

<span data-ttu-id="eaabf-312">Возвраты сотрудников — это приложение на основе [Power Apps](/powerapps/powerapps-overview), которое обеспечивает возможность обмена данными между бизнес-сотрудником и персоналом для полей.</span><span class="sxs-lookup"><span data-stu-id="eaabf-312">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview)-based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="eaabf-313">Сотрудники могут легко предоставлять критические сведения о времени и обновления состояния как в запланированной, так и на нерегламентированной основе непосредственно из Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-313">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="eaabf-314">Приложение поддерживает расположение, фотографии и заметки в режиме реального времени, а также оповещения и автоматические рабочие процессы.</span><span class="sxs-lookup"><span data-stu-id="eaabf-314">The app supports real-time location, photos, and notes as well as reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="eaabf-315">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-315">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Создание представления для возврата](../assets/images/staff-check-ins-create.png)

## <a name="visitor-management-9734"></a><span data-ttu-id="eaabf-317">&#9734; управления посетителями</span><span class="sxs-lookup"><span data-stu-id="eaabf-317">Visitor Management &#9734;</span></span>

<span data-ttu-id="eaabf-318">Приложение управления посетителями позволяет организациям и сотрудникам легко и эффективно управлять процессом посетителя на сайте непосредственно из Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="eaabf-318">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="eaabf-319">Приложение позволяет сотрудникам создавать запросы посетителей, централизованно отслеживать состояние запроса с помощью панели мониторинга посетителя и получать уведомления в режиме реального времени при поступлении посетителя.</span><span class="sxs-lookup"><span data-stu-id="eaabf-319">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="eaabf-320">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-320">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

:::row:::
  :::column span="2":::
    ![Создание представления запроса](../assets/images/visitor-management-create-request.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Уведомление о получении посетителем](../assets/images/visitor-management-notify-host.png)
:::column-end:::
:::row-end:::

## <a name="workplace-awards-9734"></a><span data-ttu-id="eaabf-323">Награды для рабочего места &#9734;</span><span class="sxs-lookup"><span data-stu-id="eaabf-323">Workplace Awards &#9734;</span></span>

<span data-ttu-id="eaabf-324">Награды на рабочем месте — это шаблон приложения Teams, который предоставляет положительную платформу для поощрения распознавания и поощрение культуры повышения стоимости сотрудников на современном рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="eaabf-324">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="eaabf-325">Приложение позволяет настраивать и управлять программой поощрений сотрудников и поощрений (R&R), на которой сотрудники могут легко назначать и заявить коллег, а ваш руководитель&R может просматривать отправленные номинатионс, предоставлять награды и объявлять получателей.</span><span class="sxs-lookup"><span data-stu-id="eaabf-325">The app enables you to setup and manage an employee rewards and recognition (R&R) program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="eaabf-326">Получение на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="eaabf-326">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="eaabf-327">Карточка назначения премий для рабочего места</span><span class="sxs-lookup"><span data-stu-id="eaabf-327">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Вкладка списка "награды рабочего места"](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="eaabf-329">Есть ли идея для шаблона приложения, который вы хотели бы увидеть?</span><span class="sxs-lookup"><span data-stu-id="eaabf-329">Have an idea for an app template you'd like to see?</span></span> <span data-ttu-id="eaabf-330">Сообщите [нам о своих возможностях](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span><span class="sxs-lookup"><span data-stu-id="eaabf-330">[Please let us know](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>
