---
title: Расширения для сообщений
author: surbhigupta
description: Узнайте, как используются расширения сообщений, их типы и сценарии, в которых они используются на платформе Microsoft Teams. Примеры по действию и расширению сообщений на основе поиска.
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6b486e732542cbd6fdfeaecbef74b9724a024e67
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819977"
---
# <a name="message-extensions"></a>Расширения для сообщений

Расширения для сообщений позволяют пользователям взаимодействовать с веб-службой с помощью кнопок и форм в клиенте Microsoft Teams. Они могут искать или запускать действия во внешней системе из области создания сообщения, командного поля или непосредственно из сообщения. Результаты этого взаимодействия можно отправить клиенту Teams в виде карточки с расширенным форматом.

> [!IMPORTANT]
> Расширения сообщений доступны в облаке сообщества государственных организаций (GCC) и GCC-High средах, но не в среде Министерства обороны (DoD).

В этом документе представлен обзор расширения для сообщений с задачами в разных сценариях, работой расширения для сообщений, командами действий и поиском, а также разгрузки ссылок.

На следующем изображении показаны расположения, из которых вызываются расширения для сообщений:

:::image type="content" source="~/assets/images/messaging-extension-invoke-locations.png" alt-text="расположения вызова расширения для сообщений":::

> [!NOTE]
> @Упоминание расширения для сообщений в поле создания больше не поддерживаются.

## <a name="scenarios-where-message-extensions-are-used"></a>Сценарии, в которых используются расширения для сообщений

| Сценарий | Пример |
|:-----------------|:-----------------|
|Вы хотите, чтобы внешняя система выполняла действие и отправляла результат действия в качестве ответа в беседу.|Можно зарезервировать ресурс и сообщить о зарезервированном периоде времени в канал.|
|Вы хотите найти что-то во внешней системе и отправить результаты в беседу.|Можно найти рабочий элемент в Azure DevOps и поделиться им с группой, представив его в виде адаптивной карточки.|
|Вы хотите выполнить сложную задачу с несколькими этапами или большим объемом информации во внешней системе и отправить результаты в беседу.|Создайте запись об ошибке в системе отслеживания на основе сообщения Teams, назначьте эту ошибку Бобу и отправьте карточку со сведениями об ошибке в цепочку беседы.|

## <a name="understand-how-message-extensions-work"></a>Сведения о работе расширений для сообщений

Расширение сообщений состоит из веб-службы, которую вы размещаете, и манифеста приложения, который определяет, откуда вызывается веб-служба в клиенте Teams. Веб-служба пользуется схемой обмена сообщениями Bot Framework и протоколом безопасной связи, поэтому вам требуется зарегистрировать веб-службу в качестве бота в Bot Framework.

> [!NOTE]
> Веб-службу можно создать вручную, однако для работы с протоколом используйте [пакет средств разработки Bot Framework](https://github.com/microsoft/botframework-sdk).

В манифесте приложения Для Teams определяется одно расширение сообщений с 10 разными командами. Каждая команда определяет тип, например действие или поиск, а также расположения в клиенте, из которого она вызывается. Расположения для вызовов — область созданий сообщений, панель команд и сообщение. При вызове веб-служба получает HTTPS-сообщение с полезные данные JSON, включая всю соответствующую информацию. Отвечайте с помощью полезных данных JSON, что позволит клиенту Teams узнать о следующем взаимодействии, которое необходимо включить.

## <a name="types-of-message-extension-commands"></a>Типы команд расширений для сообщений

Есть два типа команд расширения для сообщений: команда действия и команда поиска. Тип команды расширения для сообщений определяет элементы пользовательского интерфейса и потоки взаимодействия, доступные веб-службе. Некоторые взаимодействия, например, проверка подлинности и настройка, доступны для обоих типов команд.

### <a name="action-commands"></a>Команды действий

Команды действий используются для представления пользователям модального всплывающего окна для сбора или отображения информации. Когда пользователь отправляет форму, веб-служба отвечает, вставив сообщение непосредственно в беседу или в область создания сообщения. После этого пользователь может отправить сообщение. Вы можете объединить несколько форм для создания более сложных рабочих процессов.

Команды действий следует запускать в области создания сообщения, в командном поле или из сообщения. При вызове команды из сообщения исходные полезные данные JSON, отправляемые боту, будут включать все сообщение, из которых оно было вызвано. На следующем изображении показан модуль задачи команды действия расширения сообщения:

:::image type="content" source="~/assets/images/task-module.png" alt-text="Модуль задачи команды действия расширения сообщения":::

### <a name="search-commands"></a>Команды поиска

Команды поиска позволяют пользователям искать сведения во внешней системе либо вручную с помощью поля поиска, либо путем вставки ссылки на отслеживаемый домен в область создания сообщения и вставки результатов поиска в сообщение. В простейшем сценарии поток операций поиска выглядит следующим образом: исходное сообщение вызова включает строку поиска, которую отправил пользователь. Вы в ответ отправляете список карточек и предварительных просмотров карточек. Клиент Teams отображает список предварительных версий карт для пользователя. Когда пользователь выбирает карточку из списка, полноразмерная карточка вставляется в область редактирования сообщения.

Карточки запускаются из области создания сообщения или командного поля и не запускаются из сообщения. Они не могут быть активированы из сообщения.
На следующем изображении показан модуль задачи команды поиска расширения для сообщения:

:::image type="content" source="~/assets/images/search-extension.png" alt-text="Команда поиска расширения сообщения":::

> [!NOTE]
> Дополнительные сведения о карточках см. в статье о том, [что такое карточки](../task-modules-and-cards/what-are-cards.md).

## <a name="link-unfurling"></a>Развертывание ссылки

Веб-служба вызывается при вставке URL-адреса в область создания сообщения. Эта функция называется развертыванием ссылок. Вы можете подписаться на получение вызова, когда URL-адреса, содержащие определенный домен, вставляются в область создания сообщений. Веб-служба может "развернуть" URL-адрес в подробную карточку, предоставляющую больше информации, чем стандартная карточка предварительного просмотра веб-сайта. Вы можете добавить кнопки, чтобы пользователи могли немедленно выполнять действия, не выходя из клиента Teams.
На следующих изображениях показана функция развертывания ссылок при вставке ссылки в расширение для сообщений:

:::image type="content" source="../assets/images/messaging-extension/unfurl-link.png" alt-text="развернуть ссылку":::

![Развертывание ссылки](../assets/images/messaging-extension/link-unfurl.gif)

## <a name="code-snippets"></a>Фрагменты кода

В следующем коде приводится пример действия, основанного на расширениях для сообщений:

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

В следующем коде приводится пример поиска расширений для сообщений:

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
| Расширение для сообщений с командами на основе действий | В этом примере показано, как создать расширение для сообщений на основе действий. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Расширение для сообщений с командами на основе поиска | В этом примере показано, как создать расширение для сообщений на основе поиска. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
|Действие расширения для сообщения для планирования задач|В этом примере показано, как запланировать задачу из команды действия расширения для сообщений и получить карточку с напоминанием в запланированную дату и время.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)| Н/Д |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Определение команды действия расширения для сообщений](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Сопоставление возможностей приложения и функций Teams](../concepts/design/map-use-cases.md#app-capabilities-mapped-to-features)
* [Создание первого приложения расширения для сообщений с помощью JavaScript](../sbs-gs-msgext.yml)
* [Разработка расширения Microsoft Teams для обмена сообщениями](design/messaging-extension-design.md)
* [Определение команд действий расширения для сообщений](how-to/action-commands/define-action-command.md)
* [Определение команд поиска расширений сообщений](how-to/search-commands/define-search-command.md)
* [Добавление разворачивающейся ссылки](how-to/link-unfurling.md)
* [Схема манифеста для Teams](../resources/schema/manifest-schema.md)
* [Портал разработчика Teams](../concepts/build-and-test/teams-developer-portal.md)
