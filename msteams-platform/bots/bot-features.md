---
title: Боты и пакеты SDK
author: surbhigupta
description: Общие сведения о средствах и пакетах SDK для создания Microsoft Teams ботов.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a50f93e718dcff35d810f0f8748c97095b49b138
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073748"
---
# <a name="bots-and-sdks"></a>Боты и пакеты SDK

Вы можете создать бот, который работает в Microsoft Teams одним из следующих средств или возможностей:

* [Microsoft Bot Framework SDK](#bots-with-the-microsoft-bot-framework)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [Виртуальный помощник](~/samples/virtual-assistant.md)
* [Веб-перехватчики и соединительные линии](#bots-with-webhooks-and-connectors)

## <a name="bots-with-the-microsoft-bot-framework"></a>Боты с Microsoft Bot Framework

Ваш Teams бот состоит из следующих компонентов:

* Общедоступная веб-служба, размещенная вами.
* Регистрация Bot Framework для веб-службы.
* Ваш Teams приложения, который подключает клиент Teams к веб-службе.

> [!TIP]
> Используйте портал разработчика, чтобы зарегистрировать веб-службу в Bot Framework и указать конфигурации приложений. Дополнительные сведения см. [в статье об управлении приложениями с помощью портала разработчика Teams](~/concepts/build-and-test/teams-developer-portal.md).

[Bot Framework —](https://dev.botframework.com/) это полнофункциональный пакет SDK, используемый для создания ботов с помощью C#, Java, Python и JavaScript. Если у вас уже есть бот, основанный на Bot Framework, вы можете легко изменить его для работы в Teams. Используйте C# или Node.js, чтобы воспользоваться преимуществами [наших пакетов SDK](/microsoftteams/platform/#pivot=sdk-tools). Эти пакеты расширяют базовые классы и методы пакета SDK Bot Builder следующим образом:

* Используйте специализированные типы карточек, например Office 365 соединителя.
* Задайте Teams для определенных каналов действий.
* Обработка запросов на расширение обмена сообщениями.

> [!IMPORTANT]
> Вы можете разрабатывать Teams в любой технологии веб-программирования и напрямую вызывать [REST API Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview). Но обработку маркеров необходимо выполнять во всех случаях.

## <a name="bots-with-power-virtual-agents"></a>Боты с Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) — это служба чат-ботов, созданная на платформе Microsoft Power и Bot Framework. Процесс разработки Power Virtual Agent использует интерактивный, без кода и графический интерфейс, который позволяет участникам команды легко создавать и поддерживать интеллектуальный виртуальный агент. После создания чат-бота [на Power Virtual Agents](https://powervirtualagents.microsoft.com) портале его можно легко интегрировать с [Teams](how-to/add-power-virtual-agents-bot-to-teams.md). Дополнительные сведения о начале работы см. в Power Virtual Agents [документации](/power-virtual-agents).

>[!NOTE]
>Не следует использовать Microsoft Power Platform для создания приложений, которые должны быть опубликованы в Teams app Store. Приложения Microsoft Power Platform можно публиковать только в магазине приложений организации.

## <a name="bots-with-webhooks-and-connectors"></a>Боты с веб-перехватчиками и соединителями

Веб-перехватчики и соединители подключают бот к веб-службам. С помощью веб-перехватчиков и соединителей можно создать бот для базового взаимодействия, например для создания рабочего процесса или других простых команд. Они доступны только в команде, в которой вы их создаете, и предназначены для простых процессов, которые относятся к рабочему процессу вашей компании. Дополнительные сведения см. [в статье о веб-перехватчиках и соединителях](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="advantages-of-bots"></a>Преимущества ботов

Боты в Microsoft Teams могут быть частью личной беседы, группового чата или канала в команде. Каждая область предоставляет уникальные возможности и трудности для вашего бота для общения.

| В канале | В групповом чате | В чате "один к одному" |
| :-- | :-- | :-- |
| Массовый охват | Меньше элементов | Традиционный способ |
| Краткое взаимодействие с отдельными пользователями | @mention боту  | Q&A bots |
| @mention боту | Аналогично каналу | Боты, которые сообщают о примечаниях и заметок |

### <a name="in-a-channel"></a>В канале

Каналы содержат цепочки бесед между несколькими людьми даже до двух тысяч. Это потенциально обеспечивает большой охват бота, но отдельные взаимодействия должны быть краткими. Традиционные многоэтапные взаимодействия не работают. Вместо этого необходимо использовать интерактивные карточки или модули задач или переместить беседу в беседу "один к одному" для сбора большого количества информации. Бот имеет доступ только к тем сообщениям, где он находится `@mentioned`. Дополнительные сообщения из беседы можно получить с помощью Graph майкрософт и разрешений на уровне организации.

Боты лучше работают в канале в следующих случаях:

* Уведомления, в которых вы предоставляете интерактивную карточку, чтобы пользователи могли получать дополнительные сведения.
* Сценарии обратной связи, такие как опросы и опросы.
* Один цикл запроса или ответа разрешает взаимодействия, и результаты полезны для нескольких участников беседы.
* Социальные или интересные боты, в которых вы получаете отличное изображение кота, случайным образом выберите нужного игрока и т. д.

### <a name="in-a-group-chat"></a>В групповом чате

Групповые чаты — это не потоковые беседы между тремя или более пользователями. Как правило, у них меньше участников, чем у канала, и они более временные. Как и канал, бот имеет доступ только к тем сообщениям, где он находится `@mentioned` напрямую.

В случаях, когда боты лучше работают в канале, также лучше работают в групповом чате.

### <a name="in-a-one-to-one-chat"></a>В чате "один к одному"

Чат "один к одному" — это традиционный способ взаимодействия бота с пользователем. Ниже приведено несколько примеров чат-ботов типа "один к одному".

* Q&A bots
* боты, которые инициируют рабочие процессы в других системах
* боты, которые сообщают об этом
* Боты, которые принимают заметки перед созданием чат-ботов "один к одному", подумайте, является ли интерфейс на основе диалога лучшим способом представления функций.

## <a name="disadvantages-of-bots"></a>Недостатки ботов

Обширный диалог между ботом и пользователем — это медленный и сложный способ выполнения задачи. Бот, который поддерживает чрезмерные команды, особенно широкий спектр команд, не является успешным или просматривается пользователями положительно.

### <a name="have-multi-turn-experiences-in-chat"></a>Многоэтапное взаимодействие в чате

Для расширенного диалога разработчик должен поддерживать состояние. Чтобы выйти из этого состояния, пользователю необходимо либо время ожидания, либо выбрать " **Отмена"**. Кроме того, этот процесс утомителен. Например, см. следующий сценарий беседы:

ПОЛЬЗОВАТЕЛЬ. Запланировать собрание с Марта.

БОТ: я обнаружил 200 результатов, укажите имя и фамилию.

ПОЛЬЗОВАТЕЛЬ. Запланировать собрание с Марта Боуэн (Megan Bowen).

БОТ: ОК, когда вы хотите провести собрание с Марта Боуэн?

ПОЛЬЗОВАТЕЛЬ: 13:00.

BOT: в какой день?

### <a name="support-too-many-commands"></a>Поддержка слишком большого количества команд

Так как в текущем меню бота есть только шесть видимых команд, любые другие команды вряд ли будут использоваться с какой-либо частотой. Боты, которые углубиться в определенную область, вместо того чтобы пытаться быть более широким помощником по работе и тарифам.

### <a name="maintain-a-large-knowledge-base"></a>Обслуживание больших база знаний

Один из недостатков ботов заключается в том, что трудно поддерживать большой объем база знаний с неранкированные ответы. Боты лучше всего подходят для коротких быстрых взаимодействий, а не для поиска ответа в длинных списках.

## <a name="code-snippets"></a>Фрагменты кода

В следующем коде приведен пример действия бота для области команды канала:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}

```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});

```

---

В следующем коде приведен пример действия бота для чата "один к одному":

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle message activity
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    turnContext.Activity.RemoveRecipientMention();
    var text = turnContext.Activity.Text.Trim().ToLower();
  await turnContext.SendActivityAsync(MessageFactory.Text($"Your message is {text}."), cancellationToken);
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
this.onMessage(async (context, next) => {
    await context.sendActivity(MessageFactory.text("Your message is:" + context.activity.text));
    await next();
});
```

---

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NETCore | Node.js | Python|
|----------------|-----------------|--------------|----------------|-------|
| Бот для беседы в Teams | Обработка событий обмена сообщениями и бесед. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
| Образцы бота | Набор примеров ботов | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Обработчики действий ботов](~/bots/bot-basics.md)

## <a name="see-also"></a>См. также

* [Боты для звонков и собраний](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [Беседы с ботами](~/bots/how-to/conversations/conversation-basics.md)
* [Меню команд бота](~/bots/how-to/create-a-bot-commands-menu.md)
* [Поток проверки подлинности для ботов в Microsoft Teams](~/bots/how-to/authentication/auth-flow-bot.md)
* [Использование модулей задач из ботов](~/task-modules-and-cards/task-modules/task-modules-bots.md)
