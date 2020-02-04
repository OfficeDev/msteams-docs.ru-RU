---
title: Справочные материалы по проектированию
description: Описывает рекомендации по проектированию личного приложения
keywords: рекомендации по проектированию Teams Справочник по платформам личные приложения
ms.openlocfilehash: 6a07b618d78a3ad79850713052c88ef178c1ecc1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675240"
---
# <a name="personal-apps"></a><span data-ttu-id="ceace-104">Персональные приложения</span><span class="sxs-lookup"><span data-stu-id="ceace-104">Personal apps</span></span>

> [!Important]
> <span data-ttu-id="ceace-105">Скоро будет доступна полная поддержка вкладок на мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="ceace-105">Full support for tabs on mobile clients is coming soon.</span></span> <span data-ttu-id="ceace-106">Чтобы подготовиться к этому изменению, следуйте [указаниям для вкладок на странице Mobile](~/tabs/design/tabs-mobile.md) при создании вкладок.</span><span class="sxs-lookup"><span data-stu-id="ceace-106">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="ceace-107">В настоящее время персональные приложения (статические вкладки) доступны в [предварительной версии для разработчиков](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="ceace-107">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="ceace-108">Когда будет выпущена полная поддержка вкладок:</span><span class="sxs-lookup"><span data-stu-id="ceace-108">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="ceace-109">Все вкладки всегда будут доступны на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="ceace-109">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="ceace-110">Вы `contentUrl` **будете загружены в клиенте Mobile Teams**.</span><span class="sxs-lookup"><span data-stu-id="ceace-110">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="ceace-111">Для вкладок каналов и групп пользователи по-прежнему могут открывать вкладку в отдельном браузере `websiteUrl`, но при этом `contentUrl` будут загружаться первыми.</span><span class="sxs-lookup"><span data-stu-id="ceace-111">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>

<span data-ttu-id="ceace-112">Личное приложение — это приложение с личной областью.</span><span class="sxs-lookup"><span data-stu-id="ceace-112">A personal app is an app with a personal scope.</span></span> <span data-ttu-id="ceace-113">Разработчик приложения может предоставить версию своего приложения, созданную для отдельного пользователя.</span><span class="sxs-lookup"><span data-stu-id="ceace-113">As an app developer, you have the option to provide a version of your app that is built for the individual user.</span></span> <span data-ttu-id="ceace-114">В этой версии Коллекция вкладок (и Bot, если вы включили их), предназначена для этого человека.</span><span class="sxs-lookup"><span data-stu-id="ceace-114">In this version, the collection of tabs (and the bot, if you've included one), are designed for the person.</span></span> <span data-ttu-id="ceace-115">Таким образом вы можете создать взаимодействие с пользователями по одному пользователю.</span><span class="sxs-lookup"><span data-stu-id="ceace-115">This way, you're able to create a one-on-one interaction with your users.</span></span>

<span data-ttu-id="ceace-116">Личное приложение может просматривать все содержимое и все элементы, которые недавно просматривали в приложении.</span><span class="sxs-lookup"><span data-stu-id="ceace-116">A personal app is where someone can see everything that's theirs, and all the items they've recently viewed in the app.</span></span> <span data-ttu-id="ceace-117">Все содержимое размещается в одном месте.</span><span class="sxs-lookup"><span data-stu-id="ceace-117">It puts everything in one place.</span></span> <span data-ttu-id="ceace-118">На следующем снимке экрана Contoso — личное приложение в всплывающем меню личных приложений.</span><span class="sxs-lookup"><span data-stu-id="ceace-118">In the following screenshot, Contoso is a personal app in the personal app flyout.</span></span>

![изображение меню переполнения приложения](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a><span data-ttu-id="ceace-120">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="ceace-120">Guidelines</span></span>

<span data-ttu-id="ceace-121">Личное приложение обычно содержит следующие вкладки:</span><span class="sxs-lookup"><span data-stu-id="ceace-121">A personal app typically contains the following tabs:</span></span>

### <a name="your-tab"></a><span data-ttu-id="ceace-122">Вкладка</span><span class="sxs-lookup"><span data-stu-id="ceace-122">Your tab</span></span>

<span data-ttu-id="ceace-123">Именно здесь пользователи увидят все свои материалы.</span><span class="sxs-lookup"><span data-stu-id="ceace-123">This is where your users will see all their stuff.</span></span> <span data-ttu-id="ceace-124">Это личное место.</span><span class="sxs-lookup"><span data-stu-id="ceace-124">It's their personal space.</span></span> <span data-ttu-id="ceace-125">Вкладка может быть упорядочена в виде списка, сетки, столбцов или одного холста... все, что лучше всего подходит для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ceace-125">The tab can be arranged as a list, a grid, columns, or a single canvas...whatever works best for your application.</span></span> <span data-ttu-id="ceace-126">Дополнительные сведения о проектировании эффективных вкладок: [конструктор вкладок (~/табс/Десигн/Табс.МД).</span><span class="sxs-lookup"><span data-stu-id="ceace-126">For additional information on designing effective tabs see: [Tabs design(~/tabs/design/tabs.md).</span></span>

<span data-ttu-id="ceace-127">Так как на этой вкладке могут отображаться элементы из нескольких каналов, каждый из них должен отображать свою группу, канал и вкладку, чтобы пользователь мог легко понять, где она была создана.</span><span class="sxs-lookup"><span data-stu-id="ceace-127">Since this tab can show items from multiple channels, each item should display its own team, channel, and tab so the user can easily see where it originated.</span></span>

![Вкладка личных задач](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a><span data-ttu-id="ceace-129">Последних</span><span class="sxs-lookup"><span data-stu-id="ceace-129">Recent</span></span>

<span data-ttu-id="ceace-130">Вкладка " **последние** " позволяет пользователям просматривать все, что недавно просматривалось в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="ceace-130">The **Recent** tab lets someone browse everything they've recently viewed in your app.</span></span> <span data-ttu-id="ceace-131">Он указан в хронологическом порядке (от наиболее частого к наиболее позднему).</span><span class="sxs-lookup"><span data-stu-id="ceace-131">It's listed in chronological order (from most to least recent).</span></span> <span data-ttu-id="ceace-132">При выборе элемента в этом списке пользователь переходит к каналу и вкладке этого элемента.</span><span class="sxs-lookup"><span data-stu-id="ceace-132">Clicking on an item in this list will navigate the user to that item's channel and tab.</span></span>

![Вкладка "последние"](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a><span data-ttu-id="ceace-134">Все</span><span class="sxs-lookup"><span data-stu-id="ceace-134">All</span></span>

<span data-ttu-id="ceace-135">Это список всех вкладок в организации пользователя (у тех, у которых есть доступ к ним, в любом случае).</span><span class="sxs-lookup"><span data-stu-id="ceace-135">This is a list of all your tabs in the person's organization (the ones they have access to, anyway).</span></span> <span data-ttu-id="ceace-136">Другими словами, в нем отображаются все, что используется в приложении.</span><span class="sxs-lookup"><span data-stu-id="ceace-136">In other words, it shows them everywhere the app is being used.</span></span> <span data-ttu-id="ceace-137">Как и на вкладке " **последние** ", при выборе какого-либо элемента списка пользователь будет непосредственно на соответствующем канале и на вкладке.</span><span class="sxs-lookup"><span data-stu-id="ceace-137">As with the **Recent** tab, selecting something in the list will bring the user straight to the relevant channel and tab.</span></span>

### <a name="bot"></a><span data-ttu-id="ceace-138">Bot</span><span class="sxs-lookup"><span data-stu-id="ceace-138">Bot</span></span>

<span data-ttu-id="ceace-139">Он не требуется, но это отличный способ общаться с пользователями напрямую и лично.</span><span class="sxs-lookup"><span data-stu-id="ceace-139">A bot isn't required, but it's a great way to communicate directly and privately with your users.</span></span> <span data-ttu-id="ceace-140">Уведомление является одной из наиболее важных функций личного приложения и как лучше уведомлять о прямой связи?</span><span class="sxs-lookup"><span data-stu-id="ceace-140">Notification is one of the most important functions of a personal app, and what better way to notify than with direct communication?</span></span>

<span data-ttu-id="ceace-141">Боты доставлять сообщения в виде карточек, которые могут содержать определенные сведения (например, оповещение о доступности нового контента) или большое количество обновлений (например, для ежедневного списка дел).</span><span class="sxs-lookup"><span data-stu-id="ceace-141">Bots deliver messages in the form of cards, which can provide specific information (like an alert that new content is available) or broad updates (like a daily to-do list).</span></span> <span data-ttu-id="ceace-142">Дополнительные сведения о проектировании эффективных Боты: [Bot-дизайн (~/Ботс/Десигн/Ботс.МД).</span><span class="sxs-lookup"><span data-stu-id="ceace-142">For additional information on designing effective bots see: [Bot design(~/bots/design/bots.md).</span></span>

![Приветствие в Bot](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a><span data-ttu-id="ceace-144">Справка и параметры</span><span class="sxs-lookup"><span data-stu-id="ceace-144">Help and Settings</span></span>

<span data-ttu-id="ceace-145">Контент справки позволяет пользователям находить особенности своего приложения.</span><span class="sxs-lookup"><span data-stu-id="ceace-145">Help content enables users to discover the nuances of your app.</span></span> <span data-ttu-id="ceace-146">Добавьте вкладку **Параметры** , чтобы предоставить им возможность дальнейшей настройки.</span><span class="sxs-lookup"><span data-stu-id="ceace-146">Add a **Settings** tab to give them the ability to further customize it.</span></span>

### <a name="about"></a><span data-ttu-id="ceace-147">О программе</span><span class="sxs-lookup"><span data-stu-id="ceace-147">About</span></span>

<span data-ttu-id="ceace-148">Включение вкладки " **о программе** " для предоставления таких сведений, как номер версии, возможности, конфиденциальность и ссылки на разрешения.</span><span class="sxs-lookup"><span data-stu-id="ceace-148">Include an **About** tab to provide information like version number, capabilities, privacy, and permissions links.</span></span>

## <a name="best-practices"></a><span data-ttu-id="ceace-149">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="ceace-149">Best practices</span></span>

### <a name="communicate-directly-with-your-users"></a><span data-ttu-id="ceace-150">Непосредственное взаимодействие с пользователями</span><span class="sxs-lookup"><span data-stu-id="ceace-150">Communicate directly with your users</span></span>

<span data-ttu-id="ceace-151">Используйте Bot для уведомления пользователей об изменениях и новых возможностях.</span><span class="sxs-lookup"><span data-stu-id="ceace-151">Use a bot to notify users of changes and new features.</span></span>

### <a name="customize-your-tabs"></a><span data-ttu-id="ceace-152">Настройка вкладок...</span><span class="sxs-lookup"><span data-stu-id="ceace-152">Customize your tabs...</span></span>

<span data-ttu-id="ceace-153">Вы можете добавить другие вкладки, которые помогут пользователям выполнять определенные задачи.</span><span class="sxs-lookup"><span data-stu-id="ceace-153">Feel free to add other tabs that will help your users accomplish specific tasks.</span></span>

### <a name="and-make-them-relevant-to-every-user"></a><span data-ttu-id="ceace-154">... и сделайте их релевантными для каждого пользователя</span><span class="sxs-lookup"><span data-stu-id="ceace-154">...and make them relevant to every user</span></span>

<span data-ttu-id="ceace-155">Все вкладки, объявляемые в манифесте приложения, будут видны всем пользователям.</span><span class="sxs-lookup"><span data-stu-id="ceace-155">Every tab you declare in your app manifest will be visible to all users.</span></span> <span data-ttu-id="ceace-156">Например, если личное приложение является средством составления отчетов о расходах, которое используется обоими руководителями и сотрудниками, вкладка **утверждения** должна предоставлять содержимое, которое является значимым для обеих ролей.</span><span class="sxs-lookup"><span data-stu-id="ceace-156">For example, if your personal app is an expense reporting tool that is used by both managers and employees, an **Approval** tab should provide content that is meaningful to both roles.</span></span>
