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
# <a name="virtual-assistant-for-microsoft-teams"></a>Виртуальный помощник для Microsoft Teams

Virtual Assistant — это шаблон Microsoft Open-Source, который позволяет создавать надежное диалоговое решение, обеспечивая полный контроль над возможностями взаимодействия с пользователем, фирменной символикой и необходимыми данными. [Основной шаблон основного помощника](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) — это базовый Стандартный блок, который объединяет технологии Майкрософт, необходимые для создания виртуального помощника, включая [пакет SDK для ленты](https://github.com/microsoft/botframework-sdk), [язык (Луис)](https://www.luis.ai/), [КНА Maker](https://www.qnamaker.ai/), а также важные возможности, включая регистрацию навыков, связанные учетные записи, базовую цепочку для конечных пользователей. Кроме того, вы также включаете в себя обширные примеры полезных [навыков](https://microsoft.github.io/botframework-solutions/overview/skills)для общения.  Отдельные навыки можно интегрировать в решение Virtual Assistant для поддержки нескольких сценариев. С помощью пакета SDK для ленты, навыки представлены в форме исходного кода, что позволяет настраивать и расширять их по мере необходимости. Узнайте [, что такое навык в виде Bot-Framework](https://microsoft.github.io/botframework-solutions/overview/skills/).

![Схема обзора Virtual Assistant](../assets/images/bots/virtual-assistant/overview.png)

Текстовые действия с сообщениями направляются на связанные навыки ядром виртуального помощника с помощью модели [отправки](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) . 

## <a name="implementation-considerations"></a>Рекомендации по реализации

Решение о добавлении виртуального помощника может включать множество детерминантс и различаться для каждой организации. Ниже приведены факторы, которые поддерживают реализацию виртуального помощника для вашей организации.

- Централизованная команда управляет всеми сотрудниками отдела и имеет возможность создавать интерфейс виртуального помощника и управлять обновлениями для основного интерфейса, включая добавление новых навыков.
- Несколько приложений существуют в бизнес-функциях и/или их число в будущем должно увеличиться.
- Существующие приложения могут настраиваться, принадлежать Организации и могут быть преобразованы в навыки виртуального помощника.
- Центральная группа сотрудников может влиять на настройки существующих приложений и предоставлять необходимые рекомендации по интеграции существующих приложений в качестве навыков в интерфейсе Virtual Assistant

![Центральная группа поддерживает помощника, а бизнес-функции Teams — навыки](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Создание виртуального помощника, ориентированного на Teams

Корпорация Майкрософт опубликовала [шаблон Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) для создания виртуальных помощников и навыков. С помощью шаблона Visual Studio вы можете создать виртуальный помощник, на основе текстового интерфейса с поддержкой ограниченных карт с действиями. Мы добавили расширенный шаблон Visual Studio, чтобы включить возможности платформы Microsoft Teams и мощные возможности для работы с приложениями в Teams. Некоторые возможности включают поддержку расширенных адаптивных карт, модулей задач, команд и групповых чатов и расширений обмена сообщениями. *Кроме того*, [в этой статье рассказывается о том, как расширить свой виртуальный помощник до Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).

![Высокоуровневая схема решения Virtual Assistant](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Добавление адаптивных карт для виртуального помощника

Чтобы правильно обработать запросы, ваш виртуальный помощник должен определить правильную модель Луис и соответствующий навык, связанный с ней. Тем не менее, механизм диспетчеризации невозможно использовать для действий с карточками, так как модель Луис, связанная с навыком, может не быть обучена для текстов действий карты, так как они являются фиксированными, предопределенными ключевыми словами, а не уттеранцес от пользователя.

Мы разрешали эту проблему, внедрив сведения о навыках в полезные данные действий карты. Каждый навык должен внедряться `skillId` в `value` поле действия с карточками. Это лучший способ гарантировать, что каждое действие действия с картой несет соответствующую информацию о навыках, и виртуальный помощник сможет использовать эту информацию для диспетчеризации.

Ниже приведен пример данных действия карты. Предоставляя `skillId` конструктор, вы гарантируете, что сведения о навыках всегда присутствуют в действиях карточки.

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

Далее мы рассмотрим `SkillCardActionData` класс в шаблоне Virtual Assistant, чтобы извлечь `skillId` из полезных данных действия карточки.

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

Ниже приведен фрагмент кода, который необходимо извлечь `skillId` из данных действий карты. Мы реализовали его в качестве метода расширения в классе [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) .

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

### <a name="handle-interruptions-gracefully"></a>Мягкое прерывание обработки прерываний

Виртуальный помощник может обрабатывать прерывания в тех случаях, когда пользователь пытается вызвать навык, пока в данный момент активен другой навык. Мы предоставили `TeamsSkillDialog` и `TeamsSwitchSkillDialog` , на основе [скиллдиалог](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) и [свитчскиллдиалог](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), чтобы позволить пользователям переключать навыки из действий карты. Чтобы обработать этот запрос, виртуальный помощник запросит у пользователя сообщение с подтверждением, чтобы переключить навыки.

![Запрос подтверждения при переключении на новый навык](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a>Обработка запросов модулей задач

Чтобы добавить возможности модуля задач для виртуального помощника, в обработчик действий виртуального помощника включены два дополнительных метода: `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync` . Эти методы прослушивают действия, связанные с модулем задач, от виртуального помощника, идентифицируют навык, связанный с запросом, и пересылают запрос определенному навыку. 

Пересылка запросов выполняется с помощью [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable)метода скиллхттпклиент `PostActivityAsync` . Он возвращает ответ, `InvokeResponse` который анализируется и преобразуется в `TaskModuleResponse` .

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

Аналогичный подход используется для диспетчеризации действий карты и ответа модуля задач. Данные действий при получении и отсылке модуля задачи обновляются, чтобы включить их `skillId` . Метод расширения действия `GetSkillId` извлекает `skillId` данные из полезных данных, которые предоставляют сведения о навыках, которые необходимо вызвать.

Ниже приведен фрагмент кода для `OnTeamsTaskModuleFetchAsync` методов и `OnTeamsTaskModuleSubmitAsync` .

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

Кроме того, все домены навыков должны быть включены в `validDomains` раздел файла манифеста виртуального помощника, чтобы модули задач, вызываемые с помощью навыка, правильно отрисовывается.

### <a name="handling-collaborative-app-scopes"></a>Обработка областей приложений для сотрудничества

Приложения Teams могут существовать в нескольких областях, в том числе чат 1:1, групповой чат и каналы. Шаблон основного виртуального помощника предназначен для 1:1 сеансов. В процессе входящей миграции виртуальный помощник запрашивает у пользователей имя и сохраняет состояние пользователя. Так как этот процесс входящей миграции не подходит для областей группового чата и каналов, он был удален.

Навыки должны обрабатывать действия в нескольких областях (1:1 чат, группового чата и беседы каналов). Если какая – либо из этих областей не поддерживается, навыки должны отреагировать на соответствующее сообщение.

В ядро виртуального помощника добавлены следующие функции обработки:

- Виртуальный помощник может вызываться без текстового сообщения из группового чата или канала.
- Артикулатионс очищаются (то есть удалите необходимое @mention ленты) перед отправкой сообщения в модуль диспетчеризации.

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

### <a name="handling-messaging-extensions"></a>Обработка расширений обмена сообщениями

Команды для расширения обмена сообщениями объявляются в файле манифеста приложения. Пользовательский интерфейс расширения обмена сообщениями питается от этих команд. Чтобы виртуальный помощник по работе с командой расширения системы обмена сообщениями (в качестве присоединенного навыка), собственный манифест виртуального помощника должен содержать эти команды. Команды из манифеста отдельного навыка также необходимо добавить в манифест виртуального помощника. КОД команды предоставляет сведения о связанном навыке, добавляя идентификатор приложения для навыка с помощью разделителя ( `:` ).

Ниже приведен фрагмент файла манифеста для навыка.

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

А ниже — соответствующий фрагмент кода файла манифеста виртуального помощника.

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

Когда пользователь вызывает команды, виртуальный помощник может определить связанный навык путем синтаксического анализа идентификатора команды, обновить действие, удалив лишний суффикс ( `:<skill_id>` ) из идентификатора команды и переслать его соответствующему навыку. Коду для квалификации не требуется обрабатывать дополнительный суффикс, поэтому не следует использовать конфликты между идентификаторами команд в навыках. Благодаря этому подходу все команды поиска и действий навыка в рамках всех контекстов ("создание", "Коммандбокс" и "сообщение") могут быть включены виртуальным помощником.

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

Некоторые действия по расширению системы обмена сообщениями не включают идентификатор команды. Например, `composeExtension/selectItem` содержит только значение действия Invoke TAP. Чтобы определить связанный навык, `skillId` прикрепляется к каждой карточке товара при создании ответа на `OnTeamsMessagingExtensionQueryAsync` . (Это аналогично способу [добавления адаптивных карт для виртуального помощника](#add-adaptive-cards-to-your-virtual-assistant).

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a>Пример: преобразование шаблона приложения "книга — комната" в навык виртуального помощника

[Book-a-комната](app-templates.md#book-a-room) — это [робот Microsoft Teams](../bots/what-are-bots.md) , который позволяет пользователям быстро находить и зарезервировать комнату для собраний в течение 30 (по умолчанию), 60 или 90 минут, начиная с текущего времени. Области Bot "книга — комната" для личных или 1:1 бесед.

![Виртуальный помощник с навыком "книга" в помещении](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Ниже приведены изменения, внесенные в разницу для преобразования в навык, который можно присоединить к виртуальному помощнику. Аналогичные инструкции можно выполнить, чтобы преобразовать любой существующий робот v4 в навык.

### <a name="skill-manifest"></a>Манифест навыка

Манифест навыка это JSON-файл, который предоставляет конечную точку обмена сообщениями, идентификатор, имя и другие релевантные метаданные (этот манифест отличается от манифеста, используемого для неопубликованного приложения в Microsoft Teams). виртуальному помощнику требуется путь к этому файлу в качестве входных данных для присоединения навыка. Мы добавили следующий манифест в папку wwwroot для ленты.

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

### <a name="luis-integration"></a>Интеграция Луис

Модель диспетчеризации виртуального помощника построена на основе моделей Луис присоединенных навыков. Модель диспетчеризации определяет цель для каждого текстового действия и находит навык, связанный с ним.

Виртуальному помощнику необходимо, чтобы в качестве входных данных в качестве входного навыка была модель Луис (в `.lu` формате). Луис JSON можно преобразовать в `.lu` Формат с помощью средства ботфрамеворк – CLI.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

В книге поробота a для комнаты две основные команды для пользователей:

- `Book room`
- `Manage Favorites`

Мы создали модель Луис, которая понимает эти две команды. Соответствующие секреты должны быть заполнены `cognitivemodels.json` . Соответствующий JSON-файл Луис можно найти [здесь](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) , и именно так `.lu` выглядит соответствующий файл.

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

При использовании этого подхода любая команда, связанная с пользователем `book room` или `manage favorites` может быть идентифицирована как команда, связанная с программой-роботом Book-a-Room и Переадресованная этому навыку.
С другой стороны, для этого необходимо использовать модель Луис для изучения этих команд, если они не типизированы как есть (например: `I want to manage my favorite rooms` ).

### <a name="multi-language-support"></a>Поддержка нескольких языков

В этом примере мы создали только модель Луис с английским языком и региональными параметрами. Вы можете создавать модели Луис, соответствующие другим языкам, и добавлять записи в `cognitivemodels.json` .

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

Параллельно добавьте соответствующий `.lu` файл в путь луисфолдер. Структура папок должна выглядеть следующим образом:

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Чтобы изменить параметр, выполните команду Update ботскиллс следующим образом `languages` .

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

Виртуальный помощник использует `SetLocaleMiddleware` для определения текущего языкового стандарта и вызова соответствующей модели отправки. (Действие "Bot Framework" имеет поле языкового стандарта, которое используется этим промежуточным по.) Мы рекомендуем использовать те же сведения, что и для вашего навыка. Books — Bot для начала работы не использует это промежуточное по и вместо этого задается языковой стандарт для [объекта клиентинфо](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)действия Bot Framework.

### <a name="claim-validation"></a>Проверка утверждения

Мы добавили [клаимсвалидатор](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) , чтобы ограничить абоненты навыком. Чтобы разрешить виртуальному помощнику вызывать этот навык, заполните `AllowedCallers` массив `appsettings` с помощью идентификатора приложения конкретного виртуального помощника.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

Допустимый массив абонентов может ограничивать круг пользователей, которые могут получить доступ к навыку. Добавьте `*` к этому массиву одну запись, чтобы принимать звонки от любого потребителя опыта.

```
"AllowedCallers": [ "*" ],
```
[Здесь вы найдете](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)подробную документацию по добавлению проверки утверждений для навыка.

### <a name="card-refresh-limitation"></a>Ограничение на обновление карты

Действия по обновлению (обновление карты) пока не поддерживаются виртуальным помощником ([Ошибка GitHub](https://github.com/microsoft/botbuilder-dotnet/issues/3686)). Таким образом, мы заменили все вызовы обновления карт ( `UpdateActivityAsync` ) с учетом вызовов новых карточек ( `SendActivityAsync` ).

### <a name="card-actions-and-task-module-flows"></a>Потоки действий карты и модуля задач

Для пересылки карточки действий или действий модуля задач в связанный навык необходимо внедрить `skillId` их в этот навык.
Действие "книга" — действие с картой "подача", "модуль задач" и "действия по отсылке" изменяются в `skillId` соответствии с параметром. 

Для получения дополнительных сведений обратитесь к [этому](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) разделу из этой документации.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Обработка действий из области группового чата или канала

Почтовые роботы, предназначенные только для частных чатов (персональный/1:1 область). Так как у нас есть настроенный виртуальный помощник для поддержки областей группового чата и каналов, виртуальный помощник может вызываться из этих областей и, таким образом, может получить действия из книги "робот". Таким образом, для обработки этих действий настроен заказ ленты a-комната. Проверка включена в `OnMessageActivityAsync` методы обработчика активности для ленты "книга — комната".

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

Вы также можете использовать существующие навыки из [репозитория решений для Bot](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) или создать новый навык с нуля. Учебные пособия для более поздних версий можно найти [здесь](https://microsoft.github.io/botframework-solutions/overview/skills/). Ознакомьтесь с [документацией](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0) по архитектуре виртуального помощника и навыков.

## <a name="sample-code-to-get-started"></a>Пример кода, чтобы приступить к работе

- [Обновленный шаблон Visual Studio](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [Код квалификации botа "книга — комната"](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a>Известные ограничения виртуального помощника

- **Ендофконверсатион**. Навык должен отправить `endOfConversation` действие при завершении беседы. на основе этого действия виртуальный помощник заканчивает контекст с определенным навыком и возвращается в контекст виртуального помощника (корневого). Для ленты "книга — комната" нет четкого состояния, в котором можно завершить беседу. Поэтому мы не отправили `endOfConversation` с ленты Books — a Room, а когда пользователь хочет вернуться к корневому контексту, он может просто сделать это с помощью `start over` команды.
- **Обновление карточки**. Обновления карт пока не поддерживаются виртуальным помощником.
- **Расширения для обмена сообщениями**:
  - В настоящее время виртуальный помощник может поддерживать не более десяти команд для расширений системы обмена сообщениями.
  - Конфигурация расширений обмена сообщениями не ограничена отдельными командами, но для всего расширения. Это ограничит конфигурацию каждого отдельного навыка с помощью виртуального помощника.
  - Длина идентификаторов команд расширений обмена сообщениями не должна превышать [64 символов](../resources/schema/manifest-schema.md#composeextensions) , а для внедрения сведений о навыках будет использоваться 37 символов. Таким образом, в обновленных ограничениях для идентификатора команды можно добавить не более 27 символов.
>
>
