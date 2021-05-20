---
title: Добавьте Power Virtual Agents чат-бота в Teams
author: laujan
description: интеграция Power Virtual Agents чат-бота в Teams платформу
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 2a8f9c23eaa1acf2555b91cc4caf8d0f3298c114
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566119"
---
# <a name="add-power-virtual-agents-chatbot"></a><span data-ttu-id="fc44d-103">Добавление чатбота Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="fc44d-103">Add Power Virtual Agents chatbot</span></span> 

<span data-ttu-id="fc44d-104">Power Virtual Agents это решение без кода, управляемого графическим интерфейсом, которое позволяет каждому члену вашей команды создавать богатых разговорных чат-ботов, которые легко интегрируются с платформой Teams платформы.</span><span class="sxs-lookup"><span data-stu-id="fc44d-104">Power Virtual Agents is a no-code, guided graphical interface solution that empowers every member of your team to create rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="fc44d-105">Все содержимое, автором Power Virtual Agents, естественно, в Teams.</span><span class="sxs-lookup"><span data-stu-id="fc44d-105">All content authored in Power Virtual Agents renders naturally in Teams.</span></span> <span data-ttu-id="fc44d-106">Power Virtual Agents боты взаимодействуют с пользователями в Teams чате холст.</span><span class="sxs-lookup"><span data-stu-id="fc44d-106">Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="fc44d-107">ИТ-администраторы, бизнес-аналитики, специалисты по доменам и квалифицированные разработчики приложений могут разрабатывать, разрабатывать и публиковать интеллектуальных виртуальных агентов для Teams без настройки среды разработки.</span><span class="sxs-lookup"><span data-stu-id="fc44d-107">The IT administrators, business analysts, domain specialists, and skilled app developers can design, develop, and publish intelligent virtual agents for Teams without having to setup a development environment.</span></span> <span data-ttu-id="fc44d-108">Они могут создать веб-службу или напрямую зарегистрироваться в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="fc44d-108">They can create a web service, or directly register with the Bot Framework.</span></span> 

<span data-ttu-id="fc44d-109">Этот документ поможет вам сделать ваш чат-бот доступным в Teams через портал Power Virtual Agents, и добавить своего бота, чтобы Teams с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="fc44d-109">This document guides you on how to make your chatbot available in Teams through the Power Virtual Agents portal, and add your bot to Teams using App Studio.</span></span> 

<span data-ttu-id="fc44d-110">Power Virtual Agents позволяет создавать мощные чат-боты, которые могут отвечать на вопросы ваших клиентов, других сотрудников или посетителей вашего сайта или службы.</span><span class="sxs-lookup"><span data-stu-id="fc44d-110">Power Virtual Agents lets you create powerful chatbots that can answer questions posed by your customers, other employees, or visitors to your website or service.</span></span>

<span data-ttu-id="fc44d-111">Эти боты могут быть созданы легко без необходимости данных ученых или разработчиков.</span><span class="sxs-lookup"><span data-stu-id="fc44d-111">These bots can be created easily without the need for data scientists or developers.</span></span>

> [!NOTE]
> <span data-ttu-id="fc44d-112">Добавляя чат-бота в Microsoft Teams, некоторые данные, такие как бот-контент и содержимое чата пользователя, совместно Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fc44d-112">By adding your chatbot to Microsoft Teams, some of the data, such as bot content and user chat content, is shared with Microsoft Teams.</span></span> <span data-ttu-id="fc44d-113">Это означает, что ваши данные вытекает за [пределы соответствия требованиям вашей организации и географических или региональных границ.](/power-virtual-agents/data-location)</span><span class="sxs-lookup"><span data-stu-id="fc44d-113">It means that your data flows outside of your [organization’s compliance and geographic or regional boundaries](/power-virtual-agents/data-location).</span></span> <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a><span data-ttu-id="fc44d-114">Сделайте ваш чат-бот Teams в Power Virtual Agents портала</span><span class="sxs-lookup"><span data-stu-id="fc44d-114">Make your chatbot available in Teams through the Power Virtual Agents portal</span></span>

<span data-ttu-id="fc44d-115">Чтобы сделать чат-бота доступным Teams через Power Virtual Agents портал, необходимо выполнить следующие этапы процесса:</span><span class="sxs-lookup"><span data-stu-id="fc44d-115">To make your chatbot available in Teams through the Power Virtual Agents portal, you must perform the following process steps:</span></span>

<span data-ttu-id="fc44d-116">**Чтобы сделать чат-бота доступным в Teams**</span><span class="sxs-lookup"><span data-stu-id="fc44d-116">**To make the chatbot available in Teams**</span></span>

1. <span data-ttu-id="fc44d-117">**Публикация последнего контента бота**</span><span class="sxs-lookup"><span data-stu-id="fc44d-117">**Publish the latest bot content**</span></span>  
<span data-ttu-id="fc44d-118">После создания чат-бота на Power Virtual Agents, вы должны опубликовать свой бот, прежде чем Teams пользователи с ним свяются.</span><span class="sxs-lookup"><span data-stu-id="fc44d-118">After creating a chatbot in the Power Virtual Agents portal, you must publish your bot before Teams users can interact with it.</span></span> <span data-ttu-id="fc44d-119">Для получения дополнительной информации, [см. Публикация последнего содержания бота](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span><span class="sxs-lookup"><span data-stu-id="fc44d-119">For more information, see [Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span></span>

   ![опубликовать в силе виртуальные агенты портала](../../assets/images/pva-publish.png)

1. <span data-ttu-id="fc44d-121">**Настройка Teams канала**</span><span class="sxs-lookup"><span data-stu-id="fc44d-121">**Configure the Teams channel**</span></span>  
<span data-ttu-id="fc44d-122">После публикации бота добавьте Teams, чтобы бот был доступен Teams пользователям.</span><span class="sxs-lookup"><span data-stu-id="fc44d-122">After publishing your bot, add the Teams channel to make the bot available to Teams users.</span></span>

   ![каналы в власти виртуальных агентов портала](../../assets/images/pva-channels.png)

1. <span data-ttu-id="fc44d-124">**Создание идентификатора приложения для чат-бота**</span><span class="sxs-lookup"><span data-stu-id="fc44d-124">**Generate an App ID for your chatbot**</span></span>  
<span data-ttu-id="fc44d-125">После добавления Teams канала в чат-бот в **диалоговом поле** генерируется идентификатор App ID.</span><span class="sxs-lookup"><span data-stu-id="fc44d-125">After adding the Teams channel to your chatbot, an **App ID** is generated in the dialog box.</span></span> <span data-ttu-id="fc44d-126">Идентификатор App ID является уникальным идентификатором, генерируемым корпорацией Майкрософт для вашего бота.</span><span class="sxs-lookup"><span data-stu-id="fc44d-126">The App ID is a unique Microsoft generated identifier for your bot.</span></span> <span data-ttu-id="fc44d-127">Сохраните идентификатор приложения для создания пакета приложений для Teams.</span><span class="sxs-lookup"><span data-stu-id="fc44d-127">Save the App ID to create an app package for Teams.</span></span>

## <a name="add-your-bot-to-teams-using-app-studio"></a><span data-ttu-id="fc44d-128">Добавьте бота в Teams с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="fc44d-128">Add your bot to Teams using App Studio</span></span>

<span data-ttu-id="fc44d-129">Если [загрузка пользовательских приложений включена](/microsoftteams/admin-settings) в вашем Teams, вы можете использовать Teams App Studio, чтобы непосредственно загрузить чат-бота и начать использовать его немедленно.</span><span class="sxs-lookup"><span data-stu-id="fc44d-129">If [uploading custom apps is enabled](/microsoftteams/admin-settings) in your Teams instance, you can use Teams App Studio to directly upload your chatbot and start using it immediately.</span></span> <span data-ttu-id="fc44d-130">Чтобы поделиться своим чат-ботом, вы можете попросить администратора сделать вашего бота доступным в каталоге приложений арендатора или отправить пакет приложений другим и попросить их загрузить его самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="fc44d-130">To share your chatbot, you can request your admin to make your bot available in the tenant app catalog or you can send your app package to others and ask them to upload it independently.</span></span>

1. <span data-ttu-id="fc44d-131">**Установка App Studio в Teams**</span><span class="sxs-lookup"><span data-stu-id="fc44d-131">**Install App Studio in Teams**</span></span>  
<span data-ttu-id="fc44d-132">App Studio является Teams приложением.</span><span class="sxs-lookup"><span data-stu-id="fc44d-132">App Studio is a Teams app.</span></span> <span data-ttu-id="fc44d-133">Установите App Studio из Teams магазина, который упрощает процесс создания и регистрации ботов в Teams:</span><span class="sxs-lookup"><span data-stu-id="fc44d-133">Install App Studio from the Teams store that simplifies the process of bot creation and registration in Teams:</span></span> 

   1. <span data-ttu-id="fc44d-134">Выберите значок магазина приложений из Teams например, и ищите **App Studio.**</span><span class="sxs-lookup"><span data-stu-id="fc44d-134">Select the app store icon from Teams instance, and search for **App Studio**.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. <span data-ttu-id="fc44d-135">Выберите **плитку App Studio** и **выберите Установить** во всплывающем диалоговом поле.</span><span class="sxs-lookup"><span data-stu-id="fc44d-135">Select the **App Studio** tile and select **Install** in the pop-up dialog box.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. <span data-ttu-id="fc44d-136">**Создание Teams в App Studio**</span><span class="sxs-lookup"><span data-stu-id="fc44d-136">**Create the Teams app manifest in App Studio**</span></span>  
<span data-ttu-id="fc44d-137">Боты в Teams определяются файлом JSON, который предоставляет основную информацию о вашем боте и его возможностях.</span><span class="sxs-lookup"><span data-stu-id="fc44d-137">Bots in Teams are defined by an app manifest JSON file that provides the basic information about your bot and its capabilities.</span></span> <span data-ttu-id="fc44d-138">В **App Studio** выберите редактора **Manifest** и выберите **Создать новое приложение.**</span><span class="sxs-lookup"><span data-stu-id="fc44d-138">In **App Studio**, select **Manifest editor**, and select **Create a new app**.</span></span>

    ![создать новое приложение](../../assets/images/get-started/create-new-app.png)

1. <span data-ttu-id="fc44d-140">**Добавьте данные о боте**</span><span class="sxs-lookup"><span data-stu-id="fc44d-140">**Add your bot details**</span></span>  
<span data-ttu-id="fc44d-141">Выполните все необходимые поля.</span><span class="sxs-lookup"><span data-stu-id="fc44d-141">Complete all the required fields.</span></span> <span data-ttu-id="fc44d-142">Для полного описания каждого [](../../resources/schema/manifest-schema.md)поля см.</span><span class="sxs-lookup"><span data-stu-id="fc44d-142">For a full description of each field see [manifest schema definition](../../resources/schema/manifest-schema.md).</span></span>

    ![добавить детали приложения](../../assets/images/get-started/add-app-details.png)

1. <span data-ttu-id="fc44d-144">**Настройка бота** Чтобы настроить бота, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="fc44d-144">**Set up your bot** To set-up the bot, perform the following steps:</span></span> 
     1. <span data-ttu-id="fc44d-145">Откройте **вкладку Bots.**</span><span class="sxs-lookup"><span data-stu-id="fc44d-145">Open the **Bots** tab.</span></span> 
     1. <span data-ttu-id="fc44d-146">Выберите **Setup**  >  **Existing bot** и введите имя вашего бота.</span><span class="sxs-lookup"><span data-stu-id="fc44d-146">Select **Setup** > **Existing bot** and enter the name of your bot.</span></span>

   ![Настройка бота](../../assets/images/get-started/bot-set-up.png) 

   <span data-ttu-id="fc44d-148">На следующем изображении помесят, как настроить существующего бота:</span><span class="sxs-lookup"><span data-stu-id="fc44d-148">The following image depicts how to set-up an existing bot:</span></span>      

   ![существующая настройка бота](../../assets/images/get-started/existing-bot-set-up.png)
       
1. <span data-ttu-id="fc44d-150">**Добавить идентификатор приложения**</span><span class="sxs-lookup"><span data-stu-id="fc44d-150">**Add your App ID**</span></span>  
<span data-ttu-id="fc44d-151">Чтобы добавить идентификатор App ID, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="fc44d-151">To add your App ID, perform the following steps:</span></span>  
    1. <span data-ttu-id="fc44d-152">Выберите **Подключение другому идентификатору бота и** вставьте App **Id, который** вы скопировали ранее.</span><span class="sxs-lookup"><span data-stu-id="fc44d-152">Select **Connect to a different bot id** and paste the **App Id** you copied earlier.</span></span> 
    1. <span data-ttu-id="fc44d-153">Выберите **область**  >  **личного**  >  **сохранения**.</span><span class="sxs-lookup"><span data-stu-id="fc44d-153">Select **Scope** > **Personal** > **Save**.</span></span>

    ![добавить идентификатор приложения](../../assets/images/get-started/add-app-id.png)

1. <span data-ttu-id="fc44d-155">**Добавление действительных доменов для вашего бота**</span><span class="sxs-lookup"><span data-stu-id="fc44d-155">**Add valid domains for your bot**</span></span>  
<span data-ttu-id="fc44d-156">Этот шаг необходим только в том случае, если ваш бот требует от пользователя войти в компьютер.</span><span class="sxs-lookup"><span data-stu-id="fc44d-156">This step is only required if your bot requires the user to sign in.</span></span> <span data-ttu-id="fc44d-157">Выберите **домены и разрешения,** а также в **поле действительных доменов,** предоставьте следующие входные данные:</span><span class="sxs-lookup"><span data-stu-id="fc44d-157">Select **Domains and permissions** and in the **Valid Domains** field, provide the following input:</span></span>

    ```bash
       token.botframework.com
    ```

1. <span data-ttu-id="fc44d-158">**Тестирование и распространение бота**</span><span class="sxs-lookup"><span data-stu-id="fc44d-158">**Test and distribute your bot**</span></span>  
<span data-ttu-id="fc44d-159">Откройте **тест и распределите** вкладку **и выберите Установить,** чтобы добавить ваш бот непосредственно к Teams например.</span><span class="sxs-lookup"><span data-stu-id="fc44d-159">Open **Test and distribute** tab and select **Install** to add your bot directly to your Teams instance.</span></span> <span data-ttu-id="fc44d-160">Кроме того, вы можете скачать завершенный пакет приложений, чтобы поделиться с Teams пользователями или предоставить его администратору, чтобы сделать ваш бот доступен в каталоге приложений арендатора.</span><span class="sxs-lookup"><span data-stu-id="fc44d-160">Alternately, you can download the completed app package to share with Teams users or provide it to your admin to make your bot available in the tenant app catalog.</span></span>

1. <span data-ttu-id="fc44d-161">**Начало чата** </span><span class="sxs-lookup"><span data-stu-id="fc44d-161">**Start a chat** </span></span>  
<span data-ttu-id="fc44d-162">Процесс настройки для добавления вашего чат-Power Virtual Agents в Teams завершен.</span><span class="sxs-lookup"><span data-stu-id="fc44d-162">The set-up process for adding your Power Virtual Agents chat bot to Teams is complete.</span></span> <span data-ttu-id="fc44d-163">Теперь вы можете начать разговор с ботом в личном чате.</span><span class="sxs-lookup"><span data-stu-id="fc44d-163">You can now start a conversation with your bot in a personal chat.</span></span>

## <a name="see-also"></a><span data-ttu-id="fc44d-164">См. также</span><span class="sxs-lookup"><span data-stu-id="fc44d-164">See also</span></span>

- [<span data-ttu-id="fc44d-165">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="fc44d-165">Power Virtual Agents</span></span>](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  

- <span data-ttu-id="fc44d-166">[Создайте чат-бот для Teams с Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span><span class="sxs-lookup"><span data-stu-id="fc44d-166">[Create a chatbot for Teams with Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span></span>  

- [<span data-ttu-id="fc44d-167">Power Virtual Agents портал</span><span class="sxs-lookup"><span data-stu-id="fc44d-167">Power Virtual Agents portal</span></span>](https://powervirtualagents.microsoft.com)

- [<span data-ttu-id="fc44d-168">Опубликовать свой Power Virtual Agents бот</span><span class="sxs-lookup"><span data-stu-id="fc44d-168">Publish your Power Virtual Agents bot</span></span>](/power-virtual-agents/publication-fundamentals-publish-channels)

- <span data-ttu-id="fc44d-169">[Безопасность и соблюдение в Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span><span class="sxs-lookup"><span data-stu-id="fc44d-169">[Security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span></span>

## <a name="next-step"></a><span data-ttu-id="fc44d-170">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="fc44d-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc44d-171">Создание виртуального помощника</span><span class="sxs-lookup"><span data-stu-id="fc44d-171">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)

