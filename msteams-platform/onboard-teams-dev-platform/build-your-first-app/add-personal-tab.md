---
title: Создание вкладки "Личное" для Teams
author: heath-hamilton
description: Узнайте, как создать личную вкладку в первом приложении Microsoft Teams.
ms.topic: tutorial
ms.author: lajanuar
ms.date: 08/31/2020
ms.openlocfilehash: 5dbe3a8314102807992b15e34a15c23f395c4d74
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964601"
---
# <a name="create-a-personal-tab-for-teams"></a><span data-ttu-id="2892c-103">Создание вкладки "Личное" для Teams</span><span class="sxs-lookup"><span data-stu-id="2892c-103">Create a personal tab for Teams</span></span>

<span data-ttu-id="2892c-104">Вкладки — это простой способ отображения контента в приложении, по сути внедряя веб-страницу в Teams.</span><span class="sxs-lookup"><span data-stu-id="2892c-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="2892c-105">В Teams есть два типа вкладок.</span><span class="sxs-lookup"><span data-stu-id="2892c-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="2892c-106">В этом руководстве вы создадите базовую *вкладку личное*, страницу содержимого на полном экране для отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="2892c-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="2892c-107">(Личные вкладки — это ближайшее к традиционному интерфейсу веб-сайта в Teams.)</span><span class="sxs-lookup"><span data-stu-id="2892c-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2892c-108">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="2892c-108">Before you begin</span></span>

<span data-ttu-id="2892c-109">Для начала необходимо создать базовую вкладку выполнение личных настроек.</span><span class="sxs-lookup"><span data-stu-id="2892c-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="2892c-110">Если у вас его нет, ознакомьтесь [со статьей Создание и запуск первого приложения Teams](../build-your-first-app/build-and-run.md).</span><span class="sxs-lookup"><span data-stu-id="2892c-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="2892c-111">Ваше назначение</span><span class="sxs-lookup"><span data-stu-id="2892c-111">Your assignment</span></span>

<span data-ttu-id="2892c-112">Сотрудникам Организации не удается найти основные контактные данные для важных функций (служба технической поддержки, HR и т. д.).</span><span class="sxs-lookup"><span data-stu-id="2892c-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="2892c-113">Вы следите за тем, чтобы они могли быстро найти эту информацию в одном месте.</span><span class="sxs-lookup"><span data-stu-id="2892c-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="2892c-114">Как это сделать?</span><span class="sxs-lookup"><span data-stu-id="2892c-114">How would you do that?</span></span> <span data-ttu-id="2892c-115">Разумеется, личная вкладка группы Teams.</span><span class="sxs-lookup"><span data-stu-id="2892c-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="2892c-116">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="2892c-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="2892c-117">Определение свойств манифеста приложения и формирование шаблонов, относящихся к личным вкладкам</span><span class="sxs-lookup"><span data-stu-id="2892c-117">Identify the app manifest properties and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="2892c-118">Создание содержимого вкладки</span><span class="sxs-lookup"><span data-stu-id="2892c-118">Create tab content</span></span>
> * <span data-ttu-id="2892c-119">Обновление темы цвета вкладки в соответствии с предпочтениями пользователя</span><span class="sxs-lookup"><span data-stu-id="2892c-119">Update a tab's color theme based on user preference</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="2892c-120">Определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="2892c-120">Identify relevant app project components</span></span>

<span data-ttu-id="2892c-121">Большинство манифестов и шаблонов приложений настраиваются автоматически при создании проекта с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="2892c-121">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="2892c-122">Рассмотрим основные компоненты для создания вкладки личных сведений.</span><span class="sxs-lookup"><span data-stu-id="2892c-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="2892c-123">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="2892c-123">App manifest</span></span>

<span data-ttu-id="2892c-124">Показан следующий фрагмент манифеста приложения ( `manifest.json` файл в `.publish` каталоге проекта) [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs) , который включает свойства и значения по умолчанию, относящиеся к личным вкладкам.</span><span class="sxs-lookup"><span data-stu-id="2892c-124">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs), which includes properties and default values relevant to personal tabs.</span></span>

```JSON
    "staticTabs": [
        {
            "entityId": "index",
            "name": "Personal Tab",
            "contentUrl": "{baseUrl0}/tab",
            "scopes": [ "personal" ]
        }
    ],
```

* <span data-ttu-id="2892c-125">`entityId`: Уникальный идентификатор страницы, отображаемой на вкладке.</span><span class="sxs-lookup"><span data-stu-id="2892c-125">`entityId`: A unique identifier for the page displayed by the tab.</span></span>
* <span data-ttu-id="2892c-126">`name`: Отображаемое имя вкладки (например, "My Contacts").</span><span class="sxs-lookup"><span data-stu-id="2892c-126">`name`: The tab's display name (for example, "My Contacts").</span></span>
* <span data-ttu-id="2892c-127">`contentUrl`: URL-адрес узла страница содержимого вкладки (должна быть HTTPS).</span><span class="sxs-lookup"><span data-stu-id="2892c-127">`contentUrl`: The host URL the tab content page (must be HTTPS).</span></span>
* <span data-ttu-id="2892c-128">`scopes`: Указывает, что вкладка предназначена только для личного пользования.</span><span class="sxs-lookup"><span data-stu-id="2892c-128">`scopes`: Specifies the tab is for personal use only.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="2892c-129">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="2892c-129">App scaffolding</span></span>

<span data-ttu-id="2892c-130">Формирование шаблонов приложений предоставляет компоненты для отображения вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="2892c-130">The app scaffolding provides the components for rendering your tab in Teams.</span></span> <span data-ttu-id="2892c-131">Существует множество способов, с которыми вы можете работать, но теперь вам нужно сосредоточиться на следующих задачах:</span><span class="sxs-lookup"><span data-stu-id="2892c-131">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="2892c-132">`Tab.js` файл в `src/components` каталоге проекта</span><span class="sxs-lookup"><span data-stu-id="2892c-132">`Tab.js` file in the `src/components` directory of your project</span></span>
* <span data-ttu-id="2892c-133">Клиентский пакет SDK Microsoft Teams JavaScript, который предварительно загружен в интерфейсных компонентах проекта.</span><span class="sxs-lookup"><span data-stu-id="2892c-133">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components</span></span>

## <a name="create-your-tab-content"></a><span data-ttu-id="2892c-134">Создание содержимого вкладки</span><span class="sxs-lookup"><span data-stu-id="2892c-134">Create your tab content</span></span>

<span data-ttu-id="2892c-135">Скомпилируйте список важных контактов в Организации.</span><span class="sxs-lookup"><span data-stu-id="2892c-135">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="2892c-136">Скопируйте и обновите следующий фрагмент кода со сведениями, важными для вас или, в целях простоты, используйте код как есть.</span><span class="sxs-lookup"><span data-stu-id="2892c-136">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="2892c-137">Перейдите в `src/components` каталог и откройте его `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="2892c-137">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="2892c-138">Нахождение `render()` функции и вставка содержимого внутри `return()` (как показано на рисунке).</span><span class="sxs-lookup"><span data-stu-id="2892c-138">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="2892c-139">Добавьте следующее правило, чтобы `App.css` ссылки электронной почты легче читались независимо от того, какая тема используется.</span><span class="sxs-lookup"><span data-stu-id="2892c-139">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
  a {
    color: inherit;
  }
```

<span data-ttu-id="2892c-140">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="2892c-140">Save your changes.</span></span> <span data-ttu-id="2892c-141">Перейдите на вкладку приложения в Teams, чтобы просмотреть новый контент.</span><span class="sxs-lookup"><span data-stu-id="2892c-141">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../doc-links/images/personal-tab-tutorial-content.png" alt-text="Пример снимка экрана личной вкладки со статическим содержимым.":::

## <a name="update-the-tab-theme"></a><span data-ttu-id="2892c-143">Обновление темы вкладки</span><span class="sxs-lookup"><span data-stu-id="2892c-143">Update the tab theme</span></span>

<span data-ttu-id="2892c-144">Хорошие приложения в Teams встроены в Teams, поэтому для вкладок важна тема, в которую пользователи предпочитают: по умолчанию (Light), темный или High контрастность.</span><span class="sxs-lookup"><span data-stu-id="2892c-144">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="2892c-145">Как вы могли заметить на последнем снимке экрана, вкладка по-прежнему имеет светлый фон, когда клиент использует темную тему.</span><span class="sxs-lookup"><span data-stu-id="2892c-145">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="2892c-146">Это не рекомендуемый пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="2892c-146">This is not a recommended user experience.</span></span>

<span data-ttu-id="2892c-147">[Пакет SDK для Teams JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) может сделать ваше приложение осведомленным об изменениях темы в клиенте и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="2892c-147">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="2892c-148">Давайте разберем, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="2892c-148">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="2892c-149">Получение контекста о клиенте Teams</span><span class="sxs-lookup"><span data-stu-id="2892c-149">Get context about the Teams client</span></span>

<span data-ttu-id="2892c-150">В `Tab.js` файле существует `microsoftTeams.getContext()` вызов, который предоставляет некоторые сведения [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) о настроенной клиентской теме (помимо других сведений).</span><span class="sxs-lookup"><span data-stu-id="2892c-150">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="2892c-151">Благодаря формированию шаблонов приложений используйте этот код, чтобы получить доступ к `context` интерфейсу и его свойствам.</span><span class="sxs-lookup"><span data-stu-id="2892c-151">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

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

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="2892c-152">Создание обработчика изменений темы</span><span class="sxs-lookup"><span data-stu-id="2892c-152">Create a theme change handler</span></span>

<span data-ttu-id="2892c-153">Если у `context` вас есть свойства в наличии, ваше приложение имеет твердое представление о происходящих в Teams.</span><span class="sxs-lookup"><span data-stu-id="2892c-153">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="2892c-154">Но приложение по-прежнему не знает, что его внешний вид должен отражать любую тему, которую выбрал пользователь.</span><span class="sxs-lookup"><span data-stu-id="2892c-154">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="2892c-155">Необходимо обработчик, чтобы изменить состояние приложения с помощью темы.</span><span class="sxs-lookup"><span data-stu-id="2892c-155">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="2892c-156">Вставьте следующий обработчик изменений темы сразу после `microsoftTeams.getContext()` вызова.</span><span class="sxs-lookup"><span data-stu-id="2892c-156">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="2892c-157">Сравнение стилей темы</span><span class="sxs-lookup"><span data-stu-id="2892c-157">Match theme styles</span></span>

<span data-ttu-id="2892c-158">Ваш обработчик изменений темы размещается, но вам необходим код, который реагирует на эти изменения и выравнивает цвета вкладки с помощью текущей темы.</span><span class="sxs-lookup"><span data-stu-id="2892c-158">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="2892c-159">Приведенный ниже пример можно использовать только один из способов применения стилей к вкладке. Используйте код как есть, разверните его или напишите собственное.</span><span class="sxs-lookup"><span data-stu-id="2892c-159">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="2892c-160">Сохраните состояние, предоставленное обработчиком изменений темы, в файле `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="2892c-160">Store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="2892c-161">Предоставляет некоторую условную логику для отображения стилей вкладок на основе текущей темы.</span><span class="sxs-lookup"><span data-stu-id="2892c-161">Provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="2892c-162">В следующем примере показан простой способ, выполняемый на 1) при проверке текущей темы в `isTheme` , 2) создание `newTheme` объекта со свойствами CSS, относящимися к текущей теме, и 3) применение CSS к корневому элементу HTML содержимого вкладки ( `<div>` ).</span><span class="sxs-lookup"><span data-stu-id="2892c-162">The following example shows a basic way to do this by 1) checking the current theme in `isTheme`, 2) creating a `newTheme` object with CSS properties relevant to the current theme, and 3) applying the CSS to your tab content's root HTML element (`<div>`).</span></span>

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

<span data-ttu-id="2892c-163">Проверьте вкладку в Teams.</span><span class="sxs-lookup"><span data-stu-id="2892c-163">Check your tab in Teams.</span></span> <span data-ttu-id="2892c-164">Внешний вид должен точно соответствовать темной теме.</span><span class="sxs-lookup"><span data-stu-id="2892c-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../doc-links/images/personal-tab-tutorial-updated-theme.png" alt-text="Пример снимка экрана личной вкладки со статическим содержимым.":::

## <a name="well-done"></a><span data-ttu-id="2892c-166">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="2892c-166">Well done</span></span>

<span data-ttu-id="2892c-167">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="2892c-167">Congratulations!</span></span> <span data-ttu-id="2892c-168">У вас есть приложение Teams со вкладкой "личные", которая упрощает поиск важных контактов в Организации.</span><span class="sxs-lookup"><span data-stu-id="2892c-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="2892c-169">Подробнее</span><span class="sxs-lookup"><span data-stu-id="2892c-169">Learn more</span></span>

* <span data-ttu-id="2892c-170">[Проверка подлинности пользователей вкладки с единым входом](../../tabs/how-to/authentication/auth-aad-sso.md): Если вы хотите, чтобы авторизованные пользователи просматривали вкладку, настройте единый вход (SSO) через Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="2892c-170">[Authenticate tab users with SSO](../../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="2892c-171">[Внедрение контента из существующего веб-приложения или веб-страницы](../../tabs/how-to/add-tab.md#tab-requirements): мы показали, как создать новое содержимое для вкладки личных данных, но вы также можете загрузить контент с внешнего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="2892c-171">[Embed content from an existing web app or webpage](../../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="2892c-172">[Создайте простой интерфейс для вкладки](../../tabs/design/tabs.md): Ознакомьтесь с рекомендациями по проектированию вкладок Teams.</span><span class="sxs-lookup"><span data-stu-id="2892c-172">[Create a seamless experience for your tab](../../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="2892c-173">[Создание вкладок для мобильных устройств](../../tabs/design/tabs-mobile.md): Узнайте, как создавать вкладки для телефонов и планшетов.</span><span class="sxs-lookup"><span data-stu-id="2892c-173">[Build tabs for mobile](../../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>

## <a name="next-lesson"></a><span data-ttu-id="2892c-174">Следующий урок</span><span class="sxs-lookup"><span data-stu-id="2892c-174">Next lesson</span></span>

<span data-ttu-id="2892c-175">Вы знаете, как создать вкладку для личного использования.</span><span class="sxs-lookup"><span data-stu-id="2892c-175">You know how to build a tab for personal use.</span></span> <span data-ttu-id="2892c-176">Рассмотрим, что требуется для создания вкладки для каналов команд и чатов.</span><span class="sxs-lookup"><span data-stu-id="2892c-176">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2892c-177">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="2892c-177">Build a channel tab</span></span>](../build-your-first-app/add-channel-tab.md)
