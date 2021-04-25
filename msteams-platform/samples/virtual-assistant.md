---
title: Виртуальный помощник для Microsoft Teams
description: Создание виртуального помощника бота и навыков для использования в Microsoft Teams
ms.topic: how-to
keywords: команды виртуальных помощников-ботов
ms.openlocfilehash: 52591435c5a7e1c65a8f86a7c41fe4a3a4fa5c83
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2021
ms.locfileid: "51996025"
---
# <a name="virtual-assistant-for-microsoft-teams"></a><span data-ttu-id="01c45-104">Виртуальный помощник для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="01c45-104">Virtual Assistant for Microsoft Teams</span></span>

<span data-ttu-id="01c45-105">Виртуальный помощник — это шаблон Microsoft с открытым исходным кодом, который позволяет создавать надежное решение для беседы, сохраняя полный контроль над пользовательским опытом, организационным брендингом и необходимыми данными.</span><span class="sxs-lookup"><span data-stu-id="01c45-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="01c45-106">Основной [](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) шаблон виртуального помощника — это базовый строительный блок, который объединяет технологии Майкрософт, необходимые для создания виртуального помощника, в том числе [SDK](https://github.com/microsoft/botframework-sdk)Bot Framework, [Language Understanding (LUIS),](https://www.luis.ai/) [QnA Maker,](https://www.qnamaker.ai/)а также основные возможности, включая регистрацию навыков, связанные учетные записи, основные беседы, чтобы предложить конечным пользователям широкий спектр бесшовных взаимодействий и возможностей.</span><span class="sxs-lookup"><span data-stu-id="01c45-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), as well as essential capabilities including  skills registration, linked accounts, basic conversational intent to offer end users a range of seamless interactions and experiences.</span></span> <span data-ttu-id="01c45-107">Кроме того, возможности шаблона включают в себя богатые примеры многоиспользоваемых разговорных [навыков.](https://microsoft.github.io/botframework-solutions/overview/skills)</span><span class="sxs-lookup"><span data-stu-id="01c45-107">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="01c45-108">Отдельные навыки можно интегрировать в решение Virtual Assistant, чтобы включить несколько сценариев.</span><span class="sxs-lookup"><span data-stu-id="01c45-108">Individual skills can be integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="01c45-109">С помощью SDK Bot Framework навыки представлены в форме исходных кодов, что позволяет настраивать и расширять по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="01c45-109">Using the Bot Framework SDK, Skills are presented in source code form enabling you to customize and extend as required.</span></span> <span data-ttu-id="01c45-110">Узнайте, [что такое навык Bot Framework](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="01c45-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span>

![Схема обзора виртуального помощника](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="01c45-112">Действия текстовых сообщений перенаправлются в связанные навыки с помощью виртуального помощника с помощью [модели отправки.](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="01c45-112">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="01c45-113">Соображения реализации</span><span class="sxs-lookup"><span data-stu-id="01c45-113">Implementation considerations</span></span>

<span data-ttu-id="01c45-114">Решение о добавлении виртуального помощника может включать множество детерминантов и отличаться для каждой организации.</span><span class="sxs-lookup"><span data-stu-id="01c45-114">The decision to add a Virtual Assistant can include many determinants and differ for each organization.</span></span> <span data-ttu-id="01c45-115">Вот факторы, которые поддерживают реализацию виртуального помощника для организации:</span><span class="sxs-lookup"><span data-stu-id="01c45-115">Here are the factors that support implementing a Virtual Assistant for your organization:</span></span>

- <span data-ttu-id="01c45-116">Центральная группа управляет всеми возможностями сотрудников и может создавать виртуальный помощник и управлять обновлениями для основного опыта, включая добавление новых навыков.</span><span class="sxs-lookup"><span data-stu-id="01c45-116">A central team manages all employee experiences and has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
- <span data-ttu-id="01c45-117">Существует несколько приложений для бизнес-функций и/или ожидается, что их число будет расти в будущем.</span><span class="sxs-lookup"><span data-stu-id="01c45-117">Multiple applications exist across business functions and/or the number is expected to grow in the future.</span></span>
- <span data-ttu-id="01c45-118">Существующие приложения настраиваются, принадлежат организации и могут быть преобразованы в навыки для виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="01c45-118">Existing applications are customizable, owned by the organization, and can be converted into skills for a Virtual Assistant.</span></span>
- <span data-ttu-id="01c45-119">Центральная команда сотрудников может влиять на настройки существующих приложений и предоставлять необходимые рекомендации по интеграции существующих приложений в качестве навыков в виртуальном помощнике.</span><span class="sxs-lookup"><span data-stu-id="01c45-119">The central employee-experiences team is able to influence customizations to existing apps and provide necessary guidance for integrating existing applications as skills in Virtual Assistant experience</span></span>

![Центральная команда поддерживает помощника, а группы бизнес-функций способствуют навыкам](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="01c45-121">Создание виртуального помощника, сфокусированного на командах</span><span class="sxs-lookup"><span data-stu-id="01c45-121">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="01c45-122">Корпорация Майкрософт опубликовала шаблон [Visual Studio для](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) создания виртуальных помощников и навыков.</span><span class="sxs-lookup"><span data-stu-id="01c45-122">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="01c45-123">С помощью Visual Studio шаблона можно создать виртуальный помощник, основанный на текстовом опыте с поддержкой ограниченных богатых карт с действиями.</span><span class="sxs-lookup"><span data-stu-id="01c45-123">With the Visual Studio template, you can create a Virtual Assistant, powered by a text-based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="01c45-124">Мы усовершенствовали базовый шаблон Visual Studio, чтобы включить возможности платформы Microsoft Teams и расширить возможности приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="01c45-124">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="01c45-125">Некоторые возможности включают поддержку богатых адаптивных карт, модулей задач, командных и групповых чатов и расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="01c45-125">A few of the capabilities include support for rich adaptive cards, task modules, teams/group chats and messaging extensions.</span></span> <span data-ttu-id="01c45-126">*См. также*, [Учебник: Расширение виртуального помощника в Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span><span class="sxs-lookup"><span data-stu-id="01c45-126">*See also*, [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>

![Схема решения виртуального помощника на высоком уровне](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="01c45-128">Добавление адаптивных карт в виртуальный помощник</span><span class="sxs-lookup"><span data-stu-id="01c45-128">Add adaptive cards to your Virtual Assistant</span></span>

<span data-ttu-id="01c45-129">Чтобы правильно отправлять запросы, виртуальному помощнику необходимо определить правильную модель LUIS и соответствующие навыки, связанные с ней.</span><span class="sxs-lookup"><span data-stu-id="01c45-129">To dispatch requests properly, your Virtual Assistant needs to identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="01c45-130">Однако механизм отправки не может использоваться для действий с картами, так как модель LUIS, связанная с навыком, не может быть обучена текстам действий карт, так как это фиксированные, заранее определенные ключевые слова, а не высказывания пользователя.</span><span class="sxs-lookup"><span data-stu-id="01c45-130">However, the dispatching mechanism cannot be used for card action activities since the LUIS model associated with a skill may not be trained for card action texts since these are fixed, pre-defined keywords, not utterances from a user.</span></span>

<span data-ttu-id="01c45-131">Мы решили это, встраив сведения о навыках в полезной нагрузке действия карты.</span><span class="sxs-lookup"><span data-stu-id="01c45-131">We have resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="01c45-132">Каждый навык должен `skillId` встраить  `value` в область действий карт.</span><span class="sxs-lookup"><span data-stu-id="01c45-132">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="01c45-133">Это лучший способ убедиться, что каждое действие карты несет соответствующие сведения о навыках и виртуальный помощник может использовать эти сведения для отправки.</span><span class="sxs-lookup"><span data-stu-id="01c45-133">This is the best way to ensure that each card action activity carries the relevant skill information and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="01c45-134">Ниже приведен пример данных действий карты.</span><span class="sxs-lookup"><span data-stu-id="01c45-134">Below is a card action data sample.</span></span> <span data-ttu-id="01c45-135">Предоставляя в конструкторе сведения о навыках, всегда `skillId` присутствуют в действиях карт.</span><span class="sxs-lookup"><span data-stu-id="01c45-135">By providing `skillId` in the constructor we ensure that skill information is always present in card actions.</span></span>

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

<span data-ttu-id="01c45-136">Далее мы вводим `SkillCardActionData` класс в шаблоне Виртуальный помощник, чтобы извлечь из полезной нагрузки `skillId` действия карты.</span><span class="sxs-lookup"><span data-stu-id="01c45-136">Next, we introduce `SkillCardActionData` class in the Virtual Assistant template to extract `skillId` from the card action payload.</span></span>

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

<span data-ttu-id="01c45-137">Ниже приведен фрагмент кода, извлеченный  `skillId` из данных действия карты.</span><span class="sxs-lookup"><span data-stu-id="01c45-137">Below is a code snippet to extract  `skillId` from card action data.</span></span> <span data-ttu-id="01c45-138">Мы реализовали его как метод расширения в [классе Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)</span><span class="sxs-lookup"><span data-stu-id="01c45-138">We implemented it as an  extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>

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

### <a name="handle-interruptions-gracefully"></a><span data-ttu-id="01c45-139">Обработка прерываний изящно</span><span class="sxs-lookup"><span data-stu-id="01c45-139">Handle interruptions gracefully</span></span>

<span data-ttu-id="01c45-140">Виртуальный помощник может обрабатывать перерывы в случаях, когда пользователь пытается вызвать навык, а другой навык в настоящее время активен.</span><span class="sxs-lookup"><span data-stu-id="01c45-140">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="01c45-141">мы внедрили и, на основе `TeamsSkillDialog` `TeamsSwitchSkillDialog` [skillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) Bot Framework и [SwitchSkillDialog,](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)чтобы пользователи могли переключать навыки с действий карт.</span><span class="sxs-lookup"><span data-stu-id="01c45-141">we have introduced `TeamsSkillDialog` and `TeamsSwitchSkillDialog`, based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), to enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="01c45-142">Для обработки этого запроса виртуальный помощник запрашивает у пользователя сообщение подтверждения для переключения навыков.</span><span class="sxs-lookup"><span data-stu-id="01c45-142">To handle this request the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![Запрос подтверждения при переходе на новый навык](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a><span data-ttu-id="01c45-144">Обработка запросов модулей задач</span><span class="sxs-lookup"><span data-stu-id="01c45-144">Handling task module requests</span></span>

<span data-ttu-id="01c45-145">Чтобы добавить возможности модуля задач в виртуальный помощник, в обработник действий виртуального помощника включены два дополнительных метода: `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="01c45-145">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="01c45-146">Эти методы прослушивают действия виртуального помощника, связанные с модулем задач, определяют навыки, связанные с запросом, и переназначяют запрос в указанный навык.</span><span class="sxs-lookup"><span data-stu-id="01c45-146">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="01c45-147">Переададка запросов осуществляется [методом SkillHttpClient.](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) `PostActivityAsync`</span><span class="sxs-lookup"><span data-stu-id="01c45-147">Request forwarding is done via the  [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` method.</span></span> <span data-ttu-id="01c45-148">Он возвращает ответ, `InvokeResponse` как который разобрано и преобразовано в `TaskModuleResponse` .</span><span class="sxs-lookup"><span data-stu-id="01c45-148">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>

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

<span data-ttu-id="01c45-149">Аналогичный подход следует для отправки действий по картам и ответов модулей задач.</span><span class="sxs-lookup"><span data-stu-id="01c45-149">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="01c45-150">Модуль задач для получения и отправки данных действий обновляется, чтобы включить `skillId` .</span><span class="sxs-lookup"><span data-stu-id="01c45-150">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="01c45-151">Метод расширения действий извлекает из полезной нагрузки, которая содержит сведения о навыке, `GetSkillId` `skillId` который необходимо вызвать.</span><span class="sxs-lookup"><span data-stu-id="01c45-151">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="01c45-152">Ниже приведен фрагмент кода для и `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` методов.</span><span class="sxs-lookup"><span data-stu-id="01c45-152">Below is a code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods.</span></span>

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

<span data-ttu-id="01c45-153">Кроме того, все домены навыков должны быть включены в раздел в файл манифеста виртуального помощника, чтобы модули задач, вызываемые с помощью отрисовки `validDomains` навыков должным образом.</span><span class="sxs-lookup"><span data-stu-id="01c45-153">Additionally, all skill domains must be included in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked via a skill render properly.</span></span>

### <a name="handling-collaborative-app-scopes"></a><span data-ttu-id="01c45-154">Обработка областей совместных приложений</span><span class="sxs-lookup"><span data-stu-id="01c45-154">Handling collaborative app scopes</span></span>

<span data-ttu-id="01c45-155">Приложения teams могут существовать в нескольких сферах, включая чат 1:1, групповой чат и каналы.</span><span class="sxs-lookup"><span data-stu-id="01c45-155">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="01c45-156">Основной шаблон виртуального помощника предназначен для чатов 1:1.</span><span class="sxs-lookup"><span data-stu-id="01c45-156">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="01c45-157">В рамках интерфейса виртуального помощника виртуальный помощник подсказывая пользователям имя и поддерживает состояние пользователя.</span><span class="sxs-lookup"><span data-stu-id="01c45-157">As part of the onboarding experience Virtual Assistant  prompts users for name and maintains user state.</span></span> <span data-ttu-id="01c45-158">Так как этот опыт работы с бортовой группой не подходит для групповых чатов и каналов, он был удален.</span><span class="sxs-lookup"><span data-stu-id="01c45-158">Since that onboarding experience is not suited for group chat/channel scopes it has been removed.</span></span>

<span data-ttu-id="01c45-159">Навыки должны обрабатывать действия в нескольких сферах (чат 1:1, групповой чат и разговор по каналу).</span><span class="sxs-lookup"><span data-stu-id="01c45-159">Skills should handle activities in multiple scopes (1:1 chat, group chat, and channel conversation).</span></span> <span data-ttu-id="01c45-160">Если какие-либо из этих областей не поддерживаются, навыки должны отвечать соответствующим сообщением.</span><span class="sxs-lookup"><span data-stu-id="01c45-160">If any of these scopes are not supported, skills should respond with an appropriate message.</span></span>

<span data-ttu-id="01c45-161">В ядро Virtual Assistant добавлены следующие функции обработки:</span><span class="sxs-lookup"><span data-stu-id="01c45-161">The following  processing functions have been added to Virtual Assistant core:</span></span>

- <span data-ttu-id="01c45-162">Виртуальный помощник может вызываться без текстовых сообщений из группового чата или канала.</span><span class="sxs-lookup"><span data-stu-id="01c45-162">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
- <span data-ttu-id="01c45-163">Перед отправкой сообщения в модуль отправки удаляются @mention бота.</span><span class="sxs-lookup"><span data-stu-id="01c45-163">Articulations are cleaned (i.e.,  remove the necessary @mention of the bot) before sending the message to the dispatch module.</span></span>

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

### <a name="handling-messaging-extensions"></a><span data-ttu-id="01c45-164">Обработка расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="01c45-164">Handling messaging extensions</span></span>

<span data-ttu-id="01c45-165">Команды для расширения обмена сообщениями объявляются в файле манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="01c45-165">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="01c45-166">Пользовательский интерфейс расширения обмена сообщениями на питание от этих команд.</span><span class="sxs-lookup"><span data-stu-id="01c45-166">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="01c45-167">Чтобы виртуальный помощник завел команду расширения обмена сообщениями (в качестве прикрепленного навыка), манифест виртуального помощника должен содержать эти команды.</span><span class="sxs-lookup"><span data-stu-id="01c45-167">For a Virtual Assistant to power a messaging extension command (as an attached skill), a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="01c45-168">Команды из манифеста отдельных навыков также должны быть добавлены в манифест виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="01c45-168">The commands from an individual skill's manifest should be added to the Virtual Assistant's manifest as well.</span></span> <span data-ttu-id="01c45-169">Командный ID предоставляет сведения о связанном навыке, придав ID приложения навыка с помощью сепаратора ( `:` ).</span><span class="sxs-lookup"><span data-stu-id="01c45-169">The command ID provides information about an associated skill by appending the skill's app ID via a separator (`:`).</span></span>

<span data-ttu-id="01c45-170">Ниже приведен фрагмент из файла манифеста навыка.</span><span class="sxs-lookup"><span data-stu-id="01c45-170">Below is a snippet from a skill's manifest file.</span></span>

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

<span data-ttu-id="01c45-171">Ниже приведен соответствующий фрагмент кода файла манифеста виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="01c45-171">And, below is the corresponding Virtual Assistant manifest file code snippet.</span></span>

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

<span data-ttu-id="01c45-172">После вызова команд пользователем виртуальный помощник может определить соответствующий навык, разбором ИД команды, обновлением действия путем удаления дополнительного суффикса () из командного ИД и его переад. `:<skill_id>`</span><span class="sxs-lookup"><span data-stu-id="01c45-172">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix (`:<skill_id>`) from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="01c45-173">Код для навыка не должен обрабатывать дополнительный суффикс, поэтому конфликтов между кодами команд между навыками не требуется.</span><span class="sxs-lookup"><span data-stu-id="01c45-173">The code for a skill doesn't need to handle the extra suffix, thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="01c45-174">С помощью этого подхода все команды поиска и действий навыка во всех контекстах ("compose", "commandBox" и "message") могут быть задействовать виртуальный помощник.</span><span class="sxs-lookup"><span data-stu-id="01c45-174">With this approach, all the search and action commands of a skill within all contexts ("compose", "commandBox" and "message") can be powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="01c45-175">Некоторые действия по расширению обмена сообщениями не включают командный ID.</span><span class="sxs-lookup"><span data-stu-id="01c45-175">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="01c45-176">Например, `composeExtension/selectItem` содержит только значение действия касания.</span><span class="sxs-lookup"><span data-stu-id="01c45-176">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="01c45-177">Чтобы определить связанный навык, при формировании ответа для каждого элемента присоединяется к каждой карте `skillId` `OnTeamsMessagingExtensionQueryAsync` элемента.</span><span class="sxs-lookup"><span data-stu-id="01c45-177">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="01c45-178">(Это похоже на подход к добавлению [адаптивных карт в виртуальный помощник.](#add-adaptive-cards-to-your-virtual-assistant)</span><span class="sxs-lookup"><span data-stu-id="01c45-178">(This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a><span data-ttu-id="01c45-179">Пример: преобразование шаблона приложения Book-a-room в навык виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="01c45-179">Example: Convert the Book-a-room app template to a Virtual Assistant skill</span></span>

<span data-ttu-id="01c45-180">[Book-a-room](app-templates.md#book-a-room) — это бот [Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям быстро находить и резервировать зал собраний в течение 30 (по умолчанию), 60 или 90 минут начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="01c45-180">[Book-a-room](app-templates.md#book-a-room) is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="01c45-181">Область бота Book-a-room для личных или 1:1 бесед.</span><span class="sxs-lookup"><span data-stu-id="01c45-181">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

![Виртуальный помощник с навыком "книга комнаты"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="01c45-183">Ниже представлены изменения дельты, введенные для преобразования его в навык, который можно прикрепить к виртуальному помощнику.</span><span class="sxs-lookup"><span data-stu-id="01c45-183">Followings are the delta changes introduced to convert it to a skill which can be attached to a Virtual Assistant.</span></span> <span data-ttu-id="01c45-184">Аналогичные рекомендации можно использовать для преобразования любого существующего бота v4 в навык.</span><span class="sxs-lookup"><span data-stu-id="01c45-184">Similar guidelines can be followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="01c45-185">Манифест мастерства</span><span class="sxs-lookup"><span data-stu-id="01c45-185">Skill manifest</span></span>

<span data-ttu-id="01c45-186">Манифест навыков — это файл JSON, который предоставляет конечную точку обмена сообщениями навыка, id, имя и другие релевантные метаданные (этот манифест отличается от манифеста, используемого для загрузки приложения в Microsoft Teams) Виртуальный помощник требует путь к этому файлу в качестве ввода для придания навыка.</span><span class="sxs-lookup"><span data-stu-id="01c45-186">A skill manifest is a JSON file that exposes a skill's messaging endpoint, id, name, and other relevant metadata (this manifest is different than the manifest used for sideloading an app in Microsoft Teams) A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="01c45-187">В папку wwwroot бота добавлен следующий манифест.</span><span class="sxs-lookup"><span data-stu-id="01c45-187">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="01c45-188">ИНТЕГРАЦИЯ LUIS</span><span class="sxs-lookup"><span data-stu-id="01c45-188">LUIS Integration</span></span>

<span data-ttu-id="01c45-189">Модель отправки виртуального помощника построена на основе присоединенных моделей LUIS навыков.</span><span class="sxs-lookup"><span data-stu-id="01c45-189">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="01c45-190">Модель отправки определяет намерения для каждой текстовой активности и находит навыки, связанные с ней.</span><span class="sxs-lookup"><span data-stu-id="01c45-190">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="01c45-191">Виртуальный помощник требует модели LUIS навыка (в формате) в качестве ввода `.lu` при присоединении навыка.</span><span class="sxs-lookup"><span data-stu-id="01c45-191">Virtual Assistant requires skill's LUIS model (in `.lu` format) as an input while attaching a skill.</span></span> <span data-ttu-id="01c45-192">LUIS json можно преобразовать в `.lu` формат с помощью средства botframework-cli.</span><span class="sxs-lookup"><span data-stu-id="01c45-192">LUIS json can be converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="01c45-193">Бот Book-a-room имеет две основные команды для пользователей:</span><span class="sxs-lookup"><span data-stu-id="01c45-193">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="01c45-194">Мы создали модель LUIS, которая понимает эти две команды.</span><span class="sxs-lookup"><span data-stu-id="01c45-194">We have built a LUIS model understanding these two commands.</span></span> <span data-ttu-id="01c45-195">Соответствующие секреты должны быть заполнены `cognitivemodels.json` в .</span><span class="sxs-lookup"><span data-stu-id="01c45-195">Corresponding secrets need to be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="01c45-196">Соответствующий файл LUIS JSON можно найти [здесь,](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) и так выглядит `.lu` соответствующий файл.</span><span class="sxs-lookup"><span data-stu-id="01c45-196">The corresponding LUIS JSON file can be found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) and this is how the corresponding `.lu` file looks like.</span></span>

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

<span data-ttu-id="01c45-197">При таком подходе любые проблемы с командой пользователя виртуальным помощником, связанные с командой, связанной с ботом `book room` Book-a-room, могут быть идентифицированы и переназначаны на `manage favorites` этот навык.</span><span class="sxs-lookup"><span data-stu-id="01c45-197">With this approach, any command issues by a user to Virtual Assistant related to `book room` or `manage favorites` can be identified as a command associated with Book-a-room bot and is forwarded to this skill.</span></span>
<span data-ttu-id="01c45-198">С другой стороны, боту Book-a-room необходимо использовать модель LUIS, чтобы понять эти команды, если они не введите как есть (например: `I want to manage my favorite rooms` ).</span><span class="sxs-lookup"><span data-stu-id="01c45-198">On the other hand, Book-a-room room bot needs to use LUIS model to understand these commands if they are not typed as is (for example: `I want to manage my favorite rooms`).</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="01c45-199">Поддержка multi-Language</span><span class="sxs-lookup"><span data-stu-id="01c45-199">Multi-Language support</span></span>

<span data-ttu-id="01c45-200">В этом примере мы создали только модель LUIS с английской культурой.</span><span class="sxs-lookup"><span data-stu-id="01c45-200">For this example, we have only created a LUIS model with English culture.</span></span> <span data-ttu-id="01c45-201">Можно создать модели LUIS, соответствующие другим языкам, и добавить запись в `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="01c45-201">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="01c45-202">Параллельно добавьте соответствующий `.lu` файл в путь LuisFolder.</span><span class="sxs-lookup"><span data-stu-id="01c45-202">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="01c45-203">Структура папок должна быть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="01c45-203">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="01c45-204">Обнови команду botskills следующим образом, чтобы изменить `languages` параметр:</span><span class="sxs-lookup"><span data-stu-id="01c45-204">Update botskills command as follows to modify `languages` parameter:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="01c45-205">Виртуальный помощник `SetLocaleMiddleware` использует для определения текущего локального запроса и вызова соответствующей модели отправки.</span><span class="sxs-lookup"><span data-stu-id="01c45-205">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="01c45-206">(Действие базы ботов имеет поле locale, которое используется этим средним программным обеспечением.) Мы рекомендуем использовать то же самое и для вашего мастерства.</span><span class="sxs-lookup"><span data-stu-id="01c45-206">(Bot framework activity has locale field which is used by this middleware.) We recommend to use the same for your skill as well.</span></span> <span data-ttu-id="01c45-207">Бот book-a-room не использует это среднее повеять и вместо этого получает локализовку из сущности [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)клиентской базы Bot framework.</span><span class="sxs-lookup"><span data-stu-id="01c45-207">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="01c45-208">Проверка утверждений</span><span class="sxs-lookup"><span data-stu-id="01c45-208">Claim validation</span></span>

<span data-ttu-id="01c45-209">Мы добавили [claimsValidator, чтобы](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) ограничить вызовы навыками.</span><span class="sxs-lookup"><span data-stu-id="01c45-209">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="01c45-210">Чтобы виртуальный помощник вызывал этот навык, заполняйте массив с помощью этого конкретного ID приложения `AllowedCallers` `appsettings` виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="01c45-210">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="01c45-211">Массив разрешенных вызовов может ограничить доступ потребителей к навыкам.</span><span class="sxs-lookup"><span data-stu-id="01c45-211">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="01c45-212">Добавьте одну запись `*` в этот массив, чтобы принимать вызовы от любого потребителя навыков.</span><span class="sxs-lookup"><span data-stu-id="01c45-212">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```
<span data-ttu-id="01c45-213">Подробную документацию по добавлению проверки утверждений в навык можно найти [здесь.](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="01c45-213">Detailed documentation for adding claims validation to a skill can be found [here](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span></span>

### <a name="card-refresh-limitation"></a><span data-ttu-id="01c45-214">Ограничение обновления карт</span><span class="sxs-lookup"><span data-stu-id="01c45-214">Card refresh limitation</span></span>

<span data-ttu-id="01c45-215">Обновление активности (обновление карт) еще не поддерживается с помощью виртуального помощника[(проблема github).](https://github.com/microsoft/botbuilder-dotnet/issues/3686)</span><span class="sxs-lookup"><span data-stu-id="01c45-215">Updating activity (card refresh) is not supported yet via Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="01c45-216">Таким образом, мы заменили все вызовы обновления карт () с `UpdateActivityAsync` размещением новых звонков карты ( `SendActivityAsync` ).</span><span class="sxs-lookup"><span data-stu-id="01c45-216">Hence, we have replaced all card refresh calls (`UpdateActivityAsync`) with posting new card calls(`SendActivityAsync`).</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="01c45-217">Действия карты и потоки модулей задач</span><span class="sxs-lookup"><span data-stu-id="01c45-217">Card actions and task module flows</span></span>

<span data-ttu-id="01c45-218">Чтобы перенаставлять действия или действия модуля задач в связанные навыки, необходимо встраить в него `skillId` навыки.</span><span class="sxs-lookup"><span data-stu-id="01c45-218">To forward card action or task module activities to an associated skill, the skill needs to embed `skillId` to it.</span></span>
<span data-ttu-id="01c45-219">Действие бот-карты book-a-room, извлечение и отправка полезной нагрузки модуля задач изменены, чтобы содержать `skillId` в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="01c45-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="01c45-220">Дополнительные сведения можно [получить в этом](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) разделе из этой документации.</span><span class="sxs-lookup"><span data-stu-id="01c45-220">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="01c45-221">Обработка действий из группового чата или области канала</span><span class="sxs-lookup"><span data-stu-id="01c45-221">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="01c45-222">Бот Book-a-room предназначен только для частных чатов (область личных данных/1:1).</span><span class="sxs-lookup"><span data-stu-id="01c45-222">Book-a-room bot is designed for private chats (personal/1:1 scope) only.</span></span> <span data-ttu-id="01c45-223">Так как мы настроили виртуальный помощник для поддержки групповых чатов и областей каналов, виртуальный помощник может быть вызван из этих областей, и таким образом, бот Book-a-room может получить действия для того же.</span><span class="sxs-lookup"><span data-stu-id="01c45-223">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant might be invoked from these scopes and thus, Book-a-room bot might get activities for the same.</span></span> <span data-ttu-id="01c45-224">Поэтому бот Book-a-room настраивается для обработки этих действий.</span><span class="sxs-lookup"><span data-stu-id="01c45-224">Hence Book-a-room bot is customized to handle those activities.</span></span> <span data-ttu-id="01c45-225">Проверка была установлена в методах обработки действий бота `OnMessageActivityAsync` Book-a-room.</span><span class="sxs-lookup"><span data-stu-id="01c45-225">The check has been put in `OnMessageActivityAsync` methods of Book-a-room bot's activity handler.</span></span>

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

<span data-ttu-id="01c45-226">Вы также можете использовать существующие навыки из [репозитория Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) или создать новый навык с нуля.</span><span class="sxs-lookup"><span data-stu-id="01c45-226">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="01c45-227">Учебники для более позднего можно найти [здесь](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="01c45-227">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="01c45-228">Обратитесь к [документации для](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) виртуального помощника и архитектуре навыков.</span><span class="sxs-lookup"><span data-stu-id="01c45-228">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) for Virtual Assistant and skills architecture.</span></span>

## <a name="code-sample"></a><span data-ttu-id="01c45-229">Пример кода</span><span class="sxs-lookup"><span data-stu-id="01c45-229">Code sample</span></span>

| <span data-ttu-id="01c45-230">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="01c45-230">**Sample name**</span></span> | <span data-ttu-id="01c45-231">**Описание**</span><span class="sxs-lookup"><span data-stu-id="01c45-231">**Description**</span></span> | <span data-ttu-id="01c45-232">**C#**</span><span class="sxs-lookup"><span data-stu-id="01c45-232">**C#**</span></span> | <span data-ttu-id="01c45-233">**.NET**</span><span class="sxs-lookup"><span data-stu-id="01c45-233">**.NET**</span></span> |
|----------|-----------------|----------|------------------|
| <span data-ttu-id="01c45-234">Обновленный шаблон визуальной студии</span><span class="sxs-lookup"><span data-stu-id="01c45-234">Updated visual studio template</span></span> | <span data-ttu-id="01c45-235">Настраиваемый шаблон для поддержки возможностей групп.</span><span class="sxs-lookup"><span data-stu-id="01c45-235">Customized template to support teams capabilities.</span></span> | [<span data-ttu-id="01c45-236">View</span><span class="sxs-lookup"><span data-stu-id="01c45-236">View</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| <span data-ttu-id="01c45-237">Код навыков бота book-a-room</span><span class="sxs-lookup"><span data-stu-id="01c45-237">Book-a-room bot skill code</span></span> | <span data-ttu-id="01c45-238">Позволяет быстро найти и заказать комнату собраний на время.</span><span class="sxs-lookup"><span data-stu-id="01c45-238">Lets you quickly find and book a meeting room on the go.</span></span> |  | [<span data-ttu-id="01c45-239">View</span><span class="sxs-lookup"><span data-stu-id="01c45-239">View</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |



## <a name="virtual-assistant-known-limitations"></a><span data-ttu-id="01c45-240">Виртуальный помощник известных ограничений</span><span class="sxs-lookup"><span data-stu-id="01c45-240">Virtual Assistant known limitations</span></span>

- <span data-ttu-id="01c45-241">**EndOfConversation**.</span><span class="sxs-lookup"><span data-stu-id="01c45-241">**EndOfConversation**.</span></span> <span data-ttu-id="01c45-242">Навык должен отправлять действие по завершению `endOfConversation` беседы.</span><span class="sxs-lookup"><span data-stu-id="01c45-242">A skill should send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="01c45-243">На основе этого действия виртуальный помощник завершает контекст этим определенным навыком и возвращается в корневой контекст виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="01c45-243">basis this activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's (root) context.</span></span> <span data-ttu-id="01c45-244">Для бота Book-a-room нет четкого состояния, в котором можно было бы закончить беседу.</span><span class="sxs-lookup"><span data-stu-id="01c45-244">For Book-a-room bot, there is no clear state where conversation can be ended.</span></span> <span data-ttu-id="01c45-245">Поэтому мы не отослали из `endOfConversation` бота Book-a-room, и когда пользователь хочет вернуться к корневому контексту, он может просто сделать это по `start over` команде.</span><span class="sxs-lookup"><span data-stu-id="01c45-245">Hence we have not sent `endOfConversation` from Book-a-room bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>
- <span data-ttu-id="01c45-246">**Обновление карты.**</span><span class="sxs-lookup"><span data-stu-id="01c45-246">**Card refresh**.</span></span> <span data-ttu-id="01c45-247">Обновление карты еще не поддерживается с помощью виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="01c45-247">Card refreshes is not yet supported through Virtual Assistant.</span></span>
- <span data-ttu-id="01c45-248">**Расширения обмена сообщениями**.:</span><span class="sxs-lookup"><span data-stu-id="01c45-248">**Messaging extensions**.:</span></span>
  - <span data-ttu-id="01c45-249">В настоящее время виртуальный помощник может поддерживать не более десяти команд для расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="01c45-249">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  - <span data-ttu-id="01c45-250">Конфигурация расширений обмена сообщениями не касается отдельных команд, а всего расширения.</span><span class="sxs-lookup"><span data-stu-id="01c45-250">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="01c45-251">Это ограничивает конфигурацию для каждого отдельного навыка с помощью виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="01c45-251">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  - <span data-ttu-id="01c45-252">Командные ИД расширений обмена сообщениями имеют максимальную длину [64](../resources/schema/manifest-schema.md#composeextensions) символа, а для встраиванию сведений о навыках будут использоваться 37 символов.</span><span class="sxs-lookup"><span data-stu-id="01c45-252">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters will be used for embedding skill information.</span></span> <span data-ttu-id="01c45-253">Таким образом, обновленные ограничения для командного ID ограничены 27 символами.</span><span class="sxs-lookup"><span data-stu-id="01c45-253">Thus, updated constraints for command ID are limited to 27 characters.</span></span>
>
>
