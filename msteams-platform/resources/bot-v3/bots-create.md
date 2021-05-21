---
title: Создать бота
description: Описывает создание ботов в Microsoft Teams
ms.topic: how-to
keywords: создание командных ботов
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

Дополнительные сведения см. в [документе Bot Framework Documentation](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) для общих сведений о ботах.

## <a name="create-a-bot-for-microsoft-teams"></a>Создание бота для Microsoft Teams

**Teams App Studio** — это средство, которое может помочь создать бот, а также пакет приложений, который ссылается на бота. Оно также содержит библиотеку элементов управления React и настраиваемые примеры для карточек. Дополнительные сведения см. в [Teams App Studio.](~/concepts/build-and-test/app-studio-overview.md) Последующие действия предполагают, что вы настраиваете бот вручную и не используете **Teams App Studio:**

1. Создайте бот с помощью этой ссылки: https://dev.botframework.com/bots/new . **После создания бота обязательно добавьте Microsoft Teams в виде канала из списка основных каналов.** Вы можете повторно использовать любой сгенерированный вами идентификатор приложения Майкрософт, если вы уже создали пакет или манифест приложения.

   ![Страница регистрации в Bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Если вы не хотите создавать бота  в Azure, необходимо использовать эту ссылку для создания нового бота: https://dev.botframework.com/bots/new . Если вместо этого нажать кнопку **Создать** бот на портале Bot Framework, вместо этого вы создайте бот в [Microsoft Azure.](#bots-and-microsoft-azure)

2. Создайте бот с помощью [пакета Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet, [SDK](https://github.com/microsoft/botframework-sdk)bot Framework или [API соединителов ботов.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)

3. Проверьте бот с помощью [Bot Framework Emulator](/bot-framework/debug-bots-emulator).

4. Развертывание бота в облачной службе, например [в Microsoft Azure.](https://azure.microsoft.com/) Кроме того, запустите приложение локально и используйте службу тоннелей, такую [ngrok,](https://ngrok.com) чтобы https:// конечную точку для вашего бота, например `https://45az0eb1.ngrok.io/api/messages` .

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Боты и Microsoft Azure
> С декабря 2017 г. портал Bot Framework оптимизирован для регистрации ботов в Microsoft Azure. Вот некоторые моменты, которые следует знать:
>
> * Каналы Microsoft Teams для ботов, зарегистрированных в Azure, являются бесплатными. Сообщения, отправленные по Teams канала, не будут учитываться в отношении потребляемых сообщений для бота.
> * Хотя можно создать новый бот [Bot Framework](https://dev.botframework.com/bots/new) без использования Azure, необходимо использовать этот URL-адрес ( который больше не будет выставлен на https://dev.botframework.com/bots/new) портале Bot Framework.
> * При редактировании свойств существующего бота в списке ваших ботов в [Bot Framework,](https://dev.botframework.com/bots) таких как его "конечная точка обмена сообщениями", которая распространена при первом разработке бота, особенно если вы используете [ngrok,](https://ngrok.com)вы увидите столбец "Состояние миграции" и голубую кнопку "Миграция", которая будет принимать вас на портале Microsoft Azure. Не нажимайте кнопку "Миграция", если это не то, что вы хотите сделать; вместо этого щелкните имя бота, и вы можете изменить его свойства:</br>
   ![Изменение свойств бота](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Если вы регистрируете бота Microsoft Azure, код бота  не должен быть Microsoft Azure.
> * Если вы зарегистрировали бота с помощью портала Microsoft Azure, у вас должна быть учетная запись Microsoft Azure. Вы можете [создать ее бесплатно](https://azure.microsoft.com/free/). Чтобы проверить вашу личность при создании, необходимо предоставить кредитную карту, но она не будет взиматься; всегда бесплатно создавать и использовать боты с помощью Microsoft Teams.
> * Теперь вы можете использовать App Studio для регистрации и обновления сведений о приложениях и ботах непосредственно в Microsoft Teams. Для добавления или настройки других каналов Bot Framework Microsoft Azure, таких как Direct Line, Web Chat, Skype и Facebook Messenger, необходимо использовать Microsoft Azure портал.

## <a name="see-also"></a>См. также

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).