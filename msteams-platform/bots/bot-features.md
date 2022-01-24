---
title: Боты и пакеты SDK
author: surbhigupta
description: Обзор инструментов и SDKs для создания Microsoft Teams ботов.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: fda6092165fa55accbf5348b9850ac94396c05b5
ms.sourcegitcommit: 55d4b4b721a33bacfe503bc646b412f0e3b0203e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2022
ms.locfileid: "62185425"
---
# <a name="bots-and-sdks"></a>Боты и пакеты SDK

Вы можете создать бот, который работает в Microsoft Teams с одним из следующих средств или возможностей:

* [Microsoft Bot Framework SDK](#bots-with-the-microsoft-bot-framework)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [Виртуальный помощник](~/samples/virtual-assistant.md)
* [Веб-перехватчики и соединительные линии](#bots-with-webhooks-and-connectors)

## <a name="bots-with-the-microsoft-bot-framework"></a>Боты с Microsoft Bot Framework

Ваш Teams бот состоит из следующих:

* Общедоступный веб-сервис, на который вы наведылись.
* Регистрация Bot Framework для веб-службы.
* Пакет Teams, который подключает клиента Teams к веб-службе.

> [!TIP]
> Используйте портал разработчиков для регистрации веб-службы в Bot Framework и указания конфигураций приложений. Дополнительные сведения см. в [веб-сайте управление приложениями](~/concepts/build-and-test/teams-developer-portal.md)с помощью портала разработчиков для Teams.

Bot [Framework —](https://dev.botframework.com/) это богатый SDK, используемый для создания ботов с C#, Java, Python и JavaScript. Если у вас уже есть бот, основанный на bot Framework, вы можете легко изменить его для работы в Teams. Используйте C# или Node.js, чтобы воспользоваться нашими [SDKs](/microsoftteams/platform/#pivot=sdk-tools). Эти пакеты расширяют базовые классы и методы bot Builder SDK следующим образом:

* Используйте специализированные типы карт, такие как Office 365 соединители.
* Установите Teams для определенных каналов данных о действиях.
* Обработка запросов на расширение обмена сообщениями.

> [!IMPORTANT]
> Вы можете разрабатывать Teams в любой технологии веб-программирования и вызывать [API REST Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview) напрямую. Но обработку маркеров необходимо выполнять во всех случаях.

## <a name="bots-with-power-virtual-agents"></a>Боты с Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) — это служба чат-ботов, созданная на платформе Microsoft Power и Bot Framework. Процесс разработки виртуального агента Power использует управляемый, не кодовый и графический интерфейс, который позволяет членам группы легко создавать и поддерживать интеллектуальный виртуальный агент. После создания чат-бота на [портале Power Virtual Agents](https://powervirtualagents.microsoft.com)вы можете легко интегрировать его [с Teams](how-to/add-power-virtual-agents-bot-to-teams.md). Дополнительные сведения о работе см. в Power Virtual Agents [документации.](/power-virtual-agents)

## <a name="bots-with-webhooks-and-connectors"></a>Боты с веб-оками и соединитетелями

Веб-окки и соединители подключают бота к веб-службам. С помощью веб-ок и соединителов можно создать простой бот для базового взаимодействия, например создания рабочего процесса или других простых команд. Они доступны только в группе, в которой вы их создаете, и предназначены для простых процессов, специфических для рабочего процесса вашей компании. Дополнительные сведения см. [в webhooks и соединители.](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="advantages-of-bots"></a>Преимущества ботов

Боты в Microsoft Teams могут быть частью личной беседы, группового чата или канала в команде. Каждая область предоставляет уникальные возможности и проблемы для вашего разговорного бота.

| В канале | В групповом чате | В чате один к одному |
| :-- | :-- | :-- |
| Массовый охват | Меньше участников | Традиционный способ |
| Краткие индивидуальные взаимодействия | @mention бота  | Q&A bots |
| @mention бота | Аналогично каналу | Боты, которые рассказывают шутки и принимают заметки |

### <a name="in-a-channel"></a>В канале

Каналы содержат потоковые беседы между несколькими людьми даже до двух тысяч. Это потенциально дает вашему боту массовый охват, но отдельные взаимодействия должны быть краткими. Традиционные взаимодействия с несколькими поворотами не работают. Вместо этого необходимо использовать интерактивные карты или модули задач или перенести беседу в один разговор, чтобы собрать много информации. Ваш бот имеет доступ только к сообщениям, где он `@mentioned` находится. Дополнительные сообщения из беседы можно получить с помощью разрешений microsoft Graph и на уровне организации.

Боты лучше работают в канале в следующих случаях:

* Уведомления, в которых предоставляется интерактивная карта для получения дополнительных сведений.
* Сценарии обратной связи, такие как опросы и опросы.
* Один цикл запросов или ответов устраняет взаимодействия, и результаты полезны для нескольких участников беседы.
* Социальные или забавные боты, в которых вы получаете потрясающее изображение кошки, случайным образом выбирают победителя и так далее.

### <a name="in-a-group-chat"></a>В групповом чате

Групповые чаты — это не потоковые беседы между тремя или более пользователями. Как правило, у них меньше участников, чем у канала, и они более временные. Как и канал, у бота есть доступ только к сообщениям, где он `@mentioned` находится напрямую.

В тех случаях, когда боты лучше работают в канале, также лучше работают в групповом чате.

### <a name="in-a-one-to-one-chat"></a>В чате один к одному

Один к одному чат — это традиционный способ взаимодействия разговорного бота с пользователем. Несколько примеров одно-к-одному беседуя ботов являются:
* Q&A bots
* боты, которые инициируют рабочий процесс в других системах 
* боты, которые рассказывают шутки
* Боты, которые принимают заметки перед созданием чат-ботов один к одному, считают, является ли интерфейс, основанный на беседе, лучшим способом представить свои функции.

## <a name="disadvantages-of-bots"></a>Недостатки ботов

Обширный диалог между ботом и пользователем — это медленный и сложный способ для завершения задачи. Бот, который поддерживает чрезмерные команды, особенно широкий диапазон команд, не является успешным или рассматривается пользователями положительно.

### <a name="have-multi-turn-experiences-in-chat"></a>Многовековая переписка в чате

Обширный диалог требует от разработчика поддержания состояния. Чтобы выйти из этого состояния, пользователю необходимо либо отменить время, либо выбрать **отмену.** Кроме того, процесс является утомительным. Например, см. следующий сценарий беседы:

ПОЛЬЗОВАТЕЛЬ. Запланировать встречу с Меган.

BOT. Я нашел 200 результатов, включив имя и фамилию.

ПОЛЬЗОВАТЕЛЬ. Запланировать встречу с Меган Боуэн.

BOT: ОК, во сколько вы хотите встретиться с Меган Боуэн?

ПОЛЬЗОВАТЕЛЬ: 13:00.

BOT: В какой день?

### <a name="support-too-many-commands"></a>Поддержка слишком 10 команд

Так как в текущем меню бота только шесть видимых команд, вряд ли с какой-либо частотой будет использоваться что-либо большее. Боты, которые идут вглубь определенной области, а не пытаются быть более широким помощником работы и тарифа лучше.

### <a name="maintain-a-large-knowledge-base"></a>Поддержание большой базы знаний

Один из недостатков ботов заключается в том, что трудно поддерживать большую базу знаний по исканию с неоценяемой реакцией. Боты лучше всего подходят для коротких и быстрых взаимодействий, а не для сеяния длинных списков в поисках ответа.

## <a name="code-snippets"></a>Фрагменты кода

В следующем коде приводится пример активности бота для области группы каналов:

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

В следующем коде приводится пример активности бота для чата один к одному:

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

|Название примера | Описание | .NETCore | Node.js |
|----------------|-----------------|--------------|----------------|
| Бот для беседы в Teams | Обработка событий обмена сообщениями и бесед. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Обработчики действий ботов](~/bots/bot-basics.md)

## <a name="see-also"></a>См. также

* [Боты вызовов и собраний](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [Беседы с ботами](~/bots/how-to/conversations/conversation-basics.md)
* [Меню команд бота](~/bots/how-to/create-a-bot-commands-menu.md)
* [Поток проверки подлинности для ботов в Microsoft Teams](~/bots/how-to/authentication/auth-flow-bot.md)
* [Использование модулей задач из ботов](~/task-modules-and-cards/task-modules/task-modules-bots.md)
