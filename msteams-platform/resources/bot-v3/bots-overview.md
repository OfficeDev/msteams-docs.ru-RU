---
title: Добавление ботов в приложения Microsoft Teams
description: Описывает, как начать разработку ботов в Microsoft Teams
ms.topic: conceptual
keywords: разработка командных ботов
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: c7b719aae3a8d1b09ed8a1be7f54028fe7f2481e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019757"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Добавление ботов в приложения Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Создание и подключение интеллектуальных ботов для естественного взаимодействия с пользователями Microsoft Teams с помощью чата. Или предостереите простой бот на основе команд, который будет использоваться в качестве интерфейса "командной строки" для более широкого взаимодействия с приложениями Teams. Вы можете сделать бот только для уведомлений, который может отправлять сведения, релевантные пользователям, непосредственно к ним в канале или прямом сообщении. Вы даже можете принести существующий бот на основе Bot Framework и добавить групповую поддержку, чтобы сделать ваш опыт блеском.

![Пример бота, помогая пользователю](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Что нужно знать: боты

Бот появляется так же, как и любой другой член группы, с помощью который вы взаимодействуете в беседе, за исключением того, что он имеет шестиугольную иконку аватара и всегда находится в сети.

Бот ведет себя по-разному в зависимости от того, в какой беседе он участвует. Bots in Teams support several kinds of conversations (called scopes in the [app manifest).](~/resources/schema/manifest-schema.md)

* `teams` Также называются телефонные беседы
* `personal` Беседы между ботом и одним пользователем
* `groupChat` Беседа между ботом и двумя или более пользователями

Дополнительные [сведения см. в записи беседы с ботом Microsoft Teams.](~/resources/bot-v3/bot-conversations/bots-conversations.md)

С помощью приложений Microsoft Teams вы можете сделать бота звездой вашего опыта или просто помощником. Боты распространяются как часть более широкого пакета приложений, который [](~/tabs/what-are-tabs.md) может включать другие возможности, такие как вкладки или [расширения обмена сообщениями.](~/messaging-extensions/what-are-messaging-extensions.md)

## <a name="bot-apis"></a>API бота

Microsoft Teams поддерживает большую часть [Microsoft Bot Framework.](https://dev.botframework.com/) (Если у вас уже есть бот, основанный на bot Framework, вы можете легко адаптировать его для работы в Microsoft Teams.) Мы рекомендуем использовать C# или Node.js, чтобы воспользоваться нашими [SDKs](/microsoftteams/platform/#pivot=sdk-tools). Эти пакеты расширяют базовые классы и методы пакета SDK Bot Builder:

* Использование специализированных типов карт, таких как соединитечная карта Office 365
* Потребление и установка данных каналов, определенных для Teams, в действиях
* Обработка запросов на расширение обмена сообщениями

В расширениях SDK устанавливаются зависимости, в том числе SDK bot Builder.

* **.NET** Чтобы использовать расширения Microsoft Teams для SDK bot Builder для .NET, установите пакет [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet в Visual Studio проекте. Для Node.js разработки функциональные возможности BotBuilder для Microsoft Teams были включены в [SDK](https://github.com/microsoft/botframework-sdk) Bot Framework по данным v4.6.

*См. также* [примеры Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

> [!IMPORTANT]
> Вы можете разрабатывать приложения Teams в любой другой технологии веб-программирования и вызывать [API](/bot-framework/rest-api/bot-framework-rest-overview) REST Bot Framework напрямую, но все обработки маркеров необходимо выполнять самостоятельно.

*Teams App Studio* помогает создавать и настраивать манифест приложения, а также может создавать бот Bot Framework для вас. Он также содержит библиотеку управления React и интерактивный строитель карт.

## <a name="outgoing-webhooks"></a>Исходящие веб-перехватчики

Исходяющие веб-окки позволяют создать простой бот для базового взаимодействия, например, при старте рабочего процесса или других простых команд, которые могут потребоваться. Исходяющие веб-оки живут только в команде, в которой вы их создаете, и предназначены для простых процессов, специфических для рабочего процесса вашей компании. Дополнительные сведения см. в [исходяющих веб-сайтах.](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="build-a-great-teams-bot"></a>Создание отличного бота Teams

Следующие темы будут направлять вас в процессе создания отличного бота для Teams.

* [Создание бота.](~/resources/bot-v3/bots-create.md)Воспользоваться преимуществами отличных инструментов, документации и сообщества, предоставляемых командой Bot Framework.
* [Поговорите с ботом.](~/resources/bot-v3/bot-conversations/bots-conversations.md)Добавьте основной поток беседы и используйте функции, определенные каналу. Если вы разрабатываете в .NET или Node.js, используйте наши расширения для SDK bot Builder, чтобы упростить работу.
* [Использование карт в боте](~/resources/bot-v3/bots-cards.md) Разработка карт для связи и реагировать на отклик пользователей.
* [Реагирование на события бота.](~/resources/bot-v3/bots-notifications.md)
* [Боты только для уведомлений](~/resources/bot-v3/bots-notification-only.md) Использование ботов для отправки уведомлений для приложения.
* [Получить контекст](~/resources/bot-v3/bots-context.md) Сведения о пользователе.
* [Меню бота](~/resources/bot-v3/bots-menus.md) Использование меню в ботах.
* [Боты и файлы](~/resources/bot-v3/bots-files.md) Отправка и получение файлов от ботов.
* [Использование вкладок с ботами](~/resources/bot-v3/bots-with-tabs.md) Создание вкладок и ботов для совместной работы.
* [Проверьте бот.](~/resources/bot-v3/bots-test.md)Добавьте бот для личных или командных бесед, чтобы увидеть его в действии.
