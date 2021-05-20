---
title: Создать бота
description: Описывает, как создавать ботов в Microsoft Teams
ms.topic: how-to
keywords: создание команд ботов
localization_priority: Normal
ms.date: 12/07/2018
ms.openlocfilehash: 67aa3e2cfd1950dced84785a9f6f35cfd4d5ff85
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566777"
---
# <a name="create-a-bot"></a>Создать бота

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Все боты, созданные с Microsoft Bot Framework, настроены и готовы к работе в Microsoft Teams.

Для получения дополнительной информации [см.](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true)

## <a name="create-a-bot-for-microsoft-teams"></a>Создание бота для Microsoft Teams

**Teams App Studio является** инструментом, который может помочь создать ваш бот, и пакет приложений, который ссылается на вашего бота. Оно также содержит библиотеку элементов управления React и настраиваемые примеры для карточек. Для получения дополнительной информации [см Teams.](~/concepts/build-and-test/app-studio-overview.md) Последующие шаги предполагают, что вы настраиваете бота вручную, а **не используете Teams App Studio:**

1. Создайте бота по этой ссылке: https://dev.botframework.com/bots/new . **После создания бота обязательно добавьте Microsoft Teams в виде канала из списка основных каналов.** Вы можете повторно использовать любой сгенерированный вами идентификатор приложения Майкрософт, если вы уже создали пакет или манифест приложения.

   ![Страница регистрации в Bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Если вы не хотите создавать бота в Azure, вы **должны использовать** эту ссылку для создания нового бота: https://dev.botframework.com/bots/new . Если вы нажмете **на создать бота** на портале Bot Framework вместо этого, вы [создадите своего бота в Microsoft Azure вместо](#bots-and-microsoft-azure) этого.

2. Создайте бота с [помощью пакета Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet, [Bot Framework SDK](https://github.com/microsoft/botframework-sdk)или [API Bot Connector.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)

3. Проверьте бота с [помощью Bot Framework Emulator](/bot-framework/debug-bots-emulator).

4. Развертывание бота в облачном сервисе, например, [Microsoft Azure.](https://azure.microsoft.com/) Кроме того, запустите приложение локально и используйте туннельную службу, [такую как ngrok,](https://ngrok.com) чтобы https:// конечную точку для вашего бота, например. `https://45az0eb1.ngrok.io/api/messages`

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Боты и Microsoft Azure
> По декабрь 2017 года портал Bot Framework оптимизирован для регистрации ботов в Microsoft Azure. Вот некоторые моменты, которые следует знать:
>
> * Каналы Microsoft Teams для ботов, зарегистрированных в Azure, являются бесплатными. Сообщения, отправленные Teams канал не будут засчитыться в потребляемые сообщения для бота.
> * В то время как можно [создать нового бота Bot Framework](https://dev.botframework.com/bots/new) без использования Azure, вы должны использовать этот URL https://dev.botframework.com/bots/new) (, который больше не подвергается на портале Bot Framework.
> * При редактировании свойств существующего бота в списке [ваших ботов в Bot Framework,](https://dev.botframework.com/bots) таких как его "конечная точка обмена сообщениями", которая является общей при первой разработке бота, особенно если вы [используете ngrok,](https://ngrok.com)вы увидите столбец "Миграционный статус" и синюю кнопку "Migrate", которая приведет вас в портал Microsoft Azure. Не нажимайте на кнопку "Migrate", если только это не то, что вы хотите сделать; вместо этого нажмите на имя бота, и вы можете редактировать его свойства:</br>
   ![Изменение свойств бота](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Если вы регистрируете бота с Microsoft Azure, ваш код бота не должен быть *размещен* на Microsoft Azure.
> * Если вы зарегистрировали бота с помощью портала Microsoft Azure, у вас должна быть учетная запись Microsoft Azure. Вы можете [создать ее бесплатно](https://azure.microsoft.com/free/). Чтобы проверить свою личность при ее создании, необходимо предоставить кредитную карту, но с нее не будет взиматься плата; это всегда бесплатно создавать и использовать ботов с Microsoft Teams.
> * Теперь вы можете использовать App Studio для регистрации/обновления информации о приложении и боте непосредственно в Microsoft Teams. Вам нужно будет использовать только портал Microsoft Azure для добавления или настройки других каналов Bot Framework, таких как Direct Line, Web Chat, Skype и Facebook Messenger.

## <a name="see-also"></a>См. также

[Образцы Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).