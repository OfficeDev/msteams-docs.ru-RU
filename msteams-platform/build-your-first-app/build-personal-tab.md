---
title: Начало работы — Создание вкладки "Личное"
author: heath-hamilton
description: Быстрое создание личной вкладки Microsoft Teams с помощью набора инструментов Microsoft Teams.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: 89d9a2109a863402dd7641d0882c530a0c2e6f66
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409073"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="751c4-103">Создание вкладки "Личное" для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="751c4-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="751c4-104">Вкладки — это простой способ отображения контента в приложении, по сути внедряя веб-страницу в Teams.</span><span class="sxs-lookup"><span data-stu-id="751c4-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="751c4-105">В Teams есть два типа вкладок.</span><span class="sxs-lookup"><span data-stu-id="751c4-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="751c4-106">В этом руководстве вы создадите базовую *вкладку личное*, страницу содержимого на полном экране для отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="751c4-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="751c4-107">(Личные вкладки — это ближайшее к традиционному интерфейсу веб-сайта в Teams.)</span><span class="sxs-lookup"><span data-stu-id="751c4-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="751c4-108">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="751c4-108">Before you begin</span></span>

<span data-ttu-id="751c4-109">Для начала необходимо создать базовую вкладку выполнение личных настроек.</span><span class="sxs-lookup"><span data-stu-id="751c4-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="751c4-110">Если у вас его нет, ознакомьтесь [со статьей Создание и запуск первого приложения Teams](../build-your-first-app/build-and-run.md).</span><span class="sxs-lookup"><span data-stu-id="751c4-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="751c4-111">Ваше назначение</span><span class="sxs-lookup"><span data-stu-id="751c4-111">Your assignment</span></span>

<span data-ttu-id="751c4-112">Сотрудникам Организации не удается найти основные контактные данные для важных функций (служба технической поддержки, HR и т. д.).</span><span class="sxs-lookup"><span data-stu-id="751c4-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="751c4-113">Вы следите за тем, чтобы они могли быстро найти эту информацию в одном месте.</span><span class="sxs-lookup"><span data-stu-id="751c4-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="751c4-114">Как это сделать?</span><span class="sxs-lookup"><span data-stu-id="751c4-114">How would you do that?</span></span> <span data-ttu-id="751c4-115">Разумеется, личная вкладка группы Teams.</span><span class="sxs-lookup"><span data-stu-id="751c4-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="751c4-116">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="751c4-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="751c4-117">Определите некоторые конфигурации приложений и формирование шаблонов, относящихся к личным вкладкам.</span><span class="sxs-lookup"><span data-stu-id="751c4-117">Identify some of the app configurations and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="751c4-118">Создание содержимого вкладки</span><span class="sxs-lookup"><span data-stu-id="751c4-118">Create tab content</span></span>
> * <span data-ttu-id="751c4-119">Обновление темы цвета вкладки в соответствии с предпочтениями пользователя</span><span class="sxs-lookup"><span data-stu-id="751c4-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="751c4-120">1. определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="751c4-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="751c4-121">Многие конфигурации приложений и формирование шаблонов настраиваются автоматически при создании проекта с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="751c4-121">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="751c4-122">Рассмотрим основные компоненты для создания вкладки личных сведений.</span><span class="sxs-lookup"><span data-stu-id="751c4-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="751c4-123">Конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="751c4-123">App configurations</span></span>

<span data-ttu-id="751c4-124">Вы можете просматривать и обновлять конфигурации приложений с помощью App Studio, которая включена в набор средств.</span><span class="sxs-lookup"><span data-stu-id="751c4-124">You can view and update your app configurations using App Studio, which is included in the toolkit.</span></span>

<span data-ttu-id="751c4-125">Во время установки набор инструментов изначально настроил страницу контент вкладки, на которой отображается основной контент.</span><span class="sxs-lookup"><span data-stu-id="751c4-125">During setup, the toolkit initially configured your tab content page, which is where you display your primary content.</span></span> <span data-ttu-id="751c4-126">В наборе инструментов откройте **Приложение App Studio** и выберите **вкладки** , чтобы просмотреть конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="751c4-126">In the toolkit, go to **App Studio** and select **Tabs** to see the configuration.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="751c4-127">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="751c4-127">App scaffolding</span></span>

<span data-ttu-id="751c4-128">Формирование шаблонов приложений предоставляет компоненты для отображения вкладки "личные сведения" в Teams.</span><span class="sxs-lookup"><span data-stu-id="751c4-128">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="751c4-129">Существует множество способов, с которыми вы можете работать, но теперь вам нужно сосредоточиться на следующих задачах:</span><span class="sxs-lookup"><span data-stu-id="751c4-129">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="751c4-130">`Tab.js` файл в `src/components` каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="751c4-130">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="751c4-131">Это предназначено для отображения страницы содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="751c4-131">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="751c4-132">Клиентский пакет SDK Microsoft Teams JavaScript, который предварительно загружен в интерфейсных компонентах проекта.</span><span class="sxs-lookup"><span data-stu-id="751c4-132">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="751c4-133">2. Настройка страницы контента вкладки</span><span class="sxs-lookup"><span data-stu-id="751c4-133">2. Customize your tab content page</span></span>

<span data-ttu-id="751c4-134">Скомпилируйте список важных контактов в Организации.</span><span class="sxs-lookup"><span data-stu-id="751c4-134">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="751c4-135">Скопируйте и обновите следующий фрагмент кода со сведениями, важными для вас или, в целях простоты, используйте код как есть.</span><span class="sxs-lookup"><span data-stu-id="751c4-135">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="751c4-136">Перейдите в `src/components` каталог и откройте его `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="751c4-136">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="751c4-137">Нахождение `render()` функции и вставка содержимого внутри `return()` (как показано на рисунке).</span><span class="sxs-lookup"><span data-stu-id="751c4-137">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="751c4-138">Добавьте следующее правило, чтобы `App.css` ссылки электронной почты легче читались независимо от того, какая тема используется.</span><span class="sxs-lookup"><span data-stu-id="751c4-138">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="751c4-139">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="751c4-139">Save your changes.</span></span> <span data-ttu-id="751c4-140">Перейдите на вкладку приложения в Teams, чтобы просмотреть новый контент.</span><span class="sxs-lookup"><span data-stu-id="751c4-140">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Снимок экрана: личная вкладка со статическим содержимым.":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="751c4-142">3. Обновление темы вкладки</span><span class="sxs-lookup"><span data-stu-id="751c4-142">3. Update the tab theme</span></span>

<span data-ttu-id="751c4-143">Хорошие приложения в Teams встроены в Teams, поэтому для вкладок важна тема, в которую пользователи предпочитают: по умолчанию (Light), темный или High контрастность.</span><span class="sxs-lookup"><span data-stu-id="751c4-143">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="751c4-144">Как вы могли заметить на последнем снимке экрана, вкладка по-прежнему имеет светлый фон, когда клиент использует темную тему.</span><span class="sxs-lookup"><span data-stu-id="751c4-144">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="751c4-145">Это не рекомендуемый пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="751c4-145">This is not a recommended user experience.</span></span>

<span data-ttu-id="751c4-146">[Пакет SDK для Teams JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) может сделать ваше приложение осведомленным об изменениях темы в клиенте и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="751c4-146">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="751c4-147">Давайте разберем, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="751c4-147">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="751c4-148">Получение контекста о клиенте Teams</span><span class="sxs-lookup"><span data-stu-id="751c4-148">Get context about the Teams client</span></span>

<span data-ttu-id="751c4-149">В `Tab.js` файле существует `microsoftTeams.getContext()` вызов, который предоставляет некоторые сведения [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) о настроенной клиентской теме (помимо других сведений).</span><span class="sxs-lookup"><span data-stu-id="751c4-149">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="751c4-150">Благодаря формированию шаблонов приложений используйте этот код, чтобы получить доступ к `context` интерфейсу и его свойствам.</span><span class="sxs-lookup"><span data-stu-id="751c4-150">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

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

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="751c4-151">Создание обработчика изменений темы</span><span class="sxs-lookup"><span data-stu-id="751c4-151">Create a theme change handler</span></span>

<span data-ttu-id="751c4-152">Если у `context` вас есть свойства в наличии, ваше приложение имеет твердое представление о происходящих в Teams.</span><span class="sxs-lookup"><span data-stu-id="751c4-152">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="751c4-153">Но приложение по-прежнему не знает, что его внешний вид должен отражать любую тему, которую выбрал пользователь.</span><span class="sxs-lookup"><span data-stu-id="751c4-153">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="751c4-154">Необходимо обработчик, чтобы изменить состояние приложения с помощью темы.</span><span class="sxs-lookup"><span data-stu-id="751c4-154">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="751c4-155">Вставьте следующий обработчик изменений темы сразу после `microsoftTeams.getContext()` вызова.</span><span class="sxs-lookup"><span data-stu-id="751c4-155">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="751c4-156">Сравнение стилей темы</span><span class="sxs-lookup"><span data-stu-id="751c4-156">Match theme styles</span></span>

<span data-ttu-id="751c4-157">Ваш обработчик изменений темы размещается, но вам необходим код, который реагирует на эти изменения и выравнивает цвета вкладки с помощью текущей темы.</span><span class="sxs-lookup"><span data-stu-id="751c4-157">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="751c4-158">Приведенный ниже пример можно использовать только один из способов применения стилей к вкладке. Используйте код как есть, разверните его или напишите собственное.</span><span class="sxs-lookup"><span data-stu-id="751c4-158">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="751c4-159">Сохраните состояние, предоставленное обработчиком изменений темы, в файле `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="751c4-159">Store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="751c4-160">Предоставляет некоторую условную логику для отображения стилей вкладок на основе текущей темы.</span><span class="sxs-lookup"><span data-stu-id="751c4-160">Provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="751c4-161">В следующем примере показан простой способ, выполняемый на 1) при проверке текущей темы в `isTheme` , 2) создание `newTheme` объекта со свойствами CSS, относящимися к текущей теме, и 3) применение CSS к корневому элементу HTML содержимого вкладки ( `<div>` ).</span><span class="sxs-lookup"><span data-stu-id="751c4-161">The following example shows a basic way to do this by 1) checking the current theme in `isTheme`, 2) creating a `newTheme` object with CSS properties relevant to the current theme, and 3) applying the CSS to your tab content's root HTML element (`<div>`).</span></span>

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

<span data-ttu-id="751c4-162">Проверьте вкладку в Teams.</span><span class="sxs-lookup"><span data-stu-id="751c4-162">Check your tab in Teams.</span></span> <span data-ttu-id="751c4-163">Внешний вид должен точно соответствовать темной теме.</span><span class="sxs-lookup"><span data-stu-id="751c4-163">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Снимок экрана со вкладкой &quot;Личное&quot; и представлением статического содержимого.":::

## <a name="well-done"></a><span data-ttu-id="751c4-165">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="751c4-165">Well done</span></span>

<span data-ttu-id="751c4-166">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="751c4-166">Congratulations!</span></span> <span data-ttu-id="751c4-167">У вас есть приложение Teams со вкладкой "личные", которая упрощает поиск важных контактов в Организации.</span><span class="sxs-lookup"><span data-stu-id="751c4-167">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="751c4-168">Подробнее</span><span class="sxs-lookup"><span data-stu-id="751c4-168">Learn more</span></span>

* <span data-ttu-id="751c4-169">[Проверка подлинности пользователей вкладки с единым входом](../tabs/how-to/authentication/auth-aad-sso.md): Если вы хотите, чтобы авторизованные пользователи просматривали вкладку, настройте единый вход (SSO) через Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="751c4-169">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="751c4-170">[Внедрение контента из существующего веб-приложения или веб-страницы](../tabs/how-to/add-tab.md#tab-requirements): мы показали, как создать новое содержимое для вкладки личных данных, но вы также можете загрузить контент с внешнего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="751c4-170">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="751c4-171">[Создайте простой интерфейс для вкладки](../tabs/design/tabs.md): Ознакомьтесь с рекомендациями по проектированию вкладок Teams.</span><span class="sxs-lookup"><span data-stu-id="751c4-171">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="751c4-172">[Создание вкладок для мобильных устройств](../tabs/design/tabs-mobile.md): Узнайте, как создавать вкладки для телефонов и планшетов.</span><span class="sxs-lookup"><span data-stu-id="751c4-172">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="751c4-173">Использование данных Teams с API Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="751c4-173">Utilize Teams data with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="751c4-174">Создание вкладки без набора инструментов</span><span class="sxs-lookup"><span data-stu-id="751c4-174">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="751c4-175">Следующий урок</span><span class="sxs-lookup"><span data-stu-id="751c4-175">Next lesson</span></span>

<span data-ttu-id="751c4-176">Вы знаете, как создать вкладку для личного использования.</span><span class="sxs-lookup"><span data-stu-id="751c4-176">You know how to build a tab for personal use.</span></span> <span data-ttu-id="751c4-177">Рассмотрим, что требуется для создания вкладки для каналов команд и чатов.</span><span class="sxs-lookup"><span data-stu-id="751c4-177">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="751c4-178">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="751c4-178">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
