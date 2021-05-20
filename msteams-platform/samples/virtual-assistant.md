---
title: Создание виртуального помощника
description: Как создать виртуальный помощник бота и навыки для использования в Microsoft Teams
localization_priority: Normal
ms.topic: how-to
keywords: команды виртуальных помощников ботов
ms.openlocfilehash: 072d9cb5742cd39101587cad32e3048bd36cc1d8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566875"
---
# <a name="create-virtual-assistant"></a><span data-ttu-id="926d8-104">Создание виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="926d8-104">Create Virtual Assistant</span></span> 

<span data-ttu-id="926d8-105">Virtual Assistant — это шаблон с открытым исходным кодом корпорации Майкрософт, который позволяет создавать надежное решение для хранения, сохраняя при этом полный контроль над пользовательским опытом, организационным брендингом и необходимыми данными.</span><span class="sxs-lookup"><span data-stu-id="926d8-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="926d8-106">Основной [шаблон Virtual Assistant является](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) основным строительным блоком, который объединяет технологии Microsoft, необходимые для создания виртуального помощника, [включая Bot Framework SDK,](https://github.com/microsoft/botframework-sdk) [Language Understanding (LUIS)](https://www.luis.ai/) [и йnA Maker.](https://www.qnamaker.ai/)</span><span class="sxs-lookup"><span data-stu-id="926d8-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), and [QnA Maker](https://www.qnamaker.ai/).</span></span> <span data-ttu-id="926d8-107">Он также объединяет основные возможности, включая регистрацию навыков, связанные учетные записи, основные разговорные намерения предложить широкий спектр бесшовных взаимодействий и опыта для пользователей.</span><span class="sxs-lookup"><span data-stu-id="926d8-107">It also brings together the essential capabilities including  skills registration, linked accounts, basic conversational intent to offer a range of seamless interactions and experiences to users.</span></span> <span data-ttu-id="926d8-108">Кроме того, возможности шаблона включают богатые примеры многоразовых разговорных [навыков.](https://microsoft.github.io/botframework-solutions/overview/skills)</span><span class="sxs-lookup"><span data-stu-id="926d8-108">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="926d8-109">Индивидуальные навыки интегрированы в решение Virtual Assistant для нескольких сценариев.</span><span class="sxs-lookup"><span data-stu-id="926d8-109">Individual skills are integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="926d8-110">Используя Bot Framework SDK, навыки представлены в форме исходных кодов, что позволяет настроить и расширить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="926d8-110">Using the Bot Framework SDK, skills are presented in source code form, enabling you to customize and extend as required.</span></span> <span data-ttu-id="926d8-111">Для получения дополнительной информации о навыках Bot Framework, [см.](https://microsoft.github.io/botframework-solutions/overview/skills/)</span><span class="sxs-lookup"><span data-stu-id="926d8-111">For more information on skills of Bot Framework, see [What is a Bot Framework skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="926d8-112">Этот документ поможет вам в реализации виртуального помощника для организаций, как создать Teams виртуальный помощник, связанный пример, образец кода и ограничения виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="926d8-112">This document guides you on Virtual Assistant implementation considerations for organizations, how to create a Teams focused Virtual Assistant, related example, code sample, and limitations of Virtual Assistant.</span></span>
<span data-ttu-id="926d8-113">Следующее изображение отображает обзор виртуального помощника:</span><span class="sxs-lookup"><span data-stu-id="926d8-113">The following image displays the overview of virtual assistant:</span></span>

![Диаграмма обзора виртуального помощника](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="926d8-115">Действия текстовых сообщений направляются к связанным навыкам ядром Virtual Assistant с помощью [модели отправки.](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="926d8-115">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="926d8-116">Соображения осуществления</span><span class="sxs-lookup"><span data-stu-id="926d8-116">Implementation considerations</span></span>

<span data-ttu-id="926d8-117">Решение о добавление виртуального помощника включает в себя множество детерминантов и отличается для каждой организации.</span><span class="sxs-lookup"><span data-stu-id="926d8-117">The decision to add a Virtual Assistant includes many determinants and differs for each organization.</span></span> <span data-ttu-id="926d8-118">Поддерживающие факторы реализации виртуального помощника для вашей организации следующие:</span><span class="sxs-lookup"><span data-stu-id="926d8-118">The supporting factors of a Virtual Assistant implementation for your organization are as follows:</span></span>

* <span data-ttu-id="926d8-119">Центральная команда управляет всем опытом сотрудников.</span><span class="sxs-lookup"><span data-stu-id="926d8-119">A central team manages all employee experiences.</span></span> <span data-ttu-id="926d8-120">Он имеет возможность создавать виртуальный опыт помощника и управлять обновлениями для основного опыта, включая добавление новых навыков.</span><span class="sxs-lookup"><span data-stu-id="926d8-120">It has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
* <span data-ttu-id="926d8-121">Несколько приложений существуют в разных бизнес-функциях, и ожидается, что в будущем их число будет расти.</span><span class="sxs-lookup"><span data-stu-id="926d8-121">Multiple applications exist across business functions and the number is expected to grow in the future.</span></span>
* <span data-ttu-id="926d8-122">Существующие приложения настраиваются, принадлежат организации и преобразуются в навыки виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="926d8-122">Existing applications are customizable, owned by the organization, and are converted into skills for a Virtual Assistant.</span></span>
* <span data-ttu-id="926d8-123">Центральная команда сотрудников может влиять на настройки существующих приложений.</span><span class="sxs-lookup"><span data-stu-id="926d8-123">The central employee experiences team is able to influence customizations to existing apps.</span></span> <span data-ttu-id="926d8-124">Он также предоставляет необходимые рекомендации для интеграции существующих приложений в качестве навыков в виртуальном опыте помощника.</span><span class="sxs-lookup"><span data-stu-id="926d8-124">It also provides necessary guidance for integrating existing applications as skills in Virtual Assistant experience.</span></span>

<span data-ttu-id="926d8-125">Следующее изображение отображает бизнес-функции виртуального помощника:</span><span class="sxs-lookup"><span data-stu-id="926d8-125">The following image displays the business functions of Virtual Assistant:</span></span> 

![Центральная команда поддерживает помощника, а команды бизнес-функций вносят навыки](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="926d8-127">Создание Teams виртуального помощника, ориентированных на систему</span><span class="sxs-lookup"><span data-stu-id="926d8-127">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="926d8-128">Корпорация Майкрософт опубликовала [Visual Studio для создания](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) виртуальных помощников и навыков.</span><span class="sxs-lookup"><span data-stu-id="926d8-128">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="926d8-129">С помощью Visual Studio шаблона, вы можете создать виртуальный помощник, питание от текстового опыта с поддержкой ограниченных богатых карт с действиями.</span><span class="sxs-lookup"><span data-stu-id="926d8-129">With the Visual Studio template, you can create a Virtual Assistant, powered by a text based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="926d8-130">Мы улучшили базовый шаблон Visual Studio, чтобы включить Microsoft Teams платформы и мощность большой Teams приложений.</span><span class="sxs-lookup"><span data-stu-id="926d8-130">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="926d8-131">Некоторые из этих возможностей включают поддержку богатых адаптивных карт, модулей задач, групп или групповых чатов, а также расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="926d8-131">A few of the capabilities include support for rich Adaptive Cards, task modules, teams or group chats, and messaging extensions.</span></span> <span data-ttu-id="926d8-132">Для получения дополнительной информации о расширении виртуальный помощник Microsoft Teams, [с Microsoft Teams м.](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)</span><span class="sxs-lookup"><span data-stu-id="926d8-132">For more information on extending Virtual Assistant to Microsoft Teams, see [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>    
<span data-ttu-id="926d8-133">Следующее изображение отображает диаграмму высокого уровня решения Virtual Assistant:</span><span class="sxs-lookup"><span data-stu-id="926d8-133">The following image displays the high level diagram of a Virtual Assistant solution:</span></span>

![Диаграмма высокого уровня решения виртуального помощника](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="926d8-135">Добавьте адаптивные карты к своему виртуальному помощнику</span><span class="sxs-lookup"><span data-stu-id="926d8-135">Add Adaptive Cards to your Virtual Assistant</span></span>

<span data-ttu-id="926d8-136">Чтобы правильно отправлять запросы, ваш виртуальный помощник должен определить правильную модель LUIS и соответствующие навыки, связанные с ней.</span><span class="sxs-lookup"><span data-stu-id="926d8-136">To dispatch requests properly, your Virtual Assistant must identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="926d8-137">Тем не менее, механизм отправки не может быть использован для действий карты действий, как модель LUIS, связанные с навыком, обучается для текстов действия карты.</span><span class="sxs-lookup"><span data-stu-id="926d8-137">However, the dispatching mechanism cannot be used for card action activities as the LUIS model associated with a skill, is trained for card action texts.</span></span> <span data-ttu-id="926d8-138">Тексты действий карты являются фиксированными, заранее определенными ключевыми словами и не комментируются пользователем.</span><span class="sxs-lookup"><span data-stu-id="926d8-138">The card action texts are fixed, pre-defined keywords, and not commented from a user.</span></span>

<span data-ttu-id="926d8-139">Этот недостаток решается путем встраивания информации о навыке в полезную нагрузку действия карты.</span><span class="sxs-lookup"><span data-stu-id="926d8-139">This drawback is resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="926d8-140">Каждый навык должен `skillId` вставляться  `value` в поле карточных действий.</span><span class="sxs-lookup"><span data-stu-id="926d8-140">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="926d8-141">Вы должны убедиться, что каждая акция карты несет соответствующую информацию о навыках, и виртуальный помощник может использовать эту информацию для отправки.</span><span class="sxs-lookup"><span data-stu-id="926d8-141">You must ensure that each card action activity carries the relevant skill information, and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="926d8-142">Вы должны предоставить `skillId` в конструктор, чтобы убедиться, что информация о навыке всегда присутствует в действиях карты.</span><span class="sxs-lookup"><span data-stu-id="926d8-142">You must provide `skillId` in the constructor to ensure that the skill information is always present in card actions.</span></span>
<span data-ttu-id="926d8-143">Образец кода данных действия карты отображается в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="926d8-143">A card action data sample code is shown in the following section:</span></span>
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

<span data-ttu-id="926d8-144">Далее `SkillCardActionData` класс в шаблоне Virtual Assistant вводится для извлечения из `skillId` полезной нагрузки действия карты.</span><span class="sxs-lookup"><span data-stu-id="926d8-144">Next, `SkillCardActionData` class in the Virtual Assistant template is introduces to extract `skillId` from the card action payload.</span></span>
<span data-ttu-id="926d8-145">Фрагмент кода для извлечения из  `skillId` полезной нагрузки действия карты показан в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="926d8-145">A code snippet to extract  `skillId` from card action payload is shown in the following section:</span></span>

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

<span data-ttu-id="926d8-146">Реализация выполнена методом расширения в классе [Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)</span><span class="sxs-lookup"><span data-stu-id="926d8-146">The implementation is done by an extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>
<span data-ttu-id="926d8-147">Фрагмент кода для извлечения  `skillId` из данных действия карты показан в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="926d8-147">A code snippet to extract  `skillId` from card action data is shown in the following section:</span></span>

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

### <a name="handle-interruptions"></a><span data-ttu-id="926d8-148">Перебои в работе</span><span class="sxs-lookup"><span data-stu-id="926d8-148">Handle interruptions</span></span>

<span data-ttu-id="926d8-149">Виртуальный помощник может обрабатывать перерывы в тех случаях, когда пользователь пытается вызвать навык, в то время как другой навык в настоящее время активен.</span><span class="sxs-lookup"><span data-stu-id="926d8-149">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="926d8-150">`TeamsSkillDialog`, и `TeamsSwitchSkillDialog` представлены на основе Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) и [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs).</span><span class="sxs-lookup"><span data-stu-id="926d8-150">`TeamsSkillDialog`, and `TeamsSwitchSkillDialog`are introduced based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs).</span></span> <span data-ttu-id="926d8-151">Они позволяют пользователям переключать опыт навыков с карточных действий.</span><span class="sxs-lookup"><span data-stu-id="926d8-151">They enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="926d8-152">Чтобы справиться с этим запросом, Виртуальный помощник подсказывает пользователю сообщение о подтверждении, чтобы переключить навыки:</span><span class="sxs-lookup"><span data-stu-id="926d8-152">To handle this request, the Virtual Assistant prompts the user with a confirmation message to switch skills:</span></span>

![Подтверждение подсказки при переходе на новый навык](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a><span data-ttu-id="926d8-154">Запросы модуля задач</span><span class="sxs-lookup"><span data-stu-id="926d8-154">Handle task module requests</span></span>

<span data-ttu-id="926d8-155">Чтобы добавить возможности модуля задач в виртуальный помощник, два дополнительных метода включены в обработчик активности Виртуального помощника: `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="926d8-155">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="926d8-156">Эти методы прослушивают действия, связанные с модулем задач, от Virtual Assistant, определяют навыки, связанные с запросом, и переопределяют запрос на идентифицированный навык.</span><span class="sxs-lookup"><span data-stu-id="926d8-156">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="926d8-157">Перепродающая перемотка запросов [делается с помощью метода SkillHttpClient.](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) `PostActivityAsync`</span><span class="sxs-lookup"><span data-stu-id="926d8-157">Request forwarding is done through the [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` method.</span></span> <span data-ttu-id="926d8-158">Он возвращает ответ, `InvokeResponse` который анализируется и преобразуется в `TaskModuleResponse` .</span><span class="sxs-lookup"><span data-stu-id="926d8-158">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>


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

<span data-ttu-id="926d8-159">Аналогичный подход следует для отправки карточных действий и ответов модуля задач.</span><span class="sxs-lookup"><span data-stu-id="926d8-159">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="926d8-160">Модуль задач извлечения и отправки данных действий обновляется, чтобы включить `skillId` .</span><span class="sxs-lookup"><span data-stu-id="926d8-160">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="926d8-161">Метод расширения активности `GetSkillId` извлекает из `skillId` полезной нагрузки, которая предоставляет подробную информацию о навыках, которые необходимо вызвать.</span><span class="sxs-lookup"><span data-stu-id="926d8-161">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="926d8-162">Фрагмент кода и `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` методы приведены в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="926d8-162">The code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods are given in the following section:</span></span>

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

<span data-ttu-id="926d8-163">Кроме того, вы должны включить все области навыков в `validDomains` раздел в файле манифеста виртуального помощника, чтобы модули задач, вызванные с помощью навыка, должным образом визуализировать.</span><span class="sxs-lookup"><span data-stu-id="926d8-163">Additionally, you must include all skill domains in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked through a skill render properly.</span></span>

### <a name="handle-collaborative-app-scopes"></a><span data-ttu-id="926d8-164">Обработать совместные области приложений</span><span class="sxs-lookup"><span data-stu-id="926d8-164">Handle collaborative app scopes</span></span>

<span data-ttu-id="926d8-165">Teams могут существовать в нескольких сферах, включая чат 1:1, групповой чат и каналы.</span><span class="sxs-lookup"><span data-stu-id="926d8-165">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="926d8-166">Основной шаблон Virtual Assistant предназначен для чатов 1:1.</span><span class="sxs-lookup"><span data-stu-id="926d8-166">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="926d8-167">В рамках бортового опыта Виртуальный помощник подсказывает пользователям имя и поддерживает состояние пользователя.</span><span class="sxs-lookup"><span data-stu-id="926d8-167">As part of the onboarding experience Virtual Assistant prompts users for name and maintains user state.</span></span> <span data-ttu-id="926d8-168">Так как этот опыт посадки не подходит для группового чата или каналов, он был удален.</span><span class="sxs-lookup"><span data-stu-id="926d8-168">Since that onboarding experience is not suited for group chat or channel scopes it has been removed.</span></span>

<span data-ttu-id="926d8-169">Навыки должны обрабатывать действия в нескольких сферах, таких как чат 1:1, групповой чат и разговор по каналу.</span><span class="sxs-lookup"><span data-stu-id="926d8-169">Skills should handle activities in multiple scopes, such as 1:1 chat, group chat, and channel conversation.</span></span> <span data-ttu-id="926d8-170">Если какая-либо из этих областей не поддерживается, навыки должны отвечать соответствующим сообщением.</span><span class="sxs-lookup"><span data-stu-id="926d8-170">If any of these scopes are not supported, skills must respond with an appropriate message.</span></span>

<span data-ttu-id="926d8-171">Следующие функции обработки были добавлены в ядро Virtual Assistant:</span><span class="sxs-lookup"><span data-stu-id="926d8-171">The following  processing functions have been added to Virtual Assistant core:</span></span>

* <span data-ttu-id="926d8-172">Виртуальный помощник может быть вызван без каких-либо текстовых сообщений из группового чата или канала.</span><span class="sxs-lookup"><span data-stu-id="926d8-172">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
* <span data-ttu-id="926d8-173">Артикуляции очищаются перед отправкой сообщения в диспетчерский модуль.</span><span class="sxs-lookup"><span data-stu-id="926d8-173">Articulations are cleaned before sending the message to the dispatch module.</span></span> <span data-ttu-id="926d8-174">Например, удалите необходимые @mention бота.</span><span class="sxs-lookup"><span data-stu-id="926d8-174">For example, remove the necessary @mention of the bot.</span></span>

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

### <a name="handle-messaging-extensions"></a><span data-ttu-id="926d8-175">Ручка расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="926d8-175">Handle messaging extensions</span></span>

<span data-ttu-id="926d8-176">Команды для расширения обмена сообщениями объявлены в файле манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="926d8-176">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="926d8-177">Пользовательский интерфейс расширения обмена сообщениями питается от этих команд.</span><span class="sxs-lookup"><span data-stu-id="926d8-177">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="926d8-178">Для виртуального помощника для питания команды расширения обмена сообщениями в качестве прилагаемого навыка, собственный манифест виртуального помощника должен содержать эти команды.</span><span class="sxs-lookup"><span data-stu-id="926d8-178">For a Virtual Assistant to power a messaging extension command as an attached skill, a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="926d8-179">Вы должны добавить команды из манифеста индивидуального навыка в манифест виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="926d8-179">You must add the commands from an individual skill's manifest to the Virtual Assistant's manifest.</span></span> <span data-ttu-id="926d8-180">Идентификатор команды предоставляет информацию о связанном навыке, притяв идентификатор приложения навыка через сепаратор. `:`</span><span class="sxs-lookup"><span data-stu-id="926d8-180">The command ID provides information about an associated skill by appending the skill's app ID through a separator `:`.</span></span>

<span data-ttu-id="926d8-181">Фрагмент из файла манифеста навыка показан в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="926d8-181">The snippet from a skill's manifest file is shown in the following section:</span></span>

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

<span data-ttu-id="926d8-182">Соответствующий фрагмент кода виртуального помощника показан в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="926d8-182">The corresponding Virtual Assistant manifest file code snippet is shown in the following section:</span></span>

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

<span data-ttu-id="926d8-183">После того, как команды вызываются пользователем, виртуальный помощник может определить связанный навык, разобрать идентификатор команды, обновить действие, удалив дополнительный суффикс `:<skill_id>` из идентификатора команды, и перейти его к соответствующему навыку.</span><span class="sxs-lookup"><span data-stu-id="926d8-183">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix `:<skill_id>` from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="926d8-184">Код для навыка не требует обработки дополнительного суффикса.</span><span class="sxs-lookup"><span data-stu-id="926d8-184">The code for a skill doesnot need to handle the extra suffix.</span></span> <span data-ttu-id="926d8-185">Таким образом, избегаются конфликты между командными СВу между навыками.</span><span class="sxs-lookup"><span data-stu-id="926d8-185">Thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="926d8-186">При таком подходе все команды поиска и действия навыка во всех контекстах, таких как **compose**, **commandBox**, **и сообщение** питаются от виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="926d8-186">With this approach, all the search and action commands of a skill within all contexts, such as **compose**, **commandBox**, and **message** are powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="926d8-187">Некоторые действия по расширению обмена сообщениями не включают идентификатор команды.</span><span class="sxs-lookup"><span data-stu-id="926d8-187">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="926d8-188">Например, `composeExtension/selectItem` содержится только значение действия касаться вызова.</span><span class="sxs-lookup"><span data-stu-id="926d8-188">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="926d8-189">Чтобы определить связанный навык, `skillId`  прилагается к каждой карте элемента при формировании ответа для `OnTeamsMessagingExtensionQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="926d8-189">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="926d8-190">Это похоже на подход к добавлению [адаптивных карт к вашему виртуальному помощнику.](#add-adaptive-cards-to-your-virtual-assistant)</span><span class="sxs-lookup"><span data-stu-id="926d8-190">This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example"></a><span data-ttu-id="926d8-191">Пример</span><span class="sxs-lookup"><span data-stu-id="926d8-191">Example</span></span>

<span data-ttu-id="926d8-192">В следующем примере показано, как преобразовать шаблон приложения Book-a-room в навык виртуального помощника: Book-a-room — это Microsoft Teams, который позволяет пользователям быстро находить и резервировать зал заседаний на 30, 60 или 90 минут, начиная с текущего времени.</span><span class="sxs-lookup"><span data-stu-id="926d8-192">The following example shows how to convert the Book-a-room app template to a Virtual Assistant skill: Book-a-room is a Microsoft Teams that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="926d8-193">Время по умолчанию составляет 30 минут.</span><span class="sxs-lookup"><span data-stu-id="926d8-193">The default time is 30 minutes.</span></span> <span data-ttu-id="926d8-194">Бот-комната в книге прицелы для личных или 1:1 разговоров.</span><span class="sxs-lookup"><span data-stu-id="926d8-194">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="926d8-195">Следующее изображение отображает виртуальный помощник с **книгой номер мастерство:**</span><span class="sxs-lookup"><span data-stu-id="926d8-195">The following image displays a Virtual Assistant with a **book a room** skill:</span></span>

![Виртуальный помощник с навыком «забронируйте комнату»](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="926d8-197">Ниже приведены изменения дельты, введенные для преобразования его в навык, который прилагается к виртуальному помощнику.</span><span class="sxs-lookup"><span data-stu-id="926d8-197">Followings are the delta changes introduced to convert it to a skill which is attached to a Virtual Assistant.</span></span> <span data-ttu-id="926d8-198">Аналогичные руководящие принципы следуют, чтобы преобразовать любой существующий бот v4 в навык.</span><span class="sxs-lookup"><span data-stu-id="926d8-198">Similar guidelines are followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="926d8-199">Манифест навыков</span><span class="sxs-lookup"><span data-stu-id="926d8-199">Skill manifest</span></span>

<span data-ttu-id="926d8-200">Манифест навыков — это файл JSON, который предоставляет конечную точку обмена сообщениями, идентификатор, имя и другие соответствующие метаданные навыков.</span><span class="sxs-lookup"><span data-stu-id="926d8-200">A skill manifest is a JSON file that exposes a skill's messaging endpoint, ID, name, and other relevant metadata.</span></span> <span data-ttu-id="926d8-201">Этот манифест отличается от манифеста, используемого для боковой загрузки приложения в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="926d8-201">This manifest is different than the manifest used for sideloading an app in Microsoft Teams.</span></span> <span data-ttu-id="926d8-202">Виртуальный помощник требует путь к этому файлу в качестве ввода, чтобы прикрепить навык.</span><span class="sxs-lookup"><span data-stu-id="926d8-202">A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="926d8-203">Мы добавили следующий манифест в папку wwwroot бота.</span><span class="sxs-lookup"><span data-stu-id="926d8-203">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="926d8-204">ИНТЕГРАЦИЯ LUIS</span><span class="sxs-lookup"><span data-stu-id="926d8-204">LUIS Integration</span></span>

<span data-ttu-id="926d8-205">Модель отправки виртуального помощника построена поверх прикрепленных навыков' МОДЕЛ моделей LUIS.</span><span class="sxs-lookup"><span data-stu-id="926d8-205">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="926d8-206">Модель отправки определяет цель каждого текстового действия и находит навыки, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="926d8-206">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="926d8-207">Виртуальный помощник требует навыка LUIS модели в `.lu` формате в качестве ввода при присоединении навыка.</span><span class="sxs-lookup"><span data-stu-id="926d8-207">Virtual Assistant requires skill's LUIS model in `.lu` format as an input while attaching a skill.</span></span> <span data-ttu-id="926d8-208">LUIS json преобразуется в формат `.lu` с помощью инструмента botframework-cli.</span><span class="sxs-lookup"><span data-stu-id="926d8-208">LUIS json is converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="926d8-209">Book-a-room bot имеет две основные команды для пользователей:</span><span class="sxs-lookup"><span data-stu-id="926d8-209">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="926d8-210">Мы построили модель LUIS, понимая эти две команды.</span><span class="sxs-lookup"><span data-stu-id="926d8-210">We have built a LUIS model by understanding these two commands.</span></span> <span data-ttu-id="926d8-211">Соответствующие секреты должны быть заселены `cognitivemodels.json` в .</span><span class="sxs-lookup"><span data-stu-id="926d8-211">Corresponding secrets must be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="926d8-212">Соответствующий файл LUIS JSON находится [здесь](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json).</span><span class="sxs-lookup"><span data-stu-id="926d8-212">The corresponding LUIS JSON file is found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json).</span></span>
<span data-ttu-id="926d8-213">Соответствующий `.lu` файл отображается в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="926d8-213">The corresponding `.lu` file is shown in the following section:</span></span>

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

<span data-ttu-id="926d8-214">При этом подходе любая команда, выданная пользователем виртуальному помощнику, связана с ним или идентифицирована как `book room` `manage favorites` команда, `Book-a-room` связанная с ботом, и направляется на этот навык.</span><span class="sxs-lookup"><span data-stu-id="926d8-214">With this approach, any command issued by a user to Virtual Assistant related to `book room` or `manage favorites` are identified as a command associated with `Book-a-room` bot and is forwarded to this skill.</span></span>
<span data-ttu-id="926d8-215">С другой стороны, `Book-a-room room` бот должен использовать модель LUIS, чтобы понять эти команды, если они не на типах заполнены.</span><span class="sxs-lookup"><span data-stu-id="926d8-215">On the other hand, `Book-a-room room` bot needs to use LUIS model to understand these commands if they are not typed full.</span></span> <span data-ttu-id="926d8-216">Пример: `I want to manage my favorite rooms`.</span><span class="sxs-lookup"><span data-stu-id="926d8-216">For example: `I want to manage my favorite rooms`.</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="926d8-217">Многоязычная поддержка</span><span class="sxs-lookup"><span data-stu-id="926d8-217">Multi-Language support</span></span>

<span data-ttu-id="926d8-218">В качестве примера создается модель LUIS только с английской культурой.</span><span class="sxs-lookup"><span data-stu-id="926d8-218">As an example, a LUIS model with only English culture is created.</span></span> <span data-ttu-id="926d8-219">Вы можете создать модели LUIS, соответствующие другим языкам, и добавить запись `cognitivemodels.json` в .</span><span class="sxs-lookup"><span data-stu-id="926d8-219">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="926d8-220">Параллельно добавляйте соответствующий `.lu` файл в путь luisFolder.</span><span class="sxs-lookup"><span data-stu-id="926d8-220">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="926d8-221">Структура фолдеров должна быть следующей:</span><span class="sxs-lookup"><span data-stu-id="926d8-221">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="926d8-222">Чтобы изменить `languages` параметр, обновив команду botskills следующим образом:</span><span class="sxs-lookup"><span data-stu-id="926d8-222">To modify `languages` parameter, update botskills command as follows:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="926d8-223">Виртуальный помощник использует `SetLocaleMiddleware` для определения текущей локализации и вызова соответствующей модели отправки.</span><span class="sxs-lookup"><span data-stu-id="926d8-223">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="926d8-224">Бот фреймворка деятельности имеет локальное поле, которое используется этим средним.</span><span class="sxs-lookup"><span data-stu-id="926d8-224">Bot framework activity has locale field which is used by this middleware.</span></span> <span data-ttu-id="926d8-225">Вы можете использовать то же самое для вашего мастерства, а также.</span><span class="sxs-lookup"><span data-stu-id="926d8-225">You can use the same for your skill as well.</span></span> <span data-ttu-id="926d8-226">Book-a-room bot не использует это среднее программное обеспечение и вместо этого получает локализацию от компании [clientInfo деятельности Bot.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)</span><span class="sxs-lookup"><span data-stu-id="926d8-226">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="926d8-227">Проверка претензий</span><span class="sxs-lookup"><span data-stu-id="926d8-227">Claim validation</span></span>

<span data-ttu-id="926d8-228">Мы добавили [претензииValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) ограничить абонентов к мастерству.</span><span class="sxs-lookup"><span data-stu-id="926d8-228">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="926d8-229">Чтобы виртуальный помощник мог назвать этот навык, заселите `AllowedCallers` массив `appsettings` с помощью идентификатора приложения виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="926d8-229">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="926d8-230">Разрешенная массив абонентов может ограничить, какие навыки потребители могут получить доступ к навыку.</span><span class="sxs-lookup"><span data-stu-id="926d8-230">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="926d8-231">Добавьте одну запись `*` в этот массив, чтобы принимать звонки от любого потребителя навыков.</span><span class="sxs-lookup"><span data-stu-id="926d8-231">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```

<span data-ttu-id="926d8-232">Для получения дополнительной информации о добавлении проверки претензий к навыку, [см.](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="926d8-232">For more information on adding claims validation to a skill, see [add claims validation to skill](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span></span>

### <a name="limitation-of-card-refresh"></a><span data-ttu-id="926d8-233">Ограничение обновления карты</span><span class="sxs-lookup"><span data-stu-id="926d8-233">Limitation of card refresh</span></span> 

<span data-ttu-id="926d8-234">Обновление активности, например обновление карты, пока не поддерживается с помощью virtual Assistant[(выпуск github).](https://github.com/microsoft/botbuilder-dotnet/issues/3686)</span><span class="sxs-lookup"><span data-stu-id="926d8-234">Updating activity, such as card refresh is not supported yet through Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="926d8-235">Таким образом, мы заменили все звонки обновления карты с `UpdateActivityAsync` размещением новых телефонных звонков карты `SendActivityAsync` .</span><span class="sxs-lookup"><span data-stu-id="926d8-235">Hence, we have replaced all card refresh calls `UpdateActivityAsync` with posting new card calls `SendActivityAsync`.</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="926d8-236">Потоки карточных действий и модуля задач</span><span class="sxs-lookup"><span data-stu-id="926d8-236">Card actions and task module flows</span></span>

<span data-ttu-id="926d8-237">Чтобы перемотать действия карты или действия модуля задач на связанные навыки, навык должен `skillId` вставляться в него.</span><span class="sxs-lookup"><span data-stu-id="926d8-237">To forward card action or task module activities to an associated skill, the skill must embed `skillId` to it.</span></span>
<span data-ttu-id="926d8-238">`Book-a-room` Бот-карты действий, модуль задач извлечения и представить действия полезной нагрузки изменены, чтобы `skillId` содержать в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="926d8-238">`Book-a-room` bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="926d8-239">Для получения дополнительной информации [обратитесь к](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) этому разделу из этой документации.</span><span class="sxs-lookup"><span data-stu-id="926d8-239">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="926d8-240">Обработать действия из сферы группового чата или канала</span><span class="sxs-lookup"><span data-stu-id="926d8-240">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="926d8-241">`Book-a-room bot` предназначен для приватных чатов, таких как только личная или область 1:1.</span><span class="sxs-lookup"><span data-stu-id="926d8-241">`Book-a-room bot` is designed for private chats, such as personal or 1:1 scope only.</span></span> <span data-ttu-id="926d8-242">Так как мы настроили Виртуального помощника для поддержки группового чата и каналов, Виртуальный помощник должен быть вызван из областей канала и, таким образом, `Book-a-room` бот должен получать действия для той же области.</span><span class="sxs-lookup"><span data-stu-id="926d8-242">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant must be invoked from the channel scopes and thus, `Book-a-room` bot must get activities for the same scope.</span></span> <span data-ttu-id="926d8-243">Таким `Book-a-room` образом, бот настроен для обработки этих действий.</span><span class="sxs-lookup"><span data-stu-id="926d8-243">Hence `Book-a-room`bot is customized to handle those activities.</span></span> <span data-ttu-id="926d8-244">Вы можете найти проверку в `OnMessageActivityAsync` методах `Book-a-room` обработчика активности бота.</span><span class="sxs-lookup"><span data-stu-id="926d8-244">You can find the check in `OnMessageActivityAsync` methods of `Book-a-room` bot's activity handler.</span></span>

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

<span data-ttu-id="926d8-245">Вы также можете использовать существующие навыки [из репозитория Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) или создать новый навык с нуля.</span><span class="sxs-lookup"><span data-stu-id="926d8-245">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="926d8-246">Для создания новых навыков, [см. учебники для создания новых навыков](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="926d8-246">For creating a new skill, see [tutorials to create a new skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="926d8-247">Для виртуального помощника и навыков архитектуры документации, см[Виртуальный помощник и навыки архитектуры](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="926d8-247">For Virtual Assistant and skills architecture documentation, see[Virtual Assistant and skills architecture](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).</span></span>  

## <a name="limitations-of-virtual-assistant"></a><span data-ttu-id="926d8-248">Ограничения виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="926d8-248">Limitations of Virtual Assistant</span></span> 

* <span data-ttu-id="926d8-249">**EndOfConversation**: Навык должен отправить `endOfConversation` действие, когда он заканчивает разговор.</span><span class="sxs-lookup"><span data-stu-id="926d8-249">**EndOfConversation**: A skill must send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="926d8-250">Основываясь на действиях, виртуальный помощник заканчивает контекст с этим конкретным навыком и возвращается в корневой контекст виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="926d8-250">Based on the activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's root context.</span></span> <span data-ttu-id="926d8-251">Для бота Book-a-room нет четкого состояния, в котором разговор закончился.</span><span class="sxs-lookup"><span data-stu-id="926d8-251">For Book-a-room bot, there is no clear state where conversation is ended.</span></span> <span data-ttu-id="926d8-252">Поэтому мы не послали `endOfConversation` от `Book-a-room` бота, и когда пользователь хочет вернуться к корневому контексту они могут просто сделать это по `start over` команде.</span><span class="sxs-lookup"><span data-stu-id="926d8-252">Hence we have not sent `endOfConversation` from `Book-a-room` bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>  
* <span data-ttu-id="926d8-253">**Обновление карты**: Обновление карты пока не поддерживается через виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="926d8-253">**Card refresh**: Card refresh is not yet supported through Virtual Assistant.</span></span>  
* <span data-ttu-id="926d8-254">**Расширения сообщений**:</span><span class="sxs-lookup"><span data-stu-id="926d8-254">**Messaging extensions**:</span></span>
  * <span data-ttu-id="926d8-255">В настоящее время виртуальный помощник может поддерживать не более десяти команд для расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="926d8-255">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  * <span data-ttu-id="926d8-256">Конфигурация расширений обмена сообщениями не связана с отдельными командами, а для всего самого расширения.</span><span class="sxs-lookup"><span data-stu-id="926d8-256">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="926d8-257">Это ограничивает конфигурацию для каждого отдельного навыка через виртуального помощника.</span><span class="sxs-lookup"><span data-stu-id="926d8-257">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  * <span data-ttu-id="926d8-258">Данные команды расширения сообщений имеют максимальную длину [64 символа,](../resources/schema/manifest-schema.md#composeextensions) а 37 символов используются для встраивания информации о навыках.</span><span class="sxs-lookup"><span data-stu-id="926d8-258">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters are used for embedding skill information.</span></span> <span data-ttu-id="926d8-259">Таким образом, обновленные ограничения для идентификатора команды ограничены 27 символами.</span><span class="sxs-lookup"><span data-stu-id="926d8-259">Thus, updated constraints for command ID are limited to 27 characters.</span></span>

<span data-ttu-id="926d8-260">Вы также можете использовать существующие навыки [из репозитория Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) или создать новый навык с нуля.</span><span class="sxs-lookup"><span data-stu-id="926d8-260">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="926d8-261">Учебники на более поздний день можно найти [здесь](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="926d8-261">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="926d8-262">Пожалуйста, обратитесь [к документации](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) для виртуального помощника и архитектуры навыков.</span><span class="sxs-lookup"><span data-stu-id="926d8-262">Please refer to [documentation](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) for Virtual Assistant and skills architecture.</span></span>

## <a name="code-sample"></a><span data-ttu-id="926d8-263">Пример кода</span><span class="sxs-lookup"><span data-stu-id="926d8-263">Code sample</span></span>

| <span data-ttu-id="926d8-264">**Название образца**</span><span class="sxs-lookup"><span data-stu-id="926d8-264">**Sample name**</span></span> | <span data-ttu-id="926d8-265">**Описание**</span><span class="sxs-lookup"><span data-stu-id="926d8-265">**Description**</span></span> | <span data-ttu-id="926d8-266">**C#**</span><span class="sxs-lookup"><span data-stu-id="926d8-266">**C#**</span></span> | <span data-ttu-id="926d8-267">**.NET**</span><span class="sxs-lookup"><span data-stu-id="926d8-267">**.NET**</span></span> |
|----------|-----------------|----------|------------------|
| <span data-ttu-id="926d8-268">Обновленный шаблон визуальной студии</span><span class="sxs-lookup"><span data-stu-id="926d8-268">Updated visual studio template</span></span> | <span data-ttu-id="926d8-269">Индивидуальный шаблон для поддержки возможностей команд.</span><span class="sxs-lookup"><span data-stu-id="926d8-269">Customized template to support teams capabilities.</span></span> | [<span data-ttu-id="926d8-270">View</span><span class="sxs-lookup"><span data-stu-id="926d8-270">View</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| <span data-ttu-id="926d8-271">Код навыков бота в книге-комнате</span><span class="sxs-lookup"><span data-stu-id="926d8-271">Book-a-room bot skill code</span></span> | <span data-ttu-id="926d8-272">Позволяет быстро найти и забронировать зал заседаний на ходу.</span><span class="sxs-lookup"><span data-stu-id="926d8-272">Lets you quickly find and book a meeting room on the go.</span></span> |  | [<span data-ttu-id="926d8-273">View</span><span class="sxs-lookup"><span data-stu-id="926d8-273">View</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |


## <a name="see-also"></a><span data-ttu-id="926d8-274">См. также</span><span class="sxs-lookup"><span data-stu-id="926d8-274">See also</span></span>

- [<span data-ttu-id="926d8-275">Интеграция веб-приложений</span><span class="sxs-lookup"><span data-stu-id="926d8-275">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

- [<span data-ttu-id="926d8-276">Книга-комната</span><span class="sxs-lookup"><span data-stu-id="926d8-276">Book-a-room</span></span>](app-templates.md#book-a-room)

- [<span data-ttu-id="926d8-277">Microsoft Teams бот</span><span class="sxs-lookup"><span data-stu-id="926d8-277">Microsoft Teams bot</span></span>](../bots/what-are-bots.md)