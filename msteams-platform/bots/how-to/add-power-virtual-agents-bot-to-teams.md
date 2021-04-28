---
title: Добавление чат-бота виртуальных агентов Power в Teams
author: laujan
description: интеграция чат-бота Power Virtual Agents в платформе Teams
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: bd1528d06f9e9f4ca3a03f167ecb3c537977fb61
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058623"
---
# <a name="add-power-virtual-agents-chatbot"></a><span data-ttu-id="bcc7f-103">Добавление чатбота Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="bcc7f-103">Add Power Virtual Agents chatbot</span></span> 

<span data-ttu-id="bcc7f-104">Power Virtual Agents — это не кодовое решение графического интерфейса, которое позволяет каждому члену вашей команды создавать богатых чат-ботов, которые легко интегрируются с платформой Teams.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-104">Power Virtual Agents is a no-code, guided graphical interface solution that empowers every member of your team to create rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="bcc7f-105">Все контенты, авторские в Power Virtual Agents, отрисовка естественно в Teams.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-105">All content authored in Power Virtual Agents renders naturally in Teams.</span></span> <span data-ttu-id="bcc7f-106">Power Virtual Agents bots engage with users in the Teams native chat canvas.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-106">Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="bcc7f-107">ИТ-администраторы, бизнес-аналитики, специалисты по доменам и опытные разработчики приложений могут разрабатывать, разрабатывать и публиковать интеллектуальные виртуальные агенты для Teams без настройки среды разработки.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-107">The IT administrators, business analysts, domain specialists, and skilled app developers can design, develop and publish intelligent virtual agents for Teams without having to setup a development environment.</span></span> <span data-ttu-id="bcc7f-108">Они могут создавать веб-службы или непосредственно регистрироваться в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-108">They can create a web service, or directly register with the Bot Framework.</span></span> 

<span data-ttu-id="bcc7f-109">В этом документе вы можете ознакомиться с тем, как сделать чат-бот доступным в Teams через портал виртуальных агентов Power и добавить бот в Teams с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-109">This document guides you on how to make your chatbot available in Teams through the Power Virtual Agents portal, and add your bot to Teams using App Studio.</span></span> 

<span data-ttu-id="bcc7f-110">Виртуальные агенты Power позволяют создавать мощные чат-боты, которые могут отвечать на вопросы, заданные вашими клиентами, другими сотрудниками или посетителями веб-сайта или службы.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-110">Power Virtual Agents lets you create powerful chatbots that can answer questions posed by your customers, other employees, or visitors to your website or service.</span></span>

<span data-ttu-id="bcc7f-111">Эти боты могут быть легко созданы без необходимости для ученых или разработчиков данных.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-111">These bots can be created easily without the need for data scientists or developers.</span></span>

> [!NOTE]
> <span data-ttu-id="bcc7f-112">Добавляя чат-бота в Microsoft Teams, некоторые данные, такие как содержимое бота и содержимое пользовательского чата, делятся с Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-112">By adding your chatbot to Microsoft Teams, some of the data, such as bot content and user chat content, is shared with Microsoft Teams.</span></span> <span data-ttu-id="bcc7f-113">Это означает, что ваши данные вытекают за пределы соответствия требованиям организации и [географических или региональных границ.](/power-virtual-agents/data-location)</span><span class="sxs-lookup"><span data-stu-id="bcc7f-113">It means that your data flows outside of your [organization’s compliance and geographic or regional boundaries](/power-virtual-agents/data-location).</span></span> <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a><span data-ttu-id="bcc7f-114">Сделать чат-бот доступным в Teams через портал виртуальных агентов Power</span><span class="sxs-lookup"><span data-stu-id="bcc7f-114">Make your chatbot available in Teams through the Power Virtual Agents portal</span></span>

<span data-ttu-id="bcc7f-115">Чтобы сделать чат-бот доступным в Teams на портале виртуальных агентов Power, необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bcc7f-115">To make your chatbot available in Teams through the Power Virtual Agents portal, you must perform the following process steps:</span></span>

<span data-ttu-id="bcc7f-116">**Чтобы сделать чат-бот доступным в Teams**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-116">**To make the chatbot available in Teams**</span></span>

1. <span data-ttu-id="bcc7f-117">**Публикация последнего контента бота**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-117">**Publish the latest bot content**</span></span>  
<span data-ttu-id="bcc7f-118">После создания чат-бота на портале виртуальных агентов Power необходимо опубликовать бот, прежде чем пользователи Teams смогут взаимодействовать с ним.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-118">After creating a chatbot in the Power Virtual Agents portal, you must publish your bot before Teams users can interact with it.</span></span> <span data-ttu-id="bcc7f-119">Дополнительные сведения см. в [публикации последнего контента бота.](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)</span><span class="sxs-lookup"><span data-stu-id="bcc7f-119">For more information, see [Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span></span>

   ![публикация на портале виртуальных агентов power](../../assets/images/pva-publish.png)

1. <span data-ttu-id="bcc7f-121">**Настройка канала Teams**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-121">**Configure the Teams channel**</span></span>  
<span data-ttu-id="bcc7f-122">После публикации бота добавьте канал Teams, чтобы сделать его доступным для пользователей Teams.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-122">After publishing your bot, add the Teams channel to make the bot available to Teams users.</span></span>

   ![каналы на портале виртуальных агентов power](../../assets/images/pva-channels.png)

1. <span data-ttu-id="bcc7f-124">**Создание ID приложения для чат-бота**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-124">**Generate an App ID for your chatbot**</span></span>  
<span data-ttu-id="bcc7f-125">После добавления канала Teams в чат-бот в диалоговом окне создается **ID** приложения.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-125">After adding the Teams channel to your chatbot, an **App ID** is generated in the dialog box.</span></span> <span data-ttu-id="bcc7f-126">Идентификатор приложения — уникальный идентификатор, созданный Корпорацией Майкрософт для вашего бота.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-126">The App ID is a unique Microsoft generated identifier for your bot.</span></span> <span data-ttu-id="bcc7f-127">Сохраните ID приложения, чтобы создать пакет приложений для Teams.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-127">Save the App ID to create an app package for Teams.</span></span>

## <a name="add-your-bot-to-teams-using-app-studio"></a><span data-ttu-id="bcc7f-128">Добавление бота в Teams с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="bcc7f-128">Add your bot to Teams using App Studio</span></span>

<span data-ttu-id="bcc7f-129">Если [в экземпляре](/microsoftteams/admin-settings) Teams включена загрузка настраиваемой программы, вы можете использовать Teams App Studio для непосредственной загрузки чат-бота и немедленного его использования.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-129">If [uploading custom apps is enabled](/microsoftteams/admin-settings) in your Teams instance, you can use Teams App Studio to directly upload your chatbot and start using it immediately.</span></span> <span data-ttu-id="bcc7f-130">Чтобы поделиться своим чат-ботом, можно попросить администратора сделать бот доступным в каталоге приложений клиента или отправить пакет приложения другим и попросить их самостоятельно загрузить его.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-130">To share your chatbot, you can request your admin to make your bot available in the tenant app catalog or you can send your app package to others and ask them to upload it independently.</span></span>

1. <span data-ttu-id="bcc7f-131">**Установка App Studio в Teams**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-131">**Install App Studio in Teams**</span></span>  
<span data-ttu-id="bcc7f-132">App Studio — это приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-132">App Studio is a Teams app.</span></span> <span data-ttu-id="bcc7f-133">Установка App Studio из магазина Teams, упрощает процесс создания и регистрации ботов в Teams:</span><span class="sxs-lookup"><span data-stu-id="bcc7f-133">Install App Studio from the Teams store that simplifies the process of bot creation and registration in Teams:</span></span> 

   1. <span data-ttu-id="bcc7f-134">Выберите значок магазина приложений из экземпляра Teams и выберите **App Studio.**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-134">Select the app store icon from Teams instance, and search for **App Studio**.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. <span data-ttu-id="bcc7f-135">Выберите **плитку App Studio** и выберите **Установите** в диалоговом окне всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-135">Select the **App Studio** tile and select **Install** in the pop-up dialog box.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. <span data-ttu-id="bcc7f-136">**Создание манифеста приложения Teams в App Studio**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-136">**Create the Teams app manifest in App Studio**</span></span>  
<span data-ttu-id="bcc7f-137">Боты в Teams определяются файлом JSON манифеста приложения, который предоставляет основные сведения о вашем боте и его возможностях.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-137">Bots in Teams are defined by an app manifest JSON file that provides the basic information about your bot and its capabilities.</span></span> <span data-ttu-id="bcc7f-138">В **App Studio** выберите редактор **Манифеста** и **выберите Создание нового приложения.**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-138">In **App Studio**, select **Manifest editor**, and select **Create a new app**.</span></span>  
<span data-ttu-id="bcc7f-139">Ниже приводится руководство по созданию нового приложения в App Studio:</span><span class="sxs-lookup"><span data-stu-id="bcc7f-139">The following image guides you to create a new app in App Studio:</span></span>  

   ![создание нового приложения](../../assets/images/get-started/create-new-app.png)

1. <span data-ttu-id="bcc7f-141">**Добавление сведений о боте**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-141">**Add your bot details**</span></span>  
<span data-ttu-id="bcc7f-142">Выполните все необходимые поля.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-142">Complete all the required fields.</span></span> <span data-ttu-id="bcc7f-143">Полное описание каждого поля см. в определении [схемы манифеста.](../../resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="bcc7f-143">For a full description of each field see [manifest schema definition](../../resources/schema/manifest-schema.md).</span></span>   
<span data-ttu-id="bcc7f-144">Ниже приводится руководство по добавлению сведений о приложении:</span><span class="sxs-lookup"><span data-stu-id="bcc7f-144">The following image guides you to add the app details:</span></span>  

   ![добавление сведений о приложении](../../assets/images/get-started/add-app-details.png)

1. <span data-ttu-id="bcc7f-146">**Настройка бота** Чтобы настроить бот, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bcc7f-146">**Set up your bot** To set-up the bot, perform the following steps:</span></span> 
     1. <span data-ttu-id="bcc7f-147">Откройте **вкладку Bots.**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-147">Open the **Bots** tab.</span></span> 
     1. <span data-ttu-id="bcc7f-148">Выберите **настройка**  >  **существующего бота** и введите имя вашего бота.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-148">Select **Setup** > **Existing bot** and enter the name of your bot.</span></span>

   <span data-ttu-id="bcc7f-149">На следующем изображении вы можете настроить бота:</span><span class="sxs-lookup"><span data-stu-id="bcc7f-149">The following image guides you to set-up a bot:</span></span>    

   ![Настройка бота](../../assets/images/get-started/bot-set-up.png) 

   <span data-ttu-id="bcc7f-151">Ниже приводится руководство по настройкам существующего бота:</span><span class="sxs-lookup"><span data-stu-id="bcc7f-151">The following image guides you to set-up an existing bot:</span></span>      

   ![существующая настройка бота](../../assets/images/get-started/existing-bot-set-up.png)    
1. <span data-ttu-id="bcc7f-153">**Добавление ID приложения**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-153">**Add your App ID**</span></span>  
<span data-ttu-id="bcc7f-154">Чтобы добавить свой ID приложения, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bcc7f-154">To add your App ID, perform the following steps:</span></span>  
    1. <span data-ttu-id="bcc7f-155">Выберите **Подключение к другому бот-ид и** вклеить скопированные ранее **id** приложения.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-155">Select **Connect to a different bot id** and paste the **App Id** you copied earlier.</span></span> 
    1. <span data-ttu-id="bcc7f-156">Выберите **Область личного**  >    >  **сохранения**.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-156">Select **Scope** > **Personal** > **Save**.</span></span>      
<span data-ttu-id="bcc7f-157">Ниже приводится руководство по настройкам существующего бота:</span><span class="sxs-lookup"><span data-stu-id="bcc7f-157">The following image guides you to set-up an existing bot:</span></span>    

   ![добавление id приложения](../../assets/images/get-started/add-app-id.png)

1. <span data-ttu-id="bcc7f-159">**Добавление допустимого домена для бота**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-159">**Add valid domains for your bot**</span></span>  
<span data-ttu-id="bcc7f-160">Этот шаг необходим только в том случае, если бот требует от пользователя войти.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-160">This step is only required if your bot requires the user to sign in.</span></span> <span data-ttu-id="bcc7f-161">Выберите **домены и разрешения** и в поле **Допустимые** домены ввести следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="bcc7f-161">Select **Domains and permissions** and in the **Valid Domains** field, provide the following input:</span></span>

    ```bash
       token.botframework.com
    ```

7.  <span data-ttu-id="bcc7f-162">**Тестирование и распространение бота**</span><span class="sxs-lookup"><span data-stu-id="bcc7f-162">**Test and distribute your bot**</span></span>  
<span data-ttu-id="bcc7f-163">Откройте **тест и раздайте** вкладку и выберите **Установите,** чтобы добавить бот непосредственно в экземпляр Teams.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-163">Open **Test and distribute** tab and select **Install** to add your bot directly to your Teams instance.</span></span> <span data-ttu-id="bcc7f-164">Кроме того, вы можете скачать завершенный пакет приложений для совместной работы с пользователями Teams или предоставить его администратору, чтобы сделать бот доступным в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-164">Alternately, you can download the completed app package to share with Teams users or provide it to your admin to make your bot available in the tenant app catalog.</span></span>

8. <span data-ttu-id="bcc7f-165">**Запуск чата** </span><span class="sxs-lookup"><span data-stu-id="bcc7f-165">**Start a chat** </span></span>  
<span data-ttu-id="bcc7f-166">Процесс настройка для добавления бота чата виртуальных агентов Power в Teams завершен.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-166">The set-up process for adding your Power Virtual Agents chat bot to Teams is complete.</span></span> <span data-ttu-id="bcc7f-167">Теперь вы можете начать беседу с ботом в личном чате.</span><span class="sxs-lookup"><span data-stu-id="bcc7f-167">You can now start a conversation with your bot in a personal chat.</span></span>

## <a name="see-also"></a><span data-ttu-id="bcc7f-168">См. также</span><span class="sxs-lookup"><span data-stu-id="bcc7f-168">See also</span></span>

- [<span data-ttu-id="bcc7f-169">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="bcc7f-169">Power Virtual Agents</span></span>](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  

- <span data-ttu-id="bcc7f-170">[Создание чат-бота для Teams с виртуальными агентами Microsoft Power.](../bot-features.md#bots-and-the-microsoft-power-virtual-agents)</span><span class="sxs-lookup"><span data-stu-id="bcc7f-170">[Create a chatbot for Teams with Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span></span>  

- [<span data-ttu-id="bcc7f-171">Портал Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="bcc7f-171">Power Virtual Agents portal</span></span>](https://powervirtualagents.microsoft.com)

- [<span data-ttu-id="bcc7f-172">Публикация бота виртуальных агентов Power</span><span class="sxs-lookup"><span data-stu-id="bcc7f-172">Publish your Power Virtual Agents bot</span></span>](/power-virtual-agents/publication-fundamentals-publish-channels)

- <span data-ttu-id="bcc7f-173">[Безопасность и соответствие требованиям в Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span><span class="sxs-lookup"><span data-stu-id="bcc7f-173">[Security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span></span>

## <a name="next-step"></a><span data-ttu-id="bcc7f-174">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="bcc7f-174">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bcc7f-175">Создание виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="bcc7f-175">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)

