---
title: Тестирование и отлагивание бота локально
author: clearab
description: Тестирование и отладка бота локально с помощью IDE
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: af4b8d38b763d2266ec64fef0fe8c487b9120773
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631015"
---
# <a name="test-and-debug-your-bot-locally"></a><span data-ttu-id="7569a-103">Тестирование и отлагивание бота локально</span><span class="sxs-lookup"><span data-stu-id="7569a-103">Test and debug your bot locally</span></span>

<span data-ttu-id="7569a-104">При тестировании бота необходимо учитывать как контексты, в которые требуется запустить бота, так и все функциональные возможности, которые вы могли добавить в бот, для чего требуются данные, Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7569a-104">When testing your bot you need to take into consideration both the contexts you want your bot to run in, and any functionality you may have added to your bot that requires data specific to Microsoft Teams.</span></span> <span data-ttu-id="7569a-105">Убедитесь, что метод тестирования бота соответствует его функциональным возможностям.</span><span class="sxs-lookup"><span data-stu-id="7569a-105">Make sure that the method you choose to test your bot aligns with its functionality.</span></span>

## <a name="test-by-uploading-to-teams"></a><span data-ttu-id="7569a-106">Проверьте, загрузив Teams</span><span class="sxs-lookup"><span data-stu-id="7569a-106">Test by uploading to Teams</span></span>

<span data-ttu-id="7569a-107">Наиболее полный способ тестирования бота — это создание пакета приложений и его загрузка в Teams.</span><span class="sxs-lookup"><span data-stu-id="7569a-107">The most comprehensive way to test your bot is by creating an app package and uploading it to Teams.</span></span> <span data-ttu-id="7569a-108">Это единственный способ тестирования всех функциональных возможностей, доступных вашему боту, во всех сферах.</span><span class="sxs-lookup"><span data-stu-id="7569a-108">This is the only method to test the full functionality available to your bot, across all scopes.</span></span>

<span data-ttu-id="7569a-109">Существует два метода для загрузки приложения:</span><span class="sxs-lookup"><span data-stu-id="7569a-109">There are two methods for uploading your app:</span></span>
* <span data-ttu-id="7569a-110">Используйте [App Studio](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7569a-110">Use [App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>
* <span data-ttu-id="7569a-111">[Создайте пакет приложения](~/concepts/build-and-test/apps-package.md) вручную, а затем [загрузите приложение.](~/concepts/deploy-and-publish/apps-upload.md)</span><span class="sxs-lookup"><span data-stu-id="7569a-111">[Create an app package](~/concepts/build-and-test/apps-package.md) manually, and then [upload your app](~/concepts/deploy-and-publish/apps-upload.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7569a-112">Если необходимо изменить манифест и повторно загрузить приложение, [](#delete-a-bot-from-teams) перед отправкой измененного пакета приложения необходимо удалить бот.</span><span class="sxs-lookup"><span data-stu-id="7569a-112">If you need to alter your manifest and re-upload your app, you must [delete your bot](#delete-a-bot-from-teams) before uploading your altered app package.</span></span>

## <a name="debug-your-bot-locally"></a><span data-ttu-id="7569a-113">Отламывка бота локально</span><span class="sxs-lookup"><span data-stu-id="7569a-113">Debug your bot locally</span></span>

<span data-ttu-id="7569a-114">Если во время разработки вы размещены локально, для тестирования бота необходимо использовать службу тоннелей, например [ngrok.](https://ngrok.com/)</span><span class="sxs-lookup"><span data-stu-id="7569a-114">If you are hosting your bot locally during development, you need to use a tunneling service like [ngrok](https://ngrok.com/) in order to test your bot.</span></span> <span data-ttu-id="7569a-115">После загрузки и установки ngrok добавьте на свой путь и запустите следующую команду, `ngrok` чтобы запустить службу тоннелей:</span><span class="sxs-lookup"><span data-stu-id="7569a-115">After you download and install ngrok, add `ngrok` to your path, and run the following command to start the tunneling service:</span></span>

```bash
ngrok http <port> -host-header=localhost:<port>
```

<span data-ttu-id="7569a-116">Используйте конечную точку https, предоставленную ngrok в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="7569a-116">Use the https endpoint provided by ngrok in your app manifest.</span></span> 

> [!NOTE]
> <span data-ttu-id="7569a-117">При закрытии окна команды и перезапуске создается новый URL-адрес, и для его использования необходимо обновить конечный адрес бота.</span><span class="sxs-lookup"><span data-stu-id="7569a-117">If you close your command window and restart, a new URL is generated and you need to update your bot endpoint address to use it.</span></span>

## <a name="test-your-bot-without-uploading-to-teams"></a><span data-ttu-id="7569a-118">Тестирование бота без загрузки в Teams</span><span class="sxs-lookup"><span data-stu-id="7569a-118">Test your bot without uploading to Teams</span></span>

<span data-ttu-id="7569a-119">Иногда может потребоваться протестировать бот, не установив его в качестве приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="7569a-119">Occasionally, it may be necessary to test your bot without installing it as an app in Teams.</span></span> <span data-ttu-id="7569a-120">Мы предоставляем два метода тестирования бота.</span><span class="sxs-lookup"><span data-stu-id="7569a-120">We provide two methods for testing the bot.</span></span> <span data-ttu-id="7569a-121">Тестирование бота без установки его в качестве приложения может быть полезным для обеспечения того, что бот доступен и отвечает, однако это не позволит вам проверить всю широту функциональных возможностей Microsoft Teams, которые вы, возможно, добавили в бот.</span><span class="sxs-lookup"><span data-stu-id="7569a-121">Testing your bot without installing it as an app can be useful to ensure your bot is available and responding, however it won't allow you to test the full breadth of Microsoft Teams functionality you may have added to your bot.</span></span> <span data-ttu-id="7569a-122">Если вам нужно полностью протестировать бот, см. в этой ленте [тестирование, загрузив](#test-by-uploading-to-teams).</span><span class="sxs-lookup"><span data-stu-id="7569a-122">If you need to fully test your bot, see [testing by uploading](#test-by-uploading-to-teams).</span></span>

### <a name="use-the-bot-emulator"></a><span data-ttu-id="7569a-123">Использование эмулятора бота</span><span class="sxs-lookup"><span data-stu-id="7569a-123">Use the Bot Emulator</span></span>

<span data-ttu-id="7569a-124">The Bot Framework Emulator это настольное приложение, которое позволяет разработчикам-ботам тестировать и отлагировать их боты локально или удаленно.</span><span class="sxs-lookup"><span data-stu-id="7569a-124">The Bot Framework Emulator is a desktop application that permits bot developers to test and debug their bots locally or remotely.</span></span> <span data-ttu-id="7569a-125">Эмулятор помогает вам общаться с ботом и проверять сообщения, которые отправляет и получает бот.</span><span class="sxs-lookup"><span data-stu-id="7569a-125">The emulator helps you to chat with your bot and inspect the messages that your bot sends and receives.</span></span> <span data-ttu-id="7569a-126">Это может быть полезно для проверки того, что ваш бот доступен и отвечает.</span><span class="sxs-lookup"><span data-stu-id="7569a-126">This can be useful for verifying that your bot is available and responding.</span></span> <span data-ttu-id="7569a-127">Однако эмулятор не позволяет проверить какие-либо функциональные возможности Teams которые вы добавили в бот, и ответы от бота не являются точным визуальным представлением того, как они отрисовываны в Teams.</span><span class="sxs-lookup"><span data-stu-id="7569a-127">However, the emulator does not permit you to test any Teams-specific functionality you have added to the bot, nor the responses from your bot are an accurate visual representation of how they are rendered in Teams.</span></span> <span data-ttu-id="7569a-128">Если вам нужно проверить любой из этих вещей, лучше всего [загрузить бот](#test-by-uploading-to-teams).</span><span class="sxs-lookup"><span data-stu-id="7569a-128">If you need to test either of those things it is best to [upload your bot](#test-by-uploading-to-teams).</span></span>

<span data-ttu-id="7569a-129">Дополнительные сведения [см. в полных инструкциях по Bot Framework Emulator.](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="7569a-129">For more information, see [complete instructions on the Bot Framework Emulator](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).</span></span>

### <a name="talk-to-your-bot-directly-by-id"></a><span data-ttu-id="7569a-130">Поговорите с ботом напрямую по ID</span><span class="sxs-lookup"><span data-stu-id="7569a-130">Talk to your bot directly by ID</span></span>

> [!Important]
> <span data-ttu-id="7569a-131">Беседа с ботом по ID предназначена только для основных целей тестирования.</span><span class="sxs-lookup"><span data-stu-id="7569a-131">Talking to your bot by ID is intended for basic testing purposes only.</span></span> <span data-ttu-id="7569a-132">Все Teams, которые вы добавили в бот, не работают.</span><span class="sxs-lookup"><span data-stu-id="7569a-132">Any Teams-specific functionality you have added to your bot fails to work.</span></span>

<span data-ttu-id="7569a-133">Вы также можете инициировать беседу с ботом с помощью его ID.</span><span class="sxs-lookup"><span data-stu-id="7569a-133">You can also initiate a conversation with your bot by using its ID.</span></span> <span data-ttu-id="7569a-134">Когда бот был добавлен с помощью одного из этих методов, он не может быть адресоварен в беседах с каналами, и вы не можете воспользоваться другими возможностями Microsoft Teams приложения, такими как вкладки или расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="7569a-134">When a bot has been added through one of these methods it is not addressable in channel conversations and you cannot take advantage of other Microsoft Teams app capabilities like tabs or messaging extensions.</span></span> <span data-ttu-id="7569a-135">Вы можете инициировать беседу одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="7569a-135">You can initiate a conversation in one of the following ways:</span></span>

* <span data-ttu-id="7569a-136">На странице [Панель мониторинга](https://dev.botframework.com/bots) бота для бота в **статье Channels** выберите **Добавить Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="7569a-136">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Channels**, select **Add to Microsoft Teams**.</span></span> <span data-ttu-id="7569a-137">Microsoft Teams запускает личный чат с ботом.</span><span class="sxs-lookup"><span data-stu-id="7569a-137">Microsoft Teams launches a personal chat with your bot.</span></span>

* <span data-ttu-id="7569a-138">Непосредственно ссылаться на ID приложения вашего бота из Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="7569a-138">Directly reference your bot's app ID from within Microsoft Teams:</span></span>
   1. <span data-ttu-id="7569a-139">На странице [Панель мониторинга бота](https://dev.botframework.com/bots) для бота в **статье Details** скопируйте **ID приложения Microsoft для** бота.</span><span class="sxs-lookup"><span data-stu-id="7569a-139">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Details**, copy the **Microsoft App ID** for your bot.</span></span>
  
      ![Получение приложения для бота](~/assets/images/bots_appid_botframework.png)
  
   2. <span data-ttu-id="7569a-141">Откройте Microsoft Teams на области **чата** выберите значок **Добавить чат.**</span><span class="sxs-lookup"><span data-stu-id="7569a-141">Open Microsoft Teams, on the **Chat** pane, select the **Add chat** icon.</span></span> <span data-ttu-id="7569a-142">В **To:** вклейте iD Microsoft App вашего бота.</span><span class="sxs-lookup"><span data-stu-id="7569a-142">In **To:**, paste your bot's Microsoft App ID.</span></span>
  
      ![Загрузка ботов](~/assets/images/bots_uploading.png)

      <span data-ttu-id="7569a-144">ID приложения должен разрешить имя бота.</span><span class="sxs-lookup"><span data-stu-id="7569a-144">The app ID must resolve to your bot name.</span></span>

   3. <span data-ttu-id="7569a-145">Выберите бот и отправьте сообщение для начала беседы.</span><span class="sxs-lookup"><span data-stu-id="7569a-145">Select your bot and send a message to initiate a conversation.</span></span>
      <span data-ttu-id="7569a-146">Кроме того, вы можете вклеить ID приложения вашего бота в поле поиска в верхнем левом Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7569a-146">Alternatively, you can paste your bot's app ID in the search box in the top left in Microsoft Teams.</span></span> <span data-ttu-id="7569a-147">На странице результаты поиска перейдите на вкладку **People,** чтобы увидеть бота и начать с ним общаться в чате.</span><span class="sxs-lookup"><span data-stu-id="7569a-147">In the search results page, navigate to the **People** tab to see your bot and to start chatting with it.</span></span>

<span data-ttu-id="7569a-148">Ваш бот получает событие при добавлении ботов в команду без сведений о команде `conversationUpdate` в `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="7569a-148">Your bot receives the `conversationUpdate` event as you add the bots to a team, without the team information in the `channelData` object.</span></span>

## <a name="block-a-bot-in-personal-chat"></a><span data-ttu-id="7569a-149">Блокировка бота в личном чате</span><span class="sxs-lookup"><span data-stu-id="7569a-149">Block a bot in personal chat</span></span>

<span data-ttu-id="7569a-150">Пользователи могут заблокировать ваш бот от отправки личных сообщений чата.</span><span class="sxs-lookup"><span data-stu-id="7569a-150">Users can choose to block your bot from sending personal chat messages.</span></span> <span data-ttu-id="7569a-151">Они могут переметнуть это, щелкнув бот правой кнопкой мыши в канале чата и выбрав **блок-бот-беседу.**</span><span class="sxs-lookup"><span data-stu-id="7569a-151">They may toggle this by right-clicking your bot in the chat channel and choosing **Block bot conversation**.</span></span> <span data-ttu-id="7569a-152">Это означает, что ваши боты продолжают отправлять сообщения, однако пользователь не получает сообщения.</span><span class="sxs-lookup"><span data-stu-id="7569a-152">This means, your bots continues to send messages, however, the user does not receive the messages.</span></span>

![Блокировка бота](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a><span data-ttu-id="7569a-154">Удаление бота из группы</span><span class="sxs-lookup"><span data-stu-id="7569a-154">Remove a bot from a team</span></span>

<span data-ttu-id="7569a-155">Пользователи могут удалить бот, выбрав значок корзины в списке ботов в представлении команды.</span><span class="sxs-lookup"><span data-stu-id="7569a-155">Users can delete the bot by choosing the trash-can icon on the bots list in their team's view.</span></span> <span data-ttu-id="7569a-156">Это только удаляет бот из использования этой группы, отдельные пользователи по-прежнему могут взаимодействовать в личном контексте.</span><span class="sxs-lookup"><span data-stu-id="7569a-156">This only removes the bot from that team's use, individual users can still interact in personal context.</span></span> <span data-ttu-id="7569a-157">Боты в личном контексте не могут быть отключены или удалены пользователями.</span><span class="sxs-lookup"><span data-stu-id="7569a-157">Bots in personal context cannot be disabled or removed by users.</span></span>

## <a name="disable-a-bot-in-teams"></a><span data-ttu-id="7569a-158">Отключить бот в Teams</span><span class="sxs-lookup"><span data-stu-id="7569a-158">Disable a bot in Teams</span></span>

<span data-ttu-id="7569a-159">Чтобы остановить получение сообщений ботом,  перейдите на панель мониторинга бота и отредактировать канал Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7569a-159">To stop your bot from receiving messages, go to your **Bot Dashboard** and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="7569a-160">Очистка **параметра Включить Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="7569a-160">Clear the **Enable on Microsoft Teams** option.</span></span> <span data-ttu-id="7569a-161">Это не позволяет пользователям взаимодействовать с ботом, однако он по-прежнему будет обнаруживаемым, и пользователи по-прежнему смогут добавлять его в Teams.</span><span class="sxs-lookup"><span data-stu-id="7569a-161">This prevents users from interacting with the bot, however, it will still be discoverable and users will still be able to add it to Teams.</span></span>

## <a name="delete-a-bot-from-teams"></a><span data-ttu-id="7569a-162">Удаление бота из Teams</span><span class="sxs-lookup"><span data-stu-id="7569a-162">Delete a bot from Teams</span></span>

<span data-ttu-id="7569a-163">Чтобы полностью удалить бот из Teams,  перейдите к панели мониторинга ботов и отредактировать Microsoft Teams канал.</span><span class="sxs-lookup"><span data-stu-id="7569a-163">To remove your bot completely from Teams, go to your **Bot Dashboard** and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="7569a-164">Выберите **кнопку Удалить** в нижней части.</span><span class="sxs-lookup"><span data-stu-id="7569a-164">Choose the **Delete** button at the bottom.</span></span> <span data-ttu-id="7569a-165">Это не позволяет пользователям открывать, добавлять и взаимодействовать с вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="7569a-165">This prevents users from discovering, adding, and interacting with your bot.</span></span> <span data-ttu-id="7569a-166">Это не удаляет бота из других экземпляров Teams, однако он перестает функционировать и для них.</span><span class="sxs-lookup"><span data-stu-id="7569a-166">This does not remove the bot from other user's Teams instances, however, it stops functioning for them as well.</span></span>

## <a name="see-also"></a><span data-ttu-id="7569a-167">См. также</span><span class="sxs-lookup"><span data-stu-id="7569a-167">See also</span></span>

* [<span data-ttu-id="7569a-168">Отладка бота с помощью ПО промежуточного слоя для проверки</span><span class="sxs-lookup"><span data-stu-id="7569a-168">Debug your bot with inspection middleware</span></span>](/azure/bot-service/bot-service-debug-inspection-middleware)
* [<span data-ttu-id="7569a-169">Локальная отладка бота для звонков и собраний</span><span class="sxs-lookup"><span data-stu-id="7569a-169">Debug your calling and meeting bot locally</span></span>](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
