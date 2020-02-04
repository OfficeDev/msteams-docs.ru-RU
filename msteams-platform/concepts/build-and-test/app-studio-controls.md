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
# <a name="using-the-control-library-in-app-studio"></a>Использование библиотеки элементов управления в App Studio

[Приложение Microsoft Teams Studio](~/get-started/get-started-app-studio.md) предоставляет набор элементов управления, которые можно использовать в своих приложениях. Эти элементы управления представлены на вкладке *Библиотека управления* в App Studio.

Эти элементы управления были созданы разработчиками Microsoft Teams для упрощения собственных рабочих процессов, стандартизации управления поведением и поддержки используемых по умолчанию тем для групп. Вы можете использовать эту библиотеку в собственных приложениях для достижения единообразия внешнего вида и поведения.

Элементы управления включают:

* Кнопки
* Раскрывающихся меню
* Флажков
* Переключатели
* Включает
* Тестовые области
* Ссылки
* Вкладки
* Таблицы
* Значки

## <a name="optionally-use-react-controls"></a>При необходимости используйте элементы управления "реагирует"

В полной библиотеке управления Teams используется [платформа отклика JavaScript UI Framework](https://reactjs.org/) , однако она создается таким образом, что она не привязана к определенной платформе пользовательского интерфейса. Существует четыре разных пакета NPM:

* **мстеамс — стили пользовательского интерфейса — основные компоненты** Основные стили CSS компонентов пользовательского интерфейса. Он не зависит от любой платформы пользовательского интерфейса.
* **мстеамс — значки пользовательского интерфейса — Core** Основной набор значков Teams.
* **мстеамс – UI – компоненты — реагируть** Библиотека привязки "реакция". Он зависит от мстеамс – UI – Styles — Core.
* **мстеамс — значки пользовательского интерфейса — Реагируйте** Библиотека привязки "реакция" для набора значков Teams. Он зависит от мстеамс – UI – значки — Core.

Эти библиотеки имеют открытый источник, и вы можете использовать мстеамс – UI – Styles — Core и мстеамс – UI – значки — Core без реакции.

## <a name="adding-the-control-library"></a>Добавление библиотеки элементов управления

Установите библиотеку элемента управления и ее зависимость от `typestyle`ее узла:

```terminal
npm install --save typestyle && npm install --save msteams-ui-components-react
```

*Необязательно:* Установите значки Teams.

```terminal
npm install --save msteams-ui-icons-react
```

Найдите и откройте `src/App.js` и замените его содержимое приведенным ниже кодом.

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

Запуск приложения

```terminal
npm run start
```

При переходе на http://localhost:3000экран вы увидите следующий экран:

<img width="530px" src="~/assets/images/get-started/control-library-button.png" title="Кнопка "Библиотека элемента управления""/>

## <a name="dynamically-handling-theme-changes"></a>Динамическая обработка изменений тем

Ваше приложение должно обрабатывать темы в следующих случаях:

* Начальная загрузка вкладки
* Пользователь изменяет тему после того, как вкладка уже загружена

Тема включается в [контекст](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest)вкладки, который можно извлечь перед загрузкой вкладки через заполнители URL-адресов или в любой момент с помощью [пакета SDK Microsoft Teams JavaScript](/javascript/api/%40microsoft/teams-js/context).

Способ получения текущей темы и реагирование на изменения темы описывается здесь: [Получение контекста для вкладки Microsoft Teams](~/concepts/tabs/tabs-context.md).

В этом примере кода показано, как это сделать.

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

## <a name="connect-your-own-component-to-the-teamscomponentcontext"></a>Подключение собственного компонента к Теамскомпонентконтекст

Если вы хотите использовать собственный код CSS, вы по-прежнему можете отвечать на изменения темы и использовать цвета, определенные в Teams. Теамскомпонентконтекст позволяет сделать это.

После этого измените `src/App.js` файл и замените его содержимое следующим кодом:

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

В этом коде новый компонент определен с именем MyComponent. Затем добавляется специальный компонент из библиотеки элементов управления с именем Коннектедкомпонент. Коннектедкомпонент имеет свойство, вызванное `render` , которое принимает функцию в качестве параметра. Во время отображения эта функция будет вызываться с соответствующим контекстом для вкладки. Контекст включает тему, в которой выполняется визуализация страницы, а также глобальный объект Color, который можно использовать для применения цветов Teams к вкладке. Как видно из `switch` оператора, подходящее `<div>` значение выбирается в зависимости от темы.

Чтобы изменить темы, необходимо передать корневой Теамскомпонентконтекст другую тему. Когда тема изменяется, все дочерние элементы, обтекаемые в Коннектедкомпонент, будут повторно отрисованы. В предыдущем разделе "динамическое изменение темы". "

Существуют и другие способы подключения компонента к Теамскомпонентконтекст. Если вы знакомы с [редукс](https://redux.js.org/basics/usage-with-react), вы можете предпочесть следующий шаблон:

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

В этом методе вместо использования Коннектедкомпонент используется функция Коннекттеамскомпонент. Функция Коннекттеамскомпонент принимает текущий компонент и возвращает новый компонент с добавленным объектом context.

## <a name="next-steps"></a>Дальнейшие действия

Зайдите в Team Studio App Studio и ознакомьтесь со всеми предлагаемыми элементами управления и примерами кода, в которых их можно использовать. Не забудьте изучить их в разных темах.