---
title: Виртуальный помощник для Microsoft Teams
description: Создание ленты и навыков виртуального помощника для использования в Microsoft Teams
keywords: Боты виртуального помощника Teams
ms.openlocfilehash: 0bb1ad832fd33675e607874fcc50f20ffbb96943
ms.sourcegitcommit: 26b7404142706290810064f8216abaa1c262d1e5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/16/2020
ms.locfileid: "45146022"
---
# <a name="virtual-assistant-for-microsoft-teams"></a><span data-ttu-id="8b407-104">Виртуальный помощник для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8b407-104">Virtual Assistant for Microsoft Teams</span></span>

<span data-ttu-id="8b407-105">Virtual Assistant — это шаблон Microsoft Open-Source, который позволяет создавать надежное диалоговое решение, обеспечивая полный контроль над возможностями взаимодействия с пользователем, фирменной символикой и необходимыми данными.</span><span class="sxs-lookup"><span data-stu-id="8b407-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="8b407-106">[Основной шаблон основного помощника](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) — это базовый Стандартный блок, который объединяет технологии Майкрософт, необходимые для создания виртуального помощника, включая [пакет SDK для ленты](https://github.com/microsoft/botframework-sdk), [язык (Луис)](https://www.luis.ai/), [КНА Maker](https://www.qnamaker.ai/), а также важные возможности, включая регистрацию навыков, связанные учетные записи, базовую цепочку для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="8b407-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), as well as essential capabilities including  skills registration, linked accounts, basic conversational intent to offer end users a range of seamless interactions and experiences.</span></span> <span data-ttu-id="8b407-107">Кроме того, вы также включаете в себя обширные примеры полезных [навыков](https://microsoft.github.io/botframework-solutions/overview/skills)для общения.</span><span class="sxs-lookup"><span data-stu-id="8b407-107">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="8b407-108">Отдельные навыки можно интегрировать в решение Virtual Assistant для поддержки нескольких сценариев.</span><span class="sxs-lookup"><span data-stu-id="8b407-108">Individual skills can be integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="8b407-109">С помощью пакета SDK для ленты, навыки представлены в форме исходного кода, что позволяет настраивать и расширять их по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="8b407-109">Using the Bot Framework SDK, Skills are presented in source code form enabling you to customize and extend as required.</span></span> <span data-ttu-id="8b407-110">Узнайте [, что такое навык в виде Bot-Framework](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="8b407-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span>

![Схема обзора Virtual Assistant](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="8b407-112">Текстовые действия с сообщениями направляются на связанные навыки ядром виртуального помощника с помощью модели [отправки](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) .</span><span class="sxs-lookup"><span data-stu-id="8b407-112">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="8b407-113">Рекомендации по реализации</span><span class="sxs-lookup"><span data-stu-id="8b407-113">Implementation considerations</span></span>

<span data-ttu-id="8b407-114">Решение о добавлении виртуального помощника может включать множество детерминантс и различаться для каждой организации.</span><span class="sxs-lookup"><span data-stu-id="8b407-114">The decision to add a Virtual Assistant can include many determinants and differ for each organization.</span></span> <span data-ttu-id="8b407-115">Ниже приведены факторы, которые поддерживают реализацию виртуального помощника для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8b407-115">Here are the factors that support implementing a Virtual Assistant for your organization:</span></span>

- <span data-ttu-id="8b407-116">Централизованная команда управляет всеми сотрудниками отдела и имеет возможность создавать интерфейс виртуального помощника и управлять обновлениями для основного интерфейса, включая добавление новых навыков.</span><span class="sxs-lookup"><span data-stu-id="8b407-116">A central team manages all employee experiences and has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
- <span data-ttu-id="8b407-117">Несколько приложений существуют в бизнес-функциях и/или их число в будущем должно увеличиться.</span><span class="sxs-lookup"><span data-stu-id="8b407-117">Multiple applications exist across business functions and/or the number is expected to grow in the future.</span></span>
- <span data-ttu-id="8b407-118">Существующие приложения могут настраиваться, принадлежать Организации и могут быть преобразованы в навыки виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="8b407-118">Existing applications are customizable, owned by the organization, and can be converted into skills for a Virtual Assistant.</span></span>
- <span data-ttu-id="8b407-119">Центральная группа сотрудников может влиять на настройки существующих приложений и предоставлять необходимые рекомендации по интеграции существующих приложений в качестве навыков в интерфейсе Virtual Assistant</span><span class="sxs-lookup"><span data-stu-id="8b407-119">The central employee-experiences team is able to influence customizations to existing apps and provide necessary guidance for integrating existing applications as skills in Virtual Assistant experience</span></span>

![Центральная группа поддерживает помощника, а бизнес-функции Teams — навыки](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="8b407-121">Создание виртуального помощника, ориентированного на Teams</span><span class="sxs-lookup"><span data-stu-id="8b407-121">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="8b407-122">Корпорация Майкрософт опубликовала [шаблон Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) для создания виртуальных помощников и навыков.</span><span class="sxs-lookup"><span data-stu-id="8b407-122">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="8b407-123">С помощью шаблона Visual Studio вы можете создать виртуальный помощник, на основе текстового интерфейса с поддержкой ограниченных карт с действиями.</span><span class="sxs-lookup"><span data-stu-id="8b407-123">With the Visual Studio template, you can create a Virtual Assistant, powered by a text-based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="8b407-124">Мы добавили расширенный шаблон Visual Studio, чтобы включить возможности платформы Microsoft Teams и мощные возможности для работы с приложениями в Teams.</span><span class="sxs-lookup"><span data-stu-id="8b407-124">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="8b407-125">Некоторые возможности включают поддержку расширенных адаптивных карт, модулей задач, команд и групповых чатов и расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8b407-125">A few of the capabilities include support for rich adaptive cards, task modules, teams/group chats and messaging extensions.</span></span> <span data-ttu-id="8b407-126">*Кроме того*, [в этой статье рассказывается о том, как расширить свой виртуальный помощник до Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span><span class="sxs-lookup"><span data-stu-id="8b407-126">*See also*, [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>

![Высокоуровневая схема решения Virtual Assistant](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="8b407-128">Добавление адаптивных карт для виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="8b407-128">Add adaptive cards to your Virtual Assistant</span></span>

<span data-ttu-id="8b407-129">Чтобы правильно обработать запросы, ваш виртуальный помощник должен определить правильную модель Луис и соответствующий навык, связанный с ней.</span><span class="sxs-lookup"><span data-stu-id="8b407-129">To dispatch requests properly, your Virtual Assistant needs to identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="8b407-130">Тем не менее, механизм диспетчеризации невозможно использовать для действий с карточками, так как модель Луис, связанная с навыком, может не быть обучена для текстов действий карты, так как они являются фиксированными, предопределенными ключевыми словами, а не уттеранцес от пользователя.</span><span class="sxs-lookup"><span data-stu-id="8b407-130">However, the dispatching mechanism cannot be used for card action activities since the LUIS model associated with a skill may not be trained for card action texts since these are fixed, pre-defined keywords, not utterances from a user.</span></span>

<span data-ttu-id="8b407-131">Мы разрешали эту проблему, внедрив сведения о навыках в полезные данные действий карты.</span><span class="sxs-lookup"><span data-stu-id="8b407-131">We have resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="8b407-132">Каждый навык должен внедряться `skillId` в `value` поле действия с карточками.</span><span class="sxs-lookup"><span data-stu-id="8b407-132">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="8b407-133">Это лучший способ гарантировать, что каждое действие действия с картой несет соответствующую информацию о навыках, и виртуальный помощник сможет использовать эту информацию для диспетчеризации.</span><span class="sxs-lookup"><span data-stu-id="8b407-133">This is the best way to ensure that each card action activity carries the relevant skill information and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="8b407-134">Ниже приведен пример данных действия карты.</span><span class="sxs-lookup"><span data-stu-id="8b407-134">Below is a card action data sample.</span></span> <span data-ttu-id="8b407-135">Предоставляя `skillId` конструктор, вы гарантируете, что сведения о навыках всегда присутствуют в действиях карточки.</span><span class="sxs-lookup"><span data-stu-id="8b407-135">By providing `skillId` in the constructor we ensure that skill information is always present in card actions.</span></span>

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

<span data-ttu-id="8b407-136">Далее мы рассмотрим `SkillCardActionData` класс в шаблоне Virtual Assistant, чтобы извлечь `skillId` из полезных данных действия карточки.</span><span class="sxs-lookup"><span data-stu-id="8b407-136">Next, we introduce `SkillCardActionData` class in the Virtual Assistant template to extract `skillId` from the card action payload.</span></span>

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

<span data-ttu-id="8b407-137">Ниже приведен фрагмент кода, который необходимо извлечь `skillId` из данных действий карты.</span><span class="sxs-lookup"><span data-stu-id="8b407-137">Below is a code snippet to extract  `skillId` from card action data.</span></span> <span data-ttu-id="8b407-138">Мы реализовали его в качестве метода расширения в классе [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) .</span><span class="sxs-lookup"><span data-stu-id="8b407-138">We implemented it as an  extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>

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

### <a name="handle-interruptions-gracefully"></a><span data-ttu-id="8b407-139">Мягкое прерывание обработки прерываний</span><span class="sxs-lookup"><span data-stu-id="8b407-139">Handle interruptions gracefully</span></span>

<span data-ttu-id="8b407-140">Виртуальный помощник может обрабатывать прерывания в тех случаях, когда пользователь пытается вызвать навык, пока в данный момент активен другой навык.</span><span class="sxs-lookup"><span data-stu-id="8b407-140">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="8b407-141">Мы предоставили `TeamsSkillDialog` и `TeamsSwitchSkillDialog` , на основе [скиллдиалог](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) и [свитчскиллдиалог](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), чтобы позволить пользователям переключать навыки из действий карты.</span><span class="sxs-lookup"><span data-stu-id="8b407-141">we have introduced `TeamsSkillDialog` and `TeamsSwitchSkillDialog`, based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), to enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="8b407-142">Чтобы обработать этот запрос, виртуальный помощник запросит у пользователя сообщение с подтверждением, чтобы переключить навыки.</span><span class="sxs-lookup"><span data-stu-id="8b407-142">To handle this request the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![Запрос подтверждения при переключении на новый навык](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a><span data-ttu-id="8b407-144">Обработка запросов модулей задач</span><span class="sxs-lookup"><span data-stu-id="8b407-144">Handling task module requests</span></span>

<span data-ttu-id="8b407-145">Чтобы добавить возможности модуля задач для виртуального помощника, в обработчик действий виртуального помощника включены два дополнительных метода: `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="8b407-145">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="8b407-146">Эти методы прослушивают действия, связанные с модулем задач, от виртуального помощника, идентифицируют навык, связанный с запросом, и пересылают запрос определенному навыку.</span><span class="sxs-lookup"><span data-stu-id="8b407-146">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="8b407-147">Пересылка запросов выполняется с помощью [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable)метода скиллхттпклиент `PostActivityAsync` .</span><span class="sxs-lookup"><span data-stu-id="8b407-147">Request forwarding is done via the  [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable), `PostActivityAsync` method.</span></span> <span data-ttu-id="8b407-148">Он возвращает ответ, `InvokeResponse` который анализируется и преобразуется в `TaskModuleResponse` .</span><span class="sxs-lookup"><span data-stu-id="8b407-148">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>

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

<span data-ttu-id="8b407-149">Аналогичный подход используется для диспетчеризации действий карты и ответа модуля задач.</span><span class="sxs-lookup"><span data-stu-id="8b407-149">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="8b407-150">Данные действий при получении и отсылке модуля задачи обновляются, чтобы включить их `skillId` .</span><span class="sxs-lookup"><span data-stu-id="8b407-150">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="8b407-151">Метод расширения действия `GetSkillId` извлекает `skillId` данные из полезных данных, которые предоставляют сведения о навыках, которые необходимо вызвать.</span><span class="sxs-lookup"><span data-stu-id="8b407-151">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="8b407-152">Ниже приведен фрагмент кода для `OnTeamsTaskModuleFetchAsync` методов и `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="8b407-152">Below is a code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods.</span></span>

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

<span data-ttu-id="8b407-153">Кроме того, все домены навыков должны быть включены в `validDomains` раздел файла манифеста виртуального помощника, чтобы модули задач, вызываемые с помощью навыка, правильно отрисовывается.</span><span class="sxs-lookup"><span data-stu-id="8b407-153">Additionally, all skill domains must be included in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked via a skill render properly.</span></span>

### <a name="handling-collaborative-app-scopes"></a><span data-ttu-id="8b407-154">Обработка областей приложений для сотрудничества</span><span class="sxs-lookup"><span data-stu-id="8b407-154">Handling collaborative app scopes</span></span>

<span data-ttu-id="8b407-155">Приложения Teams могут существовать в нескольких областях, в том числе чат 1:1, групповой чат и каналы.</span><span class="sxs-lookup"><span data-stu-id="8b407-155">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="8b407-156">Шаблон основного виртуального помощника предназначен для 1:1 сеансов.</span><span class="sxs-lookup"><span data-stu-id="8b407-156">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="8b407-157">В процессе входящей миграции виртуальный помощник запрашивает у пользователей имя и сохраняет состояние пользователя.</span><span class="sxs-lookup"><span data-stu-id="8b407-157">As part of the onboarding experience Virtual Assistant  prompts users for name and maintains user state.</span></span> <span data-ttu-id="8b407-158">Так как этот процесс входящей миграции не подходит для областей группового чата и каналов, он был удален.</span><span class="sxs-lookup"><span data-stu-id="8b407-158">Since that onboarding experience is not suited for group chat/channel scopes it has been removed.</span></span>

<span data-ttu-id="8b407-159">Навыки должны обрабатывать действия в нескольких областях (1:1 чат, группового чата и беседы каналов).</span><span class="sxs-lookup"><span data-stu-id="8b407-159">Skills should handle activities in multiple scopes (1:1 chat, group chat, and channel conversation).</span></span> <span data-ttu-id="8b407-160">Если какая – либо из этих областей не поддерживается, навыки должны отреагировать на соответствующее сообщение.</span><span class="sxs-lookup"><span data-stu-id="8b407-160">If any of these scopes are not supported, skills should respond with an appropriate message.</span></span>

<span data-ttu-id="8b407-161">В ядро виртуального помощника добавлены следующие функции обработки:</span><span class="sxs-lookup"><span data-stu-id="8b407-161">The following  processing functions have been added to Virtual Assistant core:</span></span>

- <span data-ttu-id="8b407-162">Виртуальный помощник может вызываться без текстового сообщения из группового чата или канала.</span><span class="sxs-lookup"><span data-stu-id="8b407-162">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
- <span data-ttu-id="8b407-163">Артикулатионс очищаются (то есть удалите необходимое @mention ленты) перед отправкой сообщения в модуль диспетчеризации.</span><span class="sxs-lookup"><span data-stu-id="8b407-163">Articulations are cleaned (i.e.,  remove the necessary @mention of the bot) before sending the message to the dispatch module.</span></span>

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

### <a name="handling-messaging-extensions"></a><span data-ttu-id="8b407-164">Обработка расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="8b407-164">Handling messaging extensions</span></span>

<span data-ttu-id="8b407-165">Команды для расширения обмена сообщениями объявляются в файле манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="8b407-165">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="8b407-166">Пользовательский интерфейс расширения обмена сообщениями питается от этих команд.</span><span class="sxs-lookup"><span data-stu-id="8b407-166">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="8b407-167">Чтобы виртуальный помощник по работе с командой расширения системы обмена сообщениями (в качестве присоединенного навыка), собственный манифест виртуального помощника должен содержать эти команды.</span><span class="sxs-lookup"><span data-stu-id="8b407-167">For a Virtual Assistant to power a messaging extension command (as an attached skill), a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="8b407-168">Команды из манифеста отдельного навыка также необходимо добавить в манифест виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="8b407-168">The commands from an individual skill's manifest should be added to the Virtual Assistant's manifest as well.</span></span> <span data-ttu-id="8b407-169">КОД команды предоставляет сведения о связанном навыке, добавляя идентификатор приложения для навыка с помощью разделителя ( `:` ).</span><span class="sxs-lookup"><span data-stu-id="8b407-169">The command ID provides information about an associated skill by appending the skill's app ID via a separator (`:`).</span></span>

<span data-ttu-id="8b407-170">Ниже приведен фрагмент файла манифеста для навыка.</span><span class="sxs-lookup"><span data-stu-id="8b407-170">Below is a snippet from a skill's manifest file.</span></span>

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

<span data-ttu-id="8b407-171">А ниже — соответствующий фрагмент кода файла манифеста виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="8b407-171">And, below is the corresponding Virtual Assistant manifest file code snippet.</span></span>

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

<span data-ttu-id="8b407-172">Когда пользователь вызывает команды, виртуальный помощник может определить связанный навык путем синтаксического анализа идентификатора команды, обновить действие, удалив лишний суффикс ( `:<skill_id>` ) из идентификатора команды и переслать его соответствующему навыку.</span><span class="sxs-lookup"><span data-stu-id="8b407-172">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix (`:<skill_id>`) from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="8b407-173">Коду для квалификации не требуется обрабатывать дополнительный суффикс, поэтому не следует использовать конфликты между идентификаторами команд в навыках.</span><span class="sxs-lookup"><span data-stu-id="8b407-173">The code for a skill doesn't need to handle the extra suffix, thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="8b407-174">Благодаря этому подходу все команды поиска и действий навыка в рамках всех контекстов ("создание", "Коммандбокс" и "сообщение") могут быть включены виртуальным помощником.</span><span class="sxs-lookup"><span data-stu-id="8b407-174">With this approach, all the search and action commands of a skill within all contexts ("compose", "commandBox" and "message") can be powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="8b407-175">Некоторые действия по расширению системы обмена сообщениями не включают идентификатор команды.</span><span class="sxs-lookup"><span data-stu-id="8b407-175">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="8b407-176">Например, `composeExtension/selectItem` содержит только значение действия Invoke TAP.</span><span class="sxs-lookup"><span data-stu-id="8b407-176">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="8b407-177">Чтобы определить связанный навык, `skillId` прикрепляется к каждой карточке товара при создании ответа на `OnTeamsMessagingExtensionQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="8b407-177">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="8b407-178">(Это аналогично способу [добавления адаптивных карт для виртуального помощника](#add-adaptive-cards-to-your-virtual-assistant).</span><span class="sxs-lookup"><span data-stu-id="8b407-178">(This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a><span data-ttu-id="8b407-179">Пример: преобразование шаблона приложения "книга — комната" в навык виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="8b407-179">Example: Convert the Book-a-room app template to a Virtual Assistant skill</span></span>

<span data-ttu-id="8b407-180">[Book-a-комната](app-templates.md#book-a-room) — это [робот Microsoft Teams](../bots/what-are-bots.md) , который позволяет пользователям быстро находить и зарезервировать комнату для собраний в течение 30 (по умолчанию), 60 или 90 минут, начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="8b407-180">[Book-a-room](app-templates.md#book-a-room) is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="8b407-181">Области Bot "книга — комната" для личных или 1:1 бесед.</span><span class="sxs-lookup"><span data-stu-id="8b407-181">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

![Виртуальный помощник с навыком "книга" в помещении](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="8b407-183">Ниже приведены изменения, внесенные в разницу для преобразования в навык, который можно присоединить к виртуальному помощнику.</span><span class="sxs-lookup"><span data-stu-id="8b407-183">Followings are the delta changes introduced to convert it to a skill which can be attached to a Virtual Assistant.</span></span> <span data-ttu-id="8b407-184">Аналогичные инструкции можно выполнить, чтобы преобразовать любой существующий робот v4 в навык.</span><span class="sxs-lookup"><span data-stu-id="8b407-184">Similar guidelines can be followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="8b407-185">Манифест навыка</span><span class="sxs-lookup"><span data-stu-id="8b407-185">Skill manifest</span></span>

<span data-ttu-id="8b407-186">Манифест навыка это JSON-файл, который предоставляет конечную точку обмена сообщениями, идентификатор, имя и другие релевантные метаданные (этот манифест отличается от манифеста, используемого для неопубликованного приложения в Microsoft Teams). виртуальному помощнику требуется путь к этому файлу в качестве входных данных для присоединения навыка.</span><span class="sxs-lookup"><span data-stu-id="8b407-186">A skill manifest is a JSON file that exposes a skill's messaging endpoint, id, name, and other relevant metadata (this manifest is different than the manifest used for sideloading an app in Microsoft Teams) A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="8b407-187">Мы добавили следующий манифест в папку wwwroot для ленты.</span><span class="sxs-lookup"><span data-stu-id="8b407-187">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="8b407-188">Интеграция Луис</span><span class="sxs-lookup"><span data-stu-id="8b407-188">LUIS Integration</span></span>

<span data-ttu-id="8b407-189">Модель диспетчеризации виртуального помощника построена на основе моделей Луис присоединенных навыков.</span><span class="sxs-lookup"><span data-stu-id="8b407-189">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="8b407-190">Модель диспетчеризации определяет цель для каждого текстового действия и находит навык, связанный с ним.</span><span class="sxs-lookup"><span data-stu-id="8b407-190">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="8b407-191">Виртуальному помощнику необходимо, чтобы в качестве входных данных в качестве входного навыка была модель Луис (в `.lu` формате).</span><span class="sxs-lookup"><span data-stu-id="8b407-191">Virtual Assistant requires skill's LUIS model (in `.lu` format) as an input while attaching a skill.</span></span> <span data-ttu-id="8b407-192">Луис JSON можно преобразовать в `.lu` Формат с помощью средства ботфрамеворк – CLI.</span><span class="sxs-lookup"><span data-stu-id="8b407-192">LUIS json can be converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="8b407-193">В книге поробота a для комнаты две основные команды для пользователей:</span><span class="sxs-lookup"><span data-stu-id="8b407-193">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="8b407-194">Мы создали модель Луис, которая понимает эти две команды.</span><span class="sxs-lookup"><span data-stu-id="8b407-194">We have built a LUIS model understanding these two commands.</span></span> <span data-ttu-id="8b407-195">Соответствующие секреты должны быть заполнены `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="8b407-195">Corresponding secrets need to be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="8b407-196">Соответствующий JSON-файл Луис можно найти [здесь](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) , и именно так `.lu` выглядит соответствующий файл.</span><span class="sxs-lookup"><span data-stu-id="8b407-196">The corresponding LUIS JSON file can be found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) and this is how the corresponding `.lu` file looks like.</span></span>

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

<span data-ttu-id="8b407-197">При использовании этого подхода любая команда, связанная с пользователем `book room` или `manage favorites` может быть идентифицирована как команда, связанная с программой-роботом Book-a-Room и Переадресованная этому навыку.</span><span class="sxs-lookup"><span data-stu-id="8b407-197">With this approach, any command issues by a user to Virtual Assistant related to `book room` or `manage favorites` can be identified as a command associated with Book-a-room bot and is forwarded to this skill.</span></span>
<span data-ttu-id="8b407-198">С другой стороны, для этого необходимо использовать модель Луис для изучения этих команд, если они не типизированы как есть (например: `I want to manage my favorite rooms` ).</span><span class="sxs-lookup"><span data-stu-id="8b407-198">On the other hand, Book-a-room room bot needs to use LUIS model to understand these commands if they are not typed as is (for example: `I want to manage my favorite rooms`).</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="8b407-199">Поддержка нескольких языков</span><span class="sxs-lookup"><span data-stu-id="8b407-199">Multi-Language support</span></span>

<span data-ttu-id="8b407-200">В этом примере мы создали только модель Луис с английским языком и региональными параметрами.</span><span class="sxs-lookup"><span data-stu-id="8b407-200">For this example, we have only created a LUIS model with English culture.</span></span> <span data-ttu-id="8b407-201">Вы можете создавать модели Луис, соответствующие другим языкам, и добавлять записи в `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="8b407-201">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="8b407-202">Параллельно добавьте соответствующий `.lu` файл в путь луисфолдер.</span><span class="sxs-lookup"><span data-stu-id="8b407-202">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="8b407-203">Структура папок должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8b407-203">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="8b407-204">Чтобы изменить параметр, выполните команду Update ботскиллс следующим образом `languages` .</span><span class="sxs-lookup"><span data-stu-id="8b407-204">Update botskills command as follows to modify `languages` parameter:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="8b407-205">Виртуальный помощник использует `SetLocaleMiddleware` для определения текущего языкового стандарта и вызова соответствующей модели отправки.</span><span class="sxs-lookup"><span data-stu-id="8b407-205">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="8b407-206">(Действие "Bot Framework" имеет поле языкового стандарта, которое используется этим промежуточным по.) Мы рекомендуем использовать те же сведения, что и для вашего навыка.</span><span class="sxs-lookup"><span data-stu-id="8b407-206">(Bot framework activity has locale field which is used by this middleware.) We recommend to use the same for your skill as well.</span></span> <span data-ttu-id="8b407-207">Books — Bot для начала работы не использует это промежуточное по и вместо этого задается языковой стандарт для [объекта клиентинфо](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)действия Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="8b407-207">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="8b407-208">Проверка утверждения</span><span class="sxs-lookup"><span data-stu-id="8b407-208">Claim validation</span></span>

<span data-ttu-id="8b407-209">Мы добавили [клаимсвалидатор](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) , чтобы ограничить абоненты навыком.</span><span class="sxs-lookup"><span data-stu-id="8b407-209">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="8b407-210">Чтобы разрешить виртуальному помощнику вызывать этот навык, заполните `AllowedCallers` массив `appsettings` с помощью идентификатора приложения конкретного виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="8b407-210">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="8b407-211">Допустимый массив абонентов может ограничивать круг пользователей, которые могут получить доступ к навыку.</span><span class="sxs-lookup"><span data-stu-id="8b407-211">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="8b407-212">Добавьте `*` к этому массиву одну запись, чтобы принимать звонки от любого потребителя опыта.</span><span class="sxs-lookup"><span data-stu-id="8b407-212">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```
<span data-ttu-id="8b407-213">[Здесь вы найдете](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)подробную документацию по добавлению проверки утверждений для навыка.</span><span class="sxs-lookup"><span data-stu-id="8b407-213">Detailed documentation for adding claims validation to a skill can be found [here](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator).</span></span>

### <a name="card-refresh-limitation"></a><span data-ttu-id="8b407-214">Ограничение на обновление карты</span><span class="sxs-lookup"><span data-stu-id="8b407-214">Card refresh limitation</span></span>

<span data-ttu-id="8b407-215">Действия по обновлению (обновление карты) пока не поддерживаются виртуальным помощником ([Ошибка GitHub](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span><span class="sxs-lookup"><span data-stu-id="8b407-215">Updating activity (card refresh) is not supported yet via Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="8b407-216">Таким образом, мы заменили все вызовы обновления карт ( `UpdateActivityAsync` ) с учетом вызовов новых карточек ( `SendActivityAsync` ).</span><span class="sxs-lookup"><span data-stu-id="8b407-216">Hence, we have replaced all card refresh calls (`UpdateActivityAsync`) with posting new card calls(`SendActivityAsync`).</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="8b407-217">Потоки действий карты и модуля задач</span><span class="sxs-lookup"><span data-stu-id="8b407-217">Card actions and task module flows</span></span>

<span data-ttu-id="8b407-218">Для пересылки карточки действий или действий модуля задач в связанный навык необходимо внедрить `skillId` их в этот навык.</span><span class="sxs-lookup"><span data-stu-id="8b407-218">To forward card action or task module activities to an associated skill, the skill needs to embed `skillId` to it.</span></span>
<span data-ttu-id="8b407-219">Действие "книга" — действие с картой "подача", "модуль задач" и "действия по отсылке" изменяются в `skillId` соответствии с параметром.</span><span class="sxs-lookup"><span data-stu-id="8b407-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="8b407-220">Для получения дополнительных сведений обратитесь к [этому](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) разделу из этой документации.</span><span class="sxs-lookup"><span data-stu-id="8b407-220">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="8b407-221">Обработка действий из области группового чата или канала</span><span class="sxs-lookup"><span data-stu-id="8b407-221">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="8b407-222">Почтовые роботы, предназначенные только для частных чатов (персональный/1:1 область).</span><span class="sxs-lookup"><span data-stu-id="8b407-222">Book-a-room bot is designed for private chats (personal/1:1 scope) only.</span></span> <span data-ttu-id="8b407-223">Так как у нас есть настроенный виртуальный помощник для поддержки областей группового чата и каналов, виртуальный помощник может вызываться из этих областей и, таким образом, может получить действия из книги "робот".</span><span class="sxs-lookup"><span data-stu-id="8b407-223">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant might be invoked from these scopes and thus, Book-a-room bot might get activities for the same.</span></span> <span data-ttu-id="8b407-224">Таким образом, для обработки этих действий настроен заказ ленты a-комната.</span><span class="sxs-lookup"><span data-stu-id="8b407-224">Hence Book-a-room bot is customized to handle those activities.</span></span> <span data-ttu-id="8b407-225">Проверка включена в `OnMessageActivityAsync` методы обработчика активности для ленты "книга — комната".</span><span class="sxs-lookup"><span data-stu-id="8b407-225">The check has been put in `OnMessageActivityAsync` methods of Book-a-room bot's activity handler.</span></span>

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

<span data-ttu-id="8b407-226">Вы также можете использовать существующие навыки из [репозитория решений для Bot](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) или создать новый навык с нуля.</span><span class="sxs-lookup"><span data-stu-id="8b407-226">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="8b407-227">Учебные пособия для более поздних версий можно найти [здесь](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="8b407-227">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="8b407-228">Ознакомьтесь с [документацией](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0) по архитектуре виртуального помощника и навыков.</span><span class="sxs-lookup"><span data-stu-id="8b407-228">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   for Virtual Assistant and skills architecture.</span></span>

## <a name="sample-code-to-get-started"></a><span data-ttu-id="8b407-229">Пример кода, чтобы приступить к работе</span><span class="sxs-lookup"><span data-stu-id="8b407-229">Sample code to get started</span></span>

- [<span data-ttu-id="8b407-230">Обновленный шаблон Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8b407-230">Updated visual studio template</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [<span data-ttu-id="8b407-231">Код квалификации botа "книга — комната"</span><span class="sxs-lookup"><span data-stu-id="8b407-231">Book-a-room bot skill code</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a><span data-ttu-id="8b407-232">Известные ограничения виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="8b407-232">Virtual Assistant known limitations</span></span>

- <span data-ttu-id="8b407-233">**Ендофконверсатион**.</span><span class="sxs-lookup"><span data-stu-id="8b407-233">**EndOfConversation**.</span></span> <span data-ttu-id="8b407-234">Навык должен отправить `endOfConversation` действие при завершении беседы.</span><span class="sxs-lookup"><span data-stu-id="8b407-234">A skill should send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="8b407-235">на основе этого действия виртуальный помощник заканчивает контекст с определенным навыком и возвращается в контекст виртуального помощника (корневого).</span><span class="sxs-lookup"><span data-stu-id="8b407-235">basis this activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's (root) context.</span></span> <span data-ttu-id="8b407-236">Для ленты "книга — комната" нет четкого состояния, в котором можно завершить беседу.</span><span class="sxs-lookup"><span data-stu-id="8b407-236">For Book-a-room bot, there is no clear state where conversation can be ended.</span></span> <span data-ttu-id="8b407-237">Поэтому мы не отправили `endOfConversation` с ленты Books — a Room, а когда пользователь хочет вернуться к корневому контексту, он может просто сделать это с помощью `start over` команды.</span><span class="sxs-lookup"><span data-stu-id="8b407-237">Hence we have not sent `endOfConversation` from Book-a-room bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>
- <span data-ttu-id="8b407-238">**Обновление карточки**.</span><span class="sxs-lookup"><span data-stu-id="8b407-238">**Card refresh**.</span></span> <span data-ttu-id="8b407-239">Обновления карт пока не поддерживаются виртуальным помощником.</span><span class="sxs-lookup"><span data-stu-id="8b407-239">Card refreshes is not yet supported through Virtual Assistant.</span></span>
- <span data-ttu-id="8b407-240">**Расширения для обмена сообщениями**:</span><span class="sxs-lookup"><span data-stu-id="8b407-240">**Messaging extensions**.:</span></span>
  - <span data-ttu-id="8b407-241">В настоящее время виртуальный помощник может поддерживать не более десяти команд для расширений системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8b407-241">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  - <span data-ttu-id="8b407-242">Конфигурация расширений обмена сообщениями не ограничена отдельными командами, но для всего расширения.</span><span class="sxs-lookup"><span data-stu-id="8b407-242">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="8b407-243">Это ограничит конфигурацию каждого отдельного навыка с помощью виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="8b407-243">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  - <span data-ttu-id="8b407-244">Длина идентификаторов команд расширений обмена сообщениями не должна превышать [64 символов](../resources/schema/manifest-schema.md#composeextensions) , а для внедрения сведений о навыках будет использоваться 37 символов.</span><span class="sxs-lookup"><span data-stu-id="8b407-244">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters will be used for embedding skill information.</span></span> <span data-ttu-id="8b407-245">Таким образом, в обновленных ограничениях для идентификатора команды можно добавить не более 27 символов.</span><span class="sxs-lookup"><span data-stu-id="8b407-245">Thus, updated constraints for command ID are limited to 27 characters.</span></span>
>
>
