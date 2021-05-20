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
# <a name="create-virtual-assistant"></a>Создание виртуального помощника 

Virtual Assistant — это шаблон с открытым исходным кодом корпорации Майкрософт, который позволяет создавать надежное решение для хранения, сохраняя при этом полный контроль над пользовательским опытом, организационным брендингом и необходимыми данными. Основной [шаблон Virtual Assistant является](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) основным строительным блоком, который объединяет технологии Microsoft, необходимые для создания виртуального помощника, [включая Bot Framework SDK,](https://github.com/microsoft/botframework-sdk) [Language Understanding (LUIS)](https://www.luis.ai/) [и йnA Maker.](https://www.qnamaker.ai/) Он также объединяет основные возможности, включая регистрацию навыков, связанные учетные записи, основные разговорные намерения предложить широкий спектр бесшовных взаимодействий и опыта для пользователей. Кроме того, возможности шаблона включают богатые примеры многоразовых разговорных [навыков.](https://microsoft.github.io/botframework-solutions/overview/skills)  Индивидуальные навыки интегрированы в решение Virtual Assistant для нескольких сценариев. Используя Bot Framework SDK, навыки представлены в форме исходных кодов, что позволяет настроить и расширить по мере необходимости. Для получения дополнительной информации о навыках Bot Framework, [см.](https://microsoft.github.io/botframework-solutions/overview/skills/) Этот документ поможет вам в реализации виртуального помощника для организаций, как создать Teams виртуальный помощник, связанный пример, образец кода и ограничения виртуального помощника.
Следующее изображение отображает обзор виртуального помощника:

![Диаграмма обзора виртуального помощника](../assets/images/bots/virtual-assistant/overview.png)

Действия текстовых сообщений направляются к связанным навыкам ядром Virtual Assistant с помощью [модели отправки.](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) 

## <a name="implementation-considerations"></a>Соображения осуществления

Решение о добавление виртуального помощника включает в себя множество детерминантов и отличается для каждой организации. Поддерживающие факторы реализации виртуального помощника для вашей организации следующие:

* Центральная команда управляет всем опытом сотрудников. Он имеет возможность создавать виртуальный опыт помощника и управлять обновлениями для основного опыта, включая добавление новых навыков.
* Несколько приложений существуют в разных бизнес-функциях, и ожидается, что в будущем их число будет расти.
* Существующие приложения настраиваются, принадлежат организации и преобразуются в навыки виртуального помощника.
* Центральная команда сотрудников может влиять на настройки существующих приложений. Он также предоставляет необходимые рекомендации для интеграции существующих приложений в качестве навыков в виртуальном опыте помощника.

Следующее изображение отображает бизнес-функции виртуального помощника: 

![Центральная команда поддерживает помощника, а команды бизнес-функций вносят навыки](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Создание Teams виртуального помощника, ориентированных на систему

Корпорация Майкрософт опубликовала [Visual Studio для создания](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) виртуальных помощников и навыков. С помощью Visual Studio шаблона, вы можете создать виртуальный помощник, питание от текстового опыта с поддержкой ограниченных богатых карт с действиями. Мы улучшили базовый шаблон Visual Studio, чтобы включить Microsoft Teams платформы и мощность большой Teams приложений. Некоторые из этих возможностей включают поддержку богатых адаптивных карт, модулей задач, групп или групповых чатов, а также расширений обмена сообщениями. Для получения дополнительной информации о расширении виртуальный помощник Microsoft Teams, [с Microsoft Teams м.](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)    
Следующее изображение отображает диаграмму высокого уровня решения Virtual Assistant:

![Диаграмма высокого уровня решения виртуального помощника](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Добавьте адаптивные карты к своему виртуальному помощнику

Чтобы правильно отправлять запросы, ваш виртуальный помощник должен определить правильную модель LUIS и соответствующие навыки, связанные с ней. Тем не менее, механизм отправки не может быть использован для действий карты действий, как модель LUIS, связанные с навыком, обучается для текстов действия карты. Тексты действий карты являются фиксированными, заранее определенными ключевыми словами и не комментируются пользователем.

Этот недостаток решается путем встраивания информации о навыке в полезную нагрузку действия карты. Каждый навык должен `skillId` вставляться  `value` в поле карточных действий. Вы должны убедиться, что каждая акция карты несет соответствующую информацию о навыках, и виртуальный помощник может использовать эту информацию для отправки.

Вы должны предоставить `skillId` в конструктор, чтобы убедиться, что информация о навыке всегда присутствует в действиях карты.
Образец кода данных действия карты отображается в следующем разделе:
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

Далее `SkillCardActionData` класс в шаблоне Virtual Assistant вводится для извлечения из `skillId` полезной нагрузки действия карты.
Фрагмент кода для извлечения из  `skillId` полезной нагрузки действия карты показан в следующем разделе:

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

Реализация выполнена методом расширения в классе [Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)
Фрагмент кода для извлечения  `skillId` из данных действия карты показан в следующем разделе:

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

### <a name="handle-interruptions"></a>Перебои в работе

Виртуальный помощник может обрабатывать перерывы в тех случаях, когда пользователь пытается вызвать навык, в то время как другой навык в настоящее время активен. `TeamsSkillDialog`, и `TeamsSwitchSkillDialog` представлены на основе Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) и [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs). Они позволяют пользователям переключать опыт навыков с карточных действий. Чтобы справиться с этим запросом, Виртуальный помощник подсказывает пользователю сообщение о подтверждении, чтобы переключить навыки:

![Подтверждение подсказки при переходе на новый навык](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>Запросы модуля задач

Чтобы добавить возможности модуля задач в виртуальный помощник, два дополнительных метода включены в обработчик активности Виртуального помощника: `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync` . Эти методы прослушивают действия, связанные с модулем задач, от Virtual Assistant, определяют навыки, связанные с запросом, и переопределяют запрос на идентифицированный навык. 

Перепродающая перемотка запросов [делается с помощью метода SkillHttpClient.](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) `PostActivityAsync` Он возвращает ответ, `InvokeResponse` который анализируется и преобразуется в `TaskModuleResponse` .


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

Аналогичный подход следует для отправки карточных действий и ответов модуля задач. Модуль задач извлечения и отправки данных действий обновляется, чтобы включить `skillId` . Метод расширения активности `GetSkillId` извлекает из `skillId` полезной нагрузки, которая предоставляет подробную информацию о навыках, которые необходимо вызвать.

Фрагмент кода и `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` методы приведены в следующем разделе:

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

Кроме того, вы должны включить все области навыков в `validDomains` раздел в файле манифеста виртуального помощника, чтобы модули задач, вызванные с помощью навыка, должным образом визуализировать.

### <a name="handle-collaborative-app-scopes"></a>Обработать совместные области приложений

Teams могут существовать в нескольких сферах, включая чат 1:1, групповой чат и каналы. Основной шаблон Virtual Assistant предназначен для чатов 1:1. В рамках бортового опыта Виртуальный помощник подсказывает пользователям имя и поддерживает состояние пользователя. Так как этот опыт посадки не подходит для группового чата или каналов, он был удален.

Навыки должны обрабатывать действия в нескольких сферах, таких как чат 1:1, групповой чат и разговор по каналу. Если какая-либо из этих областей не поддерживается, навыки должны отвечать соответствующим сообщением.

Следующие функции обработки были добавлены в ядро Virtual Assistant:

* Виртуальный помощник может быть вызван без каких-либо текстовых сообщений из группового чата или канала.
* Артикуляции очищаются перед отправкой сообщения в диспетчерский модуль. Например, удалите необходимые @mention бота.

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

### <a name="handle-messaging-extensions"></a>Ручка расширений обмена сообщениями

Команды для расширения обмена сообщениями объявлены в файле манифеста приложения. Пользовательский интерфейс расширения обмена сообщениями питается от этих команд. Для виртуального помощника для питания команды расширения обмена сообщениями в качестве прилагаемого навыка, собственный манифест виртуального помощника должен содержать эти команды. Вы должны добавить команды из манифеста индивидуального навыка в манифест виртуального помощника. Идентификатор команды предоставляет информацию о связанном навыке, притяв идентификатор приложения навыка через сепаратор. `:`

Фрагмент из файла манифеста навыка показан в следующем разделе:

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

Соответствующий фрагмент кода виртуального помощника показан в следующем разделе:

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

После того, как команды вызываются пользователем, виртуальный помощник может определить связанный навык, разобрать идентификатор команды, обновить действие, удалив дополнительный суффикс `:<skill_id>` из идентификатора команды, и перейти его к соответствующему навыку. Код для навыка не требует обработки дополнительного суффикса. Таким образом, избегаются конфликты между командными СВу между навыками. При таком подходе все команды поиска и действия навыка во всех контекстах, таких как **compose**, **commandBox**, **и сообщение** питаются от виртуального помощника.

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

Некоторые действия по расширению обмена сообщениями не включают идентификатор команды. Например, `composeExtension/selectItem` содержится только значение действия касаться вызова. Чтобы определить связанный навык, `skillId`  прилагается к каждой карте элемента при формировании ответа для `OnTeamsMessagingExtensionQueryAsync` . Это похоже на подход к добавлению [адаптивных карт к вашему виртуальному помощнику.](#add-adaptive-cards-to-your-virtual-assistant)

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

В следующем примере показано, как преобразовать шаблон приложения Book-a-room в навык виртуального помощника: Book-a-room — это Microsoft Teams, который позволяет пользователям быстро находить и резервировать зал заседаний на 30, 60 или 90 минут, начиная с текущего времени. Время по умолчанию составляет 30 минут. Бот-комната в книге прицелы для личных или 1:1 разговоров. Следующее изображение отображает виртуальный помощник с **книгой номер мастерство:**

![Виртуальный помощник с навыком «забронируйте комнату»](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Ниже приведены изменения дельты, введенные для преобразования его в навык, который прилагается к виртуальному помощнику. Аналогичные руководящие принципы следуют, чтобы преобразовать любой существующий бот v4 в навык.

### <a name="skill-manifest"></a>Манифест навыков

Манифест навыков — это файл JSON, который предоставляет конечную точку обмена сообщениями, идентификатор, имя и другие соответствующие метаданные навыков. Этот манифест отличается от манифеста, используемого для боковой загрузки приложения в Microsoft Teams. Виртуальный помощник требует путь к этому файлу в качестве ввода, чтобы прикрепить навык. Мы добавили следующий манифест в папку wwwroot бота.

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

### <a name="luis-integration"></a>ИНТЕГРАЦИЯ LUIS

Модель отправки виртуального помощника построена поверх прикрепленных навыков' МОДЕЛ моделей LUIS. Модель отправки определяет цель каждого текстового действия и находит навыки, связанные с ним.

Виртуальный помощник требует навыка LUIS модели в `.lu` формате в качестве ввода при присоединении навыка. LUIS json преобразуется в формат `.lu` с помощью инструмента botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Book-a-room bot имеет две основные команды для пользователей:

- `Book room`
- `Manage Favorites`

Мы построили модель LUIS, понимая эти две команды. Соответствующие секреты должны быть заселены `cognitivemodels.json` в . Соответствующий файл LUIS JSON находится [здесь](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json).
Соответствующий `.lu` файл отображается в следующем разделе:

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

При этом подходе любая команда, выданная пользователем виртуальному помощнику, связана с ним или идентифицирована как `book room` `manage favorites` команда, `Book-a-room` связанная с ботом, и направляется на этот навык.
С другой стороны, `Book-a-room room` бот должен использовать модель LUIS, чтобы понять эти команды, если они не на типах заполнены. Пример: `I want to manage my favorite rooms`.

### <a name="multi-language-support"></a>Многоязычная поддержка

В качестве примера создается модель LUIS только с английской культурой. Вы можете создать модели LUIS, соответствующие другим языкам, и добавить запись `cognitivemodels.json` в .

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

Параллельно добавляйте соответствующий `.lu` файл в путь luisFolder. Структура фолдеров должна быть следующей:

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Чтобы изменить `languages` параметр, обновив команду botskills следующим образом:

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

Виртуальный помощник использует `SetLocaleMiddleware` для определения текущей локализации и вызова соответствующей модели отправки. Бот фреймворка деятельности имеет локальное поле, которое используется этим средним. Вы можете использовать то же самое для вашего мастерства, а также. Book-a-room bot не использует это среднее программное обеспечение и вместо этого получает локализацию от компании [clientInfo деятельности Bot.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)

### <a name="claim-validation"></a>Проверка претензий

Мы добавили [претензииValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) ограничить абонентов к мастерству. Чтобы виртуальный помощник мог назвать этот навык, заселите `AllowedCallers` массив `appsettings` с помощью идентификатора приложения виртуального помощника.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

Разрешенная массив абонентов может ограничить, какие навыки потребители могут получить доступ к навыку. Добавьте одну запись `*` в этот массив, чтобы принимать звонки от любого потребителя навыков.

```
"AllowedCallers": [ "*" ],
```

Для получения дополнительной информации о добавлении проверки претензий к навыку, [см.](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)

### <a name="limitation-of-card-refresh"></a>Ограничение обновления карты 

Обновление активности, например обновление карты, пока не поддерживается с помощью virtual Assistant[(выпуск github).](https://github.com/microsoft/botbuilder-dotnet/issues/3686) Таким образом, мы заменили все звонки обновления карты с `UpdateActivityAsync` размещением новых телефонных звонков карты `SendActivityAsync` .

### <a name="card-actions-and-task-module-flows"></a>Потоки карточных действий и модуля задач

Чтобы перемотать действия карты или действия модуля задач на связанные навыки, навык должен `skillId` вставляться в него.
`Book-a-room` Бот-карты действий, модуль задач извлечения и представить действия полезной нагрузки изменены, чтобы `skillId` содержать в качестве параметра. 

Для получения дополнительной информации [обратитесь к](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) этому разделу из этой документации.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Обработать действия из сферы группового чата или канала

`Book-a-room bot` предназначен для приватных чатов, таких как только личная или область 1:1. Так как мы настроили Виртуального помощника для поддержки группового чата и каналов, Виртуальный помощник должен быть вызван из областей канала и, таким образом, `Book-a-room` бот должен получать действия для той же области. Таким `Book-a-room` образом, бот настроен для обработки этих действий. Вы можете найти проверку в `OnMessageActivityAsync` методах `Book-a-room` обработчика активности бота.

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

Вы также можете использовать существующие навыки [из репозитория Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) или создать новый навык с нуля. Для создания новых навыков, [см. учебники для создания новых навыков](https://microsoft.github.io/botframework-solutions/overview/skills/). Для виртуального помощника и навыков архитектуры документации, см[Виртуальный помощник и навыки архитектуры](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).  

## <a name="limitations-of-virtual-assistant"></a>Ограничения виртуального помощника 

* **EndOfConversation**: Навык должен отправить `endOfConversation` действие, когда он заканчивает разговор. Основываясь на действиях, виртуальный помощник заканчивает контекст с этим конкретным навыком и возвращается в корневой контекст виртуального помощника. Для бота Book-a-room нет четкого состояния, в котором разговор закончился. Поэтому мы не послали `endOfConversation` от `Book-a-room` бота, и когда пользователь хочет вернуться к корневому контексту они могут просто сделать это по `start over` команде.  
* **Обновление карты**: Обновление карты пока не поддерживается через виртуального помощника.  
* **Расширения сообщений**:
  * В настоящее время виртуальный помощник может поддерживать не более десяти команд для расширения обмена сообщениями.
  * Конфигурация расширений обмена сообщениями не связана с отдельными командами, а для всего самого расширения. Это ограничивает конфигурацию для каждого отдельного навыка через виртуального помощника.
  * Данные команды расширения сообщений имеют максимальную длину [64 символа,](../resources/schema/manifest-schema.md#composeextensions) а 37 символов используются для встраивания информации о навыках. Таким образом, обновленные ограничения для идентификатора команды ограничены 27 символами.

Вы также можете использовать существующие навыки [из репозитория Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) или создать новый навык с нуля. Учебники на более поздний день можно найти [здесь](https://microsoft.github.io/botframework-solutions/overview/skills/). Пожалуйста, обратитесь [к документации](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) для виртуального помощника и архитектуры навыков.

## <a name="code-sample"></a>Пример кода

| **Название образца** | **Описание** | **C#** | **.NET** |
|----------|-----------------|----------|------------------|
| Обновленный шаблон визуальной студии | Индивидуальный шаблон для поддержки возможностей команд. | [View](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| Код навыков бота в книге-комнате | Позволяет быстро найти и забронировать зал заседаний на ходу. |  | [View](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |


## <a name="see-also"></a>См. также

- [Интеграция веб-приложений](~/samples/integrate-web-apps-overview.md)

- [Книга-комната](app-templates.md#book-a-room)

- [Microsoft Teams бот](../bots/what-are-bots.md)