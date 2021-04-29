---
title: Начало работы — создание личной вкладки
author: girliemac
description: Быстро создайте личную вкладку Microsoft Teams с помощью набор средств.
ms.author: timura
ms.date: 03/16/2020
ms.topic: tutorial
ms.openlocfilehash: 05ef9913e338a54c7e6ebc301825b27d4bec9705
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068587"
---
# <a name="build-a-basic-personal-tab-for-microsoft-teams"></a><span data-ttu-id="dee87-103">Создание базовой личной вкладки для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dee87-103">Build a basic personal tab for Microsoft Teams</span></span>

<span data-ttu-id="dee87-104">В этом руководстве рассказывается о создании базовой личной вкладки в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="dee87-104">This tutorial teaches you to build a basic personal tab in Microsoft Teams.</span></span> <span data-ttu-id="dee87-105">Вкладки — это простой способ получения сведений в приложении путем размещения веб-контента в Teams.</span><span class="sxs-lookup"><span data-stu-id="dee87-105">Tabs are a simple way to surface information in your app by hosting web content in Teams.</span></span> <span data-ttu-id="dee87-106">Вкладки — это общая функция личных приложений, которые предоставляют личное рабочее пространство для отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="dee87-106">Tabs are a common feature of personal apps that provide a private workspace for individual users.</span></span> <span data-ttu-id="dee87-107">Личные вкладки ближе всего к традиционному веб-опыту в Teams.</span><span class="sxs-lookup"><span data-stu-id="dee87-107">Personal tabs are the closest thing to a traditional web experience in Teams.</span></span> 

## <a name="what-youll-learn"></a><span data-ttu-id="dee87-108">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="dee87-108">What you'll learn</span></span>

* <span data-ttu-id="dee87-109">Понимание конфигураций приложений и строительных лесов, соответствующих личным вкладкам.</span><span class="sxs-lookup"><span data-stu-id="dee87-109">Understand the app configurations and scaffolding relevant to personal tabs.</span></span>
* <span data-ttu-id="dee87-110">Создание контента вкладки со списком контактов организации.</span><span class="sxs-lookup"><span data-stu-id="dee87-110">Create a tab content with a contact list of your organization.</span></span>
* <span data-ttu-id="dee87-111">Обновление цветовой темы вкладки с учетом предпочтений пользователей.</span><span class="sxs-lookup"><span data-stu-id="dee87-111">Update a tab's color theme based on user preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dee87-112">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="dee87-112">Prerequisites</span></span>

<span data-ttu-id="dee87-113">Убедитесь, что вы понимаете, как настроить и создать простое приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="dee87-113">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="dee87-114">Дополнительные сведения см. в [вашем первом приложении Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="dee87-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-understand-your-app-project-components"></a><span data-ttu-id="dee87-115">1. Понимание компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="dee87-115">1. Understand your app project components</span></span>

<span data-ttu-id="dee87-116">После создания базовой личной вкладки созданный эшафот приложения предоставляет компоненты для отрисовки личной вкладки в Teams.</span><span class="sxs-lookup"><span data-stu-id="dee87-116">After you have created a basic personal tab, the generated app scaffold provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="dee87-117">Вы можете много работать, но сейчас давайте сосредоточимся на следующем:</span><span class="sxs-lookup"><span data-stu-id="dee87-117">There's a lot you can work with, but for now let us focus on the following:</span></span> 

* <span data-ttu-id="dee87-118">`Tab.js` файл в `src/components` каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="dee87-118">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="dee87-119">Это для отрисовки страницы контента вкладок.</span><span class="sxs-lookup"><span data-stu-id="dee87-119">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="dee87-120">Клиент Microsoft Teams JavaScript SDK, предварительно загруженный в компоненты переднего компонента проекта.</span><span class="sxs-lookup"><span data-stu-id="dee87-120">Microsoft Teams JavaScript client SDK, which is pre-loaded in your project's front-end components.</span></span>

<span data-ttu-id="dee87-121">Как вы можете заметить из раздела в верхней части файла, пример кода использует React — библиотеку JavaScript с открытым исходным кодом для создания `import` `Tabs.js` пользовательского интерфейса. [](https://reactjs.org/)</span><span class="sxs-lookup"><span data-stu-id="dee87-121">As you may notice from the `import` section at the top of `Tabs.js` file, the sample code uses [React](https://reactjs.org/), an open-source JavaScript library for building user-interface.</span></span> 

> [!NOTE]
> <span data-ttu-id="dee87-122">Хотя использование React _не требуется_ для разработки Teams, этот учебник учит вас с React.</span><span class="sxs-lookup"><span data-stu-id="dee87-122">Although using React is _not_ required for Teams development, this tutorial teaches you with React.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="dee87-123">2. Настройка страницы контента вкладок</span><span class="sxs-lookup"><span data-stu-id="dee87-123">2. Customize your tab content page</span></span>

<span data-ttu-id="dee87-124">Вы можете настроить страницу контента вкладок для отображения списка важных контактов в организации.</span><span class="sxs-lookup"><span data-stu-id="dee87-124">You can customize your tab content page to render a list of important contacts in your organization.</span></span> 

<span data-ttu-id="dee87-125">**Настройка страницы контента вкладок**</span><span class="sxs-lookup"><span data-stu-id="dee87-125">**To customize your tab content page**</span></span>

1. <span data-ttu-id="dee87-126">Скопируйте и измените следующий пример кода с помощью соответствующих сведений.</span><span class="sxs-lookup"><span data-stu-id="dee87-126">Copy and modify the following code sample with information that's relevant to you.</span></span> <span data-ttu-id="dee87-127">Код также можно использовать так:</span><span class="sxs-lookup"><span data-stu-id="dee87-127">You can also use the code as is:</span></span> 
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
1. <span data-ttu-id="dee87-128">Добрался до `src/components` каталога и открыл `Tab.js` файл.</span><span class="sxs-lookup"><span data-stu-id="dee87-128">Got to the `src/components` directory and open the `Tab.js` file.</span></span> 
1. <span data-ttu-id="dee87-129">Перейдите `render()` и замените код шаблона измененным кодом `return()` внутри, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="dee87-129">Go to `render()` and replace the template code with the modified code inside `return()` as shown in the following example:</span></span>
    ```JavaScript
    render() {
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
1. <span data-ttu-id="dee87-130">Перейдите в каталог и измените файл со следующим кодом, чтобы облегчить чтение ссылок электронной почты с помощью любой `src/components` `App.css` используемой темы:</span><span class="sxs-lookup"><span data-stu-id="dee87-130">Go to the `src/components` directory and modify the `App.css` file with the following code to make the email links easier to read with any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```
1. <span data-ttu-id="dee87-131">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="dee87-131">Save your changes.</span></span> 

   <span data-ttu-id="dee87-132">Новое содержимое можно просмотреть на вкладке приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="dee87-132">You can view the new content in your app's tab in Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-content.png" alt-text="Снимок экрана личной вкладки со статическим контентом.":::

## <a name="3-update-your-tab-theme"></a><span data-ttu-id="dee87-134">3. Обновление темы вкладки</span><span class="sxs-lookup"><span data-stu-id="dee87-134">3. Update your tab theme</span></span>

<span data-ttu-id="dee87-135">Важно, чтобы в вкладке была тема, которая является родным для Teams.</span><span class="sxs-lookup"><span data-stu-id="dee87-135">It is important for your tab to have a theme that feels native to Teams.</span></span> <span data-ttu-id="dee87-136">Вкладку необходимо смешать с темой Teams.</span><span class="sxs-lookup"><span data-stu-id="dee87-136">You must blend your tab with the Teams theme.</span></span> <span data-ttu-id="dee87-137">Обычно пользователи предпочитают темы по умолчанию (светлые), темные или высококонтрентные.</span><span class="sxs-lookup"><span data-stu-id="dee87-137">Your users generally prefer default (light), dark, or high contrast themes.</span></span> <span data-ttu-id="dee87-138">Как вы могли заметить на последнем скриншоте, вкладка по-прежнему имеет светлый фон, когда пользователь использует темную тему.</span><span class="sxs-lookup"><span data-stu-id="dee87-138">As you might have noticed in the last screenshot, your tab still has a light background when your user is using the dark theme.</span></span> <span data-ttu-id="dee87-139">Это не рекомендуется для пользователей.</span><span class="sxs-lookup"><span data-stu-id="dee87-139">This is not a recommended user experience.</span></span>

<span data-ttu-id="dee87-140">SDK клиента Teams JavaScript может сделать ваше приложение осведомленным об изменениях темы в клиенте и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="dee87-140">The Teams JavaScript client SDK can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="dee87-141">Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="dee87-141">To do this, follow these steps:</span></span>

1. <span data-ttu-id="dee87-142">**Получите контекст для настраиваемой клиентской темы Teams** Вызов в файле содержит определенный контекст настроенной клиентской темы `microsoftTeams.getContext()` `Tab.js` (например, темная тема).</span><span class="sxs-lookup"><span data-stu-id="dee87-142">**Get context about the configured Teams client theme** The `microsoftTeams.getContext()` call in your `Tab.js` file, provides some context about the configured client theme (such as dark theme).</span></span> <span data-ttu-id="dee87-143">Следующий код имеет доступ к `context` интерфейсу и его свойствам:</span><span class="sxs-lookup"><span data-stu-id="dee87-143">The following code accesses the `context` interface and its properties:</span></span>

    ```JavaScript
    componentDidMount(){
      // Get the user context from Teams and set it in the state
      microsoftTeams.getContext((context, error) => {
        this.setState({
          context: context,
          theme: context.theme
        });
      });
    }
    ```
1. <span data-ttu-id="dee87-144">**Создание обработера изменения темы** С свойствами в руках, ваше приложение имеет четкое представление о том, что происходит `context` вокруг него в Teams.</span><span class="sxs-lookup"><span data-stu-id="dee87-144">**Create a theme change handler** With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="dee87-145">Однако при обновлении пользователя у приложения по-прежнему нет внешнего вида, отражающий тему.</span><span class="sxs-lookup"><span data-stu-id="dee87-145">However, the app still doesn't have an appearance reflecting the theme when a user updates it.</span></span>

   <span data-ttu-id="dee87-146">Чтобы обновить состояние приложения с помощью темы, необходим обработок.</span><span class="sxs-lookup"><span data-stu-id="dee87-146">You need a handler to update your app's state with the theme.</span></span> <span data-ttu-id="dee87-147">Чтобы создать обработник, вставьте следующий обработник изменения темы сразу после `microsoftTeams.getContext()` вызова:</span><span class="sxs-lookup"><span data-stu-id="dee87-147">To create a handler, insert the following theme change handler immediately after the `microsoftTeams.getContext()` call:</span></span>

    ```JavaScript
    microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.context.theme) {
    this.setState({
      context: {
      ...this.state.context,
      theme
      }
      })   
      }
    });
      ```
1. <span data-ttu-id="dee87-148">**Соответствие стилям темы** Однако обработник изменения темы должен реагировать на изменения и выравнивать цвета вкладки с текущей темой.</span><span class="sxs-lookup"><span data-stu-id="dee87-148">**Match the theme styles** Your theme change handler is in place, however, you still have to respond to changes and align your tab's colors with the current theme.</span></span>

   <span data-ttu-id="dee87-149">В этой `render()` функции храните состояние, предоставленное обработить изменение темы `isTheme` в:</span><span class="sxs-lookup"><span data-stu-id="dee87-149">In the `render()` function, store the state provided by the theme change handler in `isTheme`:</span></span>

    ```JavaScript
      const isTheme = this.state.context.theme
    ```
    
    > [!NOTE]
    > <span data-ttu-id="dee87-150">В этом примере можно применить стили к вкладке. Используйте код как есть, расширите его или напишите свой собственный.</span><span class="sxs-lookup"><span data-stu-id="dee87-150">This example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

    <span data-ttu-id="dee87-151">После хранения состояния, предоставленного обработив изменение темы, указайте условную логику для отображения стилей вкладки на основе текущей темы.</span><span class="sxs-lookup"><span data-stu-id="dee87-151">After storing the state provided by the theme change handler, provide the conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="dee87-152">В следующем примере показан базовый способ сделать это:</span><span class="sxs-lookup"><span data-stu-id="dee87-152">The following example shows a basic way to do this:</span></span>

    1. <span data-ttu-id="dee87-153">Перейдите `render()` и проверьте текущую тему в `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="dee87-153">Go to `render()` and check the current theme in `isTheme`.</span></span>
    1. <span data-ttu-id="dee87-154">Создайте `newTheme` объект со свойствами CSS, соответствующими текущей теме.</span><span class="sxs-lookup"><span data-stu-id="dee87-154">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
    1. <span data-ttu-id="dee87-155">Применить следующий CSS к корневому элементу HTML контента вкладки `<div style={newTheme}>` ():</span><span class="sxs-lookup"><span data-stu-id="dee87-155">Apply the following CSS to your tab content's root HTML element (`<div style={newTheme}>`):</span></span>

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

       <span data-ttu-id="dee87-156">Проверьте вкладку в Teams.</span><span class="sxs-lookup"><span data-stu-id="dee87-156">Check your tab in Teams.</span></span> <span data-ttu-id="dee87-157">Внешний вид теперь тесно совпадает с темной темой.</span><span class="sxs-lookup"><span data-stu-id="dee87-157">The appearance now closely matches the dark theme.</span></span>

       :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-updated-theme.png" alt-text="Снимок экрана личной вкладки со статическим представлением контента.":::

## <a name="see-also"></a><span data-ttu-id="dee87-159">См. также</span><span class="sxs-lookup"><span data-stu-id="dee87-159">See also</span></span>

* [<span data-ttu-id="dee87-160">Клиентский SDK JavaScript для Teams</span><span class="sxs-lookup"><span data-stu-id="dee87-160">Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="dee87-161">Разработка вкладки для настольных и веб-страниц Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dee87-161">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="dee87-162">Интерфейс контекста</span><span class="sxs-lookup"><span data-stu-id="dee87-162">Context interface</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="dee87-163">Разработка приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="dee87-163">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="dee87-164">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="dee87-164">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="dee87-165">Поддержка единого входного знака (SSO) для вкладок</span><span class="sxs-lookup"><span data-stu-id="dee87-165">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="dee87-166">Обзор API Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dee87-166">Microsoft Teams API overview</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="dee87-167">Создание настраиваемой личной вкладки с Node.js и генератором Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dee87-167">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="dee87-168">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="dee87-168">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dee87-169">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="dee87-169">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)