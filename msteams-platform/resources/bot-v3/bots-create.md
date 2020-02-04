---
title: Создание бота
description: Описывается создание боты в Microsoft Teams.
keywords: Создание боты в Teams
ms.date: 12/07/2018
ms.openlocfilehash: cb2d0974baf1d36a4acf077c219eb12449a5721a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675215"
---
# <a name="create-a-bot"></a>Создание бота

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Все боты, созданные с помощью Microsoft Bot Framework, настроены и готовы к работе в Microsoft Teams.

Общие сведения о боты можно найти в [документации по среде Bot](/azure/bot-service/?view=azure-bot-service-3.0) .

## <a name="create-a-bot-for-microsoft-teams"></a>Создание почтового робота для Microsoft Teams

*Приложение Teams Studio* — это средство, которое поможет вам создать робота и пакет приложения, ссылающийся на робот. Кроме того, она содержит библиотеку элементов управления реагируем и настраиваемые примеры для карточек. Ознакомьтесь с разделом [Приступая к работе с Teams App Studio](~/concepts/build-and-test/app-studio-overview.md). В приведенных ниже действиях предполагается, что вы настраиваете Bot и не используете *приложение Teams Studio*.

1. Создайте Bot с помощью этой ссылки: https://dev.botframework.com/bots/new. **После создания ленты не забудьте добавить Microsoft Teams в качестве канала из списка популярных каналов.** Вы можете повторно использовать любой идентификатор приложения Microsoft, созданный, если вы уже создали пакет или манифест приложения.

   ![Страница регистрации от платформы Bot](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Если вы не хотите создавать Bot в Azure, вы **должны** использовать эту ссылку для создания новой ленты: https://dev.botframework.com/bots/new. При нажатии кнопки *создать на* портале Bot Framework вместо этого вы [создадите робот в Microsoft Azure](#bots-and-microsoft-azure) .

2. Создайте Bot с помощью пакета NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) , [ботбуилдер-Teams](https://www.npmjs.com/package/botbuilder-teams) NPM или [API соединителя Bot](https://docs.microsoft.com/bot-framework/rest-api/bot-framework-rest-connector-api-reference).

3. Протестируйте Bot с помощью [эмулятора Bot Framework](https://docs.microsoft.com/bot-framework/debug-bots-emulator).

4. Развертывание ленты в облачной службе, такой как [Microsoft Azure](https://azure.microsoft.com/). Кроме того, запустите свое приложение на локальном компьютере и используйте службу туннелирования, например, [ngrok](https://ngrok.com) для предоставления конечной точки HTTPS://для ленты `https://45az0eb1.ngrok.io/api/messages`, например.

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Боты и Microsoft Azure
> На декабрь 2017, портал Bot Framework оптимизирован для регистрации боты в Microsoft Azure. Ниже приведены некоторые моменты, которые необходимо знать:
>
> * Канал Microsoft Teams для Боты, зарегистрированный в Azure, бесплатный. Сообщения, отправляемые по каналу Teams, не будут подсчитываться до использованных сообщений для Bot.
> * Несмотря на то, что вы можете [создать новый элемент ленты](https://dev.botframework.com/bots/new) Bot, не используя Azure, необходимо использовать этот URLhttps://dev.botframework.com/bots/new)-адрес (который больше не отображается на портале Bot Framework).
> * При изменении свойств существующего элемента Bot в [списке боты в Bot Framework](https://dev.botframework.com/bots) , например "конечная точка для обмена сообщениями", которая является распространенной при первой разработке ленты, особенно при использовании [ngrok](https://ngrok.com), появится столбец "состояние миграции" и синяя кнопка "переносить", которая попытается перейти на портал Microsoft Azure. Не нажимайте кнопку "переносить", пока не хотите делать это. Вместо этого щелкните имя Bot и вы можете изменить его свойства:</br>
   ![Изменение свойств элемента Bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Если вы зарегистрировали программу Bot с помощью Microsoft Azure, код для ленты не должен *размещаться* в Microsoft Azure.
> * Если вы зарегистрировали Bot с помощью портала Microsoft Azure, у вас должна быть учетная запись Microsoft Azure. Вы можете [создать его бесплатно](https://azure.microsoft.com/free/). Чтобы проверить удостоверение при создании, необходимо предоставить кредитную карту, но она не будет взиматься; Вы всегда можете создавать и использовать боты в Microsoft Teams.
> * Теперь вы можете использовать приложение App Studio для регистрации и обновления сведений о приложении и Bot непосредственно в Microsoft Teams. Вам потребуется использовать портал Microsoft Azure для добавления и настройки других каналов ленты, таких как прямые линии, Интернет-чат, Skype и Facebook Messenger.
