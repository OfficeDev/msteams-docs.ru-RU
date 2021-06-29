---
title: Предварительный просмотр для ссылки "Вкладки" и представление стадий
author: Rajeshwari-v
description: Как развязать ссылку, открыть представление сцены и закрепить вкладку с помощью Microsoft Teams приложения.
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: b54eb5942d19749b39bb9bb504dd8645f5655ef3
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179946"
---
# <a name="tabs-link-unfurling-and-stage-view"></a><span data-ttu-id="c2435-103">Предварительный просмотр для ссылки "Вкладки" и представление стадий</span><span class="sxs-lookup"><span data-stu-id="c2435-103">Tabs link unfurling and Stage View</span></span>

> [!NOTE]
> <span data-ttu-id="c2435-104">Эта функция доступна только для [предварительного просмотра общедоступных](../resources/dev-preview/developer-preview-intro.md) разработчиков.</span><span class="sxs-lookup"><span data-stu-id="c2435-104">This feature is available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="c2435-105">Представление stage — это новый компонент пользовательского интерфейса (пользовательского интерфейса), который позволяет отрисовки контента, открываемой на полном экране в Teams и закрепленной в качестве вкладки.</span><span class="sxs-lookup"><span data-stu-id="c2435-105">Stage View is a new user interface (UI) component, which allows you to render the content that is opened in full screen in Teams and pinned as a tab.</span></span>
 
> [!NOTE]
> <span data-ttu-id="c2435-106">В настоящее время Teams мобильные клиенты не поддерживают ссылку на разгрузку и представление stage.</span><span class="sxs-lookup"><span data-stu-id="c2435-106">Currently, Teams mobile clients do no support tabs link unfurling and Stage View.</span></span> <span data-ttu-id="c2435-107">Мобильные клиенты используют атрибут, предоставленный разработчиком, чтобы открыть страницу в `websiteUrl` веб-браузере устройства.</span><span class="sxs-lookup"><span data-stu-id="c2435-107">Mobile clients use the `websiteUrl` attribute provided by the developer to open the page in the device's web browser.</span></span>

## <a name="stage-view"></a><span data-ttu-id="c2435-108">Представление сцены</span><span class="sxs-lookup"><span data-stu-id="c2435-108">Stage View</span></span>

<span data-ttu-id="c2435-109">Представление stage — это компонент пользовательского интерфейса полного экрана, который можно вызвать для поверхности веб-контента.</span><span class="sxs-lookup"><span data-stu-id="c2435-109">Stage View is a full screen UI component that you can invoke to surface your web content.</span></span> <span data-ttu-id="c2435-110">Существующая служба разгрузки ссылок обновляется таким образом, чтобы она использовалась для того, чтобы превратить URL-адреса в вкладку с помощью служб адаптивной карты и чата.</span><span class="sxs-lookup"><span data-stu-id="c2435-110">The existing link unfurling service is updated so that it is used to turn URLs into a tab using an Adaptive Card and Chat Services.</span></span> <span data-ttu-id="c2435-111">Когда пользователь отправляет URL-адрес в чате или канале, URL-адрес будет развернут на адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="c2435-111">When a user sends a URL in a chat or channel, the URL is unfurled to an Adaptive Card.</span></span> <span data-ttu-id="c2435-112">Пользователь может выбрать **Просмотр** на карте и закрепить содержимое в качестве вкладки непосредственно из представления stage.</span><span class="sxs-lookup"><span data-stu-id="c2435-112">The user can select **View** in the card, and pin the content as a tab directly from Stage View.</span></span>

## <a name="advantage-of-stage-view"></a><span data-ttu-id="c2435-113">Преимущество представления на этапе</span><span class="sxs-lookup"><span data-stu-id="c2435-113">Advantage of Stage View</span></span>

<span data-ttu-id="c2435-114">Представление stage позволяет обеспечить более бесперебойное просмотр контента в Teams.</span><span class="sxs-lookup"><span data-stu-id="c2435-114">Stage View helps provide a more seamless experience of viewing content in Teams.</span></span> <span data-ttu-id="c2435-115">Пользователи могут открывать и просматривать контент, предоставляемый вашим приложением, не выходя из контекста, и могут прикрепить содержимое к чату или каналу для быстрого доступа в будущем.</span><span class="sxs-lookup"><span data-stu-id="c2435-115">Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access.</span></span> <span data-ttu-id="c2435-116">Это приводит к более высокому взаимодействию пользователей с приложением.</span><span class="sxs-lookup"><span data-stu-id="c2435-116">This leads to a higher user engagement with your app.</span></span>

## <a name="stage-view-vs-task-module"></a><span data-ttu-id="c2435-117">Модуль Представления сцены и задачи</span><span class="sxs-lookup"><span data-stu-id="c2435-117">Stage View vs. Task module</span></span>

|<span data-ttu-id="c2435-118">Представление сцены</span><span class="sxs-lookup"><span data-stu-id="c2435-118">Stage View</span></span>|<span data-ttu-id="c2435-119">Модуль задач</span><span class="sxs-lookup"><span data-stu-id="c2435-119">Task module</span></span>|
|:-----------|:-----------|
|<span data-ttu-id="c2435-120">Представление stage полезно, если у вас есть богатый контент для отображения для пользователей, таких как страница, панель мониторинга, файл и так далее.</span><span class="sxs-lookup"><span data-stu-id="c2435-120">Stage View is useful when you have rich content to display to the users, such as a page, a dashboard, a file, and so on.</span></span> <span data-ttu-id="c2435-121">Он предоставляет богатые функции, которые помогают отрисовки контента на полноэкранной холсте.</span><span class="sxs-lookup"><span data-stu-id="c2435-121">It provides  rich features that helps to render your content in the full-screen canvas.</span></span>|<span data-ttu-id="c2435-122">[Модуль задач](../task-modules-and-cards/task-modules/task-modules-tabs.md) особенно полезен для отображения сообщений, которые требуют внимания пользователя, или сбора сведений, необходимых для перемещения на следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="c2435-122">[Task module](../task-modules-and-cards/task-modules/task-modules-tabs.md) is especially useful to display messages that require user attention, or collect information required to move to the next step.</span></span>|
  
## <a name="invoke-stage-view"></a><span data-ttu-id="c2435-123">Вызов представления стадии</span><span class="sxs-lookup"><span data-stu-id="c2435-123">Invoke Stage View</span></span>

<span data-ttu-id="c2435-124">Вы можете вызвать представление stage следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c2435-124">You can invoke Stage View in the following  ways:</span></span>

* [<span data-ttu-id="c2435-125">Вызов представления сцены из адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="c2435-125">Invoke Stage View from Adaptive Card</span></span>](#invoke-stage-view-from-adaptive-card)
* [<span data-ttu-id="c2435-126">Вызов представления сцены по глубокой ссылке</span><span class="sxs-lookup"><span data-stu-id="c2435-126">Invoke Stage View through deep link</span></span>](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a><span data-ttu-id="c2435-127">Вызов представления сцены из адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="c2435-127">Invoke Stage View from Adaptive Card</span></span>

<span data-ttu-id="c2435-128">Когда пользователь вводит URL-адрес Teams настольного клиента, бот вызывается и [](../task-modules-and-cards/cards/cards-actions.md) возвращает адаптивную карту с возможностью открытия URL-адреса на этапе.</span><span class="sxs-lookup"><span data-stu-id="c2435-128">When the user enters a URL on the Teams desktop client, the bot is invoked and returns an [Adaptive Card](../task-modules-and-cards/cards/cards-actions.md) with the option to open the URL in a stage.</span></span> <span data-ttu-id="c2435-129">После запуска этапа и предоставляются, можно добавить возможность закрепить этап `tabInfo` в качестве вкладки.</span><span class="sxs-lookup"><span data-stu-id="c2435-129">After a stage is launched and the `tabInfo` is provided, you can add the ability to pin the stage as a tab.</span></span>  

<span data-ttu-id="c2435-130">На следующих изображениях показан этап, открытый с адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="c2435-130">The following images display a stage opened from an Adaptive Card:</span></span>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt="Open a stage from Adaptive Card" width="700"/>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt="Open a stage" width="700"/>

### <a name="example"></a><span data-ttu-id="c2435-131">Пример</span><span class="sxs-lookup"><span data-stu-id="c2435-131">Example</span></span>

<span data-ttu-id="c2435-132">Ниже приводится код, который откроет этап с адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="c2435-132">Following is the code to open a stage from an Adaptive Card:</span></span>

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

<span data-ttu-id="c2435-133">Тип `invoke` запроса должен быть `composeExtension/queryLink` .</span><span class="sxs-lookup"><span data-stu-id="c2435-133">The `invoke` request type must be `composeExtension/queryLink`.</span></span>

> [!NOTE]
> * <span data-ttu-id="c2435-134">`invoke` рабочий процесс похож на текущий `appLinking` рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="c2435-134">`invoke` workflow is similar to the current `appLinking` workflow.</span></span> 
> * <span data-ttu-id="c2435-135">Для обеспечения согласованности рекомендуется назвать `Action.Submit` как `View` .</span><span class="sxs-lookup"><span data-stu-id="c2435-135">To maintain consistency, it is recommended to name `Action.Submit` as `View`.</span></span>
> * <span data-ttu-id="c2435-136">`websiteUrl` это обязательное свойство, передав его `TabInfo` объекту.</span><span class="sxs-lookup"><span data-stu-id="c2435-136">`websiteUrl` is a required property to be passed in the `TabInfo` object.</span></span>

<span data-ttu-id="c2435-137">Ниже приводится процесс вызова представления stage:</span><span class="sxs-lookup"><span data-stu-id="c2435-137">Following is the process to invoke Stage View:</span></span>

* <span data-ttu-id="c2435-138">Когда пользователь выбирает **View,** бот получает `invoke` запрос.</span><span class="sxs-lookup"><span data-stu-id="c2435-138">When the user selects **View**, the bot receives an `invoke` request.</span></span> <span data-ttu-id="c2435-139">Тип запроса `composeExtension/queryLink` .</span><span class="sxs-lookup"><span data-stu-id="c2435-139">The request type is `composeExtension/queryLink`.</span></span>
* <span data-ttu-id="c2435-140">`invoke` Ответ от бота содержит адаптивную карточку с `tab/tabInfoAction` типом в ней.</span><span class="sxs-lookup"><span data-stu-id="c2435-140">`invoke` response from bot contains an Adaptive Card with type `tab/tabInfoAction` in it.</span></span>
* <span data-ttu-id="c2435-141">Бот отвечает `200` кодом.</span><span class="sxs-lookup"><span data-stu-id="c2435-141">The bot responds with a `200` code.</span></span>

> [!NOTE]
> <span data-ttu-id="c2435-142">В настоящее время Teams мобильные клиенты не поддерживают возможности представления stage.</span><span class="sxs-lookup"><span data-stu-id="c2435-142">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="c2435-143">Когда пользователь выбирает **View** на мобильном клиенте, он передается в браузер устройства.</span><span class="sxs-lookup"><span data-stu-id="c2435-143">When a user selects **View** on a mobile client, the user is taken to the device's browser.</span></span> <span data-ttu-id="c2435-144">Браузер открывает URL-адрес, указанный в `websiteUrl` параметре `TabInfo` объекта.</span><span class="sxs-lookup"><span data-stu-id="c2435-144">The browser opens the URL specified in the `websiteUrl` parameter of the `TabInfo` object.</span></span>

## <a name="invoke-stage-view-through-deep-link"></a><span data-ttu-id="c2435-145">Вызов представления сцены по глубокой ссылке</span><span class="sxs-lookup"><span data-stu-id="c2435-145">Invoke Stage View through deep link</span></span>

<span data-ttu-id="c2435-146">Чтобы вызвать представление стадии с помощью глубокой ссылки на вкладке, необходимо завернуть URL-адрес глубокой ссылки в `microsoftTeams.executeDeeplink(url)` API.</span><span class="sxs-lookup"><span data-stu-id="c2435-146">To invoke the Stage View through deep link from your tab, you must wrap the deep link URL in the `microsoftTeams.executeDeeplink(url)` API.</span></span> <span data-ttu-id="c2435-147">Глубокая ссылка также может быть передана через `OpenURL` действие в карточке.</span><span class="sxs-lookup"><span data-stu-id="c2435-147">The deep link can also be passed through an `OpenURL` action in the card.</span></span>

<span data-ttu-id="c2435-148">На следующем изображении отображается представление стадии, вызываемая по глубокой ссылке:</span><span class="sxs-lookup"><span data-stu-id="c2435-148">The following image displays a Stage View invoked through a deep link:</span></span>

<img src="~/assets/images/tab-images/invoke-stage-view-through-deep-link.png" alt="Invoke a Stage View through a deep link" width="400"/>

### <a name="syntax"></a><span data-ttu-id="c2435-149">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="c2435-149">Syntax</span></span>

<span data-ttu-id="c2435-150">Ниже приводится синтаксис deeplink:</span><span class="sxs-lookup"><span data-stu-id="c2435-150">Following is the deeplink syntax:</span></span>  
 
<span data-ttu-id="c2435-151"> https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":"[contentUrl]","websiteUrl":"[websiteUrl]","name":"[name]}.</span><span class="sxs-lookup"><span data-stu-id="c2435-151">https://teams.microsoft.com/l/stage/{appId}/0?context={“contentUrl”:”[contentUrl]”,“websiteUrl”:”[websiteUrl]”,“name”:”[name]”}</span></span>

### <a name="examples"></a><span data-ttu-id="c2435-152">Примеры</span><span class="sxs-lookup"><span data-stu-id="c2435-152">Examples</span></span>

<span data-ttu-id="c2435-153">Когда пользователь вводит URL-адрес, он будет развернут в адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="c2435-153">When a user enters a URL, it is unfurled into an Adaptive card.</span></span>

<span data-ttu-id="c2435-154">Ниже приводятся примеры глубоких ссылок для вызова представления stage:</span><span class="sxs-lookup"><span data-stu-id="c2435-154">Following are the deep link examples to invoke Stage View:</span></span>

<span data-ttu-id="c2435-155">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="c2435-155">**Example 1**</span></span>

<span data-ttu-id="c2435-156"> https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx",websiteUrl".:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name":"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="c2435-156">https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

<span data-ttu-id="c2435-157">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="c2435-157">**Example 2**</span></span>

<span data-ttu-id="c2435-158"> https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx",websiteUrl".:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name":"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="c2435-158">https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

> [!NOTE]
> * <span data-ttu-id="c2435-159">`name`Необязательный в глубокой ссылке.</span><span class="sxs-lookup"><span data-stu-id="c2435-159">The `name` is optional in deep link.</span></span> <span data-ttu-id="c2435-160">Если оно не включено, имя приложения заменяет его.</span><span class="sxs-lookup"><span data-stu-id="c2435-160">If not included, the app name replaces it.</span></span>
> * <span data-ttu-id="c2435-161">Глубокая ссылка также может быть передана через `OpenURL` действие.</span><span class="sxs-lookup"><span data-stu-id="c2435-161">The deep link can also be passed through an `OpenURL` action.</span></span>
> * <span data-ttu-id="c2435-162">В настоящее время Teams мобильные клиенты не поддерживают возможности представления stage.</span><span class="sxs-lookup"><span data-stu-id="c2435-162">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="c2435-163">Когда пользователи выбирают глубокую ссылку на представление stage, они перебираются в веб-браузер своего устройства.</span><span class="sxs-lookup"><span data-stu-id="c2435-163">When users select a deep link to a Stage View, they are taken to their device's web browser.</span></span> <span data-ttu-id="c2435-164">Веб-браузер открывает URL-адрес, указанный в `websiteUrl` параметре глубокой ссылки.</span><span class="sxs-lookup"><span data-stu-id="c2435-164">The web browser opens the URL specified in the `websiteUrl` parameter of the deep link.</span></span>
> * <span data-ttu-id="c2435-165">При запуске stage из определенного контекста убедитесь, что приложение работает в этом контексте.</span><span class="sxs-lookup"><span data-stu-id="c2435-165">When you launch a Stage from a certain context, ensure that your app works in that context.</span></span> <span data-ttu-id="c2435-166">Например, если представление stage запущено из личного приложения, необходимо убедиться, что ваше приложение имеет личную область.</span><span class="sxs-lookup"><span data-stu-id="c2435-166">For example, if your Stage View is launched from a personal app, you must ensure your app has a personal scope.</span></span>

## <a name="tab-information-property"></a><span data-ttu-id="c2435-167">Свойство сведений tab</span><span class="sxs-lookup"><span data-stu-id="c2435-167">Tab information property</span></span>

| <span data-ttu-id="c2435-168">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="c2435-168">Property name</span></span> | <span data-ttu-id="c2435-169">Тип</span><span class="sxs-lookup"><span data-stu-id="c2435-169">Type</span></span> | <span data-ttu-id="c2435-170">Количество символов</span><span class="sxs-lookup"><span data-stu-id="c2435-170">Number of characters</span></span> | <span data-ttu-id="c2435-171">Описание</span><span class="sxs-lookup"><span data-stu-id="c2435-171">Description</span></span> |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | <span data-ttu-id="c2435-172">String</span><span class="sxs-lookup"><span data-stu-id="c2435-172">String</span></span> | <span data-ttu-id="c2435-173">64</span><span class="sxs-lookup"><span data-stu-id="c2435-173">64</span></span> | <span data-ttu-id="c2435-174">Это свойство является уникальным идентификатором для объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="c2435-174">This property is a  unique identifier for the entity that the tab displays.</span></span> <span data-ttu-id="c2435-175">Это поле обязательно для заполнения.</span><span class="sxs-lookup"><span data-stu-id="c2435-175">This is a required field.</span></span>|
| `name` | <span data-ttu-id="c2435-176">String</span><span class="sxs-lookup"><span data-stu-id="c2435-176">String</span></span> | <span data-ttu-id="c2435-177">128</span><span class="sxs-lookup"><span data-stu-id="c2435-177">128</span></span> | <span data-ttu-id="c2435-178">Это свойство — отображаемая вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="c2435-178">This property is the display name of the tab in the channel interface.</span></span> <span data-ttu-id="c2435-179">Это поле является необязательным.</span><span class="sxs-lookup"><span data-stu-id="c2435-179">This is an optional field.</span></span>|
| `contentUrl` | <span data-ttu-id="c2435-180">String</span><span class="sxs-lookup"><span data-stu-id="c2435-180">String</span></span> | <span data-ttu-id="c2435-181">2048</span><span class="sxs-lookup"><span data-stu-id="c2435-181">2048</span></span> | <span data-ttu-id="c2435-182">Это свойство — https:// URL-адрес, который указывает на пользовательский интерфейс объекта, отображаемого на Teams холсте.</span><span class="sxs-lookup"><span data-stu-id="c2435-182">This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span> <span data-ttu-id="c2435-183">Это поле обязательно для заполнения.</span><span class="sxs-lookup"><span data-stu-id="c2435-183">This is a required field.</span></span>|
| `websiteUrl?` | <span data-ttu-id="c2435-184">String</span><span class="sxs-lookup"><span data-stu-id="c2435-184">String</span></span> | <span data-ttu-id="c2435-185">2048</span><span class="sxs-lookup"><span data-stu-id="c2435-185">2048</span></span> | <span data-ttu-id="c2435-186">Это свойство является https://, на который нужно указать, если пользователь выбирает для просмотра в браузере.</span><span class="sxs-lookup"><span data-stu-id="c2435-186">This property is the https:// URL to point at, if a user selects to view in a browser.</span></span> <span data-ttu-id="c2435-187">Это поле обязательно для заполнения.</span><span class="sxs-lookup"><span data-stu-id="c2435-187">This is a required field.</span></span>|
| `removeUrl?` | <span data-ttu-id="c2435-188">String</span><span class="sxs-lookup"><span data-stu-id="c2435-188">String</span></span> | <span data-ttu-id="c2435-189">2048</span><span class="sxs-lookup"><span data-stu-id="c2435-189">2048</span></span> | <span data-ttu-id="c2435-190">Это свойство — https:// URL-адрес, который указывает на пользовательский интерфейс, который будет отображаться при удалении вкладки пользователем. Это необязательное поле.</span><span class="sxs-lookup"><span data-stu-id="c2435-190">This property is the https:// URL that points to the UI to be displayed when the user deletes the tab. This is an optional field.</span></span>|

## <a name="see-also"></a><span data-ttu-id="c2435-191">См. также</span><span class="sxs-lookup"><span data-stu-id="c2435-191">See also</span></span>

* [<span data-ttu-id="c2435-192">Расширение обмена сообщениями связывает разгрузку</span><span class="sxs-lookup"><span data-stu-id="c2435-192">Messaging extensions link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="c2435-193">Teams вкладки</span><span class="sxs-lookup"><span data-stu-id="c2435-193">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="c2435-194">Создание личной вкладки</span><span class="sxs-lookup"><span data-stu-id="c2435-194">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="c2435-195">Создание вкладки канала или группы</span><span class="sxs-lookup"><span data-stu-id="c2435-195">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a><span data-ttu-id="c2435-196">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="c2435-196">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c2435-197">Создание вкладок бесед</span><span class="sxs-lookup"><span data-stu-id="c2435-197">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)