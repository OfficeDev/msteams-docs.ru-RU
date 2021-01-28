---
title: Отправка пользовательского приложения
description: Описание отправки приложения в Microsoft Teams
ms.topic: how-to
keywords: Отправка приложений teams
ms.openlocfilehash: 2e7a21dc27fdfe824ecacebabbb61a3b99ae8e79
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014343"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="065ac-104">Отправка пакета приложения в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="065ac-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="065ac-105">Чтобы протестировать свое приложение в Microsoft Teams, необходимо отправить приложение в Teams.</span><span class="sxs-lookup"><span data-stu-id="065ac-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="065ac-106">Отправка добавляет приложение в выбранную команду, и вы и участники вашей команды можете взаимодействовать с ним, как и с конечными пользователями.</span><span class="sxs-lookup"><span data-stu-id="065ac-106">Uploading adds the app to the team you select, and you and your team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="065ac-107">Отправка обновленного пакета для существующего приложения с помощью бота может не показывать изменения вкладки при просмотре в окне "Беседы".</span><span class="sxs-lookup"><span data-stu-id="065ac-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the Conversations window.</span></span> <span data-ttu-id="065ac-108">Доступ к нему лучше получить с помощью fly-out приложения или тестирования в чистой тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="065ac-108">It's better to access it via the Apps fly-out, or test on a clean test environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="065ac-109">Создание пакета отправки</span><span class="sxs-lookup"><span data-stu-id="065ac-109">Create your upload package</span></span>

<span data-ttu-id="065ac-110">Для разработки, а также отправки в AppSource (прежнее значение — Магазин Office) необходимо создать загружаемый пакет, содержащий сведения для описания вашего опыта.</span><span class="sxs-lookup"><span data-stu-id="065ac-110">For development as well as AppSource (formerly Office Store) submission you must create an uploadable package that contains the information to describe your experience.</span></span> <span data-ttu-id="065ac-111">Пакет , ZIP-файл, содержит манифест приложения и значки, которые однозначно определяют ваш опыт.</span><span class="sxs-lookup"><span data-stu-id="065ac-111">The package, a .zip file, contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="065ac-112">Чтобы создать пакет отправки, см. [статью "Создание пакета для приложения Microsoft Teams".](../build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="065ac-112">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="065ac-113">После создания пакета вы можете отправить его в команду.</span><span class="sxs-lookup"><span data-stu-id="065ac-113">With your package created, you can now upload it into a team.</span></span> <span data-ttu-id="065ac-114">После отправки он будет доступен для всех пользователей в выбранной команде и только для пользователей этой команды.</span><span class="sxs-lookup"><span data-stu-id="065ac-114">Once uploaded it will be available for all users in the selected team, and only the users of that team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="065ac-115">Загрузка пакета в Teams</span><span class="sxs-lookup"><span data-stu-id="065ac-115">Load your package into Teams</span></span>

<span data-ttu-id="065ac-116">Вы можете протестировать пакет, загрузив его в Teams.</span><span class="sxs-lookup"><span data-stu-id="065ac-116">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="065ac-117">Для отправки на работу администратор клиента должен сначала включить [отправку приложений.](/microsoftteams/admin-settings)</span><span class="sxs-lookup"><span data-stu-id="065ac-117">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="065ac-118">Существует два способа отправки приложения в Teams:</span><span class="sxs-lookup"><span data-stu-id="065ac-118">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="065ac-119">Использование Магазина</span><span class="sxs-lookup"><span data-stu-id="065ac-119">Using the Store</span></span>
* <span data-ttu-id="065ac-120">Использование вкладки "Приложения"</span><span class="sxs-lookup"><span data-stu-id="065ac-120">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="065ac-121">Отправка пакета в команду или беседу с помощью Магазина</span><span class="sxs-lookup"><span data-stu-id="065ac-121">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="065ac-122">В левом нижнем углу Teams выберите значок Магазина.</span><span class="sxs-lookup"><span data-stu-id="065ac-122">In the lower left corner of Teams, choose the Store icon.</span></span> <span data-ttu-id="065ac-123">На странице Магазина выберите "Отправить пользовательское приложение".</span><span class="sxs-lookup"><span data-stu-id="065ac-123">On the Store page, choose "Upload a custom app".</span></span>

  ![Просмотр команды](../../assets/images/store-upload-a-custom-app2.png)

2. <span data-ttu-id="065ac-125">В *диалоговом* окте "Открыть" перейдите к пакету, который нужно отправить, и выберите *"Открыть".*</span><span class="sxs-lookup"><span data-stu-id="065ac-125">In the *Open* dialog, navigate to the package you want to upload and choose *Open*.</span></span>

   ![Добавление меню](../../assets/images/NewappAddmenudropdown.png)

<span data-ttu-id="065ac-127">Теперь загруженный пакет должен быть доступен для использования в команде или беседе, указанной в диалоговом оке согласия.</span><span class="sxs-lookup"><span data-stu-id="065ac-127">The uploaded package should now be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="065ac-128">Если ваше приложение не появляется, наиболее распространенной причиной является ошибка в манифесте, особенно это ид для приложений, ботов и расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="065ac-128">If your app does not appear, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span> <span data-ttu-id="065ac-129">Если область приложения не является областью для бесед, этот параметр не будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="065ac-129">If the app is not scoped for conversations, that option will not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="065ac-130">Приложения в беседах в настоящее [время Developer Preview,](../../resources/dev-preview/developer-preview-intro.md)и этот параметр не будет отображаться, если Teams не работает в этом режиме.</span><span class="sxs-lookup"><span data-stu-id="065ac-130">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option will not appear if Teams is not running in that mode.</span></span>

![Пример бота в списке загруженных ботов](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="065ac-132">Отправка пакета в команду с помощью вкладки "Приложения"</span><span class="sxs-lookup"><span data-stu-id="065ac-132">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="065ac-133">В целевой команде выберите *"Дополнительные параметры"* **(&#8943;)** и *"Управление командой".*</span><span class="sxs-lookup"><span data-stu-id="065ac-133">In the target team, choose *More options* (**&#8943;**) and choose *Manage team*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="065ac-134">Вы должны быть владельцем команды или разрешить пользователям добавлять соответствующие типы приложений для появления этой функции.</span><span class="sxs-lookup"><span data-stu-id="065ac-134">You must be the team owner, or the owner must allow users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="065ac-135">Выберите вкладку "Приложения" и выберите *"Отправить пользовательское приложение"* в правом нижнем правом конце.</span><span class="sxs-lookup"><span data-stu-id="065ac-135">Select the Apps tab, and then choose *Upload a custom app* on the lower right.</span></span>

   ![Точка входа при отправке](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="065ac-137">Найдите и выберите ZIP-пакет на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="065ac-137">Browse to and select your .zip package from your computer.</span></span>

4. <span data-ttu-id="065ac-138">После короткой паузы вы увидите в списке загруженные приложения.</span><span class="sxs-lookup"><span data-stu-id="065ac-138">After a brief pause you will see your uploaded app in the list.</span></span>

   ![Пример бота в списке загруженных ботов](../../assets/images/botinlist.jpg)

<span data-ttu-id="065ac-140">Если ваше приложение не загружается, наиболее распространенной причиной является ошибка в манифесте, в частности, ид для приложений, ботов и расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="065ac-140">If your app does not load, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span>

## <a name="accessing-your-uploaded-configurable-tab"></a><span data-ttu-id="065ac-141">Доступ к загруженной настраиваемой вкладке</span><span class="sxs-lookup"><span data-stu-id="065ac-141">Accessing your uploaded configurable tab</span></span>

<span data-ttu-id="065ac-142">Если приложение содержит вкладки, пользователи могут закрепить их в любом канале беседы или команды с помощью стандартного потока коллекции вкладок:</span><span class="sxs-lookup"><span data-stu-id="065ac-142">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="065ac-143">Перейдите на канал в команде.</span><span class="sxs-lookup"><span data-stu-id="065ac-143">Go to a channel in the team.</span></span> <span data-ttu-id="065ac-144">Choose *+* ( Add a *tab*) to the right of the existing tabs.</span><span class="sxs-lookup"><span data-stu-id="065ac-144">Choose *+* (*Add a tab*) to the right of the existing tabs.</span></span>

2. <span data-ttu-id="065ac-145">Выберите вкладку в галерее.</span><span class="sxs-lookup"><span data-stu-id="065ac-145">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="065ac-146">Примите приглашение на согласие.</span><span class="sxs-lookup"><span data-stu-id="065ac-146">Accept the consent prompt.</span></span>

4. <span data-ttu-id="065ac-147">Настройте вкладку на странице [конфигурации](../../tabs/how-to/create-tab-pages/configuration-page.md) и выберите *"Сохранить".*</span><span class="sxs-lookup"><span data-stu-id="065ac-147">Configure your tab via its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and choose *Save*.</span></span>

  ![Диалоговое окно "Добавление вкладки" с галереей доступных вкладок](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a><span data-ttu-id="065ac-149">Доступ к загруженным ботам</span><span class="sxs-lookup"><span data-stu-id="065ac-149">Accessing your uploaded bot</span></span>

<span data-ttu-id="065ac-150">При добавлении бота в команду его должен использовать любой человек из этой команды, в каналах команды и за ее пределами, в зависимости от определения области бота.</span><span class="sxs-lookup"><span data-stu-id="065ac-150">When you add a bot to a team, it should be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="065ac-151">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span><span class="sxs-lookup"><span data-stu-id="065ac-151">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="065ac-152">Для бота с поддержкой команд вы можете сначала @mentioning имя бота, который должен автозаполнеть.</span><span class="sxs-lookup"><span data-stu-id="065ac-152">For a teams-enabled bot, you can start by invoking your bot by @mentioning the name of the bot, which should autocomplete.</span></span>

<span data-ttu-id="065ac-153">Чтобы протестировать прямые чаты с ботом, вы можете получить к нему доступ через домашний сайт приложения, @mention его в канале или найти в окне **"Новый чат".**</span><span class="sxs-lookup"><span data-stu-id="065ac-153">To test direct chats with your bot, you can either access it via the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="065ac-154">При добавлении бота в беседу для тестирования прямых чатов с ботом вы можете @mention его в беседе или найти в окне **"Новый чат".**</span><span class="sxs-lookup"><span data-stu-id="065ac-154">When you add your bot to a conversation To test direct chats with your bot, you can @mention it in a conversation, or search for it in the **New Chat** window.</span></span>

## <a name="accessing-your-uploaded-connector"></a><span data-ttu-id="065ac-155">Доступ к загруженным соединителам</span><span class="sxs-lookup"><span data-stu-id="065ac-155">Accessing your uploaded Connector</span></span>

<span data-ttu-id="065ac-156">После загрузки приложения в команде или беседе пользователи могут настроить соединители с помощью стандартного потока коллекции соединитеев:</span><span class="sxs-lookup"><span data-stu-id="065ac-156">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="065ac-157">Перейдите на канал в команде.</span><span class="sxs-lookup"><span data-stu-id="065ac-157">Go to a channel in the team.</span></span> <span data-ttu-id="065ac-158">Выберите *дополнительные параметры* *(&#8943;)* и выберите *соединители.*</span><span class="sxs-lookup"><span data-stu-id="065ac-158">Choose *More options* (*&#8943;*) and choose *Connectors*.</span></span>

2. <span data-ttu-id="065ac-159">Выберите соединители в разделе **"Неогруженные"** внизу.</span><span class="sxs-lookup"><span data-stu-id="065ac-159">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="065ac-160">Настройте соединитель на странице [конфигурации и](../../webhooks-and-connectors/how-to/connectors-creating.md) выберите *"Сохранить".*</span><span class="sxs-lookup"><span data-stu-id="065ac-160">Configure your Connector via its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and choose *Save*.</span></span>

  ![Диалоговое окно "Добавление вкладки" с галереей доступных вкладок.](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a><span data-ttu-id="065ac-162">Доступ к добавленным расширениям обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="065ac-162">Accessing your uploaded messaging extension</span></span>

<span data-ttu-id="065ac-163">Загруженное приложение с расширением обмена сообщениями  автоматически отображается в меню "Дополнительные параметры"*(&#8943;)* в поле "Составление".</span><span class="sxs-lookup"><span data-stu-id="065ac-163">An uploaded app with a messaging extension automatically appears in the *More options* (*&#8943;*) menu in the compose box.</span></span>

![Расширения для система обмена сообщениями](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a><span data-ttu-id="065ac-165">Удаление или обновление приложения</span><span class="sxs-lookup"><span data-stu-id="065ac-165">Removing or updating your app</span></span>

<span data-ttu-id="065ac-166">Если вы хотите удалить приложение, выберите значок корзины рядом с именем приложения в списке ботов "Просмотр Teams".</span><span class="sxs-lookup"><span data-stu-id="065ac-166">If you want to remove your app, select the trash-can icon next to the app name in the View Teams bots list.</span></span>

<span data-ttu-id="065ac-167">При изменении сведений о манифесте необходимо сначала удалить приложение, а затем добавить обновленный пакет (для каждого пакета в [команду).](#load-your-package-into-teams)</span><span class="sxs-lookup"><span data-stu-id="065ac-167">If you change manifest information, you must first remove the app and then add the updated package (per [Load your package into a team](#load-your-package-into-teams)).</span></span> <span data-ttu-id="065ac-168">Обратите внимание, что в целом изменения кода в службе не требуют повторной отправки манифеста, если только эти изменения не требуют обновления манифеста (например, изменения URL-адреса или кода приложения Майкрософт для бота).</span><span class="sxs-lookup"><span data-stu-id="065ac-168">Note that, in general, code changes on your service do not require you to re-upload your manifest, unless those changes require manifest updates (such as changes to the URL or the Microsoft app ID for its bot).</span></span>

> [!NOTE]
> <span data-ttu-id="065ac-169">Полностью удалить бота из личного контекста не существует.</span><span class="sxs-lookup"><span data-stu-id="065ac-169">There is no way to completely remove a bot from personal context.</span></span> <span data-ttu-id="065ac-170">Если бот будет удален и добавлен повторно, к предыдущей беседе будет добавлено дополнительное взаимодействие с ботом.</span><span class="sxs-lookup"><span data-stu-id="065ac-170">If the bot is removed and re-added, additional communication with the bot will append to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="065ac-171">Заметки по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="065ac-171">Troubleshooting notes</span></span>

* <span data-ttu-id="065ac-172">Если манифест не загружается, убедитесь, что вы следовали [](../../concepts/build-and-test/apps-package.md) всем инструкциям в окну "Создание пакета" и проверили манифест на [схеме.](../../resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="065ac-172">If the manifest doesn't load, please double-check that you followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>
