---
title: Начало работы — создание личной вкладки
author: heath-hamilton
description: Быстро создайте личную вкладку Microsoft Teams с помощью набор средств.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: 86be39503ec4e4fde5fafe63f83b3a4fb6d956bf
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797808"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="2bc7b-103">Создание личной вкладки для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2bc7b-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="2bc7b-104">Вкладки — это простой способ выставлять содержимое в приложении, встраив веб-страницу в Teams.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="2bc7b-105">В Teams существует два типа вкладок.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="2bc7b-106">В этом руководстве вы создайте базовую *личную* вкладку — полноэкранную страницу содержимого для отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="2bc7b-107">(Личные вкладки — это самое близкое к традиционному веб-сайту в Teams.)</span><span class="sxs-lookup"><span data-stu-id="2bc7b-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2bc7b-108">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="2bc7b-108">Before you begin</span></span>

<span data-ttu-id="2bc7b-109">Для начала вам потребуется базовая запущенная личная вкладка.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="2bc7b-110">Если у вас его нет, см. сборку и [запустите свое первое приложение Teams.](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="2bc7b-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="2bc7b-111">Назначение</span><span class="sxs-lookup"><span data-stu-id="2bc7b-111">Your assignment</span></span>

<span data-ttu-id="2bc7b-112">У людей в организации проблемы с поиском основных контактных данных для важных функций (службы поддержки, отдела кадров и т. д.).</span><span class="sxs-lookup"><span data-stu-id="2bc7b-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="2bc7b-113">Вы отвечаете за то, чтобы они могли быстро найти эти сведения в одном месте.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="2bc7b-114">Как это сделать?</span><span class="sxs-lookup"><span data-stu-id="2bc7b-114">How would you do that?</span></span> <span data-ttu-id="2bc7b-115">Конечно, личная вкладка Teams.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="2bc7b-116">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="2bc7b-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="2bc7b-117">Определение некоторых конфигураций приложений и скаолдинг, релевантный для личных вкладок</span><span class="sxs-lookup"><span data-stu-id="2bc7b-117">Identify some of the app configurations and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="2bc7b-118">Создание содержимого вкладок</span><span class="sxs-lookup"><span data-stu-id="2bc7b-118">Create tab content</span></span>
> * <span data-ttu-id="2bc7b-119">Обновление цветовой темы вкладки в зависимости от предпочтений пользователя</span><span class="sxs-lookup"><span data-stu-id="2bc7b-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="2bc7b-120">1. Определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="2bc7b-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="2bc7b-121">Большая часть конфигураций и скафаолдинга приложений автоматически заданная при создании проекта с помощью командной набор средств.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-121">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="2bc7b-122">Рассмотрим основные компоненты для создания личной вкладки.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="2bc7b-123">Конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="2bc7b-123">App configurations</span></span>

<span data-ttu-id="2bc7b-124">В наборе инструментов перейдите в **App Studio,** чтобы просмотреть и обновить конфигурации приложений.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-124">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="2bc7b-125">Скафаолдинг приложений</span><span class="sxs-lookup"><span data-stu-id="2bc7b-125">App scaffolding</span></span>

<span data-ttu-id="2bc7b-126">Скафолдинг приложения предоставляет компоненты для отображения личной вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-126">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="2bc7b-127">Вы можете работать с большим количеством работы, но на данный момент вам нужно сосредоточиться только на следующих темах:</span><span class="sxs-lookup"><span data-stu-id="2bc7b-127">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="2bc7b-128">`Tab.js` файл в `src/components` каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-128">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="2bc7b-129">Это для отображения страницы содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-129">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="2bc7b-130">Клиентский SDK JavaScript для Microsoft Teams, который предварительно загружается в клиентские компоненты вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-130">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="2bc7b-131">2. Настройка страницы содержимого вкладки</span><span class="sxs-lookup"><span data-stu-id="2bc7b-131">2. Customize your tab content page</span></span>

<span data-ttu-id="2bc7b-132">Скомпилировать список важных контактов в организации.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-132">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="2bc7b-133">Скопируйте и обновим следующий фрагмент с информацией, которая вам актуальна, или используйте код как есть.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-133">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

```JSX
<div>
  <h1>Important Contacts</h1>
    <ul>
      <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
      <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
      <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
    </ul>
</div>
```

<span data-ttu-id="2bc7b-134">Перейдите в `src/components` каталог и откройте `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="2bc7b-134">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="2bc7b-135">Найдите `render()` функцию и в paste содержимое `return()` внутри (как показано).</span><span class="sxs-lookup"><span data-stu-id="2bc7b-135">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

```JavaScript
render() {

    let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

    return (
    <div>
      <h1>Important Contacts</h1>
        <ul>
          <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
          <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
          <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
        </ul>
    </div>
    );
}
```

<span data-ttu-id="2bc7b-136">Добавьте следующее правило, чтобы упростить чтение ссылок электронной почты независимо от `App.css` используемой темы.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-136">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="2bc7b-137">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-137">Save your changes.</span></span> <span data-ttu-id="2bc7b-138">Перейдите на вкладку приложения в Teams, чтобы просмотреть новое содержимое.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-138">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Снимок экрана: личная вкладка со статическим содержимым.":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="2bc7b-140">3. Обновление темы вкладки</span><span class="sxs-lookup"><span data-stu-id="2bc7b-140">3. Update the tab theme</span></span>

<span data-ttu-id="2bc7b-141">Хорошие приложения, которые отлично работают с Teams, поэтому важно, чтобы ваша вкладка смешивала тему Teams, предпочитаемую вашими пользователями: по умолчанию (светлая), темная или высокая контрастность.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-141">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="2bc7b-142">Как вы могли заметить на последнем снимке экрана, при использовании клиентом темной темы на вкладке по-прежнему остается светлый фон.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-142">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="2bc7b-143">Это не рекомендуется для пользователей.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-143">This is not a recommended user experience.</span></span>

<span data-ttu-id="2bc7b-144">Клиентский [SDK JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) для Teams позволяет вашему приложению реагировать на изменения тем в клиенте.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-144">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="2bc7b-145">Рассмотрим, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-145">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="2bc7b-146">Получите контекст о клиенте Teams</span><span class="sxs-lookup"><span data-stu-id="2bc7b-146">Get context about the Teams client</span></span>

<span data-ttu-id="2bc7b-147">В файле есть вызов, который предоставляет некоторые сведения о настроенной теме `Tab.js` `microsoftTeams.getContext()` [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) клиента.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-147">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="2bc7b-148">Благодаря скафаолдингу приложения используйте этот код так же, как и для доступа к интерфейсу `context` и его свойствам.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-148">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

```JavaScript
componentDidMount(){
  // Get the user context from Teams and set it in the state
  microsoftTeams.getContext((context, error) => {
    this.setState({
      context: context
    });
  });
  // Next steps: Error handling using the error object
}
```

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="2bc7b-149">Создание обработера изменений темы</span><span class="sxs-lookup"><span data-stu-id="2bc7b-149">Create a theme change handler</span></span>

<span data-ttu-id="2bc7b-150">Благодаря свойствам в приложении вы четко понимаете, что происходит с ним `context` в Teams.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-150">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="2bc7b-151">Но приложение по-прежнему не знает, что его внешний вид должен отражать любую тему, выбираемую пользователем.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-151">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="2bc7b-152">Вам нужен обработок, чтобы состояние приложения менялось с темой.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-152">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="2bc7b-153">Вставьте следующий обработок изменения темы сразу после `microsoftTeams.getContext()` вызова.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-153">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="2bc7b-154">Соответствие стилям темы</span><span class="sxs-lookup"><span data-stu-id="2bc7b-154">Match theme styles</span></span>

<span data-ttu-id="2bc7b-155">Обработник изменений темы уже существует, но вам нужен код, который реагирует на эти изменения и выравнивает цвета вкладки с текущей темой.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-155">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="2bc7b-156">В следующем примере вы можете применять стили только к вкладке. Используйте код как есть, развяйте его или напишите свое.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-156">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="2bc7b-157">В `render()` функции сберегать состояние, предоставленное обработом изменения темы, в `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="2bc7b-157">In the `render()` function, store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="2bc7b-158">После с хранения состояния, предоставленного обработом изменения темы, предоберите условную логику для отрисовки стилей вкладки на основе текущей темы.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-158">After storing the state provided by the theme change handler, provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="2bc7b-159">В следующем примере показан базовый способ сделать это:</span><span class="sxs-lookup"><span data-stu-id="2bc7b-159">The following example shows a basic way to do this:</span></span>
1. <span data-ttu-id="2bc7b-160">Проверьте текущую тему в `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="2bc7b-160">Check the current theme in `isTheme`.</span></span>
2. <span data-ttu-id="2bc7b-161">Создайте `newTheme` объект со свойствами CSS, соответствующими текущей теме.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-161">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
3. <span data-ttu-id="2bc7b-162">Примените CSS к корневому HTML-элементу содержимого вкладки ( `<div>` ).</span><span class="sxs-lookup"><span data-stu-id="2bc7b-162">Apply the CSS to your tab content's root HTML element (`<div>`).</span></span>

```JavaScript
let newTheme

if (isTheme === "default") {
  newTheme = {
    backgroundColor: "#EEF1F5",
    color: "#16233A"
  };
} else {
  newTheme = {
    backgroundColor: "#2B2B30",
    color: "#FFFFFF"
  };
}
```

<span data-ttu-id="2bc7b-163">Проверьте вкладку в Teams.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-163">Check your tab in Teams.</span></span> <span data-ttu-id="2bc7b-164">Внешний вид должен близко соответствовать темной теме.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Снимок экрана: личная вкладка со статическим представлением содержимого.":::

## <a name="well-done"></a><span data-ttu-id="2bc7b-166">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="2bc7b-166">Well done</span></span>

<span data-ttu-id="2bc7b-167">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="2bc7b-167">Congratulations!</span></span> <span data-ttu-id="2bc7b-168">У вас есть приложение Teams с личной вкладками, которая упрощает поиск важных контактов в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="2bc7b-169">Подробнее</span><span class="sxs-lookup"><span data-stu-id="2bc7b-169">Learn more</span></span>

* <span data-ttu-id="2bc7b-170">[Проверка подлинности](../tabs/how-to/authentication/auth-aad-sso.md)пользователей вкладок с помощью единого входного набора: если вы хотите, чтобы на вкладке просматривали только авторизованные пользователи, необходимо настроить единый вход с помощью Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="2bc7b-170">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="2bc7b-171">[Встраивайте](../tabs/how-to/tab-requirements.md)содержимое из существующего веб-приложения или веб-страницы: мы показали вам, как создать новое содержимое для личной вкладки, но вы также можете загрузить содержимое с внешнего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-171">[Embed content from an existing web app or webpage](../tabs/how-to/tab-requirements.md): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="2bc7b-172">[Органично создайте вкладку:](../tabs/design/tabs.md)см. рекомендации по проектированию вкладок Teams.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-172">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="2bc7b-173">[Создание вкладок для мобильных устройств.](../tabs/design/tabs-mobile.md)В этой теме вы знаете, как разрабатывать вкладки для телефонов и планшетов.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-173">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="2bc7b-174">Использование данных Teams с Помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="2bc7b-174">Utilize Teams data with Microsoft Graph</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="2bc7b-175">Создание вкладки без наборов средств</span><span class="sxs-lookup"><span data-stu-id="2bc7b-175">Create a tab without the toolkit</span></span>](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a><span data-ttu-id="2bc7b-176">Следующий урок</span><span class="sxs-lookup"><span data-stu-id="2bc7b-176">Next lesson</span></span>

<span data-ttu-id="2bc7b-177">Вы знаете, как создать вкладку для личного использования.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-177">You know how to build a tab for personal use.</span></span> <span data-ttu-id="2bc7b-178">Рассмотрим, что требуется для создания вкладки для каналов и чатов команды.</span><span class="sxs-lookup"><span data-stu-id="2bc7b-178">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2bc7b-179">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="2bc7b-179">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
