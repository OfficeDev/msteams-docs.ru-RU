---
title: Использование библиотеки элементов управления
description: Использование библиотеки элементов управления, предоставляемой Microsoft Teams App Studio
keywords: Библиотека элементов управления Teams Studio App
ms.openlocfilehash: d817f55bd75216f77375b7848c5c32cbd29304c2
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675288"
---
# <a name="using-the-control-library-in-app-studio"></a><span data-ttu-id="e0c20-104">Использование библиотеки элементов управления в App Studio</span><span class="sxs-lookup"><span data-stu-id="e0c20-104">Using the control library in App Studio</span></span>

<span data-ttu-id="e0c20-105">[Приложение Microsoft Teams Studio](~/get-started/get-started-app-studio.md) предоставляет набор элементов управления, которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="e0c20-105">[Microsoft Teams App Studio](~/get-started/get-started-app-studio.md) provides you with a set of controls that you can use in your own apps.</span></span> <span data-ttu-id="e0c20-106">Эти элементы управления представлены на вкладке *Библиотека управления* в App Studio.</span><span class="sxs-lookup"><span data-stu-id="e0c20-106">These controls are provided in the *Control Library* tab of App Studio.</span></span>

<span data-ttu-id="e0c20-107">Эти элементы управления были созданы разработчиками Microsoft Teams для упрощения собственных рабочих процессов, стандартизации управления поведением и поддержки используемых по умолчанию тем для групп.</span><span class="sxs-lookup"><span data-stu-id="e0c20-107">These controls were created by the Microsoft Teams designers to streamline their own workflows, standardize control behavior and support Team's default themes.</span></span> <span data-ttu-id="e0c20-108">Вы можете использовать эту библиотеку в собственных приложениях для достижения единообразия внешнего вида и поведения.</span><span class="sxs-lookup"><span data-stu-id="e0c20-108">You can use this library in your own apps to achieve a unified look and feel.</span></span>

<span data-ttu-id="e0c20-109">Элементы управления включают:</span><span class="sxs-lookup"><span data-stu-id="e0c20-109">Controls include:</span></span>

* <span data-ttu-id="e0c20-110">Кнопки</span><span class="sxs-lookup"><span data-stu-id="e0c20-110">Buttons</span></span>
* <span data-ttu-id="e0c20-111">Раскрывающихся меню</span><span class="sxs-lookup"><span data-stu-id="e0c20-111">Dropdowns</span></span>
* <span data-ttu-id="e0c20-112">Флажков</span><span class="sxs-lookup"><span data-stu-id="e0c20-112">Checkboxes</span></span>
* <span data-ttu-id="e0c20-113">Переключатели</span><span class="sxs-lookup"><span data-stu-id="e0c20-113">Radio Buttons</span></span>
* <span data-ttu-id="e0c20-114">Включает</span><span class="sxs-lookup"><span data-stu-id="e0c20-114">Toggles</span></span>
* <span data-ttu-id="e0c20-115">Тестовые области</span><span class="sxs-lookup"><span data-stu-id="e0c20-115">Test Areas</span></span>
* <span data-ttu-id="e0c20-116">Ссылки</span><span class="sxs-lookup"><span data-stu-id="e0c20-116">Links</span></span>
* <span data-ttu-id="e0c20-117">Вкладки</span><span class="sxs-lookup"><span data-stu-id="e0c20-117">Tabs</span></span>
* <span data-ttu-id="e0c20-118">Таблицы</span><span class="sxs-lookup"><span data-stu-id="e0c20-118">Tables</span></span>
* <span data-ttu-id="e0c20-119">Значки</span><span class="sxs-lookup"><span data-stu-id="e0c20-119">Icons</span></span>

## <a name="optionally-use-react-controls"></a><span data-ttu-id="e0c20-120">При необходимости используйте элементы управления "реагирует"</span><span class="sxs-lookup"><span data-stu-id="e0c20-120">Optionally use React controls</span></span>

<span data-ttu-id="e0c20-121">В полной библиотеке управления Teams используется [платформа отклика JavaScript UI Framework](https://reactjs.org/) , однако она создается таким образом, что она не привязана к определенной платформе пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e0c20-121">The full Teams control library uses the [React JavaScript UI framework](https://reactjs.org/) however it is built so that it is not tied to a specific UI framework.</span></span> <span data-ttu-id="e0c20-122">Существует четыре разных пакета NPM:</span><span class="sxs-lookup"><span data-stu-id="e0c20-122">There are four different npm packages:</span></span>

* <span data-ttu-id="e0c20-123">**мстеамс — стили пользовательского интерфейса — основные компоненты** Основные стили CSS компонентов пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e0c20-123">**msteams-ui-styles-core** The core CSS styles of UI components.</span></span> <span data-ttu-id="e0c20-124">Он не зависит от любой платформы пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e0c20-124">It’s independent of any UI framework.</span></span>
* <span data-ttu-id="e0c20-125">**мстеамс — значки пользовательского интерфейса — Core** Основной набор значков Teams.</span><span class="sxs-lookup"><span data-stu-id="e0c20-125">**msteams-ui-icons-core** The core set of Teams icons.</span></span>
* <span data-ttu-id="e0c20-126">**мстеамс – UI – компоненты — реагируть** Библиотека привязки "реакция".</span><span class="sxs-lookup"><span data-stu-id="e0c20-126">**msteams-ui-components-react** The React binding library.</span></span> <span data-ttu-id="e0c20-127">Он зависит от мстеамс – UI – Styles — Core.</span><span class="sxs-lookup"><span data-stu-id="e0c20-127">It depends on msteams-ui-styles-core.</span></span>
* <span data-ttu-id="e0c20-128">**мстеамс — значки пользовательского интерфейса — Реагируйте** Библиотека привязки "реакция" для набора значков Teams.</span><span class="sxs-lookup"><span data-stu-id="e0c20-128">**msteams-ui-icons-react** The React binding library for the set of Teams icons.</span></span> <span data-ttu-id="e0c20-129">Он зависит от мстеамс – UI – значки — Core.</span><span class="sxs-lookup"><span data-stu-id="e0c20-129">It depends on msteams-ui-icons-core.</span></span>

<span data-ttu-id="e0c20-130">Эти библиотеки имеют открытый источник, и вы можете использовать мстеамс – UI – Styles — Core и мстеамс – UI – значки — Core без реакции.</span><span class="sxs-lookup"><span data-stu-id="e0c20-130">These libraries are all open source, and you can use msteams-ui-styles-core and msteams-ui-icons-core without React.</span></span>

## <a name="adding-the-control-library"></a><span data-ttu-id="e0c20-131">Добавление библиотеки элементов управления</span><span class="sxs-lookup"><span data-stu-id="e0c20-131">Adding the control library</span></span>

<span data-ttu-id="e0c20-132">Установите библиотеку элемента управления и ее зависимость от `typestyle`ее узла:</span><span class="sxs-lookup"><span data-stu-id="e0c20-132">Install the control library and its peer dependency `typestyle`:</span></span>

```terminal
npm install --save typestyle && npm install --save msteams-ui-components-react
```

<span data-ttu-id="e0c20-133">*Необязательно:* Установите значки Teams.</span><span class="sxs-lookup"><span data-stu-id="e0c20-133">*Optional:* Install the Teams icons.</span></span>

```terminal
npm install --save msteams-ui-icons-react
```

<span data-ttu-id="e0c20-134">Найдите и откройте `src/App.js` и замените его содержимое приведенным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="e0c20-134">Find and open `src/App.js` and replace its content with following code:</span></span>

```javascript
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, PrimaryButton } from ‘msteams-ui-components-react’

class App extends Component {
   render() {
      // Sets up the top-level context for the library. It accepts global
      // configurations such as font size and theme. fontSize is your page’s
      // default font size. We made it a parameter so that you could use this
      // library with CSS frameworks such as Bootstrap. Some CSS frameworks
      // set the default font size for the page; retrieve it and use it
      // instead of {16} in the block.
      // This library uses the power of CSS to do most of the work for you.
      // Instead of passing themes as a parameter to every UI component,
      // we set it on a parent HTML element. All HTML elements nested within
      // that parent will inherit these properties.

      return (
        <TeamsComponentContext
            fontSize={16}
            theme={ThemeStyle.Light}
        />
      );
   }
}
export default App;
```

<span data-ttu-id="e0c20-135">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="e0c20-135">Run the app</span></span>

```terminal
npm run start
```

<span data-ttu-id="e0c20-136">При переходе на http://localhost:3000экран вы увидите следующий экран:</span><span class="sxs-lookup"><span data-stu-id="e0c20-136">When you navigate to http://localhost:3000, you should see the following screen:</span></span>

<img width="530px" src="~/assets/images/get-started/control-library-button.png" title="Кнопка "Библиотека элемента управления""/>

## <a name="dynamically-handling-theme-changes"></a><span data-ttu-id="e0c20-138">Динамическая обработка изменений тем</span><span class="sxs-lookup"><span data-stu-id="e0c20-138">Dynamically handling theme changes</span></span>

<span data-ttu-id="e0c20-139">Ваше приложение должно обрабатывать темы в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="e0c20-139">Your app needs to handle themes when:</span></span>

* <span data-ttu-id="e0c20-140">Начальная загрузка вкладки</span><span class="sxs-lookup"><span data-stu-id="e0c20-140">The tab is initially loaded</span></span>
* <span data-ttu-id="e0c20-141">Пользователь изменяет тему после того, как вкладка уже загружена</span><span class="sxs-lookup"><span data-stu-id="e0c20-141">A user changes the theme after the tab is already loaded</span></span>

<span data-ttu-id="e0c20-142">Тема включается в [контекст](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest)вкладки, который можно извлечь перед загрузкой вкладки через заполнители URL-адресов или в любой момент с помощью [пакета SDK Microsoft Teams JavaScript](/javascript/api/%40microsoft/teams-js/context).</span><span class="sxs-lookup"><span data-stu-id="e0c20-142">The theme is included in a tab’s [Context](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest), which can be retrieved before the tab is loaded via URL placeholder values, or at any time by using the [Microsoft Teams JavaScript client SDK](/javascript/api/%40microsoft/teams-js/context).</span></span>

<span data-ttu-id="e0c20-143">Способ получения текущей темы и реагирование на изменения темы описывается здесь: [Получение контекста для вкладки Microsoft Teams](~/concepts/tabs/tabs-context.md).</span><span class="sxs-lookup"><span data-stu-id="e0c20-143">How the current theme is retrieved and how to respond to theme changes is discussed here: [Get context for your Microsoft Teams tab](~/concepts/tabs/tabs-context.md).</span></span>

<span data-ttu-id="e0c20-144">В этом примере кода показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="e0c20-144">This sample code shows how this is done.</span></span>

```js
componentWillMount() {
    // If you are deploying your site as a MS Teams static or configurable tab,
    // you should add “?theme={theme}” to your tabs URL in the manifest.
    // That way you will get the current theme before it’s loaded; getContext()
    // is called only after the tab is loaded, which will cause the tab to flash
    // if the current theme is different than the default.
    this.updateTheme(this.getQueryVariable('theme'));
    this.setState({
        fontSize: this.pageFontSize(),
    });

    // If you are not using the MS Teams Javascript SDK, you can remove this entire
    // if block, but if you want theme changes in the MS Teams client to propagate
    // to the tab, leave it here.
    microsoftTeams.initialize();
    microsoftTeams.registerOnThemeChangeHandler(this.updateTheme);
}
```

## <a name="connect-your-own-component-to-the-teamscomponentcontext"></a><span data-ttu-id="e0c20-145">Подключение собственного компонента к Теамскомпонентконтекст</span><span class="sxs-lookup"><span data-stu-id="e0c20-145">Connect your own component to the TeamsComponentContext</span></span>

<span data-ttu-id="e0c20-146">Если вы хотите использовать собственный код CSS, вы по-прежнему можете отвечать на изменения темы и использовать цвета, определенные в Teams.</span><span class="sxs-lookup"><span data-stu-id="e0c20-146">If you want to use your own CSS code you can still respond to theme changes and use colors defined by teams.</span></span> <span data-ttu-id="e0c20-147">Теамскомпонентконтекст позволяет сделать это.</span><span class="sxs-lookup"><span data-stu-id="e0c20-147">TeamsComponentContext allows you to do this.</span></span>

<span data-ttu-id="e0c20-148">После этого измените `src/App.js` файл и замените его содержимое следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="e0c20-148">Once again, edit your `src/App.js` file and replace its content with following code:</span></span>

```javascript
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, ConnectedComponent } from ‘msteams-ui-components-react’

class App extends Component {
    render() {
        return (
            <TeamsComponentContext
                fontSize={16}
                theme={ThemeStyle.HighContrast}>
                <MyComponent />
            </TeamsComponentContext>
        );
    }
}

class MyComponent extends Component {
    render() {
        return (
            <ConnectedComponent render={(props) => {
                const context = props.context;

                switch (context.style) {
                case ThemeStyle.Dark:
                    return <div style={{ color: context.colors.dark.brand00 }}>Dark theme!</div>;
                case ThemeStyle.HighContrast:
                    return <div style={{ color: context.colors.highContrast.black }}>High Contrast theme!</div>;
                case ThemeStyle.Light:
                    return <div style={{ color: context.colors.light.brand00 }}>Light theme!</div>;
                }
            }} />
        );
    }
}

export default App;
```

<span data-ttu-id="e0c20-149">В этом коде новый компонент определен с именем MyComponent.</span><span class="sxs-lookup"><span data-stu-id="e0c20-149">In this code, a new component is defined called MyComponent.</span></span> <span data-ttu-id="e0c20-150">Затем добавляется специальный компонент из библиотеки элементов управления с именем Коннектедкомпонент.</span><span class="sxs-lookup"><span data-stu-id="e0c20-150">Then a special component from the control library called ConnectedComponent is added.</span></span> <span data-ttu-id="e0c20-151">Коннектедкомпонент имеет свойство, вызванное `render` , которое принимает функцию в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="e0c20-151">ConnectedComponent has a property called `render` which takes a function as a parameter.</span></span> <span data-ttu-id="e0c20-152">Во время отображения эта функция будет вызываться с соответствующим контекстом для вкладки. Контекст включает тему, в которой выполняется визуализация страницы, а также глобальный объект Color, который можно использовать для применения цветов Teams к вкладке. Как видно из `switch` оператора, подходящее `<div>` значение выбирается в зависимости от темы.</span><span class="sxs-lookup"><span data-stu-id="e0c20-152">At render time this function will be called with the appropriate context for your tab. The context includes the theme that the page is being rendered in as well as the global color object that you can use to apply Teams colors to your tab. As you can see in the `switch` statement, the appropriate `<div>` is chosen based on the theme.</span></span>

<span data-ttu-id="e0c20-153">Чтобы изменить темы, необходимо передать корневой Теамскомпонентконтекст другую тему.</span><span class="sxs-lookup"><span data-stu-id="e0c20-153">To change themes, we need to pass the root-level TeamsComponentContext a different theme.</span></span> <span data-ttu-id="e0c20-154">Когда тема изменяется, все дочерние элементы, обтекаемые в Коннектедкомпонент, будут повторно отрисованы.</span><span class="sxs-lookup"><span data-stu-id="e0c20-154">When a theme changes, all the child elements wrapped in ConnectedComponent will be re-rendered.</span></span> <span data-ttu-id="e0c20-155">В предыдущем разделе "динамическое изменение темы". "</span><span class="sxs-lookup"><span data-stu-id="e0c20-155">See previous section “Dynamically Handle Theme Changes.”</span></span>

<span data-ttu-id="e0c20-156">Существуют и другие способы подключения компонента к Теамскомпонентконтекст.</span><span class="sxs-lookup"><span data-stu-id="e0c20-156">There are other ways to connect your component to TeamsComponentContext.</span></span> <span data-ttu-id="e0c20-157">Если вы знакомы с [редукс](https://redux.js.org/basics/usage-with-react), вы можете предпочесть следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="e0c20-157">If you’re familiar with [Redux](https://redux.js.org/basics/usage-with-react), you may prefer the following pattern:</span></span>

```js
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, connectTeamsComponent } from ‘msteams-ui-components-react’

class App extends Component {
    render() {
        return (
            <TeamsComponentContext
                fontSize={16}
                theme={ThemeStyle.HighContrast}>
                <MyComponent />
            </TeamsComponentContext>
        );
    }
}

class MyComponentInner extends Component {
    render() {
        const context = this.props.context;
        switch (context.style) {
            case ThemeStyle.Dark:
                return <div style={{ color: context.colors.dark.brand00 }}>Dark theme!</div>;
            case ThemeStyle.HighContrast:
                return <div style={{ color: context.colors.highContrast.black }}>High Contrast theme!</div>;
            case ThemeStyle.Light:
                return <div style={{ color: context.colors.light.brand00 }}>Light theme!</div>;
        }
    }
}

const MyComponent = connectTeamsComponent(MyComponentInner);

export default App;
```

<span data-ttu-id="e0c20-158">В этом методе вместо использования Коннектедкомпонент используется функция Коннекттеамскомпонент.</span><span class="sxs-lookup"><span data-stu-id="e0c20-158">In this method, instead of using ConnectedComponent, you use the connectTeamsComponent function.</span></span> <span data-ttu-id="e0c20-159">Функция Коннекттеамскомпонент принимает текущий компонент и возвращает новый компонент с добавленным объектом context.</span><span class="sxs-lookup"><span data-stu-id="e0c20-159">The connectTeamsComponent function takes your current component and returns a new component with the context object injected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0c20-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0c20-160">Next steps</span></span>

<span data-ttu-id="e0c20-161">Зайдите в Team Studio App Studio и ознакомьтесь со всеми предлагаемыми элементами управления и примерами кода, в которых их можно использовать.</span><span class="sxs-lookup"><span data-stu-id="e0c20-161">Head to Teams App Studio and check out all the controls we offer and sample code of how to use them.</span></span> <span data-ttu-id="e0c20-162">Не забудьте изучить их в разных темах.</span><span class="sxs-lookup"><span data-stu-id="e0c20-162">Don’t forget to explore them in different themes.</span></span>