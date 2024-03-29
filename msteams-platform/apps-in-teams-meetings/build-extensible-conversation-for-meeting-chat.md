---
title: Создание расширяемой беседы для чата собрания
author: v-sdhakshina
description: Из этой статьи вы узнаете, как создать расширяемую беседу для чата собраний Microsoft Teams с помощью ботов, карточек и расширений сообщений.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: 65fc91d51cd4c740f28d5f33a2ad578f214c20a8
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615446"
---
# <a name="build-extensible-conversation-for-meeting-chat"></a>Создание расширяемой беседы для чата собрания

Вы можете сделать беседы расширяемыми в собраниях Microsoft Teams. Боты, расширения сообщений, карточки и модули задач можно комбинировать, чтобы обеспечить интуитивно понятный интерфейс.

## <a name="bots"></a>боты;

Бот также называется чат-ботом или ботом для общения. Это приложение, которое выполняет простые и повторяющиеся задачи пользователей, например в службах обслуживания или поддержки клиентов. В быту используются боты, которые сообщают сведения о погоде, бронируют рестораны или предоставляют сведения для путешествий. Взаимодействие с ботами может быть в виде быстрых вопросов и ответов или сложных бесед. Бот должен быть включен в области `team` `groupchat` для собрания канала и области для всех других типов собраний. Чтобы реализовать боты, начните [со сборки бота](/microsoftteams/platform//sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode).

### <a name="bot-apis"></a>Интерфейсы API бота

[Bot Framework](https://dev.botframework.com/)это многофункциональный пакет SDK, используемый для создания ботов с использованием C#, Java, Python и JavaScript. Если у вас уже есть бот на базе Bot Framework, вы можете легко изменить его для работы в Teams. Используйте C# или Node.js, чтобы воспользоваться преимуществами наших [пакетов SDK](/microsoftteams/platform/).

### <a name="code-samples---bots"></a>Примеры кода — боты

|Название примера | Описание | .NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|
| Бот для беседы в Teams | Обработка событий обмена сообщениями и бесед | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |
|Образцы бота | Набор образцов ботов  | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python) |

## <a name="message-extensions"></a>Расширения для обмена сообщениями

Расширения сообщений позволяют пользователям взаимодействовать с веб-службой с помощью кнопок и форм в клиенте Teams. Пользователи могут выполнять поиск или инициировать действия во внешней системе из области создания сообщения, из командного поля или непосредственно из сообщения. Результаты этого взаимодействия можно отправить клиенту Teams в формате карточки с форматированием. Реализация расширений сообщений для чатов собраний не отличается от обычных чатов. Чтобы реализовать расширение сообщения, начните с [расширений сообщений](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions?tabs=dotnet).

## <a name="cards-and-task-modules"></a>Карточки и модули задач

Карточки предоставляют пользователям возможность отправлять различные визуальные, звуковые и доступные для выбора сообщения и помогают в потоке общения. С помощью модулей задач можно создавать модальные всплывающие окна в Teams. Они особенно полезны для запуска и выполнения задач или отображения подробной информации, такой как видео или панелей мониторинга Power BI. Дополнительные сведения см [. в статье о сборке карточек и модулей задач](/microsoftteams/platform/task-modules-and-cards/cards-and-task-modules).

## <a name="feature-compatibility-by-user-types"></a>Совместимость компонентов по типам пользователей

В следующей таблице перечислены типы пользователей и перечислены функции, к которые каждый пользователь может получить доступ на собраниях:

| Тип пользователя | боты; | Расширения для обмена сообщениями | Адаптивные карточки | Модули задач |
| :-- | :-- | :-- | :-- | :-- |
| Пользователь в клиенте | Доступно | Доступно | Доступно | Доступно |
| Гость, часть клиентского Azure AD | Недоступно | Недоступно | Взаимодействие в чате собрания разрешено. | Взаимодействие в чате собрания из адаптивной карточки разрешено. |
| Федеративные пользователи. Дополнительные сведения см. в статье о [нестандартных пользователях](/microsoftteams/non-standard-users). | Взаимодействие разрешено. Приобретение, обновление и удаление не разрешены. | Недоступно | Взаимодействие в чате собрания разрешено. | Взаимодействие в чате собрания из адаптивной карточки разрешено. |
| Анонимный пользователь | Недоступно | Недоступно | Взаимодействие в чате собрания разрешено. | Недоступно |

## <a name="see-also"></a>См. также

* [Разработка расширения Microsoft Teams для обмена сообщениями](../messaging-extensions/design/messaging-extension-design.md)
* [Проектирование модулей задач для приложения Microsoft Teams](../task-modules-and-cards/task-modules/design-teams-task-modules.md)
