---
title: Создание виртуального помощника
description: Создание бота Виртуальный помощник и навыков для использования в Microsoft Teams
localization_priority: Normal
ms.topic: how-to
keywords: команды виртуальных помощников-ботов
ms.openlocfilehash: 976dacbd8b0bef7a3158d5ff35c5c38d97707c63
ms.sourcegitcommit: e327c9766dfa05abb468cdc71319e3cba7c6c79f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/14/2021
ms.locfileid: "53428725"
---
# <a name="create-virtual-assistant"></a><span data-ttu-id="9c463-104">Создание виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="9c463-104">Create Virtual Assistant</span></span> 

<span data-ttu-id="9c463-105">Виртуальный помощник является шаблоном Microsoft с открытым исходным кодом, который позволяет создавать надежное решение для беседы, сохраняя полный контроль над пользовательским опытом, организационным брендингом и необходимыми данными.</span><span class="sxs-lookup"><span data-stu-id="9c463-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="9c463-106">Базовый [Виртуальный помощник](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) является основным строительным блоком, который объединяет технологии Майкрософт, необходимые для создания Виртуальный помощник, в том числе bot [Framework SDK,](https://github.com/microsoft/botframework-sdk) [Language Understanding (LUIS)](https://www.luis.ai/)и [QnA Maker.](https://www.qnamaker.ai/)</span><span class="sxs-lookup"><span data-stu-id="9c463-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), and [QnA Maker](https://www.qnamaker.ai/).</span></span> <span data-ttu-id="9c463-107">Он также объединяет основные возможности, включая регистрацию навыков, связанные учетные записи, основные беседы, чтобы предложить пользователям широкий спектр бесшовных взаимодействий и взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="9c463-107">It also brings together the essential capabilities including  skills registration, linked accounts, basic conversational intent to offer a range of seamless interactions and experiences to users.</span></span> <span data-ttu-id="9c463-108">Кроме того, возможности шаблона включают в себя богатые примеры многоиспользоваемых разговорных [навыков.](https://microsoft.github.io/botframework-solutions/overview/skills)</span><span class="sxs-lookup"><span data-stu-id="9c463-108">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="9c463-109">Отдельные навыки интегрированы в Виртуальный помощник, чтобы включить несколько сценариев.</span><span class="sxs-lookup"><span data-stu-id="9c463-109">Individual skills are integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="9c463-110">С помощью SDK Bot Framework навыки представлены в форме исходных кодов, что позволяет настраивать и расширять по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="9c463-110">Using the Bot Framework SDK, skills are presented in source code form, enabling you to customize and extend as required.</span></span> <span data-ttu-id="9c463-111">Дополнительные сведения о навыках Bot Framework см. в см. в поле ["Что такое навык Bot Framework".](https://microsoft.github.io/botframework-solutions/overview/skills/)</span><span class="sxs-lookup"><span data-stu-id="9c463-111">For more information on skills of Bot Framework, see [What is a Bot Framework skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="9c463-112">В этом документе вы можете Виртуальный помощник реализации для организаций, как создать Teams Виртуальный помощник, связанный пример, пример кода и ограничения Виртуальный помощник.</span><span class="sxs-lookup"><span data-stu-id="9c463-112">This document guides you on Virtual Assistant implementation considerations for organizations, how to create a Teams focused Virtual Assistant, related example, code sample, and limitations of Virtual Assistant.</span></span>
<span data-ttu-id="9c463-113">На следующем изображении отображается обзор виртуального помощника:</span><span class="sxs-lookup"><span data-stu-id="9c463-113">The following image displays the overview of virtual assistant:</span></span>

![Виртуальный помощник схема обзора](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="9c463-115">Действия текстовых сообщений отправляются в связанные навыки с помощью Виртуальный помощник с помощью модели [отправки.](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="9c463-115">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="9c463-116">Соображения реализации</span><span class="sxs-lookup"><span data-stu-id="9c463-116">Implementation considerations</span></span>

<span data-ttu-id="9c463-117">Решение о добавлении Виртуальный помощник содержит множество детерминантов и отличается для каждой организации.</span><span class="sxs-lookup"><span data-stu-id="9c463-117">The decision to add a Virtual Assistant includes many determinants and differs for each organization.</span></span> <span data-ttu-id="9c463-118">Вспомогательные факторы реализации Виртуальный помощник организации:</span><span class="sxs-lookup"><span data-stu-id="9c463-118">The supporting factors of a Virtual Assistant implementation for your organization are as follows:</span></span>

* <span data-ttu-id="9c463-119">Центральная группа управляет всеми впечатлениями сотрудников.</span><span class="sxs-lookup"><span data-stu-id="9c463-119">A central team manages all employee experiences.</span></span> <span data-ttu-id="9c463-120">Он имеет возможность создавать новые Виртуальный помощник и управлять обновлениями для основного опыта, включая добавление новых навыков.</span><span class="sxs-lookup"><span data-stu-id="9c463-120">It has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
* <span data-ttu-id="9c463-121">В бизнес-функциях существует несколько приложений, и ожидается, что в будущем их число будет расти.</span><span class="sxs-lookup"><span data-stu-id="9c463-121">Multiple applications exist across business functions and the number is expected to grow in the future.</span></span>
* <span data-ttu-id="9c463-122">Существующие приложения настраиваются, принадлежат организации и преобразуются в навыки для Виртуальный помощник.</span><span class="sxs-lookup"><span data-stu-id="9c463-122">Existing applications are customizable, owned by the organization, and are converted into skills for a Virtual Assistant.</span></span>
* <span data-ttu-id="9c463-123">Центральная группа по опытом сотрудников может влиять на настройки существующих приложений.</span><span class="sxs-lookup"><span data-stu-id="9c463-123">The central employee experiences team is able to influence customizations to existing apps.</span></span> <span data-ttu-id="9c463-124">Она также предоставляет необходимые рекомендации по интеграции существующих приложений в качестве навыков в Виртуальный помощник опыте.</span><span class="sxs-lookup"><span data-stu-id="9c463-124">It also provides necessary guidance for integrating existing applications as skills in Virtual Assistant experience.</span></span>

<span data-ttu-id="9c463-125">На следующем изображении отображаются бизнес-функции Виртуальный помощник:</span><span class="sxs-lookup"><span data-stu-id="9c463-125">The following image displays the business functions of Virtual Assistant:</span></span> 

![Центральная команда поддерживает помощника, а группы бизнес-функций способствуют навыкам](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="9c463-127">Создание Teams, ориентированных на Виртуальный помощник</span><span class="sxs-lookup"><span data-stu-id="9c463-127">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="9c463-128">Корпорация Майкрософт опубликовала шаблон [Visual Studio для](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) создания виртуальных помощников и навыков.</span><span class="sxs-lookup"><span data-stu-id="9c463-128">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="9c463-129">С помощью Visual Studio шаблона можно создать Виртуальный помощник, основанный на тексте, с поддержкой ограниченных богатых карт с действиями.</span><span class="sxs-lookup"><span data-stu-id="9c463-129">With the Visual Studio template, you can create a Virtual Assistant, powered by a text based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="9c463-130">Мы усовершенствовали базовый Visual Studio, чтобы включить Microsoft Teams платформы и Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="9c463-130">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="9c463-131">Некоторые возможности включают поддержку богатых адаптивных карт, модулей задач, групп или групповых чатов и расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9c463-131">A few of the capabilities include support for rich Adaptive Cards, task modules, teams or group chats, and messaging extensions.</span></span> <span data-ttu-id="9c463-132">Дополнительные сведения о продлении Виртуальный помощник до Microsoft Teams см. в [учебнике: Расширение Виртуальный помощник до Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span><span class="sxs-lookup"><span data-stu-id="9c463-132">For more information on extending Virtual Assistant to Microsoft Teams, see [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>    
<span data-ttu-id="9c463-133">На следующем изображении отображается диаграмма высокого уровня решения Виртуальный помощник:</span><span class="sxs-lookup"><span data-stu-id="9c463-133">The following image displays the high level diagram of a Virtual Assistant solution:</span></span>

![Схема решения Виртуальный помощник высокого уровня](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="9c463-135">Добавьте адаптивные карты в Виртуальный помощник</span><span class="sxs-lookup"><span data-stu-id="9c463-135">Add Adaptive Cards to your Virtual Assistant</span></span>

<span data-ttu-id="9c463-136">Чтобы правильно отправлять запросы, Виртуальный помощник должны определить правильную модель LUIS и соответствующие навыки, связанные с ней.</span><span class="sxs-lookup"><span data-stu-id="9c463-136">To dispatch requests properly, your Virtual Assistant must identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="9c463-137">Однако механизм отправки не может использоваться для действий с картами, так как модель LUIS, связанная с навыком, обучена текстам действий карт.</span><span class="sxs-lookup"><span data-stu-id="9c463-137">However, the dispatching mechanism cannot be used for card action activities as the LUIS model associated with a skill, is trained for card action texts.</span></span> <span data-ttu-id="9c463-138">Тексты действий карты являются фиксированными, заранее определенными ключевыми словами и не комментируются пользователем.</span><span class="sxs-lookup"><span data-stu-id="9c463-138">The card action texts are fixed, pre-defined keywords, and not commented from a user.</span></span>

<span data-ttu-id="9c463-139">Этот недостаток решается путем встраив сведения о навыках в полезной нагрузке действия карты.</span><span class="sxs-lookup"><span data-stu-id="9c463-139">This drawback is resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="9c463-140">Каждый навык должен `skillId` встраить  `value` в область действий карт.</span><span class="sxs-lookup"><span data-stu-id="9c463-140">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="9c463-141">Необходимо убедиться, что каждое действие карты несет соответствующие сведения о навыках, и Виртуальный помощник использовать эту информацию для отправки.</span><span class="sxs-lookup"><span data-stu-id="9c463-141">You must ensure that each card action activity carries the relevant skill information, and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="9c463-142">Необходимо предоставить в конструкторе сведения о навыках, которые всегда присутствуют `skillId` в действиях карт.</span><span class="sxs-lookup"><span data-stu-id="9c463-142">You must provide `skillId` in the constructor to ensure that the skill information is always present in card actions.</span></span>
<span data-ttu-id="9c463-143">Пример кода действия карты показан в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="9c463-143">A card action data sample code is shown in the following section:</span></span>
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

<span data-ttu-id="9c463-144">Далее `SkillCardActionData` класс в Виртуальный помощник вводится для извлечения из полезной нагрузки действия `skillId` карты.</span><span class="sxs-lookup"><span data-stu-id="9c463-144">Next, `SkillCardActionData` class in the Virtual Assistant template is introduces to extract `skillId` from the card action payload.</span></span>
<span data-ttu-id="9c463-145">Фрагмент кода, извлеченный из полезной нагрузки действия карты, показан  `skillId` в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="9c463-145">A code snippet to extract  `skillId` from card action payload is shown in the following section:</span></span>

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

<span data-ttu-id="9c463-146">Реализация используется методом расширения в [классе Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)</span><span class="sxs-lookup"><span data-stu-id="9c463-146">The implementation is done by an extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>
<span data-ttu-id="9c463-147">Фрагмент кода, извлеченный  `skillId` из данных действий карты, показан в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="9c463-147">A code snippet to extract  `skillId` from card action data is shown in the following section:</span></span>

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

### <a name="handle-interruptions"></a><span data-ttu-id="9c463-148">Обработка перерывов</span><span class="sxs-lookup"><span data-stu-id="9c463-148">Handle interruptions</span></span>

<span data-ttu-id="9c463-149">Виртуальный помощник может обрабатывать перерывы в случаях, когда пользователь пытается вызвать навык, а другой навык в настоящее время активен.</span><span class="sxs-lookup"><span data-stu-id="9c463-149">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="9c463-150">`TeamsSkillDialog`, и `TeamsSwitchSkillDialog` представлены на основе [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) Bot Framework и [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs).</span><span class="sxs-lookup"><span data-stu-id="9c463-150">`TeamsSkillDialog`, and `TeamsSwitchSkillDialog`are introduced based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs).</span></span> <span data-ttu-id="9c463-151">Они позволяют пользователям переключать навыки работы с действиями карт.</span><span class="sxs-lookup"><span data-stu-id="9c463-151">They enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="9c463-152">Для обработки этого запроса Виртуальный помощник пользователю с сообщением подтверждения для переключения навыков:</span><span class="sxs-lookup"><span data-stu-id="9c463-152">To handle this request, the Virtual Assistant prompts the user with a confirmation message to switch skills:</span></span>

![Запрос подтверждения при переходе на новый навык](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a><span data-ttu-id="9c463-154">Обработка запросов модулей задач</span><span class="sxs-lookup"><span data-stu-id="9c463-154">Handle task module requests</span></span>

<span data-ttu-id="9c463-155">Чтобы добавить возможности модуля задач в Виртуальный помощник, в обработник Виртуальный помощник действий включены два дополнительных метода: `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="9c463-155">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="9c463-156">Эти методы прослушивают действия, связанные с модулем задач, Виртуальный помощник, определяют навыки, связанные с запросом, и переназначяют запрос в указанный навык.</span><span class="sxs-lookup"><span data-stu-id="9c463-156">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="9c463-157">Переадтранслировать запросы можно с помощью [метода SkillHttpClient.](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) `PostActivityAsync`</span><span class="sxs-lookup"><span data-stu-id="9c463-157">Request forwarding is done through the [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` method.</span></span> <span data-ttu-id="9c463-158">Он возвращает ответ, `InvokeResponse` как который разобрано и преобразовано в `TaskModuleResponse` .</span><span class="sxs-lookup"><span data-stu-id="9c463-158">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>


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

<span data-ttu-id="9c463-159">Аналогичный подход следует для отправки действий по картам и ответов модулей задач.</span><span class="sxs-lookup"><span data-stu-id="9c463-159">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="9c463-160">Модуль задач для получения и отправки данных действий обновляется, чтобы включить `skillId` .</span><span class="sxs-lookup"><span data-stu-id="9c463-160">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="9c463-161">Метод расширения действий извлекает из полезной нагрузки, которая содержит сведения о навыке, `GetSkillId` `skillId` который необходимо вызвать.</span><span class="sxs-lookup"><span data-stu-id="9c463-161">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="9c463-162">Фрагмент кода и методы `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` даются в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="9c463-162">The code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods are given in the following section:</span></span>

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

            return invokeResponse.GetTaskModuleResponse();
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

<span data-ttu-id="9c463-163">Кроме того, необходимо включить все домены навыков в разделе Виртуальный помощник манифеста, чтобы модули задач, вызываемые с помощью отрисовки навыков `validDomains` должным образом.</span><span class="sxs-lookup"><span data-stu-id="9c463-163">Additionally, you must include all skill domains in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked through a skill render properly.</span></span>

### <a name="handle-collaborative-app-scopes"></a><span data-ttu-id="9c463-164">Обработка областей совместных приложений</span><span class="sxs-lookup"><span data-stu-id="9c463-164">Handle collaborative app scopes</span></span>

<span data-ttu-id="9c463-165">Teams приложения могут существовать в нескольких сферах, включая чат 1:1, групповой чат и каналы.</span><span class="sxs-lookup"><span data-stu-id="9c463-165">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="9c463-166">Основной шаблон Виртуальный помощник предназначен для чатов 1:1.</span><span class="sxs-lookup"><span data-stu-id="9c463-166">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="9c463-167">В рамках пользовательского интерфейса Виртуальный помощник пользователей для имени и поддерживает состояние пользователя.</span><span class="sxs-lookup"><span data-stu-id="9c463-167">As part of the onboarding experience Virtual Assistant prompts users for name and maintains user state.</span></span> <span data-ttu-id="9c463-168">Так как этот опыт в составе не подходит для групповых чатов или областей каналов, он был удален.</span><span class="sxs-lookup"><span data-stu-id="9c463-168">Since that onboarding experience is not suited for group chat or channel scopes it has been removed.</span></span>

<span data-ttu-id="9c463-169">Навыки должны обрабатывать действия в нескольких сферах, например в чате 1:1, групповом чате и разговоре по каналу.</span><span class="sxs-lookup"><span data-stu-id="9c463-169">Skills should handle activities in multiple scopes, such as 1:1 chat, group chat, and channel conversation.</span></span> <span data-ttu-id="9c463-170">Если какие-либо из этих областей не поддерживаются, навыки должны отвечать соответствующим сообщением.</span><span class="sxs-lookup"><span data-stu-id="9c463-170">If any of these scopes are not supported, skills must respond with an appropriate message.</span></span>

<span data-ttu-id="9c463-171">В Виртуальный помощник добавлены следующие функции обработки:</span><span class="sxs-lookup"><span data-stu-id="9c463-171">The following  processing functions have been added to Virtual Assistant core:</span></span>

* <span data-ttu-id="9c463-172">Виртуальный помощник можно вызывать без текстовых сообщений из группового чата или канала.</span><span class="sxs-lookup"><span data-stu-id="9c463-172">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
* <span data-ttu-id="9c463-173">Артикуляция очищается перед отправкой сообщения в модуль отправки.</span><span class="sxs-lookup"><span data-stu-id="9c463-173">Articulations are cleaned before sending the message to the dispatch module.</span></span> <span data-ttu-id="9c463-174">Например, удалите необходимые @mention бота.</span><span class="sxs-lookup"><span data-stu-id="9c463-174">For example, remove the necessary @mention of the bot.</span></span>

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

### <a name="handle-messaging-extensions"></a><span data-ttu-id="9c463-175">Обработка расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9c463-175">Handle messaging extensions</span></span>

<span data-ttu-id="9c463-176">Команды для расширения обмена сообщениями объявляются в файле манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="9c463-176">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="9c463-177">Пользовательский интерфейс расширения обмена сообщениями на питание от этих команд.</span><span class="sxs-lookup"><span data-stu-id="9c463-177">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="9c463-178">Чтобы Виртуальный помощник команду расширения обмена сообщениями в качестве присоединенного навыка, манифест Виртуальный помощник должен содержать эти команды.</span><span class="sxs-lookup"><span data-stu-id="9c463-178">For a Virtual Assistant to power a messaging extension command as an attached skill, a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="9c463-179">Вы должны добавить команды из манифеста индивидуального мастерства в манифест Виртуальный помощник в манифесте.</span><span class="sxs-lookup"><span data-stu-id="9c463-179">You must add the commands from an individual skill's manifest to the Virtual Assistant's manifest.</span></span> <span data-ttu-id="9c463-180">Командный ID предоставляет сведения о связанном навыке, привнося ID приложения навыка через сепаратор. `:`</span><span class="sxs-lookup"><span data-stu-id="9c463-180">The command ID provides information about an associated skill by appending the skill's app ID through a separator `:`.</span></span>

<span data-ttu-id="9c463-181">Фрагмент из файла манифеста навыка показан в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="9c463-181">The snippet from a skill's manifest file is shown in the following section:</span></span>

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

<span data-ttu-id="9c463-182">Соответствующий фрагмент кода Виртуальный помощник манифеста показан в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="9c463-182">The corresponding Virtual Assistant manifest file code snippet is shown in the following section:</span></span>

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

<span data-ttu-id="9c463-183">После вызова команд пользователем Виртуальный помощник соответствующий навык путем разбора ИД команды, обновления действия путем удаления дополнительного суффикса из командного ИД и его переадэффинга в соответствующий `:<skill_id>` навык.</span><span class="sxs-lookup"><span data-stu-id="9c463-183">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix `:<skill_id>` from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="9c463-184">Код для навыка не должен обрабатывать дополнительный суффикс.</span><span class="sxs-lookup"><span data-stu-id="9c463-184">The code for a skill doesnot need to handle the extra suffix.</span></span> <span data-ttu-id="9c463-185">Таким образом, можно избежать конфликтов между командными ИД между навыками.</span><span class="sxs-lookup"><span data-stu-id="9c463-185">Thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="9c463-186">С помощью этого подхода все команды поиска и действий навыка во всех контекстах, таких как **compose,**  **commandBox** и сообщения, Виртуальный помощник.</span><span class="sxs-lookup"><span data-stu-id="9c463-186">With this approach, all the search and action commands of a skill within all contexts, such as **compose**, **commandBox**, and **message** are powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="9c463-187">Некоторые действия по расширению обмена сообщениями не включают командный ID.</span><span class="sxs-lookup"><span data-stu-id="9c463-187">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="9c463-188">Например, `composeExtension/selectItem` содержит только значение действия касания.</span><span class="sxs-lookup"><span data-stu-id="9c463-188">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="9c463-189">Чтобы определить связанный навык, при формировании ответа для каждого элемента присоединяется к каждой карте `skillId` `OnTeamsMessagingExtensionQueryAsync` элемента.</span><span class="sxs-lookup"><span data-stu-id="9c463-189">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="9c463-190">Это похоже на подход к [добавлению адаптивных карт](#add-adaptive-cards-to-your-virtual-assistant)в Виртуальный помощник.</span><span class="sxs-lookup"><span data-stu-id="9c463-190">This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example"></a><span data-ttu-id="9c463-191">Пример</span><span class="sxs-lookup"><span data-stu-id="9c463-191">Example</span></span>

<span data-ttu-id="9c463-192">В следующем примере показано, как преобразовать шаблон приложения Book-a-room в навык Виртуальный помощник: Book-a-room — это Microsoft Teams, который позволяет пользователям быстро находить и резервировать зал для собраний на 30, 60 или 90 минут начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="9c463-192">The following example shows how to convert the Book-a-room app template to a Virtual Assistant skill: Book-a-room is a Microsoft Teams that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="9c463-193">Время по умолчанию — 30 минут.</span><span class="sxs-lookup"><span data-stu-id="9c463-193">The default time is 30 minutes.</span></span> <span data-ttu-id="9c463-194">Область бота Book-a-room для личных или 1:1 бесед.</span><span class="sxs-lookup"><span data-stu-id="9c463-194">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="9c463-195">На следующем изображении отображается Виртуальный помощник с **книгой навыков** комнаты:</span><span class="sxs-lookup"><span data-stu-id="9c463-195">The following image displays a Virtual Assistant with a **book a room** skill:</span></span>

![Виртуальный помощник с навыком "книга комнаты"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="9c463-197">Ниже представлены изменения дельты, введенные для преобразования его в навык, присоединенный к Виртуальный помощник.</span><span class="sxs-lookup"><span data-stu-id="9c463-197">Followings are the delta changes introduced to convert it to a skill which is attached to a Virtual Assistant.</span></span> <span data-ttu-id="9c463-198">Аналогичные рекомендации следуют для преобразования любого существующего бота v4 в навык.</span><span class="sxs-lookup"><span data-stu-id="9c463-198">Similar guidelines are followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="9c463-199">Манифест мастерства</span><span class="sxs-lookup"><span data-stu-id="9c463-199">Skill manifest</span></span>

<span data-ttu-id="9c463-200">Манифест навыков — это файл JSON, который предоставляет конечную точку обмена сообщениями, ID, имя и другие соответствующие метаданные.</span><span class="sxs-lookup"><span data-stu-id="9c463-200">A skill manifest is a JSON file that exposes a skill's messaging endpoint, ID, name, and other relevant metadata.</span></span> <span data-ttu-id="9c463-201">Этот манифест отличается от манифеста, используемого для загрузки приложения в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9c463-201">This manifest is different than the manifest used for sideloading an app in Microsoft Teams.</span></span> <span data-ttu-id="9c463-202">Для Виртуальный помощник требуется путь к этому файлу в качестве ввода, чтобы прикрепить навык.</span><span class="sxs-lookup"><span data-stu-id="9c463-202">A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="9c463-203">В папку wwwroot бота добавлен следующий манифест.</span><span class="sxs-lookup"><span data-stu-id="9c463-203">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="9c463-204">ИНТЕГРАЦИЯ LUIS</span><span class="sxs-lookup"><span data-stu-id="9c463-204">LUIS Integration</span></span>

<span data-ttu-id="9c463-205">Виртуальный помощник модель отправки построена на основе присоединенных моделей LUIS навыков.</span><span class="sxs-lookup"><span data-stu-id="9c463-205">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="9c463-206">Модель отправки определяет намерения для каждой текстовой активности и находит навыки, связанные с ней.</span><span class="sxs-lookup"><span data-stu-id="9c463-206">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="9c463-207">Виртуальный помощник в формате в формате для ввода при присоединении навыка требуется модель `.lu` LUIS.</span><span class="sxs-lookup"><span data-stu-id="9c463-207">Virtual Assistant requires skill's LUIS model in `.lu` format as an input while attaching a skill.</span></span> <span data-ttu-id="9c463-208">LUIS json преобразуется в `.lu` формат с помощью средства botframework-cli.</span><span class="sxs-lookup"><span data-stu-id="9c463-208">LUIS json is converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="9c463-209">Бот Book-a-room имеет две основные команды для пользователей:</span><span class="sxs-lookup"><span data-stu-id="9c463-209">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="9c463-210">Мы создали модель LUIS, понимая эти две команды.</span><span class="sxs-lookup"><span data-stu-id="9c463-210">We have built a LUIS model by understanding these two commands.</span></span> <span data-ttu-id="9c463-211">Соответствующие секреты должны быть заполнены `cognitivemodels.json` в .</span><span class="sxs-lookup"><span data-stu-id="9c463-211">Corresponding secrets must be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="9c463-212">Соответствующий файл LUIS JSON находится [здесь](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json).</span><span class="sxs-lookup"><span data-stu-id="9c463-212">The corresponding LUIS JSON file is found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json).</span></span>
<span data-ttu-id="9c463-213">Соответствующий `.lu` файл показан в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="9c463-213">The corresponding `.lu` file is shown in the following section:</span></span>

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

<span data-ttu-id="9c463-214">С помощью этого подхода любая команда, выдаемая пользователем для Виртуальный помощник или идентифицирована как команда, связанная с ботом, и передается `book room` `manage favorites` на этот `Book-a-room` навык.</span><span class="sxs-lookup"><span data-stu-id="9c463-214">With this approach, any command issued by a user to Virtual Assistant related to `book room` or `manage favorites` are identified as a command associated with `Book-a-room` bot and is forwarded to this skill.</span></span>
<span data-ttu-id="9c463-215">С другой стороны, боту необходимо использовать модель LUIS, чтобы понять эти команды, если `Book-a-room room` они не введите полный текст.</span><span class="sxs-lookup"><span data-stu-id="9c463-215">On the other hand, `Book-a-room room` bot needs to use LUIS model to understand these commands if they are not typed full.</span></span> <span data-ttu-id="9c463-216">Пример: `I want to manage my favorite rooms`.</span><span class="sxs-lookup"><span data-stu-id="9c463-216">For example: `I want to manage my favorite rooms`.</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="9c463-217">Поддержка multi-Language</span><span class="sxs-lookup"><span data-stu-id="9c463-217">Multi-Language support</span></span>

<span data-ttu-id="9c463-218">В качестве примера создается модель LUIS с только английской культурой.</span><span class="sxs-lookup"><span data-stu-id="9c463-218">As an example, a LUIS model with only English culture is created.</span></span> <span data-ttu-id="9c463-219">Можно создать модели LUIS, соответствующие другим языкам, и добавить запись в `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="9c463-219">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="9c463-220">Параллельно добавьте соответствующий `.lu` файл в путь LuisFolder.</span><span class="sxs-lookup"><span data-stu-id="9c463-220">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="9c463-221">Структура папок должна быть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c463-221">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="9c463-222">Чтобы изменить `languages` параметр, обнови команду botskills следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c463-222">To modify `languages` parameter, update botskills command as follows:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="9c463-223">Виртуальный помощник используется `SetLocaleMiddleware` для определения текущего локального запроса и вызова соответствующей модели отправки.</span><span class="sxs-lookup"><span data-stu-id="9c463-223">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="9c463-224">Действие базы ботов имеет поле locale, которое используется этим средним программным обеспечением.</span><span class="sxs-lookup"><span data-stu-id="9c463-224">Bot framework activity has locale field which is used by this middleware.</span></span> <span data-ttu-id="9c463-225">Вы можете использовать то же самое для вашего мастерства, а также.</span><span class="sxs-lookup"><span data-stu-id="9c463-225">You can use the same for your skill as well.</span></span> <span data-ttu-id="9c463-226">Бот book-a-room не использует это среднее повеять и вместо этого получает локализовку из сущности [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)клиентской базы Bot framework.</span><span class="sxs-lookup"><span data-stu-id="9c463-226">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="9c463-227">Проверка утверждений</span><span class="sxs-lookup"><span data-stu-id="9c463-227">Claim validation</span></span>

<span data-ttu-id="9c463-228">Мы добавили [claimsValidator, чтобы](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) ограничить вызовы навыками.</span><span class="sxs-lookup"><span data-stu-id="9c463-228">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="9c463-229">Чтобы разрешить Виртуальный помощник вызов этого навыка, заполняйте массив с помощью этого Виртуальный помощник `AllowedCallers` `appsettings` ID приложения.</span><span class="sxs-lookup"><span data-stu-id="9c463-229">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="9c463-230">Массив разрешенных вызовов может ограничить доступ потребителей к навыкам.</span><span class="sxs-lookup"><span data-stu-id="9c463-230">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="9c463-231">Добавьте одну запись `*` в этот массив, чтобы принимать вызовы от любого потребителя навыков.</span><span class="sxs-lookup"><span data-stu-id="9c463-231">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```

<span data-ttu-id="9c463-232">Дополнительные сведения о добавлении проверки утверждений в навык см. в добавлении проверки [утверждений к мастерству.](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="9c463-232">For more information on adding claims validation to a skill, see [add claims validation to skill](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span></span>

### <a name="limitation-of-card-refresh"></a><span data-ttu-id="9c463-233">Ограничение обновления карты</span><span class="sxs-lookup"><span data-stu-id="9c463-233">Limitation of card refresh</span></span> 

<span data-ttu-id="9c463-234">Обновление активности, например обновления карт, пока не поддерживается Виртуальный помощник[(проблема github).](https://github.com/microsoft/botbuilder-dotnet/issues/3686)</span><span class="sxs-lookup"><span data-stu-id="9c463-234">Updating activity, such as card refresh is not supported yet through Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="9c463-235">Таким образом, мы заменили все вызовы обновления карт `UpdateActivityAsync` на размещение новых вызовов `SendActivityAsync` карт.</span><span class="sxs-lookup"><span data-stu-id="9c463-235">Hence, we have replaced all card refresh calls `UpdateActivityAsync` with posting new card calls `SendActivityAsync`.</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="9c463-236">Действия карты и потоки модулей задач</span><span class="sxs-lookup"><span data-stu-id="9c463-236">Card actions and task module flows</span></span>

<span data-ttu-id="9c463-237">Чтобы перенаставлять действия карты или действия модуля задач в связанные навыки, навык должен встраить `skillId` в него.</span><span class="sxs-lookup"><span data-stu-id="9c463-237">To forward card action or task module activities to an associated skill, the skill must embed `skillId` to it.</span></span>
<span data-ttu-id="9c463-238">`Book-a-room` Действие бот-карты, извлечение и отправка полезной нагрузки модуля задач изменены, чтобы содержать `skillId` в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="9c463-238">`Book-a-room` bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="9c463-239">Дополнительные сведения можно [получить в этом](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) разделе из этой документации.</span><span class="sxs-lookup"><span data-stu-id="9c463-239">For more information refer [this](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="9c463-240">Обработка действий из группового чата или области канала</span><span class="sxs-lookup"><span data-stu-id="9c463-240">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="9c463-241">`Book-a-room bot` предназначена только для частных чатов, например личных или 1:1.</span><span class="sxs-lookup"><span data-stu-id="9c463-241">`Book-a-room bot` is designed for private chats, such as personal or 1:1 scope only.</span></span> <span data-ttu-id="9c463-242">Так как мы Виртуальный помощник для поддержки групповых чатов и областей каналов, Виртуальный помощник должны вызываться из областей канала, поэтому бот должен получать действия для той же `Book-a-room` области.</span><span class="sxs-lookup"><span data-stu-id="9c463-242">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant must be invoked from the channel scopes and thus, `Book-a-room` bot must get activities for the same scope.</span></span> <span data-ttu-id="9c463-243">Поэтому `Book-a-room` бот настраивается для обработки этих действий.</span><span class="sxs-lookup"><span data-stu-id="9c463-243">Hence `Book-a-room`bot is customized to handle those activities.</span></span> <span data-ttu-id="9c463-244">Вы можете найти способы `OnMessageActivityAsync` проверки методов `Book-a-room` обработки действий бота.</span><span class="sxs-lookup"><span data-stu-id="9c463-244">You can find the check in `OnMessageActivityAsync` methods of `Book-a-room` bot's activity handler.</span></span>

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

<span data-ttu-id="9c463-245">Вы также можете использовать существующие навыки из [репозитория Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) или создать новый навык с нуля.</span><span class="sxs-lookup"><span data-stu-id="9c463-245">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="9c463-246">Для создания нового навыка см. [в учебниках по созданию нового навыка.](https://microsoft.github.io/botframework-solutions/overview/skills/)</span><span class="sxs-lookup"><span data-stu-id="9c463-246">For creating a new skill, see [tutorials to create a new skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="9c463-247">В Виртуальный помощник документации по архитектуре и навыкам см. Виртуальный помощник[и архитектуру навыков.](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="9c463-247">For Virtual Assistant and skills architecture documentation, see[Virtual Assistant and skills architecture](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).</span></span>  

## <a name="limitations-of-virtual-assistant"></a><span data-ttu-id="9c463-248">Ограничения Виртуальный помощник</span><span class="sxs-lookup"><span data-stu-id="9c463-248">Limitations of Virtual Assistant</span></span> 

* <span data-ttu-id="9c463-249">**EndOfConversation.** Навык должен отправить действие по завершении `endOfConversation` беседы.</span><span class="sxs-lookup"><span data-stu-id="9c463-249">**EndOfConversation**: A skill must send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="9c463-250">На основе этого действия Виртуальный помощник контекст с этим навыком и возвращается Виртуальный помощник корневого контекста.</span><span class="sxs-lookup"><span data-stu-id="9c463-250">Based on the activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's root context.</span></span> <span data-ttu-id="9c463-251">Для бота Book-a-room нет четкого состояния, в котором беседа завершена.</span><span class="sxs-lookup"><span data-stu-id="9c463-251">For Book-a-room bot, there is no clear state where conversation is ended.</span></span> <span data-ttu-id="9c463-252">Поэтому мы не отослали от бота, и когда пользователь хочет вернуться к корневому контексту, он может просто сделать `endOfConversation` `Book-a-room` это по `start over` команде.</span><span class="sxs-lookup"><span data-stu-id="9c463-252">Hence we have not sent `endOfConversation` from `Book-a-room` bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>  
* <span data-ttu-id="9c463-253">**Обновление карты.** Обновление карты еще не поддерживается Виртуальный помощник.</span><span class="sxs-lookup"><span data-stu-id="9c463-253">**Card refresh**: Card refresh is not yet supported through Virtual Assistant.</span></span>  
* <span data-ttu-id="9c463-254">**Расширения обмена сообщениями:**</span><span class="sxs-lookup"><span data-stu-id="9c463-254">**Messaging extensions**:</span></span>
  * <span data-ttu-id="9c463-255">В настоящее время Виртуальный помощник может поддерживать не более десяти команд для расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9c463-255">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  * <span data-ttu-id="9c463-256">Конфигурация расширений обмена сообщениями не касается отдельных команд, а всего расширения.</span><span class="sxs-lookup"><span data-stu-id="9c463-256">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="9c463-257">Это ограничивает конфигурацию для каждого отдельного навыка через Виртуальный помощник.</span><span class="sxs-lookup"><span data-stu-id="9c463-257">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  * <span data-ttu-id="9c463-258">Командные ИД расширений обмена сообщениями имеют максимальную длину [64](../resources/schema/manifest-schema.md#composeextensions) символа, а для встраиванию сведений о навыках используются 37 символов.</span><span class="sxs-lookup"><span data-stu-id="9c463-258">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters are used for embedding skill information.</span></span> <span data-ttu-id="9c463-259">Таким образом, обновленные ограничения для командного ID ограничены 27 символами.</span><span class="sxs-lookup"><span data-stu-id="9c463-259">Thus, updated constraints for command ID are limited to 27 characters.</span></span>

<span data-ttu-id="9c463-260">Вы также можете использовать существующие навыки из [репозитория Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) или создать новый навык с нуля.</span><span class="sxs-lookup"><span data-stu-id="9c463-260">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="9c463-261">Учебники для более позднего можно найти [здесь](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="9c463-261">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="9c463-262">Обратитесь к [документации](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) по архитектуре Виртуальный помощник и навыкам.</span><span class="sxs-lookup"><span data-stu-id="9c463-262">Please refer to [documentation](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) for Virtual Assistant and skills architecture.</span></span>

## <a name="code-sample"></a><span data-ttu-id="9c463-263">Пример кода</span><span class="sxs-lookup"><span data-stu-id="9c463-263">Code sample</span></span>

| <span data-ttu-id="9c463-264">**Название примера**</span><span class="sxs-lookup"><span data-stu-id="9c463-264">**Sample name**</span></span> | <span data-ttu-id="9c463-265">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9c463-265">**Description**</span></span> | <span data-ttu-id="9c463-266">**C#**  **.NET**</span><span class="sxs-lookup"><span data-stu-id="9c463-266">**C#**  **.NET**</span></span> |
|----------|-----------------|---------------------------|
| <span data-ttu-id="9c463-267">Обновленный шаблон визуальной студии</span><span class="sxs-lookup"><span data-stu-id="9c463-267">Updated visual studio template</span></span> | <span data-ttu-id="9c463-268">Настраиваемый шаблон для поддержки возможностей групп.</span><span class="sxs-lookup"><span data-stu-id="9c463-268">Customized template to support teams capabilities.</span></span> | [<span data-ttu-id="9c463-269">Просмотр</span><span class="sxs-lookup"><span data-stu-id="9c463-269">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| <span data-ttu-id="9c463-270">Код навыков бота book-a-room</span><span class="sxs-lookup"><span data-stu-id="9c463-270">Book-a-room bot skill code</span></span> | <span data-ttu-id="9c463-271">Позволяет быстро найти и заказать комнату собраний на время.</span><span class="sxs-lookup"><span data-stu-id="9c463-271">Lets you quickly find and book a meeting room on the go.</span></span> | [<span data-ttu-id="9c463-272">Просмотр</span><span class="sxs-lookup"><span data-stu-id="9c463-272">View</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |


## <a name="see-also"></a><span data-ttu-id="9c463-273">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9c463-273">See also</span></span>

* [<span data-ttu-id="9c463-274">Интеграция веб-приложений</span><span class="sxs-lookup"><span data-stu-id="9c463-274">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
* [<span data-ttu-id="9c463-275">Book-a-room</span><span class="sxs-lookup"><span data-stu-id="9c463-275">Book-a-room</span></span>](app-templates.md#book-a-room)
* [<span data-ttu-id="9c463-276">Microsoft Teams бот</span><span class="sxs-lookup"><span data-stu-id="9c463-276">Microsoft Teams bot</span></span>](../bots/what-are-bots.md)
