---
title: Боты в Microsoft Teams
author: surbhigupta
description: Обзор ботов в Microsoft Teams.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a9f53654ba3240b973b77c05cd64a22c80237350
ms.sourcegitcommit: a6c39106ccc002d02a65e11627659e0c48981d8a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/13/2022
ms.locfileid: "62014565"
---
# <a name="bots-in-microsoft-teams"></a>Боты в Microsoft Teams

Бот также называется чат-ботом или чат-ботом. Это приложение, которое выполняет простые и повторяющихся задач пользователей, таких как обслуживание клиентов или сотрудников службы поддержки. Каждодневное использование ботов включает в себя боты, которые предоставляют сведения о погоде, делают бронирование обедов или предоставляют сведения о путешествиях. Взаимодействие с ботами может быстро отвечать на вопросы или может быть сложным разговором.

> [!IMPORTANT]
> В настоящее время боты доступны в облако сообщества для государственных организаций (GCC) и недоступны в GCC-High и Министерстве обороны (DOD).

Диалоговые боты позволяют пользователям взаимодействовать с веб-службой с помощью текстовых, интерактивных карт и модулей задач.

![Вызов бота с помощью текста](~/assets/images/invokebotwithtext.png)

![Вызов бота с помощью карты](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

Разговорные боты невероятно гибки. Боты могут обрабатывать несколько базовых команд или сложных задач, которые связаны с искусственным интеллектом и обработкой естественного языка. Боты могут быть частью большего приложения или автономными.

Чтобы создать полезный бот, используйте правильное сочетание модулей карт, текста и задач. На следующем изображении показан пользователь, беседующий с ботом в чате один к одному с помощью текстовых и интерактивных карт.

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="Пример бота faQ" border="true":::

Каждое взаимодействие между пользователем и ботом представлено как действие. Когда бот получает действие, он передает его обработчику действий. См. [обработчики действий ботов.](~/bots/bot-basics.md)

Боты — это приложения с диалоговом интерфейсом. Вы можете взаимодействовать с ботом с помощью текстовых, интерактивных карт и речи. Бот ведет себя по-разному в разговоре в чате канала или группы и в беседе один к одному. Беседы обрабатываются через соединители Bot Framework. См. [основы беседы.](~/bots/how-to/conversations/conversation-basics.md)

Для доступа к соответствующему контенту и улучшения работы с ботом требуется контекстная информация, например сведения о профиле пользователя. См. [Teams контексте](~/bots/how-to/get-teams-context.md).

Вы можете отправлять и получать файлы через бот с Graph API или Teams API бота. См. [отправку и получение файлов с помощью бота.](~/bots/how-to/bots-filesv4.md)

Ограничение скорости используется для оптимизации ботов, используемых для Teams приложения. Для защиты Microsoft Teams пользователей API-бота предоставляют ограничение скорости для входящих запросов. См. оптимизацию бота с ограничением [скорости в Teams.](~/bots/how-to/rate-limit.md)

С помощью Graph API майкрософт для звонков и собраний в Интернете Microsoft Teams приложения теперь могут взаимодействовать с пользователями с помощью голосовых и видеосвязи. См. [боты вызовов и собраний.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

Вы можете использовать API Teams бота для получения сведений для членов чата или группы. См. [изменения Teams API бота для получения участников группы или чата.](~/resources/team-chat-member-api-changes.md)

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Боты и пакеты SDK](~/bots/bot-features.md)

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | C # | Node.js |
|----------------|-----------------|--------------|--------------|
| Напоминание о ежедневных задачах bot| Показано, как запланировать повторяемую задачу и получить напоминание в запланированное время. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Создать бота для Teams](~/bots/how-to/create-a-bot-for-teams.md)
* [Регистрация вызовов и собраний бота для Microsoft Teams](~/bots/calls-and-meetings/registering-calling-bot.md)
* [Добавление проверки подлинности в Teams бота](~/bots/how-to/authentication/add-authentication.md)
* [Обработчики действий ботов](~/bots/bot-basics.md)
* [События бесед в вашем боте Teams](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
