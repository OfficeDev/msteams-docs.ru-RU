---
title: Виртуальный помощник для Microsoft Teams
description: Создание бота и навыков виртуального помощника для использования в Microsoft Teams
ms.topic: how-to
keywords: Боты виртуального помощника teams
ms.openlocfilehash: d72b1afbf975707d694d4aaef31263a3ce467629
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014616"
---
# <a name="virtual-assistant-for-microsoft-teams"></a><span data-ttu-id="54484-104">Виртуальный помощник для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="54484-104">Virtual Assistant for Microsoft Teams</span></span>

<span data-ttu-id="54484-105">Виртуальный помощник — это шаблон Microsoft с открытым исходным кодом, который позволяет создавать надежное решение для бесед, сохраняя полный контроль над пользовательским интерфейсом, фирмой и необходимыми данными.</span><span class="sxs-lookup"><span data-stu-id="54484-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="54484-106">Основной [](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) шаблон виртуального помощника — это базовый базовый блок, который объединяет технологии Майкрософт, необходимые для создания виртуального помощника, в том числе bot [Framework SDK,](https://github.com/microsoft/botframework-sdk) [language Understanding (КОДИБ)](https://www.luis.ai/)и [QnA Maker,](https://www.qnamaker.ai/)а также основные возможности, включая регистрацию навыков, связанные учетные записи, базовое намерение для общения, чтобы предоставить конечным пользователям широкий спектр удобных взаимодействий и возможностей.</span><span class="sxs-lookup"><span data-stu-id="54484-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), as well as essential capabilities including  skills registration, linked accounts, basic conversational intent to offer end users a range of seamless interactions and experiences.</span></span> <span data-ttu-id="54484-107">Кроме того, возможности шаблона включают в себя богатые примеры навыков для повторного работы с [беседами.](https://microsoft.github.io/botframework-solutions/overview/skills)</span><span class="sxs-lookup"><span data-stu-id="54484-107">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="54484-108">Отдельные навыки можно интегрировать в решение виртуального помощника для реализации нескольких сценариев.</span><span class="sxs-lookup"><span data-stu-id="54484-108">Individual skills can be integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="54484-109">С помощью SDK Bot Framework skills представлены в форме с исходным кодом, что позволяет настраивать и расширять их по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="54484-109">Using the Bot Framework SDK, Skills are presented in source code form enabling you to customize and extend as required.</span></span> <span data-ttu-id="54484-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="54484-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span>

![Обзорная схема виртуального помощника](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="54484-112">Действия текстовых сообщений перенаправлются на связанные навыки ядром виртуального помощника с помощью модели [отправки.](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs)</span><span class="sxs-lookup"><span data-stu-id="54484-112">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="54484-113">Вопросы реализации</span><span class="sxs-lookup"><span data-stu-id="54484-113">Implementation considerations</span></span>

<span data-ttu-id="54484-114">Решение о добавлении виртуального помощника может включать множество детерминант и отличаться для каждой организации.</span><span class="sxs-lookup"><span data-stu-id="54484-114">The decision to add a Virtual Assistant can include many determinants and differ for each organization.</span></span> <span data-ttu-id="54484-115">Вот факторы, которые поддерживают реализацию виртуального помощника для вашей организации:</span><span class="sxs-lookup"><span data-stu-id="54484-115">Here are the factors that support implementing a Virtual Assistant for your organization:</span></span>

- <span data-ttu-id="54484-116">Центральная команда управляет всеми возможностями сотрудников и может создавать виртуальный помощник и управлять обновлениями для основного опыта, включая добавление новых навыков.</span><span class="sxs-lookup"><span data-stu-id="54484-116">A central team manages all employee experiences and has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
- <span data-ttu-id="54484-117">Существует несколько приложений в различных бизнес-функциях и/или ожидается, что их число будет увеличиваться в будущем.</span><span class="sxs-lookup"><span data-stu-id="54484-117">Multiple applications exist across business functions and/or the number is expected to grow in the future.</span></span>
- <span data-ttu-id="54484-118">Существующие приложения можно настраивать, принадлежат организации и могут преобразовывать в навыки для виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="54484-118">Existing applications are customizable, owned by the organization, and can be converted into skills for a Virtual Assistant.</span></span>
- <span data-ttu-id="54484-119">Центральная группа сотрудников может влиять на настройки существующих приложений и предоставлять необходимые инструкции по интеграции существующих приложений в качестве навыков в виртуальном помощнике</span><span class="sxs-lookup"><span data-stu-id="54484-119">The central employee-experiences team is able to influence customizations to existing apps and provide necessary guidance for integrating existing applications as skills in Virtual Assistant experience</span></span>

![Центральная команда поддерживает помощника, а группы бизнес-функций способствуют работе с навыками](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="54484-121">Создание виртуального помощника для Teams</span><span class="sxs-lookup"><span data-stu-id="54484-121">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="54484-122">Корпорация Майкрософт опубликовала шаблон [Visual Studio для](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) создания виртуальных помощников и навыков.</span><span class="sxs-lookup"><span data-stu-id="54484-122">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="54484-123">С помощью Visual Studio вы можете создать виртуальный помощник на основе текстового опыта с поддержкой ограниченных форматирований карточек с действиями.</span><span class="sxs-lookup"><span data-stu-id="54484-123">With the Visual Studio template, you can create a Virtual Assistant, powered by a text-based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="54484-124">Мы усовершенствовали базовый Visual Studio, включив в него возможности платформы Microsoft Teams и отличные возможности приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="54484-124">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="54484-125">Некоторые возможности включают поддержку карточек с богатыми возможностями, модулей задач, командных или групповых чатов и расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="54484-125">A few of the capabilities include support for rich adaptive cards, task modules, teams/group chats and messaging extensions.</span></span> <span data-ttu-id="54484-126">*См. также,* [руководство. Расширение виртуального помощника до Microsoft Teams.](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)</span><span class="sxs-lookup"><span data-stu-id="54484-126">*See also*, [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>

![Высокоуровневая схема решения виртуального помощника](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="54484-128">Добавление адаптивных карточек в виртуальный помощник</span><span class="sxs-lookup"><span data-stu-id="54484-128">Add adaptive cards to your Virtual Assistant</span></span>

<span data-ttu-id="54484-129">Для правильной отправки запросов виртуальный помощник должен определить правильную модель и соответствующие навыки, связанные с ними.</span><span class="sxs-lookup"><span data-stu-id="54484-129">To dispatch requests properly, your Virtual Assistant needs to identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="54484-130">Однако механизм отправки нельзя использовать для действий с карточками, так как модель СДРЕС, связанная с навыками, может не быть обучена работе с текстами действий карточки, так как это фиксированные, предварительно определенные ключевые слова, а не изрекаемые пользователем.</span><span class="sxs-lookup"><span data-stu-id="54484-130">However, the dispatching mechanism cannot be used for card action activities since the LUIS model associated with a skill may not be trained for card action texts since these are fixed, pre-defined keywords, not utterances from a user.</span></span>

<span data-ttu-id="54484-131">Мы устраили эту проблему, встраив сведения о квалификации в полезной нагрузке действия карточки.</span><span class="sxs-lookup"><span data-stu-id="54484-131">We have resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="54484-132">Все навыки должны быть `skillId` встраиты  `value` в поле действий карт.</span><span class="sxs-lookup"><span data-stu-id="54484-132">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="54484-133">Это лучший способ убедиться, что каждое действие карточки содержит соответствующую информацию о квалификации и виртуальный помощник может использовать эту информацию для отправки.</span><span class="sxs-lookup"><span data-stu-id="54484-133">This is the best way to ensure that each card action activity carries the relevant skill information and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="54484-134">Ниже приведен пример данных о действии карточки.</span><span class="sxs-lookup"><span data-stu-id="54484-134">Below is a card action data sample.</span></span> <span data-ttu-id="54484-135">Предоставляя данные в конструкторе, мы гарантируем, что информация о квалификации всегда `skillId` присутствует в действиях карточки.</span><span class="sxs-lookup"><span data-stu-id="54484-135">By providing `skillId` in the constructor we ensure that skill information is always present in card actions.</span></span>

```csharp
    public class CardActionData
    {
        public CardActionData(string skillId)
        {
            this.SkillId = skillId;
        }

        [JsonProperty("skillId")]
        public string SkillId { get; set; }
    }

    ...
    var button = new CardAction
    {
        Type = ActionTypes.MessageBack,
        Title = "Card action button",
        Text = "card action button text",
        Value = new CardActionData(<SkillId>),
    };
```

<span data-ttu-id="54484-136">Далее мы представляем класс в шаблоне виртуального помощника для извлечения из `SkillCardActionData` `skillId` полезных полезных нагрузки действия карточки.</span><span class="sxs-lookup"><span data-stu-id="54484-136">Next, we introduce `SkillCardActionData` class in the Virtual Assistant template to extract `skillId` from the card action payload.</span></span>

```csharp
    // Skill Card action data should contain skillId parameter
    // This class is used to deserialize it and get skillId 
    public class SkillCardActionData
    {
        /// <summary>
        /// Gets the ID of the skil that should handle this card
        /// </summary>
        [JsonProperty("skillId")]
        public string SkillId { get; set; }
    }
```

<span data-ttu-id="54484-137">Ниже приведен фрагмент кода для извлечения из  `skillId` данных действий карточки.</span><span class="sxs-lookup"><span data-stu-id="54484-137">Below is a code snippet to extract  `skillId` from card action data.</span></span> <span data-ttu-id="54484-138">Мы реализовали его как метод расширения в [классе Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)</span><span class="sxs-lookup"><span data-stu-id="54484-138">We implemented it as an  extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>

```csharp
    public static class ActivityExtensions
    {
        // Fetches skillId from CardAction data if present
        public static string GetSkillId(this Activity activity)
        {
            string skillId = string.Empty;

            try
            {
                if (activity.Type.Equals(ActivityTypes.Message) && activity.Value != null)
                {
                    var data = JsonConvert.DeserializeObject<SkillCardActionData>(activity.Value.ToString());
                    skillId = data.SkillId;
                }
                else if (activity.Type.Equals(ActivityTypes.Invoke) && activity.Value != null)
                {
                    var data = JsonConvert.DeserializeObject<SkillCardActionData>(JObject.Parse(activity.Value.ToString()).SelectToken("data").ToString());
                    skillId = data.SkillId;
                }
            }
            catch
            {
                // If not able to retrive skillId, empty skillId should be returned
            }

            return skillId;
        }
    }
```

### <a name="handle-interruptions-gracefully"></a><span data-ttu-id="54484-139">Корректная обработка прерываний</span><span class="sxs-lookup"><span data-stu-id="54484-139">Handle interruptions gracefully</span></span>

<span data-ttu-id="54484-140">Виртуальный помощник может обрабатывать прерывания в тех случаях, когда пользователь пытается вызвать навыков, когда в настоящее время активен другой навыков.</span><span class="sxs-lookup"><span data-stu-id="54484-140">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="54484-141">Мы ввели и, на основе `TeamsSkillDialog` `TeamsSwitchSkillDialog` SkillDialog и [SwitchS skillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)в [Bot](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) Framework, чтобы позволить пользователям переключаться навыков из действий карт.</span><span class="sxs-lookup"><span data-stu-id="54484-141">we have introduced `TeamsSkillDialog` and `TeamsSwitchSkillDialog`, based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), to enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="54484-142">Для обработки этого запроса виртуальный помощник запрашивает у пользователя подтверждение для переключения навыков.</span><span class="sxs-lookup"><span data-stu-id="54484-142">To handle this request the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![Запрос подтверждения при переходе на новый уровень квалификации](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a><span data-ttu-id="54484-144">Обработка запросов модулей задач</span><span class="sxs-lookup"><span data-stu-id="54484-144">Handling task module requests</span></span>

<span data-ttu-id="54484-145">Чтобы добавить возможности модуля задач в виртуальный помощник, в обработок действий виртуального помощника включены два дополнительных метода: `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="54484-145">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="54484-146">Эти методы прослушивают действия, связанные с модулем задачи, из виртуального помощника, определяют навыки, связанные с запросом, и переназначили запрос на указанный уровень квалификации.</span><span class="sxs-lookup"><span data-stu-id="54484-146">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="54484-147">Переадтранслировать запросы можно с помощью метода [SkillHttpClient.](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable) `PostActivityAsync`</span><span class="sxs-lookup"><span data-stu-id="54484-147">Request forwarding is done via the  [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable), `PostActivityAsync` method.</span></span> <span data-ttu-id="54484-148">Он возвращает ответ, который будет `InvokeResponse` разобрано и преобразовано в `TaskModuleResponse` .</span><span class="sxs-lookup"><span data-stu-id="54484-148">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>

```csharp
    public static TaskModuleResponse GetTaskModuleRespose(this InvokeResponse invokeResponse)
    {
        if (invokeResponse.Body != null)
        {
            return new TaskModuleResponse()
            {
                Task = GetTask(invokeResponse.Body),
            };
        }

        return null;
    }

    private static TaskModuleResponseBase GetTask(object invokeResponseBody)
        {
            JObject resposeBody = (JObject)JToken.FromObject(invokeResponseBody);
            var task = resposeBody.GetValue("task");
            var taskType = task.SelectToken("type").ToString();

            return taskType switch
            {
                "continue" => new TaskModuleContinueResponse()
                {
                    Type = taskType,
                    Value = task.SelectToken("value").ToObject<TaskModuleTaskInfo>(),
                },
                "message" => new TaskModuleMessageResponse()
                {
                    Type = taskType,
                    Value = task.SelectToken("value").ToString(),
                },
                _ => null,
            };
        }
```

<span data-ttu-id="54484-149">Аналогичный подход следует для отправки действий карт и ответов модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="54484-149">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="54484-150">Данные о действиях и извлечении и отправке модуля задачи будут обновлены, чтобы включить `skillId` их.</span><span class="sxs-lookup"><span data-stu-id="54484-150">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="54484-151">Метод расширения действия извлекается из полезных данных, что дает подробные сведения о `GetSkillId` `skillId` навыков, которые необходимо вызвать.</span><span class="sxs-lookup"><span data-stu-id="54484-151">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="54484-152">Ниже приведен фрагмент кода для методов `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` и методов.</span><span class="sxs-lookup"><span data-stu-id="54484-152">Below is a code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods.</span></span>

```csharp
    // Invoked when a "task/fetch" event is received to invoke task module.
    protected override async Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
    {
        try
        {
            string skillId = (turnContext.Activity as Activity).GetSkillId();
            var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;

            // Forward request to correct skill
            var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken);

            return invokeResponse.GetTaskModuleRespose();
        }
        catch (Exception exception)
        {
            await turnContext.SendActivityAsync(_templateEngine.GenerateActivityForLocale("ErrorMessage"));
            _telemetryClient.TrackException(exception);

            return null;
        }
    }

    // Invoked when a 'task/submit' invoke activity is received for task module submit actions.
    protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
    {
        try
        {
            string skillId = (turnContext.Activity as Activity).GetSkillId();
            var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;

            // Forward request to correct skill
            var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

            return invokeResponse.GetTaskModuleRespose();
        }
        catch (Exception exception)
        {
            await turnContext.SendActivityAsync(_templateEngine.GenerateActivityForLocale("ErrorMessage"));
            _telemetryClient.TrackException(exception);

            return null;
        }
    }
```

<span data-ttu-id="54484-153">Кроме того, все домены навыков должны быть включены в раздел в файле манифеста виртуального помощника, чтобы модули задач, вызывались посредством правильной отрисовки `validDomains` навыков.</span><span class="sxs-lookup"><span data-stu-id="54484-153">Additionally, all skill domains must be included in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked via a skill render properly.</span></span>

### <a name="handling-collaborative-app-scopes"></a><span data-ttu-id="54484-154">Обработка областей совместной работы приложений</span><span class="sxs-lookup"><span data-stu-id="54484-154">Handling collaborative app scopes</span></span>

<span data-ttu-id="54484-155">Приложения Teams могут существовать в различных сферах, включая 1:1 чат, групповой чат и каналы.</span><span class="sxs-lookup"><span data-stu-id="54484-155">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="54484-156">Основной шаблон виртуального помощника предназначен для чатов 1:1.</span><span class="sxs-lookup"><span data-stu-id="54484-156">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="54484-157">В рамках пользовательского интерфейса виртуальный помощник запросит имя и поддерживает состояние пользователя.</span><span class="sxs-lookup"><span data-stu-id="54484-157">As part of the onboarding experience Virtual Assistant  prompts users for name and maintains user state.</span></span> <span data-ttu-id="54484-158">Так как этот подход не подходит для областей группового чата или канала, он был удален.</span><span class="sxs-lookup"><span data-stu-id="54484-158">Since that onboarding experience is not suited for group chat/channel scopes it has been removed.</span></span>

<span data-ttu-id="54484-159">Навыки должны обрабатывать действия в различных сферах (1:1 чат, групповой чат и беседа в канале).</span><span class="sxs-lookup"><span data-stu-id="54484-159">Skills should handle activities in multiple scopes (1:1 chat, group chat, and channel conversation).</span></span> <span data-ttu-id="54484-160">Если какие-либо из этих областей не поддерживаются, навыки должны отвечать соответствующим сообщением.</span><span class="sxs-lookup"><span data-stu-id="54484-160">If any of these scopes are not supported, skills should respond with an appropriate message.</span></span>

<span data-ttu-id="54484-161">В ядро виртуального помощника добавлены следующие функции обработки:</span><span class="sxs-lookup"><span data-stu-id="54484-161">The following  processing functions have been added to Virtual Assistant core:</span></span>

- <span data-ttu-id="54484-162">Виртуальный помощник можно вызвать без текстовых сообщений из группового чата или канала.</span><span class="sxs-lookup"><span data-stu-id="54484-162">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
- <span data-ttu-id="54484-163">Перед отправкой сообщения в модуль отправки удаляются @mention бота.</span><span class="sxs-lookup"><span data-stu-id="54484-163">Articulations are cleaned (i.e.,  remove the necessary @mention of the bot) before sending the message to the dispatch module.</span></span>

```csharp
    if (innerDc.Context.Activity.Conversation?.IsGroup == true)
    {
        // Remove bot atmentions for teams/groupchat scope
        innerDc.Context.Activity.RemoveRecipientMention();

        // If bot is invoked without any text, reply with FirstPromptMessage
        if (string.IsNullOrWhiteSpace(innerDc.Context.Activity.Text))
        {
            await innerDc.Context.SendActivityAsync(_templateEngine.GenerateActivityForLocale("FirstPromptMessage"));
            return EndOfTurn;
        }
    }
```

### <a name="handling-messaging-extensions"></a><span data-ttu-id="54484-164">Обработка расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="54484-164">Handling messaging extensions</span></span>

<span data-ttu-id="54484-165">Команды для расширения обмена сообщениями объявляются в файле манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="54484-165">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="54484-166">Пользовательский интерфейс расширения обмена сообщениями, на питание от этих команд.</span><span class="sxs-lookup"><span data-stu-id="54484-166">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="54484-167">Чтобы виртуальный помощник встроил команду расширения обмена сообщениями (как присоединенный навык), манифест виртуального помощника должен содержать эти команды.</span><span class="sxs-lookup"><span data-stu-id="54484-167">For a Virtual Assistant to power a messaging extension command (as an attached skill), a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="54484-168">Команды из манифеста отдельного навыков также следует добавить в манифест виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="54484-168">The commands from an individual skill's manifest should be added to the Virtual Assistant's manifest as well.</span></span> <span data-ttu-id="54484-169">Этот ИД команды предоставляет сведения о связанном с ним навыков посредством с помощью сепаратора ( `:` ).</span><span class="sxs-lookup"><span data-stu-id="54484-169">The command ID provides information about an associated skill by appending the skill's app ID via a separator (`:`).</span></span>

<span data-ttu-id="54484-170">Ниже приведен фрагмент из файла манифеста навыков.</span><span class="sxs-lookup"><span data-stu-id="54484-170">Below is a snippet from a skill's manifest file.</span></span>

```json
 "composeExtensions": [
    {
        "botId": "<Skil_App_Id>",
        "commands": [
            {
                "id": "searchQuery",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
    ....
```

<span data-ttu-id="54484-171">Ниже приведен соответствующий фрагмент кода файла манифеста виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="54484-171">And, below is the corresponding Virtual Assistant manifest file code snippet.</span></span>

```json
 "composeExtensions": [
    {
        "botId": "<VA_App_Id>",
        "commands": [
            {
                "id": "searchQuery:<skill_id>",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
    ....
```

<span data-ttu-id="54484-172">После того как команды вызываются пользователем, виртуальный помощник может определить соответствующий навык, выполнив разбор ИД команды, обновив действие, удалив дополнительный суффикс ( ) из ИД команды и перенаполнив его на соответствующий `:<skill_id>` уровень.</span><span class="sxs-lookup"><span data-stu-id="54484-172">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix (`:<skill_id>`) from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="54484-173">Код для навыков не должен обрабатывать дополнительный суффикс, поэтому конфликтов между кодами команд между навыками не требуется.</span><span class="sxs-lookup"><span data-stu-id="54484-173">The code for a skill doesn't need to handle the extra suffix, thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="54484-174">При таком подходе виртуальный помощник может использовать все команды поиска и действий навыки во всех контекстах ("compose", "commandBox" и "message").</span><span class="sxs-lookup"><span data-stu-id="54484-174">With this approach, all the search and action commands of a skill within all contexts ("compose", "commandBox" and "message") can be powered by a Virtual Assistant.</span></span>

```csharp
    const string MessagingExtensionCommandIdSeparator = ":";

    // Invoked when a 'composeExtension/submitAction' invoke activity is received for a messaging extension action command
    protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
    {
        return await ForwardMessagingExtensionActionCommandActivityToSkill(turnContext, action, cancellationToken);
    }

    // Forwards invoke activity to right skill for messaging extension action commands.
    private async Task<MessagingExtensionActionResponse> ForwardMessagingExtensionActionCommandActivityToSkill(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
    {
        var skillId = ExtractSkillIdFromMessagingExtensionActionCommand(turnContext, action);
        var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;
        var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

        return invokeResponse.GetMessagingExtensionActionResponse();
    }

    // Extracts skill Id from messaging extension command and updates activity value
    private string ExtractSkillIdFromMessagingExtensionActionCommand(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action)
    {
        var commandArray = action.CommandId.Split(MessagingExtensionCommandIdSeparator);
        var skillId = commandArray.Last();

        // Update activity value by removing skill id before forwarding to the skill.
        var activityValue = JsonConvert.DeserializeObject<MessagingExtensionAction>(turnContext.Activity.Value.ToString());
        activityValue.CommandId = string.Join(MessagingExtensionCommandIdSeparator, commandArray, 0 commandArray.Length - 1);
        turnContext.Activity.Value = activityValue;

        return skillId;
    }
```

<span data-ttu-id="54484-175">Некоторые действия расширения обмена сообщениями не включают в себя ИД команды.</span><span class="sxs-lookup"><span data-stu-id="54484-175">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="54484-176">Например, `composeExtension/selectItem` содержит только значение действия касания вызова.</span><span class="sxs-lookup"><span data-stu-id="54484-176">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="54484-177">Чтобы определить связанное навыков, `skillId`  присоединяется к каждой карточке элемента при формировании ответа для `OnTeamsMessagingExtensionQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="54484-177">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="54484-178">(Это аналогично способу добавления адаптивных [карточек в виртуальный помощник.](#add-adaptive-cards-to-your-virtual-assistant)</span><span class="sxs-lookup"><span data-stu-id="54484-178">(This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

```csharp
    // Invoked when a 'composeExtension/selectItem' invoke activity is received for compose extension query command.
    protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionSelectItemAsync(ITurnContext<IInvokeActivity> turnContext, JObject query, CancellationToken cancellationToken)
    {
        var data = JsonConvert.DeserializeObject<SkillCardActionData>(query.ToString());
        var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == data.SkillId).First().Value;
        var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

        return invokeResponse.GetMessagingExtensionResponse();
    }
```

---

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a><span data-ttu-id="54484-179">Пример. Преобразование шаблона приложения "Книга в комнату" в навыки виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="54484-179">Example: Convert the Book-a-room app template to a Virtual Assistant skill</span></span>

<span data-ttu-id="54484-180">[Book-a-room](app-templates.md#book-a-room) — это бот [Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям быстро находить и резервировать комнату для собраний на 30 (по умолчанию), 60 или 90 минут, начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="54484-180">[Book-a-room](app-templates.md#book-a-room) is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="54484-181">Бот book-a-room имеет область личных или 1:1 бесед.</span><span class="sxs-lookup"><span data-stu-id="54484-181">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

![Виртуальный помощник с навыками "книги комнаты"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="54484-183">Ниже представлены изменения изменений, внесенные для преобразования его в навыки, которые можно прикрепить к виртуальному помощнику.</span><span class="sxs-lookup"><span data-stu-id="54484-183">Followings are the delta changes introduced to convert it to a skill which can be attached to a Virtual Assistant.</span></span> <span data-ttu-id="54484-184">Аналогичные рекомендации можно использовать для преобразования любого существующего бота v4 в навыки.</span><span class="sxs-lookup"><span data-stu-id="54484-184">Similar guidelines can be followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="54484-185">Манифест навыков</span><span class="sxs-lookup"><span data-stu-id="54484-185">Skill manifest</span></span>

<span data-ttu-id="54484-186">Манифест навыков — это JSON-файл, который предоставляет конечную точку обмена сообщениями, ид, имя и другие релевантные метаданные навыки (этот манифест отличается от манифеста, используемого для загрузки неокрепленного приложения в Microsoft Teams). Виртуальный помощник требует путь к этому файлу в качестве входных данных для вложенного навыков.</span><span class="sxs-lookup"><span data-stu-id="54484-186">A skill manifest is a JSON file that exposes a skill's messaging endpoint, id, name, and other relevant metadata (this manifest is different than the manifest used for sideloading an app in Microsoft Teams) A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="54484-187">Мы добавили следующий манифест в папку wwwroot бота.</span><span class="sxs-lookup"><span data-stu-id="54484-187">We have added the following manifest to the bot's wwwroot folder.</span></span>

```bash
botskills connect --remoteManifest "<url to skill's manifest>" ..
```

```json
{
  "$schema": "https://schemas.botframework.com/schemas/skills/skill-manifest-2.1.preview-0.json",
  "$id": "microsoft_teams_apps_bookaroom",
  "name": "microsoft-teams-apps-bookaroom",
  "description": "microsoft-teams-apps-bookaroom description",
  "publisherName": "Your Company",
  "version": "1.1",
  "iconUrl": "<icon url>",
  "copyright": "Copyright (c) Microsoft Corporation. All rights reserved.",
  "license": "",
  "privacyUrl": "<privacy url>",
  "endpoints": [
    {
      "name": "production",
      "protocol": "BotFrameworkV3",
      "description": "Production endpoint for the skill",
      "endpointUrl": "<endpoint url>",
      "msAppId": "skill app id"
    }
  ],
  "dispatchModels": {
    "languages": {
      "en-us": [
        {
          "id": "microsoft-teams-apps-bookaroom-en",
          "name": "microsoft-teams-apps-bookaroom LU (English)",
          "contentType": "application/lu",
          "url": "file://book-a-meeting.lu",
          "description": "English language model for the skill"
        }
      ]
    }
  },
  "activities": {
    "message": {
      "type": "message",
      "description": "Receives the users utterance and attempts to resolve it using the skill's LU models"
    }
  }
}
```

### <a name="luis-integration"></a><span data-ttu-id="54484-188">Интеграция с ИТ-специалистом</span><span class="sxs-lookup"><span data-stu-id="54484-188">LUIS Integration</span></span>

<span data-ttu-id="54484-189">Модель диспетчеризации виртуального помощника построена на основе моделей СЕТ С присоединенными навыками.</span><span class="sxs-lookup"><span data-stu-id="54484-189">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="54484-190">Модель диспетчера определяет назначение для каждого текстового действия и находит навыки, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="54484-190">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="54484-191">Для работы с виртуальным помощником требуется модель СЕТ по навыкам (в формате) в качестве входных данных при присоединении `.lu` навыков.</span><span class="sxs-lookup"><span data-stu-id="54484-191">Virtual Assistant requires skill's LUIS model (in `.lu` format) as an input while attaching a skill.</span></span> <span data-ttu-id="54484-192">МЕТОД JSON в ФОРМАТ МОЖНО преобразовать с `.lu` помощью средства botframework-cli.</span><span class="sxs-lookup"><span data-stu-id="54484-192">LUIS json can be converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="54484-193">Бот book-a-room имеет две основные команды для пользователей:</span><span class="sxs-lookup"><span data-stu-id="54484-193">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="54484-194">Мы создали модель СЕТ, которая понимает эти две команды.</span><span class="sxs-lookup"><span data-stu-id="54484-194">We have built a LUIS model understanding these two commands.</span></span> <span data-ttu-id="54484-195">Соответствующие секреты должны быть заполнены `cognitivemodels.json` в .</span><span class="sxs-lookup"><span data-stu-id="54484-195">Corresponding secrets need to be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="54484-196">Здесь можно найти соответствующий [](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) JSON-файл СДРЕС, и так выглядит `.lu` соответствующий файл.</span><span class="sxs-lookup"><span data-stu-id="54484-196">The corresponding LUIS JSON file can be found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) and this is how the corresponding `.lu` file looks like.</span></span>

```
> ! Automatically generated by [LUDown CLI](https://github.com/Microsoft/botbuilder-tools/tree/master/Ludown), Tue Mar 31 2020 17:30:32 GMT+0530 (India Standard Time)

> ! Source LUIS JSON file: book-a-meeting.json

> ! Source QnA TSV file: Not Specified

> ! Source QnA Alterations file: Not Specified


> # Intent definitions

## BOOK ROOM
- book a room
- book room
- please book a room
- reserve a room
- i want to book a room
- i want to book a room please
- get me a room please
- get me a room


## MANAGE FAVORITES
- manage favorites
- manage favorite
- please manage my favorite rooms
- manage my favorite rooms please
- manage my favorite rooms
- i want to manage my favorite rooms

## None


> # Entity definitions


> # PREBUILT Entity definitions


> # Phrase list definitions


> # List entities

> # RegEx entities
```

<span data-ttu-id="54484-197">При таком подходе любые проблемы с командами, связанные с виртуальным помощником или связанные с ним, могут быть определены как команды, связанные с ботом `book room` book-a-room, и переназначаются на этот `manage favorites` опыт.</span><span class="sxs-lookup"><span data-stu-id="54484-197">With this approach, any command issues by a user to Virtual Assistant related to `book room` or `manage favorites` can be identified as a command associated with Book-a-room bot and is forwarded to this skill.</span></span>
<span data-ttu-id="54484-198">С другой стороны, бот book-a-room должен использовать модель СЕТ, чтобы понять эти команды, если они не введите как есть (например: `I want to manage my favorite rooms` ).</span><span class="sxs-lookup"><span data-stu-id="54484-198">On the other hand, Book-a-room room bot needs to use LUIS model to understand these commands if they are not typed as is (for example: `I want to manage my favorite rooms`).</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="54484-199">Поддержка нескольких языков</span><span class="sxs-lookup"><span data-stu-id="54484-199">Multi-Language support</span></span>

<span data-ttu-id="54484-200">В этом примере мы создали модель ТОЛЬКО с языком в английском языке.</span><span class="sxs-lookup"><span data-stu-id="54484-200">For this example, we have only created a LUIS model with English culture.</span></span> <span data-ttu-id="54484-201">Вы можете создать модели СЕТ, соответствующие другим языкам, и добавить запись в `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="54484-201">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

```json
{
  "defaultLocale": "en-us",
  "languageModels": {
    "en-us": {
      "luisAppId": "",
      "luisApiKey": "",
      "luisApiHost": ""
    },
    "<your_language_culture>": {
      "luisAppId": "",
      "luisApiKey": "",
      "luisApiHost": ""
    }
  }
}
```

<span data-ttu-id="54484-202">Параллельно добавьте соответствующий `.lu` файл в путь к папке.</span><span class="sxs-lookup"><span data-stu-id="54484-202">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="54484-203">Структура папок должна быть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="54484-203">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="54484-204">Чтобы изменить параметр, обновим команду botskills `languages` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="54484-204">Update botskills command as follows to modify `languages` parameter:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="54484-205">Виртуальный помощник использует `SetLocaleMiddleware` для определения текущего региональных 100-х и вызова соответствующей модели диспетчера.</span><span class="sxs-lookup"><span data-stu-id="54484-205">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="54484-206">(Действие bot framework имеет поле locale, которое используется этим ПО по середине.) Мы рекомендуем использовать то же самое и для вашего навыков.</span><span class="sxs-lookup"><span data-stu-id="54484-206">(Bot framework activity has locale field which is used by this middleware.) We recommend to use the same for your skill as well.</span></span> <span data-ttu-id="54484-207">Бот book-a-room не использует это по среднему по и вместо этого получает локали из объекта [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)действия bot framework.</span><span class="sxs-lookup"><span data-stu-id="54484-207">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="54484-208">Проверка утверждений</span><span class="sxs-lookup"><span data-stu-id="54484-208">Claim validation</span></span>

<span data-ttu-id="54484-209">Мы добавили [claimsValidator,](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) чтобы ограничить звоняющих навыками.</span><span class="sxs-lookup"><span data-stu-id="54484-209">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="54484-210">Чтобы виртуальный помощник вызывал этот навык, заполняйте массив с помощью этого конкретного ИД `AllowedCallers` `appsettings` приложения виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="54484-210">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="54484-211">Разрешенный массив вызывающих может ограничить доступ потребителей навыков к навыкам.</span><span class="sxs-lookup"><span data-stu-id="54484-211">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="54484-212">Добавьте одну запись `*` в этот массив, чтобы принимать вызовы от любого потребителя навыков.</span><span class="sxs-lookup"><span data-stu-id="54484-212">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```
<span data-ttu-id="54484-213">Подробную документацию по добавлению проверки утверждений в квалификацию можно найти [здесь.](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)</span><span class="sxs-lookup"><span data-stu-id="54484-213">Detailed documentation for adding claims validation to a skill can be found [here](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator).</span></span>

### <a name="card-refresh-limitation"></a><span data-ttu-id="54484-214">Ограничение на обновление карты</span><span class="sxs-lookup"><span data-stu-id="54484-214">Card refresh limitation</span></span>

<span data-ttu-id="54484-215">Обновление действия (обновление карты) еще не поддерживается с помощью виртуального помощника[(проблема с github).](https://github.com/microsoft/botbuilder-dotnet/issues/3686)</span><span class="sxs-lookup"><span data-stu-id="54484-215">Updating activity (card refresh) is not supported yet via Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="54484-216">Таким образом, мы заменили все вызовы обновления карты () на `UpdateActivityAsync` отправку новых вызовов карт( `SendActivityAsync` ).</span><span class="sxs-lookup"><span data-stu-id="54484-216">Hence, we have replaced all card refresh calls (`UpdateActivityAsync`) with posting new card calls(`SendActivityAsync`).</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="54484-217">Действия карточки и потоки модуля задач</span><span class="sxs-lookup"><span data-stu-id="54484-217">Card actions and task module flows</span></span>

<span data-ttu-id="54484-218">Чтобы перенаадтрить действия карточки или действия модуля задачи связанному с ним навыкам, необходимо встраить `skillId` в него навыки.</span><span class="sxs-lookup"><span data-stu-id="54484-218">To forward card action or task module activities to an associated skill, the skill needs to embed `skillId` to it.</span></span>
<span data-ttu-id="54484-219">Действие бота book-a-room, извлечение и отправка полезной нагрузки модуля задачи изменены в качестве `skillId` параметра.</span><span class="sxs-lookup"><span data-stu-id="54484-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="54484-220">Дополнительные сведения можно [получить в этом](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) разделе из этой документации.</span><span class="sxs-lookup"><span data-stu-id="54484-220">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="54484-221">Обработка действий из области группового чата или канала</span><span class="sxs-lookup"><span data-stu-id="54484-221">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="54484-222">Бот book-a-room предназначен только для личных чатов (личных/1:1).</span><span class="sxs-lookup"><span data-stu-id="54484-222">Book-a-room bot is designed for private chats (personal/1:1 scope) only.</span></span> <span data-ttu-id="54484-223">Так как мы настроили виртуальный помощник для поддержки группового чата и областей каналов, виртуальный помощник может быть вызван из этих областей, поэтому бот book-a-room может получить действия для того же самого.</span><span class="sxs-lookup"><span data-stu-id="54484-223">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant might be invoked from these scopes and thus, Book-a-room bot might get activities for the same.</span></span> <span data-ttu-id="54484-224">Поэтому бот book-a-room настраивается для обработки этих действий.</span><span class="sxs-lookup"><span data-stu-id="54484-224">Hence Book-a-room bot is customized to handle those activities.</span></span> <span data-ttu-id="54484-225">Проверка была установлена в методах обработки действий бота `OnMessageActivityAsync` book-a-room.</span><span class="sxs-lookup"><span data-stu-id="54484-225">The check has been put in `OnMessageActivityAsync` methods of Book-a-room bot's activity handler.</span></span>

```csharp
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        // Check if activities are from groupchat/ teams scope. This might happen when the bot is consumed by Virtual Assistant.
        if (turnContext.Activity.Conversation.IsGroup == true)
        {
            await ShowNotSupportedInGroupChatCardAsync(turnContext).ConfigureAwait(false);
        }
        else
        {
            ...
        }
    }
```

<span data-ttu-id="54484-226">Вы также можете использовать существующие навыки из [репозитория решений Bot Framework](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) или создать новый навыки с нуля.</span><span class="sxs-lookup"><span data-stu-id="54484-226">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="54484-227">Учебники по последующим вопросам можно найти [здесь.](https://microsoft.github.io/botframework-solutions/overview/skills/)</span><span class="sxs-lookup"><span data-stu-id="54484-227">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="54484-228">Обратитесь к [документации по](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   виртуальному помощнику и архитектуре навыков.</span><span class="sxs-lookup"><span data-stu-id="54484-228">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   for Virtual Assistant and skills architecture.</span></span>

## <a name="sample-code-to-get-started"></a><span data-ttu-id="54484-229">Пример кода для начала работы</span><span class="sxs-lookup"><span data-stu-id="54484-229">Sample code to get started</span></span>

- [<span data-ttu-id="54484-230">Обновленный шаблон Visual Studio</span><span class="sxs-lookup"><span data-stu-id="54484-230">Updated visual studio template</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [<span data-ttu-id="54484-231">Код навыков бота "Книга в комнате"</span><span class="sxs-lookup"><span data-stu-id="54484-231">Book-a-room bot skill code</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a><span data-ttu-id="54484-232">Известные ограничения для виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="54484-232">Virtual Assistant known limitations</span></span>

- <span data-ttu-id="54484-233">**EndOfConversation**.</span><span class="sxs-lookup"><span data-stu-id="54484-233">**EndOfConversation**.</span></span> <span data-ttu-id="54484-234">Навыки должны отправлять действия `endOfConversation` по завершению беседы.</span><span class="sxs-lookup"><span data-stu-id="54484-234">A skill should send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="54484-235">На основе этого действия виртуальный помощник завершает контекст определенным навыков и возвращается в контекст (корневой) виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="54484-235">basis this activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's (root) context.</span></span> <span data-ttu-id="54484-236">Для бота book-a-room нет четкого состояния, в котором можно бы закончить беседу.</span><span class="sxs-lookup"><span data-stu-id="54484-236">For Book-a-room bot, there is no clear state where conversation can be ended.</span></span> <span data-ttu-id="54484-237">Поэтому мы не отправляли данные из бота book-a-room, и когда пользователь хочет вернуться в корневой контекст, он может просто сделать это `endOfConversation` с помощью `start over` команды.</span><span class="sxs-lookup"><span data-stu-id="54484-237">Hence we have not sent `endOfConversation` from Book-a-room bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>
- <span data-ttu-id="54484-238">**Обновление карточки.**</span><span class="sxs-lookup"><span data-stu-id="54484-238">**Card refresh**.</span></span> <span data-ttu-id="54484-239">Обновление карточки пока не поддерживается с помощью виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="54484-239">Card refreshes is not yet supported through Virtual Assistant.</span></span>
- <span data-ttu-id="54484-240">**Расширения обмена сообщениями.:**</span><span class="sxs-lookup"><span data-stu-id="54484-240">**Messaging extensions**.:</span></span>
  - <span data-ttu-id="54484-241">В настоящее время виртуальный помощник может поддерживать не более десяти команд для расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="54484-241">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  - <span data-ttu-id="54484-242">Настройка расширений обмена сообщениями не зависит от отдельных команд, а для всего расширения.</span><span class="sxs-lookup"><span data-stu-id="54484-242">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="54484-243">Это ограничивает конфигурацию для каждого отдельного навыков с помощью виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="54484-243">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  - <span data-ttu-id="54484-244">ИД команд расширений обмена сообщениями имеют максимальную длину [64](../resources/schema/manifest-schema.md#composeextensions) символа, а для встраиванию сведений о навыках будет использоваться 37 символов.</span><span class="sxs-lookup"><span data-stu-id="54484-244">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters will be used for embedding skill information.</span></span> <span data-ttu-id="54484-245">Таким образом, обновленные ограничения для ИД команды ограничены 27 символами.</span><span class="sxs-lookup"><span data-stu-id="54484-245">Thus, updated constraints for command ID are limited to 27 characters.</span></span>
>
>
