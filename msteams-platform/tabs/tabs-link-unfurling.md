---
title: Предварительный просмотр для ссылки "Вкладки" и представление стадий
author: Rajeshwari-v
description: Как развязать ссылку, открыть представление сцены и закрепить вкладку с помощью Microsoft Teams приложения.
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 1495bba765d149d23156b136be85f39d07c2d94b
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140175"
---
# <a name="tabs-link-unfurling-and-stage-view"></a><span data-ttu-id="d664c-103">Предварительный просмотр для ссылки "Вкладки" и представление стадий</span><span class="sxs-lookup"><span data-stu-id="d664c-103">Tabs link unfurling and Stage View</span></span>

> [!NOTE]
> <span data-ttu-id="d664c-104">Эта функция доступна только для [предварительного просмотра общедоступных](../resources/dev-preview/developer-preview-intro.md) разработчиков.</span><span class="sxs-lookup"><span data-stu-id="d664c-104">This feature is available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="d664c-105">Представление stage — это новый компонент пользовательского интерфейса (пользовательского интерфейса), который позволяет отрисовки контента, открываемой на полном экране в Teams и закрепленной в качестве вкладки.</span><span class="sxs-lookup"><span data-stu-id="d664c-105">Stage View is a new user interface (UI) component, which allows you to render the content that is opened in full screen in Teams and pinned as a tab.</span></span>
 
> [!NOTE]
> <span data-ttu-id="d664c-106">В настоящее время Teams мобильные клиенты не поддерживают ссылку на разгрузку и представление stage.</span><span class="sxs-lookup"><span data-stu-id="d664c-106">Currently, Teams mobile clients do no support tabs link unfurling and Stage View.</span></span> <span data-ttu-id="d664c-107">Мобильные клиенты используют атрибут, предоставленный разработчиком, чтобы открыть страницу в `websiteUrl` веб-браузере устройства.</span><span class="sxs-lookup"><span data-stu-id="d664c-107">Mobile clients use the `websiteUrl` attribute provided by the developer to open the page in the device's web browser.</span></span>

## <a name="stage-view"></a><span data-ttu-id="d664c-108">Представление сцены</span><span class="sxs-lookup"><span data-stu-id="d664c-108">Stage View</span></span>

<span data-ttu-id="d664c-109">Представление stage — это компонент пользовательского интерфейса полного экрана, который можно вызвать для поверхности веб-контента.</span><span class="sxs-lookup"><span data-stu-id="d664c-109">Stage View is a full screen UI component that you can invoke to surface your web content.</span></span> <span data-ttu-id="d664c-110">Существующая служба разгрузки ссылок обновляется таким образом, чтобы она использовалась для того, чтобы превратить URL-адреса в вкладку с помощью служб адаптивной карты и чата.</span><span class="sxs-lookup"><span data-stu-id="d664c-110">The existing link unfurling service is updated so that it is used to turn URLs into a tab using an Adaptive Card and Chat Services.</span></span> <span data-ttu-id="d664c-111">Когда пользователь отправляет URL-адрес в чате или канале, URL-адрес будет развернут на адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="d664c-111">When a user sends a URL in a chat or channel, the URL is unfurled to an Adaptive Card.</span></span> <span data-ttu-id="d664c-112">Пользователь может выбрать **Просмотр** на карте и закрепить содержимое в качестве вкладки непосредственно из представления stage.</span><span class="sxs-lookup"><span data-stu-id="d664c-112">The user can select **View** in the card, and pin the content as a tab directly from Stage View.</span></span>

## <a name="advantage-of-stage-view"></a><span data-ttu-id="d664c-113">Преимущество представления на этапе</span><span class="sxs-lookup"><span data-stu-id="d664c-113">Advantage of Stage View</span></span>

<span data-ttu-id="d664c-114">Представление stage позволяет обеспечить более бесперебойное просмотр контента в Teams.</span><span class="sxs-lookup"><span data-stu-id="d664c-114">Stage View helps provide a more seamless experience of viewing content in Teams.</span></span> <span data-ttu-id="d664c-115">Пользователи могут открывать и просматривать контент, предоставляемый вашим приложением, не выходя из контекста, и могут прикрепить содержимое к чату или каналу для быстрого доступа в будущем.</span><span class="sxs-lookup"><span data-stu-id="d664c-115">Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access.</span></span> <span data-ttu-id="d664c-116">Это приводит к более высокому взаимодействию пользователей с приложением.</span><span class="sxs-lookup"><span data-stu-id="d664c-116">This leads to a higher user engagement with your app.</span></span>

## <a name="stage-view-vs-task-module"></a><span data-ttu-id="d664c-117">Модуль Представления сцены и задачи</span><span class="sxs-lookup"><span data-stu-id="d664c-117">Stage View vs. Task module</span></span>

|<span data-ttu-id="d664c-118">Представление сцены</span><span class="sxs-lookup"><span data-stu-id="d664c-118">Stage View</span></span>|<span data-ttu-id="d664c-119">Модуль задач</span><span class="sxs-lookup"><span data-stu-id="d664c-119">Task module</span></span>|
|:-----------|:-----------|
|<span data-ttu-id="d664c-120">Представление stage полезно, если у вас есть богатый контент для отображения для пользователей, таких как страница, панель мониторинга, файл и так далее.</span><span class="sxs-lookup"><span data-stu-id="d664c-120">Stage View is useful when you have rich content to display to the users, such as a page, a dashboard, a file, and so on.</span></span> <span data-ttu-id="d664c-121">Он предоставляет богатые функции, которые помогают отрисовки контента на полноэкранной холсте.</span><span class="sxs-lookup"><span data-stu-id="d664c-121">It provides  rich features that helps to render your content in the full-screen canvas.</span></span>|<span data-ttu-id="d664c-122">[Модуль задач](../task-modules-and-cards/task-modules/task-modules-tabs.md) особенно полезен для отображения сообщений, которые требуют внимания пользователя, или сбора сведений, необходимых для перемещения на следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="d664c-122">[Task module](../task-modules-and-cards/task-modules/task-modules-tabs.md) is especially useful to display messages that require user attention, or collect information required to move to the next step.</span></span>|
  
## <a name="invoke-stage-view"></a><span data-ttu-id="d664c-123">Вызов представления стадии</span><span class="sxs-lookup"><span data-stu-id="d664c-123">Invoke Stage View</span></span>

<span data-ttu-id="d664c-124">Вы можете вызвать представление stage следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d664c-124">You can invoke Stage View in the following  ways:</span></span>

* [<span data-ttu-id="d664c-125">Вызов представления сцены из адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="d664c-125">Invoke Stage View from Adaptive Card</span></span>](#invoke-stage-view-from-adaptive-card)
* [<span data-ttu-id="d664c-126">Вызов представления сцены по глубокой ссылке</span><span class="sxs-lookup"><span data-stu-id="d664c-126">Invoke Stage View through deep link</span></span>](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a><span data-ttu-id="d664c-127">Вызов представления сцены из адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="d664c-127">Invoke Stage View from Adaptive Card</span></span>

<span data-ttu-id="d664c-128">Когда пользователь вводит URL-адрес Teams настольного клиента, бот вызывается и [](../task-modules-and-cards/cards/cards-actions.md) возвращает адаптивную карту с возможностью открытия URL-адреса на этапе.</span><span class="sxs-lookup"><span data-stu-id="d664c-128">When the user enters a URL on the Teams desktop client, the bot is invoked and returns an [Adaptive Card](../task-modules-and-cards/cards/cards-actions.md) with the option to open the URL in a stage.</span></span> <span data-ttu-id="d664c-129">После запуска этапа и предоставляются, можно добавить возможность закрепить этап `tabInfo` в качестве вкладки.</span><span class="sxs-lookup"><span data-stu-id="d664c-129">After a stage is launched and the `tabInfo` is provided, you can add the ability to pin the stage as a tab.</span></span>  

<span data-ttu-id="d664c-130">На следующих изображениях показан этап, открытый с адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="d664c-130">The following images display a stage opened from an Adaptive Card:</span></span>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt="Open a stage from Adaptive Card" width="700"/>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt="Open a stage" width="700"/>

### <a name="example"></a><span data-ttu-id="d664c-131">Пример</span><span class="sxs-lookup"><span data-stu-id="d664c-131">Example</span></span>

<span data-ttu-id="d664c-132">Ниже приводится код, который откроет этап с адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="d664c-132">Following is the code to open a stage from an Adaptive Card:</span></span>

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

<span data-ttu-id="d664c-133">Тип `invoke` запроса должен быть `composeExtension/queryLink` .</span><span class="sxs-lookup"><span data-stu-id="d664c-133">The `invoke` request type must be `composeExtension/queryLink`.</span></span>

> [!NOTE]
> * <span data-ttu-id="d664c-134">`invoke` рабочий процесс похож на текущий `appLinking` рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="d664c-134">`invoke` workflow is similar to the current `appLinking` workflow.</span></span> 
> * <span data-ttu-id="d664c-135">Для обеспечения согласованности рекомендуется назвать `Action.Submit` как `View` .</span><span class="sxs-lookup"><span data-stu-id="d664c-135">To maintain consistency, it is recommended to name `Action.Submit` as `View`.</span></span>
> * <span data-ttu-id="d664c-136">`websiteUrl` это обязательное свойство, передав его `TabInfo` объекту.</span><span class="sxs-lookup"><span data-stu-id="d664c-136">`websiteUrl` is a required property to be passed in the `TabInfo` object.</span></span>

<span data-ttu-id="d664c-137">Ниже приводится процесс вызова представления stage:</span><span class="sxs-lookup"><span data-stu-id="d664c-137">Following is the process to invoke Stage View:</span></span>

* <span data-ttu-id="d664c-138">Когда пользователь выбирает **View,** бот получает `invoke` запрос.</span><span class="sxs-lookup"><span data-stu-id="d664c-138">When the user selects **View**, the bot receives an `invoke` request.</span></span> <span data-ttu-id="d664c-139">Тип запроса `composeExtension/queryLink` .</span><span class="sxs-lookup"><span data-stu-id="d664c-139">The request type is `composeExtension/queryLink`.</span></span>
* <span data-ttu-id="d664c-140">`invoke` Ответ от бота содержит адаптивную карточку с `tab/tabInfoAction` типом в ней.</span><span class="sxs-lookup"><span data-stu-id="d664c-140">`invoke` response from bot contains an Adaptive Card with type `tab/tabInfoAction` in it.</span></span>
* <span data-ttu-id="d664c-141">Бот отвечает `200` кодом.</span><span class="sxs-lookup"><span data-stu-id="d664c-141">The bot responds with a `200` code.</span></span>

> [!NOTE]
> <span data-ttu-id="d664c-142">В настоящее время Teams мобильные клиенты не поддерживают возможности представления stage.</span><span class="sxs-lookup"><span data-stu-id="d664c-142">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="d664c-143">Когда пользователь выбирает **View** на мобильном клиенте, он передается в браузер устройства.</span><span class="sxs-lookup"><span data-stu-id="d664c-143">When a user selects **View** on a mobile client, the user is taken to the device's browser.</span></span> <span data-ttu-id="d664c-144">Браузер открывает URL-адрес, указанный в `websiteUrl` параметре `TabInfo` объекта.</span><span class="sxs-lookup"><span data-stu-id="d664c-144">The browser opens the URL specified in the `websiteUrl` parameter of the `TabInfo` object.</span></span>

## <a name="invoke-stage-view-through-deep-link"></a><span data-ttu-id="d664c-145">Вызов представления сцены по глубокой ссылке</span><span class="sxs-lookup"><span data-stu-id="d664c-145">Invoke Stage View through deep link</span></span>

<span data-ttu-id="d664c-146">Чтобы вызвать представление стадии с помощью глубокой ссылки на вкладке, необходимо завернуть URL-адрес глубокой ссылки в `microsoftTeams.executeDeeplink(url)` API.</span><span class="sxs-lookup"><span data-stu-id="d664c-146">To invoke the Stage View through deep link from your tab, you must wrap the deep link URL in the `microsoftTeams.executeDeeplink(url)` API.</span></span> <span data-ttu-id="d664c-147">Глубокая ссылка также может быть передана через `OpenURL` действие в карточке.</span><span class="sxs-lookup"><span data-stu-id="d664c-147">The deep link can also be passed through an `OpenURL` action in the card.</span></span>

<span data-ttu-id="d664c-148">На следующем изображении отображается представление стадии, вызываемая по глубокой ссылке:</span><span class="sxs-lookup"><span data-stu-id="d664c-148">The following image displays a Stage View invoked through a deep link:</span></span>

<img src="~/assets/images/tab-images/invoke-stage-view-through-deep-link.png" alt="Invoke a Stage View through a deep link" width="400"/>

### <a name="syntax"></a><span data-ttu-id="d664c-149">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="d664c-149">Syntax</span></span>

<span data-ttu-id="d664c-150">Ниже приводится синтаксис deeplink:</span><span class="sxs-lookup"><span data-stu-id="d664c-150">Following is the deeplink syntax:</span></span>  
 
<span data-ttu-id="d664c-151"> https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":"[contentUrl]","websiteUrl":"[websiteUrl]","name":"[name]}.</span><span class="sxs-lookup"><span data-stu-id="d664c-151">https://teams.microsoft.com/l/stage/{appId}/0?context={“contentUrl”:”[contentUrl]”,“websiteUrl”:”[websiteUrl]”,“name”:”[name]”}</span></span>

### <a name="examples"></a><span data-ttu-id="d664c-152">Примеры</span><span class="sxs-lookup"><span data-stu-id="d664c-152">Examples</span></span>

<span data-ttu-id="d664c-153">Когда пользователь вводит URL-адрес, он будет развернут в адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="d664c-153">When a user enters a URL, it is unfurled into an Adaptive card.</span></span>

<span data-ttu-id="d664c-154">Ниже приводятся примеры глубоких ссылок для вызова представления stage:</span><span class="sxs-lookup"><span data-stu-id="d664c-154">Following are the deep link examples to invoke Stage View:</span></span>

<span data-ttu-id="d664c-155">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="d664c-155">**Example 1**</span></span>

<span data-ttu-id="d664c-156"> https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx",websiteUrl".:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name":"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="d664c-156">https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

<span data-ttu-id="d664c-157">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="d664c-157">**Example 2**</span></span>

<span data-ttu-id="d664c-158"> https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx",websiteUrl".:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name":"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="d664c-158">https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

> [!NOTE]
> * <span data-ttu-id="d664c-159">`name`Необязательный в глубокой ссылке.</span><span class="sxs-lookup"><span data-stu-id="d664c-159">The `name` is optional in deep link.</span></span> <span data-ttu-id="d664c-160">Если оно не включено, имя приложения заменяет его.</span><span class="sxs-lookup"><span data-stu-id="d664c-160">If not included, the app name replaces it.</span></span>
> * <span data-ttu-id="d664c-161">Глубокая ссылка также может быть передана через `OpenURL` действие.</span><span class="sxs-lookup"><span data-stu-id="d664c-161">The deep link can also be passed through an `OpenURL` action.</span></span>
> * <span data-ttu-id="d664c-162">В настоящее время Teams мобильные клиенты не поддерживают возможности представления stage.</span><span class="sxs-lookup"><span data-stu-id="d664c-162">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="d664c-163">Когда пользователи выбирают глубокую ссылку на представление stage, они перебираются в веб-браузер своего устройства.</span><span class="sxs-lookup"><span data-stu-id="d664c-163">When users select a deep link to a Stage View, they are taken to their device's web browser.</span></span> <span data-ttu-id="d664c-164">Веб-браузер открывает URL-адрес, указанный в `websiteUrl` параметре глубокой ссылки.</span><span class="sxs-lookup"><span data-stu-id="d664c-164">The web browser opens the URL specified in the `websiteUrl` parameter of the deep link.</span></span>
> * <span data-ttu-id="d664c-165">При запуске stage из определенного контекста убедитесь, что приложение работает в этом контексте.</span><span class="sxs-lookup"><span data-stu-id="d664c-165">When you launch a Stage from a certain context, ensure that your app works in that context.</span></span> <span data-ttu-id="d664c-166">Например, если представление stage запущено из личного приложения, необходимо убедиться, что ваше приложение имеет личную область.</span><span class="sxs-lookup"><span data-stu-id="d664c-166">For example, if your Stage View is launched from a personal app, you must ensure your app has a personal scope.</span></span>

## <a name="tab-information-property"></a><span data-ttu-id="d664c-167">Свойство сведений tab</span><span class="sxs-lookup"><span data-stu-id="d664c-167">Tab information property</span></span>

| <span data-ttu-id="d664c-168">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="d664c-168">Property name</span></span> | <span data-ttu-id="d664c-169">Тип</span><span class="sxs-lookup"><span data-stu-id="d664c-169">Type</span></span> | <span data-ttu-id="d664c-170">Количество символов</span><span class="sxs-lookup"><span data-stu-id="d664c-170">Number of characters</span></span> | <span data-ttu-id="d664c-171">Описание</span><span class="sxs-lookup"><span data-stu-id="d664c-171">Description</span></span> |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | <span data-ttu-id="d664c-172">String</span><span class="sxs-lookup"><span data-stu-id="d664c-172">String</span></span> | <span data-ttu-id="d664c-173">64</span><span class="sxs-lookup"><span data-stu-id="d664c-173">64</span></span> | <span data-ttu-id="d664c-174">Это свойство является уникальным идентификатором для объекта, отображаемого на вкладке.</span><span class="sxs-lookup"><span data-stu-id="d664c-174">This property is a  unique identifier for the entity that the tab displays.</span></span> <span data-ttu-id="d664c-175">Это поле обязательно для заполнения.</span><span class="sxs-lookup"><span data-stu-id="d664c-175">This is a required field.</span></span>|
| `name` | <span data-ttu-id="d664c-176">String</span><span class="sxs-lookup"><span data-stu-id="d664c-176">String</span></span> | <span data-ttu-id="d664c-177">128</span><span class="sxs-lookup"><span data-stu-id="d664c-177">128</span></span> | <span data-ttu-id="d664c-178">Это свойство — отображаемая вкладки в интерфейсе канала.</span><span class="sxs-lookup"><span data-stu-id="d664c-178">This property is the display name of the tab in the channel interface.</span></span> <span data-ttu-id="d664c-179">Это поле является необязательным.</span><span class="sxs-lookup"><span data-stu-id="d664c-179">This is an optional field.</span></span>|
| `contentUrl` | <span data-ttu-id="d664c-180">String</span><span class="sxs-lookup"><span data-stu-id="d664c-180">String</span></span> | <span data-ttu-id="d664c-181">2048</span><span class="sxs-lookup"><span data-stu-id="d664c-181">2048</span></span> | <span data-ttu-id="d664c-182">Это свойство — https:// URL-адрес, который указывает на пользовательский интерфейс объекта, отображаемого на Teams холсте.</span><span class="sxs-lookup"><span data-stu-id="d664c-182">This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span> <span data-ttu-id="d664c-183">Это поле обязательно для заполнения.</span><span class="sxs-lookup"><span data-stu-id="d664c-183">This is a required field.</span></span>|
| `websiteUrl?` | <span data-ttu-id="d664c-184">String</span><span class="sxs-lookup"><span data-stu-id="d664c-184">String</span></span> | <span data-ttu-id="d664c-185">2048</span><span class="sxs-lookup"><span data-stu-id="d664c-185">2048</span></span> | <span data-ttu-id="d664c-186">Это свойство является https://, на который нужно указать, если пользователь выбирает для просмотра в браузере.</span><span class="sxs-lookup"><span data-stu-id="d664c-186">This property is the https:// URL to point at, if a user selects to view in a browser.</span></span> <span data-ttu-id="d664c-187">Это поле обязательно для заполнения.</span><span class="sxs-lookup"><span data-stu-id="d664c-187">This is a required field.</span></span>|
| `removeUrl?` | <span data-ttu-id="d664c-188">String</span><span class="sxs-lookup"><span data-stu-id="d664c-188">String</span></span> | <span data-ttu-id="d664c-189">2048</span><span class="sxs-lookup"><span data-stu-id="d664c-189">2048</span></span> | <span data-ttu-id="d664c-190">Это свойство — https:// URL-адрес, который указывает на пользовательский интерфейс, который будет отображаться при удалении вкладки пользователем. Это необязательное поле.</span><span class="sxs-lookup"><span data-stu-id="d664c-190">This property is the https:// URL that points to the UI to be displayed when the user deletes the tab. This is an optional field.</span></span>|

## <a name="see-also"></a><span data-ttu-id="d664c-191">См. также</span><span class="sxs-lookup"><span data-stu-id="d664c-191">See also</span></span>

* [<span data-ttu-id="d664c-192">Расширение обмена сообщениями связывает разгрузку</span><span class="sxs-lookup"><span data-stu-id="d664c-192">Messaging extensions link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="d664c-193">Teams вкладки</span><span class="sxs-lookup"><span data-stu-id="d664c-193">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="d664c-194">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="d664c-194">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
* [<span data-ttu-id="d664c-195">Создать личную вкладку</span><span class="sxs-lookup"><span data-stu-id="d664c-195">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="d664c-196">Создание вкладки канала или группы</span><span class="sxs-lookup"><span data-stu-id="d664c-196">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="d664c-197">Создать страницу контента</span><span class="sxs-lookup"><span data-stu-id="d664c-197">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="d664c-198">Создать страницу конфигурации</span><span class="sxs-lookup"><span data-stu-id="d664c-198">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="d664c-199">Создание страницы удаления для вкладки</span><span class="sxs-lookup"><span data-stu-id="d664c-199">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="d664c-200">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="d664c-200">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="d664c-201">Получение контекста для вкладки</span><span class="sxs-lookup"><span data-stu-id="d664c-201">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="d664c-202">Создание вкладок с использованием адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="d664c-202">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="d664c-203">Изменения полей вкладок</span><span class="sxs-lookup"><span data-stu-id="d664c-203">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)

## <a name="next-step"></a><span data-ttu-id="d664c-204">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="d664c-204">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d664c-205">Создание вкладок бесед</span><span class="sxs-lookup"><span data-stu-id="d664c-205">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)