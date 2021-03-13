---
title: Приложения в собраниях Teams
author: laujan
description: обзор приложений на собраниях Teams в зависимости от роли участника и пользователя
ms.topic: overview
ms.author: lajanuar
keywords: teams apps meetings user participant role api
ms.openlocfilehash: 51fe2e0ebdaa56197bbebd1e5dbcf90698fb1f92
ms.sourcegitcommit: 23ed7edf145df10dcfba15c43978eae9e0d451a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2021
ms.locfileid: "50753555"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="03e34-104">Приложения в собраниях Teams</span><span class="sxs-lookup"><span data-stu-id="03e34-104">Apps in Teams meetings</span></span>

<span data-ttu-id="03e34-105">Собрания являются ключом к производительности в Teams.</span><span class="sxs-lookup"><span data-stu-id="03e34-105">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="03e34-106">Они позволяют совместное сотрудничество, партнерство, информированное общение и общие отзывы в инклюзивном и активном форуме.</span><span class="sxs-lookup"><span data-stu-id="03e34-106">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="03e34-107">Как разработчик вы можете создать настраиваемую [](../messaging-extensions/what-are-messaging-extensions.md) [вкладку,](../tabs/what-are-tabs.md#how-do-tabs-work) [бот](../bots/what-are-bots.md)и приложения расширения сообщений, чтобы улучшить и обогатить возможности собраний Teams.</span><span class="sxs-lookup"><span data-stu-id="03e34-107">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="03e34-108">Пользователи собраний могут получить доступ к приложениям через галерею вкладок, чтобы включить соответствующие сценарии, такие как предварительная инсценировка доски Kanban, запуск диалогов с действиями в собрании или создание опроса после собрания.</span><span class="sxs-lookup"><span data-stu-id="03e34-108">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="03e34-109">Приложение для собраний может предоставлять пользовательский интерфейс для каждого этапа жизненного цикла собрания в зависимости от состояния участника.</span><span class="sxs-lookup"><span data-stu-id="03e34-109">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="03e34-110">Приложение для собраний teams имеет три понятия:</span><span class="sxs-lookup"><span data-stu-id="03e34-110">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="03e34-111">✔ **жизненного цикла** собрания — до, во время и после срока собрания.</span><span class="sxs-lookup"><span data-stu-id="03e34-111">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="03e34-112">✔ **участника** — организатора собраний, презентовщика или участника.</span><span class="sxs-lookup"><span data-stu-id="03e34-112">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="03e34-113">✔ тип **пользователя** — пользователь-клиент, гость, федераированный или анонимный пользователь Teams.</span><span class="sxs-lookup"><span data-stu-id="03e34-113">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="03e34-114">Сценарии жизненного цикла собраний</span><span class="sxs-lookup"><span data-stu-id="03e34-114">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="03e34-115">Вкладки</span><span class="sxs-lookup"><span data-stu-id="03e34-115">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03e34-116">Как и во всех приложениях вкладок, вашему приложению необходимо следовать потоку проверки подлинности Teams [SSO](../tabs/how-to/authentication/auth-aad-sso.md) для вкладок.</span><span class="sxs-lookup"><span data-stu-id="03e34-116">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> * <span data-ttu-id="03e34-117">Мобильные клиенты поддерживают вкладки только на поверхностях предварительного собрания и после собрания.</span><span class="sxs-lookup"><span data-stu-id="03e34-117">Mobile clients support tabs only in pre-meeting and post-meeting surfaces.</span></span> <span data-ttu-id="03e34-118">В ближайшее время будут доступны такие опытом, как диалоговое окно на собрании и панель на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="03e34-118">The in-meeting experiences, such as in-meeting dialog and panel on mobile will be available soon.</span></span>
> * <span data-ttu-id="03e34-119">Приложения поддерживаются только на закрытых запланированных собраниях.</span><span class="sxs-lookup"><span data-stu-id="03e34-119">Apps are supported only in private scheduled meetings.</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="03e34-120">Предварительная встреча с приложением</span><span class="sxs-lookup"><span data-stu-id="03e34-120">Pre-meeting app experience</span></span>

<span data-ttu-id="03e34-121">**Опыт предварительного собрания:**</span><span class="sxs-lookup"><span data-stu-id="03e34-121">**Pre-meeting experience:**</span></span>

![Предсессия](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="03e34-123">**Вкладка предварительного собрания:**</span><span class="sxs-lookup"><span data-stu-id="03e34-123">**Pre-meeting tab:**</span></span>

![Представление вкладки перед собранием](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="03e34-125">✔ пользователи могут добавлять приложения на собрание через галерею вкладок двумя способами:</span><span class="sxs-lookup"><span data-stu-id="03e34-125">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="03e34-126">&emsp;&emsp;&#9679; вкладку **Details** в форме планирования Teams.</span><span class="sxs-lookup"><span data-stu-id="03e34-126">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="03e34-127">&emsp;&emsp;&#9679; на вкладке **Чат собрания** в существующем собрании.</span><span class="sxs-lookup"><span data-stu-id="03e34-127">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="03e34-128">✔ tab-приложения доступны на страницах  "Сведения о собраниях" и **"Чаты"** с помощью кнопки plus icon (➕).|</span><span class="sxs-lookup"><span data-stu-id="03e34-128">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

<span data-ttu-id="03e34-129">✔ макет tab должен быть в организованном состоянии, если имеется более десяти опросов или опросов.</span><span class="sxs-lookup"><span data-stu-id="03e34-129">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="03e34-130">Опыт приложения на собрании</span><span class="sxs-lookup"><span data-stu-id="03e34-130">In-meeting app experience</span></span>

<span data-ttu-id="03e34-131">✔ собрания будут организованы в верхней верхней панели окна чата и в качестве вкладки на собрании с помощью вкладки на собрании. Когда пользователи добавляют вкладку на собрание через галерею вкладок, приложения, которые находятся во время собраний, будут всплыть. </span><span class="sxs-lookup"><span data-stu-id="03e34-131">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="03e34-132">✔ пользователи могут добавлять приложения во время собрания.</span><span class="sxs-lookup"><span data-stu-id="03e34-132">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="03e34-133">✔ При загрузке в контексте собрания приложения смогут использовать SDK клиента Teams для доступа к И. И соответствующим образом `meetingId` отрисовки. `userMri` `frameContext`</span><span class="sxs-lookup"><span data-stu-id="03e34-133">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="03e34-134">✔ экспорта результатов опроса или опросов следует уведомить пользователей о том, что "результаты успешно загружены".</span><span class="sxs-lookup"><span data-stu-id="03e34-134">✔ Exporting a result of a survey or polls should notify the users stating, ‘results successfully downloaded’.</span></span>

<span data-ttu-id="03e34-135">✔ чтобы приложение было видно на собрании Teams в двух областях:</span><span class="sxs-lookup"><span data-stu-id="03e34-135">✔ For an app to be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="03e34-136">&emsp;&emsp;&#9679; **панели**.</span><span class="sxs-lookup"><span data-stu-id="03e34-136">&emsp;&emsp;&#9679; **Side panel**.</span></span> </br>

> [!NOTE]
> <span data-ttu-id="03e34-137">Если манифест _приложения указывает,_ что вкладка оптимизирована для боковой [панели,](create-apps-for-teams-meetings.md#during-a-meeting)то есть там она будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="03e34-137">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="03e34-138">Он также может быть частью работы с share-tray с учетом указанных рекомендаций по проектированию.</span><span class="sxs-lookup"><span data-stu-id="03e34-138">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="03e34-139">&emsp;&emsp;&#9679; диалоговое окно на **собрании.**</span><span class="sxs-lookup"><span data-stu-id="03e34-139">&emsp;&emsp;&#9679; **In-meeting dialog**.</span></span> <span data-ttu-id="03e34-140">Используйте диалоговое окно на собрании для демонстрации контента, который можно использовать для участников собрания.</span><span class="sxs-lookup"><span data-stu-id="03e34-140">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="03e34-141">*См.* [в руберсе Создание приложений для собраний команд.](create-apps-for-teams-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="03e34-141">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="03e34-142">**В ходе собрания:**</span><span class="sxs-lookup"><span data-stu-id="03e34-142">**In-meeting experience:**</span></span>

![в ходе собрания](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Представление диалоговое окно в собрании](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="03e34-145">**Диалоговое окно для действий на собрании для пользователей:**</span><span class="sxs-lookup"><span data-stu-id="03e34-145">**In-meeting actionable dialog for users:**</span></span>

![диалоговое представление](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="03e34-147">Опыт приложения после собрания</span><span class="sxs-lookup"><span data-stu-id="03e34-147">Post-meeting app experience</span></span>

<span data-ttu-id="03e34-148">**После собрания:**</span><span class="sxs-lookup"><span data-stu-id="03e34-148">**Post-meeting experience:**</span></span>

![Представление собрания после публикации](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="03e34-150">✔ сценарий приложения после собрания похож на текущий опыт после собрания с дополнительным преимуществом на наличие вкладки, которые существуют на поверхности.</span><span class="sxs-lookup"><span data-stu-id="03e34-150">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span> 

<span data-ttu-id="03e34-151">✔ пользователи могут добавлять приложения из галереи вкладок на  собрание с помощью вкладки Details в форме планирования Teams и вкладки **Чат** собраний в существующем собрании.</span><span class="sxs-lookup"><span data-stu-id="03e34-151">✔ Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="03e34-152">✔ макет tab должен быть в организованном состоянии, если имеется более десяти опросов или опросов.</span><span class="sxs-lookup"><span data-stu-id="03e34-152">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="bots"></a><span data-ttu-id="03e34-153">Боты</span><span class="sxs-lookup"><span data-stu-id="03e34-153">Bots</span></span>

<span data-ttu-id="03e34-154">Для реализации бота сначала [создайте бот,](../build-your-first-app/build-bot.md) а затем [создайте приложения для собраний Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)</span><span class="sxs-lookup"><span data-stu-id="03e34-154">For bot implementation, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="03e34-155">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="03e34-155">Messaging extensions</span></span>

<span data-ttu-id="03e34-156">Для реализации расширения обмена сообщениями сначала создайте расширение обмена [сообщениями,](../messaging-extensions/how-to/create-messaging-extension.md) а затем создайте [приложения для собраний Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)</span><span class="sxs-lookup"><span data-stu-id="03e34-156">For messaging extension implementation, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="03e34-157">Роли участников и типы пользователей в собрании</span><span class="sxs-lookup"><span data-stu-id="03e34-157">Participant roles and user types in a meeting</span></span>

![Участники собрания](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="03e34-159">Роли участников</span><span class="sxs-lookup"><span data-stu-id="03e34-159">Participant roles</span></span>

<span data-ttu-id="03e34-160">Вы можете создать приложение с помощью авторизации, определенной для участников.</span><span class="sxs-lookup"><span data-stu-id="03e34-160">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="03e34-161">Например, возможно, только организатор и/или презентер могут создать опрос на собраниях.</span><span class="sxs-lookup"><span data-stu-id="03e34-161">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="03e34-162">Хотя параметры участников по умолчанию определяются ИТ-администратором организации, организатор собрания может изменить параметры для определенного собрания.</span><span class="sxs-lookup"><span data-stu-id="03e34-162">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="03e34-163">Организаторы могут вносить эти изменения на веб-странице Параметры собрания.</span><span class="sxs-lookup"><span data-stu-id="03e34-163">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="03e34-164">**Организатор**.</span><span class="sxs-lookup"><span data-stu-id="03e34-164">**Organizer**.</span></span> <span data-ttu-id="03e34-165">Организатор назначает собрание, задает параметры собрания, назначает роли собраний и начинает собрание.</span><span class="sxs-lookup"><span data-stu-id="03e34-165">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="03e34-166">Организаторами и разрешениями участников могут быть только пользователи с учетной записью M365 (обладая лицензией Teams).</span><span class="sxs-lookup"><span data-stu-id="03e34-166">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="03e34-167">**Presenter**.</span><span class="sxs-lookup"><span data-stu-id="03e34-167">**Presenter**.</span></span> <span data-ttu-id="03e34-168">У презентаторов почти те же возможности, что и у организатора; однако, презентер не может удалить организатора из сеанса или изменить параметры собрания для сеанса.</span><span class="sxs-lookup"><span data-stu-id="03e34-168">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="03e34-169">По умолчанию участники, присоединяясь к собранию, имеют роль презента.</span><span class="sxs-lookup"><span data-stu-id="03e34-169">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="03e34-170">**Участник**.</span><span class="sxs-lookup"><span data-stu-id="03e34-170">**Attendee**.</span></span> <span data-ttu-id="03e34-171">Участник — это пользователь, которому было предложено принять участие в собрании, но которому не разрешено выступать в качестве презентера.</span><span class="sxs-lookup"><span data-stu-id="03e34-171">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="03e34-172">Участники могут взаимодействовать с другими участниками собрания, но не могут управлять любыми из параметров собрания или делиться содержимым.</span><span class="sxs-lookup"><span data-stu-id="03e34-172">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="03e34-173">_См._ [ **роли в собрании teams**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="03e34-173">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="03e34-174">Вы можете получить доступ к странице  **Параметры собрания** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="03e34-174">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="03e34-175">&#11200; в Teams перейдите к **логотипу календаря** ![ , выберите собрание, а затем ](../assets/images/apps-in-meetings/calendar-logo.png) **параметры Собрания.**</span><span class="sxs-lookup"><span data-stu-id="03e34-175">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

<span data-ttu-id="03e34-176">&#11200; в приглашении на собрание выберите **параметры Собрания.**</span><span class="sxs-lookup"><span data-stu-id="03e34-176">&#11200; In a meeting invitation, select **Meeting options**.</span></span>

<span data-ttu-id="03e34-177">&#11200; во время собрания выберите для участников **шоу** ![ значок "Показать участников" ](../assets/images/apps-in-meetings/show-participants.png) в элементе управления собрания.</span><span class="sxs-lookup"><span data-stu-id="03e34-177">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="03e34-178">Затем, над списком участников, выберите **Управление разрешениями**.</span><span class="sxs-lookup"><span data-stu-id="03e34-178">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="03e34-179">Типы пользователей.</span><span class="sxs-lookup"><span data-stu-id="03e34-179">User types</span></span>

> [!NOTE]
> <span data-ttu-id="03e34-180">Типы пользователей могут присоединяться к собраниям и предполагать одну из описанных выше ролей участников.</span><span class="sxs-lookup"><span data-stu-id="03e34-180">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="03e34-181">Тип пользователя не подвергается воздействию как часть **API getParticipantRole.**</span><span class="sxs-lookup"><span data-stu-id="03e34-181">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="03e34-182">**In-tenant**.</span><span class="sxs-lookup"><span data-stu-id="03e34-182">**In-tenant**.</span></span> <span data-ttu-id="03e34-183">Эти пользователи принадлежат к организации и имеют учетные данные в Azure Active Directory для клиента.</span><span class="sxs-lookup"><span data-stu-id="03e34-183">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="03e34-184">Как правило, это сотрудники, работающие полный рабочий день, на месте или удаленные сотрудники.</span><span class="sxs-lookup"><span data-stu-id="03e34-184">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="03e34-185">**Гость**.</span><span class="sxs-lookup"><span data-stu-id="03e34-185">**Guest**.</span></span> <span data-ttu-id="03e34-186">Гость — это участник из другой организации, которому было предложено получить доступ к Teams или другим ресурсам в клиенте организации.</span><span class="sxs-lookup"><span data-stu-id="03e34-186">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="03e34-187">Гости добавляются в Active Directory вашей организации и могут быть предоставлены практически все те же возможности Teams, что и родной член команды с полным доступом к чатам, собраниям и файлам группы.</span><span class="sxs-lookup"><span data-stu-id="03e34-187">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="03e34-188">_См._ [гостевой доступ в Microsoft Teams](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="03e34-188">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="03e34-189">**Federated/External**.</span><span class="sxs-lookup"><span data-stu-id="03e34-189">**Federated/External**.</span></span> <span data-ttu-id="03e34-190">Федераированный пользователь — это внешний пользователь Teams в другой организации, которому было предложено присоединиться к собранию.</span><span class="sxs-lookup"><span data-stu-id="03e34-190">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="03e34-191">Так как эти пользователи имеют действительные учетные данные с федерательными партнерами, они рассматриваются как проверки подлинности teams, но не имеют доступа к вашим командам или другим общим ресурсам из вашей организации.</span><span class="sxs-lookup"><span data-stu-id="03e34-191">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="03e34-192">Если вы хотите, чтобы внешние пользователи могли иметь доступ к группам и каналам, гостевой доступ может быть лучшим вариантом.</span><span class="sxs-lookup"><span data-stu-id="03e34-192">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="03e34-193">_Управление_ [внешним доступом в Microsoft Teams](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="03e34-193">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="03e34-194">**Анонимный**.</span><span class="sxs-lookup"><span data-stu-id="03e34-194">**Anonymous**.</span></span> <span data-ttu-id="03e34-195">Анонимные пользователи не имеют удостоверения Active Directory и не федератированы с клиентом.</span><span class="sxs-lookup"><span data-stu-id="03e34-195">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="03e34-196">Анонимный участник похож на внешнего пользователя, но его удостоверение не проецируемых на собрание.</span><span class="sxs-lookup"><span data-stu-id="03e34-196">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="03e34-197">Анонимные пользователи не смогут получить доступ к приложениям в окне собраний.</span><span class="sxs-lookup"><span data-stu-id="03e34-197">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03e34-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03e34-198">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="03e34-199">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="03e34-199">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="03e34-200">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="03e34-200">Build your app</span></span>](create-apps-for-teams-meetings.md)
