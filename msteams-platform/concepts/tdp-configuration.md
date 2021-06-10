---
title: Конфигурация приложения на портале разработчиков
description: Узнайте, как настроить и управлять приложениями с помощью портала разработчиков для Microsoft Teams
keywords: начало работы команд портала разработчиков
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: ce290bd7daa46467be279aae7c608321e75e2d57
ms.sourcegitcommit: 25539046d408c4270b988fd826d7cf1275f4b9dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2021
ms.locfileid: "52763151"
---
# <a name="app-configuration"></a><span data-ttu-id="ea077-104">Конфигурация приложения</span><span class="sxs-lookup"><span data-stu-id="ea077-104">App configuration</span></span>

<span data-ttu-id="ea077-105">Наиболее важной частью пакета Microsoft Teams является его manifest.jsфайл.</span><span class="sxs-lookup"><span data-stu-id="ea077-105">The most significant part of a Microsoft Teams app package is its manifest.json file.</span></span> <span data-ttu-id="ea077-106">Этот файл должен соответствовать схеме [Teams App](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="ea077-106">This file must conform to the [Teams App schema](~/resources/schema/manifest-schema.md).</span></span> <span data-ttu-id="ea077-107">В manifest.jsфайле содержатся метаданные, которые Teams правильно представить приложение пользователям.</span><span class="sxs-lookup"><span data-stu-id="ea077-107">The manifest.json file contains metadata, which allows Teams to correctly present your app to users.</span></span>

<span data-ttu-id="ea077-108">Следующие действия можно выполнить в разделе **Настройка** портала разработчиков:</span><span class="sxs-lookup"><span data-stu-id="ea077-108">You can perform the following actions in the **Configure** section of the Developer Portal:</span></span>

* <span data-ttu-id="ea077-109">Легко создайте пакет приложений.</span><span class="sxs-lookup"><span data-stu-id="ea077-109">Create an app package easily.</span></span>
* <span data-ttu-id="ea077-110">Опишите приложение.</span><span class="sxs-lookup"><span data-stu-id="ea077-110">Describe the app.</span></span>
* <span data-ttu-id="ea077-111">Upload значки.</span><span class="sxs-lookup"><span data-stu-id="ea077-111">Upload your icons.</span></span>
* <span data-ttu-id="ea077-112">Создать файл .zip для легкого распространения.</span><span class="sxs-lookup"><span data-stu-id="ea077-112">Produce a .zip file for easy distribution.</span></span>

> [!NOTE]
> <span data-ttu-id="ea077-113">Портал разработчиков не создает функциональный код для приложения или не создает приложение.</span><span class="sxs-lookup"><span data-stu-id="ea077-113">Developer Portal does not produce functional code for your app, or host your app.</span></span> <span data-ttu-id="ea077-114">Ваше приложение уже должно быть размещено и запущено по URL-адресу, указанному в манифесте: только в этом случае результатом процесса отправки приложения станет действующее приложение.</span><span class="sxs-lookup"><span data-stu-id="ea077-114">Your app must already be hosted and running at the URL listed in the manifest for the app upload process to result in a working app.</span></span>

:::image type="content" source="~/assets/images/tdp/tdp_configure_1.png" alt-text="Снимок экрана, показывающий страницу Настройка Teams портала разработчиков.":::

## <a name="basic-information-and-branding"></a><span data-ttu-id="ea077-116">Основные сведения и брендинг</span><span class="sxs-lookup"><span data-stu-id="ea077-116">Basic information and Branding</span></span>

<span data-ttu-id="ea077-117">Разделы **Основные** сведения и **Брендинг** определяют описание приложения на высоком уровне, которое вы делаете.</span><span class="sxs-lookup"><span data-stu-id="ea077-117">The **Basic information** and **Branding** sections define the high-level description of the app you are making.</span></span> <span data-ttu-id="ea077-118">Это включает имя, описание и визуальный брендинг приложения.</span><span class="sxs-lookup"><span data-stu-id="ea077-118">This includes the app’s name, description, and visual branding.</span></span> <span data-ttu-id="ea077-119">Сведения в этом разделе будут использоваться в диалоге Teams магазина и установки приложения.</span><span class="sxs-lookup"><span data-stu-id="ea077-119">The information in this section will be used in your app's Teams store listing and app installation dialogue.</span></span>

## <a name="capabilities"></a><span data-ttu-id="ea077-120">Возможности</span><span class="sxs-lookup"><span data-stu-id="ea077-120">Capabilities</span></span>

<span data-ttu-id="ea077-121">В **разделе Возможности** конфигурации указаны сведения о возможностях приложения.</span><span class="sxs-lookup"><span data-stu-id="ea077-121">The **Capabilities** section of Configuration has the app's capabilities details listed.</span></span>

> [!NOTE]
> <span data-ttu-id="ea077-122">Функция настройки приложения в настоящее время доступна только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="ea077-122">The app customization feature is currently available in the developer preview only.</span></span>
> 
> <span data-ttu-id="ea077-123">В качестве наилучшей практики необходимо предоставить рекомендации по настройке для пользователей и клиентов приложений, которые следует соблюдать при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="ea077-123">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="ea077-124">Дополнительные сведения см. [в Microsoft Teams.](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="ea077-124">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

<span data-ttu-id="ea077-125">Ниже следующую функцию:</span><span class="sxs-lookup"><span data-stu-id="ea077-125">Following are the capabilities:</span></span>

:::image type="content" source="~/assets/images/tdp/tdp_capabilities.png" alt-text="Снимок экрана, показывающий страницу Настройка Teams портала разработчиков.":::

* <span data-ttu-id="ea077-127">**Личное приложение**</span><span class="sxs-lookup"><span data-stu-id="ea077-127">**Personal app**</span></span> 

  <span data-ttu-id="ea077-128">В этом разделе вы можете определить набор вкладок, представленных по умолчанию в личном приложении, то есть опыт работы пользователя с приложением за пределами контекста группы или канала.</span><span class="sxs-lookup"><span data-stu-id="ea077-128">This section lets you define a set of tabs that are presented by default in the personal app experience, that is, the experience a user has with your app outside the context of a team or channel.</span></span> <span data-ttu-id="ea077-129">В этом разделе ука-ь ниже следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="ea077-129">In this section, provide the following details:</span></span>

  * <span data-ttu-id="ea077-130">Имя вкладки.</span><span class="sxs-lookup"><span data-stu-id="ea077-130">The tab name.</span></span>
  * <span data-ttu-id="ea077-131">Уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ea077-131">A unique identifier.</span></span>
  * <span data-ttu-id="ea077-132">URL-адрес, который указывает на пользовательский интерфейс, отображаемый в Teams.</span><span class="sxs-lookup"><span data-stu-id="ea077-132">The URL that points to the UI to be displayed in Teams.</span></span>
  * <span data-ttu-id="ea077-133">URL-адрес, который необходимо использовать, если пользователь выбирает для просмотра вкладки в браузере.</span><span class="sxs-lookup"><span data-stu-id="ea077-133">The URL to use if a user opts to view the tab in a browser.</span></span> <span data-ttu-id="ea077-134">Это необязательная информация.</span><span class="sxs-lookup"><span data-stu-id="ea077-134">This is an optional information.</span></span>
  * <span data-ttu-id="ea077-135">Любые дополнительные домены, с которых вкладка ожидает загрузки из или ссылки.</span><span class="sxs-lookup"><span data-stu-id="ea077-135">Any additional domains from which the tab expects to load from or link to.</span></span>

* <span data-ttu-id="ea077-136">**Приложение группы и канала**</span><span class="sxs-lookup"><span data-stu-id="ea077-136">**Group and channel app**</span></span>

  <span data-ttu-id="ea077-137">Вкладка Teams становится частью канала и обеспечивает быстрый доступ к сведениям и ресурсам группы.</span><span class="sxs-lookup"><span data-stu-id="ea077-137">A Teams tab becomes part of a channel and provides quick access to team information and resources.</span></span> <span data-ttu-id="ea077-138">Например, вкладка Planner для канала содержит один план, Power BI вкладка карты для определенного отчета.</span><span class="sxs-lookup"><span data-stu-id="ea077-138">For example, the Planner tab for a channel contains a single plan, the Power BI tab maps to a specific report.</span></span> <span data-ttu-id="ea077-139">Пользователи могут перейти к нужному контексту, но у них не должно быть возможности переходить вне вкладки. Например, вкладка "Power BI" не разрешает переходить к другим отчетам Power BI, но на ней есть кнопка **Перейти на веб-сайт**, при нажатии которой отчет открывается на главном веб-сайте Power BI.</span><span class="sxs-lookup"><span data-stu-id="ea077-139">Users can drill down to the relevant context, but they should not be able to navigate outside the tab. The Power BI tab, for instance, doesn't enable navigation to other Power BI reports, but it does enable the **Go to website** button that launches the report in the main Power BI website.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ea077-140">Для вкладок группы необходимо предоставить URL-адрес конфигурации для предоставления параметров и сбора сведений, которые помогут настроить содержимое и возможности вкладки. Эта страница HTML с iframed отображается, когда пользователь сначала добавляет вкладку в канал.</span><span class="sxs-lookup"><span data-stu-id="ea077-140">For team tabs, you must provide a Configuration URL to present options and gather information, that would help you to customize the content and experience of your tab. This iframed HTML page is displayed when a user first adds the tab to a channel.</span></span>
    > <span data-ttu-id="ea077-141">Также необходимо указать все дополнительные домены, из которых эта вкладка будет загружать информацию или с которыми она будет связана.</span><span class="sxs-lookup"><span data-stu-id="ea077-141">You must also provide any additional domains that the tab expects to load from or link to.</span></span>

* <span data-ttu-id="ea077-142">**Бот**</span><span class="sxs-lookup"><span data-stu-id="ea077-142">**Bot**</span></span>

  <span data-ttu-id="ea077-143">В этом разделе можно добавить в приложение [бот для интерактивных бесед](~/bots/what-are-bots.md).</span><span class="sxs-lookup"><span data-stu-id="ea077-143">This section allows you to add a [conversational bot](~/bots/what-are-bots.md) to your app.</span></span> <span data-ttu-id="ea077-144">Если у вас уже есть бот, зарегистрированный на платформе Bot Framework, можно добавить его: для этого щелкните **Настройка** и укажите имя бота, идентификатор Bot Framework и области, в которых будет работать этот бот.</span><span class="sxs-lookup"><span data-stu-id="ea077-144">If you already have a bot registered with Bot Framework, you can add that bot by clicking **Set Up** and supplying the bot's name, Bot Framework ID, and defining the scopes in which the bot will work.</span></span>

  <span data-ttu-id="ea077-145">Если вы еще не зарегистрировали бота в bot Framework, нажмите кнопку **Регистрация,** чтобы создать новый.</span><span class="sxs-lookup"><span data-stu-id="ea077-145">If you have not registered the bot with the Bot Framework yet, click **Register** to create a new one.</span></span> <span data-ttu-id="ea077-146">После регистрации бота возвращайся в этот раздел редактора манифеста, чтобы ввести его имя и имя Bot Framework ID.</span><span class="sxs-lookup"><span data-stu-id="ea077-146">After you have registered your bot, come back to this section of the Manifest Editor to enter its name and Bot Framework ID.</span></span>

  <span data-ttu-id="ea077-147">После того как вы предоставили сведения о боте, теперь можно дополнительно определить список команд, которые бот может предложить пользователям.</span><span class="sxs-lookup"><span data-stu-id="ea077-147">After you have supplied your bot's information, you can now optionally define a list of commands that your bot can suggest to users.</span></span> <span data-ttu-id="ea077-148">Добавьте имя команды, описание команды с указанием синтаксиса и аргументов, а также области, к которым должна применяться эта команда.</span><span class="sxs-lookup"><span data-stu-id="ea077-148">Add the name of the command, a description of the command which indicates its syntax and arguments, and the scope(s) to which this command should apply.</span></span>

  <span data-ttu-id="ea077-149">Обратите внимание, что если в вашем определении бот поддерживает только одну область. то команды, указанные для неподдерживаемых областей, будут игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="ea077-149">Note that if you have defined your bot to only support one scope, commands specified for the unsupported scope will be ignored.</span></span> <span data-ttu-id="ea077-150">Можно в любое время изменить области, поддерживаемые вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="ea077-150">You can edit the scopes your bot supports at any time.</span></span>

* <span data-ttu-id="ea077-151">**Connector**</span><span class="sxs-lookup"><span data-stu-id="ea077-151">**Connector**</span></span>

  <span data-ttu-id="ea077-152">В этом разделе можно добавить соединитель в приложение.</span><span class="sxs-lookup"><span data-stu-id="ea077-152">This section allows you to add a connector to your app.</span></span> <span data-ttu-id="ea077-153">Если вы уже зарегистрировали Office 365 соединители, выберите **Настройка** и введите имя и ID соединитетеля.</span><span class="sxs-lookup"><span data-stu-id="ea077-153">If you already have registered an Office 365 connector, select **Set up** and enter the name and ID of the connector.</span></span> <span data-ttu-id="ea077-154">Если нужен новый соединитель, щелкните **Регистрация**, чтобы перейти на панель разработчика соединителей в браузере.</span><span class="sxs-lookup"><span data-stu-id="ea077-154">If you want a new connector click **Register** to be taken to the Connector Developer Dashboard in your browser.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ea077-155">Настройка приложения позволяет администраторам изменять внешний вид приложений, загружаемых через боты, расширения обмена сообщениями, вкладки и соединители.</span><span class="sxs-lookup"><span data-stu-id="ea077-155">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="ea077-156">Например, если администратор Teams настраивает имя приложения от до , приложение будет отображаться с новым именем `Contoso` `Contoso Agent` для `Contoso Agent` пользователей.</span><span class="sxs-lookup"><span data-stu-id="ea077-156">For example, if the Teams admin customizes the name of an app from `Contoso` to `Contoso Agent`, then the app will appear with the new name `Contoso Agent` to the users.</span></span> <span data-ttu-id="ea077-157">Однако при добавлении соединитетеля в чат в списке соединители по-прежнему будут показывать имя приложения как `Contoso` .</span><span class="sxs-lookup"><span data-stu-id="ea077-157">However, while adding a connector to a chat, in the list, the connectors will still show the name of the app as `Contoso`.</span></span>

* <span data-ttu-id="ea077-158">**Расширения для сообщений**</span><span class="sxs-lookup"><span data-stu-id="ea077-158">**Messaging Extensions**</span></span>

  <span data-ttu-id="ea077-159">[Расширения для сообщений](~/messaging-extensions/what-are-messaging-extensions.md) — удобный способ работы пользователей с вашим приложением в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ea077-159">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) are a powerful way for users to engage with your app within Microsoft Teams.</span></span> <span data-ttu-id="ea077-160">Пользователи могут запрашивать сведения в вашей службе и публиковать их в виде карточек непосредственно в канале или в чате, где идет беседа.</span><span class="sxs-lookup"><span data-stu-id="ea077-160">Users can query for information from your service and post that information in the form of cards, right into the channel or chat conversation.</span></span>

  <span data-ttu-id="ea077-161">Расширения для сообщений работают на основе Bot Framework, поэтому для их работы требуется настроенный бот.</span><span class="sxs-lookup"><span data-stu-id="ea077-161">Messaging extensions are powered by Bot Framework bots, so they require a configured bot to operate.</span></span> <span data-ttu-id="ea077-162">Если у вас уже есть имя и идентификатор Bot Framework бота, на основе которого должно работать расширение для сообщений, введите эти данные.</span><span class="sxs-lookup"><span data-stu-id="ea077-162">If you have the name and Bot Framework ID of the bot you would like to power the messaging extension, enter it.</span></span> <span data-ttu-id="ea077-163">В противном случае щелкните *Регистрация*, чтобы создать бот, а затем введите соответствующие данные.</span><span class="sxs-lookup"><span data-stu-id="ea077-163">Otherwise, click *Register* to create one and enter the information afterward.</span></span> <span data-ttu-id="ea077-164">Выберите, может ли пользователь обновлять конфигурацию расширения для сообщений.</span><span class="sxs-lookup"><span data-stu-id="ea077-164">Select whether the configuration of a messaging extension can be updated by the user.</span></span>

  <span data-ttu-id="ea077-165">После настройки конечного бота определите команды и параметры, которые может принять расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="ea077-165">After you have the underlying bot configured, define the commands and parameters which the messaging extension can accept.</span></span>

  <span data-ttu-id="ea077-166">Для каждой команды требуется название и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ea077-166">Each command requires a title and an ID.</span></span> <span data-ttu-id="ea077-167">Также команда может содержать описание для пользователя.</span><span class="sxs-lookup"><span data-stu-id="ea077-167">The command can optionally contain a description for the user.</span></span> <span data-ttu-id="ea077-168">Каждая команда может поддерживать до пяти параметров, для каждого из которых требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="ea077-168">Each command can support up to five parameters, each of which requires the following:</span></span>

  * <span data-ttu-id="ea077-169">Имя параметра, как оно отображается в Teams клиенте и включено в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="ea077-169">The name of the parameter as it appears in the Teams client and is included in the user request.</span></span>
  * <span data-ttu-id="ea077-170">Удобное название.</span><span class="sxs-lookup"><span data-stu-id="ea077-170">A user-friendly title.</span></span>
  * <span data-ttu-id="ea077-171">Дополнительное описание.</span><span class="sxs-lookup"><span data-stu-id="ea077-171">An optional description.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ea077-172">Чтобы создать расширение обмена сообщениями с помощью студии приложений, см. в [приложении create messaging extension using app studio.](~/resources/create-messaging-extension-using-appstudio.md)</span><span class="sxs-lookup"><span data-stu-id="ea077-172">To create messaging extension using app studio, see [create messaging extension using app studio](~/resources/create-messaging-extension-using-appstudio.md).</span></span>

* <span data-ttu-id="ea077-173">**Расширение собрания**</span><span class="sxs-lookup"><span data-stu-id="ea077-173">**Meeting extension**</span></span>

  <span data-ttu-id="ea077-174">TODO: Rajesh R.</span><span class="sxs-lookup"><span data-stu-id="ea077-174">//TODO: Rajesh R.</span></span>

* <span data-ttu-id="ea077-175">**Сцена**</span><span class="sxs-lookup"><span data-stu-id="ea077-175">**Scene**</span></span>

  <span data-ttu-id="ea077-176">Сцены в режиме together — это артефакт, созданный разработчиком сцены с помощью студии Microsoft Scene, которая объединяет людей вместе с видеопотоком в творческой среде, задуманной создателем сцены.</span><span class="sxs-lookup"><span data-stu-id="ea077-176">Scenes in Together Mode is an artifact created by the scene developer using the Microsoft Scene studio that brings people together along with their video stream in a creative setting as conceived by the scene creator.</span></span> <span data-ttu-id="ea077-177">В зачатом параметре сцены участники обозначили места с видеопотоками, отрисовав их в этих местах.</span><span class="sxs-lookup"><span data-stu-id="ea077-177">In a conceived scene setting, participants have designated seats with video streams rendered in those seats.</span></span> <span data-ttu-id="ea077-178">Дополнительные сведения см. [в Teams Режиме совместной работы.](~/apps-in-teams-meetings/teams-together-mode.md)</span><span class="sxs-lookup"><span data-stu-id="ea077-178">For more information, see [Teams Together Mode](~/apps-in-teams-meetings/teams-together-mode.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="ea077-179">Разрешения</span><span class="sxs-lookup"><span data-stu-id="ea077-179">Permissions</span></span>

<span data-ttu-id="ea077-180">Вы можете обогатить Teams с помощью родных возможностей устройства, таких как камера, микрофон и расположение.</span><span class="sxs-lookup"><span data-stu-id="ea077-180">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span>

## <a name="languages"></a><span data-ttu-id="ea077-181">Языки</span><span class="sxs-lookup"><span data-stu-id="ea077-181">Languages</span></span>

<span data-ttu-id="ea077-182">Настройка или изменение языков, поддерживаемых вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="ea077-182">Set up or change the languages that your app supports.</span></span>

## <a name="single-sign-on"></a><span data-ttu-id="ea077-183">Единый вход</span><span class="sxs-lookup"><span data-stu-id="ea077-183">Single Sign-On</span></span>

<span data-ttu-id="ea077-184">Настройка приложения для проверки подлинности пользователей с помощью одного входного знака (SSO).</span><span class="sxs-lookup"><span data-stu-id="ea077-184">Configure your app to authenticate users with single sign-on (SSO).</span></span>

## <a name="domains"></a><span data-ttu-id="ea077-185">Домены</span><span class="sxs-lookup"><span data-stu-id="ea077-185">Domains</span></span>

<span data-ttu-id="ea077-186">Список допустимого домена для веб-сайтов, которые приложение ожидает загрузить в Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="ea077-186">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="ea077-187">Списки домена могут включать, например, поддиайки. `*.example.com`</span><span class="sxs-lookup"><span data-stu-id="ea077-187">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="ea077-188">Это соответствует ровно одному сегменту домена; если вам нужно `a.b.example.com` соответствовать, то используйте `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="ea077-188">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="ea077-189">Если конфигурации вкладок или пользовательскому интерфейсу контента необходимо перейти к любому другому домену, кроме одного использования для конфигурации вкладок, этот домен должен быть указан здесь.</span><span class="sxs-lookup"><span data-stu-id="ea077-189">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="ea077-190">Не обязательно включать в приложение домены поставщиков удостоверений, которые необходимо поддерживать.</span><span class="sxs-lookup"><span data-stu-id="ea077-190">It is not necessary to include the domains of the identity providers you want to support in your app.</span></span> <span data-ttu-id="ea077-191">Например, чтобы проверить подлинность с помощью google ID, необходимо перенаправить accounts.google.com, однако не следует включать accounts.google.com `validDomains[]` в .</span><span class="sxs-lookup"><span data-stu-id="ea077-191">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="ea077-192">Teams приложения, которые требуют нормальной работы собственных URL-адресов sharepoint, включают в допустимый список доменов "{teamsitedomain}".</span><span class="sxs-lookup"><span data-stu-id="ea077-192">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea077-193">Не добавляйте домены, которые находятся вне вашего контроля, напрямую или с помощью подкрентов.</span><span class="sxs-lookup"><span data-stu-id="ea077-193">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="ea077-194">Например, `yourapp.onmicrosoft.com` допустимо, однако, `*.onmicrosoft.com` не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="ea077-194">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="ea077-195">Объект — массив со всеми элементами `string` типа.</span><span class="sxs-lookup"><span data-stu-id="ea077-195">The object is an array with all elements of the type `string`.</span></span>

## <a name="advanced"></a><span data-ttu-id="ea077-196">Дополнительно</span><span class="sxs-lookup"><span data-stu-id="ea077-196">Advanced</span></span>
<span data-ttu-id="ea077-197">Todo by Karthig</span><span class="sxs-lookup"><span data-stu-id="ea077-197">//Todo by Karthig</span></span>

### <a name="app-content"></a><span data-ttu-id="ea077-198">Содержимое приложения</span><span class="sxs-lookup"><span data-stu-id="ea077-198">App content</span></span>
<span data-ttu-id="ea077-199">Todo by Karthig</span><span class="sxs-lookup"><span data-stu-id="ea077-199">//Todo by Karthig</span></span>

### <a name="first-party-settings"></a><span data-ttu-id="ea077-200">Параметры первой стороны</span><span class="sxs-lookup"><span data-stu-id="ea077-200">First party settings</span></span>
<span data-ttu-id="ea077-201">Todo by Karthig</span><span class="sxs-lookup"><span data-stu-id="ea077-201">//Todo by Karthig</span></span>

## <a name="see-also"></a><span data-ttu-id="ea077-202">См. также</span><span class="sxs-lookup"><span data-stu-id="ea077-202">See also</span></span>

* [<span data-ttu-id="ea077-203">Обзор портала Teams разработчиков</span><span class="sxs-lookup"><span data-stu-id="ea077-203">Overview of Teams Developer Portal</span></span>](~/concepts/build-and-test/teams-developer-portal.md)
* [<span data-ttu-id="ea077-204">Распространение Teams портала разработчиков</span><span class="sxs-lookup"><span data-stu-id="ea077-204">Distribute Teams Developer Portal</span></span>](~/concepts/tdp-distribute.md)
* [<span data-ttu-id="ea077-205">Средства в Teams портале разработчиков</span><span class="sxs-lookup"><span data-stu-id="ea077-205">Tools in Teams Developer Portal</span></span>](~/concepts/tdp-tools.md)