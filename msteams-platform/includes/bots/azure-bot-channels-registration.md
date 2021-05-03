---
title: Регистрация канала бота Azure
description: описывает каналы ботов Azure для регистрации
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta12
ms.openlocfilehash: 3cbbd204daf98f1c3528dcb6efcfde299a402912
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020951"
---
1. <span data-ttu-id="3e05f-103">На [портале Azure](https://ms.portal.azure.com/#home)в рамках служб Azure выберите **Создание ресурса.**</span><span class="sxs-lookup"><span data-stu-id="3e05f-103">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select **Create a resource**.</span></span>
1. <span data-ttu-id="3e05f-104">В поле поиска введите "бот".</span><span class="sxs-lookup"><span data-stu-id="3e05f-104">In the search box enter "bot".</span></span> <span data-ttu-id="3e05f-105">А в выпадаемом списке выберите **регистрацию каналов бота.**</span><span class="sxs-lookup"><span data-stu-id="3e05f-105">And in the drop-down list, select **Bot Channels Registration**.</span></span>
1. <span data-ttu-id="3e05f-106">Выберите **кнопку Создать.**</span><span class="sxs-lookup"><span data-stu-id="3e05f-106">Select the **Create** button.</span></span>
1. <span data-ttu-id="3e05f-107">В **лезвии регистрации канала** бота укайте запрашиваемую информацию о боте.</span><span class="sxs-lookup"><span data-stu-id="3e05f-107">In the **Bot Channel Registration** blade, provide the requested information about your bot.</span></span>
1. <span data-ttu-id="3e05f-108">Оставьте **конечную точку обмена** сообщениями пустой, после развертывания бота введите необходимый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3e05f-108">Leave the **Messaging endpoint** box empty for now, you will enter the required URL after deploying the bot.</span></span> <span data-ttu-id="3e05f-109">На следующем рисунке показан пример параметров регистрации:</span><span class="sxs-lookup"><span data-stu-id="3e05f-109">The following picture shows an example of the registration settings:</span></span>

    ![Регистрация каналов бот-приложений](../../assets/images/authentication/auth-bot-channels-registration.png)

1. <span data-ttu-id="3e05f-111">Нажмите **кнопку Microsoft App ID и пароль,** а затем **создайте новые**.</span><span class="sxs-lookup"><span data-stu-id="3e05f-111">Click **Microsoft App ID and password** and then **Create New**.</span></span>

    <span data-ttu-id="3e05f-112">![Создание ID приложения Microsoft ](../../assets/images/authentication/CreateMicrosoftAppID.png) ![ Create New Microsoft App ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span><span class="sxs-lookup"><span data-stu-id="3e05f-112">![Create Microsoft App ID](../../assets/images/authentication/CreateMicrosoftAppID.png) ![Create New Microsoft App ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span></span>    

1. <span data-ttu-id="3e05f-113">Щелкните **Создать ID приложения в ссылке Портал регистрации** приложений.</span><span class="sxs-lookup"><span data-stu-id="3e05f-113">Click **Create App ID in the App Registration Portal** link.</span></span>

   ![Регистрация приложения](../../assets/images/authentication/AppRegistration.png)
   
1. <span data-ttu-id="3e05f-115">В отображаемом **окне регистрации Приложения** щелкните **вкладку Новая регистрация** в верхнем левом окне.</span><span class="sxs-lookup"><span data-stu-id="3e05f-115">In the displayed **App registration** window, click the **New registration** tab in the upper left.</span></span>
1. <span data-ttu-id="3e05f-116">Введите имя приложения-бота, которое вы регистрируете, мы использовали *BotTeamsAuth* (необходимо выбрать свое уникальное имя).</span><span class="sxs-lookup"><span data-stu-id="3e05f-116">Enter the name of the bot application you are registering, we used *BotTeamsAuth* (you need to select your own unique name).</span></span>
1. <span data-ttu-id="3e05f-117">Для  поддерживаемых типов учетных записей выберите учетные записи в любом организационном каталоге (любой каталог *Azure AD - Multitenant)* и личных учетных записях Майкрософт (например, Skype, Xbox).</span><span class="sxs-lookup"><span data-stu-id="3e05f-117">For the **Supported account types** select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
1. <span data-ttu-id="3e05f-118">Нажмите **кнопку Регистрация.**</span><span class="sxs-lookup"><span data-stu-id="3e05f-118">Click the **Register** button.</span></span> <span data-ttu-id="3e05f-119">После завершения Azure отображает *страницу Обзор* для приложения.</span><span class="sxs-lookup"><span data-stu-id="3e05f-119">Once completed, Azure displays the *Overview* page for the application.</span></span>
1. <span data-ttu-id="3e05f-120">Скопируйте и сохраните в **файле значение ID приложения (клиента).**</span><span class="sxs-lookup"><span data-stu-id="3e05f-120">Copy and save to a file the **Application (client) ID** value.</span></span>
1. <span data-ttu-id="3e05f-121">В левой панели щелкните **Сертификат и секреты**.</span><span class="sxs-lookup"><span data-stu-id="3e05f-121">In the left panel, click **Certificate and secrets**.</span></span>
    1. <span data-ttu-id="3e05f-122">В *соответствии с секретами клиента* нажмите **кнопку Новый секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="3e05f-122">Under *Client secrets*, click **New client secret**.</span></span>
    1. <span data-ttu-id="3e05f-123">Добавьте описание, чтобы определить этот секрет от других пользователей, которые необходимо создать для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="3e05f-123">Add a description to identify this secret from others you might need to create for this app.</span></span>
    1. <span data-ttu-id="3e05f-124">Срок *действия набора истекает* в выборе.</span><span class="sxs-lookup"><span data-stu-id="3e05f-124">Set *Expires* to your selection.</span></span>
    1. <span data-ttu-id="3e05f-125">Нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3e05f-125">Click **Add**.</span></span>
    1. <span data-ttu-id="3e05f-126">Скопируйте секрет клиента и сохраните его в файле.</span><span class="sxs-lookup"><span data-stu-id="3e05f-126">Copy the client secret and save it to a file.</span></span>
1. <span data-ttu-id="3e05f-127">Возвращайся  к окну регистрации канала ботов и скопируйте код приложения и секрет клиента в полях **Microsoft App ID** и **Password** соответственно.  </span><span class="sxs-lookup"><span data-stu-id="3e05f-127">Go back to the **Bot Channel Registration** window and copy the *App ID* and the *Client secret* in the **Microsoft App ID** and **Password** boxes, respectively.</span></span>
1. <span data-ttu-id="3e05f-128">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3e05f-128">Click **OK**.</span></span>
1. <span data-ttu-id="3e05f-129">Наконец, нажмите **кнопку Создать**.</span><span class="sxs-lookup"><span data-stu-id="3e05f-129">Finally, click **Create**.</span></span>

<span data-ttu-id="3e05f-130">После создания ресурса регистрации Azure он будет включен в список групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3e05f-130">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![группа регистрации каналов бот-приложений](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

<span data-ttu-id="3e05f-132">После создания регистрации каналов бота необходимо включить Teams канал.</span><span class="sxs-lookup"><span data-stu-id="3e05f-132">Once your bot channels registration is created, you'll need to enable the Teams channel.</span></span>

1. <span data-ttu-id="3e05f-133">На [портале Azure](https://ms.portal.azure.com/#home)в службе  Azure выберите только что созданную регистрацию бот-каналов.</span><span class="sxs-lookup"><span data-stu-id="3e05f-133">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select the **Bot Channel Registration** you just created.</span></span>
1. <span data-ttu-id="3e05f-134">В левой панели щелкните **Каналы**.</span><span class="sxs-lookup"><span data-stu-id="3e05f-134">In the left panel, click **Channels**.</span></span>
1. <span data-ttu-id="3e05f-135">Щелкните значок Microsoft Teams, а затем выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3e05f-135">Click the Microsoft Teams icon, then choose **Save**.</span></span>
