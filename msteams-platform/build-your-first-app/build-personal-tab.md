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
# <a name="build-a-personal-tab-for-microsoft-teams"></a>Создание личной вкладки для Microsoft Teams

Вкладки — это простой способ встраить содержимое в приложение, встраив веб-страницу в Teams.

В Teams существует два типа вкладок. В этом руководстве вы создайте основную *личную* вкладку — полноэкранную страницу контента для отдельных пользователей. (Личные вкладки ближе всего к традиционному веб-сайту в Teams.)

## <a name="before-you-begin"></a>Прежде чем начать

Чтобы начать работу, нужна базовая личная вкладка для запуска. Если у вас его нет, см. сборку и [запуск первого приложения Teams.](../build-your-first-app/build-and-run.md)

## <a name="your-assignment"></a>Назначение

У людей в организации возникли проблемы с поиском основных контактных данных для важных функций (службы поддержки, hr и т.д.). Вы отвечаете за то, чтобы они могли быстро найти эту информацию в одном месте. Как бы вы это сделать? Личная вкладка Teams, конечно.

## <a name="what-youll-learn"></a>Что вы узнаете

> [!div class="checklist"]
>
> * Определите некоторые конфигурации приложений и леса, релевантные для личных вкладок
> * Создание контента вкладок
> * Обновление цветовой темы вкладки в зависимости от предпочтений пользователей

## <a name="1-identify-relevant-app-project-components"></a>1. Определение соответствующих компонентов проекта приложения

Большая часть конфигураций приложений и строительных лесов создается автоматически при создании проекта с командной набор средств. Рассмотрим основные компоненты для создания личной вкладки.

### <a name="app-configurations"></a>Конфигурации приложений

В наборе инструментов перейдите в **App Studio,** чтобы просмотреть и обновить конфигурации приложений.

### <a name="app-scaffolding"></a>Строительные леса приложений

Строительные леса приложений предоставляют компоненты для отрисовки личной вкладки в Teams. Вы можете много работать, но на данный момент необходимо сосредоточиться только на следующем:

* `Tab.js` файл в `src/components` каталоге проекта. Это для отрисовки страницы контента вкладок.
* Клиент Microsoft Teams JavaScript SDK, который поставляется с предварительной загрузкой в передние компоненты проекта.

## <a name="2-customize-your-tab-content-page"></a>2. Настройка страницы контента вкладок

Составить список важных контактов в организации. Скопируйте и обновив следующий фрагмент с информацией, которая имеет отношение к вам, или используйте код как есть.

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

Перейдите в `src/components` каталог и откройте `Tab.js` . Найдите `render()` функцию и вклейте содержимое внутри `return()` (как показано).

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

Добавьте следующее правило, чтобы ссылки электронной почты были проще читать независимо от `App.css` того, какая тема используется.

```CSS
a {
  color: inherit;
}
```

Сохраните изменения. Чтобы просмотреть новое содержимое, перейдите на вкладку приложения в Teams.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Снимок экрана личной вкладки со статическим контентом.":::

## <a name="3-update-the-tab-theme"></a>3. Обновление темы вкладки

Хорошие приложения считаются родными для Teams, поэтому важно, чтобы вкладка смешивается с предпочитаемой пользователями темой Teams: по умолчанию (светлая), темная или высокая контрастность. Как вы могли заметить на последнем скриншоте, вкладка по-прежнему имеет светлый фон, когда клиент использует темную тему. Это не рекомендуется для пользователей.

[SDK клиента Teams JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) может сделать ваше приложение осведомленным об изменениях темы в клиенте и реагировать на них. Давайте рассмотрим, как это сделать.

### <a name="get-context-about-the-teams-client"></a>Получить контекст о клиенте Teams

В файле есть вызов, который содержит некоторые сведения о настраиваемой `Tab.js` `microsoftTeams.getContext()` [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) клиентской теме. Благодаря строительным лесам приложений используйте этот код для доступа к интерфейсу `context` и его свойствам.

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

### <a name="create-a-theme-change-handler"></a>Создание обработера изменения темы

С свойствами в руках, ваше приложение имеет четкое представление о том, что происходит `context` вокруг него в Teams. Но приложение по-прежнему не знает, что его внешний вид должен отражать любую тему, которая выбирает пользователь.

Для изменения состояния приложения с помощью темы необходим обработок. Вставьте следующий обработник изменения темы сразу после `microsoftTeams.getContext()` вызова.

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>Совпадение стилей тем

Обработник изменения темы на месте, но вам нужен код, который отвечает на эти изменения и выравнивает цвета вкладки с текущей темой.

> [!NOTE]
> В следующем примере можно применить стили к вкладке. Используйте код как есть, расширите его или напишите свой собственный.

В `render()` функции сохраняется состояние, предоставленное обработить изменение темы `isTheme` в .

```JavaScript
  const isTheme = this.state.theme
```

После хранения состояния, предоставленного обработив изменение темы, указайте условную логику, чтобы отрисовка стилей вкладки на основе текущей темы. В следующем примере показан базовый способ сделать это:
1. Проверьте текущую тему `isTheme` в .
2. Создайте `newTheme` объект со свойствами CSS, соответствующими текущей теме.
3. Применение CSS к корневому элементу HTML контента вкладки ( `<div style={newTheme}>` ).

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

Проверьте вкладку в Teams. Внешний вид должен соответствовать темной теме.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Снимок экрана личной вкладки со статическим представлением контента.":::

## <a name="well-done"></a>Прекрасно

Поздравляем! У вас есть приложение Teams с личной вкладке, которая упрощает поиск важных контактов в организации.

## <a name="learn-more"></a>Подробнее

* Следуйте [нашим рекомендациям по проектированию](../tabs/design/tabs.md) и создайте с помощью готовых к производству шаблонов [пользовательского](../concepts/design/design-teams-app-ui-templates.md) интерфейса для создания бесшовного интерфейса.
* Понимание [мобильных соображений для](../tabs/design/tabs-mobile.md) вкладок.
* [Добавьте проверку подлинности SSO на вкладку](../tabs/how-to/authentication/auth-aad-sso.md).
* Использование данных Teams с [помощью Microsoft Graph.](https://docs.microsoft.com/graph/teams-concept-overview)
* [Создайте вкладку без инструментария.](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-lesson"></a>Следующий урок

Вы знаете, как создать вкладку для личного использования. Давайте рассмотрим, что требуется для создания вкладки для каналов и чатов группы.

> [!div class="nextstepaction"]
> [Создание вкладки канала](../build-your-first-app/build-channel-tab.md)
