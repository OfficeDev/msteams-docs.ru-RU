---
title: Создать бота
description: В этом модуле вы узнаете, как создать ботов с помощью Microsoft Bot Framework и готовых к работе в Microsoft Teams.
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 12/07/2018
ms.openlocfilehash: 0f53f26c8cb54c1d21cbe305d3ea1d433bfb864b
ms.sourcegitcommit: fb0942afb8be32d92df282dec03fbb3b13f8f303
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2022
ms.locfileid: "67264171"
---
# <a name="create-a-bot"></a>Создать бота

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Все боты, созданные с Microsoft Bot Framework, настроены и готовы к работе в Microsoft Teams.

Дополнительные сведения о ботах см. в документации [по Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) .

## <a name="create-a-bot-for-microsoft-teams"></a>Создание бота для Microsoft Teams

**Teams App Studio** — это средство, которое может помочь создать бот и пакет приложения, который ссылается на бот. Оно также содержит библиотеку элементов управления React и настраиваемые примеры для карточек. Дополнительные сведения см. в [статье "Начало работы с Teams App Studio"](~/concepts/build-and-test/app-studio-overview.md). В следующих шагах предполагается, что вы вручную настраиваете бот, а не используете **Teams App Studio**:

1. Создайте бот с помощью [Bot Framework](https://dev.botframework.com/bots/new). **После создания бота обязательно добавьте Microsoft Teams в виде канала из списка основных каналов.** Вы можете повторно использовать любой сгенерированный вами идентификатор приложения Майкрософт, если вы уже создали пакет или манифест приложения.

   ![Страница регистрации в Bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Если вы не хотите создавать бота в Azure, используйте эту ссылку для создания нового бота: [Bot Framework](https://dev.botframework.com/bots/new). Если вместо этого щелкнуть "Создать **бот"** на портале Bot Framework, вы создайте бот [в Microsoft Azure](#bots-and-microsoft-azure) .

2. Создайте бот с помощью [пакета NuGet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) ,  [пакета SDK Bot Framework](https://github.com/microsoft/botframework-sdk) или [API Bot Connector](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).

3. Протестируйте бот с помощью [Bot Framework Emulator](/bot-framework/debug-bots-emulator).

4. Разверните бот в облачной службе, например [Microsoft Azure](https://azure.microsoft.com/). Кроме того, можно запустить приложение локально и использовать службу туннелирования, такую [как ngrok](https://ngrok.com) , чтобы предоставить конечную точку https:// для бота, `https://45az0eb1.ngrok.io/api/messages`например .

> [!NOTE]
>
> ## <a name="bots-and-microsoft-azure"></a>Боты и Microsoft Azure
>
> С декабря 2017 г. портал Bot Framework оптимизирован для регистрации ботов в Microsoft Azure. Вот некоторые моменты, которые следует знать:
>
> * Каналы Microsoft Teams для ботов, зарегистрированных в Azure, являются бесплатными. Сообщения, отправляемые по каналу Teams, не учитываются в потребляемых сообщениях для бота.
> * Хотя можно создать бот [Bot Framework](https://dev.botframework.com/bots/new) без использования Azure, необходимо создать бот [Bot Framework](https://dev.botframework.com/bots/new), который больше не доступен на портале Bot Framework.
> * При изменении свойств существующего бота в списке ботов [в Bot Framework](https://dev.botframework.com/bots), таких как "конечная точка обмена сообщениями", которая часто используется при разработке бота, особенно при использовании [ngrok](https://ngrok.com), вы увидите столбец "Состояние миграции" и синюю кнопку "Миграция", которая приведет вас в Microsoft портал Azure. Не нажимайте кнопку "Миграция", если это не нужно сделать. Вместо этого щелкните имя бота, и вы можете изменить его свойства:</br>
   ![Изменение свойств бота](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Если вы регистрируете бот с помощью Microsoft Azure, код бота не обязательно должен быть *размещен в Microsoft* Azure.
> * Если вы регистрируете бот с портал Azure, у вас должна быть учетная запись Microsoft Azure. Вы можете [создать ее бесплатно](https://azure.microsoft.com/free/). Чтобы проверить удостоверение при его создании, необходимо предоставить кредитную карту, но с нее не будет взиматься плата. Всегда можно создавать и использовать боты в Teams.
> * Теперь вы можете использовать App Studio для регистрации или обновления сведений о приложении и боте непосредственно в Teams. Для добавления или настройки других каналов Bot Framework, таких как Direct Line, Веб-чат, Skype и Facebook Messenger, необходимо использовать только этот портал Azure.

> [!WARNING]
>
>* Если вы использовали App Studio, рекомендуем попробовать Портал разработчика для настройки, распространения и управления приложениями Teams. App Studio не рекомендуется к использованию 1 августа 2022 г.

## <a name="see-also"></a>Дополнительные ресурсы

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
