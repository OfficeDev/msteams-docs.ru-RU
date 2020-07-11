---
title: Отправка настраиваемого приложения в Microsoft Teams
description: Сведения о том, как отправить приложение в Microsoft Teams
keywords: Отправка приложений Teams
ms.openlocfilehash: c130ef48d3ad7476de9ca5afeb7b613197c43f18
ms.sourcegitcommit: 3ba5a5a7d9d9d906abc3ee1df9c2177de0cfd767
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2020
ms.locfileid: "45103028"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="69cae-104">Отправка пакета приложения в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="69cae-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="69cae-105">Чтобы протестировать работу приложений в Microsoft Teams, необходимо отправить приложение в Teams.</span><span class="sxs-lookup"><span data-stu-id="69cae-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="69cae-106">При отправке приложение добавляется в выбранную вами команду, а члены вашей группы могут взаимодействовать с ней, как конечные пользователи.</span><span class="sxs-lookup"><span data-stu-id="69cae-106">Uploading adds the app to the team you select, and you and your team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="69cae-107">При отправке обновленного пакета для существующего приложения с помощью ленты может не отображаться изменение вкладки при просмотре в окне беседы.</span><span class="sxs-lookup"><span data-stu-id="69cae-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the Conversations window.</span></span> <span data-ttu-id="69cae-108">Лучше получить доступ к нему через приложение или тестировать его в чистой тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="69cae-108">It's better to access it via the Apps fly-out, or test on a clean test environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="69cae-109">Создание пакета отправки</span><span class="sxs-lookup"><span data-stu-id="69cae-109">Create your upload package</span></span>

<span data-ttu-id="69cae-110">Для разработки, а также AppSource (прежнее название — магазин Office) необходимо создать пакет с перегрузкой, содержащий сведения для описания взаимодействия с пользователем.</span><span class="sxs-lookup"><span data-stu-id="69cae-110">For development as well as AppSource (formerly Office Store) submission you must create an uploadable package that contains the information to describe your experience.</span></span> <span data-ttu-id="69cae-111">Пакет, ZIP-файл содержит манифест приложения и значки, которые уникально определяют ваш интерфейс.</span><span class="sxs-lookup"><span data-stu-id="69cae-111">The package, a .zip file, contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="69cae-112">Чтобы создать пакет отправки, ознакомьтесь со статьей [Создание пакета для приложения Microsoft Teams](../build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="69cae-112">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="69cae-113">После создания пакета его можно отправить в команду.</span><span class="sxs-lookup"><span data-stu-id="69cae-113">With your package created, you can now upload it into a team.</span></span> <span data-ttu-id="69cae-114">После отправки он будет доступен всем пользователям выбранной команды и только пользователям этой команды.</span><span class="sxs-lookup"><span data-stu-id="69cae-114">Once uploaded it will be available for all users in the selected team, and only the users of that team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="69cae-115">Загрузка пакета в Teams</span><span class="sxs-lookup"><span data-stu-id="69cae-115">Load your package into Teams</span></span>

<span data-ttu-id="69cae-116">Вы можете протестировать пакет, отправив его в Teams.</span><span class="sxs-lookup"><span data-stu-id="69cae-116">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="69cae-117">Для отправки в работу администратор клиента должен сначала [Разрешить отправку приложений](/microsoftteams/admin-settings).</span><span class="sxs-lookup"><span data-stu-id="69cae-117">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="69cae-118">Существует два способа отправки приложения в teams:</span><span class="sxs-lookup"><span data-stu-id="69cae-118">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="69cae-119">Использование хранилища</span><span class="sxs-lookup"><span data-stu-id="69cae-119">Using the Store</span></span>
* <span data-ttu-id="69cae-120">Использование вкладки "приложения"</span><span class="sxs-lookup"><span data-stu-id="69cae-120">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="69cae-121">Отправка пакета в группу или беседу с помощью магазина</span><span class="sxs-lookup"><span data-stu-id="69cae-121">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="69cae-122">В левом нижнем углу Teams выберите значок магазин.</span><span class="sxs-lookup"><span data-stu-id="69cae-122">In the lower left corner of Teams, choose the Store icon.</span></span> <span data-ttu-id="69cae-123">На странице Store выберите "Отправить настраиваемое приложение".</span><span class="sxs-lookup"><span data-stu-id="69cae-123">On the Store page, choose "Upload a custom app".</span></span>

   ![Просмотр команды](../../assets/images/store-upload-a-custom-app.png)

2. <span data-ttu-id="69cae-125">В диалоговом окне *Открыть* перейдите к пакету, который требуется отправить, и нажмите кнопку *Открыть*.</span><span class="sxs-lookup"><span data-stu-id="69cae-125">In the *Open* dialog, navigate to the package you want to upload and choose *Open*.</span></span>

<span data-ttu-id="69cae-126">Переданный пакет теперь должен быть доступен для использования в команде или беседе, указанной в диалоговом окне согласия.</span><span class="sxs-lookup"><span data-stu-id="69cae-126">The uploaded package should now be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="69cae-127">Если ваше приложение не отображается, наиболее распространенной причиной является ошибка в манифесте, особенно идентификаторы для расширений приложения, Bot и сообщений.</span><span class="sxs-lookup"><span data-stu-id="69cae-127">If your app does not appear, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span> <span data-ttu-id="69cae-128">Если приложение не ограничено для бесед, этот параметр не будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="69cae-128">If the app is not scoped for conversations, that option will not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="69cae-129">Приложения в беседах в настоящее время находятся в [предварительной версии Developer](../../resources/dev-preview/developer-preview-intro.md), и этот параметр не отображается, если Teams не работает в этом режиме.</span><span class="sxs-lookup"><span data-stu-id="69cae-129">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option will not appear if Teams is not running in that mode.</span></span>

![Пример кода робота в списке отправленных Боты](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="69cae-131">Отправка пакета в команду с помощью вкладки "приложения"</span><span class="sxs-lookup"><span data-stu-id="69cae-131">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="69cae-132">В Целевой группе выберите *Дополнительные параметры* (**&#8943;**) и выберите пункт *Управление командой*.</span><span class="sxs-lookup"><span data-stu-id="69cae-132">In the target team, choose *More options* (**&#8943;**) and choose *Manage team*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="69cae-133">Вы должны быть владельцем группы, или владелец должен разрешить пользователям добавлять соответствующие типы приложений для отображения этой функции.</span><span class="sxs-lookup"><span data-stu-id="69cae-133">You must be the team owner, or the owner must allow users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="69cae-134">Перейдите на вкладку приложения, а затем выберите *Отправить настраиваемое приложение* в правом нижнем углу.</span><span class="sxs-lookup"><span data-stu-id="69cae-134">Select the Apps tab, and then choose *Upload a custom app* on the lower right.</span></span>

   ![Отправка точки входа](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="69cae-136">Найдите и выберите ZIP-пакет на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="69cae-136">Browse to and select your .zip package from your computer.</span></span>

4. <span data-ttu-id="69cae-137">После короткой паузы вы увидите ваше отправленное приложение в списке.</span><span class="sxs-lookup"><span data-stu-id="69cae-137">After a brief pause you will see your uploaded app in the list.</span></span>

   ![Пример кода робота в списке отправленных Боты](../../assets/images/botinlist.jpg)

<span data-ttu-id="69cae-139">Если ваше приложение не загружается, наиболее распространенной причиной является ошибка в манифесте, особенно идентификаторы для расширений приложения, Bot и сообщений.</span><span class="sxs-lookup"><span data-stu-id="69cae-139">If your app does not load, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span>

## <a name="accessing-your-uploaded-configurable-tab"></a><span data-ttu-id="69cae-140">Доступ к отправленной настраиваемой вкладке</span><span class="sxs-lookup"><span data-stu-id="69cae-140">Accessing your uploaded configurable tab</span></span>

<span data-ttu-id="69cae-141">Если приложение содержит вкладки, пользователи могут закреплять их во всех беседах или каналах команд с помощью стандартного процесса коллекции вкладок.</span><span class="sxs-lookup"><span data-stu-id="69cae-141">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="69cae-142">Перейдите к каналу в группе.</span><span class="sxs-lookup"><span data-stu-id="69cae-142">Go to a channel in the team.</span></span> <span data-ttu-id="69cae-143">Выберите *+* (*Добавить вкладку*) справа от существующих вкладок.</span><span class="sxs-lookup"><span data-stu-id="69cae-143">Choose *+* (*Add a tab*) to the right of the existing tabs.</span></span>

2. <span data-ttu-id="69cae-144">Выберите вкладку в появившейся коллекции.</span><span class="sxs-lookup"><span data-stu-id="69cae-144">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="69cae-145">Примите запрос согласия.</span><span class="sxs-lookup"><span data-stu-id="69cae-145">Accept the consent prompt.</span></span>

4. <span data-ttu-id="69cae-146">Настройте вкладку с помощью [страницы ее конфигурации](../../tabs/how-to/create-tab-pages/configuration-page.md) и нажмите кнопку *сохранить*.</span><span class="sxs-lookup"><span data-stu-id="69cae-146">Configure your tab via its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and choose *Save*.</span></span>

  ![Диалоговое окно "Добавление вкладки" с коллекцией доступных вкладок](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a><span data-ttu-id="69cae-148">Доступ к переданному почтовому роботу</span><span class="sxs-lookup"><span data-stu-id="69cae-148">Accessing your uploaded bot</span></span>

<span data-ttu-id="69cae-149">Когда вы добавляете робота в группу, он должен работать с другими участниками группы, в зависимости от определения области действия Bot.</span><span class="sxs-lookup"><span data-stu-id="69cae-149">When you add a bot to a team, it should be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="69cae-150">Вы и другие участники группы увидят запись в общем канале, указывающую на то, что Bot добавлен в команду.</span><span class="sxs-lookup"><span data-stu-id="69cae-150">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="69cae-151">Для ленты с включенной поддержкой Teams можно начать с запуска ленты, @mentioning имя ленты, которая должна быть автозаполнена.</span><span class="sxs-lookup"><span data-stu-id="69cae-151">For a teams-enabled bot, you can start by invoking your bot by @mentioning the name of the bot, which should autocomplete.</span></span>

<span data-ttu-id="69cae-152">Чтобы протестировать прямые беседы с помощью ленты, вы можете получить доступ к нему через домашнюю страницу приложения, @mention его в канале или выполнить поиск в **новом окне чата** .</span><span class="sxs-lookup"><span data-stu-id="69cae-152">To test direct chats with your bot, you can either access it via the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="69cae-153">Когда вы добавляете робота в беседу, чтобы протестировать прямые сеансы связи с роботом, вы можете @mention его в беседе или найти в **новом окне чата** .</span><span class="sxs-lookup"><span data-stu-id="69cae-153">When you add your bot to a conversation To test direct chats with your bot, you can @mention it in a conversation, or search for it in the **New Chat** window.</span></span>

## <a name="accessing-your-uploaded-connector"></a><span data-ttu-id="69cae-154">Доступ к переданному соединителю</span><span class="sxs-lookup"><span data-stu-id="69cae-154">Accessing your uploaded Connector</span></span>

<span data-ttu-id="69cae-155">Когда приложение загружено в группе или беседе, пользователи могут настроить соединитель с помощью процесса коллекции стандартных соединителей:</span><span class="sxs-lookup"><span data-stu-id="69cae-155">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="69cae-156">Перейдите к каналу в группе.</span><span class="sxs-lookup"><span data-stu-id="69cae-156">Go to a channel in the team.</span></span> <span data-ttu-id="69cae-157">Нажмите кнопку *Дополнительные параметры* (*&#8943;*) и выберите пункт *соединители*.</span><span class="sxs-lookup"><span data-stu-id="69cae-157">Choose *More options* (*&#8943;*) and choose *Connectors*.</span></span>

2. <span data-ttu-id="69cae-158">Выберите свой соединитель из раздела **Неопубликованные** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="69cae-158">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="69cae-159">Настройте соединитель с помощью [страницы конфигурации](../../webhooks-and-connectors/how-to/connectors-creating.md) и нажмите кнопку *сохранить*.</span><span class="sxs-lookup"><span data-stu-id="69cae-159">Configure your Connector via its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and choose *Save*.</span></span>

  ![Диалоговое окно "Добавление вкладки" с коллекцией доступных вкладок.](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a><span data-ttu-id="69cae-161">Доступ к переданному расширению обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="69cae-161">Accessing your uploaded messaging extension</span></span>

<span data-ttu-id="69cae-162">Загруженное приложение с расширением обмена сообщениями автоматически отображается в меню *дополнительных параметров* (*&#8943;*) в поле "создание".</span><span class="sxs-lookup"><span data-stu-id="69cae-162">An uploaded app with a messaging extension automatically appears in the *More options* (*&#8943;*) menu in the compose box.</span></span>

![расширения для обмена сообщениями;](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a><span data-ttu-id="69cae-164">Удаление или обновление приложения</span><span class="sxs-lookup"><span data-stu-id="69cae-164">Removing or updating your app</span></span>

<span data-ttu-id="69cae-165">Если вы хотите удалить приложение, выберите значок Корзина — может находиться рядом с именем приложения в списке вид Teams Боты.</span><span class="sxs-lookup"><span data-stu-id="69cae-165">If you want to remove your app, select the trash-can icon next to the app name in the View Teams bots list.</span></span>

<span data-ttu-id="69cae-166">При изменении сведений манифеста необходимо сначала удалить приложение, а затем добавить обновленный пакет (на [загрузку пакета в группу](#load-your-package-into-teams)).</span><span class="sxs-lookup"><span data-stu-id="69cae-166">If you change manifest information, you must first remove the app and then add the updated package (per [Load your package into a team](#load-your-package-into-teams)).</span></span> <span data-ttu-id="69cae-167">Обратите внимание, что в общем случае изменения кода для службы не требуют повторной отправки манифеста, если эти изменения не требуют обновления манифеста (например, изменения URL-адреса или идентификатора приложения Microsoft для ленты).</span><span class="sxs-lookup"><span data-stu-id="69cae-167">Note that, in general, code changes on your service do not require you to re-upload your manifest, unless those changes require manifest updates (such as changes to the URL or the Microsoft app ID for its bot).</span></span>

> [!NOTE]
> <span data-ttu-id="69cae-168">Невозможно полностью удалить Bot из личного контекста.</span><span class="sxs-lookup"><span data-stu-id="69cae-168">There is no way to completely remove a bot from personal context.</span></span> <span data-ttu-id="69cae-169">При удалении и повторном добавлении канала ленты к предыдущей беседе добавляется дополнительное соединение с Bot.</span><span class="sxs-lookup"><span data-stu-id="69cae-169">If the bot is removed and re-added, additional communication with the bot will append to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="69cae-170">Рекомендации по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="69cae-170">Troubleshooting notes</span></span>

* <span data-ttu-id="69cae-171">Если манифест не загружается, дважды убедитесь, что вы выполнили все инструкции, приведенные в разделе [Create a Package](../../concepts/build-and-test/apps-package.md) и проверили манифест в соответствии со [схемой](../../resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="69cae-171">If the manifest doesn't load, please double-check that you followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>

