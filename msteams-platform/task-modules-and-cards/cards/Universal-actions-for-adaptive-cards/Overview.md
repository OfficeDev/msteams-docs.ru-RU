---
title: Обзор универсальных действий для адаптивных карт
description: Краткий обзор универсальных действий для адаптивных карт.
ms.topic: overview
localization_priority: Normal
ms.openlocfilehash: f0adf3d1a01262ff9cbdf14128c9ffe088ae8072
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088916"
---
# <a name="universal-actions-for-adaptive-cards"></a><span data-ttu-id="09b25-103">Универсальные действия для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="09b25-103">Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="09b25-104">Универсальные действия для адаптивных карт развивались из отзывов разработчиков о том, что, несмотря на универсальность макета и отрисовки для адаптивных карт, обработка действий не была.</span><span class="sxs-lookup"><span data-stu-id="09b25-104">Universal Actions for Adaptive Cards evolved from developer feedback that even though layout and rendering for Adaptive Cards was universal, action handling was not.</span></span> <span data-ttu-id="09b25-105">Даже если разработчик хотел отправить ту же карточку в разные места, он должен обрабатывать действия по-другому.</span><span class="sxs-lookup"><span data-stu-id="09b25-105">Even if a developer wanted to send the same card to different places, they have to handle actions differently.</span></span>

<span data-ttu-id="09b25-106">Универсальные действия для адаптивных карт приносят боту в качестве общей задней части для обработки действий и вводят новый тип действий, который работает в приложениях, таких как `Action.Execute` Teams и Outlook.</span><span class="sxs-lookup"><span data-stu-id="09b25-106">Universal Actions for Adaptive Cards brings the bot as the common backend for handling actions and introduces a new action type, `Action.Execute`, which works across apps, such as Teams and Outlook.</span></span>

<span data-ttu-id="09b25-107">Этот документ поможет вам понять, как можно использовать модель Universal Actions для улучшения взаимодействия пользователей с адаптивными картами на платформах и приложениях.</span><span class="sxs-lookup"><span data-stu-id="09b25-107">This document helps you to understand how you can use Universal Actions model to enhance user experience of interacting with Adaptive Cards across platforms and applications.</span></span>

> [!NOTE]
> <span data-ttu-id="09b25-108">Поддержка универсальных действий для адаптивных карт доступна только для карт, отправленных ботом.</span><span class="sxs-lookup"><span data-stu-id="09b25-108">Support for Universal Actions for Adaptive Cards is only available for cards sent by bot.</span></span> <span data-ttu-id="09b25-109">Поддержка карт, отправленных через окне составить и ссылку unfurling карт скоро.</span><span class="sxs-lookup"><span data-stu-id="09b25-109">Support for cards sent through compose box and link unfurling cards is coming soon.</span></span>

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="09b25-110">Расширение пользовательских интерфейсов с помощью универсальных действий для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="09b25-110">Enhance user experiences with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="09b25-111">Универсальные действия для адаптивных карт улучшают пользовательский интерфейс, включив следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="09b25-111">Universal Actions for Adaptive Cards enhances user experience by enabling the following scenarios:</span></span>

* [<span data-ttu-id="09b25-112">Универсальные действия</span><span class="sxs-lookup"><span data-stu-id="09b25-112">Universal Actions</span></span>](#universal-actions)
* [<span data-ttu-id="09b25-113">Пользовательские представления</span><span class="sxs-lookup"><span data-stu-id="09b25-113">User Specific Views</span></span>](#user-specific-views)
* [<span data-ttu-id="09b25-114">Поддержка последовательного рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="09b25-114">Sequential Workflow support</span></span>](#sequential-workflow-support)
* [<span data-ttu-id="09b25-115">Просмотры на сегодняшний день</span><span class="sxs-lookup"><span data-stu-id="09b25-115">Up to date views</span></span>](#up-to-date-views)

### <a name="universal-actions"></a><span data-ttu-id="09b25-116">Универсальные действия</span><span class="sxs-lookup"><span data-stu-id="09b25-116">Universal Actions</span></span>

<span data-ttu-id="09b25-117">Перед универсальными действиями для адаптивных карт различные хосты предоставляли различные модели действий следующим образом:</span><span class="sxs-lookup"><span data-stu-id="09b25-117">Before the Universal Actions for Adaptive Cards, different hosts provided different action models as follows:</span></span>

* <span data-ttu-id="09b25-118">Teams или используемые боты , подход, который отоносят фактическую модель связи `Action.Submit` к основному каналу.</span><span class="sxs-lookup"><span data-stu-id="09b25-118">Teams or bots used `Action.Submit`, an approach which defers the actual communication model to the underlying channel.</span></span>
* <span data-ttu-id="09b25-119">Outlook `Action.Http` для связи со службой backend, явно указанной в полезной нагрузке адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="09b25-119">Outlook used `Action.Http` to communicate with the backend service explicitly specified in the Adaptive Card payload.</span></span>

<span data-ttu-id="09b25-120">На следующем изображении показана текущая несогласованная модель действий:</span><span class="sxs-lookup"><span data-stu-id="09b25-120">The following image shows the current inconsistent action model:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="Несогласованная модель действий":::

<span data-ttu-id="09b25-122">С помощью универсальных действий для адаптивных карт можно использовать для обработки действий `Action.Execute` на разных платформах.</span><span class="sxs-lookup"><span data-stu-id="09b25-122">With the Universal Actions for Adaptive Cards, you can use `Action.Execute` for action handling across different platforms.</span></span> <span data-ttu-id="09b25-123">`Action.Execute`работает через концентраторы, включая Teams и Outlook.</span><span class="sxs-lookup"><span data-stu-id="09b25-123">`Action.Execute` works across hubs including Teams and Outlook.</span></span> <span data-ttu-id="09b25-124">Кроме того, адаптивная карта может быть возвращена в качестве ответа на `Action.Execute` срабатываемом запросе на вызов.</span><span class="sxs-lookup"><span data-stu-id="09b25-124">In addition, an Adaptive Card can be returned as response for an `Action.Execute` triggered invoke request.</span></span>

<span data-ttu-id="09b25-125">На следующем изображении показана новая модель Universal Action:</span><span class="sxs-lookup"><span data-stu-id="09b25-125">The following image shows the new Universal Action model:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="Новые универсальные действия для адаптивных карт":::

<span data-ttu-id="09b25-127">Теперь вы можете отправить ту же карту как Teams, так и Outlook и синхронизировать их друг с другом с помощью бота.</span><span class="sxs-lookup"><span data-stu-id="09b25-127">You can now send the same card to both, Teams and Outlook, and keep them in sync with each other using the underlying bot.</span></span> <span data-ttu-id="09b25-128">Любое действие, принятое на любой платформе, отражается на другой с помощью этой сборки один *раз,* развертывать в любом месте (универсальные действия для адаптивных карт) модели.</span><span class="sxs-lookup"><span data-stu-id="09b25-128">Any action taken on either platform is reflected to the other with this *build once, deploy anywhere* (Universal Actions for Adaptive Cards) model.</span></span>

<span data-ttu-id="09b25-129">На следующем изображении показаны универсальные действия для адаптивных карт как для Teams, так и для Outlook:</span><span class="sxs-lookup"><span data-stu-id="09b25-129">The following image depicts the Universal Actions for Adaptive Cards for both Teams and Outlook:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="Та же Teams и Outlook":::

### <a name="user-specific-views"></a><span data-ttu-id="09b25-131">Пользовательские представления</span><span class="sxs-lookup"><span data-stu-id="09b25-131">User Specific Views</span></span>

<span data-ttu-id="09b25-132">Сегодня каждый пользователь в Teams или канале видит одно и то же представление и действия кнопки на адаптивной карте.</span><span class="sxs-lookup"><span data-stu-id="09b25-132">Today every user in the Teams chat or channel sees the exact same view and button actions on the Adaptive Card.</span></span> <span data-ttu-id="09b25-133">Однако в некоторых сценариях для некоторых пользователей существует требование действовать по-другому и иметь доступ к различным сведениям в одном чате или канале.</span><span class="sxs-lookup"><span data-stu-id="09b25-133">However, in certain scenarios there is a requirement for certain users to act differently and have access to different information within the same chat or channel.</span></span>

<span data-ttu-id="09b25-134">Например, если вы отправляете карточку отчетов об инцидентах в чате или канале, только пользователь, которому назначен инцидент, должен видеть кнопку **Разрешить.**</span><span class="sxs-lookup"><span data-stu-id="09b25-134">For example, if you send an incident reporting card in a chat or channel, only the user who is assigned the incident must see a **Resolve** button.</span></span> <span data-ttu-id="09b25-135">С другой стороны, создатель инцидента должен видеть кнопку **Изменить,** а все остальные пользователи должны иметь возможность просматривать только сведения об инциденте.</span><span class="sxs-lookup"><span data-stu-id="09b25-135">On the other hand, the incident creator must see an **Edit** button and all other users must only be able to view details of the incident.</span></span> <span data-ttu-id="09b25-136">Это можно сделать с помощью пользовательских представлений, включенных `refresh` свойством.</span><span class="sxs-lookup"><span data-stu-id="09b25-136">This is made possible by User Specific Views that is enabled by the `refresh` property.</span></span>

<span data-ttu-id="09b25-137">На следующем изображении показан пример расширения обмена сообщениями по билетам (ME), на котором различным пользователям в чате показаны различные действия, основанные на требовании:</span><span class="sxs-lookup"><span data-stu-id="09b25-137">The following image shows an example of a ticketing messaging extension (ME) where different users in the chat are shown different actions based on the requirement:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Пользовательские представления":::

<span data-ttu-id="09b25-139">Дополнительные сведения см. [в примере для пользовательских представлений.](User-Specific-Views.md)</span><span class="sxs-lookup"><span data-stu-id="09b25-139">For more information, see [sample for User Specific Views](User-Specific-Views.md).</span></span>

### <a name="sequential-workflow-support"></a><span data-ttu-id="09b25-140">Поддержка последовательного рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="09b25-140">Sequential Workflow support</span></span>

<span data-ttu-id="09b25-141">С поддержкой последовательного рабочего процесса пользователи могут проходить через ряд процессов, не отправляя разные карты отдельно.</span><span class="sxs-lookup"><span data-stu-id="09b25-141">With Sequential Workflow support, users can progress through a series of workflows without sending different cards separately.</span></span> <span data-ttu-id="09b25-142">Это возможно благодаря возможности возврата адаптивной карты в ответ `Action.Execute` на действие.</span><span class="sxs-lookup"><span data-stu-id="09b25-142">This is made possible by the ability of `Action.Execute` to return an Adaptive Card in response to an action.</span></span> <span data-ttu-id="09b25-143">Кроме того, любой пользователь в чате или канале может пройти через рабочий процесс без изменения карты для других пользователей в чате.</span><span class="sxs-lookup"><span data-stu-id="09b25-143">Also, any user in the chat or channel can progress through their workflow without modifying the card for other users in the chat.</span></span>

<span data-ttu-id="09b25-144">На следующем изображении иллюстрируется пример бота для заказа продуктов питания:</span><span class="sxs-lookup"><span data-stu-id="09b25-144">The following image illustrates a food ordering bot example:</span></span> <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="09b25-145">На следующем изображении показаны различные состояния для разных пользователей в чате или канале:</span><span class="sxs-lookup"><span data-stu-id="09b25-145">The following image shows the various states for different users in the chat or channel:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Состояния бота кейтеринга":::

<span data-ttu-id="09b25-147">Дополнительные сведения см. [в примере последовательного](Sequential-Workflows.md)рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="09b25-147">For more information, see [sample for Sequential Workflow](Sequential-Workflows.md).</span></span>

### <a name="up-to-date-views"></a><span data-ttu-id="09b25-148">Просмотры на сегодняшний день</span><span class="sxs-lookup"><span data-stu-id="09b25-148">Up to date views</span></span>

<span data-ttu-id="09b25-149">Можно создавать адаптивные карты, которые обновляются автоматически.</span><span class="sxs-lookup"><span data-stu-id="09b25-149">You can create Adaptive Cards that update automatically.</span></span> <span data-ttu-id="09b25-150">Например, это может быть запрос на утверждение, отправленный пользователем.</span><span class="sxs-lookup"><span data-stu-id="09b25-150">For example, it can be an approval request sent by a user.</span></span> <span data-ttu-id="09b25-151">После утверждения карта должна автоматически отображать сведения о времени утверждения запроса и о том, кто его одобрил.</span><span class="sxs-lookup"><span data-stu-id="09b25-151">After approval, the card must automatically display details about the request approval time and who approved the request.</span></span> <span data-ttu-id="09b25-152">Модель обновления позволяет предоставлять такие обновленные представления.</span><span class="sxs-lookup"><span data-stu-id="09b25-152">The refresh model enables you to provide such up to date views.</span></span> <span data-ttu-id="09b25-153">На следующем изображении показан многоэтапный поток утверждения и показаны представления для разных пользователей.</span><span class="sxs-lookup"><span data-stu-id="09b25-153">The following image shows a multi-step approval flow and how the views for different users is shown.</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="В курсе конкретных представлений пользователей":::

<span data-ttu-id="09b25-155">Дополнительные сведения см. [в примере для просмотра на сегодняшний день.](Up-To-Date-Views.md)</span><span class="sxs-lookup"><span data-stu-id="09b25-155">For more information, see [sample for up to date views](Up-To-Date-Views.md).</span></span>

<span data-ttu-id="09b25-156">Теперь вы можете понять, как можно преобразовать адаптивные карты с помощью новой модели универсальных действий, чтобы обеспечить уникальный и расширенный пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="09b25-156">Now, you can understand how Adaptive Cards can be transformed with the new Universal Actions model to provide a unique and enhanced user experience.</span></span>

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a><span data-ttu-id="09b25-157">Адаптивные карты и новая модель универсальных действий</span><span class="sxs-lookup"><span data-stu-id="09b25-157">Adaptive Cards and the new Universal Actions model</span></span>

<span data-ttu-id="09b25-158">Адаптивные карты — это сочетание контента, например текста и графики, и действий, которые может выполнять пользователь.</span><span class="sxs-lookup"><span data-stu-id="09b25-158">Adaptive Cards are a combination of content, such as text and graphics, and actions that can be performed by a user.</span></span> <span data-ttu-id="09b25-159">Дополнительные сведения см. в [дополнительных сведениях в адаптивных картах.](http://adaptivecards.io/)</span><span class="sxs-lookup"><span data-stu-id="09b25-159">For more information, see [Adaptive Cards](http://adaptivecards.io/).</span></span> <span data-ttu-id="09b25-160">Новые универсальные действия для адаптивных карт обеспечивают общую обработку действий адаптивной карты на платформах и приложениях.</span><span class="sxs-lookup"><span data-stu-id="09b25-160">The new Universal Actions for Adaptive Cards enables a common handling of the Adaptive Card actions across platforms and applications.</span></span> <span data-ttu-id="09b25-161">Дополнительные сведения см. в [универсальной модели действий.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model)</span><span class="sxs-lookup"><span data-stu-id="09b25-161">For more information, see [Universal Action Model](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model).</span></span>

<span data-ttu-id="09b25-162">[Работа с документом Универсальные](Work-with-universal-actions-for-adaptive-cards.md) действия для адаптивных карт проходит через шаги, чтобы использовать возможности универсальных действий для адаптивных карт для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="09b25-162">[Work with Universal Actions for Adaptive Cards](Work-with-universal-actions-for-adaptive-cards.md) document takes you through the steps to use the capabilities of Universal Actions for Adaptive Cards for your solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="09b25-163">См. также</span><span class="sxs-lookup"><span data-stu-id="09b25-163">See also</span></span>

* [<span data-ttu-id="09b25-164">Что такое боты</span><span class="sxs-lookup"><span data-stu-id="09b25-164">What are bots</span></span>](~/bots/what-are-bots.md)
* [<span data-ttu-id="09b25-165">Обзор адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="09b25-165">Adaptive Cards overview</span></span>](~/task-modules-and-cards/what-are-cards.md)
* [<span data-ttu-id="09b25-166">Адаптивные карты @ Microsoft Build 2020</span><span class="sxs-lookup"><span data-stu-id="09b25-166">Adaptive Cards @ Microsoft Build 2020</span></span>](https://youtu.be/hEBhwB72Qn4?t=1393)
* [<span data-ttu-id="09b25-167">Адаптивные карты @ Ignite 2020</span><span class="sxs-lookup"><span data-stu-id="09b25-167">Adaptive Cards @ Ignite 2020</span></span>](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)

## <a name="next-step"></a><span data-ttu-id="09b25-168">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="09b25-168">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09b25-169">Работа с универсальными действиями для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="09b25-169">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
