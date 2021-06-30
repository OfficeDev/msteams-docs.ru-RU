---
title: Добавьте Power Virtual Agents чат-бота в Teams
author: surbhigupta
description: интеграция Power Virtual Agents чат-бота в Teams платформе
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 2aa8cc510033768b68cf01cbb5b0327bffe13154
ms.sourcegitcommit: f62634c59b697107e5bb3c38867b21007d328b1e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2021
ms.locfileid: "53196252"
---
# <a name="add-power-virtual-agents-chatbot"></a><span data-ttu-id="52352-103">Добавление чатбота Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="52352-103">Add Power Virtual Agents chatbot</span></span> 

<span data-ttu-id="52352-104">Power Virtual Agents — это решение графического интерфейса без кода, которое позволяет каждому члену вашей команды создавать богатых чат-ботов, которые легко интегрируются с Teams платформой.</span><span class="sxs-lookup"><span data-stu-id="52352-104">Power Virtual Agents is a no-code, guided graphical interface solution that empowers every member of your team to create rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="52352-105">Все содержимое, которое было Power Virtual Agents, естественно, Teams.</span><span class="sxs-lookup"><span data-stu-id="52352-105">All content authored in Power Virtual Agents renders naturally in Teams.</span></span> <span data-ttu-id="52352-106">Power Virtual Agents боты вовлекались с пользователями в Teams чата.</span><span class="sxs-lookup"><span data-stu-id="52352-106">Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="52352-107">ИТ-администраторы, бизнес-аналитики, специалисты по доменам и опытные разработчики приложений могут разрабатывать, разрабатывать и публиковать интеллектуальные виртуальные агенты для Teams без установки среды разработки.</span><span class="sxs-lookup"><span data-stu-id="52352-107">The IT administrators, business analysts, domain specialists, and skilled app developers can design, develop, and publish intelligent virtual agents for Teams without having to setup a development environment.</span></span> <span data-ttu-id="52352-108">Они могут создавать веб-службы или непосредственно регистрироваться в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="52352-108">They can create a web service, or directly register with the Bot Framework.</span></span> 

<span data-ttu-id="52352-109">В этом документе вы можете узнать, как сделать чат-бот доступным в Teams через портал Power Virtual Agents и добавить бот в Teams с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="52352-109">This document guides you on how to make your chatbot available in Teams through the Power Virtual Agents portal, and add your bot to Teams using App Studio.</span></span> 

<span data-ttu-id="52352-110">Power Virtual Agents позволяет создавать мощные чат-боты, которые могут отвечать на вопросы, заданные вашими клиентами, другими сотрудниками или посетителями веб-сайта или службы.</span><span class="sxs-lookup"><span data-stu-id="52352-110">Power Virtual Agents lets you create powerful chatbots that can answer questions posed by your customers, other employees, or visitors to your website or service.</span></span>

<span data-ttu-id="52352-111">Эти боты могут быть легко созданы без необходимости для ученых или разработчиков данных.</span><span class="sxs-lookup"><span data-stu-id="52352-111">These bots can be created easily without the need for data scientists or developers.</span></span>

> [!NOTE]
> <span data-ttu-id="52352-112">Добавление чат-бота в Microsoft Teams, некоторые данные, такие как содержимое бота и содержимое пользовательского чата, Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="52352-112">By adding your chatbot to Microsoft Teams, some of the data, such as bot content and user chat content, is shared with Microsoft Teams.</span></span> <span data-ttu-id="52352-113">Это означает, что ваши данные вытекают за пределы соответствия требованиям организации и [географических или региональных границ.](/power-virtual-agents/data-location)</span><span class="sxs-lookup"><span data-stu-id="52352-113">It means that your data flows outside of your [organization’s compliance and geographic or regional boundaries](/power-virtual-agents/data-location).</span></span> <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a><span data-ttu-id="52352-114">Сделать чат-бот доступным в Teams через портал Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="52352-114">Make your chatbot available in Teams through the Power Virtual Agents portal</span></span>

<span data-ttu-id="52352-115">Чтобы сделать чат-бот доступным Teams на Power Virtual Agents портале, необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="52352-115">To make your chatbot available in Teams through the Power Virtual Agents portal, you must perform the following process steps:</span></span>

<span data-ttu-id="52352-116">**Чтобы сделать чат-бот доступным в Teams**</span><span class="sxs-lookup"><span data-stu-id="52352-116">**To make the chatbot available in Teams**</span></span>

1. <span data-ttu-id="52352-117">**Публикация последнего контента бота**</span><span class="sxs-lookup"><span data-stu-id="52352-117">**Publish the latest bot content**</span></span>  
<span data-ttu-id="52352-118">После создания чат-бота на портале Power Virtual Agents необходимо опубликовать бот, чтобы Teams пользователи могли взаимодействовать с ним.</span><span class="sxs-lookup"><span data-stu-id="52352-118">After creating a chatbot in the Power Virtual Agents portal, you must publish your bot before Teams users can interact with it.</span></span> <span data-ttu-id="52352-119">Дополнительные сведения см. в [публикации последнего контента бота.](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)</span><span class="sxs-lookup"><span data-stu-id="52352-119">For more information, see [Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span></span>

   ![публикация на портале виртуальных агентов power](../../assets/images/pva-publish.png)

1. <span data-ttu-id="52352-121">**Настройка канала Teams**</span><span class="sxs-lookup"><span data-stu-id="52352-121">**Configure the Teams channel**</span></span>  
<span data-ttu-id="52352-122">После публикации бота добавьте канал Teams, чтобы сделать его доступным для Teams пользователей.</span><span class="sxs-lookup"><span data-stu-id="52352-122">After publishing your bot, add the Teams channel to make the bot available to Teams users.</span></span>

   ![каналы на портале виртуальных агентов power](../../assets/images/pva-channels.png)

1. <span data-ttu-id="52352-124">**Создание ID приложения для чат-бота**</span><span class="sxs-lookup"><span data-stu-id="52352-124">**Generate an App ID for your chatbot**</span></span>  
<span data-ttu-id="52352-125">После добавления канала Teams чат-бота в диалоговом окне создается **ID** приложения.</span><span class="sxs-lookup"><span data-stu-id="52352-125">After adding the Teams channel to your chatbot, an **App ID** is generated in the dialog box.</span></span> <span data-ttu-id="52352-126">Идентификатор приложения — уникальный идентификатор, созданный Корпорацией Майкрософт для вашего бота.</span><span class="sxs-lookup"><span data-stu-id="52352-126">The App ID is a unique Microsoft generated identifier for your bot.</span></span> <span data-ttu-id="52352-127">Сохраните ID приложения, чтобы создать пакет приложений для Teams.</span><span class="sxs-lookup"><span data-stu-id="52352-127">Save the App ID to create an app package for Teams.</span></span>

## <a name="add-your-bot-to-teams-using-app-studio"></a><span data-ttu-id="52352-128">Добавление бота в Teams с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="52352-128">Add your bot to Teams using App Studio</span></span>

<span data-ttu-id="52352-129">Если [в экземпляре](/microsoftteams/admin-settings) Teams включена загрузка пользовательских приложений, вы можете использовать Teams App Studio для непосредственной загрузки чат-бота и немедленного его использования.</span><span class="sxs-lookup"><span data-stu-id="52352-129">If [uploading custom apps is enabled](/microsoftteams/admin-settings) in your Teams instance, you can use Teams App Studio to directly upload your chatbot and start using it immediately.</span></span> <span data-ttu-id="52352-130">Чтобы поделиться своим чат-ботом, можно попросить администратора сделать бот доступным в каталоге приложений клиента или отправить пакет приложения другим и попросить их самостоятельно загрузить его.</span><span class="sxs-lookup"><span data-stu-id="52352-130">To share your chatbot, you can request your admin to make your bot available in the tenant app catalog or you can send your app package to others and ask them to upload it independently.</span></span>

1. <span data-ttu-id="52352-131">**Установка App Studio в Teams**</span><span class="sxs-lookup"><span data-stu-id="52352-131">**Install App Studio in Teams**</span></span>  
<span data-ttu-id="52352-132">App Studio — это Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="52352-132">App Studio is a Teams app.</span></span> <span data-ttu-id="52352-133">Установите App Studio из Teams, упрощает процесс создания и регистрации ботов в Teams:</span><span class="sxs-lookup"><span data-stu-id="52352-133">Install App Studio from the Teams store that simplifies the process of bot creation and registration in Teams:</span></span> 

   1. <span data-ttu-id="52352-134">Выберите значок магазина приложений Teams экземпляре и выберите **App Studio.**</span><span class="sxs-lookup"><span data-stu-id="52352-134">Select the app store icon from Teams instance, and search for **App Studio**.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. <span data-ttu-id="52352-135">Выберите **плитку App Studio** и выберите **Установите** в диалоговом окне всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="52352-135">Select the **App Studio** tile and select **Install** in the pop-up dialog box.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. <span data-ttu-id="52352-136">**Создание манифеста Teams приложения в App Studio**</span><span class="sxs-lookup"><span data-stu-id="52352-136">**Create the Teams app manifest in App Studio**</span></span>  
<span data-ttu-id="52352-137">Боты в Teams определяются файлом JSON манифеста приложения, который предоставляет основные сведения о вашем боте и его возможностях.</span><span class="sxs-lookup"><span data-stu-id="52352-137">Bots in Teams are defined by an app manifest JSON file that provides the basic information about your bot and its capabilities.</span></span> <span data-ttu-id="52352-138">В **App Studio** выберите редактор **Манифеста** и **выберите Создание нового приложения.**</span><span class="sxs-lookup"><span data-stu-id="52352-138">In **App Studio**, select **Manifest editor**, and select **Create a new app**.</span></span>

    ![создание нового приложения](../../assets/images/get-started/create-new-app.png)

1. <span data-ttu-id="52352-140">**Добавление сведений о боте**</span><span class="sxs-lookup"><span data-stu-id="52352-140">**Add your bot details**</span></span>  
<span data-ttu-id="52352-141">Выполните все необходимые поля.</span><span class="sxs-lookup"><span data-stu-id="52352-141">Complete all the required fields.</span></span> <span data-ttu-id="52352-142">Полное описание каждого поля см. в определении [схемы манифеста.](../../resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="52352-142">For a full description of each field see [manifest schema definition](../../resources/schema/manifest-schema.md).</span></span>

    ![добавление сведений о приложении](../../assets/images/get-started/add-app-details.png)

1. <span data-ttu-id="52352-144">**Настройка бота** Чтобы настроить бот, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="52352-144">**Set up your bot** To set-up the bot, perform the following steps:</span></span> 
     1. <span data-ttu-id="52352-145">Откройте **вкладку Bots.**</span><span class="sxs-lookup"><span data-stu-id="52352-145">Open the **Bots** tab.</span></span> 
     1. <span data-ttu-id="52352-146">Выберите **настройка**  >  **существующего бота** и введите имя вашего бота.</span><span class="sxs-lookup"><span data-stu-id="52352-146">Select **Setup** > **Existing bot** and enter the name of your bot.</span></span>

   ![Настройка бота](../../assets/images/get-started/bot-set-up.png) 

   <span data-ttu-id="52352-148">На следующем изображении повествуют о том, как настроить существующий бот:</span><span class="sxs-lookup"><span data-stu-id="52352-148">The following image depicts how to set-up an existing bot:</span></span>      

   ![существующая настройка бота](../../assets/images/get-started/existing-bot-set-up.png)
       
1. <span data-ttu-id="52352-150">**Добавление ID приложения**</span><span class="sxs-lookup"><span data-stu-id="52352-150">**Add your App ID**</span></span>  
<span data-ttu-id="52352-151">Чтобы добавить свой ID приложения, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="52352-151">To add your App ID, perform the following steps:</span></span>  
    1. <span data-ttu-id="52352-152">Выберите **Подключение другой бот-id** и вклеите скопированные ранее **ID** приложения.</span><span class="sxs-lookup"><span data-stu-id="52352-152">Select **Connect to a different bot id** and paste the **App Id** you copied earlier.</span></span> 
    1. <span data-ttu-id="52352-153">Выберите **Область личного**  >    >  **сохранения**.</span><span class="sxs-lookup"><span data-stu-id="52352-153">Select **Scope** > **Personal** > **Save**.</span></span>

    ![добавление id приложения](../../assets/images/get-started/add-app-id.png)

1. <span data-ttu-id="52352-155">**Добавление допустимого домена для бота**</span><span class="sxs-lookup"><span data-stu-id="52352-155">**Add valid domains for your bot**</span></span>  
<span data-ttu-id="52352-156">Этот шаг необходим только в том случае, если бот требует от пользователя войти.</span><span class="sxs-lookup"><span data-stu-id="52352-156">This step is only required if your bot requires the user to sign in.</span></span> <span data-ttu-id="52352-157">Выберите **домены и разрешения** и в поле **Допустимые** домены ввести следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="52352-157">Select **Domains and permissions** and in the **Valid Domains** field, provide the following input:</span></span>

    ```bash
       token.botframework.com
    ```

1. <span data-ttu-id="52352-158">**Тестирование и распространение бота**</span><span class="sxs-lookup"><span data-stu-id="52352-158">**Test and distribute your bot**</span></span>  
<span data-ttu-id="52352-159">Откройте **тест и раздайте** вкладку и выберите **Установите,** чтобы добавить бот непосредственно в Teams экземпляр.</span><span class="sxs-lookup"><span data-stu-id="52352-159">Open **Test and distribute** tab and select **Install** to add your bot directly to your Teams instance.</span></span> <span data-ttu-id="52352-160">Кроме того, вы можете скачать завершенный пакет приложений, чтобы поделиться с Teams пользователями или предоставить его администратору, чтобы сделать бот доступным в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="52352-160">Alternately, you can download the completed app package to share with Teams users or provide it to your admin to make your bot available in the tenant app catalog.</span></span>

1. <span data-ttu-id="52352-161">**Запуск чата** </span><span class="sxs-lookup"><span data-stu-id="52352-161">**Start a chat** </span></span>  
<span data-ttu-id="52352-162">Процесс создания для добавления бота Power Virtual Agents чата в Teams завершен.</span><span class="sxs-lookup"><span data-stu-id="52352-162">The set-up process for adding your Power Virtual Agents chat bot to Teams is complete.</span></span> <span data-ttu-id="52352-163">Теперь вы можете начать беседу с ботом в личном чате.</span><span class="sxs-lookup"><span data-stu-id="52352-163">You can now start a conversation with your bot in a personal chat.</span></span>

## <a name="see-also"></a><span data-ttu-id="52352-164">См. также</span><span class="sxs-lookup"><span data-stu-id="52352-164">See also</span></span>

* [<span data-ttu-id="52352-165">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="52352-165">Power Virtual Agents</span></span>](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  
* <span data-ttu-id="52352-166">[Создайте чат-бот для Teams microsoft Power Virtual Agents.](../bot-features.md#bots-with-power-virtual-agents)</span><span class="sxs-lookup"><span data-stu-id="52352-166">[Create a chatbot for Teams with Microsoft Power Virtual Agents](../bot-features.md#bots-with-power-virtual-agents).</span></span>  
* [<span data-ttu-id="52352-167">Power Virtual Agents портал</span><span class="sxs-lookup"><span data-stu-id="52352-167">Power Virtual Agents portal</span></span>](https://powervirtualagents.microsoft.com)
* [<span data-ttu-id="52352-168">Публикация Power Virtual Agents бота</span><span class="sxs-lookup"><span data-stu-id="52352-168">Publish your Power Virtual Agents bot</span></span>](/power-virtual-agents/publication-fundamentals-publish-channels)
* <span data-ttu-id="52352-169">[Безопасность и соответствие требованиям в Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span><span class="sxs-lookup"><span data-stu-id="52352-169">[Security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span></span>

## <a name="next-step"></a><span data-ttu-id="52352-170">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="52352-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52352-171">Создание виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="52352-171">Create a Virtual Assistant</span></span>](~/samples/virtual-assistant.md)
