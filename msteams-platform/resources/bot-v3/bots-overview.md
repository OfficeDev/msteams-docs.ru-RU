---
title: Добавление ботов в Microsoft Teams приложения
description: Описывает, как начать разработку ботов в Microsoft Teams
ms.topic: conceptual
keywords: разработка команд ботов
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: 674576efccb2916b8a82ae27310d8fe49909a782
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566756"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Добавление ботов в Microsoft Teams приложения

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Создавайте и подключайте интеллектуальных ботов для взаимодействия с Microsoft Teams пользователями естественным путем через чат. Или предоставьте простой бот на основе команд, который будет использоваться в качестве интерфейса «командной линии» для более широкого Teams приложения. Вы можете сделать бота только для уведомлений, который может толкать информацию, относящуюся к вашим пользователям непосредственно к ним в канале или прямом сообщении. Вы даже можете принести существующий бот на основе Bot Framework и добавить Teams поддержку, чтобы сделать ваш опыт блеск.

![Пример бота, помогая пользователю](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Что нужно знать: Боты

Бот появляется так же, как и любой другой член команды вы взаимодействуете с в разговоре, за исключением того, что он имеет шестиугольный значок аватара и всегда в Сети.

Бот ведет себя по-разному в зависимости от того, в каком разговоре он участвует. Боты в Teams поддерживают несколько видов разговоров, называемых сферами в [манифесте приложения.](~/resources/schema/manifest-schema.md)

* `teams` Также называются разговоры канала.
* `personal` Разговоры между ботом и одним пользователем.
* `groupChat` Разговор между ботом и 2 или более пользователями.

Для получения дополнительной [информации, см Microsoft Teams.](~/resources/bot-v3/bot-conversations/bots-conversations.md)

С Microsoft Teams приложениями, вы можете сделать бот звездой вашего опыта, или просто помощником. Боты распространяются как часть вашего более широкого пакета приложений, который может включать в себя другие возможности, такие [как вкладки](~/tabs/what-are-tabs.md) или [расширения обмена сообщениями.](~/messaging-extensions/what-are-messaging-extensions.md)

## <a name="bot-apis"></a>Бот API

Microsoft Teams поддерживает большую часть [Microsoft Bot Framework.](https://dev.botframework.com/) (Если у вас уже есть бот, основанный на Bot Framework, вы можете легко адаптировать его к работе в Microsoft Teams.) Мы рекомендуем вам использовать либо C, либо Node.js, чтобы воспользоваться [нашими SDKs](/microsoftteams/platform/#pivot=sdk-tools). Эти пакеты расширяют базовые классы и методы пакета SDK Bot Builder:

* Использование специализированных типов карт, таких как Office 365 Connector.
* Потребление и Teams конкретных каналов данных о деятельности.
* Обработка запросов на расширение обмена сообщениями.

Расширения SDK устанавливают зависимости, включая Bot Builder SDK.

* **.NET** Чтобы использовать Microsoft Teams для Bot Builder SDK для .NET, [установите пакет Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet в свой Visual Studio проект. Для Node.js разработки BotBuilder для Microsoft Teams функциональности был включен [в Bot Framework SDK](https://github.com/microsoft/botframework-sdk) по v4.6.

> [!IMPORTANT]
> Вы можете разрабатывать Teams приложения в любой другой технологии веб-программирования и [называть Bot Framework REST API напрямую,](/bot-framework/rest-api/bot-framework-rest-overview) но вы должны выполнять все токены обработки самостоятельно.

*Teams App Studio поможет* вам создать и настроить манифест приложения, а также создать для вас бота. Он также содержит React управления и интерактивную карту строитель.

## <a name="outgoing-webhooks"></a>Исходящие веб-перехватчики

Исходящие webhooks позволяют создать простой бот для базового взаимодействия, как запуск рабочего процесса или других простых команд, которые могут понадобиться. Исходящие вебхуки живут только в команде, в которой вы их создаете, и предназначены для простых процессов, характерных для рабочего процесса вашей компании. Для получения дополнительной информации, [см.](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="build-a-great-teams-bot"></a>Создайте отличный Teams бот

Следующие темы будут направлять вас через процесс создания большой бот для Teams:

* [Создайте бота:](~/resources/bot-v3/bots-create.md)Воспользуйтесь отличными инструментами, документацией и сообществом, предоставленными командой Bot Framework.
* [Поговорите со своим ботом:](~/resources/bot-v3/bot-conversations/bots-conversations.md)Добавьте базовый поток разговоров и используйте функцию, специфичную для канала. Если вы разрабатываете в .NET Node.js, используйте наши расширения для Bot Builder SDK, чтобы упростить вашу работу.
* [Использование карт в боте: Дизайн](~/resources/bot-v3/bots-cards.md)карт для общения и принятия ответа пользователя.
* [Реагировать на бот-события](~/resources/bot-v3/bots-notifications.md)
* [Боты только для уведомлений:](~/resources/bot-v3/bots-notification-only.md)Использование ботов для отправки уведомлений для вашего приложения.
* [Получить контекст](~/resources/bot-v3/bots-context.md): Получить информацию о пользователе.
* [Бот меню](~/resources/bot-v3/bots-menus.md): Использование меню в ботов.
* [Боты и файлы](~/resources/bot-v3/bots-files.md): Отправка и получение файлов от ботов.
* [Использование вкладок с ботами:](~/resources/bot-v3/bots-with-tabs.md)Создание вкладок и ботов работать вместе.
* [Проверьте свой бот:](~/resources/bot-v3/bots-test.md)Добавьте бота для личных или командных разговоров, чтобы увидеть его в действии.

## <a name="see-also"></a>См. также

[Образцы Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).