---
title: Отправка настраиваемой приложения
description: Описывает, как загрузить приложение в Microsoft Teams
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
keywords: отправка командных приложений
ms.openlocfilehash: 3fa6a3ef00cbb55b5c663891deaabcc908de95d5
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020809"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="08ee6-104">Отправка пакета приложения в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="08ee6-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="08ee6-105">Чтобы протестировать свое приложение в Microsoft Teams, необходимо загрузить приложение в Teams.</span><span class="sxs-lookup"><span data-stu-id="08ee6-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="08ee6-106">Загрузка добавляет приложение в выбранную команду, и все члены группы могут взаимодействовать с ним, как и конечные пользователи.</span><span class="sxs-lookup"><span data-stu-id="08ee6-106">Uploading adds the app to the selected team and all the team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="08ee6-107">Загрузка обновленного пакета для существующего приложения с помощью бота может не показывать изменения вкладки при просмотре в окне бесед.</span><span class="sxs-lookup"><span data-stu-id="08ee6-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the conversations window.</span></span> <span data-ttu-id="08ee6-108">Вы можете получить доступ к приложению с помощью вылетов приложений или тестирования в чистой среде.</span><span class="sxs-lookup"><span data-stu-id="08ee6-108">You can access the app through the apps fly-out or test in a clean environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="08ee6-109">Создание пакета отправки</span><span class="sxs-lookup"><span data-stu-id="08ee6-109">Create your upload package</span></span>

<span data-ttu-id="08ee6-110">Для разработки и отправки AppSource необходимо создать пакет, который можно загрузить.</span><span class="sxs-lookup"><span data-stu-id="08ee6-110">For development and AppSource submission, you must create a package that you can upload.</span></span> <span data-ttu-id="08ee6-111">Пакет должен содержать сведения для описания вашего опыта.</span><span class="sxs-lookup"><span data-stu-id="08ee6-111">The package must contain the information to describe your experience.</span></span> <span data-ttu-id="08ee6-112">Пакет — это файл .zip, содержащий манифест приложения и значки, которые однозначно определяют ваш опыт.</span><span class="sxs-lookup"><span data-stu-id="08ee6-112">The package is a .zip file that contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="08ee6-113">Чтобы создать пакет отправки, [см. в приложении Create the package for your Microsoft Teams.](../build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="08ee6-113">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="08ee6-114">После создания пакета загрузите его в команду.</span><span class="sxs-lookup"><span data-stu-id="08ee6-114">After you create the package, upload it into a team.</span></span> <span data-ttu-id="08ee6-115">Загруженный пакет доступен только пользователям выбранной группы.</span><span class="sxs-lookup"><span data-stu-id="08ee6-115">The uploaded package is only available to the users of the selected team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="08ee6-116">Загрузка пакета в Teams</span><span class="sxs-lookup"><span data-stu-id="08ee6-116">Load your package into Teams</span></span>

<span data-ttu-id="08ee6-117">Вы можете протестировать пакет, загрузив его в Teams.</span><span class="sxs-lookup"><span data-stu-id="08ee6-117">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="08ee6-118">Для загрузки на работу администратор клиента должен сначала включить [загрузку приложений.](/microsoftteams/admin-settings)</span><span class="sxs-lookup"><span data-stu-id="08ee6-118">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="08ee6-119">Существует два способа отправки приложения в Teams:</span><span class="sxs-lookup"><span data-stu-id="08ee6-119">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="08ee6-120">Использование магазина</span><span class="sxs-lookup"><span data-stu-id="08ee6-120">Using the Store</span></span>
* <span data-ttu-id="08ee6-121">Использование вкладки Apps</span><span class="sxs-lookup"><span data-stu-id="08ee6-121">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="08ee6-122">Отправка пакета в команду или беседу с помощью Магазина</span><span class="sxs-lookup"><span data-stu-id="08ee6-122">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="08ee6-123">В левом нижнем углу Команд выберите значок **Store.**</span><span class="sxs-lookup"><span data-stu-id="08ee6-123">In the lower left corner of Teams, choose the **Store** icon.</span></span> <span data-ttu-id="08ee6-124">На странице Магазин выберите **Загрузите настраиваемую приложение.**</span><span class="sxs-lookup"><span data-stu-id="08ee6-124">On the Store page, choose **Upload a custom app**.</span></span>

  ![Просмотр группы](../../assets/images/store-upload-a-custom-app2.png)

2. <span data-ttu-id="08ee6-126">В **диалоговом** окте Open перейдите к пакету, который необходимо загрузить, и выберите Open.</span><span class="sxs-lookup"><span data-stu-id="08ee6-126">In the **Open** dialog, navigate to the package you want to upload and choose Open.</span></span>

   ![Добавление меню](../../assets/images/NewappAddmenudropdown.png)

<span data-ttu-id="08ee6-128">Загруженный пакет должен быть доступен для использования в группе или беседе, указанной в диалоговом окте согласия.</span><span class="sxs-lookup"><span data-stu-id="08ee6-128">The uploaded package must be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="08ee6-129">Если приложение не появится, наиболее распространенной причиной является ошибка в манифесте, в частности, ID для расширений приложений, ботов и сообщений.</span><span class="sxs-lookup"><span data-stu-id="08ee6-129">If your app does not appear, the most common reason is an error in the manifest, particularly IDs for the app, bot, and messaging extensions.</span></span> <span data-ttu-id="08ee6-130">Если приложение не является областью для бесед, этот параметр не появится.</span><span class="sxs-lookup"><span data-stu-id="08ee6-130">If the app is not scoped for conversations that option does not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="08ee6-131">Приложения в беседах в настоящее время [находятся в Developer Preview,](../../resources/dev-preview/developer-preview-intro.md)и этот параметр не появляется, если Teams не работает в этом режиме.</span><span class="sxs-lookup"><span data-stu-id="08ee6-131">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option does not appear if Teams is not running in that mode.</span></span>

![Пример бота в списке загруженных ботов](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="08ee6-133">Отправка пакета в команду с помощью вкладки Apps</span><span class="sxs-lookup"><span data-stu-id="08ee6-133">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="08ee6-134">В целевой группе выберите **дополнительные** параметры **(&#8943;)** и управляйте **командой**.</span><span class="sxs-lookup"><span data-stu-id="08ee6-134">In the target team, choose **More options** (**&#8943;**) and select **Manage team**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="08ee6-135">Вы должны быть владельцем группы или владелец должен предоставить доступ пользователям, чтобы добавить соответствующие типы приложений для появления этой функции.</span><span class="sxs-lookup"><span data-stu-id="08ee6-135">You must be the team owner or the owner must give access to users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="08ee6-136">Выберите **вкладку Apps** и **загрузите пользовательское приложение** в правом нижнем справа.</span><span class="sxs-lookup"><span data-stu-id="08ee6-136">Select the **Apps** tab and choose **Upload a custom app** on the lower right.</span></span>

   ![Загрузка точки входа](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="08ee6-138">Выберите пакет .zip с компьютера.</span><span class="sxs-lookup"><span data-stu-id="08ee6-138">Select your .zip package from the computer.</span></span>

4. <span data-ttu-id="08ee6-139">Вы можете увидеть загруженные приложения в списке.</span><span class="sxs-lookup"><span data-stu-id="08ee6-139">You can see your uploaded app in the list.</span></span>

   ![Пример бота в списке загруженных ботов](../../assets/images/botinlist.jpg)

<span data-ttu-id="08ee6-141">Если приложение не загружается, наиболее распространенной причиной является ошибка в манифесте, особенно ID для расширений приложений, ботов и сообщений.</span><span class="sxs-lookup"><span data-stu-id="08ee6-141">If your app does not load, the most common reason is an error in the manifest, particularly IDs for the app, bot, and messaging extensions.</span></span>

## <a name="access-your-uploaded-configurable-tab"></a><span data-ttu-id="08ee6-142">Доступ к загруженной настраиваемой вкладке</span><span class="sxs-lookup"><span data-stu-id="08ee6-142">Access your uploaded configurable tab</span></span>

<span data-ttu-id="08ee6-143">Если приложение содержит вкладки, пользователи могут прикрепить их к любому каналу беседы или группы с помощью стандартного потока галереи вкладок:</span><span class="sxs-lookup"><span data-stu-id="08ee6-143">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="08ee6-144">Перейдите на канал в команде.</span><span class="sxs-lookup"><span data-stu-id="08ee6-144">Go to a channel in the team.</span></span> <span data-ttu-id="08ee6-145">Выберите, **+** чтобы добавить вкладку справа от существующих вкладок.</span><span class="sxs-lookup"><span data-stu-id="08ee6-145">Choose **+** to add a tab to the right of the existing tabs.</span></span>

2. <span data-ttu-id="08ee6-146">Выберите вкладку из галереи, которая отображается.</span><span class="sxs-lookup"><span data-stu-id="08ee6-146">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="08ee6-147">Примите предложение о согласии.</span><span class="sxs-lookup"><span data-stu-id="08ee6-147">Accept the consent prompt.</span></span>

4. <span data-ttu-id="08ee6-148">Настройка вкладки через страницу [конфигурации и](../../tabs/how-to/create-tab-pages/configuration-page.md) выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="08ee6-148">Configure your tab through its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and select **Save**.</span></span>

  ![Диалоговое окно Добавить вкладку с галереей доступных вкладок](../../assets/images/tab_gallery.png)

## <a name="access-your-uploaded-bot"></a><span data-ttu-id="08ee6-150">Доступ к загруженным ботам</span><span class="sxs-lookup"><span data-stu-id="08ee6-150">Access your uploaded bot</span></span>

<span data-ttu-id="08ee6-151">После добавления бота в команду его должен использовать любой из этой группы, как внутри, так и за ее пределами, в зависимости от определения области бота.</span><span class="sxs-lookup"><span data-stu-id="08ee6-151">After adding the bot to a team, it must be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="08ee6-152">Все члены группы могут видеть сообщение в канале **General,** указывающее, что бот был добавлен в команду.</span><span class="sxs-lookup"><span data-stu-id="08ee6-152">All team members can see a post in the **General** channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="08ee6-153">Для бота Teams вы можете начать с того, что вы @mentioning имя бота.</span><span class="sxs-lookup"><span data-stu-id="08ee6-153">For a Teams bot, you can start by invoking your bot by @mentioning the name of the bot.</span></span>

<span data-ttu-id="08ee6-154">Чтобы протестировать прямые чаты с ботом, вы можете получить доступ к нему через дом Приложения, @mention его в канале, или найти его в окне **New Chat.**</span><span class="sxs-lookup"><span data-stu-id="08ee6-154">To test direct chats with your bot, you can either access it through the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="08ee6-155">Вы можете @mention бота в беседе или поискать его в окне **"Новый** чат", чтобы протестировать прямые чаты с ботом.</span><span class="sxs-lookup"><span data-stu-id="08ee6-155">You can @mention the bot in a conversation or search for it in the **New Chat** window to test direct chats with your bot.</span></span>

## <a name="access-your-uploaded-connector"></a><span data-ttu-id="08ee6-156">Доступ к загруженной соединители</span><span class="sxs-lookup"><span data-stu-id="08ee6-156">Access your uploaded Connector</span></span>

<span data-ttu-id="08ee6-157">С помощью приложения, загруженного в группе или беседе, пользователи могут настроить соединителет с помощью стандартного потока галереи соединители:</span><span class="sxs-lookup"><span data-stu-id="08ee6-157">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="08ee6-158">Перейдите на канал в команде.</span><span class="sxs-lookup"><span data-stu-id="08ee6-158">Go to a channel in the team.</span></span> <span data-ttu-id="08ee6-159">Выберите **дополнительные** параметры *(&#8943;)* и **соединители.**</span><span class="sxs-lookup"><span data-stu-id="08ee6-159">Choose **More options** (*&#8943;*) and choose **Connectors**.</span></span>

2. <span data-ttu-id="08ee6-160">Выберите соединителен из раздела **Sideloaded** в нижней части.</span><span class="sxs-lookup"><span data-stu-id="08ee6-160">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="08ee6-161">Настройте соединитель через страницу [конфигурации и](../../webhooks-and-connectors/how-to/connectors-creating.md) выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="08ee6-161">Configure your connector through its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and select **Save**.</span></span>

  ![Диалоговое окно Добавить вкладку с галереей доступных вкладок.](../../assets/images/connector_gallery.png)

## <a name="access-your-uploaded-messaging-extension"></a><span data-ttu-id="08ee6-163">Доступ к расширению загруженных сообщений</span><span class="sxs-lookup"><span data-stu-id="08ee6-163">Access your uploaded messaging extension</span></span>

<span data-ttu-id="08ee6-164">Загруженное приложение с расширением обмена сообщениями  автоматически отображается в меню More *(&#8943;)* в окне составить.</span><span class="sxs-lookup"><span data-stu-id="08ee6-164">An uploaded app with a messaging extension automatically appears in the **More options** (*&#8943;*) menu in the compose box.</span></span>

![Расширения для система обмена сообщениями](../../assets/images/compose-extensions/cesampleapp.png)


## <a name="remove-or-update-your-app"></a><span data-ttu-id="08ee6-166">Удаление или обновление приложения</span><span class="sxs-lookup"><span data-stu-id="08ee6-166">Remove or update your app</span></span>

<span data-ttu-id="08ee6-167">Чтобы удалить приложение, выберите значок удаления рядом с именем приложения в списке ботов **View Teams.**</span><span class="sxs-lookup"><span data-stu-id="08ee6-167">To remove your app, select the delete icon next to the app name in the **View Teams** bots list.</span></span> <span data-ttu-id="08ee6-168">Если вы измените сведения манифеста, сначала удалите приложение, а затем добавьте обновленный пакет, см. в приложении [Load your package into a team.](#load-your-package-into-teams)</span><span class="sxs-lookup"><span data-stu-id="08ee6-168">If you change manifest information, first remove the app and then add the updated package, see [Load your package into a team](#load-your-package-into-teams).</span></span> <span data-ttu-id="08ee6-169">Изменения кода в службе не требуют повторной отправки манифеста.</span><span class="sxs-lookup"><span data-stu-id="08ee6-169">Code changes on your service do not require you to upload your manifest again.</span></span> <span data-ttu-id="08ee6-170">Однако если изменения кода требуют обновлений манифеста, таких как изменения URL-адреса или ID приложения Майкрософт для бота, необходимо загрузить манифест снова.</span><span class="sxs-lookup"><span data-stu-id="08ee6-170">However, if the code changes require manifest updates, such as changes to the URL or the Microsoft app ID for its bot, you must upload the manifest again.</span></span>

> [!NOTE]
> <span data-ttu-id="08ee6-171">Невозможно полностью удалить бот из личного контекста.</span><span class="sxs-lookup"><span data-stu-id="08ee6-171">You cannot remove a bot from a personal context entirely.</span></span> <span data-ttu-id="08ee6-172">Если бот удаляется и добавляется снова, дополнительная связь с ботом добавляется к предыдущему разговору.</span><span class="sxs-lookup"><span data-stu-id="08ee6-172">If the bot is removed and added again, additional communication with the bot appends to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="08ee6-173">Заметки по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="08ee6-173">Troubleshooting notes</span></span>

<span data-ttu-id="08ee6-174">Если манифест не загружается, проверьте, следовали ли вы всем инструкциям в [Create the package](../../concepts/build-and-test/apps-package.md) и проверили манифест на [схему](../../resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="08ee6-174">If the manifest fails to load, check if you have followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>
