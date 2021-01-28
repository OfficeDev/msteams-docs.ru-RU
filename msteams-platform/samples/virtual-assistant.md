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
# <a name="virtual-assistant-for-microsoft-teams"></a>Виртуальный помощник для Microsoft Teams

Виртуальный помощник — это шаблон Microsoft с открытым исходным кодом, который позволяет создавать надежное решение для бесед, сохраняя полный контроль над пользовательским интерфейсом, фирмой и необходимыми данными. Основной [](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) шаблон виртуального помощника — это базовый базовый блок, который объединяет технологии Майкрософт, необходимые для создания виртуального помощника, в том числе bot [Framework SDK,](https://github.com/microsoft/botframework-sdk) [language Understanding (КОДИБ)](https://www.luis.ai/)и [QnA Maker,](https://www.qnamaker.ai/)а также основные возможности, включая регистрацию навыков, связанные учетные записи, базовое намерение для общения, чтобы предоставить конечным пользователям широкий спектр удобных взаимодействий и возможностей. Кроме того, возможности шаблона включают в себя богатые примеры навыков для повторного работы с [беседами.](https://microsoft.github.io/botframework-solutions/overview/skills)  Отдельные навыки можно интегрировать в решение виртуального помощника для реализации нескольких сценариев. С помощью SDK Bot Framework skills представлены в форме с исходным кодом, что позволяет настраивать и расширять их по мере необходимости. See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).

![Обзорная схема виртуального помощника](../assets/images/bots/virtual-assistant/overview.png)

Действия текстовых сообщений перенаправлются на связанные навыки ядром виртуального помощника с помощью модели [отправки.](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) 

## <a name="implementation-considerations"></a>Вопросы реализации

Решение о добавлении виртуального помощника может включать множество детерминант и отличаться для каждой организации. Вот факторы, которые поддерживают реализацию виртуального помощника для вашей организации:

- Центральная команда управляет всеми возможностями сотрудников и может создавать виртуальный помощник и управлять обновлениями для основного опыта, включая добавление новых навыков.
- Существует несколько приложений в различных бизнес-функциях и/или ожидается, что их число будет увеличиваться в будущем.
- Существующие приложения можно настраивать, принадлежат организации и могут преобразовывать в навыки для виртуального помощника.
- Центральная группа сотрудников может влиять на настройки существующих приложений и предоставлять необходимые инструкции по интеграции существующих приложений в качестве навыков в виртуальном помощнике

![Центральная команда поддерживает помощника, а группы бизнес-функций способствуют работе с навыками](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Создание виртуального помощника для Teams

Корпорация Майкрософт опубликовала шаблон [Visual Studio для](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) создания виртуальных помощников и навыков. С помощью Visual Studio вы можете создать виртуальный помощник на основе текстового опыта с поддержкой ограниченных форматирований карточек с действиями. Мы усовершенствовали базовый Visual Studio, включив в него возможности платформы Microsoft Teams и отличные возможности приложений Teams. Некоторые возможности включают поддержку карточек с богатыми возможностями, модулей задач, командных или групповых чатов и расширений обмена сообщениями. *См. также,* [руководство. Расширение виртуального помощника до Microsoft Teams.](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)

![Высокоуровневая схема решения виртуального помощника](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Добавление адаптивных карточек в виртуальный помощник

Для правильной отправки запросов виртуальный помощник должен определить правильную модель и соответствующие навыки, связанные с ними. Однако механизм отправки нельзя использовать для действий с карточками, так как модель СДРЕС, связанная с навыками, может не быть обучена работе с текстами действий карточки, так как это фиксированные, предварительно определенные ключевые слова, а не изрекаемые пользователем.

Мы устраили эту проблему, встраив сведения о квалификации в полезной нагрузке действия карточки. Все навыки должны быть `skillId` встраиты  `value` в поле действий карт. Это лучший способ убедиться, что каждое действие карточки содержит соответствующую информацию о квалификации и виртуальный помощник может использовать эту информацию для отправки.

Ниже приведен пример данных о действии карточки. Предоставляя данные в конструкторе, мы гарантируем, что информация о квалификации всегда `skillId` присутствует в действиях карточки.

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

Далее мы представляем класс в шаблоне виртуального помощника для извлечения из `SkillCardActionData` `skillId` полезных полезных нагрузки действия карточки.

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

Ниже приведен фрагмент кода для извлечения из  `skillId` данных действий карточки. Мы реализовали его как метод расширения в [классе Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)

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

### <a name="handle-interruptions-gracefully"></a>Корректная обработка прерываний

Виртуальный помощник может обрабатывать прерывания в тех случаях, когда пользователь пытается вызвать навыков, когда в настоящее время активен другой навыков. Мы ввели и, на основе `TeamsSkillDialog` `TeamsSwitchSkillDialog` SkillDialog и [SwitchS skillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)в [Bot](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) Framework, чтобы позволить пользователям переключаться навыков из действий карт. Для обработки этого запроса виртуальный помощник запрашивает у пользователя подтверждение для переключения навыков.

![Запрос подтверждения при переходе на новый уровень квалификации](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a>Обработка запросов модулей задач

Чтобы добавить возможности модуля задач в виртуальный помощник, в обработок действий виртуального помощника включены два дополнительных метода: `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync` . Эти методы прослушивают действия, связанные с модулем задачи, из виртуального помощника, определяют навыки, связанные с запросом, и переназначили запрос на указанный уровень квалификации. 

Переадтранслировать запросы можно с помощью метода [SkillHttpClient.](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable) `PostActivityAsync` Он возвращает ответ, который будет `InvokeResponse` разобрано и преобразовано в `TaskModuleResponse` .

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

Аналогичный подход следует для отправки действий карт и ответов модуля задачи. Данные о действиях и извлечении и отправке модуля задачи будут обновлены, чтобы включить `skillId` их. Метод расширения действия извлекается из полезных данных, что дает подробные сведения о `GetSkillId` `skillId` навыков, которые необходимо вызвать.

Ниже приведен фрагмент кода для методов `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` и методов.

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

Кроме того, все домены навыков должны быть включены в раздел в файле манифеста виртуального помощника, чтобы модули задач, вызывались посредством правильной отрисовки `validDomains` навыков.

### <a name="handling-collaborative-app-scopes"></a>Обработка областей совместной работы приложений

Приложения Teams могут существовать в различных сферах, включая 1:1 чат, групповой чат и каналы. Основной шаблон виртуального помощника предназначен для чатов 1:1. В рамках пользовательского интерфейса виртуальный помощник запросит имя и поддерживает состояние пользователя. Так как этот подход не подходит для областей группового чата или канала, он был удален.

Навыки должны обрабатывать действия в различных сферах (1:1 чат, групповой чат и беседа в канале). Если какие-либо из этих областей не поддерживаются, навыки должны отвечать соответствующим сообщением.

В ядро виртуального помощника добавлены следующие функции обработки:

- Виртуальный помощник можно вызвать без текстовых сообщений из группового чата или канала.
- Перед отправкой сообщения в модуль отправки удаляются @mention бота.

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

Команды для расширения обмена сообщениями объявляются в файле манифеста приложения. Пользовательский интерфейс расширения обмена сообщениями, на питание от этих команд. Чтобы виртуальный помощник встроил команду расширения обмена сообщениями (как присоединенный навык), манифест виртуального помощника должен содержать эти команды. Команды из манифеста отдельного навыков также следует добавить в манифест виртуального помощника. Этот ИД команды предоставляет сведения о связанном с ним навыков посредством с помощью сепаратора ( `:` ).

Ниже приведен фрагмент из файла манифеста навыков.

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

Ниже приведен соответствующий фрагмент кода файла манифеста виртуального помощника.

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

После того как команды вызываются пользователем, виртуальный помощник может определить соответствующий навык, выполнив разбор ИД команды, обновив действие, удалив дополнительный суффикс ( ) из ИД команды и перенаполнив его на соответствующий `:<skill_id>` уровень. Код для навыков не должен обрабатывать дополнительный суффикс, поэтому конфликтов между кодами команд между навыками не требуется. При таком подходе виртуальный помощник может использовать все команды поиска и действий навыки во всех контекстах ("compose", "commandBox" и "message").

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

Некоторые действия расширения обмена сообщениями не включают в себя ИД команды. Например, `composeExtension/selectItem` содержит только значение действия касания вызова. Чтобы определить связанное навыков, `skillId`  присоединяется к каждой карточке элемента при формировании ответа для `OnTeamsMessagingExtensionQueryAsync` . (Это аналогично способу добавления адаптивных [карточек в виртуальный помощник.](#add-adaptive-cards-to-your-virtual-assistant)

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a>Пример. Преобразование шаблона приложения "Книга в комнату" в навыки виртуального помощника

[Book-a-room](app-templates.md#book-a-room) — это бот [Microsoft Teams,](../bots/what-are-bots.md) который позволяет пользователям быстро находить и резервировать комнату для собраний на 30 (по умолчанию), 60 или 90 минут, начиная с текущего времени. Бот book-a-room имеет область личных или 1:1 бесед.

![Виртуальный помощник с навыками "книги комнаты"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Ниже представлены изменения изменений, внесенные для преобразования его в навыки, которые можно прикрепить к виртуальному помощнику. Аналогичные рекомендации можно использовать для преобразования любого существующего бота v4 в навыки.

### <a name="skill-manifest"></a>Манифест навыков

Манифест навыков — это JSON-файл, который предоставляет конечную точку обмена сообщениями, ид, имя и другие релевантные метаданные навыки (этот манифест отличается от манифеста, используемого для загрузки неокрепленного приложения в Microsoft Teams). Виртуальный помощник требует путь к этому файлу в качестве входных данных для вложенного навыков. Мы добавили следующий манифест в папку wwwroot бота.

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

### <a name="luis-integration"></a>Интеграция с ИТ-специалистом

Модель диспетчеризации виртуального помощника построена на основе моделей СЕТ С присоединенными навыками. Модель диспетчера определяет назначение для каждого текстового действия и находит навыки, связанные с ним.

Для работы с виртуальным помощником требуется модель СЕТ по навыкам (в формате) в качестве входных данных при присоединении `.lu` навыков. МЕТОД JSON в ФОРМАТ МОЖНО преобразовать с `.lu` помощью средства botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Бот book-a-room имеет две основные команды для пользователей:

- `Book room`
- `Manage Favorites`

Мы создали модель СЕТ, которая понимает эти две команды. Соответствующие секреты должны быть заполнены `cognitivemodels.json` в . Здесь можно найти соответствующий [](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) JSON-файл СДРЕС, и так выглядит `.lu` соответствующий файл.

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

При таком подходе любые проблемы с командами, связанные с виртуальным помощником или связанные с ним, могут быть определены как команды, связанные с ботом `book room` book-a-room, и переназначаются на этот `manage favorites` опыт.
С другой стороны, бот book-a-room должен использовать модель СЕТ, чтобы понять эти команды, если они не введите как есть (например: `I want to manage my favorite rooms` ).

### <a name="multi-language-support"></a>Поддержка нескольких языков

В этом примере мы создали модель ТОЛЬКО с языком в английском языке. Вы можете создать модели СЕТ, соответствующие другим языкам, и добавить запись в `cognitivemodels.json` .

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

Параллельно добавьте соответствующий `.lu` файл в путь к папке. Структура папок должна быть следующим образом:

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Чтобы изменить параметр, обновим команду botskills `languages` следующим образом:

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

Виртуальный помощник использует `SetLocaleMiddleware` для определения текущего региональных 100-х и вызова соответствующей модели диспетчера. (Действие bot framework имеет поле locale, которое используется этим ПО по середине.) Мы рекомендуем использовать то же самое и для вашего навыков. Бот book-a-room не использует это по среднему по и вместо этого получает локали из объекта [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)действия bot framework.

### <a name="claim-validation"></a>Проверка утверждений

Мы добавили [claimsValidator,](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) чтобы ограничить звоняющих навыками. Чтобы виртуальный помощник вызывал этот навык, заполняйте массив с помощью этого конкретного ИД `AllowedCallers` `appsettings` приложения виртуального помощника.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

Разрешенный массив вызывающих может ограничить доступ потребителей навыков к навыкам. Добавьте одну запись `*` в этот массив, чтобы принимать вызовы от любого потребителя навыков.

```
"AllowedCallers": [ "*" ],
```
Подробную документацию по добавлению проверки утверждений в квалификацию можно найти [здесь.](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)

### <a name="card-refresh-limitation"></a>Ограничение на обновление карты

Обновление действия (обновление карты) еще не поддерживается с помощью виртуального помощника[(проблема с github).](https://github.com/microsoft/botbuilder-dotnet/issues/3686) Таким образом, мы заменили все вызовы обновления карты () на `UpdateActivityAsync` отправку новых вызовов карт( `SendActivityAsync` ).

### <a name="card-actions-and-task-module-flows"></a>Действия карточки и потоки модуля задач

Чтобы перенаадтрить действия карточки или действия модуля задачи связанному с ним навыкам, необходимо встраить `skillId` в него навыки.
Действие бота book-a-room, извлечение и отправка полезной нагрузки модуля задачи изменены в качестве `skillId` параметра. 

Дополнительные сведения можно [получить в этом](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) разделе из этой документации.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Обработка действий из области группового чата или канала

Бот book-a-room предназначен только для личных чатов (личных/1:1). Так как мы настроили виртуальный помощник для поддержки группового чата и областей каналов, виртуальный помощник может быть вызван из этих областей, поэтому бот book-a-room может получить действия для того же самого. Поэтому бот book-a-room настраивается для обработки этих действий. Проверка была установлена в методах обработки действий бота `OnMessageActivityAsync` book-a-room.

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

Вы также можете использовать существующие навыки из [репозитория решений Bot Framework](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) или создать новый навыки с нуля. Учебники по последующим вопросам можно найти [здесь.](https://microsoft.github.io/botframework-solutions/overview/skills/) Обратитесь к [документации по](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   виртуальному помощнику и архитектуре навыков.

## <a name="sample-code-to-get-started"></a>Пример кода для начала работы

- [Обновленный шаблон Visual Studio](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [Код навыков бота "Книга в комнате"](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a>Известные ограничения для виртуального помощника

- **EndOfConversation**. Навыки должны отправлять действия `endOfConversation` по завершению беседы. На основе этого действия виртуальный помощник завершает контекст определенным навыков и возвращается в контекст (корневой) виртуального помощника. Для бота book-a-room нет четкого состояния, в котором можно бы закончить беседу. Поэтому мы не отправляли данные из бота book-a-room, и когда пользователь хочет вернуться в корневой контекст, он может просто сделать это `endOfConversation` с помощью `start over` команды.
- **Обновление карточки.** Обновление карточки пока не поддерживается с помощью виртуального помощника.
- **Расширения обмена сообщениями.:**
  - В настоящее время виртуальный помощник может поддерживать не более десяти команд для расширений обмена сообщениями.
  - Настройка расширений обмена сообщениями не зависит от отдельных команд, а для всего расширения. Это ограничивает конфигурацию для каждого отдельного навыков с помощью виртуального помощника.
  - ИД команд расширений обмена сообщениями имеют максимальную длину [64](../resources/schema/manifest-schema.md#composeextensions) символа, а для встраиванию сведений о навыках будет использоваться 37 символов. Таким образом, обновленные ограничения для ИД команды ограничены 27 символами.
>
>
