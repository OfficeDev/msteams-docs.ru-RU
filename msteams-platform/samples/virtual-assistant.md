---
title: Создание виртуального помощника
description: Узнайте, как создать Виртуальный помощник для Microsoft Teams с помощью примеров и фрагментов кода с такими функциями, как адаптивные карты; обработка перерывов, запросов модулей задач, областей совместных приложений и расширений сообщений; использование манифеста навыков; Поддержка нескольких языков, проверка утверждений, интеграция LUIS и режим.
ms.localizationpriority: medium
ms.topic: how-to
keywords: команды виртуальных помощников-ботов
ms.openlocfilehash: 2082e160387bd6ad80fa526e3dab39b385a6e955
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889232"
---
# <a name="create-virtual-assistant"></a>Создание виртуального помощника

Виртуальный помощник является шаблоном Microsoft с открытым исходным кодом, который позволяет создавать надежное решение для беседы, сохраняя полный контроль над пользовательским опытом, организационным брендингом и необходимыми данными. Базовый [Виртуальный помощник](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) является основным строительным блоком, который объединяет технологии Майкрософт, необходимые для создания Виртуальный помощник, в том числе bot [Framework SDK,](https://github.com/microsoft/botframework-sdk) [Language Understanding (LUIS)](https://www.luis.ai/)и [QnA Maker.](https://www.qnamaker.ai/) Он также объединяет основные возможности, включая регистрацию навыков, связанные учетные записи, основные беседы, чтобы предложить пользователям широкий спектр бесшовных взаимодействий и взаимодействия. Кроме того, возможности шаблона включают в себя богатые примеры многоиспользоваемых разговорных [навыков.](https://microsoft.github.io/botframework-solutions/overview/skills)  Отдельные навыки интегрированы в Виртуальный помощник, чтобы включить несколько сценариев. С помощью SDK Bot Framework навыки представлены в форме исходных кодов, что позволяет настраивать и расширять по мере необходимости. Дополнительные сведения о навыках Bot Framework см. в см. в поле ["Что такое навык Bot Framework".](https://microsoft.github.io/botframework-solutions/overview/skills/) В этом документе вы можете Виртуальный помощник реализации для организаций, как создать Teams Виртуальный помощник, связанный пример, пример кода и ограничения Виртуальный помощник.
На следующем изображении отображается обзор виртуального помощника:

![Виртуальный помощник схема обзора](../assets/images/bots/virtual-assistant/overview.png)

Действия текстовых сообщений отправляются в связанные навыки с помощью Виртуальный помощник с помощью модели [отправки.](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true)

## <a name="implementation-considerations"></a>Соображения реализации

Решение о добавлении Виртуальный помощник содержит множество детерминантов и отличается для каждой организации. Вспомогательные факторы реализации Виртуальный помощник организации:

* Центральная группа управляет всеми впечатлениями сотрудников. Он имеет возможность создавать новые Виртуальный помощник и управлять обновлениями для основного опыта, включая добавление новых навыков.
* В бизнес-функциях существует несколько приложений, и ожидается, что в будущем их число будет расти.
* Существующие приложения настраиваются, принадлежат организации и преобразуются в навыки для Виртуальный помощник.
* Центральная группа по опытом сотрудников может влиять на настройки существующих приложений. Она также предоставляет необходимые рекомендации по интеграции существующих приложений в качестве навыков в Виртуальный помощник опыте.

На следующем изображении отображаются бизнес-функции Виртуальный помощник:

![Центральная команда поддерживает помощника, а группы бизнес-функций способствуют навыкам](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Создание Teams, ориентированных на Виртуальный помощник

Корпорация Майкрософт опубликовала шаблон [Visual Studio для](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) создания виртуальных помощников и навыков. С помощью Visual Studio шаблона можно создать Виртуальный помощник, основанный на тексте, с поддержкой ограниченных богатых карт с действиями. Мы усовершенствовали базовый Visual Studio, чтобы включить Microsoft Teams платформы и Teams приложения. Некоторые возможности включают поддержку богатых адаптивных карт, модулей задач, групп или групповых чатов и расширений обмена сообщениями. Дополнительные сведения о продлении Виртуальный помощник до Microsoft Teams см. в [учебнике: Расширение Виртуальный помощник до Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).    
На следующем изображении отображается диаграмма высокого уровня решения Виртуальный помощник:

![Схема решения Виртуальный помощник высокого уровня](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Добавьте адаптивные карты в Виртуальный помощник

Чтобы правильно отправлять запросы, Виртуальный помощник должны определить правильную модель LUIS и соответствующие навыки, связанные с ней. Однако механизм отправки не может использоваться для действий с картами, так как модель LUIS, связанная с навыком, обучена текстам действий карт. Тексты действий карты являются фиксированными, заранее определенными ключевыми словами и не комментируются пользователем.

Этот недостаток решается путем встраив сведения о навыках в полезной нагрузке действия карты. Каждый навык должен `skillId` встраить  `value` в область действий карт. Необходимо убедиться, что каждое действие карты несет соответствующие сведения о навыках, и Виртуальный помощник использовать эту информацию для отправки.

Необходимо предоставить в конструкторе сведения о навыках, которые всегда присутствуют `skillId` в действиях карт.
Пример кода действия карты показан в следующем разделе:
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

Далее класс в Виртуальный помощник вводится для извлечения из полезной нагрузки `SkillCardActionData` `skillId` действия карты.
Фрагмент кода, извлеченный из полезной нагрузки действия карты, показан  `skillId` в следующем разделе:

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

Реализация используется методом расширения в [классе Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)
Фрагмент кода, извлеченный  `skillId` из данных действий карты, показан в следующем разделе:

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

### <a name="handle-interruptions"></a>Обработка перерывов

Виртуальный помощник может обрабатывать перерывы в случаях, когда пользователь пытается вызвать навык, а другой навык в настоящее время активен. `TeamsSkillDialog`, и `TeamsSwitchSkillDialog` представлены на основе [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) Bot Framework и [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs). Они позволяют пользователям переключать навыки работы с действиями карт. Для обработки этого запроса Виртуальный помощник пользователю с сообщением подтверждения для переключения навыков:

![Запрос подтверждения при переходе на новый навык](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>Обработка запросов модулей задач

Чтобы добавить возможности модуля задач в Виртуальный помощник, в обработник Виртуальный помощник действий включены два дополнительных метода: `OnTeamsTaskModuleFetchAsync` и `OnTeamsTaskModuleSubmitAsync` . Эти методы прослушивают действия, связанные с модулем задач, Виртуальный помощник, определяют навыки, связанные с запросом, и переназначяют запрос в указанный навык. 

Переадтранслировать запросы можно с помощью [метода SkillHttpClient.](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) `PostActivityAsync` Он возвращает ответ, `InvokeResponse` как который разобрано и преобразовано в `TaskModuleResponse` .


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

Аналогичный подход следует для отправки действий по картам и ответов модулей задач. Модуль задач для получения и отправки данных действий обновляется, чтобы включить `skillId` . Метод расширения действий извлекает из полезной нагрузки, которая содержит сведения о навыке, `GetSkillId` `skillId` который необходимо вызвать.

Фрагмент кода и методы `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` даются в следующем разделе:

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

Кроме того, необходимо включить все домены навыков в разделе Виртуальный помощник манифеста, чтобы модули задач, вызываемые с помощью отрисовки навыков `validDomains` должным образом.

### <a name="handle-collaborative-app-scopes"></a>Обработка областей совместных приложений

Teams приложения могут существовать в нескольких сферах, включая чат 1:1, групповой чат и каналы. Основной шаблон Виртуальный помощник предназначен для чатов 1:1. В рамках пользовательского интерфейса Виртуальный помощник пользователей для имени и поддерживает состояние пользователя. Так как он не подходит для групповых чатов или областей каналов, он удален.

Навыки должны обрабатывать действия в нескольких сферах, например в чате 1:1, групповом чате и разговоре по каналу. Если какие-либо из этих областей не поддерживаются, навыки должны отвечать соответствующим сообщением.

В Виртуальный помощник добавлены следующие функции обработки:

* Виртуальный помощник можно вызывать без текстовых сообщений из группового чата или канала.
* Артикуляция очищается перед отправкой сообщения в модуль отправки. Например, удалите необходимые @mention бота.

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

### <a name="handle-messaging-extensions"></a>Обработка расширений обмена сообщениями

Команды для расширения обмена сообщениями объявляются в файле манифеста приложения. Пользовательский интерфейс расширения обмена сообщениями на питание от этих команд. Чтобы Виртуальный помощник команду расширения обмена сообщениями в качестве присоединенного навыка, манифест Виртуальный помощник должен содержать эти команды. Вы должны добавить команды из манифеста индивидуального мастерства в манифест Виртуальный помощник в манифесте. Командный ID предоставляет сведения о связанном навыке, привнося ID приложения навыка через сепаратор. `:`

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

Соответствующий фрагмент кода Виртуальный помощник манифеста показан в следующем разделе:

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

После вызова команд пользователем Виртуальный помощник соответствующий навык путем разбора ИД команды, обновления действия путем удаления дополнительного суффикса из командного ИД и его переадэффинга в соответствующий `:<skill_id>` навык. Код для навыка не должен обрабатывать дополнительный суффикс. Таким образом, можно избежать конфликтов между командными ИД между навыками. С помощью этого подхода все команды поиска и действий навыка во всех контекстах, таких как **compose,**  **commandBox** и сообщения, Виртуальный помощник.

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

Некоторые действия по расширению обмена сообщениями не включают командный ID. Например, `composeExtension/selectItem` содержит только значение действия касания. Чтобы определить связанный навык, при формировании ответа для каждого элемента присоединяется к каждой карте `skillId` `OnTeamsMessagingExtensionQueryAsync` элемента. Это похоже на подход к [добавлению адаптивных карт](#add-adaptive-cards-to-your-virtual-assistant)в Виртуальный помощник.

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

В следующем примере показано, как преобразовать шаблон приложения Book-a-room в навык Виртуальный помощник: Book-a-room — это Microsoft Teams, который позволяет пользователям быстро находить и резервировать зал для собраний на 30, 60 или 90 минут начиная с текущего времени. Время по умолчанию — 30 минут. Область бота Book-a-room для личных или 1:1 бесед. На следующем изображении отображается Виртуальный помощник с **книгой навыков** комнаты:

![Виртуальный помощник с навыком "книга комнаты"](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Ниже представлены изменения дельты, введенные для преобразования его в навык, присоединенный к Виртуальный помощник. Аналогичные рекомендации следуют для преобразования любого существующего бота v4 в навык.

### <a name="skill-manifest"></a>Манифест мастерства

Манифест навыков — это файл JSON, который предоставляет конечную точку обмена сообщениями, ID, имя и другие соответствующие метаданные. Этот манифест отличается от манифеста, используемого для загрузки приложения в Microsoft Teams. Для Виртуальный помощник требуется путь к этому файлу в качестве ввода, чтобы прикрепить навык. В папку wwwroot бота добавлен следующий манифест.

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

Виртуальный помощник модель отправки построена на основе присоединенных моделей LUIS навыков. Модель отправки определяет намерения для каждой текстовой активности и находит навыки, связанные с ней.

Виртуальный помощник в формате в формате для ввода при присоединении навыка требуется модель `.lu` LUIS. LUIS json преобразуется в `.lu` формат с помощью средства botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Бот Book-a-room имеет две основные команды для пользователей:

- `Book room`
- `Manage Favorites`

Мы создали модель LUIS, понимая эти две команды. Соответствующие секреты должны быть заполнены `cognitivemodels.json` в . Соответствующий файл LUIS JSON находится [здесь](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json).
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

С помощью этого подхода любая команда, выдаемая пользователем для Виртуальный помощник или идентифицирована как команда, связанная с ботом, и передается `book room` `manage favorites` на этот `Book-a-room` навык.
С другой стороны, боту необходимо использовать модель LUIS, чтобы понять эти команды, если `Book-a-room room` они не введите полный текст. Пример: `I want to manage my favorite rooms`.

### <a name="multi-language-support"></a>Поддержка multi-Language

В качестве примера создается модель LUIS с только английской культурой. Можно создать модели LUIS, соответствующие другим языкам, и добавить запись в `cognitivemodels.json` .

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

Параллельно добавьте соответствующий `.lu` файл в путь LuisFolder. Структура папок должна быть следующим образом:

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Чтобы изменить `languages` параметр, обнови команду botskills следующим образом:

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

Виртуальный помощник используется `SetLocaleMiddleware` для определения текущего локального запроса и вызова соответствующей модели отправки. Действие базы ботов имеет поле locale, которое используется этим средним программным обеспечением. Вы можете использовать то же самое для вашего мастерства, а также. Бот book-a-room не использует это среднее повеять и вместо этого получает локализовку из сущности [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)клиентской базы Bot framework.

### <a name="claim-validation"></a>Проверка утверждений

Мы добавили [claimsValidator, чтобы](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) ограничить вызовы навыками. Чтобы разрешить Виртуальный помощник вызов этого навыка, заполняйте массив с помощью этого Виртуальный помощник `AllowedCallers` `appsettings` ID приложения.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

Массив разрешенных вызовов может ограничить доступ потребителей к навыкам. Добавьте одну запись `*` в этот массив, чтобы принимать вызовы от любого потребителя навыков.

```
"AllowedCallers": [ "*" ],
```

Дополнительные сведения о добавлении проверки утверждений в навык см. в добавлении проверки [утверждений к мастерству.](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)

### <a name="limitation-of-card-refresh"></a>Ограничение обновления карты 

Обновление активности, например обновления карт, пока не поддерживается Виртуальный помощник[(проблема github).](https://github.com/microsoft/botbuilder-dotnet/issues/3686) Таким образом, мы заменили все вызовы обновления карт `UpdateActivityAsync` на размещение новых вызовов `SendActivityAsync` карт.

### <a name="card-actions-and-task-module-flows"></a>Действия карты и потоки модулей задач

Чтобы перенаставлять действия карты или действия модуля задач в связанные навыки, навык должен встраить `skillId` в него.
`Book-a-room` Действие бот-карты, извлечение и отправка полезной нагрузки модуля задач изменены, чтобы содержать `skillId` в качестве параметра. 

Дополнительные сведения можно [получить в этом](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) разделе из этой документации.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Обработка действий из группового чата или области канала

`Book-a-room bot` предназначена только для частных чатов, например личных или 1:1. Так как мы Виртуальный помощник для поддержки групповых чатов и областей каналов, Виртуальный помощник должны вызываться из областей канала, поэтому бот должен получать действия для той же `Book-a-room` области. Поэтому `Book-a-room` бот настраивается для обработки этих действий. Вы можете найти способы `OnMessageActivityAsync` проверки методов `Book-a-room` обработки действий бота.

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

Вы также можете использовать существующие навыки из [репозитория Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) или создать новый навык с нуля. Для создания нового навыка см. [в учебниках по созданию нового навыка.](https://microsoft.github.io/botframework-solutions/overview/skills/) В Виртуальный помощник документации по архитектуре и навыкам см. Виртуальный помощник[и архитектуру навыков.](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)  

## <a name="limitations-of-virtual-assistant"></a>Ограничения Виртуальный помощник 

* **EndOfConversation.** Навык должен отправить действие по завершении `endOfConversation` беседы. На основе этого действия Виртуальный помощник контекст с этим навыком и возвращается Виртуальный помощник корневого контекста. Для бота Book-a-room нет четкого состояния, в котором беседа завершена. Поэтому мы не отослали от бота, и когда пользователь хочет вернуться к корневому контексту, он может просто сделать `endOfConversation` `Book-a-room` это по `start over` команде.  
* **Обновление карты.** Обновление карты еще не поддерживается Виртуальный помощник.  
* **Расширения обмена сообщениями:**
  * В настоящее время Виртуальный помощник может поддерживать не более десяти команд для расширений обмена сообщениями.
  * Конфигурация расширений обмена сообщениями не касается отдельных команд, а всего расширения. Это ограничивает конфигурацию для каждого отдельного навыка через Виртуальный помощник.
  * Командные ИД расширений обмена сообщениями имеют максимальную длину [64](../resources/schema/manifest-schema.md#composeextensions) символа, а для встраиванию сведений о навыках используются 37 символов. Таким образом, обновленные ограничения для командного ID ограничены 27 символами.

Вы также можете использовать существующие навыки из [репозитория Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) или создать новый навык с нуля. Учебники для более позднего можно найти [здесь](https://microsoft.github.io/botframework-solutions/overview/skills/). Обратитесь к [документации](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) по архитектуре Виртуальный помощник и навыкам.

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **C#**  **.NET** |
|----------|-----------------|---------------------------|
| Обновленный шаблон визуальной студии | Настраиваемый шаблон для поддержки возможностей групп. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| Код навыков бота book-a-room | Позволяет быстро найти и заказать комнату собраний на время. | [Просмотр](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |


## <a name="see-also"></a>Дополнительные ресурсы

* [Интеграция веб-приложений](~/samples/integrate-web-apps-overview.md)
* [Book-a-room](app-templates.md#app-template-code-samples)
* [Microsoft Teams бот](../bots/what-are-bots.md)
