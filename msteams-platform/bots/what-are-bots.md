---
title: Боты в Microsoft Teams
author: surbhigupta
description: В этой статье вы можете использовать чат-боты в Microsoft Teams для совместного использования файлов, отправки упреждающего уведомления, интерактивных карточек, выполнения звонков, вызова команды бота, IVR.
ms.topic: overview
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 90176b63c64d23ae76a8c98515e37455ab0742c0
ms.sourcegitcommit: 217025a61ed9c3b76b507fe95563142abc6d0318
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/17/2022
ms.locfileid: "67363508"
---
# <a name="build-bots-for-teams"></a>Создание ботов для Teams

> [!NOTE]
> Рекомендуется создать свое первое приложение бота или приложение бота уведомлений с помощью средства разработки нового поколения для Teams. Дополнительные сведения см. в [разделе "Набор средств Teams для Visual Studio Code](../toolkit/teams-toolkit-fundamentals.md) [и Набор средств Teams для Visual Studio"](../toolkit/teams-toolkit-overview-visual-studio.md).

Бот также называется чат-ботом или ботом для общения. Это приложение, которое выполняет простые и повторяющиеся задачи пользователей, например в службах обслуживания или поддержки клиентов. В быту используются боты, которые сообщают сведения о погоде, бронируют рестораны или предоставляют сведения для путешествий. Взаимодействие с ботами может быть в виде быстрых вопросов и ответов или сложных бесед.

> [!IMPORTANT]
>
> * Сейчас боты доступны в облаке сообщества для государственных организаций (GCC) и GCC High, но не в средах Министерства обороны США (DoD).
>
> * Приложения-боты в Microsoft Teams доступны в GCC-High через [службу ботов Azure](/azure/bot-service/how-to-deploy-gov-cloud-high), а регистрацию канала бота необходимо выполнить на портале Microsoft Azure для государственных организаций.
>
> * Приложения в GCCH поддерживают только версию манифеста v1.10. URL-адреса изображений в адаптивных карточках не поддерживаются в среде GCCH. URL-адрес изображения можно заменить на DataUri в кодировке Base64.

Боты для общения позволяют пользователям взаимодействовать с веб-службой с помощью текста, интерактивных карточек и модулей задач.

:::image type="content" source="../assets/images/invokebotwithtext.png" alt-text="На снимке экрана показан пример веб-службы с текстом."lightbox="../assets/images/invokebotwithtext.png":::

:::image type="content" source="../assets/images/invokebotwithcard.png" alt-text="На снимке экрана показан пример веб-службы с интерактивными карточками."lightbox="../assets/images/invokebotwithcard.png"border="true":::

:::image type="content" source="../assets/images/task-module-example.png" alt-text="На снимке экрана показан пример веб-службы, использующей модуль задач." lightbox="../assets/images/task-module-example-expanded.png":::

Боты для общения чрезвычайно гибкие. Боты могут обрабатывать несколько основных команд или сложных задач, которые включают искусственный интеллект и обработку естественного языка. Боты могут быть частью большего приложения или быть автономными.

Используйте правильное сочетание карточек, текста и модулей задач для создания полезного бота. На следующем изображении показано, как пользователь общается с ботом в личном чате с помощью текста и интерактивных карточек.

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="На снимке экрана показан пример бота часто задаваемых вопросов.":::

Каждое взаимодействие между пользователем и ботом представлено как действие. Когда бот получает действие, он передает его обработчикам действий. См. статью об [обработчиках действий ботов](~/bots/bot-basics.md).

Боты — это приложения с интерфейсом бесед. Вы можете взаимодействовать с ботом с помощью текста, интерактивных карточек и речи. Бот ведет себя по-разному в канале или групповом чате, а также в личной беседе. Беседы обрабатываются через соединители Bot Framework. См. статью [об основах бесед с ботами](~/bots/how-to/conversations/conversation-basics.md).

Для доступа к соответствующему содержимому и улучшения работы бота требуется контекстная информация, например сведения о профиле пользователя. См. статью о [получении контекста в Teams](~/bots/how-to/get-teams-context.md).

Вы можете отправлять и получать файлы с помощью бота через API Graph или API бота Teams. См. статью об [отправке и получении файлов с помощью ботов](~/bots/how-to/bots-filesv4.md).

Для оптимизации ботов, используемых для приложения Teams, применяется ограничение скорости трафика. Чтобы защитить Teams и его пользователей, API бота предоставляют ограничение скорости для входящих запросов. См. статью [Оптимизация бота с ограничением скорости в Teams](~/bots/how-to/rate-limit.md).

С помощью API Microsoft Graph для звонков и онлайн-собраний приложения Teams теперь могут взаимодействовать с пользователями с помощью голосовых вызовов и видеосвязи. См. статью о [ботах для звонков и собраний](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).

Вы можете использовать API бота Teams для получения сведений для участников чата или команды. См. статью об [изменениях API ботов Teams для получения сведений участников команды или чата](~/resources/team-chat-member-api-changes.md).

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Боты и пакеты SDK](~/bots/bot-features.md)

## <a name="code-samples"></a>Примеры кода

|Название примера | Описание | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Напоминание о ежедневной задаче бота| Демонстрация создания графика повторяющейся задачи и получения напоминания в запланированное время. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |
| Hello World Bot | Это простое приложение Hello World с возможностями расширения Bot и Message. |  | [Просмотр](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/hello-world-bot) |
| Уведомление адаптивной карточки | Это пример, в котором показано, как отправлять уведомления с помощью различных адаптивных карточек с помощью ботов. |  | [Просмотр](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/adaptive-card-notification) |
| Входящее уведомление веб-перехватчика | В этом примере показано, как отправлять уведомления через входящий веб-перехватчик в каналах Microsoft Teams. |  | [Просмотр](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/incoming-webhook-notification) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Создать бота для Teams](../resources/bot-v3/bots-create.md)
* [Как работают боты Microsoft Teams](/azure/bot-service/bot-builder-basics-teams)
* [Регистрация бота для звонков и собраний для Microsoft Teams](~/bots/calls-and-meetings/registering-calling-bot.md)
* [Добавление проверки подлинности для бота Teams](~/bots/how-to/authentication/add-authentication.md)
* [Обработчики действий ботов](~/bots/bot-basics.md)
* [События бесед в вашем боте Teams](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [Создание первого приложения бота с помощью JavaScript](../sbs-gs-bot.yml)
* [Создание бота уведомлений с помощью JavaScript](../sbs-gs-notificationbot.yml)
