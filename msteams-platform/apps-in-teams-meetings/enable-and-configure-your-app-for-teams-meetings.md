---
title: Включить и настроить приложения для Teams собраний
author: surbhigupta
description: Включить и настроить приложения для Teams собраний
ms.topic: conceptual
ms.openlocfilehash: 4b71673b683129ef00c01297ce14a677864d4eb4
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114186"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a><span data-ttu-id="75ef7-103">Включить и настроить приложения для Teams собраний</span><span class="sxs-lookup"><span data-stu-id="75ef7-103">Enable and configure your apps for Teams meetings</span></span>

<span data-ttu-id="75ef7-104">Каждая команда имеет свой способ общения и совместной работы.</span><span class="sxs-lookup"><span data-stu-id="75ef7-104">Every team has a different way of communicating and collaborating tasks.</span></span> <span data-ttu-id="75ef7-105">Вы можете достичь этих различных задач, Teams с приложениями для собраний.</span><span class="sxs-lookup"><span data-stu-id="75ef7-105">You can achieve these different tasks by customizing Teams with apps for meetings.</span></span> <span data-ttu-id="75ef7-106">Чтобы настроить и достичь различных задач, необходимо включить приложения для Teams собраний и настроить приложения, которые будут доступны в области собраний в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="75ef7-106">To customize and to achieve different tasks, you must enable your apps for Teams meetings and configure your apps to be available in meeting scope within their app manifest.</span></span>

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="75ef7-107">Включить приложение для Teams собраний</span><span class="sxs-lookup"><span data-stu-id="75ef7-107">Enable your app for Teams meetings</span></span>

<span data-ttu-id="75ef7-108">Чтобы включить приложение для Teams собраний, необходимо обновить манифест приложения и использовать свойства контекста, чтобы определить, где должно отображаться ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="75ef7-108">To enable your app for Teams meetings, you must update your app manifest and use the context properties to determine where your app must appear.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="75ef7-109">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="75ef7-109">Update your app manifest</span></span>

<span data-ttu-id="75ef7-110">Возможности приложения собраний объявляются в манифесте приложения с помощью `configurableTabs` массивов и `scopes` `context` массивов.</span><span class="sxs-lookup"><span data-stu-id="75ef7-110">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="75ef7-111">Область определяет, кому и в котором контекст определяет, где доступно ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="75ef7-111">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> * <span data-ttu-id="75ef7-112">Попробуйте обновить манифест приложения с помощью [схемы манифеста.](../resources/schema/manifest-schema-dev-preview.md)</span><span class="sxs-lookup"><span data-stu-id="75ef7-112">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> * <span data-ttu-id="75ef7-113">Приложения на собраниях требуют области группового чата.</span><span class="sxs-lookup"><span data-stu-id="75ef7-113">Apps in meetings require groupchat scope.</span></span> <span data-ttu-id="75ef7-114">Область команды работает только для вкладок в каналах.</span><span class="sxs-lookup"><span data-stu-id="75ef7-114">The team scope works for tabs in channels only.</span></span>

<span data-ttu-id="75ef7-115">Манифест приложения должен включать следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="75ef7-115">The app manifest must include the following code snippet:</span></span>

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```

> [!NOTE]
> <span data-ttu-id="75ef7-116">`meetingStage` в настоящее время доступна [только в предварительном просмотре](../resources/dev-preview/developer-preview-intro.md) разработчика.</span><span class="sxs-lookup"><span data-stu-id="75ef7-116">`meetingStage` is currently available in [developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

### <a name="context-property"></a><span data-ttu-id="75ef7-117">Свойство Context</span><span class="sxs-lookup"><span data-stu-id="75ef7-117">Context property</span></span>

<span data-ttu-id="75ef7-118">Свойство определяет, что должно быть показано, когда пользователь вызывает приложение на собрании в зависимости от того, где пользователь вызывает `context` приложение.</span><span class="sxs-lookup"><span data-stu-id="75ef7-118">The `context` property determines what must be shown when a user invokes an app in a meeting depending on where the user invokes the app.</span></span> <span data-ttu-id="75ef7-119">Вкладка `context` и свойства позволяют `scopes` определить, где должно отображаться ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="75ef7-119">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="75ef7-120">Вкладки в области или области `team` `groupchat` могут иметь несколько контекстов.</span><span class="sxs-lookup"><span data-stu-id="75ef7-120">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="75ef7-121">Ниже ниже 10 значений для свойства, из которого можно использовать все или некоторые `context` из этих значений:</span><span class="sxs-lookup"><span data-stu-id="75ef7-121">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="75ef7-122">Значение</span><span class="sxs-lookup"><span data-stu-id="75ef7-122">Value</span></span>|<span data-ttu-id="75ef7-123">Описание</span><span class="sxs-lookup"><span data-stu-id="75ef7-123">Description</span></span>|
|---|---|
| <span data-ttu-id="75ef7-124">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="75ef7-124">**channelTab**</span></span> | <span data-ttu-id="75ef7-125">Вкладка в загонах канала команды.</span><span class="sxs-lookup"><span data-stu-id="75ef7-125">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="75ef7-126">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="75ef7-126">**privateChatTab**</span></span> | <span data-ttu-id="75ef7-127">Вкладка в загонах группового чата между набором пользователей, а не в контексте группы или собрания.</span><span class="sxs-lookup"><span data-stu-id="75ef7-127">A tab in the header of a group chat between a set of users, not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="75ef7-128">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="75ef7-128">**meetingChatTab**</span></span> | <span data-ttu-id="75ef7-129">Вкладка в загонах группового чата между набором пользователей в контексте запланированного собрания.</span><span class="sxs-lookup"><span data-stu-id="75ef7-129">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="75ef7-130">**meetingDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="75ef7-130">**meetingDetailsTab**</span></span> | <span data-ttu-id="75ef7-131">Вкладка в загонах сведений о собрании для просмотра календаря.</span><span class="sxs-lookup"><span data-stu-id="75ef7-131">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="75ef7-132">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="75ef7-132">**meetingSidePanel**</span></span> | <span data-ttu-id="75ef7-133">Панель на собрании, открытая через единую панель (U-bar).</span><span class="sxs-lookup"><span data-stu-id="75ef7-133">An in-meeting panel opened through the unified bar (U-bar).</span></span> |
| <span data-ttu-id="75ef7-134">**meetingStage**</span><span class="sxs-lookup"><span data-stu-id="75ef7-134">**meetingStage**</span></span> | <span data-ttu-id="75ef7-135">Приложение из meetingSidePanel можно использовать на стадии собрания.</span><span class="sxs-lookup"><span data-stu-id="75ef7-135">An app from the meetingSidePanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="75ef7-136">`Context` свойство в настоящее время не поддерживается для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="75ef7-136">`Context` property is currently not supported on mobile clients.</span></span>

<span data-ttu-id="75ef7-137">После встройки приложения для Teams собраний необходимо настроить приложение перед собранием, во время собрания и после собрания.</span><span class="sxs-lookup"><span data-stu-id="75ef7-137">After you enable your app for Teams meetings, you must configure your app before a meeting, during a meeting, and after a meeting.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="75ef7-138">Настройка приложения для сценариев собраний</span><span class="sxs-lookup"><span data-stu-id="75ef7-138">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="75ef7-139">Чтобы приложение было видно в галерее вкладок, оно должно поддерживать настраиваемые вкладки и область группового чата.</span><span class="sxs-lookup"><span data-stu-id="75ef7-139">For your app to be visible in the tab gallery, it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="75ef7-140">Мобильные клиенты поддерживают вкладки только на этапах предварительного и после собраний.</span><span class="sxs-lookup"><span data-stu-id="75ef7-140">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="75ef7-141">В настоящее время в мобильных клиентах не поддерживается диалоговое окно и вкладка на собрании.</span><span class="sxs-lookup"><span data-stu-id="75ef7-141">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="75ef7-142">Дополнительные сведения см. [в руководстве по вкладке на мобильном устройстве](../tabs/design/tabs-mobile.md) при создании вкладок для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="75ef7-142">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) while creating your tabs for mobile.</span></span>

<span data-ttu-id="75ef7-143">Teams собрания предоставляют уникальный опыт совместной работы для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="75ef7-143">Teams meetings provides a unique collaborative experience for your organization.</span></span> <span data-ttu-id="75ef7-144">Это позволяет настроить приложение для различных сценариев собраний.</span><span class="sxs-lookup"><span data-stu-id="75ef7-144">It provides the opportunity to configure your app for different meeting scenarios.</span></span> <span data-ttu-id="75ef7-145">Вы можете настроить приложения, чтобы повысить качество собраний в зависимости от роли участника или типа пользователя.</span><span class="sxs-lookup"><span data-stu-id="75ef7-145">You can configure your apps to enhance the meeting experience based on participant role or user type.</span></span> <span data-ttu-id="75ef7-146">Теперь вы можете определить, какие действия можно принять в следующих сценариях собраний:</span><span class="sxs-lookup"><span data-stu-id="75ef7-146">Now you can identify what actions can be taken in the following meeting scenarios:</span></span>

* [<span data-ttu-id="75ef7-147">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="75ef7-147">Before a meeting</span></span>](#before-a-meeting)
* [<span data-ttu-id="75ef7-148">Во время собрания</span><span class="sxs-lookup"><span data-stu-id="75ef7-148">During a meeting</span></span>](#during-a-meeting)
* [<span data-ttu-id="75ef7-149">После собрания</span><span class="sxs-lookup"><span data-stu-id="75ef7-149">After a meeting</span></span>](#after-a-meeting)

### <a name="before-a-meeting"></a><span data-ttu-id="75ef7-150">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="75ef7-150">Before a meeting</span></span>

<span data-ttu-id="75ef7-151">Перед собранием пользователи могут добавлять вкладки, боты и расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="75ef7-151">Before a meeting, users can add tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="75ef7-152">Пользователи с ролями организатора и презентовщика могут добавлять вкладки в собрание.</span><span class="sxs-lookup"><span data-stu-id="75ef7-152">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="75ef7-153">**Добавление вкладки к собранию**</span><span class="sxs-lookup"><span data-stu-id="75ef7-153">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="75ef7-154">В календаре выберите собрание, на которое нужно добавить вкладку.</span><span class="sxs-lookup"><span data-stu-id="75ef7-154">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="75ef7-155">Выберите **вкладку Details** и выберите</span><span class="sxs-lookup"><span data-stu-id="75ef7-155">Select the **Details** tab and select</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="75ef7-156">.</span><span class="sxs-lookup"><span data-stu-id="75ef7-156">.</span></span>

    ![Опыт предварительного собрания](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="75ef7-158">В галерее вкладок, которая появится, выберите приложение, которое необходимо добавить, и выполните необходимые действия.</span><span class="sxs-lookup"><span data-stu-id="75ef7-158">In the tab gallery that appears, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="75ef7-159">Приложение устанавливается в качестве вкладки.</span><span class="sxs-lookup"><span data-stu-id="75ef7-159">The app is installed as a tab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="75ef7-160">В настоящее время на вкладке "Собрания" сведения о собраниях и сведения о участниках не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="75ef7-160">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="75ef7-161">**Добавление расширения обмена сообщениями на собрание**</span><span class="sxs-lookup"><span data-stu-id="75ef7-161">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="75ef7-162">Выберите эллипсы &#x25CF;&#x25CF;&#x25CF; , расположенные в области составить сообщение в чате.</span><span class="sxs-lookup"><span data-stu-id="75ef7-162">Select the ellipses &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="75ef7-163">Выберите приложение, которое необходимо добавить, и выполните необходимые действия.</span><span class="sxs-lookup"><span data-stu-id="75ef7-163">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="75ef7-164">Приложение устанавливается в качестве расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="75ef7-164">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="75ef7-165">**Добавление бота на собрание**</span><span class="sxs-lookup"><span data-stu-id="75ef7-165">**To add a bot to a meeting**</span></span>

<span data-ttu-id="75ef7-166">В чате собраний **@** введите ключ и выберите **Get bots**.</span><span class="sxs-lookup"><span data-stu-id="75ef7-166">In a meeting chat, enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="75ef7-167">Удостоверение пользователя должно быть подтверждено с помощью [SSO Tabs.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="75ef7-167">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="75ef7-168">После проверки подлинности приложение может получить роль пользователя с помощью `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="75ef7-168">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="75ef7-169">В зависимости от роли пользователя приложение может предоставлять определенные функции.</span><span class="sxs-lookup"><span data-stu-id="75ef7-169">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="75ef7-170">Например, приложение для опроса позволяет создавать новый опрос только организаторам и презентаторам.</span><span class="sxs-lookup"><span data-stu-id="75ef7-170">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="75ef7-171">Назначения ролей могут быть изменены во время собрания.</span><span class="sxs-lookup"><span data-stu-id="75ef7-171">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="75ef7-172">Дополнительные сведения см. [в Teams собрания.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="75ef7-172">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="75ef7-173">Во время собрания</span><span class="sxs-lookup"><span data-stu-id="75ef7-173">During a meeting</span></span>

<span data-ttu-id="75ef7-174">Во время собрания вы можете использовать диалоговое окно meetingSidePanel или диалоговое окно для собраний для создания уникальных приложений.</span><span class="sxs-lookup"><span data-stu-id="75ef7-174">During a meeting, you can use the meetingSidePanel or the in-meeting dialog box to build unique experiences for your apps.</span></span>

#### <a name="meetingsidepanel"></a><span data-ttu-id="75ef7-175">meetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="75ef7-175">meetingSidePanel</span></span>

<span data-ttu-id="75ef7-176">С помощью meetingSidePanel можно настроить опыт собрания, который позволяет организаторам и презентаторам иметь различные представления и действия.</span><span class="sxs-lookup"><span data-stu-id="75ef7-176">With the meetingSidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="75ef7-177">В манифесте приложения необходимо добавить meetingSidePanel в массив контекста.</span><span class="sxs-lookup"><span data-stu-id="75ef7-177">In your app manifest, you must add meetingSidePanel to the context array.</span></span> <span data-ttu-id="75ef7-178">В собрании и во всех сценариях приложение отрисовка в вкладке в собрании шириной 320 пикселей.</span><span class="sxs-lookup"><span data-stu-id="75ef7-178">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="75ef7-179">Дополнительные сведения см. в [интерфейсе FrameContext.](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="75ef7-179">For more information, see [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true).</span></span>

<span data-ttu-id="75ef7-180">Чтобы использовать `userContext` API для соответственного маршрута запросов, см. Teams [SDK](../tabs/how-to/access-teams-context.md#user-context).</span><span class="sxs-lookup"><span data-stu-id="75ef7-180">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="75ef7-181">Дополнительные сведения см. [в Teams поток проверки подлинности для вкладок.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="75ef7-181">For more information, see [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="75ef7-182">Поток проверки подлинности для вкладок очень похож на поток проверки подлинности для веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="75ef7-182">Authentication flow for tabs is very similar to the authentication flow for websites.</span></span> <span data-ttu-id="75ef7-183">Таким образом, вкладки могут напрямую использовать OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="75ef7-183">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="75ef7-184">Дополнительные сведения см. [в платформа удостоверений Майкрософт oAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)</span><span class="sxs-lookup"><span data-stu-id="75ef7-184">For more information, see [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="75ef7-185">Расширение обмена сообщениями работает так, как и ожидалось, когда пользователь находится в представлении на собрании, и пользователь может отправлять составить карточки расширения сообщений.</span><span class="sxs-lookup"><span data-stu-id="75ef7-185">Messaging extension works as expected when a user is in an in-meeting view, and the user can post compose message extension cards.</span></span> <span data-ttu-id="75ef7-186">AppName in-meeting — это инструмент, который сообщает имя приложения на собрании U-bar.</span><span class="sxs-lookup"><span data-stu-id="75ef7-186">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

> [!NOTE]
> <span data-ttu-id="75ef7-187">Используйте версию 1.7.0 или более высокую Teams [SDK,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)так как версии до нее не поддерживают боковую панель.</span><span class="sxs-lookup"><span data-stu-id="75ef7-187">Use version 1.7.0 or higher of [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.</span></span>

#### <a name="in-meeting-dialog-box"></a><span data-ttu-id="75ef7-188">Диалоговое окно на собрании</span><span class="sxs-lookup"><span data-stu-id="75ef7-188">In-meeting dialog box</span></span>

<span data-ttu-id="75ef7-189">Диалоговое окно на собрании можно использовать для вовлечения участников во время собрания и сбора сведений или отзывов во время собрания.</span><span class="sxs-lookup"><span data-stu-id="75ef7-189">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="75ef7-190">Используйте [`NotificationSignal`](create-apps-for-teams-meetings.md#notificationsignal-api) API для сигнала о том, что необходимо вызвать уведомление о пузыре.</span><span class="sxs-lookup"><span data-stu-id="75ef7-190">Use the [`NotificationSignal`](create-apps-for-teams-meetings.md#notificationsignal-api) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="75ef7-191">В качестве полезной нагрузки запроса уведомлений включайте URL-адрес, на котором будет хозяйствовать контент.</span><span class="sxs-lookup"><span data-stu-id="75ef7-191">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="75ef7-192">Диалоговое окно на собрании не должно использовать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="75ef7-192">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="75ef7-193">Модуль задач не вызывается в чате собрания.</span><span class="sxs-lookup"><span data-stu-id="75ef7-193">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="75ef7-194">Url-адрес внешнего ресурса используется для отображения пузыря контента на собрании.</span><span class="sxs-lookup"><span data-stu-id="75ef7-194">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="75ef7-195">Этот метод можно `submitTask` использовать для отправки данных в чате собраний.</span><span class="sxs-lookup"><span data-stu-id="75ef7-195">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="75ef7-196">Необходимо вызвать функцию [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического увольнения после действия пользователя в веб-представлении.</span><span class="sxs-lookup"><span data-stu-id="75ef7-196">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web view.</span></span> <span data-ttu-id="75ef7-197">Это требование для отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="75ef7-197">This is a requirement for app submission.</span></span> <span data-ttu-id="75ef7-198">Дополнительные сведения см. [в Teams SDK task module.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="75ef7-198">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="75ef7-199">Если вы хотите, чтобы ваше приложение поддержало анонимных пользователей, то при первоначальном запросе необходимо использовать метаданные запроса в объекте, а не `from.id` `from` `from.aadObjectId` метаданные запроса.</span><span class="sxs-lookup"><span data-stu-id="75ef7-199">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="75ef7-200">`from.id`является ИД пользователя и является `from.aadObjectId` Azure Active Directory (AAD) пользователя.</span><span class="sxs-lookup"><span data-stu-id="75ef7-200">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="75ef7-201">Дополнительные сведения см. в [таблицах](../task-modules-and-cards/task-modules/task-modules-tabs.md) с использованием модулей задач и созданием и [отправкой модуля задач.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="75ef7-201">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="shared-meeting-stage"></a><span data-ttu-id="75ef7-202">Общий этап собраний</span><span class="sxs-lookup"><span data-stu-id="75ef7-202">Shared meeting stage</span></span>

> [!NOTE]
> * <span data-ttu-id="75ef7-203">В настоящее время эта возможность доступна только [в предварительном просмотре разработчика.](../resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="75ef7-203">This capability is currently available in [developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="75ef7-204">Общая стадия собрания позволяет участникам собраний взаимодействовать с контентом приложений и сотрудничать с ними в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="75ef7-204">Shared meeting stage allows meeting participants to interact with and collaborate on app content in real-time.</span></span>

<span data-ttu-id="75ef7-205">Необходимый контекст находится `meetingStage` в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="75ef7-205">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="75ef7-206">Обязательным условием для этого является `meetingSidePanel` контекст.</span><span class="sxs-lookup"><span data-stu-id="75ef7-206">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="75ef7-207">Это позволяет **использовать Share** в собранииSidePanel.</span><span class="sxs-lookup"><span data-stu-id="75ef7-207">This enables **Share** in the meetingSidePanel.</span></span>

![Share to stage during meeting experience](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="75ef7-209">Чтобы включить общий этап собраний, настройте манифест приложения таким образом:</span><span class="sxs-lookup"><span data-stu-id="75ef7-209">To enable shared meeting stage, configure your app manifest like this:</span></span>

```json
"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```

<span data-ttu-id="75ef7-210">Узнайте, как [создать общий опыт на этапе собраний.](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="75ef7-210">See how to [design a shared meeting stage experience](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="75ef7-211">После собрания</span><span class="sxs-lookup"><span data-stu-id="75ef7-211">After a meeting</span></span>

<span data-ttu-id="75ef7-212">Конфигурации после и [до собраний](#before-a-meeting) одинаковы.</span><span class="sxs-lookup"><span data-stu-id="75ef7-212">The configurations after and [before meetings](#before-a-meeting) are the same.</span></span>

## <a name="code-sample"></a><span data-ttu-id="75ef7-213">Пример кода</span><span class="sxs-lookup"><span data-stu-id="75ef7-213">Code sample</span></span>

|<span data-ttu-id="75ef7-214">Пример имени</span><span class="sxs-lookup"><span data-stu-id="75ef7-214">Sample name</span></span> | <span data-ttu-id="75ef7-215">Описание</span><span class="sxs-lookup"><span data-stu-id="75ef7-215">Description</span></span> | <span data-ttu-id="75ef7-216">Пример</span><span class="sxs-lookup"><span data-stu-id="75ef7-216">Sample</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="75ef7-217">Приложение для собраний</span><span class="sxs-lookup"><span data-stu-id="75ef7-217">Meeting app</span></span> | <span data-ttu-id="75ef7-218">Демонстрирует, как использовать приложение Генератор маркеров собраний для запроса маркера, который создается последовательно, чтобы каждый участник имел справедливую возможность внести свой вклад в собрание.</span><span class="sxs-lookup"><span data-stu-id="75ef7-218">Demonstrates how to use the Meeting Token Generator app to request a token, which is generated sequentially so that each participant has a fair opportunity to contribute in a meeting.</span></span> <span data-ttu-id="75ef7-219">Это может быть полезно в таких ситуациях, как scrum meetings и Q&сеансов.</span><span class="sxs-lookup"><span data-stu-id="75ef7-219">This can be useful in situations like scrum meetings and Q&A sessions.</span></span> | [<span data-ttu-id="75ef7-220">View</span><span class="sxs-lookup"><span data-stu-id="75ef7-220">View</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token) |

## <a name="see-also"></a><span data-ttu-id="75ef7-221">См. также</span><span class="sxs-lookup"><span data-stu-id="75ef7-221">See also</span></span>

* [<span data-ttu-id="75ef7-222">Рекомендации по проектированию диалогов на собрании</span><span class="sxs-lookup"><span data-stu-id="75ef7-222">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="75ef7-223">Teams потока проверки подлинности для вкладок</span><span class="sxs-lookup"><span data-stu-id="75ef7-223">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
