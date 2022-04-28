---
title: Расширения сообщений
author: surbhigupta
description: Обзор расширений сообщений на платформе Microsoft Teams.
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: c81f8ec4b1158275ab796883b268d2c7fa6ecfe8
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104114"
---
# <a name="message-extensions"></a>Расширения сообщений

Расширения сообщений позволяют пользователям взаимодействовать с веб-службой с помощью кнопок и форм Microsoft Teams клиента. Они могут выполнять поиск или инициировать действия во внешней системе из области создания сообщения, из командного поля или непосредственно из сообщения. Результаты этого взаимодействия можно отправить клиенту Microsoft Teams в виде карточки с форматированием. В этом документе приводятся общие сведения о расширении сообщения, задачах, выполняемых в разных сценариях, работе расширения сообщения, командах действий и поиска, а также отмене ссылки.

На следующем рисунке отображаются расположения, из которых вызываются расширения сообщений:

![расположения вызова расширения сообщений](~/assets/images/messaging-extension-invoke-locations.png)

> [!NOTE]
> @mentioning сообщений больше не поддерживаются в поле создания сообщения.

## <a name="scenarios-where-message-extensions-are-used"></a>Сценарии, в которых используются расширения сообщений

| Сценарий | Пример |
|:-----------------|:-----------------|
|Вы хотите, чтобы внешняя система выполнит действие, а результат действия будет отправлен обратно в беседу.|Можно зарезервировать ресурс и сообщить о зарезервированном периоде времени в канал.|
|Вы хотите найти что-то во внешней системе и поделиться результатами с беседой.|Найдите рабочий элемент в Azure DevOps и предокажите его группе в качестве адаптивной карточки.|
|Вы хотите выполнить сложную задачу с несколькими шагами или большим объемом информации во внешней системе и поделиться результатами с беседой.|Создайте ошибку в системе отслеживания на основе сообщения Teams, назначьте эту ошибку Бобу и отправьте карточку в поток беседы с подробными сведениями об ошибке.|

## <a name="understand-how-message-extensions-work"></a>Общие сведения о работе расширений сообщений

Расширение сообщения состоит из размещенной веб-службы и манифеста приложения, который определяет, откуда веб-служба вызывается в клиенте Microsoft Teams клиента. Веб-служба использует схему обмена сообщениями Bot Framework и протокол безопасного обмена данными, поэтому необходимо зарегистрировать веб-службу в качестве бота в Bot Framework.

> [!NOTE]
> Хотя веб-службу можно создать вручную, используйте [пакет SDK Bot Framework](https://github.com/microsoft/botframework-sdk) для работы с протоколом.

В манифесте приложения для Microsoft Teams приложением одно расширение сообщения определяется до десяти различных команд. Каждая команда определяет тип, например действие или поиск, а также расположения в клиенте, из которого он вызывается. Расположения вызовов — это область создания сообщения, панель команд и сообщение. При вызове веб-служба получает сообщение HTTPS с полезными данными JSON, включая всю соответствующую информацию. Ответ с помощью полезных данных JSON, что позволяет Teams клиенту знать следующее взаимодействие для включения.

## <a name="types-of-message-extension-commands"></a>Типы команд расширения сообщений

Существует два типа команд расширения сообщения: команда действия и команда поиска. Тип команды расширения сообщения определяет элементы пользовательского интерфейса и потоки взаимодействия, доступные для веб-службы. Некоторые взаимодействия, такие как проверка подлинности и настройка, доступны для обоих типов команд.

### <a name="action-commands"></a>Команды действий

Команды действий используются для представления пользователям модального всплывающего окна для сбора или отображения информации. Когда пользователь отправляет форму, веб-служба отвечает, вставляя сообщение в беседу напрямую или вставляя сообщение в область создания сообщения. После этого пользователь может отправить сообщение. Для более сложных рабочих процессов можно объединить несколько форм в цепочку.

Команды действий запускаются из области создания сообщения, из командного поля или из сообщения. При вызове команды из сообщения исходные полезные данные JSON, отправленные боту, включают все сообщение, из которой он был вызван. На следующем рисунке показан модуль задачи "Действие расширения сообщения": ![модуль командной задачи действия расширения сообщения](~/assets/images/task-module.png)

### <a name="search-commands"></a>Команды поиска

Команды поиска позволяют пользователям искать информацию во внешней системе вручную с помощью поля поиска или путем вставки ссылки на отслеживаемого домена в область создания сообщения и вставки результатов поиска в сообщение. В основном потоке команд поиска начальное сообщение вызова включает строку поиска, отправленную пользователем. Вы отвечаете списком карточек и предварительных версий карточек. Клиент Teams отображает список предварительных версий карточек для пользователя. Когда пользователь выбирает карточку из списка, полная карточка вставляется в область создания сообщения.

Карточки запускаются из области создания сообщения или из командного поля и не запускаются из сообщения. Их нельзя активировать из сообщения.
На следующем рисунке показан модуль задачи "Команда поиска расширения сообщения":

![Команда поиска расширения сообщений](~/assets/images/search-extension.png)

> [!NOTE]
> Дополнительные сведения о карточках см. [в разделе "Что такое карточки"](../task-modules-and-cards/what-are-cards.md).

## <a name="link-unfurling"></a>Развертывание ссылки

Веб-служба вызывается при вставке URL-адреса в область сообщения создания. Эта функция называется размыканием ссылок. Вы можете подписаться на получение вызова при вставке URL-адресов, содержащих определенный домен, в область сообщения создания. Веб-служба может "распаковыть" URL-адрес в подробную карточку, предоставляя дополнительные сведения, чем стандартная карточка предварительного просмотра веб-сайта. Вы можете добавить кнопки, чтобы пользователи могли немедленно выполнять действия, не выходя из Microsoft Teams клиента.
На следующих изображениях при вставке ссылки в расширение сообщения отображается функция отмены ссылки:

![unfurl link](../assets/images/messaging-extension/unfurl-link.png)

![размыкание ссылок](../assets/images/messaging-extension/link-unfurl.gif)

## <a name="code-snippets"></a>Фрагменты кода

В следующем коде приведен пример действия, основанного на расширениях сообщений:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

 protected override Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
        {
            // Handle different actions using switch
            switch (action.CommandId)
            {
                case "HTML":
                    return new MessagingExtensionActionResponse
                    {
                        Task = new TaskModuleContinueResponse
                        {
                            Value = new TaskModuleTaskInfo
                            {
                                Height = 200,
                                Width = 400,
                                Title = "Task Module HTML Page",
                                Url = baseUrl + "/htmlpage.html",
                            },
                        },
                    };
                // return TaskModuleHTMLPage(turnContext, action);
                default:
                    string memberName = "";
                    var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
                    memberName = member.Name;
                    return new MessagingExtensionActionResponse
                    {
                        Task = new TaskModuleContinueResponse
                        {
                            Value = new TaskModuleTaskInfo
                            {
                                Card = <<AdaptiveAction card json>>,
                                Height = 200,
                                Width = 400,
                                Title = $"Welcome {memberName}",
                            },
                        },
                    };
            }
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

    async handleTeamsMessagingExtensionFetchTask(context, action) {
        switch (action.commandId) {
            case 'Static HTML':
                return staticHtmlPage();
        }
    }

    staticHtmlPage(){
        return {
            task: {
                type: 'continue',
                value: {
                    width: 450,
                    height: 125,
                    title: 'Task module Static HTML',
                    url: `${baseurl}/StaticPage.html`
                }
            }
        };
    }

```

---

В следующем коде приведен пример поиска на основе расширений сообщений:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
        {
            var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

            var packages = new[] {
            new { title = "A very extensive set of extension methods", value = "FluentAssertions" },
            new { title = "Fluent UI Library", value = "FluentUI" }};

            // We take every row of the results and wrap them in cards wrapped in MessagingExtensionAttachment objects.
            // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
            var attachments = packages.Select(package =>
            {
                var previewCard = new ThumbnailCard { Title = package.title, Tap = new CardAction { Type = "invoke", Value = package } };
                if (!string.IsNullOrEmpty(package.title))
                {
                    previewCard.Images = new List<CardImage>() { new CardImage(package.title, "Icon") };
                }

                var attachment = new MessagingExtensionAttachment
                {
                    ContentType = HeroCard.ContentType,
                    Content = new HeroCard { Title = package.title },
                    Preview = previewCard.ToAttachment()
                };

                return attachment;
            }).ToList();

            // The list of MessagingExtensionAttachments must we wrapped in a MessagingExtensionResult wrapped in a MessagingExtensionResponse.
            return new MessagingExtensionResponse
            {
                ComposeExtension = new MessagingExtensionResult
                {
                    Type = "result",
                    AttachmentLayout = "list",
                    Attachments = attachments
                }
            };
        }
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;     
        const attachments = [];
                const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);
                
                response.data.objects.forEach(obj => {
                        const heroCard = CardFactory.heroCard(obj.package.name);
                        const preview = CardFactory.heroCard(obj.package.name);
                        preview.content.tap = { type: 'invoke', value: { description: obj.package.description } };
                        const attachment = { ...heroCard, preview };
                        attachments.push(attachment);
                });
    
                return {
                    composeExtension:  {
                           type: 'result',
                           attachmentLayout: 'list',
                           attachments: attachments
                    }
                };
            }       
        }
```

---

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **.NET** | **Node.js** | **Python** |
|------------|-------------|----------------|------------|------------|
| Расширение сообщения с командами на основе действий | В этом примере показано, как создать расширение сообщения на основе действий. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Расширение сообщения с командами на основе поиска | В этом примере показано, как создать расширение сообщений на основе поиска. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
|Действие расширения сообщения для планирования задач|В этом примере показано, как запланировать задачу из команды действия расширения сообщения и получить карточку напоминания по расписанию.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Определение команды расширения сообщения о действии](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="see-also"></a>См. также

* [Определение команды расширения сообщения поиска](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Создание расширения сообщения](../build-your-first-app/build-messaging-extension.md)
