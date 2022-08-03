---
title: Создание виртуального помощника
description: Узнайте, как создать бот Виртуального помощника для Teams с помощью примеров кода и фрагментов кода с такими функциями, как адаптивные карточки, обработка прерываний и т. д.
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 12339ed10f1c6a6e30ebb74320fbf69018a6d3f9
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2022
ms.locfileid: "67178606"
---
# <a name="create-virtual-assistant"></a>Создание виртуального помощника

Виртуальный помощник — это шаблон Майкрософт с открытым исходным кодом, позволяющий создать надежное диалоговое решение, сохраняя полный контроль над взаимодействием с пользователем, фирменной символикой организации и необходимыми данными. [Базовый шаблон виртуального помощника](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) представляет собой основной "строительный кубик", объединяющий технологии Майкрософт, необходимые для создания виртуального помощника, в том числе [SDK Bot Framework](https://github.com/microsoft/botframework-sdk), [Распознавание речи (LUIS)](https://www.luis.ai/) и [QnA Maker](https://www.qnamaker.ai/). Он также объединяет основные возможности, в том числе регистрацию навыков, привязанные учетные записи и базовое намерение общения, чтобы предложить пользователям широкий спектр беспроблемного взаимодействия и пользовательского опыта. Кроме того, возможности шаблона включают в себя множество примеров многократно используемых [навыков общения](https://microsoft.github.io/botframework-solutions/overview/skills).  Отдельные навыки интегрированы в виртуальный помощник, чтобы реализовать сразу несколько сценариев. С помощью пакета SDK Bot Framework навыки представлены в форме исходного кода, что позволяет настраивать и расширять их по мере необходимости. Дополнительные сведения о навыках, реализованных в Bot Framework, см. в разделе [Что такое навык Bot Framework](https://microsoft.github.io/botframework-solutions/overview/skills/). В этом документе приведены рекомендации по реализации виртуальных помощников для организаций, описано создание специализированных виртуальных помощников для Teams, примеры программного кода и ограничения виртуальных помощников.
На следующем рисунке показан обзор виртуального помощника:

![Обзорная схема виртуального помощника](../assets/images/bots/virtual-assistant/overview.png)

Ядро виртуального помощника перенаправляет действия с текстовыми сообщениями привязанным навыкам по модели [диспетчеризации](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true).

## <a name="implementation-considerations"></a>Рекомендации по реализации

Решение о добавлении виртуального помощника строится на множестве факторов и отличается для каждой организации. Ниже приведены факторы, позволяющие принять решение о реализации виртуального помощника для вашей организации.

* Центральная группа управляет всем взаимодействием сотрудников. Она позволяет создавать новые виртуальные помощники и управлять обновлениями основного интерфейса, включая добавление новых навыков.
* В организации существует несколько бизнес-функций, у каждой из них несколько приложений, и ожидается, что их число в будущем увеличится.
* Существующие приложения принадлежат организации, их можно настраивать и преобразовать в навыки для виртуального помощника.
* Центральная группа по взаимодействию сотрудников может влиять на настройки существующих приложений. Она также предоставляет необходимые рекомендации по интеграции существующих приложений в качестве навыков в интерфейсы виртуального помощника.

На следующем рисунке показаны бизнес-функции виртуального помощника.

![Центральная группа поддерживает виртуального помощника, а команды бизнес-функций — навыки](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Создание специализированного виртуального помощника для Teams

Корпорация Майкрософт опубликовала шаблон [Microsoft Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) для создания виртуальных помощников и навыков. С помощью шаблона Visual Studio можно создать виртуального помощника с текстовым интерфейсом и поддержкой ограниченных форматированных карточек с действиями. Мы улучшили базовый шаблон Visual Studio, включив в него возможности платформы Microsoft Teams и отличные возможности приложений Teams. В числе возможностей - поддержка адаптивных карточек с расширенными возможностями, модулей задач, командных или групповых чатов и расширений для обмена сообщениями. Дополнительные сведения о расширении виртуального помощника для Microsoft Teams см. в документе: [Руководство по расширению виртуального помощника для взаимодействия с Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).
На следующем рисунке показана высокоуровневая схема решения виртуального помощника.

![Высокоуровневая схема решения виртуального помощника](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Добавление адаптивных карточек в виртуальный помощник

Чтобы правильно перенаправлять запросы, виртуальный помощник должен определить нужную модель LUIS и соответствующий навык, связанный с ней. Однако механизм диспетчеризации нельзя использовать для действий с карточками, так как модель LUIS, связанная с навыком, обучена для текстов действий карточки. Текст действия карточки - это набор фиксированных, предопределенных ключевых слов, и пользователь не добавляет туда своих комментариев.

Этот пробел устраняется путем внедрения сведений о навыках в полезную нагрузку действия карточки. Каждый навык нужно внедрить `skillId` в поле `value` действий карточки. Обеспечьте наличие в каждом действии карточки соответствующих сведений о навыках, Виртуальный помощник использует эти сведения для диспетчеризации.

Необходимо указать `skillId` в конструкторе, чтобы гарантировать присутствие сведений о навыке в действиях карточки.
Пример программного кода данных действия карточки показан в следующем разделе:

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

Затем вводится класс `SkillCardActionData` в шаблоне виртуального помощника для извлечения `skillId` из полезной нагрузки действия карточки.
Фрагмент кода, извлекающий `skillId` из полезной нагрузки действия карточки, показан в следующем разделе:

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

Реализация выполняется методом расширения в классе [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md).
Фрагмент кода для извлечения  `skillId` из данных действия карточки показан в следующем разделе:

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

### <a name="handle-interruptions"></a>Обработка прерываний

Виртуальный помощник может обрабатывать прерывания в случаях, когда пользователь пытается вызвать навык во время активности другого навыка. Затем вводятся `TeamsSkillDialog` и `TeamsSwitchSkillDialog`на основе [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) и [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs) платформы Bot Framework. Они позволяют пользователям переключать навыки между действиями с карточками. Для обработки этого запроса виртуальный помощник запросит у пользователя подтверждение для переключения навыков:

![Запрос подтверждения при переходе на другой навык](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>Обработка запросов модуля задач

Чтобы добавить возможности модуля задач в виртуальный помощник, в обработчик действия виртуального помощника вводятся два дополнительных метода: `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync`. Эти методы прослушивают действия, связанные с модулем задач, из виртуального помощника, определяют навык, связанный с запросом, и перенаправляют запрос в обнаруженный навык.

Переадресация запросов выполняется с помощью метода [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync`. Он возвращает ответ в виде `InvokeResponse`, который анализируется и преобразуется в `TaskModuleResponse`.

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

Аналогичный подход используется для диспетчеризации действий карточек и ответов модуля задач. Реализацию извлечения и отправки данных действий модуля задач изменяют, добавляя в нее `skillId`.
Метод расширения действия `GetSkillId` извлекает `skillId` из полезной нагрузки, содержащей сведения о навыке, который необходимо вызвать.

Фрагмент кода для методов `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync` приведен в следующем разделе:

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

Кроме того, все домены навыка необходимо включить в раздел `validDomains` файла манифеста виртуального помощника, чтобы модули задач, вызываемые с помощью навыка, отрисовывались правильно.

### <a name="handle-collaborative-app-scopes"></a>Обработка областей приложения для совместной работы

Приложения Teams могут существовать в нескольких областях, в том числе в приватных чатах, групповых чатах и каналах. Основной шаблон виртуального помощника предназначен для приватных чатов. В рамках процесса подключения виртуальный помощник запрашивает имя пользователя и сохраняет его состояние. Так как процесс подключения не подходит для группового чата или области каналов, он был удален.

Навыки должны обрабатывать действия в нескольких областях, таких как приватный чат, групповой чат и беседа в канале. Если любая из этих областей не поддерживается, навыки должны отвечать соответствующим сообщением.

Следующие функции обработки были добавлены в ядро виртуального помощника:

* Виртуальный помощник можно вызвать без текстовых сообщений из группового чата или канала.
* Артикуляции следует очистить перед отправкой сообщения в модуль диспетчеризации. Например, удалите необходимые @упоминания бота.

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

### <a name="handle-message-extensions"></a>Обработка расширений для сообщений

Команды расширения для сообщений нужно объявить в файле манифеста приложения. Этими командами поддерживается пользовательский интерфейс расширения сообщений. Чтобы виртуальный помощник обрабатывал команду расширения для сообщений в качестве присоединенного навыка, собственный манифест виртуального помощника должен содержать эти команды. Необходимо добавить команды из манифеста отдельного навыка в манифест виртуального помощника. Идентификатор команды предоставляет сведения о привязанном навыке путем добавления идентификатора приложения навыка через разделитель `:`.

Фрагмент кода из файла манифеста навыка показан в следующем разделе:

```json
 "composeExtensions": [
    {
        "botId": "<Skil_App_Id>",
        "commands": [
            {
                "id": "searchQuery",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
                 ....}
         ]
     }
 ]
                 
```

Соответствующий фрагмент программного кода из файла манифеста виртуального помощника показан в следующем разделе:

```json
 "composeExtensions": [
    {
        "botId": "<VA_App_Id>",
        "commands": [
            {
                "id": "searchQuery:<skill_id>",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
                 ....}
         ]
     }
 ]
 
```

После вызова команд пользователем виртуальный помощник может определить нужный навык посредством синтаксического анализа идентификатора команды, обновить действие, удалив лишний суффикс `:<skill_id>` из идентификатора команды, и перенаправить его в соответствующий навык. Обрабатывать дополнительный суффикс в коде, реализующем навык, не нужно. Таким образом, конфликта идентификаторов команд между навыками можно избежать. При таком подходе все команды поиска и действия навыка во всех контекстах, такие как **compose**, **commandBox** и **message**, реализуются на базе виртуального помощника.

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

Некоторые действия расширения сообщения не включают идентификатор команды. Например, `composeExtension/selectItem` содержит только значение вызова действия касания. Чтобы определить привязанный навык, `skillId` присоединяется к каждой карточке элемента при формировании ответа для `OnTeamsMessagingExtensionQueryAsync`. Это аналогично[добавлению адаптивных карточек в виртуальный помощник](#add-adaptive-cards-to-your-virtual-assistant).

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

## <a name="example"></a>Пример

В следующем примере показано, как преобразовать шаблон приложения book-a-room в навык виртуального помощника: Book-a-room — это Teams, который позволяет пользователям быстро находить и резервировать конференц-зал на 30, 60 или 90 минут, начиная с текущего времени. Длительность резервирования по умолчанию — 30 минут. Бот "Резервирование комнаты" действует в области личных или приватных бесед.
На следующем рисунке показан виртуальный помощник с навыком **Резервирование комнаты**:

![Виртуальный помощник с навыком "Резервирование комнаты"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Ниже приведены разностные изменения, внесенные для преобразования его в навык, подключенный к виртуальному помощнику. Аналогичные шаги нужны для преобразования любого существующего бота версии 4 в навык.

### <a name="skill-manifest"></a>Манифест навыка

Манифест навыка — это JSON-файл, предоставляющий параметры навыка: конечную точку обмена сообщениями, идентификатор, имя и другие соответствующие метаданные. Этот манифест отличается от манифеста, используемого для загрузки неопубликованного приложения в Teams. Виртуальному помощнику нуже путь к этому файлу в качестве входных данных для прикрепления навыка. Мы добавили следующий манифест в папку wwwroot бота.

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

### <a name="luis-integration"></a>Интеграция LUIS

Модель диспетчеризации виртуального помощника достраивается поверх моделей LUIS подключенных навыков. Модель диспетчеризации определяет намерение для каждого текстового действия и находит связанный с ним навык.

Виртуальному помощнику требуется модель LUIS навыка в формате `.lu` в качестве входного параметра при подключении навыка. JSON-файл LUIS преобразуется в формат `.lu` с помощью средства botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Бот "Резервирование комнаты" имеет две основные команды для пользователей:

* `Book room`
* `Manage Favorites`

Мы создали модель LUIS, осмыслив эти две команды. Соответствующие секреты должны быть заполнены в `cognitivemodels.json`. Соответствующий JSON-файл LUIS можно найти [здесь](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json).
Соответствующий файл `.lu` показан в следующем разделе:

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

При таком подходе любая команда, выданная пользователем виртуальному помощнику и связанная с `book room` или `manage favorites` идентифицируется как команда, связанная с ботом `Book-a-room`, и перенаправляется в этот навык.
С другой стороны, бот `Book-a-room room` должен использовать модель LUIS, чтобы понять эти команды, если они не заполнены. Пример: `I want to manage my favorite rooms`.

### <a name="multi-language-support"></a>Поддержка нескольких языков.

Например, создается модель LUIS только с английским языком и региональными параметрами. Вы можете создать модели LUIS, соответствующие другим языкам, и добавить запись в `cognitivemodels.json`.

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

Параллельно добавьте соответствующий файл `.lu` в путь luisFolder. Структура папок должна выглядеть следующим образом:

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Чтобы изменить параметр `languages` , обновите команду навыков бота следующим образом:

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

Виртуальный помощник использует `SetLocaleMiddleware` для определения текущего языкового стандарта и вызова соответствующей модели диспетчеризации. Действие Bot Framework имеет поле языкового стандарта, используемого этим ПО промежуточного слоя. Вы можете использовать то же самое для своего навыка. Бот book-a-room не использует это ПО промежуточного слоя и вместо этого получает языковой стандарт из сущности [clientInfo действия Bot Framework](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).

### <a name="claim-validation"></a>Проверка утверждений

Мы добавили [claimsValidator,](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) чтобы ограничить вызывающие объекты навыком. Чтобы разрешить виртуальному помощнику вызывать этот навык, заполните массив `AllowedCallers` на основе `appsettings` с помощью идентификатора приложения этого виртуального помощника.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

Массив разрешенных вызывающих объектов может ограничить доступ потребителей навыка к навыку. Добавьте одну запись `*` в этот массив, чтобы принимать вызовы от любого потребителя навыка.

```
"AllowedCallers": [ "*" ],
```

Дополнительные сведения о добавлении проверки утверждений в навык см. в разделе [Добавление проверки утверждений в навык](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).

### <a name="limitation-of-card-refresh"></a>Ограничение обновления карточки

Обновление действия, например обновление карточки, пока не поддерживается с помощью Виртуального помощника ([проблема с GitHub](https://github.com/microsoft/botbuilder-dotnet/issues/3686)). Таким образом, мы заменили все вызовы обновления карточек `UpdateActivityAsync` публикацией новых вызовов карт `SendActivityAsync`.

### <a name="card-actions-and-task-module-flows"></a>Действия с карточками и потоки модулей задач

Чтобы перенаправлять действия карточки или действия модуля задач в привязанный навык, навык должен внедрить в него `skillId`.
Действие карточки бота `Book-a-room`, получение и отправку полезных данных модуля задачи нужно изменить так, чтобы они содержали `skillId` в качестве параметра.

Дополнительные сведения см. [в этом](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) разделе этой документации.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Обработка действий из области группового чата или канала

`Book-a-room bot` предназначен для частных чатов, таких как личные или приватные. Так как мы настроили виртуальный помощник для поддержки областей группового чата и каналов, виртуальный помощник нужно вызывать из областей канала, поэтому бот `Book-a-room` должен получать действия для той же области. Поэтому бот `Book-a-room` нужно изменить для обработки этих действий. Вы можете найти методы проверки `OnMessageActivityAsync` обработчика `Book-a-room` действий бота.

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

Вы можете также использовать существующие навыки из [репозитория решений Bot Framework](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) или создать новый навык с нуля. В создании навыка вам помогут [руководства по созданию нового навыка](https://microsoft.github.io/botframework-solutions/overview/skills/). Документацию по архитектуре виртуального помощника и навыков см. в статье [Архитектура виртуального помощника и навыков](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).  

## <a name="limitations-of-virtual-assistant"></a>Ограничения виртуального помощника

* **EndOfConversation**: по завершении беседы навык должен отправить действие `endOfConversation`. В зависимости от действия виртуальный помощник заканчивает контекст с определенным навыком и возвращается в корневой контекст виртуального помощника. Для бота book-a-room нет четкого состояния завершения беседы. Поэтому мы не отправляли сообщения `endOfConversation` от `Book-a-room` бота, и когда пользователь хочет вернуться к корневому контексту, он может просто сделать это с помощью `start over` команды.  
* **Обновление карточки**: обновление карточки еще не поддерживается с помощью Виртуального помощника.  
* **Расширения для сообщений**
  * В настоящее время виртуальный помощник может поддерживать не более десяти команд расширения для сообщений.
  * Конфигурация расширений сообщений не предназначена для отдельных команд, а для всего расширения. Это ограничивает конфигурацию для каждого отдельного навыка с помощью виртуального помощника.
  * Идентификаторы команд расширений сообщений имеют максимальную длину [64 символа](../resources/schema/manifest-schema.md#composeextensions), а для внедрения сведений о навыках используется 37 символов. Таким образом, новое ограничение для идентификатора команды - 27 символов.

Вы можете также использовать существующие навыки из [репозитория решений Bot Framework](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) или создать новый навык с нуля. Руководства для последнего можно найти [здесь](https://microsoft.github.io/botframework-solutions/overview/skills/). См. [документацию по архитектуре виртуального помощника и навыков](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **C#**  **.NET** |
|----------|-----------------|---------------------------|
| Обновленный шаблон Visual Studio | Настраиваемый шаблон для поддержки возможностей Teams. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| Код навыка бота "Резервирование комнаты" | Позволяет быстро находить и резервировать помещения для совещаний. | [Просмотр](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Интеграция веб-приложений](~/samples/integrate-web-apps-overview.md)
* [Бот "Резервирование комнаты"](app-templates.md#app-template-code-samples)
* [Бот Microsoft Teams.](../bots/what-are-bots.md)
