---
title: Боты в Microsoft Teams
author: surbhigupta
description: Обзор ботов в Microsoft Teams.
ms.topic: overview
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 7d6996f023b6e9f706edd99429dd1575394a43f1
ms.sourcegitcommit: 6189ca81099452a3ab2ff4fff4fb1ded5ba6dcfe
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2022
ms.locfileid: "64498226"
---
# <a name="bots-in-microsoft-teams"></a>Боты в Microsoft Teams

Бот также называется чат-ботом или ботом для общения. Это приложение, которое выполняет простые и повторяющиеся задачи пользователей, например, в службах обслуживания или поддержки клиентов. В быту используются боты, которые сообщают сведения о погоде, бронируют рестораны или предоставляют сведения для путешествий. Взаимодействие с ботами может быть в виде быстрых вопросов и ответов или сложных бесед.

> [!IMPORTANT]
> В настоящее время боты доступны в средах облака сообщества для государственных организаций (GCC), но недоступны для GCC-High и Министерства обороны (DOD).

Боты для общения позволяют пользователям взаимодействовать с веб-службой с помощью текста, интерактивных карточек и модулей задач.

![Вызов бота с помощью текста](~/assets/images/invokebotwithtext.png)

![Вызов бота с помощью карточки](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

Боты для общения чрезвычайно гибкие. Боты могут обрабатывать несколько основных команд или сложных задач, которые включают искусственный интеллект и обработку естественного языка. Боты могут быть частью большего приложения или быть автономными.

Используйте правильное сочетание карточек, текста и модулей задач для создания полезного бота. На следующем изображении показано, как пользователь общается с ботом в личном чате с помощью текста и интерактивных карточек.

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="Пример вопросов и ответов бота" border="true":::

Каждое взаимодействие между пользователем и ботом представлено как действие. Когда бот получает действие, он передает его обработчикам действий. См. статью об [обработчиках действий ботов](~/bots/bot-basics.md).

Боты — это приложения с интерфейсом бесед. Вы можете взаимодействовать с ботом с помощью текста, интерактивных карточек и речи. Бот ведет себя по-разному в канале или групповом чате, а также в личной беседе. Беседы обрабатываются через соединители Bot Framework. См. статью [об основах бесед с ботами](~/bots/how-to/conversations/conversation-basics.md).

Для доступа к соответствующему содержимому и улучшения работы бота требуется контекстная информация, например сведения о профиле пользователя. См. статью о [получении контекста в Teams](~/bots/how-to/get-teams-context.md).

Вы можете отправлять и получать файлы с помощью бота через API Graph или API бота Teams. См. статью об [отправке и получении файлов с помощью ботов](~/bots/how-to/bots-filesv4.md).

Для оптимизации ботов, используемых для приложения Teams, применяется ограничение скорости трафика. Чтобы защитить Microsoft Teams и его пользователей, API бота предоставляют ограничение скорости для входящих запросов. См. статью [Оптимизация бота с ограничением скорости в Teams](~/bots/how-to/rate-limit.md).

С помощью API Microsoft Graph для звонков и онлайн-собраний приложения Microsoft Teams теперь могут взаимодействовать с пользователями с помощью голосовых вызовов и видеосвязи. См. статью о [ботах для звонков и собраний](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).

Вы можете использовать API бота Teams для получения сведений для участников чата или команды. См. статью об [изменениях API ботов Teams для получения сведений участников команды или чата](~/resources/team-chat-member-api-changes.md).

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Боты и пакеты SDK](~/bots/bot-features.md)

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Напоминание о ежедневной задаче бота| Демонстрация создания графика повторяющейся задачи и получения напоминания в запланированное время. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Создать бота для Teams](~/bots/how-to/create-a-bot-for-teams.md)
* [Как работают боты Microsoft Teams](/azure/bot-service/bot-builder-basics-teams)
* [Регистрация бота для звонков и собраний для Microsoft Teams](~/bots/calls-and-meetings/registering-calling-bot.md)
* [Добавление проверки подлинности для бота Teams](~/bots/how-to/authentication/add-authentication.md)
* [Обработчики действий ботов](~/bots/bot-basics.md)
* [События бесед в вашем боте Teams](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
