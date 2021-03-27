---
title: Приложения в собраниях Teams
author: laujan
description: обзор приложений на собраниях Teams в зависимости от роли участника и пользователя
ms.topic: overview
ms.author: lajanuar
keywords: teams apps meetings user participant role api
ms.openlocfilehash: ac4e270090dd89d370d37de88b8cba552b77a5cb
ms.sourcegitcommit: 3727fc58e84b6f1752612884c2e0b25e207fb56e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2021
ms.locfileid: "51382340"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="29c09-104">Приложения в собраниях Teams</span><span class="sxs-lookup"><span data-stu-id="29c09-104">Apps in Teams meetings</span></span>

<span data-ttu-id="29c09-105">Собрания позволяют совместное сотрудничество, партнерство, информированное общение и общие отзывы на инклюзивном и активном форуме.</span><span class="sxs-lookup"><span data-stu-id="29c09-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="29c09-106">Приложение для собраний может предоставлять пользовательский интерфейс для каждого этапа жизненного цикла собрания, включая опыт предварительного собрания, в собрании и после собрания в зависимости от состояния участника.</span><span class="sxs-lookup"><span data-stu-id="29c09-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="29c09-107">Конечные пользователи teams могут получать доступ к приложениям во время собраний с помощью галереи вкладок, например:</span><span class="sxs-lookup"><span data-stu-id="29c09-107">Teams end-users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="29c09-108">Предварительная стадия доски Kanban</span><span class="sxs-lookup"><span data-stu-id="29c09-108">Pre-stage a Kanban board</span></span>
* <span data-ttu-id="29c09-109">Запуск диалогового номера с действиями на собрании</span><span class="sxs-lookup"><span data-stu-id="29c09-109">Launch an in-meeting actionable dialog</span></span>
* <span data-ttu-id="29c09-110">Создание опроса после собрания</span><span class="sxs-lookup"><span data-stu-id="29c09-110">Create a post-meeting poll</span></span>

<span data-ttu-id="29c09-111">Размязаемость приложения собраний команд основана на следующих понятиях:</span><span class="sxs-lookup"><span data-stu-id="29c09-111">Teams’ meeting app extensibility is based on the following concepts:</span></span>

<span data-ttu-id="29c09-112">✔ жизненного цикла собрания имеет такие этапы, как до, во время и после окончания собрания.</span><span class="sxs-lookup"><span data-stu-id="29c09-112">✔ Meeting lifecycle has stages such as before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="29c09-113">✔ роли участника в собрании, например организатор собрания, презент или участник.</span><span class="sxs-lookup"><span data-stu-id="29c09-113">✔ Participant roles in a meeting such as meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="29c09-114">✔ типах пользователей на собрании, таких как пользователь in-tenant, guest, federated или anonymous Teams.</span><span class="sxs-lookup"><span data-stu-id="29c09-114">✔ User types in a meeting such as in-tenant, guest, federated, or anonymous Teams user.</span></span>

<span data-ttu-id="29c09-115">В этой статье освещаются сведения о жизненном цикле собраний и об интеграции вкладок, ботов и расширений обмена сообщениями в собрании.</span><span class="sxs-lookup"><span data-stu-id="29c09-115">This article covers information about the meeting lifecycle and how to integrate tabs, bots, and messaging extensions in your meeting.</span></span> <span data-ttu-id="29c09-116">Это также позволяет определить роли участников, а также использовать различные типы пользователей для выполнения задач.</span><span class="sxs-lookup"><span data-stu-id="29c09-116">It also enables you to identify participant roles and also use different user types to perform tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="29c09-117">Чтобы работать с функциями extensibility приложения для собраний, необходимо иметь соответствующие разрешения.</span><span class="sxs-lookup"><span data-stu-id="29c09-117">To work with the meeting app extensibility features, you must have the appropriate permissions.</span></span>

### <a name="meeting-lifecycle"></a><span data-ttu-id="29c09-118">Жизненный цикл встречи</span><span class="sxs-lookup"><span data-stu-id="29c09-118">Meeting lifecycle</span></span>

<span data-ttu-id="29c09-119">Жизненный цикл собрания состоит из предварительного собрания, в собрании и после собрания.</span><span class="sxs-lookup"><span data-stu-id="29c09-119">Meeting lifecycle consists of pre-meeting, in-meeting, and post-meeting app experience.</span></span> <span data-ttu-id="29c09-120">На каждом этапе жизненного цикла собрания можно интегрировать вкладки, боты и расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="29c09-120">You can integrate tabs, bots, and messaging extensions in each stage of the meeting lifecycle.</span></span>

## <a name="integrate-tabs-into-the-meeting-lifecycle"></a><span data-ttu-id="29c09-121">Интеграция вкладок в жизненный цикл собрания</span><span class="sxs-lookup"><span data-stu-id="29c09-121">Integrate tabs into the meeting lifecycle</span></span>

<span data-ttu-id="29c09-122">Вкладки позволяют членам группы получать доступ к службам и контенту в определенном пространстве в канале или чате.</span><span class="sxs-lookup"><span data-stu-id="29c09-122">Tabs allow team members to access services and content in a specific space within a channel or chat.</span></span> <span data-ttu-id="29c09-123">Это позволяет группе работать непосредственно со вкладками и беседами о средствах и данных, доступных в вкладке.</span><span class="sxs-lookup"><span data-stu-id="29c09-123">This lets the team work directly with tabs and have conversations about the tools and data available within tabs.</span></span> <span data-ttu-id="29c09-124">На собрании Teams пользователи могут добавить вкладку, выбрав плюс</span><span class="sxs-lookup"><span data-stu-id="29c09-124">In Teams meeting, users can add a tab by selecting plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="29c09-125">и выбор приложения, которое они хотят установить в качестве вкладки.</span><span class="sxs-lookup"><span data-stu-id="29c09-125">, and choosing the app that they want to install as a tab.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29c09-126">Если вы интегрировали вкладку со своей встречей, ваше приложение должно следовать потоку проверки подлинности для вкладки teams single [sign-on (SSO).](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="29c09-126">If you have integrated a tab with your meeting, then your app must follow the Teams [single sign-on (SSO) authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> * <span data-ttu-id="29c09-127">Мобильные клиенты поддерживают вкладки только на этапах предварительного и после собраний.</span><span class="sxs-lookup"><span data-stu-id="29c09-127">Mobile clients support tabs only in pre and post meeting stages.</span></span> <span data-ttu-id="29c09-128">В настоящее время на мобильных устройствах недоступны диалоговое окно и панель для собраний.</span><span class="sxs-lookup"><span data-stu-id="29c09-128">The in-meeting experiences that is in-meeting dialog and panel are currently not available on mobile.</span></span>
> * <span data-ttu-id="29c09-129">Приложения поддерживаются только на закрытых запланированных собраниях.</span><span class="sxs-lookup"><span data-stu-id="29c09-129">Apps are supported only in private scheduled meetings.</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="29c09-130">Предварительная встреча с приложением</span><span class="sxs-lookup"><span data-stu-id="29c09-130">Pre-meeting app experience</span></span>

<span data-ttu-id="29c09-131">**Опыт предварительного собрания:**</span><span class="sxs-lookup"><span data-stu-id="29c09-131">**Pre-meeting experience:**</span></span>

![Предсессия](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="29c09-133">**Вкладка предварительного собрания:**</span><span class="sxs-lookup"><span data-stu-id="29c09-133">**Pre-meeting tab:**</span></span>

![Представление вкладки перед собранием](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="29c09-135">✔ пользователи — это пользователи, которые могут добавлять приложения на собрание на различных этапах жизненного цикла собрания.</span><span class="sxs-lookup"><span data-stu-id="29c09-135">✔ Permissioned users are users who can add apps to a meeting during different stages of the meeting lifecycle.</span></span> <span data-ttu-id="29c09-136">Эти пользователи могут добавлять приложения на собрание через галерею вкладок двумя способами:</span><span class="sxs-lookup"><span data-stu-id="29c09-136">These users can add apps to a meeting through the tab gallery in two ways:</span></span>

   * <span data-ttu-id="29c09-137">Использование **вкладки Details** в форме планирования Teams.</span><span class="sxs-lookup"><span data-stu-id="29c09-137">Using the **Details** tab on the Teams scheduling form.</span></span>

   * <span data-ttu-id="29c09-138">Использование вкладки **Чат собрания** в существующем собрании.</span><span class="sxs-lookup"><span data-stu-id="29c09-138">Using the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="29c09-139">✔ tab-приложения доступны на страницах  "Сведения о собраниях" и **"Чаты"** с помощью кнопки плюс ➕.</span><span class="sxs-lookup"><span data-stu-id="29c09-139">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus ➕ button.</span></span>

<span data-ttu-id="29c09-140">✔ макет tab должен быть в организованном состоянии, если имеется более десяти опросов или опросов.</span><span class="sxs-lookup"><span data-stu-id="29c09-140">✔ Tab layout must be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="29c09-141">Опыт приложения на собрании</span><span class="sxs-lookup"><span data-stu-id="29c09-141">In-meeting app experience</span></span>

<span data-ttu-id="29c09-142">✔ собрания находятся в верхней верхней панели окна чата и в качестве вкладки на собрании с помощью вкладки на собрании. Когда пользователи добавляют вкладку на собрание через галерею вкладок, показано приложение, которое находится **во** время собраний.</span><span class="sxs-lookup"><span data-stu-id="29c09-142">✔ Meeting apps are hosted in the top upper bar of the chat window and as in-meeting tab experience using the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences are shown.</span></span>

<span data-ttu-id="29c09-143">✔ пользователи могут добавлять приложения во время собрания.</span><span class="sxs-lookup"><span data-stu-id="29c09-143">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="29c09-144">✔ При загрузке в контексте собрания приложения могут использовать SDK клиента Teams для доступа к И. И соответствующим образом `meetingId` `userMri` отрисовки. `frameContext`</span><span class="sxs-lookup"><span data-stu-id="29c09-144">✔ When loaded in the context of a meeting, apps can leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="29c09-145">✔ экспорт результатов опроса или опроса, оповетив пользователей об успешной загрузке результатов.</span><span class="sxs-lookup"><span data-stu-id="29c09-145">✔ Exporting a result of a survey or poll notifies the users that the results successfully downloaded.</span></span>

<span data-ttu-id="29c09-146">✔ приложение отображается на собрании Teams в боковой панели или диалоговом окне на собрании.</span><span class="sxs-lookup"><span data-stu-id="29c09-146">✔ An app is visible in a Teams meeting in the side panel or the in-meeting dialog box.</span></span> <span data-ttu-id="29c09-147">Используйте диалоговое окно на собрании для демонстрации контента, который можно использовать для участников собрания.</span><span class="sxs-lookup"><span data-stu-id="29c09-147">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="29c09-148">*См.* [в руберсе Создание приложений для собраний команд.](create-apps-for-teams-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="29c09-148">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="29c09-149">Манифест приложения указывает, что вкладка [оптимизирована для](create-apps-for-teams-meetings.md#during-a-meeting)боковой панели, то есть там, где она отображается.</span><span class="sxs-lookup"><span data-stu-id="29c09-149">Your app manifest specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it is displayed.</span></span> <span data-ttu-id="29c09-150">Он также может быть частью работы с share-tray с учетом указанных рекомендаций по проектированию.</span><span class="sxs-lookup"><span data-stu-id="29c09-150">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="29c09-151">На следующих изображениях приложение отображается в диалоговом окне на собрании и в качестве отдельной боковой панели:</span><span class="sxs-lookup"><span data-stu-id="29c09-151">The following images display the app as an in-meeting dialog box and as a separate side panel:</span></span>

![Опыт в собрании](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Представление диалоговое окно в собрании](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="in-meeting-actionable-dialog-for-users"></a><span data-ttu-id="29c09-154">Диалоговое окно для действий в собрании для пользователей</span><span class="sxs-lookup"><span data-stu-id="29c09-154">In-meeting actionable dialog for users</span></span>

![Диалоговое представление](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="29c09-156">Опыт приложения после собрания</span><span class="sxs-lookup"><span data-stu-id="29c09-156">Post-meeting app experience</span></span>

![Представление собрания после публикации](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="29c09-158">✔ сценарий приложения после собрания похож на текущий опыт после собрания с дополнительным преимуществом на наличие вкладки, которые существуют на поверхности.</span><span class="sxs-lookup"><span data-stu-id="29c09-158">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span>

<span data-ttu-id="29c09-159">✔ пользователи могут добавлять приложения из галереи вкладок на  собрание с помощью вкладки Details в форме планирования teams и вкладки **Чат** собраний в существующем собрании.</span><span class="sxs-lookup"><span data-stu-id="29c09-159">✔ Permissioned users can add apps from the tab gallery to a meeting using the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="29c09-160">✔ макет tab должен быть организован при более чем десяти опросах или опросах.</span><span class="sxs-lookup"><span data-stu-id="29c09-160">✔  Tab layout must be organized when there are more than ten polls or surveys.</span></span>

### <a name="integrate-bots-into-the-meeting-lifecycle"></a><span data-ttu-id="29c09-161">Интеграция ботов в жизненный цикл собрания</span><span class="sxs-lookup"><span data-stu-id="29c09-161">Integrate bots into the meeting lifecycle</span></span>

<span data-ttu-id="29c09-162">Для реализации бота сначала [создайте бот,](../build-your-first-app/build-bot.md) а затем [создайте приложения для собраний Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)</span><span class="sxs-lookup"><span data-stu-id="29c09-162">For bot implementation, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a><span data-ttu-id="29c09-163">Интеграция расширений обмена сообщениями в жизненный цикл собрания</span><span class="sxs-lookup"><span data-stu-id="29c09-163">Integrate messaging extensions into the meeting lifecycle</span></span>

<span data-ttu-id="29c09-164">Для реализации расширения обмена сообщениями сначала создайте расширение обмена [сообщениями,](../messaging-extensions/how-to/create-messaging-extension.md) а затем создайте [приложения для собраний Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)</span><span class="sxs-lookup"><span data-stu-id="29c09-164">For messaging extension implementation, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="29c09-165">Роли участников и типы пользователей в собрании</span><span class="sxs-lookup"><span data-stu-id="29c09-165">Participant roles and user types in a meeting</span></span>

![Участники собрания](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="29c09-167">Роли участников</span><span class="sxs-lookup"><span data-stu-id="29c09-167">Participant roles</span></span>

<span data-ttu-id="29c09-168">Параметры участников по умолчанию определяются ИТ-администратором организации.</span><span class="sxs-lookup"><span data-stu-id="29c09-168">Default participant settings are determined by an organization's IT administrator.</span></span> <span data-ttu-id="29c09-169">Ниже следующую роль участника собрания:</span><span class="sxs-lookup"><span data-stu-id="29c09-169">The following are the participant roles in a meeting:</span></span>

* <span data-ttu-id="29c09-170">**Организатор.** Организатор назначает собрание, задает параметры собрания, назначает роли собраний и начинает собрание.</span><span class="sxs-lookup"><span data-stu-id="29c09-170">**Organizer**: The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="29c09-171">Организаторами и разрешениями участников могут быть только пользователи с учетной записью M365 с лицензией Teams.</span><span class="sxs-lookup"><span data-stu-id="29c09-171">Only users with a M365 account with a Teams license can be organizers and control attendee permissions.</span></span> <span data-ttu-id="29c09-172">Организатор собрания может изменить параметры для определенного собрания.</span><span class="sxs-lookup"><span data-stu-id="29c09-172">A meeting organizer can change the settings for a specific meeting.</span></span> <span data-ttu-id="29c09-173">Организаторы могут вносить эти изменения на веб-странице **Параметры** собрания.</span><span class="sxs-lookup"><span data-stu-id="29c09-173">Organizers can make these changes on the **Meeting options** web page.</span></span>
* <span data-ttu-id="29c09-174">**Presenter**: Presenters have the same capabilities as organiser.</span><span class="sxs-lookup"><span data-stu-id="29c09-174">**Presenter**: Presenters have the same capabilities as organizer.</span></span> <span data-ttu-id="29c09-175">Однако, презентовщик не может удалить организатора из сеанса или изменить параметры собрания для сеанса.</span><span class="sxs-lookup"><span data-stu-id="29c09-175">However, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="29c09-176">По умолчанию участники, присоединяясь к собранию, имеют роль презента.</span><span class="sxs-lookup"><span data-stu-id="29c09-176">By default, participants joining a meeting have the presenter role.</span></span>
* <span data-ttu-id="29c09-177">**Участник.** Участник — это пользователь, которому было предложено присутствовать на собрании, но которому не разрешено выступать в качестве презентовщика.</span><span class="sxs-lookup"><span data-stu-id="29c09-177">**Attendee**: An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="29c09-178">Участники могут взаимодействовать с другими участниками собрания, но не могут управлять любыми из параметров собрания или делиться содержимым.</span><span class="sxs-lookup"><span data-stu-id="29c09-178">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="29c09-179">Только организатор или презент может добавлять, удалять или удалять приложения.</span><span class="sxs-lookup"><span data-stu-id="29c09-179">Only an organizer or presenter can add, remove, or uninstall apps.</span></span> <span data-ttu-id="29c09-180">Только организатор или презент может создавать опросы на собрании.</span><span class="sxs-lookup"><span data-stu-id="29c09-180">Only organizer or presenter can create polls in a meeting.</span></span>

<span data-ttu-id="29c09-181">Дополнительные сведения см. [в сведениях о ролях в собрании Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="29c09-181">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

<span data-ttu-id="29c09-182">Вы можете получить доступ к странице  **Параметры собрания** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="29c09-182">You can access the  **Meeting options** page as follows:</span></span>

* <span data-ttu-id="29c09-183">В Teams перейдите к **логотипу календаря** ![ ](../assets/images/apps-in-meetings/calendar-logo.png) календаря, выберите собрание, а затем **параметры Собрания.**</span><span class="sxs-lookup"><span data-stu-id="29c09-183">In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

* <span data-ttu-id="29c09-184">В приглашении на собрание выберите **параметры Собрания.**</span><span class="sxs-lookup"><span data-stu-id="29c09-184">In a meeting invitation, select **Meeting options**.</span></span>

* <span data-ttu-id="29c09-185">Во время собрания выберите, **чтобы** участники Шоу ![ показали значок участников в ](../assets/images/apps-in-meetings/show-participants.png) элементе управления собрания.</span><span class="sxs-lookup"><span data-stu-id="29c09-185">During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="29c09-186">Затем, над списком участников, выберите **Управление разрешениями**.</span><span class="sxs-lookup"><span data-stu-id="29c09-186">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="29c09-187">Типы пользователей.</span><span class="sxs-lookup"><span data-stu-id="29c09-187">User types</span></span>

> [!NOTE]
> <span data-ttu-id="29c09-188">Пользователи с определенными типами пользователей, которые им назначены, могут присоединяться к собраниям и принимать на себя одну из ролей участников, описанных в [ролях участников.](#participant-roles)</span><span class="sxs-lookup"><span data-stu-id="29c09-188">Users with specific user types assigned to them can join meetings and assume one of the participant roles described in [participant roles](#participant-roles).</span></span> <span data-ttu-id="29c09-189">Тип пользователя не входит в **API getParticipantRole.**</span><span class="sxs-lookup"><span data-stu-id="29c09-189">The user type is not included in the **getParticipantRole** API.</span></span>

<span data-ttu-id="29c09-190">Следующие типы пользователей определяют, что может сделать каждый пользователь и к чему он может получить доступ:</span><span class="sxs-lookup"><span data-stu-id="29c09-190">The following user types identify what each user can do and what they can access:</span></span>

* <span data-ttu-id="29c09-191">**In-tenant.** Пользователи-клиенты принадлежат к организации и имеют учетные данные в Azure Active Directory (AAD) для клиента.</span><span class="sxs-lookup"><span data-stu-id="29c09-191">**In-tenant**: In-tenant users belong to the organization and have credentials in Azure Active Directory (AAD) for the tenant.</span></span> <span data-ttu-id="29c09-192">Обычно это сотрудники, работающие полный рабочий день, на месте или удаленные сотрудники.</span><span class="sxs-lookup"><span data-stu-id="29c09-192">They are usually full-time, onsite, or remote employees.</span></span> <span data-ttu-id="29c09-193">Пользователь, наемный клиент, может быть организатором, презентером или посетителем.</span><span class="sxs-lookup"><span data-stu-id="29c09-193">An in-tenant user can be an organizer, presenter, or attendee.</span></span>
* <span data-ttu-id="29c09-194">**Гость.** Гость — это участник из другой организации, приглашенный для доступа к Teams или другим ресурсам в клиенте организации.</span><span class="sxs-lookup"><span data-stu-id="29c09-194">**Guest**: A guest is a participant from another organization invited to access Teams or other resources in the organization's tenant.</span></span> <span data-ttu-id="29c09-195">Гости добавляются в AAD организации и имеют те же возможности Teams, что и родной член команды, с доступом к чатым, собраниям и файлам группы.</span><span class="sxs-lookup"><span data-stu-id="29c09-195">Guests are added to your organization’s AAD and have the same Teams capabilities as a native team member with access to team chats, meetings, and files.</span></span> <span data-ttu-id="29c09-196">Гостевой пользователь может быть организатором, презентером или посетителем.</span><span class="sxs-lookup"><span data-stu-id="29c09-196">A guest user can be an organizer, presenter, or attendee.</span></span> <span data-ttu-id="29c09-197">Дополнительные сведения см. в [гостевом доступе в Teams.](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="29c09-197">For more information, see [guest access in Teams](/microsoftteams/guest-access).</span></span>
* <span data-ttu-id="29c09-198">**Федераированный или** внешний. Федераированный пользователь является внешним пользователем Teams в другой организации, которому было предложено присоединиться к собранию.</span><span class="sxs-lookup"><span data-stu-id="29c09-198">**Federated or external**: A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="29c09-199">Эти пользователи имеют действительные учетные данные с федерательными партнерами и уполномочены Teams.</span><span class="sxs-lookup"><span data-stu-id="29c09-199">These users have valid credentials with federated partners and are authorized by Teams.</span></span> <span data-ttu-id="29c09-200">Они не имеют доступа к вашим командам или другим общим ресурсам из вашей организации.</span><span class="sxs-lookup"><span data-stu-id="29c09-200">They do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="29c09-201">Гостевой доступ является лучшим вариантом для внешних пользователей, чтобы иметь доступ к группам и каналам.</span><span class="sxs-lookup"><span data-stu-id="29c09-201">Guest access is a better option for external users to have access to teams and channels.</span></span> <span data-ttu-id="29c09-202">Дополнительные сведения см. в [сведениях об управлении внешним доступом в Teams.](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="29c09-202">For more information, see [manage external access in Teams](/microsoftteams/manage-external-access).</span></span>
* <span data-ttu-id="29c09-203">**Анонимные.** Анонимные пользователи не имеют удостоверения AAD и не федератированы с клиентом.</span><span class="sxs-lookup"><span data-stu-id="29c09-203">**Anonymous**: Anonymous users do not have an AAD identity and are not federated with a tenant.</span></span> <span data-ttu-id="29c09-204">Анонимный участник похож на внешнего пользователя, но его удостоверение не проецируемы на собрании.</span><span class="sxs-lookup"><span data-stu-id="29c09-204">The anonymous participant is like an external user, but their identity is not projected in the meeting.</span></span> <span data-ttu-id="29c09-205">Анонимные пользователи не могут получить доступ к приложениям в окне собраний.</span><span class="sxs-lookup"><span data-stu-id="29c09-205">Anonymous users are not able to access apps in a meeting window.</span></span> <span data-ttu-id="29c09-206">Анонимный пользователь не может быть организатором, но может быть презентером или посетителем.</span><span class="sxs-lookup"><span data-stu-id="29c09-206">An anonymous user cannot be an organizer but can be a presenter or attendee.</span></span>

## <a name="see-also"></a><span data-ttu-id="29c09-207">См. также</span><span class="sxs-lookup"><span data-stu-id="29c09-207">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="29c09-208">Tab</span><span class="sxs-lookup"><span data-stu-id="29c09-208">Tab</span></span>](../tabs/what-are-tabs.md#how-do-tabs-work)

> [!div class="nextstepaction"]
> [<span data-ttu-id="29c09-209">Bot</span><span class="sxs-lookup"><span data-stu-id="29c09-209">Bot</span></span>](../bots/what-are-bots.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="29c09-210">Расширение для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="29c09-210">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="29c09-211">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="29c09-211">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-steps"></a><span data-ttu-id="29c09-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="29c09-212">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="29c09-213">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="29c09-213">Build your app</span></span>](create-apps-for-teams-meetings.md)
