---
title: Справочные материалы по проектированию
description: Описывает рекомендации по проектированию личного приложения
keywords: рекомендации по проектированию Teams Справочник по платформам личные приложения
ms.openlocfilehash: f66691234149afa56a6753dd51379c9f2355318e
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455501"
---
# <a name="personal-apps"></a><span data-ttu-id="1ea7a-104">Персональные приложения</span><span class="sxs-lookup"><span data-stu-id="1ea7a-104">Personal apps</span></span>

> [!NOTE]
> <span data-ttu-id="1ea7a-105">Полная поддержка вкладок на мобильных клиентах поддерживается в Teams.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-105">Full support for tabs on mobile clients is supported in Teams.</span></span> <span data-ttu-id="1ea7a-106">При создании вкладок для мобильных платформ следуйте [рекомендациям по использованию вкладок на мобильных устройствах](../../tabs/design/tabs-mobile.md) .</span><span class="sxs-lookup"><span data-stu-id="1ea7a-106">You should follow the [guidance for tabs on mobile](../../tabs/design/tabs-mobile.md) when creating tabs for mobile platforms.</span></span>

<span data-ttu-id="1ea7a-107">Личное приложение — это приложение Teams с личной областью.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-107">A personal app is a Teams application with a personal scope.</span></span>  <span data-ttu-id="1ea7a-108">Разработчик приложения может предоставить версию приложения, которая специализируется на взаимодействии с одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-108">As an app developer, you have the option to provide a version of your app that focuses on interactions with a single user.</span></span> <span data-ttu-id="1ea7a-109">Он может быть участником [Bot](../../bots/what-are-bots.md) для общения в беседах "один к одному" с пользователем или [личной вкладкой](../../tabs/what-are-tabs.md) , предоставляющей встроенный веб-интерфейс.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-109">It can be a [conversational bot](../../bots/what-are-bots.md) to engage in one-to-one conversations with a user or a [personal tab](../../tabs/what-are-tabs.md) providing an embedded web experience.</span></span> <span data-ttu-id="1ea7a-110">Персональные приложения позволяют пользователям просматривать их содержимое в одном месте.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-110">Personal apps enable users to view their select content in one place.</span></span> <span data-ttu-id="1ea7a-111">На следующем снимке экрана Contoso — личное приложение в всплывающем меню личных приложений.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-111">In the following screenshot, Contoso is a personal app in the personal app flyout.</span></span>

![изображение меню переполнения приложения](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a><span data-ttu-id="1ea7a-113">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="1ea7a-113">Guidelines</span></span>

<span data-ttu-id="1ea7a-114">Личное приложение обычно содержит следующие вкладки:</span><span class="sxs-lookup"><span data-stu-id="1ea7a-114">A personal app typically contains the following tabs:</span></span>

### <a name="your-tab"></a><span data-ttu-id="1ea7a-115">Вкладка</span><span class="sxs-lookup"><span data-stu-id="1ea7a-115">Your tab</span></span>

<span data-ttu-id="1ea7a-116">Именно здесь пользователи увидят все свои материалы.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-116">This is where your users will see all their stuff.</span></span> <span data-ttu-id="1ea7a-117">Это личное место.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-117">It's their personal space.</span></span> <span data-ttu-id="1ea7a-118">Вкладка может быть упорядочена в виде списка, сетки, столбцов или одного холста... все, что лучше всего подходит для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-118">The tab can be arranged as a list, a grid, columns, or a single canvas...whatever works best for your application.</span></span> <span data-ttu-id="1ea7a-119">Дополнительную информацию по проектированию эффективных вкладок можно узнать в статье [создание вкладок](../../tabs/design/tabs.md).</span><span class="sxs-lookup"><span data-stu-id="1ea7a-119">For additional information on designing effective tabs see: [Tabs design](../../tabs/design/tabs.md).</span></span>

<span data-ttu-id="1ea7a-120">Так как на этой вкладке могут отображаться элементы из нескольких каналов, каждый из них должен отображать свою группу, канал и вкладку, чтобы пользователь мог легко понять, где она была создана.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-120">Since this tab can show items from multiple channels, each item should display its own team, channel, and tab so the user can easily see where it originated.</span></span>

![Вкладка личных задач](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a><span data-ttu-id="1ea7a-122">Последних</span><span class="sxs-lookup"><span data-stu-id="1ea7a-122">Recent</span></span>

<span data-ttu-id="1ea7a-123">Вкладка " **последние** " позволяет пользователям просматривать все, что недавно просматривалось в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-123">The **Recent** tab lets someone browse everything they've recently viewed in your app.</span></span> <span data-ttu-id="1ea7a-124">Он указан в хронологическом порядке (от наиболее частого к наиболее позднему).</span><span class="sxs-lookup"><span data-stu-id="1ea7a-124">It's listed in chronological order (from most to least recent).</span></span> <span data-ttu-id="1ea7a-125">При выборе элемента в этом списке пользователь переходит к каналу и вкладке этого элемента.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-125">Clicking on an item in this list will navigate the user to that item's channel and tab.</span></span>

![Вкладка "последние"](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a><span data-ttu-id="1ea7a-127">Все</span><span class="sxs-lookup"><span data-stu-id="1ea7a-127">All</span></span>

<span data-ttu-id="1ea7a-128">Это список всех вкладок в организации пользователя (у тех, у которых есть доступ к ним, в любом случае).</span><span class="sxs-lookup"><span data-stu-id="1ea7a-128">This is a list of all your tabs in the person's organization (the ones they have access to, anyway).</span></span> <span data-ttu-id="1ea7a-129">Другими словами, в нем отображаются все, что используется в приложении.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-129">In other words, it shows them everywhere the app is being used.</span></span> <span data-ttu-id="1ea7a-130">Как и на вкладке " **последние** ", при выборе какого-либо элемента списка пользователь будет непосредственно на соответствующем канале и на вкладке.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-130">As with the **Recent** tab, selecting something in the list will bring the user straight to the relevant channel and tab.</span></span>

### <a name="bot"></a><span data-ttu-id="1ea7a-131">Bot</span><span class="sxs-lookup"><span data-stu-id="1ea7a-131">Bot</span></span>

<span data-ttu-id="1ea7a-132">Он не требуется, но это отличный способ общаться с пользователями напрямую и лично.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-132">A bot isn't required, but it's a great way to communicate directly and privately with your users.</span></span> <span data-ttu-id="1ea7a-133">Уведомление является одной из наиболее важных функций личного приложения и как лучше уведомлять о прямой связи?</span><span class="sxs-lookup"><span data-stu-id="1ea7a-133">Notification is one of the most important functions of a personal app, and what better way to notify than with direct communication?</span></span>

<span data-ttu-id="1ea7a-134">Боты доставлять сообщения в виде карточек, которые могут содержать определенные сведения (например, оповещение о доступности нового контента) или большое количество обновлений (например, для ежедневного списка дел).</span><span class="sxs-lookup"><span data-stu-id="1ea7a-134">Bots deliver messages in the form of cards, which can provide specific information (like an alert that new content is available) or broad updates (like a daily to-do list).</span></span> <span data-ttu-id="1ea7a-135">Дополнительные сведения о проектировании эффективных Боты: [Bot Design](../../bots/design/bots.md).</span><span class="sxs-lookup"><span data-stu-id="1ea7a-135">For additional information on designing effective bots see: [Bot design](../../bots/design/bots.md).</span></span>

![Приветствие в Bot](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a><span data-ttu-id="1ea7a-137">Справка и параметры</span><span class="sxs-lookup"><span data-stu-id="1ea7a-137">Help and Settings</span></span>

<span data-ttu-id="1ea7a-138">Контент справки позволяет пользователям находить особенности своего приложения.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-138">Help content enables users to discover the nuances of your app.</span></span> <span data-ttu-id="1ea7a-139">Добавьте вкладку **Параметры** , чтобы предоставить им возможность дальнейшей настройки.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-139">Add a **Settings** tab to give them the ability to further customize it.</span></span>

### <a name="about"></a><span data-ttu-id="1ea7a-140">О программе</span><span class="sxs-lookup"><span data-stu-id="1ea7a-140">About</span></span>

<span data-ttu-id="1ea7a-141">Включение вкладки " **о программе** " для предоставления таких сведений, как номер версии, возможности, конфиденциальность и ссылки на разрешения.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-141">Include an **About** tab to provide information like version number, capabilities, privacy, and permissions links.</span></span>

## <a name="best-practices"></a><span data-ttu-id="1ea7a-142">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="1ea7a-142">Best practices</span></span>

### <a name="communicate-directly-with-your-users"></a><span data-ttu-id="1ea7a-143">Непосредственное взаимодействие с пользователями</span><span class="sxs-lookup"><span data-stu-id="1ea7a-143">Communicate directly with your users</span></span>

<span data-ttu-id="1ea7a-144">Используйте Bot для уведомления пользователей об изменениях и новых возможностях.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-144">Use a bot to notify users of changes and new features.</span></span>

### <a name="customize-your-tabs"></a><span data-ttu-id="1ea7a-145">Настройка вкладок...</span><span class="sxs-lookup"><span data-stu-id="1ea7a-145">Customize your tabs...</span></span>

<span data-ttu-id="1ea7a-146">Вы можете добавить другие вкладки, которые помогут пользователям выполнять определенные задачи.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-146">Feel free to add other tabs that will help your users accomplish specific tasks.</span></span>

### <a name="and-make-them-relevant-to-every-user"></a><span data-ttu-id="1ea7a-147">... и сделайте их релевантными для каждого пользователя</span><span class="sxs-lookup"><span data-stu-id="1ea7a-147">...and make them relevant to every user</span></span>

<span data-ttu-id="1ea7a-148">Все вкладки, объявляемые в манифесте приложения, будут видны всем пользователям.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-148">Every tab you declare in your app manifest will be visible to all users.</span></span> <span data-ttu-id="1ea7a-149">Например, если личное приложение является средством составления отчетов о расходах, которое используется обоими руководителями и сотрудниками, вкладка **утверждения** должна предоставлять содержимое, которое является значимым для обеих ролей.</span><span class="sxs-lookup"><span data-stu-id="1ea7a-149">For example, if your personal app is an expense reporting tool that is used by both managers and employees, an **Approval** tab should provide content that is meaningful to both roles.</span></span>
