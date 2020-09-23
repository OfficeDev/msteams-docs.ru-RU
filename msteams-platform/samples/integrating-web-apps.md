---
author: heath-hamilton
description: Рекомендации по интеграции существующих веб-приложений с Microsoft Teams
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: Интеграция веб-приложения с Microsoft Teams
ms.openlocfilehash: e7d4f74526f7a71fe33d5a70d9ed60be960adefc
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210356"
---
# <a name="integrate-web-apps-with-teams"></a><span data-ttu-id="7e3a3-103">Интеграция веб-приложений с Teams</span><span class="sxs-lookup"><span data-stu-id="7e3a3-103">Integrate web apps with Teams</span></span>

<span data-ttu-id="7e3a3-104">Есть ли у вас веб-приложение, которое вы думаете, естественно с социальными функциями Teams и функциями совместной работы?</span><span class="sxs-lookup"><span data-stu-id="7e3a3-104">Do you have a web app you think would fit naturally with Teams' social and collaborative features?</span></span> <span data-ttu-id="7e3a3-105">Эти рекомендации помогут вам разобрались с интеграцией следующих типов приложений:</span><span class="sxs-lookup"><span data-stu-id="7e3a3-105">These guidelines can help you understand how to integrate the following types of apps:</span></span>

* <span data-ttu-id="7e3a3-106">**Автономные приложения**: может быть одностраничное приложение или большое, сложное приложение, в котором пользователи должны использовать некоторые аспекты в Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-106">**Standalone apps**: Could be a single-page app or large, complex app you want people to use some aspects of in Teams.</span></span>
* <span data-ttu-id="7e3a3-107">**Приложения для совместной работы**: приложение, уже созданное для социальных сетей и функций совместной работы, присущих Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-107">**Collaboration apps**: An app already built for the social and collaborative features inherent to Teams.</span></span>
* <span data-ttu-id="7e3a3-108">**SharePoint**: страница SharePoint, которую вы хотите использовать в Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-108">**SharePoint**: A SharePoint page you want to surface in Teams.</span></span>

<span data-ttu-id="7e3a3-109">Для каждого руководства можно узнать, применяется ли он к сценарию интеграции.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-109">For each guideline, you can see if it's applicable to your integration scenario.</span></span>

## <a name="get-to-know-teams-platform-capabilities"></a><span data-ttu-id="7e3a3-110">Знакомство с возможностями платформы Teams</span><span class="sxs-lookup"><span data-stu-id="7e3a3-110">Get to know Teams platform capabilities</span></span>

<span data-ttu-id="7e3a3-111">\***Сценарии интеграции**: автономные приложения, приложения для совместной работы, SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="7e3a3-111">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="7e3a3-112">Ваше приложение Teams может включать в себя возможности, которые пользователи хотят и могут ожидать при совместной работе, но вы можете быть незнакомы с терминологией разработки Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-112">Your Teams app can include features users want and might expect when collaborating, but you may be unfamiliar with Teams development terminology.</span></span>

|<span data-ttu-id="7e3a3-113">Общие функции приложений</span><span class="sxs-lookup"><span data-stu-id="7e3a3-113">Common app features</span></span>   |<span data-ttu-id="7e3a3-114">Возможности платформы Teams</span><span class="sxs-lookup"><span data-stu-id="7e3a3-114">Teams platform capabilities</span></span>   |
|----------|-----------|
|<span data-ttu-id="7e3a3-115">Внедренная веб-страница, Домашняя страница или вебвиев</span><span class="sxs-lookup"><span data-stu-id="7e3a3-115">Embedded webpage, homepage, or webview</span></span>  |[<span data-ttu-id="7e3a3-116">Tabs</span><span class="sxs-lookup"><span data-stu-id="7e3a3-116">Tabs</span></span>](../tabs/what-are-tabs.md)  |
|<span data-ttu-id="7e3a3-117">Совместное использование ярлыков и расширений</span><span class="sxs-lookup"><span data-stu-id="7e3a3-117">Share shortcuts and extensions</span></span>  |[<span data-ttu-id="7e3a3-118">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="7e3a3-118">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="7e3a3-119">Ярлыки действий и расширения</span><span class="sxs-lookup"><span data-stu-id="7e3a3-119">Action shortcuts and extensions</span></span>  |[<span data-ttu-id="7e3a3-120">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="7e3a3-120">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="7e3a3-121">чатботс</span><span class="sxs-lookup"><span data-stu-id="7e3a3-121">Chatbots</span></span>  |[<span data-ttu-id="7e3a3-122">Боты</span><span class="sxs-lookup"><span data-stu-id="7e3a3-122">Bots</span></span>](../bots/what-are-bots.md) |
|<span data-ttu-id="7e3a3-123">Уведомления канала</span><span class="sxs-lookup"><span data-stu-id="7e3a3-123">Channel notifications</span></span>  |[<span data-ttu-id="7e3a3-124">Боты</span><span class="sxs-lookup"><span data-stu-id="7e3a3-124">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="7e3a3-125">Входящие веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="7e3a3-125">Incoming webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[<span data-ttu-id="7e3a3-126">Соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="7e3a3-126">Office 365 Connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="7e3a3-127">Внешние службы сообщений</span><span class="sxs-lookup"><span data-stu-id="7e3a3-127">Message external services</span></span>  |[<span data-ttu-id="7e3a3-128">Боты</span><span class="sxs-lookup"><span data-stu-id="7e3a3-128">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="7e3a3-129">Исходящие веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="7e3a3-129">Outgoing webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="7e3a3-130">Оверлеи</span><span class="sxs-lookup"><span data-stu-id="7e3a3-130">Modals</span></span>  |[<span data-ttu-id="7e3a3-131">Модули задач</span><span class="sxs-lookup"><span data-stu-id="7e3a3-131">Task modules</span></span>](../task-modules-and-cards/what-are-task-modules.md)  |
|<span data-ttu-id="7e3a3-132">Карточки с широким содержимым</span><span class="sxs-lookup"><span data-stu-id="7e3a3-132">Content-rich cards</span></span>  |[<span data-ttu-id="7e3a3-133">Адаптивные карточки</span><span class="sxs-lookup"><span data-stu-id="7e3a3-133">Adaptive Cards</span></span>](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a><span data-ttu-id="7e3a3-134">Определение подмножества функциональных возможностей</span><span class="sxs-lookup"><span data-stu-id="7e3a3-134">Determine a subset of functionality</span></span>

<span data-ttu-id="7e3a3-135">\***Сценарии интеграции**: автономные приложения \*</span><span class="sxs-lookup"><span data-stu-id="7e3a3-135">\***Integration scenarios**: Standalone apps\*</span></span>

<span data-ttu-id="7e3a3-136">Интеграция всех функций существующего приложения в Teams часто приводит к форсированному или неестественному пользовательскому интерфейсу, особенно в больших приложениях.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-136">Integrating all features of an existing application into Teams often leads to a forced or unnatural user experience, particularly in larger apps.</span></span> <span data-ttu-id="7e3a3-137">Рекомендуется начать с самых затронутых функций и тем, которые будут более естественным образом взаимодействовать с Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-137">Consider starting with the most impactful features and those that will integrate more naturally with Teams.</span></span> <span data-ttu-id="7e3a3-138">Помните, что вы можете всегда разрешить пользователям запускать основное приложение и получать доступ к полному набору компонентов.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-138">Remember, you can always allow users to launch the main app and access its full set of features.</span></span>

<span data-ttu-id="7e3a3-139">Прежде чем приступить к работе, выполните некоторые действия по планированию приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-139">Before you begin any technical work, do some planning for your Teams app:</span></span>

1. <span data-ttu-id="7e3a3-140">[Сопоставьте варианты использования приложения с возможностями платформы Teams](../concepts/design/map-use-cases.md).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-140">[Map your app's use cases to Teams platform capabilities](../concepts/design/map-use-cases.md).</span></span>
1. <span data-ttu-id="7e3a3-141">[Определите точки входа приложения](../concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-141">[Determine your app's entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="7e3a3-142">Используется ли для личного использования, совместной работы или для одновременного использования?</span><span class="sxs-lookup"><span data-stu-id="7e3a3-142">Is it for personal use, collaboration, or both?</span></span>

## <a name="understand-sharepoint-requirements-and-options"></a><span data-ttu-id="7e3a3-143">Общие сведения о требованиях и возможностях SharePoint</span><span class="sxs-lookup"><span data-stu-id="7e3a3-143">Understand SharePoint requirements and options</span></span>

<span data-ttu-id="7e3a3-144">\***Сценарии интеграции**: SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="7e3a3-144">\***Integration scenarios**: SharePoint\*</span></span>

<span data-ttu-id="7e3a3-145">Вы можете интегрировать существующую [страницу SharePoint](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) в качестве вкладки групп. Помните о следующем:</span><span class="sxs-lookup"><span data-stu-id="7e3a3-145">You can integrate an existing [SharePoint page](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) as a Teams tab. Remember the following:</span></span>

* <span data-ttu-id="7e3a3-146">Это должна быть *современная* страница SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="7e3a3-146">It must be a *modern* SharePoint Online page</span></span>
* <span data-ttu-id="7e3a3-147">Поддерживаются только личные вкладки (вы не можете интегрировать страницу в качестве вкладки канала)</span><span class="sxs-lookup"><span data-stu-id="7e3a3-147">Only personal tabs are supported (you can't integrate your page as a channel tab)</span></span>

<span data-ttu-id="7e3a3-148">Кроме того, вы можете создать вкладку Teams [с помощью SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-148">Alternatively, you can build a Teams tab [using the SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction).</span></span>

## <a name="aim-towards-multi-tenancy"></a><span data-ttu-id="7e3a3-149">Цель для поддержки нескольких клиентов</span><span class="sxs-lookup"><span data-stu-id="7e3a3-149">Aim towards multi-tenancy</span></span>

<span data-ttu-id="7e3a3-150">\***Сценарии интеграции**: автономные приложения, приложения для совместной работы, SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="7e3a3-150">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="7e3a3-151">Если ваше приложение используется несколькими организациями, подумайте о размещении нескольких клиентов, которое сделает продукт масштабируемым и значительно упростит распространение.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-151">If your app is used by multiple organizations, consider multi-tenant hosting that would make your product scalable and greatly simplify distribution.</span></span>

## <a name="review-your-apis"></a><span data-ttu-id="7e3a3-152">Обзор интерфейсов API</span><span class="sxs-lookup"><span data-stu-id="7e3a3-152">Review your APIs</span></span>

<span data-ttu-id="7e3a3-153">\***Сценарии интеграции**: автономные приложения, приложения для совместной работы \*</span><span class="sxs-lookup"><span data-stu-id="7e3a3-153">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="7e3a3-154">Не думайте, что существующие API и структуры данных приложения полностью поддерживают приложение при интеграции с Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-154">Don't assume your app's existing APIs and data structures fully support the app when integrated with Teams.</span></span> <span data-ttu-id="7e3a3-155">Вам может потребоваться расширить их с помощью контекстных сведений о Teams для [сопоставления удостоверений](../concepts/authentication/configure-identity-provider.md), [поддержки глубокого связывания](../concepts/build-and-test/deep-links.md)и [включения Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-155">You might need to augment these with contextual information about Teams for [identity mapping](../concepts/authentication/configure-identity-provider.md), [deep-link support](../concepts/build-and-test/deep-links.md), and [incorporating Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="7e3a3-156">Узнайте больше о том, как получить контекст для [вкладки](../tabs/how-to/access-teams-context.md) Teams или [ленты](../bots/how-to/get-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-156">Learn more about getting context for your Teams [tab](../tabs/how-to/access-teams-context.md) or [bot](../bots/how-to/get-teams-context.md).</span></span>

## <a name="understand-authentication-options"></a><span data-ttu-id="7e3a3-157">Общие сведения о параметрах аутентификации</span><span class="sxs-lookup"><span data-stu-id="7e3a3-157">Understand authentication options</span></span>

<span data-ttu-id="7e3a3-158">\***Сценарии интеграции**: автономные приложения, приложения для совместной работы, SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="7e3a3-158">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="7e3a3-159">Azure Active Directory (AD) — это поставщик удостоверений для Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-159">Azure Active Directory (AD) is the identity provider for Teams.</span></span> <span data-ttu-id="7e3a3-160">Если ваше приложение использует другого поставщика удостоверений, необходимо либо выполнить сопоставление удостоверений, либо создать федерацию с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-160">If your app uses a different identity provider, you must either do an identity mapping exercise or federate with Azure AD.</span></span>

<span data-ttu-id="7e3a3-161">В Teams есть механизмы единого входа (SSO) с Azure AD для сторонних приложений и рекомендации по потокам проверки подлинности для других поставщиков удостоверений с использованием таких стандартов, как OAuth и Connect ID Connect (ОИДК).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-161">Teams has single sign-on (SSO) mechanisms with Azure AD for third-party apps and guidance for authentication flows to other identity providers using standards such as OAuth and Open ID Connect (OIDC).</span></span>

<span data-ttu-id="7e3a3-162">Для страниц SharePoint вы можете использовать только единый вход и не можете добавить другой идентификатор Azure AD, если вы хотите, чтобы единый вход работал для другого приложения (так как идентификатор является приложением SharePoint).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-162">For SharePoint pages, you can only use SSO and can't add another Azure AD ID if you want SSO to work for another app (since the ID is the SharePoint app).</span></span>

<span data-ttu-id="7e3a3-163">Узнайте больше о [проверке подлинности в Teams](../concepts/authentication/authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-163">Learn more about [authentication in Teams](../concepts/authentication/authentication.md).</span></span>

## <a name="follow-teams-design-guidelines"></a><span data-ttu-id="7e3a3-164">Следуйте рекомендациям по проектированию Teams</span><span class="sxs-lookup"><span data-stu-id="7e3a3-164">Follow Teams design guidelines</span></span>

<span data-ttu-id="7e3a3-165">\***Сценарии интеграции**: автономные приложения, приложения для совместной работы \*</span><span class="sxs-lookup"><span data-stu-id="7e3a3-165">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="7e3a3-166">В общем случае ваше приложение должно быть естественным в Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-166">In general, your app should feel natural in Teams.</span></span> <span data-ttu-id="7e3a3-167">Вы можете подумать о переносе существующего контента приложения на вкладку Teams достаточно, но мы настоятельно рекомендуем использовать приложение в соответствии с [рекомендациями по проектированию Teams](../concepts/design/understand-use-cases.md).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-167">You might think migrating existing app content to a Teams tab is sufficient, but we strongly recommend your app follows [Teams design guidelines](../concepts/design/understand-use-cases.md).</span></span> <span data-ttu-id="7e3a3-168">См. также: [система дизайна Fluent](https://fluentsite.z22.web.core.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-168">See also: [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).</span></span>

## <a name="maximize-deep-linking"></a><span data-ttu-id="7e3a3-169">Максимально развернуть глубокое связывание</span><span class="sxs-lookup"><span data-stu-id="7e3a3-169">Maximize deep linking</span></span>

<span data-ttu-id="7e3a3-170">\***Сценарии интеграции**: автономные приложения, приложения для совместной работы, SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="7e3a3-170">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="7e3a3-171">Практически все в Teams можно связать напрямую с [детальной ссылкой](../concepts/build-and-test/deep-links.md).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-171">Almost everything in Teams can be linked to directly with a [deep link](../concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="7e3a3-172">Ваше приложение должно максимизировать их использование, в том числе ссылки на определенные сообщения и содержимое вкладок.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-172">Your app should maximize use of these, including linking to and from specific messages and tab content.</span></span> <span data-ttu-id="7e3a3-173">С помощью глубоких ссылок можно на самом деле объединить несколько частей приложения для более простой работы в Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-173">Deep links can really tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="be-smart-when-messaging-users"></a><span data-ttu-id="7e3a3-174">Смарт-теги при почтовых пользователях</span><span class="sxs-lookup"><span data-stu-id="7e3a3-174">Be smart when messaging users</span></span>

<span data-ttu-id="7e3a3-175">\***Сценарии интеграции**: автономные приложения, приложения для совместной работы, SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="7e3a3-175">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="7e3a3-176">Обратите внимание на типы сообщений, которые приложение Teams может отправить сейчас и в долгосрочной перспективе.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-176">Consider the types of messages your Teams app might send now and in the long term.</span></span> <span data-ttu-id="7e3a3-177">Если вы считаете, что у вашего приложения когда-либо Многопотоковая беседа, [она может предоставить](../bots/what-are-bots.md) более гибкие возможности, чем веб- [перехватчик](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-177">If you think your app will ever have a multi-threaded conversation, a [bot](../bots/what-are-bots.md) might offer more flexibility than a [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

<span data-ttu-id="7e3a3-178">Боты также позволяет отправлять *Активные сообщения* отдельным пользователям или каналам.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-178">Bots also allow you to send *proactive messages* to individual users or channels.</span></span> <span data-ttu-id="7e3a3-179">Это сообщения без приглашения, вызванные выходом внешнего события, а не сообщением, отправляемым в Bot.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-179">These are unprompted messages triggered by an outside event and not a message sent to a bot.</span></span> <span data-ttu-id="7e3a3-180">(Например, вы можете отправить приветственное сообщение, когда оно установлено или новый пользователь присоединяется к каналу.)</span><span class="sxs-lookup"><span data-stu-id="7e3a3-180">(For example, your bot can send a welcome message when it's installed or a new user joins a channel.)</span></span> 

<span data-ttu-id="7e3a3-181">Для отправки упреждающих сообщений требуются идентификаторы, зависящие от Teams — вы можете записать эти сведения, выполнив [Извлечение списков или данных профилей пользователей](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile), [подписываться на события бесед](../bots/how-to/conversations/subscribe-to-conversation-events.md)или используя [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging).</span><span class="sxs-lookup"><span data-stu-id="7e3a3-181">Sending proactive messages requires Teams-specific identifiers—you can capture this information by [fetching roster or user profile data](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile), [subscribing to conversation events](../bots/how-to/conversations/subscribe-to-conversation-events.md), or using [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging).</span></span>

<span data-ttu-id="7e3a3-182">Следите за тем, чтобы пользователи с чрезмерными нежелательными сообщениями.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-182">Be careful not to spam users with excessive messages.</span></span> <span data-ttu-id="7e3a3-183">Если поддержка Teams поддерживается, рассмотрите возможность предоставления пользователям возможности настраивать параметры уведомлений для приложения (например, "не отправлять неприглашенные сообщения").</span><span class="sxs-lookup"><span data-stu-id="7e3a3-183">If the Teams capability supports it, consider letting users configure notification settings for your app (for example, "Don't send me unprompted messages.").</span></span>

## <a name="use-sharepoint-for-file-and-data-storage"></a><span data-ttu-id="7e3a3-184">Использование SharePoint для хранения файлов и данных</span><span class="sxs-lookup"><span data-stu-id="7e3a3-184">Use SharePoint for file and data storage</span></span>

<span data-ttu-id="7e3a3-185">***Сценарии интеграции:** Автономные приложения, приложения для совместной работы, страницы SharePoint*</span><span class="sxs-lookup"><span data-stu-id="7e3a3-185">***Integration scenarios:** Standalone apps, collaboration apps, SharePoint pages*</span></span>

<span data-ttu-id="7e3a3-186">При создании команды в [семействе веб-сайтов SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) также предоставляется поддержка хранилища файлов и данных для этой команды.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-186">When a team is created, a [SharePoint site collection](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) is also provisioned to support file and data storage for that team.</span></span> <span data-ttu-id="7e3a3-187">Ваше приложение может использовать эту функцию и должна использовать эту функцию, если она взаимодействует с файлами.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-187">Your app can and should leverage this feature if it interacts with files.</span></span> <span data-ttu-id="7e3a3-188">Кроме того, семейство веб-сайтов можно использовать для хранения необработанных данных в списках SharePoint и Excel.</span><span class="sxs-lookup"><span data-stu-id="7e3a3-188">You can also use the site collection to store raw data in SharePoint Lists and Excel.</span></span>