---
title: Создать бота
description: Описание создания ботов в Microsoft Teams
ms.topic: how-to
keywords: создание ботов teams
ms.date: 12/07/2018
ms.openlocfilehash: d7c618adc99f814bd677e919923c4b616f293e17
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014091"
---
# <a name="create-a-bot"></a>Создать бота

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Все боты, созданные с помощью Microsoft Bot Framework, настроены и готовы к работе в Microsoft Teams.

Общие сведения о ботах см. в документации [Bot Framework.](/azure/bot-service/?view=azure-bot-service-3.0)

## <a name="create-a-bot-for-microsoft-teams"></a>Создание бота для Microsoft Teams

*Teams App Studio* — это средство, которое может помочь в создании бота и пакета приложения, который ссылается на бота. Оно также содержит библиотеку элементов управления React и настраиваемые примеры для карточек. См. статью [Начало работы с Teams App Studio](~/concepts/build-and-test/app-studio-overview.md). В последующих шагах предполагается, что вы вручную настраиваете бота и не используете *Teams App Studio.*

1. Создайте бота по этой https://dev.botframework.com/bots/new ссылке: **После создания бота обязательно добавьте Microsoft Teams в виде канала из списка основных каналов.** Вы можете повторно использовать любой сгенерированный вами идентификатор приложения Майкрософт, если вы уже создали пакет или манифест приложения.

   ![Страница регистрации в Bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Если вы не хотите создавать бота  в Azure, используйте эту ссылку для создания нового https://dev.botframework.com/bots/new бота: Если вместо этого нажать кнопку *"Создать* бота" на портале Bot Framework, вы создайте [бота в Microsoft Azure.](#bots-and-microsoft-azure)

2. Создайте бота с помощью [пакета Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet, [пакета Bot Framework SDK](https://github.com/microsoft/botframework-sdk)или [API соединители ботов.](https://docs.microsoft.com/bot-framework/rest-api/bot-framework-rest-connector-api-reference) *См. также* [примеры Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

3. Протестировать бота с помощью [эмулятора Bot Framework.](https://docs.microsoft.com/bot-framework/debug-bots-emulator)

4. Развертывание бота в облачной службе, например [Microsoft Azure.](https://azure.microsoft.com/) Кроме того, запустите приложение локально и используйте службу туннелинга, например [ngrok,](https://ngrok.com) для https:// конечной точки вашего бота, например `https://45az0eb1.ngrok.io/api/messages` .

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Боты и Microsoft Azure
> С декабря 2017 г. портал Bot Framework оптимизирован для регистрации ботов в Microsoft Azure. Вот некоторые моменты, которые следует знать:
>
> * Каналы Microsoft Teams для ботов, зарегистрированных в Azure, являются бесплатными. Сообщения, отправленные через канал Teams, не учитываются в потребляемых сообщениях для бота.
> * Хотя можно создать бот [Bot Framework](https://dev.botframework.com/bots/new) без использования Azure, необходимо использовать этот URL-адрес ( , который больше не возможен на https://dev.botframework.com/bots/new) портале Bot Framework.
> * При редактировании свойств существующего бота в списке ботов в [Bot Framework,](https://dev.botframework.com/bots) таких как "конечная точка обмена сообщениями", которая часто используется при разработке бота, особенно если вы используете [ngrok,](https://ngrok.com)вы увидите столбец "Состояние миграции" и синюю кнопку "Миграция", которая позволит перейти на портал Microsoft Azure. Не нажимайте кнопку "Миграция", если это не то, что вы хотите сделать; вместо этого щелкните имя бота и можете изменить его свойства:</br>
   ![Изменение свойств бота](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Если вы зарегистрируете бота с помощью Microsoft Azure, код бота не нужно будет использовать *в* Microsoft Azure.
> * Если вы зарегистрировали бота с помощью портала Microsoft Azure, у вас должна быть учетная запись Microsoft Azure. Вы можете [создать ее бесплатно](https://azure.microsoft.com/free/). Чтобы проверить свою личность при ее создании, необходимо предоставить кредитную карту, но она не будет взиматься; Всегда можно свободно создавать и использовать боты в Microsoft Teams.
> * Теперь вы можете использовать App Studio для регистрации и обновления сведений о приложениях и ботах непосредственно в Microsoft Teams. You'll only have to use the Microsoft Azure portal for adding/configuring other Bot Framework channels such as Direct Line, Web Chat, Skype, and Facebook Messenger.
