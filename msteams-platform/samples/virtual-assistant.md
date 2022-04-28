---
title: Создание виртуального помощника
description: Узнайте, как создать бот Виртуальный помощник для Microsoft Teams с помощью примеров кода и фрагментов кода с такими функциями, как адаптивные карточки, обработка прерываний, запросов модулей задач, областей приложения для совместной работы и расширений сообщений; с помощью манифеста навыка; Поддержка нескольких языков, проверка утверждений, интеграция LUIS и режим.
ms.localizationpriority: medium
ms.topic: how-to
keywords: Боты виртуального помощника teams
ms.openlocfilehash: e473fd8166be6285ec90d78401b1df028d81b5b0
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104107"
---
# <a name="create-virtual-assistant"></a>Создание виртуального помощника

Виртуальный помощник — это шаблон Майкрософт с открытым исходным кодом, который позволяет создать надежное диалоговое решение, сохраняя полный контроль над взаимодействием с пользователем, фирменной символикой организации и необходимыми данными. [Базовый Виртуальный помощник](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) является базовым стандартным блоком, который объединяет технологии Майкрософт, необходимые для создания Виртуальный помощник, включая пакет [SDK Bot Framework](https://github.com/microsoft/botframework-sdk), [Распознавание речи (LUIS)](https://www.luis.ai/) и [QnA Maker](https://www.qnamaker.ai/). Он также объединяет основные возможности, включая регистрацию навыков, связанные учетные записи, базовое намерение общения, чтобы предложить пользователям широкий спектр беспроблемного взаимодействия и взаимодействия. Кроме того, возможности шаблона включают в себя множество примеров многократно используемых [навыков общения](https://microsoft.github.io/botframework-solutions/overview/skills).  Отдельные навыки интегрированы в Виртуальный помощник, чтобы включить несколько сценариев. С помощью пакета SDK Bot Framework навыки представлены в форме исходного кода, что позволяет настраивать и расширять их по мере необходимости. Дополнительные сведения о навыках Bot Framework см. в разделе "Что [такое навык Bot Framework"](https://microsoft.github.io/botframework-solutions/overview/skills/). В этом документе приведены рекомендации Виртуальный помощник реализации для организаций, создание Teams, связанных Виртуальный помощник, примера кода и ограничений Виртуальный помощник.
На следующем рисунке показан обзор виртуального помощника:

![Виртуальный помощник обзорной схемы](../assets/images/bots/virtual-assistant/overview.png)

Действия с текстовыми сообщениями направляются в связанные навыки Виртуальный помощник с помощью модели [диспетчеризации](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true).

## <a name="implementation-considerations"></a>Рекомендации по реализации

Решение о добавлении Виртуальный помощник включает множество детерминаторов и отличается для каждой организации. Ниже приведены вспомогательные факторы Виртуальный помощник реализации для вашей организации.

* Центральная команда управляет всеми рабочими процессами сотрудников. Она позволяет создавать новые Виртуальный помощник и управлять обновлениями основного интерфейса, включая добавление новых навыков.
* В бизнес-функциях существует несколько приложений, и ожидается, что их число в будущем увеличится.
* Существующие приложения можно настраивать, принадлежат организации и преобразовывать в навыки для Виртуальный помощник.
* Центральная команда по работе с сотрудниками может влиять на настройки существующих приложений. Он также предоставляет необходимые рекомендации по интеграции существующих приложений в качестве навыков в Виртуальный помощник взаимодействия.

На следующем рисунке отображаются бизнес-функции Виртуальный помощник.

![Центральная команда поддерживает помощника, а команды бизнес-функций — навыки](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Создание Teams, ориентированного на Виртуальный помощник

Корпорация Майкрософт опубликовала шаблон [Microsoft Visual Studio для](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) создания виртуальных помощников и навыков. С помощью Visual Studio шаблона можно создать Виртуальный помощник на основе текстового интерфейса с поддержкой ограниченных форматированных карточек с действиями. Мы усовершенствовали базовый Visual Studio, включив Microsoft Teams платформы и отличные Teams приложения. Некоторые из возможностей включают поддержку расширенных адаптивных карточек, модулей задач, команд или групповых чатов и расширений сообщений. Дополнительные сведения о расширении Виртуальный помощник до Microsoft Teams см. в руководстве [по расширению Виртуальный помощник до Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).
На следующем рисунке показана высокоуровневая схема Виртуальный помощник решения.

![Высокоуровневая схема Виртуальный помощник решения](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Добавление адаптивных карточек в Виртуальный помощник

Чтобы правильно отправлять запросы, Виртуальный помощник определить правильную модель LUIS и соответствующий навык, связанный с ней. Однако механизм диспетчеризации нельзя использовать для действий с карточками, так как модель LUIS, связанная с навыком, обучена для текстов действий карточки. Текст действия карточки является фиксированным, предопределенных ключевых слов и не закомментирован пользователем.

Этот недостаток устраняется путем внедрения сведений о навыках в полезные данные действия карточки. Каждый навык должен внедряться `skillId` в поле  `value` действий карточки. Необходимо убедиться, что каждое действие действия карточки содержит соответствующие сведения о навыках, Виртуальный помощник использовать эти сведения для отправки.

Необходимо указать `skillId` в конструкторе, чтобы убедиться, что сведения о навыке всегда присутствуют в действиях карточки.
Пример кода данных действия карточки показан в следующем разделе:

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

Затем класс `SkillCardActionData` в шаблоне Виртуальный помощник для извлечения из `skillId` полезных данных действия карточки.
Фрагмент кода, извлекаемый из  `skillId` полезных данных действия карточки, показан в следующем разделе:

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

Реализация выполняется методом расширения в [классе Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) .
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

Виртуальный помощник может обрабатывать прерывания в тех случаях, когда пользователь пытается вызвать навык, пока активен другой навык. `TeamsSkillDialog`и появились `TeamsSwitchSkillDialog`на основе [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) и [SwitchSkillDialog Bot](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs) Framework. Они позволяют пользователям переключаться между действиями с карточками. Для обработки этого запроса Виртуальный помощник запросит у пользователя подтверждение для переключения навыков:

![Запрос подтверждения при переходе на новый навык](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>Обработка запросов модуля задач

Чтобы добавить возможности модуля задач в Виртуальный помощник, в обработчик действия Виртуальный помощник включены два дополнительных метода: `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync`. Эти методы прослушивают действия, связанные с модулем задач, из Виртуальный помощник, определяют навык, связанный с запросом, и перенаправлять запрос в определенный навык.

Переадресация запросов выполняется с помощью [метода SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true)`PostActivityAsync`. Он возвращает ответ, который `InvokeResponse` анализируется и преобразуется в `TaskModuleResponse` .

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

Аналогичный подход используется для диспетчеризации действий карточек и ответов модуля задач. Данные действия выборки и отправки модуля задачи обновляются, чтобы включить в них данные `skillId`.
Метод расширения действия извлекает `GetSkillId` из `skillId` полезных данных сведения о навыке, который необходимо вызвать.

Фрагмент кода и методы `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` приведены в следующем разделе:

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

Кроме того, необходимо `validDomains` включить все домены навыка в раздел Виртуальный помощник файла манифеста, чтобы модули задач, вызываемые с помощью навыка, отображались правильно.

### <a name="handle-collaborative-app-scopes"></a>Обработка областей приложения для совместной работы

Teams приложения могут существовать в нескольких областях, включая чат 1:1, групповой чат и каналы. Основной шаблон Виртуальный помощник предназначен для чатов 1:1. В рамках процесса подключения Виртуальный помощник запрашивает имя пользователя и сохраняет его состояние. Так как интерфейс подключения не подходит для группового чата или области каналов, он был удален.

Навыки должны обрабатывать действия в нескольких областях, таких как чат 1:1, групповой чат и беседа канала. Если любая из этих областей не поддерживается, навыки должны отвечать соответствующим сообщением.

Следующие функции обработки были добавлены в Виртуальный помощник core:

* Виртуальный помощник можно вызвать без текстовых сообщений из группового чата или канала.
* Перед отправкой сообщения в модуль отправки очищаются скакуниции. Например, удалите необходимые @mention бота.

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

### <a name="handle-message-extensions"></a>Обработка расширений сообщений

Команды для расширения сообщения объявляются в файле манифеста приложения. Пользовательский интерфейс расширения сообщений поддерживается этими командами. Чтобы Виртуальный помощник команду расширения сообщения в качестве присоединенного навыка, манифест Виртуальный помощник должен содержать эти команды. Необходимо добавить команды из манифеста отдельного навыка в Виртуальный помощник файла. Идентификатор команды предоставляет сведения о связанном навыке путем добавления идентификатора приложения навыка через разделитель `:`.

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
    ....   
```

Соответствующий Виртуальный помощник кода файла манифеста показан в следующем разделе:

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

После вызова команд пользователем Виртуальный помощник может определить связанный навык, проанализировав идентификатор команды, `:<skill_id>` обновив действие, удалив лишний суффикс из идентификатора команды и перенаправив его в соответствующий навык. Код навыка не требует обработки дополнительного суффикса. Таким образом, конфликтов между идентификаторами команд между навыками можно избежать. При таком подходе все команды поиска и действия навыка во всех контекстах, такие как **compose**, **commandBox** и **сообщение**, на базе Виртуальный помощник.

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

Некоторые действия расширения сообщения не включают идентификатор команды. Например, содержит `composeExtension/selectItem` только значение действия касания вызова. Чтобы определить связанный навык, `skillId`  присоединяется к каждой карточке элемента при формировании ответа для `OnTeamsMessagingExtensionQueryAsync`. Это похоже на подход к [добавлению адаптивных карточек в Виртуальный помощник](#add-adaptive-cards-to-your-virtual-assistant).

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

В следующем примере показано, как преобразовать шаблон приложения book-a-room в навык Виртуальный помощник: Book-a-room — это Microsoft Teams, который позволяет пользователям быстро находить и резервировать конференц-зал на 30, 60 или 90 минут, начиная с текущего времени. Время по умолчанию — 30 минут. Бот book-a-room использует личные или 1:1 беседы.
На следующем рисунке показан Виртуальный помощник с **навыком книги комнаты**:

![Виртуальный помощник с навыком "книга комнаты"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Ниже приведены разностные изменения, внесенные для преобразования его в навык, присоединенный к Виртуальный помощник. Аналогичные рекомендации применяются для преобразования любого существующего бота версии 4 в навык.

### <a name="skill-manifest"></a>Манифест навыка

Манифест навыка — это JSON-файл, который предоставляет конечную точку обмена сообщениями навыка, идентификатор, имя и другие соответствующие метаданные. Этот манифест отличается от манифеста, используемого для загрузки неопубликованного приложения в Microsoft Teams. Для Виртуальный помощник требуется путь к этому файлу в качестве входных данных для вложения навыка. Мы добавили следующий манифест в папку wwwroot бота.

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

Виртуальный помощник модели диспетчеризации построена на основе моделей LUIS для подключенных навыков. Модель диспетчеризации определяет намерение для каждого текстового действия и находит навык, связанный с ним.

Виртуальный помощник требуется модель LUIS `.lu` навыка в формате входных данных при присоединении навыка. Luis json преобразуется в формат `.lu` с помощью средства botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Бот book-a-room имеет две основные команды для пользователей:

* `Book room`
* `Manage Favorites`

Мы создали модель LUIS, осмыслев эти две команды. Соответствующие секреты должны быть заполнены в `cognitivemodels.json`. Соответствующий JSON-файл LUIS можно найти [здесь](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json).
Соответствующий `.lu` файл показан в следующем разделе:

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

При таком подходе любая команда, `book room` `manage favorites` `Book-a-room` выданная пользователем для Виртуальный помощник или идентифицируемая как команда, связанная с ботом, и перенаправляться в этот навык.
С другой стороны, боту `Book-a-room room` необходимо использовать модель LUIS, чтобы понять эти команды, если они не заполнены. Пример: `I want to manage my favorite rooms`.

### <a name="multi-language-support"></a>Поддержка нескольких языков

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

Чтобы изменить `languages` параметр, обновите команду botskills следующим образом:

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

Виртуальный помощник используется для `SetLocaleMiddleware` определения текущего языкового стандарта и вызова соответствующей модели диспетчеризации. Действие Bot Framework имеет поле языкового стандарта, используемого этим ПО промежуточного слоя. Вы также можете использовать то же самое для своего навыка. Бот book-a-room не использует это ПО промежуточного слоя и вместо этого получает языковой стандарт из сущности [clientInfo действия Bot Framework](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).

### <a name="claim-validation"></a>Проверка утверждений

Мы добавили [claimsValidator,](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) чтобы ограничить вызывающие объекты навыком. Чтобы разрешить Виртуальный помощник этот навык, `AllowedCallers` `appsettings` заполните массив с помощью этого Виртуальный помощник идентификатора приложения.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

Массив разрешенных вызывающих объектов может ограничить доступ потребителей навыка к навыку. Добавьте одну запись `*` в этот массив, чтобы принимать вызовы от любого потребителя навыка.

```
"AllowedCallers": [ "*" ],
```

Дополнительные сведения о добавлении проверки утверждений в навык см. в разделе "Добавление проверки [утверждений в навык"](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).

### <a name="limitation-of-card-refresh"></a>Ограничение обновления карточки

Обновление действия, например обновление карточки, пока не поддерживается через Виртуальный помощник (проблема [с GitHub](https://github.com/microsoft/botbuilder-dotnet/issues/3686)). Таким образом, мы заменили все вызовы обновления карточек `UpdateActivityAsync` публикацией новых вызовов карт `SendActivityAsync`.

### <a name="card-actions-and-task-module-flows"></a>Действия с карточками и потоки модулей задач

Чтобы перенаправлять действия карточки или действия модуля задач в связанный навык, навык должен быть `skillId` внедрен в него.
`Book-a-room` Действие bot card, получение и отправка полезных данных модуля задачи изменяются для хранения `skillId` в качестве параметра.

Дополнительные сведения см. [в этом](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) разделе этой документации.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Обработка действий из области группового чата или канала

`Book-a-room bot` предназначен только для частных чатов, таких как личные или 1:1. Так как мы настроили Виртуальный помощник для поддержки областей группового чата и каналов, Виртуальный помощник должны вызываться из областей канала, `Book-a-room` поэтому бот должен получать действия для той же области. Поэтому `Book-a-room`бот настраивается для обработки этих действий. Вы можете найти методы проверки `OnMessageActivityAsync` обработчика `Book-a-room` действий бота.

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

Вы также можете использовать существующие навыки из [репозитория решений Bot Framework](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) или создать новый навык с нуля. Сведения о создании навыка см. в руководствах [по созданию нового навыка](https://microsoft.github.io/botframework-solutions/overview/skills/). Документацию Виртуальный помощник архитектуры навыков и навыков см. Виртуальный помощник [и архитектуре навыков](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).  

## <a name="limitations-of-virtual-assistant"></a>Ограничения Виртуальный помощник

* **EndOfConversation**: навык должен отправить `endOfConversation` действие по завершении беседы. В зависимости от действия Виртуальный помощник контекст с определенным навыком и возвращается Виртуальный помощник корневого контекста. Для бота book-a-room нет четкого состояния завершения беседы. Поэтому мы не отправляли сообщения `endOfConversation` от `Book-a-room` бота, и когда пользователь хочет вернуться к корневому контексту, он может просто сделать это с помощью `start over` команды.  
* **Обновление карточки**: обновление карточки пока не поддерживается через Виртуальный помощник.  
* **Расширения сообщений**:
  * В настоящее время Виртуальный помощник может поддерживать не более десяти команд для расширений сообщений.
  * Настройка расширений сообщений не предназначена для отдельных команд, а для всего расширения. Это ограничивает конфигурацию для каждого отдельного навыка с помощью Виртуальный помощник.
  * Идентификаторы команд расширений сообщений имеют максимальную длину [64](../resources/schema/manifest-schema.md#composeextensions) символа, а для внедрения сведений о навыках используется 37 символов. Таким образом, обновленные ограничения для идентификатора команды ограничены 27 символами.

Вы также можете использовать существующие навыки из [репозитория решений Bot Framework](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) или создать новый навык с нуля. Руководства для последующих версий можно найти [здесь](https://microsoft.github.io/botframework-solutions/overview/skills/). См. [документацию по архитектуре](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) Виртуальный помощник и навыков.

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **C#**  **.NET** |
|----------|-----------------|---------------------------|
| Обновленный шаблон Visual Studio | Настраиваемый шаблон для поддержки возможностей команд. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| Код навыка бота book-a-room | Позволяет быстро находить и резервировать конференц-зал в пути. | [Просмотр](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Интеграция веб-приложений](~/samples/integrate-web-apps-overview.md)
* ["Книга в комнате"](app-templates.md#app-template-code-samples)
* [Microsoft Teams бота](../bots/what-are-bots.md)
