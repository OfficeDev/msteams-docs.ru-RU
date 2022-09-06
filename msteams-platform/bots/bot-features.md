---
title: Боты и пакеты SDK
author: surbhigupta
description: Из этой статьи вы узнаете о средствах и пакетах SDK Bot Framework (C#, Python, Java, JavaScript) для ботов Microsoft Teams, а также о преимуществах и недостатках.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: b8d9f81216ea82aff3a5be9ec96c4f1dd79e9603
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2022
ms.locfileid: "67605021"
---
# <a name="bots-and-sdks"></a>Боты и пакеты SDK

Вы можете создать бота, работающего в Microsoft Teams, с помощью одного из следующих инструментов или возможностей:

* [Пакет SDK для Microsoft Bot Framework](#bots-with-the-microsoft-bot-framework)
* [Azure Active Directory](~/bots/how-to/authentication/auth-aad-sso-bots.md#develop-an-sso-teams-bot)
* [Портал разработчика](~/concepts/build-and-test/manage-your-apps-in-developer-portal.md#configure)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [Виртуальный помощник](~/samples/virtual-assistant.md)
* [Веб-перехватчики и соединительные линии](#bots-with-webhooks-and-connectors)

## <a name="bots-with-the-microsoft-bot-framework"></a>Боты с Microsoft Bot Framework

Ваш бот Teams состоит из следующих элементов:

* Размещенная вами общедоступная веб-служба.
* Регистрация Bot Framework для вашей веб-службы
* Пакет вашего приложения Teams, который подключает клиент Teams к вашей веб-службе.

> [!TIP]
> Используйте портал разработчика для регистрации веб-службы в Bot Framework и указания конфигурации приложения. Подробнее в разделе [Управление приложениями с помощью портала разработчиков для Teams](~/concepts/build-and-test/teams-developer-portal.md).

[Bot Framework](https://dev.botframework.com/)это многофункциональный пакет SDK, используемый для создания ботов с использованием C#, Java, Python и JavaScript. Если у вас уже есть бот на базе Bot Framework, вы можете легко изменить его для работы в Teams. Используйте C# или Node.js, чтобы воспользоваться преимуществами наших [пакетов SDK](/microsoftteams/platform/#pivot=sdk-tools). Эти пакеты расширяют базовые классы и методы пакета SDK Bot Builder:

* Использование специальных типов карточек, например карточек соединителя Office 365.
* Настройка данных каналов Teams для действий.
* Обработка запросов на расширение для работы с сообщениями.

> [!IMPORTANT]
> Вы можете разрабатывать приложения Teams с помощью любой технологии веб-программирования и напрямую вызывать [API-интерфейсы REST Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview). Но обработку маркеров необходимо выполнять во всех случаях.

## <a name="bots-with-power-virtual-agents"></a>Боты с Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) — это служба чат-ботов, созданная на платформе Microsoft Power и Bot Framework. В процессе разработки Power Virtual Agent используется управляемый графический интерфейс без кода, который позволяет членам вашей команды легко создавать интеллектуальный виртуальный агент и управлять им. После создания чат-бота на портале [Power Virtual Agents portal](https://powervirtualagents.microsoft.com) вы можете легко [интегрировать его с Teams.](how-to/add-power-virtual-agents-bot-to-teams.md). Подробнее о начале работы в разделе [Документация по Power Virtual Agents.](/power-virtual-agents).

>[!NOTE]
>Не следует использовать Microsoft Power Platform для создания приложений для публикации в магазине приложений Teams. Приложения Microsoft Power Platform можно публиковать только в магазине приложений организации.

## <a name="bots-with-webhooks-and-connectors"></a>Боты с веб-перехватчиками и соединитетелями

Веб-перехватчики и соединители подключают бот к веб-службам. Используя веб-перехватчики и соединители, вы можете создать бот для базового взаимодействия, например для создания рабочего процесса или других простых команд. Они доступны только в команде, в которой вы их создаете, и предназначены для простых процессов, которые относятся к рабочему процессу вашей компании. Подробнее в статье[Что такое веб-перехватчики и соединители.](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="advantages-of-bots"></a>Преимущества ботов

Боты в Microsoft Teams могут быть частью личной беседы, группового чата или канала в команде. Каждая область предлагает уникальные возможности и задачи для вашего чат-бота

| В канале | В групповом чате | В индивидуальном чате |
| :-- | :-- | :-- |
| Огромный охват | Меньше участников | Традиционный способ |
| Краткие индивидуальные взаимодействия | @упомянуть в разговоре с ботом  | Боты для вопросов и ответов |
| @упомянуть в разговоре с ботом | Похожий на канал | Боты, которые рассказывают анекдоты и делают заметки |

### <a name="in-a-channel"></a>В канале

Каналы содержат цепочки разговоров между несколькими людьми, даже до двух тысяч. Это потенциально дает вашему боту огромный охват, но отдельные взаимодействия должны быть краткими. Традиционные многоэтапные взаимодействия не работают. Вместо этого лучше использовать интерактивные карточки или модули задач, или переместиться в индивидуальную беседу, чтобы собрать больше сведений. Бот имеет доступ только к тем сообщениям, где он находится `@mentioned`. Вы можете получить дополнительные сообщения из беседы с помощью Microsoft Graph и разрешений на уровне организации.

Боты лучше работают в канале в следующих случаях:

* Уведомления, где вы предоставляете пользователям интерактивную карту для получения дополнительной информации.
* Сценарии обратной связи, такие как опросы и исследования.
* Взаимодействия, решения которых можно получить в одном цикле из запроса и ответа, и результаты которых будут полезны для нескольких участников беседы.
* Социальные или забавные боты, где вы получаете классное изображение кота, случайным образом выбираете победителя и так далее.

### <a name="in-a-group-chat"></a>В групповом чате

Групповые чаты — это не потоковые беседы между тремя или более пользователями. Как правило, у них меньше участников, чем у канала, и они более временные. Как и канал, бот имеет доступ только к тем сообщениям, где он находится `@mentioned` напрямую.

Во всех случаях, когда боты лучше работают в канале, они также лучше работают в групповом чате.

### <a name="in-a-one-to-one-chat"></a>В индивидуальном чате

Индивидуальный чат — это традиционный способ общения бота с пользователем. Вот несколько примеров диалоговых ботов для индивидуальной беседы:

* Боты для вопросов и ответов
* боты, которые инициируют рабочие процессы в других системах.
* боты, которые сообщают об этом.
* боты, которые принимают заметки.
Прежде чем создавать чат-боты "один к одному", подумайте, является ли интерфейс на основе беседы лучшим способом представления функций.

## <a name="disadvantages-of-bots"></a>Недостатки ботов

Подробный диалог между вашим ботом и пользователем — это медленный и сложный способ выполнения задачи. Бот, который поддерживает чрезмерные команды, особенно широкий спектр команд, не является успешным или просматривается пользователями положительно.

### <a name="have-multi-turn-experiences-in-chat"></a>Общение в чате с несколькими подходами

Для активного диалога разработчику требуется поддерживать состояние. Чтобы выйти из этого состояния, пользователю необходимо либо время ожидания, либо выбрать " **Отмена"**. К тому же процесс утомительный. Рассмотрим следующий сценарий разговора:

ПОЛЬЗОВАТЕЛЬ: назначь встречу с Меган.

БОТ: я нашел 200 результатов, пожалуйста, укажите имя и фамилию.

ПОЛЬЗОВАТЕЛЬ: назначь встречу с Меган Боуэн.

БОТ: хорошо, в какое время вы хотели бы встретиться с Меган Боуэн?

ПОЛЬЗОВАТЕЛЬ: 13:00.

БОТ: в какой день?

### <a name="support-too-many-commands"></a>Поддержка слишком большого количества команд

Поскольку в текущем меню бота есть только шесть видимых команд, вряд ли что-то еще будет использоваться с какой-либо частотой. Боты, которые углубляются в конкретную область, а не пытаются стать общим помощником, работают намного лучше.

### <a name="maintain-a-large-knowledge-base"></a>Поддержание широкой базы знаний

Один из недостатков ботов заключается в том, что трудно поддерживать большой объем база знаний с неранкированных ответов. Боты лучше всего подходят для коротких и быстрых взаимодействий, а не для просеивания длинных списков в поисках ответа.

## <a name="code-snippets"></a>Фрагменты кода

В следующем коде приведен пример действия бота для группы канала:

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

В следующем коде показан пример активности бота для индивидуального чата:

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
| Бот для беседы в Teams | Обработка сообщений и бесед. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
| Образцы бота | Набор образцов ботов | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) |[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Обработчики действий ботов](~/bots/bot-basics.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Боты для звонков и собраний](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [Беседы с ботами](~/bots/how-to/conversations/conversation-basics.md)
* [Меню команд бота](~/bots/how-to/create-a-bot-commands-menu.md)
* [Поток проверки подлинности для ботов в Microsoft Teams](~/bots/how-to/authentication/auth-flow-bot.md)
* [Использование модулей задач из ботов](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [Публикация бота в Azure](/azure/bot-service/bot-builder-deploy-az-cli)
* [Справочник по API для службы Bot Framework Connector](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference)
