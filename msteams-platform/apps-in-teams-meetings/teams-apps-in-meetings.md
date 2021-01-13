---
title: Приложения в собраниях Teams
author: laujan
description: обзор приложений в собраниях Teams на основе роли участника и пользователя
ms.topic: overview
ms.author: lajanuar
keywords: API роли участника собраний в приложениях teams
ms.openlocfilehash: 217737cbbf73104d4d78cf817e6df0244229c53c
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797759"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="c6ac3-104">Приложения в собраниях Teams</span><span class="sxs-lookup"><span data-stu-id="c6ac3-104">Apps in Teams meetings</span></span>

<span data-ttu-id="c6ac3-105">Собрания являются ключевыми для повышения производительности в Teams.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-105">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="c6ac3-106">Они обеспечивают совместную работу, партнерство, информационное общение и общие отзывы на инклюзивном и активном форуме.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-106">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="c6ac3-107">Как разработчик вы можете создавать настраиваемые приложения [](../messaging-extensions/what-are-messaging-extensions.md) вкладок, [](../tabs/what-are-tabs.md#how-do-tabs-work)ботов и расширений сообщений, чтобы улучшить и улучшить возможности собраний Teams. [](../bots/what-are-bots.md)</span><span class="sxs-lookup"><span data-stu-id="c6ac3-107">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="c6ac3-108">Пользователи собраний могут получать доступ к приложениям через галерею вкладок, чтобы включить соответствующие сценарии, такие как предварительная постановка доски Канбрана, запуск диалога с действиями в собрании или создание опроса после собрания.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-108">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="c6ac3-109">Ваше приложение для собраний может предоставлять пользователю интерфейс для каждого этапа жизненного цикла собрания в зависимости от состояния участника.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-109">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="c6ac3-110">В центре возможностей приложения для собраний Teams три понятия:</span><span class="sxs-lookup"><span data-stu-id="c6ac3-110">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="c6ac3-111">✔ собрания **—** до, во время и после собрания.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-111">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="c6ac3-112">✔ **участника** — организатор собрания, участник или участник.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-112">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="c6ac3-113">✔ пользователя **—** в клиенте, гостевом, федераированном или анонимном пользователе Teams.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-113">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="c6ac3-114">Сценарии жизненного цикла собраний</span><span class="sxs-lookup"><span data-stu-id="c6ac3-114">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="c6ac3-115">Вкладки</span><span class="sxs-lookup"><span data-stu-id="c6ac3-115">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6ac3-116">Как и для всех приложений вкладок, вашему приложению необходимо следовать потоку проверки подлинности с помощью [SSO](../tabs/how-to/authentication/auth-aad-sso.md) Teams для вкладок.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-116">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> <span data-ttu-id="c6ac3-117">Мобильные клиенты поддерживают вкладки только на поверхностях до и после собрания.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-117">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="c6ac3-118">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon</span><span class="sxs-lookup"><span data-stu-id="c6ac3-118">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="c6ac3-119">Предварительная встреча в приложении</span><span class="sxs-lookup"><span data-stu-id="c6ac3-119">Pre-meeting app experience</span></span>

<span data-ttu-id="c6ac3-120">**Предварительные собрания:**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-120">**Pre-meeting experience:**</span></span>

![предварительная встреча](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="c6ac3-122">**Вкладка "До собрания":**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-122">**Pre-meeting tab:**</span></span>

![Представление вкладки перед собранием](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="c6ac3-124">✔ пользователи с разрешениями могут добавлять приложения на собрание через галерею вкладок двумя способами:</span><span class="sxs-lookup"><span data-stu-id="c6ac3-124">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="c6ac3-125">&emsp;&emsp;&#9679; на **вкладке "Сведения"** формы планирования Teams.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-125">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="c6ac3-126">&emsp;&emsp;&#9679; на вкладке **"Чат** собрания" в существующем собрании.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-126">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="c6ac3-127">✔ tab доступны на страницах сведений  о  собраниях и чатах с помощью кнопки "плюс" (➕).|</span><span class="sxs-lookup"><span data-stu-id="c6ac3-127">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

<span data-ttu-id="c6ac3-128">✔ табули должны быть в уорганизованном состоянии при более чем десяти опросах или опросах.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-128">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="c6ac3-129">Приложение для собраний</span><span class="sxs-lookup"><span data-stu-id="c6ac3-129">In-meeting app experience</span></span>

<span data-ttu-id="c6ac3-130">✔ собрания будут работать в верхней верхней панели окна чата и в качестве вкладки "Собрание" на вкладке "Собрание". Когда пользователи добавляют вкладку на собрание через галерею вкладок, будут доступны приложения, которые находятся во время собраний. </span><span class="sxs-lookup"><span data-stu-id="c6ac3-130">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="c6ac3-131">✔ пользователи с разрешениями могут добавлять приложения во время собрания.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-131">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="c6ac3-132">✔ При загрузке в контексте собрания приложения смогут использовать клиентский SDK Teams для доступа к , и для правильной отрисовки `meetingId` `userMri` `frameContext` работы.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-132">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="c6ac3-133">✔ экспорт результатов опроса или опросов должен уведомить пользователей о том, что результаты успешно загружены.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-133">✔ Exporting a result of a survey or polls should notify the users stating, ‘results successfully downloaded’.</span></span>

<span data-ttu-id="c6ac3-134">✔ Чтобы приложение было видно на собрании Teams в двух областях:</span><span class="sxs-lookup"><span data-stu-id="c6ac3-134">✔ For an app to be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="c6ac3-135">&emsp;&emsp;&#9679; **боковой панели.**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-135">&emsp;&emsp;&#9679; **Side panel**.</span></span> </br>

> [!NOTE]
> <span data-ttu-id="c6ac3-136">Если манифест _вашего приложения_ указывает, что вкладка оптимизирована для боковой [панели,](create-apps-for-teams-meetings.md#during-a-meeting)в которой она будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-136">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="c6ac3-137">Она также может быть частью работы с совместной работы с учетом указанных рекомендаций по проектированию.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-137">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="c6ac3-138">&emsp;&emsp;&#9679; **собрания.**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-138">&emsp;&emsp;&#9679; **In-meeting dialog**.</span></span> <span data-ttu-id="c6ac3-139">Используйте диалоговое окно собрания для демонстрации действия содержимого для участников собрания.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-139">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="c6ac3-140">*См.* ["Создание приложений для собраний Teams".](create-apps-for-teams-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="c6ac3-140">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="c6ac3-141">**В собрании:**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-141">**In-meeting experience:**</span></span>

![в собрании](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Представление в диалоговом оке "Собрание"](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="c6ac3-144">**Диалоговое окно с действиями при собрании для пользователей:**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-144">**In-meeting actionable dialog for users:**</span></span>

![диалоговое окно](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="c6ac3-146">Приложение после собрания</span><span class="sxs-lookup"><span data-stu-id="c6ac3-146">Post-meeting app experience</span></span>

<span data-ttu-id="c6ac3-147">**После собрания:**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-147">**Post-meeting experience:**</span></span>

![представление после собрания](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="c6ac3-149">✔ сценарий приложения после собрания схож с текущим опытом после собрания с дополнительным преимуществом на наличие вкладок, существующих на поверхности.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-149">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span> 

<span data-ttu-id="c6ac3-150">✔ пользователи с разрешениями могут добавлять приложения из коллекции  вкладок на собрание с помощью вкладки "Сведения" формы планирования Teams и вкладки **"Чат"** в существующем собрании.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-150">✔ Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="c6ac3-151">✔ табули должны быть в уорганизованном состоянии при более чем десяти опросах или опросах.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-151">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="bots"></a><span data-ttu-id="c6ac3-152">Боты</span><span class="sxs-lookup"><span data-stu-id="c6ac3-152">Bots</span></span>

<span data-ttu-id="c6ac3-153">Для реализации ботов см. документацию по [собраниям Teams с нашими ботами.](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings)</span><span class="sxs-lookup"><span data-stu-id="c6ac3-153">For bot implementation, please see our [Bots in Teams meetings](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) documentation.</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="c6ac3-154">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="c6ac3-154">Messaging Extensions</span></span>

<span data-ttu-id="c6ac3-155">О реализации расширения обмена сообщениями см. в документации по собраниям [Teams.](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings)</span><span class="sxs-lookup"><span data-stu-id="c6ac3-155">For messaging extension implementation, please see our [Messaging extensions in Teams meetings](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) documentation.</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="c6ac3-156">Роли участников и типы пользователей в собрании</span><span class="sxs-lookup"><span data-stu-id="c6ac3-156">Participant roles and user types in a meeting</span></span>

![Участники собрания](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="c6ac3-158">Роли участников</span><span class="sxs-lookup"><span data-stu-id="c6ac3-158">Participant roles</span></span>

<span data-ttu-id="c6ac3-159">Вы можете разработать приложение с авторизацией, относяцией к конкретному участнику.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-159">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="c6ac3-160">Например, опрос на собраниях может создавать только организатор и/или presenter.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-160">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="c6ac3-161">Хотя параметры участников по умолчанию определяются ИТ-администратором организации, организатору собрания может потребоваться изменить параметры конкретного собрания.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-161">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="c6ac3-162">Организаторы могут внести эти изменения на веб-странице параметров собрания.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-162">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="c6ac3-163">**Организатор .**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-163">**Organizer**.</span></span> <span data-ttu-id="c6ac3-164">Организатор создает расписание собрания, задает параметры собрания, назначает роли собраний и начинает собрание.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-164">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="c6ac3-165">Организаторами и разрешениями участников могут быть только пользователи с учетной записью M365 (обладая лицензией Teams).</span><span class="sxs-lookup"><span data-stu-id="c6ac3-165">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="c6ac3-166">**Presenter**.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-166">**Presenter**.</span></span> <span data-ttu-id="c6ac3-167">У presenters практически такие же возможности, как у организатора; тем не менее, он не может удалить организатора из сеанса или изменить параметры собрания для сеанса.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-167">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="c6ac3-168">По умолчанию участники, присоединяясь к собранию, имеют роль участника.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-168">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="c6ac3-169">**Участник**.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-169">**Attendee**.</span></span> <span data-ttu-id="c6ac3-170">Участник — это пользователь, приглашенный на собрание, но не уполномоченный выступать в качестве участника.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-170">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="c6ac3-171">Участники могут взаимодействовать с другими участниками собрания, но не могут управлять любыми из параметров собрания или делиться содержимым.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-171">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="c6ac3-172">_См._ [ **роли в собрании Teams**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="c6ac3-172">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="c6ac3-173">Доступ к странице  **параметров собрания** можно получить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c6ac3-173">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="c6ac3-174">&#11200; в Teams перейдите  к логотипу календаря, выберите собрание, а затем ![ выберите ](../assets/images/apps-in-meetings/calendar-logo.png) **параметры собрания.**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-174">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

<span data-ttu-id="c6ac3-175">&#11200; в приглашении на собрание выберите **параметры собрания.**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-175">&#11200; In a meeting invitation, select **Meeting options**.</span></span>

<span data-ttu-id="c6ac3-176">&#11200; во время собрания выберите **"Показать** участников" и "Показать ![ участников" в ](../assets/images/apps-in-meetings/show-participants.png) элементе управления собрания.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-176">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="c6ac3-177">Затем над списком участников выберите **"Управление разрешениями".**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-177">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="c6ac3-178">Типы пользователей.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-178">User types</span></span>

> [!NOTE]
> <span data-ttu-id="c6ac3-179">Типы пользователей могут присоединяться к собраниям и принимать на себя одну из ролей участников, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-179">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="c6ac3-180">Тип пользователя не является частью API **getParticipantRole.**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-180">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="c6ac3-181">**В клиенте**.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-181">**In-tenant**.</span></span> <span data-ttu-id="c6ac3-182">Эти пользователи принадлежат к организации и имеют учетные данные в Azure Active Directory для клиента.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-182">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="c6ac3-183">Обычно это сотрудники, работающие на месте или удаленные сотрудники.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-183">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="c6ac3-184">**Гость.**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-184">**Guest**.</span></span> <span data-ttu-id="c6ac3-185">Гость — это участник из другой организации, приглашенный на доступ к Teams или другим ресурсам в клиенте вашей организации.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-185">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="c6ac3-186">Гости добавляются в Active Directory вашей организации и могут получить практически все возможности Teams, что и участник команды с полным доступом к чатам, собраниям и файлам команды.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-186">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="c6ac3-187">_См._ [гостевой доступ в Microsoft Teams](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="c6ac3-187">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="c6ac3-188">**Federated/External**.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-188">**Federated/External**.</span></span> <span data-ttu-id="c6ac3-189">Федераированный пользователь — это внешний пользователь Teams в другой организации, приглашенный к собранию.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-189">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="c6ac3-190">Так как эти пользователи имеют действительные учетные данные с федерательными партнерами, они рассматриваются как авторизации в Teams, но не имеют доступа к вашим командам или другим общим ресурсам из вашей организации.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-190">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="c6ac3-191">Если вы хотите, чтобы внешние пользователи могли получать доступ к командам и каналам, лучше использовать гостевой доступ.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-191">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="c6ac3-192">_См._ ["Управление внешним доступом в Microsoft Teams"](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="c6ac3-192">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="c6ac3-193">**Анонимный .**</span><span class="sxs-lookup"><span data-stu-id="c6ac3-193">**Anonymous**.</span></span> <span data-ttu-id="c6ac3-194">Анонимные пользователи не имеют удостоверения Active Directory и не являются федератными с клиентом.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-194">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="c6ac3-195">Анонимный участник похож на внешнего пользователя, но его удостоверение не проецируемых в собрание.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-195">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="c6ac3-196">Анонимные пользователи не смогут получить доступ к приложениям в окне собрания.</span><span class="sxs-lookup"><span data-stu-id="c6ac3-196">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6ac3-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6ac3-197">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c6ac3-198">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="c6ac3-198">Design your app</span></span>](create-apps-for-teams-meetings.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="c6ac3-199">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="c6ac3-199">Build your app</span></span>](create-apps-for-teams-meetings.md)
