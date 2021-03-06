---
title: Добавление ботов в Microsoft Teams приложения
description: Описывает, как начать разработку ботов в Microsoft Teams
ms.topic: conceptual
keywords: разработка командных ботов
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

Создание и подключение интеллектуальных ботов для взаимодействия с Microsoft Teams пользователями естественным образом с помощью чата. Или предостереите простой бот на основе команд, который будет использоваться в качестве интерфейса "командной строки" для более широкого Teams приложения. Вы можете сделать бот только для уведомлений, который может отправлять сведения, релевантные пользователям, непосредственно к ним в канале или прямом сообщении. Вы даже можете принести существующий бот на основе Bot Framework и добавить Teams поддержку, чтобы сделать ваш опыт блеском.

![Пример бота, помогая пользователю](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Что нужно знать: боты

Бот появляется так же, как и любой другой член группы, с помощью который вы взаимодействуете в беседе, за исключением того, что он имеет шестиугольную иконку аватара и всегда находится в сети.

Бот ведет себя по-разному в зависимости от того, в какой беседе он участвует. Боты в Teams поддерживают несколько видов бесед, называемых областью в [манифесте приложения.](~/resources/schema/manifest-schema.md)

* `teams` Также называются телефонные беседы.
* `personal` Беседы между ботом и одним пользователем.
* `groupChat` Беседа между ботом и двумя или более пользователями.

Дополнительные сведения см. [в ссылке Беседа с Microsoft Teams ботом.](~/resources/bot-v3/bot-conversations/bots-conversations.md)

С Microsoft Teams приложениями вы можете сделать бота звездой вашего опыта или просто помощником. Боты распространяются как часть более широкого пакета приложений, который [](~/tabs/what-are-tabs.md) может включать другие возможности, такие как вкладки или [расширения обмена сообщениями.](~/messaging-extensions/what-are-messaging-extensions.md)

## <a name="bot-apis"></a>API бота

Microsoft Teams поддерживает большую часть [Microsoft Bot Framework](https://dev.botframework.com/). (Если у вас уже есть бот, основанный на bot Framework, вы можете легко адаптировать его к работе в Microsoft Teams.) Мы рекомендуем использовать C# или Node.js, чтобы воспользоваться нашими [SDKs](/microsoftteams/platform/#pivot=sdk-tools). Эти пакеты расширяют базовые классы и методы пакета SDK Bot Builder:

* Использование специализированных типов карт, таких как Office 365 connector.
* Потребление и настройка Teams определенных каналов данных о действиях.
* Обработка запросов на расширение обмена сообщениями.

В расширениях SDK устанавливаются зависимости, в том числе SDK bot Builder.

* **.NET** Чтобы использовать Microsoft Teams для SDK bot Builder для .NET, установите пакет [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet в Visual Studio проекте. Для Node.js разработки функциональность BotBuilder для Microsoft Teams была включена в [SDK](https://github.com/microsoft/botframework-sdk) Bot Framework по ст. 4.6.

> [!IMPORTANT]
> Вы можете разрабатывать Teams в любой другой технологии веб-программирования и вызывать [API](/bot-framework/rest-api/bot-framework-rest-overview) REST Bot Framework напрямую, но все обработки маркеров необходимо выполнять самостоятельно.

*Teams App Studio* помогает создавать и настраивать манифест приложения и может создавать бот Bot Framework для вас. Он также содержит библиотеку React управления и интерактивный конструктор карт.

## <a name="outgoing-webhooks"></a>Исходящие веб-перехватчики

Исходяющие веб-окки позволяют создать простой бот для базового взаимодействия, например, при старте рабочего процесса или других простых команд, которые могут потребоваться. Исходяющие веб-оки живут только в команде, в которой вы их создаете, и предназначены для простых процессов, специфических для рабочего процесса вашей компании. Дополнительные сведения см. [в веб-сайтах.](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="build-a-great-teams-bot"></a>Создание отличного Teams бота

Следующие темы будут направлять вас в процессе создания отличного бота для Teams:

* [Создание бота.](~/resources/bot-v3/bots-create.md)Воспользоваться преимуществами отличных инструментов, документации и сообщества, предоставляемых командой Bot Framework.
* [Поговорите с ботом.](~/resources/bot-v3/bot-conversations/bots-conversations.md)Добавьте основной поток беседы и используйте функции, определенные каналу. Если вы разрабатываете в .NET или Node.js, используйте наши расширения для SDK bot Builder, чтобы упростить работу.
* [Использование карт в боте:](~/resources/bot-v3/bots-cards.md)разработка карт для связи и реагировать на отклик пользователей.
* [Реагирование на события бота](~/resources/bot-v3/bots-notifications.md)
* [Боты только для уведомлений.](~/resources/bot-v3/bots-notification-only.md)Использование ботов для отправки уведомлений для вашего приложения.
* [Получить контекст.](~/resources/bot-v3/bots-context.md)Сведения о пользователе.
* [Меню бота.](~/resources/bot-v3/bots-menus.md)Использование меню в ботах.
* [Боты и файлы:](~/resources/bot-v3/bots-files.md)отправка и получение файлов от ботов.
* [Использование вкладок с ботами:](~/resources/bot-v3/bots-with-tabs.md)создание вкладки и боты работают вместе.
* [Проверьте бот.](~/resources/bot-v3/bots-test.md)Добавьте бот для личных или командных бесед, чтобы увидеть его в действии.

## <a name="see-also"></a>См. также

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).