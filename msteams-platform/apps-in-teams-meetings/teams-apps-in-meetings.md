---
title: Приложения в собраниях Teams
author: laujan
description: Обзор приложений в собраниях Teams на основе роли участника и пользователя
ms.topic: overview
ms.author: lajanuar
keywords: API роли участника для собраний приложений Teams
ms.openlocfilehash: dbf12523d609d47193fb3c07bde2acd184292f64
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452640"
---
# <a name="apps-in-teams-meetings-developer-preview"></a><span data-ttu-id="aaad6-104">Приложения в собраниях Teams (разработчик предварительной версии)</span><span class="sxs-lookup"><span data-stu-id="aaad6-104">Apps in Teams meetings (Developer Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="aaad6-105">Функции, включенные в Microsoft Teams Preview, предоставляются только для раннего доступа, тестирования и создания отзывов.</span><span class="sxs-lookup"><span data-stu-id="aaad6-105">Features included in Microsoft Teams Developer Preview are provided for early-access, testing, and feedback purposes only.</span></span> <span data-ttu-id="aaad6-106">Они могут быть подвергнуты изменениям, прежде чем стать доступными в общедоступном выпуске и не должны использоваться в рабочих приложениях.</span><span class="sxs-lookup"><span data-stu-id="aaad6-106">They may undergo changes before becoming available in the public release and should not be used in production applications.</span></span>

<span data-ttu-id="aaad6-107">Собрания являются ключевыми для продуктивности в Teams.</span><span class="sxs-lookup"><span data-stu-id="aaad6-107">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="aaad6-108">Они обеспечивают совместную работу, партнерство, информирование о связи и совместную работу на активном форуме.</span><span class="sxs-lookup"><span data-stu-id="aaad6-108">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="aaad6-109">Разработчик может создавать [настраиваемые приложения вкладок](../tabs/what-are-tabs.md#how-do-tabs-work), [Bot](../bots/what-are-bots.md)и [расширений сообщений](../messaging-extensions/what-are-messaging-extensions.md) , чтобы улучшить и расширить возможности для собраний в Teams.</span><span class="sxs-lookup"><span data-stu-id="aaad6-109">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="aaad6-110">Пользователи собраний могут получать доступ к приложениям с помощью коллекции вкладок, позволяя выполнять соответствующие сценарии, такие как предварительная настройка доски Канбан, запуск диалогового окна для проведения собрания или создание опроса после собрания.</span><span class="sxs-lookup"><span data-stu-id="aaad6-110">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="aaad6-111">Ваше приложение для собраний может обеспечить взаимодействие с пользователем для каждого этапа жизненного цикла собрания на основе состояния участника.</span><span class="sxs-lookup"><span data-stu-id="aaad6-111">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="aaad6-112">Центр расширяемости приложений собраний Teams в трех концепциях:</span><span class="sxs-lookup"><span data-stu-id="aaad6-112">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="aaad6-113">✔ **Жизненный цикл собраний** — до, во время и после кадра времени собрания.</span><span class="sxs-lookup"><span data-stu-id="aaad6-113">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="aaad6-114">**Роль участника** ✔ — организатор собрания, докладчика или участник.</span><span class="sxs-lookup"><span data-stu-id="aaad6-114">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="aaad6-115">✔ **Тип пользователя** — пользователь в группах "гость", "гость", "федеративный" или "Аноним".</span><span class="sxs-lookup"><span data-stu-id="aaad6-115">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="aaad6-116">Сценарии жизненного цикла собраний</span><span class="sxs-lookup"><span data-stu-id="aaad6-116">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="aaad6-117">Вкладки</span><span class="sxs-lookup"><span data-stu-id="aaad6-117">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aaad6-118">Как и во всех приложениях с вкладками, ваше приложение должно выполнять [процесс проверки подлинности единого входа](../tabs/how-to/authentication/auth-aad-sso.md) Teams для вкладок.</span><span class="sxs-lookup"><span data-stu-id="aaad6-118">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="aaad6-119">Взаимодействие с приложением перед собранием</span><span class="sxs-lookup"><span data-stu-id="aaad6-119">Pre-meeting app experience</span></span>

<span data-ttu-id="aaad6-120">**Подготовка к собранию:**</span><span class="sxs-lookup"><span data-stu-id="aaad6-120">**Pre-meeting experience:**</span></span>

![работа перед собранием](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="aaad6-122">**Вкладка перед собранием:**</span><span class="sxs-lookup"><span data-stu-id="aaad6-122">**Pre-meeting tab:**</span></span>

![представление вкладки перед собранием](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="aaad6-124">✔ С разрешениями пользователи могут добавлять приложения к собранию через коллекцию вкладок двумя способами:</span><span class="sxs-lookup"><span data-stu-id="aaad6-124">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="aaad6-125">&emsp;&emsp;&#9679; с помощью вкладки " **сведения** " формы планирования Teams.</span><span class="sxs-lookup"><span data-stu-id="aaad6-125">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="aaad6-126">&emsp;&emsp;&#9679; с помощью вкладки " **чат** для собраний" в существующем собрании.</span><span class="sxs-lookup"><span data-stu-id="aaad6-126">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="aaad6-127">Вкладки ✔ доступны на страницах **сведений о** собраниях и **беседах** с помощью кнопки со значком плюс (➕). |</span><span class="sxs-lookup"><span data-stu-id="aaad6-127">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="aaad6-128">Взаимодействие с приложением для собраний</span><span class="sxs-lookup"><span data-stu-id="aaad6-128">In-meeting app experience</span></span>

<span data-ttu-id="aaad6-129">✔ Приложения собраний будут размещаться в верхней верхней панели окна Chat и на вкладке "в собрании". Когда пользователи добавляют вкладку на собрание с помощью коллекции вкладок, будут отображаться приложения, находящиеся **во время проведения собрания** .</span><span class="sxs-lookup"><span data-stu-id="aaad6-129">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="aaad6-130">✔ С разрешениями пользователи могут добавлять приложения во время собрания.</span><span class="sxs-lookup"><span data-stu-id="aaad6-130">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="aaad6-131">✔ При загрузке в контексте собрания приложения смогут использовать клиентский пакет SDK Teams для доступа к серверам, а также `meetingId` `userMri` `frameContext` для надлежащего отображения интерфейса.</span><span class="sxs-lookup"><span data-stu-id="aaad6-131">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="aaad6-132">✔ Для приложения могут быть видны в собрании Teams в двух областях:</span><span class="sxs-lookup"><span data-stu-id="aaad6-132">✔ For an app can be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="aaad6-133">&emsp;&emsp;&#9679; **боковой панели**.</span><span class="sxs-lookup"><span data-stu-id="aaad6-133">&emsp;&emsp;&#9679; **Side panel**.</span></span> </br>

> [!NOTE]
> <span data-ttu-id="aaad6-134">Если _манифест приложения_ указывает, что вкладка [оптимизирована для боковой панели](create-apps-for-teams-meetings.md#in-meeting), здесь будет отображаться эта вкладка.</span><span class="sxs-lookup"><span data-stu-id="aaad6-134">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#in-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="aaad6-135">Она также может быть частью интерфейса подающего лоток, в соответствии с указанными рекомендациями по проектированию.</span><span class="sxs-lookup"><span data-stu-id="aaad6-135">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="aaad6-136">&emsp;&emsp;&#9679; **диалоговое окно собраний**.</span><span class="sxs-lookup"><span data-stu-id="aaad6-136">&emsp;&emsp;&#9679; **In-meeting dialog**.</span></span> <span data-ttu-id="aaad6-137">Используйте диалоговое окно "в собрании" для демонстрации действий, выполняемых участниками собрания.</span><span class="sxs-lookup"><span data-stu-id="aaad6-137">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="aaad6-138">*Ознакомьтесь* с разделом [Создание приложений для собраний Teams](create-apps-for-teams-meetings.md).</span><span class="sxs-lookup"><span data-stu-id="aaad6-138">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="aaad6-139">**Возможности для собраний:**</span><span class="sxs-lookup"><span data-stu-id="aaad6-139">**In-meeting experience:**</span></span>

![взаимодействие с собраниями](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Представление на собрании — диалоговое окно](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="aaad6-142">**Диалоговое окно с действиями в собрании для пользователей:**</span><span class="sxs-lookup"><span data-stu-id="aaad6-142">**In-meeting actionable dialog for users:**</span></span>

![Представление диалоговых окон](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="aaad6-144">Взаимодействие с приложениями после собраний</span><span class="sxs-lookup"><span data-stu-id="aaad6-144">Post-meeting app experience</span></span>

<span data-ttu-id="aaad6-145">**Взаимодействие после собрания:**</span><span class="sxs-lookup"><span data-stu-id="aaad6-145">**Post-meeting experience:**</span></span>

![представление "опубликовать собрание"](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="aaad6-147">Сценарий приложения после собрания аналогичен текущему действию, связанному с собранием, с дополнительным преимуществом использования вкладок в области.</span><span class="sxs-lookup"><span data-stu-id="aaad6-147">The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs exist within the surface.</span></span> <span data-ttu-id="aaad6-148">Пользователи с разрешениями могут добавлять приложения из коллекции вкладок на собрание с помощью вкладки " **сведения** " в форме "Планирование команд" и на вкладке **чат** Meeting в существующем собрании.</span><span class="sxs-lookup"><span data-stu-id="aaad6-148">Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

### <a name="bots"></a><span data-ttu-id="aaad6-149">Боты</span><span class="sxs-lookup"><span data-stu-id="aaad6-149">Bots</span></span>

<span data-ttu-id="aaad6-150">В этой статье представлены сведения о реализации [боты в документации по собраниям Teams](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) .</span><span class="sxs-lookup"><span data-stu-id="aaad6-150">For bot implementation, please see our [Bots in Teams meetings](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) documentation.</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="aaad6-151">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="aaad6-151">Messaging Extensions</span></span>

<span data-ttu-id="aaad6-152">Для реализации расширения для обмена сообщениями ознакомьтесь [с нашими расширениями обмена сообщениями в документации по собраниям Teams](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) .</span><span class="sxs-lookup"><span data-stu-id="aaad6-152">For messaging extension implementation, please see our [Messaging extensions in Teams meetings](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) documentation.</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="aaad6-153">Роли участников и типы пользователей на собрании</span><span class="sxs-lookup"><span data-stu-id="aaad6-153">Participant roles and user types in a meeting</span></span>

![Участники собрания](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="aaad6-155">Роли участников</span><span class="sxs-lookup"><span data-stu-id="aaad6-155">Participant roles</span></span>

<span data-ttu-id="aaad6-156">Вы можете разработать приложение с проверкой подлинности, зависящей от участников.</span><span class="sxs-lookup"><span data-stu-id="aaad6-156">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="aaad6-157">Например, возможно, только организатор или докладчик могут создать опрос в собраниях.</span><span class="sxs-lookup"><span data-stu-id="aaad6-157">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="aaad6-158">Несмотря на то, что параметры участников по умолчанию определяются ИТ ИТ администратором, организатору собрания может потребоваться изменить параметры для определенного собрания.</span><span class="sxs-lookup"><span data-stu-id="aaad6-158">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="aaad6-159">Организаторов могут вносить эти изменения на веб-странице параметров собрания.</span><span class="sxs-lookup"><span data-stu-id="aaad6-159">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="aaad6-160">**Организатор**.</span><span class="sxs-lookup"><span data-stu-id="aaad6-160">**Organizer**.</span></span> <span data-ttu-id="aaad6-161">Организатор планирует собрание, задает параметры собрания, назначает роли собраний и запускает собрание.</span><span class="sxs-lookup"><span data-stu-id="aaad6-161">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="aaad6-162">Только пользователи с учетной записью M365 (обладающими лицензией Teams) могут быть организаторов и управлять разрешениями участников.</span><span class="sxs-lookup"><span data-stu-id="aaad6-162">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="aaad6-163">**Выступающий**.</span><span class="sxs-lookup"><span data-stu-id="aaad6-163">**Presenter**.</span></span> <span data-ttu-id="aaad6-164">У докладчиков почти те же возможности, что и у организатора; Однако докладчик не может удалить организатора из сеанса или изменить параметры собрания для этого сеанса.</span><span class="sxs-lookup"><span data-stu-id="aaad6-164">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="aaad6-165">По умолчанию участники, присоединяющиеся к собранию, имеют роль докладчика.</span><span class="sxs-lookup"><span data-stu-id="aaad6-165">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="aaad6-166">**Участник**.</span><span class="sxs-lookup"><span data-stu-id="aaad6-166">**Attendee**.</span></span> <span data-ttu-id="aaad6-167">Участник — это пользователь, приглашенный на собрание, но не уполномоченный выступающий в качестве докладчика.</span><span class="sxs-lookup"><span data-stu-id="aaad6-167">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="aaad6-168">Участники могут взаимодействовать с другими участниками собрания, но не могут управлять параметрами собрания или общими контентом.</span><span class="sxs-lookup"><span data-stu-id="aaad6-168">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="aaad6-169">_Просмотр_ [ **ролей в собрании Teams**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="aaad6-169">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="aaad6-170">Вы можете получить доступ к странице  **параметры собрания** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="aaad6-170">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="aaad6-171">&#11200; в Teams откройте раздел **Календарь календаря** ![ ](../assets/images/apps-in-meetings/calendar-logo.png) , выберите собрание, а затем — **параметры собрания**.</span><span class="sxs-lookup"><span data-stu-id="aaad6-171">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

<span data-ttu-id="aaad6-172">&#11200; в приглашении на собрание выберите **параметры собрания**.</span><span class="sxs-lookup"><span data-stu-id="aaad6-172">&#11200; In a meeting invitation, select **Meeting options**.</span></span>

<span data-ttu-id="aaad6-173">&#11200; во время собрания Установите флажок **Показывать участников** ![ Отображать значок участников ](../assets/images/apps-in-meetings/show-participants.png) в элементах управления собрания.</span><span class="sxs-lookup"><span data-stu-id="aaad6-173">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="aaad6-174">Затем над списком участников выберите **Управление разрешениями**.</span><span class="sxs-lookup"><span data-stu-id="aaad6-174">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="aaad6-175">Типы пользователей.</span><span class="sxs-lookup"><span data-stu-id="aaad6-175">User types</span></span>

> [!NOTE]
> <span data-ttu-id="aaad6-176">Пользовательские типы могут присоединяться к собраниям и принимать одну из ролей участника, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="aaad6-176">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="aaad6-177">Тип пользователя не предоставляется в составе API **жетпартиЦипантроле** .</span><span class="sxs-lookup"><span data-stu-id="aaad6-177">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="aaad6-178">**В клиенте**.</span><span class="sxs-lookup"><span data-stu-id="aaad6-178">**In-tenant**.</span></span> <span data-ttu-id="aaad6-179">Эти пользователи принадлежат организации и имеют учетные данные в Azure Active Directory для клиента.</span><span class="sxs-lookup"><span data-stu-id="aaad6-179">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="aaad6-180">Обычно они являются полноценными, сотрудниками или удаленными сотрудниками.</span><span class="sxs-lookup"><span data-stu-id="aaad6-180">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="aaad6-181">**Гость**.</span><span class="sxs-lookup"><span data-stu-id="aaad6-181">**Guest**.</span></span> <span data-ttu-id="aaad6-182">Гость — это участник другой организации, который был приглашен на доступ к Teams и другим ресурсам в клиенте Организации.</span><span class="sxs-lookup"><span data-stu-id="aaad6-182">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="aaad6-183">Гости добавляются в Active Directory вашей организации, и им могут быть предоставлены почти все возможности Teams в качестве собственного члена группы с полным доступом к разговорам групп, собраниям и файлам.</span><span class="sxs-lookup"><span data-stu-id="aaad6-183">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="aaad6-184">_Просмотр_ [гостевого доступа в Microsoft Teams](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="aaad6-184">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="aaad6-185">**Федеративные и внешние**.</span><span class="sxs-lookup"><span data-stu-id="aaad6-185">**Federated/External**.</span></span> <span data-ttu-id="aaad6-186">Федеративный пользователь — это пользователь внешней группы в другой организации, приглашенный на присоединение к собранию.</span><span class="sxs-lookup"><span data-stu-id="aaad6-186">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="aaad6-187">Так как эти пользователи имеют действительные учетные данные с федеративными партнерами, они считаются подлинными в Teams, но не имеют доступа к рабочим группам или другим общим ресурсам Организации.</span><span class="sxs-lookup"><span data-stu-id="aaad6-187">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="aaad6-188">Если вы хотите, чтобы внешние пользователи могли получать доступ к Teams и каналам, гостевой доступ может быть лучший вариант.</span><span class="sxs-lookup"><span data-stu-id="aaad6-188">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="aaad6-189">_Просмотр_ [управления внешним доступом в Microsoft Teams](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="aaad6-189">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="aaad6-190">**Анонимный**доступ.</span><span class="sxs-lookup"><span data-stu-id="aaad6-190">**Anonymous**.</span></span> <span data-ttu-id="aaad6-191">Анонимные пользователи не имеют удостоверения Active Directory и не объединены с клиентом.</span><span class="sxs-lookup"><span data-stu-id="aaad6-191">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="aaad6-192">Анонимный участник похож на внешнего пользователя, но его удостоверение не проецируется на собрание.</span><span class="sxs-lookup"><span data-stu-id="aaad6-192">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="aaad6-193">Анонимные пользователи не смогут получать доступ к приложениям в окне собрания.</span><span class="sxs-lookup"><span data-stu-id="aaad6-193">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaad6-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aaad6-194">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aaad6-195">Создание приложений для собраний групп</span><span class="sxs-lookup"><span data-stu-id="aaad6-195">Create apps for Teams meetings</span></span>](create-apps-for-teams-meetings.md)
