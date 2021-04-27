---
title: Начало работы — создание личной вкладки
author: heath-hamilton
description: Быстро создайте личную вкладку Microsoft Teams с помощью набор средств.
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: dabe427142dd3e6a1d2f01f83601cbffd4a20dbd
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019981"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="c2538-103">Создание личной вкладки для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c2538-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="c2538-104">Вкладки — это простой способ встраить содержимое в приложение, встраив веб-страницу в Teams.</span><span class="sxs-lookup"><span data-stu-id="c2538-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="c2538-105">В Teams существует два типа вкладок.</span><span class="sxs-lookup"><span data-stu-id="c2538-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="c2538-106">В этом руководстве вы создайте основную *личную* вкладку — полноэкранную страницу контента для отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="c2538-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="c2538-107">(Личные вкладки ближе всего к традиционному веб-сайту в Teams.)</span><span class="sxs-lookup"><span data-stu-id="c2538-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c2538-108">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="c2538-108">Before you begin</span></span>

<span data-ttu-id="c2538-109">Чтобы начать работу, нужна базовая личная вкладка для запуска.</span><span class="sxs-lookup"><span data-stu-id="c2538-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="c2538-110">Если у вас его нет, см. сборку и [запуск первого приложения Teams.](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="c2538-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="c2538-111">Назначение</span><span class="sxs-lookup"><span data-stu-id="c2538-111">Your assignment</span></span>

<span data-ttu-id="c2538-112">У людей в организации возникли проблемы с поиском основных контактных данных для важных функций (службы поддержки, hr и т.д.).</span><span class="sxs-lookup"><span data-stu-id="c2538-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="c2538-113">Вы отвечаете за то, чтобы они могли быстро найти эту информацию в одном месте.</span><span class="sxs-lookup"><span data-stu-id="c2538-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="c2538-114">Как бы вы это сделать?</span><span class="sxs-lookup"><span data-stu-id="c2538-114">How would you do that?</span></span> <span data-ttu-id="c2538-115">Личная вкладка Teams, конечно.</span><span class="sxs-lookup"><span data-stu-id="c2538-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="c2538-116">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="c2538-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="c2538-117">Определите некоторые конфигурации приложений и леса, релевантные для личных вкладок</span><span class="sxs-lookup"><span data-stu-id="c2538-117">Identify some of the app configurations and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="c2538-118">Создание контента вкладок</span><span class="sxs-lookup"><span data-stu-id="c2538-118">Create tab content</span></span>
> * <span data-ttu-id="c2538-119">Обновление цветовой темы вкладки в зависимости от предпочтений пользователей</span><span class="sxs-lookup"><span data-stu-id="c2538-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="c2538-120">1. Определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="c2538-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="c2538-121">Большая часть конфигураций приложений и строительных лесов создается автоматически при создании проекта с командной набор средств.</span><span class="sxs-lookup"><span data-stu-id="c2538-121">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="c2538-122">Рассмотрим основные компоненты для создания личной вкладки.</span><span class="sxs-lookup"><span data-stu-id="c2538-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="c2538-123">Конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="c2538-123">App configurations</span></span>

<span data-ttu-id="c2538-124">В наборе инструментов перейдите в **App Studio,** чтобы просмотреть и обновить конфигурации приложений.</span><span class="sxs-lookup"><span data-stu-id="c2538-124">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="c2538-125">Строительные леса приложений</span><span class="sxs-lookup"><span data-stu-id="c2538-125">App scaffolding</span></span>

<span data-ttu-id="c2538-126">Строительные леса приложений предоставляют компоненты для отрисовки личной вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="c2538-126">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="c2538-127">Вы можете много работать, но на данный момент необходимо сосредоточиться только на следующем:</span><span class="sxs-lookup"><span data-stu-id="c2538-127">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="c2538-128">`Tab.js` файл в `src/components` каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="c2538-128">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="c2538-129">Это для отрисовки страницы контента вкладок.</span><span class="sxs-lookup"><span data-stu-id="c2538-129">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="c2538-130">Клиент Microsoft Teams JavaScript SDK, который поставляется с предварительной загрузкой в передние компоненты проекта.</span><span class="sxs-lookup"><span data-stu-id="c2538-130">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="c2538-131">2. Настройка страницы контента вкладок</span><span class="sxs-lookup"><span data-stu-id="c2538-131">2. Customize your tab content page</span></span>

<span data-ttu-id="c2538-132">Составить список важных контактов в организации.</span><span class="sxs-lookup"><span data-stu-id="c2538-132">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="c2538-133">Скопируйте и обновив следующий фрагмент с информацией, которая имеет отношение к вам, или используйте код как есть.</span><span class="sxs-lookup"><span data-stu-id="c2538-133">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="c2538-134">Перейдите в `src/components` каталог и откройте `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="c2538-134">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="c2538-135">Найдите `render()` функцию и вклейте содержимое внутри `return()` (как показано).</span><span class="sxs-lookup"><span data-stu-id="c2538-135">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="c2538-136">Добавьте следующее правило, чтобы ссылки электронной почты были проще читать независимо от `App.css` того, какая тема используется.</span><span class="sxs-lookup"><span data-stu-id="c2538-136">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="c2538-137">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="c2538-137">Save your changes.</span></span> <span data-ttu-id="c2538-138">Чтобы просмотреть новое содержимое, перейдите на вкладку приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="c2538-138">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Снимок экрана личной вкладки со статическим контентом.":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="c2538-140">3. Обновление темы вкладки</span><span class="sxs-lookup"><span data-stu-id="c2538-140">3. Update the tab theme</span></span>

<span data-ttu-id="c2538-141">Хорошие приложения считаются родными для Teams, поэтому важно, чтобы вкладка смешивается с предпочитаемой пользователями темой Teams: по умолчанию (светлая), темная или высокая контрастность.</span><span class="sxs-lookup"><span data-stu-id="c2538-141">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="c2538-142">Как вы могли заметить на последнем скриншоте, вкладка по-прежнему имеет светлый фон, когда клиент использует темную тему.</span><span class="sxs-lookup"><span data-stu-id="c2538-142">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="c2538-143">Это не рекомендуется для пользователей.</span><span class="sxs-lookup"><span data-stu-id="c2538-143">This is not a recommended user experience.</span></span>

<span data-ttu-id="c2538-144">[SDK клиента Teams JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) может сделать ваше приложение осведомленным об изменениях темы в клиенте и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="c2538-144">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="c2538-145">Давайте рассмотрим, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="c2538-145">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="c2538-146">Получить контекст о клиенте Teams</span><span class="sxs-lookup"><span data-stu-id="c2538-146">Get context about the Teams client</span></span>

<span data-ttu-id="c2538-147">В файле есть вызов, который содержит некоторые сведения о настраиваемой `Tab.js` `microsoftTeams.getContext()` [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) клиентской теме.</span><span class="sxs-lookup"><span data-stu-id="c2538-147">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="c2538-148">Благодаря строительным лесам приложений используйте этот код для доступа к интерфейсу `context` и его свойствам.</span><span class="sxs-lookup"><span data-stu-id="c2538-148">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

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

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="c2538-149">Создание обработера изменения темы</span><span class="sxs-lookup"><span data-stu-id="c2538-149">Create a theme change handler</span></span>

<span data-ttu-id="c2538-150">С свойствами в руках, ваше приложение имеет четкое представление о том, что происходит `context` вокруг него в Teams.</span><span class="sxs-lookup"><span data-stu-id="c2538-150">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="c2538-151">Но приложение по-прежнему не знает, что его внешний вид должен отражать любую тему, которая выбирает пользователь.</span><span class="sxs-lookup"><span data-stu-id="c2538-151">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="c2538-152">Для изменения состояния приложения с помощью темы необходим обработок.</span><span class="sxs-lookup"><span data-stu-id="c2538-152">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="c2538-153">Вставьте следующий обработник изменения темы сразу после `microsoftTeams.getContext()` вызова.</span><span class="sxs-lookup"><span data-stu-id="c2538-153">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="c2538-154">Совпадение стилей тем</span><span class="sxs-lookup"><span data-stu-id="c2538-154">Match theme styles</span></span>

<span data-ttu-id="c2538-155">Обработник изменения темы на месте, но вам нужен код, который отвечает на эти изменения и выравнивает цвета вкладки с текущей темой.</span><span class="sxs-lookup"><span data-stu-id="c2538-155">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="c2538-156">В следующем примере можно применить стили к вкладке. Используйте код как есть, расширите его или напишите свой собственный.</span><span class="sxs-lookup"><span data-stu-id="c2538-156">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="c2538-157">В `render()` функции сохраняется состояние, предоставленное обработить изменение темы `isTheme` в .</span><span class="sxs-lookup"><span data-stu-id="c2538-157">In the `render()` function, store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="c2538-158">После хранения состояния, предоставленного обработив изменение темы, указайте условную логику, чтобы отрисовка стилей вкладки на основе текущей темы.</span><span class="sxs-lookup"><span data-stu-id="c2538-158">After storing the state provided by the theme change handler, provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="c2538-159">В следующем примере показан базовый способ сделать это:</span><span class="sxs-lookup"><span data-stu-id="c2538-159">The following example shows a basic way to do this:</span></span>
1. <span data-ttu-id="c2538-160">Проверьте текущую тему `isTheme` в .</span><span class="sxs-lookup"><span data-stu-id="c2538-160">Check the current theme in `isTheme`.</span></span>
2. <span data-ttu-id="c2538-161">Создайте `newTheme` объект со свойствами CSS, соответствующими текущей теме.</span><span class="sxs-lookup"><span data-stu-id="c2538-161">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
3. <span data-ttu-id="c2538-162">Применение CSS к корневому элементу HTML контента вкладки ( `<div style={newTheme}>` ).</span><span class="sxs-lookup"><span data-stu-id="c2538-162">Apply the CSS to your tab content's root HTML element (`<div style={newTheme}>`).</span></span>

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

<span data-ttu-id="c2538-163">Проверьте вкладку в Teams.</span><span class="sxs-lookup"><span data-stu-id="c2538-163">Check your tab in Teams.</span></span> <span data-ttu-id="c2538-164">Внешний вид должен соответствовать темной теме.</span><span class="sxs-lookup"><span data-stu-id="c2538-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Снимок экрана личной вкладки со статическим представлением контента.":::

## <a name="well-done"></a><span data-ttu-id="c2538-166">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="c2538-166">Well done</span></span>

<span data-ttu-id="c2538-167">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="c2538-167">Congratulations!</span></span> <span data-ttu-id="c2538-168">У вас есть приложение Teams с личной вкладке, которая упрощает поиск важных контактов в организации.</span><span class="sxs-lookup"><span data-stu-id="c2538-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="c2538-169">Подробнее</span><span class="sxs-lookup"><span data-stu-id="c2538-169">Learn more</span></span>

* <span data-ttu-id="c2538-170">Следуйте [нашим рекомендациям по проектированию](../tabs/design/tabs.md) и создайте с помощью готовых к производству шаблонов [пользовательского](../concepts/design/design-teams-app-ui-templates.md) интерфейса для создания бесшовного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c2538-170">Follow our [design guidelines](../tabs/design/tabs.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* <span data-ttu-id="c2538-171">Понимание [мобильных соображений для](../tabs/design/tabs-mobile.md) вкладок.</span><span class="sxs-lookup"><span data-stu-id="c2538-171">Understand [mobile considerations](../tabs/design/tabs-mobile.md) for tabs.</span></span>
* <span data-ttu-id="c2538-172">[Добавьте проверку подлинности SSO на вкладку](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="c2538-172">[Add SSO authentication to your tab](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>
* <span data-ttu-id="c2538-173">Использование данных Teams с [помощью Microsoft Graph.](https://docs.microsoft.com/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="c2538-173">Utilize Teams data with [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>
* <span data-ttu-id="c2538-174">[Создайте вкладку без инструментария.](../tabs/quickstarts/create-personal-tab-node-yeoman.md)</span><span class="sxs-lookup"><span data-stu-id="c2538-174">[Create a tab without the toolkit](../tabs/quickstarts/create-personal-tab-node-yeoman.md).</span></span>

## <a name="next-lesson"></a><span data-ttu-id="c2538-175">Следующий урок</span><span class="sxs-lookup"><span data-stu-id="c2538-175">Next lesson</span></span>

<span data-ttu-id="c2538-176">Вы знаете, как создать вкладку для личного использования.</span><span class="sxs-lookup"><span data-stu-id="c2538-176">You know how to build a tab for personal use.</span></span> <span data-ttu-id="c2538-177">Давайте рассмотрим, что требуется для создания вкладки для каналов и чатов группы.</span><span class="sxs-lookup"><span data-stu-id="c2538-177">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c2538-178">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="c2538-178">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
